---
title: Frágmentos de código (code snippets) en Github Page (Jekyll)
author: Fredy Rosero
status: published
date: '2022-01-29'
layout: post
categories: Github
tags: code-snippet github-page gits ideone trinket jekyll
---
## Markdown
Markdown permite insertar bloques de código envueltos por tres signos [acento grave](https://es.wikipedia.org/wiki/Acento_grave) (en inglés *backtick*) o tres signos [tilde de eñe](https://es.wikipedia.org/wiki/Virgulilla) (en inglés *tilde*). Por ejemplo, al escribir en el documento el siguiente fragmento
~~~markdown
```python
foo = "hola"
bar = ", mundo!"
print '{0}{1}'.format(foo,bar)
```
~~~
se nos compila en HTML un bloque `<pre>` con el código y su sintáxis resaltada para python
```python
foo = "hola"
bar = ", mundo!"
print '{0}{1}'.format(foo,bar)
```
Esto nos permite utilizar un snippet de una manera sencilla y visibles tanto en un repositorio de Github como en una Githbu Page.

## Snippets externos
En el caso de que quisieramos insertar un fragmento de código alojado de manera externa podemos utilizar *Gist* de Github o *Ideone*. La limitante aquí es que al ser scripts no se ejecutarían en el repositorio por razones de seguridad.

A continaución está un snippet en [Github Gits](https://gist.github.com/FredyRosero/46d12851134003dabeeb5b56d389e69f) escrito como:
```html
<script src="https://gist.github.com/FredyRosero/46d12851134003dabeeb5b56d389e69f.js"></script>
```
Resultado:
<script src="https://gist.github.com/FredyRosero/46d12851134003dabeeb5b56d389e69f.js"></script>

\
[Ideone](https://ideone.com/) por su parte, nos permite compilar e interpretar códigos desde su sitio web  y además guardarlos en una cuenta de usuario. Cada código puede ser insertado en un snippet de tema blanco. A continaución un snippet en [ideone.com/kKxFrr](https://ideone.com/kKxFrr):
```html
<script src="https://ideone.com/e.js/kKxFrr" type="text/javascript" ></script>
```
Resultado:
<script src="https://ideone.com/e.js/kKxFrr" type="text/javascript" ></script>

## Snippet con salida
Trinket al igual que Ideone es una platamforma para compilar e interpretar código online. La ventaja de un snippet Trinket, es que permitee no solo mostrar el código sino además nos permite correr el programa para ver la salida del programa, en realidad tenemos un `<iframe>` con una versión compacta de su aplicación web.
Código:
```html
<iframe src="https://trinket.io/embed/python3/d58e1cf1a9?runOption=run" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
```
Resultado:
<iframe src="https://trinket.io/embed/python3/d58e1cf1a9?runOption=run" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

\
Lamentablemente Trinket solo permite a los usuarios gratiutos guardar códigos en *Python 2*. Para poder gestionar códigos en además Pygame, R o Java se debe mejorar la cuenta a un [plan Code+ de 3 USD por mes](https://trinket.io/plans).

