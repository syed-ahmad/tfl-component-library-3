# tfl-component-library-3

```
cd Documents/code
mkdir tfl-component-library-3
cd tfl-component-library-3
code . -r
```

take all defaults for now

```
yarn init
```

 add preceding instructions

```
touch README.md
```

```
git init
touch .gitignore
```

in .gitignore

```
node_modules/
build/ 
```

in source control, create new empty repo

```
git remote add origin https://github.com/pgmoir/tfl-component-library-3.git
git add .
git commit -m 'Initial baseline'
git push -u origin master
```

```
yarn add react react-dom
yarn add -D typescript @types/react rollup rollup-plugin-commonjs rollup-plugin-node-resolve rollup-plugin-peer-deps-external rollup-plugin-sass rollup-plugin-typescript2
```

```
touch rollup.config.js
```

```
import typescript from "rollup-plugin-typescript2";
import sass from "rollup-plugin-sass";
import commonjs from "rollup-plugin-commonjs";
import external from "rollup-plugin-peer-deps-external";
import resolve from "rollup-plugin-node-resolve";

import pkg from "./package.json";

export default {
  input: "src/index.tsx",
  output: [
    {
      file: pkg.main,
      format: "cjs",
      exports: "named",
      sourcemap: true
    },
    {
      file: pkg.module,
      format: "es",
      exports: "named",
      sourcemap: true
    }
  ],
  plugins: [
    external(),
    resolve({
      browser: true
    }),
    typescript({
      rollupCommonJSResolveHack: true,
      exclude: "**/__tests__/**",
      clean: true
    }),
    commonjs({
      include: ["node_modules/**"],
      exclude: ["**/*.stories.js"],
      namedExports: {
        "node_modules/react/react.js": [
          "Children",
          "Component",
          "PropTypes",
          "createElement"
        ],
        "node_modules/react-dom/index.js": ["render"]
      }
    }),
    sass({
      insert: true
    })
  ]
};
```

```
mkdir src
touch src/index.tsx
```

```
import TestComponent from "./test-component/TestComponent";

export { TestComponent };
```

```
mkdir src/test-component
touch src/test-component/test-component.scss
```

```
.test-component {
    color: orange;

    .heading {
        font-size: 64px;
    }
} 
```

```
touch src/test-component/test-component.stories.js
```

```
touch src/test-component/TestComponent.tsx
```

```
import React from "react";

import './test-component.scss';

const TestComponent = () => (
  <div className="test-component">
    <h1 className="heading">I'm the test component</h1>
    <h2>Made with love by Harvey</h2>
  </div>
);

export default TestComponent;
```

```
touch tsconfig.json
```

```
{
  "compilerOptions": {
    "outDir": "build",
    "module": "esnext",
    "target": "es5",
    "lib": ["es6", "dom", "es2016", "es2017"],
    "sourceMap": true,
    "allowJs": false,
    "jsx": "react",
    "declaration": true,
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true
  },
  "include": ["src", "images.d.ts"],
  "exclude": ["node_modules", "build"]
}
```

alter package.json

```
{
  "name": "tfl-component-library-3",
  "version": "1.0.0",
  "main": "build/index.js",
  "module": "build/index.es.js",
  "jsnext:main": "build/index.es.js",
  "files": [
    "build"
  ],
  "description": "A TFL skeleton for React Component library using Rollup, TypeScript, Sass and Storybook",
  "scripts": {
    "build": "rollup -c",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/pgmoir/tfl-component-library-3.git"
  },
  "keywords": [
    "React",
    "Component",
    "Library",
    "Rollup",
    "Typescript",
    "Sass",
    "Storybook"
  ],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/pgmoir/tfl-component-library-3/issues"
  },
  "homepage": "https://github.com/pgmoir/tfl-component-library-3#readme",
  "dependencies": {
    "react": "^16.13.1",
    "react-dom": "^16.13.1"
  },
  "devDependencies": {
    "@types/react": "^16.9.35",
    "rollup": "^2.11.2",
    "rollup-plugin-commonjs": "^10.1.0",
    "rollup-plugin-node-resolve": "^5.2.0",
    "rollup-plugin-peer-deps-external": "^2.2.2",
    "rollup-plugin-sass": "^1.2.2",
    "rollup-plugin-typescript2": "^0.27.1",
    "typescript": "^3.9.3"
  }
}
```

```
yarn build
```

Builds ok

Commit




