# Mono-Repos

This is not for any specific mono-repo but rather a general guide to how to work with them.

## Initialization

This shouldn't need to happen often but if you need to create a new mono-repo you can do so here. You may also look to the [Turbo Repo](https://turbo.build/repo/docs/getting-started/create-new) website for updated instructions. Otherwise follow the instructions below.

### Create a new Turbo Repo Project

Start by running the following command in the folder you want to create the project in.

```bash
npx create-turbo@latest
```

It will ask two questions. Respond with:

1. `y` to install the Turbo repo package
2. `./` for the project location
3. `yarn` for the package manager

### Add Prisma to mono-repo

Using Prisma as the ORM is how we work at CSG, so you need a way to access the information for all of the applications. In the mono-repo sense it works almost like its own little project. Follow the steps below to add Prisma to the mono-repo with accompanying commands.

Start by coping going into the `packages` directory and coping the `ui` folder and renaming it to `db`. Now go into the `db` folder.

Delete the `turbo` folder and add a new folder named `prisma`. Inside of the `prisma` folder create a new file named `schema.prisma`. This is where you will put your Prisma schema. The schema will be the same as it would be in a normal Prisma project, and the template is as follows.

```typescript
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

You can add models needed for any of your applications here. Individual applications will **NOT** have their own `schema.prisma` file. This is the only one that will exist.

Next, rename the `card.tsx` to `prisma.ts` and update the contents to the following.

```typescript
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

export { prisma };
```

Then, change the `index.tsx` contents to be the following.

```typescript
export { prisma } from "./prisma";
```

Next, update the `package.json` file to the following.

```json
{
  "name": "db",
  "version": "1.0.0",
  "main": "index.js",
  "types": "./index.tsx",
  "license": "MIT",
  "scripts": {
    "db:generate": "prisma generate",
    "db:push": "prisma db push --skip-generate",
    "db:studio": "prisma studio"
  },
  "devDependencies": {
    "@turbo/gen": "^1.10.12",
    "@types/node": "^20.5.2",
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "eslint-config-custom": "*",
    "react": "^18.2.0",
    "tsconfig": "*",
    "typescript": "^4.5.2"
  },
  "dependencies": {
    "@prisma/client": "^5.4.2",
    "prisma": "^5.4.2"
  }
}
```

Finally, there are two files that need updated in the main directory. Update the files to include the following.

`package.json`:

```json
{
  "scripts": {
    "db:generate": "turbo run db:generate",
    "db:push": "turbo run db:push",
    "db:studio": "turbo run db:studio"
  }
}
```

`turbo.json`:

```json
{
    "db:generate": {
      "cache": false
    },
    "db:studio": {
      "cache": false
    },
    "db:push": {
      "cache": false
    },
    "dev": {
      "dependsOn": [
        "^db:generate"
      ]
    }
}
```

### Add Doppler to mono-repo

Doppler runs very similarly to how it does in a normal project. Make sure to run `doppler setup` in the root of the project.

To make Doppler used implicitly we need to change a few commands within the `package.json` file. Below are the commands that need updated and how. This assumes having already added Prisma to the mono-repo.

```json
{
  "scripts": {
    "dev": "doppler run -- turbo run dev",
    "db:push": "doppler run -- turbo run db:push",
    "db:studio": "doppler run -- turbo run db:studio"
  }
}
```

### Add new applications to mono-repo

Adding new applications is very similar to making a standalone Next.JS application. There will just be a few extra steps to make sure it works with the mono-repo.

First make the new application using the following command from the `apps` directory.

```bash
npx create-next-app@latest
```

Here are the answers to the questions:

1. What is your project named? » example_app_name
2. Would you like to use TypeScript? » Yes
3. Would you like to use ESLint? » Yes
4. Would you like to use Tailwind CSS? » No
5. Would you like to use `src/` directory? » No
6. Would you like to use App Router? (recommended) » Yes
7. Would you like to customize the default import alias (@/*)? » No

After that setup is done, go into the new application folder. There are a few files that need to be updated.

`.eslinrs.js` (full replace):

```typescript
module.exports = {
  extends: ["custom/next"],
};
```

`nextconfig.js` (full replace):

```typescript
module.exports = {
  reactStrictMode: true,
  transpilePackages: ["ui"],
};
```

`package.json` (partial changes):

For this one make sure to update the `name` field. Below is an example of what it could look like. Make sure there is a port specified on the `dev` script. `ui` is required on the `dependencies` field. Not everything may be necessary but it may be ideal to have.

```json
{
  "name": "example_app_name",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev --port 3000", //Make sure this port is unique to the other applications in the mono-repo
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "@emotion/react": "^11.11.1",
    "@emotion/styled": "^11.11.0",
    "@mui/material": "^5.14.14",
    "next": "13.5.6",
    "react": "^18",
    "react-dom": "^18",
    "ui": "*"
  },
  "devDependencies": {
    "@next/eslint-plugin-next": "^13.4.19",
    "@types/node": "^17.0.12",
    "@types/react": "^18.0.22",
    "@types/react-dom": "^18.0.7",
    "eslint-config-custom": "*",
    "tsconfig": "*",
    "typescript": "^4.5.3"
  }
}
```

`tsconfig.json` (full replace):

```json
{
  "extends": "tsconfig/nextjs.json",
  "compilerOptions": {
    "plugins": [{ "name": "next" }]
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

### Add Authentication to mono-repo

This is still a work in progress
