---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 만들고 컬렉션의 서버에서 웹 서버 팜을 구성 하는 팜 프레임 워크 WFF (웹) 2.0을 사용 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: ad557306cb4d3c62932c640b598f82d692bc74cf
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388295"
---
<a name="creating-a-server-farm-with-the-web-farm-framework"></a>웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 만들고 컬렉션의 서버에서 웹 서버 팜을 구성 하는 팜 프레임 워크 WFF (웹) 2.0을 사용 하는 방법을 설명 합니다.


WFF를 사용 하면 여러 부하 분산 된 웹 서버에서 웹 플랫폼 제품 및 구성 요소, 웹 응용 프로그램, 웹 사이트 및 구성 설정을 동기화 할 수 있습니다. 스테이징 및 프로덕션 환경에서 같은 둘 이상의 웹 서버를 해야 하는 시나리오에서 배포 및 구성 프로세스를 크게 간소화할 수 있습니다이 합니다. 단일 서버에 웹 응용 프로그램을 배포할 수 있습니다&#x2014;는 *주 서버*&#x2014;및 WFF 서버 팜의 모든 다른 웹 서버에서 해당 웹 응용 프로그램에 자동으로 복제 됩니다.

## <a name="understanding-the-web-farm-framework"></a>웹 팜 프레임 워크 이해

프로 비전, 관리 및 웹 서버 그룹에 콘텐츠를 배포 하려면 WFF 2.0을 사용할 수 있습니다. 세 가지 주요 서버 역할의 WFF 배포 구성 됩니다.

- 합니다 *컨트롤러 서버*합니다. 이 서버를 사용 하 여 만들고 WFF 서버 팜을 구성 합니다. Controller 서버를 웹 플랫폼 구성 요소, 구성 설정 및 서버 팜의 웹 서버 사이 응용 프로그램의 동기화를 관리합니다. 컨트롤러 서버의 WFF 2.0을 설치 하 고 컨트롤러 서버는 각 서버 팜의 서버에 WFF 에이전트를 설치에 키를 누릅니다. WFF 서버 팜에, controller 서버를 개념적으로 속하지 및 단일 컨트롤러 서버에는 여러 서버 팜을 관리할 수 있습니다. 이 시나리오에서는 준비 서버 팜 및 프로덕션 서버 팜 만들기 및 관리를 단일 WFF 컨트롤러 서버를 사용 합니다.
- 합니다 *주 서버*합니다. 각 WFF 서버 팜에 단일 주 서버를 포함합니다. 웹 플랫폼 구성 요소를 설치 하거나 주 서버에 응용 프로그램을 배포할 때의 WFF 서버 팜의 다른 모든 서버에 변경 내용을 동기화 합니다.
- 합니다 *보조 서버*합니다. 각 WFF 서버 팜에서 하나 이상의 보조 서버가 포함 됩니다. 서버 팜 내에서 모든 보조 서버를 주 서버로 변경 내용이 복제 됩니다.

이러한 서버 역할 Fabrikam, Inc. 스테이징 및 프로덕션 환경에 연결 하는 방법을 보여 줍니다.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

이 시나리오에서는 프로덕션 환경과 스테이징 환경 둘 다로 구성 됩니다 WFF 서버 팜. 단일 WFF 컨트롤러 서버 팜 모두 관리합니다. 각 서버 팜 내에서 주 서버로 변경 내용을 모든 보조 서버에 복제 됩니다.

스테이징 및 프로덕션 환경을 구성 하려면 먼저 WFF 2.0의 주요 개념을 숙지 하려면 다음이 문서를 읽는 것이 좋습니다.

- [IIS 7에 대 한 Web Farm Framework 2.0의 개요](https://go.microsoft.com/?linkid=9805126)
- [IIS 7에 대 한 Web Farm Framework 2.0을 사용 하 여 서버 팜을 설정](https://go.microsoft.com/?linkid=9805127)
- [시스템 및 IIS 7에 대 한 Web Farm Framework 2.0에 대 한 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a>작업 개요

작업은이 항목의 연습을 완료 하려면 3 개 이상의 서버가 해야&#x2014;하나의 WFF 컨트롤러, 서버 팜에 대 한 하나의 기본 웹 서버 및 서버 팜에 대 한 하나 이상의 보조 웹 서버입니다. 언제 든 지 WFF 서버 팜에 보조 서버를 더 추가할 수 있습니다. 높은 수준, 만들기 및 구성 해야 하는 스테이징 또는 프로덕션의 환경의 WFF 서버 팜:

- 인터넷 정보 서비스 (IIS) 7.5 및 WFF 2.0을 설치 하 여 컨트롤러 서버를 만듭니다.
- 일반적인 관리자 계정을 만들고 방화벽 예외를 구성 하 여 기본 및 보조 서버를 준비 합니다.
- 컨트롤러 서버의 IIS 관리자를 사용 하 여 서버 팜을 구성 합니다.
- 부하 분산 IIS 응용 프로그램 요청 라우팅 (ARR) 또는 대체는 부하 분산 기술을 사용 하 여 구성 합니다.

작업은이 항목의 연습에서는 Windows Server 2008 R2를 실행 하는 새로운 서버 빌드를 사용 하 여 시작 하 고 있음을 가정 합니다. 를 시작 하기 전에 각 서버에 대 한을 확인 합니다.

- Windows Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.
- 서버가는 도메인에 가입 된입니다.
- 서버에 고정 IP가 있습니다.

> [!NOTE]
> 참조 컴퓨터를 도메인에 가입 하는 방법은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [정적 IP 주소를 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다.


## <a name="create-the-wff-controller-server"></a>WFF 컨트롤러 서버 만들기

WFF 컨트롤러 서버를 만들려면 IIS 7 이상 및 WFF 2.0 이상을 설치 해야 합니다. 내부적으로 WFF (웹 배포)는 IIS 웹 배포 도구를 사용 2.x 팜에 서버를 동기화 합니다. WFF를 설치 하려면 웹 플랫폼 설치 관리자를 사용 하는 경우 설치 관리자를 자동으로 다운로드를 Web Deploy를 설치 합니다.

**WFF 컨트롤러 서버를 만들려면**

1. 다운로드 및 설치 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9739157)합니다.
2. 맨 위에 있는 합니다 **웹 플랫폼 설치 관리자 3.0** 창에서 클릭 **제품**합니다.
3. 왼쪽 탐색 창에서 창에서 클릭 **Server**합니다.
4. 에 **IIS 7 권장 구성** 행을 클릭 **추가**합니다.
5. 에 <strong>웹 팜 프레임 워크 2.</strong> <em>x</em> 행을 클릭 <strong>추가</strong>합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. **설치**를 클릭합니다. 웹 플랫폼 설치 관리자가 목록에 추가할 다른 다양 한 종속성과 함께 웹 배포 도구를 설치 하는 알 수 있습니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. 사용 조건을 검토 하 고 사용자가 약관에 동의 하면 클릭 **동의**합니다.
8. 설치가 완료 되 면 클릭 **완료**를 닫은 다음 합니다 **웹 플랫폼 설치 관리자 3.0** 창입니다.

## <a name="configure-the-primary-and-secondary-servers"></a>기본 및 보조 서버를 구성 합니다.

WFF 서버 팜을 만들려면 팜의 구성 하는 웹 서버에서 몇 가지 준비 작업을 완료 해야 합니다.

- 수 있도록 방화벽 예외를 추가 합니다 **Core Networking**, **원격 관리**, 및 **파일 및 프린터 공유** WFF 컨트롤러 서버와 통신 하는 기능 .
- 도메인 계정을 만듭니다 (예를 들어 **FABRIKAM\stagingfarm**) Active Directory에서 각 서버의 로컬 관리자 그룹에 추가 합니다. 서버 팜 관리자 계정으로이 계정은 사용 하 여 서버 팜을 만들면 됩니다.

Windows 방화벽에서 이러한 방화벽 예외를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [시스템 및 IIS 7에 대 한 Web Farm Framework 2.0에 대 한 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)합니다. 다른 방화벽 시스템, 제품 설명서를 참조 하십시오.

Windows Server 2008 R2의 로컬 관리자 그룹에 도메인 계정을 추가 하려면 다음 절차를 사용할 수 있습니다. 서버 팜에 추가 하려는 모든 서버에서이 절차를 수행 해야 하면&#x2014;즉, 각 보조 서버 및 주 서버에서 로컬 관리자 그룹에 동일한 도메인 계정을 추가 합니다.

**로컬 관리자 그룹에 도메인 계정을 추가 하려면**

1. 에 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **서버 관리자**합니다.
2. 에 **서버 관리자** 창의 트리 뷰 창에서 확장 **구성**를 확장 **로컬 사용자 및 그룹**를 클릭 하 고 **그룹**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. 에 **그룹** 창에 두 번 클릭 **관리자**합니다.
4. 에 **관리자 속성** 대화 상자, 클릭 **추가**합니다.
5. 에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자, 형식 (또는 찾아보기) 도메인 계정에 (예를 들어 **FABRIKAM\stagingfarm**)를 클릭 하 고 **확인**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. 에 **관리자 속성** 대화 상자, 클릭 **확인**합니다.

서버를 서버 팜에 추가할 준비가 됩니다. 주 서버에서의 경우 전 서버 팜을 만든 후 또는 응용 프로그램 요구 사항에 맞게 서버를 구성할 수 있습니다&#x2014;두 경우 모두는 WFF는 동기화 서버 제품, 구성 요소에 같거나 구성 배포 하 여 보조 서버입니다. 편의상이 자습서에서는 서버 팜 만들기를 마쳤으면 주 서버를 구성 하겠습니다을 가정 합니다.

## <a name="create-the-wff-server-farm"></a>WFF 서버 팜 만들기

이 시점에서 모든 서버 준비가 WFF 서버 팜에 추가 합니다.

- WFF 컨트롤러 서버에 설치 했습니다.
- 기본 및 보조 웹 서버에서 방화벽 예외를 구성 했습니다.
- 기본 및 보조 웹 서버에서 로컬 관리자 그룹에 도메인 계정을 추가 했습니다.

다음 단계 WFF에서 서버 팜을 만드는 것입니다. WFF 컨트롤러 서버의 IIS 관리자에서이 수행할 수 있습니다.

**WFF 서버 팜을 만들려면**

1. WFF 컨트롤러 서버의는 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.
2. 에 **연결** 창, 로컬 서버 노드를 마우스 오른쪽 단추로 클릭 **서버 팜**를 클릭 하 고 **서버 팜 만들기**합니다.
3. 에 **서버 팜 만들기** 대화 상자 서버 팜에 대 한 의미 있는 이름을 입력 합니다 (예를 들어 **스테이징 팜**), 선택한 후 **서버 팜 프로 비전**합니다.
4. 사용자 이름 및 각 서버의 로컬 관리자 그룹에 추가한 도메인 계정의 암호를 입력 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. **다음**을 클릭합니다.
6. 에 **서버 추가** 페이지 선택 주 서버의 정규화 된 도메인 이름 (FQDN)을 입력 **주 서버**를 클릭 하 고 **추가**합니다.
7. 이 시점에서 WFF 제공한 자격 증명을 사용 하 여 주 서버에 연결 하려고 합니다. 연결에 성공 하는 경우 주 서버를 추가할 테이블에는 **서버 추가** 페이지입니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > 보았을 것입니다 **부하 분산에 사용할 수 있는** 기본적으로 선택 됩니다. WFF 부하 분산을 구현 하 여 여러 서버 팜에 웹 서버 요청을 분산 함으로써 IIS ARR 모듈을 사용 합니다. 대부분의 경우에만 선택을 취소 합니다 **부하 분산에 사용할 수 있는** 타사 부하 분산 솔루션을 대신 사용 하려는 경우 옵션입니다.
8. 에 **서버 추가** 페이지에서 첫 번째 보조 서버의 FQDN을 입력 하 고 클릭 **추가**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. 팜에 추가 보조 서버에 대해 7 단계를 반복 하 고 클릭 **완료**합니다.

WFF 서버 팜 작동 되 고 실행 됩니다. 모든 웹 플랫폼 제품 또는 주 서버에서 모든 웹 응용 프로그램 또는 주 서버에 배포 하는 콘텐츠를 설치 하는 구성 요소 자동으로 프로 비전 할 모든 보조 서버에 있습니다.

WFF 광범위 하 고 복잡 한 항목은 및에서 자세히 알아보십시오 합니다 [IIS 7 용 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트입니다. 그러나 당분간, 가지 주의 해야 하는 두 가지 기능 영역

- *응용 프로그램 프로 비전* 서버 팜의 모든 보조 서버에서 웹 응용 프로그램 및 구성 설정과 같은 기본 서버에서 콘텐츠를 복제 하는 프로세스입니다. 예를 들어, 기본 스테이징 서버로 Contact Manager 샘플 솔루션을 배포 하는 경우 WFF 응용 프로그램 프로 비전 프로세스는 모든 보조 준비 서버에이 솔루션을 배포 합니다. 응용 프로그램 프로 비전 프로세스는 기본적으로 30 초 마다 실행 됩니다.
- *플랫폼 프로 비전* 웹 플랫폼 제품 및 주 서버에서 구성 요소 서버 팜의 모든 보조 서버를 동기화 하는 프로세스입니다. 예를 들어, 기본 스테이징 서버에서 ASP.NET MVC 3을 설치 하는 경우 플랫폼 프로 비전 프로세스는 웹 플랫폼 설치 관리자를 모든 보조 준비 서버에서 ASP.NET MVC 3을 설치 하려면 사용 합니다. 플랫폼 프로 비전 프로세스는 기본적으로 5 분 마다 실행 됩니다.

관리할 수 있습니다 기본 응용 프로그램 및 플랫폼 프로 비전 설정 IIS 관리자에서 WFF 컨트롤러 서버.

**응용 프로그램 및 설정을 프로 비전 하는 플랫폼 탐색**

1. IIS 관리자에서에 **연결** 창의 서버 팜을 선택 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. 에 **팜을** 창 두 번 클릭 **응용 프로그램 프로 비전**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. 알 수 있듯이 서버 팜의 주 서버와 보조 서버 간의 웹 콘텐츠 및 구성 설정을 30 초 마다 동기화를 현재 구성 됩니다.
4. 클릭 **다시**를 차례로 클릭 한 다음 **플랫폼 프로 비전**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. 알 수 있듯이 서버 팜의 현재 웹 플랫폼 제품 및 구성 요소는 주 서버와 보조 서버 간에 5 분 마다 동기화 하도록 구성 됩니다.
6. 클릭 **다시**입니다.
7. 서버 팜의 웹 플랫폼 제품을 즉시 동기화를 강제로는 **동작** 창 클릭 **프로 비전 플랫폼**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > 플랫폼 프로 비전 하는 데 시간이 소요 될 수 있습니다. 설치 관리자 프로세스 서버 팜의 보조 서버의 백그라운드에서 실행 됩니다.
8. 프로 비전 프로세스를 완료 하려면 충분 한 시간을 허용한 후에 제품 및 주 서버에 추가한 구성 요소는 보조 서버에서 복제 이제 확인할 수 있습니다. 보조 서버에 로그온을 사용 하는 예를 들어 합니다 **서버 관리자** 창 웹 서버 역할 설치 되어 있는지 확인 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. 또한 다양 한 웹 플랫폼 구성 요소를 추가한 적이 있는지를 확인 하려면 설치 된 프로그램 목록을 확인할 수 있습니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a>부하 분산 구성

웹 팜을 만들면 일종의 로드 균형 조정 웹 서버 간에 HTTP 요청을 분산로 설정 해야 합니다. Windows Server 2008 네트워크 부하 분산, IIS ARR 또는 타사 소프트웨어 또는 하드웨어 기반 부하 분산 솔루션을 수 있습니다.

WFF는 IIS arr.와 밀접 하 게 통합 되도록 설계 되었습니다. 이 통합을 활용 하려면 WFF 컨트롤러 서버에 ARR 모듈을 설치 해야 합니다. 하 한 다음 직접 컨트롤러 서버에 모든 웹 트래픽을 일반적으로 도메인 이름 시스템 (DNS) 레코드를 구성 하 여. Controller 서버를 서버 가용성 및 기타 다양 한 조건에 따라 팜에 서버 사이에서 들어오는 요청을 분산 한 다음 됩니다.

> [!NOTE]
> WFF;를 사용 하 여 ARR을 사용할 필요가 없습니다. WFF 타사 부하 분산 솔루션을 사용 하 여 작동 하도록 구성할 수 있습니다. 자세한 내용은 [IIS 7에 대 한 Web Farm Framework 2.0의 개요](https://go.microsoft.com/?linkid=9805126)합니다.


ARR을 사용 하 여 부하 분산는 복잡 한 주제를 가장는이 자습서에서 다루지 않습니다. 그러나 ARR 모듈을 설치 하 고 로드 균형 조정을 시작 하려면 다음 절차를 사용할 수 있습니다.

**WFF 컨트롤러 서버에 부하 분산을 설정 하려면**

1. WFF 컨트롤러 서버에서 웹 플랫폼 설치 관리자를 시작 합니다.
2. 맨 위에 있는 합니다 **웹 플랫폼 설치 관리자 3.0** 창에서 클릭 **제품**합니다.
3. 왼쪽 탐색 창에서 창에서 클릭 **Server**합니다.
4. 에 **응용 프로그램 요청 라우팅 2.5** 행을 클릭 **추가**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. 클릭 **설치**에 대 한 지침을 따릅니다 합니다 **웹 플랫폼 설치** 창입니다.
6. 설치가 완료 되 면 IIS 관리자를 시작 및 합니다 **연결** 창 서버 팜에 노드를 클릭 합니다. 여러 새 아이콘에 추가 된 합니다 **팜을** 창.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. 에 **팜을** 창 두 번 클릭 **부하 분산**합니다.
8. 에 **부하 분산** 창의 선택 부하 분산 알고리즘 (예를 들어 **요청과 이상**).

    > [!NOTE]
    > 부하 분산 알고리즘 및 기타 구성 설정에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 요청 라우팅 모듈이](https://go.microsoft.com/?linkid=9805130)합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. 에 **동작** 창 클릭 **적용**합니다.

이제 기본 서버 팜의 서버에 대 한 분산을 구성 했습니다. 하 여 웹 팜 컨트롤러 서버에 모든 트래픽을 직접, 하는 경우 요청 선택한 부하 분산 알고리즘 및 가용성에 따라 팜에 서버 간에 배포 됩니다.

ARR을 사용 하 여 분산을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 요청 라우팅 모듈이](https://go.microsoft.com/?linkid=9805130)합니다.

## <a name="monitor-the-server-farm"></a>모니터 서버 팜

언제 든 지 IIS 관리자를 통해 컨트롤러 서버에서 서버 팜의 상태를 모니터링할 수 있습니다. 에 **연결** 창에 서버 팜의 확장 한 다음 클릭 **서버**합니다. 가운데 창에는 최근 활동의 추적 로그와 함께 팜의 각 서버의 요약이 표시 됩니다.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a>결론

WFF 서버 팜을 시작 및 실행 됩니다. 원하는 어떤 배포 방법을 지원 하려면 주 서버를 구성할 수 있습니다&#x2014;세부 정보에 대 한 추가 정보 섹션을 참조 하세요&#x2014;되 고 구성 서버 팜의 각 보조 서버에서 복제 됩니다.

## <a name="further-reading"></a>추가 정보

모든 측면을 구성 하 고는 WFF를 사용 하 여에 대 한 자세한 지침을 참조 하세요. 합니다 [IIS 7 용 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트입니다.

> [!div class="step-by-step"]
> [이전](configuring-a-database-server-for-web-deploy-publishing.md)
> [다음](configuring-deployment-properties-for-a-target-environment.md)
