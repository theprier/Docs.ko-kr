---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: '2 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용: 비즈니스 논리 레이어 및 단위 테스트를 추가 합니다. | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈를 사용 하 여 시작 하 여 만든 Contoso University 웹 응용 프로그램 기반으로 합니다. 필자는 중...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 6517f037a03bb520ee4f3b3185a255b0eaa9de9a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838771"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>2 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용: 비즈니스 논리 레이어 및 단위 테스트 추가
====================
[Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈에서 만든 Contoso University 웹 응용 프로그램 빌드를 [Entity Framework 4.0을 사용 하 여 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈입니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 지점으로 할 수 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 할 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 전체 자습서 시리즈에서 만들어집니다. 이 자습서에 대 한 질문이 있으면 하기를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


이전 자습서에서 Entity Framework를 사용 하 여 n 계층 웹 응용 프로그램을 만든 및 `ObjectDataSource` 제어 합니다. 이 자습서에서는 별도 비즈니스 논리 계층 (BLL) 및 데이터 액세스 계층 DAL ()을 유지 하면서 비즈니스 논리를 추가 하는 방법 및 BLL에 대 한 자동화 된 단위 테스트를 만드는 방법을 보여 줍니다.

이 자습서에서는 다음 작업을 완료 합니다.

- 데이터 액세스 메서드를 선언 하는 리포지토리 인터페이스를 만듭니다.
- 저장소 클래스에서 리포지토리 인터페이스를 구현 합니다.
- 데이터 액세스 기능을 수행 하는 리포지토리 클래스를 호출 하는 비즈니스 논리 클래스를 만듭니다.
- 연결 된 `ObjectDataSource` 리포지토리 클래스 대신 비즈니스 논리 클래스를 제어 합니다.
- 단위 테스트 프로젝트 및 해당 데이터 저장소에 대 한 메모리 내 컬렉션을 사용 하는 리포지토리 클래스를 만듭니다.
- 테스트 실행 실패 하는지 확인 하 고 비즈니스 논리 클래스에 추가 하려는 비즈니스 논리에 대 한 단위 테스트를 만듭니다.
- 비즈니스 논리가 비즈니스 논리 클래스에서 구현 후 다시 실행 하는 단위 테스트를 통과 하는지 확인 합니다.

사용 합니다는 *Departments.aspx* 하 고 *DepartmentsAdd.aspx* 이전 자습서에서 만든 페이지입니다.

## <a name="creating-a-repository-interface"></a>리포지토리 인터페이스 만들기

리포지토리 인터페이스를 만들어 시작할 수 있습니다.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

에 *DAL* 폴더에 새 클래스 파일을 만들고, 이름을 *ISchoolRepository.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

각 CRUD에 대 한 하나의 메서드를 정의 하는 인터페이스 (만들기, 읽기, 업데이트, 삭제) 리포지토리 클래스에서 만든 메서드.

에 `SchoolRepository` 클래스의 *SchoolRepository.cs*,이 클래스를 구현 함을 나타냅니다는 `ISchoolRepository` 인터페이스:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>비즈니스 논리 클래스 만들기

다음으로, 비즈니스 논리 클래스를 만들어야 합니다. 이 작업을 수행 하 여 실행 되는 비즈니스 논리를 추가할 수 있도록는 `ObjectDataSource` 않지만 하지는 아직 제어 합니다. 현재 새 비즈니스 논리 클래스는 저장소 같은 CRUD 작업 수행 합니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

새 폴더를 만들고 이름을 *BLL*합니다. (실제 응용 프로그램에서 비즈니스 논리 계층 구현 하는 일반적으로 클래스 라이브러리로-별도 프로젝트-되지만이 자습서를 간단히 유지 하기 클래스 BLL 프로젝트 폴더에 유지 됩니다.)

에 *BLL* 폴더에 새 클래스 파일을 만들고, 이름을 *SchoolBL.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

이 코드 리포지토리 클래스의 앞부분에서 살펴본 동일한 CRUD 메서드 만들지만 Entity Framework 메서드를 직접 액세스 하는 대신 저장소 클래스 메서드 호출.

리포지토리 클래스에 대 한 참조를 보유 하는 클래스 변수의 인터페이스 형식으로 정의 하 고 리포지토리 클래스를 인스턴스화하는 코드는 두 명의 생성자에 포함 된 키를 누릅니다. 사용할 매개 변수가 없는 생성자를 `ObjectDataSource` 제어 합니다. 인스턴스를 만들고는 `SchoolRepository` 앞에서 만든 클래스입니다. 다른 생성자를 리포지토리 인터페이스를 구현 하는 개체에 전달 하는 비즈니스 논리 클래스를 인스턴스화하는 코드를 허용 합니다.

저장소 클래스 및 두 명의 생성자를 호출 하는 CRUD 메서드 수 있도록 선택 하면 모든 백 엔드 데이터 저장소를 사용 하 여 비즈니스 논리 클래스를 사용 합니다. 비즈니스 논리 클래스를 호출 하는 클래스는 데이터를 유지 하는 방법에 유의 필요가 없습니다. (이 종종 이라고 *지 속성 무시*.) 비즈니스 논리 클래스 무언가 사용 하 여 간단한 저장소 구현에 연결할 수 있으므로 단위 테스트를 용이 하 게이 메모리에서 `List` 컬렉션 데이터를 저장 합니다.

> [!NOTE]
> 기술적으로 엔터티 개체는 Entity Framework에서 상속 된 클래스에서 인스턴스화되는 때문에 여전히 없습니다 지 속성 무시를 `EntityObject` 클래스입니다. 전체 지 속성 무시에 대해 사용할 수 있습니다 *plain old CLR object*, 또는 *Poco*, 개체에서 상속 하는 대신는 `EntityObject` 클래스입니다. Poco를 사용 하 여이 자습서의 범위를 벗어납니다. 자세한 내용은 [테스트 용이성과 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) MSDN 웹 사이트입니다.)


이제 연결할 수는 `ObjectDataSource` 비즈니스 논리 클래스 대신 리포지토리에 컨트롤과 이전과 같이 작동 하는 것을 확인 합니다.

*Departments.aspx* 하 고 *DepartmentsAdd.aspx*, 변경 `TypeName="ContosoUniversity.DAL.SchoolRepository"` 를 `TypeName="ContosoUniversity.BLL.SchoolBL`". (모든 인스턴스 4 개는.)

실행 합니다 *Departments.aspx* 하 고 *DepartmentsAdd.aspx* 작동 하는지 확인 하는 계속 이전과 페이지입니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>단위 테스트 프로젝트 및 리포지토리 구현 만들기

새 프로젝트를 사용 하 여 솔루션에 추가 합니다 **테스트 프로젝트** 템플릿을 하 고 이름을 `ContosoUniversity.Tests`입니다.

테스트 프로젝트에 대 한 참조를 추가 `System.Data.Entity` 에 대 한 프로젝트 참조를 추가 하 고는 `ContosoUniversity` 프로젝트입니다.

이제 단위 테스트를 사용 하 여 사용 하는 리포지토리 클래스를 만들 수 있습니다. 이 리포지토리에 대 한 데이터 저장소 클래스 내의 됩니다.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

테스트 프로젝트에서 새 클래스 파일을 만들고, 이름을 *MockSchoolRepository.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

이 리포지토리 클래스는 Entity Framework를 직접 액세스 하는 것과 같은 CRUD 메서드 하지만 사용 하 여 작동 `List` 대신 데이터베이스를 사용 하 여 메모리의 컬렉션입니다. 그러면 설정 하 고 비즈니스 논리 클래스에 대 한 단위 테스트의 유효성을 검사 하는 테스트 클래스에 대 한 더 쉽습니다.

## <a name="creating-unit-tests"></a>단위 테스트 만들기

합니다 **테스트** 프로젝트 템플릿, 단위 테스트 스텁 클래스를 생성 하 고 다음 작업을 비즈니스 논리 클래스를 추가 하려는 비즈니스 논리에 대 한 단위 테스트 메서드를 추가 하 여이 클래스를 수정 하는 것입니다.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

Contoso University에서 모든 개별 강사 단일 부서 관리자만 될 수 있습니다 하 고이 규칙을 적용할 비즈니스 논리를 추가 해야 합니다. 테스트를 추가 하 고 실패를 보려면 테스트를 실행 하 여 시작 합니다. 다음 코드를 추가 하 고 통과 하도록 보기를 예상 하는 테스트를 다시 실행 합니다.

엽니다는 *UnitTest1.cs* 파일과 추가 `using` ContosoUniversity 프로젝트에서 만든 비즈니스 논리 및 데이터 액세스 계층에 대 한 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

대체는 `TestMethod1` 다음 메서드를 사용 하 여 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL` 메서드는 사용자가 만든 단위 테스트는 비즈니스 논리 클래스의 새 인스턴스를 전달 되는 프로젝트에 대 한 리포지토리 클래스의 인스턴스를 만듭니다. 다음 메서드는 테스트 메서드에서 사용할 수 있는 세 가지 부서를 삽입 하는 비즈니스 논리 클래스를 사용 합니다.

테스트 메서드는 비즈니스 논리 클래스는 기존 부서와 같은 관리자를 사용 하 여 새 학과 삽입 하려고 하는 사용자가 아니면 누군가 부서 관리자의 사용자 ID로 설정 하 여 업데이트 하려고 하는 경우 예외를 throw 확인 이미 있는 다른 학부의 관리자입니다.

이 코드는 컴파일되지 않습니다 있도록 예외 클래스를 아직 만들지 않았습니다. 컴파일할 수 것을 마우스 오른쪽 단추로 클릭 `DuplicateAdministratorException` 선택한 **생성**를 차례로 **클래스**합니다.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

삭제할 수 있는 테스트 프로젝트에서 클래스를 만들고이 기본 프로젝트의 예외 클래스를 만든 후 합니다. 비즈니스 논리를 구현 합니다.

테스트 프로젝트를 실행 합니다. 예상 대로 테스트가 실패 합니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>테스트 통과 하는 비즈니스 논리를 추가 합니다.

다음으로, 다른 학부의 관리자가 이미 있는 다른 사람의 도움의 부서 관리자로 설정할 수 없도록 하는 비즈니스 논리를 구현할 수 있습니다. 비즈니스 논리 계층에서 예외를 throw 하 고 사용자는 부서를 편집 하 고 클릭 하는 경우 프레젠테이션 계층에서 catch **업데이트** 후 관리자가 이미 있는 사람을 선택 합니다. (강사 페이지를 렌더링 하기 전에 관리자가 포함 되어 있는 드롭다운 목록에서 제거할 수도 있습니다 하지만 여기서 비즈니스 논리 계층을 사용 하는 것입니다.)

사용자가 강사 둘 이상의 부서의 관리자를 확인 하려고 할 때 throw 됩니다 하는 예외 클래스를 만들어 시작 합니다. 주 프로젝트에 새 클래스 파일을 만듭니다는 *BLL* 폴더 이름을 *DuplicateAdministratorException.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

이제 임시 삭제할 *DuplicateAdministratorException.cs* 앞에서 만든 테스트 프로젝트에서 컴파일할 수 있도록 하는 파일입니다.

주 프로젝트에서 엽니다는 *SchoolBL.cs* 파일 및 유효성 검사 논리를 포함 하는 다음 메서드를 추가 합니다. (코드를 나중에 만드는 메서드를 참조 합니다.)

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

삽입 하거나 업데이트 하는 경우이 메서드를 호출 하겠습니다 `Department` 다른 부서에 이미 동일한 관리자가 있는지 여부를 확인 하기 위해 엔터티.

데이터베이스를 검색할 메서드를 호출 하는 코드를 `Department` 동일한 엔터티 `Administrator` 엔터티로 속성 값이 삽입 되거나 업데이트 될 합니다. 가 검색 되 면 코드는 예외가 발생 합니다. 없습니다 유효성 검사가 필요한 경우 엔터티가 삽입 되거나 업데이트 되지 `Administrator` 업데이트 하는 동안 메서드는 값 및 예외가 throw 됩니다 및 `Department` 엔터티를 일치 항목을 찾을 수는 `Department` 엔터티를 업데이트 합니다.

새 메서드를 호출 합니다 `Insert` 고 `Update` 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

*ISchoolRepository.cs*, 새 데이터 액세스 메서드에 대 한 다음 선언을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

*SchoolRepository.cs*, 다음 추가 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

*SchoolRepository.cs*, 다음 새 데이터 액세스 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

이 코드 검색 `Department` 지정 된 관리자가 있는 엔터티. (해당 되는 경우)만 하나의 부서 발견 되어야 합니다. 그러나 데이터베이스에 제약 조건이 없는 빌드되므로 반환 형식이 컬렉션이 여러 개 발견 되는 경우입니다.

기본적으로 개체 컨텍스트는 데이터베이스에서 엔터티를 검색 하는 경우를 추적 하는 개체 상태 관리자에 있습니다. `MergeOption.NoTracking` 매개 변수 지정이 추적을이 쿼리에 대해 가능 합니다. 왜냐하면 필요한 쿼리를 업데이트 하려면 하려는 정확한 엔터티를 반환할 수 있습니다 및 다음 해당 엔터티를 연결 하지 못할 것 있습니다. 예를 들어 기록 부서를 편집 합니다 *Departments.aspx* 페이지 및 관리자가 변경 되지 않은 상태로 두고가이 쿼리는 기록 부서를 반환 합니다. 경우 `NoTracking` 개체 컨텍스트에서 해당 개체 상태 관리자에 기록 부서 엔터티를 이미 것을 설정 하지 않으면. 개체 컨텍스트에 않는다는 예외가 throw 뷰 상태를 다시 만든 기록 부서 엔터티를 연결 하는 경우 다음 `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`합니다.

(지정 하는 대 안으로 `MergeOption.NoTracking`에이 쿼리에 대해 새 개체 컨텍스트를 만들 수 있습니다. 새 개체 컨텍스트 자체 개체 상태 관리자는 있으므로 있을 충돌이 발생 하지 호출 하는 경우는 `Attach` 메서드. 새 개체 컨텍스트에 있으므로이 대체 방법의 성능 저하를 최소화 됩니다 원래 개체 컨텍스트를 사용 하 여 메타 데이터 및 데이터베이스 연결을 공유 됩니다. 그러나 여기에 표시 된 접근 방식은 소개를 `NoTracking` 다른 컨텍스트에서 유용한 옵션입니다. `NoTracking` 옵션 부분은이 시리즈의 자습서의 뒷부분에서 자세히.)

테스트 프로젝트에서 새 데이터 액세스 메서드를 추가 합니다 *MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

이 코드에서 LINQ를 사용 하 여 동일한 데이터 선택을 수행 하는 `ContosoUniversity` 프로젝트 리포지토리는 LINQ to Entities 사용 합니다.

테스트 프로젝트를 다시 실행 합니다. 이번에는 테스트가 성공합니다.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>ObjectDataSource 예외 처리

에 `ContosoUniversity` 프로젝트를 실행 합니다 *Departments.aspx* 페이지와 다른 부서에 대 한 관리자가 이미 다른 사람에 게는 부서에 대 한 관리자를 변경 하려고 합니다. (잘못 된 데이터를 사용 하 여 미리 로드 된 데이터베이스 제공 하므로이 자습서에서 추가한 부서만 편집할 수 해야 합니다.) 서버 오류 페이지 표시.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

사용자에 게 오류 처리 코드를 추가 해야 하므로 이러한 종류의 오류 페이지를 표시 하지 않으려면입니다. 열기 *Departments.aspx* 에 대 한 처리기를 지정 합니다 `OnUpdated` 의 이벤트는 `DepartmentsObjectDataSource`합니다. `ObjectDataSource` 다음 예제와 유사한 이제 여는 태그입니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

*Departments.aspx.cs*, 다음 추가 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

에 대 한 다음 처리기를 추가 합니다 `Updated` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

경우는 `ObjectDataSource` 컨트롤 업데이트를 수행 하려고 할 때 예외를 catch 하는 예외 이벤트 인수에 전달 합니다 (`e`)이이 처리기에 있습니다. 처리기의 코드가 예외 중복 관리자 예외 인지를 확인 합니다. 코드에 대 한 오류 메시지를 포함 하는 유효성 검사기 컨트롤을 만들어 인 경우는 `ValidationSummary` 컨트롤을 표시 합니다.

페이지를 실행 하 고 사용자가 두 부서 관리자가 작업을 다시 수행 하려고 합니다. 이 이번에는 `ValidationSummary` 컨트롤 오류 메시지를 표시 합니다.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

유사한 변경 하는 *DepartmentsAdd.aspx* 페이지입니다. *DepartmentsAdd.aspx*에 대 한 처리기를 지정 합니다 `OnInserted` 의 이벤트는 `DepartmentsObjectDataSource`합니다. 결과 태그에는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

*DepartmentsAdd.aspx.cs*를 추가 하 여 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

다음 이벤트 처리기를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

이제 테스트할 수 있습니다는 *DepartmentsAdd.aspx.cs* 페이지 명 둘 이상의 부서의 관리자를 확인 하려고도 올바르게 처리 하는 확인 합니다.

사용 하 여 리포지토리 패턴을 구현 하는 데 대 한 소개를 완료 합니다 `ObjectDataSource` Entity Framework를 사용 하 여 제어 합니다. 리포지토리 패턴 및 테스트 용이성에 대 한 자세한 내용은 MSDN 백서를 참조 [테스트 용이성과 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)합니다.

다음 자습서를 정렬 및 필터링 기능을 응용 프로그램을 추가 하는 방법을 배웁니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [다음](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
