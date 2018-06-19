---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 컨트롤러 (C#) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 어떤 i를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 963d3bbbadf408d7045c50bfd693069e4097d45d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868297"
---
<a name="adding-a-controller-c"></a>컨트롤러 (C#)에 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [C# 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 선호 하는 경우 전환의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


MVC는 *모델-뷰-컨트롤러*합니다. MVC는 잘 설계 하 고 유지 관리 하기 쉬운 되는 응용 프로그램을 개발 하기 위한 패턴입니다. MVC 기반 응용 프로그램에는 다음이 포함 되어 있습니다.

- 컨트롤러의 경우: 응용 프로그램에서 들어오는 요청을 처리 하는 클래스 모델 데이터를 검색 하 고 클라이언트에 대 한 응답을 반환 하는 템플릿 보기를 지정 합니다.
- 모델: 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하 고 응용 프로그램의 데이터를 나타내는 클래스입니다.
- 응용 프로그램 HTML 응답을 동적으로 생성을 사용 하 여 보기: 템플릿 파일입니다.

이 자습서 시리즈의 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.

컨트롤러 클래스를 만들어 시작 해 보겠습니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더 및 다음 선택 **컨트롤러 추가**합니다.

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

새 컨트롤러 "HelloWorldController" 이름을 지정 합니다. 기본 템플릿을으로 둡니다 **빈 컨트롤러** 클릭 **추가**합니다.

[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

**솔루션 탐색기** 새 파일이 만들어졌음을 명명 *HelloWorldController.cs*합니다. IDE에서 열려 있는 파일이 있습니다.

![](adding-a-controller/_static/image5.png)

내에서 `public class HelloWorldController` 블록을 다음 코드 처럼 보이는 두 메서드를 만듭니다. 예를 들어 컨트롤러 html 문자열을 반환 합니다.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

컨트롤러 이름은 `HelloWorldController` 고 위의 첫 번째 방법은 이름이 `Index`합니다. 브라우저에서 호출 해 보겠습니다. (누름 F5 또는 Ctrl + F5) 응용 프로그램을 실행 합니다. 브라우저에서 주소 표시줄에 경로에 "HelloWorld"를 추가 합니다. (의 아래 그림의 예를 들어 `http://localhost:43246/HelloWorld.`) 브라우저에서 페이지는 다음 스크린샷과 같이 표시 됩니다. 위의 메서드 코드 문자열이 직접 반환 합니다. 일부 HTML 반환할을 시스템에서 설정한 다시!

![](adding-a-controller/_static/image6.png)

ASP.NET MVC 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다. 호출 하는 코드를 확인 하려면 다음과 같은 형식을 사용 하는 ASP.NET MVC에서 사용 하는 기본 매핑 논리:

`/[Controller]/[ActionName]/[Parameters]`

URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다. URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다. 따라서 */HelloWorld/인덱스* 으 리라 예상는 `Index` 의 메서드는 `HelloWorldController` 실행 하는 클래스입니다. 로 이동 했습니다 사라졌는지 */HelloWorld* 및 `Index` 기본적으로 메서드를 사용 합니다. 라는 메서드가 때문에 이것이 `Index` 은 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 방법입니다.

`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다. `Welcome` 메서드는 "시작 작업 메서드입니다..."라는 문자열을 실행하고 반환합니다. 기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다. 이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다. 아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.

![](adding-a-controller/_static/image7.png)

수정 해 보겠습니다 예제 약간를 컨트롤러에 URL에서 일부 매개 변수 정보를 전달할 수 있습니다 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*). 변경 하면 `Welcome` 메서드를 다음과 같이 두 개의 매개 변수를 포함 합니다. 코드는 C# 기능 선택적 매개 변수를 사용 하 여 임을 나타내는 참고는 `numTimes` 경우 해당 매개 변수에 대해 값은 1의 매개 변수 기본값은입니다.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

ְ ְ ¿כ 예제 URL로 이동 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`합니다. 에 대해 다른 값을 시도할 수 `name` 및 `numtimes` url에서입니다. 시스템은 메서드의 매개 변수에 주소 표시줄에는 쿼리 문자열에서 명명 된 매개 변수를 자동으로 매핑합니다.

![](adding-a-controller/_static/image8.png)

두이 예제에서 컨트롤러는 작업을 하 고 "VC" 부분의 MVC-즉, 뷰 및 컨트롤러 작업 합니다. 컨트롤러 HTML을 직접 반환 됩니다. 일반적으로 코드에 번거로운 되므로 HTML을 직접 반환 하는 컨트롤러 않으려는 합니다. 대신 일반적으로에서는 별도 뷰를 서식 파일을 HTML 응답을 생성할 수 있도록 합니다. 다음 방법을 수행 수에 대해 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](intro-to-aspnet-mvc-3.md)
> [다음](adding-a-view.md)
