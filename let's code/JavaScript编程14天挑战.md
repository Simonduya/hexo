## 2665. 计数器 II

请你写一个函数 createCounter. 这个函数接收一个初始的整数值 init 并返回一个包含三个函数的对象。

这三个函数是：

increment() 将当前值加 1 并返回。
decrement() 将当前值减 1 并返回。
reset() 将当前值设置为 init 并返回。

tips: 记得要 return 这些内部方法, 不然调用不了;

```js
var createCounter = function (init) {
  let _init = init;
  let temp = init;
  function increment() {
    return ++_init;
  }
  function reset() {
    _init = temp;
    return temp;
  }
  function decrement() {
    return --_init;
  }
  return {
    increment,
    reset,
    decrement,
  };
};

const counter = createCounter(5);
console.log(counter.increment());
console.log(counter.reset());
console.log(counter.decrement());
```

### 2635. 转换数组中的每个元素

编写一个函数，这个函数接收一个整数数组 arr 和一个映射函数 fn ，通过该映射函数返回一个新的数组。

返回数组的创建语句应为 returnedArray[i] = fn(arr[i], i) 。

请你在不使用内置方法 Array.map 的前提下解决这个问题。

tips: 就是实现自己的 map 方法

`map` 方法是 JavaScript 数组对象的一个内置方法，用于对数组中的每个元素都执行一次回调函数，并将返回值存入一个新数组中返回。下面是手动实现一个 `map` 方法的示例代码：

```javascript
var map = function (arr, fn) {
  var result = []; // 用于存放结果的数组
  for (var i = 0; i < arr.length; i++) {
    result.push(fn(arr[i], i, arr)); // 执行回调函数并将返回值存入结果数组
  }
  return result; // 返回结果数组
};

// 示例用法
var arr = [1, 2, 3];
var squareArr = map(arr, function (item) {
  return item * item;
});
console.log(squareArr); // 输出 [1, 4, 9]
```

在上面的代码中，我们定义了一个名为 `map` 的函数，该函数接受两个参数：要处理的数组和一个回调函数。在函数内部，我们首先创建一个空数组，用于存放回调函数的返回值。然后，我们使用 for 循环遍历数组中的每个元素，并使用回调函数处理它。最后，将返回值存入结果数组，并将结果数组返回。这样就完成了一个简单的 `map` 方法的实现。

注意，在回调函数中，除了数组元素本身之外，还可以传入当前元素的索引和原始数组作为参数。这可以方便地进行更复杂的操作，例如根据元素索引来生成新值。另外，需要注意的是，我们没有修改原始数组的值，而是返回了一个新的数组来存放结果。这是 `map` 方法的标准实现方式。

## 2634. 过滤数组中的元素

请你编写一个函数，该函数接受一个整数数组参数 arr 和一个过滤函数 fn，并返回一个过滤后元素数量较少或元素数量相等的新数组。

返回的数组应该只包含通过过滤函数 fn(arr[i]， i) 计算后为真值的元素。

请你在不使用内置函数 Array.filter 的前提下解决该问题。

`filter` 方法是 JavaScript 数组对象的一个内置方法，用于对数组中的每个元素都执行一次回调函数，并返回一个新数组，该数组由执行回调函数时返回值为 `true` 的元素组成。以下是手动实现一个 `filter` 方法的示例代码：

```javascript
var filter = function (arr, fn) {
  var result = []; // 用于存放结果的数组
  for (var i = 0; i < arr.length; i++) {
    if (fn(arr[i], i, arr)) {
      // 判断是否应该包含该元素
      result.push(arr[i]); // 将该元素添加到结果数组中
    }
  }
  return result; // 返回结果数组
};

// 示例用法
var arr = [1, 2, 3];
var evenArr = filter(arr, function (item) {
  return item % 2 === 0;
});
console.log(evenArr); // 输出 [2]
```

```js
var filter = function (arr, fn) {
  const ans = [];
  for (let i = 0; i < arr.length; i++) {
    fn(arr[i], i, arr) && ans.push(arr[i]);
  }
  return ans;
};
```

在上面的代码中，我们定义了一个名为 `filter` 的函数，该函数接受两个参数：要处理的数组和一个回调函数。在函数内部，我们首先创建一个空数组，用于存放满足条件的元素。然后，我们使用 for 循环遍历数组中的每个元素，并使用回调函数检查它是否符合要求。如果符合要求，则将该元素添加到结果数组中。最后，将结果数组返回。

注意，在回调函数中，除了数组元素本身之外，还可以传入当前元素的索引和原始数组作为参数。这可以方便地进行更复杂的操作，例如根据元素索引来判断是否应该包含该元素。另外，需要注意的是，我们没有修改原始数组的值，而是返回了一个新的数组来存放结果。这是 `filter` 方法的标准实现方式。

## 2626. 数组归约运算

请你编写一个函数，它的参数为一个整数数组 nums 、一个计算函数 fn 和初始值 init 。返回一个数组 归约后 的值。

你可以定义一个数组 归约后 的值，然后应用以下操作： val = fn(init, nums[0]) ， val = fn(val, nums[1]) ， val = fn(val, nums[2]) ，... 直到数组中的每个元素都被处理完毕。返回 val 的最终值。

如果数组的长度为 0，它应该返回 init 的值。

请你在不使用内置数组方法的 Array.reduce 前提下解决这个问题。

你可以假设数组中的每个函数接受一个整型参数作为输入，并返回一个整型作为输出。
`reduce` 方法是 JavaScript 数组对象的一个内置方法，用于对数组中的每个元素都执行一次回调函数，并将所有返回值累加到一个最终的结果值中。以下是手动实现一个 `reduce` 方法的示例代码：

```javascript
var reduce = function (nums, fn, init) {
  var result = init; // 用于存放结果的变量，初始值为 init
  for (var i = 0; i < nums.length; i++) {
    result = fn(result, nums[i], i, nums); // 执行回调函数并更新结果值
  }
  return result; // 返回最终结果值
};

// 示例用法
var arr = [1, 2, 3];
var sum = reduce(
  arr,
  function (prev, curr) {
    return prev + curr;
  },
  0
);
console.log(sum); // 输出 6
```

在上面的代码中，我们定义了一个名为 `reduce` 的函数，该函数接受三个参数：要处理的数组、一个回调函数和一个初始值。在函数内部，我们首先将初始值赋值给结果变量 `result`。然后，我们使用 for 循环遍历数组中的每个元素，并使用回调函数更新结果变量的值。最后，将结果变量作为最终结果值返回。

注意，在回调函数中，第一个参数表示当前的结果值，第二个参数表示当前元素的值，第三个参数表示当前元素的索引，第四个参数表示原始数组。在执行回调函数时，需要返回一个新的结果值，并更新到结果变量中。这样就可以依次处理数组中的每个元素，将它们的值累加到结果中。

另外需要注意的是，我们在函数内部使用了变量 `result` 来存放最终的结果值，而不是像你的代码一样使用变量 `ans`。同时，对于 `ans` 变量来说，需要初始化为 0，否则会得到一个 `NaN` 类型的结果。

## 2629. 复合函数
请你编写一个函数，它接收一个函数数组 [f1, f2, f3，…， fn] ，并返回一个新的函数 fn ，它是函数数组的 复合函数 。

[f(x)， g(x)， h(x)] 的 复合函数 为 fn(x) = f(g(h(x))) 。

一个空函数列表的 复合函数 是 恒等函数 f(x) = x 。

你可以假设数组中的每个函数接受一个整型参数作为输入，并返回一个整型作为输出。

## 2666. 只允许一次函数调用

给定一个函数 fn ，它返回一个新的函数，返回的函数与原始函数完全相同，只不过它确保 fn 最多被调用一次。

第一次调用返回的函数时，它应该返回与 fn 相同的结果。
第一次后的每次调用，它应该返回 undefined 。

## 2623. 记忆函数
请你编写一个函数，它接收另一个函数作为输入，并返回该函数的 记忆化 后的结果。

记忆函数 是一个对于相同的输入永远不会被调用两次的函数。相反，它将返回一个缓存值。

你可以假设有 3 个可能的输入函数：sum 、fib 和 factorial 。

 sum 接收两个整型参数 a 和 b ，并返回 a + b 。
 fib 接收一个整型参数 n ，如果 n <= 1 则返回 1，否则返回 fib (n - 1) + fib (n - 2)。
 factorial 接收一个整型参数 n ，如果 n <= 1 则返回  1 ，否则返回 factorial(n - 1) * n 。
