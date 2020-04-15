# Log

## Master kubeadm init log

```shell
vagrant@eckAction-master-16:~$ sudo kubeadm init --config kubeadm.yaml
W0414 04:41:44.158547    9776 configset.go:202] WARNING: kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
[init] Using Kubernetes version: v1.18.1
[preflight] Running pre-flight checks
	[WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [eckaction-master-16 kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 10.0.2.15]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [eckaction-master-16 localhost] and IPs [10.0.2.15 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [eckaction-master-16 localhost] and IPs [10.0.2.15 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
W0414 04:48:21.165620    9776 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[control-plane] Creating static Pod manifest for "kube-scheduler"
W0414 04:48:21.167477    9776 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
[apiclient] All control plane components are healthy after 22.504662 seconds
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.18" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Skipping phase. Please see --upload-certs
[mark-control-plane] Marking the node eckaction-master-16 as control-plane by adding the label "node-role.kubernetes.io/master=''"
[mark-control-plane] Marking the node eckaction-master-16 as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
[bootstrap-token] Using token: a6a2bw.8bilxcpgh8qcmm5u
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 10.0.2.15:6443 --token a6a2bw.8bilxcpgh8qcmm5u \
    --discovery-token-ca-cert-hash sha256:7a959216821f638eea139dec84505814b95f93f167a76527932730400d77cf10
```

## kubectl describe master node

```shell
vagrant@eckAction-master-16:~$ kubectl describe node eckaction-master-16
Name:               eckaction-master-16
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=eckaction-master-16
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 14 Apr 2020 05:23:18 +0000
Taints:             node-role.kubernetes.io/master:NoSchedule
                    node.kubernetes.io/not-ready:NoSchedule
Unschedulable:      false
Lease:
  HolderIdentity:  eckaction-master-16
  AcquireTime:     <unset>
  RenewTime:       Tue, 14 Apr 2020 06:46:42 +0000
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Tue, 14 Apr 2020 06:43:42 +0000   Tue, 14 Apr 2020 06:28:42 +0000   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Tue, 14 Apr 2020 06:43:42 +0000   Tue, 14 Apr 2020 06:28:42 +0000   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Tue, 14 Apr 2020 06:43:42 +0000   Tue, 14 Apr 2020 06:28:42 +0000   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            False   Tue, 14 Apr 2020 06:43:42 +0000   Tue, 14 Apr 2020 06:28:42 +0000   KubeletNotReady              runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized
Addresses:
  InternalIP:  10.0.2.15
  Hostname:    eckaction-master-16
Capacity:
  cpu:                2
  ephemeral-storage:  10098468Ki
  hugepages-2Mi:      0
  memory:             8175012Ki
  pods:               110
Allocatable:
  cpu:                2
  ephemeral-storage:  9306748094
  hugepages-2Mi:      0
  memory:             8072612Ki
  pods:               110
System Info:
  Machine ID:                 4c514cddb10f448783e7e51b88a29472
  System UUID:                7B17BB54-BFF2-452B-ADEC-6A2EF28A6970
  Boot ID:                    a9cc2e4a-6c90-47fa-9922-4fd273209505
  Kernel Version:             4.4.0-177-generic
  OS Image:                   Ubuntu 16.04.6 LTS
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  docker://18.9.7
  Kubelet Version:            v1.18.1
  Kube-Proxy Version:         v1.18.1
Non-terminated Pods:          (5 in total)
  Namespace                   Name                                           CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                   ----                                           ------------  ----------  ---------------  -------------  ---
  kube-system                 etcd-eckaction-master-16                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         83m
  kube-system                 kube-apiserver-eckaction-master-16             250m (12%)    0 (0%)      0 (0%)           0 (0%)         83m
  kube-system                 kube-controller-manager-eckaction-master-16    200m (10%)    0 (0%)      0 (0%)           0 (0%)         83m
  kube-system                 kube-proxy-lgn2c                               0 (0%)        0 (0%)      0 (0%)           0 (0%)         83m
  kube-system                 kube-scheduler-eckaction-master-16             100m (5%)     0 (0%)      0 (0%)           0 (0%)         83m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                550m (27%)  0 (0%)
  memory             0 (0%)      0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
  hugepages-2Mi      0 (0%)      0 (0%)
Events:
  Type    Reason                   Age                From                          Message
  ----    ------                   ----               ----                          -------
  Normal  NodeHasSufficientMemory  18m (x3 over 83m)  kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    18m (x3 over 83m)  kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     18m (x3 over 83m)  kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeHasSufficientPID
  Normal  NodeNotReady             18m (x2 over 18m)  kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeNotReady
```

## 检查pod状态

```shell
vagrant@eckAction-master-16:~$ kubectl get pods -n kube-system
NAME                                          READY   STATUS    RESTARTS   AGE
coredns-66bff467f8-qmqf7                      0/1     Pending   0          91m
coredns-66bff467f8-spkp6                      0/1     Pending   0          91m
etcd-eckaction-master-16                      1/1     Running   0          91m
kube-apiserver-eckaction-master-16            1/1     Running   0          91m
kube-controller-manager-eckaction-master-16   1/1     Running   0          91m
kube-proxy-lgn2c                              1/1     Running   0          91m
kube-scheduler-eckaction-master-16            1/1     Running   0          91m
vagrant@eckAction-master-16:~$
```

## 安装网络插件weave network

```shell
vagrant@eckAction-master-16:~$ sudo kubectl apply -f "https://frontend.dev.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
serviceaccount/weave-net configured
clusterrole.rbac.authorization.k8s.io/weave-net configured
clusterrolebinding.rbac.authorization.k8s.io/weave-net configured
role.rbac.authorization.k8s.io/weave-net configured
rolebinding.rbac.authorization.k8s.io/weave-net configured
daemonset.apps/weave-net created
```

## 安装完网络插件以后的 node 状态

```shell
vagrant@eckAction-master-16:~$ kubectl describe node eckaction-master-16
Name:               eckaction-master-16
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=eckaction-master-16
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 14 Apr 2020 05:23:18 +0000
Taints:             node-role.kubernetes.io/master:NoSchedule
Unschedulable:      false
Lease:
  HolderIdentity:  eckaction-master-16
  AcquireTime:     <unset>
  RenewTime:       Tue, 14 Apr 2020 07:22:44 +0000
Conditions:
  Type                 Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----                 ------  -----------------                 ------------------                ------                       -------
  NetworkUnavailable   False   Tue, 14 Apr 2020 07:21:49 +0000   Tue, 14 Apr 2020 07:21:49 +0000   WeaveIsUp                    Weave pod has set this
  MemoryPressure       False   Tue, 14 Apr 2020 07:22:35 +0000   Tue, 14 Apr 2020 06:28:42 +0000   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure         False   Tue, 14 Apr 2020 07:22:35 +0000   Tue, 14 Apr 2020 06:28:42 +0000   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure          False   Tue, 14 Apr 2020 07:22:35 +0000   Tue, 14 Apr 2020 06:28:42 +0000   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready                True    Tue, 14 Apr 2020 07:22:35 +0000   Tue, 14 Apr 2020 07:21:54 +0000   KubeletReady                 kubelet is posting ready status. AppArmor enabled
Addresses:
  InternalIP:  10.0.2.15
  Hostname:    eckaction-master-16
Capacity:
  cpu:                2
  ephemeral-storage:  10098468Ki
  hugepages-2Mi:      0
  memory:             8175012Ki
  pods:               110
Allocatable:
  cpu:                2
  ephemeral-storage:  9306748094
  hugepages-2Mi:      0
  memory:             8072612Ki
  pods:               110
System Info:
  Machine ID:                 4c514cddb10f448783e7e51b88a29472
  System UUID:                7B17BB54-BFF2-452B-ADEC-6A2EF28A6970
  Boot ID:                    a9cc2e4a-6c90-47fa-9922-4fd273209505
  Kernel Version:             4.4.0-177-generic
  OS Image:                   Ubuntu 16.04.6 LTS
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  docker://18.9.7
  Kubelet Version:            v1.18.1
  Kube-Proxy Version:         v1.18.1
Non-terminated Pods:          (8 in total)
  Namespace                   Name                                           CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                   ----                                           ------------  ----------  ---------------  -------------  ---
  kube-system                 coredns-66bff467f8-qmqf7                       100m (5%)     0 (0%)      70Mi (0%)        170Mi (2%)     119m
  kube-system                 coredns-66bff467f8-spkp6                       100m (5%)     0 (0%)      70Mi (0%)        170Mi (2%)     119m
  kube-system                 etcd-eckaction-master-16                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         119m
  kube-system                 kube-apiserver-eckaction-master-16             250m (12%)    0 (0%)      0 (0%)           0 (0%)         119m
  kube-system                 kube-controller-manager-eckaction-master-16    200m (10%)    0 (0%)      0 (0%)           0 (0%)         119m
  kube-system                 kube-proxy-lgn2c                               0 (0%)        0 (0%)      0 (0%)           0 (0%)         119m
  kube-system                 kube-scheduler-eckaction-master-16             100m (5%)     0 (0%)      0 (0%)           0 (0%)         119m
  kube-system                 weave-net-bbkpr                                20m (1%)      0 (0%)      0 (0%)           0 (0%)         2m33s
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                770m (38%)  0 (0%)
  memory             140Mi (1%)  340Mi (4%)
  ephemeral-storage  0 (0%)      0 (0%)
  hugepages-2Mi      0 (0%)      0 (0%)
Events:
  Type    Reason                   Age                 From                          Message
  ----    ------                   ----                ----                          -------
  Normal  NodeHasSufficientMemory  54m (x3 over 119m)  kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    54m (x3 over 119m)  kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     54m (x3 over 119m)  kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeHasSufficientPID
  Normal  NodeNotReady             54m (x2 over 54m)   kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeNotReady
  Normal  NodeReady                50s                 kubelet, eckaction-master-16  Node eckaction-master-16 status is now: NodeReady
```

## 成功安装网络插件后的 pods 状态

```shell
vagrant@eckAction-master-16:~$ kubectl get pods -n kube-system
NAME                                          READY   STATUS    RESTARTS   AGE
coredns-66bff467f8-qmqf7                      1/1     Running   0          125m
coredns-66bff467f8-spkp6                      1/1     Running   0          125m
etcd-eckaction-master-16                      1/1     Running   0          125m
kube-apiserver-eckaction-master-16            1/1     Running   0          125m
kube-controller-manager-eckaction-master-16   1/1     Running   0          125m
kube-proxy-lgn2c                              1/1     Running   0          125m
kube-scheduler-eckaction-master-16            1/1     Running   0          125m
weave-net-bbkpr                               2/2     Running   0          8m22s
```

## Master节点最终部署成功apiServer地址映射到192.168.0.210

```shell
[orientsoft@test16 master-16]$ vagrant up
Bringing machine 'master' up with 'virtualbox' provider...
==> master: Importing base box 'ubuntu/xenial64'...
==> master: Matching MAC address for NAT networking...
==> master: Setting the name of the VM: k8s-eckAction-master-16
==> master: Clearing any previously set network interfaces...
==> master: Available bridged network interfaces:
1) enp2s0f1
2) enp2s0f0
3) virbr0
==> master: When choosing an interface, it is usually the one that is
==> master: being used to connect to the internet.
==> master:
    master: Which interface should the network bridge to? 1
==> master: Preparing network interfaces based on configuration...
    master: Adapter 1: nat
    master: Adapter 2: bridged
==> master: Forwarding ports...
    master: 22 (guest) => 2222 (host) (adapter 1)
==> master: Running 'pre-boot' VM customizations...
==> master: Booting VM...
==> master: Waiting for machine to boot. This may take a few minutes...
    master: SSH address: 127.0.0.1:2222
    master: SSH username: vagrant
    master: SSH auth method: private key
    master: Warning: Connection reset. Retrying...
    master: Warning: Remote connection disconnect. Retrying...
    master:
    master: Vagrant insecure key detected. Vagrant will automatically replace
    master: this with a newly generated keypair for better security.
    master:
    master: Inserting generated public key within guest...
    master: Removing insecure key from the guest if it's present...
    master: Key inserted! Disconnecting and reconnecting using new SSH key...
==> master: Machine booted and ready!
==> master: Checking for guest additions in VM...
    master: The guest additions on this VM do not match the installed version of
    master: VirtualBox! In most cases this is fine, but in rare cases it can
    master: prevent things such as shared folders from working properly. If you see
    master: shared folder errors, please make sure the guest additions within the
    master: virtual machine match the version of VirtualBox you have installed on
    master: your host and reload your VM.
    master:
    master: Guest Additions Version: 5.1.38
    master: VirtualBox Version: 6.0
==> master: Setting hostname...
==> master: Configuring and enabling network interfaces...
==> master: Mounting shared folders...
    master: /vagrant => /home/orientsoft/leiw/vagrantVMs/k8sC/eckAction/master-16
    master: /vagrant_sync_dir => /home/orientsoft/leiw/vagrantVMs/k8sC/eckAction/master-16/sync_dir
==> master: Running provisioner: shell...
    master: Running: inline script
    master: OK
    master: Get:1 http://security.ubuntu.com/ubuntu xenial-security InRelease [109 kB]
    master: Hit:2 http://archive.ubuntu.com/ubuntu xenial InRelease
    master: Get:3 http://archive.ubuntu.com/ubuntu xenial-updates InRelease [109 kB]
    master: Get:4 http://security.ubuntu.com/ubuntu xenial-security/main amd64 Packages [850 kB]
    master: Get:5 https://packages.cloud.google.com/apt kubernetes-xenial InRelease [8,993 B]
    master: Get:6 http://security.ubuntu.com/ubuntu xenial-security/main Translation-en [321 kB]
    master: Get:7 http://security.ubuntu.com/ubuntu xenial-security/universe amd64 Packages [489 kB]
    master: Get:8 http://archive.ubuntu.com/ubuntu xenial-backports InRelease [107 kB]
    master: Get:9 http://security.ubuntu.com/ubuntu xenial-security/universe Translation-en [200 kB]
    master: Get:10 http://security.ubuntu.com/ubuntu xenial-security/multiverse amd64 Packages [5,728 B]
    master: Get:11 http://security.ubuntu.com/ubuntu xenial-security/multiverse Translation-en [2,708 B]
    master: Get:12 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages [34.8 kB]
    master: Get:13 http://archive.ubuntu.com/ubuntu xenial/universe amd64 Packages [7,532 kB]
    master: Get:14 http://archive.ubuntu.com/ubuntu xenial/universe Translation-en [4,354 kB]
    master: Get:15 http://archive.ubuntu.com/ubuntu xenial/multiverse amd64 Packages [144 kB]
    master: Get:16 http://archive.ubuntu.com/ubuntu xenial/multiverse Translation-en [106 kB]
    master: Get:17 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 Packages [1,130 kB]
    master: Get:18 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 Packages [796 kB]
    master: Get:19 http://archive.ubuntu.com/ubuntu xenial-updates/universe Translation-en [333 kB]
    master: Get:20 http://archive.ubuntu.com/ubuntu xenial-updates/multiverse amd64 Packages [16.8 kB]
    master: Get:21 http://archive.ubuntu.com/ubuntu xenial-updates/multiverse Translation-en [8,468 B]
    master: Get:22 http://archive.ubuntu.com/ubuntu xenial-backports/main amd64 Packages [7,280 B]
    master: Get:23 http://archive.ubuntu.com/ubuntu xenial-backports/main Translation-en [4,456 B]
    master: Get:24 http://archive.ubuntu.com/ubuntu xenial-backports/universe amd64 Packages [8,064 B]
    master: Get:25 http://archive.ubuntu.com/ubuntu xenial-backports/universe Translation-en [4,328 B]
    master: Fetched 16.7 MB in 10s (1,599 kB/s)
    master: Reading package lists...
    master: Reading package lists...
    master: Building dependency tree...
    master:
    master: Reading state information...
    master: The following additional packages will be installed:
    master:   bridge-utils cgroupfs-mount conntrack containerd cri-tools ebtables kubectl
    master:   kubelet kubernetes-cni pigz runc socat ubuntu-fan
    master: Suggested packages:
    master:   mountall aufs-tools debootstrap docker-doc rinse zfs-fuse | zfsutils
    master: The following NEW packages will be installed:
    master:   bridge-utils cgroupfs-mount conntrack containerd cri-tools docker.io
    master:   ebtables kubeadm kubectl kubelet kubernetes-cni pigz runc socat ubuntu-fan
    master: 0 upgraded, 15 newly installed, 0 to remove and 2 not upgraded.
    master: Need to get 104 MB of archives.
    master: After this operation, 532 MB of additional disk space will be used.
    master: Get:3 http://archive.ubuntu.com/ubuntu xenial/universe amd64 pigz amd64 2.3.1-2 [61.1 kB]
    master: Get:7 http://archive.ubuntu.com/ubuntu xenial/main amd64 bridge-utils amd64 1.5-9ubuntu1 [28.6 kB]
    master: Get:1 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 cri-tools amd64 1.13.0-00 [8,776 kB]
    master: Get:8 http://archive.ubuntu.com/ubuntu xenial/universe amd64 cgroupfs-mount all 1.2 [4,970 B]
    master: Get:9 http://archive.ubuntu.com/ubuntu xenial/main amd64 conntrack amd64 1:1.4.3-3 [27.3 kB]
    master: Get:10 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 runc amd64 1.0.0~rc7+git20190403.029124da-0ubuntu1~16.04.4 [1,890 kB]
    master: Get:11 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 containerd amd64 1.2.6-0ubuntu1~16.04.3 [19.7 MB]
    master: Get:12 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 docker.io amd64 18.09.7-0ubuntu1~16.04.5 [30.4 MB]
    master: Get:13 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 ebtables amd64 2.0.10.4-3.4ubuntu2.16.04.2 [79.9 kB]
    master: Get:14 http://archive.ubuntu.com/ubuntu xenial/universe amd64 socat amd64 1.7.3.1-1 [321 kB]
    master: Get:15 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 ubuntu-fan all 0.12.8~16.04.3 [35.1 kB]
    master: Get:2 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubernetes-cni amd64 0.7.5-00 [6,473 kB]
    master: Get:4 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubelet amd64 1.18.1-00 [19.4 MB]
    master: Get:5 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubectl amd64 1.18.1-00 [8,820 kB]
    master: Get:6 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubeadm amd64 1.18.1-00 [8,163 kB]
    master: dpkg-preconfigure: unable to re-open stdin: No such file or directory
    master: Fetched 104 MB in 1min 22s (1,259 kB/s)
    master: Selecting previously unselected package pigz.
    master: (Reading database ...
    master: (Reading database ... 5%
    master: (Reading database ... 10%
    master: (Reading database ... 15%
    master: (Reading database ... 20%
    master: (Reading database ... 25%
    master: (Reading database ... 30%
    master: (Reading database ... 35%
    master: (Reading database ... 40%
    master: (Reading database ... 45%
    master: (Reading database ... 50%
    master: (Reading database ... 55%
    master: (Reading database ... 60%
    master: (Reading database ... 65%
    master: (Reading database ... 70%
    master: (Reading database ... 75%
    master: (Reading database ... 80%
    master: (Reading database ... 85%
    master: (Reading database ... 90%
    master: (Reading database ... 95%
    master: (Reading database ... 100%
    master: (Reading database ...
    master: 54295 files and directories currently installed.)
    master: Preparing to unpack .../pigz_2.3.1-2_amd64.deb ...
    master: Unpacking pigz (2.3.1-2) ...
    master: Selecting previously unselected package bridge-utils.
    master: Preparing to unpack .../bridge-utils_1.5-9ubuntu1_amd64.deb ...
    master: Unpacking bridge-utils (1.5-9ubuntu1) ...
    master: Selecting previously unselected package cgroupfs-mount.
    master: Preparing to unpack .../cgroupfs-mount_1.2_all.deb ...
    master: Unpacking cgroupfs-mount (1.2) ...
    master: Selecting previously unselected package conntrack.
    master: Preparing to unpack .../conntrack_1%3a1.4.3-3_amd64.deb ...
    master: Unpacking conntrack (1:1.4.3-3) ...
    master: Selecting previously unselected package runc.
    master: Preparing to unpack .../runc_1.0.0~rc7+git20190403.029124da-0ubuntu1~16.04.4_amd64.deb ...
    master: Unpacking runc (1.0.0~rc7+git20190403.029124da-0ubuntu1~16.04.4) ...
    master: Selecting previously unselected package containerd.
    master: Preparing to unpack .../containerd_1.2.6-0ubuntu1~16.04.3_amd64.deb ...
    master: Unpacking containerd (1.2.6-0ubuntu1~16.04.3) ...
    master: Selecting previously unselected package cri-tools.
    master: Preparing to unpack .../cri-tools_1.13.0-00_amd64.deb ...
    master: Unpacking cri-tools (1.13.0-00) ...
    master: Selecting previously unselected package docker.io.
    master: Preparing to unpack .../docker.io_18.09.7-0ubuntu1~16.04.5_amd64.deb ...
    master: Unpacking docker.io (18.09.7-0ubuntu1~16.04.5) ...
    master: Selecting previously unselected package ebtables.
    master: Preparing to unpack .../ebtables_2.0.10.4-3.4ubuntu2.16.04.2_amd64.deb ...
    master: Unpacking ebtables (2.0.10.4-3.4ubuntu2.16.04.2) ...
    master: Selecting previously unselected package kubernetes-cni.
    master: Preparing to unpack .../kubernetes-cni_0.7.5-00_amd64.deb ...
    master: Unpacking kubernetes-cni (0.7.5-00) ...
    master: Selecting previously unselected package socat.
    master: Preparing to unpack .../socat_1.7.3.1-1_amd64.deb ...
    master: Unpacking socat (1.7.3.1-1) ...
    master: Selecting previously unselected package kubelet.
    master: Preparing to unpack .../kubelet_1.18.1-00_amd64.deb ...
    master: Unpacking kubelet (1.18.1-00) ...
    master: Selecting previously unselected package kubectl.
    master: Preparing to unpack .../kubectl_1.18.1-00_amd64.deb ...
    master: Unpacking kubectl (1.18.1-00) ...
    master: Selecting previously unselected package kubeadm.
    master: Preparing to unpack .../kubeadm_1.18.1-00_amd64.deb ...
    master: Unpacking kubeadm (1.18.1-00) ...
    master: Selecting previously unselected package ubuntu-fan.
    master: Preparing to unpack .../ubuntu-fan_0.12.8~16.04.3_all.deb ...
    master: Unpacking ubuntu-fan (0.12.8~16.04.3) ...
    master: Processing triggers for man-db (2.7.5-1) ...
    master: Processing triggers for ureadahead (0.100.0-19.1) ...
    master: Processing triggers for systemd (229-4ubuntu21.27) ...
    master: Setting up pigz (2.3.1-2) ...
    master: Setting up bridge-utils (1.5-9ubuntu1) ...
    master: Setting up cgroupfs-mount (1.2) ...
    master: Setting up conntrack (1:1.4.3-3) ...
    master: Setting up runc (1.0.0~rc7+git20190403.029124da-0ubuntu1~16.04.4) ...
    master: Setting up containerd (1.2.6-0ubuntu1~16.04.3) ...
    master: Setting up cri-tools (1.13.0-00) ...
    master: Setting up docker.io (18.09.7-0ubuntu1~16.04.5) ...
    master: Adding group `docker' (GID 117) ...
    master: Done.
    master: Setting up ebtables (2.0.10.4-3.4ubuntu2.16.04.2) ...
    master: update-rc.d: warning: start and stop actions are no longer supported; falling back to defaults
    master: Setting up kubernetes-cni (0.7.5-00) ...
    master: Setting up socat (1.7.3.1-1) ...
    master: Setting up kubelet (1.18.1-00) ...
    master: Setting up kubectl (1.18.1-00) ...
    master: Setting up kubeadm (1.18.1-00) ...
    master: Setting up ubuntu-fan (0.12.8~16.04.3) ...
    master: Processing triggers for ureadahead (0.100.0-19.1) ...
    master: Processing triggers for systemd (229-4ubuntu21.27) ...
    master: [init] Using Kubernetes version: v1.18.1
    master: W0415 10:27:00.530761    4800 configset.go:202] WARNING: kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
    master: [preflight] Running pre-flight checks
    master: 	[WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
    master: [preflight] Pulling images required for setting up a Kubernetes cluster
    master: [preflight] This might take a minute or two, depending on the speed of your internet connection
    master: [preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
    master: [kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
    master: [kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
    master: [kubelet-start] Starting the kubelet
    master: [certs] Using certificateDir folder "/etc/kubernetes/pki"
    master: [certs] Generating "ca" certificate and key
    master: [certs] Generating "apiserver" certificate and key
    master: [certs] apiserver serving cert is signed for DNS names [eckaction-master-16 kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.0.210]
    master: [certs] Generating "apiserver-kubelet-client" certificate and key
    master: [certs] Generating "front-proxy-ca" certificate and key
    master: [certs] Generating "front-proxy-client" certificate and key
    master: [certs] Generating "etcd/ca" certificate and key
    master: [certs] Generating "etcd/server" certificate and key
    master: [certs] etcd/server serving cert is signed for DNS names [eckaction-master-16 localhost] and IPs [192.168.0.210 127.0.0.1 ::1]
    master: [certs] Generating "etcd/peer" certificate and key
    master: [certs] etcd/peer serving cert is signed for DNS names [eckaction-master-16 localhost] and IPs [192.168.0.210 127.0.0.1 ::1]
    master: [certs] Generating "etcd/healthcheck-client" certificate and key
    master: [certs] Generating "apiserver-etcd-client" certificate and key
    master: [certs] Generating "sa" key and public key
    master: [kubeconfig] Using kubeconfig folder "/etc/kubernetes"
    master: [kubeconfig] Writing "admin.conf" kubeconfig file
    master: [kubeconfig] Writing "kubelet.conf" kubeconfig file
    master: [kubeconfig] Writing "controller-manager.conf" kubeconfig file
    master: [kubeconfig] Writing "scheduler.conf" kubeconfig file
    master: [control-plane] Using manifest folder "/etc/kubernetes/manifests"
    master: [control-plane] Creating static Pod manifest for "kube-apiserver"
    master: [control-plane] Creating static Pod manifest for "kube-controller-manager"
    master: W0415 10:33:19.368672    4800 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
    master: [control-plane] Creating static Pod manifest for "kube-scheduler"
    master: W0415 10:33:19.370911    4800 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
    master: [etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
    master: [wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
    master: [apiclient] All control plane components are healthy after 23.004009 seconds
    master: [upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
    master: [kubelet] Creating a ConfigMap "kubelet-config-1.18" in namespace kube-system with the configuration for the kubelets in the cluster
    master: [upload-certs] Skipping phase. Please see --upload-certs
    master: [mark-control-plane] Marking the node eckaction-master-16 as control-plane by adding the label "node-role.kubernetes.io/master=''"
    master: [mark-control-plane] Marking the node eckaction-master-16 as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
    master: [bootstrap-token] Using token: qpdh2q.pjb69c8etdbkxtrx
    master: [bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
    master: [bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to get nodes
    master: [bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
    master: [bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
    master: [bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
    master: [bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
    master: [kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
    master: [addons] Applied essential addon: CoreDNS
    master: [addons] Applied essential addon: kube-proxy
    master:
    master: Your Kubernetes control-plane has initialized successfully!
    master:
    master: To start using your cluster, you need to run the following as a regular user:
    master:
    master:   mkdir -p $HOME/.kube
    master:   sudo cp -i
    master: /etc/kubernetes/admin.conf
    master:  $HOME/.kube/config
    master:   sudo chown $(id -u):$(id -g) $HOME/.kube/config
    master:
    master: You should now deploy a pod network to the cluster.
    master: Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
    master:   https://kubernetes.io/docs/concepts/cluster-administration/addons/
    master: Then you can join any number of worker nodes by running the following on each as root:
    master: kubeadm join 192.168.0.210:6443 --token qpdh2q.pjb69c8etdbkxtrx \
    master:     --discovery-token-ca-cert-hash sha256:3e5788f4f17f782e53c939bf7817d884b711acb55481eeac2438cb9d1a6f7257
    master: serviceaccount/weave-net created
    master: clusterrole.rbac.authorization.k8s.io/weave-net created
    master: clusterrolebinding.rbac.authorization.k8s.io/weave-net created
    master: role.rbac.authorization.k8s.io/weave-net created
    master: rolebinding.rbac.authorization.k8s.io/weave-net created
    master: daemonset.apps/weave-net created
[orientsoft@test16 master-16]$ vagrant ssh
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-177-generic x86_64)
vagrant@eckAction-master-16:~$ kubectl get nodes
error: no configuration has been provided, try setting KUBERNETES_MASTER environment variable
vagrant@eckAction-master-16:~$ mkdir -p $HOME/.kube
vagrant@eckAction-master-16:~$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
vagrant@eckAction-master-16:~$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
vagrant@eckAction-master-16:~$ kubectl get nodes
NAME                  STATUS     ROLES    AGE     VERSION
eckaction-master-16   Ready      master   7m28s   v1.18.1
eckaction-node1-48    NotReady   <none>   4m20s   v1.18.1
eckaction-node3-22    NotReady   <none>   4m27s   v1.18.1
eckaction-node4-77    NotReady   <none>   4m17s   v1.18.1
```

## Node节点成功join到Master

```shell
vagrant@eckAction-node4-77:~$ sudo kubeadm join 192.168.0.210:6443 --token qpdh2q.pjb69c8etdbkxtrx --discovery-token-ca-cert-hash sha256:3e5788f4f17f782e53c939bf7817d884b711acb55481eeac2438cb9d1a6f7257
W0415 10:32:27.791421    9882 join.go:346] [preflight] WARNING: JoinControlPane.controlPlane settings will be ignored when control-plane flag is not set.
[preflight] Running pre-flight checks
	[WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
[preflight] Reading configuration from the cluster...
[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.18" ConfigMap in the kube-system namespace
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Starting the kubelet
[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap...

This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
```