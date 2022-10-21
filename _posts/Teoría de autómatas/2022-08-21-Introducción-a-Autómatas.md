---
title: Introducción a Autómatas
author: 
tags: [autómatas]
date: 2022-08-21
layout: post
categories: [Ciencia de la computación teórica, Teoría de la computación, Teoría de autómatas]
excerpt_separator: <!--more-->

---

Abstract: poner un resumen de pocas lineas acá.
<!--more-->

## Alfabetos y símbolos
Los **alfabetos** son conjuntos finitos de **símbolos** denotados por lo general con Sigma. Al ser conjuntos, podemos denotar los símbolos que componen el alfabeto por notación extensional o enumeración o lista (*roster notation*):
* ~$\Sigma=\\{0,1\\}~$ es el alfabeto de los dígitos binarios. En este alfabeto solo vemos dos símbolos: 0 y 1.
* ~$\Sigma=\\{a,b,c,d,e,f,g,h,i,j,k,l,m,n,ñ,o,p,q,r,s,t,u,v,w,x,y,z\\}~$ es el alfabeto de los caracteres minúscula del alfabeto español.
* ~$\Sigma=\\{0,1,2,3,4,...\\}~$ es el alfabeto de los enteros no negativos.

Podemos también utilizar definición intensiva semántica (*semantic definition*) para definir los símbolos que componen el alfabeto: ~$\Sigma=~$"Dígitos del sistema decimal", el cual tendría por definición extensional sería ~$\\{0,1,2,3,4,5,6,7,8,9\\}~$.

Otra forma es utilizar definición intensiva por compresión (*set-builder notation*): ~$\Sigma=\\{n : n\text{ es entero, y } 0 \leq n \leq 5\\}~$, el cual por definición extensional sería ~$\\{0,1,2,3,4,5\\}~$.


## Cadenas o palabras
Una **cadena** (*string*) ~$w~$, también llamada **palabra** (*word*), sobre un **alfabeto** ~$\Sigma~$, es una secuencia finita de **símbolos** tomados de ese alfabeto ~$\Sigma~$. Por ejemplo
* "~$101~$" es un cadena sobre el alfabeto ~$\\{0,1\\}~$.
* En cambio "~$102~$" NO es un cadena sobre el alfabeto ~$\\{0,1\\}~$, pero si sobre el alfabeto ~$\\{0,1,2,3,4,5,6,7,8,9\\}~$ 
* "~$reconocer~$" es una cadena sobre el alfabeto ~$\\{a,b,c,d,e,f,g,h,i,j,k,l,m,n,ñ,o,p,q,r,s,t,u,v,w,x,y,z\\}~$ pero no del alfabeto ~$\\{a,e,i,o,u\\} ~$.
* "~$aaa~$" es una cadena sobre el alfabeto ~$\\{a,b,c,d,e,f,g,h,i,j,k,l,m,n,ñ,o,p,q,r,s,t,u,v,w,x,y,z\\}~$ y a su vez del alfabeto ~$\\{a,e,i,o,u\\} ~$.

La longitud de una cadena, denotada como ~$|w|~$, es la cantidad de símbolos de ~$\Sigma~$ presentes en la cadena ~$w~$. Así, si ~$w=~$"aaa", entonces, ~$|w|=3~$. Si ~$|w|=0~$, entonces estamos hablando de la cadena vacía denotada como ~$\varepsilon~$.
## Lenguajes
Un **lenguaje** ~$L~$ es un conjunto de cadenas formadas por un alfabeto ~$\Sigma~$.
## Automata finito 

Un autómata de estado finido es una tupla $$\cal{M}=\{Q,\Sigma, \delta,q_0,F\}$$, tal que: 
* $$Q$$ es un conjunto finito de estados internos
* $$\Sigma$$ es un conjunto finito de caracteres llamados la entrada del alfabeto de $$\cal{M}$$.
* $$q_0\in Q$$ es el estado inicial.
* $$F\subset Q$$ es un conjunto de estados de aceptación 
* $$\Sigma$$ es la función de transición de $$\cal{M}$$, la cual es una función del conjunto $$Q\times \Sigma$$ a el conjunto $$Q$$. Note que un elemento de $$Q\times \Sigma$$ es una tupla $$(q,a)$$, $$q\in$$,  $$a=w[i]$$.
     

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

## Operación de concatenación

## Estrella de kleene


