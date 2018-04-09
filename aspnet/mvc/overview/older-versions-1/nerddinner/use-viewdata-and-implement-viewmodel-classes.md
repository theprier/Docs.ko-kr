---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 사용 하 여 ViewData 및 구현 ViewModel 클래스 | Microsoft Docs
author: microsoft
description: 6 단계에서는 시나리오를 편집 하는 다양 한 형식에 대 한 지원을 어떻게 사용 하도록 설정 하 고 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법에 대해서도 설명:...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 9ba8758bd6524f3e300f3fd91ef68cfe8a3587a7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="use-viewdata-and-implement-viewmodel-classes"></a>사용 하 여 ViewData 및 구현 ViewModel 클래스
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 6 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 6 단계에서는 시나리오를 편집 하는 다양 한 형식에 대 한 지원을 어떻게 사용 하도록 설정 하 고 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법에 대해서도 설명: ViewData 및 ViewModel입니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>업그레이드 되었으며 수정 단계 6: ViewData 및 ViewModel

다양 한 폼 게시 시나리오를 대상 고 구현 하는 방법을 논의 했으므로 만들기, 업데이트 및 삭제 (CRUD) 지원 합니다. 이제 추가 DinnersController 구현은 수행할 알아보고 시나리오를 편집 하는 다양 한 형식에 대 한 지원을 사용 하도록 설정 하겠습니다. 이 작업을 수행 하는 동안 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법에 설명 합니다: ViewData 및 ViewModel입니다.

### <a name="passing-data-from-controllers-to-view-templates"></a>템플릿 보기에 컨트롤러에서 데이터 전달

엄격한 "문제의 분리" MVC 패턴의 결정적인 특징 중 하나는 응용 프로그램의 여러 구성 요소 간의 적용 하는 데 도움이 됩니다. 모델, 컨트롤러와 뷰 각각 잘 정의 되어 역할 및 책임 및 잘 정의 된 방법으로 서로 통신 합니다. 이렇게 하면 테스트 가능성을 승격 하 고 코드 재사용 합니다.

컨트롤러 클래스를 클라이언트에 다시를 HTML 응답을 렌더링 하기로 하는 경우에 응답을 렌더링 하는 데 필요한 모든 데이터 템플릿 보기에 명시적으로 전달 하는 일을 담당 합니다. 템플릿 보기 – 데이터 검색 또는 응용 프로그램 논리를 수행 하면 안 및만 하는 컨트롤러에 의해 전달 모델/데이터 구동 되는 렌더링 코드 자체 제한 대신 해야 합니다.

지금은 모델 데이터 우리의 DinnersController에 의해 전달 되 클래스 템플릿 우리의 보기를 단순 하 고 직관적인 – index ()의 경우 Dinner 개체의 목록 및 단일 Dinner 개체 Details(), Edit(), create () 및 delete ()의 경우. 응용 프로그램에 더 많은 UI 기능을 추가 했습니다 종종을 하겠습니다 보다 더 우리의 템플릿 보기에서 HTML 응답을 렌더링 하려면이 데이터를 전달 해야 합니다. 예를 들어 다음 우리의 편집 내의 "국가" 필드를 변경 하 고 dropdownlist는 HTML 텍스트 상자에서 보기를 만들 하는 것이 좋습니다. 하드 코딩 템플릿 보기에에서 국가 이름 드롭다운 목록, 대신 동적으로 채울에서는 지원 되는 국가 목록은에서 생성 하는 것이 좋습니다. 저녁 개체를 전달 하는 방법이 필요 합니다 *및* 우리의 템플릿 보기에는 컨트롤러에서 지원 되는 국가 목록은 합니다.

두 가지 방법으로이 위해 수를 살펴 보겠습니다.

### <a name="using-the-viewdata-dictionary"></a>사전은 사용 하 여

컨트롤러의 기본 클래스는 컨트롤러에서 뷰를 다른 데이터 항목을 전달 하는 데 사용할 수 있는 "ViewData" 사전 속성을 노출 합니다.

예를 들어 우리의 편집 뷰 내에서 "국가" textbox dropdownlist는 HTML 텍스트 상자에서 변경 하려는 시나리오를 지원 하려면 수 업데이트 (뿐 아니라 Dinner 개체)는 m으로 사용할 수 있는 SelectList 개체를 전달 하는 Edit() 동작 메서드 국가 dropdownlist의 odel 합니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

위의 SelectList의 생성자에서 현재 선택 된 값과 함께, 놓기 downlist를 채우는 데 군 목록을 수락 합니다.

우리의 Edit.aspx 보기 템플릿 Html.TextBox() 도우미 메서드 이전에 사용 되는 대신 Html.DropDownList() 도우미 메서드를 사용 하도록 업데이트할 수 했습니다.

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

위의 Html.DropDownList() 도우미 메서드 두 개의 매개 변수를 사용 합니다. 첫 번째에는 HTML 폼 요소 출력의 이름입니다. 두 번째는 사전은 통해 전달 했습니다 "SelectList" 모델입니다. 사용 하 여 C# "키워드 as"는 SelectList로 사전에 있는 형식을 캐스팅 합니다.

म 실행할 때이 응용 프로그램 및 액세스 하 고는 */Dinners/Edit/1* URL 브라우저 내에서 볼 수 있겠지만, 우리의 편집 UI가 텍스트 상자 대신 국가의 dropdownlist를 표시 하도록 업데이트 되었습니다.

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

시나리오에서 오류 발생 시 HTTP POST 편집 메서드에서 템플릿 편집 뷰를 렌더링할 수도, 때문에 것도 보기 템플릿 오류 시나리오에서 렌더링 될 때 ViewData 하 여 SelectList를 추가 하려면이 메서드를 업데이트할 수 있는지 확인 하려고 합니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

이제 DinnersController 편집 시나리오 DropDownList를 지원 합니다.

### <a name="using-a-viewmodel-pattern"></a>ViewModel 패턴 사용

ViewData 사전 접근 방식에 매우 쉽고 빠르게 구현할 수 있다는 이점이 있습니다. 일부 개발자 마음에 들지 않는 문자열 기반 사전을 사용 하 여 하지만 오타 컴파일 타임에 발견 되지 않으므로 오류가 발생할 수 있으므로 합니다. 형식화 되지 않은 사전은 "as" 연산자를 사용 하 여 또는 캐스팅 템플릿 보기에서에서 C#과 같은 강력한 형식의 언어를 사용 하는 경우에 필요 합니다.

한 대체 방법을 사용 하 여은 하나는 "ViewModel" 패턴 이라고 합니다. 이 패턴을 사용 하는 경우 강력한 형식의 클래스의 특정 보기 시나리오에 최적화 된 및 우리의 템플릿 보기에 필요한 동적 값/콘텐츠에 대 한 속성을 노출 합니다 만듭니다. 컨트롤러 클래스 다음 이러한 보기 액세스에 최적화 된 클래스 우리의 뷰 템플릿을 사용 하려면에 전달을 채울 수 있습니다. 이렇게 하면 형식 안전성, 컴파일 타임 검사 및 템플릿 보기 내에서 편집기 intellisense 수 있습니다.

예를 들어, 두 개의 강력한 형식의 속성을 표시 하는 dinner 양식 "DinnerFormViewModel"을 만들 수 있습니다 편집 시나리오 아래와 같은 클래스를 사용 하도록 설정 하려면: Dinner 개체 및 국가 dropdownlist를 채우는 데 필요한 SelectList 모델:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

다음 우리의 저장소에서 검색 하는 Dinner 개체를 사용 하 여 DinnerFormViewModel 만들려는 우리의 Edit() 작업 메서드를 업데이트 하 고 우리의 템플릿 보기에 전달할 수 있습니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

त ु म च 같이 우리의 보기 템플릿 한다는 "Dinner" 대신 "DinnerFormViewModel" 필요 하므로 개체 edit.aspx 페이지 맨 위에 있는 "inherits" 특성을 변경 하 여 업데이트 한 후:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

이렇게 म 우리의 보기 템플릿 내에서 "모델" 속성의 intellisense 것 전달 DinnerFormViewModel 형식의 개체 모델을 반영 하도록 업데이트 됩니다.

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

그런 다음 밖 작업 보기 코드를 업데이트할 수 있습니다. 생성 방법에서는 변경 하지 않는 입력 요소의 이름 아래 공지 (form 요소는 여전히 지정 "제목", "국가") – DinnerFormViewModel 클래스를 사용 하 여 값을 검색 하는 HTML 도우미 메서드를 업데이트 하려고 하지만:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

또한 업데이트 하는 중 오류를 렌더링할 때 DinnerFormViewModel 클래스를 사용 하는 편집 post 메서드:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

동일한 재사용 하 여 정확한 create () 동작 메서드를 업데이트할 수도 있습니다 *DinnerFormViewModel* 클래스 국가 같이 DropDownList 내는 것도 사용할 수 있도록 합니다. 다음은 HTTP GET 구현이입니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

다음은 HTTP POST 만들 메서드의 구현이입니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

고 이제이 우리의 만들기 및 편집 화면 드롭다운 목록을 국가 선택 하는 데 지원 합니다.

### <a name="custom-shaped-viewmodel-classes"></a>사용자 지정 모양의 ViewModel 클래스

위 시나리오 DinnerFormViewModel 클래스 직접 지원 SelectList 모델 속성과 함께 속성으로 저녁 모델 개체를 노출합니다. 이 방법은 시나리오 여기서 우리의 보기 템플릿 내에서 만들려고 HTML UI 비교적 밀접 하 게에 해당 도메인 모델 개체에 대 한 제대로 작동 합니다.

이 시나리오에 대 한 경우 사용할 수 있는 옵션 중 하나를 뷰에서 – 소비에 대 한 개체 모델로 최적화 더 되 고 기본 도메인 모델 개체와에서 다 같습니다 사용자 지정 모양의 ViewModel 클래스를 만드는 것입니다. 예를 들어 서로 다른 속성 이름 및/또는 여러 모델 개체에서 수집 하는 집계 속성 노출 될 수 없습니다.

사용자 지정 모양의 ViewModel 클래스 수 모두 뷰를 렌더링 하려면 뿐만 아니라 컨트롤러의 동작 메서드를 다시 게시 하는 양식 데이터를 처리 하려면 컨트롤러에서 데이터를 전달 하는 데 사용 합니다. 나중이 시나리오에 대 한 폼 게시 데이터를 사용 된 ViewModel 개체를 업데이트 하 고 다음 ViewModel 인스턴스를 사용 하 여 매핑하거나 실제 도메인 모델 개체를 검색할 작업 메서드를 할 수 있습니다.

ViewModel 클래스 사용자 지정 모양의 많은 유연성을 제공할 수 있습니다 및은 시작 너무 복잡 하는 작업 메서드 내 보기 템플릿 또는 폼 게시 코드 내에서 렌더링 코드를 찾을 언제 든 지 조사 해야 할 항목입니다. 이 도메인 모델을 생성 하는 UI 완전히 동일 하지 않습니다는 및 중간 사용자 지정 모양의 ViewModel 클래스가 도와 나타내기도 합니다.

### <a name="next-step"></a>다음 단계

이제 살펴보겠습니다 사용 하는 방법을 부분 및 마스터 페이지를 다시 사용 하 고 응용 프로그램에서 UI를 공유 합니다.

> [!div class="step-by-step"]
> [이전](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [다음](re-use-ui-using-master-pages-and-partials.md)
