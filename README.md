---
title: "Readme reveal.js template"
# For Pandoc conversion Markdown to HTML
header-includes: |
  <!--
      Fontawesome icons
      Links:
        - animate: https://fontawesome.com/docs/web/style/animate
      Example:
        <i class="fa-brands fa-linux"></i> -->
  <link rel="stylesheet" href="font-awesome/css/all.css">
---

## Summary

This project provides a template for a presentation using the [reveal.js] framework by converting a Markdown file into a reveal.js HTML presentation with [Pandoc].

This is not an official template and should not be used as such, I created it for personal use and as an inspiration to others.

Configure reveal.js and Pandoc through YAML frontmatter
```markdown
---
title: title
date: today
author: author
affiliation: university, company, ...
lang: English
theme: night
...
```

New slides are indicated by headings `#`, `##`, ... (determining horizontal/vertical progression in reveal.js, behaviour is influenced by Pandoc option `--slide-level`) or vertical lines `---`.

## Prerequisites

- [Pandoc] document converter: convert Markdown to [reveal.js] HTML file
- \*[task] build tool
- \*`xdotool` to reload browser window

\* optional


## Build

To build this project - create the reveal.js slides as a HTML file from the Markdown file `presentation.md` - install [task] and run `task` or execute the relevant commands in the `Taskfile` in your preferred way, e.g. with `make`.

Build and reload is the default task (target) of the provided Taskfile, call `task -l` to get a list of available tasks. This is achieved by converting the slides with [Pandoc] and then reloading the browser window using `xdotool`, see script `reload_browser.sh`

Pandoc is used with [Mermaid filter](https://github.com/raghur/mermaid-filter) and [reveal.js codeblock lua filter](https://github.com/pandoc/lua-filters/tree/master/revealjs-codeblock) (not working yet)
```bash
pandoc --from=markdown -t revealjs --slide-level 2 -s -o presentation.html presentation.md \
--verbose \
-F mermaid-filter \
-L revealjs-codeblock.lua
```

For inspiration on available features see these example presentations and references
- reveal.js documentation
  - [Themes](https://revealjs.com/themes/)
  - [Configuration](https://revealjs.com/config/)
  - [Backgrounds](https://revealjs.com/backgrounds/)
  - Features
    - [Fragments (fade in/out, highlight, etc. parts of slides)](https://revealjs.com/fragments/)
    - [Transitions](https://revealjs.com/transitions/)
- [reveal.js test slides by Joseph Reagle](https://reagle.org/joseph/talks/2014/exemplar.html#/title-slide) (not quite up-to-date)

You can set up your editor to run `task` after saving to automate this process. In VIM for example you can use the command
```
:autocmd BufWritePost *.md silent! !task
```

For the use of [Font Awesome] icons it is assumed that you have them installed on your system and a symlink `font-awesome` to the installation directory. If you don't want to use [Font-awesome] icons remove the corresponding import in the CSS file and usage in the presentation file.


## Acknowledgements

<a href="https://revealjs.com"><img src="https://revealjs.com/images/logo/reveal-black-text.svg" style="height: 30px; vertical-align: middle;" alt="reveal.js"></a> presentation framework

<a href="https://groups.google.com/g/pandoc-discuss/c/1bKIuyBnWaQ"><img src="https://groups.google.com/group/pandoc-discuss/attach/dd1e7eb3e2439/Sketch16021313.png?part=0.1&view=1" style="height: 30px; vertical-align: middle;"></a>
 [Pandoc](https://pandoc.org) document converter

<a href="https://mermaid.js.org/"><img src="https://raw.githubusercontent.com/mermaid-js/mermaid/develop/docs/public/favicon.svg" style="height: 30px; vertical-align: middle;"> Mermaid</a> diagrams and charts

<a href="https://taskfile.dev/"><img src="https://taskfile.dev/img/logo.svg" style="height: 30px; vertical-align: middle;"> Task</a> runner / build tool

[<i class="fa-solid fa-font-awesome"></i> Font Awesome](https://fontawesome.com/) icons

---
[Pandoc]: https://pandoc.org
[reveal.js]: https://revealjs.com
[task]: https://taskfile.dev/
[Font Awesome]: https://fontawesome.com/
