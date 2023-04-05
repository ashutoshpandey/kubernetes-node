`Steps for Mac`

- Install kubectl, minikube and docker
- Run following command in a terminal: 
  `minikube tunnel`

`To run pods and check pods`

kubectl apply -f k8s/1-express.yaml   

kubectl get pods -n staging 

`To generate AWS secret for kubernetes:`

aws ecr get-login-password --region us-east-2 --profile aws_ashutosh | docker login --username AWS --password-stdin xxxxx.dkr.ecr.us-east-2.amazonaws.com