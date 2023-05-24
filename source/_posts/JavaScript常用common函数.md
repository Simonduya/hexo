---
title: JavaScript常用common函数
tags: JavaScript
categories: JavaScript
abbrlink: e28e5a40
date: 2023-05-24 22:17:28
---

## 数组转对象

```typescript
export const arrToObj = (arr: []) => {
  return (arr || []).reduce((prev, last) => {
    (prev as { [k: string]: string })[last] = "";
    return prev;
  }, {});
};
```

```javascript
export const arrToObj = (arr = []) => {
  return arr.reduce((pre, cur) => {
    pre[cur] = "";
    return pre;
  }, {});
};
```

这段代码导出了一个名称为 `arrToObj` 的函数，该函数接收一个数组作为参数，并将数组转换为一个空对象。以下是一些示例代码，展示如何使用这个函数：

```js
import { arrToObj } from "./path/to/module.js";

// 示例 1：使用空数组作为参数
const emptyArr = [];
const emptyObj = arrToObj(emptyArr);
console.log(emptyObj); // {}

// 示例 2：使用非空数组作为参数
const fruits = ["apple", "banana", "orange"];
const fruitObj = arrToObj(fruits);
console.log(fruitObj); // { apple: "", banana: "", orange: "" }

// 示例 3：使用含有重复元素的数组作为参数
const colors = ["red", "green", "blue", "red"];
const colorObj = arrToObj(colors);
console.log(colorObj); // { red: "", green: "", blue: "" }
```

在示例中，第一行导入了定义在模块文件中的 `arrToObj` 函数。示例 1 中，使用一个空数组作为参数调用该函数，返回一个空对象 `{}`。示例 2 中，使用一个包含三个元素的数组作为参数调用该函数，返回一个包含三个键值对的对象。示例 3 中，使用一个包含四个元素、其中含有两个相同元素的数组作为参数调用该函数，返回一个包含三个键值对的对象，其中具有相同键的元素仅被包含一次。

需要注意的是，在使用 `reduce()` 方法时，初始累加器的值应该设为一个空对象 `{}`，而不是空数组 `[]`。因为每次迭代时，都需要将一个字符串作为对象的键，因此初始值必须是一个对象类型。在函数体中，使用了 TypeScript 的类型断言语法，将累加器 `prev` 显式地指定为一个具有字符串键和字符串值的对象类型 `{ [k: string]: string }`。

## url 的 query 参数转对象

```js
// let str = 'https://example.com/?name=John&age=30'
const parseUrl = () => {
  // 序列化URL
  // const q: { [key: string]: string } = {};
  const q = {};
  location.search.replace(/([^?&=]+)=([^&]+)/g, (_, k, v) => (q[k] = v));
  // str.replace(/([^?&=]+)=([^&]+)/g, (_, k, v) => (q[k] = v));
  return q;
};
// 当前页面 URL 为 https://example.com/?name=John&age=30

const query = parseUrl();
console.log(query); // { name: "John", age: "30" }

const name = query.name; // "John"
const age = parseInt(query.age); // 30
```

这段代码导出了一个名为 `parseUrl` 的函数，它的作用是将当前页面的 URL 查询参数解析为一个对象。以下是一个示例代码：

在这个示例中，首先从导入模块中获取了 `parseUrl` 函数。然后调用该函数，将返回值保存在变量 `query` 中。由于当前页面的 URL 查询参数为 `?name=John&age=30`，因此 `query` 对象将包含两个属性：`name` 和 `age`，对应的值分别为 `"John"` 和 `"30"`。

接下来，示例中演示了如何使用这些查询参数。通过访问 `query` 对象的属性，可以轻松地获取到相应的值。需要注意的是，在示例中获取 `age` 值时，使用了 JavaScript 内置的 `parseInt()` 函数来将字符串转换为整数。

需要注意的是，这个函数只能解析 URL 查询参数，并不能解析其他部分的 URL，例如协议、主机、路径等。如果需要解析完整的 URL，请参考相关库或使用 JavaScript 内置的 `URL` 对象。
