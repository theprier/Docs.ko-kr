---
uid: web-api/overview/security/external-authentication-services
title: ASP.NET Web API 사용 하 여 외부 인증 서비스 (C#) | Microsoft Docs
author: rmcmurray
description: 외부 인증 서비스를 사용 하 여 ASP.NET Web API에 설명 합니다.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: de9b64e6c582059ec66ab352f60773f50af7b1ff
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667858"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>ASP.NET Web API 사용 하 여 외부 인증 서비스 (C#)

Visual Studio 2017 및 ASP.NET 4.7.2에 대 한 보안 옵션을 확장 [단일 페이지 응용 프로그램](../../../single-page-application/index.md) (SPA) 및 [Web API](../../index.md) 몇 가지를 포함 하는 외부 인증 서비스와 통합 하는 서비스 OAuth/OpenID 및 소셜 미디어 인증 서비스: Microsoft 계정, Twitter, Facebook 및 Google 합니다.  

### <a name="in-this-walkthrough"></a>이 연습

- [외부 인증 서비스를 사용 하 여](#USING)
- [샘플 웹 응용 프로그램 만들기](#SAMPLE)
- [Facebook 인증을 사용 하도록 설정](#FACEBOOK)
- [Google 인증을 사용 하도록 설정](#GOOGLE)
- [Microsoft 인증을 사용 하도록 설정](#MICROSOFT)
- [Twitter 인증을 사용 하도록 설정](#TWITTER)
- [추가 정보](#MOREINFO)

    - [외부 인증 서비스를 결합합니다.](#COMBINE)
    - [정규화 된 도메인 이름을 사용 하도록 IIS Express 구성](#FQDN)
    - [Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법](#OBTAIN)
    - [선택 사항: 로컬 등록을 사용 하지 않도록 설정](#DISABLE)

### <a name="prerequisites"></a>전제 조건

이 연습의 예제를 따르려면 다음 조건이 충족 해야 합니다.

- Visual Studio 2017
- 응용 프로그램 식별자 및 다음과 같은 소셜 미디어 인증 서비스 중 하나에 대 한 비밀 키를 사용 하 여 개발자 계정:

  - Microsoft 계정 ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))
  - Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))
  - Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))
  - Google ([https://developers.google.com/](https://developers.google.com))

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>외부 인증 서비스를 사용 하 여

현재 개발을 위해 웹 개발자가 도움말을 사용할 수 있는 외부 인증 서비스의 새 웹 응용 프로그램을 만들 때 시간입니다. 웹 사용자를 일반적으로 여러 기존 계정이 있는 인기 있는 웹 서비스 및 소셜 미디어 웹 사이트에 대 한 따라서 외부 웹 서비스 또는 소셜 미디어 웹 사이트에서 인증 서비스는 웹 응용 프로그램 구현에 저장할 때 개발에 소요 된 인증 구현을 만들기. 외부 인증 서비스를 사용 하 여 웹 응용 프로그램에 대해 다른 계정을 만들어야 하는 것과 및 다른 사용자 이름 및 암호를 기억할 필요가에서 최종 사용자를 저장 합니다.

과거에는 개발자가 두 가지 선택 했습니다: 자체 인증 구현을 만들거나 응용 프로그램에 외부 인증 서비스를 통합 하는 방법을 알아봅니다. 가장 기본적인 수준에서 다음 다이어그램은 외부 인증 서비스를 사용 하도록 구성 된 웹 응용 프로그램에서 정보를 요청 하는 사용자 에이전트 (웹 브라우저)에 대 한 간단한 요청 흐름을 보여 줍니다.

[![](external-authentication-services/_static/image2.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image1.png)

위의 다이어그램에 사용자 에이전트 (또는이 예제에서 웹 브라우저)는 외부 인증 서비스에 웹 브라우저를 리디렉션하는 웹 응용 프로그램에 요청을 만듭니다. 사용자 에이전트 외부 인증 서비스에 해당 자격 증명을 전송 하 고 외부 인증 서비스 형태의 사용 하 여 원래 웹 응용 프로그램에 사용자 에이전트를 리디렉션하는 사용자 에이전트에 성공적으로 인증 하는 경우는 토큰을 사용자 에이전트에서 웹 응용 프로그램에 보냅니다. 웹 응용 프로그램 토큰을 사용 하 여 외부 인증 서비스에서 사용자 에이전트를 성공적으로 인증 된 고 웹 응용 프로그램 사용자 에이전트에 대 한 자세한 정보를 수집 하려면 토큰을 사용할 수 있는지 확인 합니다. 응용 프로그램이 완료 되 면 사용자 에이전트의 정보를 처리 하는, 웹 응용 프로그램은 반환 권한 부여 설정에 따라 사용자 에이전트에 대 한 적절 한 응답입니다.

이 두 번째 예제에서는 사용자 에이전트는 웹 응용 프로그램 및 외부 권한 부여 서버를 사용 하 여 협상 하 고 사용자에 대 한 추가 정보를 검색 하려면 외부 권한 부여 서버를 사용 하 여 추가 통신을 수행 하는 웹 응용 프로그램 에이전트:

[![](external-authentication-services/_static/image4.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image3.png)

Visual Studio 2017 및 ASP.NET 4.7.2 쉽게 외부 인증 서비스와의 통합 개발자를 위한 다음과 같은 인증 서비스에 대 한 기본 제공 통합을 제공 하 여:

- Facebook
- Google
- Microsoft 계정 (Windows Live ID 계정)
- Twitter

이 연습의 예제에서는 Visual Studio 2017을 사용 하 여 제공 되는 새 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 각 지원 되는 외부 인증 서비스를 구성 하는 방법을 보여 줍니다.

> [!NOTE]
> 필요한 경우 외부 인증 서비스에 대 한 설정에 FQDN을 추가 해야 합니다. 이 요구 사항은 클라이언트에서 사용 되는 FQDN과 일치 하는 응용 프로그램 설정에 FQDN을 필요로 하는 일부 외부 인증 서비스에 대 한 보안 제약 조건을 기반으로 합니다. (이 단계는 각 외부 인증 서비스에 대해 크게 달라 집니다; 각 외부 인증 서비스가 필요한 경우 참조 하 고 이러한 설정을 구성 하는 방법에 대 한 설명서를 참조 해야 합니다) 테스트이 환경에 대 한 FQDN을 사용 하려면 IIS Express를 구성 하는 경우는 [정규화 된 도메인 이름을 사용 하도록 IIS Express 구성](#FQDN) 이 연습의 뒷부분에서 섹션입니다.


<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>샘플 웹 응용 프로그램 만들기

다음 단계를 안내 합니다 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 샘플 응용 프로그램 만들기 및이 샘플 응용 프로그램을 사용 하 여이 연습의 뒷부분에서 외부 인증 서비스 각각에 대해 됩니다.

Visual Studio 2017을 시작 하 고 선택 **새 프로젝트** 시작 페이지에서. 또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 선택 **설치 됨** 확장 **시각적 C#** . 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 합니다. 프로젝트에 대 한 이름을 입력 하 고 클릭 **확인**합니다.

[![](external-authentication-services/_static/image71.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image71.png)

경우는 **새 ASP.NET 프로젝트** 표시를 선택 합니다 **단일 페이지 응용 프로그램** 템플릿과 클릭 **프로젝트 만들기**합니다.

[![](external-authentication-services/_static/image72.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image72.png)

대기 Visual studio 2017에서 프로젝트를 만듭니다.

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

Visual Studio 2017 프로젝트 만들기 완료 되 면 엽니다는 *Startup.Auth.cs* 에 있는 파일을 **앱\_시작** 폴더.

프로젝트를 처음 만들 때에 설정 된 외부 인증 서비스가 하나도 *Startup.Auth.cs* 파일 위치에 대 한 강조 표시 된 섹션을 사용 하 여 허용, 다음과 비슷한 코드를 보여 줍니다 외부 인증 서비스와 ASP.NET 응용 프로그램을 사용 하 여 Microsoft 계정, Twitter, Facebook 또는 Google 인증을 사용 하려면 모든 관련 설정 합니다.

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

빌드 및 웹 응용 프로그램을 디버그 하려면 f5 키를 누르면 표시 되는 외부 인증 서비스가 없습니다 정의 된 로그인 화면을 표시 합니다.

[![](external-authentication-services/_static/image73.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image73.png)

다음 섹션에서는 각 Visual Studio 2017의 ASP.NET을 사용 하 여 제공 되는 외부 인증 서비스를 사용 하도록 설정 하는 방법을 배웁니다.

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>Facebook 인증을 사용 하도록 설정

Facebook을 사용 하 여 인증을 사용 하면 Facebook 개발자 계정을 만들려면 해야 및 프로젝트에는 응용 프로그램 ID 및 비밀 키 Facebook에서 작동 하는 데 필요 합니다. Facebook 개발자 계정을 만들고 해당 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 자세한 내용은 [ https://go.microsoft.com/fwlink/?LinkID=252166 ](https://go.microsoft.com/fwlink/?LinkID=252166)합니다.

한 번 가져온 응용 프로그램 ID 및 비밀 키, 웹 응용 프로그램에 대해 Facebook 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 Visual Studio 2017에서 연 엽니다는 *Startup.Auth.cs* 파일입니다.

2. Facebook 인증 섹션을 코드를 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. 제거 된 &quot; // &quot; 문자 코드의 강조 표시 된 줄의 주석도 제거 한 후에 응용 프로그램 ID 및 비밀 키를 추가 합니다. 이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 여는 외부 인증 서비스와 Facebook을 정의한 표시 됩니다.

    [![](external-authentication-services/_static/image74.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image74.png)
5. 클릭할 때 합니다 **Facebook** 단추를 브라우저 Facebook 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image22.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image21.png)
6. Facebook 자격 증명을 입력 하 고 클릭 한 후 **로그인**, 웹 브라우저를 웹 응용 프로그램으로 다시 리디렉션됩니다는 묻습니다 합니다 **사용자 이름** 연결 하려는 프로그램 Facebook 계정:

    [![](external-authentication-services/_static/image24.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image23.png)
7. 사용자 이름을 입력 하 고 클릭 한 후는 **등록할** 단추를 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Facebook 계정에 대 한 합니다.

    [![](external-authentication-services/_static/image26.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>Google 인증을 사용 하도록 설정

Google을 사용 하 여 인증에 필요한 Google 개발자 계정으로 만들 수 있습니다 및 프로젝트에 응용 프로그램 ID 및 Google에서 비밀 키를 작동 하는 데 필요 합니다. Google 개발자 계정을 만들고 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 자세한 내용은 [ https://developers.google.com ](https://developers.google.com)합니다.


웹 응용 프로그램에 대해 Google 인증을 사용 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 Visual Studio 2017에서 연 엽니다는 *Startup.Auth.cs* 파일입니다.

2. Google 인증 섹션을 코드를 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. 제거 된 &quot; // &quot; 문자 코드의 강조 표시 된 줄의 주석도 제거 한 후에 응용 프로그램 ID 및 비밀 키를 추가 합니다. 이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 여는 외부 인증 서비스와 Google을 정의한 표시 됩니다.

    [![](external-authentication-services/_static/image75.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image75.png)
5. 클릭할 때 합니다 **Google** 단추 브라우저가 Google 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image32.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image31.png)
6. Google 자격 증명을 입력 하 고 클릭 **로그인**, Google 웹 응용 프로그램에 Google 계정에 액세스할 권한이 있는지 확인 하 라는 메시지가 나타납니다.

    [![](external-authentication-services/_static/image34.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image33.png)
7. 클릭 하면 **Accept**, 웹 브라우저를 웹 응용 프로그램으로 다시 리디렉션됩니다는 묻습니다 합니다 **사용자 이름** Google 계정을 사용 하 여 연결 하려는:

    [![](external-authentication-services/_static/image36.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image35.png)
8. 사용자 이름을 입력 하 고 클릭 한 후 합니다 **등록할** 단추를 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Google 계정:

    [![](external-authentication-services/_static/image38.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>Microsoft 인증을 사용 하도록 설정

Microsoft 인증 개발자 계정으로 작성 해야 하 고 클라이언트 ID 및 클라이언트 비밀을 작동 하는 데 필요 합니다. Microsoft 개발자 계정 만들기 및 클라이언트 ID 및 클라이언트 암호 가져오기에 대 한 자세한 내용은 [ https://go.microsoft.com/fwlink/?LinkID=144070 ](https://go.microsoft.com/fwlink/?LinkID=144070)합니다.

한 번 가져온 프로그램 소비자 키 및 소비자 암호 웹 응용 프로그램에 대 한 Microsoft 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 Visual Studio 2017에서 연 엽니다는 *Startup.Auth.cs* 파일입니다.

2. Microsoft 인증 섹션을 코드를 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. 제거 된 &quot; // &quot; 문자 코드의 강조 표시 된 줄의 주석도 제거를 클라이언트 ID 및 클라이언트 암호를 추가 합니다. 이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열려고 하는 경우 Microsoft는 외부 인증 서비스와 정의한는 표시 됩니다.

    [![](external-authentication-services/_static/image42.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image41.png)
5. 클릭할 때 합니다 **Microsoft** 단추 브라우저가 Microsoft 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image44.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image43.png)
6. Microsoft 자격 증명을 입력 하 고 클릭 **로그인**, 웹 응용 프로그램에 Microsoft 계정에 액세스할 권한이 있는지 확인 하 라는 메시지가 됩니다.

    [![](external-authentication-services/_static/image46.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image45.png)
7. 클릭 하면 **예**, 웹 브라우저를 웹 응용 프로그램으로 다시 리디렉션됩니다는 묻습니다 합니다 **사용자 이름** Microsoft 계정과 연결 하려는:

    [![](external-authentication-services/_static/image48.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image47.png)
8. 사용자 이름을 입력 하 고 클릭 한 후 합니다 **등록할** 단추를 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Microsoft 계정:

    [![](external-authentication-services/_static/image50.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>Twitter 인증을 사용 하도록 설정

Twitter 인증을 사용 하면 개발자 계정을 만들려면 해야 및 소비자 키 및 소비자 암호를 작동 하는 데 필요 합니다. Twitter 개발자 계정을 만들고 프로그램 소비자 키 및 소비자 암호를 가져오는 방법에 대 한 자세한 내용은 [ https://go.microsoft.com/fwlink/?LinkID=252166 ](https://go.microsoft.com/fwlink/?LinkID=252166)합니다.

한 번 가져온 프로그램 소비자 키 및 소비자 암호 웹 응용 프로그램에 대해 Twitter 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. 프로젝트를 Visual Studio 2017에서 연 엽니다는 *Startup.Auth.cs* 파일입니다.

2. Twitter 인증 섹션을 코드를 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. 제거 된 &quot; // &quot; 문자 코드의 강조 표시 된 줄의 주석도 제거 한 후에 소비자 키 및 소비자 암호를 추가 합니다. 이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열기 위해 Twitter 외부 인증 서비스를 정의 된는 표시 됩니다.

    [![](external-authentication-services/_static/image54.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image53.png)
5. 클릭할 때 합니다 **Twitter** 단추를 브라우저 Twitter 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image56.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image55.png)
6. Twitter 자격 증명을 입력 하 고 클릭 **앱 권한 부여**, 웹 브라우저를 웹 응용 프로그램으로 다시 리디렉션됩니다는 묻습니다 합니다 **사용자 이름** 연결 하려는 Twitter 계정:

    [![](external-authentication-services/_static/image58.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image57.png)
7. 사용자 이름을 입력 하 고 클릭 한 후 합니다 **등록할** 단추를 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Twitter 계정에 대해:

    [![](external-authentication-services/_static/image60.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>추가 정보

OAuth 및 OpenID를 사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 다음 Url을 참조 하세요.

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>외부 인증 서비스를 결합합니다.

유연성을 높이기 위해 동시에 여러 외부 인증 서비스를 정의할 수 있습니다-이렇게 하면 웹 응용 프로그램의 사용 가능한 외부 인증 서비스의 계정을 사용 합니다.

[![](external-authentication-services/_static/image62.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>정규화 된 도메인 이름을 사용 하도록 IIS Express 구성

일부 외부 인증 공급자와 같은 HTTP 주소를 사용 하 여 응용 프로그램 테스트를 지원 하지 않습니다 `http://localhost:port/`합니다. 이 문제를 해결 하려면 정적 정규화 된 도메인 이름 (FQDN) 매핑을 호스트 파일에 추가 테스트 하 고 디버깅 하는 것에 대 한 FQDN을 사용 하도록 Visual Studio 2017에서 프로젝트 옵션을 구성 합니다. 이렇게 하려면 다음 단계를 사용 합니다.

- 호스트 파일 매핑 정적 FQDN을 추가 합니다.

  1. Windows에서 관리자 권한 명령 프롬프트를 엽니다.
  2. 다음 명령을 입력합니다.

      <kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd>
  3. 호스트 파일에 다음과 같은 항목을 추가 합니다.

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. 저장 하 고 호스트 파일을 닫습니다.

- FQDN을 사용 하도록 Visual Studio 프로젝트를 구성 합니다.

  1. 프로젝트가 Visual Studio 2017에서 열려 있는 경우 클릭 합니다 **프로젝트** 메뉴를 선택한 다음 프로젝트의 속성입니다. 예를 들어, 선택할 수 있습니다 **WebApplication1 속성**합니다.
  2. 선택 된 **웹** 탭 합니다.
  3. 에 대 한 FQDN을 입력 합니다 <strong>프로젝트 Url</strong>합니다. 예를 들어 입력 <kbd> <http://www.wingtiptoys.com> </kbd> 호스트 파일에 추가 하는 FQDN 매핑이 있는 경우.

- 응용 프로그램에 대 한 FQDN을 사용 하도록 IIS Express를 구성 합니다.

    1. Windows에서 관리자 권한 명령 프롬프트를 엽니다.
    2. IIS Express 폴더로 변경 하려면 다음 명령을 입력 합니다.

        <kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. 응용 프로그램에 FQDN을 추가 하려면 다음 명령을 입력 합니다.

        <kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd>

  여기서 **WebApplication1** 프로젝트의 이름 및 **bindingInformation** 테스트에 사용할 포트 번호 및 FQDN을 포함 합니다.

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법

Microsoft 인증을 위해 Windows Live에 응용 프로그램을 연결 하는 것은 간단 합니다. 이미 Windows Live에 응용 프로그램을 연결 하지 않은 경우 다음 단계를 사용할 수 있습니다.

1. 이동할 [ https://go.microsoft.com/fwlink/?LinkID=144070 ](https://go.microsoft.com/fwlink/?LinkID=144070) 및 Microsoft 계정 이름 및 메시지가 표시 되 면 암호를 입력 한 다음 클릭 **로그인**:

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. 선택 **앱 추가** 메시지가 표시 되 면 응용 프로그램의 이름을 입력 하 고 클릭 하 고 **만들기**:

    [![](external-authentication-services/_static/image79.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image79.png)
3. 응용 프로그램 선택 **이름을** 및 해당 응용 프로그램 속성 페이지가 나타납니다.

4. 응용 프로그램 리디렉션 도메인을 입력 합니다. 복사 합니다 **응용 프로그램 ID** 고 **응용 프로그램 비밀**를 선택 **암호 생성**합니다. 표시 되는 암호를 복사 합니다. 응용 프로그램 ID 및 암호는 클라이언트 ID 및 클라이언트 암호입니다. 선택 **Ok** 차례로 **저장**합니다.

    [![](external-authentication-services/_static/image77.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>선택 사항: 로컬 등록을 사용 하지 않도록 설정

현재 ASP.NET 로컬 등록 기능을 사용 해도 자동화 프로그램 (봇)에서 멤버 계정 만들기 예를 들어 봇 방지 및 유효성 검사와 같은 기술을 사용 하 여 [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)합니다. 이 인해 로그인 페이지에 로컬 로그인 폼 및 등록 링크를 제거 해야 합니다. 이렇게 하려면 엽니다는  *\_Login.cshtml* 프로젝트에서 페이지 및 로컬 로그인 패널에서 등록 링크를 한 줄을 주석입니다. 결과 페이지는 다음 코드 샘플과 같아야 합니다.

[!code-html[Main](external-authentication-services/samples/sample10.html)]

로컬 로그인 패널 및 등록 링크를 비활성화 된 후 로그인 페이지에는 설정한 외부 인증 공급자만 표시 됩니다.

[![](external-authentication-services/_static/image70.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image69.png)
