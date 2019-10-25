# umi-plugin-mobx2

umi@2 的 mobx 插件。

本插件魔改自 `umi-plugin-mobx-state-tree`, 只为 mobx 做适配，如需 mst 请选择其它

约定加载 src/stores 下的所有文件(可通过设置 exclude 排除某些文件)

默认开启按需加载，build 之后根据路由添加 pages 下的 stores 文件(可通过设置 [dynamicImport](https://umijs.org/zh/plugin/umi-plugin-react.html#dynamicimport) 关闭)

所有store全部加载到顶级对象上，默认取文件名作为inject查找的对象名。
```
inject(stores => ({
    list: stores.list
}))(observer(App));
```

由于umi默认加载pages下面的文件生成路由，所以要通过设置[routes/exclude](https://umijs.org/zh/plugin/umi-plugin-react.html#routes)来把stores排除
```js
routes: {
  exclude: [/stores\//],
},
```
## 快速使用
安装
```
$ npm i umi-plugin-mobx2
```
.umirc.js

```js
export default {
  plugins: ["umi-plugin-mobx2"]
};
```

## 支持配置

```js
export default {
  plugins: [
    [
      "umi-plugin-mobx2",
      {
        exclude: [/^\$/] //这里是以$开头的stores不会被引用
      }
    ]
  ]
};
```

exclude:提供 src/stores 下的文件不被注册的功能，比如加上$前缀就不会被注册了,值为正则表达式


## /src/mobx.js
可以通过src/mobx.js配置初始值和开启mobx-react-devtools调试工具
```
export function config() {
  return {
    devTools: true,
    initStores: {
      title: 'My APP'
    }
  };
}
```
可以通过设置``devTools: true``开启mobx-devtools，这个功能需要依赖[mobx浏览器调试工具](https://github.com/mobxjs/mobx-devtools/blob/master/README.md#features)使用。

这个配置可以通过runtime修改。
