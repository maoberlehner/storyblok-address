# Storyblok Address

> A Storyblok field-type plugin which makes it possible to enter addresses.

## How to use

Storyblok Address is a custom field type plugin for the headless CMS Storyblok. In order to use it, you have to build and install it first.

### Deployment

You can start by cloning this repository and then run the build command and copy and paste the generated code into Storyblok when it's done.

```bash
git clone git@github.com:maoberlehner/storyblok-address.git
cd storyblok-address
npm install
npm run build
```

Next go to the [Plugins page](https://app.storyblok.com/#!/me/plugins) and click the `New` button in the top right. It is important to name your new custom field type plugin `address` for it to work. After creating a new plugin you can copy the contents of `dist/export.js` into the plugin editor.

## Build Setup

```bash
# Install dependencies.
npm install

# Serve with hot reload at localhost:8080.
npm run dev

# Build for production.
npm run build
```

## About

### Author

Markus Oberlehner  
Website: https://markus.oberlehner.net  
Twitter: https://twitter.com/MaOberlehner  
PayPal.me: https://paypal.me/maoberlehner  
Patreon: https://www.patreon.com/maoberlehner

### License

MIT