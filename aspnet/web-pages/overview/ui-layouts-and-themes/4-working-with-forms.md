---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: HTML Forms in ASP.NET Web Pages (Razor) 사이트를 사용 하 여 작업 | Microsoft Docs
author: Rick-Anderson
description: 폼에는 입력란, 확인란, 라디오 단추, 풀 다운 목록 등의 사용자 입력 컨트롤을 배치 하는 위치는 HTML 문서의 섹션입니다. 양식을 사용 하면 wh...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: de700055168f9d17167c82afe836b546160c6e91
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021617"
---
<a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 HTML 양식 사용
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 설명 텍스트 상자 및 단추) (사용 하 여 HTML 폼을 처리 하는 방법을 ASP.NET Web Pages (Razor) 웹 사이트에서 작업 하는 경우.
> 
> **학습할 내용:** 
> 
> - HTML 폼을 만드는 방법입니다.
> - 폼에서 사용자 입력을 읽는 방법.
> - 사용자 입력의 유효성을 검사 하는 방법.
> - 페이지가 제출 되 면 양식 값을 복원 하는 방법입니다.
> 
> 프로그래밍 개념 문서에 도입 된 ASP.NET은 다음과 같습니다.
> 
> - `Request` 개체
> - 입력된 유효성 검사 합니다.
> - HTML 인코딩입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="creating-a-simple-html-form"></a>간단한 HTML 폼 만들기

1. 새 웹 사이트를 만듭니다.
2. 루트 폴더에서 이라는 웹 페이지를 만듭니다 *Form.cshtml* 다음 태그를 입력 합니다.

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. 브라우저에서 페이지를 시작 합니다. (WebMatrix에서에 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 하 고 선택한 **브라우저에서 시작**.) 세 가지 입력된 필드를 사용 하 여 간단한 양식으로 **제출** 단추가 표시 됩니다.

    ![세 개의 텍스트 상자를 사용 하 여 폼의 스크린샷입니다.](4-working-with-forms/_static/image1.jpg)

    이때 클릭할 경우는 **제출** 단추를 아무 일도 발생 합니다. 폼을 유용 하 게 하려면 서버에서 실행 되는 일부 코드를 추가 해야 합니다.

## <a name="reading-user-input-from-the-form"></a>폼에서 사용자 입력을 읽기

폼을 처리 하려면 제출 된 필드 값을 읽고 해당를 사용 하 여 특정 작업을 수행 하는 코드를 추가 합니다. 이 절차에서는 필드를 읽을 페이지의 사용자 입력을 표시 하는 방법을 보여 줍니다. (프로덕션 응용 프로그램에서는 일반적으로 할 더 흥미로운 사용자 입력을 사용 합니다. 수행 하는 데이터베이스를 사용 하는 방법에 대 한 문서입니다.)

1. 맨 위에 있는 합니다 *Form.cshtml* 파일에서 다음 코드를 입력 합니다.

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    먼저 사용자가 페이지를 요청 하는 경우에 빈 폼만 표시 됩니다. (될 하면) 사용자는 양식 및 클릭 **제출**합니다. 이렇게 하면 제출 (게시물) 서버에 대 한 사용자 입력 합니다. 기본적으로 동일한 페이지로 이동 (즉, *Form.cshtml*).

    이 페이지를 제출 하면 폼 바로 위에 입력 한 값이 표시 됩니다.

    ![페이지에 표시 되는 입력 한 값을 보여 주는 스크린샷.](4-working-with-forms/_static/image2.jpg)

    페이지에 대 한 코드를 확인 합니다. 먼저 사용 하 여는 `IsPost` 페이지가 게시 되 고 있는지 여부를 결정 하는 방법 &#8212; 즉, 여부를 사용자를 클릭 하는 **제출** 단추입니다. 게시물을 경우 `IsPost` true를 반환 합니다. 이 초기 요청 (GET 요청) 또는 다시 게시 (POST 요청을)를 사용 하 여 작업할 여부를 확인 하는 표준 방법은 ASP.NET 웹 페이지의 경우 (GET 및 POST에 대 한 자세한 내용은 HTTP GET 및 POST 및 the IsPost "속성" 보충 기사를 참조 하세요 [ASP.NET 웹 페이지 Razor 구문으로 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)

    사용자가 입력 하는 값을 가져오려면 다음으로 `Request.Form` 개체를 배치할 변수에 나중에 대 한 합니다. `Request.Form` 개체를 키로 식별 되는 각 페이지를 사용 하 여 전송 된 모든 값을 포함 합니다. 키에 해당 되는 `name` 읽기 하려는 폼 필드의 특성입니다. 예를 들어 읽기는 `companyname` 필드 (텍스트 상자)를 사용 하면 `Request.Form["companyname"]`.

    폼 값에 저장 되는 `Request.Form` 문자열로 개체입니다. 따라서 숫자, 날짜 또는 다른 형식으로 값을 사용 하는 경우 해당 형식으로 문자열에서 변환 해야 합니다. 예에서는 `AsInt` 메서드는 `Request.Form` 의 직원 필드 (직원 수를 포함)의 값을 정수로 변환 하는 데 사용 됩니다.
2. 브라우저에서 페이지를 시작 폼 필드에 입력 하 고, 클릭 **제출**합니다. 페이지에 입력 한 값을 표시 합니다.

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>모양 및 보안에 대 한 인코딩을 HTML
> 
> HTML에는 같은 문자에 대 한 특별 한 용도가 `<`, `>`, 및 `&`합니다. 이러한 특수 문자가 표시 되지 예상 하는 경우 모양 및 기능 웹 페이지의 손상 수 있습니다. 브라우저에서 해석 하는 예를 들어 합니다 `<` HTML 요소의 시작 부분으로 (하지 않는 경우 그 뒤에 공백을)와 같은 문자 `<b>` 또는 `<input ...>`합니다. 시작 하는 문자열 브라우저 요소에서 인식 하지 못하는 경우 단순히 삭제 `<` 다시 인식 도달할 때까지 것입니다. 물론,이 페이지에서 일부 이상한 렌더링에 발생할 수 있습니다.
> 
> HTML 인코딩을 브라우저 올바른 기호로 해석 하는 코드를 사용 하 여 예약 된 문자를 바꿉니다. 예를 들어, 합니다 `<` 문자 바뀝니다 `&lt;` 하며 `>` 문자 바뀝니다 `&gt;`합니다. 브라우저를 보려는 문자로 이러한 대체 문자열을 렌더링 합니다.
> 
> 것이 HTML 문자열을 표시 하는 언제 든 지를 인코딩하는 데 (입력) 사용자에서 가져온 하는 것이 좋습니다. 그렇지 않으면 사용자 수에 웹 페이지나 악성 스크립트를 실행 하거나 다른 작업을 수행 하려면 사이트 보안을 손상 하는 의도 하지 않게 되는 가져오기를 시도 합니다. (사용자 입력을 받는, 위치, 저장 및 다음 나중에 표시 하는 경우이 특히 &#8212; 블로그 주석, 사용자 검토 또는 되죠으로 예를 들어.)
> 
> 이러한 문제를 ASP.NET 웹 페이지를 자동으로 방지 하는 데 HTML로 인코딩하고 모든 텍스트 콘텐츠를 코드에서 출력 합니다. 예를 들어, 변수 또는 같은 코드를 사용 하는 식의 내용을 표시할 때는 `@MyVar`, ASP.NET 웹 페이지 출력을 자동으로 인코딩합니다.


## <a name="validating-user-input"></a>사용자 입력 유효성 검사

사용자 실수를 확인합니다. 필드를 입력 하도록 요청 하면, 인하고 잊지 않도록 또는 직원 수를 입력 하도록 요청 하면 및 이름을 대신 입력 합니다. 폼에 채워진 올바르게 처리 되기 전에 있는지, 사용자 입력 유효성 검사 합니다.

이 절차에는 사용자 액세스 하지 비워 하지 않은 되도록 모든 세 가지 양식 필드의 유효성을 검사 하는 방법을 보여 줍니다. 또한 직원 개수 값을 숫자 인지를 확인 합니다. 오류가 있는 경우 오류가 표시 값을 사용자에 게 알리는 메시지 유효성 검사를 통과 하지 않았습니다.

1. 에 *Form.cshtml* 파일에서 첫 번째 코드 블록을 다음 코드로 바꿉니다. 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    사용자 입력 유효성 검사를 사용 하 여 `Validation` 도우미입니다. 필수 필드를 호출 하 여 등록할 `Validation.RequireField`합니다. 다른 유형의 유효성 검사를 호출 하 여 등록할 `Validation.Add` 유효성을 검사할 필드와 수행할 유효성 검사의 유형을 지정 하 고 있습니다.

    페이지를 실행 하는 경우 ASP.NET를 모든 유효성 검사를 수행 합니다. 호출 하 여 결과 확인할 수 있습니다 `Validation.IsValid`를 모두 전달 하는 경우 true를 반환 하는 및 필드 유효성 검사에 실패 하는 경우 false를 반환 합니다. 호출 하는 일반적으로 `Validation.IsValid` 사용자 입력 처리를 수행 하기 전에 합니다.
2. 업데이트를 `<body>` 를 세 번 호출을 추가 하 여 요소를 `Html.ValidationMessage` 다음과 같이 메서드:

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    유효성 검사 오류 메시지를 표시할 Html을 호출할 수 있습니다.`ValidationMessage` 및에 대 한 메시지는 필드의 이름을 전달 합니다.
3. 페이지를 실행 합니다. 필드를 비워 두고를 클릭 **제출**합니다. 오류 메시지가 표시 됩니다.

    ![사용자 입력 유효성 검사를 통과 하지 못한 경우 표시 되는 오류 메시지를 보여 주는 스크린샷.](4-working-with-forms/_static/image3.jpg)
4. 문자열 (예를 들어 "ABC")을 추가 합니다 **직원 수** 필드를 클릭 **제출** 다시 합니다. 이 시간을 나타내는 오류가 표시 문자열이 올바른 형식으로 즉, 정수에 없습니다.

    ![사용자가 직원 필드에 대 한 문자열을 입력 하는 경우 표시 되는 오류 메시지를 보여 주는 스크린샷.](4-working-with-forms/_static/image4.jpg)

ASP.NET 웹 페이지는 사용자가 브라우저에서 즉시 피드백을 받을 수 있도록 자동으로 클라이언트 스크립트를 사용 하 여 유효성 검사를 수행 하는 기능 등 사용자 입력 유효성 검사에 대 한 더 많은 옵션을 제공 합니다. 참조를 [레퍼런스](#Additional_Resources) 자세한 내용은 나중에 섹션.

## <a name="restoring-form-values-after-postbacks"></a>포스트백 후 복원 양식 값

이전 섹션에서 페이지를 테스트할 때 것을 알게 하는 유효성 검사 오류가 사라지고 되었습니다 (잘못 된 데이터 뿐 아니라)를 입력 한 모든 하 고 모든 필드에 값을 다시 입력 해야 합니다. 이 중요 한 점은 보여 줍니다: 페이지를 제출 하 고 처리 한 다음 페이지를 다시 렌더링 하는 경우 페이지는 처음부터 다시 생성 합니다. 살펴본 것 처럼 제출 시 된 페이지에 있는 모든 값은 손실 됩니다 것을 의미 합니다.

해결할 수 있습니다이 쉽게 있지만. 전송 된 값에 액세스할 수 있습니다 (에 `Request.Form` 개체, 페이지를 렌더링할 때 양식 필드에 다시 해당 값을 채울 수 있도록 합니다.

1. 에 *Form.cshtml* 파일, 대체를 `value` 특성의를 `<input>` 사용 하 여 요소를 `value` 특성.: 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    `value` 특성을 `<input>` 개 필드 값을 동적으로 읽을로 설정 된 요소를 `Request.Form` 개체. 처음 페이지가 요청 되는 값을 `Request.Form` 개체 모두 비어 있습니다. 이런 방식으로 폼 비어 있습니다. 때문 것입니다.
2. 브라우저에서 페이지를 시작, 양식 필드를 입력 하거나 그대로 비어 및 클릭 **제출**합니다. 제출 된 값을 보여 주는 페이지가 표시 됩니다.

    ![forms 5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [웹 사용자를 입력 하는 1,001 방법](https://msdn.microsoft.com/library/ms971057.aspx)
- [폼을 사용 하 고 사용자 입력 처리](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)
- [HTML 폼에 자동 완성 사용](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
