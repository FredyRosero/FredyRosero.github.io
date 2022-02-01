---
title: Latex en markdonw de repositorio Github 
author: Fredy Rosero
tags: 'GitHub Latex'
status: published
date: '2022-02-01'
layout: post
---

Si revisamos este documento directamente en el repositoriode Github notaremos que expresiones como la acontinuación no se renderizan en *LaTeX*

 La *función Gamma* satisface $\Gamma(n) = (n-1)!\quad\forall
 n\in\mathbb N$ por medio dela integral de Euler $$ \Gamma(z) = \int_0^\infty
 t^{z-1}e^{-t}dt\,. $$

GitLab por su lado tiene la capacidade de renderizar bloques con la siguiente sitáxis
```math
e^{i \pi} = -1
``` 
## Imágen GFM
Sin embargo, podemos utilizar APIs que reciban el contenido LaTeX como variable GET y que devuelan una imagen, y así insertar la imagen en el MD como elemento img HTML: 

Código: 

```HTML
<img src="https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1">
```

Resultado:

<img src="https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1">

Si queremos utilizar la sintaxis de imagen GFM (GitHub Flavored Markdown) [[4]](#4) necesitamos codificar en URL UTF-8 el contenido LaTeX o de lo contrario tendremos problemas de renderización en Stackedit y directamente en Github `https://github.com/username/username.github.io.git` sin embargo no en GHP `https://username.github.io.git`

Código: 

```markdown
![e^{i \pi} = -1](https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1)
```
Resultado:

![e^{i \pi} = -1](https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1)

Podemo utilizar herramientas en linea como [urlencoder.org] para codificarel texo correctamente (https://www.urlencoder.org/enc/latex/)

Código: 

```markdown
![e^{i \pi} = -1](https://render.githubusercontent.com/render/math?math=e%5E%7Bi%20%5Cpi%7D%20%3D%20-1)
```

Resultado:

![e^{i \pi} = -1](https://render.githubusercontent.com/render/math?math=e%5E%7Bi%20%5Cpi%7D%20%3D%20-1)

Podemos utilizar un [código sencillo](https://jsfiddle.net/faroseroc/jt6vL3dr/17/) para generar nuestras imágenes GFM a partir de LaTeX
<iframe width="100%" height="300" src="//jsfiddle.net/faroseroc/jt6vL3dr/17/embedded/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## Ejemplo

La *función Gamma* satisface <img src="https://render.githubusercontent.com/render/math?math=%5Ccolor%7Bgray%7D%20%5CGamma(n)%0A%3D%20(n-1)!%5Cquad%5Cforall%20n%5Cin%5Cmathbb%20N">
 por medio dela integral de Euler  
<p align="center"> 
 <img src="https://render.githubusercontent.com/render/math?math=\LARGE \color{gray} \Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,."> </p>