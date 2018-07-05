---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Code-Only 업데이트-12 8 배포 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: 16a9e48034536964d526717ecde2a9b813818963
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816086"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Code-Only 업데이트-12 8 배포
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

초기 배포 후 유지 관리 하 고 웹 사이트 개발의 작업 계속 되 고 오래 전에 하려는 업데이트를 배포 합니다. 이 자습서에서는 응용 프로그램 코드에 대 한 업데이트를 배포 하는 과정을 안내 합니다. 이 업데이트는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 방법에 대 한 차이점 표시 됩니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="making-a-code-change"></a>코드 변경

간단한 예로 업데이트 응용 프로그램을 추가 합니다 **강사** 선택한 강사가가 르 친 과정 목록을 페이지입니다.

실행 하는 경우는 **강사** 페이지를 보면 있는지 **선택** 표의 링크 하지 확인 이외의 행 배경색 설정 회색 있지만.

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

이제 때 실행 되는 코드를 추가 합니다 **선택** 링크를 클릭 하 고 선택한 강사가가 르 친 과정의 목록을 표시 합니다.

*Instructors.aspx*, 다음 태그를 추가 직후 합니다 **ErrorMessageLabel** `Label` 제어:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

페이지를 실행 하 고 강사를 선택 합니다. 해당 강사가가 르 친 과정의 목록이 표시 됩니다.

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>테스트 환경에 코드 업데이트 배포

테스트 환경에 배포 게시를 다시 실행 한 번의 클릭 하기만 하면 됩니다. 이 프로세스를 더 빠르게 하려면 사용할 수 있습니다 합니다 **한 번 클릭으로 웹 게시** 도구 모음입니다.

에 **뷰** 메뉴 선택 **도구 모음** 선택한 후 **한 번 클릭으로 웹 게시**합니다.

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

**솔루션 탐색기**, ContosoUniversity 프로젝트를 선택 합니다.

**한 번 클릭으로 웹 게시** 도구 모음을 선택 합니다 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시** (왼쪽과 오른쪽을 가리키는 화살표가 있는 아이콘).

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 자동으로 열립니다. 강사 페이지를 실행 하 고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

일반적으로 회귀 테스트를 수행 (즉, 테스트할 새로운 변경 사항을 기존 기능이 손상 하지 않는지 확인 하는 사이트의 나머지 부분). 하지만이 자습서에 대 한 해당 단계를 건너뜁니다 고 프로덕션에 업데이트를 배포를 진행 하겠습니다.

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>프로덕션에 대 한 초기 데이터베이스 상태를 다시 배포 방지

실제 응용 프로그램에서 사용자와 상호 작용 프로덕션 사이트에 초기 배포 후 데이터베이스 라이브 데이터로 채워집니다. 따라서 모든 라이브 데이터 초기화는 초기 상태로의 멤버 자격 데이터베이스를 다시 배포 하지 않으려는 합니다. SQL Server Compact 데이터베이스에 파일이 있으므로 합니다 *앱\_데이터* 하는 파일에 있도록 배포 설정을 변경 하 여이 방지 해야 하는 폴더를 *앱\_데이터* 폴더 배포 되지 않습니다.

엽니다는 **프로젝트 속성** ContosoUniversity 프로젝트 및 선택 창 합니다 **웹 패키지 및 게시** 탭 합니다. 있는지 확인 합니다 **구성** 드롭다운 목록 상자에 **(릴리스) 활성** 또는 **릴리스** 선택 옵션을 선택 **앱에서파일을제외\_데이터 폴더**합니다.

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

디버그 빌드 구성에 대 한 동일 하 게 변경 하는 것이 좋습니다는 것을 나중에 디버그 빌드를 배포 하려는 경우: 변경 **구성** 하 **디버그** 를 선택한 **제외 앱에서 파일\_데이터 폴더**합니다.

저장 후 닫기 합니다 **웹 패키지 및 게시** 탭 합니다.

> [!NOTE] 
> 
> [!IMPORTANT]
> 필요가 있는지 **대상에서 추가 파일 제거** 게시 프로필에서 선택 합니다. 해당 옵션을 선택 하면 배포 프로세스를 앱에 있는 데이터베이스를 삭제 합니다\_배포 된 사이트에 데이터를 앱이 삭제 됩니다\_자체 데이터 폴더.


## <a name="preventing-user-access-to-the-production-site-during-update"></a>업데이트 하는 동안 프로덕션 사이트에 대 한 사용자 액세스를 방지

배포 하는 변경에는 이제 단일 페이지에 대 한 간단한 변경이입니다. 하지만 대규모 변경 사항을 배포 하는 경우에 따라 하 고이 경우 사이트 수 작동 이상 하 게 배포 완료 되기 전에 사용자 페이지를 요청 합니다. 이 방지 하려면 사용할 수 있는 *앱\_offline.htm* 파일입니다. 라는 파일을 적용할 시기 *앱\_offline.htm* 응용 프로그램의 루트 폴더에서 IIS 자동으로 파일을 표시는 응용 프로그램을 실행 하는 대신 합니다. 배포 하는 동안 액세스를 방지 하려면 배치 되므로 *앱\_offline.htm* 루트 폴더에서 배포 프로세스를 실행 한 다음 제거 *앱\_offline.htm*합니다.

**솔루션 탐색기**, (없습니다 프로젝트 중 하나) 솔루션을 마우스 오른쪽 단추로 **새 솔루션 폴더**합니다.

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

폴더의 이름을 *SolutionFiles*합니다.

새 폴더에 명명 된 HTML 페이지를 만듭니다 *앱\_offline.htm*합니다. 기존 내용을 다음 태그로 바꿉니다.

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

복사할 수는 있지만 합니다 *앱\_offline.htm* 파일을 FTP 연결을 사용 하 여 사이트 또는 **파일 관리자** 호스팅 공급자의 제어판에서 유틸리티입니다. 이 자습서에서는 사용 된 **파일 관리자**합니다.

제어판을 열고 선택 **파일 관리자** 에서처럼 합니다 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다. 선택 **contosouniversity.com** 차례로 **wwwroot** 응용 프로그램의 루트 폴더에 누른 **업로드**합니다.

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

에 **파일 업로드** 대화 상자를 선택 합니다 *앱\_offline.htm* 파일을 클릭 **업로드**.

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

사이트의 URL로 이동 합니다. 표시 된 *앱\_offline.htm* 페이지 홈 페이지가 대신 표시 됩니다.

[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

이제 프로덕션 환경에 배포할 준비가 되었습니다.

## <a name="deploying-the-code-update-to-the-production-environment"></a>프로덕션 환경에 코드 업데이트 배포

에 **한 번 클릭으로 웹 게시** 도구 모음에서 선택 합니다 **프로덕션** 게시 프로필을 클릭 한 다음 **웹 게시**합니다.

Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지로 브라우저를 엽니다. 합니다 *앱\_offline.htm* 파일이 표시 됩니다. 를 성공적으로 배포를 확인 하려면 테스트 전에 제거 해야 합니다 *앱\_offline.htm* 파일입니다.

반환 합니다 **파일 관리자** 제어판 응용 프로그램입니다. 선택 **contosouniversity.com** 하 고 **wwwroot**를 선택 **앱\_offline.htm**를 클릭 하 고 **삭제**합니다.

[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

브라우저에서 공용 사이트에서 강사 페이지를 열고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

이제 데이터베이스 변경 내용을 포함 하지 않는 응용 프로그램 업데이트를 배포 했습니다. 다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
