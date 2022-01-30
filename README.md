# serverless-saas

## What is SaaS?


## What is Serverless SaaS?

## What is a Tenant?
Tenant is....
Tenant isolation
Noisy neighbor
Tenant Tiers

## Silo vs. Pooled
Silo is...
Pooled is ...
Tenant isolation Silo - common constructs
Tenant isolation Pooled - custom and depends on the service


## Control Plane

### Onboarding Tenants
#### 1. User Management
#### 2. Tenant Management
#### 3. Billing Management
Consumption / Tenant Activity
Billable Events
#### 4. Provisioning


### At the Edge
Entry point ....
Tenant Aware Identity
SaaS Identity
block routes
dynamically generated policies


### Single Paint of Glass 
Tenant aware metrics
Tier aware metrics
Multi users:
1. Business users
Care about 

2. Technical users


### Billing



## Application Plane

Micro Services are logical 
1. multiple lambdas represent a single microservice.  Scales independently

Developers shouldnt be aware there is Tenant concept
1. Labmda layers


## CI / CD 
Silo Services
Pooled Services

