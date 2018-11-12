# Browser에서 Media Query관련 Event를 받는 방법
- [Reference](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia)

## window.matchMedia()

``` JavaScript
if (window.matchMedia("(min-width: 400px)").matches) {
  /* the viewport is at least 400 pixels wide */
} else {
  /* the viewport is less than 400 pixels wide */
}
```
