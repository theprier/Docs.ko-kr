---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: "사이트 (Razor) 페이지에서 ASP.NET 웹 사용자 입력 유효성 검사 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 사용자 로부터 얻은 정보를 확인 하는 방법을 설명 &mdash; 즉, 되도록 하려면 사용자가 입력 유효한 html에서 정보에에서 forms는 이름으로 저장..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 3bde2a4ea69577ebcbe3e9e89a7ee07e6ece8dd1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 사용자 입력 유효성 검사
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 사용자 로부터 얻은 정보를 확인 하는 방법을 설명 &mdash; 즉, 되도록 하려면 사용자가 입력 유효한 html에서 정보 형성 ASP.NET 웹 페이지 (Razor) 사이트에 있습니다.
> 
> 학습 내용:
> 
> - 사용자의 입력을 확인 하는 방법에는 유효성 검사 기준을 정의 하는 일치 합니다.
> - 모든 유효성 검사 테스트를 통과 하는지 여부를 확인 하는 방법입니다.
> - 유효성 검사 오류를 표시 하는 방법 (및 형식을 지정 하는 방법).
> - 사용자 로부터 직접 존재 하지 않는 데이터의 유효성을 검사 하는 방법.
> 
> 프로그래밍 개념 문서에 도입 된 ASP.NET은 다음과 같습니다.
> 
> - `Validation` 도우미입니다.
> - `Html.ValidationSummary` 및 `Html.ValidationMessage` 메서드.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


이 자료에는 다음과 같은 섹션이 포함되어 있습니다.

- [사용자 입력된 유효성 검사의 개요](#Overview_of_User_Input_Validation)
- [사용자 입력 유효성 검사](#Validating_User_Input)
- [클라이언트 쪽 유효성 검사 추가](#Adding_Client-Side_Validation)
- [유효성 검사 오류를 서식 지정](#Formatting_Validation_Errors)
- [사용자 로부터 직접 존재 하지 않는 데이터 유효성 검사](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>사용자 입력된 유효성 검사의 개요

페이지에서 정보를 입력 하도록 요청 하는 경우-예를 들어 양식에-입력 하는 값이 유효한 지 확인 해야 합니다. 예를 들어 중요 한 정보를 누락 하는 폼을 처리 하지 않으려는 경우

사용자가 HTML 형식으로 값을 입력 하면 입력 하는 값은 문자열입니다. 대부분의 경우 필요한 값은 정수 또는 날짜와 같은 몇 가지 다른 데이터 형식입니다. 따라서 사용자가 입력 한 값을 적절 한 데이터 형식으로 올바르게 변환할 수 있는지 확인 수도 있습니다.

값에 특정 제한 사항을 할 수도 있습니다. 사용자가 올바르게 정수를 입력 하는 경우에 예를 들어 해야 값이 특정 범위 내에 있는지 확인 합니다.

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **중요 한** 사용자 입력 유효성 검사는 보안을 위해 중요 합니다. 폼에 입력할 수 있는 값을 제한 하면 사이트의 보안을 손상 시킬 수 있는 값을 입력할 수 누군가가 가능성이 줄어듭니다.


<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>사용자 입력 유효성 검사

ASP.NET 웹 페이지 2에서는 사용할 수 있습니다는 `Validator` 사용자 입력을 테스트 하는 도우미입니다. 다음을 수행 하는 기본 방법이입니다.

1. 유효성을 검사 하려는 요소 (필드)는 입력을 확인 합니다.

    값의 유효성을 검사할 일반적으로 `<input>` 폼에 있는 요소입니다. 그러나 것이 좋습니다는 모든 입력 유효성 검사도 입력을 같은 제약 조건이 지정 된 요소에서 제공 되는 `<select>` 목록입니다. 이렇게 하면 사용자 페이지에 컨트롤을 무시 하 고 양식을 전송 하지 않습니다 확인 합니다.
2. 메서드를 사용 하 여 각 입력 요소에 대해 페이지 코드에서 각 유효성 검사를 추가 `Validation` 도우미입니다.

    필수 필드를 확인 하려면를 사용 하 여 `Validation.RequireField(field, [error message])` (개별 필드)에 대 한 또는 `Validation.RequireFields(field1, field2, ...))` (필드 목록)에 대 한 합니다. 다른 유형의 유효성 검사를 사용 하 여 `Validation.Add(field, ValidationType)`합니다. 에 대 한 `ValidationType`, 이러한 옵션을 사용할 수 있습니다.

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
3. 페이지가 제출 되 면 유효성 검사의 검사 하 여 통과 여부를 확인 `Validation.IsValid`:

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    유효성 검사 오류가 있을 경우 일반 페이지 처리를 건너뜁니다. 예를 들어 데이터베이스를 업데이트 하는 페이지의 목적은 이면 있습니다 하지 않은 모든 유효성 검사 오류를 해결 될 때까지 만듭니다.
4. 유효성 검사 오류가 있는 경우 오류 메시지를 표시 페이지의 태그에 사용 하 여 `Html.ValidationSummary` 또는 `Html.ValidationMessage`, 또는 둘 다 합니다.

다음 예제에서는 이러한 단계를 설명 하는 페이지를 보여 줍니다.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

유효성 검사 작업 방식를 보려면이 페이지를 실행 하 고 신중 하 게 실수입니다. 예를 들어, 페이지의 모양을 잊어버렸을 때 과정 이름 입력을 입력 하는 경우 다음은 프로그램, 잘못 된 날짜를 입력 하는 경우 및:

![렌더링된 된 페이지에서 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>클라이언트 쪽 유효성 검사 추가

기본적으로 사용자 입력의 유효성을 검사 사용자가 페이지를 전송한 후-유효성 검사 서버 코드에서 수행 되는, 즉 합니다. 이 방법의 단점은 달아 오류가까지 후 페이지가 전송 대 한 사용자가 알지 못하는입니다. 폼 길거나 복잡 한 경우 오류를 보고 하는 페이지가 제출 되 후에 불편할 수 있습니다 사용자에 게 합니다.

클라이언트 스크립트에서 유효성 검사를 수행 하는 지원을 추가할 수 있습니다. 이 경우 사용자 브라우저에서 작업 하면서 유효성 검사가 수행 됩니다. 예를 들어 값은 정수 여야 있는지를 지정 한다고 가정해 보겠습니다. 사용자가 정수가 아닌 값을 입력 하는 경우 사용자가 입력 필드는 즉시 오류가 보고 됩니다. 사용자가을 편리 하 게 즉각적인 피드백을 합니다. 클라이언트 기반 유효성 검사는 사용자를 여러 개의 오류를 해결 하려면 양식을 제출 하는 횟수를 줄일 수도 수 있습니다.

> [!NOTE]
> 클라이언트 쪽 유효성 검사를 사용 하는 경우에 유효성 검사도 항상 서버 코드에서 수행 됩니다. 서버 코드에서 유효성 검사를 수행 합니다.는 사용자가 클라이언트 기반 유효성 검사를 무시 하는 경우에 보안 조치입니다.


1. 페이지에 다음 JavaScript 라이브러리를 등록 합니다.  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

 라이브러리의 두 가지는 컴퓨터 또는 서버에 포함 시 필요 없는 (CDN) 콘텐츠 배달 네트워크에서 로드할 수 있습니다. 그러나의 로컬 복사본이 있어야 *jquery.validate.unobtrusive.js*합니다. 경우 하지 이미 사용 하는 WebMatrix 템플릿 (같은 **시작 사이트** ) 라이브러리를 포함 하는 기반으로 하는 웹 페이지 사이트 만들기, **시작 사이트**합니다. 그런 다음 복사는 *.js* 현재 사이트에는 파일입니다.
2. 유효성을 검사 하는 각 요소에 대 한 태그에 대 한 호출 추가 `Validation.For(field)`합니다. 이 메서드는 클라이언트 쪽 유효성 검사에 사용 되는 특성을 내보냅니다. (메서드가 실제 JavaScript 코드 대신 같은 특성을 내보내는 `data-val-...`합니다. 이러한 특성 지원 jQuery를 사용 하 여 작업을 수행 하는 비 가시적인 클라이언트 유효성 검사 합니다.)

다음 페이지에는 이전 예제에 클라이언트 유효성 검사 기능을 추가 하는 방법을 보여 줍니다.

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

- `field-validation-error`. 출력을 정의 `Html.ValidationMessage` 오류가 표시 된 대로 메서드.
- `field-validation-valid`. 출력을 정의 `Html.ValidationMessage` 오류가 없는 경우 방법입니다.
- `input-validation-error`. 정의 방법 `<input>` 요소는 오류가 있을 때 렌더링 됩니다. (의 배경색을 설정 하려면이 클래스를 사용할 수는 예를 들어는 &lt;입력&gt; 요소 값에 유효 하지 않을 경우 다른 색입니다.) 이 CSS 클래스 (ASP.NET 웹 페이지 2)에 클라이언트 유효성 검사 중에 사용 됩니다.
- `input-validation-valid`. 모양을 정의 `<input>` 오류가 없는 경우 요소입니다.
- `validation-summary-errors`. 출력을 정의 `Html.ValidationSummary` 의 오류 목록을 표시 된 대로 메서드.
- `validation-summary-valid`. 출력을 정의 `Html.ValidationSummary` 오류가 없는 경우 방법입니다.

다음 `<style>` 블록 오류 조건에 대 한 규칙을 보여 줍니다.

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

문서의 앞부분에 나오는 예제 페이지에서이 스타일 블록을 포함 한 경우 오류 표시는 다음 그림과 같이 표시 됩니다.

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> CSS 클래스에 대 한 ASP.NET 웹 페이지 2의 클라이언트 유효성 검사를 사용 하지 않는 경우는 `<input>` 요소 (`input-validation-error` 및 `input-validation-valid` 영향을 줄 수 없습니다.


### <a name="static-and-dynamic-error-display"></a>정적 및 동적 오류 표시

CSS 규칙 쌍으로 제공와 같은 `validation-summary-errors` 및 `validation-summary-valid`합니다. 이러한 쌍을 사용 하면 두 조건 모두에 대 한 규칙을 정의할 수 있습니다: 오류 상태와 "일반" (비 오류) 조건. 오류가 없는 경우에 오류 표시에 대 한 태그는 항상 렌더링 됨을 이해 하는 것이 유용 합니다. 예를 들어, 페이지에는 `Html.ValidationSummary` 태그에서 메서드를 페이지가 처음 요청 될 경우에 페이지 소스에 다음 태그 포함 수 됩니다.

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

즉,는 `Html.ValidationSummary` 항상 메서드를 렌더링 한 `<div>` 요소 및 오류 목록이 비어 있는 경우에 목록. 마찬가지로,는 `Html.ValidationMessage` 항상 메서드를 렌더링 한 `<span>` 오류가 없는 경우에 개별 필드 오류에 대 한 자리 표시자로 요소입니다.

경우에 따라 오류 메시지를 표시 수 흐름이 페이지 시키며, 주위를 이동할 페이지에서 요소를 일으킬 수 있습니다. 종료 되는 CSS 규칙이 `-valid` 하면이 문제를 방지 하는 데 도움이 되는 레이아웃을 정의할 수 있습니다. 예를 들어 정의할 수 있습니다 `field-validation-error` 및 `field-validation-valid` 둘 다에 있는 동일한 고정 크기입니다. 이런 방식으로 필드에 대 한 표시 영역 정적 이며 오류 메시지가 표시 되 면 페이지 흐름 변경 되지 않습니다.

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>사용자 로부터 직접 존재 하지 않는 데이터 유효성 검사

HTML 양식에서 직접 존재 하지 않는 정보의 유효성을 검사 해야 하는 경우가 있습니다. 일반적인 예는 다음 예제와 같이 쿼리 문자열의 값이 전달 하는 페이지:

`http://server/myapp/EditClassInformation?classid=1022`

이 경우 다음 사항을 확인 하려면 페이지에 전달 되는 값 (여기에서는 1022의 값에 대 한 `classid`) 유효 합니다. 직접 사용할 수 없습니다는 `Validation` 도우미가 유효성이 검사를 수행 합니다. 그러나의 유효성 검사 시스템 유효성 검사 오류 메시지를 표시 하는 기능과 같은 다른 기능을 사용할 수 있습니다.

> [!NOTE] 
> 
> **중요 한** 항상에서 얻을 수 있는 값의 유효성 검사 *모든* 양식 필드 값, 쿼리 문자열 값 및 쿠키 값을 포함 하 여 소스입니다. 사용자 (아마도 악의적인 목적) 이러한 값을 변경 하는 것이 쉽습니다. 따라서 응용 프로그램을 보호 하기 위해 이러한 값을 확인 해야 합니다.


다음 예제 쿼리 문자열에 전달 되는 값 유효성 검사 될 수 있습니다. 코드의 값이 비어 및 정수 인지 테스트 합니다.

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

테스트 요청 양식 전송이 없는 경우 수행 됩니다 (`if(!IsPost)`). 이 테스트 페이지를 요청 하는 처음으로 전달 하지만 하지 요청 양식 전송 됩니다.

이 오류를 표시 하려면 수 오류 유효성 검사 오류의 목록에 호출 하 여 추가 `Validation.AddFormError("message")`합니다. 페이지에 대 한 호출을 포함 하는 경우는 `Html.ValidationSummary` 메서드, 오류는 사용자 입력 유효성 검사 오류와 동일 하 게 여기에 표시 됩니다.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 사이트에서 HTML 폼 사용](https://go.microsoft.com/fwlink/?LinkID=202892)
