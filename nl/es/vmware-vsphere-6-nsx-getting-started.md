---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a VMware vSphere 6 NSX 

NSX se despliega como una titularidad de licencia para aplicarla en su infraestructura. {{site.data.keyword.BluSoftlayer_full}} proporciona las licencias por procesador (los precios no cambian por el número de núcleos por CPU). Es necesaria una licencia de NSX en todos los servidores que utilicen un componente de NSX (Management, Control o Data Plane). NSX aporta capacidades de red adicionales a la plataforma. Puede crear una sólida red superpuesta para la seguridad del sistema, la segmentación de arrendatario y los entornos de nube híbrida que abarcan proveedores o se extienden desde nubes privadas locales.
{:shortdesc}

Puede añadir cortafuegos, equilibrio de carga, VPN, servicios NAT o micro segmentación basada en VXLAN a su entorno, con soporte para la automatización mediante una API RESTful.

## Adición de licencias
Las licencias se añaden a los servidores mediante el proceso siguiente:
1. Inicie sesión en vCenter Server con vSphere Client.
* En **Administration**, pulse **Licensing**.
* Pulse **Solutions**.
* En la lista de productos, pulse **VMware NSX for vSphere**.
* Pulse **License Key** o **Enter New license key**.
* Pulse **OK**.

## Instalación de NSX

1. Despliegue NSX Manager.
* Registre NSX Manager con vCenter Server.
* vSphere Web Client despliega las instancias de NSX Controller mediante NSX Manager.
* Prepare los hosts de vSphere utilizando NSX Manager para instalar los VIB en los hosts del clúster.
* Una vez que haya desplegado NSX Controller en todos los hosts aplicables, defina y configure los componentes de NSX como equilibradores de carga, cortafuegos y pasarelas de Edge.

## Consideraciones de despliegue

Para habilitar NSX para una solución, es necesario que utilice nodos adicionales de vSphere, además de los nodos de cálculo estándar.

**NSX Manager**<br />
IBM Informix Virtual Appliance en el clúster de gestión tiene una relación 1:1 con vCenter. Se recomiendan las características normales de HA de vSphere. NSX Manager incluye funciones de copia de seguridad programadas/bajo demanda y requiere conectividad de IP a vCenter, el controlador, los recursos de NSX Edge y los hosts de ESXi. NSX Manager se despliega en la misma subred/VLAN que vCenter, pero no es estrictamente necesario. El dimensionamiento típico de VM es el siguiente:

|Release de NSX|vCPU|Memoria|Disco de SO|
|---|---|---|---|
|6.2 Small|4|12 GB|60 GB|
|6.2 Default|4|16 GB|60 GB|
|6.2 Large Scale|4|24 GB|60 GB|
{: caption="Tabla 1. Dimensionamiento típico de VM de NSX Manager" caption-side="top"}

**Nodos de NSX Controller**<br />
Los nodos de NSX Controller se despliegan como dispositivos virtuales desde la interfaz de usuario de NSX Manager. Cada dispositivo se comunica a través de una dirección IP diferente que normalmente se encuentra dentro de la misma subred que NSX Manager, pero no es un requisito estricto. Se recomienda desplegar al menos tres VM de controlador en al menos tres nodos físicos distintos de vSphere. Estos actúan como activo-activo-activo, con delimitación de trabajo definida por NSX Manager. Si un nodo falla, una migración tras error de "regla de mayoría" redistribuye la carga de trabajo a los demás controladores. NSX no aplica esta práctica de diseño de forma nativa. Puede utilizar las reglas nativas de antiafinidad de vSphere para evitar desplegar más de un nodo de controlador en el mismo servidor ESXi. El dimensionamiento típico de VM por VM es el siguiente:

|VM de controlador|vCPU|Reserva|Memoria|Disco de SO|
|---|---|---|---|---|
|3|4|2048 Mhz|4 GB|20 GB|
{: caption="Tabla 2. Dimensionamiento típico de VM de NSX Controller" caption-side="top"}

**NSX Switch**
Se despliega un VDS (conmutador virtual distribuido) actualizado en todos los hosts para implementar las capacidades distribuidas.

**Pasarela de servicios de NSX Edge**<br />
Se despliega como dispositivos de VM multifunción según sea necesario en el entorno. Solo para el direccionamiento, se puede desplegar un clúster activo de hasta ocho pasarelas. Para todos los demás servicios, se despliega en un despliegue activo-en espera. Las comunicaciones que son externas al entorno de VM requieren direcciones IP portátiles asignadas por IBM Cloud para incluir agrupaciones NAT, puntos finales de VPN y VIP.

|Formato de pasarela|vCPU|Memoria|Uso específico|
|---|---|---|---|
|Extra grande|6|8 GB|Adecuado para LB de alto rendimiento de L7|
|Grande cuádruple|4|1 GB|Adecuado para despliegue de FW y ECMP de alto rendimiento|
|Grande|2|1 GB|Servicio único y DC pequeño|
|Compacto|1|512 MB|Despliegues pequeños o uso de servicio único o PoC|
{: caption="Tabla 3. Servicios de NSX Edge" caption-side="top"}

