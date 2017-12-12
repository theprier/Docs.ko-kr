---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 10da2b5013ae1348b69ea4f456d81bb4c4b73df6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

초기 배포 후 유지 관리 하 고 웹 사이트 개발 작업 계속 되 고 장기 하기 전에 업데이트를 배포 하려고 합니다. 이 자습서에서는 응용 프로그램 코드에 대 한 업데이트를 배포 하는 과정을 안내 합니다. 데이터베이스 변경; 구현 및이 자습서에서 배포 하는 업데이트를 초래 하지 않으므로 다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법에 대 한 차이점 표시 됩니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="make-a-code-change"></a>코드 변경

에 추가할 응용 프로그램에 대 한 업데이트의 간단한 예,으로 **강사** 선택한 강사 여 courses 목록이 페이지입니다.

실행 하는 경우는 **강사** 페이지 된다고을 알 수 있습니다 **선택** 표에서 링크 하는데 확인 이외의 행 배경 turn 회색 않으면 하지 않습니다.

![선택 된 instructors 페이지](deploying-a-code-update/_static/image1.png)

때 실행 되는 코드를 추가 하는 이제는 **선택** 링크를 클릭 하 고 선택한 강사 여 courses 목록이 표시 됩니다.

1. *Instructors.aspx*, 다음 태그를 추가 바로 뒤의 **ErrorMessageLabel** `Label` 제어:

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. 페이지를 실행 하 고 강사를 선택 합니다. 해당 강사 여 과정의 목록이 표시 됩니다.

    ![Courses 알게 된 instructors 페이지](deploying-a-code-update/_static/image2.png)
3. 브라우저를 닫습니다.

## <a name="deploy-the-code-update-to-the-test-environment"></a>코드 업데이트 테스트 환경에 배포

테스트, 스테이징 및 프로덕션에 배포 하 여 게시 프로필을 사용 하려면 먼저 데이터베이스 게시 옵션을 변경 해야 합니다. 더 이상 멤버 자격 데이터베이스에 대 한 grant 및 데이터 배포 스크립트를 실행 해야 합니다.

1. 열기는 **웹 게시** ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 마법사 **게시**합니다.
2. 클릭는 **테스트** 에서 프로 파일링 할는 **프로필** 드롭 다운 목록입니다.
3. 클릭는 **설정을** 탭 합니다.
4. **DefaultConnection** 에 **데이터베이스** 섹션을 선택 취소 된 **데이터베이스 업데이트** 확인란 합니다.
5. 클릭는 **프로필** 탭을 클릭 한 다음는 **준비** 에서 프로 파일링 할는 **프로필** 드롭 다운 목록입니다.
6. 변경 내용을 저장 하려면 묻는 하는 경우는 **테스트** 프로필을 클릭 하 여 **예**합니다.
7. 준비 프로필에 동일한 변경 내용을 확인 합니다.
8. 프로덕션 프로필에 동일한 변경 하는 프로세스를 반복 합니다.
9. 닫기는 **웹 게시** 마법사.

게시를 다시 실행 한 번의 클릭 하기만 하면 이제는 테스트 환경에 배포 합니다. 이 프로세스를 더 빠르게 수행 하려면 사용할 수 있습니다는 **한 번 클릭으로 웹 게시** 도구 모음입니다.

1. 에 **보기** 메뉴 선택 **도구 모음** 선택한 후 **한 번 클릭으로 웹 게시**합니다.

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. **솔루션 탐색기**, ContosoUniversity 프로젝트를 선택 합니다.
3. **한 번 클릭으로 웹 게시** 도구 모음에서 선택 된 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시** (왼쪽과 오른쪽을 가리키는 화살표가 있는 아이콘).

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 자동으로 열립니다.
5. 강사 페이지를 실행 하 고 강사 업데이트가 제대로 배포 되었는지 확인 하려면를 선택 합니다.

일반적인 회귀 테스트를 수행 (즉, 테스트 되는 새로운 변경 하지 않은 기존 기능이 해제 해야 하는 사이트의 나머지 부분)입니다. 하지만이 자습서에 대 한 해당 단계를 건너뜁니다 고 업데이트를 스테이징 및 프로덕션 배포를 진행 합니다.

다시 배포 하면 어떤 파일이 변경 되어 자동으로 결정 웹 배포 및 복사본만 서버에 파일을 변경 합니다. 기본적으로 웹 배포를 사용 하 여 마지막 변경 날짜 파일에 변경 된 것을 확인 합니다. 소스 제어 시스템 파일 내용을 변경 하지 않는 경우에 날짜 파일을 변경 합니다. 이 경우 다음 파일 체크섬 변경 된 파일을 확인 하는 데 웹 배포를 구성 하는 것이 좋습니다. 자세한 내용은 참조 [이유 수행 내 파일의 모든 가져오기 재배포 변경 하지 않은 있지만?](https://msdn.microsoft.com/en-us/library/ee942158.aspx#use_checksum) ASP.NET 배포 FAQ에 있습니다.

## <a name="take-the-application-offline-during-deployment"></a>배포 하는 동안 있는 오프 라인 응용 프로그램

배포 하는 변경에는 이제 단일 페이지에 대 한 간단한 변경이입니다. 하지만 더 큰 변경에 배포 하는 경우에 따라 또는 코드와 데이터베이스 변경 내용을 배포 하 고 배포 완료 되기 전에 페이지 요청 하는 경우 사이트가 올바르게 작동할 수 있습니다. 사용자가 배포 진행 중인 동안 사이트에 액세스 하지 못하도록 하려면 사용할 수 있습니다는 *앱\_offline.htm* 파일입니다. 라는 파일을 만들었을 때 *앱\_offline.htm* 응용 프로그램의 루트 폴더에 IIS에서는 응용 프로그램을 실행 하는 대신 해당 파일입니다. 배포 하는 동안 액세스를 방지 하려면 삽입 되므로 *앱\_offline.htm* 루트 폴더에 배포 프로세스를 실행 한 다음 제거 *앱\_offline.htm* 후 성공 배포 합니다.

웹 배포를 자동으로 추가 기본값을 구성할 수 있습니다 *앱\_offline.htm* 배포 시작 시 서버에서 파일을 완료 되었을 때이 제거 합니다. 수행 해야 하면 모든 작업을 수행 하는 게시 프로 파일 (.pubxml) 파일에 다음 XML 요소를 추가 합니다.

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

이 자습서에 대 한 만들고 사용자 지정을 사용 하는 방법을 알아봅니다 *앱\_offline.htm* 파일입니다.

사용 하 여 *앱\_offline.htm* 준비 사이트에서 필요 하지 않습니다, 준비 사이트에 액세스 하는 사용자가 없기 때문에 있습니다. 하지만 프로덕션 환경에서 배포 하려는 방법을 모두 테스트를 준비를 사용 하는 것이 좋습니다.

### <a name="create-appofflinehtm"></a>앱 만들기\_offline.htm

1. **솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, 클릭 하 고 **새 항목**합니다.
2. 만들기는 **HTML 페이지** 라는 *앱\_offline.htm* (최종 "l"의 삭제는 *.html* 기본적으로 Visual Studio에서 확장명입니다).
3. 템플릿 태그를 다음 태그로 바꿉니다.

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. 파일을 저장한 후 닫습니다.

### <a name="copy-appofflinehtm-to-the-root-folder-of-the-web-site"></a>복사 앱\_offline.htm 웹 사이트의 루트 폴더에

모든 FTP 도구를 사용 하 여 웹 사이트에 파일을 복사할 수 있습니다. [FileZilla](http://filezilla-project.org/) 은 인기 있는 FTP 도구 이며 스크린 샷에 표시 됩니다.

다음 세 가지 FTP 도구를 사용 하려면 필요: FTP URL, 사용자 이름 및 암호.

URL은 Azure 관리 포털에서 웹 사이트의 대시보드 페이지에 표시 되 고에서 사용자 이름 및 FTP에 대 한 암호를 확인할 수 있습니다는 *.publishsettings* 이전에 다운로드 한 파일입니다. 다음 단계에는 이러한 값을 가져오는 방법을 보여 줍니다.

1. Azure 관리 포털에서 클릭 **웹사이트** 탭 한 다음 스테이징 웹 사이트를 클릭 합니다.
2. 에 **대시보드** 페이지에서 FTP 호스트에 이름을 찾으려면 아래로 스크롤은 **빠른 보기** 섹션.

    ![FTP 호스트 이름](deploying-a-code-update/_static/image5.png)
3. 준비를 열고 *.publishsettings* 메모장 이나 다른 텍스트 편집기에서 파일입니다.
4. 찾기의 `publishProfile` FTP 프로필에 대 한 요소입니다.
5. 복사는 `userName` 및 `userPWD` 값입니다.

    ![FTP 자격 증명](deploying-a-code-update/_static/image6.png)
6. FTP 도구 및 FTP URL에 로그온을 엽니다.
7. 복사 *앱\_offline.htm* 에 솔루션 폴더에서는 */사이트/wwwroot* 준비 사이트에서 폴더입니다.

    ![App_offline 복사](deploying-a-code-update/_static/image7.png)
8. 준비 사이트의 URL로 이동 합니다. 참조 하는 *앱\_offline.htm* 페이지 홈 페이지 대신 표시 됩니다.

    ![브라우저 창에서 app_offline.htm](deploying-a-code-update/_static/image8.png)

준비를 배포할 준비가 됩니다.

## <a name="deploy-the-code-update-to-staging-and-production"></a>코드 업데이트 스테이징 및 프로덕션에 배포

1. **한 번 클릭으로 웹 게시** 도구 모음에서 선택 된 **준비** 게시 프로필을 클릭 한 다음 **웹 게시**합니다.

    Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 브라우저 사이트의 홈 페이지를 엽니다. *앱\_offline.htm* 파일이 표시 됩니다. 성공적인 배포를 확인 하려면를 테스트 하려면 먼저 제거 해야는 *앱\_offline.htm* 파일입니다.
2. FTP 도구의 반환 및 delete **앱\_offline.htm** 준비 사이트에서.
3. 브라우저에서 준비 사이트에서 강사 페이지를 열고 강사 업데이트가 제대로 배포 되었는지 확인 하려면 선택 합니다.
4. 준비에 대해 수행한 것 처럼 프로덕션에 대해 동일한 절차를 따릅니다.

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>변경 내용을 검토 하 고 특정 파일 배포

또한 visual Studio 2012는 개별 파일을 배포 하는 기능을 제공 합니다. 선택한 파일에 대 한 배포 된 버전과 로컬 버전 간의 차이점을 볼 대상 환경으로 파일을 배포 하거나 로컬 프로젝트에 대상 환경에서 파일을 복사할 수 있습니다. 이 자습서의이 섹션에서 이러한 기능을 사용 하는 방법을 볼 수 있습니다.

### <a name="make-a-change-to-deploy"></a>배포에 대 한 변경 확인

1. 열기 *Content/Site.css*, 했는데에 대 한 블록의 `body` 태그입니다.
2. 에 대 한 값을 변경 `background-color` 에서 `#fff` 를 `darkblue`합니다.

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>게시 미리 보기 창에서 변경 된 내용을 확인합니다

사용 하는 경우는 **웹 게시** 마법사 프로젝트를 게시 하는 어떤 변경 하려고에서 파일을 두 번 클릭 하 여 게시를 볼 수 있습니다는 **미리 보기** 창.

1. ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.
2. **프로필** 드롭 다운 목록에서 **테스트** 게시 프로필.
3. 클릭 **미리 보기**, 클릭 하 고 **미리 보기 시작**합니다.
4. 에 **미리 보기** 창에서 두 번 클릭 **Site.css**합니다.

    ![Site.css를 두 번 클릭](deploying-a-code-update/_static/image9.png)

    **변경 내용 미리 보기가** 대화 상자에 배포 될 변경 내용 미리 보기에 표시 합니다.

    ![Site.css에 변경 내용 미리 보기](deploying-a-code-update/_static/image10.png)

    두 번 클릭는 *Web.config* 파일인은 **변경 내용 미리 보기** 대화 상자 구성 변환 빌드 결과 보여 줍니다 및 게시 프로필 변환 합니다. 이 시점에서 프로 비전 하지 않은 원인을 *Web.config* 변경 되어 변경 내용을 확인 하려는 서버에는 파일입니다. 그러나는 **변경 내용 미리 보기가** 창 두 가지 변경 내용이 올바르게 표시 합니다. 두 개의 XML 요소를 제거할 것 같습니다. 이러한 요소를 선택 하면 게시 프로세스에 의해 추가 **실행 Code First 마이그레이션이 응용 프로그램 시작 시** 는 Code First 컨텍스트 클래스에 대 한 합니다. 게시 프로세스가 것 같습니다. 제거 되지 것입니다 되지만 제거 되 고 있으므로 해당 요소를 추가 하기 전에 비교를 수행 합니다. 이 오류는 이후 릴리스에서 수정 됩니다.
5. **닫기**를 클릭합니다.
6. **게시**를 클릭합니다.
7. 브라우저를 열면 테스트 사이트의 홈 페이지에 CTRL + f 5를 눌러 CSS 변경의 결과 확인 하기 위해 하드 새로 고쳐집니다.

    ![CSS 변경 결과](deploying-a-code-update/_static/image11.png)
8. 브라우저를 닫습니다.

### <a name="publish-specific-files-from-solution-explorer"></a>솔루션 탐색기에서 특정 파일 게시

파란색 배경을 고 원래 색으로 되돌리려면 싶으면 하지 않는 가정 합니다. 이 섹션에서는 특정 파일에서 직접 게시 하 여 원래 설정을 복원 합니다 **솔루션 탐색기**합니다.

1. 열기 *Content/Site.css* 및 복원는 `background-color` 설정을 `#fff`합니다.
2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Content/Site.css* 파일입니다.

    상황에 맞는 메뉴 옵션 3 개의 게시를 보여 줍니다.

    ![솔루션 탐색기에서 옵션 게시](deploying-a-code-update/_static/image12.png)
3. 클릭 **Site.css 변경 내용 미리 보기**합니다.

    대상 환경에 로컬 파일의 버전 사이의 차이 표시 하려면 창이 열립니다.

    ![Diff-콘텐츠/Site.css](deploying-a-code-update/_static/image13.png)
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **Site.css** 다시 클릭 하 고 **게시 Site.css**합니다.

    **웹 게시 동작** 파일 게시 된 창에 표시 합니다.

    ![웹 게시 작업 창](deploying-a-code-update/_static/image14.png)
5. 브라우저를 열고는 `http://localhost/contosouniversity` URL을 누르고 CTRL + f 5를 하드 되지만 새로 고쳐지지 CSS의 효과 변경 합니다.

    ![기본 CSS 사용한 홈 페이지](deploying-a-code-update/_static/image15.png)
6. 브라우저를 닫습니다.

## <a name="summary"></a>요약

이제 데이터베이스 변경 내용을 포함 하지 않는 응용 프로그램 업데이트를 배포 하는 여러 가지 방법을 살펴보았습니다 하 고 변경 내용을 업데이트할지 무엇 인지 확인 기대를 미리 보는 방법을 살펴보았습니다. 이제 강사 페이지에는 **Courses 알게** 섹션.

![Courses 알게 된 instructors 페이지](deploying-a-code-update/_static/image16.png)

다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다: 데이터베이스를 강사 페이지를 birthdate 필드를 추가 합니다.

>[!div class="step-by-step"]
[이전](deploying-to-production.md)
[다음](deploying-a-database-update.md)
