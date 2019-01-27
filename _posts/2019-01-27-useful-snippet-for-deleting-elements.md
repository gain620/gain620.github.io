---
published: true
layout: single
title: "Useful javascript snippet for deleting unwanted elements"
date: 2019-01-27
category: post
tags: [web, programming, javascript]
comments: true
---

You can checkout this chrome plugin to load custom scripts
**[ODM Sandbox](https://chrome.google.com/webstore/detail/odm-sandbox-custom-script/fjnjnmopbmckmaphgcecmabflgnpnfif)**

```js
let targetHost = '';
let targetClass = '';

if (window.location.host === targetHost) {
	let targetNodeList = document.getElementsByClassName(targetClass);

		for (let i = 0; i < targetNodeList.length; i++) {
		targetNodeList[i].parentElement.removeChild(targetNodeList[i]);
	}

}
```

If your page is a SPA that lazy loads some elements, you can utilize setTimeout to wait and delete those elements.

For example,

```js
let targetHost = 'www.twitch.tv';

setTimeout(()=> {
	let targetClass = 'recommended-channels';

	if (window.location.host === targetHost) {
		let targetNodeList = document.getElementsByClassName(targetClass);

			for (let i = 0; i < targetNodeList.length; i++) {
			targetNodeList[i].parentElement.removeChild(targetNodeList[i]);
		}

	}
}, 1500);
```