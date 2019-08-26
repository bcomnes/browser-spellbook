# Forms

- https://webreflection.github.io/dm/


## Form values

```js
function getFormValues (formEl) {
  return Array.from(new window.FormData(formEl).entries())
    .reduce(function (obj, [key, value]) {
      obj[key] = value
      return obj
    }, {})
}
```

A form element has accessors for input values by `name` on it magically too.  
