---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF 마이그레이션을 사용 하 고 Azure에 배포'
author: tdykstra
description: 이 자습서에서는 Code First 마이그레이션을 사용 하도록 설정 하 고 Azure에서 클라우드로 응용 프로그램을 배포 합니다.
ms.author: riande
ms.date: 01/16/2019
ms.topic: tutorial
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: dd6bf5d8eb8a05dad1d230ef40c9b863e2af7094
ms.sourcegitcommit: d5223cf6a2cf80b4f5dc54169b0e376d493d2d3a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54889914"
---
# <a name="tutorial-use-ef-migrations-in-an-aspnet-mvc-app-and-deploy-to-azure"></a>자습서: ASP.NET MVC 앱에서 EF 마이그레이션을 사용 하 고 Azure에 배포

지금까지 Contoso University 샘플 웹 응용 프로그램에서 실행 되었음을 로컬 IIS Express 개발 컴퓨터에 있습니다. 실제 응용 프로그램을 사용 하 여 인터넷을 통해 다른 사람들이 사용할 수 있도록 하려면 웹 호스팅 공급자에 배포 해야 합니다. 이 자습서에서는 Code First 마이그레이션을 사용 하도록 설정 하 고 Azure에서 클라우드로 응용 프로그램을 배포 합니다.

- Code First 마이그레이션을 사용 하도록 설정 합니다. 마이그레이션 기능을 사용 하면 데이터 모델을 변경 하 고 삭제 하 고 데이터베이스를 다시 만들 필요 없이 데이터베이스 스키마를 업데이트 하 여 변경 내용을 프로덕션에 배포할 수 있습니다.
- Azure에 배포 합니다. 이 단계는 선택 사항입니다. 프로젝트를 배포 하지 않고 나머지 자습서를 사용 하 여 계속할 수 있습니다.

소스 제어를 사용 하 여 지속적인 통합 프로세스를 사용 하 여 배포에 대 한 있지만이 자습서에서는 해당 항목을 다루지 않습니다 하는 것이 좋습니다. 자세한 내용은 참조는 [소스 제어](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) 및 [연속 통합](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) 의 단원은 [Azure 사용 하 여 실제 클라우드 앱 빌드](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)합니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * Code First 마이그레이션을 사용 하도록 설정
> * (선택 사항) Azure에서 앱 배포

## <a name="prerequisites"></a>전제 조건

- [연결 복원력 및 명령 인터셉션](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-code-first-migrations"></a>Code First 마이그레이션을 사용 하도록 설정

새 애플리케이션을 개발하는 경우 데이터 모델은 자주 변경되며 모델이 변경될 때마다 데이터베이스와 동기화를 가져옵니다. 자동으로 삭제 하 고 데이터 모델을 변경할 때마다 데이터베이스를 다시 만들지를 Entity Framework를 구성 했습니다. 때 추가, 제거 또는 엔터티 클래스를 변경 하거나 변경 하 `DbContext` 클래스 다음에 응용 프로그램을 실행할 때 자동으로 기존 데이터베이스를 삭제, 모델을 테스트 데이터로 시드합니다를 새로 만듭니다.

데이터베이스를 데이터 모델과 동기화된 상태로 유지하는 이 메서드는 애플리케이션을 프로덕션 환경에 배포할 때까지 잘 작동합니다. 프로덕션 환경에서 실행 중이면 응용 프로그램을 유지 하 고 새 열을 추가 하는 등 변경 될 때마다 모든 손실 하지 않으려는 데이터를 저장 일반적으로 합니다. 합니다 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 삭제 하 고 데이터베이스를 다시 작성 하는 대신 데이터베이스 스키마를 업데이트 하려면 Code First를 사용 하 여이 문제를 해결 하는 기능입니다. 이 자습서에서는 응용 프로그램을 배포 하 고를 준비 하려면 마이그레이션 사용 됩니다.

1. 이전 주석으로 처리 하거나 삭제 하 여 설정한 이니셜라이저를 사용 하지 않도록 설정 된 `contexts` 응용 프로그램 Web.config 파일에 추가 하는 요소입니다.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. 응용 프로그램에도 *Web.config* 파일, 연결 문자열에 데이터베이스의 이름을 ContosoUniversity2로 변경 합니다.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    이 변경은 첫 번째 마이그레이션이 새 데이터베이스를 만들 수 있도록 프로젝트를 설정 합니다. 이 필요치 있지만 것이 좋습니다 나중에 확인할 수 있습니다.
3. **도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

1. 에 `PM>` 프롬프트에 다음 명령을 입력 합니다.

    ```text
    enable-migrations
    add-migration InitialCreate
    ```

    `enable-migrations` 명령은 만듭니다는 *마이그레이션을* ContosoUniversity 프로젝트에서 폴더는 폴더에 저장을 *Configuration.cs* 파일을 편집 하 여 마이그레이션을 구성할 수 있습니다.

    (데이터베이스 이름을 변경 하도록 안내 하는 위의 단계를 놓친 경우는 기존 데이터베이스 마이그레이션과 자동으로 수행 된 `add-migration` 명령입니다. 좋은 현상, 데이터베이스를 배포 하기 전에 마이그레이션 코드의 테스트를 실행 하지 않습니다 뜻입니다. 실행할 때 이상는 `update-database` 명령을 데이터베이스에 이미 있기 때문에 아무 작업도 수행 합니다.)

    엽니다는 *ContosoUniversity\Migrations\Configuration.cs* 파일입니다. 이니셜라이저 클래스는 이전에 본 것 처럼 합니다 `Configuration` 클래스에 포함 되어는 `Seed` 메서드.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    용도 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드를 삽입 하거나 Code First를 만들거나 데이터베이스를 업데이트 한 후 테스트 데이터를 업데이트할 수 있도록 하는 것입니다. 메서드는 데이터베이스를 만들 때와 데이터 모델을 변경한 후 데이터베이스 스키마가 업데이트 될 때마다 호출 됩니다.

### <a name="set-up-the-seed-method"></a>Seed 메서드 설정

사용할 이니셜라이저 클래스의 삭제 하 고 모든 데이터 모델 변경에 대해 데이터베이스를 다시 만드는 경우 `Seed` 모델 변경할 때마다 데이터베이스가 삭제 됩니다 때문에 테스트 데이터를 삽입 하는 방법 및 모든 테스트 데이터가 손실 됩니다. Code First 마이그레이션, 데이터베이스 변경 후 데이터는 유지 하는 테스트의 테스트 데이터를 포함 하므로 합니다 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 일반적으로 메서드는 필요 없습니다. 사실, 원하지는 `Seed` 사용할 마이그레이션 데이터베이스를 프로덕션에 배포 하려면 때문에 경우에 테스트 데이터를 삽입 하는 방법의 `Seed` 메서드는 프로덕션 환경에서 실행 됩니다. 원하는 경우는 `Seed` 프로덕션 환경에서 필요한 데이터만 데이터베이스에 삽입 하는 방법입니다. 예를 들어 데이터베이스의 실제 부서 이름을 포함 하려면이 좋습니다는 `Department` 응용 프로그램이 프로덕션 환경에서 사용 가능 해지면 테이블입니다.

이 자습서에서는 사용할 마이그레이션 배포용 하지만 `Seed` 메서드는 테스트 데이터 삽입 그래도 쉽게 응용 프로그램 기능을 많은 양의 데이터를 수동으로 삽입 하지 않고도 작동 하는 방식을 확인 합니다.

1. 내용을 대체 합니다 *Configuration.cs* 새 데이터베이스 테스트 데이터를 로드 하는 다음 코드를 사용 하 여 파일입니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    합니다 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드는 입력된 매개 변수로 데이터베이스 컨텍스트 개체를 사용 하 고 메서드에서 코드를 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대 한 코드를 새 엔터티 컬렉션을 만듭니다, 적절 한 추가한 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 속성 및 데이터베이스에 변경 내용 저장 합니다. 호출할 필요는 없습니다 합니다 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 엔터티의 각 그룹 뒤 메서드를으로 여기에서 수행 되지만 코드는 데이터베이스에 쓰는 동안 예외가 발생 하는 경우 문제의 소스를 찾을 수 있습니다 작업을 수행 합니다.

    일부 데이터를 삽입 하는 문을 사용 합니다 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) "upsert" 작업을 수행 하는 방법입니다. 때문에 합니다 `Seed` 메서드를 실행할 때마다 실행 되는 `update-database` 명령, 일반적으로 각 마이그레이션 후 이기 때문에 추가 하려는 행 이미 있는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 데이터를 삽입할 수 없습니다. "Upsert" 작업 하지만 이미 존재 하는 행을 삽입 하려고 할 경우는 오류를 방지할 수 ***재정의*** 응용 프로그램을 테스트 하는 동안 만들어졌을 수 있는 데이터를 변경 합니다. 일부 테이블의 테스트 데이터를 사용 하 여 하지 않으려는 경우이 위해서는: 경우에 따라 테스트 하는 동안 데이터를 변경한 경우 원하는 데이터베이스 업데이트 후 유지 하려면 변경 내용을 합니다. 조건부 삽입 작업을 수행 하려는 경우: 존재 하지 않는 경우에 행을 삽입 합니다. Seed 메서드는 두 가지 방법을 모두 사용합니다.

    첫 번째 매개 변수가 전달 되는 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드는 행이 이미 존재 하는지 확인 하는 데 속성을 지정 합니다. 테스트 학생 데이터를 제공 하는 대 한는 `LastName` 목록의 마지막 이름이 있으므로이 목적을 위해 속성을 사용 수 있습니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    이 코드는 마지막 이름이 고유한 지를 가정 합니다. 마지막 이름이 중복 된 학생을 수동으로 추가 하는 경우 마이그레이션을 수행한 다음에 다음 예외를 볼 수 있습니다.

    **시퀀스에 요소가 둘 이상**

    예: "Alexander Carson" 라는 두 학생 중복 데이터를 처리 하는 방법에 대 한 정보를 참조 하세요 [시드 및 디버깅 EF (Entity Framework) Db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) Rick Anderson의 블로그에서입니다. 에 대 한 자세한 내용은 합니다 `AddOrUpdate` 메서드를 참조 하세요 [EF 4.3 AddOrUpdate 메서드를 사용 하 여 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) Julie Lerman의 블로그입니다.

    만드는 코드를 `Enrollment` 엔터티가 있다고 가정 합니다 `ID` 에 있는 엔터티의 값은 `students` 컬렉션 컬렉션을 만드는 코드는 해당 속성을 설정 하지 않은 하지만 합니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    사용할 수는 `ID` 여기서 속성 때문에 `ID` 를 호출할 때 값이 설정 `SaveChanges` 에 대 한는 `students` 컬렉션입니다. 데이터베이스 엔터티 삽입 및 업데이트 하는 경우 자동으로 기본 키 값을 가져옵니다 EF는 `ID` 메모리에서 엔터티의 속성입니다.

    각 추가 하는 코드 `Enrollment` 엔터티를 합니다 `Enrollments` 엔터티 집합을 사용 하지 않습니다는 `AddOrUpdate` 메서드. 확인 하는 경우 엔터티의 이미 있으며 존재 하지 않는 경우 엔터티를 삽입 합니다. 이 이렇게 변경 하면는 등록 엔터프라이즈급 응용 프로그램 UI를 사용 하 여이 유지 됩니다. 코드의 각 멤버를 반복 합니다 `Enrollment` [목록](https://msdn.microsoft.com/library/6sh2ey19.aspx) 등록 데이터베이스에 없는 경우에 등록 데이터베이스에 추가 합니다. 처음으로 데이터베이스를 업데이트할 데이터베이스 비게 됩니다 되므로 각 등록 추가 됩니다.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

2. 프로젝트를 빌드합니다.

### <a name="execute-the-first-migration"></a>첫 번째 마이그레이션 실행

실행 하는 시기를 `add-migration` 명령을 마이그레이션을 처음부터 데이터베이스를 만들 수 있는 코드를 생성 합니다. 이 코드는 또한에 *마이그레이션을* 라는 파일에 있는 폴더  *&lt;타임 스탬프&gt;\_InitialCreate.cs*합니다. `Up` 메서드를 `InitialCreate` 클래스에는 데이터 모델 엔터티 집합에 해당 하는 데이터베이스 테이블을 만듭니다 및 `Down` 메서드를 삭제 합니다.

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다. 업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다.

이 입력 했을 때 만들어진 초기 마이그레이션을 `add-migration InitialCreate` 명령입니다. 매개 변수 (`InitialCreate` 예제에서) 파일에 사용 되는 단어 또는 구를 요약 마이그레이션에서 수행 되는 일반적으로 선택;에 이름을 지정 하 고 원하는 수. 예를 들어 이후 마이그레이션의 이름을 수 있습니다 &quot;AddDepartmentTable&quot;합니다.

데이터베이스가 이미 존재할 때 초기 마이그레이션을 만든 경우 데이터베이스 만들기 코드가 생성되지만 데이터베이스는 이미 데이터 모델과 일치하기 때문에 실행할 필요는 없습니다. 데이터베이스가 아직 없는 다른 환경에 앱을 배포하는 경우 이 코드를 실행하여 데이터베이스를 만들기 때문에 먼저 테스트하는 것이 좋습니다. 이유는 앞서 연결 문자열에서 데이터베이스의 이름을 변경 했으면&mdash;마이그레이션을 처음부터 새로 만들 수 있도록 합니다.

1. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.

    `update-database`

    합니다 `update-database` 명령이 실행 되는 `Up` 데이터베이스를 만들고 해당 메서드를 실행 합니다 `Seed` 데이터베이스를 채우는 방법입니다. 동일한 프로세스에서에서 실행 됩니다 자동으로 프로덕션 응용 프로그램을 배포한 후 다음 섹션에서 확인할 수 있습니다.
2. 사용 하 여 **서버 탐색기** 첫 번째 자습서에서 수행한 것 처럼 데이터베이스를 검사 하 여 작동 하는지 확인 하려면 모든 여전히 동일한 이전 처럼 응용 프로그램을 실행 합니다.

## <a name="deploy-to-azure"></a>Azure에 배포

지금까지 응용 프로그램에서 실행 되었음을 로컬 IIS Express 개발 컴퓨터에 있습니다. 인터넷을 통해 사용 하도록 다른 사용자를 위해 사용할 수 있도록 하려면 웹 호스팅 공급자를 배포 해야 합니다. 자습서의이 섹션에서는 Azure에 배포 됩니다. 이 섹션은 선택 사항입니다. 이 생략 하 고 계속 다음 자습서를 진행 또는 원하는 다른 호스팅 공급자에 대 한이 섹션의 지침을 조정할 수 있습니다.

### <a name="use-code-first-migrations-to-deploy-the-database"></a>Code First 마이그레이션을 사용 하 여 데이터베이스를 배포 하려면

데이터베이스를 배포 하려면 Code First 마이그레이션을 사용할 수 있습니다. Visual Studio에서 배포에 대 한 설정을 구성 하는 데 사용 하는 게시 프로필을 만들 때 확인란이 선택 **데이터베이스 업데이트**합니다. 이렇게이 설정 하면 자동으로 응용 프로그램을 구성 하는 배포 프로세스 *Web.config* Code First 사용 되도록 대상 서버에서 파일을 `MigrateDatabaseToLatestVersion` 이니셜라이저 클래스입니다.

Visual Studio 프로젝트가 대상 서버로 복사 하는 동안 배포 프로세스 중 데이터베이스를 사용 하 여 어떤 작업도 수행 하지 않습니다. 배포 된 응용 프로그램을 실행 하 고 배포 후 처음으로 데이터베이스에 액세스 하는 경우 Code First 데이터베이스 데이터 모델과 일치 하는 경우 확인 합니다. 불일치의 경우 Code First 자동으로 데이터베이스를 만듭니다 (아직 존재 하지 않는) 하는 경우 또는 최신 버전으로 데이터베이스 스키마 업데이트 (데이터베이스 존재 하지만 모델과 일치 하지 않습니다) 경우입니다. 응용 프로그램을 마이그레이션을 구현 하는 경우 `Seed` 메서드를 메서드 실행 후 데이터베이스를 만들거나 스키마 업데이트 됩니다.

마이그레이션을 `Seed` 메서드 테스트 데이터를 삽입 합니다. 변경 해야 프로덕션 환경에 배포 하는 경우는 `Seed` 메서드 한다는 프로덕션 데이터베이스에 삽입할 하려는 데이터를 삽입 합니다. 예를 들어, 현재 데이터 모델과 실제 과정 이지만 가상 학생 개발 데이터베이스에 하려는 합니다. 작성할 수 있습니다는 `Seed` 개발에서 모두를 로드 하 고 프로덕션에 배포 하기 전에 가상의 학생 들을 다음 주석 방법입니다. 작성할 수 있습니다 또는 `Seed` 과정만을 로드 하 고 응용 프로그램의 UI를 사용 하 여 테스트 데이터베이스에 가상의 학생 들에 게 수동으로 입력 방법입니다.

### <a name="get-an-azure-account"></a>Azure 계정 가져오기

Azure 계정이 필요 합니다. Visual Studio 구독을 필요가 없는, 하지만 수 있습니다 [구독 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/
)합니다. 이 고, 그렇지 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 하세요 [Azure 무료 평가판](https://azure.microsoft.com/free/)합니다.

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>Azure에서 웹 사이트 및 SQL database 만들기

Azure에서 웹 앱은 다른 Azure 클라이언트와 공유 되는 virtual machines (Vm)에서 실행 됨을 의미 하는 공유 호스팅 환경에서 실행 됩니다. 공유 호스팅 환경에는 클라우드에서 시작 방법 저렴 한 비용입니다. 나중에 웹 트래픽이 증가 하면 응용 프로그램 전용된 Vm에서 실행 하 여 필요에 맞게 확장할 수 있습니다. 가격 책정 옵션에 대 한 자세한 내용은 Azure App Service에 대 한 자세한 내용은 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)합니다.

Azure SQL database로 데이터베이스를 배포할 수 있습니다. SQL database는 SQL Server 기술에 기본 제공 되는 클라우드 기반 관계형 데이터베이스 서비스입니다. SQL database를 사용 하 여 도구와 SQL Server를 사용 하는 응용 프로그램 에서도 작동 합니다.

1. 에 [Azure 관리 포털](https://portal.azure.com), 선택 **리소스 만들기** 왼쪽에 탭을 선택한 다음 **모두 보기** 에 **새로 만들기** 창 (또는 *블레이드에서*)에 사용 가능한 모든 리소스를 참조 하세요. 선택 **웹 앱 + SQL** 에 **웹** 섹션의 **모든** 블레이드. 마지막으로 선택할 **만들기**합니다.

    ![Azure Portal에서 리소스 만들기](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/create-azure-resource.png)

   새 폼 **새 웹 앱 + SQL** 리소스 열립니다.

2. 에 문자열을 입력 합니다 **앱 이름** 상자를 응용 프로그램에 대 한 고유 URL로 사용 합니다. 전체 URL을 여기에 입력 및 Azure App Services의 기본 도메인으로 구성 됩니다 (. azurewebsites.net). 경우는 **앱 이름** 이미 수행 되지 않고 마법사 빨간색 알리는 메시지를 표시 합니다 *앱 이름을 사용할 수 없는* 메시지입니다. 경우는 **앱 이름** 는 녹색 확인 표시가 표시를 사용할 수 있습니다.

3. 에 **구독** 상자에서 만들려는 Azure 구독을 선택 합니다 **App Service** 상주 하 합니다.

4. 에 **리소스 그룹** 텍스트 상자에 리소스 그룹을 선택 하거나 새로 만듭니다. 이 설정은 웹 사이트에서 실행 됩니다 하는 데이터 센터를 지정 합니다. 리소스 그룹에 대 한 자세한 내용은 참조 하세요. [리소스 그룹](/azure/azure-resource-manager/resource-group-overview#resource-groups)합니다.

5. 새 **App Service 계획** 를 클릭 하 여는 *App Service 섹션*, **새로 만들기**를 입력 **App Service 계획** (같은 이름으로 일 수 있음 App Service) **위치**, 및 **가격 책정 계층** (사용 가능한 옵션은).

6. 클릭 **SQL Database**를 선택한 후 **새 데이터베이스를 만들** 하거나 기존 데이터베이스를 선택 합니다.

7. 에 **이름을** 상자에서 데이터베이스의 이름을 입력 합니다.
8. 클릭 합니다 **대상 서버** 상자를 선택한 후 **새 서버 만들기**합니다. 또는 서버를 이전에 만든 경우 해당 서버를 사용할 수 있는 서버 목록에서 선택할 수 있습니다.
9. 선택할 **가격 책정 계층** 섹션을 선택 *무료*합니다. 추가 리소스가 필요한 경우 데이터베이스 언제 든 지 확장할 수 있습니다. 에 대해 자세히 알아보려면 Azure SQL 가격 책정을 참조 하세요 [Azure SQL Database 가격 책정](https://azure.microsoft.com/pricing/details/sql-database/managed/)합니다.
10. 수정할 [데이터 정렬](/sql/relational-databases/collations/collation-and-unicode-support) 필요에 따라 합니다.
11. 관리자가 입력 **SQL 관리자 사용자 이름** 하 고 **SQL 관리자 암호**합니다.

   - 선택한 경우 **새 SQL Database 서버**, 새 이름 및 데이터베이스를 액세스 하는 경우 나중에 사용할 암호를 정의 합니다.
   - 이전에 만든 서버를 선택한 경우 해당 서버에 대 한 자격 증명을 입력 합니다.

12. Application Insights를 사용 하 여 App Service에 대 한 원격 분석 수집을 사용할 수 있습니다. 간단한 구성을 사용 하 여 Application Insights는 중요 한 이벤트, 예외, 종속성, 요청 및 추적 정보를 수집합니다. Application Insights에 대 한 자세한 내용은 참조 하세요 [Azure Monitor](https://azure.microsoft.com/services/monitor/)합니다.
13. 클릭 **만들기** 마친를 나타내기 위해 맨 아래에 있습니다.

    관리 포털에서 대시보드 페이지를 반환 하며 **알림을** 영역 페이지의 맨 위에 있는 사이트는 생성 되 고 있음을 보여 줍니다. 잠시 (일반적으로 1 분 미만), 알림은 배포 성공 합니다. 왼쪽 탐색 모음에서 새 App Service에 표시 합니다 **App Services** 섹션 및 새 SQL database에 표시 됩니다는 **SQL database** 섹션.

### <a name="deploy-the-app-to-azure"></a>Azure에 앱 배포

1. Visual studio에서에서 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **게시** 상황에 맞는 메뉴입니다.

2. 에 **게시 대상 선택** 페이지에서 **App Service** 차례로 **기존 항목 선택**를 선택한 후 **게시**합니다.

    ![게시 대상 페이지를 선택 합니다.](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/publish-select-existing-azure-app-service.png)

3. 이전에 Visual Studio에서 Azure 구독을 추가 하지 않았으면, 화면의 단계를 수행 합니다. 다음이 단계를 사용 하도록 설정 연결 하도록 Visual Studio Azure 구독에 있으므로 목록을 **App Services** 웹 사이트가 포함 됩니다.

4. 에 **App Service** 페이지에서를 **구독** App Service에 추가 합니다. 아래 **뷰**를 선택 **리소스 그룹**합니다. App Service에 추가한 리소스 그룹을 확장 하 고 App Service를 선택 합니다. 선택할 **확인** 앱을 게시 합니다.

5. 합니다 **출력** 어떤 배포 동작을 보여 줍니다. 창과 성공적인 배포 완료를 보고 합니다.

6. 배포에 성공 하면 기본 브라우저가 자동으로 배포 된 웹 사이트의 URL로 열립니다.

    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/cloud-app-browser.png)

    이제 앱은 클라우드에서 실행 됩니다.

이 시점에서 *SchoolContext* 데이터베이스가 선택 했기 때문에 Azure SQL database에서 생성 되었습니다 **Execute Code First Migrations (앱 시작 시 실행)** 합니다. 합니다 *Web.config* 배포 된 웹 사이트의 파일이 변경 되었습니다 있도록 합니다 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저 코드를 읽거나 (발생 하는 데이터베이스에서 데이터를 씁니다 처음으로 실행 선택 했을 **학생** 탭):

![Web.config 파일 발췌](https://asp.net/media/4367421/mig.png)

배포 프로세스에도 새 연결 문자열을 생성 *(SchoolContext\_DatabasePublish*) 데이터베이스 스키마를 업데이트 하 고 데이터베이스 시 딩에 사용 하도록 Code First 마이그레이션에 대 한 합니다.

![Web.config 파일에서 연결 문자열](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

Web.config 파일에서 자신의 컴퓨터에 배포 된 버전을 찾을 수 있습니다 *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*합니다. 배포에 액세스할 수 있습니다 *Web.config* FTP를 사용 하 여 자체 파일입니다. 자세한 내용은 [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)합니다. 로 시작 하는 지침에 따라 "FTP 도구를 사용 하려면 다음 세 가지: FTP URL, 사용자 이름 및 암호."

> [!NOTE]
> 웹 앱 URL을 습득 한 사람이 데이터를 변경할 수 있도록 보안을 구현 하지 않는 합니다. 웹 사이트를 보호 하는 방법에 지침은 [멤버 자격, OAuth 및 SQL database 사용 하 여 보안 ASP.NET MVC 앱을 Azure에 배포](/aspnet/core/security/authorization/secure-data)합니다. Azure 관리 포털을 사용 하 여 서비스를 중지 하 여 사이트를 사용 하 여 다른 사용자를 방지할 수 있습니다 또는 **서버 탐색기** Visual Studio에서.

![앱 서비스 메뉴 항목 중지](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/server-explorer-stop-app-service.png)

## <a name="advanced-migrations-scenarios"></a>고급 마이그레이션 시나리오

이 자습서에 표시 된 대로 자동으로 마이그레이션을 실행 하 여 데이터베이스를 배포 하는 경우 여러 서버에서 실행 되는 웹 사이트에 배포 하는 동시 마이그레이션을 실행 하는 동안 여러 서버를 가져올 수 있습니다. 마이그레이션 되므로 원자성 두 서버를 동일한 마이그레이션을 실행 하려고 하는 경우 하나는 성공 하 고 (작업을 두 번 수행할 수 없는 것으로 가정) 다른 하지 못합니다. 이 시나리오에서는 이러한 문제를 방지 하려는 경우 마이그레이션을 수동으로 호출할를 사용자 고유의 코드를 한 번 발생 되도록 설정 합니다. 자세한 내용은 [실행 및 코드에서 마이그레이션 스크립팅](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/) Rowan Miller 블로그 및 [Migrate.exe](/ef/ef6/modeling/code-first/migrations/migrate-exe) (에 대 한 마이그레이션 명령줄에서 실행 중).

다른 마이그레이션 시나리오에 대 한 자세한 내용은 [마이그레이션을 스크린 캐스트 시리즈가](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)합니다.

## <a name="code-first-initializers"></a>첫 번째 이니셜라이저 코드

배포 섹션에서 살펴보았습니다를 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저를 사용 합니다. 코드 먼저 제공 등 다른 이니셜라이저 [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (기본값), [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) (이전에 사용한)는 및 [ DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)합니다. `DropCreateAlways` 이니셜라이저는 단위 테스트에 대 한 조건을 설정 하는 데 유용할 수 있습니다. 고유한 이니셜라이저를 작성할 수도 있습니다 및 응용 프로그램에서 읽거나 데이터베이스에 기록 될 때까지 대기 하지 않으려는 경우 이니셜라이저를 명시적으로 호출할 수 있습니다.

이니셜라이저에 대 한 자세한 내용은 참조 하세요. [Entity Framework Code first 데이터베이스 이니셜라이저 이해](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm) 책의 6 장 및 [Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 및 Rowan Miller 합니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 자료

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](xref:whitepapers/aspnet-data-access-content-map)합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * Code First 마이그레이션을 사용 하도록 설정된
> * (선택 사항) Azure에서 앱 배포

ASP.NET MVC 응용 프로그램에 대 한 더 복잡 한 데이터 모델을 만드는 방법에 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [더 복잡 한 데이터 모델 만들기](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
