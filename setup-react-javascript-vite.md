# Cài đặt môi trường để code React + Javascript với Vite (v4.1.0 trở xuống)

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
/* eslint-disable @typescript-eslint/no-var-requires */
const path = require("path");

module.exports = {
  extends: [
    // Thêm tất cả các rules mình vừa cài đặt 
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:react-hooks/recommended",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:jsx-a11y/recommended",
    "plugin:@typescript-eslint/recommended",
    // Một vài plugins bên trên sẽ gây ra conflicts nếu không đặt đúng thứ tự
    // Thế nên ta sẽ đặt 2 plugins này bên dưới để giải quyết đống conflicts
    "eslint-config-prettier",
    "prettier",
  ],
  plugins: ["prettier"],
  settings: {
    react: {
      // Tự detect version của React đang dùng
      version: "detect",
    },
    "import/resolver": {
      node: {
        paths: [path.resolve(__dirname, "")],
        extensions: [".js", ".jsx", ".ts", ".tsx"],
      },
    },
  },
  env: {
    node: true,
    // Khi code với JSX thì phải thêm đoạn này vô
    browser: true,
  },
  rules: {
    "react/react-in-jsx-scope": "off",
    "react/jsx-no-target-blank": "warn",
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
    "lint": "eslint --ext js,jsx src/",
    "lint:fix": "eslint --fix --ext js,jsx src/",
    "prettier": "prettier --check \"src/**/(*.jsx|*.js|*.css|*.scss)\"",
    "prettier:fix": "prettier --write \"src/**/(*.jsx|*.js|*.css|*.scss)\""
},
```

### Cấu hình .editorconfig

Tạo thêm một file cùng cấp với các file trên và đặt tên là `.editorconfig` có nội dung như sau:

```json
[*]
indent_size = 2
indent_style = space
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
