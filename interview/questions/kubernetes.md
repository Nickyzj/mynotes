https://coding.imooc.com/class/chapter/198.html#Anchor

https://github.com/liuyi01/kubernetes-starter

https://github.com/liuyi01/imooc-docs/blob/master/gitlab-install.md

```shell
    1  cd tool/
    2  ll
    3  cd kubernetes-bins/
    4  pwd
    5  exit
    6  apt-get remove docker docker-engine docker.io
    7  sudo apt-get remove docker docker-engine docker.io
    8  sudo add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    9  sudo  apt-get update
   10  su -i
   11  sudo -i
   12  ll
   13  cd tool/
   14  ll
   15  tar -zxvf kubernetes-bins.tar.gz
   16  echo $PATH
   17  cd ..
   18  ll
   19  vim .bashrc
   21  source .bashrc
   22  pwd
   23  git clone https://github.com/liuyi01/kubernetes-starter.git
   24  ll
   25  cd kubernetes-starter/
   26  ll
   27  cd kubernetes-simple/
   28  ll
   29  cd all-node/
   30  ll
   31  cat kube-calico.service
   32  cd ../../..
   33  ll
   34  cd kubernetes-starter/
   35  ll
   36  vim config.properties
   
   41  sudo -i
   48  sudo vim /etc/hosts
   50  sudo /etc/hostname
   51  sudo hostname server02
   52  sudo nano /etc/hostname
   53  cat /etc/hostname
   54  sudo systemctl restart systemd-logind.service
   55  hostnamectl set-hostname server02

   60  cd kubernetes-starter/
   61  vim config.properties
   62  ./gen-config.sh simple
   63  find target/ -type f
   64  cp ~/kubernetes-starter/target/master-node/etcd.service /lib/systemd/system/
   65  sudo cp ~/kubernetes-starter/target/master-node/etcd.service /lib/systemd/system/
   66  sudo systemctl enable etcd.service
   67  sudo mkdir -p /var/lib/etcd
   68  sudo service etcd start
   69  journalctl -f -u etcd.service
   70  sudo cp target/master-node/kube-apiserver.service /lib/systemd/system/
   71  sudo systemctl enable kube-apiserver.service
   72  sudo service kube-apiserver start
   73  journalctl -f -u kube-apiserver
   74  sudo cp target/master-node/kube-controller-manager.service /lib/systemd/system/
   75  sudo systemctl enable kube-controller-manager.service
   76  sudo service kube-controller-manager start
   77  journalctl -f -u kube-controller-manager
   78  sudo cp target/master-node/kube-scheduler.service /lib/systemd/system/
   79  sudo systemctl enable kube-scheduler.service
   80  sudo service kube-scheduler start
   81  journalctl -f -u kube-scheduler
   82  sudo -i
   83  cd ..
   84  ll
   85  vim .bashrc
   86  source .bashrc
   88  echo $PATH
   89  ll /home/jizheng/tool/kubernetes-bins

   95  kubectl config set-cluster kubernetes  --server=http://10.0.0.27:8080
   96  kubectl config set-context kubernetes --cluster=kubernetes
   97  kubectl config use-context kubernetes
   98  cat ~/.kube/config
   99  sudo ~/tool/kubernetes-bins/calicoctl get ipPool -o yaml
  100  sudo  vi /lib/systemd/system/docker.service
  101  sudo systemctl daemon-reload
  102  sudo service docker restart
  103  sudo ~/tool/kubernetes-bins/calicoctl node status
  104  ll
  105  calicoctl get ipPool -o yaml

  110  sudo visudo
  111  calicoctl get ipPool -o yaml
  112  sudo calicoctl node status
  113  exit
  114  journalctl -f -u kube-apiserver
  115  netstat -ntlp
  116  cat /lib/systemd/system/kube-apiserver.service
  117  sudo docker ps
  120  ps docker logs -f 6ec13a99caeb
  121  sudo docker logs -f 6ec13a99caeb
  122  sudo calicoctl node status
  123  netstat -natp|grep ESTABLISHED|grep 179
  124  kubectl get pods
  125  kubectl version
  126  kubectl get nodes
  128  kubectl run kubernetes-bootcamp --image=jocatalin/kuberenetes-bootcamp:v1 --port 8080
  129  kubectl get deployments
  131  kubectl get pods -o wide
  133  kubectl delete deployments kubernetes-bootcamp
  134  kubectl run kubernetes-bootcamp --image=jocatalin/kubernetes-bootcamp:v1 --port 8080
  135  kubectl get deploy
  136  kubectl get pods -o wide

  144  kubectl get deploy
  145  kubectl describe deploy kubernetes-bootcamp
  146  kubectl proxy
  147  kubectl scale deploy kubernetes-bootcamp --replicas=4
  148  kubectl get deploy
  149  kubectl get pods -o wide
  150  kubectl scale deploy kubernetes-bootcamp --replicas=2
  151  kubectl get pods
  152  kubectl get pods -o wide
  153  kubectl describe deploy
  154  kubectl set image deploy kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
  155  kubectl rollout status deploy kubernetes-bootcamp
  156  kubectl describe deploy
  157  cd ..
  158  ll
  159  mkdir services
  160  cd services/
  161  ll
  162  vim nginx-pod.yaml
  163  kubectl create -f nginx-pod.yaml
  164  kubectl get pods
  165  kubectl get pods -o wide
  166  kubectl proxy
```

```shel
    1  ls
    2  pwd
    3  exit
    4  apt-get update
    5  apt-get install     apt-transport-https     ca-certificates     curl     software-properties-common
    6  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
    7  apt-get install -y docker-ce
    8  apt-get install -y docker-ce --allow-unauthenticated
    9  cd /etc/ap
   10  cd /etc/apt/
   11  vi sources.list
   12  apt-get update
   13  apt-get install -y docker-ce
   14  $ add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   15  add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   16  apt-get install -y docker-ce
   17  apt-cache madison docker-ce
   18  apt-get install -y docker-ce=17.09.1~ce-0~ubuntu
   19  add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   20  apt-get install -y docker-ce
   21  sudo echo "deb https://download.docker.com/linux/ubuntu zesty edge" > /etc/apt/sources.list.d/docker.list
   22  sudo apt update && sudo apt install docker-ce
   23  history
   24  systemctl daemon-reload
   25  service docker status
   26  service docker restart
   27  ufw disable
   28  cat <<EOF > /etc/sysctl.d/k8s.conf
   29  net.ipv4.ip_forward = 1
   30  net.bridge.bridge-nf-call-ip6tables = 1
   31  net.bridge.bridge-nf-call-iptables = 1
   32  EOF
   33  sysctl -p /etc/sysctl.d/k8s.conf
   34  hostname -I
   35  pwd
   36  cd ..
   37  ll
   38  cd usr
   39  ll
   40  cd ..
   41  ll
   42  cd var
   43  ll
   44  cd ..
   45  ll
   46  cd home
   47  ll
   48  cd jizheng
   49  ll
   50  mkdir tool
   51  cd tool/
   52  pwd
   53  cd ..
   54  ll
   55  chmod 777 tool/
   56  ll
   57  cd tool/
   58  ll
   59  exit
   60  journalctl -f -u kube-scheduler
   61  cp target/all-node/kube-calico.service /lib/systemd/system/
   62  cd /home/jizheng/
   63  ll
   64  cd kubernetes-starter/
   65  ll
   66  cp target/all-node/kube-calico.service /lib/systemd/system/
   67  systemctl enable kube-calico.service
   68  service kube-calico start
   69  journalctl -f -u kube-calico
   70  docker ps
   71  calicoctl node status
   72  /home/jizheng/tool/kubernetes-bins/calicoctl node status
   73  /home/jizheng/tool/kubernetes-bins/calicoctl get ipPool -o yaml
   74  kubectl config set-cluster kubernetes  --server=http://10.0.0.27:8080
   75  exit
   76  service etcd stop && rm -fr /var/lib/etcd/*
   77  exit
   78  wget -q --show-progress --https-only --timestamping   https://pkg.cfssl.org/R1.2/cfssl_linux-amd64   https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64
   79  chmod +x cfssl_linux-amd64 cfssljson_linux-amd64
   80  mv cfssl_linux-amd64 /usr/local/bin/cfssl
   81  mv cfssljson_linux-amd64 /usr/local/bin/cfssljson
   82  cfssl version
   83  pwd
   84  cd /home/jizheng/
   85  mkdir -p /etc/kubernetes/ca
   86  cp kubernetes-starter/target/ca/ca-config.json /etc/kubernetes/ca
   87  cp kubernetes-starter/target/ca/ca-csr.json /etc/kubernetes/ca
   88  cd /etc/kubernetes/ca
   89  cfssl gencert -initca ca-csr.json | cfssljson -bare ca
   90  ls
   91  mkdir -p /etc/kubernetes/ca/etcd
   92  cp /home/jizheng/kubernetes-starter/target/ca/etcd/etcd-csr.json /etc/kubernetes/ca/etcd/
   93  cd /etc/kubernetes/ca/etcd/
   94  cfssl gencert         -ca=/etc/kubernetes/ca/ca.pem         -ca-key=/etc/kubernetes/ca/ca-key.pem         -config=/etc/kubernetes/ca/ca-config.json         -profile=kubernetes etcd-csr.json | cfssljson -bare etcd
   95  ls
   96  cd /home/jizheng/kubernetes-starter/
   97  vimdiff kubernetes-simple/master-node/etcd.service kubernetes-with-ca/master-node/etcd.service
   98  cp /home/jizheng/kubernetes-starter/target/master-node/etcd.service /lib/systemd/system/
   99  systemctl daemon-reload
  100  service etcd start
  101  journalctl -f
  102  ETCDCTL_API=3 etcdctl   --endpoints=https://192.168.1.102:2379    --cacert=/etc/kubernetes/ca/ca.pem   --cert=/etc/kubernetes/ca/etcd/etcd.pem   --key=/etc/kubernetes/ca/etcd/etcd-key.pem   endpoint health
  103  ETCDCTL_API=3 etcdctl   --endpoints=https://192.168.1.102:2379    --cacert=/etc/kubernetes/ca/ca.pem   --cert=/etc/kubernetes/ca/etcd/etcd.pem   --key=/etc/kubernetes/ca/etcd/etcd-key.pem \
  104  ETCDCTL_API=3 etcdctl   --endpoints=https://server02:2379    --cacert=/etc/kubernetes/ca/ca.pem   --cert=/etc/kubernetes/ca/etcd/etcd.pem   --key=/etc/kubernetes/ca/etcd/etcd-key.pem
  105  ETCDCTL_API=3 etcdctl   --endpoints=https://server02:2379    --cacert=/etc/kubernetes/ca/ca.pem   --cert=/etc/kubernetes/ca/etcd/etcd.pem   --key=/etc/kubernetes/ca/etcd/etcd-key.pem   endpoint health
  106  ETCDCTL_API=3 etcdctl   --endpoints=https://10.0.0.27:2379    --cacert=/etc/kubernetes/ca/ca.pem   --cert=/etc/kubernetes/ca/etcd/etcd.pem   --key=/etc/kubernetes/ca/etcd/etcd-key.pem   endpoint health
  107  ls
  108  pwd
  109  ls /etc/kubernetes/ca
  110  mkdir -p /etc/kubernetes/ca/kubernetes
  111  cp /home/jizheng/kubernetes-starter/target/ca/kubernetes/kubernetes-csr.json /etc/kubernetes/ca/kubernetes/
  112  cd /etc/kubernetes/ca/kubernetes/
  113  cfssl gencert         -ca=/etc/kubernetes/ca/ca.pem         -ca-key=/etc/kubernetes/ca/ca-key.pem         -config=/etc/kubernetes/ca/ca-config.json         -profile=kubernetes kubernetes-csr.json | cfssljson -bare kubernetes
  114  ls
  115  echo "8afdf3c4eb7c74018452423c29433609,kubelet-bootstrap,10001,\"system:kubelet-bootstrap\"" > /etc/kubernetes/ca/kubernetes/token.csv
  116  cp /home/jizheng/kubernetes-starter/target/master-node/kube-apiserver.service /lib/systemd/system/
  117  systemctl daemon-reload
  118  service kube-apiserver start
  119  journalctl -f -u kube-apiserver
  120  cp /home/jizheng/kubernetes-starter/target/master-node/kube-controller-manager.service /lib/systemd/system/
  121  systemctl daemon-reload
  122  service kube-controller-manager start
  123  journalctl -f -u kube-controller-manager
  124  service kube-scheduler start
  125  journalctl -f -u kube-scheduler
  126  mkdir -p /etc/kubernetes/ca/admin
  127  cp /home/jizheng/kubernetes-starter/target/ca/admin/admin-csr.json /etc/kubernetes/ca/admin/
  128  cd /etc/kubernetes/ca/admin/
  129  cfssl gencert         -ca=/etc/kubernetes/ca/ca.pem         -ca-key=/etc/kubernetes/ca/ca-key.pem         -config=/etc/kubernetes/ca/ca-config.json         -profile=kubernetes admin-csr.json | cfssljson -bare admin
  130  ls
  131  kubectl config set-cluster kubernetes         --certificate-authority=/etc/kubernetes/ca/ca.pem         --embed-certs=true         --server=https://10.0.0.27:6443
  132  kubectl config set-credentials admin         --client-certificate=/etc/kubernetes/ca/admin/admin.pem         --embed-certs=true         --client-key=/etc/kubernetes/ca/admin/admin-key.pem
  133  kubectl config set-context kubernetes         --cluster=kubernetes --user=admin
  134  kubectl config use-context kubernetes
  135  cat ~/.kube/config
  136  kubectl get pods
  137  kubectl get componentstatus
  138  mkdir -p /etc/kubernetes/ca/calico
  139  cp /home/jizheng/kubernetes-starter/target/ca/calico/calico-csr.json /etc/kubernetes/ca/calico/
  140  cd /etc/kubernetes/ca/calico/
  141  cfssl gencert         -ca=/etc/kubernetes/ca/ca.pem         -ca-key=/etc/kubernetes/ca/ca-key.pem         -config=/etc/kubernetes/ca/ca-config.json         -profile=kubernetes calico-csr.json | cfssljson -bare calico
  142  ls
  143  scp -r /etc/kubernetes/ca jizheng@server02:/etc/kubernetes/ca/
  144  scp -r /etc/kubernetes/ca/ jizheng@server02:/etc/kubernetes/ca/
  145  scp -r /etc/kubernetes/ca/ jizheng@server01:/etc/kubernetes/ca/
  146  ls
  147  cd ..
  148  ll
  149  scp -r /etc/kubernetes/ca/ jizheng@10.0.0.26:/etc/kubernetes/ca/
  150  scp -r /etc/kubernetes/ca/ root@10.0.0.26:/etc/kubernetes/ca/
  151  scp -r /etc/kubernetes/ca/ jizheng@server01:~/ca/
  152  scp -r /etc/kubernetes/ca/ jizheng@server01:/home/jizheng/ca/
  153  ll /etc/kubernetes/ca
  154  ping server01
  155  cat /etc/hosts
  156  vi /ect/hosts
  157  vi /etc/hosts
  158  scp -r /etc/kubernetes/ca/ jizheng@server01:~
  159  scp -r /etc/kubernetes/ca/ jizheng@server01:/etc/kubernetes/ca/
  160  scp -r /etc/kubernetes/ca/ jizheng@server03:~
  161  cp /home/jizheng/kubernetes-starter/target/all-node/kube-calico.service /lib/systemd/system/
  162  systemctl daemon-reload
  163  service kube-calico start
  164  calicoctl node status
  165  journalctl -f -u kube-calico
  166  calicoctl node status
  167  ll
  168  scp -r /etc/kubernetes/ca jizheng@server01:~/ca
  169  ll
  170  cd calico/
  171  ll
  172  cd ..
  173  scp -r /etc/kubernetes/ca jizheng@server01:~
  174  scp -r /etc/kubernetes/ca jizheng@server03:~
  175  calicoctl node status
  176  kubectl -n kube-system get clusterrole
  177  cat /etc/kubernetes/ca/kubernetes/token.csv
  178  kubectl create clusterrolebinding kubelet-bootstrap          --clusterrole=system:node-bootstrapper --user=kubelet-bootstrap
  179  kubectl get csr
  180  kubectl get csr|grep 'Pending' | awk '{print $1}'| xargs kubectl certificate approve
  181  kubectl get csr
  182  kubectl get csr|grep 'Pending' | awk '{print $1}'| xargs kubectl certificate approve
  183  kubectl get csr
  184  calicoctl node status
  185  kubectl get csr
  186  kubectl -n kube-system get clusterrole
  187  cat /etc/kubernetes/ca/kubernetes/token.csv
  188  kubectl get csr
  189  kubectl create -f /home/jizheng/kubernetes-starter/target/services/kube-dns.yaml
  190  kubectl -n kube-system get pods
  191  kubectl get node
  192  kubectl run kubernetes-bootcamp --image=jocatalin/kubernetes-bootcamp:v1 --port=8080
  193  kubectl get deploy
  194  kubectl get pod
  195  kubectl logs kubernetes-bootcamp-6b7849c495-tqwj6
  196  kubectl describe pod kubernetes-bootcamp-6b7849c495-tqwj6
```

```shell
  194  ip netns
  195  ip netns list
  196  ip netns add r1
  197  ip netns add r2
  198  ip netns list
  199  ip netns exec r1 ifconfig
  200  ip netns exec r1 ifconfig -a
  201  ip netns exec r2 ifconfig -a
  202  ip link help
  203  ip link add veth1.1 type veth peer name veth1.2
  204  ip link show
  205  ip link set dev veth1.2 netns r1
  206  ip link show
  207  ip netns exec r1 ifconfig -a
  208  ip netns exec r1 ip link set dev veth1.2 name eth0
  209  ip netns exec r1 ifconfig -a
  210  ifconfig veth1.1 10.1.0.1/24 up
  211  ifconfig
  212  ip netns exec r1 ifconfig eth0 10.1.0.2/24 up
  213  ip netns exec r1 ifconfig
  214  ping 10.1.0.2
  215  ip link set dev veth1.1 netns r2
  216  ifconfig
  217  ip netns exec r2 ifconfig -a
  218  ip netns exec r2 ifconfig veth1.1 10.1.0.3/24 up
  219  ip netns exec r2 ifconfig
  220  ip netns exec r2 ping 10.1.0.2
```

```shell
查看容器动态端口映射
iptables -t nat -vnL
docker port gitlab
```



