---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: "ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MV에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 271c244ab0b9e2524a33ea6ff4d41893ce22472f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.


## <a name="adding-an-automatic-datetime-template"></a>자동 DateTime 템플릿 추가

이 자습서의 첫 번째 부분을 명시적으로 서식을 지정 하려면 모델에 특성을 추가할 수 및 모델을 렌더링 하는 데 사용 하는 템플릿을 명시적으로 지정 하는 방법을 살펴보았습니다. 예를 들어는 [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 에 다음 코드 명시적 특성에 대 한 서식을 지정는 `ReleaseDate` 속성입니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

다음 예제에서는 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 사용 하는 `Date` 열거형, 모델을 렌더링 하는 날짜 템플릿을 쓰일 수를 지정 합니다. 프로젝트에서 date 템플릿이 없는 경우 기본 제공 된 날짜 템플릿이 사용 됩니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

그러나 ASP 합니다. MVC 형식 일치 규칙-조치-구성 형식의 이름을 일치 하는 템플릿을 검색 하 여 사용 하 여 수행할 수 있습니다. 이렇게 하면 자동으로 모든 특성이 나 코드를 전혀 사용 하지 않고 데이터의 형식을 지정 하는 템플릿을 만들 수 있습니다. 자습서의이 부분에 대 한 형식의 모델 속성에 자동으로 적용 되는 템플릿을 만듭니다 [DateTime](https://msdn.microsoft.com/en-us/library/system.datetime.aspx)합니다. 형식의 모든 모델 속성을 렌더링 하는 템플릿 쓰일 수를 지정 하는 특성 또는 다른 구성을 사용할 필요가 없습니다 [DateTime](https://msdn.microsoft.com/en-us/library/system.datetime.aspx)합니다.

또한 개별 속성 또는 개별 필드의 표시를 사용자 지정 하는 방법을 알아봅니다.

를 시작 하려면 기존 서식 지정 정보를 제거 하 고 응용 프로그램의 전체 날짜 표시 살펴보겠습니다.

열기는 *Movie.cs* 파일을 주석으로 처리는 `DataType` 특성에 `ReleaseDate` 속성:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

에 `ReleaseDate` 속성 없는 서식 지정 정보를 제공 하는 경우 기본값 이기 때문에 해당 날짜와 시간을 이제 표시 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>새 서식 파일을 테스트 하기 위한 CSS 스타일을 추가 합니다.

날짜 형식 지정에 대 한 템플릿을 만들기 전에 새 템플릿을 적용할 수 있는 몇 가지 CSS 스타일 규칙을 추가 합니다. 이러한 렌더링된 된 페이지는 새 템플릿을 사용 하 고 있는지 확인 하는 데 도움이 됩니다.

열기는 *Content\Site.cs*s 파일을 파일의 맨 아래에 다음과 같은 CSS 규칙을 추가 합니다.

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>날짜/시간 표시 템플릿 추가

이제 새 서식 파일을 만들 수 있습니다. 에 *Views\Movies* 폴더를 만들는 *DisplayTemplates* 폴더입니다.

에 *Views\Shared* 폴더를 만들는 *DisplayTemplates* 폴더 및 *EditorTemplates* 폴더입니다.

표시 템플릿은 *Views\Shared\DisplayTemplates* 폴더 모든 컨트롤러에서 사용 됩니다. 표시 템플릿은 *Views\Movie\DisplayTemplates* 폴더에만 사용 됩니다는 `Movie` 컨트롤러입니다. (동일한 이름의 템플릿이 두 폴더에서 서식 파일에 표시 되 면는 *Views\Movie\DisplayTemplates* 폴더-즉, 더 구체적인 서식 파일-에서 반환 된 뷰에 대 한 우선는 `Movie` 컨트롤러입니다.)

**솔루션 탐색기**를 확장 하 고는 *뷰* 폴더를 확장 하 고는 *Shared* 폴더를 마우스 오른쪽 단추로 *Views\Shared\DisplayTemplates* 폴더입니다.

클릭 **추가** 클릭 하 고 **보기**합니다. **뷰 추가** 대화 상자가 표시 됩니다.

에 **뷰 이름** 상자에서 입력 `DateTime`합니다. (형식의 이름을 찾을 수 있도록이 이름을 사용 해야 합니다.)

선택 된 **부분 뷰로 만들기** 확인란 합니다. 다음 사항을 확인는 **레이아웃 또는 마스터 페이지를 사용 하 여** 및 **강력한 형식의 뷰 만들기** 확인란을 선택 하지 않은 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

**추가**를 클릭합니다. A *DateTime.cshtml* 템플릿이에 생성 되는 *Views\Shared\DisplayTemplates*합니다.

다음 그림에서는 *뷰* 폴더에 **솔루션 탐색기** 후는 `DateTime` 표시 및 편집기 템플릿은 만들어집니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

열기는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 파일을 사용 하 여 다음 태그를 추가 [String.Format](https://msdn.microsoft.com/en-us/library/system.string.format.aspx) 메서드는 시간을 제외한 날짜가으로 속성을 지정 하려면. (의 `{0:d}` 형식은 간단한 날짜 서식을 지정 합니다.)

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

이 단계를 반복 만듭니다는 `DateTime` 에서 서식 파일의 *Views\Movie\DisplayTemplates* 폴더. 다음 코드를 사용 하 여는 *Views\Movie\DisplayTemplates\DateTime.cshtml* 파일입니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` CSS 클래스 때문에 해당 날짜가 굵은 빨간색 텍스트로 표시 되도록 합니다. 추가한는 `loud-1` 이 특정 템플릿이 사용 되는 경우 쉽게 확인할 수 있도록은 임시 방책와 마찬가지로 CSS 클래스입니다.

완료 했으면 생성 되 고 사용자 지정 된 날짜를 표시 하도록 ASP.NET에서 사용할 템플릿. 보다 일반적인 서식 파일 (에 *Views\Shared\DisplayTemplates* 폴더) 단순 하 고 간단한 날짜를 표시 합니다. 서식 파일을 대상으로 `Movie` 컨트롤러 (에 *Views\Movies\DisplayTemplates* 폴더) 포맷 하 고 간단한 날짜를 굵은 빨간색 텍스트로 표시 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 브라우저 응용 프로그램에 대 한 인덱스 뷰를 렌더링 합니다.

`ReleaseDate` 속성 이제는 시간을 제외한 굵은 빨간색 글꼴로 날짜를 표시 합니다. 이렇게 하면 확인는 `DateTime` 에서 템플릿 기반 도우미는 *Views\Movies\DisplayTemplates* 통해 폴더를 선택는 `DateTime` 공유 폴더에서 템플릿 기반 도우미 (*Views\Shared\ DisplayTemplates*).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

이름을 바꿀는 *Views\Movies\DisplayTemplates\DateTime.cshtml* 파일을 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

이 현재는 `ReleaseDate` 속성 시간 및 굵은 빨간색 글꼴로 없는 날짜를 표시 합니다. 데이터의 이름이 있는 서식 파일을 입력할 들 (이 경우 `DateTime`) 자동으로 해당 형식의 모든 모델 속성을 표시 하는 데 사용 됩니다. 이름을 바꾼 후는 *DateTime.cshtml* 파일을 *LoudDateTime.cshtml*, ASP.NET에는 더 이상에서 템플릿을 찾을 수는 *Views\Movies\DisplayTemplates* 있으므로 사용할 폴더 *DateTime.cshtml* 에서 서식 파일은 * Views\Movies\Shared\* 폴더입니다.

(일치 하는 서식 파일 이므로 대/소문자 구분을 만들 수는 템플릿 파일 이름 모두 대/소문자. 예를 들어 *DATETIME.chstml, datetime.cshtml*, 및 *DaTeTiMe.cshtml* 모두 일치는 `DateTime` 유형입니다.)

검토 하려면:이 시점에서 `ReleaseDate` 필드를 사용 하 여 표시 되는 *Views\Movies\DisplayTemplates\DateTime.cshtml* 템플릿을 간단한 날짜 서식을 사용 하 여 데이터를 표시 하지만 그렇지 않은 경우 추가 하는 특별 한 형식이 적용 되지 않습니다.

### <a name="using-uihint-to-specify-a-display-template"></a>UIHint를 사용 하 여 디스플레이 템플릿을 지정 하려면

웹 응용 프로그램에 많은 경우 `DateTime` 필드 전체 또는 대부분의 날짜 전용으로 표시 하려면 기본적으로는 *DateTime.cshtml* 서식 파일에 있는 좋은 방법입니다. 하지만 훨씬 쉽게 몇 가지 날짜 전체 날짜 및 시간을 표시 하 시겠습니까? 이전 버전도 계속 사용할 수 있습니다. 추가 템플릿을 만들고 사용 하는 [UIHint](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 전체 날짜 및 시간에 대 한 서식을 지정 하는 특성입니다. 그런 다음 해당 템플릿을 선택적으로 적용할 수 있습니다. 사용할 수는 [UIHint](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 이거나 모델 수준에서 특성 보기 내 파일을 지정할 수 있습니다. 이 섹션에 사용 하는 방법을 표시 됩니다는 `UIHint` 특성을 선택적으로 날짜-시간 필드의 일부 인스턴스에 대 한 서식을 변경 합니다.

열기는 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* 파일 및 기존 코드를 다음과 같이 바꿉니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

전체 날짜 및 시간을 표시할 하면 녹색과 큰 텍스트를 호출 하는 CSS 클래스를 추가 합니다.

열기는 *Movie.cs* 파일을 추가 [UIHint](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 `ReleaseDate` 속성을 다음 예제와 같이:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

그러면 ASP.NET MVC를 표시 하는 경우는 `ReleaseDate` 속성 (특히, 및 아닌 `DateTime` 개체)를 사용 해야는 *LoudDateTime.cshtml* 서식 파일입니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

에 `ReleaseDate` 속성 이제 날짜와 시간을 표시 녹색를 큰 글꼴로 합니다.

으로 돌아와서는 `UIHint` 특성에 *Movie.cs* 파일을 주석으로 처리 하므로 *LoudDateTime.cshtml* 서식 파일 사용 되지 않습니다. 응용 프로그램을 다시 실행합니다. 릴리스 날짜 광범위 하 고 녹색 표시 되지 않습니다. 이 확인은 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿은 인덱스 및 세부 정보 보기에 사용 됩니다.

앞서 언급 했 듯이 개별 인스턴스의 일부 데이터에 템플릿을 적용할 수 있는 보기에서 서식 파일을 적용할 수도 있습니다. 열기는 *Views\Movies\Details.cshtml* 보기. 추가 `"LoudDateTime"` 의 두 번째 매개 변수로 [Html.DisplayFor](https://msdn.microsoft.com/en-us/library/ee407420.aspx) 에 대 한 호출에서 `ReleaseDate` 필드입니다. 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

이 지정 하는 `LoudDateTime` 어떤 특성이 모델에 적용 되었는지에 관계 없이 모델 속성을 표시 하려면 서식 파일을 사용 해야 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

영화 인덱스 페이지를 사용 하는지 확인는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 서식 파일 (굵은 빨간색) 및 *Movie\Details* 페이지를 사용 하는 *Views\Movies\ DisplayTemplates\LoudDateTime.cshtml* 서식 파일 (대형 및 녹색).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

다음 섹션에서는 복합 유형에 대 한 서식 파일을 만듭니다.

>[!div class="step-by-step"]
[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
