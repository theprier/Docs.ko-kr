---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 12 7-프로덕션 환경에 배포 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: 26a832fd336f886ba1ddfb1682930afa4df56c58
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383638"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 12 7-프로덕션 환경에 배포
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

이 자습서에서는 호스팅 공급자를 사용 하 여 계정을 설정 하 고이 ASP.NET 배포 원클릭 Visual Studio를 사용 하 여 프로덕션 환경에 웹 응용 프로그램 기능을 게시 합니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="selecting-a-hosting-provider"></a>호스팅 공급자를 선택합니다.

이 자습서 시리즈와 Contoso University 응용 프로그램에 대 한 ASP.NET 4 및 Web Deploy를 지 원하는 공급자를 해야 합니다. 특정 호스팅 업체는 자습서에는 라이브 웹 사이트를 배포 하는 완벽 한 환경을 보여 줍니다 수 있도록 선택 했습니다. 각 호스팅 회사는 다양 한 기능을 제공 하 고 해당 서버에 배포 하는 환경에 따라 다양 합니다. 그러나이 자습서에서 설명 하는 프로세스가 전체 프로세스에 대 한 일반적입니다. 이 자습서에서는 Cytanium.com 사용 하는 호스팅 공급자를 사용할 수 있는 많은 하나인 및를 보증 하거나 권장 사항에는이 자습서에서 사용 하는 구성 하지 않습니다.

기능 및 가격에 자체 호스팅 공급자를 선택 하려면 준비가 되었을 때 비교할 수 있습니다 합니다 [공급자의 갤러리](https://www.microsoft.com/web/hosting) Microsoft.com/web 사이트의.

## <a name="creating-an-account"></a>계정 만들기

선택한 공급자에서 계정을 만듭니다. 경우 전체 SQL Server 데이터베이스는 추가 대 한 지원은 추가,이 자습서에서는 선택 필요는 없지만 대 한 필요 합니다 [SQL Server로 마이그레이션](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.

이 자습서에서는 새 도메인 이름을 등록할 필요가 없습니다. 공급자가 사이트에 할당 된 임시 URL을 사용 하 여 성공적인 배포를 확인 하려면 테스트할 수 있습니다.

계정을 만든 후 일반적으로 배포 하 고 사이트를 관리 하기 위해 필요한 모든 정보를 포함 하는 환영 전자 메일을 수신 합니다. 호스팅 공급자에 보내는 정보를 여기에 나오는 내용과 비슷할 것입니다. 새 계정 소유자에 게 전송 되는 Cytanium 환영 전자 메일에는 다음 정보가 포함 됩니다.

- 공급자의 컨트롤 패널 사이트에 사이트에 대 한 설정을 관리할 수 있는 URL입니다. ID와 암호를 지정 하는 쉽게 참조할 환영 전자 메일의이 부분에 포함 됩니다. (모두 변경 된이 그림에 대 한 데모로 합니다.)

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- 기본.NET Framework 버전 및 변경 하는 방법에 대 한 정보입니다. 여러 호스팅 사이트 기본값은 2.0, 2.0, 3.0 또는 3.5는.NET Framework를 대상으로 하는 ASP.NET 응용 프로그램과 함께 작동 하는입니다. 그러나 Contoso University 이므로.NET Framework 4 응용 프로그램을이 설정을 변경 해야 합니다. (ASP.NET 4.5 응용 프로그램에 대 한 하는.NET 4.0 설정을 사용 합니다.)

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- 웹 사이트에 액세스 하는 데 사용할 수 있는 임시 URL입니다. 이 계정을 만든 경우 기존 도메인 이름으로 "contosouniversity.com"를 입력 했습니다. 따라서 임시 URL은 `http://contosouniversity.com.vserver01.cytanium.com`합니다.

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- 데이터베이스 및 해당 액세스 하기 위해 필요한 연결 문자열을 설정 하는 방법에 대 한 정보를 제공 합니다.

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- 도구 및 설정 하 여 사이트 배포에 대 한 정보입니다. (Cytanium에서 전자 메일도 언급 WebMatrix 여기 생략 됩니다.)

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>.NET Framework 버전 설정

Cytanium 환영 전자 메일에는.NET Framework의 버전을 변경 하는 방법에 대 한 링크를 포함 합니다. 이러한 지침은 Cytanium 제어판을 통해 수행할 수 있습니다이 설명 합니다. 다른 공급자 컨트롤 패널 하는 사이트가 다르게 표시 하거나 다른 방식으로이 작업을 수행할 수 있습니다 알려 줍니다.

제어판 URL로 이동 합니다. 사용자 이름 및 암호 로그인 후 제어판을 표시 됩니다.

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

에 **호스팅 공간** 상자에서 웹 아이콘 위에 포인터를 선택 **웹 사이트** 메뉴에서.

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

에 **웹 사이트** 상자를 클릭 합니다 **contosouniversity.com** (계정을 만들 때 사용한 사이트의 이름).

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

에 **웹 사이트 속성** 상자를 선택 합니다 **확장** 탭 합니다.

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

ASP.NET에서 변경 **2.0 통합된 파이프라인** 에 **(통합 파이프라인) 4.0**를 클릭 하 고 **업데이트**합니다.

## <a name="publishing-to-the-hosting-provider"></a>호스팅 공급자에 게시

호스팅 공급자에서 시작 전자 메일을 모든 프로젝트를 게시 하는 데 필요한 설정이 포함 하 고 게시 프로필에 해당 정보를 수동으로 입력할 수 있습니다. 공급자에 게 배포를 구성 하는 쉽고 작은 오류 발생률 메서드 사용 하지만: 다운로드 한 *.publishsettings* 파일과 게시 프로필을 가져와서 합니다.

브라우저에서 Cytanium 제어판으로 이동 하 고 선택 **웹** 를 선택한 **웹 사이트입니다.**

![제어판을 웹 사이트를 선택 합니다.](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

선택 된 **contosouniversity.com** 웹 사이트입니다.

![Contosouniversity.com 선택 제어판](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

선택 된 **웹 게시** 탭 합니다.

![컨트롤 패널 웹 게시 탭](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

웹 사용자 이름 및 암호를 입력 하 여 게시에 사용할 자격 증명을 만듭니다. 제어판에 로그온 하는 데 동일한 자격 증명을 입력할 수 있습니다. 누른 **사용**합니다.

![제어판에는 게시 자격 증명 만들기](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

클릭 **이 웹 사이트에 대 한 게시 프로필 다운로드**합니다.

![게시 프로필 컨트롤 패널 다운로드](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

파일을 열지 저장할지를 묻는 메시지가 나타나면이 저장 합니다.

![게시 프로필 파일 저장](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

**솔루션 탐색기** Visual Studio에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. **웹 게시** 대화 상자가 열리고를 **미리 보기** 탭의 **테스트** 프로필을 사용해 마지막 프로 파일 이기 때문에 선택 합니다.

선택 된 **프로필** 탭을 클릭 한 다음 **가져오기**합니다.

![게시 웹 마법사 가져오기 단추](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

에 **게시 설정 가져오기** 대화 상자에서를 *.publishsettings* 파일을 다운로드 하 고 클릭 **열기**합니다. 마법사의 모든 입력 필드를 사용 하 여 연결 탭으로 이동 합니다.

![게시 웹 마법사 연결 탭](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

.Publishsettings 파일 대상 URL 상자에서 사이트에 대 한 계획 된 영구 URL을 배치 하지만 해당 도메인을 아직 구매 하지 않은, 경우 임시 URL을 사용 하 여 값을 바꿉니다. 예를 들어 URL은  *[ http://contosouniversity.com.vserver01.cytanium.com ](http://contosouniversity.com.vserver01.cytanium.com)합니다.* 이 확인란의 유일한 목적은 브라우저에 자동으로 열립니다 후 성공적으로 배포 후 URL을 지정 하는 것입니다. 이 비워 두면만 결과 이면 브라우저 배포 후 자동으로 시작 되지 않습니다.

클릭 **연결 유효성 검사** 설정이 올바른지 고 서버에 연결할 수 있는지 확인 합니다. 앞서 살펴본 것 처럼 녹색 확인 표시가 성공적으로 연결 되었는지 확인 합니다.

연결 유효성 검사를 클릭 하면 표시 될 수 있습니다는 **인증서 오류** 대화 상자. 이렇게 하면 서버 이름을 예상 대로 인지 확인 합니다. 인 경우 선택 **Visual Studio의 이후 세션에 대 한이 인증서를 저장할** 클릭 **Accept**합니다. (이 오류는를 배포 하는 URL에 대 한 SSL 인증서를 구매 비용을 방지 하려면 호스팅 공급자를 선택 하는 의미 하는 데 사용 합니다. 유효한 인증서를 사용 하 여 보안 연결을 설정 하려는 호스팅 공급자에 문의 합니다.)

![인증서 오류](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

**다음**을 클릭합니다.

에 **데이터베이스** 부분을 **설정** 탭, 동일한 입력 테스트에 대 한 입력 값을 게시 프로필. 드롭다운 목록에서 필요한 연결 문자열을 찾을 수 있습니다.

- 에 대 한 연결 문자열 상자에 **SchoolContext,** 선택 `Data Source=|DataDirectory|School-Prod.sdf`
- 아래 **SchoolContext**를 선택 **Code First 마이그레이션을 적용**합니다.
- 에 대 한 연결 문자열 상자에 **DefaultConnection**선택 `Data Source=|DataDirectory|aspnet-Prod.sdf`
- 아래 **DefaultConnection**를 그대로 둡니다 **데이터베이스 업데이트** 선택을 취소 합니다.

![게시 웹 마법사 설정 탭](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

**다음**을 클릭합니다.

에 **미리 보기** 탭을 클릭 **미리 보기 시작** 복사 될 파일의 목록을 보려면. 로컬 컴퓨터의 IIS에 배포한 경우 앞서 본 것과 동일한 목록이 표시 됩니다.

게시 하기 전에 Web.Production.config 변환 파일을 적용할 수 있도록 프로필의 이름을 변경 합니다. 선택 된 **프로필** 탭을 클릭 **프로필 관리**합니다.

![게시 웹 마법사 프로필 관리](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

에 **웹 게시 프로필 편집** 대화 상자에서 프로덕션 프로필 선택를 클릭 **이름 바꾸기**, 프로덕션에 프로필 이름을 변경 합니다. 누른 **닫기**합니다.

![웹 게시 프로필 대화 상자 편집](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

**게시**를 클릭합니다.

응용 프로그램 호스팅 공급자에 게시 됩니다. 결과에 표시 된 **출력** 창입니다.

![배포 후 출력 창](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

브라우저에 입력 한 URL로 자동으로 열립니다 **대상 URL** 상자에 **연결** 탭의 **웹 게시** 마법사. 실행할 때와 사이트 Visual Studio에서 이제 없습니다 "(테스트)"는 점을 제외 하 고 동일한 홈 페이지를 표시 또는 제목 표시줄에 "(Dev)" 환경 표시기입니다. 이 나타내는 환경 표시기 *Web.config* 변환 제대로 작동 합니다.

> [!NOTE]
> 제목에 "(테스트)" 여전히 표시 되 면 삭제 합니다 *obj* 폴더 ContosoUniversity 프로젝트를 다시 배포 합니다. 소프트웨어의 시험판 버전에서는 이전에 적용 된 변환 파일 (Web.Test.config) 적용 될 수 다시 프로덕션 프로필 사용 됩니다.


[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

데이터베이스 액세스 일으키는 페이지를 실행 하기 전에 Elmah 발생 하는 모든 오류를 기록할 수 있는지 확인 합니다.

## <a name="setting-folder-permissions-for-elmah"></a>Elmah에 대 한 폴더 권한 설정

이 시리즈의 이전 자습서에서 점만 기억 한다면 응용 프로그램에 Elmah 오류 로그 파일을 저장 하는 위치 하는 응용 프로그램에서 특정 폴더에 대 한 쓰기 권한이 있는지 확인 해야 합니다. IIS에 로컬 컴퓨터를 배포한 경우 해당 사용 권한을 수동으로 설정 합니다. 이 섹션에서는 Cytanium에서 사용 권한을 설정 하는 방법을 배웁니다. (일부 호스팅 공급자도 이렇게 설정할 수 있습니다; 쓰기 권한이 있는 하나 이상의 미리 정의 된 폴더를 제공할 수 있습니다. 이런 경우에서 해야 지정된 된 된 폴더를 사용 하도록 응용 프로그램을 수정 합니다.)

Cytanium 제어판에서 폴더 사용 권한을 설정할 수 있습니다. 선택한 컨트롤에 패널 URL로 이동 **파일 관리자**합니다.

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

에 **파일 관리자** 상자에서 **contosouniversity.com** 차례로 **wwwrooot** 응용 프로그램의 루트 폴더를 보려면. 옆에 자물쇠 아이콘을 클릭 **Elmah**합니다.

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

에 **파일**/**폴더 사용 권한을** 창에서를 **읽기** 하 고 **작성** 에 대 한 확인란  **contosouniversity.com** 누릅니다 **권한 설정**합니다.

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

Elmah에 대 한 쓰기 액세스에 있는지 확인 합니다 *Elmah* 오류가 발생 하 고 다음 Elmah 오류 보고서를 표시 하 여 폴더입니다. 같은 잘못 된 URL을 요청 *Studentsxxx.aspx*합니다. 이전에 표시 된 대로 합니다 *GenericErrorPage.aspx* 페이지입니다. 클릭 합니다 **로그 아웃** 링크를 선택한 다음 실행 *Elmah.axd*합니다. 표시는 **로그인** 페이지 먼저 확인 하는 *Web.config* 변환 Elmah 권한 부여를 성공적으로 추가 합니다. 로그인 한 후 방금 발생 한 오류를 표시 하는 보고서를 표시 됩니다.

[![Elmah.axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>프로덕션 환경에서 테스트

실행 합니다 **학생** 페이지입니다. 응용 프로그램 데이터베이스를 만들려고 Code First 마이그레이션을 트리거하는 처음에 School 데이터베이스에 액세스 하려고 시도 합니다. 잠시의 지연 후 페이지에 표시 됩니다, 학생이 없는 있는지 표시 됩니다.

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

실행 된 **강사** 페이지 시드 데이터를 데이터베이스에서 강사 데이터를 삽입 했습니다 있는지 확인 합니다.

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

테스트 환경에서 수행한 것 처럼 데이터베이스 업데이트를 프로덕션 환경에서 작동 하지만 일반적으로 원하지 않는 프로덕션 데이터베이스에 테스트 데이터를 입력 하는 확인 해야 합니다. 이 자습서에서는 테스트에서 수행한 동일한 메서드를 사용 합니다. 하지만 해당 데이터베이스의 유효성을 검사 하는 메서드를 찾을 하려는 실제 응용 프로그램 업데이트가 성공 프로덕션 데이터베이스에 테스트 데이터를 도입 하지 않고. 일부 응용 프로그램에서 개체 추가 및 삭제 하는 데 적합 수 있습니다.

학생을 추가 하 고 다음에서 입력 된 데이터를 볼 합니다 **학생** 페이지 데이터베이스의 데이터를 업데이트할 수 있는지 확인 합니다.

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

권한 부여 규칙을 선택 하 여 올바르게 작동 하는지 유효성을 검사 **업데이트 크레딧** 에서 합니다 **과정** 메뉴. 합니다 **로그인** 페이지가 표시 됩니다. 관리자 계정 자격 증명 입력, 클릭 **로그인**, 및 **업데이트 크레딧** 페이지가 표시 됩니다.

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

로그인에 성공 하면 합니다 **업데이트 크레딧** 페이지가 표시 됩니다. (단일 관리자 계정)으로 ASP.NET 멤버 자격 데이터베이스 성공적으로 배포 되었는지 나타냅니다.

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

이제 성공적으로 배포 및 테스트 사이트 이므로 사용할 수 있는 공개적으로 인터넷을 통해.

## <a name="creating-a-more-reliable-test-environment"></a>더 신뢰할 수 있는 테스트 환경 만들기

에 설명 된 대로 합니다 [테스트 환경에 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서에서는 가장 신뢰할 수 있는 테스트 환경을 프로덕션 계정 마찬가지로는 호스팅 공급자에서 두 번째 계정이 됩니다. 이 두 번째 호스팅 계정에 등록할 수 없으므로 테스트 환경으로 로컬 IIS를 사용 하는 데 비해 것입니다. 하지만 프로덕션 사이트 오류 또는 중단을 방지 하는 것이 비용을 결정할 수 있습니다.

만들기 및 테스트 계정에 배포 프로세스의 대부분은 이미 작업을 프로덕션 배포 유사 합니다.

- 만들기는 *Web.config* 변환 파일입니다.
- 호스팅 공급자에서 계정을 만듭니다.
- 새 게시 프로필을 만들고 테스트 계정에 배포 합니다.

### <a name="preventing-public-access-to-the-test-site"></a>테스트 사이트에 대 한 공용 액세스 방지

테스트 계정에 대 한 중요 한 고려 하는 것은 인터넷에서 라이브 않으려는 공용 사용 하는입니다. 사이트를 비공개로 유지 하려면 다음 방법 중 하나 이상을 사용할 수 있습니다.

- 테스트에 사용 하는 IP 주소 에서만에서 테스트 사이트에 액세스를 허용 하는 방화벽 규칙을 설정 하려면 호스팅 공급자에 게 문의 합니다.
- 공용 사이트의 URL과 유사한 되도록 URL을 가장 합니다.
- 사용 된 *robots.txt* 는 검색 엔진을 크롤링하지 않습니다 테스트 사이트 및 보고서 링크를 검색 결과에 파일입니다.

이러한 메서드의 첫 번째는 분명히 가장 안전 하 고 있지만 프로시저에 대 한 각 호스팅 공급자와 관련 되며이 자습서에서 다루지 것입니다. 테스트 계정 URL로 이동 하 여 IP 주소만 허용 하도록 호스팅 공급자를 사용 하 여 정렬 수행, 이론적 없는 경우 탐색 하는 검색 엔진에 대 한 걱정 합니다. 하지만 경우에 배포를 *robots.txt* 파일 방화벽 규칙 꺼져 우발적 경우 백업으로 좋은 방법입니다.

합니다 *robots.txt* 프로젝트 폴더의 파일과 그 안에 다음 텍스트를 있어야 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

합니다 `User-agent` 줄 지시 파일의 규칙은 모든 검색 엔진 웹 크롤러 (로봇)에 적용 되는 검색 엔진 및 `Disallow` 줄 페이지가 없는 사이트를 크롤링할 수 해야 지정 합니다.

수행할 원할 프로덕션 배포에서이 파일을 제외 해야 하므로 프로덕션 사이트를 카탈로그에 검색 엔진입니다. 이렇게 하려면 참조 **I에서 제외할 수 특정 파일 또는 폴더 배포?** 에 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)합니다. 프로덕션 게시 프로필에 대해서만 제외를 지정 하는 있는지 확인 합니다.

두 번째 호스팅 계정 만들기는 필요 하지는 않지만 비용 추가 두면 유용할 수 있는 테스트 환경을 사용 하는 방법입니다. 다음 자습서에서는 테스트 환경으로 IIS를 사용 하 여 계속 합니다.

다음 자습서에서는 응용 프로그램 코드를 업데이트 하 고 변경 내용을 테스트 및 프로덕션 환경에 배포 합니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
