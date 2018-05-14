# <a name="custom-model-binding-demo"></a>사용자 지정 모델 바인딩 데모

앱을 실행하고 base64로 인코딩된 문자열을 `ImageController` 엔드포인트(`/api/image/`)에 게시하여 `ByteArrayModelBinder`를 테스트합니다. 요청 본문에 파일 및 파일 이름 속성을 양식 데이터로 지정합니다([Postman](https://www.getpostman.com/) 또는 유사한 도구 사용). [이 샘플 문자열](Base64String.txt)을 사용할 수 있습니다. 결과는 지정된 파일 이름으로 *wwwroot/images/upload* 폴더에 저장됩니다.

사용자 지정 바인딩 예제를 테스트하려면 다음 엔드포인트를 사용합니다.

* /api/authors/1
* /api/authors/2(찾을 수 없음)
* /api/boundauthors/1
* /api/boundauthors/2(찾을 수 없음)
* /api/boundauthors/get/1
* /api/boundauthors/get/2(콘텐츠 없음) &ndash; 이 작업은 null을 검사하지 않고 *404 찾을 수 없음*을 반환합니다.
