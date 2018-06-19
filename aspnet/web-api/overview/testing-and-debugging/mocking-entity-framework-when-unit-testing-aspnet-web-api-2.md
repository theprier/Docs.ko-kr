---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Entity Framework를 모의 때 단위 테스트 ASP.NET Web API 2 | Microsoft Docs
author: tfitzmac
description: 이 지침과 응용 프로그램에는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다. 수정 하는 방법을 보여 줍니다는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/13/2013
ms.topic: article
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: abfde7edec85812de3560f4edefb110c3e374580
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
ms.locfileid: "29152867"
---
<a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>Entity Framework를 모의 때 단위 테스트 ASP.NET Web API 2
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> 이 지침과 응용 프로그램에는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다. 테스트를 위해 컨텍스트 개체를 전달할 수 있도록 스 캐 폴드 컨트롤러를 수정 하는 방법과 Entity Framework와 함께 작동 하는 테스트 개체를 만드는 방법을 보여 줍니다.
> 
> ASP.NET Web API를 사용한 단위 테스트에 대 한 소개를 참조 하십시오. [ASP.NET Web API 2를 사용 하 여 단위 테스트](unit-testing-with-aspnet-web-api.md)합니다.
> 
> 이 자습서에서는 ASP.NET Web API의 기본 개념에 익숙한 가정 합니다. 있는 소개 자습서를 참조 하십시오. [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.
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
- [모델 클래스 만들기](#modelclass)
- [컨트롤러 추가](#controller)
- [추가 종속성 주입](#dependency)
- [테스트 프로젝트에서 NuGet 패키지를 설치 합니다.](#testpackages)
- [테스트 컨텍스트 만들기](#testcontext)
- [테스트 만들기](#tests)
- [테스트 실행](#runtests)

단계를 이미 완료 한 경우 [ASP.NET Web API 2를 사용 하 여 단위 테스트](unit-testing-with-aspnet-web-api.md), 섹션으로 건너뛸 수 [컨트롤러 추가](#controller)합니다.

<a id="prereqs"></a>
## <a name="prerequisites"></a>필수 구성 요소

Visual Studio 2017 Community, Professional 또는 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>코드 다운로드

다운로드는 [완료 된 프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)합니다. 및이 항목에 대 한 단위 테스트 코드를 포함 하는 다운로드 가능한 프로젝트는 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) 항목입니다.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>응용 프로그램 단위 테스트 프로젝트 만들기

응용 프로그램을 만들 때 단위 테스트 프로젝트를 만들 하거나 기존 응용 프로그램 단위 테스트 프로젝트를 추가할 수 있습니다. 이 자습서에서는 응용 프로그램을 만들 때 단위 테스트 프로젝트를 만드는 합니다.

라는 새 ASP.NET 웹 응용 프로그램 만들기 **StoreApp**합니다.

새 ASP.NET 프로젝트 창, 선택는 **빈** 템플릿 폴더를 추가 하 고 웹 API에 대 한 참조를 핵심입니다. 선택 된 **단위 테스트 추가** 옵션입니다. 단위 테스트 프로젝트의 이름이 자동으로 **StoreApp.Tests**합니다. 이 이름을 유지할 수 있습니다.

![단위 테스트 프로젝트 만들기](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

응용 프로그램을 만든 후 나타납니다-두 개의 프로젝트가 포함 된 **StoreApp** 및 **StoreApp.Tests**합니다.

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>모델 클래스 만들기

StoreApp 프로젝트에 클래스 파일을 추가 **모델** 라는 폴더 **Product.cs**합니다. 파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

솔루션을 빌드합니다.

<a id="controller"></a>
## <a name="add-the-controller"></a>컨트롤러 추가

Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 및 **스 캐 폴드 된 새 항목**합니다. Entity Framework를 사용 하 여 동작이 포함 된 Web API 2 컨트롤러를 선택 합니다.

![새 컨트롤러 추가](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

다음 값을 설정합니다.

- 컨트롤러 이름: **ProductController**
- 모델 클래스: **제품**
- 데이터 컨텍스트 클래스: [선택 **새 데이터 컨텍스트에** 아래 에서처럼 값을 입력 하는 단추]

![컨트롤러를 지정 합니다.](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

클릭 **추가** 컨트롤러 자동으로 생성 된 코드를 만들려고 합니다. 코드 생성, 검색, 업데이트 및 제품 클래스의 인스턴스를 삭제 하기 위한 메서드를 포함 합니다. 다음 코드는 메서드를 보여 줍니다.에 대 한 제품을 추가 합니다. 메서드가의 인스턴스를 반환 한다고 확인 **IHttpActionResult**합니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

IHttpActionResult Web API 2의 새로운 기능 중 하나 이며 단위 테스트 개발을 간소화 합니다.

다음 섹션에서 사용자 지정할 용이 하 게 생성 된 코드는 컨트롤러에 테스트 개체를 전달 합니다.

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>추가 종속성 주입

현재 ProductController 클래스 StoreAppContext 클래스의 인스턴스를 사용 하도록 하드 코드입니다. 응용 프로그램을 수정 하 고 해당 하드 코드 된 종속성을 제거 하는 종속성 주입 이라는 패턴을 사용 합니다. 이 종속성을 끊음 으로써 테스트할 때 모의 개체에 전달할 수 있습니다.

마우스 오른쪽 단추로 클릭는 **모델** 폴더 라는 새 인터페이스를 추가 하 고 **IStoreAppContext**합니다.

코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

StoreAppContext.cs 파일을 열고 다음 강조 표시 된 변경 합니다. 에 중요 한 변경이 합니다.

- StoreAppContext 클래스 IStoreAppContext 인터페이스를 구현합니다.
- MarkAsModified 메서드는 구현


[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

ProductController.cs 파일을 엽니다. 강조 표시 된 코드와 일치 하도록 기존 코드를 변경 합니다. 이러한 변경 내용은 StoreAppContext에 종속성을 해제 하 고 상황에 맞는 클래스에 대 한 다른 개체에 전달 하는 다른 클래스를 사용 하도록 설정 합니다. 이렇게이 변경을 사용 하면 단위 테스트 중 테스트 컨텍스트에 전달할 수 있습니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

ProductController에서 수행 해야 하는 한 가지 더 많은 변경이 있습니다. 에 **PutProduct** 메서드, replace 엔터티 상태를 설정 하는 줄 MarkAsModified 메서드를 호출 하 여 수정 합니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

솔루션을 빌드합니다.

이제 테스트 프로젝트를 설정할 준비가 되었습니다.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>테스트 프로젝트에서 NuGet 패키지를 설치 합니다.

빈 서식 파일을 사용 하 여 응용 프로그램을 만들 때 단위 테스트 프로젝트 (StoreApp.Tests)는 모든 설치 된 NuGet 패키지를 포함 하지 않습니다. 단위 테스트 프로젝트에서 일부 NuGet 패키지를 포함 하는 Web API 템플릿 같은 다른 서식 파일. 이 자습서에서는 Entity Framework packge와 테스트 프로젝트에 Microsoft ASP.NET Web API 2 Core 패키지를 포함 해야 합니다.

StoreApp.Tests 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 해당 프로젝트에 패키지를 추가 하려면 StoreApp.Tests 프로젝트를 선택 해야 합니다.

![패키지 관리](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

온라인 패키지를 찾아 EntityFramework 패키지 (버전 6.0 이상)를 설치 합니다. EntityFramework 패키지가 이미 설치 되어 있는지, 표시 되는 경우 StoreApp.Tests 프로젝트 대신 StoreApp 프로젝트를 선택 있을 수 있습니다.

![엔터티 프레임 워크 추가](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

찾기 및 Microsoft ASP.NET Web API 2 Core 패키지를 설치 합니다.

![web api core 패키지를 설치 합니다.](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

NuGet 패키지 관리 창을 닫습니다.

<a id="testcontext"></a>
## <a name="create-test-context"></a>테스트 컨텍스트 만들기

라는 클래스를 추가 **TestDbSet** 테스트 프로젝트에 있습니다. 이 클래스는 테스트 데이터 집합에 대 한 기본 클래스로 사용 됩니다. 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

라는 클래스를 추가 **TestProductDbSet** 다음 코드를 포함 하는 테스트 프로젝트에 있습니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

라는 클래스를 추가 **TestStoreAppContext** 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>테스트 만들기

기본적으로 테스트 프로젝트에 빈 테스트 파일인 **UnitTest1.cs**합니다. 이 파일을 사용 하면 테스트 메서드를 만들 특성을 보여 줍니다. 이 자습서에서는 새 테스트 클래스를 추가 하기 때문에이 파일을 삭제할 수 있습니다.

라는 클래스를 추가 **TestProductController** 테스트 프로젝트에 있습니다. 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>테스트 실행

이제 테스트를 실행할 준비가 되었습니다. 로 표시 된 메서드의 모든는 **TestMethod** 특성을 테스트 합니다. **테스트** 메뉴 항목을 테스트를 실행 합니다.

![테스트 실행](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

열기는 **테스트 탐색기** 창 테스트의 결과 확인 합니다.

![테스트 결과](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
