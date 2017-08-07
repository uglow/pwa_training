# Progressive Web Apps - radically improving web user experiences
> @JeffPosnick - Google Developer Relations

## PWA Workshop
- [Slides](https://docs.google.com/presentation/d/10caR-9mdyDQcL4-eCldYOECAKOw1Y7rPq3au-qVMHEg/preview)
- [Exercise](https://codelabs.developers.google.com/codelabs/your-first-pwapp/#0)


## Background
We are in the middle of another significant shift in web development. In 2005, Ajax, which led to Google Maps etc which
had interactivity. Don't have to live with the click-and-wait desktop experience.

On mobile though, apps rule the day. Mobile devices now outnumber desktop devices.

Apps are:
- more predicatable
- show push notifications
- fast to start up
- work offline
- access to senses

Mobile Web has not had these capabilities, until now.

80% of users time is spent in top 3 apps - winner take all. Users feel a commitment when they install an app. It takes up space on
the device. But the web is ephemeral - you can use it and discard it without thinking about the storage space.

PWAs represent a class of apps that have a full mobile experience but are built as web applications.

Web apps need to be:
- reliable, even when offline, you can see something. Subsequent loads should be fast. Connectivity - knowing when you are online. Lie-Fi
  - Reliability means never showing the Downasaur.
  - We need to make web apps reliable even when the network is reliable
- Fast (app speed is not the focus today, but loading-speed is)
- Engaging, and re-engaging
  - Push notifications - same rules as for native apps. Finally available on mobile devices. Allows cool new use cases.
  - Home screen - Should feel like a native app. Need a standard way of adding an app to the home screen.
  - Immersive. Should be a way to hide the browser chrome for your app to appear full-screen.

The goal is not to get people to install your app, but to get people to come back and user your service. 

## Examples

Mobile Twitter - example of good PWA.
- On latest Android, likes like a regular app when added to home screen
- Can have a splash screen
- When launched from home screen, browser chrome is not visible
- When switching native-apps, you don't see the app as a Chrome-app, but it looks like a native app
- Can customize icons
- When notification appears, clicking on it takes you to the correct place in the PWA
- Size of Twitter clients: Android 24MB, iOS 214MB, PWA 600KB
- They found 65% increase in pages per session, 75% increase in tweets sent after re-writing

Lancôme - 84% decrease in time to interactive, 8% conversion on push notifications.
- iOS is important to Lancome. Even without all the PWA features, they saw 53% increase mobile sessions. This 
  is because when you start to focus on PWAs, you focus on performance and speed, which helps every user.
- Overall, 17% increase in conversions

Lyft - m.lyft.com


## Service Workers
Traditionally you always need to go to the network to get the page content you need. Using SW, you can optionally go to
the network to get things. It acts as a client-side proxy. It gets installed after you first visit the page. It has
access to a cache. It can determine how it responds to browser-requests. So you need to think about different proxying 
strategies. A good approach is to start with an offline-first design (cache-first).

SW are the foundation for Push Notifications, even when there is not a tab open for your website (this is how Facebook desktop notifications are working).


## How to get started?

1) Security - need HTTPS for a secure connection between site and users. (Even the Geolocation API is going to migrate to be HTTPS-only)
  It's about keeping users safe:
  - Identity
  - Confidentiality
  - Integrity
2) Three approaches to PWA-ifying:
    1. Ground up. Good when rebuilding app. Allows you to use the AppShell pattern.
    2. Simple version. E.g Lite-version. Choose to optimise specific features for mobile.  
    3. Single feature. The Weather Company is an example. They just added web notifications.


## Requirements
- Chrome or Firefox
  - Service Worker support

## [Workshops](https://codelabs.developers.google.com/pwa-roadshow)

AppShell - all of the code & assets that would normally be in the app store
LocalStorage - recommend using localForage library instead as it uses IndexDB which is more performant when putting lots of data into local storage

The location of where you serve the service-work from is important, as it controls the scope of the pages it can work on.
Best practice is to put it into root of your web app. If you put it into a /scripts sub directory, it wil only be able to 
proxy things under /scripts, not under the root of your site.

'install' event is fired when the service worker is installed for the first time. It is the perfect time to pre-cache things
that you want to be in your AppShell.

'event.waitUntil()' provides some guarantees around the availability of files to cache (rather than trying to cache files which the
browser has not yet downloaded yet). Look this app.

See 'Service Worker LifeCycle' by Jake Archibald

You don't need to explicitly cache the service-worker.js file.

The 'fetch' handler doesn't get triggered for Web Sockets.

Good library: sw-precache. Newest version is called Workbox (workboxjs.org).

It is also installed by default in create-react-app.