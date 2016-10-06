---
layout: index
title: Instalación de MPD
---

# Instalación y configuración de mpd

## Por qué usar MPD.

MPD es un reproductor de música que usa la estructura servidor/cliente, de forma que una vez instalado, el cliente que se use para la reproducción musical puede ser cualquiera de los muchos existentes. En este caso en particular explicaré como usar dos de ellos, uno será *_ncmpcpp_* y el otro será un cliente android llamado *_MPDroid_*, este último se puede encontrar tanto en *GooglePLayt* como en *F-Droid*.

Voy a destacar un par de ventajes que tiene el usar mpd.

- Es muy ligero, consume pocos recursos.
- Si podemos acceder a nuestro equipo desde fuera de casa es muy sencillo controlar mpd de forma remota, además de que el consumo de ancho de banda en ese control es muy pequeño.
- MPD tiene de forma nativa un servidor http con lo que se puede crear un servidor streaming de musica para nuestra LAN o incluso con salida a internet.
- Puede usar *ALSA* o *PulseAudio*. En caso de usar _pulseaudio_ podemos transmitir música directamente desde nuestro demonio mpd hacia cualquier tarjeta de sonido de nuestra LAN (aunque no lo he probado es compatible con dispositivos apple).
- Emisión directa hacia servidores ShoutCast y IceCast.
- Decodificación a través de ffmpeg.
- Multitud de clientes tanto CLI, GTK, QT y Android.
- Soporte de jerarquía de acceso a través de nombres de usuario y contraseñas.
- Soporte de expresiones regulares para hacer búsquedas en nuestra biblioteca de música.
- Posibilidad de iniciarlo como _systemwide_ o usuario al iniciar sesión.
- Letras de canciones.

## Instalación de MPD

Depende del sistema operativo se hará de una forma o de otra pero no debería suponer un gran problema.

- Debian/Ubuntu y derivados:
~~~
# apt-get update && apt-get install mpd
~~~

- Archlinux
~~~
# pacman -Syy && pacman -S mpd
~~~


