All modern browsers (down to IE8) support "hashchange" events, which provide `event.newURL` and `event.oldURL` when the hash changes.

By the time the event has fired, the hash has changed, so `event.newURL === window.location.toString()` and the new hash is at `window.location.hash`.