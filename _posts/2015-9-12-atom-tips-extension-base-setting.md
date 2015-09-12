---
layout: post
title: Atom Tips Extension Base Setting
---

![Atom]({{ site.baseurl }}/images/2015091200.png "Atom")

Previously when coding with Atom, there is a thing really irritating - when I code for php I have to set tab length 4 but for python or jade, I need tab length of 2.

Normally we set the tab length at File > Settings.

### Problem Solving
So how to solve it? Just go to "File > Open Your Config" to open config.cson, then paste the config below.

```javascript
"*":
  "exception-reporting":
    userId: ":)"
  welcome:
    showOnStartup: false
  core: {}
  editor:
    invisibles: {}
    showInvisibles: true
    fontSize: 13
    zoomFontWhenCtrlScrolling: false
    showIndentGuide: true
    softWrap: true
  "tabs-to-spaces": {}
  whitespace: {}
".php":
  editor:
    tabLength: 4
```

### Explanation
- "*" is meaning wildcard for all type of file, which come along after Atom has been installed
- ".php" means for every file extension that is php, and I set tabLength to 4 (default is 2)
