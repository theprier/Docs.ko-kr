---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 데이터 액세스 레이어 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 5b4bb5bc89938836bc37e8ebd385fa966bc6f511
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390040"
---
<a name="create-the-data-access-layer"></a>데이터 액세스 레이어 만들기
====================
[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에는 만들기, 액세스 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터베이스에서 데이터를 검토 하는 방법을 설명 합니다. 이 자습서는 이전 자습서 "프로젝트 만들기"를 기반 하 고 Wingtip 장난감 자습서 시리즈의 일부입니다. 이 자습서를 완료 하는 만든 데이터 액세스 클래스에 있는 그룹에는 *모델* 프로젝트의 폴더입니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 데이터 모델을 만드는 방법입니다.
- 데이터베이스를 만들고 초기화 하는 방법.
- 업데이트 및 데이터베이스를 지원 하도록 응용 프로그램을 구성 하는 방법입니다.

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>다음은 자습서에서 도입 된 기능입니다.

- Entity Framework Code First
- LocalDB
- 데이터 주석

## <a name="creating-the-data-models"></a>데이터 모델 만들기

[Entity Framework](https://msdn.microsoft.com/data/aa937723) 는 (ORM) 개체-관계형 매핑 프레임 워크입니다. 일반적으로 작성 해야 하는 데이터 액세스 코드가 대부분 제거 개체로 관계형 데이터로 작업할 수 있습니다. Entity Framework를 사용 하 여를 사용 하 여 쿼리를 실행할 수 있습니다 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), 다음 검색 및 강력한 형식의 개체로 데이터를 조작 합니다. LINQ는 데이터 쿼리 및 업데이트에 대 한 패턴을 제공 합니다. Entity Framework를 사용 하 여 액세스 기초를 데이터에 집중 하는 것이 아니라 응용 프로그램의 나머지 부분을 만드는 데 집중할 수 있습니다. 이 자습서 시리즈의 뒷부분에 나오는 데이터 탐색 및 제품 쿼리를 채우는 데 사용 하는 방법을 살펴보겠습니다.

Entity Framework 지원 호출 하는 개발 패러다임 *Code First*합니다. 먼저 코드에서는 클래스를 사용 하 여 데이터 모델을 정의할 수 있습니다. 클래스는 다른 형식, 메서드 및 이벤트 변수를 그룹화 하 여 사용자 고유의 사용자 지정 형식을 만들 수 있는 구문. 기존 데이터베이스에 클래스를 매핑할 수도 있고 하는 데이터베이스를 생성 하는 데 사용할 수 있습니다. 이 자습서에서는 데이터 모델 클래스를 작성 하 여 데이터 모델을 만들어야 합니다. 그런 다음 Entity Framework에서 이러한 새 클래스를 즉석에서 데이터베이스를 만들 수 있게 됩니다.

Web Forms 응용 프로그램에 대 한 데이터 모델을 정의 하는 엔터티 클래스를 만들어 시작 합니다. 그런 다음 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 상황에 맞는 클래스를 만들게 됩니다. 또한 데이터베이스를 채우는 데 사용할 이니셜라이저 클래스를 만듭니다.

### <a name="entity-framework-and-references"></a>엔터티 프레임 워크 및 참조

기본적으로 Entity Framework는 포함 된 새 만들면 **ASP.NET 웹 응용 프로그램** 사용 하는 **Web Forms** 템플릿. Entity Framework는 설치, 제거 및 NuGet 패키지로 업데이트 될 수 있습니다.

이 NuGet 패키지에는 다음과 같습니다 **런타임** 프로젝트 내에서 어셈블리:

- EntityFramework.dll – 모든 공용 런타임 코드가 Entity Framework 사용
- EntityFramework.SqlServer.dll-Entity Framework 용 Microsoft SQL Server 공급자

### <a name="entity-classes"></a>엔터티 클래스

데이터의 스키마를 정의 하기 위해 만든 클래스에는 엔터티 클래스 라고 합니다. 데이터베이스 디자인을 처음 접하는 경우 데이터베이스의 테이블 정의로 엔터티 클래스의 생각 합니다. 클래스의 각 속성 데이터베이스의 테이블의 열을 지정 합니다. 이러한 클래스는 개체 지향 코드와 데이터베이스의 관계형 테이블 구조 개체-관계형 간단한 인터페이스를 제공합니다.

이 자습서에서는 제품 및 범주에 대 한 스키마를 나타내는 간단한 엔터티 클래스를 추가 하 여 시작 합니다. Products 클래스에는 각 제품에 대 한 정의가 포함 됩니다. 각 product 클래스의 멤버의 이름은 `ProductID`, `ProductName`, `Description`, `ImagePath`를 `UnitPrice`를 `CategoryID`, 및 `Category`합니다. 범주 클래스에 속하는 제품 수, 자동차, 보트, 평면 등 각 범주에 대 한 정의가 포함 됩니다. 범주 클래스의 멤버는 각각의 이름은 `CategoryID`, `CategoryName`를 `Description`, 및 `Products`합니다. 각 제품 범주 중 하나에 속하게 됩니다. 이러한 엔터티 클래스는 프로젝트의 기존에 추가할 *모델* 폴더입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 하 고 **추가**  - &gt; **새 항목**합니다. 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image1.png)

   **새 항목 추가** 대화 상자가 표시됩니다.
2. 아래 **Visual C#** 에서 합니다 **설치 됨** 창 왼쪽에서 선택 **코드**합니다. 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image2.png)
3. 선택 **클래스** 가운데 창에서이 새 클래스 이름을 *Product.cs*합니다.
4. **추가**를 클릭합니다.  
   새 클래스 파일을 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 1 ~ 4 단계에는 있지만 새 클래스 이름을 반복 하 여 다른 클래스를 만듭니다 *Category.cs* 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

에서 설명한 대로 합니다 `Category` 클래스는 응용 프로그램 제품 유형을 판매할 하도록 설계 되었습니다 (같은 <a id="a"> </a> &quot;자동차&quot;, &quot;배&quot;, &quot;로켓&quot;등), 및 `Product` 클래스는 데이터베이스의 개별 제품 (toys)를 나타냅니다. 각 인스턴스는 `Product` 관계형 데이터베이스 테이블 내의 행에 해당 개체 및 Product 클래스의 각 속성은 관계형 데이터베이스 테이블의 열에 매핑됩니다. 이 자습서의 뒷부분에서 데이터베이스에 포함 된 제품 데이터를 검토할 수 있습니다.

### <a name="data-annotations"></a>데이터 주석

알 수 있습니다 클래스의 특정 멤버와 같은 멤버에 대 한 세부 정보를 지정 하는 특성이 있는 `[ScaffoldColumn(false)]`합니다. 이들은 *데이터 주석*합니다. 데이터 주석 특성, 형식 지정 하 고 데이터베이스를 만들 때 모델링 되는 방법을 지정 하는 멤버에 대 한 사용자 입력의 유효성을 검사 하는 방법을 설명할 수 있습니다.

### <a name="context-class"></a>Context 클래스

데이터 액세스를 위한 클래스를 사용 하려면 상황에 맞는 클래스를 정의 해야 합니다. 이전에 설명한 대로 컨텍스트 클래스가 엔터티 클래스를 관리 하는 (같은 합니다 `Product` 클래스 및 `Category` 클래스) 하 고 데이터베이스에 대 한 데이터 액세스를 제공 합니다.

이 절차에서는 새 C# 상황에 맞는 클래스를 추가 합니다 *모델* 폴더입니다.

1. 마우스 오른쪽 단추로 클릭 합니다 *모델* 한 다음 선택한 폴더 **추가**  - &gt; **새 항목**합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 **클래스** 이름을 가운데 창에서 *ProductContext.cs* 누릅니다 **추가**합니다.
3. 다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

이 코드를 추가 합니다 `System.Data.Entity` 네임 스페이스 쿼리 하는 기능을 포함 하는 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 합니다.

`ProductContext` 페치, 저장 및 업데이트를 처리 하는 Entity Framework 제품 데이터베이스 컨텍스트 클래스를 나타냅니다 `Product` 클래스 인스턴스의 데이터베이스에 있습니다. 합니다 `ProductContext` 클래스에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.

### <a name="initializer-class"></a>이니셜라이저 클래스

초기화 컨텍스트에서 사용 되는 첫 번째 데이터베이스에 사용자 지정 논리를 실행 해야 합니다. 이렇게 하면 시드 된 데이터를 제품 및 범주를 즉시 표시할 수 있도록 데이터베이스에 추가할 수 있습니다.

이 절차에서는 새 C# 이니셜라이저 클래스를 추가 합니다 *모델* 폴더입니다.

1. 만들면 `Class` 에 *모델* 폴더 이름을 *ProductDatabaseInitializer.cs*합니다.
2. 다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

데이터베이스를 생성 하 고 초기화 하는 경우 위의 코드에서 볼 수는 `Seed` 속성은 재정의 하 고 설정 합니다. 경우는 `Seed` 속성, 범주 및 제품에서 값이 데이터베이스를 채우는 데 사용 됩니다. 데이터베이스가 만들어진 후에 위의 코드를 수정 하 여 시드 데이터를 업데이트 하려고 하면 웹 응용 프로그램을 실행 하는 경우 업데이트가 표시 되지 않습니다. 이유는 위 코드의 구현을 사용 합니다 `DropCreateDatabaseIfModelChanges` 모델 (스키마) 시드 데이터를 다시 설정 하기 전에 변경 되었는지 여부를 인식 하는 클래스입니다. 에 변경 된 경우는 `Category` 고 `Product` 시드 데이터를 사용 하 여 엔터티 클래스를 데이터베이스 다시 초기화 해야 합니다.

> [!NOTE] 
> 
> 응용 프로그램을 실행 될 때마다 다시 생성 하려면 데이터베이스를 하려는 경우, 사용할 수 있습니다 합니다 `DropCreateDatabaseAlways` 클래스 대신는 `DropCreateDatabaseIfModelChanges` 클래스입니다. 그러나이 자습서 시리즈에서는 사용 된 `DropCreateDatabaseIfModelChanges` 클래스입니다.


이 시점에서이 자습서에서는 해야는 *모델* 네 개의 새로운 클래스 및 기본 클래스를 사용 하 여 폴더:

![데이터 액세스 계층-Models 폴더 만들기](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>데이터 모델을 사용 하도록 응용 프로그램 구성

데이터를 나타내는 클래스를 만들었으므로 이제 클래스를 사용 하 여 응용 프로그램을 구성 해야 합니다. 에 *Global.asax* 파일 모델을 초기화 하는 코드를 추가 합니다. 에 *Web.config* 어떤 데이터베이스 응용 프로그램에 알려 주는 정보를 사용 하 여 새 데이터 클래스에 의해 표현 되는 데이터를 저장 하는 것이 추가한 파일입니다. 합니다 *Global.asax* 응용 프로그램 이벤트 또는 메서드를 처리 하도록 파일을 사용할 수 있습니다. 합니다 *Web.config* 파일을 사용 하면 ASP.NET 웹 응용 프로그램의 구성을 제어할 수 있습니다.

#### <a name="updating-the-globalasax-file"></a>Global.asax 파일 업데이트

업데이트 파일을 시작 하면 응용 프로그램 데이터 모델을 초기화 하려면 합니다 `Application_Start` 처리기에는 *Global.asax.cs* 파일입니다.

> [!NOTE] 
> 
> 솔루션 탐색기에서 선택할 수 있습니다 합니다 *Global.asax* 파일 또는 *Global.asax.cs* 파일을 편집 합니다 *Global.asax.cs* 파일.


1. 노란색으로 강조 표시 된 다음 코드를 추가 합니다 `Application_Start` 의 메서드를 *Global.asax.cs* 파일입니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> 브라우저는 HTML5는 브라우저에서이 자습서 시리즈를 보고 하는 경우 노란색으로 강조 표시 하는 코드를 보려면 지원 해야 합니다.


위의 코드에서 응용 프로그램을 시작 하는 경우와 같이 응용 프로그램 액세스 하는 데이터 중 처음으로 실행 되는 이니셜라이저를 지정 합니다. 두 개의 추가 네임 스페이스 액세스 해야 하는 `Database` 개체 및 `ProductDatabaseInitializer` 개체입니다.

 Web.Config 파일 수정 

Entity Framework Code First는 생성 하지만 데이터베이스를 기본 위치에 데이터베이스 시드 데이터를 사용 하 여 채워질 때 응용 프로그램에 직접 연결 정보를 추가 하면 데이터베이스 위치를 제어 합니다. 응용 프로그램의 연결 문자열을 사용 하 여이 데이터베이스 연결을 지정할 *Web.config* 프로젝트의 루트에 있는 파일입니다. 새 연결 문자열에 추가 하 여 데이터베이스의 위치를 지정할 수 있습니다 (*wingtiptoys.mdf*) 응용 프로그램의 데이터 디렉터리에 빌드할 (*앱\_데이터*), 기본값 대신 위치입니다. 이렇게 변경 하면를 찾고이 자습서의 뒷부분에서 데이터베이스 파일을 검사할 수 있습니다.

1. **솔루션 탐색기**찾기 및 열기, 합니다 *Web.config* 파일입니다.
2. 노란색으로 강조 표시 된 연결 문자열을 추가 합니다 `<connectionStrings>` 의 섹션을 *Web.config* 다음과 같이 파일:  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

응용 프로그램을 처음으로 실행 하는 경우 데이터베이스 연결 문자열에서 지정 된 위치에 빌드됩니다. 하지만 응용 프로그램을 실행 하기 전에 빌드 해 보겠습니다 것 먼저 합니다.

## <a name="building-the-application"></a>응용 프로그램 빌드

모든 클래스 및 웹 응용 프로그램에 대 한 변경 내용을 올바르게 작동 하는지, 응용 프로그램이 빌드되어야 합니다.

1. **디버그** 메뉴에서 **빌드 WingtipToys**합니다.  
 합니다 **출력** 창이 표시 되 고 순조롭게 경우 표시는 *성공* 메시지입니다.  

    ![출력 Windows 데이터 액세스 계층-만들기](create_the_data_access_layer/_static/image4.png)

오류를 실행 하는 경우 위의 단계를 다시 확인 합니다. 정보는 **출력** 파일에 문제가 있어 파일에 변경 내용을 필요한 경우 창이 표시 됩니다. 이 정보를 사용 하면 부분 위 단계를 검토 하 고 프로젝트에서 수정 해야 결정할 수 있습니다.

## <a name="summary"></a>요약

이 자습서 시리즈의 수 있는 데이터 모델을 만들 뿐 데이터베이스를 만들고 초기화 하는 데 사용할 코드를 추가 합니다. 또한 응용 프로그램이 실행 될 때 데이터 모델을 사용 하도록 응용 프로그램을 구성 했습니다.

다음 자습서에서는 UI를 업데이트, 추가 탐색 하 고 데이터베이스에서 데이터를 검색 합니다. 그러면이 자습서에서 만든 엔터티 클래스에 따라 자동으로 생성 되는 데이터베이스입니다.

## <a name="additional-resources"></a>추가 리소스

[Entity Framework 개요](https://msdn.microsoft.com/library/bb399567.aspx)   
[ADO.NET Entity Framework 초보자 가이드](https://msdn.microsoft.com/data/ee712907)   
[Entity Framework를 사용 하 여 첫 번째 개발 코드](http://www.msteched.com/2010/Europe/DEV212) (비디오)   
[Code First 관계 Fluent API](https://msdn.microsoft.com/data/hh134698)   
[Code First 데이터 주석](https://msdn.microsoft.com/data/gg193958)  
[Entity Framework에 대 한 생산성 향상](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [이전](create-the-project.md)
> [다음](ui_and_navigation.md)
