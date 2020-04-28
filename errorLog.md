# Error List for deploy ECK on K8s Cluster using kubeadm

## Debug CrashingBackOff issue

```shell
vagrant@eckAction-master-16:~$ kubectl describe pod weave-net-vgw5n -n kube-system
Name:                 weave-net-vgw5n
Namespace:            kube-system
Priority:             2000001000
Priority Class Name:  system-node-critical
Node:                 eckaction-node4-77/10.0.2.15
Start Time:           Wed, 15 Apr 2020 10:33:32 +0000
Labels:               controller-revision-hash=56b95c97c6
                      name=weave-net
                      pod-template-generation=1
Annotations:          <none>
Status:               Running
IP:                   10.0.2.15
IPs:
  IP:           10.0.2.15
Controlled By:  DaemonSet/weave-net
Containers:
  weave:
    Container ID:  docker://d402110baeefc72e1f283de148c978434acf60aab5c9a8abfdf39eaa7bdafdbc
    Image:         docker.io/weaveworks/weave-kube:2.6.2
    Image ID:      docker-pullable://weaveworks/weave-kube@sha256:a1f58e75f24f02e1c2fa2a95b9e55a1b94930f455e75bd5f4799e1a55671971f
    Port:          <none>
    Host Port:     <none>
    Command:
      /home/weave/launch.sh
      --peer-discovery-url=https://frontend.dev.weave.works/api/net
    State:          Running
      Started:      Fri, 17 Apr 2020 09:24:54 +0000
    Last State:     Terminated
      Reason:       Error
      Exit Code:    1
      Started:      Fri, 17 Apr 2020 09:19:20 +0000
      Finished:     Fri, 17 Apr 2020 09:19:50 +0000
    Ready:          False
    Restart Count:  504
    Requests:
      cpu:      10m
    Readiness:  http-get http://127.0.0.1:6784/status delay=0s timeout=1s period=10s #success=1 #failure=3
    Environment:
      HOSTNAME:   (v1:spec.nodeName)
    Mounts:
      /host/etc from cni-conf (rw)
      /host/home from cni-bin2 (rw)
      /host/opt from cni-bin (rw)
      /host/var/lib/dbus from dbus (rw)
      /lib/modules from lib-modules (rw)
      /run/xtables.lock from xtables-lock (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from weave-net-token-hwxvf (ro)
      /weavedb from weavedb (rw)
  weave-npc:
    Container ID:   docker://59c52c395da8a8e0491d064a6a434cb5a8e40370c4940e54b2c4a4810ffd12dd
    Image:          docker.io/weaveworks/weave-npc:2.6.2
    Image ID:       docker-pullable://weaveworks/weave-npc@sha256:5694b0b77003780333ccd1fc79810469434779cd86e926a17675cc5b70470459
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 15 Apr 2020 10:37:07 +0000
    Ready:          True
    Restart Count:  0
    Requests:
      cpu:  10m
    Environment:
      HOSTNAME:   (v1:spec.nodeName)
    Mounts:
      /run/xtables.lock from xtables-lock (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from weave-net-token-hwxvf (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             False
  ContainersReady   False
  PodScheduled      True
Volumes:
  weavedb:
    Type:          HostPath (bare host directory volume)
    Path:          /var/lib/weave
    HostPathType:
  cni-bin:
    Type:          HostPath (bare host directory volume)
    Path:          /opt
    HostPathType:
  cni-bin2:
    Type:          HostPath (bare host directory volume)
    Path:          /home
    HostPathType:
  cni-conf:
    Type:          HostPath (bare host directory volume)
    Path:          /etc
    HostPathType:
  dbus:
    Type:          HostPath (bare host directory volume)
    Path:          /var/lib/dbus
    HostPathType:
  lib-modules:
    Type:          HostPath (bare host directory volume)
    Path:          /lib/modules
    HostPathType:
  xtables-lock:
    Type:          HostPath (bare host directory volume)
    Path:          /run/xtables.lock
    HostPathType:  FileOrCreate
  weave-net-token-hwxvf:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  weave-net-token-hwxvf
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     :NoSchedule
                 :NoExecute
                 node.kubernetes.io/disk-pressure:NoSchedule
                 node.kubernetes.io/memory-pressure:NoSchedule
                 node.kubernetes.io/network-unavailable:NoSchedule
                 node.kubernetes.io/not-ready:NoExecute
                 node.kubernetes.io/pid-pressure:NoSchedule
                 node.kubernetes.io/unreachable:NoExecute
                 node.kubernetes.io/unschedulable:NoSchedule
Events:
  Type     Reason     Age                      From                         Message
  ----     ------     ----                     ----                         -------
  Warning  Unhealthy  14m (x1503 over 46h)     kubelet, eckaction-node4-77  Readiness probe failed: Get http://127.0.0.1:6784/status: dial tcp 127.0.0.1:6784: connect: connection refused
  Warning  BackOff    4m45s (x11767 over 46h)  kubelet, eckaction-node4-77  Back-off restarting failed container
```

## network plugin weave pod restarted many times

```shell
vagrant@eckAction-master-16:~$ kubectl get pods -n kube-system
NAME                                          READY   STATUS             RESTARTS   AGE
coredns-66bff467f8-n5fwv                      1/1     Running            0          39h
coredns-66bff467f8-xqwb9                      1/1     Running            0          39h
etcd-eckaction-master-16                      1/1     Running            0          39h
kube-apiserver-eckaction-master-16            1/1     Running            0          39h
kube-controller-manager-eckaction-master-16   1/1     Running            0          39h
kube-proxy-2q2l8                              1/1     Running            0          39h
kube-proxy-dpfql                              1/1     Running            0          39h
kube-proxy-vj6v2                              1/1     Running            0          39h
kube-proxy-wr284                              1/1     Running            0          39h
kube-scheduler-eckaction-master-16            1/1     Running            0          39h
weave-net-dw4sj                               2/2     Running            0          39h
weave-net-gh4zx                               1/2     CrashLoopBackOff   427        39h
weave-net-vbw6h                               1/2     CrashLoopBackOff   426        39h
weave-net-vgw5n                               1/2     CrashLoopBackOff   426        39h
......
Name:                 weave-net-gh4zx
Namespace:            kube-system
Priority:             2000001000
Priority Class Name:  system-node-critical
Node:                 eckaction-node1-48/10.0.2.15
Start Time:           Wed, 15 Apr 2020 10:33:34 +0000
Labels:               controller-revision-hash=56b95c97c6
                      name=weave-net
                      pod-template-generation=1
Annotations:          <none>
Status:               Running
IP:                   10.0.2.15
IPs:
  IP:           10.0.2.15
Controlled By:  DaemonSet/weave-net
Containers:
  weave:
    Container ID:  docker://56362948c400b27e5ddcf5cdcabe62f447a30c916b2e3ae40a46d9a8a6d23678
    Image:         docker.io/weaveworks/weave-kube:2.6.2
    Image ID:      docker-pullable://weaveworks/weave-kube@sha256:a1f58e75f24f02e1c2fa2a95b9e55a1b94930f455e75bd5f4799e1a55671971f
    Port:          <none>
    Host Port:     <none>
    Command:
      /home/weave/launch.sh
      --peer-discovery-url=https://frontend.dev.weave.works/api/net
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       Error
      Exit Code:    1
      Started:      Fri, 17 Apr 2020 02:08:45 +0000
      Finished:     Fri, 17 Apr 2020 02:09:15 +0000
    Ready:          False
    Restart Count:  427
    Requests:
      cpu:      10m
    Readiness:  http-get http://127.0.0.1:6784/status delay=0s timeout=1s period=10s #success=1 #failure=3
    Environment:
      HOSTNAME:   (v1:spec.nodeName)
    Mounts:
      /host/etc from cni-conf (rw)
      /host/home from cni-bin2 (rw)
      /host/opt from cni-bin (rw)
      /host/var/lib/dbus from dbus (rw)
      /lib/modules from lib-modules (rw)
      /run/xtables.lock from xtables-lock (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from weave-net-token-hwxvf (ro)
      /weavedb from weavedb (rw)
  weave-npc:
    Container ID:   docker://4ae49703d744395b1448e52afc285c09350604d70d2a8a67942881b20d024ddb
    Image:          docker.io/weaveworks/weave-npc:2.6.2
    Image ID:       docker-pullable://weaveworks/weave-npc@sha256:5694b0b77003780333ccd1fc79810469434779cd86e926a17675cc5b70470459
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 15 Apr 2020 10:37:00 +0000
    Ready:          True
    Restart Count:  0
    Requests:
      cpu:  10m
    Environment:
      HOSTNAME:   (v1:spec.nodeName)
    Mounts:
      /run/xtables.lock from xtables-lock (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from weave-net-token-hwxvf (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             False
  ContainersReady   False
  PodScheduled      True
Volumes:
  weavedb:
    Type:          HostPath (bare host directory volume)
    Path:          /var/lib/weave
    HostPathType:
  cni-bin:
    Type:          HostPath (bare host directory volume)
    Path:          /opt
    HostPathType:
  cni-bin2:
    Type:          HostPath (bare host directory volume)
    Path:          /home
    HostPathType:
  cni-conf:
    Type:          HostPath (bare host directory volume)
    Path:          /etc
    HostPathType:
  dbus:
    Type:          HostPath (bare host directory volume)
    Path:          /var/lib/dbus
    HostPathType:
  lib-modules:
    Type:          HostPath (bare host directory volume)
    Path:          /lib/modules
    HostPathType:
  xtables-lock:
    Type:          HostPath (bare host directory volume)
    Path:          /run/xtables.lock
    HostPathType:  FileOrCreate
  weave-net-token-hwxvf:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  weave-net-token-hwxvf
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     :NoSchedule
                 :NoExecute
                 node.kubernetes.io/disk-pressure:NoSchedule
                 node.kubernetes.io/memory-pressure:NoSchedule
                 node.kubernetes.io/network-unavailable:NoSchedule
                 node.kubernetes.io/not-ready:NoExecute
                 node.kubernetes.io/pid-pressure:NoSchedule
                 node.kubernetes.io/unreachable:NoExecute
                 node.kubernetes.io/unschedulable:NoSchedule
Events:
  Type     Reason     Age                     From                         Message
  ----     ------     ----                    ----                         -------
  Warning  BackOff    10m (x9932 over 39h)    kubelet, eckaction-node1-48  Back-off restarting failed container
  Warning  Unhealthy  5m43s (x1276 over 39h)  kubelet, eckaction-node1-48  Readiness probe failed: Get http://127.0.0.1:6784/status: dial tcp 127.0.0.1:6784: connect: connection refused
```

## Error List 截止到：

1. Warning  FailedScheduling  84s (x30 over 37m)  default-scheduler  0/4 nodes are available: 1 node(s) had taint {node-role.kubernetes.io/master: }, that the pod didn't tolerate, 3 node(s) had taint {node.kubernetes.io/not-ready: }, that the pod didn't tolerate.
2. kube-system weave-net crashloopbackoff

## Error List 截止到：2020-04-16 上午 11:55

1. can not mix '--config' with arguments [apiserver-advertise-address]
2. error unmarshaling configuration schema.GroupVersionKind{Group:"kubeadm.k8s.io", Version:"v1beta2", Kind:"ClusterConfiguration"}: error unmarshaling JSON: while decoding JSON: json: unknown field "api" --> kubeadm.yaml 配置出错，新版kubeadm不认api
3. couldn't validate the identity of the API Server: Get https:192.168.0.210//:6443/api/v1/namespaces/kube-public/configmaps/cluster-info?timeout=10s: x509: certificate is valid for 10.0.2.15, 10.0.9.2, not 192.168.0.210
4. couldn't validate the identity of the API Server: could not find a JWS signature in the cluster-info ConfigMap for token ID "a6a2bw"
5. node: error execution phase preflight: couldn't validate the identity of the API Server: Get <https://10.0.2.15:6443/api/v1/namespaces/kube-public/configmaps/cluster-info?timeout=10s:> dial tcp 10.0.2.15:6443: connect: connection refused
6. Stderr: VBoxManage: error: VT-x is disabled in the BIOS for all CPU modes (VERR_VMX_MSR_ALL_VMX_DISABLED) VBoxManage: error: Details: code NS_ERROR_FAILURE (0x80004005), component ConsoleWrap, interface IConsole
7. unable to recognize no matches for kind daemonset in version extensions/v1beta1 weave
8. version "v1.18" doesn't match patterns for neither semantic version nor labels
9.  unknown configuration schema.GroupVersionKind{Group:"kubeadm.k8s.io", Version:"v1.18", Kind:"ClusterConfiguration"}
10. unknown configuration schema.GroupVersionKind{Group:"kubeadm.k8s.io", Version:"v1.11", Kind:"MasterConfiguration"}
11. vagrantfile error A box must be specified
12. ubuntu 16.04 vagrant up error: No usable default provider could be found for your system
13. ubuntu 16.04 E: Unable to locate package kernel-devel
14. failed to commit changes to dconf: Error spawning command line 'dbus-launch --autolaunch= --binary-syntax --close-stderr': Child process exited with code 1
15. dconf-WARNING **: failed to commit changes to dconf: Error spawning command line 'dbus-launch --autolaunch=ac8ee5c1b9a42eba1dc37016565e6978 --binary-syntax --close-stderr': Child process exited with code 1
16. pod has unbound immediate PersistentVolumeClaims
17. running "VolumeBinding" filter plugin for pod "quickstart-es-default-0": pod has unbound immediate PersistentVolumeClaims
18. JoinControlPane.controlPlane settings will be ignored when control-plane flag is not set
19. detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd"
20. kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
21. WARNING: kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
22. dpkg-preconfigure: unable to re-open stdin: No such file or directory
23. unable to recognize "kube-flannel.yml": no matches for kind "DaemonSet" in version "extensions/v1beta1"
24. WARNING: kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
25. This system is currently not set up to build kernel modules. Please install the Linux kernel "header" files matching the current kernel for adding new hardware support to the system.
26. WARNING: The vboxdrv kernel module is not loaded. Either there is no module available for the current kernel (3.10.0-1062.4.1.el7.x86_64) or it failed to load.
27. dose config.vm.box accept url address
28. /vagrant/embedded/gems/2.2.7/gems/vagrant-2.2.7/lib/vagrant/util/which.rb:37: warning: Insecure world writable dir
29. /opt/vagrant/embedded/gems/2.2.7/gems/vagrant-2.2.7/lib/vagrant/util/which.rb:37: warning: Insecure world writable dir /demo/nodejs in PATH, mode 040777