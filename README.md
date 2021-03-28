# reddit-demote-tampermonkey.js
Remove promoted posts (Ads) from reddit feed

```js
// ==UserScript==
// @name         Reddit Demote
// @version      0.1
// @description  Remove promoted ads on reddit
// @include      http://*.reddit.com/*
// @include      https://*.reddit.com/*
// @author       keithgabryelski
// @namespace    https://github.com/keithgabryelski
// @require      http://code.jquery.com/jquery-3.4.1.min.js
// ==/UserScript==
/* globals $ */

const xpath = (xpathToExecute) => {
  var result = [];
  var nodesSnapshot = document.evaluate(
    xpathToExecute,
    document,
    null,
    XPathResult.ORDERED_NODE_SNAPSHOT_TYPE,
    null
  );
  for (var i = 0; i < nodesSnapshot.snapshotLength; i++) {
    result.push(nodesSnapshot.snapshotItem(i));
  }
  return result;
};

const cleanUpAds = () => {
  const pp = xpath("//span[text()='promoted']/../../../../../../..");
  for (const p of pp) {
    p.remove();
  }
};

window.addEventListener("scroll", cleanUpAds);
cleanUpAds();
```
