# k8s_drupal
Setup Master & Worker:
apt-get update
apt-get install docker.io

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

On Master::
kubeadm init --apiserver-advertise-address=<private-IP> --pod-network-cidr=192.168.0.0/16 --ignore-preflight-errors=NumCPU


Use this in worker nodes
kubeadm join <copy the hash from master>

In order to established connection:
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Add Networking b/w pods:
kubectl apply -f https://docs.projectcalico.org/v3.11/manifests/calico.yaml (Used Calico)

Browser Access : (Used NodePort here, we need to check Ingress & LB as well)
Create Service IP to access the PODs from outside network:
=>kubectl create service nodeport nginx --tcp=80:80
=> use the nodeport port number with kube master public IP
=> Service IP act as a balencer IP

Get All Name Spaces:
kubectl get pods --all-namespaces
kubectl delete pod --all / pod-name
kubectl delete pvc --all / pvc-name
kubectl delete pv --all / pv-name

Get All Service:
kubectl get svc

Delete App by name:
kubectl delete deployment.apps/drupal
kubectl delete deployment.apps/drupal-mysql

Delete Pod:
kubectl delete pod <pod-key>

Delete service:
kubectl delete service drupal

TODO:
PV/PVC Setup with NFS
https://kubernetes.io/docs/concepts/storage/persistent-volumes/
