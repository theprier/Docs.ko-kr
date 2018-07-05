---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 3 부-ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker 팝업 일정을 ASP.NET MV에서 사용 하는 방법의 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: 11f9e0a8602e9ee1feda9d0e7d0d319add7c440c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400773"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>3 부-ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 편집기 템플릿, 표시 템플릿 및 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법의 기본 사항을 설명 합니다.


## <a name="working-with-complex-types"></a>복합 형식 사용

이 섹션의 address 클래스를 만들고 표시 하는 템플릿을 만드는 방법에 알아봅니다.

에 *모델* 폴더를 라는 새 클래스 파일을 만듭니다 *Person.cs* 배치할 두 형식:를 `Person` 클래스 및 `Address` 클래스입니다. 합니다 `Person` 클래스와 형식화 된 속성이 포함 됩니다 `Address`합니다. 합니다 `Address` 형식은 복합 형식, 즉 같은 기본 제공 형식 중 하나가 아닙니다 `int`를 `string`, 또는 `double`합니다. 대신 여러 속성이 있습니다. 새 클래스에 대 한 코드는 다음과 같습니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

에 `Movie` 컨트롤러에는 다음 추가 `PersonDetail` 사용자 인스턴스를 표시 하는 작업:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

에 다음 코드를 추가 합니다 `Movie` 채우는 데 컨트롤러는 `Person` 몇 가지 샘플 데이터를 사용 하 여 모델:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

열기는 *Views\Movies\PersonDetail.cshtml* 파일을 다음 태그를 추가 합니다 `PersonDetail` 보기.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

Ctrl + F5 키를 눌러 응용 프로그램을 실행 하 고 이동 *영화/PersonDetail*합니다.

`PersonDetail` 보기를 포함 하지 않습니다는 `Address` 복합 형식을 볼 수 있듯이이 스크린샷에 합니다. (주소 없음 표시 됩니다.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

`Address` 복합 유형 이므로 모델 데이터가 표시 되지 않습니다. 주소 정보를 표시 하려면 열을 *Views\Movies\PersonDetail.cshtml* 다시 파일을 다음 태그를 추가 합니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

전체 태그를는 `PersonDetail` 이제 뷰는 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

응용 프로그램을 다시 실행 하 고 표시 된 `PersonDetail` 보기. 주소 정보가 표시 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>복합 형식에 대 한 템플릿 만들기

이 섹션에서는 렌더링 하는 데 사용할 템플릿으로 만듭니다는 `Address` 복합 형식입니다. 에 대 한 템플릿을 만들 때의 `Address` 형식, ASP.NET MVC 자동으로 사용 하 여 응용 프로그램에서 임의의 위치를 주소 모델 형식을 지정 합니다. 이렇게 하면 렌더링을 제어 하는 방법의 `Address` 응용 프로그램의 한 위치에서 형식입니다.

에 *Views\Shared\DisplayTemplates* 폴더를 명명 된 강력한 형식의 부분 보기를 만들 **주소**:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

클릭 **추가**를 연 다음 새 *Views\Shared\DisplayTemplates\Address.cshtml* 파일입니다. 다음 생성 된 태그를 포함 하는 새 보기:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

응용 프로그램을 실행 하 고 표시 된 `PersonDetail` 보기. 이 이번에는 `Address` 방금 만든 템플릿 표시 되는 `Address` 표시를 다음과 같이 표시 되도록 복합 형식:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>요약: 모델 표시 형식 및 서식 파일을 지정 하는 방법

다음 방법 중 하나를 사용 하 여 형식 또는 모델 속성에 대 한 템플릿을 지정할 수 살펴보았습니다.

- 적용 된 `DisplayFormat` 특성을 모델의 속성입니다. 예를 들어, 다음 코드는 시간을 제외한 표시할 날짜를 발생 시킵니다.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- 적용을 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성의 속성에 모델 및 데이터 형식을 지정 합니다. 예를 들어, 다음 코드는 시간을 제외한 표시할 날짜를 하면 됩니다.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일을 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더에서 해당 템플릿을 렌더링 하는 데 사용할는 `DateTime` 속성입니다. 그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜 속성을 표시합니다.
- 표시 템플릿 만들기를 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더 이름이 서식을 지정 하려는 데이터 형식과 일치 합니다. 살펴본 예를 들어 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 렌더링 하는 데 사용 된 `DateTime` 보기에 태그를 추가 하지 않고 모델에 특성을 추가 하지 않고 모델의 속성입니다.
- 사용 하는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 모델 속성을 표시 하려면 서식 파일을 지정 하려면 모델에는 특성입니다.
- 표시 템플릿 이름을 명시적으로 추가 합니다 [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) 보기에서 호출 합니다.

응용 프로그램에서 작업을 수행 해야 하는 항목에 사용 하는 방법에 따라 달라 집니다. 혼합 해야 하는 서식 지정의 종류를 정확히 얻으려면 이러한 접근 방식은 일반적이 지 않은 것입니다.

다음 섹션에서 전환 하 여 약간 다뤄을 입력 하는 방법을 사용자 지정 데이터 표시 방법을 사용자 지정으로 이동 합니다. 날짜를 지정 하는 능률적인 방법을 제공 하기 위해 응용 프로그램에서 편집 보기로 jQuery datepicker에 연결 됩니다.

> [!div class="step-by-step"]
> [이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
