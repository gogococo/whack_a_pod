# Steps to run the EKS Whack A Pod Demo

## Cluster Set Up
1. Install (with your package manager of choice) - AWS cli, Terraform, Helm & Kubernetes. 

2. Deploy the Terraform
    - `terraform init`
    - `terraform plan`
    - `terraform apply`

    When Terraform finishes, it will output some values including `cluster_name`. 

    You can get these values again by running `terraform output` from the `./infrastructure` directory. 

3. Set your KubeConfig to the cluster we created

    `aws eks update-kubeconfig --region us-east-2 --name ${cluster_name}`

4. Deploy Ingress:

    `kubectl apply -f ingress.yaml`

    `kubectl apply -f rbac.yaml`

## Application Deployment

1. Deploy the Game

    `kubectl apply -f game-deployment.yaml`

2. Deploy the Admin

    `kubectl apply -f admin-deployment.yaml`

3. Deploy the API - these pods are the moles that we'll be whacking!

    `kubectl apply -f api-deployment.yaml`

4. Get the address to play the game!

    `kubectl get ing -n whack-a-pod`

    To play the game, go to the address outputted from the above command. 


### Troubleshooting Helpful Commands!

- Get config in yaml:

    `kubectl get deploy deploymentname -o yaml`

-  Get Logs: 

    `kubectl logs pod/admin-deployment-74dc98ff78-hp9dm -f -n whack-a-pod`

- Get more information!

    `kubectl describe deployment game-deployment -n whack-a-pod`

`kubectl describe ingress ingress-wap -n whack-a-pod`

`kubectl cluster-info`

`kubectl exec -it -n whack-a-pod game-deployment-d67b9f989-4qspn -- /bin/bash`

`kubectl logs -n kube-system -f aws-load-balancer-controller-7fd75bc756-vw8qd`
`kubectl explain ingress`

`kubectl get ing -A` 


# Additional Resources!
* (terraform-aws-eks-blueprints)[https://github.com/aws-ia/terraform-aws-eks-blueprints]
* (aws-load-balancer-controller)[https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/]
* (EKS Workshop)[https://www.eksworkshop.com/]
* (KubeCtl Explore)[https://github.com/keisku/kubectl-explore]
