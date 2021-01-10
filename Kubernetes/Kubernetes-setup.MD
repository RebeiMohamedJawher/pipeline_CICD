Installation de Kubernetes dans AWS ( Master + 2 Nodes slaves) :
   
1. créer EC2 instance ubuntu 16.04 ou 18.04 (t2.medium, 30 GB) pour le master.

2.     # sudo su
       #apt-get install -y apt-transport-https
       #curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add 
       #cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
       #deb http://apt.kubernetes.io/ kubernetes-xenial main
       #EOF
       #apt-get update
       #apt-get install -y docker.io
       #apt-get install -y kubelet kubeadm kubectl kubernetes-cni
3. Now create the ami of this machine
       #kubeadm init
       #exit
       OK! 
       #kubectl get node
       #mkdir -p $HOME/.kube
       #sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
       #sudo chown $(id -u):$(id -g) $HOME/.kube/config
       #kubectl get node
       #kubectl get pods --all-namespaces
Installing a CNI Network.
       #sudo su -
       #sysctl net.bridge.bridge-nf-call-iptables=1
       #export kubever=$(kubectl version | base64 | tr -d '\n')
       #kubectl apply -f https://cloud.weave.works/k8s/net?k8s-version=$kubever
       #exit
       OK!
       #kubectl get nodes
4. Install worker nodes, the first node – Slave 1&2 after doing the some installation before kubeadm init command on the two slaves.
       #sudo su - 
       #kubeadm join 172.31.46.228:6443 --token gbodnd.7w6y6pw3uya25a08 --discovery-token-ca-cert-hash sha256: 106d47fe01795127327b82155e41f1ce457dc0a5eba0c852612a7dac039c4814


