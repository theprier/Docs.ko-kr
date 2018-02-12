---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: "HTML 도우미 (C#)를 TagBuilder 클래스를 사용 하 여 | Microsoft Docs"
author: StephenWalther
description: "Stephen Walther TagBuilder 클래스의 이름을 ASP.NET MVC 프레임 워크에 유용한 유틸리티 클래스를 소개 합니다. TagBuilder 클래스를 쉽게 사용할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 63f07c3f95c520dbc74f3568aa65dc6a6f34a901
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a>HTML 도우미 (C#)를 TagBuilder 클래스를 사용 하 여
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther TagBuilder 클래스의 이름을 ASP.NET MVC 프레임 워크에 유용한 유틸리티 클래스를 소개 합니다. HTML 태그를 손쉽게 바인딩할 TagBuilder 클래스를 사용할 수 있습니다.


ASP.NET MVC 프레임 워크에는 HTML 도우미를 작성할 때 사용할 수 있는 TagBuilder 클래스 라는 유용한 유틸리티 클래스가 포함 되어 있습니다. TagBuilder 클래스 클래스의 이름에서 알 수 있듯이 사용 하면 HTML 태그를 쉽게 작성할 수 있습니다. 이 간략 한 자습서에서 제공 됩니다 TagBuilder 클래스의 개요 및 HTML을 렌더링 하는 간단한 HTML 도우미를 작성할 때이 클래스를 사용 하는 방법을 알아봅니다 &lt;img&gt; 태그입니다.

## <a name="overview-of-the-tagbuilder-class"></a>TagBuilder 클래스의 개요

TagBuilder 클래스 System.Web.Mvc 네임 스페이스에 포함 됩니다. 다섯 가지 메서드가 있습니다.

- AddCssClass()-를 사용 하면 새 *클래스 = ""* 태그에 특성입니다.
- GenerateId()-태그에 id 특성을 추가할 수 있습니다. 이 메서드는 id에서 마침표를 대체 자동으로 (기본적으로 마침표 밑줄로 바뀝니다)
- MergeAttribute()-를 사용 하는 태그 특성을 추가할 수 있습니다. 이 메서드의 오버 로드를 여러 개 있습니다.
- SetInnerText()-를 사용 하는 태그의 내부 텍스트를 설정할 수 있습니다. 내부 텍스트는 HTML로 자동으로 인코드 합니다.
- Tostring ()-를 사용 하는 태그를 렌더링할 수 있습니다. 일반 태그, 시작 태그, 끝 태그 또는 자체적으로 닫는 태그를 만들 것인지 여부를 지정할 수 있습니다.
  

TagBuilder 클래스에 4 개의 중요 한 속성이 있습니다.

- 특성-모든 태그의 특성을 나타냅니다.
- IdAttributeDotReplacement-마침표 (기본값은 밑줄)를 바꾸는 GenerateId() 메서드에서 사용 되는 문자를 나타냅니다.
- InnerHTML-태그의 내부 내용을 나타냅니다. 이 속성에 문자열을 할당 *없는* 문자열을 HTML로 인코드 합니다.
- TagName-태그의 이름을 나타냅니다.

이러한 메서드 및 속성 사용 하면 모든 기본 메서드 및 속성의 HTML 태그를 작성 해야 하는 있습니다. 실제로 TagBuilder 클래스를 사용할 필요가 없습니다. StringBuilder 클래스를 대신 사용할 수 있습니다. 그러나 TagBuilder 클래스를 사용 하 여 수명의 좀 더 쉽게 합니다.

## <a name="creating-an-image-html-helper"></a>이미지 HTML 도우미 만들기

TagBuilder 클래스의 인스턴스를 만들 때 TagBuilder 생성자를 작성 하려면 하는 태그의 이름을 전달 합니다. 다음으로 태그의 특성을 수정 하려면 AddCssClass 및 MergeAttribute() 메서드 등의 메서드를 호출할 수 있습니다. 마지막으로 태그를 렌더링 하 tostring () 메서드를 호출 하 합니다.

예를 들어 목록 1 이미지 HTML 도우미를 포함합니다. 이미지 도우미와 HTML을 나타내는 TagBuilder 내부적으로 구현 됩니다 &lt;img&gt; 태그입니다.

**1-Helpers\ImageHelper.cs 나열**

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

목록 1의 클래스는 정적 이미지 라는 두 개의 오버 로드 된 메서드를 포함 합니다. Image() 메서드를 호출할 때 또는 HTML 특성의 집합을 나타내는 개체를 전달할 수 있습니다.

TagBuilder.MergeAttribute() 메서드를 사용 하 여 TagBuilder에 src 특성 등의 개별 특성을 추가 하는 방법을 확인 합니다. 또한 알 TagBuilder.MergeAttributes() 메서드를 사용 하 여 TagBuilder에 특성의 컬렉션을 추가 하는 방법을 합니다. MergeAttributes() 메서드에 사전&lt;문자열, o b j&gt; 매개 변수입니다. RouteValueDictionary 클래스는 리소스를 사전에 특성의 컬렉션을 나타내는 개체를 변환 하는 데 사용&lt;문자열, o b j&gt;합니다.

이미지 도우미를 만든 후에 다른 표준 HTML 도우미 중 하나라도 마찬가지로 사용해 ASP.NET MVC 뷰에 도우미를 사용할 수 있습니다. 보기 목록 2에 이미지 도우미를 사용 하 여 Xbox의 동일한 이미지를 두 번 표시 (그림 1 참조). Image() 도우미를 사용 하거나 사용 된 HTML 특성 컬렉션이 없으면 라고 합니다.

**Listing 2 - Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


[![새 프로젝트 대화 상자](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)

**그림 01**: 이미지 도우미를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))


공지 Index.aspx 보기의 맨 위쪽에 이미지 도우미에 연결 된 네임 스페이스를 가져와야 합니다. 도우미는 다음 지시문으로 가져오게 됩니다.

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

>[!div class="step-by-step"]
[이전](creating-custom-html-helpers-cs.md)
[다음](creating-page-layouts-with-view-master-pages-cs.md)
