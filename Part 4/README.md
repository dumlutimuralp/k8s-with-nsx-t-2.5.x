# NSX-T 2.5.x & K8S  - PART 4
[Home Page](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x)

# Table of Contents
[Deploying NSX Components in K8S Cluster](#Deploying-NSX-Components-in-K8S-Cluster)

# Deploying NSX Components in K8S Cluster
[Back to Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%204#Table-of-Contents)

Copy the "nsx-ncp-ubuntu-2.5.0.14628220.tar" file (located in the Kubernetes folder of the .zip file downloaded from my.vmware.com) to a folder on each K8S node. This file is the container image file that is used for containers in the NSX Node Agent Pod and also NSX NCP Bootstracp Pod.  

Hint : Winscp is a handy tool for file copying from Windows to Linux.  

* On each K8S node, at the prompt, run the <b>"sudo docker load -i nsx-ncp-ubuntu-2.5.0.14628220.tar"</b> command to load the container image to the local Docker container image repository on each K8S node. (This command needs to be run in the same folder which the container image file was copied to on the K8S node) 

* On each K8S node, tag the image by running <b>"docker tag registry.local/2.5.0.14628220/nsx-ncp-ubuntu:latest nsx-ncp"</b> . This is needed as the container image name used in the manifest file (edited back in Part 3) is pointing out to the container image name of "nsx-ncp". Verify that the image is correctly renamed by running <b>"sudo docker images"</b>.

<pre><code>
root@k8s-master:~# <b>sudo docker images</b>
REPOSITORY                           TAG                 IMAGE ID            CREATED             SIZE
k8s.gcr.io/kube-proxy                v1.14.9             636041c2a488        5 weeks ago         82.1MB
k8s.gcr.io/kube-apiserver            v1.14.9             5811259ed0c9        5 weeks ago         209MB
k8s.gcr.io/kube-controller-manager   v1.14.9             07193a77f264        5 weeks ago         157MB
k8s.gcr.io/kube-scheduler            v1.14.9             0f036524b7a2        5 weeks ago         81.6MB
<b>nsx-ncp</b>                              latest              40aae9a4aeda        3 months ago        744MB
k8s.gcr.io/coredns                   1.3.1               eb516548c180        11 months ago       40.3MB
k8s.gcr.io/etcd                      3.3.10              2c4adeb21b4f        12 months ago       258MB
k8s.gcr.io/pause                     3.1                 da86e6ba6ca1        24 months ago       742kB
root@k8s-master:~#
</code></pre>

* On K8S master node run "kubectl 
