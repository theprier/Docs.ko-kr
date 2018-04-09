---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
title: 보안 기본 사항 및 지원 ASP.NET (VB) | Microsoft Docs
author: rick-anderson
description: 이 일련의 partic에 대 한 액세스 권한을 부여 방문자가 웹 폼을 통해 인증에 대 한 기술 탐색 자습서의 첫 번째 자습서는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/13/2008
ms.topic: article
ms.assetid: ab68a92b-fc81-40a4-a7dc-406625d2c5d4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
msc.type: authoredcontent
ms.openlocfilehash: e62bb865e211a279b60f3120162ffc3c49cbdcc5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="security-basics-and-aspnet-support-vb"></a>보안 기본 사항 및 지원 ASP.NET (VB)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_vb.pdf)

> 일련의 방문자가 웹 폼을 통해 인증, 특정 페이지와 기능에 대 한 액세스 권한을 부여 하 고, ASP.NET 응용 프로그램에서 사용자 계정 관리에 대 한 기술 탐색 자습서의 첫 번째 자습서입니다.


## <a name="introduction"></a>소개

한 가지 포럼, 전자 상거래 사이트, 온라인 메일 웹 사이트, 포털 웹 사이트 및 소셜 네트워크 사이트를 모두 서로 공통 무엇 인가요? 모든 제공 *사용자 계정*합니다. 사용자 계정을 제공 하는 사이트는 다양 한 서비스를 제공 해야 합니다. 여기에 최소한 새 방문자 계정을 만들 수 있도록 해야 하 고 방문자가 반환에 로그인 할 수 있어야 합니다. 이러한 웹 응용 프로그램에서는 로그인된 한 사용자에 따라 결정을 내릴 수: 일부 페이지 또는 작업 제한 될 수 있습니다에 사용자를 로그인 하거나 로그; 사용자의 특정 하위 집합에만 다른 페이지 수 표시 정보 특정 로그인된 한 사용자에 하거나 표시 될 수 있습니다 더 많거나 적게 어떤 사용자가 페이지를 보고에 따라 정보를.

일련의 방문자가 웹 폼을 통해 인증, 특정 페이지와 기능에 대 한 액세스 권한을 부여 하 고, ASP.NET 응용 프로그램에서 사용자 계정 관리에 대 한 기술 탐색 자습서의 첫 번째 자습서입니다. 이 자습서의 과정 동안에 살펴보겠습니다 하는 방법:

- 식별 및 사용자가 웹 사이트에 로그인
- ASP를 사용 합니다. 사용자 계정을 관리 하기 위해 NET의 멤버 자격 프레임 워크
- 만들기, 업데이트 및 사용자 계정 삭제
- 웹 페이지, 디렉터리 또는 로그인된 한 사용자를 기반으로 특정 기능에 대 한 액세스를 제한 합니다.
- ASP를 사용 합니다. 역할에 사용자 계정을 연결할 NET의 역할 프레임 워크
- 사용자 역할 관리
- 웹 페이지, 디렉터리 또는 로그인된 한 사용자의 역할에 따라 특정 기능에 대 한 액세스를 제한 합니다.
- 사용자 지정 하 고 ASP를 확장 합니다. NET의 보안 웹 컨트롤

이러한 자습서를 간결 하 게 하는 프로세스를 통해 시각적으로 다량의 스크린 샷을 단계별 지침을 제공 하 게 조정 됩니다. 각 자습서 C# 및 Visual Basic 버전에서 사용할 수 있으며 사용 되는 전체 코드의 다운로드에 포함 됩니다. (이 첫 번째 자습서 높은 수준의 관점에서 보안 개념에 중점을 두고 및 따라서 관련된 코드는 포함 하지 않습니다.)

이 자습서에서는 중요 한 보안 개념 및 어떤 장치는 폼 인증, 권한 부여, 사용자 계정 및 역할 구현 지원 하기 위해 ASP.NET에서 사용할 수 있는 설명 합니다. 이제 시작 하겠습니다.

> [!NOTE]
> 보안은 실제, 기술에 걸쳐 있는 응용 프로그램의 중요 한 기능 및 정책 결정을 하며 높은 수준의 계획 및 도메인 기술 합니다. 이 자습서 시리즈 보안 웹 응용 프로그램을 개발 하기 위한 지침으로 적합 하지 않습니다. 대신, 폼 인증, 권한 부여, 사용자 계정 및 역할에 대해서만 설명 집중 합니다. 이러한 문제를 둘러싼 일부 보안 개념,이 시리즈에서 설명 하는 동안 다른 남겨진다는 탐색 되지 않은 상태입니다.


## <a name="authentication-authorization-user-accounts-and-roles"></a>인증, 권한 부여, 사용자 계정 및 역할

인증, 권한 부여, 사용자 계정 및 역할은 ´ ֿ ´ 경우가 매우 자주이 자습서 시리즈 웹 보안 컨텍스트 내에서 이러한 용어를 정의 하려면 빠른 잠시 하겠습니다 있도록 4 개의 용어입니다. 클라이언트 서버 모델 인터넷 등에서 서버를 요청 하는 클라이언트를 식별 해야 하는 많은 시나리오가 있습니다. *인증* 클라이언트의 id를 구축 방향을 얻기 위한 하는 프로세스입니다. 클라이언트는 성공적으로 확인 되었습니다 라고 *인증*합니다. 알 수 없는 클라이언트를 라고 *인증 되지 않은* 또는 *익명*합니다.

보안 인증 시스템을 포함 하는 다음 세 가지 패싯 중 하나 이상을: [사용자가 알고, 있는 항목 또는 항목은](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html)합니다. 대부분의 웹 응용 프로그램 클라이언트 예: 암호 또는 PIN을 알고 있는 것에 의존 합니다. -그녀의 사용자 이름 및 예를 들어 암호-사용자를 식별 하는 데 사용 되는 정보 라고 *자격 증명*합니다. 이 자습서 시리즈에 중점을 두고 *폼 인증*, 하는 사용자가 웹 페이지 양식에서 자신의 자격 증명을 제공 하 여 사이트에 로그인 하는 인증 모델. म 모든 발견 된 이러한 형식의 하기 전에 인증 합니다. 모든 전자 상거래 사이트로 이동 합니다. 체크 아웃할 준비가 되 면 웹 페이지에 텍스트 상자에 사용자 이름 및 암호를 입력 하 여 로그인 하 라는 메시지가 표시 됩니다.

클라이언트를 식별 하는 것 외에도 서버는 어떤 리소스 또는 기능 요청을 만드는 클라이언트에 따라 액세스할 수 있는 제한 해야 할 수 있습니다. *권한 부여* 특정 사용자에 게 특정 리소스 또는 기능에 액세스할 수 있는 권한을 있는지를 결정 하는 프로세스입니다.

A *사용자 계정* 는 특정 사용자에 대 한 정보를 유지 하는 저장소입니다. 사용자 계정에는 사용자의 로그인 이름 및 암호 등 사용자를 고유 하 게 식별 하는 정보가 포함 최소한으로 해야 합니다. 사용자 계정을 함께이 중요 한 정보 등이 포함 될 수 있습니다: 사용자의 전자 메일 주소입니다. 날짜 및 시간 계정을 만들었습니다. 날짜 및 시간 변경 내용이;에 대해 마지막 기록 첫 번째 및 마지막 이름입니다. 전화 번호입니다. 및 우편 발송 주소입니다. 폼 인증을 사용할 경우 사용자 계정 정보는 일반적으로 Microsoft SQL Server와 같은 관계형 데이터베이스에 저장 됩니다.

사용자 계정을 지 원하는 웹 응용 프로그램 사용자가 선택적으로 그룹화 할 수 있습니다 *역할*합니다. 역할은 사용자에 적용 되 고 권한 부여 규칙 및 페이지 수준 기능을 정의 하기 위한 추상화를 제공 하는 레이블. 예를 들어 웹 사이트는 웹 페이지의 특정 집합에 액세스 하려면 관리자를 제외한 다른 사람이 수 없게 하는 권한 부여 규칙으로 관리자 역할을 포함할 수 있습니다. 또한 모든 사용자 (관리자가 아닌 포함)에 액세스할 수 있는 페이지의 다양 한 추가 데이터를 표시 또는 관리자 역할에 사용자가 방문 하는 경우 추가 기능을 제공 될 수 있습니다. 역할을 사용 하 여 정의할 수 있습니다 이러한 권한 부여 규칙에 사용자가 사용자 대신 역할에서 역할 업그레이드 시작 합니다.

## <a name="authenticating-users-in-an-aspnet-application"></a>ASP.NET 응용 프로그램에서 사용자 인증

브라우저는 응용 프로그램 사용자가 브라우저의 주소 창 또는 번의 클릭으로 URL 링크에을 입력 한 [하이퍼텍스트 전송 프로토콜 (HTTP)](http://en.wikipedia.org/wiki/HTTP) 지정된 된 내용에 대 한 웹 서버에 대 한 요청을 구성 ASP.NET 페이지, 이미지, JavaScript 파일 또는 다른 형식의 콘텐츠입니다. 웹 서버는 요청된 된 콘텐츠를 반환 해야 합니다. 이 과정에서 다양 한 작업 요청을 수행한 사람과 id는 요청한 콘텐츠를 검색할 수 있는 권한이 있는지 여부를 포함 하는 요청에 대 한 확인 해야 합니다.

기본적으로 브라우저는 모든 종류의 식별 정보가 없는 HTTP 요청을 보냅니다. 하지만 경우 브라우저에 인증 정보는 웹 서버를 시작 합니다 인증 워크플로 요청 하는 클라이언트를 식별 하려고 합니다. 인증 워크플로 단계는 웹 응용 프로그램에서 사용 중인 인증 유형에 따라 다릅니다. ASP.NET에서는 세 가지 유형의 인증 지원: Windows, Passport, 및 폼입니다. 이 자습서 시리즈 폼 인증에 중점을 두고 있지만 비교 하 고 Windows 인증 사용자 저장소와 워크플로 대조해 설명 하겠습니다.

### <a name="authentication-via-windows-authentication"></a>Windows 인증을 통해 인증

Windows 인증 워크플로 다음 인증 방법 중 하나를 사용 합니다.

- 기본 인증
- 다이제스트 인증
- Windows 통합된 인증

세 가지 기술 모두 대략 같은 방식으로 작동:가 권한이 없는 경우 익명 요청이 도착 한, 웹 서버는 권한 부여를 나타내는 HTTP 응답을 계속 하려면 있어야 다시 보냅니다. 다음 브라우저의 사용자 이름 및 암호 (그림 1 참조)에 대 한 사용자 요청 하는 모달 대화 상자를 표시 합니다. 이 정보는 다음 HTTP 헤더를 통해 웹 서버에 다시 전송 됩니다.


![모달 대화 상자 사용자가 자격 증명 확인](security-basics-and-asp-net-support-vb/_static/image1.png)

**그림 1**: 모달 대화 상자 사용자가 자격 증명 확인


제공 된 자격 증명은 웹 서버의 Windows 사용자 저장소에 대해 유효성이 검사 됩니다. 즉, 웹 응용 프로그램에서 인증 된 각 사용자가 조직에 Windows 계정이 있어야 합니다. 인트라넷 시나리오에서 일반적입니다. 사실, 인트라넷 환경에서 Windows 통합 인증을 사용할 때 브라우저 웹 서버 함으로써 그림 1에 표시 되는 대화 상자를 생략 하는 네트워크에 로그온 하는 데 사용 되는 자격 증명으로 자동으로 제공 합니다. Windows 인증은 인트라넷 응용 프로그램에 매우 유용 하는 동안 적합 하지 않다고 일반적으로 인터넷 응용 프로그램에 대 한 사이트에서을 등록 하는 각 사용자에 대 한 Windows 계정을 만드는 원하지 않는 때문입니다.

### <a name="authentication-via-forms-authentication"></a>폼 인증을 통해 인증

반면에 폼 인증에는 인터넷의 웹 응용 프로그램에 적합 합니다. 폼 인증을 웹 폼을 통해 자격 증명을 입력 하 여 사용자를 식별 하는 점에 유의 하세요. 따라서 사용자가 인증 되지 않은 리소스에 액세스 하려고 하는 경우 자동으로 리디렉션됩니다 자격 증명을 입력할 수 있는 로그인 페이지에 있습니다. 전송 된 자격 증명은 다음 사용자 지정 사용자 저장소-일반적으로 데이터베이스에 대해 확인 됩니다.

전송 된 자격 증명을 확인 한 후 한 *폼 인증 티켓* 사용자에 대해 생성 됩니다. 이 티켓 사용자가 인증 된 사용자 이름 등의 id 정보에 포함 되어 있음을 나타냅니다. 폼 인증 티켓은 일반적으로 클라이언트 컴퓨터에 쿠키로 저장 됩니다. 따라서 웹 사이트에 대 한 후속 방문 로그인 한 후 사용자를 식별 하는 웹 응용 프로그램을 사용할 수 있게 HTTP 요청에 폼 인증 티켓을 포함 합니다.

그림 2 높은 수준의 유리한 지점 폼 인증 워크플로를 보여 줍니다. ASP.NET에서 인증 및 권한 부여 조각을 두 개의 별도 엔터티로 작동 하는 방법을 확인 합니다. 폼 인증 시스템 사용자를 식별 하거나 익명이 보고. 권한 부여 시스템을 사용자가 요청된 된 리소스에 액세스할 지 여부를 결정 합니다. 경우 (에 따라 그림 2에 익명으로 ProtectedPage.aspx 방문 하려고 할 때) 사용자 권한이 부여 되어, 폼 인증 시스템을 자동으로 사용자를 로그인 페이지로 리디렉션합니다 원인이 사용자 거부 된 권한 부여 시스템에서 보고 합니다.

사용자가 성공적으로 로그인 되 면 후속 HTTP 요청이 폼 인증 티켓을 포함 합니다. 폼 인증 시스템에는 단지 사용자 식별-사용자 요청 된 리소스에 액세스할 수 있는지 여부를 결정 하는 권한 부여 시스템입니다.


![폼 인증 워크플로](security-basics-and-asp-net-support-vb/_static/image2.png)

**그림 2**: 폼 인증 워크플로


다음 두 자습서에서 훨씬 더 자세히 폼 인증에 읽기[폼 인증의 개요는](an-overview-of-forms-authentication-vb.md) 및 [폼 인증 구성 및 고급 항목](forms-authentication-configuration-and-advanced-topics-vb.md)합니다. 에 대 한 자세한 ASP 합니다. NET의 인증 옵션 참조 [ASP.NET 인증](https://msdn.microsoft.com/library/eeyk640h.aspx)합니다.

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>웹 페이지, 디렉터리 및 페이지 기능에 대 한 액세스를 제한합니다.

ASP.NET에서 특정 사용자가 특정 파일 또는 디렉터리 액세스 권한 여부를 확인 하는 두 가지를 포함 되어 있습니다.

- **권한 부여 파일** -있으므로 액세스 제어 목록 (Acl)을 통해 이러한 파일에 대 한 액세스는 웹 서버의 파일 시스템에 상주 하는 파일을 지정할 수 있습니다 ASP.NET 페이지 및 웹 서비스 구현 됩니다. Acl은 Windows 계정에 적용 되는 권한 때문에 파일 권한 부여는 Windows 인증을 사용한 가장 많이 사용 됩니다. 폼 인증을 사용할 경우 모든 운영 체제 및 파일 시스템 수준 요청은 사이트를 방문 하는 사용자에 관계 없이 동일한 Windows 계정에 의해 실행 됩니다.
- **URL 권한 부여**-URL 권한 부여 페이지 개발자 Web.config에서 권한 부여 규칙을 지정 합니다. 이러한 권한 부여 규칙 기능에 사용자 또는 역할에 액세스할 수 있습니다 또는 거부 됩니다 특정 페이지 또는 응용 프로그램에 있는 디렉터리에 액세스 하지 못하도록 지정 합니다.

파일 권한 부여 및 URL 권한 부여는 특정 디렉터리에서 모든 ASP.NET 페이지 또는 특정 ASP.NET 페이지에 액세스 하기 위한 권한 부여 규칙을 정의 합니다. 이러한 기술을 사용 하 여 우리, 특정 사용자에 대 한 특정 페이지에 대 한 요청 거부 또는 일련의 사용자에 대 한 액세스를 허용 하 고 다른 모든 사용자에 대 한 액세스를 거부 하기 위해 ASP.NET 지시할 수 있습니다. 사용자의 모든 페이지에 액세스할 수 있었지만 페이지의 기능은 사용자에 따라 달라 집니다 시나리오의 경우는 어떨까요? 예를 들어 사용자 계정을 지 원하는 많은 사이트 내용이 나 다른 인증 된 사용자 또는 익명 사용자에 대 한 데이터를 표시 하는 페이지에는. 익명 사용자 인증된 된 사용자는 대신 다시 시작, 등과 같은 메시지가 표시 되는 반면에 로그인 하는 사이트에 대 한 링크를 표시 될 수 *Username* 를 로그 아웃 링크와 함께 합니다. 또 다른 예:는 입찰 파일 또는 항목 auctioning 여부에 따라 다양 한 정보를 볼 경매 사이트에 있는 항목을 볼 때.

페이지 수준의 조정은 이러한 선언적으로 또는 프로그래밍 방식으로 수행할 수 있습니다. 에 대 한 여러 콘텐츠를 표시 익명 인증 된 사용자가 끌어서 보다는 [LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 페이지에 해당 AnonymousTemplate 및 LoggedInTemplate 서식 파일에 적절 한 콘텐츠를 입력 합니다. 또는 확인할 수 있습니다 프로그래밍 방식으로 현재 요청이 인증 되는지 여부, 사용자를 역할 (있는 경우)에 속해 있습니다. 이 정보를 표시 하거나 숨길 페이지에서 표 또는 패널의 열을 사용할 수 있습니다.

이 시리즈 권한 부여에 집중 하는 세 개의 자습서가 포함 되어 있습니다. ***사용자 기반 권한 부여***; 특정 사용자 계정에 대 한 하나 이상의 디렉터리에 있는 페이지에 대 한 액세스를 제한 하는 방법을 검사 합니다. ***역할 기반 권한 부여*** 수준이; 마지막으로, 역할에서 권한 부여 규칙을 제공에 ***는 현재 로그온 한 사용자에 따라 콘텐츠 표시*** 자습서 탐색 하는 특정 수정 페이지의 내용 및 기능 페이지를 방문 하는 사용자를 기반 합니다. 에 대 한 자세한 ASP 합니다. NET의 권한 부여 옵션 참조 [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)합니다.

## <a name="user-accounts-and-roles"></a>사용자 계정 및 역할

ASP입니다. NET의 폼 인증에서는 사용자가 사이트에 로그인 하 고 페이지 방문할 때마다 기억 인증 된 상태 수에 대 한 인프라를 제공 합니다. 및 URL 권한 부여는 ASP.NET 응용 프로그램에서 특정 파일이 나 폴더에 대 한 액세스를 제한 하기 위한 프레임 워크를 제공 합니다. 그러나 두 기능을 사용자 계정 정보를 저장 하거나 역할을 관리 하기 위한 수단을 제공 합니다.

ASP.NET 2.0 이전 개발자가 자신의 사용자 및 역할 저장소 작성을 담당 했습니다. 에 있는 것도 사용자 인터페이스를 설계 하 고 필수적인 사용자에 대 한 코드는 로그인 페이지와 다른 규칙 으로부터 새 계정을 만들려면 페이지와 같은 계정 관련 페이지를 쓰는 데 필요한 후크입니다. Asp.net에서는, 다음과 같은 질문에 자신의 디자인 결정에 도달 하 게 구현 사용자 계정에 각 개발자는 기본 제공 사용자 계정 프레임 워크 없이 저장 하는 방법 암호나 다른 중요 한 정보가 있습니까? 하 고 어떤 지침 암호 길이 및 강도 관한 적용 해야 합니까?

오늘날 훨씬 간편 하 게 감사 하는 ASP.NET 응용 프로그램에서 사용자 계정을 구현는 *구성원 프레임 워크* 및 로그인 웹을 제어 하는 기본 제공 합니다. 멤버 자격 프레임 워크는 클래스에는 소수의 [System.Web.Security 네임 스페이스](https://msdn.microsoft.com/library/system.web.security.aspx) 필수 사용자 계정 관련 작업을 수행 하기 위한 기능을 제공 합니다. 멤버 자격 framework의 주요 클래스는는 [멤버 자격 클래스](https://msdn.microsoft.com/library/system.web.security.membership.aspx), 같은 메서드가 있는:

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- ValidateUser

멤버 자격 프레임 워크 사용 하는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 멤버 자격 프레임 워크의 API 구현에서 명확 하 게 구분 하 합니다. 이 공용 API를 사용 하는 개발자가 사용할 수 있지만 자율적 이며 해당 응용 프로그램의 사용자 지정 요구를 충족 하는 구현을 사용 하도록 합니다. 즉, 멤버 자격 클래스 (메서드, 속성 및 이벤트), 프레임 워크의 필수 기능을 정의 하지만 실제로 구현 세부 정보를 제공 하지 않습니다. 대신, 멤버 자격 클래스의 메서드는 실제 작업을 수행 하는 구성 된 공급자를 호출 합니다. 예를 들어, 멤버 자격 클래스 CreateUser 메서드가 호출 되 면 멤버 자격 클래스는 사용자 저장소의 세부 정보 모릅니다. 있는지 알 수 없으므로 경우 사용자가 유지 관리 되는 XML 파일 또는 다른 저장소 또는 데이터베이스입니다. 통화를 위임 하려면 어떤 공급자를 확인 하려면 웹 응용 프로그램의 구성을 검사 하는 멤버 자격 클래스 및 해당 공급자 클래스는 실제로 새 사용자 계정의 적절 한 사용자 저장소에 만듭니다. 그림 3이 상호이 작용을 보여 줍니다.

Microsoft은.NET Framework에 두 개의 멤버 자격 공급자 클래스를 제공:

- [ActiveDirectoryMembershipProvider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) -Active Directory 및 Active Directory ADAM (Application Mode) 서버에서 멤버 API를 구현 합니다.
- [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) -SQL Server 데이터베이스에 멤버 API를 구현 합니다.

이 자습서 시리즈의 SqlMembershipProvider에만 중점을 둡니다.


[![공급자 모델 사용 하면 다른 구현을를 원활 하 게 연결에 프레임 워크](security-basics-and-asp-net-support-vb/_static/image4.png)](security-basics-and-asp-net-support-vb/_static/image3.png)

**그림 03**: The 공급자 모델 사용 하면 다른 구현을를 원활 하 게 연결에 프레임 워크 ([전체 크기 이미지를 보려면 클릭](security-basics-and-asp-net-support-vb/_static/image5.png))


공급자 모델의 이점은 대체 구현을 Microsoft, 공급 업체 또는 개별 개발자가 개발 및 원활 하 게 멤버 자격 프레임 워크에 연결 될 수입니다. 예를 들어 Microsoft는 출시 했습니다 [Microsoft Access 데이터베이스에 대 한 멤버 자격 공급자](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi)합니다. 멤버 자격 공급자에 대 한 자세한 내용은 참조는 [공급자 Toolkit](https://msdn.microsoft.com/asp.net/aa336558.aspx), 100 개 이상의 페이지의 공급자 모델에 대 한 설명서, 샘플 사용자 지정 공급자, 멤버 자격 공급자의 연습을 포함 하 고 기본 제공 멤버 자격 공급자 (즉, ActiveDirectoryMembershipProvider 및 SqlMembershipProvider)에 대 한 소스 코드를 완료 합니다.

ASP.NET 2.0에는 또한 역할 프레임 워크가 추가 되었습니다. 멤버 자격 프레임 워크와 같은 역할 framework 공급자 모델 기반 만들어집니다. 해당 API를 통해 노출 되는 [역할 클래스](https://msdn.microsoft.com/library/system.web.security.roles.aspx) 세 개의 공급자 클래스와 함께 제공 되는.NET Framework 및:

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) -Active Directory 또는 ADAM 같은 권한 부여 관리자 정책 저장소, 역할 정보를 관리 합니다.
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) -SQL Server 데이터베이스에서 역할을 구현 합니다.
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) -방문자의 Windows 그룹에 따라 역할 정보를 연결 합니다. 이 메서드는 일반적으로 Windows 인증과 함께 사용 됩니다.

이 자습서 시리즈 SqlRoleProvider에만 중점을 둡니다.

공급자 모델은 단일 정방향 웹 API (멤버 자격 및 역할 클래스)를 포함 하는 이후 구현 세부 정보에 걱정할 필요 없이 해당 API와 관련 된 기능을 빌드할 수-페이지에서 선택한 공급자에 의해 처리 되는 것 개발자입니다. 이 통합된 API Microsoft 및 타사 공급 업체 웹 컨트롤 멤버 자격 및 역할 프레임 워크와 함께 해당 인터페이스를 작성할 수 있습니다. ASP.NET의 수와 함께 제공 [로그인 웹 컨트롤](https://msdn.microsoft.com/library/ms178329.aspx) 일반적인 사용자 계정 사용자 인터페이스를 구현 합니다. 예를 들어는 [Login 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) , 유효성을 검사 하 고 폼 인증을 통해 로그에 사용자가 자격 증명을 입력 합니다. [LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 인증 된 사용자 또는 익명 사용자에 게 다른 태그 또는 사용자의 역할에 따라 다른 태그를 표시 하기 위한 템플릿을 제공 합니다. 및 [CreateUserWizard 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx) 새 사용자 계정을 만들기 위한 단계별 사용자 인터페이스를 제공 합니다.

내부적 다양 한 로그인 컨트롤 멤버 자격 및 역할 프레임 워크와 상호 작용 합니다. 한 줄의 코드를 작성할 필요 없이 대부분의 로그인 컨트롤을 구현할 수 있습니다. 이후 자습서에서을 확장 하 고 해당 기능을 사용자 지정 기술을 포함 하 여 이러한 컨트롤을 더 자세히 살펴보겠습니다.

## <a name="summary"></a>요약

사용자 계정을 지 원하는 모든 웹 응용 프로그램 요구와 유사한 기능을 같은: 로그인과 해당 로그 페이지 방문할 때마다; 저장 된 상태에 있는 사용자를 위한 기능 계정을; 만드는 새 방문자가 웹 페이지 기능과 페이지 개발자에 게 어떤 리소스, 데이터 및 기능 어떤 사용자 또는 역할에 사용할 수를 지정 합니다. 태스크의 사용자 계정 및 역할 관리 및 인증 하 고 사용자 권한 부여 덕분에 폼 인증, URL 권한 부여 및 멤버 자격 및 역할 프레임 워크는 ASP.NET 응용 프로그램에서 수행 하기 위해 매우 쉽습니다.

다음 몇 가지 자습서의 과정 동안 단계별로 처음부터 다시 웹 응용 프로그램을 작성 하 여 이러한 측면을이 충분히를 살펴보겠습니다. 다음 두 자습서에서 자세히 폼 인증을 설명 합니다. 로그인 및 로그 아웃 한 방문자를 허용 하는 웹 응용 프로그램을 작성 하는 동안 모든-폼 인증 워크플로 작업에서 폼 인증 티켓을 분석할 보안 문제에 설명 하 고 폼 인증 시스템을 구성 하는 방법을 참조 살펴봅니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0 멤버 자격, 역할, 폼 인증 및 보안 리소스](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [ASP.NET 2.0 보안 지침](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET 인증](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [ASP.NET Login 컨트롤 개요](https://msdn.microsoft.com/library/ms178329.aspx)
- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [어떻게 할까요?: 보호 멤버 자격 및 역할을 사용 하 여 내 사이트?](https://asp.net/learn/videos/video-45.aspx) (비디오)
- [멤버 자격 소개](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [MSDN 보안 개발자 센터](https://msdn.microsoft.com/security/default.aspx)
- [전문 ASP.NET 2.0 보안, 구성원 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [공급자 도구 키트](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가이 자습서 시리즈 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz, John Suru 및 Teresa 머피의 포함 됩니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](forms-authentication-configuration-and-advanced-topics-cs.md)
> [다음](an-overview-of-forms-authentication-vb.md)
