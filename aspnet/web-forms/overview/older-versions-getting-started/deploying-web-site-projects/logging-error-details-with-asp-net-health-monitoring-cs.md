---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
title: ASP.NET 상태 모니터링 (C#)를 사용 하 여 오류 세부 정보 로깅 | Microsoft Docs
author: rick-anderson
description: Microsoft의 상태 모니터링 시스템에는 처리 되지 않은 예외를 비롯 한 다양 한 웹 이벤트를 기록 하는 쉽고 사용자 지정 가능한 방법을 제공 합니다. 이 자습서에서는 사용자를 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: b1abb452-642a-4ff3-8504-37b85590ff79
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
msc.type: authoredcontent
ms.openlocfilehash: 73b78b99f68dc32f37bcd16865091deebdb1399a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363483"
---
<a name="logging-error-details-with-aspnet-health-monitoring-c"></a>ASP.NET 상태 모니터링 (C#)를 사용 하 여 오류 세부 정보 로깅
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_cs.pdf)

> Microsoft의 상태 모니터링 시스템에는 처리 되지 않은 예외를 비롯 한 다양 한 웹 이벤트를 기록 하는 쉽고 사용자 지정 가능한 방법을 제공 합니다. 이 자습서는 데이터베이스에 처리 되지 않은 예외를 기록 하 고 전자 메일 메시지를 통해 개발자에 게 알립니다 상태 시스템 모니터링 설정 안내 합니다.


## <a name="introduction"></a>소개

로깅은 배포 된 응용 프로그램의 상태를 모니터링 하 고 발생할 수 있는 모든 문제를 진단 하는 데 유용한 도구입니다. 특히 해결 될 수 있도록 배포 된 응용 프로그램에서 발생 하는 오류를 기록 하는 것이 반드시 합니다. 합니다 `Error` ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생할 때마다 이벤트가 발생 합니다 [이전 자습서](processing-unhandled-exceptions-cs.md) 오류의 개발자에 게 알리고 합니다 에대한이벤트처리기를만들어해당세부정보를기록하는방법에설명했습니다`Error` 이벤트입니다. 그러나 만들기는 `Error` ASP가이 작업을 수행할 수 있습니다 하는 대로 오류 세부 정보를 기록 하는 개발자에 게 알림 이벤트 처리기는 필요 하지 있습니다. NET의 *상태 모니터링 시스템*입니다.

상태 시스템 모니터링 ASP.NET 2.0에서 도입 되었으며 응용 프로그램 또는 요청의 수명 동안 발생 하는 이벤트를 기록 하 여 배포 된 ASP.NET 응용 프로그램의 상태를 모니터링 하도록 설계 되었습니다. 상태 모니터링 시스템에 의해 기록 된 이벤트 라고 *상태 모니터링 이벤트* 또는 *이벤트 웹*를 포함 합니다.

- 응용 프로그램이 시작 되거나 중지 될 때와 같은 응용 프로그램 수명 이벤트
- 보안 이벤트를 포함 하 여 실패 한 로그인 시도 및 실패 한 URL 권한 부여 요청
- 응용 프로그램 오류를 포함 하 여 처리 되지 않은 예외를 뷰 상태 예외, 요청 유효성 검사 예외 및 다른 유형의 오류 간에 컴파일 오류를 구문 분석

임의 개수의에 로깅될 수 있습니다 때 모니터링 이벤트가 발생 하는 상태 지정 *원본 로그*합니다. 상태 시스템 모니터링 Windows 이벤트 로그에 또는 다른 전자 메일 메시지를 통해 Microsoft SQL Server 데이터베이스에 웹 이벤트를 기록 하는 로그 원본과 함께 제공 됩니다. 또한 사용자 고유의 로그 소스를 만들 수 있습니다.

사용 로그 원본을 함께 상태 모니터링 시스템 로그, 이벤트에 정의 된 `Web.config`합니다. 몇 줄의 구성 태그를 사용 하 여 데이터베이스에 모든 처리 되지 않은 예외를 기록 하 고를 알리는 전자 메일을 통해 예외를 모니터링 하는 상태를 사용할 수 있습니다.

## <a name="exploring-the-health-monitoring-systems-configuration"></a>모니터링 시스템의 구성 상태를 탐색 합니다.

에 있는 해당 구성 정보를 정의한 상태 시스템의 동작을 모니터링 합니다 [ `<healthMonitoring>` 요소](https://msdn.microsoft.com/library/2fwh2ss9.aspx) 에서 `Web.config`합니다. 이 구성 섹션에서는 다음 세 가지 중요 한 정보가 무엇 보다도 정의합니다.

1. 상태 모니터링 이벤트를 발생을 기록해 야 하는 경우
2. 로그 원본 및
3. (1)에 정의 된 이벤트를 모니터링 하는 각 상태 로그 원본에 매핑되는 방식과 (2)에서 정의 합니다.

세 명의 하위 구성 요소를 통해이 정보를 지정 합니다. [ `<eventMappings>` ](https://msdn.microsoft.com/library/yc5yk01w.aspx), [ `<providers>` ](https://msdn.microsoft.com/library/zaa41kz1.aspx), 및 [ `<rules>` ](https://msdn.microsoft.com/library/fe5wyxa0.aspx)각각.

기본 상태 모니터링 시스템 구성 정보에서 확인할 수 있습니다 합니다 `Web.config` 파일 `%WINDIR%\Microsoft.NET\Framework\version\CONFIG` 폴더입니다. 이 기본 구성 정보를 간단히 하기 위해 제거 일부 태그를 사용 하 여 아래와 같습니다.

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample1.xml)]

관심 있는 모니터링 이벤트에 정의 된 상태는 `<eventMappings>` 상태 모니터링 이벤트의 클래스에 친숙 한 이름을 제공 하는 요소입니다. 위의 태그에는 `<eventMappings>` 요소 이름을 할당 합니다 친숙 한 "모든 오류" 유형의 이벤트를 모니터링 상태 `WebBaseErrorEvent` 및 상태 모니터링 이벤트 형식의 "실패 감사" 이름 `WebFailureAuditEvent`합니다.

`<providers>` 요소 친숙 한 이름을 제공 하 고 모든 로그 원본 관련 구성 정보를 지정 하는 로그 원본을 정의 합니다. 첫 번째 `<add>` 요소에 지정된 된 상태 모니터링 사용 하 여 이벤트를 기록 하는 "EventLogProvider" 공급자에 정의 된 `EventLogWebEventProvider` 클래스입니다. `EventLogWebEventProvider` 클래스는 Windows 이벤트 로그에 이벤트를 기록 합니다. 두 번째 `<add>` 요소를 통해 Microsoft SQL Server 데이터베이스에 이벤트를 기록 하는 "SqlWebEventProvider" 공급자에 정의 된 `SqlWebEventProvider` 클래스입니다. "SqlWebEventProvider" 구성 데이터베이스의 연결 문자열 지정 (`connectionStringName`) 다른 구성 옵션 중 하나입니다.

`<rules>` 요소에 지정 된 이벤트를 매핑합니다 합니다 `<eventMappings>` 원본에 로그인 하는 요소는 `<providers>` 요소입니다. 기본적으로 ASP.NET 웹 응용 프로그램 처리 되지 않은 모든 예외를 기록 하 고 Windows 이벤트 로그에 오류를 감사 합니다.

## <a name="logging-events-to-a-database"></a>데이터베이스에 이벤트를 기록

상태 모니터링 시스템의 기본 구성을 사용자 지정할 수 있습니다 웹 응용 프로그램에서 웹 응용 프로그램 단위로 추가 하 여는 `<healthMonitoring>` 응용 프로그램의 섹션 `Web.config` 파일입니다. 추가 요소를 포함할 수 있습니다는 `<eventMappings>`, `<providers>`, 및 `<rules>` 사용 하 여 섹션을 `<add>` 요소입니다. 기본 구성 사용 하 여에서 설정을 제거 하는 `<remove>` 요소 또는 사용 하 여 `<clear />` 이러한 섹션 중 하나에서 모든 기본값을 제거 하려면. 구성도 서 리뷰 웹 응용 프로그램을 사용 하 여 Microsoft SQL Server 데이터베이스에 처리 되지 않은 모든 예외를 기록 합니다 `SqlWebEventProvider` 클래스입니다.

`SqlWebEventProvider` 클래스 상태 모니터링 시스템의 일부 이며 지정 된 SQL Server 데이터베이스에 이벤트를 모니터링 하 여 상태를 기록 합니다. 합니다 `SqlWebEventProvider` 클래스는 지정된 된 데이터베이스는 저장된 프로시저의 이름을 포함 `aspnet_WebEvent_LogEvent`합니다. 이 저장된 프로시저 이벤트의 세부 정보를 전달 하 고 이벤트 세부 정보를 저장 하는 임무를 담당 해야 합니다. 좋은 소식은 저장 만들 필요가 없습니다 이벤트 세부 정보를 저장할 테이블 및 프로시저입니다. 사용 하 여 데이터베이스에 이러한 개체를 추가할 수 있습니다는 `aspnet_regsql.exe` 도구입니다.

> [!NOTE]
> `aspnet_regsql.exe` 년대 도구에서 설명한 합니다 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md) ASP에 대 한 지원을 추가한 경우. NET의 응용 프로그램 서비스입니다. 결과적으로,도 서 리뷰 웹 사이트의 데이터베이스에 이미 합니다 `aspnet_WebEvent_LogEvent` 저장 프로시저 라는 테이블에 이벤트 정보를 저장 하는 `aspnet_WebEvent_Events`합니다.


필요한 저장된 프로시저 및 데이터베이스에 추가 된 테이블을 만든 후에 상태 모니터링을 데이터베이스에 모든 처리 되지 않은 예외를 기록 하도록 지시 합니다. 웹 사이트의 다음 태그를 추가 하 여이 작업을 수행할 `Web.config` 파일:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample2.xml)]

상태 모니터링 사용 하 여 위에 구성 태그 `<clear />` 미리 정의 된 상태에서 구성 정보를 모니터링을 초기화 하는 요소는 `<eventMappings>`를 `<providers>`, 및 `<rules>` 섹션입니다. 그런 다음 이러한 각 섹션에 단일 항목을 추가합니다.

- `<eventMappings>` 요소는 "모든 오류" 처리 되지 않은 예외가 발생할 때마다 발생 하는 명명 된 관심 있는 이벤트를 모니터링 하는 단일 상태를 정의 합니다.
- 합니다 `<providers>` 요소를 사용 하는 "SqlWebEventProvider" 라는 단일 로그 원본을 정의 합니다 `SqlWebEventProvider` 클래스입니다. `connectionStringName` "ReviewsConnectionString"은 연결의 이름에 특성을 설정한에 정의 된 문자열을 `<connectionStrings>` 섹션입니다.
- 마지막으로, 합니다 &lt;규칙&gt; 요소는 "모든 오류가" 이벤트 다소 하는 경우 해당 기록할지 "SqlWebEventProvider" 공급자를 사용 하 여 나타냅니다.

이 구성 정보 상태 모니터링 시스템도 서 리뷰 데이터베이스에 모든 처리 되지 않은 예외를 기록 하도록 지시 합니다.

> [!NOTE]
> `WebBaseErrorEvent` 만 이벤트는 서버 오류에 대 한; 찾을 수 없는 ASP.NET 리소스 요청과 같은 HTTP 오류는 발생 하지 않습니다. 이 동작에서 다릅니다 합니다 `HttpApplication` 클래스의 `Error` 서버와 HTTP 오류에 대 한 발생 하는 이벤트입니다.


모니터링 작업의 시스템 상태를 확인 하려면 웹 사이트를 방문 하 고 방문 하 여 런타임 오류를 발생 `Genre.aspx?ID=foo`합니다. 예외 세부 정보 노란색 화면의 쇠퇴 (로컬로 방문) 하는 경우 또는 사용자 지정 오류 페이지 (프로덕션 환경에서 사이트를 방문 하) 하는 경우 적절 한 오류 페이지를 표시 됩니다. 내부적으로 상태 모니터링 시스템 데이터베이스에 오류 정보를 기록 합니다. 하나의 레코드와만 있어야 합니다 `aspnet_WebEvent_Events` 테이블 (참조 **그림 1**);이 레코드에만 발생 한 런타임 오류에 대 한 정보를 포함 합니다.

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image1.png)

**그림 1**: 오류 세부 정보를 기록 합니다 `aspnet_WebEvent_Events` 테이블  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-asp-net-health-monitoring-cs/_static/image3.png))

### <a name="displaying-the-error-log-in-a-web-page"></a>웹 페이지에 오류 로그를 표시합니다.

웹 사이트의 현재 구성과 상태 모니터링 시스템 데이터베이스에 모든 처리 되지 않은 예외를 기록 합니다. 그러나 상태 모니터링 웹 페이지를 오류 로그를 보려면 메커니즘을 제공 하지 않습니다. 그러나 데이터베이스에서이 정보를 표시 하는 ASP.NET 페이지를 작성할 수 있습니다. (일시적으로 볼 수 있겠지만, 하도록 선택할 수 있습니다 전자 메일 메시지 전송 오류 세부 정보입니다.)

이러한 페이지를 만드는 경우 오류 세부 정보를 볼 권한이 있는 사용자만을 허용 하는 단계를 수행 해야 합니다. 사이트에는 이미 사용자 계정을 사용 하는 경우 특정 사용자 또는 역할에 대 한 페이지에 대 한 액세스를 제한 하려면 URL 권한 부여 규칙을 사용할 수 있습니다. 권한을 부여 또는 로그인된 사용자를 기반으로 하는 웹 페이지에 대 한 액세스를 제한 하는 방법에 대 한 자세한 내용은 참조 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.

> [!NOTE]
> 후속 자습서에서는 ELMAH 라는 대체 오류 로깅 및 알림 시스템을 살펴봅니다. ELMAH는 모두 웹 페이지에서 RSS 피드로 오류 로그를 볼 수 있는 기본 제공 메커니즘을 포함 합니다.


## <a name="logging-events-to-email"></a>전자 메일에 이벤트를 기록합니다.

로그 원본 공급자는 이벤트를 전자 메일 메시지에 "로그"를 포함 하는 상태 시스템 모니터링 합니다. 로그 원본 데이터베이스 전자 메일 메시지 본문에 기록 되는 동일한 정보가 포함 됩니다. 특정 상태 모니터링 이벤트가 발생할 때 개발자에 알리기 위해이 로그 소스를 사용할 수 있습니다.

웹 사이트의 구성에서는 예외가 발생할 때마다 전자 메일을 받을 수 있도록 발생도 서 리뷰를 업데이트 해 보겠습니다. 이렇게 하려면 세 가지 작업을 수행 해야 합니다.

1. 전자 메일을 보내는 ASP.NET 웹 응용 프로그램을 구성 합니다. 통해 전자 메일 메시지를 전송 하는 방법을 지정 하 여 이렇게는 `<system.net>` 구성 요소입니다. 전자 메일을 전송 하는 방법은 ASP.NET 응용 프로그램에서 메시지를 참조할 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx) 하며 [System.Net.Mail FAQ](http://systemnetmail.com/)합니다.
2. 전자 메일 로그 원본 공급자를 등록 합니다 `<providers>` 요소 및
3. 항목을 추가 합니다 `<rules>` "모든 오류가" 이벤트 로그 원본 공급자 (2) 단계에서 추가한 매핑되는 요소입니다.

두 개의 전자 메일 로그 소스 공급자 클래스를 포함 하는 상태 시스템 모니터링: `SimpleMailWebEventProvider` 고 `TemplatedMailWebEventProvider`입니다. 합니다 [ `SimpleMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx) 자세히 설명 하 고 전자 메일 본문의 약간의 사용자 지정을 제공 하는 이벤트를 포함 하는 일반 텍스트 전자 메일 메시지를 보냅니다. 사용 하 여 합니다 [ `TemplatedMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) 전자 메일 메시지의 본문으로 해당 렌더링 된 태그는 ASP.NET 페이지를 지정 합니다. 합니다 [ `TemplatedMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) 내용 및 전자 메일 메시지의 형식에 대해 많은 큰 제어를 제공 하지만 전자 메일 메시지의 본문을 생성 하는 ASP.NET 페이지를 생성 해야 하는 대로 좀 사전 작업이 필요 합니다. 이 자습서를 사용 하 여 중점을 `SimpleMailWebEventProvider` 클래스입니다.

상태 모니터링 시스템의 업데이트 `<providers>` 요소에는 `Web.config` 에 대 한 로그 소스를 포함 하 여 파일을 `SimpleMailWebEventProvider` 클래스:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample3.xml)]

위의 태그를 사용 하는 `SimpleMailWebEventProvider` 로그 소스 공급자 클래스 "EmailWebEventProvider" 친숙 한 이름을 할당 합니다. 또한는 `<add>` To 등 전자 메일 메시지의 주소에서 추가 구성 옵션을 포함 합니다.

정의 된 전자 메일 로그 원본을 사용 하 여는 상태 처리 되지 않은 예외를 "로그인"이이 원본을 사용 하려면 시스템을 모니터링 하도록 지시 합니다. 새 규칙을 추가 하 여 이렇게는 `<rules>` 섹션:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample4.xml)]

`<rules>` 섹션에는 이제 두 가지 규칙이 포함 됩니다. "모든 오류를 전자 메일" 라는 첫 번째 "EmailWebEventProvider" 로그 원본으로 처리 되지 않은 모든 예외를 보냅니다. 이 규칙에 지정 된 웹 사이트에서 오류에 대 한 세부 정보를 보내고 미치는 주소입니다. 모든 오류에 "데이터베이스" 규칙은 사이트 데이터베이스에 오류 세부 정보를 기록합니다. 결과적으로 해당 세부 정보는 사이트에서 처리 되지 않은 예외가 발생할 때마다 모두 데이터베이스에 기록 되며 지정 된 전자 메일 주소로 전송 합니다.

**그림 2** 에서 생성 된 전자 메일을 보여 줍니다 합니다 `SimpleMailWebEventProvider` 방문할 때 클래스 `Genre.aspx?ID=foo`합니다.

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image4.png)

**그림 2**: 오류 세부 정보는 전자 메일 메시지 전송  
([클릭 하 여 큰 이미지 보기](logging-error-details-with-asp-net-health-monitoring-cs/_static/image6.png))

## <a name="summary"></a>요약

ASP.NET 상태 모니터링 시스템은 관리자가 배포 된 웹 응용 프로그램의 상태를 모니터링할 수 있도록 설계 되었습니다. 상태 모니터링 이벤트는 응용 프로그램이 중지 되 면 경우 사용자 성공적으로 사이트에 로그온와 같은 특정 작업을 펼치려면 하거나 처리 되지 않은 예외가 발생 하면 발생 합니다. 이러한 이벤트는 임의 개수의 로그 원본에 기록할 수 있습니다. 이 자습서에서는 데이터베이스 및 전자 메일 메시지를 통해 처리 되지 않은 예외의 세부 정보를 기록 하는 방법을 보여줍니다.

이 자습서에서 처리 되지 않은 예외를 기록 염두에 상태 모니터링는 배포 된 ASP.NET 응용 프로그램의 전반적인 상태를 측정 하도록 설계 되었습니다 및 다양 한 상태 모니터링 이벤트를 포함 하지만 하지 원본 로그를 모니터링 하는 상태를 사용 하 여 초점 여기를 살펴봅니다. 게다가 고유한 상태 모니터링 이벤트 및 로그 원본을 만들 수 있습니다 고 발생 합니다. 첫 단계로 유용 읽어야 하는 상태 모니터링에 대 한 자세히 알아보는 데 관심이 있다면 [Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)의 [FAQ를 모니터링 하는 상태](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)합니다. 그런 다음, 참조 [방법: ASP.NET 2.0에서 사용 하 여 상태 모니터링](https://msdn.microsoft.com/library/ms998306.aspx)합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 상태 모니터링 개요](https://msdn.microsoft.com/library/bb398933.aspx)
- [구성 및 상태 모니터링 시스템의 ASP.NET 사용자 지정](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [FAQ-ASP.NET 2.0의에서 상태 모니터링](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [방법: 상태 알림을 모니터링에 대 한 전자 메일 보내기](https://msdn.microsoft.com/library/ms227553.aspx)
- [방법: ASP.NET에서 상태 모니터링 사용](https://msdn.microsoft.com/library/ms998306.aspx)
- [ASP.NET의 상태 모니터링](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [이전](processing-unhandled-exceptions-cs.md)
> [다음](logging-error-details-with-elmah-cs.md)
