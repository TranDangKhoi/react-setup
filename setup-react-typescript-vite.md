# Cài đặt môi trường để code React + Javascript với Vite (v4.1.0 trở lên)

## 1. Môi trường hoàn hảo để code

1. Nodejs để run server react dưới local
2. Visual Studio Code để code
- Extensions mình khuyến khích nên cài:
  - Auto Rename Tag - Jun Han (Auto Rename Tag của VSCode mình thấy không ổn định bằng cái này, nên cài)
  - Babel Javascript - Michael McDermott
  - DotENV - mikestead (tùy sở thích)
  - ESLint - Microsoft
  - html to JSX - Riaz Laskar
  - JavaScript (ES6) code snippets - charalampos karypidis
  - Javascript Booster - Stephan Burguchev
  - Material Icon Theme - Philipp Kief
  - Multiple cursor case preserve - Cardinal90
  - npm Intellisense - Christian Kohler
  - Path Intellisense - Christian Kohler
  - Prettier - Prettier
  - Reactjs code snippets - charalampos karypidis
  - Tailwind CSS Intellisense - Tailwind Labs
  - Tailwind Docs
  
>Còn rất nhiều extensions rất tiện ích nữa nhưng như vậy là đủ rồi

3. Trình duyệt Chrome với extension là React Developer Tool và Redux Dev Tool extension
4. Git: Tạo repo trên github để quản lý source code

## 2. Cài đặt và cấu hình project (Tạo bằng Vite)

Bởi vì chúng ta đang sử dụng **Vite** 🐇⚡, chứ không phải **Create-React-App** 🐢👴, nên ta phải cài đặt và cấu hình ESLint bằng tay, dưới đây là danh sách các devDeps bạn cần phải cài đặt:

Dành cho những người dùng **npm**:

```bash
npm install eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-prettier prettier-plugin-tailwindcss eslint-plugin-react-hooks -D
```

Dành cho những người dùng **yarn**:

```bash
yarn add eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-prettier prettier-plugin-tailwindcss eslint-plugin-react-hooks -D
```

Dành cho những người dùng **pnpm**:

```bash
pnpm add eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-prettier prettier-plugin-tailwindcss eslint-plugin-react-hooks -D
```

### Cấu hình ESLint
Tạo một file `.eslintrc.cjs` trong root folder của project, và copy paste đoạn dưới vô như sau:

```cjs
// eslint-disable-next-line @typescript-eslint/no-var-requires
const path = require("path");

module.exports = {
  env: { browser: true, es2020: true, node: true },
  extends: [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react-hooks/recommended",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:jsx-a11y/recommended",
    "plugin:@typescript-eslint/recommended",
    "eslint-config-prettier",
    "prettier",
  ],
  parser: "@typescript-eslint/parser",
  parserOptions: { ecmaVersion: "latest", sourceType: "module" },
  plugins: ["react-refresh", "prettier"],
  settings: {
    react: {
      version: "detect",
    },
    "import/resolver": {
      node: {
        // Fix a path bug causing the root directory is not the current project - ESLint bug
        paths: [path.resolve(__dirname, "")],
        extensions: [".js", ".jsx", ".ts", ".tsx"],
      },
    },
  },
  rules: {
    "react-refresh/only-export-components": "warn",
    "prettier/prettier": [
      "warn",
      {
        arrowParens: "always",
        semi: true,
        trailingComma: "all",
        tabWidth: 2,
        endOfLine: "auto",
        useTabs: false,
        singleQuote: false,
        printWidth: 120,
        jsxSingleQuote: false,
        singleAttributePerLine: true,
      },
    ],
  },
};
```

Tạo một file `.eslintignore` nằm cùng cấp với file `.eslintrc.cjs` vừa tạo với nội dung như sau:

```json
node_modules/
dist/
```

Và tạo một file `.prettierrc` với nội dung như sau:

```json
{
  "arrowParens": "always",
  "semi": true,
  "trailingComma": "all",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": false,
  "printWidth": 120,
  "jsxSingleQuote": false,
  "singleAttributePerLine": true
}
```

Cuối cùng nhưng quan trọng khum kém 😉 đó là tạo `.prettierignore` với nội dung như sau:

```json
node_modules/
dist/
```

Thêm đoạn script mới sau vào trong package.json (Lưu ý là thêm vào bên dưới các đoạn script có sẵn):

```json
"scripts": {
    ...
    "lint": "eslint --ext ts,tsx src/", // thay thê script lint mặc định
    "lint:fix": "eslint --fix --ext ts,tsx src/",
    "prettier": "prettier --check \"src/**/(*.tsx|*.ts|*.css|*.scss)\"",
    "prettier:fix": "prettier --write \"src/**/(*.tsx|*.ts|*.css|*.scss)\""
},
```

### Cấu hình .editorconfig

Tạo thêm một file cùng cấp với các file trên và đặt tên là `.editorconfig` có nội dung như sau:

```json
[*]
indent_size = 2
indent_style = space
```

### Cấu hình Typescript

Trong file `tsconfig.json`, cấu hình đoạn code như sau (lưu ý, hãy update TS lên bản mới nhất):

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": "."
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

### Cấu hình vite config

Trong file `vite.config`, thêm đoạn code sau:

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    // Các bạn có thể sửa theo ý mình
    port: 3000,
  },
  css: {
    // Thêm cái này vô để debug css dễ hơn
    devSourcemap: true,
  },
  resolve: {
    alias: {
      src: path.resolve(__dirname, "./src"),
    },
  },
});
```

