
![win](./escritorioremotowin.jpeg)

# Introducción
Vamos a trabajar la actividad con los siguientes SSOO:
* Windows7
* Windows 2008 Server
* GNU/Linux Debian7.

Entrega:
* Al finalizar entregar URL con la ruta al/los archivo/s dentro del repositorio del alumno.
* Al terminar la práctica etiquetaremos la entrega en el repositorio Git con `vnc`.

Configuración de las máquinas virtuales:
* Poner en las MV la configuración de red en modo puente.
* Las máquinas que actuen de servidor o aquellas a las que nos vamos a conectar de forma repetida deben tener IP estática.
    * IP Windows7 172.18.XX.12
    * IP W2k8 172.18.XX.22
    * IP Debian7 172.18.XX.32

# 1. Escritorio remoto con VNC
* Leer la documentación sobre conexiones VNC.
* Capturar imágenes de la instalación y configuración VNC para poder acceder a una máquina remota. 

> NOTA:
> 
> * TightVNC o RealVNC, son algunas herramientas libres disponibles para Windows.
> * Si usan un servidor VNC "MarcaX", usar también el cliente "MarcaX".
> * Para esta práctica usaremos conexiones SIN cifrar.
>
> Enlaces de interés
>
> * [VNC GNU/Linux] (http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m5/servidor_vnc.html)
>

Capturar imagenes probando las conexiones remotas VNC, y ejecutando el 
comando `netstat -ntap` en cada caso, para verificar que se han establecido 
las conexiones remotas:

1. Acceder a Windows - desde Windows
1. Acceder a Windows - desde Linux
1. Acceder a Linux - desde Linux (A lo mejor no hay que instalar el software cliente VNC)
1. Acceder a Linux - desde Windows

# 2. Escritorio Remoto con RDP

Realizar las siguientes tareas:

* Leer la documentación sobre escritorio remoto.
* En Windows no hay que instalar nada, puesto que ya viene con el software de escritorio remoto RDP preinstalado.


* Capturar imagen de la configuración escritorio remoto para poder acceder a otra máquina 
(`Panel de control -> Sistema -> Configuración de Acceso Remoto`).
* Capturar imagenes probando las conexiones remotas, y ejecutando el 
comando `netstat -ntap` en cada caso, para verificar que se han establecido 
las conexiones remotas:
    1. **Acceder a Windows7 - desde Window Server**: El software ya viene preinstalado, sólo falta configurarlo.
    1. **Acceder a Windows7 - desde Linux**: Instalar software cliente RDP en GNU/Linux. Ejemplos de clientes RDP son: Cliente escritorio remoto de Remmina, vinagre (Usando protocolo RDP), rdesktop, tsclient, grdesktop, krdc, etc. Otra opción usar Knoppix CDLive que ya viene con el software cliente preinstalado.
    1. **Acceder a Linux - desde Windows7**: En Linux instalamos xrdp. Es un servidor de conexiones remotas por protocolo RDP. 
    Desde Windows iniciamos escritorio remoto. En la ventana de login ponemos modulo="vnc-any", ip="ip-de-la-máquina-Linux".

> Enlaces de interés:
>
> * [XRDP: Instalar y configurar en ubuntu-12-10] (http://www.adslfaqs.com.ar/como-instalar-y-configurar-xrdp-en-ubuntu-12-10-quantal-quetzal/)
> * [XRDP: Remote desktop para Ubuntu] (http://www.pacorabadan.com/?p=283)


# 3. Servidor de Terminales

> Información sobre TS:
>
> * Si está [instalando el servicio de función Terminal Server] (https://technet.microsoft.com/es-es/library/cc754288%28v=ws.10%29.aspx) en un controlador de dominio, recibirá un mensaje de advertencia porque NO es recomendable instalar el servicio de función Terminal Server en un controlador de dominio.
> * Para obtener más información, consulte la página sobre la instalación de Terminal Server en un controlador de dominio en la [Ayuda de Terminal Server en la biblioteca técnica de Windows Server 2008] (http://go.microsoft.com/fwlink/?LinkId=109277, puede estar en inglés).

##3.1 Realizar las siguientes tareas

* Leer el documento que se proporciona sobre la conexión Terminal Server entre máquinas Windows.
* Necesitamos una MV con Windows Server que NO sea controlador de dominio.
* Instalar el rol de Terminal Server, agregando sólo: Servidor de Terminales y Acceso Web para TS

> NOTA:
>
> Es necesario tener el SO actualizado para poder realizar la instalación de los componentes de forma correcta. Por lo que actualizaremos el servidor y volvemos a desactivar las actualizaciones automáticas de Windows Update.
>
> En W2k8server RC2, Terminal Service tiene un nombre diferente. Para instalarlo hay que hacer lo siguiente: Agregar roles -> Servicio de Escritorio Remoto -> Host de Sesión de Escritorio Remoto.
>
> IMPORTANTE: Estar atento y leer todos los mensajes para tener claro qué tenemos permitido hacer según la licencia, y que no (Incluir resumen de la licencia en el informe). Traten de entender todos los pasos.

##3.2 Configurar y probar conexiones al terminal server
Crear usuarios locales:
* Abrir `Administrador de. servidor -> Configuración -> Usuarios locales y grupos`.
* Crear varios usuarios. Por ejemplo, usar los nombres en minúsculas de los miembros del grupo.
* Añadir usuarios al grupo de acceso remoto.

Veamos un ejemplo de la creación de usuarios:
![ts-users](./ts-w2k8-users.png)

* Capturar imagenes probando las conexiones remotas, y ejecutando el 
comando `netstat -ntap` en cada caso, para verificar que se han establecido 
las conexiones remotas:
    1. Probar la conexión remota de escritorio RDP, desde el cliente Windows hacia el servidor Windows Server.
    1. Probar la conexión remota de escritorio RDP, desde el cliente Linux hacia el servidor Windows Server.
    1. Ambas conexiones de escritorio remoto deben estar funcionando simultáneamente.

> Enlace de Interés:
>
> * [Instalación de Terminal Services en Windows 2008] (http://www.bujarra.com/ProcedimientoW2008TSinstalacion.html)
> * [Vídeo de Youtube] (https://www.youtube.com/watch?v=Z_UeSGRqcG0)

#4. Aplicaciones remotas mediante RemoteApp
Realizar las siguientes tareas sólo con servidor Windows 2008 server y cliente Windows 7:
* Leer la documentación PDF proporcionada por el profesor sobre aplicaciones remotas (Consultar documentación de servidor de terminales).
* Instalar una aplicación en Windows Server que no esté en Windows7, por ejemplo Geany.
* La idea de RemoteApp es tener una aplicación instalada en el Windows Server pero que pueda ejecutarse desde el Windows7. Hay tres formas de implementar el RemoteApp:
    1. Publicar la aplicación en el sitio web del RemoteApp, por defecto https://servidor_remote_app/rdweb.
    1. Mediante la creación de un paquete instalable .msi, muy útil para instalarlo mediante GPO.
    1. Creando un archivo de conexión remota .rdp. Vamos a usar este último método.

> NOTA:
>
> * En las configuraciones usar las IP's de las máquinas y no su nombre NETBIOS.
> * No configurar Puerta de Enlace TS.
> * No usar certificados.

* Probar la aplicación desde el cliente.
* (Opcional) Añadir restricciones temporales en el uso de alguna aplicación remota.
* Comprobar el funcionamiento.

> Enlaces de interés:
> * [RemoteApp guía paso a paso] (https://technet.microsoft.com/es-ES/library/cc730673.aspx)
> * [Technet Microsoft RemoteApp] (https://technet.microsoft.com/en-us/library/cc753844%28WS.10%29.aspx)

