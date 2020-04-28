---
title: "GRE"
keywords: sample homepage
tags: [gre]
sidebar: mydoc_sidebar
permalink: gre.html
summary: Características de GRE y como configurarlo
---

## Características
GRE (definida como estándar IETF) es un protocolo de tunneling desarrollado por CISCO que puede encapsular diferentes protocolos (de capa 3 como IPv4, IPv6, AppleTalk, DECnet o IPX) en conexiones de punto a punto e IP de forma virtual. El protocolo está diseñado para administrar el transporte del tráfico multiprotocolo y de multidifusión IP desde múltiples localizaciones.

Un paquete GRE se divide en tres secciones: el header de envío, el header GRE y el paquete que se transporta. Dentro del header GRE encontramos la siguiente estructura (*Figura 1*):

{% include image.html file="gre-header.png" alt="Header GRE" caption="Figura 1" max-width="450" %}

- **C**: C es el bit que se utiliza para constatar que hay un checksum en el paquete. El checksum se utiliza para validar el paquete.
- **K**: K es el bit que se utiliza para constatar que hay una clave en el paquete. La clave se utiliza para autentificar el paquete.
- **Recursion**: Representa el número de veces que el paquete ha sido encapsulado con GRE.
- **Flags**: Se trata de un espacio reservado cuyo valor debe ser 0.
- **Tipo de Protocolo**: Representa el protocolo del paquete encapsulado.

La estructura del paquete crea (como mínimo) 24 bytes adicionales que no estarían en el paquete encapsulado.

## Configuración

{% include note.html content="Los comandos que se motrarán son para sistemas CISCO." %}

Para poder habilitar el uso del protocolo GRE hay que hacer lo siguiente:

```python
interface Tunnel X # Creamos una interfaz de túnel. X siendo el número de interfaz.
tunnel mode gre ip # Especificamos que vamos a utilizar GRE
ip address IP MASCARA # Le asignamos una IP y MASCARA al túnel
tunnel source IP_ORIGEN # Asignamos una IP de origen al túnel
tunnel destination IP_DESTINO # Asignamos una IP de destino al túnel
```

### Verificación
Para verificar que la configuración que hemos introducido funciona de la manera esperada utilizamos los siguientes comandos:

```bash
show ip interface brief # Muestra las interfaces túnel y su estado (activas o inactivas)
show interface tunnel X # Muestra el estado de un tunel específico. X siendo el número asignado al túnel
```

En caso de no funcionar, los problemas más comúnes suelen ser por:
- Asignar IPs incorrectas a la interfaz de túnel
- Las interfaces de origen y destino no tienen configurada la IP adecuada
- Las interfaces de origen o destino no están habilitadas y activas
- El routing (ya sea estático o dinámico) no está configurado correctamente

Los tres primeros problemas se pueden consultar con los comandos mostrados anteriormente. En cuanto a routing se refiere, el comando adecuado sería el siguiente:

```bash
show ip route
```