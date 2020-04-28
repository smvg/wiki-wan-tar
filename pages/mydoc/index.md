---
title: "Tecnologías WAN"
keywords: sample homepage
tags: [ general, "punto a punto", "hub & spoke", mesh ]
sidebar: mydoc_sidebar
permalink: index.html
summary: Descripción general de las WAN
---

## WAN

A día de hoy el volumen de datos y el tráfico que se genera a partir de este requiere que se implementen infraestructuras de diversos tamaños y características para garantizar que el usuario final no se enfrente a problemas de seguridad y rendimiento.

Las infraestructuras de red pueden variar en los siguientes aspectos:
- El tamaño que ocupa la infraestructura
- El número de usuarios conectados
- El número y tipo de servicios disponibles

Es por esto que existen varios tipos de redes para cubrir diferentes escenarios. En esta "Wiki" cubriremos un tipo de red conocido como WAN ("red de área amplia" si traducimos directamente del inglés), la cuál se utiliza para cubrir grandes áreas (como su nombre indica) y proporciona acceso a otras redes. Este tipo de redes normalmente están controladas por los proveedores de servicios de telecomunicación.

### 1. ¿Qué tiene de diferente con respecto LAN y MAN?

Antes de proceder a explicar más a fondo las redes WAN, es necesario compararlo con algunas de las redes existentes.

Una de las más conocidas y a la que todos tenemos acceso es la **LAN** (redes de área local). Se trata de la topología más pequeña y fácil de manejar, por eso es instalada y utilizada tanto a nivel doméstico como a nivel de pequeñas empresas y negocios. A continuación, en la *Figura 1* mostramos la red en cuestión.

{% include image.html file="lan.png" alt="LAN" max-width="300" caption="Figura 1" %}

{% include callout.html content="A diferencia de la WAN, en la LAN no es necesario subscribirse a un proveedor de servicios para obtener conexión y poder utilizar la red." type="primary" %}

Como red intermedia que se sitúa entre la LAN y la WAN tenemos la **MAN**. Las redes MAN están destinadas a grandes organizaciones/empresas cuyas necesidades son mayores de las que puede ofrecer una LAN. Uno de los requisitos que se imponen para que una red se considere una MAN en vez de una WAN es que la red conecte ordenadores a distancia (en diferentes calles, edificios...) que estén en la misma ciudad, una vez que se conecten desde otra localización no se consideraría una MAN.

Además de las redes mencionadas anteriormente, existen otras como:
- RAN (Radio Access network)
- CAN (Controller Area network)
- PAN (Personal Area Network)
- BAN (Body Area Network)

A continuación, en la *Figura 2* podemos ver la clasificación de las redes por su tamaño.

{% include image.html file="network-clasification.png" alt="Clasificación de Redes" caption="Figura 2" max-width="400" %}

### 2. Implementaciones

Una vez que hemos diferenciado las redes de área amplia de otras redes de menor tamaño, describimos las diferentes implementaciones, topologías que pueden utilizarse al implementar una WAN.

{% include note.html content="Haremos más incapie en las topologías de Punto a Punto, Hub & Spoke y Mesh en los próximos puntos. La topología de seguridad preventiva doble, al tratarse de la topología punto a punto con redundancia no la tocaremos." %}

Las topologías más utilizadas y comunes son las siguientes:
- Punto a punto: Es la topología más simple de todas. Conecta directamente dos redes.
- Hub and Spoke: Una implementación de la topología de estrella para WAN. Un punto central interconecta con puntos extremos utilizando conexiones punto a punto.
- Mesh: Este tipo de implementación proporciona un mejor rendimiento comparado con la mayoría de implementaciones pero requiere que todos los puntos estén interconectados entre sí. Esto supone un alto coste tanto administrativo como material.
- Implementación de seguridad preventiva doble: Se trata de una implementación de la topología de punto a punto con redundancia en cada una de las conexiones. Esta topología es todavía más costosa que la topología Mesh.

Implementaciones como la Hub & Spoke y Mesh hoy en día se realizan por software (aunque siempre existe alguna excepción). Este tipo de implementaciones por software se conocen como Software Defined WAN o **SD-WAN**. En el próximo punto profundizaremos un poco más.

Antes de continuar con el siguiente punto, una tabla comparando y resumiendo las diferentes topologías vistas hasta ahora. En la tabla compararemos el coste tanto administrativo como económico de la topología, la rapidez (se puede traducir también a la menor distancia entre dos puntos) y la fiabilidad (en caso de que una ruta falle, ¿sigue la red operacional?).

| Topología | Coste | Rapidez | Fiabilidad
|-------|--------|---------|---------|
| Punto a Punto | Moderado | Normal | Normal
| Hub & Spoke | Bajo | Baja | Baja
| Mesh | Alto | Muy alta | Muy alta
| SPD | Muy alto | Normal | Muy alta

### 3. SD-WAN
**Software Defined WAN**, también conocido como **SD-WAN**, consiste en implementar topologías WAN por medio de software (como su nombre indica). Utilizar implementaciones como esta supone una mejora en la administración de la red (en caso de querer cambiar de topología, no habría necesidad de adquirir nuevo hardware para poder implementarla). Las WAN tradicionales (las que funcionan por hardware) necesitan routers tradicionales para funcionar, este no es el caso para WANs de software. La operación de la SD-WAN puede llegar hasta la **capa 7 del modelo OSI**.

Tecnologías como esta permiten que empresas y organizaciones de gran tamaño puedan implementar su propia WAN con un coste reducido utilizando la infraestructura existente que ya de por sí proporciona Internet.

{% include image.html file="sd-wan-diagram.png" alt="Diagrama SD-WAN" caption="Figura 3" max-width="450" %}

En la *Figura 3* vemos un diagrama donde empresas como Amazon, Google, etc. pueden crear sus propias WAN definidas por software utilizando medios de conexión ya existentes como LTE, MPLS y "Broadband".

Las dos características principales que ofrecen las redes con arquitectura SD-WAN son:
- Dirección centralizada: Al centralizar las políticas de seguridad y rendimiento en unos pocos dispositivos (servidores, centros de procesamiento de datos, etc.), esto permite que los gastos operativos se reduzcan (esto lo hemos mencionado también en el párrafo anterior).
- ZTP (Zero-Touch Provisioning): Al estar la red definida por software, permite que la configuración se sincronice fácilmente entre todos los dispositivos de la red. No hace falta configurar cada dispositivo.

Otras de las ventajas que ofrece las WAN definidas por software es la manera que permite al usuario controlar el tráfico de datos. Las empresas/organizaciones pueden administrar y controlar el tráfico con una prioridad determinada.

A pesar de las ventajas mencionadas el problema que sigue teniendo la SD-WAN es que sigue dependiendo de infraestructuras y WAN existentes. Esto limita el rendimiento que pueda ofrecer la red.

## Operación de las WAN

Desviandonos de las WAN definidas por software, volvemos a las WAN definidas por hardware. Explicaremos a continuación, dónde se encuentra en el modelo OSI, los diferentes dispositivos utilizados y la conmutación que crea este tipo de red.

### 1. ¿Qué capas utiliza del modelo OSI?

Estas utilizan las capas 1 (capa física) y 2 (capa de enlace de datos) del modelo OSI. En la tabla vemos donde se encuentran las capas mencionadas anteriormente.

| Capa | Protocolos (no se incluyen todos)
|-------|--------
| Aplicación (7) | DNS, DHCP, FTP, HTTPS, IMAP, LDAP, POP3, SSH
| Presentación (6) | JPEF, MIDI, MPEG, PICT, TIFF
| Sesión (5) | NetBIOS, NFS, PAP, SCP, SQL
| Transporte (4) | TCP, UDP
| Red (3) | ICMP, IGMP, IPsec, IPv4, IPv6, IPX, RIP
| Enlace de datos (2) | ARP, ATM, CDP, FDDI, HDLC, MPLS, PPP
| Física (1) | Bluetooth, Ethernet, DSL, ISSDN, Wi-Fi

Es evidente por qué utiliza la capa 1, ya que es necesario conectar los dispositivos entre sí utilizando las interfaces físicas existentes, ¿pero por qué utiliza las capa 2? Esto se debe a que las WAN asignan direcciones físicas a sus dispositivos, y controlan el flujo y el encapsulamiento de los paquetes que recorren la red. En la capa 2 también se define la forma en la que los datos están encapsulados.

{% include callout.html content="Dado que una gran parte de los enlaces WAN que se utilizan tienen como topología la conexión punto a punto, la dirección de la trama (capa de enlace de datos) no se suele incluir." type="primary" %}

### 2. Hardware utilizado

Para poner en marcha una WAN se necesita una gran variedad de hardware. A pesar de no poder incluir todo el hardware utilizado, incluiremos el más "esencial".

- **Modems**: Los modems tienen como objetivo tanto convertir como traducir las señales digitales para que otros dispositivos puedan utilizar las señales (información) enviadas.
    - **"Dial-up"**: Los modems "dial-up" utilizan la red telefónica (PTSN) para conectarse al ISP. Su velocidad teórica máxima es de 56 kbit/s. Hoy en día ya no se utiliza.
    - **Banda ancha**: Este tipo de modems tiene dos variaciones, una funcionando con el serivicos DSL (también utiliza la red telefónica pero su velocidad teórica máxima se ve incrementada a los 24 Mbps) y otra utilizando cables de alta velocidad (se conocen también como ONTs).
- **Servidor de acceso**: Este servidor controla y coordina los módem que funcionan por línea telefónica. Al igual que los módems que funcionan por línea telefónica, ya no se utilizan.
- **CSU/DSU**: CSU (Channel Service Unit) y DSU (Data Service Unit) es un dispositivo (o una interfaz designada del router) que convierte los paquetes procedentes de la LAN y los traduce a un formato que la WAN pueda entender y viceversa.
- **Switches**: Los switches conecta varios dispositivos por medio de las numerosas interfaces que ofrece. Utiliza las direcciones MAC de los dispositivos para redireccionar el tráfico.
    - **WAN**: Un switch multipuerto que utilizan las ISP. Estos dispositivos conmutan el tráfico y operan en la capa de enlace de datos del modelo OSI.
    - **Multicapa**: A diferencia del switch WAN, los switch multicapa son capaces de operar a capas más externas que la capa 2 del modelo OSI. Pueden inspeccionar los paquetes de red y acceder a información como el protocolo utilizado, etc.
- **Router**: Los routers proporiconan conexión entre las LAN y WAN. Incluyen interfaces Ethernet y (dependiendo del tipo de router) seriales. Para poder conectarse con la WAN, normalmente va acompañado de un módem, ONT o DSU/CSU.
    - **Central**: Cada proveedor cuenta con varios routers centrales. Este tipo de routers debe soportar múltiples conexiones simultáneas sin ningún tipo de ralentización ya que se suelen posicionar en el núcleo de la red.
- **Router + ONT**: Para simplificar la mayoría de instalaciones los proveedores de internet instalan dispositivos que incluyen tanto el router como el módem/ONT en el mismo dispositivo.

### 3. Conmutación de la Red

En la WAN podemos diferenciar dos formas de establecer una conexión e intercambiar información. Dependiendo de lo que queramos enviar, un sistema será más eficiente que el otro.

#### 3.1. Conmutación de paquetes
La conmutación de paquetes divide los datos que el emisor envía al receptor en paquetes que se enrutan a través de una red compartida. A diferencia de la conmutación por circuitos no hace falta que se establezca un canal.

Los paquetes enviados encuentran su destinado gracias al enrutamiento que hacen los switches. Los paquetes enviados pueden varias dependiendo del sistema que se utilice. Distinguimos dos tipos de sistemas:
- Sistemas sin conexión (datagramas): Toda la información del direccionamiento se debe transportar en el paquete. Cada switch evalua la dirección para dirigir el paquete a su destino.
- Sistemas orientados a la conexión (circuitos virtuales): En este sistema, los switches consultan el identificador que se incluye en el paquete (no se incluye toda la información del direccionamiento) y lo comparan con los identificadores que ya tienen almacenados en sus tablas de enrutamiento.

Las redes de conmutación de paquetes se utilizan extensivamente en las comunicaciones de datos (salvo en una excepción que explciaremos más en el próximo subpunto).

A pesar de ser el sistema ideal para la mayoría de datos, trae consigo algunas desventajas como los retrasos y variabilidad de retraso. Esto se debe a que los switches utilizados para enrutar el tráfico tienen que procesar cada paquete generado y enrutarlo.

#### 3.2. Conmutación de circuitos
En la conmutación de circuitos se crea y establece una conexión virtual (un circuito o canal) de la fuente al destino.

La conmutación por circuitos cuenta con tres fases:
- Establecimiento
- Transferencia
- Desconexión

Su uso es ideal para transmitir y recibir voz ya que el retardo es pequeño y fijo. Sin embargo, el funcionamiento de este tipo de conmutación no es ideal para transmitir datos que no sean de voz. Esto se debe a que la conexión entre el emisor y el receptor esta diseñada para transmitir un flujo de datos continuo y fijo (en llamadas de voz el bitrate es constante). Un vídeo (comprimido), por ejemplo, normalmente cuenta con un bitrate diferente dependiendo de la cantidad de información que haya en un momento determinado.

Tener una capacidad de canal asignada significa que si por alguna razón no se enviasen datos, se estaría desaprovechando la conexión.

Los dos tipos más comunes de tecnologías WAN de conmutación de circuitos son la PSTN y ISDN.

#### 3.3. Comparación
Para resumir el punto, ofrecemos una tabla con las principales características de cada tipo de conmutación.

| Conmutación | Ancho de Banda | Retardo
|-------|--------|---------|---------|
| Paquetes | Variable | Sí
| Circuitos | Fijo | Solo en el establecimiento

## Proveedores en España

{% include note.html content="En esta comparativa no incluiré proveedores cuya área de negocio se limite a una comunidad autónoma (o unas pocas). Algunos ejemplos son: Euskaltel y R." %}

En este apartado nos centraremos en las velocidades máximas que nos ofrecen los operadores que tenemos en España (en el caso de qeu haya paquetes que ofrezcan la misma velocidad escogeremos el más barato).

### 1. Movistar
Movistar (Telefónica) cuenta con la red de fibra con más alcance de todas las operadoras. Durante los últimos años ha concentrado sus esfuerzos en sustituir la red existente de cobre por una de fibra.

A pesar de controlar una de las mayores redes de fibra del país, Movistar deja que otras operadoras utilicen la red a cambio de considerables sumas de dinero.

El mejor plan de Movistar actualmente ofrece 600 Mb simétricas por un precio de 71.4€. Este precio incluye otros servicios como Televisión, Teléfono Fijo y Líneas Móviles con acceso a la red 4G LTE.

Destacar que tanto las señales de Televisión como las del Teléfono Fijo son transmitidas por cable de fibra.

### 2. Orange y Jazztel
Orange cuenta con una de las mayores redes de Fibra (por detrás de Movistar) después de la adquisición de Jazztel. A pesar de la compra, ambas compañías ofrecen paquetes distintos.

Por un lado Orange ofrece 1 Gbps simétricos por 64.95€ al mes. Jazztel ofrece 600 Mb simétricos por 56.95€ al mes.

El paquete de Orange es uno de los paquetes que más ancho de banda ofrece de todos los ISP españoles.

### 3. Vodafone (Ono)
Otra de las redes más grandes de España es la de Vodafone, la cuál "heredó" después de la compra de Ono. Ono fue una de las primeras compañías que apostó fuerte por la fibra. Comparado con otras redes como la de Orange y Movistar, la red de Vodafone (Ono) es en gran parte HFC.

Vodafone ofrece a sus clientes una velocidad de 1 Gbps por 55.99€.

### 5. Tabla Comparativa

| Operadora | Ancho de Banda | Fijo | Móvil | Precio
|-------|--------|---------|---------|
| Movistar | 600 Mbps | Sí | Sí | 71.4€
| Orange | 1 Gbps | Sí | Sí | 64.95€
| Jazztel | 600 Mbps | Sí | Sí | 56.95€
| Vodafone | 1 Gbps | Sí | No | 55.99€