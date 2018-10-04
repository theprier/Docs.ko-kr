---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: ASP.NET MVC 및 웹 페이지에서 XSRF/CSRF 방지 | Microsoft Docs
author: Rick-Anderson
description: 교차 사이트 요청 위조 (XSRF 또는 CSRF 라고도 함)은 악의적인 웹 사이트는 interacti 영향을 줄 수는 여기서 웹 호스팅 응용 프로그램에 대 한 공격 하는 중...
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 5db661cccc58d1101f95091b069ab5cbfe78a378
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577940"
---
<a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>ASP.NET MVC 및 웹 페이지에서 XSRF/CSRF 방지
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 교차 사이트 요청 위조 (XSRF 또는 CSRF 라고도 함)은 악의적인 웹 사이트는 클라이언트 브라우저와 해당 브라우저에서 신뢰할 수 있는 웹 사이트 간의 상호 작용에 영향을 줄 가능해 집니다 웹 호스팅 응용 프로그램에 대 한 공격입니다. 이러한 공격은 웹 사이트로 웹 브라우저 인증 토큰이 모든 요청에 자동으로 보내기 때문에 가능 합니다. 정식 예로 ASP와 같은 인증 쿠키가 있습니다. NET의 폼 인증 티켓입니다. 그러나 웹 사이트 (예: Windows 인증, 기본 및 등) 영구적 인증 메커니즘을 사용 하는 이러한 공격 대상이 될 수 있습니다.
> 
> XSRF 공격은 피싱 공격과 구분 됩니다. 피싱 공격 피해자의 상호 작용을 필요로 합니다. 피싱 공격, 악의적인 웹 사이트는 대상 웹 사이트를 모방 하 고 피해자는 공격자에 게 중요 한 정보를 제공 속일 합니다. XSRF 공격에서는 종종 피해자의 필요한 없습니다 상호 작용이입니다. 대신, 공격자가 자동으로 대상 웹 사이트에 모든 관련 쿠키를 전송 하는 브라우저에서 신뢰 됩니다.
> 
> 자세한 내용은 참조는 [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page)(OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))합니다.


## <a name="anatomy-of-an-attack"></a>공격 분석

XSRF 공격을 단계별로 사용자를 일부 온라인 뱅킹 트랜잭션을 수행 하는 것이 좋습니다. 이 사용자는 WoodgroveBank.com 및에서는 로그 응답 헤더는 인증 쿠키를 포함 하는 데이 시점에서 먼저 방문:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

인증 쿠키는 세션 쿠키 이기 때문에 자동으로 지워집니다 브라우저에서 브라우저 프로세스가 종료 되 면 합니다. 그러나 그 전 까지는 브라우저 자동으로 포함 됩니다 WoodgroveBank.com 각 요청과 함께 쿠키입니다. 이제 사용자가 자신이 은행 사이트의 양식을 작성 하 고 브라우저 요청이 서버에 다른 계정에 1000 달러를 전송 하려는:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

이 작업에 부작용 (현금 트랜잭션 시작 함)에 있으므로 은행 사이트는이 작업을 시작 하기 위해 HTTP POST를 요구 하도록 선택 했습니다. 서버 요청에서 인증 토큰을 읽습니다, 그리고 현재 사용자의 계정 번호 조회, 자금이 충분 존재 하는 대상 계정에 트랜잭션 시작을 확인 합니다.

온라인 완료를 은행 만듭니다 사용자 은행 사이트에서 떨어진 이동 하 고 웹에서 다른 위치를 방문. 내에 포함 된 페이지에 다음 태그를 포함 하는 – fabrikam.com – 이러한 사이트 중 하나는 &lt;iframe&gt;:

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

그러면이이 요청에 브라우저를 발생 시킵니다.

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

공격자가 악용 사용자 대상 웹 사이트에 대 한 유효한 인증 토큰이 있을 수 있습니다 하 고 자신이 사용 하 여 Javascript의 작은 코드 조각을 브라우저가 자동으로 대상 사이트에 HTTP POST를 만듭니다. 인증 토큰이 여전히 유효한 경우 은행 사이트 공격자의 계정으로 250 달러의 전송을 시작 됩니다.

### <a name="ineffective-mitigations"></a>비효율적인 완화

위 시나리오에서 WoodgroveBank.com SSL을 통해 액세스 하 고 있던 하는 SSL 전용 인증 쿠키가 팩트 없음을 공격을 차단할 수 있는 충분 한 흥미로운 것입니다. 공격자는 지정할 수는 [URI 체계](http://en.wikipedia.org/wiki/URI_scheme) (https)에 만듭니다 &lt;폼&gt; 요소와 브라우저 계속 전송 됩니다 만료 되지 않은 쿠키 대상 사이트에 이러한 쿠키는 URI와 일치 의도 한 대상의 체계입니다.

주장할 수 사용자 하지 신뢰할 수 있는 사이트 온라인 안전 하 게 유지 하는 데 도움이 됩니다만 방문으로 신뢰할 수 없는 사이트를 방문 하 고 단순히 해야 합니다. 몇 가지 사실, 이지만 불행히도이 권장 사항은 사실상 불가능 항상. 아마도 사용자 "신뢰" 지역 뉴스 사이트 ConsolidatedMessenger 합니다. ConsolidatedMessenger.com 및 이동 하는 대신, 사이트 방문 있지만 해당 사이트는 XSS 취약점으로 인 한 공격자가 fabrikam.com에서 실행 되는 코드의 같은 조각을 삽입할 수 있는 있습니다.

들어오는 요청이 있는지 확인할 수 있습니다는 [Referer 헤더](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 도메인을 참조 합니다. 타사 도메인에서 모르게 제출 된 요청이 중지 합니다. 그러나 일부 사용자 개인 정보 보호를 위해 브라우저의 Referer 헤더를 사용 하지 않도록 설정 하 고 공격자가 희생자 안전 하지 않은 특정 소프트웨어가 설치 되어 있으면 해당 헤더를 스푸핑할 경우에 따라 수 있습니다. 확인 합니다 [Referer 헤더](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) XSRF 공격을 방지 하는 보안 방법으로 간주 되지 않습니다.

## <a name="web-stack-runtime-xsrf-mitigations"></a>웹 스택 런타임 XSRF 완화

ASP.NET 웹 스택 런타임에서의 변형을 사용 하 여 [동기화 장치 토큰 패턴이](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)_Prevention_Cheat_Sheet#General_Recommendation:_Synchronizer_Token_Pattern) XSRF 공격 으로부터 보호 하기. 일반 동기화 장치 토큰 패턴의 형식은 두 ANTI-XSRF 토큰 (인증 토큰) 외에도 각 HTTP POST를 사용 하 여 서버에 제출 되는: 쿠키 및 형식 값으로 다른 하나의 토큰입니다. ASP.NET 런타임에 의해 생성 된 토큰 값이 결정적 또는 공격자가 예측 가능한있지 않습니다. 토큰을 제출 되 면 서버에서 토큰이 모두 비교 확인을 전달 하는 경우에 계속 진행 하는 요청을 허용 합니다.

XSRF 요청 인증 *세션 토큰* 현재 해당 페이로드의 다음 정보를 포함 하는 HTTP 쿠키로 저장 됩니다.

- 구성 된 임의의 128 비트 식별자를 보안 토큰입니다.   
 다음 이미지에서는 Internet Explorer F12 개발자 도구를 사용 하 여 표시 XSRF 요청 확인 세션 토큰: (이 현재 구현 하며 제목은 변경 될 가능성이 훨씬.)

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*필드 토큰* 으로 저장 되는 `<input type="hidden" />` 페이로드는 다음 정보를 포함 하 고:

- 로그인 한 사용자의 사용자 이름 (인증) 하는 경우입니다.
- 제공한 모든 추가 데이터를 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)합니다.

ANTI-XSRF 토큰의 페이로드는 암호화 되 고 서명, 토큰을 검사 하려면 도구를 사용 하는 경우에 사용자를 볼 수 없습니다. 암호화 서비스에서 제공 하는 웹 응용 프로그램을 ASP.NET 4.0을 대상으로 하는 경우는 [MachineKey.Encode](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx) 루틴입니다. ASP.NET 4.5를 대상으로 웹 응용 프로그램 또는 더 높은 암호화 서비스에서 제공 하는 경우는 [MachineKey.Protect](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110)) 더 나은 성능, 확장성 및 보안을 제공 하는 루틴입니다. 자세한 내용은 다음 블로그 게시물을 참조 하세요.

- [ASP.NET 4.5의에서 향상 된 암호화 기능, (태평양 표준시)입니다. 1](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4.5의에서 향상 된 암호화 기능, (태평양 표준시)입니다. 2](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4.5의에서 향상 된 암호화 기능, (태평양 표준시)입니다. 3](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>토큰 생성

ANTI-XSRF 토큰을 생성 하기 위해 호출 된 [ @Html.AntiForgeryToken ](https://msdn.microsoft.com/library/dd470175.aspx) MVC 뷰에서 메서드 또는 @AntiForgery.GetHtmlRazor 페이지에서 (). 런타임에서 다음 단계를 수행 다음 됩니다.

1. 현재 HTTP 요청은 이미 ANTI-XSRF 세션 토큰을 포함 하는 경우 (ANTI-XSRF 쿠키 \_ \_RequestVerificationToken), 보안 토큰에서 추출 됩니다. ANTI-XSRF 세션 토큰을 HTTP 요청에 없으면, 보안 토큰의 추출이 실패할 경우 새 임의 ANTI-XSRF 토큰 생성 됩니다.
2. ANTI-XSRF 필드 토큰을 보안 토큰 (1) 위의 단계에서 현재 로그인 한 사용자의 id를 사용 하 여 생성 됩니다. (사용자 id를 확인 하는 방법은 참조 합니다 **[특별 한 지원 사용 하 여 시나리오](#_Scenarios_with_special)** 섹션 아래.) 또한 경우는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) 은 구성, 런타임에서 호출 됩니다 해당 [GetAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx) 메서드 필드 토큰에서 반환된 된 문자열을 포함 합니다. (참조를 **[구성 및 확장성](#_Configuration_and_extensibility)** 자세한 내용은 섹션입니다.)
3. 새 ANTI-XSRF 토큰 (1) 단계에서 생성 된 경우 새 세션 토큰을 포함 하기 위해 만들어지고 아웃 바운드 HTTP 쿠키 컬렉션에 추가 됩니다. 단계 (2)에서 필드 토큰에서 래핑될를 `<input type="hidden" />` 요소와이 HTML 태그의 반환 값이 됩니다 `Html.AntiForgeryToken()` 또는 `AntiForgery.GetHtml()`합니다.

## <a name="validating-the-tokens"></a>토큰 유효성 검사

들어오는 ANTI-XSRF 토큰의 유효성을 검사 하려면 개발자는 다음과 같이 포함 됩니다.는 [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx) 게 MVC 작업 또는 컨트롤러 그녀는 호출 특성 `@AntiForgery.Validate()` 그녀의 Razor 페이지에서. 런타임에서 다음 단계를 수행 합니다.

1. 들어오는 세션 토큰 및 필드 토큰을 읽고 각 ANTI-XSRF 토큰을 추출 합니다. ANTI-XSRF 토큰을 생성 하는 루틴의 단계 (2) 당 동일 해야 합니다.
2. 현재 사용자가 인증 되 면 자신의 사용자 이름 토큰을 필드에 저장 된 사용자 이름으로 비교 됩니다. 사용자 이름 일치 해야 합니다.
3. 경우는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 구성 된 런타임 호출 해당 *ValidateAdditionalData* 메서드. 이 메서드는 부울 값을 반환 해야 *true*합니다.

유효성 검사는 성공 하는 경우 계속 하려면 요청은 허용 됩니다. 유효성 검사에 실패 하는 경우 프레임 워크를 throw 합니다는 *HttpAntiForgeryException*합니다.

## <a name="failure-conditions"></a>오류 상태

모든 ASP.NET 웹 스택 런타임에서 v2를 사용 하 여 시작 *HttpAntiForgeryException* 하는 동안 throw 되는 유효성 검사에는 무엇이 잘못 되었는지에 대 한 자세한 정보가 포함 됩니다. 현재 정의 된 오류 조건은 다음과 같습니다.

- 세션 토큰 또는 폼 토큰을 요청에 나타나지 않습니다.
- 세션 토큰 또는 폼 토큰을 읽을 수 없는 경우 이 가장 일반적인 원인은 일치 하지 않는 버전의 ASP.NET 웹 스택 런타임에서 또는 팜을 실행 하는 팜에서 여기서 합니다 &lt;machineKey&gt; Web.config의 요소는 컴퓨터 간에 다릅니다. ANTI-XSRF 토큰 중 하나를 사용 하 여 변조 하 여이 예외를 강제로 Fiddler와 같은 도구를 사용할 수 있습니다.
- 세션 토큰 및 필드 토큰을 전환 되었습니다.
- 세션 토큰 및 필드 토큰을 일치 하지 않는 보안 토큰을 포함 합니다.
- 필드 토큰 내에 포함 된 사용자 이름에는 현재 로그인 한 사용자의 사용자 이름을 일치 하지 않습니다.
- 합니다 *[IAntiForgeryAdditionalDataProvider.ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* 반환 하는 메서드 *false*합니다.

ANTI-XSRF 기능 토큰 생성 또는 유효성 검사 중 추가 검사를 수행할 수도 있습니다 및 이러한 검사 중에 오류가 throw 된 예외가 발생할 수 있습니다. 참조를 [WIF / ACS 클레임 기반 인증](#_WIF_ACS) 하 고 **[구성 및 확장성](#_Configuration_and_extensibility)** 자세한 내용은 섹션입니다.

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>특별 한 지원 사용 하 여 시나리오

### <a name="anonymous-authentication"></a>익명 인증

ANTI-XSRF 시스템에는 "anonymous"가 정의 되어 있는 사용자로 익명 사용자에 대 한 특별 한 지원이 포함 되어 있습니다. 여기서는 *IIdentity.IsAuthenticated* 속성이 반환 *false*합니다. XSRF 보호 (사용자가 인증) 전에 로그인 페이지 및 응용 프로그램 사용 하는 메커니즘을 이외의 사용자 지정 인증 체계를 제공 하는 것이 시나리오로 *IIdentity* 사용자를 식별 합니다.

이러한 시나리오를 지원 하려면 해당 세션 및 필드 토큰 128 비트 임의로 생성 된 불투명 식별자는 보안 토큰으로 가입 되어을 기억 하십시오. 이 보안 토큰이 익명 식별자의 용도로 효과적으로 사용 하도록 사이트를 이동 하는 개별 사용자의 세션 추적 하기 위해 사용 됩니다. 빈 문자열은 위에서 설명한 생성 및 유효성 검사 루틴에 대 한 사용자 이름 대신 사용 됩니다.

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF / ACS 클레임 기반 인증

일반적으로 *IIdentity* .NET Framework에 기본 제공 하는 클래스 속성에는 *IIdentity.Name* 는 특정 응용 프로그램 내에서 특정 사용자를 고유 하 게 식별 하는 데 충분 합니다. 예를 들어 *FormsIdentity.Name* (이 해당 데이터베이스에 따라 모든 응용 프로그램에 대해 고유) 멤버 자격 데이터베이스에 저장 된 사용자 이름을 반환 *WindowsIdentity.Name* 반환 합니다 사용자 및 등의 정규화 된 도메인 id입니다. 이러한 시스템 제공 인증 뿐 아니라 또한 *식별* 응용 프로그램에 대 한 사용자입니다.

클레임 기반 인증 일 경우 다른 한편으로 필요는 없습니다 특정 사용자를 식별 합니다. 대신 합니다 *ClaimsPrincipal* 하 고 *ClaimsIdentity* 종류의 집합과 연결 되 *클레임* 인스턴스를 개별 클레임 수 있는 "is 18 + 세 이상인" 또는 " 관리자가 "다른 사용자 계정으로 합니다. 사용자 식별 필요 하지 않은 이후 런타임에서 사용할 수 없습니다는 *ClaimsIdentity.Name* 이 특정 사용자에 대 한 고유 식별자로는 속성입니다. 팀에서 실제 예제에 표시 위치 *ClaimsIdentity.Name* 반환 *null*(표시) 친숙 한 이름을 반환, 그렇지 않으면 고유 식별자로 사용 하기에 적합 하지 않은 문자열을 반환 합니다. 설정 합니다.

사용 하는 다양 한 클레임 기반 인증을 사용 하는 배포 [Azure Access Control Service](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) (ACS) 특히 합니다. ACS 개별 개발자가 구성할 수 있습니다 *id 공급자* (ADFS, Microsoft 계정 공급자와 같은 OpenID 공급자 예: yahoo! 등), id 공급자를 반환 하 고 *식별자이름지정*. 이러한 이름 식별자는 전자 메일 주소와 같은 개인 식별이 가능한 정보 (PII)를 포함할 수 있습니다 또는 같은 개인 식별자 PPID (Private)를 익명화 될 수 있습니다. 그럼에도 불구 하 고 (id 공급자, 이름 식별자) 튜플 충분히 역할을 특정 사용자에 대 한 적절 한 추적 토큰 그녀는 ASP.NET 웹 스택 런타임에 생성 하는 경우 사용자 이름 대신 튜플을 사용할 수 있도록 사이트를 검색 하는 동안 및 ANTI-XSRF 필드 토큰 유효성을 검사 합니다. Id 공급자와 이름 식별자의 특정 Uri는 다음과 같습니다.

- `http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

(이 참조 하세요 [ACS doc 페이지](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx) 자세한.)

를 생성 하거나 토큰 유효성을 검사할 때 ASP.NET 웹 스택 런타임은 런타임에 시도 형식에 바인딩:

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` (SDK에 대 한는 WIF.)
- `System.Security.Claims.ClaimsIdentity` (예:.NET 4.5).

이러한 형식은 존재 하는 경우 현재 사용자의 *IIIIdentity* 구현 또는 서브 클래스 중 형식, ANTI-XSRF 기능 사용 (id 공급자, 이름 식별자)를 생성할 때 사용자 이름 대신 튜플 및 토큰의 유효성을 검사 합니다. 이러한 튜플이 있는 경우 요청에서 사용 하 여 특정 클레임 기반 인증 메커니즘을 이해 하려면 ANTI-XSRF 시스템을 구성 하는 방법을 개발자에 게 설명 하는 오류와 함께 실패 합니다. 참조 된 **[구성 및 확장성](#_Configuration_and_extensibility)** 자세한 내용은 섹션입니다.

### <a name="oauth--openid-authentication"></a>OAuth / OpenID 인증

마지막으로, ANTI-XSRF 시설에 OAuth 또는 OpenID 인증을 사용 하는 응용 프로그램에 대 한 특별 한 지원이 있습니다. 이 지원은 추론 기반: 경우 현재 *IIdentity.Name* username 비교를 수행할 수는 다음에 http:// 또는 https:// 로 시작 기본 OrdinalIgnoreCase 비교자를 사용 하지 않고 서 수는 비교자를 사용 하 여 합니다.

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>구성 및 확장성

경우에 따라 개발자는 엄격 하 게 제어할 ANTI-XSRF 생성 및 유효성 검사 동작을 원할 수 있습니다. 예를 들어, 아마도 응답에 HTTP 쿠키를 자동으로 추가 하는 MVC 및 Web Pages 도우미의 기본 동작, 아니며 개발자 토큰을 다른 위치를 유지 하려고 합니다. 이 지원 하기 위해 두 개의 Api가 있습니다.

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

합니다 *GetTokens* 으로 메서드는 입력을 기존 XSRF 요청 확인 세션 토큰 (null 일 수 있음) 및 새 XSRF 요청 확인 세션 토큰 및 필드 토큰을 생성으로 출력 합니다. 토큰은; 장식이 없는 단순히 불투명 문자열 합니다 *formToken* 값은 예를 들어에 래핑되지 않습니다는 &lt;입력&gt; 태그입니다. 합니다 *newCookieToken* 값이 문제가 발생 하는 경우 null; 일 수는 *oldCookieToken* 값 여전히 유효 하며 없는 새 응답 쿠키를 설정 해야 합니다. 호출자 *GetTokens* 는 모든 필요한 응답 쿠키를 유지 하거나; 필요한 태그를 생성 하는 일을 담당 합니다 *GetTokens* 메서드 자체은 부작용으로 응답을 변경 하지 않습니다. 합니다 *유효성 검사* 메서드는 들어오는 세션을 사용 하 고 필드 토큰에 대해 앞에서 언급 한 유효성 검사 논리를 실행 합니다.

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

개발자는 응용 프로그램에서 ANTI-XSRF 시스템을 구성할 수 있습니다\_시작 합니다. 구성은은 프로그래밍 방식입니다. 정적 속성 *AntiForgeryConfig* 종류는 다음과 같습니다. 대부분의 사용자 클레임을 사용 하 여 UniqueClaimTypeIdentifier 속성을 설정 하려고 합니다.

| **Property** | **설명** |
| --- | --- |
| **AdditionalDataProvider** | [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 토큰 생성 하는 동안 추가 데이터를 제공 하 고 토큰 유효성 검사 중 추가 데이터를 사용 합니다. 기본값은 *null*합니다. 자세한 내용은 참조는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 섹션입니다. |
| **CookieName** | ANTI-XSRF 세션 토큰은 저장에 사용 되는 HTTP 쿠키의 이름을 제공 하는 문자열입니다. 이 값을 설정 하지 않으면 하는 경우 응용 프로그램의 배포 된 가상 경로 기준으로 이름은 자동으로 생성 됩니다. 기본값은 *null*합니다. |
| **RequireSsl** | ANTI-XSRF 토큰 SSL 보안 채널을 통해 전송할 필요한 지 여부를 결정 하는 부울입니다. 이 값이 *true*, 자동으로 생성 된 쿠키는 "secure" 플래그를 설정 하 고, 있고 ANTI-XSRF Api는 SSL을 통해 전송 되지 않습니다 하는 요청 내에서 호출 된 경우 throw 됩니다. 기본값은 *false*입니다. |
| **SuppressIdentityHeuristicChecks** | ANTI-XSRF 시스템 클레임 기반 id에 대 한 지원을 비활성화 해야 하는지 여부를 결정 하는 부울입니다. 이 값이 *true*, 시스템은 가정 *IIdentity.Name* 고유한 사용자 식별자로 사용 하기에 적합 한 특수 사례를 시도 하지 것입니다 *IClaimsIdentity*나 *ClClaimsIdentity* 에 설명 된 대로 합니다 [WIF / ACS 클레임 기반 인증](#_WIF_ACS) 섹션입니다. 기본값은 `false`입니다. |
| **UniqueClaimTypeIdentifier** | 입력 클레임을 나타내는 문자열입니다는 고유한 사용자 식별자로 사용 하기에 적합 합니다. 이 값이 설정 및 현재 *IIdentity* 여 된 클레임을 기반으로 시스템 형식의 클레임을 추출 하려고 *UniqueClaimTypeIdentifier*, 및 해당 값이 사용 됩니다 대신 사용자의 사용자 이름 필드 토큰을 생성 하는 경우입니다. 클레임 유형이 없는 경우 시스템 요청에 실패 합니다. 기본값은 *null*, 시스템에서 (id 공급자, 이름 식별자)를 사용 해야 함을 나타내는 앞에서 설명한 대로 사용자의 사용자 이름 대신 튜플. |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

합니다 *[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* 형식 개발자가 각 토큰의 추가 데이터를 왕복 하 여 ANTI-XSRF 시스템의 동작을 확장할 수 있습니다. *GetAdditionalData* 때마다 메서드는 필드 토큰 생성 되 고 반환 값은 생성 된 토큰에 포함 되어 있습니다. 구현자는 타임 스탬프, nonce, 또는 하려는 그녀는 다른 값이 메서드에서 반환할 수 있습니다.

마찬가지로, 합니다 *ValidateAdditionalData* 때마다 메서드는 필드 토큰의 유효성을 검사 하 고 토큰에 포함 된 "데이터 추가" 문자열 메서드에 전달 됩니다. 유효성 검사 루틴 (토큰을 만들 때 저장 된 시간에 대해 현재 인하여) 시간 초과 구현할 수 있습니다, 그리고 루틴 또는 기타 검사 nonce 원하는 논리입니다.

## <a name="design-decisions-and-security-considerations"></a>설계 결정 사항 및 보안 고려 사항

세션 및 필드 토큰을 연결 하는 보안 토큰은 기술적으로 필요한 경우에 XSRF 공격에 대 한 익명 / 인증 되지 않은 사용자를 보호 하는 동안. 하나로 (아마도 쿠키의 형태로 제출) 자체 인증 토큰을 사용할 수 있습니다 사용자가 인증 될 때 동기화 프로그램의 절반 토큰 쌍입니다. 그러나 인증 되지 않은 사용자에서 로그인 페이지를 보호 하는 데에 유효한 시나리오가 있으며 항상 생성 하 고 보안 토큰 인증 된 사용자에 대해서도 유효성을 검사 하 여 ANTI-XSRF 논리는 간단 했습니다. 또한 필드 토큰을 설정 하거나 세션 토큰을 극복 하기 위해 공격자에 대 한 다른 장애물 것 추측 공격자가 손상 되는 몇 가지 추가 보호를 제공지 않습니다.

개발자가 여러 응용 프로그램은 단일 도메인에서 호스트 되는 경우 주의 해야 합니다. 예를 들어, 경우에 *example1.cloudapp.net* 및 *example2.cloudapp.net* 다른 호스트에서 모든 호스트 간에 암시적 신뢰 관계가 없는  *\*. cloudapp.net* 도메인입니다. 이 암시적 신뢰 관계가 [신뢰할 수 없는 다른 사용자의 쿠키에 적용할 수 있습니다](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) (AJAX 요청을 제어 하는 동일 원본 정책을 반드시에 적용 되지 않습니다 HTTP 쿠키). ASP.NET 웹 스택 런타임 악의적인 하위 도메인을 세션 토큰을 덮어쓰기 할 경우에 되지 것입니다 사용자에 대 한 유효한 필드 토큰을 생성할 수 있도록 사용자 이름 필드 토큰에 포함 되는 몇 가지 완화 조치를 제공 합니다. 그러나 이러한 환경에서 호스트 되는 경우 기본 제공 ANTI-XSRF 루틴은 여전히 없습니다 방어 세션 하이재킹 또는 XSRF 로그인 합니다.

ANTI-XSRF 루틴 현재 않습니다 하지 프로그램 방어 [클릭 재 킹](https://www.owasp.org/index.php/Clickjacking)합니다. 클릭 재 킹을 방어 자체 하려는 응용 프로그램 수 쉽게 보내서는 X 프레임 옵션: 각 응답과 SAMEORIGIN 헤더입니다. 이 헤더는 모든 최신 브라우저에서 지원 됩니다. 자세한 내용은 참조는 [IE 블로그](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx), [SDL 블로그](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx), 및 [OWASP](https://www.owasp.org/index.php/Clickjacking)합니다. 웹 페이지 ANTI-XSRF 도우미는 자동으로이 헤더를 설정할 응용 프로그램은 자동으로이 공격 으로부터 보호 하 고 일부 릴리스에서 확인 MVC에서 ASP.NET 웹 스택 런타임 수 있습니다.

웹 개발자 계속 해당 사이트 XSS 공격에 취약 하지 않는지 확인 해야 합니다. XSS 공격은 매우 강력한 및 공격 성공 XSRF 공격 으로부터 ASP.NET 웹 스택 런타임 방어 중단도 합니다.

## <a name="acknowledgment"></a>승인

[@LeviBroderick](https://twitter.com/LeviBroderick)에서이 정보 대량의 대부분 ASP.NET 보안 코드를 작성 합니다.
