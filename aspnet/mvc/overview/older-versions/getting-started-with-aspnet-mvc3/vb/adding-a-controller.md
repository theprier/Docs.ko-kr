---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: "(VB) 컨트롤러 추가 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 74113d76a74b1da27a7f9a33a13038a0c36ad036
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-controller-vb"></a>(VB) 컨트롤러 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 된 [C# 버전](../cs/adding-a-controller.md) 이 자습서의 합니다.


MVC는 *모델-뷰-컨트롤러*합니다. MVC는 각 부분에 별도 책임 되도록 응용 프로그램을 개발 하기 위한 패턴:

- 모델: 응용 프로그램에 대 한 데이터입니다.
- 보기: HTML 응답을 동적으로 생성 하 여 응용 프로그램에서 사용할 템플릿 파일입니다.
- 컨트롤러의 경우: 응용 프로그램에서 들어오는 URL 요청을 처리 하는 클래스 모델 데이터를 검색 하 고 클라이언트에 대 한 응답을 렌더링 하는 템플릿 보기를 지정 합니다.

이 자습서에서는 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.

마우스 오른쪽 단추로 클릭 하 여 새 컨트롤러를 만들기는 *컨트롤러* 폴더에 **솔루션 탐색기** 다음를 선택 하 고 **컨트롤러 추가**합니다.

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

새 컨트롤러 이름을 &quot;HelloWorldController&quot; 클릭 **추가**합니다.

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

**솔루션 탐색기** 오른쪽의 명명 된 사용자에 대 한 새 파일이 만들어졌음을 *HelloWorldController.cs* 및 파일이 IDE에서 열려 있습니다.

새로운 내부 `public class HelloWorldController` 블록을 다음 코드 처럼 보이는 두 개의 새 메서드를 만듭니다. 예를 들어 컨트롤러에서 직접 html 문자열로 반환 합니다.

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

컨트롤러 이름은 `HelloWorldController` 새로운 메서드가 즉 `Index`합니다. (누름 F5 또는 Ctrl + F5) 응용 프로그램을 실행 합니다. 브라우저 시작 된 후 추가 &quot;HelloWorld&quot; 주소 표시줄에 경로에 있습니다. (내 컴퓨터에 있기 `http://localhost:43246/HelloWorld`) 브라우저 아래 스크린샷과 같이 표시 됩니다. 위의 메서드 코드 문자열이 직접 반환 합니다. 시스템에 반환할 일부 HTML를 말 하 고에서 수행한!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다. ASP.NET MVC에서 사용 하는 기본 매핑 논리 다음과 같은 형식을 사용 하 여 제어 어떤 코드가 호출 됩니다.

`/[Controller]/[ActionName]/[Parameters]`

URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다. URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다. 따라서 */HelloWorld/인덱스* 으 리라 예상는 `Index` 의 메서드는 `HelloWorldController` 실행 하는 클래스입니다. 방문 했습니다 사라졌는지 */HelloWorld* 위에 및 `Index` 기본적으로 메서드를 사용 합니다. 라는 메서드가 때문에 이것이 `Index` 은 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 방법입니다.

`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다. `Welcome` 메서드가 실행 되 고 문자열을 반환 &quot;이 시작 작업 방법... &quot;. 기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다. 이 URL에 대 한 컨트롤러는 `HelloWorld` 및 `Welcome` 는 메서드입니다. 사용 하지 않은 `[Parameters]` 아직 URL의 일부입니다.

![](adding-a-controller/_static/image6.png)

수정 해 보겠습니다 예제에서는 약간의 일부 매개 변수 정보 URL에서 컨트롤러에 전달할 수 있도록 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*). 변경 하면 `Welcome` 메서드를 다음과 같이 두 개의 매개 변수를 포함 합니다. 임을 나타내는 VB 선택적 매개 변수 기능을 사용 했습니다 있는지 참고는 `numTimes` 경우 해당 매개 변수에 대해 값은 1의 매개 변수 기본값은입니다.

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

ְ ְ ¿כ를 찾아 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **합니다.** 에 대해 다른 값을 연습할 수 `name` 및 `numtimes`합니다. 시스템은 메서드의 매개 변수를 쿼리 문자열의 주소 표시줄에서 명명 된 매개 변수를 자동으로 매핑합니다.

![](adding-a-controller/_static/image7.png)

이러한 예제 모두에 컨트롤러에 작업을 하 고 MVC의 VC 부분 — 뷰와 컨트롤러 작업입니다. 컨트롤러 HTML을 직접 반환 됩니다. 일반적으로 코드에 번거로운 되므로 HTML을 직접 반환 하는 컨트롤러 않도록 합니다. 대신 일반적으로에서는 별도 뷰를 서식 파일을 HTML 응답을 생성할 수 있도록 합니다. 어떻게 이렇게 하려면 살펴보겠습니다.

>[!div class="step-by-step"]
[이전](intro-to-aspnet-mvc-3.md)
[다음](adding-a-view.md)
