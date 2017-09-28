---
layout: post
published: false
categories:
  - personal
mathjax: false
featured: false
comments: false
title: Using Microsoft Flow with Office 365 Groups
---

Office 365 Groups is a collaboration service that allows groups or teams in your organization to create documents, work on project plans, send emails and schedule appointments all in one place.

It comes with a SharePoint site collection where the group files are stored. Documents can be uploaded and stored in the Group documents which is the same as 'Shared Documents' Library in the SharePoint Site.

I was curious to see if I could create workflows on this default SharePoint library, so I connected to the site collection using SharePoint Designer and I was able to create workflows.

One of the goals of this whole process was to email an attachment of files uploaded in SharePoint to members of the group. This option/feature is not available out-of-the-box, so I used Microsoft flow to accomplish this.

One of the methods to moving a virtual machine in Azure, is deleting the existing VM, creating a new VM in the new network and then attaching the existing disks. 

In this blog post, I will show you how to moving a vm to a different virtal network using Azure Recovery Services Vault.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/01.JPG)

Here is a step-by-step guide -

### 1) Create a Recovery Services Vault in Azure

Enter the name of the Vault, select the subscription, Resource group and region.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/0.JPG)

Once the recovery services vault is created, create a new backup

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/1.JPG)

### 2) Configure the Virtual Machine Backup

Create a New Backup Goal and Backup Policy. Select the Backup Frequency and Retention Range. You can create a new policy to set this backup to not re-occur.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/2.JPG)

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/3.JPG)

Select the Virtual Machine to Backup. This is the VM in our old network.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/4.JPG)

### 3) Backup the Virtual Machine from the old network

Once the configuration is complete, click Backup Now to begin the backup of the VM. You should recieve a popup alert in Azure once the backup is complete.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/5.JPG)

### 4) Restore the Virtual Machine to the new network

After Backup is complete, Select the Azure VM in Backup Items and click Restore VM.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/6.JPG)

Set Restore Type to Create Virtual Machine, Select the Resource Group and the New Virtual Network.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/7.JPG)

Once the VM is restored, you can see it in your list of virtual machines. You can then decommission the VM in the old network.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/8.JPG)


### Summary

To summarize, we used Azure Recovery Services Vault to move a vm to a different network. I find this method more straightforward and with some scripting, we can easily make this process scale. I will cover the script in a later blog post. I hope you found this post helpful!

