---
title: "HTML attribute: step"
short-title: step
slug: Web/HTML/Reference/Attributes/step
page-type: html-attribute
browser-compat: html.elements.input.step
sidebar: htmlsidebar
---

The **`step`** attribute is a number that specifies the granularity that the value must adhere to or the keyword `any`. It is valid for the numeric input types, including the {{HTMLElement("input/date", "date")}}, {{HTMLElement("input/month", "month")}}, {{HTMLElement("input/week", "week")}}, {{HTMLElement("input/time", "time")}}, {{HTMLElement("input/datetime-local", "datetime-local")}}, {{HTMLElement("input/number", "number")}} and {{HTMLElement("input/range", "range")}} types.

The `step` sets the _stepping interval_ when clicking up and down spinner buttons, moving a slider left and right on a range, and validating the different date types. If not explicitly included, `step` defaults to 1 for `number` and `range`, and 1 unit type (minute, week, month, day) for the date/time input types. The value must be a positive number - integer or float — or the special value `any`, which means no stepping is implied and any value is allowed (barring other constraints, such as [`min`](/en-US/docs/Web/HTML/Reference/Attributes/min) and [`max`](/en-US/docs/Web/HTML/Reference/Attributes/max)).

Only values which are a whole number of steps from the step base are valid. The step base is [`min`](/en-US/docs/Web/HTML/Reference/Attributes/min) if specified, [`value`](/en-US/docs/Web/HTML/Reference/Elements/input#value) otherwise, or `0` if neither is provided (except for `week`, which has a default step base of −259,200,000, representing the start of week `1970-W01`).

## Syntax

<table class="no-markdown">
  <caption>
    Default values for step
  </caption>
  <thead>
    <tr>
      <th>Input type</th>
      <th>Value</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>{{HTMLElement("input/date", "date")}}</td>
      <td>1 (day)</td>
      <td><code>&#x3C;input type="date" min="2019-12-25" step="1"></code></td>
    </tr>
    <tr>
      <td>{{HTMLElement("input/month", "month")}}</td>
      <td>1 (month)</td>
      <td><code>&#x3C;input type="month" min="2019-12" step="12"></code></td>
    </tr>
    <tr>
      <td>{{HTMLElement("input/week", "week")}}</td>
      <td>1 (week)</td>
      <td><code>&#x3C;input type="week" min="2019-W23" step="2"></code></td>
    </tr>
    <tr>
      <td>{{HTMLElement("input/time", "time")}}</td>
      <td>60 (seconds)</td>
      <td><code>&#x3C;input type="time" min="09:00" step="900"></code></td>
    </tr>
    <tr>
      <td>
        {{HTMLElement("input/datetime-local", "datetime-local")}}
      </td>
      <td>60 (seconds)</td>
      <td>
        <code
          >&#x3C;input type="datetime-local" min="2019-12-25T19:30"
          step="900"></code
        >
      </td>
    </tr>
    <tr>
      <td>{{HTMLElement("input/number", "number")}}</td>
      <td>1</td>
      <td>
        <code>&#x3C;input type="number" min="0" step="0.1" max="10"></code>
      </td>
    </tr>
    <tr>
      <td>{{HTMLElement("input/range", "range")}}</td>
      <td>1</td>
      <td><code>&#x3C;input type="range" min="0" step="2" max="10"></code></td>
    </tr>
  </tbody>
</table>

If `any` is not explicitly set, valid values for the `number`, date/time input types, and `range` input types are equal to the basis for stepping - the [`min`](/en-US/docs/Web/HTML/Reference/Attributes/min) value and increments of the step value, up to the [`max`](/en-US/docs/Web/HTML/Reference/Attributes/max) value, if specified. The following example results in any even integer, 10 or greater, being valid:

```html
<input type="number" min="10" step="2" />
```

If `step` is omitted, any integer is valid but floats like 4.2 are not valid as `step` defaults to 1. For 4.2 to be valid:

- either `step` would have to be set to `any`, 0.1, or 0.2,
- or the `min` value would have to be a number ending in .2, such as 0.2, 1.2, or -5.2.

## Examples

### `min` impact on step

The value of `min` defines valid values, even if the `step` attribute is not included. This is because `step` defaults to `1` for the `number` input type.

In this example, we add a big red border around invalid inputs:

```css
input:invalid {
  border: solid red 3px;
}
```

We then define an input with a minimum value of 1.2 and a step value of 2:

```html
<input id="myNumber" name="myNumber" type="number" step="2" min="1.2" />
```

Valid values include 1.2, 3.2, 5.2, 7.2, 9.2, 11.2, and so on. Only floats with an odd-numbered integer part and a decimal part of .2 are valid. The number spinner, if present, generates valid float values of 1.2 and greater, in increments of 2.

{{EmbedLiveSample("min_impact_on_step","100%",55)}}

> [!NOTE]
> When the data entered by the user doesn't adhere to the stepping configuration, the value is considered invalid in constraint validation and will match the {{cssxref(":invalid")}} and {{cssxref(":out-of-range")}} pseudoclasses.

See [Client-side validation](/en-US/docs/Web/HTML/Guides/Constraint_validation) and {{domxref("ValidityState.stepMismatch", "stepMismatch")}} for more information.

## Accessibility concerns

Provide instructions to help users understand how to complete the form and use individual form controls. Indicate any required and optional input, data formats, and other relevant information. When using the `min` attribute, ensure this minimum requirement is understood by the user. Providing instructions within the {{htmlelement('label')}} may be sufficient. If providing instructions outside of labels, which allows more flexible positioning and design, consider using [`aria-labelledby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby) or [`aria-describedby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-describedby).

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [`max`](/en-US/docs/Web/HTML/Reference/Attributes/max)
- [`min`](/en-US/docs/Web/HTML/Reference/Attributes/min)
- [Constraint validation](/en-US/docs/Web/HTML/Guides/Constraint_validation)
- [Form validation](/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation)
- {{domxref('validityState.stepMismatch')}}
- {{cssxref(':out-of-range')}}
- {{htmlelement('input')}}
- {{HTMLElement("input/date", "date")}}, {{HTMLElement("input/month", "month")}}, {{HTMLElement("input/week", "week")}}, {{HTMLElement("input/time", "time")}}, {{HTMLElement("input/datetime-local", "datetime-local")}}, {{HTMLElement("input/number", "number")}} and {{HTMLElement("input/range", "range")}} types, and the {{htmlelement('meter')}}
