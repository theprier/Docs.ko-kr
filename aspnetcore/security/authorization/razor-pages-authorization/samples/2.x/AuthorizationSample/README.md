# <a name="aspnet-core-authorization-sample"></a>ASP.NET Core 권한 부여 샘플

이 샘플에서는 규칙으로 사용 하 여를 Razor 페이지 권한 부여를 보여 줍니다. 이 샘플에 설명 된 기능을 보여 줍니다.는 [Razor 페이지 권한 부여 규칙](https://docs.microsoft.com/aspnet/core/security/authorization/razor-pages-authorization) 항목입니다.

이 샘플에서 사용자 권한 부여 기능에 설명 하는 쿠키 인증을 사용 하 여 [ASP.NET Core Id 없이 쿠키 인증 사용](https://docs.microsoft.com/aspnet/core/security/authentication/cookie) 항목입니다. 개념 및이 항목에 표시 하는 예제 ASP.NET Core Id를 사용 하는 앱에 동일 하 게 적용 됩니다. ASP.NET Core Id를 사용 하 여 정보를 참조 하세요 [ASP.NET core Id 소개](https://docs.microsoft.com/aspnet/core/security/authentication/identity)합니다.

전자 메일 주소를 사용 하 여 **maria.rodriguez@contoso.com** 모든 암호를 사용 하 여 사용자를 인증 합니다. 사용자가 인증을 `AuthenticateUser` 의 메서드를 *Pages/Account/Login.cshtml.cs* 파일입니다. 실제 예제에서는 데이터베이스에 대해 사용자를 인증 됩니다.

## <a name="examples-in-this-sample"></a>이 샘플의 예제

| 기능 | 설명 |
| --- | --- |
| [AuthorizePage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) | 추가 [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 페이지에 지정된 된 경로입니다. |
| [AuthorizeFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) | 추가 [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 모든 지정된 된 경로 사용 하 여 폴더의 페이지에 있습니다. |
| [AllowAnonymousToPage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) | 추가 [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로 사용 하 여 페이지에 있습니다. |
| [AllowAnonymousToFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) | 추가 [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 모든 지정된 된 경로 사용 하 여 폴더의 페이지에 있습니다. |
