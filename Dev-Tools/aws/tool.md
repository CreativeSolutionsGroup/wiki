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
Amplify is how we manage our web applications. It has a serverless functionality that allows us to only pay for what we use.

#### Creating a New App

To create a new app, follow [this](https://docs.aws.amazon.com/amplify/latest/userguide/deploy-nextjs-app.html) guide.

#### Domain Management

To manage a domain for an app, realize that you have to have an application already created.

To manage the domain for Amplify, please note that you should *purchase* your domain through [Route 53](#route-53).

Next, go to the "Domain management" tab under the app settings for the app you are working on. Click "Add domain." By clicking on the textbox, you will see all the domains that you have registered under Route 53. To use them, click on the domain. Accept the default settings and it will automatically create your SSL config for you.

#### Preview Deployments

This process will enable you to get Preview Deployments on an Amplify App. The preview deployment will automatically deploy a pull request on GitHub and put a link to the test deployment into the pull request.

**NOTE:** All instructions will assume this is on Amplify

1. Update Build Settings
   1. Go to `Build Settings` for your application
   2. Use the following commands under `build/commands`
      1. If you are not using Doppler for ENVs then you may ignore those lines.
      2. If you have a problem with Doppler not installing right, make sure your app actually uses Doppler, and try moving the install command into the `preBuild` commands.
      3. Make sure to replace `[replace-with-app-ID]` with the ID of the app. This appears in the URL of your current page, but you can also find it on the general settings under `App ARN` as the last string after a `/`.

New Commands:

```yaml
- curl -Ls https://cli.doppler.com/install.sh | sh 
- if [ "${AWS_BRANCH}" = "main" ]; then doppler setup -t ${DOPPLER_PRD_TOKEN} --no-interactive; fi
- if [ "${AWS_BRANCH}" != "main" ]; then doppler setup -t ${DOPPLER_STG_TOKEN} --no-interactive; fi
- if [ "${AWS_BRANCH}" != "main" ]; then echo "NEXTAUTH_URL=\"https://pr-${AWS_PULL_REQUEST_ID}.[replace-with-app-ID].amplifyapp.com/\"" > .env; fi
- doppler run -- env | grep -e DATABASE_ -e GOOGLE_ -e NEXTAUTH_ -e BUILD_ >> .env
- yarn prisma generate
- yarn run build
```

Example end product used for bz-commendations:

```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - yarn install
    build:
      commands:
        - curl -Ls https://cli.doppler.com/install.sh | sh 
        - if [ "${AWS_BRANCH}" = "main" ]; then doppler setup -t ${DOPPLER_PRD_TOKEN} --no-interactive; fi
        - if [ "${AWS_BRANCH}" != "main" ]; then doppler setup -t ${DOPPLER_STG_TOKEN} --no-interactive; fi
        - if [ "${AWS_BRANCH}" != "main" ]; then echo "NEXTAUTH_URL=\"https://pr-${AWS_PULL_REQUEST_ID}.[replace-with-app-ID].amplifyapp.com/\"" > .env; fi
        - doppler run -- env | grep -e DATABASE_ -e GOOGLE_ -e NEXTAUTH_ -e BUILD_ >> .env
        - yarn prisma generate
        - yarn run build
  artifacts:
    baseDirectory: .next
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

2. Add Doppler environment variables (if utilizing Doppler)
   1. Go into the `Environment variables` tab on the AWS App
   2. Create two new variables
      1. `DOPPLER_STG_TOKEN`
      2. `DOPPLER_PRD_TOKEN`
   3. Navigate to this project in Doppler. Then select the `stg` config.
   4. Select the tab labeled `ACCESS`, and under the `Service Tokens` section, click the `Generate` button.
   5. Name the variable `AWS Amplify`, then click `Generate Service Token`. Don't worry about any of the extra settings.
   6. Copy the generated token, and paste it as the value for `DOPPLER_STG_TOKEN` back on Amplify.
   7. Repeat this for `dev` from step 3.
   8. Now head back to Doppler and select any of the configs for the app.
   9. To make Auth work we need to add a VAR called `BUILD_ENV`. The value for which is `dev` | `stg` | `prd` depending on which config you are in.
   10. Make sure to add the right value to each of the 3 configs.
3. Correct Build Settings for correct Environment variables (Doppler)
    1. To make sure everything builds correctly, you need the correct environment variables.
    2. Navigate to the `Build Settings` tab, and click `edit` on the `amplify.yml` file.
    3. Go to the line that looks like: `- doppler run -- env | grep -e DATABASE_ -e GOOGLE_ -e NEXTAUTH_ -e BUILD_ >> .env`
    4. This line likely needs customized for each app. Open Doppler to the correct project and open any of the configs.
    5. Now edit the build setting to appropriately account for all of the variables. You just need up to the first `_` on each of them.
       1. For an app that has:
          1. AWS_ACCESS_KEY_ID
          2. AWS_SECRET_ACCESS_KEY
          3. GOOGLE_CLIENT_ID
          4. GOOGLE_CLIENT_SECRET
          5. NEXTAUTH_URL
          6. NEXTAUTH_SECRET
          7. BUILD_ENV
          8. DATABASE_URL
          9. TWILIO_API_KEY
          10. TWILIO_NUMBER
          11. TWILIO_SECRET
          12. TWILIO_SID
       2. The line should look like this:
          1. `- doppler run -- env | grep -e AWS_ -e GOOGLE_ -e NEXTAUTH_ -e BUILD_ - DATABASE_ -e TWILIO_ >> .env`
4. Turn on Previews
   1. Now that it will build properly, we need to actually turn on previews.
   2. Back in AWS, open the `preview` tab
   3. Click the `Enable Previews` button
   4. Click `Install GitHub App`. This will navigate you to GitHub.
      1. We already have the GitHub App installed, and this doesn't break anything.
   5. Select the `CreativeSolutionsGroup` option
   6. Scroll down to `Repository Access` and ensure that the repo you are setting up is in the list of selected repositories.
   7. Go back to AWS and there should be a new page that is titled `Previews`.
   8. Click the little circle on the same row as the `main` branch. This should make the circle turn blue and the `Manage` button turn orange.
   9. Click the `Manage` button and turn on the checkbox for `Pull Request Previews`.
   10. Click `Confirm`, and you now have Preview Deployments

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
