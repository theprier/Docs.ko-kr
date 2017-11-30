---
title: "ASP.NET Core에서 정적 파일 작업하기"
author: rick-anderson
description: "ASP.NET Core에서 정적 파일을 사용하는 방법을 알아봅니다."
keywords: "ASP.NET Core, 정적 파일, 정적 자산, HTML, CSS, JavaScript"
ms.author: riande
manager: wpickett
ms.date: 4/07/2017
ms.topic: article
ms.assetid: e32245c7-4eee-4831-bd2e-915dbf9f5f70
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/static-files
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40c9a799c6ac8a2ce712df4b8fbf3c142ef3fd82
ms.sourcegitcommit: 8f4d4fad1ca27adf9e396f5c205c9875a3963664
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-static-files-in-aspnet-core"></a>ASP.NET Core에서 정적 파일 작업하기

<a name="fundamentals-static-files"></a>

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

HTML, CSS, 이미지 및 JavaScript 같은 정적 파일은 ASP.NET Core 응용 프로그램이 클라이언트에 직접 제공할 수 있는 자산입니다. 

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="serving-static-files"></a>정적 파일 제공하기

정적 파일은 일반적으로 웹 루트 폴더에 (*\<content-root>/wwwroot*) 위치합니다. 보다 자세한 정보는 [콘텐츠 루트](xref:fundamentals/index#content-root)와 [웹 루트](xref:fundamentals/index#web-root)를 참고하시기 바랍니다. 대부분 콘텐츠 루트를 현재 디렉토리로 설정해서 개발 중에 프로젝트의 웹 루트가 드러나게 만듭니다.

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs?highlight=5&start=12&end=22)]

정적 파일은 웹 루트의 하위에 위치한 모든 폴더에 저장할 수 있으며, 웹 루트 기준의 상대 경로를 통해서 접근할 수 있습니다. 가령, Visual Studio를 사용해서 기본 웹 응용 프로그램 프로젝트를 생성하면 *wwwroot* 폴더 하위에 *css*, *images* 및 *js* 같은 몇 개의 폴더가 만들어집니다. 이 경우, *images* 하위 폴더에 위치한 이미지에 접근하기 위한 URI는 다음과 같습니다: 

* `http://<app>/images/<imageFileName>`
* `http://localhost:9189/images/banner3.svg`

정적 파일을 제공하기 위해서는 정적 파일에 대한 [미들웨어](middleware.md)를 구성해서 파이프라인에 추가해야 합니다. 프로젝트에 *Microsoft.AspNetCore.StaticFiles* 패키지에 대한 종속성을 추가한 다음, `Startup.Configure` 메서드에서 `UseStaticFiles` 확장 메서드를 호출하면 정적 파일 미들웨어를 구성할 수 있습니다:

[!code-csharp[Main](../fundamentals/static-files/sample/StartupStaticFiles.cs?highlight=3&name=snippet1)]

위의 코드에서 `app.UseStaticFiles();` 확장 메서드 호출은 웹 루트 (기본적으로 *wwwroot*) 하위의 파일들을 제공할 수 있게 해줍니다. 본문의 뒷부분에서는 `UseStaticFiles`를 이용해서 다른 디렉터리에 위치한 콘텐츠를 제공할 수 있게 만드는 방법도 살펴봅니다.

정적 파일을 서비스하기 위해서는 반드시 "Microsoft.AspNetCore.StaticFiles" NuGet 패키지가 필요합니다.

> [!NOTE]
> 기본 웹 루트는 *wwwroot* 디렉터리지만, `UseWebRoot`를 이용해서 다른 경로를 웹 루트로 지정할 수도 있습니다.

프로젝트 구조에서 서비스하고자 하는 정적 파일이 다음과 같이 웹 루트의 외부에도 존재한다고 가정해보겠습니다:

* wwwroot
  * css
  * images
  * ...
* MyStaticFiles
  * test.png

이 경우, *test.png*에 접근하기 위한 요청을 허용하려면, 다음과 같이 정적 파일 미들웨어를 구성해야 합니다:

[!code-csharp[Main](../fundamentals/static-files/sample/StartupTwoStaticFiles.cs?highlight=5,6,7,8,9,10&name=snippet1)]

이제 `http://<app>/StaticFiles/test.png`를 요청하면 test.png 파일에 접근할 수 있습니다. 

`StaticFileOptions()`로 응답 헤더를 설정할 수도 있습니다. 예를 들어, 다음 코드는 *wwwroot* 폴더 하위에 위치한 정적 파일을 서비스하도록 설정하고, 해당 파일들을 10분(600초) 동안 공개적으로 캐시할 수 있도록 `Cache-Control` 헤더를 설정합니다:

[!code-csharp[Main](../fundamentals/static-files/sample/StartupAddHeader.cs?name=snippet1)]

[HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) 메서드는 [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) 패키지에서 사용할 수 있습니다. 이 메서드를 사용할 수 없다면 *csharp* 파일에 `using Microsoft.AspNetCore.Http;` 문을 추가하십시오.

![추가 된 캐시 제어 헤더를 보여 주는 응답 헤더](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a>정적 파일 권한 부여

정적 파일 모듈은 권한 부여 기능을 **제공하지 않습니다.** *wwwroot* 폴더 하위에 위치한 파일을 비롯해서, 정적 파일 미들웨어가 제공하는 모든 파일은 공개적으로 사용할 수 있습니다. 권한 부여를 기반으로 파일을 제공하려면:

* 대상 파일을 *wwwroot* 및 정적 파일 미들웨어가 접근할 수 있는 모든 디렉터리의 외부에 저장합니다. **그리고**

* 권한 부여가 적용된 컨트롤러 액션에서 `FileResult`를 반환하는 방식으로 파일을 서비스합니다.

## <a name="enabling-directory-browsing"></a>디렉터리 브라우징 활성화하기

디렉터리 브라우징을 사용하면 웹 응용 프로그램의 사용자가 지정된 디렉터리 내의 디렉터리 및 파일 목록을 살펴볼 수 있습니다. 디렉터리 브라우징은 기본적으로 보안상의 이유로 비활성화되어 있습니다 ([고려 사항](#considerations) 참조). 디렉터리 브라우징을 활성화시키려면 `Startup.Configure`에서 `UseDirectoryBrowser` 확장 메서드를 호출합니다: 

[!code-csharp[Main](static-files/sample/StartupBrowse.cs?name=snippet1)]

그런 다음, `Startup.ConfigureServices`에서 `AddDirectoryBrowser` 확장 메서드를 호출해서 필요한 서비스를 추가합니다: 

[!code-csharp[Main](static-files/sample/StartupBrowse.cs?name=snippet2)]

위의 코드는 http://\<app>/MyImages라는 URL을 통해서 *wwwroot/images* 폴더의 디렉터리 브라우징을 허용하며, 그 하위의 각 파일과 폴더에 대한 링크를 제공합니다: 

![디렉터리 검색](static-files/_static/dir-browse.png)

디렉터리 브라우징을 허용할 경우 발생할 수 있는 보안상의 위험에 대해서는 [고려 사항](#considerations)을 참고하시기 바랍니다. 

위의 코드에서 `app.UseStaticFiles`를 두 번 호출하고 있다는 점에 주의하십시오. 첫 번째 호출은 *wwwroot* 폴더 하위의 CSS, images 및 JavaScript 디렉터리를 서비스하기 위한 호출이고, 두 번째 호출은 http://\<app>/MyImages URL을 통해서 *wwwroot/images* 폴더의 디렉터리 브라우징을 허용하기 위한 호출입니다:

[!code-csharp[Main](static-files/sample/StartupBrowse.cs?highlight=3,5&name=snippet1)]

## <a name="serving-a-default-document"></a>기본 문서 제공하기

기본 홈 페이지를 설정하면 사용자가 사이트를 방문할 때 처음 시작할 페이지를 지정할 수 있습니다. 사용자가 완전한 URI를 지정하지 않더라도 웹 응용 프로그램에서 기본 페이지를 제공하려면 다음과 같이 `Startup.Configure`에서 `UseDefaultFiles` 확장 메서드를 호출합니다:

[!code-csharp[Main](../fundamentals/static-files/sample/StartupEmpty.cs?highlight=3&name=snippet1)]

> [!NOTE]
> 기본 문서를 제공하기 위해서는 반드시 `UseStaticFiles` 확장 메서드를 `UseDefaultFiles` 확장 메서드보다 먼저 호출해야 합니다. `UseDefaultFiles` 확장 메서드는 실제로는 파일을 제공하지 않는 URL 재작성자입니다. 따라서 해당 파일을 서비스하기 위해서는 정적 파일 미들웨어를 활성화시켜야만 (`UseStaticFiles`) 합니다.

`UseDefaultFiles`를 사용하면, 폴더 요청 시 다음 파일들을 검색합니다: 

* default.htm
* default.html
* index.htm
* index.html

이 목록에서 발견된 첫 번째 파일이, 마치 정규화된 URI 요청인 것처럼 제공됩니다 (비록 브라우저에 나타나는 URI는 여전히 처음 요청된 URI 그대로지만). 

다음 코드는 기본 파일의 이름을 *mydefault.html*로 변경하는 방법을 보여줍니다:

[!code-csharp[Main](static-files/sample/StartupDefault.cs?name=snippet1)]

## <a name="usefileserver"></a>UseFileServer

`UseFileServer`는 `UseStaticFiles`, `UseDefaultFiles` 및 `UseDirectoryBrowser`의 기능을 한꺼번에 제공합니다.

다음 코드는 정적 파일과 기본 파일은 제공하지만, 디렉터리 브라우징은 허용하지 않습니다:

```csharp
app.UseFileServer();
   ```

반면, 다음 코드는 정적 파일, 기본 파일 및 디렉터리 브라우징을 모두 허용합니다: 

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
   ```

디렉터리 브라우징을 허용할 경우 발생할 수 있는 보안상의 위험에 대해서는 [고려 사항](#considerations)을 참고하시기 바랍니다. `UseStaticFiles`, `UseDefaultFiles` 및 `UseDirectoryBrowser`와 마찬가지로, 웹 루트 외부에 존재하는 파일을 제공하고 싶다면, `FileServerOptions` 개체의 인스턴스를 생성하고 구성한 다음, 이를 `UseFileServer`에 매개 변수로 전달합니다. 예를 들어서, 웹 앱의 디렉터리 계층 구조가 다음과 같다고 가정해보겠습니다:

* wwwroot

  * css

  * images

  * ...

* MyStaticFiles

  * test.png

  * default.html

이 예제 계층 구조를 사용하면서 `MyStaticFiles` 디렉터리를 대상으로 정적 파일, 기본 파일 및 디렉터리 브라우징 기능을 제공해야 하는 경우도 있습니다. 다음 코드 스니핏은 `FileServerOptions`를 한 번만 호출해서 해당 기능들을 활성화시키는 방법을 보여줍니다:

[!code-csharp[Main](static-files/sample/StartupUseFileServer.cs?highlight=5,6,7,8,9,10,11&name=snippet1)]

그리고 `enableDirectoryBrowsing`을 `true`로 설정할 경우에는 `Startup.ConfigureServices`에서 `AddDirectoryBrowser` 확장 메서드를 호출해야 합니다:

[!code-csharp[Main](static-files/sample/StartupUseFileServer.cs?name=snippet2)]

다음 표는 위의 파일 계층 구조와 코드를 사용할 경우의 요청 및 응답을 보여줍니다:

| URI            |                             응답  |
| ------- | ------|
| `http://<app>/StaticFiles/test.png`    |      MyStaticFiles/test.png |
| `http://<app>/StaticFiles`              |     MyStaticFiles/default.html |

만약 *MyStaticFiles* 디렉터리에 기본 파일이 존재하지 않으면 http://\<app>/StaticFiles URI는 클릭 가능한 링크가 제공되는 디렉터리 목록을 반환합니다:

![정적 파일 목록](static-files/_static/db2.PNG)

> [!NOTE]
> `UseDefaultFiles` 및 `UseDirectoryBrowser` 확장 메서드는 슬래시로 끝나지 않는 http://\<app>/StaticFiles 같은 URL을 전달받으면, 후행 슬래시를 추가한 http://\<app>/StaticFiles/ 같은 URL로 클라이언트 측 재지정을 수행합니다. URL이 슬래시로 끝나지 않으면 문서 내의 상대 URL이 올바르지 않게 됩니다.

## <a name="fileextensioncontenttypeprovider"></a>FileExtensionContentTypeProvider

`FileExtensionContentTypeProvider` 클래스는 파일 확장자와 MIME 콘텐츠 형식을 매핑하는 컬렉션을 갖고 있습니다. 다음 예제에서는 몇 가지 파일 확장자를 일반적으로 알려진 MIME 형식으로 등록하고, ".rtf"에 대한 MIME 형식은 대체하고, ".mp4"는 제거합니다.

[!code-csharp[Main](../fundamentals/static-files/sample/StartupFileExtensionContentTypeProvider.cs?highlight=3,4,5,6,7,8,9,10,11,12,19&name=snippet1)]

[MIME 콘텐츠 형식](http://www.iana.org/assignments/media-types/media-types.xhtml)을 참고하시기 바랍니다.

## <a name="non-standard-content-types"></a>비표준 콘텐츠 형식

ASP.NET 정적 파일 미들웨어는 거의 400 여개의 알려진 파일 콘텐츠 형식을 인식할 수 있습니다. 사용자가 알 수 없는 파일 형식의 파일을 요청할 경우, 정적 파일 미들웨어는 HTTP 404 (찾을 수 없음) 응답을 반환합니다. 디렉토리 브라우징이 활성화된 경우에도, 파일 링크는 표시되지만 해당 URI는 HTTP 404 오류를 반환합니다. 

다음 코드는 알 수 없는 형식의 파일에 대한 서비스를 활성화시키고, 알 수 없는 파일을 이미지로 렌더합니다. 

[!code-csharp[Main](static-files/sample/StartupServeUnknownFileTypes.cs?name=snippet1)]

위의 코드를 사용하면, 알 수 없는 콘텐츠 형식의 파일에 대한 요청이 이미지 형식으로 반환됩니다.

>[!WARNING]
> `ServeUnknownFileTypes`를 사용하는 것은 보안상 위험하므로 권장하지 않습니다. 앞에서 살펴본 `FileExtensionContentTypeProvider`가 비표준 확장자를 가진 파일을 서비스하기 위한 보다 안전한 방식의 대안을 제공합니다.

### <a name="considerations"></a>고려 사항

>[!WARNING]
> `UseDirectoryBrowser` 및 `UseStaticFiles`는 보안에 취약합니다. 프로덕션 환경에서는 디렉터리 브라우징을 **사용하지 않는 것**을 권장합니다. `UseStaticFiles`나 `UseDirectoryBrowser`를 이용해서 특정 디렉터리 전체를 활성화시키고 모든 하위 디렉터리에 접근할 수 있게 허용할 때는 극도로 주의해야 합니다. 공개 콘텐츠는 *\<content root>/wwwroot* 같은 자체적인 디렉터리에 저장하고, 응용 프로그램 뷰, 구성 파일 등으로부터 격리하는 것을 권장합니다.

* `UseDirectoryBrowser` 및 `UseStaticFiles`로 노출되는 콘텐츠의 URL은 기반 파일 시스템의 대소문자 구분 및 문자 제한의 영향을 받습니다. 가령, Windows는 대소문자를 구분하지 않지만, Mac과 Linux는 대소문자를 구분합니다.

* IIS에서 호스팅되는 ASP.NET Core 응용 프로그램은 ASP.NET Core 모듈을 통해서 정적 파일에 관한 요청을 비롯한 모든 요청을 응용 프로그램에 전달합니다. IIS의 정적 파일 처리기는 ASP.NET Core 모듈이 요청을 처리하기 전에 먼저 요청을 처리할 수 있는 기회가 없으므로 전혀 사용되지 않습니다. 

* 서버 수준이나 웹사이트 수준에서 IIS 정적 파일 처리기를 제거하려면: 

     *  IIS(인터넷 정보 서비스) 관리자에서 **모듈** 기능으로 이동합니다.

     * 목록에서 **StaticFileModule**을 선택합니다.

     * **작업** 사이드바에서 **제거**를 누릅니다.

>[!WARNING]
> 만약 IIS의 정적 파일 처리기가 활성화되어 **있고**, ASP.NET Core 모듈(ANCM)이 정상적으로 구성되지 않았다면 (예를 들어, *web.config* 파일이 배포되지 않았다면), IIS 정적 파일 처리기에 의해서 정적 파일이 제공됩니다.

* C#이나 Razor 같은 코드 파일은 반드시 프로젝트의 웹 루트 (기본적으로 *wwwroot*) 외부에 위치해야 합니다. 그래야만 응용 프로그램의 클라이언트 측 콘텐츠와 서버 측 코드 간에 명확한 분리를 제공하고 서버 측 코드가 유출되는 것을 방지할 수 있습니다. 

## <a name="additional-resources"></a>추가 자료

* [미들웨어](middleware.md)

* [ASP.NET Core 소개](../index.md)
