---
title: Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 앱에 모델 추가
author: rick-anderson
description: Visual Studio Code를 사용하여 ASP.NET Core의 Razor 페이지 앱에 모델을 추가하는 방법을 배웁니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
uid: tutorials/razor-pages-vsc/model
ms.openlocfilehash: c4aef369bb3965b70d1b461cf63e6f5a26a00628
ms.sourcegitcommit: c43a6f1fe72d7c2db4b5815fd532f2b45d964e07
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244725"
---
# <a name="add-a-model-to-an-aspnet-core-razor-pages-app-with-visual-studio-code"></a>Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 앱에 모델 추가

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a>데이터 모델 추가

* *Models* 폴더를 추가합니다.
* *Models* 폴더에 *Movie.cs* 클래스를 추가합니다.
* *Models/Movie.cs* 파일에 다음 코드를 추가합니다.

[!INCLUDE [model 2](../../includes/RP/model2.md)]

[!INCLUDE [model 2a](../../includes/RP/model2a.md)]

### <a name="entity-framework-core-nuget-package-for-sqlite"></a>SQLite를 위한 Entity Framework Core NuGet 패키지

명령줄에서 다음 .NET Core CLI 명령을 실행합니다.

```console
dotnet add package Microsoft.EntityFrameworkCore.SQLite
```

<a name="reg"></a>

### <a name="register-the-database-context"></a>데이터베이스 컨텍스트 등록

*Startup.cs* 파일에서 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 데이터베이스 컨텍스트를 등록합니다.

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=10-11)]

*Startup.cs* 맨 위에 다음 `using` 문을 추가합니다.

```csharp
using RazorPagesMovie.Models;
using Microsoft.EntityFrameworkCore;
```

프로젝트를 빌드하여 오류가 없는지 확인합니다.

[!INCLUDE [model 3](../../includes/RP/model3.md)]

<a name="scaffold"></a>

### <a name="scaffold-the-movie-model"></a>Movie 모델 스캐폴드

* 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.
* **Windows**: 다음 명령을 실행합니다.

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* **macOS 및 Linux**: 다음 명령을 실행합니다.

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

[!INCLUDE [model 4](../../includes/RP/model4.md)]

다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.

> [!div class="step-by-step"]
> [이전: 시작](xref:tutorials/razor-pages-vsc/razor-pages-start)
> [다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages-vsc/page)
