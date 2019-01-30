---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: ASP.NET Id 소개 | Microsoft Docs
author: jongalloway
description: ASP.NET 멤버 자격 시스템 도입 된 ASP.NET 2.0 백을 사용 하 여 이후 2005 년에 같은 방법으로 웹 응용 프로그램 정도가에 많은 변경 내용이 다음...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4a545e52d2d9ea04a10c37c116fd326c60de9f8f
ms.sourcegitcommit: c47d7c131eebbcd8811e31edda210d64cf4b9d6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55236447"
---
<a name="introduction-to-aspnet-identity"></a>ASP.NET Id 소개
====================

> ASP.NET 멤버 자격 시스템에 도입 되었습니다 ASP.NET 2.0 백 이후 2005 년에 웹 응용 프로그램 인증 및 권한 부여를 일반적으로 처리 하는 방법에 많은 변경 내용이 다음. ASP.NET Id가 보안 정책 살펴보기 멤버 자격 시스템 웹, 휴대폰 또는 태블릿 용 최신 응용 프로그램을 작성 하는 경우 여야 합니다.


## <a name="background-membership-in-aspnet"></a>배경: Asp.net에서 멤버 자격

### <a name="aspnet-membership"></a>ASP.NET 멤버 자격

[ASP.NET 멤버 자격](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx) 폼 인증 및 사용자 이름, 암호 및 프로필 데이터에 대 한 SQL Server 데이터베이스를 포함 하는 2005 년 공통 된 사이트 구성원 자격 요구 사항을 해결 하도록 설계 되었습니다. 현재는 웹 응용 프로그램에 대 한 데이터 저장소 옵션의 훨씬 더 광범위 한 배열 및 대부분의 개발자가 인증 및 권한 부여 기능에 대 한 소셜 id 공급자를 사용 하도록 해당 사이트를 사용 하도록 설정 하려면. ASP.NET 멤버 자격의 디자인 제한 사항 어렵게이 전환:

- 데이터베이스 스키마가 SQL Server에 맞게 디자인 하 고 변경할 수 없습니다. 프로필 정보를 추가할 수 있지만 어렵습니다 액세스 프로필 공급자 API를 통해를 제외한 모든 방법으로 다른 테이블에 추가 데이터를 압축 됩니다.
- 공급자 시스템을 사용 하면 백업 데이터 저장소를 변경할 수 있습니다 하지만 시스템 관계형 데이터베이스에 대 한 적절 한 가정을 중심으로 디자인 되었습니다. Azure Storage Tables와 같은 비관계형 저장소 메커니즘을에 멤버 자격 정보를 저장 하려면 공급자를 작성할 수 있지만 관계형 디자인의 많으며 많은 코드를 작성 하 여 해결 해야 `System.NotImplementedException` 하지 않는 메서드에 대 한 예외 NoSQL 데이터베이스에 적용 됩니다.
- 폼 인증에 따라 로그-/ 로그 아웃 기능이 있으므로 멤버 자격 시스템을 사용할 수 없습니다 [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)합니다. OWIN 인증의 경우 외부 id 공급자 (예: Microsoft 계정, Facebook, Google의, Twitter)를 사용 하 여 로그인에 대 한 지원을 비롯 하 여 미들웨어 구성 요소를 포함 하 고 로그인에서 조직 계정을 사용 하 여 온-프레미스 Active Directory 또는 Azure Active Directory입니다. OWIN은 OAuth 2.0, JWT 및 CORS에 대 한 지원이 포함 됩니다.

### <a name="aspnet-simple-membership"></a>ASP.NET 단순 멤버 자격

[ASP.NET 단순 멤버 자격](../../../web-pages/overview/security/16-adding-security-and-membership.md) ASP.NET 웹 페이지에 대 한 멤버 자격 시스템으로 개발 되었습니다. WebMatrix 및 Visual Studio 2010 SP1을 사용 하 여 릴리스 되었습니다. 단순 멤버 자격의 목적은 웹 페이지 응용 프로그램 멤버 자격 기능을 추가할 수 있도록 하는 것 이었습니다.

단순 멤버 자격 않았습니다 쉽게 사용자 프로필 정보를 사용자 지정할 수 있지만 ASP.NET 멤버 자격을 사용 하 여 다른 문제가 여전히 공유 있으며 몇 가지 제한 사항이:

- 비관계형 저장소에서 멤버 자격 시스템 데이터를 유지 하는 것이 어려웠습니다.
- OWIN을 사용 하 여 사용할 수 없습니다.
- 기존 ASP.NET 멤버 자격 공급자에서 잘 작동 하지 않으면 및은 확장할 수 없습니다.

### <a name="aspnet-universal-providers"></a>ASP.NET 범용 공급자

[ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) 있으며 Azure SQL Database 에서도 SQL Server Compact를 사용 하 여 작동 microsoft에서 멤버 자격 정보를 유지할 수 있도록 하기 위해 개발 되었습니다. Universal Providers 된 Entity Framework Code First, Universal Providers EF에서 지원 되는 모든 저장소에서 데이터를 유지 하기 위해 사용할 수 있다는 의미를 기반으로 합니다. 범용 공급자를 사용 하 여 데이터베이스 스키마가 상당한도 정리 합니다.

Universal Providers SqlMembership 공급자과 동일한 제한 사항이 여전히 수행 하므로 ASP.NET 멤버 자격 인프라에 빌드됩니다. 즉, 관계형 데이터베이스에 대 한 설계 하 고 프로필 및 사용자 정보를 사용자 지정 하기가 어렵습니다. 이러한 공급자도 여전히 로그인 및 로그 아웃 기능에 대 한 폼 인증을 사용 합니다.

## <a name="aspnet-identity"></a>ASP.NET ID

멤버 자격으로 스토리 ASP.NET에서 ASP.NET 팀에서 고객의 의견을 많이 얻었습니다 년에 걸쳐 발전 했습니다.

가정 사용자 이름 및 응용 프로그램에서 등록 한 암호를 입력 하 여 사용자가 로그인 하는 더 이상 유효 합니다. 웹에 더 많은 소셜 되었습니다. 사용자가 Facebook, Twitter 및 기타 소셜 웹 사이트와 같은 소셜 채널을 통해 실시간으로에서 서로 상호 작용 합니다. 개발자는 해당 소셜 id를 갖도록 수 풍부한 경험을 해당 웹 사이트에 로그인 할 수 있는 사용자를 원합니다. 최신 멤버 자격 시스템 리디렉션 기반 로그인에서 인증 공급자로 Facebook, Twitter 등을 사용 해야 합니다.

웹 개발이 발전 하는 대로 웹 개발의 패턴 커졌습니다. 단위는 중요 한 문제가 응용 프로그램 개발자가 응용 프로그램 코드의 테스트 합니다. 2008 ASP.NET 일부 개발자가 단위 테스트 가능한 ASP.NET 응용 프로그램을 빌드할 수 있도록 모델-뷰-컨트롤러 (MVC) 패턴을 기반으로 하는 새로운 프레임 워크를 추가 합니다. 단위 하려는 개발자는 또한 멤버 자격 시스템을 사용 하 여 그렇게 할 수 하고자 하는 응용 프로그램 논리를 테스트 합니다.

웹 응용 프로그램 개발에 이러한 변경 내용을 고려 ASP.NET Id는 다음과 같은 목표를 사용 하 여 개발 되었습니다.

- **ASP.NET Id 시스템**

    - 모든 ASP.NET MVC, Web Forms, 웹 페이지, 웹 API 및 SignalR 같은 ASP.NET 프레임 워크를 사용 하 여 ASP.NET Id는 사용할 수 있습니다.
    - 웹, phone, 스토어 또는 하이브리드 응용 프로그램을 작성 하는 경우 ASP.NET Id는 사용할 수 있습니다.
- **사용자에 대 한 프로필 데이터에 연결 하는 편의성**

    - 프로필 정보와 사용자의 스키마를 통해 제어할 수 있습니다. 예를 들어, 응용 프로그램에서 계정을 등록할 때 사용자가 입력 한 생년월일 저장 시스템을 쉽게 사용할 수 있습니다.

- **지 속성 컨트롤**

    - 기본적으로 ASP.NET Id 시스템 데이터베이스의 모든 사용자 정보를 저장합니다. ASP.NET Id를 사용 하 여 Entity Framework Code First는 지 속성 메커니즘의 모든 구현 합니다.
    - 데이터베이스 스키마, 테이블 이름 변경 또는 변경 등의 일반적인 작업을 제어 데이터 형식의 기본 키 이므로 간단 하 게 수행할.
    - Throw 할 필요 없이 SharePoint, Azure Storage Table Service, NoSQL 데이터베이스 등과 같은 다른 저장소 메커니즘에 연결할 쉽습니다 `System.NotImplementedExceptions` 예외입니다.
- **단위 테스트 용이성**

    - ASP.NET Id를 사용 하므로 웹 응용 프로그램 더 많은 단위 테스트할 수 있습니다. ASP.NET Id를 사용 하는 응용 프로그램의 부분에 대 한 단위 테스트를 작성할 수 있습니다.
- **역할 공급자**

    - 역할에 의해 응용 프로그램의 일부에 대 한 액세스를 제한할 수 있습니다 하는 역할 공급자가 있습니다. "Admin"와 같은 역할을 만들고 역할에 사용자 추가 쉽게 있습니다.
- **클레임 기반**

    - ASP.NET Id 사용자의 id 클레임 집합으로 표시 됩니다는 클레임 기반 인증을 지원 합니다. 클레임 개발자의 역할을 사용 하는 보다 사용자의 id를 설명 하는 훨씬 더 적합할 수 있습니다. 역할 멤버 자격만을 부울 (멤버 또는 비멤버) 인 반면 클레임을 사용자의 id 및 멤버 자격에 대 한 풍부한 정보를 포함할 수 있습니다.
- **소셜 로그인 공급자**

    - 쉽게 응용 프로그램에 Microsoft 계정, Facebook, Twitter, Google 및 기타와 같은 소셜 로그인을 추가 하 고 응용 프로그램에서 사용자 고유의 데이터를 저장할 수 있습니다.

- **OWIN 통합**

    - ASP.NET 인증은 이제 OWIN 미들웨어는 OWIN 기반 호스트에 사용할 수 있는 기반으로 합니다. System.Web에 대 한 종속성을 없습니다 ASP.NET Id. 완전 한 준수 상태가 OWIN 프레임 워크 이며 호스팅되는 OWIN 응용 프로그램에서 사용할 수 있습니다.
    - ASP.NET Id 로그-/ 로그 아웃 웹 사이트의 사용자에 대 한 OWIN 인증을 사용합니다. 이 FormsAuthentication 쿠키를 생성 하려면를 사용 하는 대신 응용 프로그램을 사용 하 여 OWIN CookieAuthentication 수행 하는 것을 의미 합니다.
- **NuGet 패키지**

    - ASP.NET Id는 Visual Studio 2017을 사용 하 여 제공 되는 ASP.NET MVC, Web Forms 및 Web API 템플릿에서 설치 된 NuGet 패키지로 배분 됩니다. NuGet 갤러리에서이 NuGet 패키지를 다운로드할 수 있습니다.
    - NuGet으로 ASP.NET Id 해제 패키지 쉽게 ASP.NET 팀이 새 기능 및 버그 수정에 반복 하 고 민첩 한 방식으로 이러한 개발자에 게 제공 합니다.

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Id 시작

ASP.NET Id는 ASP.NET MVC, Web Forms, Web API 및 SPA에 대 한 Visual Studio 2017 프로젝트 템플릿에서 사용 됩니다. 이 연습에서는 프로젝트 템플릿 등록, 로그인 및 사용자 로그 아웃 기능을 추가 하려면 ASP.NET Id를 사용 하는 방법을 보여 줍니다 됩니다 것입니다.

ASP.NET Id는 다음 절차를 사용 하 여 구현 됩니다. 이 문서의 목적은 ASP.NET Id;의 높은 수준의 개요를 제공 하는 것 단계별로 따르거나 세부 정보를 읽었습니다. 사용자, 역할 및 프로필 정보를 추가 하려면 새 API를 사용 하는 등 ASP.NET Id를 사용 하 여 앱을 만드는 방법에 대 한 자세한 내용은이 문서의 끝에 있는 다음 단계 섹션을 참조 하세요.

1. 개별 계정을 사용 하 여 ASP.NET MVC 응용 프로그램을 만듭니다. ASP.NET MVC, Web Forms, Web API, SignalR 등 ASP.NET Id를 사용할 수 있습니다. 이 문서의 ASP.NET MVC 응용 프로그램을 사용 하 여 시작 하겠습니다.  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. 만든된 프로젝트를 ASP.NET Id에 대 한 다음 세 가지 패키지를 포함합니다.

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   이 패키지에는 ASP.NET Id 데이터 및 SQL Server에 대 한 스키마를 유지 하는 ASP.NET Identity의 Entity Framework 구현이 있습니다.
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   이 패키지에는 ASP.NET Id에 대 한 핵심 인터페이스에 있습니다. 이 패키지는 대상 다른 지 속성와 같은 저장소 Azure Table Storage, NoSQL 데이터베이스 등 ASP.NET Id에 대 한 구현을 쓰는 데 사용할 수 있습니다.
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   이 패키지에는 ASP.NET 응용 프로그램에서 ASP.NET Id를 사용 하 여 OWIN 인증에 연결 하는 데 사용 되는 기능이 들어 있습니다. 이 응용 프로그램 및 쿠키를 생성 하려면 OWIN 쿠키 인증 미들웨어를 호출 하 기능에서 로그인을 추가할 때 사용 됩니다.
3. 사용자를 만드는 중입니다.  
   응용 프로그램을 시작 하 고 클릭 합니다 **등록** 링크는 사용자를 만듭니다. 다음 이미지는 사용자 이름 및 암호를 수집 하는 등록 페이지를 보여 줍니다.  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   사용자가 선택 하는 경우는 **등록** 단추를는 `Register` Account 컨트롤러의 작업은 아래 강조 표시 된 대로 ASP.NET Identity API를 호출 하 여 사용자를 만듭니다.

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. 서명하세요.  
   사용자 성공적으로 만들어진 경우 그녀는 로그인 하 여는 `SignInAsync` 메서드.  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]


   합니다 `SignInManager.SignInAsync` 메서드를 생성 한 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)합니다. ASP.NET Id 및 OWIN 쿠키 인증 클레임 기반 시스템 이므로, 사용자에 대 한 ClaimsIdentity를 생성할 앱 프레임 워크에 필요 합니다. ClaimsIdentity에 사용자가 속한 역할 등 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다.   
 
5. 로그 오프 합니다.  
   선택 된 **로그 오프** account 컨트롤러의 로그 오프 작업을 호출 하는 링크입니다. 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   강조 표시 된 코드 위의 OWIN `AuthenticationManager.SignOut` 메서드. 이 비슷합니다 [FormsAuthentication.SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) 에서 사용 하는 메서드는 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) Web Forms에서 모듈입니다.

## <a name="components-of-aspnet-identity"></a>ASP.NET Id의 구성 요소

아래 다이어그램에서는 ASP.NET Id 시스템의 구성 요소를 보여 줍니다 (선택 [이](introduction-to-aspnet-identity/_static/image3.png) 또는 다이어그램을 확대) 합니다. 녹색에서 패키지를 ASP.NET Id 시스템을 구성 합니다. 다른 모든 패키지는 ASP.NET 응용 프로그램의 ASP.NET Id 시스템을 사용 하는 데 필요한 종속성입니다.

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

다음은 이전에 언급 되지 않은 NuGet 패키지의 간략 한 설명입니다.

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 응용 프로그램이 쿠키를 사용할 수 있게 해 주는 미들웨어 기반 인증, ASP와 비슷합니다. NET의 폼 인증입니다.
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Entity Framework는 관계형 데이터베이스에 대 한 Microsoft의 권장 되는 데이터 액세스 기술입니다.

## <a name="migrating-from-membership-to-aspnet-identity"></a>멤버 자격에서 ASP.NET Id로 마이그레이션

곧 새 ASP.NET Id 시스템에 ASP.NET 멤버 자격 또는 단순 멤버 자격을 사용 하는 기존 앱 마이그레이션하는 방법에 지침을 제공 하기를 바랍니다.

## <a name="next-steps"></a>다음 단계

- [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 자습서는 ASP.NET Id API를 사용 하 여 Google 및 Facebook을 사용 하 여 인증 하는 방법과 사용자 데이터베이스에 대 한 프로필 정보를 추가 합니다.
- [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 이 자습서에는 사용자 및 역할에 추가할 Id API를 사용 하는 방법을 보여 줍니다.
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 기본 역할 및 사용자 지원 추가 하는 방법 및 역할 및 사용자 관리를 수행 하는 방법을 보여 주는 샘플 응용 프로그램입니다.
