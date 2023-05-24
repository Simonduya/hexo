## slice，splice，split方法对比
`slice()`、`splice()` 和 `split()` 这三个方法的用途和参数有些相似，容易混淆。以下是它们各自的用途和区别

1. `slice()`: 用于从数组或字符串中提取一段子序列，并返回一个新的数组或字符串，原数组或字符串不会被修改。

   - 参数：
     - `start`：表示子序列的起始位置（包括该位置）。
     - `end`：表示子序列的结束位置（不包括该位置）。
   - 示例：
     ```js
     const arr = [0, 1, 2, 3, 4];
     const slicedArr = arr.slice(1, 4); // [1, 2, 3]
     console.log(arr); // [0, 1, 2, 3, 4]
     ```

2. `splice()`: 用于向数组中插入或删除元素，并返回被删除的元素组成的数组。该方法会直接修改原数组。

   - 参数：
     - `start`：表示要插入或删除的起始位置。
     - `deleteCount`：表示要删除的元素个数，如果省略，则从 `start` 开始后面的所有元素都会被删除。
     - `item1, item2, ...`：表示要插入到数组中的元素。
   - 示例：
     ```js
     const arr = [0, 1, 2, 3, 4];
     const deletedArr = arr.splice(1, 3, "a", "b", "c"); // [1, 2, 3]
     console.log(arr); // [0, "a", "b", "c", 4]
     ```

3. `split()`: 用于将字符串按照指定的分隔符分割成一个数组，返回该数组。原字符串不会被修改。

   - 参数：
     - `separator`：表示分隔符，可以是一个字符串或正则表达式对象。如果省略，则返回包含整个字符串的单元素数组。
     - `limit`：表示返回数组的最大长度。如果省略，则不限制长度。
   - 示例：
     ```js
     const str = "hello world";
     const splittedStr = str.split(" "); // ["hello", "world"]
     console.log(str); // "hello world"
     ```

可以根据方法名来记忆这些方法的区别：

- `slice()`：切片，用于提取一段子序列。
- `splice()`：拼接和切割，用于向数组中插入或删除元素。
- `split()`：分裂，用于将字符串分割成一个数组。
