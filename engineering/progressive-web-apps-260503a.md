# Progressive Web Apps (PWA)

**Date:** 2026-05-03  
**Category:** engineering  
**Tags:** `pwa`, `web`, `mobile`, `performance`, `offline`

---

## TL;DR

- A PWA is a web app that uses modern browser APIs to behave like a native app — installable, offline-capable, and fast
- The experience lives at a URL; nothing needs to be downloaded from an app store
- Service workers are the engine: they intercept network requests, cache assets, and enable offline use
- PWAs shine when reach matters more than device APIs; native apps still win when deep hardware integration is required
- "Should this be a PWA?" reduces to one question: *Does the user need features the web can't provide?*

---

## Timeline

PWAs did not arrive in a single release — they are the result of browser capabilities layering on top of each other over about a decade.

| Year | Milestone |
|------|-----------|
| **2007** | Steve Jobs announces the original iPhone, describing web apps delivered via Safari as the model for third-party software — the idea predates the App Store |
| **2008** | App Store launches; native wins the mindshare race for the next several years |
| **2013** | Mozilla ships the first draft of the **Service Worker** spec; background caching becomes a real concept |
| **2015** | Google engineers Frances Berriman and Alex Russell coin the term **"Progressive Web App"**; Chrome begins shipping Service Worker support |
| **2016–2017** | Web App Manifest, Push Notifications, and Background Sync land in Chrome and Firefox; Android's "Add to Home Screen" prompt becomes reliable |
| **2018** | Apple ships Service Worker support in **Safari 11.1** (iOS and macOS); PWAs become cross-platform in practice for the first time |
| **2019** | Chrome on Android starts showing the **Web App Install Banner** automatically; Microsoft adds PWA support to Edge and lists PWAs in the Windows Store |
| **2021** | Web Share API, Badging API, and File System Access bring PWAs closer to native parity on desktop |
| **2023–present** | Apple incrementally expands PWA capability on iOS (push notifications land in iOS 16.4); Baseline 2023 locks in a broadly-supported PWA feature set across all major browsers |

---

## What the user actually gets

The benefits of a PWA are felt most at the edges of a user's situation — slow connections, low storage, or unfamiliar devices.

### Instant load and offline use

A service worker caches the app shell and key data on the first visit. On return visits — even with no network — the app opens immediately from cache. For a user on a subway or in a rural area, this is not a nice-to-have; it is the difference between functional and broken.

### No install friction

Reaching an app through a URL removes every barrier that exists before a user opens a native app: finding it in a store, reviewing permissions, waiting for a download, then opening it. A PWA is already open. The user can optionally "install" it — which pins a shortcut to the home screen or taskbar — but they never have to.

### Automatic updates

There is no version mismatch problem. The next time the user visits (or when the service worker detects a new cache), they get the current version silently. No update prompt, no "force close to apply update" dialogs.

### Smaller footprint

A typical PWA is measured in kilobytes of cached resources rather than the hundreds of megabytes common for native apps. On low-storage devices — still the majority of phones worldwide — this matters enormously.

### A single codebase everywhere

The user does not see this directly, but they benefit indirectly: the organization can move faster, fix bugs in one place, and ship to iOS, Android, Windows, and macOS simultaneously. Fewer parallel codebases means fewer regressions that affect only one platform.

---

## When to choose a PWA

### Choose a PWA when…

| Signal | Why it points to PWA |
|--------|----------------------|
| Your audience is broad and heterogeneous (multiple platforms, older devices) | One codebase reaches all of them equally |
| Discovery happens through search or shared links | PWAs are indexable and live at URLs; native apps are not |
| You need to ship fast and iterate frequently | Deploy to a CDN, done — no app store review cycle |
| Offline or low-connectivity use is important | Service workers handle this natively |
| Storage constraints matter to your users | PWAs have a dramatically smaller footprint |
| The feature set is content, forms, media, or light interaction | This is squarely in the web's wheelhouse |

### Choose native (or a hybrid) when…

| Signal | Why it points to native |
|--------|-------------------------|
| You need Bluetooth, NFC, USB, or advanced camera controls | Web APIs for these are partial or absent on iOS |
| The app must run complex background tasks (audio engines, GPS tracking, ML inference) | Native background execution is far more capable |
| High-performance graphics are central (AAA games, AR/VR) | WebGL/WebGPU are impressive, but not at native parity |
| Your users will find the app primarily through an app store | Native wins on discoverability in that channel |
| You need push notifications on iOS before iOS 16.4 | Service worker push is not available on older Safari |

### The honest summary

> A PWA is the right default for most content-and-interaction apps. Reach for native only when you have confirmed, specific platform requirements the web genuinely cannot meet — not because of historical assumptions.

---

## Key technical concepts (reference)

| Term | What it is |
|------|------------|
| **Service Worker** | A JavaScript file that runs in a background thread; intercepts fetch requests, manages caches, handles push events |
| **Web App Manifest** | A JSON file that tells the browser the app's name, icons, theme color, and display mode |
| **Cache API** | Browser-native storage for request/response pairs; used by the service worker to serve assets offline |
| **Install prompt** | The browser UI that lets a user add the PWA to their home screen or taskbar |
| **Push Notifications** | Server-initiated messages delivered via the Web Push protocol through the service worker |
| **Workbox** | Google's official library that wraps the Service Worker and Cache APIs with high-level caching strategies |

---

## Sources

[1] [Progressive Web Apps — web.dev](https://web.dev/explore/progressive-web-apps)  
[2] [Service Worker API — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)  
[3] [The original "Progressive Web Apps" post by Frances Berriman and Alex Russell](https://infrequently.org/2015/06/progressive-apps-escaping-tabs-without-losing-our-soul/)  
[4] [What Web Can Do Today](https://whatwebcando.today)  
[5] [Workbox — Google Developers](https://developer.chrome.com/docs/workbox)
