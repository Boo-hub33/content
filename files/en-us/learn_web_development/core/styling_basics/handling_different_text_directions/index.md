---
title: Handling different text directions
short-title: Multiple text directions
slug: Learn_web_development/Core/Styling_basics/Handling_different_text_directions
page-type: learn-module-chapter
sidebar: learnsidebar
---

Many of the properties and values that we have encountered so far in our CSS learning have been tied to the physical dimensions of our screen. We create borders on the top, right, bottom, and left of a box, for example. These physical dimensions map very neatly to content that is viewed horizontally, and by default the web tends to support left-to-right languages (e.g., English or French) better than right-to-left languages (such as Arabic).

In recent years however, CSS has evolved in order to better support different directionality of content, including right-to-left but also top-to-bottom content (such as Japanese) — these different directionalities are called **writing modes**. As you progress in your study and begin to work with layout, an understanding of writing modes will be very helpful to you, therefore we will introduce them now.

<table>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>
        <a
          href="/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Installing_software"
          >Basic software installed</a
        >, basic knowledge of
        <a
          href="/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Dealing_with_files"
          >working with files</a
        >, HTML basics (study
        <a href="/en-US/docs/Learn_web_development/Core/Structuring_content"
          >Introduction to HTML</a
        >), and an idea of how CSS works (study
        <a href="/en-US/docs/Learn_web_development/Core/Styling_basics">CSS Styling basics</a>.)
      </td>
    </tr>
    <tr>
      <th scope="row">Objective:</th>
      <td>To understand the importance of writing modes to modern CSS.</td>
    </tr>
  </tbody>
</table>

## What are writing modes?

A writing mode in CSS refers to whether the text is running horizontally or vertically. The {{cssxref("writing-mode")}} property lets us switch from one writing mode to another. You don't need to be working in a language which uses a vertical writing mode to want to do this — you could also change the writing mode of parts of your layout for creative purposes.

In the example below we have a heading displayed using `writing-mode: vertical-rl`. The text now runs vertically. Vertical text is common in graphic design, and can be a way to add a more interesting look and feel to your web design.

```html live-sample___simple-vertical
<h1>Play with writing modes</h1>
```

```css live-sample___simple-vertical
body {
  font-family: sans-serif;
  height: 300px;
}
h1 {
  writing-mode: vertical-rl;
  color: white;
  background-color: black;
  padding: 10px;
}
```

{{EmbedLiveSample("simple-vertical", "", "350px")}}

The three possible values for the [`writing-mode`](/en-US/docs/Web/CSS/writing-mode) property are:

- `horizontal-tb`: Top-to-bottom block flow direction. Sentences run horizontally.
- `vertical-rl`: Right-to-left block flow direction. Sentences run vertically.
- `vertical-lr`: Left-to-right block flow direction. Sentences run vertically.

So the `writing-mode` property is in reality setting the direction in which block-level elements are displayed on the page — either from top-to-bottom, right-to-left, or left-to-right. This then dictates the direction text flows in sentences.

## Writing modes and block and inline layout

We have already discussed [block and inline layout](/en-US/docs/Web/CSS/CSS_display/Block_and_inline_layout_in_normal_flow), and the fact that some things display as block elements and others as inline elements. As we have seen described above, block and inline is tied to the writing mode of the document, and not the physical screen. Blocks are only displayed from the top to the bottom of the page if you are using a writing mode that displays text horizontally, such as English.

If we look at an example this will become clearer. In this next example I have two boxes that contain a heading and a paragraph. The first uses `writing-mode: horizontal-tb`, a writing mode that is written horizontally and from the top of the page to the bottom. The second uses `writing-mode: vertical-rl`; this is a writing mode that is written vertically and from right to left.

```html live-sample___block-inline
<div class="wrapper">
  <div class="box horizontal">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
  </div>
  <div class="box vertical">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
  </div>
</div>
```

```css live-sample___block-inline
body {
  font-family: sans-serif;
  height: 300px;
}
.wrapper {
  display: flex;
}

.box {
  border: 1px solid #ccc;
  padding: 0.5em;
  margin: 10px;
}

.horizontal {
  writing-mode: horizontal-tb;
}

.vertical {
  writing-mode: vertical-rl;
}
```

{{EmbedLiveSample("block-inline", "", "350px")}}

When we switch the writing mode, we are changing which direction is block and which is inline. In a `horizontal-tb` writing mode the block direction runs from top to bottom; in a `vertical-rl` writing mode the block direction runs right-to-left horizontally. So the **block dimension** is always the direction blocks are displayed on the page in the writing mode in use. The **inline dimension** is always the direction a sentence flows.

This figure shows the two dimensions when in a horizontal writing mode.![Showing the block and inline axis for a horizontal writing mode.](horizontal-tb.png)

This figure shows the two dimensions in a vertical writing mode.

![Showing the block and inline axis for a vertical writing mode.](vertical.png)

Once you start to look at CSS layout, and in particular the newer layout methods, this idea of block and inline becomes very important. We will revisit it later on.

### Direction

In addition to writing mode we also have text direction. As mentioned above, some languages such as Arabic are written horizontally, but right-to-left. This is not something you are likely to use in a creative sense — if you want to line something up on the right there are other ways to do so — however it is important to understand this as part of the nature of CSS. The web is not just for languages that are displayed left-to-right!

Due to the fact that writing mode and direction of text can change, newer CSS layout methods do not refer to left and right, and top and bottom. Instead they will talk about _start_ and _end_ along with this idea of inline and block. Don't worry too much about that right now, but keep these ideas in mind as you start to look at layout; you will find it really helpful in your understanding of CSS.

## Logical properties and values

The reason to talk about writing modes and direction at this point in your learning is that we have already looked at a lot of properties that are tied to the physical dimensions of the screen, and these make more sense when in a horizontal writing mode.

Let's take a look at our two boxes again — one with a `horizontal-tb` writing mode and one with `vertical-rl`. I have given both of these boxes a {{cssxref("width")}}. You can see that when the box is in the vertical writing mode, it still has a width, and this is causing the text to overflow.

```html live-sample___width
<div class="wrapper">
  <div class="box horizontal">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have a width.</p>
  </div>
  <div class="box vertical">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have a width.</p>
  </div>
</div>
```

```css live-sample___width
body {
  font-family: sans-serif;
  height: 300px;
}
.wrapper {
  display: flex;
}

.box {
  border: 1px solid #ccc;
  padding: 0.5em;
  margin: 10px;
  width: 100px;
}

.horizontal {
  writing-mode: horizontal-tb;
}

.vertical {
  writing-mode: vertical-rl;
}
```

{{EmbedLiveSample("width", "", "350px")}}

What we really want in this scenario is to essentially swap height with width in accordance to the writing mode. When we're in a vertical writing mode we want the box to expand in the block dimension just like it does in the horizontal mode.

To make this easier, CSS has recently developed a set of mapped properties. These essentially replace physical properties — things like `width` and `height` — with **logical**, or **flow relative** versions.

The property mapped to `width` when in a horizontal writing mode is called {{cssxref("inline-size")}} — it refers to the size in the inline dimension. The property for `height` is named {{cssxref("block-size")}} and is the size in the block dimension. You can see how this works in the example below where we have replaced `width` with `inline-size`.

```html live-sample___inline-size
<div class="wrapper">
  <div class="box horizontal">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have inline-size.</p>
  </div>
  <div class="box vertical">
    <h2>Heading</h2>
    <p>A paragraph demonstrating writing modes in CSS.</p>
    <p>These boxes have inline-size.</p>
  </div>
</div>
```

```css live-sample___inline-size
.wrapper {
  display: flex;
}

.box {
  border: 1px solid #ccc;
  padding: 0.5em;
  margin: 10px;
  inline-size: 100px;
}

.horizontal {
  writing-mode: horizontal-tb;
}

.vertical {
  writing-mode: vertical-rl;
}
```

{{EmbedLiveSample("inline-size", "", "300px")}}

### Logical margin, border, and padding properties

In the last two lessons we have learned about the CSS box model, and CSS borders. In the margin, border, and padding properties you will find many instances of physical properties, for example {{cssxref("margin-top")}}, {{cssxref("padding-left")}}, and {{cssxref("border-bottom")}}. In the same way that we have mappings for width and height there are mappings for these properties.

The `margin-top` property is mapped to {{cssxref("margin-block-start")}} — this will always refer to the margin at the start of the block dimension.

The {{cssxref("padding-left")}} property maps to {{cssxref("padding-inline-start")}}, the padding that is applied to the start of the inline direction. This will be where sentences start in that writing mode. The {{cssxref("border-bottom")}} property maps to {{cssxref("border-block-end")}}, which is the border at the end of the block dimension.

You can see a comparison between physical and logical properties below.

If you change the writing mode of the boxes by switching the `writing-mode` property on `.box` to `vertical-rl`, you will see how the physical properties stay tied to their physical direction, whereas the logical properties switch with the writing mode.

You can also see that the {{htmlelement("Heading_Elements", "h2")}} has a black `border-bottom`. Can you work out how to make that bottom border always go below the text in both writing modes?

```html live-sample___logical-mbp
<div class="wrapper">
  <div class="box physical">
    <h2>Physical Properties</h2>
    <p>A paragraph demonstrating logical properties in CSS.</p>
  </div>
  <div class="box logical">
    <h2>Logical Properties</h2>
    <p>A paragraph demonstrating logical properties in CSS.</p>
  </div>
</div>
```

```css live-sample___logical-mbp
.wrapper {
  display: flex;
  border: 5px solid #ccc;
}

.box {
  margin-right: 30px;
  inline-size: 200px;
  writing-mode: horizontal-tb;
}

.logical {
  margin-block-start: 20px;
  padding-inline-end: 2em;
  padding-block-start: 2px;
  border-block-start: 5px solid pink;
  border-inline-end: 10px dotted rebeccapurple;
  border-block-end: 1em double orange;
  border-inline-start: 1px solid black;
}

.physical {
  margin-top: 20px;
  padding-right: 2em;
  padding-top: 2px;
  border-top: 5px solid pink;
  border-right: 10px dotted rebeccapurple;
  border-bottom: 1em double orange;
  border-left: 1px solid black;
}

h2 {
  border-bottom: 5px solid black;
}
```

{{EmbedLiveSample("logical-mbp", "", "200px")}}

There are a huge number of properties when you consider all of the individual border longhands, and you can see all of the mapped properties on the MDN page for [Logical Properties and Values](/en-US/docs/Web/CSS/CSS_logical_properties_and_values).

### Logical values

We have so far looked at logical property names. There are also some properties that take physical values of `top`, `right`, `bottom`, and `left`. These values also have mappings, to logical values — `block-start`, `inline-end`, `block-end`, and `inline-start`.

For example, you can float an image left to cause text to wrap round the image. You could replace `left` with `inline-start` as shown in the example below.

Change the writing mode on this example to `vertical-rl` to see what happens to the image. Change `inline-start` to `inline-end` to change the float:

```html live-sample___float
<div class="wrapper">
  <div class="box logical">
    <img
      alt="star"
      src="https://mdn.github.io/shared-assets/images/examples/big-star.png" />
    <p>
      This box uses logical properties. The star image has been floated
      inline-start, it also has a margin on the inline-end and block-end.
    </p>
  </div>
</div>
```

```css live-sample___float
.wrapper {
  display: flex;
}

.box {
  margin: 10px;
  padding: 0.5em;
  border: 1px solid #ccc;
  inline-size: 200px;
  writing-mode: horizontal-tb;
}

img {
  float: inline-start;
  margin-inline-end: 10px;
  margin-block-end: 10px;
}
```

{{EmbedLiveSample("float", "", "200px")}}

Here we are also using logical margin values to ensure the margin is in the correct place no matter what the writing mode is.

### Should you use physical or logical properties?

The logical properties and values are newer than their physical equivalents, and therefore have only recently been implemented in browsers. You can check any property page on MDN to see how far back the browser support goes. If you are not using multiple writing modes, then for now you might prefer to use the physical versions. However, ultimately we expect that people will transition to the logical versions for most things, as they make a lot of sense once you also start dealing with layout methods such as flexbox and grid.

## Summary

The concepts explained in this lesson are becoming increasingly important in CSS. An understanding of the block and inline direction — and how text flow changes with a change in writing mode — will be very useful going forward. It will help you in understanding CSS even if you never use a writing mode other than a horizontal one.
