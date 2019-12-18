# NSX-T 2.5.x & K8S  - PART 4
[Home Page](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x)

# Table of Contents
[Deploying NSX Components in K8S Cluster](#Deploying-NSX-Components-in-K8S-Cluster)

# Deploying NSX Components in K8S Cluster
[Back to Table of Contents](https://github.com/dumlutimuralp/k8s-with-nsx-t-2.5.x/tree/master/Part%204#Table-of-Contents)

1. Copy the "nsx-ncp-ubuntu-2.5.0.14628220.tar" file (located in the Kubernetes folder of the .zip file downloaded from my.vmware.com) to a folder on each K8S node. This file is the container image file that is used for containers in the NSX Node Agent Pod and also NSX NCP Bootstracp Pod.  

Hint : Winscp is a handy tool for file copying from Windows to Linux.  

2. On each K8S node, at the prompt, run the <b>"sudo docker load -i nsx-ncp-ubuntu-2.5.0.14628220.tar"</b> command to load the container image to the local Docker container image repository on each K8S node. (This command needs to be run in the same folder which the container image file was copied to on the K8S node) 

3. On each K8S node, tag the image by running <b>"docker tag registry.local/2.5.0.14628220/nsx-ncp-ubuntu:latest nsx-ncp"</b> . This is needed as the container image name used in the manifest file (edited back in Part 3) is pointing out to the container image name of "nsx-ncp". Verify that the image is correctly renamed by running <b>"sudo docker images"</b>.

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

4. On K8S master node, run "kubectl apply -f ncp-ubuntu.yaml". This command will create a namespace as "nsx-system" in the K8S cluster, then associate a few services accounts and cluster roles in that namespace, then create NCP deployment, NSX NCP Bootstracp daemonset, NSX Node Agent daemonset. 

All of the above can be verified by running "kubectl get all -n nsx-system". As shown below.

<pre><code>
root@k8s-master:~# kubectl get all -n nsx-system
NAME                           READY   STATUS    RESTARTS   AGE
pod/nsx-ncp-848cc8c8ff-k6vfg   1/1     Running   0          13d
pod/nsx-ncp-bootstrap-4mxj5    1/1     Running   0          14d
pod/nsx-ncp-bootstrap-72lvg    1/1     Running   0          14d
pod/nsx-ncp-bootstrap-s5zv4    1/1     Running   0          14d
pod/nsx-node-agent-5xtm4       3/3     Running   0          14d
pod/nsx-node-agent-68ls8       3/3     Running   0          14d
pod/nsx-node-agent-bbpjm       3/3     Running   0          14d

NAME                               DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/nsx-ncp-bootstrap   3         3         3       3            3           <none>          14d
daemonset.apps/nsx-node-agent      3         3         3       3            3           <none>          14d

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nsx-ncp   1/1     1            1           14d

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/nsx-ncp-848cc8c8ff   1         1         1       14d
root@k8s-master:~#
</code></pre>

Note : If any NSX Pods show up in "CrashLoopBackOff" status then the logs of the respective container in the respective Pod can be investigated. Please refer to [Troubleshootng](?????) section for more information.

At this stage let' s revisit the topology that was shown in previous posts.

![](2019-12-18_22-26-01.jpg)

Since a K8S cluster comes with multiple namespaces (kube-system, default etc.) and K8S services (kubernetes API, DNS etc.) by default, for these K8S constructs it is expected to have the correspding NSX-T constructs created automaticaly by NCP. (NCP is the Pod running with the name "nsx-ncp-848cc8c8ff-k6vfg" (in the previous output) in this demonstration. 

Let' s check what has changed on NSX-T side.

A new Tier 1 Gateway has been provisioned with the name "k8s-cluster".

![](2019-12-18_22-34-46.jpg)

Five new segments are provisioned (one per K8S namespace) on the Tier 1 gateway. 

![](2019-12-18_22-35-23.jpg)

A new load balancer is provisioned and attached to the Tier 1 Gateway.

![](2019-12-18_22-38-22.jpg)

The VIP for the K8S ingress (Layer 7 LB) is automatically provisioned. The IP adress of the VIP is picked from the "K8S-LB-POOL" automtically.

![](2019-12-18_22-38-40.jpg)

Two firewall rules are automatically provisioned between the sections that were manually configured before (K8S-Begin and K8S0End) . These firewall rules are for K8S node healthcheck traffic destined for CoreDNS Pods.

![](2019-12-18_22-41-42.jpg)


