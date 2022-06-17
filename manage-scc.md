---
copyright:
  years: 2020, 2022
lastupdated: "2022-06-17"

keywords: security and compliance for vmware, security for vmware, compliance for vmware,

subcollection: vmware

---

{:external: target="_blank" .external}
{:note: .note}
{:term: .term}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}


# Managing security and compliance with VMWare on IBM Cloud
{: #manage-security-compliance}


VMWare on {{site.data.keyword.BluSoftlayer_full}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to VMWare on {{site.data.keyword.BluSoftlayer_full}}
* Define rules for VMWare on {{site.data.keyword.BluSoftlayer_full}} that can help to standardize resource configuration


## Monitoring security and compliance posture with VMWare on {{site.data.keyword.BluSoftlayer_full}}
{: #monitor-vmware}

As a security or compliance focal, you can use the VMWare on {{site.data.keyword.BluSoftlayer_full}} [goals](#x2117978){: term} to help make sure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All of the goals for VMWare on {{site.data.keyword.BluSoftlayer_full}} are added to the {{site.data.keyword.cloud_notm}} Control Library profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic-security-compliance-getting-started)

### Available goals for VMWare on {{site.data.keyword.BluSoftlayer_full}}
{: #vmware-available-goals}

* Check whether certificates are automatically renewed before expiration
* Ensure that ordered bare metal servers are configured for UEFI/TXT modules and Secure Boot
* Ensure that bare metal servers include TPM/TXT modules when possible
* Ensure that bare metal servers have secure passwords and or configured with SSH keys
* Ensure that bare metal servers do not allow remote administration over the public network
* Ensure that bare metal servers are ordered with redundant power supplies for workload protection
* Ensure that bare metal servers are protected by firewall hardware
