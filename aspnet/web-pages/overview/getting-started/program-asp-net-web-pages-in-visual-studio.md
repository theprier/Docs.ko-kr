---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 프로그래밍 ASP.NET 웹 페이지 (Razor)를 사용 하 여 Visual Studio | Microsoft Docs
author: tfitzmac
description: 이 부록에서는 ASP.NET 웹 페이지 Razor 구문 사용 하 여 프로그램을 Visual Studio 2010 또는 Visual Web Developer 2010 Express를 사용 하는 방법을 설명 합니다.
ms.author: aspnetcontent
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 46807b464499b2e60d995d37f161ca129d38f439
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834457"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Visual Studio를 사용 하 여 ASP.NET 웹 페이지 (Razor) 프로그래밍
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 프로그램 ASP.NET Web Pages (Razor) 웹 사이트에 Visual Studio 또는 Visual Web Developer Express를 사용 하는 방법을 설명 합니다.
> 
> 학습할 내용
> 
> - ASP.NET 웹 페이지를 사용 하 여 Visual Studio 버전에서 작동 하도록 (내용이 있는 경우)를 설치 해야 할 항목.
> - Visual Web Developer 2010 Express에 ASP.NET 웹 페이지에 대 한 지원을 추가 하는 방법입니다.
> - ASP.NET Razor 페이지, IntelliSense 등의 디버거를 사용 하려면 Visual Studio의 기능을 사용 하는 방법.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2, Visual Studio 2012, Visual Studio 2010 및 WebMatrix 2 에서도 작동합니다.


WebMatrix 또는 다른 여러 코드 편집기를 사용 하 여 Razor 구문이 있는 ASP.NET 웹 페이지를 프로그래밍할 수 있습니다. 또한 Microsoft Visual Studio는 다양 한 유형의 응용 프로그램 (뿐 아니라 웹 사이트)를 만들기 위한 강력한 도구 집합을 제공 하는 모든 기능을 갖춘 통합된 개발 환경 (IDE)를 사용할 수 있습니다. ASP.NET Razor 페이지를 사용 하려면 Visual Studio의 전체 버전 중 하나를 사용 또는 무료 [Visual Studio Express for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express) 버전입니다.

두 특히 유용한 Visual Studio는 ASP.NET Razor 웹 페이지를 사용 하 여 프로그래밍 하는 기능은 다음과 같습니다.

- *IntelliSense*합니다. Visual Studio에 기본 제공 IntelliSense 기능은 WebMatrix에서 IntelliSense 보다 더 포괄적입니다.
- *디버거*합니다. 디버거를 사용 하면 코드 실행, 변수 검사를 한 줄씩 코드를 단계별로 실행 하면 프로그램을 중지 하 여 해결할 수 있습니다.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Visual Studio를 사용 하 여 다른 버전의 ASP.NET 웹 페이지를 사용 하 여

Visual Studio 2012 및 Visual Studio 2013에는 ASP.NET 웹 페이지에 대 한 지원이 포함 됩니다. (ASP.NET 웹 페이지를 지원 하기 위해 필요한 패키지 설치 되어 Visual Studio를 설치 합니다.)

Visual Studio 2010 지원이 포함 되지 않습니다 기본적으로 ASP.NET 웹 페이지에 대 한 합니다. Visual Studio 2010을 사용 하 여 ASP.NET 웹 페이지를 사용 하려면 ASP.NET MVC 패키지를 설치 해야 합니다. ASP.NET 웹 페이지 2를 가져오려면 ASP.NET MVC 4를 설치 합니다.

다음 표에서 서로 다른 버전의 Visual Studio에서 ASP.NET 웹 페이지에 대 한 지원.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET 웹 페이지 2** | ASP.NET MVC 4를 설치 합니다. | (포함) | (포함) |
| **ASP.NET 웹 페이지 3** |  | 업데이트를 ASP.NET 웹 페이지를 통해 NuGet 3 | (포함) |

Visual Studio 2010을 사용 하려면 참조 [Visual Studio 2010에서 ASP.NET 웹 페이지에 대 한 지원 설치](#vs2010support)합니다.

## <a name="launching-visual-studio-from-webmatrix"></a>WebMatrix에서 Visual Studio를 시작합니다.

WebMatrix에서 프로젝트를 시작 하 고 Visual Studio로 전환 하려고 할 경우 WebMatrix는 Visual Studio에서 프로젝트를 쉽게 여는 단추를 제공 합니다. 사용 하도록 Visual Studio이이 단추에 대 한 컴퓨터에 설치 되어 있어야 합니다. 다음 이미지는 WebMatrix에서 단추를 표시 합니다.

![Visual Studio를 시작 합니다.](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

단추를 클릭 하면 프로젝트를 Visual Studio에서 열려 있습니다. 전환할 수 있습니다 앞뒤로 WebMatrix 및 Visual Studio 간에 아무 문제 없이 합니다. 모든 파일에서 다른 환경에서 변경 되었습니다. 최신 변경 내용을 가져오는 다시 로드 해야 하는 경우 알려 줍니다.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Visual Studio에서 ASP.NET Razor 사이트 만들기

Visual Studio에서 ASP.NET Razor 웹 사이트를 만들려면:

1. Visual Studio 또는 Visual Web Developer를 시작 합니다.
2. 에 **파일** 메뉴에서 클릭 **새 웹 사이트**합니다.

    ![새 웹 사이트 만들기](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. 에 **새 웹 사이트** 대화 상자 (Visual C# 또는 Visual Basic)를 사용할 언어를 선택 합니다.
4. 선택 된 **ASP.NET 웹 사이트 (Razor)** 템플릿.

    ![razor 사이트](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. **확인**을 클릭합니다.

새 프로젝트가 존재 하며 시작 하는 데 몇 가지 기본 웹 페이지를 사용 하 여 채워집니다.

### <a name="using-intellisense"></a>IntelliSense 사용

사이트를 만들었으므로 이제 Visual Studio에서 IntelliSense는 작동 하는 방법을 볼 수 있습니다.

1. 방금 만든 웹 사이트에서 엽니다는 *Default.cshtml* 페이지입니다.
2. 후 합니다 `<h3>` 페이지에서 태그 입력 `@ServerInfo.` (마침표 포함). IntelliSense에 대 한 사용 가능한 메서드를 표시 하는 방법의 `ServerInfo` 드롭 다운 목록에서 도우미입니다. 

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 선택 된 `GetHtml` 메서드 목록에서 한 다음 Enter 키를 누릅니다. IntelliSense 메서드를 자동으로 채웁니다. (C#의 모든 메서드를 추가 해야 하는 대로 `()` 메서드 이후에 문자입니다.)  
   에 대 한 완성 된 코드는 `GetHtml` 메서드는 다음 예제와 같습니다.  

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. 페이지를 실행 하려면 Ctrl + F5 키를 누릅니다. 다음은 같은 브라우저에 표시 하면 페이지 모양이입니다. 

    ![브라우저의 기본 페이지](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 브라우저를 닫습니다.

### <a name="using-the-debugger"></a>디버거를 사용 하 여

1. 맨 위에 있는 *Default.cshtml* 페이지에서 시작 하는 줄 뒤 `Page.Title`, 코드의 다음 줄을 추가 합니다. 

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 왼쪽의 코드 편집기의 회색 여백에 클릭이 새 줄을 추가 하기 위해 한 *중단점*합니다. 중단점 상황을 볼 수 있도록 해당 지점에서 프로그램 실행을 중지 하도록 디버거에 지시 하는 마커를입니다.

    ![중단점 설정](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. 호출을 제거 합니다 `ServerInfo.GetHtml` 메서드를 호출을 추가 하 고는 `@myTime` 그 자리에 변수입니다. 이 호출은 코드의 새 줄에 의해 반환 되는 현재 시간 값을 표시 합니다.
4. F5 키를 눌러 디버거에서 페이지를 실행 합니다. 페이지는 사용자가 설정한 중단점에서 중지 합니다. 다음 이미지는 페이지 모양을 편집기 (노란색)에서 중단점을 사용 하 여 보여 줍니다. 

    ![디버그 중단점](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 디버그 도구 모음에서 클릭 합니다 **한 단계씩 코드 실행** 단추 (또는 F11 키를 눌러) 코드의 다음 줄을 실행 합니다. 이 단추를 클릭할 때마다 코드의 다음 줄으로 실행을 진행 합니다.

    ![단추를 한 단계씩](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 값을 검사 합니다 `myTime` 위로 마우스 포인터를 보유 하 여 또는에서 표시 되는 값을 검사 하 여 변수를 **지역** 및 **호출 스택** windows. Visual Studio 변수의 값을 표시 합니다.

    ![시간 표시 값](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 변수를 검사 하 고 단계별 코드 실행을 마친 경우 f5 키를 눌러 각 줄에서 중지 하지 않고 페이지 실행을 계속 합니다. 모든 코드를 단계별로 마쳤으면 브라우저 페이지를 표시 합니다.

디버거 및 Visual Studio에서 코드를 디버깅 하는 방법에 대 한 자세한 내용은 참조 하세요 [연습: Visual Web Developer에서 웹 페이지 디버깅](https://msdn.microsoft.com/library/z9e7w6cs.aspx)합니다.

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Razor를 사용 하 여 Visual Studio를 사용 하 여 ASP.NET MVC 프로젝트에서

ASP.NET MVC 프로젝트에서 Razor 구문은 광범위 하 게도 사용 됩니다. MVC는 강력한 패턴 기반 방식으로 동적 웹 사이트를 빌드하는입니다. ASP.NET Web Pages 사이트 유지 관리 하기가 되 면 ASP.NET MVC 응용 프로그램을 변환 하는 것이 좋습니다. MVC 응용 프로그램을 만드는 예제를 보려면 [ASP.NET MVC 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)합니다.

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Visual Studio 2010에서 ASP.NET 웹 페이지에 대 한 지원 설치

이 섹션에서는 Visual Studio에 대 한 Visual Web Developer Express 2010 및 ASP.NET 웹 페이지 도구를 설치 하는 방법을 보여 줍니다.

1. 웹 플랫폼 설치 관리자를 아직 없는 경우 다음 URL에서 다운로드 합니다.

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 웹 플랫폼 설치 관리자를 실행 합니다.
3. 클릭 합니다 **제품** 탭 합니다.

    ![WebPI 제품 탭](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. 검색할 **ASP.NET MVC 4** (ASP.NET 웹 페이지 2)에 대 한 다음 클릭 **추가**합니다. 이러한 제품에는 ASP.NET Razor 웹 사이트를 구축 하기 위한 Visual Studio 도구가 포함 됩니다.

    ![WebPi 설치 옵션](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 클릭 **설치** 설치를 완료 합니다.
