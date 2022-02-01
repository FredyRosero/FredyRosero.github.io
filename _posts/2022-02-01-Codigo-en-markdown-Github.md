---
title: Frágmento de código (code snippet) en markdown Github
author: Fredy Rosero
status: published
date: '2022-01-29'
layout: post
tasg: code-snippet
---
## Markdown
Markdown permite insertar bloques de código envueltos por ``` o `~~~`. Por ejemplo escribir el documento el siguiente fragmento
~~~markdown
```python
foo = "hola"
bar = ", mundo!"
print '{0}{1}'.format(foo,bar)
```
~~~
nos renderiza en HTML un bloque de código python con sintáxis resaltado
```python
foo = "hola"
bar = ", mundo!"
print '{0}{1}'.format(foo,bar)
```
Esto nos permite utilizar un snippet de una manera sencilla, sin embargo, a veces queremos estilizar los snippets
## Gits
A continaución está un snippet en [Github Gits](https://gist.github.com/FredyRosero/46d12851134003dabeeb5b56d389e69f) escrito como:
```html
<script src="https://gist.github.com/FredyRosero/46d12851134003dabeeb5b56d389e69f.js"></script>
```
Resultado:
<script src="https://gist.github.com/FredyRosero/46d12851134003dabeeb5b56d389e69f.js"></script>

## Ideone
A continaución está snippet en [ideone.com/kKxFrr](https://ideone.com/kKxFrr) escrito como:
Código:
```html
<script src="https://ideone.com/e.js/kKxFrr" type="text/javascript" ></script>
```
Resultado:
<script src="https://ideone.com/e.js/kKxFrr" type="text/javascript" ></script>

## Trinket
Trinket permite no solo mostrar el código sino además muestra la salida del programa
Código:
```html
<iframe src="https://trinket.io/embed/python/5ce18dede7?toggleCode=true&runOption=run" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
```
Resultado:
<iframe src="https://trinket.io/embed/python/5ce18dede7?toggleCode=true&runOption=run" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
\
Lamentablemente
