---
title: "VPN"
keywords: sample homepage
tags: [vpn]
sidebar: mydoc_sidebar
permalink: vpn.html
summary: Descripción general de las VPN
---

## VPN

Las VPN (Virtual Private Network), permiten que dispositivos se conecten a una red ajena y los dispositivos que se encuentran en esa red le traten como un dispositivo local. Dicho de otra manera, las VPN son una red privada creada mediante tunneling a través de una red pública.

Es utilizada por organizaciones y empresas que desean proporcionar a sus empleados acceso de manera segura a servicios exclusivos de la empresa desde localizaciones remotas.

Las conexiones que se realizan a este tipo de redes se hacen mediante conexiones cifradas autentificadas utilizando criptografía asimétrica (criptográfica de clave pública) y el protocolo SSL/TLS. Este tipo de autentificación hace uso de las capas 2 y 3 del modelo OSI.

Otros usos que se le está dando a las VPN proviene de usuarios que quieren acceder a contenidos que están restringidos en su país y usuarios que buscan privacidad en la red.

Las VPN se pueden configurar en varios dispositivos, ya sea servidores dedicados o en el propio router.

### 1. Tipos de VPN

A continuación describiremos brevemente los dos tipos de VPN más utilizados (de acceso remoto y de sitio a sitio) y haremos una mención especial de las DMVPN.

#### 1.1 VPN de Acceso Remoto

Este tipo de VPN conecta las redes enteras por lo que cualquier usuario que se conecte tendrá acceso completo a la red externa. Para este tipo de conexiones es necesario software tanto para el host como para el cliente. Las VPN de Acceso Remoto son las que ofrecen los proveedores de este tipo de servicios.

#### 1.2 VPN de sitio a sitio

Los dispositivos que se conectan por medio de las VPN de sitio a sitio no tratan la conexión como una VPN de Acceso Remoto, lo tratan como una conexión normal. Para que este tipo de conexión funcione es necesario tener a dos terminales (uno en una red externa y otro en la red interna) configurados correctamente para que se conecten mediante un gateway VPN.

Se distinguen dos tipos de conexiones VPN de sitio a sitio:
- Conexiones Intranet: Este tipo de conexión conecta cada LAN interna de cada usuario y la fusiona en una sola red.
- Conexiones Extranet: Permite que usuarios externos se conecten a redes locales.

#### 1.3 DMVPN

DMVPN (Dynamic Multipoint Virtual Private Network), es una solución para crear VPN múltiples. Entre sus ventajas se encuentran la escabilidad que ofrece el sistema. Tiene como objetivo simplificar la configuración y minimizar la complejidad del "setup".

Las DMVPN se apoyan de los siguientes protocolos:
- **NHRP**: es un protocolo de resolución y de almacenamiento en caché de capa 2 similar al protocolo de resolución de direcciones (ARP). Su función es almacenar las direcciones IP públicas para todos los radios del túnel VPN.
- **GRE**: es un protocolo que permite encapsular una amplia variedad de tipos de paquetes de protocolo dentro de túneles IP. Al utilizar GRE se reduce el tamaño y la complejidad de la configuración.
- **IPsec**: se utiliza para proporcionar el transporte seguro de información privada en redes públicas.

### 2. Beneficios

Dado que las razones para utilizar una VPN pueden ser diferentes, los beneficios que se obtendrán también.

Para los **usuarios no profesionales**, las ventajas que supone utilizar una VPN es la mejora tanto en **seguridad** como **privacidad**.

Por otro lado, para los **usuarios profesionales**, las ventajas incluyen: **Ahorro de costos** (las empresas no tienen que crear enlaces dedicados entre redes ya que pueden conectar el tráfico de diferentes redes con el uso de VPNs), **Escalabilidad** (las empresas pueden añadir usuarios fácilmente), **Compatibilidad** (el medio que utilizan las VPN para sus conexiones es el mismo que se utilza extensivamente para otras tareas por lo que si un usuario tiene acceso a internet, tiene acceso a la red virtual) y **Seguridad** (todas las conexiones a la red están cifradas y autentificadas).