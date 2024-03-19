# Getting Started with Create React App

## Creating a new React Project

You can create a new React project with the following command.
In the case, the project-name should be lower-case.

`npx create-react-app [project-name]`

## Using Vite

Webpack is a matured bundle, but it's kind of slow compared to Vite.
So we will be using Vite, which is fast and easy tool.

### Step1: Remove reacts-scripts
`npm uninstall react-scripts`

### Step2: Install Vite and its dependencies
vite-tsconfig-paths package is just for Typescript based project.

`npm install --save-dev vite @vitejs/plugin-react vite-plugin-svgr [vite-tsconfig-paths]`

### Step3: In package.json, replace scripts with the following.
```
"scripts": {
    "start": "vite",
    "build": "tsc && vite build",
    "serve": "vite preview"
}
```

### Step4: Create a new file called vite.config.js in the root folder (A parent folder of `src`)
```
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
    plugins: [react()],
    esbuild: {
        jsxFactory: 'h',
        jsxFragment: 'Fragment'
    },
    server: {
        host: '0.0.0.0',
        port: 3000,
    },
    preview: {
        host: '0.0.0.0',
        port: 3000,
    },
    resolve: {
        alias: {
            "@": "/src/",
            "@assets": "/src/assets",
            "@components": "/src/components",
        }
    }
})
```

### Step5: Create a file called jsconfig.json in the root folder
```
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
        "@/*": ["src/*"],
        "@assets/*": ["/src/assets/*"],
        "@components/*": ["/src/components/*"]
    }
  }
}
```
### Step6: Move public/index.html into root folder.
And move favicon.ico located in `public` folder into root folder.

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <link rel="icon" type="image/svg+xml" href="/favicon.ico" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Vaultik Brands Dashboard</title>
  <script>
    var global = global || window;
  </script>
</head>

<body>
  <div id="root"></div>
  <script type="module" src="/src/index.jsx"></script>

</body>

</html>
```

## Project Structure
```
- /src
  - /assets
  - /components
  - /pages
  - /services
  - /utils
  - /store
  - /styles
  - /test
  - App.jsx
  - index.jsx
```
`/src:` This is the root directory for your application's source code.

`/assets:` Place static assets like images, fonts, or other media files.

`/components:` Place reusable components that are used across multiple pages or features of your application.

`/pages:` Create individual directories for each page or route of your application. Each directory should contain the components and logic specific to that page.

`/services:` Handle any external services or APIs your application interacts with, such as HTTP requests or WebSocket connections.

`/utils:` Store utility functions or helper modules that can be used throughout your application.

`/store:` This folder is used for managing Redux/Recoil-related files.

`/styles:` Store global styles, CSS modules, or theme-related files.

`/test:` In this folder, you can place test functions for unit tests and integration tests.

`App.jsx:` The entry point component of your application that handles the overall structure and routing.

`index.jsx:` The file responsible for rendering your application and mounting it into the DOM.
