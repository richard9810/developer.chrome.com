---
# Required
layout: 'layouts/blog-post.njk'

# Required
title: Deprecations and removals in Chrome 80

# Required
description: >
  A round up of the deprecations and removals in Chrome 80 to help you plan.

# Optional
# How to add a new author
# https://developer.chrome.com/docs/handbook/how-to/add-an-author/
authors:
  - joemedley

# Required
date: 2019-12-19

# Optional
# Include an updated date when you update your post
updated: 2020-08-11

# Optional
# How to add a new tag
# https://developer.chrome.com/docs/handbook/how-to/add-a-tag/
tags:
  - deprecations
  - removals




---

{% Aside %}
Visit ChromeStatus.com for lists of 
<a href="https://www.chromestatus.com/features#browsers.chrome.status%3A%22Deprecated%22">current deprecations</a>
and <a href="https://www.chromestatus.com/features#browsers.chrome.status:%22Removed%22">previous removals</a>.  
{% endAside %}

## Disallow Synchronous XMLHTTPRequest() in Page Dismissal

Chrome now disallows synchronous calls to `XMLHTTPRequest()` during page
dismissal when the page is being navigated away from or is closed by the user.
This applies to `beforeunload`, `unload`, `pagehide`, and `visibilitychange`.

To ensure that data is sent to the server when a page unloads, we recommend
`sendBeacon()` or `Fetch` `keep-alive`. For now, enterprise users can use the
`AllowSyncXHRInPageDismissal` policy flag and developers can use the origin
trial flag `allow-sync-xhr-in-page-dismissal` to allow synchronous XHR requests
during page unload. This is a temporary "opt-out" measure, and we expect to
remove this flag in Chrome 88. 

For details about this and the alternatives, see [Disallowing synchronous
XMLHTTPRequest() during page dismissal]().

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/cCWNIXB4dzY/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/4664843055398912) &#124;
[Chromium Bug](https://crbug.com/827324)


## FTP support deprecated

The current FTP implementation in Chrome has no support for encrypted
connections (FTPS), nor proxies. Usage of FTP in the browser is sufficiently low
that it is no longer viable to invest in improving the existing FTP client. In
addition more capable FTP clients are available on all affected platforms.

Chrome 72 removed support for fetching document subresources over FTP and
rendering of top level FTP resources. Currently navigating to FTP URLs results
in showing a directory listing or a download depending on the type of resource.
A bug in Google Chrome 74 and later resulted in dropping support for accessing
FTP URLs over HTTP proxies. Proxy support for FTP was removed entirely in Google
Chrome 76.

The remaining capabilities of Google Chrome’s FTP implementation are restricted
to either displaying a directory listing or downloading a resource over
unencrypted connections. 

The deprecation timeline is tentatively set as follows:

**Chrome 80 (stable in February 2020)**

FTP is disabled by default for *non-enterprise clients*, but may be turned on
using either the `--enable-ftp` or the `--enable-features=FtpProtocol`
command-line flags. Alternatively, it can be turned on using the `#enable-ftp`
option on chrome://flags.

**Chrome 81 (stable in March 2020)**

FTP is disabled by default for *all Chrome installations*, but may be turned on
using either the `--enable-ftp` or the `--enable-features=FtpProtocol`
command-line flags.

**Chrome 82 (stable in April 2020)**

FTP support will be completely removed.

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/e1hkwUL4p3w/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/6246151319715840) &#124;
[Chromium Bug](https://crbug.com/333943)

## Disallow allow popups during page unload

Pages may no longer use `window.open()` to open a new page during unload. The
Chrome popup blocker already prohibited this, but now it is prohibited whether
or not the popup blocker is enabled. 

Enterprises can use the `AllowPopupsDuringPageUnload` policy flag to allow
popups during unload. Chrome expects to remove this flag in Chrome 82.

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/MkA0A1YKSw4/discussion) &#124;
[Chromestatus Tracker](https://www.chromestatus.com/feature/5989473649164288) &#124;
[Chromium Bug](https://crbug.com/844455)

## Non-origin-clean ImageBitmap serialization and transferring removed

Errors will now be raised when a script tries to serialize or transfer a
non-origin-clean ImageBitmap. A non-origin-clean ImageBitmap is one that
contains data from cross cross-origin images that is not verified by CORS logic.

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/Z1XdYf6SjDU/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/5728790883860480) &#124;
[Chromium Bug](https://crbug.com/1013087)

## Protocol handling now requires a secure context

The methods `registerProtocolHandler()` and `unregisterProtocolHandler()` now
require a secure context. These methods capable of reconfiguring client states
such that they would allow transmission of potentially sensitive data over a
network. 

The `registerProtocolHandler()` method gives a webpage a mechanism to register
itself to handle a protocol after a user consents. For example, a web-based
email application could register to handle the `mailto:` scheme. The corresponding
`unregisterProtocolHandler()` method allows a site to abandon its
protocol-handling registration.

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/1AOWqzgFQiw/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/5756636801007616) &#124;
[Chromium Bug](https://crbug.com/882284)

## Web Components v0 removed

Web Components v0 are now removed from Chrome. The Web Components v1 APIs are a
web platform standard that has shipped in Chrome, Safari, Firefox, and (soon)
Edge. For guidance on upgrading, read [Web Components update: more time to
upgrade to v1 APIs](https://developers.google.com/web/updates/2019/07/web-components-time-to-upgrade). The
following features have now been removed. This deprecation covers the items
listed below.

### Custom Elements

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/h-JwMiPUnuU/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/4642138092470272) &#124;
[Chromium Bug](http://crbug.com/180965)


### HTML Imports

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/h-JwMiPUnuU/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/5144752345317376) &#124;
[Chromium Bug](http://crbug.com/240592)


### Shadow DOM

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/h-JwMiPUnuU/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/4507242028072960) &#124;
[Chromium Bug](http://crbug.com/336121)


## Remove -webkit-appearance:button for arbitrary elements

Changes `-webkit-appearance:button` to work only with `<button>` and `<input>`
buttons. If `button` is specified for an unsupported element, the element has
the default appearance. All other `-webkit-appearance` keywords already have
such restriction. 

[Intent to Remove](https://groups.google.com/a/chromium.org/d/topic/blink-dev/QFXFzfQtlKk/discussion) &#124;
[Chrome Platform Status](https://www.chromestatus.com/feature/4867142128238592) &#124;
[Chromium Bug](https://bugs.chromium.org/p/chromium/issues/detail?id=981720)


## Deprecation policy


To keep the platform healthy, we sometimes remove APIs from the Web Platform which have run their course. There can be many reasons why we would remove an
API, such as:

- They are superseded by newer APIs.
- They are updated to reflect changes to specifications to bring alignment and consistency with other browsers.
- They are early experiments that never came to fruition in other browsers and thus can increase the burden of support for web developers.


Some of these changes will have an effect on a very small number of sites. To mitigate issues ahead of time, we try to give developers advanced notice so they can make the required changes to keep their sites running.

Chrome currently has a <a href="http://www.chromium.org/blink#TOC-Launch-Process:-Deprecation"> process for deprecations and removals of API's</a>, essentially:


- Announce on the <a href="https://groups.google.com/a/chromium.org/forum/#!forum/blink-dev">blink-dev</a> mailing list.
- Set warnings and give time scales in the Chrome DevTools Console when usage is detected on the page.
- Wait, monitor, and then remove the feature as usage drops.
 


You can find a list of all deprecated features on chromestatus.com using the <a href="https://www.chromestatus.com/features#deprecated"> deprecated filter </a> and removed features by applying the <a href="https://www.chromestatus.com/features#removed">removed filter</a>. We will also try to summarize some of the changes, reasoning, and migration paths in these posts.
