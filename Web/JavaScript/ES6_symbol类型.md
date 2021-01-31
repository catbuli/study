# symbol类型

## 简介

ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

## 使用方式

```js
let testSy = Symbol("张三")

console.log(testSy) // Symbol(张三)
typeof(testSy) // return "symbol"  
```

简单来说就是生成一个唯一值。

```js
let testSy = Symbol("张三")
let testSy1 = Symbol("张三")

console.log(testSy === testSy1) // false

// Symbol的值，可以直接调用Symbol的description属性
console.log(testSy.description) // 张三
```

## 常用场景

### 1. 定义对象的唯一属性名。

```js
let name = Symbol("name")

// 写法1
let person = {}
person[name] = "张三"

// 写法2
let person = {
  [name]: "张三"
}

// 写法3
let person = {}
// 这种方法可以 通过person[name] 得到数据，但是如果不定义 enumerable: true 则无法直接获取name属性
Object.defineProperty(person, name, { value: '张三', enumerable: true })

// 三种方法都能的到一样的结果
console.log(person) // { [Symbol(name)]: '张三' }
```

> 这种方法定义的对象属性在读取的时候要注意
>
> 不要使用 `person.name` 来获取
>
> 要使用 `person[name] ` 来获取
>
> 因为点运算符后面总是字符串，所以不会读取 `name ` 作为标识名所指代的那个Symbol

### 2. 定义常量

```js
const COLOR = {
    BLUE: Symbol("blue"),
    YELLOW: Symbol("yellow"),
    RED: Symbol("red")
}

console.log(COLOR) // { BULE: Symbol(blue), YELLOW: Symbol(yellow), RED: Symbol(red) }
console.log(COLOR.BLUE) // Symbol(blue)
```

> 这种方式用来保证常量的值都是不相等的

```js
const COLOR = {
    BLUE: Symbol(),
    YELLOW: Symbol(),
    RED: Symbol()
}

function getColor(color) {
    switch (color) {
        case COLOR.BLUE:
            return COLOR.RED;
        case COLOR.YELLOW:
            return COLOR.BLUE;
        case COLOR.RED:
            return COLOR.YELLOW;
        default:
            throw new Error('Undefined color');
    }
}

console.log(getColor(COLOR.BLUE)) // Symbol()
```

> 上面的例子可以看到
>
> 其他任何值都不可能有相同的值了，因此可以保证上面的 `switch` 语句会按设计的方式工作。

## 总结

还有 Symbol.for()，Symbol.keyFor() 可以学习一下。

其实还有很多的奇奇怪怪的使用场景，不过我个人认为以上两种场景就足够日常开发使用了。

## 参考资料

[Symbol - ECMAScript 6入门](https://es6.ruanyifeng.com/?search=Symbol&x=0&y=0#docs/symbol)

