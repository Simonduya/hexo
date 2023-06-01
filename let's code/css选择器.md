# 关系选择器

## 后代选择器

后代选择器——典型用单个空格（" "）字符——组合两个选择器

```html
.box p { color: red; }

<div class="box">
  <p>Text in .box</p>
  <p>p2</p>
</div>
<p>Text not in .box</p>
```

`Text in .box` , `p2`都会变为红色

## 子代关系选择器

子代关系选择器是个大于号（>），只会在选择器选中直接子元素的时候匹配。继承关系上更远的后代则不会匹配。

```html
ul > li { border-top: 5px solid red; }

<ul>
  <li>Unordered item //1</li>
  <li>
    Unordered item //2
    <ol>
      <li>Item 1 //3</li>
      <li>Item 2 //4</li>
    </ol>
  </li>
</ul>
```

//1 和 //2 会被加上`border-top`, 而//3 //4 不会, 因为他们不是直接的子元素, 但如果此时移除`ul > li`之间的 `>`, 那么所有`li`都会被加上`border-top`

## 邻接兄弟

邻接兄弟选择器（+）用来选中恰好处于另一个在继承关系上同级的元素旁边的物件。

```html
div+p { color: red; }

<p>p1</p>
<div>div1</div>
<p>p2</p>
<p>p3</p>
```

只有 p2 变红

## 通用兄弟

如果你想选中一个元素的兄弟元素，即使它们不直接相邻，你还是可以使用通用兄弟关系选择器（~）。

```html
div~p { color: red; }

<p>p1</p>
<div>div1</div>
<p>p2</p>
<p>p3</p>
```

p2, p3 会变红; p1 不会变红;

# 伪类选择器

伪类是选择器的一种，它用于选择处于特定状态的元素，比如当它们是这一类型的第一个元素时，或者是当鼠标指针悬浮在元素上面的时候。

## :first-child

```html
body p:first-child { color: red; }

<p>p0</p>
<p>p1</p>
<div>div1</div>
<p>p2</p>
<p>p3</p>
```

只有 p0 会变红

## :last-child

只有 p3 会变红

## :nth-child

:nth-child(an+b) 这个 CSS 伪类首先找到所有当前元素的兄弟元素，然后按照位置先后顺序从 1 开始排序，选择的结果为 CSS 伪类:nth-child 括号中表达式（an+b）匹配到的元素集合（n=0，1，2，3...）。

```css
    body p:nth-child(4) {
      color: red;
    }
  <p>p0</p>
  <p>p1</p>
  <div>
    div1
  </div>
  <p>p2</p>
  <p>p3</p>
```
`body p:nth-child(1)`: p0变红;

`body p:nth-child(2)`: p1变红;

`body p:nth-child(3)`: 没有元素变红;

`body p:nth-child(4)`: p2变红;

`body p:nth-child(5)`: p3变红;

## 用户行为类

:focus——只会在用户使用键盘控制，选定元素的时候激活。

```html
a:link, a:visited { color: rebeccapurple; font-weight: bold; } a:hover {
color:hotpink; }
```
