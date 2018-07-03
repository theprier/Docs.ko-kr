---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 단위 테스트 ASP.NET Web API 2 | Microsoft Docs
author: tfitzmac
description: 이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 이 자습서에서는 단위 테스트 프로젝트를 포함 하는 방법을 보여 줍니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/05/2014
ms.topic: article
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: da56b38809faf760b7c390eb76ac9c4556d635c6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376176"
---
<a name="unit-testing-aspnet-web-api-2"></a>단위 테스트 ASP.NET Web API 2
====================
[Tom FitzMacken](https://github.com/tfitzmac)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> 이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 이 자습서에서는 솔루션에 단위 테스트 프로젝트를 포함 하 고 컨트롤러 메서드에서 반환된 된 값을 확인 하는 테스트 메서드를 작성 하는 방법을 보여 줍니다.
> 
> 이 자습서에서는 ASP.NET Web API의 기본 개념에 익숙하다고 가정 합니다. 입문 용 자습서는를 참조 하세요 [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.
> 
> 이 항목의 단위 테스트를 간단한 데이터 시나리오를 의도적으로 제한 됩니다. 고급 데이터 시나리오를 테스트 하는 장치에 대 한 참조 [Entity Framework 머킹 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2017](https://www.visualstudio.com/vs/)
> - Web API 2


## <a name="in-this-topic"></a>항목 내용

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [필수 조건](#prereqs)
- [코드 다운로드](#download)
- [단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기](#appwithunittest)

    - [응용 프로그램을 만들 때 단위 테스트 프로젝트 추가](#whencreate)
    - [기존 응용 프로그램에 단위 테스트 프로젝트 추가](#addtoexisting)
- [Web API 2 응용 프로그램 설정](#setupproject)
- [테스트 프로젝트에서 NuGet 패키지를 설치 합니다.](#testpackages)
- [테스트 만들기](#tests)
- [테스트 실행](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>전제 조건

Visual Studio 2017 Community, Professional 또는 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>코드 다운로드

다운로드 합니다 [완성 된 프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)합니다. 다운로드 가능한 프로젝트 및이 항목에 대 한 단위 테스트 코드를 포함 합니다 [Entity Framework 머킹 때 단위 테스트 ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) 항목입니다.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기

응용 프로그램을 만들 때 단위 테스트 프로젝트 만들기 또는 기존 응용 프로그램에 단위 테스트 프로젝트를 추가 합니다. 이 자습서에는 단위 테스트 프로젝트를 만드는 방법을 모두 보여 줍니다. 이 자습서를 수행 하려면 방법 중 하나를 사용할 수 있습니다.

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>응용 프로그램을 만들 때 단위 테스트 프로젝트 추가

명명 된 새 ASP.NET 웹 응용 프로그램 만들기 **StoreApp**합니다.

![프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image1.png)

새 ASP.NET 프로젝트 창에서 선택 합니다 **빈** 템플릿 폴더를 추가 하 고 웹 API에 대 한 참조를 핵심입니다. 선택 된 **단위 테스트 추가** 옵션입니다. 단위 테스트 프로젝트 이름은 자동으로 **StoreApp.Tests**합니다. 이 이름을 유지할 수 있습니다.

![단위 테스트 프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image2.png)

응용 프로그램을 만든 후 두 개의 프로젝트가 포함 된 표시 됩니다.

![두 프로젝트](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>기존 응용 프로그램에 단위 테스트 프로젝트 추가

응용 프로그램을 만들 때에 단위 테스트 프로젝트를 만들지 않은, 경우 언제 든 지 추가할 수 있습니다. 예를 들어 이미 StoreApp, 명명 된 응용 프로그램 및 단위 테스트를 추가. 단위 테스트 프로젝트를 추가 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 하 고 **새 프로젝트**합니다.

![솔루션에 새 프로젝트 추가](unit-testing-with-aspnet-web-api/_static/image4.png)

선택 **테스트** 선택한 왼쪽된 창의 **단위 테스트 프로젝트** 프로젝트 형식에 대 한 합니다. 프로젝트 이름을 **StoreApp.Tests**합니다.

![단위 테스트 프로젝트 추가](unit-testing-with-aspnet-web-api/_static/image5.png)

솔루션에 단위 테스트 프로젝트가 표시 됩니다.

단위 테스트 프로젝트에서 원래 프로젝트에 대 한 프로젝트 참조를 추가 합니다.

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>Web API 2 응용 프로그램 설정

StoreApp 프로젝트에서 클래스 파일을 추가 합니다 **모델** 폴더가 **Product.cs**합니다. 파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

솔루션을 빌드합니다.

컨트롤러 폴더를 마우스 오른쪽 단추로 누르고 **추가** 하 고 **새 스 캐 폴드 된 항목**합니다. 선택 **Web API 2 컨트롤러-비어 있음을**합니다.

![새 컨트롤러 추가](unit-testing-with-aspnet-web-api/_static/image6.png)

컨트롤러 이름으로 설정할 **SimpleProductController**, 클릭 **추가**합니다.

![컨트롤러를 지정 합니다.](unit-testing-with-aspnet-web-api/_static/image7.png)

기존 코드를 다음 코드로 바꿉니다. 를 간소화 하기 위해이 예제 데이터는 데이터베이스 보다는 목록에 저장 됩니다. 이 클래스에 정의 된 목록에는 프로덕션 데이터를 나타냅니다. 컨트롤러 제품 개체의 목록이 매개 변수로 사용 하는 생성자에 포함 되어 있는지 확인 합니다. 이 생성자를 사용 하면 테스트 데이터를 전달할 때 단위 테스트 합니다. 컨트롤러는 또한 두 개의 **비동기** 비동기 메서드를 테스트 하는 단위를 설명 하는 방법입니다. 이러한 비동기 메서드를 호출 하 여 구현한 **Task.FromResult** 불필요 한 코드 이지만, 일반적으로 메서드를 최소화 하기 위해 리소스 집약적 작업이 포함 됩니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

GetProduct 메서드의 인스턴스를 반환 합니다 **IHttpActionResult** 인터페이스입니다. IHttpActionResult을 사용 하면 Web API 2의 새로운 기능 중 하나인 및 단위 테스트 개발을 간소화 합니다. IHttpActionResult 인터페이스를 구현 하는 클래스에서 발견 되는 [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) 네임 스페이스입니다. 이러한 클래스는 작업 요청 으로부터 가능한 응답 나타내고 HTTP 상태 코드에 해당 합니다.

솔루션을 빌드합니다.

이제 테스트 프로젝트를 설정할 준비가 되었습니다.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>테스트 프로젝트에서 NuGet 패키지를 설치 합니다.

빈 템플릿을 사용 하 여 응용 프로그램을 만들 때 단위 테스트 프로젝트 (StoreApp.Tests)는 설치 된 모든 NuGet 패키지를 포함 하지 않습니다. Web API 템플릿과 같은 다른 템플릿을 단위 테스트 프로젝트에 일부 NuGet 패키지를 포함합니다. 이 자습서에서는 Microsoft ASP.NET 웹 API 2 코어 패키지를 테스트 프로젝트를 포함 해야 합니다.

StoreApp.Tests 프로젝트를 마우스 오른쪽 단추로 누르고 **NuGet 패키지 관리**합니다. 해당 프로젝트에 패키지를 추가 하려면 StoreApp.Tests 프로젝트를 선택 해야 합니다.

![패키지 관리](unit-testing-with-aspnet-web-api/_static/image8.png)

찾기 및 Microsoft ASP.NET 웹 API 2 코어 패키지를 설치 합니다.

![웹 api core 패키지를 설치 합니다.](unit-testing-with-aspnet-web-api/_static/image9.png)

NuGet 패키지 관리 창을 닫습니다.

<a id="tests"></a>
## <a name="create-tests"></a>테스트 만들기

테스트 프로젝트는 기본적으로 UnitTest1.cs 이라는 빈 테스트 파일을 포함 합니다. 이 파일을 사용 하면 테스트 메서드를 만들 특성을 보여 줍니다. 단위 테스트에 대 한이 파일을 사용 하거나 사용자 고유의 파일을 만듭니다.

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

이 자습서에서는 사용자 고유의 테스트 클래스를 만듭니다. UnitTest1.cs 파일을 삭제할 수 있습니다. 라는 클래스를 추가 **TestSimpleProductController.cs**, 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>테스트 실행

이제 테스트를 실행할 준비가 되었습니다. 로 표시 되는 메서드의 모든 합니다 **TestMethod** 특성을 테스트 합니다. **테스트** 메뉴 항목, 테스트를 실행 합니다.

![테스트 실행](unit-testing-with-aspnet-web-api/_static/image11.png)

열기는 **테스트 탐색기** 창 테스트의 결과 확인 합니다.

![테스트 결과](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>요약

이 자습서를 완료 했습니다. 이 자습서의 데이터는 단위 테스트 조건에 초점을 맞춰 의도적으로 단순화 되었습니다. 고급 데이터 시나리오를 테스트 하는 장치에 대 한 참조 [Entity Framework 머킹 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.
