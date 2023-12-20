If we send a normal fetch on `unload` (when the user closes the browser tab), the request won't actually get sent. Some workaround:
 1. `navigator.sendBeacon`
 2. `fetch with option keepalive=true`
 3. `XMLHttpRequest with option async=false`
 4. Use a Service Worker

Whether or not 4 is feasible? This repo is to test that, whether the service worker can outlive the main document. The conclusion is YES. The request is actually get sent, with some caveat:
- Can just use normal `fetch`, don't need `fetch` with `keepalive=true` in Service Worker
- `navigator.sendBeacon` tho won't work in Service Worker
- Just like 1,2,3 If the user closes the whole browser (another word, the tab being closed is the last tab), then the request WON'T get sent.
