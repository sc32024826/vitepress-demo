# javascript

## 可选链 `?.`

## 空值合并运算符 `??`

```javascript
let b;
let a = 0;
let c = { name:'XXX' }

b = a ?? c;
```

上面的例子,当a除了undefined、null之外的任何值,b都会等于a,否则就等于c.

## 空值赋值运算符 `??=`

```javascript
let b = '你好';
let a = 0
let c = null;
let d = ’123‘
b ??= a;  // b = “你好”
c ??= d  // c = '123'
```

当??=左侧的值为null、undefined的时候,才会将右侧变量的值赋值给左侧变量.其他所有值都不会进行赋值.

## TypeScript的语法，叫非空断言操作符: `!.`

和`?.`相反，这个符号表示对象后面的属性一定不是null或undefined

## jsconfig.json 配置说明

```json
"compilerOptions": {
  "incremental": true, // TS编译器在第一次编译之后会生成一个存储编译信息的文件，第二次编译会在第一次的基础上进行增量编译，可以提高编译的速度
  "tsBuildInfoFile": "./buildFile", // 增量编译文件的存储位置
  "diagnostics": true, // 打印诊断信息 
  "target": "ES5", // 目标语言的版本
  "module": "CommonJS", // 生成代码的模板标准
  "outFile": "./app.js", // 将多个相互依赖的文件生成一个文件，可以用在AMD模块中，即开启时应设置"module": "AMD",
  "lib": ["DOM", "ES2015", "ScriptHost", "ES2019.Array"], // TS需要引用的库，即声明文件，es5 默认引用dom、es5、scripthost,如需要使用es的高级版本特性，通常都需要配置，如es8的数组新特性需要引入"ES2019.Array",
  "allowJS": true, // 允许编译器编译JS，JSX文件
  "checkJs": true, // 允许在JS文件中报错，通常与allowJS一起使用
  "outDir": "./dist", // 指定输出目录
  "rootDir": "./", // 指定输出文件目录(用于输出)，用于控制输出目录结构
  "declaration": true, // 生成声明文件，开启后会自动生成声明文件
  "declarationDir": "./file", // 指定生成声明文件存放目录
  "emitDeclarationOnly": true, // 只生成声明文件，而不会生成js文件
  "sourceMap": true, // 生成目标文件的sourceMap文件
  "inlineSourceMap": true, // 生成目标文件的inline SourceMap，inline SourceMap会包含在生成的js文件中
  "declarationMap": true, // 为声明文件生成sourceMap
  "typeRoots": [], // 声明文件目录，默认时node_modules/@types
  "types": [], // 加载的声明文件包
  "removeComments":true, // 删除注释 
  "noEmit": true, // 不输出文件,即编译后不会生成任何js文件
  "noEmitOnError": true, // 发送错误时不输出任何文件
  "noEmitHelpers": true, // 不生成helper函数，减小体积，需要额外安装，常配合importHelpers一起使用
  "importHelpers": true, // 通过tslib引入helper函数，文件必须是模块
  "downlevelIteration": true, // 降级遍历器实现，如果目标源是es3/5，那么遍历器会有降级的实现
  "strict": true, // 开启所有严格的类型检查
  "alwaysStrict": true, // 在代码中注入'use strict'
  "noImplicitAny": true, // 不允许隐式的any类型
  "strictNullChecks": true, // 不允许把null、undefined赋值给其他类型的变量
  "strictFunctionTypes": true, // 不允许函数参数双向协变
  "strictPropertyInitialization": true, // 类的实例属性必须初始化
  "strictBindCallApply": true, // 严格的bind/call/apply检查
  "noImplicitThis": true, // 不允许this有隐式的any类型
  "noUnusedLocals": true, // 检查只声明、未使用的局部变量(只提示不报错)
  "noUnusedParameters": true, // 检查未使用的函数参数(只提示不报错)
  "noFallthroughCasesInSwitch": true, // 防止switch语句贯穿(即如果没有break语句后面不会执行)
  "noImplicitReturns": true, //每个分支都会有返回值
  "esModuleInterop": true, // 允许export=导出，由import from 导入
  "allowUmdGlobalAccess": true, // 允许在模块中全局变量的方式访问umd模块
  "moduleResolution": "node", // 模块解析策略，ts默认用node的解析策略，即相对的方式导入
  "baseUrl": "./", // 解析非相对模块的基地址，默认是当前目录
  "paths": { // 路径映射，相对于baseUrl
    // 如使用jq时不想使用默认版本，而需要手动指定版本，可进行如下配置
    "jquery": ["node_modules/jquery/dist/jquery.min.js"]
  },
  "rootDirs": ["src","out"], // 将多个目录放在一个虚拟目录下，用于运行时，即编译后引入文件的位置可能发生变化，这也设置可以虚拟src和out在同一个目录下，不用再去改变路径也不会报错
  "listEmittedFiles": true, // 打印输出文件
  "listFiles": true// 打印编译的文件(包括引用的声明文件)
}
```


## `typeof` 和 `instanceof`的区别
||typeof|instanceof|
|---|---|---|
|1|'number'| 不能判断基本类型数据|
|'1'| 'string'|不能判断基本类型数据|
|true|'boolean'|不能判断基本类型数据|
|undefined| 'undefined'|不能判断基本类型数据|
|null|'object'|不能判断基本类型数据|
|[1,2,3]|'object'|[1,2,3] instanceof Array -> true|
| const a = function(){}| 'function'| a instanceof Function -> true|
| const b = {a:1}|'object'|b instanceof Object -> true|
| const c = Symbol()| 'symbol'| 不能判断基本类型数据|


## 深拷贝

- ...展开运算符

```javascript
let a = {
    name: 'sdfsd',
    age: 4
}

const b = {...a}

b.age = 5

console.log(a) // {name: 'sdfsd',age: 4}
console.log(b) // {name: 'sdfsd',age: 5}

const c = {a, b:'asda'}
const d = {...c}
d.a.age = 6

console.log(c) // {a:{name: 'sdfsd',age: 6}, b: 'asda'}
console.log(d) // {a:{name: 'sdfsd',age: 6}, b: 'asda'}

```

缺点: 只能展开第一层 多层时 仍为浅拷贝

- JSON.parse() & JSON.stringify()

```javascript
let a = {name:'张三', age: 1}
const b = JSON.parse(JSON.stringify(a))

b.age = 2

console.log(a) // {name: '张三',age: 1}
console.log(b) // {name: '张三',age: 2}
```

缺点: 当对象中包含Function时 会被忽略

- 递归函数
```javascript
let a = {
    name:'张三',
    age: 1,
    action(){
        console.log('555')
    }
}
// 通用做法
function deepClone(value){
    if (typeof value !== 'object' || value === null) return value
    const result = Array.isArray(value) ? [] : {}
    for(let key in value){
        if(value.hasOwnProperty(key)){
            result[key] = deepClone(value[key])
        }
    }
    return result
}
```
