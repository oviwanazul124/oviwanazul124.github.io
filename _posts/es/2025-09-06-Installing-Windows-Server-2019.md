---
title: "Instalando Windows Server 2019 "
date: 2025-06-09 12:00:10 +0100
categories: [Game Develop]
tags: [Game Develop, Maths, English]
description: Un pequeño tutorial de como instalar Windows Server 2019 en una máquina virtual.
math: false
lang: es
translations:
  ja: /ja/installing-windows-server-2019/
  en: /posts/installing-windows-server-2019/
  es: /es/installing-windows-server-2019/
permalink: /es/installing-windows-server-2019/
---

### ¿De que va este post?

---

Durante este post vamos a aprender como instalar Windows Server 2019, en una maquina virtual para usarlo para multiples propositos.Para tener un poco de contexto este sistema operativo se trata de la rama de sistemas dedicados a hostear servidores, como su nombre indica, en el mercado actual las estadisticas muestran que las personas suelen elegir distros de linux antes que Windows Server, pero compañias siguen utilizandolo por su compatibilidad con aplicaciones empresariales que no son posibles de usar en linux o que todavía no tienen soportes ademas de sistemas que no han sido actualizados por un largo tiempo, gracias a que esta versión del OS es la más utilizada. Ahora que conocemos un poco la historia vamos a empezar.

---

### Pasos a seguir

#### Instanlando el sistema de virtualización de OS

La primera cosa que tenemos que hacer es instalar el sistema de virtualización para el OS (También conocido como maquina virtual), para este tutorial vamos a usar [VirtualBox](https://www.virtualbox.org/) de Oracle, puedes instalarlo desde [este](https://www.virtualbox.org/wiki/Downloads) link.

> Es recomendado instalar el paquete de extensiones de VirtualBox, esto añadira multiples funcionalidades extras, si quieres saber más puedes obtener más información [aqui](https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/intro-installing.html)
{: .prompt-info}

![VirtualBox-Main-Download-Page](assets/photos/Installing-Windows-Server-2019/Virtual-Box-Main-Page.png)
_VirtualBox Página Principal de Descarga_

#### Obteniendo el ISO de Windows Server 2019

Lo siguiente que vamos a hacer será instalar el ISO the Windows Server 2019, para esto tendremos que ir a esta [página](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019) y seleccionar el idioma que queremos.

> Porfavor, recordad que estaremos descargando la versión TRIAL(Prueba) de Windows Server 2019, esta versión eliminará todos los archivos alrededor de 120 días despues de la instalación, si vas a utilizarlo para desplegar un sistema o guardar archivos importantes activa la licencia.
{: .prompt-warning}

![WindowsServer-Main-Download-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Main-Down-Page.png)
_Página Principal de Windows Server_

#### Configurando VirtualBox

##### Información del ISO

Ahora que hemos instalado VirtualBox y el ISO de Windows Server 2019, presionaremos el botón que dice: "Nuevo", y ahora se abrirá una nueva página donde nos preguntará sobre nuestro nombres, donde queremos guardar nuestra máquina virtual y seleccionar el OS que vamos a emular. No nos tenemos que preocupar por rellenar toda la información, ya que al introducir la imagen ISO, pondrá toda la información

Si no estamos utlizando el Windows ADK o no vamos a usar una instalación no atendida, podremos deshabilitar esta opción.

> Una instalación desatendida de Windows, es cuando usamos el ADK de Windows para crear una instalación con una configuración prehecha, sirve bastante para cuando tienes que hacer multiples configuraciones.
{: .prompt-info}

![VirtualBox-Main-Configuration-page](assets/photos/Installing-Windows-Server-2019/Configure-Page-VirtualBox.png)
_Página Principal de Configuración de VirtualBox_

##### Configuración del Hardware

A continuación tenemos que configurar cuantos procesadores y memoria queremos que la máquina use. Debemos recordar que estás opciones dependerán del sistema que estemos usando. Los requisitos minimos para Windows Server 2019 son:

- 2GB para la experiencia de Servidor / 4GB para la experiencia de IU (Interfaz de Usuario).
- Procesadores dependen de la aplicación que vayamos a desplegar, pero el sistema operativo podra con 2, aunque se recomiendan 4.

![VirtualBox-Hardware-Page](assets/photos/Installing-Windows-Server-2019/Virtual-Box-Hardware-Page.png)
_Página de Hardware de VirtualBox_

##### Configuración del Disco Virtual

Ahora debemos seleccionar cuanto espacio queremos otorgarle a la máquina virtual. Esto también dependerá de tu dispositivo, pero los requisitos minimos son:

- 32GB de espacio libre

![VirtualBox-Virtual-Disk-Page](assets/photos/Installing-Windows-Server-2019/Virtual-Box-Disk-Configuration-Page.png)
_Página de Disco Virtual de VirtualBox_

#### Configurando el OS

Si hemos hecho todo de manera correcta llegaremos a esta pantalla, aquí tendrás que seleccionar el lenguaje, la zona horaria y la selección de la configuración.

> Si has descargado el ISO del link proporcionado en la guía solo estará disponible el lenguaje seleccionado
{: .prompt-info}

![WindowsServer-Startup-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Startup-Page.png)
_Página de Inicio de Windows Server_

La próxima opción será las ediciones:

- Windows Server 2019 Edición Estandar (Con/Sin IU)
- Windows Server 2019 Edición Datacenter (Con/Sin IU)

Si quieres saber que versión deberías utilizar puedes usar esta [web](https://learn.microsoft.com/en-us/windows-server/get-started/editions-comparison?pivots=windows-server-2019) para observar que carácteristicas tienen cada uno.

![WindowsServer-Edition-Selection-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Selection-Edition-Screen.png)
_Windows Server 2019 Página de Selección_

La última cosa que tenemos que hacer será cambiar la contraseña de administrador

![WindowsServer-Pass-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Change-Pass-Pg.png)
_Windows Server 2019 Cambiando La Contraseña_

#### Finalizando

Con esto hemos instalando Windows Server 2019 en una máquina virtual, próximamente haré más tutoriales en estos puntos.
