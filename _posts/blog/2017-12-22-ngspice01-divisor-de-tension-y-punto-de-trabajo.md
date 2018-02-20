---
layout: default
title: "ngspice:01 Divisor de tensión y punto de trabajo"
date: 2017-12-22
resumen: Estructura y sintaxis básica de los archivos nodos y simulación del punto de trabajo.
category: blog
---


## NGSPICE01: Divisor de tensión y simulación del Punto de operación



<iframe width="650" height="366" src="https://www.youtube.com/embed/4tUSx0qRLXY" frameborder="0" allowfullscreen> </iframe>

** NOTA: Éste vídeo será reemplazado en un futuro debido a la presencia de algunos fallos y carencia de calidad.
**
### En resumen:


* La primera línea del archivo de nodos se reserva para el nombre del circuito.

* Los comentarios de línea empiezan con un asterisco <*>, y los comentarios que se colocan al final de una línea van detrás del signo dolar <$>.

```ngspice
* esto es un comentario en linea
V1 n01 n02 100 $ Comentario al final de linea que define una fuente de tensión.
```

* La última línea del archivo de nodos es:

```
.end
```

* Los componentes se definen por la primera letra del nombre de su instancia, seguido de los nodos y los parámetros. Ejemplo:

```spice
r01 n01 n02 25000 $ esto es una resistencia porque el nombre de la instancia empieza por r.
```

* Los comandos que deberá ejecurar el intérprete irán precedidos por un punto o entre las líneas <.control> y <.endc>

* También podremos ejecutar comandos directamente desde el intérprete.

* Por defecto, ngspice guarda sólo los las tensiones de los nodos y las intensidades a través de las fuentes de tensión independientes. Implicitamente definido por el comando:

```
save all
```

* Para guardar las corrientes que pasan a través de todos los componentes, deberemos escribir el siguiente comando, preferiblemente entre las líneas <.control> y <.endc> :

```
options savecurrents
```

* Para guardar otros parámetros se escribirá de la siguiente forma:  < save @componente[parametro] >  por ejemplo:

```
save all @r01[i] @r02[p]
```

* Una simulación OP, determina el punto de trabajo del circuito en corriente contínua con las bobinas cortocircuitadas y los condensadores abiertos.

* Otros comandos que se han visto son:

```
source archivodenodos.cir $ carga un nuevo archivo de nodos

print V(n01) $ imprime por pantalla la tensión del nodo n01

exit $ sale del interprete
```
