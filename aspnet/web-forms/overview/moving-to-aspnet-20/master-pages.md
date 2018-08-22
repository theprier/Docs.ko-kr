---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 마스터 페이지 | Microsoft Docs
author: microsoft
description: 성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나는 일관 된 모양과 느낌입니다. Asp.net에서 1.x에서 개발자는 일반적인 페이지 소형을 복제 하기 위해 사용자 정의 컨트롤을 사용...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: f40eb338a1b6b8eebb6578dd7938e96a05b1617f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829749"
---
<a name="master-pages"></a>마스터 페이지
====================
[Microsoft](https://github.com/microsoft)

> 성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나는 일관 된 모양과 느낌입니다. Asp.net에서 1.x에서 개발자는 웹 응용 프로그램에서 일반적인 페이지 요소를 복제할 사용자 정의 컨트롤을 사용 합니다. 확실히 작동 가능한 솔루션을 사용 되 고 있지만, 사용자 컨트롤을 사용 하는 몇 가지 단점이 있습니다. 예를 들어, 사용자 정의 컨트롤의 위치 변경 사이트 전체에서 여러 페이지에 대 한 변경에 필요합니다. 사용자 정의 컨트롤은 또한 페이지에 삽입 한 후 디자인 보기에서 렌더링 되지 않습니다.


성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나는 일관 된 모양과 느낌입니다. Asp.net에서 1.x에서 개발자는 웹 응용 프로그램에서 일반적인 페이지 요소를 복제할 사용자 정의 컨트롤을 사용 합니다. 확실히 작동 가능한 솔루션을 사용 되 고 있지만, 사용자 컨트롤을 사용 하는 몇 가지 단점이 있습니다. 예를 들어, 사용자 정의 컨트롤의 위치 변경 사이트 전체에서 여러 페이지에 대 한 변경에 필요합니다. 사용자 정의 컨트롤은 또한 페이지에 삽입 한 후 디자인 보기에서 렌더링 되지 않습니다.

ASP.NET 2.0에서는 마스터 페이지는 일관 된 모양과 느낌을 유지 관리 하는 방법으로 되며 곧 알게 되겠지만, 마스터 페이지 사용자 지정 컨트롤 메서드를 통해 상당히 향상 된 기능을 나타냅니다.

## <a name="why-master-pages"></a>마스터 페이지를 이유?

ASP.NET 2.0에서 마스터 페이지 필요한 이유는 궁금할 수 있습니다. 결국 웹 사이트 개발자 이미 사용 하는 사용자 정의 컨트롤에서 ASP.NET 1.x 콘텐츠 영역 페이지 간에 공유 합니다. 사용자 정의 컨트롤의 일반적인 레이아웃을 만드는 덜 보다 최적의 솔루션은 이유는 실제로 몇 가지 이유가 있습니다.

사용자 정의 컨트롤 페이지 레이아웃을 실제로 정의 하지 않습니다. 대신, 레이아웃 및 기능 페이지의 일부를 정의합니다. 사용자 제어 솔루션의 관리를 훨씬 더 어렵습니다 되므로 이러한 두 간의 구분이 중요 합니다. 예를 들어 페이지에서 사용자 정의 컨트롤의 위치를 변경 하려는 경우 사용자 정의 컨트롤이 표시 되는 실제 페이지를 편집 해야 합니다. Thats 잠시 페이지만 있지만 대규모 사이트에서 신속 하 게 되기 사이트 관리 문제일 경우 미세!

사용자 정의 컨트롤을 사용 하 여 일반적인 레이아웃을 정의 하기 위한 또 다른 단점은 ASP.NET 자체가의 아키텍처 기반으로 합니다. 사용자 정의 컨트롤의 모든 public 멤버 변경 되 면 모든 사용자 정의 컨트롤을 사용 하는 페이지를 다시 컴파일할 수 필요 합니다. 따라서 ASP.NET 다시 JIT 첫 번째 경우에 페이지에 액세스 한 다음 됩니다. 이 확장 가능한 비 아키텍처 및 대규모 사이트의 사이트 관리 문제는 다시 한 번 생성합니다.

ASP.NET 2.0에서 마스터 페이지에서 보기 좋게 사항은 모두 이러한 문제 (및 더 많은).

## <a name="how-master-pages-work"></a>마스터 페이지의 작동 방식

마스터 페이지는 다른 페이지에 대 한 템플릿을 유사 합니다. 페이지 요소 (즉, 메뉴, 테두리 등)에 다른 페이지 간에 공유 해야 하는 마스터 페이지에 추가 됩니다. 새 페이지는 사이트에 추가 하는 경우에 마스터 페이지를 사용 하 여 연결할 수 있습니다. 마스터 페이지와 연관 된 페이지가 호출 되는 **콘텐츠 페이지**합니다. 기본적으로 콘텐츠 페이지 마스터 페이지의 모양을 이동합니다. 그러나 마스터 페이지를 만든 경우 콘텐츠 페이지 자체 콘텐츠를 사용 하 여 대체할 수 있는 페이지의 일부를 정의할 수 있습니다. 이러한 일부 ASP.NET 2.0에 도입 된 새 컨트롤을 사용 하 여 정의 된 합니다 **ContentPlaceHolder** 제어 합니다.

마스터 페이지는 임의 개수의 contentplaceholder (또는 전혀 나타나지 않습니다.)를 포함할 수 있습니다. 콘텐츠 페이지의 내에 ContentPlaceHolder 컨트롤에서 내용이 나타납니다 **콘텐츠** 컨트롤, ASP.NET 2.0의 다른 새로운 컨트롤입니다. 기본적으로 사용자 고유의 콘텐츠를 제공할 수 있도록 콘텐츠 제어 콘텐츠 페이지는 비어 있습니다. 콘텐츠 컨트롤 내부에서 마스터 페이지의 콘텐츠를 사용 하려는 경우 수행할 수 있습니다 따라서 나중에이 모듈에에서 표시 됩니다. 콘텐츠 컨트롤의 콘텐츠 컨트롤의 ContentPlaceHolderID 특성을 통해 각각의 ContentPlaceHolder 컨트롤로 매핑됩니다. 맵 아래 코드 mainBody 마스터 페이지 라는 ContentPlaceHolder 컨트롤에 콘텐츠 컨트롤입니다.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 말을 자주 듣습니다 사람으로 다른 페이지에 대 한 기본 클래스 마스터 페이지에 설명 합니다. Thats 실제로 그렇지 않습니다. 마스터 페이지 콘텐츠 페이지와의 관계 상속의 하나가 아닙니다.


**그림 1** Visual Studio 2005에 나타나는 대로 마스터 페이지와 연결 된 콘텐츠 페이지를 보여 줍니다. 마스터 페이지 및 해당 ContentPlaceHolder 컨트롤로 표시 콘텐츠 콘텐츠 페이지에는 컨트롤입니다. 마스터 페이지 콘텐츠를 ContentPlaceHolder 외부를 볼 수 있지만 콘텐츠 페이지에서 회색 인지 확인 합니다. ContentPlaceHolder 내부 콘텐츠만 콘텐츠 페이지에서 supplanted 될 수 있습니다. 마스터 페이지에서 제공 되는 다른 모든 콘텐츠는 변경할 수 없습니다.


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


마스터 페이지의 파일 확장명은 되었다는 <em>.master</em>합니다. 일반 페이지에서 마스터 페이지와 다른 방법 중 하나입니다. 대신 프로시저의 다른 주요 차이점은는 @Page 마스터 페이지 지시문을 포함을 @Master 지시문입니다. 방금 만든 및 코드 검토 페이지 마스터에 대 한 소스 보기로 전환 합니다.

새 마스터 페이지를 기본적으로 각각의 ContentPlaceHolder 컨트롤로 하나를 사용 해야 합니다. 대부분의 경우에서 것이 더 좋은 일반적인 페이지 요소를 먼저 만들고 contentplaceholder를 삽입 한 다음 사용자 지정 내용이 필요한 곳입니다. 이러한 경우 개발자가 기본 ContentPlaceHolder 컨트롤을 삭제 하 여 페이지 개발은 새로 삽입 합니다. ContentPlaceHolder 컨트롤은 크기 조정 핸들을 표시지 않습니다 팩트 불구 하 고 크기를 조정할 수 없습니다. 한 가지 예외로; 포함 된 내용에 따라 자동으로 ContentPlaceHolder 컨트롤 크기 블록 요소 안에 각각의 ContentPlaceHolder 컨트롤로 같은 표 셀에 배치 하면 요소의 크기에 따라 크기 조정 됩니다.

## <a name="lab-1-working-with-master-pages"></a>랩 1 마스터 페이지 작업

이 실습에서는 마스터 페이지를 새로 만들고 3 개의 ContentPlaceHolder 컨트롤을 정의 합니다. 그런 다음 새 콘텐츠 페이지를 만들고 ContentPlaceHolder 컨트롤 중 하나에서 콘텐츠를 대체 합니다.

1. 마스터 페이지를 만들고 contentplaceholder를 삽입 합니다. 

    1. 위에서 설명한 대로 마스터 페이지를 새로 만듭니다.
    2. 기본 ContentPlaceHolder 컨트롤을 삭제 합니다.
    3. 각각의 ContentPlaceHolder 컨트롤로 컨트롤의 음영 처리 된 위쪽 테두리를 클릭 하 여 선택한 다음 키보드에서 DEL 키를 눌러 삭제 합니다.
    4. 사용 하 여 새 테이블을 삽입 합니다 *머리글과 쪽* 그림 3 에서처럼 템플릿. 전체 테이블 디자이너에 표시 되도록 너비와 높이 90%로 변경 합니다.


![](master-pages/_static/image3.jpg)

**그림 3**


1. 테이블의 각 셀에 커서를 놓고 설정 합니다 *valign* 속성을 *위쪽*합니다.
2. 도구 상자에서 테이블 (헤더 셀입니다.)의 맨 위 셀에는 각각의 ContentPlaceHolder 컨트롤로 삽입
3. 이 각각의 ContentPlaceHolder 컨트롤로 삽입할 때에 행 높이 차지 하는 거의 전체 페이지 그림 4 에서처럼 알 수 있습니다. Dont 신경 써야 하는 시점에서.


![빈 공간이 ContentPlaceHolder로 같은 셀에서](master-pages/_static/image1.gif)

**그림 4**: 빈 공간이 ContentPlaceHolder로 같은 셀에서


1. 다른 두 개의 셀에는 각각의 ContentPlaceHolder 컨트롤로 배치 합니다. 다른 ContentPlaceHolder 컨트롤이 삽입 후 테이블 셀의 크기를 짐작할 수 있어야 합니다. 페이지에 표시 되는 페이지 다음과 같아집니다 **그림 5**합니다.


![모든 ContentPlaceHolder 컨트롤과 마스터입니다. 머리글 셀에 대 한 셀 높이 이제 새로운 것이 알 수 있습니다.](master-pages/_static/image2.gif)

**그림 5**: 모든 ContentPlaceHolder 컨트롤로 마스터입니다. 머리글 셀에 대 한 셀 높이 이제 새로운 것이 알 수 있습니다.


1. 세 가지 ContentPlaceHolder 컨트롤로 각에 원하는 텍스트를 입력 합니다.
2. Exercise1.master로 마스터 페이지를 저장 합니다.
3. 새 Web Form을 만들고 exercise1.master 마스터 페이지를 사용 하 여 연결 합니다.
4. Visual Studio 2005에서 파일을 새 파일을 선택.
5. 선택 **Web Form** 새 항목 추가 대화 상자에서.
6. 그림 6에에서 표시 된 대로 마스터 페이지 선택 확인란을 선택 되어 있는지 확인 합니다.


![새 콘텐츠 페이지 추가](master-pages/_static/image3.gif)

**그림 6**: 새 콘텐츠 페이지 추가


1. 추가 클릭 합니다.
2. 선택 exercise1.master 선택에서 마스터 페이지 대화 상자 그림 7 에서처럼 합니다.
3. 새 콘텐츠 페이지를 추가 하려면 확인을 클릭 합니다.

새 콘텐츠 페이지는 마스터 페이지에 있는 각 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤을 사용 하 여 Visual Studio에 나타납니다. 기본적으로 콘텐츠 컨트롤은 빈 사용자 고유의 콘텐츠를 추가할 수 있도록 합니다. 분류 처럼을 마스터 페이지의 ContentPlaceHolder 컨트롤로의 콘텐츠를 사용할 수 있도록 하는 경우 단순히 스마트 태그 기호 (컨트롤의 오른쪽 위 모서리에 있는 작은 검은색 화살표)를 클릭 하 고 선택 *마스터 콘텐츠 기본값으로* 스마트 태그에 표시 된 것 처럼 **그림 8**합니다. 이렇게 하면 메뉴 항목으로 변경 *사용자 지정 콘텐츠 만들기*합니다. 이때 클릭 하는 특정 콘텐츠 컨트롤에 대 한 사용자 지정 콘텐츠를 정의할 수 있도록 마스터 페이지에서 콘텐츠를 제거 합니다.


![기본적으로 마스터 페이지 콘텐츠를 콘텐츠 컨트롤을 설정 합니다.](master-pages/_static/image4.gif)

**그림 7**: 콘텐츠 컨트롤을 마스터 페이지 콘텐츠를 기본값으로 설정


## <a name="connecting-master-page-and-content-pages"></a>마스터 페이지 및 콘텐츠 페이지 연결

네 가지 방법 중 하나에서 마스터 페이지 콘텐츠 페이지와의 연결을 구성할 수 있습니다.

- 합니다 <strong>MasterPageFile</strong> 특성을 @Page 지시문
- 설정 된 **Page.MasterPageFile** 코드에서 속성입니다.
- 합니다 **&lt;페이지&gt;** 응용 프로그램 구성 파일 (응용 프로그램의 루트 폴더에 web.config)에서 요소
- 합니다 **&lt;페이지&gt;** 하위 구성 파일 (하위 폴더에 web.config)에서 요소

## <a name="masterpagefile-attribute"></a>MasterPageFile 특성

MasterPageFile 특성을 사용 하면 쉽게 특정 ASP.NET 페이지에 마스터 페이지를 적용할 수 있습니다. 선택 하면 마스터 페이지를 적용할 사용 되는 방법 이기도 합니다 **마스터 페이지 선택** 실습 1에서 수행한 것 확인란을 선택 합니다.

## <a name="setting-pagemasterpagefile-in-code"></a>코드에서 Page.MasterPageFile 설정

코드의 MasterPageFile 속성을 설정 하 여 런타임 시 콘텐츠에 특정 마스터 페이지를 적용할 수 있습니다. 사용자 역할 또는 기타 일부 조건에 따라 특정 마스터 페이지를 적용 해야 하는 경우에 유용 합니다. PreInit 메서드에서 MasterPageFile 속성을 설정 해야 합니다. PreInit 메서드 후에 설정 된 경우 InvalidOperationException은 throw 됩니다. 이 속성을 설정 하는 페이지에 콘텐츠가 있어야 컨트롤을 최상위 컨트롤로 페이지에 대 한 합니다. 그렇지 않은 경우는 HttpException MasterPageFile 속성을 설정 하는 경우 throw 됩니다.

## <a name="using-the-ltpagesgt-element"></a>사용 하 여 &lt;페이지&gt; 요소

MasterPageFile 특성을 설정 하 여 페이지의 마스터 페이지를 구성할 수 있습니다 합니다 &lt;페이지&gt; web.config 파일의 요소입니다. 이 메서드를 사용 하면 응용 프로그램 구조에서 하위 web.config 파일에이 설정을 재정의할 수는 염두에서에 둡니다. 설정 MasterPageFile 특성을 @Page 지시문은이 설정을 재정의할 수도 있습니다. 사용 하는 &lt;페이지&gt; 요소를 사용 하면 간단 하 게 만들를 <em>마스터</em> 특정 폴더 또는 파일에서 필요한 경우 재정의할 수 있는 마스터 페이지입니다.

## <a name="properties-in-master-pages"></a>마스터 페이지의 속성

마스터 페이지는 간단 하 게 속성만 마스터 페이지 내에서 공용 속성을 노출할 수 있습니다. 예를 들어, 다음 코드는 SomeProperty 라는 속성을 정의 합니다.

[!code-csharp[Main](master-pages/samples/sample2.cs)]

마스터를 사용 해야 SomeProperty 속성에서 콘텐츠 페이지에 액세스 하려면 다음과 같이 속성:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>중첩 마스터 페이지

마스터 페이지는 대규모 웹 응용 프로그램에서 일반적인 모양 및 느낌을 위한 완벽 한 솔루션입니다. 그러나 다른 부분에는 다른 인터페이스를 공유 하는 동안 대규모 사이트 공유 공용 인터페이스의 특정 부분을 해야 일반적이 지 않은 아닙니다. 해당 요구를 해결 하기 위해 여러 마스터 페이지는는 완벽 한 솔루션입니다. 그러나 여전히 해당 사이트의 특정 섹션 간에 공유 되는 다른 구성 요소 및 특정 구성 요소 (예: 예를 들어 메뉴) 모든 페이지 간에 공유 되는 대형 응용 프로그램에 있을 팩트를 다루지 않습니다. 이러한 상황을 중첩 된 마스터 페이지 필요 원활 하 게 입력합니다. 지금까지 살펴본 대로 기본 마스터 페이지는 마스터 페이지 콘텐츠 페이지의 구성 됩니다. 중첩된 마스터 페이지를 사용 하는 경우에는 두 마스터 페이지 부모 마스터 및 자식 master입니다. 자식 마스터 페이지는 콘텐츠 페이지 및 마스터 부모 마스터 페이지입니다.

일반적인 마스터 페이지에 대 한 코드는 다음과 같습니다.

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

중첩된 된 마스터 시나리오에서 부모 master가 됩니다. 다른 마스터 페이지가이 페이지를 사용 하 여 해당 마스터 페이지는 하 고 해당 코드는 다음과 같습니다.

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

이 시나리오에서, 자식 마스터의 부모 마스터에 대 한 콘텐츠 페이지 이기도 합니다. 모든 자식 마스터의 콘텐츠를 콘텐츠 컨트롤 부모의 각각의 ContentPlaceHolder 컨트롤로에서 해당 콘텐츠를 가져오는 내부 나타납니다.

> [!NOTE]
> 디자이너 지원에 중첩 된 마스터 페이지에 대해 사용할 수 없는 경우 중첩 된 마스터를 사용 하 여를 개발 하는 경우 소스 뷰를 사용 해야 합니다.


이 비디오 연습은 중첩된 마스터 페이지를 사용 하 여 보여 줍니다.


![](master-pages/_static/image1.png)


[전체 화면 비디오 열기](master-pages/_static/nested1.wmv)


![마스터 페이지를 선택합니다.](master-pages/_static/image4.jpg)

**그림 8**: 마스터 페이지를 선택 합니다.
