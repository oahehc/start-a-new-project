# How to start a new project

the steps to start a new project

---

1. [Generate template](https://github.com/oahehc/react-vue-comparison/blob/master/CLI.md)

```sh
npx create-next-app --example with-typescript [project-name]
cd [project-name]
npm run install
```

2. Create github repo

```sh
gh repo create [project-name]
git push --set-upstream origin main
```

3. Setup Vercel: https://vercel.com/new
   Configure github applications: https://github.com/settings/installations

4. Clear-up the project, remove un-use code

5. eslint and prettier

```sh
npx eslint --init
```

```js
// @.eslintrc.js
...
  rules: {
    'react/react-in-jsx-scope': false,
  },
...
```

```json
// @package.json
...
  "prettier": {
    "printWidth": 120,
    "singleQuote": true,
    "trailingComma": "es5",
    "arrowParens": "avoid"
  }
...
```

6. Add Tailwind: https://tailwindcss.com/docs/guides/nextjs

```sh
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
npx tailwindcss init -p
```

```js
// @tailwind.config.js
module.exports = {
  ...
  purge: ["./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}"],
  ...
};
```

```css
/* @./styles/globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```ts
// pages/_app.tsx
import { AppProps } from "next/app";
import "../styles/globals.css";

function MyApp({ Component, pageProps }: AppProps): JSX.Element {
  return <Component {...pageProps} />;
}

export default MyApp;
```

7. Add Google Analytics

   - create new property: https://analytics.google.com/
   - custom hook

   ```typescript
   import { useEffect } from "react";

   export function googleAnalytics(id: string): void {
     const isProd = process.env.NEXT_PUBLIC_VERCEL_ENV === "production";

     useEffect(() => {
       if (!isProd) return;
       function init() {
         if (window) {
           // @ts-ignore
           window.dataLayer = window.dataLayer || [];
           function gtag() {
             // @ts-ignore
             dataLayer.push(arguments);
           }
           // @ts-ignore
           gtag("js", new Date());
           // @ts-ignore
           gtag("config", id);
         }
       }

       const scriptTag = document.createElement("script");
       scriptTag.src = `https://www.googletagmanager.com/gtag/js?id=${id}`;
       scriptTag.onload = init;
       document.body.appendChild(scriptTag);
     }, []);
   }
   ```



## Optional

- Icons: https://github.com/tabler/tabler-icons
- UI components: https://headlessui.dev/

--

## TODO:
- google search console
- pre-commit hook: husky
- CICD:
  - GitHub action
  - Circle CI
- Jest
- semantic-release
- commitlint
- error tracking: sentry, logRocket, trackJS
- 
