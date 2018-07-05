---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC 라우팅 개요 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen walther가 ASP.NET MVC 프레임 워크에 브라우저 요청이 컨트롤러 작업에 매핑하는 방법 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: 0f078455397014ba1bcddaeece6dea7737f33710
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384159"
---
<a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC 라우팅 개요 (VB)
====================
[Stephen walther가](https://github.com/StephenWalther)

> 이 자습서에서는 Stephen walther가 ASP.NET MVC 프레임 워크에 브라우저 요청이 컨트롤러 작업에 매핑하는 방법 보여 줍니다.


이 자습서에서는 호출 하는 모든 ASP.NET MVC 응용 프로그램의 중요 한 기능에 도입 된 *ASP.NET 라우팅에서*합니다. ASP.NET 라우팅 모듈은 들어오는 브라우저 요청을 특정 MVC 컨트롤러 작업에 매핑하는 일을 담당 합니다. 이 자습서를 마치면 표준 경로 테이블 요청 컨트롤러 작업에 매핑하는 방법을 이해할 수 있습니다.

## <a name="using-the-default-route-table"></a>기본 경로 테이블을 사용 하 여

새 ASP.NET MVC 응용 프로그램을 만들 때 응용 프로그램이 ASP.NET 라우팅을 사용 하도록 이미 구성 됩니다. ASP.NET 라우팅이 두 위치에서 설치 합니다.

먼저 ASP.NET 라우팅 응용 프로그램의 웹 구성 파일 (web.config)에서 사용 됩니다. 라우팅과 관련 된 구성 파일에서 4 개의 섹션이 있습니다: system.web.httpModules 섹션, system.web.httpHandlers 섹션, system.webserver.modules 섹션 및 system.webserver.handlers 섹션입니다. 이 섹션에서는 없이 라우팅 더 이상 작동 하기 때문에 이러한 섹션을 삭제 하지 않도록 주의 해야 합니다.

둘째, 및 무엇 보다도 응용 프로그램의 Global.asax 파일에 경로 테이블을 만들어집니다. Global.asax 파일은 ASP.NET 응용 프로그램 수명 주기 이벤트에 대 한 이벤트 처리기를 포함 하는 특수 한 파일입니다. 경로 테이블 응용 프로그램 시작 이벤트를 사용 하는 동안 만들어집니다.

목록 1에서 파일을 ASP.NET MVC 응용 프로그램에 대 한 기본 Global.asax 파일을 포함합니다.

**1-Global.asax.vb 나열**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

MVC 응용 프로그램을 처음 시작 되 면 응용 프로그램\_start () 메서드가 호출 됩니다. 이 메서드는 차례로 RegisterRoutes() 메서드를 호출합니다. RegisterRoutes() 메서드는 경로 테이블을 만듭니다.

기본 경로 테이블 (Default 라는)를 단일 경로 포함 합니다. 기본 경로 매핑되는 URL의 첫 번째 세그먼트 컨트롤러 이름, 컨트롤러 작업에 대 한 URL의 세그먼트를 두 번째 및 세 번째 세그먼트 라는 매개 변수에 **id**합니다.

Imagine 웹 브라우저의 주소 표시줄에 다음 URL을 입력 합니다.

/ 홈/인덱스/3

기본 경로 다음 매개 변수를이 URL을 매핑합니다.

- 컨트롤러 = 홈

- 작업 = 인덱스

- id = 3

URL /Home/인덱스/3을 요청 하면 다음 코드가 실행 됩니다.

HomeController.Index(3)

기본 경로 세 매개 변수 모두에 대 한 기본값을 포함합니다. 컨트롤러를 지정 하지 않으면, 다음 컨트롤러 매개 변수 기본값 **홈**합니다. Action 매개 변수 값 작업을 지정 하지 않으면 경우 기본값으로 **인덱스**합니다. 마지막으로 id를 제공 하지 않으면 id 매개 변수 기본값은 빈 문자열입니다.

기본 경로 Url 컨트롤러 작업에 매핑하는 방법의 몇 가지 예를 살펴보겠습니다. 브라우저 주소 표시줄에 다음 URL을 입력 하는 가정해 보겠습니다.

/ 홈

기본 경로 매개 변수 기본값을 때문에이 URL을 입력 하면 HomeController 클래스의 index () 메서드를 호출할 목록 2.

**2-HomeController.vb 나열**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

목록 2 HomeController 클래스 id 라는 이름의 단일 매개 변수를 허용 하는 index () 메서드가 포함 됩니다. URL /Home는 index () 메서드가 호출 되는 값을 사용 하 여 Id 매개 변수 값으로 아무 작업도 수행 합니다.

MVC 프레임 워크 컨트롤러 작업을 호출 하는 방식으로 인해 URL /Home index () 메서드의 목록 3에서 HomeController 클래스와 일치 합니다.

**3-HomeController.vb (매개 변수가 없는 인덱스 작업)를 나열합니다.**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

보기 3의 index () 메서드는 매개 변수를 허용 하지 않습니다. URL /Home가 index () 메서드를 호출 하면 됩니다. 또한 URL /Home/인덱스/3 (Id 무시 됨)이이 메서드를 호출 합니다.

또한 URL /Home 4에서 HomeController 클래스의 index () 메서드를 찾습니다.

**4-HomeController.vb (nullable 매개 변수를 사용 하 여 인덱스 작업)를 나열합니다.**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

목록 4 index () 메서드에는 정수에 대 한 매개 변수를 하나 있습니다. 매개 변수 (값을 가질 수 Nothing) nullable 매개 변수 이기 때문에 오류가 발생 하지는 index ()는 호출할 수 있습니다.

마지막으로, URL /Home를 사용 하 여 목록 5에서 index () 메서드를 호출 하면 예외가 발생 이후 Id 매개 변수에 *아닙니다* nullable 매개 변수입니다. Index () 메서드를 호출 하려고 하면 다음 오류가 발생 하면 그림 1에 표시 합니다.

**5-HomeController.vb (Id 매개 변수를 사용 하 여 인덱스 작업)를 나열합니다.**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]


[![매개 변수 값을 필요로 하는 컨트롤러 작업을 호출 합니다.](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**그림 01**: 매개 변수 값을 필요로 하는 컨트롤러 동작 호출 ([큰 이미지를 보려면 클릭](asp-net-mvc-routing-overview-vb/_static/image2.png))


또한 목록 5에서 인덱스 컨트롤러 작업을 사용 하 여 URL /Home/인덱스/3, 다른 한편으로 잘 작동합니다. 요청 /Home/Index/3 index () 메서드를 3 값이 있는 Id 매개 변수를 사용 하 여 호출 하면 됩니다.

## <a name="summary"></a>요약

이 자습서의 목적은 ASP.NET 라우팅에 대 한 간략 한 소개를 제공 하는 것 이었습니다. 새 ASP.NET MVC 응용 프로그램을 시작 하는 기본 경로 테이블을 검사 했습니다. 기본 경로 Url 컨트롤러 작업에 매핑하는 방법 알아봅니다.

> [!div class="step-by-step"]
> [이전](creating-an-action-cs.md)
> [다음](understanding-action-filters-vb.md)
