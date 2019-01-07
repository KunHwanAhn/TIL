# About Multipart Upload
- [Reference](https://ec.haxx.se/http-multipart.html)
- [MDN / FormData](https://developer.mozilla.org/ko/docs/Web/API/FormData)
- [MDN / Using FormData Objects](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)

## 개요
본 문서는 Form에서 Multipart Data로 Upload하는 방법에 대한 문서이다.

## Form with multipart/form-data

### Using HTML attribute

``` HTML
<form action="submit.cgi" method="post" enctype="multipart/form-data">
  Name: <input type="text" name="person"><br>
  File: <input type="file" name="secret"><br>
  <input type="submit" value="Submit">
</form>
```

### Using JavaScript Object

``` JavaScript
var formData = new FormData();

formData.append("username", "Groucho");
formData.append("accountnum", 123456); // number 123456 is immediately converted to a string "123456"

// HTML file input, chosen by user
formData.append("userfile", fileInputElement.files[0]);
```

> File Object 추가 시, FormData.append(name, value, filename) 마지막 Parameter인 filename을 넣을 경우 해당 File Object가 추가되지 않는 문제가 있음. 추 후에 확인 필요
