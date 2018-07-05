---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: 프로젝트 속성 구성-4/12 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: 4aa1e55f21e74ae8da67d6d13c35a8de5693ec3a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396273"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: 프로젝트 속성 구성-4/12
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

일부 배포 옵션은 프로젝트 파일에 저장 된 프로젝트 속성에서 구성 (합니다 *.csproj* 하거나 *.vbproj* 파일). 대부분의 경우에서 이러한 설정의 기본값은 원하는 항목을 사용할 수 있지만 합니다 **프로젝트 속성** UI 변경 해야 할 경우 이러한 설정을 사용 하려면 Visual Studio에 기본 제공 합니다. 이 자습서에서 배포 설정을 검토 **프로젝트 속성**합니다. 배포할 빈 폴더는 자리 표시자 파일을 만들 수도 있습니다.

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>프로젝트 속성 창에서 배포 설정 구성

다음 자습서에서 살펴보겠지만 배포 과정에 영향을 주는 대부분의 설정은 게시 프로필에 포함 됩니다. 알고 있어야 하는 몇 가지 설정은 합니다 **패키지 및 게시** 탭의 **프로젝트 속성** 창. 이러한 설정은 각 빌드 구성에 대해 지정 된-즉, 디버그 빌드에 대 한 보다 릴리스 빌드에 대 한 다른 설정이 있을 수 있습니다.

**솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 합니다 **ContosoUniversity** 프로젝트를 선택 **속성**를 선택한 후는 **웹 패키지 및 게시**탭 합니다.

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

창이 표시 되 면 기본적으로 솔루션에 대 한 현재 빌드 구성에 대 한 설정을 보여 줍니다. 경우는 **구성** 상자를 나타내지 않습니다 **(릴리스) 활성**를 선택 **릴리스** 릴리스 빌드 구성에 대 한 설정을 표시 하기 위해. 테스트 및 프로덕션 환경에 릴리스 빌드를 배포 합니다.

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

사용 하 여 **(릴리스) 활성** 또는 **릴리스** 릴리스 빌드 구성을 사용 하 여 배포할 때 적용 되는 값이 표시를 선택 합니다.

- 에 **배포할 항목** 상자에서 **응용 프로그램을 실행 하는 데 필요한 파일만** 선택 합니다. 다른 옵션은 **이 프로젝트의 모든 파일** 하거나 **이 프로젝트 폴더의 모든 파일**합니다. 변경 하지 않고 기본 선택 하지 않고 소스 코드 파일을 예를 들어 배포 하지 마십시오. 이 설정은 SQL Server Compact 이진 파일이 포함 된 폴더를 프로젝트에 포함 해야 하는 이유는 무엇 때문입니다. 이 설정에 대 한 자세한 내용은 참조 하세요. **이유는 없는 프로젝트 폴더 내에 있는 파일의 모든 배포?** 에 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)합니다.
- **디버그 기호 생성 제외** 을 선택 합니다. 이 빌드 구성을 사용 하면 디버깅 수 없습니다.
- **앱에서 파일 제외\_데이터 폴더** 선택 하지 않으면. 멤버 자격 데이터베이스에 대 한 SQL Server Compact 파일을 해당 폴더 및 배포 해야 합니다. 데이터베이스 변경 내용을 포함 하지 않는 업데이트를 배포할 때이 확인란을 선택 합니다.
- **게시 하기 전에이 응용 프로그램을 미리 컴파일할** 선택 하지 않으면. 대부분의 시나리오에서 웹 응용 프로그램 프로젝트 미리 컴파일할 필요가 없습니다 있습니다. 이 옵션에 대 한 자세한 내용은 참조 하세요. [웹 패키지 및 게시 탭, 프로젝트 속성](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx) 하 고 [미리 컴파일 설정 대화 상자 고급](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx)합니다.
- **SQL 패키지 및 게시 탭에서 구성 하는 모든 데이터베이스가 포함 됩니다** 을 선택 하면이 옵션은 효과가 없습니다 이제 구성 되지 때문에 있지만 합니다 **SQL 패키지 및 게시** 탭 합니다. 해당 탭은 SQL Server 데이터베이스를 배포 하기 위한 유일한 옵션 이어야 하는 데 사용 하는 레거시 데이터베이스 배포 방법입니다. 사용 하 여 합니다 **SQL 패키지 및 게시** 탭에 [SQL Server로 마이그레이션](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) 자습서입니다.
- 합니다 **Web Deployment 패키지 설정** 원클릭을 사용 중 이므로 섹션이 적용 되지 않습니다이 자습서에서 게시 합니다.

변경 된 **구성** 디버그 빌드에 대 한 기본 설정을 보려면 디버그 드롭다운 목록 상자입니다. 값을 제외 하 고는 동일 **생성 된 디버그 기호 제외** 디버그 빌드를 배포 하는 경우 디버깅할 수 있도록 지워집니다.

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>Elmah 폴더 배포는 물론 만들기

이전 자습서에서 보았듯이 합니다 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 오류 로깅 및 보고 기능을 제공 합니다. Contoso University 응용 프로그램에서 Elmah를 구성한 라는 폴더에 오류 세부 정보를 저장할 *Elmah*:

![Elmah 폴더](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

배포에서 특정 파일 또는 폴더를 제외 하는 것은 일반적인 요구 사항; 또 다른 예로 사용자가 파일을 업로드할 수 있는 폴더 것입니다. 프로덕션에 배포 하도록 개발 환경에서 생성 된 파일을 업로드 하거나 로그 파일 하지 있습니다. 프로덕션에 업데이트를 배포 하는 사용 하지 않으려면 프로덕션에 있는 파일을 삭제 하는 배포 프로세스를 (어떻게 파일이 있으면 원본 사이트가 아닌 대상 사이트에 배포할 때 배포 옵션을 설정에 따라 웹 배포에서 삭제 대상입니다.)

이 자습서의 앞부분에서 본 것 처럼를 **배포할 항목** 옵션을 **웹 패키지 및 게시** 탭으로 설정 됩니다 **만이 응용 프로그램을 실행 하는 데 필요한 파일이**. 결과적으로, 개발에서 Elmah에서 만든 로그 파일 배포 되지 않습니다가 원하는 발생 합니다. (배포 해야 하는 것이 프로젝트에 포함 될 및 해당 **빌드 작업** 속성으로 설정 해야 **콘텐츠**합니다. 자세한 내용은 **이유는 없는 프로젝트 폴더 내에 있는 파일의 모든 배포?** 에 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)). 그러나 웹 배포 하지 폴더가 만들어집니다 대상 사이트에서 하나 이상의 파일을 복사할 경우를 제외 합니다. 따라서 추가할를 *.txt* 폴더를 복사할 수 있도록 자리 표시자 역할을 폴더에 파일을 합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *Elmah* 폴더를 선택 **새 항목 추가**, 라는 파일을 만듭니다 *Placeholder.txt*합니다. 여기에 다음 텍스트를 넣을: "This is 자리 표시자 파일을 폴더 배포를 확인 합니다." 파일을 저장 합니다. 이것이 전부는 Visual Studio 때문에이 파일 및 폴더, 것을 배포 하는지 확인 하기 위해 수행 해야 합니다 **빌드 작업** 속성을 *.txt* 파일 설정 되어 **콘텐츠**기본적으로 합니다.

이제 배포 설정 작업을 모두 완료 했습니다. 다음 자습서에서는 테스트 환경에는 Contoso University 사이트를 배포 하 고 테스트 합니다 됩니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
