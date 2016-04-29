# Práctica 6

## 1. Configuración del RAID 1

Primero de todo añadimos 2 discos a nuestra VM. Un vez arrancada, listamos los discos disponibles con el comando `fdisk -l` y descubrimos que los discos añadidos tienen nombre de **sdb** y **sdc**. A continuación instalamos **mdadm** con el comando `apt-get install mdadm`. 
Creamos el RAID 1 con el comando `mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc`, le damos formato con el comando `mkfs /dev/md0`, creamos el directorio donde lo vamos a montar con `mkdir /dat` y lo montamos con `mount /dev/md0 /dat`. Una vez hecho esto, comprobamos el estado del RAID con `mdadm --detail /dev/md0 `. A continuación editamos el archivo `fstab` para que se monte el dispositivo RAID al arrancar el sistema, para ello tenemos que sacar el `UUID` del mismo con `ls -l /dev/disk/by-uuid`.

- [Información de los discos](http://s1380.photobucket.com/user/adnan1989/media/info discos_zpsqi6kbhmr.png.html)
- [Creando RAID](http://s1380.photobucket.com/user/adnan1989/media/crear raid_zpshfqtzsa9.png.html)
- [Formateando dispositivo RAID](http://s1380.photobucket.com/user/adnan1989/media/formateo raid_zps88psck9u.png.html)
- [Creando directorio y montando dispositivo RAID](http://s1380.photobucket.com/user/adnan1989/media/directotrio montar raid_zps1tdnrbch.png.html)
- [Estado del RAID](http://s1380.photobucket.com/user/adnan1989/media/estado raid_zpssjchgfjr.png.html)
- [Sacando UUID del RAID](http://s1380.photobucket.com/user/adnan1989/media/uuid raid_zpsurivladb.png.html)
- [Editando 'fstab'](http://s1380.photobucket.com/user/adnan1989/media/fstab edit_zpswky8xybi.png.html)


## 2. Manipulación del dspositivo RAID

Una vez configurado, vamos a provocarle un fallo a uno de los discos que lo compone, a retirarlo "en caliente" y a restaurarlo de nuevo. Para provocar el fallo ejecutamos el comando `mdadm --manage --set-faulty /dev/md0 /dev/sdb`, para retirarlo "en caliente" lo hacemos con `mdadm --manage --remove /dev/md0 /dev/sdb` y para restaurarlo ejcutamos `mdadm --manage --add /dev/md0 /dev/sdb`. Cada vez que ejecuctamos los comandos anteriormente citados, vamos viendo los cambios con `mdadm --detail /dev/md0`.

- [Provocando fallo](http://s1380.photobucket.com/user/adnan1989/media/fallo raid_zpsjpy9tukg.png.html)
- [Retirando "en caliente"](http://s1380.photobucket.com/user/adnan1989/media/retiro en caliente raid_zpsseaqcw1j.png.html)
- [Restaurando "en caliente"](http://s1380.photobucket.com/user/adnan1989/media/antildeadido en caliente_zpsbufpc77g.png.html)
