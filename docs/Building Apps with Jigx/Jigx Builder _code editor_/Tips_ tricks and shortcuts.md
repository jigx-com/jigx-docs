---
title: Tips, tricks and shortcuts
slug: P-U8-tips-and-tricks
description: Learn essential shortcuts for Jigx Builder, including publishing files, invoking IntelliSense, using quick fix, and navigating to definitions. Discover the color indicators in Jigx Builder for issue-free files (white), files with validation issues (red), 
createdAt: Tue Jun 20 2023 08:34:27 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Aug 05 2024 13:26:50 GMT+0000 (Coordinated Universal Time)
---

Discover shortcuts and tricks that boost efficiency and maximize your output.

## Jigx Builder shortcuts

| **Shortcuts**                                                                                                                                                                                                                                     | **Mac**                                      | **Windows**                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | ----------------------------------------------- |
| Publish all files in Jigx solution                                                                                                                                                                                                                | ⌘R⌘R                                         | Alt+R Alt+R                                     |
| Publishing an individual file is useful if multiple developers work on the same solution. You only want to publish your changes. Note index.jigx, is a shared file that people all work on, so the last one updated on the server gets published. | ⌘R⌘F                                         | Alt+R Alt+F                                     |
| Invoke IntelliSense                                                                                                                                                                                                                               | Ctrl+space                                   | Ctrl+space                                      |
| Quick Fix                                                                                                                                                                                                                                         | ⌘+.                                          | Ctrl+.                                          |
|  [Go to definition](./Editor.md)                                                                                                                                                                                                                  | F12 &#xA;or &#xA;⌘+click                     | F12&#xA;or&#xA;Ctrl+click                       |
| [Go to reference](./Editor.md)                                                                                                                                                                                                                    | shift+F12&#xA;F12                            | shift+F12&#xA;F12                               |
| The swagger parser function                                                                                                                                                                                                                       | ⌘ + shift + p<br />`Generate Jigx Functions` | Ctrl + shift + p<br />`Generate Jigx Functions` |

## What colors indicate in Jigx Builder&#x20;

| **Color** | **Description**                                                                                                                                                             |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| white     | The file is issue-free. If connected to a Git repository, the file is committed.                                                                                            |
| <span style="color: red;">red</span>       | The file has validation issues/errors/deprecated properties that must be fixed. The number of issues is shown by a red number on the right of the file name in the sidebar. |
| <span style="color: yellow;">yellow</span>    | This means the file is connected to a Git repository and is modified; the letter M displays on the right of the file name in the sidebar.                                   |
| <span style="color: green;">green</span>     | Indicates a new file has been created but not committed to the Git repository yet.                                                                                          |
| <span style="color: blue;">blue</span>      | Indicates the active screen on the mobile device that you are debugging in the builder using Jigx Dev Tools.                                                                |



