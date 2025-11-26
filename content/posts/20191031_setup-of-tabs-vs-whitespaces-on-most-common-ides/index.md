---
title: "Setup of Tabs vs Whitespaces on most common IDEs"
slug: "setup-of-tabs-vs-whitespaces-on-most-common-ides"
draft: false
date: "2019-10-31T08:47:02Z"
categories:
  - "Software Development"
tags:
  - "Android Studio"
  - "Visual Studio"
  - "Xcode"
author: "Curia Damiano"
image: "img/TabsVsSpaces.png"
---

If for you it is important to correctly format your code, you know very well
about the whitespaces versus tabs dilemma.
Generally, in the past tabs were preferred, because they optimized source code
file sizes; they also allowed to switch between 2 and 4 spaces easily.
In the last times, I see more and more spaces used instead, as they offer a more
consistent view across different IDE configurations.
Even if personally I still prefer tabs (and luckily I am not alone
[https://www.hanselman.com/blog/TabsVsSpacesAPeacefulResolutionWithEditorConfigInVisualStudioPlusNETExtension]
), in this guide I will explain how to configure them in the most popular IDEs.

EditorConfig
The EditorConfig settings override the local developer settings, so I strongly
suggest using this approach to have a consistent and reproducible working
environment across all developers of a team.
Sadly not all settings are available here, so in the other cases you'll still
need to fall back to the specific IDE settings that will follow later.

* How to choose between spaces and tabs
  indent_style
  [https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties#indent_style] 
  = {space|tab}
  indent_size
  [https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties#indent_size] 
  = {4|tab}
  tab_width
  [https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties#tab_width] 
  = 4
* How to visually display whitespaces
  n.a.
* How to reformat existing code
  n.a.
* Other useful settings * How display line numbers
  n.a.
* How display indentation lines
  n.a.

Visual Studio for Windows
* How to choose between spaces and tabs
  From Tools | Options | Text Editor | All Languages | Tabs, here choose
  "Insert spaces" or "Keep tabs"
  From this same dialog, you can also configure "Tab size" and Indent size"
* How to visually display whitespaces
  You need to open a source code file before finding the following setting
  From Edit | Advanced | "View White Space" (Ctrl+E, S)
* How to reformat existing code
  From Edit | Advanced | "Format Document" (Ctrl+E, D) or "Format Selection"
  (Ctrl+E, F)
* Other useful settings * How display line numbers
  From Tools | Options | Text Editor | All Languages | General, "Line
  numbers"
* How display indentation lines
  From Tools | Options | Text Editor | General, "Show structure guide lines"

Visual Studio for Mac
* How to choose between spaces and tabs
  From Visual Studio | Preferences | Source Code | Code Formatting | Text File
  | Whitespace, "Convert tabs to spaces"
  From this same dialog, you can also configure "Tab width" and Indent width"
* How to visually display whitespaces
  From Visual Studio | Preferences | Text Editor | Markers and Rules | Show
  invisible characters, here choose "Always", "Selection" or "Never"
* How to reformat existing code
  From Visual Studio | Edit | Format, "Format Document" (Ctrl+I)
* Other useful settings * How display line numbers
  From Visual Studio | Preferences | Text Editor | Markers and Rules, "Show
  line numbers"
* How display indentation lines
  From Visual Studio | Preferences | Text Editor | Markers and Rules, "Show
  indentation lines"

Visual Studio Code
* How to choose between spaces and tabs
  From File | Preferences | Settings | Text Editor, "Detect Indentation"
  From File | Preferences | Settings | Text Editor, "Insert Spaces"
  From File | Preferences | Settings | Text Editor, "Tab Size"
* How to visually display whitespaces
  From File | Preferences | Settings | Text Editor, "Render Whitespace"
* How to reformat existing code
  From View | Command Palette (Ctrl+Shift+P), "Format Document" (Shift+Alt+F)
* Other useful settings * How display line numbers
  From File | Preferences | Settings | Text Editor, "Line Numbers"
* How display indentation lines
  From File | Preferences | Settings | Text Editor, "Render Indent Guides"

Xcode
* How to choose between spaces and tabs
  From Xcode | Preferences | Text Editing | Indentation | "Prefer Indent
  Using", here choose between "Spaces" or "Tabs"
  From this same dialog, you can also configure "Tab Width" and "Indent Width"
* How to visually display whitespaces
  From Editor, Invisibles
* How to reformat existing code
  From Editor | Structure, "Re-Indent" (Ctrl+I)
* Other useful settings * How display line numbers
  From Xcode | Preferences | Text Editing | Display, "Line Numbers"
* How display indentation lines
  There is no a permanent setting for this, but hovering over a structure
  and pressing Command will display the indentation guide

Android Studio
* How to choose between spaces and tabs
  From File | Settings... | Editor | Code Style | Kotlin | check or remove "Use
  tab character"
  From the same dialog, you can also configure "Tab size" and "Indent"
* How to visually display whitespaces
  You need to open a source code file before finding the following setting
  From View | Active Editor | Show Whitespaces
* How to reformat existing code
  From Code | Reformat Code (Ctrl+Alt+L)
* Other useful settings * How display line numbers
  You need to open a source code file before finding the following setting
  From View | Active Editor | Show Line Numbers
* How display indentation lines
  You need to open a source code file before finding the following setting
  From View | Active Editor | Show Indent Guides
