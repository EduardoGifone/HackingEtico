# Permisos y derechos en linux

***

## Fuentes
[Permisos basicos de GNU](https://blog.desdelinux.net/permisos-basicos-en-gnulinux-con-chmod/)
[Permisos y derechos en linux](https://blog.desdelinux.net/permisos-y-derechos-en-linux/)

## Permisos en archivos

|Permiso|archivo|directorio|
|-|-|-|
|read|visualizar contenido|ver archivos que contiene|
|write|modificar contenido|agregar, remover o mover archivos|
|execute|ejecutar el archivo|poder atraversarlo (cd)|

## Cambiar permisos

*chmod* (change mode)
* Agregar o remover permisos
    * *+* *-*

```
$ chmod -rwx archivo
$ chmod -w tuArchivo
$ chmod =r archivo
```

## Usuarios, grupos y otros
* Usuario (u) rwx------
* Grupo (g) ---rwx---
* Otros (o) ------rwx

```
$ chmod g-x,o-x archivo
$ chmod u-x archivo
$ chmod u-x+w archivo
```

### chmod en octal

||octal|permisos|
|-|-|-|
| rwx |  7  | Lectura, escritura y ejecución|
| rw- |  6  | Lectura, escritura|
| r-x |  5  | Lectura y ejecución|
| r-- |  4  | Lectura|
| -wx |  3  | Escritura y ejecución|
| -w- |  2  | Escritura|
| --x |  1  | Ejecución|
| --- |  0  | Sin permisos|

```
$ chmod 775 > chmod u=rwx,g=rwx,o=rx
```

## Tipos de archivos o directorios

|permiso|identifica|
|-|-|
|-|archivo|
|d|Directorio|
|b|Archivo de bloques especiales (Archivos especiales de dispositivo)|
|c|Archivo de caracteres especiales (Dispositivo tty, impresora…)|
|l|Archivo de vinculo o enlace (soft/symbolic link)|
|p|Archivo especial de cauce (pipe o tubería)|

## Campos
![Campos](https://blog.desdelinux.net/wp-content/uploads/2012/01/ls-l-Explicacion.png)

[Enlaces duros y simbolicos](https://rm-rf.es/diferencias-entre-soft-symbolic-y-hard-links/)

## Permisos especiales

### SETUID
Set User ID
* Permite que cuando un usuario ejecute dicho fichero, el proceso adquiera los permisos del propietario del fichero ejecutado.

```
$ su
$ chmod u+s /bin/su
```

### SETGID
Set Group ID
* Permite adquirir los privilegios del grupo asignado al fichero, también es asignable a directorios.

```
$ chmod g+s /carpeta_compartida
```

### STICKY
* Suele asignarse en directorios a los que todos los usuarios tienen acceso, y *permite evitar que un usuario pueda borrar ficheros/directorios de otro usuario dentro de ese directorio*, ya que todos tienen permiso de escritura.

```
$ chmod +t /test
```

## GFTOBins
[GFTOBins para explotar proviligeos](https://gtfobins.github.io/)

## Buscar binarios con bit SUID

    $ find \-perm -4000 2> /dev/null

## Buscar archivos con capacidad de escritura

    $ find \-writable