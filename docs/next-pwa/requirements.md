---
title: Requirements 📜
sidebar_label: Requirements 📜
slug: /requirements
---

<head>
  <title>Requirements 📜</title>
</head>

##

Your machine should have [Yarn](https://classic.yarnpkg.com/en/docs/install/#windows-stable) or [Npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) installed.

_Note: Preferable versions_

|       | Version |
| ----- | ------- |
| node  | 16      |
| npm   | 6       |
| yarn  | 1.16    |
| lerna | 4       |

- Check the node and npm version by running following commands.

```sh
node -v
npm -v
```

- Install yarn globally

```
npm i yarn -g
```

## Installation Steps :walking:

### 1. Fork it :fork_and_knife:

You can get your own fork/copy of [Next-PWA](https://github.com/Samagra-Development/Nextjs-PWA) by using the <kbd><b>Fork</b></kbd> button.

### 2. Clone it :busts_in_silhouette:

You need to clone (download) it to a local machine using

```sh
git clone https://github.com/Samagra-Development/Nextjs-PWA
```

> This makes a local copy of the repository in your machine.

Once you have cloned the `Nextjs-PWA` repository in GitHub, move to that folder first using the change directory command.

This will change directory to a folder

```sh
cd Nextjs-PWA
```

Move to this folder for all other commands.

### 3. Set it up :arrow_up:

Run the following commands to see that _your local copy_ has a reference to _your forked remote repository_ in GitHub :octocat:

```sh
git remote -v
```

By running the above command, you can see that the local copy has a reference to the forked remote repository in GitHub.

```
origin  https://github.com/Your_Username/Nextjs-PWA.git (fetch)
origin  https://github.com/Your_Username/Nextjs-PWA.git (push)
```

### 4. Install and Build 💻

- Install dependencies

```
yarn install
```

- Build the code

```
yarn build
```

Browse - http://localhost:3000

### 5. Running the application 🏃‍♂️


- Run application in dev environment

```
yarn run dev 
```

This is implemented through [next-pwa](https://www.npmjs.com/package/next-pwa) and [offline-sync-handler](https://www.npmjs.com/package/offline-sync-handler).

_You can check the detailed demo [here](https://drive.google.com/file/d/12CEFf2M9dOVgwalgG_WIF8cnAvquocLi/view?usp=sharing)_ 