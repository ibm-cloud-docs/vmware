---
copyright:
  years: 1994, 2017
lastupdated: "2017-06-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 NSX Overview

VMware NSX&reg; is a software networking and security virtualization platform that delivers the operational model of a virtual machine for the network. Virtual networks reproduce the Layer2 - Layer7 network model in software, allowing complex multi-tier network topologies to be created and provisioned programmatically in seconds, without the need for additional {{site.data.keyword.BluSoftlayer_notm}} Private Networks. NSX also provides a new model for network security. Security profiles are distributed to and enforced by virtual ports and move with virtual machines.

NSX supports VMware's software-defined data center strategy. By extending the virtualization capabilities of abstraction, pooling and automation across all data center resources and services, the software-defined data center architecture simplifies and speeds the provisioning and management of compute, storage and networking resources through policy-driven automation. By virtualizing the network, NSX delivers a new operational model for networking that breaks through current physical network barriers and enables VMware and {{site.data.keyword.BluSoftlayer_notm}} to achieve better speed and agility with reduced costs.

NSX includes a library of logical networking services - logical switches, logical routers, logical firewalls, logical load balancers, logical VPN, and distributed security. You can create custom combinations of these services in isolated software-based virtual networks that support existing applications without modification, or deliver unique requirements for new application workloads. Virtual networks are programmatically provisioned and managed independent of {{site.data.keyword.BluSoftlayer_notm}} networking constructs. This decoupling from hardware introduces agility, speed, and operational efficiency that can transform datacenter operations. Benefits of NSX include the following features:
* DataCenter automation
* Self-service networking services
* Rapid application deployment with automated network and service provisioning
* Isolation of development, test, and production environments on the same bare metal infrastructure
* Single Account multi-tenant clouds

NSX can be configured through the vSphere Web Client, a command line interface (CLI), and REST API. The core network services offered by NSX are:

## Logical Switches
A cloud deployment or a virtual data center might have a variety of applications across multiple tenants. These applications and tenants require isolation from each other for security, fault isolation, and avoiding overlapping IP addressing issues. The NSX logical switch creates logical broadcast domains or segments (VXLAN vWires) to which an application or tenant virtual machine can be logically wired. This allows for flexibility and speed of deployment while still providing all the characteristics of a physical network's broadcast domains (VLANs) without physical Layer 2 sprawl. Logical switches allow for thousands of tenant networks to be provisioned onto a single {{site.data.keyword.BluSoftlayer_notm}} Private Network (VLAN). A logical switch is distributed and can span arbitrarily large compute clusters, even across pods within the same data center. This allows for virtual machine mobility within the datacenter without limitations of physical Layer 2 (VLAN) boundaries across pods.

## Logical Routers
Dynamic routing provides the necessary forwarding information between layer 2 broadcast domains (VXLAN vWires/Logical Switches), thereby allowing you to decrease layer 2 broadcast domains and improve network efficiency and scale. NSX extends this intelligence to where the workloads reside for providing East-West routing functions. This allows more direct virtual machine to virtual machine communication without the costly or timely need to extend hops. At the same time, NSX also provides North-South connectivity inbound/outbound of {{site.data.keyword.BluSoftlayer_notm}} data centers , thereby enabling tenants to access public networks securely and efficiently.

## Logical Firewall
Logical Firewall provides security mechanisms for dynamic virtual data centers. The Distributed Firewall component of a NSX Logical Firewall allows you to segment virtual datacenter entities, like virtual machines, based on VM names and attributes, user identity, vCenter objects like DataCenters and hosts, as well as traditional networking attributes like IP addresses, VLANs, etc. The Edge Firewall component helps you achieve key perimeter security needs such as building DMZs based on IP/VLAN constructs, tenant to tenant isolation in multi-tenant virtual data centers, Network Address Translation (NAT), VPNs, and User based SSL VPNs. Edge Firewalls can be leveraged in combination with or in place of Vyatta & Fortinet services from {{site.data.keyword.BluSoftlayer_notm}} for perimeter protection. The Firewall Flow Monitoring feature displays network activity between virtual machines at the application protocol level. You can use this information to audit network traffic, define and refine firewall policies, and identify threats to your network.

## Logical Virtual Private Networks (VPN)s
SSL VPN-Plus allows remote users to access private corporate applications. IPSec VPN offers site-to-site connectivity between an NSX Edge instance and remote sites (VMware running on {{site.data.keyword.BluSoftlayer_notm}}). L2 VPNs allow you to extend your datacenter by allowing virtual machines to retain network connectivity across geographical boundaries and across {{site.data.keyword.BluSoftlayer_notm}} data centers and your local VMware environment.

## Logical Load Balancer
The NSX Edge load balancer enables network traffic to follow multiple paths to a specific destination. It distributes incoming service requests evenly among multiple servers in such a way that the load distribution is transparent to users. Load balancing thus helps in achieving optimal resource utilization, maximizing throughput, minimizing response time, and avoiding overload. NSX Edge provides load balancing up to Layer 7.

## Service Composer
Service Composer helps you provision and assign network and security services to applications in a virtual infrastructure. These services can be mapped and applied to virtual machines in the security groups. Data Security provides visibility into sensitive data stored within your organization's virtualized and cloud environments including {{site.data.keyword.BluSoftlayer_notm}}. Based on the violations reported by NSX Data Security, you can ensure that sensitive data is adequately protected and assess compliance with regulations around the world.

## NSX Extensibility
VMware partners can integrate their network service solutions with the NSX platform, which enables customers to have an integrated experience across VMware products and partner solutions. Data center operators can provision complex, multi-tier virtual networks in seconds, independent of the underlying network topology or components from {{site.data.keyword.BluSoftlayer_notm}}.

## NSX Core Components
This section describes the core NSX components that would be deployed on {{site.data.keyword.BluSoftlayer_notm}}. These components can be configured/managed through the vSphere Web Client, a command line interface (CLI), and REST API. VMware NSX requires a functional {{site.data.keyword.BluSoftlayer_notm}} environment with at least vSphere & vCenter version 6 deployed. All components described in this section are deployed as VMware Appliance VMs running on {{site.data.keyword.BluSoftlayer_notm}}. NSX Components are not supported as  Virtual Server Instances (VSI). It is recommended that guidance be followed to create a dedicated ESX Management Cluster, additionally an Edge Services Cluster may also be required as will be discussed further in this document.

<!-- ![Figure 1](images/vmware6_nsx_overview_1.png)-->

## NSX Manager
The NSX Manager is the centralized network management component of NSX, and is installed as a virtual appliance on an ESX host in your vCenter Server environment. {{site.data.keyword.BluSoftlayer_notm}} Architecture recommends this VM be deployed on a dedicated Management ESX Cluster. One NSX Manager maps to a single vCenter Server environment and multiple NSX Edge, vShield Endpoint, and NSX Data Security instances.

## NSX vSwitch
NSX vSwitch is the software that operates on {{site.data.keyword.BluSoftlayer_notm}} ESX hosts to form a software abstraction layer between servers and the physical network. As the demands on DataCenters continue to grow and accelerate, requirements related to speed and access to the data itself continue to grow as well. In most infrastructures, virtual machine access and mobility usually depend on physical networking infrastructure and the physical networking environments they reside in. This can force virtual workloads into less than ideal environments due to potential layer 2 or layer 3 boundaries, such as being tied to specific {{site.data.keyword.BluSoftlayer_notm}} Private Networks (VLANs) in specific pods. NSX vSwitch allows you to place these virtual workloads on any available infrastructure in the data center, regardless of the underlying physical network infrastructure. This not only allows increased flexibility and mobility, but increased availability and resilience.

## NSX Controller 
NSX controller is an advanced distributed state management system that controls virtual networks and VXLAN overlay transport tunnels. NSX controller is the central control point for all logical switches within a network and maintains information of all virtual machines, hosts, logical switches, and VXLANs. The controller supports three logical switch control plane modes, Multicast, Unicast, and Hybrid. These modes decouple NSX from the physical network. {{site.data.keyword.BluSoftlayer_notm}} requires Unicast mode as {{site.data.keyword.BluSoftlayer_notm}} Private Networks (VLANs) do not offer IGMP services for Multicast or Hybrid mode. The NSX Controller(s) will utilize Unicast mode with virtual tunnel endpoints (VTEPS) to provide mac learning and other functions to allow VXLAN Broadcast, Unknown unicast, and Multicast (BUM) traffic within a logical switch. The unicast mode replicates all the BUM traffic locally on the host and requires no physical network configuration outside of Layer 3 connectivity between VTEPS. NSX Controllers are deployed by the NSX Manager as a minimum set of 3 controller nodes, as well as various other nodes to support (distributed) Layer 3 routing services. All of the nodes are deployed as virtual machines and are managed by the NSX Manager on an ESX Management Cluster at {{site.data.keyword.BluSoftlayer_notm}}.

## NSX Edge
NSX Edge provides network edge security and gateway services to isolate a virtualized networks. You can install an NSX Edge either as a logical (distributed) router or as a services gateway. The NSX Edge logical (distributed) router provides East-West distributed routing with tenant IP address space and data path isolation. Virtual machines or workloads that reside on the same host on different subnets can communicate with one another without having to traverse a traditional routing interface. The NSX Edge Gateway connects isolated stub networks to shared (uplink) networks by providing common gateway services such as DHCP, VPN, NAT, dynamic routing, and Load Balancing. Common deployments of NSX Edge include in the DMZ, VPN Extranets, and multi-tenant cloud environments where the NSX Edge creates virtual boundaries for each tenant.
