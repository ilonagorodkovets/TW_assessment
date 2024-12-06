# Getting started with Redis

## Table of contents
- [Overview](#overview)
- [Deploy Redis from Service Catalog](#deploy-redis-from-service-catalog)
- [Check the information about the Redis connection in Google Cloud Console](#check-the-information-about-the-redis-connection-in-google-cloud-console)
- [Check the information about the Redis connection via Cloud Shell Terminal and gcloud CLI](#check-the-information-about-the-redis-connection-via-cloud-shell-terminal-and-gcloud-cli)
- [Test the Redis connection](#test-the-redis-connection)
- [Update and deprovision a Terraform deployment](#update-and-deprovision-a-terraform-deployment)
- [Useful resources](#useful-resources)

## Overview
Memorystore for Redis provides a fully-managed service powered by the Redis in-memory data store to build application caches that provide sub-millisecond data access.

The solution from Service Catalog provides an additional private network configuration.

## Quick start using Service Catalog
To get started with Redis:
1. In [the Google Cloud console](https://console.cloud.google.com/getting-started), go to [Service Catalog](https://console.cloud.google.com/catalog), type **Redis** in the search box, and select **[CloudApp] Redis**.<br>
>To log in, use the EPAM account (*Your_Name@epam.com*) and select your project (*EPM-< tenant >-ANTHOS*) to deploy the Redis solution.<br>

![assets/redis_1.png](redis_1.png)

2. Read the description and click **DEPLOY**.<br>
![assets/redis_2new.png](redis_2new.png)

3. Configure the parameters and click **PREVIEW AND DEPLOY**.<br>
>[Redis AUTH](https://cloud.google.com/memorystore/docs/redis/about-redis-auth) is always enabled for the Service Catalog solution due to security risks in Shared VPC.<br>

![redis_3new.png](redis_3new.png)

| Parameter | Description | Example |
| --------- | ----------- | ------- | 
| **Deployment name** | Readable unique name for Redis deployment. | epm-acme-redis-01 |
| **instance_id** | Name of your Redis instance. | epm-acme-redis-01 |
| **network_project_id**| Project ID of VPC where to create the instance.<br> - You can find your project ID on [the main page](https://console.cloud.google.com/welcome).<br> - In the case of Shared VPC, it can be shared with your project. Check shared networks [here](https://console.cloud.google.com/networking/networks/list?pageTab=SHARED_SUBNETS).||
| **vpc_name**| VPC name to create instance within selected project.<br> - You can find the VPC name in [the VPC menu](https://console.cloud.google.com/networking/networks/list) tab.<br> - In the case of Shared VPC, it can be shared with your project. Check shared networks [here](https://console.cloud.google.com/networking/networks/list?pageTab=SHARED_SUBNETS).||
| **tier** | Determines availability, cost, and performance.<br> A basic tier is lower cost and doesn't provide high availability.<br> A standard tier supports automatic failover for high availability and up to 5 read replicas for scaling reads.<br> Possible values: BASIC, STANDARD_HA. | BASIC |
| **memory_size_gb** | Redis memory size in GiB. | 1 |
| **replica_count** | Read replica mode READ_REPLICAS_DISABLED or READ_REPLICAS_ENABLED.<br> Can only be specified when trying to create the instance. If disabled, the read endpoint won't be provided, and the instance cannot scale up or down the number of replicas. | READ_REPLICAS_DISABLED |
| **redis_version** | The version of Redis software. Possible values: REDIS_6_X, REDIS_7_0. | REDIS_6_X |
| **transit_encryption_mode** | The TLS mode of the Redis instance.<br> Possible values: SERVER_AUTHENTICATION, DISABLED.| DISABLED |
| **persistence_mode**| Automatically takes RDB snapshots at the specified interval and recovers data from the last available RDB snapshot when the instance is restarted.<br> Possible values: RDB, DISABLED.| DISABLED|
|**rdb_snapshot_period**|Available snapshot periods for scheduling: ONE_HOUR, SIX_HOURS, TWELVE_HOURS, TWENTY_FOUR_HOURS. | ONE_HOUR|
|**redis_config**|Memorystore documentation for [the list of supported parameters](https://cloud.google.com/memorystore/docs/redis/reference/rest/v1/projects.locations.instances#Instance.FIELDS.redis_configs).|{<br>maxmemory-policy = "volatile-lru"<br>}|

4. Click **DEPLOY** when the button gets highlighted.
Wait until the deployment is completed.<br>
![assets/redis_4new.png](redis_4new.png)
5. To check the installation, do one of the following:<br>
    a. In the GCP console, go to [Memorystore](https://console.cloud.google.com/memorystore/redis/instances).<br>
    b. In the [terminal](https://cloud.google.com/shell/docs/launching-cloud-shell), use [gcloud CLI](https://cloud.google.com/sdk/docs/install-sdk).<br>
A Redis instance is listed; save its `HOST` value.<br>

Specify your PROJECT_ID here.

```
export PROJECT_ID=or2-msq-epm-paas-b-t1iylu
```

```
gcloud redis instances list --region=europe-west3 --project=$PROJECT_ID
```
 
```disable-copy
INSTANCE_NAME      VERSION    REGION        TIER         SIZE_GB  HOST            PORT  NETWORK                   RESERVED_IP       STATUS  CREATE_TIME
epm-acme-redis-01  REDIS_7_0  europe-west3  STANDARD_HA  1        100.100.250.12  6379  epm-paas-poc-shared-vpc1  100.100.250.8/29  READY   2023-10-27T11:46:27
```

Get `authString` of the created instance and save it.

```
gcloud redis instances get-auth-string epm-acme-redis-01 --region=europe-west3 --format="value(authString)"
```

```disable-copy
09b28ca2-85ac-4bfe-9e14-abc1871445b9
```

Try to connect from the GKE cluster in the same VPC using the saved `HOST` and `authString`.

- Run a Redis container.

```
kubectl run -i --tty redis --image=redis --restart=Never -- bash
```

- Call the `redis-cli` command and use the `HOST` value from the created instance to connect.

```
redis-cli -h 100.100.250.12 -a 09b28ca2-85ac-4bfe-9e14-abc1871445b9
```

- Get the instance info.

```
info
```
 
```disable-copy
Server
redis_version:7.0.12
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:d34a72c39ad5196e
redis_mode:standalone
...
```

- Exit from the instance and the Redis container using this command. 

```
exit
```

Now, Redis is ready to use.

## Updating and deprovisioning
For more information on updating a terraform deployment, see the [official Google documentation](https://cloud.google.com/service-catalog/docs/view-and-launch#update_terraform).<br>

For more information on deprovisioning a terraform deployment, see the [official Google documentation](https://cloud.google.com/service-catalog/docs/view-and-launch#deprovision_a_terraform_deployment).

## Useful resources
- [Memorystore for Redis official documentation](https://cloud.google.com/memorystore/docs/redis)
- [Redis documentation](https://redis.io/docs/)
