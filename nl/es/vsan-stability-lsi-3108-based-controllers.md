---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuración de vSAN para estabilidad en controladores basados en LSI 3108

Para evitar fallos relacionados con dispositivos al ejecutar vSAN con controladores de la serie LSI 3108, ejecute los mandatos siguientes desde el shell de ESXi:

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

Tenga en cuenta lo siguiente:

* Estos mandatos deben ejecutarse en cada host de ESXi en el clúster de vSAN.
* Estos mandatos son efectivos inmediatamente. No es necesario reiniciar.
* Estos mandatos tienen como resultado cambios persistentes y siguen configurados de un rearranque a otro.

Para obtener más información, consulte el tema de la Base de conocimiento de VMware sobre la [Configuración necesaria de vSAN y ESXi para los controladores con base en el conjunto de chips LSI 3108 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://kb.vmware.com/s/article/2144936){: new_window}.
