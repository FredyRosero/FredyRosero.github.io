---
title: Latex en Github Page
author: Fredy Rosero
tags: 'GitHub Jekyll Latex Katex'
status: published
date: '2022-01-29'
layout: post
---

Podemos incertar ecuaciones en línea como $E=mc^2$ y tambien podemos insertar bloques de ecuaciones como:

$$
\begin{align}
\dot{x} &amp; = \sigma(y-x) \\
\dot{y} &amp; = \rho x - y - xz \\
\dot{z} &amp; = -\beta z + xy
\end{align}
$$

Si visualizamos este documento desde el repositorio de Github notaremos que Github por defecto no renderiza esta ecuaciones a diferencia de GitLab. Pero detras de la funcionaiidad Githbu Page está Jekyll que simplemente compila un sitio HTML a patir de Markdown. Un sitio basado en Jekyll (como los de Github Page) utiliza *includes* que son simplemente fragmentos HTML, que es pueden reutilizar en los *layouts* que son plantillas HTML. Un caso en particular es el `_includes/head-custom.html` que está referenciado por la mayoria de temas de Jekyll-Github. Es en este archivo donde podemos incrustos scripts de Javascript como *KaTeX*. Así un parte del archivo luciría así:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.15.2/dist/katex.min.css" integrity="sha384-MlJdn/WNKDGXveldHDdyRP1R4CTHr3FeuDNfhsLPYrq2t0UBkUdK2jyTnXPEK1NQ" crossorigin="anonymous">
<!-- Se obtiene el JS en paralelo con el renderizado del DOM HTML y se ejecuta una vez se haya cargado el DOM -->
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.2/dist/katex.min.js" integrity="sha384-VQ8d8WVFw0yHhCk5E8I86oOhv48xLpnDZx5T9GogA/Y84DcCKWXDmSDfn13bzFZY" crossorigin="anonymous"></script>
<!-- Extension de KaTeX para autorenderizar sintaxis LaTeX -->    
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.2/dist/contrib/auto-render.min.js" integrity="sha384-+XBljXPPiv+OzfbB3cVmLHf4hdUFHlWNZN5spNQ7rmHTXpd7WvJum6fIACpNNfIR" crossorigin="anonymous"></script>
<!-- Para configurar y ejecutar la extensión de autorenderizar una vez se haya cargado el DOM  -->
<script>
document.addEventListener("DOMContentLoaded", function() {
    renderMathInElement(document.body, {
        // customised options
        // • auto-render specific keys, e.g.:
        delimiters: [
            {left: '$$', right: '$$', display: true},
            {left: '$', right: '$', display: false},
            {left: '\\(', right: '\\)', display: false},
            {left: '\\[', right: '\\]', display: true}
        ],
        // • rendering keys, e.g.:
        throwOnError : false
    });
});
</script>    
```

Mas info en [katex.org/docs/autorender.html](https://katex.org/docs/autorender.html)