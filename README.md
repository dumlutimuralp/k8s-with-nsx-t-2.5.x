# VMware NSX-T 2.5.x and Kubernetes (K8S) Guide
by Dumlu Timuralp [@dumlutimuralp](https://twitter.com/dumlutimuralp) / [LinkedIn](https://www.linkedin.com/in/dumlutimuralp/) 

_**This disclaimer informs readers that the views, thoughts, and opinions expressed in this series of posts belong solely to the author, and not necessarily to the author’s employer, organization, committee or other group or individual.**_

The goal of this series of posts is to outline and explain the steps to integrate <b>VMware NSX-T 2.5.0</b>, using its declarative API called **Policy API** , with Kubernetes control plane.

List of components used in this environment are;

- vCenter 6.7 U1b (Build 11727113)
- ESX 6.7 U2 (Build 13006603)
- NSX-T 2.5.0 (Build 14663978)
- NSX Container Plugin 2.5.0 (Build 14628220)
- Ubuntu Server 18.04.3
- Docker CE 18.06.0
- Kubernetes 1.14.7

It is highly recommended to check the following resources for compatibility requirements.

* VMware Product Interoperability Matrices  
https://www.vmware.com/resources/compatibility/sim/interop_matrix.php#interop&175=&2=&1=

* NSX Container Plugin 2.5 Release Notes
https://docs.vmware.com/en/VMware-NSX-T-Data-Center/2.5/rn/NSX-Container-Plugin-25-Release-Notes.html

* NSX Container Plug-in for Kubernetes and Cloud Foundry - Installation and Administration Guide
https://docs.vmware.com/en/VMware-NSX-T-Data-Center/2.5/rn/NSX-Container-Plugin-25-Release-Notes.html

This series does **NOT** provide the generic intro level information on NSX-T or K8S. To have a basic understanding of NSX-T please watch the VMworld session recordings. Similarly for K8S, Pluralsight and A Cloud Guru trainings by Nigel Poulton and Udemy trainings by Mumshad Mannambeth is highly recommended.  

<b>The [Part 1](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.4.x/blob/master/Part%201/README.md) , [Part 2](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.4.x/blob/master/Part%202/README.md) and [Part 3](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.4.x/blob/master/Part%203/README.md) of the NSX-T 2.4.x series</b> can be reviewed to get a basic understanding of how the integration of NSX-T with K8S looks like. <b>[Part 5](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.4.x/blob/master/Part%205/README.md) and [Part 6](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.4.x/blob/master/Part%206/README.md)</b> of same series may still help in understanding and learning K8S Service an K8S Network Policy constructs though.

This series will be focusing on the delta between NSX-T 2.4.x and NSX-T 2.5.x hence it may refer to some of the points that were mentioned in previous series [K8S with NSX-T 2.4.x](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.4.x)

## [Part 1](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/blob/master/Part%201/README.md)

* Lab Infrastructure
* Current State

## [Part 2](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/blob/master/Part%202/README.md)

* NSX Components in K8S Integration
* Ubuntu 18.04 Installation
* Docker Installation
* K8S Installation

## [Part 3](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/blob/master/Part%203/README.md)

* Configuring NSX Objects for K8S 
* NSX Downloadables for K8S  
* Content of Manifest File

## [Part 4](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/blob/master/Part%204/README.md)

* Deploying NSX Components in K8S Cluster
* Creating Namespace and Deploying Test Workloads
* Troubleshooting
