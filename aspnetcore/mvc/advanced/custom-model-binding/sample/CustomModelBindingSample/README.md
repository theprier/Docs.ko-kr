# <a name="custom-model-binding-demo"></a>사용자 지정 모델 바인딩 데모

응용 프로그램을 실행하고 base64 인코딩된 문자열을 ImageController 끝점(/api/image/)에 게시하여 `ByteArrayModelBinder`를 테스트할 수 있습니다. 요청 본문에 파일 및 파일 이름 특징을 양식 데이터로 지정해야 합니다(Postman 또는 유사한 도구 사용). [이 샘플 문자열](Base64String.txt)을 사용할 수 있습니다. 결과는 지정한 파일 이름으로 wwwroot/images/upload 폴더에 저장됩니다.

사용자 지정 바인딩 샘플을 테스트하려면 /api/authors/1 /api/authors/2 (NOT FOUND) /api/boundauthors/1 /api/boundauthors/2 (NOT FOUND) /api/boundauthors/get/1 /api/boundauthors/get/2 (NO CONTENT)의 끝점을 사용합니다. 이 작업은 null을 검사하지 않고 찾을 수 없음을 반환하지 않습니다.
