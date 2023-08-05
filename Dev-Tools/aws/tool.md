<img src="./images/logo.png" width=100px alt="aws Logo"/>

# AWS (Amazon Web Services)

[Home](../../Readme.md) / [Dev Tools](../dev-tools.md) / [AWS](tool.md)

AWS is our cloud service. It is separate from all IT infrastructure, and works as our main system for anything hosted. If you are wondering where any data or applications live, they live in AWS.

It handles our frontend (websites), backend (business logic), and database (data storage).

## Installation

There is no installation needed for AWS. AWS is a web service. Depending on your executive, they will either issue everyone on the team an account, or give out accounts to specific people only. Please contact your executive to understand if you have/need an account.

https://us-east-2.signin.aws.amazon.com/

Our account ID: 177987852765

## How to use

Navigate to: https://us-east-2.signin.aws.amazon.com/ and place the account ID given under Installation in the box.

Next, if you have credentials, input your username and password.

We use 4 main services.

1. Lightsail (backend, serverful services)
2. Amplify (frontend, serverless services)
3. RDS (database, postgres)
4. Route 53 (DNS management)

### Lightsail deployment
First, ask yourself... should you really be deploying serverful? Only do this if you require application logic that preserves state. The only times where this is required currently is prolonged socket connections.

We deploy everything to Lightsail via docker. See https://aws.amazon.com/blogs/aws/lightsail-containers-an-easy-way-to-run-your-containers-in-the-cloud/ for an example of how to package your application. Here is the CSG standard for packaging applications: https://github.com/CreativeSolutionsGroup/smart-events-api/blob/main/Dockerfile

The most important thing that you should do is make sure that this process is automated. Please see [here](https://github.com/CreativeSolutionsGroup/smart-events-api/blob/main/.github/workflows/docker-publish.yml) for how Smart Events API does this.

### Amplify Deployment
***NOTE*** Env variables are set up specially! Please see other environments on Amplify for how we do this.

https://docs.aws.amazon.com/amplify/latest/userguide/deploy-nextjs-app.html

### RDS
RDS is a beast. Esssentially, we have 2 branches: `dev` and `prod`, which correspond to temporary data and production data. As a developer, you should never have access to prod data. Please ask you executive if you believe you need access to this data before doing anything with it.

As a developer, you should have access to `dev` to create and delete data and databases. Mess this up as much as you want, as long as it does not interfere with other developers. Again, ask your executive for credentials into the dev database.

### Route 53
You will probably never have to interact with this. You may need to assign a static CNAME record with a Lightsail instance to get a nice looking URL.

https://documentation.unbounce.com/hc/en-us/articles/360059868872-Setting-Up-Your-CNAME-with-Amazon-Route-53-AWS-

## FAQ

### Where do frontend or NextJS applications go?
All frontend applications go on Amplify.

### Where do backend or NodeJS applications go?
All backend applications go on Lightsail.

### Where do I deploy a new database?
Currently, we are using RDS. For a new project, please create a new database on both the `dev` and the `prod` branches that are present in RDS.

### How do I get credentials into RDS?
Usually the executives will have the information available. Developers should not be able to create `prod` databases. Developers may have admin credentials into the `dev` branch, however.

### Where do I manage domain names or purchase additional domain names?
Additional domain names go on Route 53. Every service (most importantly, Amplify) has ways of mapping to domains, so please don't manually create `A record`s.

https://docs.aws.amazon.com/amplify/latest/userguide/to-add-a-custom-domain-managed-by-amazon-route-53.html
