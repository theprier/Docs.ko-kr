---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-vb
title: 사용자 기반 권한 부여 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 살펴보겠습니다 페이지에 대 한 액세스를 제한 하 고 다양 한 기술을 통해 페이지 수준 기능을 제한 합니다.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: bc937e9d-5c14-4fc4-aec7-440da924dd18
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: 263b421cbce68cbc9a596e40a6be4ff140edc0d4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835520"
---
<a name="user-based-authorization-vb"></a>사용자 기반 권한 부여 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_vb.pdf)

> 이 자습서에서는 살펴보겠습니다 페이지에 대 한 액세스를 제한 하 고 다양 한 기술을 통해 페이지 수준 기능을 제한 합니다.


## <a name="introduction"></a>소개

사용자 계정을 제공 하는 대부분의 웹 응용 프로그램 특정 방문자가 사이트 내의 특정 페이지에 액세스 하지 못하도록 제한 하는 부분에서 수행 합니다. 예를 들어 대부분의 온라인 보드 사이트-익명 및 인증-모든 사용자는 보드의 게시물을 볼 수 있지만 인증 된 사용자만 새 게시물을 작성 하는 웹 페이지를 방문할 수입니다. 및 특정 사용자 (또는 사용자의 특정 집합)에 액세스할 수 있는 관리 페이지가 있을 수 있습니다. 또한 페이지 수준 기능 사용자 간 별로 다를 수 있습니다. 게시물 목록을 볼 때에 인증 된 사용자가이 인터페이스를 익명 방문자에 게 사용할 수 없는 반면 각 게시물을 평가 하기 위한 인터페이스에 표시 됩니다.

ASP.NET을 사용 하면 쉽게 사용자 기반 권한 부여 규칙을 정의할 수 있습니다. 태그에 약간 `Web.config`, 특정 웹 페이지 또는 전체 디렉터리 에서만 사용자 지정 된 하위 집합에 액세스할 수 있도록 아래로 잠글 수 있습니다. 페이지 수준 기능이 수 설정 또는 해제 프로그래밍 방식 및 선언적 수단을 통해 현재 로그인 한 사용자를 기반으로 합니다.

이 자습서에서는 살펴보겠습니다 페이지에 대 한 액세스를 제한 하 고 다양 한 기술을 통해 페이지 수준 기능을 제한 합니다. 이제 시작 하겠습니다.

## <a name="a-look-at-the-url-authorization-workflow"></a>URL 권한 부여 워크플로 살펴보고

에 설명 된 대로 합니다 [ *는 폼 인증 개요* ](../introduction/an-overview-of-forms-authentication-vb.md) 자습서에서는 ASP.NET 런타임은 ASP.NET 리소스 요청 수명 주기 동안 이벤트 수가 발생에 대 한 요청을 처리 하는 경우. *HTTP 모듈* 는 요청 수명 주기에서 특정 이벤트에 대 한 응답에서 해당 코드가 실행 되는 관리 되는 클래스입니다. ASP.NET 여러 백그라운드에서 필수 작업을 수행 하는 HTTP 모듈이 함께 제공 됩니다.

이러한 HTTP 모듈 중 하나는 [ `FormsAuthenticationModule` ](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)합니다. 이전 자습서에서는 주요 기능에에서 설명 된 대로 `FormsAuthenticationModule` 현재 요청의 id를 결정 하는 것입니다. 이 쿠키에 되었거나 URL 내에 포함 된 폼 인증 티켓을 검사 하 여 이루어집니다. 이 식별 하는 동안 수행 합니다 [ `AuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)합니다.

또 다른 중요 한 HTTP 모듈을를 [ `UrlAuthorizationModule` ](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)에 대 한 응답으로 발생 하는 [ `AuthorizeRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx) (후 발생 하는 `AuthenticateRequest` 이벤트). `UrlAuthorizationModule` 구성 태그 검사 `Web.config` 현재 id를 지정된 된 페이지를 방문 하는 기관에 있는지 확인 합니다. 이 프로세스 라고 *URL 권한 부여*합니다.

살펴보겠습니다 1 단계에서에서 URL 권한 부여 규칙에 대 한 구문을 우선 보겠습니다을 파악 합니다 `UrlAuthorizationModule` 여부 요청이 승인 되는 여부에 따라 않습니다. 경우는 `UrlAuthorizationModule` 는 요청이 승인 되 아무 것도 수행 하 고 수명 주기를 통해 요청이 계속 확인 합니다. 그러나 요청이 *되지* 권한이 부여 하면 `UrlAuthorizationModule` 수명 주기를 중단 하 고 지시를 `Response` 반환할 개체를 [HTTP 401 권한이 없음](http://www.checkupdown.com/status/E401.html) 상태. 때문에이 HTTP 401 상태 클라이언트에 반환 되지 않고 폼 인증을 사용 하는 경우 경우 합니다 `FormsAuthenticationModule` 검색 상태는 HTTP 401을 수정 하는 [HTTP 302 리디렉션](http://www.checkupdown.com/status/E302.html) 로그인 페이지로 합니다.

그림 1은 ASP.NET 파이프라인의 워크플로 `FormsAuthenticationModule`, 및 `UrlAuthorizationModule` 권한이 없는 요청이 도착 하는 경우. 그림 1에 대 한 익명는 방문자에서 요청을 보여 줍니다 특히 `ProtectedPage.aspx`, 익명 사용자에 대 한 액세스를 거부 하는 페이지는 합니다. 방문자 익명 이므로 `UrlAuthorizationModule` 요청을 중단 하 고 HTTP 401 권한이 없음 상태를 반환 합니다. `FormsAuthenticationModule` 로그인 페이지로 302 리디렉션으로 401 상태를 변환 합니다. 사용자가 로그인 페이지를 통해 인증 되 면 그 리디렉션됩니다 `ProtectedPage.aspx`합니다. 이 이번에는 `FormsAuthenticationModule` 인증 티켓을 기반으로 사용자를 식별 합니다. 방문자가 인증 했으므로 `UrlAuthorizationModule` 페이지에 대 한 액세스를 허용 합니다.


[![폼 인증 및 권한 부여 워크플로 URL](user-based-authorization-vb/_static/image2.png)](user-based-authorization-vb/_static/image1.png)

**그림 1**: The 폼 인증 및 권한 부여 워크플로 URL ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image3.png))


그림 1에서는 익명 방문자는 익명 사용자에 게 제공 되지 않는 리소스에 액세스 하려고 할 때 발생 하는 상호 작용을 보여 줍니다. 이러한 경우 익명 방문자가 쿼리 문자열에 지정 된 방문 하려고 그녀는 페이지를 사용 하 여 로그인 페이지로 리디렉션됩니다. 사용자가 성공적으로 로그온 되 면 그녀 자동으로 리디렉션됩니다 다시 그녀 보고 하려고 처음 리소스입니다.

익명의 사용자 권한이 없는 요청이 이루어지면이 간단 하 게 워크플로와 무엇이 달라졌는지 알아야 방문자에 대 한 간단 하 고 이유. 하지만에서 유지 합니다 `FormsAuthenticationModule` 리디렉션됩니다 *모든* 인증된 된 사용자가 요청 하는 경우에 로그인 페이지로 사용자를 권한이 없는 합니다. 이 값은 인증된 된 사용자가 인증 기관에 그녀는 페이지를 방문 하려고 할 경우 혼란 스러운 사용자 환경에서 발생할 수 있습니다.

웹 사이트의 URL 권한 부여 규칙 구성 생각할 되도록 ASP.NET 페이지 `OnlyTito.aspx` Tito에만 액세스할 수 있습니다 되었습니다. 이제 Sam은 사이트를 방문, 로그온을 방문 하려고 imagine `OnlyTito.aspx`합니다. `UrlAuthorizationModule` 요청 수명 주기의 중단 되며 HTTP 401 권한이 없음 상태를 반환 하는 `FormsAuthenticationModule` 감지 하 고 Sam 로그인 페이지로 리디렉션합니다. Sam가 이미 로그인 되므로 그러나 그녀 궁금할 것 이유는 자신이 보낸 로그인 페이지로 돌아갈 수입니다. 그녀는 어떻게 해서든 로그인 자격 증명 된 손실 또는 잘못 된 자격 증명을 입력 한 노트 이유 수 있습니다. Sam 로그인 페이지에서 자격 증명을 해당 하는 경우 자신이 (다시) 기록 되며 리디렉션됩니다 `OnlyTito.aspx`합니다. `UrlAuthorizationModule` 에서 감지 하 고 Sam이이 페이지를 방문할 수 없습니다. 그녀는 로그인 페이지에 반환 됩니다.

그림 2에서는이 혼란 스 러 워크플로 보여 줍니다.


[![기본 워크플로 혼동 순환 시킬 수 있습니다.](user-based-authorization-vb/_static/image5.png)](user-based-authorization-vb/_static/image4.png)

**그림 2**:의 기본 워크플로 발생할 수 있습니다 혼동 주기 ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image6.png))


그림 2의 워크플로에 대부분의 컴퓨터 전문 방문자를 befuddle 신속 하 게 수 있습니다. 이 2 단계에서에서 주기를 혼동을 방지 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 현재 사용자가 특정 웹 페이지를 액세스할 수 있는지를 확인 하려면 두 가지 메커니즘을 사용 하는 ASP.NET: URL 권한 부여 및 권한 부여 파일입니다. 파일 권한 부여에 의해 구현 됩니다 합니다 [ `FileAuthorizationModule` ](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx), 기관 요청한 파일 Acl을 참조 하 여 결정 합니다. 파일 권한 부여에 Windows 계정에 적용 되는 권한 Acl 때문에 Windows 인증을 사용 하 여 가장 많이 사용 됩니다. Forms 인증을 사용 하는 경우 모든 운영 체제 및 파일 시스템 수준 요청 사이트를 방문 하는 사용자에 관계 없이 동일한 Windows 계정에 의해 실행 됩니다. 이 자습서 시리즈는 폼 인증에 중점을 두고, 이후 하지 논의할 파일 권한 부여 합니다.


### <a name="the-scope-of-url-authorization"></a>URL 권한 부여 범위

`UrlAuthorizationModule` 는 ASP.NET 런타임이 포함 된 코드를 관리 합니다. Microsoft의 버전 7 이전의 [인터넷 정보 서비스 (IIS)](https://www.iis.net/) 웹 서버에 IIS의 HTTP 파이프라인 및 ASP.NET 런타임의 파이프라인 간에 고유한 장벽 했습니다. 즉, IIS 6 및 이전 버전에서는 ASP 합니다. NET의 `UrlAuthorizationModule` IIS에서 ASP.NET 런타임에서 요청을 위임 하는 경우에 실행 합니다. 기본적으로 IIS HTML 페이지 및 CSS, JavaScript 및 이미지 파일 같은 정적 콘텐츠 자체를 처리 하 고만의 확장을 사용 하 여 페이지가 ASP.NET 런타임에서 요청을 전달한 `.aspx`, `.asmx`, 또는 `.ashx` 요청 합니다.

그러나 IIS 7 허용 통합된 IIS 및 ASP.NET에 대 한 파이프라인 합니다. 몇 가지 구성 설정을 사용 하 여 호출 하는 IIS 7을 설정할 수 있습니다 합니다 `UrlAuthorizationModule` 에 대 한 *모든* 요청, 즉 모든 형식의 파일에 대 한 URL 권한 부여 규칙을 정의할 수 있습니다. 또한 IIS 7 자체 URL 권한 부여 엔진을 포함합니다. ASP.NET 통합 및 IIS 7의 기본 URL 권한 부여 기능에 대 한 자세한 내용은 참조 하세요. [이해 IIS7 URL 권한 부여](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)합니다. Shahram Khosravi 책 복사본에 대 한 자세한 내용은 ASP.NET 및 IIS 7 통합, 승차 *Professional IIS 7 및 ASP.NET 통합 프로그래밍* (ISBN: 978 0470152539).

간단히 말해 IIS 7 이전 버전에서는 URL 권한 부여 규칙 ASP.NET 런타임에 의해 처리 되는 리소스에 적용만 됩니다. 이지만 IIS 7을 사용 하 여 IIS의 기본 URL 권한 부여 기능을 사용 하거나 ASP를 통합할 수 있습니다. NET의 `UrlAuthorizationModule` IIS의 HTTP 파이프라인에 모든 요청에이 기능을 확장 하므로 합니다.

> [!NOTE]
> 가지는 방법에 몇 가지 미묘 하면서도 중요 한 차이점이 ASP 합니다. NET의 `UrlAuthorizationModule` 및 IIS 7의 URL 권한 부여 기능을 권한 부여 규칙을 처리 합니다. 이 자습서는 IIS 7의 URL 권한 부여 기능이 나 하는 방법에 비해 권한 부여 규칙을 구문 분석의 차이점을 검사 하지는 `UrlAuthorizationModule`합니다. 이러한 항목에 대 한 자세한 내용은 MSDN 또는 IIS 7 설명서를 참조 [www.iis.net](https://www.iis.net/)합니다.


## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>1 단계: URL 권한 부여 규칙의 정의`Web.config`

`UrlAuthorizationModule` 권한 부여 또는 응용 프로그램의 구성에 정의 된 URL 권한 부여 규칙을 기준으로 하는 특정 id에 대 한 요청된 된 리소스에 대 한 액세스를 거부 여부를 결정 합니다. 권한 부여 규칙에 명시 되는 [ `<authorization>` 요소](https://msdn.microsoft.com/library/8d82143t.aspx) 형태로 `<allow>` 및 `<deny>` 자식 요소입니다. 각 `<allow>` 고 `<deny>` 자식 요소를 지정할 수 있습니다.

- 특정 사용자
- 사용자의 쉼표로 구분 된 목록
- 물음표 (?)로 표시 하는 모든 익명 사용자
- 모든 사용자에 별표를 가리키는 (\*)

다음 태그에서는 Tito 및 Scott 사용자 허용 및 거부 하는 다른 모든 URL 권한 부여 규칙을 사용 하는 방법을 보여 줍니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample1.xml)]

합니다 `<allow>` 요소-Tito 및 Scott-사용자 수를 정의 하는 동안 합니다 `<deny>` 요소에 지시 하는 *모든* 사용자는 거부 됩니다.

> [!NOTE]
> 합니다 `<allow>` 고 `<deny>` 요소는 역할에 대 한 권한 부여 규칙을 지정할 수도 있습니다. 이후 자습서에서 역할 기반 권한 부여를 살펴보겠습니다.


다음 설정을 Sam (익명 방문자 포함) 이외의 모든 사용자에 게 액세스 권한을 부여 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample2.xml)]

인증 된 사용자만을 허용 하려면 모든 익명 사용자에 대 한 액세스를 거부 하는 다음 구성을 사용 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample3.xml)]

내에서 권한 부여 규칙을 정의 하는 합니다 `<system.web>` 요소에 `Web.config` 웹 응용 프로그램의 ASP.NET 리소스 모두에 적용 합니다. 경우가 많습니다 응용 프로그램에 다른 섹션에 대 한 다른 권한 부여 규칙이 있습니다. 예를 들어 전자 상거래 사이트에서 모든 방문자 수 제품 목록을 살펴보고, 제품 사용 후기를 참조 하세요, 카탈로그 검색 등에입니다. 그러나 체크 아웃 또는 배송 기록을 관리 하는 페이지에 인증 된 사용자만 도달할 수 있습니다. 또한 사이트 관리자와 같은 사용자 선택 하 여 액세스할 수 있는 사이트의 부분 있을 수 있습니다.

ASP.NET을 사용 하면 쉽게 사이트에서 다른 파일 및 폴더에 대 한 다른 권한 부여 규칙을 정의할 수 있습니다. 루트 폴더에 지정 된 권한 부여 규칙 `Web.config` 파일 사이트에서 모든 ASP.NET 리소스에 적용 합니다. 그러나 이러한 기본 권한 부여 설정을 재정의할 수 있습니다 특정 폴더에 대 한 추가 하 여는 `Web.config` 사용 하 여는 `<authorization>` 섹션입니다.

인증 된 사용자만의 ASP.NET 페이지를 방문할 수 있도록 웹 사이트를 업데이트 해 보겠습니다는 `Membership` 폴더입니다. 추가 해야이 작업을 수행 하는 `Web.config` 파일을 `Membership` 폴더 익명 사용자를 거부 하려면 해당 권한 부여 설정을 합니다. 마우스 오른쪽 단추로 클릭 합니다 `Membership` 상황에 맞는 메뉴에서 새 항목 추가 메뉴를 선택 하 고 라는 새 웹 구성 파일을 추가 하는 솔루션 탐색기에서 폴더 `Web.config`합니다.


[![멤버 자격 폴더에 Web.config 파일 추가](user-based-authorization-vb/_static/image8.png)](user-based-authorization-vb/_static/image7.png)

**그림 3**: 추가 된 `Web.config` 파일을 합니다 `Membership` 폴더 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image9.png))


이 시점에서 프로젝트 두 개 포함 해야 `Web.config` 파일: 루트 디렉터리에서 하나에 하나는 `Membership` 폴더.


[![이제 응용 프로그램 Web.config 파일을 두 개 포함](user-based-authorization-vb/_static/image11.png)](user-based-authorization-vb/_static/image10.png)

**그림 4**: 사용자 응용 프로그램은 이제 포함 두 `Web.config` 파일 ([클릭 하 여 큰 이미지 보기](user-based-authorization-vb/_static/image12.png))


구성 파일 업데이트는 `Membership` 폴더는 익명 사용자에 대 한 액세스를 금지 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample4.xml)]

이것이 전부입니다!

이 변경은 테스트 하려면 브라우저에서 홈 페이지를 방문 하 고는 로그 아웃 해야 합니다. 모든 방문자를 허용 하는 것이 ASP.NET 응용 프로그램의 기본 동작 이므로 및 루트 디렉터리의 권한 부여 수정 만들지 않았기 때문 `Web.config` 파일에서는 수 익명 방문자는 루트 디렉터리에 파일을 참조 하세요.

왼쪽된 열에서 찾은 사용자 계정 만들기 링크를 클릭 합니다. 이 데는 `~/Membership/CreatingUserAccounts.aspx`합니다. 때문를 `Web.config` 파일을 `Membership` 익명 액세스를 금지 하는 권한 부여 규칙을 정의 하는 폴더는 `UrlAuthorizationModule` 요청을 중단 하 고 HTTP 401 권한이 없음 상태를 반환 합니다. `FormsAuthenticationModule` 로그인 페이지에 보내는 302 리디렉션 상태에이 수정 합니다. 페이지에서는 하 려 했던 액세스 확인 (`CreatingUserAccounts.aspx`)를 통해 로그인 페이지로 전달 되는 `ReturnUrl` querystring 매개 변수입니다.


[![URL 권한 부여 규칙 금지 익명 액세스를 로그인 페이지로 리디렉션됩니다 됩니다 것](user-based-authorization-vb/_static/image14.png)](user-based-authorization-vb/_static/image13.png)

**그림 5**: URL 권한 부여 규칙의 경우 익명 액세스를 금지, 이후 로그인 페이지로 리디렉션됩니다 것 ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image15.png))


리디렉션됩니다에서는 성공적으로 로그인 할 때를 `CreatingUserAccounts.aspx` 페이지입니다. 이 이번에는 `UrlAuthorizationModule` 익명 하는 것을 더 이상 없으므로 페이지에 대 한 액세스를 허용 합니다.

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>특정 위치에 URL 권한 부여 규칙을 적용합니다.

정의한 권한 부여 설정을 합니다 `<system.web>` 의 섹션 `Web.config` 디렉터리와 하위 디렉터리에 있는 ASP.NET 리소스 모두에 적용 (그렇지 않은 경우 다른 재정의 될 때까지 `Web.config` 파일). 경우에 따라 그러나 할에서 하나 또는 두 개의 특정 페이지를 제외 하 고 특정 권한 부여 구성이 지정 된 디렉터리의 모든 ASP.NET 리소스입니다. 추가 하 여 수행할 수 있습니다는 `<location>` 요소에서 `Web.config`, 권한 부여 규칙의 다른 파일을 가리키는 및 그 안에 해당 고유 권한 부여 규칙을 정의 합니다.

에서는 사용 하는 `<location>` 특정 리소스에 대 한 구성 설정을 재정의 하려면 보겠습니다만 Tito 방문할 수 있도록 권한 부여 설정을 사용자 지정할 요소 `CreatingUserAccounts.aspx`합니다. 이렇게 하려면 추가 `<location>` 요소를 `Membership` 폴더의 `Web.config` 파일을 다음과 같이 표시 되도록 해당 태그를 업데이트:

[!code-xml[Main](user-based-authorization-vb/samples/sample5.xml)]

`<authorization>` 요소에 `<system.web>` ASP.NET 리소스에 대 한 기본 URL 권한 부여 규칙을 정의 합니다 `Membership` 폴더와 하위 폴더입니다. `<location>` 요소를 사용 하면 특정 리소스에 대 한 이러한 규칙을 재정의 합니다. 위의 태그에는 `<location>` 요소 참조를 `CreatingUserAccounts.aspx` 페이지 및 해당 권한 부여 규칙 Tito, 가령 지정 하지만 거부 다른 모든 사용자.

이 권한 부여 변경을 테스트 하려면 익명 사용자로 웹 사이트를 방문 하 여 시작 합니다. 모든 페이지를 방문 하려고 하면 합니다 `Membership` 폴더와 같은 `UserBasedAuthorization.aspx`, `UrlAuthorizationModule` 요청을 거부 하도록 및 로그인 페이지로 리디렉션됩니다. 예를 들어 Scott, 다른 이름으로 로그인 한 후의 모든 페이지를 방문할 수 있습니다 합니다 `Membership` 폴더 *제외한* 에 대 한 `CreatingUserAccounts.aspx`합니다. 방문 하려고 `CreatingUserAccounts.aspx` 모든 사용자로 로그온 있지만 Tito 됩니다 무단된 액세스를 시도 하는 로그인 페이지로 다시 리디렉션됩니다.

> [!NOTE]
> 합니다 `<location>` 외부 구성 요소와 야 `<system.web>` 요소입니다. 별도 사용 해야 할 `<location>` 권한 부여 설정을 재정의 하려는 각 리소스에 대 한 요소입니다.


### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>확인 하는 방법을`UrlAuthorizationModule`권한 부여 규칙을 사용 하 여 액세스를 부여 하거나 거부할

`UrlAuthorizationModule` 여부 URL 권한 부여를 분석 하 여 특정 URL에 대 한 특정 id에 권한 부여 규칙 1에서 시작 하 고 아래쪽으로 작업 한 번에 하나씩 확인 합니다. 사용자는 액세스가 허용 되거나 거부, 경우에 따라 일치 항목에서 찾을 수는 일치 하는 항목이 즉시는 `<allow>` 또는 `<deny>` 요소입니다. <strong>일치 하는 항목이 없으면 사용자는 액세스 권한이 부여 됩니다.</strong> 결과적으로 액세스를 제한 하려는 경우 반드시 사용 하는 `<deny>` URL 권한 부여 구성에서 마지막 요소로 요소입니다. <strong>생략 하면는</strong><strong>`<deny>`</strong><strong>요소인 모든 사용자에 게 부여 됩니다.</strong>

사용 하는 프로세스를 더 잘 이해 하려면는 `UrlAuthorizationModule` 기관을 확인 하려면 예제를 고려해 보세요 URL 권한 부여 규칙을이 단계에서는 이전에 대해 살펴보았습니다. 첫 번째 규칙은는 `<allow>` Tito 및 Scott에 대 한 액세스를 허용 하는 요소입니다. 두 번째 규칙은 한 `<deny>` 모든 사용자에 게 액세스를 거부 하는 요소입니다. 익명 사용자를 방문 하는 경우는 `UrlAuthorizationModule` 를 요청 하 여 시작 되는 익명 Scott 또는 Tito? 두 번째 규칙에 진행 되므로 물론 대답은 아니요. 모든 사용자 집합에는 익명 기능 답변 이후 같습니다 예는 `<deny>` 규칙 적용에 배치 되 고 방문자 로그인 페이지로 리디렉션됩니다. 마찬가지로 Jisun 방문 하는 경우는 `UrlAuthorizationModule` 는 Jisun를 요청 하 여 시작 Scott 또는 Tito? 그렇지 않은 이므로 `UrlAuthorizationModule` 두 번째 질문을 모든 사용자 집합에는 Jisun 진행? 그녀는 그대로 유지 되므로도 액세스가 거부 됩니다. 마지막으로, Tito 방문 하는 경우 첫 번째 질문 야기는 `UrlAuthorizationModule` 받겠다고 긍정 대답 이므로 Tito 액세스 권한이 부여 됩니다.

이후는 `UrlAuthorizationModule` 프로세스를 덜 구체적인 앞에 야 구체적인 규칙이 반드시 권한 부여 규칙에서 하향식으로 모든 일치 항목에 중지 합니다. 즉, 다른 모든 인증 된 사용자를 허용 하지만 Jisun 및 익명 사용자를 금지 하는 권한 부여 규칙을 정의 하려면 가장 구체적인 규칙-하나에 영향을 주는 Jisun-로 시작 하는 설정한 다음 다른 모든 허용 된 덜 구체적인 규칙- 인증 된 사용자가 있지만 모든 익명 사용자를 거부 합니다. 다음 URL 권한 부여 규칙을 먼저 Jisun, 거부 및 다음 익명 사용자를 거부 하 여이 정책을 구현 합니다. Jisun 이외의 모든 인증 된 사용자는 액세스할 수 있으므로 이러한 `<deny>` 문은 일치 됩니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>2 단계: 인증, 권한 없는 사용자에 대 한 워크플로 해결

A Look URL 권한 부여 워크플로 섹션에서이 자습서의 앞부분에서 설명한 대로 권한이 없는 요청을 다소 언제 든 지,는 `UrlAuthorizationModule` 요청을 중단 하 고 HTTP 401 권한이 없음 상태를 반환 합니다. 401이 상태에 의해 수정 됩니다는 `FormsAuthenticationModule` 302에 사용자를 로그인 페이지로 전송 하는 상태를 리디렉션합니다. 이 워크플로 사용자가 인증 하는 경우에 모든 권한이 없는 요청에서 발생 합니다.

인증된 된 사용자를 로그인 페이지로 돌아가려면가 시스템에 이미 로그인 한 것 이므로 이러한 혼동을 줄 가능성이 높습니다. 약간의 작업을 사용 하 여 제한 된 페이지에 액세스를 시도 하기는 설명 하는 페이지에 무단으로 요청 하는 인증 된 사용자를 리디렉션하여이 워크플로 향상 시킬 수 했습니다.

웹 응용 프로그램의 루트 폴더에 새 ASP.NET 페이지를 만들어 시작 `UnauthorizedAccess.aspx`;이 페이지에 연결할 것을 잊지 마세요는 `Site.master` 마스터 페이지입니다. 이 페이지를 만든 후를 참조 하는 콘텐츠 컨트롤을 제거 합니다 `LoginContent` ContentPlaceHolder 마스터 페이지의 기본 콘텐츠 되도록 표시 됩니다. 다음으로, 즉 상황을 설명 하는 메시지를 추가 사용자가 보호 된 리소스에 액세스 하려고 합니다. 이러한 메시지를 추가한 후의 `UnauthorizedAccess.aspx` 페이지의 선언적 태그는 다음과 유사 합니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample7.aspx)]

이제 인증된 된 사용자가 권한이 없는 요청을 수행할 경우에 전송 되도록 워크플로 변경 해야 합니다 `UnauthorizedAccess.aspx` 로그인 페이지 대신 페이지입니다. 로그인 페이지에 인증 되지 않은 요청을 리디렉션하는 논리는의 전용 메서드에 포함 되어 있습니다를 `FormsAuthenticationModule` 클래스,에서는이 동작을 사용자 지정할 수 없습니다. 그러나 사용자를 리디렉션하는 로그인 페이지에 고유한 논리를 추가 수행할 수 있는, `UnauthorizedAccess.aspx`, 필요한 경우.

경우는 `FormsAuthenticationModule` 리디렉션하는 무단된 방문자 이름의 querystring에 요청 된, 무단 URL 로그인 페이지에 추가 `ReturnUrl`합니다. 예를 들어 권한이 없는 사용자가 방문 하려고 `OnlyTito.aspx`서 `FormsAuthenticationModule` 하도록 리디렉션하 `Login.aspx?ReturnUrl=OnlyTito.aspx`합니다. 따라서 포함 된 querystring 사용 하 여 인증된 된 사용자가 로그인 페이지에 도달 하면는 `ReturnUrl` 매개 변수, 그런 다음이 인증 되지 않은 사용자를 볼 권한이 없습니다 그녀는 페이지를 방문 하 여 방금 시도 했음을 알고 있습니다. 이러한 경우로 사용자를 리디렉션하 하려는 `UnauthorizedAccess.aspx`합니다.

이를 위해 다음 코드를 추가 하 여 로그인 페이지의 `Page_Load` 이벤트 처리기:

[!code-vb[Main](user-based-authorization-vb/samples/sample8.vb)]

위의 코드를 인증, 권한 없는 사용자를 리디렉션하는 `UnauthorizedAccess.aspx` 페이지입니다. 작업에서이 논리를 보려면 익명는 방문자와 사이트를 방문 하 고 왼쪽된 열에서 사용자 계정 만들기 링크를 클릭 합니다. 이 데는 `~/Membership/CreatingUserAccounts.aspx` 만 구성에서는 1 단계에서에서 Tito에 대 한 액세스를 허용 하는 페이지입니다. 익명 사용자는 금지 하므로 `FormsAuthenticationModule` 우리 로그인 페이지로 리디렉션합니다.

이 시점에서 우리는 익명 이므로 `Request.IsAuthenticated` 반환 `False` 것에 리디렉션되지 않습니다 및 `UnauthorizedAccess.aspx`합니다. 대신 로그인 페이지가 표시 됩니다. Bruce 같은 Tito 이외의 사용자로 로그인 합니다. 적절 한 자격 증명을 입력 한 후 로그인 페이지를 미국 리디렉션을 `~/Membership/CreatingUserAccounts.aspx`합니다. 그러나 Tito에 액세스할 수만이 페이지 이므로 볼 수 있는 권한이 하 고 로그인 페이지에 즉시 반환 됩니다. 그러나이 시간 `Request.IsAuthenticated` 반환 `True` (및 `ReturnUrl` querystring 매개 변수 존재) 이므로에서는 리디렉션됩니다는 `UnauthorizedAccess.aspx` 페이지.


[![인증, 권한 없는 사용자가 리디렉션됩니다 UnauthorizedAccess.aspx](user-based-authorization-vb/_static/image17.png)](user-based-authorization-vb/_static/image16.png)

**그림 6**: 인증, 권한 없는 사용자가 리디렉션됩니다 `UnauthorizedAccess.aspx` ([클릭 하 여 큰 이미지 보기](user-based-authorization-vb/_static/image18.png))


이 사용자 지정된 워크플로 단락 (short-circuit) 그림 2에 나와 있는 주기에서 더욱 합리적인 하 고 간단한 사용자 환경을 제공 합니다.

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>3 단계: 현재 로그인 한 사용자를 기반으로 하는 기능 제한

URL 권한 부여 쉽게 정교 하지 않은 권한 부여 규칙을 지정할 수 있습니다. 1 단계에서에서 보았듯이 URL 권한 부여를 사용 하 여에서는 수 간결 하 게 상태 어떤 id 허용 되는 폴더의 모든 페이지 또는 특정 페이지를 볼 수 없도록 거부 됩니다. 그러나 특정 시나리오에서 수 하려고 방문 페이지를 방문 하 고 사용자를 기반으로 하는 페이지의 기능을 제한 하는 모든 사용자를 허용 합니다.

해당 제품을 검토 하려면 인증 된 방문자를 허용 하는 전자 상거래 웹 사이트의 경우를 생각해 보겠습니다. 익명 사용자는 제품 페이지를 방문 하면 제품 정보만 표시할 않으며 리뷰를 남길 수를 지정할 수 없습니다. 그러나 동일한 페이지를 방문 하는 인증 된 사용자 인터페이스를 검토 한 후 표시 됩니다. 인증된 된 사용자가이 제품을 아직 검토 되지 않음, 인터페이스는 수 있도록 검토; 제출 그렇지 않은 경우 표시 됩니다 하 이전에 제출한 검토 합니다. 이 시나리오는 단계를 수행 하 또한 제품 페이지 수 추가 정보를 표시 및 전자 상거래 회사는 해당 사용자를 위한 확장된 기능을 제공 합니다. 예를 들어, 제품 페이지 재고에서 인벤토리를 나열 하 고 제품의 가격 및 직원을 방문한 경우 설명을 편집 하는 옵션을 포함할 수 있습니다.

선언적으로 또는 프로그래밍 방식 (또는 둘의 조합)에 이러한 세부적으로 권한 부여 규칙을 구현할 수 있습니다. 다음 섹션에서 LoginView 컨트롤을 통해 세부적으로 권한 부여를 구현 하는 방법을 살펴보겠습니다. 그런 다음, 프로그래밍 기술을 살펴봅니다. 그러나 세부적으로 권한 부여 규칙을 적용할 살펴보면 전에 먼저 생성 해야 페이지 방문 하 고 사용자에 해당 기능에 따라 달라 집니다.

GridView 내에서 특정 디렉터리의 파일을 나열 하는 페이지를 만들어 보겠습니다. GridView는 Linkbutton의 두 열을 포함 하는 데 함께 각 파일의 이름, 크기 및 기타 정보를 나열 합니다: 보기 및 하나의 이라는 Delete 라는 하나입니다. 보기 LinkButton을 클릭 하면 선택한 파일의 내용이 표시 됩니다. 삭제 LinkButton을 클릭 하면 파일이 삭제 됩니다. 처음에 만들겠습니다이 페이지의 보기 및 삭제 기능을 모든 사용자에 게 사용할 수 있도록 합니다. Using에서 LoginView 컨트롤 및 프로그래밍 방식으로 제한 기능 섹션을 사용 하도록 설정 하거나 페이지를 방문 하 여 사용자를 기반으로 이러한 기능을 사용 하지 않도록 설정 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 빌드에 ASP.NET 페이지 파일의 목록을 표시 하려면 GridView 컨트롤을 사용 합니다. 계열 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 두고이 자습서에서는 이후는 너무 많은 시간을 GridView 컨트롤의 내부 작업에 설명 하지 않겠습니다. 이 자습서에서이 페이지를 설정 하기 위한 특정 단계별 지침을 제공 하지만 특정 변경한 이유는 렌더링 된 출력을 미치는 효과 특정 속성의 세부 정보를 자세히 하지 않습니다. GridView 컨트롤의 철저 한 검사를 참조 하세요. 필자의 *[ASP.NET 2.0에서 데이터로 작업할](../../data-access/index.md)* 자습서 시리즈입니다.


열어서 시작 합니다 `UserBasedAuthorization.aspx` 파일을 `Membership` 폴더 및 라는 페이지에 GridView 컨트롤을 추가 `FilesGrid`. GridView의 스마트 태그에서 필드 대화 상자를 시작 하는 열 편집 링크를 클릭 합니다. 여기에서 왼쪽된 아래 모서리에서 자동 생성 필드 확인란의 선택을 취소 합니다. 그런 다음 (선택한 Delete 단추 CommandField 형식에서 찾을 수 있습니다) 왼쪽된 위 모퉁이에서 선택 단추, Delete 단추 및 두 BoundFields를 추가 합니다. 선택 단추를 설정 `SelectText` 속성을 보고 된 첫 번째 BoundField `HeaderText` 및 `DataField` 속성 이름입니다. 두 번째 BoundField의 설정 `HeaderText` 속성 크기 (바이트), 해당 `DataField` 길이 속성 해당 `DataFormatString` 속성을 {0:N0} 고 `HtmlEncode` 속성을 false로 합니다.

GridView의 열을 구성한 후 필드 대화 상자를 닫으려면 확인을 클릭 합니다. 속성 창에서 설정 된 GridView `DataKeyNames` 속성을 `FullName`입니다. 이 시점에서 GridView의 선언적 태그는 다음과 같아야 합니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample9.aspx)]

GridView의 태그 생성에서는 특정 디렉터리의 파일을 검색 하 고 GridView에 바인딩할 수 있는 코드를 작성할 준비가 된 것입니다. 페이지의 다음 코드를 추가할 `Page_Load` 이벤트 처리기:

[!code-vb[Main](user-based-authorization-vb/samples/sample10.vb)]

위의 코드에서는 합니다 [ `DirectoryInfo` 클래스](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx) 응용 프로그램의 루트 폴더의 파일 목록을 가져올 수 있습니다. 합니다 [ `GetFiles()` 메서드](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx) 배열로 디렉터리의 모든 파일 반환 [ `FileInfo` 개체](https://msdn.microsoft.com/library/system.io.fileinfo.aspx), 다음 GridView에 바인딩됩니다. 합니다 `FileInfo` 개체와 같은 다양 한 속성을가지고 `Name`를 `Length`, 및 `IsReadOnly`, 특히 합니다. 해당 선언적 태그에서 보듯이 GridView만 표시 합니다 `Name` 및 `Length` 속성입니다.

> [!NOTE]
> `DirectoryInfo` 하 고 `FileInfo` 클래스에서 발견 되는 [ `System.IO` 네임 스페이스](https://msdn.microsoft.com/library/system.io.aspx)합니다. 따라서가 해당 네임 스페이스 이름 사용 하 여 이러한 클래스 이름 앞에 클래스 파일을 가져올 네임 스페이스를 가진 (통해 `Imports System.IO`).


잠시 브라우저를 통해이 페이지를 방문 합니다. 응용 프로그램의 루트 디렉터리에 있는 파일 목록이 표시 됩니다. 뷰 또는 Linkbutton 삭제 중 하나를 클릭 하면 포스트백을 하지만 조치가를 아직 했습니다 때문에 발생 합니다. 필요한 이벤트 처리기를 만들어야 합니다.


[![웹 응용 프로그램의 루트 디렉터리의 파일을 나열 하는 GridView](user-based-authorization-vb/_static/image20.png)](user-based-authorization-vb/_static/image19.png)

**그림 7**: 웹 응용 프로그램의 루트 디렉터리의 파일을 나열 하는 GridView ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image21.png))


선택한 파일의 내용을 표시 하는 데 필요 합니다. Visual Studio로 돌아가서 라는 텍스트 상자 추가 `FileContents` GridView 위에 있습니다. 설정 해당 `TextMode` 속성을 `MultiLine` 및 해당 `Columns` 고 `Rows` 속성 95% 및 10을 각각.

[!code-aspx[Main](user-based-authorization-vb/samples/sample11.aspx)]

다음으로 GridView의에 대 한 이벤트 처리기를 만듭니다 [ `SelectedIndexChanged` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx) 다음 코드를 추가 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample12.vb)]

이 코드에서는 GridView의 `SelectedValue` 선택한 파일의 전체 파일 이름을 확인 하는 속성입니다. 내부적으로 `DataKeys` 얻으려면 컬렉션은 참조를 `SelectedValue`GridView의 설정 하는 필수 이므로, `DataKeyNames` 속성 이름에이 단계의 앞부분에 설명 된 대로 합니다. [ `File` 클래스](https://msdn.microsoft.com/library/system.io.file.aspx) 에 할당 한 다음는 문자열로 선택한 파일의 콘텐츠를 읽는 데 사용 되는 `FileContents` 텍스트 상자의 `Text` 속성 페이지에서 선택한 파일의 내용을 표시할 수 있습니다.


[![텍스트 상자에 선택한 파일의 내용이 표시 됩니다.](user-based-authorization-vb/_static/image23.png)](user-based-authorization-vb/_static/image22.png)

**그림 8**: 선택한 파일의 내용을 텍스트 상자에 표시 됩니다 ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image24.png))


> [!NOTE]
> HTML 태그를 포함 하는 파일의 내용 보기를 보거나 파일 삭제를 시도 하는 경우 받게는 `HttpRequestValidationException` 오류입니다. 이 텍스트 상자의 내용을 다시 게시할 때 웹 서버에 다시 전송 되기 때문에 발생 합니다. 기본적으로 asp는 `HttpRequestValidationException` HTML 태그와 같은 잠재적으로 위험한 포스트백 콘텐츠를 감지 될 때마다 오류입니다. 이 오류가 발생 하는 사용 하지 않도록 설정, 해제 페이지에 대 한 요청 유효성 검사를 추가 하 여 `ValidateRequest="false"` 에 `@Page` 지시문입니다. 뿐만 아니라 예방 조치를 취해야 때로 요청 유효성 검사의 이점에 대 한 자세한 내용은 참조를 사용 하지 않도록 설정 [요청 유효성 검사-스크립트 공격 방지](https://asp.net/learn/whitepapers/request-validation/)합니다.


마지막으로 gridview의 다음 코드를 사용 하 여 이벤트 처리기를 추가 [ `RowDeleting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx):

[!code-vb[Main](user-based-authorization-vb/samples/sample13.vb)]

코드에서 삭제할 파일의 전체 이름을 표시 합니다 `FileContents` 텍스트 상자 *없이* 실제로 파일을 삭제 합니다.


[![삭제 단추를 클릭 하면 실제로 삭제 되지 않습니다 파일](user-based-authorization-vb/_static/image26.png)](user-based-authorization-vb/_static/image25.png)

**그림 9**: 파일을 클릭 하 여 삭제 단추 실제로 삭제 되지 않습니다 ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image27.png))


1 단계에서에서 익명 사용자의 페이지를 보고 하지 못하게 하려면 URL 권한 부여 규칙을 구성 했습니다는 `Membership` 폴더입니다. 더 잘 나타낼 세부적으로 인증을 위해 방문 하 여 익명 사용자를 허용 해 보겠습니다는 `UserBasedAuthorization.aspx` 페이지 하지만 제한 된 기능입니다. 에 모든 사용자가 액세스할 수 있도록이 페이지를 열려면 다음을 추가 `<location>` 요소를 `Web.config` 파일을 `Membership` 폴더:

[!code-xml[Main](user-based-authorization-vb/samples/sample14.xml)]

이 추가한 후 `<location>` 요소인 사이트에서 로그인 하 여 새 URL 권한 부여 규칙을 테스트 합니다. 익명 사용자로 있습니다 허용할지 방문 하 여 `UserBasedAuthorization.aspx` 페이지입니다.

현재 인증 또는 익명 사용자 방문할 수는 `UserBasedAuthorization.aspx` 페이지를 보거나 파일을 삭제 합니다. 보겠습니다 있도록 인증 된 사용자만 파일의 콘텐츠를 볼 수 있으며 Tito만 파일을 삭제할 수 있도록 합니다. 선언적으로, 프로그래밍 방식으로 또는 두 메서드 모두의 결합을 통해 이러한 세부적으로 권한 부여 규칙을 적용할 수 있습니다. 보겠습니다 선언적 방법을 사용 하 여 파일의 내용을 볼 수 있는 사람 제한 파일을 삭제할 수 있는 사용자를 제한 하려면 프로그래밍 방식을 사용 하겠습니다.

### <a name="using-the-loginview-control"></a>LoginView 컨트롤을 사용 하 여

이전 자습서에서 살펴본 대로 통해 LoginView 컨트롤은 인증 및 익명 사용자에 대 한 다른 인터페이스를 표시 하는 데 유용 하 고 숨기기 익명 사용자에 게 액세스할 수 있는 기능 쉽게를 제공 합니다. 익명 사용자가 보거나 파일을 삭제할 수 없습니다, 이후 하기만 표시는 `FileContents` 인증된 된 사용자가 해당 페이지를 방문 하는 경우 텍스트 상자에 붙여넣습니다. 이 위해 페이지 LoginView 컨트롤을 추가 하 고 이름을 `LoginViewForFileContentsTextBox`를 이동 합니다 `FileContents` LoginView 컨트롤에 선언적 태그 텍스트 상자의 `LoggedInTemplate`합니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample15.aspx)]

LoginView의 템플릿에서 웹 컨트롤이 더 이상 코드 숨김 클래스에서 직접 액세스할 수 없습니다. 예를 들어, 합니다 `FilesGrid` GridView의 `SelectedIndexChanged` 하 고 `RowDeleting` 이벤트 처리기에서 현재 참조를 `FileContents` 과 같은 코드를 사용 하 여 텍스트 상자 컨트롤:

[!code-aspx[Main](user-based-authorization-vb/samples/sample16.aspx)]

그러나이 코드는 더 이상 유효 합니다. 이동 하 여 합니다 `FileContents` 텍스트 상자에는 `LoggedInTemplate` 텍스트 상자에 직접 액세스할 수 없습니다. 대신 사용 해야 합니다는 `FindControl("controlId")` 프로그래밍 방식으로 컨트롤을 참조 하는 방법입니다. 업데이트 된 `FilesGrid` 같이 텍스트를 참조 하는 이벤트 처리기:

[!code-vb[Main](user-based-authorization-vb/samples/sample17.vb)]

텍스트 상자 LoginView의로 이동한 후 `LoggedInTemplate` 텍스트 상자를 통해 참조 페이지의 코드를 업데이트 하 고는 `FindControl("controlId")` 패턴 익명 사용자로 페이지를 방문 하십시오. 그림 10과 같이 `FileContents` 텍스트 상자에 표시 되지 않습니다. 그러나 보기 LinkButton 계속 표시 됩니다.


[![LoginView 컨트롤에만 인증 된 사용자는 FileContents 텍스트 렌더링](user-based-authorization-vb/_static/image29.png)](user-based-authorization-vb/_static/image28.png)

**그림 10**: The LoginView 컨트롤만 렌더링 합니다 `FileContents` Authenticated Users에 대 한 텍스트 상자에 붙여넣습니다 ([클릭 하 여 큰 이미지 보기](user-based-authorization-vb/_static/image30.png))


익명 사용자에 대 한 뷰 단추를 숨기려면 하나의 방법은 GridView 필드를 TemplateField로 변환 하는 것입니다. 이 보기 linkbutton 선언적 태그를 포함 하는 템플릿으로 생성 됩니다. 그런 다음를 TemplateField LoginView 컨트롤을 추가 하 고 LoginView의 내 LinkButton을 배치할 수 있습니다 `LoggedInTemplate`시켜 익명 방문자에서 뷰 단추를 숨기기. 이를 위해 필드 대화 상자를 시작 하려면 GridView의 스마트 태그에서 열 편집 링크를 클릭 합니다. 다음으로, 왼쪽된 아래 모서리에 있는 목록에서 선택 단추를 선택 하 고 변환을이 필드를 templatefield로 링크를 클릭 합니다. 이렇게 수정 필드의 선언 태그에서:

[!code-aspx[Main](user-based-authorization-vb/samples/sample18.aspx)]

 대상: 

[!code-aspx[Main](user-based-authorization-vb/samples/sample19.aspx)]

 이 시점에서 LoginView를 TemplateField를 추가할 수 있습니다. 다음 태그는 인증 된 사용자에 대해서만 보기 LinkButton을 표시합니다. 

[!code-aspx[Main](user-based-authorization-vb/samples/sample20.aspx)]

그림 11에서 알 수 있듯이, 최종 결과 아닌 경우는 상당히 뷰로 열이 여전히 표시 열 내의 보기 Linkbutton 숨겨진 경우에 살펴보겠습니다 전체 GridView 열 (및 뿐 아니라 LinkButton)를 숨기는 방법을 다음 섹션에 있습니다.


[![LoginView 컨트롤 익명 방문자에 대 한 보기 Linkbutton을 숨깁니다.](user-based-authorization-vb/_static/image32.png)](user-based-authorization-vb/_static/image31.png)

**그림 11**: LoginView 컨트롤 익명 방문자에 대 한 보기 Linkbutton을 숨깁니다 ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image33.png))


### <a name="programmatically-limiting-functionality"></a>프로그래밍 방식으로 기능 제한

일부 경우에는 선언적 기술을 페이지에 기능 제한에 대 한 충분 하지 않습니다. 예를 들어, 특정 페이지 기능의 가용성 페이지를 방문 하는 사용자 인증 또는 익명 인지 이외의 기준에 종속 될 수 있습니다. 이러한 경우 다양 한 사용자 인터페이스 요소 표시 하거나 프로그래밍 방식으로 수단을 통해 숨길 수 있습니다.

기능에 프로그래밍 방식으로 제한 하기 위해 두 가지 작업을 수행 해야 합니다.

1. 사용자 페이지를 방문 하는 기능에 액세스할 수 있는지 여부를 확인 하 고
2. 프로그래밍 방식으로 사용자에 해당 기능에 대 한 액세스에 있는지 여부에 따라 사용자 인터페이스를 수정 합니다.

이러한 두 작업 중 응용 프로그램을 보여 주기 위해 Tito GridView에서 파일을 삭제만 허용 해 보겠습니다. 이 첫 번째 작업 하는 것 Tito 페이지를 방문 하 인지 확인 합니다. 일단 결정 되는 (표시 하거나 숨길) GridView의 열 삭제 해야 합니다. GridView의 열을 통해 액세스할 수 있는 해당 `Columns` 속성 열만 렌더링 되 면 해당 `Visible` 속성이 `True` (기본값).

다음 코드를 추가 합니다 `Page_Load` GridView에 데이터를 바인딩하기 전에 이벤트 처리기:

[!code-vb[Main](user-based-authorization-vb/samples/sample21.vb)]

설명한 대로 합니다 [ *는 폼 인증 개요* ](../introduction/an-overview-of-forms-authentication-vb.md) 자습서에서는 `User.Identity.Name` id의 이름을 반환 합니다. Login 컨트롤에 입력 한 사용자 이름에 해당 합니다. 방문 페이지에 GridView의 두 번째 열 Tito 인지 `Visible` 속성이로 설정 되어 `True`이 고, 그렇지 않으면로 설정 됩니다 `False`. 결과적으로는 다른 인증 된 사용자 또는 익명 사용자, 페이지를 방문 하는 Tito 아닌 다른 열 삭제는 렌더링 되지 않습니다 (그림 12 참조). 그러나 Tito 페이지를 방문 하면 삭제 열이 있는 (그림 13 참조).


[![삭제할 열이 없습니다 렌더링 경우 방문 하 여 누군가가 이외의 Tito (예: Bruce)](user-based-authorization-vb/_static/image35.png)](user-based-authorization-vb/_static/image34.png)

**그림 12**: 열은 삭제 되지 렌더링 때 방문 하 여 사용자가 아닌 다른 Tito (예: Bruce)는 ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image36.png))


[![열 삭제는 Tito 렌더링](user-based-authorization-vb/_static/image38.png)](user-based-authorization-vb/_static/image37.png)

**그림 13**: 열 삭제는 Tito 렌더링 ([큰 이미지를 보려면 클릭](user-based-authorization-vb/_static/image39.png))


## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>4 단계: 클래스 및 메서드를 권한 부여 규칙을 적용

3 단계에서에서 익명 사용자가 파일의 내용을 볼 하 고 모든 사용자가 있지만 Tito 파일 삭제에서 사용할 수 없습니다. 이 작업을 선언적 방법과 프로그래밍 기술을 통해 무단된 방문자에 대 한 연결 된 사용자 인터페이스 요소를 숨겨 수행 했습니다. 간단한 예를 들어 사용자 인터페이스 요소를 제대로 숨기기 되었지만 간단한 어떨까요 더 복잡 한 사이트 다양 한 방법으로 동일한 기능을 수행 될 수 있는? 권한 없는 사용자에 해당 기능을 제한에 미치는 영향을 숨기 거 나 모든 적용 가능한 사용자 인터페이스 요소를 사용 하지 않도록 설정 하지 않으면

권한이 없는 사용자가 기능의 특정 부분에 액세스할 수 없도록 하는 간편한 방법은 해당 클래스 또는 메서드를 데코 레이트 하는 것은 [ `PrincipalPermission` 특성](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)합니다. .NET 런타임 클래스를 사용 하 여, 해당 메서드 중 하나를 실행 하는 경우 현재 보안 컨텍스트 클래스를 사용 하거나 메서드를 실행할 권한이 있는지 확인 하려면 확인 합니다. `PrincipalPermission` 특성에서는 이러한 규칙을 정의할 수 있는 메커니즘을 제공 합니다.

사용 하 여 살펴보겠습니다 합니다 `PrincipalPermission` GridView의 특성 `SelectedIndexChanged` 및 `RowDeleting` 각각 Tito, 이외의 사용자 인 경우 익명 사용자로 실행을 금지 하는 이벤트 처리기입니다. 각 함수 정의 위에 적절 한 특성을 추가 하기만 됩니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample22.vb)]

에 대 한 특성을 `SelectedIndexChanged` 인증 된 사용자만 하도록 이벤트 처리기 규정에 대 한 특성으로 작업 하는 경우 이벤트 처리기를 실행할 수 있습니다는 `RowDeleting` Tito 하 고 실행을 제한 하는 이벤트 처리기입니다.

> [!NOTE]
> 특성은 클래스, 메서드, 속성 또는 이벤트에 적용할 수 있습니다. 특성을 추가할 때는 클래스, 메서드, 속성 또는 이벤트 선언문의 일부 이어야 합니다. Visual Basic에서는 줄 바꿈으로 문 구분 기호 이후 선언 또는 바로 위의 줄 연속 문자 (밑줄)를 사용 하 여 동일한 줄에 특성 하거나 나타나야 합니다. 위의 코드 조각에서 줄 연속 문자 줄 및 다른 메서드 선언에 특성을 배치에 사용 됩니다.


Tito 이외의 사용자 어떻게 해서든 실행 하려고 하는 경우는 `RowDeleting` 이벤트 처리기 또는 인증 되지 않은 사용자가 실행 하려고 합니다 `SelectedIndexChanged` .NET 런타임 발생 이벤트 처리기를 `SecurityException`.


[![보안 컨텍스트는 메서드를 실행할 수 있는 권한이 없습니다, 경우 SecurityException이 Throw 됩니다.](user-based-authorization-vb/_static/image41.png)](user-based-authorization-vb/_static/image40.png)

**그림 14**: 보안 컨텍스트 메서드를 실행할 권한이 없는 경우는 `SecurityException` 이 Throw 됩니다 ([클릭 하 여 큰 이미지 보기](user-based-authorization-vb/_static/image42.png))


> [!NOTE]
> 클래스 또는 메서드에 액세스할 수 있는 여러 보안 컨텍스트를 허용 하려면 클래스 또는 메서드를 데코레이팅하는 `PrincipalPermission` 각 보안 컨텍스트에 대 한 특성입니다. 즉, Tito 및 Bruce 실행을 허용 하는 `RowDeleting` 이벤트 처리기를 추가 *두* `PrincipalPermission` 특성:


[!code-vb[Main](user-based-authorization-vb/samples/sample23.vb)]

ASP.NET 페이지 외에도 많은 응용 프로그램은 수도 비즈니스 논리 및 데이터 액세스 계층 같은 다양 한 계층을 포함 하는 아키텍처에 연결 합니다. 이러한 계층은 일반적으로 클래스 라이브러리로 구현 및 비즈니스 논리 및 데이터 관련 기능을 수행 하기 위한 메서드와 클래스를 제공 합니다. `PrincipalPermission` 특성은 이러한 계층에 권한 부여 규칙을 적용 하는 데 유용 합니다.

사용 하 여 대 한 자세한 내용은 합니다 `PrincipalPermission` 클래스 및 메서드에서 권한 부여 규칙을 정의 참조 특성 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [비즈니스 및 데이터 레이어 사용하여권한부여규칙추가`PrincipalPermissionAttributes` ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>요약

이 자습서에서는 사용자 기반 권한 부여 규칙을 적용 하는 방법에 살펴보았습니다. ASP 시작 했습니다. NET의 URL 권한 부여 프레임 워크입니다. 각 요청에 ASP.NET 엔진의 `UrlAuthorizationModule` id가 요청 된 리소스에 액세스할 수 있는 권한이 있는지 확인 하려면 응용 프로그램의 구성에 정의 된 URL 권한 부여 규칙을 검사 합니다. 즉, URL 권한 부여 쉽게 특정 디렉터리의 모든 페이지 또는 특정 페이지에 대 한 권한 부여 규칙을 지정할 수 있습니다.

URL 권한 부여 프레임 워크에서 페이지 단위로 권한 부여 규칙을 적용합니다. URL 권한 부여를 요청 id 또는 특정 리소스에 액세스할 수 있는 권한이 있습니다. 그러나 대부분의 시나리오에서는 더 세부적으로 권한 부여 규칙에 대 한 호출합니다. 이 페이지에 액세스할 수를 정의 하는 대신 수 해야 모든 페이지에 액세스할 수 있도록 하지만 다양 한 데이터를 표시 하거나 페이지를 방문 하는 사용자에 따라 다른 기능을 제공 합니다. 일반적으로 페이지 수준 권한 부여는 권한이 없는 사용자가 허용 되지 않는 기능에 액세스 하지 못하게 하기 위해 특정 사용자 인터페이스 요소를 숨기는 포함 됩니다. 또한 특성을 사용 하 여 클래스 및 특정 사용자에 대 한 해당 메서드의 실행에 대 한 액세스를 제한 하는 것이 같습니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [비즈니스 및 데이터 계층을 사용 하 여 권한 부여 규칙 추가 `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [IIS6 사이의 IIS7 보안 변경 내용](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [특정 파일 및 하위 디렉터리를 구성합니다.](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [사용자를 기반으로 하는 데이터 수정 기능 제한](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb.md)
- [LoginView 컨트롤 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [IIS7 URL 권한 부여를 이해합니다.](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` 기술 문서](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [ASP.NET 2.0의에서 데이터로 작업](../../data-access/index.md)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](validating-user-credentials-against-the-membership-user-store-vb.md)
> [다음](storing-additional-user-information-vb.md)
