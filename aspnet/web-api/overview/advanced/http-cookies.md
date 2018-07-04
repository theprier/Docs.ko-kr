---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API에서에서 HTTP 쿠키 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/17/2012
ms.topic: article
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 5885586df1d0f67d4e7e04ad88bc4fd1af71dc80
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368407"
---
<a name="http-cookies-in-aspnet-web-api"></a>ASP.NET Web API에서에서 HTTP 쿠키
====================
[Mike Wasson](https://github.com/MikeWasson)

이 항목에는 Web API에서 HTTP 쿠키를 송수신 하는 방법을 설명 합니다.

## <a name="background-on-http-cookies"></a>HTTP 쿠키에 대 한 배경

이 섹션에서는 쿠키 HTTP 수준에서 구현 하는 방법에 대해 간략하게 설명 합니다. 자세한 내용은 참조 하세요 [RFC 6265](http://tools.ietf.org/html/rfc6265)합니다.

쿠키는 HTTP 응답에는 서버에 보내는 데이터의 일부입니다. (선택 사항) 클라이언트는 쿠키를 저장 하 고 subsequet 요청에 반환 합니다. 이렇게 하면 클라이언트 및 서버 상태를 공유할 수 있습니다. 쿠키를 설정 하려면 서버 응답에서 Set-cookie 헤더를 포함 합니다. 쿠키의 형식은 선택적 특성이 있는 이름-값 쌍을 합니다. 예를 들어:

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

특성의 예는 다음과 같습니다.

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

쿠키를 서버에 반환할 클라이언트가 이후 요청에 쿠키 헤더를 포함 합니다.

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

HTTP 응답을 여러 Set-cookie 헤더를 포함할 수 있습니다.

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

클라이언트에서는 단일 쿠키 헤더를 사용 하 여 여러 쿠키를 반환 합니다.

[!code-console[Main](http-cookies/samples/sample5.cmd)]

범위 및 기간 쿠키를 Set-cookie 헤더에 다음 특성에 의해 제어 됩니다.

- **도메인**:는 도메인에 쿠키를 받아야 합니다. 클라이언트에 게 알립니다. 예를 들어 도메인이 "example.com" 인 경우 클라이언트 example.com의 모든 하위 도메인에 쿠키를 반환 합니다. 지정 하지 않으면 도메인에 원본 서버입니다.
- **경로**: 도메인 내에서 지정된 된 경로에 쿠키를 제한 합니다. 지정 하지 않으면 요청 URI의 경로 사용 됩니다.
- **만료**: 쿠키의 만료 날짜를 설정 합니다. 클라이언트는 만료 되 면 쿠키를 삭제 합니다.
- **최대 처리 기간**: 쿠키의 최대 보관 기간을 설정 합니다. 최대 보존 기간에 도달 하면 클라이언트 쿠키를 삭제 합니다.

둘 다 `Expires` 하 고 `Max-Age` 설정 된 `Max-Age` 우선적으로 적용 합니다. 설정 하지 않으면 하는 경우 현재 세션이 종료 될 때 클라이언트 쿠키를 삭제 합니다. ("세션"의 정확한 의미는 사용자-에이전트에 의해 결정 됩니다.)

그러나 클라이언트가 쿠키를 무시 해도 주의 합니다. 예를 들어, 사용자 개인 정보 보호에 대 한 쿠키를 비활성화할 수 있습니다. 저장 된 쿠키 수를 제한 하거나 만료 하기 전에 클라이언트에서 쿠키를 삭제할 수 있습니다. 개인 정보 보호를 위해 클라이언트는 종종 "타사" 쿠키를 도메인 원본 서버에 맞지 않습니다 거부 합니다. 즉, 서버 설정 하는 쿠키를 다시 시작에 의존 하지 않아야 합니다.

## <a name="cookies-in-web-api"></a>Web API에서 쿠키

HTTP 응답에 쿠키를 추가 하려면 만들기를 **CookieHeaderValue** 쿠키를 나타내는 인스턴스입니다. 다음 호출을 **AddCookies** 에 정의 된 확장 메서드를 **System.Net.Http 합니다. HttpResponseHeadersExtensions** 클래스에 쿠키를 추가 합니다.

예를 들어, 다음 코드는 컨트롤러 작업 내에서 쿠키를 추가합니다.

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

있음을 **AddCookies** 배열을 **CookieHeaderValue** 인스턴스.

호출에 클라이언트 요청에서 쿠키를 추출 합니다 **GetCookies** 메서드:

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

A **CookieHeaderValue** 의 컬렉션을 포함 **CookieState** 인스턴스. 각 **CookieState** 하나 쿠키를 나타냅니다. 인덱서 메서드를 사용 하 여 가져올는 **CookieState** 이름순으로 표시 된 것 처럼 합니다.

## <a name="structured-cookie-data"></a>구조화 된 쿠키 데이터

다양 한 브라우저 제한 횟수 쿠키를 저장 합니다&#8212;, 총 수와 각 도메인 수입니다. 따라서 여러 쿠키를 설정 하는 대신 단일 쿠키 구조화 된 데이터를 넣을 유용할 수 있습니다.

> [!NOTE]
> RFC 6265 쿠키 데이터 구조를 정의 하지 않습니다.


사용 하는 **CookieHeaderValue** 클래스 쿠키 데이터에 대 한 이름-값 쌍의 목록을 전달할 수 있습니다. 이러한 이름-값 쌍 Set-cookie 헤더의 URL로 인코딩된 양식 데이터로 인코딩됩니다.

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

이전 코드는 다음과 같은 Set-cookie 헤더를 생성합니다.

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

합니다 **CookieState** 클래스 값을 읽는 하위 요청 메시지의 쿠키에서 인덱서 메서드를 제공 합니다.

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>예제: 설정 및 메시지 처리기에서 쿠키를 검색 합니다.

이전 예제에는 Web API 컨트롤러 내에서 쿠키를 사용 하는 방법을 보여 주었습니다. 사용 하는 다른 옵션도 [메시지 처리기](http-message-handlers.md)합니다. 이전 컨트롤러 보다 파이프라인에서에서 메시지 처리기가 호출 됩니다. 메시지 처리기 요청에는 컨트롤러에 도달 하기 전에 요청에서 쿠키를 읽을 하거나 컨트롤러 응답을 생성 한 후 응답에 쿠키를 추가할 수 있습니다.

![](http-cookies/_static/image2.png)

다음 코드는 세션 Id를 만들기에 대 한 메시지 처리기를 보여 줍니다. 세션 ID는 쿠키에 저장 됩니다. 처리기는 세션 쿠키에 대 한 요청을 확인합니다. 처리기는 새 세션 ID가 생성 요청 쿠키를 포함 하지 않는 경우 두 경우 모두 처리기에 세션 ID를 저장 합니다 **HttpRequestMessage.Properties** 속성 모음입니다. 또한 세션 쿠키를 HTTP 응답에 추가합니다.

이 구현은 클라이언트에서 세션 ID를 서버에서 실제로 발행 하는 것을 확인 하지 않습니다. 인증 형식으로 사용 하지 않아도! 이 예제에서는 지점의 HTTP 쿠키 관리를 보여 줍니다.

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

컨트롤러의 세션 ID를 가져올 수는 **HttpRequestMessage.Properties** 속성 모음입니다.

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
