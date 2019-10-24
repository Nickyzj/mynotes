- hostname

  - ```
    hostnamectl set-hostname 
    ```

- ntpserver

  - https://www.xiaoz.me/archives/12989

- add sudo

- add hosts



kubernetes github

https://github.com/kubernetes/kubernetes/releases/tag/v1.11.10

阿里云镜像

https://opsx.alibaba.com/mirror

https://mirrors.aliyun.com/kubernetes/yum/repos/

https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/

systemctl disable iptables

systemctl disable firewalld

```shell
cd /etc/yum.repos.d/
vim kubernetes.repo
[kubernetes]
name=Kubernetes Repo
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
gpgcheck=0
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
enable=1

yum repolist

scp kubernetes.repo docker-ce.repo node01:/etc/yum.repo.d/

wget https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
rpm --import rpm-package-key.gpg

yum install docker-ce kubelet kubeadm kubectl


```

docker

```
wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

vim docker-ce.repo
```



----



```shell
cd /etc/yum.repos.d
wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

```shell
vi kubernetes.repo

[kubernetes]
name=Kubernetes Repo
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
gpgcheck=0
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
enabled=1

yum repolist

wget https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
rpm --import rpm-package-key.gpg

scp kubernetes.repo docker-ce.repo k-node01:/etc/yum.repos.d/
scp kubernetes.repo docker-ce.repo k-node02:/etc/yum.repos.d/

yum install docker-ce-18.06.0.ce-3.el7 kubelet-1.11.1-0 kubeadm-1.11.1-0 kubectl-1.11.1-0 kubernetes-cni-0.6.0
```

```shell
vi /usr/lib/systemd/system/docker.service

Environment="HTTPS_PROXY=http://www.ik8s.io:10080"
Environment="NO_PROXY=127.0.0.0/8,10.0.0.0/16"

systemctl daemon-reload
systemctl start docker
docker info

cat /proc/sys/net/bridge/bridge-nf-call-ip6tables
cat /proc/sys/net/bridge/bridge-nf-call-iptables

rpm -ql kubelet

# 不要启动
systemctl start kubelet
tail /var/log/messages

systemctl enable kubelet
systemctl enable docker

kubeadm init --help

vi /etc/sysconfig/kubelet
KUBELET_EXTRA_ARGS="--fail-swap-on=false"

kubeadm init --kubernetes-version=v1.11.1 --pod-network-cidr=10.244.0.0/16 --service-cidr=10.96.0.0/12 --ignore-preflight-errors=Swap
```

```shell
docker pull mirrorgooglecontainers/kube-apiserver-amd64:v1.11.1
docker pull mirrorgooglecontainers/kube-controller-manager-amd64:v1.11.1
docker pull mirrorgooglecontainers/kube-scheduler-amd64:v1.11.1
docker pull mirrorgooglecontainers/kube-proxy-amd64:v1.11.1
docker pull mirrorgooglecontainers/pause:3.1
docker pull mirrorgooglecontainers/etcd-amd64:3.2.18
docker pull coredns/coredns:1.1.3

docker tag docker.io/mirrorgooglecontainers/kube-proxy-amd64:v1.11.1 k8s.gcr.io/kube-proxy-amd64:v1.11.1
docker tag docker.io/mirrorgooglecontainers/kube-scheduler-amd64:v1.11.1 k8s.gcr.io/kube-scheduler-amd64:v1.11.1
docker tag docker.io/mirrorgooglecontainers/kube-apiserver-amd64:v1.11.1 k8s.gcr.io/kube-apiserver-amd64:v1.11.1
docker tag docker.io/mirrorgooglecontainers/kube-controller-manager-amd64:v1.11.1 k8s.gcr.io/kube-controller-manager-amd64:v1.11.1
docker tag docker.io/mirrorgooglecontainers/etcd-amd64:3.2.18  k8s.gcr.io/etcd-amd64:3.2.18
docker tag docker.io/mirrorgooglecontainers/pause:3.1  k8s.gcr.io/pause:3.1
docker tag docker.io/coredns/coredns:1.1.3  k8s.gcr.io/coredns:1.1.3


	[ERROR ImagePull]: failed to pull image [k8s.gcr.io/kube-apiserver-amd64:v1.11.1]: exit status 1
	[ERROR ImagePull]: failed to pull image [k8s.gcr.io/kube-controller-manager-amd64:v1.11.1]: exit status 1
	[ERROR ImagePull]: failed to pull image [k8s.gcr.io/kube-scheduler-amd64:v1.11.1]: exit status 1
	[ERROR ImagePull]: failed to pull image [k8s.gcr.io/kube-proxy-amd64:v1.11.1]: exit status 1
	[ERROR ImagePull]: failed to pull image [k8s.gcr.io/pause:3.1]: exit status 1
	[ERROR ImagePull]: failed to pull image [k8s.gcr.io/etcd-amd64:3.2.18]: exit status 1
	[ERROR ImagePull]: failed to pull image [k8s.gcr.io/coredns:1.1.3]: exit status 1


docker rmi mirrorgooglecontainers/kube-apiserver-amd64:v1.11.1
docker rmi mirrorgooglecontainers/kube-controller-manager-amd64:v1.11.1
docker rmi mirrorgooglecontainers/kube-scheduler-amd64:v1.11.1
docker rmi mirrorgooglecontainers/kube-proxy-amd64:v1.11.1
docker rmi mirrorgooglecontainers/pause:3.1
docker rmi mirrorgooglecontainers/etcd-amd64:3.2.18
docker rmi coredns/coredns:1.1.3
```

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

docker image ls # see flannel pull
kubectl get nodes # status ready

kubectl get pods -n kube-system
```



```
To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  
kubeadm join 10.0.0.30:6443 --token 1mk8bx.u4xr8etbx58eyers --discovery-token-ca-cert-hash sha256:2c6750cb1b254fb60195b49e210e0c2494a2e4b4c58e1b1eed94c8b02217763e --ignore-preflight-errors=Swap
```

