---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: ASP.NET 웹 페이지 (Razor) 사이트에 대 한 방문자 정보 (분석)를 추적 | Microsoft Docs
author: tfitzmac
description: 이동 하 여 웹 사이트를 받은 후에 웹 사이트 트래픽을 분석 하는 것이 좋습니다.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: aabe3177ba9479bfafafe81e1ea99a58f29d5271
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837325"
---
<a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 대 한 방문자 정보 (분석)를 추적합니다.
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 ASP.NET Web Pages (Razor) 웹 사이트의 페이지에 웹 분석을 추가 하려면 도우미를 사용 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 분석 공급자 웹 사이트 트래픽이 대 한 정보를 보내는 방법입니다.
> 
> ASP.NET 문서에 도입 된 기능을 프로그래밍은 다음과 같습니다.
> 
> - `Analytics` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - ASP.NET Web Helpers Library (NuGet 패키지)


Analytics는 사용자가 사이트를 사용 하는 방식을 이해할 수 있도록 웹 사이트의 트래픽을 측정 하는 기술에 대 한 일반적인 용어입니다. 많은 분석 서비스에서 Google, Yahoo, StatCounter, 및 기타 서비스를 포함 하 여 사용할 수 있습니다.

Works는 등록할는 계정에 대 한 사이트를 등록 하는 위치는 분석 공급자를 사용 하 여 해당 하는 방식으로 분석 추적 하려고 합니다. 공급자는 ID 또는 계정에 대 한 코드 추적을 포함 하는 JavaScript 코드 조각을 보냅니다. 추적 하려는 사이트의 웹 페이지에 JavaScript 코드 조각을 추가 합니다. (일반적으로 분석 코드 조각을 추가한 바닥글 또는 레이아웃 페이지 또는 사이트에서 모든 페이지에 표시 되는 다른 HTML 태그입니다.) 사용자가 이러한 JavaScript 조각 중 하나를 포함 하는 페이지에 요청 하는 경우 코드 조각 페이지에 대 한 다양 한 세부 정보를 기록 하는 분석 공급자에 게 현재 페이지에 대 한 정보를 보냅니다.

사이트 통계를 확인 하려는 경우 분석 공급자의 웹 사이트에 로그인 합니다. 그런 다음 같은 사이트에 대 한 모든 종류의 보고서를 볼 수 있습니다.

- 개별 페이지에 대 한 페이지 보기 수입니다. 그러면 개략적으로 얼마나 많은 사람들이 사이트를 방문 하 여 및 가장 널리 사용 되는 사이트에서 페이지입니다.
- 기간 사용자 특정 페이지에 소비 합니다. 이 홈 페이지에는 사람들의 관심을 유지 하는 여부 등을 알 수 있습니다.
- 사이트 사람들이 전의 사이트를 방문한 적이 있습니다. 그러면 트래픽이 검색에서 링크를에서 제공 되는지 여부를 파악할 수 있습니다.
- 사용자가 사이트를 방문 하는 경우 및 기간 유지 합니다.
- 어떤 국가에서 방문자입니다.
- 브라우저 및 운영 체제를 방문자에 게 사용 합니다.

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>분석 페이지를 추가 하는 도우미를 사용 하 여

ASP.NET 웹 페이지에는 몇 가지 분석 도우미가 포함 되어 (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, 및 `Analytics.GetStatCounterHtml`)는 쉽게 분석에 사용 되는 JavaScript 코드를 관리 합니다. 방법 및 위치를 파악 하는 대신 JavaScript 코드를 삽입할 수행 해야 됩니다 도우미 페이지에 추가. 정보만 제공 해야 할 경우 계정 이름, ID 또는 추적 코드 (StatCounter, 또한 해야 몇 가지 추가 값을 제공 합니다.)

이 절차를 사용 하는 레이아웃 페이지 만듭니다는 `GetGoogleHtml` 도우미입니다. 다른 분석 공급자 중 하나를 사용 하 여 계정이 이미 있는 경우에 계정을 대신 사용 하 고 필요에 따라 약간의 조정이 수 있습니다.

> [!NOTE]
> Analytics 계정을 만들면 추적 하려는 사이트의 URL을 등록 합니다. 수 없습니다 (트래픽만으로 하는) 실제 트래픽을 추적, 테스트 하려는 모든 로컬 컴퓨터의 경우 사이트 통계를 기록 하 고 봅니다 수 있도록 합니다. 하지만이 이렇게 페이지 분석 도우미를 추가 하는 방법을 보여 줍니다. 사이트를 게시할 때 라이브 사이트 분석 공급자에 정보를 보낼 됩니다.


1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)추가 하지 않은 경우.
2. Google 웹 로그 분석을 사용 하 여 계정을 만들고 계정 이름을 기록 합니다.
3. 명명 된 레이아웃 페이지를 만듭니다 *Analytics.cshtml* 다음 태그를 추가 합니다.

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > 에 대 한 호출을 배치 해야 합니다는 `Analytics` 웹 페이지의 본문에는 도우미 (전에 `</body>` 태그). 그렇지 않은 경우 브라우저는 스크립트를 실행 되지 않습니다.

    다른 분석 공급자를 사용 하는 경우 대신 다음 도우미 중 하나:

    - (Yahoo) `@Analytics.GetYahooHtml("myaccount")`
    - (StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`
4. 대체 `myaccount` 계정, ID 또는 1 단계에서 만든 추적 코드의 이름입니다.
5. 브라우저에서 페이지를 실행 합니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.)
6. 브라우저에서 페이지 소스를 봅니다. 렌더링 된 분석 코드를 볼 수 있습니다.

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. Google Analytics 사이트에 로그인 하 고 사이트에 대 한 통계를 검사 합니다. 라이브 사이트에서 페이지를 실행 하는 경우 기록 페이지에 방문 하는 항목이 표시 됩니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [Google Analytics 사이트](https://www.google.com/analytics/)
- [Yahoo! Web Analytics 사이트](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter 사이트](http://statcounter.com/)
