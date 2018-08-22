---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: '3 부: 레이아웃 및 범주 메뉴 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 3 부에서는 레이아웃 및 범주 메뉴를 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: f55b29a271dbdb72d3e2249ed74517b77d78cf5e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829682"
---
<a name="part-3-layout-and-category-menu"></a>3 부: 레이아웃 및 범주 메뉴
====================
[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다. 해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 3 부에서는 레이아웃 및 범주 메뉴를 추가 합니다.


## <a id="_Toc260221669"></a>  일부 레이아웃 및 범주 메뉴 추가

사이트 마스터 페이지에는 제품 범주 메뉴를 포함 하는 왼쪽 열에 대 한 div를 추가 하겠습니다.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

원하는 정렬 및 기타 형식을 제공 됩니다 Style.css 파일을 추가한 CSS 클래스에 의해 note 합니다.

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

기존 제품 범주 및 메뉴 항목을 만들고 해당 연결에 대 한 전자 상거래 데이터베이스를 쿼리하여 런타임에 제품 범주 메뉴를 동적으로 만들 수 됩니다.

이렇게 하려면 두 ASP 사용 됩니다. NET의 강력한 데이터 컨트롤입니다. "엔터티 데이터 원본" 컨트롤과 "ListView" 컨트롤입니다.

![](tailspin-spyworks-part-3/_static/image1.jpg)

디자인 뷰로 전환 "" 및이 제어를 구성 하는 도우미를 사용 하겠습니다.

![](tailspin-spyworks-part-3/_static/image2.jpg)

EDS를 EntityDataSource ID 속성을 설정 해 보겠습니다\_범주\_메뉴 및 "데이터 소스 구성"을 클릭 합니다.

![](tailspin-spyworks-part-3/_static/image3.jpg)

상거래 데이터베이스에 대 한 데이터 소스 엔터티 모델을 만들었을 때 우리 회사에 생성 된 CommerceEntities 연결을 선택 하 고 "다음"을 클릭 합니다.

![](tailspin-spyworks-part-3/_static/image4.jpg)

"범주" 엔터티 집합 이름을 선택 하 고 고 나머지 옵션은 기본값으로 둡니다. [마침]을 클릭 합니다.

이제 했습니다 보면 페이지 ListView 배치 하는 ListView 컨트롤 인스턴스의 ID 속성을 설정 해 보겠습니다\_ProductsMenu 및 해당 도우미를 활성화 합니다.

![](tailspin-spyworks-part-3/_static/image5.jpg)

하지만 데이터 항목 표시 형식을 지정 하려면 제어 옵션을 사용할 수 및 서식 지정,이 메뉴 만들기만 해야 간단한 태그 소스 뷰에서 코드를 입력할 됩니다 있도록 합니다.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

"Eval" 문을 참고: &lt;% # Eval("CategoryName") %&gt;

ASP.NET 구문 &lt;% # %&gt; 는 약식 규칙 내에 포함 된 모든 및 결과 "Line"를 실행 하도록 런타임에 지시입니다.

문이 Eval("CategoryName") 지시는 바인딩된 데이터 항목 컬렉션의 현재 항목에 대 한 "CatagoryName" 엔터티 모델 항목 이름의 값을 인출 합니다. 이 값은 매우 강력한 기능에 대 한 간결한 구문입니다.

이제 응용 프로그램을 실행할 수 있습니다.

![](tailspin-spyworks-part-3/_static/image6.jpg)

표시 되는 제품 범주 메뉴 및 ProductsList.aspx 라는 메뉴 항목 링크가 가리키는 아직을 구현 해야 하는 페이지를 보면 범주 메뉴 항목 중 하나를 통한 대화형 것 및은 만들었습니다 동적 쿼리 문자열 인수는 포함 된  범주 id입니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-2.md)
> [다음](tailspin-spyworks-part-4.md)
