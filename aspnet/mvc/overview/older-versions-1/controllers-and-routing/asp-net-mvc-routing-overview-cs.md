---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
title: ASP.NET MVC 라우팅 개요 (C#) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen Walther ASP.NET MVC 프레임 워크 컨트롤러 작업에 브라우저 요청을 매핑하 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 5b39d2d5-4bf9-4d04-94c7-81b84dfeeb31
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: fa565d2ef253539844f5224df00bdcdc047bb3f9
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868596"
---
<a name="aspnet-mvc-routing-overview-c"></a>ASP.NET MVC 라우팅 개요 (C#)
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

> 이 자습서에서는 Stephen Walther ASP.NET MVC 프레임 워크 컨트롤러 작업에 브라우저 요청을 매핑하 하는 방법을 보여 줍니다.


이 자습서에서는 호출 하는 모든 ASP.NET MVC 응용 프로그램의 중요 한 기능을 도입 된 *ASP.NET 라우팅에서*합니다. ASP.NET 라우팅 모듈은 특정 MVC 컨트롤러 작업을 들어오는 브라우저 요청에 매핑합니다. 이 자습서의 끝으로 표준 경로 테이블 매핑되는 방법을 요청 컨트롤러 작업을 이해할 수 있습니다.

## <a name="using-the-default-route-table"></a>기본 경로 테이블을 사용 하 여

새 ASP.NET MVC 응용 프로그램을 만들 때 응용 프로그램은 이미 ASP.NET 라우팅을 사용 하도록 구성 됩니다. ASP.NET 라우팅에는 다음 두 위치에서 설치 프로그램입니다.

첫째, 응용 프로그램의 웹 구성 파일 (Web.config)에서 ASP.NET 라우팅이 사용 됩니다. 라우팅과 관련 된 구성 파일에 4 개의 섹션이: system.web.httpModules 섹션, system.web.httpHandlers 섹션, system.webserver.modules 섹션 및 system.webserver.handlers 섹션. 이 섹션에서는 없이 라우팅 더 이상 작동 하기 때문에 이러한 섹션을 삭제 하지 않도록 주의 해야 합니다.

둘째, 및 무엇 보다도 응용 프로그램의 Global.asax 파일에 경로 테이블이 만들어집니다. Global.asax 파일은 ASP.NET 응용 프로그램 수명 주기 이벤트에 대 한 이벤트 처리기를 포함 하는 특수 한 파일입니다. 경로 테이블 응용 프로그램 시작 이벤트를 사용 하는 동안 만들어집니다.

파일 목록 1의 ASP.NET MVC 응용 프로그램에 대 한 기본 Global.asax 파일을 포함합니다.

**1-Global.asax.cs 나열**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample1.cs)]

MVC 응용 프로그램 처음 시작 되 면 응용 프로그램\_start () 메서드를 호출 합니다. 이 메서드는 차례로 RegisterRoutes() 메서드를 호출합니다. RegisterRoutes() 메서드는 경로 테이블을 만듭니다.

기본 경로 테이블 (기본 이름) 단일 경로 포함 합니다. 기본 경로 매핑되는 URL의 첫 번째 세그먼트 컨트롤러 이름, 컨트롤러 작업에 대 한 URL의 두 번째 세그먼트 및 세 번째 세그먼트 라는 매개 변수를 **id**합니다.

웹 브라우저의 주소 표시줄에 다음 URL을 입력 같이 가정해 봅니다.

/ Home/Index/3

기본 경로 다음 매개 변수를이 URL을 매핑합니다.

- controller = Home

- 동작 인덱스 =

- id = 3

URL /Home/인덱스/3을 요청 하는 경우 다음 코드를 실행 됩니다.

HomeController.Index(3)

기본 경로 세 매개 변수 모두에 대 한 기본값을 포함합니다. 컨트롤러를 지정 하지 않으면, 다음은 컨트롤러 매개 변수의 기본값은 값 **홈**합니다. Action 매개 변수 값 작업을 지정 하지 않으면 경우 기본값으로 **인덱스**합니다. 마지막으로, id를 지정 하지 않으면, id 매개 변수 기본값은 빈 문자열입니다.

기본 경로 매핑되는 방법을 Url 컨트롤러 작업의 몇 가지 예를 살펴 보겠습니다. 브라우저 주소 표시줄에 다음 URL을 입력 같이 가정해 봅니다.

/ 홈

기본 경로 매개 변수 기본값 때문에이 URL을 입력 하면 HomeController 클래스의 index () 메서드를 호출할 수 있는 목록 2에서.

**2-HomeController.cs 나열**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample2.cs)]

목록 2 HomeController 클래스 id입니다. 명명 된 단일 매개 변수를 허용 하는 index () 라는 메서드를 포함 됩니다. URL /Home 하면 Id 매개 변수 값으로 빈 문자열이 있는 호출 될 index () 메서드입니다.

MVC 프레임 워크 컨트롤러 작업을 호출 하는 방식으로 인해 URL /Home는 또한 목록 3에서 HomeController 클래스의 index () 메서드와 일치 합니다.

**3-HomeController.cs (매개 변수가 없는 인덱스 작업)를 나열합니다.**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample3.cs)]

보기 3의 index () 메서드 매개 변수를 허용 하지 않습니다. URL /Home가 index () 메서드를 호출할 수 발생 합니다. 또한 URL /Home/인덱스/3 (Id 무시 됨)이이 메서드를 호출 합니다.

또한 URL /Home 목록 4에서 HomeController 클래스의 index () 메서드를 찾습니다.

**4-HomeController.cs (nullable 매개 변수와 함께 인덱스 작업)를 나열합니다.**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample4.cs)]

목록 4 index ()은 정수 예외입니다. 매개 변수 (Null 값 포함) nullable 매개 변수 이기 때문에 오류가 발생 하지는 index ()는 호출할 수 있습니다.

마지막으로 URL /Home와 목록 5에서 index () 메서드를 호출 하면 예외가 발생 Id 매개 변수 이후 *않습니다* nullable 매개 변수입니다. Index () 메서드를 호출 하려고 그림 1에 표시 된 오류를 메시지가 있습니다.

**5-HomeController.cs (Id 매개 변수 인덱스 작업)를 나열합니다.**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample5.cs)]


[![매개 변수 값을 가지는 컨트롤러 동작 호출](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)

**그림 01**: 매개 변수 값을 가지는 컨트롤러 동작 호출 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-routing-overview-cs/_static/image2.png))


또한 목록 5에서 인덱스 컨트롤러 작업으로는 URL /Home/인덱스/3, 반면에 잘 작동합니다. 요청 /Home/Index/3은 index () 호출 될 메서드를 3 값이 있는 Id 매개 변수를 사용 하면 됩니다.

## <a name="summary"></a>요약

이 자습서의 목표 ASP.NET 라우팅에 대 한 간략 한 소개를 제공 하는 것 이었습니다. 새 ASP.NET MVC 응용 프로그램으로 얻을 수 있는 기본 경로 테이블을 검사 했습니다. 기본 경로 컨트롤러 작업에 Url을 매핑합니다 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [다음](understanding-action-filters-cs.md)
