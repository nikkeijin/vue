# Must have Node to use Vue CLI.

To install Node via command line on MAC you must install Homebrew:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then you can install Node using the following command:
```bash
brew install node
```

# Vue CLI

To install Vue CLI globally you can use the following command:
```bash
npm install -g @vue/cli
```
OR
```bash
yarn global add @vue/cli
```

Create a project:
```bash
vue create my-project
```

# Pre-Processors

SASS
```bash
npm install -D sass-loader sass
```

Less
```bash
npm install -D less-loader less
```

Stylus
```bash
npm install -D stylus-loader stylus
```


# Tailwind

```bash
vue add tailwind
```
    
# Router

To switch the mode of router modify your router initialization in router/main.ts as follows:
    
```JavaScript
/*

################################################## 

History Mode

By default, Vue Router uses history mode, which requires server configuration to handle client-side routing correctly.

*/

import { createRouter, createWebHistory, RouteRecordRaw } from "vue-router";

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes,
});

export default router;

/*

##################################################

Hash Mode

When you switch to hash mode, Vue Router uses the hash portion of the URL (example.com/#/about) to handle routing.
This mode does not require any server configuration changes and works out of the box on most shared hosting servers.

*/

import { createRouter, createWebHashHistory, RouteRecordRaw } from "vue-router";

const router = createRouter({
  history: createWebHashHistory(),
  routes,
});

export default router;

```
    
# Build

Open vue.config.js and add the following code:
```bash
module.exports = {
  publicPath: './'
}
```

Then:
```bash
npm run build
OR
yarn run build
```

This will create a dist folder with your project inside of.
