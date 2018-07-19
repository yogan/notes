# Progressive Web Apps (PWAs)

## Resources

* Google Chrome Developers [PWA Roadshow YouTube playlist](https://www.youtube.com/playlist?list=PLNYkxOF6rcICnIOm4cfylT0-cEfytBtYt&disable_polymer=true)
* Google's [PWA Checklist](https://developers.google.com/web/progressive-web-apps/checklist)
* [Progressive Web Apps on the Desktop](https://developers.google.com/web/updates/2018/05/dpwa)
* [Progressive Web Apps on MDN](https://developer.mozilla.org/en-US/Apps/Progressive)

## Frameworks / Generators

* [PWA Starter Kit](https://github.com/Polymer/pwa-starter-kit) Google project,
  based on [Polymer](https://www.polymer-project.org/)
* [Create React App](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#making-a-progressive-web-app)
  comes with PWA support
* [Progressifying an Angular 5 Application](https://medium.com/@nsmirnova/creating-pwa-with-angular-5-part-2-progressifying-the-application-449e3a706129)
  Medium article

## PWA Technologies

### Web App Manifest

* [MDN: Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest)
* [Web App Manifest](https://developers.google.com/web/fundamentals/web-app-manifest/)
  on Google Developers Web Fundamentals

### App Shell

* [The App Shell Model](https://developers.google.com/web/fundamentals/architecture/app-shell)
  on Google Developers Web Fundamentals

### Service Workers

#### Documentation

* [Service Workers: an Introduction](https://developers.google.com/web/fundamentals/primers/service-workers/)
  on Google Developers Web Fundamentals
* Extensive [list of resources](https://jakearchibald.github.io/isserviceworkerready/resources.html#moar)
  by Jake Archibald

#### Quick Facts

* requires HTTPS
* cannot access the DOM
* has a life-cycle consisting of registration, installation, and (de-)activation
* can intercept network requests, so a major use-case for service workers is the
  implementation of a cache, to enable offline functionality, and/or to
  pre-fetch sources to improve load performance
* needed to offer push notifications (see below)

### Offline

* [The Offline Cookbook](https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/)
  on Google Developers Web Fundamentals
* [Cache API](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
  * designed to save HTTP responses (in contrast to the more generic
    IndexedDB/WebSQL APIs)
  * works well in service workers
  * not supported in IE, but neither are service workers, so ¯\\\_(ツ)\_/¯
* [sw-precache](https://github.com/GoogleChromeLabs/sw-precache)
  * node module to generate service worker code that will precache specific
    resources so they work offline

### Client-side Data Storage

* [Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API),
  [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
  * synchronous, might be slow on some devices
  * easy to use:
    * `localStorage.setItem('myCat', 'Tom');`
    * `var cat = localStorage.getItem('myCat');`
    * `localStorage.removeItem('myCat');`
* [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)
  * low-level API, rather complicated
  * transactional, SQL-like RDBMS (but object-oriented instead of fixed column
    tables)
* [Web SQL](https://www.w3.org/TR/webdatabase/)
  * *deprecated, W3C recommends to use Web Storage or IndexedDB*
* [localForage](https://localforage.github.io/localForage/) JS lib
  * asynchronous, with `localStorage`-like API
  * uses IndexedDB or WebSQL internally (called "backend drivers")
  * falls back to localStorage in Browsers without support for IndexedDB/WebSQL
  * [frameworks support](https://github.com/localForage/localForage#framework-support)
     for AngularJS, Angular ≥ 4, Backbone, Ember, and Vue

### Push Notifications

* [Web Push Notifications](https://developers.google.com/web/fundamentals/push-notifications/)
  on Google Developers Web Fundamentals
* based on service workers (they operate in the background)

### Hardware Access

*Not really PWA-specific, but related.*

* [MediaDevices API](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices)
  (access to cameras and microphones)
* [Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation)
* [Gamepad API](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad)
* [WebVR API](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API)
  *(experimental)*
* [WebUSB API](https://developer.mozilla.org/en-US/docs/Web/API/USB)
  *(experimental)*
