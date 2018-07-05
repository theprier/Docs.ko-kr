---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor 구문 (Visual Basic)를 사용 하 여 ASP.NET 웹 프로그래밍 소개 | Microsoft Docs
author: tfitzmac
description: 이 부록 개요를 제공 ASP.NET 웹 페이지를 사용 하 여 프로그래밍의 Visual basic에서는 Razor 구문을 사용 합니다.
ms.author: aspnetcontent
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 72f995e62141df4e8f4cd082b4873d82067af8c1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816550"
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>Razor 구문 (Visual Basic)를 사용 하 여 ASP.NET 웹 프로그래밍 소개
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 프로그래밍 개요 ASP.NET 웹 페이지 Razor 구문 및 Visual Basic을 사용 하 여 합니다. ASP.NET은 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft의 기술입니다.
> 
> **학습할**:
> 
> - 프로그래밍 팁 Razor 구문을 사용 하 여 ASP.NET 웹 페이지 프로그래밍 시작 하기 위한 상위 8입니다.
> - 기본 프로그래밍 개념을 해야 합니다.
> - 어떤 ASP.NET 서버 코드 및 Razor 구문에 대 한 all입니다.
>   
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하 여 대부분의 예제 C#을 사용 합니다. 하지만 Razor 구문을 Visual Basic을 지원 합니다. 사용 하 여 웹 페이지를 만들면 Visual Basic의 ASP.NET 웹 페이지를 프로그래밍 하는 *.vbhtml* 파일 이름 확장명, Visual Basic 코드를 추가 합니다. 이 문서에서는 Visual Basic 언어 및 ASP.NET 웹 페이지를 만드는 구문을 사용 하 여 작업의 개요를 제공 합니다.

> [!NOTE]
> Microsoft WebMatrix에 대 한 기본 웹 사이트 템플릿 (**빵집**를 **사진 갤러리**, 및 **시작 사이트**등) C# 및 Visual Basic 버전에서 사용할 수 있습니다. Visual Basic 템플릿을 NuGet 패키지로 설치할 수 있습니다. 라는 폴더에 사이트의 루트 폴더에 설치 된 웹 사이트 템플릿을 *Microsoft 템플릿*합니다.


## <a name="the-top-8-programming-tips"></a>상위 8 프로그래밍 팁

이 섹션에서는 반드시 알아야 할 Razor 구문을 사용 하 여 ASP.NET 서버 코드 작성을 시작 하는 몇 가지 팁을 나열 합니다.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. 코드를 사용 하 여 페이지를 추가 하 여 @ 문자

`@` 문자 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

브라우저에 표시 된 결과:

![Razor Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 인코딩**
> 
> 사용 하 여 페이지의 콘텐츠를 표시 하는 `@` 문자를 앞의 예에서 같이 ASP.NET을 HTML로 인코딩하고 출력 합니다. 이 예약 된 HTML 문자를 대체 (같은 `<` 하 고 `>` 및 `&`) 문자가 HTML 태그 또는 엔터티로 해석 되지 않고 웹 페이지에 표시할 문자를 사용 하도록 설정 하는 코드를 사용 하 여 합니다. HTML 인코딩하지 않고 서버 코드의 출력을 올바르게 표시 되지 않 및 페이지 보안 위험에 노출 될 수 있습니다.
> 
> 목표는 태그로 태그를 렌더링 하는 HTML 태그를 출력 하는 경우 (예를 들어 `<p></p>` 단락 또는 `<em></em>` 텍스트를 강조 하기 위해), 섹션을 참조 하세요 [결합 텍스트, 태그 및 코드 블록의 코드](#BM_CombiningTextMarkupAndCode) 이 문서의 뒷부분에 나오는.
> 
> 알아볼 수 있습니다에 HTML 인코딩에 대 한 [ASP.NET Web Pages 사이트에서 HTML 양식 작업](https://go.microsoft.com/fwlink/?LinkId=202892)합니다.


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. 코드를 사용 하 여 코드 블록 안에 포함 하는 중... 종료 코드

코드 블록을 하나 이상의 코드 문을 포함 및 키워드와 함께 묶입니다 `Code` 고 `End Code`입니다. 열기를 배치할 `Code` 키워드 바로 뒤를 `@` 문자 &#8212; 간의 공백 수 없습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

브라우저에 표시 된 결과:

![Razor Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. 줄 바꿈 사용 하 여 각 코드 문 블록 내 종료

Visual Basic 코드 블록을 각 문은 줄 바꿈을 끝납니다. (이 문서의 뒷부분 표시 필요한 경우 긴 코드 문을 여러 줄으로 줄 바꿈 하는 방법입니다.)

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. 변수를 사용 하 여 값을 저장 하려면

값을 저장할 수 있습니다는 *변수*, 문자열, 숫자 및 날짜 등을 포함 합니다. 사용 하 여 새 변수를 만든를 `Dim` 키워드입니다. 사용 하 여 페이지에서 직접 변수 값을 삽입할 수는 있지만 `@`합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

브라우저에 표시 된 결과:

![Razor Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 리터럴 문자열 값 큰따옴표로 묶어야

A *문자열* 텍스트로 처리 되는 문자 시퀀스입니다. 문자열을 지정 하려면 묶습니다 큰따옴표:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

문자열 값 안에 큰따옴표를 포함 하려면 두 개의 큰따옴표 문자를 삽입 합니다. 페이지 출력에 1 번 나타나야 큰따옴표 문자를 하려는 경우 입력으로 `""` 내의 따옴표 붙은 문자열을 두 번 표시 하려는 경우 입력으로 `""""` 따옴표 붙은 문자열 내에서.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

브라우저에 표시 된 결과:

![Razor Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic 코드 대/소문자 구분 됩니다.

Visual Basic 언어는 대/소문자 구분 아닙니다. 프로그래밍 키워드 (같은 `Dim`, `If`, 및 `True`) 및 변수 이름 (같은 `myString`, 또는 `subTotal`) 어떤 경우 든 작성할 수 있습니다.

변수에 값을 할당 하는 코드의 다음 줄 `lastname` 소문자를 사용 하 여 이름을 지정 하 고 다음 대문자로 된 이름을 사용 하 여 변수 값을 출력 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

브라우저에 표시 된 결과:

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. 개체를 사용 하 여 코딩의 대부분의 작업이

개체로 사용 하 여 프로그래밍할 수 있는 것을 나타내는 &#8212; 페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등입니다. 개체 특징을 설명 하는 속성이 있습니다 &#8212; 텍스트 상자 개체의를 `Text` 속성인 요청 개체에는 `Url` 속성에는 전자 메일 메시지에는 `From` 속성을 고객 개체에는 `FirstName` 속성입니다. 개체 수도 있는 메서드를 &quot;동사&quot; 을 수행할 수 있습니다. 파일 개체의 예로 `Save` 메서드를 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드.

자주 사용 하는 `Request` 양식의 값 같은 정보를 제공 하는 개체를 요청, 페이지, 사용자 id 등의 URL을 수행 하는 브라우저 종류 (텍스트 상자, 등) 페이지에서 필드입니다. 속성에 액세스 하는 방법을 보여주는이 예제는 `Request` 개체 및 호출 하는 방법을 합니다 `MapPath` 메서드의 `Request` 서버의 페이지의 절대 경로 제공 하는 개체:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

브라우저에 표시 된 결과:

![Razor Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 의사 결정 하는 코드를 작성할 수 있습니다.

동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 확인할 수 있습니다. 이 작업을 수행 하는 가장 일반적인 방법은 된 합니다 `If` 문 (및 선택적 `Else` 문).

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

문이 `If IsPost` 작성 하는 약식 방법 `If IsPost = True`합니다. 와 함께 `If` 문 다양 한 조건에서 반복 코드 블록을 테스트 하는 방법 및 등과이 문서의 뒷부분에서 설명 합니다.

브라우저에 표시 된 결과 (클릭 한 후 **제출**):

![Razor Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET 및 POST 메서드는 IsPost 속성**
> 
> 웹 페이지 (HTTP)에 사용 되는 프로토콜은 매우 제한 된 몇 가지 지원 (&quot;동사&quot;) 서버에 요청을 확인 하는 데 사용 되는 합니다. 두 가지 자주 사용 되는 가져오기에 사용 되는 페이지를 읽으려는 및 페이지를 제출 하는 데 사용 되는 게시물입니다. 일반적으로 사용자가 페이지를 요청할 처음 페이지가 요청 될 GET을 사용 하 여 합니다. 사용자 양식을 채웁니다을 클릭 하는 경우 **제출**, 브라우저는 서버에는 POST 요청을 만듭니다.
> 
> 웹 프로그래밍에서 유용 여부는 페이지 요청 POST 또는 GET으로 페이지를 처리 하는 방법을 알 수 있도록 알아야 합니다. ASP.NET 웹 페이지에서 사용할 수는 `IsPost` 속성 GET 또는 POST 요청 인지 여부를 확인 합니다. 요청을 POST 이면는 `IsPost` 속성은 true를 반환 하 고 폼의 입력란의 값 등 읽기를 수행할 수 있습니다. 표시 되는 많은 예제 값에 따라 다르게 페이지를 처리 하는 방법을 보여 줍니다. `IsPost`합니다.


## <a name="a-simple-code-example"></a>간단한 코드 예제

이 절차에서는 기본적인 프로그래밍 기술을 설명 하는 페이지를 만드는 방법을 보여 줍니다. 예제에서는 입력 하 고 두 숫자를 추가 하 고 결과 표시 하는 사용자가 수 있는 페이지를 만듭니다.

1. 편집기에서 새 파일을 만들고 이름을 *AddNumbers.vbhtml*합니다.
2. 페이지에 이미 아무 것도 대체 페이지에 다음 코드와 태그를 복사 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    알아두어야 할 몇 가지는 다음과 같습니다.

    - 합니다 `@` 문자 페이지에서 첫 번째 코드 블록을 시작 하 고 뒤에 나오는 `totalMessage` 아래쪽에 있는 변수를 포함 합니다.
    - 페이지의 맨 위에 있는 블록으로 묶여 `Code...End Code`합니다.
    - 변수 `total`, `num1`를 `num2`, 및 `totalMessage` 여러 숫자 및 문자열을 저장 합니다.
    - 에 할당 된 리터럴 문자열 값을 `totalMessage` 큰따옴표로 변수가 합니다.
    - Visual Basic 코드 때 대/소문자를 구분 하지 않으므로 `totalMessage` 페이지 하단에 있는 변수를 사용 하는, 해당 이름을 페이지의 맨 위에 있는 변수 선언의 표기와 일치 해야 합니다. 대/소문자는 중요 하지 않습니다.
    - 식을 `num1.AsInt()`  +  `num2.AsInt()` 개체 및 메서드를 사용 하는 방법을 보여 줍니다. `AsInt` 메서드 각 변수를 추가할 수 있는 전체 숫자 (정수)는 사용자가 입력 한 문자열을 변환 합니다.
    - `<form>` 태그를 포함 한 `method="post"` 특성입니다. 사용자가 지정 하는 **추가**, 페이지 HTTP POST 메서드를 사용 하 여 서버에 전송 됩니다. 페이지가 제출 되는 경우, 코드 `If IsPost` true 나 조건부 코드를 실행, 숫자를 더한 결과 표시 합니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 두 정수를 입력 한 다음 클릭 합니다 **추가** 단추입니다.

    ![Razor Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic 언어 및 구문

이전 기본 예제 ASP.NET 웹 페이지를 만드는 방법 및 서버 코드는 HTML 태그를 추가 하는 방법을 살펴보았습니다. 여기 Visual Basic을 사용 하 여 Razor 구문을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본적인 알아봅니다 &#8212; , 프로그래밍 언어 규칙입니다.

(특히 경우 C, c + +, C#, Visual Basic 또는 JavaScript를 사용한) 프로그래밍에 익숙한 경우 어떤 매기면 많은 익숙할 것입니다. 기능을 살펴보고 WebMatrix 코드가 태그에 추가 하는 방법을 익히는 필요할 것 *.vbhtml* 파일입니다.

### <a id="BM_CombiningTextMarkupAndCode"></a>  텍스트, 태그 및 코드 블록의 코드를 결합합니다.

서버 코드 블록에서에서는 하려는 경우가 많습니다 텍스트와 태그 페이지를 출력 합니다. 서버 코드 블록을 텍스트 코드 없는 하는 대신 렌더링할지 그대로 있으면 ASP.NET 코드에서 해당 텍스트를 구분할 수 해야 합니다. 다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.

- 와 같은 HTML 블록 요소에서 텍스트를 묶으십시오 `<p></p>` 또는 `<em></em>`:

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML 요소는 텍스트, HTML 요소 추가 및 서버 코드 식에 포함할 수 있습니다. ASP.NET에서 여는 HTML 태그를 표시 하는 경우 (예를 들어 `<p>`), 모든 요소 렌더링 및 해당 콘텐츠를 브라우저 (및 서버 코드 식 확인) 하는 것입니다.

- 사용 된 `@:` 연산자 또는 `<text>` 요소입니다. 합니다 `@:` 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 콘텐츠의 단일 줄을 출력 합니다 `<text>` 요소 출력에 여러 줄을 포함 합니다. 이러한 옵션은 출력의 일부로 HTML 요소를 렌더링 하지 않을 때 유용 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    다음 예제에서는 앞의 예제를 반복 하지만 단일 쌍을 사용 하 여 `<text>` 태그를 렌더링할 텍스트를 묶으십시오.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    다음 예제에서는 `<text>` 및 `</text>` 태그는 모두 일부 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 세 줄을 묶습니다 (`<br />`), 서버 코드와 일치 하는 HTML 태그입니다. 마찬가지로 수도 앞에 개별적으로 각 줄은 `@:` 연산자; 둘 다 방식으로 작동 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > 이 섹션에 표시 된 대로 텍스트를 출력할 때 &#8212; HTML 요소를 사용 하는 `@:` 연산자와 `<text>` 요소 &#8212; ASP.NET 하지 HTML 인코딩 출력 합니다. (ASP.NET 서버 코드 식 및 서버 코드 블록 뒤에 나오는의 출력을 인코딩하는 앞에서 설명한 대로 `@`를 제외 하 고이 섹션에서 설명 하는 특수 한 현상.)

### <a name="whitespace"></a>Whitespace

문에서 (및 문자열 리터럴 외부에서) 공백이 문이 영향을 주지 않습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>긴 문을 여러 줄으로 분리

밑줄 문자를 사용 하 여 여러 줄 긴 코드 문의 중단할 수 있습니다 `_` (Visual Basic에서 호출 되는 *연속 문자*) 코드의 각 줄 끝입니다. 다음 줄으로 문 중단 하려면 줄의 끝에 공백을 차례로 연속 문자를 추가 합니다. 다음 줄에서 문을 계속 합니다. 문을 가독성을 개선 하기 위해 알아야 하는 만큼의 줄으로 래핑할 수 있습니다. 다음 문은 동일합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

그러나 문자열 리터럴로 중간 줄을 둘러쌀 수 없습니다. 다음 예제에서는 작동 하지 않습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

위의 코드와 같이 여러 줄으로 줄 바꿈되는 긴 문자열을 결합 하려면 사용 해야 합니다 *concatenation 연산자* (`&`),이 문서의 뒷부분에서 볼 수 있는 합니다.

### <a name="code-comments"></a>코드 주석

주석 자신 또는 다른 사용자에 대 한 정보를 그대로 수 있습니다. Razor 구문 주석은 붙습니다 `@*` 하 고 끝나야 `*@`합니다.

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

Razor 구문 주석은 코드 블록 내에서 사용 하거나 작은따옴표는 일반적인 Visual Basic 주석 문자를 사용할 수 있습니다 (`'`) 각 줄에 접두사로 지정 됩니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>변수

변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다. 변수를 아무 것도 이름을 지정할 수 있습니다 하지만 이름은 영문자로 시작 해야 하 고 공백 또는 예약 된 문자를 포함할 수 없습니다. Visual Basic의 경우 앞에서 본 것 처럼 변수 이름에 소문자 중요 하지 않습니다.

### <a name="variables-and-data-types"></a>변수 및 데이터 형식

변수는 어떤 종류의 데이터를 변수에 저장 됨을 나타내는 특정 데이터 형식에 있을 수 있습니다. 문자열 값을 저장 하는 문자열 변수를 할 수 있습니다 (같은 &quot;Hello world&quot;), 다양 한 형식 (예: 2012/4/12 또는 2009 년 3 월의에서 날짜 값을 저장 하는 정수 값 (예: 3 또는 79)를 저장 하는 정수 변수 및 날짜 ). 및 다른 여러 데이터 형식을 사용할 수 있습니다.

그러나 변수 형식을 지정할 필요가 없습니다. 대부분의 경우에서 ASP.NET 데이터 변수를 어떻게 사용 되 고 있는지에 따라 형식을 알아낼 수 있습니다. (형식을 지정 해야 하는 경우에 따라,이 참 이어야 하는 예제 표시 됩니다.)

변수를 선언 된 형식을 지정 하지 않고, 사용 하 여 `Dim` 및 변수 이름 (예를 들어 `Dim myVar`). 를 형식으로 변수를 선언 하려면 `Dim` 변수 이름 뒤에 더하기 `As` 유형 이름 다음에 (예를 들어 `Dim myVar As String`).

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

다음 예에서는 변수를 사용 하 여 웹 페이지에는 몇 가지 인라인 식을 보여 줍니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

브라우저에 표시 된 결과:

![Razor Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>변환 및 데이터 형식 테스트

일반적으로 ASP.NET 데이터 형식을 자동으로 확인할 수 있습니다, 있지만 경우에 따라 만들 수 없습니다. 따라서 명시적 변환을 수행 하 여 ASP.NET을 도와줄 해야 합니다. 형식을 변환 하는 것이 없는, 하는 경우에 때때로 것이 좋습니다 테스트 하려는 어떤 유형의 데이터를 작업할 수 있습니다.

가장 일반적인 경우는 정수 또는 날짜와 같은 다른 형식으로 문자열을 변환 해야 합니다. 다음 예제에서는 문자열을 숫자로 변환 해야 여기서는 일반적인 경우를 보여 줍니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

일반적으로 사용자 입력을 문자열로 제공 합니다. 숫자를 입력 하 라는 메시지가 표시 한 경우에을 때 사용자 입력을 제출 하 고 코드에서 읽을 때 숫자를 입력 한 경우에 데이터를 문자열 형식입니다. 따라서 문자열을 숫자로 변환 해야 합니다. 예에서를 변환 하지 않고 값에 산술 연산을 수행 하려는 경우 다음 오류가 발생을 ASP.NET 두 문자열을 추가할 수 없습니다.

`Cannot implicitly convert type 'string' to 'int'.`

정수 값으로 변환 하려면 호출을 `AsInt` 메서드. 변환이 성공한 경우에 다음 숫자를 추가할 수 있습니다.

다음 표에서 변수에 대 한 몇 가지 일반적인 변환 및 테스트 메서드를 나열합니다.


::: 행:::::: 열::: <strong>메서드</strong> ::: 열 끝:::::: 열::: <strong>설명</strong> ::: 열 끝:::::: 열::: <strong>예제</strong> ::: 열 끝:::::: 행 끝:::
* * *
::: 행:::::: 열::: `AsInt(), IsInt()` ::: 열 끝:::::: 열::: 정수를 나타내는 문자열을 변환 합니다 (같은 &quot;593&quot;)는 정수입니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `AsBool(), IsBool()` ::: 열 끝:::::: 열:::와 같은 문자열 변환 &quot;true&quot; 또는 &quot;false&quot; 부울 형식입니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `AsFloat(), IsFloat()` ::: 열 끝:::::: 열:::와 같은 10 진수 값이 있는 문자열로 변환 &quot;1.3&quot; 또는 &quot;7.439&quot; 부동 소수점 수입니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `AsDecimal(), IsDecimal()` ::: 종료 열:::::: 열::: 같은 10 진수 값이 있는 문자열로 변환 &quot;1.3&quot; 또는 &quot;7.439&quot; 소수입니다. (ASP.NET, 10 진수는 부동 소수점 숫자를 보다 정확 합니다.) ::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `AsDateTime(), IsDateTime()` ::: 열 끝:::::: 열::: asp.net 날짜 및 시간 값을 나타내는 문자열을 변환 `DateTime` 형식입니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `ToString()` ::: 종료 열:::::: 열::: 다른 데이터 형식 문자열로 변환 합니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    ::: 종료 열:::::: 행 끝:::


## <a name="operators"></a>연산자

연산자는 키워드 또는 식에서 수행할 수 있는 명령의 종류를 ASP.NET에 지시 하는 문자입니다. Visual Basic에서는 다양 한 연산자를 지원 하지만 ASP.NET 웹 페이지 개발을 시작 하려면 몇 가지를 인식 해야 합니다. 다음 표에서 가장 일반적인 연산자를 보여 줍니다.


::: 행:::::: 열::: <strong>연산자</strong> ::: 열 끝:::::: 열::: <strong>설명</strong> ::: 열 끝:::::: 열::: <strong>예제</strong> ::: 열 끝:::::: 행 끝:::
* * *
::: 행:::::: 열::: `+ - * /` ::: 종료 열:::::: 열::: 숫자 식에 사용 되는 수학 연산자입니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `=` ::: 종료 열:::::: 열::: 할당 및 같음. 컨텍스트에 따라 왼쪽에 있는 개체 문의 오른쪽에 있는 값을 할당 하거나 하거나 같음에 대 한 값을 확인 합니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `<>` ::: 종료 열:::::: 열::: 같지 않음. 반환 `True` 값 같지 않은 경우.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `< > <= >=` ::: 종료 열:::::: 열::: 보다 작은지, 보다 큼, 작거나 보다 같음, 및 보다 크거나 같으면 합니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `&` ::: 열 끝:::::: 열::: 연결 문자열을 조인 하는 데 사용 됩니다.
::: 종료 열:::::: 열::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `+= -=` ::: 종료 열:::::: 열:::를 추가 및 변수에서 각각 1을 뺌 증가 및 감소 연산자입니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `.` ::: 종료 열:::::: 열::: 점입니다. 개체 및 해당 속성 및 메서드를 구분 하는 데 사용 합니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `()` ::: 종료 열:::::: 열::: 괄호입니다. 그룹 식에 사용 하 여 배열 및 컬렉션의 멤버에 액세스 하는 방법에 매개 변수를 전달 합니다.
::: 종료 열:::::: 열::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `Not` ::: 종료 열:::::: 열::: 없습니다. False로 또는 그 반대로 true 값을 반대로 바꿉니다. 일반적으로 테스트 하는 약식 방법으로 사용 `False` (즉,에 대 한 없습니다 `True`).
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    ::: 종료 열:::::: 행 끝:::
* * *
::: 행:::::: 열::: `AndAlso OrElse` ::: 열 끝:::::: 열::: 논리적이 고 또는 및 연결 하는 데 사용 되는 조건 그룹화 합니다.
::: 종료 열:::::: 열::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    ::: 종료 열:::::: 행 끝:::

## <a name="working-with-file-and-folder-paths-in-code"></a>파일 및 코드의 폴더 경로 사용 하 여 작업

종종 코드에서 파일 및 폴더 경로 작업할 수 있습니다. 개발 컴퓨터에 나타나는 웹 사이트에 대 한 실제 폴더 구조의 예 다음과 같습니다.

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

Url 및 경로 대 한 몇 가지 필수 세부 정보는 다음과 같습니다.

- 도메인 이름을 사용 하 여 시작 URL (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`).
- URL은 호스트 컴퓨터의 실제 경로에 해당합니다. 예를 들어 `http://myserver` 폴더에 해당할 수 있습니다 *C:\websites\mywebsite* 서버의 합니다.
- 가상 경로 전체 경로 지정 하지 않고도 코드에서 경로 나타내는 축약형입니다. 도메인 또는 서버 이름 다음에 나오는 URL 부분을 포함 합니다. 가상 경로 사용 하는 경우에 경로 업데이트 하지 않고도 다른 도메인 또는 서버에 코드를 이동할 수 있습니다.

차이점을 이해 하는 데 예는 다음과 같습니다.

| 전체 URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| 서버 이름 | *mycompanyserver* |
| 가상 경로 | */humanresources/CompanyPolicy.htm* |
| 실제 경로 | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

가상 루트가 / 드라이브는 c:의 루트와 마찬가지로 \입니다. (가상 폴더 경로 항상 슬래시를 사용 합니다.) 폴더의 가상 경로 실제 폴더 이름이 같은 필요가 없습니다. 별칭 수 있습니다. (프로덕션 서버에서 가상 경로 거의 일치 하는 실제 경로 정확 하 게 합니다.)

코드에서 파일 및 폴더를 사용 하 여 작업할 때의 실제 경로 및 경우에 따라 사용 하는 개체에 따라 가상 경로 참조 해야 경우가 있습니다. ASP.NET이 도구를 제공 하면 이러한 코드에서 파일 및 폴더 경로 사용 하 여 작업에 대 한: 합니다 `Server.MapPath` 메서드 및 `~` 연산자 및 `Href` 메서드.

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>실제 가상 경로로 변환: Server.MapPath 메서드

합니다 `Server.MapPath` 메서드는 가상 경로 변환 (같은 */default.cshtml*) 절대 실제 경로에 (같은 *C:\WebSites\MyWebSiteFolder\default.cshtml*). 전체 실제 경로 필요할 때 언제 든이이 메서드를 사용 합니다. 일반적인 예로 읽거나 텍스트 파일 또는 웹 서버의 이미지 파일을 작성 하는 경우입니다.

일반적으로 알 수 없는 호스팅 사이트 서버의 사이트의 절대 실제 경로 알고이 메서드는 경로 변환할 수 있도록-가상 경로-를 서버에 해당 경로에 있습니다. 파일 또는 폴더 메서드에 가상 경로 전달 하 고 실제 경로 반환 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>가상 루트 참조:는 ~ 연산자 및 Href 메서드

에 *.cshtml* 또는 *.vbhtml* 파일을 사용 하 여 가상 루트 경로 참조할 수 있습니다는 `~` 연산자입니다. 사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크는 손상 되지 때문에 매우 유용 합니다. 그 어느 때 다른 위치로 웹 사이트를 이동 하는 경우에 유용 합니다. 다음은 몇 가지 예입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

웹 사이트가 `http://myserver/myapp`, 이러한 경로 페이지가 실행 될 때 ASP.NET에서 어떻게 처리 다음과 같습니다.

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

(실제로 이러한 경로 변수 값으로 표시 되지 않습니다 하지만 어떤는 처럼 ASP.NET 경로 처리 합니다.)

사용할 수는 `~` 연산자 위와 같이 서버 코드와 같이 태그에서:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

태그를 사용 하 여는 `~` 연산자를 이미지 파일, 다른 웹 페이지 및 CSS 파일 같은 리소스에 대 한 경로 만듭니다. ASP.NET 페이지 (코드 및 태그)를 통해 찾아 해결 하는 모든 페이지를 실행 하는 경우는 `~` 적절 한 경로에 대 한 참조입니다.

## <a name="conditional-logic-and-loops"></a>조건부 논리 및 루프

ASP.NET 서버 코드 하면 조건 및 루프를 실행 하는 문이 지정한 횟수 만큼 즉, 코드를 반복 하는 쓰기 코드에 따라 작업을 수행).

### <a name="testing-conditions"></a>테스트 조건

사용할 간단한 조건을 테스트 하는 `If...Then` 문이 반환 하는 `True` 또는 `False` 지정할 테스트 기준:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If` 키워드는 블록을 시작 합니다. 실제 테스트 (조건) 뒤의 `If` 키워드 및 true 또는 false를 반환 합니다. 합니다 `If` 문이 끝나는 `Then`합니다. 테스트가 참일 경우 실행할 문을 묶여 `If` 고 `End If`입니다. `If` 문을 포함할 수는 `Else` 조건이 false 인 경우 실행할 문을 지정 하는 블록:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

경우는 `If` 문이 코드 블록을 시작, 법선을 사용 하 여 필요가 `Code...End Code` 블록을 포함 하도록 문을 합니다. 추가 하기만 하면 `@` 블록에 있으며 작동 합니다. 이 방법은 사용 하 여 `If` 프로그래밍 키워드 뒤에 코드 블록을 포함 하는 다른 Visual Basic 뿐만 아니라 `For`를 `For Each`, `Do While`등입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

하나를 사용 하 여 여러 조건을 추가할 수 있습니다 `ElseIf` 블록:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

이 예제에서는 첫 번째 조건이 합니다 `If` 블록이 true가 아니면는 `ElseIf` 조건이 확인 됩니다. 조건이 충족 될 경우의 문에서 `ElseIf` 블록이 실행 됩니다. 어떤 조건 충족 되 면의 문에서 `Else` 블록이 실행 됩니다. 개수에 관계 없이 추가할 수 있습니다 `ElseIf` 블록을 닫고 사용 하 여는 `Else` 으로 차단 합니다 &quot;등등&quot; 조건.

많은 수의 조건 테스트 하려면 사용을 `Select Case` 블록:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

테스트할 값입니다 (예제에서는 요일 변수)의 괄호 안에 있는 경우 각 개별 테스트를 사용 하는 `Case` 값을 나열 하는 문입니다. 하는 경우의 값을 `Case` 문이 일치 하는 코드를 테스트 값을 `Case` 블록이 실행 됩니다.

브라우저에 표시 된 마지막 두 조건부 블록의 결과:

![Razor Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>코드를 반복합니다.

자주 반복적으로 동일한 문을 실행 해야 합니다. 반복 하 여이 작업을 수행 합니다. 예를 들어, 종종 문을 실행 하면 동일한 각 항목에 대 한 데이터의 컬렉션에서입니다. 사용할 수 있습니다 정확 하 게 하는 횟수를 반복 하려면를 알고 있는 경우는 `For` 루프입니다. 이러한 종류의 루프까지 셈 카운트다운에 특히 유용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

로 시작 하는 루프를 `For` 키워드 뒤에 세 개의 요소:

- 바로 뒤를 `For` 카운터 변수 선언 문을 (사용할 필요가 없습니다 `Dim`)에서 같이 범위, 표시 및 `i = 10 to 20`합니다. 즉, 변수의 `i` 10부터 계산을 시작 하 고 20 (포함)에 도달할 때까지 계속 됩니다.
- 간의 합니다 `For` 및 `Next` 문 블록의 내용입니다. 하나 이상의 코드 문을 실행 하는 각 루프를 사용 하 여 포함할 수 있습니다.
- `Next i` 문 루프를 종료 합니다. 카운터를 증가 하 고 루프의 다음 반복을 시작 합니다.

사이 코드 줄을 `For` 및 `Next` 줄 루프의 각 반복에 대해 실행 되는 코드를 포함 합니다. 태그를 만들고 새 단락 (`<p>` 요소) 각 시간 및의 값을 표시할 출력에 줄을 추가 i (카운터). 이 페이지를 실행 하면 항목 수를 나타내는 각 줄의 텍스트를 사용 하 여 출력을 표시 하는 11 줄을 만듭니다.

![Razor Img11](introducing-razor-syntax-vb/_static/image11.jpg)

컬렉션 또는 배열을 사용 하 여 작업할 경우 자주 사용 하는 `For Each` 루프입니다. 컬렉션은 유사한 개체의 그룹 및 `For Each` 루프는 컬렉션의 각 항목에서 작업을 수행할 수 있습니다. 이 유형의 루프는 컬렉션에 대 한 편리한 있으므로 달리는 `For` 루프 필요가 카운터를 증가 시키거나 제한을 설정 합니다. 대신는 `For Each` 루프 코드 컬렉션을 통해 완료 될 때까지 간단히 진행 합니다.

항목을 반환 하는이 예제는 `Request.ServerVariables` 컬렉션 (웹 서버에 대 한 정보 포함). 사용 하 여는 `For Each` 새 각 항목의 이름을 표시 하려면 루프 `<li>` HTML 글머리 기호 목록의 요소에에서 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each` 키워드 뒤에 컬렉션의 단일 항목을 나타내는 변수 (예에서 `myItem`) 뒤를 `In` 키워드를 반복 하려는 컬렉션에 따라 합니다. 본문에는 `For Each` 루프 앞에서 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

보다 일반적인 루프를 만들려면 사용 합니다 `Do While` 문:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

이 루프 시작의 `Do While` 반복 블록 뒤에 키워드, 조건을 뒤에 있습니다. 루프는 일반적으로 증가 (추가) 또는 감소 (에서 빼기) 변수 또는 계산에 사용 되는 개체입니다. 예에서를 `+=` 연산자 1 값을 추가 변수는 루프가 실행 될 때마다 합니다. (카운트다운 되는 루프에서 변수를 감소 시키기 위해 감소 연산자를 사용 하는 `-=`.)

## <a name="objects-and-collections"></a>개체 및 컬렉션

ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지 자체를 포함 하 여 개체입니다. 이 섹션에서는 자주 사용 하 여 코드에서 몇 가지 중요 한 개체를 설명 합니다.

### <a name="page-objects"></a>Page 개체

ASP.NET에서 가장 기본적인 개체는 페이지입니다. 조건에 맞는 개체 없이 직접 page 개체의 속성에 액세스할 수 있습니다. 다음 코드는 페이지의 파일 경로 가져오고 사용 하는 `Request` 페이지의 개체:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

속성을 사용할 수는 `Page` 와 같은 많은 정보를 가져올 개체입니다.

- `Request`. 이미 살펴보았듯이, 요청, 페이지, 사용자 id 등의 URL을 수행 하는 브라우저 종류를 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.
- `Response`. 서버 코드 실행이 완료 된 경우 브라우저에 보낼 응답 (페이지)에 대 한 정보 컬렉션입니다. 예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>컬렉션 개체 (배열 및 사전을)

컬렉션은 개체의 컬렉션과 같은 동일한 유형의 그룹 `Customer` 데이터베이스에서 개체입니다. ASP.NET와 같은 많은 기본 제공 컬렉션을 포함 합니다 `Request.Files` 컬렉션입니다.

컬렉션의 데이터를 자주 사용 됩니다. 두 가지 일반적인 컬렉션 형식은 합니다 *배열* 하며 *사전*합니다. 배열 유사 항목 컬렉션을 저장 하 고 싶지만를 각 항목을 보유 하는 별도 변수를 만들지 않으려는 경우에 유용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

배열에서 특정 데이터 형식을 선언와 같은 `String`, `Integer`, 또는 `DateTime`합니다. 변수 배열을 포함할 수 있습니다, 선언에서 변수 이름에 괄호를 추가 하 (같은 `Dim myVar() As String`). 항목의 위치 (인덱스)를 사용 하는 배열 또는 사용 하 여 액세스할 수 있습니다는 `For Each` 문입니다. 배열 인덱스는 0부터 시작 &#8212; 즉, 첫 번째 항목은에서 위치 0, 두 번째 항목은 위치 1입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

시작 하 여 배열에 있는 항목의 수를 확인할 수 있습니다 해당 `Length` 속성입니다. 배열에서 특정 항목의 위치를 가져올 수 (즉, 배열을 검색)를 사용 하 여를 `Array.IndexOf` 메서드. 수행할 수도 있습니다 역방향 등 배열의 내용을 (합니다 `Array.Reverse` 메서드) 또는 콘텐츠를 정렬 (합니다 `Array.Sort` 메서드).

브라우저에 표시 하는 문자열 배열 코드의 출력:

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

사전이 같습니다 키/값 쌍의 컬렉션을 설정 하거나 해당 값을 검색 키 (또는 이름)을 제공 하는 위치

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

사전을 만들려면를 사용 합니다 `New` 키워드는 만드는 새를 `Dictionary` 개체입니다. 사용 하 여 변수를 사전에 할당할 수 있습니다는 `Dim` 키워드입니다. 괄호를 사용 하 여 사전에 있는 항목의 데이터 형식을 ( `( )` ). 선언의 끝 실제로 새 사전을 만듭니다 하는 방법 이기 때문에 다른 괄호 쌍을 추가 해야 합니다.

사전에 항목을 추가 하려면 호출할 수 있습니다 합니다 `Add` 사전 변수의 메서드 (`myScores` 이 경우), 키 및 값을 지정 합니다. 또는 키를 나타내고 다음 예제와 같이 단순한 할당을 수행 하려면 괄호를 사용할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

사전에서 값을 가져오려면 괄호로 키를 지정 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>매개 변수를 사용 하 여 메서드를 호출합니다.

이 문서의 앞부분에서 살펴본 것 처럼 개체를 프로그래밍 하는 메서드가 있습니다. 예를 들어, 한 `Database` 개체에 있을 `Database.Connect` 메서드. 여러 방법에는 하나 이상의 매개 변수 수도 있습니다. A *매개 변수* 메서드에 전달 하는 값은 해당 작업을 완료 하는 메서드를 사용 하도록 설정 합니다. 예를 들어,에 대 한 선언을 확인 된 `Request.MapPath` 세 개의 매개 변수를 사용 하는 메서드:

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

이 메서드는 지정된 된 가상 경로에 해당 하는 서버의 실제 경로 반환 합니다. 메서드에 대 한 세 가지 매개 변수는 `virtualPath`하십시오 `baseVirtualDir`, 및 `allowCrossAppMapping`합니다. (알 수 있습니다 선언 매개 변수를 수락 하 게 하는 데이터의 데이터 형식으로 나열 됩니다.) 이 메서드를 호출 하는 경우 모든 세 매개 변수에 대 한 값을 제공 해야 합니다.

메서드에 매개 변수를 전달 하기 위한 두 가지 옵션이 Razor 구문을 사용 하 여 Visual Basic을 사용 하는 경우: *위치 매개 변수* 하거나 *명명 된 매개 변수*합니다. 위치 매개 변수를 사용 하 여 메서드를 호출 하는 엄격한 순서를 메서드 선언에 지정 된 매개 변수를 전달 합니다. (일반적으로 알 수이 순서 메서드에 대 한 설명서를 참조 하 여.) 순서를 따라야 하며 매개 변수를 건너뛸 수 없습니다 &#8212; 하는 경우 필요한 전달 하면 빈 문자열 (`""`)에 대 한 값이 없는 위치 매개 변수에 대해 null입니다.

다음 예제에서는 라는 폴더가 있다고 가정 *스크립트* 웹 사이트입니다. 호출 된 `Request.MapPath` 메서드와 전달 올바른 순서로 세 가지 매개 변수 값입니다. 다음의 결과 매핑된 경로가 표시 됩니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

메서드에 대 한 여러 매개 변수가 있는 경우 유지할 수 있습니다 코드 깔끔하고 더 읽을 수 있는 명명 된 매개 변수를 사용 하 여. 명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 뒤에 매개 변수 이름을 지정 `:=` 고 다음 값을 제공 합니다. 명명 된 매개 변수의 장점은는 원하는 순서에 관계 없이 추가할 수 있습니다. (단점은 메서드 호출으로 compact 아닙니다.)

다음 예제에서는 위와 같은 메서드를 호출 하지만 명명 된 값을 제공 하는 매개 변수를 사용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

알 수 있듯이 다른 순서로 매개 변수 전달 됩니다. 그러나 앞의 예제 및이 예제를 실행 하는 경우 동일한 값을 반환 됩니다.

## <a name="handling-errors"></a>오류 처리

### <a name="try-catch-statements"></a>Try / Catch 문

종종 컨트롤 외부 이유로 실패할 수 있는 코드에 문의 해야 합니다. 예를 들어:

- 코드를 열기, 만들기, 읽기, 또는 파일을 작성 하 려 하면 모든 종류의 오류가 발생할 수 있습니다. 원하는 파일이 존재 하지 않을, 잠긴 상태일 수 있습니다, 그리고 코드 수 하지 권한이 등.
- 마찬가지로 코드에는 데이터베이스의 레코드를 업데이트 하려고 하는 경우 사용 권한 문제가 발생할 수, 데이터베이스에 연결이 삭제 될 수 있습니다, 그리고 잘못 된 경우 등에 데이터를 저장할 수 있습니다.

프로그래밍 측면에서 이러한 상황 이라고 *예외*합니다. 코드에서 예외가 발생 (throw)를 생성 오류 메시지, 최적 시 사용자에 게 성가신 합니다.

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

사용할 수 있는 코드 예외가 발생할 수 있는 경우에서 및이 유형의 오류 메시지를 방지 하기 위해 `Try/Catch` 문입니다. 에 `Try` 문을 체크 인하는 코드를 실행 합니다. 하나 이상의 `Catch` 문을 찾을 수 있습니다 특정 발생 했을 수 있는 오류 (특정 유형의 예외). 만큼 포함할 수 있습니다 `Catch` 때 문이 예상 되는 오류에 대 한 확인 해야 합니다.

> [!NOTE]
> 사용 하지 않는 것이 좋습니다 합니다 `Response.Redirect` 의 메서드 `Try/Catch` 문을 페이지에서 예외가 발생할 수 있기 때문에 합니다.


다음 예제에서는 첫 번째 요청에서 텍스트 파일을 만들고 다음 사용자가 파일을 열 수 있는 단추를 표시 하는 페이지를 보여 줍니다. 이 예제에서는 예외가 하면 있도록 의도적으로 잘못 된 파일 이름을 사용 합니다. 코드에 포함 되어 `Catch` 두 가지 가능한 예외에 대 한 문을: `FileNotFoundException`, 파일 이름에 잘못 된 경우 발생 하는 및 `DirectoryNotFoundException`, ASP.NET 폴더를도 찾을 수 없는 경우 발생 합니다. (모든 항목이 제대로 작동 하는 경우 실행 방식을 확인 하기 위해이 예에서 문은 주석 수 있습니다.)

코드에서 예외를 처리 하지 않은 경우 이전 스크린 샷에서 처럼 오류 페이지가 표시 됩니다. 그러나는 `Try/Catch` 섹션은 사용자가 이러한 종류의 오류를 표시 하지 못하도록 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>추가 리소스

### <a name="reference-documentation"></a>참조 설명서

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic 언어](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
