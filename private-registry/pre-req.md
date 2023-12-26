Create Docker file and build an image
Tag the image 
Push to private dcoker repository using below commands 
pull image from docker private registry
docker login first
docker tag <image> dockerusername/<image>
docker push <dockerusername>/<image>
ex: docker tag httpd veeranarni/test-httpd:latest
docker push veeranarni/test-httpd:latest

need to setup secrets first
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

#Pull image from ecr private registry

aws ecr get-login-password --region us-east-1


aws ecr get-login-password --region us-east-1 | kubectl create secret docker-registry ecr-secret \
--docker-server=042309865848.dkr.ecr.us-east-1.amazonaws.com \
--docker-username=gprashanth \
--docker-password=stdin

apiVersion: v1
kind: Pod
metadata:
  name: private-reg
spec:
  containers:
  - name: private-reg-container
    image: 042309865848.dkr.ecr.us-east-1.amazonaws.com/frontend:latest
  imagePullSecrets:
  - name: ecr-secret 
