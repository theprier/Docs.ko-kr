---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 컨트롤러 개요 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen walther가 ASP.NET MVC 컨트롤러를 소개합니다. 새 컨트롤러를 만들고 다양 한 유형의 작업 응답을 반환 하는 방법을 배웁니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: d1fa2e71ae37d9123b489511c57ae0f79c0802ff
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371780"
---
<a name="aspnet-mvc-controller-overview-vb"></a>ASP.NET MVC 컨트롤러 개요 (VB)
====================
[Stephen walther가](https://github.com/StephenWalther)

> 이 자습서에서는 Stephen walther가 ASP.NET MVC 컨트롤러를 소개합니다. 새 컨트롤러를 만들고 다양 한 유형의 작업 결과 반환 하는 방법을 알아봅니다.


이 자습서에서는 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 작업 결과의 항목을 살펴봅니다. 이 자습서를 완료 한 후에 컨트롤러 방문자는 ASP.NET MVC 웹 사이트와 상호 작용 하는 방식을 제어를 사용 하는 방법을 이해할 수 있습니다.

## <a name="understanding-controllers"></a>컨트롤러의 이해

MVC 컨트롤러는 ASP.NET MVC 웹 사이트에 대해 수행 된 요청에 응답 하는 것에 대 한 책임이 있습니다. 각 브라우저 요청을 특정 컨트롤러에 매핑됩니다. 예를 들어 브라우저의 주소 표시줄에 다음 URL을 입력 하는 가정해 보겠습니다.

`http://localhost/Product/Index/3`

이 경우 ProductController 라는 컨트롤러가 호출 됩니다. ProductController는 브라우저 요청에 대 한 응답을 생성 하는 일을 담당 합니다. 예를 들어 컨트롤러 브라우저로 특정 보기를 반환할 수 있습니다 또는 컨트롤러 다른 컨트롤러에 사용자를 리디렉션할 수 있습니다.

목록 1 ProductController 라는 간단한 컨트롤러가 포함 되어 있습니다.

**Listing1 - Controllers\ProductController.vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

목록 1에서 보듯이 컨트롤러 클래스 (Visual Basic.NET 또는 C# 클래스)만 됩니다. 컨트롤러는 기본 System.Web.Mvc.Controller 클래스에서 파생 된 클래스입니다. 컨트롤러를 몇 가지 유용한 메서드를 무료로 상속 컨트롤러를이 기본 클래스에서 상속 하기 때문에 (에서는 이러한 메서드에 대해 잠시 후에).

## <a name="understanding-controller-actions"></a>컨트롤러 작업 이해

컨트롤러는 컨트롤러 작업을 노출합니다. 작업을 사용 하면 브라우저 주소 표시줄에서 특정 URL을 입력 하면 호출 되는 컨트롤러의 메서드입니다. 예를 들어 다음 URL에 대 한 요청을 수행 하는 가정해 보겠습니다.

`http://localhost/Product/Index/3`

이 예에서 index () 메서드는 ProductController 클래스에서 호출 됩니다. Index () 메서드는 컨트롤러 동작의 예입니다.

컨트롤러 동작을 컨트롤러 클래스의 공용 메서드여야 합니다. 기본적으로 visual Basic.NET 메서드는 공용 메서드. 컨트롤러 클래스에 추가한 모든 public 메서드를 컨트롤러 작업으로 자동으로 노출 된다는 것을 실현 (않도록 주의 해야이 대 한 브라우저 주소 표시줄에 올바른 URL을 입력 하면 universe의 모든 사용자가 컨트롤러 작업을 호출할 수 있습니다 때문).

컨트롤러 작업에 의해 충족 되어야 하는 몇 가지 추가 요구 사항이 있습니다. 컨트롤러 작업으로 사용 된 메서드를 오버 로드할 수 없습니다. 또한 컨트롤러 작업에는 정적 메서드 수 없습니다. 이외에 컨트롤러 작업으로 거의 모든 메서드를 사용할 수 있습니다.

## <a name="understanding-action-results"></a>작업 결과 이해

컨트롤러 작업 반환 이라는 것을 *작업 결과*합니다. 작업 결과 브라우저 요청에 대 한 응답에서 컨트롤러 작업을 반환 하는 항목입니다.

ASP.NET MVC 프레임 워크는 여러 유형의 작업 결과 포함 하 여 지원 합니다.

1. ViewResult-나타내는 HTML 및 태그입니다.
2. EmptyResult-없는 결과를 나타냅니다.
3. 된 RedirectResult-새 URL로 리디렉션을 나타냅니다.
4. JsonResult-AJAX 응용 프로그램에서 사용할 수 있는 JavaScript Object Notation 결과를 나타냅니다.
5. JavaScriptResult-JavaScript 스크립트를 나타냅니다.
6. ContentResult-텍스트 결과를 나타냅니다.
7. FileContentResult-은 다운로드 가능한 파일을 (이진 콘텐츠)를 나타냅니다.
8. FilePathResult-다운로드 한 파일을 (경로로)를 나타냅니다.
9. FileStreamResult-다운로드 한 파일을 (파일 스트림과)를 나타냅니다.

이러한 작업 결과의 모든 기본 ActionResult 클래스에서 상속합니다.

대부분의 경우 컨트롤러 작업을 ViewResult를 반환합니다. 예를 들어 인덱스 컨트롤러 작업 목록 2에서는 ViewResult를 반환합니다.

**2-Controllers\BookController.vb 나열**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

액션을 ViewResult 반환 될 때 HTML 브라우저에 반환 됩니다. 목록 2에서 index () 메서드는 브라우저에 인덱스를 명명 된 뷰를 반환 합니다.

목록 2에서 index () 작업을 ViewResult() 반환 하지 않음을 알 수 있습니다. 대신, 기본 컨트롤러 클래스의 View() 메서드 호출 됩니다. 일반적으로 작업 결과 직접 돌아가지 않으면. 대신, 호출 기본 컨트롤러 클래스의 다음 메서드 중 하나:

1. 보기-ViewResult 작업 결과 반환 합니다.
2. 리디렉션-된 RedirectResult 작업 결과 반환 합니다.
3. RedirectToAction-RedirectToRouteResult 작업 결과 반환 합니다.
4. RedirectToRoute-RedirectToRouteResult 작업 결과 반환 합니다.
5. Json-JsonResult 작업 결과 반환 합니다.
6. JavaScriptResult-JavaScriptResult를 반환 합니다.
7. 콘텐츠-ContentResult 작업 결과 반환 합니다.
8. 파일-반환 FileContentResult, FilePathResult, 또는 매개 변수에 따라 FileStreamResult 메서드에 전달 합니다.

따라서 브라우저에 뷰를 반환 하려는 경우에 View() 메서드를 호출 합니다. 다른 하나의 컨트롤러 작업에서 사용자를 리디렉션하 하려는 경우 RedirectToAction() 메서드를 호출 합니다. 예를 들어 목록 3에서 Details() 작업으로 표시 또는 Id 매개 변수 값에 있는지 여부에 따라 index () 작업에 사용자를 리디렉션합니다.

**3-CustomerController.vb 나열**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

ContentResult 작업 결과은 특별 합니다. 일반 텍스트로 된 작업 결과를 반환할 ContentResult 작업 결과 사용할 수 있습니다. 예를 들어, 4에서 index () 메서드는 일반 텍스트와 HTML 아니라 메시지를 반환합니다.

**4-Controllers\StatusController.vb 나열**

> StatusController
> 
> 
> System.Web.Mvc.Controller


[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

StatusController.Index() 작업이 호출 되 면 뷰를 반환 되지 않습니다. 대신 원시 텍스트 "Hello World!" 브라우저에 반환 됩니다.

컨트롤러 작업 결과 작업 결과 없습니다-예를 들어, 날짜 또는-정수를 반환 하는 경우 다음 결과에 래핑됩니다 ContentResult를 자동으로. 예를 들어, index () 작업 목록 5에서 WorkController 호출 되 면 날짜도 반환 됩니다 ContentResult를 자동으로.

**5-WorkController.vb 나열**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

목록 5에서 index () 작업에는 DateTime 개체를 반환합니다. ASP.NET MVC 프레임 워크 DateTime 개체를 문자열로 변환 하 고는 ContentResult에 DateTime 값을 자동으로 래핑합니다. 브라우저에는 날짜 및 시간을 일반 텍스트로 받습니다.

## <a name="summary"></a>요약

이 자습서의 목적은 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 컨트롤러 작업 결과의 개념을 소개 하는 것 이었습니다. 첫 번째 섹션에서는 ASP.NET MVC 프로젝트에 새 컨트롤러를 추가 하는 방법을 알아보았습니다. 다음으로, 컨트롤러의 메서드를 공개 하는 방법을 알아보았습니다 우주 컨트롤러 작업으로 노출 됩니다. 마지막으로, 다양 한 컨트롤러 작업에서 반환 될 수 있는 작업 결과 설명 했습니다. 특히 ViewResult 고 RedirectToActionResult, ContentResult 컨트롤러 작업에서 반환 하는 방법에 설명 했습니다.

> [!div class="step-by-step"]
> [이전](creating-a-custom-route-constraint-cs.md)
> [다음](creating-custom-routes-vb.md)
