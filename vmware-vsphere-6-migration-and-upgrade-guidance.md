---

copyright:
  years: 2017, 2022
lastupdated: "2022-09-15"

keywords: upgrade vsphere 

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Migrating and upgrading to VMware vSphere
{: migrate-upgrade-vsphere-6}

Expand or move your VMware cloud environments to any {{site.data.keyword.BluSoftlayer_full}} data center quickly and easily by using the VMware management control panel. To migrate and upgrade vSphere workloads, use the following steps as a guide.
{: shortdesc}

1. Gather data.
2. Review the existing architecture:
   1. Resource utilization (CPU/Memory/Storage).
   2. Track and project growth rates.
   3. Identify upcoming future projects.
   4. Determine what assigned vlans/subnets/etc are deployed (available in the control portal).
   5. Find the self-defined RFC1918 (private) subnets in use for the solution.
3. Review the VMWare documentation and join the VMWare communities:
   - [VMware vSphere documentation](https://docs.vmware.com/en/VMware-vSphere/index.html){: external}
   - [VMware Technology Network](https://communities.vmware.com/welcome){: external}
4. Update your admin team's training to support VMWare.
5. Plan and design a new architecture.
6. Select a data center that is based on compliance. Work with {{site.data.keyword.cloud}} sales to refine your candidate location based on availability of products and services.
7. Define your required VLANs and subnets (portable public and private IPs).
8. Design the vSphere Servers:
   1. Review the current IBM Cloud server catalog. Intel Xeon v3 Servers are recommended along with redundant uplinks, redundant power supplies, and RAID-1 for local (boot) disks.
   2. Most customers with VMWare follow an N+1 hard capacity ceiling (all VMs can be comfortably allocated to servers with a single node removed (for maintenance/failure/etc).
   3. Many customers want a higher "soft ceiling" of ~80% (80% capacity on the 'n' server configuration) compared to the more standard 60-75% due to the short turn around of compute.
   4. External OS Licensing (such as Microsoft, Red Hat) might be needed for vSphere guests from an external vendor.
   5. Review [Performance Best Practices for VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/vmware-perfbest-practices-vsphere6-0-white-paper.pdf){: external}
9. Design the vCenter Server:
   1. Typically, a midsized virtual server instance is the entry point for small environments (8 vCPU + 16 GB RAM). While bare metal is used for larger environments.
   2. vCenter can be deployed on a stand-alone virtual server instance Windows virtual machine as an OS add-on or as an appliance.
      * Reference Links:
         - [vCenter Server requirements for installation](https://kb.vmware.com/s/article/2107948){: external}
         - [VMware vCenter Server Performance and Best Practices](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/vmware-vcenter6-performance-white-paper.pdf){: external}
         - [Deploying and Configuring a vCenter Server Appliance (vCSA) with VMware vSphere](/docs/vmware?topic=vmware-config-vcsa)
10. Non-VMWare servers. Identify and plan for any non-VMWare servers (virtual or Bare Metal) that are needed.
11. Storage
   1. Develop a storage plan for the environment. Endurance 2 IOPS/GB with snapshot space for virtualization is a good starting storage plan, but if virtual databases or other high-performance applications are used, then the 4 IOPS/GB tier is a better fit.  NFS storage is typically recommended.  
   2. Snapshot space is most commonly used as a secondary measure for point-in-time restores. 10% is a good starting place because the process is efficient and can be easily sized up.
12. Backups
   1. Make sure that the existing backup strategy works. If a backup strategy does not exist, create one.
   2. You can use your own backup solution. You can use the backup features that are included with vSphere Enterprise Plus licensing, optimized third-party solutions like VEEAM, or traditional IBM Cloud r1soft backups.
13. Develop a migration strategy:
   1. Review [Best practices to install or upgrade to ESXi](https://kb.vmware.com/s/article/2109712){: external}.
   2. Review the existing DNS and IP configurations and shorten the TTL as needed.
   3. Develop a plan for VMs to include Source host, destination host, source IPs, destination IPs, and associated DNS entries.
   4. In most scenarios, it is best to migrate VM-by-VM and then update the public and private network configurations. When you move from older versions to newer versions, it is best to simply "rip and ship" the VM by shutting it down and performing a _detach/attach_ between the environments. If you are moving between locations, a long-distance vMotion is possible.
   5. Develop testing plans for verification of the environment.
   6. Coordinate a change/maintenance window with users. Individual VM maintenance windows can account for transfer of data, configuration of the VM, changing, and propagation of DNS, and time for troubleshooting.
14. Deploy the new environment:
   1. Order the new vSphere and vCenter servers (and any other servers that you need).
      **Note:** Make sure that the proper "unbonded" network uplinks are selected.
   2. Order and configure the appropriate storage: [Architecture Guide for IBM File Storage for IBM Cloud with VMware](https://cloud.ibm.com/docs/FileStorage?topic=FileStorage-architectureguide)
   3. Order the new VLANs and portable subnets (detailed architecture diagrams and justification might be required).
   4. Configure vCenter to communicate the with vSphere servers and configure of the environment.
   5. Take backups in the live environment.
   6. Run the migration plan and associated test plans.
   8. Implement backups in the new environment.
   9. Operate the new environment.
   10. Decommission the legacy environment.
