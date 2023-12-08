# Getting started with CloudApp Kubernetes Enterprise

## Before you begin
Before you start working with CloudApp Kubernetes Enterprise, get familiar with the following recommendations:<br>
- **Learn Google Cloud fundamentals**<br>
As an [Application Team engineer](https://docs.cloudapp.epam.com/#/responsibilities) (developer or DevOps engineer), you need to gain basic Google Cloud knowledge. We recommend two learning paths where you can choose the best option for you:<br>

| Options | Google Cloud Skills Boost for Partners links | Estimations |
| ----------- | ----------- | ----------- |
| Fast track path | Required:<br> 1. [Google Cloud Fundamentals: Core Infrastructure](https://partner.cloudskillsboost.google/course_templates/60)<br> 2. [Architecting with Google Kubernetes Engine: Foundations](https://partner.cloudskillsboost.google/course_templates/32)<br> 3. [Architecting with Google Kubernetes Engine: Workloads](https://partner.cloudskillsboost.google/course_templates/34)<br> Optional:<br> 1. [Architecting with Google Kubernetes Engine: Production](https://partner.cloudskillsboost.google/course_templates/33)  | About 10 full-time days (min)<br><br><br><br><br>About 5 full-time days (min)|
| Full path | 1. [Associate Cloud Engineer Certification Learning Path](https://partner.cloudskillsboost.google/journeys/69)<br> 2. [Architecting with Google Kubernetes Engine: Production](https://partner.cloudskillsboost.google/course_templates/33) | About 35 full-time days (min) |

> Make sure that you have approval for learning from your PM or DM.

For more information on GCP Certification and training for EPAM, see [GCP Certification](https://kb.epam.com/display/EPMCEDU/GCP+Certification).

- **Learn architectural aspects of CloudApp Kubernetes Enterprise**<br>
Architectural aspects of CloudApp Kubernetes Enterprise include the following items: 
    - **Regions**<br>
Google Cloud supports a huge list of regions, but we use the regions where EPAM has Interconnects to their on-premise infrastructure. For CloudApp Kubernetes Enterprise, the following regions are available:<br>
        - **EU-WEST3**—Frankfurt, Germany<br>
        - **US-EAST**—Ashburn, Virginia, North America
    - **Networking**<br>
With Anthos architecture, every project leverages shared VPC that has network subnets available from the EPAM network, and vice versa. The Client doesn't need to request additional subnets or EPAM VPN via our support portal, and can use subnets shared with the project. You can check it in the VPC networking service view, for example:<br>
![assets/gettingstartedwithCKE_1.png](assets/gettingstartedwithCKE_1.png)

    - **GKE Autopilot**<br>
By default, we provide GKE Autopilot clusters as the most cost-effective way, where you don't need to manage autoscalers or choose node pools. After activating CloudApp Kubernetes Enterprise (Anthos Fleet), the GKE Autopilot cluster(s) should be available in both tabs:<br>
        - Kubernetes Engine/Clusters<br>
        - Anthos/Fleet management/Clusters<br>

    GKE Autopilot mode is a hands-off, fully managed Kubernetes platform that manages your cluster’s underlying compute infrastructure (without you needing to configure or monitor)—while still delivering a complete Kubernetes experience.<br>
For more information, see [Autopilot is now GKE’s default mode of operation — here’s what that means for you](https://cloud.google.com/blog/products/containers-kubernetes/gke-autopilot-is-now-default-mode-of-cluster-operation).

    - **Anthos Fleet**<br>
Anthos (GKE Enterprise) and Google Cloud use the concept of a fleet to simplify managing multi-cluster deployments. A fleet provides a way to logically group and normalize Kubernetes clusters, helping us uplevel management from individual clusters to entire groups of clusters.<br>
For more information, see [GKE Enterprise (Anthos) fleets management](https://cloud.google.com/anthos/fleet-management/docs).

## Get started with CloudApp Kubernetes Enterprise
To get started with CloudApp Kubernetes Enterprise, do the following:<br>
1. To activate CloudApp Kubernetes Enterprise in GCP, submit the [support request](https://support.epam.com/ess?id=sc_cat_item&sys_id=112bf2234719b1d001d2f59a436d4311).<br>
For that, use the following information:<br>
>:warning: Before you order a cluster, get familiar with the key differences between the Autopilot and Standard cluster types. For more information on their comparison, see the [official Google documentation](https://cloud.google.com/kubernetes-engine/docs/resources/autopilot-standard-feature-comparison).<br><br>When you choose a cluster type, pay attention to the following:<br>- The Autopilot mode doesn't support privileged and root access to containers.<br>- By default, Autopilot goes with minimum and maximum allowed resource requests for each POD. Thus, to deploy a lot of PODs with resource request requirements less than in the Autopilot restrictions, the Standard mode is preferable. For more information on the minimum and maximum resource requests, see the [official Google documentation](https://cloud.google.com/kubernetes-engine/docs/concepts/autopilot-resource-requests#min-max-requests).<br>- Autopilot doesn't fully support some services from Google Cloud Marketplace.<br>- Autopilot sets <code>limits</code> to the values in <code>requests</code>.<br>- DaemonSet doesn't trigger Autopilot scaling.

| Field name | Value | Actions | Example |
| ----------- | ----------- | ----------- | ----------- |
| **Request title** | Manage CloudApp Kubernetes Enterprise powered by Anthos. | Default value | x |
| **Checkbox** | I confirm that I have read and accept the EPAM Cloud Security Policy and EPAM Cloud Terms and Conditions. | Manual input | x |
| **Project** | Enter the Project name or part of it, and then select it from the list provided. | Manual input | EPM-PAAS |
| **Action** | Select **Activate Anthos fleet in GCP** from the list. | Manual input |  x |
| **Estimated monthly cost** | Indicate the estimated monthly cost of running the cloud. This information is needed only to inform you if the threshold of the specified amount is reached. Specify the amount in USD without the $ sign. | Manual input | 1000 |
| **Comments** | Any information you'd like to add. | Manual input | x |
| **Clusters configuration** | To configure clusters:<br>1. In **Clusters configuration**, select **Add**.<br><br>2. In the **Add Row** dialog, specify the cluster configuration.<br>&nbsp;**Cluster name**: Enter a Cluster name.<br>&nbsp;*Important*: The Cluster name you specify will only be used to determine the number of clusters and their parameters. When a cluster is created by EPAM CloudApp Engine team, the Cluster name will be given based on the following template: ```<project name>-Anthos-<region>-<ordinal postfix>```.<br>&nbsp;**Region**: Select the region: Europe or Americas.<br>&nbsp;**Cluster type**: Select the cluster type: [Autopilot](https://cloud.google.com/kubernetes-engine/docs/concepts/autopilot-overview) or [Standard](https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-zonal-cluster).<br><br>3. Select **Add**.<br> :information_source: To deploy several clusters for your Project, go through the described steps for each cluster.<br>To edit the parameters already entered for the cluster, select the ![assets/editrow_1.png](assets/editrow_1.png)**Edit Row** button opposite the corresponding cluster.<br>To delete the parameters already entered for the cluster, select the ![assets/removerow_1.png](assets/removerow_1.png) **Remove Row** button opposite the corresponding cluster.<br>To delete all the parameters already entered for the clusters, select the ![assets/removeall_1.png](assets/removeall_1.png) **Remove All** button.<br><br>If you are new to Public Clouds, we recommend choosing the following settings for your clusters:<br>- Region - Europe<br>- Cluster type - [Autopilot](https://cloud.google.com/kubernetes-engine/docs/concepts/autopilot-overview) | Manual input | ![assets/gettingstartedwithGKE_1new.png](assets/gettingstartedwithGKE_1new.png) |
| **Approver** | Enter the approver's name or part of it, and then select it from the list provided. | Manual input | x |

2. Log in to Google Cloud console.<br>
After the Anthos Fleet activation, you can connect to the GCP project via [Google Cloud console](https://console.cloud.google.com/) with EPAM domain credentials by choosing a particular GCP Project at the top of it (for example, EPM-PAAS).<br>
![assets/gettingstartedwithCKE_2.png](assets/gettingstartedwithCKE_2.png)
3. Set up gcloud CLI.<br>
To manage Google Cloud (gcloud) from CLI, do the following:<br>
a. Install google-cloud-sdk.<br>
For more details, see the [Install the gcloud CLI](https://cloud.google.com/sdk/docs/install) guide.<br>
b. Authorize the gcloud CLI.<br>
`gcloud init`<br>
`gcloud info`<br>
`gcloud projects list`<br>
For more details, see the [Authorize the gcloud CLI](https://cloud.google.com/sdk/docs/authorizing) guide.<br>
c. Configure the gcloud CLI.<br>
`gcloud config list`<br>
`gcloud config set project or2-msq-epm-paas-t1iylu`<br>
For more details, see [gcloud config set](https://cloud.google.com/sdk/gcloud/reference/config/set).<br>
4. Start onboarding.<br>
For reference, see the following how-to guides:<br>
- [First steps with GKE Enterprise](https://docs.cloudapp.epam.com/#/gcpuserguides/firstStepsWithGKEEnteprise)<br>
- [Load balance traffic using Gateway API](https://docs.cloudapp.epam.com/#/gcpuserguides/loadbalancetrafficusingGatewayAPI)<br>
- [Deploying app to GKE](https://docs.cloudapp.epam.com/#/gcpuserguides/deployingapptoGKE)<br>
- [Workload placement-GKE Autopilot](https://docs.cloudapp.epam.com/#/gcpuserguides/workloadplacementGKEAutopilot)<br>
- [Managing GCP IAM and roles](https://docs.cloudapp.epam.com/#/gcpuserguides/manageGCPIAMandroles)<br>
- [Namespaces RBAC Management](https://docs.cloudapp.epam.com/#/gcpuserguides/namespacesRBACManagement)<br>
- [Secrets Management for applications](https://docs.cloudapp.epam.com/#/gcpuserguides/secretsManagementforapplications)<br>
- [GKE Storage](https://docs.cloudapp.epam.com/#/gcpuserguides/gkestorage)<br>
- [Getting started with GitLab Runner](https://docs.cloudapp.epam.com/#/gcpuserguides/gettingstartedwithGitLabRunner)<br>
- [Cloud SQL for PostgreSQL](https://docs.cloudapp.epam.com/#/gcpuserguides/cloudSQLforPostgreSQL)<br>
- Using monitoring ***<img alt="" src="http://static.cdn.epam.com/uploads/64af6d6845a542b3d306573d064482a8/EPM-PAAS/States.svg "/>***<br>
- Using logging ***<img alt="" src="http://static.cdn.epam.com/uploads/64af6d6845a542b3d306573d064482a8/EPM-PAAS/States.svg "/>***<br>



    
