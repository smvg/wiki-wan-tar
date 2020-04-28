---
title: "Descripción general de Mesh"
keywords: sample homepage
tags: [mesh]
sidebar: mydoc_sidebar
permalink: mesh.html
summary: Descripción general de la topología Mesh
---

## Descripción general

La topología Mesh es una topología en la que todos los nodos cooperan para distribuir los datos entre cada uno de ellos. Hoy en día se utiliza extensivamente en IoT (esto se debe a la escabilidad de la red y los requisitos de interconectividad entre todos los dispositivos).

Los dispositivos que residen en sistemas que utilizan las redes con la topología Mesh no funcionan en torno a un nodo central como otras topologías por lo que tiene un alto grado de fiabilidad y tolerancia a fallos. Aunque varios nodos salgan de la red de forma precipitada e inmediata, los nodos activos encontraran inmediatamente otra ruta para en enviar sus paquetes.

Un diagrama de la topología utilizada en las redes Mesh (o malla) la podemos ver en la *Figura 1*.

{% include image.html file="mesh.png" alt="Red MESH" caption="Figura 1" max-width="450" %}

## Ventajas y desventajas

Entre sus ventajas, al contar con una gran cantidad de rutas, es posible mover grandes cantidades de datos sin provocar que la red se ralentice demasiado. Al estar todos los dispositivos conectados entre sí, añadir nuevos dispositivos a la red es relativamente sencillo ya que la configuración se sincroniza entre los dispositivos (también depende de la configuración). Como mencionamos al principio, no depender de un nodo central supone una mejor fiabilidad y tolerancia a fallos.

Uno de los problemas que surgen al conectar redes Mesh, es la forma en la que se conectan. En caso de utilizar cable, el coste de las instalaciones es sustancial; si se opta por utilizar conexiones inalámbricas, el coste es moderado pero el rango de la red se limita considerablemente. Es por esto que las empresas que diseñan este tipo de redes a gran escala optan por su implementación por software (SD-WAN).