---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: ASP.NET Id는 비어 있는 또는 기존 웹 폼 프로젝트 추가 | Microsoft Docs
author: raquelsa
description: 이 자습서에서는 ASP.NET 응용 프로그램에 ASP.NET Id (ASP.NET에 대 한 새 멤버 자격 시스템)를 추가 하는 방법을 보여 줍니다. 만들 때 새 Web Forms 또는 MVC...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: cd28cc68db96b52eb205b8764aa2af014ffad9c3
ms.sourcegitcommit: c47d7c131eebbcd8811e31edda210d64cf4b9d6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55236512"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>추가 ASP.NET Id는 비어 있는 또는 기존 웹 폼 프로젝트


> 이 자습서에서는 추가 하는 방법을 보여 줍니다 [ASP.NET Id](introduction-to-aspnet-identity.md) (ASP.NET에 대 한 새 멤버 자격 시스템) ASP.NET 응용 프로그램에 있습니다.
> 
> 개별 계정을 사용 하 여 Visual Studio 2017 RTM의 새 Web Forms 또는 MVC 프로젝트를 만들 때 Visual Studio를 모든 필요한 패키지를 설치 하면에 대 한 모든 필요한 클래스를 추가 합니다. 이 자습서에서는 기존 Web Forms 프로젝트 또는 새로운 빈 프로젝트를 ASP.NET Id 지원을 추가 하는 단계를 설명 합니다. 살펴보도록는 및에 추가 해야 하는 클래스를 모든 NuGet 패키지를 설치 해야 합니다. 새 사용자를 등록 하 고 사용자 관리 및 인증에 대 한 모든 주요 항목 지점 Api를 강조 표시 하는 동안 로그인에 대 한 샘플 Web Forms를 통해으로. 이 샘플은 Entity Framework을 기반으로 하는 SQL 데이터 저장소에 대 한 ASP.NET Id 기본 구현을 사용 합니다. 이 자습서에서는 LocalDB는 SQL database에 대 한 사용 합니다.
> 

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Id 시작

1. 설치 및 실행 하 여 시작 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)합니다.
2. 선택 **새 프로젝트** 시작 페이지 또는 사용자 메뉴를 사용 하 여 선택할 **파일**를 차례로 **새 프로젝트**합니다.
3. 왼쪽된 창에서 확장 **시각적 C#** 을 선택한 후 **웹**, 다음 **ASP.NET 웹 응용 프로그램 (.NET Framework)**. "WebFormsIdentity" 프로젝트 이름을 지정 하 고 선택 **확인**합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. 에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   알림 합니다 **인증 변경** 단추가 비활성화 되 고이 템플릿에 없는 인증 지원이 제공 됩니다. Web Forms, MVC 및 Web API 템플릿을 통해 인증 방법을 선택할 수 있습니다.

## <a name="add-identity-packages-to-your-app"></a>앱에 Identity 패키지 추가

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 검색 하 고 설치 합니다 **Microsoft.AspNet.Identity.EntityFramework** 패키지 있습니다. 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
이 패키지 종속성 패키지 설치는 참고 합니다. **EntityFramework** 하 고 **Microsoft ASP.NET Identity Core**합니다.

## <a name="add-a-web-form-to-register-users"></a>사용자를 등록 하는 web form 추가

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가**를 차례로 **Web Form**합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. 에 **항목에 대 한 이름 지정** 대화 상자에서 이름 새 web form **등록**를 선택한 후 **확인**
3. 생성 된 태그 바꿉니다 *Register.aspx* 아래 코드를 사용 하 여 파일입니다. 코드 변경 내용은 강조 표시되어 있습니다. 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > 이의 단순화 된 버전에만 합니다 *Register.aspx* 새 ASP.NET Web Forms 프로젝트를 만들 때 생성 되는 파일. 위의 태그는 양식 필드 및 새 사용자를 등록 하는 단추를 추가 합니다.
4. 엽니다는 *Register.aspx.cs* 파일 및 파일의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. 위의 코드는의 단순화 된 버전의 *Register.aspx.cs* 새 ASP.NET Web Forms 프로젝트를 만들 때 생성 되는 파일입니다.
    > 2. 합니다 *IdentityUser* 클래스는 기본 EntityFramework 구현의 합니다 *IUser* 인터페이스입니다. *IUser* 인터페이스는 Asp.net Identity의 사용자에 대 한 최소 인터페이스입니다.
    > 3. 합니다 *UserStore* 클래스는 사용자 저장소의 기본 EntityFramework 구현 합니다. 이 클래스는 ASP.NET Identity 코어의 최소 인터페이스를 구현합니다. *IUserStore*, *IUserLoginStore*합니다 *IUserClaimStore* 하 고 *IUserRoleStore*합니다.
    > 4. *UserManager* 클래스는 사용자는 관련 Api를 자동으로 변경 내용을 저장 합니다 *UserStore*합니다.
    > 5. 합니다 *IdentityResult* 클래스 id 작업의 결과 나타냅니다.
5. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가**하십시오 **ASP.NET 폴더 추가** 차례로 **앱\_데이터**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. 엽니다는 *Web.config* 파일 및 사용자 정보를 저장 하는 데 사용 하는 데이터베이스에 대 한 연결 문자열 항목을 추가 합니다. 데이터베이스에 만들어집니다 런타임 EntityFramework에서 Identity 엔터티에 대 한 합니다. 연결 문자열 하나를 새 Web Forms 프로젝트를 만들 때 생성 하는 것과 비슷합니다. 강조 표시 된 코드를 추가 해야 태그를 보여 줍니다.

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > Visual Studio 2015 이상에서 대체 `(localdb)\v11.0` 사용 하 여 `(localdb)\MSSQLLocalDB` 연결 문자열에 있습니다.
    
7. 파일을 마우스 오른쪽 단추로 클릭 *Register.aspx* 선택한 서버 프로젝트 **시작 페이지로 설정**합니다. 빌드 및 웹 응용 프로그램을 실행 하려면 Ctrl + F5 키를 누릅니다. 새 사용자 이름 및 암호를 입력 한 다음 선택 **등록**합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Id에 유효성 검사를 지원 하 고이 샘플에서 사용자 이름 및 암호에 대 한 기본 동작을 확인할 수 있습니다 Identity 코어 패키지에서 제공 되는 유효성 검사기입니다. 사용자에 대 한 기본 유효성 검사기 (`UserValidator`) 속성이 `AllowOnlyAlphanumericUserNames` 로 설정 하는 기본 값이 `true`합니다. 암호에 대 한 기본 유효성 검사기 (`MinimumLengthValidator`) 하면 해당 암호는 6 자 이상입니다. 이러한 유효성 검사기 속성에 `UserManager` 사용자 지정 유효성 검사 하려는 경우 재정의할 수 있습니다

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>Entity Framework에서 생성 된 테이블과 LocalDb Id 데이터베이스를 확인 합니다.

1. 에 **뷰** 메뉴에서 **서버 탐색기**합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. 확장 **DefaultConnection (WebFormsIdentity)** 를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭 **AspNetUsers** 선택한 후 **테이블 데이터 표시**합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>OWIN 인증에 대 한 응용 프로그램 구성

이 시점에서 사용자를 만들기 위한 지원을 추가 했습니다. 이제 하겠습니다 인증 사용자 로그인을 추가할 수 있습니다 하는 방법을 보여 줍니다. ASP.NET Id는 폼 인증을 위해 Microsoft OWIN 인증 미들웨어를 사용합니다. OWIN 쿠키 인증 쿠키 및 클레임 기반된 인증 메커니즘에서 호스팅되는 모든 프레임 워크에서 사용할 수 있는 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) 또는 IIS입니다. 이 모델에서는 동일한 인증 패키지를 ASP.NET MVC 및 Web Forms를 비롯 한 여러 프레임 워크에서 사용할 수 있습니다. 프로젝트 Katana 및 호스트 알 수 없는 참조에 미들웨어를 실행 하는 방법에 대 한 자세한 내용은 [Katana 프로젝트 시작](https://msdn.microsoft.com/magazine/dn451439.aspx)합니다.

## <a name="install-authentication-packages-to-your-application"></a>응용 프로그램에 인증 패키지를 설치 합니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 검색 하 고 설치 합니다 ***Microsoft.AspNet.Identity.Owin*** 패키지 있습니다. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. 검색 하 고 설치 합니다 ***Microsoft.Owin.Host.SystemWeb*** 패키지 있습니다.

    > [!NOTE]
    > 합니다 **Microsoft.Aspnet.Identity.Owin** 패키지에는 Asp.net Identity 패키지에서 사용할 수 있도록 OWIN 인증 미들웨어를 구성 하는 OWIN 확장 클래스의 집합을 포함 합니다.
    > 합니다 **Microsoft.Owin.Host.SystemWeb** 패키지 OWIN 기반 응용 프로그램을 ASP.NET 요청 파이프라인을 사용 하 여 IIS에서 실행할 수 있게 해 주는 OWIN 서버를 포함 합니다. 자세한 내용은 참조 [OWIN 미들웨어입니다. iis에서 통합 파이프라인](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md)합니다.

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>OWIN 시작 및 인증 구성 클래스를 추가 합니다.

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭, 선택 **추가**를 차례로 **새 항목 추가**합니다. 검색 텍스트 상자 대화 상자에서 "*owin*"입니다. 클래스 이름을 "*시작*"를 선택 하 고 **추가**합니다. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. Startup.cs 파일에서 OWIN 쿠키 인증을 구성 하려면 아래 표시 된 강조 표시 된 코드를 추가 합니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > 이 클래스는 포함 된 `OwinStartup` OWIN startup 클래스를 지정 하는 특성입니다. 모든 OWIN 응용 프로그램에 시작 클래스가 응용 프로그램 파이프라인에 대 한 구성 요소를 지정 하는 위치입니다. 참조 [OWIN 시작 클래스 검색](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) 이 모델에 대 한 자세한 내용은 합니다.

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>등록 하 고 사용자를 로그인에 대 한 웹 양식을 추가합니다

1. 엽니다는 *Register.aspx.cs* 파일과 등록에 성공 하면 다음 코드는 로그인 한 사용자를 추가 합니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - 프레임 워크 앱 개발자 생성 하도록 요구 되므로 ASP.NET Id 및 OWIN 쿠키 인증 클레임 기반 시스템에는 [ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) 사용자에 대 한 합니다. ClaimsIdentity에 사용자가 속한 역할 등 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다. 또한이 단계에서 사용자에 대 한 더 많은 클레임을 추가할 수 있습니다.
    > - OWIN 및 호출에서 AuthenticationManager를 사용 하 여 사용자 로그인 수 `SignIn` 위에 표시 된 대로 ClaimsIdentity를 전달 합니다. 이 코드는 사용자를 로그인 하 고도 쿠키를 생성 합니다. 이 호출은 비슷합니다 [FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 에서 사용 합니다 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈입니다.
2. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭, 선택 **추가**를 차례로 **Web Form**합니다. 웹 폼의 이름을 **로그인**합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. 내용을 대체 합니다 *Login.aspx* 를 다음 코드로 파일:

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. 내용을 대체 합니다 *Login.aspx.cs* 다음 파일:

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - 합니다 `Page_Load` 이제 현재 사용자의 상태를 확인 하 고 기반으로 하는 작업을 수행 해당 `Context.User.Identity.IsAuthenticated` 상태입니다.
    >     **로그인 한 사용자 이름 표시** : Microsoft ASP.NET Identity Framework의 확장 메서드를 추가 했습니다 [System.Security.Principal.IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) 가져올 수 있도록 합니다 `UserName` 및 `UserId` 사용자 로그인에 대 한 합니다. 에 정의 된 이러한 확장 메서드는 `Microsoft.AspNet.Identity.Core` 어셈블리입니다. 이러한 확장 메서드는 대체 [HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) 합니다.
    > - SignIn 메서드: `This` 메서드를 이전 대체 `CreateUser_Click` 이 샘플에 성공적으로 사용자를 만든 후 사용자 로그인 때 이제는 메서드.   
    >   Microsoft OWIN 프레임 워크에서 확장 메서드를 추가 했습니다 `System.Web.HttpContext` 에 대 한 참조를 가져올 수 있도록는 `IOwinContext`합니다. 이러한 확장 메서드에 정의 된 `Microsoft.Owin.Host.SystemWeb` 어셈블리입니다. 합니다 `OwinContext` 노출 클래스는 `IAuthenticationManager` 현재 요청에서 사용 가능한 인증 미들웨어 기능을 나타내는 속성입니다. 사용자를 사용 하 여 로그인 합니다 `AuthenticationManager` OWIN 및 호출 `SignIn` 전달는 `ClaimsIdentity` 위에 표시 된 대로. 생성할 앱 프레임 워크에 필요한 ASP.NET Id 및 OWIN 쿠키 인증 클레임 기반 시스템 이기 때문에 `ClaimsIdentity` 사용자에 대 한 합니다. `ClaimsIdentity` 사용자가 속한 역할 등 사용자에 대 한 모든 클레임에 대 한 정보입니다. 또한이 코드는 사용자를 로그인 하 고도 쿠키를 생성 합니다.이 단계에서 사용자에 대 한 더 많은 클레임을 추가할 수 있습니다. 이 호출은 비슷합니다 [FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 에서 사용 합니다 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈입니다.
    > - `SignOut` 방법: 에 대 한 참조를 가져옵니다 합니다 `AuthenticationManager` OWIN 및 호출에서 `SignOut`합니다. 이 비슷합니다 [FormsAuthentication.SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) 에서 사용 하는 메서드는 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈입니다.
5. 키를 눌러 **ctrl+f5** 을 빌드 및 웹 응용 프로그램을 실행 합니다. 새 사용자 이름 및 암호를 입력 한 다음 선택 **등록**합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   참고: 이 시점에서 새 사용자 생성 되어 로그인 됩니다.
6. 선택 된 **로그 아웃** 단추입니다. 로그 형식에 리디렉션됩니다.
7. 잘못 된 사용자 이름 또는 암호를 입력 하 고 선택 합니다 **로그인** 단추입니다. 
   `UserManager.Find` 메서드는 null이 고 오류 메시지를 반환 합니다. " *잘못 된 사용자 이름 또는 암호가* "표시 됩니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)
