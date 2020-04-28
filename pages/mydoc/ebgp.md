---
title: "eBGP"
keywords: sample homepage
tags: [bgp]
sidebar: mydoc_sidebar
permalink: ebgp.html
summary: Características de BGP, eBGP y como configurarlo
---

## Características
Existen varios protocolos que nos permiten enrutar tráfico en redes internas (protocolos IGP). Estos se encargan de intercambiar información entre los diferentes dispositivos y sistemas autónomos de la red para que todos los dispositivos tengan un conocimiento de los "hosts" que existen en la red. Sin embargo, este tipo de tecnología es necesaria también para redes externas y protocolos como RIP y IS-IS no son suficientes. Es utilizado por los sistemas autónomos para publicar las redes que se originaron internamente o redes que se generaron en otros sistemas autónomos.

Es por esto que existe otro tipo de protocolos, especificamente los EGP, diseñados para la sincronización de información (de routing) en redes externas. BGP (border gateway protocol) es uno de los protocolos EGP más utilizados y que comentaremos en este punto junto con su extensión eBGP. 

Para su funcionamiento, BGP utiliza:
- Un identificador **único** (de 16 o 32 bits) utilizado para identificar sistemas autónomos.
- Métricas que le ayudan a determinar cuáles son las mejores rutas. Entre los parámetros que tiene en cuenta están los "hops" necesarios para establecer la conexión, la distancia, el código de origen, la ID del router y de los router vecinos (hay más parámetros, estos solo son algunos de ellos).

BGP ha visto mejoras incrementales durante los años, desde su "nacimiento" en 1994 se han visto 4 versiones diferentes del protocolo.

La comunicación entre los diferentes dispositivos activos en la red se realiza por el puerto 179. Los dispositivos mantienen La conexión siempre activa enviando cada 60 segundos mensajes de "keep-alive".

Un sistema autónomo que utiliza el protocolo BGP puede encontrarse en **seis estados**:
- Estado Desocupado/Inicialización: El protocolo incializa los recursos que necesita. Durante este estado, el dispositivo rechaza cualquier tipo de conexión BGP.
- Estado de Conexión: Espera a que la conexión TCP haya completado. Si se conecta se pasa al estado "OpenSent", en caso de "timeout" pasa al estado "Activo".
- Estado Activo: El dispositivo resetea el contador utilizado para el "timeout" y vuelve al estado de Conexión.
- Estado "OpenSent": El dispositivo envía un mensaje a los demás dispositivos. Si recibe respuesta pasa al estado de "OpenConfirm".
- Estado "OpenConfirm": Espera la llegada de cualquier mensaje "keep-alive" de otros dispositivos, si lo recibe pasa al estado final
- Estado de Conexión establecida: El funcionamiento del dispositivo es el esperado e intercambia información con otros dispositivos.

Existen dos extensiones del protocolo BGP:
- **eBGP**: El BGP externo es el protocolo de routing utilizado entre los routers de sistemas autónomos diferentes.
- **iBGP**: El BGP interno es el protocolo de routing utilizado entre los routers del mismo AS.

¿Cuándo es ideal utilizar BGP? BGP es apropiado utilizarlo cuando un sistema autónomo debe comunicarse con una gran cantidad de sistemas autónomos diferentes. En caso de contar con una sola conexión con un sistema autónomo no se debería utilizar BGP.

## Configuración

{% include note.html content="Los comandos que se motrarán son para sistemas CISCO." %}

{% include callout.html content="Antes de configurar un sistema autónomo con el protocolo BGP, es necesario que el administrador conozca y entienda bien el protocolo." type="primary" %}

Existen tres formas diferentes de configurar el protocolo BGP:
- **Por ruta predeterminada**: Este es el método más simple para implementar el BGP. Sin embargo, debido a que el usuario solo recibe una sola ruta se puede producir el routing por debajo del nivel óptimo.
- **Por ruta predeterminada y rutas del proveedor de internet**: A pesar de tener más rutas disponibles es posible que no sea consiguen siempre las mejores rutas.
- **Por todas las rutas de Internet**: Las rutas serán siempre las óptimas, sin embargo los routers deben ser capaces de contener en memoria la increible cantidad de redes existentes.

### 1. Comandos

Para configurar nuestro router CISCO con BGP, introducimos los siguientes comandos:

```bash
router bgp X # Habilita BGP con X siendo el número de proceso BGP
neighbor IP remote-as X # Especifica un vecino. IP siendo la IP del vecino y X el número de proceso BGP
network IP MASCARA # Publica una red al vecino que hemos especificado anteriormente. La IP y la MASCARA deben de ser de la red a publicar
```

### 2. Verificación

Para verificar que hemos configurado correctamente nuestro router CISCO utilizamos los siguientes comandos:
```bash
show ip route # Aquí podemos verificar que las rutas publicadas por los demás dispositivos se están reconociendo correctamente
show ip bgp # Aquí podemos consultar que las redes recibidas y publicadas están presentes en la tabla BGP
show ip bgp summary # Aquí verificamos otra información del protocolo, como la IP, el número de proceso, etc.
```