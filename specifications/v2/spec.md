# V2 Spec (Cascading Reaction Sheets)

## Syntax
SELECTOR {
    PROPERTY_NAME: PROPERTY_VALUE;
}

The three primary entities are SELECTOR, PROPERTY_NAME, PROPERTY_VALUE; all of these are detailed below.
Additional syntax includes:
1. CSS-like block, represented with braces `{}`
2. A property colon `:`, which associates the previous PROPERTY_NAME with the following PROPERTY_VALUE in a 1:1 relationship
3. A semicolon `;`, designating a statement termination

## SELECTOR
    All selectors adhere to CSS selector specification.

## PROPERTY_NAME
Can be one of:
1. HTML Attribute
2. `content`
3. JS Event Listener

### HTML Attribute - is the same as CSS properties. E.g.
```scss
input {
    required: "";
    class: "red-text thick-border";
}
```
The above code will add the [required=""] and [class="red-text thick-border"] attributes to all input elements.

### `content` - is the same as the CSS content property. It functions similar to CSS content property as well. E.g.
```scss
span.greeting {
    content: "Hey there!";
}
```
The above code will set `textContent` of all span.greeting elements to `Hey there!`

### JS Event Listener - uses parenthesis to differentiate itself from the previous two property types. E.g.
```scss
form {
    (submit): $onSubmitHandler, $logSubmitEvent;
}
```
The above code will add two event listeners to all forms: the `onSubmitHandler` function and `logSubmitEvent`, both variables defined in JS code.
Prefixing an event listener variable with a `!` will remove that particular event listener. E.g.
```scss
form[do-not-log] {
    (submit): $onSubmitHandler, !$logSubmitEvent;
}
```
The above code will select all form[do-not-log] elements and add the `onSubmitHandler` listener and remove the `logSubmitEvent` listener, if it exists.

## PROPERTY_VALUE
Can be one of these value types:
1. String, represented with ' or " chars
2. `none`, the removal of the property
3. A variable, prefixed with `$` and defined in JS runtime

### Strings - e.g.
```scss
input {
    required: "";
    title: "Please fill out this field";
}
```
The example above will add two attributes to all inputs: [required=""] and [title="Please fill out this field"]

### `none` - this value literal will remove the property. e.g.
```scss
form {
    class: none;
    disabled: none;
    (submit): none;
}
```
The above code will select all forms and remove the [class] and [disabled] attributes as well as remove all `submit` event listeners.

### Variables - these function similarly to CSS variables, but should only be defined in JS runtime E.g.
```scss
form {
    (submit): $onSubmitHandler, $logSubmitEvent;
}
```
```js
document.body.reactions.setProperty('onSubmitHandler', e => { /* handler code block */ })
document.body.reactions.setProperty('logSubmitEvent', e => { /* handler code block */ })
```
The above CRS code will add two (submit) event listeners to all form elements.
The above JS code will register two CRS variables, which are used in the corresponding CRS.

All CWR variables are prefixed with the `$` character.
Variables, like CSS custom properties are defined at runtime using JavaScript: document.body.reactions.setProperty(`variableName`, JSVARIABLE)