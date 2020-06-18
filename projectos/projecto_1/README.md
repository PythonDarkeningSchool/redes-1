# Tabla de Contenidos



# Pre-requisitos

<details>
  <summary>Click aqui para ver los pre-requistos</summary>
  
## Multipass

![multipass](assets/img/multipass_logo.png)

[Multipass](https://multipass.run) proporciona una interfaz de línea de comandos para iniciar, administrar y, en general, jugar con instancias 
de Linux. La descarga de una imagen fresca lleva unos segundos, y en cuestión de minutos una VM puede estar en 
funcionamiento.

[Multipass](https://multipass.run) es un software gratuito desarrollado por Ubuntu que permite instalar maquinas virtuales de manera similar
a que si las tuvieramos en un [container](https://www.docker.com).
Las ventajas de Multipass a comparacion de las clasicas maquinas virtuales es basicamente que no se necesita un gran
equipo para poder instancias de ubuntu.
Cuando se habla de una instancia se hace referencia a una imagen que contiene cierto sistema operativo.

### Instalando Multipass

El siguiente link lleva a la descarga de un ejecutable desde el sitio oficial:

- :link: [Link de descarga](https://github.com/canonical/multipass/releases/download/v1.2.1/multipass-1.2.1%2Bwin-win64.exe)

### Habilitando Hyper-V en Windows

Para poder correr cualquier maquina virtual en Windows tenemos que habilitar `Hyper-V`, que por default viene deshabilitado.

Para poder habilitarlo basta con abrir Windows Power Shell (como Administrador), escribir el siguiente comando y reiniciar:

```bash
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

> Si no sabe como abrir Windows Power Shell en Windows vea el siguiente video [como abrir Windows Power Shell en Windows](https://www.youtube.com/watch?v=doUhN9YwZ6U)

</details>

# Instalando la maquina virtual

Para instalar la maquina virtual lo haremos a travez de `multipass`, lo cual nos creara una instancia de ubuntu
de manera muy sencilla a la cual podemos acceder muy facilmente y sin necesitar gran cantidad de recursos de nuestro
sistema.

## Creando el servidor

Con el siguiente comando crearemos el servidor en una VM de ubuntu con version 18.04

```bash
multipass launch bionic --name servidor
```

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![multipass_launch_cmd](assets/img/multipass_launch_cmd.png)

</details>


## Instalando paquetes en el servidor

Una vez creado el servidor, procederemos a instalar paquetes para poder crear nuestro servidor proxy, para eso tendremos
que estar dentro del servidor antes de poder instalar cualquier paquete.

Inserta el siguiente comando en la terminal para poder entrar al servidor

````bash
multipass shell servidor
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![multipass_shell_cmd](assets/img/multipass_shell_cmd.png)

</details>

Una vez dentro del servidor procederemos a instalar los paquetes necesarios

Inserta el siguiente comando para actualizar los paquetes que ya contiene nuestro servidor

```bash
sudo apt update -y && sudo apt upgrade -y
```

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![apt_update](assets/img/apt_update.png)

</details>

Inserta el siguiete comando para instalar el servidor proxy `squid`

```bash
sudo apt install vim squid -y
```

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![squid_cmd](assets/img/squid_cmd.png)

</details>

Inserta el siguiente comando para eliminar los paquetes innecesarios del servidor

````bash
sudo apt autoremove -y
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![autoremove_cmd](assets/img/autoremove_cmd.png)

</details>

Inserta el siguiente comando para reiniciar el servidor

```bash
sudo reboot
```

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![reboot_cmd](assets/img/reboot_cmd.png)

</details>

Inserta el siguiente comando para forzar el inicio del servidor con `multipass`

````bash
multipass start servidor
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![multipass_start_server_cmd](assets/img/multipass_start_server_cmd.png)

</details>