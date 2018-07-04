---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3649f0250e830b76c42d832e51038c2c52ed4561
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368216"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다. 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

초기 배포 후 유지 관리 하 고 웹 사이트 개발의 작업 계속 되 고 오래 전에 하려는 업데이트를 배포 합니다. 이 자습서에서는 응용 프로그램 코드에 대 한 업데이트를 배포 하는 과정을 안내 합니다. 구현 하 고이 자습서에서 배포 된 업데이트는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 방법에 대 한 차이점 표시 됩니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="make-a-code-change"></a>코드 변경

간단한 예로 업데이트 응용 프로그램을 추가 합니다 **강사** 선택한 강사가가 르 친 과정 목록을 페이지입니다.

실행 하는 경우는 **강사** 페이지를 보면 있는지 **선택** 표의 링크 하지 확인 이외의 행 배경색 설정 회색 있지만.

![선택 된 강사 페이지](deploying-a-code-update/_static/image1.png)

이제 때 실행 되는 코드를 추가 합니다 **선택** 링크를 클릭 하 고 선택한 강사가가 르 친 과정의 목록을 표시 합니다.

1. *Instructors.aspx*, 다음 태그를 추가 직후 합니다 **ErrorMessageLabel** `Label` 제어:

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. 페이지를 실행 하 고 강사를 선택 합니다. 해당 강사가가 르 친 과정의 목록이 표시 됩니다.

    ![르 친 과정을 사용 하 여 강사 페이지](deploying-a-code-update/_static/image2.png)
3. 브라우저를 닫습니다.

## <a name="deploy-the-code-update-to-the-test-environment"></a>테스트 환경에 코드 업데이트를 배포 합니다.

게시 프로필을 사용 하 여 테스트, 스테이징 및 프로덕션에 배포할 수 있습니다, 전에 데이터베이스 게시 옵션을 변경 해야 합니다. 멤버 자격 데이터베이스에 대 한 권한 부여 및 데이터 배포 스크립트를 실행할 필요가 없습니다.

1. 엽니다는 **웹 게시** ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 하 여 마법사 **게시**합니다.
2. 클릭 합니다 **테스트** 에서 프로 파일링 합니다 **프로필** 드롭 다운 목록.
3. 클릭 합니다 **설정을** 탭 합니다.
4. 아래 **DefaultConnection** 에 **데이터베이스** 섹션의 선택을 취소는 **데이터베이스 업데이트** 확인란 합니다.
5. 클릭는 **프로필** 탭을 클릭 합니다 **스테이징** 에서 프로 파일링를 **프로필** 드롭 다운 목록.
6. 변경 내용을 저장 하려는 경우 묻는 하는 경우는 **테스트** 프로 파일링, 클릭 **예**합니다.
7. 스테이징 프로필에 동일한 변경 내용을 확인 합니다.
8. 프로덕션 프로필에서 동일 하 게 변경 하는 프로세스를 반복 합니다.
9. 닫기 합니다 **웹 게시** 마법사.

테스트 환경에 배포 하는 것은 이제 실행 한 번의 클릭 하기만 하면 다시 게시 합니다. 이 프로세스를 더 빠르게 하려면 사용할 수 있습니다 합니다 **한 번 클릭으로 웹 게시** 도구 모음입니다.

1. 에 **뷰** 메뉴 선택 **도구 모음** 선택한 후 **한 번 클릭으로 웹 게시**합니다.

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. **솔루션 탐색기**, ContosoUniversity 프로젝트를 선택 합니다.
3. **한 번 클릭으로 웹 게시** 도구 모음을 선택 합니다 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시** (왼쪽과 오른쪽을 가리키는 화살표가 있는 아이콘).

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 자동으로 열립니다.
5. 강사 페이지를 실행 하 고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.

일반적으로 회귀 테스트를 수행 (즉, 테스트할 새로운 변경 사항을 기존 기능이 손상 하지 않는지 확인 하는 사이트의 나머지 부분). 하지만이 자습서에서는 단계를 건너뛸 하 스테이징 및 프로덕션에 업데이트 배포를 진행 합니다.

다시 배포 하면 웹 배포를 자동으로 결정 변경 된 파일 및 복사본에만 서버에 파일을 변경 합니다. 기본적으로 웹 배포를 사용 하 여 마지막 변경 날짜 파일에는 변경 된을 확인 합니다. 일부 소스 제어 시스템 파일 내용을 변경 하지 않은 경우 날짜에도 파일을 변경 합니다. 이 경우 다음 파일 체크섬을 사용 하 여 변경 된 파일을 확인 하려면 웹 배포를 구성 하는 것이 좋습니다. 자세한 내용은 [왜 수행 내 파일을 모두 다시 배포 해도 변경 하지 않지만?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) ASP.NET 배포 faq에서.

## <a name="take-the-application-offline-during-deployment"></a>동안 응용 프로그램을 오프 라인 배포를 수행 합니다.

배포 하는 변경에는 이제 단일 페이지에 대 한 간단한 변경이입니다. 하지만 대규모 변경 사항을 배포 하는 경우에 따라 또는 코드와 데이터베이스 변경 내용을 배포 및 배포 완료 되기 전에 사용자 페이지를 요청 하는 경우 사이트 올바르게 작동할 수 있습니다. 사용자가 배포가 진행에서 되는 동안 사이트에 액세스 하지 못하도록 하려면 사용할 수는 *앱\_offline.htm* 파일입니다. 라는 파일을 적용할 시기 *앱\_offline.htm* 응용 프로그램의 루트 폴더에서 IIS 자동으로 파일을 표시는 응용 프로그램을 실행 하는 대신 합니다. 배포 하는 동안 액세스를 방지 하려면 배치 되므로 *앱\_offline.htm* 루트 폴더에서 배포 프로세스를 실행 한 다음 제거 *앱\_offline.htm* 후 성공 배포 합니다.

기본값을 자동으로 적용할 웹 배포를 구성할 수 있습니다 *앱\_offline.htm* 배포 시작 시 서버에서 파일 및 완료 되 면 제거 합니다. 이렇게 모든 작업을 수행 하 게시 프로필 (.pubxml) 파일에 다음 XML 요소를 추가할 것입니다.

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

이 자습서에 대 한 표시를 만들고 사용자 지정을 사용 하는 방법 *앱\_offline.htm* 파일입니다.

사용 하 여 *앱\_offline.htm* 스테이징 사이트에서 필요 하지 않습니다, 스테이징 사이트에 액세스 하는 사용자가 없기 때문입니다. 하지만 모든 프로덕션 환경에서 배포 하려는 방법을 테스트할 준비를 사용 하는 것이 좋습니다.

### <a name="create-appofflinehtm"></a>앱 만들기\_offline.htm

1. **솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**를 클릭 하 고 **새 항목**합니다.
2. 만들기는 **HTML 페이지** 라는 *앱\_offline.htm* (에서 마지막 "l"을 삭제 합니다 *.html* 기본적으로 Visual Studio에서 확장명입니다).
3. 템플릿 태그를 다음 태그로 바꿉니다.

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. 파일을 저장한 후 닫습니다.

### <a name="copy-appofflinehtm-to-the-root-folder-of-the-web-site"></a>앱 복사\_offline.htm 웹 사이트의 루트 폴더에

웹 사이트에 파일을 복사할 모든 FTP 도구를 사용할 수 있습니다. [FileZilla](http://filezilla-project.org/) 인기 있는 FTP 도구 이며 스크린 샷에 표시 됩니다.

FTP 도구를 사용 하려면 다음 세 가지: FTP URL, 사용자 이름 및 암호입니다.

URL은 Azure 관리 포털에서 웹 사이트의 대시보드 페이지에 표시 되 고에서 사용자 이름 및 FTP에 대 한 암호를 찾을 수 있습니다 합니다 *.publishsettings* 앞에서 다운로드 한 파일입니다. 다음 단계에는 이러한 값을 가져오는 방법을 보여 줍니다.

1. Azure 관리 포털에서 클릭 **웹 사이트** 탭 한 다음 스테이징 웹 사이트를 클릭 합니다.
2. 에 **대시보드** 페이지에서 FTP 호스트 이름 찾기까지 아래로 스크롤합니다 합니다 **간략 상태** 섹션입니다.

    ![FTP 호스트 이름](deploying-a-code-update/_static/image5.png)
3. 준비를 엽니다 *.publishsettings* 메모장 이나 다른 텍스트 편집기에서 파일입니다.
4. 찾기는 `publishProfile` FTP 프로필에 대 한 요소입니다.
5. 복사 합니다 `userName` 고 `userPWD` 값입니다.

    ![FTP 자격 증명](deploying-a-code-update/_static/image6.png)
6. FTP 도구 열고 FTP URL에 로그온 합니다.
7. 복사본 *앱\_offline.htm* 솔루션 폴더에서의 */site/wwwroot* 스테이징 사이트의 폴더입니다.

    ![App_offline 복사](deploying-a-code-update/_static/image7.png)
8. 스테이징 사이트의 URL로 이동 합니다. 표시 된 *앱\_offline.htm* 페이지 홈 페이지가 대신 표시 됩니다.

    ![브라우저 창에서 app_offline.htm](deploying-a-code-update/_static/image8.png)

스테이징에 배포 준비가 되었습니다.

## <a name="deploy-the-code-update-to-staging-and-production"></a>스테이징 및 프로덕션에 코드 업데이트를 배포 합니다.

1. 에 **한 번 클릭으로 웹 게시** 도구 모음에서 선택 합니다 **스테이징** 게시 프로필을 클릭 한 다음 **웹 게시**.

    Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지로 브라우저를 엽니다. 합니다 *앱\_offline.htm* 파일이 표시 됩니다. 를 성공적으로 배포를 확인 하려면 테스트 전에 제거 해야 합니다 *앱\_offline.htm* 파일입니다.
2. FTP 도구를 사용 하 여 돌아가서 삭제할 **앱\_offline.htm** 스테이징 사이트에서.
3. 브라우저에서 스테이징 사이트에서 강사 페이지를 열고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.
4. 스테이징에 대해 수행한 것 처럼 프로덕션 환경에 동일한 절차를 따릅니다.

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>변경 내용을 검토 하 고 특정 파일 배포

또한 visual Studio 2012는 개별 파일을 배포 하는 기능을 제공 합니다. 선택한 파일에 대 한 배포 된 버전과 로컬 버전 간의 차이점을 볼, 대상 환경으로 파일을 배포 또는 대상 환경에서 로컬 프로젝트 파일을 복사할 수 있습니다. 이 자습서의이 섹션에서는 이러한 기능을 사용 하는 방법을 볼 수 있습니다.

### <a name="make-a-change-to-deploy"></a>배포 변경

1. 오픈 *Content/Site.css*에 대 한 블록을 찾아서는 `body` 태그입니다.
2. 값을 변경 `background-color` 에서 `#fff` 에 `darkblue`입니다.

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>게시 미리 보기 창에서 변경 내용을 보고합니다

사용 하는 경우는 **웹 게시** 프로젝트를 게시 하려면 마법사에서 파일을 두 번 클릭 하 여 게시할 변경은 상황을 볼 수 있습니다 합니다 **미리 보기** 창입니다.

1. ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.
2. 합니다 **프로필** 드롭 다운 목록에서 선택 합니다 **테스트** 게시 프로필.
3. 클릭 **미리 보기**를 클릭 하 고 **미리 보기 시작**합니다.
4. 에 **미리 보기** 창에 두 번 클릭 **Site.css**합니다.

    ![Site.css를 두 번 클릭](deploying-a-code-update/_static/image9.png)

    합니다 **변경 내용 미리 보기** 대화 배포 되는 변경 내용 미리 보기를 표시 합니다.

    ![Site.css에 변경 내용 미리 보기](deploying-a-code-update/_static/image10.png)

    두 번 클릭 합니다 *Web.config* 파일을를 **변경 내용 미리 보기** 대화 상자 구성 변환 빌드의 결과 보여 줍니다 및 게시 프로필 변환 합니다. 이 시점에서 수행 하지 않은 원인을 합니다 *Web.config* 변경 내용이 예상한 수 있으므로 서버에는 파일입니다. 그러나 합니다 **변경 내용 미리 보기** 창 두 가지 변경 사항을 올바르게 표시 합니다. 두 개의 XML 요소를 제거할 것 같습니다. 이러한 요소는 선택 하는 경우 게시 프로세스에 의해 추가 됩니다 **Execute Code First Migrations 응용 프로그램 시작 시** Code First 컨텍스트 클래스에 대 한 합니다. 비교는 제거 되지 것입니다 하지만 제거 되는 것 처럼 보입니다 하므로 게시 프로세스가 해당 요소를 추가 하기 전에 수행 됩니다. 이 오류는 향후 릴리스에서 수정 될 예정입니다.
5. **닫기**를 클릭합니다.
6. **게시**를 클릭합니다.
7. 테스트 사이트의 홈 페이지로 브라우저가 열리면 CTRL + F5 키를 눌러 CSS 변경의 결과 확인 하기 위해 하드 새로 고쳐집니다.

    ![CSS 변경의 효과](deploying-a-code-update/_static/image11.png)
8. 브라우저를 닫습니다.

### <a name="publish-specific-files-from-solution-explorer"></a>솔루션 탐색기에서 특정 파일 게시

배경이 파란색 하 고 싶으면 원래 색으로 되돌릴 수 없는 경우 이 섹션에서 직접 특정 파일을 게시 하 여 원래 설정을 복원 하겠습니다 **솔루션 탐색기**합니다.

1. 열기 *Content/Site.css* 및 복원 합니다 `background-color` 설정을 `#fff`합니다.
2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *Content/Site.css* 파일입니다.

    상황에 맞는 메뉴 옵션 세 개의 게시를 보여 줍니다.

    ![솔루션 탐색기에서 옵션 게시](deploying-a-code-update/_static/image12.png)
3. 클릭 **Site.css에 변경 내용 미리 보기**합니다.

    대상 환경에 로컬 파일 및 해당 버전 간의 차이점을 표시 하는 창이 열립니다.

    ![Diff-콘텐츠/Site.css](deploying-a-code-update/_static/image13.png)
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **Site.css** 다시 누릅니다 **Site.css 게시**합니다.

    합니다 **웹 게시 활동** 파일 게시 된 창에 표시 됩니다.

    ![웹 게시 활동 창](deploying-a-code-update/_static/image14.png)
5. 브라우저를 열어는 `http://localhost/contosouniversity` URL을 누릅니다. 하드 시킬 ctrl+f5 CSS의 변경 결과 보려면 새로 고침 합니다.

    ![일반 CSS 사용 하 여 홈 페이지](deploying-a-code-update/_static/image15.png)
6. 브라우저를 닫습니다.

## <a name="summary"></a>요약

데이터베이스 변경 내용을 포함 하지 않는 응용 프로그램 업데이트를 배포 하는 여러 방법을 확인 하 셨 고 업데이트될지 무엇 인지 확인 예상과 변경 내용 미리 보기 하는 방법을 살펴보았습니다. 강사 페이지에는 **강좌를 수업** 섹션입니다.

![르 친 과정을 사용 하 여 강사 페이지](deploying-a-code-update/_static/image16.png)

다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다: 강사 페이지를 데이터베이스로 생년월일 필드를 추가 합니다.

> [!div class="step-by-step"]
> [이전](deploying-to-production.md)
> [다음](deploying-a-database-update.md)
