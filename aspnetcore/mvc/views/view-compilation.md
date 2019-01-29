---
title: ASP.NET Core에서 Razor 파일 컴파일 및 미리 컴파일
author: rick-anderson
description: Razor 파일을 미리 컴파일할 경우의 이점과 ASP.NET Core 앱에서 Razor 파일 미리 컴파일을 구현하는 방법에 대해 알아보세요.
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 01/23/2019
uid: mvc/views/view-compilation
ms.openlocfilehash: 2720708f8e58fdc55b82bfb56665005170e79934
ms.sourcegitcommit: d5223cf6a2cf80b4f5dc54169b0e376d493d2d3a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54889758"
---
# <a name="razor-file-compilation-in-aspnet-core"></a>ASP.NET Core의 Razor 파일 컴파일

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

::: moniker range="= aspnetcore-1.1"

Razor 파일은 런타임 시 관련 MVC 뷰가 호출되면 컴파일됩니다. 빌드 시 Razor 파일 게시는 지원되지 않습니다. Razor 파일은 필요에 따라 미리 컴파일 도구를 사용하여 앱 게시 및 배포 시 컴파일될 수 있습니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

Razor 파일은 런타임 시 관련 Razor 페이지 또는 MVC 뷰가 호출되면 컴파일됩니다. 빌드 시 Razor 파일 게시는 지원되지 않습니다. Razor 파일은 필요에 따라 미리 컴파일 도구를 사용하여 앱 게시 및 배포 시 컴파일될 수 있습니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

Razor 파일은 런타임 시 관련 Razor 페이지 또는 MVC 뷰가 호출되면 컴파일됩니다. Razor 파일은 [Razor SDK](xref:razor-pages/sdk)를 사용하여 빌드 및 게시 시 컴파일됩니다.

::: moniker-end

## <a name="precompilation-considerations"></a>미리 컴파일 고려 사항

다음은 Razor 파일을 미리 컴파일할 경우의 부작용입니다.

* 더 작게 게시되는 번들
* 더 빠른 시작 시간
* 게시된 번들에 연관 콘텐츠가 없기 때문에 Razor 파일을 편집할 수 없습니다.

## <a name="deploy-precompiled-files"></a>미리 컴파일된 파일 배포

::: moniker range=">= aspnetcore-2.1"

Razor 파일의 빌드 및 게시 시점 컴파일은 Razor SDK에서 기본적으로 사용하도록 설정됩니다. 업데이트된 후에 Razor 파일을 편집하는 작업은 빌드 시 지원됩니다. 기본적으로 컴파일된 *Views.dll*만이 앱과 함께 배포되고 *cshtml* 파일은 배포되지 않습니다.

> [!IMPORTANT]
> 미리 컴파일 도구는 ASP.NET Core 3.0에서 제거됩니다. [Razor Sdk](xref:razor-pages/sdk)로 마이그레이션하는 것이 좋습니다.
>
> Razor SDK는 미리 컴파일 특정 속성이 프로젝트 파일에서 설정되지 않은 경우에만 유효합니다. 예를 들어 *.csproj* 파일의 `MvcRazorCompileOnPublish` 속성을 `true`로 설정하면 Razor SDK가 비활성화됩니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

프로젝트가 .NET Framework를 대상으로 하는 경우 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 패키지를 설치하세요.

[!code-xml[](view-compilation/sample/DotNetFrameworkProject.csproj?name=snippet_ViewCompilationPackage)]

프로젝트가 .NET Core를 대상으로 하는 경우 변경 작업이 필요하지 않습니다.

ASP.NET Core 2.x 프로젝트 템플릿은 기본적으로 `MvcRazorCompileOnPublish` 속성을 암시적으로 `true`로 설정합니다. 다라서 이 요소는 *.csproj* 파일에서 안전하게 제거할 수 있습니다.

> [!IMPORTANT]
> 미리 컴파일 도구는 ASP.NET Core 3.0에서 제거됩니다. [Razor Sdk](xref:razor-pages/sdk)로 마이그레이션하는 것이 좋습니다.
>
> ASP.NET Core 2.0에서 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)를 수행하는 경우 Razor 파일 미리 컴파일은 사용 불가능합니다.

::: moniker-end

::: moniker range="= aspnetcore-1.1"

`MvcRazorCompileOnPublish` 속성을 `true`로 설정하고 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 패키지를 설치하세요. 다음 *.csproj* 샘플은 이러한 설정을 강조 표시합니다.

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=4,10)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[.NET Core CLI 게시 명령](/dotnet/core/tools/dotnet-publish)을 사용하여 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)에 대한 앱을 준비합니다. 예를 들어 프로젝트 루트에서 다음 명령을 실행합니다.

```console
dotnet publish -c Release
```

미리 컴파일에 성공하면 컴파일된 Razor 파일이 포함된 *<project_name>.PrecompiledViews.dll* 파일이 생성됩니다. 예를 들어 아래 스크린샷은 *WebApplication1.PrecompiledViews.dll* 내부에서 *Index.cshtml*의 내용을 보여 줍니다.

![DLL 내에서 Razor 뷰](view-compilation/_static/razor-views-in-dll.png)

::: moniker-end

## <a name="recompile-razor-files-on-change"></a>변경 시 Razor 파일 다시 컴파일

<xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions> `AllowRecompilingViewsOnFileChange`는 디스크의 파일이 변경되면 Razor 파일(Razor 뷰 및 Razor Pages)이 컴파일되고 업데이트되는지 여부를 결정하는 값을 가져오거나 설정합니다.

`true`로 설정하면 [IFileProvider.Watch](xref:Microsoft.Extensions.FileProviders.IFileProvider.Watch*)는 구성된 <xref:Microsoft.Extensions.FileProviders.IFileProvider> 인스턴스에서 Razor 파일의 변경 내용을 감시합니다.

다음의 경우 기본값은 `true`입니다.

* ASP.NET Core 2.1 또는 이전 버전의 앱.
* 개발 환경의 ASP.NET Core 2.2 이상의 앱.

`AllowRecompilingViewsOnFileChange`는 호환성 스위치와 연결되어 있으며 앱에 대해 구성된 호환성 버전에 따라 다른 동작을 제공할 수 있습니다. `AllowRecompilingViewsOnFileChange`를 설정하여 앱을 구성하면 앱의 호환성 버전에 의해 암시된 값보다 우선 순위가 높습니다.

앱의 호환성 버전이 <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1> 또는 이전 버전으로 설정된 경우 명시적으로 구성하지 않는 한 `AllowRecompilingViewsOnFileChange`는 `true`로 설정됩니다.

앱의 호환성 버전이 `CompatibilityVersion.Version_2_2` 이상으로 설정된 경우 환경이 개발이 아니거나 값이 명시적으로 구성되지 않은 경우 `AllowRecompilingViewsOnFileChange`가 `false`로 설정됩니다.

앱의 호환성 버전 설정에 대한 지침과 예는 <xref:mvc/compatibility-version>을 참조하세요.

## <a name="additional-resources"></a>추가 자료

::: moniker range="= aspnetcore-1.1"

* <xref:mvc/views/overview>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>
* <xref:razor-pages/sdk>

::: moniker-end
