---
title: "PPPoE"
keywords: sample homepage
tags: [ppp, pppoe]
sidebar: mydoc_sidebar
permalink: pppoe.html
summary: Descripción general de la extensión de PPP por Ethernet
---

## Descripción
En el punto anterior hemos hablado sobre las conexiones que normalmente utilizan los clientes de los proveedores para acceder a internet. ¿Pero qué conexiones utilizan las ISP?

Como ya explicamos uno de los protocolos de capa de enlace que se utiliza es PPP. Las ISP utilizan este protocolo ya que les permite asignar direcciones IP a extremos remotos de un enlace además de autentificar las conexiones. PPP permite utilizar enlaces de diferentes tipos entre los que se encuentra el protocolo *PPPoE*, el cuál permite el envío de tramas PPP encapsuladas dentro de tramas de Ethernet.

PPPoE permite que las operadoras permanezcan utilizando el protocolo PPP sin quitarle al usuario la comodidad que supone utilizar interfaces conocidas y compatibles como lo es la interfaz Ethernet.

## Configuración

{% include note.html content="Los comandos que se motrarán son para sistemas CISCO." %}

Para configurar una comunicación utilizando el protocolo PPP entre dos dispositivos es necesario seguir los pasos a continuación.

```python
interface dialer X # X siendo el número de la interfaz del marcador. Esto no es la interfaz física.
encapsulation ppp
ip address negotiated

# Estas credenciales deben coincidir con las credenciales que residen en el router del cliente
ppp chap hostname NOMBRE
ppp chap password PASSWORD

ip mtu 1492 # Utilizamos 1492 ya que el valor predeterminado (1500) no funcionará con PPPoE
dialer pool X # X siendo un número que le asignaremos al pool. Este número lo utilizaremos después.
no shutdown

interface INTERFAZ # INTERFAZ siendo la interfaz que está conectada al módem
no ip address
pppoe enable
pppoe-client dial-pool-number X # X siendo el número que previamente le asignamos al pool.
no shutdown
```

{% include callout.html content="El MTU máximo pasa a ser  de 1492 ya que PPPoE necesita unos 8 bytes adicionales para su encabezado." type="primary" %}


### 1. Verificación de PPPoE
Para verificar que la configuración que hemos aplicado y guardado es la correcta utilizamos los siguientes comandos:

```bash
show ip interface brief # Nos sirve para verificar que la interfaz del marcador está activa
show interface dialer # Con esto verificamos que el MTU es de 1492 y la encapsulación es PPP
show ip route # Con este comando comprobamos la tabla de routing
show pppoe session # Muestra las sesiones PPPoE actualmente activas
```
A pesar de haber configurado correctamente los dispositivos, pueden seguir surgiendo razones por las que nuestra conexión PPPoE no funciona correctamente.

#### 1.1 Fallo en la negociación del PPPoE
Este fallo se puede dar si:
- Falla del protocolo de control de IP
- No hay respuesta del dispositivo remoto
- El LCP no se ha abierto
- Error al autentificar las credenciales


<br>
Para depurar este tipo de errores se utiliza:
```bash
debug ppp negotiation # Aquí se mostrará la información de los 4 puntos mencionados anteriormente
```

#### 1.2 Fallo de autentificación
Si se cree que el error que se produce es de autentificación, se puede consultar la verificación de las credenciales con el comando:

```bash
debug ppp negotiation # En caso de no coincidir mostrará "FAILURE" en la salida del comando
```

#### 1.3 Sesiones TCP descartadas
En el caso de que la configuración muestre incosistencias al manejar sesiones TCP, esto se puede ser por no configurar el tamaño máximo de segmento. Esto se puede configurar de la siguiente manera:

```bash
ip tcp adjust-mss 1452 # 1452 es el valor recomendado
```