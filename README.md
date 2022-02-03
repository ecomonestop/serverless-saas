# serverless-saas

## What is SaaS?
SaaS is a business model not a technical architecture.  Its the creation of a service experience for customers that focuses on zero downtime, regular updates, and closer connection with customers.

**Staying agile and getting features to customers faster**

Its a system where all tenants are managed and operated through a single, unified experience. This means that every tenant is running the same version of the software, they all get deployments at the same time, they are all onboarded through the same process, and they are all managed through a single operational experience, which applies to all tenants. This how SaaS providers stay agile taking features to market faster as they are not maintaining separate versions of the product, reinventing the wheel on non-differentiating activities, but instead focusing on your business domain and instantly taking this value to all customers in a single deployment.

**Targeting Customer Segments via tiers**

Tiers in SaaS business model is common.  E.g. Basic vs. Standard vs. Premium packages.  Your tiering strategy will align with the different market segments you are targeting.  Each Tier has its own value proposition.  

**Metering / pay for what you use pricing monetization**

For customers, “paying for what you use” is a value proposition in itself.  SaaS has a concept of a “tenant”, which enables this business model.   In a SaaS system, you are expected to perform “tenant aware” operations such as publishing billable events with tenant information attached.  Furthermore, consumption of a tenant is also captured. This allows customers to have a pricing model that is more tightly coupled to the value and load they are placing on a SaaS system.


## What is Serverless SaaS?
As you guest it, Serverless SaaS is using AWS Serverless Services and applying it to SaaS.  Why does SaaS and Serverless fit well togehter?  

**Paying for what you use pricing is natural in serverless**

In Serverless, paying for only what you use is the pricing model.  E.g. When you execute a Lambda function you are only paying for the duration that function is running. This aligns with SaaS model as you can charge your customer for value they consume and nothing more.  In traditional archecture, i.e. Ec2 instances, you do not have this luxary.  


**Agility is built into serverless**

In serverless, no need to focus on scaling polices, availability, much of that is handled for you. So you spend more time writing code that matters to your business and differentiate you rather than infrastructure.  This makes you more agile enabling you to react to market needs quicker.

**Tiering basics built in**

Features in serverless not originally built for tiering, but lends itself nicely for this use case:
1.	API gateway – You have concept of a usage plan.  This usage plan can throttle users if they send in too many requests (e.g. Basic tiers would def want to do this).  Furthermore, usage plan also has concept of quotas, which can be used to prevent lower tiers from taking up more resources than desired from the upper tiers.
2.	Lambda – Lambda has a concept called reserve concurrency and it can be used to limit the consumption of a given tenant tier.  On the opposite side of this spectrum, Lambda has a concept called Provisioned concurrency, which can be used for Premium tiers to ensure that the Lambda is “warm” and can respond to requests with lower latency

## Basic Vocabulary of SaaS

### What is a Tenant?
Customers who sign up for your SaaS product are represented as tenants in your system.  Upon signing up, the tenant typically is designated as the admin and can add other users, all of which would be operating under the same tenant. 

A few other tenant related topics:
   
   - Tenant isolation ensures that each tenant is prevented from accessing another tenant’s resources.
   - Noisy neighbor is where a tenant of your system places load on the system’s resources that have an adverse effect on other tenants of the system.  E.g. Basic tier user with poor throttling controls places signficant load on your system effecting a premium tier tenant.  
   - Tenant Tiers - tiers give ability to target market segments, providing separate pricing and experiences to a spectrum of customer profiles

### Isolation strategies - Silo vs. Pooled
Silo is...
Pooled is ...
Your system will likely be a hybrid
Pros / Cons of Silo and Pooled
Tenant isolation Silo - common constructs
Tenant isolation Pooled - custom and depends on the service

### Control Plane vs. Application Plane
Need both to have a true SaaS solution
High level control plane is
High level application plane is


## Control Plane

### Onboarding Tenants
Single, automated, repeatable process...
#### 1. User Management
#### 2. Tenant Management
#### 3. Billing Management
#### 4. Provisioning

### At the Edge
Entry point ....
Tenant Aware Identity / SaaS Identity
1. custom claims
dynamically generated policies
block routes
throttling - typically based on tiers


### Metering and Billing
Consumption / Tenant activity
Billable Events
Correlating Consumption with AWS Bill
Billing Architecture

### Tenant aware Metrics
Metrics should include tier, tenant, service 
Should have both System and App metrics all enriche with tier, tenant, service data
Architecture of instrumentation, ingestion, and aggregation of metrics 


### Single Paint of Glass for SaaS Provider
Tenant aware metrics
Tier aware metrics
Multi users:
1. Business users
Care about 
2. Technical users
How to keep costs of tenant in line with revenue its generating for the business?

### Control Plane integration with Application Plane
How coupled should this be?
A few options for this integration:



## Application Plane

Micro Services are logical 
1. multiple lambdas represent a single microservice.  Scales independently

Decisions on isolation is at the microservice level
1. Example of Resource level isolation
2. Example of Item level isolation - Course grain access required for static policies. At runtime, policy for tenant is injected

How to make the isolation decision?
Many factors, e.g. tiers - could turn silo per tier for example using AWS Lambda, you can use reserve concurrency to limit the consumption of a given tenant tier e.g. basic tier gets less and premium gets more, ...

Isolation could be different for compute and storage within same microservice

Developers shouldnt be aware there is Tenant concept
1. Labmda layers
Examples of client (microservice) using shared libraries (tenant aware code) from lambda layers


## Testing multi-tenant capabilities of your SaaS application
Should test extreemes like attempt for a basic tier to consume tons of resources.  Does your system handle that well? i.e other tiers effected?, high bill?


## CI / CD 
Silo Services
Pooled Services

