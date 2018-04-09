---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 소스 제어에 콘텐츠 추가 | Microsoft Docs
author: jrjlee
description: 이 Team Foundation Server (TFS) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다. 팀 proje에 솔루션 및 프로젝트를 추가 하는 방법을 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: c9c3a506d2745a6793661453a293732429d3e46e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-content-to-source-control"></a>소스 제어에 콘텐츠 추가
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 Team Foundation Server (TFS) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다. TFS의 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법을 설명 하 고 소스 제어에 프레임 워크 또는 어셈블리와 같은 외부 종속성을 추가 하는 방법을 설명 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.

## <a name="task-overview"></a>작업 개요

대부분의 경우에서 개발자 팀의 모든 멤버는 소스 제어에 콘텐츠를 추가 할 수 있어야 합니다. TFS에서 소스 제어에 솔루션을 추가 하려면 같은 대략적인 단계를 완료 해야 합니다.

- 팀 프로젝트에 연결 합니다.
- 로컬 컴퓨터의 폴더 구조를 서버에서 팀 프로젝트 폴더 구조를 매핑하십시오.
- 소스 제어에 솔루션 및 해당 내용을 추가 합니다.
- 소스 제어에는 외부 종속성을 추가 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다.

작업은이 항목의 연습에서는 콘텐츠를 관리할 새 TFS 팀 프로젝트를 이미 만든 가정 합니다. 새 팀 프로젝트를 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [TFS에서 팀 프로젝트를 만드는](creating-a-team-project-in-tfs.md)합니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람?

대부분의 경우에서 개발자 팀의 모든 멤버를 추가 및 특정 팀 프로젝트 내에서 콘텐츠를 수정할 수 있어야 합니다.

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>팀 프로젝트에 연결 하 고 폴더 매핑 만들기

소스 제어에 콘텐츠를 추가 하기 전에 팀 프로젝트에 연결 하 고 로컬 컴퓨터의 서버에서 폴더 구조 및 파일 시스템 간에 매핑을 설정 해야 합니다.

**로컬 경로 매핑한 팀 프로젝트에 연결 하려면**

1. 개발자 워크스테이션에서 Visual Studio 2010을 엽니다.
2. Visual Studio에서에 **팀** 메뉴를 클릭 하 여 **Team Foundation Server에 연결**합니다.

    > [!NOTE]
    > TFS 서버에 대 한 연결을 이미 구성 했다면 3-6 단계를 생략할 수 있습니다.
3. 에 **팀 프로젝트에 연결** 대화 상자를 클릭 **서버**합니다.
4. 에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **추가**합니다.
5. 에 **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**합니다.

    ![](adding-content-to-source-control/_static/image1.png)
6. 에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **닫기**합니다.
7. 에 **팀 프로젝트에 연결** 대화 상자에서 팀 선택에 연결 하려면 TFS 인스턴스 선택 프로젝트 컬렉션에 추가 하려는 팀 프로젝트를 선택 하 고 클릭 한 다음 **연결**합니다.

    ![](adding-content-to-source-control/_static/image2.png)
8. 에 **팀 탐색기** 창, 팀 프로젝트를 확장 하 고 두 번 클릭 **소스 제어**합니다.

    ![](adding-content-to-source-control/_static/image3.png)
9. 에 **소스 제어 탐색기** 탭을 클릭 **매핑되지**합니다.

    ![](adding-content-to-source-control/_static/image4.png)
10. 에 **지도** 대화 상자는 **로컬 폴더** 상자, 찾은 (만들거나) 역할을 팀 프로젝트에 대 한 루트 폴더를 클릭 한 다음 로컬 폴더 **지도**합니다.

    ![](adding-content-to-source-control/_static/image5.png)
11. 소스 파일을 다운로드 하도록 메시지가 면 클릭 **예**합니다.

    ![](adding-content-to-source-control/_static/image6.png)

이 시점에서 팀 프로젝트에 대 한 서버 쪽 폴더 개발자 워크스테이션의 로컬 폴더에 매핑 했습니다. 또한 팀 프로젝트에서 기존 내용을 로컬 폴더 구조에 다운로드 한 합니다. 소스 제어에 내용을 직접 추가를 시작할 수 있습니다.

## <a name="add-projects-and-solutions-to-source-control"></a>소스 제어에 프로젝트와 솔루션 추가

프로젝트 및 솔루션 소스 제어에 추가 하려면 먼저 로컬 컴퓨터에서 매핑된 팀 프로젝트에 대 한 폴더로 이동 해야 합니다. 다음에 서버와 동기화 할 콘텐츠에서 확인할 수 있습니다.

**소스 제어에 프로젝트를 추가 하려면**

1. 개발자 워크스테이션에서 팀 프로젝트에 매핑된 폴더 구조 내에서 적절 한 위치 프로젝트 및 솔루션을 이동 합니다.

    > [!NOTE]
    > 대부분의 조직에서는 소스 제어에서 프로젝트 및 솔루션을 구성 하는 방법을 대 한 기본 액세스를 해야 합니다. 폴더를 구조화 하는 방법에 대 한 지침을 참조 하십시오. [How To: Team Foundation Server에서 구조 Your 소스 제어 폴더](https://msdn.microsoft.com/library/bb668992.aspx)합니다.
2. Visual Studio 2010에서 솔루션을 엽니다.
3. 에 **솔루션 탐색기** 창 솔루션을 마우스 오른쪽 단추로 클릭 **소스 제어에 솔루션 추가**합니다.

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > TFS의 구조 콘텐츠를 조직 선호 하는 방법에 따라 소스 코드의 구성 하는 방법을 보다 세부적으로 제어를 제공 하는 개별적으로 소스 제어에 프로젝트를 추가 해야 합니다.
4. 확인 하는 **소스 제어 탐색기** 추가할 팀 프로젝트에 대 한 서버 폴더 구조 내에서 콘텐츠 탭에 표시 됩니다.

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > **소스 제어 탐색기** 더 이상 로컬 파일 시스템에 매핑된 폴더에 솔루션을 추가 하기 때문에 메시지를 표시 하는 사용 하 여 콘텐츠 탭에 표시 됩니다. 솔루션을 매핑되지 않은 위치에 있는 경우에서 TFS 및 로컬 파일 시스템 폴더 위치를 지정 하 라는 메시지가 표시 합니다.
5. 에 **소스 제어 탐색기** 탭에 **폴더** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭 (예를 들어 **ContactManager**)를 클릭 하 고 **체크 인 보류 중인 변경 내용을**합니다.
6. 에 **체크 인-소스 파일** 대화 상자에 설명을 입력 하 고 클릭 **체크 인**합니다.

    ![](adding-content-to-source-control/_static/image9.png)

이 시점에서 TFS의 소스 제어에 솔루션을 추가 했습니다.

## <a name="add-external-dependencies-to-source-control"></a>소스 제어에 외부 종속성 추가

소스 제어에 프로젝트 또는 솔루션을 추가 하는 경우 모든 파일 및 폴더를 프로젝트 또는 솔루션 내에서 추가 됩니다. 그러나 대부분의 경우에서 프로젝트 및 솔루션에 의존할 수 제대로 작동 하려면 로컬 어셈블리와 같은 외부 종속성. 코드를 성공적으로 빌드 팀 빌드 및 개발자 팀의 다른 멤버 수 있도록 소스 제어에 이러한 리소스를 추가 해야 합니다.

예를 들어 않아 샘플 솔루션에 대 한 폴더 구조에는 패키지 라는 폴더가 포함 됩니다. ADO.NET Entity Framework 4.1에 대 한 어셈블리 및 다양 한 지원 리소스를 포함합니다. 패키지 폴더 Contact Manager 솔루션의 일부가 아닙니다. 하지만 솔루션 없이 성공적으로 빌드되지 않습니다. 팀이 솔루션을 빌드하려면 빌드를 사용 하도록 설정 하려면 소스 제어에 패키지 폴더를 추가 합니다.

> [!NOTE]
> 패키지 폴더의 포함 여부는 Visual Studio 2010 용 NuGet 확장을 사용 하 여 솔루션에는 Entity Framework 또는 유사한 리소스를 추가 하면 어떤 일이 생기의 전형입니다.


**소스 제어에 프로젝트 이외의 콘텐츠를 추가 하려면**

1. (예: 패키지 폴더) 항목을 추가 로컬 파일 시스템에 매핑된 폴더 내에서 적절 한 위치에 있는지 확인 합니다.
2. Visual Studio 2010에서에 **팀 탐색기** 창, 팀 프로젝트를 확장 하 고 두 번 클릭 **소스 제어**합니다.

    ![](adding-content-to-source-control/_static/image10.png)
3. 에 **소스 제어 탐색기** 탭에 **폴더** 창에서 항목 또는 항목을 포함 하는 폴더를 추가 하려고 합니다.
4. 클릭는 **폴더에 항목 추가** 단추입니다.

    ![](adding-content-to-source-control/_static/image11.png)
5. 에 **소스 제어에 추가** 대화 상자에서 폴더 또는 항목을 추가 하 고, 클릭 한 다음 선택 **다음**합니다.

    ![](adding-content-to-source-control/_static/image12.png)
6. 에 **항목 제외** 탭에서 자동으로 제외 되었습니다 (예: 어셈블리)을 클릭 한 다음 필요한 항목을 선택 **항목 포함**합니다.

    ![](adding-content-to-source-control/_static/image13.png)
7. 에 **추가할 항목을** 탭에서 포함 하려는 모든 파일 나열 되 고 클릭 한 다음 확인 **마침**합니다.

    ![](adding-content-to-source-control/_static/image14.png)
8. 에 **소스 제어 탐색기** 창 클릭는 **체크 인** 단추입니다.

    ![](adding-content-to-source-control/_static/image15.png)
9. 에 **체크 인-소스 파일** 대화 상자에 설명을 입력 하 고 클릭 **체크 인**합니다.

이 시점에서 소스 제어에 솔루션에 대 한 외부 종속성을 추가 했으므로 있습니다.

## <a name="conclusion"></a>결론

이 항목에는 팀 프로젝트에 연결 하 고 폴더 구조를 매핑할 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다. 소스 제어에서 항목을 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [버전 제어를 사용 하 여](https://msdn.microsoft.com/library/ms181368.aspx)합니다.

다음 항목인 [웹 배포를 위한 TFS 빌드 서버 구성](configuring-a-tfs-build-server-for-web-deployment.md), 빌드 및 솔루션 배포를 TFS 팀 빌드 서버를 준비 하는 방법을 설명 합니다.

## <a name="further-reading"></a>추가 정보

TFS에서 소스 제어를 사용한 작업에 대 한 자세한 내용은 참조 하십시오. [버전 제어를 사용 하 여](https://msdn.microsoft.com/library/ms181368.aspx)합니다.

> [!div class="step-by-step"]
> [이전](creating-a-team-project-in-tfs.md)
> [다음](configuring-a-tfs-build-server-for-web-deployment.md)
