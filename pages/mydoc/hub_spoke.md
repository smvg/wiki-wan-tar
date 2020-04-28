---
title: "Descripción general de Hub and Spoke"
keywords: sample homepage
tags: ["hub & spoke"]
sidebar: mydoc_sidebar
permalink: hub_spoke.html
summary: Descripción general de la topología Hub & Spoke
---

## Descripción general
El modelo de distribución "Hub and Spoke" tal y como describimos en el primer punto, utiliza una topología de estrella. Con esto se consigue que se reduzca el número de rutas para comunicar las diferentes redes entre sí.

El funcionamiento de este tipo de topologías funciona mejor cuando el punto intermedio se limita a interconectar todas las redes que residen en los extremos.

Este modelo de distribución es muy popular en la industria del transporte, tanto por aire, mar y tierra.

Un esquema de la topología de red "Hub and Spoke" lo podemos apreciar en la *Figura 1*. Aquí vemos la topología de estrella que sigue el esquema.

{% include image.html file="hub-spoke.png" alt="Topología Hub & Spoke" caption="Figura 1" max-width="500" %}

## Ventajas y desventajas
Tal y como mencionamos en la introducción, este tipo de modelo permite que la comunicación entre redes precise de un nivel de rutas menor. Para las redes Hub & Spoke, conectar {% include equation.html expression="n" %} nodos supone la necesidad de utilizar {% include equation.html expression="n-1" %} conexiones para poder conectar todos los nodos entre sí. Esto se traduce en una complejidad de {% include equation.html expression="O(n)" %}. La topología de Punto a Punto, requiere {% include equation.html expression="\frac{n(n-1)}{2}" %} lo cual es considerablemente mayor que las redes Hub & Spoke.

Otra de las ventajas que proporciona este tipo de redes es la facilidad que supone añadir un punto/nodo/extremo más a la topología ya que toda la carga de la red la lleva el nodo central (el Hub).

Una vez descritas las ventajas, pasamos a las desventajas que trae consigo escoger una red con la topología Hub & Spoke.

Tener menos rutas y conexiones que otras topologías puede suponer ventajas en varios aspectos (al configurar las redes, menos gasto material...) pero también supone desventajas de gran importancia. Al tener menos rutas, la distancia que debe recorrer un paquete para alcanzar su destino será con total seguridad mayor que la distancia que le supondría al paquete llegar al mismo destino en una topología de punto a punto. Esto hace que la eficiencia de la red sea menor.

Otra desventaja sería la dependencia que tiene el sistema en el nodo central. En caso de que el nodo central no se encontrase operativo, la red entera se encontraría no funcional ya que el tráfico de esta depende del nodo no operativo. Aún estando el nodo operativo, si por alguna razón no estuviese funcionando correctamente la red también se vería afectada. Otro caso donde el problema la dependencia con el nodo central se haría evidente, sería en una situación donde uno de los nodos extremos estuviese ocupando gran parte del ancho de banda de la red, provocando que los demás nodos tengan que esperar.