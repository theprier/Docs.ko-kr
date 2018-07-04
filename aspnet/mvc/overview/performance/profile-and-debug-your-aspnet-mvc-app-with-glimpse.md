---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 프로 파일링 및 디버깅 Glimpse 사용해 ASP.NET MVC 앱 | Microsoft Docs
author: Rick-Anderson
description: Glimpse은 번성 하 고 자세한 성능을 제공 하는 오픈 소스 NuGet 패키지의 제품군 증가, 디버깅 및 ASP.NET에 대 한 진단 정보는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: ef65b512645d3f013ea34d3557da93254425c419
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391072"
---
<a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>프로 파일링 및 디버깅 Glimpse 사용해 ASP.NET MVC 앱
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> Glimpse는 번성 하 고 자세한 성능을 제공 하는 오픈 소스 NuGet 패키지의 제품군 증가, 디버깅 및 ASP.NET 앱에 대 한 진단 정보. 설치가 간단 간단 하 고 매우 빠른 이며 모든 페이지의 맨 아래에 주요 성능 메트릭을 표시 합니다. 서버 진행 상황을 찾아야 할 때 앱에 드릴 수 있습니다. Glimpse Azure 테스트 환경을 포함 하 여 개발 주기 전체에서 사용 하는 것이 좋습니다는 훨씬 중요 한 정보를 제공 합니다. 하는 동안 [Fiddler](http://www.telerik.com/fiddler) 하며 [F-12 개발 도구](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) 제공 클라이언트 쪽 보기 Glimpse 서버의 상세 보기를 제공 합니다. 이 자습서는 간략 한 ASP.NET MVC 및 EF 패키지를 사용 하 여 중점 되지만 다른 많은 패키지 사용할 수 있습니다. 가능한 경우 적절 한 연결 됩니다 [docs 슬라이드](http://getglimpse.com/Docs/) 유지 관리할 수 있도록 하는 합니다. Glimpse는 오픈 소스 프로젝트, 너무 기여할 수 있는 소스 코드 및 문서입니다.


- [Glimpse를 설치합니다.](#ig)
- [Localhost에 대 한 이해를 사용 하도록 설정](#eg)
- [타임 라인 탭](#Time)
- [모델 바인딩](#mb)
- [경로](#route)
- [Glimpse를 사용 하 여 Azure에서](#da)
- [추가 리소스](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>Glimpse를 설치합니다.

NuGet 패키지 관리자 콘솔에서 또는 Glimpse를 설치할 수 있습니다 합니다 **NuGet 패키지 관리** 콘솔. 이 데모에서는 Mvc5 및 EF6 패키지를 설치 하겠습니다.

![Glimpse NuGet 대화 상자에서 설치](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

검색할 *Glimpse.EF*

![NuGet 설치 대화 상자에서 Glimpse.EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

선택 하 여 **설치 된 패키지**, 간략 한 종속 모듈 설치를 볼 수 있습니다.

![대화 상자에서 Glimpse 패키지 설치](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

다음 명령을 패키지 관리자 콘솔에서 간략 한 MVC5 및 EF6 모듈을 설치 합니다.

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>Localhost에 대 한 이해를 사용 하도록 설정

이동할 http://localhost:&lt; 포트 번호&gt;/glimpse.axd를 클릭 합니다 <strong>Glimpse 켜기</strong> 단추입니다.

![Glimpse axd 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

표시 즐겨찾기 모음에 있는 경우 있습니다 수 Glimpse 단추 끌어서 bookmarklets로 추가 합니다.

![Glimpse boookmarklets IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

이제 앱을 탐색할 수 있습니다 및 **표시를 헤드** (hud가) 페이지의 맨 아래에 표시 됩니다.

![HUD 사용 하 여 contact Manager 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

합니다 [Glimpse HUD 페이지](http://getglimpse.com/Docs/Heads-up-Display) 위에 표시 되는 타이밍 정보를 자세히 설명 합니다. 비간섭 성능에 표시 되는 데이터 HUD 알릴 수 문제의 즉시 테스트 사이클에 도달 하기 전에 합니다. 클릭 하는 &quot;g&quot; Glimpse 패널의 오른쪽 아래 모서리에 나타납니다.

![Glimpse 패널](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

위의 이미지에는 [실행 탭](http://getglimpse.com/Docs/Execution-Tab) 을 선택 하면 파이프라인에서 작업 및 필터의 타이밍 정보를 보여 주는 합니다. 볼 수 있습니다 내 [조사식 중지 필터 타이머](http://www.nuget.org/packages/StopWatch/) 파이프라인의 6 단계를 시작 합니다. 내 간단한 타이머를 제공할 수 있지만 뷰를 렌더링 하 고 권한 부여에 소요 된 시간 모든 누락 데이터 프로필/시간으로 유용 합니다. 내 타이머를 확인할 수 있습니다 [프로 파일링 하 고 Azure에 ASP.NET MVC 앱 시간](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)합니다. 합니다 [탭](http://getglimpse.com/Docs/Tabs) 페이지 각 탭에서 자세한 정보 링크를 제공 합니다.

<a id="Time"></a>
## <a name="the-timeline-tab"></a>타임 라인 탭

Tom Dykstra 수정 했지만 미해결 [EF 6/MVC 5 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 를 다음 코드로 강사 컨트롤러를 변경 합니다.

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

위의 코드 쿼리 문자열에 전달할 수 있습니다 (`eager`) 즉시 또는 명시적 컨트롤에 데이터 로드 합니다. 아래 이미지에서 명시적 로딩 사용 되 고 타이밍이 페이지에 로드 된 각 등록에 표시 된 `Index` 작업 메서드:

![명시적 로드(explicit loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

다음 코드를 즉시를 지정 하 고 각 등록 후 인출 되는 `Index` 라는:

![eager 지정](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

자세한 타이밍 정보를 가져올 시간 세그먼트 위로 가져가면 수 있습니다.

![자세한 타이밍을 보려면 가리키기](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>모델 바인딩

합니다 [모델 바인딩 탭](http://getglimpse.com/Docs/Model-Binding-Tab) 는 다양 한 폼 변수는 바인딩하는 방법 및 이유는 일부 바인딩되지 않은 예상한 대로 이해 하는 데 유용한 정보를 제공 합니다. 아래 이미지는 **?** 아이콘에 해당 기능에 대 한 간략 한 도움말을 클릭할 수 있습니다.

![모델 바인딩 뷰 기능 개요](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>경로

 Glimpse 경로 탭은 도움이 될 수 있습니다 디버그 및 라우팅 이해 합니다. 아래 이미지에서 제품 경로가 선택 됩니다 (및 간략 한 규칙을 녹색으로 표시). ![선택한 제품 이름을](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 경로 제약 조건, 영역 및 데이터 토큰에도 표시 됩니다. 참조 [Glimpse 경로](http://getglimpse.com/Docs/Routes-Tab) 하 고 [ASP.NET MVC 5의 특성 라우팅](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) 자세한 내용은 합니다. 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>Glimpse를 사용 하 여 Azure에서

간략 한 기본 보안 정책을 이해 표시할 데이터를 로컬 호스트에서 허용 합니다. 원격 서버 (예: Azure에서 웹 앱)에서이 데이터를 볼 수 있도록이 보안 정책을 변경할 수 있습니다. Azure에서 테스트 환경에 대 한 아래쪽까지 강조 표시를 추가 합니다 *web.confg* 눈에 볼 수 있도록 파일:

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

모든 사용자만이 변경으로 원격 사이트에 간략 한 데이터를 볼 수입니다. 에 배포할 수 있도록 적용 된 게시 프로필 (예를 들어 사용자 Azure 테스트 proifle.)를 사용 하는 경우 게시 프로필에 위의 태그를 추가 하는 것이 좋습니다. 간략 한 데이터를 제한 하려면 추가 `canViewGlimpseData` 역할만 간략 한 데이터를 보려면이 역할의 사용자를 허용 합니다.

주석을 제거 합니다 *GlimpseSecurityPolicy.cs* 파일을 변경 합니다 [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) 에서 호출 `Administrator` 에 `canViewGlimpseData` 역할:

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> 보안-Glimpse이 제공한 다양 한 데이터에는 앱의 보안을 노출 될 수 있습니다. 프로덕션 앱에서 사용 하기 위해 Microsoft Glimpse의 보안 감사를 수행 하지.


추가 역할에 대 한 정보를 참조 하세요. 필자의 [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 Azure에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) 자습서입니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 5 앱을 Azure에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- [구성에 간략하게](http://getglimpse.com/Docs/Configuration) -Doc 페이지 탭, 런타임 정책, 로깅 등을 구성 합니다.
