---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS에서 팀 프로젝트를 만들면 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: 9218a22ff221dc7067662c58ccd3e758fca493b7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824135"
---
<a name="creating-a-team-project-in-tfs"></a>TFS에서 팀 프로젝트 만들기
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

## <a name="task-overview"></a>작업 개요

프로 비전 하 고 TFS에서 새 팀 프로젝트를 사용 하 여, 이러한 높은 수준의 단계를 완료 해야 합니다.

- 새 팀 프로젝트를 생성 하는 사용자에 게 권한을 부여 합니다.
- 팀 프로젝트를 만듭니다.
- 프로젝트에서 작동 하는 팀 멤버에 권한을 부여 합니다.
- 일부 콘텐츠를 확인 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 표시 되 고 사용자 및 각 프로시저에 대 한 책임을 집니다 가능성이 있는 작업 역할을 식별 하는. 조직의 구조에 따라 이러한 각 작업 수를 다른 사용자의 책임에 유의 합니다.

작업은이 문서의 연습 설치 되었으며 TFS를 구성 하 고 팀 프로젝트 컬렉션 구성 프로세스의 일부로 만든 가정 합니다. 이러한 가정에 대 한 자세한 내용은 및 시나리오에 보다 일반적인 배경 정보에 대 한 참조 [웹 배포용 TFS 빌드 서버를 구성](configuring-a-tfs-build-server-for-web-deployment.md)합니다.

## <a name="grant-permissions-to-the-team-project-creator"></a>팀 프로젝트 생성기에 대 한 권한 부여

새 팀 프로젝트를 만들기 위해 이러한 권한이 필요 합니다.

- 있어야 합니다 **새 프로젝트를 만들** TFS 응용 프로그램 계층에 대 한 권한이 있습니다. 일반적으로 사용자를 추가 하 여이 권한을 부여 합니다 **Project Collection Administrators** TFS 그룹입니다. 합니다 **Team Foundation Administrators** 전역 그룹에도이 권한을 포함 합니다.
- TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 컬렉션 내의 새 팀 사이트를 만들 수 있는 권한이 있어야 합니다. 일반적으로 사용 하 여 SharePoint 그룹에 사용자를 추가 하 여이 권한을 부여 **전면적인** SharePoint에 대 한 권한 사이트 모음입니다.
- SQL Server Reporting Services 기능을 사용 하는 경우의 구성원 이어야 합니다 **Team Foundation Content Manager** Reporting Services의 역할입니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람?

일반적으로 개인 또는 TFS 배포를 관리 하는 방법과 그룹 이러한 프로시저도 수행 합니다.

사용 권한 집합을 높은 이기 때문에 새 팀 프로젝트 일반적으로 생성 됩니다 사용자의 작은 하위 집합에서 TFS 배포를 관리 하는 것에 대 한 책임을 사용 하 여. 개발자가 부여 되지 않습니다 일반적으로 새 팀 프로젝트를 만드는 데 필요한 사용 권한.

### <a name="grant-permissions-in-tfs"></a>TFS에서 권한 부여

첫 번째 상위 수준 작업 사용자를 추가 하는 사용자가 새 팀 프로젝트를 만들 수 있도록 하려는 경우는 **Project Collection Administrators** 팀 프로젝트 컬렉션에 대 한 그룹입니다.

**Project Collection Administrators 그룹에 사용자를 추가 하려면**

1. TFS 서버의는 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Team Foundation Server 2010**를 클릭 하 고 **Team Foundation 관리 콘솔**합니다.
2. 탐색 트리 뷰에서 확장 **응용 프로그램 계층**를 클릭 하 고 **팀 프로젝트 컬렉션**합니다.

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. 에 **팀 프로젝트 컬렉션** 창 팀 프로젝트를 관리 하려는 컬렉션입니다.

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. 에 **일반적인** 탭을 클릭 **그룹 멤버 자격**합니다.

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. 에 **글로벌 그룹** 대화 상자에서를 **Project Collection Administrators** 그룹을 마우스 클릭 **속성**합니다.
6. 에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**를 클릭 하 고 **추가**합니다.

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. 에 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 새 팀 프로젝트를 만들 수 있게 되기를 원하는 사용자의 사용자 이름을 클릭 **이름 확인**를 클릭 하 고 **확인** .

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. 에 **Team Foundation Server 그룹 속성** 대화 상자, 클릭 **확인**합니다.
9. 에 **글로벌 그룹** 대화 상자, 클릭 **닫기**합니다.

### <a name="grant-permissions-in-sharepoint-services"></a>SharePoint Services의 권한 부여

다음으로, TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 컬렉션에서 새 팀 사이트를 만들 수 있는 사용자 권한을 부여 해야 합니다.

**SharePoint 사이트 컬렉션에 대 한 모든 권한을 부여 하려면**

1. Team Foundation Server 관리 콘솔에서에 **팀 프로젝트 컬렉션** 페이지에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.
2. 에 **SharePoint 사이트** 탭에서 값을 확인 합니다 **현재 기본 사이트 위치** URL입니다.

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. Internet Explorer를 열고 2 단계에서 언급 한 URL로 이동 합니다.

    > [!NOTE]
    > 하지 로그인 Windows에는 팀 프로젝트 컬렉션을 만든 사용자로, SharePoint에 로그인이 사용자로 계속 해야 합니다.
4. 에 **사이트 작업** 메뉴에서 클릭 **사이트 설정**합니다.

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. 에 **사이트 설정** 페이지의 **사용자 권한과**, 클릭 **사용자 및 그룹**합니다.
6. 왼쪽된 탐색 창에서 클릭 **그룹**합니다.

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. 에 **사용자 및 그룹: 모든 그룹** 페이지에서 클릭 **그룹이이 사이트에 대 한 설정**합니다.

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > 표시 될 수 있습니다는 <strong>HTTP 404 찾을 수 없음</strong> 이중 HTTP 인코딩 버그로 인해 오류가 발생 했습니다. 이 경우이 사용 하 여 URL을 바꿉니다.   
   > `[site_collection_URL]/_layouts/permsetup.aspx` 예를 들어:  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. 에 **그룹이이 사이트에 대 한 설정** 페이지, 팀 프로젝트를 생성 하는 사용자를 추가 합니다 **소유자** 그룹을 마우스 클릭 **확인**합니다.

    ![](creating-a-team-project-in-tfs/_static/image10.png)

사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 하는 방법은 참조 하세요 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)합니다.

## <a name="create-a-new-team-project-and-add-users"></a>새 팀 프로젝트를 만들고 사용자를 추가 합니다.

사용자에 게 필요한 권한이 후 사용할 수 있습니다 합니다 **팀 탐색기** 새 팀 프로젝트를 만들려면 Visual Studio 2010의 창. 이 방법은 필요한 모든 정보를 수집 하 고 TFS, SharePoint 및 SQL Server Reporting Services에서 필요한 작업을 수행 하는 마법사를 제공 합니다. 추가 하 고 콘텐츠를 수정할 수 있도록 개발자 팀의 구성원에 게 새 팀 프로젝트에 대 한 권한을 부여 해야 합니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람?

일반적으로 TFS 관리자 또는 개발자 팀 리더는 이러한 절차를 수행 합니다.

### <a name="create-a-new-team-project"></a>새 팀 프로젝트 만들기

다음 절차에는 TFS 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.

**새 팀 프로젝트를 만들려면**

1. 에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Visual Studio 2010**를 마우스 오른쪽 단추로 클릭 **Microsoft Visual Studio 2010**, 클릭 하 고 **관리자 권한으로 실행**합니다.

    > [!NOTE]
    > 관리자 권한으로 Visual Studio 2010을 실행 하지 않으면, 새 팀 프로젝트 마법사에서 마지막 단계에서 실패 합니다.
2. 경우는 **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**합니다.
3. Visual Studio에서에 **Team** 메뉴에서 클릭 **Team Foundation Server에 연결**합니다.

    > [!NOTE]
    > TFS 서버에 연결을 이미 구성한 경우에 4 ~ 7 단계를 생략할 수 있습니다.
4. 에 **팀 프로젝트에 연결** 대화 상자, 클릭 **서버**합니다.
5. 에 **Team Foundation Server 추가/제거** 대화 상자, 클릭 **추가**합니다.
6. 에 **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 제공 하 고 클릭 **확인**합니다.

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. 에 **Team Foundation Server 추가/제거** 대화 상자, 클릭 **닫기**합니다.
8. 에 **팀 프로젝트에 연결** 대화 상자에서 팀을 선택 하려면 연결 하려는 TFS 인스턴스에 프로젝트 컬렉션에 추가 하 고 클릭 하려는 **Connect**합니다.

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. 에 **팀 탐색기** 창을 마우스 오른쪽 단추로 클릭 팀 프로젝트 컬렉션, 클릭 **새 팀 프로젝트**합니다.

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. 에 **새 프로젝트** 대화 상자에서 이름 및 팀 프로젝트에 대 한 설명을 제공 하 고 클릭 **다음**합니다.

    > [!NOTE]
    > 공백이 포함 된 팀 프로젝트에는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 출력 경로에서 패키지를 배포할 수에 도달 하면 문제가 발생할 수 있습니다. 경로에 공백이 웹 배포 명령을 실행 하는 훨씬 더 어렵게 만들 수 있습니다.

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. 에 **프로세스 템플릿 선택** 페이지에서 프로세스 템플릿을 사용 하 여 개발 프로세스를 관리 하 고 클릭 하려는 선택 **다음**합니다.

    > [!NOTE]
    > Tfs 프로세스 템플릿에 자세한 내용은 참조 [프로세스 템플릿 및 도구](https://msdn.microsoft.com/vstudio/aa718795)합니다.
12. 에 **팀 사이트 설정** 페이지에서 변경 하지 않고 기본 설정을 유지 하 고 클릭 **다음**합니다.
13. 이 설정을 만들거나 TFS 팀 프로젝트와 연결 된 SharePoint 팀 사이트를 식별 합니다. 개발 팀이이 사이트를 사용 설명서를 관리, 토론에 참여, wiki 페이지 만들기 및 코드에 관련 되지 않은 다른 다양 한 작업을 수행할 수 있습니다. 자세한 내용은 [SharePoint 제품 간의 상호 작용 및 Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx)합니다.
14. 에 **소스 제어 설정 지정** 페이지에서 변경 하지 않고 기본 설정을 유지 하 고 클릭 **다음**합니다.
15. 이 설정은 식별 하거나 콘텐츠에 대 한 루트 폴더로 할 TFS 폴더 계층의 위치를 만듭니다.
16. 에 **팀 프로젝트 설정 확인** 페이지에서 클릭 **마침**합니다.
17. 경우 새 팀 프로젝트를 성공적으로 생성 되는 **팀 프로젝트를 만들었습니다** 페이지에서 클릭 **닫기**합니다.

### <a name="add-users-to-a-team-project"></a>팀 프로젝트에 사용자를 추가 합니다.

새 팀 프로젝트를 만들었으므로 이제 추가 하 고 콘텐츠 공동 작업을 시작할 수 있도록 사용자에 게 권한을 부여할 수 있습니다.

**팀 프로젝트에 사용자를 추가 하려면**

1. Visual Studio 2010에서에 **팀 탐색기** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭을 가리킵니다 **팀 프로젝트 설정**, 클릭 하 고 **그룹 멤버 자격**.

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. 추가, 수정, 소스 제어에서 코드를 제거 하는 사용자를 사용 하도록 설정 하려면에 그렇게 해야 합니다 **참가자** 그룹입니다.
3. **프로젝트 그룹** 대화 상자를 선택 합니다 **참가자** 그룹을 마우스 클릭 **속성**합니다.

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. 에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**를 클릭 하 고 **추가**합니다.

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. 에 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 팀 프로젝트에 추가 하려는 사용자의 사용자 이름을 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. 에 **Team Foundation Server 그룹 속성** 대화 상자, 클릭 **확인**합니다.
7. 에 **프로젝트 그룹** 대화 상자, 클릭 **닫기**합니다.

## <a name="conclusion"></a>결론

이 시점에서 새 팀 프로젝트를 사용 하려면 준비 되어 개발자 팀 콘텐츠를 추가 하 고 공동 작업 개발 프로세스를 시작할 수 있습니다.

다음 항목인 [소스 제어에 추가 콘텐츠](adding-content-to-source-control.md), 소스 제어에 콘텐츠를 추가 하는 방법에 설명 합니다.

## <a name="further-reading"></a>추가 정보

TFS에서 팀 프로젝트 만들기에 대 한 광범위 한 지침을 참조 하세요 [팀 프로젝트를 만들](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)합니다. 사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 하는 방법은 참조 하세요 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)합니다. 팀 프로젝트에 사용자를 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [팀 프로젝트에 사용자 추가](https://msdn.microsoft.com/library/bb558971.aspx)합니다.

> [!div class="step-by-step"]
> [이전](configuring-team-foundation-server-for-web-deployment.md)
> [다음](adding-content-to-source-control.md)
