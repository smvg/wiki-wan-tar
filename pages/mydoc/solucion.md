---
title: "Solución de Problemas"
keywords: sample homepage
tags: [general]
sidebar: mydoc_sidebar
permalink: solucion.html
summary: Solución de problemas de conectividad WAN
---

## Resolución de Problemas

{% include note.html content="Los comandos que se motrarán son para sistemas CISCO." %}

Para resolver problemas de conectividad WAN (y LAN, etc.) se utiliza en comando "debug" acompañado del parámetro que queremos depurar. 

{% include callout.html content="Para poder ejecutar estos comandos es necesario contar con los privilegios suficientes." type="primary" %}

```bash
debug ppp packet # Muestra los paquetes recibidos y enviados
debug ppp negotiation # Muestra los paquetes enviados al establecer la conexión
debug ppp error # Muestra errores de protocolo y estadísticas de error
debug ppp authentication # Muestra mensajes que tengan que ver con los protocolos CHAP y PAP
debug ppp compression # Muestra información sobre el intercambio de paquetes comprimidos
debug ppp cbcp # Muestra errores del protocolo y estadísticas relacionadas con las negociaciones de conexión PPP
```