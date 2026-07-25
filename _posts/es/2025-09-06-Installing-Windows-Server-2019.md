---
title: Instalando Windows Server 2019
date: 2025-06-09 12:00:10 +0100

categories: [SysAdmin]

tags:
  - SysAdmin
  - Spanish

toc: true
toc_sticky: true
excerpt: Un tutorial de como instalar Windows Server 2019

language: es
ref: installing-windows-server-2019
lang_en: /en/installing-windows-server-2019
lang_es: /es/installing-windows-server-2019
lang_ja: /jp/installing-windows-server-2019
permalink: /es/installing-windows-server-2019
---

### ¿De que trata este post?

A lo largo de este post vamos a explorar y aprender como instalar Windows Server 2019, en una máquina virtual para utilizarlo para otros propositos. Para tener un poco de contexto de este OS, Windows Server es una rama, de la rama principal de sistemas operativos de Windows orientada a la isntalación de servidores. Aun cuándo existe una gran parte del mercado que utiliza Linux aún así existen empresas que por compatibilidad empresarial u otros motivos necsitan utilizar Windows Server,.

### Pasos a seguir

#### Instalando un sistema de virtualización en el sistema

Lo primero que vamos a hacer es instalar un sistema de virtualización para el sistema (o también conocido como máquina virtual), para ello utilizaremos [VirtualBox](https://www.virtualbox.org/) de Oracle, para instalarlo puedes hacer click en este [link](https://www.virtualbox.org/wiki/Downloads)

Es recomendable que también instales el paquete de extensiones de VirtualBox, esto añadirá funcionalidades adicionales, si quieres saber más información puedes pulsar [aquí](com/en/virtualization/virtualbox/6.0/user/intro-installing.html)
{: .notice--info }

![VirtualBox-Main-Download-Page](/assets/images/Installing-Windows-Server-2019/Virtual-Box-Main-Page.png)

#### Obteniendo la ISO de Windows Server 2019

Lo siguiente que vamos a hacer será descargar la ISO de Windows Server 2019, para ello lo primero que tendremos que hacer es ir a esta [página](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019), tendremos que seleccionar el idioma y la versión que queremos.

Por favor recuerda que estamos instalando la versión de prueba de Windows Server 2019, por lo que el sistema operativo puede eliminar los archivos y reinicarse a fábrica tras los 120 días, así que vas a usarlo para desplegar un sistema por favor obtenga una licencia o no lo use junto a archivos importantes.
{: .notice--warning}

![WindowsServer-Main-Download-Page](/assets/images/Installing-Windows-Server-2019/Windows-Server-2019-Main-Down-Page.png)

#### Configurando VirtualBox

##### Información de la ISO

Ahora que hemos instalado y descargado VirtualBox y la ISO de Windows Server 2019, vamos a presionar en VirtualBox el botón que dice: "Nuevo", y se nos abrirá una página donde se nos preguntará, el nombre de la máquina, donde queremos que se guarde y el OS que nos encontramos emulando. No tenemos que rellenar todas las opciones ya que normalmente con la ISO, VirtualBox puede reconocer alguna información.

Si no nos encontramos haciendo ninguna prueba con ADK, desahabilitamos la opción de instalación desantendida.

Una instalación desatendida, es cuándo tu usas el Windows ADK para desarrollar una instalación con configuraciones ya prehechas, es interesante conocerlo si vas a realizar la instalación en múltiples dispositivos.

![VirtualBox-Main-Configuration-page](/assets/images/Installing-Windows-Server-2019/Configure-Page-VirtualBox.png)

##### Configuración del Hardware

Lo siguiente que vamos a hacer es seleccionar cuanta memoria y procesadores queremos proporcionarle. Es bueno recordar que esto depende del sistema nativo (el real) que tenemos. Los requisitos minimos de Windows Server 2019 son:

- 2GB para la experiencia de Servidor / 4GB para la experiencia con Interfaz Gráfica (nos adentraremos más en la siguiente sección).
- Depende de las aplicaciones y servicios que vayamos a desplegar, para el OS solo necesitamos 2, aunque lo recomendado serían 4.

![VirtualBox-Hardware-Page](/assets/images/Installing-Windows-Server-2019/Virtual-Box-Hardware-Page.png)

##### Virtual Disk Configuration

##### Configuración de discos virtuales

Lo siguiente que vamos a hacer es crear un disco virtual. Aquí ocurre lo mismo que en la sección del hardware y es que dependerá mucho de nuestra máquina fisica, los requisitos minimos de Microsoft son:

- 32GB de espacio libre

![VirtualBox-Virtual-Disk-Page](/assets/images/Installing-Windows-Server-2019/Virtual-Box-Disk-Configuration-Page.png)

#### Configurando el OS

Si hemos hecho todo correctamente llegaremos a esta ventana, donde tendremos que seleccionar nuestro idioma, la zona horario donde nos encontramos y la configuración del teclado.

Si lo descargas desde el link que he proporcionado puede que no aparezca esta función que ya poseen configurada el lenguaje predeterminado.
{: .notice--info}

![WindowsServer-Startup-Page](/assets/images/Installing-Windows-Server-2019/Windows-Server-2019-Startup-Page.png)

La siguiente opción será

- Windows Server 2019 Standard Edition (With/Without GUI)
- Windows Server 2019 Datacenter Edition (With/Without GUI)

Si quieres saber que versión usar, usa esta [guía](https://learn.microsoft.com/en-us/windows-server/get-started/editions-comparison?pivots=windows-server-2019) de microsoft para conocer más acerca de ellas.

![WindowsServer-Edition-Selection-Page](/assets/images/Installing-Windows-Server-2019/Windows-Server-2019-Selection-Edition-Screen.png)

Y por último tendremos que cambiar la contraseña por defecto del sistema.

![WindowsServer-Pass-Page](/assets/images/Installing-Windows-Server-2019/Windows-Server-2019-Change-Pass-Pg.png)

#### Final

Con esto hemos configurado de manera exitosa Windows Server 2019 en una máquina virtual, próximamente haré más tutoriales con más información.
