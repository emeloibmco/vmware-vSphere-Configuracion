# vmware-vSphere-Configuracion :computer: :globe_with_meridians:

*VMware vSphere庐* es una plataforma de solicitud racional y optimizada para *VMware庐*. con esta plataforma, puede crear su propio entorno de *VMware* alojado por *IBM庐* personalizando y solicitando el hardware compatible con *VMware* en funci贸n de los componentes de VMware seleccionado.

## Tabla de contenido 馃搼
1. [Requisitos](#Requisitos-newspaper)
2. [Configuraci贸n de conexi贸n a VPN con SSL desde clientes de MotionPro](#configuraci贸n-de-conexi贸n-a-vpn-con-ssl-desde-clientes-de-motionpro)
3. [Creaci贸n y gesti贸n de clave API para infraestructura cl谩sica](#creaci贸n-y-gesti贸n-de-la-clave-api-para-infraestructura-cl谩sica-key)
4. [Despliegue de Baremetal con VMware Solutions vCenter server](#despliegue-de-baremetal-con-vmware-solutions-VCenter-server)
    * [Opci贸n 1: VCenter appliance](#opci贸n-1-vcenter-appliance) 
    * [Opci贸n 2: Virtual server](#opci贸n-2-virtual-server) 
5. [Configuraci贸n vCenter Server](#configuraci贸n-vcenter-server)
6. [Referencias](#referencias-)
7. [Autores](#autores-black_nib)

## Requisitos: newspaper:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>
* Contar con una cuenta de infraestructura en <a href="https://cloud.ibm.com/"> IBM Cloud</a>



## Configuraci贸n de conexi贸n a VPN con SSL desde clientes de MotionPro.
Antes de iniciar con la descarga y configuraci贸n del software MotionPro es necesario habilitar el acceso VPN con SSL en su cuenta de *IBM Cloud*, para esto tenga en cuenta los siguientes pasos:
1. Desde la consola de *IBM Cloud* vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana, all铆 de click sobre el bot贸n ```Usuarios/Users```.
2. Seleccione el nombre del usuario al cual desea asignarle acceso VPN con SSL.
3. En la pagina principal del usuario de click sobre el bot贸n ```Infraestructura cl谩sica/Classic infrastructure``` y luego de click sobre ```Subredes VPN/VPN subnets```.
4. seleccione el campo de ```Habilitar acceso VPN con SSL/Enable SSL VPN Access``` y de click en el bot贸n ```Guardar```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Enable.png>
</p>


Luego de haber habilitado el acceso VPN con SSL en su cuenta debe actualizar la contrase帽a de VPN de infraestructura cl谩sica para poder establecer la conexi贸n mas adelante, para esto tenga en cuenta los siguientes pasos:
1. Desde la consola de *IBM Cloud* vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana y aqu铆 de click sobre el bot贸n ```Usuarios/Users```.
2. Seleccione el nombre del usuario al cual le quiere modificar la contrase帽a.
3. En la pesta帽a de detalles de usuario vaya a la secci贸n ```Contrase帽a de VPN```y de click sobre el bot贸n ```Editar``` para ingresar la nueva contrase帽a, luego de esto de click sobre el bot贸n ```Aplicar```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Password.png>
</p>

Una vez terminados estos dos procesos puede continuar con la instalaci贸n y configuraci贸n de MotionPro, para esto tenga en cuenta los siguientes pasos:
1. Descargue la versi贸n de MotionPro adecuada para su sistema operativo en el siguiente <a href="https://support.arraynetworks.net/prx/001/http/supportportal.arraynetworks.net/downloads/downloads.html"> Link</a>.
2. Ejecute MotionProSetup para instalar el software.
3. Ejecute el asistente de configuraci贸n de MotionPro.
4. A continuaci贸n, pulse en el icono de MotionPro del escritorio y seleccione ```Perfil > A帽adir```.
5. Para crear un perfil llene la siguiente informaci贸n:
     * Nombre: Nombre distintivo del perfil
     * Host: Selecci贸n entre los <a href="https://cloud.ibm.com/docs/iaas-vpn?topic=iaas-vpn-available-vpn-endpoints"> puntos finales de VPN</a> disponibles en *IBM Cloud*
     * Nombre de usuario: utilice el nombre de usuario que se encuentra en la pesta帽a de detalles de usuario en la secci贸n ```Contrase帽a de VPN```
     * Contrase帽a: ingrese la contrase帽a generada anteriormente. 
6. Luego de esto de click sobre el bot贸n guardar.
7. Para efectuar la conexion de dobre click sobre el perfil generado.
<p align="center">
<img width="800" alt="img8" src=Imagenes/MotionPro.png>
</p>

## Creaci贸n y gesti贸n de la clave API para infraestructura cl谩sica :key:

Antes de iniciar el despliegue de la plataforma *VMware vSphere* es necesario crear una clave API para infraestructura cl谩sica, para esto tenga en cuenta los siguientes pasos:

1. En la consola de IBM Cloud, vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana y aqu铆 de click sobre el bot贸n ```Claves API/API keys```.
2. Esto lo llevara a la ventana de claves API, aqu铆 cambie la vista a claves API de la infraestructura cl谩sica y de click sobre el bot贸n ```Crear una clave de infraestructura cl谩sica/Create classic infrastructure key```.
3. Luego de esto copie y descargue la clave de API en un lugar seguro para poder utilizarla mas adelante.

<p align="center">
<img width="800" alt="img8" src=Imagenes/API.png>
</p>

## Despliegue de Baremetal con VMware Solutions vSphere

Antes de iniciar con el despliegue vCenter Server Appliance mediante cualquiera de las dos opciones es necesario crear el Host de vSphere con recursos suficientes para dar soporte al VMware vCenter server Appliance, para esto tenga en cuenta los siguientes pasos:

1. Desde la consola de *IBM Cloud* dir铆jase al catalogo de productos, una vez aqu铆 busque  ```VMware solutions```.
2. En esta nueva ventana de click sobre ```VMware Solutions Dedicated```, esto lo llevara a la ventana de configuraci贸n del servicio de VMware Solutions Dedicated, aqu铆 debe ingresar la siguiente informaci贸n:
   * ```Before you begin```: Tenga en cuenta la informaci贸n especificada en esta secci贸n, aqu铆 debe ingresar el nombre de usuario y la clave API obtenidos en el numeral <a href="https://github.com/emeloibmco/vmware-vSphere-Configuracion/blob/main/README.md#creaci贸n-y-gesti贸n-de-la-clave-api-para-infraestructura-cl谩sica-key"> 3</a> de este repositorio. 
         <p align="center">
      <img width="800" alt="img8" src=Imagenes/Before.png>
      </p>

   * ```Solutions types```: Seleccione VMare vSphere, luego de esto confirme que la casilla ```Create new``` esta marcada
   * ```Cluster configurations```: (New cluster).
   * *Licensing:*
      * ```Cluster name```: Ingrese un nombre distintivo para el cluster.
      * ```Licensing```: Seleccione la versi贸n de la licencia que desee, tenga en cuenta que esta no puede ser superior a la version mas reciente de la <a href="https://github.com/emeloibmco/vmware-vSphere-Configuracion/blob/main/README.md#despliegue-y-configuraci贸n-de-vcenter-server-appliance"> imagen</a> ISO del vCSA en este caso se selecciona **vSphere 6.7u3** dado que la ultima version disponible de la imagen es **VMware-VCSA-all-6.7.0-16046470.iso**, luego de esto seleccione las casillas de ```Include license with purchase```y```VMware vCenter Server > Include license with purchase```.
   * *Bare metal server:*
      * ```Location```: Seleccione la ubicaci贸n en la cual quiere que se despliegue el servicio, en este caso se utilizo Dallas 12.
      * ```CPU generation```: Seleccione la casilla ```Cascade Lake```.
      * ```CPU model```: Seleccione la configuraci贸n que desee.
      * ```RAM```: Seleccione la cantidad de memoria necesaria.
      * ```Number of bare metal server```: Seleccione la cantidad de servidores bare metal que desee desplegar.
   * *Network interface:*
      * ```Hostname prefix```: Ingrese un prefijo distintivo para el hostname.
      * ```Domain name```: Ingrese un nombre distintivo para el dominio, para instancias de vSphere 6.7, el nombre de dominio debe constar de tres o m谩s series separadas por un punto (.) con un m谩ximo de 50 caracteres. 
      * ```Navigation type```: Seleccione ```Public and private network```.
      * ```Uplink speed```: Seleccione ```10Gb```.
      * ```VLANs```: Seleccione ```Order new VLANs```.
   * Luego de esto de click en el bot贸n ```Create```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Host.gif>
</p>

Luego de tener desplegado el Host de vSphere con recursos suficientes se puede pasar al despliegue vCenter. Este se puede realizar mediante dos opciones, la primera es desplegando y configurando una imagen ISO de vCenter Server Appliance en una VSI de infraestructura cl谩sica de Windows y la segunda opci贸n es desplegar el software de vCenter al momento de crear y configurar la VSI de infraestructura cl谩sica de Windows en la misma VLAN de Host. Ambas opciones se explicar谩n a continuaci贸n.

### Opci贸n 1: VCenter appliance

#### Requisitos previos

Para esta primera opci贸n es necesario desplegar una VSI Windows de infraestructura cl谩sica, para hacer esto tenga en cuenta los siguientes pasos:
1.  Desde la consola de *IBM Cloud* dir铆jase al catalogo de productos, una vez aqu铆 busque ```Virtual Server for Classic```.
2.  Esto lo llevara a una ventana de configuraci贸n, aqu铆 ingrese la siguiente informaci贸n:
   * ```Type of virtual server```: seleccione ```Public```.
   * ```Hostname```: Ingrese un nombre distintivo.
   * ```Quantity```: seleccione 1
   * ```Biling method```: En este caso puede seleccionar cualquiera de las dos opciones dependiendo de sus preferencias.
   * ```Location```: Seleccione la ubicaci贸n en la cual desee desplegar la VSI, en este caso se utilizo Dallas 12.
   * ```Profile```: Seleccione la configuraci贸n de perfil que desee, en este caso se utilizo ```B1.4x16```.
   * *Operating system:*
      * ```Vendor```: seleccione ```Microsoft```.
      * ```Version```: Seleccione la versi贸n que desee en este caso se utilizo ```2016 Standard 864bit9 - HVM``` .
   *  ```Attached storage disks```: De click en el bot贸n ```Add new``` y seleccione un disco adicional de 100GB.
   *  *Network interface*
      *  ```Uplink port speeds```: Seleccione ```1 Gbps non rate-limited private network uplinks```.
      *  ```Private VLAN```: Seleccione la misma VLAN en la que esta ubicado el Host. Para ver esta informaci贸n dir铆jase a la lista de recursos y en la pesta帽a de ```Devices```encontrara el Host creado anteriormente de click sobre el nombre, esto lo llevara a la pesta帽a de ```overview```, en esta pesta帽a en la secci贸n de ```Network details``` encontrara las VLANs asociadas a cada interfaz.
   *  Luego de completar esta informaci贸n de click sobre el bot贸n ```Crear```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/VSI1.gif>
</p>

Luego de esto es necesario crear una subred portable sobre la VLAN privada del Host la cual usaremos despu茅s, para esto tenga en cuenta los siguientes pasos:
1. Desde la lista de recursos en la secci贸n ```Devices```ingrese al servidor de vShpere, una vez aqu铆 dir铆jase a la secci贸n ```Network details```y de click sobre la IP privada del servidor, esto le permitir谩 ver todas las subredes disponibles
2. de click sobre ```All subnets```, esto lo llevara a una nueva ventana, aqu铆 de click sobre ```Create subnet```.
3. En la pesta帽a de configuraci贸n ingrese la siguiente informaci贸n:
   * ```Scope```: Seleccione la misma ubicaci贸n en la que se desplego el Host, en este caso es Dallas 12.
   * ```Network```: Seleccione ```Private```.
   * ```Version```: Seleccione ```Ipv4```.
   * ```Size```: Seleccion ```/29```.
   * ```Routing```: Seleccione ```Portable```.
   * ```Select VLAN```: Seleccione la VLAN privada del Host.
   * De click en el bot贸n ```Create```.
   * Una vez creada guarde la IP de la subred para usarla mas adelante

<p align="center">
<img width="800" alt="img8" src=Imagenes/SN.gif>
</p>

#### Despliegue y configuraci贸n de vCenter Server Appliance

Una vez desplegada la VSI Windows de infraestructura cl谩sica se debe descargar la imagen ISO de vCenter Server Appliance. Para esto primero ejecute la conexi贸n en MotionPro con el perfil de la ubicaci贸n en la cual se encuentran tanto el Host como la VSI desplegados (en este caso es Dallas 12), luego de esto ingrese mediante ```Remote Desktop``` a la VSI desplegada anteriormente con la IP (la cual la encuentra en la pesta帽a de overview), el usuario y contrase帽a (Los cuales encuentra en la pesta帽a de Passwords) una vez aqu铆 ingrese al siguiente link mediante cualquier navegador para descargar la imagen ISO del vCSA, este proceso se realiza en la VSI para ahorrar tiempo y mejorar su eficiencia.
```
http://downloads.service.softlayer.com/vmware/
```
Una vez aqu铆 busque el link de descarga con el nombre ```VMware-VCSA-all-6.7.0-16046470.iso```y de click sobre este para iniciar el proceso de descarga. Luego de descargar el software tenga en cuenta los siguientes pasos para desplegarlo sobre la VSI:

1. Monte la ISO de vCenter Server Appliance (vCSA).
2. dir铆jase a la carpeta ```vcsa-ui-installer > win32``` y ejecute el installer.exe.
3. Esto abrir谩 una la ventana del instalador, aqu铆 de click sobre el bot贸n ```Install``` y tenga en cuenta los siguientes pasos para la instalaci贸n. 
   * **STAGE 1**
   * ```Introduction```: Lea la informaci贸n y de click en ```Next```.
   * ```End user license agreement```: Lea y acepte los t茅rminos y condiciones y de click en ```next```.
   * ```Select deployment type```: seleccione ```Embedded Platform Services Controller``` para desplegar el vCenter junto con el Platform Services Controller en la misma maquina.
   * ```Appliance deployment target```:
      * ```ESXi host or vCenter Server name```: ingrese la IP privada del Host creado anteriormente (esta la encuentra en la pesta帽a overview del servidor de vSphere).
      * ```User name```: ingrese el usuario root del Host.
      * ```Password```: ingrese la contrase帽a del usuario root del Host (esta la puede encontrar en la pesta帽a passwords del servidor de vSphere).
      * De click en ```Next``` y acepte la advertencia de certificado.
   * ```Set up appliance VM```:
      * ```VM name```: Ingrese un nombre distintivo para la maquina.
      * ```Set root password```: Ingrese la contrase帽a de root que desee teniendo en cuenta las especificaciones requeridas.
      * ```Confirm root password```: confirme la contrase帽a ingresada anteriormente.
      * De click en ```Next```.
   * ```Select deployment size```:
      * ```Deployment size```: Ingrese el tama帽o deseado dependiendo de su aplicaci贸n, en este caso se utilizo ```Small```.
      * ```Storage size```: Ingrese el tama帽o de almacenamiento dependiendo de su aplicaci贸n, en este caso se dejo ```Default```.
      * De click en ```Next```.
   * ```Select datastore```: Seleccione la opci贸n ```install on an existing datastore accesible from the target host``` y de click en ```Next```.
   * ```Configure network settings```:
      * ```Network```: Ingrese el nombre asignado a la subred portable creada anteriormente.
      * ```IP version```: Ingrese la versi贸n que asigno al momento de crear la subred, en este caso es ```IPv4```
      * ```IP assignment```: Static.
      * ```IP address```: Ingrese la IP que desee asignar.
      * ```Subnet mask or prefix lenght```: Ingrese el prefijo para determinar el tama帽o de la subnet.
      * De click en el boton ```Next```.
   * ```Ready to complete stage 1```: espere a que se termine el primer stage de la instalaci贸n.
   
<p align="center">
<img width="800" alt="img8" src=Imagenes/ST1.gif>
</p>

   * **STAGE 2**
   * Luego de terminar la configuraci贸n del Stage 1 se abrir谩 de manera autom谩tica el Stage 2, en caso de que esto no suceda siga las instrucciones de la ventana emergente para acceder a la configuraci贸n del stage 2 como se muestra en la siguiente imagen.
   <p align="center">
<img width="800" alt="img8" src=Imagenes/Error.png>
</p>

   * Una vez se encuentre en la pesta帽a de configuraci贸n del stage 2 tenga en cuenta los siguientes pasos.
   * Ingrese el usuario y contrase帽a que le asigno al vCenter Server Appliance anteriormente
   * ```Introduction```: Lea la informaci贸n y de click en ```Next```.
   * ```Appliance configuration```: Lea la configuraci贸n y aseg煤rese que todos los datos est茅n correctos, luego de click en ```Next```.
   * ```SSO Configuration```
      * ```Single Sign-On domain name```: Ingrese un nombre distintivo para el dominio del SSO.
      * ```Single Sign-On password```: Ingrese una contrase帽a teniendo en cuenta las especificaciones requeridas.
      * De click en ```Next```.
   * ```Configure CEIP```: Lea la informaci贸n, si esta de acuerdo seleccione la casilla de ```Join the VMware's Customer Experience Improvement Program (CEIP)``` y de click en ```Next```.
   * ```Ready to Complete```: Verifique la informaci贸n y de click en ```Finish```.
   * Espere a que termine la instalaci贸n del segundo Stage.

<p align="center">
<img width="800" alt="img8" src=Imagenes/ST2.gif>
</p>


### Opci贸n 2: Virtual server instance

Para esta segunda opci贸n es necesario desplegar una VSI Windows de infraestructura cl谩sica en la misma VLAN del Host creado anteriormente para poder desplegar el software de vCenter en esta maquina virtual, para esto tenga en cuenta los siguientes pasos:

1.  Desde la consola de *IBM Cloud* dir铆jase al catalogo de productos, una vez aqu铆 busque ```Virtual Server for Classic```.
2.  Esto lo llevara a una ventana de configuraci贸n, aqu铆 ingrese la siguiente informaci贸n:
   * ```Type of virtual server```: seleccione ```Public```.
   * ```Hostname```: Ingrese un nombre distintivo.
   * ```Quantity```: seleccione 1
   * ```Biling method```: Seleccione ```Monthly```.
   * ```Location```: Seleccione la ubicaci贸n en la cual desee desplegar la VSI, en este caso se utilizo Dallas 12.
   * ```Profile```: Seleccione la configuraci贸n de perfil que desee, en este caso se utilizo ```B1.4x16```.
   * *Operating system:*
      * ```Vendor```: seleccione ```Microsoft```.
      * ```Version```: Seleccione  ```2016 Standard 864bit9 - HVM``` .
      * ```OS add-on```: Seleccione ```VMware``` > ```vCenter 6.7```.
   *  ```Attached storage disks```: De click en el bot贸n ```Add new``` y seleccione un disco adicional de 100GB.
   *  *Network interface*
      *  ```Uplink port speeds```: Seleccione ```1 Gbps non rate-limited private network uplinks```.
      *  ```Private VLAN```: Seleccione la misma VLAN en la que esta ubicado el Host. Para ver esta informaci贸n dir铆jase a la lista de recursos y en la pesta帽a de ```Devices```encontrara el Host creado anteriormente de click sobre el nombre, esto lo llevara a la pesta帽a de ```overview```, en esta pesta帽a en la secci贸n de ```Network details``` encontrara las VLANs asociadas a cada interfaz.
   *  Luego de completar esta informaci贸n de click sobre el bot贸n ```Crear```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/OP2.gif>
</p>

## Configuraci贸n vCenter Server

### Configuraci贸n inicial
Una vez desplegado el vCenter Server Appliance se puede pasar a la configuraci贸n de este, para hacer esto tenga en cuenta los siguientes pasos:

1. Ingrese a la pesta帽a de configuraci贸n del vCenter vSphere Client de la VSI creada anteriormente mediante cualquiera de las dos opciones propuestas, para esto tenga en cuenta los siguientes pasos:
   * Ejecute la conexi贸n en MotionPro con el perfil de la ubicaci贸n en la cual se encuentran tanto el Host como la VSI desplegados (en este caso es Dallas 12).
   * Desde la consola de *IBM Cloud* dir铆jase a la lista de recursos, una vez aqu铆 busque la VSI que desplego anteriormente y de click sobre esta.
   * Esto lo llevara a la pesta帽a de ```Overview```, aqu铆 copie la IP publica de la maquina y p茅guela en un buscador para acceder a una pesta帽a principal de VMware.
   * De click sobre el bot贸n ```LAUNCH VSPHERE CLIENT (HTML 5)```.
   * Esto lo llevara a la pesta帽a de inicio de VMware vCenter Single Sign-on (En caso de que ocurra un error edite el archivo de Hosts en su computador para que este reconozca la IP publica asociada al nombre de la instancia de la VSI)
   * Ingrese el usuario y la contrase帽a del vCenter, estos los encuentra en la pesta帽a ```Passwords```.

2. Cree un Datacenter, para esto tenga en cuenta los siguientes pasos:
   * De click izquierdo sobre el nombre de la VSI, esto abrir谩 un men煤 emergente, aqu铆 de click sobre ```New Datacenter```.
   * Ingrese un nombre distintivo para el Datacenter y de click en ```Next```.

3. Cree un CLuster, para esto tenga en cuenta los siguientes pasos:
   * De click izquierdo sobre el nombre del Datacenter creado anteriormente, luego de esto de click sobre ```New Cluster```.
   * Ingrese un nombre distintivo para el cluster y de click en ```OK```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Configuracion.gif>
</p>



4. Agregue un Host, para esto tenga en cuenta los siguientes pasos:
   * De click izquierdo sobre el nombre del Datacenter creado anteriormente, luego de esto de click sobre ```Add Host```.
   * **Name and Location**
      * ```Host name or IP adress```: Copie y pegue la IP privada del Host de vSphere creado anteriormente.
   * **Connection settings**
   * ```User name```: Ingrese el usuario root del Host de vSphere.
   * ```Password```: Ingrese la contrase帽a del usuario root del Host de vSphere.
   * **Host summary**: Lea la informacion y de click en ```Next```.
   * **Assign license**: Lea la informacion y de click en ```Next```.
   * **Lockdown mode**: Lea la informacion, seleccionde ```Disabled``` y de click en ```Next```.
   * **Ready to complete**: Lea la informacion y de click en ```Finish```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/addHost.gif>
</p>


### Configuraci贸n seg煤n los requerimientos

#### Creaci贸n de un switch virtual est谩ndar adicional

Antes de crear el switch adicional es necesario revisar que adaptadores est谩n conectados al switch existente, en este caso al switch vSwitch0, para hacer esto tenga en cuenta los siguientes pasos:

1. De click sobre el Host desplegado anteriormente, luego de esto de click sobre el bot贸n ```Configure```.
2. De click sobre el bot贸n ```Physical adapters``` en el grupo ```Networking```.
3. Esto desplegara una nueva ventana en donde se pueden ver los adaptadores f铆sicos, su configuraci贸n y a que switch est谩n conectados si es el caso.

<p align="center">
<img width="800" alt="img8" src=Imagenes/Rev.gif>
</p>

Luego de esto ya se puede pasar a crear el virtual switch adicional, en este caso se crear谩 un v-switch publico para conectar en este las interfaces 1 y 3 que son las encargadas del trafico publico en la maquina, para esto tenga en cuenta los siguientes pasos:

1. De click sobre el Host desplegado anteriormente, luego de esto de click sobre el bot贸n ```Configure```.
2. De click sobre el bot贸n ```Virtual switches``` en el grupo ```Networking```.
3. De click sobre el bot贸n ```Add Networking```.
4. Esto abrir谩 una ventana de configuraci贸n, aqu铆 ingrese la siguiente informaci贸n:
   * ```Select connection type```: Seleccione ```Virtual Machine Port Group for a Standard Switch```.
   * ```Select target device```: Seleccione ```New Standard switch```.
   * ```Create a Standard Switch```: de click en el bot贸n ```+``` para asignar los adaptadores deseados en el nuevo switch, luego de esto seleccione el adaptador vmnic1 y repita el proceso para el vmnic3. Si desea balancear cargas en los adaptadores utilice las flechas azules de la parte superior para asignar un adaptador a la categor铆a de ```Standby adapters```.
   * ```Connection settings```:
      * ```Network label```: Ingrese un nombre distintivo.
      * ```VLAN ID```: Seleccione ```None (0)``` para seleccionar la VLAN primaria.
   * ```Ready to Complete```: De click en ```Finish```.


<p align="center">
<img width="800" alt="img8" src=Imagenes/VSAd.gif>
</p>

Luego de crear el switch adicional puede editar el switch que estaba creado anteriormente para agregar la interfaz 2, para esto tenga en cuenta los siguientes pasos:

1. De click sobre el Host desplegado anteriormente, luego de esto de click sobre el bot贸n ```Configure```.
2. De click sobre el bot贸n ```Virtual switches``` en el grupo ```Networking```.
3. De click sobre el nombre el virtual switch que desea editar, en este caso es el vSwitch0, luego de esto de click sobre el bot贸n ```Manage physical Adapters```.
4. Esto abrir谩 una nueva pesta帽a de configuraci贸n, aqu铆 de click sobre el bot贸n ```+```para asignar un nuevo adaptador al switch, aqu铆 de click sobre la instancia vmnic2 y ub铆quela en la regi贸n de ```Standby adapters```para generar el balanceo de cargas.

<p align="center">
<img width="800" alt="img8" src=Imagenes/VS2.gif>
</p>


#### Adicionar un vKernel a un vSwitch para conectarse al Host mediante la IP publica sin necesidad de utilizar VPNs 

para esto tenga en cuenta los siguientes pasos:
1. De click sobre el Host desplegado anteriormente, luego de esto de click sobre el bot贸n ```Configure```.
2. De click sobre el bot贸n ```Virtual switches``` en el grupo ```Networking```.
3. De click sobre el nombre del vSwitch al cual desea adicionarle un vKernel, en este caso es el vSwitch1, luego de esto de click sobre el bot贸n ```Add Networking```.
4. Esto abrir谩 una ventana de configuraci贸n, aqu铆 ingrese la siguiente informaci贸n:
   * ```Select connection type```: Seleccione ```VMKernel Network Adapter```.
   * ```Select target device```: Seleccione ```Select an existing standard switch```.
   * ```Port properties```:
      * ```Network label```: Ingrese un nombre distintivo.
      * ```VLAN ID```: Seleccione ```None (0)``` para seleccionar la VLAN primaria.
      * ```IP settings```: Seleccione ```IPv4```.
      * ```Enabled services```: Seleccione ```Management```.
   * ```IPv4 settings```: Seleccione ```Use static IPv4 settings```, pegue la direcci贸n IP publica del Host de vSphere, ingrese una mascara de subnet y pegue la direcci贸n IP del gateway del Host.
   * ```Ready to Complete```: De click en ```Finish```.

<p align="center">
<img width="800" alt="img8" src=Imagenes/vKernel.gif>
</p>


#### Crear una imagen Ubuntu.vmdk
Antes de iniciar con la creaci贸n de la maquina virtual es necesario subir el archivo .vmdk al datastore que creamos anteriormente, para esto tenga en cuenta los siguientes pasos:
1. De click sobre la pesta帽a de ```Storage``` y despliegue los men煤s hasta encontrar el datastore creado anteriormente, de click sobre este.
2. una vez se encuentre en la pesta帽a de configuraci贸n del datastore, de click sobre ```Files```
3. Aqu铆 de click sobre el bot贸n de ```New folder``` e ingrese un nombre apropiado para la carpeta, en este caso puede ser ```Ubuntu VM```.
4. De click sobre la carpeta que acabo de crear y de click sobre el bot贸n ```Upload Files``` y seleccione el archivo .mkv que tiene descargado en su PC.

Luego de esto puede continuar con la creaci贸n de la maquina virtual, para esto tenga en cuenta los siguientes pasos:
1. De click sobre El Host que acabomos de crear.
2. una vez se encuentre en la pesta帽a de configuraci贸n del Host, de click sobre ```VMs```.
3. Aqu铆 de click sobre el bot贸n de ```Actions``` y seleccione ```New Virtual Machine```. esto desplegara un nuevo men煤 de configuraci贸n, aqu铆 ingrese la siguiente informaci贸n:
   * ```Select a creation type```: seleccione la opci贸n ```Create a new virtual machine```.
   * ```Select a name and folder```: Ingrese un nombre distintivo para la maquina virtual y seleccione la ubicaci贸n que desee utilizar para desplegarla.
   * ```Select a compute resource```: seleccione el Host creado anteriormente.
   * ```Select storage```: seleccione el datastorage creado anteriormente.
   * ```Select compatibility```: Seleccione la opci贸n ```ESXi 6.7 and later```.
   * ```Select a guest OS```: 
      * ```Guest OS Family```: Seleccione ```Linux```.
      * ```Guest OS Version```: Seleccione ```Ubuntu Linux (64.bit)```.
   * ```Customize hardware```: 
      * ```CPU```: seleccione la cantidad que desee.
      * ```Memory```: Seleccione la cantidad que desee.
      * ```New Hard disk```: Elimine el disco que se genera por defecto de click sobre el bot贸n ```ADD NEW DEVICE```y seleccione ```Existing Hard Disk```, esto abrira una nueva pesta帽a, aqu铆 seleccione el disco que adiciono anteriormente en el datastore.
      * Despliegue el men煤 de ```New Hard disk``` y cambie el valor en ```Virtual Device Node```por ```IDE 0```,```IDE (0:0) New Hard Disk```.
   * ```Ready to complete```: De click en ```Finish```.
<p align="center">
<img width="800" alt="img8" src=Imagenes/VM.gif>
</p>


# Referencias 馃摉

* [Gesti贸n de claves de API de la infraestructura cl谩sica](https://cloud.ibm.com/docs/account?topic=account-classic_keys#create-classic-infrastructure-key).
* [Iniciaci贸n a VMware Solutions](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-getting-started).

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />

     
