# Create the Self-hosted Gateway

We need to provision the self-hosted gateway in the APIM service.

> NOTE: Provisioning the API Self-hosted gateway is still a manual process through the portal. Eventually, this will 
> be available through the Azure CLI, Terraform, etc.

## Provision the Gateway

![Image of API Self-Hosted Gateway Creation](/assets/apim-gateway-screenshot.png)

Values might look like:

* _Name_ => apim-gateway  
* _Location_ => arc-enabled-cluster  
* _Description_ => This is the on-prem APIM self-hosted gateway for a Kubernetes cluster.

## Get the Install and Config Info

![Image of API Self-Hosted Gateway Creation](/assets/apim-gateway-screenshot-2.png)

After you have provisioned the gateway, you will be able to find the _Deployment... Kubernetes..._ tab with code and information about deploying the gateway.

For the sake of this demo, we split this configuration up into the following files:

* [config.yaml](/04_cluster-config/config-sample.yaml) - this is where we will apply our secrets to the cluster.
* [gateway.yaml](/flux/apim-gateway/gateway.yaml) - this is how we will deploy the gateway itself to Kubernetes.

