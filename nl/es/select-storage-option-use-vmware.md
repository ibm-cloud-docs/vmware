---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Almacenamiento para utilizar con sistemas VMware
En lo que respecta al almacenamiento, tiene varias opciones. Puede ser privado, compartido o puede traer sus propias soluciones de almacenamiento. Utilice la siguiente información para decidir qué solución de almacenamiento se adapta mejor a se carga de trabajo.

La tabla 1 contiene los niveles de almacenamiento en los que puede entrar su carga de trabajo.
<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabla 1. Niveles de almacenamiento</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Nivel 1</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Nivel 2</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Nivel 3</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Uso empresarial</strong></p>
			</td>
			<td style="width:160px;">
				<p>Datos, bases de datos y aplicaciones de producción de alta disponibilidad o de alto rendimiento</p>
			</td>
			<td style="width:160px;">
				<p>Datos, bases de datos y aplicaciones de prueba y desarrollo no indispensables</p>
			</td>
			<td style="width:160px;">
				<p>Archivado, copia de seguridad y almacenamiento de datos no indispensables</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Rendimiento</strong></p>
			</td>
			<td style="width:160px;">
				<p>Alto (SSD, SAS)</p>
			</td>
			<td style="width:160px;">
				<p>Medio (SAS, SATA)</p>
			</td>
			<td style="width:160px;">
				<p>Bajo (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>IOPS garantizadas</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sí</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Alta disponibilidad (HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sí</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Réplica</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sí</p>
			</td>
			<td style="width:160px;">
				<p>Sí</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Instantáneas</strong></p>
			</td>
			<td style="width:160px;">
				<p>Sí</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
	</tbody>
</table>


## Opciones de almacenamiento compartido y privado de VMware

Puede elegir entre varias opciones de almacenamiento. Para el almacenamiento privado, puede seleccionar opciones de disco local, VSAN o QuantaStor. Para el almacenamiento compartido, puede seleccionar almacenamiento de Resistencia o Rendimiento. Si decide traer su propio almacenamiento, hay varias opciones "privadas", incluido NetApp OnTap Edge, NetApp Private Storage (NPS), {{site.data.keyword.IBM}} Spectrum Accelerate y almacenamiento definido por software. La tabla 2 y la tabla 3 ofrecen una comparación paralela de las opciones, para su comodidad.

## Opciones de almacenamiento privado

Existen varias opciones para el almacenamiento para conectarse a VMware en un entorno de un solo arrendatario: 

* Local
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## Almacenamiento local

Haga un pedido de {{site.data.keyword.baremetal_short}} desde el portal de clientes de IBM Cloud con ESX y seleccione los discos que desee [SATA, SCSI conectadas en serie (SA SCSI) o SSD].
 
Puede traer su propia licencia de ESX, pero debe abrir una incidencia para informar del cambio al equipo de soporte.

* Cargas de trabajo recomendadas: Nivel 3
* Rendimiento: limitado, depende de RAID y del tipo de disco. Las SSD suponen un aumento del coste a cambio de un mejor rendimiento.
* Escalabilidad: limitada al número de ranuras de unidad del chasis
* Protocolos: no aplicable
* Coste: gastos de capital (CAPEX) y gastos operativos (OPEX) bajos
* HA: no disponible
* Réplica: [Dispositivo virtual de vSphere Replication ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Fiabilidad: varios puntos únicos de anomalía



## vSAN [1]

* Cargas de trabajo recomendadas: Nivel 1
* Rendimiento: +90.000 IOPS por host según la configuración de host
* Escalabilidad: v5.5 de disco de máquina virtual (VMDK), hasta 2 TB; v6.0 de VMDK, hasta 62 TB. Se escala horizontalmente con más nodos.
* Protocolos: propietario
* Coste: medio, tanto CAPEX como OPEX
* HA: admitida tanto en errores de disco como de host. Los dominios de anomalía se admiten desde la v6 de VMware.
* Réplica: [Dispositivo virtual de vSphere Replication ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Réplica y recuperación tras desastre:
    1. Planificación de copia de seguridad de VM a través de VMware vCenter Server
    2. Creación de instantáneas de VM
    3. Creación de DE de datos para la VM
    4. Restauración de la VM
 * Fiabilidad: tolera hasta tres anomalías de host con siete o más hosts. Los dominios de anomalía se incluyeron en v6 de VMware.   

[1] La nueva característica de vSan 6.2, los clústeres extendidos, permite que los hosts estén en distintos pods en el mismo centro de datos (hay pruebas de validación en curso). <!-- Should this in progress mention be removed? -->

vSAN 5.5 sólo está disponible con BYOL (traiga su propia licencia). VMware sólo lo admite si se utiliza un controlador de disco Avago LSI MegaRAID SAS 9361-8i.

vSAN 6.0 está disponible directamente desde el portal de IBM Cloud con una base de facturación de licencia de CPU.

## QuantaStor

Puede utilizar la [Guía de diseño de solución de OSNexus ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} para conectar VMware con QuantaStor.

* Cargas de trabajo recomendadas: Niveles 2 y 3 
* Rendimiento: variable en función del número de unidades, RAID y el uso de disco (iSCSI o NFS)  
* Escalabilidad: v3 de un solo bastidor admite 128 TB, no aumenta ni se escala horizontalmente. 
* Protocolos: iSCSI, NFS y SMB 
* Coste: alto, tanto CAPEX como OPEX 
* HA: no disponible  
* Réplica: características de réplica incorporadas; sin SRA disponible. También puede utilizar vSphere Replication Appliance. 
* Fiabilidad: punto único de anomalía para el alojamiento y el controlador RAID.


<a name="NetApp"></a>
## NetApp Data OnTap Edge

Debe adquirir un dispositivo NetApp de NetApp o IBM. Debe instalarlo en un {{site.data.keyword.baremetal_short}} en su centro de datos de {{site.data.keyword.BluSoftlayer}}.

Para obtener más información sobre la conexión de VMware con NetApp, consulte los enlaces siguientes:
* [Selección de NetApp ONTAP ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: cree un centro de datos en un servidor con los principios básicos de NetApp ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* Cargas de trabajo recomendadas: Niveles 2 y 3
* Rendimiento: variable en función del número de unidades y RAID
* Escalabilidad: admite 110 TB; no se escala horizontalmente.
* Protocolos: iSCSI, NFS y SMB
* Coste: medio, tanto CAPEX como OPEX
* HA: no disponible
* Réplica: admite SnapMirror; también se consigue mediante [vRealize Automation ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.vmware.com/products/vrealize-automation){: new_window} (vRA).
* Fiabilidad: punto único de anomalía para el alojamiento y el controlador RAID.

<a name="NPS"></a>
## NetApp Private Storage

Debe adquirir un dispositivo NetApp de NetApp o IBM. Debe instalarlo en uno de los sitios de colocación cerca del centro de datos de IBM Cloud y conectarlo mediante Direct Link Colocation o Direct Link Cloud.

Para obtener más información sobre la conexión a VMware con NetApp, consulte los enlaces siguientes: 
* [NetApp Private Storage for IBM Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Resumen de solución: NetApp Private Storage for IBM Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* Cargas de trabajo recomendadas: Nivel 1
* Rendimiento: según el modelo de NetApp
* Escalabilidad: admite la adición de unidades y bastidores para aumentar la capacidad y las IOPS
* Protocolos: iSCSI, NFS y SMB
* Coste: alto, tanto CAPEX como OPEX
* HA: controladores y cabeceras duales
* Réplica: admite SnapVault y SnapMirror; también se consigue mediante [vRealize Automation ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.vmware.com/products/vrealize-automation).
* Fiabilidad: admite MPIO y alta redundancia

<a name="IBM"></a>
## IBM Spectrum Accelerate

La opción de almacenamiento privado de IBM Spectrum Accelerate no está disponible en el portal de clientes de IBM Cloud. <!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* Cargas de trabajo recomendadas: Nivel 1
* Rendimiento: depende del número de discos, SSD (opcional) y la cantidad de memoria que se da a cada VM "de nodo".
* Escalabilidad: se escala ~8 - 325 TB utilizables
  * Capacidad mínima: 3 VM x 6 unidades
  * Capacidad máxima: 15 VM x 12 unidades
  * Aumenta hasta 144 matrices virtuales y más de 40 PB utilizables mediante IBM Hyper-Scale Manager
  * Expansión de capacidad no disruptiva añadiendo más nodos
  * 1 x SSD de 500 u 800 GB por nodo admitida
* Protocolos: solo iSCSI
* Coste: depende del modelo de precios y las máquinas físicas desplegadas para los nodos. CAPEX alto, OPEX medio-bajo en función de la licencia.
  * Precio por binario (TiB) de capacidad utilizable
  * No vinculado a ninguna configuración de hardware específica. Ejemplo: una licencia de 200 TiB se podría desplegar de varias formas: una instancia de 200 TiB, dos instancias de 100 TiB o cuatro instancias de 50 TiB
  * Se ofrece de dos maneras: licencia perpetua [incluye un año de suscripción y servicio (S&S)] y licencia mensual (incluye S&S)
* HA: solución en clúster
* Réplica: se consigue mediante [vRealize Automation ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.vmware.com/products/vrealize-automation){: new_window} o SRA, que se puede utilizar para replicar desde IBM XIV físico con Site Recovery Manager (SRM) de VMware
  * [Réplica de vSphere ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [Directrices de VMware vCenter Site Recovery Manager versión 5.x para IBM XIV Gen3 Storage System ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* Fiabilidad: admite MPIO y alta redundancia. Cualquier nodo disponible puede gestionar el clúster. Las siguientes prestaciones no están admitidas por IBM Spectrum Accelerate en este momento en IBM XIV basado en hardware:
  * Duplicación de tres sitios
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG v6
  * Unidades de disco de 6 TB
  * Storage Management Initiative Specifications (SMI-S) 1.6
  * Cifrado de datos en descanso
  * Licencias de VAAI (vStorage for API Array Integration) alineadas con volúmenes virtuales (VVol)
  * vCenter Operations Manager (VCop)
  * Para obtener más información sobre IBM XIV Storage System, consulte la página sobre [Integración de aplicaciones y plataformas para IBM XIV Storage System ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}

## Opciones de almacenamiento compartido

Hay dos opciones de almacenamiento que puede utilizar para conectarse a VMware en un entorno multiarrendatario: Almacenamiento en bloque y Almacenamiento de archivos.

### Almacenamiento en bloque y de archivos

Solicite el {{site.data.keyword.baremetal_short}} desde el portal de clientes de IBM Cloud con ESX.

En VMware, se proporcionan tres valores predefinidos <!--**Authorize** (**Block** or **File**) **Storage SoftLayer** --> en el separador **Host Device Details Storage**: Username, Password (for CHAP authentication) y Host IQN.

Para obtener más información sobre cómo suministrar almacenamiento en bloque, consulte la página de [Suministro y gestión de almacenamiento en bloque](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Para obtener más información sobre cómo suministrar almacenamiento de archivos, consulte la página de [Suministro y gestión de almacenamiento de archivos de IBM para IBM Cloud](/docs/infrastructure/FileStorage/provisioning-file-storage.html).

* Cargas de trabajo recomendadas: Niveles 1, 2 y 3
* Dos formas de suministrar rendimiento:
    1. Niveles de IOPS de Resistencia: disponible en 0,25, 2, 4 o 104 IOPS por GB
    2. IOPS asignadas de Rendimiento: especifique las IOPS independientemente de la capacidad. Recomendado para cargas de trabajo con requisitos de rendimiento bien definidos.
    * Parámetros de rendimiento de almacenamiento previsibles
    * Es posible seccionar conjuntamente diversos volúmenes para conseguir más IOPS y un mayor rendimiento
* Latencia <10 ms HASTA 48.000 IOPS
* Escalabilidad: pida desde 20 GB hasta 12 TB. No puede redimensionar el volumen una vez hecho el pedido.
* Protocolos: iSCSI y NFS
* Coste: alto, tanto CAPEX (10x para SAN del mismo tamaño) como OPEX
* HA: controladores y cabeceras duales
* Réplica: instantánea y réplica proporcionadas a través de la red privada de IBM Cloud; también se consiguen mediante [vRealize Automation ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.vmware.com/products/vrealize-automation){: new_window}, pero no SRA.
* Fiabilidad: alta redundancia, iSCSI utiliza una conexión MPIO, el almacenamiento basado en NFS se direcciona a través de conexiones TCP/IP. Instantánea y réplica habilitadas.

La tabla 2 proporciona los pros y los contras del almacenamiento privado en un entorno de un solo arrendatario.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabla 2. Pros y contras de las opciones de almacenamiento privado de VMware</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; Almacenamiento privado (un solo arrendatario)</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>Factores clave/opción de almacenamiento</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>Local</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>SAN Virtual</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:99px;">
				<p>QuantaStor</p>
			</td>
			<td bgcolor="#C6D9F1" colspan="2" style="width:159px;">
				<p align="center">NetApp</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p>IBM Spectrum Accelerate</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>OnTap Edge</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>NPS</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p align="center">&nbsp;</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Tipo</strong></p>
			</td>
			<td style="width:87px;">
				<p>Local</p>
			</td>
			<td style="width:95px;">
				<p>SDS</p>
			</td>
			<td style="width:99px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>Monolítico</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Rendimiento</strong></p>
			</td>
			<td style="width:87px;">
				<p>Basado en especificaciones SA-SCSI/SSD; además RAID 5/10 puede utilizarse para leer/grabar las ganancias.</p>
			</td>
			<td style="width:95px;">
				<p>+90.000 IOPS por host según la configuración de host. 100 VM por host, 32 hosts por clúster, 3.200 VM por clúster, solo 2048 protegidas (v5.5).</p>
				<p>Hasta 20.000 IOPS, 200 VM por host, 64 hosts por clúster y 6000 VM protegidas por clúster (v6.0).</p>
			</td>
			<td style="width:99px;">
				<p>Basado en los tipos y el número de discos seleccionados, así como en las configuraciones RAID y el uso de iSCSI o NFS.</p>
			</td>
			<td style="width:80px;">
				<p>Basado en los tipos y el número de discos seleccionados, así como en las configuraciones RAID. </p>
			</td>
			<td style="width:80px;">
				<p>Según el modelo.</p>
			</td>
			<td style="width:96px;">
				<p>Basado en los tipos y el número de discos seleccionados, así como en las configuraciones RAID y el uso opciones de disco SSD por nodo de hipervisor.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Escalabilidad</strong></p>
			</td>
			<td style="width:87px;">
				<p>Crecimiento limitado en tamaño y en rendimiento de E/S de disco.</p>
			</td>
			<td style="width:95px;">
				<p>Disco de máquina virtual (VMDK) de hasta 2 TB con v5.5, y hasta 62 TB con v6.0.</p>
				<p>Se escala horizontalmente con más nodos.</p>
			</td>
			<td style="width:99px;">
				<p>QS único hasta 128 TB (3.x). No aumenta ni se escala horizontalmente.</p>
			</td>
			<td style="width:80px;">
				<p>Hasta 10 TB; no se escala horizontalmente.</p>
			</td>
			<td style="width:80px;">
				<p>Sí, añadir estantes de disco para capacidad e IOPS.</p>
			</td>
			<td style="width:96px;">
				<p>Se escala de ~8 a 325 TB de espacio utilizable.</p>
				<p>La capacidad mín. es de 3 VM x 6 unidades.</p>
				<p>La capacidad máx. es de 15 VM x 12 unidades.</p>
				<p>Aumenta hasta 144 matrices virtuales y más de 40 PB utilizables mediante IBM Hyper-Scale Manager.</p>
				<p>Expansión de capacidad no disruptiva añadiendo más nodos.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocolos</strong></p>
			</td>
			<td style="width:87px;">
				<p>NA</p>
			</td>
			<td style="width:95px;">
				<p>Propietario</p>
			</td>
			<td style="width:99px;">
				<p>iSCSI/NFS/SMB</p>
			</td>
			<td colspan="2" style="width:159px;">
				<p align="center">iSCSI/NFS/SMB</p>
			</td>
			<td style="width:96px;">
				<p>iSCSI</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Casos prácticos</strong></p>
			</td>
			<td style="width:87px;">
				<p>Cargas de trabajo de nivel 2 y 3</p>
			</td>
			<td style="width:95px;">
				<p>Cargas de trabajo de nivel 1</p>
			</td>
			<td style="width:99px;">
				<p>Cargas de trabajo de nivel 2 y 3</p>
			</td>
			<td style="width:80px;">
				<p>Cargas de trabajo de nivel 2 y 3</p>
			</td>
			<td style="width:80px;">
				<p>Cargas de trabajo de nivel 1</p>
			</td>
			<td style="width:96px;">
				<p>Cargas de trabajo de nivel 1</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Alta disponibilidad (HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>Disponible con RAID</p>
			</td>
			<td style="width:95px;">
				<p>Sí; errores de disco y de host; dominios de anomalía (v6.0)</p>
			</td>
			<td style="width:99px;">
				<p>No disponible en IBM Cloud.</p>
			</td>
			<td style="width:80px;">
				<p>NA</p>
			</td>
			<td style="width:80px;">
				<p>Sí; controladores y cabeceras duales.</p>
			</td>
			<td style="width:96px;">
				<p>Sí; solución en clúster.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Posibilidades de configuración</strong></p>
			</td>
			<td style="width:87px;">
				<p>Número y tipo de discos; niveles de RAID.</p>
			</td>
			<td style="width:95px;">
				<p>Controladores específicos necesarios.</p>
			</td>
			<td style="width:99px;">
				<p>CPU, memoria, memoria caché, número y tipo de discos y niveles de RAID.</p>
			</td>
			<td style="width:80px;">
				<p>CPU, memoria, memoria caché, número y tipo de discos y niveles de RAID.</p>
			</td>
			<td style="width:80px;">
				<p>Por determinar</p>
			</td>
			<td style="width:96px;">
				<p>CPU, memoria, caché, número y tipo de discos, SSD, memoria caché, configuración de puerto de iSCSI. QOS multiarrendatario.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Réplica y recuperación tras desastre</strong></p>
			</td>
			<td style="width:87px;">
				<p>Se utiliza vRA para replicar; sin SRA.</p>
			</td>
			<td style="width:95px;">
				<p>Se utiliza vRA para replicar.</p>
			</td>
			<td style="width:99px;">
				<p>Réplica incorporada; sin SRA disponible.</p>
			</td>
			<td style="width:80px;">
				<p>Se puede utilizar vRA para replicar, SnapMirror.</p>
			</td>
			<td style="width:80px;">
				<p>Se puede utilizar vRA para replicar, SnapMirror, SnapVault.</p>
			</td>
			<td style="width:96px;">
				<p>Se admiten vRA o SRA; réplica entre dispositivos XIV físicos y SDS.</p>
				<p>Se admiten instantáneas; recuperación de aplicaciones a través de IBM FlashCopy Manager.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Fiabilidad</strong></p>
			</td>
			<td style="width:87px;">
				<p>Punto único de anomalía sin HA.</p>
			</td>
			<td style="width:95px;">
				<p>Tolera hasta tres anomalías de host con siete o más hosts.</p>
				<p>Los dominios de anomalía se incluyen en v6.0.</p>
			</td>
			<td style="width:99px;">
				<p>Punto único de anomalía (alojamiento y controlador RAID) y sin HA.</p>
			</td>
			<td style="width:80px;">
				<p>Punto único de anomalía (alojamiento y controlador RAID) y sin HA.</p>
			</td>
			<td style="width:80px;">
				<p>Conexión de E/S de multivía de acceso (MPIO) de alta redundancia.</p>
			</td>
			<td style="width:96px;">
				<p>Conexiones MPIO de iSCSI de alta redundancia: cualquier nodo puede gestionar el clúster.</p>
			</td>
		</tr>
	</tbody>
</table>

Enlaces de documentación de la tabla 2:
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge: no disponible en el portal de clientes - traiga su propia solución.
  * [Guía de instalación y administración de Data ONTAP ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Guía de configuración exprés de Data ONTAP ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate: no disponible en el portal de clientes - traiga su propia solución.
  * [Cómo trabajar con un sistema IBM Spectrum Accelerate ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

La tabla 3 proporciona los pros y los contras del almacenamiento compartido en un entorno multiarrendatario.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabla 3. Pros y contras de las opciones de almacenamiento compartido de VMware</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>Almacenamiento compartido de VMware (multiarrendatario)</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Factores clave/opciones de almacenamiento</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">Resistencia, en bloque y de archivos</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">Rendimiento, en bloque y de archivos</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Tipo</strong></p>
			</td>
			<td style="width:266px;">
				<p>SDS</p>
			</td>
			<td style="width:271px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Rendimiento</strong></p>
			</td>
			<td style="width:266px;">
				<p>Disponible en 0,25, 2, 4 o 104 IOPS por GB.</p>
				<p>Parámetros de rendimiento de almacenamiento previsibles.</p>
				<p>Es posible seccionar conjuntamente diversos volúmenes para conseguir más IOPS y un mayor rendimiento.</p>
			</td>
			<td style="width:271px;">
				<p>El cliente suministra el nivel deseado de rendimiento en función de las necesidades de carga de trabajo o nivel de precio.</p>
				<p>&nbsp;</p>
				<p>Parámetros de rendimiento de almacenamiento previsibles.</p>
				<p>Es posible seccionar conjuntamente diversos volúmenes para conseguir más IOPS y un mayor rendimiento.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Escalabilidad</strong></p>
			</td>
			<td style="width:266px;">
				<p>Los tamaños de volumen oscilan entre 20 GB y 12 TB. No se pueden redimensionar una vez realizado el pedido. </p>
			</td>
			<td style="width:271px;">
				<p>Los tamaños de volumen oscilan entre 20 GB y 12 TB. No se pueden redimensionar una vez realizado el pedido.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocolos</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI y NFS.</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI y NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Conexiones de host</strong></p>
			</td>
			<td style="width:266px;">
				<p>Un máximo de ocho para iSCSI y 64 para NFS.</p>
			</td>
			<td style="width:271px;">
				<p>Un máximo de ocho para iSCSI y 64 para NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Casos prácticos</strong></p>
			</td>
			<td style="width:266px;">
				<p>Cargas de trabajo de nivel 1, 2 y 3:</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 0,25 IOPS por GB: baja intensidad de E/S. Entre las aplicaciones de ejemplo, se incluyen el almacenamiento de buzones de correo o el uso compartido de archivos a nivel departamental.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 2 IOPS por GB: fines generales. Entre las aplicaciones de ejemplo, se incluye el alojamiento de bases de datos pequeñas que respaldan aplicaciones web o imágenes de disco de máquinas virtuales para un hipervisor.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 4 IOPS por GB: alta intensidad de E/S. Entre las aplicaciones de ejemplo, se incluyen las bases de datos transaccionales y otras bases de datos que dependen del rendimiento.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 10 IOPS por GB: alta intensidad de E/S. Entre las aplicaciones de ejemplo, se incluye el análisis.</p>
			</td>
			<td style="width:271px;">
				<p>Cargas de trabajo de nivel 1, 2 y 3:</p>
				<p>Almacenamiento basado en iSCSI MPIO ideal para aplicaciones de E/S intensiva, como bases de datos relacionales que requieren niveles previsibles de rendimiento. Los volúmenes de almacenamiento vienen en tamaños de 20 GB a 12 TB con IOPS seleccionables por el usuario que oscilan entre 100 y 48.000 IOPS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>HA</strong></p>
			</td>
			<td style="width:266px;">
				<p>Sí, controladores y cabeceras duales.</p>
			</td>
			<td style="width:271px;">
				<p>Sí, controladores y cabeceras duales.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Posibilidades de configuración</strong></p>
			</td>
			<td style="width:266px;">
				<p>Solo tamaño e IOPS.</p>
			</td>
			<td style="width:271px;">
				<p>Solo tamaño e IOPS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Réplica y recuperación tras desastre</strong></p>
			</td>
			<td style="width:266px;">
				<p>Se proporcionan instantánea y réplica, que se realizan a través de la red privada de IBM Cloud. Puede utilizar vRA para replicar a nivel de la VM; sin SRA.</p>
			</td>
			<td style="width:271px;">
				<p>Se proporcionan instantánea y réplica, que se realizan a través de la red privada de IBM Cloud. Puede utilizar vRA para replicar a nivel de la VM; sin SRA.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Fiabilidad</strong></p>
			</td>
			<td style="width:266px;">
				<p>Alta redundancia, conexión MPIO, conexiones TCP/IP direccionadas por almacenamiento de archivos basado en NFS. Instantáneas y réplica habilitadas.</p>
			</td>
			<td style="width:271px;">
				<p>Alta redundancia, conexión MPIO, conexiones TCP/IP direccionadas por almacenamiento de archivos basado en NFS.</p>
			</td>
		</tr>
	</tbody>
</table>

Enlaces de documentación de la tabla 3:
* [Almacenamiento en bloque](/docs/infrastructure/BlockStorage/index.html)
* [Almacenamiento de archivos](/docs/infrastructure/FileStorage/index.html)
