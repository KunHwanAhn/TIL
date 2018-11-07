# The Difference Between Width and Flex Basis
- [Reference](https://gedd.ski/post/the-difference-between-width-and-flex-basis/)

> 아래 예제들은 flex-direction: row;를 기준으로 작성했습니다.

## 개요
본 문서는 Flexbox를 사용하면서 `flex-basis`, `width`, `min-width`, `max-width` 등 너비 및 높이와 관련된 속성들에 대해서 정리하는 문서이다.

## Flex Items Formula
content -> width -> flex-basis (Limited by max-width or min-width)

### flex-basis가 정의되어 있지 않은 경우
`width` 속성을 Fall back으로 사용한다.

### width가 정의되어 있지 않은 경우
대상 아이템의 계산된 width를 Fall back으로 사용한다.

#### Example 1

``` CSS
container {
  display: flex;
  width: 1000px;
}

item {
  width: 200px;
  height: 200px;
}
```

위 예제에서는 `flex-basis`를 정의하지 않았기 때문에, `flex-basis: auto`로 설정되며, width를 Fall back으로 사용하기에, 200px로 설정된다.

#### Example 2

``` CSS
container {
  display: flex;
  width: 1000px;
}

item {
  width: 30px;
  flex-basis: 250px;
}
```
위 예제에서는 `flex-basis`를 정의했기 때문에, `width`를 정의했음에도 불구하고 무시하고 250px로 설정된다.

### flex-basis with max-width
flex-basis와 `max-width`를 같이 사용할 경우, flex-basis의 값을 max-width보다 크게 잡아도 max-width에 의해서 너비가 제한 된다.

#### Example 3

``` CSS
container {
  display: flex;
  width: 1000px;
}

item {
  max-width: 100px;
  flex-basis: 250px;
}
```

### flex-basis with min-width
flex-basis와 `min-width`를 같이 사용할 경우, flex-basis의 값을 min-width보다 작게 잡아도 min-width에 의해서 너비가 flex-basis에서 설정한 값보다 크게 된다.

#### Example 4

``` CSS
container {
  display: flex;
  width: 1000px;
}

item {
  min-width: 200px;
  flex-basis: 100px;
}
```

## So What Exactly is the flex-basis?
flex-basis는 flex Item들이 flex container에 배치 되기 전의 크기를 지정하는 것이다. 하지만, `flex-basis`는 **지정한 크기를 보장하지 않는다**.
하지만, 항상 flex-basis에서 지정한 크기를 보장할 수 있는 Container가 있는 경우는 드물다. 따라서, 이후 부터는 해당하는 경우에 대해서 설명한다.

## When Not Enough Space
`flex-basis: 200px`을 설정하고, Item의 갯수가 8개인 경우

### Example 5

``` CSS
container {
  display: flex;
  width: 1000px;
}

item {
  flex-basis: 200px;
}
```

너비를 200px로 설정했음에도 불구하고 Container 안에 Item들이 많아, 너비가 모두 `125px`로 **줄어서** 배치됐다.

## When Extra Space Available

### Example 6
`flex-basis: 100px; flex-grow: 1;`을 설정하고, Item의 갯수가 4개인 경우

``` CSS
container {
  display: flex;
  width: 1000px;
}

item {
  flex-basis: 100px;
  flex-grow: 1;
}
```

너비를 100px로 설정했음에도 불구하고, Container 안에 Item의 기본 너비로는 Container를 다채우지 못한다. 하지만 `flex-grow`에 의해서 Item들의 너비가 `250px`로 **늘어나서** 배치됐다.

## 정리하며...
이처럼 flex-basis는 width와 밀접하게 동작하기에, 사용할 때도 이러한 점을 생각하고 사용해야 한다. Flexbox는 매우 강력한 기능이면서, `잘` 사용하기도 그만큼 까다로우니, 잘 이해하고 사용하는 것이 중요하다.

현재는 flex-direction이 `row` 였기에 `width`로 설명했지만, `column`일 경우 `height`도 동일하게 적용된다.
