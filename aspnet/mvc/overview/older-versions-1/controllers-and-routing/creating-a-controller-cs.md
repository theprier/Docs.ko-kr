---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: 컨트롤러 (C#) 만들기 | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen Walther ASP.NET MVC 응용 프로그램에 컨트롤러를 추가할 수는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 86966f1064d09419e2102542c6d14c4162d153e4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868362"
---
<a name="creating-a-controller-c"></a>컨트롤러 (C#) 만들기
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

> 이 자습서에서는 Stephen Walther ASP.NET MVC 응용 프로그램에 컨트롤러를 추가할 수는 방법을 보여 줍니다.


이 자습서의 목표를 만드는 방법을 새 ASP.NET MVC 컨트롤러를 설명 하는 것입니다. 클래스 파일을 직접 만들어 및 Visual Studio 추가 컨트롤러 메뉴 옵션을 사용 하 여 컨트롤러를 만드는 방법을 배웁니다.

### <a name="using-the-add-controller-menu-option"></a>사용 하는 컨트롤러 메뉴 옵션 추가

새 컨트롤러를 만드는 가장 쉬운 방법은 Visual Studio 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 여 선택 되는 **추가, 컨트롤러** 메뉴 옵션 (그림 1 참조). 이 메뉴 옵션을 선택 하면 열립니다는 **컨트롤러 추가** 대화 상자 (그림 2 참조).


[![새 프로젝트 대화 상자](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

**그림 01**: 새 컨트롤러 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-cs/_static/image2.png))


[![새 프로젝트 대화 상자](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

**그림 02**: 컨트롤러 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-cs/_static/image4.png))


컨트롤러 이름의 첫 번째 부분에서 강조 표시 된 통지는 **컨트롤러 추가** 대화 상자. 모든 컨트롤러 이름을 접미사로 끝나야 *컨트롤러*합니다. 예를 들어 라는 컨트롤러를 만들 수 있습니다 *ProductController* 있지만 라는 컨트롤러 하지 *제품*합니다.


누락 된 컨트롤러를 만드는 경우는 *컨트롤러* 접미사 컨트롤러를 호출 해 수는 없습니다. 실행 하지 마십시오.--이 실수를 수행한 후 내 수명 많은 시간 불필요 하 게 했습니다.


**1-Controllers\ProductController.cs 나열**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

항상 Controllers 폴더의 컨트롤러를 만들어야 합니다. 그렇지 않은 경우 ASP.NET MVC의 규칙 위반 수 있으며, 다른 개발자가 응용 프로그램 이해 하기가 더 어려워지므로 시간 있습니다.

### <a name="scaffolding-action-methods"></a>스 캐 폴딩 작업 메서드

작업 메서드 만들기, 업데이트 및 세부 정보를 자동으로 생성 하는 옵션이 있는 컨트롤러를 만들 때 (그림 3 참조). 이 옵션을 선택 하는 경우 컨트롤러 클래스 목록 2에서 생성 됩니다.


[![작업 메서드를 자동으로 만들기](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

**그림 03**: 작업 메서드를 자동으로 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-cs/_static/image6.png))


**2-Controllers\CustomerController.cs 나열**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

이러한 생성 된 메서드는 스텁 메서드. 생성, 업데이트 및 사용자가 직접 고객에 대 한 세부 정보를 표시 하는 실제 논리를 추가 해야 합니다. 하지만 스텁 메서드 좋은 시작 지점을 제공 합니다.

### <a name="creating-a-controller-class"></a>컨트롤러 클래스 만들기

ASP.NET MVC 컨트롤러에는 클래스 뿐입니다. 원하는 경우 Visual Studio는 편리한 컨트롤러 기반 구조를 무시 하 고 컨트롤러 클래스를 직접 만들 수 있습니다. 아래 단계를 수행합니다.

1. Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 새 항목** 선택 하 고는 **클래스** 서식 파일 (그림 4 참조).
2. 새 클래스 PersonController.cs 이름을 지정 하 고 클릭는 **추가** 단추입니다.
3. 클래스가 상속 하는 기본 System.Web.Mvc.Controller 클래스 (코드 3 참조)에서 생성 된 클래스 파일을 수정 합니다.


[![새 클래스 만들기](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

**그림 04**: 새 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-cs/_static/image8.png))


**3-Controllers\PersonController.cs 나열**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

컨트롤러 목록 3에 "Hello World!" 문자열을 반환 하는 index () 라는 하나의 작업만 노출 합니다. 응용 프로그램을 실행 하 고 다음과 같은 URL을 요청 하 여이 컨트롤러 작업을 호출할 수 있습니다.

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET 개발 서버는 임의의 포트 번호 (예를 들어 40071)를 사용합니다. 컨트롤러를 호출 하는 URL을 입력할 때 올바른 포트 번호를 제공 해야 합니다. Windows 알림 영역 (의 오른쪽 아래 화면)에서 ASP.NET 개발 서버에 대 한 아이콘 위로 마우스를 이동 하 여 포트 번호를 확인할 수 있습니다.
> 
> [!div class="step-by-step"]
> [이전](adding-dynamic-content-to-a-cached-page-cs.md)
> [다음](creating-an-action-cs.md)
