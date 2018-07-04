---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 작업 (VB) 만들기 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 알아봅니다. 작업 메서드에 대 한 요구 사항에 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: 64bc75eaccdd71ebff59f34a824c9b6c520a27ef
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367870"
---
<a name="creating-an-action-vb"></a>작업 (VB) 만들기
====================
[Microsoft](https://github.com/microsoft)

> ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 알아봅니다. 작업 메서드에 대 한 요구 사항에 알아봅니다.


이 자습서의 목표는 새 컨트롤러 작업을 만드는 방법을 설명 합니다. 동작 메서드의 요구 사항에 대해 알아봅니다. 메서드를 작업으로 노출 되지 않도록 방지 하는 방법을 배웁니다.

## <a name="adding-an-action-to-a-controller"></a>컨트롤러에 작업 추가

컨트롤러에 새 메서드를 추가 하 여 새 작업 컨트롤러에 추가 합니다. 예를 들어 목록 1의 컨트롤러는 index () 라는 작업 및 sayhello () 라는 작업을 포함 합니다. 두 방법 모두 작업으로 노출 됩니다.

**1-Controllers\HomeController.vb 나열**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

메서드는 동작으로 universe를 노출 하기 위해 특정 요구 사항을 충족 해야 합니다.

- 메서드는 public 이어야 합니다.
- 메서드는 정적 메서드 일 수 없습니다.
- 메서드는 확장 메서드를 수 없습니다.
- 생성자, getter 또는 setter 메서드 일 수 없습니다.
- 메서드는 개방형 제네릭 형식은 사용할 수 없습니다.
- 메서드는 컨트롤러의 기본 클래스의 메서드가 아닙니다.
- 메서드를 포함할 수 없습니다 **ref** 하거나 **out** 매개 변수입니다.

컨트롤러 동작의 반환 형식에 제한이 있는지 확인 합니다. 컨트롤러 작업을 string, DateTime, void 또는 Random 클래스의 인스턴스를 반환할 수 있습니다. ASP.NET MVC 프레임 워크는 작업 결과 문자열에 없는 모든 반환 형식을 변환 되며 브라우저에 문자열을 렌더링 합니다.

컨트롤러에 이러한 요구 사항을 위반 하지 않는 모든 메서드를 추가 하는 경우 메서드는 컨트롤러 작업으로 노출 됩니다. 까다로우므로 주의 합니다. 컨트롤러 작업을 인터넷에 연결 하는 누구나 호출할 수 있습니다. 예를 들어 만들지 DeleteMyWebsite() 컨트롤러 작업을 합니다.

## <a name="preventing-a-public-method-from-being-invoked"></a>공용 메서드 호출에서 방지

컨트롤러 클래스의 public 메서드를 생성 해야 하 고 컨트롤러 작업으로 메서드를 노출 하지 않으려는 경우를 사용 하 여 호출 되는 메서드를 방지할 수 있습니다 합니다 &lt;NonAction&gt; 특성입니다. 목록 2에서 컨트롤러를 사용 하 여 데코 레이트 된 CompanySecrets() 라는 public 메서드를 포함 하는 예를 들어 합니다 &lt;NonAction&gt; 특성입니다.

**Listing 2 - Controllers\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

/Work/CompanySecrets 브라우저의 주소 표시줄에 입력 하 여 CompanySecrets() 컨트롤러 작업을 호출 하려고 하면 그림 1에서 오류 메시지를 받게 됩니다.


[![NonAction 메서드 호출](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**그림 01**: NonAction 메서드 호출 ([큰 이미지를 보려면 클릭](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [이전](creating-a-controller-vb.md)
> [다음](aspnet-mvc-controllers-overview-cs.md)
