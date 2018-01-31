---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: "웹 페이지 및 ASP.NET MVC에서 XSRF/CSRF 방지 | Microsoft Docs"
author: Rick-Anderson
description: "교차 사이트 요청 위조 (XSRF 또는 CSRF 라고도 함)가 악의적인 웹 사이트는 interacti 영향을 줄 수는 그에 따라 웹 호스팅 응용 프로그램에 대 한 공격 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2013
ms.topic: article
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 6cf30daa7ed966b11405cec715c5bc803b567249
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>웹 페이지 및 ASP.NET MVC에서 XSRF/CSRF 방지
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 교차 사이트 요청 위조 (XSRF 또는 CSRF 라고도 함)가 악의적인 웹 사이트 클라이언트 브라우저와 해당 브라우저에서 신뢰할 수 있는 웹 사이트 간의 상호 작용 영향을 줄 수는 그에 따라 웹 호스팅 응용 프로그램에 대 한 공격입니다. 이러한 공격은 웹 브라우저가 웹 사이트에 대 한 모든 요청에 자동으로 인증 토큰을 전송할 때문에 가능 합니다. 정식는 예: ASP 인증 쿠키를 수 있습니다. NET의 폼 인증 티켓입니다. 그러나 이러한 공격에 의해 모든 영구 인증 메커니즘 (예: Windows 인증, 기본 및 등)을 사용 하는 웹 사이트를 지정할 수 있습니다.
> 
> XSRF 공격은 피싱 공격과에서 다릅니다. 피싱 공격 희생자에서 상호 작용을 필요로 합니다. 피싱 공격에서는 악의적인 웹 사이트는 대상 웹 사이트를 모방 됩니다 및 상태가 발생 하 여 공격자에 게 중요 한 정보를 제공 하도록 속일 됩니다. XSRF 공격에서 종종 희생자에서 필요한 조작은 하지 않습니다. 대신, 공격자가 자동으로 대상 웹 사이트에 모든 관련 쿠키를 전송 하는 브라우저에 신뢰 됩니다.
> 
> 자세한 내용은 참조는 [웹 응용 프로그램 보안 프로젝트 열기](https://www.owasp.org/index.php/Main_Page)(OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))합니다.


## <a name="anatomy-of-an-attack"></a>공격 분석

XSRF 공격을 진행 하기 위해 사용자를 일부 온라인 뱅킹 트랜잭션을 수행 하는 것이 좋습니다. 이 사용자는 먼저 WoodgroveBank.com 고에 있는 로그 지점을 응답 헤더 포함 됩니다. 자신의 인증 쿠키 방문:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

인증 쿠키는 세션 쿠키, 때문에 자동으로 지워집니다 브라우저에서 브라우저 프로세스가 종료 될 때입니다. 그러나 그 전 까지는 브라우저에서는 자동으로 포함 WoodgroveBank.com 각 요청과 함께 쿠키입니다. 사용자가 이제 하므로 그녀 은행 사이트의 양식을 작성 하 고 브라우저는 서버에이 요청을 다른 계정으로 1000 달러를 전송 하려는:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

이 작업 (통화 트랜잭션 시작 함) 부작용을 사용 하므로 은행 사이트는이 작업을 시작 하기 위해 HTTP POST를 요구 하도록 선택 했습니다. 서버 요청에서 인증 토큰을 읽고, 현재 사용자의 계정 번호를 찾고, 확인 자금 부족 존재 한 다음 대상 계정으로 트랜잭션을 시작 합니다.

완료를 온라인 뱅킹 her, 사용자 은행 사이트 밖으로 이동 하 고는 웹에서 다른 위치를 열어 봅니다. 내에 포함 된 페이지에 다음 태그를 포함 하는 해당 사이트 – fabrikam.com – 중 하나는 &lt;iframe&gt;:

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

다음이이 요청에 대 한 브라우저를 사용 하면:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

공격자가 사용자 대상 웹 사이트에 대 한 유효한 인증 토큰이 있을 수 있습니다 하 고 Javascript의 작은 조각을 사용 하 여 대상 사이트에 HTTP POST를 자동으로 확인 하려면 브라우저는 그녀 악용 됩니다. 인증 토큰이 여전히 유효한 경우 은행 사이트 공격자가 선택한의 계정으로 $250의 전송을 시작 됩니다.

### <a name="ineffective-mitigations"></a>비효율적인 완화

위의 시나리오에 WoodgroveBank.com SSL을 통해 액세스 하 고 있던 한 SSL 인증 쿠키에 있다는 점에서 되었음을 방지할 수 있었던 공격을 차단 하는 데 충분을 보면 흥미롭습니다. 공격자는 지정할 수는 [URI 체계](http://en.wikipedia.org/wiki/URI_scheme) (https)에 &lt;양식&gt; 요소 및 브라우저 쿠키 만료 되지 않은 사이트에 보내는 대상으로 이러한 쿠키는 URI와 일치를 계속 의도 한 대상의 구성표입니다.

하나는 사용자 단순히 하지 방문 하 여 신뢰할 수 없는 사이트를 방문 하는 온라인 안전 하 게 유지를 활용 하 여 신뢰할 수 있는 사이트에만 주장 수 합니다. 이 어느 정도 가능성이 있지만 불행히도이 충고 불가능 한 항상 합니다. 아마도 사용자 "신뢰" 지역 뉴스 사이트 ConsolidatedMessenger 합니다. ConsolidatedMessenger.com 및이 되는 대신, 사이트 방문 되었지만 해당 사이트를 통해 공격자가 동일한 fabrikam.com에서 실행 되 던 코드 조각을 삽입할 수 있는 XSS 취약성을 있습니다.

들어오는 요청 권한이 있는지 확인할 수 있습니다는 [Referer 헤더로](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 도메인을 참조 합니다. 이렇게 하면 실수로 제 3 자 도메인에서 제출 된 요청 중지 됩니다. 그러나 일부 사용자 개인 정보 보호를 위해 브라우저의 참조 페이지 헤더가 사용 하지 않도록 설정 하 고 공격자가 희생자에 특정 보안 되지 않은 소프트웨어가 설치 되어 있는 경우 해당 헤더를 스푸핑할 경우가 수 있습니다. 확인 하 고 [Referer 헤더로](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) XSRF 공격을 방지 하는 안전한 방법으로 간주 되지 않습니다.

## <a name="web-stack-runtime-xsrf-mitigations"></a>웹 스택 런타임 XSRF 완화

ASP.NET 웹 스택 런타임에서의 변형을 사용 하 여 [동기화 장치 토큰 패턴이](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)_Prevention_Cheat_Sheet#General_Recommendation:_Synchronizer_Token_Pattern) XSRF 공격 으로부터 보호 하기 위해 합니다. 일반적인 형태의 동기화 장치 토큰 패턴은 두 개의 ANTI-XSRF 토큰 (인증 토큰) 외에도 각 HTTP POST를 사용 하 여 서버에 제출 되: 쿠키를 지정 하 고 양식 값으로 다른 토큰을 두 개 있습니다. ASP.NET 런타임에 의해 생성 된 토큰 값이 결정적 또는 공격자가 예측 가능한있지 않습니다. 토큰을 전송할 때 서버에서 두 토큰 비교 검사를 통과 하는 경우에 계속 진행 하는 요청을 허용 합니다.

XSRF 요청 확인 *세션 토큰* HTTP 쿠키로 저장 되 고 현재 페이로드에서 다음 정보를 포함 합니다.

- 임의 128 비트 식별자로 구성 된 보안 토큰입니다.   
 다음 이미지는 Internet Explorer F12 개발자 도구와 함께 표시 XSRF 요청 확인 세션 토큰을 표시: (이 현재 구현 되며 제목, 변경 될 가능성이 합니다.)

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*필드 토큰이* 으로 저장 되는 `<input type="hidden" />` 페이로드에서 다음 정보를 포함 하 고:

- 로그인 한 사용자의 사용자 이름 (인증) 하는 경우입니다.
- 제공 하는 모든 추가 데이터는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)합니다.

ANTI-XSRF 토큰의 페이로드가 암호화 되 고 서명, 토큰을 검사 하려면 도구를 사용 하는 경우 사용자 이름을 볼 수 없습니다. 웹 응용 프로그램은 ASP.NET 4.0을 대상으로 지정 하는 경우 암호화 서비스에 의해 제공 되는 [MachineKey.Encode](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx) 루틴입니다. 웹 응용 프로그램은 ASP.NET 4.5를 대상으로 하거나 더 높은, 암호화 서비스에서 제공 때는 [MachineKey.Protect](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110)) 더 나은 성능, 확장성 및 보안을 제공 하는 루틴입니다. 자세한 내용은 다음 블로그 게시물을 참조 하십시오.

- [ASP.NET 4.5 암호화 향상 된 기능, pt입니다. 1](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4.5 암호화 향상 된 기능, pt입니다. 2](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4.5 암호화 향상 된 기능, pt입니다. 3](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>토큰 생성

ANTI-XSRF 토큰을 생성 하려면 호출는 [ @Html.AntiForgeryToken ](https://msdn.microsoft.com/library/dd470175.aspx) MVC 뷰에서 메서드 또는 @AntiForgery.GetHtmlRazor 페이지에서 (). 런타임은 다음 단계를 수행 다음 합니다.

1. 현재 HTTP 요청 ANTI-XSRF 세션 토큰에 이미 포함 되어 있는 경우 (ANTI-XSRF 쿠키 \_ \_RequestVerificationToken), 보안 토큰에서 추출 됩니다. HTTP 요청에는 ANTI-XSRF 세션 토큰 또는 보안 토큰의 추출이 실패할 경우 새 임의 ANTI-XSRF 토큰 생성 됩니다.
2. ANTI-XSRF 필드 토큰이 현재 로그인 한 사용자의 id (1) 위의 단계에서 보안 토큰을 사용 하 여 생성 됩니다. (사용자 id 확인에 대 한 자세한 내용은 참조는  **[특별 한 지원 사용 하는 시나리오](#_Scenarios_with_special)**  아래 섹션.) 또한 경우는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) 은 구성 런타임에서 호출 됩니다는 [GetAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx) 메서드 field 토큰에는 반환 된 문자열을 포함 합니다. (참조는  **[구성 및 확장성](#_Configuration_and_extensibility)**  한 자세 합니다.)
3. 새 ANTI-XSRF 토큰 단계 (1)에서 생성 된, 새 세션 토큰 및 포함 하기 위해 만들어집니다 아웃 바운드 HTTP 쿠키 컬렉션에 추가 됩니다. 단계 (2)에서 필드 토큰이에 래핑됩니다는 `<input type="hidden" />` 요소, 그리고이 HTML 태그의 반환 값이 됩니다 `Html.AntiForgeryToken()` 또는 `AntiForgery.GetHtml()`합니다.

## <a name="validating-the-tokens"></a>토큰 유효성 검사

들어오는 ANTI-XSRF 토큰의 유효성을 검사 하는 개발자가 포함 된 [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx) 그녀의 MVC 동작 또는 컨트롤러 또는 그녀는 호출에 특성 `@AntiForgery.Validate()` 그녀의 Razor 페이지에서. 런타임에서 다음 단계를 수행 합니다.

1. 들어오는 세션 토큰 및 필드 토큰이 읽고 ANTI-XSRF 토큰 각에서 추출 합니다. ANTI-XSRF 토큰 생성 루틴에서 단계 (2) 당 동일 해야 합니다.
2. 현재 사용자가 인증 되 면 그녀의 사용자 이름 필드 토큰에 저장 된 사용자 이름으로 비교 됩니다. 사용자 이름의 일치 해야 합니다.
3. 경우는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 구성 된 런타임 호출 해당 *ValidateAdditionalData* 메서드. 이 메서드는 부울 값을 반환 해야 *true*합니다.

유효성 검사는 성공 요청은 계속 진행 하도록 허용 합니다. 유효성 검사가 실패할 경우 프레임 워크에서 throw 한 *HttpAntiForgeryException*합니다.

## <a name="failure-conditions"></a>오류 상태

ASP.NET 웹 스택 런타임 v 2와 함께 시작 하는 모든 *HttpAntiForgeryException* 중에 throw 되는 유효성 검사에는 무엇이 잘못 되었는지에 대 한 자세한 정보가 포함 됩니다. 현재 정의 된 오류 조건에 해당 합니다.

- 세션 토큰 또는 폼 토큰 요청에 나타나지 않습니다.
- 세션 토큰 또는 폼 토큰을 읽을 수 있습니다. 이 가장 일반적인 원인은 다른 버전의 ASP.NET 웹 스택 런타임 또는 팜의를 실행 하는 팜에서 여기서는 &lt;machineKey&gt; Web.config의 요소는 컴퓨터 간에 다릅니다. 둘 중 한 ANTI-XSRF 토큰을 변조 하 여이 예외를 강제로 Fiddler와 같은 도구를 사용할 수 있습니다.
- 세션 토큰 및 필드 토큰 교체 되었습니다.
- 세션 토큰 및 필드 토큰이 일치 하지 않는 보안 토큰을 포함 합니다.
- Field 토큰 내에 포함 된 사용자 이름에는 현재 로그인 한 사용자의 사용자 이름을 일치 하지 않습니다.
- *[IAntiForgeryAdditionalDataProvider.ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)*  메서드 반환 *false*합니다.

ANTI-XSRF 시설 토큰 생성 또는 유효성 검사를 하는 동안 추가 검사 수행 될 수 있습니다 하며 이러한 검사 중에 오류가 발생 하는 예외가 발생할 수 있습니다. 참조는 [WIF / ACS / 클레임 기반 인증](#_WIF_ACS) 및  **[구성 및 확장성](#_Configuration_and_extensibility)**  섹션에서 자세한 정보.

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>특별 한 지원 사용 하는 시나리오

### <a name="anonymous-authentication"></a>익명 인증

ANTI-XSRF 시스템에 "익명"가 정의 되어 있는 사용자로 익명 사용자에 대 한 특별 한 지원이 포함 되어 있는 *IIdentity.IsAuthenticated* 속성에서 반환 *false*합니다. XSRF 보호 (사용자가 인증) 전에 로그인 페이지 및 응용 프로그램 사용 하는 경우는 메커니즘이 아닌 다른 사용자 지정 인증 체계를 제공 하는 것이 시나리오로 *IIdentity* 사용자를 식별 하 합니다.

이러한 시나리오를 지원 하려면 세션 및 필드 토큰 보안 토큰에는 128 비트 임의로 생성 된 불투명 식별자로 결합 된 점에 유의 하십시오. 이 보안 토큰이 이므로 익명 식별자의 용도 효과적으로 역할은 사이트를 탐색 하면서 그녀는 개별 사용자의 세션을 추적 하기 위해 사용 됩니다. 빈 문자열은 위에서 설명한 생성 및 유효성 검사 루틴에 대 한 사용자 이름 대신 사용 됩니다.

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF / ACS / 클레임 기반 인증

일반적으로 *IIdentity* .NET Framework에 기본 제공 하는 클래스 속성에는 있는 *IIdentity.Name* 특정 응용 프로그램 내에서 특정 사용자를 고유 하 게 식별 하는 충분 합니다. 예를 들어 *FormsIdentity.Name* (이 해당 데이터베이스에 따라 모든 응용 프로그램에 대해 고유) 구성원 데이터베이스에 저장 된 사용자 이름을 반환 *WindowsIdentity.Name* 반환는 사용자 및 등의 정규화 된 도메인 id입니다. 이러한 시스템 제공 뿐만 아니라 인증; 또한 *식별* 응용 프로그램에 사용자입니다.

클레임 기반 인증 반면에 필요는 없습니다 특정 사용자를 식별 합니다. 대신,는 *ClaimsPrincipal* 및 *ClaimsIdentity* 유형은의 집합과 연결 *클레임* 인스턴스를 개별 클레임 수 있는 "18 + 세 is" 또는 " 관리자가 다른 사용자 계정으로 "입니다. 사용자를 확인 했으면 반드시 않은 이후 런타임에서 사용할 수 없습니다는 *ClaimsIdentity.Name* 이 특정 사용자에 대 한 고유 식별자로 속성입니다. 팀에서 실제 예에 표시 여기서 *ClaimsIdentity.Name* 반환 *null*, 대화명 (표시) 이름을 반환 또는 그렇지 않은 경우 고유 식별자로 사용 하기에 적합 하지 않은 문자열을 반환 합니다. 에 대 한 사용자입니다.

사용 하는 다양 한 클레임 기반 인증을 사용 하 여 배포 [Azure 액세스 제어 서비스](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) (ACS) 특히 합니다. ACS 개별 개발자가 구성할 수 있습니다 *id 공급자* (ADFS를 Microsoft 계정 공급자와 같은 OpenID 공급자 등의 yahoo! 등)를 반환 하는 id 공급자 및 *식별자이름지정*. 이러한 이름 식별자 개인 식별이 가능한 정보 (PII) 전자 메일 주소 처럼 포함 되거나 같은 식별자 PPID (Private Personal)를 실적과 될 수 없습니다. 그럼에도 불구 하 고 (id 공급자, 이름 식별자) 튜플 충분히 역할을 특정 사용자에 대 한 적절 한 추적 토큰 그녀 ASP.NET 웹 스택 런타임이 생성 하는 경우 사용자 이름 대신 튜플을 사용할 수 있도록 사이트를 검색 하는 동안 및 ANTI-XSRF 필드 토큰 유효성을 검사 합니다. Id 공급자와의 이름 식별자에 대 한 특정 Uri는:

- `http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

(이 [ACS doc 페이지](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx) 대 한 자세한 정보.)

를 생성 하거나 유효성을 검사 하는 토큰 ASP.NET 웹 스택 런타임 런타임 시 시도 합니다 형식에 바인딩:

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35`(SDK에 대 한는 WIF.)
- `System.Security.Claims.ClaimsIdentity`(.NET 4.5) 용.

이러한 형식은 존재 한 경우 현재 사용자의 *IIIIdentity* 유형 중 하나 구현 또는 서브 클래스 (id 공급자, 이름 식별자) ANTI-XSRF 시설 사용, 생성 하는 경우 사용자 이름 대신 튜플 및 토큰의 유효성 검사. 이러한 튜플이 있는 경우 사용 중인 특정 클레임 기반 인증 메커니즘을 이해 하려면 ANTI-XSRF 시스템을 구성 하는 방법을 개발자에 게 설명 하는 오류와 함께 요청이 실패 합니다. 참조는  **[구성 및 확장성](#_Configuration_and_extensibility)**  한 자세 합니다.

### <a name="oauth--openid-authentication"></a>OAuth / OpenID 인증

마지막으로, ANTI-XSRF 시설에 OAuth 또는 OpenID 인증을 사용 하는 응용 프로그램에 대 한 특별 한 지원이 있습니다. 이 지원은 추론 기반: 경우 현재 *IIdentity.Name* 다음 사용자 이름 비교를 수행할 수는 http:// 또는 https://로 시작 기본 OrdinalIgnoreCase 비교자 보다는 서 수는 비교자를 사용 하 여 합니다.

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>구성 및 확장성

경우에 따라 개발자 ANTI-XSRF 생성 및 유효성 검사 동작 더 엄격한 제어를 원할 수 있습니다. 예를 들어 웹 페이지 및 MVC 도우미 기본 동작은 자동으로 응답에 HTTP 쿠키를 추가 하는 것이 좋은 경우 아마도 및 개발자는 토큰을 다른 위치를 유지 하려는 경우가 있을 수 있습니다. 이 지원 하기 위해 두 개의 Api 존재 합니다.

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

*GetTokens* 는 기존 XSRF 요청 확인 세션 토큰 (null 일 수 있음)을 입력 하는 메서드 사용으로 및 새 XSRF 요청 확인 세션 토큰 및 필드 토큰이 생성으로 출력 합니다. 토큰은; 장식이 없는 단순히 불투명 문자열 *formToken* 값 예를 들어 바꿈되지에 &lt;입력&gt; 태그입니다. *newCookieToken* 값 null 일 수 있습니다;이 문제가 발생 하면 *oldCookieToken* 값이 유효한 지 그리고 없는 새 응답 쿠키를 설정 해야 합니다. 호출자 *GetTokens* 은 모든 필요한 응답 쿠키를 유지 하거나 필요한 모든 태그; 생성는 *GetTokens* 메서드 자체 응답 부작용으로 영향을 주지 것입니다. *유효성 검사* 메서드는 들어오는 세션을 사용 하 고 필드 토큰에 대해 앞에서 언급 한 유효성 검사 논리를 실행 합니다.

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

개발자는 응용 프로그램에서 ANTI-XSRF 시스템을 구성할 수 있습니다\_시작 합니다. 구성은은 프로그래밍 방식입니다. 정적 속성 *AntiForgeryConfig* 종류는 다음과 같습니다. 대부분의 사용자 클레임을 사용 하 여 UniqueClaimTypeIdentifier 속성을 설정 해야 합니다.

| **Property** | **설명** |
| --- | --- |
| **AdditionalDataProvider** | [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 토큰 생성 하는 동안 추가 데이터를 제공 하 고 토큰 유효성 검사 중 추가 데이터를 많이 사용 합니다. 기본값은 *null*합니다. 자세한 내용은 참조는 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 섹션. |
| **CookieName** | ANTI-XSRF 세션 토큰을 저장 하는 데 사용 되는 HTTP 쿠키의 이름을 지정 하는 문자열입니다. 이 값을 설정 하지 않으면 경우 응용 프로그램의 배포 된 가상 경로에 따라 이름이 자동으로 생성 됩니다. 기본값은 *null*합니다. |
| **RequireSsl** | ANTI-XSRF 토큰 SSL 보안 채널을 통해 전송 될 필요한 지 여부를 결정 하는 부울입니다. 이 값이 *true*이 고, 자동으로 생성 된 쿠키는 "secure" 플래그를 설정 하 고, 고 ANTI-XSRF Api는 SSL을 통해 전송 되지 않습니다는 요청 내에서 호출 된 경우 throw 됩니다. 기본값은 *false*입니다. |
| **SuppressIdentityHeuristicChecks** | ANTI-XSRF 시스템 클레임 기반 id에 대 한 지원을 비활성화 해야 하는지 여부를 결정 하는 부울입니다. 이 값이 *true*, 시스템이 있다고 가정 합니다 *IIdentity.Name* 고유한 사용자 식별자로 사용 하기에 적합 하 고는 특별 한 경우 하려고 *IClaimsIdentity*또는 *ClClaimsIdentity* 에 설명 된 대로 [WIF / ACS / 클레임 기반 인증](#_WIF_ACS) 섹션. 기본값은 `false`입니다. |
| **UniqueClaimTypeIdentifier** | 클레임 유형 나타내는 문자열은 고유한 사용자 식별자로 사용 하기에 적합 합니다. 이 값이 설정 및 현재 *IIdentity* 하 여 지정 된 클레임 기반, 시스템이 형식의 클레임을 추출 하는 *UniqueClaimTypeIdentifier*, 해당 값이 사용 됩니다 대신 사용자의 사용자 이름 필드 토큰을 생성 하는 경우입니다. 클레임 유형이 없는 경우 시스템은 요청을 거부 합니다. 기본값은 *null*, 시스템 (id 공급자, 이름 식별자)을 사용 해야 함을 나타내는 튜플 앞에서 설명한 대로 사용자의 사용자 이름 대신 합니다. |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

*[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)*  형식에서는 개발자가 각 토큰의 추가 데이터를 왕복 하 여 ANTI-XSRF 시스템의 동작을 확장할 수 있습니다. *GetAdditionalData* 될 때마다 메서드는 필드 토큰이 생성 되 고 반환 값은 생성 되는 토큰 내에 포함 되어 있습니다. 구현 자가이 메서드에서 타임 스탬프, nonce, 또는 그녀 하지 않고자 한다면 다른 모든 값을 반환할 수 있습니다.

마찬가지로,는 *ValidateAdditionalData* 될 때마다 메서드는 필드 토큰의 유효성을 검사 하 고 토큰 내에 포함 된 "데이터 추가" 문자열 메서드에 전달 됩니다. 루틴 또는 기타 검사 nonce 원하는 논리, 유효성 검사 루틴 (토큰을 만들 때 저장 된 시간에 대해 현재 시간을 확인 하는 중)에서 시간 초과 구현할 수 없습니다.

## <a name="design-decisions-and-security-considerations"></a>디자인 결정 사항 및 보안 고려 사항

세션 및 필드 토큰을 연결 하는 보안 토큰은 기술적으로 필요한 경우에 XSRF 공격에 대 한 익명 / 인증 되지 않은 사용자가 보호 하려고 합니다. 하나로 (아마도 쿠키의 형태로 제출) 자체 인증 토큰을 사용할 수는 사용자가 인증 될 때 동기화 프로그램의 절반 토큰 쌍입니다. 그러나 인증 되지 않은 사용자가 로그인 페이지를 보호 하는 데 유효한 시나리오가 있습니다 않으며 ANTI-XSRF 논리 항상 생성 하 고 인증 된 사용자에 대해서도 보안 토큰을 확인 하 여 간단한 만들어졌습니다. 또한 필드 토큰이 설정 또는 세션 토큰에 해결 하기 위해 공격자에 대 한 다른 장애물 것 추측 공격자가 손상 되는 몇 가지 추가 보호를 제공지 않습니다.

개발자가 여러 응용 프로그램이 단일 도메인에서 호스팅되는 경우 주의 해야 합니다. 예를 들어 있지만 *example1.cloudapp.net* 및 *example2.cloudapp.net* 는 서로 다른 호스트의 모든 호스트 간의 암시적 트러스트 관계가 있는  *\*. cloudapp.net에* 도메인입니다. 이 암시적 신뢰 관계가 [통해 다른 사용자의 쿠키에 영향을 신뢰할 수 없는 호스트](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) (AJAX 요청을 제어 하는 동일 원본 정책 반드시에 적용 되지 않습니다 HTTP 쿠키). 사용자 이름 필드 토큰에 포함 되어 있으므로 악의적인 하위 도메인은 세션 토큰을 덮어쓸 수 있는 경우에 됩니다 하지 사용자에 대 한 유효한 필드 토큰을 생성할 수 있다는 점에서 ASP.NET 웹 스택 런타임 몇 가지 완화를 제공 합니다. 그러나 이러한 환경에서 호스팅되는 경우 기본 제공 ANTI-XSRF 루틴 여전히 없습니다 방어 세션 하이재킹 또는 XSRF 로그인 합니다.

ANTI-XSRF 루틴 현재 로부터 보호 되지 않는 [clickjacking](https://www.owasp.org/index.php/Clickjacking)합니다. Clickjacking 으로부터 자신을 방어 하는 응용 프로그램 수 쉽게 수행할 보내기는 X 프레임 옵션: SAMEORIGIN 헤더는 각 응답 합니다. 이 헤더는 모든 최신 브라우저에서 지원 됩니다. 자세한 내용은 참조는 [IE 블로그](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx), [SDL 블로그](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx), 및 [OWASP](https://www.owasp.org/index.php/Clickjacking)합니다. 이 공격 으로부터 응용 프로그램은 자동으로 보호 되도록 자동으로이 헤더를 설정할 웹 페이지 ANTI-XSRF 도우미 및 ASP.NET 웹 스택 런타임 일부 향후 릴리스에서 make MVC 수 있습니다.

웹 개발자는 자신의 사이트 XSS 공격에 노출 되지 않도록 하려면 계속 해야 합니다. XSS 공격은 매우 강력 하 고 성공적으로 악용은 XSRF 공격에 대 한 ASP.NET 웹 스택 런타임을 방어 페이지 나누기입니다.

## <a name="acknowledgment"></a>승인

[@LeviBroderick](https://twitter.com/LeviBroderick)누가 작성 ASP.NET 보안 코드의 대부분이 정보의 대부분 합니다.
