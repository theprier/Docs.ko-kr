---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로젝트 속성 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: 85b6dbcc8d40c168a49513ef6b549f9ec7fa5097
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment-using-visual-studio-project-properties"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로젝트 속성
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

일부 배포 옵션은 프로젝트 파일에 저장 된 프로젝트 속성에서 구성 (의 *.csproj* 또는 *.vbproj* 파일). 대부분의 경우에서 이러한 설정의 기본값은 원하는 하지만 사용할 수 있습니다는 **프로젝트 속성** UI를 변경할 수 있는 경우 이러한 설정으로 작동 하도록 Visual Studio에 빌드됩니다. 이 자습서에서 배포 설정을 검토 **프로젝트 속성**합니다. 배포할 빈 폴더는 자리 표시자 파일을 만들 수도 있습니다.

## <a name="configure-deployment-settings-in-the-project-properties-window"></a>프로젝트 속성 창에서 배포 설정 구성

배포 하는 동안 수행 되는 작업에 영향을 주는 대부분의 설정은 다음과 같은 자습서에서 확인할 수 게시 프로필에 포함 됩니다. 알고 있어야 하는 몇 가지 설정에는 **패키지/게시** 의 탭에서 **프로젝트 속성** 창. 이러한 설정은 각 빌드 구성에 대해 지정 되어-즉, 디버그 빌드에 있는 것 보다 릴리스 빌드에 대 한 다른 설정을 사용할 수 있습니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **ContosoUniversity** 프로젝트를 **속성**를 선택한 후는 **웹패키지/게시**탭 합니다.

![웹 패키지 및 게시 탭](project-properties/_static/image1.png)

창이 표시 되 면 기본적으로 솔루션에 대 한 현재 활성 나오든 이들 빌드 구성에 대 한 설정을 보여 줍니다. 경우는 **구성** 상자를 나타내지 않습니다 **활성 (Release)**선택, **릴리스** 릴리스 빌드 구성에 대 한 설정을 표시 하려면. 테스트 환경과 프로덕션 환경으로 릴리스 빌드를 배포 합니다.

![릴리스 빌드 구성 선택](project-properties/_static/image2.png)

와 **활성 (Release)** 또는 **릴리스** 릴리스 빌드 구성을 사용 하 여 배포할 때 적용 되는 값이 표시를 선택 합니다.

- 에 **배포할 항목** 상자 **응용 프로그램을 실행 하는 데 필요한 파일만** 을 선택 합니다. 다른 옵션은 **이 프로젝트의 모든 파일** 또는 **이 프로젝트 폴더의 모든 파일**합니다. 변경 되지 않은 기본 선택 하지 않고 예를 들어 소스 코드 파일을 배포 하지 마십시오. 이 설정은 SQL Server Compact 이진 파일이 있는 폴더를 프로젝트에 포함 해야 하는 이유는 이유입니다. 이 설정에 대 한 자세한 내용은 참조 **이유 하지 않는 프로젝트 폴더 내에 있는 파일의 모든 배포?** 에 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)합니다.
- **디버그 기호 생성 제외** 을 선택 합니다. 이 빌드 구성을 사용 하면 디버깅 수 없습니다.
- **SQL 패키지 및 게시 탭에서 구성 된 모든 데이터베이스가 포함** 을 선택 합니다. Visual Studio 파일 뿐만 아니라 데이터베이스를 배포할지 여부를 지정 합니다. 확인란 레이블만 언급 되어 있지만 **SQL 패키지 및 게시** 탭이 확인란의 선택을 취소도 기능을 해제 게시 프로필에서 구성 된 데이터베이스를 배포 합니다. 수행 하는 나중 확인란은 선택 된 상태로 유지 해야 하므로 합니다. **SQL 패키지 및 게시** 게시이 자습서에 사용 하지 않을 메서드는 이전 버전의 데이터베이스에 대 한 탭을 사용 합니다.
- **Web Deployment 패키지 설정** 섹션에는 한 번의 클릭을 사용 중 이므로 적용 되지 않습니다이 자습서에 게시 합니다.

변경 된 **구성** 디버그 빌드에 대해 기본 설정을 보려면 디버그 드롭다운 상자입니다. 값이 동일한 경우를 제외 하 고 **생성 된 디버그 기호 제외** 디버그 빌드를 배포할 때 디버그할 수 있도록 지워집니다.

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a>Elmah 폴더 가져옵니다 배포 되었는지 확인

이전 자습서에서 볼 수 있듯이 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 오류 로깅 및 보고에 대 한 기능을 제공 합니다. Contoso 대학 응용 프로그램에서 Elmah 하도록 구성 된 명명 된 폴더에 오류 세부 정보 저장 *Elmah*:

![Elmah 폴더](project-properties/_static/image3.png)

배포에서 특정 파일이 나 폴더를 제외 하는 일반적인; 또 다른 예로 사용자가 파일을 업로드할 수 있는 폴더 것입니다. 로그 파일을 원하지 또는 프로덕션에 배포 하 여 개발 환경에서 생성 된 파일을 업로드 합니다. 프로덕션 환경에 대 한 업데이트를 배포 하는 경우 하지 않고를 프로덕션에 있는 파일을 삭제 하려면 배포 프로세스입니다. (설정한에 따라 배포 옵션을 배포할 때 대상 사이트는 원본 사이트에 파일이 있는 경우, 웹 배포에서 삭제 대상.)

이 자습서의 앞부분에서 본 것 처럼는 **배포할 항목** 옵션에 **웹 패키지 및 게시** 탭으로 설정 되어 **만이 응용 프로그램을 실행 하는 데 필요한 파일이**합니다. 결과적으로, 개발에서 Elmah에 의해 만들어진 로그 파일 배포 되지 않습니다가 원하는 발생 합니다. (¹ è æ ÷, 문서를 업로드 하려면 프로젝트에 포함할 수 및 해당 **빌드 작업** 속성으로 설정 해야 합니다. **콘텐츠**합니다. 자세한 내용은 참조 **이유 하지 않는 프로젝트 폴더 내에 있는 파일의 모든 배포?** 에 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)). 그러나 웹 배포 되지 폴더가 만들어집니다 대상 사이트에서 하나 이상의 파일을 복사할 경우를 제외 합니다. 따라서 추가한는 *.txt* 파일을 복사할 폴더를 자리 표시자 역할을 폴더입니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Elmah* 폴더를 **새 항목 추가**, 라는 텍스트 파일을 만들고 *Placeholder.txt*합니다. 다음 텍스트 모드로: "폴더 가져옵니다 배포 되는지 확인 하려면 자리 표시자 파일입니다." 한 파일을 저장 합니다. Visual Studio 때문에이 파일 및 컴퓨터가 폴더에 배포 되었는지 확인 하기 위해 수행 해야 그는 **빌드 작업** 속성 *.txt* 파일으로 설정 되어 **콘텐츠**기본적으로 합니다.

## <a name="summary"></a>요약

이제 배포 설치 작업을 모두 완료 했습니다. 다음 자습서에서는 Contoso 대학 사이트 테스트 환경에 배포 하 고 테스트 합니다.

>[!div class="step-by-step"]
[이전](web-config-transformations.md)
[다음](deploying-to-iis.md)
