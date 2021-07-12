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

Después de reiniciar el sistema configuramos los repositorios con la aplicación **software & updates**

*Pestaña Debian software*

![image](https://user-images.githubusercontent.com/20421050/125216660-dadac000-e28c-11eb-9946-82ae2b54c0f0.png)

*Pestaña Updates*

![image](https://user-images.githubusercontent.com/20421050/125217234-2a6dbb80-e28e-11eb-81d1-f9867ebe4107.png)

Nuevamente actualizamos el sistema.

```sh
sudo apt update
sudo apt upgrade -y
```

## Habilitar botón minimizar
Para mostrar el botón minimizar, se debe abrir **gnome tweaks** y habilitar el botón en la sección **Barra de títulos de ventana**

![image](https://user-images.githubusercontent.com/20421050/125217960-e2e82f00-e28f-11eb-9101-46d684781989.png)

## Instalar microcode
Microcode es un firmaware para la CPU que controla cómo trabaja el procesador. En mi caso tengo un procesador Intel, por lo que se debe instalar

```sh
sudo apt install intel-microcode -y
```

## Instalar build-essential

```sh
sudo apt install build-essential dkms linux-headers-$(uname -r) -y
```

## Configurar Swappiness
El uso de la memoria swap está configurada en 60 por defecto, que para la mayoría de los casos está bien. Pero si disminuimos éste número el sistema utilizará más **RAM** y comenzará a utilizar la swap más tarde.

Chequear valor swapiness

```sh
cat /proc/sys/vm/swappiness
```
