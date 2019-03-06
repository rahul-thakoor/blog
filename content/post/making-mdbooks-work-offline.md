---
title: "Making mdBooks work offline"
date: 2019-03-04T18:06:48+04:00
image: /img/mdbook_offline_new_version_prompt.png
tags:
- rust
- mdbook
- web
layout: post
description: Use workbox to cache your mdBook contents 
externalLink: false
---

`mdBook`[^mdbook] is a great utility to create online books from Markdown files. It is used extensively in the Rust community. Here are some books made with `mdBook`:
    
- The Rust Programming Language (_"the book"_)[^thebook]
- Embedded Book [^embedded]
- mdBook user guide[^mdbook_user_guide]


## Motivation

- I usually read the books while commuting and this usually consumes mobile data. Given the contents don't change that often, I thought it would be useful if they were cached. 
- Prevent the dreaded _"no internet connection"_ screen (downasaur). 
- I want to eventually convert an `mdBook` into a PWA[^pwa]. Offline support is important for reliability.

## Google Workbox

A service worker[^sw] is responsible for caching and retrieving resources from the cache (among other things). Google's Workbox[^wb] _is a library that bakes in a set of best practices and removes the boilerplate every developer writes when working with service workers._ It allows us to precache assets, and also cache assets at runtime. There are several caching strategies[^strategies] which can be selected depending on your specific use-case.

## Customising the mdBook
I followed Google's workbox codelab[^codelab] and modified the steps accordingly. mdBook allows us to add additional javascript via the `additional-js` option in `book.toml`. We need to add a service worker registration code in the template page:

````js
// source: https://codelabs.developers.google.com/codelabs/workbox-lab/#2
  if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => {
      navigator.serviceWorker.register('sw.js')
        .then(registration => {
          console.log(`Service Worker registered! Scope: ${registration.scope}`);
        })
        .catch(err => {
          console.log(`Service Worker registration failed: ${err}`);
        });
    })
  }
````
The code attempts to install a service worker(`sw.js`)

We can save the above code in a file, `register-sw.js` and save it at the root level of the book. Then in `book.toml` add the following:

```toml
[output.html]
additional-js=["register-sw.js"]
```

Next I created a basic service worker file(`sw.js`) at the root level of the book.

````js
// source: https://codelabs.developers.google.com/codelabs/workbox-lab/#3
importScripts('https://storage.googleapis.com/workbox-cdn/releases/3.5.0/workbox-sw.js');

if (workbox) {
  console.log(`Yay! Workbox is loaded 🎉`);

  workbox.precaching.precacheAndRoute([]);

} else {
  console.log(`Boo! Workbox didn't load 😬`);
}
````
However, when I used the code above, routes with search parameters were not being served properly. I removed search parameters using `ignoreUrlParametersMatching`[^url_param]. Also, besides precaching, we need to cache some assets like google fonts which mdBook uses and then update the cache when new versions are available. I changed the `sw.js` to the following:

````js
importScripts(
  "https://storage.googleapis.com/workbox-cdn/releases/3.5.0/workbox-sw.js"
);

if (workbox) {
  console.log(`Yay! Workbox is loaded 🎉`);

  workbox.precaching.precacheAndRoute([], {
    ignoreUrlParametersMatching: [/.*/]
  });

  // Cache the Google Fonts stylesheets with a stale while revalidate strategy.
  workbox.routing.registerRoute(
    /^https:\/\/fonts\.googleapis\.com/,
    new workbox.strategies.CacheFirst({
      cacheName: "google-fonts-stylesheets"
    })
  );

  self.addEventListener('activate', function(event) {
    
    event.waitUntil(
      caches.keys().then(function(cacheNames) {
        return Promise.all(
          cacheNames.filter(function(cacheName) {

          }).map(function(cacheName) {
            return caches.delete(cacheName);
          })
        );
      })
    );
  });

  self.addEventListener('message', function(event) {
    if (event.data.action === 'skipWaiting') {
      self.skipWaiting();
    }
  });

} else {
  console.log(`Boo! Workbox didn't load 😬`);
}

````
I modified the `registration-sw.js` to prompt the user when updates are available based on suggestions on this post[^update].

````js
var indexController = this;

if ("serviceWorker" in navigator) {
  window.addEventListener("load", () => {
    navigator.serviceWorker
      .register("sw.js")
      .then(registration => {
        if (registration.waiting) {
          indexController.updateReady(registration.waiting);
          return;
        }
        if (registration.installing) {
          indexController.trackInstalling(registration.installing);
          return;
        }

        registration.addEventListener("updatefound", function() {
          indexController.trackInstalling(registration.installing);
        });

        console.log(`Service Worker registered! Scope: ${registration.scope}`);
      })
      .catch(err => {
        console.log(`Service Worker registration failed: ${err}`);
      });
  });
}

function trackInstalling(worker) {
  var indexController = this;
  worker.addEventListener("statechange", function() {
    if (worker.state == "installed") {
      indexController.updateReady(worker);
    }
  });
}

function updateReady(worker) {
  var res = confirm("New version available, reload page?");
  if (res) {
    worker.postMessage({ action: "skipWaiting" });
    location.reload();
  }
}

````
Here we are showing a confirm box to prompt the user that there is a new version of the book available. It is based on Jake Archibald's suggestion[^jaffa]. Ideally, you would show a banner when a service worker has updated and waiting to install.

Now, everytime we build the book, we need to generate the proper "revision hashes" to the files in the manifest entries. We can use the `workbox-cli`[^wbcli] to inject a precache manifest into the service worker. You need `node.js` to use the cli. During the setup, we can choose which file types we want to cache. The configuration is saved in `workbox-config.js`. 

````js
module.exports = {
  "globDirectory": "book/",
  "globPatterns": [
    "**/*.{css,js,html,png,eot,svg,ttf,woff,woff2,json}"
  ],
  "swDest": "book/sw.js",
  "swSrc": "sw.js"
};
````
You can modify the `globPatterns` accordingly. The production service worker will be `book/sw.js`. After building the book, we need to run the `workbox injectManifest workbox-config.js` command.

![new versioon available](/img/mdbook_offline_new_version_prompt.png)

## Automating the build in Travis CI
You can customise the build to generate the proper service worker every time there is a change. I made a sample repo[^demo_repo]. 
You should set an environment variable `GITHUB_TOKEN` in `Travis CI`. You’ll need to generate a personal access token with the `public_repo` or `repo` scope on `Github`. This can be done in `Settings` > `Developer settings` > `Personal access tokens` > `Generate new token`


![travis build success](/img/mdbook_offline_travis.png)


## That's it!
Hope you find this useful and integrate service workers in your mdBook so your users can enjoy your content wherever they are! If you want to help, you can contribute to make the sample repo[^demo_repo] better.

## References
[^mdbook]: [mdBook](https://github.com/rust-lang-nursery/mdBook)
[^thebook]: [The Rust Programming Language](https://doc.rust-lang.org/book/)
[^mdbook_user_guide]: [mdBook user Documentation](https://rust-lang-nursery.github.io/mdBook/)
[^embedded]: [Embedded Book](https://rust-embedded.github.io/book/)
[^pwa]: [Progressive Web Apps](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)
[^sw]:[Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
[^wb]: [Workbox](https://developers.google.com/web/tools/workbox/)
[^strategies]: [Workbox strategies](https://developers.google.com/web/tools/workbox/modules/workbox-strategies)
[^codelab]: [Workbox Codelab](https://codelabs.developers.google.com/codelabs/workbox-lab)
[^url_param]: [Ignore URL Parameters](https://developers.google.com/web/tools/workbox/modules/workbox-precaching#ignore_url_parameters)
[^update]: [Activate updated service worker on refresh](https://stackoverflow.com/questions/40100922/activate-updated-service-worker-on-refresh)
[^jaffa]: [Toast to show sw updated](https://github.com/jakearchibald/wittr/compare/task-update-notify...update-interaction)
[^wbcli]: [Workbox CLI](https://developers.google.com/web/tools/workbox/guides/precache-files/cli)
[^demo_repo]: [Sample repository](https://github.com/rahul-thakoor/mdBook-offline-support)
<!-- [^pcwr]: https://rahul-thakoor.github.io/physical-computing-rust/ -->
