`Steps for Mac`

- Install kubectl, minikube and docker
- Run following command in a terminal: 
  `minikube tunnel`

`To build and update image`

Since we are pushing images to aws ecr, we need to login first

aws ecr get-login-password --region us-east-2 --profile aws_ashutosh | docker login --username AWS --password-stdin 312854552697.dkr.ecr.us-east-2.amazonaws.com

Now build and push

docker build -t ashutoshkubertest:v1.0 .  
docker tag ashutoshkubertest:v1.0 312854552697.dkr.ecr.us-east-2.amazonaws.com/ashutoshkubertest:v1.0.0
docker push 312854552697.dkr.ecr.us-east-2.amazonaws.com/ashutoshkubertest:v1.0.0 

`To run pods and check pods`

kubectl apply -f k8s

kubectl get pods -n staging 

`To generate AWS secret for kubernetes:`

kubectl create secret docker-registry regcred \
--docker-server=312854552697.dkr.ecr.us-east-2.amazonaws.com \
--docker-username=AWS \
--docker-password=$(aws ecr get-login-password --profile aws_ashutosh) \
--namespace=staging

`To delete all resources of a namespace`

kubectl delete all --all --namespace staging
