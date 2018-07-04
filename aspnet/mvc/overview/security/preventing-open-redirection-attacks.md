---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 오픈 리디렉션 공격 방지 (C#) | Microsoft Docs
author: jongalloway
description: 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 오픈 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다. 이 자습서에는 적용 된 변경 내용을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: 27921e23d38d34332b81fb85dcc795c8f9ff0352
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375472"
---
<a name="preventing-open-redirection-attacks-c"></a>오픈 리디렉션 공격 방지 (C#)
====================
[Jon Galloway](https://github.com/jongalloway)

> 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 오픈 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다. 이 자습서는 ASP.NET MVC 3에서 AccountController에 적용 된 변경 내용을 설명 하 고에 기존 ASP.NET MVC 1.0 및 2 응용 프로그램에서 이러한 변경 내용을 적용 하는 방법을 보여 줍니다.


## <a name="what-is-an-open-redirection-attack"></a>오픈 리디렉션 공격 란?

잠재적으로 쿼리 문자열 또는 폼 데이터와 같은 요청을 통해 지정 된 URL로 리디렉션하는 모든 웹 응용 프로그램 외부, 악성 URL에 사용자를 리디렉션할 사용 하 여 변경할 수 있습니다. 이 변조 오픈 리디렉션 공격을 이라고 합니다.

때마다 응용 프로그램 논리를 지정 된 URL로 리디렉션되면 리디렉션 URL을 사용 하 여 손상 되지 않았는지를 확인 해야 합니다. ASP.NET MVC 1.0 및 ASP.NET MVC 2 모두에 대 한 기본 AccountController에에서 사용 된 로그인은 엽니다 리디렉션 공격에 취약 합니다. 다행 스럽게도 ASP.NET MVC 3 미리 보기에서 수정 사항을 사용 하려면 기존 응용 프로그램을 업데이트 하기 쉽습니다.

취약성을 이해 하려면 살펴보겠습니다 로그인 리디렉션 기본 ASP.NET MVC 2 웹 응용 프로그램 프로젝트에서 작동 하는 방법. 이 응용 프로그램에서 [Authorize] 특성을 갖는 컨트롤러 작업을 방문 하는 동안 권한이 없는 사용자로 리디렉션됩니다 /Account/LogOn 보기. /Account/LogOn이 이동이 성공적으로 로그인 한 후 원래 요청 된 URL에 사용자를 반환 될 수 있도록 returnUrl 쿼리 문자열 매개 변수가 포함 됩니다.

아래 스크린샷에서 /Account/LogOn을 로그인 하지 않은 경우 /Account/ChangePassword 뷰에 액세스 하려고 하면 리디렉션에 발생는 알 수 있습니다? ReturnUrl = %2fAccount %2fChangePassword %2f입니다.

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**그림 01**:는 열린 리디렉션 사용 하 여 로그인 페이지

ReturnUrl 쿼리 문자열 매개 변수는 유효성이 검사 되지 때문 공격자 오픈 리디렉션 공격을 수행 하는 매개 변수에 모든 URL 주소를 삽입할 수정할 수 있습니다. 이 보여 주기 위해 ReturnUrl 매개 변수를 수정할 수 있습니다 [ http://bing.com ](http://bing.com)이므로 결과 로그인 URL은 / 계정/로그온? ReturnUrl =<http://www.bing.com/>합니다. 성공적으로 사이트에 로그인 시에서는 리디렉션됩니다 [ http://bing.com ](http://bing.com)합니다. 이 리디렉션은 유효성이 검사 되지 않습니다 하므로 사용자를 시도 하는 악성 사이트를 대신 가리킬 수 있습니다.

### <a name="a-more-complex-open-redirection-attack"></a>더 복잡 한 오픈 리디렉션 공격

오픈 리디렉션 공격은 취약 하 게 특정 웹 사이트에 로그인 하려고 하는 공격자가 알고 있기 때문에 특히 위험을 [피싱 공격](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)합니다. 예를 들어 공격자가 암호를 캡처할 하려고 웹 사이트 사용자에 게 악성 전자 메일을 보낼 수 있습니다. NerdDinner 사이트의 작동 원리에 대해 살펴보겠습니다. (Note: 오픈 리디렉션 공격 으로부터 보호 하기 위해 라이브 NerdDinner 사이트 변경 되었습니다.)

첫째, 공격자 우리 링크를 보내는 NerdDinner가 위조 된 페이지로 리디렉션을 포함 하는 로그인 페이지:

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

반환 URL을 가리키는 nerddiner.com "n" 없는 단어 dinner에서 note 합니다. 이 예에서이 공격자가 제어 하는 도메인. 위의 링크에 액세스 하는 경우 합법적인 NerdDinner.com 로그인 페이지로 이동 하는 것입니다.

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**그림 02**:는 오픈 리디렉션으로 NerdDinner 로그인 페이지

제대로 로그인에서는 ASP.NET MVC AccountController 로그온 작업 returnUrl 쿼리 문자열 매개 변수에서 지정한 URL에 우리를 리디렉션합니다. 즉 공격자가 입력 하는 URL이이 예에서 [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn)합니다. 우리는 매우 워치 가능성이 매우 높하지 않습니다 알 수 있습니다 따라서 공격자가 있는지 신중 하 게 되지 않았기 때문에 특히 하지 않는 한 해당 위조 된 페이지 합법적인 로그인 페이지와 동일 하 게 보입니다. 이 로그인 페이지에서는 다시 로그인 요청 오류 메시지를 포함 합니다. 괴로운 us,에서는 암호를 잘못 입력 했 해야 합니다.

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**그림 03**: 위조 된 NerdDinner 로그인 화면

에서는 사용자 이름 및 암호를 다시 입력, 하는 경우 위조 된 로그인 페이지 정보를 저장 하 고 합법적인 NerdDinner.com 사이트로 다시 우리를 보냅니다. 이 시점에서 NerdDinner.com 사이트에 이미 인증 us, 위조 된 로그인 페이지는 해당 페이지에 직접 리디렉션할 수 있도록 합니다. 최종 결과 사용자 이름 및 암호를 공격자가 하는 한 것에 인식 되지 됩니다.

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>AccountController 로그온 동작에서 취약 한 코드를 살펴보면

ASP.NET MVC 2 응용 프로그램에서 로그온 작업에 대 한 코드는 다음과 같습니다. 로그인에 성공 하면 컨트롤러 돌아갑니다 리디렉션을 반환 된 Url을 참고 합니다. ReturnUrl 매개 변수에 대해 유효성을 검사 하지 수행될지를 볼 수 있습니다.

**목록 1 –에서 ASP.NET MVC 2 로그온 작업 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

이제 ASP.NET MVC 3 로그온 동작 변경에 살펴보겠습니다. 이 코드 라는 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 returnUrl 매개 변수 유효성 검사로 변경 되었습니다 `IsLocalUrl()`합니다.

**2 –에서 ASP.NET MVC 3 로그온 작업 나열 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

이 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 반환 URL 매개 변수 유효성 검사로 바뀌었습니다 `IsLocalUrl()`합니다.

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>및 보호 하 여 ASP.NET MVC 1.0 MVC 2 응용 프로그램

IsLocalUrl() 도우미 메서드를 추가 하 고 returnUrl 매개 변수 유효성을 검사 하려면 로그온 작업을 업데이트 하 여이 기존 ASP.NET MVC 1.0 및 2 응용 프로그램에서 ASP.NET MVC 3 변경 내용 활용을 걸릴 수 있습니다 했습니다.

이 유효성 검사로 System.Web.WebPages 메서드가 실제로 호출 UrlHelper IsLocalUrl() 메서드도 ASP.NET Web Pages 응용 프로그램에서 사용 됩니다.

**3 – ASP.NET MVC 3 UrlHelper에서 IsLocalUrl() 메서드를 나열합니다. `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

IsUrlLocalToHost 메서드 목록 4에 나와 있는 것 처럼 실제 유효성 검사 논리를 포함 합니다.

**4-IsUrlLocalToHost() 메서드에서 System.Web.WebPages RequestExtensions 클래스 나열**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

ASP.NET MVC 1.0 또는 2 응용 프로그램에서 IsLocalUrl() 메서드는 AccountController를 추가한 않지만 가능 하면 별도 도우미 클래스를 추가 하는 것이 좋습니다. AccountController 내에서 작동할 수 있도록 IsLocalUrl()의 ASP.NET MVC 3 버전 두 작은 변경을 수행 됩니다. 먼저에서는 변경 고 public 메서드에서 개인 메서드에 컨트롤러 작업으로 컨트롤러의 공용 메서드에 액세스할 수 있으므로 합니다. 둘째, 응용 프로그램 호스트에 대 한 URL 호스트를 확인 하는 호출이 수정 합니다. 호출 로컬 RequestContext를 활용할 수 있도록 UrlHelper 클래스의 필드입니다. 대신이 사용 합니다. RequestContext.HttpContext.Request.Url.Host,이 항목이 사용 됩니다. Request.Url.Host 합니다. 다음 코드는 ASP.NET MVC 1.0 및 2 응용 프로그램 컨트롤러 클래스 사용에 대 한 수정 된 IsLocalUrl() 메서드를 보여줍니다.

**5-IsLocalUrl() 메서드를 나열 하는 사용할 수 있도록 수정 하는 MVC 컨트롤러 클래스를 사용 하 여**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

IsLocalUrl() 메서드 내부에는 이제 다음 코드 에서처럼 returnUrl 매개 변수 유효성을 검사 하 여 로그온 작업에서 호출할 수 했습니다.

**6-returnUrl 매개 변수 유효성을 검사 하는 업데이트 된 로그온 메서드를 나열 합니다.**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

이제 오픈 리디렉션 공격 외부 반환 URL을 사용 하 여 로그인을 시도 하 여 테스트할 수 있습니다. /Account/LogOn 사용해 보겠습니다. ReturnUrl =<http://www.bing.com/> 다시 합니다.

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**그림 04**: 업데이트 된 로그온 작업 테스트

성공적으로 로그인 한 후에 외부 URL이 아닌 Home/Index 컨트롤러 작업 리디렉션됩니다 했습니다.

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**그림 05**: 패 오픈 리디렉션 공격

## <a name="summary"></a>요약

오픈 리디렉션 공격 리디렉션 Url은 응용 프로그램에 대 한 URL에 매개 변수로 전달 될 때 발생할 수 있습니다. 템플릿은 으로부터 보호 하기 위해 코드를 포함 하는 ASP.NET MVC 3 리디렉션 공격을 엽니다. ASP.NET MVC 1.0 및 2 응용 프로그램에 일부 수정 하 여이 코드를 추가할 수 있습니다. ASP.NET 1.0 및 2 응용 프로그램에 로그인 할 때 오픈 리디렉션 공격을 방지 하기 IsLocalUrl() 메서드를 추가 하 고 로그온 작업 returnUrl 매개 변수를 확인 합니다.
