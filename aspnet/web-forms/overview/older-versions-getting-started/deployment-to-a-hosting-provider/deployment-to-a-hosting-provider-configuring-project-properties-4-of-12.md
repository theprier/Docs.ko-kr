---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 프로젝트 속성 구성-4/12 | Microsoft Docs'
author: tdykstra
description: 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: b8352c1832ffc79db93b6324dd673afaff6b0d74
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 프로젝트 속성 구성-4/12
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. 웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다. 계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능을 표시, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Azure 앱 서비스 웹 앱을 배포 하는 방법을 보여 줍니다. 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.


## <a name="overview"></a>개요

일부 배포 옵션은 프로젝트 파일에 저장 된 프로젝트 속성에서 구성 (의 *.csproj* 또는 *.vbproj* 파일). 대부분의 경우에서 이러한 설정의 기본값은 원하는 하지만 사용할 수 있습니다는 **프로젝트 속성** UI를 변경할 수 있는 경우 이러한 설정으로 작동 하도록 Visual Studio에 빌드됩니다. 이 자습서에서 배포 설정을 검토 **프로젝트 속성**합니다. 배포할 빈 폴더는 자리 표시자 파일을 만들 수도 있습니다.

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>프로젝트 속성 창에서 배포 설정 구성

배포 하는 동안 수행 되는 작업에 영향을 주는 대부분의 설정은 다음과 같은 자습서에서 확인할 수 게시 프로필에 포함 됩니다. 알고 있어야 하는 몇 가지 설정에는 **패키지/게시** 의 탭에서 **프로젝트 속성** 창. 이러한 설정은 각 빌드 구성에 대해 지정 되어-즉, 디버그 빌드에 있는 것 보다 릴리스 빌드에 대 한 다른 설정을 사용할 수 있습니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **ContosoUniversity** 프로젝트를 **속성**를 선택한 후는 **웹패키지/게시**탭 합니다.

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

창이 표시 되 면 기본적으로 솔루션에 대 한 현재 활성 나오든 이들 빌드 구성에 대 한 설정을 보여 줍니다. 경우는 **구성** 상자를 나타내지 않습니다 **활성 (Release)**선택, **릴리스** 릴리스 빌드 구성에 대 한 설정을 표시 하려면. 테스트 환경과 프로덕션 환경으로 릴리스 빌드를 배포 합니다.

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

와 **활성 (Release)** 또는 **릴리스** 릴리스 빌드 구성을 사용 하 여 배포할 때 적용 되는 값이 표시를 선택 합니다.

- 에 **배포할 항목** 상자 **응용 프로그램을 실행 하는 데 필요한 파일만** 을 선택 합니다. 다른 옵션은 **이 프로젝트의 모든 파일** 또는 **이 프로젝트 폴더의 모든 파일**합니다. 변경 되지 않은 기본 선택 하지 않고 예를 들어 소스 코드 파일을 배포 하지 마십시오. 이 설정은 SQL Server Compact 이진 파일이 있는 폴더를 프로젝트에 포함 해야 하는 이유는 이유입니다. 이 설정에 대 한 자세한 내용은 참조 **이유 하지 않는 프로젝트 폴더 내에 있는 파일의 모든 배포?** 에 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)합니다.
- **디버그 기호 생성 제외** 을 선택 합니다. 이 빌드 구성을 사용 하면 디버깅 수 없습니다.
- **응용 프로그램에서 파일을 제외\_데이터 폴더** 선택 하지 않으면 합니다. 멤버 자격 데이터베이스에 대 한 SQL Server Compact 파일은 해당 폴더에 있으며 배포 해야 합니다. 데이터베이스 변경 내용을 포함 하지 않는 업데이트를 배포할 때이 확인란을 선택 합니다.
- **이 응용 프로그램을 게시 하기 전에 미리 컴파일할** 선택 하지 않으면 합니다. 대부분의 시나리오에서 웹 응용 프로그램 프로젝트를 미리 컴파일하 않아도가 됩니다. 이 옵션에 대 한 자세한 내용은 참조 [웹 패키지 및 게시 탭, 프로젝트 속성](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx) 및 [미리 컴파일할 설정 대화 상자 고급](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx)합니다.
- **SQL 패키지 및 게시 탭에서 구성 된 모든 데이터베이스가 포함** 을 선택 하면이 옵션은 효과가 없습니다 지금 구성 하지 때문에 있지만 **SQL 패키지 및 게시** 탭 합니다. SQL Server 데이터베이스를 배포 하기 위한 유일한 옵션으로 사용 되는 이전 버전의 데이터베이스 배포 방법에 대 한 해당 탭이 있습니다. 사용 하 여는 **SQL 패키지 및 게시** 탭에 [SQL Server로 마이그레이션](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) 자습서입니다.
- **Web Deployment 패키지 설정** 섹션에는 한 번의 클릭을 사용 중 이므로 적용 되지 않습니다이 자습서에 게시 합니다.

변경 된 **구성** 디버그 빌드에 대해 기본 설정을 보려면 디버그 드롭다운 상자입니다. 값이 동일한 경우를 제외 하 고 **생성 된 디버그 기호 제외** 디버그 빌드를 배포할 때 디버그할 수 있도록 지워집니다.

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>Elmah 폴더 배포 가져옵니다 시겠습니까 만들기

이전 자습서에서 볼 수 있듯이 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 오류 로깅 및 보고에 대 한 기능을 제공 합니다. Contoso 대학 응용 프로그램에서 Elmah 하도록 구성 된 명명 된 폴더에 오류 세부 정보 저장 *Elmah*:

![Elmah 폴더](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

배포에서 특정 파일이 나 폴더를 제외 하는 일반적인; 또 다른 예로 사용자가 파일을 업로드할 수 있는 폴더 것입니다. 로그 파일을 원하지 또는 프로덕션에 배포 하 여 개발 환경에서 생성 된 파일을 업로드 합니다. 프로덕션 환경에 대 한 업데이트를 배포 하는 경우 하지 않고를 프로덕션에 있는 파일을 삭제 하려면 배포 프로세스입니다. (설정한에 따라 배포 옵션을 배포할 때 대상 사이트는 원본 사이트에 파일이 있는 경우, 웹 배포에서 삭제 대상.)

이 자습서의 앞부분에서 본 것 처럼는 **배포할 항목** 옵션에 **웹 패키지 및 게시** 탭으로 설정 되어 **만이 응용 프로그램을 실행 하는 데 필요한 파일이**합니다. 결과적으로, 개발에서 Elmah에 의해 만들어진 로그 파일 배포 되지 않습니다가 원하는 발생 합니다. (¹ è æ ÷, 문서를 업로드 하려면 프로젝트에 포함할 수 및 해당 **빌드 작업** 속성으로 설정 해야 합니다. **콘텐츠**합니다. 자세한 내용은 참조 **이유 하지 않는 프로젝트 폴더 내에 있는 파일의 모든 배포?** 에 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)). 그러나 웹 배포 되지 폴더가 만들어집니다 대상 사이트에서 하나 이상의 파일을 복사할 경우를 제외 합니다. 따라서 추가한는 *.txt* 파일을 복사할 폴더를 자리 표시자 역할을 폴더입니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Elmah* 폴더를 **새 항목 추가**, 명명 된 파일을 만듭니다 *Placeholder.txt*합니다. 다음 텍스트 모드로: "폴더 가져옵니다 배포 되는지 확인 하려면 자리 표시자 파일입니다." 한 파일을 저장 합니다. Visual Studio 때문에이 파일 및 컴퓨터가 폴더에 배포 되었는지 확인 하기 위해 수행 해야 그는 **빌드 작업** 속성 *.txt* 파일으로 설정 되어 **콘텐츠**기본적으로 합니다.

이제 배포 설치 작업을 모두 완료 했습니다. 다음 자습서에서는 Contoso 대학 사이트 테스트 환경에 배포 하 고 테스트 합니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
