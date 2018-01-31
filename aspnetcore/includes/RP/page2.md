`<form method="post">` 요소는 [폼 태그 도우미](xref:mvc/views/working-with-forms#the-form-tag-helper)입니다. 폼 태그 도우미에는 [위조 방지 토큰](xref:security/anti-request-forgery)이 자동으로 포함됩니다.

스캐폴딩 엔진은 다음과 비슷한 모델에서 각 필드(ID 제외)에 대한 Razor 태그를 만듭니다.

[!code-cshtml[Main](../../tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml?range=15-20)]

[유효성 검사 태그 도우미](xref:mvc/views/working-with-forms#the-validation-tag-helpers)(`<div asp-validation-summary` 및 ` <span asp-validation-for`)는 유효성 검사 오류를 표시합니다. 유효성 검사는 이 시리즈의 뒷부분에서 자세히 설명합니다.

[레이블 태그 도우미](xref:mvc/views/working-with-forms#the-label-tag-helper)(`<label asp-for="Movie.Title" class="control-label"></label>`)는 `Title` 속성에 대한 레이블 캡션 및 `for` 특성을 생성합니다.

[입력 태그 도우미](xref:mvc/views/working-with-forms)(`<input asp-for="Movie.Title" class="form-control" />`)는 [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 특성을 사용하고 클라이언트 쪽의 jQuery 유효성 검사에 필요한 HTML 특성을 생성합니다.