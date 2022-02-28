---
title: Análisis geométrico de un softbox para su fabricación
author: Fredy Rosero
tags: 'matemáticas, softbox, frustum, pirámide'
date: '2022-02-27'
layout: post
category: matemáticas
---

![Tronco de pirámide cuadrada de un softbox](https://docs.google.com/drawings/d/e/2PACX-1vTTa4TjiFSqIUGVfC5KPJpTd1300vcSihWxw1kiutRjzXbqL0YtNOyKaYaxX0SnVcA15Y-QPILm_YWE/pub?w=540&h=543)

A continuación se desarrollará un análisis geométrico del diseño de un [softbox](https://es.wikipedia.org/wiki/Soft_box) o caja difuminadora de luz.

## Luz suave y luz dura

La luz suave en fotografía se caracteriza por tener sombras son bordes muy difuminados, a diferencia de la luz dura donde los bordes de las sombras son mas definidos y rellenadas.

![Luz suave y dura](https://docs.google.com/drawings/d/e/2PACX-1vTSgpnfd_sLX7TMRjzVl1OuphWVg1Nar8K009bywwZTe4gdtV4jcS06LMA1pM4Fuxi0cAN6VDG6Gl39/pub?w=575&amp;h=262)
## Softbox
Un softbox en si es una caja o paraguas con una piel interna reflectora que envuelve un bombillo, y da paso a su luz a través de una capa difusora de luz.

## Difusor de luz

Un difusor de luz nos permite dispersar (el angulo de) los rayos de la fuente de luz
![Bombilla con y sin difusor](https://docs.google.com/drawings/d/e/2PACX-1vRZD_kufz5mqlaFwVvrIc_mnGqraplcj1nNbJJixVwvlKfkBzmkfj_SZLHJClr4BkNQHKDZ2JwpXPoe/pub?w=477&amp;h=287)
## Reflector de luz

Un reflector nos permite redirigir los rayos de una fuente de luz para aplicarlos a otro angulo. 

#### Angulo de reflexión
![Ley de la reflexión](https://docs.google.com/drawings/d/e/2PACX-1vQBIChBiNabVkSD4UMlu1-e5ltWADRvid5qI1BwDoP5w10HHOtGCB1kPt9Jar8dFwNdmWECxEn8K5_H/pub?w=346&amp;h=279)
El angulo de rayo de luz con respecto a la perpendicular de la superficie que incide es equivalente al angulo de rayo de luz reflejado con respecto a la perpendicular de la misma superficie

<iframe width="560" height="315" src="https://www.youtube.com/embed/OPppoNyZoPE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Para la imagen a continuación en (a) tenemos una iluminación radial que irradia luz en todas las direcciones. En (b) podemos aprovechar los rayos que se emiten hacia la derecha y no hacia el objetivo, re-dirigiéndolos hacia el objetivo con una superficie reflectora en un angulo de 45º con respecto al eje de apuntado. En (c.) podemos aprovechar aún mas la luz con dos superficies reflectoras, lo que nos disminuiría las sombras significativamente. 
 
![Bombilla con y sin reflectores latereales](https://docs.google.com/drawings/d/e/2PACX-1vSnW1ToduVsiTTD5dd560UatjQEmI0Jh48C_p-3rwADIAvqr2XhvyXG7CqnzanD0nc7ctXnOcDNNqrR/pub?w=673&amp;h=188)
Podemos inclusive pensar en 4 superficies reflectoras que envuelvan a la fuente de luz. Dicha unión de superficies nos daría una pirámide cuadrada si sus lados son iguales.

![Pirámide cuadrada](https://docs.google.com/drawings/d/e/2PACX-1vTsUqk_mPdNXDLuoGY2ohtIr2zBfdxLhqzBmBPNMpZ5CD2veEbd-3Cwx2Jgo0ldFZCCmk_hBH_s1oSk/pub?w=566&amp;h=280)
Necesitamos truncar la pirámide ya que no necesitamos la punta de la misma. El sólido resultante se conoce como tronco de pirámide. Mas info en [Tronco de pirámide (Wikipedia)](https://es.wikipedia.org/wiki/Tronco_de_pir%C3%A1mide).

### Tronco de pirámide cuadrada o Frustum cuadrado

Necesitamos entonces contruir un tronco de piramide cuadrada sin tapa inferior y superior y cuyas caras laterales tengan un ángulo de 45º con respecto a su eje de centroide.

![Tronco de pirámide cuadrada](https://docs.google.com/drawings/d/e/2PACX-1vRxEmi-h2ZPUAQOUcAmsP3b6EZ9m2QYxW8pB-rvnkgTif8TL1gnUw0dBTAJWguAEwR1TZsSJihHVC7q/pub?w=595&amp;h=310)
Los laterales de tronco son 4 trapecios isósceles, por lo que calcularemos dichos trapecios.


### Cálculo del trapecio

#### Condiciones
1. El trapecio a calcular caracteriza las caras de un tronco de pirámide cuadrada.
2. El trapecio que describe las caras del trapecio tiene base superior $b_2$ y base inferior $b_1$. 
3. La base superior es mas larga que la base inferior $b_2>b_1$.
4. El eje de apuntado es una recta que pasa por el centro de ambas bases del tronco de la pirámide.
5. El angulo entre la sus caras y el eje de apuntado es de 45º.

#### Desarrollo 

![Trapecio de tronco de pirámide](https://docs.google.com/drawings/d/e/2PACX-1vTx-J072YVylGCv_kPuYM1g_Lv2E8uLRpSxV_wNat-TYdbf20k8qS1TWEw5EJejd6jkywkGQvVX5hKl/pub?w=342&amp;h=206)

Si $A=(A_x,A_y,A_z)$ es un punto vértice de la base superior y $B=(B_x,B_y,B_z)$ es el punto vértice de la base inferior conectado a $A$ por medio de la arista $AB$, tenemos:

Componentes de A
$$
A_x = \frac{b_2}{2}, A_y =  \frac{b_2}{2}, A_z = h
$$

Componentes del punto B
$$
B_x = \frac{b_1}{2}, B_y = \frac{b_1}{2}, B_z = 0
$$

Puntos auxiliares
$$
A'=(A_x,A_y,B_z)\\
A''=(B_x,A_y,A_z)\\
A'''=(B_x,A_y,B_z)\\
$$
Se debe cumplir que entre la cara y el eje de apuntado haya un ángulo determinado
$$
tan(\alpha)=\frac{A''_y-B_y}{A_z}\\
tan(\alpha)=\frac{\frac{b_2}{2}-\frac{b_1}{2}}{A_z}\\
tan(\alpha)=\frac{b_2-b_1}{2h}\\
h=\frac{b_2-b_1}{2\cdot tan(\alpha)}\\
$$
Para $\alpha=45ª$, tenemos la altura del tronco a partir de sus bases
$$
h=\frac{b_2-b_1}{2}\\
$$
Para $\alpha=45ª$, la longitud de su vértice $AB$ es
$$
|AB|=\sqrt{(A_x-B_x)^2+(A_y-B_y)^2+(A_z-B_z)^2}\\
|AB|=\sqrt{3\frac{(b_2-b_1)^2}{4}}\\
|AB|=\frac{\sqrt{3}(b_2-b_1)}{2}\\
$$
Para $\alpha=45ª$, todas las caras del tronco son un trapecio isósceles de bases $b_1$ y $b_2$ y laterales de $|AB|$, cuya altura $h'$ es
$$
h'=|A''B|\\
|A''B|=\sqrt{(A''_x-B_x)^2+(A''_y-B_y)^2+(A''_z-B_z)^2}\\
|A''B|=\sqrt{(B_x-B_x)^2+(A_y-B_y)^2+\frac{(b_2-b_1)^2}{4}}\\
|A''B|=\sqrt{\frac{(b_2-b_1)^2}{4}+\frac{(b_2-b_1)^2}{4}}\\
|A''B|=\sqrt{\frac{(b_2-b_1)^2}{2}}\\
h'=\frac{b_2-b_1}{\sqrt{2}}\\
$$
<iframe src="https://www.geogebra.org/3d/z6cu7b7n?embed" width="800" height="600" allowfullscreen style="border: 1px solid #e4e4e4;border-radius: 4px;" frameborder="0"></iframe>

Para un trapecio con un ángulo de 45º tenemos entonces la altura  $z$ en función de sus bases $x$ y $y$
$$
z=f(x,y)=\frac{x-y}{\sqrt{2}}, x>y
$$
Donde $z$ es la variable dependiente y $x$ y $y$ son variables independientes. De la función anterior vemos que $y$ no puede ser mayor que $x$ ya que tendríamos una longitud negativa y que a mayor $x$ o $y$, mas grande será $z$. 

### Moldes de corte
Podemos ahora proyectar las caras del tronco en una superficie, para obtener nuestros moldes de corte. La manera mas eficiente para encajar las cuatro caras es en parejas una sobre la otra, compartido su lado mas ancho, donde en cada pareja, una de las caras esta girada 180°. Para el desarrollo de los moldes de corte debemos procurar que no se salgan de los limites de la superficie a cortar, pero a su vez debemos usar la mayor cantidad de superficie, por lo que nos apoyaremos de GeoGebra para realizar la tarea de manera visual. Por practicidad vamos representar solo una pareja, ya que no es necesario representar la segunda pareja para conocer el área total utilizada por las cuatro caras sobre un pliego para su corte:

<iframe src="https://www.geogebra.org/geometry/whahvyyy?embed" width="800" height="400" allowfullscreen style="border: 1px solid #e4e4e4;border-radius: 4px;" frameborder="0"></iframe>

El ensamblaje del softbox lo cubriremos a detalle en otro artículo.

## Resultados
Una vez cortado y ensamblado el softbox podemos apreciar su beneficios la iluminación de fotografía:

![](https://docs.google.com/drawings/d/e/2PACX-1vS2ZjkiJCVaMiR_wNvrwJDbUP0ebkv43novfnbKIJahCcjn29PY5VFmqynU6yG7ouRs5bqT7QSj4J6i/pub?w=517&h=518)


