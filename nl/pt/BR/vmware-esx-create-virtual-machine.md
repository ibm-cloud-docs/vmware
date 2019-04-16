---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Criando uma máquina virtual VMware ESX
{: #create-esx-vm}

Para criar uma nova máquina virtual, siga estas etapas.
{:shortdesc}

1. Clique com o botão direito no endereço IP do nó do host na área de janela Inventário do vSphere Client.
2. Selecione **Customizado** na janela de configuração.
3. Dê um nome apropriado a máquina virtual e clique em **Avançar**.
4. Selecione o local de Armazenamento para arquivos da máquina virtual e clique em **Avançar**.
5. Na **Versão da máquina virtual**, selecione **Máquina Virtual Versão 8**. <!-- since we are using vSphere instead of the Web Client to create it (in which case we would use version 11 instead).-->
6. Selecione o **Sistema operacional**.
7. Selecione o número de processadores virtuais (**página da CPU**) e a quantidade de **Memória** que você gostaria para criar a máquina virtual. **Nota:** será possível mudar o número de processadores e a memória posteriormente, se houver recursos disponíveis.
Na seção de rede, será necessário conectar dois NICs, com o NIC 1 sendo a rede privada e o NIC 2 sendo a rede pública. O tipo de adaptador será “Flexível”. Certifique-se de que **Conectar-se na ativação** esteja selecionado.
8. Mantenha a tela **Controlador SCSI** com o padrão ”LSI Logic Parallel”. Na tela **Selecionar um disco**, selecione **Criar um novo disco virtual**. A tela **Opções avançadas** e a tela **Pronto para concluir** também devem ser deixadas padrão. A criação de uma nova máquina virtual agora está concluída. 

Para começar a carregar sua mídia de instalação, clique no nome do servidor na lista de inventário. Em seguida, clique em **Editar configurações da máquina virtual** sob **Tarefas básicas**.

9. Com a **Unidade 1 de CD/DVD** selecionada, marque a caixa de seleção **Conectar-se na ativação** sob Status do dispositivo. Para especificar um arquivo ISO que está localizado em seu Armazenamento de dados, clique em **Procurar**.
10. Os arquivos ISO que são transferidos por upload para o Armazenamento de dados Storage1 padrão são selecionáveis aqui. Você também vê as pastas que contêm os arquivos de configuração/log (configurados durante a seção **Armazenamento de dados** da Etapa 3 do processo Criar uma nova máquina virtual) para todas as máquinas virtuais do servidor.

Depois de selecionar sua imagem ISO, você estará pronto para iniciar o processo de instalação do respectivo OS.

Para obter mais informações sobre como configurar uma rede de máquina virtual, consulte [Configurando uma rede da máquina virtual](/docs/infrastructure/virtualization/virtual-machine-network-setup.html){:new_window}.
