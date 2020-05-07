# Setting up AWS EKS Cluster

The Amazon Elastic Kubernetes Service (EKS) is the AWS service for deploying, managing and scaling containerized applications with Kubernetes.


## Download kubectl
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin
```

## Setup kubectl autocomplete
```
source <(kubectl completion bash) # setup autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell
```

## Download the aws-iam-authenticator
```
wget https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.3.0/heptio-authenticator-aws_0.3.0_linux_amd64
chmod +x heptio-authenticator-aws_0.3.0_linux_amd64
sudo mv heptio-authenticator-aws_0.3.0_linux_amd64 /usr/local/bin/heptio-authenticator-aws
```

## Install the AWS CLI tool
```
sudo apt install -y python3-pip awscli && pip3 install --upgrade --user awscli
```

## Modify providers.tf

Choose your region.


## Terraform apply
```
terraform init
terraform plan
terraform apply
```

## Configure kubectl
```
mkdir -p ~/.kube
terraform output kubeconfig > ~/.kube/config
aws eks --region <region> update-kubeconfig --name terraform-eks-demo
```

## Configure config-map-auth-aws
```
terraform output config-map-aws-auth > ~/config-map-aws-auth.yaml
kubectl apply -f ~/config-map-aws-auth.yaml
```

## Check and see nodes coming up
```
kubectl get nodes
```
## Admin user is created by default and full permissions on all namespaces

## Create namespace for user-1 and user-1
```
kubectl create ns user-1
kubectl create ns user-2
```
## Create role for user-1 and user-2
```
kubectl create role user-1 --resource=* --verb=* -n user-1
kubectl create role user-2 --resource=* --verb=* -n user-2
```
## Create role binding for the users
```
kubectl create rolebinding user-1 --role=user-1 --user=user-1 -n user-1
kubectl create rolebinding user-2 --role=user-2 --user=user-2 -n user-2
```
## Update configmap.... using kubectl edit –n kube-system configmap config-map-aws-auth.yaml

## Auto-update DNS records in a private Route53 zone using ExternalDNS

## Deploying Traefik Ingress Controller
```
kubectl apply –f traefik-deploy.yaml
kubectl apply –f traefik-rbac.yaml
```

## Creating an IAM role and policy for your service account on AWS
## Set up a hosted zone on AWS Route53

## Deploy ExternalDNS
```
kubectl apply -f external-dns.yaml
```

### Verify ExternalDNS works (Ingress example)
```
kubectl apply -f  test-ingress.yaml
```
## Verify ExternalDNS works (Service example)
```
kubectl apply -f websvc.yaml
kubectl run –generator=run-pod/v1 web-server –image=nginx
kubectl expose pod web-server –name=web-server –port=80
```

## To run commands permanently as a specific user in the current session, update the AWS_PROFILE environment variable as shown below
```
export AWS_PROFILE=user-1
```

## Destroy
Make sure all the resources created.
```
terraform destroy
```

