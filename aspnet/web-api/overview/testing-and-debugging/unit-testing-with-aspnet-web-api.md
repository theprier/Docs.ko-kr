---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 단위 테스트 ASP.NET Web API 2 | Microsoft Docs
author: tfitzmac
description: 이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 단위 테스트 프로젝트를 포함 하는 방법을 보여 주는이 자습서 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/05/2014
ms.topic: article
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4d6102dd81589e41894d8ecd95bf9ddd761a65bd
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28042747"
---
<a name="unit-testing-aspnet-web-api-2"></a>단위 테스트 ASP.NET Web API 2
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> 이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 이 자습서, 솔루션의 단위 테스트 프로젝트를 포함 하 고 컨트롤러 메서드에서 반환 된 값을 확인 하는 테스트 메서드를 작성 하는 방법을 보여 줍니다.
> 
> 이 자습서에서는 ASP.NET Web API의 기본 개념에 익숙한 가정 합니다. 있는 소개 자습서를 참조 하십시오. [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.
> 
> 이 항목의 단위 테스트는 의도적으로 간단한 데이터 시나리오로 제한 합니다. 단위 테스트 고급 데이터 시나리오에 대 한 참조 [Entity Framework 모의 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2017](https://www.visualstudio.com/vs/)
> - Web API 2


## <a name="in-this-topic"></a>항목 내용

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [필수 조건](#prereqs)
- [코드 다운로드](#download)
- [응용 프로그램 단위 테스트 프로젝트 만들기](#appwithunittest)

    - [응용 프로그램을 만들 때 단위 테스트 프로젝트에 추가](#whencreate)
    - [기존 응용 프로그램에 단위 테스트 프로젝트 추가](#addtoexisting)
- [Web API 2 응용 프로그램 설정](#setupproject)
- [테스트 프로젝트에서 NuGet 패키지를 설치 합니다.](#testpackages)
- [테스트 만들기](#tests)
- [테스트 실행](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>필수 구성 요소

Visual Studio 2017 Community, Professional 또는 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>코드 다운로드

다운로드는 [완료 된 프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)합니다. 및이 항목에 대 한 단위 테스트 코드를 포함 하는 다운로드 가능한 프로젝트는 [Entity Framework 모의 때 단위 테스트 ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) 항목입니다.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>응용 프로그램 단위 테스트 프로젝트 만들기

응용 프로그램을 만들 때 단위 테스트 프로젝트를 만들 하거나 기존 응용 프로그램 단위 테스트 프로젝트를 추가할 수 있습니다. 이 자습서에는 단위 테스트 프로젝트를 만들기 위한 두 메서드 모두 보여 줍니다. 이 자습서를 수행 하려면 방법 중 하나를 사용할 수 있습니다.

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>응용 프로그램을 만들 때 단위 테스트 프로젝트에 추가

라는 새 ASP.NET 웹 응용 프로그램 만들기 **StoreApp**합니다.

![프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image1.png)

새 ASP.NET 프로젝트 창, 선택는 **빈** 템플릿 폴더를 추가 하 고 웹 API에 대 한 참조를 핵심입니다. 선택 된 **단위 테스트 추가** 옵션입니다. 단위 테스트 프로젝트의 이름이 자동으로 **StoreApp.Tests**합니다. 이 이름을 유지할 수 있습니다.

![단위 테스트 프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image2.png)

응용 프로그램을 만든 후 두 개의 프로젝트가 포함 된 표시 됩니다.

![두 개의 프로젝트](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>기존 응용 프로그램에 단위 테스트 프로젝트 추가

응용 프로그램을 만들 때 단위 테스트 프로젝트를 만들지 않은, 언제 든 지 추가할 수 있습니다. 예를 들어 StoreApp, 이라는 응용 프로그램에 이미 있는데 단위 테스트를 추가 합니다. 단위 테스트 프로젝트를 추가 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 및 **새 프로젝트**합니다.

![새 프로젝트를 솔루션에 추가](unit-testing-with-aspnet-web-api/_static/image4.png)

선택 **테스트** 고 왼쪽된 창에서 **단위 테스트 프로젝트** 프로젝트 형식에 대 한 합니다. 프로젝트 이름을 **StoreApp.Tests**합니다.

![단위 테스트 프로젝트에 추가](unit-testing-with-aspnet-web-api/_static/image5.png)

솔루션에 단위 테스트 프로젝트에 표시 됩니다.

단위 테스트 프로젝트에서 원래 프로젝트에 대 한 프로젝트 참조를 추가 합니다.

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>Web API 2 응용 프로그램 설정

StoreApp 프로젝트에 클래스 파일을 추가 **모델** 라는 폴더 **Product.cs**합니다. 파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

솔루션을 빌드합니다.

Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 및 **스 캐 폴드 된 새 항목**합니다. 선택 **Web API 2 컨트롤러-빈**합니다.

![새 컨트롤러 추가](unit-testing-with-aspnet-web-api/_static/image6.png)

컨트롤러 이름을 설정 **SimpleProductController**를 클릭 하 고 **추가**합니다.

![컨트롤러를 지정 합니다.](unit-testing-with-aspnet-web-api/_static/image7.png)

기존 코드를 다음 코드로 바꿉니다. 를 간소화 하기 위해이 예에서는 데이터는 데이터베이스 보다는 목록에 저장 됩니다. 이 클래스에 정의 된 목록이 프로덕션 데이터를 나타냅니다. 제품 개체 목록을 매개 변수로 사용 하는 생성자를 포함 하는 컨트롤러를 확인 합니다. 이 생성자를 사용 하면 테스트 데이터를 전달 하는 경우 단위 테스트 합니다. 컨트롤러도 두 개의 **비동기** 단위 테스트 비동기 메서드를 설명 하는 메서드. 이러한 비동기 메서드를 호출 하 여 구현 된 **Task.FromResult** 불필요 한 코드 있지만 일반적으로 메서드를 최소화 하기 위해 리소스 중심 작업을 포함 합니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

인스턴스를 반환 하는 GetProduct 메서드는 **IHttpActionResult** 인터페이스입니다. IHttpActionResult Web API 2의 새로운 기능 중 하나 이며 단위 테스트 개발을 간소화 합니다. IHttpActionResult 인터페이스를 구현 하는 클래스에서 발견 되는 [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) 네임 스페이스입니다. 이러한 클래스 동작 요청에 대 한 가능한 응답을 나타내고 HTTP 상태 코드에 해당 합니다.

솔루션을 빌드합니다.

이제 테스트 프로젝트를 설정할 준비가 되었습니다.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>테스트 프로젝트에서 NuGet 패키지를 설치 합니다.

빈 서식 파일을 사용 하 여 응용 프로그램을 만들 때 단위 테스트 프로젝트 (StoreApp.Tests)는 모든 설치 된 NuGet 패키지를 포함 하지 않습니다. 단위 테스트 프로젝트에서 일부 NuGet 패키지를 포함 하는 Web API 템플릿 같은 다른 서식 파일. 이 자습서에서는 Microsoft ASP.NET Web API 2 코어 패키지 테스트 프로젝트를 포함 해야 합니다.

StoreApp.Tests 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 해당 프로젝트에 패키지를 추가 하려면 StoreApp.Tests 프로젝트를 선택 해야 합니다.

![패키지 관리](unit-testing-with-aspnet-web-api/_static/image8.png)

찾기 및 Microsoft ASP.NET Web API 2 Core 패키지를 설치 합니다.

![web api core 패키지를 설치 합니다.](unit-testing-with-aspnet-web-api/_static/image9.png)

NuGet 패키지 관리 창을 닫습니다.

<a id="tests"></a>
## <a name="create-tests"></a>테스트 만들기

기본적으로 테스트 프로젝트 UnitTest1.cs 라는 빈 테스트 파일을 포함 합니다. 이 파일을 사용 하면 테스트 메서드를 만들 특성을 보여 줍니다. 단위 테스트에 대 한이 파일을 사용 하거나 직접 파일을 만듭니다.

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

이 자습서에서는 사용자 고유의 테스트 클래스를 만듭니다. UnitTest1.cs 파일을 삭제할 수 있습니다. 라는 클래스를 추가 **TestSimpleProductController.cs**, 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>테스트 실행

이제 테스트를 실행할 준비가 되었습니다. 로 표시 된 메서드의 모든는 **TestMethod** 특성을 테스트 합니다. **테스트** 메뉴 항목을 테스트를 실행 합니다.

![테스트 실행](unit-testing-with-aspnet-web-api/_static/image11.png)

열기는 **테스트 탐색기** 창 테스트의 결과 확인 합니다.

![테스트 결과](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>요약

이 자습서를 완료 했습니다. 이 자습서의 데이터는 단위 테스트 조건에 초점을 의도적으로 단순화 되었습니다. 단위 테스트 고급 데이터 시나리오에 대 한 참조 [Entity Framework 모의 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.
