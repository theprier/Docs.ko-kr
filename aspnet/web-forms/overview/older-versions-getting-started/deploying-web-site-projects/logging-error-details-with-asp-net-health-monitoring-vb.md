---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
title: "ASP.NET 상태 모니터링 (VB)를 사용 하 여 오류 세부 정보를 로깅 | Microsoft Docs"
author: rick-anderson
description: "Microsoft의 상태 모니터링 시스템에는 처리 되지 않은 예외를 포함 하 여 다양 한 웹 이벤트를 기록 하는 편리 하 고 사용자 지정할 수 있는 방법을 제공 합니다. 이 자습서에서는 thr 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: 09a6c74e-936a-4c04-8547-5bb313a4e4a3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
msc.type: authoredcontent
ms.openlocfilehash: 83f7504e3aeb02ed222712e7e51f612f7ffd5744
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="logging-error-details-with-aspnet-health-monitoring-vb"></a>ASP.NET 상태 모니터링 (VB)를 사용 하 여 오류 세부 정보를 로깅
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_vb.pdf)

> Microsoft의 상태 모니터링 시스템에는 처리 되지 않은 예외를 포함 하 여 다양 한 웹 이벤트를 기록 하는 편리 하 고 사용자 지정할 수 있는 방법을 제공 합니다. 이 자습서에서는 처리 되지 않은 예외는 데이터베이스에 로그온 하 고 알림을 전자 메일 메시지를 통해 개발자가 상태 시스템 모니터링을 설정 하 여 설명 합니다.


## <a name="introduction"></a>소개

로깅은 배포 된 응용 프로그램의 상태를 모니터링 하 고 발생할 수 있는 모든 문제를 진단 하는 데 유용한 도구입니다. 특히 해결 될 수 있도록 배포 된 응용 프로그램에서 발생 하는 오류를 기록 하는 것이 유용 합니다. `Error` ; ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생할 때마다 이벤트는 [이전 자습서](processing-unhandled-exceptions-vb.md) 오류 개발자 팀에 알리고는 에대한이벤트처리기를만들어해당세부정보를기록하는방법을배웠습니다`Error` 이벤트입니다. 그러나 만들기는 `Error` ASP가이 작업을 수행할 수는 오류 세부 정보를 기록 하는 개발자에 게 알리는 이벤트 처리기는, 필요 하지 않습니다. NET의 *상태 시스템 모니터링*합니다.

상태 시스템 모니터링 ASP.NET 2.0에서 도입 되었으며 응용 프로그램이 나 요청의 수명 동안 발생 하는 이벤트를 기록 하 여 배포 된 ASP.NET 응용 프로그램의 상태를 모니터링 하도록 설계 되었습니다. 상태 모니터링 시스템에 의해 기록 된 이벤트 라고 *상태 모니터링 이벤트* 또는 *웹 이벤트*를 포함 합니다.

- 응용 프로그램을 시작 하거나 중지 하는 등의 응용 프로그램 수명 이벤트
- 보안 이벤트를 포함 하 여 실패 한 로그인 시도 실패 한 URL 권한 부여 요청
- 처리 되지 않은 예외, 예외, 요청 유효성 검사 예외 및 기타 유형 오류 중 컴파일 오류를 구문 분석 뷰 상태를 응용 프로그램 오류를 포함 합니다.

원하는 수의 기록 될 수 있습니다 때 모니터링 이벤트는 상태 지정 *소스 로그*합니다. 상태 시스템 모니터링 다른 규칙 으로부터 전자 메일 메시지를 통해 또는 Windows 이벤트 로그에 Microsoft SQL Server 데이터베이스를 웹 이벤트를 기록 하는 로그 원본과 함께 제공 됩니다. 고유한 로그 소스를 만들 수 있습니다.

을 사용 하는 로그 소스와 함께 상태 모니터링 시스템 로그, 이벤트에 정의 된 `Web.config`합니다. 구성 태그의 몇 줄만 데이터베이스에 모든 처리 되지 않은 예외를 기록 하 고이를 알리는 전자 메일을 통해 예외의 모니터링 상태를 사용할 수 있습니다.

## <a name="exploring-the-health-monitoring-systems-configuration"></a>상태 시스템의 구성을 모니터링 탐색

상태 시스템의 동작 모니터링에 있는 해당 구성 정보에 의해 정의 됩니다는 [ `<healthMonitoring>` 요소](https://msdn.microsoft.com/library/2fwh2ss9.aspx) 에서 `Web.config`합니다. 이 구성 섹션의 정보는 다음 세 가지 중요 한 부분 무엇 보다도 정의합니다.

1. 상태 모니터링 이벤트를 기록해 야, 발생 하는 경우
2. 로그 원본 및
3. 각 상태 모니터링 (1)에 정의 된 이벤트 로그 소스에 매핑하는 방법을 (2)에서 정의 합니다.

이 정보는 세 명의 하위 구성 요소를 통해 지정 되어: [ `<eventMappings>` ](https://msdn.microsoft.com/library/yc5yk01w.aspx), [ `<providers>` ](https://msdn.microsoft.com/library/zaa41kz1.aspx), 및 [ `<rules>` ](https://msdn.microsoft.com/library/fe5wyxa0.aspx)각각.

기본 상태 시스템 구성 정보를 모니터링에서 확인할 수 있습니다는 `Web.config` 파일 `%WINDIR%\Microsoft.NET\Framework\version\CONFIG` 폴더입니다. 이 기본 구성 정보를 간단 하 게 나타내기에 대 한 제거 일부 태그와 함께 아래 나와 있습니다.

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample1.xml)]

관심 있는 모니터링 이벤트에 정의 된 상태는 `<eventMappings>` 상태 모니터링 이벤트의 클래스에 사용자에 게 친숙 한 이름을 제공 하는 요소입니다. 위의 태그에는 `<eventMappings>` 요소 사용자에 게 친숙 한 이름이 "모두" 오류 "상태 형식의 이벤트를 모니터링 할당 `WebBaseErrorEvent` 와 이름" 실패 "상태 모니터링 이벤트 유형의 `WebFailureAuditEvent`합니다.

`<providers>` 요소 정의 로그 소스, 사용자에 게 친숙 한 이름을 부여 및 로그 소스 관련 구성 정보를 지정 합니다. 첫 번째 `<add>` 요소 정의 사용 하 여 이벤트를 모니터링 하는 지정된 된 상태를 기록 하는 "EventLogProvider" 공급자는 `EventLogWebEventProvider` 클래스입니다. `EventLogWebEventProvider` 클래스는 이벤트를 Windows 이벤트 로그에 기록 합니다. 두 번째 `<add>` 요소를 통해 Microsoft SQL Server 데이터베이스에 이벤트를 기록 하는 "SqlWebEventProvider" 공급자 정의 `SqlWebEventProvider` 클래스입니다. "SqlWebEventProvider" 구성 데이터베이스의 연결 문자열 지정 (`connectionStringName`) 다른 구성 옵션 중 하나입니다.

`<rules>` 요소에 지정 된 이벤트를 매핑합니다는 `<eventMappings>` 소스에 로그인 하는 요소는 `<providers>` 요소입니다. 기본적으로 ASP.NET 웹 응용 프로그램 처리 되지 않은 모든 예외를 기록 하 고 감사 Windows 이벤트 로그에 실패 합니다.

## <a name="logging-events-to-a-database"></a>데이터베이스에 이벤트를 기록

상태 모니터링 시스템의 기본 구성을 사용자 지정할 수 있습니다를 웹 응용 프로그램-웹 응용 프로그램으로 추가 하 여 한 `<healthMonitoring>` 섹션에는 응용 프로그램의 `Web.config` 파일입니다. 추가 요소를 포함할 수 있습니다는 `<eventMappings>`, `<providers>`, 및 `<rules>` 사용 하 여 섹션에서 `<add>` 요소입니다. 기본 구성 사용 하 여에서 설정을 제거 하려면는 `<remove>` 요소 또는 사용 하 여 `<clear />` 이러한 섹션 중 하나에서 모든 기본값을 제거 하려면. 처리 되지 않은 모든 예외를 사용 하 여 Microsoft SQL Server 데이터베이스에 기록 하는 책 검토 웹 응용 프로그램 구성에서 `SqlWebEventProvider` 클래스입니다.

`SqlWebEventProvider` 클래스 상태 모니터링 시스템의 일부 이며 지정 된 SQL Server 데이터베이스에 이벤트를 모니터링 상태를 기록 합니다. `SqlWebEventProvider` 클래스에서는 지정된 된 데이터베이스에 저장된 프로시저 이름이 포함 되도록 `aspnet_WebEvent_LogEvent`합니다. 이 저장된 프로시저는 이벤트의 세부 정보를 전달 되 고 이벤트 세부 정보를 저장 하면 업무를 맡았다고 합니다. 이 저장 만들 필요가 없습니다 다행 스럽게도 프로시저 및 테이블 이벤트 세부 정보를 저장 합니다. 이러한 개체를 사용 하 여 데이터베이스를 추가할 수 있습니다는 `aspnet_regsql.exe` 도구입니다.

> [!NOTE]
> `aspnet_regsql.exe` 도구에서 다시 설명한는 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-vb.md) 때 ASP에 대 한 지원이 추가 되었습니다. NET의 응용 프로그램 서비스입니다. 따라서 책 검토 웹 사이트의 데이터베이스에 이미는 `aspnet_WebEvent_LogEvent` 저장 프로시저 라는 테이블에 대 한 이벤트 정보를 저장 하는 `aspnet_WebEvent_Events`합니다.


필요한 저장된 프로시저와 테이블을 데이터베이스에 추가 했으면 이제 남은 것 상태 모니터링 되지 않은 예외가 데이터베이스에 기록 하도록 지시 하 합니다. 웹 사이트의에 다음 태그를 추가 하 여이 작업을 수행할 `Web.config` 파일:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample2.xml)]

상태 모니터링 사용 하 여 위에 구성 태그 `<clear />` 초기화는 미리 정의 된 상태에서 구성 정보를 모니터링 하는 요소는 `<eventMappings>`, `<providers>`, 및 `<rules>` 섹션. 그런 다음 이러한 각 섹션에 단일 항목을 추가합니다.

- `<eventMappings>` 요소 정의 단일 상태 라는 "모두" 하는 오류는 처리 되지 않은 예외가 발생할 때마다 발생 하는 관련 이벤트를 모니터링 합니다.
- `<providers>` 요소는 단일 로그 원본을 사용 하 여 "SqlWebEventProvider" 라는 정의 `SqlWebEventProvider` 클래스입니다. `connectionStringName` "ReviewsConnectionString" 우리의 연결의 이름에 설정 된 특성이에 정의 된 문자열의 `<connectionStrings>` 섹션.
- 마지막으로 &lt;규칙&gt; "모든 오류가" 이벤트 다소 하는 경우이 기록 된다는 것 "SqlWebEventProvider" 공급자를 사용 하 여 요소를 나타냅니다.

이 구성 정보 상태 모니터링 책 검토 데이터베이스에 모든 처리 되지 않은 예외를 기록 하는 시스템에 지시 합니다.

> [!NOTE]
> `WebBaseErrorEvent` 이벤트는 서버 오류만 발생; 찾을 수 없는 ASP.NET 리소스에 대 한 요청 등의 HTTP 오류에는 발생 하지 않습니다. 동작은이 점에서 차이가 `HttpApplication` 클래스의 `Error` 서버와 HTTP 오류에 대 한 발생 하는 이벤트입니다.


모니터링 작업의 시스템 상태를 보려면 웹 사이트를 방문 하 고 방문 하 여 런타임 오류를 발생 `Genre.aspx?ID=foo`합니다. 예외 세부 정보 노란색 화면의 사망 (로컬로 방문) 하는 경우 또는 사용자 지정 오류 페이지 (프로덕션 환경에서 사이트를 방문) 하는 경우 적절 한 오류 페이지-나타납니다. 내부적으로, 상태 모니터링 시스템 데이터베이스에 오류 정보를 기록 합니다. 하나의 레코드 있어야는 `aspnet_WebEvent_Events` 테이블 (참조 **그림 1**);이 레코드는 발생 한 런타임 오류에 대 한 정보를 포함 합니다.

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image1.png)

**그림 1**: 기록 된 오류 세부 정보는 `aspnet_WebEvent_Events` 테이블  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-asp-net-health-monitoring-vb/_static/image3.png))

### <a name="displaying-the-error-log-in-a-web-page"></a>웹 페이지에 오류 로그 표시

웹 사이트의 현재 구성을 사용 하 여 상태 모니터링 시스템 데이터베이스에 모든 처리 되지 않은 예외를 기록 합니다. 그러나 상태 모니터링 웹 페이지를 오류 로그를 확인 하는 어떠한 메커니즘도 제공 하지 않습니다. 그러나 데이터베이스에서이 정보를 표시 하는 ASP.NET 페이지를 작성할 수 있습니다. (일시적으로 볼 수 있겠지만, 하도록 선택할 수 있습니다 전자 메일 메시지에 전송 오류 정보를 포함 합니다.)

이러한 페이지를 만드는 경우 오류 세부 정보를 볼 권한이 있는 사용자만을 허용 하는 단계를 수행 해야 합니다. 사이트가 이미에서 하는 경우 사용자 계정 URL 권한 부여 규칙을 사용 하 여 특정 사용자 또는 역할에 대 한 페이지에 대 한 액세스를 제한 합니다. 권한을 부여 하거나 웹 페이지를 기반으로 로그인된 한 사용자 액세스를 제한 하는 방법에 대 한 자세한 내용은 참조 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.

> [!NOTE]
> 이후의 자습서 ELMAH 라는 대체 오류 로깅 및 알림 시스템을 탐색 합니다. ELMAH는 RSS 피드로 웹 페이지에서 오류 로그를 볼 수 있는 기본 제공 메커니즘을 포함 합니다.


## <a name="logging-events-to-email"></a>전자 메일에 이벤트 로깅

상태 시스템 모니터링 이벤트를 전자 메일 메시지에 "기록" 하는 로그 소스 공급자가 포함 되어 있습니다. 로그 원본 데이터베이스 전자 메일 메시지 본문에 기록 되는 동일한 정보를 포함 합니다. 특정 상태 모니터링 이벤트가 발생할 때 개발자에 알리기 위해이 로그 소스를 사용할 수 있습니다.

웹 사이트의 구성에서는 예외가 발생할 때마다 전자 메일을 받을 수 있도록 발생 책 검토를 업데이트 해 보겠습니다. 이렇게 하려면 세 가지 작업을 수행 해야 합니다.

1. 전자 메일을 보내는 ASP.NET 웹 응용 프로그램을 구성 합니다. 전자 메일 메시지를 통해 전송 되는 방법을 지정 하 여 이렇게는 `<system.net>` 구성 요소입니다. 전자 메일을 보내는 방법에 대 한 자세한 내용은 ASP.NET 응용 프로그램에서 메시지를 참조 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx) 및 [System.Net.Mail FAQ](http://systemnetmail.com/)합니다.
2. 등록에서 전자 메일 로그 소스 공급자는 `<providers>` 요소 및
3. 항목을 추가 `<rules>` "모든 오류가" 이벤트 로그 소스 공급자 (2) 단계에서 추가한에 매핑하는 요소입니다.

두 개의 전자 메일 로그 소스 공급자 클래스를 포함 하는 상태 시스템 모니터링: `SimpleMailWebEventProvider` 및 `TemplatedMailWebEventProvider`합니다. [ `SimpleMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx) 자세히 설명 하 고 전자 메일 본문의 사용자 지정이 거의 제공 하는 이벤트를 포함 하는 일반 텍스트 전자 메일 메시지를 보냅니다. 와 [ `TemplatedMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) 렌더링 된 피드백 전자 메일 메시지의 본문으로 사용 되는 ASP.NET 페이지를 지정 합니다. [ `TemplatedMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) 내용과 전자 메일 메시지의 서식을 통해 보다 광범위 제어를 제공 하지만 전자 메일 메시지의 본문을 생성 하는 ASP.NET 페이지를 만들어야 할 때 좀 더 선행 작업이 필요 하지 않습니다. 이 자습서를 사용 하 여 중점적는 `SimpleMailWebEventProvider` 클래스입니다.

상태 시스템의 모니터링 업데이트 `<providers>` 요소에는 `Web.config` 파일에 대 한 로그 소스를 포함 하는 `SimpleMailWebEventProvider` 클래스:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample3.xml)]

위의 태그를 사용 하 여는 `SimpleMailWebEventProvider` 로그 소스 공급자와 클래스 "EmailWebEventProvider" 친숙 한 이름을 할당 합니다. 또한는 `<add>` 특성 전자 메일 메시지의 주소와 같은 추가 구성 옵션을 포함 합니다.

전자 메일 로그 소스를 정의 했으므로 이제 남은 것에 대 한 상태 모니터링 "log" 처리 되지 않은 예외에이 원본을 사용 하도록 시스템 명령입니다. 새 규칙을 추가 하 여 이렇게는 `<rules>` 섹션:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample4.xml)]

`<rules>` 섹션에는 이제 두 개의 규칙이 포함 됩니다. "모든 오류에 전자 메일", 명명 된 첫 번째 "EmailWebEventProvider" 로그 소스를 모든 처리 되지 않은 예외를 보냅니다. 이 규칙에 지정 된 웹 사이트에서 오류에 대 한 세부 정보를 보내는 효과가 주소입니다. 모든 오류에 "데이터베이스" 규칙은 사이트의 데이터베이스에 오류 세부 정보를 기록합니다. 따라서 세부 정보는 사이트에서 처리 되지 않은 예외가 발생할 때마다 모두 되 데이터베이스에 로깅되 고 지정 된 전자 메일 주소로 전송 합니다.

**그림 2** 에 의해 생성 된 전자 메일을 보여 줍니다는 `SimpleMailWebEventProvider` 을 방문할 때 클래스 `Genre.aspx?ID=foo`합니다.

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image4.png)

**그림 2**: 오류 세부 정보는 전자 메일 메시지에 보내집니다.  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-asp-net-health-monitoring-vb/_static/image6.png))

## <a name="summary"></a>요약

ASP.NET 상태 모니터링 시스템은 관리자가 배포 된 웹 응용 프로그램의 상태를 모니터링할 수 있도록 설계 되었습니다. 상태 모니터링 이벤트 응용 프로그램 중지 시 때 사용자 성공적으로 사이트에 로그온을 같은 특정 작업 펼침 또는 처리 되지 않은 예외가 발생할 때 발생 합니다. 이러한 이벤트는 임의 개수의 원본 로그에 기록할 수 있습니다. 이 자습서에는 데이터베이스에 및 전자 메일 메시지를 통해 처리 되지 않은 예외의 세부 정보를 기록 하는 방법을 배웠습니다.

이 자습서에 처리 되지 않은 예외를 기록 하지만 상태 모니터링은 배포 된 ASP.NET 응용 프로그램의 전반적인 상태를 측정 하도록 설계 된 및 다양 한 상태 모니터링 이벤트만 포함 되어 염두에 둬야 및 소스를 하지 로그 모니터링 상태를 사용 하 여에 집중 여기를 탐색 합니다. 더구나 고유한 상태 모니터링 이벤트 및 로그 소스를 만들 수 필요한 발생 합니다. 좋은 파악 하는 상태 모니터링에 대 한 더 자세히 알고 싶은 경우 [Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)의 [상태 모니터링 FAQ](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)합니다. 그런 다음, 참조 [방법: ASP.NET 2.0에서 사용 하 여 상태 모니터링](https://msdn.microsoft.com/library/ms998306.aspx)합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 상태 모니터링 개요](https://msdn.microsoft.com/library/bb398933.aspx)
- [구성 및 상태 모니터링 시스템의 ASP.NET 사용자 지정](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [FAQ-상태 모니터링 ASP.NET 2.0에서](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [방법: 상태 모니터링 알림을 위한 전자 메일 보내기](https://msdn.microsoft.com/library/ms227553.aspx)
- [방법: ASP.NET에서 상태 모니터링 사용](https://msdn.microsoft.com/library/ms998306.aspx)
- [ASP.NET에서 모니터링 하는 상태](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

>[!div class="step-by-step"]
[이전](processing-unhandled-exceptions-vb.md)
[다음](logging-error-details-with-elmah-vb.md)
