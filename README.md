# Spotify Android — checkout WebView origin PoC

Proof-of-concept page for a coordinated-disclosure report to Spotify via HackerOne.

`SpotifyCheckoutCallbackActivity` in the Spotify Android app is exported and
`BROWSABLE`. It accepts:

```
spotify-checkout://payment-callback/<uuid>?status=success&success_url=<URL>
```

URL-decodes `success_url` and loads it in the in-app checkout WebView **without any
origin, scheme or allow-list validation**. Any web page or installed app can therefore
render arbitrary content inside Spotify's own payment UI, where there is no address
bar for a user to inspect.

`index.html` is the page used to demonstrate that a remote, non-Spotify origin is
loaded. It is **deliberately and prominently labelled as attacker-controlled**.

## This page collects nothing

The form is inert: `submit` is cancelled in JavaScript and the values are echoed
back into the page only, to illustrate what a real attacker would capture.
There is no network transmission, no logging, no analytics, no backend.

Not affiliated with or endorsed by Spotify. Spotify is a trademark of Spotify AB;
its name and logo appear here solely to demonstrate the security issue being reported.
