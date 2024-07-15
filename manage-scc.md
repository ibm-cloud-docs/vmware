---
copyright:
  years: 2020, 2024
lastupdated: "2024-07-15"

keywords: security and compliance for vmware, security for vmware, compliance for vmware,

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance with VMWare on {{site.data.keyword.cloud}}
{: #manage-security-compliance}

VMWare on {{site.data.keyword.cloud}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to VMWare on {{site.data.keyword.cloud}}
* Define rules for VMWare on {{site.data.keyword.cloud}} that can help to standardize resource configuration

## Monitoring security and compliance posture with VMWare on {{site.data.keyword.cloud}}
{: #monitor-vmware}

As a security or compliance focal, you can use the VMWare on {{site.data.keyword.cloud}} to help make sure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All of the goals for VMWare on {{site.data.keyword.cloud}} are added to the {{site.data.keyword.cloud_notm}} Control Library but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

### Available goals for VMWare on {{site.data.keyword.cloud}}
{: #vmware-available-goals}

* Check whether certificates are automatically renewed before expiration
* Make sure that ordered bare metal servers are configured for UEFI/TXT modules and Secure Boot
* Make sure that bare metal servers include TPM/TXT modules when possible
* Make sure that bare metal servers have secure passwords and or configured with SSH keys
* Make sure that bare metal servers do not allow remote administration over the public network
* Make sure that bare metal servers are ordered with redundant power supplies for workload protection
* Make sure that bare metal servers are protected by firewall hardware
