---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: ASP.NET MVC-3 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MV에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: fd1ae746f4f134b779c7eee50cf6c840bbb7068e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869467"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>ASP.NET MVC-3 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.


## <a name="working-with-complex-types"></a>복합 형식 사용

이 섹션에서는 주소 클래스를 만드는 하 고 표시 하는 템플릿을 만드는 방법을 설명 합니다.

에 *모델* 폴더를 라는 새 클래스 파일을 만들 *Person.cs* 두 유형이 넣습니다:는 `Person` 클래스 및 `Address` 클래스입니다. `Person` 클래스도 형식화 된 속성에 포함 될 `Address`합니다. `Address` 형식이 같은 기본 제공 형식 중 하나가 아니므로 의미 하는 복합 유형을 `int`, `string`, 또는 `double`합니다. 대신에 몇 가지 속성이 있습니다. 새 클래스에 대 한 코드는 다음과 같습니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

에 `Movie` 컨트롤러에는 다음 추가 `PersonDetail` 사용자 인스턴스를 표시 하는 작업:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

다음 코드를 추가 `Movie` 를 채우는 컨트롤러는 `Person` 예제 데이터 모델:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

열기는 *Views\Movies\PersonDetail.cshtml* 파일에 대 한 다음 태그를 추가 하 고는 `PersonDetail` 보기.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

Ctrl + f 5를 눌러 응용 프로그램을 실행 하 여 탐색 하 *영화/PersonDetail*합니다.

`PersonDetail` 보기 포함 되어 있지 않습니다는 `Address` 복합 유형을 볼 수 있듯이이 스크린 샷에 합니다. (주소가 없는 표시 됩니다.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

`Address` 복합 유형 이므로 모델 데이터가 표시 되지 않습니다. 주소 정보를 표시 하려면 열에서 *Views\Movies\PersonDetail.cshtml* 다시 파일을 다음 태그를 추가 합니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

에 대 한 전체 태그는 `PersonDetail` 이제 보기는 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

응용 프로그램을 다시 실행 하 고 표시 된 `PersonDetail` 보기. 주소 정보는 이제 표시 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>복합 형식에 대 한 서식 파일 만들기

이 섹션에서는 렌더링에 사용 되는 템플릿을 만듭니다는 `Address` 복합 유형입니다. 에 대 한 템플릿을 만들 때의 `Address` 유형, ASP.NET MVC 자동으로 사용할 수는 주소 모델은 응용 프로그램의 서식을 지정 합니다. 이렇게 하면 렌더링을 제어 하는 방법의 `Address` 응용 프로그램에서 한 장소에서 형식입니다.

에 *Views\Shared\DisplayTemplates* 폴더 라는 강력한 형식의 부분 뷰를 만들 **주소**:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

클릭 **추가**를 연 다음 새 *Views\Shared\DisplayTemplates\Address.cshtml* 파일입니다. 새 보기는 다음과 같은 생성 된 태그가 포함 되어 있습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

응용 프로그램을 실행 하 고 표시 된 `PersonDetail` 보기. 이 이번에는 `Address` 방금 만든 서식 파일은 표시 하는 데 사용 되는 `Address` 복합 형식 이므로 표시는 다음과 같습니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>요약: 모델 표시 형식 및 서식 파일을 지정 하는 방법

다음 방법 중 하나를 사용 하 여 형식 또는 모델 속성에 대 한 템플릿을 지정할 수 살펴보았습니다.

- 적용 된 `DisplayFormat` 특성 모델의 속성입니다. 예를 들어 다음 코드는 시간을 제외 표시할 날짜를 생성 합니다.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- 적용 한 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성 데이터 형식 지정 및 모델에 속성입니다. 예를 들어 다음 코드에서는 시간을 제외한 표시할 날짜를 생성 합니다.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일은 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 해당 서식 파일, 폴더 렌더링에 사용 되는 `DateTime` 속성입니다. 그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜로 속성을 표시합니다.
- 디스플레이 템플릿을 만드는 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더 이름이 서식을 지정할 데이터 형식이 일치 합니다. 예를 들어 언급 했 듯이 하는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 렌더링 하는 데 사용한 `DateTime` 모델에 특성을 추가 하지 않고 및 보기에 태그를 추가 하지 않고 모델의 속성.
- 사용 하는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 모델 속성을 표시 하려면 서식 파일을 지정 하려면 모델에는 특성입니다.
- 표시 템플릿 이름을 명시적으로 추가 된 [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) 보기에서 호출 합니다.

응용 프로그램에서 작업을 수행 해야 할 작업에 사용 하는 방법에 따라 달라 집니다. 이러한 접근 방식을 정확 하 게 종류의 서식 지정 해야 하는 get를 혼합 하는 일반적이 지 않습니다.

다음 섹션에서 전환 하 여 약간 주제 및 입력 방식을 사용자 지정 데이터 표시 방법을 사용자 지정에서 이동 합니다. JQuery datepicker 날짜를 지정 하는 편리한 방법을 제공 하기 위해 응용 프로그램의 편집 뷰에 연결 합니다.

> [!div class="step-by-step"]
> [이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
