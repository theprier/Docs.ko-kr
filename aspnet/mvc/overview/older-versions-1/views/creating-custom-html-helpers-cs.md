---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 사용자 지정 HTML 도우미 (C#) 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다. HTML 도우미를 활용 하면...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: ebc9aa2aa8dbc02dc01833d671c3bfd19141ba74
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-custom-html-helpers-c"></a>사용자 지정 HTML 도우미 (C#) 만들기
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> 이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다. HTML 도우미 활용 함으로써 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력의 양을 줄일 수 있습니다.


이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다. HTML 도우미 활용 함으로써 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력의 양을 줄일 수 있습니다.

이 자습서의 첫 번째 부분에서 설명 기존 ASP.NET MVC 프레임 워크에 포함 된 HTML 도우미 중 일부입니다. 다음으로, 사용자 지정 HTML 도우미를 작성 하는 두 가지 방법 설명: 정적 메서드를 작성 하 고 확장 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 설명할 합니다.

## <a name="understanding-html-helpers"></a>HTML 도우미 이해

HTML 도우미는 문자열을 반환 하는 메서드입니다. 문자열에는 모든 유형의 원하는 콘텐츠를 나타낼 수 있습니다. 예를 들어 HTML와 같은 표준 HTML 태그를 렌더링할 HTML 도우미를 사용할 수 있습니다 `<input>` 및 `<img>` 태그입니다. 탭 스트립 또는 데이터베이스 데이터의 HTML 테이블 등의 보다 복잡 한 콘텐츠를 렌더링할 HTML 도우미를 사용할 수도 있습니다.

ASP.NET MVC 프레임 워크에는 다음과 같은 표준 HTML 도우미 (이것은 전체 목록이 아님) 집합이 포함 됩니다.

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropDownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

폼 목록 1의 예로 들 수 있습니다. 이 양식은 두 (그림 1 참조)는 표준 HTML 도우미를 사용 하 여 렌더링 됩니다. 이 양식에서 사용 하 여 `Html.BeginForm()` 및 `Html.TextBox()` 양식을 렌더링 하는 간단한 HTML 도우미 메서드.


[![HTML 도우미를 사용 하 여 페이지 렌더링](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**그림 01**: HTML 도우미를 사용 하 여 페이지 렌더링 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image3.png))


**1 – 나열 `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

열기 및 닫기 HTML을 만들기 위해 Html.BeginForm() 도우미 메서드는 `<form>` 태그입니다. 다음에 유의 `Html.BeginForm()` using 내에서 메서드는 문입니다. 문을 사용 하면는 `<form>` 태그를 사용 하 여 끝에 닫힐 블록입니다.

사용 하 여 만드는 대신 선호 하는 경우 블록을 닫는 Html.EndForm() 도우미 메서드를 호출할 수 있습니다는 `<form>` 태그입니다. 여는 만들기 및 닫기에 어떤 방법을 사용 하 여 `<form>` 가장 직관적으로 보이는 태그입니다.

`Html.TextBox()` 도우미 메서드 목록 1의 HTML을 렌더링 하는 데 사용 됩니다 `<input>` 태그입니다. 선택 하면 소스 보기 브라우저에서 목록 2의 HTML 소스를 참조 합니다. 소스 표준 HTML 태그가 포함 되어 있는지 확인 합니다.

> [!IMPORTANT]
> 에 `Html.TextBox()`HTML 도우미와 함께 렌더링 된 `<%= %>` 대신 태그 `<% %>` 태그입니다. 등호 기호를 포함 하지 않는 경우 브라우저에 렌더링 가져옵니다 nothing입니다.

ASP.NET MVC 프레임 워크 도우미 중 작은 부분만 포함 되어 있습니다. 대부분의 경우 사용자 지정 HTML 도우미와 MVC 프레임 워크를 확장 해야 합니다. 이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 작성 하는 두 가지 방법에 설명 합니다.

**2 – 나열 `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>정적 메서드를 사용 하 여 HTML 도우미 만들기

새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 정적 메서드를 만드는 것입니다. 한다고 가정, 예를 들어 HTML을 렌더링 하는 새 HTML 도우미 만들려는 `<label>` 태그입니다. 목록 2 클래스를 사용 하 여 렌더링 하는 수는 `<label>` 합니다.

**2 – 나열 `Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

목록 2의 클래스에 대 한 특별 한 일은 없습니다. `Label()` 메서드는 단순히 문자열을 반환 합니다.

목록 3에서 수정 된 인덱스 뷰를 사용 하는 `LabelHelper` HTML을 렌더링 하 `<label>` 태그입니다. 공지 보기를 포함 하는 `<%@ imports %>` 가져오는 지시문의 `Application1.Helpers` 네임 스페이스입니다.

**2 – 나열 `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>확장 메서드를 사용 하 여 HTML 도우미 만들기

만들려는 경우에 작동 하는 HTML 도우미 확장 메서드를 만들어야 하는 다음 ASP.NET MVC 프레임 워크에 포함 된 표준 HTML 도우미 같은입니다. 확장 메서드를 사용 하 여 기존 클래스에 새 메서드를 추가할 수 있습니다. HTML 도우미 메서드를 만들 때 뷰의 Html 속성으로 표현 HtmlHelper 클래스에 새 메서드를 추가 합니다.

확장 메서드를 추가 하는 보기 3의 클래스는 `HtmlHelper` 라는 클래스 `Label()`합니다. 이 클래스에 대 한 주의 해야 하는 것의 두 가지가 있습니다. 첫째, 클래스는 정적 클래스 인지 확인 합니다. 정적 클래스와 확장 메서드를 정의 해야 합니다.

둘째, 알 수 있듯이 첫 번째 매개 변수에 `Label()` 메서드 키워드에 의해 앞 `this`합니다. 확장 메서드의 첫 번째 매개 변수는 확장 메서드를 확장 하는 클래스를 나타냅니다.

**3 – 나열 `Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

확장 메서드 같은 모든 클래스의 다른 메서드에서 Visual Studio Intellisense에 표시 되는 확장 메서드를 만들고 응용 프로그램을 성공적으로 작성 한 후 (그림 2 참조). 유일한 차이점은 해당 확장 메서드는 특수 기호가 옆에 (아래쪽 화살표 아이콘)와 함께 표시 합니다.


[![Html.Label() 확장 메서드를 사용 하 여](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**그림 02**: Html.Label() 확장 메서드를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image6.png))


수정한 인덱스 뷰 목록 4에서의 모든 렌더링를 Html.Label() 확장 메서드를 사용 하 여 해당 `<label>` 태그입니다.

**4 – 나열 `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>요약

이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 살펴보았습니다. 사용자 지정을 만드는 방법을 배웠습니다 먼저 `Label()` 정적 메서드를 만들어 HTML 도우미는 문자열을 반환 합니다. 다음으로, 사용자 지정을 만드는 방법을 배웠습니다 `Label()` 에 확장 메서드를 만들어 HTML 도우미 메서드는 `HtmlHelper` 클래스입니다.

이 자습서에서는 매우 간단한 HTML 도우미 메서드는 구축에 집중 합니다. 참고로, 하는 HTML 도우미는 원하는 만큼 복잡 해질 수 있습니다. 트리 뷰, 메뉴 또는 데이터베이스 데이터 테이블 같은 풍부한 콘텐츠를 렌더링 하는 HTML 도우미를 작성할 수 있습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-views-overview-cs.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
