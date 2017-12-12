---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: "웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 만들고 컬렉션의 서버에서 웹 서버 팜을 구성 하는 웹 팜 wff (프레임 워크) 2.0을 사용 하는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 2458abc863a83364f90fc9d6edaace897c23b4c9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-server-farm-with-the-web-farm-framework"></a>웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 만들고 컬렉션의 서버에서 웹 서버 팜을 구성 하는 웹 팜 wff (프레임 워크) 2.0을 사용 하는 방법을 설명 합니다.


WFF 여러 부하 분산 된 웹 서버에서 웹 플랫폼 제품 및 구성 요소, 웹 응용 프로그램, 웹 사이트 및 구성 설정을 동기화 할 수 있습니다. 스테이징 및 프로덕션 환경 같은 둘 이상의 웹 서버를 필요한 시나리오가 크게 배포 및 구성 프로세스를 간소화할 수 있습니다. 단일 서버 & #x 2014; 웹 응용 프로그램을 배포할 수는 *주 서버*& #x 2014; 및 WFF가 해당 웹 응용 프로그램 서버 팜에 있는 모든 다른 웹 서버에 자동으로 복제 합니다.

## <a name="understanding-the-web-farm-framework"></a>웹 팜 프레임 워크 이해

프로 비전, 관리 및 콘텐츠를 웹 서버 그룹을 배포 하려면 WFF 2.0을 사용할 수 있습니다. 세 가지 주요 서버 역할의 WFF 배포 구성 됩니다.

- *컨트롤러 서버*합니다. 이 서버를 사용 하 여 만들고 WFF 서버 팜을 구성할 수 있습니다. 컨트롤러 서버는 웹 플랫폼 구성 요소, 구성 설정 및 응용 프로그램 서버 팜에 웹 서버 간의 동기화를 관리합니다. 컨트롤러 서버에서 WFF 2.0을 설치 하 고 컨트롤러 서버에 에이전트가 설치 되 고 WFF 각 서버 팜의 서버에서 키를 누릅니다. 컨트롤러 서버 개념적으로에 속하지 않은 모든 WFF 서버 팜 및 단일 컨트롤러 서버에 여러 서버 팜을 관리할 수 있습니다. 이 시나리오에서는 준비 서버 팜 및 프로덕션 서버 그룹 만들기 및 관리를 단일 WFF 컨트롤러 서버를 사용 합니다.
- *주 서버*합니다. 각 WFF 서버 팜에서 단일 주 서버를 포함 합니다. 웹 플랫폼 구성 요소를 설치 하거나 하면 주 서버에 응용 프로그램 배포는 WFF 서버 팜의 다른 모든 서버에 변경 내용을 동기화 합니다.
- *보조 서버*합니다. 각 WFF 서버 팜에서 하나 이상의 보조 서버가 포함 됩니다. 서버 팜 내에서 모든 보조 서버에 주 서버에 적용 한 변경 내용 복제 됩니다.

이러한 서버 역할 Fabrikam, Inc. 스테이징 및 프로덕션 환경에 어떻게 관련 되는지를 보여 줍니다.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

이 시나리오에서는 프로덕션 환경과 준비 환경을 둘 다로 구성 됩니다 WFF 서버 팜. 단일 WFF 컨트롤러 서버 두 그룹을 관리합니다. 각 서버 팜 내에서 주 서버에 변경 내용을 모든 보조 서버에 복제 됩니다.

스테이징 및 프로덕션 환경을 구성 하려면 먼저 WFF 2.0의 주요 개념을 잘 이해 하려면 다음이 문서를 읽는 것이 좋습니다.

- [IIS 7에 대 한 Web Farm Framework 2.0의 개요](https://go.microsoft.com/?linkid=9805126)
- [Web Farm Framework 2.0 서버 팜에서 IIS 7에 대 한 설정](https://go.microsoft.com/?linkid=9805127)
- [시스템 및 IIS 7에 대 한 웹 팜 프레임 워크 2.0에 대 한 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a>작업 개요

작업 및이 항목의 연습을 완료 하려면 해야 3 개 이상 서버 & #x 2014; 하나의 WFF 컨트롤러, 서버 팜에 대 한 기본 웹 서버 및 서버 팜에 대 한 하나 이상의 보조 웹 서버입니다. 언제 든 지 WFF 서버 팜에 보조 서버를 더 추가할 수 있습니다. 상위 수준, 만들기 및 구성 해야 스테이징 또는 프로덕션 환경에 대 한 WFF 서버 팜:

- 인터넷 정보 서비스 (IIS) 7.5 및 WFF 2.0을 설치 하 여 컨트롤러 서버를 만듭니다.
- 일반적인 관리자 계정을 만들고 방화벽 예외를 구성 하 여 기본 및 보조 서버를 준비 합니다.
- 컨트롤러 서버에서 IIS 관리자를 사용 하 여 서버 팜을 구성 합니다.
- IIS 응용 프로그램 요청 라우팅 (ARR) 또는 대체는 부하 분산 기술을 사용 하 여 부하 분산을 구성 합니다.

작업은이 항목의 연습에서는 Windows Server 2008 r 2를 실행 하는 새로운 서버 빌드도 시작 하는 가정 합니다. 각 서버에 대 한 시작 하기 전에 다음 사항을 확인.

- Windows Server 2008 R2 서비스 팩 1 및 가능한 모든 업데이트가 설치 됩니다.
- 서버가 도메인에 가입 합니다.
- 서버에 고정 IP 주소입니다.

> [!NOTE]
> 참조 컴퓨터는 도메인에 가입에 대 한 자세한 내용은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/en-us/library/cc725618(v=WS.10).aspx)합니다. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [고정 IP 주소 구성](https://technet.microsoft.com/en-us/library/cc754203(v=ws.10).aspx)합니다.


## <a name="create-the-wff-controller-server"></a>WFF 컨트롤러 서버 만들기

WFF 컨트롤러 서버를 만들려면 IIS 7 이상와 WFF 2.0 이상을 설치 해야 합니다. 내부적으로 WFF (웹 배포) IIS 웹 배포 도구를 사용 2.x 팜에 서버를 동기화 합니다. WFF를 설치 하는 웹 플랫폼 설치 관리자를 사용 하는 경우 설치 관리자는 자동으로 다운로드 하 드립니다 웹 배포를 설치 합니다.

**WFF 컨트롤러 서버를 만들려면**

1. 다운로드 및 설치는 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9739157)합니다.
2. 맨 위에 있는 **웹 플랫폼 설치 관리자 3.0** 창 클릭 **제품**합니다.
3. 왼쪽 탐색 창에서 창에서 클릭 **서버**합니다.
4. 에 **IIS 7 권장 구성** 행에서 클릭 **추가**합니다.
5. 에 **웹 팜 프레임 워크 2.** *x* 행에서 클릭 **추가**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. **설치**를 클릭합니다. 웹 플랫폼 설치 관리자 설치 목록에 웹 배포 도구 다른 다양 한 종속성과 함께 추가 있는지 확인 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. 라이선스 조건을 검토 하 고 사용자가 약관에 동의 하는 경우 클릭 **동의**합니다.
8. 설치가 완료 되 면 클릭 **마침**, 한 다음 닫습니다는 **웹 플랫폼 설치 관리자 3.0** 창.

## <a name="configure-the-primary-and-secondary-servers"></a>기본 및 보조 서버를 구성 합니다.

WFF 서버 팜 만들기 전에 팜의 구성 하는 웹 서버에서 일부 준비 작업을 완료 해야 합니다.

- 허용 하는 방화벽 예외가 추가 **핵심 네트워킹**, **원격 관리**, 및 **파일 및 프린터 공유** WFF 컨트롤러 서버와 통신 하는 기능 .
- 도메인 계정을 만듭니다 (예를 들어 **FABRIKAM\stagingfarm**) Active Directory에서 각 서버에서 로컬 관리자 그룹에 추가 합니다. 서버 팜을 만들 때이 계정은 서버 팜 관리자 계정으로 사용 합니다.

Windows 방화벽에서 다음 방화벽 예외를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [시스템 및 IIS 7에 대 한 Web Farm Framework 2.0에 대 한 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)합니다. 다른 방화벽 시스템, 제품 설명서를 참조 하십시오.

Windows Server 2008 r 2의 로컬 관리자 그룹에 도메인 계정을 추가 하려면 다음 절차를 사용할 수 있습니다. 서버 팜 & #x 2014;에 추가할 모든 서버에서이 절차를 수행 해야 즉, 주 서버 및 각 보조 서버에서 로컬 관리자 그룹에 동일한 도메인 계정을 추가 합니다.

**로컬 관리자 그룹에 도메인 계정을 추가 하려면**

1. 에 **시작** 메뉴에서 **관리 도구**, 클릭 하 고 **서버 관리자**합니다.
2. 에 **서버 관리자** 창의 트리 뷰 창에서 확장 **구성**, 확장 **로컬 사용자 및 그룹**, 클릭 하 고 **그룹**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. 에 **그룹** 창에서 두 번 클릭 **관리자**합니다.
4. 에 **Administrators 속성** 대화 상자를 클릭 **추가**합니다.
5. 에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자, 형식 (또는 찾아보기) 도메인 계정에 (예를 들어 **FABRIKAM\stagingfarm**)를 클릭 하 고 **확인**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. 에 **Administrators 속성** 대화 상자를 클릭 **확인**합니다.

서버를 서버 팜에 추가할 준비가 됩니다. 주 서버에서의 경우 서버 팜 & #x 2014 만든 후 전이나 응용 프로그램 요구 사항에 맞게 서버를 구성할 수 있습니다 해야 하며 두 경우 모두의 WFF는 서버는 동일한 제품 구성 요소를 배포 하 여 또는 보조 서버에 구성 합니다. 간단한 설명을 위해가이 자습서에서는 서버 팜을 만드는 했으면 주 서버를 구성 합니다을 가정 합니다.

## <a name="create-the-wff-server-farm"></a>WFF 서버 팜 만들기

이 시점에서 모든 서버 준비가 WFF 서버 팜에 추가 합니다.

- 이전에 설치한 WFF 컨트롤러 서버에 있습니다.
- 기본 및 보조 웹 서버에 방화벽 예외를 구성 했습니다.
- 기본 및 보조 웹 서버에 도메인 계정을 로컬 관리자 그룹에 추가 했습니다.

다음 단계 WFF에서 서버 팜을 만들어야 하는 것입니다. WFF 컨트롤러 서버에서 IIS 관리자에서이 수행할 수 있습니다.

**WFF 서버 팜을 만들려면**

1. WFF 컨트롤러 서버에서에 **시작** 메뉴에서 **관리 도구**, 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.
2. 에 **연결** 창에서 로컬 서버 노드를 마우스 오른쪽 단추로 클릭 **서버 팜**, 클릭 하 고 **서버 팜 만들기**합니다.
3. **서버 팜 만들기** 대화 상자에 서버 팜에 대 한 의미 있는 이름을 입력 합니다 (예를 들어 **준비 팜**)를 선택한 후 **서버 팜의 프로 비전**합니다.
4. 사용자 이름 및 각 서버의 로컬 관리자 그룹에 추가 하는 도메인 계정의 암호를 입력 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. **다음**을 클릭합니다.
6. 에 **서버 추가** 페이지 선택 주 서버의 정규화 된 도메인 이름 (FQDN)을 입력 **주 서버**, 클릭 하 고 **추가**합니다.
7. 이 시점에서 WFF 제공한 자격 증명을 사용 하 여 주 서버에 연결 하려고 시도 합니다. 연결 되 면 주 서버를 추가할 테이블에는 **서버 추가** 페이지.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > 발견할 수 있습니다는 **부하 분산에 사용할 수 있는** 기본적으로 선택 됩니다. WFF 배포 하는 로드 균형을 조정 함으로써 요청이 서버 팜의 웹 서버를 통해 IIS ARR 모듈을 사용 합니다. 대부분의 시나리오에서만 선택을 취소는 **부하 분산에 사용할 수 있는** 는 제 3 자 부하 분산 솔루션을 대신 사용 하려는 경우 옵션입니다.
8. 에 **서버 추가** 페이지의 첫 번째 보조 서버를 FQDN을 입력 하 고 클릭 **추가**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. 팜에서 추가 보조 서버에 대해 7 단계를 반복한 다음 클릭 **마침**합니다.

WFF 서버 팜의 지금 실행 되 고 있습니다. 모든 웹 플랫폼 제품 또는 주 서버 및 웹 응용 프로그램 또는 주 서버에 배포 콘텐츠를 설치 하는 구성 요소 자동으로 프로 비전 할 모든 보조 서버에 있습니다.

WFF 광범위 한 및 복잡 한 주제 이며에서 항목에 대 한 자세히 알아볼 수 있습니다는 [IIS 7 용 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트입니다. 시간 되는 반면 가지 있습니다에 주의 해야 하는 두 가지 기능 영역.

- *응용 프로그램 프로 비전은* 서버 팜에 있는 모든 보조 서버에서 주 서버와 같은 웹 응용 프로그램 및 구성 설정에서에서 콘텐츠를 복제 하는 프로세스입니다. 예를 들어 않아 샘플 솔루션 스테이징 주 서버에 배포 하는 경우 WFF 응용 프로그램 프로 비전 프로세스는 보조 준비 되 면 모든 서버에이 솔루션을 배포 합니다. 응용 프로그램 프로 비전 프로세스는 기본적으로 30 초 마다 실행 됩니다.
- *플랫폼 프로 비전은* 웹 플랫폼 제품 및 주 서버에서 구성 요소 서버 팜에 있는 모든 보조 서버를 동기화 하는 프로세스입니다. 예를 들어 기본 스테이징 서버에 ASP.NET MVC 3을 설치 하는 경우 플랫폼 프로 비전 프로세스는 모든 보조 준비 서버에서 ASP.NET MVC 3을 설치 하는 웹 플랫폼 설치 관리자를 사용 합니다. 플랫폼 프로 비전 프로세스는 기본적으로 5 분 마다 실행 됩니다.

관리할 수 있습니다 기본 응용 프로그램 및 플랫폼 프로 비전 설정을 IIS 관리자에서 WFF 컨트롤러 서버에서.

**탐색 응용 프로그램 및 플랫폼에 대 한 설정**

1. IIS 관리자에서에서 **연결** 창에서 서버 팜을 선택 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. 에 **서버 팜** 창에서 두 번 클릭 **응용 프로그램 프로 비전은**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. 볼 수 있듯이 서버 팜은 현재 주 서버와 보조 서버 간에 웹 콘텐츠 및 구성 설정을 30 초 마다 동기화 하도록 구성 됩니다.
4. 클릭 **다시**를 두 번 클릭 하 고 **플랫폼 프로 비전은**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. 볼 수 있듯이 서버 팜의 현재 웹 플랫폼 제품 및 구성 요소는 주 서버와 보조 서버 간에 5 분 마다 동기화 하도록 구성 됩니다.
6. 클릭 **다시**합니다.
7. 웹 플랫폼 제품을 즉시 동기화 하는 서버 팜의 강제로는 **동작** 창에서 클릭 **프로 비전 플랫폼**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > 플랫폼 프로 비전은 다소 시간이 걸릴 수 있습니다. 서버 팜에 있는 보조 서버에서 설치 프로세스가 백그라운드에서 실행 합니다.
8. 프로 비전 프로세스를 완료에 대 한 충분 한 시간을 허용한 후 제품 및 주 서버에 추가 하는 구성 요소가 보조 서버에서 복제 이제 확인할 수 있습니다. 예를 들어 수 보조 서버에 로그온 하 여 사용 하는 **서버 관리자** 웹 서버 역할 설치 되어 있는지 확인 하는 창입니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. 또한 다양 한 웹 플랫폼 구성 요소가 추가 되었는지 확인 하려면 설치 된 프로그램 목록을 확인할 수 있습니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a>부하 분산 구성

웹 팜을 만들 때 특정 형태의 부하 분산 웹 서버 간에 HTTP 요청을 분산을 설정 해야 합니다. Windows Server 2008 네트워크 부하 분산, IIS ARR 또는 제 3 자 소프트웨어 또는 하드웨어 기반의 부하를 분산 솔루션 수 있습니다.

WFF는 IIS arr.와 밀접 하 게 통합 되도록 설계 되었습니다. 이러한 통합을 활용 하려면 WFF 컨트롤러 서버에 ARR 모듈을 설치 합니다. 하면 다음 비롯 된 모든 웹 트래픽이 컨트롤러 서버를 일반적으로 DNS 도메인 이름 () 레코드를 구성 하 여 합니다. 그런 다음 컨트롤러 서버 팜에서 서버에 서버 가용성 및 다른 다양 한 기준에 따라 들어오는 요청으로 배포 합니다.

> [!NOTE]
> ARR을 사용 하 여 WFF;와 필요가 없습니다. WFF 타사 부하 분산 솔루션에 맞게 구성할 수 있습니다. 자세한 내용은 참조 [IIS 7에 대 한 Web Farm Framework 2.0의 개요](https://go.microsoft.com/?linkid=9805126)합니다.


ARR을 사용 하 여 부하 분산 대부분는이 자습서의 범위를 벗어나는 복잡 한 항목입니다. 그러나 하 ARR 모듈을 설치 하 고 로드 균형 조정을 시작 하려면 다음 절차를 사용할 수 있습니다.

**WFF 컨트롤러 서버에서 부하 분산을 설정 하려면**

1. WFF 컨트롤러 서버에서 웹 플랫폼 설치 관리자를 시작 합니다.
2. 맨 위에 있는 **웹 플랫폼 설치 관리자 3.0** 창 클릭 **제품**합니다.
3. 왼쪽 탐색 창에서 창에서 클릭 **서버**합니다.
4. 에 **응용 프로그램 요청 라우팅 2.5** 행에서 클릭 **추가**합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. 클릭 **설치**, 한 다음 지침에 따라는 **웹 플랫폼 설치** 창.
6. 설치가 완료 되 면 IIS 관리자를 시작 및는 **연결** 창에서 서버 팜 노드를 클릭 합니다. 에 추가 된 몇 가지 새로운 아이콘이 표시 된 **서버 팜** 창.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. 에 **서버 팜** 창에서 두 번 클릭 **부하 분산**합니다.
8. 에 **부하 분산** 창 부하 분산 알고리즘 (예를 들어 **이상 현재 요청**).

    > [!NOTE]
    > 부하 분산 알고리즘 및 기타 구성 설정에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 요청 라우팅 모듈이](https://go.microsoft.com/?linkid=9805130)합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. 에 **동작** 창에서 클릭 **적용**합니다.

이제 기본 부하 분산 서버 팜의 서버에 대 한 구성 했습니다. 컨트롤러 서버에 모든 웹 팜 트래픽을 지시 하는 경우 요청 배포 되 가용성에 따라 팜에 서버 및 선택한 부하 분산 알고리즘입니다.

ARR을 사용한 부하 분산을 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 요청 라우팅 모듈이](https://go.microsoft.com/?linkid=9805130)합니다.

## <a name="monitor-the-server-farm"></a>모니터 서버 팜

언제 든 지 IIS 관리자를 통해 컨트롤러 서버에서 서버 팜의 상태를 모니터링할 수 있습니다. 에 **연결** 창에서 서버 팜의 확장 한 다음 클릭 **서버**합니다. 가운데 창에는 최근 활동의 추적 로그와 함께 팜의 각 서버에 대 한 요약을 표시 됩니다.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a>결론

WFF 서버 팜을 실행 되 고 있어야 합니다. 어떤 배포 접근 & #x 2014 지원 하도록 주 서버를 구성할 수 있습니다; 세부 정보 및 2014; #x 및 구성에 대 한 추가 정보 섹션을 참조 서버 팜에 있는 각 보조 서버에 복제 됩니다.

## <a name="further-reading"></a>추가 정보

모든 측면을 구성 하 고는 WFF를 사용 하 여에 대 한 자세한 지침을 참조 하십시오.는 [IIS 7 용 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트입니다.

>[!div class="step-by-step"]
[이전](configuring-a-database-server-for-web-deploy-publishing.md)
[다음](configuring-deployment-properties-for-a-target-environment.md)
