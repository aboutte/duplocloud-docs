---
description: Popular and frequently asked questions about DuploCloud
---

# FAQ

{% hint style="info" %}
**NOTICE:** This document provides frequently asked questions related to high-level design and business models. For more detailed technical FAQs, refer to the [AWS FAQ](aws/aws-faq.md), [Azure FAQ](azure/azure-faq.md), or [Google Cloud FAQ](gcp/gcp-faq.md).
{% endhint %}

## Is DuploCloud a SaaS product?

No. DuploCloud is a self-hosted solution deployed within the customer's cloud account. This hosted solution provides the customer with a SaaS-like experience. If the customer desires, DuploCloud can provide a fully managed service to maintain uptime, provide updates, and supply ongoing support.

## How is DuploCloud Portal accessing my cloud infrastructure and how is it secured?

DuploCloud is a self-hosted single-tenant solution deployed within the customer's cloud account. The software runs in a virtual machine (VM) and the VM derives permissions to call the cloud provider using the VM's permissions. For example, in AWS, permissions are derived via an instance profile. In Azure, permissions are derived via managed identity.

The DuploCloud VM and DuploCloud Portal are secured, as is any other workload in the cloud. In addition to SSO login for portal access, the VM runs behind a VPN. Therefore, only internal users can load the portal when connected to a VPN.

## What cloud providers are supported?

DuploCloud supports the following public cloud providers:

* Amazon AWS
* Microsoft Azure
* Google Cloud

## If my company has no DevOps experience, can your company provide services to build out our environment and support us? What level of support does DuploCloud provide?

Absolutely! In fact, more than half of our customers have no DevOps team. With our managed service offering, we handle your deployments, act as the first line of defense for any issues, and are constantly involved in daily tasks like CI/CD updates, etc.

The DuploCloud team acts as your extended DevOps team, assisting with white glove environment setup and daily operations with 24x7 Slack and/or email support. We cover what is supported in the DuploCloud platform, as well as assist with your cloud provider's requirements.&#x20;

After the initial onboarding of the platform, we recommend that you engage the DuploCloud team as your second line of defense by setting up an internal triage process of your own. We can assist you in setting up this process.&#x20;

{% hint style="info" %}
DuploCloud is your extended DevOps team! We are available 24x7 on your Slack channel, by phone, and by email.
{% endhint %}

## Can I make changes directly in the cloud account managed by DuploCloud?

Yes. Many times this is required because DuploCloud may not support all cloud features or configurations. Direct changes to your cloud account can be categorized within the following groups:

### Independent Changes

DuploCloud labels the resources and configurations it manages. If independent changes are being made directly in your cloud provider, DuploCloud does not interfere. However, DuploCloud still monitors changes for compliance and alerts you to any non-compliant configurations.

### Non-conflicting changes to DuploCloud managed resources

For resources that DuploCloud does not directly manage, you make the change directly in your cloud provider. For example, if you add additional forwarding rules to a load balancer created through DuploCloud, DuploCloud does not interfere with the new configuration that you created.&#x20;

### Conflicting Changes to DuploCloud managed resources

For resources that DuploCloud manages, DuploCloud automatically detects the conflicts and either reverts the changes or raises an alert about the inconsistency.

{% hint style="info" %}
DuploCloud provides flexibility when a feature that is not supported by DuploCloud can be programmed directly in your cloud provider. If you are using Terraform, then the DuploCloud provider, as well as the native cloud provider, can be used in tandem. For an example of this use case, see [https://duplocloud.com/white-papers/devops/#PAAS](https://duplocloud.com/white-papers/devops/#PAAS).
{% endhint %}

## Is DuploCloud generating Terraform code behind the scenes to configure the cloud?

No. DuploCloud is calling the cloud provider's API directly. Based on user requirements, the software interacts with the cloud provider API asynchronously, maintaining a [state machine](https://en.wikipedia.org/wiki/Finite-state\_machine) of operations with built-in retries to ensure robustness. Any configuration drift, system faults, security, and compliance controls are monitored continuously by interacting with the cloud provider.

## If DuploCloud is not generating Terraform code behind the scenes, then how can I use Infrastructure-as-code?

The Terraform and DuploCloud Web UIs are layered on top of the DuploCloud platform.

![User Interaction with the DuploCloud Platform](<.gitbook/assets/image (11) (1) (1).png>)

DuploCloud provides an SDK into Terraform called the [DuploCloud Terraform Provider](https://registry.terraform.io/providers/duplocloud/duplocloud/latest). This SDK allows the user to configure their cloud infrastructure using DuploCloud constructs, rather than using lower-level cloud provider constructs. This enables the user to get the benefits of Infrastructure-as-Code, while significantly reducing the amount of code that is needed. The DuploCloud Terraform Provider calls DuploCloud APIs. Our [DevOps white paper](https://duplocloud.com/white-papers/devops) provides detailed examples.

## Am I locked into DuploCloud? If I wanted to move away from DuploCloud, what work do I need to do?

DuploCloud is running in your own cloud account, along with your workloads. DuploCloud is a provisioning system, so stopping DuploCloud does not impact any of your applications and cloud services.

The following is a list of automation constructs managed by DuploCloud, and a summary of what you need to do to maintain them directly, instead of through DuploCloud.

1. Cloud Provider Configuration (Terraform): This involves various cloud services, IAM roles, Security groups, VPC, etc. DuploCloud can export your latest cloud configuration into native Terraform code and state files. Once exported, you maintain the configuration.
2. Kubernetes: All applications and configurations that have been deployed in K8s are available in the form of deployments, StatefulSets, DaemonSet, K8s Secrets, ConfigMaps, etc. One can run `kubectl`commands to export configurations as YAML files and continue to maintain them in the future.
3. Compliance monitoring: DuploCloud uses a third-party SIEM solution called [Wazuh](https://www.wazuh.com). Wazuh is an open-source software platform running in an independent VM in your cloud account, and you have full permission to retain it "as-is." However, going forward, any new systems that need compliance monitoring need to be integrated into the SIEM by you.
4. Diagnostics tools: Tools include Prometheus, Grafana, and Elasticsearch. All of these tools are open source and run in your cloud account. You can continue to manage them directly.

{% hint style="info" %}
If DuploCloud is down, it's similar to having an unavailable DevOps engineer. If you need to opt out of DuploCloud, you are replacing your DevOps management. DuploCloud is neither a PaaS nor a hosted solution, which hosts your workloads.
{% endhint %}

## I don't know IaC (Infrastructure-as-Code). Can I still use DuploCloud?

Yes. DuploCloud's Web UI is a no-code interface for DevOps. You do not need to know IaC or have any cloud expertise to operate it. You simply need to understand the basic constructs in DuploCloud by reading the product documentation.

## **My application developers don't know IaC (Infrastructure-as-Code), but my DevOps engineers do. If my developers make changes via the DuploCloud UI, what happens to the Terraform code my DevOps engineers have written?**

You should create a separation between your developers and your DevOps team. Allowing developers to use the Web UI in non-production development environments, to quickly iterate product changes, can create an inconsistency.&#x20;

In both production and critical non-production environments, the cloud services setup, as well as first-time application deployment, can be done via Terraform code. CI/CD workflows can be built that only update the application (Docker and Lambda) deployments. Any cloud service level change should be done by the DevOps team via Terraform and developers should ask the DevOps team to do the same. Developers should still be able to trigger CI/CD for their application rollouts without DevOps involvement.

## **Should I use low-code or no-code?**

The answer depends on the following key factors:

### How much Developer self-service is required, and are you an operations-centric organization?

Especially in a rapid-growth company environment, where architecture is constantly evolving and services are being constantly updated, there may be a desire to let developers self-service and move fast. This would be a case for no-code. On the other hand, in cases where there is an established operations organization, with centralized requirements, then a low-code Terraform solution may be a better option.

Note that Terraform is a client-side scripting tool and a single-user system, so the scope of a project is limited to one person operating at one time. This can incur constraints if a project has many components and two people cannot operate at the same time, even if they are dealing with completely independent constructs.

### Dealing with a broad scope of changes vs. small just-in-time changes

Terraform projects typically have a broad scope with multiple components. At times, you need to make small targeted changes (for example, a health check URL change). But when the change is being executed, there may be other drifts and the user is forced to resolve them. This can be inconvenient and often the user will make the change in the UI, resulting in further configuration drifts.

{% hint style="info" %}
About half of our customer base uses no-code, while the other half uses Terraform. Ironically, software developer-centric companies prefer no-code because it enables engineers to be agile and focus on their application code. By contrast, in DevOps-centric organizations, the low-code Terraform provider is often used.
{% endhint %}

## How do I use Datadog and others diagnostics tools?

DuploCloud's out-of-the-box diagnostics stack is optional. To integrate with a third-party toolset like Datadog, you follow the toolset's guidelines and deploy collector agents. You can do this as if you are running an application within the respective DuploCloud tenants.

## How will CI/CD work with DuploCloud?

CI/CD is the topmost layer of the DevOps stack. DuploCloud should be viewed as a deployment and monitoring solution that is invoked by your CI/CD pipelines, written with tools such as CircleCI, Jenkins, GitHub Actions, etc. You build images and push them to container registries without involving DuploCloud, but invoke DuploCloud to update the container image. An example of this is in the CI/CD section. DuploCloud offers its own CI/CD tool, as well.

## Do I need an AWS access key for my application when using AWS?

CI/CD is the topmost layer of the DevOps stack. DuploCloud should be viewed as a deployment and monitoring solution that is invoked by your CI/CD pipelines, written with tools such as CircleCI, Jenkins, GitHub Actions, etc. You build images and push them to container registries without involving DuploCloud, but invoke DuploCloud to update the container image. An example of this is in the [CI/CD](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/\~/changes/r966TcV3ISnUcfuJxUa3/ci-cd/continuous-integration-and-deployment-ci-cd) section. DuploCloud offers its own CI/CD tool ([KatKit](ci-cd/katkit/)), as well.

If your application is running in a DuploCloud [Tenant](getting-started/application-focussed-interface/tenant.md) you do not need a long-term credential, such as an AWS access key. After your application is running in the Tenant, test your connection using the AWS CLI to verify access. For more information, see the [AWS FAQ](aws/aws-faq.md).  &#x20;

## With DuploCloud, will we be more secure and compliant out-of-the-box, as opposed to using a default AWS configuration?

Yes. This is a major advantage of using DuploCloud. All controls are mapped to various compliance standards. DuploCloud is also very flexible in enabling you to add custom policies (resource quotas, ability to create public-facing endpoints, etc.)

##
