---
layout: default
title: "ngspice:02 Simulaciones. Parte 1."
date: 2018-04-04
resumen: Cómo funciona una Análisis de punto de trabajo, análisis transitorio, y un análisis de pequeña señal.
category: blog
---

# {{ page.title  }}


## Análisis OP, o 'punto de operación':


Un análiisis del punto de trabajo sirve para simular un circuito en régimen permanente, es decir, sólo con fuentes contínuas, con los condensadores abiertos y las bobinas cortocircuitadas.

Para relizar ésta simulación debemos escribir:
```
op
```
dentro de las etiquetas \<*.control*\> y \<*.endc*\> o antecedido de un punto si lo escribimos fuera de esas equiquetas.

Para mostrar el valor de cualquier nodo, se escribe:

```
print V(nodo1), V(nodo2), <V(nodo3)>
```

o simplemente:

```
print nodo1, nodo2, <nodo3>
```


Evidentemente, al ser régimen permanente, el intérprete devolverá un único valor por nodo.

## Análisis DC

Éste análisis es muy similar al anterior, sólo que en vez de usar el parámetro 'DC' de las fuentes, se podrá usar un barrido de valores. También se puede realizar el barrido sobre el valor de una resistencia o sobre la temperatura del circuito.

```
.dc srcnam vstart vstop vincr [src2 start2 stop2 incr2]
```

\<*srcnam*\> es el nombre de la  fuente de tensión o de corriente independiente, el nombre de la resistencia o la temperatura del ciscuito, en este caso \<*TEMP*\>. Una segunda fuente puede ser añadida con sus correspondientes parámetros de barrido. En este caso, la primera fuente hace un barrido para cada valor de la segunda fuente.

\<*vstart*\>, \<_vstop_\> y \<*vincr*\> son el primer valor, el último, y el incremento, respectivamente.

## Análisis transitorio

En el análisis transitorio se busca la respuesta de un circuito durante un tiempo determinado.

La sintaxis es la siguiente:

```
.tran tstep tstop <tstart <tmax >> <uic>
```

Donde \<*tstep*\> es el incremento de tiempo para cada iteracción de la simulación, aunque ngspice podrá hacer cálculos para incrementos de tiempo menores, si es necesario.

\<*tstop*\> es el tiempo final de la simulación, y \<*tstart*\> , opcional, es el tiempo en el que comience la simulación. En caso de omitirse será cero.

\<*tmax*\> se utiliza cuando se desea un tiempo de cálculo, menor que el del intervalo de impresión, es opcional y no se suele usar.

\<*uic*\> (uso de condiciones iniciales) se utiliza cuando se utilizan condiciones iniciales. Por ejemplo, para definir la tensión en un condensador, o la corriente de una bobina. Éstas condiciones iniciales se indican en cada componente que lo admita mediante el parámetro \<*IC=...*\>, o en la línea .ic (se tratará más adelante).

Hay que tener en cuenta que si \<*tstart*\> es distinto de cero, el análisis se realiza desde el tiempo cero, pero no se guardan los valores, por lo que el uso de las condiciones iniciales puede ayudar a ahorrar tiempo de cómputo.  


## Análisis AC: Análisis de pequeña señal o barrido de frecuencias.

En un análisis AC o de 'pequeña señal', lo que se hace es calcular la ganancia que tiene un circuito, para diferentes frecuencias, sobre un punto de trabajo. Ésto es especialmente útil si se quiere simular por ejemplo un filtro de sonido, una etapa de audio, etc. en donde un análisis transitorio aporta realmente poca información.

```
.ac dec nd fstart fstop
.ac oct no fstart fstop
.ac lin np fstart fstop
```

En donde \<*dec*\> es una progresión logaritmica en base 10 (10, 100, 1000, ...), \<*oct*\> es una progresión logaritmica en base 2 (2,4,8,16,...) , y \<*lin*\> es una progresión lineal (10,20,30,...). \<*nd*\>, \<*no*\>, y \<*np*\> son el número de puntos por década, por octava, y totales respectivamente.

Como lo que estamos calculando es una ganancia, querremos calcularla en decibelios. En este caso, la orden de impresión por pantalla deberá ser tal que así:

```
plot db(nodo1)
```

y para calcular la fase (en radianes):

```
plot phase(nodo1)
```
Efectivamente podremos aplicar ecuaciones a los vectores de salida, pero todo a su tiempo.


Ya que una ganancia es el cociente de la salida entre la entrada, deberemos añadir a nuestra fuente de tensión o intensidad el parámetro: \<*ac 1*\> dónde el "1" no indica necesariamente 1V, sino que más bien indica que el denominador es 1, y si por ejemplo, se pone 0.1, la ganancia será 10 veces mayor, lo que podrá llevar a confusiones.

En el ejemplo:
```
v01 nodo_1 nodo_2 DC 5 ac 1
```
al calcular en barrido de frecuencias, el parámetro \<*DC 5*\> se ignorará.
