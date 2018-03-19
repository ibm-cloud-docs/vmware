---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Despliegue y configuración de vCenter Server Appliance (vCSA) con VMware vSphere 6  

Efectúe los pasos siguientes para desplegar VMware vCenter Server Appliance.
{:shortdesc}

**Requisitos previos**
* Sistema Windows con un navegador compatible instalado
  * Internet Explorer/Firefox/Chrome
* Hosts de vSphere con recursos suficientes para dar soporte a VMware vCenter Server Appliance
  * Para obtener más información sobre los recursos de sistema necesarios, consulte los [Requisitos mínimos para VMware vCenter Server 6.0 Appliance ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://kb.vmware.com/s/article/2106572){: new_window}.
* Imagen ISO de vCSA
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* Capacidad para montar una ISO
* Sesión de VPN con acceso a la red privada de IBM Cloud

**Despliegue y configuración de vCenter Server Appliance**

1. Monte la ISO de vCenter Server Appliance (vCSA).
2. Abra vcsa-setup.html en un navegador compatible.
3. Revise y acepte la instalación del plugin de integración de cliente de VMware.
4. Pulse **Allow**.
5. Pulse **Install**.
6. Revise y acepte los términos del acuerdo de licencia y pulse **Next**.
7. Especifique el FQDN o la dirección IP privada y el nombre de usuario y la contraseña del host de VMware en el que desea instalar vCSA. Pulse **Next**.
8. Pulse **Yes** para aceptar el aviso de certificado.
9. Especifique un nombre de dispositivo y una contraseña de SO y pulse **Next**.
10. Para el tipo de despliegue, seleccione 'Install vCenter Server with an Embedded Platform Services Controller' y, a continuación, pulse **Next**.
11. Pulse 'Create an SSO domain' y pulse **Next**. <!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. Elija un tamaño de dispositivo y pulse **Next**.
13. Seleccione un almacén de datos y pulse **Next**.
14. Seleccione 'Use an embedded database (PostgreSQL)' y pulse **Next*.
15. Defina las configuraciones de red especificando los valores siguientes:
  1. Network
  * IP address Family
  * Network Type
  * Network Address
  * System name
  * Subnet mask
  * Network gateway
  * Network DNS Servers
      * Para obtener más información, consulte la página sobre [Cuáles son las resoluciones de DNS locales](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-).
  * Configure time sync
  * Pulse **Next**.
16. Revise los valores y pulse **Finish**. La instancia de vCSA estará suministrada.

