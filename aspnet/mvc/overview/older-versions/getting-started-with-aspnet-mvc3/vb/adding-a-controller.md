---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: 컨트롤러 (VB) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 75451be20bd39f37bb692a06389ed7f04bc75a2a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367854"
---
<a name="adding-a-controller-vb"></a>(VB) 컨트롤러 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [VB.NET 버전](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 합니다 [C# 버전](../cs/adding-a-controller.md) 이 자습서의 합니다.


MVC는 의미 *모델-뷰-컨트롤러*합니다. MVC는 각 파트에는 별도 책임이 되도록 응용 프로그램을 개발 하기 위한 패턴:

- 모델: 응용 프로그램에 대 한 데이터입니다.
- 보기: 동적으로 HTML 응답을 생성 하려면 응용 프로그램에서 사용할 템플릿 파일입니다.
- 컨트롤러: 응용 프로그램에 들어오는 URL 요청을 처리 하는 클래스 모델 데이터를 검색 하 고 클라이언트에 대 한 응답을 렌더링 하는 템플릿 보기를 지정 합니다.

이 자습서에서 이러한 모든 개념을 다루는 수 하 고 응용 프로그램을 만들고 사용 하는 방법을 보여 됩니다.

마우스 오른쪽 단추로 클릭 하 여 새 컨트롤러를 만듭니다는 *컨트롤러* 폴더에서 **솔루션 탐색기** 을 선택한 다음 **컨트롤러 추가**합니다.

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

새 컨트롤러의 이름을 &quot;HelloWorldController&quot; 누릅니다 **추가**합니다.

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

확인할 수 있습니다 **솔루션 탐색기** 오른쪽를 새 파일로 만들어진 것 이라는 *HelloWorldController.cs* IDE에 열려 있는 파일 인지 합니다.

새 내부 `public class HelloWorldController` 차단, 다음 코드 처럼 보이는 두 개의 새 메서드를 만듭니다. 예를 들어 컨트롤러에서 직접 html 문자열로 반환 합니다.

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

컨트롤러 이름은 `HelloWorldController` 라는 새 메서드 및 `Index`합니다. (F5 또는 ctrl+f5를 누릅니다) 응용 프로그램을 실행 합니다. 브라우저에 시작 되 면 추가 &quot;HelloWorld&quot; 주소 표시줄의 경로에 있습니다. (내 컴퓨터에 `http://localhost:43246/HelloWorld`) 브라우저 아래 스크린샷과 같이 표시 됩니다. 위의 메서드에 코드를 직접 문자열을 반환 합니다. 일부 HTML을 반환 하도록 시스템을 말씀을 수행한 것!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC는 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 그 안에 다양 한 작업 메서드)를 호출합니다. ASP.NET MVC에서 사용 되는 매핑 논리 코드는 호출을 제어 하려면 다음과 같은 형식을 사용 합니다.

`/[Controller]/[ActionName]/[Parameters]`

URL의 첫 번째 부분 실행할 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다. URL의 두 번째 부분 클래스에 대 한 작업 메서드를 결정 합니다. 따라서 */HelloWorld/인덱스* 로 인해를 `Index` 메서드의 `HelloWorldController` 실행 하는 클래스입니다. 방문 했습니다 */HelloWorld* 위에 및 `Index` 메서드는 기본적으로 사용 되었습니다. 라는 메서드가 때문에 이것이 `Index` 명시적으로 지정 하지 않으면 컨트롤러에서 호출 되는 기본 방법입니다.

`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다. 합니다 `Welcome` 실행 하 고 문자열을 반환 &quot;이 시작 작업 메서드입니다... &quot;. 기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다. 컨트롤러는이 URL에 대 한 `HelloWorld` 고 `Welcome` 는 메서드입니다. 사용 하지 않은 것을 `[Parameters]` 아직 URL의 일부입니다.

![](adding-a-controller/_static/image6.png)

URL에서에서 일부 매개 변수 정보를 컨트롤러에 전달할 수 있도록 약간에서 예제를 보겠습니다 수정 (예를 들어 */HelloWorld/시작? 이름 = Scott&amp;numtimes = 4*). 변경에 `Welcome` 아래와 같이 두 개의 매개 변수를 포함 하는 방법입니다. VB 선택적 매개 변수 기능을 나타내는 했습니다는 참고를 `numTimes` 매개 변수는 기본적으로 1 값이 없는 매개 변수에 대해 전달 되 면 합니다.

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

응용 프로그램을 실행 하 고 이동할 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **합니다.** 다른 값을 사용할 수 있습니다 `name` 고 `numtimes`입니다. 시스템에는 메서드의 매개 변수를 쿼리 문자열의 주소 표시줄에서 명명 된 매개 변수를 자동으로 매핑합니다.

![](adding-a-controller/_static/image7.png)

이러한 두 예제에서 컨트롤러 작업을 수행 VC 부분 MVC-보기 및 컨트롤러 작업입니다. 컨트롤러 HTML을 직접 반환 됩니다. 일반적으로 HTML을 직접 반환 코드에 번거로운 복잡해 지므로 컨트롤러 않으려 합니다. 대신 일반적으로 별도 뷰 템플릿 파일을 HTML 응답을 생성 하는 데 사용 됩니다. 어떻게이 위해서는 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](intro-to-aspnet-mvc-3.md)
> [다음](adding-a-view.md)
