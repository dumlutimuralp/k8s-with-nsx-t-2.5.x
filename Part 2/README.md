# NSX-T 2.5.x & K8S  - PART 2
[Home Page](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x)

# Table of Contents
[NSX Components in K8S Integration](#NSX-Components-in-K8S-Integration)  
[Ubuntu 18.04 Installation](#Ubuntu-18.04-Installation) 
[Docker Installation](#Docker-Installation)
[K8S Installation](#K8S-Installation)

# NSX Components in K8S Integration
[Back Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%202#Table-of-Contents)

This section focuses only on the differences between NSX-T 2.4 and NSX-T 2.5' s integration with K8S. For the detailed explanation of the architecture please refer to Part 2 of the prevous series (K8S with NSX-T 2.4.x) which is published [here](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.4.x/blob/master/Part%202/README.md)

* First difference with NSX-T 2.5 is that previously the admin had to login to each K8S node; then install and configure CNI Plugin and Open vSwitch on each node seperately and alsoo upgraded manually. Now this is all managed and maintained by <b>a new K8S daemonset called "NSX-NCP-Bootstrap"</b>. Now with NSX-T 2.5.x, the "NSX-NCP-Bootstrap" Pod on each K8S node takes care of that. 

* Second difference with NSX-T 2.5 is <b>a new/additional container called "NSX-OVS" which is packaged within "NSX Node Agent" Pod.</b> It keeps the OVS daemon running on the container host. Which means the OVS daemon is run in the container' s IPC namespace. 

* Third difference is the manifest for all the following components are now packaged in a single YAML file. (Components : NSX Container Plugin (and all the config parameters of NCP.ini as configmap) , NSX Node Agent, the NSX infrastructure' s own namespace "nsx-system" , the role based access control architecture that is applied to that namespace, and the NSX NCP Bootstrap)

* Fourth difference is previously each K8S namespace in a given K8S cluster used to have its own Tier1 Logical Router at all times and all the stateful services like Source NAT was configured on Tier 0 Logical Router. Not only that K8S Ingress and Service Type Load Balancer was implemented on a seperate/dedicated Tier 1 Logical Router. <b>With NSX-T 2.5 all these services can be collapsed on a single Tier 1 Logical Router. </b> When a new namespace s provisioned that will be realized as a new downlink attached to the same Tier 1 Logical Router. K8S Pods is SNATed on the same Tier 1 Logical Router and also K8S Ingress and Service Type Load Balancer VIPs are realized on the same Tier 1 Logical Router. This implementation model is presented as an option in the NCP.ini configmap of the NSX Container Plugin replicaset. 

* Fifth difference is the NSX-T Policy API is supported with K8S. As mentioned Policy API corresponds to Simplified UI in the NSX-T GUI. This also is presented as an option in the NCP.ini.

* Sixth difference is the K8S Network Policy driven NSX-T DFW rules can be placed in the "Application" category of the DFW in the simplified UI. (with three different options as allow cluster, allow namespace, none)  This is also presented as a new NCP.ini parameter. ("baseline_policy_type")

* There are additional new parameters introduced in NCP.ini file which will be explained later on.

# Ubuntu 18.04 Installation
[Back Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%202#Table-of-Contents)

For Ubuntu 18.04 installation [this article](https://www.linuxtechi.com/ubuntu-18-04-lts-desktop-installation-guide-screenshots/) outlines the steps needed in a simplified flow structure.


# Docker Installation
[Back Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%202#Table-of-Contents)

# K8S Installation
[Back Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%202#Table-of-Contents)
