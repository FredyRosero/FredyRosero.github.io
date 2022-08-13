---
title: Primeros pasos con TMux
author: FredyRosero
tags: [tag1, tag2]
date: 2022-08-10
layout: post
categories: [category]
excerpt_separator: <!--more-->
---

![thumbnail del post](assets/default-banner.jpg)

Abstract: poner un resumen de pocas lineas acá.
<!--more-->

## Dividir pantalla

## Soporte de mouse
En  ` ~/.tmux.conf`:
```
set -g mouse on
``` 

## Plugins
Instalar

https://github.com/tmux-plugins/tpm

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```


## Portapapeles
Para sistemas X11
```bash
sudo apt-get install xsel
```
https://github.com/tmux-plugins/tmux-yank
https://www.seanh.cc/2020/12/27/copy-and-paste-in-tmux/

En  ` ~/.tmux.conf`:
```
set -g mouse on

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-yank'
bind -T copy-mode    C-c send -X copy-pipe-no-clear "xsel -i --clipboard"
bind -T copy-mode-vi C-c send -X copy-pipe-no-clear "xsel -i --clipboard"

set -g @yank_action 'copy-pipe-no-clear'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

