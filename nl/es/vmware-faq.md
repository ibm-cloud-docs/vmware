---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Preguntas frecuentes: VMware 

## ¿Qué nivel de licencia se habilita al desplegar vSphere desde el portal de IBM Cloud?

Enterprise Plus, el nivel más alto de licencia de vSphere.

## ¿Cómo se otorgan las licencias de VMware vSphere 6?

El método de licencias está ligado al mecanismo de despliegue. Hay dos formas de desplegar VMware 6:

1. Cuando se despliega vSphere desde el portal de control, se habilita el programa de licencias VMware Service Provider (VSPP) automáticamente. Durante el despliegue, se añade el usuario predeterminado "slvmadmin" al host para los servicios de integración y administración de vSphere en el portal de control.

2. Si despliega vSphere manualmente, puede traer su propia licencia y soporte (BYOL/BYOM), lo que permite aplicar las licencias estándar para estos hosts. **Nota:** Si desea utilizar su propia licencia de VMWare, se recomienda que pida el servidor con un sistema operativo gratuito, como CentOS, o sin sistema operativo. Después, instale el sistema operativo de VMWare mediante la [ISO virtual](../bare_metal/mount-iso-bare-metal-server.html) de IPMI.

## ¿Puedo crear una nube privada aislada de VMware?

Sí, puede desplegar sistemas nativos e instalar cualquier hipervisor admitido (incluido VMware ESX) en estos hosts. También puede desplegar máquinas virtuales utilizando las herramientas nativas de gestión. De forma predeterminada, los sistemas se despliegan en VLAN para los componentes de red y segregación (como pasarelas, direccionadores y cortafuegos) y se utilizan para crear casi cualquier topología.

## ¿Cómo se otorgan las licencias de VMware?

El método de licencias está ligado al mecanismo de despliegue.Hay dos formas de desplegar VMware:

1. Cuando se despliega ESX desde el portal, se habilita el programa de licencias VMware Service Provider (VSPP) automáticamente. Durante el despliegue, se añade el usuario predeterminado 'vmadmin' al servidor ESX para la recopilación de datos. No suprima este usuario predeterminado. El VSPP le cobrará la RAM que está reservada y se utiliza para todas las máquinas virtuales "encendidas" (no "por socket", como una licencia de host estándar).

2. Si despliega ESX manualmente, puede traer su propia licencia (BYOL), de modo que puede aplicar las licencias estándar para estos hosts. **Nota:** BYOL no se puede utilizar para hosts que se despliegan a través del portal. Se espera que se habilite el VSPP.

    * Además, no es necesaria una instancia de vCenter Server para que VSPP funcione.

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## ¿Puedo desplegar componentes de VMware directamente desde el portal de IBM Cloud?

Sí, tiene dos opciones:

1. Seleccione y despliegue el hipervisor de ESX automáticamente con un sistema nativo mensual<!-- (Figure 2)-->. También puede desplegar la gestión de vCenter automáticamente con una máquina virtual o un sistema nativo (solo Windows).

2. Despliegue un host nativo con un sistema operativo gratuito, como CentOS, y luego instale ESX manualmente mediante la consola remota y el acceso de soporte virtual del host. Puede entonces instalar manualmente vCenter Server o desplegar la instancia de VMware vCenter Server Appliance que se utiliza en Linux.

