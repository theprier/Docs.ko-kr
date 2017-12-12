---
uid: web-api/overview/security/external-authentication-services
title: "외부 인증 서비스가 ASP.NET web API (C#) | Microsoft Docs"
author: rmcmurray
description: "외부 인증 서비스를 사용 하 여 ASP.NET Web API에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2013
ms.topic: article
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: 5d6e6727f387d047e7b41a6efa0d2dadf467558e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="external-authentication-services-with-aspnet-web-api-c"></a>외부 인증 서비스가 ASP.NET web API (C#)
====================
으로 [Robert McMurray](https://github.com/rmcmurray)

Visual Studio 2013 및 ASP.NET 4.5.1에 대 한 보안 옵션을 확장 [단일 페이지 응용 프로그램](../../../single-page-application/index.md) (SPA) 및 [웹 API](../../index.md) 몇 가지를 포함 하는 외부 인증 서비스와 통합 하는 서비스 OAuth/OpenID 및 소셜 미디어 인증 서비스: Microsoft 계정, Twitter, Facebook 및 Google 합니다.

### <a name="in-this-walkthrough"></a>이 연습에서

- [외부 인증 서비스를 사용 하 여](#USING)
- [샘플 웹 응용 프로그램 만들기](#SAMPLE)
- [Facebook 인증을 사용 하도록 설정](#FACEBOOK)
- [Google 인증을 사용 하도록 설정](#GOOGLE)
- [Microsoft 인증을 사용 하도록 설정](#MICROSOFT)
- [Twitter 인증 사용](#TWITTER)
- [추가 정보](#MOREINFO)

    - [외부 인증 서비스를 결합합니다.](#COMBINE)
    - [정규화 된 도메인 이름을 사용 하 여 IIS Express를 구성 합니다.](#FQDN)
    - [Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법](#OBTAIN)
    - [로컬 등록을 사용 하지 않도록 선택 사항:](#DISABLE)

### <a name="prerequisites"></a>필수 구성 요소

이 연습에서 예제를 수행 하려면 다음 조건이 충족 해야 합니다.

- Visual Studio 2013
- 다음과 같은 외부 인증 서비스 중 하나 이상에 대 한 계정:

    - Google 사용자 계정
    - 응용 프로그램 식별자 및 다음과 같은 소셜 미디어 인증 서비스 중 하나에 대 한 비밀 키와 함께 개발자 계정:

        - Microsoft 계정 ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))
        - Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))
        - Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>외부 인증 서비스를 사용 하 여

다양 한 개발을 줄이기 위해 웹 개발자 도움말을 현재 사용할 수 있는 외부 인증 서비스는 새로운 웹 응용 프로그램을 만들 때 시간입니다. 웹 사용자 일반적으로 여러 기존 계정이 있는 인기 있는 웹 서비스 및 소셜 미디어 웹 사이트에 대 한 따라서는 웹 응용 프로그램으로 구현 외부 웹 서비스 또는 소셜 미디어 웹 사이트에서 인증 서비스를 저장할 때 개발 시는 소요 된 인증 구현을 만들기. 웹 응용 프로그램에 대해 다른 계정을 만들지 않아도 및 다른 사용자 이름 및 암호를 기억 하지 않아도 최종 사용자가 저장 하는 외부 인증 서비스를 사용 하 여 합니다.

이전에 개발자는 했습니다 두 가지 선택 사항: 자체 인증 구현을 만들거나 외부 인증 서비스 응용 프로그램에 통합 하는 방법을 알아봅니다. 가장 기본적인 수준에서 다음 다이어그램은 외부 인증 서비스를 사용 하도록 구성 된 웹 응용 프로그램에서 정보를 요청 하는 사용자 에이전트 (웹 브라우저)에 대 한 간단한 요청 흐름을 보여줍니다.

[![](external-authentication-services/_static/image2.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image1.png)

위 다이어그램에 사용자 에이전트 (또는이 예제에서 웹 브라우저) 외부 인증 서비스에 웹 브라우저를 리디렉션하는 웹 응용 프로그램을 요청을 합니다. 사용자 에이전트 자격 증명을 외부 인증 서비스에 보내고 몇 가지 형태의 원래 웹 응용 프로그램에 외부 인증 서비스에서 사용자 에이전트를 리디렉션할 사용자 에이전트에 성공적으로 인증 하는 경우는 토큰의 사용자 에이전트에서 웹 응용 프로그램으로 보냅니다. 웹 응용 프로그램 외부 인증 서비스에서 사용자 에이전트를 성공적으로 인증 된 하 고 웹 응용 프로그램 사용자 에이전트에 대 한 추가 정보를 수집 토큰을 사용할 수 있는지 확인 하는 토큰을 사용 합니다. 응용 프로그램이 작업이 완료 되 면 사용자 에이전트의 정보를 처리 하는, 웹 응용 프로그램은 반환 권한 부여 설정에 따라 사용자 에이전트에 대 한 적절 한 응답입니다.

이 두 번째 예에서 사용자 에이전트는 웹 응용 프로그램 및 외부 권한 부여 서버와 협상 하 고 사용자에 대 한 추가 정보를 검색 하기 위해 외부 권한 부여 서버와 추가 통신을 수행 하는 웹 응용 프로그램 에이전트:

[![](external-authentication-services/_static/image4.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image3.png)

Visual Studio 2013 및 ASP.NET 4.5.1 쉽게 외부 인증 서비스와의 통합 개발자를 위한 다음과 같은 인증 서비스에 대 한 기본 제공 통합을 제공 하 여:

- Facebook
- Google
- Microsoft 계정 (Windows Live ID 계정)
- Twitter

이 연습에 나와 있는 예제에서는 Visual Studio 2013과 함께 제공 되는 새 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 각 지원 되는 외부 인증 서비스를 구성 하는 방법을 보여 줍니다.

> [!NOTE]
> 필요한 경우에 FQDN 외부 인증 서비스에 대 한 설정에 추가 해야 합니다. 이 요구 사항은 응용 프로그램 설정에 FQDN 클라이언트에서 사용 되는 FQDN과 일치 해야 하는 일부 외부 인증 서비스의 보안 제약 조건을 기반으로 합니다. (각 외부 인증 서비스에 대해이 단계는 크게 달라질 수;이 코드는 필요한 각 외부 인증 서비스 및 이러한 설정을 구성 하는 방법에 대 한 설명서를 참조 해야 합니다.) 참조를 테스트이 환경에 대 한 FQDN을 사용 하려면 IIS Express를 구성 하는 경우는 [정규화 된 도메인 이름을 사용 하 여 IIS Express 구성](#FQDN) 이 연습 뒷부분의 섹션입니다.


<a id="SAMPLE"></a>
## <a name="creating-a-sample-web-application"></a>샘플 웹 응용 프로그램 만들기

다음 단계를 안내 합니다 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 샘플 응용 프로그램 만들기 및 각이 연습의 뒷부분에서 외부 인증 서비스에 대 한이 샘플 응용 프로그램을 사용 합니다.

Visual Studio 2013 선택 시작 **새 프로젝트** 시작 페이지에서. 또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.

[![](external-authentication-services/_static/image6.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image5.png)

경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 선택 **설치 됨** **템플릿** 확장 **Visual C#**합니다. 아래 **Visual C#**선택, **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET 웹 응용 프로그램**합니다. 프로젝트에 대 한 이름을 입력 하 고 클릭 **확인**합니다.

[![](external-authentication-services/_static/image8.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image7.png)

경우는 **새 ASP.NET 프로젝트** 표시, select는 **SPA** 템플릿을 **프로젝트 만들기**합니다.

[![](external-authentication-services/_static/image10.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image9.png)

대기 Visual studio 2013에서 프로젝트를 만듭니다.

[![](external-authentication-services/_static/image12.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image11.png)

Visual Studio 2013 프로젝트 만들기 완료 되 면 열는 *Startup.Auth.cs* 에 있는 파일의 **앱\_시작** 폴더입니다.

[![](external-authentication-services/_static/image14.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image13.png)

프로젝트를 처음 만들 때 외부 인증 서비스가 사용할 수에서 *Startup.Auth.cs* 파일; 허용 위치에 대 한 강조 표시 된 섹션으로, 다음 떠올릴 코드를 보여 줍니다. 외부 인증 서비스 및 ASP.NET 응용 프로그램과 Microsoft 계정, Twitter, Facebook 또는 Google 인증을 사용 하려면 모든 관련 설정:

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

F5 키를 눌러을 빌드하고 웹 응용 프로그램을 디버깅할 때 표시 되는 외부 인증 서비스가 없습니다 정의 된 로그인 화면이 표시 됩니다.

[![](external-authentication-services/_static/image16.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image15.png)

다음 섹션에서는 각 Visual Studio 2013에서 ASP.NET과 제공 하는 외부 인증 서비스를 사용 하는 방법에 설명 합니다.

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>Facebook 인증을 사용 하도록 설정

Facebook을 사용 하 여 인증에 필요한 Facebook 개발자 계정을 만들 수 있습니다 하 고 프로젝트에 작동 하는 데는 응용 프로그램 ID와 Facebook의 비밀 키를 해야 합니다. Facebook 개발자 계정을 만들고 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 정보를 참조 하십시오. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)합니다.

한 번에 받은 응용 프로그램 ID 및 비밀 키 웹 응용 프로그램에 대 한 Facebook 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:

    [![](external-authentication-services/_static/image18.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image17.png)
2. 강조 표시 된 코드 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. 제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄을 주석 표시 한 후 응용 프로그램 ID 및 비밀 키를 추가 합니다. 이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. 웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Facebook 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.

    [![](external-authentication-services/_static/image20.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image19.png)
5. 클릭할 때는 **Facebook** 단추, 브라우저 Facebook 로그인 페이지로 이동 합니다.

    [![](external-authentication-services/_static/image22.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image21.png)
6. Facebook 자격 증명을 입력 하 고를 클릭 한 후 **로그인**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 연관 시킬 프로그램 Facebook 계정:

    [![](external-authentication-services/_static/image24.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image23.png)
7. 사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Facebook 계정에 대 한:

    [![](external-authentication-services/_static/image26.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>Google 인증을 사용 하도록 설정

Google은 단연 가장 쉬운 개발자 계정으로 필요 하지 않거나 다른 외부 인증 서비스와 응용 프로그램 ID 또는 비밀 키와 같은 추가 정보 필요 아니므로 사용할 수 있도록 외부 인증 서비스 해야 합니다.

웹 응용 프로그램에 대 한 Google 인증을 사용 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:

    [![](external-authentication-services/_static/image28.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image27.png)
2. 강조 표시 된 코드 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. 제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄의 주석 처리 제거 후 프로젝트를 다시 컴파일해야 합니다.

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. 웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Google 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.

    [![](external-authentication-services/_static/image30.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image29.png)
5. 클릭는 **Google** 단추 브라우저가 Google 로그인 페이지로 이동 합니다.

    [![](external-authentication-services/_static/image32.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image31.png)
6. Google 자격 증명을 입력 하 고를 클릭 한 후 **로그인**, Google 웹 응용 프로그램 Google 계정에 액세스할 수 있는 권한이 있는지 확인 하 라는 메시지가 나타납니다.

    [![](external-authentication-services/_static/image34.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image33.png)
7. 클릭할 때 **Accept**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 을 Google 계정에 연결 하려는:

    [![](external-authentication-services/_static/image36.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image35.png)
8. 사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Google 계정에 대 한:

    [![](external-authentication-services/_static/image38.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>Microsoft 인증을 사용 하도록 설정

Microsoft 인증에 필요한 개발자 계정을 만들 수 있습니다 및 클라이언트 ID와 클라이언트 암호가 작동 하는 데 필요 합니다. Microsoft 개발자 계정 만들기 및 클라이언트 ID와 클라이언트 암호를 가져오는 방법에 대 한 정보를 참조 하십시오. [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)합니다.

한 번에 받은 소비자 키 및 소비자 암호 웹 응용 프로그램에 대 한 Microsoft 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:

    [![](external-authentication-services/_static/image40.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image39.png)
2. 강조 표시 된 코드 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. 제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄을 주석 표시 한 후 클라이언트 ID와 클라이언트 암호를 추가 합니다. 이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. 웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Microsoft 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.

    [![](external-authentication-services/_static/image42.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image41.png)
5. 클릭할 때는 **Microsoft** 단추, 브라우저 Microsoft 로그인 페이지로 이동 합니다.

    [![](external-authentication-services/_static/image44.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image43.png)
6. Microsoft 자격 증명을 입력 하 고를 클릭 한 후 **로그인**, 웹 응용 프로그램에 Microsoft 계정에 액세스할 수 있는 권한이 있는지 확인 하 라는 메시지가 표시 됩니다.

    [![](external-authentication-services/_static/image46.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image45.png)
7. 클릭할 때 **예**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 을 Microsoft 계정에 연결 하려는:

    [![](external-authentication-services/_static/image48.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image47.png)
8. 사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Microsoft 계정에 대 한:

    [![](external-authentication-services/_static/image50.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>Twitter 인증 사용

Twitter 인증에 필요한 개발자 계정을 만들 수 있습니다 및 소비자 키 및 소비자 암호 작동 하는 데 필요 합니다. Twitter 개발자 계정을 만들고 소비자 키 및 소비자 암호를 가져오는 방법에 대 한 정보를 참조 하십시오. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)합니다.

한 번에 받은 소비자 키 및 소비자 암호 웹 응용 프로그램에 대 한 Twitter 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:

    [![](external-authentication-services/_static/image52.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image51.png)
2. 강조 표시 된 코드 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. 제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄을 주석 표시 한 후 소비자 키 및 소비자 암호를 추가 합니다. 이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. 웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Twitter 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.

    [![](external-authentication-services/_static/image54.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image53.png)
5. 클릭할 때는 **Twitter** 단추, 브라우저 Twitter 로그인 페이지로 이동 합니다.

    [![](external-authentication-services/_static/image56.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image55.png)
6. Twitter 자격 증명을 입력 하 고를 클릭 한 후 **Authorize 앱**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 연관 시킬 Twitter 계정:

    [![](external-authentication-services/_static/image58.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image57.png)
7. 사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Twitter 계정에 대 한:

    [![](external-authentication-services/_static/image60.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>추가 정보

OAuth 및 OpenID를 사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 다음 Url을 참조 하십시오.

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>외부 인증 서비스를 결합합니다.

유연성을 높이기 위해 동시에 여러 외부 인증 서비스를 정의할 수 있습니다-이렇게 하면 웹 응용 프로그램의 사용자가 활성화 된 외부 인증 서비스가 중 어디에서 든 계정을 사용 하도록 합니다.

[![](external-authentication-services/_static/image62.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configuring-iis-express-to-use-a-fully-qualified-domain-name"></a>정규화 된 도메인 이름을 사용 하 여 IIS Express를 구성 합니다.

일부 외부 인증 공급자와 같은 HTTP 주소를 사용 하 여 응용 프로그램 테스트를 지원 하지 않는 `http://localhost:port/`합니다. 이 문제를 해결 하려면 정적 정규화 된 도메인 이름 (FQDN) 매핑 호스트 파일을 추가한 테스트 하 고 디버깅에 대 한 FQDN을 사용 하려면 Visual Studio 2013에서 프로젝트 옵션을 구성 합니다. 이렇게 하려면 다음 단계를 사용 합니다.

- 호스트 파일 매핑 정적 FQDN을 추가 합니다.

    1. 창에서 관리자 권한 명령 프롬프트를 엽니다.
    2. 다음 명령을 입력합니다.

        <kbd>메모장 %WinDir%\system32\drivers\etc\hosts</kbd>
    3. 호스트 파일에 다음과 같은 항목을 추가 합니다.

        <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
    4. 저장 하 고 호스트 파일을 닫습니다.
- FQDN을 사용 하도록 Visual Studio 프로젝트를 구성 합니다.

    1. 프로젝트를 Visual Studio 2013에서 연 클릭는 **프로젝트** 메뉴에서 다음 프로젝트의 속성을 선택 하 고 있습니다. 예를 들어, 선택할 수 **WebApplication1 속성**합니다.
    2. 선택 된 **웹** 탭 합니다.
    3. 에 대 한 FQDN을 입력에서 **프로젝트 Url**합니다. 예를 들어 입력 <kbd>http://www.wingtiptoys.com</kbd> 호스트 파일에 추가 되는 FQDN 매핑은 복제본이 있는 경우.
- IIS Express 응용 프로그램에 대 한 FQDN을 사용 하도록 구성 합니다.

    1. 창에서 관리자 권한 명령 프롬프트를 엽니다.
    2. IIS Express 폴더에 변경 하려면 다음 명령을 입력 합니다.

        <kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. 응용 프로그램에 FQDN을 추가 하려면 다음 명령을 입력 합니다.

        <kbd>appcmd.exe 설정 구성-section:system.applicationHost/sites / +&quot;[이름 = 'WebApplication1'].bindings. [ 프로토콜 bindingInformation'http ', = ='*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd>

 여기서 **WebApplication1** 프로젝트의 이름 및 **bindingInformation** 테스트에 사용할 포트 번호 및 FQDN을 포함 합니다.

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법

Microsoft 인증에 대 한 Windows Live에 응용 프로그램을 연결 하는 것은 간단 합니다. Windows Live에 응용 프로그램을 아직 연결 하지 않은 경우 다음 단계를 사용할 수 있습니다.

1. 찾아 [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) 고 Microsoft 계정 이름 및 메시지가 표시 되 면 암호를 입력 한 다음 클릭 **로그인**:

    [![](external-authentication-services/_static/image64.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image63.png)
2. 이름 및 메시지가 표시 되 면 응용 프로그램의 언어를 입력 한 다음 클릭 **동의**:

    [![](external-authentication-services/_static/image66.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image65.png)
3. 에 **API 설정** 응용 프로그램 페이지에서 응용 프로그램 및 복사에 대 한 리디렉션 도메인을 입력 합니다.는 **클라이언트 ID** 및 **클라이언트 암호** 프로젝트에 대 한 다음 클릭 **저장**:

    [![](external-authentication-services/_static/image68.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image67.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>로컬 등록을 사용 하지 않도록 선택 사항:

현재 ASP.NET 로컬 등록 기능 자동된 프로그램 (bot) 계정; 멤버를 만드는 하는 것을 금지 하지 않습니다. 예를 들어 봇 방지 및 유효성 검사와 같은 기술을 사용 하 여 [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)합니다. 이 인해 로그인 페이지에 로컬 로그인 폼과 등록 링크를 제거 해야 합니다. 이 위해 엽니다는  *\_Login.cshtml* 프로젝트에서 페이지 한 다음 로컬 로그인 패널 및 등록 링크에 대 한 줄을 설명 합니다. 다음 코드 예제와 같은 결과 페이지와 같은 모습:

[!code-html[Main](external-authentication-services/samples/sample10.html)]

로컬 로그인 패널과 등록 링크가 비활성화 된 후 로그인 페이지에는 설정한 상태 여야 하는 외부 인증 공급자만 표시 됩니다.

[![](external-authentication-services/_static/image70.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image69.png)
