---
title: ASP.NET Core에서 Facebook, Google 및 외부 공급자 인증
author: rick-anderson
description: 이 자습서에는 외부 인증 공급자에 OAuth 2.0을 사용하여 ASP.NET Core 2.x 앱을 빌드하는 방법을 보여줍니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/social/index
ms.openlocfilehash: 19074d5014a09446ceec1b89449e78760fc8e7cf
ms.sourcegitcommit: 09bcda59a58019fdf47b2db5259fe87acf19dd38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51708376"
---
# <a name="facebook-google-and-external-provider-authentication-in-aspnet-core"></a>ASP.NET Core에서 Facebook, Google 및 외부 공급자 인증

작성자: [Valeriy Novytskyy](https://github.com/01binary) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

이 자습서에는 사용자가 외부 인증 공급자의 자격 증명으로 OAuth 2.0을 사용하여 로그인할 수 있도록 ASP.NET Core 2.x 앱을 빌드하는 방법을 보여줍니다.

[Facebook](xref:security/authentication/facebook-logins), [Twitter](xref:security/authentication/twitter-logins), [Google](xref:security/authentication/google-logins) 및 [Microsoft](xref:security/authentication/microsoft-logins) 공급자는 다음 섹션에서 다룹니다. 다른 공급자는 [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) 및 [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers)와 같은 타사 패키지에서 사용할 수 있습니다.

![Facebook, Twitter, Google Plus 및 Windows용 소셜 미디어 아이콘](index/_static/social.png)

사용자가 자신의 기존 자격 증명을 사용하여 로그인할 수 있게 되면 사용자에게 편리하고 로그인 프로세스를 관리하는 복잡성을 타사에 양도합니다. 소셜 로그인이 트래픽 및 고객 변환을 제공할 수 있는 방법에 대한 예제는 [Facebook](https://www.facebook.com/unsupportedbrowser) 및 [Twitter](https://dev.twitter.com/resources/case-studies)의 사례 연구를 참조하세요.

참고: 여기에 제공된 패키지는 OAuth 인증 흐름의 복잡성을 상당히 추상화하지만 문제를 해결하는 경우 자세히 이해해야 할 수도 있습니다. 많은 리소스를 사용할 수 있습니다. 예를 들어 [OAuth 2 소개](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2) 또는 [OAuth 2 이해](http://www.bubblecode.net/2016/01/22/understanding-oauth2/)를 참조하세요. [공급자 패키지의 ASP.NET Core 소스 코드](https://github.com/aspnet/Security/tree/master/src)를 확인하여 몇 가지 문제를 해결할 수 있습니다.

## <a name="create-a-new-aspnet-core-project"></a>새 ASP.NET Core 프로젝트 만들기

* Visual Studio 2017의 시작 페이지에서 또는 **파일** > **새로 만들기** > **프로젝트**를 통해 새 프로젝트를 만듭니다.

* **Visual C#** > **.NET Core** 범주에서 사용할 수 있는 **ASP.NET Core 웹 애플리케이션** 템플릿을 선택합니다.

![새 프로젝트 대화 상자](index/_static/new-project.png)

* **웹 응용 프로그램**을 누르고 **인증**이 **개별 사용자 계정**으로 설정되었는지 확인합니다.

![새 웹 응용 프로그램 대화 상자](index/_static/select-project.png)

참고: 이 자습서에서는 마법사의 위쪽에서 선택할 수 있는 ASP.NET Core 2.0 SDK 버전에 적용됩니다.

## <a name="apply-migrations"></a>마이그레이션 적용

* 앱을 실행하고 **로그인** 링크를 선택합니다.
* **Register as a new user**(새 사용자로 등록) 링크를 선택합니다.
* 새 계정의 메일과 암호를 입력한 다음 **등록**을 선택합니다.
* 지침에 따라 마이그레이션을 적용합니다.

## <a name="require-ssl"></a>SSL 필요

OAuth 2.0은 HTTPS 프로토콜을 통한 인증을 위해 SSL을 사용해야 합니다.

ASP.NET Core 2.1 이상에서 **웹 애플리케이션** 또는 **Web API** 프로젝트 템플릿을 사용하여 만든 프로젝트는 SSL을 사용하도록 자동으로 구성됩니다. 프로젝트 마법사의 **인증 변경 대화 상자**에서 **개별 사용자 계정** 옵션을 선택한 경우 앱이 안전한 기본 엔드포인트에서 시작됩니다.

자세한 내용은 <xref:security/enforcing-ssl>을 참조하세요.

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="use-secretmanager-to-store-tokens-assigned-by-login-providers"></a>SecretManager를 사용하여 로그인 공급자에 의해 할당된 토큰 저장

소셜 로그인 공급자는 등록 프로세스 중에 **응용 프로그램 ID** 및 **응용 프로그램 암호** 토큰을 할당합니다. 정확한 토큰 이름은 공급자에 따라 달라집니다. 이러한 토큰은 앱이 API에 액세스하는 데 사용하는 자격 증명을 나타냅니다. 토큰은 [Secret Manager](xref:security/app-secrets#secret-manager)의 도움으로 앱 구성에 연결할 수 있는 "암호"를 구성합니다. Secret Manager는 *appsettings.json*과 같은 구성 파일에 토큰을 저장하는 보다 안전한 대안입니다.

> [!IMPORTANT]
> Secret Manager는 개발 목적으로만 사용됩니다. [Azure Key Vault 구성 제공자](xref:security/key-vault-configuration)로 Azure 테스트 및 프로덕션 암호를 저장하고 보호할 수 있습니다.

[ASP.NET Core에서 개발 중인 앱 암호의 안전한 저장소](xref:security/app-secrets) 항목의 단계에 따라 아래의 각 로그인 공급자에 의해 할당된 토큰을 저장합니다.

## <a name="setup-login-providers-required-by-your-application"></a>응용 프로그램에 필요한 로그인 공급자 설정

다음 항목을 사용하여 해당 공급자를 사용하도록 응용 프로그램을 구성합니다.

* [Facebook](xref:security/authentication/facebook-logins) 지침
* [Twitter](xref:security/authentication/twitter-logins) 지침
* [Google](xref:security/authentication/google-logins) 지침
* [Microsoft](xref:security/authentication/microsoft-logins) 지침
* [다른 공급자](xref:security/authentication/otherlogins) 지침

[!INCLUDE[](includes/chain-auth-providers.md)]

## <a name="optionally-set-password"></a>필요에 따라 암호 설정

외부 로그인 공급자를 등록하는 경우 앱에 암호를 등록하지 않은 상태입니다. 그러면 사이트에 암호를 만들고 기억하지 않아도 되지만 외부 로그인 공급자에 따라 다르게 적용해야 합니다. 외부 로그인 공급자를 사용할 수 없는 경우 웹 사이트에 로그인할 수 없습니다.

외부 공급자로 로그인하는 프로세스 중에 설정한 전자 메일을 사용하여 암호를 만들고 로그인하려면:

* 오른쪽 위 모서리에 있는 **Hello &lt;이메일 별칭&gt;** 링크를 눌러 **관리** 보기로 이동합니다.

![웹 응용 프로그램 관리 뷰](index/_static/pass1a.png)

* **만들기** 탭

![암호 페이지 설정](index/_static/pass2a.png)

* 올바른 암호를 설정하고 사용자의 전자 메일을 사용하여 로그인하는 데 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

* 이 문서는 외부 인증을 고새하고 ASP.NET Core 앱에 외부 로그인을 추가하는 데 필요한 필수 구성 요소를 설명합니다.

* 앱에 필요한 공급자에 대한 로그인을 구성하기 위해 공급자 관련 페이지를 참조합니다.

* 사용자와 해당 액세스 및 새로 고침 토큰에 대한 추가 데이터를 유지할 수 있습니다. 자세한 내용은 <xref:security/authentication/social/additional-claims>을 참조하세요.
