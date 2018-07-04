---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 배포 데이터베이스 업데이트-12 9 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: e94281e36192c91a04392735af318bbc517b0521
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382461"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 배포 데이터베이스 업데이트-12 9
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

데이터베이스 변경 및 관련된 코드 변경 확인이 자습서에서는 Visual Studio에서 변경 내용을 테스트 한 다음 테스트 및 프로덕션 환경에 업데이트를 배포 합니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="adding-a-new-column-to-a-table"></a>테이블에 새 열 추가

Birth date 열을 추가 하면이 섹션에서는 합니다 `Person` 기본 클래스에 대 한 합니다 `Student` 및 `Instructor` 엔터티. 새 열이 표시 되도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다.

에 *ContosoUniversity.DAL* 프로젝트를 열고 *Person.cs* 끝에 다음 속성을 추가 하 고는 `Person` 클래스 (없어야 닫는 중괄호 다음 두):

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

그런 다음 새 열의 값을 제공 하도록 시드 메서드를 업데이트 합니다. 오픈 *migrations\ configuration.cs* 시작 하는 코드 블록을 바꾸고 `var instructors = new List<Instructor>` 생년월일 정보를 포함 하는 다음 코드 블록을 사용 하 여:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

ContosoUniversity 프로젝트에서 엽니다 *Instructors.aspx* 생년월일에 표시할 새 템플릿 필드를 추가 합니다. 고용 날짜 및 office 할당 용 간에 추가 합니다.

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

(코드 들여쓰기 동기화 되지 않는 경우를 누르면 CTRL + K와 CTRL-D 파일을 자동으로 서식을 다시 지정 하려면 다음 됩니다.)

솔루션을 작성 하 고 엽니다는 **패키지 관리자 콘솔** 창입니다. ContosoUniversity.DAL으로 아직 선택 되어 있는지 확인 합니다 **기본 프로젝트**합니다.

에 **패키지 관리자 콘솔** 창에서 **ContosoUniversity.DAL** 으로 **기본 프로젝트**, 다음 명령을 입력:

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

이 명령은 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMIgration` 클래스 및는 `Up` 메서드는 새 열을 만드는 코드를 볼 수 있습니다.

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

솔루션을 빌드하고에서 다음 명령을 입력 합니다 **패키지 관리자 콘솔** 창 (ContosoUniversity.DAL 프로젝트 여전히 선택 되어 있는지 확인):

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

명령이 완료 되 면 응용 프로그램을 실행 하 고 강사 페이지를 선택 합니다. 새에 참조 페이지를 로드 하는 경우 birth date 필드입니다.

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>데이터베이스 업데이트 테스트 환경에 배포

**솔루션 탐색기** ContosoUniversity 프로젝트를 선택 합니다.

에 **한 번 클릭으로 웹 게시** 도구 모음을 선택 합니다 **테스트** 프로필을 게시 하 고 클릭 **웹 게시**합니다. (도구 모음을 사용 하지 않도록 설정 하는 경우에서 ContosoUniversity 프로젝트를 선택 **솔루션 탐색기**.)

Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저의 홈 페이지가 열립니다. 강사 페이지 업데이트를 성공적으로 배포 되었는지 확인 하려면을 실행 합니다. 응용 프로그램에이 페이지에 대 한 데이터베이스에 액세스 하려고 하는 경우 Code First 데이터베이스 스키마를 업데이트 하 고 실행 되는 `Seed` 메서드. 예상 된 참조 페이지를 표시 하는 경우 **Birth Date** 에 날짜 열입니다.

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>데이터베이스 업데이트를 프로덕션 환경에 배포

이제 프로덕션 환경에 배포할 수 있습니다. 유일한 차이점은 사용할 수 있습니다 *앱\_offline.htm* 사용자가 사이트에 액세스 하 고 있으므로 변경 내용을 배포 하는 동안 데이터베이스를 업데이트 하지 못하도록 합니다. 프로덕션 배포를 위한 다음 단계를 수행 합니다.

- 업로드 합니다 *앱\_offline.htm* 프로덕션 사이트에는 파일입니다.
- Visual Studio에서의 프로덕션 프로필을 선택 합니다 **한 번 클릭으로 웹 게시** 도구 모음 및 클릭 **웹 게시**합니다.
- 삭제 된 *앱\_offline.htm* 프로덕션 사이트에서 파일입니다.

> [!NOTE]
> 응용 프로그램은 프로덕션 환경에서 사용 되는 동안 백업 계획을 구현 해야 합니다. 즉, 사용자는 주기적으로 복사 하는 합니다 *학교 Prod.sdf* 하 고 *aspnet Prod.sdf* 안전한 저장소 위치에 파일에서 프로덕션 사이트 및 등의 여러 세대를 유지 해야 백업 합니다. 데이터베이스를 업데이트할 때 변경 직전의 백업 복사본을 만들어야 합니다. 그런 다음 실수를 프로덕션에 배포한 후까지 검색 하지 해야 손상 하기 전의 상태로 데이터베이스를 복구할 수 있습니다.


Visual Studio가 브라우저에서 홈 페이지 URL을 열면 합니다 *앱\_offline.htm* 페이지가 표시 됩니다. 삭제 한 후 합니다 *앱\_offline.htm* 홈 페이지에 업데이트를 성공적으로 배포 되었는지 확인 하려면 다시 찾아보면 파일입니다.

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

이제 테스트와 생산에 모두에 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 배포 했습니다. 다음 자습서에서는 SQL Server Express 및 SQL Server에서 SQL Server Compact 데이터베이스를 마이그레이션하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [다음](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
