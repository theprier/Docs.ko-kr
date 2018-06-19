---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: '2 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여,: 비즈니스 논리 계층 및 단위 테스트 추가 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈 시작 하기에 의해 만들어진 Contoso 대학 웹 응용 프로그램 기반으로 합니다. I 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: ecdfb2bdc546f55778ec4cc1f61aa66e129134ea
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30888317"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>2 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여,: 비즈니스 논리 계층 및 단위 테스트 추가
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> 에 의해 만들어진 Contoso 대학 웹 응용 프로그램을 기반으로 하는이 자습서 시리즈의 [Entity Framework 4.0이 있는 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 점으로 하면 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 완료 하는 자습서 시리즈에서 만들어진 합니다. 이 자습서에 대 한 질문이 있으면에 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


Entity Framework를 사용 하 여 n 계층 웹 응용 프로그램을 만든 이전 자습서에서 및 `ObjectDataSource` 제어 합니다. 이 자습서에서는, 별도 비즈니스 논리 계층 (BLL) 및 데이터 액세스 계층 DAL ()을 유지 하면서 비즈니스 논리를 추가 하는 방법을 설명 하 고 BLL에 대 한 자동화 된 단위 테스트를 만드는 방법을 보여 줍니다.

이 자습서에서는 다음 작업을 수행 합니다.

- 필요한 데이터 액세스 메서드를 선언 하는 리포지토리 인터페이스를 만듭니다.
- 저장소 클래스에 저장소 인터페이스를 구현 합니다.
- 데이터 액세스 기능을 수행 하는 저장소 클래스를 호출 하는 비즈니스 논리 클래스를 만듭니다.
- 연결 된 `ObjectDataSource` 저장소 클래스 대신 비즈니스 논리 클래스에는 컨트롤입니다.
- 단위 테스트 프로젝트와 해당 데이터 저장소에 대 한 메모리 내 컬렉션을 사용 하는 저장소 클래스를 만듭니다.
- 테스트를 실행 하 고 실패를 확인 한 다음 비즈니스 논리 클래스에 추가 하려면 비즈니스 논리에 대 한 단위 테스트를 만듭니다.
- 비즈니스 논리 클래스에서 비즈니스 논리를 구현 합니다. 다음 실행에서 단위 테스트를 통과 참조 하십시오.

사용 하는 *Departments.aspx* 및 *DepartmentsAdd.aspx* 이전 자습서에서 만든 페이지입니다.

## <a name="creating-a-repository-interface"></a>저장소 인터페이스 만들기

리포지토리 인터페이스를 만들어 되기 시작 합니다.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

에 *DAL* 폴더를 새 클래스 파일을 만듭니다, 이름을 *ISchoolRepository.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

인터페이스는 각는 CRUD에 대 한 한 가지 방법은 정의 (만들기, 읽기, 업데이트, 삭제) 저장소 클래스에서 만든 메서드.

에 `SchoolRepository` 클래스 *SchoolRepository.cs*,이 클래스를 구현 함을 나타냅니다는 `ISchoolRepository` 인터페이스:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>비즈니스 논리 클래스 만들기

다음으로, 비즈니스 논리 클래스를 만듭니다. 이렇게 하면에서 실행 되는 비즈니스 논리를 추가할 수 있도록는 `ObjectDataSource` 않지만 하지는 아직 제어 합니다. 새 비즈니스 논리 클래스 지금은 저장소 수행 하는 동일한 CRUD 작업을 수행 합니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

새 폴더를 만들고 이름을 *BLL*합니다. (실제 응용 프로그램에서는 비즈니스 논리 계층 구현 하는 일반적으로 클래스 라이브러리로-별도 프로젝트-하지만이 자습서를 간단히 유지 하기 위해 BLL 클래스 프로젝트 폴더에 보관 됩니다.)

에 *BLL* 폴더를 새 클래스 파일을 만듭니다, 이름을 *SchoolBL.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

이 코드는 저장소 클래스의 앞부분에 언급 했 듯이 동일한 CRUD 방법을 만들지만 Entity Framework 메서드를 직접 액세스 하는 대신 저장소 클래스 메서드 호출 합니다.

저장소 클래스에 대 한 참조를 보유 하는 클래스 변수는 인터페이스 형식으로 정의 하 고 두 명의 생성자에 포함 된 저장소 클래스를 인스턴스화하는 코드. 매개 변수가 없는 생성자에서 사용 될는 `ObjectDataSource` 제어 합니다. 인스턴스를 만듭니다는 `SchoolRepository` 앞에서 만든 클래스입니다. 다른 생성자는 클래스를 인스턴스화하는 비즈니스 논리는 리포지토리 인터페이스를 구현 하는 모든 개체를 전달 하는 코드를 허용 합니다.

저장소 클래스와 두 명의 생성자를 호출 하는 CRUD 메서드는 비즈니스 논리 클래스를 사용 하 여 선택한 모든 백 엔드 데이터 저장소와 수 있도록 설정 합니다. 비즈니스 논리 클래스를 호출 하는 클래스 데이터를 유지 하는 방법을 알아야 할 필요는 없습니다. (이 이라고 하는데 *지 속성 무시*.) 비즈니스 논리 클래스 단순할 무언가 사용 하는 저장소 구현에 연결할 수 있으므로 단위 테스트을 용이 하 게이 메모리 내로 `List` 컬렉션 데이터를 저장 합니다.

> [!NOTE]
> 기술적으로 엔터티 개체는 Entity Framework에서 상속 된 클래스에서 인스턴스화되 때문에 여전히 하지 지 속성 무시를 `EntityObject` 클래스입니다. 전체 지 속성 무시 사용할 *일반 이전 CLR 개체*, 또는 *POCOs*, 개체에서 상속 하는 대신는 `EntityObject` 클래스입니다. POCOs를 사용 하 여이 자습서의 범위를 벗어납니다. 자세한 내용은 참조 [테스트 용이성 및 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) MSDN 웹 사이트입니다.)


연결할 수 이제는 `ObjectDataSource` 비즈니스 논리에 컨트롤 클래스 대신 저장소에 하 고 이전과 같이 작동 하는 것을 확인 합니다.

*Departments.aspx* 및 *DepartmentsAdd.aspx*, 각 변경 `TypeName="ContosoUniversity.DAL.SchoolRepository"` 를 `TypeName="ContosoUniversity.BLL.SchoolBL`"입니다. (모든 페이지에서 다음 네 인스턴스는.)

실행 된 *Departments.aspx* 및 *DepartmentsAdd.aspx* 여전히 작동 하는지 전과 마찬가지로 확인 하는 페이지입니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>단위 테스트 프로젝트 및 저장소 구현 만들기

새 프로젝트를 사용 하 여 솔루션 추가 **테스트 프로젝트** 서식 파일을 하 고 이름을 `ContosoUniversity.Tests`합니다.

테스트 프로젝트에서에 대 한 참조를 추가 `System.Data.Entity` 프로젝트 참조를 추가 하 고는 `ContosoUniversity` 프로젝트.

이제 단위 테스트와 함께 사용 하는 저장소 클래스를 만들 수 있습니다. 클래스 내에서이 저장소에 대 한 데이터 저장소가 됩니다.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

테스트 프로젝트에서 새 클래스 파일을 만들고, 이름을 *MockSchoolRepository.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

이 저장소 클래스에는 Entity Framework에 직접 액세스 하는 것과 동일한 CRUD 메서드가 있지만 작업할 `List` 대신 데이터베이스와 메모리에에서 있는 컬렉션입니다. 이를 설정 하 고 비즈니스 논리 클래스에 대 한 단위 테스트 유효성 검사 테스트 클래스에 대 한 쉽게 있습니다.

## <a name="creating-unit-tests"></a>단위 테스트 만들기

**테스트** 프로젝트 템플릿을 스텁 단위 테스트 클래스를 만들고이 클래스는 비즈니스 논리 클래스에 추가 하려면 비즈니스 논리에 대 한 단위 테스트 메서드를 추가 하 여 수정 하려면 다음 작업은 합니다.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

Contoso 대학의 모든 개별 강사는 단일 부서 관리자만 될 수 있습니다 하 고이 규칙을 적용 하는 비즈니스 논리를 추가 해야 합니다. 테스트를 추가 하 고 실패를 볼 테스트를 실행 하 여 시작 합니다. 다음 코드를 추가 하 고 통과 하도록 예상 하 고 테스트를 실행 합니다.

열기는 *UnitTest1.cs* 파일을 추가 `using` ContosoUniversity 프로젝트에서 만든 비즈니스 논리 및 데이터 액세스 계층에 대 한 문을:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

대체는 `TestMethod1` 메서드는 다음과 같은 방법을:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL` 메서드 단위 테스트는 비즈니스 논리 클래스의 새 인스턴스를 전달 되는 프로젝트에 대해 만든 저장소 클래스의 인스턴스를 만듭니다. 다음 메서드는 테스트 메서드에서 사용할 수 있는 세 가지 부서를 삽입 하는 비즈니스 논리 클래스를 사용 합니다.

테스트 메서드는 비즈니스 논리 클래스를 동일한 관리자는 기존 부서로 사용 하는 새 부서를 삽입 하려고 또는 누군가 부서 관리자는 사용자의 ID로 설정 하 여 업데이트 하려고 하는 경우 예외를 throw 확인 다른 부서 관리자가 이미입니다.

이 코드는 컴파일되지 않습니다 되므로 예외 클래스를 아직 만들지 않았습니다. 컴파일하기를 마우스 오른쪽 단추로 클릭 `DuplicateAdministratorException` 선택 **생성**, 차례로 **클래스**합니다.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

삭제할 수 있는 테스트 프로젝트에서 클래스를 만듭니다이 기본 프로젝트에서 예외 클래스를 만든 후 합니다. 비즈니스 논리를 구현 합니다.

테스트 프로젝트를 실행 합니다. 예상 대로 테스트가 실패 합니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>테스트 통과 하는 비즈니스 논리를 추가 합니다.

다음으로, 사용자는 이미 다른 부서의 관리자가 부서 관리자 권한으로 설정할 수 없는 비즈니스 논리를 구현 합니다. 비즈니스 논리 계층에서 예외를 throw 하는 사용자가 편집 하는 부서를 클릭할 경우 프레젠테이션 계층에서 catch **업데이트** 관리자가 이미 다른 사용자를 선택한 후 합니다. (강사가 이미 관리자 페이지를 렌더링 하기 전에 드롭 다운 목록에서 제거할 수도 수 있지만 여기 목적은 비즈니스 논리 계층을 사용 하는 것).

사용자가 둘 이상의 부서 관리자 강사를 확인 하려고 할 때 throw 됩니다 하는 예외 클래스를 만들어 시작 합니다. 주 프로젝트에 새 클래스 파일을 만듭니다는 *BLL* 폴더 이름을 *DuplicateAdministratorException.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

이제 임시 삭제 *DuplicateAdministratorException.cs* 파일 앞에서 만든 테스트 프로젝트에서 컴파일할 수 있도록 합니다.

주 프로젝트를 열고는 *SchoolBL.cs* 파일 및 유효성 검사 논리를 포함 하는 다음 메서드를 추가 합니다. (코드는 나중에 만드는 메서드를 참조 합니다.)

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

삽입 또는 업데이트 하는 경우에이 메서드를 호출 합니다 `Department` 다른 부서에 이미 동일한 관리자가 있는지 여부를 확인 하기 위해 엔터티.

에 대 한 데이터베이스를 검색 하려면 메서드를 호출 하는 코드는 `Department` 같은 엔터티 `Administrator` 업데이트 되거나 삽입 되는 엔터티로 속성 값입니다. 가 있는 경우 코드 예외를 throw 합니다. 유효성 검사 안 함은 업데이트 되거나 삽입 되는 엔터티가 없는 경우 필요 `Administrator` 업데이트 하는 동안 메서드는 값 및 예외가 throw 됩니다 및 `Department` 엔터티를 일치 하는 항목을 찾을 수는 `Department` 엔터티를 업데이트 합니다.

새 메서드를 호출 하는 `Insert` 및 `Update` 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

*ISchoolRepository.cs*, 새 데이터 액세스 방법에 대 한 다음 선언을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

*SchoolRepository.cs*, 다음 추가 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

*SchoolRepository.cs*, 다음 새 데이터 액세스 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

이 코드에서는 검색 `Department` 지정 된 관리자가 있는 엔터티를 합니다. (있는 경우) 하나만 부서 발견 되어야 합니다. 그러나 데이터베이스에 제약 조건이 없는 빌드되므로 반환 형식은 컬렉션이 여러 부서 발견 되는 경우입니다.

기본적으로 개체 컨텍스트는 데이터베이스에서 엔터티를 검색 하는 경우를 추적 하는 개체 상태 관리자에서 합니다. `MergeOption.NoTracking` 매개 변수 지정이 추적을이 쿼리에 대 한 가능 합니다. 쿼리를 업데이트 하려고 하는 정확한 엔터티를 반환할 수 있습니다 되므로이 작업이 필요 하 고 됩니다 해당 엔터티에 연결할 수 있습니다. 예를 들어, 기록 부서에 편집 하는 경우는 *Departments.aspx* 페이지와 관리자가 변경 하지 않음이 쿼리는 기록 부서를 반환 합니다. 경우 `NoTracking` 개체 컨텍스트에 이미 기록 부서 엔터티에 해당 개체 상태 관리자에서를 설정 하지 않으면 합니다. 개체 컨텍스트에 것 이라는 예외를 throw 뷰 상태에서 다시 만들어지는 기록 department 엔터티를 연결할 경우 다음 `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`합니다.

(지정 하는 대신 `MergeOption.NoTracking`,이 쿼리에 대 한 바로 새 개체 컨텍스트를 만들 수 있습니다. 새 개체 컨텍스트의 개체 상태 관리자는 자체, 하므로 있을 것 충돌 하지 호출 하는 경우는 `Attach` 메서드. 새 개체 컨텍스트에 메타 데이터와 데이터베이스 연결을 공유 원래 개체 컨텍스트에 있으므로이 대체 방법의 성능 저하를 최소화 됩니다. 그러나 여기에 표시 된 접근 방식을 소개는 `NoTracking` 옵션을 다른 컨텍스트에서 유용할 수 있습니다. `NoTracking` 옵션 설명이 시리즈의 자습서의 뒷부분에서 자세히.)

테스트 프로젝트에서 새 데이터 액세스 메서드를 추가 *MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

이 코드 LINQ를 사용 하 여 동일한 데이터 선택을 수행 하는 `ContosoUniversity` 프로젝트 저장소에서 LINQ to Entities에 대 한 합니다.

테스트 프로젝트를 다시 실행 합니다. 이번에는 테스트가 성공합니다.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>ObjectDataSource 예외 처리

에 `ContosoUniversity` 실행 프로젝트는 *Departments.aspx* 페이지와 다른 부서에 대 한 관리자가 이미 다른 사람에 게는 부서에 대 한 관리자를 변경 하려고 합니다. (기억: 데이터베이스가 잘못 된 데이터와 미리 로드 때문에이 자습서에서는 중에 추가 하는 부서를 편집만 할 수 있습니다.) 다음 서버 오류 페이지를 가져오는:

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

오류 처리 코드를 추가 해야 하므로 이러한 유형의 오류 페이지를 보려면 사용자가 받지 않도록 합니다. 열기 *Departments.aspx* 에 대 한 처리기를 지정 하 고는 `OnUpdated` 의 이벤트는 `DepartmentsObjectDataSource`합니다. `ObjectDataSource` 는 다음 예제와 여는 태그 이제 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

*Departments.aspx.cs*, 다음 추가 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

에 대 한 다음 처리기를 추가 `Updated` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

경우는 `ObjectDataSource` 업데이트를 수행 하려고 할 때 제어 된 예외를 catch 예외 이벤트 인수에 전달 합니다 (`e`)이이 처리기에 있습니다. 처리기에서 코드 중복 관리자 예외 예외 인지 확인 합니다. 코드에 대 한 오류 메시지가 포함 된 유효성 검사기 컨트롤을 만듭니다.이 경우는 `ValidationSummary` 컨트롤을 표시 합니다.

페이지를 실행 하 고 사람 지정 관리자 두 부서에 다시 시도 합니다. 이 현재는 `ValidationSummary` 컨트롤 오류 메시지를 표시 합니다.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

비슷한 변경는 *DepartmentsAdd.aspx* 페이지. *DepartmentsAdd.aspx*에 대 한 처리기를 지정 하는 `OnInserted` 의 이벤트는 `DepartmentsObjectDataSource`합니다. 결과 태그는 다음 예제를 비슷합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

*DepartmentsAdd.aspx.cs*를 추가 하 여 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

다음 이벤트 처리기를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

이제 테스트할 수 있습니다는 *DepartmentsAdd.aspx.cs* 페이지도 제대로 두 명 이상의 부서 관리자 되도록 시도 처리 하는 확인 합니다.

사용에 대 한 리포지토리 패턴을 구현 하기 위해 도입이 작업이 완료 되는 `ObjectDataSource` Entity Framework와 제어 합니다. 리포지토리 패턴 및 테스트 가능성에 대 한 자세한 내용은 MSDN 백서를 참조 [테스트 용이성 및 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)합니다.

다음 자습서에서는 정렬 및 필터링 기능을 응용 프로그램을 추가 하는 방법을 볼 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [다음](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
