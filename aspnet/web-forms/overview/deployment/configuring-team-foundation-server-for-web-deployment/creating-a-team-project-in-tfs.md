---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: "TFS에서 팀 프로젝트를 만들면 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: 4cb0d72330086ecb8cd9e6fb70ce0a57698dda5a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-team-project-in-tfs"></a>TFS에서 팀 프로젝트 만들기
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.

## <a name="task-overview"></a>작업 개요

프로 비전 하 고 TFS에서 새 팀 프로젝트를 사용 하려면 같은 대략적인 단계를 완료 해야 합니다.

- 사용자에 게 새 팀 프로젝트를 만들 권한을 부여 합니다.
- 팀 프로젝트를 만듭니다.
- 프로젝트에서 작업 하는 팀 멤버에 권한을 부여 합니다.
- 일부 콘텐츠를 확인 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 설명 하 고 사용자와 각 프로시저에 대 한 책임을 가능성이 있는 작업 역할 식별 됩니다. 즉, 조직의 구조에 따라 각이 작업 수 있으므로 주의 해야 다른 사용자의 책임입니다.

작업은이 항목의 연습에서는 설치 되었으며 TFS를 구성 하 고 팀 프로젝트 컬렉션의 구성 프로세스의 일부로 만든 가정 합니다. 이러한 가정에 대 한 자세한 내용은 하 고 그렇지 않은 경우 보다 일반적인 배경 정보에 대 한 참조 [웹 배포를 위한 TFS 빌드 서버 구성](configuring-a-tfs-build-server-for-web-deployment.md)합니다.

## <a name="grant-permissions-to-the-team-project-creator"></a>팀 프로젝트 생성자에 게 권한을 부여합니다

새 팀 프로젝트를 만들기 위해 이러한 권한이 필요 합니다.

- 있어야는 **새 프로젝트를 만들** TFS 응용 프로그램 계층에 대 한 권한이 있습니다. 일반적으로 사용자를 추가 하 여이 권한을 부여는 **Project Collection Administrators** TFS 그룹입니다. **Team Foundation Administrators** 글로벌 그룹에도이 권한이 포함 됩니다.
- TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 모음 내에서 새 팀 사이트를 만들 수 있는 권한이 있어야 합니다. 일반적으로 SharePoint 그룹에 사용자를 추가 하 여이 권한을 부여 **모든 권한** SharePoint에 대 한 권한 사이트 모음입니다.
- SQL Server Reporting Services 기능을 사용 하는 경우의 멤버 여야 합니다는 **Team Foundation Content Manager** Reporting Services의 역할입니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람?

일반적으로 사람 또는 그룹에 TFS 배포를 운영 하는 이러한 프로시저도 수행 합니다.

매우 강력한 권한의 권한 집합 이기 때문에 새 팀 프로젝트는 일반적 만들어집니다 사용자의 작은 하위 집합에서 TFS 배포를 관리 하기 위한 책임입니다. 개발자는 일반적으로 권한은 할당 하지는 새 팀 프로젝트를 만드는 데 필요한 합니다.

### <a name="grant-permissions-in-tfs"></a>TFS에서 사용 권한을 부여 합니다.

첫 번째 상위 수준 작업은 사용자를 추가 하려면 사용자가 새 팀 프로젝트를 만들 수 있도록 하려는 경우는 **Project Collection Administrators** 팀 프로젝트 컬렉션에 대 한 그룹입니다.

**Project Collection Administrators 그룹에 사용자를 추가 하려면**

1. TFS 서버에서에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Team Foundation Server 2010**, 클릭 하 고 **Team Foundation 관리 콘솔**합니다.
2. 탐색 트리 보기에서 확장 **응용 프로그램 계층**, 클릭 하 고 **팀 프로젝트 컬렉션**합니다.

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. 에 **팀 프로젝트 컬렉션** 창에서 팀 프로젝트를 관리 하려는 컬렉션입니다.

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. 에 **일반** 탭을 클릭 **그룹 구성원 자격**합니다.

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. 에 **글로벌 그룹** 대화 상자는 **Project Collection Administrators** 그룹을 마우스 클릭 **속성**합니다.
6. 에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**, 클릭 하 고 **추가**합니다.

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. 에 **사용자, 컴퓨터 또는 그룹 선택** 새 팀 프로젝트를 만들 수 있도록 하려는 사용자의 사용자 이름을 클릭 하 여 대화 상자에서 **이름 확인**, 클릭 하 고 **확인** .

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. 에 **Team Foundation Server 그룹 속성** 대화 상자를 클릭 **확인**합니다.
9. 에 **글로벌 그룹** 대화 상자를 클릭 **닫기**합니다.

### <a name="grant-permissions-in-sharepoint-services"></a>SharePoint Services의 권한 부여

다음으로, TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 모음에 새 팀 사이트를 만들 수 있는 사용자 권한을 부여 해야 합니다.

**SharePoint 사이트 모음에 대 한 모든 권한을 부여 하려면**

1. Team Foundation Server 관리 콘솔에에 **팀 프로젝트 컬렉션** 페이지에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.
2. 에 **SharePoint 사이트** 탭에서 값을 확인는 **현재 기본 사이트 위치** URL입니다.

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. Internet Explorer를 열고 2 단계에서 기록해둔 URL로 이동 합니다.

    > [!NOTE]
    > 하지 로그인 Windows에는 팀 프로젝트 컬렉션을 만든 사용자로, 하는 경우 SharePoint에이 사용자로 로그인이 계속 해야 합니다.
4. 에 **사이트 작업** 메뉴를 클릭 하 여 **사이트 설정**합니다.

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. 에 **사이트 설정** 페이지의 **사용자 및 사용 권한**, 클릭 **사용자 및 그룹**합니다.
6. 왼쪽된 탐색 패널에서 클릭 **그룹**합니다.

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. 에 **사용자 및 그룹: 모든 그룹** 페이지 **그룹이이 사이트에 대 한 설정**합니다.

    ![](creating-a-team-project-in-tfs/_static/image9.png)

    > [!NOTE]
    > 나타날 수 있습니다는 **HTTP 404 찾을 수 없음** 오류 이중 HTTP 인코딩 버그 때문에 발생 합니다. 이 경우이 URL을 바꿉니다.   
    > [*사이트 컬렉션 URL*] /\_layouts/permsetup.aspx  
    > 예:  
    > http://tfs/sites/Fabrikam%20Web%20Projects/\_layouts/permsetup.aspx
8. 에 **그룹이이 사이트에 대 한 설정** 페이지에서 사용자를 팀 프로젝트를 만들고는 추가 **소유자** 그룹을 마우스 클릭 **확인**합니다.

    ![](creating-a-team-project-in-tfs/_static/image10.png)

사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만드는 설정에 대 한 자세한 내용은 참조 하십시오. [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/en-us/library/dd547204.aspx)합니다.

## <a name="create-a-new-team-project-and-add-users"></a>새 팀 프로젝트를 만들고 사용자 추가

필요한 사용 권한이 면 사용할 수 있습니다는 **팀 탐색기** 새 팀 프로젝트를 만들려면 Visual Studio 2010의 창. 이 방법은 필요한 모든 정보를 수집 하 고 TFS, SharePoint 및 SQL Server Reporting Services에서 필요한 작업을 수행 하는 마법사를 제공 합니다. 새 팀 프로젝트에 대 한 권한을 추가 하 고 콘텐츠를 수정할 수 있도록 개발자 팀의 멤버에 권한을 부여 해야 합니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람?

일반적으로 TFS 관리자 또는 개발자 팀 리더는이 절차를 수행합니다.

### <a name="create-a-new-team-project"></a>새 팀 프로젝트 만들기

다음 절차에는 TFS 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.

**새 팀 프로젝트를 만들려면**

1. 에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Visual Studio 2010**를 마우스 오른쪽 단추로 클릭 **Microsoft Visual Studio 2010**, 클릭 하 고 **관리자 권한으로 실행**합니다.

    > [!NOTE]
    > 관리자 권한으로 Visual Studio 2010을 실행 하지 않으면, 새 팀 프로젝트 마법사는 마지막 단계에서 실패 합니다.
2. 경우는 **사용자 계정 컨트롤** 대화 상자가 나타나면 클릭 **예**합니다.
3. Visual Studio에서에 **팀** 메뉴를 클릭 하 여 **Team Foundation Server에 연결**합니다.

    > [!NOTE]
    > TFS 서버에 대 한 연결을 이미 구성 했다면 4-7 단계를 생략할 수 있습니다.
4. 에 **팀 프로젝트에 연결** 대화 상자를 클릭 **서버**합니다.
5. 에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **추가**합니다.
6. 에 **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**합니다.

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. 에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **닫기**합니다.
8. 에 **팀 프로젝트에 연결** 대화 상자에서 팀 선택에 연결 하려는 TFS 인스턴스에 프로젝트 컬렉션에 추가 하 고 클릭 하려는 **연결**합니다.

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. 에 **팀 탐색기** 창에서 마우스 오른쪽 단추로 팀 프로젝트 컬렉션을 누른 **새 팀 프로젝트**합니다.

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. 에 **새 팀 프로젝트** 대화 상자에서 이름과 팀 프로젝트에 대 한 설명을 입력 하 고 클릭 **다음**합니다.

    > [!NOTE]
    > 팀 프로젝트에 공백이 있으면 출력 경로에서 패키지를 배포 하는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하도록 제공 되 면 몇 가지 문제가 발생할 수 있습니다. 경로에 공백이 웹 배포 명령을 실행 하 훨씬 더 어렵게 만들 수 있습니다.

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. 에 **프로세스 템플릿 선택** 페이지에서 클릭 하 고 개발 프로세스를 관리 하는 데 사용할 프로세스 템플릿을 선택 **다음**합니다.

    > [!NOTE]
    > 프로세스 템플릿 TFS에 대 한 자세한 내용은 참조 하십시오. [프로세스 템플릿과 도구](https://msdn.microsoft.com/en-us/vstudio/aa718795)합니다.
12. 에 **팀 사이트 설정** 페이지 변경 하지 않은 기본 설정을 유지 하 고 클릭 **다음**합니다.
13. 이 설정을 만들거나 TFS 팀 프로젝트와 연결 된 SharePoint 팀 사이트를 식별 합니다. 개발 팀이이 사이트를 사용 설명서를 관리할를 토론에 참여, wiki 페이지를 만들고 코드와 관련 되지 않은 다른 다양 한 작업을 수행할 수 있습니다. 자세한 내용은 참조 [SharePoint 제품 간의 상호 작용 및 Team Foundation Server](https://msdn.microsoft.com/en-us/library/ms253177.aspx)합니다.
14. 에 **소스 제어 설정 지정** 페이지 변경 하지 않은 기본 설정을 유지 하 고 클릭 **다음**합니다.
15. 이 설정은 식별 하거나 루트 폴더 콘텐츠를 작동할 TFS 폴더 계층의 위치를 만듭니다.
16. 에 **팀 프로젝트 설정 확인** 페이지 **마침**합니다.
17. 때 새 팀 프로젝트가 성공적으로 만들어지면에 **팀 프로젝트를 만들었습니다** 페이지 **닫기**합니다.

### <a name="add-users-to-a-team-project"></a>팀 프로젝트에 사용자 추가

새 팀 프로젝트를 만들었으므로 이제 추가 하 고 공동 작업에 콘텐츠를 시작할 수 있도록 사용자에 게 권한을 부여할 수 있습니다.

**팀 프로젝트에 사용자를 추가 하려면**

1. Visual Studio 2010에서에 **팀 탐색기** 창, 팀 프로젝트를 마우스 오른쪽 단추로 클릭를 가리킨 **팀 프로젝트 설정**, 클릭 하 고 **그룹 멤버 자격**합니다.

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. 그렇게 하는 추가, 수정 및 소스 제어에서 코드를 제거 하는 사용자를 사용 하도록 설정 하려면 필요는 **참가자** 그룹입니다.
3. 에 **프로젝트 그룹** 대화 상자는 **참가자** 그룹을 마우스 클릭 **속성**합니다.

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. 에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**, 클릭 하 고 **추가**합니다.

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. 에 **사용자, 컴퓨터 또는 그룹 선택** 팀 프로젝트에 추가 하려는 사용자의 사용자 이름을 클릭 하 여 대화 상자에서 **이름 확인**, 클릭 하 고 **확인**합니다.

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. 에 **Team Foundation Server 그룹 속성** 대화 상자를 클릭 **확인**합니다.
7. 에 **프로젝트 그룹** 대화 상자를 클릭 **닫기**합니다.

## <a name="conclusion"></a>결론

이 시점에서 새 팀 프로젝트 되 사용할 수 있는 상태가 하 고 콘텐츠를 추가 하 고 공동 작업 개발 프로세스에 개발자 팀 시작할 수 있습니다.

다음 항목인 [소스 제어에 추가 콘텐츠](adding-content-to-source-control.md), 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다.

## <a name="further-reading"></a>추가 정보

TFS에서 팀 프로젝트를 만드는 방법에 광범위 한 지침을 참조 하십시오. [팀 프로젝트를 만들](https://msdn.microsoft.com/en-us/library/ms181477(v=VS.100).aspx)합니다. 사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만드는 설정에 대 한 자세한 내용은 참조 하십시오. [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/en-us/library/dd547204.aspx)합니다. 팀 프로젝트에 사용자를 추가 하는 방법에 대 한 자세한 내용은 참조 하십시오. [팀 프로젝트에 사용자 추가](https://msdn.microsoft.com/en-us/library/bb558971.aspx)합니다.

>[!div class="step-by-step"]
[이전](configuring-team-foundation-server-for-web-deployment.md)
[다음](adding-content-to-source-control.md)
