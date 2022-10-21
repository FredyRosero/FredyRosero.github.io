---
title: Jekyll para Github Pages
author: Fredy Rosero
tags: [jekyll, GitHub, GitHub-pages]
date: 2022-05-12'
layout: post
categories: [jekyll]
excerpt_separator: <!--more-->
---
![github pages + jekyll](/assets/github%20pages%20%2B%20jekyll.jpg)

Abstract.
 <!--more-->

## Creación del repositorio remoto del sitio
Debes crear un repositorio con nombre `nombredeusuario.github.io` donde "nombredeusuario" es tu usuario de github o el usuario de la organización si es el caso. Por ejemplo `FredyRosero.github.io`.

Luego en `Settings > Code and autoamtion > Pages` escoges un tema

## Instalación de Jekyll
Sique las intrucciones de como instalar Jekyll con Ruby. Luego instalaremos 
```bash
gem install github-pages
```


## Agregar dependencias a tu repositorio local
Al clonar el repositorio en tu máquina con `git clone https://github.com/FredyRosero/FredyRosero.github.io.git` algunos archivos quedan faltando para que Jekyll pueda trabajar. Para instalar las dependencias faltantes vamos a ejecutar el siguiente comando

```bash
jekyll new --skip-bundle . --force
```

Esto modificará y agregará algunos archivos
```bash
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   .gitignore
    modified:   _config.yml
    modified:   index.markdown

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    404.html
    Gemfile
    Gemfile.lock
    _posts/2022-08-17-welcome-to-jekyll.markdown
    about.markdown

no changes added to commit (use "git add" and/or "git commit -a")

```

Queremos restaurar el archivo `index.markdown` con `git checkout -- index.markdown`. Tambien vamos a eliminar `_posts/2022-08-17-welcome-to-jekyll.markdown` y `about.markdown`.

## Reconfigurando el sitio
En el archivo `Gemfile` Comenta la línea `gem "jekyll"` y agrega `gem "github-pages", group: :jekyll_plugins `

Para los temas en `_config.yml`
```yaml
remote_theme: pages-themes/hacker@v0.2.0
plugins:
- jekyll-remote-theme # add this line to the plugins list if you already have one
```

El plugin `ekyll-remote-theme` tambien debe ser agregado al `Gemfile`
```Gemfile
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-remote-theme"
end
```

Necesitas tambien en `_config.yml` agregar la metadata de Github. la cual contiene datos como la Authenticación de la API de Github:
```yaml
github: [metadata]
```

Elmina el archivo `Gemfile.lock` es instala las (nuevas) dependencias con `bundle install`.

Recuerda actualizar el `layout` de tus markdowns con los disponibles en tu tema. Por ejemplo el tema [hacker](https://github.com/pages-themes/hacker/tree/master/_layouts) solo tiene `default` y `page`. Puedes definir el *layout* por defecto en `_config.yml` con
```yaml
defaults:
  -
    scope:
      path: "" # an empty string here means all files in the project
    values:
      layout: "default"
```



## Lanzamiento local de Github Page
Ahora podemos copmilar o servi
```bash
cd ~/.../FredyRosero.github.io
bundle exec jekyll serve
```

## Valores por defecto
https://jekyllrb.com/docs/configuration/front-matter-defaults/

## Posts

https://jekyllrb.com/docs/posts/

### Drafts
```bash
jekyll serve --drafts
```

## Front Matter

https://jekyllrb.com/docs/front-matter/