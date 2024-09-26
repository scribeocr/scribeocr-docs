---
layout: default
title: Controls
nav_order: 3
---

# Navigation
### Pan
Users can pan using the following methods.
- Holding down `Mouse middle` and dragging the mouse.
- Using a 2 finger "pan" gesture (on touch pads).
- Using a 1 finger "pan" gesture (on mobile devices).

### Zoom
Users can zoom in/out using the following methods.
- Using `Ctrl + Scroll wheel`.
- Using pinch gesture (touch pads and mobile devices only).
- Using `+` and `-` buttons on the interface (next to `prev`/`next`)
- Using `Ctrl + +` and `Ctrl + -` keyboard shortcuts.

# Words
### Select
Individual words can be selected by clicking or tapping them.  Groups of words can be selected by clicking and dragging to create a selection box.  Words can be added to an existing selection by holding down `Ctrl` when selecting them.  There is currently no way to select multiple words on mobile devices.

Words can also be selected using the keyboard arrow keys.  For a full list of shortcuts for selecting words, see the [Shortcuts Cheat Sheet section](#select-words).

### Split Words
A single word can be split into two words by positioning the cursor where the word should be split, right clicking, and selecting `Split Word`.

### Combine Words
Multiple adjacent words can be combined into a single word by selecting the words, right clicking, and selecting `Merge Words`.

# Keyboard Shortcut Cheat Sheet
### General

| Shortcut                  | Action                                      |
|---------------------------|---------------------------------------------|
| `Ctrl + +`                | Zoom in                                     |
| `Ctrl + -`                | Zoom out                                    |
| `PageUp`                  | Previous page                               |
| `PageDown`                | Next page                                   |

### Select Words

| Shortcut                  | Action                                      |
|---------------------------|---------------------------------------------|
| `Tab`                     | Select next word[^next-word]                |
| `Shift + Tab`             | Select previous word                        |
| `ArrowRight`              | Select word to right                        |
| `ArrowLeft`               | Select word to left                         |
| `ArrowUp`                 | Select word above selected word             |
| `ArrowDown`               | Select word beneath selected word           |
| `Shift + ArrowRight`      | Expand selection to right                   |
| `Shift + ArrowLeft`       | Expand selection to left                    |

### Edit Words
Once words have been selected, shortcuts using the `Ctrl` modifier can be used to edit them.

| Shortcut                  | Action                                      |
|---------------------------|---------------------------------------------|
| `Ctrl + i`                | Toggle italic font style                    |
| `Ctrl + b`                | Toggle bold font style                      |
| `Ctrl + Alt + +`          | Increase word font size                     |
| `Ctrl + Alt + -`          | Decrease word font size                     |
| `Ctrl + ArrowLeft`        | Move the word's left bound to the left      |
| `Ctrl + ArrowRight`       | Move the word's left bound to the right     |
| `Ctrl + Alt + ArrowLeft`  | Move the word's right bound to the left     |
| `Ctrl + Alt + ArrowRight` | Move the word's right bound to the right    |
| `Enter`                   | Start/stop editing word text (from start)   |
| `Alt + Enter`             | Start/stop editing word text (from end)     |
| `Ctrl + Delete`           | Delete word(s)                              |

[^next-word]: The "next word" (selected with `Tab`) is selected based on what Scribe.js believes the reading order is.  After reaching the end of a line, the `Tab` shortcut will jump to whatever it believes the next line in the document is, whereas `ArrowRight` will go to the word visually to the right (if any).  The "next word" can be unpredictable for documents without an unambiguous reading order--for example, data tables or documents with many floating elements.