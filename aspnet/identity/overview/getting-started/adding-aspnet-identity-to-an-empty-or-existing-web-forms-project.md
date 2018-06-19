---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: 프로젝트를 구성 하는 ASP.NET Identity 비어 있거나 기존 웹에 추가 합니다. | Microsoft Docs
author: raquelsa
description: 이 자습서에서는 ASP.NET 응용 프로그램에 ASP.NET Id (ASP.NET에 대 한 새 멤버 자격 시스템)를 추가 하는 방법을 보여 줍니다. 만들 때 새 MVC 또는 Web Forms 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/23/2013
ms.topic: article
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8961e596f0d6cc4810e2439be1ec2915bddb8c78
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874657"
---
<a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>프로젝트를 구성 하는 비어 있거나 기존 웹에 ASP.NET Id 추가
====================
으로 [Raquel Soares De Almeida](https://github.com/raquelsa)

> 이 자습서에서는 추가 하는 방법을 보여 줍니다 [ASP.NET Identity](introduction-to-aspnet-identity.md) (ASP.NET에 대 한 새 멤버 자격 시스템) ASP.NET 응용 프로그램에 있습니다.
> 
> 개별 계정으로 Visual Studio 2013 RTM에서 새 MVC 또는 Web Forms 프로젝트를 만들 때 Visual Studio는 필요한 모든 패키지를 설치 및 있습니다에 대 한 모든 필요한 클래스를 추가 합니다. 이 자습서는 ASP.NET Identity 지원을 기존 Web Forms 프로젝트 또는 비어 있는 새 프로젝트에 추가 하는 단계를 설명 합니다. 모든 NuGet 패키지를 설치 해야 할 및 클래스를 추가 해야 간략히 소개 합니다. 새 사용자 등록 및 사용자 관리 및 인증에 대 한 모든 주요 항목 지점 Api를 강조 표시 하는 동안 로그인에 대 한 샘플 Web Forms을 통해 전환 됩니다. 이 예제에서는 기본적으로 ASP.NET Identity Entity Framework에 만들어진 SQL 데이터 저장소에 대 한 사용 합니다. 이 자습서에서는 LocalDB는 SQL 데이터베이스에 대 한 사용 합니다.
> 
> 이 자습서는 Raquel Soares De Almeida 및 Rick Anderson에 의해 작성 되었으므로 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ).


## <a name="getting-started-aspnet-identity"></a>ASP.NET Identity를 시작 하기

1. 설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.
2. 클릭 **새 프로젝트** 시작 페이지 또는 있습니다 메뉴를 사용 하 여 선택할 **파일**, 차례로 **새 프로젝트**합니다.
3. 선택 **Visual C# i** n 왼쪽된 창 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다. "WebFormsIdentity" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.   
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image1.png)
4. 에 **새 ASP.NET 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   공지는 **인증 변경** 단추가 비활성화 되 고 인증 지원 되지 않습니다는이 서식 파일에서 제공 됩니다. Web Forms, MVC 및 Web API 템플릿을 사용 인증 접근 방법을 선택할 수 있습니다. 자세한 내용은 참조 [인증 개요](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth) 합니다.

## <a name="adding-identity-packages-to-your-app"></a>응용 프로그램에 Identity 패키지 추가

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 검색 텍스트 상자 대화 상자에 입력 "*Identity.E*"입니다. 이 패키지에 대 한 설치를 클릭 합니다.   
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image3.png)  
  
이 패키지에서는 종속성 패키지를 설치 하는 참고: EntityFramework 및 Microsoft ASP.NET Identity Core 합니다.

## <a name="adding-web-forms-to-register-users"></a>사용자가 등록 하는 Web Forms를 추가 합니다.

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, 차례로 **Web Form**합니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. 에 **항목에 대 한 이름 지정** 대화 상자에 새 web form 이름 **등록**, 클릭 하 고 **확인**
3. 생성 된 태그 바꿉니다 *Register.aspx* 아래 코드가 포함 된 파일입니다. 코드 변경 내용은 강조 표시되어 있습니다.   

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > 간단한 버전 이것이 *Register.aspx* 새 ASP.NET Web Forms 프로젝트를 만들 때 만들어지는 파일입니다. 위의 태그는 양식 필드와 새 사용자를 등록 하는 단추를 추가 합니다.
4. 열기는 *Register.aspx.cs* 파일 및 파일의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. 위의 코드는 단순화 된 버전의는 *Register.aspx.cs* 새 ASP.NET Web Forms 프로젝트를 만들 때 만들어지는 파일입니다.
    > 2. *IdentityUser* 클래스는 기본 EntityFramework 구현은 *IUser* 인터페이스입니다. *IUser* 인터페이스는 ASP.NET Identity Core에서 사용자에 대 한 최소 인터페이스입니다.
    > 3. *UserStore* 클래스는 사용자 저장소의 기본 EntityFramework 구현 합니다. 이 클래스는 ASP.NET Identity Core 최소한의 인터페이스를 구현: *IUserStore*, *IUserLoginStore*, *IUserClaimStore* 및 *IUserRoleStore* .
    > 4. *UserManager* 자동으로 변경 내용을 저장 하는 클래스는 사용자 관련 Api는 *UserStore*합니다.
    > 5. *IdentityResult* 클래스 id 작업의 결과 나타냅니다.
5. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, **ASP.NET 폴더 추가** 차례로 **앱\_데이터**합니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. 열기는 *Web.config* 파일 및 사용자 정보를 저장 하는 데 사용할 데이터베이스에 대 한 연결 문자열 항목을 추가 합니다. 데이터베이스가 만들어질 수 런타임에 EntityFramework 하 여 Identity 엔터티에 대 한 있습니다. 연결 문자열은 새 Web Forms 프로젝트를 만들 때 생성 한 비슷합니다. 강조 표시 된 코드를 추가 해야 태그를 보여 줍니다.

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > Visual Studio 2015 이상에서는 대체 `(localdb)\v11.0` 와 `(localdb)\MSSQLLocalDB` 연결 문자열에 있습니다.
    
7. 파일을 마우스 오른쪽 단추로 클릭 *Register.aspx* 에서 프로젝트를 선택 **시작 페이지로 설정**합니다. Ctrl + f 5를 눌러 작성 하 고 웹 응용 프로그램을 실행 하는 키를 누릅니다. 새 사용자 이름 및 암호를 입력 한 후에 클릭 **등록**합니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity은 유효성 검사를 지원 하며이 샘플에서 사용자 및 암호에 대 한 기본 동작을 확인할 수 있습니다 Identity Core 패키지에서 제공 하는 유효성 검사기입니다. 사용자에 대 한 기본 유효성 검사기 (`UserValidator`)에 속성이 `AllowOnlyAlphanumericUserNames` 기본값 설정 되어 있는 `true`합니다. 암호에 대 한 기본 유효성 검사기 (`MinimumLengthValidator`) 6 자 이상의 암호 인지 확인 합니다. 이러한 유효성 검사기는 속성에 `UserManager` 사용자 지정 유효성 검사를 포함 하려는 경우 재정의할 수 있습니다

## <a name="verifying-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>확인 Id LocalDb 데이터베이스 및 Entity Framework에서 생성 한 테이블

1. 에 **보기** 메뉴를 클릭 하 여 **서버 탐색기**합니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. 확장 **DefaultConnection (WebFormsIdentity)** 를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭 **AspNetUsers** 클릭 **테이블 데이터 표시**합니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configuring-the-application-for-owin-authentication"></a>OWIN 인증에 대 한 응용 프로그램 구성

이 시점에서 사용자 만들기에 대 한 지원만 추가 했습니다. 이제 하겠습니다 인증 사용자 로그인을 추가할 수 있는 방법을 보여 줍니다. 폼 인증을 위해 Microsoft OWIN 인증 미들웨어를 사용 하는 ASP.NET Identity 합니다. OWIN 쿠키 인증은 쿠키 및 클레임 기반된 인증 메커니즘에서 호스팅되는 모든 프레임 워크에서 사용할 수 있는 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) 또는 IIS 합니다. 이 모델을 ASP.NET MVC 및 Web Forms를 비롯 한 여러 프레임 워크에서 동일한 인증 패키지를 사용할 수 있습니다. 프로젝트 Katana 하 고 호스트 중립적인 보고 미들웨어를 실행 하는 방법에 대 한 자세한 내용은 [Katana 프로젝트 시작](https://msdn.microsoft.com/magazine/dn451439.aspx)합니다.

## <a name="installing-authentication-packages-to-your-application"></a>응용 프로그램에 인증 패키지를 설치합니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 검색 텍스트 상자 대화 상자에 입력 "*Identity.Owin*"입니다. 이 패키지에 대 한 설치를 클릭 합니다.   
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image10.png)
2. 패키지에 대 한 검색 ***Microsoft.Owin.Host.SystemWeb*** 하 고 설치 합니다.   

    > [!NOTE]
    > **Microsoft.Aspnet.Identity.Owin** 패키지를 관리 하 고 ASP.NET Identity Core 패키지에서 사용할 수 있도록 OWIN 인증 미들웨어를 구성 하는 OWIN 확장 클래스의 집합을 포함 합니다.  
    > **Microsoft.Owin.Host.SystemWeb** OWIN 기반 응용 프로그램을 ASP.NET 요청 파이프라인을 사용 하 여 IIS에서 실행 하는 OWIN 서버 패키지에 포함 되어 있습니다. 자세한 내용은 참조 [OWIN 미들웨어입니다. iis에서 통합 파이프라인](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md)합니다.

## <a name="adding-owin-startup-and-authentication-configuration-classes"></a>OWIN 시작 및 인증 구성 클래스 추가

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가**, 차례로 **새 항목 추가**합니다. 검색 텍스트 상자 대화 상자에 입력 "*owin*"입니다. 클래스의 이름을 "*시작*"를 클릭 하 고 **추가**합니다.   
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. Startup.cs 파일에서 OWIN 쿠키 인증을 구성 하려면 아래 표시 된 강조 표시 된 코드를 추가 합니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > 이 클래스에 포함 된 `OwinStartup` OWIN 시작 클래스를 지정 하기 위한 특성입니다. 모든 OWIN 응용 프로그램에 응용 프로그램 파이프라인에 대 한 구성 요소를 지정 하는 시작 클래스입니다. 참조 [OWIN 시작 클래스 검색](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) 이 모델에 대 한 자세한 정보에 대 한 합니다.

## <a name="adding-web-forms-for-registering-and-logging-in-users"></a>Web Forms를 등록 하 고 사용자가 로그인 추가

1. 열기는 *Register.cs* 파일을 등록에 성공 하면 사용자에 로깅하는 다음 코드를 추가 합니다. 변경 내용이 아래 강조 표시 됩니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - 프레임 워크를 생성 하는 앱 개발자 필요 ASP.NET Identity 및 OWIN 쿠키 인증 클레임 기반 시스템 이므로 [ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) 사용자에 대 한 합니다. ClaimsIdentity에 사용자가 속한 역할 등 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다. 또한이 단계에서 사용자에 대 한 더 많은 클레임을 추가할 수 있습니다.
    > - OWIN 및 호출에서 AuthenticationManager를 사용 하 여 사용자에 서명할 수 `SignIn` 위와 같이 ClaimsIdentity를 전달 합니다. 이 코드는 사용자에 로그인 하 고도 쿠키를 생성 합니다. 이 호출은 비슷합니다 [FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 에서 사용 하는 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈입니다.
2. **솔루션 탐색기**, 프로젝트 클릭을 마우스 오른쪽 단추로 클릭 **추가**, 차례로 **Web Form**합니다. 웹 폼의 이름을 **로그인**합니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. 내용을 대체는 *Login.aspx* 를 다음 코드로 파일:  

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. 내용을 대체는 *Login.aspx.cs* 다음 파일:  

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` 이제 현재 사용자의 상태를 확인 하 고 작업 실행에 따라 해당 `Context.User.Identity.IsAuthenticated` 상태입니다.  
    >     **사용자 이름에 로그 된 표시** : Microsoft ASP.NET Identity 프레임 워크에 확장 메서드를 추가 했습니다 [System.Security.Principal.IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) 를 얻을 수 있도록 하는 `UserName` 및 `UserId` 에 대 한는 사용자를 로그인합니다. 에 정의 된 이러한 확장 메서드는 `Microsoft.AspNet.Identity.Core` 어셈블리입니다. 이러한 확장 메서드는에 대 한 대체 [HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) 합니다.
    > - SignIn 방법:   
    >     `This` 메서드는 이전 대체 `CreateUser_Click` 이 샘플의 사용자를 성공적으로 만든 후 사용자의 기호 이제 메서드.   
    >  Microsoft OWIN 프레임 워크에 확장 메서드를 추가 했습니다 `System.Web.HttpContext` 에 대 한 참조를 가져올 수 있는 프로그램 `IOwinContext`합니다. 이러한 확장 메서드에 정의 된 `Microsoft.Owin.Host.SystemWeb` 어셈블리입니다. `OwinContext` 클래스가 노출 한 `IAuthenticationManager` 현재 요청에서 사용 가능한 인증 미들웨어 기능을 나타내는 속성입니다.  
    >  사용자를 사용 하 여 로그인의 `AuthenticationManager` OWIN 및 호출에서 `SignIn` 를 전달 하 고는 `ClaimsIdentity` 위와 같이 합니다.   
    >  응용 프로그램에서 생성 하면 프레임 워크에 필요 하 고 ASP.NET Identity OWIN 쿠키 인증 클레임 기반 시스템에 있으므로 `ClaimsIdentity` 사용자에 대 한 합니다.   
    >  `ClaimsIdentity` 사용자가 속한 역할 같은 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다. 이 단계에서 사용자에 대 한 더 많은 클레임을 추가할 수도 있습니다.  
    >  이 코드는 사용자에 로그인 하 고도 쿠키를 생성 합니다. 이 호출은 비슷합니다 [FormAuthentication.SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 에서 사용 하는 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈입니다.
    > - `SignOut` 방법:   
    >  에 대 한 참조는 `AuthenticationManager` OWIN 및 호출에서 `SignOut`합니다. 이 방법은 유사 [FormsAuthentication.SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) 사용 하는 방법의 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈입니다.
5. 키를 눌러 **Ctrl + f 5를 눌러** 작성 하 고 웹 응용 프로그램을 실행 합니다. 새 사용자 이름 및 암호를 입력 한 후에 클릭 **등록**합니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   참고:이 시점에서 새 사용자 만들고에 기록 합니다.
6. 클릭 **로그 아웃** 단추입니다. 로그인 폼으로 이동 합니다.
7. 에 잘못 된 사용자 이름 또는 암호 및 클릭 입력 **로그인** 단추입니다.   
   `UserManager.Find` 메서드는 null이 고 오류 메시지가 반환 됩니다: " *잘못 된 사용자 이름 또는 암호가* " 표시 됩니다.  
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)
