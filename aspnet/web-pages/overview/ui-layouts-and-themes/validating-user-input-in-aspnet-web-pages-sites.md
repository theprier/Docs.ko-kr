---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 페이지 (Razor) 사이트를 Asp.net에서 사용자 입력 유효성 검사 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 사용자 로부터 얻은 정보를 확인 하는 방법을 설명 &mdash; , 있는지는 사용자가 입력 유효한 html에서 정보에서에서 forms AS...
ms.author: aspnetcontent
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: d412f3fa4ca144a8a9107c971279f7bf2663cfe5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819268"
---
<a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 사용자 입력 유효성 검사
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 사용자 로부터 얻은 정보를 확인 하는 방법을 설명 &mdash; , 있는지는 사용자가 입력 유효한 html에서 정보 forms ASP.NET Web Pages (Razor) 사이트에서.
> 
> 학습할 내용:
> 
> - 사용자의 입력을 확인 하는 방법을 정의 하는 유효성 검사 조건에 일치 합니다.
> - 모든 유효성 검사 테스트를 통과 하는지 여부를 결정 하는 방법입니다.
> - 유효성 검사 오류를 표시 하는 방법 (및 서식을 지정 하는 방법).
> - 사용자 로부터 직접 존재 하지 않는 데이터의 유효성을 검사 하는 방법.
> 
> 프로그래밍 개념 문서에 도입 된 ASP.NET은 다음과 같습니다.
> 
> - `Validation` 도우미입니다.
> - 합니다 `Html.ValidationSummary` 고 `Html.ValidationMessage` 메서드.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


이 자료에는 다음과 같은 섹션이 포함되어 있습니다.

- [사용자 입력된 유효성 검사 개요](#Overview_of_User_Input_Validation)
- [사용자 입력 유효성 검사](#Validating_User_Input)
- [클라이언트 쪽 유효성 검사 추가](#Adding_Client-Side_Validation)
- [유효성 검사 오류를 서식 지정](#Formatting_Validation_Errors)
- [사용자 로부터 직접 존재 하지 않는 데이터 유효성 검사](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>사용자 입력된 유효성 검사 개요

페이지에서 정보를 입력 하도록 요청 하는 경우-형태로 예를 들어, 입력 값이 유효한 지 확인 해야 합니다. 예를 들어, 중요 한 정보를 누락 된 폼을 처리 하지 않으려는 합니다.

사용자가 HTML 형식으로 값을 입력 하면 값을 입력 하는 문자열입니다. 대부분의 경우 필요한 값에는 정수 또는 날짜와 같은 몇 가지 다른 데이터 형식. 따라서 해야 사용자가 입력 한 값을 적절 한 데이터 형식으로 올바르게 변환 수 있는지 확인 합니다.

값에 특정 제한 해야 할 수 있습니다. 사용자가 정수를 올바르게 입력 하면 경우에 값을 특정 범위에 속하는지 확인 해야 예를 들어 있습니다.

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **중요 한** 사용자 입력 유효성 검사는 보안을 위해 중요 합니다. 폼에 입력할 수 있는 값을 제한 하는 사이트의 보안을 손상 시킬 수 있는 값을 입력할 수 누군가가 가능성이 줄어듭니다.


<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>사용자 입력 유효성 검사

ASP.NET 웹 페이지 2에서 사용할 수 있습니다는 `Validator` 사용자 입력을 테스트 하는 도우미입니다. 다음을 수행 하는 기본 방법이입니다.

1. 입력의 유효성을 검사 하려는 요소 (필드)를 결정 합니다.

    일반적으로 값을 확인할 `<input>` 요소 형식에서입니다. 그러나 같은 제약 조건이 지정 된 요소에서 제공 되는 모든 입력의 유효성을 검사 하려면 입력도 좋습니다 것을 `<select>` 목록입니다. 이렇게 하면 사용자 페이지의 제어를 우회 하 고 양식을 제출 하지 않도록 할 수 있습니다.
2. 메서드를 사용 하 여 각 입력 요소에 대 한 페이지 코드에서 각 유효성 검사를 추가 합니다 `Validation` 도우미입니다.

    필수 필드를 확인 하려면 사용 하 여 `Validation.RequireField(field, [error message])` (개별 필드)에 대 한 또는 `Validation.RequireFields(field1, field2, ...))` (목록은 필드). 다른 유형의 유효성 검사를 사용 하 여 `Validation.Add(field, ValidationType)`입니다. 에 대 한 `ValidationType`, 이러한 옵션을 사용할 수 있습니다.

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. 페이지가 제출 되 면 확인 하 여 유효성 검사를 통과 하는지 여부를 확인 `Validation.IsValid`:

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    모든 유효성 검사 오류가 있는 경우 일반적인 페이지 처리를 건너뜁니다. 예를 들어 페이지의 목적은 데이터베이스를 업데이트 하는 경우 그럴 필요가 모든 유효성 검사 오류가 수정 되었습니다.
4. 유효성 검사 오류가 있으면 오류 메시지를 표시 페이지의 태그를 사용 하 여 `Html.ValidationSummary` 또는 `Html.ValidationMessage`, 또는 둘 다.

다음 예제에서는 다음이 단계를 보여 주는 페이지를 보여 줍니다.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

유효성 검사의 작동 원리를 보려면이 페이지를 실행 하 고 의도적으로 실수입니다. 예를 들어, 다음은 페이지 모습 잊어버렸을 때 과정 이름을 입력을 입력 하는 경우는, 잘못 된 날짜를 입력 하는 경우:

![렌더링된 된 페이지에 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>클라이언트 쪽 유효성 검사 추가

기본적으로 사용자 입력 유효성을 검사할지 사용자 제출 페이지-유효성 검사 서버 코드에서 수행 되는, 합니다. 이 방식의 단점은 사용자 오류까지 후 페이지를 전송할 설정한 값을 알지는입니다. 폼 길거나 복잡 한 경우 페이지 제출 된 후에 오류를 보고 불편할 수 있습니다 사용자에 게 합니다.

클라이언트 스크립트에서 유효성 검사를 수행 하는 지원을 추가할 수 있습니다. 이 경우 사용자 브라우저에서 작업 하면서 유효성 검사가 수행 됩니다. 예를 들어, 값은 정수 여야 있는지를 지정 한다고 가정해 보겠습니다. 사용자가 정수가 아닌 값을 입력 하면 사용자가 입력 필드는 즉시 오류가 보고 됩니다. 사용자가 편리 하 게 되는 즉시 피드백을 가져옵니다. 클라이언트 기반 유효성 검사는 사용자가 여러 오류를 해결 하려면 양식을 제출 해야 하는 횟수를 줄일 수도 있습니다.

> [!NOTE]
> 클라이언트 쪽 유효성 검사를 사용 하는 경우에 유효성 검사 서버 코드에도 항상 수행 됩니다. 사용자는 클라이언트 기반 유효성 검사를 무시 하는 경우 보안을 위해는 서버 코드에서 유효성 검사를 수행 합니다.


1. 페이지에는 다음과 같은 JavaScript 라이브러리를 등록 합니다.  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   라이브러리의 두 가지 하므로 컴퓨터나 서버에 반드시 필요가 content delivery network (CDN)에서 로드할 수입니다. 그러나의 로컬 복사본이 있어야 *jquery.validate.unobtrusive.js*합니다. 경우 하지 이미 작업 중인 WebMatrix 템플릿을 사용 하 여 (같은 **시작 사이트** ) 라이브러리를 포함 하는의 기반이 되는 웹 페이지 사이트를 만들 **시작 사이트**합니다. 복사 합니다 *.js* 현재 사이트에는 파일입니다.
2. 유효성을 검사 하는 각 요소에 대 한 태그에 대 한 호출 추가 `Validation.For(field)`합니다. 이 메서드는 클라이언트 쪽 유효성 검사에 사용 되는 특성을 내보냅니다. (실제 JavaScript 코드 대신 메서드 같은 특성을 내보내는 `data-val-...`합니다. 이러한 특성 지원 jQuery를 사용 하 여 작업을 수행 하는 비 가시적인 클라이언트 유효성 검사 합니다.)

페이지에는 앞서 살펴본 예제 클라이언트 유효성 검사 기능을 추가 하는 방법을 보여 줍니다.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

일부 유효성 검사는 클라이언트에서 실행 합니다. 특히, 데이터 형식 유효성 검사 (정수, 날짜 및 등)는 클라이언트에서 실행 되지 않습니다. 다음 검사는 클라이언트와 서버 모두에서 작동합니다.

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

이 예제에서는 유효한 날짜에 대 한 테스트는 클라이언트 코드에서 작동 하지 않습니다. 그러나 테스트 서버 코드에서 수행 됩니다.

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>유효성 검사 오류를 서식 지정

다음 예약 된 이름을 포함 하는 CSS 클래스를 정의 하 여 유효성 검사 오류가 표시 되는 방식을 제어할 수 있습니다.

- `field-validation-error`. 출력을 정의 합니다 `Html.ValidationMessage` 메서드는 오류를 표시 하는 경우.
- `field-validation-valid`. 출력을 정의 합니다 `Html.ValidationMessage` 메서드 오류가 없는 경우.
- `input-validation-error`. 정의 하는 방법을 `<input>` 요소 오류가 있을 때 렌더링 됩니다. (예를 들어의 배경색을 설정 하려면이 클래스를 사용할 수 있습니다는 &lt;입력&gt; 요소 값에 유효 하지 않은 경우 다른 색입니다.) 이 CSS 클래스 (ASP.NET 웹 페이지 2)의 클라이언트 유효성 검사 중에 사용 됩니다.
- `input-validation-valid`. 모양을 정의 `<input>` 오류가 없는 경우 요소입니다.
- `validation-summary-errors`. 출력을 정의 합니다 `Html.ValidationSummary` 메서드 오류 목록을 표시 하는 것입니다.
- `validation-summary-valid`. 출력을 정의 합니다 `Html.ValidationSummary` 메서드 오류가 없는 경우.

다음 `<style>` 블록 오류 조건에 대 한 규칙을 보여 줍니다.

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

이 문서 앞부분에 나오는 예제 페이지에서이 style 블록을 포함 하는 경우 오류 표시는 다음 그림과 같이 표시 됩니다.

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> CSS 클래스에 대 한 ASP.NET 웹 페이지 2의 클라이언트 유효성 검사를 사용 하지 않는 경우는 `<input>` 요소 (`input-validation-error` 고 `input-validation-valid` 아무런 효과가 없습니다.


### <a name="static-and-dynamic-error-display"></a>정적 및 동적 오류 표시

CSS 규칙 등 쌍으로 제공 `validation-summary-errors` 고 `validation-summary-valid`입니다. 이러한 쌍 모두 조건에 대 한 규칙을 정의할 수: 오류 조건 및 "normal" (오류가 아닌) 조건입니다. 오류가 없는 경우에 오류 표시에 대 한 태그가 항상 렌더링 됨을 이해 하는 것이 반드시 합니다. 예를 들어 페이지에는 `Html.ValidationSummary` 태그에서 메서드를 페이지가 처음 요청 될 경우에 페이지 소스 다음 태그를 포함할 수는:

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

즉, 합니다 `Html.ValidationSummary` 메서드를 항상 렌더링을 `<div>` 요소 및 오류 목록이 비어 있는 경우에 목록. 마찬가지로, 합니다 `Html.ValidationMessage` 메서드를 항상 렌더링을 `<span>` 개별 필드, 오류가 발생 한 오류가 없는 경우에 자리 표시자로 요소.

상황에 따라 오류 메시지를 표시 페이지 흐름이 발생할 수 있습니다 하 고 이동할 페이지의 요소를 발생할 수 있습니다. CSS 규칙 끝나는 `-valid` 이 문제를 방지 하는 데 도움이 되는 레이아웃을 정의할 수 있습니다. 예를 들어 정의할 수 있습니다 `field-validation-error` 및 `field-validation-valid` 둘 다에 있는 동일한 고정 크기입니다. 이런 방식으로 필드의 표시 영역은 정적 이며 오류 메시지가 표시 되 면 페이지 흐름을 변경 하지 않습니다.

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>사용자 로부터 직접 존재 하지 않는 데이터 유효성 검사

때로는 HTML 양식에서 직접 존재 하지 않는 정보의 유효성을 검사 해야 합니다. 일반적인 예는 다음 예제와 같이 쿼리 문자열에서 값이 전달 하는 위치 페이지:

`http://server/myapp/EditClassInformation?classid=1022`

확인 하려는 경우 페이지에 전달 되는 값 (여기의 값에 대 한 1022 `classid`) 유효 합니다. 직접 사용할 수 없습니다는 `Validation` 도우미가 유효성이 검사를 수행 합니다. 그러나 유효성 검사 시스템 유효성 검사 오류 메시지를 표시 하는 기능 등의 다른 기능을 사용할 수 있습니다.

> [!NOTE] 
> 
> **중요** 항상에서 얻을 수 있는 값의 유효성 검사 *모든* 원본, 폼 필드 값, 쿼리 문자열 값 및 쿠키 값을 포함 합니다. (아마도 악의적인 목적) 이러한 값을 변경 하는 데는 것이 쉽습니다. 따라서 응용 프로그램을 보호 하기 위해 이러한 값을 확인 해야 합니다.


다음 예제 쿼리 문자열에 전달 되는 값을 어떻게 확인할 수 있습니다. 코드 값을 비어 있지 않고 정수 인지 테스트 합니다.

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

테스트 요청 양식을 제출 하 여 없을 때 수행 됩니다 (`if(!IsPost)`). 이 테스트는 페이지가 요청 되 면 처음 전달 하지만 요청 양식을 제출 하 여를 하는 경우에 없습니다.

이 오류를 표시할 수 오류 유효성 검사 오류의 목록에 호출 하 여 추가 `Validation.AddFormError("message")`합니다. 페이지에 대 한 호출을 포함 하는 경우는 `Html.ValidationSummary` 메서드를 오류는 사용자 입력 유효성 검사 오류와 마찬가지로 여기에서 표시 됩니다.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 사이트에서 HTML 양식 사용](https://go.microsoft.com/fwlink/?LinkID=202892)
