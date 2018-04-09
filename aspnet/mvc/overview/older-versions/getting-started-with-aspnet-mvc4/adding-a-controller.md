---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: bb76c0a87d935322406b9d8e18fbdb3e41f327f5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-controller"></a>컨트롤러 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.


MVC는 *모델-뷰-컨트롤러*합니다. MVC는은 잘 설계, 테스트 및 유지 관리 하기 쉬운 응용 프로그램을 개발 하기 위한 패턴입니다. MVC 기반 응용 프로그램에는 다음이 포함 되어 있습니다.

- **M** odels: 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하 고 응용 프로그램의 데이터를 나타내는 클래스입니다.
- **V** iews: 응용 프로그램 사용 HTML 응답을 동적으로 생성 하는 템플릿 파일입니다.
- **C** ontrollers: 들어오는 브라우저 요청을 처리 하는 클래스 모델 데이터를 검색 한 다음 브라우저에 대 한 응답을 반환 하는 템플릿 보기를 지정 합니다.

이 자습서 시리즈의 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.

컨트롤러 클래스를 만들어 시작 해 보겠습니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더 및 다음 선택 **컨트롤러 추가**합니다.

![](adding-a-controller/_static/image1.png)

새 컨트롤러 이름을 &quot;HelloWorldController&quot;합니다. 기본 템플릿을으로 둡니다 **빈 MVC 컨트롤러** 클릭 **추가**합니다.

![컨트롤러 추가](adding-a-controller/_static/image2.png)

**솔루션 탐색기** 새 파일이 만들어졌음을 명명 *HelloWorldController.cs*합니다. IDE에서 열려 있는 파일이 있습니다.

![](adding-a-controller/_static/image3.png)

파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

예를 들어 컨트롤러 메서드에 html 문자열을 반환 합니다. 컨트롤러 이름은 `HelloWorldController` 고 위의 첫 번째 방법은 이름이 `Index`합니다. 브라우저에서 호출 해 보겠습니다. (누름 F5 또는 Ctrl + F5) 응용 프로그램을 실행 합니다. 브라우저에서 추가 &quot;HelloWorld&quot; 주소 표시줄에 경로에 있습니다. (의 아래 그림의 예를 들어 `http://localhost:1234/HelloWorld.`) 브라우저에서 페이지는 다음 스크린샷과 같이 표시 됩니다. 위의 메서드 코드 문자열이 직접 반환 합니다. 일부 HTML 반환할을 시스템에서 설정한 다시!

![](adding-a-controller/_static/image4.png)

ASP.NET MVC 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다. ASP.NET MVC에서 사용 하는 기본 URL 라우팅 논리를 호출 하는 코드를 확인 하려면 다음과 같은 형식을 사용 합니다.

`/[Controller]/[ActionName]/[Parameters]`

URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다. URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다. 따라서 */HelloWorld/인덱스* 으 리라 예상는 `Index` 의 메서드는 `HelloWorldController` 실행 하는 클래스입니다. 로 이동 했습니다 사라졌는지 */HelloWorld* 및 `Index` 기본적으로 메서드를 사용 합니다. 라는 메서드가 때문에 이것이 `Index` 은 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 방법입니다.

`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다. `Welcome` 메서드가 실행 되 고 문자열을 반환 &quot;이 시작 작업 방법... &quot;. 기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다. 이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다. 아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.

![](adding-a-controller/_static/image5.png)

수정 해 보겠습니다 예제 약간를 컨트롤러에 URL에서 일부 매개 변수 정보를 전달할 수 있습니다 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*). 변경 하면 `Welcome` 메서드를 다음과 같이 두 개의 매개 변수를 포함 합니다. 코드는 C# 기능 선택적 매개 변수를 사용 하 여 임을 나타내는 참고는 `numTimes` 경우 해당 매개 변수에 대해 값은 1의 매개 변수 기본값은입니다.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

ְ ְ ¿כ 예제 URL로 이동 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`합니다. 에 대해 다른 값을 시도할 수 `name` 및 `numtimes` url에서입니다. [ASP.NET MVC 모델 바인딩 시스템이](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 메서드의 매개 변수에 주소 표시줄에는 쿼리 문자열에서 명명 된 매개 변수를 자동으로 매핑합니다.

![](adding-a-controller/_static/image6.png)

이러한 예제 모두에 컨트롤러에 작업을 하 고는 &quot;VC&quot; MVC의 부분 — 뷰와 컨트롤러 작업 즉, 합니다. 컨트롤러 HTML을 직접 반환 됩니다. 일반적으로 코드에 번거로운 되므로 HTML을 직접 반환 하는 컨트롤러 않으려는 합니다. 대신 일반적으로에서는 별도 뷰를 서식 파일을 HTML 응답을 생성할 수 있도록 합니다. 다음 방법을 수행 수에 대해 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](intro-to-aspnet-mvc-4.md)
> [다음](adding-a-view.md)
