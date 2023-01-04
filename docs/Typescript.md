# Typescript

## 找不到名称“__dirname”

``` bash
yarn add -D @types/node
 ```


## 找不到指定的模块XXX, 有时候`import XXX from '@/XXX/index'` 省略`index` 或者 `.ts` 后缀名时会报错

需要在`tsconfig.json` 中 配置`compilerOptions.paths` 例如 `"@/*": ["src/*"]`