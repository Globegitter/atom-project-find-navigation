# project-find-navigation

![gif](https://raw.githubusercontent.com/t9md/t9md/55e7fd32500d45751e2d7824f008e42b06763cd1/img/atom-project-find-navigation.gif)

Provides keyboard navigation for project-find-result.

# What's this?

Provide keyboard navigation for project-find-result of [find-and-replace](https://github.com/atom/find-and-replace) package.  
find-and-replace provides `project-find:show` command which shows found entries in project.  
With this package you can navigate each match with keyboard.  

# Excuse

This package's code is greatly and directly depending on internal variables and functions of [find-and-replace](https://github.com/atom/find-and-replace) provides.

So this package might not work in future version of find-and-replace.  
If code change made on find-and-replace was too big, I might give up this navigation hack package.  
So essentially this is proof of concept to evaluate how project-find's result pane navigation could be improved.  

# Features

Here is summary table of what project-find-navigation provides.

| available on |  command       | pure project-find  | project-find-navigation  |
| ------------ | ------------- |-------------| -----|
| results-pane | mousedown   | Jump to found entry and select | Scroll to found entry with flashing effect, focus remains on result pane |
| results-pane | confirm   | Jump to found entry and select | Jump to found entry with flashing effect, no select |
| results-pane | confirm-and-continue | N/A | Scroll to found entry with flashing effect, focus remains on result pane |
| results-pane | select-next-and-confirm | N/A | Select next item and then confirm-and-continue(auto preview) |
| results-pane | select-prev-and-confirm | N/A | Select previous item and then confirm-and-continue(auto preview) |
| global | next | N/A | goto next result |
| global | prev | N/A | goto previous result |
| global | activate-results-pane | N/A | Focus to results-pane if exists |

Other features.

- Focus to result-pane by keymap.
- Highlight(decorate) found entries on editor, auto-cleared when result-pane destroyed.
- Open found entry in **adjacent** pane. This mean, if result-pane was on left pane open found entry on right pane when confirmed.

# Keymap

No keymap provides by default.

e.g.

My setting, navigate results-pane with Vim like keymap.

```coffeescript
'.preview-pane.project-find-navigation':
  'l': 'core:move-right'
  'h': 'core:move-left'
  'j': 'project-find-navigation:select-next-and-confirm'
  'k': 'project-find-navigation:select-prev-and-confirm'
  'enter': 'project-find-navigation:confirm'

'atom-workspace:not([mini])':
  # This key override window:toggle-full-screen(I'm not using it).
  'ctrl-cmd-f': 'project-find-navigation:activate-results-pane'
  'ctrl-cmd-n': 'project-find-navigation:next'
  'ctrl-cmd-p': 'project-find-navigation:prev'
```

# Style

In your `styles.less`, you can tweak match entry's decoration like following.

```less
@import "syntax-variables";
atom-text-editor::shadow {
  .project-find-navigation-match .region {
    background-color: @syntax-selection-color;
    border: none;
  }
}
```
