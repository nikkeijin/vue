# Must have node, npm, and npx to use Vue CLI.

To install Node with NPM via command line you must install Homebrew:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then you can install Node with NPM using the following command:
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
```

This will create a dist folder with your project inside of.
