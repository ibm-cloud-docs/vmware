---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-10"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Criando uma máquina virtual com o VMware vSphere 6 

1. Clique com o botão direito no endereço IP do nó do host na área de janela Inventário do vSphere Client.
2. Na janela de configuração, selecione **Customizado**.
3. Dê um nome apropriado a máquina virtual e clique em **Avançar**.
4. Selecione o local de Armazenamento para arquivos da máquina virtual e clique em **Avançar**.
* O menu Versão da máquina virtual fornece a opção para usar tipos de cluster diferentes. Como esse é um novo cluster e você não precisa de suporte para versões mais antigas, selecione **Máquina Virtual Versão 8**. **Nota:** se você usar o Web client para criar um cluster, use a versão 11.
5. Selecione o tipo **Sistema operacional**.
6. Configure o número de processadores virtuais (na página CPUs) e clique em **Avançar**
  1. **Nota:** será possível mudar o número de CPUs posteriormente, se houver recursos disponíveis.
7. Configure a quantidade de memória desejada para a máquina virtual. Clique em **Avançar**
  1. **Nota:** será possível mudar a quantidade de memória posteriormente, se houver recursos disponíveis.
8. Na seção de rede, é necessário se conectar a dois NICs. O NIC 1 é para a rede privada e o NIC 2 é para a rede pública. O tipo de adaptador é “Flexível”. Certifique-se de que a caixa de seleção “Conectar na ativação“ esteja selecionada.
9. Deixe a tela Controlador SCSI com o padrão “LSI Logic Parallel“. Na tela Selecionar um disco, selecione **Criar um novo disco virtual**. Mantenha as configurações padrão na tela **Opções avançadas** e na tela **Pronto para concluir**. Sua nova máquina virtual agora está criada. Para começar a carregar sua mídia de instalação, clique no nome do servidor na lista de inventários e clique em **Editar configurações da máquina virtual** sob Tarefas básicas.
<!--* false-->
10. Com a Unidade 1 de CD/DVD selecionada, selecione **Conectar-se na ativação** sob Status do dispositivo. Para especificar um arquivo ISO que está localizado em seu Armazenamento de dados, clique em **Procurar**.
* Os arquivos ISO que são transferidos por upload para o Armazenamento de dados Storage1 padrão são selecionáveis aqui. Você também vê as pastas que contêm os arquivos de configuração/log (configurados durante a seção Armazenamento de dados da Etapa 3 do processo Criar uma nova máquina virtual) para todas as máquinas virtuais do servidor.
11. Depois de selecionar sua imagem ISO, você estará pronto para iniciar o processo de instalação do respectivo OS.
* Após sua VM guest estar funcionando com êxito, se suportado, instale o [VMWare Tools ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://kb.vmware.com/s/article/1014294){: new_window}.
* Para obter mais informações sobre as instruções de rede, consulte [Configurando uma rede da máquina virtual](/docs/infrastructure/virtualization/virtual-machine-network-setup.html).
