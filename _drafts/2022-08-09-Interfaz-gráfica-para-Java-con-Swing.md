---
title: Interfaz gráfica para Java con Swing
author: FredyRosero
tags: [tag1, tag2]
date: 2022-08-09
layout: post
categories: [category]
excerpt_separator: <!--more-->
---

![thumbnail del post](assets/default-banner.jpg)

Abstract: poner un resumen de pocas lineas acá.
<!--more-->

## Introducción
Swing es una librería de controles gráficos para Java.

## Hola mundo
Creamos un carpeta llamada `start` y dentro de la misma un archivo llamado `HelloWorldSwing.java`. En un editor de texto o preferiblemente un IDE ingresamos al archivo lo siguiente
```java
package start;

import javax.swing.*;

public class HelloWorldSwing {

    private static void createAndShowGUI() {
        JFrame frame = new JFrame("HelloWorldSwing");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        JLabel label = new JLabel("Hello World");
        frame.getContentPane().add(label);
        frame.pack();
        frame.setVisible(true);
    }

    public static void main(String[] args) {

        createAndShowGUI();

    }
}
```

En una consola vamos a el directorio `src` y ahí compilamos con

```bash
javac start/HelloWorldSwing.java
```

para luego ejecutar el bytecode con 

```bash
java start.HelloWorldSwing
```

### JFrame

https://docs.oracle.com/javase/7/docs/api/javax/swing/JFrame.html

![El panel raíz y sus partes](https://docs.oracle.com/javase/tutorial/figures/uiswing/components/1layers.gif)

