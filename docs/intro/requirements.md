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
| turbo | 1.9.1   |

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

You can get your own fork/copy of [Sunbird-UCI](https://github.com/samagra-comms/uci-web-channel) by using the <kbd><b>Fork</b></kbd> button.

### 2. Clone it :busts_in_silhouette:

You need to clone (download) it to a local machine using

```sh
git clone https://github.com/samagra-comms/uci-web-channel.git
```

> This makes a local copy of the repository in your machine.

Once you have cloned the `Sunbird-UCI` repository in GitHub, move to that folder first using the change directory command.

This will change directory to a folder

```sh
cd uci-web-channel
```

Move to this folder for all other commands.

### 3. Set it up :arrow_up:

Run the following commands to see that _your local copy_ has a reference to _your forked remote repository_ in GitHub :octocat:

```sh
git remote -v
```

By running the above command, you can see that the local copy has a reference to the forked remote repository in GitHub.

```
origin  https://github.com/Your_Username/uci-web-channel.git (fetch)
origin  https://github.com/Your_Username/uci-web-channel.git (push)
```

### 4. Run it :checkered_flag:

- Install dependencies

```
yarn install or npm install 
```

Browse it on: ```http://localhost:3003```

### 5. Rendering Offline 💻

- Build the code

```
yarn build or npm run build 
```

- Run application in dev environment

```
yarn start or npm run dev 
```

This is implemented through [NextJS](nextjs.org) and [socket-package](https://www.npmjs.com/package/socket-package)
