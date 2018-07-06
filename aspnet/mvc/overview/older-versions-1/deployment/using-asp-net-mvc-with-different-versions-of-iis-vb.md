---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: ASP.NET MVC를 사용 하 여 다른 버전의 IIS (VB)를 사용 하 여 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 ASP.NET MVC 및 URL 라우팅 인터넷 정보 서비스의 서로 다른 버전을 사용 하는 방법을 알아봅니다. 다른 전략에 알아봅니다.
ms.author: aspnetcontent
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 4c0dc1ac08cfe06ad7ea35a6e6552ab1174ff989
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818206"
---
<a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>ASP.NET MVC를 사용 하 여 다른 버전의 IIS (VB)
====================
[Microsoft](https://github.com/microsoft)

> 이 자습서에서는 ASP.NET MVC 및 URL 라우팅 인터넷 정보 서비스의 서로 다른 버전을 사용 하는 방법을 알아봅니다. ASP.NET MVC를 사용 하 여 IIS 7.0 (기본 모드), IIS 6.0 및 이전 버전의 IIS에 대 한 다른 전략에 알아봅니다.


ASP.NET MVC 프레임 워크 컨트롤러 작업에 브라우저 요청을 라우팅하도록 ASP.NET 라우팅에 따라 달라 집니다. ASP.NET 라우팅에서 활용 하기 위해 웹 서버에서 추가 구성 단계를 수행 해야 합니다. 모든 버전의 인터넷 정보 서비스 (IIS) 및 처리 모드 응용 프로그램에 대 한 요청에 따라 달라 집니다.

다른 버전의 IIS 요약이 다음과 같습니다.

- IIS 7.0 (통합된 모드)-ASP.NET 라우팅을 사용 하는 데 필요한 특별 한 구성이 없습니다.
- IIS 7.0 (기본 모드)-ASP.NET 라우팅을 사용 하려면 특별 한 구성을 수행 해야 합니다.
- IIS 6.0 또는 아래-ASP.NET 라우팅을 사용 하려면 특별 한 구성을 수행 해야 합니다.

IIS의 최신 버전은 버전 7.5 (Win7). IIS 7의 IIS와 Windows Server 2008 및 VISTA/s p 1 제공 되어 높은 합니다. 설치할 수도 있습니다 IIS 7.0 Home Basic을 제외한 Vista 운영 체제의 모든 버전 (참조 [ https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx ](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).

IIS 7.0 요청 처리를 위한 두 가지 모드를 지원 합니다. 통합된 모드 또는 클래식 모드를 사용할 수 있습니다. 통합된 모드의 IIS 7.0을 사용 하는 경우 모든 특수 구성 단계를 수행할 필요가 없습니다. 그러나 클래식 모드에서 IIS 7.0을 사용 하는 경우 추가 구성을 수행할 필요가 있습니다.

Microsoft Windows Server 2003에는 IIS 6.0 포함 됩니다. Windows Server 2003 운영 체제를 사용 하는 경우 IIS 7.0으로 IIS 6.0을 업그레이드할 수 없습니다. IIS 6.0을 사용 하는 경우에 추가 구성 단계를 수행 해야 합니다.

Microsoft Windows XP Professional에는 IIS 5.1 포함 됩니다. IIS 5.1을 사용 하는 경우에 추가 구성 단계를 수행 해야 합니다.

마지막으로, Microsoft Windows 2000 및 Microsoft Windows 2000 Professional IIS 5.0을 포함 합니다. IIS 5.0을 사용 하는 경우에 추가 구성 단계를 수행 해야 합니다.

## <a name="integrated-versus-classic-mode"></a>클래식 모드와 통합

IIS 7.0 두 가지 다른 요청 처리 모드를 사용 하 여 요청을 처리할 수 있습니다: 클래식 및 통합 합니다. 통합된 모드는 더 나은 성능과 더 많은 기능을 제공합니다. 클래식 모드에 대 한 이전 버전과 포함 된 이전 버전의 IIS와의 호환성.

요청 처리 모드는 응용 프로그램 풀에 의해 결정 됩니다. 처리 모드는 응용 프로그램과 관련 응용 프로그램 풀을 확인 하 여 특정 웹 응용 프로그램에서 사용 중인 것을 확인할 수 있습니다. 아래 단계를 수행합니다.

1. 인터넷 정보 서비스 관리자를 시작 합니다.
2. 연결 창에서 응용 프로그램 선택
3. 작업 창에서 클릭 합니다 **기본 설정** 응용 프로그램 편집 대화 상자를 열려면 링크 상자 (그림 1 참조)
4. 선택한 응용 프로그램 풀을 기록해 둡니다.

기본적으로 IIS는 두 개의 응용 프로그램 풀을 지원 하도록 구성: **DefaultAppPool** 하 고 **클래식.NET AppPool**합니다. DefaultAppPool을 선택 하면 응용 프로그램 통합된 요청 처리 모드에서 실행 됩니다. 클래식.NET AppPool을 선택 하면 응용 프로그램은 클래식 요청 처리 모드에서 실행 됩니다.


[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**그림 1**: 검색 요청 처리 모드 ([큰 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))


응용 프로그램 편집 대화 상자에서 요청 처리 모드를 수정할 수 있는지 확인 합니다. 선택 단추를 클릭 하 고 응용 프로그램을 사용 하 여 연결 된 응용 프로그램 풀을 변경 합니다. 통합된 모드를 클래식에서 ASP.NET 응용 프로그램을 변경 하는 경우 호환성 문제는 점을 명심 하십시오. 자세한 내용은 다음 항목을 참조하세요.

- Windows Vista 및 Windows Server 2008-IIS 7.0으로 ASP.NET 1.1로 업그레이드 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- IIS 7.0-를 사용 하 여 ASP.NET 통합 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)


ASP.NET 응용 프로그램을 DefaultAppPool를 사용 하는 경우 ASP.NET 라우팅 (및 따라서 ASP.NET MVC) 작업 가져오기에 추가 단계를 수행할 필요가 없습니다. 그러나 ASP.NET 응용 프로그램을 클래식.NET AppPool을 사용 하 여 다음 계속 진행 하세요, 하도록 경우 많은 작업을 수행 합니다.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>ASP.NET MVC를 사용 하 여 이전 버전의 IIS 사용 하 여

IIS 7.0 이전 버전의 IIS 사용 하 여 ASP.NET MVC를 사용 해야 할 경우 클래식 모드에서 IIS 7.0을 사용 해야 할 다음 두 가지 옵션이 있습니다. 첫째, 파일 확장명을 사용 하 여 경로 테이블을 수정할 수 있습니다. 예를 들어 /Store/Details과 같은 URL을 요청 하는 대신 /Store.aspx/Details 같은 URL을 요청 합니다.

두 번째 옵션은 라는 것을 만듭니다는 *와일드 카드 스크립트 매핑*합니다. 와일드 카드 스크립트 매핑을 사용 하면 ASP.NET framework에 모든 요청을 매핑할 수 있습니다.

웹 서버 (예를 들어, 응용 프로그램을 인터넷 서비스 공급자에서 호스팅하는 ASP.NET MVC)에 액세스할 수 없는 경우 첫 번째 옵션을 사용 해야 합니다. Url의 모양을 수정 하지 않으려는 경우 웹 서버에 액세스할 수 있는 두 번째 옵션을 사용할 수 있습니다.

다음 섹션에서 자세히 각 옵션을 살펴봅니다.

## <a name="adding-extensions-to-the-route-table"></a>경로 테이블에 확장 추가

이전 버전의 IIS 사용 하려면 ASP.NET 라우팅에서 얻을 수 있는 가장 쉬운 방법은 Global.asax 파일에 경로 테이블을 수정 하는 경우 기본 목록 1에서 수정 되지 않은 Global.asax 파일 기본 경로 라는 한 개의 경로 구성 합니다.

**1-Global.asax (수정 되지 않은)를 나열 합니다.**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

목록 1에 구성 된 기본 경로 다음과 같은 Url 경로에 있습니다.

/ Home/Index

/ 제품/세부 정보/3

/ 제품

그러나 이전 버전의 IIS는 ASP.NET 프레임 워크를 이러한 요청을 전달 하지 않습니다. 따라서 이러한 요청 않습니다 컨트롤러로 라우팅됩니다. 예를 들어 URL /Home/인덱스에 대 한 브라우저 요청을 만드는 경우 다음 얻게 오류 페이지 그림 2.


[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**그림 2**: 404 찾을 수 없음 오류를 수신 ([큰 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))


이전 버전의 IIS는 ASP.NET 프레임 워크를 특정 요청을 매핑합니다. 올바른 파일 확장명을 사용 하 여 URL에 대 한 요청 이어야 합니다. 예를 들어, /SomePage.aspx에 대 한 요청은 ASP.NET 프레임 워크에 매핑됩니다 가져옵니다. 그러나 /SomePage.htm 요청 되지 않습니다.

따라서 ASP.NET 라우팅을 작동 하기를 가져오려면에서는 수정 해야 기본 경로 ASP.NET 프레임 워크에 매핑되는 파일 확장명을 포함 하도록 합니다.

이렇게 라는 스크립트를 사용 하 여 `registermvc.wsf`입니다. ASP.NET MVC 1 릴리스에 포함 된 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, ASP.NET 2부터이 스크립트로 이동 되었습니다 ASP.NET Futures에 사용할 수 있지만 [ http://aspnet.codeplex.com/releases/view/39978 ](http://aspnet.codeplex.com/releases/view/39978)합니다.

이 스크립트를 실행 합니다. IIS를 사용 하 여 새.mvc 확장을 등록 합니다. .Mvc 확장명을 등록 하면.mvc 확장을 사용 하는 경로 Global.asax 파일의 경로 수정할 수 있습니다.

목록 2에서 수정 된 Global.asax 파일을 이전 버전의 IIS 사용 하 여 작동합니다.

**2-Global.asax (확장을 사용 하 여 수정)를 나열 합니다.**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]


중요: 해야 Global.asax 파일을 변경 후에 다시 ASP.NET MVC 응용 프로그램을 작성 합니다.


목록 2에서 Global.asax 파일 두 가지 중요 한 변경 내용이 있습니다. Global.asax에 정의 된 두 개의 경로가 됩니다. 첫 번째 경로의 기본 경로 대 한 URL 패턴 이제 다음과 같습니다.

{controller}.mvc/{action}/{id}

ASP.NET 라우팅 모듈을 가로채는 파일의 종류를 변경 하는.mvc 확장명 추가 합니다. 이 변경으로 이제 ASP.NET MVC 응용 프로그램에는 다음과 같은 요청 경로:

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

두 번째 경로의 루트 경로, 새로운 기능입니다. 루트 경로 대 한 URL 패턴이 빈 문자열인 경우 이 경로 응용 프로그램의 루트에 대 한 요청이 일치 하는 데 필요한입니다. 예를 들어, 루트 경로 다음과 같은 요청을 일치 합니다.

[http://www.YourApplication.com/](http://www.YourApplication.com/)

경로 테이블에 다음과 같이이 수정에 확인 한 후 모든 응용 프로그램에서 링크는 이러한 새 URL 패턴을 사용 하 여 호환 되도록 해야 합니다. 즉,.mvc 확장명을 포함 한 모든 링크 해야 합니다. Html.ActionLink() 도우미 메서드를 사용 하 여 링크를 생성 하는 경우 변경할 필요가 없습니다.


Registermvc.wcf 스크립트를 사용 하는 대신 직접 ASP.NET 프레임 워크에 매핑되는 IIS에 새 확장을 추가할 수 있습니다. 새 확장을 직접 추가 하는 경우 확인란을 레이블이 지정 되었는지 확인 **파일이 있는지 확인** 확인 하지 않습니다.


## <a name="hosted-server"></a>호스트 서버

항상 웹 서버에 액세스할을 수 없는 있습니다. 예를 들어 인터넷 호스팅 공급자를 사용 하 여 ASP.NET MVC 응용 프로그램을 호스트 하는 경우 다음 반드시 액세스할 수 없습니다 iis입니다.

이 경우 ASP.NET 프레임 워크에 매핑되는 기존 파일 확장명 중 하나를 사용 해야 합니다. Asp 파일 확장명의 예로.aspx,.axd, 및.ashx 확장을 들 수 있습니다.

예를 들어 목록 3에서 수정된 된 Global.asax 파일.mvc 확장명 대신.aspx 확장을 사용합니다.

**3-Global.asax (.aspx 확장을 사용 하 여 수정)를 나열 합니다.**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

보기 3의 Global.asax 파일 확장명이.aspx.mvc 확장명 대신 사용 한다는 점 제외 하면 이전 Global.asax 파일과 정확히 같습니다. .Aspx 확장을 사용 하 여 원격 웹 서버의 모든 설치를 수행할 필요가 없습니다.

## <a name="creating-a-wildcard-script-map"></a>와일드 카드 스크립트 매핑 만들기

ASP.NET MVC 응용 프로그램에 대 한 Url을 수정 하지 않으려는 경우 웹 서버에 액세스할 수 있는 추가 옵션을 있습니다. ASP.NET framework 웹 서버에 모든 요청을 매핑하는 와일드 카드 스크립트 맵을 만들 수 있습니다. 이런 방식으로 클래식 모드에서 IIS 7.0 또는 IIS 6.0을 사용 하 여 기본 ASP.NET MVC 경로 테이블을 사용할 수 있습니다.

이 옵션을 IIS 웹 서버에 대 한 모든 요청을 가로채를 사용 하면 있는지 알아야 합니다. 이미지, 클래식 ASP 페이지 및 HTML 페이지에 대 한 요청이 포함 됩니다. 따라서 와일드 카드를 사용 하도록 설정 하면 asp.net 스크립트 매핑 않은 성능에 미치는 영향입니다.

IIS 7.0에 대 한 와일드 카드 스크립트 매핑을 사용 하는 방법을 다음과 같습니다.

1. 연결 창에서 응용 프로그램을 선택 합니다.
2. 있는지 확인 합니다 **기능** 뷰 선택
3. 두 번 클릭 합니다 **처리기 매핑** 단추
4. 클릭 합니다 **와일드 카드 스크립트 매핑 추가** (그림 3 참조) 링크
5. Aspnet의 경로 입력\_isapi.dll – 파일 (에서 복사할 수 있습니다이 경로 PageHandlerFactory 스크립트 매핑)
6. MVC 이름 입력
7. 클릭 합니다 **확인** 단추


[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**그림 3**: IIS 7.0을 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([큰 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))


IIS 6.0을 사용 하 여 와일드 카드 스크립트 맵을 만들려면 다음이 단계를 수행 합니다.

1. 웹 사이트를 마우스 오른쪽 단추로 클릭 하 고 속성 선택
2. 선택 된 **홈 디렉터리** 탭
3. 클릭 합니다 **구성** 단추
4. 선택 된 **매핑을** 탭
5. 클릭 합니다 **삽입** 단추 (그림 4 참조)
6. Aspnet에 대 한 경로 붙여\_isapi.dll – 실행 파일 (.aspx 파일에 대 한 스크립트 맵을에서이 경로 복사할 수) 필드에
7. 확인란의 선택을 취소 **파일이 있는지 확인**
8. 클릭 합니다 **확인** 단추


[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**그림 4**: IIS 6.0을 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([큰 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))


와일드 카드 스크립트 매핑을 사용 하도록 설정한 후에 루트 경로 포함 하도록 Global.asax 파일에 경로 테이블을 수정 해야 합니다. 그렇지 않은 경우 응용 프로그램의 루트 페이지에 대 한 요청을 하는 경우 그림 5에 오류 페이지를 얻을 수 있습니다. 목록 4의 수정된 된 Global.asax 파일을 사용할 수 있습니다.


[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**그림 5**: 누락 된 루트 경로 오류 ([큰 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))


**4-Global.asax (루트 경로 사용 하 여 수정)를 나열 합니다.**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

IIS 7.0 또는 IIS 6.0에 대 한 와일드 카드 스크립트 매핑을 사용 하도록 설정한 후에 다음과 같은 기본 경로 테이블을 사용 하는 요청을 만들 수 있습니다.

/

/ Home/Index

/ 제품/세부 정보/3

/ 제품

## <a name="summary"></a>요약

이 자습서의 목표는 이전 버전의 IIS (또는 클래식 모드에서 IIS 7.0)를 사용 하는 경우 Asp.net을 사용 하는 방법을 설명 하는 것 이었습니다. 이전 버전의 IIS 사용 하려면 ASP.NET 라우팅에서 가져오는 두 가지 방법에 설명 했습니다: 기본 경로 테이블을 수정 하거나 와일드 카드 스크립트 매핑 만들기.

첫 번째 옵션을 사용 하면 ASP.NET MVC 응용 프로그램에서 사용 하는 Url을 수정 해야 합니다. 이 첫 번째 옵션의 매우 중요 한 장점은 경로 테이블을 수정 하려면 웹 서버에 액세스할 필요가 수행입니다. 즉, 인터넷을 사용 하 여 ASP.NET MVC 응용 프로그램을 호스트 하는 경우에이 첫 번째 옵션을 사용할 수 있는 호스팅 회사입니다.

와일드 카드 스크립트 맵을 만들려면 두 번째 옵션이입니다. 이 두 번째 옵션의 장점은 Url을 수정할 필요가 없습니다. 이 두 번째 옵션의 단점은 ASP.NET MVC 응용 프로그램의 성능에 영향을 주기는입니다.

> [!div class="step-by-step"]
> [이전](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
