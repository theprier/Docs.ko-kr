---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
title: 파일 (C#)를 업로드 하는 중 | Microsoft Docs
author: rick-anderson
description: '서버의 파일 시스템에 저장 될 수 있는 웹 사이트 (예: Word 또는 PDF 문서) 이진 파일을 업로드 하는 사용자가 허용 하는 방법 알아보기...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: b381b1da-feb3-4776-bc1b-75db53eb90ab
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
msc.type: authoredcontent
ms.openlocfilehash: 3c758e94311817d01b17d27083733f805caf600f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="uploading-files-c"></a>업로드 파일 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_CS.exe) 또는 [PDF 다운로드](uploading-files-cs/_static/datatutorial54cs1.pdf)

> 서버의 파일 시스템 또는 데이터베이스에 저장 될 수 있는 웹 사이트에 이진 파일 (예: Word 또는 PDF 문서)를 업로드 하는 사용자가 허용 하는 방법에 알아봅니다.


## <a name="introduction"></a>소개

이 자습서의 모든 우리 텍스트 데이터로 작업 하는 지금까지 검사 했습니다. 그러나 대부분의 응용 프로그램 텍스트와 이진 데이터를 캡처하는 데이터 모델은 다릅니다. 온라인 데이트 사이트 사용자가 사진을 업로드 하 여 해당 프로필과 연결할 수를 통합할 수 있습니다. 채용 웹 사이트는 Microsoft Word 또는 PDF 문서로 경력을 업로드 하는 사용자가 할당할 수도 있습니다.

이진 데이터 작업을 추가 새 부담감이 상당한 일련의 합니다. 응용 프로그램에 이진 데이터가 저장 되는 방법을 결정 해야 합니다. 새 레코드를 삽입 하는 데 사용 되는 인터페이스에 사용자가 자신의 컴퓨터에서 파일을 업로드 하도록 허용 하도록 업데이트 되어야 하 고 추가 단계를 수행 하 여 표시 하거나 연결 된 이진 데이터를 레코드 s 다운로드 하기 위한 수단을 제공 해야 합니다. 다음 세 개와이 자습서에서 이러한 과제 hurdle 하는 방법을 살펴보겠습니다. 이 자습서의 끝에 합니다 빌드 했습니다 그림 및 PDF 브로슈어 각 범주와 연결 하는 모든 기능을 갖춘 응용 프로그램입니다. 특정이 자습서에서는 이진 데이터를 저장 하기 위한 다양 한 기술을 살펴볼을 사용자가 자신의 컴퓨터에서 파일을 업로드할 수 있도록 하는 방법을 탐색 합니다 고 웹 서버의 파일 시스템에 저장 했습니다.

> [!NOTE]
> 이진 데이터를 응용 프로그램 s 데이터 모델의 일부인 경우에 따라 라고는 [BLOB](http://en.wikipedia.org/wiki/Binary_large_object), Binary Large OBject에 대 한 약어입니다. 이 자습서에 용어 BLOB 동의어입니다. 하지만 용어 이진 데이터를 사용 하도록 선택 했습니다 I.


## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>1 단계: 웹 페이지 이진 데이터와 작업 만들기

이진 데이터에 대 한 지원을 추가와 관련 된 과제 탐색을 시작 하기 전에 s를 먼저 잠시이 자습서와 다음 3에 대 한 사용 해야 하는 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `BinaryData`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`


![이진 데이터와 관련 된 자습서에 대 한 ASP.NET 페이지 추가](uploading-files-cs/_static/image1.gif)

**그림 1**: 이진 데이터와 관련 된 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `BinaryData` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](uploading-files-cs/_static/image2.gif)](uploading-files-cs/_static/image1.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image2.png))


마지막으로, 이러한 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, 확장 된 후 다음 태그를 추가 GridView `<siteMapNode>`:


[!code-xml[Main](uploading-files-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 이제는 왼쪽 메뉴에서 이진 데이터 자습서 사용에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 자습서 이진 데이터 사용에 대 한 항목을 포함](uploading-files-cs/_static/image3.gif)

**그림 3**: 이제 사이트 맵 자습서 이진 데이터 사용에 대 한 항목을 포함


## <a name="step-2-deciding-where-to-store-the-binary-data"></a>2 단계: 이진 데이터를 저장할 위치를 결정

두 위치 중 하나에 응용 프로그램의 데이터 모델과 연관 된 이진 데이터를 저장할 수:; 데이터베이스에 저장 된 파일에 대 한 참조로 웹 서버의 파일 시스템에 또는 데이터베이스 자체 내에서 직접 (그림 4 참조). 각 접근 마다 고유한 장점 및 단점 및 자세한 토론을 받아들입니다.


[![데이터베이스에서 직접 또는 파일 시스템에 이진 데이터를 저장할 수 있습니다.](uploading-files-cs/_static/image4.gif)](uploading-files-cs/_static/image3.png)

**그림 4**: 데이터베이스에서 직접 또는 파일 시스템에 이진 데이터를 저장할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image4.png))


각 제품 사진을 연결 Northwind 데이터베이스를 확장 하 려 한다고 가정 합니다. 웹 서버의 파일 시스템에 이러한 이미지 파일을 저장 하 고에 포함 된 경로 기록할 수 있습니다는 `Products` 테이블입니다. 이 접근 방식 d 추가 `ImagePath` 열에는 `Products` 형식의 테이블을 `varchar(200)`, 아마도 합니다. 추가한 사용자 그림 chai을 업로드 시 웹 서버의 파일 시스템에 저장 될 수 `~/Images/Tea.jpg`여기서 `~` 응용 프로그램 s 실제 경로 나타냅니다. 즉, 웹 사이트 실제 경로에서 시작 하는 경우 `C:\Websites\Northwind\`, `~/Images/Tea.jpg` 에 해당 `C:\Websites\Northwind\Images\Tea.jpg`합니다. 이미지 파일을 업로드 한 후 d 업데이트의 Chai 레코드는 `Products` 테이블 되도록 해당 `ImagePath` 열 참조 되는 새 이미지의 경로입니다. 사용 하 여 `~/Images/Tea.jpg` 또는 그냥 `Tea.jpg` 하기로 결정는 모든 제품 이미지 응용 프로그램 s에 배치할 경우 `Images` 폴더입니다.

파일 시스템에 이진 데이터를 저장할 경우의 주요 이점은 다음과 같습니다.

- **구현의 용이성** 곧 볼 수 있겠지만, 저장 하 고 데이터베이스 내에 직접 저장 된 이진 데이터 검색 때 파일 시스템을 통해 데이터를 사용할 때 보다 더 복잡 한 코드를 포함 합니다. 또한 사용자는 보거나 이진 데이터를 다운로드 하는 순서 대로 이러한 제공 해야 해당 데이터에 대 한 URL입니다. 데이터와 웹 서버의 파일 시스템에 있는 경우 URL은 간단 합니다. 그러나 데이터는 데이터베이스에 저장 됩니다 웹 페이지로 이동해 요구에 따라 만들 수를 검색 하 고 데이터베이스에서 데이터를 반환 합니다.
- **이진 데이터에 대 한 광범위 한 액세스** 이진 데이터는 다른 서비스 또는 응용 프로그램 데이터베이스에서 데이터를 끌어올 수 없습니다는 액세스할 수 있도록 할 수 있습니다. 예를 들어 각 제품와 관련 된 이미지도 해야 통해 사용자에 게 사용할 수 [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol),이 경우 d 하려는 파일 시스템에 이진 데이터를 저장 합니다.
- **성능** 이진 데이터는 파일 시스템에 저장 되 면 데이터베이스 서버와 웹 서버 간에 요청 및 네트워크 정체 됩니다 이진 데이터는 데이터베이스 내에 직접 저장 하는 경우 보다 작습니다.

파일 시스템에 이진 데이터를 저장할 경우의 주요 단점은 데이터베이스에서 데이터를 구분할입니다. 레코드가 삭제 되는 `Products` 테이블, 웹 서버의 파일 시스템에 연결된 된 파일을 자동으로 삭제 되지 않습니다. 파일 또는 파일 시스템을 삭제 하려면 추가 코드가 사용 되지 않는 분리 된 파일을 사용 쌓이게 됩니다 작성 해야 합니다. 또한 데이터베이스를 백업 하는 경우 항상 해야는 파일 시스템에 연결 된 이진 데이터의 백업 하십시오. 데이터베이스를 다른 사이트 또는 서버 동작 하는 문제를 이동 합니다.

형식의 열을 만들어 Microsoft SQL Server 2005 데이터베이스에 직접 이진 데이터에 저장할 있습니다는 또는 `varbinary`합니다. 마찬가지로 다른 가변 길이 데이터 형식으로 저장할 수 있는 이진 데이터의 최대 길이이 열에 지정할 수 있습니다. 예를 들어 최대을 예약 하 고 5, 000 바이트 사용 `varbinary(5000)`; `varbinary(MAX)` 약 2GB 최대 저장소 크기에 대 한 허용 합니다.

데이터베이스에서 직접 이진 데이터를 저장할 경우의 주요 장점은 이진 데이터와 데이터베이스 레코드 간의 긴밀 하 게 결합 됩니다. 이 백업 또는 다른 사이트 또는 서버에 데이터베이스를 이동 하는 등의 데이터베이스 관리 작업을 크게 단순화 합니다. 또한 자동으로 레코드를 삭제 하면 해당 이진 데이터를 삭제 합니다. 데이터베이스의 이진 데이터를 저장할 경우의 많은 미묘한 혜택도 있습니다. 참조 [저장 이진 파일 직접 데이터베이스를 사용 하 여 ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx) 에 대 한 자세한 내용은 합니다.

> [!NOTE]
> Microsoft SQL Server 2000 및 이전 버전의 `varbinary` 데이터 형식에 최대 제한인 8, 000 바이트입니다. 최대 2GB의 이진 데이터를 저장 하는 [ `image` 데이터 형식](https://msdn.microsoft.com/library/ms187993.aspx) 를 대신 사용 해야 합니다. 그러나 추가 하 여 `MAX` SQL Server 2005에서는는 `image` 데이터 형식이 사용 되지 않습니다. 그 s 계속 지원에 대 한 이전 버전과 호환성을 되지만 Microsoft를 발표 했습니다는 `image` 데이터 형식은 나중 버전의 SQL Server에서 제거 됩니다.


이전 데이터 모델을 사용 하 여 작업할 경우 발생할 수 있습니다는 `image` 데이터 형식입니다. Northwind 데이터베이스 s `Categories` 테이블에는 `Picture` 범주에 대 한 이미지 파일의 이진 데이터를 저장 하기 위해 사용할 수 있는 열입니다. Northwind 데이터베이스에 Microsoft Access 및 이전 버전의 SQL Server에 있으므로이 열이 유형이 `image`합니다.

이 자습서 및 다음 세 가지 방법을 모두 사용 합니다. `Categories` 테이블에는 `Picture` 범주에 대 한 이미지의 이진 콘텐츠를 저장 하기 위한 열입니다. 추가 열을 추가 하겠습니다 `BrochurePath`, 경로 PDF 범주의 인쇄 품질, 세련 된 개요를 제공 하는 데 사용할 수 있는 웹 서버의 파일 시스템에 저장할 수 있습니다.

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>3 단계: 추가 된`BrochurePath`열에는`Categories`테이블

현재 Categories 테이블에 4 개의 열: `CategoryID`, `CategoryName`, `Description`, 및 `Picture`합니다. 이러한 필드 이외에 가리킵니다 범주의 브로슈어 (있는 경우) 하는 새 계정을 추가 해야 합니다. 이 열을 추가 하려면 마우스 오른쪽 단추로 클릭 하려면 서버 탐색기에서 드릴 다운 테이블로 이동는 `Categories` 테이블 및 테이블 정의 열기 (그림 5 참조). 서버 탐색기에 표시 되지 않으면 보기 메뉴에서 서버 탐색기 옵션을 선택 하 여 표시 하거나 Ctrl + Alt + S를 적중 합니다.

새로 추가 `varchar(200)` 열에는 `Categories` 라는 테이블을 `BrochurePath` 알리고 `NULL` s 및 저장 아이콘을 클릭 (또는 Ctrl + S를 적중).


[![Categories 테이블에 BrochurePath 열 추가](uploading-files-cs/_static/image5.gif)](uploading-files-cs/_static/image5.png)

**그림 5**: 추가 된 `BrochurePath` 열에는 `Categories` 테이블 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image6.png))


## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>4 단계: 사용할 아키텍처를 업데이트 하는`Picture`및`BrochurePath`열

`CategoriesDataTable` 데이터 액세스 계층 (DAL)에서 현재에 네 개의 `DataColumn` 정의 s: `CategoryID`, `CategoryName`, `Description`, 및 `NumberOfProducts`합니다. 이 DataTable에를 원래 설계 했습니다는 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-cs.md) 자습서는 `CategoriesDataTable` 만으로는 처음 3 개의 열, `NumberOfProducts` 열에서 추가 되었습니다는 [마스터/세부 정보는 글머리 기호를 사용 하 여 세부 정보 사용 마스터 레코드 목록](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 자습서입니다.

에 설명 된 대로 *데이터 액세스 계층을 만들려면*, 형식의 DataSet에 Datatable 비즈니스 개체를 확인 합니다. Tableadapter는 데이터베이스와 통신 하 고 쿼리 결과 함께 비즈니스 개체를 채우기 위해 합니다. `CategoriesDataTable` 채워집니다는 `CategoriesTableAdapter`, 세 가지 데이터 검색 방법을:

- `GetCategories()` TableAdapter s 주 쿼리를 실행 하 고 반환 된 `CategoryID`, `CategoryName`, 및 `Description` 의 모든 레코드의 필드는 `Categories` 테이블입니다. 주 쿼리에서 사용 하는 것은 자동으로 생성 하 여 `Insert` 및 `Update` 메서드.
- `GetCategoryByCategoryID(categoryID)` 반환는 `CategoryID`, `CategoryName`, 및 `Description` 범주 필드를 `CategoryID` equals *categoryID*합니다.
- `GetCategoriesAndNumberOfProducts()` -반환 된 `CategoryID`, `CategoryName`, 및 `Description` 의 모든 레코드에 대 한 필드는 `Categories` 테이블입니다. 또한 각 범주와 관련 된 제품의 수를 반환 하는 하위 쿼리를 사용 합니다.

아무것도 반환을 쿼리 하는 알림은 `Categories` 테이블 s `Picture` 또는 `BrochurePath` 열; 없으며는 `CategoriesDataTable` 제공 `DataColumn` 이러한 필드에 대 한 합니다. 그림에서 사용 하려면 및 `BrochurePath` 속성을 먼저 추가 해야 하도록는 `CategoriesDataTable` 한 다음 업데이트는 `CategoriesTableAdapter` 이러한 열을 반환 하는 클래스입니다.

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>추가`Picture`및`BrochurePath``DataColumn` s

이러한 두 열을 추가 하 여 시작 된 `CategoriesDataTable`합니다. 마우스 오른쪽 단추로 클릭는 `CategoriesDataTable`의 헤더 상황에 맞는 메뉴에서 추가 선택한 다음 열 옵션을 선택 합니다. 이렇게 하면 새 만들어집니다 `DataColumn` 라는 DataTable의 `Column1`합니다. 이 열을 이름 바꾸기 `Picture`합니다. 속성 창에서 설정 된 `DataColumn` s `DataType` 속성을 `System.Byte[]` (이 드롭다운 목록에서 옵션)에 직접 입력 해야 합니다.


[![데이터 형식을 갖는 System.Byte DataColumn 라는 그림 만들기](uploading-files-cs/_static/image6.gif)](uploading-files-cs/_static/image7.png)

**그림 6**: 만들기는 `DataColumn` 명명 된 `Picture` 인 `DataType` 은 `System.Byte[]` ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image8.png))


다른 항목 추가 `DataColumn` 의 DataTable에 이름을 지정 하 고 `BrochurePath` 기본값을 사용 하 여 `DataType` 값 (`System.String`).

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>반환 된`Picture`및`BrochurePath`TableAdapter의 값

이 두와 `DataColumn` s에 추가 `CategoriesDataTable`, 업데이트 하는 준비 된 것은 `CategoriesTableAdapter`합니다. 가 두 주 TableAdapter 쿼리에서 반환 된 열 값을 하지만이 데이터 다시 가져오기는 이진 될 때마다는 `GetCategories()` 메서드가 호출 되었습니다. Let s 돌아가려고 주 TableAdapter 쿼리를 업데이트 하는 대신, `BrochurePath` 특정 범주의 s를 반환 하는 추가 데이터 검색 메서드를 만들고 `Picture` 열입니다.

주 TableAdapter 쿼리를 업데이트 하려면 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 하 고 상황에 맞는 메뉴에서 구성 옵션을 선택 합니다. 우리는 테이블 어댑터 구성 마법사가 표시 지난 자습서의 숫자에 표시 했습니다. 업데이트 다시 상태로 전환 하려면 쿼리는 `BrochurePath` 하 고 마침을 클릭 합니다.


[![또한 BrochurePath를 반환 하는 SELECT 문에서 열 목록 업데이트](uploading-files-cs/_static/image7.gif)](uploading-files-cs/_static/image9.png)

**그림 7**:의 열 목록도 업데이트는 `SELECT` 문 실행도 `BrochurePath` ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image10.png))


TableAdapter에 대 한 임시 SQL 문이 사용할 경우 기본 쿼리에 열 목록을 업데이트 하는 모든에 대 한 열 목록을 업데이트는 `SELECT` 쿼리는 TableAdapter의 메서드. 즉,는 `GetCategoryByCategoryID(categoryID)` 메서드 반환 하도록 업데이트 되었습니다는 `BrochurePath` 열-의도 한 기능을 수 있습니다. 그러나 열 목록에도 업데이트는 `GetCategoriesAndNumberOfProducts()` 메서드를 각 범주에 대 한 제품 개수를 반환 하는 하위 쿼리! 따라서이 메서드는 s를 업데이트 해야 `SELECT` 쿼리 합니다. 마우스 오른쪽 단추로 클릭는 `GetCategoriesAndNumberOfProducts()` 메서드를 구성을 선택 하 고 되돌릴는 `SELECT` 원래 값으로 다시 쿼리 합니다.


[!code-sql[Main](uploading-files-cs/samples/sample2.sql)]

다음으로, 특정 범주의 s를 반환 하는 새 TableAdapter 메서드를 만들 `Picture` 열 값입니다. 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 TableAdapter 쿼리 구성 마법사를 시작 하려면 추가 쿼리 옵션을 선택 합니다. 이 마법사의 첫 번째 단계는 임시 SQL 문을 사용 하 여 데이터를 쿼리 하기 원하는 경우 새 저장 프로시저 또는 기존 us를 요청 합니다. SQL 문 사용을 선택 하 고 클릭 합니다. 에서는 행 ' 돌아가지, 하므로 행 옵션의 두 번째 단계에서 반환 하는 SELECT를 선택 합니다.


[![사용 하 여 SQL 문을 옵션을 선택 합니다.](uploading-files-cs/_static/image8.gif)](uploading-files-cs/_static/image11.png)

**그림 8**: 사용 하 여 SQL 문 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image12.png))


[![선택 행을 반환 하는 SELECT 쿼리는 Categories 테이블에서 레코드를 반환 하 고, 이후](uploading-files-cs/_static/image9.gif)](uploading-files-cs/_static/image13.png)

**그림 9**: 쿼리는 행을 반환 합니다 선택 선택 Categories 테이블에서 레코드를 반환 하므로 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image14.png))


3 단계에서 다음 SQL 쿼리를 입력 하 고 클릭 합니다.


[!code-sql[Main](uploading-files-cs/samples/sample3.sql)]

새 메서드에 대 한 이름을 선택 하는 마지막 단계가입니다. 사용 하 여 `FillCategoryWithBinaryDataByCategoryID` 및 `GetCategoryWithBinaryDataByCategoryID` 채우기 DataTable 및 반환 DataTable 패턴, 각각. 마법사를 완료 하려면 마침을 클릭 합니다.


[![TableAdapter의 방법에 대 한 이름을 선택합니다](uploading-files-cs/_static/image10.gif)](uploading-files-cs/_static/image15.png)

**그림 10**: TableAdapter의 방법에 대 한 이름을 선택 합니다 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image16.png))


> [!NOTE]
> 테이블 어댑터 쿼리 구성 마법사를 완료 한 후 새 명령 텍스트 반환 하는지 스키마와 데이터는 주 쿼리의 스키마와에서 다른 알리는 대화 상자가 표시 될 수 있습니다. 즉, 마법사는 것을 확인 하는 TableAdapter s 주 쿼리에서 `GetCategories()` 방금 만든 아닌 다른 스키마를 반환 합니다. 하지만이 원하는 이므로이 메시지를 무시할 수 있습니다.


또한 염두에서에 둬야는 임시 SQL 문을 사용 하는 마법사를 사용 하 여 시간에는 나중에 TableAdapter s 주 쿼리를 변경 하는 경우 수정 됩니다는 `GetCategoryWithBinaryDataByCategoryID` s 메서드에 `SELECT`의 문 열 목록에서 해당 열을 포함 하는 주 쿼리 (즉, 제거 됩니다는 `Picture` 쿼리에서 열)입니다. 반환할 열 목록을 수동으로 업데이트 해야 합니다는 `Picture` 와 했던 집합과 유사한은 `GetCategoriesAndNumberOfProducts()` 이 단계에서 메서드.

두를 추가한 후 `DataColumn` s는 `CategoriesDataTable` 및 `GetCategoryWithBinaryDataByCategoryID` 메서드를는 `CategoriesTableAdapter`, 그림 11에서 스크린 샷 같이 형식화 된 데이터 집합 디자이너에서 이러한 클래스에 표시 됩니다.


![데이터 집합 디자이너에 새 열과 메서드](uploading-files-cs/_static/image11.gif)

**그림 11**: 데이터 집합 디자이너에 새 열과 메서드


## <a name="updating-the-business-logic-layer-bll"></a>비즈니스 논리 계층 BLL ()를 업데이트합니다.

DAL 업데이트와 이제 남은 것은 BLL 비즈니스 논리 계층 ()에서 새 메서드를 포함 하도록 확장할 수 `CategoriesTableAdapter` 메서드. 다음 메서드를 추가 `CategoriesBLL` 클래스:


[!code-csharp[Main](uploading-files-cs/samples/sample4.cs)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>웹 서버에 클라이언트에서 파일을 업로드 하는 5 단계:

종종 이진 데이터를 수집 하려는 경우이 데이터는 최종 사용자가 제공 됩니다. 이 정보를 캡처하려면 사용자를 웹 서버에 컴퓨터의 파일을 업로드할 수 있도록 해야 합니다. 업로드 된 데이터는 다음을 의미할 수 있습니다. 파일을 웹 서버의 파일 시스템 및 데이터베이스의 파일 경로 추가 또는 데이터베이스에 직접 이진 콘텐츠를 쓰기 저장 데이터 모델에 통합할 수 있어야 합니다. 이 단계에서는 사용자가 자신의 컴퓨터에서 서버에 파일을 업로드 하도록 허용 하는 방법을 살펴보겠습니다. 다음 자습서에는 데이터 모델을 업로드 한 파일을 통합 하는 데 주의 살펴보겠습니다.

ASP.NET 2.0 새로운 [파일 업로드 웹 컨트롤](https://msdn.microsoft.com/library/ms227677(VS.80).aspx) 사용자가 자신의 컴퓨터에서 웹 서버에 파일을 보낼 수에 대 한 메커니즘을 제공 합니다. 파일 업로드 컨트롤으로 렌더링는 `<input>` 요소 인 `type` 특성은 브라우저는 찾아보기 단추가 있는 textbox로 표시 된 파일을로 설정 합니다. 사용자 파일을 선택할 수 있는 대화 상자에서 찾아보기 단추를 클릭 하면 나타납니다. 양식에 다시 게시 하는 경우 선택한 파일의 내용은 포스트백 함께 전송 됩니다. 서버 쪽에서 업로드 된 파일에 대 한 정보는 파일 업로드 컨트롤의의 속성을 통해 액세스할 수 있습니다.

업로드 파일을 보여 주기 위해 열고는 `FileUpload.aspx` 페이지에 `BinaryData` 폴더를 디자이너에 도구 상자에서 파일 업로드 컨트롤을 끌어서 컨트롤 s 설정 `ID` 속성을 `UploadTest`합니다. 다음으로 설정 단추 웹 컨트롤을 추가 해당 `ID` 및 `Text` 속성을 `UploadButton` 각각 선택한 파일을 업로드 합니다. 마지막으로, 지우기 단추 아래의 Label 웹 컨트롤을 배치 해당 `Text` 속성 집합과 해당 `ID` 속성을 `UploadDetails`합니다.


[![ASP.NET 페이지에 파일 업로드 컨트롤을 추가 합니다.](uploading-files-cs/_static/image12.gif)](uploading-files-cs/_static/image17.png)

**그림 12**: ASP.NET 페이지에는 파일 업로드 컨트롤을 추가 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image18.png))


그림 13에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다. 파일 선택 대화 상자를 제공 찾아보기 단추를 클릭 하면 사용자가 자신의 컴퓨터에서 파일을 선택 하는 수 있도록 하는 것을 참고 합니다. 파일을 선택 하 고 나면 웹 서버에 선택한 파일 s 이진 콘텐츠를 보내는 포스트백이 발생 선택한 파일 업로드 단추를 클릭 합니다.


[![사용자는 자신의 컴퓨터에서 서버에 업로드할 파일을 선택할 수 있습니다.](uploading-files-cs/_static/image13.gif)](uploading-files-cs/_static/image19.png)

**그림 13**: 서버에 자신의 컴퓨터에서 업로드 파일을 선택할 수 있는 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image20.png))


다시 게시 될 파일 시스템에 업로드 된 파일을 저장할 수 있습니다 또는 이진 데이터 스트림을 통해 직접 작업할 수 있습니다. 예를 들어 s 만들 수는 `~/Brochures` 폴더에 업로드 된 파일을 저장 하 고 있습니다. 추가 하 여 시작 된 `Brochures` 사이트 루트 디렉터리의 하위 폴더입니다. 에 대 한 이벤트 처리기를 다음으로 만듭니다는 `UploadButton` s `Click` 이벤트를 다음 코드를 추가 합니다.


[!code-csharp[Main](uploading-files-cs/samples/sample5.cs)]

파일 업로드 컨트롤 다양 한 업로드 된 데이터를 사용 하기 위한 속성을 제공 합니다. 예를 들어,는 [ `HasFile` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx) 사용자가 업로드 된 한 파일이 있는지 여부를 나타내는 동안는 [ `FileBytes` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx) 바이트의 배열로 업로드 된 이진 데이터에 대 한 액세스를 제공 합니다. `Click` 파일 업로드 되었는지 확인 하 여 이벤트 처리기를 시작 합니다. 파일을 업로드 경우 레이블을 업로드 된 파일, 바이트의 크기 및 해당 콘텐츠 형식을의 이름을 표시 합니다.

> [!NOTE]
> 사용자를 확인할 수 있습니다 파일 업로드를 위해는 `HasFile` 속성 경우 경고를 표시 하 고 그 s `false`, 하거나 사용할 수 있습니다는 [RequiredFieldValidator 제어](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx) 대신 합니다.


파일 업로드 s `SaveAs(filePath)` 업로드 된 파일을 지정 된 저장 *filePath*합니다. *filePath* 이어야 합니다는 *실제 경로* (`C:\Websites\Brochures\SomeFile.pdf`) 대신 *가상* *경로* (`/Brochures/SomeFile.pdf`). [ `Server.MapPath(virtPath)` 메서드](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx) 가상 경로 사용 하 고 해당 물리적 경로 반환 합니다. 여기에서 가상 경로가 `~/Brochures/fileName`여기서 *fileName* 업로드 된 파일의 이름입니다. 참조 [를 사용 하 여 Server.MapPath](http://www.4guysfromrolla.com/webtech/121799-1.shtml) 가상 및 실제 경로 및 사용에 대 한 자세한 내용은 `Server.MapPath`합니다.

완료 한 후는 `Click` 이벤트 처리기를 충분히 브라우저에서 페이지를 테스트해 보십시오. 찾아보기 단추를 클릭 하드 드라이브에서 파일을 선택 하 고 선택한 파일 업로드 단추를 클릭 합니다. 파일에 대 한 정보를 저장 하기 전에 다음 표시 하는 웹 서버에 포스트백 선택한 파일의 내용을 송신할는 `~/Brochures` 폴더입니다. 파일을 업로드 한 후 Visual Studio로 반환 하 고 솔루션 탐색기에서 새로 고침 단추를 클릭 합니다. 방금 ~/Brochures 폴더에 업로드 한 파일에 표시 됩니다!


[![웹 서버에 업로드 된 파일 EvolutionValley.jpg](uploading-files-cs/_static/image14.gif)](uploading-files-cs/_static/image21.png)

**그림 14**: 파일 `EvolutionValley.jpg` 웹 서버에 업로드 된 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image22.png))


![EvolutionValley.jpg은 ~/Brochures 폴더에 저장 되었습니다.](uploading-files-cs/_static/image15.gif)

**그림 15**: `EvolutionValley.jpg` 에 저장 된는 `~/Brochures` 폴더


## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>파일 시스템에 업로드 된 파일을 저장 하는 미묘한

웹 서버의 파일 시스템에 파일 업로드를 저장할 때 해결 해야 하는 몇 가지 미묘한 가지가 있습니다. 보안의 첫 번째, 네의 문제입니다. 파일 시스템에는 파일을 저장 하려면 ASP.NET 페이지를 실행 중인 보안 컨텍스트 쓰기 권한이 있어야 합니다. ASP.NET 개발 웹 서버는 현재 사용자 계정의 컨텍스트에서 실행 됩니다. Microsoft의 인터넷 정보 서비스 (IIS)를 웹 서버로 사용 하는 경우 보안 컨텍스트가 IIS 및 해당 구성의 버전에 따라 달라 집니다.

파일 시스템에 파일 저장의 또 다른 문제는 다음을 파일 이름을 지정 합니다. 가격 페이지에 업로드 된 파일의 모든 저장 현재는 `~/Brochures`의 클라이언트 컴퓨터에서 파일과 같은 이름을 사용 하 여 디렉터리입니다. 사용자 A는 브로슈어 이름으로 업로드 하는 경우 `Brochure.pdf`, 파일으로 저장 됩니다 `~/Brochure/Brochure.pdf`합니다. 잠시 이후 사용자 B 있는 파일 이름이 같은 다른 브로슈어 파일을 업로드 하는 경우에 어떻게 하지만 (`Brochure.pdf`)? 코드는 이제 사용자와 사용자 B의 업로드의 파일을 덮어쓸 수 있습니다.

다양 한 파일 이름 충돌을 해결 하는 데 대 한 기술을 갖추고 있습니다. 한 가지 방법은 이미 있을 경우 동일한 이름으로 파일을 업로드 하지 못하도록 하는 것입니다. 이 방법에서는 사용자 B 라는 파일을 업로드 하려고 할 때 `Brochure.pdf`, 시스템은 해당 파일을 저장 및 대신 사용자 B 파일 이름을 바꾸고 다시 시도를 알리는 메시지를 표시 하지 않습니다. 또 다른 방법은 될 수 있는 고유한 파일 이름을 사용 하 여 파일을 저장 하는 [전역 고유 식별자 (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 또는 레코드 s 기본 키 열을 데이터베이스에서 해당 값 (업로드가 연관 가정 하는 특정 행의 데이터 모델)입니다. 다음 자습서에서 이러한 옵션을을 자세히 살펴보겠습니다.

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>매우 많은 양의 이진 데이터와 관련 된 문제

이 자습서는 캡처된 이진 데이터 크기에 어느 정도의 라고 가정 합니다. 이진 데이터 파일을 몇 메가바이트 매우 많은 양의 작업 또는 더 큰이 자습서의 범위를 벗어나는 새로운 과제가 있습니다. 예를 들어 기본적으로 ASP.NET 거부 업로드 작업 4MB 보다이 통해 구성할 수 있지만 [ `<httpRuntime>` 요소](https://msdn.microsoft.com/library/e1f13641.aspx) 에서 `Web.config`합니다. IIS는 너무 고유 파일 업로드 크기 제한을 적용합니다. 참조 [IIS 업로드 파일 크기](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html) 자세한 정보에 대 한 합니다. 또한, 큰 파일을 업로드 하는 데 걸린 시간 기본 ASP.NET 요청을 기다리는 110 초 초과할 수 있습니다. 큰 파일을 작업할 때 발생 하는 메모리 및 성능 문제가 있습니다.

파일 업로드 컨트롤 대형 파일 업로드 시에 유용 합니다. 파일의 내용을 서버에 게시 되는, 최종 사용자가 업로드 진행 되 고 있다는 확인 없이 꾸준히 기다려야 합니다. 몇 초 후에 업로드할 수 있지만 더 큰 파일을 업로드 하는 데 시간이 걸릴 수를 처리할 때 문제가 발생할 수 있는 더 작은 파일을 다룰 때에 많은 양의 문제가 되지 않습니다. 다양 한 제 3 자 파일 업로드 컨트롤 대규모 업로드를 처리 하기 위한 더 적합 있으며 이들 공급이 업체의 많은 제공 진행률 표시기 및 ActiveX 업로드 훨씬 더 세련 된 사용자 환경을 제공 하는 관리자.

응용 프로그램을 큰 파일을 처리 하는 경우 신중 하 고 문제를 조사 하 고 특정 요구 사항에 대 한 적합 한 솔루션을 찾을 해야 합니다.

## <a name="summary"></a>요약

이진 데이터를 캡처 하는데 필요한 응용 프로그램에 빌드하는 많은 문제를 소개 합니다. 이 자습서에서는 처음 두 살펴본: 이진 데이터를 저장할 위치를 결정 하 고 사용자가 웹 페이지를 통해 이진 콘텐츠를 업로드 합니다. 다음 세 개의 자습서를 통해 업로드 된 데이터는 데이터베이스의 레코드와 연결 하는 방법 뿐만 아니라 해당 텍스트 데이터 필드와 함께 이진 데이터를 표시 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [큰 값 데이터 형식 사용](https://msdn.microsoft.com/library/ms178158.aspx)
- [파일 업로드 컨트롤 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2.0 파일 업로드 서버 컨트롤](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [파일 업로드](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피 및 박 광 준 Leigh 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](displaying-binary-data-in-the-data-web-controls-cs.md)
