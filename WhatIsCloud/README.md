# What is the Cloud?


- [What is the Cloud?](#what-is-the-cloud)
  - [Definition](#definition)
  - [NIST Definition:](#nist-definition)
  - [History of Cloud Computing.](#history-of-cloud-computing)
  - [Cloud - 4 Service Types:](#cloud---4-service-types)
  - [4 Types of Cloud Deployment Models:](#4-types-of-cloud-deployment-models)
  - [What can they do](#what-can-they-do)
  - [Essential Characteristics](#essential-characteristics)
  - [Advantages of Adopting Cloud (Business Standpoint):](#advantages-of-adopting-cloud-business-standpoint)
  - [Disadvantages of Adopting Cloud (Business Standpoint):](#disadvantages-of-adopting-cloud-business-standpoint)
  - [Cloud Providers:](#cloud-providers)
    - [Amazon Web Services (AWS)](#amazon-web-services-aws)
    - [Microsoft Azure](#microsoft-azure)
    - [Google Cloud Platform (GCP)](#google-cloud-platform-gcp)
  - [Cloud Provider Marketshare:](#cloud-provider-marketshare)
  - [Four Pillars of DevOps](#four-pillars-of-devops)
  - [OPEX vs CAPEX](#opex-vs-capex)

## Definition

 Instead of owning and maintaining physical servers and infrastructure, developers and organizations can use resources and services provided by a third-party cloud service provider.


## NIST Definition:

- Convenient, on-demand network access
- To a shared pool of configurable computing resources
- Rapidly allocated and released with minimal management effort or service provider interaction(easily scalable - self orchestrating)

## History of Cloud Computing.

Cloud computing has its roots in the 1960s with mainframe computing but saw significant evolution in the 2000s. In 2006, Amazon Web Services (AWS) launched, introducing Infrastructure as a Service (IaaS) and kickstarting the modern era of cloud computing. This was followed by the emergence of other major players like Microsoft Azure and Google Cloud Platform. 

Throughout the 2010s, cloud computing witnessed rapid adoption, diversification of services (IaaS, PaaS, SaaS), and the rise of containerization with technologies like Docker. Serverless computing gained traction in the mid-2010s with the introduction of AWS Lambda and Azure Functions. The 2020s brought continued innovation, including advancements in edge computing, AI, and machine learning. Organizations increasingly embraced multi-cloud strategies to leverage services from multiple providers, marking the ongoing evolution of cloud computing. </br>

## Cloud - 4 Service Types:

 * Infrastructure as a Service (IaaS): Provisioning of complex foundational resources such as networks, storage and virtual machines - build applications from the ground up.

* Platform as a Service (PaaS): Provisioning of a platform that includes tools and services for application development such as databases, development frameworks - environment that simplify software development.

* Software as a Service (SaaS): SaaS delivers software applications over the internet. Users can access these applications through a web browser without needing to install or maintain any software on their local devices.

* Function as a Service (FaaS) / Serverless Computing: Allows developers to run individual functions or pieces of code in response to events without managing the infrastructure. Users only pay for the actual compute resources consumed during the execution of these functions.

![Alt text](../READMEImages/CloudServiceDiff.png)

</br>

## 4 Types of Cloud Deployment Models:
- **Public Cloud:**
  Services and infrastructure are provided by an external company, accessible over the internet. Users pay for the resources they use on a flexible, pay-as-you-go basis.

- **Private Cloud:**
  Cloud services and infrastructure are dedicated to a single organization, offering greater control and security. It can be hosted on-premises or by a third-party provider.

- **Hybrid Cloud:**
  Combines elements of public and private clouds, allowing data and applications to be shared between them. Provides flexibility by using both on-premises and public cloud resources.

- **Multi-Cloud:**
  Involves using services from multiple cloud providers, offering redundancy and flexibility. Organizations can choose the best services for specific needs, avoiding reliance on a single provider.


## What can they do
- **Scalable Infrastructure:**
  Provision and scale computing resources on-demand.

- **Web Hosting and Application Deployment:**
  Host websites and deploy applications without physical servers.

- **Data Storage and Backup:**
  Reliable and scalable storage solutions with backup features.

- **Development and Testing:**
  Quickly create development and testing environments.

- **Big Data Analytics:**
  Process and analyze large datasets for insights.

- **Machine Learning and AI:**
  Leverage cloud-based ML and AI services.

- **Internet of Things (IoT):**
  Manage and analyze data from IoT devices.

- **Collaboration and Communication:**
  Cloud-based tools for teamwork and communication.

- **Content Delivery and Streaming:**
  Use CDNs for fast and reliable content delivery.

- **Serverless Computing:**
  Deploy and run code without managing infrastructure.

- **Desktop Virtualization:**
  Implement Virtual Desktop Infrastructure (VDI) in the cloud.

- **Security and Compliance:**
  Utilize cloud security services and adhere to compliance.

- **Cost Optimization:**
  Pay for only the resources and services used.

- **Disaster Recovery:**
  Implement robust disaster recovery solutions.

- **Hybrid and Multi-Cloud Strategies:**
  Build hybrid or multi-cloud architectures for flexibility.

</br>

## Essential Characteristics

- Combined computation/resources - Resource Pooling
- Rapid Elasticity - (Quick Scalability relative to demand without human intervention)
- Accessibility - Broad network access
- Measured Service - (Management)
- Self-Service - On-demand self-service

## Advantages of Adopting Cloud (Business Standpoint):

- **Cost Savings:** Cloud eliminates upfront hardware costs and allows pay-as-you-go pricing.
- **Scalability and Flexibility:** Easily scale resources based on demand for efficient workload management.
- **Accessibility and Collaboration:** Remote access fosters collaboration among distributed teams.
- **Rapid Deployment:** Cloud enables quick deployment of applications and infrastructure.
- **Innovation and Technological Edge:** Cloud providers offer cutting-edge technologies for competitive advantage.
- **Security and Compliance:** Reputable providers invest in robust security measures and compliance certifications.

## Disadvantages of Adopting Cloud (Business Standpoint):

- **Security Concerns:** Entrusting data to a third party raises security considerations.
- **Dependency on Service Providers:** Reliability depends on the performance of chosen providers.
- **Data Transfer Costs:** While storage is cost-effective, data transfer costs can accrue.
- **Limited Customization:** Public cloud services may have limitations on customization.
- **Potential for Vendor Lock-In:** Proprietary technologies may lead to dependency on specific providers.
- **Downtime and Reliability:** Cloud services, despite high reliability, are not immune to downtime.


## Cloud Providers:

### Amazon Web Services (AWS)

**Advantages:**
- Largest and most mature cloud provider.
- Extensive range of services.
- Global infrastructure with data centers worldwide.
- Active user community and rich ecosystem.

### Microsoft Azure

**Advantages:**
- Seamless integration with Microsoft products.
- Strong hybrid cloud capabilities.
- Well-suited for enterprise-scale deployments.

### Google Cloud Platform (GCP)

**Advantages:**
- Strengths in data analytics, machine learning, and big data services.
- Extensive global network infrastructure.
- Expertise in containerization and Kubernetes.

## Cloud Provider Marketshare:

- **Amazon Web Services (AWS):**
  - Market Share: 32% to 33% (2021)
  - Position: Leading cloud service provider

- **Microsoft Azure:**
  - Market Share: 20% to 21% (2021)
  - Position: Strong competitor to AWS

- **Google Cloud Platform (GCP):**
  - Market Share: 9% to 10% (2021)
  - Position: Growing steadily, third-largest cloud provider

## Four Pillars of DevOps

**Collaboration:**
Encourages open communication and collaboration among development, operations, and QA teams.

**Automation:**
Emphasizes the use of automation tools to streamline and accelerate the software delivery process.

**Continuous Integration (CI):**
Involves frequent integration of code changes into a repository, to detect and address issues early in development.

**Continuous Delivery/Continuous Deployment (CD):**
Focuses on continuously delivering and, in some cases, deploying software changes to production. Ensures software is always in a deployable state.

## OPEX vs CAPEX

**OPEX (Operating Expenditure):**
- Represents ongoing, day-to-day operational costs.
- Includes recurring expenses deducted in the year incurred.

**CAPEX (Capital Expenditure):**
- Involves investments in long-term assets.
- Capitalized and depreciated over the asset's useful life.

In summary, OPEX covers immediate operational expenses, while CAPEX represents long-term investments with costs spread over time.

