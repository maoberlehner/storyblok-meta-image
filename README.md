# Storyblok Meta Image

Storyblok Meta Image is a Storyblok field-type plugin which provides an image field with meta data like width, height, alt and title texts and the images dominant color attached to it.

## How to use

Storyblok Meta Image is a custom field type plugin for the headless CMS Storyblok. In order to use it, you have to build and install it first.

### Deployment

You can start by cloning this repository and installing its dependencies.

```bash
git clone git@github.com:maoberlehner/storyblok-meta-image.git
cd storyblok-meta-image
npm install
```

Because Storyblok plugins share a global namespace, you have to choose a distinct name for your plugin first. Go to `src/Plugin.vue` and change the following line of code.

```diff
     initWith() {
       return {
         assets: [],
-        plugin: `meta-image`,
+        plugin: `YOUR-DISTINCT-NAME`,
       };
     },
```

Now you can run the build command and copy and paste the generated code into Storyblok when it's done.

```bash
npm run build
```

Next go to the [Plugins page](https://app.storyblok.com/#!/me/plugins) and click the `New` button in the top right.

It is important to choose the same name you specified in the `initWith()` method for your plugin to work.

Now you can copy the contents of `dist/export.js` into the plugin editor.

## Advanced features

This is an example value of a field using the Storyblok Cloudinary Assets plugin.

```json
{
  "alt": "Alt text",
  "dominant_color": "#355c7b",
  "height": 1600,
  "src": "//a.storyblok.com/f/52752/35e1e27517/foo.jpg",
  "title": "Title text",
  "width": 900,
}
```

## Build Setup

```bash
# Install dependencies.
npm install

# Serve with hot reload at localhost:8080.
npm run serve

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
