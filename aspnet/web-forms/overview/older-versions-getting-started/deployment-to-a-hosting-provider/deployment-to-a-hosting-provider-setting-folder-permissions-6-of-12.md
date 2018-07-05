---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 설정 폴더 사용 권한-6/12 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 17910952e78418ef9e5b80efb04b5fe1e70c11bf
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385313"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 설정 폴더 사용 권한-6/12
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

이 자습서에 대 한 폴더 사용 권한을 설정 합니다 *Elmah* 폴더에 배포 된 웹 사이트 응용 프로그램 폴더에 로그 파일을 만들 수 있도록 합니다.

Visual Studio 개발 서버 (Cassini)를 사용 하 여 Visual Studio에서 웹 응용 프로그램을 테스트할 때 응용 프로그램 id에서 실행 됩니다. 개발 컴퓨터에서 관리자는 대부분을 모든 폴더의 모든 파일에 아무것도 할 권한이 전체. 하지만 사이트에 할당 되는 응용 프로그램 풀에 대해 정의 된 id에서 실행 되는 응용 프로그램이 IIS에서 실행 하는 경우. 일반적으로 권한이 제한 된 시스템 정의 계정입니다. 기본적으로 읽기와 웹 응용 프로그램의 파일 및 폴더에 대 한 실행 하지만 쓰기 권한이 정보를 참조 하지 않습니다.

응용 프로그램을 만들거나 웹 응용 프로그램에서 일반적인 업데이트 파일 해야 하는 경우 이것이 문제가 됩니다. Elmah를 Contoso University 응용 프로그램에서의 XML 파일을 만듭니다는 *Elmah* 오류에 대 한 세부 정보를 저장 하기 위해 폴더입니다. 같은 Elmah를 사용 하지 않는 경우에 사이트 사용자가 파일을 업로드 하거나 사이트의 폴더에 데이터를 기록 하는 다른 작업을 수행할 수 있습니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="testing-error-logging-and-reporting"></a>오류 로깅 및 보고를 테스트 합니다.

어떻게 표시 되는지 확인 응용 프로그램 하지 올바르게 IIS에서 (했을 때 Visual Studio에서 테스트) 하지만, 일반적으로 Elmah에서 로깅될를 열고 다음 세부 정보를 보려면 Elmah 오류 로그는 오류가 발생할 수 있습니다. Elmah는 XML 파일을 만들고 오류 세부 정보를 저장할 수 없는 경우, 빈 오류 보고서를 표시 합니다.

브라우저를 열고 이동할 `http://localhost/ContosoUniversity`, 한 다음 같은 잘못 된 URL을 요청 하 고 *Studentsxxx.aspx*합니다. 시스템에서 생성 된 오류 페이지가 대신 표시 합니다 *GenericErrorPage.aspx* 때문에 페이지를 `customErrors` Web.config 파일에서 설정이 "RemoteOnly"이 고 로컬로 실행 하는 IIS:

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

지금 실행 *Elmah.axd* 오류 보고서를 볼 수 있습니다. Elmah는 XML 파일을 만들 수 없기 때문에 빈 오류 로그 페이지를 표시 합니다 *Elmah* 폴더:

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>Elmah 폴더에 쓰기 권한 설정

폴더 사용 권한을 수동으로 설정 하거나 배포 프로세스의 자동 부분을 만들 수 있습니다. 복잡 한 MSBuild 코드를 필요 하므로 자동 및 배포한 처음으로이 작업을 수행 해야 하므로,이 자습서에만 수동으로 작업을 수행 하는 방법을 보여 줍니다. (배포 프로세스의이 부분을 확인 하는 방법에 대 한 정보를 참조 하세요 [웹 게시에 폴더 권한 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) Sayed Hashimi의 블로그입니다.)

**Windows 탐색기**, 이동할 *C:\inetpub\wwwroot\ContosoUniversity*합니다. 마우스 오른쪽 단추로 클릭 합니다 *Elmah* 폴더를 선택 **속성**를 선택한 후는 **보안** 탭 합니다.

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

(표시 되지 않는 경우 **DefaultAppPool** 에 **그룹 또는 사용자 이름** 목록 아마도 데이 자습서에서 지정한 것 보다 몇 가지 다른 방법을 컴퓨터에 IIS 및 ASP.NET 4를 설정 합니다. 이런 경우 해당 id에 쓰기 권한 부여 확인 하 고 Contoso University 응용 프로그램에 할당 된 응용 프로그램 풀 id가 어떻게 되 알아보십시오. 링크를 참조 응용 프로그램 풀 id에 대 한이 자습서의 끝입니다.)


              **편집**을 클릭합니다. 에 **Elmah에 대 한 권한을** 대화 상자에서 **DefaultAppPool**를 선택한 후는 **작성** 확인란을 **허용** 열.

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

클릭 **확인** 두 대화 상자에서.

## <a name="retesting-error-logging-and-reporting"></a>오류 로깅 및 보고를 다시 테스트

동일한 방식으로 (잘못 된 URL 요청) 오류가 다시 발생 하 여 테스트 하 고 실행 합니다 **오류 로그** 페이지입니다. 이 오류는 페이지에 나타납니다.

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

또한 쓰기 권한이 필요에 *앱\_데이터* 폴더 하므로 해당 폴더에 있는 SQL Server Compact 데이터베이스 파일이 있고 해당 데이터베이스에서 데이터를 업데이트할 수 있게 되기를 원하는 합니다. 그러나이 경우 필요가 배포 프로세스에 대 한 쓰기 권한이 자동으로 설정 되므로 추가 작업을 수행 하는 *앱\_데이터* 폴더입니다.

이제 마친 Contoso University 하는 데 필요한 작업을 모두 로컬 컴퓨터에 IIS에서 올바르게 작동 합니다. 다음 자습서에서 생성 됩니다 사이트 공개적으로 사용 가능한 호스팅 공급자에 배포 하 여.

## <a name="more-information"></a>추가 정보

이 예제에서는 Elmah 로그 파일을 저장할 수 없게 된 이유 비교적 명확 했습니다. IIS 추적을 사용 하 여 문제의 원인을 명확; 있지 않은 경우 참조 [문제 해결 실패 한 요청 추적 사용 IIS 7에서](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) IIS.net 사이트의.

응용 프로그램 풀 id에 사용 권한을 부여 하는 방법에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 풀 Id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) 하 고 [파일 시스템 Acl을 통해 IIS에서 콘텐츠 보호](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) IIS.net 사이트의.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
