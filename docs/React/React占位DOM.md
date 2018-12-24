## 一、React占位DOM

与 Vue 的 `<template></template>` 功能类似，是一种占位的节点，并不会真正的渲染。

React 中是 `Fragments`，使用方式如下：

### 1、第一种(建议这种清晰的方式)：

```js
<React.Fragment>
     <td>Hello</td>
     <td>World</td>
</React.Fragment>
```

### 2、第二种：

```js
<>
     <td>Hello</td>
     <td>World</td>
</>
```

## 二、参考&拓展
- [Fragments](https://react.docschina.org/docs/fragments.html)

