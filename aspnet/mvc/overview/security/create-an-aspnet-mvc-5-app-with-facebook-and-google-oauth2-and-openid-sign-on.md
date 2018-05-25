---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: MVC 5 만들기 Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 (C#)로 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 사용자가 OAuth 2.0을 사용 하 여 외부 인증의 자격 증명으로 로그인 할 수 있는 ASP.NET MVC 5 웹 응용 프로그램을 작성 하는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2015
ms.topic: article
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: c289c209b50f0c2c1f2d8b15a3aedeaebf671d0b
ms.sourcegitcommit: 24c32648ab0c6f0be15333d7c23c1bf680858c43
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2018
---
<a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 (C#)으로 ASP.NET MVC 5 앱 만들기
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서를 사용 하 여 사용자가 로그인 할 수 있는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다. [OAuth 2.0](http://oauth.net/2/) 외부 인증 공급자는 Facebook, Twitter, LinkedIn, Microsoft 또는 Google 등에서 자격 증명을 사용 합니다. 간단한 설명을 위해이 자습서에서는 Facebook 및 Google 자격 증명 사용에 중점을 둡니다.
> 
> 수백만 명 이상의 사용자 계정을 이러한 외부 공급자와 함께 이미 있기 때문에 중요 한 장점을 제공 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 합니다. 이러한 사용자 더 만들고 새로운 자격 증명 집합을 기억 하지 않아도 되는 경우 사이트에 대 한 등록을 저장할 수 있습니다.
> 
> 참고 항목 [SMS 및 전자 메일 2 단계 인증을 사용 하는 ASP.NET MVC 5 앱](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)합니다.
> 
> 또한 자습서에는 사용자에 대 한 프로필 데이터를 추가 하는 방법 및 역할을 추가 하는 멤버 API를 사용 하는 방법을 보여 줍니다. 이 자습서에 의해 작성 되었으므로 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter에 따라 me: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).


<a id="start"></a>
## <a name="getting-started"></a>시작

설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. Visual Studio 설치 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상. 이 참조에 대 한 도움말 Dropbox, GitHub, Linkedin, Instagram, 버퍼, Salesforce, 스트림을, 스택 Exchange, Tripit, Twitch, Twitter, yahoo! 등, [샘플 프로젝트](https://github.com/matthewdunsdon/oauthforaspnet)합니다.

> [!NOTE]
> Visual Studio를 설치 해야 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 또는 Google OAuth 2를 사용 하 고 SSL 경고 없이 로컬로 디버깅할 이상.


클릭 **새 프로젝트** 에서 **시작** 페이지 또는 있습니다 메뉴를 사용 하 고 선택할 수 **파일**, 차례로 **새 프로젝트**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  
 

<a id="1st"></a>
## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

클릭 **새 프로젝트**을 선택한 후 **Visual C#** 다음 왼쪽에 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다. "MvcAuth" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

에 **새 ASP.NET 프로젝트** 대화 상자를 클릭 하 여 **MVC**합니다. 인증이 없으면 **개별 사용자 계정**, 클릭는 **인증 변경** 선택한 단추 **개별 사용자 계정**합니다. 확인 하 여 **클라우드의 호스트에에서**, 앱에서 Azure에서 호스팅할 매우 쉽게 됩니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

선택한 경우 **클라우드의 호스트에에서**, 구성 대화 상자를 완료 합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)


### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>NuGet을 사용 하 여 최신 OWIN 미들웨어를 업데이트 하려면

NuGet 패키지 관리자를 사용 하 여 업데이트 하는 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)합니다. 선택 **업데이트** 왼쪽된 메뉴에 있습니다. 클릭할 수는 **모두 업데이트** 단추나 있습니다 (다음 그림에 표시) OWIN 패키지만 검색할 수 있습니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

아래 이미지에는 OWIN 패키지에만 표시 됩니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

패키지 관리자 콘솔 (PMC)에서 입력할 수 있는 `Update-Package` 명령을 모든 패키지를 업데이트 합니다.

키를 눌러 **F5** 또는 **Ctrl + f 5** 응용 프로그램을 실행 합니다. 아래 이미지에 포트 번호가 1234입니다. 응용 프로그램을 실행 하는 경우에 다른 포트 번호를 표시 됩니다.

브라우저 창의 크기에 따라 탐색 아이콘을 클릭 해야 할 수 있습니다는 **홈**, **에 대 한**, **연락처**, **등록**및 **로그인** 링크 합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>프로젝트에서 SSL을 설정합니다.

같은 Google Facebook 인증 공급자에 연결 하려면 IIS Express SSL을 사용 하도록 설정 해야 합니다. SSL을 사용 하 여 로그인 한 후 유지 하 고 HTTP로 다시 삭제 해야로, 로그인 쿠키는 암호와 마찬가지로 사용자 이름 및 암호를으로 보내는 일반 텍스트에서 네트워크를 통해 SSL을 사용 하지 않고 합니다. 게다가 이미 수행 하는 데 핸드셰이크를 수행 하 고 (즉, HTTPS HTTP 보다 느린 있기 때문에 대량의) 채널을 보호 하는 데 시간이 MVC 파이프라인을 실행 하기 전에 현재 요청 또는 미래 확인 되지 않습니다 있으므로 로그인 한 후을 HTTP로 리디렉션 요청 훨씬 빠릅니다.

1. **솔루션 탐색기**, 클릭는 **MvcAuth** 프로젝트.
2. 프로젝트 속성을 표시 하려면 F4 키를 누릅니다. 또는 **보기** 메뉴를 선택할 수 있습니다 **속성 창**합니다.
3. 변경 **SSL 사용 가능** True로 합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. SSL URL 복사 (될 `https://localhost:44300/` 다른 SSL 프로젝트 생성 하지 않는 한).
5. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **MvcAuth** 프로젝트를 마우스 선택 **속성**합니다.
6. 선택 된 **웹** 탭을 클릭 한 다음에 SSL URL을 붙여는 **프로젝트 Url** 상자입니다. 파일 저장 합니다 (Ctl + S). 이 URL을 Facebook 및 Google 인증 앱을 구성 해야 합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. 추가 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 특성을 `Home` 모든 요청을 요구 하도록 컨트롤러는 HTTPS를 사용 해야 합니다. 추가 하는 것 보다 안전한 방법은 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 응용 프로그램에는 필터입니다. 섹션을 참조 &quot;SSL과 인증 특성을 사용 응용 프로그램을 보호&quot; tutoral 내에서 [인증 및 SQL DB ASP.NET MVC 응용 프로그램 만들기 및 Azure 앱 서비스 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. Home 컨트롤러의 일부는 다음과 같습니다.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 이전에 인증서를 설치한 경우이 섹션의 나머지 부분을 건너뛰고 이동할 [OAuth 2에 대 한 Google 앱을 만들고 응용 프로그램 프로젝트에 연결할](#goog), 그렇지 않으면 자체 서명 된 신뢰 하도록 지시에 따라 IIS Express에서 생성 하는 인증서입니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. 읽기는 **보안 경고** 대화 상자와 클릭 **예** 나타내는 localhost 인증서를 설치 하려는 경우.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE 표시는 *홈* 페이지 및 SSL 경고가 없습니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome 인증서도 받아들이고 경고 HTTPS 콘텐츠만 표시 됩니다. Firefox에서 경고를 표시 하므로 인증서 저장소를 사용 합니다. 응용 프로그램에 대해 클릭할 수 있는 안전 하 게 **위험을 이해**합니다.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>OAuth 2에 대 한 Google 앱 만들기 및 앱 프로젝트 연결

> [!WARNING]
> 현재 Google OAuth 지침은 [에서 ASP.NET Core 구성 Google 인증](/aspnet/core/security/authentication/social/google-logins)합니다.

1. 탐색 하 고 [Google 개발자 콘솔](https://console.developers.google.com/)합니다.
2. 이전 프로젝트를 만들지 않은 경우 선택 **자격 증명** 왼쪽된 탭 한 다음 선택에서 **만들기**합니다.
3. 왼쪽된 탭에서 클릭 **자격 증명**합니다.
4. 클릭 **자격 증명을 만들어** 다음 **OAuth 클라이언트 ID**합니다. 

    1. 에 **클라이언트 ID 만들기** 대화 상자에서 기본값을 그대로 두고 **웹 응용 프로그램** 응용 프로그램 종류에 대 한 합니다.
    2. 설정의 **권한이 JavaScript** 위에서 사용한 SSL URL 원본이 (`https://localhost:44300/` 다른 SSL 프로젝트 생성 하지 않는 한)
    3. 설정의 **권한이 부여 된 리디렉션 URI** 에:  
         `https://localhost:44300/signin-google`
5. OAuth 동의 화면 메뉴 항목을 클릭 한 다음 전자 메일 주소 및 제품 이름을 설정 합니다. 양식 클릭을 완료 한 경우 **저장**합니다.
6. 라이브러리 메뉴 항목을 클릭, 검색 **Google + API**를 클릭 한 다음 활성화 키를 누릅니다.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   아래 이미지에서는 활성화 된 Api를 보여 줍니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Google Api API 관리자에서 참조 된 **자격 증명** 얻으려고 탭은 **클라이언트 ID**합니다. 응용 프로그램 암호 있는 JSON 파일을 저장 하려면 다운로드 하십시오. 복사 및 붙여넣기의 **ClientId** 및 **ClientSecret** 에 `UseGoogleAuthentication` 에 있는 메서드가 *Startup.Auth.cs* 파일에 *App_Start* 폴더입니다. **ClientId** 및 **ClientSecret** 아래 표시 된 값은 샘플 및 작동 하지 않습니다.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명은 위의 예제를 단순하게 유지 하기 위해 코드에 추가 됩니다. 참조 [ASP.NET 및 Azure 앱 서비스에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.
8. 키를 눌러 **CTRL + f 5** 작성 하 고 응용 프로그램을 실행 합니다. 클릭는 **로그인** 링크 합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. 아래 **다른 서비스를 사용 하 여 로그인 할**, 클릭 **Google**합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 위의 단계를 수행 하지 HTTP 401 오류를 얻게 됩니다. 위의 단계를 다시 확인 합니다. 필수 설정 수행 되지 않은 경우 (예를 들어 **제품 이름**), 누락 된 항목을 추가 하 고 저장; 인증이 작동 하려면 몇 분 정도 걸릴 수 있습니다.
10. 자격 증명을 입력할 Google 사이트로 이동 합니다.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 자격 증명을 입력 한 후 방금 만든 웹 응용 프로그램에 권한을 부여 하 라는 메시지가 표시 됩니다.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. 클릭 **수락**합니다. 이제 다시 이동 합니다는 **등록** Google 계정을 등록할 수 있는 MvcAuth 응용 프로그램의 페이지입니다. Gmail 계정에 사용 되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭 (즉, 인증에 사용할 하나)을 유지 하려면. **등록**을 클릭합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Facebook에서 앱을 만들기 및 앱 프로젝트에 연결

> [!WARNING]
> 현재 Facebook OAuth2 인증 지침은 [구성 Facebook 인증](/aspnet/core/security/authentication/social/facebook-logins)

Facebook OAuth2 인증에 대 한 Facebook에서 만드는 응용 프로그램에서 일부 설정의 프로젝트에 복사 해야 합니다.

1. 브라우저에서로 이동 [ https://developers.facebook.com/apps ](https://developers.facebook.com/apps) Facebook 자격 증명을 입력 하 여 로그인 하십시오.
2. Facebook 개발자 아직 등록 되지 경우 클릭 **개발자 등록** 등록 지침을 따릅니다.
3. 에 **앱** 탭을 클릭 **Create New App**합니다.

    ![새 앱 만들기](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image22.png)
4. 입력 한 **응용 프로그램 이름** 및 **범주**, 클릭 **앱 만들기**합니다.

    Facebook에서 고유 해야 합니다. <strong>앱 Namespace</strong> 앱 하는 인증에 대 한 Facebook 응용 프로그램에 액세스 하는 데 사용할 URL의 일부 (예를 들어 https://apps.facebook.com/{App Namespace}). 지정 하지 않으면는 <strong>앱 Namespace</strong>, <strong>앱 ID</strong> URL에 사용 됩니다. <strong>앱 ID</strong> 긴 시스템에서 생성 된 번호는 다음 단계에 표시 되는입니다.

    ![새 응용 프로그램 대화 상자 만들기](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image23.png)
5. 표준 보안 검사를 제출 합니다.

    ![보안 검사](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image24.png)
6. 선택 **설정** 왼쪽된 메뉴 모음의![ Facebook 개발자의 메뉴 모음](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image25.png)
7. 에 **기본** 페이지의 설정 섹션을 선택 **추가 플랫폼** 웹 사이트 응용 프로그램을 추가 지정할 수 있습니다. ![기본 설정](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image26.png)
8. 선택 **웹 사이트** 플랫폼 선택 항목 중에서 합니다.  
  
    ![플랫폼 선택](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image27.png)
9. 메모 프로그램 **앱 ID** 하였고 **응용 프로그램 암호** 이 자습서의 뒷부분에 나오는 모두 MVC 응용 프로그램에 추가할 수 있습니다. 또한 사이트 URL을 추가 (`https://localhost:44300/`) MVC 응용 프로그램을 테스트 합니다. 또한 추가 된 **Contact Email**합니다. 그런 다음 선택 **변경 내용 저장**합니다.   

    ![기본 응용 프로그램 세부 정보 페이지](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image28.png)

    > [!NOTE]
    > Note 등록 전자 메일 별칭을 사용 하 여 인증할 수만 있습니다. 다른 사용자와 테스트 계정이 됩니다 등록할 수 있습니다. Facebook에서 응용 프로그램에 대 한 다른 Facebook 계정 액세스 권한을 부여할 수 있습니다 **개발자 역할** 탭 합니다.
10. Visual Studio에서 열고 *앱\_Start\Startup.Auth.cs*합니다.
11. 복사 및 붙여넣기의 **AppId** 및 **응용 프로그램 암호** 에 `UseFacebookAuthentication` 메서드. **AppId** 및 **응용 프로그램 암호** 아래 표시 된 값은 샘플 및 작동 하지 것입니다.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample3.cs?highlight=33-35,38-39)]
12. 클릭 **ब ा ळ**합니다.
13. 키를 눌러 **CTRL + f 5** 응용 프로그램을 실행 합니다.


선택 **로그인** 로그인 페이지를 표시 합니다. 클릭 **Facebook** 아래 **필요한 다른 서비스가 사용 하 여 로그인 합니다.**

Facebook 자격 증명을 입력 합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image29.png)

공개 프로필 및 친구 목록에 액세스 하는 응용 프로그램에 대 한 권한을 부여 하 라는 메시지가 표시 됩니다.

![Facebook 응용 프로그램 세부 정보](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image30.png)

이제 로깅됩니다. 이제 응용 프로그램과 함께이 계정을 등록할 수 있습니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image31.png)

등록 하면 항목에 추가 됩니다는 *사용자* 멤버 자격 데이터베이스의 테이블입니다.

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>멤버 자격 데이터를 검사 합니다.

에 **보기** 메뉴를 클릭 하 여 **서버 탐색기**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

확장 **DefaultConnection (MvcAuth)** 를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭 **AspNetUsers** 클릭 **테이블 데이터 표시**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 테이블 데이터](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>프로필 데이터를 사용자 클래스에 추가합니다.

이 섹션에 추가 합니다 생년월일 및 홈 도시 사용자 데이터를 등록 하는 동안 다음 그림에 나와 있는 것 처럼.

![홈 동 및 Bday reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

열기는 *Models\IdentityModels.cs* 파일 및 birth date 및 홈 동 속성 추가:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

열기는 *Models\AccountViewModels.cs* 파일 및 집합에서 날짜 및 홈 동 속성 birth `ExternalLoginConfirmationViewModel`합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

열기는 *Controllers\AccountController.cs* 파일 및 코드의 날짜 및 홈 동 생년월일에 대 한 추가 `ExternalLoginConfirmation` 동작 메서드 같이:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

생년월일 및 홈 도시에 추가 된 *Views\Account\ExternalLoginConfirmation.cshtml* 파일:

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

다시 응용 프로그램과 함께 Facebook 계정을 등록 하 고 새 생년월일 및 홈 동 프로필 정보를 추가할 수 있습니다 확인 수 있도록 멤버 자격 데이터베이스를 삭제 합니다.

**솔루션 탐색기**, 클릭는 **모든 파일 표시** 아이콘을 다음 마우스 오른쪽 단추로 클릭 *추가\_Data\aspnet-MvcAuth-&lt;날짜 스탬프&gt;.mdf* 클릭 **삭제**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

**도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자**, 클릭 **패키지 관리자 콘솔** (PMC). PMC에서 다음 명령을 입력 합니다.

1. Enable-migrations
2. 추가 마이그레이션 초기화
3. 데이터베이스 업데이트

응용 프로그램을 실행 하 고 FaceBook 및 Google에 로그인 하 고 일부 사용자를 등록에 사용 합니다.

## <a name="examine-the-membership-data"></a>멤버 자격 데이터를 검사 합니다.

에 **보기** 메뉴를 클릭 하 여 **서버 탐색기**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

마우스 오른쪽 단추로 클릭 **AspNetUsers** 클릭 **테이블 데이터 표시**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

`HomeTown` 및 `BirthDate` 필드 아래에 표시 됩니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>로그 앱 오프 하 고 다른 계정으로 로그인

Facebook, 사용 하 여 앱에 로그온 하 고 다음 로그 아웃 및 로그인 하려고 하는 경우 다시 (동일한 브라우저 사용), 다른 Facebook 계정으로 있습니다 즉시에 기록 됩니다 사용한 Facebook 계정 이전 합니다. 다른 계정을 사용 하려면 Facebook을 찾아 Facebook에서 로그 아웃 해야 합니다. 모든 다른 타사 인증 공급자에 동일한 규칙이 적용 됩니다. 또는 다른 브라우저를 사용 하 여 다른 계정으로 기록할 수 있습니다.

## <a name="next-steps"></a>다음 단계

참조 [Yahoo 및 LinkedIn OAuth 보안 공급자 OWIN에 대 한 소개](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Yahoo 및 LinkedIn 지침은 Jerrie Pelser 여 합니다. Jerrie의 참조 사용 소셜 로그인 단추를 가져오려는 ASP.NET MVC 5에 대 한 소셜 로그인 단추가 정말 합니다.

내 자습서에 따라 [인증 및 SQL DB ASP.NET MVC 응용 프로그램 만들기 및 Azure 앱 서비스 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data),이 자습서를 계속 하 고 다음을 보여 줍니다.

1. Azure에 응용 프로그램을 배포 하는 방법입니다.
2. 역할과 응용 프로그램을 보호 하는 방법입니다.
3. 응용 프로그램을 보호 하는 방법의 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 및 [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 필터입니다.
4. 사용자 및 역할에 추가할 구성원 API를 사용 하는 방법.

이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다. 에 게 요청 하 고 ASP.NET에 추가할 수 있는 새로운 기능에 대해 투표도 있습니다. 예를 들어를 도구에 대 한 투표 수 [만들고 사용자 및 역할을 관리 합니다.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

ASP.NET 외부 인증 서비스가 작동 하는 방법의 좋은 설명 Robert McMurray의을 참조 하십시오. [외부 인증 서비스](https://asp.net/web-api/overview/security/external-authentication-services)합니다. Microsoft 및 Twitter 인증을 사용 하기 위한 정보를 확인할 Robert의 문서도 이동 합니다. Tom Dykstra의 뛰어난 [EF/MVC 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework와 함께 작업 하는 방법을 보여 줍니다.
