---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: Entity Framework 4.0의에서 새로운 기능 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈를 사용 하 여 시작 하 여 만든 Contoso University 웹 응용 프로그램 기반으로 합니다. 필자는 중...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 402e7ace1abad899d32ed179d6b68de4e5a129f5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829835"
---
<a name="whats-new-in-the-entity-framework-40"></a>Entity Framework 4.0의에서 새로운 기능
====================
[Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈에서 만든 Contoso University 웹 응용 프로그램 빌드를 [Entity Framework를 사용 하 여 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈입니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 지점으로 할 수 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 할 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 전체 자습서 시리즈에서 만들어집니다. 이 자습서에 대 한 질문이 있으면 하기를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


이전 자습서에서 Entity Framework를 사용 하는 웹 응용 프로그램의 성능을 극대화 하기 위한 몇 가지 방법을 살펴보았습니다. 이 자습서는 Entity Framework 버전 4의에서 가장 중요 한 새로운 기능 중 일부를 검토 하 고 모든 새 기능에 대 한 자세한 소개를 제공 하는 리소스에 연결 합니다. 이 자습서에서 강조 표시 된 기능은 다음과 같습니다.

- 외래 키 연결 합니다.
- 사용자 정의 SQL 명령을 실행 합니다.
- 모델 우선 개발 합니다.
- POCO 지원 합니다.

또한 자습서에서는 간단 하 게 소개 *코드 중심 개발*, Entity Framework의 다음 릴리스에서 제공 되는 기능입니다.

이 자습서를 시작 하려면 Visual Studio를 시작 하 고 이전 자습서에서 사용 하 여 작업 하는 Contoso University 웹 응용 프로그램을 엽니다.

## <a name="foreign-key-associations"></a>외래 키 연결

Entity Framework 버전 3.5에는 탐색 속성을 포함 하지만 데이터 모델에서 외래 키 속성을 포함 하지 않습니다. 예를 들어를 `CourseID` 및 `StudentID` 열의 합니다 `StudentGrade` 테이블에서 생략할 수는 `StudentGrade` 엔터티.

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

이 방법에 대 한 이유를 엄격히 말해, 외래 키를 물리적 구현 세부 정보를 개념적 데이터 모델에 속하지 않는 경우 그러나 실제 문제로 경우가 외래 키에 직접 액세스할 수 있는 경우 코드에서 엔터티를 사용 하기 쉬운 합니다.

데이터 모델에서 어떻게 외래 키의 예제 코드를 간소화할 수에 대 한 고려 하는 방법을 했지만 이제는 코드에는 *DepartmentsAdd.aspx* 않고도 페이지입니다. 에 `Department` 엔터티는 `Administrator` 속성은 해당 하는 외래 키 `PersonID` 에서 `Person` 엔터티. 새 학과와 해당 관리자의 연결을 설정 하기 위해 값을 설정 했습니다 수행 했던 모든 합니다 `Administrator` 속성에는 `ItemInserting` 데이터 바인딩된 컨트롤의 이벤트 처리기:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

데이터 모델에서 외래 키가 없이 처리 하는 것을 `Inserting` 대신 데이터 소스 컨트롤의 이벤트는 `ItemInserting` 엔터티는 엔터티 집합에 추가 되기 전에 엔터티 자체에 대 한 참조를 가져오기 위해 데이터 바인딩된 컨트롤의 이벤트입니다. 참조 하는 경우 다음 예와에서 같은 코드를 사용 하는 연결을 설정 합니다.

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

Entity Framework 팀에서 알 수 있듯이 [외래 키 연결에서 블로그 게시물](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx), 코드 복잡성의 차이 훨씬 더 큰 있는 다른 경우도 있습니다. 코드가 더 간단 하기 위해 개념적 데이터 모델의 구현 세부 정보를 사용 하 여 라이브 하려는 사용자의 요구를 달성 하기 위해 Entity Framework 이제는 옵션이 있습니다 데이터 모델에 외래 키를 포함 합니다.

Entity Framework 용어에서 데이터 모델에서 외래 키를 포함 하는 경우 사용 중인 *외래 키 연결*를 사용 하는 외래 키를 제외 하 고 *독립 연결*합니다.

## <a name="executing-user-defined-sql-commands"></a>사용자 정의 SQL 명령 실행

Entity Framework의 이전 버전에서는 쉽게 직접 SQL 명령을 즉석에서 만들고 실행할 수 있었습니다. Entity Framework 동적으로 생성 된 SQL 명령 또는 저장된 프로시저를 만들고 함수로 가져와서 해야 했습니다. 버전 4 추가 `ExecuteStoreQuery` 하 고 `ExecuteStoreCommand` 메서드를 `ObjectContext` 쉽게 데이터베이스를 직접 쿼리를 전달할 수 있는 클래스입니다.

Contoso University 관리자가 저장된 프로시저를 만들고 데이터 모델로 가져오는 과정을 거칠 필요 없이 데이터베이스에 대량 변경 내용이 수행할 수 있으려면 가정 합니다. 첫 번째 요청은 데이터베이스의 모든 강좌에 대 한 학점 수를 변경 하도록 하는 페이지입니다. 웹 페이지에서 사용할 값을 곱할 숫자를 입력할 수 하려는 모든 `Course` 행의 `Credits` 열입니다.

사용 하는 새 페이지를 만들 합니다 *Site.Master* 마스터 페이지 및 이름을 *UpdateCredits.aspx*합니다. 다음 태그를 추가 합니다 `Content` 제어 라는 `Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

이 태그를 만듭니다는 `TextBox` 사용자 승수 값을 입력할 수 있는 컨트롤을 `Button` 명령을 실행 하기 위해 클릭 하는 컨트롤 및 `Label` 영향을 받는 행 수를 나타내는 컨트롤입니다.

오픈 *UpdateCredits.aspx.cs*, 다음을 추가 합니다 `using` 문과 단추에 대 한 처리기 `Click` 이벤트:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

이 코드는 SQL 실행 `Update` 텍스트 상자에 값을 사용 하 여 명령 및 영향을 받는 행 수를 표시 하는 레이블을 사용 합니다. 페이지를 실행 하기 전에 실행 된 *Courses.aspx* 일부 데이터는 "before" 그림을 가져오려면 페이지를 합니다.

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

실행할 *UpdateCredits.aspx*의 승수로 "10"을 입력 하 고 클릭 **Execute**합니다.

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

실행 합니다 *Courses.aspx* 페이지 변경된 된 데이터를 다시 합니다.

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

(원래 값으로 다시의 학점 수를 설정 하려는 경우 *UpdateCredits.aspx.cs* 변경 `Credits * {0}` 에 `Credits / {0}` 제수로 10 입력 페이지를 다시 실행 합니다.)

코드에서 정의 하는 쿼리를 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 직접 실행 명령에 대 한 데이터 원본](https://msdn.microsoft.com/library/ee358769.aspx)합니다.

## <a name="model-first-development"></a>모델 우선 개발

이러한 연습에서 먼저 데이터베이스를 생성 하 고 그런 다음 데이터베이스 구조를 기반으로 데이터 모델을 생성 합니다. Entity Framework 4에서 대신 데이터 모델을 사용 하 여 시작할 수 있으며 데이터베이스를 데이터 모델 구조를 기반으로 생성 키를 누릅니다. 모델-첫 번째 방법은 실제 구현 세부 정보에 대 한 걱정 하지 하는 동안 응용 프로그램에 대 한 개념적 이해는 엔터티 및 관계를 만들 수 있습니다는 데이터베이스 존재 하지 않는 응용 프로그램을 만드는 경우 . 그러나 (이 마찬가지 개발의 초기 단계를 통해만입니다. 결국 데이터베이스 만들어질 수, 프로덕션 데이터를 해야 하 고 모델에서 다시 실용적인; 더 이상 이때 수 데이터베이스 중심으로 합니다.)

자습서의이 섹션에서는 간단한 데이터 모델을 만들고 여기에서 데이터베이스를 생성 합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *DAL* 폴더를 선택 **새 항목 추가**합니다. 에 **새 항목 추가** 대화 상자의 **설치 된 템플릿** 선택 **데이터** 를 선택한 합니다 **ADO.NET 엔터티 데이터 모델** 템플릿 . 새 파일의 이름을 *AlumniAssociationModel.edmx* 누릅니다 **추가**합니다.

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

엔터티 데이터 모델 마법사가 시작 됩니다. 에 **Model 콘텐츠 선택** 선택 단계 **빈 모델** 클릭 하 고 **마침**합니다.

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

합니다 **엔터티 데이터 모델 디자이너** 빈 디자인 화면을 사용 하 여 엽니다. 끌어서를 **엔터티** 에서 항목을 **도구 상자** 디자인 화면으로 합니다.

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

엔터티 이름을 변경 `Entity1` 에 `Alumnus`를 변경 합니다 `Id` 속성 이름입니다 `AlumnusId`, 라는 새 스칼라 속성을 추가 하 고 `Name`입니다. 새 속성을 추가할 수 있습니다 끝에서 Enter 키의 이름을 변경 합니다 `Id` 열 또는 엔터티를 마우스 오른쪽 단추로 클릭 하 고 선택 **스칼라 속성 추가**합니다. 새 속성에 대 한 기본 형식은 `String`것이 간단한 데모를 보려면 되지만 데이터 형식 등을 변경할 수는 물론 합니다 **속성** 창입니다.

다른 엔터티와 같은 방식으로 만들고 이름을 `Donation`입니다. 변경 된 `Id` 속성을 `DonationId` 라는 스칼라 속성을 추가 하 고 `DateAndAmount`입니다.

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

이러한 두 엔터티 간의 연결을 추가 하려면 마우스 오른쪽 단추로 클릭 합니다 `Alumnus` 엔터티를 선택 **추가**를 선택한 후 **연결**합니다.

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

기본 값을 **연결 추가** 대화 상자는 원하는 (다를 탐색 속성을 포함, 외래 키 포함) 하므로 클릭 **확인**합니다.

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

디자이너에는 연결 선 및 외래 키 속성을 추가합니다.

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

이제 데이터베이스를 만들 준비가 되었습니다. 디자인 화면을 마우스 오른쪽 단추로 클릭 **모델에서 데이터베이스 생성**합니다.

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

데이터베이스 생성 마법사가 시작 됩니다. (엔터티 매핑되지 않은 경고가 나타나면 무시할 수 있습니다 당분간 이러한.)

에 **데이터 연결 선택** 단계를 클릭 **새 연결**합니다.

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

에 **연결 속성** 대화 상자, 로컬 SQL Server Express 인스턴스를 선택 하 고, 데이터베이스 이름을 `AlumniAsssociation`입니다.

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

클릭 **예** 데이터베이스를 만들 것인지 묻는 하는 경우. 경우는 **데이터 연결 선택** 단계를 다시 표시 됩니다, 클릭 **다음**합니다.

에 **요약 및 설정** 단계를 클릭 **마침**합니다.

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

A *.sql* 명령을 아직 실행 하지 않은 하지만 데이터 정의 언어 (DDL) 명령 사용 하 여 파일이 만들어집니다.

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

와 같은 도구를 사용 **SQL Server Management Studio** 스크립트를 실행 하 고 있습니다 수행한 경우 만들 때 테이블을 만들 합니다 `School` 에 대 한 데이터베이스 [시작 자습서 시리즈의 첫 번째 자습서 ](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). (하지 않는 한 데이터베이스 다운로드 한.)

이제 사용할 수 있습니다 합니다 `AlumniAssociation` 웹에서 데이터 모델에 사용 했던 동일한 방식으로 페이지는 `School` 모델입니다. 이 사용 하려면 테이블에 일부 데이터를 추가 하 고 데이터를 표시 하는 웹 페이지를 만듭니다.

사용 하 여 **서버 탐색기**, 다음 행을 추가 합니다 `Alumnus` 및 `Donation` 테이블입니다.

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

라는 새 웹 페이지를 만듭니다 *Alumni.aspx* 를 사용 하는 *Site.Master* 마스터 페이지입니다. 다음 태그를 추가 합니다 `Content` 제어 라는 `Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

이 태그는 중첩 된 만듭니다 `GridView` 동문 이름을 표시 하려면 외부 하나 및 내부 하나 기부 날짜 및 시간 표시를 제어 합니다.

오픈 *Alumni.aspx.cs*합니다. 추가 된 `using` 문의 데이터에 대 한 액세스 계층과 외부 처리기 `GridView` 컨트롤의 `RowDataBound` 이벤트:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

이 코드 계열을 내부 `GridView` 사용 하 여 제어 합니다 `Donations` 탐색 속성의 현재 행의 `Alumnus` 엔터티.

페이지를 실행 합니다.

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

(참고:이 페이지는 다운로드 가능한 프로젝트에 포함 되어 있지만 작동 하도록 만들어야 데이터베이스 로컬 SQL Server Express 인스턴스에 데이터베이스와 포함 되지 않습니다는 *.mdf* 파일을 *앱\_ 데이터* 폴더입니다.)

Entity Framework의 모델 중심 기능을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Entity Framework 4에서 Model-first](https://msdn.microsoft.com/data/ff830362.aspx)합니다.

## <a name="poco-support"></a>POCO 지원

도메인 기반 디자인 방법론을 사용 하면 데이터 및 비즈니스 도메인에 관련 된 동작을 나타내는 데이터 클래스 디자인 합니다. 이러한 클래스는 저장 하는 데 사용 된 특정 기술의 영향을 받지 않아야 합니다. (유지) 데이터를 즉, 되어야 *지 속성 무시*합니다. 지 속성 무시도 가능 클래스 단위 테스트를 쉽게 지 속성 기술 테스트 하는 데 가장 유용 단위 테스트 프로젝트를 사용할 수 있으므로 합니다. 엔터티 클래스에서 상속 해야 하기 때문에 지 속성 무시에 대 한 제한 된 지원을 제공 하는 이전 버전의 Entity Framework는 `EntityObject` 클래스 및 따라서 많은 Entity Framework 전용 기능을 포함 합니다.

Entity Framework 4에서 상속 하지 않은 엔터티 클래스를 사용 하는 기능을 소개 합니다 `EntityObject` 클래스 이며 따라서 지 속성 무시 합니다. Entity Framework의 컨텍스트에서이 같은 클래스는 대개 *plain old CLR object* (POCO 또는 Poco). POCO 클래스를 수동으로 작성할 수 있습니다 또는 Entity Framework에서 제공 하는 Template Transformation Toolkit (T4) 템플릿을 사용 하 여 기존 데이터 모델에 따라 자동으로 생성할 수 있습니다.

Entity Framework에서 Poco를 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [POCO 엔터티 작업](https://msdn.microsoft.com/library/dd456853.aspx)합니다. 이 더 자세한 정보를 제공 하는 다른 문서에 대 한 링크를 사용 하 여 Poco 개요는 MSDN 문서.
- [연습: POCO 엔터티 프레임 워크에 대 한 템플릿을](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) Poco에 대 한 다른 블로그 게시물에 대 한 링크를 사용 하 여 Entity Framework 개발 팀의 블로그 게시물입니다.

## <a name="code-first-development"></a>코드 중심 개발

Entity Framework 4에서 POCO 지원을 여전히 데이터 모델을 만들고 데이터 모델에 엔터티 클래스를 연결에 필요 합니다. Entity Framework의 다음 릴리스에서 라는 기능이 포함 됩니다 *코드 중심 개발*합니다. 이 기능을 사용 하면 Entity Framework 데이터 모델 디자이너 또는 데이터 모델 XML 파일을 사용 하도록 하지 않고도 사용자 자신의 POCO 클래스를 사용 하 여 사용할 수 있습니다. (따라서이 옵션 또한 호출한 *코드만*; *코드 중심* 하 고 *코드만* 모두 동일한 Entity Framework 기능을 가리킵니다.)

개발 코드 중심 접근 방식을 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [코드 중심 Entity Framework 4 사용 하 여 개발](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)합니다. 이 Scott Guthrie 소개 하는 코드 중심 개발 하 여 블로그 게시물.
- [Entity Framework 개발 팀 블로그-태그가 지정 된 CodeOnly 게시](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [Entity Framework 개발 팀 블로그-태그가 지정 된 코드 첫 번째 게시](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC Music Store 자습서-4 부: 모델 및 데이터 액세스](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [Getting Started with MVC 3-4 부: Entity Framework 코드 중심 개발](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

Contoso University 응용 프로그램과 유사한 응용 프로그램을 작성 하는 새 MVC 코드-첫 번째 자습서에서 2011 년 봄에 게시할 프로젝션 되는 또한 [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)

## <a name="more-information"></a>추가 정보

이 개요의 Entity Framework 및 Entity Framework 자습서 시리즈를이 계속이 새로운를 완료 합니다. 여기에 포함 되지 않는 Entity Framework 4의 새로운 기능에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ADO.NET의 새로운](https://msdn.microsoft.com/library/ex6y04yf.aspx) Entity Framework 버전 4의에서 새로운 기능에 대 한 MSDN 항목.
- [Entity Framework 4의 릴리스를 발표](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) 버전 4의에서 새로운 기능에 대 한 Entity Framework 개발 팀의 블로그 게시물.

> [!div class="step-by-step"]
> [이전](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
