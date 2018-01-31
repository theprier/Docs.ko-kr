---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: "SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트-11/12 배포 | Microsoft Docs"
author: tdykstra
description: "이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: aeec69c7373a111d30e8f32a374a9f02fb4c080a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트-12 11를 배포 합니다.
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. 웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다. 계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능 보여주며 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. Windows Azure 웹 사이트를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에서는 전체 SQL Server 데이터베이스를 데이터베이스 업데이트를 배포 하는 방법을 보여 줍니다. 프로세스는 거의 동일 수행한 작업에서 SQL Server Compact에 대 한 데이터베이스를 업데이트 하는 모든 작업을 수행 하는 Code First 마이그레이션을, 때문에 [데이터베이스 업데이트를 배포](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) 자습서입니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="adding-a-new-column-to-a-table"></a>테이블에 새 열 추가

자습서의이 섹션의 변경 하는 데이터베이스와 다음 테스트 및 프로덕션 환경에 배포 하기 위해에서 Visual Studio에서 테스트, 해당 코드 변경 내용을 지정 합니다. 변경 내용을 추가 해야는 `OfficeHours` 열을는 `Instructor` 엔터티 및 새로운 정보를 표시는 **강사** 웹 페이지입니다.

ContosoUniversity.DAL 프로젝트를 열고 *Instructor.cs* 은 다음 속성을 추가 하 고는 `HireDate` 및 `Courses` 속성:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

테스트 데이터로 새 열을 시드합니다 이니셜라이저 클래스를 업데이트 합니다. 열기 *Migrations\Configuration.cs* 및 시작 하는 코드 블록을 바꾸기 `var instructors = new List<Instructor>` 새 열을 포함 하는 다음 코드 블록:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

ContosoUniversity 프로젝트를 열고 *Instructors.aspx* 닫기 바로 전에 업무 시간에 대 한 새 서식 파일 필드를 추가 하 고 `</Columns>` 첫 번째 범위에서 태그 `GridView` 제어:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

솔루션을 빌드합니다.

열기는 **패키지 관리자 콘솔** 창과로 선택 ContosoUniversity.DAL는 **기본 프로젝트**합니다.

다음 명령을 입력 합니다.

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

응용 프로그램을 실행 하 고 선택 된 **강사** 페이지. 페이지 약간 Entity Framework는 데이터베이스를 만들고 다시 테스트 데이터로 초기값을 설정 하기 때문에 로드 하는 데 평소 보다 오래 걸립니다.

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>테스트 환경에 데이터베이스 업데이트 배포

Code First 마이그레이션을 사용 하는 경우 SQL Server로 데이터베이스 변경 내용을 배포 하기 위한 메서드는 SQL Server Compact의 경우와 동일 합니다. 그러나 변경 하 고 테스트 해야 SQL Server Compact에서 SQL Server로 마이그레이션하려면 여전히 설정 되어 있으므로 게시 프로필.

이전 자습서에서 만든 연결 문자열 변환을 제거 하는 첫 번째 단계가입니다. 이러한 더 이상 되므로 세 키워드가 필요 게시 프로필에 연결 문자열 변환을 지정 합니다을 구성 하기 전에 수행한 것 처럼는 **SQL 패키지 및 게시** SQL Server로의 마이그레이션 위한 탭.

열기는 *Web.Test.config* 파일을 제거는 `connectionStrings` 요소입니다. 유일한 나머지 변환을 *Web.Test.config* 에 대 한 파일은는 `Environment` 값에 `appSettings` 요소입니다.

이제 테스트 환경에 게시 프로필 및 게시를 업데이트할 수 있습니다.

열기는 **웹 게시** 마법사, 그리고 후는 **프로필** 탭 합니다.

선택 된 **테스트** 게시 프로필.

선택 된 **설정을** 탭 합니다.

클릭 **새 데이터베이스에서 향상 된 게시 설정**합니다.

에 대 한 연결 문자열 상자에서 **SchoolContext**에서 사용한 동일한 값을 입력에서 *Web.Test.config* 이전 자습서에서 변환 파일:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

선택 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다. (프로그램 버전의 Visual Studio에서 확인란을 레이블이 지정 될 수 있습니다 **Code First 마이그레이션을 적용**.)

에 대 한 연결 문자열 상자에서 **DefaultConnection**에서 사용한 동일한 값을 입력에서 *Web.Test.config* 이전 자습서에서 변환 파일:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

둡니다 **데이터베이스 업데이트** 의 선택을 취소 합니다.

**게시**를 클릭합니다.

Visual Studio에서 코드 변경 내용을 테스트 환경에 배포 하 고 브라우저 Contoso 대학 홈 페이지를 엽니다.

강사 페이지를 선택 합니다.

이 페이지를 실행 하는 응용 프로그램 데이터베이스에 액세스 하려고 합니다. Code First 마이그레이션을 확인 하는 데이터베이스 현재 상태는 최신 마이그레이션 적용 되지 않은 아직 찾습니다 합니다. Code First 마이그레이션을 최신 마이그레이션 적용의 경우 실행는 `Seed` 메서드를 다음 페이지는 정상적으로 실행 합니다. 시드 된 데이터로 새 근무 시간 열을 참조 하는 경우.

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>데이터베이스 업데이트는 프로덕션 환경에 배포

또한 프로덕션 환경에 대 한 게시 프로필을 변경 해야 합니다. 이 경우 기존 프로필을 제거 하 고 업데이트 된.publishsettings 파일을 가져와서 새로 만들 합니다. 업데이트 된 파일에는 Cytanium에서 SQL Server 데이터베이스에 대 한 연결 문자열이 포함 됩니다.

연결 문자열 변환 테스트 환경에 배포 하는 경우 본 것 처럼 더 이상 필요는 *Web.Production.config* 변환 파일입니다. 파일을 제거 하는 열려는 `connectionStrings` 요소입니다. 나머지 변형은 대 한는 `Environment` 값에 `appSettings` 요소 및 `location` Elmah 오류 보고서에 대 한 액세스를 제한 하는 요소입니다.

프로덕션에 대 한 새 게시 프로필을 만들기 전에 업데이트 된.publishsettings 파일에서 이전에 수행한 동일한 방식으로 다운로드는 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다. (Cytanium 제어판 **웹사이트**, 클릭 하 고는 **contosouniversity.com** 웹 사이트입니다. 선택 된 **웹 게시** 탭을 클릭 한 다음 **이 웹 사이트에 대 한 게시 프로필 다운로드**.) 이렇게 하는 이유는.publishsettings 파일에서 데이터베이스 연결 문자열을 선택할 것입니다. 연결 문자열을 여전히를 사용한 SQL Server Compact 및 Cytanium에서 SQL Server 데이터베이스 아직 만들지 않았다면 때문에 파일을 다운로드 처음으로 사용할 수 있습니다.

이제 프로덕션 환경에 게시 프로필 및 게시를 업데이트할 수 있습니다.

열기는 **웹 게시** 마법사, 그리고 후는 **프로필** 탭 합니다.

클릭 **프로필 관리**, 한 다음 프로덕션 프로필을 삭제 합니다.

닫기는 **웹 게시** 이 변경 내용을 저장 하는 마법사입니다.

열기는 **웹 게시** 마법사를 다시 클릭 하 고 **가져오기**합니다.

에 **연결** 탭으로 변경 **대상 URL** 임시 URL을 사용 하는 경우 적절 한 값입니다.

**다음**을 클릭합니다.

에 **설정** 탭을 클릭 **새 데이터베이스에서 향상 된 게시 설정**합니다.

에 대 한 연결 문자열 드롭 다운 목록에서 **SchoolContext**를 Cytanium 연결 문자열을 선택 합니다.

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

선택 **실행 Code First 마이그레이션 (응용 프로그램 시작 시 실행)**합니다.

에 대 한 연결 문자열 드롭 다운 목록에서 **DefaultConnection**를 Cytanium 연결 문자열을 선택 합니다.

선택 된 **프로필** 탭을 클릭 **프로필 관리**, "Production"를 "contosouniversity.com-웹 배포"에서 프로필의 이름을 바꿉니다.

게시 프로필의 변경 내용을 저장 다음 다시 여십시오.

**게시**를 클릭합니다. (실제 프로덕션 웹 사이트에 대 한 복사 *앱\_offline.htm* 프로덕션 및 put를 게시 하기 전에 해당 프로젝트 폴더에서 다음 제거 배포가 완료 되 면.)

Visual Studio에서 코드 변경 내용을 테스트 환경에 배포 하 고 브라우저 Contoso 대학 홈 페이지를 엽니다.

강사 페이지를 선택 합니다.

Code First 마이그레이션을 테스트 환경에서 동일한 방식으로 데이터베이스를 업데이트 합니다. 시드 된 데이터로 새 근무 시간 열을 참조 하는 경우.

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

이제 성공적으로 배포한 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트는 SQL Server 데이터베이스를 사용 하 여 합니다.

## <a name="more-information"></a>추가 정보

이 일련의 제 3 자 호스팅 공급자에 ASP.NET 웹 응용 프로그램 배포에 대 한 자습서를 완료 했습니다. 이 자습서에 포함 된 항목 중 하나에 대 한 자세한 내용은 참조는 [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) MSDN 웹 사이트입니다.

## <a name="acknowledgements"></a>감사의 글

이 자습서 시리즈의 내용에 중요 한 기여를 수행한 다음 사람에 게 감사 하 고 싶습니다.

- [Alberto Poblacion, MVP &amp; MCT, 스페인](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod 퍼거슨, 데이터 플랫폼 개발 MVP United States
- Harsh Mittal, Microsoft
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi 이탈리아](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))
- [Scott 헌터, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))
- [Srđan Božović, 세르비아](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))

>[!div class="step-by-step"]
[이전](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[다음](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
