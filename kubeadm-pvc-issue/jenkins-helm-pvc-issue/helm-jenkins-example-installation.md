helm installation jenkins stable .

1) apply the yaml file pv-pvc.yaml 
2) Check pvc if the volume is Bound
3) Accoriding the docs in jenkins please apply the pv and pvc as follows :

helm install jenkins stable/jenkins  --set persistence.enabled=true --set persistence.storageClass=pv-name  --set persistence.existingClaim=pvc-name --set persistence.annotati    ons=storageclass.kubernetes.io/is-default-class:"true" --set master.adminPassword=your-desired-pass --set master.serviceType=NodePort

real data example :
helm install jenkins stable/jenkins  --set persistence.enabled=true --set persistence.storageClass=jenkins-pv  --set persistence.existingClaim=jenkins-pvc --set persistence.annotati    ons=storageclass.kubernetes.io/is-default-class:"true" --set master.adminPassword=mypass --set master.serviceType=NodePort

Please note for creating jenkins on VM you should expose the service type as NodePort in order to connect to jenkins GUI.
