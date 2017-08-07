# Progressive Web Applications
Progressive Web Apps (PWAs) provide a native app experience using modern web technologies. 

PWAs benefit from being developed using the same code as traditional web applications. Building native apps for multiple platforms requires different technologies (i.e., Swift and Java) and can be more expensive. Also, being indexable on Google enables your app to be discovered as opposed to being hidden amongst millions of apps in an app store.

With the right set of capabilities in a browser, a PWA can be as performant, reliable, and engaging as a native app.

### Progressive
The PWA should enhance progressively on devices and browsers that allow it, taking advantage of any features available on the user's device and browser.

### Responsive
The PWA should fit any form factor: desktop, mobile, or tablet.

### Connectivity Independent
The PWA should work in areas of low connectivity, or when there's no internet connection available.

### App Like
A PWA needs to feel like a native app to the user, with app-like interactions, navigation, and minimal page refreshes.

### Fresh
The PWA should always be up to date. When new content is published, it should be made available in the app.

### Safe
A PWA should be served via HTTPS to prevent snooping and to ensure content hasn't been tampered with.

### Discoverable
Users should be able to discover the PWA in search engines. 

### Re-engageable
The PWA makes re-engagement easy through features like push notifications.

### Installable
A PWA can be installed on a device's home screen, making it readily available.

### Linkable
A PWA is easily shareable via a URL. It does not require complex installation. 

### [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
Service Workers provide the technical foundation for PWAs. 
Service Workers are event-driven JavaScript scripts the browser runs in the background, separate from a webpage.

They act as client-side proxies that listen for and handle events triggered in your app, even when it isn't open in the browser.

They also allow the app to cache static assets locally, which can enable you to display useful information to the user even when offline. Once a user's network connection is restored, a service worker can seamlessly fetch and sync data.

They allow the developer to control how network requests are handled, which gives you complete control over the experience. 

Service Workers always require a HTTPS connection.

### [Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest)
A Web App Manifest is a JSON file that describes the configuration of your app.

It contains metadata associated with your app, configures how your app appears to users, and makes your app indexable by search engines.

Once you create your manifest file, you link it to the HTML in the HEAD of the document:

```
<link rel="manifest" href="/manifest.webmanifest">
```

### [Application Shell Architecture](https://developers.google.com/web/fundamentals/architecture/app-shell)
App Shell Architecture separates the core application infrastructure and UI from the data.

The application shell itself is the minimal HTML, CSS, and JavaScript required to power the user interface of your app. The application shell is similar to the bundle of code you'd submit to an app store.

The application shell should load fast, be cached locally, and dynamically display content. 

The core components of the application shell are any components that need to be on the screen immediately, other key UI components, and any supporting resources necessary for the app (i.e, images, styles, and JavaScript).

### [Google Lighthouse](https://developers.google.com/web/tools/lighthouse/)
Lighthouse is an open-source tool developed by Google to test the quality of a web application. It has a large focus on PWA features, such as homescreen and offline support; but can be used to audit any web application. 
