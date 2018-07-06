---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
title: 데이터베이스 (VB) 배포 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 응용 프로그램 개발 환경에서 프로덕션 환경에 필요한 파일 및 리소스를 시작 하는 작업을 수반 합니다. 에 대 한 da...
ms.author: aspnetcontent
ms.date: 04/23/2009
ms.assetid: 96ac3e69-04c7-4917-ad06-5f8968c3fbf1
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: c49b963cb5cfc40d8a0b03eb3ca722e3b789eab2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836277"
---
<a name="deploying-a-database-vb"></a>배포 데이터베이스 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_vb.pdf)

> ASP.NET 웹 응용 프로그램 개발 환경에서 프로덕션 환경에 필요한 파일 및 리소스를 시작 하는 작업을 수반 합니다. 데이터 기반 웹 응용 프로그램에 대 한 데이터베이스 스키마 및 데이터 포함 합니다. 이 자습서는 성공적으로 프로덕션 개발 환경에서 데이터베이스를 배포 하는 데 필요한 단계를 탐색 하는 일련의 첫 번째입니다.


### <a name="introduction"></a>소개

ASP.NET 웹 응용 프로그램 개발 환경에서 프로덕션 환경에 필요한 파일 및 리소스를 시작 하는 작업을 수반 합니다. 지난 6 자습서를 통해 간단한도 서 리뷰 웹 응용 프로그램 배포 살펴보았습니다. 이 데모 사이트 다양 한 서버 쪽 리소스-ASP.NET 페이지, 구성 파일, 구성 된는 `Web.sitemap` 이미지 및 CSS 파일과 같은 파일 및 등-클라이언트 쪽 리소스와 함께 합니다. 하지만 웹 응용 프로그램 데이터 기반 어떨까요? 데이터베이스를 사용 하는 웹 응용 프로그램을 배포 하는 추가 단계를 수행 해야?

다음 몇 가지 자습서를 통해 데이터 기반 웹 응용 프로그램을 배포 하는 데 필요한 단계를 다룰 것입니다. 이 자습서를 시작 하는 방법 데이터베이스의 스키마 및 콘텐츠 개발 환경에서 프로덕션 환경 이후 자습서에서 필요한 구성 변경 내용을 검색 하는 동안를 검사 하 여 시작 합니다. 다음 응용 프로그램 서비스 (멤버 자격, 역할, 프로필 및 등)를 사용 하는 데이터베이스를 배포 하는 문제를 살펴봅니다.

## <a name="examining-the-updated-book-reviews-web-application"></a>업데이트 된 책 검토 웹 응용 프로그램 검사

데이터 기반 웹 응용 프로그램을 배포를 보여 주기 위해 있습니까 ve 업데이트도 서 리뷰 웹 응용 프로그램을 간단 하 고 정적 웹 사이트에서 데이터를 기반으로 합니다. 이전에이 자습서가의 다운로드에 응용 프로그램의 두 가지 버전: 하나는 웹 응용 프로그램 프로젝트 모델 및 웹 사이트 프로젝트 모델을 사용 하는 하나를 사용 합니다.

업데이트 된도 서 리뷰 웹 응용 프로그램 사용을 [SQL Server 2008 Express Edition](https://www.microsoft.com/express/sql/default.aspx) s 사이트에 저장 된 데이터베이스 `App_Data` 폴더 (`~/App_Data/Reviews.mdf`). SQL Server 2008 컴퓨터에 설치 되어 있는 경우에 데모 오류 없이 실행 해야 합니다. 이전 버전의 경우 하거나 SQL Server 무료 SQL Server 2008 Express Edition을 설치 하거나이 자습서가 제공 되는 스크립트 다운로드 직접 데이터베이스를 만들 데이터베이스를 사용할 수 있습니다.

`Reviews.mdf` 데이터베이스 4 개의 테이블을 포함 합니다.

- `Genres` -비즈니스, 기술 및 Fiction, 등 각 장르에 대 한 레코드를 포함 합니다.
- `Books` -같은 열이 포함 된 각 검토에 대 한 레코드를 포함 `Title`, `GenreId`를 `ReviewDate`, 및 `Review`, 특히 합니다.
- `Authors` -검토 북에 기여한 각 작성자에 대 한 정보를 포함 합니다.
- `BooksAuthors` -어떤 작성자가 어떤 권의 책을 저술 하는 것을 지정 하는 다 대 다 조인 테이블이 있습니다.
  

그림 1에서는 이러한 네 가지 테이블의 ER 다이어그램을 보여 줍니다.


[![책 검토 웹 응용 프로그램의 데이터베이스는 네 가지 테이블의 구성](deploying-a-database-vb/_static/image2.jpg)](deploying-a-database-vb/_static/image1.jpg) 

**그림 1**: 책 검토 웹 응용 프로그램의 데이터베이스는 네 가지 테이블의 구성 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image3.jpg))


이전 버전도 서 리뷰 웹 사이트의 각 책에 대 한 별도 ASP.NET 페이지를 했습니다. 예를 들어 라는 페이지 했습니다 `~/Tech/TYASP35.aspx` 에 대 한 검토를 포함 하는 *가르치는 직접 ASP.NET 3.5 24 시간 동안에서*합니다. 웹 사이트의이 새 데이터 기반 버전에는 데이터베이스 및 Review.aspx?ID= 단일 ASP.NET 페이지에 저장 된 검토*bookId*, 지정 된 책에 대 한 검토를 표시 합니다. 마찬가지로, 있는지는 Genre.aspx?ID=*genreId* 지정 장르의 검토 책을 나열 하는 페이지입니다.

그림 2와 3 표시 합니다 `Genre.aspx` 및 `Review.aspx` 작업의 페이지입니다. 각 페이지에 대 한 주소 표시줄에 URL을 note 합니다. 그림 2 it s Genre.aspx? ID = 4-1123 85d164ba-c 47-82a0-c8ec75de7e0e 합니다. 85d164ba-1123-4c47-82a0-c8ec75de7e0e 이므로 `GenreId` 기술 장르, "기술 검토" s 페이지 머리글 읽기 및 글머리 기호 목록에 대 한 값이이 장르에 속하는 사이트에서 해당 검토를 열거 합니다.


[![기술 장르 페이지](deploying-a-database-vb/_static/image5.jpg)](deploying-a-database-vb/_static/image4.jpg) 

**그림 2**: The 기술 장르 페이지 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image6.jpg))


[![에 대 한 검토를 익힐 ASP.NET 3.5에서 24 시간](deploying-a-database-vb/_static/image8.jpg)](deploying-a-database-vb/_static/image7.jpg) 

**그림 3**:에 대 한 The 검토 *설명 직접 ASP.NET 3.5 24 시간 동안의* ([클릭 하 여 큰 이미지 보기](deploying-a-database-vb/_static/image9.jpg))


서평 웹 응용 프로그램에 있는 관리자 수 추가, 편집, 삭제 장르를 검토 하 고 정보를 작성 하는 관리 섹션도를 포함 됩니다. 현재 모든 방문자의 관리 섹션을 액세스할 수 있습니다. 이후 자습서에서 사용자 계정에 대 한 지원을 추가 하 고 관리 페이지에만 권한이 있는 사용자를 허용 했습니다.

다운로드 하는 경우도 서 리뷰 응용 프로그램 하세요의 용도 데이터 기반 응용 프로그램 배포를 설명 하는 것에 유의 합니다. 응용 프로그램 디자인에 관해서는 모범 사례는 발생 하지 않습니다. 예를 들어 방법이 없는 별도 DAL 데이터 액세스 계층 (); ASP.NET 페이지 SqlDataSource 컨트롤 또는 해당 코드 숨김 클래스의 ADO.NET 코드를 통해 데이터베이스와 직접 통신합니다. 계층화 된 아키텍처를 사용 하 여 데이터 기반 응용 프로그램 만들기에 대 한 자세한 설명, 참조 내 [ *데이터로 작업할* 자습서](../../data-access/index.md)합니다.

## <a name="databases-on-development-versus-production"></a>개발 및 프로덕션 데이터베이스

데이터 기반 웹 응용 프로그램 개발을 시작할 때 데이터베이스에 연결 하는 방법은 응용 프로그램 세부 정보를 제공 하는 데이터베이스 연결 문자열을 지정 해야 합니다. 다른 작업, 데이터베이스 서버, 데이터베이스 이름 및 보안 정보 간의이 연결 문자열 지정합니다. 대부분의 경우 개발 하는 동안 응용 프로그램에서 사용 하는 데이터베이스가 다른 데이터베이스를 사용 하는 경우이 프로덕션 환경에서 s입니다. 다른 데이터베이스를 사용 하 여 개발 및 프로덕션에 대 한 많은 이점이 있습니다. 안 개발에서 데이터베이스를 다른 것 실수로 수정 하거나 라이브 데이터를 삭제 하는 방법에 대 한 걱정 해야 합니다. 또한 더미 테스트 데이터에 배치 하거나 프로덕션에서 응용 프로그램에 미치는 영향에 걱정할 필요 없이 데이터 모델에 주요 변경 내용 확인 수 있습니다. S 데이터베이스 스키마를 가진 경우의 단점은 다른 데이터베이스 개발 및 프로덕션 환경에는 응용 프로그램은 배포 데이터베이스 및 모든 관련 변경 하거나 데이터를 배포 해야 합니다.

첫 번째 배포 하기 전에 데이터베이스의 인스턴스를 하나만 이며 인스턴스가 개발 환경에서 해당 합니다. 처음에 대 한 프로덕션 응용 프로그램을 배포 하는 경우에서는 해야 필요한 서버 쪽 및 클라이언트 쪽 파일을 복사 뿐만 아니라 프로덕션 환경으로 개발 환경에서 데이터베이스를 복사할 수도 합니다. 이 위치에서는 독립 오른쪽에 있는 데이터베이스도 서 리뷰 웹 응용 프로그램-를 사용 하 여 이제는 `App_Data` 개발 환경에서 폴더 되지 않은 하지만 아직 프로덕션 환경에 푸시 되었습니다.

응용 프로그램을 배포한 후 데이터베이스의 두 복사본이 설정 됩니다. 응용 프로그램을 완성 되어 감에 새로운 기능이 추가 될 수 있습니다, 데이터 모델에 대 한 변경 필요 (예: 기존 테이블에 새 열을 추가, 변경 기존 열에 새 테이블을 추가 및 등). 다음 웹 응용 프로그램을 배포 하면는 변경 내용이 적용 개발 환경에서 데이터베이스에 마지막 배포는 프로덕션 데이터베이스에 적용 되어야 합니다. 이 프로세스를 관리 하기 위한 몇 가지 전략은 이후 자습서에서 설명 됩니다. 이 자습서는 프로덕션 개발 환경에서 전체 데이터베이스를 배포 하는 방법에 중점을 둡니다.

## <a name="deploying-the-database-to-the-production-environment"></a>프로덕션 환경에 데이터베이스 배포

이 자습서의 나머지 부분에서는 개발 환경에서 데이터베이스를 프로덕션 환경에 배포 하는 방법에 살펴봅니다. 수에 따라 수행 하는 경우 웹 호스트 공급자를 사용 하 여 계정의 Microsoft SQL Server에 포함 되도록 데이터베이스 지원이 필요 합니다. 일부 정보가 있어야 당면한, 즉 데이터베이스 서버 이름, 데이터베이스 이름, 및는 사용자 이름 및 데이터베이스에 연결 하는 데 사용 되는 암호도 해야 합니다.

이 자습서의 앞부분에서 설명 했 듯이 서 리뷰 s 웹 사이트 데이터베이스가 저장 된 SQL Server 2008 Express Edition 데이터베이스는 `App_Data` 폴더입니다. 이러한 데이터베이스를 배포 합니다. 복사 만큼 간단한 것 이유를 눈에 띄는 것은 `App_Data` 개발 환경에서 프로덕션 환경으로 폴더입니다. 그러나 대부분의 웹 호스트 공급자 호스팅 데이터베이스에서 지원 하지 않습니다는 `App_Data` 보안상의 이유로 폴더입니다. 대신 웹 호스트는 해당 환경 내에서 SQL Server 데이터베이스 서버에 계정을 제공합니다. 개발 환경에서 프로덕션 환경에 데이터베이스 배포를 위해서는 웹 호스트의 데이터베이스 서버에 등록 된 데이터베이스입니다.

그렇다면 어떻게 합니까 데이터베이스 개발 환경에서 프로덕션 환경으로? 웹 호스트 제품 서비스에 따라이 작업을 수행 하는 방법은 몇 가지가 있습니다. DiscountASP.NET와 같은 일부 호스트를 사용 하 여 데이터베이스의 실제 백업 FTP 수 `.mdf` 웹 사이트에 파일 및 그런 다음 제어판에서 백업 파일을 복원 또는 연결 된 `.mdf` 파일을 SQL Server 데이터베이스 서버입니다. 이러한 도구를 사용 하 여 데이터베이스를 배포 하기만 하면 됩니다 복사는 `App_Data` 프로덕션 환경 폴더 제어판을 통해 연결 합니다. 이것이 아마도 처음으로 데이터베이스를 게시할 쉽고 빠른 방법입니다.

다른 방법은 데이터베이스 게시 마법사를 사용 하는 것입니다. 데이터베이스 게시 마법사는 해당 테이블의 데이터베이스의 스키마에서 테이블, 저장된 프로시저, 뷰, 사용자 정의 함수 및 등-및 필요에 따라 데이터를 만들려면 SQL 명령을 생성 하는 Windows 데스크톱 응용 프로그램입니다. 다음 SQL Server Management Studio를 통해 웹 호스트 공급자가의 데이터베이스 서버에 연결 하 고 프로덕션 데이터베이스를 복제 하려면이 스크립트를 실행할 수 있습니다. 웹 호스트 공급자에는 Microsoft가 지 원하는 경우 향상도 [Database Publishing Services](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home) 귀하를 대신해 데이터베이스 서버에 자동으로 실행 되는 데이터베이스 게시 마법사에서 생성 된 스크립트를 할 수 있습니다. 데이터베이스 게시 마법사에서는 s 데이터베이스 스키마 및 데이터를 만드는 스크립트를 생성 하므로 웹 호스트 공급자는 업로드 된 연결과 같은 기능을 제공 하는 여부에 관계 없이 작동 하는지 `.mdf` 파일입니다.

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>데이터베이스 스키마 및 데이터베이스 게시 마법사를 사용 하 여 데이터를 만드는 SQL 명령 생성

데이터베이스 게시 마법사를 사용 하 여 프로덕션에도 서 리뷰 데이터베이스 배포를 안내 하는 s 수 있습니다. Visual Studio 2008을 사용 하는 경우 그 이후에 데이터베이스 게시 마법사를 이미 설치 되어 있습니다. Visual Studio 2005를 사용 하는 경우 첫 번째 해야 [다운로드 및 설치](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en) 마법사.

Visual Studio를 열고 이동할는 `Reviews.mdf` 데이터베이스입니다. Visual Web Developer를 사용 하는 경우 데이터베이스 탐색기;로 이동 Visual Studio를 사용 하는 경우 서버 탐색기를 사용 합니다. 그림 4는 `Reviews.mdf` Visual Web Developer에서 데이터베이스 탐색기에서 데이터베이스입니다. 그림 4에서 알 수 있듯이는 `Reviews.mdf` 데이터베이스 4 개의 테이블, 3 개의 저장된 프로시저 및 사용자 정의 함수를 이루어집니다.


[![데이터베이스 탐색기 또는 서버 탐색기에서 데이터베이스를 찾아](deploying-a-database-vb/_static/image11.jpg)](deploying-a-database-vb/_static/image10.jpg) 

**그림 4**: 데이터베이스 탐색기 또는 서버 탐색기에서 데이터베이스를 찾아 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image12.jpg))


데이터베이스 이름을 마우스 오른쪽 상황에 맞는 메뉴에서 "공급자에 게시" 옵션을 선택 합니다. 데이터베이스 게시 마법사가 시작 됩니다 (그림 5 참조). 시작 화면을 지 나 고급을 클릭 합니다.


[![데이터베이스 게시 마법사 시작 화면](deploying-a-database-vb/_static/image14.jpg)](deploying-a-database-vb/_static/image13.jpg) 

**그림 5**: The 데이터베이스 게시 마법사 시작 화면 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image15.jpg))


마법사에서 두 번째 화면 데이터베이스 게시 마법사에 액세스할 수 있는 데이터베이스를 나열 하 고 선택한 데이터베이스의 모든 개체 스크립팅 또는 스크립팅할 개체 선택 여부를 선택할 수 있습니다. 적절 한 데이터베이스를 선택 하 고 "모든 스크립트는 선택한 데이터베이스에서 개체" 옵션을 선택한 상태로 둡니다.

> [!NOTE]
> 오류가 발생 하는 경우 "데이터베이스에 개체가 없는 *databaseName* 이 마법사에서 스크립팅 가능한 형식" 그림 6에 표시 된 화면에서 다음을 클릭 하는 경우에 데이터베이스 파일의 경로를 지나치게 긴 없습니다 인지 확인 합니다. 설명 했 듯이 [토론 항목](http://www.codeplex.com/sqlhost/Thread/View.aspx?ThreadId=11014) 데이터베이스 게시 마법사 프로젝트 페이지에서 데이터베이스 파일 경로가 너무 긴 경우이 오류가 발생할 수 있습니다.


[![데이터베이스 게시 마법사 시작 화면](deploying-a-database-vb/_static/image17.jpg)](deploying-a-database-vb/_static/image16.jpg) 

**그림 6**: The 데이터베이스 게시 마법사 시작 화면 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image18.jpg))


다음 화면에서 스크립트 파일 생성을 하거나 수 웹 호스트가 지 원하는 경우 웹 호스트 공급자가의 데이터베이스 서버에 직접 데이터베이스를 게시 합니다. 그림 7에서 알 수 있듯이, 있음 파일에 작성 된 스크립트 `C:\REVIEWS.MDF.sql`합니다.


[![데이터베이스를 파일에 스크립트 또는 사용자 웹 호스트 공급자에 게 직접 게시](deploying-a-database-vb/_static/image20.jpg)](deploying-a-database-vb/_static/image19.jpg) 

**그림 7**: 데이터베이스를 파일에 스크립트 또는 해당 웹 호스트 공급자에 직접 게시할 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image21.jpg))


후속 화면 다양 한 스크립팅 옵션에 대 한 라는 메시지를 표시 합니다. 스크립트에서 이러한 기존 개체를 제거 하려면 drop 문을 포함할지 여부를 지정할 수 있습니다. 이 기본값은 True로 되어 있는데 처음으로 데이터베이스를 배포 하는 경우입니다. SQL Server 2000, SQL Server 2005 또는 SQL Server 2008 데이터베이스에서 대상 데이터베이스로 인지 여부를 지정할 수 있습니다. 마지막으로, 스키마 및 데이터를 스크립팅할 지 여부를 지정할 수 있습니다는 데이터만 또는 스키마만 합니다. 스키마는 데이터베이스 개체, 테이블, 저장된 프로시저, 뷰 및 등의 컬렉션입니다. 데이터는 테이블에 있는 정보입니다.

그림 8에서 알 수 있듯이, I ve SQL Server 2008 데이터베이스에 대 한 스크립트를 생성 하 고 스키마와 데이터를 게시 하려면 기존 데이터베이스 개체를 삭제 하려면 구성 마법사를 가져왔습니다.


[![지정 된 게시 옵션](deploying-a-database-vb/_static/image23.jpg)](deploying-a-database-vb/_static/image22.jpg) 

**그림 8**: 게시 옵션 지정 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image24.jpg))


마지막 두 개의 화면 요약 작업을 수행 하 고 다음 스크립트의 상태를 표시 하려고 합니다. 마법사를 실행 결과 프로덕션에서 데이터베이스를 만들고 개발에서와 동일한 데이터를 입력 하는 데 필요한 SQL 명령이 포함 된 스크립트 파일을 하는 것입니다.

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>프로덕션 환경 데이터베이스에서 SQL 명령 실행

이제 남아 있는 데이터베이스 및 해당 데이터를 만드는 SQL 명령이 포함 된 스크립트를 프로덕션 데이터베이스에서 스크립트를 실행 합니다. 일부 웹 호스트 공급자가 제어판의 데이터베이스에서 실행할 SQL 명령을 입력할 수 있는 텍스트 상자를 제공 합니다. 매우 큰 스크립트 파일이 있는 경우이 옵션이 작동 하지 않을 수 있습니다 (의 `REVIEWS.MDF.sql` 스크립트 파일은 크기가 425 KB 개 예를 들어).

SQL Server Management Studio (SSMS)를 사용 하 여 프로덕션 데이터베이스 서버에 직접 연결 하는 것이 좋습니다. 비-Express Edition의 SQL Server 컴퓨터에 설치 되어 있는 경우 다음 있을 가능성이 높습니다 이미 SSMS를 설치 합니다. 수이 고, 그렇지 [다운로드 및 설치](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) SQL Server Management Studio Express Edition의 무료 버전입니다.

SSMS를 시작 하 고 웹 호스트 공급자가 제공한 정보를 사용 하 여 웹 호스트의 데이터베이스 서버에 연결 합니다.


[![웹 호스트 공급자가의 데이터베이스 서버에 연결](deploying-a-database-vb/_static/image26.jpg)](deploying-a-database-vb/_static/image25.jpg) 

**그림 9**: 해당 웹 호스트 공급자가의 데이터베이스 서버에 연결 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image27.jpg))


데이터베이스 탭을 확장 하 고 데이터베이스를 찾습니다. 도구 모음의 왼쪽된 위 모퉁이에 있는 새 쿼리 단추를 클릭 하 고 데이터베이스 게시 마법사에서 만든 스크립트 파일에서 SQL 명령에 붙여 넣습니다 프로덕션 데이터베이스 서버에서 다음이 명령을 실행 하려면 실행 단추를 클릭 합니다. 스크립트 파일은 특히 큰 명령을 실행 하는 데 몇 분 정도 걸릴 수 있습니다.


[![웹 호스트 공급자가의 데이터베이스 서버에 연결](deploying-a-database-vb/_static/image29.jpg)](deploying-a-database-vb/_static/image28.jpg) 

**그림 10**: 해당 웹 호스트 공급자가의 데이터베이스 서버에 연결 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image30.jpg))


S 모두 완료 되었습니다! 이 시점에서 개발 데이터베이스를 프로덕션 중복 되었습니다. SSMS에서 데이터베이스를 새로 고치는 경우 새 데이터베이스 개체가 표시 됩니다. 그림 11에는 프로덕션 데이터베이스의 테이블, 저장된 프로시저 및 개발 데이터베이스의 미러는 사용자 정의 함수를 보여 줍니다. 및 프로덕션 데이터베이스의 테이블 마법사 실행 된 시간 개발 데이터베이스 s 테이블과 동일한 데이터에 있으므로 데이터를 게시할 데이터베이스 게시 마법사에 지시 했습니다. 데이터를 표시 하는 그림 12는 `Books` 프로덕션 데이터베이스에서 테이블입니다.


[![프로덕션 데이터베이스에서 중복 된 데이터베이스 개체](deploying-a-database-vb/_static/image32.jpg)](deploying-a-database-vb/_static/image31.jpg) 

**그림 11**:의 데이터베이스 개체는 복제 된 프로덕션 데이터베이스에서 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image33.jpg))


[![프로덕션 데이터베이스 개발 데이터베이스와 동일한 데이터를 포함합니다.](deploying-a-database-vb/_static/image35.jpg)](deploying-a-database-vb/_static/image34.jpg) 

**그림 12**: 개발 데이터베이스에서 동일한 데이터를 포함 하는 프로덕션 데이터베이스 ([큰 이미지를 보려면 클릭](deploying-a-database-vb/_static/image36.jpg))


이 시점에서 프로덕션 환경에 개발 데이터베이스를 배포만 했습니다. 아직 웹 응용 프로그램 자체 배포 살펴보았습니다 중이거나 응용 프로그램을 프로덕션에서 프로덕션 데이터베이스를 사용 하는 데 필요한 구성 변경 내용을 검사 했습니다. 여기서 다음 자습서에서 이러한 문제를 살펴보겠습니다.

## <a name="summary"></a>요약

데이터 기반 웹 응용 프로그램 배포 프로덕션 환경으로 개발 하는 동안 사용 된 데이터베이스를 복사 해야 합니다. 대부분의 웹 호스트 공급자는 데이터베이스를 배포 하는 과정을 간소화 하기 위한 도구를 제공 합니다. 예를 들어 DiscountASP.NET를 사용 하 여 있습니다 수 FTP 데이터베이스 `.mdf` 파일 (또는 백업) 한 다음 제어판에서 데이터베이스 서버에 데이터베이스를 연결 합니다. 웹 호스트 공급자 제품 개발 데이터베이스의 스키마 및 데이터를 만드는 SQL 명령에 대 한 스크립트를 생성 하는 Microsoft의 데이터베이스 게시 마법사 도구는 기능에 관계 없이 작동 하는 방법도 있습니다. 이 스크립트를 생성 한 후에 프로덕션 데이터베이스에서 실행할 수 있습니다.

이제도 서 리뷰 웹 응용 프로그램 s 데이터베이스가 프로덕션에서 응용 프로그램을 배포할 수 했습니다. 그러나 웹 응용 프로그램의 구성 정보를 데이터베이스에 연결 문자열을 지정 하 고 해당 연결 문자열 개발 데이터베이스를 참조 합니다. 프로덕션 사이트를 배포 하는 경우이 연결 문자열 정보를 업데이트 해야 합니다. 다음 자습서는 이러한 구성 차이 살펴봅니다 하 고 프로덕션에도 서 리뷰 데이터 기반 사이트를 게시 하는 데 필요한 단계를 안내 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Microsoft SQL Server 데이터베이스 게시 마법사 1.1 다운로드](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [Microsoft SQL Server Management Studio Express Edition 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

> [!div class="step-by-step"]
> [이전](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
> [다음](configuring-the-production-web-application-to-use-the-production-database-vb.md)
