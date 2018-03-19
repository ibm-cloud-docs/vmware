---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Stabilität für vSANs auf LSI 3108-basierten Controllern konfigurieren

Führen Sie in der ESCi-Shell die folgenden Befehle aus, um gerätebezogene Fehler beim Ausführen von vSAN mit Controllern der Serie LSI 3108 zu vermeiden:

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

Dabei ist Folgendes zu beachten:

* Diese Befehle müssen auf jedem ESXi-Host im vSAN-Cluster ausgeführt werden.
* Diese Befehle sind sofort wirksam. Es ist kein Warmstart erforderlich.
* Diese Befehle bewirken persistente Änderungen, die auch nach Warmstarts konfiguriert bleiben.

Weitere Informationen finden Sie in der VMware Knowledge Base im Abschnitt [Required vSAN and ESXi configuration for controllers based on the LSI 3108 chipset ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://kb.vmware.com/s/article/2144936){: new_window}.
