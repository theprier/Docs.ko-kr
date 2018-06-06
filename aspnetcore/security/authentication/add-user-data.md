---
title: 추가, 다운로드 및 ASP.NET Core 프로젝트에서 Id에 사용자 지정 사용자 데이터를 삭제 합니다.
author: rick-anderson
description: ASP.NET Core 프로젝트에 사용자 지정 사용자 데이터 Id로 추가 하는 방법에 알아봅니다. GDPR 당 데이터를 삭제 합니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 6/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/add-user-data
ms.openlocfilehash: 23fd792c0d93c038f31ce947e7885ad6e36d119e
ms.sourcegitcommit: d4cefc0c63550c64a8040b11867cc05efcfb7e86
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34758777"
---
# <a name="add-download-and-delete-custom-user-data-to-identity-in-an-aspnet-core-project"></a>추가, 다운로드 및 ASP.NET Core 프로젝트에서 Id에 사용자 지정 사용자 데이터를 삭제 합니다.

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 문서에서는 설명 하는 방법:

* ASP.NET Core 웹 앱에 사용자 지정 사용자 데이터를 추가 합니다.
* 사용 하 여 사용자 지정 데이터 모델을 데코레이팅하는 [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) 자동으로 다운로드 및 삭제에 사용할 수 있도록 특성입니다. 충족 사용 하 여 데이터를 다운로드 하 고 삭제할 수 [GDPR](xref:security/gdpr) 요구 사항입니다.

Razor 페이지 웹 앱에서 프로젝트 샘플 만들어지지만 ASP.NET Core MVC 웹 응용 프로그램에 대 한 지침 비슷합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="prerequisites"></a>전제 조건

[!INCLUDE [](~/includes/2.1-SDK.md)]

## <a name="create-a-razor-web-app"></a>Razor 웹앱 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다. 프로젝트 이름을 **WebApp1** 를 원하는 경우의 네임 스페이스와 일치는 [샘플 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) 코드입니다.
* 선택 **ASP.NET Core 웹 응용 프로그램** > **확인**
* 선택 **ASP.NET Core 2.1** 드롭다운에
* 선택 **웹 응용 프로그램**  > **확인**
* 프로젝트를 빌드하고 실행합니다.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```cli
dotnet new webapp -o WebApp1
```

------

## <a name="run-the-identity-scaffolder"></a>Identity scaffolder 실행

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 > **추가** > **스 캐 폴드 된 새 항목**합니다.
* 왼쪽된 창에서는 **추가 스 캐 폴드** 대화 상자에서 **Identity** > **추가**합니다.
* 에 **추가 Identity** 대화 상자에서 다음 옵션:
  * 기존 레이아웃 파일을 선택 *~/Pages/Shared/_Layout.cshtml*
  * 재정의 하려면 다음 파일을 선택 합니다.
    * **계정/레지스터**
    * **계정/관리/인덱스**
  * 선택 된 **+** 단추를 새 **데이터 컨텍스트 클래스가**합니다. 형식을 사용할 수 (**WebApp1.Models.WebApp1Context** 프로젝트의 이름을 **WebApp1**).
  * 선택 된 **+** 단추를 새 **사용자 클래스**합니다. 형식을 사용할 수 (**WebApp1User** 프로젝트의 이름을 **WebApp1**) > **추가**합니다.
* 선택 **추가**합니다.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

ASP.NET scaffolder 이전에 설치 하지 않은 경우 지금 설치 합니다.

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

에 대 한 패키지 참조 추가 [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) 프로젝트 (.csproj) 파일입니다. 프로젝트 디렉터리에서 다음 명령을 실행 합니다.

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

Identity scaffolder 옵션을 나열 하려면 다음 명령을 실행 합니다.

```cli
dotnet aspnet-codegenerator identity -h
```

프로젝트 폴더에 Identity scaffolder를 실행 합니다.

```cli
dotnet aspnet-codegenerator identity -u WebApp1User -fi Account.Register;Account.Manage.Index
```

-------------

지침에 따라 [마이그레이션, UseAuthentication, 및 레이아웃](xref:security/authentication/scaffold-identity#efm) 다음 단계를 수행 하려면:

* 마이그레이션 만들고 데이터베이스를 업데이트 합니다.
* `UseAuthentication`를 `Startup.Configure`에 추가합니다.
* 추가 `<partial name="_LoginPartial" />` 레이아웃 파일.
* 앱을 테스트합니다.
  * 사용자 등록
  * 새 사용자 이름 선택 (옆에 **로그 아웃** 링크)입니다. 창이 확장 또는 사용자 이름 및 다른 링크 표시 하려면 탐색 모음의 아이콘을 선택 해야 합니다.
  * 선택 된 **개인 데이터** 탭 합니다.
  * 선택 된 **다운로드** 단추 및 검사는 *PersonalData.json* 파일입니다.
  * 테스트는 **삭제** 단추를 사용자에 로그인을 삭제 합니다.

## <a name="add-custom-user-data-to-the-identity-db"></a>Identity db 사용자 지정 사용자 데이터를 추가 합니다.

업데이트는 `IdentityUser` 사용자 지정 속성을 사용 하 여 클래스를 파생 합니다. 파일의 이름은 프로젝트 WebApp1 명명 *Areas/Identity/Data/WebApp1User.cs*합니다. 다음 코드는 파일을 업데이트 합니다.

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Data/WebApp1User.cs)]

속성으로 데코레이팅되 어는 [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) 특성:

* 때 삭제 됩니다는 *Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* Razor 페이지 호출 `UserManager.Delete`합니다.
* 다운로드 한 데이터에 포함 된 *Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* Razor 페이지.

### <a name="update-the-accountmanageindexcshtml-page"></a>업데이트 Account/Manage/Index.cshtml 페이지

업데이트는 `InputModel` 에 *Areas/Identity/Pages/Account/Manage/Index.cshtml.cs* 를 다음으로 코드를 강조 표시 합니다.

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml.cs?name=snippet&highlight=28-36,63-64,87-95)]

업데이트는 *Areas/Identity/Pages/Account/Manage/Index.cshtml* 강조 표시 된 다음 태그로:

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml?highlight=34-41)]

### <a name="update-the-accountregistercshtml-page"></a>업데이트 Account/Register.cshtml 페이지

업데이트는 `InputModel` 에 *Areas/Identity/Pages/Account/Register.cshtml.cs* 를 다음으로 코드를 강조 표시 합니다.

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml.cs?name=snippet&highlight=8-16,43,44)]

업데이트는 *Areas/Identity/Pages/Account/Register.cshtml* 강조 표시 된 다음 태그로:

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml?highlight=16-25)]

프로젝트를 빌드합니다.

### <a name="add-a-migration-for-the-custom-user-data"></a>추가 사용자 지정 사용자 데이터에 대 한 마이그레이션

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Visual Studio에서 **패키지 관리자 콘솔**:

```PMC
Add-Migration CustomUserData
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```cli
dotnet ef migrations add CustomUserData
dotnet ef database update
```

------

## <a name="test-create-view-download-delete-custom-user-data"></a>테스트 만들기, 보기, 다운로드, 사용자 지정 사용자 데이터를 삭제 합니다.

앱을 테스트합니다.

* 새 사용자를 등록 합니다.
* 사용자 지정 사용자 데이터를 표시는 `/Identity/Account/Manage` 페이지.
* 다운로드 하 고 사용자 개인 데이터를 볼는 `/Identity/Account/Manage/PersonalData` 페이지.