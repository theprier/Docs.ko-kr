---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 마스터 페이지 | Microsoft Docs
author: microsoft
description: 성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나에 일관 된 모양과 느낌입니다. ASP.NET에서 1.x 개발자는 일반적인 페이지 소형 복제 하기 위해 사용자 정의 컨트롤을 사용...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: f45dd9704f665244d2a48ec000326f6e98984e4f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="master-pages"></a>마스터 페이지
====================
by [Microsoft](https://github.com/microsoft)

> 성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나에 일관 된 모양과 느낌입니다. ASP.NET에서 1.x 개발자는 웹 응용 프로그램에서 일반 페이지 요소를 복제 하기 위해 사용자 정의 컨트롤을 사용 합니다. 확실히 처리 가능한 여러 솔루션 사용 되 고 있지만, 사용자 정의 컨트롤을 사용 하 여 일부의 단점이 있습니다. 예를 들어, 사용자 정의 컨트롤의 위치는 변경 사이트 전체에서 여러 페이지에 대 한 변경이 필요합니다. 사용자 정의 컨트롤은 또한 페이지에 삽입 되 고 후 디자인 보기에서 렌더링 되지 않습니다.


성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나에 일관 된 모양과 느낌입니다. ASP.NET에서 1.x 개발자는 웹 응용 프로그램에서 일반 페이지 요소를 복제 하기 위해 사용자 정의 컨트롤을 사용 합니다. 확실히 처리 가능한 여러 솔루션 사용 되 고 있지만, 사용자 정의 컨트롤을 사용 하 여 일부의 단점이 있습니다. 예를 들어, 사용자 정의 컨트롤의 위치는 변경 사이트 전체에서 여러 페이지에 대 한 변경이 필요합니다. 사용자 정의 컨트롤은 또한 페이지에 삽입 되 고 후 디자인 보기에서 렌더링 되지 않습니다.

ASP.NET 2.0 소개 마스터 페이지 일관 된 모양 및 느낌을 유지 관리 하는 방법으로 및 때 보시, 마스터 페이지 사용자 지정 컨트롤 메서드를 통해 훨씬 향상 된 기능을 나타냅니다.

## <a name="why-master-pages"></a>이유 마스터 페이지?

마스터 페이지가 ASP.NET 2.0에서 필요한 이유 할까요? 즉, 웹 사이트 개발자가 이미 사용 하는 사용자 정의 컨트롤 ASP.NET에서 1.x를 콘텐츠 영역 페이지 간에 공유 합니다. 사용자 정의 컨트롤의 일반적인 레이아웃을 만들기 위한 작음 보다 최적의 솔루션은 이유는 실제로 몇 가지 이유가 있습니다.

실제로 사용자 정의 컨트롤 페이지 레이아웃을 정의 하지 않습니다. 대신, 레이아웃 및 기능 페이지의 부분을 정의합니다. 사용자 제어 솔루션의 관리를 하기가 훨씬 더 어려워지므로 만들므로이 두 구분이 중요 합니다. 예를 들어 페이지에서 사용자 정의 컨트롤의 위치를 변경 하려는 경우 사용자 정의 컨트롤이 표시 되는 실제 페이지를 편집 해야 합니다. Thats 일부 페이지만 있지만 대규모 사이트에서 확장 되는 사이트 관리 밋 미세!

사용자 정의 컨트롤을 사용 하 여 일반적인 레이아웃을 정의 하기 위한 또 다른 단점은 작성과 자체 ASP.NET의 아키텍처. 사용자 정의 컨트롤의 모든 public 멤버를 변경 하는 경우 모든 사용자 정의 컨트롤을 사용 하는 페이지를 다시 컴파일할 수 필요 합니다. 차례로 ASP.NET 다시 JIT 컴파일하는 처음 때 페이지에 액세스 한 다음 됩니다. 이 다시 한 번, 확장 불가능 아키텍처 및 대규모 사이트에 대 한 사이트 관리 문제를 생성합니다.

이러한 문제 (및 더 많은) 둘 다 ASP.NET 2.0의 마스터 페이지로 주소가 지정 원활 하 게 됩니다.

## <a name="how-master-pages-work"></a>마스터 페이지의 작동 방식

마스터 페이지는 다른 페이지에 대 한 템플릿을 같습니다. 페이지 요소 (예: 메뉴, 테두리, 등)에 다른 페이지 간에 공유 해야 하는 마스터 페이지에 추가 됩니다. 새 페이지는 사이트에 추가 되 면 마스터 페이지와 연결할 수 있습니다. 마스터 페이지와 연결 된 페이지 라고는 **콘텐츠 페이지**합니다. 기본적으로 콘텐츠 페이지의 마스터 페이지에서 모양에 적용 됩니다. 그러나 마스터 페이지를 만들 때 콘텐츠 페이지 자체 내용으로 대체할 수 있는 페이지의 일부를 정의할 수 있습니다. ASP.NET 2.0;에 도입 된 새 컨트롤을 사용 하 여 이러한 부분 정의 **ContentPlaceHolder** 제어 합니다.

마스터 페이지에 임의 개수의 ContentPlaceHolder 컨트롤 (또는 전혀 나타나지 않습니다.)이 포함 될 수 있습니다. 콘텐츠 페이지에서 ContentPlaceHolder 컨트롤의 콘텐츠 안에 나타납니다 **콘텐츠** 컨트롤, ASP.NET 2.0의 다른 새 컨트롤입니다. 기본적으로 직접 콘텐츠를 제공할 수 있도록 콘텐츠를 제어 하는 콘텐츠 페이지는 비어 있습니다. 콘텐츠 컨트롤 안의 마스터 페이지에서 콘텐츠를 사용 하려는 경우 수행할 수 있습니다 때마다이 모듈의 뒷부분에 표시 됩니다. 콘텐츠 컨트롤은 콘텐츠 컨트롤의 ContentPlaceHolderID 특성을 통해 ContentPlaceHolder 컨트롤에 매핑됩니다. 지도 아래 코드는 콘텐츠 ContentPlaceHolder 컨트롤을 mainBody 마스터 페이지를 제어 합니다.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 다른 페이지에 대 한 기본 클래스에 있는 것으로 마스터 페이지에 설명 하는 사용자를 종종 들립니다. Thats 실제로 그렇지 않습니다. 마스터 페이지 및 콘텐츠 페이지 간에 관계 상속의 하나가 아닙니다.


**그림 1** 마스터 페이지와 연결 된 콘텐츠 페이지는 Visual Studio 2005에 나타나는 순서 대로 보여 줍니다. 마스터 페이지 및 해당 ContentPlaceHolder 컨트롤을 볼 수 콘텐츠 페이지에서 컨트롤의 콘텐츠입니다. ContentPlaceHolder는 밖에 있는 마스터 페이지 콘텐츠 표시 되기는 하지만 콘텐츠 페이지에서 흐리게 표시 됩니다. ContentPlaceHolder는 내부 콘텐츠만 콘텐츠 페이지에서 supplanted 될 수 있습니다. 마스터 페이지에서 제공 되는 모든 콘텐츠를 변경할 수 없습니다.


![마스터 페이지와 연결 된 해당 콘텐츠 페이지](master-pages/_static/image1.jpg)

**그림 1**: 마스터 페이지와 연결 된 해당 콘텐츠 페이지


## <a name="creating-a-master-page"></a>마스터 페이지 만들기

마스터 페이지를 새로 만들려면:

1. Visual Studio 2005를 열고 새 웹 사이트를 만듭니다.
2. 파일을 새 파일을 클릭 합니다.
3. 에 표시 된 대로 마스터 파일을 새 항목 추가 대화 상자에서 선택 **그림 2**합니다.
4. 추가 클릭 합니다.


![새 마스터 페이지 만들기](master-pages/_static/image2.jpg)

**그림 2**: 새 마스터 페이지 만들기


마스터 페이지에 대 한 파일 확장명은 <em>.master</em>합니다. 일반 페이지에서 마스터 페이지와 다른 방법 중 하나입니다. 다른 주요 차이점은 대신 하는 @Page 지시문, 마스터 페이지에는 @Master 지시문입니다. 방금 만든 및 코드 검토 페이지는 마스터에 대 한 소스 보기로 전환 합니다.

새 마스터 페이지에는 기본적으로 하나의 ContentPlaceHolder 권한을 갖게 됩니다. 대부분의 경우는 것이를 일반적인 페이지 요소를 먼저 만들고 ContentPlaceHolder 컨트롤을 삽입 한 다음 사용자 지정 콘텐츠를 원할 경우. 이 경우 개발자가 기본 ContentPlaceHolder 컨트롤을 삭제 하 고 페이지도 개발 된 대로 새 레코드를 삽입 하려고 합니다. ContentPlaceHolder 컨트롤은 크기 조정 핸들을 표시 않는지도 크기를 조정할 수 없습니다. 한 가지 예외로; 포함 된 내용에 따라 자동으로 ContentPlaceHolder 컨트롤 크기 예: 표 셀 블록 요소 안에 ContentPlaceHolder 컨트롤을 추가 하면 그 요소의 크기에 따라 크기 됩니다.

## <a name="lab-1-working-with-master-pages"></a>랩 1 마스터 페이지 사용

이 랩에서 마스터 페이지를 새로 만들고 세 개의 ContentPlaceHolder 컨트롤을 정의 합니다. 그런 다음 새 콘텐츠 페이지를 만들고 쿼리하고 ContentPlaceHolder 컨트롤 중 하나 이상에서 콘텐츠를 대체 합니다.

1. 마스터 페이지를 만들고 ContentPlaceHolder 컨트롤을 삽입 합니다. 

    1. 위에 설명 된 대로 새 마스터 페이지를 만듭니다.
    2. 기본 ContentPlaceHolder 컨트롤을 삭제 합니다.
    3. 컨트롤의 위쪽 회색된 테두리를 클릭 하 여 ContentPlaceHolder 컨트롤을 선택한 다음 키보드에서 DEL 키를 클릭 하 여 삭제 합니다.
    4. 사용 하 여 새 테이블을 삽입의 *헤더 편인* 그림 3에에서 표시 된 것 처럼 템플릿. 전체 테이블 디자이너에서 볼 수 있도록을 90%의 너비와 높이 변경 합니다.


![](master-pages/_static/image3.jpg)

**그림 3**


1. 테이블의 각 셀에 커서를 놓고 설정는 *valign* 속성을 *top*합니다.
2. 도구 상자에서 ContentPlaceHolder 컨트롤 테이블 (머리글 셀.)의 맨 위 셀 삽입
3. 이 ContentPlaceHolder 컨트롤을 삽입 하는 경우에 행 높이 차지 하는 거의 전체 페이지 그림 4에에서 나와 있는 것 처럼 확인할 수 있습니다. 금지 관여 하는 시점에서.


![빈 공간은 ContentPlaceHolder로 동일한 셀](master-pages/_static/image1.gif)

**그림 4**: 빈 공간은 ContentPlaceHolder로 동일한 셀


1. 다른 두 셀에서 ContentPlaceHolder 컨트롤을 배치 합니다. 다른 ContentPlaceHolder 컨트롤이 삽입 되 면 테이블 셀의 크기를 예상 해야 합니다. 이제 페이지에 표시 된 페이지 같은 모양이 **그림 5**합니다.


![모든 ContentPlaceHolder 컨트롤과 마스터입니다. 머리글 셀에 대 한 셀 높이 이제가 원래 표시 되어야](master-pages/_static/image2.gif)

**그림 5**: 모든 ContentPlaceHolder 컨트롤과 The 마스터 합니다. 머리글 셀에 대 한 셀 높이 이제가 원래 표시 되어야


1. 각각의 세 가지 ContentPlaceHolder 컨트롤에 사용자가 선택한 텍스트를 입력 합니다.
2. Exercise1.master로 마스터 페이지를 저장 합니다.
3. 새 Web Form을 만들고 exercise1.master 마스터 페이지와 연결 합니다.
4. Visual Studio 2005에서 파일을 새 파일을 선택.
5. 선택 **Web Form** 새 항목 추가 대화 상자에서.
6. 그림 6에에서 나와 있는 것 처럼에서 마스터 페이지 선택 확인란을 선택 하 고 있는지 확인 합니다.


![새 콘텐츠 페이지를 추가합니다.](master-pages/_static/image3.gif)

**그림 6**: 새 콘텐츠 페이지를 추가 합니다.


1. 추가 클릭 합니다.
2. Exercise1.master 선택에서 마스터 페이지 대화 상자에에서 표시 된 선택 그림 7입니다.
3. 새 콘텐츠 페이지를 추가 하려면 확인을 클릭 합니다.

새 콘텐츠 페이지는 마스터 페이지에 있는 각 ContentPlaceHolder 컨트롤에 대 한 하나의 콘텐츠 컨트롤과 Visual Studio에 표시 됩니다. 기본적으로 콘텐츠 컨트롤 내용을 직접 추가할 수 있도록 비어 있습니다. Youd 마음에 마스터 페이지에서 ContentPlaceHolder 컨트롤에서 콘텐츠를 사용 하지 않으면 하기만 하면 스마트 태그 기호 (컨트롤의 오른쪽 위 모서리에 작은 검은색 화살표)를 클릭 하 고 선택 *마스터 콘텐츠 기본값* 와 같이 스마트 태그에서 **그림 8**합니다. 이렇게 하면 메뉴 항목을 변경 *사용자 지정 콘텐츠 만들기*합니다. 시점 클릭 하면 해당 특정 콘텐츠 컨트롤에 대 한 사용자 지정 콘텐츠를 정의할 수 있도록 마스터 페이지에서 콘텐츠를 제거 합니다.


![콘텐츠 컨트롤을 마스터 페이지 콘텐츠를 기본값으로 설정](master-pages/_static/image4.gif)

**그림 7**: 콘텐츠 컨트롤에 마스터 페이지 콘텐츠를 기본값으로 설정


## <a name="connecting-master-page-and-content-pages"></a>마스터 페이지 및 콘텐츠 페이지에 연결

네 가지 방법 중 하나에서 마스터 페이지 콘텐츠 페이지와의 연결을 구성할 수 있습니다.

- <strong>MasterPageFile</strong> 특성에는 @Page 지시문
- 설정의 **Page.MasterPageFile** 코드에서 속성입니다.
- **&lt;페이지&gt;** 응용 프로그램 구성 파일 (응용 프로그램의 루트 폴더에 web.config)의 요소
- **&lt;페이지&gt;** 하위 폴더 구성 파일 (하위 폴더에 web.config)의 요소

## <a name="masterpagefile-attribute"></a>MasterPageFile 특성

MasterPageFile 특성을 사용 하면 쉽게 특정 ASP.NET 페이지에 마스터 페이지를 적용할 수 있습니다. 마스터 페이지를 검사할 때 적용 하는 데 사용 하는 방법 이기도 **마스터 페이지 선택** 실습 1에서 수행한 때 확인란을 선택 합니다.

## <a name="setting-pagemasterpagefile-in-code"></a>코드에서 Page.MasterPageFile 설정

코드에서 MasterPageFile 속성을 설정 하 여 특정 마스터 페이지를 런타임에 콘텐츠에 적용할 수 있습니다. 사용자가 역할 또는 기타 일부 조건에 따라 특정 마스터 페이지를 적용 해야 하는 경우에 유용 합니다. MasterPageFile 속성 PreInit 메서드에서 설정 되어야 합니다. PreInit 메서드 다음으로 설정 하는 InvalidOperationException throw 됩니다. 이 속성을 설정 하는 페이지 콘텐츠 있어야 페이지에 대 한 최상위 컨트롤로 제어 합니다. 그렇지 않은 경우는 HttpException MasterPageFile 속성이 설정 된 경우 throw 됩니다.

## <a name="using-the-ltpagesgt-element"></a>사용 하 여 &lt;페이지&gt; 요소

masterPageFile 특성을 설정 하 여 페이지에 대 한 마스터 페이지를 구성할 수 있습니다는 &lt;페이지&gt; web.config 파일의 요소입니다. 이 메서드를 사용 하면 응용 프로그램 구조에서 하위 web.config 파일에이 설정을 재정의할 수를 염두에서에 둬야 합니다. 모든 MasterPageFile 속성 세트는 @Page 지시문이이 설정을 재정의 합니다. 사용 하는 &lt;페이지&gt; 요소를 사용 하면 간단 하 게 만들 수는 <em>마스터</em> 특정 폴더 또는 파일에 필요한 경우 재정의할 수 있는 마스터 페이지입니다.

## <a name="properties-in-master-pages"></a>마스터 페이지에서 속성

마스터 페이지 하기만 하면 이러한 속성 마스터 페이지 내에서 public 속성을 노출할 수 있습니다. 예를 들어 다음 코드는 SomeProperty 라는 속성을 정의 합니다.

[!code-csharp[Main](master-pages/samples/sample2.cs)]

콘텐츠 페이지의 SomeProperty 속성에 액세스 하려면 Master를 사용 해야 합니다 같이 속성:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>중첩 마스터 페이지

마스터 페이지는 대형 웹 응용 프로그램에서 공통 된 모양 및 느낌을 위한 완벽 한 솔루션입니다. 그러나 다른 파트는 다른 인터페이스를 공유 하는 동안 큰 사이트 공유 공통 인터페이스의 특정 부분에 있는 것 도지 않습니다. 해당 요구를 해결 하기 위해 다중 마스터 페이지는 완벽 한 솔루션입니다. 그러나 해당 여전히 사이트의 특정 섹션만 간에 공유 되는 다른 구성 요소 및 특정 구성 요소 (예: 메뉴, 예를 들어) 모든 페이지 간에 공유 되는 대형 응용 프로그램에 있을 수 있다는 사실을 해결 되지 않습니다. 해당 유형의 상황에 대 한 중첩 된 마스터 페이지의 필요성을 원활 하 게 채웁니다. 앞서 살펴본 것 처럼 표준 마스터 페이지 마스터 페이지 및 콘텐츠 페이지 이루어져 있습니다. 중첩 된 마스터 페이지를 사용 하는 경우에는 두 개의 마스터 페이지; 부모 마스터 및 하위 마스터 합니다. 자식 마스터 페이지 콘텐츠 페이지 진행 되며 해당 마스터 부모 마스터 페이지입니다.

일반적인 마스터 페이지에 대 한 코드는 다음과 같습니다.

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

중첩된 된 마스터 시나리오에서 부모 마스터가 됩니다. 다른 마스터 페이지는 마스터 페이지의으로이 페이지를 사용 하 고 해당 코드는 다음과 같습니다.

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

이 시나리오를 자식 마스터 부모 마스터에 대 한 콘텐츠 페이지 이기도 합니다. 모든 자식 마스터 콘텐츠 부모의 ContentPlaceHolder 컨트롤에서 해당 콘텐츠를 가져오는 콘텐츠 컨트롤 안에 표시 합니다.

> [!NOTE]
> 중첩 된 마스터 페이지에 대 한 디자이너 지원을 ´ ù. 중첩 된 마스터를 사용 하 여를 개발 하는 경우 소스 뷰를 사용 해야 합니다.


이 비디오에서는 중첩 된 마스터 페이지를 사용 하 여 보여 주는 연습을 보여 줍니다.


![](master-pages/_static/image1.png)


[전체 화면 비디오 열기](master-pages/_static/nested1.wmv)


![마스터 페이지를 선택합니다.](master-pages/_static/image4.jpg)

**그림 8**: 마스터 페이지를 선택 합니다.
