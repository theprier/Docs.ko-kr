---
title: Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 앱에 모델 추가
author: rick-anderson
description: Visual Studio Code를 사용하여 ASP.NET Core의 Razor 페이지 앱에 모델을 추가하는 방법을 배웁니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages-vsc/model
ms.openlocfilehash: 20282b491162e9f35e40702655532a78edceb89a
ms.sourcegitcommit: 2ab550f8c46e1a8a5d45e58be44d151c676af256
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2018
---
# <a name="add-a-model-to-an-aspnet-core-razor-pages-app-with-visual-studio-code"></a>Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 앱에 모델 추가

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a>데이터 모델 추가

* *Models* 폴더를 추가합니다.
* *Models* 폴더에 *Movie.cs* 클래스를 추가합니다.
* *Models/Movie.cs* 파일에 다음 코드를 추가합니다.

[!INCLUDE [model 2](../../includes/RP/model2.md)]

[!INCLUDE [model 2a](../../includes/RP/model2a.md)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

프로젝트를 빌드하여 오류가 없는지 확인합니다.

### <a name="entity-framework-core-nuget-packages-for-migrations"></a>마이그레이션을 위한 Entity Framework Core NuGet 패키지

CLI(명령줄 인터페이스)용 EF 도구는 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)에서 제공됩니다. 이 패키지를 설치하려면 *.csproj* 파일의 `DotNetCliToolReference` 컬렉션에 패키지를 추가합니다. **참고:** *.csproj* 파일을 편집하여 이 패키지를 설치해야 합니다. `install-package` 명령이나 패키지 관리자 GUI를 사용할 수 없습니다.

*RazorPagesMovie.csproj* 파일을 편집합니다.

* **파일** > **파일 열기**를 선택한 다음, *RazorPagesMovie.csproj* 파일을 선택합니다.
* `Microsoft.EntityFrameworkCore.Tools.DotNet`에 대한 도구 참조를 두 번째 **\<ItemGroup>** 에 추가합니다.

[!code-xml[](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj)]

[!INCLUDE [model 3](../../includes/RP/model3.md)]

<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>Movie 모델 스캐폴드

* 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.
* 다음 명령을 실행합니다.

**참고: Windows에서는 다음 명령을 실행합니다. MacOS 및 Linux의 경우 다음 명령 참조**

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* MacOS 및 Linux에서는 다음 명령을 실행합니다.

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

오류가 표시될 경우:
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

Visual Studio를 종료하고 명령을 다시 실행합니다.

[!INCLUDE [model 4](../../includes/RP/model4.md)]

다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.

> [!div class="step-by-step"]
> [이전: 시작](xref:tutorials/razor-pages-vsc/razor-pages-start)
> [다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages-vsc/page)
