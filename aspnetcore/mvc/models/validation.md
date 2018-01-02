---
title: "ASP.NET Core MVC에서 모델 유효성 검사"
author: rachelappel
description: "ASP.NET Core MVC에서 모델 유효성 검사에 알아봅니다."
keywords: "ASP.NET Core, MVC에서 유효성 검사"
ms.author: riande
manager: wpickett
ms.date: 12/18/2016
ms.topic: article
ms.assetid: 3a8676dd-7ed8-4a05-bca2-44e288ab99ee
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/models/validation
ms.openlocfilehash: 7f641c247cb672934e76fa13bc7b7beb3990dd82
ms.sourcegitcommit: f5a7f0198628f0d152257d90dba6c3a0747a355a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2017
---
# <a name="introduction-to-model-validation-in-aspnet-core-mvc"></a>ASP.NET Core MVC에서 모델 유효성 검사 소개

으로 [Rachel Appel](https://github.com/rachelappel)

## <a name="introduction-to-model-validation"></a>모델 유효성 검사 소개

응용 프로그램 데이터베이스에 데이터를 저장 하기 전에 응용 프로그램 데이터를 확인 해야 합니다. 데이터 유형 및 크기로 적절 하 게 서식이 지정을 여 규칙을 준수 해야 하는 잠재적 보안 위협을 확인 해야 합니다. 중복 되 고 구현 하기 번거로운 울 수 있지만 유효성 검사는 필요 합니다. Mvc에서 유효성 검사는 클라이언트와 서버 모두에서 발생합니다.

다행히.NET에 유효성 검사 특성에 대 한 유효성 검사를 추상화 합니다. 이러한 특성에는 유효성 검사 코드를 작성 해야 하는 코드의 양을 줄이는 포함 합니다.

[보기 또는 GitHub에서 샘플을 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/models/validation/sample)합니다.

## <a name="validation-attributes"></a>유효성 검사 특성

유효성 검사 특성은 데이터베이스 테이블의 필드에 유효성 검사를 개념적으로 유사 하므로 모델 유효성 검사를 구성 하는 방법입니다. 데이터 형식이 나 필수 필드를 할당 하는 등 제약 조건을 포함 됩니다. 다른 종류의 유효성 검사 전자 메일 주소 또는 전화 번호, 신용 카드와 같은 비즈니스 규칙을 적용 하는 데이터 패턴을 적용 하는 합니다. 유효성 검사 특성 확인 훨씬 간단 하 고 사용 하기 쉽게 이러한 요구 사항을 적용 합니다.

다음은 이러한는 주석이 추가 된 `Movie` 동영상과 TV 프로그램에 대 한 정보를 저장 하는 응용 프로그램에서 모델입니다. 대부분의 속성 필요 하며 여러 문자열 속성에는 길이 요구 사항이입니다. 또한는에 대 한 숫자 범위 제한이 `Price` 속성을 0에서 $999.99, 사용자 지정 유효성 검사 특성을 합니다.

[!code-csharp[Main](validation/sample/Movie.cs?range=6-29)]

단순히 모델을 통해 읽을 쉽게 코드를 유지 하기 위해이 앱에 대 한 데이터에 대 한 규칙이 표시 됩니다. 다음은 여러 인기 있는 기본 제공 유효성 검사 특성입니다.

* `[CreditCard]`: 유효성을 검사 속성에는 신용 카드 형식입니다.

* `[Compare]`: 일치 하는 모델 항목에 두 속성의 유효성을 검사 합니다.

* `[EmailAddress]`: 유효성을 검사 속성에는 전자 메일 형식입니다.

* `[Phone]`: 유효성을 검사 속성에는 전화 형식입니다.

* `[Range]`: 지정된 된 범위 내에서 속성 값 변경의 유효성을 검사 합니다.

* `[RegularExpression]`: 데이터에 지정된 된 정규식과 일치 하는지 확인 합니다.

* `[Required]`: 필수 속성으로 설정 합니다.

* `[StringLength]`: 문자열 속성에 지정 된 최대 길이 최대 있는지 확인 합니다.

* `[Url]`: 유효성을 검사 속성이 URL 형식입니다.

MVC에서 파생 된 모든 특성을 지원 `ValidationAttribute` 유효성 검사를 위해서입니다. 많은 유용한 유효성 검사 특성에서 확인할 수 있습니다는 [System.ComponentModel.DataAnnotations](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations) 네임 스페이스입니다.

제공 하는 기본 제공 특성 보다 더 많은 기능을 할 수 있는 인스턴스가 있을 수 있습니다. 해당 시간에 대 한 사용자 지정 유효성 검사 특성에서 파생 하 여 만들 수 있습니다 `ValidationAttribute` 구현 하 여 모델을 변경 하거나 `IValidatableObject`합니다.

## <a name="notes-on-the-use-of-the-required-attribute"></a>필수 특성의 사용에 대 한 참고 사항

nullable 형식이 아닌 [값 형식](/dotnet/csharp/language-reference/keywords/value-types)(`decimal`, `int`, `float`,`DateTime`)은 기본적으로 필요하며 `Required` 특성은 필요하지 않습니다. 표시 된 null이 아닌 형식에 대 한 없는 서버 쪽 유효성 검사를 수행 하는 응용 프로그램 `Required`합니다.

MVC 모델 바인딩 유효성 검사 및 유효성 검사 특성으로 관련 되지 않습니다는 누락 값 또는 공백 nullable이 아닌 형식에 대 한 포함 된 양식 필드 전송을 거부 합니다. 없는 경우에는 `BindRequired` 특성 모델 바인딩 대상 속성에 양식 필드 없는 nullable이 아닌 형식에 대 한 누락 된 데이터를 무시에서 들어오는 양식 데이터입니다.

[BindRequired 특성](/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.bindrequiredattribute) (참조도 [특성으로 모델 바인딩 동작 사용자 지정](xref:mvc/models/model-binding#customize-model-binding-behavior-with-attributes))는 양식 데이터를 완료 하는 데 유용 합니다. 속성에 적용 하는 경우 모델 바인딩 시스템이 해당 속성에 대 한 값이 필요 합니다. 형식에 적용 하는 경우 모델 바인딩 시스템이 모든 해당 형식의 속성에 대 한 값이 필요 합니다.

사용 하는 경우는 [Nullable\<T > 형식](/dotnet/csharp/programming-guide/nullable-types/) (예를 들어 `decimal?` 또는 `System.Nullable<decimal>`) 하 고 표시 `Required`, 속성 (nullable 표준 형식인 경우 처럼 서버 쪽 유효성 검사가 수행 됩니다 예제에서는 한 `string`).

클라이언트 쪽 유효성 검사 모델 속성을 표시 한에 해당 하는 양식 필드의 값이 필요 `Required` 하 고 nullable이 아닌 형식 속성으로 표시 하지 않은 `Required`합니다. `Required`클라이언트 쪽 유효성 검사 오류 메시지를 제어 하 사용할 수 있습니다.

## <a name="model-state"></a>모델 상태

모델 상태 제출 된 HTML 폼 값의 유효성 검사 오류를 나타냅니다.

MVC는 계속 필드에 도달할 때까지 유효성 검사 오류 (기본적으로 200)의 최대 수입니다. 다음 코드를 삽입 하 여이 번호를 구성할 수 있습니다는 `ConfigureServices` 에서 메서드는 *Startup.cs* 파일:

[!code-csharp[Main](validation/sample/Startup.cs?range=27)]

## <a name="handling-model-state-errors"></a>처리 모델 상태 오류

모델 유효성 검사가 호출 되는 각 컨트롤러 동작 하기 전에 발생 하 고 검사 해야 하는 작업 메서드의 `ModelState.IsValid` 하 고 적절 하 게 대처 합니다. 대부분의 경우에서 적합 한 반응 이상적 모델 유효성 검사에 실패 한 이유를 자세히 보여 주는 오류 응답을 반환 하는 것입니다.

모델 유효성 검사 오류,이 경우 필터 수 이어야 이러한 정책을 구현 하는 적절 한 위치를 처리 하기 위한 표준 규칙을 따르는 일부 응용 프로그램을 선택 합니다. 유효 하지 않은 모델 상태와 작업을 수행할 때 동작 하는 방법을 테스트 해야 합니다.

## <a name="manual-validation"></a>수동 유효성 검사

모델 바인딩 및 유효성 검사 완료 되 면 일부를 반복 하는 것이 좋습니다. 예를 들어, 사용자, 정수가 필요한 필드에 텍스트 입력 한 수 또는 모델의 속성에 대 한 값을 계산 해야 할 수 있습니다.

유효성 검사를 수동으로 실행 해야 합니다. 이렇게 하려면 호출 된 `TryValidateModel` 메서드를 다음과 같이 합니다.

[!code-csharp[Main](validation/sample/MoviesController.cs?range=52)]

## <a name="custom-validation"></a>사용자 지정 유효성 검사

유효성 검사 특성에 대 한 대부분의 유효성 검사 요구 사항을 사용 됩니다. 그러나 일부 유효성 검사 규칙은 비즈니스 관련이 있습니다. 규칙을 직접 만들 필드를 확인 하는 것이 필요 하거나 값의 범위를 준수와 같은 일반적인 데이터 유효성 검사 방법 아닐 수 있습니다. 이러한 시나리오에 대 한 사용자 지정 유효성 검사 특성은이 가장 좋은 방법입니다. MVC에서 사용자 고유의 사용자 지정 유효성 검사 특성을 만들기 쉽습니다. 상속 하는 것은 `ValidationAttribute`, 재정의 `IsValid` 메서드. `IsValid` 메서드는 두 개의 매개 변수를 첫 번째는 라는 개체 *값* 고 두 번째는 `ValidationContext` 라는 개체 *validationContext*합니다. *값* 지정 유효성 검사기의 유효성을 검사할 필드의 실제 값을 나타냅니다.

다음 샘플에서는 비즈니스 규칙에 따르면 사용자가 장르를 설정 하지 않을 수 있습니다 *클래식* 1960 이후에 출시 동영상에 대 한 합니다. `[ClassicMovie]` 특성 장르를 먼저 확인 하 고 기존 인 경우 다음 검사 릴리스 날짜 이후 1960 중인지 확인 합니다. 1960 후 해제 되 면 유효성 검사가 실패 합니다. 특성은 데이터 유효성을 검사 하는 데 사용할 수 있는 연도 나타내는 정수 매개 변수를 허용 합니다. 다음과 같이 특성의 생성자에서 매개 변수의 값을 캡처할 수 있습니다.

[!code-csharp[Main](validation/sample/ClassicMovieAttribute.cs?range=9-29)]

`movie` 나타냅니다 위에 변수는 `Movie` 유효성을 검사할 양식 전송에서 데이터를 포함 하는 개체입니다. 이 경우 유효성 검사를 확인 하는 날짜에 장르는 `IsValid` 의 메서드는 `ClassicMovieAttribute` 규칙에 따라 클래스입니다. 유효성을 검사 `IsValid` 반환는 `ValidationResult.Success` 코드 시점과 유효성 검사에 실패 한 `ValidationResult` 오류 메시지와 함께 합니다. 사용자가 수정 하는 경우는 `Genre` 필드에서 폼을 전송 하 고는 `IsValid` 의 메서드는 `ClassicMovieAttribute` 영화 기존 인지 확인 합니다. 기본 제공 특성과 마찬가지로 적용 된 `ClassicMovieAttribute` 와 같은 속성에 `ReleaseDate` 앞의 코드 예제에 표시 된 대로 발생 하는 유효성 검사를 진행 하려면. 이 예제 에서만 작동 하므로 `Movie` 형식, 더 나은 옵션은 사용 하 `IValidatableObject` 다음 단락에서 표시 된 것 처럼 합니다.

구현 하 여 모델에이 동일한 코드에 배치 수는 또는 `Validate` 에서 메서드는 `IValidatableObject` 인터페이스입니다. 사용자 지정 유효성 검사 특성을 개별 속성 유효성 검사 잘 작동 하는 동안 구현 `IValidatableObject` 는 다음 그림과 같이 클래스 수준 유효성 검사를 구현 하는 데 사용할 수 있습니다.

[!code-csharp[Main](validation/sample/MovieIValidatable.cs?range=32-40)]

## <a name="client-side-validation"></a>클라이언트 쪽 유효성 검사

클라이언트 쪽 유효성 검사는 사용자에 대 한 매우 편리 합니다. 시간을 절약 그렇지 않은 경우 많은 비용이 들어가는지는 왕복에 대 한 대기 중인 서버. 비즈니스 관계에서 몇 초 부분을 곱한 수백 번 매일 추가 최대 많은 시간과 비용, 노력 합니다. 간단 하 고 즉시 유효성 검사를 사용 하면 보다 효율적으로 작동 하 고 더 좋은 품질 입력 및 출력을 생성할 수 있습니다.

여기에 표시 된 대로 작동 하도록 클라이언트 쪽 유효성 검사에 대 한 위치에서 적절 한 JavaScript 스크립트 참조 하 여 뷰에 있어야 합니다.

[!code-cshtml[Main](validation/sample/Views/Shared/_Layout.cshtml?range=37)]

[!code-cshtml[Main](validation/sample/Views/Shared/_ValidationScriptsPartial.cshtml)]

[유효성 검사 비 가시적인 jQuery](https://github.com/aspnet/jquery-validation-unobtrusive) 스크립트는 인기 있는에 작성 되는 사용자 지정 Microsoft 프런트 엔드 라이브러리 [jQuery 유효성 검사](https://jqueryvalidation.org/) 플러그 인 합니다. JQuery 비간섭 유효성 검사 없이 두 위치에서 동일한 유효성 검사 논리를 코딩 해야: 모델 속성에 대 한 서버 쪽 유효성 검사 특성에 두 번 한 다음 클라이언트 쪽 스크립트에서 다시 (jQuery 유효성 검사의에 대 한 예제 [ `validate()` ](https://jqueryvalidation.org/validate/) 메서드 표시 하 고 복잡 한 정도이 될 수 있습니다). 대신, MVC의 [태그 도우미](xref:mvc/views/tag-helpers/intro) 및 [HTML 도우미](xref:mvc/views/overview) HTML 5 렌더링 하는 모델 속성의 메타 데이터를 입력 하 고 유효성 검사 특성을 사용 하 여 [데이터 특성](http://w3c.github.io/html/dom.html#embedding-custom-non-visible-data-with-the-data-attributes) 에서 유효성 검사는 폼 요소입니다. MVC에서는 오류가 발생 하는 `data-` 기본 제공 및 사용자 지정 특성에 대 한 특성입니다. jQuery 비간섭 유효성 검사 후 구문 분석 하 thes `data-` 특성 및 jQuery 유효성 검사를 효과적으로 "복사" 서버 쪽 유효성 검사 논리를 클라이언트에는 논리를 전달 합니다. 다음과 같이 관련 태그 도우미를 사용 하 여 클라이언트에서 유효성 검사 오류를 표시할 수 있습니다.

[!code-cshtml[Main](validation/sample/Views/Movies/Create.cshtml?highlight=4,5&range=19-25)]

위의 태그 도우미 아래 HTML을 렌더링합니다. 다음에 유의 `data-` HTML의 특성에 대 한 유효성 검사 특성에 해당 출력은 `ReleaseDate` 속성입니다. `data-val-required` 특성 아래 릴리스 날짜 필드에 사용자 이름을 입력 하지 않는 경우를 표시 하려면 오류 메시지를 포함 합니다. jQuery 유효성 검사 비 가시적인 jQuery 유효성 검사에이 값을 전달 [ `required()` ](https://jqueryvalidation.org/required-method/) 다음 함께 제공 되의 해당 메시지를 표시 하는 메서드를  **\<걸쳐 >** 요소입니다.

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

폼이 유효한 될 때까지 전송을 방지 하는 클라이언트 쪽 유효성 검사 합니다. 제출 단추가 양식을 전송 또는 오류 메시지를 표시 하는 JavaScript를 실행 합니다.

MVC 유형 특성 값을 사용 하 여를 재정의할 수 있는 속성의.NET 데이터 형식을 기반으로 결정 `[DataType]` 특성입니다. 기본 `[DataType]` 특성 실제 서버 쪽 유효성 검사가 수행 되지 않습니다. 그러나 브라우저 자신의 오류 메시지를 선택 하 고 만들려는, jQuery 유효성 검사 비간섭 패키지는 메시지를 무시 하 고 다른 사용자와 일관 되 게 표시 수도 있지만 이러한 오류를 표시 합니다. 사용자를 적용할 때 가장 분명 이런 `[DataType]` 하위 클래스와 같은 `[EmailAddress]`합니다.

### <a name="add-validation-to-dynamic-forms"></a>동적 양식을에 유효성 검사 추가

유효성 검사 비 가시적인 jQuery 유효성 검사 논리 및 매개 변수 jQuery 유효성 검사 페이지 처음 로드 될 때를 전달 하기 때문에 동적으로 생성 된 양식 유효성 검사를 자동으로 발생 하지 않습니다. 대신, jQuery 비간섭 유효성 검사 만든 후 즉시 동적 폼의 구문 분석을 알려야 합니다. 예를 들어 아래 코드는 AJAX를 통해 추가 폼의 클라이언트 쪽 유효성 검사를 설정할 수 있는 방법을 보여 줍니다.

```js
$.get({
    url: "https://url/that/returns/a/form",
    dataType: "html",
    error: function(jqXHR, textStatus, errorThrown) {
        alert(textStatus + ": Could not add form. " + errorThrown);
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

`$.validator.unobtrusive.parse()` 메서드는 하나의 인수에 필요한 jQuery 선택기를 허용 합니다. 이 메서드는 jQuery의 구문 분석을 비 가시적인 유효성 검사를 지시는 `data-` 해당 선택기 내 폼의 특성입니다. 이러한 특성의 값을 양식에서 원하는 클라이언트 쪽 유효성 검사 규칙을 보여 줍니다.에 다음 jQuery 유효성 검사 플러그 인에 전달 됩니다.

### <a name="add-validation-to-dynamic-controls"></a>동적 컨트롤에 유효성 검사 추가

등의 개별 컨트롤 때에 폼에 대 한 유효성 검사 규칙을 업데이트할 수 있습니다 `<input/>`s 및 `<select/>`s, 동적으로 생성 됩니다. 이러한 요소에 대 한 선택기를 전달할 수 없습니다는 `parse()` 메서드를 직접 주변 폼 이미 구문 분석 하 고 업데이트 되지 것입니다.  대신, 있습니다 먼저 기존 유효성 검사 데이터를 제거한 다음 아래와 같이 전체 폼 재분석:

```js
$.get({
    url: "https://url/that/returns/a/control",
    dataType: "html",
    error: function(jqXHR, textStatus, errorThrown) {
        alert(textStatus + ": Could not add form. " + errorThrown);
    },
    success: function(newInputHTML) {
        var form = document.getElementById("my-form");
        form.insertAdjacentHTML("beforeend", newInputHTML);
        form.removeData("validator")    // Added by the raw jQuery Validate
            .removeData("unobtrusiveValidation");   // Added by jQuery Unobtrusive Validation
        $.validator.unobtrusive.parse(form);
    }
})
```

## <a name="iclientmodelvalidator"></a>IClientModelValidator

사용자 지정 특성에 대 한 클라이언트 쪽 논리를 만들 수 있습니다 및 [비간섭 유효성 검사](http://jqueryvalidation.org/documentation/) 클라이언트에 유효성 검사의 일부로 자동으로 실행 됩니다. 첫 번째 단계를 구현 하 여 어떤 데이터 특성 추가 제어 하는 것은 `IClientModelValidator` 다음과 같이 인터페이스:

[!code-csharp[Main](validation/sample/ClassicMovieAttribute.cs?range=30-42)]

이 인터페이스를 구현 하는 특성이 생성 된 필드를 HTML 특성을 추가할 수 있습니다. 에 대 한 출력을 검사 하는 `ReleaseDate` 요소는 이전 예제와 비슷하지만 이제는 HTML을 표시는 `data-val-classicmovie` 에 정의 된 특성의 `AddValidation` 방식의 `IClientModelValidator`합니다.

```html
<input class="form-control" type="datetime"
    data-val="true"
    data-val-classicmovie="Classic movies must have a release year earlier than 1960."
    data-val-classicmovie-year="1960"
    data-val-required="The ReleaseDate field is required."
    id="ReleaseDate" name="ReleaseDate" value="" />
```

비 가시적인 유효성 검사에서 데이터를 사용 하는 `data-` 특성 오류 메시지를 표시 합니다. 그러나 jQuery 규칙을 인식 하지 못합니다 또는 jQuery의에 추가 될 때까지 메시지 `validator` 개체입니다. 라는 메서드를 추가 하는 아래 예제에서이 확인할 `classicmovie` jQuery로 사용자 지정 클라이언트 유효성 검사 코드가 포함 된 `validator` 개체입니다.

[!code-javascript[Main](validation/sample/Views/Movies/Create.cshtml?range=71-93)]

이제 jQuery 유효성 검사 코드는 false를 반환 하는 경우 표시할 오류 메시지 뿐 아니라 사용자 지정 JavaScript 유효성 검사를 실행 하는 정보를 있습니다.

## <a name="remote-validation"></a>원격 유효성 검사

원격 유효성 검사는 서버에서 데이터에 대 한 클라이언트에서 데이터의 유효성을 검사 해야 할 때 사용할 수 있는 유용한 기능입니다. 예를 들어 앱 여부는 전자 메일 또는 사용자 이름이 이미 사용에서 되 고 많은 양의 데이터를 쿼리해야 할 수 있습니다. 하나는 유효성 검사에 대 한 데이터 집합 다운로드 큰 또는 할 필드가 단 몇 너무 많은 리소스를 소비 합니다. 중요 한 정보를 노출할 수 있습니다. 필드의 유효성을 검사 하는 왕복 요청 하는 대신이입니다.

2 단계 프로세스에서 원격 유효성 검사를 구현할 수 있습니다. 첫째, 주석으로 처리 해야 사용 하 여 모델의 `[Remote]` 특성입니다. `[Remote]` 특성 직접 클라이언트 쪽 JavaScript는 해당 코드를 호출 하는 데 사용할 수 있는 여러 오버 로드를 허용 합니다. 다음 예제에서는 가리키는 `VerifyEmail` 의 동작 메서드는 `Users` 컨트롤러입니다.

[!code-csharp[Main](validation/sample/User.cs?range=7-8)]

두 번째 단계는 지정 하는 것 유효성 검사 코드는 해당 작업 메서드에서 정의 된 대로 `[Remote]` 특성입니다. JQuery 유효성 검사에 따라 [ `remote()` ](https://jqueryvalidation.org/remote-method/) 메서드 설명서:

> Serverside 응답 해야 하는 JSON 문자열 이어야 합니다. `"true"` 유효한 요소에 대 한 일 수 있습니다 및 `"false"`, `undefined`, 또는 `null` 잘못 된 요소에 대 한 기본 오류 메시지를 사용 하 여 합니다. Serverside 응답 문자열인 경우를 제외 합니다. `"That name is already taken, try peter123 instead"`이 문자열의 기본 대신 사용자 지정 오류 메시지로 표시 됩니다.

정의 `VerifyEmail()` 메서드 아래 표시 된 대로 다음이 규칙을 따릅니다. 유효성 검사 오류가 반환 전자 메일 사용 된 경우 메시지 또는 `true` 전자 메일 것은 무료 이며 사용 하는지를 확인 하 고 결과를 래핑하는 `JsonResult` 개체입니다. 클라이언트 쪽 계속 필요한 경우 오류를 표시 하려면 반환된 된 값을 유도할 수 있습니다.

[!code-csharp[Main](validation/sample/UsersController.cs?range=19-28)]

이제 사용자가 전자 메일을 입력 하면 보기에는 JavaScript에서는 한 원격 호출을 참조 하는 경우 해당 전자 메일 작업이 수행 되 고,이 경우 오류 메시지를 표시 합니다. 그렇지 않으면 사용자는 일반적으로 폼을 제출할 수 있습니다.

`AdditionalFields` 의 속성은 `[Remote]` 특성은 조합에 서버에서 데이터에 대 한 유효성을 검사 하는 데 유용 합니다.  예를 들어 경우는 `User` 위쪽에서 모델에 라는 두 개의 추가 속성 `FirstName` 및 `LastName`, 기존 사용자가 이미 있는 해당 쌍의 이름 확인 해야 할 수 있습니다.  다음 코드 에서처럼 새 속성을 정의 합니다.

[!code-csharp[Main](validation/sample/User.cs?range=10-13)]

`AdditionalFields`설정 될 수 명시적으로 문자열에 `"FirstName"` 및 `"LastName"`, 하지만 사용 하 여는 [ `nameof` ](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/nameof) 리팩터링 나중에 다음과 같은 연산자를 간소화 합니다.  유효성 검사를 수행 하는 작업 메서드를 다음의 값에 대해 하나씩 두 개의 인수를 받아들여야 `FirstName` 및의 값에 대해 하나씩 `LastName`합니다.


[!code-csharp[Main](validation/sample/UsersController.cs?range=30-39)]

이제 때 사용자가 입력 한 이름과 성, JavaScript:

* 해당 쌍의 이름 사용 중인 경우를 확인 하려면 원격 호출을 수행 합니다.
* 쌍은 수행 된 경우 오류 메시지가 표시 됩니다. 
* 되지 않은 경우, 사용자는 양식을 전송할 수 있습니다.

두 개 이상의 추가 필드와 유효성을 검사 해야 하는 경우는 `[Remote]` 특성을 제공 하는 쉼표로 구분 된 목록으로 합니다.  예를 들어, 추가 하는 `MiddleName` 모델에 속성이 설정는 `[Remote]` 다음 코드와 같이 특성:

```cs
[Remote(action: "VerifyName", controller: "Users", AdditionalFields = nameof(FirstName) + "," + nameof(LastName))]
public string MiddleName { get; set; }
```

`AdditionalFields`모든 특성 인수가 같은 상수 식 이어야 합니다.  따라서 사용 하면 안는 [문자열 보간](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interpolated-strings) 호출 또는 [ `string.Join()` ](https://msdn.microsoft.com/en-us/library/system.string.join(v=vs.110).aspx) 초기화 `AdditionalFields`합니다. 에 추가 하는 모든 추가 필드에는 `[Remote]` 특성을 해당 컨트롤러 동작 메서드에 다른 인수를 추가 해야 합니다.
