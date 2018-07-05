---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: ASP.NET 웹 페이지 소개-프로그래밍의 기초 | Microsoft Docs
author: tfitzmac
description: "이 자습서 Razor 구문이 있는 ASP.NET 웹 페이지에서 프로그램에는 방법에 대 한 개요를 제공합니다. 학습할 내용: 기본 'Razor' 구문을 pr에 사용 하는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/17/2015
ms.topic: article
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 3824db99b3313876585fe284c254ac89b256bc8f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383247"
---
<a name="introducing-aspnet-web-pages---programming-basics"></a>ASP.NET 웹 페이지 프로그래밍 기본 사항 소개
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 Razor 구문이 있는 ASP.NET 웹 페이지에서 프로그램에는 방법에 대 한 개요를 제공합니다.
> 
> 학습할 내용:
> 
> - ASP.NET 웹 페이지의 프로그래밍에 사용 하는 기본 "Razor" 구문입니다.
> - 일부 기본 C#를 사용 하 여 프로그래밍 언어입니다.
> - 웹 페이지에 대 한 몇 가지 기본적인 프로그래밍 개념입니다.
> - 사이트 사용 (구성 요소 미리 작성 된 코드를 포함 하는) 패키지를 설치 하는 방법입니다.
> - 사용 하는 방법 *도우미* 일반적인 프로그래밍 작업을 수행할 수 있습니다.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - NuGet 및 패키지 관리자입니다.
> - `Gravatar` 도우미입니다.


이 자습서는 주로 ASP.NET 웹 페이지를 사용 하는 프로그래밍 구문을 소개 연습입니다. 에 대해 알아봅니다 *Razor 구문* 및 C#에서 작성 된 코드는 프로그래밍 언어입니다. 이 구문의 잠깐은 이전 자습서에서 가져온 이 자습서에서는 자세한 구문에 설명 합니다.

이 자습서에서는 단일 자습서의 경우에 표시 됩니다는 유일한 자습서는 프로그래밍 대부분은 약속 드립니다 *만* 프로그래밍에 대 한 합니다. 이 집합의 나머지 자습서에서 실제로 흥미로운 작업을 수행 하는 페이지 만들어야 합니다.

에 대 한 사례도 *도우미*합니다. 도우미는 구성 요소-코드 패키지 접속 부분-페이지에 추가할 수 있는 합니다. 그렇지 않으면 길거나 복잡 손으로 수 있습니다 하는 작업을 수행 하는 도우미입니다.

## <a name="creating-a-page-to-play-with-razor"></a>Razor를 사용 하 여 재생 페이지 만들기

이 섹션을 재생할 약간 Razor를 사용한 기본 구문의 이해를 얻을 수 있습니다.

아직 실행 되는 경우에 WebMatrix를 시작 합니다. 이전 자습서에서 만든 웹 사이트를 사용 하 여 ([가져오는 시작 된 웹 페이지](https://go.microsoft.com/fwlink/?LinkId=251578)). 닫았다가, 클릭 **내 사이트** 선택한 **WebPageMovies**:

![WebMatrix 시작 사이트 열기 옵션과 강조 표시 하는 내 사이트를 보여 주는 화면](intro-to-web-pages-programming/_static/image1.png)

선택 된 **파일** 작업 영역입니다.

리본 메뉴에서 클릭 **새로 만들기** 페이지를 만듭니다. 선택 **CSHTML** 하 고 새 페이지 이름을 *TestRazor.cshtml*합니다.

**확인**을 클릭합니다.

무엇이 있는지 이미 완전히 교체 파일에 다음을 복사 합니다.

> [!NOTE]
> 예제에서 코드 또는 태그를 페이지에 복사 하면 들여쓰기 및 맞춤 아닐 자습서와 동일 합니다. 들여쓰기 및 맞춤 어떻게 코드를 실행 하지만 영향을 주지 않습니다.


[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>예제 페이지를 검사합니다.

표시 되는 항목의 대부분에는 일반 HTML입니다. 위쪽에 있는 것 인데,이 코드 블록:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

이 코드 블록에 대 한 다음 작업을 확인 합니다.

- @ 문자 인지 여부를 ASP.NET는 다음 HTML이 아닌 Razor 코드입니다. ASP.NET은 처리 후의 모든는 @ 문자 코드로 다시 몇 가지 HTML로 실행 될 때까지 합니다. (이 경우에는 &lt;! DOCTYPE&gt; 요소입니다.
- 중괄호 ({및}) 코드에 둘 이상의 줄 Razor 코드 블록을 묶습니다. 해당 블록에 대 한 코드를 시작 하 고 끝나는 위치 중괄호 ASP.NET을 알려 줍니다.
- / 문자 주석 표시 /-즉, 실행 되지 않습니다 하는 코드의 일부입니다.
- 각 문을 세미콜론 (;)를 사용 하 여 종료 해야 합니다. (없습니다 주석을 통해.)
- 값을 저장할 수 있습니다 *변수*를 만들 수 있는 (*선언*) 키워드 차이 사용 하 여 변수를 만들 때 사용자 이름을, 문자, 숫자 및 밑줄을 포함할 수 있는 (\_). 변수 이름은 숫자로 시작할 수 없습니다 하며 (예: var) 프로그래밍 키워드를 사용할 수 없습니다.
- 문자열을 (예: "ASP.NET" 및 "웹 페이지") 따옴표로 묶습니다. (큰따옴표 여야 합니다 있습니다.) 숫자는 인용 부호에 있지 않습니다.
- 공백을 따옴표 외부에서 중요 하지 않습니다. 줄 바꿈에는 주로 다음이 중요 하지; 여러 줄 따옴표 안의 문자열을 분할할 수 없습니다 하는 예외가입니다. 맞춤 및 들여쓰기는 중요 하지 않습니다.

이 예제에서 명확 하지 않은 것은 모든 코드가 대/소문자 구분입니다. 이 변수 합계가 합계가 또는 합계가 이름이 될 수 있는 변수 보다 다른 변수에 임을 의미 합니다. 마찬가지로, var 키워드 이지만 Var 아닙니다.

### <a name="objects-and-properties-and-methods"></a>개체 속성 및 메서드

DateTime.Now 식이 됩니다. 간단히 말해에서 DateTime은는 *개체*합니다. 개체가 사용 하 여 프로그래밍할 수 있는 것-페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 등입니다. 개체에는 하나 이상의 *속성* 특징을 설명 하는 합니다. 텍스트 상자 개체 등 텍스트 속성이, 요청 개체 Url 속성 (및 기타)에 전자 메일 메시지에는 From 속성과 To 속성인 등입니다. 개체도 가집니다 *메서드* 는 "동사"을 수행할 수 있습니다. 많은 개체를 사용 하 여 사용 됩니다.

예제에서 보듯이 DateTime은 프로그램 날짜 및 시간 수 있는 개체입니다. 여기에 현재 날짜와 시간을 반환 하는 이제 라는 속성이 있습니다.

### <a name="using-code-to-render-markup-in-the-page"></a>코드를 사용 하 여 페이지의 태그를 렌더링 합니다.

페이지의 본문에서 다음을 확인 합니다.

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

마찬가지로 @ 문자 ASP.NET에 지시 하는 그 뒤에 나오는 HTML이 아닌 코드입니다. 태그를 추가할 수 있습니다 뒤에 코드 식 및 ASP.NET 식 오른쪽에 해당 값을 해당 지점에서 렌더링 됩니다. 예에서 @a 명명 된 변수의 값이 무엇이 든 렌더링을 @product 변수 명명 된 제품 및 등 무엇이 렌더링 합니다.

모르는 변수를 제한 하지만 합니다. 몇 가지 점에서 여기에 @ 문자 앞에 오는 식:

- @(한\*b)를 곱한 값에 변수를 렌더링 합니다.는 및 b. (의 \* 연산자는 곱하기를 의미 합니다.)
- @(기술 + "" + 제품) 사이 공백을 추가 하 고 연결 후 변수 기술 및 제품의 값을 렌더링 합니다. 문자열 연결 연산자 (+)가 숫자를 더하는입니다 연산자와 동일 합니다. 문자열 또는 숫자를 사용 하 여 작업 하는 하 고 사용 하 여 올바른 작업을 수행 하는지 여부를 일반적으로 ASP.NET 알 수는 + 연산자입니다.
- @Request.Url 요청 개체의 Url 속성을 렌더링합니다. 요청 개체 브라우저에서 현재 요청에 대 한 정보를 포함 하 고 Url 속성은 현재 요청의 URL을 포함 하는 과정입니다.

예제는 또한 수 있는 작업 않는 다른 방법으로 표시 하도록 설계 됩니다. 맨 위에 있는 코드 블록에는 계산을 수행 하 고, 결과 변수에 삽입 하 고, 다음 태그에서 변수를 렌더링 수 있습니다. 또는 태그에는 식 오른쪽에 있는 계산을 수행할 수 있습니다. 사용 하는 방법이 무엇에, 사용자 고유의 기본 설정에 어느 정도 따라 달라 집니다.

### <a name="seeing-the-code-in-action"></a>작업의 코드를 표시합니다.

파일의 이름을 마우스 오른쪽 단추로 클릭 하 고 선택한 **브라우저에서 시작**합니다. 모든 값 및 페이지에서 해결 하는 식을 사용 하 여 브라우저에서 페이지가 표시 됩니다.

![브라우저에서 실행 되는 'TestRazor' 페이지](intro-to-web-pages-programming/_static/image2.png)

브라우저에서 소스를 확인 합니다.

![브라우저에서 페이지 소스 'Razor ' 테스트'](intro-to-web-pages-programming/_static/image3.png)

이전 자습서의 사용자 환경에서 예상한 대로 페이지에는 Razor 코드의 없음입니다. 실제 표시 값이 표시 됩니다. 페이지를 실행 하면 실제로 변경 하려는 요청을 WebMatrix로 빌드되는 웹 서버입니다. 요청을 받으면 ASP.NET 모든 값과 식을 확인 하 고 페이지에 해당 값을 렌더링 합니다. 그런 다음 페이지를 브라우저에 보냅니다.

> [!TIP] 
> 
> **Razor 및 C#**
> 
> 지금까지 Razor 구문을 사용 하 여 작업 중인 말한 것입니다. 이것이 사실 이지만 전체 목록이 아닙니다. 사용 중인 실제 프로그래밍 언어 라고 *C#* 합니다. C#은 10 년 전 Microsoft에서 만든 및 Windows 앱을 만들기 위한 기본 프로그래밍 언어 중 하나가 되었습니다. 지금까지 살펴본 변수에 이름을 지정 하는 방법 및 등에 문을 작성 하는 방법에 대 한 모든 규칙은 C# 언어의 모든 규칙 실제로 합니다.
> 
> Razor는 페이지에이 코드를 포함 하는 방법에 대 한 규칙의 작은 집합을 좀 더 구체적으로 가리킵니다. 를 사용 하 여 페이지의 코드를 표시 하 고 사용 하는 규칙 예를 들어 @ {} 코드 블록을 포함 하는 페이지의 Razor 측면입니다. 도우미는 Razor의 일부로 간주 됩니다. Razor 구문에서 ASP.NET 웹 페이지 보다 더 많은 장소에서 사용 됩니다. (예를 들어,이 ASP.NET MVC 보기도 합니다.)
> 
> 언급 하는 것이 있으므로 프로그래밍 ASP.NET 웹 페이지에 대 한 정보를 찾으려는 경우 많은 Razor에 대 한 참조를 찾을 수 있습니다. 그러나 이러한 참조의 많은 새로운 자신이 수행 하 고 혼동 될 수 있습니다에 적용 되지 않습니다. 그리고 실제로 다양 한 프로그래밍 질문은 실제로 C#을 사용 하 여 작업 또는 ASP.NET을 사용 하 여 작업에 대 한 합니다. 따라서 Razor에 대 한 정보에 대 한 구체적으로 살펴보면 찾을 수 없는 답변 합니다.


## <a name="adding-some-conditional-logic"></a>일부 조건부 논리 추가

페이지의 코드를 사용 하는 방법에 대 한 유용한 기능 중 하나입니다는 다양 한 조건에 따라 발생 변경할 수 있습니다. 자습서의이 부분에서는 페이지에 표시 되는 항목을 변경 하는 몇 가지 이리저리 됩니다.

이 예제에서는 간편 하 고 다소에서는 조건부 논리에 집중할 수 있도록 거리가 됩니다. 만들어야 하는 페이지는이 수행 합니다.

- 처음으로 인지에 따라 페이지 표시 됩니다. 또는 페이지 전송 단추를 클릭 하면 여부 페이지의 다양 한 텍스트를 표시 합니다. 첫 번째 조건부 테스트 사용 됩니다.
- URL (http://...?show=true)의 쿼리 문자열에 특정 값이 전달 하는 경우에 메시지를 표시 합니다. 두 번째 조건부 테스트 사용 됩니다.

WebMatrix에서 페이지를 만들고 이름을 *TestRazorPart2.cshtml*합니다. (리본 메뉴에서 클릭 **새로 만들기**, 선택 **CSHTML**에서 파일 이름을 지정 하 고 클릭 **확인**.)

해당 페이지의 내용을 다음으로 바꿉니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

맨 위에 있는 코드 블록에는 일부 텍스트를 사용 하 여 message 라는 변수를 초기화 합니다. 페이지의 본문에서 message 변수의 내용 안에 표시 됩니다는 &lt;p&gt; 요소입니다. 태그도 포함 되어 있습니다는 &lt;입력&gt; 만들려는 요소를 **제출** 단추입니다.

지금 작동 하는지는 어떻게 확인 페이지를 실행 합니다. 지금은는 기본적으로 정적 페이지를 클릭 하는 경우에 합니다 **제출** 단추입니다.

WebMatrix로 돌아갑니다. 코드 블록을 다음 강조 표시 된 코드를 추가 *후* 메시지를 초기화 하는 줄:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>If {} 블록

If가 방금 추가한 새로운 조건입니다. 코드에는 조건이 다음과 같은 구조가 경우:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

괄호 안에 테스트할 조건이입니다. 이 값 또는 true 또는 false를 반환 하는 식 이어야 합니다. 조건이 true 인 경우 ASP.NET에는 중괄호 내에 있는 문은 실행 됩니다. (되는 *한 다음* 의 일부로 *면* 논리.) 조건이 false 인 경우에 코드 블록은 생략 됩니다.

다음은 몇 가지 조건 if에서 테스트할 수 있습니다 문:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

식 또는 값에 대 한 변수를 사용 하 여 테스트할 수 있습니다는 <em>논리 연산자</em> 또는 <em>비교 연산자</em>: 같음 (= =), 보다 큼 (&gt;), 보다 작은 (&lt;), 보다 크거나 같음 (&gt;=), 보다 작거나 같음 (&lt;=) 합니다. ! 같지 않음 연산자 의미 =-예를 들어 경우 (을! = 0) 의미 <em>경우</em> <em>는</em><em>0과 같지 않은</em>합니다.

> [!NOTE]
> 같음 (= =)에 대 한 비교 연산자가 동일 하 게 =을 확인 해야 합니다. = 연산자에만 값을 할당 하는 (var을 = 2). 이러한 연산자를 혼합 하면 오류가 얻게 또는 이상한 결과 받게 됩니다.


항목 인지를 테스트 하려면 전체 구문은 if(IsDone == true) 합니다. 하지만 바로 가기 if(IsDone) 이용할 수 있습니다. 비교 연산자 인 경우 ASP.NET true에 대해 테스트 하는 것을 가정 합니다.

합니다. 자체적으로 연산자는 논리 NOT을 의미합니다. 예를 들어, 조건이 if (! IsPost) 의미 *IsPost true가 아니면*합니다.

논리적 AND를 사용 하 여 조건을 결합할 수 있습니다 (&amp; &amp; 연산자) 또는 논리적 OR (| | 연산자). 이전 예제에서에서 경우 마지막 조건 예를 들어 *AND 표시 메시지를 true를 false로 설정 되어 FileProcessingIsDone 설정 되지 않은 경우*합니다.

### <a name="the-else-block"></a>Else 블록

에 대 한 마지막 블록:는 경우 블록 else 블록 올 수 있습니다. Else 블록 유용 조건이 false 인 경우 다른 코드를 실행 해야 합니다. 간단한 예는 다음과 같습니다.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

Else 블록을 사용 하 여 유용이 시리즈의 뒷부분에 나오는 자습서에서 몇 가지 예에 표시 됩니다.

### <a name="testing-whether-the-request-is-a-submit-post"></a>요청을 제출 (post) 인지를 테스트 합니다.

다시 돌아가겠습니다 조건 if(IsPost) {...}에 있는 예제에서는 있지만 더 많은입니다. IsPost에는 실제로 현재 페이지의 속성입니다. 처음으로 페이지를 요청 하 고, IsPost false를 반환 합니다. 그러나 단추를 클릭 하거나 그렇지 않으면 페이지를 전송 하는 경우-게시할-IsPost true를 반환 합니다. 따라서 IsPost 폼 제출을 처리 하는 여부를 확인할 수 있습니다. (HTTP 동사를 기준으로 요청은 GET 작업이 IsPost false를 반환 합니다. 요청은 POST 작업, IsPost true를 반환 합니다.) 자습서의 뒷부분에서이 테스트에 특히 유용 되는 입력된 된 폼을 작업할 수 있습니다.

페이지를 실행 합니다. 요청 하는 처음 이기 때문에 "This is 처음 페이지를 요청 했습니다"을 참조 페이지입니다. 문자열 메시지 변수를 초기화 하는 값입니다. 있지만 if(IsPost) 테스트를 반환 하는 지금은 false 경우 내 코드를 차단 하므로 실행 되지 않습니다.

클릭 합니다 **제출** 단추입니다. 페이지를 다시 요청 합니다. 로 "This is 처음..."를 이전에 메시지 변수가 설정 됩니다. 하지만이 이번에 if 내에서 코드 실행을 차단 하므로 테스트 if(IsPost) true를 반환 합니다. 코드 태그에서 렌더링할 대상을 다른 값으로 message 변수의 값을 변경 합니다.

이제 if 추가 태그에는 조건입니다. 아래는 &lt;p&gt; 포함 하는 요소는 **제출** 단추, 다음 태그를 추가 합니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

시작 하려면 있다면 태그 내에 코드를 추가 하는 @합니다. 경우에는 테스트와 유사한 이전에서 추가한 코드 블록입니다. 중괄호 안의 추가 하는 일반 HTML-적어도 것이 일반적인 아래에 도달할 때까지 @DateTime.Now입니다. Razor 코드의 약간 다른 이기 다시 해야 앞에 추가 합니다.

요점은 맨 위에 있는 및 태그에 조건을 둘 다에서 코드를 차단 하는 경우 추가할 수 있습니다. If를 사용 하는 경우 태그 또는 코드 블록 내에서 줄 페이지의 본문에는 조건이 될 수 있습니다. 이 경우 게 분명히 ASP.NET 코드의 위치를 사용 하 여 해야 할 경우 true 태그 및 코드를 혼합 하 여 언제 든 지 합니다.

페이지를 실행 하 고 클릭 **제출**합니다. 이 시간 뿐만 아니라 다른 메시지가 표시 ("이제 사용자가 제출한...")을 제출 하지만 날짜 및 시간을 나열 하는 새 메시지를 표시 합니다.

![제출 후를 보여 주는 타임 스탬프를 사용 하 여 브라우저에서 실행 되는 'Razor 2 test' 페이지](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>쿼리 문자열의 값을 테스트

하나 이상의 테스트 합니다. 이 이번에는 경우 추가 값을 테스트 하는 블록 라는 쿼리 문자열에 전달 될 수 있는 표시 합니다. (다음과 같은: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) 메시지 있습니다 했으므로 된 표시 되도록 페이지를 변경할 수 있습니다 ("This is 처음..." 등)은 표시의 값이 true만 표시 됩니다.

아래쪽 (하지만 내부)에서 페이지의 맨 위에 있는 코드 블록은 다음 추가 합니다.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

다음 예제와 같이 전체 코드 블록 이제 확인 합니다. (기억 페이지에 코드를 복사할 때 들여쓰기를 다르게 보일 수 있습니다. 하지만 코드를 실행 하는 방법에 영향을 주지는.)

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

새 코드 블록에서 false로 showMessage 라는 변수를 초기화 합니다. 그런 다음 if 수행 쿼리 문자열의 값을 테스트 합니다. 페이지를 처음 요청할 때 다음과 같은 URL에 있습니다.

`http://localhost:43097/TestRazorPart2.cshtml`

코드는 URL 쿼리 문자열을 URL의이 버전 처럼 표시 라는 변수에 포함 되는지 여부를 결정 합니다.

`http://localhost:43097/TestRazorPart2.cshtml`?show=true

자체 테스트 요청 개체의 QueryString 속성에 살펴봅니다. 쿼리 문자열이 포함 되 면 명명 된 항목을 표시 하 고 해당 항목의 경우 true로 설정 된 경우 블록 실행 및 매개 변수를 true로 설정 합니다.

알 수 있듯이 여기서 트릭을 있습니다. 이름이 의미 하는, 같은 쿼리 문자열은 문자열입니다. 그러나 테스트할 수 있습니다만 true 및 false 테스트 하는 값이 부울 (true/false) 값입니다. 쿼리 문자열에서 표시 변수 값을 테스트할 수 있습니다, 전에 부울 값으로 변환 해야 합니다. AsBool 메서드가 수행 하는 하는-입력 문자열을 사용 하 고 부울 값으로 변환 합니다. 물론 문자열 "true" 이면 AsBool 메서드를 true로 해당 값을 변환 합니다. 문자열의 값이 다른 작업 인 경우 AsBool false를 반환 합니다.

> [!TIP] 
> 
> **데이터 형식 및 as () 메서드**
> 
> 만 말한 지금 변수를 만들 때 사용 하는 키워드 차이 없는 전체 스토리를 통해입니다. 값을 조작 하기 위해-숫자를 추가 또는 연결 문자열, 날짜를 비교 하거나 true/false에 대 한 테스트-C#에서 값의 적절 한 내부 표현으로 사용 해야 합니다. C# 수 *일반적으로* 해야 해당 표현을 파악 (즉, 어떤 *형식* 데이터가) 값을 사용 하 여 수행 하는 기반입니다. 이제 합니다 그러나이 그렇게 할 수 없습니다. 그러지 않으면 C#은 데이터를 나타내는 방법을 명시적으로 지정 하 여 지원 해야 합니다. AsBool 메서드는-"true" 또는 "false"의 문자열 값을 부울 값으로 처리 해야 함을 C# 지시 합니다. 이와 유사한 메서드 AsInt (정수로 처리), AsDateTime (날짜/시간으로 처리), AsFloat (부동 소수점 숫자로 처리) 등도 다른 형식으로 문자열을 나타내기 위해 존재 합니다. 를 사용 하면 () 메서드로 이러한 C# 나타낼 수 없는 문자열 값을 요청 하는 경우 오류가 표시 됩니다.


페이지의 태그를 제거 하거나이 요소에 주석 (여기 그림 주석):

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

제거 되었거나 해당 텍스트를 주석으로 처리 하는 오른쪽 다음 추가 합니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

테스트 라는 매개 변수가 true 인 경우 렌더링 하는 경우는 &lt;p&gt; message 변수의 값을 가진 요소가 있습니다.

### <a name="summary-of-your-conditional-logic"></a>조건부 논리의 요약

어떤 방금 수행한의 완전히 잘 모를 경우 요약은 다음과 같습니다.

- 메시지 변수는 기본 문자열로 초기화 됩니다 ("This is 처음...").
- "..."제출한 이제 메시지의 값으로 변경 된 페이지 요청을 제출 (post)의 결과 하는 경우
- 매개 변수는 false로 초기화 됩니다.
- 쿼리 문자열이 포함 되 면? 표시 = true 매개 변수가 설정 된 true로 합니다.
- 태그에서 showMessage 참인 경우에 &lt;p&gt; 메시지의 값을 보여 주는 요소가 렌더링 됩니다. (ShowMessage false 이면 아무 것도 렌더링 됩니다 이때 태그.)
- 태그에서 요청을 post 하는 경우는 &lt;p&gt; 날짜 및 시간을 표시 하는 요소가 렌더링 됩니다.

페이지를 실행 합니다. 태그에 if(showMessage) 테스트가 false를 반환 하므로 showMessage false 이므로 메시지 없음, 있습니다.

**제출**을 클릭합니다. 날짜 및 시간만 메시지가 계속 표시 됩니다.

브라우저에서 URL 상자로 이동 하 고 다음 URL의 끝에 추가:? 표시 = true 및 다음 Enter를 누릅니다.

![쿼리 문자열을 표시 하는 브라우저에서 '테스트 Razor 2' 페이지](intro-to-web-pages-programming/_static/image5.png)

페이지가 다시 표시 됩니다. (URL을 변경 했기 때문이 새 요청을 전송 하지 않습니다.) 클릭 **제출** 다시 합니다. 날짜 및 시간을 그대로 메시지가 다시 표시 됩니다.

![쿼리 문자열이 있으면 'Razor 2 test' 페이지 후 제출](intro-to-web-pages-programming/_static/image6.png)

URL에서 변경? 표시 = true? 표시 = false 및 Enter 키를 누릅니다. 페이지를 다시 전송 합니다. 페이지를 다시 시작 하는 방법-메시지가 없습니다.

앞에서 설명한 대로이 예제의 논리를 작은 거리가 됩니다. 그러나 다양 한 페이지에 표시 하려는 경우, 하며 지금까지 살펴본 형식 중 하나 이상의 여기 있습니다.

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>설치 도우미 (Gravatar 이미지를 표시 합니다.)

일부 작업을 사용자 웹 페이지에서 작업을 수행 하려는 경우가 많습니다 많은 코드가 필요 하거나 추가 정보가 필요 합니다. 예: 데이터에 대 한 차트를 표시합니다. 페이지에 Facebook "좋아요" 단추를 배치 합니다. 웹 사이트에서 보내는 전자 메일 자르기 또는 이미지 크기 조정 PayPal을 사용 하 여 사이트에 대 한 합니다. 이러한 유형의 작업을 위해 쉽게 ASP.NET 웹 페이지를 사용 하면 *도우미*합니다. 도우미는 사이트에 설치 하 고 Razor 코드의 몇 줄을 사용 하 여 일반적인 작업을 수행할 수 있는 구성 요소입니다.

ASP.NET 웹 페이지에 기본 제공 하는 몇 가지 도우미 그러나 많은 도우미 NuGet 패키지 관리자를 사용 하 여 제공 되는 패키지 (추가 기능)에서 사용할 수 있습니다. NuGet 패키지 설치를 선택 하면 및 설치의 모든 세부 정보 처리 합니다.

자습서의이 부분에서는 ("전역적으로 인식된 아바타") Gravatar 이미지를 표시할 수 있는 도우미를 설치 합니다. 두 가지를 알아봅니다. 하나는 찾아서 도우미를 설치 하는 방법입니다. 어떻게 도우미 쉽게 직접 작성 해야 하는 코드를 많이 사용 하 여 작업을 수행 해야 그렇지 않은 경우 작업을 수행할 수도 알아봅니다.

사용자 고유의 Gravatar Gravatar 웹 사이트에서 등록할 수 있습니다 [ http://www.gravatar.com/ ](http://www.gravatar.com/), 자습서의이 부분을 수행 하려면 Gravatar 계정을 만들려면 필수 이지만 합니다.

WebMatrix에서를 클릭 합니다 **NuGet** 단추입니다.

![WebMatrix에서 NuGet 갤러리 대화 상자](intro-to-web-pages-programming/_static/image7.png)

이 NuGet 패키지 관리자를 시작 하 고 사용 가능한 패키지를 표시 합니다. (패키지의 일부 도우미는 일부 추가 기능 자체 WebMatrix에 일부 템플릿은 추가 등에입니다.) 버전 비 호환성에 대 한 오류 메시지가 표시 될 수 있습니다. 클릭 하 여이 오류 메시지를 무시할 수 있습니다 **확인** 이 자습서를 진행 합니다.

![WebMatrix에서 NuGet 갤러리 대화 상자](intro-to-web-pages-programming/_static/image8.png)

검색 상자에서 "asp.net 도우미"를 입력 합니다. NuGet에는 검색 조건과 일치 하는 패키지를 보여 줍니다.

![패키지를 표시 하는 WebMatrix의 NuGet 갤러리](intro-to-web-pages-programming/_static/image9.png)

ASP.NET Web Helpers Library Gravatar 이미지 사용을 비롯 한 많은 일반 태스크를 단순화 하는 코드가 포함 되어 있습니다. 선택 된 **ASP.NET Web Helpers Library** 패키징하고 클릭 **설치** 설치 관리자를 시작 하려면. 선택 **예** 패키지를 설치 하 고 설치를 완료 하려면 동의 하려는 경우 메시지가 표시 되 면 합니다.

이제 NuGet 다운로드 하 고 필요할 수도 있는 추가 구성 요소를 포함 하 여 모든 설치 (*종속성*).

어떤 이유로 도우미를 제거 해야 하는 경우 프로세스 매우 비슷합니다. 클릭 합니다 **NuGet** 단추를 클릭 하는 **설치 된** 탭을 제거 하려는 패키지를 선택 합니다.

## <a name="using-a-helper-in-a-page"></a>도우미를 사용 하 여 페이지에서

이제 방금 설치한 도우미를 사용 합니다. 도우미 페이지를 추가 하기 위한 프로세스는 대부분의 도우미에 대 한 비슷합니다.

WebMatrix에서 페이지를 만들고 이름을 *GravatarTest.cshml*합니다. (도우미를 테스트 하려면 특수 페이지 만들 하지만 사이트에서 모든 페이지에 도우미를 사용할 수 있습니다.)

내 합니다 &lt;본문&gt; 요소를 추가 &lt;div&gt; 요소입니다. 내 합니다 &lt;div&gt; 요소인 입력:

@Gravatar.

@ 문자는 Razor 코드를 표시 하기 위해 사용 했던 동일한 문자입니다. **Gravatar** 는 사용 하는 도우미 개체입니다.

WebMatrix의 목록을 표시 마침표 (.)를 입력 하는 즉시 *메서드* Gravatar 도우미 사용 가능 (함수):

![Gravatar 도우미 IntelliSense 드롭다운 목록](intro-to-web-pages-programming/_static/image10.png)

이 기능 이라고 *IntelliSense*합니다. 상황에 맞는 적절 한 선택 항목을 제공 하 여 코드를 수 있습니다. IntelliSense는 HTML, CSS, ASP.NET 코드, JavaScript 및 WebMatrix에서 지원 되는 다른 언어를 사용 하 여 작동 합니다. 쉽게 WebMatrix에서 웹 페이지를 개발할 수 있도록 하는 다른 기능입니다.

G 키 키보드에서 IntelliSense GetHtml 메서드를 찾습니다는 참조 하세요. Tab 키를 누릅니다. IntelliSense는 선택한 메서드 (GetHtml)를 삽입합니다. 여는 괄호를 입력 하 고 닫는 괄호를 자동으로 추가 되어 있는지 확인 합니다. 따옴표 두 괄호 사이에서 전자 메일 주소를 입력 합니다. Gravatar 계정이 있는 경우 자신의 프로필 사진을 반환 됩니다. Gravatar 계정이 없는 경우 기본 이미지가 반환 됩니다. 완료 되 면 줄은 다음과 같습니다.

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

이제 브라우저에서 페이지를 봅니다. Gravatar 계정이 있는지 여부에 따라 기본 이미지 또는 사진을 표시 됩니다.

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![기본 이미지](intro-to-web-pages-programming/_static/image12.png)

수행 하는 도우미의는 아이디어를 얻고, 브라우저에서 페이지의 소스를 봅니다. 페이지에 있던 HTML과 함께 식별자를 포함 하는 이미지 요소를 표시 합니다. 이 위치에 추가 해야 하는 페이지에 렌더링 된 도우미는 코드는 @Gravatar.GetHtml합니다. 도우미 정보를 제공 하 고 제공 된 계정에 대 한 올바른 이미지를 다시 얻기 위해 Gravatar 직접 통신 하는 코드를 생성 했습니다.

또한 GetHtml 메서드를 사용 하면 다른 매개 변수를 제공 하 여 이미지를 사용자 지정할 수 있습니다. 다음 코드는 너비와 높이가 40 픽셀의 이미지를 요청 하 라는 지정 된 기본 이미지를 사용 하는 방법을 보여 줍니다 **wavatar** 지정한 계정이 없는 경우.

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

이 코드 (기본 이미지 다릅니다 임의로) 다음 결과 같은 항목을 생성 합니다.

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>다음에 나오는

을 유지 하기 위해이 자습서 짧은 몇 가지 기본 사항에 집중 했습니다. 물론 방법이 *많은* Razor 및 C#에 있습니다. 이 자습서를 진행 하면 더 자세히 알아봅니다. 지금 바로 Razor 및 C#의 프로그래밍 측면을 자세히 알고 싶은 경우 여기에 보다 정확 하 게 소개를 읽을 수 있습니다: [로 ASP.NET 웹 프로그래밍 Razor 구문 소개](https://go.microsoft.com/fwlink/?LinkID=202890)합니다.

다음 자습서는 데이터베이스를 사용 하 여 작업을 소개 합니다. 해당 자습서에서 즐겨 찾는 영화를 표시할 수 있도록 샘플 응용 프로그램을 만드는 먼저 합니다.

## <a name="complete-listing-for-testrazor-page"></a>TestRazor 페이지에 대 한 전체 목록

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>TestRazorPart2 페이지에 대 한 전체 목록

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>GravatarTest 페이지에 대 한 전체 목록

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Twitter 도우미](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [이전](getting-started.md)
> [다음](displaying-data.md)
