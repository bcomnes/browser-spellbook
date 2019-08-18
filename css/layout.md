# CSS laout

https://cssdb.org

## Flexbox

- https://css-tricks.com/snippets/css/a-guide-to-flexbox/

# CSS Grid

- https://codeburst.io/css-grid-crash-course-9b13dfaaa43a
- https://css-tricks.com/snippets/css/complete-guide-grid/


## Mobile

- https://webkit.org/blog/7929/designing-websites-for-iphone-x/

## CSS Columns

- [Guide to Responsive-Friendly CSS Columns](https://css-tricks.com/guide-responsive-friendly-css-columns/)


```css
/* absolute column count */
article {
  column-count: 2;
}
```

```css
/* minimum width column count */
article {
  column-width: 150px;
}
```

```css
/* both */
article {
  columns: 2 200px;
}

/* or */

article {
  column-count: 2;
  column-width: 200px;
}
```


```css
/* column gap */
article {
  -webkit-columns: 2 200px;
     -moz-columns: 2 200px;
          columns: 2 200px;
  -webkit-column-gap: 4em;
     -moz-column-gap: 4em;
          column-gap: 4em;
}
```

```css
/* column rule */
article {
  -webkit-columns: 2 200px;
     -moz-columns: 2 200px;
          columns: 2 200px;
  -webkit-column-gap: 4em;
     -moz-column-gap: 4em;
          column-gap: 4em;
  -webkit-column-rule: 1px dotted #ddd;
     -moz-column-rule: 1px dotted #ddd;
          column-rule: 1px dotted #ddd;
}
```

```css
/* column span */
h3 {
  -webkit-column-span: all;
          column-span: all;
}
```

```css
/* column fill */
article {
  -webkit-columns: 2 200px;
     -moz-columns: 2 200px;
          columns: 2 200px;
  -moz-column-fill: auto;
       column-fill: auto;
  height: 350px;
}
```


## Line clamp

https://css-tricks.com/almanac/properties/l/line-clamp/
