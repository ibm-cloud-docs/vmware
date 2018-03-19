---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# Instalando o VMware Tools - Linux

O VMware Tools é um conjunto de utilitários que melhora o desempenho do sistema operacional guest da máquina virtual e melhora o gerenciamento da máquina virtual. A instalação do VMware Tools no sistema operacional guest é vital. Embora o sistema operacional guest possa ser executado sem o VMware Tools, você perde funcionalidade e conveniência importantes.

O serviço é denominado `vmware-guestd` em guests Linux, FreeBSD e Solaris. O serviço `vmware-guestd` executa as tarefas a seguir no sistema operacional guest:

* Transmite mensagens do sistema operacional do host para o sistema operacional guest.
* Executa comandos no sistema operacional para encerrar ou reiniciar de forma limpa um sistema Linux, FreeBSD ou Solaris quando você seleciona operações de energia na Estação de Trabalho.
* Sincroniza o tempo no sistema operacional guest com o tempo no sistema operacional do host.
* Executa scripts que ajudam a automatizar operações do sistema operacional guest. Os scripts são executados quando o estado da energia da máquina virtual muda.

O serviço é iniciado quando o sistema operacional guest é iniciado.

Para instalar as ferramentas do VMware em um servidor Linux, clique com o botão direito no servidor apropriado em seu cliente vSphere, passe o mouse sobre **Guest** e clique em **Instalar/fazer upgrade de ferramentas do VMware**.

Esse link monta uma unidade de CD-ROM virtual que contém o rpm de ferramentas do VMware. Para instalar as ferramentas depois de montar a unidade de CD-ROM virtual, siga estas etapas:
1. Monte a unidade de CD-ROM usando o comando: `mount /dev/cdrom /mnt`
2. Verifique se o arquivo existe e está montado corretamente usando o comando `ls /mnt` no diretório montado. Você verá o arquivo `VMWareTools-4.0.0-208167.i386.rpm`. 
3. Execute o comando `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm`.
4. Execute o comando a seguir para configurar o VMware Tools para o kernel em execução: `/usr/bin/vmware-config-tools.pl`. **Nota:** é solicitado que você pressione **ENTER** uma vez durante as atualizações de configuração.
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**Nota:** não é necessário reiniciar a VM após instalar as ferramentas do VMware, no entanto, é recomendado.

Se as ferramentas do VMware foram instaladas corretamente, “OK“ será exibido em sua interface do cliente vSphere.
