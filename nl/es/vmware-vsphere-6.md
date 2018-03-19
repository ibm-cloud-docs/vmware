---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opciones de licencias de VMware 

Los administradores de VMware pueden aprovechar rápidamente las rentables características de la nube híbrida desplegando en una nube global de nivel empresarial de {{site.data.keyword.BluSoftlayer_full}}. Un diferenciador clave de {{site.data.keyword.BluSoftlayer_notm}} es que se pueden suministrar catálogos y cargas de trabajo de vSphere en entornos de VMware vSphere en centros de datos de {{site.data.keyword.BluSoftlayer_notm}} sin modificar invitados ni VM de VMware. Estos despliegues son posibles gracias al uso de una plataforma de gestión/orquestación y un hipervisor de vSphere común.

Además de la oferta de licencia Enterprise Plus de vSphere 6, {{site.data.keyword.BluSoftlayer_notm}} ofrece licencias mensuales para vCenter, NSX, vRealize, vSAN y Site Recovery Manager (SRM).

## VMware vSphere

**Uso previsto:** plataforma de SO de virtualización de servidor nativo que abstrae el procesador, la memoria, el almacenamiento y los recursos de red para crear varios servidores virtuales en un único servidor físico. Se pueden agrupar en clúster varios servidores físicos para crear una nube privada.

**Interfaz de usuario:** clientes de vCenter, API de VMware, CLI de VMware

**Características:**
* Migración en directo de vMotion
* Alta disponibilidad
* Tolerancia al error
* Réplica
* Virtualización de Nvidia GRID vGPU
* Optimización de capacidad de carga de trabajo
* DRS (planificador de recursos distribuidos)
* Suministro ligero
* Control de E/S de red

## VMware vCenter

**Uso previsto:** centralizar la gestión de los recursos de cálculo dentro de cada host de vSphere. Si bien los hosts de vSphere se pueden gestionar individualmente, colocarlos bajo el control de vCenter habilita las siguientes funciones:

**Interfaz de usuario:** Web Client, Thick Client, API de VMware, CLI de VMware

**Características:**
* Control y visibilidad centralizados para todos los aspectos de las máquinas virtuales de invitado y los hosts de vSphere gestionados.
* Proporciona una vista de interfaz de un único panel mediante vCenter Web Client para la red de cálculo y la gestión de almacenamiento.
* Optimización proactiva. Permite la asignación y la optimización de recursos para la máxima eficiencia en los hosts de vSphere.
* Función de gestión ampliada para otros complementos y servicios integrados, como NSX, vRealize, vSAN y Site Recovery Manager (SRM).
* Supervisión, alertas, planificación. Los administradores de la nube pueden ver sucesos y alertas en el vCenter Web Client y configurar acciones planificadas.
* Motor de automatización. vCenter es el motor que realiza las tareas que le asignan a través de la interfaz web de la API de vSphere. VMware vRealize Automation y vRealize Orchestration son ejemplos de aplicaciones que dirigen las acciones de vCenter a través de la API de VMware.

## VMware NSX

**Uso previsto:** NSX ofrece funciones de SDN (red definida por software) fundamentales para dar soporte a las operaciones de la plataforma de nube.

**Interfaz de usuario:** clientes de vCenter, API de VMware, CLI de VMware

**Características:**
* Equilibrio de carga
* Cortafuegos
* Direccionamiento
* Conmutadores lógicos
* VPN
* Segmentación VxLAN/puntos finales de túnel

## VMware vRealize

**Uso previsto:** la suite VMware vRealize es una plataforma de gestión de nube para la empresa que puede utilizar para gestionar una nube híbrida y heterogénea.

**Interfaz de usuario:** clientes de vCenter, API de VMware, CLI de VMware

**Modelo de licencia:** por procesador por mes

**Características:**
* vRealize Automation: entrega automatizada de infraestructura personalizada, aplicaciones y servicios de TI personalizados
* vRealize Operations: orquestación inteligente de gestión de la configuración, capacidad, rendimiento y estado
* vRealize Log Insight: análisis de registros y gestión de registros en tiempo real.

## VMware vSAN

**Uso previsto:** VMware vSAN es una tecnología de almacenamiento distribuido que permite que las unidades de almacenamiento local en cada host de vSphere se agreguen y agrupen en un dispositivo de almacenamiento no compartido que sea accesible para todos los hosts de un clúster de vSAN.

**Interfaz de usuario:** clientes de vCenter, API de VMware, CLI de VMware

**Características:**
* Almacenamiento basado en host distribuido
* Arquitectura no compartida
* Se amplía hasta 64 nodos
* Baja latencia
* Tolerancia al error configurable

## VMware Site Recovery Manager (SRM)

**Uso previsto:** VMware Site Recovery Manager (SRM) permite la disponibilidad y la movilidad de aplicaciones en sitios que están en entornos de nube privada. Al aprovechar al máximo la encapsulación y el aislamiento de las máquinas virtuales, Site Recovery Manager permite la automatización simplificada de la recuperación tras desastre para cumplir los objetivos de tiempo de recuperación (RTO). SRM también ayuda a reducir los costes asociados con los planes de continuidad de negocio y a conseguir resultados predecibles de bajo riesgo para la recuperación de un entorno virtual.

**Interfaz de usuario:** clientes de vCenter, API de VMware, CLI de VMware

**Características:**
* Pruebas de recuperación no disruptivas
* Flujos de trabajo de orquestación automatizada
* Recuperación automática de valores de red y seguridad
* Extensibilidad para automatización personalizada
* vMotion en vCenter orquestado
* Planes de recuperación centralizada
* Gestión basada en políticas
