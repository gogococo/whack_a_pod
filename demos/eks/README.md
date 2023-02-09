# Implementation steps 
## Pre Steps
- Install (with your package manager of choice) - AWS cli, Terraform, Helm & Kubernetes. 
- Deploy the Terraform
- `terraform init`
- `terraform plan`
- `terraform apply`


# Set your KubeConfig to the cluster we created
`aws eks update-kubeconfig --region us-east-2 --name ${ClusterName}`

- Deploy the Ingress 
`kubectl apply -f ingress.yaml`

## Get kubeconfig (example command)
`aws eks update-kubeconfig --region us-east-2 --name whack-a-pod-CYlVLiZ2`

## Deploy Ingress
`kubectl apply -f ingress.yaml`
`kubectl apply -f rbac.yaml`

## Deploy the API
`kubectl apply -f api-deployment.yaml`

## Deploy the Game
`kubectl apply -f game-deployment.yaml`

## Deploy the Admin pods
`kubectl apply -f admin-deployment.yaml`

## Troubleshooting Helpful Commands!

# Get config in yaml 
`kubectl get deploy deploymentname -o yaml`


# Get Logs 
`kubectl logs pod/admin-deployment-74dc98ff78-hp9dm -f -n whack-a-pod`

# Get more information!
`kubectl describe deployment game-deployment -n whack-a-pod`
`kubectl describe ingress ingress-wap -n whack-a-pod`

`kubectl cluster-info`

`kubectl exec -it -n whack-a-pod game-deployment-d67b9f989-4qspn -- /bin/bash`


# Resources to Share!
* (terraform-aws-eks-blueprints)[https://github.com/aws-ia/terraform-aws-eks-blueprints]
