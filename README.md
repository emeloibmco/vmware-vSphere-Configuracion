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

Antes de iniciar con las dos opciones para el proceso de despliegue del vCenter server es necesario crear el Host de vSphere con recursos suficientes para dar soporte al VMware vCenter server Appliance, para esto tenga en cuenta los siguientes pasos:

1. Desde la consola de *IBM Cloud* diríjase al catalogo de productos, una vez aquí busque  ```VMware solutions```.
2. Esto lo llevara a una nueva ventana, aquí de click sobre ```VMware Solutions Dedicated```, esto lo llevara a la ventana de configuración del servicio de VMware Solutions Dedicated, aquí debe ingresar la siguiente información:
   * ```Before you begin```: Tenga en cuenta la información especificada en esta sección, aquí debe ingresar el nombre de usuario y la clave API obtenidos en el numeral <a href="https://github.com/emeloibmco/vmware-vSphere-Configuracion/blob/main/README.md#creación-y-gestión-de-la-clave-api-para-infraestructura-clásica-key"> 3</a> de este repositorio. 
         <p align="center">
      <img width="800" alt="img8" src=Imagenes/Before.png>
      </p>

   * ```Solutions types```: Seleccione VMare vSphere, luego de esto confirme que la casilla ```Create new``` esta marcada
   * ```Cluster configurations```: (New cluster).
   * *Licensing:*
      * ```Cluster name```: Ingrese un nombre distintivo para el cluster.
      * ```Licensing```: Seleccione la ultima versión disponible de la licencia, en este caso *vSphere 7.0u2* y seleccione las casillas de ```Include license with purchase```y```VMware vCenter Server > Include license with purchase```.
   * *Bare metal server:*
      * ```Location```: Seleccione la ubicación en la cual quiere que se despliegue el servicio.
      * ```CPU generation```: Seleccione la casilla ```Cascade Lake```.
      * ```CPU model```: Seleccione la configuración que desee.
      * ```RAM```: Seleccione la cantidad de memoria necesaria.
      * ```Number of bare metal server```: Seleccione la cantidad de servidores bare metal que desee desplegar.
   * *Network interface:*
      * ```Hostname prefix```: Ingrese un prefijo distintivo para el hostname.
      * ```Domain name```: Ingrese un nombre distintivo para el dominio, para instancias de vSphere 7.0, el nombre de dominio debe constar de tres o más series separadas por un punto (.) con un máximo de 50 caracteres.
      * ```Navigation type```: Seleccione ```Public and private network```.
      * ```Uplink speed```: Seleccione ```10Gb```.
      * ```VLANs```: Seleccione ```Order new VLANs```.
   * Luego de esto de click en el botón ```Create```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Host.gif>
</p>

Luego de tener desplegado el Host de vSphere con recursos suficientes se puede pasar al despliegue vCenter. Este se puede realizar mediante dos opciones, la primera es desplegando y configurando una imagen ISO de vCenter Server Appliance en una VSI de infraestructura clásica de Windows y la segunda opción es desplegar el software de vCenter al momento de crear y configurar la VSI de infraestructura clásica de Windows en la misma VLAN de Host. Ambas opciones se explicarán a continuación.

### Opción 1: VCenter appliance
Para esta primera opción es necesario desplegar una VSI Windows de infraestructura clásica, para hacer esto tenga en cuenta los siguientes pasos:
1.  Desde la consola de *IBM Cloud* diríjase al catalogo de productos, una vez aquí busque ```Virtual Server for Classic```.
2.  Esto lo llevara a una ventana de configuración, aquí ingrese la siguiente información:
   * ```Type of virtual server```: seleccione ```Public```.
   * ```Hostname```: Ingrese un nombre distintivo.
   * ```Quantity```: seleccione 1
   * ```Biling method```: En este caso puede seleccionar cualquiera de las dos opciones dependiendo de sus preferencias.
   * ```Location```: Seleccione la ubicación en la cual desee desplegar la VSI.
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


### Opción 2: Virtual server instance









# Referencias 📖

* [Gestión de claves de API de la infraestructura clásica](https://cloud.ibm.com/docs/account?topic=account-classic_keys#create-classic-infrastructure-key).
* [Iniciación a VMware Solutions](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-getting-started).

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />

     
