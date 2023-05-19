
### VM Setup 
- Download latest version of [Ubuntu server iso image](https://ubuntu.com/download/server)
- Download [VMWare Fusion Player](https://customerconnect.vmware.com/en/evalcenter?p=fusion-player-personal-13) using outlook email.
- Install VMWare Fusion Player in Mac OS X
- Change following settings while creating new Virtual Machines using Ubuntu server images
  - Sharing > Add macOS user folder - rajpalvirk
  - Hard Disk > Increase disk space to 100GB.
  - Check OpenSSL installation
- Shutdown VM after installation and during restart to get rid of start up errors and restart manually

### Disable swap memory
```shell
sudo nano /etc/fstab
```
- add # in front of swap memory line
- save and exit

### Reboot VM
```shell
sudo reboot
```

### Clone repository


### Perform basic kubernetes cluster node setup
```shell
sh kubernetes-common-setup.sh
```

### Install only on Kubernetes Master Node - Control Plane 
#### Kubeadm init
```shell
sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --cri-socket=unix:///var/run/cri-dockerd.sock

```

#### Troubleshooting - Kubeadm
- If you get fatal errors while running kubeadm init command, reset kubeadm init settings and retry
```shell
sudo kubeadm reset --cri-socket=unix:///var/run/cri-dockerd.sock
```
- Rerun kubeadm init command again

#### Using Kubeadm as regular user
```shell
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```