---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: "10 단계: 탐색 및 사이트 설계, 결론에 대 한 최종 업데이트 | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 부 10에서는 탐색 및에 대 한 마지막 업데이트를 다룹니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: af08039de2d810948b9ab64974111b0346c7fa0f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>10 단계: 탐색 및 사이트 설계, 결론에 대 한 마지막 업데이트
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 10 탐색 및 사이트 설계, 결론에 대 한 마지막 업데이트를 설명합니다.


이 사이트에 대 한 모든 주요 기능을 완료 한 것 하지만 아직 몇 가지 기능이 사이트 탐색, 홈 페이지 및 저장소 찾아보기 페이지에 추가 합니다.

## <a name="creating-the-shopping-cart-summary-partial-view"></a>쇼핑 카트 요약 부분 뷰 만들기

전체 사이트 사용자의 쇼핑 카트에 항목 수를 표시 하려고 합니다.

![](mvc-music-store-part-10/_static/image1.png)

우리의 Site.master에 추가 된 부분 뷰를 만들어 쉽게 구현할 수 있습니다.

이전에 표시 된 것 처럼 ShoppingCart 컨트롤러 부분 뷰를 반환 하는 CartSummary 작업 메서드에 포함 되어 있습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

CartSummary 부분 뷰를 만들려면 뷰/ShoppingCart 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 선택 합니다. CartSummary 뷰 이름을 지정 하 고 아래와 같이 "부분 뷰 만들기" 확인란을 확인 합니다.

![](mvc-music-store-part-10/_static/image2.png)

CartSummary 부분 뷰는 매우 간단-바구니에 항목의 수를 보여 주는 ShoppingCart 인덱스 뷰를 링크 일 뿐입니다. CartSummary.cshtml에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

부분 뷰 Html.RenderAction 메서드를 사용 하 여 사이트 마스터를 비롯 하 여 사이트의 모든 페이지에 포함 수 있습니다. RenderAction 아래으로 ("ShoppingCart") 컨트롤러 이름 및 작업 이름 ("CartSummary")을 지정할 수 있어야 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

이 레이아웃 사이트에 추가 하기 전에 만듭니다 장르 메뉴 우리의 Site.master 업데이트를 모두 한 번에 내릴 수 있도록 합니다.

## <a name="creating-the-genre-menu-partial-view"></a>Genre 메뉴 부분 뷰 만들기

시나리오에서는 사용자가 스토어에서 사용할 수 있는 모든 장르를 나열 하는 장르 메뉴를 추가 하 여 스토어를 통해 이동에 대 한 훨씬 쉽게 만들 수 있습니다.

![](mvc-music-store-part-10/_static/image3.png)

동일한 따르 단계 GenreMenu 부분 뷰를 만들 수도 및 다음을 추가할 수 있습니다를 모두 사이트 마스터 합니다. 첫째,는 StoreController를 다음 GenreMenu 컨트롤러 동작을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

이 작업 장르 다음 만들어집니다 여 부분 뷰를 표시 하는 목록을 반환 합니다.

*참고: 한다는이 작업 부분 뷰에서 사용할 수 있는이 컨트롤러 작업을 [ChildActionOnly] 특성을 추가 했습니다. 이 특성에는 컨트롤러 동작 /Store/GenreMenu로 이동 하 여 실행 되지 않도록 수 없게 됩니다. 부분 뷰 필요 하지 않습니다 이지만 것이 좋습니다 우리의 컨트롤러 작업은 원래의 의도 대로 사용 되도록 하는 데 있습니다. 에서는 또한 반환 하는 경우는 뷰 엔진이 다른 보기에 포함 되는이 보기에 대 한 레이아웃을 사용해 서는 안 것을 알 수 있도록 뷰가 아닌 PartialView 합니다.*

GenreMenu 컨트롤러 작업 단추로 클릭 하 고 아래와 같이 데이터 클래스는 장르 보기를 사용 하 여 강력 하 게 형식화 된 GenreMenu 라는 부분 뷰를 만듭니다.

![](mvc-music-store-part-10/_static/image4.png)

다음과 같이 정렬 되지 않은 목록을 사용 하 여 항목을 표시 하려면 GenreMenu 부분 뷰에 대 한 코드 보기를 업데이트 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>사이트 우리의 부분 뷰를 표시 하는 레이아웃 업데이트

부분 뷰는 사이트 레이아웃에 추가할 수 있습니다 (/ / Shared/뷰에\_Layout.cshtml) Html.RenderAction()를 호출 하 여 합니다. 아래와 같이 몇 가지 추가 태그를 표시할 수 뿐만 아니라 둘을 추가 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

이제 응용 프로그램을 실행 하면 왼쪽된 탐색 영역에서 장르와 맨 위에 있는 장바구니 요약 표시 됩니다 했습니다.

## <a name="update-to-the-store-browse-page"></a>저장소 찾아보기 페이지를 업데이트 합니다.

저장소 찾아보기 페이지 작동 하지만 매우 양호 보이지 않습니다. 코드 보기 (/Views/Store/Browse.cshtml에 있음) 다음과 같이 업데이트 하 여 더 나은 레이아웃 앨범 표시 하려면 페이지를 업데이트할 수 있습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

만들어져 여기 사용 Html.ActionLink 것이 아니라 Url.Action 앨범 아트 워크를 포함 하려면 링크에 특수 한 서식을 적용할 수도 있습니다.

*참고: 이러한 앨범에 대 한 일반 앨범 표지를 표시 됩니다. 이 정보는 데이터베이스에 저장 되며 저장소 관리자를 통해 편집할 수 있습니다. 사용자 고유의 아트 워크를 추가 하려면 시작 됩니다.*

이제는 장르를 찾아, 우리 앨범 아트 워크가 있는 표에 표시 된 앨범 표시 됩니다.

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>홈 페이지 위쪽 판매 앨범 표시 하도록 업데이트

이 가장 많이 판매 되 앨범 판매를 증진 홈 페이지에서 기능 하려고 합니다. 처리 하는, 고도 몇 가지 추가 그래픽에 추가할 우리의 HomeController에 일부 업데이트 만들면 되 합니다.

첫째, EntityFramework 연결 된 것을 알 수 있도록 탐색 속성 앨범 클래스를 추가 합니다 했습니다. 마지막 몇 줄의 우리의 **앨범** 클래스는 이제 다음과 같이 표시 됩니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*참고: 여기에 필요 합니다를 사용 하 여 추가 System.Collections.Generic 네임 스페이스에는 문입니다.*

첫째, storeDB 필드와는 다른 컨트롤러에서와 같이 문을 사용 하 여 MvcMusicStore.Models 추가 합니다. 다음으로, OrderDetails에 따라 상위 판매 앨범을 찾으려고 데이터베이스를 쿼리 하는 HomeController를 다음 메서드를 추가 합니다 했습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

이것이 전용 메서드를 컨트롤러 작업으로 사용할 수 있도록 않도록 하기입니다. 간단한 설명을 위해 HomeController에 포함 하는 것 이지만 적절 하 게 별도 서비스 클래스에 비즈니스 논리를 이동 하는 것이 좋습니다.

원위치에서에, 앨범 판매 된 상위 5 쿼리하고 보기로 돌려보낼 인덱스 컨트롤러 작업을 업데이트할 수 있습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

HomeController 업데이트에 대 한 전체 코드는 아래와 같습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

마지막으로 모델 유형 업데이트 및 앨범 목록 맨 아래에 추가 하 여 앨범 목록이 표시할 수 있습니다 우리의 홈 인덱스 뷰를 업데이트 해야 합니다. 또한 페이지 머리글과 프로 모션 섹션을 추가 하려면이 기회 해당 메뉴로 이동 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

이제 응용 프로그램을 실행 했습니다에서는 최상위 판매 앨범 판촉 메시지와 업데이트 된 홈 페이지가 표시 됩니다.

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>결론

ASP.NET MVC를 사용 하면 쉽게 버퍼 오버런 등의 데이터베이스 액세스 권한이 있으면 멤버 자격, AJAX 정교한 웹 사이트를 만들려고 합니다. 매우 신속 하 게 합니다. 다행히이 자습서가 제공한 사용자 고유의 ASP.NET MVC 응용 프로그램을 구축 하는 데 필요한 도구!


>[!div class="step-by-step"]
[이전](mvc-music-store-part-9.md)
