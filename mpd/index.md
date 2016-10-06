---
layout: index
title: Instalación de MPD
---

# Instalación y configuración de mpd

## Por qué usar MPD.

MPD es un reproductor de música que usa la estructura servidor/cliente, de forma que una vez instalado, el cliente que se use para la reproducción musical puede ser cualquiera de los muchos existentes. En este caso en particular explicaré como usar dos de ellos, uno será *ncmpcpp* y el otro será un cliente android llamado *_MPDroid_*, este último se puede encontrar tanto en *GooglePLayt* como en *F-Droid*.

Voy a destacar un par de ventajes que tiene el usar mpd.

- Es muy ligero, consume pocos recursos.
- Si podemos acceder a nuestro equipo desde fuera de casa es muy sencillo controlar mpd de forma remota, además de que el consumo de ancho de banda en ese control es muy pequeño.
- MPD tiene de forma nativa un servidor http con lo que se puede crear un servidor streaming de musica para nuestra LAN o incluso con salida a internet.
- Puede usar *ALSA* o *PulseAudio*. En caso de usar __pulseaudio__ podemos transmitir música directamente desde nuestro demonio mpd hacia cualquier tarjeta de sonido de nuestra LAN (aunque no lo he probado es compatible con dispositivos apple).
- Emisión directa hacia servidores ShoutCast y IceCast.
- Decodificación a través de ffmpeg.
- Multitud de clientes tanto CLI, GTK, QT y Android.
- Soporte de jerarquía de acceso a través de nombres de usuario y contraseñas.
- Soporte de expresiones regulares para hacer búsquedas en nuestra biblioteca de música.
- Posibilidad de iniciarlo como __systemwide__ o usuario al iniciar sesión.
- Letras de canciones.

## Instalación de MPD

Depende del sistema operativo se hará de una forma o de otra pero no debería suponer un gran problema.

- Debian/Ubuntu y derivados.

```
# apt-get update && apt-get install mpd
```

- Archlinux.

```
# pacman -Syy && pacman -S mpd
```

### Instalación del cliente _ncmpcpp_

- Debian

```
# apt-get install ncmpcpp
```

- Archlinux

```
# pacman -S ncmpcpp
```

## Configuración de MPD

Crear el fichero __~/.mpd/mpd.conf__ con el siguiente contenido:

```
# Estas rutas de ficheros y de directorios hay que crearlas a mano

# Ruta a nuestra biblioteca de música
music_directory     "~/music/"

playlist_directory  "~/.mpd/playlist"

pid_file            "~/.mpd/mpd.pid"
db_file             "~/.mpd/mpd.db"
state_file          "~/.mpd/mpdstate"
log_file            "~/.mpd/log"
sticker_file        "~/.mpd/sticker.sql"

# aquí se puede especificar por que interfaz escuchar
bind_to_address     "any"

# Con esta línea podemos usar ncmpcpp a modo de navegador de archivos
bind_to_address     "~/.mpd/socket"

# puerto de escucha del demonio mpd
port                "6600"

# nivel de log
log_level           "default"

input {
    plugin "curl"
}

### Líneas opcionales
#####################

# restaurar por donde se quedó al reiniciar mpd
restore_paused      "no"

# no hace falta decir para qué es esto
save_absolute_paths_in_playlists "no"

# no hace falta decir para qué es esto
auto_update             "yes"
follow_outside_symlinks "yes"
follow_inside_symlinks  "yes"

# en caso de usar avahi en la LAN se puede configurar zeroconf
zeroconf_enabled                "yes"
zeroconf_name                   "MPD zhora"

### Descomentar esta línea si se quioere password en la conexion
# y poner el password que se quiera

#password                       "password@read,add,control,admin"

# Esta linea descomentada establece cuales son los privilegios para una conexion sin password
#default_permissions            "read,add,control,admin"

### FIN Líneas opcionales


# configuración para emitir a un servidor icecast
audio_output {
    type        "shout"
    encoding    "ogg"                               # optional
    name        "Radio de pruebas"
    host        "icecast.example.com"
    port        "8000"
    mount       "/example"
    password    "hackme"
    bitrate     "128"
    #quality    "10"
    format      "44100:16:2"
    protocol    "icecast2"                          # optional
    user        "myuser"                            # optional
    description "Mi descripcion"                    # optional
    url         "http://icecast.example.com"        # optional
    genre       "varios"                            # optional
    mixer_type  "software"                          # optional
}

# Salida a pulseaudio
audio_output {
    type "pulse"
    name "My Pulse Output"
}


decoder  {
    plugin "ffmpeg"
    enabled "yes"
}

# Salida Alsa
audio_output {
    type "alsa"
    name "My ALSA Device"
    device "hw:0,0" # optional
}
```

## Ejecución de MPD

Por ahora solo explicaré como lanzarlo en modo usuario, de esta forma solo estará activo si iniciamos sesión con nuestro usuario.

- Archlinux

```
$ systemctl --user enable mpd.service --now
```

- Debian

```
$ systemctl --user enable mpd.service
$ systemctl --user start mpd.service
```

## Uso de ncmpcpp

En la misma máquina donde estamos ejecutando mpd:

```
$ ncmpcpp
```

1. Para actualizar la base de datos de ncmpcpp pulsar __u__.

2. Pulsar __F1__ para la ayuda.

3. Con las teclas del __1__ al __8__ podremos ir pasando desde la lista de reproducción actual hasta la pantalla de selección de salida.


