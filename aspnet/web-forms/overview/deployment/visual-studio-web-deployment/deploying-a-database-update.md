---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 88652a33d5367241fec4d442e9deb15d88a096c9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817625"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다. 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

데이터베이스 변경 및 관련된 코드 변경 확인이 자습서에서는 Visual Studio에서 변경 내용을 테스트 한 다음 테스트, 스테이징 및 프로덕션 환경에 업데이트를 배포 합니다.

자습서에는 먼저에서 Code First 마이그레이션을 관리 하는 데이터베이스를 업데이트 하는 방법을 보여 줍니다 하 고 dbDacFx 공급자를 사용 하 여 데이터베이스를 업데이트 하는 방법을 보여줍니다 나중에 키를 누릅니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a>Code First 마이그레이션을 사용 하 여 데이터베이스 업데이트 배포

Birth date 열을 추가 하면이 섹션에서는 합니다 `Person` 기본 클래스에 대 한 합니다 `Student` 및 `Instructor` 엔터티. 새 열이 표시 되도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다. 마지막으로, 테스트, 스테이징 및 프로덕션에 변경 내용을 배포 합니다.

### <a name="add-a-column-to-a-table-in-the-application-database"></a>응용 프로그램 데이터베이스의 테이블에 열을 추가 합니다.

1. 에 *ContosoUniversity.DAL* 프로젝트를 열고 *Person.cs* 끝에 다음 속성을 추가 하 고는 `Person` 클래스 (없어야 닫는 중괄호 다음 두):

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    다음으로 업데이트 된 `Seed` 메서드는 새 열에 대 한 값을 제공 합니다. 오픈 *migrations\ configuration.cs* 시작 하는 코드 블록을 바꾸고 `var instructors = new List<Instructor>` 생년월일 정보를 포함 하는 다음 코드 블록을 사용 하 여:

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. 솔루션을 작성 하 고 엽니다는 **패키지 관리자 콘솔** 창입니다. ContosoUniversity.DAL으로 아직 선택 되어 있는지 확인 합니다 **기본 프로젝트**합니다.
3. 에 **패키지 관리자 콘솔** 창에서 **ContosoUniversity.DAL** 으로 **기본 프로젝트**, 다음 명령을 입력:

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    이 명령은 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMIgration` 클래스 및는 `Up` 메서드는 새 열을 만드는 코드를 볼 수 있습니다. 합니다 `Up` 변경 내용을 구현 하는 경우 메서드는 열을 만듭니다 및 `Down` 롤백하는 변경 하는 경우 메서드는 열을 삭제 합니다.

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. 솔루션을 빌드하고에서 다음 명령을 입력 합니다 **패키지 관리자 콘솔** 창 (ContosoUniversity.DAL 프로젝트 여전히 선택 되어 있는지 확인):

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    Entity Framework를 실행 합니다 `Up` 메서드를 실행 합니다 `Seed` 메서드.

### <a name="display-the-new-column-in-the-instructors-page"></a>강사 페이지에서 새 열을 표시 합니다.

1. ContosoUniversity 프로젝트에서 엽니다 *Instructors.aspx* 생년월일에 표시할 새 템플릿 필드를 추가 합니다. 고용 날짜 및 office 할당 용 간에 추가 합니다.

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    (코드 들여쓰기 동기화 되지 않는 경우를 누르면 CTRL + K와 CTRL-D 파일을 자동으로 서식을 다시 지정 하려면 다음 됩니다.)
2. 응용 프로그램을 실행 하 고 클릭 합니다 **강사** 링크 합니다.

    새에 참조 페이지를 로드 하는 경우 birth date 필드입니다.

    ![Birthdate 사용 하 여 강사 페이지](deploying-a-database-update/_static/image2.png)
3. 브라우저를 닫습니다.

### <a name="deploy-the-database-update"></a>데이터베이스 업데이트 배포

1. **솔루션 탐색기** ContosoUniversity 프로젝트를 선택 합니다.
2. 에 **한 번 클릭으로 웹 게시** 도구 모음에서 클릭 합니다 **테스트** 프로필을 게시 하 고 클릭 **웹 게시**합니다. (도구 모음을 사용 하지 않도록 설정 하는 경우에서 ContosoUniversity 프로젝트를 선택 **솔루션 탐색기**.)

    Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저의 홈 페이지가 열립니다.
3. 실행 합니다 **강사** 페이지 업데이트를 성공적으로 배포 되었는지 확인 합니다.

    응용 프로그램에이 페이지에 대 한 데이터베이스에 액세스 하려고 하는 경우 Code First 데이터베이스 스키마를 업데이트 하 고 실행 되는 `Seed` 메서드. 예상 된 참조 페이지를 표시 하는 경우 **Birth Date** 에 날짜 열입니다.
4. 에 **한 번 클릭으로 웹 게시** 도구 모음에서 클릭 합니다 **준비** 프로필을 게시 하 고 클릭 **웹 게시**.
5. 실행 된 **강사** 페이지 업데이트를 성공적으로 배포 되었는지 확인 하려면 준비 합니다.
6. 에 **한 번 클릭으로 웹 게시** 도구 모음에서 클릭 합니다 **프로덕션** 프로필을 게시 하 고 클릭 **웹 게시**합니다.
7. 실행 합니다 **강사** 업데이트가 성공적으로 배포 되었는지 확인 하려면 프로덕션 환경에서 페이지입니다.

    데이터베이스 변경 내용을 포함 하는 실제 프로덕션 응용 프로그램 업데이트에 대 한 일반적으로 수행 동안 응용 프로그램을 오프 라인 배포를 사용 하 여 *앱\_offline.htm*이전 자습서에서 보았듯이, 합니다.

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a>DbDacFx 공급자를 사용 하 여 데이터베이스 업데이트 배포

이 섹션에서는 추가 *주석을* 열을는 *사용자* 멤버 자격 데이터베이스에서 테이블을 만들고 표시 하 고 각 사용자에 대 한 주석을 편집할 수 있는 페이지. 다음 변경 내용을 테스트, 스테이징 및 프로덕션에 배포 합니다.

### <a name="add-a-column-to-a-table-in-the-membership-database"></a>멤버 자격 데이터베이스의 테이블에 열을 추가 합니다.

1. Visual Studio에서 엽니다 **SQL Server 개체 탐색기**합니다.
2. 확장 **(localdb) \v11.0**, 확장 **데이터베이스**를 확장 하 고 **aspnet ContosoUniversity** (되지 **aspnet-ContosoUniversity-Prod**) 펼쳐 **테이블**합니다.

    표시 되지 않는 경우 **(localdb) \v11.0** 아래를 **SQL Server** 노드를 마우스 오른쪽 단추로 클릭 합니다 **SQL Server** 노드를 클릭 **SQL Server 추가**합니다. 에 **서버에 연결** 대화 상자에 입력 합니다 *(localdb) \v11.0* 으로 **서버 이름**를 클릭 하 고 **연결**.

    표시 되지 않는 경우 **aspnet ContosoUniversity**프로젝트를 실행 하 고 사용 하 여 로그인 합니다 *관리자* 자격 증명 (암호가 *devpwd*), 고 새로 고쳐서는  **SQL Server 개체 탐색기** 창입니다.
3. 마우스 오른쪽 단추로 클릭 합니다 **사용자가** 테이블을 마우스 클릭 **뷰 디자이너**합니다.

    ![SSOX 뷰 디자이너](deploying-a-database-update/_static/image3.png)
4. 디자이너에서 추가 *주석을* 열 게 *nvarchar (128)* null을 허용 하 고 클릭 하 고 **업데이트**합니다.

    ![주석 열 추가](deploying-a-database-update/_static/image4.png)
5. 에 **데이터베이스 업데이트 미리 보기** 상자를 클릭 합니다 **데이터베이스 업데이트**합니다.

    ![데이터베이스 업데이트 미리 보기](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a>표시 하 고 새 열을 편집 페이지 만들기

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **계정** ContosoUniversity 프로젝트에서 폴더를 클릭 **추가**를 클릭 하 고 **새 항목** .
2. 새 **웹 폼 마스터 페이지를 사용 하 여** 하 고 이름을 *UserInfo.aspx*합니다. 기본값을 그대로 *Site.Master* 마스터 페이지 파일입니다.
3. 에 다음 태그를 복사 합니다 `MainContent` `Content` 요소 (3 중 마지막 `Content` 요소).

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. 마우스 오른쪽 단추로 클릭 합니다 *UserInfo.aspx* 페이지를 클릭 **브라우저에서 보기**합니다.
5. 로그인에 *관리자* 사용자 자격 증명 (암호가 *devpwd*) 페이지 올바르게 작동 하는지 확인 하려면 사용자에 게 몇 가지 설명을 추가 합니다.

    ![사용자 정보 페이지](deploying-a-database-update/_static/image6.png)
6. 브라우저를 닫습니다.

## <a name="deploy-the-database-update"></a>데이터베이스 업데이트 배포

DbDacFx 공급자를 사용 하 여 배포에 선택 해야 합니다 **데이터베이스 업데이트** 게시 프로필에 대 한 옵션입니다. 그러나 초기 배포에 대 한이 옵션을 사용할 때도 구성한 일부 추가 SQL 스크립트를 실행할: 프로필에서 계속 되 고 다시 실행 되지 않도록 해야 합니다.

1. 엽니다는 **웹 게시** ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 하 여 마법사 **게시**합니다.
2. 선택 된 **테스트** 프로필입니다.
3. 클릭 합니다 **설정을** 탭 합니다.
4. 아래 **DefaultConnection**를 선택 **데이터베이스 업데이트**합니다.
5. 초기 배포에 대해 실행 하도록 구성 된 추가 스크립트를 사용 하지 않도록 설정 합니다.

    1. 클릭 **데이터베이스 업데이트 구성**합니다.
    2. 에 **데이터베이스 업데이트 구성** 대화 상자에서 지우기 확인란 옆에 *Grant.sql* 하 고 *aspnet-데이터-dev.sql*합니다.
    3. **닫기**를 클릭합니다.
6. 클릭 합니다 **미리 보기** 탭 합니다.
7. 아래 **데이터베이스** 의 오른쪽 **DefaultConnection**를 클릭 합니다 **데이터베이스 미리 보기** 링크 합니다.

    ![데이터베이스 미리 보기](deploying-a-database-update/_static/image7.png)

    미리 보기 창에는 원본 데이터베이스의 스키마와 일치 하는 데이터베이스 스키마를 확인 하기 위해 대상 데이터베이스에서 실행 되는 스크립트를 보여 줍니다. 스크립트에 새 열을 추가 하는 ALTER TABLE 명령을 포함 합니다.
8. 닫기 합니다 **Database 미리 보기** 대화 상자 및 클릭 **게시**합니다.

    Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저의 홈 페이지가 열립니다.
9. 사용자 정보 페이지를 실행 (추가 *Account/UserInfo.aspx* 홈 페이지 url) 업데이트가 성공적으로 배포 되었는지 확인 합니다. 입력 하 여 로그인 해야 *admin* 하 고 *devpwd*합니다.

    테이블의 데이터는 기본적으로 배포 되지 않습니다 및 개발에서 추가한 주석을 찾을 수 없습니다 있도록 데이터 배포 스크립트를 실행 하려면 구성 되지 않았습니다. 이제에 변경 된 데이터베이스에 배포 하 여 페이지가 제대로 작동을 확인 하려면 스테이징에서 새 메모를 추가할 수 있습니다.
10. 스테이징 및 프로덕션에 배포 하려면 동일한 절차를 따릅니다.

    추가 스크립트를 사용 하지 않도록 설정 하려면 두는 것을 잊지 마세요. 테스트 프로필에 비해 유일한 차이점은 하나의 스크립트 준비에 사용 하지 않도록 설정 됩니다 하만 실행 하도록 구성 된 때문에 프로덕션 프로필 *aspnet-prod-data.sql*합니다.

    스테이징 및 프로덕션에 대 한 자격 증명은 관리자 및 prodpwd입니다.

    데이터베이스 변경 내용을 포함 하는 실제 프로덕션 응용 프로그램 업데이트에 대 한 일반적으로 수행 동안 응용 프로그램을 오프 라인 배포를 업로드 하 여 *앱\_offline.htm* 게시 하 고 삭제 하기 전에 나중에 볼 수 있듯이 [이전 자습서](deploying-a-code-update.md)합니다.

## <a name="summary"></a>요약

이제 dbDacFx 공급자와 Code First 마이그레이션을 사용 하 여 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 배포 했습니다.

![Birthdate 사용 하 여 강사 페이지](deploying-a-database-update/_static/image8.png)

![사용자 정보 페이지](deploying-a-database-update/_static/image9.png)

다음 자습서에서는 명령줄을 사용 하 여 배포를 실행 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deploying-a-code-update.md)
> [다음](command-line-deployment.md)
