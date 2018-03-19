---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# iSCSI an VMWare ESXi anhängen

Das Anhängen von iSCSI an VMWare ESXi kann mit wenigen Schritten und den Details des Servers und des Speicherknotens durchgeführt werden.
{:shortdesc}

1. Melden Sie sich bei vSphere mit der primären privaten IP-Adresse als Rootbenutzer (**root**) und mit dem zugehörigen Kennwort an.
* Klicken Sie auf der Begrüßungsseite auf die Registerkarte **Konfiguration**.
* Klicken Sie auf **Speicheradapter** und anschließend auf **Hinzufügen...**.
* Klicken Sie auf **OK**, um den Software-iSCSI-Adapter hinzuzufügen.
* Klicken Sie zur Bestätigung auf **OK**.
* Nach der Aktualisierung wird der neue iSCSI-Adapter aufgelistet.
* Klicken Sie im unteren Fensterbereich auf **Eigenschaften**.
* Klicken Sie im Fenster 'Eigenschaften' auf **Konfigurieren** im unteren Fensterbereich und geben Sie für **Name** den IQN des Servers an, wie auf der Seite für die Speichereinheit bei den autorisierten Hosts aufgelistet.
* Klicken Sie auf die **Registerkarte 'Dynamische Erkennung'** und anschließend auf **Hinzufügen...**.
* Der iSCSI-Server wird als Ziel-IP-Adresse der Speichereinheit angegeben. Klicken Sie auf die Schaltfläche **CHAP...**.
* Wählen Sie **CHAP verwenden** aus und wählen Sie **Vom übergeordneten Element übernehmen** aus. Geben Sie den Wert für **Benutzername** ein, wie auf der Seite für die Speichereinheit bei den autorisierten Hosts aufgelistet.
* Wählen Sie **CHAP nicht verwenden** im Abschnitt für gegenseitige CHAP-Authentifizierung aus und klicken Sie anschließend auf **OK**.
* Die Einheit wird nun im Fenster 'Dynamische Erkennung' angezeigt. Klicken Sie auf **Schließen**.
* Bestätigen Sie das erneute Scannen der Speichereinheiten.
* Danach wird die Einheit im unteren Fensterbereich grau und als nicht angehängt dargestellt.
* Klicken Sie mit der rechten Maustaste auf den Namen der Einheit und wählen Sie **Anhängen** aus.
* Klicken Sie auf das Menü **Datenspeicher** in der linken Spalte und anschließend auf **Speicher hinzufügen** und wählen Sie **Disk/LUN** aus.
* Klicken Sie auf die Einheit mit der Angabe 'iqn.'.
* Wählen Sie die gewünschte Dateisystemversion aus, klicken Sie auf **Weiter** und fahren Sie anschließend mit dem Assistenten fort.
* Nachdem der Assistent abgeschlossen ist, können Sie iSCSI nach Bedarf für den Host und für die VMs verwenden, die Sie erstellen.



Beim Anhängen einer iSCSI-Einheit für den Datenübertragungsservice wird das gleiche Verfahren verwendet. Hierbei müssen Sie die IQN jedoch vom Server abrufen. Führen Sie die folgenden Schritte in der ESXi-Konsole aus:

Als Erstes müssen Sie die Einheit abrufen:

`esxcfg-scsidevs -a | grep iSCSI`

Anschließend müssen Sie den IQN abrufen (in diesem Beispiel ist 'vmhba33' die iSCSI-Einheit):

`vmkiscsi-tool -I -l vmhba33`
