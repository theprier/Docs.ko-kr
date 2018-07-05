---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-vb
title: 역할 기반 권한 부여 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서를 살펴보고 역할 프레임 워크의 보안 컨텍스트를 사용 하 여 사용자의 역할에 연결 하는 방법을 시작 합니다. 다음 역할을 기준으로 URL을 적용 하는 방법을 검사 하는 중...
ms.author: aspnetcontent
ms.date: 03/24/2008
ms.assetid: 83b4f5a4-4f5a-4380-ba33-f0b5c5ac6a75
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: 6bf9e1f0832b811ce8e2033dd45f94dc3baaeea6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829647"
---
<a name="role-based-authorization-vb"></a>역할 기반 권한 부여 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.11.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_vb.pdf)

> 이 자습서를 살펴보고 역할 프레임 워크의 보안 컨텍스트를 사용 하 여 사용자의 역할에 연결 하는 방법을 시작 합니다. 다음 역할 기반 URL 권한 부여 규칙을 적용 하는 방법을 설명 합니다. 표시 되는 데이터 및 ASP.NET 페이지에서 제공 하는 기능 변경에 대 한 선언적 방법과 프로그래밍 방법을 사용 하 여 살펴보겠습니다는 다음과 같습니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서 URL 권한 부여를 사용 하 여 어떤 사용자 페이지의 특정 집합을 방문 하 여 수를 지정 하는 방법에 살펴보았습니다. 태그의 약간을 사용 하 여 `Web.config`, ASP.NET 페이지를 방문 하 여 인증 된 사용자만을 허용 하도록 지시 수 없습니다. 또는 우리가 수 Tito와 bob은 사용자만 허용 된 받아쓰기 Sam 제외 하 고 인증 된 모든 사용자 허용 되어 있는지를 나타냅니다.

URL 권한 부여 하는 것 외에도 살펴봤습니다 표시 되는 데이터 및 방문 하는 사용자를 기반으로 페이지에서 제공 하는 기능을 제어 하기 위한 선언적 방법과 프로그래밍 기법입니다. 특히 현재 디렉터리의 내용을 나열 하는 페이지를 만들었습니다. 이 페이지를 방문할 수 있습니다 누구나 하지만 인증 된 사용자만 파일의 내용을 볼 수 있습니다 및 Tito만 파일을 삭제할 수 없습니다.

사용자가 사용자 기준 권한 부여 규칙을 적용은 부 기 악몽으로 증가할 수 있습니다. 더 쉽게 유지 관리할 방법은 역할 기반 권한 부여를 사용 하는 것입니다. 좋은 소식은 권한 부여 규칙을 적용 하기 위한 우리의 폐기 도구 동일 하 게 작동 하는지와 사용자 계정에 대 한 역할을 잘 합니다. URL 권한 부여 규칙 사용자 대신 역할을 지정할 수 있습니다. 로그인된 한 사용자의 역할을 기반으로 하는 다른 콘텐츠를 표시 하려면 인증 및 익명 사용자에 대 한 다른 출력을 렌더링 하는 LoginView 컨트롤을 구성할 수 있습니다. 및 역할 API에 로그인된 한 사용자의 역할을 결정 하기 위한 메서드를 포함 합니다.

이 자습서를 살펴보고 역할 프레임 워크의 보안 컨텍스트를 사용 하 여 사용자의 역할에 연결 하는 방법을 시작 합니다. 다음 역할 기반 URL 권한 부여 규칙을 적용 하는 방법을 설명 합니다. 표시 되는 데이터 및 ASP.NET 페이지에서 제공 하는 기능 변경에 대 한 선언적 방법과 프로그래밍 방법을 사용 하 여 살펴보겠습니다는 다음과 같습니다. 이제 시작 하겠습니다.

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>이해 하는 방법을 역할 연관 된 사용자의 보안 컨텍스트

요청을 ASP.NET 파이프라인에 들어갈 때마다 요청자를 식별 하는 정보를 포함 하는 보안 컨텍스트를 사용 하 여 연결 됩니다. Forms 인증을 사용 하는 경우 인증 티켓 id 토큰으로 사용 됩니다. 설명한 대로 합니다 <a id="_msoanchor_2"> </a> [ *는 폼 인증 개요* ](../introduction/an-overview-of-forms-authentication-vb.md) 고 <a id="_msoanchor_3"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) 자습서를 `FormsAuthenticationModule` 결정 하는 동안 수행 하는 요청자의 id를 [ `AuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx).

유효 하 고 만료 되지 않은 인증 티켓을 있으면는 `FormsAuthenticationModule` 요청자의 id를 정확 하 게 디코딩합니다. 새로 만듭니다 `GenericPrincipal` 개체를 할당 하려면이 옵션은 `HttpContext.User` 개체입니다. 보안 주체에의 용도 같은 `GenericPrincipal`, 인증된 된 사용자 이름 및 식별 하는 자신이 속한 역할입니다. 목적은 분명 하 게 모든 보안 주체 개체는이 `Identity` 속성 및 `IsInRole(roleName)` 메서드. 그러나 합니다 `FormsAuthenticationModule`, 아닙니다 역할 정보를 기록 하는 데 관심이 및 `GenericPrincipal` 생성 하는 개체 역할을 지정 하지 않습니다.

역할 프레임 워크를 사용 하는 경우는 [ `RoleManagerModule` ](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx) HTTP 모듈에서 다음 단계는 `FormsAuthenticationModule` 하는 동안 인증된 된 사용자의 역할을 식별 하 고는 [ `PostAuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)는 후 발생 합니다 `AuthenticateRequest` 이벤트입니다. 인증된 된 사용자에서 요청이 시작 된 경우는 `RoleManagerModule` 덮어씁니다 합니다 `GenericPrincipal` 하 여 만든 개체를 `FormsAuthenticationModule` 바꿉니다를 [ `RolePrincipal` 개체](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx). `RolePrincipal` 클래스 역할 API를 사용 하 여 사용자가 속한 역할을 결정 합니다.

그림 1에서는 폼 인증 및 역할 프레임 워크를 사용 하는 경우 ASP.NET 파이프라인 워크플로를 보여 줍니다. 합니다 `FormsAuthenticationModule` , 먼저 실행 하 고, 자신의 인증 티켓을 통해 사용자를 식별 하 고, 새 `GenericPrincipal` 개체입니다. 다음으로 `RoleManagerModule` 를 덮어씁니다를 `GenericPrincipal` 개체를 `RolePrincipal` 개체입니다.

익명 사용자도 사이트를 방문 하는 경우는 `FormsAuthenticationModule` 또는 `RoleManagerModule` 보안 주체 개체를 만듭니다.


[![폼 인증 및 역할 프레임 워크를 사용 하는 경우 인증된 된 사용자에 대 한 ASP.NET 파이프라인 이벤트](role-based-authorization-vb/_static/image2.png)](role-based-authorization-vb/_static/image1.png)

**그림 1**: The ASP.NET 파이프라인 이벤트는 인증 된 사용자 때 사용 하 여 폼 인증 및 역할 프레임 워크에 대 한 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image3.png))


### <a name="caching-role-information-in-a-cookie"></a>쿠키에 캐싱 역할 정보

합니다 `RolePrincipal` 개체의 `IsInRole(roleName)` 메서드 호출 `Roles`합니다.`GetRolesForUser` 사용자의 멤버 인지 여부를 확인 하기 위해 사용자에 대 한 역할을 가져오려면 *roleName*합니다. 사용 하는 경우는 `SqlRoleProvider`,이 인해 쿼리에서 역할 저장소 데이터베이스에 있습니다. 역할 기반 URL 권한 부여 규칙을 사용 하는 경우는 `RolePrincipal`의 `IsInRole` 역할 기반 URL 권한 부여 규칙에 의해 보호 되는 페이지를 요청할 때마다 호출 됩니다. 모든 요청에는 데이터베이스의 역할 정보를 조회 하기 보다는 `Roles` 프레임 워크에 사용자의 역할이 쿠키에 캐시 하는 옵션이 있습니다.

역할 프레임 워크는 사용자의 역할이 쿠키에 캐시 하도록 구성 된 경우는 `RoleManagerModule` 하는 동안 ASP.NET 파이프라인의 쿠키를 만듭니다 [ `EndRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)합니다. 후속 요청에서이 쿠키를 사용 합니다 `PostAuthenticateRequest`, 하는 경우는 `RolePrincipal` 개체가 만들어집니다. 쿠키의 데이터를 구문 분석 되 고 저장 하 여 사용자의 역할을 채우는 데 쿠키 올바르고 만료 되지 않은 경우는 `RolePrincipal` 에 대 한 호출을 만드는 것을 `Roles` 사용자의 역할을 확인 하려면 클래스입니다. 그림 2에서는이 워크플로 보여 줍니다.


[![성능 향상을 위해 쿠키에 사용자의 역할 정보를 저장할 수 있습니다.](role-based-authorization-vb/_static/image5.png)](role-based-authorization-vb/_static/image4.png)

**그림 2**: 사용자의 역할 정보에에서 저장할 수 성능 향상에 대 한 쿠키 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image6.png))


역할 캐시 쿠키 메커니즘은 기본적으로 비활성화 됩니다. 통해 사용할 수는 `<roleManager>`; 구성 태그 `Web.config`합니다. 사용 하 여 설명한 합니다 [ `<roleManager>` 요소](https://msdn.microsoft.com/library/ms164660.aspx) 의 역할 공급자를 지정 하는 <a id="_msoanchor_4"> </a> [ *만들기 및 관리 역할* ](creating-and-managing-roles-vb.md) 자습서 응용 프로그램에서이 요소를 이미 해야 하므로 `Web.config` 파일입니다. 특성으로 지정 된 역할 캐시 쿠키 설정은 `<roleManager>`; 요소와는 표 1에 요약 되어 있습니다.

> [!NOTE]
> 표 1에 나와 있는 구성 설정이 결과 역할 캐시 쿠키의 속성을 지정 합니다. 쿠키, 그 작동 방법 및 다양 한 속성에 대 한 자세한 내용은 읽을 [이 쿠키 자습서](http://www.quirksmode.org/js/cookies.html)합니다.


| <strong>Property</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>설명</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              쿠키 캐싱 사용 되는지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     역할 캐시 쿠키의 이름입니다. 기본값은 ". ASPXROLES "로 설정 합니다.                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                역할 이름 쿠키에 대 한 경로입니다. Path 특성에는 개발자를 특정 디렉터리 계층 구조를 쿠키의 범위를 제한할 수 있습니다. 기본값은 "/"를 도메인에 대 한 모든 요청에서 인증 티켓 쿠키를 보낼 브라우저에 게 알립니다.                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               역할 캐시 쿠키를 보호 하기 위해 어떤 기술이 사용 되는지 나타냅니다. 허용 되는 값은: `All` (기본값). `Encryption`; `None`; 및 `Validation`합니다. 3 단계를 다시 참조를 <a id="_anchor_5"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) 이러한 보호 수준에 대 한 자세한 내용은 자습서입니다.                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   SSL 연결을 인증 쿠키를 전송 해야 하는지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  사용자가 단일 세션에서 사이트를 방문할 때마다 쿠키의 시간 초과 다시 설정 하는지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다. 이 값은만 관련 될 때 `createPersistentCookie` 로 설정 된 `true`합니다.                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         인증 티켓 쿠키 만료 되는 분 단위로 시간을 지정 합니다. 기본값은 `30`입니다. 이 값은만 관련 될 때 `createPersistentCookie` 로 설정 된 `true`합니다.                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   역할 캐시 쿠키는 세션 쿠키 또는 영구 쿠키 인지 여부를 지정 하는 부울 값입니다. 경우 `false` (기본값), 브라우저를 닫을 때 삭제 되는 세션 쿠키가 사용 됩니다. 하는 경우 `true`, 영구 쿠키는; 만료 되기 `cookieTimeout` 숫자 값에 따라 이전 방문을 만든 후 시간 (분) 이후로 `cookieSlidingExpiration`합니다.                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 쿠키의 도메인 값을 지정합니다. 기본값은 빈 문자열입니다 (예: www.yourdomain.com) 발급 된 도메인을 사용 하 여 브라우저는 합니다. 쿠키는이 예에서 <strong>되지</strong> admin.yourdomain.com 같은 하위 도메인을 위해 요청 하면 전송 합니다. 사용자 지정 해야 하는 모든 하위 도메인에 전달할 쿠키를 하려는 경우는 `domain` 특성을 "yourdomain.com"로 설정 합니다.                                                                                                                                                 |
|    `maxCachedResults`     | 쿠키에 캐시 되는 역할 이름의 최대 개수를 지정 합니다. 기본값은 25입니다. 합니다 `RoleManagerModule` 에 속한 사용자에 대 한 쿠키를 만들지 않으므로 둘 `maxCachedResults` 역할입니다. 따라서 합니다 `RolePrincipal` 개체의 `IsInRole` 메서드를 사용 합니다는 `Roles` 사용자의 역할을 확인 하려면 클래스입니다. 이유 `maxCachedResults` 존재 이므로 많은 사용자 에이전트는 4,096 바이트 보다 큰 쿠키를 허용 하지 않습니다. 따라서이 한도이 크기 제한을 초과의 가능성을 줄일 것입니다. 작은 지정 하려는 매우 긴 역할 이름에 있는 경우 `maxCachedResults` contrariwise, 아주 짧은 역할 이름에 있는 경우 아마도이 값 늘릴 수 있습니다이; 값입니다. |

**표 1**: 역할 캐시 쿠키 구성 옵션

비영구적 역할 캐시 쿠키를 사용 하도록 응용 프로그램을 구성 하겠습니다. 이를 위해 업데이트를 `<roleManager>` 요소에서 `Web.config` 다음 쿠키와 관련 된 특성을 포함 하려면:

[!code-xml[Main](role-based-authorization-vb/samples/sample1.xml)]

업데이트 합니다 `<roleManager>`; 세 가지 특성을 추가 하 여 요소: `cacheRolesInCookie`를 `createPersistentCookie`, 및 `cookieProtection`합니다. 설정 하 여 `cacheRolesInCookie` 하 `true`는 `RoleManagerModule` 각 요청에 사용자의 역할 정보를 조회 하는 대신는 이제 자동으로 캐시를 쿠키에 사용자의 역할입니다. 명시적으로 설정 합니다 `createPersistentCookie` 하 고 `cookieProtection` 특성을 `false` 및 `All`, 각각. 기술적으로 영구 쿠키를 사용 하지 않습니다 및 암호화 및 유효성 검사 쿠키를 둘 다 선택을 취소 하는 바로 해당 기본값으로 해당 할당 했지만 필자 여기에 해당 하도록 명시적으로 하므로 이러한 특성에 대 한 값을 지정 해야 하지 않았습니다.

이것이 전부입니다! 예측이 역할 프레임 워크는 사용자의 역할이 쿠키에 캐시 합니다. 사용자의 브라우저에서 쿠키를 지원 하지 않거나 쿠키 삭제 되거나 손실 되 면 어떻게 해서든를 별일이 – 합니다 `RolePrincipal` 개체를 사용 합니다 `Roles` 쿠키가 없는 (또는 잘못 되었거나 만료 된 항목을)를 사용할 수 있는지 경우에서 클래스.

> [!NOTE]
> Microsoft의 Patterns &amp; 사례 그룹 영구 역할 캐시 쿠키를 사용 하 여 동시성이 보장 합니다. 역할 캐시 쿠키를 소유한 경우 역할 멤버 자격을 증명 하기 위해 충분 한 해커는 유효한 사용자의 쿠키에 대 한 액세스를 얻으면 수 있으므로 해당 사용자를 가장할 수 있습니다. 일이 일어날 가능성에는 사용자의 브라우저에서 쿠키 유지 되 면 증가 합니다. 이 보안 권장 사항 뿐만 아니라 다른 보안 고려 사항에 대 한 자세한 내용은 참조는 [ASP.NET 2.0에 대 한 보안 질문 목록](https://msdn.microsoft.com/library/ms998375.aspx)합니다.


## <a name="step-1-defining-role-based-url-authorization-rules"></a>1 단계: 역할 기반 URL 권한 부여 규칙 정의

에 설명 된 대로 합니다 <a id="_msoanchor_6"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서, URL 권한 부여-사용자 또는 역할-역할별 페이지 집합에 대 한 액세스를 제한 하는 방법을 제공 합니다 기준입니다. URL 권한 부여 규칙에 명시 됩니다 `Web.config` 를 사용 하는 [ `<authorization>` 요소](https://msdn.microsoft.com/library/8d82143t.aspx) 사용 하 여 `<allow>` 및 `<deny>` 자식 요소입니다. 이전 자습서에서 설명 하는 사용자 관련 권한 부여 규칙 외에도 각 `<allow>` 고 `<deny>` 자식 요소를 포함할 수도 있습니다.

- 특정 역할
- 역할의 쉼표로 구분 된 목록

예를 들어, URL 권한 부여 규칙의 관리자 및 감독자 역할에 해당 사용자에 게 액세스 권한을 부여 하지만 다른 모든 사용자의 액세스 거부:

[!code-xml[Main](role-based-authorization-vb/samples/sample2.xml)]

`<allow>` 위의 태그의 요소에에서는 관리자 및 감독자 역할 허용 되는 상태는 `<deny>`; 요소에 지시 하는 *모든* 사용자는 거부 됩니다.

응용 프로그램을 구성 해 보겠습니다 되도록 합니다 `ManageRoles.aspx`, `UsersAndRoles.aspx`, 및 `CreateUserWizardWithRoles.aspx` 페이지는 관리자 역할에 해당 사용자에 게 액세스할 수만 하는 동안는 `RoleBasedAuthorization.aspx` 페이지 계속 모든 방문자에 게 액세스할 수 있습니다.

이를 위해 추가 하 여 시작 된 `Web.config` 파일을 `Roles` 폴더입니다.


[![역할 디렉터리에 Web.config 파일 추가](role-based-authorization-vb/_static/image8.png)](role-based-authorization-vb/_static/image7.png)

**그림 3**: 추가 된 `Web.config` 파일을 합니다 `Roles` 디렉터리 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-vb/_static/image9.png))


다음 구성 태그를 다음으로, 추가 `Web.config`:

[!code-xml[Main](role-based-authorization-vb/samples/sample3.xml)]

`<authorization>` 요소에는 `<system.web>` 구역 관리자 역할의 사용자만의 ASP.NET 리소스에 액세스할 수 있는지 나타냅니다는 `Roles` 디렉터리입니다. `<location>` 대체에 대 한 URL 권한 부여 규칙 집합을 정의 하는 요소는 `RoleBasedAuthorization.aspx` 페이지에서 페이지를 방문 하 여 모든 사용자 허용 합니다.

변경 내용을 저장 한 후 `Web.config`, 관리자 역할에 없는 사용자로 로그인 하 고 보호 되는 페이지 중 하나를 방문 하려고 합니다. 합니다 `UrlAuthorizationModule` 는 요청 된 리소스를 참조 하세요. 권한이 검색 결과적으로 `FormsAuthenticationModule` 로그인 페이지로 리디렉션합니다. 로그인 페이지는 다음 리디렉션 수를 `UnauthorizedAccess.aspx` 페이지 (그림 4 참조). 로그인 페이지에서이 최종 리디렉션 `UnauthorizedAccess.aspx` 의 2 단계에서에서 로그인 페이지에 추가한 코드 때문에 발생 합니다 <a id="_msoanchor_7"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서입니다. 특히, 로그인 페이지에 인증 된 모든 사용자를 자동으로 리디렉션합니다 `UnauthorizedAccess.aspx` 문자열을 포함 하는 경우는 `ReturnUrl` 매개 변수를이 매개 변수로 없습니다 그 페이지를 시도한 후 사용자가 로그인 페이지에 도착를 나타냅니다 볼 수 있는 권한이 있습니다.


[![관리자 역할의 사용자만 보호 되는 페이지를 볼 수 있습니다.](role-based-authorization-vb/_static/image11.png)](role-based-authorization-vb/_static/image10.png)

**그림 4**: 관리자 역할의 사용자만 보호 페이지를 볼 수 있습니다 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image12.png))


로그 오프 한 다음 관리자 역할에 있는 사용자로 로그인 합니다. 이제 보호 되는 세 개의 페이지를 볼 수 있게 해야 합니다.


[![Tito는 UsersAndRoles.aspx 페이지 있으므로 담당 하 고 관리자 역할에 방문할 수](role-based-authorization-vb/_static/image14.png)](role-based-authorization-vb/_static/image13.png)

**그림 5**: Tito 방문할 수는 `UsersAndRoles.aspx` 관리자 역할에는 페이지 때문에 그 ([클릭 하 여 큰 이미지 보기](role-based-authorization-vb/_static/image15.png))


> [!NOTE]
> URL 권한 부여 규칙 – 역할에 사용자 지정 때 중단 되는 규칙을 분석된 한 위쪽에서 한 번에 하나씩 염두에서에 두는 것이 중요 합니다. 사용자는 액세스가 허용 되거나 거부, 경우에 따라 일치 항목에서 찾을 수는 일치 하는 항목이 즉시는 `<allow>` 또는 `<deny>` 요소입니다. **일치 하는 항목이 없으면 사용자는 액세스 권한이 부여 됩니다.** 따라서 하나 이상의 사용자 계정에 대 한 액세스를 제한 하려는 경우 반드시 사용 하는 `<deny>` URL 권한 부여 구성에서 마지막 요소로 요소입니다. **URL 권한 부여 규칙에 포함 되지 않은 경우는**`<deny>`**요소인 모든 사용자에 게 부여 됩니다.** URL 권한 부여 규칙을 분석 하는 방법에 대 한 더 상세히 논의 다시 참조는 "하는 방법을 `UrlAuthorizationModule` 권한 부여 규칙을 사용 하 여 액세스를 부여 하거나 거부할" 섹션을 <a id="_msoanchor_8"> </a> [  *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서입니다.


## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>2 단계: 현재 로그인된 한 사용자의 역할을 기반으로 하는 기능 제한

URL 권한 부여는 어떤 id는 상태 규칙 쉽게 정교 하지 않은 권한 부여를 지정 하는 허용 하 고는 특정 페이지 (또는 폴더 및 하위 폴더의 모든 페이지) 보기에서 거부 됩니다. 그러나 일부 경우에 방문 페이지를 방문한 사용자의 역할을 기반으로 하는 페이지의 기능을 제한 하는 모든 사용자 허용 하려는 수 있습니다. 이 특정 역할에 속하는 사용자에 게 추가 기능을 제공 또는 사용자의 역할에 따라 표시 또는 숨김 데이터 수반 될 수 있습니다.

선언적으로 또는 프로그래밍 방식 (또는 둘의 조합)에 이러한 세부적으로 역할 기반 권한 부여 규칙을 구현할 수 있습니다. 다음 섹션에서 LoginView 컨트롤을 통해 세부적으로 선언적 권한 부여를 구현 하는 방법을 살펴보겠습니다. 그런 다음, 프로그래밍 기술을 살펴봅니다. 그러나 세부적으로 권한 부여 규칙을 적용할 살펴보면 전에 먼저 생성 해야 페이지 해당 기능이 여기에 방문 하는 사용자의 역할에 따라 달라 집니다.

GridView의 시스템에 사용자 계정을 모두 나열 하는 페이지를 만들어 보겠습니다. GridView에는 각 사용자의 사용자 이름, 전자 메일 주소, 마지막 로그인 날짜 및 사용자에 대 한 설명을 포함 됩니다. GridView 각 사용자의 정보를 표시 하는 것 외에도 편집 등이 기능을 삭제 합니다. 처음에 편집을 사용 하 여이 페이지를 만들기를 모든 사용자에 게 사용할 수 있는 기능을 삭제 합니다. "LoginView 컨트롤 사용 하 여" 및 "프로그래밍 방식으로 제한 기능" 섹션을 사용 하도록 설정 하거나 방문한 사용자의 역할에 따라 이러한 기능을 사용 하지 않도록 설정 하는 방법을 살펴보겠습니다.

> [!NOTE]
> ASP.NET 페이지 구축 하기는 GridView 컨트롤을 사용 하 여 사용자 계정을 표시. 계열 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 두고이 자습서에서는 이후는 너무 많은 시간을 GridView 컨트롤의 내부 작업에 설명 하지 않겠습니다. 이 자습서에서이 페이지를 설정 하기 위한 특정 단계별 지침을 제공 하지만 특정 변경한 이유는 렌더링 된 출력을 미치는 효과 특정 속성의 세부 정보를 자세히 하지 않습니다. GridView 컨트롤의 철저 한 검사를 체크 아웃 내 *[ASP.NET 2.0에서 데이터로 작업할](../../data-access/index.md)* 자습서 시리즈입니다.


열어서 시작 합니다 `RoleBasedAuthorization.aspx` 페이지에 `Roles` 폴더입니다. 디자이너와 집합에 페이지의 GridView를 끌어 해당 `ID` 에 `UserGrid`입니다. 잠시 후에 호출 하는 코드 작성을 `Membership`입니다.`GetAllUsers` 메서드 결과 바인딩합니다 `MembershipUserCollection` GridView에는 개체입니다. 합니다 `MembershipUserCollection` 포함 된 `MembershipUser` 시스템에서 각 사용자 계정에 대 한 개체 `MembershipUser` 개체와 같은 속성을 가질 `UserName`를`Email`,`LastLoginDate` 등입니다.

표에 사용자 계정에 바인딩하는 코드를 작성 하면서 보겠습니다 먼저 GridView의 필드 정의 합니다. GridView의 스마트 태그에서 필드 대화 상자를 시작 하는 "열 편집" 링크를 클릭 상자 (그림 6 참조). 여기에서 왼쪽된 아래 모서리에서 "자동 생성 필드" 확인란의 선택을 취소 합니다. 이 GridView를 CommandField 추가 편집 및 삭제 기능을 포함 하 고 설정할 것 이므로 해당 `ShowEditButton` 고 `ShowDeleteButton` 속성을 true로 합니다. 다음으로 표시 하기 위한 4 개의 필드를 추가 합니다 `UserName`, `Email`를 `LastLoginDate`, 및 `Comment` 속성입니다. BoundField를 사용 하 여 두 개의 읽기 전용 속성에 대 한 (`UserName` 하 고 `LastLoginDate`) 및 TemplateFields 두 편집 가능한 필드 (`Email` 및 `Comment`).

첫 번째 BoundField을 표시 합니다 `UserName` 속성; 집합 해당 `HeaderText` 및 `DataField` 속성 "UserName"으로 합니다. 이 필드는 편집할 수 없습니다, 설정 하므로 해당 `ReadOnly` 속성을 true로 합니다. 구성 합니다 `LastLoginDate` BoundField 설정 하 여 해당 `HeaderText` "마지막 로그인" 고 `DataField` "LastLoginDate"를 합니다. (날짜 및 시간) 대신 날짜만 표시 되도록이 BoundField의 출력에 서식을 지정 하겠습니다. 이렇게 하려면 설정이 BoundField `HtmlEncode` 속성을 false로 및 해당 `DataFormatString` 속성을 "{0:d}"입니다. 설정 된 `ReadOnly` 속성을 true로 합니다.

설정 된 `HeaderText` "Email" 및 "Comment" 두 TemplateFields의 속성입니다.


[![GridView의 필드를 필드 대화 상자를 통해 구성할 수 있습니다.](role-based-authorization-vb/_static/image17.png)](role-based-authorization-vb/_static/image16.png)

**그림 6**: GridView의 필드 수 수 구성 통해 the 필드 대화 상자 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image18.png))


이제 정의 해야 합니다 `ItemTemplate` 고 `EditItemTemplate` "Email" 및 "Comment" TemplateFields 합니다. 각 Label 웹 컨트롤을 추가 합니다 `ItemTemplates` 바인딩하고 해당 `Text` 속성을 합니다 `Email` 및 `Comment` 속성을 각각.

"Email" TemplateField 추가 라는 텍스트 상자 `Email` 에 해당 `EditItemTemplate` 바인딩하고 해당 `Text` 속성을는 `Email` 양방향 데이터 바인딩을 사용 하 여 속성입니다. RequiredFieldValidator 및 RegularExpressionValidator에 추가 된 `EditItemTemplate` 전자 메일 속성을 편집 하는 방문자가 유효한 전자 메일 주소를 입력 했는지 확인 합니다. "Comment" TemplateField 추가 명명 된 여러 줄 TextBox `Comment` 에 해당 `EditItemTemplate`합니다. TextBox의 설정 `Columns` 하 고 `Rows` 40 및 4에 속성 각각 바인딩하고 및 해당 `Text` 속성을는 `Comment` 양방향 데이터 바인딩을 사용 하 여 속성.

이러한 TemplateFields를 구성한 후 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample4.aspx)]

편집 하거나 해당 사용자의 알아야는 사용자 계정을 삭제할 때 `UserName` 속성 값입니다. GridView의 설정 `DataKeyNames` 속성이 "UserName"으로이 정보는 GridView의를 통해 사용할 수 있도록 `DataKeys` 컬렉션입니다.

마지막으로 페이지로 ValidationSummary 컨트롤을 추가 하 고 설정 해당 `ShowMessageBox` 속성을 true로 고 `ShowSummary` 속성을 false로 합니다. 이러한 설정을 사용 하 여는 ValidationSummary 사용자가 누락 되었거나 잘못 된 전자 메일 주소를 사용 하는 사용자 계정 편집 하려고 하는 경우 클라이언트 쪽 경고가 표시 됩니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample5.aspx)]

이 페이지의 선언적 태그를 이제 했습니다. 에서는 다음 작업이 GridView에 사용자 계정 집합을 바인딩하는 것입니다. 라는 메서드를 추가 `BindUserGrid` 에 `RoleBasedAuthorization.aspx` 바인딩하는 페이지의 코드 숨김 클래스는 `MembershipUserCollection` 반환한 `Membership.GetAllUsers` 에 `UserGrid` GridView. 이 메서드를 호출 합니다 `Page_Load` 첫 번째 페이지 방문의 이벤트 처리기입니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample6.vb)]

이 코드를 사용 하 여 브라우저를 통해 페이지를 방문 합니다. 그림 7에서 알 수 있듯이, 시스템에서 각 사용자 계정에 대 한 정보를 나열 하는 GridView 표시 되어야 합니다.


[![시스템에서 각 사용자에 대 한 정보를 나열 하는 UserGrid GridView](role-based-authorization-vb/_static/image20.png)](role-based-authorization-vb/_static/image19.png)

**그림 7**: 합니다 `UserGrid` GridView 나열 정보에 대 한 각 사용자 시스템에서 ([클릭 하 여 큰 이미지 보기](role-based-authorization-vb/_static/image21.png))


> [!NOTE]
> `UserGrid` GridView 비페이징 인터페이스에서 사용자의 모든를 나열 합니다. 이 간단한 모눈 인터페이스 시나리오에 적합 하지 않은 몇 가지 이상의 사용자가 있는 경우. 한 가지 옵션 GridView 페이징을 사용 하도록 구성 하는 것입니다. `Membership.GetAllUsers` 메서드에 두 개의 오버 로드가: 하나 없습니다 입력된 매개 변수를 수락 하 고 모든 사용자 및 페이지 크기와 인덱스 페이지에 대 한 정수 값에서 지정 된 사용자의 하위 집합만 반환 하는 하나를 반환 합니다. 사용자가 페이지 보다 효율적으로 사용자 계정의 정확한 하위 집합만 반환 되므로 두 번째 오버 로드 데 사용할 수 있습니다 대신 *모든* 하 합니다. 수천 개의 사용자 계정에 있는 경우 예를 들어 사용자는 선택한 문자로 시작 하는 해당 사용자만 표시 하는 필터 기반 인터페이스를 고려 하는 것이 좋습니다. 합니다 [ `Membership.FindUsersByName` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) 필터 기반 사용자 인터페이스를 만드는 데 적합 한 합니다. 이후 자습서에서 이러한 인터페이스를 구축 살펴보겠습니다.


GridView 컨트롤은 기본 제공 편집 및 ObjectDataSource, SqlDataSource 등 올바르게 구성 된 데이터 소스 컨트롤에 컨트롤을 바인딩할 때 지원 삭제를 제공 합니다. 그러나 `UserGrid` GridView 프로그래밍 방식으로 바인딩하고 해당 데이터에 따라서 이러한 두 작업을 수행 하는 코드를 작성 해야 했습니다. GridView의 이벤트 처리기 만들기 해야 특히 `RowEditing`, `RowCancelingEdit`를 `RowUpdating`, 및 `RowDeleting` 방문자가 GridView의를 클릭할 때 발생 하는 이벤트에 업데이트를 취소, 편집 또는 삭제 단추입니다.

GridView의에 대 한 이벤트 처리기를 만들어 시작 `RowEditing`, `RowCancelingEdit`, 및 `RowUpdating` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample7.vb)]

`RowEditing` 하 고 `RowCancelingEdit` 이벤트 처리기 설정 하기만 하면 됩니다. GridView의 `EditIndex` 속성과 표에 계정 사용자 목록을 바인딩하고 합니다. 발생 하는 흥미로운 항목을 `RowUpdating` 이벤트 처리기입니다. 이 이벤트 처리기는 데이터는 유효 하 고 다음 가져와 함으로써 시작 합니다 `UserName` 값에서 편집할된 사용자 계정의 `DataKeys` 컬렉션입니다. `Email` 및 `Comment` 텍스트 상자에서 두 TemplateFields' `EditItemTemplate` s는 다음 프로그래밍 방식으로 참조 합니다. 해당 `Text` 속성 편집된 전자 메일 주소 및 설명을 포함 합니다.

처음 호출을 통해 수행 하는 사용자의 정보를 가져와야 하는 멤버 API를 통해 사용자에 대 한 계정을 업데이트 하기 위해 `Membership.GetUser(userName)`합니다. 반환 된 `MembershipUser` 개체의 `Email` 고 `Comment` 속성 편집 인터페이스에서 두 개의 텍스트 상자에 입력 된 값을 사용 하 여 업데이트 됩니다. 호출 하 여 수정이 내용을 저장 하는 마지막으로, [ `Membership.UpdateUser` ](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)합니다. `RowUpdating` 미리 편집 인터페이스에 GridView 되돌리기 하 여 이벤트 처리기를 완료 합니다.

다음으로 만듭니다는 `RowDeleting` RowDeleting 이벤트 처리기 다음 코드를 추가 합니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample8.vb)]

위의 이벤트 처리기를 통해 시작 합니다 `UserName` GridView의 값 `DataKeys` 컬렉션;이 `UserName` 값이 다음 구성원 클래스에 전달 [ `DeleteUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)합니다. `DeleteUser` 메서드 (역할 등이 사용자가 속한) 관련 된 멤버 자격 데이터를 포함 하 여 시스템에서 사용자 계정을 삭제 합니다. 사용자, 표를 삭제 한 후 `EditIndex` (하는 경우 사용자가 다른 행이 편집 모드에서 하는 동안 삭제를 클릭)-1로 설정 되어 및 `BindUserGrid` 메서드가 호출 됩니다.

> [!NOTE]
> 삭제 단추는 모든 종류의 사용자 계정을 삭제 하기 전에 사용자 로부터 확인 필요 하지 않습니다. 계정 실수로 삭제할 가능성을 줄이기 위해 사용자에 게 확인 형태의 추가 하시기 바랍니다. 작업을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자를 통해입니다. 이 기술에 대 한 자세한 내용은 참조 하세요. [삭제 하는 경우 클라이언트 쪽 확인 추가](https://asp.net/learn/data-access/tutorial-42-vb.aspx)합니다.


이 페이지 예상 대로 작동 하는지 확인 합니다. 사용자 계정을 삭제할 수 있을 뿐만 아니라 모든 사용자의 전자 메일 주소 및 설명을 편집할 수 있어야 합니다. 이후를 `RoleBasedAuthorization.aspx` 페이지는 모든 사용자에 게 액세스할 수 있는, 모든 –도 익명 방문자 –이 페이지를 방문 하 고 편집할 수 있으며 사용자 계정을 삭제할! 사용자의 전자 메일 주소 및 주석, 감독자 및 관리자 역할에 대 한 사용자만 편집할 수 있으며 관리자만 사용자 계정을 삭제할 수 있도록이 페이지를 업데이트 해 보겠습니다.

LoginView 컨트롤을 사용 하 여 사용자의 역할에 특정 지침을 표시 하려면 "LoginView 컨트롤 사용" 섹션을 찾습니다. 관리자 역할에 사용자가이 페이지를 방문 하는 경우 편집 하 고 사용자를 삭제 하는 방법에 지침을 살펴보겠습니다. 감독자 역할의 사용자가이 페이지에 도달 하면 사용자가 편집에 지시를 살펴보겠습니다. 및 방문자는 익명, 감독자 또는 관리자 역할에 없는 경우 편집 하거나 사용자 계정 정보를 삭제할 수 없습니다를 설명 하는 메시지 표시 됩니다. "프로그래밍 방식으로 제한 기능" 섹션에 프로그래밍 방식으로 표시 하거나 사용자의 역할에 따라 편집 및 삭제 단추를 숨기는 코드를 작성 합니다.

### <a name="using-the-loginview-control"></a>LoginView 컨트롤을 사용 하 여

이전 자습서에서 살펴본 대로 LoginView 컨트롤은 인증 및 익명 사용자에 대 한 다른 인터페이스를 표시 하는 데 유용 하지만 통해 LoginView 컨트롤은 사용자의 역할을 기반으로 하는 다른 태그를 표시 하려면 사용할 수도 있습니다. 방문한 사용자의 역할에 따라 다른 명령을 표시할 LoginView 컨트롤을 사용해 보겠습니다.

위의 LoginView를를 추가 하 여 시작 된 `UserGrid` GridView입니다. LoginView 컨트롤에 두 개의 기본 제공 템플릿을 이전에 설명한 대로: `AnonymousTemplate` 고 `LoggedInTemplate`입니다. 이러한 두 템플릿은 편집 하거나 사용자 정보를 삭제할 수 없는 사용자에 게 알려 주는 간단한 메시지를 입력 합니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample9.aspx)]

외에 합니다 `AnonymousTemplate` 및 `LoggedInTemplate`, LoginView 컨트롤 포함 될 수 있습니다 *RoleGroups*, 역할별 템플릿은입니다. 단일 속성을 포함 하는 각 RoleGroup `Roles`는 RoleGroup 적용할 역할을 지정 하는 합니다. `Roles` (예: "Administrators")를 단일 역할 또는 역할 (예: "Administrators, 감독자")의 쉼표로 구분 된 목록에 속성을 설정할 수 있습니다.

RoleGroups를 관리 하려면 RoleGroup 컬렉션 편집기를 표시 하려면 컨트롤의 스마트 태그에서 "RoleGroups 편집" 링크를 클릭 합니다. 두 개의 새 RoleGroups를 추가 합니다. 첫 번째 RoleGroup의 설정 `Roles` 속성을 "Administrators" 하 고 두 번째의 "감독자"입니다.


[![LoginView의 역할별 템플릿 RoleGroup 컬렉션 편집기를 통해 관리](role-based-authorization-vb/_static/image23.png)](role-based-authorization-vb/_static/image22.png)

**그림 8**: LoginView의 역할별 템플릿 the RoleGroup 컬렉션 편집기를 통해 관리할 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image24.png))


확인을 클릭 합니다 RoleGroup 컬렉션 편집기를 닫습니다 포함 하도록 LoginView의 선언적 태그를 업데이트 하는이 `<RoleGroups>` 섹션을 `<asp:RoleGroup>` 각 RoleGroup에 대 한 자식 요소 RoleGroup 컬렉션 편집기에서 정의 합니다. LoginView의 스마트 태그-처음에 나열 된 "보기" 드롭 다운 목록 또한 테이블만 `AnonymousTemplate` 및 `LoggedInTemplate` – 이제 추가 RoleGroups에도 포함 됩니다.

감독자 역할의 사용자는 관리자 역할의 사용자 편집 및 삭제에 대 한 지침을 표시 되어 사용자 계정을 편집 하는 방법에 대 한 표시 지침을 RoleGroups를 편집 합니다. 다음과 같이 변경한 후 LoginView의 선언적 태그 다음과 유사 합니다.

[!code-aspx[Main](role-based-authorization-vb/samples/sample10.aspx)]

다음과 같이 변경한 후 페이지를 저장 하 고 방문 하 여 브라우저를 통해. 먼저 익명 사용자로 페이지를 방문 합니다. 메시지를 표시 해야, "로그인 하지 않은 시스템에 있습니다. 따라서 편집 하거나 수 사용자 정보를 모두 삭제 합니다. " 그런 다음 인증된 된 사용자에 있지만 감독자 및 관리자 역할의 아닌 것으로 로그인 합니다. 이 시간 "없는 감독자 또는 관리자 역할의 멤버인 경우 메시지가 표시 됩니다. 따라서 편집 하거나 수 사용자 정보를 모두 삭제 합니다. "

다음으로, 감독자 역할의 구성원 인 사용자로 로그인 합니다. 역할별 감독자 표시이 이번 메시지 (그림 9 참조). 역할별 관리자를 표시 하는 역할 (그림 10 참조) 메시지 관리자에서 사용자로 로그인 하는 경우.


[![Bruce는 감독자 역할 관련 메시지가 표시 됩니다.](role-based-authorization-vb/_static/image26.png)](role-based-authorization-vb/_static/image25.png)

**그림 9**: Bruce 감독자 역할 관련 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image27.png))


[![Tito는 관리자 역할 관련 메시지가 표시 됩니다.](role-based-authorization-vb/_static/image29.png)](role-based-authorization-vb/_static/image28.png)

**그림 10**: Tito 관리자 역할 관련 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image30.png))


그림 9에 스크린 샷을와 10 표시 LoginView만 렌더링 하나의 템플릿 여러 템플릿을 적용 하는 경우에 합니다. Bruce 및 Tito 둘 다 로그인 사용자에 게 아직 LoginView 렌더링 된 일치 하는 RoleGroup만 아니라는 `LoggedInTemplate`합니다. 또한 관리자 및 감독자 역할에 속하는 Tito 아직 LoginView 컨트롤 렌더링 감독자 대신 관리자 역할 관련 템플릿을 하나.

그림 11에서는 렌더링 템플릿을 결정할 LoginView 컨트롤에서 사용 하는 워크플로 보여 줍니다. 가 둘 이상의 RoleGroup 지정 하는 경우 LoginView 템플릿을 렌더링 되는지 확인 합니다 *첫 번째* RoleGroup 일치 하는 합니다. 즉, 첫 번째 RoleGroup으로 감독자 RoleGroup와 두 번째 관리자를 배치 했기 것을 다음 Tito이이 페이지를 방문 하는 경우 그는 감독자 메시지가 표시 됩니다.


[![렌더링할 템플릿을 결정 하는 데 LoginView 컨트롤의 워크플로](role-based-authorization-vb/_static/image32.png)](role-based-authorization-vb/_static/image31.png)

**그림 11**: 확인 항목 템플릿을 사용 하 여 렌더링은 LoginView 컨트롤의 워크플로 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image33.png))


### <a name="programmatically-limiting-functionality"></a>프로그래밍 방식으로 기능 제한

LoginView 컨트롤 페이지를 방문 하는 사용자의 역할에 따라 다른 명령을 표시 하는 동안 편집 및 취소 단추를 계속 모두 표시 됩니다. 프로그래밍 방식으로 익명 방문자 및 감독자 아니고 관리자 역할에 사용자에 대 한 편집 및 삭제 단추를 숨기기 해야 합니다. 관리자가 아닌 사용자에 게 삭제 단추를 숨기려면 해야 합니다. 이 작업을 수행 하기 위해 약간의 프로그래밍 방식으로 CommandField의 편집 및 삭제 하는 Linkbutton 및 집합을 참조 하는 코드를 작성 자신의 `Visible` 속성을 `False`필요한 경우.

프로그래밍 방식으로 컨트롤을 CommandField에서를 참조 하는 가장 쉬운 방법은 먼저을 템플릿으로 변환 방법은입니다. 이를 위해 GridView의 스마트 태그에서 "열 편집" 링크를 클릭 합니다 CommandField 현재 필드 목록에서 선택한 "이이 필드를 TemplateField로 변환 하 는" 링크를 클릭 합니다. CommandField를 사용 하 여 templatefield로 바뀝니다이 `ItemTemplate` 고 `EditItemTemplate`입니다. 합니다 `ItemTemplate` 편집 및 삭제 Linkbutton 하는 동안 포함을 `EditItemTemplate` Linkbutton 취소 확인 하 고 업데이트를 포함 합니다.


[![CommandField templatefield로 변환](role-based-authorization-vb/_static/image35.png)](role-based-authorization-vb/_static/image34.png)

**그림 12**: TemplateField로는 CommandField 변환 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image36.png))


편집 및 삭제 Linkbutton에서 업데이트를 `ItemTemplate`설정, 해당 `ID` 속성의 값을 `EditButton` 및 `DeleteButton`, 각각.

[!code-aspx[Main](role-based-authorization-vb/samples/sample11.aspx)]

GridView의 레코드를 열거 데이터를 GridView에 바인딩되어 때마다 해당 `DataSource` 속성 해당 생성 `GridViewRow` 개체입니다. 각 `GridViewRow` 개체를 만든를 `RowCreated` 이벤트가 발생 합니다. 권한이 없는 사용자에 대 한 편집 및 삭제 단추를 숨기려면이 이벤트에 대 한 이벤트 처리기를 만들고 편집 및 삭제 Linkbutton, 설정에 프로그래밍 방식으로 참조 해야 해당 `Visible` 속성 적절 하 게 합니다.

이벤트 처리기를 만들고는 `RowCreated` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample12.vb)]

에 유의 합니다 `RowCreated` 에 대 한 이벤트가 발생 *모든* GridView 행 머리글, 바닥글, 호출기 인터페이스 등을 포함 하 여 합니다. 편집 모드에 있지 데이터 행 (편집 모드에 있는 행에는 편집 및 삭제 하는 대신 업데이트 및 취소 단추가) 되므로 처리 중인 경우 편집 및 삭제 하는 Linkbutton을 프로그래밍 방식으로 참조 하려고 합니다. 이 검사를 처리 합니다 `If` 문입니다.

편집 및 삭제 하는 Linkbutton 참조 처리 하 고 편집 모드에 있지 않은 데이터 행을 포함 하는 경우 및 해당 `Visible` 속성에서 반환 하는 부울 값에 따라 설정 됩니다는 `User` 개체의 `IsInRole(roleName)` 메서드. `User` 개체가 참조 하 여 만든 보안 주체를 `RoleManagerModule`; 따라서를 `IsInRole(roleName)` 메서드는 역할 API를 사용 하 여 현재 방문자에 속하는지 여부를 결정할 *roleName*합니다.

> [!NOTE]
> 사용 역할 클래스를 직접 호출을 바꾸는 `User.IsInRole(roleName)` 에 대 한 호출을 사용 하 여 합니다 [ `Roles.IsUserInRole(roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)합니다. 보안 주체 개체를 사용 하기로 `IsInRole(roleName)` 이 예제의 메서드 역할 API를 직접 사용 하 여 보다 효율적 이기 때문에 있습니다. 이 자습서의 앞부분에서 역할 관리자를 사용자의 역할이 쿠키에 캐시를 구성 했습니다. 이 캐시 된 쿠키 데이터를 때 사용 되는 것이 주체의 `IsInRole(roleName)` 역할 API를 직접 호출에는 항상 역할 저장소에 여정 관련; 메서드가 호출 됩니다. 역할 쿠키에 캐시 되지 않습니다 하는 경우에 보안 주체 개체의 호출 `IsInRole(roleName)` 요청 중 처음으로 결과 캐시에 대 한 호출 되는 경우 때문에 메서드는 일반적으로 더 효율적입니다. 역할 API를 다른 한편으로 수행 하지 않습니다 모든 캐싱. 때문에 합니다 `RowCreated` GridView의 모든 행에 대 한 이벤트를 한 번 발생를 사용 하 여 `User.IsInRole(roleName)` 반면 역할 저장소에 한 번만 포함 됩니다 `Roles.IsUserInRole(roleName)` 필요 *N* 왕복 여기서 *N* 는 표에 표시 된 사용자 계정의 수입니다.


편집 단추 `Visible` 속성이 `True` 이 페이지를 방문 하는 사용자가 관리자나 감독자 역할; 그렇지 않으면로 설정 됩니다 `False`합니다. Delete 단추의 `Visible` 속성이 `True` 관리자 역할에 사용자가 경우에 합니다.

브라우저를 통해이 페이지를 테스트 합니다. 또는 감독자 아니고 관리자 인 사용자는 익명 방문자로 페이지를 방문 하는 경우는 CommandField 비어 있습니다. 여전히 존재 하지만 편집 하거나 삭제 하지 않고 씬 은색으로 단추.

> [!NOTE]
> CommandField 숨길 수 있습니다 완전히 경우-감독자 및 비관리자는 페이지를 방문 합니다. 필자는 판독기에 대 한 연습으로 둡니다.


[![비-감독자 및 관리자가 아닌 숨겨져 편집 및 삭제 단추](role-based-authorization-vb/_static/image38.png)](role-based-authorization-vb/_static/image37.png)

**그림 13**: 비 감독자 및 관리자가 아닌 숨겨져은 편집 및 삭제 단추 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image39.png))


감독자 역할 (아니라 관리자 역할)에 속하는 사용자를 방문 하는 경우 그 편집 단추를 확인 합니다.


[![삭제 단추가 숨겨집니다 편집 단추 감독자에 대 한 사용 가능한 상태인](role-based-authorization-vb/_static/image41.png)](role-based-authorization-vb/_static/image40.png)

**그림 14**: 동안 편집 단추 감독자에 대 한 사용 가능 이면 삭제 단추가 숨겨집니다 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image42.png))


및 관리자를 방문 하는 경우에 편집 및 삭제 단추에 액세스 합니다.


[![편집 및 삭제 단추를 사용할 수만 관리자는](role-based-authorization-vb/_static/image44.png)](role-based-authorization-vb/_static/image43.png)

**그림 15**: The 편집 및 삭제 단추는 사용할 수만 관리자 ([큰 이미지를 보려면 클릭](role-based-authorization-vb/_static/image45.png))


## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>클래스 및 메서드를 역할 기반 권한 부여 규칙을 적용 하는 3 단계:

제한 2 단계에서에서 감독자 및 관리자 역할에 사용자에 게 기능을 편집 하 고만 기능 관리자를 삭제 합니다. 이 작업을 프로그래밍 방식으로 기술을 통해 권한이 없는 사용자가 연결 된 사용자 인터페이스 요소를 숨기면 수행 했습니다. 이러한 측정값은 권한이 없는 사용자 없게 됩니다 권한 있는 작업을 수행 하는 것을 보장 하지 않습니다. 나중에 추가 되는 사용자 인터페이스 요소 또는 하는 것을 잊었습니다 권한이 없는 사용자가 숨기려면 수 있습니다. 또는 해커가 원하는 메서드를 실행 하는 ASP.NET 페이지를 가져오는 다른 방법으로 검색할 수 있습니다.

권한이 없는 사용자가 기능의 특정 부분에 액세스할 수 없도록 하는 간편한 방법은 해당 클래스 또는 메서드를 데코 레이트 하는 것은 [ `PrincipalPermission` 특성](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)합니다. .NET 런타임 클래스를 사용 하 여, 해당 메서드 중 하나를 실행 하는 경우 현재 보안 컨텍스트의 권한을 갖도록 확인 합니다. `PrincipalPermission` 특성에서는 이러한 규칙을 정의할 수 있는 메커니즘을 제공 합니다.

사용 하 여 살펴보았습니다 합니다 `PrincipalPermission` 년대 특성을 <a id="_msoanchor_9"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서. GridView의 데코 레이트 하는 방법을 살펴보았습니다 특히 `SelectedIndexChanged` 고 `RowDeleting` 이벤트 처리기는 수만 실행할 수 있도록 인증 된 사용자로 Tito, 각각. `PrincipalPermission` 특성이 역할과 마찬가지로 작동 합니다.

사용 하 여 살펴보겠습니다 합니다 `PrincipalPermission` GridView의 특성 `RowUpdating` 및 `RowDeleting` 승인 되지 않은 사용자에 대 한 실행을 금지 하는 이벤트 처리기입니다. 각 함수 정의 위에 적절 한 특성을 추가 하기만 됩니다.

[!code-vb[Main](role-based-authorization-vb/samples/sample13.vb)]

에 대 한 특성을 `RowUpdating` 이벤트 처리기 관리자나 감독자 역할의 사용자만의 특성으로 작업 하는 경우 이벤트 처리기를 실행할 수 있는지 결정를 `RowDeleting` 사용자 관리자에 게 실행을 제한 하는 이벤트 처리기 역할입니다.


> [!NOTE]
> 합니다 `PrincipalPermission` 특성의 클래스로 표시 됩니다는 `System.Security.Permissions` 네임 스페이스입니다. 추가 해야는 `Imports System.Security.Permissions` 이 네임 스페이스를 가져오는 코드 숨김 클래스 파일의 맨 위에 있는 문.


라면 어떻게 해서든 관리자가 아닌 실행 하려고 합니다 `RowDeleting` 이벤트 처리기는 비-감독자 또는 관리자가 아닌 실행 하려는 경우 또는 `RowUpdating` 이벤트 처리기에서.NET 런타임 시킵니다를 `SecurityException`.


[![보안 컨텍스트는 메서드를 실행할 수 있는 권한이 없습니다, 경우 SecurityException이 Throw 됩니다.](role-based-authorization-vb/_static/image47.png)](role-based-authorization-vb/_static/image46.png)

**그림 16**: 보안 컨텍스트 메서드를 실행할 권한이 없는 경우는 `SecurityException` 이 Throw 됩니다 ([클릭 하 여 큰 이미지 보기](role-based-authorization-vb/_static/image48.png))


ASP.NET 페이지 외에도 많은 응용 프로그램은 수도 비즈니스 논리 및 데이터 액세스 계층 같은 다양 한 계층을 포함 하는 아키텍처에 연결 합니다. 이러한 계층은 일반적으로 클래스 라이브러리로 구현 및 비즈니스 논리 및 데이터 관련 기능을 수행 하기 위한 메서드와 클래스를 제공 합니다. `PrincipalPermission` 특성은 이러한 계층에도 권한 부여 규칙을 적용 하는 데 유용 합니다.

사용 하 여 대 한 자세한 내용은 합니다 `PrincipalPermission` 클래스 및 메서드에서 권한 부여 규칙을 정의 참조 특성 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [비즈니스 및 데이터 레이어 사용하여권한부여규칙추가`PrincipalPermissionAttributes` ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>요약

이 자습서에서는 대략적인 지정 하는 방법에 살펴보았습니다 및 사용자의 역할을 기반으로 하는 세부적으로 권한 부여 규칙. ASP 합니다. NET의 URL 권한 부여 기능에는 페이지 개발자를 어떤 id 허용 또는 거부 페이지에 대 한 액세스를 지정할 수 있습니다. 다시 살펴본 것 처럼 합니다 <a id="_msoanchor_10"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서, URL 권한 부여 사용자 간 기준 규칙을 적용할 수 있습니다. 이러한도 적용할 수 있습니다-역할에 따라이 자습서의 1 단계에서에서 보았듯이.

프로그래밍 방식으로 또는 선언적으로 세부적으로 권한 부여 규칙을 적용할 수 있습니다. 2 단계에서에서 방문한 사용자의 역할을 기반으로 하는 다른 출력을 렌더링 하 LoginView 컨트롤의 RoleGroups 기능을 사용 하 여 살펴보았습니다. 또한 살펴보았습니다 프로그래밍 방식으로 페이지의 기능을 적절 하 게 조정 하는 방법과 특정 역할에 사용자가 속할 경우를 확인 하는 방법.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [비즈니스 및 데이터 계층을 사용 하 여 권한 부여 규칙 추가 `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필: 역할 작업](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [ASP.NET 2.0에 대 한 보안 질문 목록](https://msdn.microsoft.com/library/ms998375.aspx)
- [에 대 한 기술 설명서는 `<roleManager>` 요소](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사 하는 중...

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Suchi Banerjee 및 Teresa Murphy 포함 됩니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](assigning-roles-to-users-vb.md)
