---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker 팝업 일정을 ASP.NET MV에서 사용 하는 방법의 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 572185507016afc26fc2e06ede55361b2daed277
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823753"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 편집기 템플릿, 표시 템플릿 및 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법의 기본 사항을 설명 합니다.


## <a name="adding-an-automatic-datetime-template"></a>자동 날짜/시간 서식 파일을 추가합니다.

이 자습서의 첫 번째 부분을 명시적으로 서식 지정을 지정 하려면 모델에 특성을 추가 하는 방법 및 모델을 렌더링 하는 데 사용 되는 템플릿을 명시적으로 지정 하는 방법을 살펴보았습니다. 예를 들어 합니다 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 다음 코드가 명시적으로 특성에 대 한 서식을 지정 합니다 `ReleaseDate` 속성입니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

다음 예제에서는 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 사용 하 여를 `Date` 열거형 지정 하는 날짜 사용 되는 템플릿 모델을 렌더링 하 합니다. 프로젝트에서 날짜 템플릿이 없는 경우에 기본 제공 날짜 템플릿이 사용 됩니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

그러나 ASP 합니다. MVC 형식 일치 규칙-over-configuration을 사용 하 여 형식의 이름과 일치 하는 템플릿을 검색 하 여 수행할 수 있습니다. 이렇게 하면 자동으로 모든 특성 또는 코드를 전혀 사용 하지 않고 데이터의 형식을 지정 하는 템플릿을 만들 수 있습니다. 자습서의이 부분에 대 한 형식의 모델 속성에 자동으로 적용 되는 템플릿을 만들어 [날짜/시간](https://msdn.microsoft.com/library/system.datetime.aspx)합니다. 형식의 모든 모델 속성을 렌더링 하는 템플릿을 사용 해야를 지정 하려면 특성 또는 다른 구성을 사용할 필요가 없습니다 [날짜/시간](https://msdn.microsoft.com/library/system.datetime.aspx)합니다.

또한 개별 속성 또는 개별 필드의 표시를 사용자 지정 하는 방법을 알아봅니다.

먼저 기존 서식 지정 정보를 제거 하 고 응용 프로그램의 전체 날짜를 표시 해 보겠습니다.

열기는 *Movie.cs* 파일을 주석으로 처리 합니다 `DataType` 특성을 `ReleaseDate` 속성:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

다음에 유의 합니다 `ReleaseDate` 속성 없는 서식 지정 정보를 제공 하는 경우 기본값 이기 때문에 해당 날짜와 시간을 이제 표시 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>새 템플릿 테스트에 대 한 CSS 스타일 추가

날짜 형식 지정에 대 한 서식 파일을 만들기 전에 새 템플릿에 적용할 수 있는 몇 가지 CSS 스타일 규칙을 추가 합니다. 이러한 새 템플릿 렌더링된 된 페이지를 사용 하는지 확인 하는 데 도움이 됩니다.

열기는 *Content\Site.cs*s 파일 및 파일의 맨 아래에 다음 CSS 규칙을 추가 합니다.

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>날짜/시간 표시 템플릿 추가

이제 새 템플릿을 만들 수 있습니다. 에 *Views\Movies* 폴더를 만들기는 *DisplayTemplates* 폴더입니다.

에 *Views\Shared* 폴더 만들기를 *DisplayTemplates* 폴더와 *EditorTemplates* 폴더.

표시 템플릿은 합니다 *Views\Shared\DisplayTemplates* 폴더 모든 컨트롤러에서 사용 됩니다. 표시 템플릿은 합니다 *Views\Movie\DisplayTemplates* 폴더에만 사용 됩니다는 `Movie` 컨트롤러입니다. (템플릿이 두 폴더에 이름이 같은 템플릿을 표시 하는 경우는 *Views\Movie\DisplayTemplates* 폴더-구체적인 서식 파일 즉,-반환한 보기에 대 한 우선는 `Movie` 컨트롤러.)

**솔루션 탐색기**, 확장를 *뷰* 폴더를 확장 합니다 *공유* 폴더 및 마우스 오른쪽 단추로 *Views\Shared\DisplayTemplates* 폴더입니다.

클릭 **추가** 을 클릭 한 다음 **보기**합니다. 합니다 **뷰 추가** 대화 상자가 표시 됩니다.

에 **뷰 이름** 상자에 입력 `DateTime`합니다. (형식의 이름과 일치 하기 위해이 이름을 사용 해야 합니다.)

선택 된 **부분 뷰로 만들기** 확인란 합니다. 있는지 확인 합니다 **레이아웃 또는 마스터 페이지를 사용** 및 **강력한 형식의 뷰를 만들** 확인란을 선택 하지 않은 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

**추가**를 클릭합니다. A *DateTime.cshtml* 에서 템플릿을 만든 합니다 *Views\Shared\DisplayTemplates*합니다.

다음 이미지는 *뷰* 폴더에서 **솔루션 탐색기** 후의 `DateTime` 표시 및 편집기 템플릿이 생성 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

열기는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 파일을 사용 하는 다음 태그를 추가 합니다 [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) 속성 시간 없이 날짜 서식을 지정 하는 방법입니다. (의 `{0:d}` 형식은 간단한 날짜 서식을 지정 합니다.)

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

만들려면이 단계를 반복을 `DateTime` 서식 파일에는 *Views\Movie\DisplayTemplates* 폴더입니다. 다음 코드를 사용 합니다 *Views\Movie\DisplayTemplates\DateTime.cshtml* 파일입니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` 날짜를 굵은 빨간색 텍스트로 표시를 사용 하면 CSS 클래스입니다. 추가 된 `loud-1` 이 특정 템플릿에서 사용 되는 경우 쉽게 확인할 수 있도록 임시 수단으로 바로 CSS 클래스입니다.

완료 했으면 생성 되 고 ASP.NET가 날짜를 표시 하는 데 사용할 템플릿을 사용자 지정할 수도 있습니다. 일반 템플릿 (에 *Views\Shared\DisplayTemplates* 폴더) 간단한 짧은 날짜를 표시 합니다. 템플릿을 합니다 `Movie` 컨트롤러 (에 *Views\Movies\DisplayTemplates* 폴더) 포맷 하는 간단한 날짜를 굵은 빨간색 텍스트로 표시 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 브라우저 응용 프로그램에 대 한 인덱스 뷰를 렌더링합니다.

`ReleaseDate` 속성 시간 없이 굵은 빨간색 글꼴로 이제 날짜를 표시 합니다. 이렇게 확인 하면를 `DateTime` 에서 템플릿 기반 도우미는 *Views\Movies\DisplayTemplates* 를 통해 폴더를 선택 합니다 `DateTime` 공유 폴더에서 템플릿 기반 도우미 (*Views\Shared\ DisplayTemplates*).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

이제 이름을 변경 합니다 *Views\Movies\DisplayTemplates\DateTime.cshtml* 파일을 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

이 이번에는 `ReleaseDate` 빨간색 굵게 하지 않고 시간 날짜를 표시 하는 속성입니다. 데이터의 이름을 가진 템플릿 형식 있음을 보여줍니다 (이 경우 `DateTime`)는 자동으로 해당 형식의 모든 모델 속성을 표시 하는 데 사용 됩니다. 이름을 바꾼 후는 *DateTime.cshtml* 파일을 *LoudDateTime.cshtml*, ASP.NET에서 템플릿을 찾을 수 없는 합니다 *Views\Movies\DisplayTemplates* 폴더를 사용 하므로 합니다 *DateTime.cshtml* 템플릿에서 * Views\Movies\Shared\* 폴더입니다.

(일치 하는 템플릿 이므로 대/소문자 구분, 없습니다 템플릿 파일 이름을 사용 하 여 만든 모든 대/소문자 구분 합니다. 예를 들어 *DATETIME.chstml, datetime.cshtml*, 및 *DaTeTiMe.cshtml* 일치 모든는 `DateTime` 형식입니다.)

검토 하려면:이 시점에서 `ReleaseDate` 필드를 사용 하 여 표시 되는 *Views\Movies\DisplayTemplates\DateTime.cshtml* 서식 파일을 간단한 날짜 형식을 사용 하 여 데이터를 표시 하지만 그렇지 않으면 없는 특수 형식으로 추가 합니다.

### <a name="using-uihint-to-specify-a-display-template"></a>UIHint를 사용 하 여 표시 템플릿을 지정 하려면

웹 응용 프로그램에 여러 `DateTime` 필드 및 모든 또는 대부분의 날짜 전용으로 표시 하려면 기본적으로는 *DateTime.cshtml* 템플릿은 좋은 방법입니다. 있으 나 경우 몇 가지 날짜 전체 날짜 및 시간을 표시 하 시겠습니까? 이전 버전도 계속 사용할 수 있습니다. 추가 템플릿을 만들고 사용할 수 있는 합니다 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 전체 날짜 및 시간에 대 한 서식을 지정 하는 특성입니다. 그런 다음 해당 템플릿을 선택적으로 적용할 수 있습니다. 사용할 수는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 하거나 모델 수준에서 특성에는 뷰 내에서 템플릿을 지정할 수 있습니다. 이 섹션에서는 사용 하는 방법을 볼는 `UIHint` 특성을 선택적으로 일부 인스턴스의 날짜-시간 필드에 대 한 서식 지정을 변경 합니다.

엽니다는 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* 파일 및 기존 코드를 다음으로 바꿉니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

이 표시 전체 날짜 및 시간을 사용 하면 고 녹색 크고 텍스트를 호출 하는 CSS 클래스를 추가 합니다.

열기는 *Movie.cs* 파일을 추가 합니다 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 `ReleaseDate` 속성을 다음 예와에서 같이:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

그러면 ASP.NET MVC는 표시 될 때를 `ReleaseDate` 속성 (특히 및 되지 `DateTime` 개체)를 사용 해야 합니다 *LoudDateTime.cshtml* 템플릿.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

다음에 유의 합니다 `ReleaseDate` 속성 이제 날짜와 시간을 표시는 큰 녹색 글꼴로 합니다.

돌아가서를 `UIHint` 특성을 *Movie.cs* 파일을 주석으로 처리 하므로 *LoudDateTime.cshtml* 템플릿을 사용할 수 없습니다. 응용 프로그램을 다시 실행합니다. 릴리스 날짜 크고 녹색 표시 되지 않습니다. 이 있는지 확인 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿이 인덱스 및 세부 정보 보기에 사용 됩니다.

앞에서 설명한 대로 뷰의 일부 데이터의 개별 인스턴스에 템플릿을 적용할 수 있는 템플릿을 적용할 수도 있습니다. 엽니다는 *Views\Movies\Details.cshtml* 보기. 추가 `"LoudDateTime"` 의 두 번째 매개 변수로 합니다 [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) 에 대 한 호출을 `ReleaseDate` 필드입니다. 완성된 코드는 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

이 지정 된 `LoudDateTime` 어떤 특성이 모델에 적용 되었는지에 관계 없이 모델 속성을 표시 하려면 사용 되는 템플릿.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

영화 인덱스 페이지를 사용 하는지 확인 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿 (굵은 빨간색) 및 *Movie\Details* 페이지를 사용 하는 *Views\Movies\ DisplayTemplates\LoudDateTime.cshtml* 템플릿 (크고 녹색).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

다음 섹션에서는 복합 형식에 대 한 템플릿을 만들어야 합니다.

> [!div class="step-by-step"]
> [이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
