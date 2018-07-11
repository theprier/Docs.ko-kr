---
uid: mvc/overview/getting-started/introduction/adding-validation
title: 유효성 검사 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: 97526d908dd3b835040453b53eae76f733a01c04
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38172195"
---
<a name="adding-validation"></a>유효성 검사 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

이 섹션에서는 유효성 검사 논리를 추가 합니다 `Movie` 모델 및 있습니다 유효성 검사 규칙을 만들거나 응용 프로그램을 사용 하 여 동영상을 편집 하려면 사용자가 언제 든 지 사항이 적용 되도록 확인 됩니다.

## <a name="keeping-things-dry"></a>작업을 반복 금지 유지

ASP.NET MVC의 핵심 디자인 개념 중 하나인 [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself) (&quot;반복&quot;). ASP.NET MVC 기능이 나 동작을 한 번만 지정 한 후 응용 프로그램에서 모든 곳에 반영 될 것을 권장 합니다. 작성 해야 하는 코드의 양을 줄이고 적은 오류가 발생할 가능성이 적고 더 쉬워진 유지 관리를 작성 하는 코드입니다.

ASP.NET MVC 및 Entity Framework Code First에서 제공 되는 유효성 검사 지원은 작업에서 반복 금지 원칙의 좋은 예입니다. (모델 클래스)의 한 곳에서 유효성 검사 규칙을 선언적으로 지정할 수 있습니다 및 규칙을 어디에서 나 응용 프로그램에 적용 됩니다.

동영상 응용 프로그램에서이 유효성 검사 지원 활용을 걸릴 수 있습니다 하는 방법을 살펴보겠습니다.

## <a name="adding-validation-rules-to-the-movie-model"></a>영화 모델에 유효성 검사 규칙 추가

일부 유효성 검사 논리를 추가 하 여 먼저는 `Movie` 클래스입니다.

*Movie.cs* 파일을 엽니다. 알림 합니다 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스에 없는 `System.Web`합니다. DataAnnotations는 클래스 또는 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 집합을 제공 합니다. (또한 같은 서식 특성 포함 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 서식 지정에 도움을 유효성 검사를 제공 하지 않습니다.)

지금 업데이트 합니다 `Movie` 기본 제공 기능을 활용 하는 클래스 [ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)를 [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)를 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx), 및 [ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성입니다. 대체는 `Movie` 클래스를 다음으로:

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

합니다 [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 문자열의 최대 길이 설정 하는 특성 및이 제한은 데이터베이스의 설정, 따라서 데이터베이스 스키마가 변경 됩니다. 마우스 오른쪽 단추로 클릭 합니다 **영화** 테이블의 **서버 탐색기** 클릭 **테이블 정의 열기**:

![](adding-validation/_static/image1.png)

위의 이미지에서 문자열 필드에 설정이 모두 볼 수 있습니다 [NVARCHAR (MAX)](https://technet.microsoft.com/library/ms186939.aspx)합니다. 마이그레이션 스키마를 업데이트 하려면 사용 합니다. 솔루션을 연 다음 합니다 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.

[!code-console[Main](adding-validation/samples/sample2.cmd)]

이 명령이 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMIgration` 지정한 이름을 가진 파생 클래스 (`DataAnnotations`), 및는 `Up` 메서드 스키마 제약 조건을 업데이트 하는 코드를 볼 수 있습니다.

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

`Genre` 필드를 더 이상 null을 허용 (즉, 값을 입력 해야 합니다). 합니다 `Rating` 필드의 최대 길이 5 및 `Title` 의 최대 길이는 60입니다. 3의 최소 길이 `Title` 에서 범위 `Price` 스키마 변경을 만들지 않았습니다.

영화 스키마를 검사 합니다.

![](adding-validation/_static/image2.png)

문자열 필드 표시 새 길이 제한 및 `Genre` nullable로 확인란이 없습니다.

이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다. `Required` 및 `MinimumLength` 특성은 속성에 값이 있어야 하지만 사용자가 이 유효성 검사를 만족하기 위해 공백을 입력하는 것을 예방할 수 없다는 것을 나타냅니다. 합니다 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 특성을 사용 제한 될 수 있는 문자를 입력 합니다. 위의 코드에서 `Genre` 및 `Rating`은 문자만을 사용해야 합니다(공백, 숫자 및 특수 문자가 허용되지 않음). 합니다 [ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 특성에 지정된 된 범위 내의 값을 제한 합니다. `StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 필요에 따라 최소 길이를 설정할 수 있습니다. 값 형식 (같은 `decimal, int, float, DateTime`)은 기본적으로 필요 하 고 필요 하지 않습니다는 `Required` 특성입니다.

먼저 코드 하면 응용 프로그램 데이터베이스에 변경 내용을 저장 하기 전에 모델 클래스에서 지정 유효성 검사 규칙 적용 됩니다. 아래 코드는 throw 하는 예를 들어를 [DbEntityValidationException](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) 예외 때를 `SaveChanges` 여러 필요 하기 때문에 메서드가 호출 되 `Movie` 속성 값이 누락 되었습니다.

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

위의 코드에는 다음 예외가 throw 됩니다.

*하나 이상의 엔터티에 대 한 유효성 검사가 실패 했습니다. 자세한 내용은 'EntityValidationErrors' 속성을 참조 하세요.*

.NET Framework에 의해 자동으로 적용 하는 유효성 검사 규칙 사용 하면 확인 응용 프로그램 보다 강력 합니다. 또한 유효성 검사를 잊거나, 데이터베이스에 불량 데이터가 실수로 들어가지 않게 할 수 있습니다.

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC에서 UI 유효성 검사 오류

응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다.

클릭 합니다 **새로 만들기** 새 영화를 추가 합니다. 일부 잘못된 값으로 양식을 기입합니다. jQuery 클라이언트 쪽 유효성 검사에서 오류를 발견한 즉시 오류 메시지를 표시합니다.

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> 쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하기 위해 (",") 소수점 NuGet를 포함 해야이 자습서에서 설명한 대로 전역화 합니다.


폼에 자동으로 사용 하는 방법을 빨간색 테두리 색을 잘못 된 데이터를 포함 하 고 각각 옆에 있는 적절 한 유효성 검사 오류 메시지를 내보낼에 있는 입력란을 강조 표시를 확인 합니다. 오류는 클라이언트 쪽(JavaScript 및 jQuery 사용) 및 서버 쪽(사용자가 JavaScript를 사용하지 않도록 설정한 경우) 모두 적용됩니다.

실제 혜택은 코드 한 줄도 변경할 필요가 없었습니다 합니다 `MoviesController` 클래스 또는 합니다 *Create.cshtml* 이 유효성 검사 UI를 사용 하기 위해. 이 자습서의 앞 부분에서 만든 컨트롤러와 보기에서는 `Movie` 모델 클래스의 속성의 유효성 검사 특성을 사용하여 유효성 검사 규칙을 자동으로 선택했습니다. `Edit` 작업 메서드로 유효성 검사를 테스트하며 동일한 유효성 검사가 적용됩니다.

양식 데이터는 클라이언트 쪽 유효성 검사 오류가 없을 때까지 서버에 전송되지 않습니다. 사용 하 여 HTTP Post 메서드에 중단점을 배치 하 여이 확인할 수 있습니다 합니다 [fiddler 도구](http://fiddler2.com/fiddler2/), 또는 IE [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478)합니다.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>만들기를 살펴보고 작업 메서드를 만들어 유효성 검사에서 발생 하는 방법

컨트롤러나 보기에서 코드에 대한 업데이트 없이 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다. 다음 목록을 보여 줍니다 합니다 `Create` 의 메서드는 `MovieController` 클래스 형태입니다. 없는 것 이므로 만든 방법으로이 자습서의 앞부분에서 변경 합니다.

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

첫 번째(HTTP GET) `Create` 작업 메서드는 최초 만들기 양식을 표시합니다. 두 번째(`[HttpPost]`) 버전은 양식 게시를 처리합니다. 두 번째 `Create` 메서드(`HttpPost` 버전)은 `ModelState.IsValid`를 호출하여 동영상의 유효성 검사 오류 여부를 확인합니다. 이 메서드 호출에서는 개체에 적용된 모든 유효성 검사 특성을 평가합니다. 개체에 유효성 검사 오류가 있으면 `Create` 메서드는 양식을 다시 표시합니다. 오류가 없으면 메서드가 데이터베이스에 새 동영상을 저장합니다. 영화 예에서 **양식을 서버에 게시 되지 클라이언트측;에서 검색 하는 유효성 검사 오류가 있을 때 두 번째** `Create` **메서드가 절대 호출**합니다. 클라이언트 유효성 검사가 해제 된 경우 브라우저에서 JavaScript를 비활성화 하 고 HTTP POST `Create` 메서드 호출 `ModelState.IsValid` 동영상에 유효성 검사 오류가 있는지 확인 하려면.

`HttpPost Create` 메서드에서 중단점을 설정하고 메서드가 호출되지 않게 확인할 수 있으며, 유효성 검사 오류가 탐지되면 클라이언트 쪽 유효성 검사가 양식 데이터를 제출하지 않습니다. 브라우저에서 JavaScript를 사용하지 않으면서 오류가 있는 상태로 양식을 제출하면 중단점에 이르게 됩니다. JavaScript 없이도 전체 유효성 검사가 가능합니다. 다음 이미지에는 Internet Explorer에서 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

다음 이미지에서는 FireFox 브라우저에서 JavaScript를 사용하지 않도록 설정하는 방법을 보여 줍니다.

![](adding-validation/_static/image7.png)

다음 이미지에서는 Chrome 브라우저에서 JavaScript를 사용하지 않도록 설정하는 방법을 보여 줍니다.

![](adding-validation/_static/image8.png)

다음은 *Create.cshtml* 자습서의 앞부분에서 스 캐 폴드 하는 템플릿 보기. 이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

코드를 사용 하는 방법을 확인할 수 있습니다는 `Html.EditorFor` 도우미 출력에 `<input>` 요소 각각에 대해 `Movie` 속성. 이 도우미 옆에 있는 호출 되는 `Html.ValidationMessageFor` 도우미 메서드입니다. 이러한 두 가지 도우미 메서드를 컨트롤러에서 보기로 전달 되는 모델 개체 사용 (이 경우에 `Movie` 개체). 적절 하 게 모델 및 표시 오류 메시지에 지정 된 유효성 검사 특성에 대 한 자동으로 찾습니다.

이 방법에서는 컨트롤러나 `Create` 보기 템플릿이 실제 적용되는 유효성 검사 규칙이나, 표시되는 특정 오류 메시지에 대해 전혀 알지 못한다는 장점이 있습니다. 유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다. 이러한 유효성 검사 규칙은 `Edit` 보기와, 모델을 편집하여 만들 수 있는 다른 보기 템플릿에 자동으로 적용됩니다.

나중에 유효성 검사 논리를 변경 하려는 경우 하면 정확 하 게 한 곳에서 모델 유효성 검사 특성을 추가 하 여 (이 예는 `movie` 클래스). 모든 유효성 검사 논리가 한 곳에 정의되어 모든 곳에서 사용되므로 응용 프로그램의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다. 이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다. 수는 있습니다 됩니다 수 완벽 하 게 구분 하지 않고 있음을 의미 합니다 *DRY* 원칙입니다.

## <a name="using-datatype-attributes"></a>DataType 특성 사용

*Movie.cs* 파일을 열고 `Movie` 클래스를 확인합니다. 합니다 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에도 서식 특성을 제공 합니다. 에서는 이미 적용을 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 출시일을 가격 필드를 열거형 값입니다. 다음 코드에서는 합니다 `ReleaseDate` 하 고 `Price` 적절 한 속성 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성입니다.

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

합니다 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 데이터의 형식을 지정 하도록 뷰 엔진에 대 한 힌트만 제공 (같은 특성 제공 하 고 `<a>` URL에 대 한 및 `<a href="mailto:EmailAddress.com">` 전자 메일에 대 한 합니다. 사용할 수는 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 유효성을 검사할 데이터 형식의 특성입니다. 합니다 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 데이터베이스 내장 형식 보다 구체적인 데이터 형식을 지정 하는 데 사용 됩니다, 이들은 ***하지*** 유효성 검사 특성입니다. 이 경우에는 날짜 및 시간이 아닌 날짜만 추적하고자 합니다. 합니다 [DataType 열거형](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 와 같은 많은 데이터 형식을 제공 *날짜 "," 시간 "," PhoneNumber "," 통화 "," EmailAddress* 등입니다. `DataType` 특성을 통해 응용 프로그램에서 자동으로 유형별 기능을 제공하도록 설정할 수도 있습니다. 예를 들어, 한 `mailto:` 에 대 한 링크를 만들 수 있습니다 [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), 및 날짜 선택 기가 제공 될 수 있습니다 [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 지 원하는 브라우저에서 [HTML5](http://html5.org/). [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성에는 HTML 5 내보냅니다 [데이터](http://ejohn.org/blog/html-5-data-attributes/) (발음 *데이터 대시로*) HTML 5 브라우저가 인식할 수 있는 특성입니다. 합니다 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 유효성 검사를 제공 하지 않습니다.

`DataType.Date`는 표시되는 날짜의 서식을 지정하지 않습니다. 기본적으로 데이터 필드는 서버의 기본 형식에 따라 표시 됩니다 [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)합니다.

`DisplayFormat` 특성은 날짜 형식을 명시적으로 지정하는 데 사용됩니다.


[!code-csharp[Main](adding-validation/samples/sample8.cs)]


`ApplyFormatInEditMode` 설정은 지정 된 서식도 적용 되어야 함을 값 편집을 위해 텍스트 상자에 표시 되 면을 지정 합니다. (원하지 않을 수 있습니다 하는 일부 필드에 대 한-예를 들어 통화 값 하지 않을 텍스트 상자에 통화 기호 편집 합니다.)

사용할 수는 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 자체 하지만 특성은 일반적으로 사용 하는 것이 좋습니다는 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성도 합니다. 합니다 `DataType` 특성에 전달 합니다 *의미 체계* 데이터의 화면에 렌더링 하는 방법과 반대로으로 가져올 수 없는 다음과 같은 이점을 제공 `DisplayFormat`:

- 브라우저는 HTML5 기능 (예: 달력 컨트롤, 로캘에 적합 한 통화 기호, 이메일 링크, 등을 표시 합니다.)를 설정할 수 있습니다.
- 기본적으로 브라우저에 따라 올바른 형식을 사용 하 여 데이터는 렌더링 프로그램 [로캘](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)합니다.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성에서 데이터를 렌더링할 올바른 필드 템플릿을 선택 하는 MVC를 설정할 수 있습니다. (합니다 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 에서 사용 하는 경우 자체 템플릿을 사용 하 여 문자열). 자세한 내용은 Brad Wilson의을 참조 하세요 [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)합니다. (MVC 2 용으로 작성 된, 하지만이 문서에서는 여전히 적용를 ASP.NET MVC의 현재 버전)

사용 하는 경우는 `DataType` 특성 날짜 필드를 사용 하 여 지정 해야 합니다 `DisplayFormat` 필드 Chrome 브라우저에서 올바르게 렌더링 되도록 하기 위해도 특성입니다. 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)합니다.

> [!NOTE]
> jQuery 유효성 검사는 사용 하지 않고 합니다 [범위](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 특성 및 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)합니다. 예를 들어 다음 코드는 날짜가 지정된 범위에 있을 경우에도 클라이언트 쪽 유효성 검사 오류를 항상 표시합니다.
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> 사용 하려면 jQuery 날짜 유효성 검사를 사용 하지 않도록 설정 해야 합니다 [범위](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 특성과 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx). 없기 일반적으로 사용 하 여 모델에서 하드 날짜를 컴파일하는 것이 좋습니다 합니다 [범위](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 특성 및 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) 것이 좋습니다.


다음 코드는 한 줄에 결합 특성을 보여 줍니다.

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=6,10)]

이 시리즈의 다음 부분에서는 응용 프로그램을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.

> [!div class="step-by-step"]
> [이전](adding-a-new-field.md)
> [다음](examining-the-details-and-delete-methods.md)
