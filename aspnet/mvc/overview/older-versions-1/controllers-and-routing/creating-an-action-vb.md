---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 만들기 동작 (VB) | Microsoft Docs
author: microsoft
description: ASP.NET MVC 컨트롤러에 새 동작을 추가 하는 방법에 알아봅니다. 메서드는 작업에 대 한 요구 사항에 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: c77e4738444c61d60bdd78a50b36f98be41fc271
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-an-action-vb"></a>액션 (VB) 만들기
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET MVC 컨트롤러에 새 동작을 추가 하는 방법에 알아봅니다. 메서드는 작업에 대 한 요구 사항에 알아봅니다.


이 자습서의 목표 새 컨트롤러 동작을 만드는 방법을 설명 하는 것입니다. 동작 메서드의 요구 사항에 알아봅니다. 메서드는 작업으로 노출 되지 않도록 방지 하는 방법을 배웁니다.

## <a name="adding-an-action-to-a-controller"></a>컨트롤러에 작업 추가

컨트롤러에 새 메서드를 추가 하 여 컨트롤러에 새 동작을 추가 합니다. 예를 들어 컨트롤러 목록 1의 index ()는 작업 및 sayhello () 라는 동작을 포함 합니다. 두 방법 모두 작업으로 노출 됩니다.

**Listing 1 - Controllers\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

동작으로 universe에 게 노출 메서드는 특정 요구 사항을 충족 해야 합니다.

- 메서드는 공용 이어야 합니다.
- 메서드는 정적 메서드 일 수 없습니다.
- 메서드가 확장 메서드 수 없습니다.
- 생성자, getter 또는 setter 메서드 일 수 없습니다.
- 메서드가 개방형 제네릭 형식은 사용할 수 없습니다.
- 메서드는 컨트롤러의 기본 클래스의 메서드가 아닙니다.
- 메서드를 포함할 수 없습니다 **ref** 또는 **아웃** 매개 변수입니다.

컨트롤러 동작의 반환 형식에 제한이 없음을 인지 확인 합니다. 컨트롤러 동작 문자열을 DateTime, void 또는 Random 클래스의 인스턴스를 반환할 수 있습니다. ASP.NET MVC 프레임 워크는 작업 결과 문자열로 하지 않은 모든 반환 형식을 변환 하 고 브라우저에 문자열을 렌더링 됩니다.

컨트롤러에 이러한 요구 사항을 위반 하지 않는 모든 메서드를 추가 하면 메서드는 컨트롤러 작업으로 노출 됩니다. 주의 여기 해야 합니다. 인터넷에 연결 된 모든 사용자가 컨트롤러 작업을 호출할 수 있습니다. 예를 들어 만들지 마십시오 DeleteMyWebsite() 컨트롤러 작업.

## <a name="preventing-a-public-method-from-being-invoked"></a>호출 되는 공용 메서드를 방지

컨트롤러 클래스에는 공용 메서드를 만들어야 할 메서드를 컨트롤러 작업으로 노출 하지 않으려는 경우 때문 메서드를 사용 하 여 호출 되지는 &lt;NonAction&gt; 특성입니다. 목록 2에 있는 컨트롤러로 데코레이팅된 CompanySecrets() 라는 공용 메서드를 포함 하는 예를 들어는 &lt;NonAction&gt; 특성입니다.

**Listing 2 - Controllers\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

/Work/CompanySecrets 브라우저의 주소 표시줄에 입력 하 여 CompanySecrets() 컨트롤러 작업을 호출 하려고 하면 그림 1에 오류 메시지가 있게 됩니다.


[![NonAction 메서드 호출](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**그림 01**: NonAction 메서드 호출 ([전체 크기 이미지를 보려면 클릭](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [이전](creating-a-controller-vb.md)
> [다음](aspnet-mvc-controllers-overview-cs.md)
