---
title: "Textexpander & Markdown"
date: 2016-01-18 22:40
---

- [利用 TextExpander 提高在 Mac 上撰写 Markdown 的效率 - 少数派](http://sspai.com/27479/)
    - Link to front browser tab 这个功能是我之前就想到过的，没有想到真的有
- [Quicker Markdown linking with TextExpander ](http://www.leancrew.com/all-this/2014/07/quicker-markdown-linking-with-textexpander/)
    - 我感觉aText或者TextExpander的功能，与Workflow在iOS中的功能挺像的。
        - 用某种方式触发动作
        - 执行一系列动作
    - 可以再想想
- [Applescript to get frontmost tab’s url and title of various browsers.](https://gist.github.com/vitorgalvao/5392178)
    - messing around with applescript is funny. it seems they’re experimenting with those browsers rather than referring to a official document.
- [7 Tips For Automating Your Mac With TextExpander](http://www.makeuseof.com/tag/7-tips-for-automating-your-mac-with-textexpander/)
    - Special Keys, this is really handy..

```applescript
tell application "System Events"
  set numChrome to count (every process whose name is "Google Chrome")
end tell

if numChrome > 0 then
    tell application "Google Chrome"
      set frontIndex to active tab index of front window
      set fURL to URL of tab frontIndex of front window
      set fTitle to title of tab frontIndex of front window
    end tell
end if

get "[" & fTitle & "](" & fURL & ")【|】"
```