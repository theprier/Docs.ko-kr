---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: 컨트롤러 (C#) 만들기 | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가할 수는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6fe880775a5d477aefcf0fe6cedb3e719760ed90
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835550"
---
<a name="creating-a-controller-c"></a>컨트롤러 (C#) 만들기
====================
[Stephen walther가](https://github.com/StephenWalther)

> 이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가할 수는 방법을 보여 줍니다.


이 자습서의 목표는 새 ASP.NET MVC 컨트롤러 만들 수는 방법을 설명 합니다. 클래스 파일을 직접 만들어 및 Visual Studio 추가 컨트롤러 메뉴 옵션을 사용 하 여 컨트롤러를 만드는 방법에 알아봅니다.

### <a name="using-the-add-controller-menu-option"></a>사용 하 여 컨트롤러 메뉴 옵션 추가

새 컨트롤러를 만드는 가장 쉬운 방법은 Visual Studio 솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 하는 것은 **추가, 컨트롤러** 메뉴 옵션 (그림 1 참조). 이 메뉴 옵션을 선택 하면 열립니다는 **컨트롤러 추가** 대화 상자 (그림 2 참조).


[![새 프로젝트 대화 상자](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

**그림 01**: 새 컨트롤러 추가 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image2.png))


[![새 프로젝트 대화 상자](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

**그림 02**: 컨트롤러 추가 대화 상자 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image4.png))


첫 번째 부분에서 컨트롤러 이름 강조 표시 하는 **컨트롤러 추가** 대화 합니다. 모든 컨트롤러 이름을 접미사로 끝나야 *컨트롤러*합니다. 예를 들어 라는 컨트롤러를 만들 수 있습니다 *ProductController* 있지만 라는 컨트롤러가 아닌 *제품*합니다.


누락 된 컨트롤러를 만드는 경우 합니다 *컨트롤러* 접미사 컨트롤러를 호출할 수 없습니다. 실행 하지 마십시오.--이 실수 후 위해 시간 필자의 인생을 불필요 하 게 했습니다.


**1-Controllers\ProductController.cs 나열**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

항상 Controllers 폴더에서 컨트롤러를 만들어야 합니다. 이 고, 그렇지 ASP.NET MVC의 규칙 위반 수 및 다른 개발자가 좀 더 어려울 응용 프로그램을 이해 해야 합니다.

### <a name="scaffolding-action-methods"></a>스 캐 폴딩 작업 메서드

만들기, 업데이트 및 정보 작업 메서드를 자동으로 생성 하는 옵션이 있는 컨트롤러를 만들 때 (그림 3 참조). 이 옵션을 선택 하는 경우에 목록 2의 컨트롤러 클래스가 생성 됩니다.


[![작업 메서드를 자동으로 만들기](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

**그림 03**: 작업 메서드를 자동으로 만들기 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image6.png))


**2-Controllers\CustomerController.cs 나열**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

생성 된 이러한 메서드는 스텁 메서드입니다. 만들기, 업데이트 및 직접 고객에 대 한 세부 정보를 표시 하는 실제 논리를 추가 해야 합니다. 그러나 스텁 메서드 유용한 시작점을 제공 합니다.

### <a name="creating-a-controller-class"></a>컨트롤러 클래스 만들기

ASP.NET MVC 컨트롤러가 클래스 뿐입니다. 원한다 면를 편리 하 게 Visual Studio 컨트롤러 스 캐 폴딩을 무시 하 고 컨트롤러 클래스를 직접 만들 수 있습니다. 아래 단계를 수행합니다.

1. 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 새 항목** 선택 합니다 **클래스** 템플릿 (그림 4 참조).
2. PersonController.cs 새 클래스 이름을 지정 하 고 클릭 합니다 **추가** 단추입니다.
3. 클래스는 기본 System.Web.Mvc.Controller 클래스 (참조 코드 3)에서 상속 되도록 생성 된 클래스 파일을 수정 합니다.


[![새 클래스 만들기](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

**그림 04**: 새 클래스 만들기 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image8.png))


**3-Controllers\PersonController.cs 나열**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

보기 3의 컨트롤러는 "Hello World!" 문자열을 반환 하는 index () 이라는 하나의 작업이 노출 합니다. 응용 프로그램을 실행 하 고 다음과 같은 URL을 요청 하 여이 컨트롤러 작업을 호출할 수 있습니다.

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET Development Server는 임의의 포트 번호 (예를 들어 40071)를 사용합니다. 컨트롤러를 호출 하는 URL을 입력 하는 경우 올바른 포트 번호를 제공 해야 합니다. Windows 알림 영역 (아래쪽 오른쪽 화면)에서 ASP.NET 개발 서버에 대 한 아이콘 위로 마우스를 이동 하 여 포트 번호를 확인할 수 있습니다.
> 
> [!div class="step-by-step"]
> [이전](adding-dynamic-content-to-a-cached-page-cs.md)
> [다음](creating-an-action-cs.md)
