---
title: "ASP.NET Core에서 정적 파일로 작업"
author: rick-anderson
description: "처리 하 고 정적 파일을 보호 하 고 정적 파일 미들웨어 동작 ASP.NET Core 웹 앱에서 호스트를 구성 하는 방법을 알아봅니다."
keywords: "ASP.NET Core, 정적 파일, 정적 자산, HTML, CSS, JavaScript"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/18/2018
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/static-files
ms.openlocfilehash: 912923860939a1d1dd91ccc79862e23f9095d161
ms.sourcegitcommit: a3e88639a6bcf8fb4d634036dac93130c464a097
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="work-with-static-files-in-aspnet-core"></a>ASP.NET Core에서 정적 파일로 작업

여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Scott Addie](https://twitter.com/Scott_Addie)

HTML, CSS, JavaScript 및 이미지와 같은 정적 파일은 자산 클라이언트에 직접 ASP.NET Core 응용 프로그램을 제공 합니다. 일부 구성은 이러한 파일의 처리를 사용 하도록 설정 하는 데 필요 합니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="serve-static-files"></a>정적 파일을 제공

정적 파일은 프로젝트의 웹 루트 디렉터리 안에 저장 됩니다. 기본 디렉터리는  *\<content_root > / wwwroot*을 통해 변경할 수 있습니다 하지만 [UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) 메서드. 참조 [콘텐츠 루트](xref:fundamentals/index#content-root) 및 [웹 루트](xref:fundamentals/index#web-root) 자세한 정보에 대 한 합니다.

응용 프로그램의 웹 호스트 콘텐츠 루트 디렉터리의 인식 수 있어야 합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

`WebHost.CreateDefaultBuilder` 메서드 콘텐츠 루트를 현재 디렉터리로 설정 합니다.

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

호출 하 여 콘텐츠 루트 현재 디렉터리로 설정 [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) 내부에 `Program.Main`:

[!code-csharp[](static-files/samples/1x/Program.cs?name=snippet_ProgramClass&highlight=7)]

---

정적 파일은 웹 루트에 상대적인 경로 통해 액세스할 수 있습니다. 예를 들어는 **웹 응용 프로그램** 내에서 여러 폴더를 포함 하는 프로젝트 템플릿에 *wwwroot* 폴더:

* **wwwroot**
  * **css**
  * **images**
  * **js**

파일에 액세스 하려면 URI 형식이 고 *이미지* 하위 폴더는 *http://\<server_address > /images/\<image_file_name >*합니다. 예를 들어 *http://localhost:9189/images/banner3.svg*합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

.NET Framework를 대상으로 하는 경우 추가 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) 프로젝트에 패키지 합니다. .NET Core를 대상으로 하는 경우는 [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) 이 패키지를 포함 합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

추가 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) 프로젝트에 패키지 합니다.

---

구성에서 [미들웨어](xref:fundamentals/middleware) 정적 파일 처리 할 수 있게 합니다.

### <a name="serve-files-inside-of-web-root"></a>웹 루트 내부에서 파일을 제공 합니다

호출 된 [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 메서드 내에서 `Startup.Configure`:

[!code-csharp[](static-files/samples/1x/StartupStaticFiles.cs?name=snippet_ConfigureMethod&highlight=3)]

매개 변수가 없는 `UseStaticFiles` 메서드 오버 로드로 servable 웹 루트에 있는 파일을 표시 합니다. 다음 태그 참조 *wwwroot/images/banner1.svg*:

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_wwwroot)]

### <a name="serve-files-outside-of-web-root"></a>웹 루트 외부 파일을 제공 합니다

서비스할 수 정적 파일 외부에 있는 웹 루트 디렉터리 계층 구조를 고려해 야 합니다.

* **wwwroot**
  * **css**
  * **images**
  * **js**
* **MyStaticFiles**
  * **images**
      * *banner1.svg*

요청에 액세스할 수는 *banner1.svg* 정적 파일 미들웨어를 다음과 같이 구성 하 여 파일:

[!code-csharp[](static-files/samples/1x/StartupTwoStaticFiles.cs?name=snippet_ConfigureMethod&highlight=5-10)]

위의 코드는 *MyStaticFiles* 디렉터리 계층 구조를 통해 공개적으로 노출 됩니다는 *StaticFiles* URI 세그먼트입니다. 요청을 *http://\<server_address > /StaticFiles/images/banner1.svg* 역할는 *banner1.svg* 파일입니다.

다음 태그 참조 *MyStaticFiles/images/banner1.svg*:

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_outside)]

### <a name="set-http-response-headers"></a>HTTP 응답 헤더 설정

A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions) 개체는 HTTP 응답 헤더를 설정할 데 사용할 수 있습니다. 웹 루트에서 정적 파일 서비스를 구성 하는 것 외에도 다음 코드에서는 `Cache-Control` 헤더:

[!code-csharp[](static-files/samples/1x/StartupAddHeader.cs?name=snippet_ConfigureMethod)]

[HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) 에 있는 메서드는 [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) 패키지 합니다.

파일 내용이 공개적으로 캐시할 수 10 분 (600 초):

![추가 된 캐시 제어 헤더를 보여 주는 응답 헤더](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a>정적 파일 권한 부여

정적 파일 미들웨어 인증 검사를 제공 하지 않습니다. 모든 파일에서 제공 비롯 *wwwroot*, 공개적으로 액세스할 수 있습니다. 파일을 제공 하려면 권한 부여 기반으로 합니다.

* 외부에 보관해 두면 *wwwroot* 및 정적 파일 미들웨어에 액세스할 수 있는 모든 디렉터리 **및**
* 권한 부여 적용 되는 동작 메서드를 통해 역할입니다. 반환 된 [FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult) 개체:

[!code-csharp[](static-files/samples/1x/Controllers/HomeController.cs?name=snippet_BannerImageAction)]

## <a name="enable-directory-browsing"></a>디렉터리 검색을 사용 하도록 설정

디렉터리 검색 웹 응용 프로그램의 사용자가 디렉터리 목록을 볼 수 및 지정된 된 디렉터리 내의 파일입니다. 보안상의 이유로 기본적으로 비활성화 되어 디렉터리 검색 (참조 [고려 사항](#considerations)). Enable 디렉터리를 호출 하 여 검색 된 [UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_) 메서드에서 `Startup.Configure`:

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=12-17)]

필요한 서비스를 호출 하 여 추가 된 [AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 메서드에서 `Startup.ConfigureServices`:

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureServicesMethod&highlight=3)]

위의 코드 디렉터리를 검색할 수는 *wwwroot/이미지* URL을 사용 하 여 폴더 *http://\<server_address > / MyImages*, 각 파일 및 폴더에 대 한 링크로:

![디렉터리 검색](static-files/_static/dir-browse.png)

참조 [고려 사항](#considerations) 검색을 사용 하도록 설정할 때는 보안 위험에 있습니다.

두 참고 `UseStaticFiles` 다음 예제에서를 호출 합니다. 첫 번째 호출의 정적 파일 처리를 사용 하면는 *wwwroot* 폴더입니다. 두 번째 호출의 디렉터리 검색을 사용 하면는 *wwwroot/이미지* URL을 사용 하 여 폴더 *http://\<server_address > / MyImages*:

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=3,5)]

## <a name="serve-a-default-document"></a>기본 문서를 제공

설정 기본 홈 페이지 방문자 논리는 시작점을 제공 사이트를 방문할 때. 기본 페이지의 URI를 정규화 하는 사용자 없이 처리 하려면 호출는 [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 메서드에서 `Startup.Configure`:

[!code-csharp[](static-files/samples/1x/StartupEmpty.cs?name=snippet_ConfigureMethod&highlight=3)]

> [!IMPORTANT]
> `UseDefaultFiles`먼저 호출 해야 `UseStaticFiles` 기본 파일 역할을 합니다. `UseDefaultFiles`파일 사용 될 실제로 하지 않는 URL 재작성 기가입니다. 정적 파일 미들웨어를 통해 사용 하도록 설정 `UseStaticFiles` 파일 역할을 합니다.

와 `UseDefaultFiles`에 대 한 폴더 검색에 대 한 요청:

* *default.htm*
* *default.html*
* *index.htm*
* *index.html*

목록에서 첫 번째 파일이 요청에는 정규화 된 URI가 것 처럼 서비스 됩니다. 요청 된 URI를 반영 하기 위해 브라우저 URL이 계속 됩니다.

다음 코드에서는 기본 파일 이름을 변경 *mydefault.html*:

[!code-csharp[](static-files/samples/1x/StartupDefault.cs?name=snippet_ConfigureMethod)]

## <a name="usefileserver"></a>UseFileServer

[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 의 기능을 결합 `UseStaticFiles`, `UseDefaultFiles`, 및 `UseDirectoryBrowser`합니다.

다음 코드에서는 기본 파일 및 정적 파일 처리 합니다. 디렉터리 검색 기능이 사용 되지 않습니다.

```csharp
app.UseFileServer();
```

매개 변수가 없는 오버 로드에 디렉터리 검색을 사용 하 여 다음 코드를 작성 합니다.

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
```

다음 디렉터리 계층 구조를 고려해 야 합니다.

* **wwwroot**
  * **css**
  * **images**
  * **js**
* **MyStaticFiles**
  * **images**
      * *banner1.svg*
  * *default.html*

다음 코드를 통해 정적 파일, 기본 파일 및 디렉터리 검색의 `MyStaticFiles`:

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureMethod&highlight=5-11)]

`AddDirectoryBrowser`호출 해야 합니다는 `EnableDirectoryBrowsing` 속성 값은 `true`:

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureServicesMethod)]

Url 및 파일 계층 구조를 사용 하 여 앞에 오는 코드를 다음과 같이 확인 됩니다.

| URI            |                             응답  |
| ------- | ------|
| *http://\<server_address>/StaticFiles/images/banner1.svg*    |      MyStaticFiles/images/banner1.svg |
| *http://\<server_address>/StaticFiles*             |     MyStaticFiles/default.html |

에 기본 이름이 지정 된 파일이 없는 경우는 *MyStaticFiles* 디렉터리 *http://\<server_address > / StaticFiles* 클릭 가능한 링크와 함께 나열 하는 디렉터리를 반환 합니다.

![정적 파일 목록](static-files/_static/db2.png)

> [!NOTE]
> `UseDefaultFiles`및 `UseDirectoryBrowser` URL을 사용 하 여 *http://\<server_address > / StaticFiles* 리디렉션됩니다 후행 슬래시를 트리거하는 클라이언트 쪽 없이 *http://\<server_address > / StaticFiles /*합니다. 후행 슬래시를 추가 확인 합니다. 문서 내에서 상대 Url은 후행 슬래시가 없는 잘못 된 것으로 간주 됩니다.

## <a name="fileextensioncontenttypeprovider"></a>FileExtensionContentTypeProvider

[FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider) 클래스를 포함 한 `Mappings` 속성의 MIME 콘텐츠 형식에 대 한 파일 확장명 매핑을 역할을 수행 합니다. 다음 샘플에서는 여러 파일 확장명이 알려진된 MIME 형식에 등록 됩니다. *.rtf* 확장 바뀝니다 및 *.mp4* 제거 됩니다.

[!code-csharp[](static-files/samples/1x/StartupFileExtensionContentTypeProvider.cs?name=snippet_ConfigureMethod&highlight=3-12,19)]

참조 [MIME 콘텐츠 형식을](http://www.iana.org/assignments/media-types/media-types.xhtml)합니다.

## <a name="non-standard-content-types"></a>사용할 수 없는 콘텐츠 형식

거의 400 알려진된 파일 콘텐츠 형식을 이해 하는 정적 파일 미들웨어입니다. 사용자가 알 수 없는 파일 형식의 파일을 요청 하는 경우 정적 파일 미들웨어는 HTTP 404 (찾을 수 없음) 응답을 반환 합니다. 디렉터리 검색을 사용 하는 경우 파일에는 링크가 표시 됩니다. URI는 HTTP 404 오류를 반환합니다.

다음 코드는 알 수 없는 형식을 처리를 사용 하도록 설정 하 고 알 수 없는 파일을 이미지로 렌더링.

[!code-csharp[](static-files/samples/1x/StartupServeUnknownFileTypes.cs?name=snippet_ConfigureMethod)]

위의 코드에서 알 수 없는 콘텐츠 형식으로 파일에 대 한 요청 이미지 형식으로 반환 됩니다.

> [!WARNING]
> 사용 하도록 설정 [ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes) 보안상 위험할 수 있습니다. 기본적으로 비활성화 되어 및의 사용은 권장 되지 않습니다. [FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider) 비표준 확장명을 가진 파일을 처리 하는 보다 안전한 대체 방법을 제공 합니다.

### <a name="considerations"></a>고려 사항

> [!WARNING]
> `UseDirectoryBrowser`및 `UseStaticFiles` 비밀 정보를 누출 할 수 있습니다. 해제 디렉터리를 프로덕션 환경에서 검색을 사용 하는 것이 좋습니다. 디렉터리를 활성화를 주의 깊게 검토 `UseStaticFiles` 또는 `UseDirectoryBrowser`합니다. 전체 디렉터리와 해당 하위 디렉터리의 공개적으로 액세스할 수 있게 합니다. 저장소 파일을 공개적으로 서비스에 대 한 적합 한 전용된 디렉터리에 같은  *\<content_root > / wwwroot*합니다. MVC 뷰, Razor 페이지 (2.x에만 해당), 구성 파일 등에서 이러한 파일을 구분 합니다.

* 노출 된 콘텐츠에 대 한 Url `UseDirectoryBrowser` 및 `UseStaticFiles` 는 대/소문자 구분 및 기본 파일 시스템의 문자 제한이 적용 됩니다. 예를 들어 Windows는 대/소문자 구분&mdash;Mac 및 Linux 되지 않습니다.

* ASP.NET Core 응용 프로그램을 사용 하 여 IIS에서에서 호스팅되는 [ASP.NET Core 모듈 (ANCM)](xref:fundamentals/servers/aspnet-core-module) 정적 파일 요청을 비롯 한 응용 프로그램에 대 한 모든 요청을 전달 합니다. IIS 정적 파일 처리기는 사용 되지 않습니다. 요청을 처리 하기 전에 ANCM 하 여 처리 중인 확률이 없습니다.

* IIS 관리자에서 서버 또는 웹 사이트 수준에서 IIS 정적 파일 처리기를 제거 하려면 다음 단계를 완료 합니다.
    1. 탐색 하 고 **모듈** 기능입니다.
    1. 선택 **모듈은 staticfilemodule입니다** 목록에 있습니다.
    1. 클릭 **제거** 에 **동작** 사이드바 합니다.

> [!WARNING]
> IIS 정적 파일 처리기에서 사용 되는 경우 **및** 는 ANCM 올바르게 구성 되었는지, 정적 파일에서 제공 됩니다. 이런 경우 예를 들어 경우는 *web.config* 파일이 배포 되지 않습니다.

* 코드 파일을 배치할 (포함 하 여 *.cs* 및 *.cshtml*) 응용 프로그램 프로젝트의 웹 루트 외부입니다. 따라서 응용 프로그램의 클라이언트 쪽 콘텐츠 및 서버 기반 코드 사이 논리적 분리를 만들어집니다. 이렇게 하면 서버 쪽 코드를에서 유출 되지 않습니다.

## <a name="additional-resources"></a>추가 리소스

* [미들웨어](xref:fundamentals/middleware)

* [ASP.NET Core 소개](xref:index)