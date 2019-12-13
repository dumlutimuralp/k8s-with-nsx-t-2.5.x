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

* Second difference with NSX-T 2.5 is a new/additional container called "NSX-OVS" which is packaged within "NSX Node Agent" Pod. It keeps the OVS daemon running on the container host. Which means the OVS daemon is run in the container' s IPC namespace. 

* Third difference is the manifest for all the following components are now packaged in a single YAML file. (Components : NSX Container Plugin (and all the config parameters of NCP.ini as configmap) , NSX Node Agent, the NSX infrastructure' s own namespace "nsx-system" , the role based access control architecture that is applied to that namespace, and the NSX NCP Bootstrap)

* Fourth difference is prevo

# Ubuntu 18.04 Installation
[Back Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%202#Table-of-Contents)

For Ubuntu 18.04 installation [this article](https://www.linuxtechi.com/ubuntu-18-04-lts-desktop-installation-guide-screenshots/) outlines the steps needed in a simplified flow structure.


# Docker Installation
[Back Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%202#Table-of-Contents)

# K8S Installation
[Back Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%202#Table-of-Contents)
