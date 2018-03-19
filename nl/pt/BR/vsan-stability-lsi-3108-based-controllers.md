---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurando vSANs para estabilidade em controladores baseados no LSI 3108

Para ajudar a evitar falhas relacionadas a dispositivo ao executar vSAN com controladores de série LSI 3108, execute os comandos a seguir no shell ESXi:

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

Observe:

* Esses comandos devem ser executados em cada host ESXi no cluster vSAN.
* Esses comandos ficam imediatamente efetivos. Nenhuma reinicialização é necessária.
* Esses comandos resultam em mudanças persistentes e permanecem configurados entre reinicializações.

Para obter mais informações, consulte o tópico da Base de Conhecimento do VMware, [Configuração de vSAN e ESXi necessária para controladores baseados no chipset LSI 3108 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://kb.vmware.com/s/article/2144936){: new_window}.
