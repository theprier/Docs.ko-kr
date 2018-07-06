---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
title: ASP.NET MVC 보기 개요 (C#) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 뷰를 무엇이 고 HTML 페이지에서와 어떻게 합니까? 이 자습서에서는 Stephen walther가 보기 소개 하 고 t 하는 방법을 보여 줍니다....
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: 152ab1e5-aec2-4ea7-b8cc-27a24dd9acb8
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: adf995529b34c84969125adcc6249ba8e22a7af4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387792"
---
<a name="aspnet-mvc-views-overview-c"></a>ASP.NET MVC 보기 개요 (C#)
====================
[Stephen walther가](https://github.com/StephenWalther)

> ASP.NET MVC 뷰를 무엇이 고 HTML 페이지에서와 어떻게 합니까? 이 자습서에서는 Stephen walther가 보기 소개 하 고 데이터 보기 및 보기 내에서 HTML 도우미 활용을 걸릴 수 있습니다 하는 방법을 보여 줍니다.


이 자습서의 목적은 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 하는 것입니다. 이 자습서를 마치면 새 보기 만들기, 보기를 컨트롤러에서 데이터를 전달 및 HTML 도우미를 사용 하 여 보기에 콘텐츠를 생성 하는 방법을 알아야 합니다.

## <a name="understanding-views"></a>뷰 이해

Active Server Pages, ASP.NET에 대 한 ASP.NET MVC 포함 되어 있지는 페이지에 직접 해당 합니다. ASP.NET MVC 응용 프로그램에서 않습니다 페이지 브라우저의 주소 표시줄에 입력 된 URL의 경로에 해당 하는 디스크. ASP.NET MVC 응용 프로그램의 페이지에 가깝습니다는 호출을 *보기*합니다.

ASP.NET MVC 응용 프로그램, 들어오는 브라우저 요청 컨트롤러 작업에 매핑됩니다. 컨트롤러 작업 보기를 반환할 수 있습니다. 그러나 컨트롤러 작업을 다른 유형의 다른 컨트롤러 작업으로 리디렉션하는 중 등의 작업을 수행할 수 있습니다.

목록 1 HomeController 라는 간단한 컨트롤러가 포함 되어 있습니다. HomeController는 index () 및 Details() 라는 두 개의 컨트롤러 작업을 표시 합니다.

**1-HomeController.cs 나열**

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample1.cs)]

브라우저 주소 표시줄에 다음 URL을 입력 하 여 첫 번째 작업, index () 작업을 호출할 수 있습니다.

/ Home/Index

브라우저에이 주소를 입력 하 여 두 번째 작업에서 Details() 작업을 호출할 수 있습니다.

/ Home/세부 정보

Index () 작업에는 뷰를 반환합니다. 사용자가 만든 대부분의 작업 보기를 반환 합니다. 그러나 작업은 다른 유형의 작업 결과 반환할 수 있습니다. 예를 들어 Details() 작업 index () 작업으로 들어오는 요청을 리디렉션하는 RedirectToActionResult를 반환 합니다.

다음 코드 줄이 줄을 포함 하는 index () 작업:

View();

이 코드 줄을 웹 서버에서 다음 경로 있어야 하는 뷰를 반환 합니다.

\Views\Home\Index.aspx

뷰에 대 한 경로 컨트롤러의 이름 및 컨트롤러 작업의 이름에서 유추 됩니다.

원하는 경우 뷰에 대 한 명시적 수 있습니다. 다음 코드 줄에 Fred 라는 뷰를 반환 합니다.

보기 (Fred);

이 코드 줄이 실행 되 면 뷰는 다음 경로에서 반환 됩니다.

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> ASP.NET MVC 응용 프로그램에 대 한 단위 테스트를 만들 계획인 경우 다음 것 뷰 이름에 대 한 명시적 이어야 하는 것이 좋습니다. 이런 방식으로 필요한 뷰 컨트롤러 작업에 의해 반환 된 확인 하기 위한 단위 테스트를 만들 수 있습니다.


## <a name="adding-content-to-a-view"></a>보기에 콘텐츠 추가

뷰는 (X) 스크립트를 포함할 수 있는 HTML 문서 표준. 스크립트를 사용 하 여 동적 콘텐츠 뷰를 추가 합니다.

예를 들어 목록 2에서 뷰는 현재 날짜 및 시간을 표시합니다.

**2-나열 \Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample2.aspx)]

목록 2에서 HTML 페이지의 본문에 다음 스크립트를 확인 합니다.

&lt;% Response.Write(DateTime.Now);%&gt;

스크립트 구분 기호를 사용할 &lt;% 및 %&gt; 스크립트의 시작과 끝을 표시 합니다. 이 스크립트는 C#으로 작성 됩니다. 브라우저에 콘텐츠를 렌더링 response.write () 메서드를 호출 하 여 현재 날짜 및 시간이 표시 됩니다. 스크립트 구분 기호 &lt;% 및 %&gt; 하나 이상의 문을 실행 하기 위해 사용할 수 있습니다.

Response.write ()를 자주 호출 되므로 Microsoft 제공 바로 가기를 사용 하 여 response.write () 메서드를 호출 합니다. 구분 기호를 사용 하는 목록 3 뷰 &lt;% = %&gt; response.write () 호출에 대 한 바로 가기로 합니다.

**Listing 3 - Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample3.aspx)]

보기에서 동적 콘텐츠를 생성 하려면 모든.NET 언어를 사용할 수 있습니다. 일반적으로 안내 컨트롤러와 보기를 쓸 Visual Basic.NET 또는 C#을 사용 합니다.

## <a name="using-html-helpers-to-generate-view-content"></a>HTML 도우미를 사용 하 여 콘텐츠 보기를 생성 합니다.

쉽게 콘텐츠 뷰를 추가 하면 활용 이라는 것을 *HTML 도우미*합니다. 일반적으로 HTML 도우미는 문자열을 생성 하는 메서드입니다. 텍스트 상자, 링크, 드롭다운 목록, 목록 상자 등 표준 HTML 요소를 생성 하려면 HTML 도우미를 사용할 수 있습니다.

예를 들어 3 명의 HTML 도우미-활용 4 뷰 BeginForm(), TextBox() 및 Password() 도우미-로그인을 생성 하려면 (그림 1 참조)를 형성 합니다.

**Listing 4 -- \Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample4.aspx)]


[![새 프로젝트 대화 상자](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)

**그림 01**: 표준 로그인 폼 ([큰 이미지를 보려면 클릭](asp-net-mvc-views-overview-cs/_static/image2.png))


HTML 도우미 메서드의 모든 뷰의 Html 속성 이라고 합니다. 예를 들어 Html.TextBox() 메서드를 호출 하 여 텍스트를 렌더링 합니다.

스크립트 구분 기호를 사용 하는 공지 &lt;% = %&gt; Html.TextBox()와 Html.Password() 도우미를 호출 하는 경우. 이러한 도우미는 단순히 문자열을 반환 합니다. 브라우저에 문자열을 렌더링 하기 위해 response.write () 호출 해야 합니다.

HTML 도우미 메서드를 사용 하는 것은 선택 사항입니다. 이러한 쉽게 HTML과 스크립트를 작성 해야 하는 양을 줄여 합니다. 목록 5에서 뷰는 HTML 도우미를 사용 하지 않고 4의 보기와 정확히 동일한 폼을 렌더링 합니다.

**Listing 5 -- \Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample5.aspx)]

사용자 고유의 HTML 도우미를 만들 수가 있습니다. 예를 들어, HTML 테이블에서 데이터베이스 레코드 집합을 자동으로 표시 하는 GridView() 도우미 메서드를 만들 수 있습니다. 이 항목에서는 자습서에서 살펴봅니다 **사용자 지정 HTML 도우미 만들기**합니다.

## <a name="using-view-data-to-pass-data-to-a-view"></a>뷰 데이터를 사용 하 여 보기로 데이터 전달

데이터 보기를 사용 하 여 컨트롤러에서 보기로 데이터를 전달 합니다. 메일을 통해 전송 되는 패키지와 같은 데이터 보기 생각할 수 있습니다. 이 패키지를 사용 하 여 컨트롤러에서 보기로 전달 된 모든 데이터를 전송 되어야 합니다. 예를 들어 목록 6의 컨트롤러 데이터를 보려면 메시지를 추가 합니다.

**6-ProductController.cs 나열**

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample6.cs)]

ViewData 속성이 컨트롤러 이름 및 값 쌍의 컬렉션을 나타냅니다. 목록 6 index () 메서드는 값이 Hello World 메시지를 명명 된 뷰 데이터 컬렉션에 항목을 추가!. 뷰는 index () 메서드에 의해 반환 되 면 뷰 데이터를 자동으로 뷰로 전달 됩니다.

7 목록 뷰 데이터 보기에서에서 메시지를 검색 하 고 브라우저에 메시지를 렌더링 합니다.

**7-나열 \Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample7.aspx)]

뷰를 활용 한다는 Html.Encode() HTML 도우미 메서드는 메시지를 렌더링할 때 알 수 있습니다. Html.Encode() HTML 도우미와 같은 특수 문자를 인코딩합니다 &lt; 고 &gt; 안전한 웹 페이지에 표시할 문자에 있습니다. 사용자가 웹 사이트에 제출 하는 콘텐츠를 렌더링할 때마다 JavaScript 주입 공격을 방지 하기 위해 콘텐츠를 인코딩해야 합니다.

(만들었기 때문에 메시지를 직접 여 ProductController에서, 우리가 인할 실제로 메시지를 인코딩하는 데 필요 합니다. 그러나는 것이 뷰 내에서 데이터 보기에서에서 검색 콘텐츠를 표시 하는 경우 항상 Html.Encode() 메서드를 호출 하는 좋은 습관입니다.)

7 목록 보기 컨트롤러에서 단순 문자열 메시지를 전달 하는 뷰 데이터를 활용을 했습니다. 다른 유형의 데이터베이스 레코드 보기 컨트롤러에서 컬렉션과 같은 데이터를 전달할 데이터 보기를 사용할 수도 있습니다. 예를 들어 데이터베이스의 컬렉션을 전달 하는 제품 데이터베이스 테이블의 내용을 보기에 표시 하려는 경우 보기에 데이터 기록 합니다.

컨트롤러에서 보기로 강력한 형식의 뷰 데이터를 전달할 수가 있습니다. 이 항목에서는 자습서에서 살펴봅니다 **이해 강력한 형식의 뷰 데이터 뷰와**합니다.

## <a name="summary"></a>요약

이 자습서는 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 합니다. 첫 번째 섹션에서는 프로젝트에 새 뷰를 추가 하는 방법을 알아보았습니다. 추가 해야 뷰 오른쪽 폴더로 특정 컨트롤러에서 호출 하기 위해 배웠습니다. 다음으로, HTML 도우미의 항목에 설명 했습니다. HTML 도우미 표준 HTML 콘텐츠를 쉽게 생성할 수 있도록 하는 방법을 배웠습니다. 마지막으로, 컨트롤러에서 보기로 데이터를 전달 하는 뷰 데이터를 활용 하는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [다음](creating-custom-html-helpers-cs.md)
