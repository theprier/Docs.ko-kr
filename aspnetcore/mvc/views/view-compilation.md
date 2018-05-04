---
title: ASP.NET Core에서 Razor 뷰 컴파일 및 미리 컴파일
author: rick-anderson
description: ASP.NET Core 앱에서 MVC Razor 뷰 컴파일 및 미리 컴파일을 사용하도록 설정하는 방법에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 12/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/view-compilation
ms.openlocfilehash: 5d971645106a79497a9902063c7774dc6d546395
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="razor-view-compilation-and-precompilation-in-aspnet-core"></a>ASP.NET Core에서 Razor 뷰 컴파일 및 미리 컴파일

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

Razor 뷰는 뷰를 호출할 때 런타임에서 컴파일됩니다. ASP.NET Core 1.1.0 이상에서는 필요에 따라 Razor 뷰를 컴파일하고 앱(미리 컴파일로 알려진 프로세스)을 통해 배포할 수 있습니다. ASP.NET Core 2.x 프로젝트 템플릿에는 기본적으로 미리 컴파일을 사용할 수 있도록 설정되어 있습니다.

> [!IMPORTANT]
> ASP.NET Core 2.0에서 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)를 수행하는 경우 Razor 뷰 미리 컴파일은 현재 사용 불가능합니다. 이 기능은 2.1이 릴리스되면 SCD에 사용 가능합니다. 자세한 내용은 [Windows의 Linux에 대해 교차 컴파일 시 뷰 컴파일 실패](https://github.com/aspnet/MvcPrecompilation/issues/102)를 참조하세요.

미리 컴파일 고려 사항:

* 뷰를 미리 컴파일하면 게시된 번들 크기는 작아지고 시작 시간은 빨라집니다.
* 뷰를 미리 컴파일한 후에는 Razor 파일을 편집할 수 없습니다. 편집된 뷰는 게시된 번들에 표시되지 않습니다. 

미리 컴파일된 뷰를 배포하려면

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
프로젝트가 .NET Framework를 대상으로 하는 경우 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/)에 대한 패키지 참조를 포함시킵니다.

```xml
<PackageReference Include="Microsoft.AspNetCore.Mvc.Razor.ViewCompilation" Version="2.0.0" PrivateAssets="All" />
```

프로젝트가 .NET Core를 대상으로 하는 경우 변경 작업이 필요하지 않습니다.

ASP.NET Core 2.x 프로젝트 템플릿은 기본적으로 `MvcRazorCompileOnPublish`를 `true`로 암시적으로 설정하므로 이 노드를 *.csproj* 파일에서 안전하게 제거할 수 있습니다. 명시적인 방법을 선호하는 경우 `MvcRazorCompileOnPublish` 속성을 `true`로 설정하는 데 아무런 문제가 없습니다. 다음 *.csproj* 샘플은 이 설정을 강조 표시합니다.

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish2.csproj?highlight=5)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
`MvcRazorCompileOnPublish`를 `true`로 설정하고 `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`에 대한 패키지 참조를 포함시킵니다. 다음 *.csproj* 샘플은 이러한 설정을 강조 표시합니다.

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=5,12)]

[.NET Core CLI 게시 명령](/dotnet/core/tools/dotnet-publish)을 사용하여 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)에 대한 앱을 준비합니다. 예를 들어 프로젝트 루트에서 다음 명령을 실행합니다.

```console
dotnet publish -c Release
```

미리 컴파일에 성공하면 컴파일된 Razor 뷰가 포함된 *<project_name>.PrecompiledViews.dll* 파일이 생성됩니다. 예를 들어 아래 스크린샷은 *WebApplication1.PrecompiledViews.dll* 내부에서 *Index.cshtml*의 내용을 보여 줍니다.

![DLL 내에서 Razor 뷰](view-compilation/_static/razor-views-in-dll.png)
