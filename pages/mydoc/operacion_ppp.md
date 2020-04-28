---
title: "Operación PPP"
keywords: sample homepage
tags: [ppp]
sidebar: mydoc_sidebar
permalink: operacion_ppp.html
summary: Como opera el protocolo PPP
---

## Introducción

De poco sirve tener un estándar como la comunicación punto a punto si no se define un protocolo para que los dispositivos se comuniquen entre sí. Dos protocolos utilizados extensivamente son: **HDLC** y **PPP**.

Las diferencias entre los dos protocolos son las siguientes:

|     | PPP | HDLC |
|-----|-----|------|
| **Tipo de Datos** | Síncrono y asíncrono | Síncrono |
| **Autentificación** | Sí | No
| **Orientada a** | Bytes | Bits
| **Enrutamiento dinámico** | Sí | No
| **Implementada en configuraciones** | Punto a punto | Punto a punto y multipunto

Además de las características descritas en la tabla, el protocolo PPP ofrece algunas características como el cifrado de transmisiones y la compresión de estas.

{% include callout.html content="Especificar que las implementaciones HDLC por vendedores como CISCO son propietarias. Solo los dispositivos CISCO lo soportan. PPP está diseñado para funcionar y ser compatible con el mayor número de dispositivos." type="primary" %}

Para establecer conexión con los diversos dispositivos que existen en el mercado actual, PPP soporta conexiones directas por cables seriales, líneas telefónicas, líneas troncales, teléfonos celulares, enlaces de radio especializados o enlaces de fibra óptica. También soporta conexiones por Ethernet, aunque esto ya lo veremos más adelante.

## Arquitectura

### 1. Descripción

La arquitectura de PPP viene a ser una variante de la HDLC, en la que se comparte la misma capa física que OSI pero algunas funciones, LCP y NCP en concreto, se distribuyen de manera diferente. Si cogemos la tabla de OSI que realizamos anteriormente y la actualizamos con la comparación con PPP, quedaría de la siguiente manera:

| Capas | OSI | PPP
|-------|--------
| 5, 6, 7 | Aplicación |  Capas exteriores
| 4 | Transporte | TCP/ UDP
| 3 | Internet | IP
| 1, 2 | Red | PPP y enlaces físicos

El protocolo punto a punto se divide tres componentes principales:
- Entramado del estilo de HDLC para transportar paquetes multiprotocolo a través de enlaces punto a punto.
- Protocolo de control de enlace (LCP) extensible para establecer, configurar y probar la conexión de enlace de datos.
- Familia de protocolos de control de red (NCP) para establecer y configurar distintos protocolos de capa de red. PPP permite el uso simultáneo de varios protocolos de capa de red. Los NCP más comunes son el protocolo de control IPv4 y el protocolo de control IPv6.

<br>

Los campos que contiene una trama del protocolo PPP son los siguientes:

| Señalizador | Dirección | Control | Protocolo | FCS
|-------|--------|-------|--------|-------|--------
| 1 byte | 1 byte | 2 bytes | variable | 2 ó 4 bytes

- **Indicador**: Indica el inicio y el final de una trama.
- **Dirección**: Contiene la dirección broadcast PPP estándar.
- **Control**: Su valor es constante: 0000 0011
- **Protocolo**: Sirve para identificar el protocolo utilizado.
- **Datos**: Contienen el diagrama para el protocolo especificado.
- **FCS**: Una secuencia que se utiliza para verificar la integridad de la trama. Una implementación de 4 bytes mejorará la posibilidad de detectar algún error.

<br>

El establecimiento de una sesión PPP cuenta con tres fases (la segunda fase se puede omitir):
- Fase donde se establece el enlace y se negocia la configuración
- Fase donde se determina la calidad del enlace
- Fase de negociación de la configuración del protocolo de la capa de red

{% include callout.html content="Como veremos más adelante, la función LCP se encarga de llevar a cabo las tres fases." type="primary" %}

### 2. LCP y NCP

En el punto anterior mencionamos que las funciones LCP y NCP diferian con respecto al modelo OSI. ¿Cuál es la finalidad de las funciones LCP y NCP?

#### 2.1 LCP

LCP, Link Control Protocol, reside dentro de la capa de enlace de datos (se puede ver en la tabla anterior) y funciona tanto en el establecimiento, configuración, mantenimiento y prueba de la conexión de enlace de datos.

Otras función que desempeña LCP es la negociación y configuración de las opciones disponibles del control de enlace de datos, las cuáles son administradas por la función NCP (más adelante).

Entre las opciones disponibles de configuración, se encuentran:
- Cómo y cuando termina el enlace
- Cuando el enlace funciona correctamente
- Definir el tamaño de los paquetes utilizados
- Detección de configuración errónea

#### 2.2 NCP

La función NCP se encarga de indicar el protocolo que PPP encapsula. Además, negocia las posibles configuraciones que los protocolos puedan tener.

LCP y NCP van turnandose al tomar control del enlace. Una vez que NCP haya indicado y negociado la configuración del protocolo se pasa el control al LCP (lo mismo sucede al revés, una vez que LCP haya establecido la conexión el control se pasa al NCP).