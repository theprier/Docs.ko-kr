# <a name="update-the-generated-pages"></a>생성된 페이지 업데이트

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다. 시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 **Release Date**(두 단어)이어야 합니다.

![동영상 데이터를 표시하는 크롬에서 열린 동영상 응용 프로그램](../../tutorials/razor-pages/sql/_static/m55.png)

## <a name="update-the-generated-code"></a>생성된 코드 업데이트

*Models/Movie.cs* 파일을 열고 다음 코드에 표시된 강조 표시된 줄을 추가합니다.

[!code-csharp[](code/Models/Movie.cs?highlight=2,11-12)]
