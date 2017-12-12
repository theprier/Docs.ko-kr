---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
title: "처리 되지 않은 예외로 (VB) | Microsoft Docs"
author: rick-anderson
description: "프로덕션 환경에서 웹 응용 프로그램에서 런타임 오류가 발생할 때 고 것이 중요 개발자에 알리기 위해 la a에서 진단 수 있도록 오류를 기록 하려면..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: 051296f0-9519-4e78-835c-d868da13b0a0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: c1653cb3a8c684fd3d4fc2a039a947cfb5d42400
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="processing-unhandled-exceptions-vb"></a>처리 되지 않은 예외 (VB)를 처리 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_12_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial12_ErrorHandling_vb.pdf)

> 프로덕션 환경에서 웹 응용 프로그램에서 런타임 오류가 발생할 때에 개발자에 게 시간에 나중에 진단할 수 수 있도록 오류를 기록 하려면 중요 합니다. 이 자습서에서는 ASP.NET 런타임 오류를 처리 하 고 때마다 ASP.NET 런타임에 처리 되지 않은 예외가 거품을 실행 하는 사용자 지정 코드가 있는 한 가지 방법은 조사 하는 방법을 대 한 개요를 제공 합니다.


## <a name="introduction"></a>소개

발생 시키는 ASP.NET 런타임에 버블링 ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하는 경우는 `Error` 이벤트 적절 한 오류 페이지가 표시 됩니다. 세 가지 유형의 오류 페이지에 없는:는 런타임 오류 노란색 화면의 사망 (YSOD); YSOD; 예외 세부 정보 및 사용자 지정 오류 페이지입니다. 에 [이전 자습서](displaying-a-custom-error-page-vb.md) 로컬로 방문 하는 사용자에 대 한 예외 세부 정보 YSOD 및 원격 사용자에 대 한 사용자 지정 오류 페이지를 사용 하도록 응용 프로그램을 구성 했습니다.

사이트의 모양과 느낌을 일치 하는 사용자에 게 친숙 한 사용자 지정 오류 페이지를 사용 하 여 기본 런타임 오류 YSOD에 선호 않으며 사용자 지정 오류 페이지를 표시 하는 것은 솔루션을 처리 하는 포괄적인 오류의 한 부분일 뿐입니다. 프로덕션 환경에서 응용 프로그램에서 오류가 발생 하는 경우에 예외의 원인을 unearth 하 고 해결할 수 있도록 개발자가 오류 된다는 중요 합니다. 또한 오류의 세부 정보를 기록할 오류를 검사 하 고 나중에 시간에 진단 수 있도록 합니다.

이 자습서에서는 기록 될 수 있도록 처리 되지 않은 예외의 세부 정보에 액세스 하는 방법과 알림을 개발자 보여 줍니다. 이 중 하나를 수행 하는 두 개의 자습서 탐색 오류 로깅 하는 라이브러리, 구성, 약간만 자동 런타임 오류는 개발자에 게 알림 및 세부 정보를 기록 합니다.

> [!NOTE]
> 이 자습서에서는 검사 정보 일부 고유 또는 사용자 지정 방식으로 처리 되지 않은 예외를 처리 하는 경우 가장 유용 합니다. 만 해야 하는 경우 예외를 기록 하는 개발자에 게 알림, 오류 로깅 라이브러리를 사용 하는 이동 하는 방법입니다. 다음 두 자습서에서는 이러한 두 개의 라이브러리의 개요를 제공 합니다.


## <a name="executing-code-when-theerrorevent-is-raised"></a>때 코드 실행은`Error`이벤트 발생

이벤트 개체 발생 하는 흥미로운, 신호에 대 한 다른 개체에 대 한 응답에서 코드를 실행 하는 메커니즘을 제공 합니다. ASP.NET 개발자로 서 이벤트를 기준으로 생각 하는 데 익숙한 합니다. 해당 단추에 대 한 이벤트 처리기를 만들고 방문자가 특정 단추를 클릭할 때 일부 코드를 실행 하려는 경우 `Click` 이벤트 및 코드 대시보드에 배치한 것입니다. ASP.NET 런타임에서 발생 하는 [ `Error` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.error.aspx) 의 오류 세부 정보를 기록 하기 위한 코드는 이벤트 처리기에서 라인으로 설정 하에 따라 처리 되지 않은 예외가 발생할 때마다 합니다. 하지만 방법에 대 한 이벤트 처리기를 만들 수 있습니다는 `Error` 이벤트?

`Error` 이벤트는에서 대부분의 이벤트 중 하나는 [ `HttpApplication` 클래스](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.aspx) 요청 되는 동안 HTTP 파이프라인에서 특정 단계에서 발생 하는 합니다. 예를 들어는 `HttpApplication` 클래스의 [ `BeginRequest` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.beginrequest.aspx) 모든 요청;의 시작 부분에서 발생 해당 [ `AuthenticateRequest` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.authenticaterequest.aspx) 보안 모듈에서 요청자를 확인 하는 경우 발생 합니다. 이러한 `HttpApplication` 이벤트 페이지 개발자는 요청 수명에 다양 한 포인트에서 사용자 지정 논리를 실행 하는 방법을 제공 합니다.

에 대 한 이벤트 처리기는 `HttpApplication` 이벤트 라는 특수 한 파일에 배치할 수 있습니다 `Global.asax`합니다. 웹 사이트에서이 파일을 만들려면 이름을 가진 전역 응용 프로그램 클래스 템플릿을 사용 하 여 웹 사이트의 루트에 새 항목을 추가 `Global.asax`합니다.

[![](processing-unhandled-exceptions-vb/_static/image2.png)](processing-unhandled-exceptions-vb/_static/image1.png)

**그림 1**: 추가 `Global.asax` 웹 응용 프로그램  
 ([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-vb/_static/image3.png))

구조와 내용을 `Global.asax` Visual Studio에서 만든 파일은 응용 프로그램 프로젝트 WAP (웹) 또는 웹 사이트 프로젝트 (WSP) 사용 여부에 따라 약간씩 다 합니다. WAP와 `Global.asax` 두 개의 별도 파일로-구현 `Global.asax` 및 `Global.asax.vb`합니다. `Global.asax` 파일에 다음 아무 것도 포함 되어 있지만 `@Application` 참조 하는 지시문의 `.vb` 파일; 관심의 처리기에 정의 된 이벤트는 `Global.asax.vb` 파일입니다. WSPs에 대 한 단일 파일만 만들어지면 `Global.asax`, 이벤트 처리기에서 정의 됩니다는 `<script runat="server">` 블록입니다.

`Global.asax` 라는 이벤트 처리기를 포함 하는 Visual Studio의 전역 응용 프로그램 클래스 템플릿에서 WAP에서 만든 파일 `Application_BeginRequest`, `Application_AuthenticateRequest`, 및 `Application_Error`에 대 한 이벤트 처리기를가 하는 `HttpApplication` 이벤트 `BeginRequest`, `AuthenticateRequest`, 및 `Error`각각. 명명 된 이벤트 처리기도 있습니다. `Application_Start`, `Session_Start`, `Application_End`, 및 `Session_End`이며 웹 응용 프로그램이 시작 되 면 새 세션이 시작할 때 응용 프로그램이 종료 될 때 발생 하는 이벤트 처리기가 세션이 종료 되 고 각각. `Global.asax` WSP에서 Visual Studio에서 만든 파일을 포함 된 `Application_Error`, `Application_Start`, `Session_Start`, `Application_End`, 및 `Session_End` 이벤트 처리기입니다.

> [!NOTE]
> 복사 해야 하는 ASP.NET 응용 프로그램을 배포 하는 경우는 `Global.asax` 프로덕션 환경에는 파일입니다. `Global.asax.vb` 는 WAP에서 생성 된 파일을 프로젝트의 어셈블리에이 코드는 컴파일되므로 프로덕션에 복사할 필요가 없습니다.


Visual Studio의 전역 응용 프로그램 클래스 템플릿으로 만든 이벤트 처리기 하지는 않습니다. 에 대 한 이벤트 처리기를 추가할 수 있습니다 `HttpApplication` 이벤트 처리기의 이름을 지정 하 여 이벤트 `Application_EventName`합니다. 예를 들어 다음 코드를 추가할 수 있습니다는 `Global.asax` 에 대 한 이벤트 처리기를 만들려는 파일의 [ `AuthorizeRequest` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.authorizerequest.aspx):

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample1.vb)]

마찬가지로, 전역 응용 프로그램 클래스 템플릿으로 만든 필요 하지 않은 모든 이벤트 처리기를 제거할 수 있습니다. 이 자습서에서는 필요한에 대 한 이벤트 처리기는 `Error` 이벤트를 자유롭게 다른 이벤트 처리기를 제거 하 고 `Global.asax` 파일입니다.

> [!NOTE]
> *HTTP 모듈* 제공에 대 한 이벤트 처리기를 정의 하는 다른 방법은 `HttpApplication` 이벤트입니다. HTTP 모듈은 별도 클래스 라이브러리에 직접 웹 응용 프로그램 프로젝트 내에 배치 하거나 분리할 수 있는 클래스 파일을으로 생성 됩니다. HTTP 모듈을 만들기 위한 보다 유연 하 고 다시 사용할 수 있는 모델을 제공 클래스 라이브러리로 구분 될 수 있습니다, 때문에 `HttpApplication` 이벤트 처리기입니다. 반면는 `Global.asax` 파일은 특정 있는 웹 응용 프로그램에 HTTP 모듈 이때 웹 사이트에 HTTP 모듈을 추가 하기만 하면 됩니다 어셈블리를 삭제 하는 중 어셈블리로 컴파일할 수는 `Bin` 폴더 및 등록 된 모듈에 `Web.config`합니다. 이 자습서를 작성 하 고 HTTP 모듈을 사용 하 여 찾지 않습니다 되지만 다음과 같은 두 개의 자습서에 사용 되는 두 개의 오류 로깅 라이브러리 HTTP 모듈로 구현 됩니다. 자세한 배경을 알고 싶으면 HTTP 모듈의 이점에 대 한 참조 [를 사용 하 여 HTTP 모듈 및 처리기 플러그형 ASP.NET 구성 요소 만들기에](https://msdn.microsoft.com/en-us/library/aa479332.aspx)합니다.


## <a name="retrieving-information-about-the-unhandled-exception"></a>처리 되지 않은 예외에 대 한 정보 검색

Global.asax 파일을 했으므로 시점에서 `Application_Error` 이벤트 처리기입니다. 이 이벤트 처리기를 실행 하는 경우 오류 개발자에 게 알림와 세부 정보를 로그 필요 합니다. 이러한 작업을 수행 하려면 먼저 발생 한 예외의 세부 정보를 확인 해야 합니다. 서버 개체를 사용 하 여 [ `GetLastError` 메서드](https://msdn.microsoft.com/en-us/library/system.web.httpserverutility.getlasterror.aspx) 시킨 처리 되지 않은 예외의 세부 정보를 검색 하는 `Error` 이벤트를 발생 합니다.

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample2.vb)]

`GetLastError` 메서드 반환 형식의 개체 `Exception`가.NET Framework의 모든 예외에 대 한 기본 유형입니다. 그러나 위의 코드에서 I am 캐스팅 반환 되는 예외 개체 `GetLastError` 에 `HttpException` 개체입니다. 경우는 `Error` 내에서 throw 된 예외 래핑된 다음 ASP.NET 리소스를 처리 하는 동안 예외가 throw 되었기 때문에 이벤트가 발생 되는 `HttpException`합니다. 시킨 오류 이벤트를 사용 하 여 실제 예외를 가져오려는 `InnerException` 속성입니다. 경우는 `Error` HTTP 기반 예외로 인해 존재 하지 않는 페이지에 대 한 요청과 같이 이벤트가 발생 한 `HttpException` throw 되며, 내부 예외가 없는 합니다.

다음 코드에서는 `GetLastErrormessage` 를 발생 시킨 예외에 대 한 정보를 검색 하는 `Error` 이벤트를 저장 된 `HttpException` 이라는 변수에 `lastErrorWrapper`합니다. 다음 저장 유형, 메시지 및 스택 추적 원래 예외의 세 개의 문자열 변수를 확인 하는 경우에 `lastErrorWrapper` 는 실제 예외를 발생 시킨는 `Error` 이벤트 (의 경우 HTTP 기반 예외 포함) 또는 단순히 인지는 요청을 처리 하는 동안 throw 된 예외에 대 한 래퍼.

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample3.vb)]

이 시점에서 데이터베이스 테이블에는 예외 세부 정보를 기록 합니다는 코드를 작성 하는 데 필요한 모든 정보를 해야 합니다. 각 관심-유형, 메시지, 스택 추적 등에-다른 유용한 가지 요청된 된 페이지의 URL 및 현재 로그온된 한 사용자의 이름과 같은 정보를 함께 오류 세부 정보에 대 한 열이 있는 데이터베이스 테이블을 만들 수 있습니다. 에 `Application_Error` 이벤트 처리기 다음 데이터베이스에 연결 하는 테이블에 레코드를 삽입 합니다. 마찬가지로, 개발자는 전자 메일을 통해 오류를 경고 하는 코드를 추가할 수 있습니다.

다음 두 자습서에서 검사 하는 오류 로깅 라이브러리 이므로이 오류 로그 및 알림 사용자가 직접 구성할 필요가 없습니다 기본적으로 이러한 기능을 제공 합니다. 그러나를 설명 하기 위해는 `Error` 이벤트가 발생 하는 `Application_Error` 이벤트 처리기를 사용 하 여 오류 세부 정보를 기록 하 고 개발자에 게 알림, 오류가 발생 하면 개발자에 게 알려 주는 코드를 추가 하겠습니다를 수 있습니다.

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>처리 되지 않은 예외가 발생할 때 개발자에 게 알리는

프로덕션 환경에서 처리 되지 않은 예외가 발생 하는 경우에 개발 팀의 경고는 오류를 평가 하 고 수행 해야 하는 작업을 확인할 수 있도록 해야 합니다. 예를 들어 없을 경우 double로 해야 합니다는 데이터베이스에 대 한 연결에 오류가 확인 연결 문자열 하 고, 웹 호스팅 회사도 지원 티켓을 엽니다. 예외는 프로그래밍 오류 때문에 발생 한 경우 추가 코드 또는 유효성 검사 논리를 나중에 이러한 오류를 방지 하기 위해 추가 해야 합니다.

사용 되는.NET Framework 클래스는 [ `System.Net.Mail` 네임 스페이스](https://msdn.microsoft.com/en-us/library/system.net.mail.aspx) 쉽게 전자 메일을 보낼 수 있도록 합니다. [ `MailMessage` 클래스](https://msdn.microsoft.com/en-us/library/system.net.mail.mailmessage.aspx) 전자 메일 메시지를 나타내며 같은 속성을 보유 `To`, `From`, `Subject`, `Body`, 및 `Attachments`합니다. `SmtpClass` 보내는 데 사용 되는 `MailMessage` 개체는 지정 된 SMTP 서버를 사용 하 여, SMTP 서버 설정에서 프로그래밍 방식으로 또는 선언적으로 지정할 수 있습니다는 [ `<system.net>` 요소](https://msdn.microsoft.com/en-us/library/6484zdc1.aspx) 에 `Web.config file`합니다. 전자 메일을 보내는 방법에 대 한 자세한 내용은 ASP.NET 응용 프로그램에서 메시지 확인해 내 문서 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx), 및 [System.Net.Mail FAQ](http://systemnetmail.com/)합니다.

> [!NOTE]
> `<system.net>` 요소에서 사용 하는 SMTP 서버 설정이 포함 되어는 `SmtpClient` 전자 메일을 보낼 때 클래스입니다. 웹 호스팅 회사 가능성이 응용 프로그램에서 전자 메일을 보내는 데 사용할 수 있는 SMTP 서버를 있습니다. 웹 응용 프로그램에서 사용 해야 하는 SMTP 서버 설정에 대 한 정보는 웹 호스트의 지원 섹션을 참조 하십시오.


다음 코드를 추가 하는 `Application_Error` 개발자는 전자 메일을 보낼 오류가 발생할 때 이벤트 처리기.

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample4.vb)]

위의 코드는 매우 긴,에서는 대량의 개발자에 게 보내는 전자 메일에 표시 되는 HTML을 만듭니다. 참조 하 여 시작 하는 코드는 `HttpException` 에서 반환 되는 `GetLastError` 메서드 (`lastErrorWrapper`). 요청에 의해 발생 한 실제 예외를 통해 검색은 `lastErrorWrapper.InnerException` 변수에 할당 하 고 `lastError`합니다. 유형, 메시지 및 스택 추적 정보에서 검색 됩니다 `lastError` 이며 세 개의 문자열 변수에 저장 합니다.

다음으로 `MailMessage` 라는 개체 `mm` 만들어집니다. 전자 메일 본문에는 HTML 형식의 이며 요청된 된 페이지의 URL는 현재 로그온된 한 사용자 이름과 (유형, 메시지 및 스택 추적) 예외에 대 한 정보를 표시 합니다. 에 대 한 유용한 기능 중 하나는 `HttpException` 클래스는를 호출 하 여는 예외 세부 정보 노란색 화면의 사망 (YSOD)를 만드는 데 사용 되는 HTML을 생성할 수 있습니다는 [GetHtmlErrorMessage 메서드](https://msdn.microsoft.com/en-us/library/system.web.httpexception.gethtmlerrormessage.aspx)합니다. 이 메서드는 예외 세부 정보 YSOD 태그를 검색 하 고 첨부 파일로 메일에 추가 하려면 여기 사용 됩니다. 주의 사항: 발생 하는 예외는 `Error` 이벤트 (예: 존재 하지 않는 페이지에 대 한 요청) HTTP 기반 예외가 했습니다 하면 `GetHtmlErrorMessage` 메서드는 반환 `null`합니다.

마지막 단계는 보낼는 `MailMessage`합니다. 새 이렇게 `SmtpClient` 메서드와 호출 해당 `Send` 메서드.

> [!NOTE]
> 웹 응용 프로그램에서이 코드를 사용 하기 전에 값을 변경 해야는 `ToAddress` 및 `FromAddress` 상수 support@example.com 어떤 전자 메일 주소로 오류 알림 전자 메일에 보내야 및에서 발생 합니다. 에 SMTP 서버 설정을 지정 해야는 `<system.net>` 섹션 `Web.config`합니다. 사용할 SMTP 서버 설정을 확인 하 여 웹 호스트 공급자를 참조 하십시오.


이 코드 위치에서 오류가 있으면 언제 든 지 개발자는 전송 전자 메일 메시지를 오류를 요약 하 고는 YSOD 포함 됩니다. 이전 자습서에서 시연을 런타임 오류 Genre.aspx를 방문 하 고 잘못 된를 전달 하 여 `ID` like는 쿼리 문자열을 통해 값 `Genre.aspx?ID=foo`합니다. 사용 하 여 페이지 방문의 `Global.asax` -이전 자습서에서 개발 환경에서 계속 해 서에서는 프로덕션 환경에서 예외 세부 정보 노란색 화면의 사망, 볼 처럼으로 동일한 사용자 환경을 생성 하는 곳에 파일 사용자 지정 오류 페이지를 참조 하십시오. 개발자는이 기존 동작 외에도 전자 메일을 전송 됩니다.

**그림 2** 을 방문할 때 받은 전자 메일을 보여 줍니다 `Genre.aspx?ID=foo`합니다. 전자 메일 본문에서 예외 정보를 요약 하는 동안는 `YSOD.htm` 첨부 파일에는 예외 세부 정보 YSOD에 표시 되는 콘텐츠가 표시 됩니다 (참조 **그림 3**).

[![](processing-unhandled-exceptions-vb/_static/image5.png)](processing-unhandled-exceptions-vb/_static/image4.png)

**그림 2**: 개발자 처리 되지 않은 예외가 있을 때마다 전자 메일 알림이 전송 됩니다  
 ([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-vb/_static/image6.png))

[![](processing-unhandled-exceptions-vb/_static/image8.png)](processing-unhandled-exceptions-vb/_static/image7.png)

**그림 3**: 전자 메일 첨부 파일로 YSOD 예외 정보 포함  
 ([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-vb/_static/image9.png))

## <a name="what-about-using-the-custom-error-page"></a>사용자 지정 오류 페이지를 사용 하 여 작업은 어떤가요?

이 자습서에 사용 하는 방법을 보여 주었습니다 `Global.asax` 및 `Application_Error` 이벤트 처리기에 코드를 실행 하 여 처리 되지 않은 예외가 발생 합니다. 구체적으로, 개발자는 오류를 알리기 위해이 이벤트 처리기를 사용 했습니다. 도 데이터베이스에서 오류 세부 정보를 기록 하에 모두 확장할 수 있습니다. 존재는 `Application_Error` 이벤트 처리기는 최종 사용자 환경에 영향을 주지 않습니다. 오류 세부 정보 YSOD, 런타임 오류 YSOD 또는 사용자 지정 오류 페이지 수는 구성 된 오류 페이지도 표시 됩니다.

관심을 가질 수 있도록 자연스럽 여부는 `Global.asax` 파일 및 `Application_Error` 이벤트는 사용자 지정 오류 페이지를 사용 하는 경우에 필요 합니다. 오류가 발생할 사용자가 사용자 지정 오류 페이지를 표시 하는 경우 지금 이유 없습니다 우리는 코드를 삽입 개발자에 게 사용자 지정 오류 페이지의 코드 숨김 클래스에 오류 세부 정보를 로그인 합니다. 발생 시킨 예외의 세부 정보에 액세스할 수 없는 사용자 지정 오류 페이지의 코드 숨김 클래스를 확실히 코드를 추가할 수는 있지만 `Error` 이전 자습서에서 살펴본 기법을 사용할 때에 이벤트입니다. 호출 된 `GetLastError` 사용자 지정 오류 페이지에 있는 메서드의 반환 `Nothing`합니다.

이 동작에 대 한 이유는 리디렉션을 통해 사용자 지정 오류 페이지에 도달 하면 때문입니다. 처리 되지 않은 예외에 도달 하면 ASP.NET 런타임이 ASP.NET 엔진 발생 해당 `Error` 이벤트 (를 실행 하는 `Application_Error` 이벤트 처리기) 차례로 *리디렉션합니다* 는 를실행하여사용자지정오류페이지를사용자`Response.Redirect(customErrorPageUrl)`. `Response.Redirect` 메서드는 사용자 지정 오류 페이지 새 URL을 요청 하도록 브라우저에 지시 하는 HTTP 302 상태 코드로 클라이언트에 대 한 응답을 보냅니다. 브라우저에서 다음 자동으로 요청이 새 페이지. 알 수 있습니다는 사용자 지정 오류 페이지는 페이지에서 별도로 요청 되는 사용자 지정 오류 페이지 URL을 브라우저의 주소 표시줄 변경 되기 때문에 오류가 발생 (참조 **그림 4**).

[![](processing-unhandled-exceptions-vb/_static/image11.png)](processing-unhandled-exceptions-vb/_static/image10.png)

**그림 4**: 때 오류가 발생 브라우저 사용자 지정 오류 페이지 URL로 리디렉션됩니다.  
 ([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-vb/_static/image12.png))

한 순수 효과 처리 되지 않은 예외가 발생 하는 요청 HTTP 302 리디렉션을 때 끝나는 것입니다. 사용자 지정 오류 페이지에 대 한 후속 요청은 완전히 새로운 요청; ASP.NET이 시점 엔진 오류 정보는 삭제 하 고는 또한 사용자 지정 오류 페이지에 대 한 새 요청 이전 요청에서 처리 되지 않은 예외를 연결할 수 없습니다. 이 인해 `GetLastError` 반환 `null` 사용자 지정 오류 페이지에서 호출 합니다.

그러나, 사용자 지정 오류 페이지에 오류가 발생 한 동일한 요청 하는 동안 실행 수는 있습니다. [ `Server.Transfer(url)` ](https://msdn.microsoft.com/en-us/library/system.web.httpserverutility.transfer.aspx) 메서드 실행을 지정된 된 URL로 이동 하 고 동일한 요청 내에서 처리 합니다. 코드를 이동할 수는 `Application_Error` 이벤트 처리기에서 대체 되는 사용자 지정 오류 페이지의 코드 숨김 클래스를 `Global.asax` 를 다음 코드로:

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample5.vb)]

처리 되지 않은 예외가 발생할 때 이제는 `Application_Error` 이벤트 처리기는 HTTP 상태 코드에 따라 적절 한 사용자 지정 오류 페이지에 제어를 전달 합니다. 사용자 지정 오류 페이지에 통해 처리 되지 않은 예외 정보에 대 한 액세스 제어 전송 되어 `Server.GetLastError` 와 오류의 개발자에 게 알림 하 고 해당 정보를 기록할 수 있습니다. `Server.Transfer` 호출이 사용자 지정 오류 페이지에 사용자를 리디렉션할 ASP.NET 엔진을 중지 합니다. 대신, 사용자 지정 오류 페이지의 콘텐츠는 오류를 생성 하는 페이지에 대 한 응답으로 반환 됩니다.

## <a name="summary"></a>요약

ASP.NET 런타임에서 발생 하는 ASP.NET 웹 응용 프로그램에서 처리 되지 않은 예외가 발생 하는 경우는 `Error` 이벤트 구성 된 오류 페이지가 표시 됩니다. 오류를 개발자에 게 수 공지 세부 정보를 기록 하거나 오류 이벤트에 대 한 이벤트 처리기를 만들어이 다른 방식으로 처리 합니다. 두 가지 방법으로 이벤트 처리기를 만들 수 `HttpApplication` 와 같은 이벤트 `Error`:에서 `Global.asax` 파일 또는 HTTP 모듈에서 합니다. 이 자습서를 만드는 방법을 살펴보았습니다는 `Error` 의 이벤트 처리기는 `Global.asax` 파일을 전자 메일 메시지를 사용 하 여 개발자가 오류를 알립니다.

만들기는 `Error` 이벤트 처리기는 몇 가지 고유한 또는 사용자 지정 방식으로 처리 되지 않은 예외를 처리 해야 하는 경우에 유용 합니다. 그러나 직접 만들어 `Error` 있습니다 몇 분 내에 설치 될 수 있는 무료 및 사용 하기 쉬운 오류 로깅 라이브러리에 이미 존재 이벤트 처리기 예외가 로그 또는 개발자에 게는의 시간을 가장 효율적으로 사용 되지 않습니다. 다음 두 자습서에서는 이러한 두 라이브러리를 검사합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET HTTP 모듈 및 HTTP 처리기 개요](https://support.microsoft.com/kb/307985)
- [정상적으로 처리 되지 않은 예외를 처리 하는 처리 되지 않은 예외-에 응답](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication`클래스 및 ASP.NET 응용 프로그램 개체](http://www.eggheadcafe.com/articles/20030211.asp)
- [HTTP 처리기 및 asp.net에서 HTTP 모듈](http://www.15seconds.com/Issue/020417.htm)
- [ASP.NET에서 메일을 보내는 중](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [이해의 `Global.asax` 파일](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [HTTP 모듈 및 처리기를 사용 하 여 플러그형 ASP.NET 구성 요소 만들기](https://msdn.microsoft.com/en-us/library/aa479332.aspx)
- [ASP.NET 작업 `Global.asax` 파일](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [작업 `HttpApplication` 인스턴스](https://msdn.microsoft.com/en-us/library/a0xez8f2.aspx)

>[!div class="step-by-step"]
[이전](displaying-a-custom-error-page-vb.md)
[다음](logging-error-details-with-asp-net-health-monitoring-vb.md)
