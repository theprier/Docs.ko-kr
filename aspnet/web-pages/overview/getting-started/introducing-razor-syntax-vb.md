---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: "Razor 구문 (Visual Basic)를 사용 하 여 ASP.NET 웹 프로그래밍 소개 | Microsoft Docs"
author: tfitzmac
description: "이 부록 한 개요를 제공 ASP.NET 웹 페이지를 사용한 프로그래밍의 Visual Basic에서 Razor 구문을 사용 하 여 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 8f5d223a5944d8adb9fe65c89e87829d18d1c7ee
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>Razor 구문 (Visual Basic)를 사용 하 여 ASP.NET 웹 프로그래밍 소개
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는의 프로그래밍 개요 ASP.NET 웹 페이지 Razor 구문 및 Visual Basic을 사용 하 여 합니다. ASP.NET은 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft의 기술입니다.
> 
> **학습할**:
> 
> - 프로그래밍 팁 시작 ASP.NET 웹 페이지 Razor 구문을 사용 하 여 프로그래밍에 대 한 상위 8입니다.
> - 기본 프로그래밍 개념을 매핑해야 합니다.
> - 어떤 ASP.NET 서버 코드와 Razor 구문에 대 한 all입니다.
>   
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하 여 대부분의 예에서는 C#을 사용 합니다. 만 Razor 구문 Visual Basic을 지원 합니다. 웹 페이지를 만들면 Visual Basic의 ASP.NET 웹 페이지를 프로그래밍 하는 *.vbhtml* 파일 이름 확장명, Visual Basic 코드를 추가 합니다. 이 문서에서는 Visual Basic 언어 및를 ASP.NET 웹 페이지를 만드는 구문을 작업에 대 한 개요를 제공 합니다.

> [!NOTE]
> Microsoft WebMatrix에 대 한 기본 웹 사이트 템플릿 (**Bakery**, **사진 갤러리**, 및 **시작 사이트**등) C# 및 Visual Basic 버전에서 사용할 수 있습니다. NuGet 패키지로 하 여 Visual Basic 서식 파일을 설치할 수 있습니다. 웹 사이트 템플릿 이라는 폴더에 사이트의 루트 폴더에 설치 된 *Microsoft 템플릿을*합니다.


## <a name="the-top-8-programming-tips"></a>상위 8 프로그래밍 팁

이 섹션에서는 절대 Razor 구문을 사용 하 여 ASP.NET 서버 코드 작성을 시작할 때 알아야 할 몇 가지 팁을 나열 합니다.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. 코드 사용 하 여 페이지를 추가 하 여 @ 문자

`@` 문자 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

브라우저에 표시 된 결과:

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 인코딩**
> 
> 사용 하 여 페이지의 콘텐츠를 표시 하는 `@` ASP.NET을 HTML로 인코딩하고 출력 앞의 예와 문자입니다. 이 예약 된 HTML 문자를 대체 (같은 `<` 및 `>` 및 `&`) 문자를 HTML 태그 또는 엔터티로 해석 되지 않고 웹 페이지의에서 문자를 표시할 수 있도록 하는 코드와 함께 합니다. HTML 인코딩하지 않고 서버 코드의에서 출력을 올바르게 표시 되지 않습니다 및 페이지 보안 위험에 노출 될 수 있습니다.
> 
> 목표는 태그로 태그를 렌더링 하는 HTML 태그를 출력 하는 경우 (예를 들어 `<p></p>` 단락 또는 `<em></em>` 텍스트를 강조 하기 위해)를 섹션을 참조 [결합 텍스트, 태그 및 코드 블록의에서 코드를](#BM_CombiningTextMarkupAndCode) 이 문서의 뒷부분에 나오는 합니다.
> 
> 읽어볼 수 있는 HTML의 인코딩에 대 한 [ASP.NET 웹 페이지 사이트에서 HTML 양식 사용](https://go.microsoft.com/fwlink/?LinkId=202892)합니다.


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. 코드를 사용 하 여 코드 블록 안에 포함 하는 중... 종료 코드

코드 블록 하나 이상의 코드 문을 포함 및 키워드와 함께 둘러싸입니다 `Code` 및 `End Code`합니다. 열기 배치 `Code` 키워드 바로 뒤의 `@` 문자 및 #8212; 사이의 공백 수 없습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

브라우저에 표시 된 결과:

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. 블록 안에 줄 바꿈이 각 코드 문을 종료합니다

Visual Basic 코드 블록에 각 문에 줄 바꿈을로 끝납니다. (문서의 뒷부분에 표시 됩니다 필요에 따라 긴 코드 문을 여러 줄으로 줄 바꿈 하는 방법을.)

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. 변수를 사용 하 여 값을 저장

에 값을 저장 한 *변수*, 문자열, 숫자 및 날짜 등을 포함 합니다. 사용 하 여 새 변수를 만들면는 `Dim` 키워드입니다. 사용 하 여 페이지에 직접 변수 값을 삽입할 수는 있지만 `@`합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

브라우저에 표시 된 결과:

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 리터럴 문자열 값을 큰따옴표로 묶습니다.

A *문자열* 텍스트로 처리 되는 문자 시퀀스입니다. 문자열을 지정 하면 나타내므로 큰따옴표:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

문자열 값을 큰따옴표를 포함 하려면 두 개의 큰따옴표 문자를 삽입 합니다. 페이지 출력에 한 번 표시 큰따옴표 문자를 입력으로 `""` 내 따옴표 붙은 문자열 및 열을 두 번 표시 하려는 경우 입력으로 `""""` 따옴표 붙은 문자열 내에서.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

브라우저에 표시 된 결과:

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic 코드 대/소문자 구분 됩니다.

Visual Basic 언어가 대/소문자 구분 되지 않습니다. 프로그래밍 키워드 (같은 `Dim`, `If`, 및 `True`) 및 변수 이름 (같은 `myString`, 또는 `subTotal`) 어떤 경우에 쓸 수 있습니다.

변수에 값을 할당 하는 코드의 다음 줄 `lastname` 소문자를 사용 하 여 이름을 지정 하 고 다음 대문자 이름을 사용 하 여 페이지에 변수 값을 출력 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

브라우저에 표시 된 결과:

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. 개체를 사용 하 여 코딩의 대부분

개체를 사용 하 여 프로그래밍 수 있는 항목 &#8212; 나타냅니다. 페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등입니다. 개체에는 #8212; 및 해당 특성을 설명 하는 속성이 텍스트 상자 개체에는 `Text` 속성, 요청 개체에는 `Url` 속성, 전자 메일 메시지에는 `From` 속성을 고객 개체에는 `FirstName` 속성입니다. 개체에 갖게 되는 메서드와 &quot;동사&quot; 수행할 수 있습니다. 예로 파일 개체의 `Save` 메서드를 이미지 개체의 `Rotate` 메서드와 메일 개체의 `Send` 메서드.

자주 사용 하 여 `Request` 폼의 값 등의 정보를 제공 하는 개체 브라우저 종류 요청, 페이지, 사용자 id, 등의 URL을 한 페이지 (텍스트 상자, 등)에 필드입니다. 속성에 액세스 하는 방법을 보여 주는이 예제는 `Request` 개체와 호출 하는 방법의 `MapPath` 의 메서드는 `Request` 서버에서 해당 페이지의 절대 경로 제공 하는 개체:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

브라우저에 표시 된 결과:

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 의사 결정 하는 코드를 작성할 수 있습니다.

동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 확인할 수 있습니다. 이 작업을 수행 하는 가장 일반적인 방법은 `If` 문 (및 선택적 `Else` 문).

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

문이 `If IsPost` 작성 하는 약식 방법 `If IsPost = True`합니다. 와 함께 `If` 문 다양 한 조건에서 반복 코드 블록을 테스트 하는 방법 및에이 문서의 뒷부분에 설명 되어 있습니다.

브라우저에 표시 된 결과 (클릭 한 후 **전송**):

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET 및 POST 메서드 IsPost 속성**
> 
> 웹 페이지 (HTTP)에 사용 되는 프로토콜은 매우 제한 된 수의 메서드를 지원 (&quot;동사&quot;) 서버에 요청을 수행 하는 데 사용 되는 합니다. 두 가지 가장 일반적인 요소는 페이지를 사용 되는 GET 및 POST는 페이지를 제출 하는 데 사용 되는 합니다. 일반적으로 사용자 요청 페이지를 처음으로 페이지를 요청 GET를 사용 하 여 합니다. 사용자 폼에 입력 한 다음 클릭 **전송**, 브라우저는 서버에는 POST 요청을 만듭니다.
> 
> 웹 프로그래밍을 유용 여부는 페이지 요청은 GET 또는 POST로 페이지를 처리 하는 방법을 알 수 있도록 알아야 합니다. 사용할 수 있는 ASP.NET 웹 페이지에는 `IsPost` 는 GET 또는 POST 요청 인지 확인 하려면 속성입니다. 요청이 게시물에 면는 `IsPost` 속성은 true를 반환 하 고 폼에서 텍스트 상자의 값 읽기 등으로를 수행할 수 있습니다. 표시 되는 많은 예제 페이지의 값에 따라 다르게 처리 하는 방법을 보여 줍니다. `IsPost`합니다.


## <a name="a-simple-code-example"></a>간단한 코드 예제

이 절차를 기본 프로그래밍 기술을 설명 하는 페이지를 만드는 방법을 보여 줍니다. 예제에서는 사용자가 추가 하 고 결과 표시 한 다음 두 숫자를 입력할 수 있는 페이지를 만듭니다.

1. 편집기에서 새 파일을 만들고 이름을 *AddNumbers.vbhtml*합니다.
2. 페이지에 이미 있는 모든 항목을 교체 하는 페이지에 다음 코드와 태그를 복사 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    몇 가지 사항은 다음과 같습니다.

    - `@` 문자 페이지에서 첫 번째 코드 블록을 시작 하 고 뒤에 나오는 `totalMessage` 아래쪽에 있는 변수를 포함 합니다.
    - 페이지 맨 위에 있는 블록 `Code...End Code`합니다.
    - 변수 `total`, `num1`, `num2`, 및 `totalMessage` 여러 숫자 및 문자열을 저장 합니다.
    - 리터럴 문자열 값에 할당 된는 `totalMessage` 변수가 큰따옴표 안에 표시 합니다.
    - Visual Basic 코드 때 대/소문자를 구분 되지 않으므로 `totalMessage` 페이지의 아래쪽에 있는 변수를 사용 하는, 이름이 페이지 맨 위에 있는 변수 선언의 표기와 일치 해야 합니다. 대/소문자는 중요 하지 않습니다.
    - 식 `num1.AsInt()`  +  `num2.AsInt()` 개체 및 메서드를 사용 하는 방법을 보여 줍니다. `AsInt` 각 변수에 메서드 값을 정수로 (정수) 추가할 수 있는 사용자가 입력 문자열을 변환 합니다.
    - `<form>` 태그를 포함 한 `method="post"` 특성입니다. 이 지정 하는 사용자가 클릭할 때 **추가**, 페이지 HTTP POST 메서드를 사용 하 여 서버에 보내집니다. 페이지가 제출 되는 경우, 코드 `If IsPost` 조건부 true로 평가 되 코드를 실행, 숫자를 추가 하는 결과 표시 합니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다. (있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.) 두 정수를 입력 한 다음 클릭는 **추가** 단추입니다.

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic 언어 및 구문

이전 ASP.NET 웹 페이지를 만드는 방법 및 서버 코드 HTML 태그를 추가할 수는 방법의 기본 예제에서는 있을 것입니다. 여기서 Visual Basic을 사용 하 여 Razor 구문 &#8212;를 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본적인 방법과 알아봅니다. 즉, 프로그래밍 언어 규칙입니다.

(특히 사용한 적이 있다면 C, c + +, C#, Visual Basic 또는 JavaScript) 프로그래밍 경험이 경우 설명한 여기 대부분 익숙할 것입니다. 아마도 할 숙지만 태그에 WebMatrix 코드에 어떻게 추가 되었는지를 *.vbhtml* 파일입니다.

### <a id="BM_CombiningTextMarkupAndCode"></a>텍스트, 태그 및 코드 블록의에서 코드를 결합합니다.

서버 코드 블록에서 텍스트와 페이지에는 태그를 출력 하고자 합니다. 서버 코드 블록에 코드 되 고 하는 대신 링크로 렌더링할지는 텍스트가 포함 하는 경우 ASP.NET 코드에서 해당 텍스트를 구별할 수 있어야 합니다. 다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.

- 와 같은 블록 HTML 요소에 텍스트를 묶으십시오 `<p></p>` 또는 `<em></em>`:

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML 요소는 텍스트, 추가 HTML 요소와 서버 코드 식을 포함할 수 있습니다. ASP.NET에서 여는 HTML 태그를 표시 하는 경우 (예를 들어 `<p>`), 모든 요소 렌더링 및 해당 콘텐츠는 브라우저 (및 서버 코드 식 확인) 하는 것입니다.

- 사용 하 여 `@:` 연산자 또는 `<text>` 요소입니다. `@:` 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 콘텐츠의 한 줄을 출력에서 `<text>` 요소 출력에 여러 줄을 포함 합니다. 이러한 옵션은 출력의 일부로 HTML 요소를 렌더링 하지 않을 경우에 유용 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    다음 예제에서는 앞의 예제를 반복 하지만 한 쌍의를 사용 하 여 `<text>` 태그를 렌더링할 텍스트를 묶으십시오.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    다음 예제에서는 `<text>` 및 `</text>` 태그는 모두 일부 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 3 줄을 묶습니다 (`<br />`), 서버 코드와 일치 하는 HTML 태그와 함께 합니다. 각 줄을 따로 앞 수는 다시는 `@:` 연산자; 둘 다 방식으로 작동 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > 이 섹션 및 #8212;에 표시 된 대로 텍스트를 출력할 때 HTML 요소를 사용 하 여 `@:` 연산자 또는 `<text>` 요소 &#8212; ASP.NET 하지 않는 HTML 인코딩할 출력 합니다. (ASP.NET 서버 코드 식 및 뒤에 나오는 서버 코드 블록의 출력에서는 인코딩하지 앞에서 설명한 대로 `@`,이 섹션에서 설명 하는 특별 한 경우를 제외 하 고 있습니다.)

### <a name="whitespace"></a>Whitespace

추가 공백 문에서 (및 문자열 리터럴 외부에서) 문을 영향을 주지:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>긴 문은 여러 줄으로 분리

밑줄 문자를 사용 하 여 긴 코드 문은 여러 줄으로 나눌 수 있습니다 `_` (Visual Basic의는 호출 되는 *연속 문자*) 코드의 각 줄 뒤 합니다. 다음 줄으로 문을 중단 하려면 줄의 끝에 공백을 차례로 연속 문자를 추가 합니다. 다음 줄에서 문을 계속 합니다. 문을 가독성을 향상 하는 데 필요한 만큼 여러 줄으로 래핑할 수 있습니다. 다음 문은 동일합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

그러나 문자열 리터럴을 중간 줄을 둘러쌀 수 없습니다. 다음 예제에서는 작동 하지 않습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

위의 코드와 같은 여러 줄으로 줄 바꿈 하는 긴 문자열을 결합 하려면 해야 사용 하는 *연결 연산자* (`&`),이 문서의 뒷부분에 살펴보겠습니다.

### <a name="code-comments"></a>코드 주석

주석 또는 받는 사람에 대 한 정보를 두고 수 있습니다. Razor 구문 설명 접두사가 추가 되며 `@*` 하 고 끝나야 `*@`합니다.

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

Razor 구문 주석을 코드 블록 내에서 사용 하거나 일반 Visual Basic 주석 문자를 작은따옴표를 사용할 수 있습니다 (`'`) 각 줄에 접두사로 지정 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>변수

변수는 명명된 된 개체를 사용 하면 데이터를 저장할입니다. 이름은 변수, 하지만 이름은 알파벳 문자로 시작 해야 하 고 공백 또는 예약 된 문자를 포함할 수 없습니다. Visual Basic의 경우 앞에서 보았듯이 변수 이름에 있는 문자의 대/소문자 중요 하지 않습니다.

### <a name="variables-and-data-types"></a>변수 및 데이터 형식

변수를 나타내는 데이터의 종류는 변수에 저장 된 특정 데이터 형식을 가질 수 있습니다. 문자열 값을 저장 하는 문자열 변수를 포함할 수 있습니다 (같은 &quot;Hello world&quot;), (예: 3 또는 79) 정수 값을 저장 하는 정수 변수 및 다양 한 형식 (예: 2012/4/12 또는 2009 년 3 월의에서 날짜 값을 저장 하는 날짜 변수 ). 및 다른 여러 데이터 형식을 사용할 수 있습니다.

그러나 변수에 대 한 형식을 지정할 필요가 없습니다. 대부분의 경우에서 ASP.NET 변수에서 데이터 사용 방법에 따라 형식을 알 수 있습니다. (형식을 지정 해야 하는 경우에 따라,이 true 예제 표시 됩니다.)

형식을 지정 하지 않고 변수를 선언 하려면 `Dim` 및 변수 이름 (예를 들어, `Dim myVar`). 형식의 변수를 선언 하려면 `Dim` 변수 이름, 밑줄 및 `As` 및 형식 이름을 다음 (예를 들어, `Dim myVar As String`).

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

다음 예제에서는 웹 페이지에는 변수를 사용 하는 일부 인라인 식을 보여 줍니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

브라우저에 표시 된 결과:

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>변환 및 데이터 형식 테스트

ASP.NET 데이터 형식을 자동으로 확인할 일반적으로 수 있지만 때로는 만들 수 없습니다. 따라서 ASP.NET 명시적 변환을 수행 하 여 도움을 해야 합니다. 가 없는 형식을 변환 하는 경우에 때때로 유용 테스트 데이터의 형식을 있습니다 작업할 수 하 합니다.

가장 일반적인 경우는 정수 또는 날짜와 같은 다른 형식으로 문자열 변환 해야 합니다. 다음 예제에서는 문자열을 숫자로 변환 해야 여기서는 일반적인 경우를 보여 줍니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

일반적으로 사용자 입력을 문자열로 가져옵니다. 숫자를 입력 하 라는 메시지가 표시 한 경우에 및 사용자 입력을 제출 하 고 코드에서 읽을 때 숫자를 입력 한 경우에 데이터는 문자열 형식입니다. 따라서 문자열을 숫자로 변환 해야 합니다. 예제에서는 변환 하지 않고 값에 산술 연산을 수행 하려는 경우 다음과 같은 오류가 발생 ASP.NET 두 문자열을 추가할 수 없습니다.

`Cannot implicitly convert type 'string' to 'int'.`

호출 하면 값을 정수로 변환할는 `AsInt` 메서드. 변환이 성공 하는 경우에 숫자를 추가 합니다.

다음 표에서 변수에 대 한 몇 가지 일반적인 변환 및 테스트 메서드를 나열합니다.

| **메서드** | **설명** | **예제** |
| --- | --- | --- |
| `AsInt(), IsInt()` | 숫자를 나타내는 문자열로 변환 (같은 &quot;593&quot;)는 정수입니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)] |
| `AsBool(), IsBool()` | 와 같은 문자열 변환 &quot;true&quot; 또는 &quot;false&quot; 부울 형식으로. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)] |
| `AsFloat(), IsFloat()` | 같은 10 진수 값을 가진 문자열 변환 &quot;1.3&quot; 또는 &quot;7.439&quot; 된 부동 소수점 수입니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)] |
| `AsDecimal(), IsDecimal()` | 와 같은 10 진수 값을 가진 문자열 변환 &quot;1.3&quot; 또는 &quot;7.439&quot; 소수로 합니다. (Asp.net에서 10 진수는 부동 소수점 숫자 보다 더 정확한.) | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)] |
| `AsDateTime(), IsDateTime()` | ASP.NET에는 날짜 및 시간 값을 나타내는 문자열 변환 `DateTime` 유형입니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)] |
| `ToString()` | 다른 데이터 형식을 문자열로 변환합니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)] |

## <a name="operators"></a>연산자

연산자는 키워드 또는 ASP.NET 어떤 유형의 식에서 수행 하기 위한 명령에 알려 주는 문자입니다. Visual Basic에서는 많은 연산자를 지원 하지만 ASP.NET 웹 페이지 개발을 시작 하려면 몇 가지를 인식 해야 합니다. 다음 표에서 가장 일반적인 연산자 요약 되어 있습니다.

| **Operator** | **설명** | **예제** |
| --- | --- | --- |
| `+ - * /` | 숫자 식에 사용 되는 수학 연산자. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)] |
| `=` | 할당 및 같음입니다. 컨텍스트에 따라 왼쪽에 있는 개체를 문의 오른쪽에 있는 값을 할당 하거나 하거나 값이 같은지를 확인 합니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)] |
| `<>` | 같지 않음 반환 `True` 값 같지 않으면 합니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)] |
| `< > <= >=` | 보다 작음, 보다 큼, 작거나 보다 또는 같음, 및 보다 크거나 합니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)] |
| `&` | 연결 문자열을 조인 하는 데 사용 됩니다. | [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)] |
| `+= -=` | 증가 및 감소 연산자의 추가 하 고 변수에서 각각 1을 뺌입니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)] |
| `.` | 점입니다. 개체의 속성 및 메서드를 구별 하는 데 사용 합니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)] |
| `()` | 괄호입니다. 그룹 식에 배열 및 컬렉션의 멤버에 액세스 하 고 하는 메서드에 매개 변수를 전달 하는 데 사용 합니다. | [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)] |
| `Not` | 필요는 없습니다. False로 그리고 반대로 true 값을 반대로 바꿉니다. 일반적으로 테스트 하는 약식 방법으로 사용 `False` (즉,에 대 한 하지 `True`). | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)] |
| `AndAlso OrElse` | 논리 AND 또는 및 연결 하는 데 사용 되는 조건입니다. | [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)] |

## <a name="working-with-file-and-folder-paths-in-code"></a>파일 및 코드의 폴더 경로 작업

종종 코드에서 파일 및 폴더 경로 작업할 수 있습니다. 개발 컴퓨터에 나타나는 실제 폴더 구조는 웹 사이트에 대 한 예로 다음과 같습니다.

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

Url 및 경로 대 한 일부 필수 세부 정보는 다음과 같습니다.

- 도메인 이름으로 시작 하며 URL (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`).
- URL은 호스트 컴퓨터에 실제 경로에 해당합니다. 예를 들어 `http://myserver` 폴더에 해당할 수 있습니다 *C:\websites\mywebsite* 서버에 있습니다.
- 가상 경로 전체 경로 지정 하지 않고 코드의 경로 나타내기 위해의 줄임 표기입니다. 도메인 또는 서버 이름 뒤에 오는 URL의 일부를 포함 합니다. 가상 경로 사용 하는 경우에 경로 업데이트 하지 않고 다른 도메인 또는 서버에 코드를 이동할 수 있습니다.

차이점을 이해 하려면 예를 들면 다음과 같습니다.

| 전체 URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| 서버 이름 | *mycompanyserver* |
| 가상 경로 | */humanresources/CompanyPolicy.htm* |
| 실제 경로 | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

가상 루트는 / 하면 c: 드라이브의 루트와 마찬가지로 드라이브는 \ \. (가상 폴더 경로 항상 슬래시를 사용 합니다.) 폴더의 가상 경로 실제 폴더가; 이름이 동일한 필요가 없습니다. 별칭 수 있습니다. (프로덕션 서버에서 가상 경로 거의 일치는 정확한 실제 경로입니다.)

코드에서 파일 및 폴더를 사용 하는 경우 실제 경로 및 경우에 따라 작업 하는 개체의 종류에 따라 가상 경로 참조 해야 경우에 따라 합니다. ASP.NET을 사용 하면 이러한 도구 코드의 파일 및 폴더 경로 사용 하기 위한:는 `Server.MapPath` 메서드, 및 `~` 연산자 및 `Href` 메서드.

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>실제 가상 경로 변환: Server.MapPath 메서드

`Server.MapPath` 메서드 가상 경로 변환 (같은 */default.cshtml*)에 대 한 절대 실제 경로 (같은 *C:\WebSites\MyWebSiteFolder\default.cshtml*). 완전 한 실제 경로 언제 든 지가이 메서드를 사용 합니다. 일반적인 예는 읽기 또는 텍스트 파일 또는 웹 서버의 이미지 파일을 작성 하는 경우입니다.

일반적으로 알 수 없는 호스팅 사이트의 서버에 사이트의 실제 절대 경로, 모르면이 메서드는 경로 변환할 수 있도록-가상 경로-의 서버에 해당 경로에 있습니다. 파일 또는 메서드로 폴더에 가상 경로 전달 하 고 실제 경로 반환 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>가상 루트 참조:는 ~ 연산자와 Href 메서드

에 *.cshtml* 또는 *.vbhtml* 파일을 사용 하 여 가상 루트 경로 참조할 수 있습니다는 `~` 연산자입니다. 즉 매우 편리 하 여 사이트의 페이지를 이동할 수 있으며 다른 페이지에 포함 한 링크가 손상 됩니다. 다른 위치에 웹 사이트를 계속 이동 하는 경우에 유용 합니다. 다음은 몇 가지 예입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

웹 사이트가 경우 `http://myserver/myapp`, 같습니다. 방법을 통해 ASP.NET 페이지를 실행할 때 이러한 경로 처리 합니다.

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

(이러한 경로 변수를 값으로 실제로 나타나지 않지만 즉, 이전 하는 경우 ASP.NET 경로 처리 합니다.)

사용할 수는 `~` 연산자 (위에서) 서버 코드와 같은 태그에서:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

태그를 사용 하 여는 `~` 연산자 이미지 파일, 다른 웹 페이지 및 CSS 파일 같은 리소스에 경로를 만듭니다. ASP.NET 페이지 (코드 및 태그)를 통해 찾아 해결 하는 모든 페이지를 실행 하는 경우는 `~` 적절 한 경로에 대 한 참조입니다.

## <a name="conditional-logic-and-loops"></a>조건부 논리, 루프

ASP.NET 서버 코드 하면 조건 및 루프를 실행 하는 지정 된 횟수의 즉, 코드 문을 반복 되는 쓰기 코드에 따라 작업을 수행).

### <a name="testing-conditions"></a>조건 테스트

사용 하면 간단한 조건 테스트는 `If...Then` 반환 하는 문에 `True` 또는 `False` 지정한 테스트에 따라:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If` 키워드 블록을 시작 합니다. 실제 테스트 (조건) 뒤에 오는 `If` 키워드와 true 또는 false를 반환 합니다. `If` 문을 끝나는 `Then`합니다. 테스트가 true 인 경우 실행할 문을 묶여 `If` 및 `End If`합니다. `If` 문에 포함할 수 있는 `Else` 조건이 false 인 경우 실행할 문을 지정 하는 블록:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

경우는 `If` 문이 시작 되는 코드 블록을 수직 사용할 필요가 없습니다 `Code...End Code` 는 블록을 포함 하도록 문입니다. 추가 하면 `@` 블록에 작동 합니다. 이 접근 방식은으로 `If` 다른 Visual Basic 키워드를 포함 하 여 코드 블록 뒤에 프로그래밍 뿐 아니라 `For`, `For Each`, `Do While`등입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

하나 이상을 사용 하 여 여러 조건을 추가할 수 있습니다 `ElseIf` 블록:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

이 예제에서는 첫 번째 조건이 `If` 블록이 true 이면는 `ElseIf` 조건이 확인 됩니다. 조건이 충족 될 경우의 문에서 `ElseIf` 블록이 실행 됩니다. 조건 중 만족 되 면에 있는 문은 `Else` 블록이 실행 됩니다. 개수에 관계 없이 추가할 수 있습니다 `ElseIf` , 차단 하 고 다음에 닫기는 `Else` 차단는 &quot;나머지 모든&quot; 조건입니다.

다양 한 조건 테스트 하려면 사용 하는 `Select Case` 블록:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

테스트할 값입니다 (예에서 weekday 변수) 괄호 안의 항목은 합니다. 사용 하 여 각 개별 테스트는 `Case` 는 값을 나열 하는 문입니다. 하는 경우의 값을 `Case` 문이 테스트 값을 하는 코드와 일치 `Case` 블록이 실행 됩니다.

브라우저에 표시 하는 마지막 두 개의 조건부 블록의 결과:

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>코드를 반복합니다.

동일한 문을 반복적으로 실행 해야 하는 경우가 많습니다. 반복 하 여이 작업을 수행 합니다. 예를 들어 자주 문을 실행 하면 같은 각 항목에 대 한 데이터의 컬렉션에서입니다. 정확히 몇 번 반복 하려면 알고 있는 경우 사용할 수 있습니다는 `For` 루프입니다. 이러한 종류의 루프 계산 하거나 개수를 계산에 특히 유용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

로 시작 하는 루프는 `For` 키워드와 세 개의 요소:

- 바로 뒤의 `For` 카운터 변수를 선언 하면 문 (사용할 필요가 없습니다 `Dim`)에서 같이 범위를 나타내는 `i = 10 to 20`합니다. 즉, 변수 `i` 10부터 계산을 시작 하 고 20 (포함)에 도달할 때까지 계속 됩니다.
- 사이 `For` 및 `Next` 문 블록의 내용입니다. 이 하나 이상의 코드 문을 실행 하는 각 루프를 포함할 수 있습니다.
- `Next i` 문이 루프를 종료 합니다. 카운터 값을 증가 하 고 루프의 다음 반복을 시작 합니다.

사이 코드 줄은 `For` 및 `Next` 줄 루프의 각 반복에 대해 실행 되는 코드를 포함 합니다. 태그에 새 단락 만듭니다 (`<p>` 요소) 시간 및의 값을 표시 하는 출력에 추가 하는 각 i (카운터). 이 페이지를 실행 하면이 예제에서는 항목 수를 나타내는 각 줄에 있는 텍스트로 출력을 표시 하는 11 선을 만듭니다.

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

를 컬렉션 또는 배열으로 작업 하는 경우 자주 사용 하는 `For Each` 루프입니다. 컬렉션은 유사한 개체의 그룹 및 `For Each` 루프는 컬렉션의 각 항목에 작업을 수행할 수 있습니다. 이 유형의 루프는 컬렉션에 대 한 편리한 때문에 달리는 `For` 카운터를 증가 또는 제한을 설정 하지 않아도 루프입니다. 대신,는 `For Each` 루프 코드 컬렉션을 통해 완료 될 때까지 단순히 진행 합니다.

에 있는 항목을 반환 하는이 예제는 `Request.ServerVariables` 컬렉션 (을 웹 서버에 대 한 정보 포함). 사용 하 여 한 `For Each` 새 각 항목의 이름을 표시 하는 루프 `<li>` HTML 글머리 기호 목록에 있는 요소입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each` 키워드 다음에 컬렉션의 단일 항목을 나타내는 변수 (예제에서는 `myItem`)와 `In` 키워드, 컬렉션을 순환 검색 하려면 다음 합니다. 본문에는 `For Each` 루프 앞에서 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

범용 루프를 만들려면 사용은 `Do While` 문:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

로 시작 하는이 루프는 `Do While` 키워드는 조건에 따라 다음 뒤에 블록을 반복 합니다. 일반적으로 루프를 하나씩 늘립니다 (추가) 또는 감소 시키는 (에서 빼기) 변수 또는 계산에 사용 되는 개체입니다. 예제에서는 `+=` 연산자 1 값을 추가 변수는 루프 실행 될 때마다 합니다. (아래로 계산 하는 루프에서 변수를 감소 시키기 위해 감소 연산자 사용 `-=`.)

## <a name="objects-and-collections"></a>개체 및 컬렉션

거의 모든 ASP.NET 웹 사이트는 웹 페이지 자체를 포함 하 여 개체입니다. 이 섹션에서는 합니다 자주 사용 하 여 코드에서 몇 가지 중요 한 개체를 설명 합니다.

### <a name="page-objects"></a>Page 개체

Asp.net에서 가장 기본적인 개체 페이지입니다. 조건에 맞는 개체 하지 않고 직접 page 개체의 속성에 액세스할 수 있습니다. 다음 코드는 페이지의 파일 경로 가져옵니다.를 사용 하 여 `Request` 페이지의 개체:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

속성을 사용할 수는 `Page` 와 같은 많은 정보를 가져올 개체입니다.

- `Request`. 앞서 설명한 바 대로 브라우저 종류는 요청한, 페이지, 사용자 id, 등의 URL을 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.
- `Response`. 서버 코드 실행이 완료 된 경우 브라우저에 전송 될 응답 (페이지)에 대 한 정보 컬렉션입니다. 예를 들어 응답에 정보를 기록 하려면이 속성을 사용할 수 있습니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>컬렉션 개체 (배열 및 사전을)

컬렉션은 개체의 컬렉션과 같은 동일한 유형의 그룹 `Customer` 데이터베이스에서 개체입니다. ASP.NET 같은 많은 기본 제공 컬렉션이 포함 되어는 `Request.Files` 컬렉션입니다.

컬렉션의 데이터에 자주 작업할 수 있습니다. 두 가지 일반적인 컬렉션 형식은 *배열* 및 *사전*합니다. 배열 모음 유사한 항목을 저장 하려고 하지만 각 항목을 보유 하는 별도 변수를 만들지 않으려는 경우에 유용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

배열, 특정 데이터 형식을 선언와 같은 `String`, `Integer`, 또는 `DateTime`합니다. 변수 배열 포함 될 수 있습니다, 선언에 변수 이름에 괄호를 추가 하 (같은 `Dim myVar() As String`). 항목의 위치 (인덱스)를 사용 하는 배열 또는 사용 하 여 액세스할 수 있습니다는 `For Each` 문. 배열 인덱스는 0부터 시작 &#8212; 즉, 첫 번째 항목은 위치 0, 두 번째 항목은 1, 위치입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

가져와서 배열에 있는 항목의 수를 확인할 수는 `Length` 속성입니다. 배열에 있는 특정 항목의 위치를 가져오기 위해 (즉,의 배열을 검색 합니다)를 사용 하 여는 `Array.IndexOf` 메서드. 할 수도 있습니다 등으로 역방향 배열 내용이 (의 `Array.Reverse` 메서드) 내용을 정렬 또는 (의 `Array.Sort` 메서드).

브라우저에 표시 된 문자열 배열 코드의 출력:

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

사전에 키 (또는 이름)을 설정 하거나 해당 값을 검색할를 입력할 수 있는 키/값 쌍의 컬렉션입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

사전을 만드는 데 사용 하는 `New` 키워드를 새 만드는지에 나타내려면 `Dictionary` 개체입니다. 변수를 사용 하 여 사전에 할당할 수 있습니다는 `Dim` 키워드입니다. 괄호를 사용 하 여 사전에 있는 항목의 데이터 형식을 ( `( )` ). 선언의 끝 실제로 새 사전을 만듭니다 하는 방법 이므로 다른 쌍 괄호를 추가 해야 합니다.

사전에 항목을 추가 하려면 호출할 수 있습니다는 `Add` 메서드 또는 사전 변수의 (`myScores` 이 경우), 키 및 값을 지정 합니다. 또는 키를 지정 하 고 다음 예제와 같이 단순한 할당을 수행 하려면 괄호를 사용할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

사전에서 값을 가져오려면 괄호로 키를 지정 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>매개 변수를 사용 하 여 메서드를 호출합니다.

이 문서의 앞부분에서 본 것 처럼 개체를 프로그래밍 하는 메서드가 있습니다. 예를 들어 한 `Database` 개체 가질 수 있습니다는 `Database.Connect` 메서드. 많은 메서드가 하나 이상의 매개 변수를 갖게 됩니다. A *매개 변수* 메서드에 전달 하는 값은 해당 작업을 완료 하려면 사용할 수 있도록 합니다. 예를 들어에 대 한 선언을 확인는 `Request.MapPath` 메서드를 세 개의 매개 변수를 사용 합니다.

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

이 메서드는 지정 된 가상 경로에 해당 하는 서버의 실제 경로 반환 합니다. 메서드에 대 한 매개 변수 3 개 `virtualPath`, `baseVirtualDir`, 및 `allowCrossAppMapping`합니다. (선언에서 수락 하 게 하는 데이터의 데이터 형식과 매개 변수가 나열 됩니다 확인 합니다.) 이 메서드를 호출할 때에 세 매개 변수 모두에 대 한 값을 입력 해야 합니다.

메서드에 매개 변수를 전달 하기 위한 두 가지 옵션이 Razor 구문을 사용 하 여 Visual Basic을 사용 하는 경우: *위치 매개 변수* 또는 *명명 된 매개 변수*합니다. 위치 매개 변수를 사용 하 여 메서드를 호출 하는 엄격한 순서를 메서드 선언에 지정 된 매개 변수를 전달 합니다. (일반적으로 알 수이 순서는 메서드에 대 한 설명서를 참조 하 여.) 순서를 따라야 하며 매개 변수 중 &#8212; 건너뛸 수 없습니다. 필요에 따라 전달 하면 빈 문자열 (`""`) 또는 null에 대 한 값을 갖지 위치 매개 변수입니다.

다음 예제에서는 라는 폴더가 있다고 가정 *스크립트* 웹 사이트에 있습니다. 코드를 호출 하 여는 `Request.MapPath` 올바른 순서로 세 개의 매개 변수가 대 한 값을 메서드에 전달 합니다. 다음 결과 매핑된 경로 표시합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

메서드에 대 한 여러 매개 변수가 있는 경우 유지할 수 있습니다 코드 보다 명확 하 고 보다 읽기 쉬운 명명 된 매개 변수를 사용 하 여. 명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 다음 매개 변수 이름 지정 `:=` 고 다음 값을 제공 합니다. 명명 된 매개 변수는 경우의 이점은입니다는 원하는 순서에 관계 없이 추가할 수 있습니다. (단점이 메서드 호출이 간단해있지 않습니다.)

다음 예에서는 위와 같은 메서드를 호출 하지만 명명 된 값을 제공할 매개 변수를 사용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

볼 수 있듯이 다른 순서로 매개 변수 전달 됩니다. 그러나 앞의 예제 및이 예제를 실행 하는 경우 동일한 값을 반환 합니다.

## <a name="handling-errors"></a>오류 처리

### <a name="try-catch-statements"></a>Try Catch 문

종종 컨트롤 외부에 같은 이유로 실패할 수 있는 코드에 문의 해야 합니다. 예:

- 코드를 열고, 만들기, 읽기, 또는 파일을 작성 하 려 하면 모든 종류의 오류가 발생할 수 있습니다. 원하는 파일이 존재 하지 않을, 잠긴 상태일 수 코드 수 하지 사용 권한이 하 고, 합니다.
- 마찬가지로, 코드를 데이터베이스에서 레코드를 업데이트 하려고 하는 경우 사용 권한 문제가 있을 수 있습니다, 그리고 데이터베이스에 연결을 삭제 될 수 있습니다, 그리고 유효 하지 않은, 및 등 데이터를 저장할 수 있습니다.

프로그래밍 측면에서 이러한 경우 라고 *예외*합니다. 코드에서 예외를 발견 하는 경우 (throw)를 생성 오류 메시지 인 즉, 가장 좋은 경우 사용자에 게까지 합니다.

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

코드 예외, 발생할 수 있는 경우에이 유형의 오류 메시지를 방지 하기 위해을 사용 하면 `Try/Catch` 문. 에 `Try` 체크 인하는 코드를 실행 하면 문입니다. 하나 이상의 `Catch` 문을 찾을 수 있습니다 특정 발생 했을 수 있는 오류 (특정 형식의 예외). 여러 개 포함할 수 있습니다 `Catch` 있습니다과 문에서 예상 하는 오류에 대 한 확인 해야 합니다.

> [!NOTE]
> 사용 하지 않는 것이 좋습니다는 `Response.Redirect` 에서 메서드 `Try/Catch` 문, 페이지에서 예외가 발생할 수 있기 때문에 있습니다.


다음 예제에서는 첫 번째 요청에서 텍스트 파일을 만들고 다음 사용자가 파일을 열 수 있는 단추를 표시 하는 페이지를 보여 줍니다. 이 예제에서는 하면 예외가 발생 되도록 의도적으로 잘못 된 파일 이름을 사용 합니다. 코드에 `Catch` 두 가지 가능한 예외에 대 한 문을: `FileNotFoundException`, 파일 이름이 잘못 된 경우 발생 및 `DirectoryNotFoundException`, ASP.NET도 폴더를 찾을 수 없는 경우 발생 합니다. (모두 제대로 작동 하는 경우 실행 방법을 보려면 예에서 문은 주석 수 있습니다.)

코드에서 예외를 처리 하지 않은 경우에 이전 스크린 샷에서 같은 오류 페이지가 표시 됩니다. 그러나는 `Try/Catch` 섹션을 사용 하면 사용자가 이러한 종류의 오류를 볼 방지할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>추가 리소스

### <a name="reference-documentation"></a>참조 설명서

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic 언어](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
