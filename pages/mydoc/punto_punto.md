---
title: "Descripción general de Punto a Punto"
keywords: sample homepage
tags: ["punto a punto"]
sidebar: mydoc_sidebar
permalink: punto_punto.html
summary: Descripción general de las conexiones punto a punto
---

## Introducción

La conexión punto a punto es el tipo de conexión WAN más utilizado. Como explicamos también en uno de los puntos anteriores, la conexión punto a punto (también conocida como conexión serial o conexión de línea arrendada) es una de las conexiones más simple ya que se conecta solo una ruta entre dos dispositivos ya que no existe redundancia ni se utiliza topologías complejas como la estrella o mesh.

Existen dos tipos de puertos compatibles con la conexión punto a punto:
- Comunicación Serie: Se utiliza un solo canal donde la información se transmite secuencialmente. Para este tipo de conexiones se utilizan puertos bidireccionales. Estos son capaces de enviar información a la vez que reciben (aunque la limitación de un solo canal por dirección sigue existiendo).
- Comunicación Paralela: A diferencia de las conexiones serie, es capaz de aceptar tráfico simultáneo por diversos cables. La mayor velocidad de transferencia trae consigo varios inconvenientes: el llamado "crosstalk" (interferencias entre los distintos cables) y las desincronizaciones entre envíos. La mayoría de comunicaciones paralelas solo llegan a ser unidireccionales (unas pocas admiten la comunicación bidireccional pero solo una dirección a la vez). Dado que la circuitería de los cables que se utilizan en este tipo de comunicaciones, la comunicacińo serial es considerablemente más económica.

## Ventajas y desventajas

Las conexiones punto a punto, comparada con otros tipos de conexiones (Hub & Spoke y Mesh) ofrece el equilibrio entre coste y rendimiento. Si es verdad que en caso de conectar redes a gran distancia el coste seguiría siendo elevado comparado con servicios compartidos.

Hoy en día, una desventaja que se está haciendo evidente, es la poca utilidad (o por lo menos rendimiento inferior) que tiene para IoT. Este tipo de comunicación se sigue utilizando para sistemas SCADA y de tráfico pero conforme pasa el tiempo estos sistemas se están migrando a tipos comunicaciones más versátiles.