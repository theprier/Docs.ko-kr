---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: ASP.NET Id 소개 | Microsoft Docs
author: jongalloway
description: ASP.NET 멤버 자격 시스템 도입 된 ASP.NET 2.0 다시 이후 및 2005에서는 같은 방법으로 웹 응용 프로그램 일반적에 많은 변경 내용이 다음 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 59272f4659256e108ee99b22eb3bd3e2583a617c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874098"
---
<a name="introduction-to-aspnet-identity"></a>ASP.NET Id 소개
====================
여 [Jon Galloway](https://github.com/jongalloway), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

> ASP.NET 멤버 자격 시스템 도입 되었습니다 ASP.NET 2.0 백 이후 및 2005에서는 웹 응용 프로그램 인증 및 권한 부여를 일반적으로 처리 하는 방법에 많은 변경 내용이 다음. ASP.NET Id에는 멤버 자격 시스템 야 하는 웹, phone 또는 태블릿에 대 한 최신 응용 프로그램을 작성 하는 경우에 새롭게입니다.
> 
> 이 문서 Pranav Rastogi에 의해 작성 되었으므로 ([@rustd](https://twitter.com/rustd)), Jon Galloway ([@jongalloway](https://twitter.com/jongalloway)), Tom Dykstra 및 Rick Anderson ([ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ).


## <a name="background-membership-in-aspnet"></a>ASP.NET에서 배경: 멤버 자격

### <a name="aspnet-membership"></a>ASP.NET 멤버 자격

[ASP.NET 멤버 자격](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx) 일반적 2005 폼 인증 및 사용자 이름, 암호 및 프로 파일 데이터에 대 한 SQL Server 데이터베이스에서에서 사용 되 던 사이트 구성원 자격 요구 사항을 해결 하도록 설계 되었습니다. 현재는 웹 응용 프로그램에 대 한 데이터 저장소 옵션의 훨씬 더 광범위 한 배열 및 대부분의 개발자가 인증 및 권한 부여 기능에 대 한 소셜 id 공급자를 사용 하도록 해당 사이트를 사용 하도록 설정 하려면. ASP.NET 멤버 자격의 디자인 제한 어려운 이러한 전환을 수행 합니다.

- 데이터베이스 스키마는 SQL Server에 맞게 디자인 하 고 변경할 수 없습니다. 프로필 정보를 추가할 수는 있지만 어렵습니다 액세스 프로필 공급자 API를 통해 제외 하 고 어떤 방법으로 다른 테이블에 추가 데이터가 압축 됩니다.
- 공급자 시스템을 통해 백업 데이터 저장소를 변경할 수 있지만 시스템 관계형 데이터베이스에 대 한 적절 한 가정을 기반으로 설계 되었습니다. Azure 저장소 테이블 등의 비 관계형 저장소 메커니즘에 멤버 등록 정보를 저장 하는 공급자를 작성할 수 있지만 관계형 디자인 많은 코드와 많이 작성 하 여 해결 해야 `System.NotImplementedException` 하지 않는 메서드에 대 한 예외 NoSQL 데이터베이스에 적용 됩니다.
- 멤버 자격 시스템을 사용할 수 없습니다 로그-/ 로그 아웃 기능 폼 인증을 기반으로 하기 때문 [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)합니다. OWIN 미들웨어 구성 요소 (예: Microsoft 계정, Facebook, Google의, Twitter), 외부 id 공급자를 사용 하 여 로그 기능에 대 한 지원을 비롯 하 여 인증을 위해 포함 및 로그인에서 조직 계정을 사용 하 여 온-프레미스 Active Directory 또는 Azure Active Directory 합니다. OWIN에 OAuth 2.0, JWT 및 CORS에 대 한 지원이 포함 되어 있습니다.

### <a name="aspnet-simple-membership"></a>ASP.NET 단순 멤버 자격

[ASP.NET 단순 멤버 자격](../../../web-pages/overview/security/16-adding-security-and-membership.md) ASP.NET 웹 페이지에 대 한 멤버 자격 시스템으로 개발 되었습니다. WebMatrix 및 Visual Studio 2010 SP1와 함께 출시 된 것입니다. 단순 멤버 자격의 목표를 쉽게 웹 페이지 응용 프로그램에 멤버 자격 기능을 추가 했습니다.

단순 멤버 자격 않은 쉽게 사용자 프로필 정보를 사용자 지정할 수 있지만 여전히 ASP.NET 멤버 자격에 다른 문제가 공유 있으며에 몇 가지 제한이:

- 비 관계형 저장소에서 멤버 자격 시스템 데이터를 유지 하는 것이 어려웠습니다.
- OWIN과 사용할 수 없습니다.
- 기존 ASP.NET 멤버 자격 공급자와 잘 작동 하지 않는 하 고 확장할 수는 없습니다.

### <a name="aspnet-universal-providers"></a>ASP.NET 범용 공급자

[ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) 있으며 Azure SQL 데이터베이스, SQL Server Compact와 확대할 Microsoft에서 멤버 자격 정보를 유지할 수 있도록 하기 위해 개발 되었습니다. Universal Providers 된 Entity Framework Code First, EF에서 지 원하는 모든 저장소에 데이터를 유지 하는 범용 공급자를 사용할 수 있다는 의미를 기반으로 합니다. Universal Providers 데이터베이스 스키마는 매우 큰도 정리 되었습니다. 합니다.

Universal Providers는 ASP.NET 멤버 자격 인프라에서 빌드되므로 SqlMembership 공급자로 동일한 제한 사항이 계속 수행 합니다. 즉, 관계형 데이터베이스용 만들었던 하 고 프로필 및 사용자 정보를 사용자 지정 하는 것이 어렵습니다. 이러한 공급자는 여전히 로그인 및 로그 아웃 기능에 대 한 폼 인증을 사용 합니다.

## <a name="aspnet-identity"></a>ASP.NET ID

멤버 자격으로 ASP.NET의 스토리 ASP.NET 팀이 고객의 피드백에서을 너무 많이 알고 수 년에 걸쳐 발전 했습니다.

사용자는 사용자 이름 및 응용 프로그램에서 등록 한 암호를 입력 하 여에 로그인 하는 가정 하므로 더 이상 유효 합니다. 웹 더 소셜 되 고 있습니다. 사용자가 Facebook, Twitter 및 다른 소셜 웹 사이트와 같은 소셜 채널을 통해 실시간으로에서 서로 상호 작용 하는 합니다. 개발자는 사용자가 웹 사이트에서 풍부한 환경을 한 수를 포함 하도록 소셜 자신의 id를 사용 하 여 로그인 할 수 있도록 원합니다. 최신 멤버 자격 시스템 리디렉션 기반 로그인에 Facebook, Twitter, 등과 같은 인증 공급자를 사용 하도록 설정 해야 합니다.

웹 개발 발전 함에 따라으로 웹 개발 패턴 커졌습니다. 단위 상태가 된 응용 프로그램 개발자를 위한 중요 문제가 응용 프로그램 코드의 테스트 합니다. 2008 ASP.NET 단위 테스트 가능한 ASP.NET 응용 프로그램을 구축 하는 개발자가 있도록 부분적으로 모델-뷰-컨트롤러 (MVC) 패턴을 기반으로 하는 새로운 프레임 워크를 추가 합니다. 단위 하려는 개발자가 하는 멤버 자격 시스템으로 수행할 수 있어야 하 고 싶었습니다 응용 프로그램 논리를 테스트 합니다.

웹 응용 프로그램 개발에서 이러한 변경 내용은 고려 하면 다음과 같은 목표 ASP.NET Identity 위해 개발 되었습니다.

- **ASP.NET Id 시스템**

    - ASP.NET MVC, Web Forms, 웹 페이지, 웹 API SignalR 등 ASP.NET 프레임 워크의 모든 ASP.NET Id는 사용할 수 있습니다.
    - 웹, 전화, 저장소 또는 하이브리드 응용 프로그램을 작성 하는 경우에 ASP.NET Identity는 사용할 수 있습니다.
- **사용자에 대 한 프로필 데이터에 연결 편리한**

    - 스키마 사용자 및 프로필 정보를 제어할을 수 있습니다. 예를 들어 응용 프로그램에서 계정을 등록할 때 사용자가 입력 한 생년월일을 저장 하기 위한 시스템을 쉽게 사용할 수 있습니다.

- **지 속성 컨트롤**

    - 기본적으로 ASP.NET Identity 시스템 데이터베이스의 모든 사용자 정보를 저장합니다. ASP.NET Id를 사용 하 여 Entity Framework Code First를 모두 지 속성 메커니즘을 구현 합니다.
    - 데이터베이스 스키마, 테이블 이름 변경 또는 변경과 같은 일반적인 작업을 제어할는 데이터의 기본 키 형식이 간단 하 게 수행할입니다.
    - SharePoint, Azure 저장소 테이블 서비스, NoSQL 데이터베이스 등과 같은 다른 저장 메커니즘에 연결 하 여 throw 할 필요 없이 쉽게 `System.NotImplementedExceptions` 예외입니다.
- **단위 테스트 가능성**

    - ASP.NET Id 사용 하면 웹 응용 프로그램 자세한 단위 테스트할 수 있습니다. ASP.NET Id를 사용 하는 응용 프로그램의 부분에 대 한 단위 테스트를 작성할 수 있습니다.
- **역할 공급자**

    - 역할 공급자 역할에서 액세스 응용 프로그램의 일부를 제한할 수 있습니다. 쉽게 "Admin" 등의 역할 만들고 역할에 사용자를 추가할 수 있습니다.
- **클레임 기반**

    - ASP.NET Id 사용자의 id 클레임 집합이로 표시 되는 여기서 클레임 기반 인증을 지원 합니다. 클레임 될 사용자의 id를 설명 하는 역할을 사용 하는 보다 훨씬 더 많은 정보를 수 있습니다. (멤버 또는 비멤버) 부울 방금 역할 멤버 자격을 사용 하는 반면 클레임 사용자의 id 및 멤버 자격에 대 한 풍부한 정보를 포함할 수 있습니다.
- **소셜 로그인 공급자로 로그인**

    - 쉽게 응용 프로그램에 Microsoft 계정, Facebook, Twitter, Google, 등과 같은 소셜 로그인을 추가 하 고 응용 프로그램에서 사용자 관련 데이터를 저장할 수 있습니다.
- **Azure Active Directory**

    - Azure Active Directory를 사용 하 여 로그-기능을 추가 하 고 응용 프로그램에서 사용자 관련 데이터를 저장할 수도 있습니다. 자세한 내용은 참조 [조직 계정](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauth) 에서 Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기
- **OWIN 통합**

    - ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어 기반으로 합니다. System.Web에 ASP.NET Identity 종속성을 않아도 됩니다. 모두 호환 OWIN 프레임 워크 이며 모든 OWIN 호스팅 응용 프로그램에서 사용할 수 있습니다.
    - ASP.NET Identity OWIN 인증을 사용 하 여 로그 인/로그 아웃 웹 사이트의 사용자에 대 한 합니다. 이 쿠키를 생성 하려면 FormsAuthentication를 사용 하는 대신 응용 프로그램을 사용 하 여 OWIN CookieAuthentication 그렇게 것을 의미 합니다.
- **NuGet 패키지**

    - ASP.NET Id에 Visual Studio 2013과 함께 제공 되는 ASP.NET MVC, Web Forms 및 Web API 템플릿에 설치 된 NuGet 패키지로 재배포 됩니다. NuGet 갤러리에서이 NuGet 패키지를 다운로드할 수 있습니다.
    - Nuget ASP.NET Identity 해제 패키지 쉽게 새로운 기능과 버그 수정 프로그램을 반복 하 고 개발자에 게 이러한 민첩 한 방식으로 전달할 ASP.NET 팀에 있습니다.

## <a name="getting-started-with-aspnet-identity"></a>ASP.NET Identity 시작

ASP.NET Identity는 ASP.NET MVC, Web Forms, 웹 API 및 SPA에는 Visual Studio 2013 프로젝트 템플릿에 사용 됩니다. 이 연습에서는 프로젝트 템플릿이 등록, 로그인 기능을 추가 하려면 ASP.NET Identity를 사용 하는 방법을 보여 줍니다 알아보고 로그 아웃 한 사용자 하겠습니다.

ASP.NET Id는 다음 절차를 사용 하 여 구현 됩니다. 이 문서의 목적은 ASP.NET Identity;의 높은 수준의 개요를 제공 하는 것 해결 따르거나 세부 정보를 읽는 것입니다. ASP.NET Id, 사용자, 역할 및 프로필 정보를 추가 하는 새로운 API를 사용 하는 등을 사용 하 여 앱을 만드는 방법에 대 한 자세한 지침은이 문서의 끝에 다음 단계 섹션을 참조 합니다.

1. 개별 계정으로 ASP.NET MVC 응용 프로그램을 만듭니다. ASP.NET MVC, Web Forms, Web API SignalR 등에서 ASP.NET Identity를 사용할 수 있습니다. 이 문서에서 우리는 ASP.NET MVC 응용 프로그램으로 시작 됩니다.  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. 만든된 프로젝트는 ASP.NET Identity에 대 한 다음과 같은 세 가지 패키지를 포함합니다.

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   이 패키지에는 ASP.NET Identity 데이터 및 SQL Server에 대 한 스키마를 유지 하는 ASP.NET Identity의 Entity Framework 구현이 있습니다.
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   이 패키지에는 ASP.NET Identity에 대 한 핵심 인터페이스에 있습니다. 이 패키지 저장 하는 다른 지 속성을 대상으로 NoSQL Azure 테이블 저장소와 같은 데이터베이스 등 ASP.NET Identity에 대 한 구현을 쓰는 데 사용할 수 있습니다.
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   이 패키지에는 ASP.NET 응용 프로그램에서 ASP.NET Id를 가진 OWIN 인증에 연결 하는 데 사용 되는 기능이 들어 있습니다. 이 기능에서 응용 프로그램 및 쿠키를 생성 하는 OWIN 쿠키 인증 미들웨어로 호출에 로그를 추가할 때 사용 됩니다.
3. 사용자를 생성 합니다.  
   응용 프로그램을 시작 하 고을 클릭는 **등록** 사용자를 만들려면 링크 합니다. 다음 이미지는 사용자 이름 및 암호를 수집 하는 등록 페이지를 보여 줍니다.  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   사용자가 클릭할 때는 **등록** 단추를는 `Register` 계정 컨트롤러의 작업 아래 강조 표시 된 대로 ASP.NET Identity API를 호출 하 여 사용자를 만듭니다.

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. 로그인  
   사용자가 만들어졌음을 그녀는에 기록 하 여는 `SignInAsync` 메서드.  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample2.cs?highlight=12)]

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample3.cs?highlight=5-6)]

   위의 강조 표시 된 코드는 `SignInAsync` 메서드를 생성 한 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)합니다. ASP.NET Id 및 OWIN 쿠키 인증 클레임 기반 시스템 이므로 응용 프로그램에서 사용자에 대 한 ClaimsIdentity를 생성 하면 프레임 워크에 필요 합니다. ClaimsIdentity에 사용자가 속한 역할 같은 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다. 또한이 단계에서 사용자에 대 한 더 많은 클레임을 추가할 수 있습니다.  
  
   아래에 강조 표시 된 코드는 `SignInAsync` 메서드 호출 및 OWIN AuthenticationManager를 사용 하 여 사용자 로그인 `SignIn` 는 ClaimsIdentity를 전달 합니다.  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample4.cs?highlight=8-11)]
5. 로그 오프 합니다.  
   클릭 하 고 **로그 오프** 링크 계정 컨트롤러에서 로그 오프 동작을 호출 합니다. 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   강조 표시 된 코드 위의 OWIN `AuthenticationManager.SignOut` 메서드. 이 방법은 유사 [FormsAuthentication.SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) 사용 하는 방법의 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) Web Forms에는 모듈입니다.

## <a name="components-of-aspnet-identity"></a>ASP.NET Id의 구성 요소

아래 다이어그램에서는 ASP.NET Identity 시스템의 구성 요소를 보여 줍니다 (클릭 [이](introduction-to-aspnet-identity/_static/image3.png) 확대 하려면 다이어그램 또는). 녹색의 패키지는 ASP.NET Identity 시스템을 확인합니다. 다른 모든 패키지는 ASP.NET 응용 프로그램의 ASP.NET Id 시스템을 사용 하는 데 필요한 종속성입니다.

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

다음은 이전에 언급 되지 않은 NuGet 패키지에 대 한 간단한 설명입니다.

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 쿠키를 사용 하 여 응용 프로그램 미들웨어 기반 인증, ASP 비슷합니다. NET의 폼 인증입니다.
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Entity Framework는 관계형 데이터베이스에 대 한 Microsoft의 권장 되는 데이터 액세스 기술입니다.

## <a name="migrating-from-membership-to-aspnet-identity"></a>멤버 자격에서 ASP.NET Identity로 마이그레이션

곧 새 ASP.NET Identity 시스템 ASP.NET 멤버 자격 또는 단순 멤버 자격을 사용 하는 기존 앱 마이그레이션하는 방법에 지침을 제공 하기 위해 노력 합니다.

## <a name="next-steps"></a>다음 단계

- [Facebook, Google OAuth2 및 OpenID 로그온 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 이 자습서는 ASP.NET Identity API를 사용 하 여 사용자 데이터베이스에 프로필 정보 및 Google 및 Facebook 인증 하는 방법을 추가 합니다.
- [ASP.NET MVC 응용 프로그램 인증 및 SQL DB 만들기 및 Azure 앱 서비스 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 이 자습서에는 사용자 및 역할을 추가할 Id API를 사용 하는 방법을 보여 줍니다.
- [개별 사용자 계정](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#indauth) Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기에서
- [조직 계정](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauth) Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기에서
- [VS 2013 서식 파일에서 ASP.NET Identity에 프로필 정보를 사용자 지정](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)
- [VS 2013 프로젝트 템플릿에 사용 되는 소셜 공급자에서 자세한 정보 얻기](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 역할 및 사용자 관리를 수행 하는 방법 및 기본 역할 및 사용자 지원을 추가 하는 방법을 보여 주는 샘플 응용 프로그램입니다.
