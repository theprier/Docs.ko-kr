---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: f9f100ccaf5e9cfdaf0633f9bfebbad273212a0e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839174"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms
====================
[Tom Dykstra](https://github.com/tdykstra)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다.
> 
> 자습서에서 C# 예제를 보여 줍니다. 합니다 [다운로드할 수 있는 샘플](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) C# 및 Visual Basic 코드를 포함 합니다.
> 
> ## <a name="database-first"></a>먼저 데이터베이스
> 
> 세 가지 방법으로 Entity Framework에서 데이터로 작업할 수 있습니다: *Database First*를 *Model First*, 및 *Code First*합니다. Database First에 대 한이 자습서가입니다. 시나리오에 가장 적합 한 선택 하는 방법은 이러한 워크플로 및 지침 간의 차이점에 대 한 정보를 참조 하세요 [Entity Framework 개발 워크플로](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.
> 
> ## <a name="web-forms"></a>Web Forms
> 
> 이 자습서 시리즈는 ASP.NET Web Forms 모델을 사용 하 고 Visual Studio에서 ASP.NET Web Forms를 사용 하는 방법을 알고 있다고 가정 합니다. 를 찾을 수 없으면 [Getting Started with ASP.NET 4.5 Web Forms](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다. ASP.NET MVC 프레임 워크를 사용 하 여 작업 하려는 경우 참조 [Getting Started with ASP.NET MVC를 사용 하 여 Entity Framework](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **자습서에 표시** | **역시** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web입니다. 자습서는 뒷부분에 나오는 버전의 Visual Studio를 사용 하 여 거치지 않았습니다. 메뉴 선택, 대화 상자 및 템플릿에서 다음과 같은 많은 차이가 있습니다. |
> | .NET 4 | .NET 4.5는.NET 4와 역방향 호환이 가능 하지만.NET 4.5를 사용 하 여 자습서를 거치지 않았습니다. |
> | Entity Framework 4 | 자습서는 뒷부분에 나오는 버전의 Entity Framework를 사용 하 여 거치지 않았습니다. Entity Framework 5 부터는 EF는 기본적으로 `DbContext API` 는 EF 4.1에서 도입 되었습니다. EntityDataSource 컨트롤을 사용 하도록 설계 되었습니다는 `ObjectContext` API. 컨트롤의 EntityDataSource를 사용 하는 방법에 대 한 자세한 합니다 `DbContext` API 참조 [이 블로그 게시물](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)합니다. |
> 
> ## <a name="questions"></a>질문
> 
> 에 자습서로 직접 관련 되지 않은 질문이 있을 수를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)서 [Entity Framework 및 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), 또는 [ StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="overview"></a>개요

이 자습서에서 작성 하는 응용 프로그램은 간단한 대학 웹 사이트입니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 만든 화면 중 몇 가지는 다음과 같습니다.

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>웹 응용 프로그램 만들기

이 자습서를 시작 하려면 Visual Studio를 열고 사용 하 여 새 ASP.NET 웹 응용 프로그램 프로젝트를 만든 합니다 **ASP.NET 웹 응용 프로그램** 템플릿:

[![Image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

이 템플릿은 이미 스타일 시트 및 마스터 페이지를 포함 하는 웹 응용 프로그램 프로젝트를 만듭니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

엽니다는 *Site.Master* 파일과 "My ASP.NET Application"를 "Contoso University" 변경 합니다.

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

찾을 합니다 *메뉴* 라는 컨트롤 `NavigationMenu` 만들게 될 페이지에 대 한 메뉴 항목을 추가 하는 다음 태그로 바꿉니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

엽니다는 *Default.aspx* 페이지 및 변경 합니다 `Content` 라는 컨트롤 `BodyContent` 이:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

이제 간단한 홈 페이지를 만들 수 있는 다양 한 페이지에 대 한 링크를 사용 하 여 제공 됩니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>데이터베이스 만들기

이 자습서에서는 기존 데이터베이스를 기반으로 데이터 모델을 자동으로 만들려면 Entity Framework 데이터 모델 디자이너를 사용 하겠습니다 (라고도 합니다 *데이터베이스 중심* 접근 방식). 이 자습서 시리즈에서 다루지 않는 대신 수동으로 데이터 모델을 생성 한 후 데이터베이스를 만든 디자이너 생성 스크립트를 (합니다 *모델 우선* 접근 방식).

이 자습서에 사용 되는 데이터베이스를 첫 번째 방법의 경우 사이트 데이터베이스를 추가 하려면 다음 단계가입니다. 먼저이 자습서를 사용 하 여 이동 하는 프로젝트를 다운로드 하는 가장 쉬운 방법은 있습니다. 마우스 오른쪽 단추로 클릭는 *앱\_데이터* 폴더를 선택 **기존 항목 추가**를 선택 합니다 *School.mdf* 다운로드 한 프로젝트에서 데이터베이스 파일.

대안은에서 지침을 따릅니다 [School 샘플 데이터베이스 만들기](https://msdn.microsoft.com/library/bb399731.aspx)합니다. 데이터베이스를 다운로드 하거나 만드는 하는지 여부를 복사 합니다 *School.mdf* 응용 프로그램의 다음 폴더에서 파일 *앱\_데이터* 폴더:

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

(이 위치는 *.mdf* 파일 SQL Server 2008 Express를 사용 하는 것으로 가정 합니다.)

스크립트에서 데이터베이스를 만든 경우에 데이터베이스 다이어그램을 만들려면 다음 단계를 수행 합니다.

1. **서버 탐색기**, 확장 **데이터 연결**를 확장 *School.mdf*를 마우스 오른쪽 단추로 클릭 **데이터베이스 다이어그램**, 선택한 **새 다이어그램 추가**합니다.

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. 모든 테이블을 선택 하 고 클릭 **추가**합니다.

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server 테이블, 테이블 및 테이블 간의 관계에서 열을 보여 주는 데이터베이스 다이어그램을 만듭니다. 원하는 구성 하기 위한 해결 방법은 테이블을 이동할 수 있습니다.
3. "SchoolDiagram"으로 다이어그램을 저장 하 고 닫습니다.

다운로드 하는 경우는 *School.mdf* 이 자습서에서는 이동 하는 파일을 두 번 클릭 하 여 데이터베이스 다이어그램을 볼 수 있습니다 **SchoolDiagram** 아래의 **데이터베이스 다이어그램** 에서 **서버 탐색기**합니다.

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

다이어그램을 사용 하면 다음과 같은 모양의 (여기에 나오는 내용과 다른 위치에 있는 테이블 수 있음):

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>Entity Framework 데이터 모델 만들기

이제이 데이터베이스에서 Entity Framework 데이터 모델을 만들 수 있습니다. 응용 프로그램의 루트 폴더에서 데이터 모델을 만들 수 있지만이 자습서에서는 배치한 라는 폴더에 *DAL* (데이터 액세스 계층)에 대 한 합니다.

**솔루션 탐색기**, 프로젝트 폴더를 추가 *DAL* (프로젝트, 솔루션에 포함 되지 않는 것이 있는지 확인).

마우스 오른쪽 단추로 클릭 합니다 *DAL* 한 다음 선택한 폴더 **추가** 하 고 **새 항목**. 아래 **설치 된 템플릿**를 선택 **데이터**를 선택 합니다 **ADO.NET 엔터티 데이터 모델** 템플릿을 이름을 *SchoolModel.edmx*, 및 누른 **추가**합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

엔터티 데이터 모델 마법사가 시작 됩니다. 첫 번째 마법사 단계의 합니다 **데이터베이스에서 생성** 옵션은 기본적으로 선택 됩니다. **다음**을 클릭합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

에 **데이터 연결 선택** 단계에서 기본값을 그대로 두고 클릭 **다음**합니다. School 데이터베이스는 기본적으로 선택 되 고 연결 설정에 저장 됩니다는 *Web.config* 다른 이름으로 파일 **SchoolEntities**합니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

에 **데이터베이스 개체 선택** 마법사 단계를 제외 하 고 테이블 모두 선택 `sysdiagrams` (이전에 생성 된 다이어그램에 대 한 만든)을 클릭 한 다음 **마침**.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

모델 만들기, 완료 된 후 Visual Studio 표시 그래픽 데이터베이스 테이블에 해당 하는 Entity Framework 개체 (엔터티). (데이터베이스 다이어그램에서와 마찬가지로 개별 요소의 위치 다를 수 있습니다이 그림에 표시 합니다. 끌 수 있습니다 요소 하려는 경우이 그림과를 약.)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>Entity Framework 데이터 모델 탐색

엔터티 다이어그램 매우 비슷하지만 몇 가지 차이점을 사용 하 여 데이터베이스 다이어그램을 볼 수 있습니다. 한 가지 차이점은 연결의 형식을 나타내는 기호가 각 연결의 끝에 추가 (테이블 관계 라고 엔터티 연결에서 데이터 모델):

- 0 또는 1을 한 연결을 "1" 및 "0..1"으로 표시 됩니다.

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    이 경우에 `Person` 엔터티 수 또는 사용 하 여 연결 될 수 있습니다는 `OfficeAssignment` 엔터티. `OfficeAssignment` 엔터티를 사용 하 여 연결 되어야 합니다는 `Person` 엔터티. 즉, 강사 사무실에 할당할 수 없습니다 수도 있으며 모든 office 하나만 강사에 할당할 수 있습니다.
- 1 대 다 연결을 "1"은 표현 및 "\*"입니다.

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    이 경우에 `Person` 엔터티 수 또는 연결 된 가능성이 `StudentGrade` 엔터티. A `StudentGrade` 엔터티 하나를 사용 하 여 연결 해야 합니다. `Person` 엔터티. `StudentGrade` 엔터티는 실제로 등록된 과정을에서이 데이터베이스를 나타냅니다. 학생 과정에 등록 되 고 없습니다 등급을 아직 없는 경우는 `Grade` 속성이 null입니다. 즉, 학생 과정에 등록할 수 있습니다 아직 하나의 강좌에 등록할 수 있습니다 또는 여러 과목에 등록할 수 있습니다. 등록된 과정에서 각 학년 하나만 학생에 적용 됩니다.
- 다 대 다 연결을 나타내는 "\*"및"\*"입니다.

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    이 경우에 `Person` 엔터티 수 또는 연결 되어 있지 `Course` 엔터티와 반대로 마찬가지입니다:는 `Course` 엔터티 수 또는 연결 되어 있지 `Person` 엔터티. 즉, 강사는 여러 강좌를 가르칠 수 있습니다 하 고 여러 강사가 한 강좌를 수업 할 수 있습니다. (이 데이터베이스에서이 관계 강사 에게만 적용 됩니다.; 과정에 학생을 연결 하지 않습니다. 학생에 연결 된 과정 StudentGrades 테이블입니다.)

데이터베이스 다이어그램 및 데이터 모델의 또 다른 차이점은 추가로 **탐색 속성** 각 엔터티에 대 한 섹션입니다. 엔터티의 탐색 속성을 관련된 엔터티를 참조합니다. 예를 들어를 `Courses` 에서 속성을 `Person` 모든 컬렉션을 포함 하는 엔터티를 `Course` 는 관련 된 엔터티 `Person` 엔터티.

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

데이터베이스 및 데이터 모델의 또 다른 차이점이 아직를 `CourseInstructor` 연결할 데이터베이스에 사용 되는 연결 테이블을 `Person` 및 `Course` 다 대 다 관계의 테이블입니다. 탐색 속성을 관련 가져올 수 `Course` 에서 엔터티는 `Person` 엔터티 및 관련 `Person` 에서 엔터티를 `Course` 엔터티 데이터 모델의 연결 테이블을 나타내는 데 필요 하지 않으므로 합니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

이 자습서에 대 한 가정 합니다 `FirstName` 열의 `Person` 실제로 표에 모두 사람의 첫 번째 이름과 중간 이름입니다. 이 반영 하 여 필드의 이름을 변경 하려고 하지만 데이터베이스 관리자 (DBA) 데이터베이스를 변경 하지 않을 수도 있습니다. 이름을 변경할 수 있습니다는 `FirstName` 해당 데이터베이스를 해당 하는 그대로 유지 하면서 데이터 모델에서 속성 변경 되지 않습니다.

디자이너에서 마우스 오른쪽 단추로 클릭 **FirstName** 에 `Person` 엔터티를 선택한 후 **이름 바꾸기**합니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

"FirstMidName" 새 이름을 입력 합니다. 이 데이터베이스를 변경 하지 않고 코드의 열 참조 방식으로 변경 합니다.

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

Model 브라우저에는 데이터베이스 구조, 데이터 모델 구조 및 이들 간의 매핑을 보려면 다른 방법을 제공 합니다. 을 확인 하려면 entity designer의 빈 영역을 마우스 오른쪽 단추로 클릭 하 고 클릭 **Model 브라우저**합니다.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

합니다 **Model 브라우저** 창의 트리 뷰를 표시 합니다. (합니다 **Model 브라우저** 창에 도킹할 수 있습니다 합니다 **솔루션 탐색기** 창입니다.) **SchoolModel** 노드가 데이터 모델 구조와 **SchoolModel.Store** 노드 데이터베이스 구조를 나타냅니다.

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

확장 **SchoolModel.Store** 테이블을 보려면 확장 **테이블 / 뷰** 테이블 참조를 확장 한 다음 **코스** 테이블 내의 열을 표시 합니다.

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

확장 **SchoolModel**, 확장 **엔터티 형식**를 차례로 확장 합니다 **과정** 노드에서 엔터티 및 엔터티 내의 속성을 볼 수.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

하거나 디자이너에서 또는 **Model 브라우저** 창 Entity Framework 두 모델의 개체를 연결 하는 방법을 볼 수 있습니다. 마우스 오른쪽 단추로 클릭 합니다 `Person` 엔터티 및 선택 **테이블 매핑**합니다.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

열립니다는 **매핑 정보** 창입니다. 이 창에서는 볼 수 있습니다는 알림 데이터베이스 열 `FirstName` 매핑되 `FirstMidName`, 내용에서 이름을 바꾼 되도록 데이터 모델입니다.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

Entity Framework는 XML을 사용 하 여 데이터베이스, 데이터 모델 사이의 매핑을 대 한 정보를 저장 합니다. 합니다 *SchoolModel.edmx* 파일은 실제로이 정보를 포함 하는 XML 파일입니다. 마우스 오른쪽 단추로 클릭 하 여 XML로 파일을 볼 수도 있습니다 하지만 그래픽 형식으로 정보를 렌더링 하는 디자이너는 *.edmx* 파일 **솔루션 탐색기**을 클릭 하 고 **열기와**를 선택 하 고 **XML (텍스트) 편집기**합니다. (데이터 모델 디자이너 및 XML 편집기는 두 가지가 열기와 같은 파일을 사용 하므로 디자이너를 열고 동시 XML 편집기에서 파일을 열 수 없습니다.)

이제 웹 사이트, 데이터베이스 및 데이터 모델을 만들었습니다. 작업 데이터 모델 및 ASP.NET을 사용 하 여 데이터를 사용 하 여 다음 연습에서는 먼저 `EntityDataSource` 제어 합니다.

> [!div class="step-by-step"]
> [다음](the-entity-framework-and-aspnet-getting-started-part-2.md)
