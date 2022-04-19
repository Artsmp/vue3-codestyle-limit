## eslint 和 prettier 项目规范配置

1. `npm install --save-dev --save-exact prettier`
2. `echo {}> .prettierrc.json`
3. `npm install --save-dev eslint eslint-plugin-vue eslint-config-prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin`

在 package.json 文件中添加：

```json
{
  "scripts": {
    "lint": "eslint --ext .js,.ts,.vue,.tsx,.jsx --ignore-path .gitignore --fix src",
    "format": "prettier .  --write"
  }
}
```

添加 eslintrc.js 文件：

```js
module.exports = {
  env: {
    node: true,
    browser: true,
    es2021: true,
    // 开启setup语法糖环境
    'vue/setup-compiler-macros': true,
  },
  extends: [
    'eslint:recommended',
    'plugin:vue/vue3-recommended',
    'plugin:@typescript-eslint/recommended',
    'prettier',
  ],
  // 新增，解析vue文件
  parser: 'vue-eslint-parser',
  // 支持ts的最新语法
  parserOptions: {
    ecmaVersion: 'latest',
    parser: '@typescript-eslint/parser',
    sourceType: 'module',
  },
  // 添加vue和@typescript-eslint插件，增强eslint的能力
  plugins: ['vue', '@typescript-eslint'],
  rules: {
    // override/add rules settings here, such as:
    // 'vue/no-unused-vars': 'error'
    'vue/require-default-prop': 'off',
  },
};
```

在 .prettierrc.json 文件中添加：

```json
{
  "singleQuote": true,
  "semi": true,
  "printWidth": 80
}
```

## 提交时代码自动格式化校验规范约束

1. `pi husky lint-staged -D`

2. 在 package.json 中添加内容：

```json
  "scripts": {
    "prepare": "husky install"
  },
  "lint-staged": {
    "*.{js,vue,ts,jsx,tsx}": [
      "prettier --write",
      "eslint --fix"
    ],
    "*.{html,css,less,scss,md}": [
      "prettier --write"
    ]
  }
```

3. `pnpm prepare`
4. `pnpx husky add .husky/pre-commit "npx --no-install lint-staged"`

## 提交消息规范

按文档进行操作即可：https://github.com/conventional-changelog/commitlint
