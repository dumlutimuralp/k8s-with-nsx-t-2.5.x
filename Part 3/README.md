# NSX-T 2.5.x & K8S  - PART 3
[Home Page](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x)

# Table of Contents
[Configuring NSX Objects for K8S](#Configuring-NSX-Objects-for-K8S)  
[NSX Downloadables for K8S](#NSX-Downloadables-for-K8S)  
[Content of Manifest File](#Content-of-Manifest-File)

# Configuring NSX Objects for K8S
[Back to Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%203#Table-of-Contents)

In this section the ports of the "K8S-NodeTransport" segment, to which the Kubernetes Nodes second vNIC is connected to, will be configured with specific scopes as "ncp/cluster" , "ncp/node_name" and with specific tags as "k8s-cluster" and K8S Node hostname.

Navigate to "Networking -> Segments" in the NSX-T Simplified UI and then CLICK three dots on the left of the  "K8S-NodeTransport" segment and then click edit in the pop up menu. Click on the right arrow next to where it says "Ports" and then click on the number "3" on the right to edit the tagging of the ports. 

![](2019-12-18_13-25-54.jpg)

When the ports screen come up then click on three dots on the left of the port on top, and then click on edit, this will bring up the settings screen for that segment port.

![](2019-12-18_13-31-39.jpg)

Configure the tag and scope as shown below.

![](2019-12-18_13-34-39.jpg)

![](2019-12-18_13-44-34.jpg)


Repeat the steps for the remaining nodes

Note#1 : The tag should match the node name which should match the hostname of the Ubuntu node, since that specific hostname will be used by Kubernetes as the node name.

Note#2 : If the admin changes the Kubernetes node name, then the tag ncp/node_name should also be updated and NCP needs to be restarted. Once Kubernetes is installed, "kubectl get nodes" can be used to provide the the node names in the output. The tags should be added to the logical switch port before that node gets added to the K8S cluster by using the "kubeadm join" command. Otherwise, the new node will not have network connectivity. In case of tags being incorrect or missing, then to fix the issue, correct tags should be applied and NCP should be restarted.

# NSX Downloadables for K8S
[Back to Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%203#Table-of-Contents)

NSX Container Plug-in for Kubernetes and Cloud Foundry - Installation and Administration Guide, published [here](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/2.5/ncp-kubernetes/GUID-FB641321-319D-41DC-9D16-37D6BA0BC0DE.html), guides the user on the installation steps of the NSX components on a K8S cluster. In this article a more simplified and explanatory view is provided.

Kubernetes related NSX files can be downloaded from NSX-T download page at my.vmware.com (shown below)

![](2019-12-16_17-38-09.jpg)

When "Go To Downloads" is clicked the details of the content can be reviewed in the following page (below)

![](2019-12-16_17-43-07.jpg)

Once the .zip file is downloaded and extracted the content is as below.

![](2019-12-16_22-06-35.jpg)

The breakdown of the content is following :

* Kubernetes : This folder contains the unified manifest file (Yaml) and container image (.tar) for RHEL and Ubuntu operating systems. The same container image is used for NSX Node Agent, NSX Kube Proxy, NSX OVS and NSX Dummy containers. (Note that there is a container image also for Photon operating system which is used on nodes in Pivotal Application Services (PAS) solution)

* Openshift : This folder contains the unified manifest file (.yaml) for Openshift baremetal nodes andd Openshift virtual machine nodes.

* Open vSwitch : This folder contains the Open vSwitch package for various operating systems. 

* PAS : This folder contains the Pivotal Application Services (PAS) specific installation file. 

* Scripts : As the name suggests this folder contains the scripts to clean all the K8S related objects in NSX-T objecct database in a policy API based or management API based NSX-T environment in the event of a K8S cluster decommission process.

Since in this environment Ubuntu is the operating system for K8S nodes, "nsx-ncp-ubuntu-2.5.0.14628220.tar" and "ncp-ubuntu.yaml" will be used. 

Let' s look at the manfiest file "ncp-ubuntu.yaml" in more detail now.



