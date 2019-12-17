# NSX-T 2.5.x & K8S  - PART 3
[Home Page](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x)

# Table of Contents
[NSX Downloadables for K8S](#NSX-Downloadables-for-K8S)  
[Configuring NSX Objects for K8S](#Configuring-NSX-Objects-for-K8S)  
[Content of Manifest File](#Content-of-Manifest-File)

# NSX Downloadables for K8S
[Back to Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%203#Table-of-Contents)

NSX Container Plug-in for Kubernetes and Cloud Foundry - Installation and Administration Guide, published [here](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/2.5/ncp-kubernetes/GUID-FB641321-319D-41DC-9D16-37D6BA0BC0DE.html), guides the user on the installation steps. In this article a more simplified and explanatory view is provided.

Kubernetes related NSX files can be downloaded from NSX-T download page at my.vmware.com (shown below)

![](2019-12-16_17-38-09.jpg)

When "Go To Downloads" is clicked the details of the content can be reviewed in the following page (below)

![](2019-12-16_17-43-07.jpg)

Once the .zip file is downloaded and extracted the content is as below.

![](2019-12-16_22-06-35.jpg)

The breakdown of the content is following :

* Kubernetes : This folder contains the unified manifest file (.yaml) and container image (.tar) for RHEL and Ubuntu operating systems. The same container image is used for NSX Node Agent, NSX Kube Proxy, NSX OVS and NSX NCP Boostrap containers. (Note that there is a container image file for Photon operating system which is used on nodes in Pivotal Application Services (PAS) solution)

* Openshift : This folder contains the unified manifes files (.yaml) for Openshift baremetal nodes andd Openshift virtual machine nodes.

* Open vSwitch : This folder contains the Open vSwitch package for various operating systems. 

* PAS : This folder contains the Pivotal Application Services (PAS) installation file. 

* Scripts : As the name suggests this folder contains the scripts to clean all the K8S related objects in NSX-T objecct database in a policy API based or management API based NSX-T environment.

Since in this environment Ubuntu is the operating system for K8S nodes, "nsx-ncp-ubuntu-2.5.0.14628220.tar" and "ncp-ubuntu.yaml" will be used. 

