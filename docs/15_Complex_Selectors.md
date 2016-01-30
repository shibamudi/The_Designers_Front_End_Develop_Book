# 课程15：复杂选择器

选择器如果不是CSS中最重要的部分，也是其中之一。它们形成级联，并决定样式如何应用到页面中的元素上。

直到最近，对CSS的关注从未真正触及选择器。偶尔会有包含选择器规范在内的增量更新，但从没有任何突破性的改进。幸运的是，最近选择器得到了更多的关注，看看如何选择不同类型的元素和不同使用状态下的元素。

CSS3提供了新的选择器、开启一个全新的世界的机会以并对原有做法的改善。在这里我们将讨论选择器，原有的和新增的，以及如何最好地利用它们。

## 普通选择器

在深潜到一些更复杂的由CSS3提供的选择器之前，让我们先快速浏览一些今天看来更普通的选择器。这些选择器包括类型选择器、类选择器和ID选择器。

**类型选择器**基于自身类型匹配一个元素，确切地说就是元素如何在HTML中声明。**类选择器**基于自身class属性的值匹配一个元素，如有必要class属性的值可能重复用于多个元素以共用通用的样式。**ID选择器**基于自身id属性的值匹配一个元素，id属性的值是独一无二的，在一页中应只使用一次。

CSS

```css
h1 {...}
.tagline {...}
#intro {...}
```

HTML

```html
<section id="intro">
  <h1>...</h1>
  <h2 class="tagline">...</h2>
</section>
```

### 普通选择器概览

示例|分类|说明
---|---|---
`h1`|类型选择器|根据类型选择一个元素
`.tagline`|类选择器|根据class属性的值选择一个元素，在一页中可以使用多次
`#intro`|ID选择器|根据id属性的值选择一个元素，独一无二且在一页中只能使用一次

## 子选择器

子选择器提供了一个途径来选择包含在另一元素之中的元素，如此称这些元素为他们父元素的孩子。这种选择方式可以演变为两种不同的方法，后代选择器和直接子元素选择器。

### 后代选择器

后代选择器是最常用的子选择器，它匹配继承了指定祖先的每个元素。在文档树内，后代元素不一定直接位于祖先元素之后，像父-子关系，而是可以位于祖先元素内的任意位置。后代选择器由选择器内以空格分隔的元素构成，每个元素列表创建一个新的层次结构。

`article h2`是一个后代选择器，它只选择位于`article`元素之内的`h2`元素。注意，无论`h2`元素在哪，只要在`article`元素之内，它就会被选中。此外，任何`article`元素之外的`h2`元素都会回被选中。

如下，第3行和第5行被选中。

CSS

```css
article h2 {...}
```

HTML

```html
<h2>...</h2>
<article>
  <h2>This heading will be selected</h2>
  <div>
    <h2>This heading will be selected</h2>
  </div>
</article>
```

### 直接子元素选择器

有时后代选择器有点过于热心，选择的比希望的更多。有时只需要选择父元素的直接子类，而不是嵌套在祖先深处元素的每一个实例。此时可以在选择器中父元素与子元素之间放置一个大于号，`>`，使用直接子元素选择器。

例如，`article > p`是一个直接子元素选择器，它只匹配直接从属于`article`元素的`p`元素。任何`article`元素之外的`p`元素，或嵌套在其他元素而非`article`元素之内的`p`元素，都不会被选中。

如下，第3行是父元素`article`唯一一个直接`p`子元素，因而被选中。

CSS

```css
article > p {...}
```

HTML

```html
<p>...</p>
<article>
  <p>This paragraph will be selected</p>
  <div>
    <p>...</p>
  </div>
</article>
```

### 子选择器概览

示例|分类|说明
---|---|---
`article h2`|后代选择器|选择位于指定祖先元素内任意位置的元素
`article > p`|直接子选择器|选择指定父元素内紧邻的子元素

## Sibling Selectors

Knowing how to select children of an element is largely beneficial, and quite commonly seen. However sibling elements, those elements that share a common parent, may also need to be selected. These sibling selections can be made by way of the general sibling and adjacent sibling selectors.

### General Sibling Selector

The general sibling selector allow elements to be selected based on their sibling elements, those which share the same common parent. They are created by using the tilde character, `~`, between two elements within a selector. The first element identifies what the second element shall be a sibling with, and both of which must share the same parent.

The `h2 ~ p` selector is a general sibling selector that looks for `p` elements that follow, and share the same parent, of any `h2` elements. In order for a `p` element to be selected it must come after any `h2` element.

The paragraphs on lines 5 and 9 are selected as they come after the heading within the document tree and share the same parent as their sibling heading.

CSS

```css
h2 ~ p {...}
```

HTML

```html
<p>...</p>
<section>
  <p>...</p>
  <h2>...</h2>
  <p>This paragraph will be selected</p>
  <div>
    <p>...</p>
  </div>
  <p>This paragraph will be selected</p>
</section>
```

### Adjacent Sibling Selector

Occasionally a little more control may be desired, including the ability to select a sibling element that directly follows after another sibling element, which is where the adjacent sibling element comes in. The adjacent sibling selector will only select sibling elements directly following after another sibling element. Instead of using the tilde character, as with general sibling selectors, the adjacent sibling selector uses a plus character, `+`, between the two elements within a selector. Again, the first element identifies what the second element shall directly follow after and be a sibling with, and both of which must share the same parent.

Looking at the adjacent sibling selector `h2 + p` only `p` elements directly following after `h2` elements will be selected. Both of which must also share the same parent element.

The paragraph on line 5 is selected as it directly follows after its sibling heading along with sharing the same parent element, thus selected.

CSS

```css
h2 + p {...}
```

HTML

```html
<p>...</p>
<section>
  <p>...</p>
  <h2>...</h2>
  <p>This paragraph will be selected</p>
  <div>
    <p>...</p>
  </div>
  <p>...</p>
</section>
```

> ### Sibling Selectors Example

> HTML

> ```html
> <input type="checkbox" id="toggle">
> <label for="toggle">&#9776;</label>
> <nav>
>   <ul>
>     <li><a href="#">Home</a></li>
>     <li><a href="#">About</a></li>
>     <li><a href="#">Services</a></li>
>     <li><a href="#">Contact</a></li>
>   </ul>
> </nav>
> ```

> CSS

> ```css
> input {
>   display: none;
> }
> label,
> ul {
>   border: 1px solid #cecfd5;
>   border-radius: 6px;
> }
> label {
>   color: #0087cc;
>   cursor: pointer;
>   display: inline-block;
>   font-size: 18px;
>   padding: 5px 9px;
>   transition: all .15s ease;
> }
> label:hover {
>   color: #ff7b29;
> }
> input:checked + label {
>   box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.15);
>   color: #9799a7;
> }
> nav {
>   max-height: 0;
>   overflow: hidden;
>   transition: all .15s ease;
> }
> input:checked ~ nav {
>   max-height: 500px;
> }
> ul {
>   list-style: none;
>   margin: 8px 0 0 0;
>   padding: 0;
>   width: 100px;
> }
> li {
>   border-bottom: 1px solid #cecfd5;
> }
> li:last-child {
>   border-bottom: 0;
> }
> a {
>   color: #0087cc;
>   display: block;
>   padding: 6px 12px;
>   text-decoration: none;
> }
> a:hover {
>   color: #ff7b29;
> }
> ```

### Sibling Selectors Overview

Example|Classification|Explanation
---|---|---
`h2 ~ p`|General Sibling Selector|Selects an element that follows anywhere after the prior element, in which both elements share the same parent
`h2 + p`|Adjacent Sibling Selector|Selects an element that follows directly after the prior element, in which both elements share the same parent

## Attribute Selectors

Some of the common selectors looked at early may also be defined as attribute selectors, in which an element is selected based up on its class or ID value. These class and ID attribute selectors are widely used and extremely powerful but only the beginning. Other attribute selectors have emerged over the years, specifically taking a large leap forward with CSS3. Now elements can be selected based on whether an attribute is present and what its value may contain.

### Attribute Present Selector

The first attribute selector identifies an element based on whether it includes an attribute or not, regardless of any actual value. To select an element based on if an attribute is present or not simply include the attribute name in square brackets, `[]`, within a selector. The square brackets may or may not follow any qualifier such as an element type or class, all depending on the level of specificity desired.

CSS

```css
a[target] {...}
```

HTML

```html
<a href="#" target="_blank">...</a>
```

### Attribute Equals Selector

To identify an element with a specific, and exact matching, attribute value the same selector from before may be used, however this time inside of the square brackets following the attribute name, include the desired matching value. Inside the square brackets should be the attribute name followed by an equals sign, `=`, quotations, `""`, and inside of the quotations should be the desired matching attribute value.

CSS

```css
a[href="http://google.com/"] {...}
```

HTML

```html
<a href="http://google.com/">...</a>
```

### Attribute Contains Selector

When looking to find an element based on part of an attribute value, but not an exact match, the asterisk character, `*`, may be used within the square brackets of a selector. The asterisk should fall just after the attribute name, directly before the equals sign. Doing so denotes that the value to follow only needs to appear, or be contained, within the attribute value.

CSS

```css
a[href*="login"] {...}
```

HTML

```html
<a href="/login.php">...</a>
```

### Attribute Begins With Selector

In addition to selecting an element based on if an attribute value contains a stated value, it is also possible to select an element based on what an attribute value begins with. Using a circumflex accent, `^`, within the square brackets of a selector between the attribute name and equals sign denotes that the attribute value should begin with the stated value.

CSS

```css
a[href^="https://"] {...}
```

HTML

```html
<a href="https://chase.com/">...</a>
```

### Attribute Ends With Selector

Opposite of the begins with selector, there is also an ends with attribute selector. Instead of using the circumflex accent, the ends with attribute selector uses the dollar sign, `$`, within the square brackets of a selector between the attribute name and equals sign. Using the dollar sign denotes that the attribute value needs to end with the stated value.

CSS

```css
a[href$=".pdf"] {...}
```

HTML

```html
<a href="/docs/menu.pdf">...</a>
```

### Attribute Spaced Selector

At times attribute values may be spaced apart, in which only one of the words needs to be matched in order to make a selection. In this event using the tilde character, `~`, within the square brackets of a selector between the attribute name and equals sign denotes an attribute value that should be whitespace-separated, with one word matching the exact stated value.

CSS

```css
a[rel~="tag"] {...}
```

HTML

```html
<a href="#" rel="tag nofollow">...</a>
```

### Attribute Hyphenated Selector

When an attribute value is hyphen-separated, rather than whitespace-separated, the vertical line character, `|`, may be used within the square brackets of a selector between the attribute name and equals sign. The vertical line denotes that the attribute value may be hyphen-separated however the hyphen-separated words must begin with the stated value.

CSS

```css
a[lang|="en"] {...}
```

HTML

```html
<a href="#" lang="en-US">...</a>
```

> ### Attribute Selectors Example

> HTML

> ```html
> <ul>
>   <li><a href="#.pdf">PDF Document</a></li>
>   <li><a href="#.doc">Word Document</a></li>
>   <li><a href="#.jpg">Image File</a></li>
>   <li><a href="#.mp3">Audio File</a></li>
>   <li><a href="#.mp4">Video File</a></li>
> </ul>
> ```

> CSS

> ```css
> ul {
>   list-style: none;
>   margin: 0;
>   padding: 0;
> }
> a {
>   background-position: 0 50%;
>   background-repeat: no-repeat;
>   color: #0087cc;
>   padding-left: 22px;
>   text-decoration: none;
> }
> a:hover {
>   color: #ff7b29;
> }
> a[href$=".pdf"] {
>   background-image: url("images/pdf.png");
> }
> a[href$=".doc"] {
>   background-image: url("images/doc.png");
> }
> a[href$=".jpg"] {
>   background-image: url("images/image.png");
> }
> a[href$=".mp3"] {
>   background-image: url("images/audio.png");
> }
> a[href$=".mp4"] {
>   background-image: url("images/video.png");
> }
> ```

### Attribute Selectors Overview

Example|Classification|Explanation
---|---|---
`a[target]`|Attribute Present Selector|Selects an element if the given attribute is present
`a[href="http://google.com/"]`|Attribute Equals Selector|Selects an element if the given attribute value exactly matches the value stated
`a[href*="login"]`|Attribute Contains Selector|Selects an element if the given attribute value contains at least once instance of the value stated
`a[href^="https://"]`|Attribute Begins With Selector|Selects an element if the given attribute value begins with the value stated
`a[href$=".pdf"]`|Attribute Ends With Selector|Selects an element if the given attribute value ends with the value stated
`a[rel~="tag"]`|Attribute Spaced Selector|Selects an element if the given attribute value is whitespace-separated with one word being exactly as stated
`a[lang|="en"]`|Attribute Hyphenated Selector|Selects an element if the given attribute value is hyphen-separated and begins with the word stated

## Pseudo-classes

Pseudo-classes are similar to regular classes in HTML however they are not directly stated within the markup, instead they are a dynamically populated as a result of users actions or the document structure. The most common pseudo-class, and one you’ve likely seen before, is `:hover`. Notice how this pseudo-class begins with the colon character, `:`, as will all other pseudo-classes.

###　Link Pseudo-classes

Some of the more basic pseudo-classes include two revolving around links specifically. The `:link` and `:visited` pseudo-classes define if a link has or hasn’t been visited. To style an anchor which has not been visited the `:link` pseudo-class comes into play, where the `:visited` pseudo-class styles links that a user has already visited based on their browsing history.

```css
a:link {...}
a:visited {...}
User Action Pseudo-classes
```

Based on a users actions different pseudo-classes may be dynamically applied to an element, of which include the `:hover`, `:active`, and `:focus` pseudo-classes. The `:hover` pseudo-class is applied to an element when a user moves their cursor over the element, most commonly used with anchor elements. The `:active` pseudo-class is applied to an element when a user engages an element, such as clicking on an element. Lastly, the `:focus` pseudo-class is applied to an element when a user has made an element the focus point of the page, often by using the keyboard to tab from one element to another.

```css
a:hover {...}
a:active {...}
a:focus {...}
```

### User Interface State Pseudo-classes

As with the link pseudo-classes there are also some pseudo-classes generated around the user interface state of elements, particularly within form elements. These user interface element state pseudo-classes include `:enabled`, `:disabled`, `:checked`, and `:indeterminate`.

The `:enabled` pseudo-class selects an input that is in the default state of enabled and available for use, where the `:disabled` pseudo-class selects an input that has the disabled attribute tied to it. Many browsers by default will fade out disabled inputs to inform users that the input is not available for interaction, however those styles may be adjusted as wished with the `:disabled` pseudo-class.

```css
input:enabled {...}
input:disabled {...}
```

The last two user interface element state pseudo-classes of `:checked` and `:indeterminate` revolve around checkbox and radio button input elements. The `:checked` pseudo-class selects checkboxes or radio buttons that are, as you may expect, checked. When a checkbox or radio button has neither been selected or unselected it lives in an indeterminate state, from which the `:indeterminate` pseudo-class can be used to target these elements.

```css
input:checked {...}
input:indeterminate {...}
```

### Structural & Position Pseudo-classes

A handful of pseudo-classes are structural and position based, in which they are determined based off where elements reside in the document tree. These structural and position based pseudo-classes come in a few different shapes and sizes, each of which provides their own unique function. Some pseudo-classes have been around longer than others, however CSS3 brought way of an entire new set of pseudo-classes to supplement the existing ones.

#### :first-child, :last-child, & :only-child

The first structural and position based pseudo-classes one is likely to come across are the `:first-child`, `:last-child`, and `:only-child` pseudo-classes. The `:first-child` pseudo-class will select an element if it’s the first child within its parent, while the `:last-child` pseudo-class will select an element if it’s the last element within its parent. These pseudo-classes are prefect for selecting the first or last items in a list and so forth. Additionally, the `:only-child` will select an element if it is the only element within a parent. Alternately, the `:only-child` pseudo-class could be written as `:first-child:last-child`, however `:only-child` holds a lower specificity.

Here the selector `li:first-child` identifies the first list item within a list, while the selector `li:last-child` identifies the last list item within a list, thus lines 2 and 10 are selected. The selector `div:only-child` is looking for a division which is the single child of a parent element, without any other other siblings. In this case line 4 is selected as it is the only division within the specific list item.

CSS

```css
li:first-child {...}
li:last-child {...}
div:only-child {...}
```

HTML

```html
<ul>
  <li>This list item will be selected</li>
  <li>
    <div>This div will be selected</div>
  </li>
  <li>
    <div>...</div>
    <div>...</div>
  </li>
  <li>This list item will be selected</li>
</ul>
```

#### :first-of-type, :last-of-type, & :only-of-type

Finding the first, last, and only children of a parent is pretty helpful, and often all that is needed. However sometimes you only want to select the first, last, or only child of a specific type of element. For example, should you only want to select the first or last paragraph within an article, or perhaps the only image within an article. Fortunately this is where the `:first-of-type`, `:last-of-type`, and `:only-of-type` pseudo-selectors come into place.

The `:first-of-type` pseudo-class will select the first element of its type within a parent, while the `:last-of-type` pseudo-class will select the last element of its type within a parent. The `:only-of-type` pseudo-class will select an element if it is the only of its type within a parent.

In the example below the `p:first-of-type` and `p:last-of-type` pseudo-classes select the first and last paragraphs within the article respectively, regardless if they are actually the first or last children within the article. Lines 3 and 6 are selected reflex these selectors. The img:only-of-type selector identifies the image on line 5 as it is the only image to appear within the article, thus also selected.

CSS

```css
p:first-of-type {...}
p:last-of-type {...}
img:only-of-type {...}
```
HTML

```html
<article>
  <h1>...</h1>
  <p>This paragraph will be selected</p>
  <p>...</p>
  <img src="#"><!-- This image will be selected -->
  <p>This paragraph will be selected</p>
  <h6>...</h6>
</article>
```

Lastly there are a few structural and position based pseudo-classes that select elements based on a number or an algebraic expression. These pseudo-classes include `:nth-child(n)`, `:nth-last-child(n)`, `:nth-of-type(n)`, and `:nth-last-of-type(n)`. All of these unique pseudo-classes are prefixed with nth and accept a number or expression inside of the parenthesis, indicated by the character `n` argument.

The number or expression that falls within the parenthesis determines exactly what element, or elements, are to be selected. Using a number outright will count individual elements from the beginning or end of the document tree and then select one element, while using an expression will count numerous elements from the beginning or end of the document tree and select them in groups or multiples.

> ### Using Pseudo-class Numbers & Expressions

> As mentioned, using numbers outright within a pseudo-class will count from the beginning, or end, of the document tree and select one element accordingly. For example, the `li:nth-child(4)` selector will select the fourth list item within a list. Counting begins with the first list item and increases by one for each list item, until finally locating and selecting the forth item. When using a number outright it must be a positive number.

> Expressions for pseudo-classes fall in the format of `an`, `an+b`, `an-b`, `n+b`, `-n+b`, and `-an+b`. The same expression may be translated and read as `(a×n)±b`. The `a` variable stands for the multiplier in which elements will be counted in while the `b` variable stands for where the counting will begin or take place.

> For example, the `li:nth-child(3n)` selector will identify every third list item within a list. Using the expression this equates to `3×0`, `3×1`, `3×2`, and so forth. As you can see the results of this expression lead to the third, sixth, and every element a multiple of three being selected.

> Additionally, the `odd` and `even` keyword values may be used. As expected, these will select odd or even elements respectively. Should keyword values not be appealing the expression of `2n+1` would select all odd elements while the expression of `2n` would select all even elements.

> Using the `li:nth-child(4n+7)` selector will identify every forth list item starting with the seventh list item. Again, using the expression this equates to `(4×0)+7`, `(4×1)+7`, `(4×2)+7`, and so forth. The results of this expression leading to the seventh, eleventh, fifteenth, and every element a multiple of four here on out being selected.

> Using the `n` argument without being prefixed by a number results in the a variable being interpreted as 1. With the `li:nth-child(n+5)` selector every list item will be selected starting with the fifth list item, leaving the first four list items unselected. Within the expression this breaks down as `(1×0)+5`, `(1×1)+5`, `(1×2)+5`, and so forth.

> To make things a bit more complicated negative numbers may also be used. For example, the `li:nth-child(6n-4)` selector will start counting every sixth list item starting at negative four, selecting the second, eighth, and fourteenth list items and so forth. The same selector, `li:nth-child(6n-4)`, could also be written as `li:nth-child(6n+2)`, without the use of a negative b variable.

> A negative a variable, or a negative `n` argument, must be followed by a positive `b` variable. When preceded by a negative a variable or negative `n` argument the `b` variable identifies how high the counting will reach. For example, the `li:nth-child(-3n+12)` selector will select every third list item within the first twelve list items. The selector `li:nth-child(-n+9)` will select the first nine list items within a list as the `n` argument, without any stated `a` variable, is defaulted to `-1`.

#### :nth-child(n) & :nth-last-child(n)

With a general understanding of how the pseudo-class numbers and expressions work let’s take a look at the actual pseudo-classes in which these numbers and expressions may be used, the first of which being the `:nth-child(n)` and `:nth-last-child(n)` pseudo-classes. These pseudo-classes work a bit like the `:first-child` and `:last-child` pseudo-classes in that they look, and count, all of the elements within a parent and only select the element specifically identified. The `:nth-child(n)` works from the beginning of the document tree while the `:nth-last-child(n)` works from the end of the document tree.

Using the `:nth-child(n)` pseudo-class, let’s look at the `li:nth-child(3n)` selector. The selector here will identify every third list item, thus lines 4 and 7 are selected.

CSS

```css
li:nth-child(3n) {...}
```

HTML

```html
<ul>
  <li>...</li>
  <li>...</li>
  <li>This list item will be selected</li>
  <li>...</li>
  <li>...</li>
  <li>This list item will be selected</li>
</ul>
```

Using a different expression within the `:nth-child(n)` pseudo-class will yield a different selection. The `li:nth-child(2n+3)` selector, for example, will identify every second list item starting with the third and then onward. As a result, the list items lines 4 and 6 are selected.

CSS

```css
li:nth-child(2n+3) {...}
```

HTML

```html
<ul>
  <li>...</li>
  <li>...</li>
  <li>This list item will be selected</li>
  <li>...</li>
  <li>This list item will be selected</li>
  <li>...</li>
</ul>
```

Changing the expression again, this time with a negative value, yields new selection. Here the `li:nth-child(-n+4)` selector is identifying the top four list items, leaving the rest of the list items unselected, thus lines 2 through 5 are selected.

CSS

```css
li:nth-child(-n+4) {...}
```

HTML

```html
<ul>
  <li>This list item will be selected</li>
  <li>This list item will be selected</li>
  <li>This list item will be selected</li>
  <li>This list item will be selected</li>
  <li>...</li>
  <li>...</li>
</ul>
```

Adding an negative integer before the `n` argument changes the selection again. Here the `li:nth-child(-2n+5)` selector identifies every second list item within the first five list items, thus the list items on lines 2, 4, and 6 are selected.

CSS

```css
li:nth-child(-2n+5) {...}
```

HTML

```html
<ul>
  <li>This list item will be selected</li>
  <li>...</li>
  <li>This list item will be selected</li>
  <li>...</li>
  <li>This list item will be selected</li>
  <li>...</li>
</ul>
```

Changing from the `:nth-child(n)` pseudo-class to the `:nth-last-child(n)` pseudo-class switches the direction of counting, with counting starting from the end of the document tree using the `:nth-last-child(n)` pseudo-class. The `li:nth-last-child(3n+2)` selector, for example, will identify every third list item starting from the second to last item in a list, moving towards the beginning of the list. Here the list items on lines 3 and 6 are selected.

CSS

```css
li:nth-last-child(3n+2) {...}
```

HTML

```html
<ul>
  <li>...</li>
  <li>This list item will be selected</li>
  <li>...</li>
  <li>...</li>
  <li>This list item will be selected</li>
  <li>...</li>
</ul>
```

#### :nth-of-type(n) & :nth-last-of-type(n)

The `:nth-of-type(n)` and `:nth-last-of-type(n)` pseudo-classes are very similar to that of the `:nth-child(n)` and `:nth-last-child(n)` pseudo-classes, however instead of counting every element within a parent the `:nth-of-type(n)` and `:nth-last-of-type(n)` pseudo-classes only count elements of their own type. For example, when counting paragraphs within an article, the `:nth-of-type(n)` and `:nth-last-of-type(n)` pseudo-classes will skip any headings, divisions, or miscellaneous elements that are not paragraphs, while the `:nth-child(n)` and `:nth-last-child(n)` would count every element, no matter it’s type, only selecting the ones that match the element within the stated selector. Additionally, all of the same expression possibilities used within the `:nth-child(n)` and `:nth-last-child(n)` pseudo-classes are also available within the `:nth-of-type(n)` and `:nth-last-of-type(n)` pseudo-classes.

Using the `:nth-of-type(n)` pseudo-class within the `p:nth-of-type(3n)` selector we are able to identify every third paragraph within a parent, regardless of other sibling elements within the parent. Here the paragraphs on lines 5 and 9 are selected.

CSS

```css
p:nth-of-type(3n) {...}
```

HTML

```html
<article>
  <h1>...</h1>
  <p>...</p>
  <p>...</p>
  <p>This paragraph will be selected</p>
  <h2>...</h2>
  <p>...</p>
  <p>...</p>
  <p>This paragraph will be selected</p>
</article>
```

As with the `:nth-child(n)` and `:nth-last-child(n)` pseudo-classes, the primary difference between the `:nth-of-type(n)` and `:nth-last-of-type(n)` pseudo-classes is that the `:nth-of-type(n)` pseudo-class counts elements from the beginning of the document tree and the `:nth-last-of-type(n)` pseudo-class counts elements from the end of the document tree.

Using the `:nth-last-of-type(n)` pseudo-class we can write the `p:nth-last-of-type(2n+1)` selector which identifies every second paragraph from the end of a parent element starting with the last paragraph. Here the paragraphs on lines 4, 7, and 9 are selected.

CSS

```css
p:nth-last-of-type(2n+1) {...}
```

HTML

```html
<article>
  <h1>...</h1>
  <p>...</p>
  <p>This paragraph will be selected</p>
  <p>...</p>
  <h2>...</h2>
  <p>This paragraph will be selected</p>
  <p>...</p>
  <p>This paragraph will be selected</p>
</article>
```

### Target Pseudo-class

The `:target` pseudo-class is used to style elements when an element’s ID attribute value matches that of the URI fragment identifier. The fragment identifier within a URI can be recognized by the hash character, `#`, and what directly follows it. The URL `http://example.com/index.html#hello` includes the fragment identifier of `hello`. When this identifier matches the ID attribute value of an element on the page, `<section id="hello">` for example, that element may be identified and stylized using the `:target` pseudo-class. Fragment identifiers are most commonly seen when using on page links, or linking to another part of the same page.

Looking at the code below, if a user would visit a page with the URI fragment identifier of `#hello` the section with that same ID attribute value would be stylized accordingly using the `:target` pseudo-class. If the URI fragment identifier changes, and matches the ID attribute value of another section, that new section may be stylized using the same selector and pseudo-class from before.

CSS

```css
section:target {...}
```

HTML

```html
<section id="hello">...</section>
```

### Empty Pseudo-class

The `:empty` pseudo-class allows elements that do not contain children or text nodes to be selected. Comments, processing instructions, and empty text nodes are not considered children and are not treated as such.

Using the `div:empty` pseudo-class will identify divisions without any children or text nodes. Below the divisions on lines 2 and 3 are selected as they are completely empty. Even though the second division contains a comment it is not considered to be a child, thus leaving the division empty. The first division contains text, the third division contains one blank text space, and the last division contains a strong child element, thus they are all ruled out and are not selected.

CSS

```css
div:empty {...}
```

HTML

```html
<div>Hello</div>
<div><!-- Coming soon --></div><!-- This div will be selected -->
<div></div><!-- This div will be selected -->
<div> </div>
<div><strong></strong></div>
```

### Negation Pseudo-class

The negation pseudo-class, `:not(x)`, is a pseudo-class that takes an argument which is filtered out from the selection to be made. The `p:not(.intro)` selector uses the negation pseudo-class to identify every paragraph element without the class of `intro`. The paragraph element is identified at the beginning of the selector followed by the `:not(x)` pseudo-class. Inside of the parentheses falls the negation selector, the class of `.intro` in this case.

Below both the `div:not(.awesome)` and `:not(div)` selectors use the `:not(x)` pseudo-class. The `div:not(.awesome)` selector identifies any division without the class of awesome, while the `:not(div)` selector identifies any element that isn’t a division. As a result the division on line 1 is selected as well as the two sections on lines 3 and 4, thus they are marked bold. The only element not selected is the division with the class of awesome, as it falls outside of the two negation pseudo-classes.

CSS

```css
div:not(.awesome) {...}
:not(div) {...}
```

HTML

```html
<div>This div will be selected</div>
<div class="awesome">...</div>
<section>This section will be selected</section>
<section class="awesome">This section will be selected</section>
```

> ### Pseudo-classes Example

> HTML

> ```html
> <table>
>   <thead>
>     <tr>
>       <th>Number</th>
>       <th>Player</th>
>       <th>Position</th>
>       <th>Height</th>
>       <th>Weight</th>
>     </tr>
>   </thead>
>   <tbody>
>     <tr>
>       <td>8</td>
>       <td>Marco Belinelli</td>
>       <td>G</td>
>       <td>6-5</td>
>       <td>195</td>
>     </tr>
>     <tr>
>       <td>5</td>
>       <td>Carlos Boozer</td>
>       <td>F</td>
>       <td>6-9</td>
>       <td>266</td>
>     </tr>
>     ...
>   </tbody>
> </table>
> ```

> CSS

> ```css
> table {
>   border-collapse: separate;
>   border-spacing: 0;
>   width: 100%;
> }
> th,
> td {
>   padding: 6px 15px;
> }
> th {
>   background: #42444e;
>   color: #fff;
>   text-align: left;
> }
> tr:first-child th:first-child {
>   border-top-left-radius: 6px;
> }
> tr:first-child th:last-child {
>   border-top-right-radius: 6px;
> }
> td {
>   border-right: 1px solid #c6c9cc;
>   border-bottom: 1px solid #c6c9cc;
> }
> td:first-child {
>   border-left: 1px solid #c6c9cc;
> }
> tr:nth-child(even) td {
>   background: #eaeaed;
> }
> tr:last-child td:first-child {
>   border-bottom-left-radius: 6px;
> }
> tr:last-child td:last-child {
>   border-bottom-right-radius: 6px;
> }
> ```

Pseudo-classes Overview

Example|Classification|Explanation
---|---|---
`a:link`|Link Pseudo-class|Selects a link that has not been visited by a user
`a:visited`|Link Pseudo-class|Selects a link that has been visited by a user
`a:hover`|Action Pseudo-class|Selects an element when a user has hovered their cursor over it
`a:active`|Action Pseudo-class|Selects an element when a user has engaged it
`a:focus`|Action Pseudo-class|Selects an element when a user has made it their focus point
`input:enabled`|State Pseudo-class|Selects an element in the default enabled state
`input:disabled`|State Pseudo-class|Selects an element in the disabled state, by way of the disabled attribute
`input:checked`|State Pseudo-class|Selects a checkbox or radio button that has been checked
`input:indeterminate`|State Pseudo-class|Selects a checkbox or radio button that neither been checked or unchecked, leaving it in an indeterminate state
`li:first-child`|Structural Pseudo-class|Selects an element that is the first within a parent
`li:last-child`|Structural Pseudo-class|Selects an element that is the last within a parent
`div:only-child`|Structural Pseudo-class|Selects an element that is the only element within a parent
`p:first-of-type`|Structural Pseudo-class|Selects an element that is the first of it’s type within a parent
`p:last-of-type`|Structural Pseudo-class|Selects an element that is the last of it’s type within a parent
`img:only-of-type`|Structural Pseudo-class|Selects an element that is the only of it’s type within a parent
`li:nth-child(2n+3)`|Structural Pseudo-class|Selects an element that matches the given number or expression, counting all elements from the beginning of the document tree
`li:nth-last-child(3n+2)`|Structural Pseudo-class|Selects an element that matches the given number or expression, counting all elements from the end of the document tree
`p:nth-of-type(3n)`|Structural Pseudo-class|Selects an element that matches the given number or expression, counting only elements of it’s type from the beginning of the document tree
`p:nth-last-of-type(2n+1)`|Structural Pseudo-class|Selects an element that matches the given number or expression, counting only elements of it’s type from the end of the document tree
`section:target`|Target Pseudo-class|Selects an element whose ID attribute value matches that of the URI fragment identifier
`div:empty`|Empty Pseudo-class|Selects an element that does not contain any children or text nodes
`div:not(.awesome)`|Negation Pseudo-class|Selects an element not represented by the stated argument

## Pseudo-elements

Pseudo-elements are dynamic elements that don’t exist in the document tree, and when used within selectors these pseudo-elements allow unique parts of the page to be stylized. One important point to note, only one pseudo-element may be used within a selector at a given time.

### Textual Pseudo-elements

The first pseudo-elements ever released were the `:first-letter` and `:first-line` textual pseudo-elements. The `:first-letter` pseudo-element will identify the first letter of text within an element, while the `:first-line` pseudo-element will identify the first line of text within an element.

In the demonstration below the first letter of the paragraph with the class of `alpha` is set in a larger font size and colored orange, as is the first line of the paragraph with the class of `bravo`. These selections are made by use of the `:first-letter` and `:first-line` textual pseudo-elements respectively.

CSS

```css
.alpha:first-letter,
.bravo:first-line {
  color: #ff7b29;
  font-size: 18px;
}
```

HTML

```html
<p class="alpha">Lorem ipsum dolor...</p>
<p class="bravo">Integer eget enim...</p>
```

### Generated Content Pseudo-elements

The `:before` and `:after` generated content pseudo-elements create new inline level pseudo-elements just inside the selected element. Most commonly these pseudo-elements are used in conjunction with the `content` property to add insignificant information to a page, however that is not always the case. Additional uses of these psuedo-elements may be to add user interface components to the page without having to clutter the document with unsemantic elements.

The `:before` pseudo-element creates an pseudo-element before, or in front of, the selected element, while the `:after` pseudo-element creates an pseudo-element after, or behind, the selected element. These pseudo-elements appear nested within the selected element, not outside of it. Below the `:after` pseudo-element is used to display the `href` attribute value of anchor links within parentheses after the actual links. The information here is helpful, but not ultimately necessary should a browser not support these pseudo-elements.

CSS

```css
a:after {
  color: #9799a7;
  content: " (" attr(href) ")";
  font-size: 11px;
}
```

HTML

```html
<a href="http://google.com/">Search the Web</a>
<a href="http://learn.shayhowe.com/">Learn How to Build Websites</a>
```

### Fragment Pseudo-element

The `::selection` fragment pseudo-element identifies part of the document that has been selected, or highlighted, by a user’s actions. The selection may then be stylized, however only using the `color`, `background`, `background-color`, and `text-shadow` properties. It is worth noting, the `background-image` property is ignore. While the shorthand `background` property may be used to add a color, any images will be ignored.

> ### Single Colon (:) versus Double Colons (::)

> The fragment pseudo-element was added with CSS3 and in attempt to differentiate pseudo-classes from pseudo-elements the double colons were added to pseudo-elements. Fortunately most browsers will support both values, single or double colons, for pseudo-elements however the `::selection` pseudo-element must always start with double colons.

When selecting any of the text within the demonstration below the background will appear orange and any text shadows will be removed thanks to the `::selection` fragment pseudo-element. Also note, the `::-moz-selection` Mozilla prefixed fragment pseudo-element has been added to ensure the best support for all browsers.

```css
::-moz-selection {
    background: #ff7b29;
}
::selection {
  background: #ff7b29;
}
```

> Pseudo-elements Example

> HTML

> ```html
> <a class="arrow" href="#">Continue Reading</a>
> ```

> CSS

> ```css
> .arrow {
>   background: #2db34a;
>   color: #fff;
>   display: inline-block;
>   height: 30px;
>   line-height: 30px;
>   padding: 0 12px;
>   position: relative;
>   text-decoration: none;
> }
> .arrow:before,
> .arrow:after {
>   content: "";
>   height: 0;
>   position: absolute;
>   width: 0;
> }
> .arrow:before {
>   border-bottom: 15px solid #2db34a;
>   border-left: 15px solid transparent;
>   border-top: 15px solid #2db34a;
>   left: -15px;
> }
> .arrow:after {
>   border-bottom: 15px solid transparent;
>   border-left: 15px solid #2db34a;
>   border-top: 15px solid transparent;
>   right: -15px;
> }
> .arrow:hover {
>   background: #ff7b29;
> }
> .arrow:hover:before {
>   border-bottom: 15px solid #ff7b29;
>   border-top: 15px solid #ff7b29;
> }
> .arrow:hover:after {
>   border-left: 15px solid #ff7b29;
> }
> ```

### Pseudo-elements Overview

Example|Classification|Explanation
---|---|---
`.alpha:first-letter`|Textual Pseudo-elements|Selects the first letter of text within an element
`.bravo:first-line`|Textual Pseudo-elements|Selects the first line of text within an element
`div:before`|Generated Content|Creates a pseudo-element inside the selected element at the beginning
`a:after`|Generated Content|Creates a pseudo-element inside the selected element at the end
`::selection`|Fragment Pseudo-element|Selects the part of a document which has been selected, or highlighted, by a users actions

> ### Selector Browser Support

> While these selectors provide a variety of opportunity and the ability to do some truly amazing things with CSS, they are at times plagued by poor browser support. Before doing anything too critical check the selectors you are wishing to use across your visitors most common browsers, and then make the judgment call as to whether they are appropriate or not.

> CSS3.info provides a CSS3 Selectors Test tool which will inform you as to which selectors are supported by the browser in use. It’s also never a bad idea to check browser support directly from the vendor.

> Additionally, Selectivizr, a JavaScript utility, provides great support for these selectors in Internet Explorer 6-8. More support, should it be necessary, can also be provided by jQuery selectors.

-
> ### Selector Speed & Performance

> It is important to pay attention the speed and performance of selectors, as using too many intricate selectors can slow down the rendering of a page. Be attentive and when a selector begins to look a bit foreign think about revisiting it, and seeing if a better solution can be found.

## Resources & Links

* [The 30 CSS Selectors you Must Memorize](http://net.tutsplus.com/tutorials/html-css-techniques/the-30-css-selectors-you-must-memorize/) via Nettuts+
* [Child and Sibling Selectors](http://css-tricks.com/child-and-sibling-selectors/) via CSS-Tricks
* [CSS3 Substring Matching Attribute Selectors](http://www.css3.info/preview/attribute-selectors/) via CSS3.info
* [How To Use CSS3 Pseudo-Classes](http://coding.smashingmagazine.com/2011/03/30/how-to-use-css3-pseudo-classes/) via Smashing Magazine
* [Understanding :nth-child Pseudo-class Expressions](http://reference.sitepoint.com/css/understandingnthchildexpressions) via SitePoint
* [Taming Advanced CSS Selectors](http://coding.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/) via Smashing Magazine

