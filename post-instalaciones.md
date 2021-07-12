# debian-testing
Mis configuraciones para Debian Testing Gnome.

## Intro
A continuación están mis configuraciones para **Debian Testing Gnome**. Actualmente lo estoy utilizando con wyland.

## Contenido
- [1. Habilitar sudo](#1-habilitar-sudo)
- [2. Repostorios non-free](#2-repositorios-non-free)
- [3. Instalar firmware](#3-instalar-firmware)
- [4. Habilitar botón minimizar](#4-habilitar-boton-minimizar)
- [5. Instalar microcode](#5-instalar-microcode)
- [6. Instalar build-essential](#6-instalar-build-essential)
- [7. Configurar Swappiness](#7-configurar-swappiness)
- [8. Aumentar la velocidad de inicio](#8-aumentar-la-velocidad-de-inicio)
- [9. Extender bateria para notebooks](#9-extender-bateria-para-notebooks)
- [10. Habilitar extensiones gnome](#10-habilitar-extensiones-gnome)

## 1. Habilitar sudo
Lo primero para empezar a trabajar es habilitar el sudo, ya que por defecto en Debian viene deshabilitado.
Para ello vamos a cambiar al usuario root y editar el archivo sudoers, para agregar nuestro usuario.

```sh
su -
vi /etc/sudoers
```
## 2. Repositorios non-free
Este es el primer paso para solucionar problemas con paquetes non-free, como el wifi. Para crear los repositorios de debian stable o testing, los podemos realizar en el siguiente enlace <a href="https://debgen.simplylinux.ch/">debgen</a>

Una vez generados los repositorios se deben pegar en el archivo correspondiente.

*Se debe comentar todo el contenido y pegar la información generada en la página.*

```sh
sudo vi /etc/apt/sources.list
sudo apt update
sudo apt upgrade -y
```

## 3. Instalar firmware
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

## 4. Habilitar botón minimizar
Para mostrar el botón minimizar, se debe abrir **gnome tweaks** y habilitar el botón en la sección **Barra de títulos de ventana**

![image](https://user-images.githubusercontent.com/20421050/125217960-e2e82f00-e28f-11eb-9101-46d684781989.png)

## 5. Instalar microcode
Microcode es un firmaware para la CPU que controla cómo trabaja el procesador. En mi caso tengo un procesador Intel, por lo que se debe instalar

```sh
sudo apt install intel-microcode -y
```

## 6. Instalar build-essential

```sh
sudo apt install build-essential dkms linux-headers-$(uname -r) -y
```

## 7. Configurar Swappiness
El uso de la memoria swap está configurada en 60 por defecto, que para la mayoría de los casos está bien. Pero si disminuimos éste número el sistema utilizará más **RAM** y comenzará a utilizar la swap más tarde.

Chequear valor swapiness

```sh
cat /proc/sys/vm/swappiness
```

Abrir y editar el archivo de conf de swap

```sh
sudo vim /etc/sysctl.conf
```

Pegar el siguiente contenido el final del archivo *vm.swappiness = 10*

***Guardar y reiniciar el sistema***

## 8. Aumentar la velocidad de inicio
Al momento de inciar el sistema nos muestra el menú del **grub**. Ésto es útil cuando tenemos más de un S.O. instalado en nuestro dispositivo, pero si no es el caso entonces vamos a omnitir este paso.

Editar el archivo de configuración del grub

```sh
sudo vim /etc/default/grub
```

Dejar la propiedad **GRUB_TIMEOUT** en 0, como muestra la siguiente imágen

![image](https://user-images.githubusercontent.com/20421050/125221015-90aa0c80-e295-11eb-9386-45ed1eca97b7.png)

Luego de editado el archivo debemos actualizar la configuración del grub

```sh
sudo update-grub
```

## 9. Extender bateria para notebooks
Si estamos corriendo **Debian** en un notebook, podemos extender el tiempo de la batería con la herramienta TLP

```sh
sudo apt install tlp -y
```

Después de la instalación, reiniciamos el sistema y podemos verificar el proceso corriendo con el siguiente comando

```sh
sudo systemctl status tlp
```

## 10. Habilitar extensiones gnome
- Caffeine
- OpenWeather
- Remove Dropdown Arrows
- Sound Input & Output Device Chooser
- Tray Icons: Reloaded
- Workspace indicator
- *Workspace Matrix **(opcional)***
- *ArcMenu **(opcional)***
- *Dash to Dock **(opcional)***
- *Dash to Panel **(opcional)***
