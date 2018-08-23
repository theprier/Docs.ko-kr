---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용할 | Microsoft Docs
author: microsoft
description: 7 단계 템플릿 부분 보기 및 마스터 페이지를 사용 하 여, 코드 중복을 제거 하는 보기 템플릿 내에서 ' 반복 금지 원칙의 ' 적용할 수 있습니다 하는 방법에 살펴봅니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0da32e6ac38f10df6e581517989b3b1fd2f2328c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837987"
---
<a name="re-use-ui-using-master-pages-and-partials"></a>마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 7 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 7 단계 템플릿 부분 보기 및 마스터 페이지를 사용 하 여, 코드 중복을 제거 하는 보기 템플릿 내에서 "반복 금지 원칙의" 적용할 수 있습니다 하는 방법에 살펴봅니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner 단계 7: 부분 및 마스터 페이지

ASP.NET MVC는 수용 디자인 원칙 중 하나는 "수행 하지 반복 금지" 원칙 ("시험" 라고 함)입니다. DRY 디자인 코드와는 궁극적으로 빌드를 빠르고 쉽게 유지 관리 하는 응용 프로그램 논리의 중복을 제거 하는 데 도움이 됩니다.

NerdDinner 시나리오의 몇 가지 적용 반복 금지 원칙의 이미 살펴보았습니다. 몇 가지 예: 유효성 검사 논리는 컨트롤러;에서 시나리오를 만들고 편집에서 적용할 수 있도록 하는 모델 계층 내에서 구현 됩니다 편집, 세부 정보 및 삭제 작업 메서드를 통해 다시 사용 "NotFound" 보기 템플릿 View() 도우미 메서드를 호출할 때 이름을 명시적으로 지정 하지 않아도 되는 뷰 템플릿을 사용 하 여 규칙-명명 패턴을 사용 하는 것 및는 다시 편집에 대 한 DinnerFormViewModel 클래스를 사용 하 고 작업 시나리오를 만듭니다.

이제 방법을 살펴보겠습니다 "반복 금지 원칙의" 적용할 수 있습니다도 있습니다 코드 중복을 제거 하는 보기 템플릿 내에서.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>다시 방문 하 여 편집 및 보기 템플릿 만들기

현재 Dinner 폼 UI를 표시할 두 개의 서로 다른 뷰 템플릿 – "Edit.aspx" 및 "Create.aspx" –를 사용 하는 것입니다. 이러한 빠른 visual 비교는 얼마나 유사한 지 강조 표시 합니다. 만들기 폼 모양은 다음과 같습니다.

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

및 "편집" 폼 모양은 다음과 같습니다.

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

큰 차이 무엇입니까? 제목 및 헤더 텍스트 이외에 다른 폼 레이아웃 및 입력 컨트롤은 동일 합니다.

보기 템플릿은 소요 됩니다 "Edit.aspx" 및 "Create.aspx" 열에서는 경우에 동일한 양식 레이아웃 및 입력 컨트롤 코드를 포함 합니다. 이 중복이 소개에서는 또는 좋은 없는 새 Dinner 속성-변경 하는 때마다에 두 번 변경 생길 것을 의미 합니다.

### <a name="using-partial-view-templates"></a>부분 뷰 템플릿 사용

ASP.NET MVC 페이지의 하위 부분 뷰 렌더링 논리를 캡슐화 하는 "부분 보기" 템플릿을 정의 하는 기능을 지원 합니다. "부분" 뷰 렌더링 논리를 한 번 정의 하는 유용한 방법을 제공 하 고 다시 사용 여러 위치에서 응용 프로그램 간에 합니다.

"시험" 우리의 Edit.aspx 및 Create.aspx 보기 템플릿 복제를 위해 "DinnerForm.ascx" 양식 레이아웃 및 둘 다에 공통적으로 적용 되는 입력된 요소를 캡슐화 하는 명명 된 부분 뷰 템플릿을 만들 수 있습니다. 우리의/보기/Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여이 작업을 수행 하겠습니다는 "추가-&gt;보기" 메뉴 명령:

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

그러면 "뷰 추가" 대화 상자를 표시 됩니다. 이름을 새 보기 "DinnerForm"를 만들고,이 대화 상자에 "부분 뷰 만들기" 확인란을 선택 하 고는 전달 되는 것을 DinnerFormViewModel 클래스를 나타냅니다.

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

"추가" 단추를 클릭 하는 경우 Visual Studio는 우리 회사에 새 "DinnerForm.ascx" 보기 템플릿을 "\Views\Dinners" 디렉터리 내에서 만듭니다.

에서는 다음 붙여 넣을 수 중복 폼 레이아웃 /에 새 "DinnerForm.ascx" 부분 보기 템플릿은 Edit.aspx/ Create.aspx 우리의 보기 템플릿에서 컨트롤 코드를 입력 합니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

그런 다음 DinnerForm 부분 템플릿을 호출할 폼 중복을 제거 하는 편집 및 만들기 보기 템플릿을 업데이트할 수 있습니다. 에서는 이렇게 호출 Html.RenderPartial("DinnerForm") 우리의 보기 템플릿 내에서:

##### <a name="createaspx"></a>Create.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Html.RenderPartial를 호출 하는 경우 원하는 부분 서식 파일의 경로 명시적으로 한정할 수 있습니다 (예: ~ Views/Dinners/DinnerForm.ascx "). 위의 코드에서 그러나는 ASP.NET MVC에서 규칙 기반 명명 패턴을 활용 하 고 렌더링할 부분 이름으로 "DinnerForm"를 지정 합니다. 이 작업을 수행 하는 경우 ASP.NET MVC는 찾습니다 규칙 기반 views 디렉터리의 첫 번째 (DinnersController/보기/Dinners 됩니다). 부분 템플릿을 찾지 못하면 있습니다 다음 보일지에 대 한 /Views/Shared 디렉터리에 있습니다.

Html.RenderPartial() 부분 보기의 이름만 사용 하 여 호출 되 면 ASP.NET MVC 동일한 모델과 ViewData 사전을 사용 하는 개체 뷰 템플릿을 호출 하 여 부분 보기에 전달 합니다. 또는 대체 모델 개체 및/또는 ViewData 사전을 사용 하 여 부분 뷰를 전달할 수 있도록 하는 오버 로드 된 버전의 Html.RenderPartial() 됩니다. 만을 저장할 전체 모델/ViewModel의 하위 집합을 전달 하는 시나리오에 유용 합니다.

| **쪽 항목: 왜 &lt;% %&gt; of &lt;% = %&gt;?** |
| --- |
| 사용 하는 미묘한 위의 코드를 사용 하 여 보았을 것 중 하나를 &lt;% %&gt; 블록 대신를 &lt;% = %&gt; Html.RenderPartial()를 호출 하는 경우 차단 합니다. &lt;% = %&gt; 개발자가 지정된 된 값을 렌더링 하는 ASP.NET의 블록 나타냅니다 (예: &lt;% = "Hello" %&gt; "Hello"를 렌더링 하는). &lt;% %&gt; 블록에는 대신 개발자가 코드를 실행 하려고 하 고 내에 출력을 렌더링 된 어떠한 이루어져야 합니다. 명시적으로 함을 나타냅니다 (예: &lt;Response.Write("Hello") %&gt;합니다. 사용 하는 이유는 &lt;% %&gt; 위의 Html.RenderPartial 코드 블록은 Html.RenderPartial() 메서드는 문자열을 반환 하지 않습니다 하 고 대신 호출 템플릿 보기에 직접 콘텐츠를 스트림에 출력을 출력 합니다. 성능상의 이유로 효율성 및 해당 하면 (잠재적으로 매우 큼) 임시 문자열 개체를 만들 필요가 없습니다. 이렇게 하 여이 수행 합니다. 메모리 사용량 줄이고 전체 응용 프로그램 처리량을 향상 합니다. 한 가지 일반적인 실수 때 Html.RenderPartial()를 사용 하 여 내에 없을 때 호출의 끝에 세미콜론을 추가 해야 하는 &lt;% %&gt; 블록입니다. 예를 들어이 코드 하면 컴파일러 오류가 발생 합니다. &lt;Html.RenderPartial("DinnerForm") %&gt; 작성 해야 하는 대신: &lt;Html.RenderPartial("DinnerForm") %; %&gt; 때문에 이것이 &lt;% %&gt; 블록은 자체 포함 된 코드 문의 문을 세미콜론으로 종료 하는 데 필요한 C# 코드를 사용 하는 경우. |

### <a name="using-partial-view-templates-to-clarify-code"></a>부분 뷰 템플릿을 사용 하 여 코드를 명확 하 게

여러 위치에서 뷰 렌더링 논리를 복제 하지 않으려면 "DinnerForm" 부분 뷰 템플릿을 만들었습니다. 부분 뷰 템플릿을 만드는 가장 일반적인 이유입니다.

경우에 따라 여전히는 것이 좋습니다만 단일 위치에서 호출 될 경우에 부분 보기를 만들 수 있습니다. 매우 복잡 한 뷰 템플릿 자주 해당 뷰 렌더링 논리를 추출 및 하나로 분할 또는 템플릿의 부분을 더 잘 라는 하는 경우 읽기를 훨씬 쉽게 될 수 있습니다.

예를 들어를 Site.master 파일 (살펴볼 것에서 곧)는 프로젝트에서 코드 조각 아래. 코드는 비교적 간단 읽을 – 맨 위에 있는 로그인/로그 아웃을 표시 하는 논리를 연결 하기 때문에 부분적으로 화면의 오른쪽 "LogOnUserControl" 부분 내에서 캡슐화 됩니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

혼란 직접 찾을 때마다 템플릿 보기 내에서 html/코드 태그를 이해 하는 동안, 여부를 추출 하 고 이름을 잘 지정 부분 보기로 리팩터링 되었으면 일부 정보를 더 분명히 알 수 없습니다 하는 것이 좋습니다.

### <a name="master-pages"></a>마스터 페이지

ASP.NET MVC 부분 뷰를 지원할 뿐 아니라 일반적인 레이아웃 및 최상위 html 사이트의 정의를 사용할 수 있는 "마스터 페이지" 템플릿을 만드는 기능도 지원 합니다. 콘텐츠 자리 표시자 컨트롤 재정의 하거나 "입력" 보기에서 실행할 수 있는 대체 가능 영역을 식별 하는 마스터 페이지에 추가할 수 있습니다. 응용 프로그램 간에 일반적인 레이아웃을 적용 하는 매우 효과적인 (및 반복 금지) 방법을 제공 합니다.

기본적으로 새 ASP.NET MVC 프로젝트에 자동으로 추가 하는 마스터 페이지 템플릿을 적용 합니다. 이 마스터 페이지에는 "Site.master" 및 \Views\Shared\ 폴더 내에서 있는 이름이 지정 됩니다.

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

기본 Site.master 파일을 아래와 같습니다. 맨 위에 있는 탐색에 대 한 메뉴와 함께 사이트의 외부 html을 정의 합니다. 콘텐츠 자리 표시자를 대체할 수 있는 두 개의 – 제목 및 페이지의 기본 콘텐츠는 바꿔야 하는 것에 대 한 기타 하나 포함 합니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

NerdDinner 응용 프로그램 ("List", "Details", "편집", "만들기", "NotFound" 등) 용으로 만든 모든 보기 기반을 두었습니다이 Site.master 템플릿. 이 기본적으로 위쪽에 추가 된 "MasterPageFile" 특성을 통해 표시 됩니다 &lt;% @ 페이지 %&gt; 지시문 "뷰 추가" 대화 상자를 사용 하 여 뷰를 만들 때:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

즉 Site.master 콘텐츠를 변경할 수 있습니다 및가 변경 내용을 자동으로 적용 되며 우리의 보기 템플릿 중 하나를 렌더링 하는 경우에 사용 합니다.

응용 프로그램의 헤더는 "내 MVC 응용 프로그램" 대신 "NerdDinner" 있도록 우리의 Site.master 헤더 섹션을 업데이트 해 보겠습니다. 보겠습니다도 업데이트는 탐색 메뉴 되도록 첫 번째 탭 "찾기는 저녁 식사" (HomeController의 index () 동작 메서드에서 처리), "호스트를 저녁 식사" (DinnersController의 create () 동작 메서드에서 처리 됨) 이라는 새 탭을 추가 해 보겠습니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Site.master 파일 및 새로 고침 저장이 헤더를 보면 브라우저는 표시 응용 프로그램 내에서 모든 뷰에 변경 합니다. 예를 들어:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

와 */Dinners/편집 / [id]* URL:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>다음 단계

마스터 페이지 및 부분 뷰를 완전히 구성할 수 있도록 매우 유연한 옵션을 제공 합니다. 뷰에서 중복을 방지할 수 콘텐츠 / 코드 하며 보기 템플릿을 더 쉽게 읽고 유지 관리를 찾을 수 있습니다.

보겠습니다 이제 앞서 작성 목록 시나리오를 다시 방문 및 확장 가능한 페이징 지원을 사용 하도록 설정 합니다.

> [!div class="step-by-step"]
> [이전](use-viewdata-and-implement-viewmodel-classes.md)
> [다음](implement-efficient-data-paging.md)
