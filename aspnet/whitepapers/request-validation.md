---
uid: whitepapers/request-validation
title: 요청 유효성 검사-스크립트 공격 방지 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는의 where, 기본적으로 응용 프로그램 수 없거나 인코딩되지 않은 HTML 콘텐츠 submitt 처리 되지 않도록 하는 ASP.NET 요청 유효성 검사 기능을 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 0b24fe2193d2c7a858667505bad9ed0b1d70a328
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
ms.locfileid: "28883557"
---
<a name="request-validation---preventing-script-attacks"></a>요청 유효성 검사-스크립트 공격 방지
====================
> 이 문서에서는의 where, 기본적으로 응용 프로그램 수 없거나 서버에 제출 하는 인코딩되지 않은 HTML 콘텐츠를 처리 하는 ASP.NET 요청 유효성 검사 기능을 설명 합니다. 응용 프로그램 HTML 데이터를 안전 하 게 처리 하도록 디자인 된 경우이 요청 유효성 검사 기능을 비활성화할 수 있습니다.
> 
> ASP.NET 1.1 및 ASP.NET 2.0에 적용 됩니다.


ASP.NET의 버전 1.1에서 이후 기능 요청 유효성 검사를 포함 하는 콘텐츠 인코딩되지 않은 HTML으로 서버를 방지 합니다. 이 기능은 그에 따라 클라이언트 스크립트 코드 또는 HTML 수 될 서버에 제출 하지 못하도록 저장 하 고 다른 사용자에 게 표시 한 다음 몇 가지 스크립트 삽입 공격을 방지 하도록 설계 되었습니다. 여전히이 모든 입력된 데이터를 유효성 검사 및 HTML 인코딩으로 적절 한 시기.

예를 들어 사용자의 전자 메일 주소 및 저장소 데이터베이스에서 전자 메일 주소를 요청 하는 웹 페이지를 만들 있습니다. 사용자가 입력 &lt;스크립트&gt;경고 ("스크립트에서 hello")&lt;/script&gt; 유효한 전자 메일 주소 대신 해당 데이터가 제공 될 때이 스크립트 경우 실행할 수 있습니다 콘텐츠가 제대로 인코딩되지 않았습니다. 요청 유효성 검사 기능을 ASP.NET의 상황이 발생 하면 수 없습니다.

## <a name="why-this-feature-is-useful"></a>이 기능은 유용

대부분의 사이트는 단순한 스크립트 삽입 공격에 열려 있는지 확인 하지 않습니다. 이러한 공격의 목적은 HTML을 표시 하 여 사이트를 손상 또는 잠재적으로 클라이언트 스크립트를 실행 하는 해커의 사이트에 사용자를 리디렉션할 인지 스크립트 삽입 공격 웹 개발자가 충돌 하는 문제는 합니다.

스크립트 삽입 공격은 모든 웹 개발자의 문제가 ASP.NET, ASP, 또는 기타 웹 개발 기술을 사용 하는 여부.

ASP.NET 요청 유효성 검사 기능을 개발자가 해당 콘텐츠를 허용 하도록 결정 하지 않는 한 서버에서 처리 되도록 인코딩되지 않은 HTML 콘텐츠를 허용 하지 않음으로써 이러한 공격을 방지 하는 사전입니다.

## <a name="what-to-expect-error-page"></a>기대 하는: 오류 페이지

아래 스크린샷과 몇 가지 샘플 ASP.NET 코드를 보여 줍니다.

![](request-validation/_static/image1.png)

이 코드의 결과 텍스트 상자에 일부 텍스트를 입력할 수 있는 간단한 페이지에 실행 단추를 클릭 하 고 텍스트 레이블 컨트롤에 표시:

![](request-validation/_static/image2.png)

그러나 JavaScript 같은 된 `<script>alert("hello!")</script>` 를 입력 하 고 제출 예외가 발생 합니다.

![](request-validation/_static/image3.png)

없다는 오류 메시지가 '잠재적으로 위험한 Request.Form 값이 발견 되었습니다' 정확 하 게 발생 한 문제와 동작을 변경 하는 방법에 대 한 설명에 자세한 세부 정보를 제공 합니다. 예:

요청 중단 되었습니다. 요청을 처리 및 유효성 검사는 잠재적으로 위험한 클라이언트 입력된 값을 검색 했습니다. 이 값에는 사이트 간 스크립팅 공격과 같이 응용 프로그램의 보안을 손상 시킬를 나타낼 수 있습니다. 요청 유효성 검사를 사용 하지 않도록 설정 하 여 수 `validateRequest=false` Page 지시문에서 또는 구성 섹션에 있습니다. 그러나는 응용 프로그램이 명시적으로 검사 모든 입력이 경우 것이 좋습니다.

## <a name="disabling-request-validation-on-a-page"></a>페이지에서 요청 유효성 검사를 사용 하지 않도록 설정

설정 해야 하는 페이지에서 요청 유효성 검사를 사용 하지 않도록 설정 하는 `validateRequest` 페이지 지시문의 특성 `false`:

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> 요청 유효성 검사를 비활성화; 페이지에 콘텐츠를 전송할 수 있습니다. 해당 콘텐츠를 확인 하려면 페이지 개발자의 책임은 제대로 인코딩된 또는 처리지 않습니다.

## <a name="disabling-request-validation-for-your-application"></a>응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정

응용 프로그램에 대 한 요청 유효성 검사를 해제 하려면 수정 하거나 응용 프로그램에 대 한 Web.config 파일을 만들어 하 고 validateRequest 특성의 값으로 설정 된 `<pages />` 섹션을 `false`:

[!code-xml[Main](request-validation/samples/sample2.xml)]

서버의 모든 응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하려면 Machine.config 파일에이 수정 작업을 만들 수 있습니다.

> [!CAUTION]
> 요청 유효성 검사를 사용 하지 않도록 설정 하는 경우 콘텐츠 전송할 수 있습니다. 응용 프로그램입니다. 해당 콘텐츠를 확인 하는 응용 프로그램 개발자의 책임은 제대로 인코딩된 또는 처리지 않습니다.

아래 코드를 수정 하 여 요청 유효성 검사를 해제 하려면:

![](request-validation/_static/image4.png)

이제 텍스트 상자에 입력 한 다음 JavaScript `<script>alert("hello!")</script>` 라고 할 때 결과:

![](request-validation/_static/image5.png)

이 방지 하려면 기능을 해제 하는 요청 유효성 검사와 म 필요 HTML로 인코딩 콘텐츠입니다.

## <a name="how-to-html-encode-content"></a>Html 콘텐츠를 인코딩 방법

요청 유효성 검사를 비활성화 한 경우 이기 HTML 인코딩 콘텐츠 나중에 사용할 저장 될 것이 좋습니다. HTML 인코딩을 자동으로 덮어씁니다 모든 '&lt;'또는'&gt;' (함께 다른 여러 기호)와 해당 HTML 인코딩 표현입니다. 예를 들어 '&lt;'으로 바뀝니다'&amp;lt;' 및 '&gt;'으로 바뀝니다'&amp;gt;'. 브라우저는 이러한 특수 코드 표시 하는 데 사용 된 '&lt;'또는'&gt;' 브라우저에서 합니다.

콘텐츠를 쉽게 HTML로 인코딩된 사용 하 여 서버 수는 `Server.HtmlEncode(string)` API입니다. 콘텐츠 수도 있습니다 쉽게 HTML로 디코딩되어, 즉, 사용 하 여 표준 HTML 되돌아가서는 `Server.HtmlDecode(string)` 메서드.

![](request-validation/_static/image6.png)

결과:

![](request-validation/_static/image7.png)
