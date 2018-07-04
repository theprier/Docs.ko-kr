---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Contact Manager 솔루션 설정 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 다운로드 개발자 워크스테이션에서 로컬로 실행 하려면 Contact Manager 솔루션을 구성 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: a7675a793909ec4d95164ee47a3a43f73600c5bc
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366691"
---
<a name="setting-up-the-contact-manager-solution"></a>Contact Manager 솔루션 설정
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 다운로드 개발자 워크스테이션에서 로컬로 실행 하려면 Contact Manager 솔루션을 구성 하는 방법을 설명 합니다.


## <a name="system-requirements"></a>시스템 요구 사항

Contact Manager 솔루션을 로컬로 실행 하 고이 자습서에 설명 된 다른 작업을 수행 하 여 개발자 워크스테이션에서이 소프트웨어를 설치 해야 합니다.

- Visual Studio 2010 서비스 팩 1, Premium 또는 Ultimate Edition
- IIS (인터넷 정보 서비스) 7.5 Express
- SQL Server 2008 R2 Express
- IIS 웹 배포 도구 (웹 배포) 2.1 이상
- ASP.NET 4.0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

Visual Studio 2010을 제외 하 고 다운로드 하 고 수 이러한 제품 및 구성 요소를 통해 모든 최신 버전을 설치 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.

## <a name="download-and-extract-the-solution"></a>다운로드 하 고 솔루션을 추출

MSDN 코드 갤러리에서 Contact Manager 샘플 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)합니다.

## <a name="configure-and-run-the-solution"></a>구성 및 솔루션 실행

를 구성 및 로컬 컴퓨터에서 Contact Manager 솔루션을 실행 하려면 이러한 높은 수준의 단계를 수행 해야 합니다.

1. 없는 경우 하나 이미를 사용 하도록 설정 하는 멤버 자격 및 역할 관리 기능을 사용 하 여 로컬 ASP.NET 응용 프로그램 서비스 데이터베이스를 만듭니다.
2. 연결 문자열을 편집 합니다 *web.config* 파일을 로컬 SQL Server Express 인스턴스를 가리키도록 합니다.
3. Visual Studio 2010에서 솔루션을 실행 합니다.

이 섹션의 나머지 부분에서는 이러한 각 작업을 완료 하는 방법에 자세한 지침을 제공 합니다.

**응용 프로그램 서비스 데이터베이스를 만들려면**

1. Visual Studio 2010 명령 프롬프트를 엽니다. 이 작업을 수행 하는 **시작** 메뉴에서 **프로그램도**, 클릭 **Microsoft Visual Studio 2010**, 클릭 **Visual Studio Tools**, 차례로 클릭 **Visual Studio 명령 프롬프트 (2010)** 합니다.
2. 명령 프롬프트에서 다음이 명령을 입력 하 고 enter 키를 누릅니다.

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. 사용 된 **– C** 데이터베이스 서버에 대 한 연결 문자열을 지정 하는 스위치입니다.
    2. 사용 된 **–** 응용 프로그램 서비스 데이터베이스에 추가 하려는 기능을 지정 하는 스위치입니다. 이 예에서 **m** 멤버 자격 공급자에 대 한 지원을 추가 하려면 원하는 지 나타냅니다 및 **r** 역할 관리자에 대 한 지원을 추가할 것임을 나타냅니다.
    3. 사용 된 **– d** 응용 프로그램 서비스 데이터베이스에 대 한 이름을 지정 하는 스위치입니다. 유틸리티의 기본 이름을 사용 하 여 데이터베이스를 만들기는이 스위치를 생략 하면 **aspnetdb**합니다.
3. 데이터베이스를 성공적으로 만들었으면, 명령 프롬프트 확인 메시지가 표시 됩니다.

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> Aspnet 대 한 자세한 내용은\_regsql 유틸리티 참조 [ASP.NET SQL Server 등록 도구 (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)합니다.


Contact Manager 솔루션의 연결 문자열을 SQL Server Express의 로컬 인스턴스를 가리키는지 확인 하려면 다음 단계가입니다.

**연결 문자열을 업데이트 하려면**

1. Visual Studio 2010에서 Contact Manager 솔루션을 엽니다.
2. 에 **솔루션 탐색기** 창 확장를 **ContactManager.Mvc** 프로젝트를 마우스 두 번 클릭 합니다 **Web.config** 노드.

    > [!NOTE]
    > ContactManager.Mvc 프로젝트에 두 개의 *web.config* 파일입니다. 프로젝트 수준 파일을 편집 해야 합니다.

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. 에 **connectionStrings** 요소인 명명 된 연결 문자열 확인 **ApplicationServices** 로컬 ASP.NET 응용 프로그램 서비스 데이터베이스를 가리킵니다.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. 에 **솔루션 탐색기** 창 확장를 **ContactManager.Service** 프로젝트를 마우스 두 번 클릭 합니다 **Web.config** 노드.

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. 에 **connectionStrings** 라는 연결 문자열에서 요소를 **ContactManagerContext**, 되어 있는지 확인 합니다 **데이터 원본** SQL의 로컬 인스턴스에 속성 Server Express입니다. 다른 연결 문자열에 아무 것도 변경할 필요가 없습니다.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. 열려 있는 모든 파일을 저장합니다.

이제 Contact Manager 솔루션을 로컬 컴퓨터에서 실행 하도록 준비 해야 합니다.

> [!NOTE]
> ASP.NET은 첫 번째 응용 프로그램 서비스 데이터베이스를 만들지 않고 다음이 단계를 수행 하면 처음으로 사용자를 만들려고 시도 하면 데이터베이스를 만듭니다. 그러나 수동으로 데이터베이스를 만드는 제어할 수 많은 지원 하려는 응용 프로그램 서비스 기능 집합입니다.


**Contact Manager 솔루션을 실행 하려면**

1. Visual Studio 2010에서 f5 키를 누릅니다.
2. Internet Explorer 시작 하 고 Contact Manager ASP.NET MVC 3 응용 프로그램의 URL을 요청 합니다. 기본적으로 응용 프로그램을 표시 합니다 **모든 연락처** 페이지입니다.

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. 연락처를 몇 개를 추가 하 고 응용 프로그램이 예상 대로 작동 하는지 확인 합니다.

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. 이동할 `http://localhost:50114/Account/Register` (다른 포트에서 응용 프로그램을 호스팅하는 경우 URL 조정). 사용자 이름, 전자 메일 주소 및 암호를 추가 하 고 계정을 성공적으로 등록할 수 있는지 확인 합니다.

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. 이동할 `http://localhost:50114/Account/LogOn` (다른 포트에서 응용 프로그램을 호스팅하는 경우 URL 조정). 방금 만든 계정을 사용 하 여 로그온 할 수 있는지 확인 합니다.

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. 디버깅을 중지 하려면 Internet Explorer를 닫습니다.

## <a name="conclusion"></a>결론

이 시점에서 로컬 컴퓨터에서 실행 되도록 Contact Manager 솔루션 완벽 하 게 구성 되어야 합니다. 이 자습서에서 다른 항목을 진행할 때 참조로 솔루션을 사용할 수 있습니다.

다음 항목인 [프로젝트 파일 이해](understanding-the-project-file.md), Contact Manager 솔루션 내에서 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법을 설명 합니다.

> [!div class="step-by-step"]
> [이전](the-contact-manager-solution.md)
> [다음](understanding-the-project-file.md)
