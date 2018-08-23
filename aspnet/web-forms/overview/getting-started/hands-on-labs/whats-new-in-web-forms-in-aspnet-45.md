---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5의에서 Forms 웹의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 새 버전의 ASP.NET Web Forms 다양 한 데이터로 작업 하는 경우 사용자 환경 개선에 집중 하는 향상 된 기능을 소개 합니다. 이전 버전의...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 54e0234d6f13ce62803dbe55a836414a93a207b2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828821"
---
<a name="whats-new-in-web-forms-in-aspnet-45"></a>Asp.net 4.5 Web Forms의 새로운 기능
====================
[웹 캠프 팀](https://twitter.com/webcamps)

> 새 버전의 ASP.NET Web Forms 다양 한 데이터로 작업 하는 경우 사용자 환경 개선에 집중 하는 향상 된 기능을 소개 합니다.
> 
> Web Forms, 데이터 바인딩 사용 하 여 개체 멤버의 값을 내보낼 때의 이전 버전에서는 bind () 또는 eval () 데이터 바인딩 식을 사용 했습니다. 새 버전의 ASP.NET에서 수 있다면 어떤 형식의 데이터 컨트롤을 새 ItemType 속성을 사용 하 여 바인딩할 것을 선언 합니다. 이 속성을 설정 하면 강력한 형식의 변수를 사용 하 여 IntelliSense, 멤버 탐색 및 컴파일 타임 검사와 같은 Visual Studio 개발 환경의 전체 혜택을 받을 수 있습니다.
> 
> 데이터 바인딩된 컨트롤을 사용 하 여 이제 지정할 수 있습니다도 선택, 업데이트, 삭제 및 데이터를 삽입에 대 한 사용자 고유의 사용자 지정 메서드 페이지 컨트롤 및 응용 프로그램 논리 간의 상호 작용을 단순화 합니다. 또한 메서드 형식 매개 변수로 직접 페이지에서 데이터를 매핑할 수 있습니다 즉 asp.net 모델 바인딩 기능이 추가 되었습니다.
> 
> 사용자 입력 유효성 검사 Web Forms의 최신 버전을 사용 하 여 더 쉬울 수도 해야 합니다. 유효성 검사 특성을 사용 하 여 모델 클래스를 이제 주석을 달 수 있습니다 합니다 **System.ComponentModel.DataAnnotations** 네임 스페이스 및 모든 사이트를 제어 하는 요청 사용자 정보를 사용 하 여 입력의 유효성을 검사 합니다. Web Forms에서 클라이언트 쪽 유효성 검사는 jQuery, 수행 되는 클리너 클라이언트 쪽 코드 및 비 가시적인 JavaScript 기능을 제공 통합 되었습니다.
> 
> 요청 유효성 검사 영역에서 향상 된 기능을 선택적으로 응용 프로그램의 특정 부분에 대 한 요청 유효성 검사를 해제 하거나 무효화 요청 데이터를 읽을 수 있도록 이루어졌습니다.
> 
> 몇 가지 개선이 이루어졌습니다 Web forms 서버 컨트롤 HTML5의 새로운 기능을 활용 하려면:
> 
> - TextBox 컨트롤의 텍스트 모드 속성은 전자 메일, datetime 등 새 HTML5 입력된 형식을 지원 하도록 업데이트 되었습니다.
> - 이제 FileUpload 컨트롤이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드를 지원 합니다.
> - 유효성 검사기는 이제 지원 유효성 검사 HTML5 입력된 요소를 제어합니다.
> - 이제 URL을 나타내는 특성이 있는 새 HTML5 요소 지원 runat =&quot;server&quot;합니다. 결과적으로 같은 사용할 수 있습니다 ASP.NET 규칙 URL 경로에 ~를 나타내는 응용 프로그램 루트 연산자 (예를 들어 &lt;비디오 runat =&quot;server&quot; src =&quot;~/myVideo.wmv&quot; &gt; &lt;비디오/&gt;).
> - UpdatePanel 컨트롤 게시 HTML5 입력된 필드를 지원 하도록 수정 되었습니다.
> 
> 공식 ASP.NET 포털에서 ASP.NET WebForms 4.5의 새로운 기능의 더 많은 예제를 찾을 수 있습니다: [ASP.NET 4.5와 Visual Studio 2012의 새로운 기능](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)
> 
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.


<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 강력한 데이터 바인딩 식을 사용 하 여
- Web Forms에서 새 모델 바인딩 기능을 사용 합니다.
- 값 공급자를 사용 하 여 코드 숨김 방법 페이지 데이터를 매핑하기 위한
- 사용자 입력된 유효성 검사에 대 한 데이터 주석 사용
- Web Forms에서 advange jQuery 사용한 unobstrusive 클라이언트 쪽 유효성 검사의 수행
- 세분화 된 요청 유효성 검사 구현
- Web Forms에서 처리 하는 비동기 페이지를 구현 합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 코드 조각**

편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다. 설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 c:를 사용 하 여 코드 조각](#AppendixC)&quot;합니다.

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [연습 1: 모델 ASP.NET Web Forms에서 바인딩](#Exercise1)
2. [연습 2: 데이터 유효성 검사](#Exercise2)
3. [연습 3: 비동기 페이지 처리에 ASP.NET Web Forms](#Exercise3)

> [!NOTE]
> 각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다. 이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


이 랩을 완료 하기 위한 예상 시간: **60 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>연습 1: 모델 ASP.NET Web Forms에서 바인딩

ASP.NET Web Forms의 새 버전의 데이터로 작업할 때 환경 개선에 집중 하는 기능이 도입 되었습니다. 이 연습에서는 전체에서 강력한 형식의 데이터 컨트롤에 알아봅니다을 모델 바인딩.

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>작업 1-강력한 형식의 데이터 바인딩을 사용 하 여

이 태스크에서는 ASP.NET 4.5에서 사용할 수 있는 새 강력한 형식의 바인딩 알게 됩니다.

1. 엽니다는 **시작할** 솔루션에 있는 **소스/e x 1-ModelBinding/시작/** 폴더.

   1. 일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 엽니다는 **Customers.aspx** 페이지입니다. 주 컨트롤에는 번호가 없는 목록을 배치 하 고 각 고객을 나열 하기 위한 내부 repeater 컨트롤을 포함 합니다. 반복기 이름으로 설정할 **customersRepeater** 다음 코드와 같이 합니다.

    Web Forms의 이전 버전의 경우 데이터 바인딩 개체에 대 한 멤버의 값을 내보낼 데이터 바인딩을 사용 하는 경우에 사용할는 Eval 메서드를 호출 하는 데이터 바인딩 식 전달 멤버의 이름을 문자열로 합니다.

    런타임 시 이러한 호출 Eval 현재 바인딩된 개체에 대해 리플렉션을 사용 하 여 지정 된 이름의 멤버의 값을 읽을 수를 HTML의 결과 표시 합니다. 이 방법은 매우 쉽게 unshaped 임의의 데이터에 대 한 데이터 바인딩.

    그러나 다양 한 지원 (예: 정의로 이동), 탐색 및 컴파일 타임 검사, 멤버 이름에 대 한 IntelliSense를 비롯 한 Visual Studio에서 개발 타임 환경을 개선 기능 손실 됩니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. 엽니다는 **Customers.aspx.cs** 파일입니다.
4. 다음 추가 문을 사용 하 여 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. 에 **페이지\_부하** 메서드를 고객의 목록 사용 하 여 반복기를 채우는 코드를 추가 합니다.

    (코드 조각- *Forms 랩-Ex01-고객은 데이터 원본 바인드 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    솔루션은 codefirst의 경우 함께 EntityFramework를 사용 하 여 만들고 데이터베이스에 액세스 합니다. 다음 코드에서는 customersRepeater 데이터베이스에서 모든 고객을 반환 하는 구체화 된 쿼리에 바인딩되어 있습니다.
6. 키를 눌러 **F5** 솔루션을 실행 하 고 이동 하는 **고객** 페이지를 실행 중인 repeater를 참조 하세요. 솔루션에는 codefirst의 경우 사용 하는, 데이터베이스를 생성 하 고 응용 프로그램을 실행 하는 경우에 로컬 SQL Express 인스턴스에서 채워집니다 됩니다.

    ![Repeater 사용 하 여 고객을 나열](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "repeater 사용 하 여 고객 목록")

    *Repeater 사용 하 여 고객 목록*

    > [!NOTE]
    > Visual Studio 2012의 IIS Express는 기본 웹 개발 서버입니다.
7. 브라우저를 닫고 Visual Studio로 다시 이동 합니다.
8. 이제 강력한 형식의 바인딩을 사용 하는 구현을 대체 합니다. 엽니다는 **Customers.aspx** 페이지를 사용 하 여 새 **ItemType** 특성을 설정 하는 반복기에는 **고객** 바인딩 형식으로 형식.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    ItemType 속성을 사용 하면 어떤 유형의 데이터 컨트롤에 바인딩할 수 및 사용 하면 강력한 형식의 데이터 바인딩된 컨트롤 내에서 바인딩 선언에 있습니다.
9. ItemTemplate 콘텐츠를 다음 코드로 대체 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    위의 방법으로 단점 중 하나는 eval () 및 bind ()에 대 한 호출 바인딩된-속성 이름을 나타내는 문자열을 전달 하면 의미 합니다. 즉, 멤버 이름, (예: 정의로 이동), 코드 탐색에 대 한 지원 하거나 컴파일 타임 검사 지원에 대 한 Intellisense를 활용할 수 없습니다.

    ItemType 속성을 설정 하면 데이터 바인딩 식의 범위에 생성 될 새 형식화 된 변수를 두 개: **항목** 하 고 **binditem을**입니다. 데이터 바인딩 식에서 이러한 강력한 형식의 변수를 사용할 수 있으며 Visual Studio 개발 환경의 모든 혜택을 얻을 수 있습니다.

    &quot; **:** &quot; 식에 사용 됩니다 자동으로 HTML 인코딩 보안 문제 (예: 사이트 간 스크립팅 공격)를 방지 하려면 출력 합니다. 이 표기법 사용 가능한.NET 4 이후를 작성 하는 응답에 대 한 되었지만 이제도 데이터 바인딩 식에서 사용할 수 있습니다.

    > [!NOTE]
    > 단방향 바인딩 항목 멤버를 사용할 수 있습니다. 양방향 바인딩을 사용 하 여 수행 하려는 경우는 **binditem을** 멤버입니다.

    ![강력한 형식의 바인딩에 IntelliSense 지원을](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "바인딩에 강력한 IntelliSense 지원")

    *강력한 형식의 바인딩에 IntelliSense 지원*
10. 키를 눌러 **F5** 솔루션을 실행 하 여 변경 내용이 예상 대로 작동 하는지 확인 하려면 고객 페이지로 이동 합니다.

    ![고객 세부 정보를 나열](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "고객 세부 정보를 나열 합니다.")

    *고객 세부 정보를 나열합니다.*
11. 브라우저를 닫고 Visual Studio로 다시 이동 합니다.

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>작업 2-Web Forms에서 바인딩 소개 모델

ASP.NET Web Forms의 이전 버전을 모두 검색 하 고 데이터 업데이트, 양방향 데이터 바인딩을 수행 하려는 경우 데이터 원본 개체를 사용 하려면 필요 합니다. 이 수 개체 데이터 소스, SQL 데이터 원본, LINQ 데이터 소스 등입니다. 그러나 시나리오에 데이터를 처리 하는 것에 대 한 사용자 지정 코드를 필요한 경우 개체 데이터 소스를 사용 하는 데 필요한 만들었다가이 몇 가지 단점이 있습니다. 예를 들어, 한 복합 형식을 방지 하는 데 필요한 및 유효성 검사 논리를 실행 하는 경우 예외를 처리 하는 데 필요한 합니다.

데이터 바인딩된 컨트롤을 새 버전의 ASP.NET Web Forms에서 모델 바인딩을 지원합니다. 이 수 선택 지정, 업데이트, 추가 및 삭제 논리를 호출 하 여 코드 숨김 파일에서 또는 다른 클래스에서 데이터 바인딩된 컨트롤에서 직접 메서드를 의미 합니다.

이 알아보려면 사용할지 GridView를 사용 하 여 새 제품 범주를 나열 하려면 **SelectMethod** 특성입니다. 이 특성을 사용 하면 GridView 데이터를 검색 하는 메서드를 지정할 수 있습니다.

1. 엽니다는 **Products.aspx** 페이지 및 포함을 **GridView**. 아래와 같이 강력한 형식의 바인딩을 사용 하 여 정렬 및 페이징을 활성화 GridView를 구성 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. 새 **SelectMethod** 를 호출 하는 GridView를 구성 하는 특성을 **GetCategories** 데이터를 선택 하는 방법입니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. 엽니다는 **Products.aspx.cs** 코드 숨김 파일을 추가한 다음 문을 사용 하 여 합니다.

    (코드 조각- *Forms 랩-Ex01-네임 스페이스 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. private 멤버를 추가 합니다 **제품** 클래스의 새 인스턴스를 할당 하 고 **ProductsContext**합니다. 이 속성은 데이터베이스에 연결할 수 있는 Entity Framework 데이터 컨텍스트를 저장 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. 만들기는 **GetCategories** LINQ를 사용 하 여 범주 목록을 검색 하는 방법입니다. 이 쿼리에 포함 되도록 합니다 **제품** 속성 GridView에는 각 범주에 대 한 제품의 양을 표시 될 수 있습니다. 메서드가 반환 되도록 쿼리를 나타내는 원시 IQueryable 개체 실행 페이지 수명 주기 나중에 확인할 수 있습니다.

    (코드 조각- *Forms-Ex01-랩 GetCategories 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > ASP.NET Web Forms의 이전 버전에서는 사용 하도록 설정 하면 정렬 및 페이징, 데이터 원본 개체 컨텍스트 내에서 사용자 고유의 리포지토리 논리를 사용 하 여 하는 데 필요한 사용자 지정 코드를 작성 하 고 필요한 모든 매개 변수를 수신 합니다. 데이터 바인딩 메서드는 IQueryable을 반환할 수 있습니다 하 고 쿼리를 나타냅니다이 이제 실행을 계속 ASP.NET 적절 한 정렬을 추가 하려면 쿼리 및 페이징 매개 변수를 수정 하는 처리할 수 있습니다.
6. 키를 눌러 **F5** 사이트 디버깅을 시작 하 여 제품 페이지로 이동 합니다. GridView GetCategories 메서드에서 반환 되는 범주를 사용 하 여 채워져 있는지 표시 됩니다.

    ![모델 바인딩을 사용 하 여 GridView를 채우기를](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "모델 바인딩을 사용 하 여 GridView를 채우기를")

    *모델 바인딩을 사용 하 여 GridView를 채우기를*
7. 키를 눌러 **SHIFT**+**F5** 디버깅을 중지 합니다.

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>작업 3-모델 바인딩에 대 한 값 공급자

모델 바인딩 데이터 바인딩된 컨트롤에서 직접 데이터를 사용 하려면 사용자 지정 메서드를 지정할 수 뿐만 아니라 데이터 페이지에서 이러한 메서드에서 매개 변수를 매핑할 수 있습니다. 메서드 매개 변수에 값의 데이터 원본을 지정 하려면 값 공급자 특성을 사용할 수 있습니다. 예를 들어:

- 페이지의 컨트롤
- 쿼리 문자열 값
- 데이터 보기
- 세션 상태
- 쿠키
- 게시 된 양식 데이터
- 뷰 상태
- 사용자 지정 값 공급자도 지원 됩니다.

ASP.NET MVC 4를 사용한 모델 바인딩 지원은 유사한 것을 확인할 수 있습니다. 실제로 이러한 기능은 ASP.NET MVC에서 수행 되었으며로 이동 합니다 **System.Web** 어셈블리 에서도 Web Forms에서 사용할 수 있습니다.

이 태스크에서는 모델 바인딩을 사용 하 여 filter 매개 변수를 받는 각 범주에 대 한 제품의 양에 따라 결과 필터링 할 GridView 업데이트할는 있습니다.

1. 로 다시 이동 합니다 **Products.aspx** 페이지입니다.
2. GridView의 맨 위에 추가 **레이블을** 및 **ComboBox** 아래와 같이 각 범주에 대 한 제품의 수를 선택 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. 추가 된 **있도록 EmptyDataTemplate** 경우 선택한 제품 수를 사용 하 여 범주 없음 메시지를 표시 하려면 GridView에 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. 엽니다는 **Products.aspx.cs** 코드 숨김 및 다음을 추가 합니다 문을 사용 하 여 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. 수정 합니다 **GetCategories** 정수를 수신 하는 방법 **minProductsCount** 인수 및 반환된 된 결과 필터링 합니다. 이 위해 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *Forms-Ex01-랩 GetCategories 2 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    새 **[컨트롤]** 특성을 **minProductsCount** 인수 ASP.NET 페이지에서 컨트롤을 사용 하 여 해당 값을 채워야 알 수 있습니다. ASP.NET은 인수 (minProductsCount)의 이름과 일치 하는 모든 컨트롤에 대 한 확인 하 고 변환 컨트롤 값을 사용 하 여 매개 변수를 입력 하 고 필요한 매핑을 수행 합니다.

    또는 특성 값을 가져올 수 있는 위치에서 제어를 지정할 수 있는 오버 로드 된 생성자를 제공 합니다.

    > [!NOTE]
    > 데이터 바인딩 기능에의 한 가지 목표 페이지 상호 작용을 위해 작성 해야 하는 코드의 양을 줄이는 것입니다. [컨트롤] 값 공급자 외에도 메서드 매개 변수에서 다른 모델 바인딩 공급자를 사용할 수 있습니다. 그 중 일부는 작업 도입에 나열 됩니다.
6. 키를 눌러 **F5** 사이트 디버깅을 시작 하 여 제품 페이지로 이동 합니다. 드롭다운 목록에서 제품을 선택 하 고 GridView 이제 업데이트 되는 방식을 확인할 수 있습니다.

    ![필터링 드롭다운 목록에서 값을 사용 하 여 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "드롭다운 목록에서 값을 사용 하 여 GridView를 필터링 합니다.")

    *드롭다운 목록에서 값을 사용 하 여 GridView를 필터링합니다.*
7. 디버깅을 중지합니다.

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>작업 4-를 사용 하 여 모델을 필터링 하는 것에 대 한 바인딩

이 태스크에서는 선택한 범주에 포함 된 제품을 표시 하는 GridView 자식 보조를 추가 합니다.

1. 엽니다는 **Products.aspx** 페이지 및 범주 선택 단추를 자동으로 생성 하는 GridView를 업데이트 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. 두 번째 추가 **GridView** 라는 **productsGrid** 맨 아래에 있습니다. 설정 합니다 **ItemType** 하 **WebFormsLab.Model.Product**의 **DataKeyNames** 에 **ProductId** 및 **SelectMethod**  하 **GetProducts**합니다. 설정할 **AutoGenerateColumns** 하 **false** ProductId, ProductName, 설명 및 UnitPrice에 대 한 열을 추가 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. 엽니다는 **Products.aspx.cs** 코드 숨김 파일입니다. 구현 된 **GetProducts** GridView 범주에서 범주 ID를 받고 제품을 필터링 하는 메서드. 모델 바인딩에에서 선택한 행을 사용 하 여 매개 변수 값을 설정 합니다 **categoriesGrid**합니다. 인수 이름 및 컨트롤 이름을 일치 하지 않으면 이후 컨트롤 값 공급자에서 컨트롤의 이름을 지정 해야 합니다.

    (코드 조각- *Forms-Ex01-랩 GetProducts 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > 이 접근 방식을 쉽게 단위 이러한 메서드를 테스트 합니다. 여기서 Web Forms는 실행할 수 없습니다, 단위 테스트 컨텍스트를에서 [컨트롤] 특성은 특정 작업을 수행 하지 않습니다.
4. 엽니다는 **Products.aspx** 페이지 및 GridView 제품을 찾습니다. 선택한 제품을 편집 하는 것에 대 한 링크를 표시 하는 GridView 제품을 업데이트 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. 엽니다는 **ProductDetails.aspx** 바꾸고 코드 숨김 페이지의 **SelectProduct** 메서드를 다음 코드로 합니다.

    (코드 조각- *Forms-Ex01-랩 SelectProduct 메서드 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > 에 **[QueryString]** 특성은 쿼리 문자열에는 productId 매개 변수에서 메서드 매개 변수를 채우는 데 사용 됩니다.
6. 키를 눌러 **F5** 사이트 디버깅을 시작 하 여 제품 페이지로 이동 합니다. GridView 범주의 모든 범주를 선택 하 고 제품 GridView 업데이트 됩니다.

    ![선택한 범주에서 제품을 보여 주는](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "선택한 범주의 제품 표시")

    *선택한 범주의 제품 표시*
7. 클릭 합니다 **보기** ProductDetails.aspx 페이지를 열려면 제품에 대 한 링크입니다.

    쿼리 문자열에서 productId 매개 변수를 사용 하는 SelectMethod를 사용 하 여 제품 페이지를 검색 하는 것을 확인 합니다.

    ![제품 세부 정보를 보는](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "제품 세부 정보 보기")

    *제품 세부 정보 보기*

    > [!NOTE]
    > HTML에 대 한 설명을 입력할 수 있도록 다음 연습에서 구현 됩니다.

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>작업 5-를 사용 하 여 모델 업데이트 작업에 대 한 바인딩

이전 태스크에서 사용한 모델 바인딩을 주로 데이터를 선택 하면,이 작업에서 업데이트 작업에서 모델 바인딩을 사용 하는 방법을 배우게 됩니다.

사용자가 범주를 업데이트 하는 GridView 범주를 업데이트 합니다.

1. 엽니다는 **Products.aspx** 페이지 및 GridView 편집 단추를 자동으로 생성 하 여 새 범주를 업데이트 **UpdateMethod** 지정 하는 특성을 **UpdateCategory**선택한 항목을 업데이트 하는 방법입니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    GridView DataKeyNames 특성 모델 바인딩된 개체를 고유 하 게 식별 하는 멤버를 정의 하 고 update 메서드를 최소한으로 받아야 매개 변수는 따라서 키를 누릅니다.
2. 엽니다는 **Products.aspx.cs** 코드 숨김 파일 및 구현 합니다 **UpdateCategory** 메서드. 메서드는 현재 범주를 로드 하 고 GridView에서 값을 채우는 다음 범주를 업데이트할 범주 ID를 받게 됩니다.

    (코드 조각- *Forms-Ex01-랩 UpdateCategory 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    새 **tryupdatemodel에 전달** 페이지 클래스의 메서드는 컨트롤의 값을 사용 하 여 페이지에서 모델 개체를 채우는 담당 합니다. 이 경우 업데이트 된 값을 편집 하 고 현재 GridView 행에서 대체할 합니다 **범주** 개체입니다.

    > [!NOTE]
    > 다음 연습에서는 개체를 편집 하는 경우 사용자가 입력 데이터 유효성 검사에 대 한 ModelState.IsValid의 사용법을 설명 합니다.
3. 사이트를 실행 하 고 제품 페이지로 이동 합니다. 범주를 편집 합니다. 새 이름을 입력 하 고 클릭 **업데이트** 의 변경 사항을 유지 합니다.

    ![범주 편집](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "범주 편집")

    *범주 편집*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>연습 2: 데이터 유효성 검사

이 연습에서는 ASP.NET 4.5의 새로운 데이터 유효성 검사 기능에 배웁니다. Web Forms에서 새 비간섭 유효성 검사 기능을 사용해 확인 합니다. 사용자 입력된 유효성 검사를 위해 응용 프로그램 모델 클래스에서 데이터 주석을 사용 하 고 마지막으로, 요청 유효성 검사 페이지에서 개별 컨트롤을 켜거나 끌 하는 방법을 배웁니다.

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>작업 1-비간섭 유효성 검사

유효성 검사기를 포함 하 여 복잡 한 데이터를 사용 하 여 양식을 코드 중 약 60%를 나타낼 수 있는 페이지에 너무 많은 JavaScript 코드를 생성 하는 경향이 있습니다. 비간섭 유효성 검사를 사용 하도록 설정, 사용 하 여 HTML 코드에 보다 명확 하 고 좀 더 깔끔하게 살펴보겠습니다.

이 섹션에서는 두 구성에 의해 생성 된 HTML 코드를 비교 하는 ASP.NET에서 비간섭 유효성 검사 사용 하도록 설정 됩니다.

1. 엽니다 **Visual Studio 2012** 연 합니다 **시작** 솔루션에는 **Source\Ex2 Validation\Begin** 이 랩의 폴더입니다. 또는 이전 연습에서 기존 솔루션에서 작업을 계속할 수 있습니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이렇게 하려면 솔루션 탐색기에서를 클릭 합니다 **WebFormsLab** 프로젝트 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 키를 눌러 **F5** 웹 응용 프로그램을 시작 합니다. 고객에 게 페이지를 이동 합니다 **새 고객이 추가** 링크 합니다.
3. 브라우저 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기** 옵션 응용 프로그램에서 생성 된 HTML 코드를 엽니다.

    ![HTML 코드 페이지를 보여주는](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "HTML 코드 페이지를 표시 합니다.")

    *HTML 코드 페이지를 표시합니다.*
4. 페이지 소스 코드를 통해 스크롤하여 ASP.NET가 JavaScript 코드 및 데이터의에서 유효성 검사기 페이지 유효성 검사를 수행 하 여 오류 목록 표시를 삽입에 있음을 확인 합니다.

    ![CustomerDetails 페이지의 JavaScript 코드를 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails 페이지의 JavaScript 유효성 검사 코드")

    *CustomerDetails 페이지의 JavaScript 코드를 유효성 검사*
5. 브라우저를 닫고 Visual Studio로 다시 이동 합니다.
6. 이제 비간섭 유효성 검사를 사용 합니다. 오픈 **Web.Config** 찾아서 **ValidationSettings:UnobtrusiveValidationMode** 키를 **AppSettings** 섹션 **합니다.** 키 값을 설정 **WebForms**합니다.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > 이 속성을 설정할 수도 있습니다는 &quot; **페이지\_부하** &quot; 일부 페이지에 대해서만 비간섭 유효성 검사를 사용 하도록 설정 하려는 경우에는 이벤트입니다.
7. 오픈 **CustomerDetails.aspx** 누릅니다 **F5** 웹 응용 프로그램을 시작 합니다.
8. IE 개발자 도구를 열려면 F12 키를 누릅니다. 개발자 도구를 열면 스크립트 탭을 선택 합니다. 선택 **CustomerDetails.aspx** 사용 하 고 메뉴에서 페이지에 jQuery를 실행 하는 데 필요한 스크립트는 참고에 로드 되어 로컬 사이트에서 브라우저입니다.

    ![로컬 IIS 서버에서 직접 파일을 로드 하는 jQuery JavaScript](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "로컬 IIS 서버에서 직접 파일 jQuery JavaScript를 로드 합니다.")

    *로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드*
9. Visual Studio로 돌아가서 브라우저를 닫습니다. 엽니다는 **Site.Master** 찾아서 파일을 다시 합니다 **ScriptManager**. 특성을 추가 합니다 **EnableCdn** 속성 값을 가진 **True**합니다. 이렇게 하면 jQuery 로컬 사이트의 URL에서가 아니라 온라인 URL에서 로드 되도록 합니다.
10. 오픈 **CustomerDetails.aspx** Visual Studio에서. 사이트를 실행 하려면 F5 키를 누릅니다. Internet Explorer가 열립니다는 한 번, F12 키를 눌러 개발자 도구를 엽니다. 선택 된 **스크립트** 탭을 선택한 다음 드롭다운 목록에 살펴보겠습니다. 온라인 jQuery CDN 아니라 로컬 사이트에서 jQuery JavaScript 파일 로드 되 더 이상 note 합니다.

    ![CDN에서 파일을 로드 하는 jQuery JavaScript](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "CDN에서 파일을 로드 하는 jQuery JavaScript")

    *CDN에서 jQuery JavaScript 파일 로드*
11. 다시 보기 원본 옵션을 사용 하 여 브라우저에서 HTML 페이지 소스 코드를 엽니다. 비간섭 유효성 검사를 사용 하 여 ASP.NET에 삽입된 된 JavaScript 코드와 교체 데이터 알림 \*특성입니다.

    ![비간섭 유효성 검사 코드](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "비간섭 유효성 검사 코드")

    *비간섭 유효성 검사 코드*

    > [!NOTE]
    > 이 예제에서는 몇 가지 HTML 및 JavaScript 선만에 유효성 검사 요약 데이터 주석을 사용한 단순화 했습니다. 어떻게 하는 것이 살펴보았습니다. 이전에 비간섭 유효성 검사를 추가 하면 더 많은 유효성 검사 컨트롤 없이 클수록 JavaScript 유효성 검사 코드가 커집니다.

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>작업 2-데이터 주석 사용한 모델 유효성 검사

ASP.NET 4.5 Web Forms에 대 한 데이터 주석 유효성 검사를 소개합니다. 각 입력의 유효성 검사 컨트롤 대신 모델 클래스에 제약 조건을 정의 하 고 모든 웹 응용 프로그램에서 사용할 이제 수 있습니다. 이 섹션에서는 새로 만들기/편집 고객 양식 유효성 검사에 대 한 데이터 주석을 사용 하는 방법을 배우게 됩니다.

1. 오픈 **CustomerDetail.aspx** 페이지입니다. 고객 이름 및 두 번째 이름를 **EditItemTemplate** 하 고 **먼저** 섹션 RequiredFieldValidator 컨트롤을 사용 하 여 유효성이 검사 됩니다. 각 유효성 검사기는 확인할 조건으로 만큼 유효성 검사기를 포함 해야 하므로 특정 조건에 연결 됩니다.
2. 데이터 주석 유효성을 검사할 Customer 모델 클래스를 추가 합니다. 열기 **Customer.cs** 클래스는 **모델** 폴더와 *데코 레이트* 데이터 주석 특성을 사용 하 여 각 속성입니다.

    (코드 조각- *Forms 랩-Ex02-데이터 주석 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET framework 4.5에는 기존 데이터 주석 컬렉션을 확장 했습니다. 다음은 일부 데이터 주석을 사용할 수 있습니다: [CreditCard] [Phone] [EmailAddress], [범위] [비교]를 [Url] [FileExtensions] [Required], [키], [RegularExpression].
    > 
    > 몇 가지 사용 예:
    > 
    > [키]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > 또한 각 특성 내에서 고유한 오류 메시지를 정의할 수 있습니다.
3. 오픈 **CustomerDetails.aspx** 및 FormView 컨트롤에 EditItemTemplate 및 먼저 섹션의 첫 번째 및 마지막 이름 필드에 대 한 모든 RequiredFieldvalidators를 제거 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > 데이터 주석 사용의 장점 중 하나는 응용 프로그램 페이지에 유효성 검사 논리 중복 되지 않습니다. 모델에서 한 번 정의 하 고 데이터를 조작 하는 모든 응용 프로그램 페이지에 걸쳐 사용 합니다.
4. 오픈 **CustomerDetails.aspx** 코드 숨김 및 SaveCustomer 메서드를 찾습니다. 이 메서드는 새 고객 삽입 될 때 호출 됩니다 및 FormView 컨트롤 값에서 고객 매개 변수를 받습니다. ASP.NET에서 실행 됩니다 매핑을 페이지 컨트롤 사이의 매개 변수 개체 않을 때 발생 하는 경우 모든 데이터 주석에 대 한 모델 유효성 검사 특성 및 있으면 발생 하는 오류와 함께 ModelState 사전을 입력 합니다.

    ModelState.IsValid 유효성 검사를 수행한 후 모델의 모든 필드가 유효 하면 true를 반환 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. 추가 된 **ValidationSummary** 끝 모델 오류 목록에 표시할 CustomerDetails 페이지의 컨트롤입니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    합니다 **ShowModelStateErrors** 로 설정 된 경우는 ValidationSummary에 새 속성을 컨트롤은 **true**, 컨트롤 ModelState 사전에서 오류가 표시 됩니다. 이러한 오류는 데이터 주석 유효성 검사에서 제공 됩니다.
6. 키를 눌러 **F5** 웹 응용 프로그램을 실행 합니다. 일부 잘못 된 값으로 양식을 완료 하 고 클릭 **저장할** 유효성 검사를 실행 합니다. 맨 아래에 요약 오류를 확인 합니다.

    ![데이터 주석 사용한 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "데이터 주석 사용한 유효성 검사")

    *데이터 주석 사용한 유효성 검사*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>작업 3-ModelState 사용 하 여 사용자 지정 데이터베이스 오류 처리

Web Forms의 이전 버전에서는 너무 긴 문자열 또는 고유 키 위반이 같은 데이터베이스 오류 처리 포함 될 수 있습니다 리포지토리 코드에서 예외를 throw 하 고 다음 오류를 표시 하려면 코드 숨김에 예외를 처리 합니다. 코드의 상당한 비교적 간단한 작업을 수행 해야 합니다.

Web Forms 4.5에서 ModelState 개체 모델 또는 데이터베이스에서 페이지에서 일관 된 방식으로 오류를 표시 하려면 사용할 수 있습니다.

이 태스크에서는 올바르게 데이터베이스 예외를 처리 하 고 ModelState 개체를 사용 하 여 사용자에 게 적절 한 메시지를 표시 하는 코드를 추가 합니다.

1. 응용 프로그램이 여전히 실행 되는 동안 중복 된 값을 사용 하는 범주의 이름을 업데이트 하려고 합니다.

    ![중복 된 이름을 사용 하 여 범주를 업데이트](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "중복 된 이름을 사용 하 여 범주를 업데이트 하는 중")

    *중복 된 이름을 사용 하 여 범주를 업데이트 하는 중*

    로 인해 예외가 발생 하는 &quot;고유&quot; 의 제약 조건을 합니다 **CategoryName** 열.

    ![중복 된 범주 이름에 대 한 예외](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "중복 된 범주 이름에 대 한 예외")

    *중복 된 범주 이름에 대 한 예외*
2. 디버깅을 중지합니다. 에 **Products.aspx.cs** 코드 숨김 파일을 업데이트 합니다 **UpdateCategory** db에서 throw 한 예외를 처리 하는 방법. Savechanges () 메서드를 호출 하 고 오류를 추가 합니다 **ModelState** 개체입니다.

    새 **tryupdatemodel에 전달** 메서드는 사용자가 제공 되는 폼 데이터를 사용 하 여 데이터베이스에서 검색 된 범주 개체를 업데이트 합니다.

    (코드 조각- *Forms 랩-Ex02-오류 UpdateCategory 처리 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > 이상적으로 하면 DbUpdateException의 원인을 파악 하 고 근본 원인을 unique key 제약 조건 위반 인지 확인 해야 합니다.
3. 오픈 **Products.aspx** 추가한를 **ValidationSummary** 모델 오류 목록을 표시 하는 GridView 범주 아래에 컨트롤입니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. 사이트를 실행 하 고 제품 페이지로 이동 합니다. 중복 된 값을 사용 하 여 범주 이름을 업데이트 하려고 합니다.

    예외 처리 및 오류 메시지에 표시 합니다 **ValidationSummary** 컨트롤입니다.

    ![범주 오류 중복](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "범주 오류 중복")

    *중복 된 범주 오류*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>ASP.NET Web Forms 4.5에서에서 유효성 검사 요청 작업 4-

Asp.net에서 요청 유효성 검사 기능에는 특정 수준의 교차 사이트 스크립팅 (XSS) 공격에 대 한 기본 보호를 제공합니다. 이전 버전의 ASP.NET 요청 유효성 검사 기본적으로 사용 하도록 설정한에 전체 페이지에 대해서 사용할 수 없습니다. 새 버전의 ASP.NET Web Forms를 사용 하 여 이제, 단일 컨트롤에 대 한 요청 유효성 검사를 사용 하지 않도록 설정, 지연 요청 유효성 검사를 수행 하거나 액세스할 수 되지 않은 유효성이 검사 된 요청 데이터 (이렇게 할 경우 신중 하 게!).

1. 키를 눌러 **ctrl+f5** 디버깅 하지 않고 사이트를 시작 하 여 제품 페이지로 이동 합니다. 범주를 선택 하 고 클릭 합니다 **편집** 제품에 대 한 링크입니다.
2. 예를 들어 HTML 태그를 포함 하 여 잠재적으로 위험한 콘텐츠가 포함 된 설명을 입력 합니다. 요청 유효성 검사로 인해 발생 한 예외에 대 한 공지를 수행 합니다.

    ![잠재적으로 위험한 콘텐츠가 포함 된 제품을 편집](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "잠재적으로 위험한 콘텐츠가 포함 된 제품 편집")

    *잠재적으로 위험한 콘텐츠가 포함 된 제품 편집*

    ![요청 유효성 검사로 인해 예외가](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "요청 유효성 검사로 인해 throw 된 예외")

    *요청 유효성 검사로 인해 throw 된 예외*
3. 페이지를 닫고 Visual Studio에서 눌러 **shift+f5** 디버깅을 중지 합니다.
4. 엽니다는 **ProductDetails.aspx** 찾아서 페이지는 **설명** 텍스트 상자에 붙여넣습니다.
5. 새 추가 **ValidateRequestMode** 텍스트 상자에 속성으로 값을 설정 하 고 **사용 안 함**합니다.

    새 **ValidateRequestMode** 특성을 사용 하면 각 컨트롤에 세부적으로 요청 유효성 검사를 해제할 수 있습니다. HTML 코드를 받을 수 있지만 페이지의 나머지 부분에 대 한 작업 유효성 검사를 유지 하려고 하는 입력에 사용 하려는 경우에 유용 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. 키를 눌러 **F5** 웹 응용 프로그램을 실행 합니다. 편집 제품 페이지를 다시 열고 HTML 태그를 포함 하 여 제품 설명을 완료 합니다. 설명에 HTML 콘텐츠를 추가할 이제 수를 확인 합니다.

    ![제품 설명에 대 한 사용 하지 않도록 설정 하는 유효성 검사 요청](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "요청 제품 설명에 대 한 사용 하지 않도록 설정 하는 유효성 검사")

    *제품 설명에 대 한 사용 하지 않도록 설정 하는 요청 유효성 검사*

    > [!NOTE]
    > 프로덕션 응용 프로그램에서 HTML 태그를 안전 하 게 입력 되지 않도록 하는 사용자가 입력 한 HTML 코드를 삭제 해야 합니다 (예를 들어, 없습니다 &lt;스크립트&gt; 태그). 이 위해 사용할 수 있습니다 [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS)합니다.
7. 제품을 다시 편집 합니다. 이름 필드에 HTML 코드를 입력 하 고 클릭 **저장할**합니다. 설명 필드에 대 한 요청 유효성 검사를 비활성화만 되 고 잠재적으로 위험한 콘텐츠에 대해 여전히 유효성 검사 다시 필드의 나머지 부분을 확인 합니다.

    ![필드의 나머지 부분에서 사용 하도록 설정 하는 유효성 검사 요청](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "요청 필드의 나머지 부분에서 사용 하도록 설정 하는 유효성 검사")

    *필드의 나머지 부분에서 사용 하도록 설정 하는 요청 유효성 검사*

    ASP.NET Web Forms 4.5 지연 요청 유효성 검사를 수행 하는 새 요청 유효성 검사 모드를 포함 합니다. 로 설정 하는 요청 유효성 검사 모드를 사용 하 여 **4.5**이면 코드 액세스 부분 *Request.Form [&quot;키&quot;]*, ASP.NET 4.5의 요청 유효성 검사는 유일한 트리거 요청 유효성 검사 에 대 한 폼 컬렉션의 특정 요소에 해당 합니다.

    또한 ASP.NET 4.5에는 Microsoft에서 ANTI-XSS 라이브러리 v4.0에서 주요 인코딩 루틴은 이제 포함 됩니다. ANTI-XSS 인코딩 루틴은 새 구현 됩니다 *AntiXssEncoder* 새 형식을 찾을 **System.Web.Security.AntiXss** 네임 스페이스입니다. 사용 하 여는 **encoderType** 를 사용 하도록 구성 하는 매개 변수 *AntiXssEncoder*, 새 인코딩 루틴을 사용 하 여 ASP.NET 내에 인코딩을 자동으로 모든 출력 합니다.
8. ASP.NET 4.5 요청 유효성 검사는 또한 요청 데이터에 대 한 유효성을 검사 되지 않은 액세스를 지원합니다. ASP.NET 4.5에는 새 컬렉션 속성을 추가 합니다 **HttpRequest** 라는 개체 **Unvalidated**합니다. 로 이동 하는 경우 **HttpRequest.Unvalidated** Forms "," 문자열이 "," 쿠키 "," Url "및" 등을 포함 하 여 요청 데이터의 일반적인 부분 모두에 액세스할 수 있습니다.

    ![Request.Unvalidated 개체](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated 개체")

    *Request.Unvalidated 개체*

    > [!NOTE]
    > **주의 해 서 HttpRequest.Unvalidated 속성을 사용 하세요!** 신중 하 게에 원시 요청 데이터를 위험한 텍스트 라운드트립 및 모르는 고객에 게 렌더링 되지 않는 사용자 지정 유효성 검사를 수행 해야 합니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>연습 3: 비동기 페이지 처리에 ASP.NET Web Forms

이 연습에서는 ASP.NET Web Forms의 기능을 처리 하는 새 비동기 페이지에 소개 합니다.

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>작업 1-제품 업데이트 페이지 업로드 하 고 이미지를 표시 하려면 세부 정보

이 태스크에서는 사용자가 제품에 대 한 이미지 URL을 지정 하 여 읽기 전용 뷰에 표시를 허용 하도록 제품 정보 페이지를 업데이트 합니다. 동기적으로 다운로드 하 여 지정된 된 이미지의 로컬 복사본을 만들게 됩니다. 다음 태스크에서는이 구현을 비동기적으로 작동 하도록 업데이트 합니다.

1. 열기 **Visual Studio 2012** 로드 합니다 **시작** 솔루션 **Source\Ex3 Async\Begin** 이 랩의이 폴더에서. 또는 이전 연습에서 기존 솔루션에 작업을 계속할 수 있습니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이렇게 하려면 솔루션 탐색기에서를 클릭 합니다 **WebFormsLab** 프로젝트를 마우스 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 엽니다는 **ProductDetails.aspx** 원본 페이지 및 FormView의 ItemTemplate 제품 이미지를 표시 하려면 필드를 추가 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. FormView의 EditTemplate에 이미지 URL을 지정 하는 필드를 추가 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. 엽니다는 **ProductDetails.aspx.cs** 코드 숨김 파일을 다음 네임 스페이스 지시문을 추가 합니다.

    (코드 조각- *Forms 랩-Ex03-네임 스페이스 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. 만들기는 **UpdateProductImage** 로컬에서 원격 이미지를 저장 하는 방법 **이미지** 폴더 및 새 이미지 위치 값을 지닌 제품 엔터티를 업데이트 합니다.

    (코드 조각- *Forms-Ex03-랩 UpdateProductImage 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. 업데이트를 **UpdateProduct** 메서드를 호출 합니다 **UpdateProductImage** 메서드.

    (코드 조각- *웹 폼 랩-Ex03-UpdateProductImage 호출*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. 응용 프로그램을 실행 하는 제품에 대 한 이미지를 업로드 하려고 합니다. 예를 들어 Office 클립 예술에서 다음 이미지 URL을 사용할 수 있습니다. [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![제품에 대 한 이미지를 설정](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "제품에 대 한 이미지 설정")

    *제품에 대 한 이미지 설정*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>2-제품 세부 정보 페이지가 처리 비동기 추가 작업

이 태스크에서는 제품 정보 페이지를 비동기적으로 작동 하도록 업데이트 합니다. ASP.NET 4.5의 비동기 페이지 처리를 사용 하 여-이미지 다운로드 프로세스-장기 실행 작업을 향상 시킬가 있습니다.

웹 응용 프로그램에서 비동기 메서드는 ASP.NET 스레드 풀이 사용 되는 방식을 최적화를 사용할 수 있습니다. ASP.NET 있습니다는 참가 대 한 스레드 풀의 스레드 수가 제한 요청, 따라서 모든 스레드를 사용 중인 경우 ASP.NET 새 요청을 거부 하기 시작, 응용 프로그램 오류 메시지를 보낼에 사이트를 사용할 수 없게 합니다.

웹 사이트에 시간이 많이 걸리는 작업 오랜 시간 동안 할당 된 스레드를 차지 하기 때문에 비동기 프로그래밍을 위한 훌륭한 후보가.입니다. 장기 실행 요청, 많은 다양 한 요소를 사용 하 여 페이지 및 오프 라인 작업, 이러한 데이터베이스를 쿼리 또는 외부 웹 서버에 액세스 해야 하는 페이지가 포함 됩니다. 비동기 메서드를 사용 하면 이러한 작업에 대 한 페이지를 처리 하는 동안 스레드가 해제 되며 스레드로 반환 장점은 풀 및 새 페이지 요청에 참가 하는 데 사용할 수 있습니다. 이 즉, 페이지에서 스레드 풀 스레드에 처리 시작 되 고 비동기 처리가 완료 된 후에 다른 곳에 처리를 완료할 수 있습니다.

1. 엽니다는 **ProductDetails.aspx** 페이지입니다. 추가 합니다 **비동기** 특성을 **페이지** 요소로 설정 **true**합니다. 이 특성은 IHttpAsyncHandler 인터페이스를 구현 하는 ASP.NET에 알립니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. 페이지를 실행 하는 스레드에 세부 정보를 표시할 페이지의 맨 아래에 레이블을 추가 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. 열어야 **ProductDetails.aspx.cs** 다음 네임 스페이스 지시문을 추가 합니다.

    (코드 조각- *Forms 랩-Ex03-네임 스페이스 2 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. 수정 된 **UpdateProductImage** 메서드를 비동기 작업을 사용 하 여 이미지를 다운로드 합니다. 바꿉니다 합니다 **WebClient** **DownloadFile** 메서드를 **DownloadFileTaskAsync** 메서드 포함 및를 **await** 키워드.

    (코드 조각- *Forms-Ex03-랩 UpdateProductImage 비동기 웹*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    RegisterAsyncTask는 다른 스레드에서 실행할 새 페이지 비동기 작업을 등록 합니다. 실행할 작업 (t)를 사용 하 여 람다 식을 받습니다. 합니다 **await** 키워드는 **DownloadFileTaskAsync** 메서드 변환 후 비동기적으로 호출 되는 콜백 메서드의 나머지는 **DownloadFileTaskAsync** 메서드를 완료 합니다. ASP.NET 자동으로 모든 HTTP 요청 원래 값을 유지 하 여 메서드의 실행을 다시 시작 됩니다. .NET 4.5의 새로운 비동기 프로그래밍 모델을 사용 하면 콜백 함수나 연속 코드의 복잡성을 처리 하 고 컴파일러 및 동기 코드와 매우 비슷하며 비동기 코드를 작성할 수 있습니다.
    > [!NOTE]
    > RegisterAsyncTask 및 PageAsyncTask 된 이미.NET 2.0부터입니다. Await 키워드는.NET 4.5의 비동기 프로그래밍 모델에서 새로운 기능과.NET WebClient 개체에서 새 TaskAsync 메서드와 함께 사용할 수 있습니다.
5. 코드를 시작 및 실행이 완료 스레드를 표시 하는 코드를 추가 합니다. 이 작업을 수행 하려면 업데이트 된 **UpdateProductImage** 메서드를 다음 코드로 합니다.

    (코드 조각- *Web Forms 랩-Ex03-Show 스레드*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. 웹 사이트를 엽니다 **Web.config** 파일입니다. 다음 appSetting 변수를 추가 합니다.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. 키를 눌러 **F5** 응용 프로그램을 실행 하는 제품에 대 한 이미지를 업로드 합니다. 시작 및 완료 된 코드를 다른 수 있는 스레드 ID를 확인 합니다. ASP.NET 스레드 풀에서 별도 스레드에서 실행 하는 비동기 작업 때문입니다. 작업이 완료 되 면 ASP.NET 태스크를 큐에 다시 배치 하 고 사용 가능한 스레드 중 하나를 할당 합니다.

    ![이미지를 비동기로 다운로드할](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "이미지를 비동기적으로 다운로드")

    *이미지를 비동기적으로 다운로드*

> [!NOTE]
> 또한 Azure는 다음이 응용이 프로그램을 배포할 수 있습니다 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.


* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서 다음 개념 해결 되었으며 설명:

- 강력한 데이터 바인딩 식을 사용 하 여
- Web Forms에서 새 모델 바인딩 기능을 사용 합니다.
- 값 공급자를 사용 하 여 코드 숨김 방법 페이지 데이터를 매핑하기 위한
- 사용자 입력된 유효성 검사에 대 한 데이터 주석 사용
- Web Forms에서 advange jQuery 사용한 unobstrusive 클라이언트 쪽 유효성 검사의 수행
- 세분화 된 요청 유효성 검사 구현
- Web Forms에서 처리 하는 비동기 페이지를 구현 합니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Azure SDK를 사용 하 여</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록은 Azure Portal에서 새 웹 사이트를 만들고 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>작업 1-Azure Portal에서 새 웹 사이트 만들기

1. 로 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다. 등록할 수 있습니다 [여기](http://aka.ms/aspnet-hol-azure)합니다.

    ![Windows Azure 포털에 로그온](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Windows Azure 포털에 로그온")

    *포털에 로그온*
2. 클릭 **새로 만들기** 명령 모음에서.

    ![새 웹 사이트를 만드는](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 선택한 **빨리 만들기** 옵션입니다. 새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Azure는 웹 응용 프로그램을 제어 하 고 관리할 수 있는 클라우드에서 실행 중인 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 Azure에 완전된 한 웹 응용 프로그램을 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지를 열어](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.

    > [!NOTE]
    > 합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Azure에 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다. **Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Azure에 웹 응용 프로그램을 게시합니다.

    ![게시 프로필 다운로드 웹 사이트](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 Azure에 웹 응용 프로그램을 게시 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "게시 프로필 저장")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다. SQL Database 서버에 Azure 관리 포털의 구독에서 볼 수 있습니다 **Sql Database** | **서버** | **서버대시보드**. 만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다. 만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.

    ![SQL Database 서버 대시보드](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다. 이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.

    ![변경 확인](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *변경 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션 돌아갑니다. 에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.

    ![응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "응용 프로그램 게시")

    *웹 사이트를 게시합니다.*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결의 유효성을 검사**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).

    ![웹 배포 구성](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - 에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름을 입력 합니다.

     ![대상 연결 문자열 구성](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들라는 메시지가 나오면 **예**합니다.

    ![데이터베이스를 만드는](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. 기본 연결 텍스트 상자 내에서 사용 하 여 Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다. **다음**을 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지에서 클릭 **게시**합니다.

    ![웹 응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 c: 코드 조각 사용

코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다. 랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")

*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*

***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![Tab 키를 다시 코드 조각 확장 됩니다](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")

*Tab 키를 다시 및 코드 조각에서는 확장*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")

*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 코드 조각 선택](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "클릭 하 여 목록에서 관련 코드 조각 선택")

*클릭 하 여 목록에서 관련 코드 조각 선택*
