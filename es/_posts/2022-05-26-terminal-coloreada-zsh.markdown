---
layout:     post
title:      "Terminal coloreada con zsh"
subtitle:   "para las últimas versiones de macOS"
date:       2022-05-26 01:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-17.jpg"
locale:     es
lang-ref:   colored-terminal-zsh
---

Las últimas versiones de **macOS** tienen instalada el _zsh_ por defecto, en vez del tradicional _bash_. Mejor que volver a instalar _bash_, es usar un nuevo sistema para colorear la Terminal de _zsh_.

Empieza por crear un fichero llamado `.zshrc` en tu path `$HOME`, con el siguiente contenido (después, reinicia la terminal):

```sh
LS_COLORS='no=00;37:fi=00:di=00;33:ln=04;36:pi=40;33:so=01;35:bd=40;33;01:'
export LS_COLORS
export CLICOLOR=1
zstyle ':completion:*' list-colors ${(s.:.)LS_COLORS}
PROMPT='%F{green}%n@%m%k %B%F{cyan}%(4~|...|)%3~%F{white} %# %b%f%k'
```

## Documentación adicional
- [How Do I Change My ZSH Prompt Name](https://linuxhint.com/change-zsh-prompt-name/)
- [Zsh not recognizing ls colors](https://superuser.com/questions/700406/zsh-not-recognizing-ls-colors)