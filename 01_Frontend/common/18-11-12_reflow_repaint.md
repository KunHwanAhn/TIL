# About Repaint and Reflow on browsers
- [Reference](https://github.com/nhnent/fe.javascript/wiki/Reflow%EC%99%80-Repaint)
- [CSS Triggers](https://csstriggers.com/)

## 개요
본 문서는 DOM의 변화로 인해 발생하는 Reflow와 Repaint에 대한 문서이다.

## Reflow & Repaint

### Reflow
`렌더트리가 배치`되는 과정으로 렌더러가 생성되어 렌더트리에 추가될 때 할당되지 않았던 정보(크기, 위치 등)를 계산한다.

### Repaint
렌더러의 시각적 요소(visibility, outline, background-color 등)가 표현되는 과정으로 렌더러의 "paint" 메서드가 호출된다.

> 배경색  =>  배경이미지  =>  테두리  =>  자식  =>  아웃라인
