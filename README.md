# Installing Node Exporter on IBM Cloud

This document will describe how to install Node Exporter on IBM Cloud using Kubernetes services.

**Step 1 provision Kubernetes Cluster**

- Click the **Catalog** button on the top

- Select **Service** from the **Catalog**

- Search for **Kubernetes Service** and click on it

  ![Node Exporter2](https://user-images.githubusercontent.com/5286796/106587901-2d8eae00-6570-11eb-9006-eaace4f27f60.png)

- You are now at the Kubernetes deployment page. You need to specify some details about the cluster

- Choose a plan **standard** or **free** , the free plan only has one worker node and no subnet, to provision a standard cluster, you will need to upgrade your account to Pay-As-You-Go

- To upgrade to a Pay-As-You-Go account, complete the following steps:

- In the console, go to Manage > Account.

- Select Account settings; and click Add credit card.

- Enter your payment information, click Next, and submit your information

- Choose **classic** or **VPC** , read the docs and choose the most suitable type for yourself

  ![Node Exporter1](https://user-images.githubusercontent.com/5286796/106587895-2cf61780-6570-11eb-88a3-733e5c110279.png)

- Now choose your location settings,

- Choose **Geography** (continent)

![Node Exporter3](https://user-images.githubusercontent.com/5286796/106587887-2b2c5400-6570-11eb-9006-0df5feae0762.png)

-   Choose 	Single or Multizone, in single zone your data is only kept in on 	datacenter, on the

​      other hand with Multizone it is distributed to multiple zones, thus safer in an unforeseen

​      zone failure

- If you wish to use Multizone please set up your account with[VRF

- If at your current location selection, there is no available Virtual LAN, a new VLAN will be created for you
- Choose a Worker node setup or use the preselected one, set Worker node amount per zone
- Choose **Master Service Endpoint**. In VRF-enabled accounts, you can choose private-only to make your master accessible on the private network or via VPN tunnel. Choose public-only to make your master publicly accessible. When you have a VRF-enabled account, your cluster is set up by default to use both private and public endpoints.
   Give desired **tags** to your cluster, for more information visit tags
- Click **create**
   • Wait for your cluster to be provisioned
   • Your cluster is ready for usage

**Step 2 Deploy IBM Cloud Block Storage plug-in**

The Block Storage plug-in is a persistent, high-performance iSCSI storage that you can add to your apps by using Kubernetes Persistent Volumes (PVs).

- Click the **Catalog** button on the top

- Select **Software** from the catalog

- Search for **IBM Cloud Block Storage plug-in** and click on it
  
   • On the application page Click in the dot next to the cluster, you wish to use
   • Click on Enter or Select Namespace and choose the default Namespace or use a custom one (if you get error please wait 30 minutes for the cluster to finalize)
   
   
   
- Give a **name** to this workspace

- Click **install** and wait for the deployment



# **Step 3 **Installing **Node Exporter**

The [node exporter](https://github.com/prometheus/node_exporter) can read system-level statistics about bare-metal nodes or virtual machines and export them for Prometheus.

Using a [DaemonSet](http://kubernetes.io/docs/admin/daemons/), Kubernetes can run one node exporter per cluster node, and expose the node exporter as a service.

Download the [node exporter daemon set manifest](https://coreos.com/assets/blog/promk8s/node-exporter.yaml) and deploy it:

```sh
$ kubectl create -f node-exporter.yaml
```

```sh
daemonset "node-exporter" created
```

Verify that four node exporter pods have been started:

```sh
$ kubectl **get** pods
```

```sh
NAME READY STATUS RESTARTS AGE
```

```sh
node-exporter-4r4vq 1/1 Running 0 1m
```

```sh
node-exporter-6n2ah 1/1 Running 0 1m
```

```sh
node-exporter-9x57u 1/1 *Running* 0 1m
```

```sh
node-exporter-dk99a 1/1 Running 0 1m
```

```sh
prometheus-1189099554-6ah3y 1/1 Running 0 1h
```

**Introduction**

This chart bootstraps a prometheus [node exporter](http://github.com/prometheus/node_exporter) deployment on a [Kubernetes](http://kubernetes.io/) cluster using the [Helm](https://helm.sh/) package manager.

**Installing the Chart**

To install the chart with the release name my-release:

```sh
$ helm install --name my-release stable/prometheus-node-exporter
```

The command deploys node exporter on the Kubernetes cluster in the default configuration. The [configuration](https://github.com/helm/charts/tree/master/stable/prometheus-node-exporter#configuration) section lists the parameters that can be configured during installation.

**Uninstalling the Chart**

To uninstall/delete the *my-release* deployment:

```sh
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

**Upgrading Chart**

```sh
# Helm 3 or 2
```

```sh
$ helm upgrade [RELEASE_NAME] [CHART] --install
```

## Configuring

```sh
# Helm 2
```

```sh
$ helm inspect values prometheus-community/prometheus-node-exporter
```

```sh
# Helm 3
```

```sh
$ helm show values prometheus-community/prometheus-node-exporter
```