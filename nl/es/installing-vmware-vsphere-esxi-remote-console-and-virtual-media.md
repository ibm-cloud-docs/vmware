---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Instalación de VMware vSphere ESXi mediante la consola remota y soportes virtuales

El despliegue de ESX desde soportes de instalación es similar en todas las versiones y se puede utilizar en casos de ejemplo BYOL (traiga su propia licencia).

## Requisitos
* Una instancia de máquina virtual (VM) que tenga acceso a la red privada [como por ejemplo una instancia de cálculo en nube (VSI) que se instale con Windows o Linux, con un navegador habilitado para Java, accesible mediante dvpn.softlayer.com o una IP pública]. La VSI debe estar en la misma red privada que las direcciones de Intelligent Platform Management Interface (IPMI) del servidor.
* Una copia de la ISO del programa de instalación VIM de VMware ESXi.

<!--## Steps -->

## Conexión a IPMI
1. Cargue la ISO de VMware en la VSI que se especifica en los requisitos (las VSI deben tener acceso web público).
2. Recopile la información de inicio de sesión y la dirección de IPMI del portal de clientes.
3. Seleccione **Dispositivos** > **Lista de dispositivos** > **[Servidor]** > y el separador **Gestión remota**.
4. Conéctese por Remote Desktop Protocol (RDP) o Remote X a la VSI en la que se almacena la imagen de ESXi.
5. Abra un navegador web en la sesión RDP e indique la dirección de IPMI que ha recopilado en el paso 2.
6. Inicie sesión en la consola de IPMI con las credenciales, que también se encuentran en el paso 2 (normalmente, root).
* Tome nota de su nivel de acceso de usuario de IPMI. Podría ser Administrator. Si está definido en **Operator**, se podría producir un problema al montar el almacenamiento remoto. Presente una incidencia de soporte para elevar sus credenciales de IPMI si no puede montar soportes.
7. Confirme que está en la página de inicio de sesión y pulse **Remote Control** > **Console Redirection** > **Launch Console**.

## Conexión de ISO
1. En el visor de KVM (máquina virtual basada en kernel), seleccione **Virtual Media** > **Virtual Storage**. El sistema operativo y la versión de Java pueden requerir que permita el acceso para iniciar el visor basado en Java.
2. Pulse el separador **CDROM & ISO** en la ventana Virtual Storage. Para Logical Drive Type, seleccione **ISO File** y pulse **Open Image**.
3. Vaya a la ISO de ESXi y pulse **OK**. A continuación, pulse **Plug in**.
4. Una vez que la ISO esté conectada a la sesión, pulse **OK**.
* Vuelva a la página web de IPMI y pulse **Remote** **Control** > **Reset Server** > **Perform Action** para reiniciar el servidor.

### Instalación y definición de la configuración de red
1. Instale ESXi.
* Una vez finalizada la instalación, asegúrese de pulsar **Plug Out** para desconectar la ISO y poder reiniciar el servidor.
2. Reinicie el servidor.
3. Configure la dirección IP del servidor después de que se reinicie.
4. Recopile los detalles del separador de configuración del dispositivo.

Ahora puede gestionar el host de ESXi.

Para obtener más información sobre cómo configurar el almacenamiento en bloque de Resistencia o Rendimiento, consulte la página de [Suministro y gestión de almacenamiento en bloque](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Para obtener más información sobre cómo configurar QuantaStor, consulte la [Guía de arquitectura para QuantaStor](architecture-guide-quantastor-vmwaresoftlayer.html).
