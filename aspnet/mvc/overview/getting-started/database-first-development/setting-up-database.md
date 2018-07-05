---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: Entity Framework 6 Database First MVC 5를 사용 하 여 시작 | Microsoft Docs
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: 98deeb91dc2b9a1bad535be1bf1e2ec85dfe4028
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371715"
---
<a name="getting-started-with-entity-framework-6-database-first-using-mvc-5"></a>Entity Framework 6 Database First MVC 5를 사용 하 여 시작
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다. 시리즈의 마지막 부분에서는 사이트 및 데이터베이스를 Azure에 배포 됩니다.
> 
> 시리즈의이 부분 데이터베이스를 만들고 데이터로 채우는에 중점을 둡니다.
> 
> 이 시리즈는 Tom Dykstra 및 Rick Anderson 기여를 사용 하 여 작성 되었습니다. 의견 섹션에는 사용자의 의견에로 기반 향상 되었습니다.


## <a name="introduction"></a>소개

이 항목에서는 기존 데이터베이스 및 신속 하 게 데이터와 상호 작용할 수 있도록 하는 웹 응용 프로그램을 만들기 시작 하는 방법을 보여 줍니다. 사용 하 여 Entity Framework 6 및 MVC 5 웹 응용 프로그램을 빌드합니다. ASP.NET 스 캐 폴딩 기능을 사용 하면 자동으로 표시, 업데이트, 만들기, 데이터 삭제에 대 한 코드를 생성할 수 있습니다. Visual Studio 내에서 게시 도구를 사용 하 여 쉽게 배포할 수 있습니다 사이트 및 데이터베이스를 Azure로 합니다.

이 항목에서는 데이터베이스 및 해당 데이터베이스의 필드를 기반으로 하는 웹 응용 프로그램에 대 한 코드를 생성 하려면 상황을 해결 합니다. 이 방법은 Database First 개발을 라고 합니다. 기존 데이터베이스를 아직 없는 경우 데이터 클래스를 정의 하 고 클래스 속성에서 데이터베이스 생성을 포함 하는 Code First 개발을 호출 하는 방법 대신 사용할 수 있습니다.

Code First 개발을 소개 하는 예제를 보려면 [ASP.NET MVC 5 시작](../introduction/getting-started.md)합니다. 고급 예제를 보려면 [ASP.NET MVC 4 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.

Entity Framework 접근 방식을 사용할 것인지를 선택 하는 지침을 참조 하세요 [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.

## <a name="prerequisites"></a>전제 조건

Visual Studio 2013 또는 Visual Studio Express 2013 for Web

## <a name="set-up-the-database"></a>데이터베이스 설정

기존 데이터베이스의 환경, 모방 하기 위해 먼저 데이터베이스 일부 미리 채워진 데이터로 만들고 데이터베이스에 연결 하는 웹 응용 프로그램을 만듭니다.

이 자습서는 Visual Studio 2013 또는 Visual Studio Express 2013을 사용 하 여 LocalDB를 사용 하 여 웹에 대 한 개발 되었습니다. 기존 데이터베이스 서버를 사용 하 여 LocalDB 대신 있지만 버전, Visual Studio 및 데이터베이스의 사용자 형식에 따라 모든 데이터 도구가 Visual Studio에서 지원 되지 않는 경우. 도구를 데이터베이스에 대해 사용할 수 없는 경우에 데이터베이스에 대 한 일부 관리 도구 모음 내에서 데이터베이스 관련 단계를 수행 하는 것이 해야 합니다.

Visual Studio 버전에서 데이터베이스 도구를 사용 하 여 문제가 있는 경우 최신 버전의 데이터베이스 도구를 설치 했는지 확인 합니다. 업데이트 또는 데이터베이스 도구를 설치 하는 방법에 대 한 내용은 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027)합니다.

Visual Studio를 시작 하 고 만듭니다는 **SQL Server 데이터베이스 프로젝트**합니다. 프로젝트 이름을 **ContosoUniversityData**합니다.

![데이터베이스 프로젝트 만들기](setting-up-database/_static/image1.png)

이제 빈 데이터베이스 프로젝트가 있습니다. 프로젝트의 대상 플랫폼으로 Azure SQL Database를 설정 해야 하므로이 자습서의 뒷부분에서 Azure에이 데이터베이스를 배포 합니다. 대상 플랫폼을 설정 실제로 배포 되지는 않습니다 데이터베이스 데이터베이스 프로젝트 데이터베이스 디자인 대상 플랫폼과 호환 되는지 확인 합니다만 의미 합니다. 대상 플랫폼을 설정 하려면 엽니다는 **속성** 선택한 프로젝트에 대 한 **Microsoft Azure SQL Database** 대상 플랫폼에 대 한 합니다.

![집합 대상 플랫폼](setting-up-database/_static/image2.png)

테이블을 정의 하는 SQL 스크립트를 추가 하 여이 자습서에 필요한 테이블을 만들 수 있습니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 합니다.

![새 항목 추가](setting-up-database/_static/image3.png)

학생 라는 새 테이블을 추가 합니다.

![student 테이블 추가](setting-up-database/_static/image4.png)

테이블 파일에서 T-SQL 명령이 테이블을 만들려면 다음 코드로 바꿉니다.

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

디자인 창 코드를 사용 하 여 자동으로 동기화 하는 확인 합니다. 코드 또는 디자이너를 사용 하 여 작업할 수 있습니다.

![코드와 디자인 표시](setting-up-database/_static/image5.png)

다른 테이블을 추가 합니다. 이 이번 과정을 이름을 지정 하 고 다음 T-SQL 명령을 사용 합니다.

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

및 등록 라는 테이블을 만들려면 한 번 더 반복 합니다.

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

데이터베이스를 배포한 후 실행 되는 스크립트를 통해 데이터를 사용 하 여 데이터베이스를 채울 수 있습니다. 배포 후 스크립트를 프로젝트에 추가 합니다. 기본 이름을 사용할 수 있습니다.

![배포 후 스크립트를 추가 합니다.](setting-up-database/_static/image6.png)

배포 후 스크립트에 다음 T-SQL 코드를 추가 합니다. 이 스크립트에 추가 하기만 하면 데이터 데이터베이스 없는 일치 하는 레코드가 발견 되 면 합니다. 덮어쓰기 하거나 데이터베이스에 입력 데이터를 삭제 하지 않습니다.

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

데이터베이스 프로젝트를 배포할 때마다 배포 후 스크립트를 실행 하는 것이 반드시 합니다. 따라서이 스크립트를 작성 하는 경우 요구 사항을 신중 하 게 검토 해야 합니다. 경우에 따라 프로젝트를 배포할 때마다 알려진된 데이터 집합에서 다시 시작 하려고 할 수 있습니다. 다른 경우에 어떤 방식으로 기존 데이터를 변경 하려는 없습니다. 요구 사항에 따라, 배포 후 스크립트 또는 스크립트에 포함 해야 하는 새로운 필요 여부를 결정할 수 있습니다. 배포 후 스크립트를 사용 하 여 데이터베이스에 대 한 자세한 내용은 참조 하세요. [SQL Server 데이터베이스 프로젝트의 데이터를 포함 하 여](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)입니다.

이제 SQL 스크립트 파일을 4 하지만 실제 테이블이 없습니다. Localdb에 데이터베이스 프로젝트를 배포할 준비가 되었습니다. Visual Studio에서 빌드 및 데이터베이스 프로젝트를 배포 하려면 시작 단추 (또는 f5 키)를 클릭 합니다. 빌드 및 배포 성공 했는지 확인 하려면 출력 탭을 확인 합니다.

![출력 표시](setting-up-database/_static/image7.png)

새 데이터베이스 생성 되어 있는지를 보려면 **SQL Server 개체 탐색기** 올바른 로컬 데이터베이스 서버에 있는 프로젝트의 이름을 찾습니다 (이 예제의 **(localdb) \ProjectsV12**).

![새 데이터베이스를 표시 합니다.](setting-up-database/_static/image8.png)

테이블 데이터와 채워져 있는지를 확인 하려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 보기**합니다.

![테이블 데이터 표시](setting-up-database/_static/image9.png)

테이블 데이터의 편집 가능한 뷰에 표시 됩니다.

![테이블 데이터 결과 표시 합니다.](setting-up-database/_static/image10.png)

이제 데이터베이스가 설정 이며 데이터로 채워집니다. 다음 자습서에서는 데이터베이스에 대 한 웹 응용 프로그램을 만들게 됩니다.

> [!div class="step-by-step"]
> [다음](creating-the-web-application.md)
