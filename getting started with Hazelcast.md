# Getting started with Hazelcast

## Quick overview
You can install Hazelcast with the help of a preconfigured Hazelcast Platform Operator.

Also pay attention to the following:
- For more examples of using a Hazelcast cluster, see the public kb page.
- We are constantly monitoring security issues. You can see the results of these reports on the [Hazelcast Security Benchmark](https://kb.epam.com/display/EPMPAASPUB/Hazelcast+Security+Benchmark) page.

## How to get started
### Prerequisites
1. Create a personal or project namespace using the [Getting Started](https://kb.epam.com/pages/viewpage.action?spaceKey=EPMPAASPUB&title=Getting+Started) guide.
2. Prepare your local workstation using the [How to set up the OpenShift command line tools](https://kb.epam.com/display/EPMPAASPUB/How+to+set+up+the+OpenShift+command+line+tools) guide.
3. **Dive deeper into Hazelcast IMDG**, its limitations and use cases:
    - [FAQ](https://docs.hazelcast.com/imdg/4.1/faq)
    - [Redis replacement](https://hazelcast.com/use-cases/redis-replacement/)
    - Troubleshooting

### Approaches to get started
There are **3 approaches** to using the service:
- via the Web interface
- via Terminal (for example, Bash)
- via the Operator API (in CI/CD pipelines and automation)

You can choose one or any approach depending on your needs. If you prefer to use a simple database and CI/CD processes are not available for your environment, select the first simple option. However, if you intend to use CI/CD pipelines with auto-deployment of Hazelcast instances, use the last approach.

1. **Web Console guidelines**  
Follow these steps to use this service with the OpenShift Web Console in the **Developer** perspective:  
        1. Go to the Web Console using your namespace and select **+Add**.  
        2. Select **All Services** in **Developer Catalog**.  
        3. Then, follow the [Quick start](https://kb.epam.com/display/EPMPAASPUB/Create+a+Hazelcast+cluster) guide.

2. **Terminal guidelines**
Follow these steps to use this service with the OpenShift CLI tool:  
        1. Check that CLI is installed on your PC → the [How to set up the OpenShift command line tools](https://kb.epam.com/display/EPMPAASPUB/How+to+set+up+the+OpenShift+command+line+tools) guide.  
        2. Then, follow the instructions on [Quick start](https://kb.epam.com/display/EPMPAASPUB/Create+a+Hazelcast+cluster) using the OpenShift CLI.

3. **Automation guidelines**  
        1. See an example [here](https://docs.hazelcast.com/operator/5.2/get-started#step-2-start-the-hazelcast-cluster).    
        2. Read CRD spec for available configuration information.   
<code>$ oc explain hazelcast</code>  
<code>#</code>   
<code>$ oc explain managementcenter</code>

>The CloudApp Engine team assumes no responsibility for the performance and stability of the CloudApp Engine Managed Services if any third-party add-ons and/or plugins are introduced at the discretion of a Service User. It is the User's responsibility to conduct compatibility testing.

## Questions?
If you still have questions, create a [request](https://support.epam.com/ess?id=sc_cat_item_guide&table=sc_cat_item&sys_id=8571a1dc476f5958ed13b2bd436d43d1) at support.epam.com.
***
****Early Access***—a Beta version of a fully functional CloudApp Engine Service or Cluster. EA Service is covered by reduced support SLAs and in most cases, CloudApp Engine Observability capabilities would not be available. All workloads of EA services and clusters should take the risk of being shut down with full data loss after an e-mail notice in one-day advance. EA services and clusters are recommended only for development and testing purposes.