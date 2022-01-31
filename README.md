# serverless-saas

## What is SaaS?
SaaS is a business model not a technical architecture....

## What is Serverless SaaS?
As you guest it, Serverless SaaS is using AWS Serverless Services and applying it to SaaS.  Why does SaaS and Serverless fit well togehter?  You want to ensure revenue of the tenant is greatern than the cost of tenant...
Agility is key to SaaS and Serverless provides this bc ... no need to foucs on scaling polices, availability, much of that is handled, so you spend more time writing code that matters to your business and differenates you rather than infrastructure.
...

## Basic Vocabulary of SaaS

### What is a Tenant?
Tenant is....
Tenant isolation
Noisy neighbor
Tenant Tiers

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

