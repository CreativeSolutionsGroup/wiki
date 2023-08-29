<img src="./images/logo.jpg" width=100px alt="Doppler Logo"/>

# Doppler

[Home](../../Readme.md) / [Dev Tools](../dev-tools.md) / [Doppler](tool.md)

Welcome to the wonderful world of Doppler. Doppler is the SecretOps tool that we use. It holds onto all of our environment variables and allows easy access to them while still being secure. 

As an analogy from Westin puts it this way. Before we used Google Drive which forced everyone to copy and paste all env files. We gave our mom (Google Drive) our secrets, but when her kid (CSG developers) wanted to use the secret with dad, she just shouted it out. There could have been another kid (anyone on the internet) that tried listening from the street and so far we have just gotten lucky that it hasn't happened yet. With our databases this means that they could have gotten all student info on campus

```mermaid
---
title: Before Doppler
---
%%{init: {'theme':'dark'}}%%
flowchart LR
    M(Mom - Google Drive)
    O(Other Kid - anyone else)
    K(Kid - CSG developer)
    D[(Dad - other software)]
    M --> K <--> D
    M -.-> O <--> D
```

Now with Doppler, when a kid wants to talk to Dad, they must first request the secret from mom. Mom covertly sends the secret to the Kid in a sealed letter riding atop a cat. The kid cannot open the letter but can give it to Dad to start talking to him. In this scenario the other kid would have to capture the cat and find a way to open the letter before being able to talk to dad.

```mermaid
---
title: After Doppler
---
%%{init: {'theme':'dark'}}%%
flowchart LR
    M(Mom - Doppler)
    O(Other Kid - anyone else)
    K(Kid - CSG developer)
    D[(Dad - other software)]
    M -- cat w/ letter --> K <--> D
    M -.-x O
```

## Installation

Instillation is pretty simple. You can visit <https://docs.doppler.com/docs/install-cli> to follow the steps for your specific OS.

When logging in you will want to use your Cedarville account. You should have received an email invitation from Doppler to join our group. If you have not accepted the invitation please do.

## How to use

### Authentication

*If you didn't do this during installation.*

1. Open your terminal and run `doppler login`
2. This should open a web window prompting you to login
3. After logging in go back to your terminal, and it should ask if you want to use it as a global login or for your workspace (it just means your directories branching from the one you are in currently). Choose whichever option applies.

### Project Setup

1. Open a terminal and navigate to the directory containing the project. You may do this by opening a terminal within VSCode.
2. Run `doppler setup`
3. Select the project that you are working in, and then press enter
4. Select the `dev` config, and press enter

### Running commands

The default command for anything now will have `doppler run &&` attached to the front of it. Doppler needs to give you the secrets before you can do things like run the application or access prisma. Here a few examples of popular commands

- `doppler run && prisma studio`
- `doppler run && next dev`
  - This one in particular may be different. Within the `package.json` we are able to setup commands that run a different set of commands. For instance, in most project we setup `yarn dev` to run `next dev`. After adding doppler to the project `yarn dev` will likely run the doppler part as well.

## FAQ
