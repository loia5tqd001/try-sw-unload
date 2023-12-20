If we send a normal fetch on `unload` (when the user closes the browser tab), the request won't actually get sent. Some workaround:
 1. `navigator.sendBeacon`
 2. `fetch with option keepalive=true`
 3. `XMLHttpRequest with option async=false`
 4. Use a Service Worker

Whether or not 4 is feasible? This repo is to test that, whether the service worker can outlive the main document. The conclusion is YES. The request is actually get sent, with some caveat:
- Can just use normal `fetch`, don't need `fetch` with `keepalive=true` in Service Worker
- `navigator.sendBeacon` tho won't work in Service Worker
- Just like 1,2,3 If the user closes the whole browser (another word, the tab being closed is the last tab), then the request WON'T get sent.

Another caveat: Working with Service Worker is not a pleasant exp at all with React. I have to deal with Service Worker in build mode (`npm run build`) not in dev mode, see more [here](https://github.com/facebook/create-react-app/issues/2396#issuecomment-304539651).
