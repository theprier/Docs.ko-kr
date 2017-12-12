---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: "ASP.NET 웹 페이지-시작 소개 | Microsoft Docs"
author: tfitzmac
description: "WebMatrix 더 이상 권장 통합된 개발 환경에 대 한 ASP.NET 웹 페이지입니다. Visual Studio 또는 Visual Studio 코드를 사용 합니다. 이 설명서는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 615ddc31d0d857e5bf9a7f372b7efcf67d185905
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introducing-aspnet-web-pages---getting-started"></a>ASP.NET 웹 페이지-시작 소개
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > 
> > WebMatrix 더 이상 권장 통합된 개발 환경에 대 한 ASP.NET 웹 페이지입니다. 사용 하 여 [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) 또는 [Visual Studio Code](https://code.visualstudio.com/)합니다.
> 
> 
> 이 지침 하 고 응용 프로그램 제공 ASP.NET 웹 페이지 (2 이상 버전)의 개요 및 Razor 구문, 동적 웹 사이트를 만들기 위한 경량 프레임 워크입니다. 또한 WebMatrix, 페이지 및 사이트를 만들기 위한 도구를 소개 합니다.
> 
> **수준**: ASP.NET 웹 페이지를 처음 사용 합니다.  
> **가정 기술**: HTML, 기본 css 스타일 시트 ().
> 
> 학습 내용 집합의 첫 번째 자습서:
> 
> - ASP.NET 웹 페이지 기술은 이며이 대 한 합니다.
> - WebMatrix의는입니다.
> - 모든 항목을 설치 하는 방법입니다.
> - WebMatrix를 사용 하 여 웹 사이트를 만드는 방법.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - Microsoft 웹 플랫폼 설치 관리자입니다.
> - WebMatrix 합니다.
> - *.cshtml* 페이지
>   
> 
> 원래 Mike 서가이 자습서를 썼습니다. Tom FitzMacken Microsoft WebMatrix 3에 대 한 업데이트 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3


## <a name="what-should-you-know"></a>해야 알고 있습니까?

에 익숙할 것으로 가정 합니다.

- **HTML**합니다. 없음 심층 전문 지식이 필요 합니다. HTML, 설명 하지 않겠습니다에서는 또한 사용 하지 마십시오 복잡 한 것입니다. 여기서 한다고 생각 유용 HTML 자습서의 링크를 제공 합니다.
- **Css 스타일 시트 ()**합니다. 와 동일 html 합니다.
- **Basic 데이터베이스 아이디어**합니다. 스프레드시트 데이터에 사용 되 고 정렬 되었으며 전문 지식 수준을 아닌 데이터를 필터링 하는 경우 일반적으로 있으리라이 자습서 집합에 대 한 합니다.

또한 기본 프로그래밍 학습에 관심이으로 가정 합니다. ASP.NET 웹 페이지 라는 C# 프로그래밍 언어를 사용 합니다. 프로그래밍에서는 방금 것에 관심 있는 배경 필요가 없습니다. 계속 하기 전에 웹 페이지에서 모든 JavaScript 작성 한, 충분 한 배경 했습니다.

프로그래밍에 익숙한 경우 수 되어이 자습서에서는 처음 설정 하는 참고 새 프로그래머 속도 제공 하는 동안 느린 이동 합니다. 첫 번째 몇 가지 자습서 지나서 대로, 하지만 설명 하기 위해 작은 기본 프로그래밍 있고이 작업에 더 빠르게 클립을 따라 이동 합니다.

## <a name="what-do-you-need"></a>어떻게 해야 합니까?

필요한 사항은 다음과 같습니다.

- Windows 8, Windows 7, Windows Server 2008 또는 Windows Server 2012를 실행 하는 컴퓨터.
- 라이브 인터넷 연결입니다.
- 관리자 권한 (설치 과정에 필요).

## <a name="what-is-aspnet-web-pages"></a>ASP.NET 웹 페이지는 무엇입니까?

ASP.NET 웹 페이지에는 동적 웹 페이지를 만드는 데 사용할 수 있는 프레임 워크입니다. 간단한 HTML 웹 페이지 정적입니다. 페이지에는 HTML 태그를 고정된 의해 그 내용이 결정 됩니다. ASP.NET 웹 페이지를 만드는 것과 같은 동적 페이지에는 코드를 사용 하 여 즉시 페이지 콘텐츠를 만들 수 있습니다.

동적 페이지를 사용 하 여 모든 종류의 작업을 수행할 수 있습니다. 폼을 사용 하 여 입력 메시지를 표시 하 고 페이지에 표시 하거나 어떻게 나타나는지를 변경할 수 있습니다. 사용자 정보를 가져올 하 고, 데이터베이스에 저장 하 고, 그런 다음 나중에 나열 수 있습니다. 사이트에서 전자 메일을 보낼 수 있습니다. 웹 (예: 매핑 서비스)에서 다른 서비스와 상호 작용할 수 있으며 해당 소스에서 정보를 통합 하는 페이지를 생성할 수 있습니다.

## <a name="what-is-webmatrix"></a>WebMatrix는 무엇입니까?

WebMatrix는 웹 페이지 편집기, 데이터베이스 유틸리티, 페이지 및 웹 사이트를 인터넷에 게시 하기 위한 기능 테스트용 웹 서버를 통합 하는 도구입니다. WebMatrix는 무료 이며 쉽게 설치 하 고 사용 하기 쉽습니다. (또한 작동 셨 겠지만 HTML 페이지에 대 한 것은 물론 PHP와 같은 다른 기술 합니다.)

실제로 하지 않으면 *가* WebMatrix ASP.NET 웹 페이지를 사용 하 합니다. 편집기에서 텍스트를 사용 하 여 페이지를 만들 예를 들어 있고 액세스할 수 있는 웹 서버를 사용 하 여 페이지를 테스트 합니다. 그러나 WebMatrix를 사용 하면 모든,이 자습서 전체에서 WebMatrix를 사용 합니다.

## <a name="about-these-tutorials"></a>이 자습서에 대 한

이 자습서 집합은 ASP.NET 웹 페이지를 사용 하는 방법에 소개 합니다. 이 소개 용 자습서 집합의 총 9 자습서 있습니다. 그의 real, 전문가 수준의 웹 사이트를 만드는 데 ASP.NET 웹 페이지 초보자에서 이동 하는 자습서 집합 시리즈의 일부입니다.

이 첫 번째 자습서에서 ASP.NET 웹 페이지를 사용 하는 방법의 기본 사항을 보여 주는 중점적을 설정 합니다. 완료 되 면 여기서이 이와 종료 하는 웹 페이지 및 탐색 좀 더 깊이 선택 하는 추가 자습서 집합으로 작업할 수 있습니다.

의도 한 대로, 이제 쉽게에서 자세한 설명을 비롯 되었습니다. 선택 하 고 문제가 알아보겠습니다 때마다이 자습서 집합에 대 한에서는 항상 한다고 생각 하는 방법을 이해 하기 쉽습니다. 이후 자습서 더 자세하게 검토할 집합과 보다 효율적인 또는 보다 유연한 방법을 (도 더 재미 있게)를 표시 합니다. 하지만 해당 자습서 먼저 기본 사항을 이해 해야 합니다.

처음 자습서 집합 ASP.NET 웹 페이지의 이러한 기능에 설명 합니다.

- 소개 및 가져오는 모든 항목이 설치 되어 있습니다. (하는 현재 읽고 있는 자습서입니다.)
- ASP.NET 웹 페이지 프로그래밍의 기본입니다.
- 데이터베이스를 만드는 중
- 만들기 및 사용자 입력된 폼을 처리 합니다.
- 추가, 업데이트 및 데이터베이스의에서 데이터를 삭제 합니다.

## <a name="what-will-you-create"></a>만들 있습니까?

이 자습서를 설정 하 고 원하는 영화를 나열할 수 있는 웹 사이트를 중심으로 이후의 조건 키를 누릅니다. 영화를 입력 하 고 편집을 나열 하는 작업을 할 수 있습니다. 다음은 자습서이 집합에서 페이지가입니다. 첫 번째 만들게 페이지 나열 영화를 보여 줍니다.

![동영상 목록을 보여 주는 완료 했습니다 만든 동영상 앱](getting-started/_static/image1.png)

및 새 동영상 정보를 사이트에 추가할 수 있는 페이지가 표시 되어 있습니다.

![동영상 추가 페이지를 보여 주는 완성된 동영상 앱](getting-started/_static/image2.png)

이 후속 자습서 집합 빌드 설정 및 사진 업로드, 로그인 사용자 수 있도록, 전자 메일을 보내고 소셜 미디어와 통합 같은 다른 기능을 추가 합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 응용 프로그램 참조

실시간 웹 앱으로 실행 하는 완료 된 사이트를 참조 하 시겠습니까? 다음 단추 클릭 하 여 Azure 계정에 완전 한 버전의 앱을 배포할 수 있습니다.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션:

- [무료 Azure 계정을 개설](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.

## <a name="installing-everything"></a>설치 하는 모든 항목

Microsoft에서 웹 플랫폼 설치 관리자를 사용 하 여 모든 항목을 설치할 수 있습니다. 실제로 설치 관리자를 설치 하 고를 사용 하 여 다른 모든 요소를 설치 합니다.

이상 있을 수 있는 웹 페이지를 사용 하려면 Windows Server 2008 이상 또는 Windows XP sp3 이상 설치 합니다.

에 [웹 페이지의 페이지](../../../index.md) ASP.NET 웹 사이트의 클릭 **설치**합니다.

![ASP.NET 웹 사이트 보여 주는 &quot;WebMatrix 설치&quot; 단추](getting-started/_static/image3.png)

WebMatrix를 설치 하기 전에 개인정보취급방침 사용 조건에 동의 하 라는 메시지가 표시 됩니다.

![설치를 시작 하는 용어를 허용 합니다.](getting-started/_static/image4.png)

클릭 **실행** 설치를 시작 합니다. (설치 프로그램을 저장 하려면 클릭 **저장** 다음 사용자가 저장 폴더에서 설치 프로그램을 실행 합니다.)

![](getting-started/_static/image5.png)

웹 플랫폼 설치 관리자 나타나고 해당 WebMatrix를 설치 합니다. **설치**를 클릭합니다.

![](getting-started/_static/image6.png)

설치 프로세스에 컴퓨터에 설치으로 파악 하 고 프로세스를 시작 합니다. 정확 하 게 설치에 기능에 따라 프로세스 걸릴 수 있습니다 몇 분에서 몇 분 정도. 선택 **동의** 하려면 사용 조건에 동의 합니다.

## <a name="hello-webmatrix"></a>Hello, WebMatrix

완료 되 면 설치 프로세스는 WebMatrix를 자동으로 시작할 수 있습니다. 그렇지 않은 경우 windows에서에서 **시작** 메뉴에서 **Microsoft WebMatrix**합니다.

처음으로 WebMatrix를 시작할 때 Microsoft 계정으로 Microsoft Azure에 로그인 하 여 제공 됩니다. 에 로그인 하면 Azure 통해 무료 웹 앱을 10 받게 됩니다. 이러한 무료 웹 앱에 앱을 테스트 하는 편리한 방법을 제공 합니다. Azure 계정이 아직 없는 MSDN 구독이 있는 경우 다음을 할 수 있습니다 [MSDN 구독 혜택을 활성화](https://www.windowsazure.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)합니다. 그렇지 않은 경우 몇 분에서에서 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.

이 자습서와 함께 계속 하려면 지금 바로 로그인 필요가 없습니다. 사용자 로그인 하지 않는 이제,는 여전히 경우 나중에 로그인 하는 옵션입니다. 마지막 [항목](publishing.md) 해당 항목을 완료 하려면 로그인 해야 하는 따라서; 시리즈가이 자습서에서는 Azure에 웹 사이트를 배포 하는 방법에 설명 합니다.

Microsoft 계정 또는 select를 사용 하 여 로그인 하거나이 시점에서 **나중** 오른쪽 아래에 있습니다.

![링크를](getting-started/_static/image7.png)

를 시작 하려면 빈 웹 사이트를 만들 하 고 페이지를 추가 합니다. 이 자습서의 뒷부분에서 기본 제공 웹 사이트 템플릿 중 하나을 사용할 수 있습니다.

시작 창에서 클릭 **새로**합니다.

![WebMatrix 시작 화면](getting-started/_static/image8.png)

서식 파일은 미리 작성 된 파일 및 다른 유형의 웹 사이트에 대 한 페이지입니다. 기본적으로 사용할 수 있는 서식 파일의 모든을 보려면 템플릿 갤러리 옵션을 선택 합니다.

![선택 템플릿 갤러리](getting-started/_static/image9.png)

에 **빠른 시작** 창에서 **빈 사이트** 에서 **ASP.NET** 그룹화 하 고 새 사이트 "WebPagesMovies" 이름을 지정 합니다.

![선택 된 빈 사이트 템플릿 사용 하 여 WebMatrix 빠른 시작 창](getting-started/_static/image10.png)

**다음**을 클릭합니다.

Microsoft 계정에 로그인 하면 Azure에서 사이트를 만들 수 있습니다를 제공 됩니다. 기본 이름은 사이트의 이름에 따라 **WebPagesMovies.azurewebsites.net** 제안 됩니다; 그러나 느낌표가이 이름은 Windows Azure에서 제공 하지 않음을 나타냅니다. 간단히 하기 위해 선택 **Skip** 지금은 Azure에서 웹 사이트를 만드는 무시 하도록 합니다. 이 시리즈의 뒷부분에 나오는 azure 사이트를 발표 합니다.

![azure 사이트 만들기](getting-started/_static/image11.png)

WebMatrix를 만들고 해당 사이트:

![에 열어 새 WebPagesMovies 사이트](getting-started/_static/image12.png)

맨 위에 있는 빠른 실행 도구 모음 및가 리본 메뉴 왼쪽 아래에 표시 작업 영역 선택기 작업 간에 전환 하는 위치 (**사이트**, **파일**, **데이터베이스**, **보고서**). 오른쪽 편집기 및 보고서에 대 한 콘텐츠 창이입니다. 및 아래쪽 종종 보게 메시지에 대 한 알림 표시줄입니다.

이 자습서를 진행할 때 WebMatrix 및 해당 기능에 대해 자세히 설명 합니다.

## <a name="creating-a-web-page"></a>웹 페이지 만들기

WebMatrix 및 ASP.NET 웹 페이지를 살펴, 간단한 페이지를 만듭니다.

작업 영역 편집기 도구 모음에서 선택 된 **파일** 작업 영역입니다. 이 작업 영역에는 파일 및 폴더를 사용할 수 있습니다. 왼쪽된 창 사이트의 파일 구조를 표시 합니다. 파일 관련 작업을 표시 하는 리본 바뀝니다.

![WebMatrix에서 파일 작업 영역](getting-started/_static/image13.png)

리본 메뉴에 아래의 화살표를 클릭 합니다. **새로** 클릭 하 고 **새 파일**합니다.

![사용 하는 &quot;새로&quot; 새 파일을 만들려면 리본 메뉴의 명령을](getting-started/_static/image14.png)

WebMatrix에는 파일 형식 목록이 표시 됩니다. 선택 **CSHTML**, 및는 **이름** "HelloWorld"를 입력 합니다. CSHTML 페이지에는 ASP.NET 웹 페이지 페이지가입니다.

![HelloWorld.cshtml 라는 새 CSHTML 페이지 만들기](getting-started/_static/image15.png)

**확인**을 클릭합니다.

WebMatrix 페이지를 만들고이 편집기에서 열립니다.

![WebMatrix 편집기에서 새 HelloWorld 페이지](getting-started/_static/image16.png)

볼 수 있듯이 페이지 대부분 일반 HTML 태그를 다음과 같은 맨 위에 있는 블록을 제외한 포함 되어 있습니다.

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

코드를 추가, 잠시 후에 확인할 수 있습니다.

해당 페이지의 다른 부분 &mdash; 요소 이름, 특성 및 텍스트와 맨 위에 블록이-는 서로 다른 색으로 모든 합니다. 이 라고 *구문 강조 표시*를 보다 쉽게 지우기 모든 항목을 유지 하 고 있습니다. WebMatrix에서 웹 페이지를 사용 하기 쉽게 있는 기능 중 하나입니다.

에 대 한 내용을 추가 `<head>` 및 `<body>` 다음 예제에서와 같은 요소입니다. (원할 경우 방금 다음 블록을 복사 하 수 기존 페이지 전체를이 코드로 바꿉니다.)

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

빠른 실행 도구 모음 또는 **파일** 메뉴를 클릭 하 여 **저장**합니다.

![WebMatrix 빠른 실행 도구 모음에서 저장 단추](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>테스트 페이지

에 **파일** 작업 영역을 마우스 오른쪽 단추로 클릭는 *HelloWorld.cshtml* 페이지 한 다음 클릭 **브라우저에서 시작**합니다.

![WebMatrix 리본에서 [실행] 단추를 사용 하는 페이지를 실행 합니다.](getting-started/_static/image18.png)

WebMatrix는 컴퓨터에 있는 페이지를 테스트 하는 데 사용할 수 있는 기본 제공 웹 서버 (IIS Express)를 시작 합니다. (사용 하지 않으면 WebMatrix에서 IIS Express는 해야 페이지는 웹 서버에 게시 어딘가에 전에 테스트할 수 있습니다.) 페이지 기본 브라우저에 표시 됩니다.

![&quot;Hello World&quot; 브라우저에서 실행 되 고 페이지](getting-started/_static/image19.png)

WebMatrix에서 페이지를 테스트할 때 브라우저의 URL은 다음과 같이 `http://localhost:33651/HelloWorld.cshtml.` 이름 *localhost* 의미 페이지가 컴퓨터에 있는 웹 서버에 의해 반환 되는 로컬 서버를 가리킵니다. 설명한 것 처럼, IIS Express는 페이지를 시작할 때 실행 되는 명명 된 웹 서버 프로그램 WebMatrix에 포함 되어 있습니다.

다음의 숫자 *localhost* (예를 들어 *localhost:33651*) 참조 하는 *포트 번호* 컴퓨터에 있습니다. 이 특정 웹 사이트에 대 한 사용 하 여 IIS Express는 "채널"의 수입니다. 포트 번호는 사이트를 만들고 만든 모든 사이트에 대 한 다른 1024 65536부터 범위에서 임의로 선택 됩니다. (사이트를 테스트할 때 포트 번호는 거의 항상 됩니다 33561 보다 다른 숫자를.) 각 웹 사이트에 대 한 서로 다른 포트를 사용 하 여 IIS Express 유지할 수 직선 통신 중인 사이트입니다.

나중에 게시할 때 사이트에 공용 웹 서버를 더 이상 참조 *localhost* url에서입니다. 이때 표시와 같은 대부분의 일반적인 URL `http://myhostingsite/mywebsite/HelloWorld.cshtml` 어떤 페이지가 또는 합니다. 이 자습서 시리즈의 뒷부분에 나오는 사이트를 게시 하는 방법에 대 한 더 설명 합니다.

## <a name="adding-some-server-side-code"></a>서버 쪽 코드 추가

브라우저를 닫고 WebMatrix에서 페이지로 다시 이동 합니다.

다음 코드 처럼 표시 되도록 코드 블록을 한 줄을 추가 합니다.

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

약간의 Razor 코드입니다. 현재 날짜 및 시간을 가져옵니다 하 고 해당 값에 아마도 명확는 *변수* 라는 `currentDateTime`합니다. 읽게 되는 내용은 다음 자습서에서 Razor 구문에 대 한 합니다.

페이지의 본문에서 후는 `<p>Hello World!</p>` 요소를 다음에 추가 합니다.

[!code-html[Main](getting-started/samples/sample4.html)]

이 코드를 설정 하는 값을 가져옵니다는 `currentDateTime` 변수 맨 위에 있는 페이지의 태그에 삽입 합니다. `@` 문자 페이지에서 ASP.NET 웹 페이지 코드를 표시 합니다.

(WebMatrix 변경 내용을 저장 하면에 대 한 페이지를 실행 하기 전에)의 페이지를 다시 실행 합니다. 이 시간 날짜 및 시간 페이지에 표시 합니다.

![&quot;Hello World&quot; 동적으로 생성 된 시간 표시를 사용 하 여 브라우저에서 실행 되 고 페이지](getting-started/_static/image20.png)

몇 분 정도 후 브라우저에서 페이지를 새로 고 치세요. 날짜 및 시간 디스플레이가 업데이트 됩니다.

브라우저에서 페이지 소스를 확인 합니다. 다음 태그 비슷합니다.

[!code-html[Main](getting-started/samples/sample5.html)]

에 `@{ }` 블록이 없는 합니다. 또한가 표시 된 날짜 및 시간 표시는 실제 문자열 (`1/18/2012 2:49:50 PM` 또는)이 아니라 `@currentDateTime` 에서 제공 되었던 처럼는 *.cshtml* 페이지. 여기서는 페이지를 실행 한 경우 ASP.NET을 처리 하는 모든 코드 (거의이 경우)로 표시 된 변경 사항 `@`합니다. 코드 출력을 생성 하 고 해당 출력의 페이지에 삽입 된 키를 누릅니다.

## <a name="this-is-what-aspnet-web-pages-are-about"></a>이에 대 한 ASP.NET 웹 페이지는

된 ASP.NET 웹 페이지 생성 동적 웹 콘텐츠를 읽을 때 개념은 무엇을 보았을 여기 합니다. 방금 만든 페이지 하기 전에 살펴 보았으며 하는 동일한 HTML 태그를 포함 합니다. 모든 종류의 작업을 수행할 수 있는 코드를 포함할 수도 있습니다. 이 예제에서는 trivial 작업의 현재 날짜와 시간을 가져오는 것입니다. 살펴본 것 처럼 페이지에서 출력을 생성 하는 html 코드 중간에 삽입할 수 있습니다. 다른 사람이 요청 하는 경우는 *.cshtml* ASP.NET 브라우저에서 페이지에 웹 서버에에서 있는 동안 해당 페이지를 처리 합니다. ASP.NET 코드의 출력 (있는 경우)에 삽입 페이지 HTML로 합니다. 코드 처리가 완료 되 면 ASP.NET 결과 페이지를 브라우저에 보냅니다. 브라우저가 현재까지 받는 HTML입니다. 다음 다이어그램은입니다.

![ASP.NET 설명 생성 방법을 HTML 동적으로 개념적 흐름](getting-started/_static/image21.png)

개념은 간단 하지만 여러 흥미로운 작업을 코드로 수행할 수 있으며 여러 가지 흥미로운를 동적으로 추가할 수 HTML 콘텐츠 페이지. 및 ASP.NET *.cshtml* 자체 (JavaScript 및 jQuery 코드) 브라우저에서 실행 되는 코드 페이지, HTML 페이지, 처럼 포함할 수도 있습니다. 이 자습서에서는 및 이후의 조건은에서 이러한 작업을 모두 방법을 알아봅니다.

## <a name="coming-up-next"></a>다음에 나오는

이 시리즈의 다음 자습서에서는 ASP.NET 웹 페이지 프로그래밍 좀 더 살펴볼 있습니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 사이트를 처음부터 만들](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)합니다. 이것은 자습서를 WebMatrix (하지: ASP.NET 웹 페이지)를 사용 하는 방법에 대 한 합니다. 이동에 약간이 자습서에서는 다루지 않습니다 WebMatrix의 추가 기능 중 일부에 대 한 자세한 정보.

>[!div class="step-by-step"]
[다음](intro-to-web-pages-programming.md)
