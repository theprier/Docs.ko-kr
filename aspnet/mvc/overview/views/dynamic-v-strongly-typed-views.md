---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 동적 v입니다. Strongly Typed Views | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2011
ms.topic: article
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 8a96d43e04a0a50d5176c10c26aa49918a0e56ef
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26504092"
---
<a name="dynamic-v-strongly-typed-views"></a>동적 v입니다. 강력한 형식의 뷰
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

ASP.NET MVC 3의 보기에는 컨트롤러에서 정보를 전달 하는 방법은 세 가지가 있습니다.

1. 강력한 형식의 모델 개체로 반환 합니다.
2. 동적 형식으로 (사용 하 여 @model 동적)
3. ViewBag을 사용 하 여

비교 하 고 동적이 고 강력한 형식의 뷰 비교 하는 간단한 MVC 3 상위 블로그 응용 프로그램을 작성 합니다. 컨트롤러는 블로그 단순 목록으로 시작 합니다.

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

IndexNotStonglyTyped() 메서드에서 마우스 오른쪽 단추로 클릭 하 고 Razor 뷰를 추가 합니다.

[![8475.NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

있는지 확인는 **강력한 형식의 뷰 만들기** 확인란을 선택 하지 않습니다. 결과 뷰가 대부분 포함 되어 있지 않습니다.

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

동적 및 강력한 형식의 뷰가 아니라, 사용 하기 때문에 intellisense 도움이 되지 않습니다. 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646.NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

이제 강력한 형식의 뷰를 추가 합니다. 컨트롤러에 다음 코드를 추가 합니다.

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


정확 하 게는 동일한 반환 View(topBlogs); 것이 확인 비 강력한 형식의 뷰를 호출 합니다. 내부에 마우스 오른쪽 단추로 클릭 *StonglyTypedIndex()* 선택 **뷰 추가**합니다. 이 시간 선택은 **블로그** 선택한 모델 클래스 **목록** 스 캐 폴드 템플릿으로 합니다.

[![5658.StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

새 보기 템플릿 내부 intellisense 지원을 구했습니다.

[![7002.intellesince [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

C# 프로젝트를 다운로드할 수 있습니다 [여기](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)합니다.
