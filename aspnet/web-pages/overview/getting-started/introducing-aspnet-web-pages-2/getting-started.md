---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: ASP.NET 웹 페이지-Getting Started 소개 | Microsoft Docs
author: tfitzmac
description: WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다. Visual Studio 또는 Visual Studio Code를 사용 합니다. 이 설명서는 중...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 12878082306cf51f8ea08ae614d9420251ecb587
ms.sourcegitcommit: 8bf4dff3069e62972c1b0839a93fb444e502afe7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46482959"
---
<a name="introducing-aspnet-web-pages---getting-started"></a>시작-ASP.NET 웹 페이지 소개
====================
[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다. 사용 하 여 [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) 하거나 [Visual Studio Code](https://code.visualstudio.com/)합니다.
> 
> 
> 이 지침과 응용 프로그램 사용 하면 ASP.NET 웹 페이지 (버전 2 이상)의 개요 및 Razor 구문, 동적 웹 사이트를 만들기 위한 간단한 프레임 워크입니다. 또한 WebMatrix, 페이지 및 사이트를 만들기 위한 도구를 소개 합니다.
> 
> **수준**: 새 ASP.NET 웹 페이지입니다.  
> **가정 하는 기술을**: HTML, 기본 css 스타일 시트 ().
> 
> 학습할 내용 집합의 첫 번째 자습서에서:
> 
> - ASP.NET Web Pages 기술 이며에 대 한 것입니다.
> - WebMatrix의는입니다.
> - 모든 항목을 설치 하는 방법입니다.
> - WebMatrix를 사용 하 여 웹 사이트를 만드는 방법입니다.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - Microsoft 웹 플랫폼 설치 관리자
> - WebMatrix 합니다.
> - *.cshtml* 페이지
>   
> 
> Mike 되는 원래이 자습서를 작성 합니다. Tom FitzMacken Microsoft WebMatrix 3에 대 한 업데이트 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - WebMatrix 3


## <a name="what-should-you-know"></a>무엇을 알아야 합니다 있습니다?

사용 하 여 친숙 하다는 것으로 가정 합니다.

- **HTML**합니다. 없는 심층적인 전문 지식이 필요 합니다. HTML 설명 하지 않겠습니다 것도 사용 하지 마십시오 복잡 한 것입니다. 여기서 생각 유용 HTML 자습서의 링크를 제공 합니다.
- **Css 스타일 시트 ()** 합니다. 과 HTML입니다.
- **기본 데이터베이스 아이디어**합니다. 데이터에 대 한 스프레드시트를 사용 하 고 정렬 하 고 수준의 전문성을를 데이터를 필터링 하는 경우이 자습서 집합 일반적으로 하는 것 이라고 가정 합니다.

기본 프로그래밍을 알아보는 데 관심이 있다고도 하는 것으로 가정 합니다. ASP.NET Web Pages 라는 C# 프로그래밍 언어를 사용 합니다. 프로그래밍에서는 방금 것에 관심이 있는 배경 지식이 필요가 없습니다. 그 어느 때 하기 전에 웹 페이지에서 JavaScript를 작성 한, 배경의 충분 했습니다.

신규 프로그래머 속도 제공 하는 동안는 프로그래밍에 익숙한 경우 볼 수 있습니다이 자습서를 처음 설정 하는 참고 느리게 이동 합니다. 첫 번째 몇 가지 자습서 이전 해지면 하지만 작은 기본 프로그래밍에 대해 설명 하 고 작업 빠른 클립에 따라 이동 됩니다.

## <a name="what-do-you-need"></a>무엇이 필요?

필요한 사항은 다음과 같습니다.

- Windows 8, Windows 7, Windows Server 2008 또는 Windows Server 2012를 실행 하는 컴퓨터입니다.
- 인터넷으로 연결 합니다.
- 관리자 권한 (설치 과정에 필요).

## <a name="what-is-aspnet-web-pages"></a>ASP.NET 웹 페이지는 무엇입니까?

ASP.NET 웹 페이지에는 동적 웹 페이지를 만드는 데 사용할 수 있는 프레임 워크입니다. 간단한 HTML 웹 페이지를 정적입니다. 콘텐츠는 페이지에는 HTML 태그를 고정된 하 여 결정 됩니다. ASP.NET 웹 페이지를 사용 하 여 만든 것과 같은 동적 페이지 코드를 사용 하 여 즉석에서 페이지 콘텐츠를 만들 수 있습니다.

동적 페이지를 통해 모든 종류의 작업을 수행할 수 있습니다. 폼을 사용 하 여 입력 메시지를 표시 하 고 페이지를 표시 하는 내용 또는 모양을 변경할 수 있습니다. 사용자 로부터 정보를 사용 하 고, 데이터베이스에 저장 하 고, 다음 나중에 나열할 수 있습니다. 사이트에서 전자 메일을 보낼 수 있습니다. (예: 매핑 서비스) 웹에서 다른 서비스와 상호 작용할 수 있으며 해당 소스에서 정보를 통합 하는 페이지를 생성할 수 있습니다.

## <a name="what-is-webmatrix"></a>WebMatrix는 무엇입니까?

WebMatrix는 웹 페이지 편집기, 데이터베이스 유틸리티, 페이지 및 웹 사이트를 인터넷에 게시 하기 위한 기능 테스트에 대 한 웹 서버를 통합 하는 도구입니다. WebMatrix는 무료로 사용할 수 있는 및 설치 하 고 사용 하기 쉬운 것입니다. (또한 작동 일반 HTML 페이지 및 PHP와 같은 다른 기술에 대 한 합니다.)

실제로 하지 *있는* WebMatrix를 사용 하 여 ASP.NET 웹 페이지를 사용 하 여 작업을 합니다. 편집기에서 텍스트를 사용 하 여 페이지를 만드는 예를 들어 하 수에 대 한 액세스를 해야 하는 웹 서버를 사용 하 여 페이지를 테스트 합니다. 그러나 WebMatrix 모두 매우 쉽게,이 자습서 전체에서 WebMatrix를 사용 됩니다.

## <a name="about-these-tutorials"></a>이 자습서에 대 한

이 자습서 집합은 ASP.NET 웹 페이지를 사용 하는 방법 소개 합니다. 이 소개 자습서 집합에서 총 9 자습서가 있습니다. 실제, 전문적인 웹 사이트를 만드는 ASP.NET Web Pages 초보자에서 안내 하는 일련의 자습서 집합 느껴집니다.

이 첫 번째 자습서에서 ASP.NET 웹 페이지를 사용 하 여 작업 하는 방법의 기본 사항을 보여 주는 중점적으로 다룹니다를 설정 합니다. 완료 되 면이 종료 하 고 좀 더 깊이 웹 페이지를 탐색 하는 위치를 선택 하는 추가 자습서 집합으로 작업할 수 있습니다.

에서는 의도적으로 이동 쉽게 자세히 설명 합니다. 선택한 항목 살펴보겠습니다 때마다이 자습서 집합에 대 한에서는 항상 생각 하는 방식은 가장 이해 하기 쉽습니다. 이후 자습서 더 심층적으로 살펴보는 집합과 보다 효율적인 또는 보다 유연한 방법 (더 재미도)를 표시 합니다. 하지만 이러한 자습서를 먼저 기본 사항을 이해 해야 합니다.

방금 시작한 자습서 집합 ASP.NET 웹 페이지의 이러한 기능에 설명 합니다.

- 소개 및 시작 하는 모든 항목이 설치 되어 있습니다. (이것이 여러분 글을 읽고 자습서입니다.)
- ASP.NET 웹 페이지 프로그래밍의 기초입니다.
- 데이터베이스를 만드는 중입니다.
- 만들기 및 사용자 입력된 양식을 처리 합니다.
- 추가, 업데이트 및 데이터베이스의 데이터를 삭제 합니다.

## <a name="what-will-you-create"></a>만드나요?

이 자습서 집합 및 이후의 조건은 원하는 영화를 나열할 수 있는 웹 사이트를 중심으로 합니다. 영화를 입력 하면 편집 하 고 나열을 수 있습니다. 이 자습서 집합에서 만들어야 하는 페이지를 가지는 다음과 같습니다. 첫 번째 목록 페이지를 만들어야 하는 영화를 보여 줍니다.

![동영상 목록을 보여 주는 완료 했습니다 동영상 앱](getting-started/_static/image1.png)

그리고은 사이트에 새 영화 정보를 추가할 수 있는 페이지.

![추가 동영상 페이지를 보여 주는 완료 된 동영상 앱](getting-started/_static/image2.png)

후속 자습서 집합 빌드에 설정 하 고, 전자 메일 보내기 및 소셜 미디어 통합에 로그인 하는 사람, 사진 업로드 같은 더 많은 기능을 추가 합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 참조

라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까? 다음 단추를 클릭 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션:

- [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.

## <a name="installing-everything"></a>모든 설치

Microsoft에서 웹 플랫폼 설치 관리자를 사용 하 여 모든 항목을 설치할 수 있습니다. 실제로 설치 관리자를 설치 하 고를 사용 하 여 다른 모든 요소를 설치 합니다.

웹 페이지를 사용 하려면 적어도 대해서도 해야 Windows Server 2008 이상 또는 Windows XP SP3 설치 합니다.

에 [웹 페이지의 페이지](../../../index.md) ASP.NET 웹 사이트 클릭 **설치**합니다.

![ASP.NET 웹 사이트 표시 &quot;WebMatrix 설치&quot; 단추](getting-started/_static/image3.png)

개인정보취급방침 WebMatrix를 설치 하기 전에 사용 약관에 동의 하 라는 메시지가 표시 됩니다.

![설치를 시작 하는 용어를 허용 합니다.](getting-started/_static/image4.png)

클릭 **실행** 설치를 시작 합니다. (설치 관리자를 저장 하려면 클릭 **저장할** 다음 저장 폴더에서 설치 관리자를 실행 합니다.)

![](getting-started/_static/image5.png)

웹 플랫폼 설치 관리자를 표시 하는 작업은 WebMatrix를 설치할 준비가 되었습니다. **설치**를 클릭합니다.

![](getting-started/_static/image6.png)

설치 프로세스는 컴퓨터에 설치 하는 것에 파악 하 고 프로세스를 시작 합니다. 어떤 정확 하 게 설치할 수에 따라 프로세스 걸릴 수 있습니다 몇 분에서 몇 분 정도입니다. 선택 **동의** 라이선스 사용 조건에 동의 합니다.

## <a name="hello-webmatrix"></a>Hello, WebMatrix

완료 되 면 설치 프로세스는 WebMatrix를 자동으로 시작할 수 있습니다. 그렇지 않은 경우 Windows에서의를 **시작** 메뉴에서 **Microsoft WebMatrix**합니다.

WebMatrix를 처음 시작할 때 Microsoft 계정으로 Microsoft Azure에 로그인 할 수 있는 기회를 제공 됩니다. 로그인 하면 Azure 통해 10 개의 무료 웹 앱 받게 됩니다. 이러한 무료 웹 앱에 앱을 테스트 하는 편리한 방법을 제공 합니다. Azure 계정이 아직 없는 경우 MSDN subscription 필요가 있습니다 [MSDN 구독 혜택을 활성화](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)합니다. 이 고, 그렇지 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 하세요 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.

이 자습서를 계속 하려면 지금 로그인 필요가 없습니다. 서명 하지 않은 이제, 하는 경우 여전히 나중에 로그인 하는 옵션을 해야 합니다. 마지막 [항목](publishing.md) 시계열이이 자습서에서는 Azure에 웹 사이트를 배포 하는 방법에 설명, 따라서 해당 항목을 완료 하려면 로그인 해야 합니다.

Microsoft 계정 또는 선택 로그인 하거나 이때 **나중에** 오른쪽 아래 모퉁이에서.

![링크를](getting-started/_static/image7.png)

시작 하려면 있습니다 빈 웹 사이트를 만들고 페이지를 추가 합니다. 이 자습서의 뒷부분에서 기본 제공 웹 사이트 템플릿 중 하나를 사용 하 여 재생할 수 있습니다.

시작 창에서 클릭 **새로 만들기**합니다.

![WebMatrix 시작 화면](getting-started/_static/image8.png)

템플릿은 미리 작성 된 파일 및 다양 한 유형의 웹 사이트에 대 한 페이지입니다. 기본적으로 사용할 수 있는 템플릿을 모두를 보려면 템플릿 갤러리 옵션을 선택 합니다.

![템플릿 갤러리 선택](getting-started/_static/image9.png)

에 **빠른 시작** 창에서 **빈 사이트** 에서 **ASP.NET** 그룹화 하 고 새 사이트 "WebPagesMovies" 이름입니다.

![선택한 빈 사이트 템플릿 사용 하 여 WebMatrix 빠른 시작 창](getting-started/_static/image10.png)

**다음**을 클릭합니다.

Microsoft 계정에 로그인 한 경우 Azure에서 사이트를 만들 수를 제공 됩니다. 기본 이름은 사이트의 이름을 기반으로 **WebPagesMovies.azurewebsites.net** 제안 됩니다; 그러나 느낌표가이 이름은 Windows Azure에서 제공 되지 않음을 나타냅니다. 간단히 하기 위해 선택 **Skip** 지금 Azure에서 웹 사이트를 작성 하지 않으려면입니다. 이 시리즈의 뒷부분에서 Azure로 사이트를 게시 됩니다.

![azure 사이트 만들기](getting-started/_static/image11.png)

WebMatrix가 만들고 사이트가 열립니다.

![WebMatrix에 새 WebPagesMovies 사이트 열기](getting-started/_static/image12.png)

맨 위에 있는 빠른 실행 도구 모음 및 리본 메뉴가 있습니다. 왼쪽 아래에 표시 작업 영역 선택기 작업 간에 전환 하는 위치 (**사이트**를 **파일**를 **데이터베이스**를 **보고서**). 오른쪽의 편집기 및 보고서에 대 한 콘텐츠 창이입니다. 및 맨 아래에서 종종 보게 메시지에 대 한 알림 표시줄을 합니다.

이 자습서를 진행 하면서 WebMatrix 및 해당 기능에 대해 자세히 알아봅니다.

## <a name="creating-a-web-page"></a>웹 페이지 만들기

WebMatrix 및 ASP.NET Web Pages에 익숙해지고 간단한 페이지를 만들어야 합니다.

작업 영역 선택기를 선택 합니다 **파일** 작업 영역입니다. 이 작업 영역에는 파일 및 폴더를 사용 하 여 작업할 수 있습니다. 왼쪽된 창에 사이트의 파일 구조를 보여 줍니다. 파일 관련 작업을 표시 하는 리본 바뀝니다.

![WebMatrix 작업 영역 파일](getting-started/_static/image13.png)

리본 메뉴에 아래의 화살표를 클릭 **새로 만들기** 을 클릭 한 다음 **새 파일**합니다.

![사용 하는 &quot;새로 만들기&quot; 새 파일을 만들려면 리본 메뉴에 명령](getting-started/_static/image14.png)

WebMatrix에는 파일 형식 목록을 표시합니다. 선택 **CSHTML**, 및는 **이름** 상자에 "HelloWorld"를 입력 합니다. CSHTML 페이지는 ASP.NET Web Pages 페이지가입니다.

![HelloWorld.cshtml 라는 새 CSHTML 페이지 만들기](getting-started/_static/image15.png)

**확인**을 클릭합니다.

WebMatrix 페이지를 만들고 편집기에서 열립니다.

![WebMatrix 편집기에서 새 HelloWorld 페이지](getting-started/_static/image16.png)

알 수 있듯이 대부분 일반 HTML 태그를 다음과 같이 맨 위에 있는 블록을 제외 하 고 페이지에 포함 됩니다.

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

잠시 후에 볼 수 있듯이 코드를 추가 합니다.

페이지의 다른 부분 &mdash; 요소 이름, 특성 및 텍스트와 맨 위에 있는 블록-서로 다른 색으로 모든 됩니다. 이 이라고 *구문 강조 표시*, 쉽게 모든 항목의 선택을 취소 하 고 있습니다. 쉽게 WebMatrix에서 웹 페이지를 사용 하 여 작업할 수 있도록 하는 기능 중 하나입니다.

콘텐츠를 추가 합니다 `<head>` 및 `<body>` 다음 예와에서 같은 요소입니다. (원한다 면 방금 다음 블록을 복사 하 수 전체 기존 페이지를 다음이 코드로 바꿉니다.)

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

빠른 실행 도구 모음 또는 합니다 **파일** 메뉴에서 클릭 **저장**합니다.

![WebMatrix 빠른 실행 도구 모음에서 저장 단추](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>페이지 테스트

에 **파일** 작업 영역에서 마우스 오른쪽 단추로 클릭 합니다 *HelloWorld.cshtml* 페이지를 클릭 한 다음 **브라우저에서 시작**합니다.

![WebMatrix 리본에서 [실행] 단추를 사용 하는 페이지를 실행 합니다.](getting-started/_static/image18.png)

WebMatrix는 컴퓨터에 페이지를 테스트 하는 데 사용할 수 있는 기본 제공 웹 서버 (IIS Express)를 시작 합니다. (WebMatrix에서 IIS Express 없이 해야 페이지를 웹 서버에 게시 어딘가에 전에 테스트할 수 있습니다.) 페이지는 기본 브라우저에 표시 됩니다.

![&quot;Hello World&quot; 브라우저에서 실행 되 고 페이지](getting-started/_static/image19.png)

WebMatrix에서 페이지를 테스트 하는 경우 브라우저에서 URL는 비슷하게 `http://localhost:33651/HelloWorld.cshtml.` 이름을 *localhost* 페이지가 자신의 컴퓨터에 있는 웹 서버에서 반환 되는 즉, 로컬 서버를 가리킵니다. 언급 했 듯이 WebMatrix 라는 페이지를 시작 하는 경우 실행 되는 IIS Express 웹 서버 프로그램을 포함 합니다.

다음의 숫자 *localhost* (예를 들어 *localhost:33651*) 참조를 *포트 번호* 컴퓨터에. 이 특정 웹 사이트의 IIS Express를 사용 하는 "채널"입니다. 포트 번호는 사이트를 만들고이 사용자가 만든 모든 사이트에 대 한 다른 1024 ~ 65536 범위에서 임의로 선택 됩니다. (고유한 사이트를 테스트 하는 경우 포트 번호를 반드시 있습니다 33561 보다 여러.) 각 웹 사이트에 다른 포트를 사용 하 여 IIS Express 유지할 수 직선와 통신 하는지 사이트입니다.

사이트를 게시할 공용 웹 서버에 더 이상 표시 하는 경우 이후 *localhost* url에서입니다. 이 시점에서 볼 수와 같은 보다 일반적인 URL `http://myhostingsite/mywebsite/HelloWorld.cshtml` 무엇이 든 페이지 또는 합니다. 이 자습서 시리즈의 뒷부분에서 사이트를 게시 하는 방법에 대 한 더 알아봅니다 됩니다.

## <a name="adding-some-server-side-code"></a>일부 서버 쪽 코드를 추가합니다.

브라우저를 닫고 WebMatrix에서 페이지로 돌아갑니다.

다음 코드와 같이 표시 되도록 줄 코드 블록을 추가 합니다.

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

약간 Razor 코드의 경우 아마도 명확 현재 날짜 및 시간을 가져옵니다 해당 값을 배치 하는 *변수* 라는 `currentDateTime`합니다. 자세한 내용을 확인할 수 있습니다 다음 자습서의 Razor 구문에 대 한 합니다.

페이지의 본문에 후는 `<p>Hello World!</p>` 요소에 다음을 추가 합니다.

[!code-html[Main](getting-started/samples/sample4.html)]

이 코드에 배치 하는 값을 가져옵니다는 `currentDateTime` 맨 위에 있는 변수는 페이지의 태그에 삽입 합니다. `@` 문자 페이지에서 ASP.NET 웹 페이지 코드를 표시 합니다.

(WebMatrix 변경 내용을 저장 하면에 대 한 페이지를 실행 하기 전에)의 페이지를 다시 실행 합니다. 이 현재 날짜 및 시간 페이지에 표시 됩니다.

![&quot;Hello World&quot; 동적으로 생성 된 시간 표시를 사용 하 여 브라우저에서 실행 되는 페이지](getting-started/_static/image20.png)

몇 분 정도 기다린 다음 브라우저에서 페이지를 새로 고칩니다. 날짜 및 시간 표시를 업데이트 됩니다.

브라우저에서 페이지 소스를 확인 합니다. 다음 태그는 다음과 같습니다.

[!code-html[Main](getting-started/samples/sample5.html)]

에 `@{ }` 맨 위에 있는 블록 없는 합니다. 날짜 및 시간 표시는 실제 문자열을 확인할 수도 (`1/18/2012 2:49:50 PM` 또는)가 아니라 `@currentDateTime` 에서 제공 되었던 같은 합니다 *.cshtml* 페이지. 같습니다. 페이지를 실행 하면 ASP.NET 처리 모든 코드 (거의이 경우)로 표시 된 내용 `@`합니다. 코드 출력을 생성 하 고 출력을 페이지에 삽입 된 키를 누릅니다.

## <a name="this-is-what-aspnet-web-pages-are-about"></a>이 새로운 ASP.NET 웹 페이지에 대 한

ASP.NET 웹 페이지 동적 웹 콘텐츠를 생성 한다는 읽을 때 개념은 여기서 살펴본 것입니다. 방금 만든 페이지 전에 볼 수 있는 동일한 HTML 태그를 포함 합니다. 모든 종류의 작업을 수행할 수 있는 코드를 포함할 수도 있습니다. 이 예제에서는 현재 날짜 및 시간을 가져오는 간단한 작업을 수행한 것입니다. 살펴본 것 처럼 HTML 페이지에서 출력을 사용 하 여 코드 중간에 삽입할 수 있습니다. 사용자가 요청 하는 경우는 *.cshtml* ASP.NET 브라우저에서 페이지의 웹 서버에에서 있는 동안 해당 페이지를 처리 합니다. ASP.NET 코드의 출력 (있는 경우) 페이지에 삽입 된 HTML로. 코드를 처리 하는 완료 되 면 ASP.NET 결과 페이지를 브라우저에 보냅니다. 브라우저가 적이 받는 HTML입니다. 다음 다이어그램은입니다.

![생성 하는 방법을 ASP.NET HTML 동적으로의 개념적 흐름](getting-started/_static/image21.png)

개념은 간단 하지만 코드를 수행할 수 있는 여러 가지 흥미로운 작업 않으며 여러 가지 흥미로운 수 동적으로 추가할 수 있는 HTML 콘텐츠 페이지에 있습니다. 및 ASP.NET *.cshtml* 모든 HTML 페이지와 같은 페이지를 브라우저 자체 (JavaScript 및 jQuery 코드)에서 실행 되는 코드를 포함할 수도 있습니다. 이 자습서 집합 및 이후의 조건은 이러한 작업을 모두 알아봅니다.

## <a name="coming-up-next"></a>다음에 나오는

이 시리즈의 다음 자습서에서는 ASP.NET 웹 페이지 프로그래밍 좀 더 살펴봅니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 사이트를 처음부터 만들기](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)합니다. 이것은 특히는 자습서 WebMatrix (없습니다: ASP.NET 웹 페이지)를 사용 하는 방법에 대 한 합니다. 으로 이동 하기 잠시이 자습서 집합에서 다루지는 WebMatrix의 추가 기능 중 일부에 대 한 자세한 정보.

> [!div class="step-by-step"]
> [다음](intro-to-web-pages-programming.md)
