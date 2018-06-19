---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: (Razor) 사이트 페이지는 ASP.NET 웹의 외부 사이트를 사용 하 여 로그인 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 Facebook, Google, Twitter, Yahoo, 및 다른 사이트를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인 하는 방법에 설명-즉,를 지 원하는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/21/2014
ms.topic: article
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 47d15686194b15b7b06a99d63125c19a41f91ed9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26530172"
---
<a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>외부 사이트를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Facebook, Google, Twitter, Yahoo, 및 다른 사이트를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인 하는 방법에 설명-즉, OAuth 및 OpenID 사이트에서 지 원하는 방법에 있습니다.
> 
> 학습 내용:
> 
> - WebMatrix 시작 사이트 템플릿의 사용 하는 경우 다른 사이트에서 로그인을 사용 하도록 설정 하는 방법.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `OAuthWebSecurity` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3

ASP.NET 웹 페이지에 대 한 지원 포함 [OAuth](http://oauth.net/) 및 [OpenID](http://openid.net/) 공급자입니다. 이러한 공급자를 사용 하 여 사용자가 로그인 하도록 하 할 Facebook, Twitter, Microsoft 및 Google에서 기존 자격 증명을 사용 하 여 사이트에 있습니다. 예를 들어 Facebook 계정을 사용 하 여 로그인, 사용자가 선택 하기만 Facebook 아이콘을 사용자 정보를 입력할 있습니다 Facebook 로그인 페이지로 리디렉션합니다. 그런 다음 사이트에서 자신의 계정으로 Facebook 로그인을 연결할 수 있습니다. 웹 페이지 멤버 자격 기능에도 사용자가 여러 로그인 (소셜 네트워킹 사이트에서의 로그인 포함)를 연결할 수 웹 사이트에서 단일 계정을 사용 하 여 합니다.

이 이미지에서 로그인 페이지를 보여 줍니다.는 **시작 사이트** 사용자 외부 계정으로 로그인을 사용 하도록 설정 하려면 Facebook, Twitter, Google 또는 Microsoft 아이콘을 선택할 수 있는 템플릿:

![외부 공급자](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

코드 몇 줄의 주석 처리 하 여 OAuth 및 OpenID 멤버 자격을 사용할 수 있습니다는 **시작 사이트** 템플릿. OAuth를 사용 하는 사용 하 여는 메서드 및 속성이 있으며 OpenID 공급자에서는 `WebMatrix.Security.OAuthWebSecurity` 클래스입니다. **시작 사이트** 완전 한 구성원 인프라를 포함 하는 서식 파일, 로그인 페이지, 멤버 자격 데이터베이스 및 모든 코드와 함께 완료 해야 사용자가 로그인 로컬 자격 증명 또는 다른 사이트에서 사용 하 여 사이트에 .

이 섹션에서는 사용자가을 기반으로 하는 사이트 외부 사이트에서 로그인을 사용 하는 방법의 예는 **시작 사이트** 템플릿. 시작 사이트를 만든 후 (세부 정보 수행)를 수행 합니다.

- OAuth 공급자 (Facebook, Twitter 및 Microsoft)를 사용 하는 사이트에 대해 외부 사이트에서 응용 프로그램을 만듭니다. 이렇게 하면 응용 프로그램 키를 해당 사이트에 대 한 로그인 기능을 호출 하기 위해 필요 합니다.
- OpenID 공급자 (Google)를 사용 하는 사이트, 응용 프로그램을 만들 필요가 없습니다. 모든 이러한 사이트에 로그인 하 고를 개발자 응용 프로그램을 만들 수 계정이 있어야 합니다.

    > [!NOTE]
    > Microsoft 응용 프로그램 로그인을 테스트 하기 위한 로컬 웹 사이트 URL을 사용할 수 없습니다는 작업 중인 웹 사이트에 대 한 라이브 URL만 허용 합니다.
- 사용 하려는 사이트에 대 한 로그인을 전송 하 고 적절 한 인증 공급자를 지정 하기 위해 웹 사이트의 몇 개의 파일을 편집 합니다.

이 문서에서는 다음과 같은 작업에 대 한 별도 지침을 제공합니다.

- [Google 로그인을 사용 하도록 설정](#To_enable_Google_logins)
- [Facebook 로그인을 사용 하도록 설정](#To_enable_Facebook_logins)
- [Twitter 로그인을 사용 하도록 설정](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>Google 로그인을 사용 하도록 설정

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.
2. 열기는  *\_AppStart.cshtml* 페이지 및 다음 코드 줄을 주석 처리 제거 합니다. 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>테스트 Google 로그인

1. 실행의 *default.cshtml* 사이트의 페이지를 선택 하 고는 **로그인** 단추입니다.
2. 에 *로그인* 페이지는 **다른 서비스를 사용 하 여 로그인 할** 섹션 중 하나를 선택는 **Google** 또는 **Yahoo** 전송 단추입니다. 이 예제에서는 Google 로그인을 사용 합니다. 

    웹 페이지 요청을 Google 로그인 페이지로 리디렉션합니다.

    ![Google 로그인](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. 기존 Google 계정 자격 증명을 입력 합니다.
4. Google 요청 하면 허용 하려는 *Localhost* 계정에서 정보를 사용 하려면 **허용**합니다.

    코드는 사용자를 인증 하 고 Google 토큰을 사용 하 고 웹 사이트에이 페이지를 반환 합니다. 이 페이지에서는 사용자가 자신의 Google 로그인에 웹 사이트에서 기존 계정을 연결 또는 외부 로그인으로 연결 하려면 사이트에서 새 계정을 등록할 수 있습니다.

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. 선택 된 **연결** 단추입니다. 브라우저 응용 프로그램의 홈 페이지를 반환합니다.

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>Facebook 로그인을 사용 하도록 설정

1. 이동 하 여 [Facebook 개발자 사이트](https://developers.facebook.com/apps) (로그인 아직 로그인 하는 경우).
2. 선택 된 **Create New App** 단추를 클릭 한 다음 지시에 따라 이름을 지정 하 고 새 응용 프로그램을 만듭니다.
3. 섹션에서 **앱은 Facebook과 통합 하는 방법을 선택**, 선택는 **웹 사이트** 섹션.
4. 입력은 **사이트 URL** 필드와 사이트의 URL (예를 들어 `http://www.example.com`). **도메인** 필드는 선택 사항 이지만 전체 도메인 인증을 제공 하는 데 사용할 수 있습니다 (예: *example.com*). 

    > [!NOTE]
    > 다음과 같은 URL 사용 하 여 로컬 컴퓨터에서 사이트를 실행 하는 경우 `http://localhost:12345` (여기서 번호는 로컬 포트 번호는)이이 값을 추가할 수 있습니다는 **사이트 URL** 사이트 테스트에 대 한 필드입니다. 그러나 언제 든 지 변경 내용을 로컬 사이트의 포트 번호를 업데이트 해야 합니다는 **사이트 URL** 응용 프로그램의 필드입니다.
5. 선택 된 **변경 내용 저장** 단추입니다.
6. 선택 된 **앱** 다시 탭 한 다음 응용 프로그램에 대 한 시작 페이지를 표시 합니다.
7. 복사는 **앱 ID** 및 **응용 프로그램 암호** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다. Facebook 공급자에 코드를 웹 사이트에서 이러한 값을 전달 합니다.
8. Facebook 개발자 사이트를 종료 합니다.

이제 변경 하 두 페이지 웹 사이트에서의 사용자에 게 있도록 자신의 Facebook 계정을 사용 하는 사이트에 로그인 할 수 있습니다.

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.
2. 열기는  *\_AppStart.cshtml* 페이지 및 Facebook OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다. 주석 처리가 제거 코드 블록은 다음과 같습니다. 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. 복사는 **앱 ID** 의 값으로 Facebook 응용 프로그램에서 값의 `appId` (인용 부호 제외) 내 매개 변수입니다.
4. 복사 **응용 프로그램 암호** 으로 Facebook 응용 프로그램에서 값의 `appSecret` 매개 변수 값입니다.
5. 파일을 저장한 후 닫습니다.

### <a name="testing-facebook-login"></a>Facebook 로그인을 테스트

1. 사이트의 실행 *default.cshtml* 페이지를 선택 하 고는 **로그인** 단추입니다.
2. 에 *로그인* 페이지는 **다른 서비스를 사용 하 여 로그인 할** 섹션에서 **Facebook** 아이콘입니다. 

    웹 페이지는 Facebook 로그인 페이지에 요청을 리디렉션합니다.

    ![oauth 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. Facebook 계정에 로그인 합니다. 

    코드는 Facebook 토큰을 사용 하 여 사용자를 인증 하 고 페이지를 반환 합니다 사이트의 로그인을 사용 하 여 Facebook 로그인을 연결할 수 있습니다. 사용자 이름이 나 전자 메일 주소에 채워지는 **전자 메일** 폼에 필드입니다.

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. 선택 된 **연결** 단추입니다. 

    브라우저 홈 페이지로 돌아가고에 기록 됩니다.

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>Twitter 로그인을 사용 하도록 설정

1. 찾아는 [Twitter 개발자 사이트](https://dev.twitter.com/)합니다.
2. 선택 된 **응용 프로그램을 만들** 에 연결 하 고 사이트에 로그인 합니다.
3. 에 **응용 프로그램을 만들** 양식에서 입력의 **이름** 및 **설명** 필드입니다.
4. 에 **웹 사이트** 필드 사이트의 URL을 입력 합니다 (예를 들어 `http://www.example.com`). 

    > [!NOTE]
    > 로컬 사이트를 테스트 하는 경우 (같은 URL을 사용 하 여 `http://localhost:12345`), Twitter URL을 허용 하지 않을 합니다. 그러나 로컬 루프백 IP 주소를 사용할 수 있습니다 (예를 들어 `http://127.0.0.1:12345`). 이 응용 프로그램을 로컬로 테스트 하는 과정이 간단해 집니다. 그러나 로컬 사이트의 포트 번호 변경 될 때마다 해야 업데이트는 **웹 사이트** 응용 프로그램의 필드입니다.
5. 에 **콜백 URL** 필드에, 사용자가 Twitter로 로그인 한 후에 반환 하는 웹 사이트의 페이지에 대 한 URL을 입력 합니다. 예를 들어 사용자 (로그인 상태를 인식 하)는 시작 사이트의 홈 페이지를 보내려면에 입력 된 동일한 URL을 입력에서 **웹 사이트** 필드입니다.
6. 조건에 동의 하 고 선택 된 **Twitter 응용 프로그램을 만드는** 단추입니다.
7. 에 **내 응용 프로그램** 방문 페이지를 만든 응용 프로그램을 선택 합니다.
8. 에 **세부 정보** 탭, 아래로 스크롤하여 선택한는 **내 액세스 토큰 만들기** 단추입니다.
9. 에 **세부 정보** 탭에서 복사 된 **소비자 키** 및 **소비자 암호** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다. Twitter 공급자에 코드를 웹 사이트에서 이러한 값을 전달 합니다.
10. Twitter 사이트를 종료 합니다.

이제 변경 하면 두 페이지에 웹 사이트의 사용자가 Twitter 계정을 사용 하 여 사이트에 로그인 할 수 있도록 합니다.

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.
2. 열기는  *\_AppStart.cshtml* 페이지 하 고 Twitter OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다. 주석 처리가 제거 코드 블록은 다음과 같습니다. 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. 복사는 **소비자 키** 의 값으로 Twitter 응용 프로그램에서 값의 `consumerKey` (인용 부호 제외) 내 매개 변수입니다.
4. 복사는 **소비자 암호** 의 값으로 Twitter 응용 프로그램에서 값의 `consumerSecret` 매개 변수입니다.
5. 파일을 저장한 후 닫습니다.

### <a name="testing-twitter-login"></a>Twitter 로그인 테스트

1. 실행의 *default.cshtml* 사이트의 페이지를 선택 하 고는 **로그인** 단추입니다.
2. 에 *로그인* 페이지는 **다른 서비스를 사용 하 여 로그인 할** 섹션에서 **Twitter** 아이콘입니다. 

    웹 페이지 요청을 만든 응용 프로그램에 대 한 Twitter 로그인 페이지로 리디렉션합니다.

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. Twitter 계정에 로그인 합니다.
4. 코드는 Twitter 토큰을 사용 하 여 사용자를 인증 하 고 돌아갑니다 페이지에 연결할 수 있습니다 웹 사이트 계정으로 로그인 합니다. 사용자 이름 또는 전자 메일 주소에 채워지는 **전자 메일** 폼에 필드입니다.

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. 선택 된 **연결** 단추입니다. 

    브라우저 홈 페이지로 돌아가고에 기록 됩니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


- [사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ASP.NET 웹 페이지 사이트에 보안 및 구성원 추가](https://go.microsoft.com/fwlink/?LinkID=202904)
