---
title: "ASP.NET Core의 파일 공급자"
author: ardalis
description: "ASP.NET Core에서 파일 공급자를 사용하여 파일 시스템 액세스를 추상화하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/file-providers
ms.openlocfilehash: 06197f967e111d75531e9c3bcbcbdb971cb9f99b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="file-providers-in-aspnet-core"></a>ASP.NET Core의 파일 공급자

작성자: [Steve Smith](https://ardalis.com/)

ASP.NET Core에서 파일 공급자를 사용하여 파일 시스템 액세스를 추상화합니다.

[예제 코드 보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="file-provider-abstractions"></a>파일 공급자 추상화

파일 공급자는 파일 시스템에 대한 추상화로. 기본 인터페이스는 `IFileProvider`입니다. `IFileProvider`는 파일 정보(`IFileInfo`)나 디렉터리 정보(`IDirectoryContents`)를 가져오고, 변경 알림을 설정(`IChangeToken` 을 사용) 하는 메서드를 노출합니다.

`IFileInfo`는 개별 파일 또는 디렉터리에 대한 메서드 및 속성을 제공합니다. 두 개의 부울 속성, `Exists` 및 `IsDirectory`와 파일의 `Name`, `Length`(바이트) 및 `LastModified` 날짜를 설명하는 속성이 있습니다. 해당 `CreateReadStream` 메서드를 사용하여 파일에서 읽을 수 있습니다.

## <a name="file-provider-implementations"></a>파일 공급자 구현

`IFileProvider`의 세 가지 구현, 물리적, 포함 및 복합을 사용할 수 있습니다. 물리적 공급자는 실제 시스템의 파일에 액세스하는 데 사용됩니다. 포함된 공급자는 어셈블리에 포함된 파일에 액세스하는 데 사용됩니다. 복합 공급자는 하나 이상의 다른 공급자에서 파일 및 디렉터리에 대한 결합된 액세스를 제공하는 데 사용됩니다.

### <a name="physicalfileprovider"></a>PhysicalFileProvider

`PhysicalFileProvider`는 실제 파일 시스템에 대한 액세스를 제공합니다. 모든 경로를 디렉터리 및 해당 자식으로 범위를 지정하여 `System.IO.File` 형식(물리적 공급자용)을 래핑합니다. 이 범위 지정은 이 경계 외부의 파일 시스템에 대한 액세스를 방지하여 특정 디렉터리 및 해당 자식에 대한 액세스를 제한합니다. 이 공급자를 인스턴스화할 때 이 공급자에 대해 만들어진 모든 요청에 대한 기본 경로로 제공하는(및 이 경로 외부의 액세스 제한) 디렉터리 경로와 함께 제공해야 합니다. ASP.NET Core 앱에서 `PhysicalFileProvider` 공급자를 직접 인스턴스화하거나 [종속성 주입](dependency-injection.md)을 통해 컨트롤러 또는 서비스의 생성자에서 `IFileProvider`를 요청할 수 있습니다. 후자의 방법은 일반적으로 보다 유연하고 테스트 가능한 솔루션을 생성합니다.

아래 샘플에서는 `PhysicalFileProvider`를 만드는 방법을 보여 줍니다.


```csharp
IFileProvider provider = new PhysicalFileProvider(applicationRoot);
IDirectoryContents contents = provider.GetDirectoryContents(""); // the applicationRoot contents
IFileInfo fileInfo = provider.GetFileInfo("wwwroot/js/site.js"); // a file under applicationRoot
```

해당 디렉터리 내용을 반복하거나 하위 경로를 제공하여 특정 파일의 정보를 얻을 수 있습니다.

컨트롤러에서 공급자를 요청하려면 컨트롤러의 생성자에서 지정하고 로컬 필드에 할당합니다. 작업 방법 중에서 로컬 인스턴스를 사용합니다.

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Controllers/HomeController.cs?highlight=5,7,12&range=6-19)]

그런 다음, 앱의 `Startup` 클래스에서 공급자를 만듭니다.

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=35,40&range=1-43)]

*Index.cshtml* 보기에서 제공된 `IDirectoryContents`를 반복합니다.

[!code-html[Main](file-providers/sample/src/FileProviderSample/Views/Home/Index.cshtml?highlight=2,7,9,11,15)]

결과:

![물리적 파일 및 폴더를 나열하는 파일 공급자 샘플 응용 프로그램](file-providers/_static/physical-directory-listing.png)

### <a name="embeddedfileprovider"></a>EmbeddedFileProvider

`EmbeddedFileProvider`는 어셈블리에 포함된 파일에 액세스하는 데 사용됩니다. .NET Core에서 *.csproj* 파일의 `<EmbeddedResource>` 요소를 사용하여 어셈블리에 파일을 포함합니다.

[!code-json[Main](file-providers/sample/src/FileProviderSample/FileProviderSample.csproj?range=13-18)]

파일을 어셈블리에 포함하도록 지정할 때 [와일드카드 사용 패턴](#globbing-patterns)을 사용할 수 있습니다. 하나 이상의 파일에 맞게 이러한 패턴을 사용할 수 있습니다.

> [!NOTE]
> 실제로 해당 어셈블리의 프로젝트에 모든 .js 파일을 포함하려고 할 가능성은 낮습니다. 위의 샘플은 데모 목적입니다.

`EmbeddedFileProvider`를 만들 때 읽는 어셈블리를 해당 생성자에 전달합니다.

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

위의 코드 조각은 현재 실행 중인 어셈블리에 대한 액세스로 `EmbeddedFileProvider`를 만드는 방법을 보여 줍니다.

`EmbeddedFileProvider`를 사용하도록 샘플 앱을 업데이트하면 다음 출력과 같은 결과가 발생합니다.

![포함된 파일을 나열하는 파일 공급자 샘플 응용 프로그램](file-providers/_static/embedded-directory-listing.png)

> [!NOTE]
> 포함된 리소스는 디렉터리를 공개하지 않습니다. 대신, 리소스에 대한 경로(해당 네임스페이스를 통해)는 `.` 구분 기호를 사용하여 해당 파일 이름에서 포함됩니다.

> [!TIP]
> `EmbeddedFileProvider` 생성자는 선택적 `baseNamespace` 매개 변수를 허용합니다. 이를 지정하면 `GetDirectoryContents`에 대한 호출을 제공된 네임스페이스 아래의 해당 리소스로 범위를 지정합니다.

### <a name="compositefileprovider"></a>CompositeFileProvider

`CompositeFileProvider`는 여러 공급자에서 파일을 사용하기 위한 단일 인터페이스를 노출하여 `IFileProvider` 인스턴스를 결합합니다. `CompositeFileProvider`를 만들 때 하나 이상의 `IFileProvider` 인스턴스를 해당 생성자에 전달합니다.

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=3&range=35-37)]

이전에 구성된 물리적 및 포함된 공급자 모두를 포함하는 `CompositeFileProvider`를 사용하도록 샘플 앱을 업데이트하면 다음 출력과 같은 결과가 발생합니다.

![물리적 파일 및 폴더와 포함된 파일을 나열하는 파일 공급자 샘플 응용 프로그램](file-providers/_static/composite-directory-listing.png)

## <a name="watching-for-changes"></a>변경 내용 감시

`IFileProvider` `Watch` 메서드는 하나 이상의 파일 또는 디렉터리의 변경 내용을 감시하는 방법을 제공합니다. 이 메서드는 [와일드카드 사용 패턴](#globbing-patterns)을 사용하여 여러 파일을 지정할 수 있는 경로 문자열을 허용하고, `IChangeToken`을 반환합니다. 이 토큰은 조사될 수 있는 `HasChanged` 속성 및 지정된 경로 문자열에 변경 내용이 발견될 때 호출되는 `RegisterChangeCallback` 메서드를 노출합니다. 각 변경 토큰만 단일 변경에 대한 응답으로 연결된 해당 콜백을 호출합니다. 지속적인 모니터링을 활성화하기 위해 아래와 같이 `TaskCompletionSource`를 사용하거나 변경에 대한 응답으로 `IChangeToken` 인스턴스를 다시 만들 수 있습니다.

이 문서 샘플에서 콘솔 응용 프로그램은 텍스트 파일이 수정될 때마다 메시지를 표시하도록 구성됩니다.

[!code-csharp[Main](file-providers/sample/src/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

파일을 여러 번 저장한 후 결과는 다음과 같습니다.

![dotnet 실행을 실행한 후 명령 창은 변경 내용에 대한 quotes.txt 파일을 모니터링하는 응용 프로그램과 파일이 5번 변경된 것을 보여 줍니다.](file-providers/_static/watch-console.png)

> [!NOTE]
> Docker 컨테이너 및 네트워크 공유와 같은 일부 파일 시스템은 안정적으로 변경 알림을 보내지 않을 수도 있습니다. `DOTNET_USE_POLLINGFILEWATCHER` 환경 변수를 `1` 또는 `true`로 설정하여 4초마다 변경 내용에 대한 파일 시스템을 폴링합니다.

## <a name="globbing-patterns"></a>와일드카드 사용 패턴

파일 시스템 경로는 *와일드카드 사용 패턴*이라는 와일드카드 패턴을 사용합니다. 이러한 단순한 패턴은 파일의 그룹을 지정하는 데 사용될 수 있습니다. 두 개의 와일드카드 문자는 `*` 및 `**`입니다.

**`*`**

   현재 폴더 수준의 모든 것 또는 모든 파일 이름 또는 모든 파일 확장명을 일치시킵니다. 일치 항목은 파일 경로에서 `/` 및 `.` 문자로 종료됩니다.

<strong><code>**</code></strong>

   여러 디렉터리 수준에서 모든 것을 일치시킵니다. 디렉터리 계층 구조 내의 여러 파일과 일치시키는 데 재귀적으로 사용될 수 있습니다.

### <a name="globbing-pattern-examples"></a>와일드카드 사용 패턴 예

**`directory/file.txt`**

   특정 디렉터리에 있는 특정 파일을 일치시킵니다.

**<code>directory/*.txt</code>**

   특정 디렉터리에서 `.txt` 확장명으로 모든 파일을 일치시킵니다.

**`directory/*/bower.json`**

   `directory` 디렉터리보다 정확히 한 수준 아래의 디렉터리에서 모든 `bower.json` 파일을 일치시킵니다.

**<code>directory/&#42;&#42;/&#42;.txt</code>**

   `directory` 디렉터리 아래의 모든 곳에서 찾은 모든 파일을 `.txt` 확장명으로 일치시킵니다.

## <a name="file-provider-usage-in-aspnet-core"></a>ASP.NET Core에서 파일 공급자 사용

ASP.NET Core의 여러 부분에서 파일 공급자를 사용합니다. `IHostingEnvironment`는 `IFileProvider` 형식으로 앱의 콘텐츠 루트 및 웹 루트를 노출합니다. 정적 파일 미들웨어는 파일 공급자를 사용하여 정적 파일을 찾습니다. Razor는 보기 찾기에서 `IFileProvider`를 많이 사용합니다. Dotnet의 게시 기능은 파일 공급자 및 와일드카드 사용 패턴을 사용하여 게시되어야 하는 파일을 지정합니다.

## <a name="recommendations-for-use-in-apps"></a>앱에서 사용에 대한 권장 사항

ASP.NET Core 앱에 파일 시스템 액세스가 필요한 경우 종속성 주입을 통해 `IFileProvider`의 인스턴스를 요청한 다음, 이 샘플에 나와 있는 것처럼 해당 메서드를 사용하여 액세스를 수행할 수 있습니다. 이를 통해 앱이 시작하고 앱이 인스턴스화하는 구현 형식의 수를 줄일 때 공급자를 한 번 구성할 수 있습니다.
