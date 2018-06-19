---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 모델에 유효성 검사 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 39d1d9d4cb8b11f7ce5a3a85c51f652115d79db7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874550"
---
<a name="adding-validation-to-the-model"></a>모델에 유효성 검사 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.


이 섹션에서는 유효성 검사 논리를 추가 합니다는 `Movie` 모델과 하면 사용자가 만들거나 응용 프로그램을 사용 하 여 동영상을 편집 하는 언제 든 지 유효성 검사 규칙이 적용 되도록 유지 됩니다.

## <a name="keeping-things-dry"></a>건조 구성을

ASP.NET MVC의 핵심 디자인 개념 중 하나는 드라이 (&quot;하지 반복 직접&quot;). ASP.NET MVC 기능 또는 동작을 한 번만 지정 한 다음 응용 프로그램에 everywhere 반영 하는 것이 권장 합니다. 작성 해야 하는 코드의 양을 줄어들고 오류가 발생 하기 쉽고 유지 관리가 더 용이 작성 하는 코드를 만듭니다.

ASP.NET MVC 및 Entity Framework Code First 제공 하는 유효성 검사 지원은 동작의 건조 원칙의 좋은 예입니다. (모델 클래스)의 한 지점에서 유효성 검사 규칙을 선언적으로 지정할 수 있습니다 및 규칙은 응용 프로그램에 모든 위치에서 적용 됩니다.

있습니다 사용할 수 있는 방법을이 유효성 검사 지원의 영화 응용 프로그램에서 살펴보겠습니다.

## <a name="adding-validation-rules-to-the-movie-model"></a>영화 모델에 유효성 검사 규칙 추가

일부 유효성 검사 논리를 추가 하 여 먼저는 `Movie` 클래스입니다.

*Movie.cs* 파일을 엽니다. 추가 `using` 문을 참조 하는 파일 맨 위에 있는 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

네임 스페이스 포함 하지 않는 `System.Web`합니다. DataAnnotations 모든 클래스 또는 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 된 집합을 제공 합니다.

이제 업데이트 된 `Movie` 클래스는 기본 제공 기능을 활용 하려면 [ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), 및 [ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성 . 특성을 적용 대상의 예를 들어 다음 코드를 사용 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

응용 프로그램을 실행 하 고 다시 얻게 됩니다 다음 런타임 오류가 발생 합니다.

***'MovieDBContext' 컨텍스트를 백업 하는 모델 데이터베이스를 만든 후에 변경 되었습니다. Code First 마이그레이션을 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).***

마이그레이션 스키마 업데이트를 사용 합니다. 솔루션을 작성 한 다음 엽니다는 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

Visual Studio 새 정의 하는 클래스 파일을 엽니다이 명령이 완료 되 면 `DbMIgration` 지정한 이름을 가진 파생 클래스 (*AddDataAnnotationsMig*), 및는 `Up` 메서드를 업데이트 하는 코드를 볼 수 있습니다 스키마 제약 조건입니다. `Title` 및 `Genre` 필드는 null을 허용 더 이상 (즉, 값을 입력 해야 합니다) 및 `Rating` 필드의 최대 길이는 5입니다.

이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다. `Required` 특성 나타냅니다 속성 값을 가져야 합니다;이 샘플에서는 동영상은에 대 한 값은 `Title`, `ReleaseDate`, `Genre`, 및 `Price` 유효 하려면 속성입니다. `Range` 특성은 지정된 범위 내의 값을 제한합니다. `StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 필요에 따라 최소 길이를 설정할 수 있습니다. 내장 형식 (예: `decimal, int, float, DateTime`) 기본적으로 필요 하며, 필요 하지 않습니다는 `Required` 특성입니다.

코드는 먼저 응용 프로그램 데이터베이스에 변경 내용을 저장 하기 전에 모델 클래스에서 지정 된 유효성 검사 규칙 적용 되도록 보장 합니다. 예를 들어 아래 코드는 예외를 throw 할 때는 `SaveChanges` 메서드는, 여러 필요 하기 때문에 `Movie` 속성 값이 누락 되 고 가격 기본값은 0 (이 범위를 벗어났습니다).

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

.NET Framework에 의해 자동으로 적용 하는 유효성 검사 규칙을 만드는 것 사용 하면 확인 응용 프로그램 보다 강력 합니다. 또한 유효성 검사를 잊거나, 데이터베이스에 불량 데이터가 실수로 들어가지 않게 할 수 있습니다.

다음은 업데이트 된 항목에 대 한 전체 코드 *Movie.cs* 파일:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC에서 UI 유효성 검사 오류

응용 프로그램을 다시 실행을 탐색 하 고 */Movies* URL입니다.

클릭는 **새로 만들기** 새 동영상을 추가 하는 링크입니다. 일부 잘못 된 값으로 양식을 작성 한 다음 클릭는 **만들기** 단추입니다.

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> 쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하기 위해 (&quot;,&quot;) 소수점을 포함 해야 *globalize.js* 및 특정 *cultures/globalize.cultures.js* 파일 (에서 [ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 및 사용 하는 JavaScript `Globalize.parseFloat`합니다. 다음 코드와 작업할 Views\Movies\Edit.cshtml 파일을 수정 된 &quot;FR-FR&quot; 문화권:


[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

어떻게 폼에 자동으로 빨강 테두리 색을 강조 하기 위해 사용 각 옆에 있는 적절 한 유효성 검사 오류 메시지가 방사 및 잘못 된 데이터를 포함 하는 텍스트 상자를 확인 합니다. 오류는 클라이언트 쪽(JavaScript 및 jQuery 사용) 및 서버 쪽(사용자가 JavaScript를 사용하지 않도록 설정한 경우) 모두 적용됩니다.

실제 혜택은 한 줄의 코드를 변경 해야 하지 않은 `MoviesController` 클래스 또는 *Create.cshtml* UI이 유효성이 검사를 사용 하도록 설정 하려면 보기. 이 자습서의 앞 부분에서 만든 컨트롤러와 보기에서는 `Movie` 모델 클래스의 속성의 유효성 검사 특성을 사용하여 유효성 검사 규칙을 자동으로 선택했습니다.

속성에 대 한 알 수 있습니다 `Title` 및 `Genre`, 필수 특성은 양식을 제출 될 때까지 적용 되지 않습니다 (적중는 **만들기** 단추), 또는 입력된 필드에 텍스트를 입력 하 고 제거 합니다. 변수가 처음에 (예: 뷰 만들기에 대 한 필드) 비어 하 고 여기에 필수 특성만 및 다른 유효성 검사 특성을 필드에 대해 다음 유효성 검사 트리거를 수행할 수 있습니다.

1. 필드를 탭 합니다.
2. 텍스트를 입력 합니다.
3. 필드 밖을 탭합니다.
4. 필드에 다시 여기를 탭 합니다.
5. 텍스트를 제거 합니다.
6. 필드 밖을 탭합니다.

위의 순서를 제출 단추에 도달 하지 않고 필요한 유효성 검사를 트리거합니다. 필드를 입력 하지 않고 제출 단추를 누르기 단순히 클라이언트 쪽 유효성 검사를 트리거합니다. 양식 데이터는 클라이언트 쪽 유효성 검사 오류가 없을 때까지 서버에 전송되지 않습니다. HTTP Post 메서드에 중단점을 배치 하거나 사용 하 여 테스트할 수 있습니다는 [fiddler 도구](http://fiddler2.com/fiddler2/) 또는 IE 9 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478)합니다.

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>만들기 확인 하 고 작업 메서드를 작성할 유효성 검사에서 발생 하는 방법

컨트롤러나 보기에서 코드에 대한 업데이트 없이 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다. 다음 목록에서는 `Create` 의 메서드는 `MovieController` 클래스 표시 합니다. 만든 방법으로이 자습서의 앞부분에 나오는 것에서 변경 하기가 되지 않습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

첫 번째(HTTP GET) `Create` 작업 메서드는 최초 만들기 양식을 표시합니다. 두 번째(`[HttpPost]`) 버전은 양식 게시를 처리합니다. 두 번째 `Create` 메서드(`HttpPost` 버전)은 `ModelState.IsValid`를 호출하여 동영상의 유효성 검사 오류 여부를 확인합니다. 이 메서드 호출에서는 개체에 적용된 모든 유효성 검사 특성을 평가합니다. 개체에 유효성 검사 오류가 있으면 `Create` 메서드는 양식을 다시 표시합니다. 오류가 없으면 메서드가 데이터베이스에 새 동영상을 저장합니다. 영화 예에서 사용 하 여, **클라이언트측;에서 검색 된 유효성 검사 오류가 있을 때에 폼이 서버에 게시 하지 두 번째** `Create` **메서드 호출 되지 않습니다**합니다. 브라우저에서 JavaScript를 사용 하지 않도록 설정 하면, 클라이언트 유효성 검사를 사용할 수 없습니다 및 HTTP POST `Create` 메서드 호출 `ModelState.IsValid` 동영상에 모든 유효성 검사 오류가 있는지 확인 합니다.

`HttpPost Create` 메서드에서 중단점을 설정하고 메서드가 호출되지 않게 확인할 수 있으며, 유효성 검사 오류가 탐지되면 클라이언트 쪽 유효성 검사가 양식 데이터를 제출하지 않습니다. 브라우저에서 JavaScript를 사용하지 않으면서 오류가 있는 상태로 양식을 제출하면 중단점에 이르게 됩니다. JavaScript 없이도 전체 유효성 검사가 가능합니다. 다음 그림에는 Internet Explorer에서 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

다음 이미지에서는 FireFox 브라우저에서 JavaScript를 사용하지 않도록 설정하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image5.png)

다음 이미지는 Chrome 브라우저에서 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image6.png)

다음은 이러한는 *Create.cshtml* 자습서의 앞부분에 나오는 스 캐 폴드 된 템플릿 보기. 이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

코드 사용 하는 여는 `Html.EditorFor` 출력 하는 도우미는 `<input>` 요소 각각에 대해 `Movie` 속성. 이 도우미 옆에 대 한 호출 되는 `Html.ValidationMessageFor` 도우미 메서드입니다. 이러한 두 개의 도우미 메서드를 보기에는 컨트롤러에 의해 전달 되는 모델 개체 사용 (이 경우는 `Movie` 개체). 적절 하 게 모델 및 표시 오류 메시지에 지정 된 유효성 검사 특성에 대 한 자동으로 검색 합니다.

이 방법에 대 한 훌륭한은 컨트롤러도 아니고 만들기 보기 템플릿이 알고 있는 아무 것도 표시 되는 특정 오류 메시지 또는 적용을 실제 유효성 검사 규칙에 대 한입니다. 유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다. 이 동일한 유효성 검사 규칙 편집 보기 및 모든 다른 뷰 템플릿을 만들 수 있습니다 모델을 편집 하는 자동으로 적용 됩니다.

나중에 유효성 검사 논리를 변경 하려는 경우 후 그렇게 정확 하 게 한 곳에서 모델에 유효성 검사 특성을 추가 하 여 (이 예제는 `movie` 클래스). 모든 유효성 검사 논리가 한 곳에 정의되어 모든 곳에서 사용되므로 응용 프로그램의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다. 이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다. 또한 반복 금지 원칙에 완전히 부합하게 됩니다.

## <a name="adding-formatting-to-the-movie-model"></a>영화 모델에 서식 추가

*Movie.cs* 파일을 열고 `Movie` 클래스를 확인합니다. [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에 서식 특성을 제공 합니다. 이미 적용 한 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 출시 날짜에 시작 및 끝 price 필드 열거형 값입니다. 다음 코드는 `ReleaseDate` 및 `Price` 는 적절 한 속성 [ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성입니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 사용 하는 뷰 엔진이 HTML을 렌더링 하는 방법을 설명 하는, 특성은 유효성 검사 특성이 아닙니다. 위의 예에는 `DataType.Date` 특성 시간 없이 날짜로 영화 날짜를 표시 합니다. 예를 들어, 다음 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성 형식의 데이터의 유효성을 검사 하지 않습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

위에 나열 된 특성에만 데이터의 서식을 지정 하는 뷰 엔진이 대 한 힌트 제공 (같은 특성을 제공 하 고 &lt;는&gt; URL에 대 한 및 &lt;는 href =&quot;mailto:EmailAddress.com&quot; &gt; 전자 메일입니다. 사용할 수는 [정규식으로](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 유효성을 검사할 데이터 형식의 특성입니다.

사용 하 여 다른 방법은 `DataType` 특성을 명시적으로 설정 된 [ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx) 값입니다. 다음 코드와 날짜 형식 문자열을 사용 하 여 릴리스 날짜 속성 (즉, &quot;d&quot;). 않으려면 시간 릴리스 날짜의 일환으로 지정 하려면이 사용 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

전체 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러입니다. 릴리스 날짜 및 가격의 형식이 적절 하 게 됩니다. 릴리스 날짜 및 사용 하 여 가격을 표시 하는 아래 이미지 &quot;FR-FR&quot; 문화권으로 합니다.

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

아래 이미지는 기본 문화권 (미국 영어)으로 표시 되는 동일한 데이터를 보여줍니다.

![](adding-validation-to-the-model/_static/image8.png)

이 시리즈의 다음 부분에서는 응용 프로그램을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.

> [!div class="step-by-step"]
> [이전](adding-a-new-field-to-the-movie-model-and-table.md)
> [다음](examining-the-details-and-delete-methods.md)
