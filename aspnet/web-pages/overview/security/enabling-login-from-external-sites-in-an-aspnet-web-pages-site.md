---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 페이지 (Razor) 사이트를 외부 ASP.NET 웹 사이트를 사용 하 여 로그인 합니다. | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 Facebook, Google, Twitter, Yahoo 및 다른 사이트를 사용 하 여 ASP.NET Web Pages (Razor) 사이트에 로그인 하는 방법에 설명-즉, 지 원하는 방법...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: a74b13e9d1ddb5bc02f4ea5184108de5e014ead0
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827532"
---
<a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>외부 사이트를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Facebook, Google, Twitter, Yahoo 및 다른 사이트를 사용 하 여 ASP.NET Web Pages (Razor) 사이트에 로그인 하는 방법에 설명-즉, OAuth 및 OpenID 사이트에서 지 원하는 방법입니다.
> 
> 학습할 내용:
> 
> - WebMatrix 시작 사이트 템플릿을 사용 하 여 다른 사이트에서 로그인을 사용 하도록 설정 하는 방법.
> 
> 문서에 도입 된 ASP.NET 기능은 다음과 같습니다.
> 
> - `OAuthWebSecurity` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - WebMatrix 3

ASP.NET 웹 페이지에 대 한 지원도 [OAuth](http://oauth.net/) 하 고 [OpenID](http://openid.net/) 공급자입니다. 이러한 공급자를 사용 하 여, Facebook, Twitter, Microsoft 및 Google에서 자신의 기존 자격 증명을 사용 하 여 사이트에 사용자가 로그인을 시킬 수 있습니다. 예를 들어 Facebook 계정을 사용 하 여 로그인 하려면 사용자만 선택할 수 Facebook 아이콘을 사용자 정보를 입력할 있습니다 Facebook 로그인 페이지로 리디렉션합니다. 그런 다음 사이트에서 자신의 계정으로 Facebook 로그인을 연결할 수 있습니다. 웹 사이트에서 단일 계정을 사용 하 여 웹 페이지 멤버 자격 기능에 관련 된 향상 기능을는 사용자가 여러 번의 로그인 (소셜 네트워킹 사이트에서의 로그인 포함)를 연결할 수 있습니다.

이 이미지에서 로그인 페이지를 표시 합니다 **시작 사이트** 템플릿을, 사용자가 외부 계정의 로그인을 사용 하도록 설정 하려면 Facebook, Twitter, Google 또는 Microsoft 아이콘을 선택할 수 있는:

![외부 공급자](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

몇 줄의 코드의 주석 처리를 제거 하 여 OAuth 및 OpenID 멤버 자격을 사용할 수 있습니다 합니다 **시작 사이트** 템플릿. 메서드 및 속성을 사용 하 여 OAuth를 사용 하 여 작업을 OpenID 공급자에는 `WebMatrix.Security.OAuthWebSecurity` 클래스입니다. 합니다 **시작 사이트** 템플릿은 정식 멤버 자격 인프라를 포함 하면 로그인 페이지, 멤버 자격 데이터베이스 및 모든 코드를 사용 하 여 전체 로컬 자격 증명 또는 다른 사이트에서 해당 항목을 사용 하 여 사이트에 사용자가 로그인 수 .

이 섹션에서는 사용자를 기반으로 하는 사이트 외부 사이트에서 로그인 하는 방법의 예제를 제공 합니다 **시작 사이트** 템플릿. 시작 사이트를 만든 후 (세부 정보 수행) 수행할 수 있습니다.

- OAuth 공급자 (Facebook, Twitter 및 Microsoft)를 사용 하는 사이트, 외부 사이트에서 응용 프로그램을 만듭니다. 이렇게 하면 해당 사이트에 대 한 로그인 기능을 호출 하기 위해 해야 하는 응용 프로그램 키입니다.
- OpenID 공급자 (Google)를 사용 하는 사이트에 대 한 응용 프로그램을 만들 필요가 없습니다. 이러한 사이트의 모든 로그인 하 고 개발자 응용 프로그램을 만들려면 계정이 있어야 합니다.

    > [!NOTE]
    > Microsoft 응용 프로그램 작업 웹 사이트에 대 한 라이브 URL에만 동의 로그인 테스트를 위해 로컬 웹 사이트 URL을 사용할 수 없습니다.
- 사용 하려는 사이트에 로그인을 제출 하 고 적절 한 인증 공급자를 지정 하기 위해 웹 사이트에서 몇 가지 파일을 편집 합니다.

이 문서에서는 다음 작업에 대 한 별도 지침을 제공 합니다.

- [Google 로그인을 사용 하도록 설정](#To_enable_Google_logins)
- [Facebook 로그인을 사용 하도록 설정](#To_enable_Facebook_logins)
- [Twitter 로그인을 사용 하도록 설정](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>Google 로그인을 사용 하도록 설정

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.
2. 엽니다는  *\_AppStart.cshtml* 페이지 및 코드의 다음 줄을 주석 처리 제거 합니다. 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>Google 로그인 테스트

1. 실행 합니다 *default.cshtml* 사이트의 페이지 선택 합니다 **로그인** 단추입니다.
2. 에 *로그인* 페이지를 **다른 서비스를 사용 하 여 로그인** 섹션 중 하나를 선택 합니다 **Google** 또는 **Yahoo** 제출 단추. 이 예제에서는 Google 로그인을 사용 합니다. 

    웹 페이지는 Google 로그인 페이지로 요청을 리디렉션합니다.

    ![Google 로그인](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. 기존 Google 계정 자격 증명을 입력 합니다.
4. Google 묻는 허용 것인지 *Localhost* 계정에서 정보를 사용 하려면 **허용**합니다.

    코드를 Google 토큰을 사용 하 여 사용자를 인증 하 고 웹 사이트에이 페이지에 반환 합니다. 이 페이지에서는 사용자가 Google 로그인을 웹 사이트에서 기존 계정을 연결 하거나 사용한 외부 로그인을 연결할 사이트에서 새 계정을 등록할 수 있습니다.

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. 선택 된 **연결** 단추입니다. 브라우저 응용 프로그램의 홈 페이지를 반환합니다.

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>Facebook 로그인을 사용 하도록 설정

1. 로 이동 합니다 [Facebook 개발자 사이트](https://developers.facebook.com/apps) (로그인 하는 아직 로그인 하지 않은 경우).
2. 선택 합니다 **Create New App** 단추를 클릭 한 다음 새 응용 프로그램을 만들고 이름을 따릅니다.
3. 단원의 **앱은 Facebook에 통합할 방법을 선택**를 선택 합니다 **웹 사이트** 섹션.
4. 입력 합니다 **사이트 URL** 사이트의 URL을 사용 하 여 필드 (예를 들어 `http://www.example.com`). 합니다 **도메인** 필드는 선택 사항 이지만 전체 도메인에 대 한 인증을 제공 하는 데 사용할 수 있습니다 (같은 *example.com*). 

    > [!NOTE]
    > 사이트 URL 사용 하 여 로컬 컴퓨터에서 실행 하는 경우와 같은 `http://localhost:12345` (여기서 번호는 로컬 포트 번호는)이이 값을 추가할 수 있습니다 합니다 **사이트 URL** 사이트 테스트에 대 한 필드입니다. 그러나 언제 든 지 변경 내용을 로컬 사이트의 포트 번호를 업데이트 해야 합니다 **사이트 URL** 응용 프로그램의 필드입니다.
5. 선택 된 **변경 내용 저장** 단추입니다.
6. 선택 된 **앱** 다시 탭 한 다음 응용 프로그램에 대 한 시작 페이지를 확인 합니다.
7. 복사 합니다 **앱 ID** 하 고 **앱 비밀** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다. Facebook 공급자에 게 웹 사이트 코드에서 이러한 값을 전달 합니다.
8. Facebook 개발자 사이트를 종료 합니다.

이제 변경 하면 두 페이지에 웹 사이트에서 사용자가 되도록 자신의 Facebook 계정을 사용 하 여 사이트에 로그인 할 수 됩니다.

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.
2. 엽니다는  *\_AppStart.cshtml* 페이지 및 Facebook OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다. 주석 처리가 제거 된 코드 블록은 다음과 같습니다. 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. 복사 합니다 **앱 ID** 값으로 Facebook 응용 프로그램에서 값을 `appId` (따옴표 포함) 내부 매개 변수입니다.
4. 복사본 **앱 비밀** Facebook 응용 프로그램에서 값을 `appSecret` 매개 변수 값입니다.
5. 파일을 저장한 후 닫습니다.

### <a name="testing-facebook-login"></a>Facebook 로그인 테스트

1. 사이트의를 실행 *default.cshtml* 선택한 페이지의 **로그인** 단추입니다.
2. 에 *로그인* 페이지를 **다른 서비스를 사용 하 여 로그인** 섹션을 선택 합니다 **Facebook** 아이콘입니다. 

    웹 페이지는 Facebook 로그인 페이지로 요청을 리디렉션합니다.

    ![oauth 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. Facebook 계정에 로그인 합니다. 

    코드는 Facebook 토큰을 사용 하 여 사용자 인증을 위해를 페이지에 반환 합니다 사이트의 로그인을 사용 하 여 Facebook 로그인을 연결할 수 있습니다. 사용자 이름 또는 전자 메일 주소에 채워집니다 합니다 **전자 메일** 양식의 필드입니다.

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. 선택 된 **연결** 단추입니다. 

    브라우저 홈 페이지로 돌아가고에 기록 됩니다.

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>Twitter 로그인을 사용 하도록 설정

1. 로 이동 합니다 [Twitter 개발자 사이트](https://dev.twitter.com/)합니다.
2. 선택 합니다 **앱 만들기** 에 연결 하 고 사이트에 로그인 합니다.
3. 에 **응용 프로그램을 만듭니다** 양식에서 입력 합니다 **이름** 및 **설명** 필드입니다.
4. 에 **웹 사이트** 필드에 사이트의 URL을 입력 합니다 (예를 들어 `http://www.example.com`). 

    > [!NOTE]
    > 로컬 사이트를 테스트 하는 경우 (같은 URL을 사용 하 여 `http://localhost:12345`), Twitter URL을 허용 하지 않을 수 있습니다. 그러나 로컬 루프백 IP 주소를 사용할 수 있습니다 (예를 들어 `http://127.0.0.1:12345`). 이 응용 프로그램을 로컬로 테스트 하는 과정을 간소화 합니다. 그러나 로컬 사이트의 포트 번호를 변경할 때마다 있습니다 업데이트 해야 합니다 **웹 사이트** 응용 프로그램의 필드입니다.
5. 에 **콜백 URL** 필드, 사용자가 Twitter로 로그인 한 후에 반환 하려는 웹 사이트의 페이지에 대 한 URL을 입력 합니다. 예를 들어, 시작 사이트 (해당 로그인 상태 인식)의 홈 페이지에 사용자를 보낼에 입력 된 동일한 URL을 입력 합니다 **웹 사이트** 필드입니다.
6. 선택한 조건에 동의 합니다 **Twitter 응용 프로그램을 만드는** 단추입니다.
7. 에 **내 응용 프로그램** 방문 페이지에서 만든 응용 프로그램을 선택 합니다.
8. 에 **세부 정보** 탭, 아래쪽으로 스크롤하여 선택한 합니다 **내 액세스 토큰 만들기** 단추입니다.
9. 에 **세부 정보** 탭에서 복사 합니다 **소비자 키** 및 **Consumer Secret** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다. 웹 사이트 코드에서 Twitter 공급자에 이러한 값을 전달 됩니다.
10. Twitter 사이트를 종료 합니다.

이제 변경한 두 페이지에 웹 사이트에서 사용자가 Twitter 계정을 사용 하 여 사이트에 로그인 할 수 있도록 합니다.

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.
2. 엽니다는  *\_AppStart.cshtml* 페이지 및 Twitter OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다. 주석 처리가 제거 된 코드 블록은 다음과 같습니다. 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. 복사 합니다 **소비자 키** 값으로 Twitter 응용 프로그램에서 값을 `consumerKey` (따옴표 포함) 내부 매개 변수입니다.
4. 복사 합니다 **Consumer Secret** 값으로 Twitter 응용 프로그램에서 값을 `consumerSecret` 매개 변수입니다.
5. 파일을 저장한 후 닫습니다.

### <a name="testing-twitter-login"></a>Twitter 로그인 테스트

1. 실행 합니다 *default.cshtml* 사이트의 페이지 선택 합니다 **로그인** 단추입니다.
2. 에 *로그인* 페이지를 **다른 서비스를 사용 하 여 로그인** 섹션을 선택 합니다 **Twitter** 아이콘입니다. 

    웹 페이지 요청을 만든 응용 프로그램에 대 한 Twitter 로그인 페이지로 리디렉션합니다.

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. Twitter 계정에 로그인 합니다.
4. 코드는 Twitter 토큰을 사용 하 여 사용자를 인증 하 하 고 돌아갑니다 페이지로 연결할 수 있습니다 웹 사이트 계정으로 로그인 합니다. 사용자 이름 또는 전자 메일 주소에 채워집니다 합니다 **전자 메일** 양식의 필드입니다.

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. 선택 된 **연결** 단추입니다. 

    브라우저 홈 페이지로 돌아가고에 기록 됩니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


- [사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkID=202904)
