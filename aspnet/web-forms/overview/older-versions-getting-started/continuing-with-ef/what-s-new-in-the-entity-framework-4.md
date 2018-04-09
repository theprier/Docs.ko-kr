---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: Entity Framework 4.0의에서 새로운 기능 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈 시작 하기에 의해 만들어진 Contoso 대학 웹 응용 프로그램 기반으로 합니다. I 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 04444ce98fa60045cf617a6c518dd55677258148
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="whats-new-in-the-entity-framework-40"></a>Entity Framework 4.0의에서 새로운 기능
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> 에 의해 만들어진 Contoso 대학 웹 응용 프로그램을 기반으로 하는이 자습서 시리즈의 [Entity Framework와 함께 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 점으로 하면 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 완료 하는 자습서 시리즈에서 만들어진 합니다. 이 자습서에 대 한 질문이 있으면에 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


이전 자습서에서 Entity Framework를 사용 하는 웹 응용 프로그램의 성능을 최대화 하는 몇 가지 방법을 살펴보았습니다. 이 자습서의 Entity Framework 버전 4에에서 가장 중요 한 새로운 기능 중 일부를 검토 하며 모든 새 기능에 대 한 자세한 소개를 제공 하는 리소스에 연결 합니다. 이 자습서에서는 강조 표시 된 기능은 다음과 같습니다.

- 외래 키 연결 합니다.
- 사용자 정의 SQL 명령을 실행 합니다.
- 모델 중심 개발 합니다.
- POCO 지원 합니다.

또한이 자습서에서는 간단 하 게 소개 *코드 중심 개발*, Entity Framework의 다음 릴리스에서 가져오는 기능입니다.

이 자습서를 시작 하려면 Visual Studio를 시작 하 고 이전 자습서에서 작업 하는 Contoso 대학 웹 응용 프로그램을 엽니다.

## <a name="foreign-key-associations"></a>외래 키 연결

Entity Framework 버전 3.5 탐색 속성을 포함 하지만 데이터 모델에 외래 키 속성을 포함 하지 않은 것입니다. 예를 들어는 `CourseID` 및 `StudentID` 의 열은 `StudentGrade` 테이블은 생략 됩니다는 `StudentGrade` 엔터티.

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

이 방법에 대 한 이유를 엄격히 말해서, 외래 키 물리적 구현 세부 정보를 개념적 데이터 모델에 속하지 않는 했습니다. 그러나 실제 문제로 쉽습니다 외래 키에 직접 액세스할 때 코드에서 엔터티를 사용할 수 있습니다.

데이터 모델에서 어떻게 외래 키의 예제 코드를 단순화할 수를 고려해 보세요 방법을 했지만 이제는 코드에는 *DepartmentsAdd.aspx* 없이도 페이지입니다. 에 `Department` 엔터티에 `Administrator` 속성은 해당 하는 외래 키 `PersonID` 에 `Person` 엔터티. 새 부서와 해당 관리자의 연결을 설정 하기 위해 값을 설정한만 하면는 `Administrator` 속성에는 `ItemInserting` 데이터 바인딩된 컨트롤의 이벤트 처리기.

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

데이터 모델에 외래 키가 없는 처리 하는 것은 `Inserting` 대신 데이터 소스 컨트롤의 이벤트는 `ItemInserting` 엔터티를 엔터티 집합에 추가 하기 전에 엔터티 자체에 대 한 참조를 얻기 위해 데이터 바인딩된 컨트롤의 이벤트입니다. 참조 하는 사용 하는 경우 다음 예제에서와 같은 코드를 사용 하는 연결 설정:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

Entity Framework 팀에서 볼 수 있듯이 [외래 키 연결에 대 한 블로그 게시물](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx), 코드 복잡성의 차이 훨씬 큰 다른 경우가 있습니다. 구현 세부 사항을 보다 간단한 코드 위해 개념적 데이터 모델에서의 라이브 하 길 원하는 요구를 충족 하기 위해 Entity Framework 이제 제공 데이터 모델에 외래 키를 포함 합니다.

Entity Framework 용어에서 데이터 모델에 외래 키를 포함 하는 경우 사용 중인 *외래 키 연결*를 사용 하는 외래 키를 제외 하는 경우 및 *독립 연결만*합니다.

## <a name="executing-user-defined-sql-commands"></a>사용자 정의 SQL 명령 실행

Entity Framework의 이전 버전에서 쉽게 즉석에서 직접 SQL 명령을 생성 하 고 실행할 수 있었습니다. Entity Framework 동적으로 생성 된 SQL 명령 또는 저장된 프로시저를 만들고 함수로 가져올 해야 했습니다. 추가 하는 버전 4 `ExecuteStoreQuery` 및 `ExecuteStoreCommand` 메서드는 `ObjectContext` 쉽게 데이터베이스에 직접 쿼리를 전달 하는 클래스입니다.

Contoso 대학 관리자 데이터베이스에 대량 변경 내용이 저장된 프로시저를 만들고 데이터 모델로 가져오는 과정을 거치지 않고도 할 수 있게 되기를 원하는 가정 합니다. 데이터베이스의 모든 과정에 대 한 크레딧 수를 변경할 수 있는 페이지에 대 한 첫 번째 요청은 합니다. 값과 곱할 사용할 숫자를 입력할 수 있게 하려는 웹 페이지에서 모든 `Course` 행의 `Credits` 열입니다.

사용 하는 새 페이지를 만들고는 *Site.Master* 마스터 페이지 하 고 이름을 *UpdateCredits.aspx*합니다. 다음에 다음 태그를 추가 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

이 태그를 만듭니다는 `TextBox` 사용자 승수 값을 입력할 수 있는 제어는 `Button` 명령을 실행 하기 위해 클릭 하 여 컨트롤 및 `Label` 영향을 받는 행 수를 나타내는 대 한 제어 합니다.

열기 *UpdateCredits.aspx.cs*, 다음 코드를 추가 하 고 `using` 문과 단추에 대 한 처리기 `Click` 이벤트:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

이 코드를 실행 하는 SQL `Update` 명령을 텍스트 상자에 값을 사용 하 고 영향을 받는 행 수를 표시 하려면 해당 레이블을 사용 합니다. 페이지를 실행 하기 전에 실행 된 *Courses.aspx* 확인 하려면 "이전"의 일부 데이터는 페이지입니다.

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

실행 *UpdateCredits.aspx*의 승수로: "10"을 입력 한 다음 클릭 **Execute**합니다.

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

실행 된 *Courses.aspx* 변경 된 데이터를 다시 페이지입니다.

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

(에 원래 값으로 돌아가기 크레딧의 수를 설정 하려는 경우 *UpdateCredits.aspx.cs* 변경 `Credits * {0}` 를 `Credits / {0}` 제도 10을 입력 하 고 페이지를 다시 실행 합니다.)

코드에서 정의 하는 쿼리를 실행 하는 방법에 대 한 자세한 내용은 참조 [하는 방법: 직접 실행 명령에 대 한 데이터 원본](https://msdn.microsoft.com/library/ee358769.aspx)합니다.

## <a name="model-first-development"></a>우선 모델 개발

이러한 연습에서 데이터베이스를 먼저 만든 및 다음 데이터베이스 구조를 기반으로 데이터 모델을 생성 합니다. Entity Framework 4에서 대신 데이터 모델을 통해 시작 하 고 데이터 모델 구조를 기반으로 데이터베이스 생성 키를 누릅니다. 모델 중심 접근 방식을 물리적 구현 세부 정보에 대 한 걱정 하지 하는 동안 응용 프로그램에 대 한 개념적으로 의미가 엔터티 및 관계를 만들 수 있습니다를 데이터베이스가 존재 하지 않는 응용 프로그램을 만드는 경우 . 그러나 (이 마찬가지만 개발의 초기 단계를 통해입니다. 모델에서 다시 만들어 됩니다 실용적인; 및 데이터베이스가 생성 되 고, 프로덕션 데이터 갖습니다 결국 해당 시점 수 데이터베이스 중심 접근 방식에 다시.)

자습서의이 섹션에서는 간단한 데이터 모델을 만들어 하 고 여기에서 데이터베이스를 생성 합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *DAL* 폴더와 선택 **새 항목 추가**합니다. 에 **새 항목 추가** 대화 상자의 **설치 된 템플릿** 선택 **데이터** 선택한 후는 **ADO.NET 엔터티 데이터 모델** 서식 파일 . 새 파일 이름을 *AlumniAssociationModel.edmx* 클릭 **추가**합니다.

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

엔터티 데이터 모델 마법사가 시작 됩니다. 에 **모델 콘텐츠 선택** 단계에서는 **빈 모델** 클릭 하 고 **마침**합니다.

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

**엔터티 데이터 모델 디자이너** 빈 디자인 화면을 엽니다. 끌어서는 **엔터티** 에서 항목의 **도구 상자** 디자인 화면으로 합니다.

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

엔터티 이름을 변경 `Entity1` 를 `Alumnus`, 변경의 `Id` 에 속성 이름을 `AlumnusId`, 라는 새 스칼라 속성을 추가 하 고 `Name`합니다. 새 속성을 추가 하려면 수 한 다음 enter 요소의 이름을 변경 하는 `Id` 열 또는 엔터티를 마우스 오른쪽 단추로 클릭 하 고 선택 **스칼라 속성 추가**합니다. 새 속성에 대 한 기본 형식이 `String`, 되어 있는데이 간단한 데모를 보려면 하지만 물론의 데이터 형식 등으로를 변경할 수 있습니다는 **속성** 창.

다른 엔터티와 같은 방식으로 만들고 이름을 `Donation`합니다. 변경 된 `Id` 속성을 `DonationId` 라는 스칼라 속성을 추가 하 고 `DateAndAmount`합니다.

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

이러한 두 엔터티 간의 연결을 추가 하려면 마우스 오른쪽 단추로 클릭는 `Alumnus` 엔터티를 **추가**를 선택한 후 **연결**합니다.

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

기본 값에 **연결 추가** 대화 상자는 원하는 대로 (1 대 다는 탐색 속성, 외래 키를 포함), 되므로 클릭 **확인**합니다.

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

디자이너는 연결 선 및 외래 키 속성을 추가합니다.

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

이제 데이터베이스를 만들 수 있습니다. 선택 하 고 화면의 디자인을 마우스 오른쪽 단추로 클릭 **모델에서 데이터베이스 생성**합니다.

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

데이터베이스 생성 마법사가 시작 됩니다. (엔터티 매핑되지 않은 나타내는 경고를 나타나면 무시할 수 있습니다 되는 시간에 대 한.)

에 **데이터 연결 선택** 단계, 클릭 **새 연결**합니다.

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

에 **연결 속성** 대화 상자, 로컬 SQL Server Express 인스턴스를 선택 하 고, 데이터베이스의 이름을 `AlumniAsssociation`합니다.

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

클릭 **예** 데이터베이스를 만들 것인지 묻는 하는 경우. 경우는 **데이터 연결 선택** 단계 다시 표시 되 면 클릭 **다음**합니다.

에 **요약 및 설정을** 단계, 클릭 **마침**합니다.

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

A *.sql* 데이터 정의 언어 (DDL) 명령 사용 하 여 파일 만들어지기는 하지만 명령은 아직 실행 하지 않았습니다.

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

와 같은 도구를 사용 하 여 **SQL Server Management Studio** 스크립트를 실행 하 고 수행한 경우 만들 때 처럼, 테이블을 만들는 `School` 에 대 한 데이터베이스 [시작 하는 자습서 시리즈의 첫 번째 자습서 ](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). (있는 경우 제외 하면이 데이터베이스를 다운로드 합니다.)

이제 사용할 수 있습니다는 `AlumniAssociation` 웹에서 데이터 모델 페이지를 사용 했던 동일한 방식으로 `School` 모델입니다. 이를 실행 하려면 테이블에 일부 데이터를 추가 하 고 데이터를 표시 하는 웹 페이지를 만듭니다.

사용 하 여 **서버 탐색기**에 다음 행을 추가할는 `Alumnus` 및 `Donation` 테이블입니다.

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

라는 새 웹 페이지 생성 *Alumni.aspx* 를 사용 하는 *Site.Master* 마스터 페이지입니다. 다음 태그를 추가 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

이 태그는 중첩 된 만듭니다 `GridView` 졸업생 이름을 표시 하려면 한 외부 및 내부 하나에 기부 날짜와 시간 표시를 제어 합니다.

열기 *Alumni.aspx.cs*합니다. 추가 `using` 문이 데이터에 대 한 액세스 계층과 외부에 대 한 처리기 `GridView` 컨트롤의 `RowDataBound` 이벤트:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

이 코드 데이터 바인딩합니다 내부 `GridView` 를 사용 하 여 제어는 `Donations` 탐색 속성의 현재 행의 `Alumnus` 엔터티.

페이지를 실행 합니다.

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

(참고:이 페이지에서 다운로드할 수 있는 프로젝트에 포함 되어 있지만 있습니다 작동 하도록 만들어야 데이터베이스에 로컬 SQL Server Express 인스턴스는 데이터베이스가 아닌로 포함 되어는 *.mdf* 파일에 *앱\_ 데이터* 폴더입니다.)

Entity Framework의 모델 중심 기능을 사용 하는 방법에 대 한 자세한 내용은 참조 [Entity Framework 4의 중심 모델](https://msdn.microsoft.com/data/ff830362.aspx)합니다.

## <a name="poco-support"></a>POCO 지원

도메인 기반 디자인 방법론을 사용 하면 데이터와 비즈니스 도메인에 관련 된 동작을 나타내는 데이터 클래스를 디자인 합니다. 이러한 클래스를 저장 하는 데 사용 하는 특정 기술에 독립적 이어야 합니다. (유지)에서 데이터 즉, 것 *지 속성을 무시*합니다. 지 속성 무시도 쉽게 수행할 수는 클래스 단위 테스트에 단위 테스트 프로젝트를 지 속성 기술은 테스트를 위한 가장 편리 하 게 사용할 수 있으므로 합니다. 엔터티 클래스에서 상속 해야 때문에 지 속성 무시에 대 한 제한 된 지원을 제공 하는 이전 버전의 Entity Framework는 `EntityObject` 클래스 이며 따라서 있는 다양 한 엔터티 프레임 워크 관련 기능을 포함 합니다.

상속 하지는 엔터티 클래스를 사용 하는 기능을 소개 하는 Entity Framework 4는 `EntityObject` 클래스 및 따라서 지 속성 무시 됩니다. Entity Framework의 컨텍스트에서이 같은 클래스는 대개 *old CLR 개체* (POCO, 또는 POCOs). POCO 클래스를 직접 작성할 수 있습니다 또는 Entity Framework에서 제공 하는 Text Template Transformation Toolkit (T4) 템플릿을 사용 하 여 기존 데이터 모델에 따라 자동으로 생성할 수 있습니다.

POCOs Entity Framework에서 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [POCO 엔터티 작업](https://msdn.microsoft.com/library/dd456853.aspx)합니다. 이 파일은 더 자세한 정보를 제공 하는 다른 문서에 대 한 링크가 있는 POCOs에 대 한 개요는는 MSDN 문서입니다.
- [연습: POCO 엔터티 프레임 워크에 대 한 템플릿을](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) POCOs에 대 한 다른 블로그 게시물에 대 한 링크와 Entity Framework 개발팀의 블로그 게시물입니다.

## <a name="code-first-development"></a>코드 중심 개발

Entity Framework 4의 POCO 지원은 여전히 데이터 모델을 만들고 데이터 모델에 엔터티 클래스를 연결에 필요 합니다. Entity Framework의 다음 릴리스에서 라는 새로운 기능이 포함 됩니다 *코드 중심 개발*합니다. 이 기능을 사용 하면 Entity Framework 데이터 모델 디자이너 또는 데이터 모델 XML 파일을 사용 하도록 필요 없이 사용자 고유의 POCO 클래스와 함께 사용할 수 있습니다. (이 옵션 호출 또한에 따라서 *코드 전용*; *코드 중심* 및 *코드 전용* 모두 동일한 Entity Framework 기능을 가리킵니다.)

개발에 코드 중심 접근 방식을 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [Code-first Entity Framework 4 사용 하 여 개발](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)합니다. Scott Guthrie 소개 코드 중심 개발 하 여 블로그 게시물입니다.
- [Entity Framework 개발 팀 블로그-태그가 지정 된 CodeOnly 게시](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [Entity Framework 개발 팀 블로그-태그가 지정 된 코드 첫 번째 게시](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC Music Store 자습서-4 부: 모델 및 데이터 액세스](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [MVC 3-4 부 시작: Entity Framework 코드 중심 개발](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

2011 년 봄에 게시 될 Contoso 대학 응용 프로그램과 유사한 응용 프로그램을 작성 하는 새 MVC Code-first 자습서 추정 되는 또한 [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)

## <a name="more-information"></a>추가 정보

이 개요 항목을 새로운 Entity Framework와 Entity Framework 자습서 시리즈를이 계속이 완료 되었습니다. 여기에 포함 되지 않는 Entity Framework 4의 새로운 기능에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [ADO.NET의 새로운](https://msdn.microsoft.com/library/ex6y04yf.aspx) 의 Entity Framework 버전 4의에서 새로운 기능에 대 한 MSDN 항목.
- [Entity Framework 4의 릴리스 발표](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) 버전 4의에서 새로운 기능에 대 한 Entity Framework 개발 팀의 블로그 게시물입니다.

> [!div class="step-by-step"]
> [이전](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
