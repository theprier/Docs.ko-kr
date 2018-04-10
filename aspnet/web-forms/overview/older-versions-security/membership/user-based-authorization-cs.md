---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-cs
title: 사용자 기반 권한 부여 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 살펴보겠습니다 다양 한 기술을 통해 페이지 수준 기능을 제한 하 고 페이지에 대 한 액세스를 제한 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/18/2008
ms.topic: article
ms.assetid: 3c815a9e-2296-4b9b-b945-776d54989daa
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 9a0d476ffaf1f176c21b245520fa943f66e8c0d5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="user-based-authorization-c"></a>사용자 기반 권한 부여 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_cs.pdf)

> 이 자습서에서는 살펴보겠습니다 다양 한 기술을 통해 페이지 수준 기능을 제한 하 고 페이지에 대 한 액세스를 제한 합니다.


## <a name="introduction"></a>소개

사용자 계정을 제공 하는 대부분의 웹 응용 프로그램 특정 방문자 사이트 내의 특정 페이지에 액세스 하지 못하도록 제한 하는 부분에서 이렇게 합니다. 예를 들어 대부분의 온라인 보드 사이트-익명 및 인증 된-모든 사용자가 보드의 게시물을 볼 수 있는 있지만 인증 된 사용자만 새 게시물을 만들려는 웹 페이지를 방문 수 있습니다. 및 특정 사용자 (또는 사용자의 특정 집합)에 액세스할 수 있는 관리 페이지가 있을 수 있습니다. 또한 페이지 수준 기능 사용자 간 별로 다를 수 있습니다. 게시물의 목록을 볼 때에 인증 된 사용자가이 인터페이스를 익명 방문자에 게 사용할 수 없는 반면 각 게시물 등급에 대 한 인터페이스에 표시 됩니다.

ASP.NET 쉽게 사용자 기반 권한 부여 규칙을 정의할 수 있습니다. 태그에 약간 `Web.config`, 특정 웹 페이지 또는 전체 디렉터리의 사용자 지정 된 하위 집합에 액세스할 수만 있도록 아래로 잠글 수 있습니다. 페이지 수준 기능 수 설정 또는 해제 프로그래밍 및 선언적 수단을 통해 현재 로그인된 한 사용자에 따라 합니다.

이 자습서에서는 살펴보겠습니다 다양 한 기술을 통해 페이지 수준 기능을 제한 하 고 페이지에 대 한 액세스를 제한 합니다. 이제 시작 하겠습니다.

## <a name="a-look-at-the-url-authorization-workflow"></a>URL 권한 부여 워크플로 살펴보면

에 설명 된 대로 [ *폼 인증의 개요는* ](../introduction/an-overview-of-forms-authentication-cs.md) 자습서에서는 ASP.NET 런타임은 ASP.NET 요청 리소스를 수명 주기 동안 다양 한 이벤트를 발생 시킵니다.에 대 한 요청을 처리할 때. *HTTP 모듈* 는 관리 되는 클래스는 요청 수명에 특정 이벤트에 해당 코드가 실행 됩니다. ASP.NET 원리를 자세히 파악할수록 필수 작업을 수행 하는 HTTP 모듈의 수와 함께 제공 합니다.

이러한 하나의 HTTP 모듈은 [ `FormsAuthenticationModule` ](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)합니다. 이전 자습서의 기본 기능은에 설명 된 대로 `FormsAuthenticationModule` 현재 요청의 id를 결정 하는 것입니다. 이 쿠키에 되었거나 URL 내에 포함 된 폼 인증 티켓을 검사 하 여 수행 됩니다. 이 식별 하는 동안 일어나는 [ `AuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)합니다.

또 다른 중요 한 HTTP 모듈을는 [ `UrlAuthorizationModule` ](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx), 대 한 응답으로 발생 하는 [ `AuthorizeRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx) (후 발생 하는 `AuthenticateRequest` 이벤트). `UrlAuthorizationModule` 구성 태그를 검사 하 여 `Web.config` 현재 id 지정된 된 페이지를 방문 하 여 권한을 갖는지 확인 합니다. 이 프로세스 라고 *URL 권한 부여*합니다.

살펴봅니다 1 단계에서에서 URL 권한 부여 규칙에 대 한 구문을 하지만 먼저 보겠습니다을 파악는 `UrlAuthorizationModule` 여부는 요청이 허용 되는지 여부에 따라 않습니다. 경우는 `UrlAuthorizationModule` 판단 하는 요청이 승인 되 다음 아무것도 수행 하지, 주기를 통해 요청이 계속 합니다. 그러나 요청이 면 *하지* 에 게 권한이 부여 하면 `UrlAuthorizationModule` 수명 주기를 중단 하 고 지시는 `Response` 반환할 개체는 [HTTP 401 권한이 없음](http://www.checkupdown.com/status/E401.html) 상태입니다. 때문에이 HTTP 401 상태 클라이언트에 반환 되지 않습니다 폼 인증을 사용 하는 경우 경우는 `FormsAuthenticationModule` 감지 하면 HTTP 401 상태를 수정 하는 [HTTP 302 리디렉션](http://www.checkupdown.com/status/E302.html) 로그인 페이지에 있습니다.

그림 1은 ASP.NET 파이프라인의 워크플로 `FormsAuthenticationModule`, 및 `UrlAuthorizationModule` 권한이 없는 요청 도착 합니다. 특히, 그림 1에 대 한 익명는 방문자의 요청에 나와 `ProtectedPage.aspx`은 익명 사용자에 대 한 액세스를 거부 하는 페이지입니다. 방문자는 익명 이며, 이후는 `UrlAuthorizationModule` 는 요청을 중단 하 고 HTTP 401 권한이 없음 상태를 반환 합니다. `FormsAuthenticationModule` 로그인 페이지로 302 리디렉션으로 401 상태를 변환 합니다. 사용자가 로그인 페이지를 통해 인증 되 면 그 리디렉션됩니다 `ProtectedPage.aspx`합니다. 이 현재는 `FormsAuthenticationModule` 그의 인증 티켓을 기반으로 사용자를 식별 합니다. 방문자가 인증 되 면 했으므로 `UrlAuthorizationModule` 페이지에 대 한 액세스를 허용 합니다.


[![폼 인증 및 URL 권한 부여 워크플로](user-based-authorization-cs/_static/image2.png)](user-based-authorization-cs/_static/image1.png)

**그림 1**: URL 권한 부여 워크플로 및 폼 인증 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image3.png))


그림 1은 익명 방문자가 익명 사용자에 게 사용할 수 없는 리소스에 액세스 하려고 할 때 발생 하는 상호 작용을 보여 줍니다. 이 경우 익명 방문자는 쿼리 문자열에 지정 된 방문 하려고 그녀 페이지와 함께 로그인 페이지로 리디렉션됩니다. 사용자가 로그온 되 면 그녀 자동으로 리디렉션됩니다 볼 하려고 처음 그녀 리소스 이동 합니다.

이 워크플로 간단 하며가 상황을 이해 하는 방문자에 대 한 쉽게에 익명의 사용자 권한이 없는 요청이 수행 될 때 및 이유입니다. 에 유지 하는 `FormsAuthenticationModule` 리디렉션됩니다 *모든* 인증된 된 사용자가 요청 하는 경우에 로그인 페이지에는 사용자 권한이 없는 합니다. 인증된 된 사용자가을 영업 관리자에 게 없는 경우 기관 페이지를 방문 하려고 할 경우 사용자 환경에 혼란 발생할 수 있습니다.

웹 사이트의 URL 권한 부여 규칙 구성 되어 있는지 생각할 되도록 ASP.NET 페이지 `OnlyTito.aspx` Tito에만 액세스할 수 있습니다 되었습니다. Sam 사이트를 방문 하, 로그온 방문 하려고를 가정해 보겠습니다 `OnlyTito.aspx`합니다. `UrlAuthorizationModule` 요청 수명 주기의 중단 되며 HTTP 401 권한이 없음 상태를 반환 하는 `FormsAuthenticationModule` 에서는 검색 하 고 Sam 로그인 페이지로 리디렉션합니다. Sam가 이미 로그인 한 이후 경과 하지만 그녀 궁금할 이유 그녀 ध 로그인 페이지에 다시입니다. 그녀 어떻게 하 든, 자신의 로그인 자격 증명이 손실 또는 잘못 된 자격 증명을 입력 한 그녀 이유 수 있습니다. Sam 로그인 페이지에서 자격 증명을 입력 하는 경우 그녀 (다시) 기록 되며 리디렉션됩니다 `OnlyTito.aspx`합니다. `UrlAuthorizationModule` 에서 검색 하 고 Sam이이 페이지를 방문할 수 없으면 그녀는 로그인 페이지에 반환 됩니다.

그림 2는 혼동이 워크플로 보여 줍니다.


[![기본 워크플로 혼동 사이클에 발생할 수 있습니다.](user-based-authorization-cs/_static/image5.png)](user-based-authorization-cs/_static/image4.png)

**그림 2**: The 기본 워크플로 발생할 수 있습니다 혼란 스 러 주기 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image6.png))


그림 2에 설명 된 워크플로 대부분 컴퓨터 숙련 방문자를 befuddle 신속 하 게 수 있습니다. 이 주기 2 단계에서에서 혼동을 방지 하는 방법을 알아봅니다.

> [!NOTE]
> ASP.NET는 두 가지 메커니즘을 사용 하 여 현재 사용자는 특정 웹 페이지에 액세스할 수 있는지 여부를 확인 하려면: URL 권한 부여 및 파일 권한 부여 합니다. 파일 권한 부여에 의해 구현 됩니다는 [ `FileAuthorizationModule` ](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx), 요청한 파일 Acl을 참고 하 여 기관을 결정 합니다. Acl은 Windows 계정에 적용 되는 권한 때문에 파일 권한 부여는 Windows 인증을 사용한 가장 많이 사용 됩니다. 폼 인증을 사용할 경우 모든 운영 체제 및 파일 시스템 수준 요청은 사이트를 방문 하는 사용자에 관계 없이 동일한 Windows 계정에 의해 실행 됩니다. 폼 인증을 중점적으로이 자습서 시리즈, 이후에서는 설명 하지 파일 권한 부여 합니다.


### <a name="the-scope-of-url-authorization"></a>URL 권한 부여 범위

`UrlAuthorizationModule` 은 ASP.NET 런타임이의 일부인 코드를 관리 합니다. Microsoft의의 버전 7 이전 [인터넷 정보 서비스 (IIS)](https://www.iis.net/) 웹 서버 IIS의 HTTP 파이프라인 및 파이프라인 ASP.NET 런타임 간의 고유한 장벽 했습니다. 즉, IIS 6 및 이전 버전에서는 ASP 합니다. NET의 `UrlAuthorizationModule` ASP.NET 런타임에 IIS에서 요청을 위임 하는 경우에 실행 합니다. 기본적으로 IIS HTML 페이지 및 CSS, JavaScript 및 이미지 파일-같은 정적 콘텐츠 자체를 처리 하 고만 ASP.NET 런타임 때의 확장에 있는 페이지에 대 한 요청에 전달한 `.aspx`, `.asmx`, 또는 `.ashx` 를 요청 합니다.

그러나 IIS 7 허용 통합된 IIS 및 ASP.NET 파이프라인 합니다. 몇 가지 구성 설정을 사용 하 여 IIS 7 호출을 설정할 수 있습니다는 `UrlAuthorizationModule` 에 대 한 *모든* 요청을 모든 형식의 파일에 대 한 URL 권한 부여 규칙을 정의할 수 있다는 의미입니다. 또한 IIS 7 자체 URL 권한 부여 엔진을 포함합니다. ASP.NET 통합 및 IIS 7의 기본 URL 권한 부여 기능에 대 한 자세한 내용은 참조 하십시오. [이해 IIS7 URL 권한 부여](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)합니다. ASP.NET 및 IIS 7 통합에 대 한 자세한 설명에 대 한 선택 Shahram Khosravi 책의 복사본을 *Professional IIS 7 및 ASP.NET 통합 프로그래밍* (ISBN: 978 0470152539).

간단히 말해, IIS 7 이전 버전, URL 권한 부여 규칙 ASP.NET 런타임에 의해 처리 되는 리소스에 적용만 됩니다. 하지만 IIS 7과 IIS의 네이티브 URL 권한 부여 기능을 사용 하거나 ASP 통합 하려면 가능한 쉽습니다. NET의 `UrlAuthorizationModule` IIS의 HTTP 파이프라인에 대 한 모든 요청에이 기능을 확장 함으로써 합니다.

> [!NOTE]
> 몇 가지 미묘한 아직 중요 한 차이점이 있습니다 방법에서 ASP 합니다. NET의 `UrlAuthorizationModule` 및 IIS 7의 URL 권한 부여 기능을 권한 부여 규칙을 처리 합니다. 이 자습서에는 IIS 7의 URL 권한 부여 기능은 이나 방식에 비해 권한 부여 규칙을 구문 분석에 차이 검사 하지 않습니다는 `UrlAuthorizationModule`합니다. 이러한 항목에 대 한 자세한 내용은 MSDN 또는 IIS 7 설명서를 참조 [www.iis.net](https://www.iis.net/)합니다.


## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>1 단계: URL 권한 부여 규칙의 정의`Web.config`

`UrlAuthorizationModule` 권한을 부여 하거나 응용 프로그램의 구성에 정의 된 URL 권한 부여 규칙에 따라 특정 id에 대 한 요청된 된 리소스에 대 한 액세스를 거부할 것인지 결정 합니다. 권한 부여 규칙에 명시 되는 [ `<authorization>` 요소](https://msdn.microsoft.com/library/8d82143t.aspx) 의 형태로 `<allow>` 및 `<deny>` 자식 요소입니다. 각 `<allow>` 및 `<deny>` 자식 요소를 지정할 수 있습니다.

- 특정 사용자
- 사용자의 쉼표로 구분 된 목록
- 물음표 (?)를 가리키는 모든 익명 사용자
- 단독으로 표시 하는 모든 사용자 (\*)

다음 태그 Tito 및 Scott 사용자가 허용 하거나 거부 하는 다른 모든 URL 권한 부여 규칙을 사용 하는 방법을 보여 줍니다.

[!code-xml[Main](user-based-authorization-cs/samples/sample1.xml)]

`<allow>` 요소-Tito 및 Scott-어떤 사용자 허용 되는 정의 하는 동안는 `<deny>` 요소에 지시 하는 *모든* 사용자는 거부 됩니다.

> [!NOTE]
> `<allow>` 및 `<deny>` 요소 역할에 대 한 권한 부여 규칙을 지정할 수도 있습니다. 이후 자습서에서 역할 기반 권한 부여를 검사 합니다.


다음 설정을 Sam (익명 방문자 포함) 이외에 대 한 액세스를 부여 합니다.

[!code-xml[Main](user-based-authorization-cs/samples/sample2.xml)]

인증 된 사용자만을 허용 하려면 모든 익명 사용자에 대 한 액세스를 거부 하는 다음 구성을 사용 합니다.

[!code-xml[Main](user-based-authorization-cs/samples/sample3.xml)]

권한 부여 규칙 내에 정의 된는 `<system.web>` 요소 `Web.config` 모든 웹 응용 프로그램에서 ASP.NET 리소스에 적용 합니다. 종종 응용 프로그램은 다양 한 섹션에 대 한 다양 한 권한 부여 규칙. 예를 들어 전자 상거래 사이트에서 모든 방문자 수는 제품을 살펴보고, 제품 검토를 보거나, 카탈로그에서 검색 등에입니다. 그러나 체크 아웃 또는 배송 기록을 관리 하는 페이지 인증 된 사용자만 연결할 수 있습니다. 또한 사이트 관리자와 같은 선택 사용자가 액세스할 수 있는 사이트의 부분 있을 수 있습니다.

ASP.NET을 사용 하면 쉽게 사이트에서 다른 파일 및 폴더에 대 한 다양 한 권한 부여 규칙을 정의할 수 있습니다. 루트 폴더에 지정 된 권한 부여 규칙 `Web.config` 파일 사이트에 있는 모든 ASP.NET 리소스에 적용 합니다. 그러나 이러한 기본 권한 부여 설정을 재정의할 수 있습니다는 특정 폴더에 대 한 추가 하 여 한 `Web.config` 와 `<authorization>` 섹션.

인증 된 사용자만의 ASP.NET 페이지를 방문 수 있도록 웹 사이트를 업데이트 해 보겠습니다는 `Membership` 폴더입니다. 추가 해야이를 위해는 `Web.config` 파일을 `Membership` 폴더 및 해당 권한 부여 설정을 익명 사용자가 거부 하도록 설정 합니다. 마우스 오른쪽 단추로 클릭는 `Membership` 상황에 맞는 메뉴에서 새 항목 추가 메뉴를 선택 하 고 라는 새 웹 구성 파일을 추가 하는 솔루션 탐색기에서 폴더 `Web.config`합니다.


[![멤버 자격 폴더에 Web.config 파일 추가](user-based-authorization-cs/_static/image8.png)](user-based-authorization-cs/_static/image7.png)

**그림 3**: 추가 된 `Web.config` 파일을 여 `Membership` 폴더 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image9.png))


두 개의 프로젝트가 포함 되어야이 시점에서 `Web.config` 파일: 및 1의 루트 디렉터리에 각각 하나씩의 `Membership` 폴더입니다.


[![응용 프로그램 두 Web.config 파일 포함](user-based-authorization-cs/_static/image11.png)](user-based-authorization-cs/_static/image10.png)

**그림 4**: Your 응용 프로그램은 이제 포함 두 `Web.config` 파일 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image12.png))


업데이트의 구성 파일에는 `Membership` 폴더를 익명 사용자에 대 한 액세스를 금지 하도록 합니다.

[!code-xml[Main](user-based-authorization-cs/samples/sample4.xml)]

그을 마쳤습니다.

이 변경은 테스트 하려면 브라우저에서 홈 페이지를 방문 하 고 로그 아웃 해야 합니다. 모든 방문자를 허용 하는 것이 ASP.NET 응용 프로그램의 기본 동작 이므로 되며 루트 디렉터리에 대 한 권한 부여 수정을 하도록 하지 않은 `Web.config` 에 익명 방문자와 루트 디렉터리에 파일을 방문할 수는 파일입니다.

왼쪽된 열에서 찾은 사용자 계정 만들기 링크를 클릭 합니다. 이 데는 `~/Membership/CreatingUserAccounts.aspx`합니다. 이후는 `Web.config` 파일에 `Membership` 익명 액세스를 금지 하는 권한 부여 규칙을 정의 하는 폴더는 `UrlAuthorizationModule` 는 요청을 중단 하 고 HTTP 401 권한이 없음 상태를 반환 합니다. `FormsAuthenticationModule` 로그인 페이지로 보내더라도 302 리디렉션 상태에이 수정 합니다. 페이지 म 하 려 했던 액세스 확인 (`CreatingUserAccounts.aspx`)를 통해 로그인 페이지에 전달 되는 `ReturnUrl` querystring 매개 변수입니다.


[![URL 권한 부여 규칙을 허용 하지 않는 익명 액세스를 로그인 페이지로 리디렉션되는 했습니다.](user-based-authorization-cs/_static/image14.png)](user-based-authorization-cs/_static/image13.png)

**그림 5**: 로그인 페이지로 리디렉션되는 URL 권한 부여 규칙의 경우 익명 액세스를 금지, 이후 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image15.png))


성공적으로 로그인 시 우리는 리디렉션됩니다는 `CreatingUserAccounts.aspx` 페이지. 이 현재는 `UrlAuthorizationModule` 익명 더 이상 있으므로 페이지에 대 한 액세스를 허용 합니다.

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>특정 위치에 URL 권한 부여 규칙을 적용

에 정의 된 권한 부여 설정을 `<system.web>` 섹션 `Web.config` 모든 디렉터리와 하위 디렉터리에 ASP.NET 리소스에 적용 (그렇지 않으면 다른 재정의 될 때까지 `Web.config` 파일). 경우에 따라 하지만 좋겠습니다 하나 또는 두 개의 특정 페이지를 제외 하 고 특정 권한 부여 구성으로 지정된 된 디렉터리의 모든 ASP.NET 리소스입니다. 이 작업을 추가 하 여 수행할 수는 `<location>` 요소 `Web.config`, 권한 부여 규칙의 다른 파일을 가리키는 및 그 안에 해당 고유 권한 부여 규칙을 정의 합니다.

사용 하 여 설명 하기 위해는 `<location>` 보겠습니다만 Tito를 방문할 수 있도록 권한 부여 설정을 사용자 지정, 특정 리소스에 대 한 구성 설정을 재정의 하는 요소 `CreatingUserAccounts.aspx`합니다. 이를 위해 추가 `<location>` 요소를는 `Membership` 폴더의 `Web.config` 파일을 다음과 같이 되도록 해당 태그를 업데이트 합니다.

[!code-xml[Main](user-based-authorization-cs/samples/sample5.xml)]

`<authorization>` 요소 `<system.web>` ASP.NET 리소스에 대 한 기본 URL 권한 부여 규칙을 정의 `Membership` 폴더와 하위 폴더입니다. `<location>` 요소를 사용 하는 특정 리소스에 대 한 이러한 규칙을 재정의 합니다. 위의 태그에는 `<location>` 요소 참조는 `CreatingUserAccounts.aspx` 페이지와 같은 Tito, 허용 권한 부여 규칙을 지정 하지만 거부 다른 모든 사용자입니다.

이 권한 부여 변경을 테스트 하려면 익명 사용자로 웹 사이트를 방문 하 여 시작 합니다. 모든 페이지를 방문 하 여 사용 하려는 경우는 `Membership` 폴더와 같은 `UserBasedAuthorization.aspx`, `UrlAuthorizationModule` 는 요청을 거부 및 로그인 페이지로 이동 합니다. 예를 들어, Scott 다른 이름으로 로그인 한 후의 모든 페이지에 방문할 수 있습니다는 `Membership` 폴더 *제외 하 고* 에 대 한 `CreatingUserAccounts.aspx`합니다. 방문 하려고 `CreatingUserAccounts.aspx` 모든 사용자로 로그온 이지만 Tito 로그인 페이지로 리디렉션됩니다는 무단된 액세스 시도에서 발생 됩니다.

> [!NOTE]
> `<location>` 구성의 외부에서 나타나야 합니다 `<system.web>` 요소입니다. 별도 사용 해야 `<location>` 권한 부여 설정을 재정의 하려면 각 리소스에 대 한 요소입니다.


### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>참조 방법을`UrlAuthorizationModule`액세스를 부여 하거나 거부 권한 부여 규칙을 사용 하 여

`UrlAuthorizationModule` 여부 URL 권한 부여를 분석 하 여 특정 URL에 대 한 특정 id를 갖도록 규칙 하려면 첫 번째에서 시작 하 고 아래쪽의 방식으로 작업 한 번에 하나씩 결정 합니다. 사용자가 허용 하거나 거부, 경우에 따라 일치가 발생에 일치 항목이 발견 되는 즉시는 `<allow>` 또는 `<deny>` 요소입니다. <strong>일치 하는 항목이 사용자 액세스 권한이 부여 됩니다.</strong> 따라서 액세스를 제한 하려는 경우 사용 하 여는 `<deny>` URL 권한 부여 구성에서 마지막 요소로 요소입니다. <strong>생략 하면는</strong><strong>`<deny>`</strong><strong>요소를 모든 사용자에 게 권한이 부여 됩니다.</strong>

사용 하는 프로세스를 보다 잘 이해 하려면는 `UrlAuthorizationModule` 기관을 확인 하려면 예를 들어 URL 권한 부여 규칙에서이 단계에서 찾았습니다. 첫 번째 규칙은 한 `<allow>` Tito 및 Scott에 액세스할 수 있는 요소입니다. 두 번째 규칙은 한 `<deny>` 모든 사용자에 게 액세스를 거부 하는 요소입니다. 익명 사용자를 방문 하는 경우는 `UrlAuthorizationModule` 를 요청 하 여 시작 되는 익명 Scott 또는 Tito? 응답, 분명 한 것 이므로 No, 두 번째 규칙에 진행 됩니다. 모든 사용자에 게 집합에서 익명 인가요? 대답 이후 예, 다음은 `<deny>` 규칙 적용 배치 되 고 방문자 로그인 페이지로 리디렉션됩니다. 마찬가지로 Jisun 방문 중인 경우, 고 `UrlAuthorizationModule` 요청은 Jisun 하 여 시작 Scott 또는 Tito? 그녀는 사용 되지 않는 이후는 `UrlAuthorizationModule` 두 번째 질문의 모든 사용자 집합에는 Jisun 진행? 그녀 이므로, she, 너무,의 액세스가 거부 됩니다. 에 의해 첫 번째 질문 제기 되 Tito 방문 하는 경우 마지막으로 `UrlAuthorizationModule` 확실 한 응답, 이므로 Tito 액세스 권한이 부여 됩니다.

이후는 `UrlAuthorizationModule` 프로세스에 더 구체적인 규칙이 덜 구체적인 예외 보다 앞에 오도록 해야 권한 부여 규칙에서 하향식으로 모든 일치 항목에 중지 합니다. 즉, 다른 모든 인증 된 사용자가 허용 하지만 Jisun 및 익명 사용자가 금지 하는 권한 부여 규칙을 정의 하려면 가장 구체적인 규칙-하나의 영향 Jisun-로 시작 하는 다른 모든을 허용 하는 것 보다 덜 구체적인 규칙-후 계속 진행 인증 된 사용자가 있지만 모든 익명 사용자를 거부 합니다. 다음 URL 권한 부여 규칙 Jisun를 거부 하면 먼저 다음 모든 익명 사용자를 거부 하 여이 정책을 구현 합니다. Jisun 이외의 모든 인증 된 사용자 권한이 부여 됩니다 때문에 이러한 `<deny>` 문은 일치 됩니다.

[!code-xml[Main](user-based-authorization-cs/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>2 단계: 인증, 권한 없는 사용자에 대 한 워크플로 수정

URL 권한 부여 워크플로 섹션에는 위치에서이 자습서의 앞부분에서 설명한 대로 권한이 없는 요청 다소 언제 든 지,는 `UrlAuthorizationModule` 는 요청을 중단 하 고 HTTP 401 권한이 없음 상태를 반환 합니다. 이 401 상태에 의해 수정 됩니다는 `FormsAuthenticationModule` 는 302에 사용자의 로그인 페이지에 전송 하는 상태를 리디렉션합니다. 이 워크플로 사용자가 인증 하는 경우에 모든 승인 되지 않은 요청에 발생 합니다.

인증된 된 사용자는 로그인 페이지로 돌아가기 시스템에 이미 로그인 한 이후 혼동 하기 쉽습니다. 약간의 작업으로 제한 된 페이지에 액세스 하려고 시도한 있는지에 대해 설명 하는 페이지에 무단으로 요청 하는 인증 된 사용자가 리디렉션하여이 워크플로 개선할 수 있는 합니다.

라는 웹 응용 프로그램의 루트 폴더에서 새 ASP.NET 페이지를 만들어 시작 `UnauthorizedAccess.aspx`;이 페이지와 연결 하도록 설정 된 `Site.master` 마스터 페이지입니다. 이 페이지를 만든 후를 참조 하는 콘텐츠 컨트롤을 제거는 `LoginContent` ContentPlaceHolder 마스터 페이지의 기본 콘텐츠 되도록 표시 됩니다. 다음으로, 즉 상황을 설명 하는 메시지를 추가 사용자가 보호 된 리소스에 액세스 하려고 합니다. 이러한 메시지를 추가한 후의 `UnauthorizedAccess.aspx` 페이지의 선언적 태그는 다음과 비슷해야 합니다.

[!code-aspx[Main](user-based-authorization-cs/samples/sample7.aspx)]

이제에 보내도록 인증된 된 사용자가 승인 되지 않은 요청을 수행 하는 경우 워크플로 변경할 필요는 `UnauthorizedAccess.aspx` 로그인 페이지 대신 페이지. 로그인 페이지에 허가 되지 않은 요청을 리디렉션하는 논리의 전용 메서드 내에서 숨겨져는 `FormsAuthenticationModule` 클래스,에서는이 동작을 사용자 지정할 수 없습니다. 그러나 고유한 발급자의 사용자를 리디렉션하는 로그인 페이지에는 수행할 수 있는, `UnauthorizedAccess.aspx`, 필요한 경우.

경우는 `FormsAuthenticationModule` 무단된 방문자 리디렉션합니다 로그인 페이지에 요청 된, 무단 URL 이름으로 쿼리 문자열을 추가 `ReturnUrl`합니다. 예를 들어, 권한이 없는 사용자가 방문 하려고 `OnlyTito.aspx`, `FormsAuthenticationModule` 하도록 리디렉션합니다 `Login.aspx?ReturnUrl=OnlyTito.aspx`합니다. 따라서 포함 된 querystring으로 인증된 된 사용자가 로그인 페이지에 도달 하는 경우는 `ReturnUrl` 매개 변수, 그런 다음이 인증 되지 않은 사용자를 볼 권한이 없는 그녀는 페이지를 방문 하 여 방금 늘리려고 했음을 알고 있습니다. 이러한 경우를 리디렉션할 하려고 `UnauthorizedAccess.aspx`합니다.

이를 위해 다음 코드를 추가 하 여 로그인 페이지의 `Page_Load` 이벤트 처리기.

[!code-csharp[Main](user-based-authorization-cs/samples/sample8.cs)]

위의 코드를 인증, 권한 없는 사용자를 리디렉션하는 `UnauthorizedAccess.aspx` 페이지. 작업에서이 논리를 보려면 익명 방문자와 사이트를 방문 하 고 왼쪽된 열에서 사용자 계정 만들기 링크를 클릭 합니다. 이 데는 `~/Membership/CreatingUserAccounts.aspx` 1 단계만에 구성한에서 Tito에 대 한 액세스를 허용 하는 페이지입니다. 익명 사용자는 금지 하므로 `FormsAuthenticationModule` 우리 로그인 페이지로 리디렉션합니다.

익명 하는 시점에서 하므로 `Request.IsAuthenticated` 반환 `false` 에 리디렉션되지 우리 및 `UnauthorizedAccess.aspx`합니다. 대신, 로그인 페이지가 표시 됩니다. 1 세 같은 Tito가 아닌 사용자로 로그인 합니다. 적절 한 자격 증명을 입력 한 후 로그인 페이지에 다시 우리 리디렉션을 `~/Membership/CreatingUserAccounts.aspx`합니다. 그러나이 페이지를 Tito에 액세스할 수만 있으므로에서는 볼 수 있는 권한이 있으며 신속 하 게 반환 됩니다 로그인 페이지에. 그러나이 시간 `Request.IsAuthenticated` 반환 `true` (및 `ReturnUrl` querystring 매개 변수가 있는지) 이므로 우리는 리디렉션됩니다는 `UnauthorizedAccess.aspx` 페이지.


[![인증, 권한 없는 사용자는 리디렉션됩니다 UnauthorizedAccess.aspx](user-based-authorization-cs/_static/image17.png)](user-based-authorization-cs/_static/image16.png)

**그림 6**: 인증, 권한 없는 사용자는 리디렉션됩니다 `UnauthorizedAccess.aspx` ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image18.png))


이 사용자 지정 된 워크플로 짧은 단락 circuit 그림 2에 표시 된 주기에서 보다 적절 하 고 간단 하 게 사용자 환경을 제공 합니다.

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>현재 로그인된 한 사용자에 따라 기능을 제한 하는 3 단계:

URL 권한 부여 쉽게 거친 권한 부여 규칙을 지정할 수 있습니다. 1 단계에서에서 보았듯이 URL 권한 부여 म 간결 하 게 명시할 수 어떤 id는 허용 하 고 알림을 폴더에 있는 특정 페이지 또는 모든 페이지를 볼 수 없도록 거부 됩니다. 그러나 특정 시나리오에서 수 하려고 모든 사용자가 페이지를 방문 하십시오. 하지만 여기에 방문 하는 사용자를 기반으로 하는 페이지의 기능을 제한 하도록 허용 합니다.

인증 된 제품 검토 방문자를 허용 하는 전자 상거래 웹 사이트의 대/소문자를 고려 합니다. 익명 사용자는 제품의 페이지를 방문 제품 정보만 표시 되는 것은 및 리뷰를 남겨 수를 지정할 수 없습니다. 그러나 동일한 페이지를 방문 하는 인증된 된 사용자는 검토 인터페이스를 참조 합니다. 인증된 된 사용자가이 제품을 아직 검토 하지 않은, 하는 경우 인터페이스를 사용 하면; 검토를 제출 하도록 그렇지 않으면 나타납니다에 자신의 이전에 제출한 검토 합니다. 이 시나리오는 단계를 수행 하려면 뿐만 아니라 제품 페이지 수 추가 정보를 표시 있으며 전자 상거래 회사에 대해 작동 하는 해당 사용자에 대 한 확장된 기능을 제공 합니다. 예를 들어 제품 페이지 재고 인벤토리를 나열 하 고 제품의 가격 및 직원으로 방문 하는 경우 설명을 편집 하는 옵션을 포함할 수 있습니다.

선언적으로 또는 프로그래밍 방식 (또는 둘의 조합)에 이러한 세부적인 권한 부여 규칙을 구현할 수 있습니다. 다음 섹션에서 LoginView 컨트롤을 통해 세부적인 권한 부여를 구현 하는 방법을 살펴봅니다. 그런 다음, 프로그래밍 기술을 설명 합니다. 그러나 세부적인 권한 부여 규칙을 적용 살펴보면 전에 먼저 해야 해당 기능이 여기에 방문 하는 사용자에 따라 다릅니다. 페이지를 만듭니다.

GridView 내에서 특정 디렉터리의 파일을 나열 하는 페이지를 만들어 보겠습니다. 각 파일의 이름, 크기 및 기타 정보를 나열 하는, 함께 GridView linkbutton이 있는의 두 개의 열이 포함 됩니다: 하나 제목은 보기 및 제목이 지정된 삭제 합니다. 보기 LinkButton을 클릭 하면 선택한 파일의 내용이 표시 됩니다. 삭제 LinkButton을 클릭 하면 파일이 삭제 됩니다. 처음 만들겠습니다이 페이지의 보기 및 삭제 기능을 모든 사용자에 게 사용할 수 있도록 합니다. 사용에서 LoginView 컨트롤 및 프로그래밍 방식으로 제한 기능 섹션을 사용 하도록 설정 하거나 페이지를 방문 하는 사용자에 따라 이러한 기능을 사용 하지 않도록 설정 하는 방법을 살펴봅니다.

> [!NOTE]
> 작성 하려고 하는 ASP.NET 페이지 파일의 목록을 표시 하는 GridView 컨트롤을 사용 합니다. 이 자습서에서는 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 두고 시리즈 이후 하지 않음 GridView 컨트롤의 내부 작업에 논의 너무 많은 시간이 소비 하 합니다. 이 자습서에서이 페이지를 설정 하기 위한 특정 단계별 지침을 제공 하지만 특정 선택 사항이 이유 또는 렌더링된 된 출력에 효과 특정 속성의 세부 정보를 자세히 하지 않습니다. GridView 컨트롤의 철저 한 검사를 참조 하세요. 내 *[ASP.NET 2.0에서 데이터 작업](../../data-access/index.md)* 자습서 시리즈 합니다.


열어 시작는 `UserBasedAuthorization.aspx` 파일에 `Membership` 라는 페이지에 GridView 컨트롤 추가 같은 폴더 `FilesGrid`합니다. GridView의 스마트 태그에서 필드 대화 상자를 시작 하는 열 편집 링크를 클릭 합니다. 여기에서 왼쪽된 아래 모서리에서 자동 생성 필드 확인란의 선택을 취소 합니다. (선택 및 삭제 단추가 CommandField 형식에서 찾을 수 있습니다) 왼쪽된 위 모서리에서 선택 단추, 삭제 단추 및 두 개의 BoundFields를 다음으로 추가 합니다. 선택 단추 설정 `SelectText` 속성 보기 및 첫 번째 BoundField의을 `HeaderText` 및 `DataField` 속성 이름입니다. 두 번째 BoundField의 설정 `HeaderText` 속성 크기 (바이트)을 해당 `DataField` 길이에 대 한 속성 해당 `DataFormatString` {0: n0}에 대 한 속성 및 해당 `HtmlEncode` 속성을 false로 합니다.

GridView의 열을 구성한 후 필드 대화 상자를 닫으려면 확인을 클릭 합니다. 속성 창에서 설정 된 GridView `DataKeyNames` 속성을 `FullName`합니다. 이 시점에서 GridView의 선언적 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](user-based-authorization-cs/samples/sample9.aspx)]

GridView의 태그를 생성, म 특정 디렉터리의 파일을 검색 하 고 GridView에 바인딩할 수 있는 코드를 작성할 준비가 된 것입니다. 다음 코드는 페이지를 추가 `Page_Load` 이벤트 처리기.

[!code-csharp[Main](user-based-authorization-cs/samples/sample10.cs)]

위의 코드를 사용 하 여는 [ `DirectoryInfo` 클래스](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx) 응용 프로그램의 루트 폴더에 있는 파일의 목록을 가져올 수 있습니다. [ `GetFiles()` 메서드](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx) 배열로 서 디렉터리의 모든 파일 반환 [ `FileInfo` 개체](https://msdn.microsoft.com/library/system.io.fileinfo.aspx), GridView에 바인딩된 다음 합니다. `FileInfo` 개체와 같은 다양 한 속성에는 `Name`, `Length`, 및 `IsReadOnly`, 등입니다. 선언적 태그 알 수 있듯이 GridView 방금 표시는 `Name` 및 `Length` 속성입니다.

> [!NOTE]
> `DirectoryInfo` 및 `FileInfo` 에서 찾을 수 없는 클래스는 [ `System.IO` 네임 스페이스](https://msdn.microsoft.com/library/system.io.aspx)합니다. 따라서가를 앞에 이러한 클래스 이름은 네임 스페이스 이름으로, 아니면 클래스 파일에 가져온 네임 스페이스 (통해 `using System.IO`).


브라우저를 통해이 페이지를 방문 하 여 보십시오. 응용 프로그램의 루트 디렉터리에 있는 파일 목록이 표시 됩니다. 뷰 또는 링크 삭제 단추가 중 하나를 클릭 하면, 다시 게시 되지만 아직를 이유임 때문에 아무 작업도 발생 합니다 필요한 이벤트 처리기를 만들어야 합니다.


[![웹 응용 프로그램의 루트 디렉터리의 파일을 나열 하는 GridView](user-based-authorization-cs/_static/image20.png)](user-based-authorization-cs/_static/image19.png)

**그림 7**: 웹 응용 프로그램의 루트 디렉터리의 파일을 나열 하는 GridView ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image21.png))


선택한 파일의 내용을 표시 하는 수단 필요 합니다. Visual Studio로 돌아가서 라는 텍스트 상자 추가 `FileContents` GridView 위에 있습니다. 설정의 `TextMode` 속성을 `MultiLine` 및 해당 `Columns` 및 `Rows` 속성을 95% 및 10, 각각.

[!code-aspx[Main](user-based-authorization-cs/samples/sample11.aspx)]

다음으로 GridView에 대 한 이벤트 처리기를 만들고 [ `SelectedIndexChanged` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx) 다음 코드를 추가 합니다.

[!code-csharp[Main](user-based-authorization-cs/samples/sample12.cs)]

이 코드를 사용 하는 GridView 여 `SelectedValue` 선택한 파일의 전체 파일 이름을 확인 하는 속성입니다. 내부적으로 `DataKeys` 를 얻기 위해 컬렉션은 참조는 `SelectedValue`GridView의 설정 하는 명령적 큽니다 `DataKeyNames` 속성을 이름,이 단계에서 설명한 대로 합니다. [ `File` 클래스](https://msdn.microsoft.com/library/system.io.file.aspx) 다음에 할당 되는 문자열에 선택한 파일의 내용을 읽는 데 사용 되는 `FileContents` 텍스트 상자의 `Text` 페이지에서 선택한 파일의 내용을 표시할 속성입니다.


[![선택한 파일의 내용은 텍스트 상자에 표시 됩니다.](user-based-authorization-cs/_static/image23.png)](user-based-authorization-cs/_static/image22.png)

**그림 8**: 텍스트 상자에 선택한 파일의 내용이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image24.png))


> [!NOTE]
> HTML 태그를 포함 하는 파일의 내용을 보려면 다음 보기 또는 파일을 삭제 하려고 하는 경우 표시 됩니다는 `HttpRequestValidationException` 오류입니다. 텍스트 상자의 내용을 다시 게시 될 때 웹 서버에 다시 전송 되기 때문에 발생 합니다. 기본적으로 asp는 `HttpRequestValidationException` HTML 태그와 같은 잠재적으로 위험한 포스트백 콘텐츠 감지 될 때마다 오류입니다. 이 오류 발생을 사용 하지 않으려면 해제 페이지에 대 한 요청 유효성 검사를 추가 하 여 `ValidateRequest="false"` 에 `@Page` 지시문입니다. 요청 유효성 검사로 뿐만 아니라 예방 조치를 취해야 할 때의 이점에 대 한 자세한 내용은 사용 중지, 읽을 [요청 유효성 검사-스크립트 공격 방지](https://asp.net/learn/whitepapers/request-validation/)합니다.


GridView의에 대 한 이벤트 처리기를 다음 코드로 마지막으로 추가 [ `RowDeleting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx):

[!code-csharp[Main](user-based-authorization-cs/samples/sample13.cs)]

코드는 단순히에서 삭제할 파일의 전체 이름을 표시는 `FileContents` TextBox *없이* 실제로 파일을 삭제 합니다.


[![삭제 단추를 클릭 하면 실제로 삭제 되지 않습니다 파일](user-based-authorization-cs/_static/image26.png)](user-based-authorization-cs/_static/image25.png)

**그림 9**: 파일을 클릭 하 고 삭제 단추 실제로 삭제 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image27.png))


1 단계에서에서 구성한 URL 권한 부여 규칙에서 페이지를 볼 수 없도록 익명 사용자가 금지 하 고 `Membership` 폴더입니다. 더 잘 나타낼 세부적인 인증을 위해 보겠습니다 익명 사용자가 방문 하도록 허용 된 `UserBasedAuthorization.aspx` 페이지 된 제한 된 기능입니다. 이 페이지 모든 사용자가 액세스를 열려면 다음을 추가 `<location>` 요소는 `Web.config` 파일에 `Membership` 폴더:

[!code-xml[Main](user-based-authorization-cs/samples/sample14.xml)]

이 추가한 후 `<location>` 요소를 사이트에서 로그인 하 여 새 URL 권한 부여 규칙을 테스트 합니다. 익명 사용자로 있습니다 허용할지를 방문 하 여 `UserBasedAuthorization.aspx` 페이지.

모든 인증 또는 익명 사용자를 방문할 수 있는 현재는 `UserBasedAuthorization.aspx` 페이지 및 확인 하거나 파일을 삭제 합니다. 설정 파일을 삭제할 수만 Tito 하 고 인증 된 사용자만 파일의 내용을 볼 수 있도록 합니다. 선언적으로, 프로그래밍 방식으로 또는 두 방법의 조합을 사용 하 여 이러한 세부적인 권한 부여 규칙을 적용할 수 있습니다. 파일의 내용을 볼 수 있는 사용자 에게만 선언적 접근 방식 사용 파일을 삭제할 수 있는 사람을 제한할 프로그래밍 방식을 사용 합니다.

### <a name="using-the-loginview-control"></a>LoginView 컨트롤을 사용 하 여

지난 자습서에서 살펴본 대로 LoginView 컨트롤은 인증 되 고 익명 사용자에 대 한 다른 인터페이스를 표시 하는 데 유용 있으며 쉽게 익명 사용자가 액세스할 수 없는 기능을 숨길 수 있습니다. 익명 사용자가 보거나 파일을 삭제할 수 없습니다, 원하므로 해야 표시는 `FileContents` 인증된 된 사용자가 해당 페이지를 방문 하는 경우 텍스트 상자에 붙여넣습니다. 이 위해 페이지에 LoginView 컨트롤을 추가, 이름을 `LoginViewForFileContentsTextBox`, 이동 하 고는 `FileContents` LoginView 컨트롤에 선언적 태그를 텍스트 상자의 `LoggedInTemplate`합니다.

[!code-aspx[Main](user-based-authorization-cs/samples/sample15.aspx)]

LoginView의 서식 파일에서 웹 컨트롤을 코드 숨김 클래스에서 직접 액세스할 수 있는 더 이상. 예를 들어는 `FilesGrid` GridView의 `SelectedIndexChanged` 및 `RowDeleting` 이벤트 처리기를 현재 참조는 `FileContents` 코드를 있는 TextBox 컨트롤 같은:

[!code-csharp[Main](user-based-authorization-cs/samples/sample16.cs)]

그러나이 코드는 더 이상 유효 합니다. 이동 하 여는 `FileContents` 텍스트 상자에는 `LoggedInTemplate` TextBox에 직접 액세스할 수 없습니다. 대신 사용 해야 합니다는 `FindControl("controlId")` 프로그래밍 방식으로 컨트롤을 참조 하는 메서드. 업데이트는 `FilesGrid` 같이 TextBox를 참조 하는 이벤트 처리기.

[!code-csharp[Main](user-based-authorization-cs/samples/sample17.cs)]

텍스트 상자는 LoginView를 이동한 후 `LoggedInTemplate` 페이지의 코드를 사용 하 여 TextBox 참조를 업데이트 하 고는 `FindControl("controlId")` 패턴, 익명 사용자로 페이지를 방문 합니다. 그림 10과 같이 `FileContents` 텍스트 상자에 표시 되지 않습니다. 그러나 보기 LinkButton 계속 표시 됩니다.


[![LoginView 컨트롤에만 인증 된 사용자에 대 한 FileContents TextBox 렌더링](user-based-authorization-cs/_static/image29.png)](user-based-authorization-cs/_static/image28.png)

**그림 10**: The LoginView 컨트롤만 렌더링는 `FileContents` 인증 된 사용자에 대 한 텍스트 상자에 붙여넣습니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image30.png))


익명 사용자에 게 보기 단추를 숨기려면 가지 방법은 GridView 필드를 TemplateField로 변환 하는 것입니다. 이 보기 LinkButton에 대 한 선언적 태그를 포함 하는 서식 파일을 생성 됩니다. 다음에 TemplateField LoginView 컨트롤을 추가 LoginView의 내에서 LinkButton을 배치할 수 있습니다 `LoggedInTemplate`없어지고 익명 방문자 로부터 보기 단추 숨기기. 이를 위해 필드 대화 상자를 시작 하려면 스마트 태그는 GridView에서 열 편집 링크를 클릭 합니다. 다음에 왼쪽된 아래 모서리에 있는 목록에서 선택 단추를 선택 하 고이 필드를 TemplateField 링크 변환을 클릭 합니다. 이렇게 필드의 선언적 태그를 수정 합니다.

[!code-aspx[Main](user-based-authorization-cs/samples/sample18.aspx)]

 대상: 

[!code-aspx[Main](user-based-authorization-cs/samples/sample19.aspx)]

이 시점에서 LoginView는 TemplateField에 추가할 수 있습니다. 다음 태그 보기 LinkButton 인증 된 사용자에 대해서만 표시 됩니다.

[!code-aspx[Main](user-based-authorization-cs/samples/sample20.aspx)]

그림 11에서 볼 수 있듯이 최종 결과 하지 그는 상당히 보기로 열은 여전히 표시 열 내에서 보기 링크 단추가 숨겨진 경우에 합니다. 살펴보도록 하겠습니다 전체 GridView 열 (및 LinkButton 뿐 아니라) 숨기는 방법에는 다음 섹션에 있습니다.


[![LoginView 컨트롤 익명 방문자에 대 한 보기 링크 단추가 숨깁니다.](user-based-authorization-cs/_static/image32.png)](user-based-authorization-cs/_static/image31.png)

**그림 11**: LoginView 컨트롤 익명 방문자에 대 한 보기 링크 단추가 숨깁니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image33.png))


### <a name="programmatically-limiting-functionality"></a>기능을 프로그래밍 방식으로 제한

일부 환경에서는 선언적 기술을 페이지에 기능을 제한 하기 위한 충분 하지 않습니다. 예를 들어 특정 페이지 기능 가용성 조건 페이지를 방문 하는 사용자 인증 또는 익명 외에 종속 될 수 있습니다. 이런 경우에서 다양 한 사용자 인터페이스 요소 표시 하거나 숨길 수 프로그래밍 수단을 통해.

기능을 프로그래밍 방식으로 제한 하기 위해 두 가지 작업을 수행 해야 합니다.

1. 페이지를 방문 하는 사용자의 기능에 액세스할 수 있는지 여부를 확인 하 고
2. 프로그래밍 방식으로 사용자에 게 해당 기능에 액세스할 수 있는지 여부에 따라 사용자 인터페이스를 수정 합니다.

이러한 두 작업 중 응용 프로그램을 보여 주기 위해 Tito GridView에서 파일을 삭제만 허용 해 보겠습니다. 그런 다음이 첫 번째 작업 페이지를 방문 Tito 인지 확인 되려고 합니다. 일단 결정 되는 (표시 하거나 숨길 수) GridView의 열 삭제 해야 합니다. GridView의 열을 통해 액세스할 수 있는 해당 `Columns` 속성 열만 렌더링 되 면 해당 `Visible` 속성이 `true` (기본값).

다음 코드를 추가 하는 `Page_Load` GridView에 데이터를 바인딩하기 전에 이벤트 처리기.

[!code-csharp[Main](user-based-authorization-cs/samples/sample21.cs)]

설명한 것 처럼는 [ *폼 인증의 개요는* ](../introduction/an-overview-of-forms-authentication-cs.md) 자습서 `User.Identity.Name` id의 이름을 반환 합니다. Login 컨트롤에 입력 한 사용자 이름에 해당 합니다. 방문 페이지, GridView의 두 번째 열의 Tito 경우 `Visible` 속성이로 설정 되어 `true`, 그렇지 않으면로 설정 된 `false`합니다. 결과는 다른 인증 된 사용자 또는 익명 사용자 페이지를 방문 Tito 아닌 다른 동기화 그룹 열 삭제 렌더링 되지 않습니다 (그림 12 참조). 그러나 Tito 페이지를 방문 Delete 열이 있는 (그림 13 참조).


[![삭제할 열이 되지 렌더링 때 방문 하 여 다른 사람이 아닌 다른 Tito (예: 1 세)](user-based-authorization-cs/_static/image35.png)](user-based-authorization-cs/_static/image34.png)

**그림 12**: 열 삭제 되지 렌더링 때 방문 하 여 다른 사람이 아닌 다른 Tito (예: 1 세)은 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image36.png))


[![열 삭제 Tito 위해 렌더링](user-based-authorization-cs/_static/image38.png)](user-based-authorization-cs/_static/image37.png)

**그림 13**: Tito 위해 렌더링 하기 열 삭제 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image39.png))


## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>4 단계: 클래스 및 메서드를 권한 부여 규칙을 적용

3 단계에서는 익명 사용자가 파일의 내용을 볼 수 없습니다. 하 고 모든 사용자가 있지만 Tito에서 파일 삭제 금지 합니다. 이 연결 된 사용자 인터페이스 요소에 대해 선언적 방법과 프로그래밍 기술을 통해 무단 방문자가 숨기는 방식으로 수행 되었습니다. 간단한 예에서는 사용자 인터페이스 요소를 제대로 숨기기 되었으나 간단한 어떤 점이 더 복잡 한 사이트 동일한 기능을 수행 하는 많은 방법이 될 수 있는? 권한이 없는 사용자가 해당 기능을 제한에서 숨기 거 나 모든 적용 가능한 사용자 인터페이스 요소를 사용 하지 않도록 설정 하지 않으면는 것이 되나요?

해당 클래스 또는 메서드를 장식 하는 기능의 특정 부분 권한이 없는 사용자가 액세스할 수 없도록 하는 쉬운 방법을 [ `PrincipalPermission` 특성](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)합니다. .NET 런타임 클래스를 사용 하 여 또는 메서드 중 하나를 실행 하는 경우 현재 보안 컨텍스트 클래스를 사용 하거나 메서드를 실행할 수 있는 권한을 갖는지 확인을 확인 합니다. `PrincipalPermission` 특성은 이러한 규칙을 정의할 수 있습니다 하는 메커니즘을 제공 합니다.

사용 하 여 살펴보겠습니다는 `PrincipalPermission` GridView의 특성이 `SelectedIndexChanged` 및 `RowDeleting` 각각 Tito, 이외의 사용자가 익명 사용자로 실행 하지 못하도록 하는 이벤트 처리기입니다. 각 함수 정의 위에 적절 한 특성을 추가 해야 할 됩니다.

[!code-csharp[Main](user-based-authorization-cs/samples/sample22.cs)]

에 대 한 특성은 `SelectedIndexChanged` 인증 된 사용자만 이벤트 처리기 중에 특성으로 작업 하는 경우 이벤트 처리기를 실행할 수 있습니다는 `RowDeleting` 이벤트 처리기 실행 Tito 제한 합니다.

Tito 이외의 사용자가 실행 하려고 하는 경우는 `RowDeleting` 이벤트 처리기 또는 인증 되지 않은 사용자가 실행 하려고는 `SelectedIndexChanged` 이벤트 처리기는.NET 런타임에서 발생 한 `SecurityException`합니다.


[![보안 컨텍스트는 메서드를 실행할 수 있는 권한이 없습니다,는 SecurityException Throw](user-based-authorization-cs/_static/image41.png)](user-based-authorization-cs/_static/image40.png)

**그림 14**: 보안 컨텍스트는 메서드를 실행할 권한이 없는 경우는 `SecurityException` Throw 됩니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-cs/_static/image42.png))


> [!NOTE]
> 클래스 또는 메서드에 액세스할 수 있는 여러 보안 컨텍스트를 허용 하려면 클래스 또는 메서드를 데코레이팅하는 `PrincipalPermission` 각 보안 컨텍스트에 대 한 특성입니다. 즉, Tito와 1 세 모두 실행할 수 있도록는 `RowDeleting` 이벤트 처리기 추가 *두* `PrincipalPermission` 특성:


[!code-csharp[Main](user-based-authorization-cs/samples/sample23.cs)]

ASP.NET 페이지 외에도 많은 응용 프로그램은 레이블에도 비즈니스 논리 및 데이터 액세스 계층 등의 다양 한 계층을 포함 하는 아키텍처에 연결 합니다. 이러한 계층은 일반적으로 클래스 라이브러리로 구현 및 클래스와 비즈니스 논리 및 데이터 관련 기능을 수행 하기 위한 메서드를 제공 합니다. `PrincipalPermission` 특성은 이러한 계층에 권한 부여 규칙을 적용 하는 데 유용 합니다.

사용 하 여 대 한 자세한 내용은 `PrincipalPermission` 특성을 클래스 및 메서드에서 권한 부여 규칙을 정의 합니다 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [비즈니스 및 데이터 계층이 사용 권한부여규칙추가`PrincipalPermissionAttributes` ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>요약

이 자습서에서는 사용자 기반 권한 부여 규칙을 적용 하는 방법을 검토 합니다. ASP 보는 것으로 시작 했습니다. NET의 URL 권한 부여 프레임 워크입니다. 각 요청에서 ASP.NET 엔진의 `UrlAuthorizationModule` id가 요청 된 리소스에 액세스할 수 있는 권한이 있는지 확인 하는 응용 프로그램의 구성에 정의 된 URL 권한 부여 규칙을 검사 합니다. 즉, URL 권한 부여 쉽게는 특정 디렉터리에서 모든 페이지 또는 특정 페이지에 대 한 권한 부여 규칙을 지정할 수 있습니다.

URL 권한 부여 프레임 워크에서 페이지 단위로 권한 부여 규칙을 적용합니다. URL 권한 부여를 요청 id 또는 특정 리소스에 액세스할 수 있는 권한이 됩니다. 그러나 대부분의 시나리오는 더 세부적인 권한 부여 규칙에 대 한 호출합니다. 사용자가 페이지에 액세스할 수를 정의 하는 대신 everyone는 페이지에 액세스 하 하지만 서로 다른 데이터를 표시 하거나 페이지를 방문 하는 사용자에 따라 서로 다른 기능을 제공 해야 할 수 있습니다. 일반적으로 페이지 수준 권한 부여는 허용 되지 않는 기능에 액세스할 권한이 없는 사용자가 방지 하기 위해 특정 사용자 인터페이스 요소가 표시 작업이 포함 됩니다. 또한 특성 클래스 및 특정 사용자에 게 해당 메서드의 실행에 대 한 액세스를 제한 하는 데 수는 있습니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [비즈니스 및 데이터 계층을 사용 하 여 권한 부여 규칙 추가 `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [Iis 6 및 IIS7 보안 간의 변경 사항](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [특정 파일 및 하위 디렉터리를 구성합니다.](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [사용자를 기반으로 하는 데이터 수정 기능 제한](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs.md)
- [LoginView 컨트롤 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [IIS7 URL 권한 부여 이해](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` 기술 문서](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [ASP.NET 2.0에서에서 데이터 사용](../../data-access/index.md)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](validating-user-credentials-against-the-membership-user-store-cs.md)
> [다음](storing-additional-user-information-cs.md)
