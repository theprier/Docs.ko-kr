---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: "마스터 페이지 및 부분을 사용 하 여 UI를 사용 하 여 다시 | Microsoft Docs"
author: microsoft
description: "7 단계 부분 뷰 서식 파일 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하는 보기 템플릿 내에서 ' 건조 원칙 '를 적용할 수 있습니다 하는 방법을 살펴봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: c42cd6aca40b08a9f8461532fbfd0589901b64ad
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="re-use-ui-using-master-pages-and-partials"></a>마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 7 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 7 단계 부분 뷰 서식 파일 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하는 보기 템플릿 내에서 "건조 원칙"을 적용할 수 있습니다 하는 방법을 살펴봅니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-7-partials-and-master-pages"></a>업그레이드 되었으며 수정 단계 7: 부분 및 마스터 페이지

ASP.NET MVC 수용 디자인 이론 중 하나 (일반적으로 "드라이" 라고 함) "수행 하지 반복 직접" 원칙입니다. 건조 디자인 코드 및 빌드를 빠르고 쉽게 유지 관리 하는 응용 프로그램에 궁극적으로 낮추는 논리의 복제를 제거할 수 있습니다.

몇 가지 업그레이드 되었으며 수정 시나리오에서 적용 건조 원칙을 이미 살펴보았습니다. 몇 가지 예: 두 편집에서 강제 적용 하 고 컨트롤러; 시나리오를 만들 수 있도록 하는 모델 계층 내에서 유효성 검사 논리 구현 됩니다 편집, 세부 정보 및 Delete 동작 메서드를 통해 다시 사용 "NotFound" 보기 템플릿 규칙-명명 패턴 View() 도우미 메서드를 호출할 때 이름을 명시적으로 지정 하지 않아도 우리의 뷰 템플릿으로 사용 하 여 우리는 다시 사용 하 여 고 DinnerFormViewModel 클래스 모두 편집에 대 한 작업 시나리오를 만들 합니다.

이제 방법을 살펴보겠습니다 "건조 원칙"을 적용할 수 있습니다도 없는 코드 중복을 제거 하는 보기 템플릿 내에서.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>다시 파악 하 여 편집 및 보기 템플릿 만들기

현재 두 개의 서로 다른 뷰 템플릿 – "Edit.aspx" 및 "Create.aspx" – Dinner 폼 UI를 표시 하려면 사용 했습니다. 그중에서 빠르게 시각적 비교는 얼마나 비슷한지 강조 표시 합니다. 다음은 폼 만들기의 모양을입니다.

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

및 "편집" 폼의 모양은 다음과 같습니다.

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

큰 차이 무엇입니까? 제목 및 머리글 텍스트 이외의 폼 레이아웃 및 입력 컨트롤은 동일 합니다.

템플릿 보기 소요 됩니다 "Edit.aspx" 및 "Create.aspx"를 열고에서는 동일한 폼 레이아웃 및 입력 제어 코드를 포함 합니다. 이러한 중복 두 번 소개 우리 하거나 적합 하지 않습니다 새 Dinner 속성-변경로 인해 변경 하지 정리할 의미 합니다.

### <a name="using-partial-view-templates"></a>부분 뷰 템플릿 사용

ASP.NET MVC 페이지의 하위 부분 뷰 렌더링 논리를 캡슐화 하는 데 사용할 수 있는 "부분 뷰" 템플릿을 정의 하는 기능을 지원 합니다. 뷰 렌더링 논리를 한 번 정의 하는 유용한 방법을 제공 하 고 다시 사용 될 여러 위치에서 응용 프로그램 간에 하는 "부분".

"드라이" 우리의 Edit.aspx 및 Create.aspx 보기 템플릿 복제를 위해 폼 레이아웃 및 둘 다에 공통 되는 입력된 요소를 캡슐화 하는 "DinnerForm.ascx" 라는 부분 뷰 템플릿을 만들 수 있습니다. 우리의/뷰/Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 수행 됩니다는 "추가-&gt;보기" 메뉴 명령:

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

이 "뷰 추가" 대화 상자를 표시 됩니다. 이름을 새 보기를 만드는 "DinnerForm", "부분 뷰 만들기" 대화 상자에서 확인란을 선택 하 고는 통과 됩니다 것 DinnerFormViewModel 클래스를 나타냅니다.

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

"추가" 단추를 클릭 하면 Visual Studio에서는 us에 대 한 새 "DinnerForm.ascx" 보기 템플릿을 "\Views\Dinners" 디렉터리 내에서 만듭니다.

म 수 다음 복사/붙여넣기 중복 폼 레이아웃 / 우리의 새 "DinnerForm.ascx" 부분 뷰 템플릿으로 우리의 Edit.aspx/ Create.aspx 보기 템플릿에서 제어 코드를 입력 합니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

그런 다음이 편집 및 Create 템플릿 보기 DinnerForm 부분 서식 파일을 호출 하 고 중복 제거 하 여 폼을 업데이트할 수 있습니다. 우리의 보기 템플릿 내 Html.RenderPartial("DinnerForm") 호출 하 여 수행할 수 있습니다.

##### <a name="createaspx"></a>Create.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Html.RenderPartial를 호출할 때 원하는 부분 서식 파일의 경로 명시적으로 한정할 수 있습니다 (예: ~ Views/Dinners/DinnerForm.ascx "). 위의 코드에서 하지만 내 ASP.NET MVC에서 규칙 기반 명명 패턴을 활용 하기 위해 했으며 "DinnerForm" 렌더링할 부분 이름으로 지정 하면 됩니다. 이 작업을 수행 하는 경우 ASP.NET MVC는 검색 규칙 기반 views 디렉터리의 첫 번째 (DinnersController/뷰/Dinners 것) 합니다. 부분 서식 파일을 찾지 못하는 경우 있습니다를 다음 찾습니다 것 /Views/Shared 디렉터리에 있습니다.

Html.RenderPartial() 부분 뷰의 이름으로 호출 되 면 ASP.NET MVC에서 호출 뷰 템플릿이 사용 되는 동일한 모델 및 ViewData 사전 개체 부분 뷰로 전달 합니다. 또는 대체 모델 개체 및/또는 부분 뷰를 인덱싱하지에 대 한 사전은 전달할 수 있도록 하는 오버 로드 된 버전의 Html.RenderPartial() 됩니다. 만을 저장할 전체 모델/ViewModel의 하위 집합을 전달 하는 시나리오에 유용 합니다.

| **쪽 주제: 이유 &lt;% %&gt; 대신 &lt;% = %&gt;?** |
| --- |
| 사용 함을 위의 코드와 함께 보았을 것 미묘한 작업 중 하나는 &lt;% %&gt; 대신 차단는 &lt;% = %&gt; Html.RenderPartial()를 호출할 때 차단 합니다. &lt;% = %&gt; 블록 ASP.NET에서 개발자가 지정된 된 값을 렌더링 하려고 나타냅니다 (예: &lt;% = "Hello" %&gt; "Hello" 하 게 렌더링). &lt;% %&gt; 블록 코드를 실행 하려는 개발자 및 그 안에 포함 하는 출력을 렌더링 된 어떠한 이루어져야 합니다. 명시적으로 나타냅니다 (예: &lt;% Response.Write("Hello") %&gt;합니다. 사용 하는 이유는 &lt;% %&gt; 위의 우리의 Html.RenderPartial 코드와 함께 블록은 Html.RenderPartial() 메서드는 문자열을 반환 하 고 대신 호출 템플릿 보기에 직접 콘텐츠를 스트림의 출력을 출력 합니다. 성능상의 이유로 효율성 및 (잠재적으로 매우 큰) 임시 문자열 개체를 만들지 않아도 되므로 수행 하 여 이렇게 수행 합니다. 이 메모리 사용을 줄이고 전반적인 응용 프로그램 처리량을 향상 합니다. Html.RenderPartial()을 사용 하는 내에 없을 때 호출의 끝에 세미콜론을 추가 하는 경우 한 가지 일반적인 실수는 &lt;% %&gt; 블록입니다. 예를 들어이 코드는 컴파일러 오류 하면: &lt;% Html.RenderPartial("DinnerForm") %&gt; 작성 해야 하는 대신: &lt;%Html.RenderPartial("DinnerForm"); %&gt; 때문에 이것이 &lt;% %&gt; 블록은 자체 포함 된 코드 문을 때 및 C# 코드 문은 세미콜론으로 종료 해야 할를 사용 합니다. |

### <a name="using-partial-view-templates-to-clarify-code"></a>부분 뷰 템플릿을 사용 하 여 코드를 명확 하 게

여러 위치에서 뷰 렌더링 논리 중복 되지 않도록 하려면 "DinnerForm" 부분 뷰 템플릿을 만들었는지 여부입니다. 부분 뷰 템플릿을 만들 수는 가장 일반적인 이유입니다.

경우에 따라 여전히 이렇게 하면 부분 뷰를 한 곳에만 호출 되는 경우에 있습니다. 매우 복잡 한 뷰 템플릿 종종 뷰 렌더링 논리 추출 하 고 하나에 분할 또는 부분 서식 파일을 이름이 더 잘 읽을 하기가 훨씬 커질 수 있습니다.

예를 들어는 아래 코드 조각 (있음 살펴볼 것에 곧) 프로젝트에는 Site.master 파일에서입니다. 코드는 비교적 간단 읽을 – 로그인/로그 아웃을 표시 하는 논리를 위쪽에 링크 있기 때문에 화면 오른쪽 "LogOnUserControl" 부분 내에서 캡슐화 됩니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

혼란 사용자 자신이 때마다 템플릿 보기 내에서 태그를 html/코드를 이해, 여부 추출 되 고 잘 명명 된 부분 뷰도 리팩터링 되는데이 중 일부 하면 분명히 알 수 없게 하는 것이 좋습니다. 하려고 합니다.

### <a name="master-pages"></a>마스터 페이지

부분 뷰를 지원할 뿐 아니라 ASP.NET MVC도 일반적인 레이아웃 및 사이트의 최상위 html을 정의 하는 데 사용할 수 있는 "마스터 페이지" 템플릿을 만들 수 있는 기능을 지원 합니다. 콘텐츠 자리 표시자 컨트롤 "" 의해 채워진 뷰 또는 재정의 될 수 있는 대체 가능 영역을 식별 하는 마스터 페이지에 추가할 수 있습니다. 이 응용 프로그램에 걸쳐 공통 레이아웃을 적용 하는 매우 효과적인 (및 건조) 방법을 제공 합니다.

기본적으로 새 ASP.NET MVC 프로젝트에 자동으로 추가 하는 마스터 페이지 서식 파일을가지고 있습니다. 이 마스터 페이지에는 "Site.master" 및 생활 \Views\Shared\ 폴더 내에서 이름이 지정 됩니다.

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

기본 Site.master 파일은 아래와 같습니다. 위쪽 탐색을 위한 메뉴와 함께 사이트의 외부 html을 정의합니다. 제목, 용이고 다른 페이지의 기본 콘텐츠 바꿔야에 대 한 두 개의 대체 가능 콘텐츠 자리 표시자 컨트롤-포함 됩니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

업그레이드 되었으며 수정 응용 프로그램 ("List", "Details", "편집", "만들기", "NotFound" 등)에 대 한 만들었습니다 템플릿 보기의 모든 토대로이 Site.master 서식 파일입니다. 이 기본적으로 위쪽에 추가 된 "MasterPageFile" 특성을 통해 표시 &lt;% 페이지 % @&gt; 지시문 "뷰 추가" 대화 상자를 사용 하 여이 뷰를 만들 때:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

따라서 Site.master 콘텐츠를 변경할 수 있습니다 및가 변경 내용을 자동으로 적용 하 고 사용할 म 우리의 보기 템플릿 중 하나를 렌더링 합니다.

응용 프로그램의 머리글은 "내 MVC 응용 프로그램" 대신 "업그레이드 되었으며 수정" 되도록 우리의 Site.master 헤더 섹션을 업데이트 해 보겠습니다. 보겠습니다도 업데이트 우리의 탐색 메뉴 첫 번째 탭이 "찾을 정도 Dinner" (HomeController의 index () 동작 메서드에서 처리), 되 고 "호스트 정도 Dinner" (DinnersController의 create () 동작 메서드에서 처리) 이라고 하는 새 탭을 추가 해 보겠습니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Site.master 파일 및 새로 고침을 저장 하는 경우이 헤더를 보면 브라우저 표시 응용 프로그램 내에서 모든 뷰에 변경 합니다. 예:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

와 */Dinners/편집 / [id]* URL:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>다음 단계

부분 및 마스터 페이지 보기를 완전히 구성 수 있도록 하는 매우 유연한 옵션을 제공 합니다. 도움말 보기 중복을 피하기 위해 콘텐츠 / 코드, 고 있다고 보기 템플릿을 보다 쉽게 읽고 유지 관리할 수 있도록를 찾을 수 있습니다.

보겠습니다 이제 앞에서 만든 목록 시나리오를 다시 확인 하 고 확장 가능한 페이징 지원을 사용 하도록 설정 합니다.

>[!div class="step-by-step"]
[이전](use-viewdata-and-implement-viewmodel-classes.md)
[다음](implement-efficient-data-paging.md)
