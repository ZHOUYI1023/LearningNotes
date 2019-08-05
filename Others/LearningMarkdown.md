# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

ctrl-k v	Open preview to the Side

*这会是 斜体 的文字*
**这会是 粗体 的文字**
*你也 **组合** 这些符号*
~~这个文字将会被横线删除~~

* Item 1
* Item 2
  * Item 2a
  * Item 2b

1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b

---

我觉得你应该在这里使用 `<addr>` 

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

```javascript {.line-numbers}
function add(x, y) {
  return x + y
}
```

```javascript {highlight=10}
function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y

```

```javascript {highlight=[1-10,15,20-22]}
function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
  function add(x, y) {
  return x + y
```

- [x] @mentions, #refs, [http://testwebsitelink.com/](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item

&ensp;&ensp;30^th^

&emsp;&emsp;H~2~O

Content [^1]

[^1]: Hi! This is a footnote

*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
The HTML specification is maintained by the W3C.

==marked==

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

---
presentation:
  width: 1280
  height: 720
---

$ f(x) = sin(x) + x^5 + x/2 $

$\nabla \partial$

$\begin{bmatrix}
   a & b \\
   c & d
\end{bmatrix}$

$\textstyle\sum_{i=1}^n$

$\textcolor{blue}{F=ma}$

$\frac{a}{b+1}\\ 
a/(b+1)
$

$\sum_{1 < i\le j\ge n} x_{ij}$

email: foo@bar.com

[Click me!](http://test.com/)
[Click me!](http://test.com/ "Link to Test.com")

[Click this link][link1] for more info about it!
[Also check out this link][foobar] if you want to.

[link1]: http://test.com/ "Cool!"
[foobar]: http://foobar.biz/ "Alright!"

![This is the alt-attribute for my image](http://baidu.com/pic/doge.png "An optional title")

![This is the alt-attribute.][myimage]

[myimage]: /home/yi/Documents/LearningSeries/Font_2.PNG "if you need a title, it's here"
