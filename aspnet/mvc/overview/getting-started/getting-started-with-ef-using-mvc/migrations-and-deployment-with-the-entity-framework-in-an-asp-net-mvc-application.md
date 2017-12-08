---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: "Code First 마이그레이션 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 배포 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 2294f2aba3f765d7849d1f407e85f424dc8b2518
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="code-first-migrations-and-deployment-with-the-entity-framework-in-an-aspnet-mvc-application"></a>Code First 마이그레이션 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 배포
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.

지금까지 응용 프로그램에 되었습니다에서 로컬로 실행 중 IIS Express에서 개발 컴퓨터. 실제 응용 프로그램을 인터넷을 통해 사용 하 여 다른 사람들이 사용할 수 있도록 하려면 웹 호스팅 공급자를 배포 해야 합니다. 이 자습서에서는 Azure에서 클라우드로 Contoso 대학교 응용 프로그램을 배포 합니다.

이 자습서에는 다음 섹션이 포함 됩니다.

- Code First 마이그레이션을 사용 하도록 설정 합니다. 마이그레이션 기능을 사용 하면 데이터 모델을 변경 하 고 삭제 하 고 데이터베이스를 다시 만들 필요 없이 데이터베이스 스키마를 업데이트 하 여 프로덕션 환경에 변경 내용을 배포할 수 있습니다.
- Azure에 배포 합니다. 이 단계는 선택 사항입니다. 나머지 자습서 프로젝트를 배포 하지 않고 계속할 수 있습니다.

배포에 대 한 소스 제어를 사용한 연속 통합 프로세스를 사용 하지만이 자습서 항목에 대 한를 다루지 않습니다 것이 좋습니다. 자세한 내용은 참조는 [소스 제어](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) 및 [연속 통합](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) 의 장에 [Azure로 실제 클라우드 응용 프로그램 빌딩](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction) 전자책 (영문) 합니다.

## <a name="enable-code-first-migrations"></a>Code First 마이그레이션을 사용 하도록 설정

새 응용 프로그램을 개발 하는 경우 데이터 모델에 자주 및 변경 될 때마다 모델 변경, 데이터베이스와 동기화를 가져옵니다. 자동으로 삭제 하 고 데이터 모델을 변경할 때마다 데이터베이스를 다시 만드는 Entity Framework를 구성 했습니다. 추가, 제거 또는 엔터티 클래스를 변경 하거나 변경할 경우 프로그램 `DbContext` 클래스 다음에 응용 프로그램을 실행 하 고 자동으로 기존 데이터베이스를 삭제, 모델을 일치 시키고 테스트 데이터로 초기값을 설정 하는 새 브러시를 만듭니다.

이 방법은 데이터베이스를 데이터 모델을 통해 동기화 유지 프로덕션 환경에 응용 프로그램을 배포할 때까지 잘 작동 합니다. 응용 프로그램이 프로덕션 환경에서 실행 중인 경우 것에서 일반적으로 데이터를 저장, 보관 하 고 새 열을 추가 하는 등 변경할 때마다 모든 내용을 손실 하지 않으려면입니다. [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 삭제 하 고 데이터베이스를 다시 작성 하는 대신 데이터베이스 스키마를 업데이트 하려면 Code First를 사용 하 여이 문제를 해결 하는 기능입니다. 이 자습서에서는 응용 프로그램을 배포 합니다 및 해당 준비 마이그레이션을 설정 합니다.

1. 이전 주석으로 처리 하거나 삭제 하 여 설정한 이니셜라이저를 사용 하지 않도록 설정 된 `contexts` 응용 프로그램 Web.config 파일에 추가 하는 요소입니다.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. 응용 프로그램에도 *Web.config* 파일, 연결 문자열에 데이터베이스의 이름을 ContosoUniversity2로 변경 합니다.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    이러한 변경 하 여 첫 번째 마이그레이션 새 데이터베이스를 만드는 프로젝트를 설정 합니다. 에서는 필요 하지 않습니다 되지만 것이 좋습니다 나중에 표시 됩니다.
3. **도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

    ![Selecting_Package_Manager_Console](https://asp.net/media/4336350/1pm.png)
4. 에 `PM>` 프롬프트에 다음 명령을 입력 합니다.

    `enable-migrations`  
    `add-migration InitialCreate`

    ![enable-migrations 명령](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

    `enable-migrations` 명령은 만듭니다는 *마이그레이션* 폴더 ContosoUniversity 프로젝트에 해당 폴더에 배치는 *Configuration.cs* 마이그레이션을 구성 하는 편집할 수 있는 파일입니다.

    (마이그레이션 기존 데이터베이스를 찾이 되며 자동으로 수행 하는 경우 데이터베이스 이름을 변경할 수를 알려 주는 위의 단계를 벗어나는 `add-migration` 명령입니다. 하지만 괜찮습니다, 그리고 할 데이터베이스를 배포 하기 전에 마이그레이션 코드의 테스트를 실행 되지 않습니다. 실행할 때 나중는 `update-database` 명령 데이터베이스가 이미 존재 하기 때문에 아무 작업도 수행 합니다.)

    ![Migrations 폴더](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    이전에 본 이니셜라이저 클래스와 마찬가지로 `Configuration` 클래스를 포함 한 `Seed` 메서드.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    용도 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 방법은 삽입 또는 Code First를 만들거나 데이터베이스를 업데이트 한 후 테스트 데이터를 업데이트할 수 있도록 하는 것입니다. 메서드는 데이터베이스를 만들 때 및 데이터 모델 변경 후 데이터베이스 스키마가 업데이트 될 때마다 호출 됩니다.

### <a name="set-up-the-seed-method"></a>Seed 메서드 설정

삭제 하 고 이니셜라이저 클래스 사용에 대 한 모든 데이터 모델을 변경 하는 데이터베이스를 다시 만드는 시점과 `Seed` 메서드를 변경할 때마다 모델 데이터베이스를 삭제 하기 때문에 테스트 데이터를 삽입 하 고 모든 테스트 데이터 손실 됩니다. Code First 마이그레이션을, 데이터베이스 변경 된 후 데이터는 유지 하는 테스트의 테스트 데이터를 포함 하므로 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 일반적으로 메서드는 필요 없습니다. 않도록 실제로 `Seed` 합니다 사용할 경우 마이그레이션에 데이터베이스를 프로덕션에 배포 하기 때문에 테스트 데이터를 삽입 하는 메서드는 `Seed` 메서드가 프로덕션 환경에서 실행 됩니다. 원하는 경우에 `Seed` 메서드를 프로덕션 환경에서 필요한 데이터만 데이터베이스에 삽입 합니다. 데이터베이스의 실제 부서 이름을 포함 하도록 할 수는 예를 들어는 `Department` 응용 프로그램이 프로덕션 환경에서 사용할 수 있을 때 테이블입니다.

이 자습서를 사용 하기 마이그레이션 배포에 대 한 하지만 `Seed` 메서드는 테스트 데이터 삽입 그래도 보다 쉽게 응용 프로그램 기능을 수동으로 많은 데이터를 삽입 하지 않고도 어떻게 작동 하는지 확인할 수 있도록 합니다.

1. 내용을 대체는 *Configuration.cs* 가 새 데이터베이스에 테스트 데이터를 로드 하는 다음 코드로 파일입니다. 

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드가 데이터베이스 컨텍스트 개체를 입력된 매개 변수로 하 고는 메서드의 코드에서에서 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대 한 새 엔터티 컬렉션을 만듭니다을 코드에 적절 한 추가 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 속성을 선택한 다음 변경 내용이 데이터베이스에 저장 합니다. 호출할 필요가 없습니다는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 엔터티의 각 그룹 뒤 메서드, 여기서 단원의 하지만 코드는 데이터베이스에 쓰는 동안 예외가 발생 하면 문제의 원인의 찾을 수 있습니다 작업을 수행 합니다.

    사용 하 여 일부 데이터를 삽입 하는 문에 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드는 "upsert" 작업을 수행 하도록 합니다. 때문에 `Seed` 메서드를 실행할 때마다 실행 되는 `update-database` 명령, 각 마이그레이션 후 일반적으로 때문에 추가 하려고 하는 행 이미 있는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 데이터를 삽입할 수 없습니다. "Upsert" 작업이 있지만 이미 존재 하는 행을 삽입 하려고 할 경우 수행 하는 오류를 방지할 수 ***재정의*** 응용 프로그램을 테스트 하는 동안 실행 한 데이터 변경 사항이 있습니다. 테스트 테이블의에서 데이터 일부 원하지 않을 수 있습니다이 위해서는: 경우에 따라 테스트 하는 동안 데이터를 변경 하면 원하는 변경 내용을 데이터베이스 업데이트 후 하 게 유지 합니다. 조건부 삽입 작업을 수행 하려는 경우: 존재 하지 않는 경우에 행을 삽입 합니다. Seed 메서드는 두 가지 방법을 모두 사용합니다.

    에 전달 된 첫 번째 매개 변수는 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드 행 이미 존재 하는지 확인 하는 데 속성을 지정 합니다. 테스트 학생 데이터를 제공 하는 대 한는 `LastName` 속성 목록에 각 성이 고유 이므로이 용도로 사용할 수 수 있습니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    이 코드는 마지막 이름이 고유한 지 가정 합니다. 중복 되는 마지막 이름이 인 학생을 수동으로 추가 하는 경우 마이그레이션을 수행 하는 다음에 다음과 같은 예외를 얻을 수 있습니다.

    시퀀스에 요소가 둘 이상

    예: "Alexander Carson" 라는 두 명의 학생 중복 데이터를 처리 하는 방법에 대 한 정보를 참조 하십시오. [Seeding 및 디버깅 Entity Framework (EF)](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) Rick Anderson의 블로그에서 합니다. 에 대 한 자세한 내용은 `AddOrUpdate` 메서드를 참조 [EF 4.3 AddOrUpdate 메서드로 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) Julie Lerman 블로그.

    만드는 코드 `Enrollment` 있다고 가정 하 고 엔터티는 `ID` 값의 엔터티에 `students` 컬렉션, 컬렉션을 만드는 코드에서 해당 속성을 설정 하지 않은 있지만 합니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    사용할 수는 `ID` 여기에서 속성 때문에 `ID` 호출할 때 값이 설정 `SaveChanges` 에 대 한는 `students` 컬렉션입니다. 데이터베이스에 엔터티를 삽입 하 고 업데이트 하는 경우 자동으로 기본 키 값을 가져옵니다 EF는 `ID` 메모리에는 엔터티의 속성입니다.

    각 추가 하는 코드 `Enrollment` 엔터티를는 `Enrollments` 엔터티 집합을 사용 하지는 `AddOrUpdate` 메서드. 확인 하는 경우 엔터티 이미 있으며 존재 하지 않는 경우 엔터티를 삽입 합니다. 이 방법은 응용 프로그램 UI를 사용 하 여 등록 등급에 수행한 변경 내용을 유지 됩니다. 코드의 각 멤버를 반복는 `Enrollment` [목록](https://msdn.microsoft.com/library/6sh2ey19.aspx) 등록 데이터베이스에 없는 경우에 등록 데이터베이스에 추가 합니다. 데이터베이스를 업데이트 하는 처음으로 데이터베이스가 비어 있게 됩니다, 되므로 각 등록 추가 됩니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]
2. 프로젝트를 빌드합니다.

### <a name="execute-the-first-migration"></a>첫 번째 마이그레이션 실행

실행 하는 시기는 `add-migration` 명령, 마이그레이션을 처음부터 데이터베이스를 만들 수 있는 코드를 생성 합니다. 이 코드는 또한에 *마이그레이션* 라는 파일에 폴더  *&lt;타임 스탬프&gt;\_InitialCreate.cs*합니다. `Up` 의 메서드는 `InitialCreate` 클래스는 데이터 모델 엔터티 집합에 해당 하는 데이터베이스 테이블을 만듭니다 및 `Down` 메서드 삭제 합니다.

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

마이그레이션 호출은 `Up` 마이그레이션에 대 한 데이터 모델 변경 내용을 구현 하려면 메서드. Update, 마이그레이션 호출을 롤백해야 하는 명령을 입력할 때는 `Down` 메서드.

이 입력 했을 때 만들어진 초기 마이그레이션은 `add-migration InitialCreate` 명령입니다. 매개 변수 (`InitialCreate` 예제에서) 파일에 사용; 단어 또는 구를 마이그레이션에서 수행 되는 것을 요약 하는 일반적으로 선택 하면 이름을 지정 하 고 원하는 작업이 무엇이 든 될 수 있습니다. 나중에 마이그레이션할 이름을 지정할 수 있습니다는 예를 들어 &quot;AddDepartmentTable&quot;합니다.

데이터베이스가 이미 존재 하는 경우 초기 마이그레이션을 만든 경우 데이터베이스 만들기 코드 생성 되지만 데이터베이스는 이미 데이터 모델 일치 하기 때문에 실행할 필요는 없습니다. 여기서 데이터베이스가 아직 없는, 데이터베이스를 만들려면이 코드가 실행 되는 다른 환경에 앱을 배포할 때 하므로 이기 먼저 테스트 하는 것이 좋습니다. 바로 이러한 이유로 마이그레이션을 처음부터 다시 만들 수 있도록 이전-연결 문자열에 데이터베이스의 이름을 변경 합니다.

1. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.

    `update-database`

    ![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    `update-database` 명령이 실행 되는 `Up` 데이터베이스를 만들고 해당 메서드를 실행 된 `Seed` 데이터베이스를 채우는 메서드. 동일한 프로세스가 실행 될 자동으로 프로덕션 환경에서 응용 프로그램을 배포한 후 다음 섹션에서 확인할 수 있습니다.
- 사용 하 여 **서버 탐색기** 를 첫 번째 자습서에서와 같이 데이터베이스를 검사 하 고 작동 하는지 확인 하려면 모든 여전히 동일한 이전 처럼 응용 프로그램을 실행 합니다.

## <a name="deploy-to-azure"></a>Azure에 배포

지금까지 응용 프로그램에 되었습니다에서 로컬로 실행 중 IIS Express에서 개발 컴퓨터. 인터넷을 통해 사용 하도록 다른 사용자가 사용할 수 있도록 하려면 웹 호스팅 공급자를 배포 해야 합니다. 이 자습서의이 섹션에서는 Azure에 배포 합니다. 이 섹션은 선택 사항입니다. 이 절차를 생략 하 고 다음 자습서를 계속 진행 하거나 선택한 다른 호스팅 공급자에 대 한이 섹션의 지침을 조정할 수 있습니다.

### <a name="using-code-first-migrations-to-deploy-the-database"></a>Code First 마이그레이션을 사용 하 여 데이터베이스를 배포

데이터베이스를 배포 하는 Code First 마이그레이션을 사용 합니다. Visual Studio에서 배포에 대 한 설정을 구성 하는 데 사용할 수 있는 게시 프로필을 만들 때에 이라는 확인란도 선택 합니다 **데이터베이스 업데이트**합니다. 이 설정을 사용 하면 배포 프로세스를 자동으로 응용 프로그램을 구성할 *Web.config* Code First 사용 하 여 있도록 대상 서버에서 파일의 `MigrateDatabaseToLatestVersion` 이니셜라이저 클래스입니다.

Visual Studio 프로젝트는 대상 서버로 복사 하는 동안 배포 프로세스 중 데이터베이스와 함께 어떤 작업도 수행 하지 않습니다. 배포 된 응용 프로그램을 실행 하 고 배포 후 처음으로 데이터베이스에 액세스 하는 경우 Code First 데이터 모델 데이터베이스에 일치 하는 경우 확인 합니다. 불일치가 있을 경우 Code First 자동으로 데이터베이스를 만듭니다 (아직 존재 하지 않는) 하는 경우 또는 최신 버전으로 데이터베이스 스키마 업데이트 (경우 데이터베이스는 존재 하지만 모델 일치 하지 않습니다). 응용 프로그램에는 마이그레이션이 구현 하는 경우 `Seed` 메서드, 데이터베이스를 만들거나 스키마 업데이트 후의 메서드를 실행 합니다.

마이그레이션을 `Seed` 메서드 테스트 데이터를 삽입 합니다. 프로덕션 환경에 배포 하는 경우 변경 해야 합니다는 `Seed` 메서드 한다는 프로덕션 데이터베이스에 삽입할 수 있는 데이터를 삽입 합니다. 예를 들어, 현재 데이터 모델에서 실제 courses 하지만 가상의 학생 개발 데이터베이스에 대 한 수 있습니다. 작성할 수 있습니다는 `Seed` 메서드를 둘 다 개발에서 로드 하 고 다음 주석으로 처리 가상의 학생 프로덕션에 배포 하기 전에. 작성할 수 있습니다는 `Seed` 과정만 로드 하는 응용 프로그램의 UI를 사용 하 여 가상의 학생에 테스트 데이터베이스에 직접 입력 메서드입니다.

### <a name="get-an-azure-account"></a>Azure 계정 얻기

Azure 계정이 필요 합니다. 아직 없는 하나, Visual Studio 구독이 있는 경우 다음을 할 수 있습니다 [구독 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)합니다. 그렇지 않은 경우 몇 분에서에서 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/)합니다.

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>Azure에서 웹 사이트 및 SQL 데이터베이스 만들기

Azure에서 웹 앱은 다른 Azure 클라이언트와 공유 되는 가상 컴퓨터 (Vm)에서 실행 되는 공유 호스팅 환경에서 실행 됩니다. 공유 호스팅 환경 수 있는 방법이 저렴 한 비용 클라우드에서 시작 합니다. 이상 버전에서는 웹 트래픽 증가 하는 경우 응용 프로그램 전용된 Vm에서 실행 하 여 필요에 맞게 확장할 수 있습니다. 자세한 가격 책정 옵션에 대 한 Azure 앱 서비스에 대 한 설명서에서 읽은 [Azure Docs](https://azure.microsoft.com/pricing/details/app-service/)

Azure SQL 데이터베이스에 데이터베이스를 배포 합니다. SQL 데이터베이스는 SQL Server 기술을 기반으로 하는 클라우드 기반의 관계형 데이터베이스 서비스입니다. SQL 데이터베이스 도구와 SQL Server와 함께 작동 하는 응용 프로그램 에서도 작동 합니다.

1. [Azure 관리 포털](https://portal.azure.com), 클릭 **새로** 왼쪽된 탭에서를 클릭 **스크롤하게** 새 블레이드 누른 **웹 응용 프로그램, SQL** 에 **웹** 섹션 마지막으로 **만들기**합니다.

    ![관리 포털에서 새로 만들기 단추](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/CreateWeb-Sql.png)

 **새 웹 응용 프로그램, SQL-만들** 마법사가 열립니다.

2. 블레이드에서 문자열을 입력에서 **응용 프로그램 이름** 상자 응용 프로그램에 대 한 고유 URL로 사용할 수 있습니다. 전체 URL을 입력 한 내용을 여기과 Azure 앱 서비스의 기본 도메인으로 구성 됩니다 (. azurewebsites.net). 경우는 **응용 프로그램 이름** 이미 수행 되지 않고 마법사는 알려주고이 빨간색 *응용 프로그램 이름을 사용할 수 없으면* 메시지입니다. 경우는 **응용 프로그램 이름** 은 사용할 수 있는 얻게 됩니다 녹색 확인 표시 합니다.

    ![관리 포털에서 데이터베이스 링크를 사용 하 여 만들기](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Create-WebApp.png)

3. 에 **구독** 드롭다운에서 Azure 구독을 선택 하세요는 **앱 서비스** 를 두어야 합니다.

4. 에 **리소스 그룹** 입력란 리소스 그룹을 선택 하거나 새로 만듭니다. 이 설정은 웹 사이트에서 실행 되는 데이터 센터를 지정 합니다. 리소스 그룹에 대 한 자세한 내용은 설명서에서 읽은 [Azure Docs](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)합니다.
5. 새 **앱 서비스 계획** 클릭 하 여는 *앱 서비스 섹션*, **새로 만들기**를 입력 하 고 **앱 서비스 계획** (동일한 이름으로 될 수 있음 앱 서비스) **위치**, 및 **가격 책정 계층** (사용 가능한 옵션은).

    ![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Create-AppService.png)
6. 클릭는 **SQL 데이터베이스**, 선택 *새로 만들기* 하거나 기존 데이터베이스를 선택 합니다.

    ![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Create-Database.png)

7. 에 **이름** 상자에 데이터베이스에 대 한 이름을 입력 합니다.
8. 클릭는 **대상 서버** 상자 **새 서버 만들기**합니다. 또는 이전에 서버를 만든 경우 해당 서버를 사용할 수 있는 서버 목록에서 선택할 수 있습니다.
9. 선택 **가격 책정 계층** 섹션에서 선택 *무료*합니다. 추가 리소스는 필요한 경우 언제 든 지를 데이터베이스에 확장할 수 있습니다. Azure SQL 가격에 대 한 자세한 내용을 보려면, 설명서에서 읽은 [Azure Docs](https://azure.microsoft.com/pricing/details/sql-database/)합니다.
10. 수정 [데이터 정렬](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support) 필요에 따라 합니다.
11. 관리자가 입력 **SQL 관리자 사용자 이름** 및 **SQL 관리자 암호**합니다. 선택한 경우 **새 SQL 데이터베이스 서버**, 기존 이름 및 암호를 입력 하지, 새 이름 및 데이터베이스에 액세스할 때 나중에 다시 사용할 이제 정의 하는 암호를 입력 합니다. 이전에 만든 서버를 선택한 경우에 해당 서버에 대 한 자격 증명을 입력 합니다.
12. Application Insights를 사용 하 여 응용 프로그램 서비스에 대 한 원격 분석 수집을 사용할 수 있습니다. Application Insights 거의 구성 사용 하 여 중요 한 이벤트, 예외, 종속성, 요청 및 추적 정보를 수집 합니다. 시작 하려면 Application Insights에 대 한 자세한 내용은 [Azure Docs](https://azure.microsoft.com/services/application-insights/)합니다.
12. 클릭 **만들기** 완료 되 나타내려면 블레이드 맨 아래에 있습니다.
  
 관리 포털의 대시보드 페이지에 반환 및 **알림** 블레이드 페이지 맨 위에 있는 사이트가 생성 되 고 있음을 보여 줍니다. 잠시 후 (일반적으로 보다 작음 1 분), 배포 성공 알림이 됩니다. 왼쪽 탐색 모음에서 새 **앱 서비스** 에 표시는 *응용 프로그램 서비스* 섹션과 새 **SQL 데이터베이스** 에 표시는 *SQL 데이터베이스*  섹션.

### <a name="deploy-the-application-to-azure"></a>Azure 응용 프로그램 배포

1. Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시** 상황에 맞는 메뉴입니다.
  
    ![프로젝트 상황에 맞는 메뉴에서 게시](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)
2. 에 **프로필** 탭은 **웹 게시** 마법사를 클릭 하 여 **Microsoft Azure 앱 서비스**합니다.
  
    ![게시 설정 가져오기](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-ChooseTarget.png)
3. Visual Studio에서 Azure 구독을 이전에 추가 하지 않은 경우 화면에 단계를 수행 합니다. 다음이 단계를 사용 하도록 설정 연결 하도록 Visual Studio Azure 구독에 있으므로 목록이 **응용 프로그램 서비스** 웹 사이트가 포함 됩니다.
 
4. 선택 된 **구독** 다음에 앱 서비스를 추가한는 **앱 서비스 계획** 앱 서비스의 일부인 폴더 마지막으로 **앱 서비스** 이어서 자체 **확인**합니다.

    ![앱 서비스 선택](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-AppService.png)
5. 프로필을 구성한 후의 **연결** 탭이 표시 됩니다. 클릭 **연결 유효성 검사** 설정이 정확한 지 확인 하려면

    ![연결 확인](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Connection.png)
7. 연결 검증 된 녹색 확인 표시가 옆에 표시 되는 **연결 유효성 검사** 단추입니다. **다음**을 클릭합니다.
  
    ![성공적으로 유효성이 검사 된 연결](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-SettingsValidated.png)
8. 열기는 **원격 연결 문자열** 드롭 다운 목록에서 **SchoolContext** 만든 데이터베이스에 대 한 연결 문자열을 선택 합니다.
9. 선택 **데이터베이스 업데이트**합니다.

    ![설정 탭](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Settings.png)

    이 설정을 사용 하면 배포 프로세스를 자동으로 응용 프로그램을 구성할 *Web.config* Code First 사용 하 여 있도록 대상 서버에서 파일의 `MigrateDatabaseToLatestVersion` 이니셜라이저 클래스입니다.
10. **다음**을 클릭합니다.
11. 에 **미리 보기** 탭을 클릭 **미리 보기 시작**합니다.
  
    ![미리 보기 탭에서 미리 단추](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Preview.png)
  
 탭에는 서버에 복사 되는 파일의 목록이 표시 됩니다. 미리 보기를 표시할 응용 프로그램을 게시 하 필요 하지 않지만 알아두어야 하는 유용한 기능을 합니다. 이 경우 표시 되는 파일의 목록으로 아무 작업도 수행할 필요가 없습니다. 이 응용 프로그램을 배포한 다음에이 목록에 변경 된 파일만 됩니다.
    ![미리 파일 출력](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-PreviewLoaded.png)

12. **게시**를 클릭합니다.
 Visual Studio Azure 서버에 파일을 복사 프로세스를 시작 합니다.
13. **출력** 창 수행 된 배포 작업을 표시 및 배포를 성공적으로 완료를 보고 합니다.
  
    ![성공적인 배포를 보고 하는 출력 창](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-BuildOutput.png)
14. 배포가 성공 하면 기본 브라우저가 자동으로 배포 된 웹 사이트의 URL로 열립니다.
 만든 응용 프로그램은 클라우드에서 실행 됩니다. 
  
    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Site.png)

이 시점에서 프로그램 *SchoolContext* 데이터베이스 선택 했기 때문에 Azure SQL 데이터베이스에 생성 되었음을 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다. *Web.config* 배포 된 웹 사이트의 파일이 변경 되어 있도록는 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저 코드에서 읽거나 (발생 하는 데이터베이스에 데이터를 쓸 처음으로 실행 선택 하는 경우는 **학생** 탭):

![](https://asp.net/media/4367421/mig.png)

배포 프로세스에도 새 연결 문자열을 생성 *(SchoolContext\_의 DatabasePublish*) 데이터베이스 스키마를 업데이트 하 고 시드 데이터베이스에 사용할 Code First 마이그레이션에 대 한 합니다.

![Database_Publish 연결 문자열](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

배포 된 버전에서 자신의 컴퓨터에서 Web.config 파일을 찾을 수 있습니다 *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*합니다. 가 배포에 액세스할 수 있습니다 *Web.config* FTP를 사용 하 여 자체 파일입니다. 자세한 내용은 [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)합니다. 로 시작 하는 지침에 따라 "FTP 도구를 사용 하려면 다음 세 가지: FTP URL, 사용자 이름 및 암호."

> [!NOTE]
> 웹 앱 URL을 검색 하는 모든 사람이 데이터를 변경할 수 보안을 구현 하지 않습니다. 웹 사이트를 보호 하는 방법에 지침은 [멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 응용 프로그램을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 중이거나 다른 사용자가 Azure 관리 포털을 사용 하 여 사이트를 사용 하 여 또는 **서버 탐색기** 사이트를 중지 하려면 Visual Studio에서 합니다.


![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Stop-Service.png)

## <a name="advanced-migrations-scenarios"></a>고급 마이그레이션 시나리오

이 자습서에 나와 있는 것 처럼 자동으로 마이그레이션을 실행 하 여 데이터베이스를 배포 하는 경우 여러 서버에서 실행 되는 웹 사이트에 배포 하는 여러 서버 마이그레이션을 동시에 실행 하는 동안 얻을 수 있습니다. 마이그레이션은 원자성 이므로 두 서버를 동일한 마이그레이션 실행 하려고 하는 경우 하나에 성공 하 고 다른 (작업을 두 번 수행할 수 없습니다. 가정할 경우)에 실패 합니다. 이 시나리오에서 이러한 문제를 방지 하려면 마이그레이션을 수동으로 호출할 수 있고 으로만 발생 하는 한 번만 있도록 사용자 고유의 코드를 설정 합니다. 자세한 내용은 참조 [실행 및 코드에서 마이그레이션을 스크립팅](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/) Rowan Miller 블로그 및 [Migrate.exe](https://msdn.microsoft.com/data/jj618307) (에 대 한 마이그레이션 명령줄에서 실행 중) msdn 합니다.

다른 마이그레이션 시나리오에 대 한 자세한 내용은 참조 하십시오. [마이그레이션 동영상 가이드 시리즈](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)합니다.

## <a name="code-first-initializers"></a>코드의 첫 번째 이니셜라이저

배포 섹션에서 언급 했 듯이 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저를 사용 하 고 있습니다. 먼저 또한 제공 다른 이니셜라이저를 포함 하 여 [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (기본값) 이면 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) (이전 사용)입니다 및 [ DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)합니다. `DropCreateAlways` 이니셜라이저는 단위 테스트에 대 한 조건을 설정 하는 데 유용할 수 있습니다. 사용자 고유의 이니셜라이저를 작성할 수 있습니다 및 응용 프로그램에서 읽거나 데이터베이스에 기록 될 때까지 대기 하지 않을 경우 이니셜라이저를 명시적으로 호출할 수 있습니다. 이 자습서에서는 2013 년 11 월에에서 쓸 때에서 마이그레이션을 사용 하도록 설정 하기 전에 만들기 및 DropCreate 이니셜라이저만 사용할 수 있습니다. Entity Framework 팀이 이러한 이니셜라이저에도 마이그레이션과 함께 사용할 수 있는 작업입니다.

이니셜라이저에 대 한 자세한 내용은 참조 [의 Entity Framework Code First 이해 데이터베이스 이니셜라이저](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm) 및 책의 6 장 [프로그래밍 Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 하 여 및 Rowan Miller 합니다.

## <a name="summary"></a>요약

이 자습서에서는 마이그레이션을 사용 하도록 설정 하 고 응용 프로그램을 배포 하는 방법에 살펴보았습니다. 다음 자습서에서는 데이터 모델을 확장 하 여 더 많은 고급 항목을 살펴보고 먼저 하겠습니다.

이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](xref:whitepapers/aspnet-data-access-content-map)합니다.

>[!div class="step-by-step"]
[이전](xref:mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)
[다음](xref:mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application)
