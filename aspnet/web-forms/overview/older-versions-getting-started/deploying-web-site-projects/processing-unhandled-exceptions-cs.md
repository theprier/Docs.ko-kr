---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
title: 처리 하는 처리 되지 않은 예외 (C#) | Microsoft Docs
author: rick-anderson
description: 프로덕션 환경에서 웹 응용 프로그램에서 런타임 오류가 발생 하는 경우 것이 중요 개발자에 게 알림 하는 데는 la에서 진단 수 있도록 오류를 기록 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: 5bc1afd5-2484-4528-b158-ab218ba150e8
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 784290f1390668518ad88df9d38b60c0179a5923
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371858"
---
<a name="processing-unhandled-exceptions-c"></a>처리 되지 않은 예외 (C#)를 처리 합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs/samples)([다운로드 방법](/aspnet/core/tutorials/index#how-to-download-a-sample))

> 프로덕션 환경에서 웹 응용 프로그램에서 런타임 오류가 발생할 때 개발자에 게 알림를 시간에 나중에 진단 수 있도록 오류 로그에 중요 한 것입니다. 이 자습서에는 ASP.NET 런타임 오류를 처리 하 고 ASP.NET 런타임이까지 처리 되지 않은 예외가 거품을 받을 때마다 실행할 사용자 지정 코드가 있는 한 가지 방법은 조사 하는 방법을 간략하게를 설명 합니다.


## <a name="introduction"></a>소개

ASP.NET 런타임까지 전달 하는 ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하는 경우는 `Error` 이벤트 적절 한 오류 페이지를 표시 합니다. 오류 페이지의 세 가지 종류가 있습니다:는 런타임 오류 노란색 화면의 사망 (YSOD); 예외 세부 정보 YSOD; 및 사용자 지정 오류 페이지입니다. 에 [이전 자습서](displaying-a-custom-error-page-cs.md) 원격 사용자 및 예외 세부 정보 YSOD 로컬로 방문 하는 사용자에 대 한 사용자 지정 오류 페이지를 사용 하도록 응용 프로그램을 구성 했습니다.

사이트의 모양과 느낌을 일치 하는 친숙 한 사용자 지정 오류 페이지를 사용 하는 기본 런타임 오류 YSOD 하는 것이 좋습니다 이지만 사용자 지정 오류 페이지 표시는 포괄적인 오류 처리 솔루션의 한 부분입니다. 프로덕션 환경에서 응용 프로그램에서 오류가 발생 하는 경우 반드시는 개발자에 대 한 알림을 오류는 예외를 발생 시킨 알아보기 하 고 해결할 수 있도록 합니다. 또한 오류를 검사 하 고 나중에 시간에 진단 수 있도록 오류 세부 정보 기록 합니다.

이 자습서에는 기록 될 수 있도록 처리 되지 않은 예외의 세부 정보에 액세스 하는 방법 및 개발자 알림을 보여 줍니다. 다음이 두 자습서를 구성, 잠시 후 자동으로 런타임 오류는 개발자에 알리는 하 고 해당 세부 정보를 기록 하는 오류 로깅 라이브러리를 탐색 합니다.

> [!NOTE]
> 이 자습서에서는 검사 정보를 일부 고유 또는 사용자 지정 방식으로 처리 되지 않은 예외를 처리 해야 할 경우 가장 유용 합니다. 경우에 해야 하는 예외를 로그인 하 고 개발자에 게 알림, 오류 로깅 라이브러리를 사용 하 여는 이동 방법입니다. 이러한 라이브러리의 개요를 제공 하는 다음 두 자습서입니다.


## <a name="executing-code-when-theerrorevent-is-raised"></a>때 코드 실행을`Error`이벤트 발생

이벤트 개체 발생 하는 흥미로운, 신호 및 다른 개체에 대 한 응답에서 코드를 실행 하는 메커니즘을 제공 합니다. ASP.NET 개발자는 이벤트에 관하여 생각 하는 데 익숙한 합니다. 해당 단추에 대 한 이벤트 처리기를 만듭니다 방문자가 특정 단추를 클릭할 때 일부 코드를 실행 하려는 경우 `Click` 이벤트 있는 코드를 배치 합니다. ASP.NET 런타임에서 발생 하는 [ `Error` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) 이벤트 처리기에서 오류 세부 정보를 기록 하기 위한 코드 이동은 처리 되지 않은 예외가 발생할 때마다 따릅니다. 하지만 하는 방법에 대 한 이벤트 처리기를 만들 수 있습니다는 `Error` 이벤트?

합니다 `Error` 이벤트는에서 여러 이벤트 중 하나는 [ `HttpApplication` 클래스](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) 요청의 수명 동안 HTTP 파이프라인의 특정 단계에서 발생 하는 합니다. 예를 들어, 합니다 `HttpApplication` 클래스의 [ `BeginRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx) 모든 요청의; 시작할 때 발생 하는 해당 [ `AuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) 보안 모듈에서 요청자를 식별 하는 경우 발생 합니다. 이러한 `HttpApplication` 이벤트 페이지 개발자는 요청 수명에 다양 한 지점에 사용자 지정 논리를 실행 하는 방법을 제공 합니다.

에 대 한 이벤트 처리기를 `HttpApplication` 이라는 특수 파일에 이벤트를 배치할 수 있습니다 `Global.asax`합니다. 웹 사이트에서이 파일을 만들려면 이름의 전역 응용 프로그램 클래스 템플릿을 사용 하 여 웹 사이트의 루트에 새 항목을 추가 `Global.asax`합니다.

[![](processing-unhandled-exceptions-cs/_static/image2.png)](processing-unhandled-exceptions-cs/_static/image1.png)

**그림 1**: 추가 `Global.asax` 웹 응용 프로그램  
([클릭 하 여 큰 이미지 보기](processing-unhandled-exceptions-cs/_static/image3.png))

구조와 내용을 `Global.asax` Visual Studio에서 만든 파일에 웹 응용 프로그램 프로젝트 (WAP) 또는 웹 사이트 프로젝트 (WSP)를 사용 하는지에 따라 약간씩 다릅니다. WAP를 사용 하 여는 `Global.asax` 두 개의 별도 파일-으로 구현 됩니다 `Global.asax` 고 `Global.asax.cs`입니다. `Global.asax` 파일을 포함 하지 않는 되지만 `@Application` 참조 하는 지시문을 `.cs` 파일; 관심 처리기에 정의 된 이벤트는 `Global.asax.cs` 파일. 하며에 대 한 단일 파일만 만들어지면 `Global.asax`, 이벤트 처리기가 정의 하 고는 `<script runat="server">` 블록.

합니다 `Global.asax` 라는 이벤트 처리기를 포함 하는 Visual Studio의 전역 응용 프로그램 클래스 템플릿에서 WAP에서 만든 파일 `Application_BeginRequest`, `Application_AuthenticateRequest`, 및 `Application_Error`에 대 한 이벤트 처리기는 합니다 `HttpApplication` 이벤트 `BeginRequest`를 `AuthenticateRequest`, 및 `Error`, 각각. 명명 된 이벤트 처리기도 `Application_Start`, `Session_Start`, `Application_End`, 및 `Session_End`는 웹 응용 프로그램 시작는 새 세션 시작 응용 프로그램 종료 될 때 발생 하는 이벤트 처리기 및 세션을 종료 하는 경우 각각. `Global.asax` WSP에서 Visual Studio에서 만든 파일을 포함 합니다 `Application_Error`, `Application_Start`, `Session_Start`, `Application_End`, 및 `Session_End` 이벤트 처리기입니다.

> [!NOTE]
> 복사 해야 하는 ASP.NET 응용 프로그램을 배포 하는 경우는 `Global.asax` 프로덕션 환경에는 파일입니다. `Global.asax.cs` WAP에서 만들어진 파일을 프로젝트의 어셈블리에이 코드는 컴파일되기 때문에 프로덕션에 복사할 필요가 없습니다.


Visual Studio의 전역 응용 프로그램 클래스 템플릿에서 만든 이벤트 처리기 하지는 않습니다. 에 대 한 이벤트 처리기를 추가할 수 있습니다 `HttpApplication` 이벤트 처리기의 이름을 지정 하 여 이벤트 `Application_EventName`합니다. 예를 들어, 다음 코드를 추가할 수 있습니다 합니다 `Global.asax` 에 대 한 이벤트 처리기를 만들려는 파일의 [ `AuthorizeRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx):

[!code-cs[Main](processing-unhandled-exceptions-cs/samples/sample1.cs)]

마찬가지로, 전역 응용 프로그램 클래스 템플릿에서 만든 필요 하지 않은 모든 이벤트 처리기를 제거할 수 있습니다. 이 자습서에만 필요에 대 한 이벤트 처리기를 `Error` 이벤트;에서 다른 이벤트 처리기를 제거 하는 `Global.asax` 파일입니다.

> [!NOTE]
> *HTTP 모듈* 에 대 한 이벤트 처리기를 정의 하는 또 다른 방법은 제공 `HttpApplication` 이벤트입니다. HTTP 모듈은 별도 클래스 라이브러리로 웹 응용 프로그램 프로젝트 내에서 직접 배치 하거나 분리할 수 있는 클래스 파일으로 생성 됩니다. HTTP 모듈을 만들기 위한 더 유연 하 고 다시 사용할 수 있는 모델을 제공 클래스 라이브러리로 구분할 수 있습니다, 되므로 `HttpApplication` 이벤트 처리기입니다. 반면 합니다 `Global.asax` 파일은 특정 있는 웹 응용 프로그램에 HTTP 컴파일할 수 있는 모듈을 어셈블리에이 시점에서 웹 사이트에 HTTP 모듈을 추가 하기만 하면 됩니다에서 어셈블리를 삭제 합니다 `Bin` 폴더 및 등록 합니다 모듈에서 `Web.config`합니다. 이 자습서를 작성 하 고 HTTP 모듈을 사용 하 여 찾지 않습니다 하지만 다음 두 가지 자습서에서 사용 된 두 개의 오류 로깅 라이브러리는 HTTP 모듈로 구현 됩니다. 참조에 대 한 자세한 배경 HTTP 모듈의 이점 [를 사용 하 여 HTTP 모듈 및 처리기 플러그형 ASP.NET 구성 요소 만들기를](https://msdn.microsoft.com/library/aa479332.aspx)입니다.


## <a name="retrieving-information-about-the-unhandled-exception"></a>처리 되지 않은 예외에 대 한 정보를 검색합니다.

Global.asax 파일이 있다고 이때는 `Application_Error` 이벤트 처리기입니다. 이 이벤트 처리기를 실행 하는 경우 오류의 개발자에 게 알리고 해당 세부 정보를 기록 하려고 합니다. 이러한 작업을 수행 하려면 먼저 발생 하는 예외 세부 정보를 확인 해야 합니다. 서버 개체를 사용 하 여 [ `GetLastError` 메서드](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx) 시킨 처리 되지 않은 예외의 세부 정보를 검색 하는 `Error` 이벤트가 발생 합니다.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample2.cs)]

합니다 `GetLastError` 형식의 개체를 반환 하는 메서드 `Exception`,.NET Framework의 모든 예외에 대 한 기본 형식입니다. 그러나 위의 코드에서 I am 캐스팅 반환 하는 예외 개체 `GetLastError` 에 `HttpException` 개체입니다. 경우는 `Error` 내에서 throw 된 예외를 래핑된 다음 ASP.NET 리소스를 처리 하는 동안 예외가 throw 되었기 때문에 이벤트가 발생 중인을 `HttpException`입니다. 사용 하는 오류 이벤트를 살펴보고 실제 예외를 가져오려고 합니다 `InnerException` 속성입니다. 경우는 `Error` HTTP 기반 예외로 인해 존재 하지 않는 페이지 요청과 같은 이벤트가 발생을 `HttpException` throw 되 면 내부 예외가 없는 합니다.

다음 코드에서는 `GetLastErrormessage` 트리거되는 예외에 대 한 정보를 검색 하는 `Error` 이벤트를 저장 합니다 `HttpException` 라는 변수에 `lastErrorWrapper`합니다. 그런 다음 저장 형식, 메시지 및 예외의 원래 스택 추적 확인 하는 경우 3 개의 문자열 변수에 `lastErrorWrapper` 는 실제 예외를 트리거한는 `Error` (의 경우 HTTP 기반 예외)는 이벤트 또는 경우에 단순히를 요청을 처리 하는 동안 throw 된 예외에 대 한 래퍼.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample3.cs)]

이 시점에서 데이터베이스 테이블에는 예외의 세부 정보는 코드를 작성 해야 할 모든 정보가 있습니다. 각 요청된 된 페이지의 URL 및 현재 로그온된 한 사용자의 이름과 같은 정보를 다른 유용한 함께-형식, 메시지, 스택 추적 및 등-관심 오류 세부 정보에 대 한 열을 사용 하 여 데이터베이스 테이블을 만들 수 있습니다. 에 `Application_Error` 이벤트 처리기 다음 데이터베이스에 연결 하는 테이블에 레코드를 삽입 합니다. 마찬가지로, 개발자는 전자 메일을 통해 오류를 경고 하는 코드를 추가할 수 있습니다.

이 오류 로깅 및 알림을 직접 작성 하지 않아도 되므로 기본적으로 이러한 기능을 제공 하는 다음 두 자습서의 검사 오류 로깅 라이브러리입니다. 그러나는 설명 하기 위해 합니다 `Error` 이벤트가 발생 하 고는 `Application_Error` 이벤트 처리기를 사용 하 여 오류 세부 정보를 기록 하 고 개발자에 게 알림 오류가 있을 때 개발자에 게 알려 주는 코드를 추가 해 보겠습니다 하 수 있습니다.

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>처리 되지 않은 예외가 발생 하면 개발자에 게 알리지

프로덕션 환경에서 처리 되지 않은 예외가 발생 하면 오류를 평가 하 고 수행 해야 하는 작업을 확인할 수 있도록 개발 팀을 경고 하도록 반드시 합니다. 예를 들어 있으면 double 해야 데이터베이스 연결에 오류가 확인 연결 문자열 하 고, 웹 호스팅 회사를 사용 하 여 지원 티켓을 엽니다. 프로그래밍 오류로 인해 예외가 발생 하는 경우 추가 코드 또는 유효성 검사 논리 오류를 방지 하려면 이러한 나중에 추가 해야 합니다.

.NET Framework의 클래스는 [ `System.Net.Mail` 네임 스페이스](https://msdn.microsoft.com/library/system.net.mail.aspx) 전자 메일을 보낼 수 있도록 합니다. [ `MailMessage` 클래스](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) 전자 메일 메시지를 나타내며 같은 속성이 `To`를 `From`를 `Subject`를 `Body`, 및 `Attachments`합니다. `SmtpClass` 보내는 데 사용 되는 `MailMessage` 지정된 된 SMTP 서버를 사용 하 여; SMTP 서버 설정에 프로그래밍 방식으로 또는 선언적으로 지정할 수 있습니다 합니다 [ `<system.net>` 요소](https://msdn.microsoft.com/library/6484zdc1.aspx) 에 `Web.config file`. ASP.NET 응용 프로그램에서 메시지 확인 전자 메일을 보내는 방법에 대 한 자세한 내용은 필자의 기사 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx), 및 [System.Net.Mail FAQ](http://systemnetmail.com/)합니다.

> [!NOTE]
> 합니다 `<system.net>` 요소에서 사용 하는 SMTP 서버 설정을 포함 합니다 `SmtpClient` 전자 메일을 보낼 때 클래스입니다. 웹 호스팅 가능성이 회사 전자 메일을 보내는 응용 프로그램에서 사용할 수 있는 SMTP 서버를 있습니다. 웹 응용 프로그램에서 사용 해야 하는 SMTP 서버 설정에 대 한 정보는 웹 호스트의 지원 섹션을 참조 하세요.


다음 코드를 추가 합니다 `Application_Error` 개발자는 전자 메일을 보내는 오류가 발생할 때 이벤트 처리기:

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample4.cs)]

위의 코드는 매우 긴 하지만 대량으로 개발자에 게 보낸 전자 메일에 표시 되는 HTML을 만듭니다. 참조 하 여 시작 하는 코드를 `HttpException` 반환한 합니다 `GetLastError` 메서드 (`lastErrorWrapper`). 요청에서 발생 하는 실제 예외를 통해 검색 됩니다 `lastErrorWrapper.InnerException` 변수에 할당 됩니다 `lastError`합니다. 유형, 메시지 및 스택 추적 정보에서 검색 됩니다 `lastError` 이며 3 개의 문자열 변수에 저장 합니다.

다음으로 `MailMessage` 개체인 `mm` 만들어집니다. 전자 메일 본문에는 HTML 형식의 이며 (형식, 메시지 및 스택 추적)는 예외에 대 한 정보와 현재 로그온된 한 사용자 이름, 요청된 된 페이지의 URL을 표시 합니다. 에 대 한 멋진 기능 중 하나는 `HttpException` 클래스는 호출 하 여는 예외 세부 정보 노란색 화면의 사망 (YSOD)를 만드는 데 HTML를 생성할 수 있습니다 합니다 [GetHtmlErrorMessage 메서드](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx)합니다. 이 메서드는 예외 세부 정보 YSOD 태그를 검색 하 고 전자 메일 첨부 파일에 추가 하려면 여기 사용 됩니다. 주의 사항: 트리거되는 예외를 `Error` 이벤트 예외가 HTTP 기반 (예: 존재 하지 않는 페이지에 대 한 요청) 하면 `GetHtmlErrorMessage` 메서드는 반환 `null`합니다.

마지막 단계는 보내도록는 `MailMessage`합니다. 새 이렇게 `SmtpClient` 메서드를 호출 해당 `Send` 메서드.

> [!NOTE]
> 웹 응용 프로그램에서이 코드를 사용 하기 전에 값을 변경 하려는 합니다 `ToAddress` 및 `FromAddress` 상수 support@example.com 모든 전자 메일에 오류 알림 전자 메일 주소를 보낼 및에서 발생 합니다. 에 SMTP 서버 설정을 지정 해야 합니다 `<system.net>` 단원의 `Web.config`합니다. 사용할 SMTP 서버 설정을 확인 하 여 웹 호스트 공급자를 참조 하세요.


이 코드를 사용 하 여 오류가 발생 하는 언제 든 지 개발자가 보내집니다 오류를 요약 하 고는 YSOD 포함 한 전자 메일 메시지. 이전 자습서에서 주었습니다 런타임 오류가 Genre.aspx를 방문 하 고 잘못에서 전달 `ID` querystring을 통해 같은 값 `Genre.aspx?ID=foo`합니다. 사용 하 여 페이지를 방문 하 여 `Global.asax` -이전 자습서에서 개발 환경에서 계속 해 서 하면 프로덕션 환경에서 하는 동안 예외 세부 정보 노란색 화면의 쇠퇴, 보려는 처럼 동일한 사용자 환경을 생성 하는 준비 된 파일 사용자 지정 오류 페이지를 참조 하세요. 이 기존 동작 외에도 개발자는 전자 메일이 전송 됩니다.

**그림 2** 방문할 때 받은 전자 메일을 보여 줍니다 `Genre.aspx?ID=foo`합니다. 전자 메일 본문에 예외 정보를 요약 하는 동안 합니다 `YSOD.htm` 첨부 파일에는 예외 세부 정보 YSOD에 표시 되는 콘텐츠가 표시 됩니다 (참조 **그림 3**).

[![](processing-unhandled-exceptions-cs/_static/image5.png)](processing-unhandled-exceptions-cs/_static/image4.png)

**그림 2**: 개발자 처리 되지 않은 예외가 있을 때마다 전자 메일 알림이 전송 됩니다  
([클릭 하 여 큰 이미지 보기](processing-unhandled-exceptions-cs/_static/image6.png))

[![](processing-unhandled-exceptions-cs/_static/image8.png)](processing-unhandled-exceptions-cs/_static/image7.png)

**그림 3**: 첨부 파일로 YSOD 예외 세부 정보를 포함 하는 전자 메일 알림  
([클릭 하 여 큰 이미지 보기](processing-unhandled-exceptions-cs/_static/image9.png))

## <a name="what-about-using-the-custom-error-page"></a>사용자 지정 오류 페이지를 사용 하 여 어떨까요?

이 자습서에 사용 하는 방법을 보여 주었습니다 `Global.asax` 하며 `Application_Error` 처리 되지 않은 예외가 발생 하면 코드를 실행 하는 이벤트 처리기입니다. 특히에서는이 이벤트 처리기에 게 알리는 데 오류의; 개발자 또한 데이터베이스에 오류 정보를 기록 하도록 확장 수 없습니다. 현재 상태는 `Application_Error` 이벤트 처리기에 최종 사용자의 환경 영향을 주지 않습니다. 이러한 오류 세부 정보 YSOD, 런타임 오류 YSOD 또는 사용자 지정 오류 페이지 구성된 오류 페이지를 계속 참조 합니다.

궁금해에 자연 스러운 것 여부를 `Global.asax` 파일 및 `Application_Error` 이벤트는 사용자 지정 오류 페이지를 사용 하는 경우에 필요 합니다. 오류가 발생 사용자에 게는 사용자 지정 오류 페이지를 표시 하는 경우 따라서 이유 없습니다 넣을까요 개발자에 게 알리고 사용자 지정 오류 페이지의 코드 숨김 클래스에 오류 정보를 기록 하는 코드? 물론 사용자 지정 오류 페이지의 코드 숨김 클래스에 코드를 추가할 수 있는 반면 필요가 없습니다를 트리거한 예외의 세부 정보에 대 한 액세스는 `Error` 이전 자습서에서 살펴본 기술을 사용 하는 경우에 이벤트입니다. 호출 된 `GetLastError` 사용자 지정 오류 페이지에서 반환 `Nothing`합니다.

이 동작에 대 한 이유는 리디렉션을 통해 사용자 지정 오류 페이지에 도달 하는 때문입니다. 처리 되지 않은 예외에 도달 하면 ASP.NET 런타임이 ASP.NET 엔진을 발생 시킵니다 해당 `Error` 이벤트 (실행 하는 합니다 `Application_Error` 이벤트 처리기) 차례로 *리디렉션합니다* 를실행하여사용자지정오류페이지로`Response.Redirect(customErrorPageUrl)`. `Response.Redirect` 메서드 브라우저를 사용자 지정 오류 페이지 즉 새 URL을 요청 하도록 지시 하는 HTTP 302 상태 코드와 함께 클라이언트에 대 한 응답을 보냅니다. 브라우저가 자동으로 요청 합니다이 새 페이지. 알 수 있습니다 지정 오류 페이지는 페이지에서 별도로 요청 된 사용자 지정 오류 페이지 URL을 브라우저의 주소 표시줄 변경 되기 때문에 오류 발생 (참조 **그림 4**).

[![](processing-unhandled-exceptions-cs/_static/image11.png)](processing-unhandled-exceptions-cs/_static/image10.png)

**그림 4**: 때 오류가 발생 브라우저 사용자 지정 오류 페이지 URL로 리디렉션됩니다.  
([클릭 하 여 큰 이미지 보기](processing-unhandled-exceptions-cs/_static/image12.png))

서버는 HTTP 302 리디렉션으로 응답 하는 경우 처리 되지 않은 예외가 발생 하는 요청이 종료는 최종적 이며 사용자 지정 오류 페이지에 대 한 후속 요청은 새로운 요청; 이 여기서는 ASP.NET 엔진이 오류 정보를 무시 하 여, 또한에 사용자 지정 오류 페이지에 대 한 새 요청을 사용 하 여 이전 요청에서 처리 되지 않은 예외를 연결할 수 없습니다. 이 인해 `GetLastError` 반환 `null` 사용자 지정 오류 페이지에서 호출 합니다.

그러나 것 같은 요청 오류를 발생 하는 동안 실행 하는 사용자 지정 오류 페이지를 가질 수 있습니다. 합니다 [ `Server.Transfer(url)` ](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx) 메서드 실행을 지정된 된 URL로 이동 하 고 동일한 요청 내에서 처리 합니다. 코드를 이동할 수 있습니다 합니다 `Application_Error` 이벤트 처리기에서 대체 되는 사용자 지정 오류 페이지의 코드 숨김 클래스를 `Global.asax` 다음 코드를 사용 하 여:

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample5.cs)]

처리 되지 않은 예외가 발생 하면 이제는 `Application_Error` 이벤트 처리기는 HTTP 상태 코드를 기반으로 적절 한 사용자 지정 오류 페이지에 제어를 전송 합니다. 사용자 지정 오류 페이지를 통해 처리 되지 않은 예외 정보에 대 한 액세스 권한이 제어를 전송 된 하므로 `Server.GetLastError` 오류의 개발자에 게 알림 수 및 해당 세부 정보를 기록 합니다. `Server.Transfer` 호출에서 사용자 지정 오류 페이지로 사용자를 리디렉션 ASP.NET 엔진을 중지 합니다. 대신 사용자 지정 오류 페이지의 콘텐츠는 오류를 생성 하는 페이지에 대 한 응답으로 반환 됩니다.

## <a name="summary"></a>요약

ASP.NET 런타임에서 발생 하는 ASP.NET 웹 응용 프로그램에서 처리 되지 않은 예외가 발생 하는 경우는 `Error` 이벤트 구성된 오류 페이지를 표시 합니다. 오류의 개발자에 게 해당 세부 정보를 기록 하거나 오류 이벤트에 대 한 이벤트 처리기를 만들어 몇 가지 다른 방식으로 처리할 수 있습니다 했습니다. 두 가지 방법으로 이벤트 처리기를 만들려면 `HttpApplication` 와 같은 이벤트가 `Error`:에서 `Global.asax` 파일 또는 HTTP 모듈에서. 이 자습서에는 만드는 방법을 보여 주었습니다를 `Error` 이벤트 처리기는 `Global.asax` 전자 메일 메시지를 사용 하 여 오류가 발생 하는 개발자에 게 알려 주는 파일입니다.

만들기는 `Error` 이벤트 처리기는 몇 가지 고유한 또는 사용자 지정 방식으로 처리 되지 않은 예외를 처리 해야 하는 경우에 유용 합니다. 그러나 직접 만드는 `Error` 이벤트 처리기를 예외를 기록 하거나 개발자에 알리기 위해가 시간을 가장 효율적으로 사용 있습니다 몇 분 내에에서 설치 될 수 있는 무료이 고 사용 하기 쉬운 오류 로깅 라이브러리에 이미 존재 합니다. 다음 두 자습서는 이러한 라이브러리를 검사합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET HTTP 모듈과 HTTP 처리기 개요](https://support.microsoft.com/kb/307985)
- [정상적으로 처리 되지 않은 예외를 처리 하는 처리 되지 않은 예외-응답](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication` 클래스 및 ASP.NET 응용 프로그램 개체](http://www.eggheadcafe.com/articles/20030211.asp)
- [ASP.NET에서 HTTP 모듈과 HTTP 처리기](http://www.15seconds.com/Issue/020417.htm)
- [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [이해를 `Global.asax` 파일](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [플러그형 ASP.NET 구성 요소를 만드는 HTTP 모듈 및 처리기를 사용 하 여](https://msdn.microsoft.com/library/aa479332.aspx)
- [ASP.NET을 사용 하 여 작업 `Global.asax` 파일](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [작업할 `HttpApplication` 인스턴스](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [이전](displaying-a-custom-error-page-cs.md)
> [다음](logging-error-details-with-asp-net-health-monitoring-cs.md)
