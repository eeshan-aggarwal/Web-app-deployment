# Web-app-deployment

Step 1: Provision Cloud Infrastructure Using Terraform

Clone the repository containing the Terraform files.
Run the following commands to initialize and apply the Terraform plan:

terraform init
terraform apply

This will provision the VPC, Subnet, and EKS cluster. Note the EKS cluster endpoint output.


Step 2: Set up Kubernetes Cluster

Install kubectl and configure it to use your EKS cluster:

aws eks --region us-west-2 update-kubeconfig --name web-app-cluster


Step 3: Deploy Kubernetes Resources

1. Deploy the web application and Prometheus:


kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f prometheus-configmap.yaml

2. Verify the application is running:

kubectl get pods
kubectl get svc

Step 4: Access the Web Application

- Once the service is exposed, access the web application via the external LoadBalancer IP or DNS name.

Step 5: Access Prometheus Dashboard

- Prometheus will be available on port 9090 (you may need to expose this through a service or port-forwarding if testing locally):

kubectl port-forward deployment/prometheus 9090:9090