---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-cs
title: 보안 기본 사항 및 ASP.NET 지원 (C#) | Microsoft Docs
author: rick-anderson
description: 이 일련의 참여에 대 한 액세스 권한을 부여 하는 web form 통해 방문자를 인증 하는 기술을 살펴봅니다는 자습서의 첫 번째 자습서...
ms.author: aspnetcontent
ms.date: 01/13/2008
ms.assetid: 07e15538-2f29-40c6-b2e7-e6115075ac83
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-cs
msc.type: authoredcontent
ms.openlocfilehash: 9600dc0c5bee5fa81cbe19a35dab7fb35e01df1b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815810"
---
<a name="security-basics-and-aspnet-support-c"></a>보안 기본 사항 및 ASP.NET 지원 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_cs.pdf)

> 웹 양식을 통해 방문자를 인증 하 고, 특정 페이지 및 기능에 대 한 액세스 권한을 부여, ASP.NET 응용 프로그램에서 사용자 계정 관리에 대 한 기술에 학습 하는 자습서의 시리즈의 첫 번째 자습서입니다.


## <a name="introduction"></a>소개

한 가지 포럼, 전자 상거래 사이트, 온라인 전자 메일 웹 사이트, 포털 웹 사이트 및 소셜 네트워크 사이트 모두 서로 공통 되는 무엇 인가요? 모두 제공할 *사용자 계정*합니다. 사용자 계정을 제공 하는 사이트에는 여러 가지 서비스를 제공 해야 합니다. 최소한 새 방문자가 계정을 만들 수 해야 하 고 반환 방문자에 게 로그인 할 수 있어야 합니다. 이러한 웹 응용 프로그램에 로그온 한 사용자를 기반으로 하는 결정을 내릴 수 있습니다: 일부 페이지 또는 작업 제한 될 수 있습니다만 사용자 또는 사용자의 특정 하위 집합으로 기록 다른 페이지 수 정보 특정 로그인된 사용자에 게 수 표시 또는 더 많거나 적은 사용자가 페이지를 보고에 따라 정보를 합니다.

웹 양식을 통해 방문자를 인증 하 고, 특정 페이지 및 기능에 대 한 액세스 권한을 부여, ASP.NET 응용 프로그램에서 사용자 계정 관리에 대 한 기술에 학습 하는 자습서의 시리즈의 첫 번째 자습서입니다. 이 자습서의 과정을 살펴보겠습니다 방법:

- 식별 및 사용자가 웹 사이트에 로그인
- ASP를 사용 합니다. 사용자 계정을 관리 하려면 NET의 멤버 자격 프레임 워크
- 만들기, 업데이트 및 사용자 계정 삭제
- 웹 페이지, 디렉터리 또는 로그인된 사용자를 기반으로 하는 특정 기능에 대 한 액세스를 제한 합니다.
- ASP를 사용 합니다. 사용자 계정을 역할과 연결 하려면 NET의 역할 프레임 워크
- 사용자 역할 관리
- 웹 페이지, 디렉터리 또는 로그인된 한 사용자의 역할을 기반으로 하는 특정 기능에 대 한 액세스를 제한 합니다.
- 사용자 지정 하 고 ASP를 확장 합니다. NET의 보안 웹 컨트롤

이 자습서는 간결 하 게 되며 프로세스를 안내 하는 시각적으로 스크린 샷을 많은 단계별 지침을 제공 하도록 설계 되었습니다. 각 자습서는 C# 및 Visual Basic 버전에서 사용할 수 및 사용 된 전체 코드를 다운로드 하 여 포함 합니다. (이 첫 번째 자습서 대략적인 관점에서 보안 개념에 중점을 두고 및 따라서 연결 된 코드는 포함 하지 않습니다.)

이 자습서에서는 중요 한 보안 개념 및 기능은 폼 인증, 권한 부여, 사용자 계정 및 역할을 구현 하는 데 도움이 되는 ASP.NET에서 사용할 수 있는 어떤 살펴보겠습니다. 이제 시작 하겠습니다.

> [!NOTE]
> 보안 물리적, 기술적에 걸쳐 있는 응용 프로그램의 중요 한 측면 이며 정책 결정 및 높은 수준의 계획과 영역 지식 필요 합니다. 이 자습서 시리즈는 보안 웹 응용 프로그램을 개발 하기 위한 지침으로 없습니다. 대신에 중점을 둡니다 특히 폼 인증, 권한 부여, 사용자 계정 및 역할입니다. 다른 사용자가 왼쪽이 시리즈의 이러한 문제를 둘러싼 일부 보안 개념을 설명 하며, 하는 동안 탐색 되지 않은 합니다.


## <a name="authentication-authorization-user-accounts-and-roles"></a>인증, 권한 부여, 사용자 계정 및 역할

인증, 권한 부여, 사용자 계정 및 역할은 사용 되는 자주이 자습서 시리즈에서는 전체 빠른 시간을 내어 웹 보안의 컨텍스트 내에서 이러한 용어를 정의 하려고 하므로 네 가지 용어입니다. 인터넷과 같은 클라이언트-서버 모델에는 서버를 요청 하는 클라이언트를 식별 해야 하는 많은 시나리오가 있습니다. *인증* 은 프로세스 부분도 클라이언트의 id입니다. 클라이언트는 성공적으로 확인 되었습니다 이라고 *인증*합니다. 알 수 없는 클라이언트를 이라고 *인증 되지 않은* 하거나 *익명*합니다.

보안 인증 시스템을 포함 하는 다음 세 가지 패싯 중 하나 이상이: [사용자가 아는 항목, 작업, 또는 사용자](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html)합니다. 대부분의 웹 응용 프로그램 클라이언트 암호 또는 PIN 같은 알고 있는 것에 의존 합니다. -사용자 이름과 암호를 예를 들어 자신의-사용자를 식별 하는 데 정보 라고 *자격 증명*합니다. 이 자습서 시리즈에 중점을 둡니다 *폼 인증*는 사용자가 웹 페이지 폼에서 자신의 자격 증명을 제공 하 여 사이트에 로그인 하는 인증 모델. 모든 목격한이 유형의 하기 전에 인증 합니다. 모든 전자 상거래 사이트로 이동 합니다. 체크 아웃할 준비 되 면 웹 페이지에서 텍스트 상자에 사용자 이름 및 암호를 입력 하 여 로그인 하 라는 메시지가 표시 됩니다.

클라이언트를 식별 하는 것 외에도 서버 어떤 리소스 또는 기능 요청을 하는 클라이언트에 따라 액세스할 수를 제한 해야 할 수 있습니다. *권한 부여* 특정 사용자를 특정 리소스 또는 기능에 액세스할 권한이 있는지 여부를 결정 하는 프로세스입니다.

A *사용자 계정* 특정 사용자에 대 한 정보를 유지에 대 한 저장소입니다. 사용자 계정을 사용자의 로그인 이름 및 암호와 같은 사용자를 고유 하 게 식별 하는 정보를 포함 최소 해야 합니다. 사용자 계정 등이 중요 한 정보를 함께 포함 될 수 있습니다: 사용자의 전자 메일 주소입니다. 날짜 및 시간 계정이 생성 되었습니다. 날짜 및 시간에서 마지막으로 로그인 첫 번째 및 마지막 이름입니다. 전화 번호입니다. 및 우편 주소입니다. Forms 인증을 사용 하면 사용자 계정 정보는 일반적으로 Microsoft SQL Server와 같은 관계형 데이터베이스에 저장 됩니다.

사용자 계정을 지 원하는 웹 응용 프로그램에 사용자를 선택적으로 그룹화 할 수 있습니다 *역할*입니다. 역할은 사용자에 게 적용 되 고 권한 부여 규칙 및 페이지 수준 기능을 정의 하기 위한 추상화를 제공 하는 레이블을 하기만 하면 됩니다. 예를 들어, 웹 사이트 관리자가 웹 페이지의 특정 집합에 액세스할 수 있지만 모든 사용자를 방해 하는 권한 부여 규칙을 사용 하 여 관리자 역할을 포함할 수 있습니다. 또한 모든 사용자 (관리자가 아닌 포함)에 액세스할 수 있는 페이지의 다양 한 추가 데이터를 표시 하거나 관리자 역할에 사용자가 방문 하는 경우 추가 기능을 제공 수 있습니다. 역할을 사용 하에서는 사용자가 사용자 대신 역할-역할별 별로 이러한 권한 부여 규칙을 정의할 수 있습니다.

## <a name="authenticating-users-in-an-aspnet-application"></a>ASP.NET 응용 프로그램에서 사용자 인증

브라우저는 사용자가 링크를 브라우저의 주소 창 또는 번의 클릭으로 URL을 입력 하는 경우는 [하이퍼텍스트 전송 프로토콜 (HTTP)](http://en.wikipedia.org/wiki/HTTP) 지정된 된 내용에 대 한 웹 서버에 대 한 요청, ASP.NET 페이지, 이미지, JavaScript 파일 또는 다른 종류의 콘텐츠입니다. 웹 서버는 요청 된 콘텐츠를 반환 해야 합니다. 이 과정에서 다양 한 요청을 수행 하는 등 id 요청 된 콘텐츠를 검색할 수 있는 권한이 있는지 여부는 요청에 대 한 작업 확인 해야 합니다.

브라우저는 기본적으로 모든 종류의 식별 정보 없는 HTTP 요청을 보냅니다. 하지만 브라우저는 인증 정보를 포함 하는 경우 다음 웹 서버 시작 요청을 만드는 클라이언트를 식별 하는 인증 워크플로에 합니다. 인증 워크플로 단계를 웹 응용 프로그램에서 사용 중인 인증의 유형에 따라 달라 집니다. ASP.NET은 세 가지 유형의 인증을 지원 합니다: Windows, Passport 및 폼입니다. 이 자습서 시리즈 폼 인증을 중점적으로 다루지만 비교 및 대조 Windows 인증 사용자 저장소와 워크플로를 설명 하겠습니다.

### <a name="authentication-via-windows-authentication"></a>Windows 인증을 통해 인증

Windows 인증 워크플로 다음 인증 방법 중 하나를 사용 합니다.

- 기본 인증
- 다이제스트 인증
- Windows 통합된 인증

세 가지 기술 모두 거의 동일한 방식으로 작동 합니다:가 권한이 없는 경우 익명 요청이 도착 하면, 웹 서버는 권한 부여를 나타내는 HTTP 응답을 계속 하려면 반드시 다시 보냅니다. 그런 다음 브라우저 (그림 1 참조)는 사용자 이름과 암호를 묻는 있는 모달 대화 상자를 표시 합니다. 이 정보는 HTTP 헤더를 통해 웹 서버에 다시 전송 됩니다.


![모달 대화 상자를 사용자 자신의 자격 증명 확인](security-basics-and-asp-net-support-cs/_static/image1.png)

**그림 1**: 모달 대화 상자를 사용자 자신의 자격 증명 확인


제공 된 자격 증명을 웹 서버의 Windows 사용자 저장소에 대해 유효성이 검사 됩니다. 이 웹 응용 프로그램에서 각 인증 된 사용자 조직에서 Windows 계정을 있어야 한다는 것을 의미 합니다. 인트라넷 시나리오에서 일반적입니다. 사실, 인트라넷 설정에 Windows 통합 인증을 사용 하면 브라우저 웹 서버 하므로 그림 1에 표시 된 대화 상자를 표시 하지 않는 네트워크에 로그온 하는 데 사용 하는 자격 증명을 사용 하 여 자동으로 제공 합니다. Windows 인증은 인트라넷 응용 프로그램에 적합 하는 동안 적합 하지 않다고 일반적으로 인터넷 응용 프로그램에 대 한 사이트에서 등록 하는 각 사용자에 대 한 Windows 계정 만들기를 원하지 않는 때문입니다.

### <a name="authentication-via-forms-authentication"></a>Forms 인증을 통해 인증

다른 한편으로 폼 인증의 경우 인터넷 웹 응용 프로그램에 적합합니다. Web form 통해 자격 증명을 입력 하 여 사용자를 식별 하는 폼 인증을 기억 하십시오. 따라서 사용자가 인증 되지 않은 리소스에 액세스 하려고 하는 경우 자동으로 리디렉션됩니다 자격 증명을 입력할 수 있는 로그인 페이지에 있습니다. 제출 된 자격 증명을 사용자 지정 사용자 저장소-일반적으로 데이터베이스에 대해 유효성이 검사 한 다음 됩니다.

제출 된 자격 증명을 확인 한 후에 *폼 인증 티켓* 사용자에 대해 생성 됩니다. 이 티켓 사용자가 인증 된 사용자 이름 등의 식별 정보를 포함 함을 나타냅니다. 폼 인증 티켓을 클라이언트 컴퓨터에 쿠키로 저장 (보통) 됩니다. 따라서 웹 사이트를 방문할 HTTP 요청 되므로 다음 로그인 한 후 사용자를 식별 하는 웹 응용 프로그램에서에서 폼 인증 티켓을 포함 합니다.

그림 2는 높은 수준의 유리한 지점에서 폼 인증 워크플로를 보여 줍니다. ASP.NET에서 인증 및 권한 부여 요소 두 개의 별도 엔터티에 역할도 하는 방법을 확인할 수 있습니다. Forms 인증 시스템 사용자를 식별 하거나 익명 지 보고. 권한 부여 시스템을 사용자 요청된 된 리소스에 대 한 액세스 권한이 있는지 여부를 결정 합니다. 경우 (되므로 그림 2에 익명으로 ProtectedPage.aspx를 방문 하려고 할 때) 사용자 권한이 부여 되어, 폼 인증 시스템을 자동으로 로그인 페이지로 사용자를 리디렉션할 원인이 사용자 거부는 권한 부여 시스템에서 보고 합니다.

사용자가 성공적으로 로그인 되 면 후속 HTTP 요청이 폼 인증 티켓이 포함 됩니다. Forms 인증 시스템은 단순히 사용자를 식별-사용자 요청 된 리소스에 액세스할 수 있는지 여부를 결정 하는 권한 부여 시스템입니다.


![Forms 인증 워크플로](security-basics-and-asp-net-support-cs/_static/image2.png)

**그림 2**: Forms 인증 워크플로


다음 두 자습서에서는 훨씬 더 큰 세부 정보에서 폼 인증 살펴보기[는 폼 인증 개요](an-overview-of-forms-authentication-cs.md) 하 고 [폼 인증 구성 및 고급 항목](forms-authentication-configuration-and-advanced-topics-cs.md)합니다. 에 대 한 자세한 ASP 합니다. NET의 인증 옵션을 참조 하세요 [ASP.NET 인증](https://msdn.microsoft.com/library/eeyk640h.aspx)합니다.

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>웹 페이지, 디렉터리 및 페이지 기능에 대 한 액세스를 제한합니다.

ASP.NET에 특정 사용자 특정 파일이 나 디렉터리에 액세스 권한이 있는지 여부를 결정 하는 두 가지 방법에 포함 됩니다.

- **권한 부여 파일** -때문에 ASP.NET 페이지 및 웹 서비스 액세스 제어 목록 (Acl)을 통해 이러한 파일에 대 한 액세스는 웹 서버의 파일 시스템에 상주 하는 파일을 지정할 수 있습니다 하는 대로 구현 됩니다. 파일 권한 부여에 Windows 계정에 적용 되는 권한 Acl 때문에 Windows 인증을 사용 하 여 가장 많이 사용 됩니다. Forms 인증을 사용 하는 경우 모든 운영 체제 및 파일 시스템 수준 요청 사이트를 방문 하는 사용자에 관계 없이 동일한 Windows 계정에 의해 실행 됩니다.
- **URL 권한 부여**-URL 권한 부여를 사용 하 여 페이지 개발자 Web.config에 권한 부여 규칙을 지정 합니다. 이러한 권한 부여 규칙에는 어떤 사용자 또는 역할에 액세스할 수 있습니다 또는 거부 특정 페이지나 응용 프로그램의 디렉터리에 액세스 하지 못하도록 지정 합니다.

파일 권한 부여와 URL 권한 부여는 특정 디렉터리에서 모든 ASP.NET 페이지 또는 특정 ASP.NET 페이지에 액세스 하기 위한 권한 부여 규칙을 정의 합니다. 이러한 기술을 사용 하 여에서는 특정 사용자에 대해 특정 페이지에는 요청 거부 또는 사용자 집합에 대 한 액세스를 허용, 다른 모든 사용자에 대 한 액세스를 거부 하는 ASP.NET을 지시할 수 있습니다. 사용자의 모든 페이지에 액세스할 수 있었지만 사용자에 따라 달라 집니다 페이지의 기능 시나리오의 경우는 어떨까요? 예를 들어, 사용자 계정을 지원는 많은 사이트 서로 다른 콘텐츠 또는 익명 사용자 및 인증 된 사용자에 대 한 데이터를 표시 하는 페이지를 설치 합니다. 익명 사용자 인증된 된 사용자는 같은, 다시 시작 메시지를 표시 하는 반면 사이트에 로그인에 대 한 링크가 나타날 *Username* 로그 아웃에 대 한 링크와 함께 합니다. 또 다른 예:는 입찰 나 auctioning 항목 인지에 따라 다른 정보 경매 사이트에 있는 항목을 볼 때 표시 됩니다.

프로그래밍 방식으로 또는 선언적으로 이와 같은 페이지 수준 조정 작업을 수행할 수 있습니다. 에 대 한 여러 콘텐츠를 표시 익명 인증 된 사용자가 끌어서 보다는 [LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 페이지로 해당 AnonymousTemplate 템플릿과 LoggedInTemplate에 적절 한 콘텐츠를 입력 합니다. 또는 프로그래밍 방식으로 및 확인할 수 있습니다 요청과 인증 되는지 여부, 사용자를 역할 (있는 경우)에 속해 있습니다. 페이지의 표 또는 패널에서 열을 다음 표시 하거나 숨기려면이 정보를 사용할 수 있습니다.

이 시리즈는 권한 부여에 중점을 둔 세 개의 자습서를 포함 합니다. ***사용자 기반 권한 부여***; 특정 사용자 계정의 또는 디렉터리에 여러 페이지에 대 한 액세스를 제한 하는 방법 검사 ***역할 기반 권한 부여*** 조사 수준; 마지막으로 역할의 권한 부여 규칙을 제공 합니다 ***는 현재 로그온 한 사용자에 따라 콘텐츠 표시*** 자습서에서는 특정 수정 페이지의 콘텐츠 및 기능 페이지를 방문 하 여 사용자를 기반으로 합니다. 에 대 한 자세한 ASP 합니다. NET의 권한 부여 옵션을 참조 하세요 [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)합니다.


## <a name="user-accounts-and-roles"></a>사용자 계정 및 역할

ASP 합니다. NET의 폼 인증 사용자가 사이트에 로그인 하 고 기억 방문 페이지에서 인증 된 상태에 대 한 인프라를 제공 합니다. 및 URL 권한 부여는 ASP.NET 응용 프로그램에서 특정 파일이 나 폴더에 대 한 액세스를 제한 하기 위해 프레임 워크를 제공 합니다. 그러나 두 기능을 사용자 계정 정보를 저장 하거나 역할 관리에 대 한 수단을 제공 합니다.

ASP.NET 2.0 이전 개발자가 자신의 사용자 및 역할 저장소 생성을 담당 했습니다. 에 있는 것도 사용자 인터페이스 디자인 및 코딩 필수 사용자에 대 한 로그인 페이지 및 다른 새 계정을 만들려면 페이지와 같은 계정 관련 페이지에 대 한 후크입니다. ASP.NET 구현 하는 사용자 계정에 다음과 같은 질문에 자신의 디자인 결정에 도착 해야 하는 각 개발자의에서 모든 기본 제공 사용자 계정 프레임 워크 없이 저장 하는 방법 암호나 다른 중요 한 정보가? 하 고 어떤 지침 암호 길이 및 강도 대 한 적용 해야 하나요?

오늘날 ASP.NET 응용 프로그램에서 사용자 계정을 구현 하는 훨씬 간단 하 게 감사 인사를 전 합니다 *멤버 자격 프레임 워크* 및 로그인 웹 컨트롤 기본 제공 합니다. 멤버 자격 프레임 워크는 소수의의 클래스는 [System.Web.Security 네임 스페이스](https://msdn.microsoft.com/library/system.web.security.aspx) 필수 사용자 계정 관련 작업을 수행 하는 것에 대 한 기능을 제공 합니다. 멤버 자격 프레임 워크의 핵심 클래스는 합니다 [멤버 자격 클래스](https://msdn.microsoft.com/library/system.web.security.membership.aspx), 있으며 그와 같은 메서드:

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- ValidateUser

멤버 자격 프레임 워크를 사용 합니다 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 멤버 자격 프레임 워크의 API 구현에서 명확 하 게 구분 하는 합니다. 이 공용 API를 사용 하는 개발자를 사용 하도록 설정 하지만 수 있도록 해당 응용 프로그램의 사용자 지정 요구를 충족 하는 구현을 사용 하도록 합니다. 즉, 멤버 자격 클래스 (메서드, 속성 및 이벤트), 프레임 워크의 필수 기능을 정의 하지만 실제로 구현 세부 정보를 제공 하지 않습니다. 대신, 멤버 자격 클래스의 메서드는 실제 작업을 수행 하는 구성된 공급자를 호출 합니다. 예를 들어, 멤버 자격 클래스의 CreateUser 메서드를 호출 하면 멤버 자격 클래스는 사용자 저장소의 세부 정보를 알지 못합니다. 하는 경우 사용자가 유지 관리 되는 데이터베이스, XML 파일 또는 다른 저장소 알고 있지 않습니다. 대리자를 호출 하 여 어떤 공급자를 확인 하려면 웹 응용 프로그램의 구성을 검사 하는 멤버 자격 클래스 및 해당 공급자 클래스는 실제로 적절 한 사용자 저장소에 새 사용자 계정 생성을 담당 합니다. 그림 3이 상호이 작용을 보여 줍니다.

Microsoft는.NET Framework의 두 가지 멤버 자격 공급자 클래스를 제공합니다.

- [ActiveDirectoryMembershipProvider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) -Active Directory 및 Active Directory 응용 프로그램 모드 (ADAM) 서버에서 멤버 자격 API를 구현 합니다.
- [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) -SQL Server 데이터베이스의 멤버 자격 API를 구현 합니다.

이 자습서 시리즈를 SqlMembershipProvider에만 중점을 둡니다.


[![공급자 모델 사용 하면 다른 구현을 원활 하 게 연결에 프레임 워크를 &lt; /s o n&gt;](security-basics-and-asp-net-support-cs/_static/image4.png)](security-basics-and-asp-net-support-cs/_static/image3.png)

**그림 03**: The 공급자 모델 사용 하면 다른 구현을를 원활 하 게 연결에 프레임 워크 ([큰 이미지를 보려면 클릭](security-basics-and-asp-net-support-cs/_static/image5.png))


공급자 모델의 장점은 대체 구현을 Microsoft, 타사 공급 업체 또는 개별 개발자가 개발 및 멤버 자격 프레임 워크에 원활 하 게 연결할 수 있습니다. 예를 들어, Microsoft는 출시 했습니다 [Microsoft Access 데이터베이스에 대 한 멤버 자격 공급자](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi)합니다. 멤버 자격 공급자에 대 한 자세한 내용은 참조는 [Provider Toolkit](https://msdn.microsoft.com/asp.net/aa336558.aspx), 멤버 자격 공급자, 샘플 사용자 지정 공급자는 공급자 모델에 대 한 설명서의 100 개 이상의 페이지의 연습을 포함 하는 및 기본 멤버 자격 공급자 (즉, ActiveDirectoryMembershipProvider 및 SqlMembershipProvider)에 대 한 소스 코드를 완료 합니다.

ASP.NET 2.0에는 역할 프레임 워크가 도입 되었습니다. 멤버 자격 프레임 워크와 같은 역할 프레임 워크는 공급자 모델 작성 됩니다. 해당 API를 통해 노출 되는 [역할 클래스](https://msdn.microsoft.com/library/system.web.security.roles.aspx) 세 개의 공급자 클래스와 함께 제공 되는.NET Framework 및:

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) -Active Directory 또는 ADAM와 같은 권한 부여 관리자 정책 저장소를에서 역할 정보를 관리 합니다.
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) -SQL Server 데이터베이스의 역할을 구현 합니다.
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) -방문자의 Windows 그룹을 기반으로 하는 역할 정보를 연결 합니다. 이 메서드는 일반적으로 Windows 인증과 함께 사용 됩니다.

이 자습서 시리즈 SqlRoleProvider에만 중점을 둡니다.

구현 세부 정보에 걱정할 필요 없이 해당 API에 대 한 기능을 작성 하는 것이 불가능-페이지에서 선택한 공급자에 의해 처리 되는 공급자 모델을 단일 정면 API (멤버 자격 및 역할 클래스)를 포함 하므로 개발자입니다. 이 통합된 API는 Microsoft 및 타사 공급 업체 웹 컨트롤 멤버 자격 및 역할 프레임 워크를 사용 하 여 해당 인터페이스를 빌드할 수 있습니다. ASP.NET은 다양 한 [로그인 웹 컨트롤](https://msdn.microsoft.com/library/ms178329.aspx) 일반 사용자 계정을 사용자 인터페이스를 구현 합니다. 예를 들어 합니다 [Login 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) , 유효성을 검사 하 고 폼 인증을 통해 로그에 사용자 자격 증명을 묻는 메시지를 표시 합니다. 합니다 [LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 인증 된 사용자 및 익명 사용자에 게 다른 태그 또는 사용자의 역할을 기반으로 하는 다른 태그를 표시 하기 위한 템플릿을 제공 합니다. 하며 [CreateUserWizard 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx) 새 사용자 계정을 만들기 위한 단계별 사용자 인터페이스를 제공 합니다.

내부적 다양 한 로그인 컨트롤 멤버 자격 및 역할 프레임 워크와 상호 작용 합니다. 코드를 전혀 작성 하지 않고도 대부분의 로그인 컨트롤을 구현할 수 있습니다. 이후 자습서에서는 확장 및 해당 기능을 사용자 지정 기술을 포함 하 여 이러한 컨트롤을을 더 자세히 살펴보겠습니다.

## <a name="summary"></a>요약

사용자 계정을 지 원하는 모든 웹 응용 프로그램 비슷한 기능이 필요 합니다: 사용자가 로그인 하 여 페이지 방문;에서 저장 된 상태에서 해당 로그에는 기능 계정을 만들려면 새 방문자에 대 한 웹 페이지 어떤 사용자 또는 역할에 사용할 수 있는 리소스, 데이터 및 기능을 지정 하는 페이지 개발자에 게 기능 하 고 있습니다. 인증 및 사용자 권한 부여 및 사용자 계정 및 역할 관리 작업을 위해 폼 인증, URL 권한 부여 및 멤버 자격 및 역할 프레임 워크 덕분에 ASP.NET 응용 프로그램에서 매우 쉽습니다.

다음 몇 가지 자습서를 통해 단계별 방식에서부터 작업 웹 응용 프로그램을 구축 하 여 이러한 측면을 살펴보겠습니다. 다음 두 자습서의 세부 정보에서 폼 인증을 살펴봅니다. 로그인 및 로그 아웃 하는 방문자를 허용 하는 웹 응용 프로그램을 빌드하는 동안 모든-폼 인증 티켓을 분석, 보안 문제를 설명 및 forms 인증 시스템을 구성 하는 방법은 폼 인증 워크플로에서 작업을 살펴보겠습니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0 멤버 자격, 역할, 폼 인증 및 보안 리소스](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [ASP.NET 2.0 보안 지침](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET 인증](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [ASP.NET 로그인 컨트롤 개요](https://msdn.microsoft.com/library/ms178329.aspx)
- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [I: 멤버 자격 및 역할을 사용 하 여 내 사이트를 보호 하는 방법](https://asp.net/learn/videos/video-45.aspx) (비디오)
- [멤버 자격 소개](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [MSDN 보안 개발자 센터](https://msdn.microsoft.com/security/default.aspx)
- [Professional ASP.NET 2.0 보안, 멤버 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [공급자 도구 키트](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는이 자습서 시리즈를 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz, John Suru 및 Teresa Murphy 포함 됩니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](an-overview-of-forms-authentication-cs.md)
