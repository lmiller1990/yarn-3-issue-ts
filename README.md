I recreated it. It is a different issue that manifests the same error.

I did something like:

```sh
yarn create vite --template vue-ts my-yarn-vue-app
cd my-yarn-vue-app
yarn set version berry
yarn init                                                         
yarn
yarn add vite vue typescript @vitejs/plugin-vue --dev
```

It did not detect I was using TypeScript. Seems like a bug, I guess we are not considering where yarn 3 saves `node_modules`. It generated a `cypress.config.js` with CJS.

I changed `cypress.config.js` to `cypress.config.ts` and added:

```ts
mport { defineConfig } from "cypress"

export default defineConfig({
  component: {
    devServer: {
      framework: "vue",
      bundler: "vite",
    },
  },
});
```

Now I can reproduce the error.



