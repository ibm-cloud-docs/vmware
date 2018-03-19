---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  Migrando e fazendo upgrade para o VMware vSphere 6

Expanda ou mova seus ambientes de nuvem VMware para qualquer data center do {{site.data.keyword.BluSoftlayer_full}} de maneira rápida e fácil utilizando o painel de controle de gerenciamento do VMware. Para migrar e fazer upgrade de cargas de trabalho do vSphere, use as etapas a seguir como um guia.
{:shortdesc}

1. Reúna dados.
2. Revise a arquitetura existente:
  1. Utilização de recurso (CPU/Memória/Armazenamento).
  2. Controle e projete as taxas de crescimento.
  3. Identifique os projetos futuros.
  4. Determine quais vlans/sub-redes/etc designadas estão implementadas (disponível no portal de controle).
  5. Localize as sub-redes RFC1918 (privadas) autodefinidas em uso para a solução.
3. Revise a documentação do VMWare 6 e participe das comunidades do VMWare:
  1. [Documentação do VMware vSphere ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [VMware Technology Network ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://communities.vmware.com/welcome){: new_window}
4. Atualize o treinamento da equipe de seu administrador para suportar VMWare 6.
5. Planeje e projete uma nova arquitetura.
6. Selecione um [data center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window} que seja baseado em conformidade. Trabalhe com o IBM Cloud Sales para refinar seu local candidato com base na disponibilidade de produtos/serviços.
7. Defina suas VLANs e sub-redes necessárias (IPs públicos e privados móveis).
8. Projete os servidores vSphere:
  1. Revise o catálogo do servidor atual do IBM Cloud. São recomendados servidores Intel Xeon v3 juntamente com uplinks redundantes, fontes de alimentação redundantes e discos RAID-1 para local (inicialização).
  2. A maioria dos clientes com VMWare segue um limite de capacidade física N+1 (todas as VMs podem ser alocadas confortavelmente em servidores com um único nó removido (para manutenção/falha/etc).
  3. Muitos clientes desejam um "limite temporário" mais alto de ~80% (80% de capacidade na configuração do servidor 'n') em comparação com o padrão máximo de 60-75% devido ao pequeno ajuste de cálculo.
  4. Pode ser necessário um licenciamento de S.O. externo (como Microsoft, Red Hat) para os guests do vSphere de um fornecedor externo.
  5. Revise [Melhores práticas para desempenho do VMware vSphere 6.0 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window}
9. Projete o vCenter Server:
  1. Geralmente, uma Instância de Servidor Virtual (VSI) de médio porte é o ponto de entrada para ambientes pequenos (8 vCPU + 16 GB de RAM). Enquanto o Bare Metal é usado para ambientes maiores.
  2. O vCenter pode ser implementado em uma máquina virtual Windows VSI independente como um complemento do S.O. ou como um dispositivo.
    1. Links de referência:
        * [Requisitos do vCenter Server 6.0 para instalação ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://kb.vmware.com/s/article/2107948){: new_window}
        * [Desempenho e melhores práticas do VMware vCenter Server ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}
        * [Implementando e configurando um vCenter Server Appliance (vCSA) com o VMware vSphere 6](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. Servidores não VMWare: identifique quaisquer servidores não VMWare (virtuais ou Bare Metal) que possam ser necessários e planeje adequadamente.
11. Armazenamento:
  1. Desenvolva um plano de armazenamento para o ambiente. 2 IOPS/GB de resistência com espaço de captura instantânea para virtualização é um bom plano de armazenamento inicial, mas se bancos de dados virtuais ou outros aplicativos de alto desempenho forem usados, a camada 4 IOPS/GB será mais adequada. O armazenamento NFS geralmente é recomendado.  
  2. A matriz de seleção pode ser localizada em [Armazenamento para usar com VMware Systems](select-storage-option-use-vmware.html).
  3. O espaço de captura instantânea é mais comumente usado como uma medida secundária para restaurações point-in-time. 10% é um bom ponto de início porque o processo é muito eficiente e pode ser facilmente aumentado.
12. Backups:
  1. Certifique-se de que a estratégia de backup existente funcione. Se uma estratégia de backup não existir, será necessário criá-la.
  2. É possível usar sua própria solução de backup. É possível usar os recursos de backup que são incluídos com o licenciamento do vSphere Enterprise Plus, soluções otimizadas de terceiros como VEEAM ou backups r1soft tradicionais do IBM Cloud.
13. Desenvolva uma estratégia de migração:
  1. Revise [Melhores práticas para instalar ou fazer upgrade para o ESXi 6.0 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://kb.vmware.com/s/article/2109712){: new_window}.
  2. Revise as configurações de DNS e/ou IP existentes e encurte a TTL conforme necessário.
  3. Desenvolva um plano para VMs para incluir o host de origem, o host de destino, os IPs de origem, os IPs de destino e as entradas DNS associadas.
  4. Na maioria dos cenários, é melhor migrar VM por VM e, em seguida, atualizar as configurações de rede pública e privada. Quando você move de versões mais antigas para versões mais recentes, geralmente é melhor simplesmente "reinicializar" a VM encerrando-a e executando um _detach/attach_ entre os ambientes. Se você está movendo entre locais, é possível um vMotion de longa distância.
  5. Desenvolva planos de teste para verificação do ambiente.
  6. Coordene uma janela de mudança/manutenção com usuários. As janelas de manutenção de VM individuais podem contar para transferência de dados, configuração da VM, mudança e propagação de DNS, bem como o tempo para resolução de problemas.
14. Implemente o novo ambiente:
  1. [Introdução ao VMware vSphere 6](vmware-vsphere-6-getting-started.html).
  2. Solicite os novos servidores vSphere e vCenter (bem como quaisquer outros servidores que você precisar).
      **Nota:** assegure-se de que os uplinks de rede "ilimitados" adequados sejam selecionados.
  3. Solicite e configure o armazenamento apropriado: [Guia de arquitetura do IBM File Storage for IBM Cloud com o VMware](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html)
  4. Solicite as novas VLANs e sub-redes móveis (diagramas de arquitetura detalhados e justificativa podem ser necessários).
  5. Configure o vCenter para se comunicar com os servidores vSphere e configure o ambiente.
  6. Faça backups no ambiente de produção.
  7. Execute o plano de migração e os planos de teste associados.
  8. Implemente os backups no novo ambiente.
  9. Opere o novo ambiente.
  10. Desative o ambiente anterior.
