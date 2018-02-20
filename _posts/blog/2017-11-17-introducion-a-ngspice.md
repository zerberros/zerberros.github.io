---
layout: default
title: "ngspice:00 Introducción a ngspice"
date: 2017-11-17
resumen: Primara entrada de una serie de tutoriales sobre simulación de circuitos electrónicos con ngspice.
category: blog
---


## Introdución a NGSPICE    


Ngspice (Next Generation Simulation Program with Integrated Circuits Emphasis ) es un programa para la simulación de circuitos electrónicos lineales y no lineales con propósito general.

### Origen

La primera versión de spice, (spice1), fué liberada bajo dominio público en el año 1972 por la universidad de California en Berkeley y fué escrita en Fortran. En 1996 se lanzó la última versión de spice por parte de la universidad, la cual, se reescribió en C y se  liberó bajo la licencia BSD, lo que permitió que numerosas empresas continuaran desarrollando spice con cambios de licencia a software cerrado (LTSpice, PSpice, Altium, Proteus, Tina, etc, ...), o manteniendo la misma licencia original, como es el caso de ngspice.

### Características

Ngspice soporta una gran cantidad de elementos como resistencias, condensadores, bobinas, bobinas acopladas, fuentes de tensión y de corriente tanto independientes como independientes, líneas de transmisión con y sin pérdidas, interruptores controlados por tensión o por corriente, diodos, transistores BJT, JFETs, MESFETs y MOSFETs.

Ngspice trae además una biblioteca de 'modelos-código' gracias a la extensión Xspice, que complementan ngspice y se utilizan de manera muy similar a los componentes antes citados.
Éstos modelos incluyen suma de señales, multiplicación, división, limitador, bloque de histéresis, integración, derivación, ecuaciones en dominio-S, etc, etc, ... y por la parte digital, incluye buffer, inversor, puertas And, Nand, Or, Xor,... , Triestado, pullup, pulldown, FlipFlops, D Latch, etc, etc.

Además se pueden encapsular subcircuitos, y usar ecuaciones en los parámetros de los componentes, y usar estructuras de control, tales como while, dowhile, if, goto, etc, etc. y por si fuese poco, también se pueden añadir componentes escritos en Verilog.

Ngspice soporta además las siguientes simulacines:

* Análisis en corriente contínua
* Análisis de pequeña señal en corriente alterna
* Análisis temporal
* Análisis de polos y ceros
* Análisis de distorsión en pequeña señal
* Análisis de ruidos

### Interfaz Gráfica de Usuario

Sin embargo, pese a que la mayoria de las soluciones han incorporado una capa de abstración visual, donde los componentes se usan por su símbolo gráfico, ngspice se sigue usando en modo texto, y aunque esta característica pueda parecer una desventaja, lo cierto es que si se llega a dominar, ngspice puede llegar a ser la herramienta de simulación más potente de todas.

Pero no perdamos el norte, porque las soluciones privativas transforman el esquemático en el fichero de texto plano que podremos ver, y que es o será, el que  procese el motor de spice, y por otra parte,  ngspice también puede hacer uso de diferentes interfaces gráficas para crear esquemas y poder posteriormente simularlos (gschem, kicad, etc).

No obstante, tanto en aplicaciones privativas como en las interfases gráficas para ngspice, es casi seguro que tendremos que añadir manualmente alguna línea de spice, o editar los parámetros de algún componente, por lo que sea cual fuere la solución que se vaya a usar, siempre que esté basada en spice3f5, conviene saber como se escriben los archivos de nodos, y cuales son sus principales directrices.

### Funcionamiento interno

Supongo que al lector que ha llegado hasta aqui, no le sorprenderá saber que ngspice utiliza las mismas [leyes de Kirchhoff](https://es.wikipedia.org/wiki/Leyes_de_Kirchhoff) que ya habrá estudiado en Teoria de Circuitos. Para cada punto de tiempo, ngspice tiene que crear una matriz y resolverla. Adicionalmente se usa el algoritmo de [Newton-raphson](https://es.wikipedia.org/wiki/M%C3%A9todo_de_Newton) para resolver ecuaciones no lineales que surgen de la descripción de los circuitos.

En las partes digitales, no se utilizan las leyes de kirchoff, y además, sólo se evalúan cuando se produce un evento, por lo que la simulación es considerablemente más rápida.

No soy muy experto en el funcionamiento interno de ngspice, asi que aprovecho para despedirme pedir disculpas por los posibles fallos y fallas que seguramente habrá en esta serie de tutoriales. Nos vemos dentro de poco en el primer videootutorial ;).

Un saludo.
