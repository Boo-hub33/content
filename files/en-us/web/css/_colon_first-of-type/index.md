---
title: :first-of-type
slug: Web/CSS/:first-of-type
page-type: css-pseudo-class
browser-compat: css.selectors.first-of-type
sidebar: cssref
---

The **`:first-of-type`** [CSS](/en-US/docs/Web/CSS) [pseudo-class](/en-US/docs/Web/CSS/Pseudo-classes) represents the first element of its type (tag name) among a group of sibling elements.

{{InteractiveExample("CSS Demo: :first-of-type", "tabbed-shorter")}}

```css interactive-example
dt {
  font-weight: bold;
}

dd {
  margin: 3px;
}

dd:first-of-type {
  border: 2px solid orange;
}
```

```html interactive-example
<dl>
  <dt>Vegetables:</dt>
  <dd>1. Tomatoes</dd>
  <dd>2. Cucumbers</dd>
  <dd>3. Mushrooms</dd>
  <dt>Fruits:</dt>
  <dd>4. Apples</dd>
  <dd>5. Mangos</dd>
  <dd>6. Pears</dd>
  <dd>7. Oranges</dd>
</dl>
```

## Syntax

```css
:first-of-type {
  /* ... */
}
```

## Examples

### Styling the first paragraph

#### HTML

```html
<h2>Heading</h2>
<p>Paragraph 1</p>
<p>Paragraph 2</p>
```

#### CSS

```css
p:first-of-type {
  color: red;
  font-style: italic;
}
```

#### Result

{{EmbedLiveSample('Styling_the_first_paragraph')}}

### Nested elements

This example shows how nested elements can also be targeted. Note that the [universal selector](/en-US/docs/Web/CSS/Universal_selectors) (`*`) is implied when no type selector is written.

#### HTML

```html
<article>
  <div>This `div` is first!</div>
  <div>This <span>nested `span` is first</span>!</div>
  <div>
    This <em>nested `em` is first</em>, but this <em>nested `em` is last</em>!
  </div>
  <div>This <span>nested `span` gets styled</span>!</div>
  <p>This `p` qualifies!</p>
  <div>This is the final `div`.</div>
</article>
```

#### CSS

```css
article :first-of-type {
  background-color: pink;
}
```

#### Result

{{EmbedLiveSample('Nested_elements', 500)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{Cssxref(":first-child")}}, {{Cssxref(":last-of-type")}}, {{Cssxref(":nth-of-type")}}
