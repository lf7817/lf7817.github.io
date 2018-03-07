---
title: 在create-react-app中启用修饰器
date: 2018-01-22 10:22:32
tags: [mobx, create-react-app]
---
最近在学习mobx，文档提倡使用修饰器的写法，但create-react-app默认是不支持修饰器的写法，这里记录下过程

### 弹出配置文件
```bash
yarn eject
```
<!--more-->
### 安装插件
```bash
yarn add babel-plugin-transform-decorators-legacy
```

### 配置<code>package.json</code>
```json
"babel": {
  "presets": [
    "react-app"
  ],
+ "plugins": ["transform-decorators-legacy"]
}
```
### 配置<code>vscode</code>
如果你用vscode，编辑器会报<code>experimentalDecorators</code>警告，看着烦，这是因为修饰器是实验性的写法。

如果你使用的typescript就在tsconfig.json里加一个配置项。
如果你使用的是js或者jsx就在当前目录新建一个jsconfig.json，同样加入以下配置即可。
```json
{
    "compilerOptions": {
        "experimentalDecorators": true
    }
}
```