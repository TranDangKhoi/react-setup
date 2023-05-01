# Cài đặt môi trường code React + Javascript với CRA

## 1. Môi trường hoàn hảo để code

1. Nodejs để run server react dưới local
2. Visual Studio Code để code
- Extension mình khuyến khích nên cài:
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

## 2. Sử dụng prettier và Eslint trong React.js (Tạo bằng Create React App)

### 2.1. Setting prettier on User

- Editor: Default Formatter => Chọn Prettier
- Editor: Format On Save => true
- Files: Eol => auto

Nếu như các bạn muốn setting mỗi workspace hiện tại thôi (nghĩa là cái folder hiện tại) thì các bạn setting bên workspace

### 2.2. Tạo file `.editorconfig` để chia sẻ một số setting giữa các editor với nhau

Một số người khi code họ không sử dụng VSCode giống như mình, họ có thể dùng Visual Studio, IntelliJ, Vim, ... rất nhiều các editor khác nữa đều có các setting editor khác nhau và không thống nhất. Vậy nên ta cần thêm `.editorconfig` để config lại và cụ thể ở dưới mình đang config việc canh lề cách ra bên trái một khoảng

```bash
[*]
indent_style = space
indent_size = 2
```

### 2.3. Tạo file `.prettierrc` để chia sẻ setting prettier giữa các editor

Lí do tạo file này cũng tương tự như ở trên

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

Bên trên là setting mình sử dụng và cảm thấy thích hợp và dễ nhìn nhất, các bạn có thể chỉnh sửa lại tùy theo team thống nhất

### 2.4. Cài các devDependencies hỗ trợ prettier và eslint trên terminal

Ở trên thì chúng ta mới chỉ setting prettier cho editor (tức là UI), bây giờ là cho terminal. Editor thì có thể mỗi máy sẽ kiểm tra khác nhau nhưng trên terminal thì không, setting trên terminal sẽ giúp code thống nhất.

```bash
npm i prettier eslint-plugin-prettier eslint-config-prettier -D
```

Trên là những plugin cần thiết để setting Pretter và Eslint cho CRA. Các bạn nếu dùng yarn thì chạy `yarn add` nhé.

*Update*: Bonus thêm nếu bạn đang sử dụng tailwind thì nên cài thêm `prettier-plugin-tailwindcss`, vì nó sẽ giúp sort class theo thứ tự chuẩn nhất để code các bạn không gặp lỗi override (một lỗi cực kì nghiêm trọng mà sẽ khiến bạn phải mệt mỏi khi debug - According to [Theo](https://youtu.be/QBajvZaWLXs?t=260))

### 2.5. Tạo file `.eslintrc` để setting eslint

```json
{
  "extends": ["react-app", "prettier"],
  "plugins": ["react", "prettier"],
  "rules": {
    "prettier/prettier": [
      "warn",
      {
        "arrowParens": "always",
        "semi": false,
        "trailingComma": "all",
        "tabWidth": 2,
        "endOfLine": "auto",
        "useTabs": false,
        "singleQuote": true,
        "printWidth": 120,
        "jsxSingleQuote": true
      }
    ]
  }
}
```

### 2.6. Thêm scripts vào package.json

```json
{
  "lint": "eslint --ext js,jsx,ts,tsx src/",
  "lint:fix": "eslint --fix --ext js,jsx,ts,tsx src/",
  "prettier": "prettier --check \"src/**/(*.jsx|*.js|*.tsx|*ts|*.css|*.scss)\"",
  "prettier:fix": "prettier --write \"src/**/(*.jsx|*.js|*.tsx|*ts|*.css|*.scss)\""
}
```

Lúc này bạn chỉ cần chạy

- `npm run lint`: Kiểm tra lỗi eslint
- `npm run lint:fix`: Fix lỗi liên quan eslint (đôi lúc có những lỗi bạn phải tự fix bằng tay)
- `npm run prettier`: Kiểm tra lỗi prettier format
- `npm run prettier:fix`: Tự fix lỗi prettier format

### 2.7. Thêm file `.prettierrignore` và `.eslintignore` để ignore những file bạn không muốn prettier và eslint format

Cú pháp viết trong những file này tương tự như trong file `.gitignore`

## 3. CICD và deploy với Vercel

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
