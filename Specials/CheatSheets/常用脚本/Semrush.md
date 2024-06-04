- 抓取 Semrush 中的排行数据

```js
JSON.stringify(
  Array.from(document.querySelectorAll(".sm-group-item__content")).map(($e) => {
    return {
      name: $e.querySelector(".sm-group-item__text").innerText,
      number: $e.querySelector(".sm-group-item__number").innerText,
    };
  })
);
```
