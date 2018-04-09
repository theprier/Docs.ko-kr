# <a name="aspnet-core-authorization-sample"></a>ASP.NET Core 권한 부여 샘플

이 샘플 규칙에 의해 Razor 페이지 권한 부여 사용을 보여 줍니다. 이 샘플에서 설명 하는 기능을 보여 줍니다.는 [Razor 페이지 권한 부여 규칙](https://docs.microsoft.com/aspnet/core/security/authorization/razor-pages-authorization) 항목입니다.

이 샘플의 사용자 권한 부여 기능에 설명 하는 쿠키 인증을 사용 하는 [ASP.NET Core Id 없이 사용 하 여 쿠키 인증](https://docs.microsoft.com/aspnet/core/security/authentication/cookie) 항목입니다. ASP.NET Core Id를 사용 하는 방법은 항목을 참조는 [인증](https://docs.microsoft.com/aspnet/core/security/authentication/index) 설명서의 섹션입니다.

이 샘플을 실행 하는 경우 전자 메일 주소를 사용 하 여 **maria.rodriguez@contoso.com** 사용자를 인증할 수 있습니다.

## <a name="examples-in-this-sample"></a>이 샘플의 예제

|                                                                              기능                                                                               |                                                                                        설명                                                                                         |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          [AuthorizePage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)          |                추가 [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정된 된 경로와 페이지에 있습니다.                |
|        [AuthorizeFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder)        |      추가 [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 모든 지정된 된 경로와 같은 폴더에 대 한 페이지에 있습니다.      |
|   [AllowAnonymousToPage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage)   |            추가 [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로와 페이지에 있습니다.            |
| [AllowAnonymousToFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) | 추가 [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 모든 지정된 된 경로와 같은 폴더에 대 한 페이지에 있습니다. |

