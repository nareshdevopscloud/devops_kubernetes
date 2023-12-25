Create Docker file and build an image
Tag the image 
Push to private dcoker repository using below commands 
----------------------------------------------------
docker login first
docker tag <image> dockerusername/<image>
docker push <dockerusername>/<image>
ex: docker tag httpd veeranarni/test-httpd:latest
docker push veeranarni/test-httpd:latest
----------------------------------------------
     -------------- need to setup secrets first-------
kubectl create secret docker-registry regcred --docker-server=<your-registry-server> --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>

kubectl get secrtes 


apiVersion: v1
kind: Pod
metadata:
  name: private-reg
spec:
  containers:
  - name: private-reg-container
    image: <your-private-image>
  imagePullSecrets:
  - name: regcred (secretname)
