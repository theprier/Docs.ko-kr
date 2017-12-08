---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: "열린 리디렉션 공격 방지 (C#) | Microsoft Docs"
author: jongalloway
description: "이 자습서에서는 ASP.NET MVC 응용 프로그램에서 열려 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다. 이 자습서에는 적용 된 변경 사항에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: 97e0aacbf21914bf95f01019cf4dcc9e7ca1c4be
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="preventing-open-redirection-attacks-c"></a>열린 리디렉션 공격 방지 (C#)
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 열려 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다. 이 자습서 AccountController ASP.NET MVC 3에서에서 적용 된 변경에 설명 하 고 기존 ASP.NET MVC 1.0 프로그램 및 2 응용 프로그램에서 이러한 변경 내용을 적용 하는 방법을 시연 합니다.


## <a name="what-is-an-open-redirection-attack"></a>열린 리디렉션 공격 무엇입니까?

잠재적으로 쿼리 문자열 또는 폼 데이터와 같은 요청을 통해 지정 된 URL로 리디렉션하는 웹 응용 프로그램 외부, 악성 URL로 사용자를 리디렉션하기와 훼손 될 수 있습니다. 이 변조 열려 리디렉션 공격을 이라고 합니다.

응용 프로그램 논리를 지정 된 URL로 리디렉션합니다, 때마다와 리디렉션 URL이 손상 되지 않았음을 확인 해야 합니다. ASP.NET MVC 1.0와 ASP.NET MVC 2에 대 한 기본 AccountController에에서 사용 되는 로그인은 열 리디렉션 공격에 취약 합니다. 다행히 ASP.NET MVC 3 Preview의 수정 사항이 사용 하 여 기존 응용 프로그램을 업데이트 하기 쉽습니다.

이 취약점을 이해 하려면 살펴보겠습니다 로그인 리디렉션 기본 ASP.NET MVC 2 웹 응용 프로그램 프로젝트에서 작동 하는 방식. 이 응용 프로그램에서 [Authorize] 특성이 있는 컨트롤러 작업을 방문 하는 권한이 없는 사용자를를 리디렉션합니다 /Account/LogOn 보기. /Account/LogOn이 이동이 성공적으로 로그인 한 후 원래 요청 된 URL로 사용자를 반환 수 있도록 returnUrl querystring 매개 변수를 포함 됩니다.

아래 스크린샷에서 /Account/LogOn을 리디렉션에 로그인 하지 않은 경우 /Account/ChangePassword 보기에 액세스 하려고 발생 알 수 있습니다. ReturnUrl = %2fAccount 2fChangePassword% 2f%입니다.

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**그림 01**: 열려 리디렉션을 로그인 페이지

이후 ReturnUrl querystring 매개 변수 유효성이 검사 되지 않습니다 하면 공격자가 열려 리디렉션 공격을 수행 하 고 매개 변수를 모든 URL 주소를 삽입 하도록 수정할 수 있습니다. 이 증명 하려면 ReturnUrl 매개 변수를 수정할 수 있을 [http://bing.com](http://bing.com)결과 로그인 URL을 갖게 됩니다/계정/로그온,? ReturnUrl = http://www.bing.com/ 합니다. 성공적으로 사이트에 로그인 하 되 면 우리는 리디렉션됩니다 [http://bing.com](http://bing.com)합니다. 이후이 리디렉션이 유효성이 검사 되지 않습니다 대신 사용자 속일 하려는 악성 사이트를 가리킬 수 있습니다.

### <a name="a-more-complex-open-redirection-attack"></a>더 복잡 한 열기 리디렉션 공격

열기 리디렉션 공격은 특히 위험에 취약해 우리 특정 웹 사이트에 로그인 하려고 하는 공격자가 알기 때문에 [피싱 공격](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)합니다. 예를 들어 공격자가 암호를 캡처할 하기 위해 웹 사이트 사용자에 게 악성 전자 메일을 보낼 수 있습니다. 업그레이드 되었으며 수정 사이트에서 어떻게 작동할 것에서 살펴보겠습니다. (Note: 라이브 업그레이드 되었으며 수정 사이트가 열려 리디렉션 공격 으로부터 보호 하도록 업데이트 되었습니다.)

첫째, 공격자가 보내는 링크 로그인 페이지 리디렉션을 위조 된 페이지를 포함 하는 업그레이드 되었으며 수정에:

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

Note 반환 URL 단어 dinner에서 "n" 없는 nerddiner.com 가리킵니다. 이 예제에서는 공격자가 제어 하는 도메인입니다. 위의 링크에 액세스 했습니다 합법적인 NerdDinner.com 로그인 페이지로 이동 하 했습니다.

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**그림 02**: 열려 리디렉션을 업그레이드 되었으며 수정 로그인 페이지

ASP.NET MVC AccountController 로그온 작업을 올바르게에 로그인 하겠습니다 returnUrl querystring 매개 변수에서 지정 된 URL로 우리 리디렉션합니다. 이 경우에 공격자가 입력 한 URL을는 [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)합니다. We're 매우 워치 매우 높습니다이 알 수 없습니다 공격자가 있는지 확인 하려면 신중 하 게 되지 않았기 때문에 특히 하지 않는 한 해당 위조 된 페이지 합법적인 로그인 페이지와 동일 하 게 보입니다. 이 로그인 페이지에 다시 로그인 하는 오류 메시지 요청에 포함 됩니다. 어 색 하 게 us, 암호를 입력 했 해야 했습니다.

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**그림 03**: 위조 업그레이드 되었으며 수정 로그인 화면

에서는 사용자 이름과 암호를 다시 입력, 위조 된 로그인 페이지 정보를 저장 하 고 합법적인 NerdDinner.com 사이트에 다시 보내는 합니다. 이 시점에서 NerdDinner.com 사이트가 이미 인증 us, 위조 된 로그인 페이지는 해당 페이지에 직접 리디렉션할 수 있도록 합니다. 최종 결과는 공격자가 사용자 이름과 암호를 및 하 나와 것을 알지는입니다.

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>AccountController 로그온 액션에 취약 한 코드를 살펴보면

ASP.NET MVC 2 응용 프로그램에서 로그온 작업에 대 한 코드는 다음과 같습니다. 성공적으로 로그인 할 때 컨트롤러 돌아갑니다 리디렉션을 returnUrl 참고 합니다. 유효성 검사가 수행 되지 returnUrl 매개 변수에 대해 수행 되 고 있는지 확인할 수 있습니다.

**1 –에서 ASP.NET MVC 2 로그온 작업 나열`AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

이제 ASP.NET MVC 3 로그온 동작의 변경 내용을 살펴 보겠습니다. 이 코드는 returnUrl 매개 변수 이름의 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 유효성을 검사 하도록 변경 되었습니다 `IsLocalUrl()`합니다.

**2 –에서 ASP.NET MVC 3 로그온 작업 나열`AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

반환 URL 매개 변수 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 유효성을 검사 하도록 변경 되었습니다이 `IsLocalUrl()`합니다.

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>ASP.NET MVC 1.0 및 MVC 2 보호 응용 프로그램

IsLocalUrl() 도우미 메서드를 추가 하 고 returnUrl 매개 변수 유효성을 검사 하는 로그온 동작을 업데이트 하 여 기존 ASP.NET MVC 1.0 우리의 및 2 응용 프로그램에서 ASP.NET MVC 3 변경 내용 활용을 수행할 수 있습니다.

ASP.NET 웹 페이지 응용 프로그램에서 실제로 호출에서이 유효성 검사와 System.Web.WebPages 메서드로 UrlHelper IsLocalUrl() 메서드도 사용 됩니다.

**3 – ASP.NET MVC 3 UrlHelper에서 IsLocalUrl() 메서드를 나열합니다.`class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

IsUrlLocalToHost 메서드 목록 4와 같이 실제 유효성 검사 논리를 포함 합니다.

**4 – System.Web.WebPages RequestExtensions 클래스에서 IsUrlLocalToHost() 메서드를 나열합니다.**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

ASP.NET MVC 1.0 우리의 또는 2 응용 프로그램에서 IsLocalUrl() 메서드는 AccountController를 추가 합니다 바꿔야 하는데이 가능 하다 면 별도 도우미 클래스에 추가 하는 것이 좋습니다. 해 드립니다 두 약간 변경 IsLocalUrl()의 ASP.NET MVC 3 버전에는 AccountController 내 작동할 수 있도록 합니다. 먼저 변경 합니다 것 public 메서드에서 전용 메서드를 컨트롤러의 public 메서드를 컨트롤러 작업으로 액세스할 수 있으므로 합니다. 둘째, 응용 프로그램 호스트에 대해 URL 호스트를 확인 하는 호출이 수정 합니다. 호출에서 로컬 RequestContext를 활용 필드 UrlHelper 클래스에 있습니다. 대신이 사용 합니다. RequestContext.HttpContext.Request.Url.Host,이 사용 합니다 했습니다. Request.Url.Host 합니다. 다음 코드는 ASP.NET MVC 1.0 및 2 응용 프로그램 컨트롤러 클래스와 함께 사용 하기 위해 수정 된 IsLocalUrl() 메서드를 보여 줍니다.

**MVC 컨트롤러 클래스에 수정 될 목록 5 – IsLocalUrl() 메서드**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

IsLocalUrl() 메서드 이면 했으므로 다음 코드에 나와 있는 것 처럼 returnUrl 매개 변수 유효성을 검사 하 여 로그온 작업에서 호출할 수 있습니다.

**6-업데이트 된 로그온 방법 returnUrl 매개 변수를의 유효성을 검사 목록**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

이제 열려 리디렉션 공격 외부 반환 URL을 사용 하 여 로그인을 시도 하 여 테스트할 수 있습니다. 다음을 사용해 봅시다/계정/로그온? ReturnUrl http://www.bing.com/ 다시 = 합니다.

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**그림 04**: 업데이트 된 로그온 동작을 테스트

성공적으로 로그인 한 후에 외부 URL이 아닌 Home/Index 컨트롤러 동작 리디렉션됩니다 했습니다.

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**그림 05**: 열기 리디렉션 공격을 막을 수

## <a name="summary"></a>요약

열기 리디렉션 공격 리디렉션 Url은 응용 프로그램에 대 한 URL에 매개 변수로 전달 될 때 발생할 수 있습니다. 리디렉션 공격 으로부터 보호 하기 위해 코드를 포함 하는 서식 파일은 ASP.NET MVC 3을 엽니다. 일부 수정 하지 않고도 ASP.NET MVC 1.0 및 2 응용 프로그램에이 코드를 추가할 수 있습니다. ASP.NET 1.0 및 2 응용 프로그램에 로그인 할 때 열린 리디렉션 공격을 방지 하기 위해 IsLocalUrl() 메서드를 추가 하 고 로그온 동작에서 returnUrl 매개 변수 유효성 검사.
