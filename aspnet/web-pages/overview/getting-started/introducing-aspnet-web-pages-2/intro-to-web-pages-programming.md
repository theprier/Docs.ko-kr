---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: ASP.NET 웹 페이지를 소개-프로그래밍 기본 사항 | Microsoft Docs
author: tfitzmac
description: "이 자습서에서는 Razor 구문이 있는 ASP.NET 웹 페이지에서 프로그램에는 방법의 개요를 제공합니다. 학습할: 기본 'Razor' 구문을 프로젝트에 대 한 사용 하는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/17/2015
ms.topic: article
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 60115dd06a27bf856427953de29e993194afb991
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
<a name="introducing-aspnet-web-pages---programming-basics"></a>ASP.NET 웹 페이지-프로그래밍 기본 사항 소개
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 Razor 구문이 있는 ASP.NET 웹 페이지에서 프로그램에는 방법의 개요를 제공합니다.
> 
> 학습 내용:
> 
> - ASP.NET 웹 페이지에서 프로그래밍을 위해 사용 하는 기본 "Razor" 구문입니다.
> - 몇 가지 기본 된 C# 프로그래밍 언어를 사용 합니다.
> - 웹 페이지에 대 한 몇 가지 근본적인 프로그래밍 개념입니다.
> - 사이트에 사용 하도록 (구성 요소 미리 작성 된 코드를 포함 하는) 패키지를 설치 하는 방법입니다.
> - 사용 하는 방법 *도우미* 일반적인 프로그래밍 작업을 수행할 수 있습니다.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - NuGet 및 패키지 관리자입니다.
> - `Gravatar` 도우미입니다.


이 자습서에는 ASP.NET 웹 페이지에 사용할 프로그래밍 구문에 소개 하는 활동이 주로입니다. 에 대 한 알아봅니다 *Razor 구문을* 및 C#에서 작성 된 코드는 프로그래밍 언어입니다. 이 구문의 glimpse; 이전 자습서에서 가져온 이 자습서에서는 자세한 구문을 설명 합니다.

이 자습서에 대 한 단일 자습서에서 확인할 수 있습니다 하 고 있는 유일한 자습서 인지 프로그래밍 가장 과정이 포함 되어 있음을 promise 우리 *만* 프로그래밍에 대 한 합니다. 이 집합의 나머지 자습서에서 실제로 흥미로운 작업을 수행 하는 페이지 만들어야 합니다.

또한에 대 한 알아봅니다 *도우미*합니다. 도우미 구성 요소는-코드의 패키지 위쪽 부분 — 페이지에 추가할 수 있는 합니다. 도우미 길거나을 수동으로 복잡 한 그렇지 있을 수 있습니다에 대 한 작업을 수행 합니다.

## <a name="creating-a-page-to-play-with-razor"></a>Razor를 사용 하 여 재생을 페이지 만들기

이 섹션에서는 재생할 약간 Razor를 사용한 하므로 기본 구문의 의미를 발생할 수 있습니다.

WebMatrix를 아직 실행 되는 경우 시작 합니다. 이전 자습서에서 만든 웹 사이트를 사용 합니다 ([가져오기 시작 된 웹 페이지](https://go.microsoft.com/fwlink/?LinkId=251578)). 다시 여시겠습니까 클릭 **내 사이트** 선택 **WebPageMovies**:

![WebMatrix 시작 화면 열기 사이트 옵션 및 강조 표시 하는 내 사이트를 보여 주는](intro-to-web-pages-programming/_static/image1.png)

선택 된 **파일** 작업 영역입니다.

리본 메뉴에서 클릭 **새로** 페이지를 만듭니다. 선택 **CSHTML** 새 페이지 이름을 *TestRazor.cshtml*합니다.

**확인**을 클릭합니다.

이미 완전히 교체를 파일에 다음을 복사 합니다.

> [!NOTE]
> 예제에서 코드 또는 태그를 페이지에 복사 하면 들여쓰기 및 맞춤 아닐 수 있습니다 자습서와 다릅니다. 들여쓰기 및 맞춤 코드 있지만 실행 되는 방법을 적용 되지 않습니다.


[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>검사 페이지 예

대부분의 표시 되는 일반 HTML입니다. 그러나, 위쪽에는이 코드 블록:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

이 코드 블록에 대 한 다음 사항을 참고 하세요.

- 지시 ASP.NET @ 문자 뒤에 오는 Razor 코드의 HTML이 아닌 임을 합니다. ASP.NET에서는 다음에 오는 모든 처리는 @ 문자 코드로 다시 일부 HTML로 실행 될 때까지 합니다. (이 경우는 &lt;! DOCTYPE&gt; 요소입니다.
- 중괄호 ({및}) 코드에 둘 이상의 줄 Razor 코드 블록을 묶습니다. 해당 블록에 대 한 코드를 시작 하 고 끝나는 위치 중괄호 ASP.NET을 지시 합니다.
- / 문자는 주석을 표시할 /-즉, 실행 되지 하는 코드의 일부입니다.
- 각 문에 세미콜론 (;)로 끝나야 합니다. (하지 설명, 하지만.)
- 에 값을 저장 *변수*, 만들 있는 (*선언*) 키워드 차이와 변수를 만들 때 사용자 이름을 지정, 문자, 숫자 및 밑줄을 포함할 수 있는 (\_). 변수 이름은 숫자로 시작할 수 없습니다 하며 (예: var) 프로그래밍 키워드 이름을 사용할 수 없습니다.
- 따옴표로 문자열을 (예: "ASP.NET" 및 "웹 페이지")를 묶습니다. (큰따옴표 되어야 합니다.) 숫자는 인용 부호에 있지 않습니다.
- 인용 부호 밖에 공백 문제가 되지 않습니다. 대부분 줄 바꿈 중요 하지 않으면 예외는 여러 줄 따옴표로 문자열을 분할할 수 없습니다. 들여쓰기 및 맞춤 중요 하지 않습니다.

이 예제에서 명확 하지 않은 경우 모든 코드는 대/소문자 구분 이 변수 합계가 다른 변수에 변수 이름이 수 합계가 또는 합계가 보다 임을 의미 합니다. 마찬가지로, var 키워드를 하지만 Var 없습니다.

### <a name="objects-and-properties-and-methods"></a>개체 속성 및 메서드

다음 식을 DateTime.Now 있습니다. 간단히 말해서에서 DateTime이는 *개체*합니다. 이 이벤트는 개체를 프로그래밍할 수 있는 항목 — 페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 등입니다. 개체 하나 이상 있을 *속성* 특징을 설명 하는 합니다. 텍스트 상자 개체에는 Text 속성 (등), 요청 개체는 Url 속성 (및 기타), 전자 메일 메시지에는 From 속성과 To 속성에 있습니다. 개체에 있습니다 *메서드* 하는 "동사" 수행할 수 있습니다. 작업할 개체와 사용을 너무 많이 있습니다.

이 예제에서는 알 수 있듯이 DateTime은 프로그램 날짜 및 시간 수 있는 개체. 현재 날짜와 시간을 반환 하는 이제 라는 속성이 있습니다.

### <a name="using-code-to-render-markup-in-the-page"></a>코드를 사용 하 여 페이지에는 태그를 렌더링 하

페이지 본문에서 다음을 확인 합니다.

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

다시는 @ 문자 asp 그 뒤에 오는 코드를 HTML이 아닌 합니다. 태그에 추가할 수 뒤에 코드 식으로 있으며 ASP.NET 해당 식 오른쪽의 값을 해당 지점에서 렌더링 됩니다. 예제에서는 @a 이라는 변수의 값은 무엇이 든 렌더링 a, @product 변수 명명 된 제품 및 등 무엇이 렌더링 합니다.

제한 되지는 변수에 하지만 합니다. 몇 가지 점에서 여기에서 @ 문자는 식 앞에 옵니다.

- @(한\*b) 변수에 무엇이 곱일 렌더링 한와 b 합니다. (의 \* 연산자 곱하기를 의미 합니다.)
- @(기술 + "" + 제품) 사이 공백을 추가 하 고 연결 후 변수 기술 및 제품의 값을 렌더링 합니다. 문자열 연결에 대 한 연산자 (+)는 숫자를 추가 하기 위한은 연산자와 같습니다. 숫자 또는 문자열 작업 하 고 올바른 작업으로 수행 하 여부를 일반적으로 ASP.NET 알 수는 + 연산자입니다.
- @Request.Url 요청 개체의 Url 속성을 렌더링합니다. 요청 개체를 브라우저에서 현재 요청에 대 한 정보를 포함 하 고 Url 속성은 현재 요청의 URL을 포함 하는 물론 합니다.

이 예제에서는 설정할 수 있는 작업 않는 다양 한 방식에서 보여주도록 설계 되어 있습니다. 맨 위에 있는 코드 블록에는 계산을 수행 하 고, 결과 변수에 설정 하 고, 태그에서 변수를 렌더링 한 다음 수 있습니다. 또는 태그에는 식 오른쪽에 있는 계산을 수행할 수 있습니다. 사용 하는 방법에 따라 다릅니다 사람에 게, 사용자 고유의 기본 설정에 어느 정도 까지는.

### <a name="seeing-the-code-in-action"></a>작업의 코드를 표시합니다.

파일의 이름을 마우스 오른쪽 단추로 클릭 하 고 눌러 **브라우저에서 시작**합니다. 모든 값과 페이지에서 해결 하는 식을 사용 하 여 브라우저에서 페이지를 참조 합니다.

![브라우저에서 실행 되 고 'TestRazor' 페이지](intro-to-web-pages-programming/_static/image2.png)

브라우저에서 소스를 확인 합니다.

![브라우저에서 페이지 소스 'Razor ' 테스트'](intro-to-web-pages-programming/_static/image3.png)

이전 자습서의 사용자 환경에서 예상한 대로 Razor 코드의 없음 페이지에서입니다. 실제 표시 값이 표시 됩니다. 페이지를 실행 하면 실질적인 요청 WebMatrix에는 기본 제공 웹 서버에 있습니다. 요청을 받으면 ASP.NET 값과 식을 확인 하 고 페이지에 해당 값을 렌더링 합니다. 다음 페이지를 브라우저에 보냅니다.

> [!TIP] 
> 
> **Razor 및 C#**
> 
> 지금까지 Razor 구문을 사용 하 고 있음을 말한 것입니다. 이것이 사실 있지만 전체 스토리 아닙니다. 사용 중인 실제 프로그래밍 언어 라고 *C#* 합니다. C# 10 년 전에 대해 Microsoft에서 생성 된 및 Windows 앱을 만들기 위한 기본 프로그래밍 언어 중 하나로 성장 했습니다. 지금까지 살펴본 변수에 이름을 지정 하는 방법 및 등 문을 작성 하는 방법에 대 한 모든 규칙은 C# 언어의 모든 규칙 실제로 합니다.
> 
> Razor 좀 더 구체적으로이 코드 페이지에 포함 되는 방법에 대 한 규칙의 작은 집합을 나타냅니다. 을 사용 하 여 코드 페이지에 표시 하 고 사용 하 여 규칙 예를 들어 @ {} 코드 블록을 포함 하는 페이지의 Razor 측면입니다. 도우미는 Razor의 일부로 간주 됩니다. Razor 구문이 ASP.NET 웹 페이지에서 보다 더 많은 장소에 사용 됩니다. (예를 들어 사용 됩니다 ASP.NET MVC 뷰에.)
> 
> 많은 Razor에 대 한 참조를 찾을 수 프로그래밍 ASP.NET 웹 페이지에 대 한 정보에 대 한 보면 때문에이 언급 합니다. 하지만 해당 참조의 많은 기능 수행 하 고 따라서 혼동 될 수에 적용 하지 않습니다. 및 실제로 다양 한 프로그래밍 질문 실제로 하려는 작업을 C# 또는 ASP.NET을 사용 하는 방법에 대 한 합니다. 따라서 Razor에 대 한 정보에 대 한 구체적으로 보면 필요한 답변 찾지 못할 수 있습니다.


## <a name="adding-some-conditional-logic"></a>일부 조건부 논리 추가

코드 페이지를 사용 하는 방법에 대 한 뛰어난 기능 중 하나를 어떤 일이 생기 따라 다양 한 조건에 변경할 수입니다. 자습서의이 부분에서는 페이지에 표시 되는 내용 변경 하는 몇 가지 시도해보고 합니다.

이 예제에서는 간단한와 다소 거리가 있습니다 조건부 논리에 집중할 수 있도록 됩니다. 만들게 페이지는이 수행 합니다.

- 처음으로 인지에 따라 페이지가 표시 됩니다 또는 페이지를 전송 하는 단추를 클릭 한 여부 페이지에서 다양 한 텍스트를 표시 합니다. 첫 번째 조건 테스트가 사용 됩니다.
- URL (http://...?show=true)의 쿼리 문자열에 특정 값이 전달 하는 경우에 메시지를 표시 합니다. 두 번째 조건 테스트가 사용 됩니다.

WebMatrix에서 페이지를 만들고 이름을 *TestRazorPart2.cshtml*합니다. (리본 메뉴에서 클릭 **새로**, 선택 **CSHTML**파일 이름을 지정 하 고 클릭 한 다음, **확인**.)

해당 페이지의 내용을 다음으로 바꿉니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

맨 위에 있는 코드 블록에는 일부 텍스트와 메시지 변수를 초기화 합니다. 페이지 본문의 메시지 변수 내용을 안에 표시 됩니다는 &lt;p&gt; 요소입니다. 태그를 포함 한 &lt;입력&gt; 만들 요소는 **전송** 단추 합니다.

이제 작동 방식을 보려면 페이지를 실행 합니다. 지금은 앱은 기본적으로 정적 페이지를 클릭 하더라도 **전송** 단추입니다.

WebMatrix로 돌아갑니다. 코드 블록 안에 다음 강조 표시 된 코드를 추가 *후* 메시지를 초기화 하는 줄:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>If {} 블록

If가 방금 추가한 어떤 조건입니다. 코드에서의 조건에는 구조가 다음과 같은 경우:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

괄호 안에 테스트할 조건이입니다. 후에 값 또는 true 또는 false를 반환 하는 식 이어야 합니다. 조건이 true 이면 ASP.NET 중괄호 내에 있는 문은 실행 합니다. (모두는 *다음* 의 일부로 *if then* 논리.) 조건이 false 이면 코드 블록을 건너뜁니다.

다음은 조건 if에서 테스트할 수의 몇 가지 예제 문:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

식 또는 값에 대 한 변수를 사용 하 여 테스트할 수 있습니다는 <em>논리 연산자</em> 또는 <em>비교 연산자</em>: 같음 (= =), 보다 큼 (&gt;), 미만 (&lt;), 보다 크거나 같음 (&gt;=), 보다 작거나 같음 (&lt;=) 합니다. ! = 같지 않음 연산자 의미-예를 들어 경우 (한! = 0) 의미 <em>경우</em> <em>는</em><em>0과 같지 않은</em>합니다.

> [!NOTE]
> 같음 (= =)에 대 한 비교 연산자는 = 동일 확인할 수 있는지 확인 합니다. = 연산자 값을 할당 하는 데에 사용 됩니다 (var는 = 2). 이러한 연산자 혼합 하면 오류가 얻게 또는 이상한 결과 얻게 됩니다.


무언가 true 인지를 테스트 하려면 전체 구문은 if(IsDone == true) 합니다. 하지만 바로 가기 if(IsDone) 사용할 수도 있습니다. 비교 연산자가 없습니다 이면 ASP.NET true에 대 한 테스트 한다고 가정 합니다.

! 단독으로 연산자는 논리 NOT을 의미합니다. 예를 들어 조건 if (! IsPost) 의미 *IsPost true가 아니면*합니다.

논리 AND를 사용 하 여 조건을 결합할 수 있습니다 (&amp; &amp; 연산자) 또는 논리 OR (| | 연산자). 이전 예제에에서 마지막 if 조건 예를 들어 *true AND 표시 메시지를 false로 설정 되어 FileProcessingIsDone로 설정 되지 않은 경우*합니다.

### <a name="the-else-block"></a>Else 블록

If에 대 한 할 사항이 하나 블록:는 else 블록 블록 뒤 될 수 있습니다. Else 블록 유용은 조건이 false 인 경우 다른 코드를 실행 해야 합니다. 간단한 예는 다음과 같습니다.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

이후의 자습서 else 블록을 사용 하는 유용한이 시리즈의 몇 가지 예제에 표시 됩니다.

### <a name="testing-whether-the-request-is-a-submit-post"></a>요청이 제출 (post) 인지를 테스트 합니다.

더 많은, 하지만 돌아가 보겠습니다 조건 if(IsPost) {...}를 하는 예제입니다. IsPost은 실제로 현재 페이지의 속성입니다. 처음으로 페이지를 요청 IsPost false를 반환 합니다. 그러나 단추를 클릭 하거나 그렇지 않으면 페이지를 전송 하는 경우-게시 즉,-IsPost true를 반환 합니다. 따라서 IsPost 양식 제출 하 여 다룰 때는 여부를 결정할 수 있습니다. (HTTP 동사를 기준으로 요청 되는 가져오기 작업을 IsPost false를 반환 합니다. 요청이 있는 POST 작업 인 경우 IsPost true를 반환 합니다.) 자습서의 뒷부분에서 다루게 입력된 양식,이 테스트는 특히 유용 합니다.

페이지를 실행 합니다. 요청 하는 처음으로 이므로 "This is 처음으로 페이지를 요청 했습니다"을 참조 페이지입니다. 해당 문자열은 메시지 변수를 초기화 하는 값입니다. if(IsPost) 테스트 하지만 if 내의 코드를 차단 하는 반환 false는 현재 실행 되지 않습니다.

클릭는 **전송** 단추입니다. 페이지를 다시 요청 합니다. 로 "This is 처음..."를 이전에 메시지 변수가 설정 됩니다. 하지만이 이번에 if 내에 있는 코드 실행을 차단 하므로 테스트 if(IsPost) true를 반환 합니다. 태그에서 렌더링 됩니다을 다른 값으로 메시지 변수 값을 변경 하는 코드입니다.

이제 if 추가 태그에는 조건입니다. 아래는 &lt;p&gt; 요소를 포함 하는 **전송** 단추, 다음 태그를 추가 합니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

시작 하 여 해야 하므로 태그 내에서 코드를 추가 하는 @합니다. If이 테스트와 유사한 이전에 추가한 코드 블록에 있습니다. 중괄호 안의 하지만 추가 하는 일반 HTML-적어도 일반 도달할 때까지 @DateTime.Now합니다. Razor 코드의 약간 다른 이것이 다시 추가 해야 앞에 있습니다.

여기 점이 위쪽 및 태그에서 조건 모두에 코드를 차단 하는 경우 추가할 수 있습니다. If를 사용 하는 경우 태그 또는 코드 블록 안에 줄 페이지의 본문에는 조건이 될 수 있습니다. 이 경우 있도록 ASP.NET 코드의 위치를 사용 해야 하는 태그와 코드를 혼합 하 여 언제 든 지 true 인, 및입니다.

페이지를 실행 하 고 클릭 **전송**합니다. 이 시간 뿐만 아니라 다른 메시지가 표시 ("이제 사용자가 제출한...")을 전송 하면 되지만 날짜 및 시간을 나열 하는 새 메시지를 표시 하는 경우.

![다음 표시 타임 스탬프와 브라우저에서 실행 되는 'test Razor 2' 페이지에 제출](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>쿼리 문자열의 값을 테스트

한 더 많은 테스트 합니다. If 추가이 이번에는 값을 테스트 하는 블록 라는 쿼리 문자열에 전달 될 수 있는 표시 합니다. (다음과 같은: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) 메시지 있습니다 한 된 표시 되도록 페이지를 변경 합니다 ("이것이 처음..." 등) 표시의 값은 경우에 표시 됩니다.

페이지 맨 위에 있는 코드 블록 아래쪽 (그러나 내부)에서 다음을 추가.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

다음 예제와 같은 전체 코드 블록 지금은 모양입니다. (기억 페이지에 코드를 복사 하는 경우 들여쓰기 다르게 보일 수 있습니다. 하지만 코드 실행 하는 방법에 영향을 주지입니다.)

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

블록의 새 코드를 false로 매개 변수를 초기화 합니다. 그런 다음 if 수행 테스트에 쿼리 문자열의 값을 찾으십시오. 페이지를 처음으로 요청할 때 다음과 같은 URL에 있습니다.

`http://localhost:43097/TestRazorPart2.cshtml`

코드는 URL 쿼리 문자열의 예: URL의이 버전에는 show 라는 변수가 포함 되어 있는지 여부를 결정 합니다.

`http://localhost:43097/TestRazorPart2.cshtml`?show=true

자체 테스트 요청 개체의 QueryString 속성을 살펴봅니다. 쿼리 문자열에는 명명 된 항목 표시 하 고 해당 항목이 if를 true로 설정 된 경우 블록 실행 및 매개 변수를 true로 설정 합니다.

볼 수 있듯이 여기에서 트릭을 있습니다. 이름에서 지정한 대로 쿼리 문자열에는 문자열이입니다. 그러나 테스트할 수 있습니다만 true와 false를 테스트 하는 값이 부울 (true/false) 값입니다. 쿼리 문자열에서 표시 변수 값을 테스트할 수 있습니다, 전에 부울 값으로 변환 해야 합니다. 즉, AsBool 메서드가 수행 하는 작업-입력으로 문자열을 사용 하 고 부울 값을 변환 합니다. 명확 하 게 문자열은 "true" AsBool 메서드 해당 값을 true로 변환 합니다. 문자열의 값이 다른 것 이면 AsBool false를 반환 합니다.

> [!TIP] 
> 
> **데이터 형식 및 as () 메서드**
> 
> 만 말한 것 지금까지 변수를 만들 때 사용 하는 키워드 차이 가 아닌 전체 스토리 하지만입니다. 값을 조작 하기 위해-숫자를 추가 또는 문자열을 연결 또는 날짜를 비교 하거나 true/false에 대 한 테스트-C#에서 값의 적절 한 내부 표현으로 사용 해야 합니다. C# 수 *일반적으로* 표현을 해야 하는지 파악 (즉, 어떤 *형식* 데이터는) 기반으로 하는 일 값을 사용 합니다. 하지만 없습니다입니다. 그렇지 않으면 명시적으로 어떻게 C#을 나타내야 데이터를 지정 하 여 도움을 해야 합니다. AsBool 메서드는-"true" 또는 "false"의 문자열 값을 부울 값으로 처리 해야 함을 C# 표시 합니다. 이와 유사한 메서드 AsInt (treat 정수로), AsDateTime (날짜/시간으로 처리), AsFloat (부동 소수점 숫자로 처리) 등도 다른 형식으로 문자열을 나타내기 위해 존재 합니다. C# 수 없는 문자열 값을 나타내는 요청 하는 경우이 방법으로 () 메서드 사용, 하는 경우 오류가 표시 됩니다.


페이지의 태그를 제거 하거나이 요소를 주석 처리 (여기 그림 주석으로 처리):

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

다음 오른쪽 제거 되거나 해당 텍스트를 주석 처리를 추가 합니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

테스트 매개 변수가 true 이면 렌더링 하는 표시 되 면는 &lt;p&gt; 메시지 변수 값을 가진 요소가 있습니다.

### <a name="summary-of-your-conditional-logic"></a>조건부 논리의 요약

까지 방금 작업 한 내용을 완전히 하는지 모르는 경우은 다음과 같습니다.

- 메시지 변수는 기본 문자열으로 초기화 됩니다 ("이것이 처음...").
- "이제 사용자가 제출한..." 메시지의 값으로 변경 된 페이지 요청이 제출 (post)의 결과 상태인 경우
- 매개 변수를 false로 초기화 됩니다.
- 쿼리 문자열에 포함 되어 있는 경우? 표시 = true 이면 매개 변수가 설정 되어 true로 합니다.
- 이 true 이면 매개 태그에는 &lt;p&gt; 메시지의 값을 보여 주는 요소가 렌더링 됩니다. (매개 false 이면 렌더링이 시점 태그에 있습니다.)
- 태그는 post 요청이 시작 된 경우에 &lt;p&gt; 날짜와 시간을 표시 하는 요소가 렌더링 됩니다.

페이지를 실행 합니다. 매개가 false 이면 if(showMessage) 테스트 태그에서 false 반환 하기 때문에 메시지가 없는 있습니다.

**제출**을 클릭합니다. 날짜 및 시간, 있지만 메시지가 없는 여전히 표시 됩니다.

브라우저에서 URL 상자도 이동 하 고 URL의 끝에 다음 추가:? 표시 = true 및 다음 Enter 키를 누릅니다.

![쿼리 문자열을 표시 하는 브라우저에서 페이지 '테스트 Razor 2'](intro-to-web-pages-programming/_static/image5.png)

페이지 다시 표시 됩니다. (URL 변경 때문에 새 요청을 전송 하지 않습니다.) 클릭 **전송** 다시 합니다. 날짜 및 시간으로 메시지가 다시 표시 됩니다.

![이후 페이지 'Razor 2 테스트' 쿼리 문자열이 때에서 제출](intro-to-web-pages-programming/_static/image6.png)

URL에서 변경? 표시 = true를? 표시 = false 및 Enter 키를 누릅니다. 페이지를 다시 전송 합니다. 페이지를 다시 시작 하는 방법-메시지가 없습니다.

앞에서 설명한 대로이 예제의 논리 거리가 약간 것입니다. 그러나에서 다양 한 페이지를 발견 하는 경우, 걸립니다를 살펴 보았으며 형식 중 하나 이상을 여기 고 합니다.

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>도우미 메서드 (Gravatar 이미지 표시)를 설치 합니다.

사용자 웹 페이지에서 작업을 수행 하고자 하는 몇 가지 작업 코드 많이 필요 하거나 추가 정보가 필요 합니다. 예: 데이터에 대 한 차트를 표시합니다. 페이지에 Facebook "좋아요" 단추를 배치 합니다. 웹 사이트에서 메일을 보내는 중 자르기 또는; 이미지 크기 조정 PayPal을 사용 하 여 사이트에 대 한 합니다. 이러한 종류의 작업을 수행 하기 쉽도록 ASP.NET 웹 페이지 사용 하면 사용 하 여 *도우미*합니다. 도우미는 사이트에 대해 설치 하 고 Razor 코드의 몇 줄을 사용 하 여 일반적인 작업을 수행할 수 있는 구성 요소.

ASP.NET 웹 페이지에서 기본적으로 제공 하는 몇 가지 도우미에 있습니다. 그러나 많은 도우미는 NuGet 패키지 관리자를 사용 하 여 제공 되는 (추가 기능) 패키지에서 사용할 수 있습니다. 설치의 모든 세부 정보는 담당 다음 및 NuGet 패키지를 설치 하도록 선택할 수 있습니다.

자습서의이 부분에서는 Gravatar ("전체적으로 인식 된 아바타") 이미지를 표시할 수 있는 도우미를 설치 합니다. 다음 두 가지를 설명 합니다. 하나를 찾아서 도우미를 설치 하는 방법입니다. 또한 도우미 손쉽게 방법을 직접 작성 해야 하는 코드를 많이 사용 하 여 작업을 수행 하 고, 그렇지 해야 작업을 설명 합니다.

Gravatar 웹 사이트에서 사용자 고유의 Gravatar를 등록할 수 있습니다 [ http://www.gravatar.com/ ](http://www.gravatar.com/), 이지만를 반드시 자습서의이 부분을 수행할 수 있는 Gravatar 계정을 만들어야 합니다.

WebMatrix에서 클릭 하 고 **NuGet** 단추입니다.

![WebMatrix에서 NuGet 갤러리 대화 상자](intro-to-web-pages-programming/_static/image7.png)

이 NuGet 패키지 관리자를 시작 하 고 사용 가능한 패키지를 표시 합니다. (모든 패키지에는 도우미; 일부 추가 기능 자체는 WebMatrix에 일부 추가 서식 파일을 등.) 버전 비 호환성에 대 한 오류 메시지가 발생할 수 있습니다. 클릭 하 여이 오류 메시지를 무시할 수 **확인** 및이 자습서를 진행 합니다.

![WebMatrix에서 NuGet 갤러리 대화 상자](intro-to-web-pages-programming/_static/image8.png)

검색 상자에 "asp.net 도우미"를 입력 합니다. NuGet 검색 단어와 일치 하는 패키지를 표시 합니다.

![패키지를 보여 주는 WebMatrix에서 NuGet 갤러리](intro-to-web-pages-programming/_static/image9.png)

ASP.NET Web Helpers Library Gravatar 이미지의 사용을 포함 하 여 여러 가지 일반적인 작업을 간소화 하기 위해 코드를 포함 합니다. 선택 된 **ASP.NET Web Helpers Library** 패키지 하 고 클릭 **설치** 설치 관리자를 시작 해야 합니다. 선택 **예** 패키지를 설치 하 고 설치를 완료 하려면 조건에 동의 하려면 메시지가 표시 되 면 합니다.

이제 NuGet 다운로드 하 고 필요할 수 있는 모든 추가 구성 요소를 포함 한 모든 설치 (*종속성*).

어떤 이유로 도우미 메서드를 제거 해야 할, 프로세스 매우 비슷합니다. 클릭는 **NuGet** 단추를 클릭 하 여는 **설치 됨** 탭을 제거 하려는 패키지를 선택 합니다.

## <a name="using-a-helper-in-a-page"></a>도우미 메서드를 사용 하 여 페이지에서

이제 방금 설치한 도우미를 사용 합니다. 도우미 페이지에 추가 하기 위한 프로세스는 대부분 도우미에 대 한 비슷합니다.

WebMatrix에서 페이지를 만들고 이름을 *GravatarTest.cshml*합니다. (특별 한 페이지 도우미, 테스트를 만드는 있지만 사이트의 모든 페이지에 도우미를 사용할 수 있습니다.)

내에서 &lt;본문&gt; 요소를 추가 &lt;div&gt; 요소입니다. 내부는 &lt;div&gt; 요소를 다음과 같이 입력 합니다.

@Gravatar.

@ 문자는 Razor 코드 표시에 사용 했던 동일한 문자입니다. **Gravatar** 작업할 때 있는 도우미 개체입니다.

WebMatrix의 목록을 표시 마침표 (.)를 입력 하는 즉시 *메서드* Gravatar 도우미 사용할 수 있도록 (역할):

![Gravatar 도우미 IntelliSense 드롭 다운 목록](intro-to-web-pages-programming/_static/image10.png)

이 기능은 라고 *IntelliSense*합니다. 컨텍스트에 따라 적절 한 선택 항목을 제공 하 여 작성 한 코드가 도움이 됩니다. IntelliSense는 HTML, CSS, ASP.NET 코드, JavaScript 및 WebMatrix에서 지원 되는 다른 언어에서 작동 합니다. 다른 기능 쉽게 WebMatrix에서 웹 페이지를 개발 하는 수입니다.

키보드에 G 키 참조 IntelliSense GetHtml 메서드를 찾습니다. Tab 키를 눌러 합니다. IntelliSense를 (GetHtml) 선택한 메서드를 삽입합니다. 여는 괄호를 입력 하 고 닫는 괄호 자동으로 추가 됩니다. 따옴표 두 괄호 사이에서 전자 메일 주소를 입력 합니다. Gravatar 계정이 있는 경우 프로필 사진 반환 됩니다. Gravatar 계정이 없는 경우 기본 이미지 반환 됩니다. 완료 되 면 줄은 다음과 같습니다.

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

이제는 브라우저에서 페이지를 표시 합니다. Gravatar 계정이 있는지 여부에 따라 그림 또는 기본 이미지가 표시 됩니다.

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![기본 이미지](intro-to-web-pages-programming/_static/image12.png)

어떤 아이디어 도우미 수행 하는 작업을, 브라우저에서 페이지의 소스를 검토 합니다. HTML 페이지에 있던 함께 식별자를 포함 하는 이미지 요소를 볼 수 있습니다. 이 도우미 많았습니다 곳에서 페이지에 렌더링 하는 코드는 @Gravatar.GetHtml합니다. 도우미 정보를 제공 하 고 제공 된 계정에 대 한 올바른 이미지를 다시 얻기 위해 Gravatar에 직접 통신 하는 코드를 생성 했습니다.

또한 GetHtml 메서드를 사용 하면 다른 매개 변수를 제공 하 여 이미지를 사용자 지정할 수 있습니다. 다음 코드에서는 너비와 높이가 40 픽셀의 이미지를 요청 하 라는 지정 된 기본 이미지를 사용 하는 방법을 보여 줍니다. **wavatar** 지정한 계정이 존재 하지 않는 경우.

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

이 코드의 결과 (기본 이미지가 됩니다 다 임의로) 다음과 같은 결과가 같습니다.

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>다음에 나오는

이 자습서 짧은 유지 하기 위해 기본 몇 가지 사항에 집중 해야 했습니다. 물론는 *많은* Razor 및 C#을 더 합니다. 이 자습서를 통해 이동으로 설명 합니다. 현재 Razor 및 C#의 프로그래밍 요소에 대해 자세히 알고 싶은 경우 여기에 보다 철저 한 소개를 읽을 수 있습니다: [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkID=202890)합니다.

다음 자습서는 데이터베이스 사용을 소개 합니다. 해당 자습서의 하면 좋아하는 영화를 나열할 수 있는 샘플 응용 프로그램을 만들기 시작할 합니다.

## <a name="complete-listing-for-testrazor-page"></a>TestRazor 페이지에 대 한 전체 목록을 보려면

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>TestRazorPart2 페이지에 대 한 전체 목록을 보려면

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>GravatarTest 페이지에 대 한 전체 목록을 보려면

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>추가 자료

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Twitter 도우미](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [이전](getting-started.md)
> [다음](displaying-data.md)
