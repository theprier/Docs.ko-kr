---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: ASP.NET 웹 페이지 (Razor) 사이트의 HTML 양식 작업 | Microsoft Docs
author: tfitzmac
description: 양식은은 텍스트 상자, 확인란, 라디오 단추, 풀 다운 목록 등의 사용자 입력 컨트롤을 배치 하는 위치는 HTML 문서의 섹션입니다. 양식을 사용 하면 wh...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: 8579c444fd19d1a366349cc09f9f768de23055f8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "28046432"
---
<a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 HTML 폼 사용
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 텍스트 상자 및 단추) (사용 하 여 HTML 폼을 처리 하는 방법을 설명에서 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 작업 하는 경우.
> 
> **학습 내용:** 
> 
> - HTML 폼을 만드는 방법.
> - 폼에서 사용자 입력을 읽고 하는 방법.
> - 사용자 입력의 유효성을 검사 하는 방법.
> - 페이지가 제출 되 양식 값을 복원 하는 방법입니다.
> 
> 프로그래밍 개념 문서에 도입 된 ASP.NET은 다음과 같습니다.
> 
> - `Request` 개체
> - 입력된 유효성 검사 합니다.
> - HTML 인코딩입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="creating-a-simple-html-form"></a>간단한 HTML 양식 만들기

1. 새 웹 사이트를 만듭니다.
2. 루트 폴더에 명명 된 웹 페이지 생성 *Form.cshtml* 다음 태그를 입력 합니다.

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. 브라우저에서 페이지를 시작 합니다. (WebMatrix에서에서 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 선택 **브라우저에서 시작**.) 세 개의 입력된 필드가 있는 간단한 양식 및 **전송** 단추가 표시 됩니다.

    ![세 가지 텍스트 상자를 사용 하 여 폼의 스크린 샷](4-working-with-forms/_static/image1.jpg)

    클릭 하면이 시점에서 **전송** 단추를 아무 일도 발생 합니다. 폼을 유용 하 게 하는 서버에서 실행 되는 일부 코드를 추가 해야 합니다.

## <a name="reading-user-input-from-the-form"></a>폼에서 사용자 입력을 읽기

폼을 처리 하려면 제출 된 필드 값을 읽고를 이러한 특정 작업을 수행 하는 코드를 추가 합니다. 이 절차는 필드를 읽고 페이지에서 사용자 입력을 표시 하는 방법을 보여 줍니다. (프로덕션 응용 프로그램에서는 일반적으로 수행한 사용자 입력으로 더욱 흥미로운 작업 합니다. 작업입니다 데이터베이스 작업에 대 한 문서에서.)

1. 맨 위에 있는 *Form.cshtml* 파일에서 다음 코드를 입력 합니다.

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    먼저 사용자가 페이지를 요청 하는 경우 빈 폼에만 표시 됩니다. (있습니다 수) 있는 사용자는 양식을 누르면 **전송**합니다. (게시)를 전송 하는이 서버에 사용자 입력 합니다. 기본적으로 동일한 페이지로 이동 (즉, *Form.cshtml*).

    이 현재 페이지를 전송 하는 경우 폼 바로 위에 입력 한 값이 표시 됩니다.

    ![페이지에 표시 하는 입력 한 값을 보여 주는 스크린 샷](4-working-with-forms/_static/image2.jpg)

    코드 페이지를 확인 합니다. 먼저 사용 하 여는 `IsPost` 페이지가 게시 되 고 있는지 여부를 확인할 수 있는 방법은 &#8212; 즉, 여부는 사용자가 클릭 한는 **전송** 단추입니다. Post, 이것이 `IsPost` true를 반환 합니다. 이것이 있는지 여부를 사용 하는 초기 요청 (GET 요청) 또는 다시 게시 (POST 요청)을 확인 하려면 ASP.NET 웹 페이지에서 표준 방법입니다. (GET 및 POST에 대 한 자세한 내용은 "HTTP GET 및 POST 및 IsPost Property" 세로 막대의 참조 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)

    사용자가 입력 하는 값을 가져오려면 다음으로 `Request.Form` 개체에 추가한 변수 나중에 적용 하도록 합니다. `Request.Form` 키로 식별 하는 각 페이지와 전송 된 모든 값을 포함 하는 개체입니다. 키는 해당 하는 고 `name` 읽으려는 양식 필드의 특성입니다. 예를 들어, 읽을 수는 `companyname` 필드 (텍스트 상자)를 사용 하면 `Request.Form["companyname"]`합니다.

    폼 값에 저장 되는 `Request.Form` 문자열로 개체입니다. 따라서는 숫자, 날짜 또는 일부 다른 형식으로 값을 사용 해야 할 때 해당 형식으로 문자열에서 변환 해야 합니다. 예제에서는 `AsInt` 의 메서드는 `Request.Form` (포함 하는 직원 수) 직원 필드의 값을 정수로 변환 하는 데 사용 됩니다.
2. 브라우저에서 페이지를 시작, 양식 필드를 입력 하 고 클릭 **전송**합니다. 페이지 입력 한 값을 표시 합니다.

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>모양 및 보안에 대 한 인코딩을 HTML
> 
> 등의 문자에 대 한 특별 한 용도로 사용할 HTML `<`, `>`, 및 `&`합니다. 이러한 특수 문자가 표시 되지 필요한 위치, 모양 및 기능 웹 페이지의 손상 수 있습니다. 브라우저에서 해석 하는 예를 들어는 `<` (에 오지 않으면 공백)는 HTML 요소의 시작으로 같은 문자 `<b>` 또는 `<input ...>`합니다. 브라우저에서 요소를 인식 하지 못하는 경우는 삭제 됩니다로 시작 하는 문자열 `<` 다시 인식 도달할 때까지 것입니다. 물론,이 페이지에서 일부 이상한 렌더링에 발생할 수 있습니다.
> 
> HTML 인코딩을 브라우저 올바른 기호로 해석 된 코드와 같은 예약 된 문자를 바꿉니다. 예를 들어는 `<` 문자 아래 템플릿으로 바뀝니다 `&lt;` 및 `>` 문자 아래 템플릿으로 바뀝니다 `&gt;`합니다. 브라우저 보려는 문자로 이러한 대체 문자열을 렌더링 합니다.
> 
> 되었기 HTML 문자열을 표시 하는 언제 든 지 인코딩을 사용 하도록 (입력) 사용자 로부터 받은 하는 것이 좋습니다. 이렇게 하지 않으면 사용자는 사용자 웹 페이지를 악성 스크립트를 실행 하거나 다른 작업을 사이트 보안을 저해 하 또는 의도 하지 않은 시도할 수 있습니다. (사용자 입력을 받아, 했지만 위치를 저장 한 다음 나중에 표시 하는 경우이 특히 중요 &#8212; 블로그 주석, 사용자 검토 또는 되죠로 예를 들어 있습니다.)
> 
> 이러한 문제를 ASP.NET 웹 페이지를 자동으로 방지 하려면 HTML로 인코딩하고 텍스트 콘텐츠를 사용자 코드에서 출력 합니다. 예를 들어, 변수 또는 같은 코드를 사용 하는 식의 내용을 표시할 때는 `@MyVar`, ASP.NET 웹 페이지는 출력을 자동으로 인코딩합니다.


## <a name="validating-user-input"></a>사용자 입력 유효성 검사

사용자 실수. 필드에 입력 하도록 요청 하면 및, 인하고 잊지 않도록 또는 직원 수를 입력 하도록 요청 하면 및 대신 이름을 입력 합니다. 을 하는 폼 채워져 올바르게 처리 하기 전에 확인 하기 위해 사용자의 입력을 검증할 수 있습니다.

이 절차에서는 사용자 하지 않았습니다 고 비워 두어도 되도록 모든 세 양식 필드의 유효성을 검사 하는 방법을 보여 줍니다. 또한 직원 수 값이 숫자 인지를 확인 합니다. 오류를 표시 합니다 오류가 있는 경우 값은 사용자에 게 알리는 메시지 유효성 검사를 통과 하지 못했습니다.

1. 에 *Form.cshtml* 파일, 코드의 첫 번째 블록을 다음 코드로 바꿉니다. 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    사용자 입력 유효성 검사를 사용 하면는 `Validation` 도우미입니다. 필수 필드를 호출 하 여 등록 `Validation.RequireField`합니다. 다른 종류의 유효성 검사를 호출 하 여 등록 `Validation.Add` 유효성을 검사할 필드와 수행할 유효성 검사의 유형을 지정 하 고 있습니다.

    페이지를 실행 하는 경우 ASP.NET 사용자에 대 한 모든 유효성 검사를 수행 합니다. 호출 하 여 결과 확인할 수 `Validation.IsValid`, 모든 항목에 전달 되 면 true를 반환 하 고 필드 유효성 검사에 실패 하면 false입니다. 일반적으로 호출 `Validation.IsValid` 전에 사용자 입력에 처리를 수행 합니다.
2. 업데이트는 `<body>` 를 세 번 호출을 추가 하 여 요소는 `Html.ValidationMessage` 다음과 같이 메서드:

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    유효성 검사 오류 메시지를 표시 하려면 Html을 호출할 수 있습니다.`ValidationMessage` 에 대 한 메시지를 원하는 필드의 이름을 전달 합니다.
3. 페이지를 실행 합니다. 필드를 비워 두고 클릭 **전송**합니다. 오류 메시지가 표시 됩니다.

    ![사용자 입력 유효성 검사를 통과 하지 못하면 오류 메시지가 표시를 보여 주는 스크린 샷](4-working-with-forms/_static/image3.jpg)
4. 문자열 (예를 들어 "ABC")을 추가 **직원 수** 필드를 클릭 **전송** 다시 합니다. 이 시간을 나타내는 오류가 표시 문자열 올바른 형식으로 정수 즉, 잘못 되었습니다.

    ![사용자가 직원 필드에 대 한 문자열을 입력 하는 경우 표시 되는 오류 메시지를 보여 주는 스크린 샷](4-working-with-forms/_static/image4.jpg)

ASP.NET 웹 페이지에는 사용자 입력을 자동으로 사용자가 브라우저에 대 한 즉각적인 피드백 얻을 수 있도록 클라이언트 스크립트를 사용 하 여 유효성 검사를 수행 하는 기능을 포함 하 여 유효성을 검사 하는 옵션이 더 제공 합니다. 참조는 [추가 리소스](#Additional_Resources) 자세한 내용은 나중에 부분입니다.

## <a name="restoring-form-values-after-postbacks"></a>포스트백 후 양식 값을 복원합니다.

이전 섹션에서 페이지를 테스트할 때 발견할 수 있습니다 하는 경우 다음 유효성 검사 오류, (잘못 된 데이터 뿐 아니라)를 입력 한 모든 항목이 제거 되었고가 모든 필드에 대 한 값을 다시 입력 해야 합니다. 중요 한 점은 들: 페이지는 처음부터 다시 만들어질 때 페이지를 제출 하 고 처리 한 다음 페이지를 다시 렌더링 합니다. 살펴본 것 처럼 즉, 전송 될 때 페이지에 있는 모든 값은 손실 됩니다.

그러나 해결할 수 있습니다이 쉽게. 전송 된 값에 액세스할 수 있습니다 (에 `Request.Form` 개체, 페이지 렌더링 될 때 다시 양식 필드에 해당 값을 채울 수 있습니다.

1. 에 *Form.cshtml* 파일, 대체는 `value` 의 특성은 `<input>` 사용 하 여 요소는 `value` 특성.: 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    `value` 특성에는 `<input>` 동적으로의 필드 값을 읽을로 설정 된 요소는 `Request.Form` 개체입니다. 처음으로 페이지를 요청 하는 값은 `Request.Form` 개체 모두 비어 있습니다. 이런 방식으로 폼 비어 있습니다. 때문에 이것이 문제가 있습니다.
2. 브라우저에서 페이지를 시작, 폼 필드에 또는 해당 비워 놓고 클릭 **전송**합니다. 제출 된 값을 보여 주는 페이지가 표시 됩니다.

    ![forms-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 자료

- [웹 사용자의 입력에 1,001 방법](https://msdn.microsoft.com/library/ms971057.aspx)
- [폼을 사용 하 고 사용자 입력 처리](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)
- [HTML 폼에서 자동 완성 사용](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
