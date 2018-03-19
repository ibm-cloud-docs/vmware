---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# LSI 3108 ベース・コントローラーでの安定性のための vSAN の構成

LSI 3108 シリーズのコントローラーを使用して vSAN を実行するときにデバイス関連の障害を防ぐために、ESXi シェルから以下のコマンドを実行します。

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

以下に注意してください。

* これらのコマンドは、vSAN クラスター内の各 ESXi ホスト上で実行する必要があります。
* これらのコマンドの内容は、即時に有効になります。リブートは不要です。
* これらのコマンドでは、永続的な変更が行われ、リブート後もその構成のままになります。

詳しくは、VMware Knowledge Base のトピック[「Required vSAN and ESXi configuration for controllers based on the LSI 3108 chipset」 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://kb.vmware.com/s/article/2144936){: new_window} を参照してください。
