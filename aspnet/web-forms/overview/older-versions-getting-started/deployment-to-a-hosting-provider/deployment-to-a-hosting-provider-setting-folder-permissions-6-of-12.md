---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 폴더 사용 권한 설정-6/12 | Microsoft Docs'
author: tdykstra
description: 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 573e75221a1c0018bded7544e584b0c75f47d607
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "30887267"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 폴더 사용 권한 설정-6/12
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. 웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다. 계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능을 표시, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Azure 앱 서비스 웹 앱을 배포 하는 방법을 보여 줍니다. 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.


## <a name="overview"></a>개요

에 대 한 폴더 사용 권한을 설정 하면이 자습서는 *Elmah* 폴더에 배포 된 웹 사이트 응용 프로그램 해당 폴더에 로그 파일을 만들 수 있도록 합니다.

Visual Studio 개발 서버 (Cassini)를 사용 하 여 Visual Studio에서 웹 응용 프로그램을 테스트할 때 응용 프로그램 id에서 실행 됩니다. 개발 컴퓨터의 관리자는 거의 하 고 모든 폴더에 모든 파일에 아무 것도 할 수 있는 전체 권한을 갖고 있습니다. 하지만 사이트에 할당 된 응용 프로그램 풀에 대해 정의 된 id에서 실행 하는 응용 프로그램에서 IIS를 실행 합니다. 이것은 일반적으로 제한 된 권한을 가진 시스템 정의 계정입니다. 기본적으로 읽기와 웹 응용 프로그램의 파일 및 폴더에 대 한 실행 하지만 쓰기 권한이 필요 하지 않습니다.

응용 프로그램을 만들거나는 공통 업데이트 파일을 웹 응용 프로그램에서 필요 하는 경우에 문제가 됩니다. Elmah Contoso 대학 응용 프로그램에서의 XML 파일을 만듭니다는 *Elmah* 오류에 대 한 세부 정보를 저장 하려면 폴더입니다. 다음과 같이 Elmah를 사용 하지 않는 경우에 사이트 파일을 업로드 하거나 사이트의 폴더에 데이터를 쓰는 다른 작업을 수행 하는 사용자를 할당할 수도 있습니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="testing-error-logging-and-reporting"></a>오류 로깅 및 보고를 테스트 합니다.

어떻게 표시 되는지 확인 응용 프로그램 하지 않는 올바르게 IIS에서 (했을 때 Visual Studio에서 테스트) 하지만, 일반적으로 Elmah로 로깅될 및 다음 세부 정보를 Elmah 오류 로그를 엽니다는 오류가 발생할 수 있습니다. Elmah, XML 파일을 만들고 오류 세부 정보를 저장할 수 없는 경우 빈 오류 보고서를 표시 합니다.

브라우저를 열고로 이동 `http://localhost/ContosoUniversity`, 후 같은 잘못 된 URL 요청 *Studentsxxx.aspx*합니다. 시스템에서 생성 된 오류 페이지가 대신 표시는 *GenericErrorPage.aspx* 때문에 페이지는 `customErrors` Web.config 파일에서 설정이 "RemoteOnly"이 고 IIS를 로컬로 실행:

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

이제 실행 *Elmah.axd* 오류 보고서를 볼 수 있습니다. Elmah XML 파일을 만들 수 없기 때문에 빈 오류 로그 페이지를 참조는 *Elmah* 폴더:

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>Elmah 폴더에 대 한 쓰기 권한 설정

폴더 사용 권한을 수동으로 설정 하거나는 자동 배포 프로세스 도중을 만들 수 있습니다. 자동 만들기 복잡 한 MSBuild 코드 걸리며 배포한 처음으로이 작업을 수행 해야 하므로,이 자습서에서는 수동으로 수행 하는 방법을 보여 줍니다. (배포 프로세스의이 부분을 확인 하는 방법에 대 한 정보를 참조 하십시오. [웹 게시에 대 한 폴더 권한을 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) Sayed Hashimi 블로그에서.)

**Windows 탐색기**로 이동 *C:\inetpub\wwwroot\ContosoUniversity*합니다. 마우스 오른쪽 단추로 클릭는 *Elmah* 폴더를 **속성**를 선택한 후는 **보안** 탭 합니다.

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

(표시 되지 않으면 **DefaultAppPool** 에 **그룹 또는 사용자 이름** 목록 것이 자습서에서는 지정 된 다른 방법을 하는 데 사용한 컴퓨터에서 IIS 및 ASP.NET 4를 설정 합니다. 이 경우 어떤 id가 Contoso 대학 응용 프로그램에 할당 된 응용 프로그램 풀에서 사용 하 고 해당 id로 쓰기 권한을 부여 봅니다. 링크를 참조 응용 프로그램 풀 id에 대 한이 자습서의 끝에.)


              **편집**을 클릭합니다. 에 **Elmah에 대 한 권한을** 대화 상자에서 **DefaultAppPool**, 선택한 후는 **쓰기** 확인란에는 **허용** 열입니다.

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

클릭 **확인** 두 대화 상자에서.

## <a name="retesting-error-logging-and-reporting"></a>오류 로깅 및 보고를 다시 테스트

같은 방식으로 (잘못 된 URL 요청) 오류가 다시 발생 하 여 테스트 하 고 실행 된 **오류 로그** 페이지. 이 오류는 페이지에 나타납니다.

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

하면 또한 필요에 대 한 쓰기는 *앱\_데이터* 폴더 때문에 해당 폴더에 있는 SQL Server Compact 데이터베이스 파일 있고 해당 데이터베이스의 데이터를 업데이트할 수 있게 되기를 원하는 합니다. 그러나이 경우 배포 프로세스에 대 한 쓰기 권한이 자동으로 설정 하기 때문에 추가 하는 어떤 작업 없는는 *앱\_데이터* 폴더입니다.

완료 했으므로 Contoso 대학 하는 데 필요한 작업을 모두 로컬 컴퓨터에서 IIS에서 올바르게 작동 합니다. 다음 자습서에서 생성 됩니다 사이트 공개적으로 사용할 수는 호스팅 공급자를 배포 하 여.

## <a name="more-information"></a>추가 정보

이 예제에서는 Elmah 로그 파일을 저장할 수 없게 된 이유 상당히 당연 합니다. IIS 추적을 사용 하 여 문제의 원인을; 명확 하지 않은 경우 참조 [문제 해결 실패 한 요청을 사용 하 여 추적 IIS 7에서](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) IIS.net 사이트에 있습니다.

응용 프로그램 풀 id에 권한을 부여 하는 방법에 대 한 자세한 내용은 참조 [응용 프로그램 풀 Id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) 및 [콘텐츠 파일 시스템 Acl을 통해 IIS에서 Secure](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) IIS.net 사이트에 있습니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
