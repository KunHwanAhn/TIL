# About Open Graph Protocol
- [opg.me](http://ogp.me/)
- [Reference](https://medium.com/@pks2974/%EC%9B%B9%EC%82%AC%EC%9D%B4%ED%8A%B8-%EB%A7%81%ED%81%AC-%ED%94%84%EB%A6%AC%EB%B7%B0-open-graph-protocol-41a0ee40f6d)

## 개요
본 문서는 Open Graph Protocol에 대한 내용을 정리한 문서이다.

## 링크 미리보기?
페이스북, 트위터 등에서 링크를 공유하면 나오는 이미지와 텍스트 등을 함께 표현하여, 사용자가 조금 더 쉽게 정보를 알 수 있게 도와주고, 사이트 접근성을 쉽게 해주는 것

## Open Graph Protocol
- 페이스북에서 최초로 정의한 메타 태그 규약

## Metadata
- HTML의 <head> 영역에 추가하여 원하는 Metadata를 정의할 수 있다.
- `og:title`: 전달할 제목
- `og:type`: 전달할 데이터의 타입, e.g. video, image website etc..
- `og:image`: 전달할 이미지의 URI
- `og:url`: 전달할 사이트 주소

``` HTML
<head>
 <meta property=”og:title” content=”제목” />
 <meta property=”og:type” content=”website” />
 <meta property=”og:image” content=”http://이미지.jpg" />
 <meta property=”og:url” content=”http://주소" />
</head>
```

## How to test?
[Facebook 개발자 도구](https://developers.facebook.com/tools/debug/)

## 사용 시 이점
- 링크 프리뷰에 알맞는 이미지와 제목을 부여해, 사용자에게 호기심을 유발하여 접속률을 높일 수 있다.
- 링크가 복잡하더라도, 이미지와 제목을 사용해서 사용자에게 정확한 정보를 전달할 수 있다.

## 사용 시 주의점
- 공식으로 HTML에서 지원하는 기능이 아니기에, 기능을 지원하는 업체별로 조금씩 다를 수 있다.
