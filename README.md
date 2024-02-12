# aks-terraform-starter

This terraform code deploys a minimal AKS cluster.

## Requirements

You will need the following installed:

- [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/)

## Get Started

### 1. Authenticate with your Azure Account

Run `az login` to authenticate with your Azure Account.

### 2. Deploy the infrastructure with Terraform

Update the defaults in `./variables.tf`.

``` bash
terraform apply
```

[!IMPORTANT]  
You can run `terraform plan` first to see what all resources will be deployed.

### 3. Connect Kubectl to the deployed cluster

After `terraform apply` is done running, you will get the following output:

``` bash
Apply complete! Resources: 8 added, 0 changed, 0 destroyed.

Outputs:

client_certificate = <sensitive>
client_key = <sensitive>
cluster_ca_certificate = <sensitive>
cluster_password = <sensitive>
cluster_username = <sensitive>
host = <sensitive>
key_data = <sensitive>
kube_config = <sensitive>
kubernetes_cluster_name = "cluster-upright-tapir"
resource_group_name = "rg-upright-tapir"
```

Make a note of the `kubernetes_cluster_name`

``` bash
az aks get-credentials --resource-group learning-aks-rg --name <kubernetes_cluster_name>
```

The above command will save the file in default `.kube\config` directory, to get `kubeconfig` file in the specific location use the following:

```bash
az aks get-credentials --resource-group learning-aks-rg --name <kubernetes_cluster_name> --file <specific_location>
```

### 4. Create an app with a deployment and service

``` bash
kubectl apply -f app.yaml
```

## Your App

You can check what pods are running in your cluster:

``` bash
kubectl get pods
```

To get the external IP for your load-balancer, you can:

``` bash
kubectl get service aks-sample-linux-service
```

## Author

- GitHub - [Rishab Kumar](https://github.com/rishabkumar7)
- Twitter - [Rishab Kumar](https://x.com/rishabincloud)