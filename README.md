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

## 提交规范约束

`pi husky lint-staged -D`
