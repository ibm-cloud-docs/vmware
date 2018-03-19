---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  Migración y actualización a VMware vSphere 6

Expanda o traslade sus entornos de nube de VMware a cualquier centro de datos de {{site.data.keyword.BluSoftlayer_full}} rápida y fácilmente mediante el panel de control de gestión de VMware. Para migrar y actualizar las cargas de trabajo de vSphere, utilice los pasos siguientes como guía.
{:shortdesc}

1. Recopile datos.
2. Revise la arquitectura existente:
  1. Utilización de recursos (CPU/memoria/almacenamiento).
  2. Rastree y proyecte las tasas de crecimiento.
  3. Identifique los proyectos futuros próximos.
  4. Determine qué vlan/subredes/etc están desplegadas (disponible en el portal de control).
  5. Busque las subredes autodefinidas RFC1918 (privadas) en uso para la solución.
3. Revise la documentación de VMWare 6 y únase a las comunidades de VMWare:
  1. [Documentación de VMware vSphere ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [Red de tecnología de VMware ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://communities.vmware.com/welcome){: new_window}
4. Actualice la formación de su equipo de administración para dar soporte a VMWare 6.
5. Planifique y diseñe una nueva arquitectura.
6. Seleccione un [centro de datos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window} según la conformidad. Colabore con el departamento de ventas de IBM Cloud para refinar la ubicación candidato en función de la disponibilidad de productos/servicios.
7. Defina las VLAN y subredes necesarias (IP públicas y privadas portátiles).
8. Diseñe los servidores de vSphere:
  1. Revise el catálogo actual de servidores de IBM Cloud. Los servidores Intel Xeon v3 se recomiendan junto con enlaces ascendentes redundantes, fuentes de alimentación redundantes y RAID-1 para discos locales (de arranque).
  2. La mayoría de los clientes con VMWare siguen un techo de capacidad de disco duro de N+1 (todas las VM se pueden asignar cómodamente a los servidores con un solo nodo eliminado, para mantenimiento/fallo/etc.).
  3. Muchos clientes quieren un "techo flexible" más alto del 80% aproximadamente (80% de capacidad en la configuración de servidor 'n') en comparación con el estándar de 60-75%, debido a la breve respuesta del cálculo.
  4. Es posible que se necesiten licencias de SO externo (como Microsoft, Red Hat) para los invitados de vSphere de un proveedor externo.
  5. Revise el documento de [mejores prácticas de rendimiento para VMware vSphere 6.0 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window}.
9. Diseñe el servidor de vCenter Server:
  1. Normalmente, una instancia de servidor virtual mediana (VSI) es el punto de entrada para entornos pequeños (8 vCPU + 16 GB de RAM), mientras que un servidor nativo se utiliza para entornos más grandes.
  2. vCenter puede desplegarse en una máquina virtual autónoma VSI de Windows como complemento del sistema operativo o como dispositivo.
    1. Enlaces de referencia:
        * [Requisitos de instalación de vCenter Server 6.0 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://kb.vmware.com/s/article/2107948){: new_window}.
        * Documento de [mejores prácticas y rendimiento de VMware vCenter Server ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}.
        * [Despliegue y configuración de vCenter Server Appliance (vCSA) con VMware vSphere 6](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. Servidores no VMWare: identifique y planifique los servidores no VMWare (virtuales o nativos) que puedan ser necesarios y planifique en consecuencia.
11. Almacenamiento:
  1. Desarrolle un plan de almacenamiento para el entorno. Resistencia 2 IOPS/GB con espacio de instantáneas para virtualización es un buen plan de almacenamiento para empezar, pero si se utilizan bases de datos virtuales u otras aplicaciones de alto rendimiento, es más adecuado el nivel 4 IOPS/GB. Normalmente se recomienda el almacenamiento NFS.  
  2. La matriz de selección está disponible en [Almacenamiento para utilizar con sistemas VMware](select-storage-option-use-vmware.html).
  3. El espacio de instantáneas se utiliza de forma más común como medida secundaria para restauraciones de punto en el tiempo. El 10% es un buen punto de inicio porque el proceso es muy eficiente y se puede medir con facilidad.
12. Copias de seguridad:
  1. Asegúrese de que la estrategia de copia de seguridad existente funciona. Si no existe ninguna estrategia de copia de seguridad, se debe crear.
  2. Puede utilizar su propia solución de copia de seguridad. Puede utilizar las funciones de copia de seguridad que se incluyen con la licencia Enterprise Plus de vSphere, soluciones optimizadas de terceros, como VEEAM, o copias de seguridad tradicionales r1soft de IBM Cloud.
13. Desarrolle una estrategia de migración:
  1. Revise las [mejores prácticas para instalar o actualizar a ESXi 6.0 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://kb.vmware.com/s/article/2109712){: new_window}.
  2. Revise el DNS existentes y las configuraciones IP existentes y reduzca el TTL según sea necesario.
  3. Desarrollar un plan para las VM para incluir el host de origen, el host de destino, las IP de origen, las IP de destino y las entradas de DNS asociadas.
  4. En la mayoría de los casos, es mejor migrar VM por VM y luego actualizar las configuraciones de red públicas y privadas. Cuando pasa de versiones anteriores a versiones más recientes, suele ser mejor apagar la VM y realizar una _desconexión/conexión_ entre los entornos. Si se desplaza entre ubicaciones, es posible un vMotion de larga distancia.
  5. Desarrolle planes de prueba para la verificación del entorno.
  6. Coordine una ventana de cambio/mantenimiento con los usuarios. Las ventanas de mantenimiento de VM individual pueden concentrar la transferencia de datos, la configuración de la VM, el cambio y la propagación del DNS y el tiempo de resolución de problemas.
14. Despliegue el nuevo entorno:
  1. [Iniciación a VMware vSphere 6](vmware-vsphere-6-getting-started.html).
  2. Pida los nuevos servidores de vSphere y vCenter (así como cualquier otro servidor que necesite).
      **Nota:** Asegúrese de que se seleccionen los enlaces ascendentes de red "no enlazados" adecuados.
  3. Solicite y configure el almacenamiento adecuado: [Guía de arquitectura para almacenamiento de archivos de IBM para IBM Cloud con VMware](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html)
  4. Solicite las nuevas VLAN y subredes portátiles (puede que sean necesarios diagramas de arquitectura detallada y una justificación).
  5. Configure vCenter para comunicarse con los servidores de vSphere y configure el entorno.
  6. Realice copias de seguridad en el entorno en directo.
  7. Ejecute el plan de migración y los planes de prueba asociados.
  8. Implemente copias de seguridad en el nuevo entorno.
  9. Active el nuevo entorno.
  10. Deje fuera de servicio el entorno antiguo.
