---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
title: 파일 업로드 (VB) | Microsoft Docs
author: rick-anderson
description: '웹 사이트 중 하나는 서버의 파일 시스템에 저장 될 수 있는 위치에 이진 파일 (예: Word 또는 PDF 문서)를 업로드할 수 있도록 하는 방법 알아보기...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: f7c00fbd-652c-433d-8ed3-0e5168a4d4df
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
msc.type: authoredcontent
ms.openlocfilehash: 1b6257c05bcefa01d3358536ffbdfc3a31d6b280
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373161"
---
<a name="uploading-files-vb"></a>파일 업로드 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_VB.exe) 또는 [PDF 다운로드](uploading-files-vb/_static/datatutorial54vb1.pdf)

> 서버의 파일 시스템 또는 데이터베이스에 저장 될 수 있는 웹 사이트에 이진 파일 (예: Word 또는 PDF 문서)를 업로드할 수 있도록 하는 방법을 알아봅니다.


## <a name="introduction"></a>소개

모든 자습서에서는 지금 검사 ve 텍스트 데이터로 작업 합니다. 그러나 여러 응용 프로그램에서는 텍스트와 이진 데이터를 캡처하는 데이터 모델입니다. 온라인 데이트 사이트를 사용자가 사진을 업로드 하 여 해당 프로필에 연결할 수 있습니다. 채용 웹 사이트 사용자가 다시 시작으로 Microsoft Word 또는 PDF 문서를 업로드할 수 있습니다.

문제의 새 집합을 추가 하는 이진 데이터를 사용 합니다. 응용 프로그램의 이진 데이터가 저장 되는 방법을 결정 해야 합니다. 새 레코드 삽입에 사용 되는 인터페이스에 사용자가 자신의 컴퓨터에서 파일을 업로드 하도록 허용 하도록 업데이트 되어야 하 고 추가 단계를 수행 하 여 표시 하거나 관련 된 이진 데이터를 레코드 s를 다운로드 하기 위한 수단을 제공 해야 합니다. 이 자습서에는 다음 세는 걸림돌 이러한 문제를이 해결 하는 방법을 살펴봅니다. 이 자습서의 끝에서는 만들었습니다 사진 및 PDF 브로슈어 각 범주를 사용 하 여 연결 하는 응용 프로그램을 완벽 하 게 작동 합니다. 이 특정 자습서에서는 이진 데이터를 저장 하기 위한 다양 한 기술을 확인 하 고 사용자가 자신의 컴퓨터에서 파일 업로드 수 있게 하는 방법에 대해 및 웹 서버의 파일 시스템에 저장 한 합니다.

> [!NOTE]
> 응용 프로그램 s 데이터 모델이 포함 된 이진 데이터는 때때로 이라고 하는 [BLOB](http://en.wikipedia.org/wiki/Binary_large_object), Binary Large OBject에 대 한 머리글자어입니다. 이 자습서에서 BLOB 동의어 이라는 용어가 있지만 용어 이진 데이터를 사용 하도록 선택 했습니다 하나요.


## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>1 단계: 이진 데이터 웹 페이지를 사용 하 여 작업 만들기

이진 데이터에 대 한 지원을 추가와 관련 된 문제를 탐색을 시작 하기 전에 s를 먼저 시간을 내어이 자습서에는 다음 세 할 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `BinaryData`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`


![이진 데이터 관련 자습서에 대 한 ASP.NET 페이지 추가](uploading-files-vb/_static/image1.gif)

**그림 1**: 이진 데이터 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `BinaryData` 폴더 섹션의 자습서를 나열 됩니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지의 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](uploading-files-vb/_static/image2.gif)](uploading-files-vb/_static/image1.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](uploading-files-vb/_static/image2.png))


마지막으로, 이러한 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히 다음 태그를 확장 한 후 추가 GridView `<siteMapNode>`:


[!code-xml[Main](uploading-files-vb/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 이제 메뉴 왼쪽에서 이진 데이터 자습서를 사용 하 여 작업에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 이진 데이터 자습서를 사용 하 여 작업 항목을 포함](uploading-files-vb/_static/image3.gif)

**그림 3**: 이제 사이트 맵 이진 데이터 자습서를 사용 하 여 작업 항목을 포함


## <a name="step-2-deciding-where-to-store-the-binary-data"></a>이진 데이터를 저장할 위치를 결정 하는 2 단계:

두 위치 중 하나에서 응용 프로그램의 데이터 모델을 사용 하 여 연결 된 이진 데이터를 저장할 수 있습니다: 데이터베이스에 저장 된 파일에 대 한 참조를 사용 하 여 웹 서버의 파일 시스템에서 또는 데이터베이스 자체 내에서 직접 (그림 4 참조). 각 방법 마다 고유한 장점과 단점 및 부분에 자세한 내용은 합니다.


[![파일 시스템 또는 데이터베이스에서 직접 이진 데이터를 저장할 수 있습니다.](uploading-files-vb/_static/image4.gif)](uploading-files-vb/_static/image3.png)

**그림 4**: 파일 시스템 또는 데이터베이스에서 직접 이진 데이터를 저장할 수 있습니다 ([큰 이미지를 보려면 클릭](uploading-files-vb/_static/image4.png))


각 제품을 사용 하 여 그림을 연결 하려면 Northwind 데이터베이스를 확장 하 려 한다고 가정 합니다. 하나의 옵션은 웹 서버의 파일 시스템에 이러한 이미지 파일을 저장할 경로 기록 하는 것은 `Products` 테이블입니다. 이 방법을 사용 하 여 d 추가 `ImagePath` 열을 `Products` 형식의 테이블 `varchar(200)`를 합니다. 사용자 사진 chai에 업로드 하는 경우 해당 그림이 웹의 서버 파일 시스템에 저장 될 수 `~/Images/Tea.jpg`여기서 `~` 응용 프로그램 s 실제 경로 나타냅니다. 즉, 웹 사이트 실제 경로에서 시작 하는 경우 `C:\Websites\Northwind\`하십시오 `~/Images/Tea.jpg` 에 해당 `C:\Websites\Northwind\Images\Tea.jpg`합니다. 이미지 파일을 업로드 한 후 d 업데이트에 Chai 레코드를 `Products` 테이블 있도록 해당 `ImagePath` 새 이미지의 경로 참조 하는 열입니다. 사용 하 여 `~/Images/Tea.jpg` 또는 그냥 `Tea.jpg` 모든 제품 이미지는 배치 하는 것 응용 프로그램에서 결정 한 경우 `Images` 폴더입니다.

파일 시스템에 이진 데이터를 저장 하는 주요 이점은 다음과 같습니다.

- **구현 편의성** 곧 볼 수 있겠지만, 데이터베이스 내에 직접 저장 하는 이진 데이터 저장 및 검색 파일 시스템을 통해 데이터를 사용 하 여 사용할 때 보다 더 복잡 한 코드를 포함 합니다. 또한 보기 또는 이진 데이터를 다운로드 하는 사용자에 대 한 순서로 이러한 제공 해야 해당 데이터에 대 한 URL입니다. 데이터는 웹 서버 파일 시스템에 있는 경우 URL은 간단 합니다. 그러나 데이터를 데이터베이스에 저장 됩니다 웹 만들어야 검색 하 고 데이터베이스에서 데이터를 반환 하는 페이지입니다.
- **이진 데이터에 대 한 광범위 한 액세스** 이진 데이터를 다른 서비스 또는 데이터베이스에서 데이터를 끌어올 수 없습니다는 응용 프로그램에 액세스할 수 있도록 해야 할 수 있습니다. 예를 들어, 각 제품과 관련 된 이미지 해야 할 수도 통해 사용자에 게 사용할 수 있습니다 [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol), 이때 d 하고자 이진 데이터를 파일 시스템에 저장 합니다.
- **성능** 이진 데이터를 파일 시스템에 저장 된 경우 데이터베이스 서버 및 웹 서버 간에 요청 및 네트워크 정체 보다 작을 것 경우 이진 데이터를 데이터베이스에 직접 저장 됩니다.

파일 시스템에 이진 데이터를 저장 하는 데 가지 주요 단점은 데이터베이스에서 데이터를 구분할 수입니다. 레코드에서 삭제 되 면는 `Products` 테이블, 웹 서버의 파일 시스템에 연결된 된 파일 자동으로 삭제 되지 않습니다. 사용 되지 않는, 분리 된 파일을 사용 하 여 파일 또는 파일 시스템을 삭제 하기 위해 추가 코드는 복잡해 작성 해야 합니다. 또한 데이터베이스를 백업할 때 항상 해야도 파일 시스템에 연결 된 이진 데이터의 백업을 확인 해야 합니다. 다른 사이트 또는 서버와 유사한 문제가 데이터베이스를 이동 합니다.

형식의 열을 만들어 Microsoft SQL Server 2005 데이터베이스에 직접 이진 데이터에 저장 수는 또는 `varbinary`합니다. 와 같은 다른 가변 길이 데이터 형식과 보유할 수 있는 이진 데이터의 최대 길이이 열에 지정할 수 있습니다. 예를 들어, 예약할 최대 5,000 바이트 사용 `varbinary(5000)`; `varbinary(MAX)` 2GB에 대 한 최대 저장소 크기를 허용 합니다.

데이터베이스에서 직접 이진 데이터를 저장 하는 주요 장점은 이진 데이터와 데이터베이스 간의 긴밀 한 결합입니다. 이 백업 또는 다른 사이트 또는 서버에 데이터베이스를 이동 하는 같은 데이터베이스 관리 작업을 크게 간소화 합니다. 또한 자동으로 레코드를 삭제 하면 해당 이진 데이터를 삭제 합니다. 데이터베이스에 이진 데이터를 저장 하는 미묘한 이점이 더 있습니다. 참조 [저장할 이진 파일 직접 데이터베이스를 사용 하 여 ASP.NET 2.0의](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx) 심도 있는 논의 대 한 합니다.

> [!NOTE]
> Microsoft SQL Server 2000 및 이전 버전의 `varbinary` 데이터 형식의 8,000 바이트의 최대 제한이 있었습니다. 최대 2GB의 이진 데이터를 저장 하는 [ `image` 데이터 형식](https://msdn.microsoft.com/library/ms187993.aspx) 를 대신 사용 해야 합니다. 그러나 추가 된 `MAX` SQL Server 2005에서는는 `image` 데이터 형식에 사용 되지 않습니다. 그가 계속 지원에 대 한 이전 버전과 호환성을 하지만 Microsoft는 발표 했습니다는 `image` 데이터 형식을 SQL Server의 이후 버전에서 제거 됩니다.


오래 된 데이터 모델을 사용 하는 경우 발생할 수 있습니다는 `image` 데이터 형식입니다. Northwind 데이터베이스 s `Categories` 테이블에는 `Picture` 범주에 대 한 이미지 파일의 이진 데이터를 저장할 수 있는 열입니다. 이 열 형식의 Northwind 데이터베이스에 Microsoft Access 및 이전 버전의 SQL Server에 기반을 두고 있으므로 `image`합니다.

이 자습서에는 다음 세 가지 방법을 모두 사용 하겠습니다. 합니다 `Categories` 테이블에 이미를 `Picture` 범주에 대 한 이미지의 이진 콘텐츠를 저장 하기 위한 열입니다. 추가 열을 추가한 `BrochurePath`범주의 인쇄 품질의 고급 개요를 제공 하는 데 사용할 수 있는 웹 서버의 파일 시스템에 PDF에 대 한 경로 저장 합니다.

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>3 단계: 추가 된`BrochurePath`열에는`Categories`테이블

현재 범주 테이블에 4 개의 열: `CategoryID`, `CategoryName`를 `Description`, 및 `Picture`합니다. 이러한 필드 외에도 새로 가리키는 범주의 브로슈어 (있는 경우)를 추가 해야 합니다. 이 열을 추가 하려면 서버 탐색기에서 드릴 다운 테이블을 마우스 오른쪽 단추로 클릭 이동 된 `Categories` 테이블 및 테이블 정의 열기 (그림 5 참조). 서버 탐색기에 표시 되지 않는다면 보기 메뉴에서 서버 탐색기 옵션을 선택 하 여 표시 하거나 Ctrl + Alt + S를 누릅니다.

새 `varchar(200)` 열을 `Categories` 라는 테이블을 `BrochurePath` 하며 `NULL` s 및 저장 아이콘을 클릭 (또는 Ctrl + S를 누릅니다).


[![Categories 테이블 BrochurePath 열을 추가 합니다.](uploading-files-vb/_static/image5.gif)](uploading-files-vb/_static/image5.png)

**그림 5**: 추가 된 `BrochurePath` 열을 합니다 `Categories` 테이블 ([전체 크기 이미지를 보려면 클릭](uploading-files-vb/_static/image6.png))


## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>4 단계: 아키텍처를 사용 하도록 업데이트 합니다`Picture`고`BrochurePath`열

합니다 `CategoriesDataTable` 데이터 액세스 계층 (DAL)에서 현재 4 개가 `DataColumn` s 정의: `CategoryID`, `CategoryName`를 `Description`, 및 `NumberOfProducts`합니다. 이 DataTable을 원래 디자인에서는 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서를 `CategoriesDataTable` 처음 3 개의 열만 있었습니다; 그리고 `NumberOfProducts` 열에 추가 되었습니다는 [마스터/세부 정보는 글머리 기호를 사용 하 여 세부 정보 DataList와 함께 마스터 레코드의 목록을](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) 자습서입니다.

에 설명 된 대로 *데이터 액세스 레이어 만들기*, 형식화 된 DataSet의 Datatable 비즈니스 개체를 구성 합니다. Tableadapter는 데이터베이스와 통신 하 고 쿼리 결과 사용 하 여 비즈니스 개체를 채우는 하는 일을 담당 합니다. `CategoriesDataTable` 채워집니다는 `CategoriesTableAdapter`, 세 가지 데이터 검색 메서드보다 있는:

- `GetCategories()` TableAdapter가 기본 쿼리를 실행 하 고 반환 합니다 `CategoryID`, `CategoryName`, 및 `Description` 의 모든 레코드의 필드는 `Categories` 테이블입니다. 기본 쿼리는 자동으로 생성 하 여 용도 `Insert` 고 `Update` 메서드.
- `GetCategoryByCategoryID(categoryID)` 반환 합니다 `CategoryID`, `CategoryName`, 및 `Description` 범주 필드입니다 `CategoryID` equals *categoryID*합니다.
- `GetCategoriesAndNumberOfProducts()` -반환 합니다 `CategoryID`, `CategoryName`, 및 `Description` 의 모든 레코드에 대 한 필드를 `Categories` 테이블입니다. 또한 하위 쿼리를 사용 하 여 각 범주와 관련 된 제품의 수를 반환 합니다.

이러한 반환을 쿼리 하는 알림을 `Categories` 테이블 s `Picture` 또는 `BrochurePath` 없으며 열을 `CategoriesDataTable` 제공 `DataColumn` 이러한 필드에 대 한 합니다. 그림 사용 하기 위해서는 및 `BrochurePath` 속성을 먼저 추가 해야 하는 `CategoriesDataTable` 한 다음 업데이트는 `CategoriesTableAdapter` 이러한 열이 반환 하는 클래스입니다.

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>추가 된`Picture`고`BrochurePath``DataColumn` s

이러한 두 열을 추가 하 여 시작 된 `CategoriesDataTable`합니다. 마우스 오른쪽 단추로 클릭는 `CategoriesDataTable`의 헤더를 상황에 맞는 메뉴에서 추가 선택 하 고 다음 열 옵션을 선택 합니다. 이렇게 하면 새 만들어집니다 `DataColumn` 이라는 DataTable에서 `Column1`합니다. 이 열의 이름을 바꿀 `Picture`합니다. 속성 창에서 설정 합니다 `DataColumn` s `DataType` 속성을 `System.Byte[]` (드롭다운 목록에는 옵션이 아닙니다.) 입력 해야 합니다.


[![데이터 형식을 갖는 System.Byte DataColumn 라는 그림 만들기](uploading-files-vb/_static/image6.gif)](uploading-files-vb/_static/image7.png)

**그림 6**: 만들기를 `DataColumn` 명명 된 `Picture` 인 `DataType` 됩니다 `System.Byte[]` ([클릭 하 여 큰 이미지 보기](uploading-files-vb/_static/image8.png))


다른 항목 추가 `DataColumn` 이름을 DataTable로 `BrochurePath` 기본값을 사용 하 여 `DataType` 값 (`System.String`).

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>반환 된`Picture`고`BrochurePath`TableAdapter의 값

이 두 가지를 사용 하 여 `DataColumn` s에 추가 합니다 `CategoriesDataTable`, 업데이트 하려면 준비 된 것을 `CategoriesTableAdapter`. 주 TableAdapter 쿼리에서 반환 된 두 열의 값을 사용할 수도 있습니다 하지만이 데이터 다시 가져오기는 이진 때마다는 `GetCategories()` 메서드가 호출 되었습니다. Let s를 다시 주 TableAdapter 쿼리를 업데이트 하는 대신 `BrochurePath` s 특정 범주를 반환 하는 추가 데이터 검색 메서드를 만들어 `Picture` 열입니다.

주 TableAdapter 쿼리를 업데이트 하려면 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 및 상황에 맞는 메뉴에서 구성 옵션을 선택 합니다. 그러면 어떤에서는 테이블 어댑터 구성 마법사 ve 다양 한 이전 자습서에에서 표시 합니다. 쿼리 되돌리기를 업데이트 합니다 `BrochurePath` 하 고 마침을 클릭 합니다.


[![또한 BrochurePath를 반환 하려면 SELECT 문에 열 목록을 업데이트합니다](uploading-files-vb/_static/image7.gif)](uploading-files-vb/_static/image9.png)

**그림 7**: 열 목록을 업데이트 합니다 `SELECT` 반환할 수도 문을 `BrochurePath` ([클릭 하 여 큰 이미지 보기](uploading-files-vb/_static/image10.png))


TableAdapter에 대 한 임시 SQL 문을 사용 하는 경우 기본 쿼리에 열 목록을 업데이트 하는 모든 열 목록 업데이트는 `SELECT` TableAdapter의 메서드를 쿼리 합니다. 즉, 합니다 `GetCategoryByCategoryID(categoryID)` 메서드를 반환 하도록 업데이트 되었습니다는 `BrochurePath` 에서는 의도 될 수 있는 열입니다. 그러나 열 목록도 업데이트 된 `GetCategoriesAndNumberOfProducts()` 메서드를 제거 하는 각 범주에 대 한 제품 개수를 반환 하는 하위! 가이 메서드를 업데이트 해야 하므로 `SELECT` 쿼리 합니다. 마우스 오른쪽 단추로 클릭 합니다 `GetCategoriesAndNumberOfProducts()` 메서드를 구성, 선택 및 되돌리기는 `SELECT` 원래 값으로 다시 쿼리:


[!code-sql[Main](uploading-files-vb/samples/sample2.sql)]

다음으로, 특정 범주의 s를 반환 하는 새 TableAdapter 메서드를 만듭니다 `Picture` 열 값입니다. 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 TableAdapter 쿼리 구성 마법사를 시작 하는 추가 쿼리 옵션을 선택 합니다. 이 마법사의 첫 번째 단계는 임시 SQL 문을 사용 하 여 데이터를 쿼리, 필요한 경우 새 저장 프로시저 또는 기존 우리를 요청 합니다. SQL 문 사용을 선택 하 고 클릭 합니다. 우리는 반환할 행, 하므로 행 옵션 두 번째 단계에서 반환 하는 SELECT를 선택 합니다.


[![사용 하 여 SQL 문을 옵션 선택](uploading-files-vb/_static/image8.gif)](uploading-files-vb/_static/image11.png)

**그림 8**: 사용 하 여 SQL 문을 옵션을 선택 ([큰 이미지를 보려면 클릭](uploading-files-vb/_static/image12.png))


[![선택 행을 반환 하는 SELECT 쿼리는 Categories 테이블에서 레코드를 반환 하 고, 이후](uploading-files-vb/_static/image9.gif)](uploading-files-vb/_static/image13.png)

**그림 9**: 쿼리는 행을 반환 하는 선택 선택 범주 테이블에서 레코드를 반환 하므로 ([큰 이미지를 보려면 클릭](uploading-files-vb/_static/image14.png))


세 번째 단계에서는 다음 SQL 쿼리를 입력 하 고 클릭 합니다.


[!code-sql[Main](uploading-files-vb/samples/sample3.sql)]

마지막 단계는 새 메서드의 이름을 선택 합니다. 사용 하 여 `FillCategoryWithBinaryDataByCategoryID` 및 `GetCategoryWithBinaryDataByCategoryID` 채우기 돌아가 DataTable DataTable 패턴, 각각. 마법사를 완료 하려면 마침을 클릭 합니다.


[![TableAdapter가의 메서드에 대 한 이름을 선택 합니다.](uploading-files-vb/_static/image10.gif)](uploading-files-vb/_static/image15.png)

**그림 10**: tableadapter 메서드 이름 선택 ([큰 이미지를 보려면 클릭](uploading-files-vb/_static/image16.png))


> [!NOTE]
> 테이블 어댑터 쿼리 구성 마법사를 완료 한 후 새 명령 텍스트를 반환 하는 스키마를 사용 하 여 데이터와 다른 주 쿼리의 스키마를 알리는 대화 상자가 표시 될 수 있습니다. 즉, 마법사는 유의 해야 하는 TableAdapter가 기본 쿼리 `GetCategories()` 방금 만든 아닌 다른 스키마를 반환 합니다. 하지만이 원하는 항목 이므로이 메시지를 무시할 수 있습니다.


또한 염두에 임시 SQL 문을 사용 하는 시간에 나중에 TableAdapter가 기본 쿼리를 변경 하려면 마법사를 사용 하는 경우 수정 됩니다는 `GetCategoryWithBinaryDataByCategoryID` s 메서드에 `SELECT`의 문 열 목록에서 해당 열을 포함 하는 기본 쿼리 (즉, 제거 됩니다는 `Picture` 쿼리에서 열). 반환할 열 목록을 수동으로 업데이트 해야 합니다 `Picture` 열을 사용 하 여 저희 비슷합니다를 `GetCategoriesAndNumberOfProducts()` 이 단계에서는 이전 메서드.

두를 추가한 후 `DataColumn` 에 `CategoriesDataTable` 및 `GetCategoryWithBinaryDataByCategoryID` 메서드를는 `CategoriesTableAdapter`, 입력 데이터 집합 디자이너에서 이러한 클래스에 그림 11의 스크린샷과 같습니다.


![새 열 및 메서드를 포함 하는 데이터 집합 디자이너](uploading-files-vb/_static/image11.gif)

**그림 11**: 새 열 및 메서드를 포함 하는 데이터 집합 디자이너


## <a name="updating-the-business-logic-layer-bll"></a>비즈니스 논리 계층 BLL ()를 업데이트 하는 중

업데이트 DAL을 사용 하 여 이제 남은 것은 계층 BLL (비즈니스 논리) 새 메서드를 포함 하도록 확장할 수 `CategoriesTableAdapter` 메서드. 다음 메서드를 추가 합니다 `CategoriesBLL` 클래스:


[!code-vb[Main](uploading-files-vb/samples/sample4.vb)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>웹 서버에 클라이언트에서 파일을 업로드 하는 5 단계:

종종 이진 데이터를 수집 하려는 경우이 데이터는 최종 사용자가 제공 됩니다. 이 정보를 캡처하려면 사용자는 자신의 컴퓨터에서 웹 서버에 파일을 업로드할 수 해야 합니다. 업로드 된 데이터를 웹 서버 파일 시스템 및 데이터베이스의 파일 경로 추가 또는 이진 콘텐츠 데이터베이스에 직접 작성 파일을 저장 합니다. 데이터 모델을 통합 해야 합니다. 이 단계에서는 사용자가 자신의 컴퓨터에서 서버에 파일 업로드를 허용 하는 방법을 살펴보겠습니다. 다음 자습서에서는 데이터 모델을 사용 하 여 업로드 된 파일을 통합에 대해 살펴보겠습니다.

ASP.NET 2.0 새로운 [FileUpload 웹 컨트롤](https://msdn.microsoft.com/library/ms227677(VS.80).aspx) 자신의 컴퓨터에서 파일을 웹 서버에 보낼 사용자에 대 한 메커니즘을 제공 합니다. FileUpload 컨트롤 렌더링을 `<input>` 요소입니다 `type` 파일 브라우저 찾아보기 단추를 사용 하 여 텍스트 상자로 표시 하는 특성이 설정 되어 있습니다. 찾아보기 단추를 누르면 사용자 파일을 선택할 수 있는 대화 상자를 나타납니다. 양식에 다시 게시 되 면 선택한 파일이의 내용은 포스트백 함께 전송 됩니다. 서버 쪽에서 업로드 된 파일에 대 한 정보는 FileUpload 컨트롤 속성을 통해 액세스할 수 있습니다.

파일 업로드를 보여 주기 위해 엽니다는 `FileUpload.aspx` 페이지에 `BinaryData` 폴더 디자이너 도구 상자에서 FileUpload 컨트롤을 끌어서 s control 설정 `ID` 속성을 `UploadTest`. 다음으로 설정 단추 웹 컨트롤을 추가 해당 `ID` 하 고 `Text` 속성을 `UploadButton` 각각 선택한 파일을 업로드 합니다. 마지막으로 지웁니다 단추 아래의 Label 웹 컨트롤을 배치할 해당 `Text` 속성 집합과 해당 `ID` 속성을 `UploadDetails`입니다.


[![ASP.NET 페이지에 FileUpload 컨트롤을 추가 합니다.](uploading-files-vb/_static/image12.gif)](uploading-files-vb/_static/image17.png)

**그림 12**: ASP.NET 페이지에 FileUpload 컨트롤 추가 ([큰 이미지를 보려면 클릭](uploading-files-vb/_static/image18.png))


그림 13에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다. 사용자가 자신의 컴퓨터에서 파일을 선택할 수 있도록 파일 선택 대화 상자, 표시 찾아보기 단추를 클릭 하는 참고 합니다. 파일 선택 되 면 웹 서버로 선택한 파일이 이진 콘텐츠를 전송 하는 포스트백을 발생 시키는 선택한 파일 업로드 단추를 클릭 합니다.


[![사용자가 자신의 컴퓨터에서 서버로 업로드할 파일을 선택할 수 있습니다.](uploading-files-vb/_static/image13.gif)](uploading-files-vb/_static/image19.png)

**그림 13**: 사용자가 컴퓨터를 서버에서 업로드할 파일을 선택할 수 ([큰 이미지를 보려면 클릭](uploading-files-vb/_static/image20.png))


포스트백에서 업로드 한 파일이 파일 시스템에 저장할 수 있습니다 또는 이진 데이터는 Stream을 통해 직접 작동할 수 있습니다. 예를 들어 만든 수는 `~/Brochures` 폴더에 업로드 된 파일을 저장 하 고 있습니다. 추가 하 여 시작 합니다 `Brochures` 루트 디렉터리의 하위 사이트에는 폴더입니다. 다음에 대 한 이벤트 처리기를 만듭니다는 `UploadButton` s `Click` 이벤트 다음 코드를 추가 합니다.


[!code-vb[Main](uploading-files-vb/samples/sample5.vb)]

FileUpload 컨트롤 다양 한 업로드 된 데이터로 작업 하기 위한 속성을 제공 합니다. 예를 들어 합니다 [ `HasFile` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx) 파일로 된 사용자가 업로드 되었는지 여부를 나타냅니다 하는 동안는 [ `FileBytes` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx) 바이트 배열 업로드 된 이진 데이터에 대 한 액세스를 제공 합니다. `Click` 이벤트 처리기는 파일이 업로드 된 함으로써 시작 합니다. 파일을 업로드 한 경우 레이블 이름을 업로드 된 파일, 해당 크기 (바이트)에서 및 해당 콘텐츠 형식을 보여 줍니다.

> [!NOTE]
> 사용자를 확인할 수 있습니다 파일 업로드를 확인 하는 `HasFile` 속성 경우 경고를 표시 하 고이 s `False`, 하거나 사용할 수 있습니다를 [RequiredFieldValidator 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx) 대신 합니다.


S FileUpload `SaveAs(filePath)` 업로드 된 파일을에 저장 된 *filePath*합니다. *filePath* 이어야 합니다는 *실제 경로* (`C:\Websites\Brochures\SomeFile.pdf`) 대신 *virtual* *경로* (`/Brochures/SomeFile.pdf`). 합니다 [ `Server.MapPath(virtPath)` 메서드](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx) 가상 경로 사용 하 고 실제 경로 반환 합니다. 여기서는 가상 경로 `~/Brochures/fileName`, 여기서 *fileName* 업로드 된 파일의 이름입니다. 참조 [Server.MapPath를 사용 하 여](http://www.4guysfromrolla.com/webtech/121799-1.shtml) 가상 및 실제 경로 및 사용에 대 한 자세한 내용은 `Server.MapPath`합니다.

완료 한 후의 `Click` 이벤트 처리기를 잠시 브라우저에서 페이지를 테스트 합니다. 찾아보기 단추를 클릭 하 고 하드 드라이브에서 파일을 선택 합니다. 선택한 파일 업로드 단추를 클릭 합니다. 그런 다음 저장 하기 전에 파일에 대 한 정보를 표시 하는 웹 서버에 포스트백 선택한 파일의 내용을 전송할는 `~/Brochures` 폴더입니다. 파일을 업로드 한 후 Visual Studio로 반환 하 고 솔루션 탐색기에서 새로 고침 단추를 클릭 합니다. ~/Brochures 폴더에서 방금 업로드 한 파일에 표시 됩니다.


[![웹 서버에 업로드 된 파일 EvolutionValley.jpg](uploading-files-vb/_static/image14.gif)](uploading-files-vb/_static/image21.png)

**그림 14**: 파일 `EvolutionValley.jpg` 웹 서버에 업로드 된 ([클릭 하 여 큰 이미지 보기](uploading-files-vb/_static/image22.png))


![EvolutionValley.jpg은 ~/Brochures 폴더에 저장 된](uploading-files-vb/_static/image15.gif)

**그림 15**: `EvolutionValley.jpg` 에 저장 된 된 `~/Brochures` 폴더


## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>파일 시스템에 업로드 된 파일을 저장 하는 미묘한

웹 서버의 파일 시스템에 파일 업로드를 저장할 때 해결 해야 하는 몇 가지 미묘한 있습니다. 보안 먼저 여기의 문제입니다. 파일 시스템에 파일을 저장 하는 ASP.NET 페이지가 실행 되는 보안 컨텍스트는 쓰기 권한이 있어야 합니다. ASP.NET 개발 웹 서버를 현재 사용자 계정의 컨텍스트에서 실행 됩니다. Microsoft가의 인터넷 정보 서비스 (IIS) 웹 서버를 사용 하는 경우 보안 컨텍스트는 버전의 IIS 및 해당 구성에 따라 달라 집니다.

파일 시스템에 파일을 저장 하는 또 다른 문제는 다음 파일 이름 지정을 합니다. 페이지에 업로드 된 파일의 모든 저장 현재는 `~/Brochures`의 클라이언트 컴퓨터의 파일로 동일한 이름을 사용 하 여 디렉터리입니다. 사용자는 이름의 브로슈어 업로드 하는 경우 `Brochure.pdf`, 파일으로 저장 됩니다 `~/Brochure/Brochure.pdf`합니다. 하지만 이후 잠시 사용자 B는 동일한 파일 이름을 가진 다른 브로슈어 파일을 업로드 하는 경우 (`Brochure.pdf`)? 코드를 사용 하 여에서는 이제 사용자를 사용자 B가의 업로드를 사용 하 여 s 파일을 덮어쓰게 됩니다.

파일 이름 충돌을 해결 하기 위한 기술의 여러 가지가 있습니다. 한 가지 방법은 이미 있을 경우 동일한 이름의 파일을 업로드 하지 못하도록 하는 것입니다. 이 방법에서는 사용자 B 라는 파일을 업로드 하려고 할 때 `Brochure.pdf`, 시스템은 하지 해당 파일을 저장 하 고 대신 파일 이름을 바꾸고 다시 시도를 사용자 B에 게 알리는 메시지를 표시 합니다. 일 수 있는 고유한 파일 이름을 사용 하 여 파일을 저장 하는 또 다른 방법은 [전역적으로 고유 식별자 (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 또는 레코드 s 기본 키 열을 데이터베이스에서 해당 값 (업로드 연관 된 가정를 특정 행에서 데이터 모델)입니다. 다음 자습서에서는 이러한 옵션을을 더 자세히 살펴봅니다.

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>매우 많은 양의 이진 데이터와 연관 된 문제

이러한 자습서 캡처된 이진 데이터 크기에 있다고 가정 합니다. 매우 많은 양의 이진 데이터 파일을 몇 메가바이트 작업 또는 더 큰 이러한 자습서에서 다루지 않은 새로운 과제가 있습니다. 예를 들어, 기본적으로 ASP.NET는 거부 4MB 보다의 업로드를 통해 구성할 수 있습니다 하지만 합니다 [ `<httpRuntime>` 요소](https://msdn.microsoft.com/library/e1f13641.aspx) 에서 `Web.config`합니다. IIS 자체 파일 업로드 크기 제한이 너무 적용합니다. 참조 [IIS 업로드 파일 크기](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html) 자세한 내용은 합니다. 또한 큰 파일을 업로드 하는 데 걸리는 시간이 기본 ASP.NET 요청을 기다리는 110 초 초과할 수 있습니다. 큰 파일로 작업할 때 발생 하는 메모리 및 성능 문제가 있습니다.

FileUpload 컨트롤 불가능 한 대형 파일 업로드에 대 한 합니다. 파일의 콘텐츠 서버에 게시 되는, 최종 사용자가 업로드 진행 되 고 있는지 확인 하지 않고 있으므로 편안 하 게 대기 해야 합니다. 잠시 후에 업로드할 수 있지만 업로드할 분 정도 더 큰 파일을 처리할 때 문제가 발생할 수 있는 작은 파일을 처리 하는 경우에 많은 문제가 되지 않습니다. 많은 공급이 업체 제공 진행률 표시기와 ActiveX 업로드를 훨씬 더 세련 된 사용자 환경을 제공 하는 관리자와 다양 한 타사 파일을 더 큰 업로드를 처리 하기 위한 적합 한 업로드 컨트롤 있습니다.

큰 파일을 처리 하도록 응용 프로그램에 필요한 경우 신중 하 게 문제를 조사 하 고 특정 요구 사항에 대 한 적합 한 솔루션을 찾을를 해야 합니다.

## <a name="summary"></a>요약

이진 데이터를 캡처 하는데 필요한 응용 프로그램을 빌드하는 많은 문제를 소개 합니다. 이 자습서에서는 처음 두 살펴보았습니다: 이진 데이터를 저장할 위치를 결정 하 고 사용자가 웹 페이지를 통해 이진 콘텐츠를 업로드할 수 있도록 합니다. 다음 세 개의 자습서를 통해 데이터베이스에서 레코드를 사용 하 여 업로드 된 데이터를 연결 하는 방법 뿐만 아니라 해당 텍스트 데이터 필드와 함께 이진 데이터를 표시 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [큰 값 데이터 형식 사용](https://msdn.microsoft.com/library/ms178158.aspx)
- [FileUpload 컨트롤 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2.0 FileUpload 서버 컨트롤](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [파일의 업로드](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Teresa Murphy 및 박 광 준 Leigh 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](updating-and-deleting-existing-binary-data-cs.md)
> [다음](displaying-binary-data-in-the-data-web-controls-vb.md)
