---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 캐시 된 페이지 (C#)에 동적 콘텐츠 추가 | Microsoft Docs
author: microsoft
description: 같은 페이지의 동적 및 캐시 된 콘텐츠를 혼합 하는 방법을 알아봅니다. 캐시 후 대체 배너 광고 o 같은 동적 콘텐츠를 표시할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 9f91cc07bc531cfb3edf577ab79e91fd94a57a3c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-dynamic-content-to-a-cached-page-c"></a>캐시 된 페이지 (C#)에 동적 콘텐츠 추가
====================
by [Microsoft](https://github.com/microsoft)

> 같은 페이지의 동적 및 캐시 된 콘텐츠를 혼합 하는 방법을 알아봅니다. 캐시 후 대체 배너 보급 알림 또는 뉴스 항목 캐시 페이지 출력 된 변수가 있는 내에서 같은 동적 콘텐츠를 표시할 수 있습니다.


출력 캐싱을 활용 하기 위해, ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다. 매번 페이지가 요청 될 페이지를 다시 생성 하는 대신 페이지 한 번만 생성 되어 여러 사용자에 대 한 메모리에 캐시 합니다.

하지만 문제가 있습니다. 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 어떻게? 예를 들어 페이지에 배너 광고를 표시할 것인지 한다고 가정 합니다. 모든 사용자가 동일한 광고를 볼 수 있도록 캐시 되도록 배너 광고가 되기를 원하지 않습니다. 이런 방식으로 돈을 더를 확인 하지 않습니다!

다행히 쉬운 방법이입니다. 라는 ASP.NET 프레임 워크의 기능을 이용할 수 있습니다 *캐시 후 대체*합니다. 캐시 후 대체를 사용 하면 메모리에 캐시 되어 있는 페이지의 동적 콘텐츠를 대체할 수 있습니다.


일반적으로 [OutputCache] 특성을 사용 하 여 캐시 된 페이지를 출력할 때 페이지는 서버와 클라이언트 (웹 브라우저)에 캐시 됩니다. 캐시 후 대체를 사용 하는 경우 페이지는 서버에만 캐시 됩니다.


#### <a name="using-post-cache-substitution"></a>캐시 후 대체를 사용 하 여

캐시 후 대체를 사용 하 여 하려면 두 단계가 필요 합니다. 첫째, 캐시 된 페이지에 표시 하려고 하는 동적 콘텐츠를 나타내는 문자열을 반환 하는 메서드를 정의 해야 합니다. 다음으로 페이지에 동적 콘텐츠를 삽입할 HttpResponse.WriteSubstitution() 메서드를 호출.

예를 들어 임의로 캐시 된 페이지에 다른 뉴스 항목을 표시 한다고 가정해 보세요. 목록 1의 클래스에는 라는 RenderNews() 임의로 세 뉴스 항목의 목록에서 하나의 뉴스 항목을 반환 하는 단일 메서드를 노출 합니다.

**1 – Models\News.cs 나열**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

캐시 후 대체를 이용 하려면 HttpResponse.WriteSubstitution() 메서드를 호출 합니다. 동적 콘텐츠는 캐시 된 페이지의 영역 바꿉니다 WriteSubstitution() 메서드 코드를 설정 합니다. WriteSubstitution() 메서드를 사용 하 여 목록 2의 뷰에서 임의의 뉴스 항목을 표시 합니다.

**Listing 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

RenderNews 메서드에 WriteSubstitution() 메서드에 전달 됩니다. 확인 된 RenderNews 메서드가 호출 되지 않습니다 (없습니다 괄호는 있음). 대신 WriteSubstitution()는 메서드에 대 한 참조가 전달 됩니다.

인덱스 뷰 캐시 됩니다. 보기는 보기 3의 컨트롤러에 의해 반환 됩니다. Index () 동작 60 초 동안 캐시 될 인덱스 뷰를 발생 시키는 [OutputCache] 특성으로 데코레이팅되 어 있는지를 확인 합니다.

**3 – Controllers\HomeController.cs 나열**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

인덱스 뷰 캐시 되는 경우에 인덱스 페이지를 요청 하는 경우 다른 임의의 뉴스 항목이 표시 됩니다. 인덱스 페이지를 요청 하는 경우 60 초 (그림 1 참조)에 대 한 페이지에 의해 표시 된 시간이 변경 되지 않습니다. 시간 변경 되지 않는 팩트 페이지가 캐시를 증명 합니다. 각 요청과 함께 WriteSubstitution() 메서드-임의 뉴스 항목 – 변경에 의해 콘텐츠 삽입 되는 반면 합니다.

**그림 1-캐시 된 페이지에 동적 뉴스 항목 삽입**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>도우미 메서드에서 캐시 후 대체를 사용 하 여

캐시 후 대체 기능을 활용할 수 있는 더욱 손쉬운 방법을 사용자 지정 도우미 메서드 내에서 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 합니다. 목록 4의 도우미 메서드에 의해이 방법은 보여 줍니다.

**4 – AdHelper.cs 나열**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

두 개의 메서드를 노출 하는 정적 클래스를 포함 목록 4: RenderBanner() 및 RenderBannerInternal() 합니다. RenderBanner() 메서드를 실제 도우미 메서드를 나타냅니다. 이 메서드는 다른 도우미 메서드와 마찬가지로 뷰에서 Html.RenderBanner()를 호출할 수 있도록 표준 ASP.NET MVC HtmlHelper 클래스를 확장 합니다.

RenderBanner() 메서드 RenderBannerInternal() 메서드 WriteSubsitution() 메서드에 전달 HttpResponse.WriteSubstitution() 메서드를 호출 합니다.

RenderBannerInternal() 메서드는 private 메서드입니다. 이 메서드는 도우미 메서드로 노출 되지 않습니다. 임의로 RenderBannerInternal() 메서드는 세 가지 배너 광고 이미지의 목록에서 광고 배너 이미지를 반환합니다.

목록 5의 수정 된 인덱스 뷰 RenderBanner() 도우미 메서드를 사용 하는 방법을 보여 줍니다. 다음에 유의 추가 &lt;% @ 가져오기 %&gt; 지시문 MvcApplication1.Helpers 네임 스페이스를 가져오는 뷰의 맨 아래에 포함 되어 있습니다. 이 네임 스페이스를 가져오지 않은, RenderBanner() 메서드 Html 속성의 메서드로 표시 되지 않습니다.

**5-Views\Home\Index.aspx (RenderBanner() 메서드로)를 나열합니다.**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

목록 5의 보기에서 렌더링 된 페이지를 요청 다른 배너 보급을 각 요청과 함께 표시 됩니다 (그림 2 참조). 페이지 캐시 되지만 RenderBanner() 도우미 메서드에 의해 배너 광고를 동적으로 삽입 합니다.

**그림 2 – 임의 배너 광고를 표시 된 인덱스 뷰**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 캐시 된 페이지의 내용을 동적으로 업데이트 하는 방법을 설명 합니다. 동적 콘텐츠 캐시 된 페이지에 지정 된 수를 사용할 수 있도록 HttpResponse.WriteSubstitution() 메서드를 사용 하는 방법을 배웠습니다. 또한 HTML 도우미 메서드 내에서 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 방법을 배웠습니다.

웹 응용 프로그램의 성능에 큰 영향을 줄 수 것-가능한 경우 항상 캐싱을 활용 합니다. 이 자습서에서 설명 했 듯이를 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 캐싱의 이용할 수 있습니다.

## 

## 

> [!div class="step-by-step"]
> [이전](improving-performance-with-output-caching-cs.md)
> [다음](creating-a-controller-cs.md)
