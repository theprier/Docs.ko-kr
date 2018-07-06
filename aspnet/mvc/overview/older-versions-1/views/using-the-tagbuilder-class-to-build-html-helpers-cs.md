---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: HTML 도우미 (C#)를 빌드하는 TagBuilder 클래스를 사용 하 여 | Microsoft Docs
author: StephenWalther
description: Stephen walther가 ASP.NET MVC 프레임 워크는 TagBuilder 클래스 라는의 유용한 유틸리티 클래스를 소개 합니다. TagBuilder 클래스를 쉽게 사용할 수 있습니다...
ms.author: aspnetcontent
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 9990fc7ad8093643a564a5e02ff65264d4a7fe15
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813228"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a>HTML 도우미 (C#)를 빌드하는 TagBuilder 클래스를 사용 하 여
====================
[Stephen walther가](https://github.com/StephenWalther)

> Stephen walther가 ASP.NET MVC 프레임 워크는 TagBuilder 클래스 라는의 유용한 유틸리티 클래스를 소개 합니다. HTML 태그를 쉽게 빌드하는 TagBuilder 클래스를 사용할 수 있습니다.


ASP.NET MVC 프레임 워크는 TagBuilder 클래스 HTML 도우미를 작성할 때 사용할 수 있는 유용한 유틸리티 클래스가 포함 됩니다. TagBuilder 클래스는 클래스의 이름에서 알 수 있듯이, 빌드할 수 있도록 쉽게 HTML 태그입니다. 이 간략 한 자습서는 TagBuilder 클래스의 개요가 제공 됩니다 및 HTML을 렌더링 하는 간단한 HTML 도우미를 작성 하는 경우이 클래스를 사용 하는 방법에 알아봅니다 &lt;img&gt; 태그입니다.

## <a name="overview-of-the-tagbuilder-class"></a>TagBuilder 클래스 개요

TagBuilder 클래스 System.Web.Mvc 네임 스페이스에 포함 됩니다. 다섯 가지 메서드가 있습니다.

- AddCssClass()-을 사용 하면 새 추가할 수 있습니다 *클래스 = ""* 태그에 특성입니다.
- GenerateId()-를 사용 하면 태그 id 특성을 추가할 수 있습니다. 이 메서드는 id에서 마침표를 자동으로 대체 (기본적으로 기간 밑줄로 바뀝니다)
- MergeAttribute()-를 사용 하는 태그에 특성을 추가할 수 있습니다. 이 메서드의 여러 오버 로드가 있습니다.
- SetInnerText()-를 사용 하면 태그의 내부 텍스트를 설정할 수 있습니다. 내부 텍스트 HTML 인코딩 자동입니다.
- Tostring ()-를 사용 하면 태그를 렌더링할 수 있습니다. 일반 태그, 시작 태그, 끝 태그 또는 자체 닫음 태그를 만들 것인지 여부를 지정할 수 있습니다.
  

TagBuilder 클래스에는 네 가지 중요 한 속성에 있습니다.

- 특성-모든 태그의 특성을 나타냅니다.
- IdAttributeDotReplacement-기간 (기본값은 밑줄)를 바꾸는 데 GenerateId() 메서드에서 문자를 나타냅니다.
- InnerHTML-태그의 내부 콘텐츠를 나타냅니다. 이 속성에 문자열을 할당 *하지 않습니다* HTML 문자열을 인코딩합니다.
- TagName-태그의 이름을 나타냅니다.

이러한 메서드 및 속성 사용 하면 모든 기본 메서드 및 HTML 태그를 작성 해야 하는 속성이 있습니다. 실제로 TagBuilder 클래스를 사용할 필요가 없습니다. StringBuilder 클래스를 대신 사용할 수 있습니다. 그러나는 TagBuilder 클래스를 사용 하면 업무를 더 쉽게 합니다.

## <a name="creating-an-image-html-helper"></a>이미지 HTML 도우미 만들기

TagBuilder 클래스의 인스턴스를 만들면 빌드하는 TagBuilder 생성자에 원하는 태그의 이름을 전달 합니다. 다음으로 태그의 특성을 수정할 수 MergeAttribute() 메서드와 AddCssClass와 같은 메서드를 호출할 수 있습니다. 마지막으로 태그를 렌더링 하는 tostring () 메서드를 호출 합니다.

예를 들어 목록 1 이미지 HTML 도우미를 포함합니다. 이미지 도우미는 HTML을 나타내는 TagBuilder를 사용 하 여 내부적으로 구현 됩니다 &lt;img&gt; 태그입니다.

**1-Helpers\ImageHelper.cs 나열**

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

목록 1에서 클래스는 정적 이미지 라는 두 개의 오버 로드 된 메서드를 포함 합니다. Image() 메서드를 호출 하면 여부 HTML 특성의 집합을 나타내는 개체를 전달할 수 있습니다.

TagBuilder.MergeAttribute() 메서드를 사용 하는 TagBuilder에 src 특성 등의 개별 특성을 추가 하는 방법을 확인할 수 있습니다. 또한 확인 TagBuilder.MergeAttributes() 메서드를 사용 하는 TagBuilder 특성의 컬렉션을 추가 하는 방법을 합니다. MergeAttributes() 메서드에서 사전을&lt;문자열, 개체&gt; 매개 변수입니다. RouteValueDictionary 클래스 사전에 특성의 컬렉션을 나타내는 개체를 변환 하는 데 사용 됩니다&lt;문자열, 개체&gt;합니다.

이미지 도우미를 만든 후에 모든 다른 표준 HTML 도우미와 마찬가지로 ASP.NET MVC 보기에서 도우미를 사용할 수 있습니다. 목록 2 뷰 이미지 도우미를 사용 하 여 Xbox의 동일한 이미지를 두 번 표시할 (그림 1 참조). 포함 및 제외 HTML 특성 컬렉션을 모두 Image() 도우미 라고 합니다.

**Listing 2 - Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


[![새 프로젝트 대화 상자](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)

**그림 01**: 이미지 도우미를 사용 하 여 ([큰 이미지를 보려면 클릭](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))


알림 Index.aspx 뷰의 맨 위에 있는 이미지 도우미에 연결 된 네임 스페이스를 가져와야 합니다. 도우미는 다음 지시문을 사용 하 여 가져옵니다.

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> [이전](creating-custom-html-helpers-cs.md)
> [다음](creating-page-layouts-with-view-master-pages-cs.md)
