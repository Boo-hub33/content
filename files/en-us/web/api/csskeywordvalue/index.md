---
title: CSSKeywordValue
slug: Web/API/CSSKeywordValue
page-type: web-api-interface
browser-compat: api.CSSKeywordValue
---

{{APIRef("CSS Typed Object Model API")}}

The **`CSSKeywordValue`** interface of the [CSS Typed Object Model API](/en-US/docs/Web/API/CSS_Object_Model#css_typed_object_model) creates an object to represent CSS keywords and other identifiers.

The interface instance name is a {{Glossary("stringifier")}} meaning that when used anywhere a string is expected it will return the value of `CSSKeyword.value`.

{{InheritanceDiagram}}

## Constructor

- {{domxref("CSSKeywordValue.CSSKeywordValue", "CSSKeywordValue()")}}
  - : Creates a new `CSSKeywordValue` object.

## Instance properties

- {{domxref('CSSKeywordValue.value')}}
  - : Returns or sets the value of the `CSSKeywordValue`.

## Instance methods

_Inherits methods from {{domxref('CSSStyleValue')}}._

## Examples

The following example resets the CSS {{cssxref('display')}} property to its defaults, setting the inline [`style`](/en-US/docs/Web/HTML/Reference/Global_attributes/style) attribute to `style="display: initial"` if viewed in the [developer tools inspector](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/select_an_element/index.html).

```css hidden
#myElement {
  display: flex;
}
```

```html hidden
<div id="myElement">
  Check the developer tools to see the log in the console and to inspect the
  style attribute on this div.
</div>
```

```js
let myElement = document.getElementById("myElement").attributeStyleMap;
myElement.set("display", new CSSKeywordValue("initial"));

console.log(myElement.get("display").value); // 'initial'
```

{{EmbedLiveSample("Examples", 120, 120)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref('CSSImageValue')}}
- {{domxref('CSSNumericValue')}}
- {{domxref('CSSPositionValue')}}
- {{domxref('CSSTransformValue')}}
- {{domxref('CSSUnparsedValue')}}
