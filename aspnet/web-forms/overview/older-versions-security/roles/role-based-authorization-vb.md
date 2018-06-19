---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-vb
title: 역할 기반 권한 부여 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서 역할 프레임 워크의 보안 컨텍스트와 사용자 역할에 연결 하는 방법을 보는 것으로 시작 합니다. 그런 다음 역할 기반 URL을 적용 하는 방법을 검사...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/24/2008
ms.topic: article
ms.assetid: 83b4f5a4-4f5a-4380-ba33-f0b5c5ac6a75
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ca92fd194ed36f55c58666145efe445fd92823b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892155"
---
<a name="role-based-authorization-vb"></a>역할 기반 권한 부여 (VB)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.11.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_vb.pdf)

> 이 자습서 역할 프레임 워크의 보안 컨텍스트와 사용자 역할에 연결 하는 방법을 보는 것으로 시작 합니다. 다음 역할 기반 URL 권한 부여 규칙을 적용 하는 방법을 설명 합니다. 표시 되는 데이터 및 ASP.NET 페이지의 기능 변경에 대 한 선언적 방법과 프로그래밍 방법을 사용 하 여 살펴보겠습니다, 수행 합니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서 URL 권한 부여를 사용 하 여 어떤 사용자가 페이지의 특정 집합을 방문할 수를 지정 하는 방법에 살펴보았습니다. 약간의 태그와 `Web.config`, ASP.NET 페이지를 방문 하 여 인증 된 사용자만을 허용 하도록 지시할 했습니다. 또는 Tito와 Bob 사용자만 허용 된 사항이 수 없습니다. 하거나 Sam 제외한 모든 인증 된 사용자가 허용 된 나타냅니다.

또한 URL 권한 부여 외에도 표시 되는 데이터 및 페이지 방문 하는 사용자에 따라 제공 하는 기능을 제어 하기 위한 선언적 방법과 프로그래밍 기법에 찾았습니다. 특히, 현재 디렉터리의 내용을 나열 하는 페이지를 만들었는지 여부입니다. 이 페이지를 방문 수 누구나 하지만 인증 된 사용자만 파일의 내용을 볼 수 있습니다 및 Tito만 파일을 삭제할 수 있습니다.

사용자가 사용자 단위로 권한 부여 규칙을 적용 부 기 밋으로 증가할 수 있습니다. 더 쉽게 유지 관리할 방법은 역할 기반 권한 부여를 사용 하는 것입니다. 다행 스럽게도 도구 권한 부여 규칙을 적용 하기 위한 우리의 처리에서 동일 하 게 작동 방식은 사용자 계정을 역할와 제대로 합니다. URL 권한 부여 규칙 사용자 대신 역할을 지정할 수 있습니다. 로그인된 한 사용자의 역할을 기반으로 하는 다른 콘텐츠를 표시 하려면 인증 되 고 익명 사용자에 대 한 다른 출력을 렌더링 하는 LoginView 컨트롤을 구성할 수 있습니다. 한 역할 API 로그인된 한 사용자의 역할을 결정 하기 위한 메서드를 포함 합니다.

이 자습서 역할 프레임 워크의 보안 컨텍스트와 사용자 역할에 연결 하는 방법을 보는 것으로 시작 합니다. 다음 역할 기반 URL 권한 부여 규칙을 적용 하는 방법을 설명 합니다. 표시 되는 데이터 및 ASP.NET 페이지의 기능 변경에 대 한 선언적 방법과 프로그래밍 방법을 사용 하 여 살펴보겠습니다, 수행 합니다. 이제 시작 하겠습니다.

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>어떻게 역할 이해 연관 된 사용자의 보안 컨텍스트

ASP.NET 파이프라인에 들어갈 때마다 요청자를 식별 하는 정보를 포함 하는 보안 컨텍스트를와 연결 됩니다. 폼 인증을 사용할 때는 인증 티켓 id 토큰으로 사용 됩니다. 설명한 것 처럼는 <a id="_msoanchor_2"> </a> [ *폼 인증의 개요는* ](../introduction/an-overview-of-forms-authentication-vb.md) 및 <a id="_msoanchor_3"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) 자습서는 `FormsAuthenticationModule` 결정 하는 동안에 요청자의 id는 [ `AuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx).

유효 하 고 만료 되지 않은 인증 티켓을이 없으면는 `FormsAuthenticationModule` 디코딩 요청자의 id를 확인 합니다. 만드는 새 `GenericPrincipal` 개체를 할당 하려면이 옵션은 `HttpContext.User` 개체입니다. 보안 주체가의 용도 같은 `GenericPrincipal`, 인증된 된 사용자의 이름 및 기능을 식별 하는 역할에 속하는 영업 관리자입니다. 이 용도로 확실할 모든 주 개체에 `Identity` 속성 및 `IsInRole(roleName)` 메서드. 그러나 `FormsAuthenticationModule`, 않습니다 역할 정보를 기록 하는 데 관심이 및 `GenericPrincipal` 개체 생성 된 모든 역할을 지정 하지 않습니다.

역할 프레임 워크를 사용 하는 경우는 [ `RoleManagerModule` ](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx) HTTP 모듈에서 다음 단계는 `FormsAuthenticationModule` 하는 동안 인증된 된 사용자의 역할을 설명 하 고는 [ `PostAuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)이며 후에 발생는 `AuthenticateRequest` 이벤트입니다. 인증된 된 사용자에서 요청이 시작 된 경우는 `RoleManagerModule` 덮어씁니다는 `GenericPrincipal` 하 여 만든 개체는 `FormsAuthenticationModule` 바꿉니다는 [ `RolePrincipal` 개체](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)합니다. `RolePrincipal` 클래스 역할 API를 사용 하 여 사용자가 속한 역할을 결정 합니다.

그림 1에서는 폼 인증 및 역할 프레임 워크를 사용 하는 경우 ASP.NET 파이프라인 워크플로를 보여 줍니다. `FormsAuthenticationModule` , 먼저 실행 하 고, 그녀의 인증 티켓을 통해 사용자를 식별 하 고, 새 `GenericPrincipal` 개체입니다. 다음으로 `RoleManagerModule` 의 단계를 하 고 덮어씁니다는 `GenericPrincipal` 개체는 `RolePrincipal` 개체입니다.

익명 사용자도는 사이트를 방문 하는 경우는 `FormsAuthenticationModule` 와 `RoleManagerModule` 정책 개체를 만듭니다.


[![폼 인증 및 역할 프레임 워크를 사용 하는 경우 인증된 된 사용자에 대 한 ASP.NET 파이프라인 이벤트](role-based-authorization-vb/_static/image2.png)](role-based-authorization-vb/_static/image1.png)

**그림 1**: The ASP.NET 파이프라인 이벤트는 인증 된 사용자 때 사용 하 여 폼 인증 및 역할 프레임 워크에 대 한 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image3.png))


### <a name="caching-role-information-in-a-cookie"></a>쿠키에서 캐싱 역할 정보

`RolePrincipal` 개체의 `IsInRole(roleName)` 메서드 호출 `Roles`합니다.`GetRolesForUser` 사용자의 멤버 인지를 확인 하기 위해 사용자에 대 한 역할을 가져올 *roleName*합니다. 사용 하는 경우는 `SqlRoleProvider`,이 인해 쿼리 역할 저장소 데이터베이스에 있습니다. 역할 기반 URL 권한 부여 규칙을 사용 하는 경우는 `RolePrincipal`의 `IsInRole` 메서드가 역할 기반 URL 권한 부여 규칙에 의해 보호 되는 페이지를 요청할 때마다 호출 됩니다. 모든 요청에서 데이터베이스에 역할 정보를 조회 하는 것 보다는 `Roles` 프레임 워크를 쿠키에 사용자의 역할을 캐시 하는 옵션을 포함 합니다.

역할 프레임 워크를 쿠키에 사용자의 역할을 캐시 하도록 구성 된 경우는 `RoleManagerModule` ASP.NET 파이프라인 하는 동안 쿠키 만듭니다 [ `EndRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)합니다. 후속 요청에서이 쿠키를 사용 하는 `PostAuthenticateRequest`때 되는 `RolePrincipal` 개체가 만들어집니다. 쿠키의 데이터를 구문 분석 되 고 사용자의 역할을 줄여줍니다를 채우는 데 사용할 경우 쿠키가 유효 하 고 만료 되지 않았는지는 `RolePrincipal` 에 대 한 호출을 만드는 것은 `Roles` 사용자의 역할을 확인 하려면 클래스입니다. 그림 2는이 워크플로 보여 줍니다.


[![성능 향상을 위해 쿠키에 사용자의 역할 정보를 저장할 수 있습니다.](role-based-authorization-vb/_static/image5.png)](role-based-authorization-vb/_static/image4.png)

**그림 2**: 사용자 역할 정보에에서 저장할 수 성능 개선 하는 쿠키 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image6.png))


역할 캐시 쿠키 메커니즘은 기본적으로 비활성화 됩니다. 통해 사용할 수 있습니다는 `<roleManager>`;에서 구성 태그 `Web.config`합니다. 사용 하 여 논의 [ `<roleManager>` 요소](https://msdn.microsoft.com/library/ms164660.aspx) 의 역할 공급자를 지정 하는 <a id="_msoanchor_4"> </a> [ *만들기 및 역할 관리* ](creating-and-managing-roles-vb.md) 자습서 이 요소 응용 프로그램에 이미 있어야 하므로 `Web.config` 파일입니다. 특성으로 지정 된 역할 캐시 쿠키 설정은 `<roleManager>`; 표 1에 대 한 요소를 요약 합니다.

> [!NOTE]
> 표 1에 나와 있는 구성 설정이 결과 역할 캐시 쿠키의 속성을 지정 합니다. 에 대 한 자세한 내용은 쿠키, 작동 방법 및 다양 한 속성을 [이 쿠키 자습서](http://www.quirksmode.org/js/cookies.html)합니다.


| <strong>Property</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>설명</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              쿠키 캐싱 사용 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     역할 캐시 쿠키의 이름입니다. 기본값은 ". ASPXROLES "입니다.                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                역할 이름 쿠키에 대 한 경로입니다. Path 특성에는 개발자를 특정 디렉터리 계층 구조를 쿠키의 범위를 제한할 수 있습니다. 기본값은 "/", 도메인에 대 한 모든 요청을 인증 티켓 쿠키를 보낼 브라우저에 게 알립니다.                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               역할 캐시 쿠키를 보호 하기 위해 어떤 기술을 사용을 나타냅니다. 허용 가능한 값은: `All` (기본값); `Encryption`; `None`; 및 `Validation`합니다. 3 단계로 다시 참조는 <a id="_anchor_5"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) 이러한 보호 수준에 대 한 자세한 내용은 자습서입니다.                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   인증 쿠키를 전송 하는 SSL 연결이 필요한 지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  사용자가 단일 세션에서 사이트를 방문할 쿠키의 시간 초과 될 때마다 다시 설정 하는지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다. 이 값은 관련 때 `createPersistentCookie` 로 설정 된 `true`합니다.                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         인증 티켓 쿠키가 만료 된 후 분 후에는 시간을 지정 합니다. 기본값은 `30`입니다. 이 값은 관련 때 `createPersistentCookie` 로 설정 된 `true`합니다.                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   역할 캐시 쿠키는 세션 쿠키 또는 영구 쿠키 여부를 지정 하는 부울 값입니다. 경우 `false` (기본값) 이면 브라우저를 닫을 때 삭제 되는 세션 쿠키 사용 됩니다. 경우 `true`, 영구 쿠키 사용 됩니다; 만료 `cookieTimeout` 시간 만들어진 후에 또는 값에 따라 이전 방문 후 숫자 `cookieSlidingExpiration`합니다.                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 쿠키의 도메인 값을 지정합니다. 기본값은 빈 문자열입니다 (예: www.yourdomain.com) 발급 도메인을 사용 하도록 브라우저. 이 경우 쿠키를 <strong>하지</strong> admin.yourdomain.com 같은 하위 도메인을 요청 하면 보낼 수 있습니다. 사용자 지정 해야 하는 모든 하위 도메인에 전달할 쿠키 하려는 경우는 `domain` 특성을 "yourdomain.com"로 설정 합니다.                                                                                                                                                 |
|    `maxCachedResults`     | 쿠키에 캐시 되는 역할 이름의 최대 수를 지정 합니다. 기본값은 25입니다. `RoleManagerModule` 에 속하는 사용자에 대 한 쿠키를 만들지 않습니다 이상 `maxCachedResults` 역할입니다. 따라서는 `RolePrincipal` 개체의 `IsInRole` 메서드를 사용 합니다는 `Roles` 사용자의 역할을 확인 하려면 클래스입니다. 이유 `maxCachedResults` 존재는 많은 사용자 에이전트는 4, 096 바이트 보다 큰 쿠키를 허용 하지 않기 때문입니다. 따라서이 cap이 크기 제한 초과의 가능성을 위한 것입니다. 보다 작은 지정 하는 것이 좋습니다 하려는 매우 긴 역할 이름이 있는 경우 `maxCachedResults` 값; contrariwise, 매우 짧은 역할 이름이 있는 경우 아마도이 값 늘릴 수 있습니다이 있습니다. |

**표 1**: 역할 캐시 쿠키 구성 옵션

보겠습니다 비 영구적인 역할 캐시 쿠키를 사용 하도록 응용 프로그램을 구성 합니다. 이를 위해 업데이트 된 `<roleManager>` 요소에 `Web.config` 다음 쿠키와 관련 된 특성을 포함 하려면:

[!code-xml[Main](role-based-authorization-vb/samples/sample1.xml)]

업데이트는 `<roleManager>`; 세 가지 특성을 추가 하 여 요소: `cacheRolesInCookie`, `createPersistentCookie`, 및 `cookieProtection`합니다. 설정 하 여 `cacheRolesInCookie` 를 `true`, `RoleManagerModule` 각 요청에 사용자의 역할 정보를 조회 하는 대신는 이제 자동으로 캐시를 쿠키에 사용자의 역할입니다. 명시적으로 설정 된 `createPersistentCookie` 및 `cookieProtection` 특성을 `false` 및 `All`각각. 기술적으로 영구 쿠키를 사용 하지 않습니다 및 암호화 하 고 유효성을 검사 쿠키를 모두 해제 하는 방금 해당 기본값에 해당 지정한 있지만 I에 넣으십시오를 명시적으로 확인 하므로 이러한 특성에 대 한 값을 지정 해야 하지 않았습니다.

그을 마쳤습니다. 예측이 역할 프레임 워크는 쿠키에 사용자의 역할을 캐시 합니다. 사용자의 브라우저에서 쿠키를 지원 하지 않거나 해당 쿠키에서 삭제 되거나 분실 하는 경우 어떻게 하 든,를 간단 –는 `RolePrincipal` 개체를 사용 합니다는 `Roles` 쿠키가 없는 (또는 잘못 되었거나 만료 된 하나)은 사용할 수 있는 경우에는 클래스입니다.

> [!NOTE]
> Microsoft의 Patterns &amp; 사례 그룹 영구적 역할 캐시 쿠키를 사용할 수 없게 합니다. 해커가 유효한 사용자의 쿠키에 액세스할 될 수 있는 경우 역할 캐시 쿠키를 소유한 역할 멤버 자격 증명에 충분 한 이므로 해당 사용자를 가장할 수 그 합니다. 이 문제가 발생할 가능성 쿠키는 사용자의 브라우저에 유지 하는 경우에 증가 합니다. 기타 보안 고려 사항:이 보안 권장 사항에 대 한 자세한 내용은 참조는 [ASP.NET 2.0에 대 한 보안 질문 목록](https://msdn.microsoft.com/library/ms998375.aspx)합니다.


## <a name="step-1-defining-role-based-url-authorization-rules"></a>1 단계: 역할 기반 URL 권한 부여 규칙 정의

에 설명 된 대로 <a id="_msoanchor_6"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서, URL 권한 부여-사용자 또는 역할에서 역할에는 페이지 집합에 대 한 액세스를 제한 하는 수단을 제공 합니다 기초로 사용 됩니다. URL 권한 부여 규칙에 명시 된 `Web.config` 를 사용 하는 [ `<authorization>` 요소](https://msdn.microsoft.com/library/8d82143t.aspx) 와 `<allow>` 및 `<deny>` 자식 요소입니다. 이전 자습서에서 설명 하는 사용자와 관련 된 권한 부여 규칙 외에 각 `<allow>` 및 `<deny>` 자식 요소가 포함 될 수도 있습니다.

- 특정 역할
- 역할의 쉼표로 구분 된 목록

예를 들어, URL 권한 부여 규칙 관리자 및 감독자 역할에 해당 사용자에 게 액세스 권한을 부여 하는 다른 모든 사용자에 대 한 액세스를 거부:

[!code-xml[Main](role-based-authorization-vb/samples/sample2.xml)]

`<allow>` 위의 태그 요소에에서는 관리자 및 감독자 역할은 허용 되지만 상태는 `<deny>`; 요소에 지시 하는 *모든* 사용자는 거부 됩니다.

응용 프로그램 구성 되도록는 `ManageRoles.aspx`, `UsersAndRoles.aspx`, 및 `CreateUserWizardWithRoles.aspx` 페이지는 해당 사용자가 관리자 역할에 액세스할 수만 동안는 `RoleBasedAuthorization.aspx` 페이지 모든 방문자에 게 액세스할 수 있는 상태로 유지 됩니다.

이를 위해 추가 하 여 시작 된 `Web.config` 파일을 `Roles` 폴더입니다.


[![역할 디렉터리에 Web.config 파일 추가](role-based-authorization-vb/_static/image8.png)](role-based-authorization-vb/_static/image7.png)

**그림 3**: 추가 된 `Web.config` 파일을 여 `Roles` 디렉터리 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image9.png))


다음 구성 태그를 다음으로 추가 `Web.config`:

[!code-xml[Main](role-based-authorization-vb/samples/sample3.xml)]

`<authorization>` 요소에는 `<system.web>` 구역 관리자 역할에 사용자만에 ASP.NET 리소스에 액세스할 수 있도록 나타냅니다는 `Roles` 디렉터리입니다. `<location>` 요소는 다른 집합에 대 한 URL 권한 부여 규칙을 정의 `RoleBasedAuthorization.aspx` 페이지에서 페이지를 방문 하는 모든 사용자가 허용 합니다.

변경 내용을 저장 한 후 `Web.config`, 관리자 역할에 없는 사용자로 로그인 한 후 보호 되는 페이지 중 하나를 방문 하십시오. `UrlAuthorizationModule` 는 요청된 된 리소스; 방문 권한이 감지 따라서는 `FormsAuthenticationModule` 로그인 페이지로 리디렉션합니다. 로그인 페이지를 수 있습니다 다음으로 리디렉션하는 `UnauthorizedAccess.aspx` 페이지 (그림 4 참조). 로그인 페이지에서이 최종 리디렉션을 `UnauthorizedAccess.aspx` 의 2 단계에서에서 로그인 페이지에 추가 된 때문에 발생는 <a id="_msoanchor_7"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서입니다. 로그인 페이지에 모든 인증 된 사용자를 자동으로 리디렉션합니다 특히 `UnauthorizedAccess.aspx` 쿼리 문자열을 포함 하는 경우는 `ReturnUrl` 매개 변수를이 매개 변수도 하지는 않았다고 페이지를 시도한 후 사용자가 로그인 페이지에 도착 했음을 나타냅니다 볼 수 있는 권한이 있습니다.


[![관리자 역할에 사용자만 보호 되는 페이지를 볼 수 있습니다.](role-based-authorization-vb/_static/image11.png)](role-based-authorization-vb/_static/image10.png)

**그림 4**: 관리자 역할에 사용자만 보호 된 페이지를 볼 수 있습니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image12.png))


로그 오프 한 다음의 관리자 역할에 속하는 사용자로 로그인 합니다. 이제 세 개의 보호 된 페이지를 볼 수 있습니다.


[![Tito는 UsersAndRoles.aspx 페이지 때문에 그는 관리자 역할에 방문할 수 있는](role-based-authorization-vb/_static/image14.png)](role-based-authorization-vb/_static/image13.png)

**그림 5**: Tito 방문할 수 있는 `UsersAndRoles.aspx` 페이지 때문에 그는 관리자 역할에 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image15.png))


> [!NOTE]
> 역할 또는 사용자-에 대 한 URL 권한 부여 규칙 –를 지정 하는 경우에 중단 되는 규칙은 위쪽에서 한 번에 분석 된 하나씩 유의 해야 합니다. 사용자가 허용 하거나 거부, 경우에 따라 일치가 발생에 일치 항목이 발견 되는 즉시는 `<allow>` 또는 `<deny>` 요소입니다. **일치 하는 항목이 사용자 액세스 권한이 부여 됩니다.** 따라서 하나 이상의 사용자 계정에 대 한 액세스를 제한 하려는 경우 사용 하 여는 `<deny>` URL 권한 부여 구성에서 마지막 요소로 요소입니다. **URL 권한 부여 규칙 포함 되지 않은 경우는**`<deny>`**요소를 모든 사용자에 게 권한이 부여 됩니다.** URL 권한 부여 규칙은 분석 하는 방법에 대 한 보다 철저 한 설명을에 대 한 다시 참조는 "어떻게는 `UrlAuthorizationModule` 액세스를 부여 하거나 거부 권한 부여 규칙을 사용 하 여"의 섹션은 <a id="_msoanchor_8"> </a> [  *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서입니다.


## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>현재 로그인된 한 사용자의 역할을 기반으로 하는 기능을 제한 하는 2 단계:

URL 권한 부여는 어떤 id 상태 규칙 쉽게 거친 권한 부여를 지정 하는 허용 하 고 알림을 특정 페이지 (또는 폴더와 그 하위 폴더의 모든 페이지)를 볼 수 없도록 거부 됩니다. 그러나 일부 경우에는 페이지를 방문 있지만 방문한 사용자의 역할을 기반으로 하는 페이지의 기능을 제한할 수 있도록 하려고 수 합니다. 이 특정 역할에 속하는 사용자에 게 추가 기능을 제공 또는 사용자의 역할에 따라 표시 또는 숨기기 데이터 수반 될 수 있습니다.

선언적으로 또는 프로그래밍 방식 (또는 둘의 조합)에 이러한 세부적인 역할 기반 권한 부여 규칙을 구현할 수 있습니다. 다음 섹션에서 LoginView 컨트롤을 통해 세부적인 선언적 권한 부여를 구현 하는 방법을 살펴봅니다. 그런 다음, 프로그래밍 기술을 설명 합니다. 그러나 세부적인 권한 부여 규칙을 적용 살펴보면 전에 먼저 해야 해당 기능이 여기에 방문 하는 사용자의 역할에 따라 다릅니다. 페이지를 만듭니다.

GridView에 시스템에 사용자 계정을 모두 나열 하는 페이지를 만들어 보겠습니다. GridView에는 각 사용자의 사용자 이름, 전자 메일 주소, 마지막 로그인 날짜 및 사용자에 대 한 설명을 포함 됩니다. 각 사용자의 정보를 표시할 뿐 아니라 GridView은 편집을 포함 하 고 기능을 삭제 합니다. 처음에 편집이 페이지를 만들 하 고 모든 사용자에 게 사용할 수 있는 기능을 삭제 합니다. "LoginView 컨트롤 사용 하 여" 및 "프로그래밍 방식으로 제한 기능" 섹션을 사용 하도록 설정 하거나 방문한 사용자의 역할에 따라 이러한 기능을 사용 하지 않도록 설정 하는 방법을 살펴봅니다.

> [!NOTE]
> 작성 하려고 하는 ASP.NET 페이지 GridView 컨트롤을 사용 하 여 사용자 계정을 표시 합니다. 이 자습서에서는 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 두고 시리즈 이후 하지 않음 GridView 컨트롤의 내부 작업에 논의 너무 많은 시간이 소비 하 합니다. 이 자습서에서이 페이지를 설정 하기 위한 특정 단계별 지침을 제공 하지만 특정 선택 사항이 이유 또는 렌더링된 된 출력에 효과 특정 속성의 세부 정보를 자세히 하지 않습니다. GridView 컨트롤의 철저 한 검사를 체크 아웃 내 *[ASP.NET 2.0에서 데이터 작업](../../data-access/index.md)* 자습서 시리즈 합니다.


열어 시작는 `RoleBasedAuthorization.aspx` 페이지에 `Roles` 폴더입니다. 디자이너와 설정으로 페이지에서 GridView를 끌어 해당 `ID` 를 `UserGrid`합니다. 잠시 후에 호출 하는 코드 작성 하는 `Membership`합니다.`GetAllUsers` 메서드 결과 바인딩합니다 `MembershipUserCollection` GridView에는 개체입니다. `MembershipUserCollection` 포함 한 `MembershipUser` ; 시스템에서 각 사용자 계정에 대 한 개체 `MembershipUser` 개체에는 같은 속성이 `UserName`,`Email`,`LastLoginDate` 등입니다.

먼저 표를 사용자 계정에 바인딩하는 코드를 작성 했습니다 보겠습니다 정의 GridView의 필드입니다. GridView의 스마트 태그에서 필드 대화 상자를 시작 하려면 "열 편집" 링크를 클릭 합니다. 상자 (그림 6 참조). 여기에서 왼쪽된 아래 모서리에 있는 "필드 자동 생성" 확인란의 선택을 취소 합니다. 이 GridView는 CommandField 추가 편집 및 삭제 기능을 포함 하 고 설정 해야 하므로 해당 `ShowEditButton` 및 `ShowDeleteButton` 속성을 True로 합니다. 다음으로 표시 하기 위한 4 개의 필드를 추가 `UserName`, `Email`, `LastLoginDate`, 및 `Comment` 속성입니다. BoundField를 사용 하 여 두 개의 읽기 전용 속성에 대 한 (`UserName` 및 `LastLoginDate`) 및 두 편집 가능한 필드 TemplateFields (`Email` 및 `Comment`).

첫 번째 BoundField 디스플레이 `UserName` 속성; 설정의 `HeaderText` 및 `DataField` 속성 "UserName"을 합니다. 이 필드를 편집할 수 없습니다, 따라서 설정 해당 `ReadOnly` 속성을 True로 합니다. 구성에서 `LastLoginDate` BoundField 설정 하 여 해당 `HeaderText` "마지막 로그인" 및 해당 `DataField` "LastLoginDate"를 합니다. 날짜 및 시간) (대신 날짜만 표시 되도록이 BoundField의 출력의 서식을 지정 해 보겠습니다. 이를 위해이 BoundField 설정 `HtmlEncode` 속성을 false로 및 해당 `DataFormatString` 속성을 "{0: d}"입니다. 설정 된 `ReadOnly` 속성을 True로 합니다.

설정의 `HeaderText` 두 TemplateFields "Email" 및 "Comment"의 속성입니다.


[![GridView의 필드를 필드 대화 상자를 통해 구성할 수 있습니다.](role-based-authorization-vb/_static/image17.png)](role-based-authorization-vb/_static/image16.png)

**그림 6**: GridView의 필드 수 수 구성 통해 the 필드 대화 상자 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image18.png))


이제를 정의 해야는 `ItemTemplate` 및 `EditItemTemplate` "Email" 및 "주석" TemplateFields에 대 한 합니다. Label 웹 컨트롤을 각각의 추가 `ItemTemplates` 바인딩하고 해당 `Text` 속성을는 `Email` 및 `Comment` 속성을 각각.

"Email" TemplateField 라는 텍스트 상자를 추가 합니다. `Email` 를 해당 `EditItemTemplate` 바인딩하고 해당 `Text` 속성을는 `Email` 양방향 데이터 바인딩을 사용 하 여 속성입니다. RequiredFieldValidator 및 RegularExpressionValidator에 추가 `EditItemTemplate` 하는 전자 메일 속성을 편집 하는 방문자가 유효한 메일 주소를 입력 했는지 확인 합니다. "주석" TemplateField 라는 여러 줄 텍스트 상자 추가 `Comment` 를 해당 `EditItemTemplate`합니다. 텍스트 상자의 설정 `Columns` 및 `Rows` 40 고 4, 속성을 각각 다음 해당 `Text` 속성을는 `Comment` 양방향 데이터 바인딩을 사용 하 여 속성입니다.

이러한 TemplateFields를 구성한 후 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample4.aspx)]

편집 하거나 해당 사용자의 알아야는 사용자 계정을 삭제할 때 `UserName` 속성 값입니다. GridView의 설정 `DataKeyNames` 속성 "UserName"을이 정보는 GridView의를 통해 사용할 수 있도록 `DataKeys` 컬렉션입니다.

마지막으로, 페이지로 ValidationSummary 컨트롤을 추가 하 고 설정의 `ShowMessageBox` 속성을 True로 및 해당 `ShowSummary` 속성을 false로 합니다. 이러한 설정으로는 ValidationSummary 누락 되었거나 잘못 된 전자 메일 주소가 있는 사용자 계정을 편집 하려면 사용자가 클라이언트 쪽 경고를 표시 됩니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample5.aspx)]

이제이 페이지의 선언적 태그를 완성 했습니다. 다음 작업이에 GridView에 사용자 계정 집합을 바인딩하는 것입니다. 라는 메서드를 추가 `BindUserGrid` 에 `RoleBasedAuthorization.aspx` 바인딩하는 페이지의 코드 숨김 클래스는 `MembershipUserCollection` 반환한 `Membership.GetAllUsers` 에 `UserGrid` GridView입니다. 이 메서드를 호출 하는 `Page_Load` 이벤트 처리기에 첫 번째 페이지 방문 합니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample6.vb)]

이 코드가 브라우저를 통해 페이지를 방문 합니다. 그림 7에서 볼 수 있듯이 시스템에서 각 사용자 계정에 대 한 정보를 나열 하는 GridView 표시 되어야 합니다.


[![시스템에서 각 사용자에 대 한 정보를 나열 하는 UserGrid GridView](role-based-authorization-vb/_static/image20.png)](role-based-authorization-vb/_static/image19.png)

**그림 7**:는 `UserGrid` GridView 나열 정보에 대 한 각 시스템의 사용자 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image21.png))


> [!NOTE]
> `UserGrid` GridView 비페이징 인터페이스에 사용자를 모두 나열 합니다. 이 간단한 모눈 인터페이스 시나리오에 적합 하지 않은 있는 여러 가지 이상의 합니다. 한 가지 옵션 페이징을 사용 하도록 설정 하 여 GridView를 구성 하는 것입니다. `Membership.GetAllUsers` 메서드에 두 개의 오버 로드가: 하나 입력된 된 매개 변수를 허용 하 고 페이지 크기와 인덱스 페이지에 대 한 정수 값 고를 반환 하는 사용자의 하위 집합에 지정 된 하나 및 모든 사용자가 반환 합니다. 두 번째 오버 로드에 사용할 수 보다 효율적으로 페이지에서 사용자가 사용자 계정의 정확한 하위 집합만 반환 하므로 보다는 *모든* 그 중입니다. 수천 개의 사용자 계정이 있는 경우에 예를 들어 선택한 문자로 시작 했는데 사용자는 해당 사용자만 표시 하는 필터 기반 인터페이스를 고려 하는 것이 좋습니다. [ `Membership.FindUsersByName` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) 필터 기반 사용자 인터페이스 빌드에 적합 합니다. 이러한 인터페이스는 이후 자습서에서 빌드 살펴보겠습니다.


GridView 컨트롤은 기본 제공를 편집 및 컨트롤이 SqlDataSource 또는 ObjectDataSource 같은 올바르게 구성 된 데이터 소스 제어에 바인딩되어 있을 때 지원 삭제를 제공 합니다. 그러나 `UserGrid` GridView에 프로그래밍 방식으로 바인딩된 데이터에 있습니다; 따라서 이러한 두 작업을 수행 하는 코드를 작성 해야 합니다. 특히를 수집 해야 GridView의에 대 한 이벤트 처리기를 만들 `RowEditing`, `RowCancelingEdit`, `RowUpdating`, 및 `RowDeleting` 방문자 GridView의 클릭 될 때 발생 하는 이벤트와 편집 취소, 업데이트 또는 삭제 단추입니다.

GridView의에 대 한 이벤트 처리기를 만들어 시작 `RowEditing`, `RowCancelingEdit`, 및 `RowUpdating` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample7.vb)]

`RowEditing` 및 `RowCancelingEdit` 설정 하면 이벤트 처리기입니다. GridView의 `EditIndex` 속성과 다음 rebind 모눈에 계정을 사용자의 목록입니다. 관심 있는 항목에서 발생 하는 `RowUpdating` 이벤트 처리기입니다. 이 이벤트 처리기 데이터 유효 하 고 다음 가져와 하 여 시작는 `UserName` 에서 편집 된 사용자 계정의 값은 `DataKeys` 컬렉션입니다. `Email` 및 `Comment` 텍스트 상자에 두 개의 TemplateFields' `EditItemTemplate` s 프로그래밍 방식으로 참조 합니다. 자신의 `Text` 속성 편집 된 전자 메일 주소와 메모를 포함 합니다.

먼저 호출을 통해 작업을 수행 하기는 사용자의 정보를 가져와야 하는 멤버 API를 통해 사용자에 대 한 계정 업데이트 하기 위해 `Membership.GetUser(userName)`합니다. 반환 된 `MembershipUser` 개체의 `Email` 및 `Comment` 속성 그런 다음 편집 인터페이스에서 두 개의 텍스트 상자에 입력 된 값으로 업데이트 됩니다. 이러한 수정에 대 한 호출 함께 저장 되므로 마지막으로, [ `Membership.UpdateUser` ](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)합니다. `RowUpdating` 를 미리 편집 인터페이스에 GridView 되돌리면 이벤트 처리기를 완료 합니다.

다음으로 만듭니다는 `RowDeleting` RowDeleting 이벤트 처리기는 다음 코드를 추가 합니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample8.vb)]

밖으로 시작 되는 위의 이벤트 처리기는 `UserName` GridView의에서 값 `DataKeys` 컬렉션;이 `UserName` 다음 값은 멤버 자격 클래스에 [ `DeleteUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)합니다. `DeleteUser` 메서드 (예: 어떤 역할이이 사용자가 속한) 관련된 멤버 자격 데이터를 포함 하 여 시스템에서 사용자 계정을 삭제 합니다. 사용자, 모눈의 삭제 한 후 `EditIndex` (경우에 사용자 편집 모드에서 다른 행 되는 동안 삭제를 클릭)-1로 설정 및 `BindUserGrid` 메서드를 호출 합니다.

> [!NOTE]
> 삭제 단추는 모든 종류의 사용자 로부터 사용자 계정을 삭제 하기 전에 확인 필요 하지 않습니다. 확인해 추가할 특정 형태의 사용자에 게 확인을 실수로 삭제 되는 계정의 가능성을 줄일 수 있습니다. 작업을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자입니다. 이 방법에 대 한 자세한 내용은 참조 하십시오. [추가 클라이언트 쪽 확인 때 삭제](https://asp.net/learn/data-access/tutorial-42-vb.aspx)합니다.


이 페이지 예상 대로 작동 하는지 확인 합니다. 사용자 계정을 삭제할 수 있을 뿐만 아니라 모든 사용자의 전자 메일 주소 및 메모를 편집할 수 있습니다. 이후는 `RoleBasedAuthorization.aspx` 페이지는 모든 사용자가 액세스할 수, 모든 –도 익명 방문자 –이 페이지를 방문 하 고 편집할 수 있으며 사용자 계정을 삭제할! 사용자의 전자 메일 주소 및 메모, 감독자가 및 관리자 역할의 사용자만 편집할 수 있으며 관리자만 사용자 계정을 삭제할 수 있도록이 페이지를 업데이트 해 보겠습니다.

"LoginView 제어를 사용 하 여" 섹션 LoginView 컨트롤을 사용 하 여 지침을 사용자의 역할에 표시를 살펴 봅니다. 관리자 역할의 사용자가이 페이지를 방문 하는 경우 편집 하 고 사용자를 삭제 하는 방법에 지침은 제공 됩니다. 감독자 역할의 사용자도이 페이지에 도달 하면 사용자가 편집에 지침이 제공 됩니다. 및 방문자 익명 감독자 또는 관리자 역할에 없는 경우 편집 하거나 사용자 계정 정보를 삭제할 수 없는 설명 하는 메시지가 표시 됩니다. "프로그래밍 방식으로 제한 기능" 섹션에서는 프로그래밍 방식으로 표시 하거나 사용자의 역할에 따라 편집 및 삭제 단추가 숨기는 코드를 작성 합니다.

### <a name="using-the-loginview-control"></a>LoginView 컨트롤을 사용 하 여

지난 자습서에서 살펴본 대로 LoginView 컨트롤은 인증 되 고 익명 사용자에 대 한 다른 인터페이스를 표시 하는 데 유용 하지만 LoginView 컨트롤 사용자의 역할을 기반으로 하는 다른 태그를 표시 하려면 사용할 수도 있습니다. LoginView 컨트롤 방문한 사용자의 역할에 따라 다른 명령을 표시 하려면 사용 합니다.

위의 LoginView를 추가 하 여 시작 된 `UserGrid` GridView입니다. LoginView 컨트롤에 두 개의 기본 제공 템플릿을 한 앞에서 설명한, 대로: `AnonymousTemplate` 및 `LoggedInTemplate`합니다. 이러한 템플릿은 편집 하거나 모든 사용자 정보를 삭제할 수 없는 사용자에 게 알려 주는 모두에 대 한 간단한 메시지를 입력 합니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample9.aspx)]

외에 `AnonymousTemplate` 및 `LoggedInTemplate`, LoginView 컨트롤 포함 될 수 있습니다 *RoleGroups*, 역할 관련 템플릿은입니다. 단일 속성을 포함 하는 각 RoleGroup `Roles`는 RoleGroup 적용할 역할을 지정 하는 합니다. `Roles` (예: "Administrators")를 동일한 역할 또는 역할 (예: "관리자, 감독자")의 쉼표로 구분 된 목록에 속성을 설정할 수 있습니다.

RoleGroups를 관리 하려면 RoleGroup 컬렉션 편집기를 표시 하려면 컨트롤의 스마트 태그에서 "편집 RoleGroups" 링크를 클릭 합니다. 두 개의 새 RoleGroups를 추가 합니다. 첫 번째 RoleGroup의 설정 `Roles` 속성을 "Administrators"에서 두 번째 작업의 "감독자"입니다.


[![LoginView의 역할별 템플릿 RoleGroup 컬렉션 편집기를 통해 관리](role-based-authorization-vb/_static/image23.png)](role-based-authorization-vb/_static/image22.png)

**그림 8**: LoginView의 역할별 템플릿 the RoleGroup 컬렉션 편집기를 통해 관리 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image24.png))


확인을 클릭; RoleGroup 컬렉션 편집기를 닫습니다 이 업데이트를 포함 하도록 선언 태그 LoginView의는 `<RoleGroups>` 섹션는 `<asp:RoleGroup>` 각 RoleGroup에 대 한 자식 요소가 RoleGroup 컬렉션 편집기에서 정의 합니다. 처음에 나열 된 스마트 태그-LoginView의 "뷰" 드롭 다운 목록 또한 테이블만 `AnonymousTemplate` 및 `LoggedInTemplate` – 이제 추가 RoleGroups에도 포함 됩니다.

관리자 역할의 사용자가 편집 및 삭제에 대 한 지침을 표시 되어 사용자 계정을 편집 하는 방법에 대 한 표시 지침 감독자 역할에 사용자가 없도록는 RoleGroups를 편집 합니다. 다음과 같이 변경한 후 LoginView의 선언적 태그 다음과 비슷해야 합니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample10.aspx)]

다음과 같이 변경한 후 페이지를 저장 하 고 브라우저를 통해 방문. 먼저 익명 사용자로 페이지를 방문 합니다. 메시지를 표시 합니다, 그리고 "로그인 하지 않은 시스템에 있습니다. 따라서 편집 하거나 수 사용자 정보를 모두 삭제 합니다. " 그런 다음 인증된 된 사용자에 사용할 수 있지만 권한이 나 관리자 역할에 모두 아닌로 로그인 합니다. 이 시간 "없는 감독자 또는 관리자 역할의 멤버인 경우 메시지를 표시 됩니다. 따라서 편집 하거나 수 사용자 정보를 모두 삭제 합니다. "

다음으로 감독자 역할의 구성원 인 사용자로 로그인 합니다. 감독자 역할 관련 나타나야 합니다.이 시간 메시지 (그림 9 참조). 역할별 관리자가 표시 되어야 하는 역할 (그림 10 참조) 메시지 관리자에서 사용자로 로그인 하는 경우.


[![1 세 감독자 역할 관련 메시지 표시](role-based-authorization-vb/_static/image26.png)](role-based-authorization-vb/_static/image25.png)

**그림 9**: 1 세 감독자 역할 관련 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image27.png))


[![Tito는 관리자 역할 관련 메시지 표시](role-based-authorization-vb/_static/image29.png)](role-based-authorization-vb/_static/image28.png)

**그림 10**: Tito 관리자 역할 관련 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image30.png))


그림 9에 스크린 샷 및 10 표시는 LoginView만 렌더링 하나의 템플릿이 여러 템플릿을 적용 하는 경우에 합니다. 1 세 및 Tito 모두 로깅됩니다 사용자에 아직는 LoginView 일치 하는 RoleGroup만 렌더링 및 not는 `LoggedInTemplate`합니다. 또한 관리자와 감독자 역할에 속한 Tito 아직 LoginView 컨트롤 렌더링는 감독자 하는 대신 관리자가 역할 관련 파일 하나.

그림 11 LoginView 컨트롤을 렌더링 하는 서식 파일을 확인 하는 데 워크플로 보여 줍니다. 가 둘 이상의 RoleGroup 지정 LoginView 템플릿이 렌더링 되는지 확인은 *첫 번째* 일치 하는 RoleGroup 합니다. 즉, 첫 번째 RoleGroup으로 감독자 RoleGroup와 두 번째 관리자, 배치에서는 다음 Tito가이 페이지를 방문 하는 경우 그는 감독자 메시지가 표시 합니다.


[![LoginView 컨트롤의 렌더링 템플릿을 결정 하는 워크플로](role-based-authorization-vb/_static/image32.png)](role-based-authorization-vb/_static/image31.png)

**그림 11**: 결정 어떤 템플릿을 사용 하 여 렌더링 The LoginView 컨트롤의 워크플로 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image33.png))


### <a name="programmatically-limiting-functionality"></a>기능을 프로그래밍 방식으로 제한

LoginView 컨트롤 표시 되지만 페이지를 방문 하는 사용자의 역할에 따라 다른 명령을, 편집 및 취소 단추 계속 모두 표시 됩니다. 프로그래밍 방식으로 익명 방문자와 감독자 아니고 관리자 역할에 사용자에 대 한 연결 편집 및 삭제 단추를 숨기려면이 필요 합니다. 모든 관리자가 아닌 사용자에 대해 삭제 단추를 숨기려면이 필요 합니다. 이 수행 하기 위해 약간의 프로그래밍 방식으로 CommandField의 편집 하며 삭제할 링크 단추가 집합을 참조 하는 코드를 작성 하는 `Visible` 속성을 `False`필요한 경우.

CommandField에서 컨트롤을 프로그래밍 방식으로 참조 하는 가장 쉬운 방법은 먼저을 템플릿으로 변환 하는 합니다. 이를 위해 GridView의 스마트 태그에서 "열 편집" 링크를 클릭 하는 CommandField 현재 필드 목록에서 선택한 "이이 필드를 TemplateField로 변환" 링크를 클릭 합니다. 와 TemplateField는 CommandField 바뀝니다이 `ItemTemplate` 및 `EditItemTemplate`합니다. `ItemTemplate` 편집 하며 하는 동안 삭제 링크 단추가 포함 되어는 `EditItemTemplate` 업데이트 및 링크 취소 단추가 포함 합니다.


[![CommandField를 TemplateField로 변환](role-based-authorization-vb/_static/image35.png)](role-based-authorization-vb/_static/image34.png)

**그림 12**: TemplateField에는 CommandField 변환 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image36.png))


편집 하며 삭제할 링크 단추가에서 업데이트는 `ItemTemplate`설정 자신의 `ID` 속성의 값을 `EditButton` 및 `DeleteButton`각각.

[!code-aspx[Main](role-based-authorization-vb/samples/sample11.aspx)]

GridView에서 레코드를 열거 데이터 GridView에 바인딩될, 때마다 해당 `DataSource` 속성 해당 생성 `GridViewRow` 개체입니다. 각 `GridViewRow` 개체가 만들어지면는 `RowCreated` 이벤트가 발생 합니다. 권한이 없는 사용자가 편집 및 삭제 단추를 숨기면 하려면를이 이벤트에 대 한 이벤트 처리기를 만들고 편집 하며 삭제할 링크 단추가, 설정에 프로그래밍 방식으로 참조 해야 해당 `Visible` 속성 적절 하 게 합니다.

이벤트 처리기를 만들고는 `RowCreated` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample12.vb)]

`RowCreated` 이벤트에 대 한 실행 *모든* 머리글, 바닥글, 호출기 인터페이스 등을 포함 하 여 GridView 행. 만 다루는 편집 모드에 있지 데이터 행 (이후 편집 모드에서 행에 업데이트 및 취소 단추 편집 및 삭제 하는 대신) 하는 경우 편집 하며 삭제할 링크 단추가 프로그래밍 방식으로 참조 하려고 합니다. 이 검사에서 처리 되는 `If` 문.

편집 하며 삭제할 링크 단추가 참조 편집 모드에 있지 않은 데이터 행을 다루는 하는 경우 및 해당 `Visible` 속성에서 반환 하는 부울 값에 따라 설정 됩니다는 `User` 개체의 `IsInRole(roleName)` 메서드. `User` 개체가 참조 하 여 만든 사용자는 `RoleManagerModule`; 따라서는 `IsInRole(roleName)` 메서드 역할 API를 사용 하 여 현재 방문자에 속하는지 여부를 결정 *roleName*합니다.

> [!NOTE]
> 사용할 수도 역할 클래스를 직접 호출을 대체 `User.IsInRole(roleName)` 을 호출 하 여는 [ `Roles.IsUserInRole(roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)합니다. Principal 개체를 사용 하기로 `IsInRole(roleName)` 메서드이 예제에서 직접 역할 API를 사용 하 여 보다 더 효율적 이므로 합니다. 이 자습서의 앞부분에서 역할 관리자 캐시를 쿠키에 사용자의 역할을 구성 했습니다. 이 캐시 된 쿠키 데이터만 사용 하면 보안 주체의 `IsInRole(roleName)` 메서드는; 역할 API를 직접 호출에는 항상 역할 저장소에 이동 포함 합니다. 역할이 쿠키에 캐시 되지 않으므로 경우에 주 개체 호출 `IsInRole(roleName)` 요청 하는 동안 처음으로 결과 캐시에 대 한 호출 된 메서드가 일반적으로 더 효율적입니다. 역할 API을 반면에 캐싱을 수행 하지 않습니다. 때문에 `RowCreated` 이벤트는 GridView의 모든 행에 대해 한 번 발생를 사용 하 여 `User.IsInRole(roleName)` 반면 역할 저장소에 한 번만 포함 `Roles.IsUserInRole(roleName)` 필요 *N* 줄어들며, 여기서 *N* 은 눈금에 표시 하는 사용자 계정 수를 지정 합니다.


편집 단추 `Visible` 속성이 `True` 이 페이지를 방문 하는 사용자가 관리자 또는 감독자 역할;에 그렇지 않으면 설정은 `False`합니다. 삭제 단추 `Visible` 속성이 `True` 관리자 역할에 사용자가 경우에 합니다.

브라우저를 통해이 페이지를 테스트 합니다. 감독자 아니고 관리자 인 사용자 또는 익명 방문자도 페이지를 방문 하는 경우는 CommandField 비어 있습니다. 여전히 존재 하지만 편집 또는 삭제 하지 않고 씬 실버로 단추입니다.

> [!NOTE]
> CommandField 숨길 수는 모두 때 비 Supervisor와 관리자가 아닌이 페이지를 방문 합니다. I이 그대로 실행으로 판독기에 대 한 합니다.


[![비 감독자 및 관리자가 아닌 숨겨져 편집 및 삭제 단추](role-based-authorization-vb/_static/image38.png)](role-based-authorization-vb/_static/image37.png)

**그림 13**: The 편집 및 삭제 단추가 아닌 감독자 및 관리자가 아닌 숨겨집니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image39.png))


감독자 역할 (속하지만 관리자 역할에)에 속하는 사용자를 방문 하는 경우 그 편집 단추를 확인 합니다.


[![편집 단추가 감독자에 사용 가능 이면 삭제 단추 사라집니다.](role-based-authorization-vb/_static/image41.png)](role-based-authorization-vb/_static/image40.png)

**그림 14**: 동안 the 편집 단추는 감독자에 사용 가능, 삭제 단추는 숨겨집니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image42.png))


있으며 관리자가 방문 하는 경우 그녀 편집 및 삭제 단추에 대 한 액세스입니다.


[![편집 및 삭제 단추는 사용할 수만 관리자](role-based-authorization-vb/_static/image44.png)](role-based-authorization-vb/_static/image43.png)

**그림 15**: The 편집 및 삭제 단추가 개만 사용할 수 있는 관리자를 위한 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image45.png))


## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>3 단계: 클래스 및 메서드에 역할 기반 권한 부여 규칙을 적용

삭제만 관리자에 게 기능을 제한 하는 단계 2에서 감독자 및 관리자 역할에 사용자에 게 기능을 편집 합니다. 이 프로그래밍 기술을 통해 권한이 없는 사용자가 연결 된 사용자 인터페이스 요소 숨기는 방식으로 수행 되었습니다. 이러한 측정값 권한이 없는 사용자 권한 있는 작업을 수행할 수 됩니다 수 있는지를 보장 하지 않습니다. 나중에 추가 된 사용자 인터페이스 요소 또는 권한이 없는 사용자가 숨기려는 잊어버린 있을 수 있습니다. 또는 해커가 원하는 메서드를 실행 하 여 ASP.NET 페이지에 다른 방법으로 검색할 수 있습니다.

해당 클래스 또는 메서드를 장식 하는 기능의 특정 부분 권한이 없는 사용자가 액세스할 수 없도록 하는 쉬운 방법을 [ `PrincipalPermission` 특성](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)합니다. .NET 런타임 클래스를 사용 하 여 또는 메서드 중 하나를 실행 하는 경우 현재 보안 컨텍스트에 사용 권한을 확인 합니다. `PrincipalPermission` 특성은 이러한 규칙을 정의할 수 있습니다 하는 메커니즘을 제공 합니다.

사용 하 여 살펴보았습니다는 `PrincipalPermission` 다시 특성는 <a id="_msoanchor_9"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서입니다. 특히 여 GridView를 장식 하는 방법에 대해 살펴보았습니다 `SelectedIndexChanged` 및 `RowDeleting` 이벤트 처리기 것만 통해 이루어집니다 인증 된 사용자와 Tito, 각각 되도록 합니다. `PrincipalPermission` 특성의 역할과 마찬가지로 작동 합니다.

사용 하 여 살펴보겠습니다는 `PrincipalPermission` GridView의 특성이 `RowUpdating` 및 `RowDeleting` 승인 되지 않은 사용자에 대 한 실행을 (를) 금지 하는 이벤트 처리기입니다. 각 함수 정의 위에 적절 한 특성을 추가 해야 할 됩니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample13.vb)]

에 대 한 특성은 `RowUpdating` 이벤트 처리기 지정 즉 관리자나 감독자 역할에 속한 사용자만의 특성으로 작업 하는 경우 이벤트 처리기를 실행할 수는 `RowDeleting` 사용자의 관리자에 게 실행을 제한 하는 이벤트 처리기 역할입니다.


> [!NOTE]
> `PrincipalPermission` 특성은의 클래스로 표현 되는 `System.Security.Permissions` 네임 스페이스입니다. 에 추가 해야는 `Imports System.Security.Permissions` 문에이 네임 스페이스를 가져오는 코드 숨김 클래스 파일의 맨 위쪽에 있습니다.


하는 경우 어떻게 하 든, 관리자가 아닌 실행 하려고 하지만 `RowDeleting` 이벤트 처리기는 감독자 비 또는 관리자가 아닌 실행 하려는 경우 또는 `RowUpdating` 이벤트 처리기는.NET 런타임에서 발생 한 `SecurityException`합니다.


[![보안 컨텍스트는 메서드를 실행할 수 있는 권한이 없습니다,는 SecurityException Throw](role-based-authorization-vb/_static/image47.png)](role-based-authorization-vb/_static/image46.png)

**그림 16**: 보안 컨텍스트는 메서드를 실행할 권한이 없는 경우는 `SecurityException` Throw 됩니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image48.png))


ASP.NET 페이지 외에도 많은 응용 프로그램은 레이블에도 비즈니스 논리 및 데이터 액세스 계층 등의 다양 한 계층을 포함 하는 아키텍처에 연결 합니다. 이러한 계층은 일반적으로 클래스 라이브러리로 구현 및 클래스와 비즈니스 논리 및 데이터 관련 기능을 수행 하기 위한 메서드를 제공 합니다. `PrincipalPermission` 특성은도 이러한 계층에 권한 부여 규칙을 적용 하는 데 유용 합니다.

사용 하 여 대 한 자세한 내용은 `PrincipalPermission` 특성을 클래스 및 메서드에서 권한 부여 규칙을 정의 합니다 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [비즈니스 및 데이터 계층이 사용 권한부여규칙추가`PrincipalPermissionAttributes` ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>요약

이 자습서에서 개괄적인 지정 하는 방법을 살펴보았습니다 하 고 사용자의 역할에 따라 세부적인 권한 부여 규칙. ASP입니다. NET의 URL 권한 부여 기능에는 페이지 개발자를가 어떤 id 허용 또는 거부 페이지에 대 한 액세스를 지정할 수 있습니다. 다시에서 설명한 것 처럼는 <a id="_msoanchor_10"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서, URL 권한 부여 규칙은 사용자가 사용자 단위로 적용할 수 있습니다. 수도 적용 될 있습니다 역할-역할별 별로이 자습서의 1 단계에서에서 설명한 것 처럼 합니다.

프로그래밍 방식으로 또는 선언적으로 미세 권한 부여 규칙을 적용할 수 있습니다. 2 단계에서에서 방문한 사용자의 역할에 따라 서로 다른 출력을 렌더링 LoginView 컨트롤 RoleGroups 기능을 사용 하 여 살펴보았습니다. 또한 프로그래밍 방식으로 사용자 페이지의 기능을 적절 하 게 조정 하는 방법과 특정 역할에 속하는지 확인 하는 방법에 찾았습니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [비즈니스 및 데이터 계층을 사용 하 여 권한 부여 규칙 추가 `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필: 역할 작업](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [ASP.NET 2.0에 대 한 보안 질문 목록](https://msdn.microsoft.com/library/ms998375.aspx)
- [에 대 한 기술 문서는 `<roleManager>` 요소](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특히 감사 드립니다.

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Suchi Banerjee 및 Teresa 머피의 포함 됩니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](assigning-roles-to-users-vb.md)
