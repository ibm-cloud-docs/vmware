---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-15"

keywords: upgrade vsphere

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Migrating and upgrading to VMware vSphere
{: migrate-upgrade-vsphere-6}

Expand or move your VMware cloud environments to any {{site.data.keyword.cloud}} data center quickly and easily by using the VMware management control panel. To migrate and upgrade vSphere workloads, use the following steps as a guide.
{: shortdesc}

1. Gather data and review the existing architecture:
   * Resource usage (CPU/Memory/Storage).
   * Track and project growth rates.
   * Identify upcoming future projects.
   * Determine what assigned vlans/subnets/etc are deployed (available in the control portal).
   * Find the self-defined RFC1918 (private) subnets in use for the solution.
1. Review the VMWare documentation and join the VMWare communities:
   * [VMware vSphere documentation](https://docs.vmware.com/en/VMware-vSphere/index.html){: external}
1. Update your admin team's training to support VMWare.
1. Plan and design a new architecture.
1. Select a data center that is based on compliance. Work with {{site.data.keyword.cloud}} sales to refine your candidate location that is based on availability of products and services.
1. Define your required VLANs and subnets (portable public and private IPs).
1. Design the vSphere servers:
   * Review the current IBM Cloud server catalog. Intel Xeon v3 Servers are recommended along with redundant uplinks, redundant power supplies, and RAID-1 for local (boot) disks.
   * Most customers with VMWare follow an N+1 hard capacity ceiling (all VMs can be comfortably allocated to servers with a single node removed (for maintenance/failure/etc).
   * Many customers want a higher "soft ceiling" of ~80% (80% capacity on the 'n' server configuration) compared to the more standard 60-75% due to the short turn around of compute.
   * External OS Licensing (such as Microsoft, Red Hat) might be needed for vSphere guests from an external vendor.
   * Review [Performance best practices for VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/vmware-perfbest-practices-vsphere6-0-white-paper.pdf){: external}
1. Design the vCenter Server:
   * Typically, a midsized virtual server instance is the entry point for small environments (8 vCPU + 16 GB RAM). While bare metal is used for larger environments.
   * vCenter can be deployed on a stand-alone virtual server instance Windows virtual machine as an OS add-on or as an appliance.
      * Reference Links:
         * [VMware vCenter Server performance and best practices](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/vmware-vcenter6-performance-white-paper.pdf){: external}
         * [Deploying and Configuring a vCenter Server Appliance (vCSA) with VMware vSphere](/docs/vmware?topic=vmware-config-vcsa)
1. Non-VMWare servers. Identify and plan for any non-VMWare servers (virtual or Bare Metal) that are needed.
1. Storage
   * Develop a storage plan for the environment. Endurance 2 IOPS/GB with snapshot space for virtualization is a good starting storage plan. If virtual databases or other high-performance applications are used, then the 4 IOPS/GB tier is a better fit. NFS storage is typically recommended.
   * Snapshot space is most commonly used as a secondary measure for point-in-time restores. 10% is a good starting place because the process is efficient and can be easily sized up.
1. Backups
   * Make sure that the existing backup strategy works. If a backup strategy does not exist, create one.
   * You can use your own backup solution. You can use the backup features that are included with vSphere Enterprise Plus licensing, optimized third-party solutions like Veeam, or traditional IBM Cloud r1soft backups.
1. Develop a migration strategy:
   * Review the existing DNS and IP configurations and shorten the TTL as needed.
   * Develop a plan for VMs to include Source host, destination host, source IPs, destination IPs, and associated DNS entries.
   * In most scenarios, it is best to migrate VM-by-VM and then update the public and private network configurations. When you move from older versions to newer versions, it is best to "rip and ship" the VM by shutting it down and performing a _detach/attach_ between the environments. If you are moving between locations, a long-distance vMotion is possible.
   * Develop testing plans for verification of the environment.
   * Coordinate a change and maintenance window with users. Individual VM maintenance windows can account for transfer of data, configuration of the VM, changing, and propagation of DNS, and time for troubleshooting.
1. Deploy the new environment:
   * Order the new vSphere and vCenter servers (and any other servers that you need).

      Make sure that the proper "unbonded" network uplinks are selected.
      {: note}

   * Order and configure the appropriate storage: [Architecture Guide for IBM File Storage for {{site.data.keyword.cloud}} with VMware](https://cloud.ibm.com/docs/FileStorage?topic=FileStorage-architectureguide)
   * Order the new VLANs and portable subnets (detailed architecture diagrams and justification might be required).
   * Configure vCenter to communicate the with vSphere servers and configure of the environment.
   * Take backups in the live environment.
   * Run the migration plan and associated test plans.
   * Implement backups in the new environment.
   * Operate the new environment.
   * Decommission the traditional environment.
