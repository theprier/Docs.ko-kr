---
title: ASP.NET Core MVC의 모델 유효성 검사
author: rachelappel
description: ASP.NET Core MVC의 모델 유효성 검사에 대해 알아봅니다.
ms.author: riande
ms.date: 12/18/2016
uid: mvc/models/validation
ms.openlocfilehash: 19202ffce2ce5394824b401780ce750ef7852bf7
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278894"
---
# <a name="model-validation-in-aspnet-core-mvc"></a>ASP.NET Core MVC의 모델 유효성 검사

작성자: [Rachel Appel](https://github.com/rachelappel)

## <a name="introduction-to-model-validation"></a>모델 유효성 검사 소개

앱은 데이터베이스에 데이터를 저장하기 전에 데이터를 확인해야 합니다. 데이터는 잠재적 보안 위협을 확인하고, 형식 및 크기별로 적절하게 서식이 지정되었는지 확인하고, 규칙을 준수해야 합니다. 유효성 검사는 중복되고 구현되기 번거로울 수 있지만 필요합니다. MVC에서 유효성 검사는 클라이언트와 서버 모두에서 발생합니다.

다행히 .NET는 유효성 검사를 유효성 검사 특성으로 추상화했습니다. 이러한 특성에는 유효성 검사 코드가 포함되어 작성해야 하는 코드의 양을 감소시킵니다.

[GitHub에서 샘플 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/models/validation/sample)

## <a name="validation-attributes"></a>유효성 검사 특성

유효성 검사 특성은 모델 유효성 검사를 구성하는 방법이므로 데이터베이스 테이블의 필드에 대한 유효성 검사와 개념적으로 유사합니다. 데이터 형식이나 필수 필드를 할당하는 등 제약 조건이 포함됩니다. 다른 종류의 유효성 검사에는 신용 카드, 전화 번호 또는 이메일 주소와 같은 비즈니스 규칙을 적용하기 위해 데이터에 대한 패턴을 적용하는 것이 포함됩니다. 유효성 검사 특성을 통해 훨씬 간단하고 사용하기 쉽게 이러한 요구 사항을 적용할 수 있습니다.

영화 및 TV 프로그램에 대 한 정보를 저장하는 앱에서 주석이 추가된 `Movie` 모델은 다음과 같습니다. 대부분의 속성은 필수이며 여러 문자열 속성에는 길이 요구 사항이 적용됩니다. 또한 사용자 지정 유효성 검사 특성과 함께 `Price` 속성 대신에 0~$999.99 사이라는 숫자 범위 제한이 있습니다.

[!code-csharp[](validation/sample/Movie.cs?range=6-29)]

단순히 모델을 통해 읽으면 이 앱에서 데이터에 대한 규칙을 표시하여 코드를 쉽게 유지할 수 있습니다. 널리 사용되는 여러 기본 제공 유효성 검사 특성은 다음과 같습니다.

* `[CreditCard]`: 속성에 신용 카드 형식이 있는지 유효성을 검사합니다.

* `[Compare]`: 모델의 두 속성이 일치하는지 유효성을 검사합니다.

* `[EmailAddress]`: 속성에 이메일 형식이 있는지 유효성을 검사합니다.

* `[Phone]`: 속성에 전화 번호 형식이 있는지 유효성을 검사합니다.

* `[Range]`: 지정된 범위 내에서 속성 값이 포함되는지 유효성을 검사합니다.

* `[RegularExpression]`: 데이터가 지정된 정규식과 일치하는지 유효성을 검사합니다.

* `[Required]`: 필수 속성으로 설정합니다.

* `[StringLength]`: 문자열 속성에 지정된 최대 길이가 있는지 유효성을 검사합니다.

* `[Url]`: 속성에 URL 형식이 있는지 유효성을 검사합니다.

MVC는 유효성 검사를 위해 `ValidationAttribute`에서 파생된 모든 특성을 지원합니다. 많은 유용한 유효성 검사 특성을 [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) 네임스페이스에서 확인할 수 있습니다.

제공되는 기본 제공 특성보다 더 많은 기능이 필요한 인스턴스가 있을 수 있습니다. 이 경우에 `ValidationAttribute`에서 파생하거나 `IValidatableObject`를 구현하도록 모델을 변경하여 사용자 지정 유효성 검사 특성을 만들 수 있습니다.

## <a name="notes-on-the-use-of-the-required-attribute"></a>필수 특성 사용에 대한 참고

nullable 형식이 아닌 [값 형식](/dotnet/csharp/language-reference/keywords/value-types)(`decimal`, `int`, `float`,`DateTime`)은 기본적으로 필요하며 `Required` 특성은 필요하지 않습니다. 앱은 `Required`으로 표시된 null이 아닌 형식에 서버 쪽 유효성 검사를 수행하지 않습니다.

유효성 검사 및 유효성 검사 특성과 관련되지 않는 MVC 모델 바인딩은 null이 아닌 형식에 누락 값 또는 공백을 포함하는 형식 필드 전송을 거부합니다. 대상 속성에 `BindRequired` 특성이 없는 경우에 모델 바인딩은 null이 아닌 형식에 대한 누락 데이터를 무시합니다. 여기서 들어오는 형식 데이터에서 형식 필드는 비어 있습니다.

[BindRequired 특성](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.bindrequiredattribute)([특성을 포함한 모델 바인딩 동작 사용자 지정](xref:mvc/models/model-binding#customize-model-binding-behavior-with-attributes) 참조)은 형식 데이터를 완료하는 데 유용합니다. 속성에 적용하는 경우 모델 바인딩 시스템에는 해당 속성에 대한 값이 필요합니다. 형식에 적용하는 경우 모델 바인딩 시스템에는 해당 형식의 모든 속성에 대한 값이 필요합니다.

[Nullable\<T > 형식](/dotnet/csharp/programming-guide/nullable-types/)(예: `decimal?` 또는 `System.Nullable<decimal>`)을 사용하고 `Required`으로 표시하는 경우 속성이 표준 null 형식인 것처럼 서버 쪽 유효성 검사가 수행됩니다(예: `string`).

클라이언트 쪽 유효성 검사에는 `Required`로 표시한 모델 속성에 해당하는 형식 필드에 대한 값 및 `Required`로 표시하지 않은 null이 아닌 형식 속성에 대한 값이 필요합니다. `Required`는 클라이언트 쪽 유효성 검사 오류 메시지를 제어하는 데 사용할 수 있습니다.

## <a name="model-state"></a>모델 상태

모델 상태는 제출된 HTML 형식 값으로 유효성 검사 오류를 나타냅니다.

MVC는오류의 최대 수(기본적으로 200개)에 도달할 때까지 필드를 계속 유효성 검사합니다. *Startup.cs* 파일의 `ConfigureServices` 메서드에 다음 코드를 삽입하여 이 번호를 구성할 수 있습니다.

[!code-csharp[](validation/sample/Startup.cs?range=27)]

## <a name="handling-model-state-errors"></a>모델 상태 오류 처리

모델 유효성 검사는 각 컨트롤러 작업을 호출하기 전에 발생하며, `ModelState.IsValid`를 검사하고 적절하게 반응하는 것은 작업 메서드의 책임입니다. 대부분의 경우 적합한 반응은 이상적으로 모델 유효성 검사에 실패한 이유를 자세히 보여주는 오류 응답을 반환하는 것입니다.

필터가 이러한 정책을 구현하기에 적절한 경우에 일부 앱은 모델 유효성 검사 오류를 처리하는 표준 규칙을 따르도록 선택합니다. 유효한 모델 및 잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다.

## <a name="manual-validation"></a>수동 유효성 검사

모델 바인딩 및 유효성 검사가 완료되면 일부를 반복하는 것이 좋습니다. 예를 들어 사용자는 정수가 필요한 필드에 텍스트를 입력하거나 모델의 속성에 대한 값을 계산해야 할 수 있습니다.

유효성 검사를 수동으로 실행해야 합니다. 이렇게 하려면 다음과 같이 `TryValidateModel` 메서드를 호출합니다.

[!code-csharp[](validation/sample/MoviesController.cs?range=52)]

## <a name="custom-validation"></a>사용자 지정 유효성 검사

유효성 검사 특성은 대부분의 유효성 검사 요구 사항에 적용됩니다. 그러나 일부 유효성 검사 규칙은 비즈니스에 따라 다릅니다. 규칙은 필드가 필요하거나 값의 범위를 준수하는지 확인하는 등 일반적인 데이터 유효성 검사 기술이 아닐 수 있습니다. 이러한 시나리오에서 사용자 지정 유효성 검사 특성을 사용하는 것이 좋습니다. MVC에서 고유한 사용자 지정 유효성 검사 특성을 쉽게 만들 수 있습니다. `ValidationAttribute`에서 상속하고, `IsValid` 메서드를 재정의합니다. `IsValid` 메서드는 *value*라는 개체 및 *validationContext*라는 `ValidationContext` 개체 등 두 개의 매개 변수를 허용합니다. *값*은 사용자 지정 유효성 검사기의 유효성을 검사하는 필드의 실제 값을 나타냅니다.

다음 샘플에서 비즈니스 규칙에 따르면 사용자가 1960년 이후에 출시된 영화에 대해 장르를 *클래식*으로 설정하지 않을 수 있습니다. `[ClassicMovie]` 특성은 장르를 먼저 확인하고, 클래식인 경우 출시 날짜를 확인하여 1960년보다 이후인지를 확인합니다. 1960년 이후에 출시되었다면 유효성 검사에 실패합니다. 특성은 데이터 유효성을 검사하는 데 사용할 수 있는 연도를 나타내는 정수 매개 변수를 허용합니다. 다음과 같이 특성의 생성자에서 매개 변수의 값을 캡처할 수 있습니다.

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?range=9-28)]

위의 `movie` 변수는 유효성을 검사할 형식 전송의 데이터를 포함하는 `Movie` 개체를 나타냅니다. 이 경우에 유효성 검사 코드는 규칙에 따라 `ClassicMovieAttribute` 클래스의 `IsValid` 메서드에서 날짜 및 장르를 확인합니다. 유효성을 검사하여 `IsValid`가 `ValidationResult.Success` 코드를 반환합니다. 유효성 검사에 실패하면 오류 메시지가 발생하여 `ValidationResult`가 반환됩니다.

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?range=55-58)]

사용자가 `Genre` 필드를 수정하고 형식을 제출하는 경우 `ClassicMovieAttribute`의 `IsValid` 메서드는 영화가 클래식인지 확인합니다. 기본 제공 특성과 마찬가지로 `ClassicMovieAttribute`을 `ReleaseDate`와 같은 속성에 적용하여 앞의 코드 샘플에 표시된 대로 유효성 검사를 진행합니다. 이 예제가 `Movie` 형식에서만 작동하므로 더 나은 옵션은 다음 단락에 표시된 대로 `IValidatableObject`를 사용하는 것입니다.

또는 `IValidatableObject` 인터페이스에서 `Validate` 메서드를 구현하여 모델에서 이 동일한 코드를 배치할 수 있습니다. 사용자 지정 유효성 검사 특성이 개별 속성 유효성 검사에서 잘 작동하는 반면 `IValidatableObject`를 구현하는 작업은 다음과 같이 클래스 수준 유효성 검사를 구현하는 데 사용될 수 있습니다.

[!code-csharp[](validation/sample/MovieIValidatable.cs?range=32-40)]

## <a name="client-side-validation"></a>클라이언트 쪽 유효성 검사

클라이언트 쪽 유효성 검사는 사용자에게 매우 편리합니다. 그렇지 않은 경우 서버에 대한 왕복을 기다리는 데 드는 시간을 절약할 수 있습니다. 비즈니스 용어로 몇 초를 매일 수백 번 반복하게 되면 많은 시간과 비용, 노력이 추가됩니다. 간단하고 즉각적인 유효성 검사를 사용하면 사용자는 보다 효율적으로 작업하고 더 좋은 품질의 입력 및 출력을 생성할 수 있습니다.

다음에 표시된 대로 사용할 클라이언트 쪽 유효성 검사 대신 적절한 JavaScript 스크립트 참조를 사용하는 보기가 있어야 합니다.

[!code-cshtml[](validation/sample/Views/Shared/_Layout.cshtml?range=37)]

[!code-cshtml[](validation/sample/Views/Shared/_ValidationScriptsPartial.cshtml)]

[jQuery 비간섭 유효성 검사](https://github.com/aspnet/jquery-validation-unobtrusive) 스크립트는 널리 사용되는 [jQuery 유효성 검사](https://jqueryvalidation.org/) 플러그 인에 기반한 사용자 지정 Microsoft 프런트 엔드 라이브러리입니다. jQuery 비간섭 유효성 검사를 사용하지 않고 두 위치(모델 속성에 대한 서버 쪽 유효성 검사 특성에서 한 번 및 클라이언트 쪽 스크립트에서 다시 한 번)에서 동일한 유효성 검사 논리를 코딩해야 합니다. (jQuery 유효성 검사의 [`validate()`](https://jqueryvalidation.org/validate/) 메서드에 대한 예제는 복잡함을 보여줍니다.) 대신 MVC의 [태그 도우미](xref:mvc/views/tag-helpers/intro) 및 [HTML 도우미](xref:mvc/views/overview)는 모델 속성의 유효성 검사 특성 및 형식 메타데이터를 사용하여 유효성 검사가 필요한 형식 요소에서 HTML 5 [데이터 특성](http://w3c.github.io/html/dom.html#embedding-custom-non-visible-data-with-the-data-attributes)을 렌더링할 수 있습니다. MVC에서는 기본 제공 및 사용자 지정 특성에 대한 `data-` 특성을 생성합니다. jQuery 비간섭 유효성 검사는 `data-` 특성을 구문 분석한 다음, jQuery 유효성 검사에 대한 논리를 전달하여 효과적으로 서버 쪽 유효성 검사 논리를 클라이언트에 "복사"합니다. 다음과 같이 관련 태그 도우미를 사용하여 클라이언트에서 유효성 검사 오류를 표시할 수 있습니다.

[!code-cshtml[](validation/sample/Views/Movies/Create.cshtml?highlight=4,5&range=19-25)]

위의 태그 도우미는 아래의 HTML을 렌더링합니다. HTML의 `data-` 특성 출력은 `ReleaseDate` 속성에 대한 유효성 검사 특성에 해당합니다. 아래의 `data-val-required` 특성은 사용자가 릴리스 날짜 필드를 입력하지 않았음을 표시하는 오류 메시지를 포함합니다. jQuery 비간섭 유효성 검사는 jQuery 유효성 검사 [`required()`](https://jqueryvalidation.org/required-method/) 메서드에 이 값을 전달합니다. 그러면**\<span>** 요소와 함께 해당 메시지를 표시합니다.

```html
<form action="/Movies/Create" method="post">
    <div class="form-horizontal">
        <h4>Movie</h4>
        <div class="text-danger"></div>
        <div class="form-group">
            <label class="col-md-2 control-label" for="ReleaseDate">ReleaseDate</label>
            <div class="col-md-10">
                <input class="form-control" type="datetime"
                data-val="true" data-val-required="The ReleaseDate field is required."
                id="ReleaseDate" name="ReleaseDate" value="" />
                <span class="text-danger field-validation-valid"
                data-valmsg-for="ReleaseDate" data-valmsg-replace="true"></span>
            </div>
        </div>
    </div>
</form>
```

클라이언트 쪽 유효성 검사는 형식이 유효할 때까지 전송을 방지합니다. 제출 단추는 형식을 전송하거나 오류 메시지를 표시하는 JavaScript를 실행합니다.

MVC는 속성의 .NET 데이터 형식에 따라 형식 특성 값을 결정하고 `[DataType]` 특성을 사용하여 재정의할 수 있습니다. 기본 `[DataType]` 특성은 실제 서버 쪽 유효성 검사를 수행하지 않습니다. 브라우저는 고유한 오류 메시지를 선택하고 원하는 대로 해당 오류를 표시하지만 jQuery 유효성 검사 비간섭 패키지는 이 메시지를 재정의하고 다른 메시지와 일관되게 표시할 수 있습니다. 사용자가 `[EmailAddress]`와 같은 `[DataType]` 하위 클래스를 적용할 때 가장 분명하게 발생합니다.

### <a name="add-validation-to-dynamic-forms"></a>동적 형식에 유효성 검사 추가

페이지가 처음 로드될 때 jQuery 비간섭 유효성 검사가 유효성 검사 논리 및 매개 변수를 jQuery 유효성 검사에 전달하기 때문에 동적으로 생성된 형식은 유효성 검사를 자동으로 표시하지 않습니다. 대신 jQuery 비간섭 유효성 검사에서 동적 폼을 만든 후에 즉시 구문 분석하도록 지시합니다. 예를 들어 아래 코드에서는 AJAX를 통해 추가된 형식에서 클라이언트 쪽 유효성 검사를 설정할 수 있는 방법을 보여줍니다.

```js
$.get({
    url: "https://url/that/returns/a/form",
    dataType: "html",
    error: function(jqXHR, textStatus, errorThrown) {
        alert(textStatus + ": Couldn't add form. " + errorThrown);
    },
    success: function(newFormHTML) {
        var container = document.getElementById("form-container");
        container.insertAdjacentHTML("beforeend", newFormHTML);
        var forms = container.getElementsByTagName("form");
        var newForm = forms[forms.length - 1];
        $.validator.unobtrusive.parse(newForm);
    }
})
```

`$.validator.unobtrusive.parse()` 메서드는 하나의 인수에 대해 jQuery 선택기를 허용합니다. 이 메서드는 jQuery 비간섭 유효성 검사에서 해당 선택기 내에 있는 형식의 `data-` 특성을 구문 분석하도록 지시합니다. 이러한 특성의 값은 jQuery 유효성 검사 플러그 인에 전달되므로 형식은 원하는 클라이언트 쪽 유효성 검사 규칙을 나타냅니다.

### <a name="add-validation-to-dynamic-controls"></a>동적 컨트롤에 유효성 검사 추가

`<input/>` 및 `<select/>` 등의 개별 컨트롤이 동적으로 생성될 경우 형식에 대한 유효성 검사 규칙을 업데이트할 수도 있습니다. 주변 형식이 이미 구문 분석되고 업데이트되지 않았기 때문에 이러한 요소에 대한 선택기를 `parse()` 메서드로 직접 전달할 수 없습니다. 대신 먼저 기존 유효성 검사 데이터를 제거한 다음, 아래와 같이 전체 형식을 다시 구문 분석합니다.

```js
$.get({
    url: "https://url/that/returns/a/control",
    dataType: "html",
    error: function(jqXHR, textStatus, errorThrown) {
        alert(textStatus + ": Couldn't add control. " + errorThrown);
    },
    success: function(newInputHTML) {
        var form = document.getElementById("my-form");
        form.insertAdjacentHTML("beforeend", newInputHTML);
        $(form).removeData("validator")    // Added by jQuery Validate
               .removeData("unobtrusiveValidation");   // Added by jQuery Unobtrusive Validation
        $.validator.unobtrusive.parse(form);
    }
})
```

## <a name="iclientmodelvalidator"></a>IClientModelValidator

사용자는 사용자 지정 특성에 대한 클라이언트 쪽 논리를 만들 수 있으며, [jquery 유효성 검사](http://jqueryvalidation.org/documentation/)에 어댑터를 만드는 [비간섭 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)는 클라이언트에서 유효성 검사 중에 자동으로 실행합니다. 첫 번째 단계는 다음과 같이 `IClientModelValidator` 인터페이스를 구현하여 추가할 데이터 특성을 제어하는 것입니다.

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?range=30-42)]

이 인터페이스를 구현하는 특성은 생성된 필드에 HTML 특성을 추가할 수 있습니다. `ReleaseDate` 요소에 대한 출력을 검사하면 이전 예제와 비슷한 HTML을 표시합니다. 단지 이제는 `data-val-classicmovie` 특성이 `IClientModelValidator`라는 `AddValidation` 메서드에서 정의됩니다.

```html
<input class="form-control" type="datetime"
    data-val="true"
    data-val-classicmovie="Classic movies must have a release year earlier than 1960."
    data-val-classicmovie-year="1960"
    data-val-required="The ReleaseDate field is required."
    id="ReleaseDate" name="ReleaseDate" value="" />
```

비간섭 유효성 검사는 `data-` 특성에서 데이터를 사용하여 오류 메시지를 표시합니다. 그러나 jQuery는 jQuery의 `validator` 개체에 추가될 때까지 규칙 또는 메시지를 인식하지 못합니다. 아래 예제에서 jQuery `validator` 개체에 대한 사용자 지정 클라이언트 유효성 검사 코드가 포함된 `classicmovie`라는 메서드를 추가합니다. unobtrusive.adapters.add 메서드에 대한 설명은 [여기](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)에서 확인할 수 있습니다.

[!code-javascript[](validation/sample/Views/Movies/Create.cshtml?range=71-93)]

이제 jQuery에는 유효성 검사 코드가 false를 반환하는 경우 표시할 오류 메시지뿐만 아니라 사용자 지정 JavaScript 유효성 검사를 실행하는 정보도 포함됩니다.

## <a name="remote-validation"></a>원격 유효성 검사

원격 유효성 검사는 서버의 데이터에 대한 클라이언트의 데이터 유효성을 검사해야 할 경우에 사용할 수 있는 유용한 기능입니다. 예를 들어 앱은 이메일 또는 사용자 이름을 이미 사용 중인지 확인해야 하고, 이를 위해 많은 양의 데이터를 쿼리해야 합니다. 하나 이상의 필드에 대한 유효성을 검사하는 대규모 데이터 집합을 다운로드하면 너무 많은 리소스를 소비하게 됩니다. 또한 중요한 정보를 노출할 수 있습니다. 대안은 필드의 유효성을 검사하는 왕복 요청을 수행하는 것입니다.

2단계 프로세스에서 원격 유효성 검사를 구현할 수 있습니다. 먼저 `[Remote]` 특성을 사용하여 모델을 주석으로 처리해야 합니다. `[Remote]` 특성은 클라이언트 쪽 JavaScript를 적절한 코드를 호출하는 데 사용할 수 있는 여러 오버로드를 허용합니다. 다음 예제에서는 `Users` 컨트롤러의 `VerifyEmail` 작업 메서드를 가리킵니다.

[!code-csharp[](validation/sample/User.cs?range=7-8)]

두 번째 단계는 `[Remote]` 특성에 정의된 대로 해당 작업 메서드에서 유효성 검사 코드를 지정하는 것입니다. jQuery 유효성 검사 [`remote()`](https://jqueryvalidation.org/remote-method/) 메서드 설명서에 따라:

> 서버 쪽 응답은 기본 오류 메시지를 사용하며 유효한 요소에 대해 `"true"`인 JSON 문자열이며 잘못된 요소에 대해 `"false"`, `undefined` 또는 `null`일 수 있습니다. 서버 쪽 응답이 문자열인 경우(예: `"That name is already taken, try peter123 instead"`) 이 문자열은 기본값 대신 사용자 지정 오류 메시지로 표시됩니다.

`VerifyEmail()` 메서드의 정의는 아래 표시된 대로 이러한 규칙을 따릅니다. 이메일을 사용한 경우 유효성 검사 오류 메시지가 반환됩니다. 또는 이메일이 무료인 경우 `true`이며 `JsonResult` 개체에서 결과를 래핑합니다. 클라이언트 쪽은 반환 값을 계속 사용하거나 필요한 경우 오류를 표시할 수 있습니다.

[!code-csharp[](validation/sample/UsersController.cs?range=19-28)]

이제 사용자가 이메일을 입력하면 보기의 JavaScript에서는 해당 이메일을 사용하는지 확인하기 위해 원격 호출을 수행하고, 해당하는 경우 오류 메시지를 표시합니다. 그렇지 않으면 사용자는 일반적으로 형식을 제출할 수 있습니다.

`[Remote]` 특성의 `AdditionalFields` 속성은 서버에서 데이터에 대한 필드 조합의 유효성을 검사하는 데 유용합니다. 예를 들어 위의 `User` 모델에 `FirstName` 및 `LastName`라는 두 개의 추가 속성이 있는 경우 기존 사용자가 해당 쌍의 이름을 사용하지 않는지 확인하는 것이 좋습니다. 다음 코드와 같이 새로운 속성을 정의합니다.

[!code-csharp[](validation/sample/User.cs?range=10-13)]

`AdditionalFields`는 명시적으로 `"FirstName"` 및 `"LastName"` 문자열로 설정될 수 있지만 다음과 같은 [`nameof`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/nameof) 연산자를 사용하면 나중에 리팩터링을 간소화할 수 있습니다. 유효성 검사를 수행하는 작업 메서드는 `FirstName` 값 및 `LastName` 값에 대해 하나씩 두 개의 인수를 허용해야 합니다.

[!code-csharp[](validation/sample/UsersController.cs?range=30-39)]

이제 사용자가 이름과 성을 입력할 때 JavaScript:

* 해당 쌍의 이름을 사용 중인지 확인하기 위해 원격 호출을 수행합니다.
* 쌍이 사용 중인 경우 오류 메시지가 표시됩니다. 
* 그렇지 않은 경우 사용자는 형식을 전송할 수 있습니다.

`[Remote]` 특성을 포함하는 두 개 이상의 추가 필드 유효성을 검사해야 하는 경우 쉼표로 구분된 목록으로 제공합니다. 예를 들어 `MiddleName` 특성을 메서드에 추가하고, 다음 코드에 표시된 대로 `[Remote]` 특성을 설정합니다.

```cs
[Remote(action: "VerifyName", controller: "Users", AdditionalFields = nameof(FirstName) + "," + nameof(LastName))]
public string MiddleName { get; set; }
```

모든 특성 인수와 같은 `AdditionalFields`은 상수 식이어야 합니다. 따라서 [보간된 문자열](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/interpolated-strings)을 사용하거나 [`string.Join()`](https://msdn.microsoft.com/library/system.string.join(v=vs.110).aspx)를 호출하여 `AdditionalFields`을 초기화하지 않아야 합니다. `[Remote]` 특성에 추가한 모든 추가 필드의 경우 해당하는 컨트롤러 작업 메서드에 다른 인수를 추가해야 합니다.
