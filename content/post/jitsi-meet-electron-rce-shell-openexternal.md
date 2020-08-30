---
title: "RCE in Jitsi Meet Electron prior to 2.3.0 due to insecure use of shell.openExternal() (CVE-2020-25019)"
slug: "jitsi-meet-electron-rce-shell-openexternal"
date: 2020-08-30T11:29:41+02:00
description: "I discovered a remote code execution vulnerability in Jitsi Meet Electron versions prior to 2.3.0 (CVE-2020-25019). This post contains a write-up of the problem which was caused by an insecure use of Electron's shell.openExternal()."
tags: ["jitsi meet", "electron", "shell.openExternal()", "remote code execution", "IT security", "video conferencing"]
featured_image: /img/jitsi-meet-electron-rce-shell-openexternal.png
---

[Jitsi Meet](https://jitsi.org/) is an open source video conferencing software that organizations can deploy on their own servers and that is frequently recommended as an alternative to proprietary solutions. [Jitsi Meet Electron](https://github.com/jitsi/jitsi-meet-electron) is the official desktop client implemented using Electron that can be used both with the official [`meet.jit.si`](https://meet.jit.si/) server as well as any third-party instance.

For my bachelor's thesis, I manually analysed a couple popular Electron apps for security vulnerabilities. I discovered multiple vulnerabilities, including the remote code execution vulnerability in Jitsi Meet Electron described in this post. [CVE-2020-25019](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25019) was assigned to this issue.

First, I scanned the apps with the help of a [modified](https://github.com/baltpeter/en-ba) version of the great [Electronegativity](https://github.com/doyensec/electronegativity) by Doyensec. The results from the scan revealed the following use of Electron's `shell.openExternal()` function (code from [here](https://github.com/jitsi/jitsi-meet-electron/blob/7b2b0c4e710bb626b9d886bb8c283357b223c23b/main.js#L209-L216)):

```js
mainWindow.webContents.on('new-window', (event, url, frameName) => {
  const target = getPopupTarget(url, frameName);

  if (!target || target === 'browser') {
    event.preventDefault();
    shell.openExternal(url);
  }
});
```

This hooks the creation of new windows to instead pass the URL to `shell.openExternal()` unless a popup target other than `browser` is registered for the URL and frame name of the new window. These popup targets are however only used to handle windows that should always stay on top (see [here](https://github.com/jitsi/jitsi-meet-electron-utils/blob/ba851e726b62e93bdcd7ec69414a9c90e3412d58/alwaysontop/index.js#L5-L10)) and are thus not a security check.

As mentioned before, the app can be used with third-party servers. As such, it is possible for an attacker to inject a malicious call to `window.open()` into the pages of their Jitsi Meet instance that will then allow them to pass arbitrary URLs to `shell.openExternal()` when a user uses their server with the app. I have already written another blog post that goes into the details of the [security problems with `shell.openExternal()`]({{< ref "shell-openexternal-dangers" >}}).

In the case of this app, the attack surface was somewhat limited insofar as the external server is loaded through an `<iframe>` and opening `file:` URLs was thus blocked. However, all the other protocols could still be used as discussed. For example, a `smb:` URL to a `.desktop` file on a remote server allowed for RCE on Xubuntu 20.04, as described in the other post. Below is a video demonstrating the exploit:

<video controls autoplay loop><source src="/vid/jitsi-meet-electron-rce-shell-openexternal.mp4" type="video/mp4"></video>

The attack surface was further extended by the [recent introduction](https://github.com/jitsi/jitsi-meet-electron/pull/389) of a protocol handler that allows linking to rooms on external servers (using `jitsi-meet://jitsi.attacker.tld/dangerous-room`). An attacker could use a link like this to lead a user to use their server without having to set the server URL in the app preferences.

Additionally, the app exposed the `shell.openExternal()` function on the `window` object which could be accessed from the renderer process as context isolation is disabled. This was not a critical problem as the remote site is only loaded in an `<iframe>` and thus doesn't have access to the app's `window` object. However, if an attacker somehow managed to achieve XSS in the renderer process, they could use this to escalate it into RCE. As there were no uses of the exposed function in the code, I included a recommendation to remove it in my report.

I reported the vulnerability to the developers on June 28, 2020. I confirmed that it worked using the latest release of the app at that time, version 2.2.0. Props to the Jitsi developers who implemented a fix just a few days later, on June 30, 2020, by filtering the URLs that may be passed to `shell.openExternal()` to only allow HTTP(S) URLs (see the [fix commit](https://github.com/jitsi/jitsi-meet-electron/commit/ca1eb702507fdc4400fe21c905a9f85702f92a14)). The fix was released in version 2.3.0 on July 2, 2020.

---

## Timeline

* June 28, 2020: Vulnerability discovered and reported to <security@jitsi.org>
* June 30, 2020: Developers implement fix in commit [ca1eb702507fdc4400fe21c905a9f85702f92a14](https://github.com/jitsi/jitsi-meet-electron/commit/ca1eb702507fdc4400fe21c905a9f85702f92a14)
* July 2, 2020: Version 2.3.0 [released](https://github.com/jitsi/jitsi-meet-electron/releases/tag/v2.3.0), containing the fix
* August 29, 2020: CVE-2020-25019 [assigned](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-25019)
* August 30, 2020: Details published in this blog post
