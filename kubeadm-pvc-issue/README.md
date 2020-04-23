1) Option 1 : Create manually volumes and attach it to projects .

Take the example of creating a volume and volumeClaim in the file pv-pvc.yaml 

Then try to install helm chart with the resources that you have created above , take an example of jenkins problem.


2) Option 2 is not yet tried , but it was suggested by a lot of people .
# Local Path provisioner for testing purposes .

This was taken from Rancher github repo :
https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml

check the docs.

e.g. :-
#example of storageClass
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: local-path-pvc
  namespace: default
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: local-path
  resources:
    requests:
      storage: 2Gi

#example for a pod using this pvc :
---
apiVersion: v1
kind: Pod
metadata:
  name: volume-test
  namespace: default
spec:
  containers:
  - name: volume-test
    image: nginx:stable-alpine
    imagePullPolicy: IfNotPresent
    volumeMounts:
    - name: volume
      mountPath: /data
    ports:
    - containerPort: 80
  volumes:
  - name: volume
    persistentVolumeClaim:
      claimName: local-path-pvc
