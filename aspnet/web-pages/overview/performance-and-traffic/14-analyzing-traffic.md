---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: ASP.NET 웹 페이지 (Razor) 사이트에 대 한 추적 방문자 정보 (분석) | Microsoft Docs
author: tfitzmac
description: 라인 웹 사이트를 참조 한 후에 웹 사이트 트래픽을 분석 하는 것이 좋습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 9a381ebaed30325fdfa5f0f558910d3002c61559
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26528762"
---
<a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 대 한 방문자 정보 (분석)를 추적합니다.
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 웹 사이트 분석을 추가 하는 도우미를 사용 하는 방법을 설명 합니다.
> 
> 학습 내용:
> 
> - 웹 사이트 트래픽 정보 분석 공급자를 전송 하는 방법.
> 
> 다음은 문서에 도입 된 기능을 프로그래밍 하는 ASP.NET입니다.
> 
> - `Analytics` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - ASP.NET Web Helpers Library (NuGet 패키지)


분석은 사용자가 해당 사이트를 사용 하는 방식을 이해할 수 있도록 웹 사이트의 트래픽을 측정 하는 기술에 대 한 일반적인 용어입니다. 많은 분석 서비스는 Google, Yahoo, StatCounter, 등에서 서비스를 포함 하 여 사용할 수 있습니다.

작동 하에 등록할 계정 등록 한다고 가정해 봅시다 사이트 분석 공급자와 함께 하는 방식으로 분석 추적 하려고 합니다. 공급자 ID 또는 계정에 대 한 코드를 추적을 포함 하는 JavaScript 코드의 코드 조각은 보냅니다. 추적 하려는 사이트의 웹 페이지에는 JavaScript 코드 조각을 추가 합니다. (일반적으로 분석 코드 조각을 추가한 바닥글 또는 레이아웃 페이지 또는 사이트의 모든 페이지에 표시 되는 다른 HTML 태그입니다.) 사용자가 이러한 JavaScript 조각 중 하나를 포함 하는 페이지를 요청, 코드 조각을 현재 페이지에 대 한 정보를 페이지에 대 한 다양 한 세부 정보를 기록 하 게 분석 공급자를 보냅니다.

사이트 통계를 확인 하려는 경우에 분석 공급자의 웹 사이트에 로그인 합니다. 같은 사이트에 대 한 모든 종류의 보고서를 볼 수 있습니다.

- 개별 페이지에 대 한 페이지 보기 수입니다. 이 표시는 사이트를 방문 하는 개략적인 얼마나 많은 사람들이 사이트에 해당 페이지가 가장 많이 사용 합니다.
- 시간 사람들은 특정 페이지에 대 한 주입니다. 이 홈 페이지 관심 있는 사람들의 동기화가 있는지 여부 등을 확인할 수 있습니다.
- 사이트를 방문 하기 전에 사이트 사용자에 했습니다. 이렇게 하면 트래픽이 검색과 등에서 링크에서 온 것인지 여부를 이해 하는 데 있습니다.
- 사용자 사이트를 방문 하는 경우 및 시간을 유지 합니다.
- 어떤 국가에서 방문자가 있습니다.
- 어떤 브라우저와 운영 체제 방문자가 사용 하는 합니다.

    ![Ch14traffic 1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>도우미 메서드를 사용 하 여 분석 한 페이지에 추가 하려면

ASP.NET 웹 페이지에는 여러 가지 분석 도우미가 포함 되어 (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, 및 `Analytics.GetStatCounterHtml`) 쉽게 분석에 사용 되는 JavaScript 코드 조각을 관리할 수 있도록 하는 합니다. 방법 및 위치를 파악 하는 대신 JavaScript 코드에만 하면 됩니다 도우미 페이지에 추가 합니다. 제공 하는 데 필요한 유일한 정보는 계정 이름, ID 또는 추적 코드는 합니다. (StatCounter, 있어 몇 가지 추가 값을 제공 합니다.)

이 절차에서 사용 하는 레이아웃 페이지 만듭니다는 `GetGoogleHtml` 도우미입니다. 다른 분석 공급자 중 하나가 지정 된 계정이 이미 있는 경우 해당 계정을 대신 사용할 수 있으며 필요에 따라 약간의 조정 합니다.

> [!NOTE]
> 분석 계정을 만들 때 추적 될 사이트의 URL을 등록 합니다. 경우 로컬 컴퓨터의 모든 항목을 테스트 하는, 있하지 않습니다을 추적 하지 (트래픽만 사용자) 실제 트래픽, 사이트 통계를 기록 하 고 봅니다를 수 없습니다. 하지만이 절차는 분석 도우미 페이지에 추가 되는 방법을 보여 줍니다. 사이트를 게시할 라이브 사이트 분석 공급자에 정보를 전송 합니다.


1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)추가 하지 않은 경우.
2. Google 웹 로그 분석 계정을 만들고 및 계정 이름을 기록 합니다.
3. 명명 된 레이아웃 페이지 만들기 *Analytics.cshtml* 다음 태그를 추가 합니다.

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > 에 대 한 호출을 배치 해야는 `Analytics` 웹 페이지의 본문에는 도우미 (전에 `</body>` 태그). 그렇지 않은 경우 브라우저는 스크립트를 실행 되지 않습니다.

    다른 분석 공급자를 사용 하는 경우 대신 다음 도우미 중 하나:

    - (Yahoo)`@Analytics.GetYahooHtml("myaccount")`
    - (StatCounter)`@Analytics.GetStatCounterHtml("project", "security")`
4. 대체 `myaccount` 계정, ID 또는 1 단계에서 만든 추적 코드의 이름으로 합니다.
5. 브라우저에서 페이지를 실행 합니다. (있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.)
6. 브라우저에서 페이지 소스를 봅니다. 렌더링 된 분석 코드를 볼 수 있습니다.

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. Google Analytics 사이트로 하 고 사이트에 대 한 통계를 검사 합니다. 라이브 사이트에서 페이지를 실행할 방문 페이지를 기록 하는 항목이 표시 됩니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [Google Analytics 사이트](https://www.google.com/analytics/)
- [Yahoo! 웹 사이트 분석](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter 사이트](http://statcounter.com/)
