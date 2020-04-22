This is an automated vagrant2.2+VirutalBox5.2 setup for creating kubeadm kubernetes .

The project was modified and rebuilt in order to install 1 Master node and two slave nodes for learning purposes from your machine.

Please note that I am using Ubuntu18.04 image from vagrant.

If you are using machine MacOS or Windows , there will be changes only in installing the docker and kubeadm,kubelete and kubectl .

My localmachine runs on ubuntu 18.04 which I wrote the code to create 3 VMs .

You can change the slave nodes to get  more Nodes in the vagrant file with the hardcode parameter N=2

Default Behaviour:
vagrant can ssh to the VMs, if you would like to ssh directly then you need to edit the file /etc/ssh/ssh_config , and replace :
PasswordAuthentication no
TO => PasswordAuthentication yes
Then do sshd restart : sudo service sshd restart


=> Connecting your local machine to the K8S Master Node Cluster :
1) Grab the .kube file from the Master Node by issuing :
scp -r /home/vagrant/.kube $HOME 
NOTE: If you have more than one cluster then copy it to the Cluster directory .

2) export the kubernetes config env , or add it directly to .bashrc, .zshrc :
export KUBECONFIG=$KUBECONFIG:$HOME/.kube/config
source $HOME/.bashrc or $HOME/.zshrc


!!! Voila , you should be able afterwards to issue the command " kubectl get nodes -o wide " and see the nodes with its IP.



