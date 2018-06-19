---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: 인증 및 ASP.NET Web API의에서 권한 부여 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API의 인증 및 권한 부여에 대 한 일반적인 개요를 제공 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/27/2012
ms.topic: article
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d7cbb9505afb6461ba4c2087d57e9ea0da38ede
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
ms.locfileid: "29726760"
---
<a name="authentication-and-authorization-in-aspnet-web-api"></a>인증 및 ASP.NET Web API의에서 권한 부여
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

웹 API를 만들었지만 이제에 대 한 액세스를 제어 하려고 합니다. 이러한 일련의 문서, 웹 API 권한 없는 사용자 로부터 보호 하기 위한 몇 가지 옵션 살펴보겠습니다. 이 시리즈에서는 인증 및 권한 부여에 모두 설명 합니다.

- *인증* 사용자의 id를 아는 것입니다. 예를 들어 Alice가 자신의 사용자 이름과 암호를 로그인 하 고 서버 암호를 사용 하 여 Alice를 인증 합니다.
- *권한 부여* 사용자가 작업을 수행할 수 있는지 여부를 결정 해야 합니다. 예를 들어 Alice에 리소스를 가져오지만 리소스를 만들 수 있는 권한이 있습니다.

시리즈에서 첫 번째 문서 ASP.NET Web API에 인증 및 권한 부여에 대 한 일반적인 개요를 제공합니다. 다른 항목 웹 API에 대 한 일반적인 인증 시나리오를 설명합니다.

> [!NOTE]
> 이 시리즈를 검토 하 고 고객 의견을 제공 하는 사용자 덕분에: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, 김 Roth, Tim Teebken 합니다.


## <a name="authentication"></a>인증

Web API에 인증 하는 호스트에서 발생 하는 가정 합니다. 웹 호스팅에 대 한 호스트가 IIS 인증에 HTTP 모듈을 사용 합니다. IIS 또는 ASP.NET에 기본 제공 인증 모듈을 사용 하 여 프로젝트를 구성 하거나 사용자 지정 인증을 수행할 사용자 고유의 HTTP 모듈을 작성할 수 있습니다.

호스트에서 사용자를 인증 하는 경우 생성 한 *주*, 변수인는 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 코드가 실행 되는 보안 컨텍스트를 나타내는 개체입니다. 호스트가 현재 스레드를 설정 하 여 주 서버를 연결할 **Thread.CurrentPrincipal**합니다. 연결 된 보안 주체가 포함 **Identity** 사용자에 대 한 정보를 포함 하는 개체입니다. 사용자가 인증 하는 경우는 **Identity.IsAuthenticated** 속성에서 반환 **true**합니다. 익명 요청에 대 한 **IsAuthenticated** 반환 **false**합니다. 보안 주체에 대 한 자세한 내용은 참조 [역할 기반 보안](https://msdn.microsoft.com/library/shz8h065.aspx)합니다.

### <a name="http-message-handlers-for-authentication"></a>인증에 대 한 HTTP 메시지 처리기

인증에 대 한 호스트를 사용 하는 대신에 인증 논리를 넣을 수 있습니다는 [HTTP 메시지 처리기](../advanced/http-message-handlers.md)합니다. 이 경우 메시지 처리기는 HTTP 요청을 검사 하 고 주 서버를 설정 합니다.

인증에 대 한 메시지 처리기를 사용 해야는 경우 다음은 몇 가지 단점입니다.

- HTTP 모듈 ASP.NET 파이프라인을 통해 이동 하는 모든 요청을 볼 수 있습니다. 메시지 처리기 라우팅된 웹 API에 요청을 볼 수 있습니다.
- 경로 당 메시지 처리기에 특정 경로에 인증 체계를 적용할 수 있는 설정할 수 있습니다.
- HTTP 모듈을 IIS에 적용 됩니다. 메시지 처리기 호스트-불가 지론 적 되므로 웹 호스팅 및 자체 호스트와 함께 사용할 수 있습니다.
- HTTP 모듈 IIS 로깅, 감사 등에 참여 합니다.
- 파이프라인의 앞부분에 나오는 HTTP 모듈 실행합니다. 메시지 처리기에서 인증을 처리 하는 경우에 처리기가 실행 가져올 보안 주체 설정지 않습니다. 또한 주 서버는 응답 메시지 처리기를 벗어날 때 이전 주 서버로 되돌리면 되돌립니다.

일반적으로 셀프 호스팅을 지 원하는 데 필요 하지 않으면, HTTP 모듈이 더 좋습니다. 셀프 호스팅을 지원 하도록 해야 할 경우 메시지 처리기를 것이 좋습니다.

### <a name="setting-the-principal"></a>주 서버를 설정합니다.

모든 사용자 지정 인증 논리를 수행 하는 응용 프로그램을 두 위치에 주 서버를 설정 해야 합니다.

- **Thread.CurrentPrincipal**. 이 속성은.net에서 스레드의 보안 주체를 설정 하는 표준 방법입니다.
- **HttpContext.Current.User**. 이 속성은 ASP.NET 관련이 있습니다.

다음 코드에는 주 서버를 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

웹 호스팅을 위한; 양쪽 모두에서 보안 주체를 설정 해야 그렇지 않으면 보안 컨텍스트에 일관성이 없을 수 있습니다. 그러나 자체 호스팅, **HttpContext.Current** null입니다. 코드는 호스트를 알 수 있도록 따라서 null 확인을 할당 하기 전에 **HttpContext.Current**표시 된 것 처럼 합니다.

## <a name="authorization"></a>권한 부여

권한 부여는 파이프라인의 뒷부분에 나오는 발생 컨트롤러에 더 가깝기 때문입니다. 기능을 사용 하면 리소스에 대 한 액세스 권한을 부여 하면 더 세분화 된 항목을 선택할 수 있습니다.

- *권한 부여 필터* 컨트롤러 작업 전에 실행 합니다. 요청이 허가 되지 않았습니다 오류 응답을 반환 하는 필터 및 작업은 호출 되지 않습니다.
- 컨트롤러 작업 내에서 현재 보안 주체를 얻을 수 있습니다는 **ApiController.User** 속성입니다. 예를 들어 해당 사용자에 게 속해 있는 리소스에만 반환 합니다. 사용자 이름을 기반으로 하는 리소스의 목록을 필터링 할 수 있습니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>사용 하 고 [인증] 특성

기본 제공 권한 부여 필터를 제공 하는 web API [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)합니다. 이 필터는 사용자가 인증 여부를 확인 합니다. 그렇지 않으면 다음 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)를 반환 합니다.

컨트롤러 수준에서 전역적으로 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.

**전역으로**: 모든 Web API 컨트롤러에 대 한 액세스를 제한 하려면 추가 **AuthorizeAttribute** 필터를 전역 필터 목록:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**컨트롤러**: 특정 컨트롤러에 대 한 액세스를 제한 하려면 필터 특성으로 컨트롤러를 추가 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**작업**: 특정 작업에 대 한 액세스를 제한 하려면 동작 메서드에 특성을 추가 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

컨트롤러를 제한 한 다음 사용 하 여 특정 작업에 대 한 익명 액세스를 허용 하는 또는 `[AllowAnonymous]` 특성입니다. 다음 예제에서는 `Post` 메서드 액세스가 제한 되지만 `Get` 메서드 익명 액세스를 허용 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

이전 예제에서 필터는; 제한 된 메서드에 액세스 하려면 모든 인증 된 사용자 익명 사용자만 상태로 유지 됩니다. 또한 특정 역할에 사용자 또는 특정 사용자에 게 액세스를 제한할 수 있습니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> **AuthorizeAttribute** Web API 컨트롤러에 대 한 필터에는 **System.Web.Http** 네임 스페이스입니다. MVC 컨트롤러에 대 한 유사한 필터는 **System.Web.Mvc** 네임 스페이스에 Web API 컨트롤러와 호환 되지 않습니다.


### <a name="custom-authorization-filters"></a>사용자 지정 권한 부여 필터

사용자 지정 권한 부여 필터를 작성 하려면 이러한 형식 중 하나에서 파생 됩니다.

- **AuthorizeAttribute**합니다. 현재 사용자와 사용자의 역할 기반 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.
- **AuthorizationFilterAttribute**합니다. 현재 사용자 또는 역할에 기반 하지 않는 동기 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.
- **IAuthorizationFilter**합니다. 비동기 권한 부여 논리를 수행 하려면이 인터페이스를 구현 합니다. 예를 들어, 권한 부여 논리 비동기 I/O 또는 네트워크 호출을 하는 경우. (권한 부여 논리 CPU 바인딩된 경우 간단 하 게에서 파생 되는 **AuthorizationFilterAttribute**때문에 비동기 메서드를 작성 하지 않아도 됩니다.)

다음 다이어그램에 대 한 클래스 계층 구조를 보여 줍니다.는 **AuthorizeAttribute** 클래스입니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>컨트롤러 작업 내의 권한 부여

경우에 따라 계속 되지만 보안 주체에 따라 동작을 변경 하는 요청을 통합할 수 있습니다. 예를 들어 사용자가 반환 하는 정보는 사용자의 역할에 따라 변경 될 수 있습니다. 컨트롤러 메서드 내에서 현재 사용자를 가져올 수 있습니다는 **ApiController.User** 속성입니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
