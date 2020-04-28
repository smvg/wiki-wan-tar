---
title: "Implementación PPP"
keywords: sample homepage
tags: [ppp]
sidebar: mydoc_sidebar
permalink: implementacion_ppp.html
summary: Configuración de PPP en dispositivos CISCO
---

## Configuración

Entre las numerosas opciones que contamos para configurar el protocolo PPP, existen:

- **Opciones de devolución de llamada PPP**: Esta opción nos permite mejorar la seguridad de la conexión. Uno de los dos dispositivos actuará como cliente y el otro como servidor. El intercambio de información se llevará a cabo utilizando la misma configuración bajo ciertas restricciones.

- **Opciones de autenticación**: Otra opción que podemos configurar, es el tipo de autentificación que tendrá el protocolo. Se distinguen dos tipos: PAP (Password Authentication Protocol) y CHAP (Challenge Handshake Authentication Protocol).
    - **PAP**: El momento en el que se establece el enlace inicial el router comprueba que tanto el usuario como contraseña enviados coinciden con la configuración.
    - **CHAP**: Este protocolo, comprueba periódicamente (a partir del momento que se establece el enlace inicial) la identidad del dispositivo conectado mediante un protocolo de enlace de tres vías. El nombre del host y contraseña de los routers deben coincidir.

- **Opciones de Compresión**: Nos ofrece comprimir los datos transmitidos entre dispositivos. Podemos elegir entre varios tipos de compresión dependiendo del dispositivo que tengamos. Los más comunes son: Stacker, MPPC y Predictor. Una tabla comparativa la podemos encontrar a continuación:

<br>

| Característica | Stacker | MPPC | Predictor |
|-----|-----|------|------|
| **Usa el algoritmo LZ** | Sí | Sí | No
| **Usa el algoritmo Predictor** | No | No | Sí
| **Lo soporta HDLC** | Sí | No | No
| **Lo soporta PPP** | Sí | Sí | Sí
| **Lo soporta FR** | Sí | No | No
| **Soporte para ATM y ATM-to-FR** | Sí | Sí | Sí

<br>

- **Opciones multienlace**: Esta opción nos habilita la posibilidad de propagar el tráfico a través de varios enlaces WAN físicos.

- **Opciones de detección de errores**: En esta opción podemos configurar propiedades como la calidad para identificar los fallos que pueda tener la conexión.

A continuación, en el próximo punto, mostraremos los comandos utilizados para cambiar las opciones listadas anteriormente.

### Comandos

{% include note.html content="Los comandos que se motrarán son para sistemas CISCO." %}

Para inicializar la configuración de nuestro dispositivo CISCO con el protocolo PPP, utilizamos el siguiente comando:

```
encapsulation ppp
```

#### Compresión

{% include callout.html content="No utilizar este comando si en la conexión ya de por sí transporta archivos comprimidos." type="primary" %}

Podemos comprimir el tráfico con el siguiente comando.

``` bash
compress predictor # Si queremos utilizar el algoritmo "predictor"
compress stac # Si queremos utilizar el algoritmo "stacker"
```

#### Calidad de enlace

La calidad que debe tener la conexión se especifica de la siguiente manera.

{% include callout.html content="La calidad se calcula tanto para direcciones entrantes como salientes. **En caso de no alcanzar la calidad deseada, el enlace se desactiva.**" type="primary" %}


``` bash
quality x # x siendo un número entre 1 y 100
```

#### Multienlace

Para poder propagar el tráfico a través de varios enlaces WAN, hace falta configurar correctamente MPPP. A continuación, mostramos como hacerlo:

``` bash
# PASO 1
interface Multilink X # x siendo un número cualquiera
ip address IP MÁSCARA # IP siendo la dirección IPv4 que le vamos a dar la interfaz multienlace
ipv6 address IP MÁSCARA # IP siendo la dirección IPv6 que le vamos a dar la interfaz multienlace
ppp multilink
ppp multilink group X # X siendo un número cualquiera que le asignamos a un grupo multienlace

# PASO 2
interface INTERFAZ # INTERFAZ siendo la interfaz que le vamos a asignar el grupo que acabamos de crear
no ip address
encapsulation ppp
ppp multilink
ppp multilink group X # X siendo el número que le hemos asignado el grupo multienlace en el paso 1
```

{% include callout.html content="En caso de querer añadir el grupo a más de una interfaz, repetimos el paso 2 tantas veces como sea necesario." type="primary" %}

#### Autentificación

Para mejorar la seguridad de nuestra conexión, contamos con las siguientes opciones:

``` bash
ppp authentication chap # Aplica la autentificación CHAP
ppp authentication chap pap # Aplica la autentificación CHAP primero y después la PAP
ppp authentication pap chap # Aplica la autentificación PAP primero y después la CHAP
ppp authentication pap # Aplica la autentificación PAP
ppp pap sent-username NOMBRE password CONSTRASEÑA # Necesario al utilizar PAP
```

#### Comprobación

Una vez configurado nuestro dispositivo, comprobamos que la configuración que hemos introducido es la correcta y adecuada, esto se puede realizar con los siguientes comandos:

``` bash
show interfaces serial INTERFAZ # INTERFAZ siendo la interfaz que queremos consultar
show ppp multilink # Con este comando verificamos que PPP está habilitado en el dispositivo adecuado
```