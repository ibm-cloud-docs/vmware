---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Instalando o EVault Backup Client for VMware

A instalação do EVault Backup Client em um servidor VMware pode ser feita por meio de uma série de comandos no shell ou terminal no servidor ESX de destino. Esse procedimento descreve as etapas necessárias para instalar o EVault Backup Client em seu servidor VMware:
{:shortdesc}

Para instalar o Agente, faça download e copie o pacote `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` para o ESX Server de destino usando o comando a seguir:

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**Nota:** deve-se executar as etapas a seguir localmente no ESX Server de destino.

1. Extraia os arquivos do pacote. Para fazer isso, use este comando (em que “PACKAGENAME“ poderia ser “Agent-VMware ESX-Server-6.71“):<br/>`tar xvfz PACKAGENAME.tar.gz`
2. Acesse o diretório no qual você extraiu o pacote.
3. Execute o script de instalação:<br />`# ./install.sh`<br/><br/>
**Nota:** o script de instalação solicitará interativamente as informações de configuração, tais como o registro da web (endereço, número da porta e autenticação) e o nome do arquivo de log.

Insira o nome de usuário WebCC para esse servidor.

4. Insira o **Nome de Usuário do EVault Backup** como a entrada para o prompt que solicita o nome de usuário WebCC. Consulte o procedimento [Visualizar Detalhes de Armazenamento do EVault Backup](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal) para obter instruções para visualizar o Nome de Usuário do EVault Backup.
5. Insira a Senha do EVault Backup como a entrada para o prompt que solicita a senha do WebCC.
6. Quando a instalação for concluída, uma mensagem de conclusão será exibida e o daemon do agente estará em execução.


Outras notas de instalação:<br/>
O Install.log estará no diretório de instalação se a instalação for bem-sucedida.<br/>
Por exemplo: `/opt/BUAgent/Install.log`

Se a instalação falhar e retroceder, o log de instalação estará no `<Installation Failure directory>.`<br/>
Se ela falhar e não retroceder, o log de instalação estará no `<Installation Kit directory>`.<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
Certifique-se de que você esteja conectado à VPN do {{site.data.keyword.BluSoftlayer_full}} para visualizar o link acima. Para obter mais informações sobre a conexão com a VPN do IBM Cloud, consulte [Ativar acesso à rede privada da infraestrutura do IBM Cloud](/docs/customer-portal/getting-started.html#enable-private-network)).
