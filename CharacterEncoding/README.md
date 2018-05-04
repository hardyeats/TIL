## 바이트 순서 표식(Byte Order Mark, BOM)

텍스트 스트림의 시작에 BOM이 있다면 다음을 알 수 있다!

- 텍스트 스트림이 유니코드라는 사실
- 텍스트 스트림이 저장되는 바이트 순서(엔디언)



## CSV파일을 윈도우즈 엑셀에서 잘 열수 있게 만드는 방법

```javascript
function exportCsvFileFromJson(headers, items, fileTitle) {

    if (headers) {
        items.unshift(headers);
    }

    // Convert Object to JSON
    var jsonObject = JSON.stringify(items);

    var csv = this.convertToCsv(jsonObject);

    var exportedFileName = fileTitle + '.csv' || 'export.csv';
    console.log("[exportCSVFile] exportedFileName :");
    console.log(exportedFileName);

    var blob = new Blob(["\ufeff", csv], { type: 'text/csv;charset=utf-8;' });
    console.log(blob);
    if (navigator.msSaveBlob) { // IE 10+
        navigator.msSaveBlob(blob, exportedFileName);
    } else {
        var link = document.createElement("a");
        if (link.download !== undefined) { // feature detection
            // Browsers that support HTML5 download attribute
            var url = URL.createObjectURL(blob);
            console.log("[exportCSVFile] url :");
            console.log(url);
            link.setAttribute("href", url);
            link.setAttribute("download", exportedFileName);
            link.style.visibility = 'hidden';
            console.log("[exportCSVFile] link :");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }
    }
}
```

`"\ufeff"`이라는 UTF-8 BOM을 삽입하여, 오피스 프로그램이 디코딩 방식을 스스로 바꾸게 만든다.



## 참고

[위키문서 : 바이트 순서 표식](https://ko.wikipedia.org/wiki/%EB%B0%94%EC%9D%B4%ED%8A%B8_%EC%88%9C%EC%84%9C_%ED%91%9C%EC%8B%9D)