kubeadm cannot make auto-provisioning , and does not create dynamic storageClass.

storageClass default is to create persistent volume , if you are using aws,gcp,azure then there is predefined kubernetes , check the docs https://kubernetes.io/docs/concepts/storage/storage-classes/

So the issue is consistent for every installation you should create the volume and the pvc manually then install the chart with the set the storageClass as the pv created and pvCLaimed as in pvc in helm installation .

For example : 
	Make volume and persistent volume for as in the example  pv-pvc.yaml
	Name the volume and volumeClaim as your needs .

Apply in helm installations the map for the pv, pvc.
Have a look at helm-jenkins-example-installation.md as an example
