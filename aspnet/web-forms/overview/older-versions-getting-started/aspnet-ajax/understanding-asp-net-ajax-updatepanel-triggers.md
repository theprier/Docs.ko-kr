---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: ASP.NET AJAX UpdatePanel 트리거 이해 | Microsoft Docs
author: scottcate
description: Visual Studio에서 태그 편집기를 사용할 때 표시 될 수도 있습니다 (IntelliSense)에서 UpdatePanel 컨트롤의 두 자식 요소는 합니다. 호환성이 다음 중 하나를 사용 하는 중...
ms.author: riande
ms.date: 03/12/2008
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: 9501a2e855bdffe8c9d85c0dd0d836f50935b306
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838528"
---
<a name="understanding-aspnet-ajax-updatepanel-triggers"></a>ASP.NET AJAX UpdatePanel 트리거 이해
====================
[Scott Cate](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> Visual Studio에서 태그 편집기를 사용할 때 표시 될 수도 있습니다 (IntelliSense)에서 UpdatePanel 컨트롤의 두 자식 요소는 합니다. 그 중 하나는 컨트롤의 페이지 (또는 사용자 정의 컨트롤을 하나를 사용 하는 경우)을 지정 하는 트리거 요소에는 요소가 상주 하 고 UpdatePanel 컨트롤의 부분 렌더링 트리거됩니다.


## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술을 개체 지향 및 이벤트 구동 프로그래밍 모델을 제공 및 컴파일된 코드의 이점과 결합 합니다. 그러나 해당 서버 쪽 처리 모델에는 Microsoft ASP.NET 3.5 AJAX 확장에 포함 된 새 기능을 통해 해결할 수 있으며이 중 대다수가 기술에 내재 된 몇 가지 단점이 있습니다. 이러한 확장 페이지의 부분 렌더링을 포함 하 여 전체 페이지 새로 고침 (ASP.NET 프로 파일링 API 포함), 클라이언트 스크립트 및 광범위 한 클라이언트 쪽 API를 통해 웹 서비스에 액세스 하는 기능을 요구 하지 않고 새로운 많은 리치 클라이언트 기능을 사용 하도록 설정 다양 한 ASP.NET 서버측 컨트롤 집합에서 표시 하는 컨트롤 스키마를 반영 하도록 설계 되었습니다.

이 백서에는 ASP.NET AJAX의 XML 트리거 기능 검사 `UpdatePanel` 구성 요소입니다. XML 트리거는 특정 UpdatePanel 컨트롤에 대 한 부분 렌더링을 일으킬 수 있는 구성 요소에 대 한 세부적인 제어를 제공 합니다.

이 백서는 Visual Studio 2008 및.NET framework 3.5 베타 2 릴리스를 기반으로 합니다. 이제 ASP.NET AJAX Extensions, ASP.NET 2.0을 대상으로 하는 추가 기능 어셈블리 이전에.NET Framework 기본 클래스 라이브러리에 통합 되었습니다. 이 백서도 가정 하지 Visual Web Developer Express를 Visual Studio 2008을 사용 하 여 작업 (코드 목록에 관계 없이 완전히 호환 됩니다. 하지만 Visual Studio의 사용자 인터페이스에 따라 연습을 제공 합니다. 개발 환경)입니다.

## <a name="triggers"></a>*트리거*

기본적으로 지정 된 UpdatePanel에 대 한 트리거가 포함 된 TextBox 컨트롤 (예) 포스트백을 호출 하는 모든 자식 컨트롤을 자동으로 포함 자신의 `AutoPostBack` 속성으로 설정 **true**합니다. 그러나 트리거 포함 될 수 있습니다; 태그를 사용 하 여 선언적인 내에서 이렇게는 `<triggers>` UpdatePanel 컨트롤 선언의 섹션입니다. 트리거를 통해 액세스할 수 있지만 합니다 `Triggers` 컬렉션 속성을 것이 좋습니다 (예를 들어, 컨트롤을 사용할 수 없는 경우 디자인 타임) 런타임 시 모든 부분 렌더링 트리거를 등록 하는 사용 하 여를 `RegisterAsyncPostBackControl(Control)` 메서드는 ScriptManager 내 페이지에 대 한 개체는 `Page_Load` 이벤트입니다. 페이지는 상태 비저장 이므로 다시 등록 해야 이러한 컨트롤 만들어질 때마다 기억 하세요.

자동 자식 트리거 포함도 해제할 수 있습니다 (있도록 다시 게시를 만든 자식 컨트롤이 자동으로 부분 렌더링을 트리거하지 않음)을 설정 하 여 합니다 `ChildrenAsTriggers` 속성을 **false**합니다. 이렇게 하면 되도록 개발자가 옵트인 발생할 수 있는 모든 이벤트를 처리 하는 것이 아니라 이벤트에 응답할 특정 컨트롤 할당에 최대한의 유연성을 페이지 렌더링을 호출할 수 있습니다 및 권장 있습니다.

UpdatePanel 컨트롤은 중첩 된 경우 경우는 UpdateMode로 설정 되어 있는지 확인 **조건부**이면 자식 UpdatePanel 트리거될 아닌 부모를 다음 자식 UpdatePanel 새로 고쳐집니다. 그러나 부모 UpdatePanel 새로 고칠 경우 다음 자식 UpdatePanel도 고쳐집니다.

## <a name="the-lttriggersgt-element"></a>*합니다 &lt;트리거&gt; 요소*

Visual Studio에서 태그 편집기를 사용할 때 표시 될 수도 있습니다 (IntelliSense)에서 두 개의 자식 요소는의 `UpdatePanel` 제어 합니다. 가장 자주 나타나는 요소는는 `<ContentTemplate>` 기본적으로 updatepanel에서 보유 하는 콘텐츠를 캡슐화 하는 요소 (부분 렌더링에서는 사용 콘텐츠). 다른 요소는 합니다 `<Triggers>` 페이지 (또는 사용자 정의 컨트롤을 하나를 사용 하는 경우)에 있는 컨트롤을 지정 하는 요소는 UpdatePanel 컨트롤의 부분 렌더링을 트리거하는 합니다 &lt;트리거&gt; 요소가 상주 하 합니다.

합니다 `<Triggers>` 요소에는 임의 개수의 각 두 개의 자식 노드가 포함 될 수 있습니다: `<asp:AsyncPostBackTrigger>` 및 `<asp:PostBackTrigger>`합니다. 두 가지 특성을 모두 수락 `ControlID` 및 `EventName`, 캡슐화의 현재 단위 내에서 모든 컨트롤을 지정할 수 (예를 들어 UpdatePanel 컨트롤에 웹 사용자 컨트롤에 있는 경우 하지 않아야에 컨트롤 참조 페이지는 사용자 정의 컨트롤 상주할)입니다.

합니다 `<asp:AsyncPostBackTrigger>` 요소는 자식으로 있는 컨트롤에서 모든 이벤트를 대상 수에 특히 유용 *모든* 캡슐화는이 트리거는 자식 뿐 아니라 UpdatePanel의 단위로 UpdatePanel 컨트롤 . 따라서 부분 페이지 업데이트를 트리거하도록 모든 컨트롤을 만들 수 있습니다.

마찬가지로,는 `<asp:PostBackTrigger>` 트리거 부분 페이지 렌더링 하지만 서버에 대 한 전체 왕복을 요구 하는 요소를 사용할 수 있습니다. 컨트롤 그렇지 않은 경우 일반적으로 트리거할 부분 페이지 렌더링 될 때 전체 페이지 렌더링을 강제로 실행 하려면이 트리거 요소를 사용할 수도 있습니다 (경우에 예를 들어, 한 `Button` 컨트롤에 있는 `<ContentTemplate>` UpdatePanel 컨트롤의 요소). 마찬가지로 PostBackTrigger 요소 캡슐화의 현재 단위로 UpdatePanel 컨트롤의 자식 컨트롤을 지정할 수 있습니다.

## <a name="lttriggersgt-element-reference"></a>*&lt;트리거&gt; 요소 참조*

*태그 하위 항목:*

| **태그** | **설명** |
| --- | --- |
| &lt;asp:AsyncPostBackTrigger&gt; | 컨트롤과이 트리거 참조를 포함 하는 UpdatePanel에 대 한 부분 페이지 업데이트를 발생 시키는 이벤트를 지정 합니다. |
| &lt;asp:PostBackTrigger&gt; | 컨트롤 및 전체 페이지 업데이트 (전체 페이지 새로 고침)를 일으키는 이벤트를 지정 합니다. 부분 렌더링 컨트롤을 트리거할 수이 고, 그렇지 때 전체 새로 고침을 강제로 하려면이 태그를 사용할 수 있습니다. |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*연습: 간 UpdatePanel 트리거*

1. 부분 렌더링을 사용 하도록 설정 하는 ScriptManager 개체를 사용 하 여 새 ASP.NET 페이지를 만듭니다. 두 Updatepanel이이 페이지에 추가-첫 번째에서 Label 컨트롤 (레이블 1) 및 두 개의 단추 컨트롤 (Button1 및 Button2)를 포함 합니다. Button1 둘 다를 업데이트 하려면 클릭 나타나야 합니다. 그리고 Button2 해야이 또는 줄을 업데이트 하려면 클릭 합니다. 두 번째 UpdatePanel의 Label 컨트롤 (Label2)만 포함 하지만 전경색 속성을 구분 하기 위해 기본값이 아닌 값으로 설정 합니다.
2. 두 UpdatePanel 태그의 UpdateMode 속성을 설정 **조건부**합니다.

**Default.aspx에 대 한 목록 1: 태그:** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. Button1에 대 한 클릭 이벤트 처리기에서 Label1.Text 및 Label2.Text 값으로 설정 (예: DateTime.Now.ToLongTimeString()) 종속 되는 시간. Button2에 대 한 클릭 이벤트 처리기에 대 한만 Label1.Text 시간 종속 값으로 설정 합니다.

**목록 2 코드 숨김 default.aspx.cs의 (잘립니다).:** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. F5 키를 눌러 프로젝트를 빌드하고 실행 합니다. 모두 패널 업데이트를 클릭 하면 두 레이블 텍스트입니다;이 변경 그러나이 패널 업데이트를 클릭 하면 Label1만 업데이트 합니다.


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png))


## <a name="under-the-hood"></a>*내부 살펴보기*

이 예제에서는 방금 구성한를 활용 하는 UpdatePanel 간 패널 트리거 작동 하는 방법 및 ASP.NET AJAX 수행 하는 취할 수 있습니다. 이렇게 하려면, FireBug-이라고 하는 Mozilla Firefox 확장 뿐만 아니라 생성 된 페이지의 HTML 소스 노력할 AJAX 포스트백을 쉽게 검사할 수 했습니다. 또한 Lutz Roeder의.NET Reflector 도구를 사용 합니다. 두이 도구를 무료로 사용할 수 있는 온라인 되며 인터넷 검색을 사용 하 여 확인할 수 있습니다.

페이지 소스 검사를 보여 줍니다 거의 특이; UpdatePanel 컨트롤은으로 렌더링 됩니다 `<div>` 컨테이너를 볼 수 있습니다 제공 스크립트 리소스를 포함 하 여는 `<asp:ScriptManager>`. 내부 AJAX 클라이언트 스크립트 라이브러리에 있는 PageRequestManager에 몇 가지 새로운 AJAX 전용 호출도 있습니다. 마지막으로 렌더링 된 개 두 UpdatePanel 컨테이너-표시 `<input>` 두 개의 단추 `<asp:Label>` 컨트롤 렌더링 `<span>` 컨테이너입니다. (FireBug에서 DOM 트리를 검사 하는 경우 표시 됩니다는 레이블이 표시 되는 콘텐츠의 생성 하지는 나타내려면 흐리게 표시 됩니다).

이 패널 업데이트 단추를 클릭 상위 UpdatePanel 현재의 서버 시간으로 업데이트 됩니다. FireBug에서 요청을 검사할 수 있도록 콘솔 탭을 선택 합니다. POST 요청 매개 변수를 먼저 검토:


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png))


UpdatePanel에 표시 된 서버 쪽 AJAX 코드 ScriptManager1 매개 변수를 통해 컨트롤 트리 정확 하 게 발생 하는 참고: `Button1` 의 `UpdatePanel1` 제어 합니다. 이제 모두 패널 업데이트 단추를 클릭 합니다. 그런 다음 응답을 검사할 것을 볼 파이프로 구분 된 일련의 문자열을 설정 하는 변수 상위 UpdatePanel 볼 특히 `UpdatePanel1`를 브라우저로 전송 되는 해당 HTML 전체에 있습니다. UpdatePanel의 원래 HTML 콘텐츠를 통해 새 콘텐츠로 대체 하는 AJAX 클라이언트 스크립트 라이브러리는 `.innerHTML` 속성 이므로 서버는 HTML로 서버에서 변경 된 내용을 보냅니다.

이제 모두 패널 업데이트 단추를 클릭 하 고 서버에서 결과 검사 합니다. 결과 매우 유사-두 Updatepanel 서버에서 새 HTML을 수신 합니다. 이전 콜백 마찬가지로 추가 페이지 상태 전송 됩니다.

볼 수 있듯이, 특수 코드 없이 AJAX 포스트백을 수행 하는 데 사용 하기 때문에, AJAX 클라이언트 스크립트 라이브러리는 추가 코드 없이 폼 포스트백을 가로챌 수 있습니다. 서버 컨트롤은 자동으로 JavaScript를 사용 하는 자동으로 폼을 제출 하지 않는-주로 자동 스크립트 리소스 포함, PostBackOptions 클래스 (l2tp) 양식 유효성 검사 및 이미 상태에 대 한 코드를 자동으로 삽입 하는 ASP.NET 및 ClientScriptManager 클래스입니다.

예를 들어 CheckBox 컨트롤을; 것이 좋습니다. .NET Reflector의 클래스 디스어셈블리를 검사 합니다. 이렇게 하려면 System.Web 어셈블리 열려 있는지 확인 하 고 이동 합니다 `System.Web.UI.WebControls.CheckBox` 클래스를 열고는 `RenderInputTag` 메서드. 확인 하는 조건부 찾습니다는 `AutoPostBack` 속성:


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png))


자동 포스트백에서 사용 되는 경우는 `CheckBox` 결과 (true AutoPostBack 속성)를 통해 제어할 `<input>` ASP.NET 이벤트 처리에서 스크립트를 사용 하 여는 태그를 렌더링 하므로 해당 `onclick` 특성입니다. 그런 다음 폼의 제출, 인터 셉 션의 주요 변경 내용 수 있습니다 정확 하지 않은 문자열 대체를 활용 하 여 발생할 수 있는 모든 가능성을 방지 하는 데 nonintrusively, 페이지에 주입 하려는 ASP.NET AJAX를 수 있습니다. 또한이 통해 *모든* 사용자 지정 ASP.NET 컨트롤을 UpdatePanel 컨테이너 내에서 해당 사용을 지원 하려면 추가 코드 없이 ASP.NET AJAX의 기능을 활용 합니다.

합니다 `<triggers>` PageRequestManager 호출에서 초기화 되는 값에 해당 하는 기능 \_updateControls (참고는 ASP.NET AJAX 클라이언트 스크립트 라이브러리는 메서드, 이벤트 및 필드 이름을 시작 하는 규칙을 사용 하는 밑줄은 내부로 표시 되지 않으며 라이브러리 자체 외부에서 사용할). 사용 하 여 제어 하는 AJAX 포스트백을 발생 하는 것 관찰할 수 있습니다.

예를 들어 Updatepanel 외부 컨트롤을 완전히 종료 하 고 UpdatePanel 내에서 하나를 그대로 두고 페이지로 추가 두 개의 추가 컨트롤이 해 보겠습니다. 위 UpdatePanel 내에서 확인란 컨트롤을 추가 하 고 목록 내에서 정의 된 색의 수를 사용 하 여 DropDownList를 삭제 합니다. 새 태그는 다음과 같습니다.

**새 태그 코드 3:**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

및 새 코드 숨김은 다음과 같습니다.

**코드 4: 코드 숨김**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

이 페이지의 기본 개념 드롭다운 목록 두 번째 레이블을 표시 하려면 세 가지 색 중 하나를 선택 하, 확인란 굵게, 인지 및 레이블의 시간 뿐만 아니라 날짜를 표시 하는지 여부를 확인 하는 경우 확인란 AJAX 업데이트 발생 하지 않아야 하지만 UpdatePanel 내에 상주 하지는 경우에 드롭다운 목록 해야 합니다.


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png))


위의 스크린샷에서 명백한 경우 가장 최근의 단추를 클릭 한 오른쪽 단추를 아래쪽에 위쪽 시간에 관계 없이 업데이트는 업데이트가 패널 했습니다. 또한이 날짜를 날짜 아래쪽 레이블에 표시 되는 번의 클릭 만으로 간에 전환 됩니다. 마지막으로 관심은 맨 아래 레이블의 색: 컨트롤 상태는 중요 하는 방법을 보여 줍니다, 레이블의 텍스트 보다 더 최근에 업데이트 된 및 사용자 기대 AJAX 포스트백을 통해 유지 되도록 합니다. *그러나*, 시간 업데이트 되지 않았습니다. 시간을의 지 속성을 통해 자동으로 다시 채워야 합니다 \_ \_컨트롤이 서버에 다시 렌더링 되는 경우 ASP.NET 런타임에 의해 해석 되 고 페이지의 VIEWSTATE 필드입니다. ASP.NET AJAX 서버 코드를 인식 하지 못하는 컨트롤 메서드는 상태 변경 뷰 상태에서 단순히 다시 채웁니다 하 고 적절 한 이벤트를 실행 합니다.

그러나이 점을 지적 합니다는 I 초기화 페이지 내에\_Load 이벤트에 있는 증가 올바르게 합니다. 따라서 개발자는 해당 코드는 적절 한 이벤트 처리기 중 실행 되 고 있는 주의 있고 페이지의 사용을 방지\_컨트롤 이벤트 처리기를 적절 한 경우 로드 합니다.

## <a name="summary"></a>요약

ASP.NET AJAX 확장 UpdatePanel 컨트롤은 다양 한 이며 다양 한 방법 업데이트 하면 해야 하는 컨트롤 이벤트를 식별 하는 데 활용할 수 있습니다. 해당 자식 컨트롤에 자동으로 업데이트 되 고 지원 있지만 다른 곳에서 페이지의 컨트롤 이벤트에 응답할 수도 있습니다.

서버 처리 부하에 대 한 가능성을 줄이기 위해 것이 좋습니다 합니다 `ChildrenAsTriggers` UpdatePanel의 속성 설정할 `false`, 옵트인에 기본적으로 포함 되지 않고 이벤트 수입니다. 또한 이렇게 하면 불필요 한 이벤트 유효성 검사 및 변경 내용을 입력 필드를 포함 하 여 잠재적으로 원치 않는 효과 때문입니다. 이러한 유형의 버그는 페이지를 사용자에 게 투명 하 게 업데이트 이므로 원인을 따라서 명확 하지 않을 즉시을 격리 하기 어려울 수 있습니다.

ASP.NET AJAX 폼의 내부 작업을 검사 하 여 인터 셉 션 모델을 게시, ASP.NET에서 이미 제공 하는 프레임 워크를 활용 하는 것을 결정할 수 있었습니다. 이 과정에서 동일한 프레임 워크를 사용 하 여 디자인 된 컨트롤을 사용 하 여 최대 호환성을 유지 하 고 페이지 용으로 작성 된 추가 JavaScript에서 최소가 개입 합니다.

## <a name="bio"></a>사용자 정보

Rob Paveza Terralever의 선임.NET 응용 프로그램 개발자가 ([www.terralever.com](http://www.terralever.com)), 템피 소재를 AZ.에서 대화형 마케팅 기관인 연락할 수 있습니다 [ robpaveza@gmail.com ](mailto:robpaveza@gmail.com)에 있는 저자의 블로그 이며 [ http://geekswithblogs.net/robp/ ](http://geekswithblogs.net/robp/)합니다.

Scott Cate 1997 년부터 Microsoft 웹 기술을 사용 하 여 왔습니다 이며 myKB.com의 대표이사로 서 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 전문적 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott 전자 메일을 통해 연락할 수 있습니다 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 저자의 블로그 또는 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [이전](understanding-partial-page-updates-with-asp-net-ajax.md)
> [다음](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
