---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC 뷰 개요 (VB) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 뷰 란 무엇이 고 어떻게 다른 것 일까요 HTML 페이지에서? 이 자습서에서는 Stephen Walther에서는 보기에 소개 하 고 t 하는 방법을 보여 줍니다. 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a64c70851d13b923964dfd1cf3bad55612ae0d0f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-mvc-views-overview-vb"></a>ASP.NET MVC 뷰 (VB) 개요
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC 뷰 란 무엇이 고 어떻게 다른 것 일까요 HTML 페이지에서? 이 자습서에서는 Stephen Walther 보기에 소개 하 고 있습니다 사용할 수 있는 방법을 데이터 보기와 보기 내에서 HTML 도우미 보여 줍니다.


이 자습서의 목적은 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 하는 것입니다. 이 자습서를 마치면 하 여 새 보기를 만들 컨트롤러에서 뷰로 데이터를 전달 하 고 콘텐츠를 생성 하는 뷰에서 HTML 도우미를 사용 하는 방법을 이해 해야 합니다.

## <a name="understanding-views"></a>뷰 이해

ASP.NET 또는 Active Server Pages 달리 ASP.NET MVC는 제외 페이지에 직접 해당 하는 아무 것도 됩니다. ASP.NET MVC 응용 프로그램 즉 하지 페이지를 브라우저의 주소 표시줄에 입력 하는 URL의 경로에 해당 하는 디스크에 있습니다. ASP.NET MVC 응용 프로그램의 페이지에 가깝습니다 리 라는 *보기*합니다.

ASP.NET MVC 응용 프로그램에서 들어오는 브라우저 요청 컨트롤러 작업에 매핑됩니다. 컨트롤러 작업 보기를 반환할 수 있습니다. 그러나 컨트롤러 작업이 일부 다른 형식의 다른 컨트롤러 작업 리디렉션됩니다 등의 작업을 수행할 수 있습니다.

목록 1 HomeController 라는 간단한 컨트롤러를 포함 합니다. HomeController는 index () 및 Details() 라는 두 개의 컨트롤러 작업을 노출 합니다.

**1-HomeController.vb 나열**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

브라우저 주소 표시줄에 다음 URL을 입력 하 여 첫 번째 동작인 index () 작업을 호출할 수 있습니다.

/ Home/Index

브라우저에이 주소를 입력 하 여 두 번째 작업에서 Details() 동작을 호출할 수 있습니다.

/ Home/세부 정보

Index () 작업 뷰를 반환 합니다. 만드는 대부분의 동작 뷰를 반환 합니다. 그러나 작업은 다른 유형의 작업 결과 반환할 수 있습니다. 예를 들어 Details() 작업 index () 작업으로 들어오는 요청을 리디렉션하는 RedirectToActionResult를 반환 합니다.

Index () 작업에 다음 줄을의 코드 포함 되어 있습니다.

View()

이 코드 줄을 웹 서버에서 다음 경로에 있어야 하는 뷰를 반환 합니다.

\Views\Home\Index.aspx

뷰에 대 한 경로 컨트롤러의 이름 및 컨트롤러 동작의 이름에서 유추 됩니다.

원하는 경우 뷰에 대 한 명시적을 할 수 있습니다. 다음 코드 줄 Fred 이라는 뷰를 반환 합니다.

보기 (Fred)

이 줄의 코드를 실행 하면 다음 경로에서 뷰 반환 됩니다.

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> ASP.NET MVC 응용 프로그램에 대 한 단위 테스트를 만들려고 계획 하는 경우 다음 이기 뷰 이름에 대 한 명시적으로 지정 해야 하는 것이 좋습니다. 이런 방식으로 예상된 보기 컨트롤러 동작에 의해 반환 된 것을 확인 하는 단위 테스트를 만들 수 있습니다.


## <a name="adding-content-to-a-view"></a>콘텐츠 뷰를 추가

뷰는 (스크립트를 포함할 수 있는 HTML 문서 X) 표준입니다. 스크립트를 사용 하 여 동적 콘텐츠 보기에 추가 합니다.

예를 들어 목록 2는 보기는 현재 날짜 및 시간을 표시합니다.

**Listing 2 - \Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

다음 스크립트는 목록 2에 있는 HTML 페이지의 본문에 포함 되어 있는지 확인 합니다.

&lt;% Response.Write(DateTime.Now)%&gt;

스크립트 구분 기호를 사용 하 여 &lt;% 및 %&gt; 스크립트의 시작과 끝을 표시 합니다. 이 스크립트는 Visual basic로 작성 됩니다. 내용을 브라우저에 렌더링 하 Response.Write() 메서드를 호출 하 여 현재 날짜 및 시간을 표시 합니다. 스크립트 구분 기호 &lt;% 및 %&gt; 는 하나 이상의 문을 실행 하는 데 사용할 수 있습니다.

Response.Write()를 자주 호출할 수 있으므로 Microsoft 제공 바로 가기를 Response.Write() 메서드를 호출 합니다. 목록 3에서 보기의 구분 기호를 사용 하 여 &lt;% = %&gt; Response.Write() 호출에 대 한 바로 가기로 합니다.

**Listing 3 - Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

동적 콘텐츠 보기에서 생성 하는 모든.NET 언어를 사용할 수 있습니다. 일반적으로 ll 있습니다 컨트롤러와 뷰를 작성 하 Visual Basic.NET 또는 C#을 사용 합니다.

## <a name="using-html-helpers-to-generate-view-content"></a>HTML 도우미를 사용 하 여 콘텐츠 보기를 생성 합니다.

콘텐츠 뷰를 추가할 좀 더 쉽게 있습니다 활용할 수 라는 것는 *HTML 도우미*합니다. HTML 도우미, 문자열을 생성 하는 메서드를 일반적으로 합니다. 텍스트 상자, 링크, 드롭다운 목록, 목록 상자와 같은 표준 HTML 요소를 생성 하려면 HTML 도우미를 사용할 수 있습니다.

예를 들어 3 명의 HTML 도우미-활용 목록 4에서에서 보기 BeginForm(), TextBox() 및 Password() 도우미-로그인을 생성 하려면 (그림 1 참조)을 형성 합니다.

**Listing 4 -- \Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]


[![새 프로젝트 대화 상자](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**그림 01**: 표준 로그인 폼 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-views-overview-vb/_static/image2.png))


뷰의 Html 속성에서 모든 HTML 도우미 메서드를 호출 합니다. 예를 들어 Html.TextBox() 메서드를 호출 하 여 텍스트 상자를 렌더링 합니다.

스크립트 구분 기호를 사용 하는 알림 &lt;% = %&gt; Html.TextBox()와 Html.Password() 도우미를 호출할 때입니다. 이러한 도우미 클래스는 단순히 문자열을 반환 합니다. 브라우저에 문자열을 렌더링 하는 데 Response.Write()를 호출 해야 합니다.

HTML 도우미 메서드를 사용 하는 것은 선택 사항입니다. 쉽게 단순화 하 여 HTML 및 스크립트를 작성 해야 하는 양이 줄어듭니다. 목록 5에서 보기는 HTML 도우미를 사용 하지 않고 목록 4의 보기와 정확히 같은 폼을 렌더링 합니다.

**Listing 5 -- \Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

사용자 고유의 HTML 도우미를 만들을 수도 있습니다. 예를 들어 HTML 테이블에 데이터베이스 레코드 집합을 자동으로 표시 하는 GridView() 도우미 메서드를 만들 수 있습니다. 자습서의이 항목을 탐색 **사용자 지정 HTML 도우미 만들기**합니다.

## <a name="using-view-data-to-pass-data-to-a-view"></a>데이터 보기를 사용 하 여 데이터를 전달 하는 보기

데이터 보기를 사용 하 여 보기에는 컨트롤러에서 데이터를 전달 합니다. 메일을 통해 전송 하는 패키지와 같이 데이터 보기 생각할 수 있습니다. 이 패키지를 사용 하 여 보기에는 컨트롤러에서 전달 된 모든 데이터를 전송 되어야 합니다. 예를 들어 컨트롤러 목록 6에 데이터를 보려면 메시지를 추가 합니다.

**6-ProductController.vb 나열**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

컨트롤러 ViewData 속성 이름 / 값 쌍의 컬렉션을 나타냅니다. 목록 6 index () 메서드는 Hello World 값으로 메시지를 명명 된 뷰 데이터 컬렉션에 항목을 추가!입니다. 보기는 index () 메서드에 의해 반환 되 면 뷰 데이터 보기를 자동으로 전달 됩니다.

보기 목록 7의 데이터 보기에서에서 메시지를 검색 하 고 브라우저에 메시지를 렌더링 합니다.

**Listing 7 -- \Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

확인 메시지를 렌더링 하는 경우 보기에서는 Html.Encode() HTML 도우미 메서드를 활용 합니다. Html.Encode() HTML 도우미와 같은 특수 문자를 인코딩합니다 &lt; 및 &gt; 웹 페이지에 표시 하기에 안전한 문자로 합니다. 사용자가 웹 사이트에 전송 하는 콘텐츠를 렌더링할 때마다 JavaScript 주입 공격을 방지 하기 위해 콘텐츠를 인코딩해야 합니다.

(메시지 직접에서 만든는 ProductController, 때문에 여기서 인할 실제로 메시지를 인코딩하는 데 필요 합니다. 그러나이 뷰 내의 데이터 보기에서에서 검색 콘텐츠를 표시 하는 경우 항상 Html.Encode() 메서드를 호출 하는 좋은 습관입니다.)

목록 7에서의 순서로 보기 데이터를 보기에 컨트롤러에서 간단한 문자열 메시지를 전달 합니다. 다른 보기에는 컨트롤러에서 데이터베이스 레코드의 컬렉션과 같은 데이터 형식을 전달 하려면 데이터 보기를 사용할 수도 있습니다. 예를 들어 데이터베이스의 컬렉션을 전달 하는 다음 제품 데이터베이스 테이블의 내용을 보기에 표시 하려는 경우 보기에 데이터 기록 합니다.

또한 보기를 컨트롤러에서 강력한 형식의 뷰 데이터를 전달 하는 옵션도 있습니다. 자습서의이 항목을 탐색 **이해 강력한 형식의 뷰 데이터와 뷰**합니다.

## <a name="summary"></a>요약

이 자습서에는 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공합니다. 첫 번째 섹션에서는 프로젝트에 새 보기를 추가 하는 방법을 알아보았습니다. 특정 컨트롤러에서 호출 하기 위해 뷰를 추가에 적합 한 폴더 해야 한다고 설명 했습니다. 다음으로, HTML 도우미의 주제에 설명 했습니다. HTML 도우미 표준 HTML 콘텐츠를 쉽게 생성할 수 있도록 방법을 배웠습니다. 마지막으로, 보기에는 컨트롤러에서 데이터를 전달 하는 뷰 데이터를 활용 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](passing-data-to-view-master-pages-cs.md)
> [다음](creating-custom-html-helpers-vb.md)
