---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: MVC 5 만들기 Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on (C#)를 사용 하 여 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 사용자는 외부 인증에서 자격 증명을 사용 하 여 OAuth 2.0을 사용 하 여 로그인 할 수 있도록 하는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2015
ms.topic: article
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 8a9528f76b0166175f950543b4b8a7250bdf5100
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388768"
---
<a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on (C#)를 사용 하 여 ASP.NET MVC 5 앱 만들기
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 사용 하 여 사용자가 로그인 할 수 있도록 하는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다 [OAuth 2.0](http://oauth.net/2/) 외부 인증 공급자, 예: Facebook, Twitter, LinkedIn, Microsoft 또는 Google에서에서 자격 증명을 사용 합니다. 간단히 하기 위해이 자습서는 Facebook 및 Google에서 자격 증명을 사용 하 여 작업에 집중 합니다.
> 
> 수백만 명의 사용자는 이러한 외부 공급자를 사용 하 여 계정을 이미 있기 때문에 중요 한 장점을 제공 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 합니다. 이러한 사용자를 만들고 새 자격 증명 집합을 기억 없는 경우 사이트에 대 한 등록 싶다는 더욱 수 있습니다.
> 
> 참고 항목 [SMS 및 전자 메일 2 단계 인증을 사용 하 여 ASP.NET MVC 5 앱](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)합니다.
> 
> 또한 자습서에는 사용자의 프로필 데이터를 추가 하는 방법 및 역할을 추가 하는 멤버 API를 사용 하는 방법을 보여 줍니다. 이 자습서를 통해 작성 했습니다 [Rick Anderson](https://blogs.msdn.com/rickAndy) (하세요 me Twitter에서 팔 로우: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).


<a id="start"></a>
## <a name="getting-started"></a>시작

설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. Visual Studio를 설치 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상. Dropbox, GitHub, Linkedin, Instagram, 버퍼, Salesforce, 스트림, 스택 교환, Tripit, Twitch, Twitter, yahoo! 등을 사용 하 여 도움말을 참조 하세요 [샘플 프로젝트](https://github.com/matthewdunsdon/oauthforaspnet)합니다.

> [!NOTE]
> Visual Studio를 설치 해야 합니다 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상 Google OAuth 2를 사용 하 고 SSL 경고 없이 로컬로 디버그 합니다.


클릭 **새 프로젝트** 에서 합니다 **시작** 페이지 또는 사용자 메뉴를 사용 하 고 선택할 수 **파일**를 차례로 **새 프로젝트**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  
 

<a id="1st"></a>
## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

클릭 **새 프로젝트**을 선택한 후 **Visual C#** 한 다음 왼쪽의 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다. "MvcAuth" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서 클릭 **MVC**합니다. 인증이 없는 경우 **개별 사용자 계정**를 클릭 합니다 **인증 변경** 단추를 선택 **개별 사용자 계정**합니다. 체크 인하여 **클라우드에서 호스트**, 앱은 매우 쉽게 Azure에서 호스트할 수 있습니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

선택한 경우 **클라우드에서 호스트**, 구성 대화 상자를 완료 합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)


### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>NuGet을 사용 하 여 최신 OWIN 미들웨어를 업데이트 하려면

NuGet 패키지 관리자를 사용 하 여 업데이트 합니다 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)합니다. 선택 **업데이트** 왼쪽된 메뉴에서. 클릭할 수 있습니다 합니다 **모두 업데이트** 단추나 있습니다 (다음 이미지에 표시 됨)만 OWIN 패키지를 검색할 수 있습니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

아래 이미지에서 OWIN 패키지만 표시 됩니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

패키지 관리자 콘솔 (PMC)을 입력할 수 있습니다는 `Update-Package` 명령을 모든 패키지를 업데이트 합니다.

키를 눌러 **F5** 하거나 **ctrl+f5** 응용 프로그램을 실행 합니다. 아래 이미지에서 포트 번호가 1234입니다. 응용 프로그램을 실행 하는 경우 다른 포트 번호를 표시 됩니다.

브라우저 창의 크기에 따라 탐색 아이콘을 클릭 해야 합니다 **홈**를 **에 대 한**를 **연락처**, **등록**하 고 **로그인** 링크 합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>프로젝트의 SSL 설정

Google 및 Facebook과 같은 인증 공급자에 연결 하려면 IIS Express SSL을 사용 하도록 설정 해야 합니다. SSL을 사용 하 여 로그인 한 후 유지 하 고 HTTP로 다시 삭제 해야, 사용자 이름 및 암호와 네트워크를 통해 일반 텍스트로 전송 하는 SSL을 사용 하지 않고 암호 처럼 프로그램 로그인 쿠키는 합니다. 핸드셰이크를 수행 하 고 (즉, HTTPS HTTP 보다 느린 이유 대량의) 채널을 보호 하는 시간을 이미 사용 했습니다 외에, MVC 파이프라인 실행 되기 전에 미래를 현재 요청 확인 하지 않습니다 따라서 로그인 후 HTTP로 다시 리디렉션 요청을 훨씬 더 빠릅니다.

1. **솔루션 탐색기**를 클릭 합니다 **MvcAuth** 프로젝트입니다.
2. 프로젝트 속성을 표시 하려면 F4 키를 누릅니다. 또는 합니다 **뷰** 메뉴를 선택할 수 있습니다 **속성 창**합니다.
3. 변경 **SSL 사용** True로 합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. SSL URL을 복사 (될 `https://localhost:44300/` 다른 SSL 프로젝트를 만든 하지 않는 한).
5. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **MvcAuth** 프로젝트를 마우스 **속성**합니다.
6. 선택 된 **웹** 탭을 선택한 다음 SSL URL을 붙여 넣습니다 합니다 **프로젝트 Url** 상자입니다. 파일을 저장 합니다 (Ctl + S). 이 URL을 Facebook 및 Google 인증 앱을 구성 해야 합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. 추가 된 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 특성을 `Home` 모든 요청을 요구 하는 컨트롤러에서 HTTPS를 사용 해야 합니다. 추가 하는 것 보다 안전한 방법을 사용 합니다 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 응용 프로그램에는 필터입니다. 섹션을 참조 하세요 &quot;SSL 및 권한 부여 특성을 사용 하 여 응용 프로그램 보호&quot; tutoral 내에서 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. Home 컨트롤러의 일부는 다음과 같습니다.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 이전에 인증서를 설치한 경우이 섹션의 나머지 부분을 건너뛰고 이동할 [OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결 하는](#goog), 그렇지 않은 경우 자체 서명 된 신뢰 지침에 따라 IIS Express에서 생성 하는 인증서입니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. 읽기를 **보안 경고** 대화 상자 및 클릭 **예** 나타내는 localhost 인증서를 설치 하려는 경우.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE를 표시 합니다 *홈* 페이지 되며 SSL 경고가 없습니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome도 인증서를 수락 및 경고 없이 HTTPS 콘텐츠를 표시 됩니다. Firefox에서 경고를 표시 하므로 자체 인증서 저장소를 사용 합니다. 응용 프로그램에 대 한 안전 하 게 클릭할 수 **위험을 이해**합니다.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결

> [!WARNING]
> 현재 Google OAuth 지침은 [ASP.NET Core의 구성 Google 인증](/aspnet/core/security/authentication/social/google-logins)합니다.

1. 로 이동 합니다 [Google 개발자 콘솔](https://console.developers.google.com/)합니다.
2. 선택 하기 전에 프로젝트를 만들지 않은 경우 **자격 증명** 는 왼쪽된 탭을 선택한 후 **만들기**합니다.
3. 왼쪽된 탭에서 클릭 **자격 증명**합니다.
4. 클릭 **자격 증명을 만들어야** 한 다음 **OAuth 클라이언트 ID**합니다. 

    1. 에 **클라이언트 ID 만들기** 대화 상자에서 기본값을 그대로 **웹 응용 프로그램** 응용 프로그램 형식에 대 한 합니다.
    2. 설정 된 **권한이 부여 된 JavaScript** 위에서 사용 된 SSL URL 원본이 (`https://localhost:44300/` 다른 SSL 프로젝트를 만든 경우가 아니면)
    3. 설정 된 **권한이 부여 된 리디렉션 URI** 에:  
         `https://localhost:44300/signin-google`
5. OAuth 동의 화면 메뉴 항목을 클릭 한 다음에 전자 메일 주소 및 제품 이름을 설정 합니다. 양식을 클릭을 마쳤으면 **저장할**합니다.
6. 라이브러리 메뉴 항목 클릭, 검색 **Google + API**를 클릭 한 다음 활성화 키를 누릅니다.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   아래 이미지에서는 사용 가능한 Api를 보여 줍니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Google Api API 관리자에서 참조를 **자격 증명** 가져오려고 탭의 **클라이언트 ID**. 응용 프로그램 비밀을 사용 하 여 JSON 파일을 저장 하는 다운로드. 복사 및 붙여넣기 합니다 **ClientId** 및 **ClientSecret** 에 `UseGoogleAuthentication` 메서드를 *Startup.Auth.cs* 파일을 *App_Start* 폴더입니다. 합니다 **ClientId** 하 고 **ClientSecret** 아래 표시 된 값은 샘플 및 작동 하지 않습니다.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명을 단순하게 유지 하기 위해 샘플 위의 코드에 추가 됩니다. 참조 [ASP.NET 및 Azure App Service에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.
8. 키를 눌러 **ctrl+f5** 를 빌드하고 응용 프로그램을 실행 합니다. 클릭 합니다 **로그인** 링크 합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. 아래 **다른 서비스를 사용 하 여 로그인 할**, 클릭 **Google**합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 위의 단계를 하나라도 누락 되 면 HTTP 401 오류가 표시 됩니다. 위의 단계를 다시 확인 합니다. 필수 설정도 누락 되 면 (예를 들어 **제품 이름**); 인증이 작동 하려면 몇 분 정도 걸릴 수 있습니다, 누락 된 항목을 추가 하 고 저장 합니다.
10. 자격 증명을 입력할 Google 사이트로 리디렉션됩니다.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 자격 증명을 입력 한 후 방금 만든 웹 응용 프로그램에 권한을 부여 하려면 묻는 메시지가 나타납니다.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. 클릭 **수락**합니다. 이제 다시 이동 합니다는 **등록** Google 계정을 등록할 수 있는 MvcAuth 응용 프로그램의 페이지입니다. Gmail 계정에 사용 되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭 (즉, 인증에 사용할 하나)를 유지 하려는 합니다. **등록**을 클릭합니다.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Facebook에서 앱을 만들고 앱 프로젝트에 연결

> [!WARNING]
> 현재 Facebook OAuth2 인증 지침을 참조 하세요. [구성 Facebook 인증](/aspnet/core/security/authentication/social/facebook-logins)

Facebook OAuth2 인증을 위해 Facebook에서 만든 응용 프로그램에서 일부 설정의 프로젝트에 복사 해야 합니다.

1. 브라우저에서로 이동 [ https://developers.facebook.com/apps ](https://developers.facebook.com/apps) Facebook 자격 증명을 입력 하 여 로그인 합니다.
2. 이미 Facebook 개발자로 등록 되지 경우 클릭 **개발자로 등록** 등록 지침을 따릅니다.
3. 에 **앱** 탭을 클릭 **Create New App**합니다.

    ![새 앱 만들기](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image22.png)
4. 입력을 **앱 이름** 하 고 **범주**, 클릭 **앱 만들기**합니다.

    합니다 <strong>앱 Namespace</strong> 앱 인증을 위해 Facebook 응용 프로그램에 액세스를 사용 하 여 URL 부분 (예를 들어 https\://apps.facebook.com/{App Namespace}). 지정 하지 않으면를 <strong>앱 Namespace</strong>서 <strong>앱 ID</strong> URL에 사용 됩니다. 합니다 <strong>앱 ID</strong> 는 다음 단계에서 표시 되는 장기 시스템에서 생성 된 숫자입니다.

    ![새 앱 대화 상자 만들기](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image23.png)
5. 표준 보안 검사를 제출 합니다.

    ![보안 검사](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image24.png)
6. 선택 **설정을** 왼쪽된 메뉴 모음에 대 한![ Facebook 개발자의 메뉴 모음](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image25.png)
7. 에 **기본** 페이지의 설정 섹션 선택 **플랫폼 추가** 웹 사이트 응용 프로그램을 추가 하는 지정 합니다. ![기본 설정](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image26.png)
8. 선택 **웹 사이트** 플랫폼 선택 항목에서입니다.  
  
    ![플랫폼 선택](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image27.png)
9. 기록해 하 **앱 ID** 및 **App Secret** 이 자습서의 뒷부분에 나오는 MVC 응용 프로그램에 모두 추가할 수 있도록 합니다. 또한 사이트 URL을 추가 (`https://localhost:44300/`) MVC 응용 프로그램을 테스트 합니다. 또한 추가 된 **Contact Email**합니다. 그런 다음 선택 **변경 내용 저장**합니다.   

    ![기본 응용 프로그램 세부 정보 페이지](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image28.png)

    > [!NOTE]
    > 등록 한 전자 메일 별칭을 사용 하 여 인증할 수만 note 합니다. 다른 사용자와 테스트 계정을 등록할 수 되지 않습니다. Facebook 응용 프로그램에 대 한 다른 Facebook 계정 액세스를 부여할 수 있습니다 **개발자 역할** 탭 합니다.
10. Visual Studio에서 엽니다 *앱\_Start\Startup.Auth.cs*합니다.
11. 복사 및 붙여넣기 합니다 **AppId** 및 **App Secret** 에 `UseFacebookAuthentication` 메서드. 합니다 **AppId** 하 고 **App Secret** 아래 표시 된 값은 샘플 및 작동 하지 것입니다.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample3.cs?highlight=33-35,38-39)]
12. 클릭 **변경 내용을 저장**합니다.
13. 키를 눌러 **ctrl+f5** 응용 프로그램을 실행 합니다.


선택 **로그인** 로그인 페이지를 표시 합니다. 클릭 **Facebook** 아래에서 **다른 서비스를 사용 하 여 로그인 합니다.**

Facebook 자격 증명을 입력 합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image29.png)

공개 프로필 및 친구 목록에 액세스 하려면 응용 프로그램에 대 한 권한을 부여 하 라는 메시지가 표시 됩니다.

![Facebook 앱 세부 정보](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image30.png)

이제 로그인 됩니다. 이제 응용 프로그램을 사용 하 여이 계정에 등록할 수 있습니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image31.png)

항목에 추가 됩니다을 등록할 때 합니다 *사용자* 멤버 자격 데이터베이스의 테이블입니다.

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>멤버 자격 데이터를 검사 합니다.

에 **뷰** 메뉴에서 클릭 **서버 탐색기**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

확장 **DefaultConnection (MvcAuth)** 를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭 **AspNetUsers** 클릭 **테이블 데이터 표시**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 테이블 데이터](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>사용자 클래스에 프로필 데이터 추가

이 단원의 추가할 생년월일 및 홈 마을 사용자 데이터에 등록 하는 동안 다음 그림과에서 같이 합니다.

![reg 홈 town과 Bday를 사용 하 여](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

엽니다는 *Models\IdentityModels.cs* 파일 및 birth date 및 홈 마을 속성 추가:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

엽니다는 *Models\AccountViewModels.cs* 파일과 집합 birth date 및 홈 마을 속성 `ExternalLoginConfirmationViewModel`합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

열기는 *controllers\ accountcontroller.cs* 파일 및 birth date 및 홈 타운에 대 한 코드를 추가 합니다 `ExternalLoginConfirmation` 동작 메서드 같이:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

생년월일 및 홈 마을에 추가 합니다 *Views\Account\ExternalLoginConfirmation.cshtml* 파일:

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

다시 응용 프로그램에 Facebook 계정을 등록 하 고 새 생년월일 및 홈 마 프로필 정보를 추가할 수 있습니다 확인 수 있도록 멤버 자격 데이터베이스를 삭제 합니다.

**솔루션 탐색기**를 클릭 합니다 **모든 파일 표시** 아이콘을 마우스 오른쪽 단추로 클릭 *추가\_Data\aspnet-MvcAuth-&lt;날짜 스탬프&gt;.mdf* 누릅니다 **삭제**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

**도구** 메뉴에서 클릭 **NuGet 패키지 관리자**, 클릭 **패키지 관리자 콘솔** (PMC). PMC에서 다음 명령을 입력 합니다.

1. Enable-migrations
2. Add-migration Init
3. 데이터베이스 업데이트

응용 프로그램을 실행 하 고 FaceBook 및 Google을 사용 하 여 로그인 하 고 일부 사용자를 등록 합니다.

## <a name="examine-the-membership-data"></a>멤버 자격 데이터를 검사 합니다.

에 **뷰** 메뉴에서 클릭 **서버 탐색기**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

마우스 오른쪽 단추로 클릭 **AspNetUsers** 누릅니다 **테이블 데이터 표시**합니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

합니다 `HomeTown` 고 `BirthDate` 필드 아래에 표시 됩니다.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>로그 오프 앱 및 다른 계정으로 로그인

그런 다음 로그 아웃 및 로그인 하려고 Facebook, 사용 하 여 앱에 로그온 하는 경우 다시 (동일한 브라우저 사용) 다른 Facebook 계정을 사용 하 여 있습니다 즉시에 기록 됩니다 사용한 이전 Facebook 계정. 다른 계정을 사용 하려면 Facebook에 이동 하 고 Facebook에서 로그 아웃 해야 합니다. 모든 다른 타사 인증 공급자에 동일한 규칙이 적용 됩니다. 또는 다른 브라우저를 사용 하 여 다른 계정으로 기록할 수 있습니다.

## <a name="next-steps"></a>다음 단계

참조 [Yahoo 및 LinkedIn OAuth 보안 공급자를 OWIN에 대 한 소개](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Yahoo와 LinkedIn 지침은 Jerrie Pelser 여 합니다. Jerrie의를 참조 하세요. 소셜 로그인 단추 ASP.NET MVC 5의 소셜 로그인 단추 사용을 가져오려고 합니다.

내 자습서를 따릅니다 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data),이 자습서를 계속 하 고 다음을 보여 줍니다.

1. Azure에 앱을 배포 하는 방법입니다.
2. 역할을 사용 하 여 앱에 보안을 유지 하는 방법입니다.
3. 사용 하 여 앱을 보호 하는 방법을 합니다 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 하 고 [권한 부여](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 필터입니다.
4. 멤버 자격 API를 사용 하 여 사용자 및 역할을 추가 하는 방법.

이 자습서를 연결 하는 방법을 개선할 수 것에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [표시 코드 사용 방법 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다. 에 대 한 요청 하 고 ASP.NET에 추가 될 새 기능에 투표도 있습니다. 예를 들어를 도구용 투표할 수 있습니다 [사용자 및 역할 만들기 및 관리 합니다.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

ASP.NET 외부 인증 서비스가 작동 하는 방법의 좋은 설명 Robert McMurray의을 참조 하세요 [외부 인증 서비스](https://asp.net/web-api/overview/security/external-authentication-services)합니다. Robert의 기사는 Microsoft 및 Twitter 인증을 사용 하기 위한 세부 정보로도 포함 됩니다. Tom Dykstra의 뛰어난 [EF/MVC 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework를 사용 하는 방법을 보여 줍니다.
