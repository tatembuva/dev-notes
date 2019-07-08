## ✏️
### NeoVim Cheat Sheet
*Key bindings for my neovim config*

[*back*](../README.md)

---

#### Sections
- [Snippets](#snippets)
- [Common](#common)
- [Macros](#macros)
- [Movement](#movement)
- [Markdown](#markdown)
- [Folding](#folding)
- [Random](#random)

#### Random

_File Format_, change the line ending of a file that was edited on a windows machine...Really annoying, I should just write a function that does this whenever a file is opened.
q`` vim
:set ++ff=dos
```
_Light/Dark_, change the background to light or dark, using the solarized color scheme and it just works, makes it easy to quickly switch the theme...
``` vim
:set background=light
:set background=dark
```
