---
title: "ASP.NET Core의 파일 공급자"
author: ardalis
description: "ASP.NET Core가 파일 공급자를 이용해서 파일 시스템에 대한 접근을 추상화하는 방법을 알아봅니다."
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.assetid: 1e35d362-0005-4f84-a187-274ca203a787
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/file-providers
translationtype: Machine Translation
ms.sourcegitcommit: 0ebb9b63931ccb26126740de08270eda9b1ea486
ms.openlocfilehash: 813fc1747714ae8d26aff58ec32555df677eb813
ms.lasthandoff: 03/23/2017

---
# <a name="file-providers-in-aspnet-core"></a>ASP.NET Core의 파일 공급자

작성자: [Steve Smith](http://ardalis.com)

ASP.NET Core는 파일 공급자를 이용해서 파일 시스템에 대한 접근을 추상화합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample)

## <a name="file-provider-abstractions"></a>파일 공급자 추상화

파일 공급자는 파일 시스템에 대한 추상화로, 기본 인터페이스는 `IFileProvider`입니다. `IFileProvider`는 파일 정보(`IFileInfo`)나 디렉터리 정보(`IDirectoryContents`)를 가져오고, 변경 알림을 설정하는 메서드를 (`IChangeToken`을 사용해서) 노출합니다.

`IFileInfo`는 개별 파일 및 디렉터리에 대한 메서드와 속성을 제공합니다. 두 가지 불리언 속성인 `Exists` 속성과 `IsDirectory` 속성을 비롯해서 파일 이름 (`Name`), 크기 (`Length`, 바이트), 마지막 수정 날짜 (`LastModified`) 및 물리적 경로를 (`PhysicalPath`) 기술하는 속성들을 갖고 있습니다. `CreateReadStream` 메서드를 사용해서 파일을 읽을 수도 있습니다.

## <a name="file-provider-implementations"></a>파일 공급자 구현

`IFileProvider`의 구현으로 물리적 공급자, 임베디드 공급자 그리고 복합 공급자의 세 가지 공급자를 사용할 수 있습니다. 물리적 공급자는 시스템의 실제 파일에 접근하기 위해서 사용됩니다. 그리고 임베디드 공급자는 어셈블리에 포함된 파일에 접근하기 위해서 사용됩니다. 마지막으로 복합 공급자는 하나 이상의 개별 공급자로부터 얻어진 파일 및 디렉터리에 대한 복합적인 접근을 지원하기 위해서 사용됩니다.

### <a name="physicalfileprovider"></a>PhysicalFileProvider

`PhysicalFileProvider`는 실제 파일 시스템에 대한 접근을 제공합니다. `System.IO.File` 형식을 (물리적 공급자에 대한) 래핑하고, 특정 디렉터리와 그 하위의 자식들에 대한 모든 경로를 대상 범위로 지정합니다. 이렇게 범위를 지정함으로써 특정 디렉터리 및 그 하위 자식들에 대한 접근만 허용해서 경계 외부의 파일 시스템에 대한 접근을 차단합니다. 이 공급자의 인스턴스를 생성하려면 공급자를 대상으로 하는 모든 요청에 대해 기본 경로 역할을 하는 (그리고 해당 경로 외부에 대한 접근은 차단하는) 디렉터리 경로를 반드시 제공해야 합니다. ASP.NET Core 응용 프로그램에서는 `PhysicalFileProvider`의 인스턴스를 직접 생성하거나, 컨트롤러 또는 서비스의 생성자에서 [종속성 주입](dependency-injection.md)을 통해서 `IFileProvider`를 요청할 수 있습니다. 일반적으로 후자의 접근 방식이 보다 유연하고 테스트 가능한 솔루션을 만들어줍니다.

다음 예제는 `PhysicalFileProvider`를 생성하는 방법을 보여줍니다.

```csharp
IFileProvider provider = new PhysicalFileProvider(applicationRoot);
IDirectoryContents contents = provider.GetDirectoryContents(""); // the applicationRoot contents
IFileInfo fileInfo = provider.GetFileInfo("wwwroot/js/site.js"); // a file under applicationRoot
```

하위 경로를 지정해서 디렉터리의 내용을 반복 조회하거나 특정 파일의 정보를 가져올 수도 있습니다.

컨트롤러에서 공급자를 사용하려면 공급자를 컨트롤러의 생성자 매개 변수로 지정한 다음, 전달받은 공급자 개체를 필드에 할당합니다. 그리고 액션 메서드에서는 이 지역 인스턴스를 사용합니다:

[!code-csharp[주](file-providers/sample/src/FileProviderSample/Controllers/HomeController.cs?highlight=5,7,12&range=6-19)]

그런 다음, 응용 프로그램의 `Startup` 클래스에서 공급자를 생성합니다:

[!code-csharp[주](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=35,40&range=1-43)]

다음 *Index.cshtml* 뷰는 전달된 `IDirectoryContents`를 반복 조회합니다:

[!code-html[주](file-providers/sample/src/FileProviderSample/Views/Home/Index.cshtml?highlight=2,7,9,11,15)]

그 결과는 다음과 같습니다:

![파일 공급자 예제 응용 프로그램이 실제 파일 및 폴더의 목록을 출력합니다.](file-providers/_static/physical-directory-listing.png)

### <a name="embeddedfileprovider"></a>EmbeddedFileProvider

`EmbeddedFileProvider`는 어셈블리에 포함된 파일에 접근하기 위한 용도로 사용됩니다. .NET Core에서는 *.csproj* 파일의 `<EmbeddedResource>` 요소에 지정된 파일들이 어셈블리에 포함됩니다:

[!code-json[주](file-providers/sample/src/FileProviderSample/FileProviderSample.csproj?range=13-18)]

어셈블리에 포함시킬 파일들을 지정할 때, [Globbing 패턴](#globbing-patterns)을 사용할 수 있습니다. 이 패턴을 사용하면 하나 이상의 파일을 지정할 수 있습니다.

> [!NOTE]
> 실제로 프로젝트의 모든 .js 파일을 어셈블리에 포함시키고 싶지는 않을 것입니다. 이번 예제는 단지 설명을 위한 것입니다.

`EmbeddedFileProvider`를 생성할 때, 생성자에게 읽고자 하는 어셈블리를 전달해야 합니다.

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

위의 코드는 현재 실행중인 어셈블리에 접근하는 `EmbeddedFileProvider`를 생성하는 방법을 보여줍니다.

앞의 예제 응용 프로그램을 `EmbeddedFileProvider`를 사용하도록 변경하면 다음과 같은 결과가 출력됩니다:

![파일 공급자 예제 응용 프로그램이 임베디드 파일들의 목록을 출력합니다.](file-providers/_static/embedded-directory-listing.png)

> [!NOTE]
> 어셈블리에 포함된 리소스는 디렉터리를 노출하지 않는 반면, 파일명 자체에 `.` 구분자를 이용한 리소스의 경로가 (네임스페이스로) 포함되어 있습니다.

> [!TIP]
> `EmbeddedFileProvider`의 생성자에 선택적 `baseNamespace` 매개 변수를 전달할 수도 있습니다. 이 매개 변수를 지정하면 전달된 네임스페이스 하위의 리소스들만을 대상으로 `GetDirectoryContents` 호출의 범위가 제한됩니다.

### <a name="compositefileprovider"></a>CompositeFileProvider

`CompositeFileProvider`는 `IFileProvider`의 인스턴스들을 결합해서 다수의 공급자를 이용한 파일 작업을 처리할 수 있는 단일 인터페이스를 제공합니다. `CompositeFileProvider`를 생성할 때는 생성자에 하나 이상의 `IFileProvider` 인스턴스를 전달합니다:

[!code-csharp[주](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=3&range=35-37)]

앞에서 구성한 물리적 공급자와 임베디드 공급자를 모두 포함하는 `CompositeFileProvider`를 사용하도록 예제 응용 프로그램을 수정해보면 다음과 같은 결과가 출력됩니다:

![파일 공급자 예제 응용 프로그램이 실제 파일 및 폴더와 임베디드 파일들의 목록을 모두 출력합니다.](file-providers/_static/composite-directory-listing.png)

## <a name="watching-for-changes"></a>변경 내용 감시하기

`IFileProvider`의 `Watch` 메서드를 이용하면 여러 파일 및 디렉터리의 변경 사항을 감지할 수 있습니다. 이 메서드는 [Globbing 패턴](#globbing-patterns)을 이용해서 복수의 파일을 지정할 수 있는 경로 문자열을 전달받고 `IChangeToken`을 반환합니다. 이 토큰은 변경 여부 확인에 사용할 수 있는 `HasChanged` 속성과, 지정된 경로 문자열에서 변경 내용이 감지되면 호출되는 `RegisterChangeCallback` 메서드를 제공합니다. 각 변경 토큰은 단일 변경에 대한 응답으로 자신과 연결된 콜백만 호출한다는 점에 주의하시기 바랍니다. 모니터링을 지속적으로 수행하기 위해서는 다음 예제처럼 `TaskCompletionSource`를 활용하거나 변경 사항에 대한 응답에서 다시 `IChangeToken` 인스턴스를 생성해야 합니다.

다음 예제는 텍스트 파일이 수정될 때마다 콘솔 응용 프로그램이 메시지를 표시하도록 구성됩니다:

[!code-csharp[주](file-providers/sample/src/WatchConsole/Program.cs?highlight=11,12,24,26,27)]

파일을 여러 번 저장한 결과는 다음과 같습니다:

![dotnet run을 실행한 후, 명령 창에서 quotes.txt 파일을 모니터링해서 변경 내용을 확인하고 파일이 다섯 번 변경되었음을 보여줍니다.](file-providers/_static/watch-console.png)

> [!NOTE]
> Docker 컨테이너나 네트워크 공유 같은 일부 파일 시스템은 변경 알림을 안정적으로 전송할 수 없습니다. 그러나 `DOTNET_USE_POLLINGFILEWATCHER` 환경 변수를 `1`이나 `true`로 설정하면 파일 시스템이 4 초마다 폴링됩니다.

## <a name="globbing-patterns"></a>Globbing 패턴

파일 시스템 경로는 *Globbing 패턴*이라고도 부르는 와일드 카드 패턴을 사용합니다. 이 단순 패턴을 이용해서 파일 그룹을 지정할 수 있습니다. 두 개의 와일드 카드 문자는 `*`와 `**` 입니다.

**`*`**

   현재 폴더 수준의 모든 항목, 모든 파일명 또는 모든 파일 확장자를 찾습니다. 파일 경로의 `/` 및 `.` 문자에 의해서 일치가 중단됩니다.

<strong><code>**</code></strong>

   여러 디렉터리 수준의 모든 항목과 일치합니다. 디렉터리 계층 내에서 많은 파일들을 재귀적으로 찾기 위해서 사용할 수 있습니다.

### <a name="globbing-pattern-examples"></a>Globbing 패턴 예제

**`directory/file.txt`**

   특정 디렉터리의 특정 파일을 찾습니다.

**<code>directory/*.txt</code>**

   지정한 디렉터리에 존재하는 확장자가 `.txt`인 모든 파일을 찾습니다.

**`directory/*/bower.json`**

   `directory` 디렉터리의 한 수준 아래의 모든 하위 디렉터리들의 모든 `bower.json` 파일을 찾습니다.

**<code>directory/&#42;&#42;/&#42;.txt</code>**

   `directory` 디렉터리의 하위의 모든 위치에 존재하는 확장자가 `.txt`인 모든 파일을 찾습니다.

## <a name="file-provider-usage-in-aspnet-core"></a>ASP.NET Core의 파일 공급자 활용

ASP.NET Core는 다양한 부분에서 파일 공급자를 활용합니다. 예를 들어, `IHostingEnvironment`는 응용 프로그램의 콘텐츠 루트와 웹 루트를 `IFileProvider` 형식으로 노출합니다. 정적 파일 미들웨어는 파일 공급자를 이용해서 정적 파일을 찾습니다. Razor는 뷰를 찾기 위해 `IFileProvider`를 빈번히 사용합니다. Dotnet의 게시 기능은 파일 공급자와 Globbing 패턴을 사용해서 게시해야 할 파일들을 지정합니다.

## <a name="recommendations-for-use-in-apps"></a>응용 프로그램에서 사용시 권장 사항

ASP.NET Core 응용 프로그램에서 파일 시스템에 접근해야 할 때, 본문에서 살펴본 것처럼 [종속성 주입](dependency-injection.md)을 통해서 `IFileProvider`의 인스턴스를 요청한 다음, 해당 인스턴스의 메서드를 사용해서 접근 작업을 수행할 수 있습니다. 이 방식을 사용하면 응용 프로그램이 시작될 때 한 번만 공급자를 구성해서 응용 프로그램이 생성하는 구현 형식의 인스턴스 개수를 줄일 수 있습니다.
