---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
title: ELMAH (VB)를 사용 하 여 오류 세부 정보를 로깅 | Microsoft Docs
author: rick-anderson
description: 오류 로깅 모듈 및 처리기 (ELMAH)는 또 다른 방법은 프로덕션 환경에서 런타임 오류 로그를 제공 합니다. ELMAH 무료 오픈 소스 오류가 발생 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: a5f0439f-18b2-4c89-96ab-75b02c616f46
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
msc.type: authoredcontent
ms.openlocfilehash: 584791a944c9e8eb0113da68719292f448573980
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "30891310"
---
<a name="logging-error-details-with-elmah-vb"></a>오류 세부 정보 ELMAH (VB)를 사용 하 여 로깅
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_vb.pdf)

> 오류 로깅 모듈 및 처리기 (ELMAH)는 또 다른 방법은 프로덕션 환경에서 런타임 오류 로그를 제공 합니다. ELMAH 오류를 필터링 하 고 로그를 보려면 오류 웹 페이지에서 RSS 피드로 하거나 쉼표로 구분 된 파일로 다운로드 하는 기능은 같은 기능을 포함 하는 무료 오픈 소스 오류 로깅 라이브러리입니다. 이 자습서를 다운로드 하 고 구성 ELMAH 안내 합니다.


## <a name="introduction"></a>소개

[이전 자습서](logging-error-details-with-asp-net-health-monitoring-vb.md) ASP를 검사 합니다. NET의 상태를 모니터링의 다양 한 종류의 웹 이벤트 기록에 대 한 상자 라이브러리를 제공 하는 시스템입니다. 대부분의 개발자 상태 로그온 하 고 처리 되지 않은 예외의 세부 정보를 전자 메일로 보내기 모니터링을 사용 합니다. 그러나이 시스템에 몇 가지 문제점 있습니다. 무엇 보다도 모든 종류 기록 된 이벤트에 대 한 정보를 보기 위한 사용자 인터페이스의 부족이입니다. 데이터베이스를 통해 어느 poke 해야 10 마지막 오류의 요약을 볼 또는 지난주에 발생 한 오류의 세부 정보를 확인 하려는 경우, 전자 메일 받은 편지함을 통해 검색 또는 정보를 표시 하는 웹 페이지는 `aspnet_WebEvent_Events` 테이블입니다.

다른 창 지점 상태 모니터링의 복잡성 중심으로 진행 합니다. 상태 모니터링도 사용할 수 있으므로 다양 한 다른 이벤트를 기록 하 고 다양 한 이벤트는 기록 하는 방법 및 시기를 지정 하는 것에 대 한 옵션 때문에 상태 시스템 모니터링을 올바르게 구성 성가실 태스크 수 있습니다. 마지막으로, 호환성 문제가 있습니다. ASP.NET 버전을 사용 하 여 작성 하는 오래 된 웹 응용 프로그램에 사용할 수 없는 상태 모니터링 먼저.NET Framework 버전 2.0에 추가 되었으므로, 1.x 합니다. 또한는 `SqlWebEventProvider` 클래스를 사용 하기 위해 데이터베이스에 오류 정보를 로그 이전 자습서에는 Microsoft SQL Server 데이터베이스 에서만 작동 합니다. 필요한 경우에 오류를 기록 하는 XML 파일 또는 Oracle 데이터베이스와 같은 대체 데이터 저장소에는 사용자 지정 로그 공급자 클래스를 만들 해야 합니다.

상태 시스템을 모니터링 하는 대신 오류 로깅 모듈 및 처리기 (ELMAH) 하 여 작성 된 무료 오픈 소스 오류 로깅 시스템은 [Atif Aziz](http://www.raboof.com/)합니다. 두 시스템 간의 가장 주목할 만한 차이점은 ELAMH의 오류 및 웹 페이지에서 및 특정 오류의 세부 정보를 RSS 피드로 목록을 표시 하는 기능입니다. ELMAH 상태 모니터링만 오류를 기록 하기 때문에 보다 구성 하기 쉽습니다. 또한 ELMAH ASP.NET 1.x, ASP.NET 2.0 및 ASP.NET 3.5 응용 프로그램 및 다양 한 로그 소스 공급자와 함께 제공 되며가에 대 한 지원이 포함 되어 있습니다.

이 자습서에 ELMAH ASP.NET 응용 프로그램에 추가 하는 단계를 안내 합니다. 이제 시작 하겠습니다.

> [!NOTE]
> 상태 시스템 및 ELMAH 모니터링 둘 다의 장단점 자신의 집합입니다. 확인해 보십시오 두 시스템을 시도 하 고 어떤 하나 되는 가장 좋은 결정할 필요 합니다.


## <a name="adding-elmah-to-an-aspnet-web-application"></a>ELMAH는 ASP.NET 웹 응용 프로그램에 추가

새로운 또는 기존 ASP.NET 응용 프로그램에 통합 하는 ELMAH 5 분 이내에 사용 하는 쉽고 간단한 프로세스입니다. 간단히 말해서 4 개의 간단한 단계가 포함 됩니다.

1. ELMAH를 다운로드 하 여 추가 된 `Elmah.dll` 웹 응용 프로그램에 어셈블리
2. ELMAH의 HTTP 모듈 및 처리기에 등록 `Web.config`,
3. ELMAH의 구성 옵션을 지정 하 고
4. 필요한 경우 오류 로그 원본 인프라를 만듭니다.

한 번에 하나씩 다음 네 단계를 살펴보겠습니다.

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>1 단계: ELMAH 프로젝트 파일을 다운로드 하 고 추가`Elmah.dll`웹 응용 프로그램

ELMAH 1.0 BETA 3 (빌드 10617) 문서 작성 당시 최신 버전은이 자습서와 함께 제공 되는 다운로드에 포함 됩니다. 방문할 수 있습니다는 [ELMAH 웹 사이트](https://code.google.com/p/elmah/) 최신 버전을 얻으려면 또는 소스 코드를 다운로드 합니다. ELMAH 다운로드 바탕 화면에 폴더에 압축을 풀고 ELMAH 어셈블리 파일을 찾습니다 (`Elmah.dll`).

> [!NOTE]
> `Elmah.dll` 다운로드의 파일은 `Bin` 폴더에 대 한 서로 다른.NET Framework 버전 및 릴리스 및 디버그 빌드에 대 한 하위 폴더에 있습니다. 릴리스 빌드를 사용 하 여 적절 한 프레임 워크 버전에 대 한 합니다. 예를 들어, ASP.NET 3.5 웹 응용 프로그램을 작성 하는 경우 복사는 `Elmah.dll` 에서 파일을 `Bin\net-3.5\Release` 폴더입니다.


다음으로 Visual Studio를 열고 솔루션 탐색기와 상황에 맞는 메뉴에서 선택 하면 추가 참조에 웹 사이트 이름을 마우스 오른쪽 단추로 클릭 하 여 프로젝트에 어셈블리를 추가 합니다. 이 참조 추가 대화 상자를 엽니다. 찾아보기 탭으로 이동 하 고 선택 된 `Elmah.dll` 파일입니다. 이 작업을 추가 `Elmah.dll` 파일을 웹 응용 프로그램의 `Bin` 폴더입니다.

> [!NOTE]
> 응용 프로그램 프로젝트 WAP (웹) 형식이 표시 되지 않습니다는 `Bin` 솔루션 탐색기에서 폴더입니다. 대신, 참조 폴더에서 이러한 항목을 나열 합니다.


`Elmah.dll` 어셈블리 ELMAH 시스템에서 사용 되는 클래스를 포함 합니다. 이러한 클래스는 세 가지 범주 중 하나에 속합니다.

- **HTTP 모듈** -HTTP 모듈에 대 한 이벤트 처리기를 정의 하는 클래스를은 `HttpApplication` 이벤트와 같은 `Error` 이벤트입니다. ELMAH 있는 세 가지 가장 콘텐츠와 구성을 여러 HTTP 모듈 포함 되 고 있습니다. 

    - `ErrorLogModule` -로그 소스에 처리 되지 않은 예외를 기록 합니다.
    - `ErrorMailModule` -전자 메일 메시지의 처리 되지 않은 예외의 세부 정보를 보냅니다.
    - `ErrorFilterModule` -어떤 예외가 기록를 결정 하는 개발자가 지정한 필터를 적용 되는 무시 됩니다.
- **HTTP 처리기** -HTTP 처리기는 특정 유형의 요청에 대 한 태그를 생성을 담당 하는 클래스입니다. ELMAH 오류 세부 정보를 웹 페이지, RSS 피드, 또는 쉼표로 구분 된 파일 (CSV) 렌더링 하는 HTTP 처리기를 포함 합니다.
- **오류 로그 소소** -즉시 ELMAH를 메모리에서 Oracle 데이터베이스에는 Microsoft Access 데이터베이스에는 Microsoft SQL Server 데이터베이스에 오류를 기록할 수 있습니다 또는 Vista DB 데이터베이스 SQLite 데이터베이스에 XML 파일입니다. 모니터링 시스템 상태와 같은 ELMAH의 아키텍처는 공급자 모델을 만들 수 있으며 필요한 경우 고유한 사용자 지정 로그 소스 공급자를 원활 하 게 통합 의미를 사용 하 여 빌드 되었습니다.

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>2 단계: ELMAH의 HTTP 모듈 및 이벤트 처리기를 등록합니다.

반면는 `Elmah.dll` HTTP 모듈을 포함 하는 파일 및 처리기 자동으로 처리 되지 않은 예외를 기록 하 고 웹 페이지에서 오류 세부 정보를 표시 하는 데 필요한, 이러한 명시적으로 등록 해야 웹 응용 프로그램의 구성 합니다. `ErrorLogModule` HTTP 모듈을 등록 한 후 구독 하는 `HttpApplication`의 `Error` 이벤트입니다. 이 이벤트는 발생 하는 경우는 `ErrorLogModule` 지정 된 로그 소스에 예외 정보를 기록 합니다. 다음 섹션에 로그 소스 공급자를 정의 하는 방법을 살펴보려는 "" ELMAH 구성 합니다. `ErrorLogPageFactory` HTTP 처리기 팩터리는 웹 페이지에서 오류 로그를 볼 때 태그를 생성 하는 일을 담당 합니다.

사이트를 부팅 하는 웹 서버에 HTTP 모듈 및 처리기를 등록 하기 위한 특정 구문에 따라 다릅니다. ASP.NET Development Server와 Microsoft의 IIS 6.0 및 이전 버전에 대 한 HTTP 모듈 및 처리기에 등록 된는 `<httpModules>` 및 `<httpHandlers>` 섹션 내에서 표시 되는 `<system.web>` 요소입니다. IIS 7.0을 사용 하는 경우에 등록 하는 데 필요한는 `<system.webServer>` 요소의 `<modules>` 및 `<handlers>` 섹션. 다행히 HTTP 모듈 및 처리기를 정의할 수 있습니다 *둘 다* 사용 중인 웹 서버에 관계 없이 배치 합니다. 이 옵션은 대부분의 휴대용 동일한 구성을 사용 하 고 웹 서버에 관계 없이 개발 및 프로덕션 환경에서 사용할 수 있게 하므로 합니다.

등록 하 여 시작 된 `ErrorLogModule` HTTP 모듈 및 `ErrorLogPageFactory` 에서 HTTP 처리기는 `<httpModules>` 및 `<httpHandlers>` 섹션 `<system.web>`합니다. 정의 하는 경우 구성에 이미이 두 요소 다음 단순히 포함는 `<add>` ELMAH의 HTTP 모듈 및 이벤트 처리기에 대 한 요소입니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample1.xml)]

다음으로 ELMAH의 HTTP 모듈 및 처리기를 등록 된 `<system.webServer>` 요소입니다. 이전 처럼이 요소는 이미 구성에 추가 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample2.xml)]

기본적으로 IIS 7 불만 HTTP 모듈 및 처리기에 등록 된 경우는 `<system.web>` 섹션. `validateIntegratedModeConfiguration` 특성에 `<validation>` 요소를 이러한 오류 메시지를 표시 하지 않는 IIS 7 하도록 지시 합니다.

등록 하기 위한 구문을 `ErrorLogPageFactory` HTTP 처리기에 포함 되어는 `path` 특성으로 설정 된 `elmah.axd`합니다. 이 특성 되는 경우 웹 응용 프로그램에 알립니다 요청이 도착 하는 명명 된 페이지에 대 한 `elmah.axd` 요청에서 처리 되어야 한다는 한 다음는 `ErrorLogPageFactory` HTTP 처리기입니다. 볼 수 있겠지만,는 `ErrorLogPageFactory` 이 자습서의 뒷부분에 나오는 작업에서 HTTP 처리기입니다.

### <a name="step-3-configuring-elmah"></a>3 단계: ELMAH 구성

웹 사이트에서 해당 구성 옵션에 대 한 ELMAH 찾습니다 `Web.config` 라는 사용자 지정 구성 섹션에는 파일 `<elmah>`합니다. 사용자 지정 섹션을 사용 하려면 `Web.config` 에 먼저 정의 되어야 합니다는 `<configSections>` 요소입니다. 열기는 `Web.config` 파일을 다음 태그를 추가 `<configSections>`:

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample3.xml)]

> [!NOTE]
> ELMAH ASP.NET 1.x 응용 프로그램에 대 한 구성 하는 경우 다음 제거는 `requirePermission="false"` 에서 특성은 `<section>` 위의 요소.


위의 구문에는 사용자 지정 등록 `<elmah>` 섹션과 하위: `<security>`, `<errorLog>`, `<errorMail>`, 및 `<errorFilter>`합니다.

다음으로 추가 된 `<elmah>` 섹션을 `Web.config`합니다. 이 섹션은 동일한 수준으로 표시 됩니다는 `<system.web>` 요소입니다. 내에서 `<elmah>` 섹션 추가 `<security>` 및 `<errorLog>` 같이 섹션:

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample4.xml)]

`<security>` 섹션의 `allowRemoteAccess` 원격 액세스 허용 되는지 여부를 나타내는 특성입니다. 이 값을 0으로 설정 하는 경우 다음 오류 로그 웹 페이지 에서만 볼 수 있습니다 로컬로 합니다. 이 특성이 1로 설정 된 오류 로그 웹 페이지 원격 및 로컬 방문자에 대해 활성화 됩니다. 지금은 보겠습니다 원격 방문자를 오류 로그 웹 페이지를 비활성화 합니다. 그러한 작업의 보안 문제를 논의할 기회를 가져온 다음 나중에 원격 액세스를 허용 합니다.

`<errorLog>` 섹션에 있는 오류 세부 정보 기록 되지만 비슷합니다는 중 오류 로그 원본 정의 `<providers>` 는 상태 시스템 모니터링 섹션입니다. 위의 구문은 지정 된 `SqlErrorLog` 클래스에 의해 지정 된 Microsoft SQL Server 데이터베이스 오류를 기록 하는 오류 로그 원본으로는 `connectionStringName` 특성 값입니다.

> [!NOTE]
> ELMAH 오류를 기록 하는 XML 파일, Microsoft Access 데이터베이스, Oracle 데이터베이스 및 다른 데이터 저장소를 사용할 수 있는 추가 오류 로그 공급자와 함께 제공 됩니다. 이 샘플을 참조 `Web.config` 이러한 대체 오류 로그 공급자를 사용 하는 방법에 대 한 내용은 ELMAH 다운로드에 포함 된 파일입니다.


### <a name="step-4-creating-the-error-log-source-infrastructure"></a>4 단계: 만들기 오류 로그 소스 인프라

ELMAH의 `SqlErrorLog` 공급자는 지정된 된 Microsoft SQL Server 데이터베이스에 오류 세부 정보를 기록 합니다. `SqlErrorLog` 공급자가이 데이터베이스 이라는 테이블이를 원하는 `ELMAH_Error` 및 3 개의 저장 프로시저: `ELMAH_GetErrorsXml`, `ELMAH_GetErrorXml`, 및 `ELMAH_LogError`합니다. ELMAH 다운로드에는 `SQLServer.sql` 에 `db` 저장 프로시저를이 테이블 및 이러한 만들기에 대 한 T-SQL 포함 된 폴더입니다. 사용 하려면 데이터베이스에서 이러한 문을 실행 해야는 `SqlErrorLog` 공급자입니다.

**그림 1** 및 **2** 에 필요한 데이터베이스 개체 후 Visual Studio에서 데이터베이스 탐색기에 표시 된 `SqlErrorLog` 공급자 추가 되었습니다.

[![](logging-error-details-with-elmah-vb/_static/image2.png)](logging-error-details-with-elmah-vb/_static/image1.png)

**그림 1**:는 `SqlErrorLog` 공급자에 대 한 오류 로그에 기록 된 `ELMAH_Error` 테이블

[![](logging-error-details-with-elmah-vb/_static/image4.png)](logging-error-details-with-elmah-vb/_static/image3.png)

**그림 2**:는 `SqlErrorLog` 공급자 3 개의 저장된 프로시저를 사용 하 여

## <a name="elmah-in-action"></a>동작에서 ELMAH

이 시점에서 ELMAH 등록 웹 응용 프로그램에 추가 했습니다는 `ErrorLogModule` HTTP 모듈 및 `ErrorLogPageFactory` HTTP 처리기에서 ELMAH의 구성 옵션을 지정 된 `Web.config`, 필요한 데이터베이스 개체에 대 한 추가 `SqlErrorLog` 오류 로그 공급자입니다. 이제 ELMAH 방법이 작동 되는지 확인 준비가 되었습니다! 책 검토 웹사이트를 방문와 같은 런타임 오류를 생성 하는 페이지를 방문 `Genre.aspx?ID=foo`, 또는 존재 하지 않는 페이지와 같은 `NoSuchPage.aspx`합니다. 에 따라 달라 집니다 이러한 페이지를 방문 하는 경우에 표시 된 `<customErrors>` 구성 및 로컬 또는 원격으로 방문 중인 여부. (다시 참조는 [ *사용자 지정 오류 페이지 표시* 자습서](displaying-a-custom-error-page-vb.md) 이 항목에 대 한 세부 정보에 대 한.)

ELMAH는 콘텐츠 처리 되지 않은 예외가 발생할 때 사용자에 게 표시는 영향을 주지 않습니다. 방금 세부 정보를 기록합니다. 이 오류 로그는 웹 페이지에서 액세스할 수 있는 `elmah.axd` 웹 사이트의 루트 로부터 같은 `http://localhost/BookReviews/elmah.axd`합니다. (이 파일에 대 한 요청이 들어올 경우 있지만 프로젝트에 실제로 존재 하지 않는 `elmah.axd` 런타임을 디스패치합니다는 `ErrorLogPageFactory` 브라우저에 다시 전송 하는 태그를 생성 하는 HTTP 처리기입니다.)

> [!NOTE]
> 사용할 수도 있습니다는 `elmah.axd` ELMAH 테스트 오류를 생성 하 게 지시 하는 페이지입니다. 방문 `elmah.axd/test` (에서 같이 `http://localhost/BookReviews/elmah.axd/test`) ELMAH 형식의 예외를 throw 하면 `Elmah.TestException`, 오류 메시지를 있는: "이는 안전 하 게 무시할 수 있는 테스트 예외입니다."


**그림 3** 을 방문할 때 오류 로그를 보여 줍니다. `elmah.axd` 개발 환경에서입니다.

[![](logging-error-details-with-elmah-vb/_static/image6.png)](logging-error-details-with-elmah-vb/_static/image5.png)

**그림 3**: `Elmah.axd` 웹 페이지에서 오류 로그를 표시 합니다.  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image7.png))

오류 로그인 **그림 3** 6 개 오류 항목을 포함 합니다. 각 항목에는 HTTP 상태 코드 (404 또는 이러한 오류에 대 한 500), 유형, 설명, 오류가 발생할 때 로그온된 한 사용자의 이름 및 날짜 및 시간 포함 됩니다. 세부 정보 링크를 클릭 하는 오류 세부 정보 노란색 화면의 사망에 표시 된 동일한 오류 메시지가 포함 된 페이지가 표시 됩니다. (참조 **그림 4**)는 오류 발생 시 서버 변수 값과 함께 (참조  **그림 5**). 또한 HTTP POST 헤더에 값과 같은 추가 정보를 포함 하는 오류 정보가 저장 되는 원시 XML을 볼 수 있습니다.

[![](logging-error-details-with-elmah-vb/_static/image9.png)](logging-error-details-with-elmah-vb/_static/image8.png)

**그림 4**: YSOD 오류 세부 정보를 보려면  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image10.png))

[![](logging-error-details-with-elmah-vb/_static/image12.png)](logging-error-details-with-elmah-vb/_static/image11.png)

**그림 5**:는 오류 발생 시 서버 변수 컬렉션의 값을 탐색 합니다.  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image13.png))

ELMAH 프로덕션 웹 사이트에 배포 하는 과정이 수반 됩니다.

- 복사는 `Elmah.dll` 파일을 여 `Bin` 프로덕션 환경에는 폴더
- ELMAH 관련 구성 설정을 복사는 `Web.config` 프로덕션에 사용 되는 파일 및
- 프로덕션 데이터베이스를 오류 로그 원본 인프라를 추가 합니다.

이전 자습서에서 프로덕션으로 개발에서 파일을 복사 하기 위한 기술에서 살펴본 했습니다. 프로덕션 데이터베이스를 오류 로그 원본 인프라를 받을 수는 가장 쉬운 방법은 가장 프로덕션 데이터베이스에 연결 하 고 다음 실행할 SQL Server Management Studio를 사용 하 여 `SqlServer.sql` 됩니다 필요한 테이블을 만들지 않고 저장 여부를 지정 하는 스크립트 파일 프로시저입니다.

### <a name="viewing-the-error-details-page-on-production"></a>프로덕션에서 오류 세부 정보 페이지 보기

사이트를 프로덕션에 배포 후 프로덕션 웹 사이트를 방문 하 고 처리 되지 않은 예외를 생성 합니다. 개발 환경에서와 같이 ELMAH 영향을 미치지 않습니다 처리 되지 않은 예외가 발생할 때 표시 되는 오류 페이지 대신, 오류만 기록합니다. 오류 로그 페이지를 방문 하려고 하면 (`elmah.axd`) 프로덕션 환경에서 있습니다 됩니다 될 설정에 사용할 수 없음 페이지 **그림 6**합니다.

[![](logging-error-details-with-elmah-vb/_static/image15.png)](logging-error-details-with-elmah-vb/_static/image14.png)

**그림 6**: 원격 방문자가 기본적으로 오류 로그 웹 페이지를 볼 수 없습니다  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image16.png))

ELMAH 구성에서 이전에 설명한 대로 `<security>` 설정 섹션에서 `allowRemoteAccess` 특성을 0으로, 원격 사용자가 오류 로그를 볼 수 없도록 금지 합니다. 오류 세부 정보는 보안 문제 또는 기타 중요 한 정보에 나타날 수 있습니다으로 오류 로그를 볼 수 없도록 익명 방문자를 금지 하는 것이 유용 합니다. 이 특성을 1로 설정 하 고 오류 로그에 대 한 원격 액세스를 사용 하도록 설정 하려는 경우 잠금 해야는 `elmah.axd` 방문자 권한 있으므로 경로 액세스할 수 있습니다. 이 작업을 추가 하 여 수행할 수는 `<location>` 요소에는 `Web.config` 파일입니다.

오류 로그 웹 페이지에 액세스 하려면 관리자 역할의 사용자만을 허용 하는 다음 구성:

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample5.xml)]

> [!NOTE]
> -Scott, Jisun, 및 Alice-시스템의 세 가지 사용자 및 관리자 역할에 추가 된는 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-vb.md)합니다. 사용자 Scott 및 Jisun는 관리자 역할의 멤버입니다. 인증 및 권한 부여에 대 한 자세한 내용은 참조 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.


원격 사용자가; 이제 프로덕션 환경에서 오류 로그를 볼 수 다시 참조 **그림 3**, **4**, 및 **5** 오류 로그 웹 페이지의 스크린 샷을 대 한 합니다. 그러나 오류 로그 페이지를 보려면 익명 또는 관리자가 아닌 사용자가 자동으로 리디렉션됩니다 로그인 페이지로 (`Login.aspx`),으로 **그림 7** 보여 줍니다.

[![](logging-error-details-with-elmah-vb/_static/image18.png)](logging-error-details-with-elmah-vb/_static/image17.png)

**그림 7**: 권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다.  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image19.png))

### <a name="programmatically-logging-errors"></a>프로그래밍 방식으로 오류 로깅

ELMAH의 `ErrorLogModule` HTTP 모듈 지정 된 로그 소스를 자동으로 처리 되지 않은 예외를 기록 합니다. 사용 하 여 처리 되지 않은 예외가 발생 하지 않고 오류를 로그할 수 또는 `ErrorSignal` 클래스 및 해당 `Raise` 메서드. `Raise` 메서드에 전달 되는 `Exception` 개체 하 고 해당 예외를 throw 되었다는 사실 및가 처리 하지 않고 ASP.NET 런타임이 도달한 마치 기록 합니다. 그러나 한다는 점에서 차이가 요청 후 정상적으로 실행을 계속 하는 `Raise` 메서드를 호출한 반면는 throw 된 처리 되지 않은 예외를 요청의 정상적인 실행을 중단 하 고 구성 된 표시할 ASP.NET 런타임이 오류 페이지입니다.

`ErrorSignal` 클래스는 해당 오류가 수행 되는 전체 작업 치명적인 있고 오류가 발생할 수 있는 몇 가지 작업이 있는 경우에 유용 합니다. 예를 들어, 웹 사이트, 사용자의 입력을 사용 하 고,는 데이터베이스에 저장 하 고, 다음 사용자를 알리는 전자 메일 보내는 양식을 포함할 수 있습니다는 정보를 처리 합니다. 정보는 데이터베이스에 성공적으로 저장 되지만 전자 메일 메시지를 보낼 때 오류가 발생 하는 경우 수행할 작업? 한 가지 예외를 throw 하 고 사용자에 게 보낼 오류 페이지를 수 있습니다. 그러나 사용자를 입력 한다 정보 저장 되지 않았습니다 혼동이 있습니다. 또 다른 방법은 전자 메일 관련 오류를 기록 하는 사용자의 경험에 전혀 변경 하지 것입니다. 여기에는 `ErrorSignal` 클래스는 유용 합니다.

[!code-vb[Main](logging-error-details-with-elmah-vb/samples/sample6.vb)]

## <a name="error-notification-via-email"></a>전자 메일을 통해 오류 알림

데이터베이스에 오류와 함께 ELMAH 오류 세부 정보 지정 된 받는 사람에 게 전자 메일을 구성할 수도 있습니다. 이 기능을 제공는 `ErrorMailModule` HTTP 모듈에서이 HTTP 모듈을 등록 해야 따라서 `Web.config` 전자 메일을 통해 오류 정보를 전송 하기 위해.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample7.xml)]

그런 다음 오류 메일에 대 한 정보를 지정는 `<elmah>` 요소의 `<errorMail>` 메일의 보낸 사람과 받는 사람, 제목, 나타내는 섹션 여부는 전자 메일 비동기적으로 전송 됩니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample8.xml)]

위치에 위의 설정을 사용 하면 런타임 오류가 발생할 때마다 ELMAH 메일을 보냅니다 support@example.com 오류 세부 정보를 사용 합니다. ELMAH의 오류 전자 메일 오류 메시지, 스택 추적 및 서버 변수 즉 오류 세부 정보 웹 페이지에 표시 된 것 같은 정보가 포함 됩니다 (다시 참조 **그림 4** 및 **5**). 오류 전자 메일 첨부 파일로 예외 세부 정보 노란색 화면의 사망 콘텐츠가 포함 되어 (`YSOD.html`).

**그림 8** ELMAH의 오류 방문 하 여 생성 된 전자 메일을 보여 줍니다 `Genre.aspx?ID=foo`합니다. 반면 **그림 8** 서버 변수도 복사 추가 아래로 메일의 본문에만 오류 메시지 및 스택 추적을 보여 줍니다.

[![](logging-error-details-with-elmah-vb/_static/image21.png)](logging-error-details-with-elmah-vb/_static/image20.png)

**그림 8**: ELMAH 보낼 전자 메일을 통해 오류 정보를 구성할 수 있습니다  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image22.png))

## <a name="only-logging-errors-of-interest"></a>만 관심 있는 오류를 로깅

기본적으로 ELMAH 404 및 기타 HTTP 오류를 포함 하 여 처리 되지 않은 모든 예외의 세부 정보를 기록 합니다. ELMAH 이러한 열 데이터 나 다른 유형의 오류를 필터링을 사용 하 여 오류를 무시 하도록 지시할 수 있습니다. 필터링 논리 ELMAH의 수행한 `ErrorFilterModule` 에 등록 해야 하는 HTTP 모듈 `Web.config` 필터링 논리를 사용 하려면. 필터링에 대 한 규칙에 지정 된는 `<errorFilter>` 섹션.

다음 태그 ELMAH 404 오류를 기록 하지를 지시 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample9.xml)]

> [!NOTE]
> 오류를 등록 해야 필터링을 사용 하기 위해 반드시 여 `ErrorFilterModule` HTTP 모듈입니다.


`<equal>` 요소 안에 `<test>` 섹션 어설션을 라고 합니다. True로 평가 되 고 어설션 오류 ELMAH의 로그에서 필터링 됩니다. 모두 포함 하 여 사용 가능한 다른 어설션: `<greater>`, `<greater-or-equal>`, `<not-equal>`, `<lesser>`, `<lesser-or-equal>`등입니다. 어설션을 사용 하 여 결합할 수도 있습니다는 `<and>` 및 `<or>` 부울 연산자입니다. 게다가를 어설션으로 간단한 JavaScript 식을 포함 하거나 C# 또는 Visual Basic 해당 어설션을 작성할 수 있습니다.

필터링 기능 ELMAH의 오류에 대 한 자세한 내용은 참조는 [섹션 오류를 필터링](https://code.google.com/p/elmah/wiki/ErrorFiltering) 에 [ELMAH wiki](https://code.google.com/p/elmah/w/list)합니다.

## <a name="summary"></a>요약

ELMAH는 ASP.NET 웹 응용 프로그램에서 오류를 기록 하는 단순 하면서도 강력한 메커니즘을 제공합니다. Microsoft의 상태 모니터링 시스템 같이 ELMAH 데이터베이스에 오류를 로깅할 수 있으며 전자 메일을 통해 개발자에 게 오류 세부 정보를 보낼 수 있습니다. 모니터링 시스템 상태와는 달리 ELMAH 보다 넓은 범위의 포함 하 여 오류 로그 데이터 저장소에 대 한 상자 지원이 중지 포함: Microsoft SQL Server, Microsoft Access, Oracle, XML 파일, 이후 몇 개의. ELMAH에서는 오류 로그 및 웹 페이지에서 특정 오류에 대 한 세부 정보를 보기 위한 기본 제공 메커니즘을 제공 하는 또한 `elmah.axd`합니다. `elmah.axd` 페이지 RSS 피드로 또는 Microsoft Excel을 사용 하 여 읽을 수 있는 쉼표로 구분 된 값 파일 (CSV)로 오류 정보를 렌더링할 수도 있습니다. 선언적 또는 프로그래밍 방식으로 어설션을 사용 하 여 로그에서 오류를 필터링 할 ELMAH를 지시할 수 있습니다. 및 ELMAH ASP.NET 버전 1.x 응용 프로그램과 함께 사용할 수 있습니다.

모든 배포 응용 프로그램을 자동으로 처리 되지 않은 예외를 로깅 및 알림 개발 팀에 전송 하기 위한 메커니즘이 있어야 합니다. 여부 이렇게 ELMAH 또는 상태 모니터링을 사용 하는 보조 데이터베이스입니다. 즉, 중요 하지 훨씬 사용할지 ELMAH; 또는 상태 모니터링 두 시스템을 평가 하 고 사용자의 요구에 가장 잘 맞는 하나를 선택 합니다. 기본적으로 중요 한 점은 메커니즘이 프로덕션 환경에서 처리 되지 않은 예외를 기록 하는 위치에 배치할 수입니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ELMAH-오류 로깅 모듈 및 처리기](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH 프로젝트 페이지](https://code.google.com/p/elmah/) (소스 코드, 샘플, wiki)
- [ELMAH에는 웹 응용 프로그램 처리 되지 않은 예외를 Catch 연결](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx) (비디오)
- [보안 오류 로그 페이지](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [HTTP 모듈 및 처리기를 사용 하 여 플러그형 ASP.NET 구성 요소 만들기](https://msdn.microsoft.com/library/aa479332.aspx)
- [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [이전](logging-error-details-with-asp-net-health-monitoring-vb.md)
> [다음](precompiling-your-website-vb.md)
