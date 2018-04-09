---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 데이터 액세스 계층 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 671d1bbf661dfb3e56c6ccd67ce0d383990918d6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="create-the-data-access-layer"></a>데이터 액세스 계층 만들기
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에는 만들기, 액세스 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터베이스에서 데이터를 검토 하는 방법을 설명 합니다. 이 자습서에서는 이전 자습서 "프로젝트 만들기"를 바탕으로 하며 Wingtip 장난감 저장소 자습서 시리즈의 일부입니다. 이 자습서를 완료 합니다 빌드에 있는 데이터 액세스 클래스 들의 그룹은 *모델* 프로젝트의 폴더입니다.

## <a name="what-youll-learn"></a>학습 내용:

- 데이터 모델을 만드는 방법.
- 초기화 하 고 데이터베이스를 시드하고 하는 방법.
- 업데이트 및 응용 프로그램 데이터베이스를 지원 하도록 구성 하는 방법.

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>다음은 자습서에 도입 된 기능입니다.

- Entity Framework Code First
- LocalDB
- 데이터 주석

## <a name="creating-the-data-models"></a>데이터 모델 만들기

[Entity Framework](https://msdn.microsoft.com/data/aa937723) (ORM) 개체-관계형 매핑 프레임 워크입니다. 관계형 데이터를 쓰려고 일반적으로 해야 하는 데이터 액세스 코드의 대부분 제거 개체로 작업할 수 있습니다. Entity Framework를 사용 하 여 사용 하 여 쿼리를 실행할 수 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), 다음 검색 및 강력한 형식의 개체로 데이터를 조작 합니다. LINQ 쿼리 및 데이터를 업데이트 하기 위한 패턴을 제공 합니다. Entity Framework를 사용 하 여 액세스 기초를 데이터에 집중 하는 대신 응용 프로그램의 나머지 부분을 만드는 데 집중할 수 있습니다. 이 자습서 시리즈의 뒷부분에 나오는 데이터 탐색 및 제품 쿼리를 채우는 데 사용 하는 방법을 살펴보겠습니다.

Entity Framework를 호출 하는 개발 패러다임 지원 *Code First*합니다. 먼저 코드에서는 클래스를 사용 하 여 데이터 모델을 정의할 수 있습니다. 클래스는 고유한 사용자 지정 형식을 다른 형식, 메서드 및 이벤트 변수를 함께 그룹화 하 여 만들 수 있도록 하는 구문입니다. 클래스는 기존 데이터베이스에 매핑하거나 데이터베이스를 생성 하는 데 사용할 수 있습니다. 이 자습서에서는 데이터 모델 클래스를 작성 하 여 데이터 모델 만듭니다. 그런 다음 이러한 새 클래스에서 즉석에서 데이터베이스를 생성 하는 Entity Framework 해보겠습니다.

Web Forms 응용 프로그램에 대 한 데이터 모델을 정의 하는 엔터티 클래스를 만들어 시작 합니다. 그런 다음 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 컨텍스트 클래스를 만듭니다. 데이터베이스를 채우는 데 사용할 이니셜라이저 클래스도를 만들어집니다.

### <a name="entity-framework-and-references"></a>엔터티 프레임 워크 및 참조

기본적으로 Entity Framework는 포함 된 새를 만들 때 **ASP.NET 웹 응용 프로그램** 를 사용 하는 **Web Forms** 템플릿. Entity Framework 설치, 제거 및 NuGet 패키지를 업데이트할 수 있습니다.

이 NuGet 패키지에는 다음과 같은 **런타임** 프로젝트 내에서 어셈블리:

- EntityFramework.dll-모든 일반적인 런타임 코드 Entity Framework에서 사용 하는
- EntityFramework.SqlServer.dll – Entity Framework 용 Microsoft SQL Server 공급자

### <a name="entity-classes"></a>엔터티 클래스

데이터의 스키마를 정의 하기 위해 만드는 클래스는 엔터티 클래스 라고 합니다. 데이터베이스 디자인을 처음 접하는 경우 데이터베이스의 테이블 정의로 엔터티 클래스의 생각 합니다. 클래스의 각 속성은 데이터베이스의 테이블에 열을 지정합니다. 이러한 클래스는 개체 지향 코드와 데이터베이스의 관계형 테이블 구조는 간단 하 고 개체-관계형 인터페이스를 제공합니다.

이 자습서에서는 제품 및 범주에 대 한 스키마를 나타내는 간단한 엔터티 클래스를 추가 하 여 시작 합니다. 제품 클래스에는 각 제품에 대 한 정의가 포함 됩니다. 각 product 클래스 멤버의 이름은 됩니다 `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, 및 `Category`합니다. 범주 클래스에는 제품 자동차, 보트, 평면 등,에 속할 수 있는 각 범주에 대 한 정의가 포함 됩니다. 각 범주 클래스 멤버의 이름은 됩니다 `CategoryID`, `CategoryName`, `Description`, 및 `Products`합니다. 각 제품 범주 중 하나에 속하게 됩니다. 이러한 엔터티 클래스를 프로젝트의 기존 추가할 *모델* 폴더입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다. 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image1.png)

   **새 항목 추가** 대화 상자가 표시됩니다.
2. 아래 **Visual C#** 에서 **설치 됨** 선택 왼쪽 창에서 **코드**합니다. 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image2.png)
3. 선택 **클래스** 가운데 창에서이 새 클래스 이름 및 *Product.cs*합니다.
4. **추가**를 클릭합니다.  
   새 클래스 파일은 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 하지만 1-4 단계는, 새 클래스의 이름을 반복 하 여 다른 클래스를 만들 *Category.cs* 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

에서 설명한 대로 `Category` 클래스는 응용 프로그램은 제품의 형식은 판매할 디자인 (같은 <a id="a"> </a> &quot;자동차&quot;, &quot;배&quot;, &quot;로켓&quot;등), 및 `Product` 클래스는 데이터베이스에서 개별 제품 (toys)를 나타냅니다. 각 인스턴스는 `Product` 개체는 관계형 데이터베이스 테이블 내의 행에 해당 하 고 제품 클래스의 각 속성은 관계형 데이터베이스 테이블의 열에 매핑됩니다. 이 자습서의 뒷부분에 나오는 데이터베이스에 포함 된 제품 데이터를 검토 합니다.

### <a name="data-annotations"></a>데이터 주석

클래스의 특정 멤버와 같은 멤버에 대 한 세부 정보를 지정 하는 속성 한지 단어로 `[ScaffoldColumn(false)]`합니다. 이들은 *데이터 주석*합니다. 데이터 주석 특성,에 대 한 서식을 지정 하 고 데이터베이스를 만들 때 모델링 되는 방법을 지정 하려면 해당 멤버에 대 한 사용자 입력의 유효성을 검사 하는 방법을 설명 합니다.

### <a name="context-class"></a>Context 클래스

데이터 액세스를 위한 클래스를 사용 하 여을 시작 하려면 컨텍스트 클래스를 정의 해야 합니다. 컨텍스트 클래스는 엔터티 클래스를 관리에서 설명한 대로 (같은 `Product` 클래스 및 `Category` 클래스) 하 고 데이터베이스에 대 한 데이터 액세스를 제공 합니다.

새 C# 컨텍스트 클래스를 추가 하는이 절차는 *모델* 폴더입니다.

1. 마우스 오른쪽 단추로 클릭는 *모델* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 **클래스** 이름을 가운데 창에서 *ProductContext.cs* 클릭 **추가**합니다.
3. 다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

이 코드는 추가 `System.Data.Entity` 네임 스페이스를 쿼리 하는 기능을 포함 하는 Entity Framework의 모든 핵심 기능에 대 한 액세스를 마쳤으므로 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 합니다.

`ProductContext` 클래스 인출, 저장 및 업데이트 처리는 Entity Framework 제품 데이터베이스 컨텍스트를 나타내는 `Product` 클래스 인스턴스는 데이터베이스에 있습니다. `ProductContext` 클래스에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.

### <a name="initializer-class"></a>이니셜라이저 클래스

컨텍스트를 사용 하는 첫 번째 데이터베이스 시간을 초기화 하는 일부 사용자 지정 논리를 실행 해야 합니다. 이렇게 하면 데이터 제품 및 범주를 즉시 표시할 수 있도록 데이터베이스에 추가할 수 있습니다.

새 C# 이니셜라이저 클래스를 추가 하는이 절차는 *모델* 폴더입니다.

1. 다른 만들 `Class` 에 *모델* 폴더 이름을 지정 *ProductDatabaseInitializer.cs*합니다.
2. 다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

데이터베이스를 만들고 초기화 하는 위의 코드에서 볼 수 있듯이 `Seed` 속성을 재정의 하 고 설정 합니다. 경우는 `Seed` 속성이 설정 되어, 범주 및 제품에서 값이 데이터베이스를 채우는 데 사용 됩니다. 데이터베이스를 만든 후 위의 코드를 수정 하 여 시드 데이터를 업데이트 하려고 하면 웹 응용 프로그램을 실행 하면 모든 업데이트가 표시 되지 않습니다. 이유는 위의 코드 구현을 사용 하는 `DropCreateDatabaseIfModelChanges` (스키마) 모델에는 데이터를 다시 설정 하기 전에 변경 되었는지 여부를 인식 하는 클래스입니다. 에 변경 될 경우는 `Category` 및 `Product` 시드 데이터 엔터티 클래스, 데이터베이스, 다시 초기화 해야 합니다.

> [!NOTE] 
> 
> 응용 프로그램을 실행 될 때마다 다시 만들어야 하는 데이터베이스를 원하는 경우, 사용할 수는 `DropCreateDatabaseAlways` 클래스 대신는 `DropCreateDatabaseIfModelChanges` 클래스입니다. 그러나이 자습서 시리즈에 대 한 사용은 `DropCreateDatabaseIfModelChanges` 클래스입니다.


이 시점에서이 자습서에서는 나면는 *모델* 네 개의 새로운 클래스 및 하나의 기본 클래스를 사용한 폴더:

![데이터 액세스 계층-모델 폴더를 만듭니다.](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>데이터 모델을 사용 하 여 응용 프로그램 구성

데이터를 나타내는 클래스를 만들었으므로 이제 클래스를 사용 하는 응용 프로그램을 구성 해야 합니다. 에 *Global.asax* 모델을 초기화 하는 코드를 추가할 파일입니다. 에 *Web.config* 어떤 데이터베이스 응용 프로그램에 알려 주는 정보를 사용 하 여 새 데이터 클래스에 의해 표현 되는 데이터 저장을 추가할 파일입니다. *Global.asax* 응용 프로그램 이벤트 또는 메서드를 처리할 수 파일을 사용할 수 있습니다. *Web.config* 파일을 사용 하면 ASP.NET 웹 응용 프로그램의 구성을 제어할 수 있습니다.

#### <a name="updating-the-globalasax-file"></a>Global.asax 파일 업데이트

을 초기화 하기 위해 데이터 모델 시작 하면 응용 프로그램을 업데이트 하는 `Application_Start` 의 처리기는 *Global.asax.cs* 파일입니다.

> [!NOTE] 
> 
> 솔루션 탐색기에서 선택할 수 있습니다는 *Global.asax* 파일 또는 *Global.asax.cs* 편집할 파일의 *Global.asax.cs* 파일입니다.


1. 다음 코드를 노란색으로 강조 표시를 추가 `Application_Start` 에서 메서드는 *Global.asax.cs* 파일입니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> 브라우저는 HTML5 브라우저에서이 자습서 시리즈를 볼 때 노란색으로 강조 표시 하는 코드를 보려면를 지원 해야 합니다.


위의 코드는 응용 프로그램이 시작 될 때와 같이 이니셜라이저 중에 실행 되는 처음으로 데이터에 액세스 하는 응용 프로그램 지정 합니다. 두 개의 추가 네임 스페이스에 액세스 하는 데 필요한는 `Database` 개체 및 `ProductDatabaseInitializer` 개체입니다.

 Web.Config 파일 수정 

Entity Framework Code First는 생성 하지만 데이터베이스를 기본 위치에 데이터베이스 데이터도 채워질 때 응용 프로그램에 직접 연결 정보를 추가 하면 데이터베이스 위치를 제어 합니다. 응용 프로그램의 연결 문자열을 사용 하 여이 데이터베이스 연결을 지정 *Web.config* 프로젝트의 루트에 파일입니다. 새 연결 문자열을 추가 하 여 데이터베이스의 위치를 지정할 수 있습니다 (*wingtiptoys.mdf*) 응용 프로그램의 데이터 디렉터리에 빌드할 (*앱\_데이터*), 기본 대신 위치입니다. 이 변경을 적용 하면 검색 하 고이 자습서의 뒷부분에 나오는 데이터베이스 파일을 검사 합니다.

1. **솔루션 탐색기**찾기 및 열기는 *Web.config* 파일입니다.
2. 노란색으로 강조 표시 된 연결 문자열을 추가 `<connectionStrings>` 의 섹션은 *Web.config* 다음과 같이 파일:  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

응용 프로그램을 처음으로 실행 된 연결 문자열에서 지정 된 위치의 데이터베이스가 빌드됩니다. 하지만 응용 프로그램을 실행 하기 전에 제작 해 보겠습니다 것 먼저 합니다.

## <a name="building-the-application"></a>응용 프로그램 빌드

을 모든 클래스와 웹 응용 프로그램에 대 한 변경 내용이 작동 하는지 확인 하기 위해 응용 프로그램을 작성 해야 합니다.

1. **디버그** 메뉴 선택 **빌드 WingtipToys**합니다.  
 **출력** 창이 표시 되 고 순조롭게 경우 표시는 *성공* 메시지입니다.  

    ![데이터 액세스 계층-출력 창을 만들기](create_the_data_access_layer/_static/image4.png)

오류를 실행 하면 위의 단계를 다시 확인 합니다. 정보는 **출력** 에 문제가 되는 파일 및 파일의 변경이 필요한 경우 창을 표시 합니다. 이 정보를 사용 하면 위 단계 중 어떤 부분이 검토 하 고 프로젝트에서 수정 해야 할 수 있습니다.

## <a name="summary"></a>요약

계열의이 자습서에서는 있습니다가 데이터 모델을 만든 뿐만 아니라, 초기화 하 고 데이터베이스를 시드하고 사용할 코드를 추가 합니다. 또한 응용 프로그램이 실행 될 때 데이터 모델을 사용 하도록 응용 프로그램을 구성 했습니다.

다음 자습서에서는 UI를 업데이트, 추가 탐색 하 고 데이터베이스에서 데이터를 검색 합니다. 이렇게 하면이 자습서에서 만든 엔터티 클래스에 따라 자동으로 생성 되는 데이터베이스입니다.

## <a name="additional-resources"></a>추가 자료

[Entity Framework 개요](https://msdn.microsoft.com/library/bb399567.aspx)   
[ADO.NET Entity Framework에 대 한 기본 설명](https://msdn.microsoft.com/data/ee712907)   
[Entity Framework와 함께 첫 번째 개발 코드](http://www.msteched.com/2010/Europe/DEV212) (비디오)   
[코드 첫 번째 관계 Fluent API](https://msdn.microsoft.com/data/hh134698)   
[코드의 첫 번째 데이터 주석](https://msdn.microsoft.com/data/gg193958)  
[Entity Framework에 대 한 성능 향상 기능](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [이전](create-the-project.md)
> [다음](ui_and_navigation.md)
