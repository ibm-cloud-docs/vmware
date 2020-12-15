---
copyright:
  years: 2020
lastupdated: "2020-12-15"

keywords: security and compliance for vmware, security for vmware*, compliance for vmware,

subcollection: vmware

---

{:external: target="_blank" .external}
{:note: .note}
{:term: .term}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}


# Managing security and compliance with *service_name*
{: #manage-security-compliance}

<!-- Name this file `manage-scc.md` and place it in the "Enhancing security" topic group. -->

VMWare on {{site.data.keyword.BluSoftlayer_full}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

<!--Add the following sections as your service onboards to the Security and Compliance Center. You might have only monitoring or you might also have configuration enforcement. Also, if you only have one of the options, be sure to remove the bulleted list and write the following section as a sentence.-->

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to VMWare on {{site.data.keyword.BluSoftlayer_full}}.
* Define rules for VMWare on {{site.data.keyword.BluSoftlayer_full}} that can help to standardize resource configuration.


## Monitoring security and compliance posture with VMWare on {{site.data.keyword.BluSoftlayer_full}}
{: #monitor-vmware}

As a security or compliance focal, you can use the VMWare on {{site.data.keyword.BluSoftlayer_full}} [goals](#x2117978){: term} to help make sure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All of the goals for VMWare on {{site.data.keyword.BluSoftlayer_full}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
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

## Governing VMWare on {{site.data.keyword.BluSoftlayer_full}} resource configuration
{: #govern-service_name}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of *service_name* that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the data that you can use to create a rule for VMWare on {{site.data.keyword.BluSoftlayer_full}}, review the following table.

| Resource kind | Property | Operator | Value | Description |
|---------------|----------|---------------|-------|-------------|
| *instance* | *private_network_only* | *is_true* <br>*is_false* | - | *Indicates whether access to a Certificate Manager instance is allowed only through a private network. |
| <resource_kind> | <property_name> | <operator> | <value> | <description> |
{: caption="Table 1. Rule properties for VMWare on {{site.data.keyword.BluSoftlayer_full}}" caption-side="top"}

To learn more about config rules, check out [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-rule).
