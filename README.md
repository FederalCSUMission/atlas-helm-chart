
# atlas-helm-chart

This is a Kubernetes Helm Chart that Deploys the Apache Atlas Cluster on Azure Kubernetes Service. Atlas will use Solr for indexing and Cassandra as Backend Storage.

More precisely, it provides:

* solr 7.7.2
* atlas 2.1.1
* cassandra 3.11.3
* zookeeper 3.4.4

# PreRequisites

This post assumes that you have an already running Kubernetes Cluster in Azure Kubernetes Service. If not follow the steps in the link up until you connect to the cluster: [AKS Quickstart](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal?tabs=azure-cli)


# Helm Chart Deployment

Let us go through the Folder Structure of the Helm Chart. The charts folder contains solr, atlas, Cassandra and zookeeper Helm Charts embedded. The Atlas Chart will deploy these charts. 

To deploy the helm chart, clone the repo
```sh
 gh repo clone FederalCSUMission/atlas-helm-chart
```
Note: you may need to create a personal access token. [Classic Personnal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
```sh
helm install --name <release name>  atlas-helm-chart

Sample Example: helm install --name atlas atlas-helm-chart
```
This will run the solr, atlas, Cassandra and zookeeper pods. The Helm Chart for Cassandra, Zookeeper and Solr is taken from Helm Stable Chart repository.

```sh
kubectl get svc -w atlas-helm-chart-<release name>-atlas
```

This will show the status of the loadBalancer to access the ATLAS GUI. The service will be running but it may take up to 10 minutes before you can access the GUI. 

To access the GUI you can go into the Azure portal under "Kubernetes resources" on the left side and click "servcies and ingresses" there you will see your atlas service running and an external IP you can click on which will open a new tab in your browser.