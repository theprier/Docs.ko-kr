---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Code-Only 업데이트-8/12 배포 | Microsoft Docs'
author: tdykstra
description: 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: 6305a8cb87d9b00b6bb4c4f8fa6114bddc4eb89f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886916"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Code-Only 업데이트-12 8을 배포 합니다.
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. 웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다. 계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능을 표시, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Azure 앱 서비스 웹 앱을 배포 하는 방법을 보여 줍니다. 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.


## <a name="overview"></a>개요

초기 배포 후 유지 관리 하 고 웹 사이트 개발 작업 계속 되 고 장기 하기 전에 업데이트를 배포 하려고 합니다. 이 자습서에서는 응용 프로그램 코드에 대 한 업데이트를 배포 하는 과정을 안내 합니다. 이 업데이트는 데이터베이스 변경; 포함 되지 않습니다. 다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법에 대 한 차이점 표시 됩니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="making-a-code-change"></a>코드 변경 내용을

에 추가할 응용 프로그램에 대 한 업데이트의 간단한 예,으로 **강사** 선택한 강사 여 courses 목록이 페이지입니다.

실행 하는 경우는 **강사** 페이지 된다고을 알 수 있습니다 **선택** 표에서 링크 하는데 확인 이외의 행 배경 turn 회색 않으면 하지 않습니다.

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

때 실행 되는 코드를 추가 하는 이제는 **선택** 링크를 클릭 하 고 선택한 강사 여 courses 목록이 표시 됩니다.

*Instructors.aspx*, 다음 태그를 추가 바로 뒤의 **ErrorMessageLabel** `Label` 제어:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

페이지를 실행 하 고 강사를 선택 합니다. 해당 강사 여 과정의 목록이 표시 됩니다.

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>테스트 환경에 배포 하는 코드 업데이트

테스트 환경에 배포 하는 게시를 다시 한 번의 클릭을 실행 하는 간단한 방법입니다. 이 프로세스를 더 빠르게 수행 하려면 사용할 수 있습니다는 **한 번 클릭으로 웹 게시** 도구 모음입니다.

에 **보기** 메뉴 선택 **도구 모음** 선택한 후 **한 번 클릭으로 웹 게시**합니다.

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

**솔루션 탐색기**, ContosoUniversity 프로젝트를 선택 합니다.

**한 번 클릭으로 웹 게시** 도구 모음에서 선택 된 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시** (왼쪽과 오른쪽을 가리키는 화살표가 있는 아이콘).

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 자동으로 열립니다. 강사 페이지를 실행 하 고 강사 업데이트가 제대로 배포 되었는지 확인 하려면를 선택 합니다.

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

일반적인 회귀 테스트를 수행 (즉, 테스트 되는 새로운 변경 하지 않은 기존 기능이 해제 해야 하는 사이트의 나머지 부분)입니다. 하지만이 자습서에 대 한 해당 단계를 건너뜁니다 고 프로덕션 환경에 업데이트 배포를 진행 합니다.

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>프로덕션에 대 한 초기 데이터베이스 상태를 재배포 하면 방지

실제 응용 프로그램에서 초기 배포 후 사용자 프로덕션 사이트와 상호 작용 하 고 데이터베이스 라이브 데이터로 채워집니다. 따라서 라이브 데이터를 모두 지우고 것의 초기 상태인 멤버 자격 데이터베이스를 다시 배포 하지 않으려는 경우 SQL Server Compact 데이터베이스의 파일은는 *앱\_데이터* 하는 파일에 있도록 배포 설정을 변경 하 여이 방지 해야 하는 폴더는 *앱\_데이터* 폴더 배포 되지 않습니다.

열기는 **프로젝트 속성** ContosoUniversity 프로젝트 및 선택 창에서 **웹 패키지 및 게시** 탭 합니다. 다음 사항을 확인는 **구성** 하거나 드롭다운 목록 상자에 **활성 (Release)** 또는 **릴리스** 선택을 선택 **앱에서파일을제외\_데이터 폴더**합니다.

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

것이 좋습니다 디버그 빌드 구성에 대 한 동일한 변경 작업을 수행 하 고 디버그 빌드를 나중에 배포 하려는 경우: 변경 **구성** 를 **디버그** 선택한 후 **제외 앱에서 파일\_데이터 폴더**합니다.

저장 하 고 닫습니다는 **웹 패키지 및 게시** 탭 합니다.

> [!NOTE] 
> 
> [!IMPORTANT]
> 없는지 확인 **대상에서 추가 파일 제거** 게시 프로필에서 선택 합니다. 해당 옵션을 선택 하면 배포 프로세스 응용 프로그램에 있는 데이터베이스를 삭제 됩니다\_하며 배포 된 사이트의 데이터를 앱이 삭제 됩니다\_자체 데이터 폴더.


## <a name="preventing-user-access-to-the-production-site-during-update"></a>업데이트 하는 동안 프로덕션 사이트에 대 한 사용자 액세스를 방지

배포 하는 변경에는 이제 단일 페이지에 대 한 간단한 변경이입니다. 더 큰 변경에 배포 하는 경우에 따라 있고이 경우 사이트 행동할 수 있으므로 이상 하 게 배포 완료 되기 전에 페이지를 요청 하면 합니다. 이 방지 하려면 사용할 수 있습니다는 *앱\_offline.htm* 파일입니다. 라는 파일을 만들었을 때 *앱\_offline.htm* 응용 프로그램의 루트 폴더에 IIS에서는 응용 프로그램을 실행 하는 대신 해당 파일입니다. 배포 하는 동안 액세스를 방지 하려면 삽입 되므로 *앱\_offline.htm* 루트 폴더에 배포 프로세스를 실행 한 다음 제거 *앱\_offline.htm*합니다.

**솔루션 탐색기**(하지 프로젝트 중 하나) 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **새 솔루션 폴더**합니다.

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

폴더 이름을 *SolutionFiles*합니다.

새 폴더에 명명 된 HTML 페이지를 만듭니다 *앱\_offline.htm*합니다. 기존 내용을 다음 태그로 바꿉니다.

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

복사할 수는 *앱\_offline.htm* 파일을 FTP 연결을 사용 하 여 사이트 또는 **파일 관리자** 호스팅 공급자의 제어판에서 유틸리티입니다. 이 자습서에서는 사용 된 **파일 관리자**합니다.

제어판을 열고 선택 **파일 관리자** 에서 같이 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다. 선택 **contosouniversity.com** 차례로 **wwwroot** 을 응용 프로그램의 루트 폴더에 가져오고 클릭 **업로드**합니다.

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

에 **파일 업로드** 대화 상자는 *앱\_offline.htm* 파일을 클릭 한 다음 **업로드**합니다.

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

사이트의 URL로 이동 합니다. 참조 하는 *앱\_offline.htm* 페이지 홈 페이지 대신 표시 됩니다.

[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

이제 프로덕션 환경에 배포할 준비가 되었습니다.

## <a name="deploying-the-code-update-to-the-production-environment"></a>프로덕션 환경에 배포 하는 코드 업데이트

**한 번 클릭으로 웹 게시** 도구 모음에서 선택 된 **프로덕션** 게시 프로필을 클릭 한 다음 **웹 게시**합니다.

Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 브라우저 사이트의 홈 페이지를 엽니다. *앱\_offline.htm* 파일이 표시 됩니다. 성공적인 배포를 확인 하려면를 테스트 하려면 먼저 제거 해야는 *앱\_offline.htm* 파일입니다.

으로 돌아와서는 **파일 관리자** 제어판에 응용 프로그램입니다. 선택 **contosouniversity.com** 및 **wwwroot**선택, **앱\_offline.htm**, 클릭 하 고 **삭제**합니다.

[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

브라우저에서 공용 사이트에서 강사 페이지를 열고 강사 업데이트가 제대로 배포 되었는지 확인 하려면 선택 합니다.

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

이제 데이터베이스 변경 내용을 포함 하지 않는 응용 프로그램 업데이트를 배포 했습니다. 다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
