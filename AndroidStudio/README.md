- 루트의 `build.gradle`이 안 보인다 : 일단 빌드가 제대로 되는지 확인한 후 AS를 끈다. 그리고 프로젝트 루트 폴더에서 `.idea` 폴더를 지운 후 다시 시작한다.

---

- (Windows 기준) `Ctrl` + `Q`를 눌렀을 때, 문서가 빨리 빨리 뜨지 않는다(캐시를 하고 싶다) : 

  `C:\Users\[사용자 이름]\.AndroidStudio3.0\config\options\jdk.table.xml`을 찾아 연다.

  ```xml
  <root type="simple" url="http://developer.android.com/reference/" />
  ```

  를

  ```xml
  <root type="simple" url="file://C:/Android/sdk/docs/reference" />
  ```

  로 바꾼다.

  AS에서 `File` -> `Invalidate Caches / Restart...` 클릭한다.