---
title: ASP.NET Core Razor SDK
author: Rick-Anderson
description: ASP.NET Core의 Razor 페이지를 통해 MVC를 사용하는 것보다 더 쉽고 더 생산적으로 코딩 페이지에 초점을 맞춘 시나리오를 만드는 방법을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 4/12/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: mvc/razor-pages/sdk
ms.openlocfilehash: 2cbebb12ccd1098e1950aa7eeb22fab4ffc689e6
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="aspnet-core-razor-sdk"></a>ASP.NET Core Razor SDK

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE[](~/includes/2.1.md)]

[!INCLUDE[](~/includes/2.1-SDK.md)]에는 `Microsoft.NET.Sdk.Razor` MSBuild SDK(Razor SDK)가 포함되어 있습니다. Razor SDK:

* ASP.NET Core MVC 기반 프로젝트용 [Razor](xref:mvc/views/razor) 파일을 포함하는 프로젝트의 빌드, 패키징 및 게시와 관련된 환경을 표준화합니다.
* Razor 파일 컴파일의 사용자 지정을 허용하는 사전 정의된 대상, 속성 및 항목 집합이 포함됩니다.

## <a name="prerequisites"></a>전제 조건

[!INCLUDE[](~/includes/2.1-SDK.md)]

## <a name="using-the-razor-sdk"></a>Razor SDK 사용

대부분의 웹앱은 Razor SDK를 명시적으로 참조할 필요가 없습니다. 

Razor SDK를 사용하여 Razor 보기 또는 Razor 페이지를 포함하는 클래스 라이브러리를 빌드하려면:

* `Microsoft.NET.Sdk` 대신 `Microsoft.NET.Sdk.Razor`를 사용합니다.
```xml
<Project SDK="Microsoft.NET.Sdk.Razor">
  ...
</Project>
```

* 일반적으로 Razor 페이지 및 Razor 보기를 빌드하고 컴파일하는 데 필요한 추가 종속성을 가져오려면 `Microsoft.AspNetCore.Mvc`에 대한 패키지 참조가 필요합니다. 최소한 프로젝트는 다음에 패키지 참조를 추가해야 합니다.

    * `Microsoft.AspNetCore.Razor.Design` 
    * `Microsoft.AspNetCore.Mvc.Razor.Extensions`
    
 이전 패키지는 `Microsoft.AspNetCore.Mvc`에 포함되어 있습니다. 다음 표시에서는 Razor SDK를 사용하여 ASP.NET Core Razor 페이지 앱용 Razor 파일을 빌드하는 기본 *.csproj* 파일을 보여 줍니다.
    
 [!code-xml[Main](sdk/sample/RazorSDK.csproj)]

### <a name="properties"></a>속성

다음 속성은 Razor의 SDK 동작을 프로젝트 빌드의 일부로 제어합니다.

* `RazorCompileOnBuild`: `true`인 경우, 프로젝트 빌드 중에 Razor 어셈블리를 컴파일하고 내보냅니다. 기본값은 `true`입니다.
* `RazorCompileOnPublish`: `true`인 경우, 프로젝트 게시 중에 Razor 어셈블리를 컴파일하고 내보냅니다. 기본값은 `true`입니다.

다음 속성 및 항목은 Razor SDK에 대한 입력 및 출력을 구성하는 데 사용됩니다.

| 항목                                         | 설명                                                                   |
| ------------                                  | -------------                                                                 |
| RazorGenerate                                 | 코드 생성 대상에 입력되는 항목 요소(*.cshtml* 파일). |
| RazorCompile                                  | Razor 컴파일 대상에 입력되는 항목 요소(.cs 파일). 이 ItemGroup을 사용하여 Razor 어셈블리에 컴파일할 추가 파일을 지정합니다. |
| RazorAssemblyAttribute                        | 코드에 사용된 항목 요소는 Razor 어셈블리의 특성을 생성합니다. 예:  <br />`<RazorAssemblyAttribute ` <br />  `Include="System.Reflection.AssemblyMetadataAttribute"`<br />`  _Parameter1="BuildSource" _Parameter2="https://docs.asp.net/">` |
| RazorEmbeddedResource                         | 생성된 Razor 어셈블리에 포함 리소스로 추가된 항목 요소 |

| 속성                                      | 설명                                                                   |
| ------------                                  | -------------                                                                 |
| RazorTargetName                               | Razor에서 생성한 어셈블리의 파일 이름(확장명 제외). | 
| RazorOutputPath                               | Razor 출력 디렉터리.                                      |
| RazorCompileToolset                           | Razor 어셈블리를 빌드하는 데 사용되는 도구 집합을 결정하는 데 사용됩니다. 유효한 값은 `Implicit` 및 `PrecompilationTool`입니다. |
| EnableDefaultContentItems                     | `true`인 경우, *.cshtml* 파일과 같은 특정 파일 형식이 프로젝트의 콘텐츠로 포함됩니다. Microsoft.NET.Sdk.Web을 통해 참조하면 *wwwroot* 및 구성 파일에 있는 모든 파일도 포함됩니다.         |
| EnableDefaultRazorGenerateItems               | `true`인 경우, `RazorGenerate` 항목의 `Content` 항목에서 *.cshtml* 파일을 포함합니다. |
| GenerateRazorTargetAssemblyInfo               | `true`인 경우, `RazorAssemblyAttribute`로 지정된 특성을 포함하는 *.cs* 파일을 생성하고 이를 컴파일 출력에 포함시킵니다. |
| EnableDefaultRazorTargetAssemblyInfoAttributes | `true`인 경우, `RazorAssemblyAttribute`에 어셈블리 특성의 기본 집합을 추가합니다. |
| CopyRazorGenerateFilesToPublishDirectory       | `true`인 경우, RazorGenerate 항목(*.cshtml*) 파일을 게시 디렉터리에 복사합니다. 일반적으로 Razor 파일은 빌드 시간 또는 게시 시간에 컴파일에 참여하는 경우 게시된 응용 프로그램에 필요하지 않습니다. 기본값은 `false`입니다. |
| CopyRefAssembliesToPublishDirectory            | `true`인 경우, 참조 어셈블리 항목을 게시 디렉터리에 복사합니다. 일반적으로 참조 어셈블리는 Razor 컴파일이 빌드 시간 또는 게시 시간에 발생하는 경우 게시된 응용 프로그램에 필요하지 않습니다. 게시된 응용 프로그램에 런타임 컴파일이 필요한 경우(예: 런타임에 cshtml 파일을 수정하거나 포함된 보기를 사용하는 경우) `true`로 설정합니다. 기본값은 `false`입니다. |
| IncludeRazorContentInPack                      | `true`인 경우, 모든 Razor 콘텐츠 항목(*.cshtml* 파일)은 생성된 NuGet 패키지에 포함되도록 표시됩니다. 기본값은 `false`입니다. |
| EmbedRazorGenerateSources | `true`인 경우, 생성된 Razor 어셈블리에 포함된 파일로 RazorGenerate(*.cshtml*) 항목을 추가합니다. 기본값은 `false`입니다. |
| UseRazorBuildServer                           | `true`인 경우, 영구적 빌드 서버 프로세스를 사용하여 코드 생성 작업을 오프로드합니다. 기본값은 `UseSharedCompilation`입니다. |

### <a name="targets"></a>대상
Razor SDK는 두 기본 대상을 정의합니다.

* `RazorGenerate` - 코드는 RazorGenerate 항목 요소에서 *.cs* 파일을 생성합니다. 이 대상 전후에 실행할 수 있는 추가 대상을 지정하려면 `RazorGenerateDependsOn` 속성을 사용합니다.
* `RazorCompile` - 생성된 *.cs* 파일을 Razor 어셈블리로 컴파일합니다. 이 대상 전후에 실행할 수 있는 추가 대상을 지정하려면 `RazorCompileDependsOn`을 사용합니다.