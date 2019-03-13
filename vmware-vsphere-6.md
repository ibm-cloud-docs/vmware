---

copyright:
  years: 1994, 2019
lastupdated: "2018-08-23"

keywords: vmware vcenter, vmware license, vsphere, vrealize, vsan, srm, nsx

subcollection: vmware

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# VMware licensing options 
{: #license-options-vmware}

VMware administrators can quickly realize cost-effective hybrid cloud characteristics by deploying into an {{site.data.keyword.BluSoftlayer_full}} enterprise-grade global cloud. A key {{site.data.keyword.BluSoftlayer_notm}} differentiator is that vSphere workloads and catalogs can be provisioned onto VMware vSphere environments within {{site.data.keyword.BluSoftlayer_notm}} data centers without modifying VMware VMs or guests. These deployments are made possible by using a common vSphere hypervisor and management/orchestration platform.

In addition to offering the vSphere 6 Enterprise Plus License, {{site.data.keyword.BluSoftlayer_notm}} offers monthly licensing for vCenter, NSX, vRealize, vSAN, and Site Recovery Manager (SRM).

## VMware vSphere
{: #vmware-vsphere-features}

**Intended Use:** Bare Metal Server virtualization OS platform that abstracts processor, memory, storage, and networking resources to create multiple virtual servers on a single physical server. Multiple physical servers can be clustered together to create a private cloud.

**User Interface:** vCenter Clients, VMware API, VMware CLI

**Features:**
* vMotion live migration
* High Availability
* Fault Tolerance
* Replication
* Nvidia GRID vGPU Virtualization
* Workload Capacity Optimization
* Distributed Resources Scheduler (DRS)
* Thin Provisioning
* Network I/O Control

## VMware vCenter
{: #vmware-vcenter-features}

**Intended Use:** To centralize the management of the compute resources within each vSphere host. While the vSphere hosts can be managed individually, placing them under the vCenter control enables the following capabilities:

**User Interface:** Web Client, Thick Client, VMware API, VMware CLI

**Features:**
* Centralized control and visibility for all aspects within managed vSphere hosts and guest virtual machines.
* Provides a single pane of glass interface view via the vCenter web client for compute network and storage management.
* Proactive Optimization. Enables allocation and optimization of resources for maximum efficiency across the vSphere hosts.
* Extended management function for other integrated add-ons and services such as NSX, vRealize, vSAN, and Site Recovery Manager (SRM).
* Monitoring, alerting, scheduling. Cloud admins can view events, alerts within the vCenter web client and configure scheduled actions.
* Automation engine. vCenter is the engine that performs the tasks that are given to it via the vSphere API web interface. VMware vRealize Automation and vRealize Orchestration are examples of applications that drive vCenter actions via the VMware API.

## VMware NSX
{: #vmware-nsx-features}

**Intended Use:** NSX offers Software-Defined Network (SDN) capabilities crucial to support the cloud platform operations.

**User Interface:** vCenter Clients, VMware API, VMware CLI

**Features:**
* Load Balancing
* Firewalls
* Routing
* Logical switches
* VPN
* VxLAN Segmentation / Tunnel Endpoints

## VMware vRealize
{: #vmware-vrealize-features}

**Intended Use:** The VMware vRealize Suite is an enterprise-ready, cloud management platform that you can use to manage a heterogeneous, hybrid cloud.

**User Interface:** vCenter Clients, VMware API, VMware CLI

**License Model:** Per processor per month

**Features:**
* vRealize Automation - Automated delivery of personalized infrastructure, applications, and custom IT services.
* vRealize Operations - Intelligent health, performance, capacity, and configuration management orchestration.
* vRealize Log Insight - Real-time log management and log analysis.
* vRealize Network Insight - Accelerated security management for applications and network infrastructures.

## VMware vSAN
{: #vmware-vsan-features}

**Intended Use:** VMware vSAN is a distributed storage technology that enables local storage drives on each vSphere host to be aggregated and pooled into a shared-nothing storage device that is accessible to all hosts in a vSAN cluster.

**User Interface:** vCenter Clients, VMware API, VMware CLI

**Features:**
* Distributed Host based storage
* Shared-nothing architecture
* Scales up to 64 nodes
* Low latency
* Configurable fault tolerance

## VMware Site Recovery Manager (SRM)
{: #vmware-srm-features}

**Intended Use:** VMware Site Recovery Manager (SRM) enables application availability and mobility across sites that are in private cloud environments. By taking full advantage of the encapsulation and isolation of virtual machines, Site Recovery Manager enables simplified automation of disaster recovery to meet recovery time objectives (RTOs). SRM also helps reduce costs that are associated with business continuity plans, and achieve low-risk, predictable results for recovery of a virtual environment.

**User Interface:** vCenter Clients, VMware API, VMware CLI

**Features:**
* Non-disruptive recovery testing
* Automated orchestration workflows
* Automated recovery of network and security settings
* Extensibility for custom automation
* Orchestrated cross-vCenter vMotion
* Centralized recovery plans
* Policy-based management
