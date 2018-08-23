---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
title: ELMAH (C#)를 사용 하 여 오류 세부 정보 로깅 | Microsoft Docs
author: rick-anderson
description: 오류 로깅 모듈 및 처리기의 ELMAH ()는 프로덕션 환경에서 런타임 오류를 기록 하는 다른 방법은 제공 합니다. ELMAH는 무료 오픈 소스 오류...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 11f6fe44-64ef-4a38-a3b4-35c7bb992352
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
msc.type: authoredcontent
ms.openlocfilehash: 4337500e0da3c6a75737438f3eeed731350847dd
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837229"
---
<a name="logging-error-details-with-elmah-c"></a>ELMAH (C#)를 사용 하 여 오류 세부 정보 로깅
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_cs.pdf)

> 오류 로깅 모듈 및 처리기의 ELMAH ()는 프로덕션 환경에서 런타임 오류를 기록 하는 다른 방법은 제공 합니다. ELMAH는 오류 필터링 및 RSS 피드, 웹 페이지에서 오류 로그를 보려면 또는 쉼표로 구분 된 파일로 다운로드 하는 기능 등의 기능을 포함 하는 무료 오픈 소스 오류 로깅 라이브러리입니다. 이 자습서를 다운로드 하 고 ELMAH 구성 안내 합니다.


## <a name="introduction"></a>소개

합니다 [이전 자습서](logging-error-details-with-asp-net-health-monitoring-cs.md) ASP를 검사 합니다. NET의 상태 모니터링 시스템의 다양 한 웹 이벤트 기록에 대 한 상자 라이브러리를 제공 합니다. 대부분의 개발자는 상태를 로깅하고 전자 메일 처리 되지 않은 예외의 세부 정보 모니터링을 사용 합니다. 그러나이 시스템을 사용 하 여 몇 가지 문제점 있습니다. 무엇 보다도 부족 하다는 것 기록된 된 이벤트에 대 한 정보를 보기 위한 사용자 인터페이스의 모든 정렬 합니다. 데이터베이스를 통해 두 포크 해야 10 마지막 오류의 요약을 볼 또는 지난 주에 발생 한 오류의 세부 정보를 확인 하려는 경우, 전자 메일 받은 편지함을 검색할 또는 정보를 표시 하는 웹 페이지 작성을 `aspnet_WebEvent_Events` 테이블입니다.

상태 모니터링의 복잡성을 중심으로 다른 고민 합니다. 상태 모니터링을 사용할 수 있는 다양 한 여러 이벤트를 기록 하 고 다양 한 이벤트를 기록 하는 시기와 방법을 지시 하는 것에 대 한 옵션이 있기 때문에 상태 모니터링 시스템을 올바르게 구성 다루고자 하는 작업을 수 있습니다. 마지막으로, 호환성 문제가 있습니다. ASP.NET 버전을 사용 하 여 작성 하는 이전 웹 응용 프로그램에 사용할 수 없는 상태 모니터링 먼저.NET framework 버전 2.0에서에서 추가 되었으므로, 1.x 합니다. 또한는 `SqlWebEventProvider` 클래스를 데이터베이스에 로그 오류 세부 정보를 이전 자습서에서 사용 하는 Microsoft SQL Server 데이터베이스 에서만 작동 합니다. 클래스를 만드는 사용자 지정 로그 공급자는 XML 파일 또는 Oracle 데이터베이스와 같은 대체 데이터 저장소에 오류를 기록해 야 하는 것이 해야 합니다.

상태 시스템을 모니터링 하는 대신 오류 로깅 모듈 및 처리기의 ELMAH (), 무료, 오픈 소스 오류 로깅 시스템에서 생성 됩니다 [Atif Aziz](http://www.raboof.com/)합니다. 두 시스템 간의 가장 중요 한 차이점 하는 기능은 ELAMH의 RSS 피드로 오류 및 웹 페이지에서 특정 오류의 세부 정보 목록을 표시 합니다. ELMAH의 오류만 기록 하기 때문에 상태 모니터링 보다 구성 하기 쉽습니다. 또한 ELMAH ASP.NET 1.x에서 ASP.NET 2.0 및 ASP.NET 3.5 응용 프로그램 및 다양 한 로그 소스 공급자와 함께 제공 됩니다에 대 한 지원이 포함 되어 있습니다.

이 자습서는 ASP.NET 응용 프로그램에 ELMAH를 추가 하는 단계를 안내 합니다. 이제 시작 하겠습니다.

> [!NOTE]
> 장점 및 단점 자신의 집합이 둘 상태 시스템과 ELMAH를 모니터링 합니다. 바랍니다 요구를 사항을 두 시스템을 시도 하 고 가장 적합 한 어떤 하나를 결정할 수 있습니다.


## <a name="adding-elmah-to-an-aspnet-web-application"></a>ELMAH는 ASP.NET 웹 응용 프로그램에 추가

ELMAH를 신규 또는 기존 ASP.NET 응용 프로그램 통합 5 분을 사용 하는 쉽고 간단한 프로세스입니다. 간단히 말해 간단한 4 단계를 수행합니다.

1. ELMAH를 다운로드 하 고 추가 `Elmah.dll` 웹 응용 프로그램에 어셈블리
2. ELMAH의 HTTP 모듈 및 처리기의 등록 `Web.config`,
3. ELMAH의 구성 옵션을 지정 하 고
4. 필요한 경우, 오류 로그 원본 인프라를 만듭니다.

한 번에 하나씩 다음 네 단계를 살펴보겠습니다.

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>1 단계: ELMAH 프로젝트 파일을 다운로드 및 추가`Elmah.dll`웹 응용 프로그램

ELMAH 1.0 BETA 3 (빌드 10617) 문서 작성 당시에 최신 버전은이 자습서와 함께 제공 되는 다운로드에 포함 됩니다. 방문할 수 있습니다 합니다 [ELMAH 웹 사이트](https://code.google.com/p/elmah/) 가장 최근 버전 또는 소스 코드를 다운로드 합니다. ELMAH 다운로드 바탕 화면에 폴더를 압축을 풀고 ELMAH 어셈블리 파일을 찾습니다 (`Elmah.dll`).

> [!NOTE]
> 합니다 `Elmah.dll` 다운로드의 파일은 `Bin` 폴더에 있는 서로 다른.NET Framework 버전을 디버그 및 릴리스 빌드에 대 한 하위 폴더입니다. 적절 한 프레임 워크 버전에 대 한 릴리스 빌드를 사용 합니다. ASP.NET 3.5 웹 응용 프로그램을 작성 하는 경우 복사 하는 예를 들어 합니다 `Elmah.dll` 에서 파일을 `Bin\net-3.5\Release` 폴더입니다.


다음으로, Visual Studio를 열고 솔루션 탐색기에서 상황에 맞는 메뉴에서 선택 하면 추가 참조 웹 사이트 이름을 마우스 오른쪽 단추로 클릭 하 여 프로젝트에 어셈블리를 추가 합니다. 이 참조 추가 대화 상자를 엽니다. 찾아보기 탭으로 이동 하 고 선택 된 `Elmah.dll` 파일입니다. 이 작업을 추가 합니다 `Elmah.dll` 웹 응용 프로그램의 파일 `Bin` 폴더입니다.

> [!NOTE]
> 웹 응용 프로그램 프로젝트 (WAP) 형식을 표시 하지 않습니다는 `Bin` 솔루션 탐색기에서 폴더입니다. 대신 참조 폴더 아래에 있는 이러한 항목을 나열합니다.


`Elmah.dll` 어셈블리 ELMAH 시스템에서 사용 하는 클래스를 포함 합니다. 이러한 클래스는 세 가지 범주 중 하나에 속합니다.

- **HTTP 모듈** -HTTP 모듈은에 대 한 이벤트 처리기를 정의 하는 클래스 `HttpApplication` 이벤트와 같은 `Error` 이벤트입니다. ELMAH 여러 HTTP 모듈을 세 가지 가장 밀접 것 포함 되 고: 

    - `ErrorLogModule` -로그 원본에 처리 되지 않은 예외를 기록 합니다.
    - `ErrorMailModule` -전자 메일 메시지의 처리 되지 않은 예외의 세부 정보를 보냅니다.
    - `ErrorFilterModule` -예외에 대해 기록 됩니다 확인 하려면 개발자가 지정한 필터를 적용 합니다. 항목은 무시 됩니다.
- **HTTP 처리기** -HTTP 처리기는 특정 유형의 요청에 대 한 태그를 생성 하는 일을 담당 하는 클래스입니다. ELMAH는 웹 페이지, RSS 피드, 또는 쉼표로 구분 된 파일 (CSV) 오류 세부 정보를 렌더링 하는 HTTP 처리기를 포함 합니다.
- **오류 로그 소스** -ELMAH를 메모리, Microsoft Access 데이터베이스, Oracle 데이터베이스에는 Microsoft SQL Server 데이터베이스에 오류를 기록할 수 있습니다 기본를 SQLite 데이터베이스 또는 Vista DB 데이터베이스에 XML 파일입니다. ELMAH의 아키텍처에는 상태 시스템 모니터링와 같은 공급자 모델을 만들 수 있습니다 및 필요한 경우 사용자 고유의 사용자 지정 로그 소스 공급자를 원활 하 게 통합 의미를 사용 하 여 구축 되었습니다.

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>2 단계: ELMAH의 HTTP 모듈 및 처리기를 등록합니다.

하는 동안는 `Elmah.dll` 처리기 자동으로 처리 되지 않은 예외를 기록 하 고 웹 페이지에서 오류 세부 정보를 표시 하는 데 필요한 HTTP 모듈을 포함 하는 파일을이 명시적으로 등록 해야 웹 응용 프로그램의 구성 합니다. 합니다 `ErrorLogModule` 장치가 등록 되 면 HTTP 모듈을 구독 하는 `HttpApplication`의 `Error` 이벤트입니다. 이 이벤트는 발생 될 때마다는 `ErrorLogModule` 지정한 로그 원본에 예외의 세부 정보를 기록 합니다. 다음 섹션에서는 로그 원본 공급자를 정의 하는 방법을 살펴보겠습니다 "ELMAH 구성 합니다." `ErrorLogPageFactory` HTTP 처리기 팩터리는 웹 페이지에서 오류 로그를 볼 때 태그를 생성 하는 일을 담당 합니다.

HTTP 모듈 및 처리기를 등록 하기 위한 특정 구문을 사이트를 강화 하는 웹 서버에 따라 달라 집니다. HTTP 모듈 및 처리기는 ASP.NET 개발 서버와 Microsoft의 IIS 버전 6.0 및 이전 버전에 대 한 등록 합니다 `<httpModules>` 및 `<httpHandlers>` 섹션 내에서 나타나는 `<system.web>` 요소. IIS 7.0을 사용 하는 경우에 등록 해야 합니다 `<system.webServer>` 요소의 `<modules>` 및 `<handlers>` 섹션입니다. 다행 스럽게도 HTTP 모듈 및 처리기를 정의할 수 있습니다 *둘 다* 사용 중인 웹 서버에 관계 없이 배치 합니다. 이 옵션 가장 이식 가능한 것은 동일한 구성을 사용 하 고 웹 서버에 관계 없이 개발 및 프로덕션 환경에서 사용할 수 있습니다.

등록 하 여 시작 합니다 `ErrorLogModule` HTTP 모듈 및 `ErrorLogPageFactory` 에서 HTTP 처리기를 `<httpModules>` 하 고 `<httpHandlers>` 섹션 `<system.web>`. 정의 하는 경우 이미 구성에 이러한 두 요소 다음 단순히이 포함 된 `<add>` ELMAH의 HTTP 모듈 및 처리기에 대 한 요소입니다.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample1.xml)]

다음으로 ELMAH의 HTTP 모듈 및 처리기를 등록 합니다 `<system.webServer>` 요소입니다. 이전 처럼이 요소는 이미 구성에 있는 경우 추가 합니다.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample2.xml)]

기본적으로 IIS 7에서 HTTP 모듈 및 처리기에 등록 된 경우는 `<system.web>` 섹션입니다. `validateIntegratedModeConfiguration` 특성을 `<validation>` 요소에는 이러한 오류 메시지를 표시 하지 않으려면 IIS 7 하도록 지시 합니다.

등록에 대 한 구문 합니다 `ErrorLogPageFactory` HTTP 처리기를 포함를 `path` 로 설정 되어 있는 특성 `elmah.axd`합니다. 이 특성이 있는 경우 웹 응용 프로그램에 알립니다 라는 페이지에 대 한 요청이 도착 `elmah.axd` 하 여 요청을 처리한 다음는 `ErrorLogPageFactory` HTTP 처리기입니다. 살펴보겠습니다는 `ErrorLogPageFactory` 이 자습서의 뒷부분에 나오는 작업에서 HTTP 처리기입니다.

### <a name="step-3-configuring-elmah"></a>3 단계: ELMAH 구성

ELMAH는 웹 사이트의 해당 구성 옵션을 찾고 `Web.config` 라는 사용자 지정 구성 섹션에서 파일 `<elmah>`합니다. 사용자 지정 섹션을 사용 하려면 `Web.config` 에 먼저 정의 해야 합니다는 `<configSections>` 요소입니다. 엽니다는 `Web.config` 파일을 다음 태그를 추가 합니다 `<configSections>`:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample3.xml)]

> [!NOTE]
> ELMAH ASP.NET 1.x 응용 프로그램에 대 한 구성 하는 경우 제거 합니다는 `requirePermission="false"` 에서 특성을 `<section>` 위의 요소입니다.


위의 구문 등록 사용자 지정 `<elmah>` 섹션과 하위: `<security>`, `<errorLog>`합니다 `<errorMail>`, 및 `<errorFilter>`합니다.

다음을 추가 합니다 `<elmah>` 섹션을 `Web.config`입니다. 이 섹션에서는 동일한 수준으로 표시 됩니다는 `<system.web>` 요소입니다. 내를 `<elmah>` 섹션에 추가 합니다 `<security>` 및 `<errorLog>` 섹션에서는 다음과 같이:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample4.xml)]

합니다 `<security>` 섹션의 `allowRemoteAccess` 원격 액세스 허용 되는지 여부를 나타내는 특성입니다. 이 값을 0으로 설정 하는 경우 다음 오류 로그 웹 페이지만 볼 수 있습니다 로컬로 합니다. 이 특성은 1로 설정 하는 경우에 원격 및 로컬 방문자에 대 한 오류 로그 웹 페이지가 사용 됩니다. 지금은 보겠습니다 사용 하지 않도록 설정 오류 로그 웹 페이지 원격 방문자에 대 한 합니다. 그러한 작업의 보안 문제를 논의할 기회를 가져온 다음 나중에 원격 액세스를 허용 됩니다 것입니다.

합니다 `<errorLog>` 섹션에 있는 오류 세부 정보를 기록 됩니다. 즉, 비슷합니다는 중 오류 로그 원본 정의 `<providers>` 상태 시스템 모니터링 섹션입니다. 위의 구문에서 지정 합니다 `SqlErrorLog` 로 지정 된 Microsoft SQL Server 데이터베이스에 오류를 기록 하는 오류 로그 원본으로 클래스는 `connectionStringName` 특성 값입니다.

> [!NOTE]
> ELMAH는 오류를 기록 하는 XML 파일, Microsoft Access 데이터베이스, Oracle 데이터베이스 및 다른 데이터 저장소를 사용할 수 있는 추가 오류 로그 공급자를 사용 하 여 제공 됩니다. 샘플을 참조 하세요 `Web.config` 이러한 대체 오류 로그 공급자를 사용 하는 방법에 대 한 내용은 ELMAH 다운로드에 포함 된 파일입니다.


### <a name="step-4-creating-the-error-log-source-infrastructure"></a>4 단계: 오류 로그 원본 인프라 만들기

ELMAH의 `SqlErrorLog` 공급자를 지정된 하는 Microsoft SQL Server 데이터베이스에 오류 세부 정보를 기록 합니다. `SqlErrorLog` 공급자는이 데이터베이스 라는 테이블이 있을 `ELMAH_Error` 3 개의 저장 프로시저 및: `ELMAH_GetErrorsXml`, `ELMAH_GetErrorXml`, 및 `ELMAH_LogError`합니다. 라는 파일을 포함 하는 ELMAH 다운로드 `SQLServer.sql` 에 `db` 저장 프로시저를 만들고이 테이블 다음에 대 한 T-SQL을 포함 하는 폴더입니다. 사용 하려면 데이터베이스에서 이러한 문을 실행 해야 합니다 `SqlErrorLog` 공급자입니다.

**그림 1** 하 고 **2** 하 여 필요한 데이터베이스 개체 후 Visual Studio에서 데이터베이스 탐색기에 표시는 `SqlErrorLog` 공급자 추가 되었습니다.

[![](logging-error-details-with-elmah-cs/_static/image2.png)](logging-error-details-with-elmah-cs/_static/image1.png)

**그림 1**: 합니다 `SqlErrorLog` 공급자가 오류를 로깅하는 `ELMAH_Error` 테이블

[![](logging-error-details-with-elmah-cs/_static/image4.png)](logging-error-details-with-elmah-cs/_static/image3.png)

**그림 2**:는 `SqlErrorLog` 공급자는 3 개의 저장된 프로시저 사용

## <a name="elmah-in-action"></a>작업에서 ELMAH

이 시점에서 ELMAH 등록 웹 응용 프로그램에 추가 합니다 `ErrorLogModule` HTTP 모듈 및 `ErrorLogPageFactory` HTTP 처리기의 ELMAH의 구성 옵션을 지정 `Web.config`에서 필요한 데이터베이스 개체를 추가 하 고는 `SqlErrorLog` 오류 로그 공급자입니다. 이제 작업에서 ELMAH를 참조 하십시오. 준비가 되었습니다! 도 서 리뷰 웹 사이트를 방문 하 고 같은 런타임 오류를 생성 하는 페이지를 방문 `Genre.aspx?ID=foo`, 또는 존재 하지 않는 페이지와 같은 `NoSuchPage.aspx`합니다. 이러한 페이지를 방문할 때 표시 되는 내용에 따라 달라 집니다는 `<customErrors>` 구성 및 로컬 또는 원격으로 방문 중인 여부. (다시 참조를 [ *사용자 지정 오류 페이지 표시* 자습서](displaying-a-custom-error-page-cs.md) 이 항목에 대 한 합니다.)

ELMAH 처리 되지 않은 예외가 발생할 때 사용자에 게 콘텐츠 표시는 영향을 주지 않습니다. 만 해당 세부 정보를 기록 합니다. 이 오류 로그는 웹 페이지에서 액세스할 수 있습니다 `elmah.axd` 웹 사이트의 루트에서 같은 `http://localhost/BookReviews/elmah.axd`합니다. (이 파일에 대 한 요청이 들어올 때 있지만 프로젝트에 실제로 존재 하지 않습니다 `elmah.axd` 런타임에서를 디스패치합니다는 `ErrorLogPageFactory` 브라우저로 다시 전송 하는 태그를 생성 하는 HTTP 처리기입니다.)

> [!NOTE]
> 사용할 수도 있습니다는 `elmah.axd` 테스트 오류를 생성 하는 ELMAH를 지시 하는 페이지입니다. 방문 `elmah.axd/test` (에서 같이 `http://localhost/BookReviews/elmah.axd/test`) ELMAH 형식의 예외를 throw 하면 `Elmah.TestException`, 있는 오류 메시지: "This is 테스트 예외를 무시 해도 됩니다."


**그림 3** 방문할 때 오류 로그를 보여 줍니다. `elmah.axd` 개발 환경에서.

[![](logging-error-details-with-elmah-cs/_static/image6.png)](logging-error-details-with-elmah-cs/_static/image5.png)

**그림 3**: `Elmah.axd` 웹 페이지에서 오류 로그를 표시 합니다.  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-elmah-cs/_static/image7.png))

오류에 로그인 **그림 3** 6 오류 항목을 포함 합니다. 각 항목에는 HTTP 상태 코드 (404 또는 500 이러한 오류에 대 한), 형식, 설명, 오류가 발생할 때 로그온된 한 사용자의 이름 및 날짜 및 시간 포함 됩니다. 세부 정보 링크를 클릭 하면 오류 세부 정보 노란색 화면의 쇠퇴에 표시 된 동일한 오류 메시지가 포함 된 페이지가 표시 됩니다. (참조 **그림 4**) 오류 시 서버 변수 값과 함께 (참조  **그림 5**). 또한 HTTP POST 헤더의 값과 같은 추가 정보를 포함 하는 오류 세부 정보 저장 되는 원시 XML을 볼 수 있습니다.

[![](logging-error-details-with-elmah-cs/_static/image9.png)](logging-error-details-with-elmah-cs/_static/image8.png)

**그림 4**: YSOD 오류 세부 정보를 보려면  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-elmah-cs/_static/image10.png))

[![](logging-error-details-with-elmah-cs/_static/image12.png)](logging-error-details-with-elmah-cs/_static/image11.png)

**그림 5**: 오류 시 서버 변수 컬렉션의 값을 탐색  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-elmah-cs/_static/image13.png))

ELMAH는 프로덕션 웹 사이트에 배포 해야 합니다.

- 복사 합니다 `Elmah.dll` 파일을 `Bin` 프로덕션 폴더
- ELMAH 관련 구성 설정을 복사는 `Web.config` 프로덕션 환경에서 사용 되는 파일 및
- 프로덕션 데이터베이스에 오류 로그 원본 인프라를 추가 합니다.

이전 자습서에서 프로덕션으로 개발에서 파일을 복사 하는 기술을 살펴보았습니다. 프로덕션 데이터베이스에서 오류 로그 원본 인프라를 얻을 수 있는 가장 쉬운 방법은 가장 프로덕션 데이터베이스에 연결 하 고 실행 한 다음 SQL Server Management Studio를 사용 하 여 `SqlServer.sql` 는 필요한 테이블을 만들고 저장 하는 스크립트 파일 절차입니다.

### <a name="viewing-the-error-details-page-on-production"></a>프로덕션에서 오류 세부 정보 페이지를 보고합니다.

사이트를 프로덕션에 배포 후 프로덕션 웹 사이트를 방문 하 고 처리 되지 않은 예외를 생성 합니다. 개발 환경 처럼 ELMAH에 영향을 미치지 않습니다 처리 되지 않은 예외가 발생할 때 표시 되는 오류 페이지 대신, 단순히 오류를 기록 됩니다. 오류 로그 페이지를 방문 하면 (`elmah.axd`) 프로덕션 환경에서 있습니다 됩니다 수 셸과에 표시 된 사용 권한 없음 페이지로 **그림 6**합니다.

[![](logging-error-details-with-elmah-cs/_static/image15.png)](logging-error-details-with-elmah-cs/_static/image14.png)

**그림 6**: 원격 방문자가 기본적으로 오류 로그 웹 페이지를 볼 수 없습니다  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-elmah-cs/_static/image16.png))

ELMAH 구성에서 이전에 설명한 대로 `<security>` 설정 섹션을 `allowRemoteAccess` 특성을 0으로, 오류 로그 보기에서 원격 사용자를 금지 합니다. 오류 세부 정보는 보안 취약점으로 인 한 또는 기타 중요 한 정보 드러날 수 있습니다 하는 대로 오류 로그 보기에서 익명 방문자를 금지 하는 것이 반드시 합니다. 이 특성을 1로 설정 하 고 오류 로그에 대 한 원격 액세스를 사용 하도록 설정 하려는 경우를 잠그는 것은 `elmah.axd` 방문자만 권한 있는 경로 액세스할 수 있습니다. 추가 하 여 수행할 수 있습니다는 `<location>` 요소는 `Web.config` 파일입니다.

오류 로그 웹 페이지에 액세스 하려면 관리자 역할의 사용자만 허용 하는 다음 구성 합니다.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample5.xml)]

> [!NOTE]
> 시스템-Scott, Jisun,-Alice의에서 세 가지 사용자 및 관리자 역할에 추가 된 합니다 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md)합니다. 사용자 Scott Jisun와 관리자 역할의 멤버입니다. 인증 및 권한 부여에 대 한 자세한 내용은 참조 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.


원격 사용자; 이제 프로덕션 환경에서 오류 로그를 볼 수 다시 가리킵니다 **그림 3**를 **4**, 및 **5** 오류 로그 웹 페이지의 스크린 샷은 합니다. 그러나 익명 또는 관리자가 아닌 사용자는 오류 로그 페이지 보기를 시도할 경우 자동으로 리디렉션됩니다 로그인 페이지에 (`Login.aspx`),으로 **그림 7** 보여 줍니다.

[![](logging-error-details-with-elmah-cs/_static/image18.png)](logging-error-details-with-elmah-cs/_static/image17.png)

**그림 7**: 권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다.  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-elmah-cs/_static/image19.png))

### <a name="programmatically-logging-errors"></a>프로그래밍 방식으로 오류를 로깅

ELMAH의 `ErrorLogModule` HTTP 모듈이 지정한 로그 원본에 자동으로 처리 되지 않은 예외를 기록 합니다. 사용 하 여 처리 되지 않은 예외가 발생 하지 않고 오류를 로그할 수 또는 합니다 `ErrorSignal` 클래스 및 해당 `Raise` 메서드. 합니다 `Raise` 메서드에 전달 됩니다는 `Exception` 개체 및 해당 예외가 throw 되었다는 사실을 처리 하지 않고 ASP.NET 런타임이 도달한 처럼 기록 합니다. 차이점 것 인데, 요청 후 정상적으로 실행을 계속 하 여 `Raise` 메서드가 throw 된 처리 되지 않은 예외는 요청의 정상적인 실행을 중단 하 고 구성 된 표시할 ASP.NET 런타임에서 호출 되었습니다 오류 페이지입니다.

`ErrorSignal` 클래스는 실패할 수 있는 일부 작업은 있고 해당 오류가 수행 되는 전체 작업에 치명적일 수 있는 경우에 유용 합니다. 예를 들어 웹 사이트, 사용자 입력을 사용 하 고, 데이터베이스에 저장 하 고, 다음 사용자 알리는 전자 메일을 보냅니다는 폼 있을입니다 정보를 처리 합니다. 정보를 데이터베이스에 성공적으로 저장 되지만 전자 메일 메시지를 보낼 때 오류가 발생 하는 경우 수행할 작업? 첫째 예외를 throw 하 여 오류 페이지에 사용자를 보낼 것입니다. 그러나 듯한 오해는 입력 한 정보가 저장 되지 않았습니다 하는 사용자 혼동을 줄 수이 있습니다. 또 다른 방법은 전자 메일 관련 오류를 기록 하지만 어떤 방식으로 사용자의 환경을 변경 하지 것입니다. 이 경우는 `ErrorSignal` 클래스는 유용 합니다.

[!code-csharp[Main](logging-error-details-with-elmah-cs/samples/sample6.cs)]

## <a name="error-notification-via-email"></a>전자 메일을 통해 오류 알림

데이터베이스 오류와 함께 ELMAH는 지정 된 받는 사람에 게 전자 메일 오류 세부 정보를 구성할 수도 있습니다. 이 기능을 제공 합니다 `ErrorMailModule` HTTP 모듈에이 HTTP 모듈에서 등록 해야 하므로 `Web.config` 전자 메일을 통해 오류 정보를 전송 하기 위해.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample7.xml)]

다음으로에서 오류 전자 메일에 대 한 정보를 지정 합니다 `<elmah>` 요소의 `<errorMail>` 섹션에서는 전자 메일의 보낸 사람 및 받는 사람, 제목, 나타내는 전자 메일을 비동기식으로 전송 여부 및 합니다.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample8.xml)]

위치에 위의 설정을 사용 하 여 런타임 오류가 발생할 때마다 ELMAH 전자 메일을 보내는 support@example.com 오류 세부 정보를 사용 하 여 합니다. ELMAH의 오류 전자 메일에 오류 메시지, 스택 추적 및 서버 변수 namely 오류 세부 정보 웹 페이지에 표시 되는 동일한 정보를 포함 (다시 가리킵니다 **그림 4** 하 고 **5**). 오류 전자 메일 첨부 파일로 예외 세부 정보 노란색 화면 죽음의 내용에도 포함 되어 있습니다 (`YSOD.html`).

**그림 8** ELMAH의 오류 방문 하 여 생성 된 전자 메일을 보여 줍니다 `Genre.aspx?ID=foo`합니다. 하는 동안 **그림 8** 서버 변수가 아래쪽에 포함 되어 전자 메일의 본문에만 오류 메시지 및 스택 추적을 보여 줍니다.

[![](logging-error-details-with-elmah-cs/_static/image21.png)](logging-error-details-with-elmah-cs/_static/image20.png)

**그림 8**: 전자 메일을 통해 오류 정보를 보낼 ELMAH를 구성할 수 있습니다  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-elmah-cs/_static/image22.png))

## <a name="only-logging-errors-of-interest"></a>만 관심 오류 로깅

기본적으로 ELMAH는 404 등 다른 HTTP 오류 처리 되지 않은 모든 예외의 세부 정보를 기록 합니다. ELMAH 이러한 또는 다른 유형의 오류 필터링을 사용 하 여 오류를 무시 하도록 지시할 수 있습니다. 필터링 논리는 ELMAH의 수행한 `ErrorFilterModule` 에 등록 해야 하는 HTTP 모듈 `Web.config` 필터링 논리를 사용 하려면. 필터링에 대 한 규칙에 지정 된 된 `<errorFilter>` 섹션입니다.

다음 태그는 ELMAH를 404 오류를 기록 하지 지시 합니다.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample9.xml)]

> [!NOTE]
> 오류를 등록 해야 필터링을 사용 하려면 잊지는 `ErrorFilterModule` HTTP 모듈입니다.


합니다 `<equal>` 요소 내는 `<test>` 섹션 어설션 이라고 합니다. True로 평가 되 면 어설션이 ELMAH의 로그에서 오류 필터링 됩니다. 모두 포함 하 여 사용 가능한 다른 어설션: `<greater>`, `<greater-or-equal>`를 `<not-equal>`를 `<lesser>`, `<lesser-or-equal>`등입니다. 사용 하 여 어설션을 결합할 수도 있습니다는 `<and>` 고 `<or>` 부울 연산자입니다. 게다가 어설션으로 간단한 JavaScript 식을 포함 하거나 C# 또는 Visual Basic에서 사용자 고유의 어설션을 작성 수 있습니다.

ELMAH의 오류 필터링 기능에 대 한 자세한 내용은 참조는 [오류 필터링 섹션](https://code.google.com/p/elmah/wiki/ErrorFiltering) 에 [ELMAH wiki](https://code.google.com/p/elmah/w/list)합니다.

## <a name="summary"></a>요약

ELMAH는 ASP.NET 웹 응용 프로그램에서 오류를 기록 하는 단순 하면서도 강력한 메커니즘을 제공합니다. Microsoft의 상태 모니터링 시스템과 마찬가지로 ELMAH는 데이터베이스에 오류를 기록할 수 및 전자 메일을 통해 개발자에 게 오류 세부 정보를 보낼 수 있습니다. 에 상태 시스템 모니터링 달리 ELMAH 즉시 광범위 한 포함 하 여 오류 로그 데이터 저장소에 대 한 지원을 포함: Microsoft SQL Server, Microsoft Access, Oracle, XML 파일 및 기타 여러 가지입니다. ELMAH의 오류 로그 및 웹 페이지에서 특정 오류에 대 한 세부 정보 보기에 대 한 기본 제공 메커니즘을 제공 하는 또한 `elmah.axd`합니다. `elmah.axd` 페이지 RSS 피드 또는 Microsoft Excel을 사용 하 여 읽을 수 있는 쉼표로 구분 된 값 파일 (CSV)로 오류 정보를 렌더링할 수도 있습니다. 선언적 또는 프로그래밍 방식으로 어설션을 사용 하 여 로그에서 오류를 필터링 할 ELMAH를 지시할 수 있습니다. 및 ELMAH는 ASP.NET 버전 1.x 응용 프로그램과 함께 사용할 수 있습니다.

모든 배포 응용 프로그램 개발 팀에 알림을 보내고 자동으로 처리 되지 않은 예외를 로깅 하기 위한 메커니즘이 있어야 합니다. 이 있는지 여부에 상태 모니터링 또는 ELMAH를 사용 하 여 수행 됩니다 하는 것은 보조 합니다. 즉, 중요 하지 훨씬 사용할지 상태 모니터링 또는 ELMAH; 두 시스템을 평가 하 고 요구에 가장 잘 맞는 하나를 선택 합니다. 근본적으로 중요 한 점은 프로덕션 환경에서 처리 되지 않은 예외를 기록 하는 위치에 몇 가지 메커니즘을 추가 하는 수입니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ELMAH-오류 로깅 모듈 및 처리기](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH 프로젝트 페이지](https://code.google.com/p/elmah/) (원본 코드, 샘플, wiki)
- [ELMAH에는 웹 응용 프로그램 처리 되지 않은 예외를 Catch 연결](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx) (비디오)
- [보안 오류 로그 페이지](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [플러그형 ASP.NET 구성 요소를 만드는 HTTP 모듈 및 처리기를 사용 하 여](https://msdn.microsoft.com/library/aa479332.aspx)
- [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [이전](logging-error-details-with-asp-net-health-monitoring-cs.md)
> [다음](precompiling-your-website-cs.md)
