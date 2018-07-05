---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 모델에 유효성 검사 추가 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 47c3f16d4592d2f61c6f1c3c1988e3622cb84a00
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384805"
---
<a name="adding-validation-to-the-model"></a>모델에 유효성 검사 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.


이 섹션에서는 유효성 검사 논리를 추가 합니다 `Movie` 모델 및 있습니다 유효성 검사 규칙을 만들거나 응용 프로그램을 사용 하 여 동영상을 편집 하려면 사용자가 언제 든 지 사항이 적용 되도록 확인 됩니다.

## <a name="keeping-things-dry"></a>작업을 반복 금지 유지

ASP.NET MVC의 핵심 디자인 개념 중 하나는 시험 (&quot;반복&quot;). ASP.NET MVC 기능이 나 동작을 한 번만 지정 한 후 응용 프로그램에서 모든 곳에 반영 될 것을 권장 합니다. 작성 해야 하는 코드의 양을 줄이고 적은 오류가 발생할 가능성이 적고 더 쉬워진 유지 관리를 작성 하는 코드입니다.

ASP.NET MVC 및 Entity Framework Code First에서 제공 되는 유효성 검사 지원은 작업에서 반복 금지 원칙의 좋은 예입니다. (모델 클래스)의 한 곳에서 유효성 검사 규칙을 선언적으로 지정할 수 있습니다 및 규칙을 어디에서 나 응용 프로그램에 적용 됩니다.

동영상 응용 프로그램에서이 유효성 검사 지원 활용을 걸릴 수 있습니다 하는 방법을 살펴보겠습니다.

## <a name="adding-validation-rules-to-the-movie-model"></a>영화 모델에 유효성 검사 규칙 추가

일부 유효성 검사 논리를 추가 하 여 먼저는 `Movie` 클래스입니다.

*Movie.cs* 파일을 엽니다. 추가 된 `using` 문을 참조 하는 파일의 맨 위에 있는 합니다 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

네임 스페이스에 없는 확인 `System.Web`합니다. DataAnnotations는 클래스 또는 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 집합을 제공 합니다.

이제 업데이트 된 `Movie` 기본 제공 기능을 활용 하는 클래스 [ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)를 [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), 및 [ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성 . 특성을 적용 하는 예로 다음 코드를 사용 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

응용 프로그램을 실행 하 고 다음 런타임 오류가 다시 표시 됩니다.

***'MovieDBContext' 컨텍스트를 지 원하는 모델 데이터베이스를 만든 이후에 변경 되었습니다. Code First 마이그레이션을 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).***

마이그레이션 스키마를 업데이트 하려면 사용 합니다. 솔루션을 연 다음 합니다 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

이 명령은 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMIgration` 지정한 이름을 가진 파생 클래스 (*AddDataAnnotationsMig*), 및는 `Up` 메서드를 업데이트 하는 코드를 볼 수 있습니다 스키마 제약 조건입니다. 합니다 `Title` 하 고 `Genre` 필드는 더 이상 null을 허용 (즉, 값을 입력 해야 합니다) 및 `Rating` 필드의 최대 길이 5입니다.

이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다. 합니다 `Required` 특성 속성 값을 가져야 합니다 나타내고이 샘플에서는 영화에 대 한 값에는 `Title`, `ReleaseDate`, `Genre`, 및 `Price` 유효 하기 위해 속성입니다. `Range` 특성은 지정된 범위 내의 값을 제한합니다. `StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 필요에 따라 최소 길이를 설정할 수 있습니다. 내장 형식 (같은 `decimal, int, float, DateTime`)는 기본적으로 필요 하 고 필요 하지 않습니다는 `Required` 특성입니다.

먼저 코드 하면 응용 프로그램 데이터베이스에 변경 내용을 저장 하기 전에 모델 클래스에서 지정 유효성 검사 규칙 적용 됩니다. 아래 코드는 예외를 throw 하는 예를 들어 경우는 `SaveChanges` 여러 필요 하기 때문에 메서드가 호출 되 `Movie` 속성 값은 누락 이며 가격은 0 (유효 범위를 벗어난)입니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

.NET Framework에 의해 자동으로 적용 하는 유효성 검사 규칙 사용 하면 확인 응용 프로그램 보다 강력 합니다. 또한 유효성 검사를 잊거나, 데이터베이스에 불량 데이터가 실수로 들어가지 않게 할 수 있습니다.

업데이트 된 전체 코드 다음과 같습니다 *Movie.cs* 파일:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC에서 UI 유효성 검사 오류

응용 프로그램을 다시 실행 하 고 이동 합니다 */Movies* URL입니다.

클릭 합니다 **새로 만들기** 새 영화를 추가 합니다. 일부 잘못 된 값을 사용 하 여 양식을 입력 하 고 클릭 합니다 **만들기** 단추입니다.

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> 쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하도록 (&quot;,&quot;) 포함 해야 소수점 *globalize.js* 및 특정 *cultures/globalize.cultures.js* 파일 (에서 [ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 및 JavaScript를 사용 하 여 `Globalize.parseFloat`입니다. 다음 코드에서는 Views\Movies\Edit.cshtml 파일을 사용 하려면 수정 된 &quot;FR-FR&quot; 문화권:


[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

폼에 자동으로 사용 하는 방법을 빨간색 테두리 색을 잘못 된 데이터를 포함 하 고 각각 옆에 있는 적절 한 유효성 검사 오류 메시지를 내보낼에 있는 입력란을 강조 표시를 확인 합니다. 오류는 클라이언트 쪽(JavaScript 및 jQuery 사용) 및 서버 쪽(사용자가 JavaScript를 사용하지 않도록 설정한 경우) 모두 적용됩니다.

실제 혜택은 코드 한 줄도 변경할 필요가 없었습니다 합니다 `MoviesController` 클래스 또는 합니다 *Create.cshtml* 이 유효성 검사 UI를 사용 하기 위해. 이 자습서의 앞 부분에서 만든 컨트롤러와 보기에서는 `Movie` 모델 클래스의 속성의 유효성 검사 특성을 사용하여 유효성 검사 규칙을 자동으로 선택했습니다.

속성에 대해 알 수 있습니다 `Title` 및 `Genre`, 폼에 제출 하기 전에 필수 특성이 적용 되지 않습니다 (적중 합니다 **만들기** 단추), 또는 입력된 필드에 텍스트를 입력 하 고 제거 합니다. 처음에 비어 (예: Create view의 필드) 및 필요한 특성만 있는 다른 유효성 검사 특성을 필드에 대해 다음 유효성 검사 트리거를 수행할 수 있습니다.

1. 필드를 탭 합니다.
2. 일부 텍스트를 입력 합니다.
3. 필드 밖을 탭합니다.
4. 필드를 다시 탭 합니다.
5. 텍스트를 제거 합니다.
6. 필드 밖을 탭합니다.

위의 순서는 제출 단추를 연결 하지 않고도 필요한 유효성 검사를 트리거합니다. 단순히 필드 중 하나를 입력 하지 않고 제출 단추를 누르면 클라이언트 쪽 유효성 검사를 트리거합니다. 양식 데이터는 클라이언트 쪽 유효성 검사 오류가 없을 때까지 서버에 전송되지 않습니다. HTTP Post 메서드에 중단점을 배치 하거나 사용 하 여 테스트할 수 있습니다 합니다 [fiddler 도구](http://fiddler2.com/fiddler2/) 또는 IE 9 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478)합니다.

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>만들기를 살펴보고 작업 메서드를 만들어 유효성 검사에서 발생 하는 방법

컨트롤러나 보기에서 코드에 대한 업데이트 없이 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다. 다음 목록을 보여 줍니다 합니다 `Create` 의 메서드는 `MovieController` 클래스 형태입니다. 없는 것 이므로 만든 방법으로이 자습서의 앞부분에서 변경 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

첫 번째(HTTP GET) `Create` 작업 메서드는 최초 만들기 양식을 표시합니다. 두 번째(`[HttpPost]`) 버전은 양식 게시를 처리합니다. 두 번째 `Create` 메서드(`HttpPost` 버전)은 `ModelState.IsValid`를 호출하여 동영상의 유효성 검사 오류 여부를 확인합니다. 이 메서드 호출에서는 개체에 적용된 모든 유효성 검사 특성을 평가합니다. 개체에 유효성 검사 오류가 있으면 `Create` 메서드는 양식을 다시 표시합니다. 오류가 없으면 메서드가 데이터베이스에 새 동영상을 저장합니다. 를 사용 하기 동영상 예제에서 **양식을 서버에 게시 되지 클라이언트측;에서 검색 하는 유효성 검사 오류가 있을 때 두 번째** `Create` **메서드가 절대 호출**합니다. 클라이언트 유효성 검사가 해제 된 경우 브라우저에서 JavaScript를 비활성화 하 고 HTTP POST `Create` 메서드 호출 `ModelState.IsValid` 동영상에 유효성 검사 오류가 있는지 확인 하려면.

`HttpPost Create` 메서드에서 중단점을 설정하고 메서드가 호출되지 않게 확인할 수 있으며, 유효성 검사 오류가 탐지되면 클라이언트 쪽 유효성 검사가 양식 데이터를 제출하지 않습니다. 브라우저에서 JavaScript를 사용하지 않으면서 오류가 있는 상태로 양식을 제출하면 중단점에 이르게 됩니다. JavaScript 없이도 전체 유효성 검사가 가능합니다. 다음 이미지에는 Internet Explorer에서 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

다음 이미지에서는 FireFox 브라우저에서 JavaScript를 사용하지 않도록 설정하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image5.png)

다음 이미지는 Chrome 브라우저를 사용 하 여 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image6.png)

다음은 *Create.cshtml* 자습서의 앞부분에서 스 캐 폴드 하는 템플릿 보기. 이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

코드를 사용 하는 방법을 확인할 수 있습니다는 `Html.EditorFor` 도우미 출력에 `<input>` 요소 각각에 대해 `Movie` 속성. 이 도우미 옆에 있는 호출 되는 `Html.ValidationMessageFor` 도우미 메서드입니다. 이러한 두 가지 도우미 메서드를 컨트롤러에서 보기로 전달 되는 모델 개체 사용 (이 경우에 `Movie` 개체). 적절 하 게 모델 및 표시 오류 메시지에 지정 된 유효성 검사 특성에 대 한 자동으로 찾습니다.

이 방법을 사용 하는 방법에 대 한 훌륭한 점은 컨트롤러도 아니고 보기 템플릿 만들기가 알고 있는 아무 것도 표시 되는 특정 오류 메시지 또는 적용 되는 실제 유효성 검사 규칙에 대 한입니다. 유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다. 이러한 동일한 유효성 검사 규칙 편집 보기와 보기를 만들 수 있습니다 하는 다른 템플릿에 모델 편집에 자동으로 적용 됩니다.

나중에 유효성 검사 논리를 변경 하려는 경우 하면 정확 하 게 한 곳에서 모델 유효성 검사 특성을 추가 하 여 (이 예는 `movie` 클래스). 모든 유효성 검사 논리가 한 곳에 정의되어 모든 곳에서 사용되므로 응용 프로그램의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다. 이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다. 또한 반복 금지 원칙에 완전히 부합하게 됩니다.

## <a name="adding-formatting-to-the-movie-model"></a>영화 모델 형식 추가

*Movie.cs* 파일을 열고 `Movie` 클래스를 확인합니다. 합니다 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에도 서식 특성을 제공 합니다. 에서는 이미 적용을 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 출시일을 가격 필드를 열거형 값입니다. 다음 코드에서는 합니다 `ReleaseDate` 하 고 `Price` 적절 한 속성 [ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성입니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

합니다 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) HTML을 렌더링 하는 뷰 엔진을 알리는 데 사용 되는, 특성은 유효성 검사 특성이 아닙니다. 위의 예제는 `DataType.Date` 특성 시간 없이 날짜로 영화 날짜를 표시 합니다. 다음 예를 들어 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성 데이터 형식의 유효성을 검사 하지 않습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

위에 나열 된 특성 데이터의 형식을 지정 하도록 뷰 엔진에 대 한 힌트만 제공 (같은 특성 제공 하 고 &lt;는&gt; URL에 대 한 및 &lt;a =&quot;mailto:EmailAddress.com&quot; &gt; 전자 메일입니다. 사용할 수는 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 유효성을 검사할 데이터 형식의 특성입니다.

사용 하는 대체 방법을 `DataType` 특성을 명시적으로 설정 된 [ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx) 값. 다음 코드는 날짜 형식 문자열을 사용 하 여 릴리스 날짜 속성을 보여 줍니다 (즉, &quot;d&quot;). 이 사용 하면는 않으려는 시간 출시일의 일부로 지정 됩니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

전체 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

응용 프로그램을 실행 하 고 이동 하 여 `Movies` 컨트롤러입니다. 릴리스 날짜 및 가격 서식이 지정 원활 하 게 됩니다. 릴리스 날짜 및 가격을 사용 하 여 아래 이미지를 보여 줍니다 &quot;FR-FR&quot; 문화권으로 합니다.

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

아래 이미지는 기본 culture (영어 (미국))를 사용 하 여 표시 되는 동일한 데이터를 보여 줍니다.

![](adding-validation-to-the-model/_static/image8.png)

이 시리즈의 다음 부분에서는 응용 프로그램을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.

> [!div class="step-by-step"]
> [이전](adding-a-new-field-to-the-movie-model-and-table.md)
> [다음](examining-the-details-and-delete-methods.md)
