---
title: Introducción a desarrollo de Android Studio
author: FredyRosero
tags: [tag1, tag2]
date: 2022-05-23
layout: post
categories: [category]
excerpt_separator: <!--more-->
---

![thumbnail del post](assets/default-banner.jpg)

Abstract: poner un resumen de pocas lineas acá.
<!--more-->

## Section 1
Recuerda definir la variable `GIT_USER` en el perfil de tu shell
```bash
echo export GIT_USER=MyGithubUser >> ~/.bashrc
source ~/.bash_profile
```

o de manera temporal
```bash
GIT_USER=MyGithubUser
echo $GIT_USER
```

### Subsection 1.1
Body of Section 1.1   

## Section 2
Cuerpo de la sección 2 $\mathrm{e} = \sum_{n=0}^{\infty} \dfrac{1}{n!}$ con ecuación en línea.
A continuación un bloque de ecuaciones alineadas:
$$
\begin{align}
Then,\ (x+z)+t & = x+(z+t)\ (\because Rule2) \\
& = x+0_V \\
& = x\ (\because Rule3) \\
\end{align}
$$

## Sección 3
A continuación un diagrama renderizado de Github. 

https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/
<div class="mermaid">
flowchart TD
    View --> ViewModel
    ViewModel --> Model
    MO -- Room --> F[SQLite]
    RD -- Retrofit --> WS[Webservice]
    CF --> RS[res]
subgraph View
    AC[Activity]
    AC2[Activity]
    FR1[Fragment]
    FR2[Fragment]
    FR3[Fragment]
    AC --> FR1 & FR2 & FR3
end
subgraph ViewModel
    LD1[LiveData]
    LD2[LiveData]
    LD3[LiveData]
end
subgraph Model
    RE[Repository]
    MO[Model]
    RD[Remote data source]
    CF[App config]
    RE --> MO & RD & CF    
end
</div>

