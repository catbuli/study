# CommonJs 和 ES6 module 的区别

## CommonJs 规范

### 概述

**CommonJS**是一个项目，其目标是为[JavaScript](https://zh.wikipedia.org/wiki/JavaScript)在[网页浏览器](https://zh.wikipedia.org/wiki/网页浏览器)之外创建[模块](https://zh.wikipedia.org/wiki/子程序)约定。创建这个项目的主要原因是当时缺乏普遍可接受形式的JavaScript脚本模块单元，模块在与运行JavaScript脚本的常规网页浏览器所提供的不同的环境下可以重复使用。

Node 应用由模块组成，采用 CommonJS 模块规范。

每个文件就是一个模块，有自己的作用域。在一个文件里面定义的变量、函数、类，都是私有的，对其他文件不可见。

CommonJS规范规定，每个模块内部，`module`变量代表当前模块。这个变量是一个对象，它的`exports`属性（即`module.exports`）是对外的接口。加载某个模块，其实是加载该模块的`module.exports`属性。

```js
var x = 5;
var addX = function (value) {
  return value + x;
};
module.exports.x = x;
module.exports.addX = addX;
```

上面代码通过`module.exports`输出变量`x`和函数`addX`。

`require`方法用于加载模块。

```js
var example = require('./example.js');

console.log(example.x); // 5
console.log(example.addX(1)); // 6
```

> - 所有代码都运行在模块作用域，不会污染全局作用域。
> - 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。
> - 模块加载的顺序，按照其在代码中出现的顺序。

### 模块的导出

```js
module.exports = {
    flag: "flag",
    add: function (a, b) {
        return a + b;
    }
}
```

另一种导出方法。

```js
exports.flag = "flag";
exports.add = (a, b) => {
    return a + b;
}
```

两种方法效果是一样的。

有两点需要注意

1. **不要把module.exports与exports混用**

   > ```js
   > exports.add = (a, b) => {
   >     return a + b;
   > };
   > module.exports = {
   >     flag: 'flag'
   > };
   > ```
   >
   > 这么写相当于对于用一个新的对象覆盖了 `module.exports` 将会导致 `add` 丢失，无法导出。

2. **导出语句尽量放在文件的末尾**

   > ```js
   > module.exports = {
   >     flag: 'flag'
   > };
   > console.log("test")
   > ```
   >
   > 导出语句后面的console依然会被执行，从可读性角度讲。
   >
   > 建议将导出语句放入文件结尾。

### 模块的导入

```js
const commonJs = require('./add.js')

console.log(commonJs.flag, '')          //flag
console.log(commonJs.add(1, 2), '')     //3
```

## ES6 module 规范

### 概述

历史上，JavaScript 一直没有模块（module）体系，无法将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。其他语言都有这项功能，比如 Ruby 的`require`、Python 的`import`，甚至就连 CSS 都有`@import`，但是 JavaScript 任何这方面的支持都没有，这对开发大型的、复杂的项目形成了巨大障碍。

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

这边建议直接[Module 的语法 - ECMAScript 6入门](https://es6.ruanyifeng.com/#docs/module) 阮大佬写的非常通俗易懂了。

# 参考资料

[CommonJS - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/CommonJS)

[CommonJS规范 -- JavaScript 标准参考教程（alpha）](https://javascript.ruanyifeng.com/nodejs/module.html)

[CommonJS 和 ES Module的导入导出](https://zhuanlan.zhihu.com/p/301326042)

[JavaScript modules 模块 - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Modules)

[Module 的语法 - ECMAScript 6入门](https://es6.ruanyifeng.com/#docs/module)