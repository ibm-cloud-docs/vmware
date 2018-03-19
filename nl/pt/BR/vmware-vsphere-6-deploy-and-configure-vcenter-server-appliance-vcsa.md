---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Implementando e configurando um vCenter Server Appliance (vCSA) com o VMware vSphere 6  

Use as etapas a seguir para implementar um VMware vCenter Server Appliance.
{:shortdesc}

**Pré-requisitos**
* Sistema Windows com um navegador compatível instalado
  * Internet Explorer / Firefox / Chrome
* Hosts vSphere com recursos adequados para suportar um VMware vCenter Server Appliance
  * Para obter mais informações sobre recursos do sistema necessários, consulte [Requisitos mínimos para o VMware vCenter Server 6.0 Appliance ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://kb.vmware.com/s/article/2106572){: new_window}.
* Imagem ISO do vCSA
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* Capacidade para montar um ISO
* Sessão de VPN com acesso à rede privada do IBM Cloud

**Implementando e configurando um vCenter Server Appliance**

1. Monte o vCenter Server Appliance (vCSA) ISO.
2. Abra o vcsa-setup.html em um navegador compatível.
3. Revise e aceite a instalação do plug-in do VMware Client Integration.
4. Clique em **Permitir**
5. Clique em **Instalar**
6. Revise e aceite os termos do contrato de licença e clique em **Avançar**.
7. Insira o FQDN ou endereço IP privado e o nome de usuário e a senha do Host VMware que você gostaria para instalar o vCSA. Clique em **Avançar**.
8. Clique em **Sim** para aceitar o aviso de certificado.
9. Insira um nome de dispositivo apropriado e a senha do S.O. e clique em **Avançar**.
10. Para o tipo de implementação, selecione 'Instalar o vCenter Server com um Controlador de serviços de Plataforma Integrado', em seguida, clique em **Avançar**.
11. Clique em 'Criar um domínio de SSO' e clique em **Avançar**. <!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. Escolha um tamanho do dispositivo e clique em **Avançar**.
13. Selecione um armazenamento de dados e clique em **Avançar**.
14. Selecione 'Usar um banco de dados integrado (PostgreSQL)' e clique em **Avançar*.
15. Defina suas configurações de rede inserindo as informações a seguir:
  1. Rede
  * Família de endereços IP
  * Tipo de rede
  * Endereço de rede
  * Nome do sistema
  * Máscara de sub-rede
  * Gateway de rede
  * Servidores DNS de rede
      * Para obter mais informações, consulte [Quais são os resolvedores de DNS locais](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-).
  * Configure a sincronização de tempo
  * Clique em **Avançar**
16. Revise as configurações, em seguida, clique em **Concluir**. Sua instância do vCSA é provisionada.

