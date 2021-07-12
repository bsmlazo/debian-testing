# debian-testing
Mis configuraciones para Debian Testing Gnome.

## Intro
A continuación están mis configuraciones para **Debian Testing Gnome**. Actualmente lo estoy utilizando con wyland.

## Contenido
- [Habilitar sudo](#habilitar-sudo)
- [Repostorios non-free](#repositorios-non-free)
- [Instalar firmware](#instalar-firmware)
- [Instalar firmware](#instalar-firmware)

## Habilitar sudo
Lo primero para empezar a trabajar es habilitar el sudo, ya que por defecto en Debian viene deshabilitado.
Para ello vamos a cambiar al usuario root y editar el archivo sudoers, para agregar nuestro usuario.

```sh
su -
vi /etc/sudoers
```
## Repositorios non-free
Este es el primer paso para solucionar problemas con paquetes non-free, como el wifi. Para crear los repositorios de debian stable o testing, los podemos realizar en el siguiente enlace <a href="https://debgen.simplylinux.ch/">debgen</a>

Una vez generados los repositorios se deben pegar en el archivo correspondiente.

*Se debe comentar todo el contenido y pegar la información generada en la página.*

```sh
sudo vi /etc/apt/sources.list
sudo apt update
sudo apt upgrade -y
```

## Instalar firmware
En debian es muy frecuente tener problemas con el firmware no libre, como el wifi. Para ello vamos a instalar los siguiente paquetes que estan arrojando error en los mensajes del sistema.

Si queremos revisar los mensajes de error, podemos ejecutar lo siguiente

```sh
sudo dmesg
```

Instalar los paquetes restantes

```sh
sudo apt install firmware-iwlwifi firmware-misc-nonfree firmware-realtek firmware-sof-signed -y
```
***Reiniciar sistema.***
