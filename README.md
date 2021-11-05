# vmware-vSphere-Configuracion :computer: :globe_with_meridians:

*VMware vSphere®* es una plataforma de solicitud racional y optimizada para *VMware®*. con esta plataforma, puede crear su propio entorno de *VMware* alojado por *IBM®* personalizando y solicitando el hardware compatible con *VMware* en función de los componentes de VMware seleccionado.

## Tabla de contenido 📑
1. [Requisitos](#Requisitos-newspaper)
2. [Configuración de conexión a VPN con SSL desde clientes de MotionPro](#configuración-de-conexión-a-vpn-con-ssl-desde-clientes-de-motionpro)
3. [Creación y gestión de clave API para infraestructura clásica](#creación-y-gestión-de-la-clave-api-para-infraestructura-clásica-key)
4. [Despliegue de Baremetal con VMware Solutions vCenter server](#despliegue-de-baremetal-con-vmware-solutions-VCenter-server)
    * [Opción 1: VCenter appliance](#opción-1-vcenter-appliance) 
    * [Opción 2: Virtual server](#opción-2-virtual-server) 
6. [Referencias](#referencias-)
7. [Autores](#autores-black_nib)

## Requisitos: newspaper:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>
* Contar con una cuenta de infraestructura en <a href="https://cloud.ibm.com/"> IBM Cloud</a>



## Configuración de conexión a VPN con SSL desde clientes de MotionPro.
Antes de iniciar con la descarga y configuración del software MotionPro es necesario habilitar el acceso VPN con SSL en su cuenta de *IBM Cloud*, para esto tenga en cuenta los siguientes pasos:
1. Desde la consola de *IBM Cloud* vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana y aquí de click sobre el botón ```Usuarios/Users```.
2. Seleccione el nombre del usuario al cual desea asignarle acceso VPN con SSL.
3. En la pagina principal del usuario de click sobre el botón ```Infraestructura clásica/Classic infrastructure``` y luego de click sobre ```Subredes VPN/VPN subnets```.
4. seleccione el campo de ```Habilitar acceso VPN con SSL/Enable SSL VPN Access``` y de click en el botón ```Guardar```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Enable.png>
</p>


Luego de haber habilitado el acceso VPN con SSL en su cuenta debe actualizar la contraseña de VPN de infraestructura clásica para poder establecer la conexión mas adelante, para esto tenga en cuenta los siguientes pasos:
1. Desde la consola de *IBM Cloud* vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana y aquí de click sobre el botón ```Usuarios/Users```.
2. Seleccione el nombre del usuario al cual le quiere modificar la contraseña.
3. En la pestaña de detalles de usuario vaya a la sección ```Contraseña de VPN```y de click sobre el botón ```Editar``` para ingresar la nueva contraseña, luego de esto de click sobre el botón ```Aplicar```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Password.png>
</p>

Una vez terminados estos dos procesos puede continuar con la instalación y configuración de MotionPro, para esto tenga en cuenta los siguientes pasos:
1. Descargue la versión de MotionPro adecuada para su sistema operativo en el siguiente <a href="https://support.arraynetworks.net/prx/001/http/supportportal.arraynetworks.net/downloads/downloads.html"> Link</a>.
2. Ejecute MotionProSetup para instalar el software.
3. Ejecute el asistente de configuración de MotionPro.
4. A continuación, pulse en el icono de MotionPro del escritorio y seleccione ```Perfil > Añadir```.
5. Para crear un perfil llene la siguiente información:
     * Nombre: Nombre distintivo del perfil
     * Host: Selección entre los <a href="https://cloud.ibm.com/docs/iaas-vpn?topic=iaas-vpn-available-vpn-endpoints"> puntos finales de VPN</a> disponibles en *IBM Cloud*
     * Nombre de usuario: utilice el nombre de usuario que se encuentra en la pestaña de detalles de usuario en la sección ```Contraseña de VPN```
     * Contraseña: ingrese la contraseña generada anteriormente. 
6. Luego de esto de click sobre el botón guardar.
7. Para efectuar la conexion de dobre click sobre el perfil generado.
<p align="center">
<img width="800" alt="img8" src=Imagenes/MotionPro.png>
</p>

## Creación y gestión de la clave API para infraestructura clásica :key:

Antes de iniciar el despliegue de la plataforma *VMware vSphere* es necesario crear una clave API para infraestructura clásica, para esto tenga en cuenta los siguientes pasos:

1. En la consola de IBM Cloud, vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana y aquí de click sobre el botón ```Claves API/API keys```.
2. Esto lo llevara a la ventana de claves API, aqui cambie la vista a claves API de la infraestructura clásica y de click sobre el botón ```Crear una clave de infraestructura clásica/Create classic infrastructure key```.
3. Luego de esto copie y descargue la clave de API en un lugar seguro para poder utilizarla mas adelante.

<p align="center">
<img width="800" alt="img8" src=Imagenes/API.png>
</p>

## Despliegue de Baremetal con VMware Solutions vCenter server

### Opción 1: VCenter appliance


#### Requisitos previos


Antes de iniciar con la primera opcion para el proceso de despliegue del vCenter server es necesario crear el Host de vSphere con recursos suficientes para dar soporte al VMware vCenter server Appliance, para esto tenga en cuenta los siguientes pasos:

1. Desde la consola de *IBM Cloud* diríjase al catalogo de productos, una vez aquí busque  ```VMware solutions```.
2. En esta nueva ventana de click sobre ```VMware Solutions Dedicated```, esto lo llevara a la ventana de configuración del servicio de VMware Solutions Dedicated, aquí debe ingresar la siguiente información:
   * ```Before you begin```: Tenga en cuenta la información especificada en esta sección, aquí debe ingresar el nombre de usuario y la clave API obtenidos en el numeral <a href="https://github.com/emeloibmco/vmware-vSphere-Configuracion/blob/main/README.md#creación-y-gestión-de-la-clave-api-para-infraestructura-clásica-key"> 3</a> de este repositorio. 
         <p align="center">
      <img width="800" alt="img8" src=Imagenes/Before.png>
      </p>

   * ```Solutions types```: Seleccione VMare vSphere, luego de esto confirme que la casilla ```Create new``` esta marcada
   * ```Cluster configurations```: (New cluster).
   * *Licensing:*
      * ```Cluster name```: Ingrese un nombre distintivo para el cluster.
      * ```Licensing```: Seleccione la versión de la licencia que desee, tenga en cuenta que esta no puede ser superior a la version mas reciente de la <a href="https://github.com/emeloibmco/vmware-vSphere-Configuracion/blob/main/README.md#despliegue-y-configuración-de-vcenter-server-appliance"> imagen</a> ISO del vCSA en este caso se selecciona **vSphere 6.7u3** dado que la ultima version disponible de la imagen es **VMware-VCSA-all-6.7.0-16046470.iso**, luego de esto seleccione las casillas de ```Include license with purchase```y```VMware vCenter Server > Include license with purchase```.
   * *Bare metal server:*
      * ```Location```: Seleccione la ubicación en la cual quiere que se despliegue el servicio, en este caso se utilizo Dallas 12.
      * ```CPU generation```: Seleccione la casilla ```Cascade Lake```.
      * ```CPU model```: Seleccione la configuración que desee.
      * ```RAM```: Seleccione la cantidad de memoria necesaria.
      * ```Number of bare metal server```: Seleccione la cantidad de servidores bare metal que desee desplegar.
   * *Network interface:*
      * ```Hostname prefix```: Ingrese un prefijo distintivo para el hostname.
      * ```Domain name```: Ingrese un nombre distintivo para el dominio, para instancias de vSphere 6.7, el nombre de dominio debe constar de tres o más series separadas por un punto (.) con un máximo de 50 caracteres. 
      * ```Navigation type```: Seleccione ```Public and private network```.
      * ```Uplink speed```: Seleccione ```10Gb```.
      * ```VLANs```: Seleccione ```Order new VLANs```.
   * Luego de esto de click en el botón ```Create```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Host.gif>
</p>




Adicionalmente, Para esta primera opción es necesario desplegar una VSI Windows de infraestructura clásica, para hacer esto tenga en cuenta los siguientes pasos:
1.  Desde la consola de *IBM Cloud* diríjase al catalogo de productos, una vez aquí busque ```Virtual Server for Classic```.
2.  Esto lo llevara a una ventana de configuración, aquí ingrese la siguiente información:
   * ```Type of virtual server```: seleccione ```Public```.
   * ```Hostname```: Ingrese un nombre distintivo.
   * ```Quantity```: seleccione 1
   * ```Biling method```: En este caso puede seleccionar cualquiera de las dos opciones dependiendo de sus preferencias.
   * ```Location```: Seleccione la ubicación en la cual desee desplegar la VSI, en este caso se utilizo Dallas 12.
   * ```Profile```: Seleccione la configuración de perfil que desee, en este caso se utilizo ```B1.4x16```.
   * *Operating system:*
      * ```Vendor```: seleccione ```Microsoft```.
      * ```Version```: Seleccione la versión que desee en este caso se utilizo ```2016 Standard 864bit9 - HVM``` .
      *  ```Attached storage disks```: De click en el botón ```Add new``` y seleccione un disco adicional de 100GB.
   *  *Network interface*
      *  ```Uplink port speeds```: Seleccione ```1 Gbps non rate-limited private network uplinks```.
      *  ```Private VLAN```: Seleccione la misma VLAN en la que esta ubicado el Host. Para ver esta información diríjase a la lista de recursos y en la pestaña de ```Devices```encontrara el Host creado anteriormente de click sobre el nombre, esto lo llevara a la pestaña de ```overview```, en esta pestaña en la sección de ```Network details``` encontrara las VLANs asociadas a cada interfaz.
   *  Luego de completar esta información de click sobre el botón ```Crear```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/VSI1.gif>
</p>

Luego de esto es necesario crear una subred portable sobre la VLAN privada del Host la cual usaremos después, para esto tenga en cuenta los siguientes pasos:
1. Desde la lista de recursos en la sección ```Devices```ingrese al servidor de vShpere, una vez aquí diríjase a la sección ```Network details```y de click sobre la IP privada del servidor, esto le permitirá ver todas las subredes disponibles
2. de click sobre ```All subnets```, esto lo llevara a una nueva ventana, aquí de click sobre ```Create subnet```.
3. En la pestaña de configuración ingrese la siguiente información:
   * ```Scope```: Seleccione la misma ubicación en la que se desplego el Host, en este caso es Dallas 12.
   * ```Network```: Seleccione ```Private```.
   * ```Version```: Seleccione ```Ipv4```.
   * ```Size```: Seleccion ```/29```.
   * ```Routing```: Seleccione ```Portable```.
   * ```Select VLAN```: Seleccione la VLAN privada del Host.
   * De click en el botón ```Create```.
   * Una vez creada guarde la IP de la subred para usarla mas adelante

<p align="center">
<img width="800" alt="img8" src=Imagenes/SN.gif>
</p>

#### Despliegue y configuración de vCenter Server Appliance

Una vez desplegada la VSI Windows de infraestructura clásica se debe descargar la imagen ISO de vCenter Server Appliance. Para esto primero ejecute la conexión en MotionPro con el perfil de la ubicación en la cual se encuentran tanto el Host como la VSI desplegados (en este caso es Dallas 12), luego de esto ingrese mediante ```Remote Desktop``` a la VSI desplegada anteriormente con la IP (la cual la encuentra en la pestaña de overview) y el usuario y contraseña (Los cuales encuentra en la pestaña de Passwords) una vez aquí ingrese al siguiente link mediante cualquier navegador para descargar la imagen ISO del vCSA, este proceso se realiza en la VSI para ahorrar tiempo y mejorar su eficiencia.
```
http://downloads.service.softlayer.com/vmware/
```
Una vez aquí busque el link de descarga con el nombre ```VMware-VCSA-all-6.7.0-16046470.iso```y de click sobre este para iniciar el proceso de descarga. Luego de descargar el software tenga en cuenta los siguientes pasos para desplegarlo sobre la VSI:

1. Monte la ISO de vCenter Server Appliance (vCSA).
2. diríjase a la carpeta ```vcsa-ui-installer > win32``` y ejecute el installer.exe.
3. Esto abrirá una la ventana del instalador, aquí de click sobre el botón ```Install``` y tenga en cuenta los siguientes pasos para la instalación. 
   * **STAGE 1**
   * ```Introduction```: Lea la información y de click en ```Next```.
   * ```End user license agreement```: Lea y acepte los términos y condiciones y de click en ```next```.
   * ```Select deployment type```: seleccione ```Embedded Platform Services Controller``` para desplegar el vCenter junto con el Platform Services Controller en la misma maquina.
   * ```Appliance deployment target```:
      * ```ESXi host or vCenter Server name```: ingrese la IP privada del Host creado anteriormente (esta la encuentra en la pestaña overview del servidor de vSphere).
      * ```User name```: ingrese el usuario root del Host.
      * ```Password```: ingrese la contraseña del usuario root del Host (esta la puede encontrar en la pestaña passwords del servidor de vSphere).
      * De click en ```Next``` y acepte la advertencia de certificado.
   * ```Set up appliance VM```:
      * ```VM name```: Ingrese un nombre distintivo para la maquina.
      * ```Set root password```: Ingrese la contraseña de root que desee teniendo en cuenta las especificaciones requeridas.
      * ```Confirm root password```: confirme la contraseña ingresada anteriormente.
      * De click en ```Next```.
   * ```Select deployment size```:
      * ```Deployment size```: Ingrese el tamaño deseado dependiendo de su aplicación, en este caso se utilizo ```Small```.
      * ```Storage size```: Ingrese el tamaño de almacenamiento dependiendo de su aplicación, en este caso se dejo ```Default```.
      * De click en ```Next```.
   * ```Select datastore```: Seleccione la opción ```install on an existing datastore accesible from the target host``` y de click en ```Next```.
   * ```Configure network settings```:
      * ```Network```: Ingrese el nombre asignado a la subred portable creada anteriormente.
      * ```IP version```: Ingrese la versión que asigno al momento de crear la subred, en este caso es ```IPv4```
      * ```IP assignment```: Static.
      * ```IP address```: Ingrese la IP que desee asignar.
      * ```Subnet mask or prefix lenght```: Ingrese el prefijo para determinar el tamaño de la subnet.
      * De click en el boton ```Next```.
   * ```Ready to complete stage 1```: espere a que se termine el primer stage de la instalación.


### Opción 2: Virtual server instance









# Referencias 📖

* [Gestión de claves de API de la infraestructura clásica](https://cloud.ibm.com/docs/account?topic=account-classic_keys#create-classic-infrastructure-key).
* [Iniciación a VMware Solutions](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-getting-started).

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />

     
