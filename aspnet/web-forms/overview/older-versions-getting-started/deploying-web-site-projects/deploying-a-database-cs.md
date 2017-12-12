---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
title: "데이터베이스 (C#)를 배포 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET 웹 응용 프로그램 개발 환경에서 프로덕션 환경에 필요한 파일 및 리소스를 가져오는 과정이 수반 됩니다. Da...에 대 한"
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/23/2009
ms.topic: article
ms.assetid: ff537a10-9f1f-43fe-9bcb-3dda161ba8f5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: f71e3cd1e81644df7b3dfed363b6f2ca826e610d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="deploying-a-database-c"></a>배포 데이터베이스 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_cs.pdf)

> ASP.NET 웹 응용 프로그램 개발 환경에서 프로덕션 환경에 필요한 파일 및 리소스를 가져오는 과정이 수반 됩니다. 데이터 기반 웹 응용 프로그램에 대해 여기에 데이터베이스 스키마 및 데이터입니다. 이 자습서를 프로덕션 개발 환경에서 데이터베이스를 성공적으로 배포 하는 데 필요한 단계를 사용 하는 일련의 첫 번째입니다.


## <a name="introduction"></a>소개

ASP.NET 웹 응용 프로그램 개발 환경에서 프로덕션 환경에 필요한 파일 및 리소스를 가져오는 과정이 수반 됩니다. 지난 6 개의 자습서의 과정 동안 간단한 책 검토 웹 응용 프로그램 배포 살펴보았습니다. 이 데모 사이트 다양 한 서버 쪽 리소스-ASP.NET 페이지, 구성 파일의 구성 된 한 `Web.sitemap` 이미지, CSS 파일 등의 파일 및 클라이언트 쪽 리소스와 함께 등-합니다. 하지만 웹 응용 프로그램 데이터 기반 어떻습니까? 데이터베이스를 사용 하는 웹 응용 프로그램을 배포 하는 추가 단계를 수행 해야?

다음 몇 가지 자습서를 통해 데이터 기반 웹 응용 프로그램을 배포 하는 데 필요한 단계가 다룰 것입니다. 이 자습서를 가져오는 방법을 내용과 데이터베이스의 스키마 개발 환경에서 프로덕션 환경에 후속 자습서에 필요한 구성 변경 내용을 검색 하는 동안를 검사 하 여 시작 합니다. 다음 배포 응용 프로그램 서비스 (멤버 자격, 역할, 프로필 및 등)를 사용 하는 데이터베이스의 과제 살펴보겠습니다.

## <a name="examining-the-updated-book-reviews-web-application"></a>업데이트 된 책 검토 웹 응용 프로그램 검사

데이터 기반 웹 응용 프로그램 배포를 보여 주기 위해 필자는 책 검토 웹 응용 프로그램 간단 하 고 정적 웹 사이트에서 데이터 기반 컴퓨터로 업데이트 했습니다. 이전에이 s 자습서 다운로드에 응용 프로그램의 두 가지 버전으로: 하나는 웹 응용 프로그램 프로젝트 모델 및 웹 사이트 프로젝트 모델을 사용 하는 하나를 사용 합니다.

업데이트 된 책 검토 웹 응용 프로그램 사용 하 여 한 [SQL Server 2008 Express Edition](https://www.microsoft.com/express/sql/default.aspx) s 사이트에 저장 되는 데이터베이스 `App_Data` 폴더 (`~/App_Data/Reviews.mdf`). SQL Server 2008 컴퓨터에 설치 되어 있는 경우에 데모 오류 없이 실행 해야 합니다. 이전 버전의 경우 무료 SQL Server 2008 Express Edition을 설치 하는 SQL Server를 유지할 수 있습니다 또는 데이터베이스를 만들 수 s이이 자습서에서 사용할 수 있는 스크립트를 다운로드 하는 데이터베이스를 사용할 수 있습니다.

`Reviews.mdf` 데이터베이스 4 개의 테이블이 포함 되어 있습니다.

- `Genres`-비즈니스, 기술 및 소설, 등 각 장르에 대 한 레코드가 포함 됩니다.
- `Books`-같은 열이 있는 각 검토에 대 한 레코드를 포함 `Title`, `GenreId`, `ReviewDate`, 및 `Review`, 등입니다.
- `Authors`-각 작성자 검토 책에 기여 하는 방법에 대 한 정보가 포함 됩니다.
- `BooksAuthors`-어떤 작성자 책 이나 작성 한을 지정 하는 다 대 다 조인 테이블입니다.
  

그림 1는 이러한 네 가지 테이블의 다이어그램을 보여 줍니다.


[![책 검토 웹 응용 프로그램의 데이터베이스는 4 개의 테이블 구성](deploying-a-database-cs/_static/image2.jpg)](deploying-a-database-cs/_static/image1.jpg) 

**그림 1**: 책 검토 웹 응용 프로그램의 데이터베이스는 4 개의 테이블 구성 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image3.jpg))


책 검토 웹 사이트의 이전 버전의 책에 대 한 별도 ASP.NET 페이지를 있습니다. 예를 들어 했습니다 라는 페이지 `~/Tech/TYASP35.aspx` 에 대 한 검토를 포함 하는 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서*합니다. 웹 사이트의이 새 데이터 기반 버전에는 데이터베이스와 Review.aspx?ID= 단일 ASP.NET 페이지에 저장 된 검토*bookId*, 지정 된 책에 대 한 검토를 표시 합니다. 마찬가지로, 한 Genre.aspx?ID=는*genreId* 지정 장르의 검토 한 책을 나열 하는 페이지입니다.

그림 2와 3 표시는 `Genre.aspx` 및 `Review.aspx` 동작의 페이지입니다. 각 페이지에 대 한 주소 표시줄에 URL을 note 합니다. 그림 2 it s Genre.aspx? ID = 85d164ba-1123-4 c 47-82a0-c8ec75de7e0e 합니다. 85d164ba-1123-4c47-82a0-c8ec75de7e0e 이므로 `GenreId` 기술 장르, "기술 검토" s 페이지 머리글 읽기 및 글머리 기호 목록에 대 한 값이이 장르에 속하는 사이트에 해당 리뷰를 열거 합니다.


[![기술 장르 페이지](deploying-a-database-cs/_static/image5.jpg)](deploying-a-database-cs/_static/image4.jpg) 

**그림 2**: The 기술 장르 페이지 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image6.jpg))


[![에 대 한 검토 학습 ASP.NET 3.5에서 24 시간](deploying-a-database-cs/_static/image8.jpg)](deploying-a-database-cs/_static/image7.jpg) 

**그림 3**:에 대 한 The 검토 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서* ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image9.jpg))


검토 하는 책 웹 응용 프로그램에 있는 관리자 수 추가, 편집 및 삭제 장르, 검토 및 정보를 작성 하는 관리 섹션도를 포함 됩니다. 현재 모든 방문자 관리 섹션에는 액세스할 수 있습니다. 이후 자습서에서 사용자 계정에 대 한 지원을 추가 알아보고 관리 페이지에 권한이 있는 사용자가 통해서만 수 있도록 하겠습니다.

다운로드 하는 경우 책 검토 응용 프로그램 하십시오의 용도 데이터 기반 응용 프로그램 배포를 보여 주는 것에 유의 합니다. 응용 프로그램 디자인 뿌리 모범 사례는 발생 하지 않습니다. 예를 들어는 없는 별도 DAL 데이터 액세스 계층 (); ASP.NET 페이지 SqlDataSource 컨트롤 또는 해당 코드 숨김 클래스의 ADO.NET 코드를 통해 데이터베이스와 직접 통신 합니다. 계층화 된 아키텍처를 사용 하 여 데이터 기반 응용 프로그램을 만들기에 대 한 자세한 설명, 참조 내 [ *데이터로 작업* 자습서](../../data-access/index.md)합니다.

## <a name="databases-on-development-versus-production"></a>개발 및 프로덕션에 있는 데이터베이스

데이터 기반 웹 응용 프로그램에서 개발을 시작 하면 데이터베이스에 연결 하는 방법에는 응용 프로그램 세부 정보를 제공 하는 데이터베이스 연결 문자열을 지정 해야 합니다. 이 연결 문자열 지정 하지만, 다른 작업, 데이터베이스 서버, 데이터베이스 이름 및 보안 정보입니다. 대부분의 경우 개발 하는 동안 응용 프로그램에서 사용 되는 데이터베이스 다른 경우에 데이터베이스를 사용 하는 경우는 해당 프로덕션 환경에서 s 합니다. 프로덕션 및 개발을 위한 다른 데이터베이스를 사용 하는 방법은 많은 이점이 있습니다. 안 실수로 수정 하거나 라이브 데이터를 삭제 하는 방법에 대 한 걱정할 필요가 개발에 데이터베이스를 다른 것입니다. 또한 더미 테스트 데이터에 배치 하거나 주요 변경 사항을 데이터 모델을 프로덕션 환경에서 응용 프로그램에 미치는 영향에 걱정할 필요 없이 수도 있습니다. 다른 데이터베이스 개발 및 프로덕션 환경에는 응용 프로그램이 단점은의 데이터베이스 스키마를 데이터베이스와 관련 된 변경 사항을 배포 하거나 데이터를 배포 해야 합니다.

첫 번째 배포 하기 전에 데이터베이스의 인스턴스 하나만 않으며 개발 환경에서 해당 인스턴스는 합니다. 처음으로 프로덕션 환경에 응용 프로그램을 배포 하는 경우 म 해야 필요한 서버 쪽 및 클라이언트 파일을 복사할 뿐만 아니라 또한 개발 환경에서 프로덕션 환경에 데이터베이스를 복사 합니다. 이 여기서 변함이 없으며 오른쪽 책 검토 웹 응용 프로그램-으로 데이터베이스에 상주 하는 이제는 `App_Data` 개발 환경에서 폴더 하지 않았으면 하지만 프로덕션 환경에 밀어 넣은 아직 합니다.

응용 프로그램이 배포 된 후에 데이터베이스의 두 복사본이 있습니다. 응용 프로그램이 완성 되어 감에 새로운 기능이 추가 될 수 있습니다, 데이터 모델에 대 한 변경 하기 하며 (예: 기존 테이블에 새 열 추가, 변경 하기 새 테이블을 추가 하는 기존 열 및 등). 웹 응용 프로그램은 다음 배포를 마지막 배포는 프로덕션 데이터베이스에 적용 해야 하는 이후 개발 환경에서 데이터베이스에 변경 내용을 적용 합니다. 이 프로세스를 관리 하기 위한 몇 가지 전략은 이후 자습서에 설명 되어 있습니다. 이 자습서를 프로덕션 개발 환경에서 전체 데이터베이스를 배포 하는 방법에 중점을 둡니다.

## <a name="deploying-the-database-to-the-production-environment"></a>프로덕션 환경에 데이터베이스 배포

이 자습서의 나머지 부분에서는 개발 환경에서 데이터베이스를 프로덕션 환경에 배포 하는 방법을 살펴봅니다. 사용자와 함께 하는 경우 필요한 하려면 웹 호스트 공급자를 사용 하 여 계정에 Microsoft SQL Server를 포함 해야 데이터베이스 지원 합니다. 몇 가지 정보, 즉 데이터베이스 서버 이름, 데이터베이스 이름 및는 사용자 이름 및 암호는 데이터베이스에 연결 하는 데 사용 해야 합니다.

책 검토 s 웹 사이트 데이터베이스에 저장 된 SQL Server 2008 Express Edition 데이터베이스는이 자습서의 앞부분에서 설명 했 듯이 `App_Data` 폴더입니다. 이러한 데이터베이스를 배포 복사 처럼 간단할 것 이유를 stand가 `App_Data` 개발 환경에서 프로덕션 환경에 폴더입니다. 그러나 대부분의 웹 호스트 공급자 호스팅 데이터베이스에 지원 하지 않습니다는 `App_Data` 보안상의 이유로 인해 폴더입니다. 대신, 웹 호스트 환경 내에서 SQL Server 데이터베이스 서버에서 계정을 제공 합니다. 개발 환경에서 데이터베이스를 프로덕션 환경으로 배포 웹 호스트의 데이터베이스 서버에 등록 된 데이터베이스를 가져오는 필요 합니다.

따라서 가져오려면 어떻게 해야 할까요 데이터베이스 개발 환경에서 프로덕션 환경으로? 이를 위해 해당 웹 호스트 제공 서비스에 따라 몇 가지가 있습니다. DiscountASP.NET, 같은 일부 호스트와의 데이터베이스 또는 실제 백업을 FTP 수 `.mdf` 웹 사이트에 파일 및 그런 다음 제어판에서 백업 파일을 복원 또는 연결 된 `.mdf` 파일을 SQL Server 데이터베이스 서버입니다. 이러한 도구와 함께 데이터베이스 배포 하는 작업은 복사 하는 것은 `App_Data` 프로덕션 환경과 한 다음 제어판을 통해 연결 하는 폴더입니다. 이 데이터베이스를 처음으로 게시할 수 쉽고 빠른 방법입니다.

또 다른 방법은 데이터베이스 게시 마법사를 사용 하는 것입니다. 데이터베이스 게시 마법사는 해당 테이블에서-테이블, 저장된 프로시저, 뷰, 사용자 정의 함수 및 기타-s 스키마 및 필요에 따라 데이터를 만드는 SQL 명령을 생성 하는 Windows 데스크톱 응용 프로그램입니다. 다음 SQL Server Management Studio를 통해 웹 호스트 공급자의 데이터베이스 서버에 연결 하 고 프로덕션에 있는 데이터베이스를 복제 하는이 스크립트를 실행할 수 있습니다. 더 나은, 웹 호스트 공급자에서 지원할 경우 Microsoft s [Database Publishing Services](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home) 사용자 대신 데이터베이스 서버에서 자동으로 실행 되는 데이터베이스 게시 마법사에 의해 생성 된 스크립트를 사용할 수 있습니다. 웹 호스트 공급자는 업로드 된 연결과 같은 기능을 제공 하는 여부에 관계 없이 작동 데이터베이스 게시 마법사에서는 s 데이터베이스 스키마 및 데이터를 만드는 스크립트를 생성 하므로 `.mdf` 파일입니다.

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>데이터베이스 스키마 및 데이터베이스 게시 마법사를 사용 하 여 데이터를 만드는 SQL 명령 생성

데이터베이스 게시 마법사를 사용 하 여 프로덕션 환경에 책 검토 데이터베이스를 배포 하는 과정을 안내 하는 s를 사용 합니다. Visual Studio 2008을 사용 하는 경우 또는 다음, 데이터베이스 게시 마법사 이미 설치 되었습니다. Visual Studio 2005를 사용 하는 경우 첫 번째 해야 [다운로드 및 설치](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en) 마법사.

Visual Studio를 열고 탐색 하 고 `Reviews.mdf` 데이터베이스입니다. Visual Web Developer를 사용 하는 경우 데이터베이스 탐색기;로 이동 Visual Studio를 사용 하는 경우 서버 탐색기를 사용 합니다. 그림 4는 `Reviews.mdf` Visual Web Developer에서 데이터베이스 탐색기에서 데이터베이스입니다. 그림 4에서 볼 수 있듯이 `Reviews.mdf` 데이터베이스 테이블 4, 3 개의 저장된 프로시저 및 사용자 정의 함수로 구성 됩니다.


[![데이터베이스 탐색기 또는 서버 탐색기에서 데이터베이스를 찾으려면](deploying-a-database-cs/_static/image11.jpg)](deploying-a-database-cs/_static/image10.jpg) 

**그림 4**: 데이터베이스 탐색기 또는 서버 탐색기에서 데이터베이스를 찾습니다 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image12.jpg))


데이터베이스 이름을 단추로 클릭 하 고 상황에 맞는 메뉴에서 "공급자에 게시" 옵션을 선택 합니다. 데이터베이스 게시 마법사가 시작 됩니다 (그림 5 참조). 클릭 하 여 시작 화면을 지 나 이동 합니다.


[![데이터베이스 게시 마법사 시작 화면](deploying-a-database-cs/_static/image14.jpg)](deploying-a-database-cs/_static/image13.jpg) 

**그림 5**: The 데이터베이스 게시 마법사 시작 화면 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image15.jpg))


마법사에서 두 번째 화면 데이터베이스 게시 마법사에 액세스할 수 있는 데이터베이스를 나열 하 고 선택한 데이터베이스의 모든 개체를 스크립팅하려면 하거나 스크립트에 개체를 선택할를 선택할 수 있습니다. 적절 한 데이터베이스를 선택 하 고 "스크립트에 모든 선택된 된 데이터베이스에 개체" 옵션을 선택 된 상태로 둡니다.

> [!NOTE]
> 오류가 발생 하는 경우 "데이터베이스에는 개체가 *databaseName* 이 마법사에서 스크립팅할 수 있는 유형의" 그림 6에 표시 된 화면에서 다음을 클릭 하는 경우 데이터베이스 파일의 경로를 너무 길지 않은지 있는지 확인 합니다. 검색 데이터베이스 파일의 경로를 너무 길면이 오류가 발생할 수 있습니다.


[![데이터베이스 게시 마법사 시작 화면](deploying-a-database-cs/_static/image17.jpg)](deploying-a-database-cs/_static/image16.jpg) 

**그림 6**: The 데이터베이스 게시 마법사 시작 화면 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image18.jpg))


다음 화면에서 있습니다 수 스크립트 파일을 생성 하거나 웹 호스트 지원 가능한 경우 웹 호스트 공급자의 데이터베이스 서버에 직접 데이터베이스를 게시 합니다. 그림 7에서 볼 수 있듯이 스크립트 파일에 쓸 수 없는 `C:\REVIEWS.MDF.sql`합니다.


[![데이터베이스를 파일 또는 Your 웹 호스트 공급자에 직접 게시](deploying-a-database-cs/_static/image20.jpg)](deploying-a-database-cs/_static/image19.jpg) 

**그림 7**: 데이터베이스를 파일 또는 Your 웹 호스트 공급자에 직접 게시 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image21.jpg))


다음 화면에서 다양 한 스크립팅 옵션에 대 한 라는 메시지가 나타납니다. 스크립트를 이러한 기존 개체를 제거 하려면 drop 문을 포함할지 여부를 지정할 수 있습니다. 기본값은 True 이면은 처음으로 데이터베이스를 배포 하는 경우. SQL Server 2000, SQL Server 2005 또는 SQL Server 2008 데이터베이스에서 대상 데이터베이스로 인지 여부를 지정할 수 있습니다. 마지막으로, 스키마와 데이터를 스크립팅할 지 여부를 나타낼 수 있습니다는 데이터만 또는 스키마만. 스키마는 데이터베이스 개체, 테이블, 저장된 프로시저, 뷰 및 등의 컬렉션입니다. 데이터는 테이블에 있는 정보입니다.

그림 8 에서처럼 I 했습니다 (SQL Server 2008 데이터베이스에 대 한 스크립트를 생성 하 고 스키마와 데이터를 게시 하려면 기존 데이터베이스 개체를 삭제 하도록 구성 마법사를) 가져왔습니다.


[![지정 된 게시 옵션](deploying-a-database-cs/_static/image23.jpg)](deploying-a-database-cs/_static/image22.jpg) 

**그림 8**: 게시 옵션 지정 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image24.jpg))


마지막 두 개의 화면 요약 작업을 수행 하 고 다음 스크립트의 상태를 표시 하려고 합니다. 마법사를 실행의 결과에 프로덕션 데이터베이스를 만들고 개발에서와 같이 동일한 데이터로 채우는 데 필요한 SQL 명령을 포함 하는 스크립트 파일을 포함할 것입니다.

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>프로덕션 환경 데이터베이스에서 SQL 명령 실행

이제 남아 있는 데이터베이스 및 해당 데이터를 만드는 SQL 명령이 포함 된 스크립트를 프로덕션 데이터베이스에서 스크립트를 실행 합니다. 일부 웹 호스트 공급자는 SQL 데이터베이스에서 실행할 명령을 입력할 수 있는 해당 제어판의 textbox를 제공 합니다. 매우 큰 스크립트 파일이 있는 경우이 옵션이 작동 하지 않을 수 있습니다 (의 `REVIEWS.MDF.sql` 스크립트 파일은 크기가 425 647KB 넘는 예를 들어).

SQL Server Management Studio (SSMS)를 사용 하 여 프로덕션 데이터베이스 서버에 직접 연결 하는 것이 좋습니다. 비-Express Edition의 SQL Server 컴퓨터에 설치 되어 있는 경우 다음 가능성이 이미 있으면 SSMS를 설치 합니다. 수, [다운로드 및 설치](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) SQL Server Management Studio Express Edition의 무료 복사본입니다.

SSMS를 시작 하 고 웹 호스트 공급자가 제공 하는 정보를 사용 하 여 웹 호스트의 데이터베이스 서버에 연결 합니다.


[![웹 호스트 공급자의 데이터베이스 서버에 연결](deploying-a-database-cs/_static/image26.jpg)](deploying-a-database-cs/_static/image25.jpg) 

**그림 9**: Your 웹 호스트 공급자의 데이터베이스 서버에 연결 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image27.jpg))


데이터베이스 탭을 확장 하 고 데이터베이스를 찾습니다. 도구 모음의 왼쪽된 위 모서리에서 새 쿼리 단추를 클릭 하 고 데이터베이스 게시 마법사에서 만든 스크립트 파일에서 SQL 명령에 붙여 넣고 프로덕션 데이터베이스 서버에서 이러한 명령을 실행 하 고 실행 단추를 클릭 합니다. 스크립트 파일은 특히 큰 경우 명령을 실행 하는 데 몇 분 정도 걸릴 수 있습니다.


[![웹 호스트 공급자의 데이터베이스 서버에 연결](deploying-a-database-cs/_static/image29.jpg)](deploying-a-database-cs/_static/image28.jpg) 

**그림 10**: Your 웹 호스트 공급자의 데이터베이스 서버에 연결 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image30.jpg))


모두 완료 s가입니다! 이 시점에서 개발 데이터베이스를 프로덕션 중복 되었습니다. SSMS에서 데이터베이스를 새로 고치는 경우 새 데이터베이스 개체를 표시 됩니다. 그림 11 프로덕션의 데이터베이스 테이블, 저장된 프로시저 및 개발 데이터베이스의 미러링 하는 사용자 정의 함수를 보여 줍니다. 있고 데이터를 게시할 데이터베이스 게시 마법사를 시작 하는 것 때문에 프로덕션 데이터베이스의 테이블 개발 데이터베이스의 테이블와 동일한 데이터에 마법사가 실행 된 시간입니다. 그림 12에서 데이터를 보여 줍니다.는 `Books` 프로덕션 데이터베이스의 테이블입니다.


[![프로덕션 데이터베이스에서 데이터베이스 개체에 중복 된 된](deploying-a-database-cs/_static/image32.jpg)](deploying-a-database-cs/_static/image31.jpg) 

**그림 11**: The 데이터베이스 개체는 복제 된 프로덕션 데이터베이스에서 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image33.jpg))


[![프로덕션 데이터베이스 개발 데이터베이스에서와 동일한 데이터를 포함합니다.](deploying-a-database-cs/_static/image35.jpg)](deploying-a-database-cs/_static/image34.jpg) 

**그림 12**: 개발 데이터베이스에서와 동일한 데이터를 포함 하는 프로덕션 데이터베이스 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image36.jpg))


이 시점에서 개발 데이터베이스를 프로덕션 배포만 있는 되었습니다. म 아직 하거나 하지 않은 자체 웹 응용 프로그램 배포에서 응용 프로그램을 프로덕션에서 프로덕션 데이터베이스를 사용 하는 데 필요한 어떤 구성 변경 내용을 검사 합니다. 이러한 문제는 다음 자습서에서 설명 합니다!

## <a name="summary"></a>요약

데이터 기반 웹 응용 프로그램 배포 프로덕션 환경으로 개발 하는 동안 사용 되는 데이터베이스를 복사 해야 합니다. 많은 웹 호스트 공급자는 데이터베이스를 배포 하는 과정을 단순화 하는 도구를 제공 합니다. 예를 들어 DiscountASP.NET와 있습니다 수 FTP 데이터베이스 `.mdf` 파일 (또는 백업) 후 제어판에서 데이터베이스 서버에 데이터베이스를 연결 합니다. 어떤 기능에 관계 없이 작동 하는 또 다른 옵션 해당 웹 호스트 공급자 제공은 개발 데이터베이스의 스키마 및 데이터를 만드는 SQL 명령에 대 한 스크립트를 생성 하는 Microsoft의 데이터베이스 게시 마법사 도구입니다. 이 스크립트를 생성 한 후에 프로덕션 데이터베이스에서 실행할 수 있습니다.

이제 책 검토 웹 응용 프로그램의 데이터베이스는 프로덕션에 응용 프로그램을 배포할 수 있습니다. 그러나 웹 응용 프로그램의 구성 정보를 데이터베이스에 대 한 연결 문자열을 지정 하 고 해당 연결 문자열 개발 데이터베이스를 참조 합니다. 프로덕션 환경에 사이트를 배포 하는 경우이 연결 문자열 정보를 업데이트 해야 합니다. 이러한 구성의 차이 다음 자습서 찾은 프로덕션 환경에 데이터 기반 책 검토 사이트를 게시 하는 데 필요한 단계를 안내 합니다.

만족도 매우 프로그래밍!

#### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Microsoft SQL Server 데이터베이스 게시 마법사 1.1을 다운로드 합니다.](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [Microsoft SQL Server Management Studio Express Edition 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

>[!div class="step-by-step"]
[이전](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
[다음](configuring-the-production-web-application-to-use-the-production-database-cs.md)
