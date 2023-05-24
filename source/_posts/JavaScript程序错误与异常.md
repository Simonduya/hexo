---
title: JavaScript程序错误与异常
tags: JavaScript
categories: JavaScript
abbrlink: 48466cd5
date: 2023-05-24 22:17:28
---

## 程序错误与异常

### 访问对象的未知属性

在 JavaScript 中，如果一个对象的某个属性为 null 或 undefined，那么在访问该属性的方法或属性时会导致程序抛出异常并停止执行。

```javascript
const person = {
  name: "lili",
  address: {
    city: "shang",
  },
  kind: null,
};
//undefined
console.log(person.age);
//Uncaught TypeError: Cannot read properties of undefined (reading 'split')
console.log(person.age.split(""));
//不会执行
console.log(person.kind);
```

使用`try...catch`可以捕获异常，程序不会中断

```javascript
const person = {
  name: "lili",
  address: {
    city: "shang",
  },
  kind: null,
};
//undefined
console.log(person.age);
try {
  console.log(person.age.split(""));
} catch (e) {
  console.warn(e);
}

//依然执行
console.log(person.kind);
```

使用可选链操作符访问对象属性可以确保即使 对象的属性 为 null 或 undefined，代码也可以正常执行，避免程序抛出异常。

```javascript
const person = {
  name: "lili",
  address: {
    city: "shang",
  },
  kind: null,
};
//undefined
console.log(person.age);
console.log(person.age?.split(""));
//依然执行
console.log(person.kind);
```

#### 更多示例
以下是一个复杂对象的示例代码，演示了在 JavaScript 中访问属性或方法时可能出现异常的情况：

```js
const user = {
  name: 'Alice',
  age: 30,
  address: {
    street: '123 Main St',
    city: 'New York',
    state: 'NY',
    country: 'USA',
    zip: '10001',
  },
  orders: [
    {
      id: 1,
      date: '2023-05-24',
      items: [
        {
          sku: '001',
          name: 'Product A',
          price: 10.99,
          qty: 2,
        },
        {
          sku: '002',
          name: 'Product B',
          price: 5.99,
          qty: 3,
        },
      ],
    },
    {
      id: 2,
      date: '2023-05-23',
      items: [
        {
          sku: '003',
          name: 'Product C',
          price: 15.99,
          qty: 1,
        },
      ],
    },
  ],
};

// Accessing property that may not exist

console.log(user.phone); // undefined

// Accessing nested property that may not exist

console.log(user.address.zipcode); // TypeError: Cannot read property 'zipcode' of undefined

// Accessing array element that may not exist

console.log(user.orders[2]); // undefined

// Accessing property of array element that may not exist

console.log(user.orders[1].items[0].quantity); // TypeError: Cannot read property 'quantity' of undefined
```

在这个示例中，对象 `user` 包含了多层嵌套的属性和数组元素。如果在访问某个属性或方法时出现了未知的属性、数组元素或者 `null`/`undefined` 值，将会导致程序抛出异常并停止执行。

因此，在编写 JavaScript 程序时应该特别注意这种情况，并使用适当的方法来避免出现异常。例如，可以使用可选链操作符 `?.` 来避免访问不存在的属性或方法，或者使用条件判断语句来检查数组元素是否存在等。

#### 使用可选链操作符
以下是使用可选链操作符 `?.` 的示例代码，演示了如何避免访问不存在的属性或方法：

```js
// Accessing property that may not exist

console.log(user.phone?.number); // undefined

// Accessing nested property that may not exist

console.log(user.address?.zipcode); // undefined

// Accessing array element that may not exist

console.log(user.orders?.[2]); // undefined

// Accessing property of array element that may not exist

console.log(user.orders?.[1]?.items?.[0]?.quantity); // undefined
```

在这个示例中，使用了可选链操作符 `?.` 来避免访问可能不存在的属性、方法或数组元素。

例如，`user.phone?.number` 表示如果 `phone` 属性存在，则访问它的 `number` 属性，否则返回 `undefined`。

同样地，`user.address?.zipcode` 和 `user.orders?.[2]` 都表示在相应的属性或数组元素存在时才进行访问，否则返回 `undefined`。

最后，`user.orders?.[1]?.items?.[0]?.quantity` 使用了多重可选链操作符来避免深层次的属性访问出现异常。如果某个属性不存在，则整个表达式都会返回 `undefined`。

总之，可选链操作符是一种非常实用的语法特性，可以避免因为未知属性或方法而导致程序崩溃或停止执行。

### JavaScript错误类型示例代码
以下是 JavaScript 中错误类型的示例代码，它们都会导致程序抛出异常并停止执行：

1. `EvalError` 错误：当使用全局函数 eval() 中的代码存在错误时，JavaScript 抛出 EvalError 错误。

```javascript
eval("console.log('Hello, world!';"); // Uncaught EvalError: missing ) after argument list
```

2. `RangeError` 错误：当使用超出有效范围的值创建对象或数组时，JavaScript 抛出 RangeError 错误。

```javascript
new Array(-1); // Uncaught RangeError: Invalid array length
```

3. `ReferenceError` 错误：当尝试访问一个不存在的变量或函数时，JavaScript 抛出 ReferenceError 错误。

```javascript
console.log(a); // Uncaught ReferenceError: a is not defined

function foo() {
  bar();
}

foo(); // Uncaught ReferenceError: bar is not defined
```

4. `SyntaxError` 错误：当 JavaScript 代码包含语法错误时，例如括号不匹配、缺少分号等，JavaScript 抛出 SyntaxError 错误。

```javascript
console.log("Hello, world!" // Uncaught SyntaxError: missing ) after argument list
```

5. `TypeError` 错误：当尝试访问一个不存在或不支持的方法或属性时，JavaScript 抛出 TypeError 错误。

```javascript
const person = {
  name: "Tom",
  age: 25,
};

person.sayHi(); // Uncaught TypeError: person.sayHi is not a function
```

6. `URIError` 错误：当传递给 URI 相关的全局函数的参数无效时，例如解码无效的 URI 字符串，JavaScript 抛出 URIError 错误。

```javascript
decodeURIComponent("%"); // Uncaught URIError: URI malformed
```

7. `AggregateError` 错误：当 Promise.all() 或 Promise.allSettled() 方法中的一个或多个 Promise 拒绝了（rejected）时，JavaScript 抛出 AggregateError 错误。它包含一个具有所有拒绝原因的数组。

```javascript
Promise.all([
  Promise.resolve(1),
  Promise.reject("error"),
  Promise.resolve(3),
]).catch((err) => {
  console.log(err); // Uncaught AggregateError: error
});
```

8. `InternalError` 错误：当 JavaScript 引擎发生内部错误时，例如无限递归、堆栈溢出等，JavaScript 抛出 InternalError 错误。

```javascript
function foo() {
  foo();
}

foo(); // Uncaught InternalError: too much recursion
```

总之，这些错误类型都可能导致程序崩溃或停止执行，并且通常需要使用调试工具来找到和解决。在编写 JavaScript 程序时，应该仔细考虑并避免出现这些错误，以确保程序的正确性和稳定性。
