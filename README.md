# vmware-vSphere-Configuracion :computer: :globe_with_meridians:

*VMware vSphere®* es una plataforma de solicitud racional y optimizada para *VMware®*. con esta plataforma, puede crear su propio entorno de *VMware* alojado por *IBM®* personalizando y solicitando el hardware compatible con *VMware* en función de los componentes de VMware seleccionado.

## Tabla de contenido 📑
1. [Requisitos](#Requisitos-newspaper)
2. [Configuración de conexión a VPN con SSL desde clientes de MotionPro]
3. [Creación y gestión de clave API para infraestructura clásica](#creación-y-gestión-de-la-clave-api-para-infraestructura-clásica-key)
4. [Despliegue de VMware Solutions Dedicated - VMware vSphere]
5. [Referencias](#referencias-)
6. [Autores](#autores-black_nib)

## Requisitos: newspaper:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>
* Contar con una cuenta de infraestructura en <a href="https://cloud.ibm.com/"> IBM Cloud</a>
* Tener instalado <a href="https://support.arraynetworks.net/prx/001/http/supportportal.arraynetworks.net/downloads/downloads.html"> MotionPro</a>


## Configuración de conexión a VPN con SSL desde clientes de MotionPro.
Antes de inciar con la descarga y configuracion del software MotionPro es necesario habilitar el acceso VPN con SSL en su cuenta de *IBM Cloud*, para esto tenga en cuenta los siguientes pasos:
1. Desde la consola de *IBM Cloud* vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana y aqui de click sobre el boton ``Usuarios/Users```.
2. Seleccione el nombre del usuario al cual desea asignarle acceso VPN con SSL.
3. En la pagina principal del ususario de click sobre el boton 

## Creación y gestión de la clave API para infraestructura clásica :key:

Antes de iniciar el despliegue de la plataforma *VMware vSphere* es necesario crear una clave API para infraestructura clásica, para esto tenga en cuenta los siguientes pasos:

1. En la consola de IBM Cloud, vaya a ```Gestionar/Manage > Acceso (IAM)/Access (IAM)```, esto lo llevara a una nueva ventana y aquí de click sobre el botón ```Claves API/API keys```.
2. Esto lo llevara a la ventana de claves API, aqui cambie la vista a claves API de la infraestructura clásica y de click sobre el botón ```Crear una clave de infraestructura clásica/Create classic infrastructure key```.
3. luego de esto copie y descargue la clave de API en un lugar seguro para poder utilizarla mas adelante.

<p align="center">
<img width="800" alt="img8" src=Imagenes/API.png>
</p>










# Referencias 📖

* [Gestión de claves de API de la infraestructura clásica](https://cloud.ibm.com/docs/account?topic=account-classic_keys#create-classic-infrastructure-key).
* [Iniciación a VMware Solutions](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-getting-started).

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />

     
