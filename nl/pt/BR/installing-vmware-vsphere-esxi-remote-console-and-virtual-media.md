---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Instalando o VMware vSphere ESXi por meio do console remoto e da mídia virtual
{: #installing-vsphere-esxi}

A implementação do ESX por meio da mídia de instalação é semelhante em todas as versões e pode ser usada em cenários BYOL (trazer sua própria licença).

## Requisitos
* Uma instância de máquina virtual (VM) que tem acesso à Rede Privada [tal como uma instância de computação em nuvem (VSI) que é instalada com o Windows ou Linux, com um navegador ativado para Java, acessível por meio de vpn.softlayer.com ou de IP público]. O VSI deve estar na mesma rede privada que os endereços de Intelligent Platform Management Interface (IPMI) do servidor estão localizados.
* Uma cópia do VMware ESXi VIM Installer ISO.

<!--## Steps -->

## Conectando-se ao IPMI
1. Faça upload do VMware ISO para o VSI que foi especificado em Requisitos (os VSIs devem ter acesso à web pública.)
2. Reúna o endereço IPMI e as informações de login do portal do cliente.
3. Selecione **Dispositivos** > **Lista de dispositivos** > **[Servidor]** > e a guia **Gerenciamento remoto**.
4. Desktop remoto (RDP) ou X remoto para o VSI que está armazenando a imagem do ESXi.
5. Abra um navegador da web na sessão RDP e insira o endereço IPMI que você coletou na Etapa 2.
6. Efetue login no console do IPMI com as credenciais que também foram localizadas na Etapa 2 (geralmente raiz).
* Anote o nível de acesso do usuário ao IPMI. Ele pode ser Administrador. Você poderá ter um problema ao montar seu armazenamento remoto se ele for configurado como **Operador**. Registre um chamado de suporte para elevar suas credenciais do IPMI se você não puder montar a mídia.
7. Confirme se você está na página de login inicial e clique em **Controle remoto** > **Redirecionamento do console** > **Ativar console**.

## Anexando o ISO
1. No visualizador da máquina virtual baseada em kernel (KVM), selecione **Mídia virtual** > **Armazenamento virtual**. Sua versão do sistema operacional e de Java pode requerer que você permita o acesso para iniciar o visualizador baseado em Java.
2. Clique na guia **CDROM e ISO** na janela Armazenamento virtual. Para o Tipo de Unidade Lógica, selecione **Arquivo ISO** e clique em **Abrir imagem**.
3. Acesse o ISO ESXi e clique em **OK**. Em seguida, clique em **Conectar**.
4. Após a ISO ser conectado à sessão, clique em **OK**.
* Volte para a página da web do IPMI e clique em **Remoto** > **Controle** > **Reconfigurar servidor** > **Executar ação** para reiniciar o servidor.

### Instalando e concluindo a configuração de rede
1. Instale o ESXi.
* Após a instalação ser concluída, certifique-se de **Desconectar** o ISO para que você possa reiniciar o servidor.
2. Reinicie o servidor.
3. Configure o endereço IP do servidor após ele reiniciar.
4. Reúna os detalhes da guia Configuração do dispositivo.

Agora é possível gerenciar o host ESXi.

Para obter mais informações sobre como configurar o armazenamento de bloco de resistência ou de desempenho, consulte [Fornecendo e gerenciando o armazenamento de bloco](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Para obter mais informações sobre como configurar o QuantaStor, consulte [Guia de arquitetura do QuantaStor](architecture-guide-quantastor-vmwaresoftlayer.html).
