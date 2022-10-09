---
title: 'Instalación QEMU/libvirt. Conexión local y remota'
date: 2022-10-09T19:27:37+10:00
weight: 2
summary: En esta entrada se instala qemu/libvirt y se hace una introdución a virsh.
---
_______________




**1. Una vez instalado el sistema de virtualización en tu equipo, entrega la salida del comando virsh version.**

```
arantxa@debian:~$ virsh version
Compilada con biblioteca: libvirt 7.0.0
Uso de biblioteca: libvirt  7.0.0
Utilizando API: QEMU 7.0.0
Ejecutando hypervisor: QEMU 5.2.0
```

**2. Ejecuta el comando list de virsh realizando una conexión privilegiada con tu usuario sin privilegios (no uses el root).**

```
arantxa@debian:~$ virsh -c qemu:///system list
 Id   Nombre         Estado
---------------------------------
 4    debianprueba   ejecutando
```

**3. Una vez creada la máquina en gnome-boxes responde y razona la siguiente pregunta: ¿Por qué al ejecutar virsh -c qemu:///system list --all no aparece la máquina creada por gnome-boxes?**

Al hacer 'virsh -c qemu:///system list --all' no aparece la máquina creada en gnome-boxes porque estamos haciendo una conexión privilegiada con el usuario sin privilegios. Es decir, se nos mostrarán las máquinas del sistema pero no las del usuario.
```
arantxa@debian:~$ virsh -c qemu:///system list --all
 Id   Nombre         Estado
---------------------------------
 4    debianprueba   ejecutando
```

**4. Entrega la instrucción y la salida del comando virsh que muestra en el terminal la máquina creada en gnome-boxes.**

Al hacer una conexión local con el usuario no privilegiado nos aparece la máquina creada en gnome-boxes.
```
arantxa@debian:~$ virsh -c qemu:///session list --all
 Id   Nombre        Estado
-----------------------------
 -    ubuntu20.10   apagado
```

**5. Entrega la instrucción y la salida del comando virsh haciendo una conexión remota a un equipo de un compañero. Explica los principales pasos para configurar tu equipo para que se puedan realizar conexiones remotas.**

He hecho una conexión remota desde otro portátil en casa a mi portátil de trabajo.
Antes de conectarme en la maquina remota he copiado la clave pública SSH del usuario cliente al fichero ~/.ssh/authorized_keys de la máquina remota.
El usuario remoto será arantxa y la ip la 192.168.1.136. He listado las maquinas virtuales del equipo remoto para comprobar que ha funcionado. El comando usado y la salida generada es la siguiente:
```
virsh -c qemu+ssh://arantxa@192.168.1.136/system list --all

  Id   Name              State
----------------------------------
  -    debianprueba      shut off
  -    linux_arantxa     shut off
  -    vagrant_default   shut off
```
