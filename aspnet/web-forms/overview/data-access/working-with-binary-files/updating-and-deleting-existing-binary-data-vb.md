---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
title: "기존 이진 데이터 (VB) 업데이트 및 삭제 | Microsoft Docs"
author: rick-anderson
description: "이전 자습서에서 어떻게 GridView 컨트롤을 간단히 편집 및 삭제 텍스트 데이터에 살펴보았습니다. 이 자습서에서 GridView 컨트롤 또한 확인 방법을 보기..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: 3a052ced-9cf5-47b8-a400-934f0b687c26
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 8baf187d484424aeaee57f8c57ac391a0ae9e946
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="updating-and-deleting-existing-binary-data-vb"></a>기존 이진 데이터 (VB) 업데이트 및 삭제
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_VB.exe) 또는 [PDF 다운로드](updating-and-deleting-existing-binary-data-vb/_static/datatutorial57vb1.pdf)

> 이전 자습서에서 어떻게 GridView 컨트롤을 간단히 편집 및 삭제 텍스트 데이터에 살펴보았습니다. 이 자습서에서는 어떻게 GridView 컨트롤 쉽게 처리할 수를 편집 하 여 해당 이진 데이터를 데이터베이스에 저장 하거나 파일 시스템에 저장 된 이진 데이터를 삭제 하는 것이 보면 됩니다.


## <a name="introduction"></a>소개

이전 세 개의 자습서를 통해 म 했습니다 많은 양의 이진 데이터로 작업 하기 위한 기능을 추가 합니다. 추가 하 여을 시작 했습니다. 한 `BrochurePath` 열에는 `Categories` 테이블 및이 아키텍처에 따라 업데이트 합니다. 또한 기존 범주 테이블 s 작동 하도록 데이터 액세스 계층 및 비즈니스 논리 계층 메서드를 추가 했습니다 `Picture` 이미지 파일의 이진 콘텐츠 s 보유 하는 열입니다. 범주의 그림에 표시 된 것으로 GridView의 이진 데이터는 브로슈어에 대 한 다운로드 링크를 표시 하는 웹 페이지를 구축 했으므로 `<img>` 요소 및 사용자가 새 범주를 추가 하 고 브로슈어 개요 및 데이터를 업로드할 수 있도록 DetailsView를 추가 했습니다.

모든 작업을 구현 해야 할 나머지 편집 및 편집을 사용 하는 GridView s 기본 제공 및 삭제 기능이이 자습서에서는 위해서는 기존 범주를 삭제할 수 있다는 점입니다. 범주를 편집할 때 사용자는 필요에 따라 새 그림을 업로드 하거나 기존 하나를 사용 하려면 계속의 범주 수. 있습니다 브로슈어에 대 한 새 브로슈어 업로드 또는 범주에 더 이상 연결 된 브로슈어에 나타내기 위해 기존 브로슈어를 사용 하도록 선택할 수 없습니다. Let s가 시작 되었습니다.

## <a name="step-1-updating-the-data-access-layer"></a>1 단계: 업데이트 데이터 액세스 계층

DAL에 자동으로 생성 된 `Insert`, `Update`, 및 `Delete` 메서드, 하지만 이러한 방법에 따라 생성 된는 `CategoriesTableAdapter` 포함 하지 않는 s 주 쿼리에서 `Picture` 열입니다. 따라서는 `Insert` 및 `Update` 메서드 범주의 사진에 대 한 이진 데이터를 지정 하기 위한 매개 변수를 포함 하지 마십시오. 수행한 것 처럼는 [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-vb.md), 업데이트 하기 위한 새 TableAdapter 메서드를 만들어야 하는 `Categories` 이진 데이터를 지정 하는 경우 테이블입니다.

열고 입력 데이터 집합 디자이너에서 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 추가 쿼리 상황에 맞는 메뉴를 선택한 launche TableAdapter 쿼리 구성 마법사. 이 마법사는 요청 하는 TableAdapter 쿼리는 데이터베이스에 액세스 하는 방법으로 시작 합니다. SQL 문 사용을 선택 하 고 클릭 합니다. 다음 단계에서는 메시지를 생성 쿼리 형식에 대 한 표시 합니다. 이후 새 레코드를 추가 하는 쿼리를 만드는 다시 우리는 `Categories` 테이블 업데이트를 선택 하 고 다음을 클릭 합니다.


[![업데이트 옵션을 선택](updating-and-deleting-existing-binary-data-vb/_static/image2.png)](updating-and-deleting-existing-binary-data-vb/_static/image1.png)

**그림 1**: 업데이트 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image3.png))


지금 지정 해야는 `UPDATE` SQL 문입니다. 마법사가 자동으로 제안는 `UPDATE` TableAdapter s 주 쿼리에 해당 하는 문 (업데이트 하는 `CategoryName`, `Description`, 및 `BrochurePath` 값). 문을 변경 하는 `Picture` 열이 함께 포함 됩니다는 `@Picture` 매개 변수를 다음과 같이:


[!code-sql[Main](updating-and-deleting-existing-binary-data-vb/samples/sample1.sql)]

마법사의 마지막 화면에 새 TableAdapter 메서드 이름을 묻는 메시지가 나타납니다. 입력 `UpdateWithPicture` 하 고 마침을 클릭 합니다.


[![새 TableAdapter 메서드 UpdateWithPicture 이름](updating-and-deleting-existing-binary-data-vb/_static/image5.png)](updating-and-deleting-existing-binary-data-vb/_static/image4.png)

**그림 2**: 새 TableAdapter 메서드 이름을 `UpdateWithPicture` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image6.png))


## <a name="step-2-adding-the-business-logic-layer-methods"></a>2 단계: 비즈니스 논리 계층 메서드를 추가합니다.

DAL을 업데이트할 뿐만 아니라 BLL 업데이트 및 범주를 삭제 하는 메서드를 포함 하도록 업데이트 해야 합니다. 이들은 프레젠테이션 계층에서 호출 될 메서드입니다.

범주를 삭제 하는 데 사용할 수는 `CategoriesTableAdapter` 자동 생성 된 s `Delete` 메서드. 다음 메서드를 추가 `CategoriesBLL` 클래스:


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample2.vb)]

이 자습서에서는 let s 만듭니다 그림 이진 데이터를 필요로 하 고 호출 하는 범주-업데이트 하기 위한 두 가지 방법에서 `UpdateWithPicture` 에 방금 추가한 메서드는 `CategoriesTableAdapter` 허용 하는 쿼리와 테이블만 `CategoryName`, `Description`, 및 `BrochurePath`값을 사용 하 여 `CategoriesTableAdapter` s 자동 생성 된 클래스 `Update` 문. 두 가지 방법으로 기초가 되는 경우에 따라 범주의 사진과 새 사진을 업로드할 경우 사용자 갖습니다, 다른 필드를 업데이트 해야 사용자 할 수입니다. 업로드 된 그림 s 이진 데이터에 사용할 수 있습니다는 `UPDATE` 문. 다른 경우에는 사용자만 관심을 가질 수 업데이트, 예를 들어, 이름 및 설명 합니다. 경우에 `UPDATE` 에 대 한 이진 데이터를 필요로 하는 문에 `Picture` 열에도, 그런 다음 d 해야 할 뿐만 아니라 해당 정보를 제공 합니다. 편집 중인 레코드에 대 한 그림 데이터 다시 가져오기 하려면 데이터베이스에 추가로 이동을 해야 합니다. 따라서 원하는 두 개의 `UPDATE` 메서드. 비즈니스 논리 계층 사용할 그림 데이터 범주를 업데이트할 때 제공 여부에 따라 결정 됩니다.

이 작업을 위해 두 개의 메서드를 추가 `CategoriesBLL` 명명 된 클래스 `UpdateCategory`합니다. 첫 번째 3 개를 허용 해야 `String` s는 `Byte` 배열 및 `Integer` 입력으로 매개 변수, 3 초 `String` s 및 `Integer`합니다. `String` s 범주 이름, 설명 및 브로슈어 파일 경로 대 한 입력된 매개 변수는는 `Byte` 배열이 범주의 그림의 이진 콘텐츠 및 `Integer` 식별 된 `CategoryID` 업데이트할 레코드의 합니다. 첫 번째 오버 로드에는 전달 된 두 번째 경우는를 호출 하는 알림 `Byte` 배열이 `Nothing`:


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample3.vb)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>3 단계: 삽입 및 보기 기능을 통해 복사

에 [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-vb.md) 라는 페이지 만든 `UploadInDetailsView.aspx` 는 GridView에 모든 범주를 나열 하 고 시스템에 새 범주를 추가 하려면 DetailsView를 제공 합니다. 이 자습서에서는 GridView 편집 및 삭제 지원 포함 하도록 확장 합니다. 계속 작업 하는 대신 `UploadInDetailsView.aspx`, let s에는 대신에이 자습서 s 변경 내용을 배치는 `UpdatingAndDeleting.aspx` 동일한 폴더의 페이지 `~/BinaryData`합니다. 복사 하거나 선언 태그를 붙여 넣고에서 발생 한 코드 `UploadInDetailsView.aspx` 를 `UpdatingAndDeleting.aspx`합니다.

열어 시작는 `UploadInDetailsView.aspx` 페이지. 모든 선언적 구문 내에서 복사 된 `<asp:Content>` 그림 3에 나와 있는 것 처럼 요소인 합니다. 을 열고 `UpdatingAndDeleting.aspx` 내에서이 태그를 붙여 해당 `<asp:Content>` 요소입니다. 마찬가지로,에서 코드를 복사는 `UploadInDetailsView.aspx` s 코드 숨김 클래스를 페이지 `UpdatingAndDeleting.aspx`합니다.


[![선언적 태그 UploadInDetailsView.aspx에서 복사](updating-and-deleting-existing-binary-data-vb/_static/image8.png)](updating-and-deleting-existing-binary-data-vb/_static/image7.png)

**그림 3**: 복사 된 선언적 태그 `UploadInDetailsView.aspx` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image9.png))


선언적 태그 및 코드를 복사한 후 방문 `UpdatingAndDeleting.aspx`합니다. 출력을 동일한 사용자 환경을 제공 하는 동일한 표시와 마찬가지로 `UploadInDetailsView.aspx` 이전 자습서의 페이지입니다.

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>4 단계: 삭제 ObjectDataSource 및 GridView에 대 한 지원 추가

다시에서 설명한 것 처럼는 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서 기본 삭제 기능을 제공 하는 GridView와 경우 checkbox의 눈금에 이러한 기능을 사용할 수 있습니다 표 s 내부 데이터 소스 삭제를 지원합니다. 현재는 ObjectDataSource GridView에 바인딩됩니다 (`CategoriesDataSource`) 삭제 하는 것을 지원 하지 않습니다.

이 해결 하려면 마법사를 시작 하려면 ObjectDataSource s 스마트 태그에서 데이터 소스 구성 옵션을 클릭 합니다. 첫 번째 화면에 표시 됩니다는 ObjectDataSource 함께 작동 하도록 구성 되는 `CategoriesBLL` 클래스입니다. 다음에 도달 했습니다. 현재만 ObjectDataSource s `InsertMethod` 및 `SelectMethod` 속성을 지정 합니다. 그러나 마법사 자동으로 채워진와 UPDATE 및 DELETE 탭에 있는 드롭 다운 목록에서 `UpdateCategory` 및 `DeleteCategory` 메서드를 각각. ¿¡´에 `CategoriesBLL` 이러한 메서드를 사용 하 여 표시 된 것 클래스는 `DataObjectMethodAttribute` 업데이트 및 삭제 하는 기본적인 방법으로 합니다.

지금은 업데이트의 탭 드롭 다운 목록을 (None), 설정 하지만 삭제의 탭 드롭 다운 목록을로 설정 된 상태로 두고 `DeleteCategory`합니다. 업데이트 지원을 추가 하려면 6 단계에서에서이 마법사에서는 작업을 반환 합니다.


[![ObjectDataSource DeleteCategory 메서드를 사용 하도록 구성](updating-and-deleting-existing-binary-data-vb/_static/image11.png)](updating-and-deleting-existing-binary-data-vb/_static/image10.png)

**그림 4**: 구성에 사용 하 여 ObjectDataSource는 `DeleteCategory` 메서드 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image12.png))


> [!NOTE]
> 마법사를 완료 되 면 Visual Studio 필드 새로 고침 및 키 하려는 경우에 필드 제어 웹 데이터를 다시 생성 됩니다는 요청할 수 있습니다. 예를 선택 하면 필드 사용자 지정 사용자가 변경한 내용이 덮어쓰게 됩니다 아니요를 선택 합니다.


ObjectDataSource에 대 한 값을 포함 합니다 해당 `DeleteMethod` 속성 및 `DeleteParameter`합니다. 메서드를 지정 하는 마법사를 사용할 때 Visual Studio 설정 ObjectDataSource s 회수 `OldValuesParameterFormatString` 속성을 `original_{0}`, 된 업데이트와 함께 문제가 발생 하 고이 메서드 호출을 삭제 합니다. 따라서이 속성을 완전히 지울 또는 기본값으로 다시 설정 `{0}`합니다. 이 ObjectDataSource 속성에 메모리를 새로 고치려면 해야 할 경우 참조는 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서입니다.

마법사를 완료 하 고 수정 후의 `OldValuesParameterFormatString`, ObjectDataSource s 선언 태그는 다음과 같은 유사 합니다.


[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample4.aspx)]

ObjectDataSource를 구성한 후 GridView s 스마트 태그에서 삭제 사용 확인란을 선택 하 여 GridView에 삭제 기능을 추가 합니다. GridView에는 CommandField 추가 됩니다 인 `ShowDeleteButton` 속성이 `True`합니다.


[![GridView에서 삭제에 대 한 지원을 사용 하도록 설정](updating-and-deleting-existing-binary-data-vb/_static/image14.png)](updating-and-deleting-existing-binary-data-vb/_static/image13.png)

**그림 5**: GridView에서 삭제 하는 중에 대 한 지원을 사용 하도록 설정 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image15.png))


충분히 삭제 기능을 테스트해 보십시오. 간의 외래 키가는 `Products` 테이블 s `CategoryID` 및 `Categories` 테이블의 `CategoryID`이므로 처음 8 개 범주 중 하나를 삭제 하려고 하면 외래 키 제약 조건을 위반 예외를 얻을 수 있습니다. Out이 기능을 테스트 하려면 브로슈어와 그림을 제공 하는 새 범주를 추가 합니다. 그림 6에 나와 내 테스트 범주에는 테스트 브로슈어 `Test.pdf` 그림을 테스트 합니다. 그림 7 테스트 범주를 추가한 후 GridView를 보여줍니다.


[![브로슈어 및 이미지를 사용 하 여 테스트 범주를 추가 합니다.](updating-and-deleting-existing-binary-data-vb/_static/image17.png)](updating-and-deleting-existing-binary-data-vb/_static/image16.png)

**그림 6**: 브로슈어 및 이미지를 사용 하 여 테스트 범주 추가 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image18.png))


[![테스트 범주를 삽입 한 후 표시 되는 GridView](updating-and-deleting-existing-binary-data-vb/_static/image20.png)](updating-and-deleting-existing-binary-data-vb/_static/image19.png)

**그림 7**: 테스트 범주를 삽입 한 후 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image21.png))


Visual Studio에서 솔루션 탐색기를 새로 고칩니다. 이제 새 파일에 표시 된 `~/Brochures` 폴더 `Test.pdf` (그림 8 참조).

다음으로 인해 포스트백 페이지가 테스트 범주 행의 삭제 링크를 클릭 및 `CategoriesBLL` s 클래스 `DeleteCategory` 메서드를 발생 하도록 합니다. 이렇게 하면 DAL s `Delete` 에서 메서드는 적절 한 `DELETE` 데이터베이스에 보낼 문의 합니다. 데이터는 GridView에 리바운드 다음 및 태그를 더 이상 존재 테스트 범주를 사용 하 여 클라이언트에 다시 전송 됩니다.

Delete 워크플로에서 테스트 범주 레코드를 성공적으로 제거 하는 동안는 `Categories` 테이블, 웹 서버의 파일 시스템에서 해당 브로슈어 파일을 제거 하지 못했습니다. 솔루션 탐색기를 새로 고치고 확인 하 게 `Test.pdf` 에서 여전히 대기 중임는 `~/Brochures` 폴더입니다.


![Test.pdf 파일이 웹 서버의 파일 시스템에서 삭제 되지 않았습니다.](updating-and-deleting-existing-binary-data-vb/_static/image1.gif)

**그림 8**:는 `Test.pdf` 파일이 웹 서버의 파일 시스템에서 삭제 되지 않았습니다


## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>5 단계: 삭제 된 범주의 브로슈어 파일 제거

데이터베이스 외부의 이진 데이터를 저장할 경우의 단점은 중 하나는 관련된 데이터베이스 레코드가 삭제 될 때 이러한 파일을 정리 하려면 추가 단계를 수행 해야 하입니다. GridView 및 ObjectDataSource 전과 delete 명령의 수행 된 후 실행 하는 이벤트를 제공 합니다. 빌드 전 및 작업 후 이벤트에 대 한 이벤트 처리기를 만드는 실제로 필요 합니다. 전에 `Categories` 레코드가 삭제 되 PDF의 파일 경로 결정 해야 하지만 t 하려는 경우 몇 가지 예외 이며 범주는 삭제 되지 않습니다는 범주를 삭제 하기 전에 PDF를 삭제 하지 않는 것입니다.

GridView s [ `RowDeleting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx) 발생 전에 ObjectDataSource의 삭제 명령을 실행 하는 동안 해당 [ `RowDeleted` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx) 후에 발생 합니다. 다음 코드를 사용 하 여 이러한 두 개의 이벤트에 대 한 이벤트 처리기를 만듭니다.


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample5.vb)]

에 `RowDeleting` 이벤트 처리기는 `CategoryID` 행의 삭제 되는 잡고 GridView s에서 `DataKeys` 컬렉션을 통해이 이벤트 처리기에서 액세스할 수 있는 `e.Keys` 컬렉션입니다. 다음으로 `CategoriesBLL` s 클래스 `GetCategoryByCategoryID(categoryID)` 삭제 하 고 레코드에 대 한 정보를 반환 하기 위해 호출 된 합니다. 하는 경우 반환 된 `CategoriesDataRow` 개체에 비-`NULL``BrochurePath` 값 페이지 변수에 저장 됩니다 `deletedCategorysPdfPath` 파일에서 삭제 될 수 있도록는 `RowDeleted` 이벤트 처리기입니다.

> [!NOTE]
> 검색 하는 대신는 `BrochurePath` 에 대 한 정보는 `Categories` 기록 삭제 되는 것은 `RowDeleting` 이벤트 처리기 수 또는 추가 했습니다는 `BrochurePath` GridView s에 `DataKeyNames` 속성 레코드의 값에 액세스 통해는 `e.Keys` 컬렉션입니다. 이렇게는 약간 GridView의 보기 상태 크기 증가 필요한 코드의 양을 줄일 수 있고 한 이동 하 여 데이터베이스에 저장 합니다.


기본 delete 명령의 s 호출 된 GridView의 ObjectDataSource 후 `RowDeleted` 이벤트 처리기에 발생 합니다. 에 대 한 값이 있으면이 고 예외가 데이터를 삭제 된 경우 `deletedCategorysPdfPath`, PDF 파일 시스템에서 삭제 됩니다. 그림와 관련 된 범주 s 이진 데이터를 정리 하는 데이 추가 코드가 필요 하지 않으므로 참고 합니다. S 그림 데이터에는 데이터베이스에 직접 저장 하므로 삭제 된 `Categories` 행에 해당 범주의 그림 데이터도 삭제 합니다.

두 개의 이벤트 처리기를 추가한 후이 테스트 사례를 다시 실행 합니다. 범주를 삭제할 때 연결 된 해당 PDF도 삭제 됩니다.

기존 레코드 s 연관 된 이진 데이터를 업데이트 몇 가지 흥미로운 문제가 있습니다. 이 자습서의 나머지 부분에서는 업데이트 기능 브로슈어와 그림을 추가 자세하게 합니다. 6 단계 7 단계에서는 그림을 업데이트 하는 동안 브로슈어 정보 업데이트에 대 한 기술 탐색 합니다.

## <a name="step-6-updating-a-category-s-brochure"></a>6 단계: 업데이트 범주의 브로슈어

개요의 삽입, 업데이트 및 삭제 데이터 자습서에서 설명 했 듯이 GridView 원본으로 사용 하는 데이터 원본 적절 하 게 구성 하는 경우 확인란의 틱으로 구현할 수 있는 기본 제공 행 수준 편집 지원을 제공 합니다. 현재는 `CategoriesDataSource` ObjectDataSource let s에 있는 추가 지원, 업데이트를 포함 하도록 아직 구성 되지 않았습니다.

ObjectDataSource의 마법사에서 데이터 소스 구성 링크를 클릭 하 고 두 번째 단계를 진행 합니다. 때문에 `DataObjectMethodAttribute` 에 사용 된 `CategoriesBLL`, 업데이트 드롭 다운 목록을 자동으로 채워져야 할지는 `UpdateCategory` 를 4 개의 입력 매개 변수를 받아들이는 오버 로드 (모든 열에 대 한 하지만 `Picture`). 이 모양을 변경 하는 오버 로드를 사용 하 여 다섯 개의 매개 변수를 사용 합니다.


[![ObjectDataSource 사진에 대 한 매개 변수를 포함 하는 UpdateCategory 방법을 사용 하도록 구성](updating-and-deleting-existing-binary-data-vb/_static/image23.png)](updating-and-deleting-existing-binary-data-vb/_static/image22.png)

**그림 9**: 구성에 사용 하 여 ObjectDataSource는 `UpdateCategory` 에 대 한 매개 변수를 포함 하는 메서드 `Picture` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image24.png))


ObjectDataSource에 대 한 값을 포함 합니다 해당 `UpdateMethod` 속성으로 해당 `UpdateParameter` s입니다. Visual Studio 설정 ObjectDataSource의 4 단계에서에서 설명 했 듯이 `OldValuesParameterFormatString` 속성을 `original_{0}` 데이터 소스 구성 마법사를 사용 하는 경우. 업데이트 문제가 발생 되 고이 메서드 호출을 삭제 합니다. 따라서이 속성을 완전히 지울 또는 기본값으로 다시 설정 `{0}`합니다.

마법사를 완료 하 고 수정 후의 `OldValuesParameterFormatString`, ObjectDataSource s 선언 태그는 다음과 같습니다.


[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample6.aspx)]

GridView s 기본 제공 편집 기능을 활성화 하려면 GridView s 스마트 태그에서 편집 사용 옵션을 선택 합니다. 이렇게 하면 CommandField s 설정 됩니다 `ShowEditButton` 속성을 `True`로 편집 단추 (및 편집 되는 행에 대 한 업데이트 및 취소 단추)를 추가 합니다.


[![GridView 지원 편집 구성](updating-and-deleting-existing-binary-data-vb/_static/image26.png)](updating-and-deleting-existing-binary-data-vb/_static/image25.png)

**그림 10**: GridView 지원 편집 구성 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image27.png))


브라우저를 통해 페이지를 방문 하 고 행의 편집 단추 중 하나를 클릭 합니다. `CategoryName` 및 `Description` BoundFields 입력란으로 렌더링 됩니다. `BrochurePath` TemplateField에 게 없는 경우는 `EditItemTemplate`계속 표시 되므로 해당 `ItemTemplate` 브로슈어에 대 한 링크입니다. `Picture` 갖는 TextBox로 ImageField 렌더링 `Text` 속성 ImageField s의 값이 할당은 `DataImageUrlField` 값,이 경우 `CategoryID`합니다.


[![GridView에 BrochurePath에 대 한 편집 인터페이스 부족](updating-and-deleting-existing-binary-data-vb/_static/image29.png)](updating-and-deleting-existing-binary-data-vb/_static/image28.png)

**그림 11**: GridView에 게 없는 경우에 대 한 편집 인터페이스 `BrochurePath` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image30.png))


## <a name="customizing-thebrochurepaths-editing-interface"></a>사용자 지정의`BrochurePath`s 편집 인터페이스

에 대 한 편집 인터페이스를 만들어야 하는 `BrochurePath` TemplateField 하나를 사용 하면:

- 으로 범주의 브로슈어 둡니다-,
- 새 브로슈어 업로드 하 여 범주의 브로슈어 업데이트 또는
- 범주의 브로슈어 (범주에 더 이상 연결된 브로슈어 된 경우)에 함께 제거 합니다.

또한 업데이트 해야는 `Picture` ImageField s 편집 인터페이스 했지만 합니다 च प ा क 7 단계에서에서.

GridView s 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 선택 된 `BrochurePath` TemplateField의 `EditItemTemplate` 드롭 다운 목록에서 합니다. RadioButtonList 웹 컨트롤 설정이 서식 파일을 추가 해당 `ID` 속성을 `BrochureOptions` 및 해당 `AutoPostBack` 속성을 `True`합니다. 속성 창에서의 줄임표를 클릭 하 고 `Items` 속성이 표시 됩니다는 `ListItem` 컬렉션 편집기입니다. 다음 세 가지 옵션을 추가 `Value`의 1, 2 및 3, 각각.

- 현재 브로슈어 사용
- 현재 브로슈어 제거
- 새 브로슈어 업로드

첫 행 `ListItem` s `Selected` 속성을 `True`합니다.


![세 가지 ListItems RadioButtonList에 추가](updating-and-deleting-existing-binary-data-vb/_static/image2.gif)

**그림 12**: 세 개의 추가 `ListItem`의 RadioButtonList


RadioButtonList 아래 라는 파일 업로드 컨트롤을 추가 `BrochureUpload`합니다. 설정의 `Visible` 속성을 `False`합니다.


[![에 EditItemTemplate RadioButtonList 및 파일 업로드 컨트롤 추가](updating-and-deleting-existing-binary-data-vb/_static/image32.png)](updating-and-deleting-existing-binary-data-vb/_static/image31.png)

**그림 13**: RadioButtonList 및 파일 업로드 컨트롤을 추가 `EditItemTemplate` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image33.png))


이 RadioButtonList 사용자에 대 한 세 가지 옵션을 제공합니다. 업로드 새 브로슈어 마지막 옵션을 선택한 경우에 파일 업로드 컨트롤에 표시 됩니다. 이를 위해 RadioButtonList s에 대 한 이벤트 처리기를 만들고 `SelectedIndexChanged` 이벤트를 다음 코드를 추가 합니다.


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample7.vb)]

RadioButtonList 및 파일 업로드 컨트롤 템플릿 내에서 되므로 약간의 프로그래밍 방식으로 이러한 컨트롤을 액세스 하는 코드를 작성 해야 합니다. `SelectedIndexChanged` radiobuttonlist에 대 한 참조를 전달 된 이벤트 처리기는 `sender` 입력된 매개 변수입니다. 부모를 가져올 RadioButtonList의 제어 및 사용 해야 파일 업로드 컨트롤을 가져오려면는 `FindControl("controlID")` 거기서에서 메서드. 파일 업로드 컨트롤 s RadioButtonList와 파일 업로드 컨트롤에 대 한 참조, 있으면 `Visible` 속성이 `True` 경우에만 RadioButtonList s `SelectedValue` 은 3이 고,이 `Value` 업로드 새 브로슈어에 대 한 `ListItem`.

이 코드 위치에서 편집 인터페이스를 테스트 하는 데 시간이 걸릴 합니다. 행에 대 한 편집 단추를 클릭 합니다. 처음에 사용 하 여 현재 브로슈어 옵션을 선택 해야 합니다. 선택한 인덱스를 변경 하면 다시 게시 합니다. 세 번째 옵션을 선택 하면 파일 업로드 컨트롤을 표시, 숨겨져 그렇지 않은 경우. 편집 단추를 클릭 하면 먼저; 그림 14 나와 편집 인터페이스 그림 15 업로드 새 브로슈어 옵션을 선택한 후 인터페이스를 보여 줍니다.


[![사용 하 여 현재 브로슈어 처음에 옵션을 선택](updating-and-deleting-existing-binary-data-vb/_static/image35.png)](updating-and-deleting-existing-binary-data-vb/_static/image34.png)

**그림 14**: 사용 하 여 현재 브로슈어 처음에 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image36.png))


[![업로드 새 브로슈어 옵션 표시 파일 업로드 컨트롤 선택](updating-and-deleting-existing-binary-data-vb/_static/image38.png)](updating-and-deleting-existing-binary-data-vb/_static/image37.png)

**그림 15**: 업로드 새 브로슈어 옵션 표시 파일 업로드 컨트롤을 선택 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image39.png))


## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>브로슈어 저장 파일 및 업데이트는`BrochurePath`열

GridView s의 [업데이트] 단추를 클릭 하면 해당 `RowUpdating` 이벤트 발생 합니다. S 업데이트 명령이 호출 될 ObjectDataSource와 GridView의 `RowUpdated` 이벤트 발생 합니다. 삭제 워크플로 이러한 이벤트에 대 한 이벤트 처리기를 만드는 필요 합니다. 에 `RowUpdating` 필요에 따라 수행할 작업을 확인 하려면 이벤트 처리기는 `SelectedValue` 의 `BrochureOptions` RadioButtonList:

- 경우는 `SelectedValue` 는 1, 동일한를 계속 사용 하려는 `BrochurePath` 설정 합니다. 따라서 원하므로 설정 해야 ObjectDataSource s `brochurePath` 매개 변수를 기존 `BrochurePath` 업데이트 되는 레코드의 값입니다. ObjectDataSource s `brochurePath` 매개 변수를 사용 하 여 설정할 수 있습니다 `e.NewValues["brochurePath"] = value`합니다.
- 경우는 `SelectedValue` 가 2 인 다음 s 레코드를 설정 하려고 `BrochurePath` 값을 `NULL`합니다. ObjectDataSource s를 설정 하 여이 작업을 수행할 수 있습니다 `brochurePath` 매개 변수를 `Nothing`, 데이터베이스를 만드는 `NULL` 에 사용 되는 `UPDATE` 문. 기존 브로슈어 파일 제거 되는 경우 기존 파일을 삭제 해야 합니다. 그러나만 하고자 예외를 발생 시키는 없이 업데이트가 완료 된 경우이 작업을 수행 합니다.
- 경우는 `SelectedValue` 하 사용자가을 PDF 파일로 업로드 있는지 확인 한 다음 파일 시스템에 저장 하 고 s 레코드를 업데이트 한 후에 3 `BrochurePath` 열 값입니다. 또한 기존 브로슈어 파일 대체 되는 경우 이전 파일을 삭제 해야 합니다. 그러나만 하고자 예외를 발생 시키는 없이 업데이트가 완료 된 경우이 작업을 수행 합니다.

때 완료 하는 데 필요한 단계 RadioButtonList s `SelectedValue` 은 3 DetailsView s에 의해 사용 되는 거의 동일 `ItemInserting` 이벤트 처리기입니다. 이 이벤트 처리기에 추가 된 DetailsView 컨트롤에서 새 범주 레코드가 추가 될 때 실행 되는 [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-vb.md)합니다. 따라서 별도 메서드로 아웃이 기능을 리팩터링 하 behooves 합니다. 특히, I 제외 공통 기능 두 개의 메서드로:

- `ProcessBrochureUpload(FileUpload, out bool)`파일 업로드 컨트롤 인스턴스 및 일부 유효성 검사 오류로 인해 취소 되도록 하는 경우 또는 삭제 또는 편집 작업을 계속할지 여부를 지정 하는 출력 부울 값을 입력으로 받아들입니다. 이 메서드는 저장 된 파일에 경로 반환 하거나 `null` 없는 파일을 저장 하는 경우.
- `DeleteRememberedBrochurePath`페이지 변수에서 경로 지정 된 파일을 삭제 `deletedCategorysPdfPath` 경우 `deletedCategorysPdfPath` 않습니다 `null`합니다.

이러한 두 가지 방법에 대 한 코드를 따릅니다. 사이의 유사성 확인 `ProcessBrochureUpload` 및 DetailsView의 `ItemInserting` 이전 자습서에서 이벤트 처리기입니다. 이 자습서에서는 이러한 새 메서드를 사용 하는 DetailsView의 이벤트 처리기가 업데이트 합니다. DetailsView의 이벤트 처리기의 수정 내용을 확인 하려면이 자습서와 연결 된 코드를 다운로드 합니다.


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample8.vb)]

GridView s `RowUpdating` 및 `RowUpdated` 사용 하 여 이벤트 처리기는 `ProcessBrochureUpload` 및 `DeleteRememberedBrochurePath` 메서드에 다음 코드 에서처럼:


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample9.vb)]

참고 방법을 `RowUpdating` 이벤트 처리기는 일련의 조건문을 사용 하 여에 따라 적절 한 조치를 수행 하는 `BrochureOptions` RadioButtonList의 `SelectedValue` 속성 값입니다.

이 코드 위치에서 범주를 편집 하 고 해당 현재 브로슈어 사용 하거나, 없습니다 브로슈어 사용 하거나 업로드 한 새 하 게 사용할 수 있습니다. 계속 해 서 항목을 사용해 보세요. 중단점을 설정는 `RowUpdating` 및 `RowUpdated` 파악할 수 있는 워크플로 이벤트 처리기입니다.

## <a name="step-7-uploading-a-new-picture"></a>7 단계: 새 사진을 업로드

`Picture` ImageField s의 값으로 채워진 textbox로 인터페이스 렌더링 편집 해당 `DataImageUrlField` 속성입니다. 편집 워크플로 중 GridView에서 매개 변수 전달 된 매개 변수의 이름과 ObjectDataSource ImageField의 값 `DataImageUrlField` 속성 및 매개 변수 s 값 편집 인터페이스에서 텍스트 상자에 입력 한 값입니다. 이 동작은 적합 한 이미지 파일 시스템에 파일로 저장 되 고 `DataImageUrlField` 이미지의 전체 URL을 포함 합니다. 이 경우와 편집 인터페이스는 사용자를 변경할 수 있으며 데이터베이스에 다시 저장 하는 텍스트 상자에 이미지의 URL을 표시 합니다. 이 기본 인터페이스 대상이 t 부여 새 이미지를 업로드 하는 데 사용할 수 주지만 마법사를 통해 현재 값에서 다른 이미지의 URL을 변경 하지 않습니다. 그러나이 자습서에서는 편집 인터페이스 ImageField의 기본 충분 하지 않은 때문에 `Picture` 데이터베이스에 직접 저장 되는 이진 데이터 및 `DataImageUrlField` 속성에 저장 하면 `CategoryID`합니다.

사용자는 이미지 필드를 사용 하 여 행을 편집할 때이 자습서에서 발생 하는 기능을 더 잘 이해 하려면 다음 예제를 참조 하세요.: 사용자가 포함 된 행을 편집 `CategoryID` 일으키는 10는 `Picture` ImageField 값 10 textbox로 렌더링 하 합니다. 사용자를 50이이 입력란에 값을 변경 하 고 업데이트 단추를 클릭 한다고 가정 합니다. 포스트백이 발생할 및 GridView 라는 매개 변수를 처음으로 만든 `CategoryID` 50 값을 사용 합니다. 그러나 GridView에서이 매개 변수를 전송 하기 전에 (및 `CategoryName` 및 `Description` 매개 변수), 쿼리의 값에 추가 `DataKeys` 컬렉션입니다. 따라서 덮어씁니다는 `CategoryID` 매개 변수를 현재 행 s 기본 `CategoryID` 값을 10입니다. 즉, ImageField s 편집 인터페이스에 영향을 주지 않습니다에 편집 워크플로이 자습서에 대 한 ImageField s의 이름을 `DataImageUrlField` 속성 및 표의 `DataKey` 값은 동일한 합니다.

이미지 필드를 사용 하면 쉽게 데이터베이스 데이터를 기반으로 이미지를 표시 하려면, t 편집 인터페이스에는 입력란을 제공 하려는 않는 했습니다. 대신, 최종 사용자는 범주의 그림을 변경 하는 데 사용할 수 있는 파일 업로드 컨트롤을 제공 하려고 합니다. 와 달리는 `BrochurePath` 값을 이러한 자습서에서는 각 범주는 그림 있어야 해야 할 하기로 결정 했습니다. 사용자로 현재 그림을 주거나 그림이 없습니다. 연결 된 사용자.vhd 새 그림 수 없다는 메시지가 t 필요 하지 않는 म 따라서-됩니다.

ImageField s 편집 인터페이스를 사용자 지정 하려면를 TemplateField로 변환 해야 합니다. GridView s 스마트 태그에서 열 편집 링크를 클릭 하 고 이미지 필드를 선택한를 TemplateField 링크로 Convert이이 필드를 클릭 합니다.


![이미지 필드를 TemplateField로 변환](updating-and-deleting-existing-binary-data-vb/_static/image3.gif)

**그림 16**:는 이미지 필드를 TemplateField로 변환


템플릿 두 TemplateField 생성의 이미지 필드를 TemplateField 이러한 방식으로 변환 합니다. 다음과 같은 선언 구문을 볼 수 있듯이 `ItemTemplate` 포함 이미지 웹 컨트롤 `ImageUrl` ImageField s에 따라 데이터 바인딩을 구문을 사용 하 여 속성에 할당 되 `DataImageUrlField` 및 `DataImageUrlFormatString` 속성입니다. `EditItemTemplate` TextBox를 포함 인 `Text` 에 지정 된 값에 바인딩되는 `DataImageUrlField` 속성입니다.


[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample10.aspx)]

업데이트 해야는 `EditItemTemplate` 파일 업로드 컨트롤을 사용 합니다. 템플릿 편집에서 s 스마트 태그를 클릭 하 여 GridView에서 연결 하 고 다음 선택에서 `Picture` TemplateField의 `EditItemTemplate` 드롭 다운 목록에서 합니다. 서식 파일에서이 줄을 제거 하는 텍스트 상자가 표시 됩니다. 다음으로로 설정 하 고 서식 파일을 도구 상자에서 파일 업로드 컨트롤을 끌어 해당 `ID` 를 `PictureUpload`합니다. 또한 범주의 사진 변경, 새 기호를 지정 하려면 텍스트를 추가 합니다. 을 유지 하기 위해 범주의 그림 동일한 필드를 비워 둡니다 해당 템플릿으로 합니다.


[![EditItemTemplate에 파일 업로드 컨트롤 추가](updating-and-deleting-existing-binary-data-vb/_static/image41.png)](updating-and-deleting-existing-binary-data-vb/_static/image40.png)

**그림 17**: 파일 업로드 컨트롤을 추가 `EditItemTemplate` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image42.png))


편집 인터페이스를 사용자 지정한 후 브라우저에서 진행률을 보고 합니다. 읽기 전용 모드에서 한 행을 볼 때 과거에 있지만 파일 업로드 컨트롤이 있는 텍스트로 그림 열 렌더링 편집 단추를 클릭 하 여 범주의 이미지가 표시 됩니다.


[![한 파일 업로드 컨트롤을 포함 하는 편집 인터페이스](updating-and-deleting-existing-binary-data-vb/_static/image44.png)](updating-and-deleting-existing-binary-data-vb/_static/image43.png)

**그림 18**: 한 파일 업로드 컨트롤을 포함 하는 편집 인터페이스 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image45.png))


ObjectDataSource 호출 하도록 구성 되며 회수는 `CategoriesBLL` s 클래스 `UpdateCategory` 그림에 대 한 이진 데이터를 입력으로 허용 하는 메서드는 `Byte` 배열입니다. 그러나이 배열이 `Nothing`, 대체 `UpdateCategory` 오버 로드를 호출한는 문제는 `UPDATE` 수정 하지 않는 SQL 문을 `Picture` 열을 함으로써 현재 s 범주를 두면 그림 그대로 유지 합니다. GridView s에 따라서 `RowUpdating` 프로그래밍 방식으로 참조 해야 하는 이벤트 처리기는 `PictureUpload` 파일 업로드를 제어 하 고 파일을 업로드 하는 경우를 결정 합니다. 수행 하는 경우 업로드 되지 않았습니다 *하지* 에 대 한 값을 지정 하는 `picture` 매개 변수입니다. 반면에 파일을 업로드 하는 경우에 `PictureUpload` JPG 파일 인지 확인 하고자 하는 파일 업로드 컨트롤입니다. 이진 내용을 통해 ObjectDataSource을 받을 경우 이기는 `picture` 매개 변수입니다.

DetailsView s에 있는 대부분 이미 여기에 필요한 코드의 6 단계에서에서 사용 되는 코드와 마찬가지로 `ItemInserting` 이벤트 처리기입니다. 따라서 I 했습니다 새 메서드로 공통 기능을 리팩터링 `ValidPictureUpload`, 업데이트는 `ItemInserting` 이 방법을 사용 하려면 이벤트 처리기입니다.

GridView s의 시작 부분에 다음 코드를 추가 `RowUpdating` 이벤트 처리기입니다. 것이 코드에서는 인할 이후 브로슈어 파일을 저장 하는 코드 보다 먼저 편중 s 그림이 잘못 되었습니다. 파일을 업로드 하는 경우 브로슈어 웹 서버의 파일 시스템에 저장 하려면.


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample11.vb)]

`ValidPictureUpload(FileUpload)` 되므로 그림 파일을 업로드 하는 경우만 라고 메서드 유일한 입력된 매개 변수로 파일 업로드 컨트롤에서 사용 하 고 업로드 한 파일은 JPG 되는지 알아보려면 s 업로드 된 파일 확장을 확인 합니다. 없는 파일을 업로드 경우 그림 매개 변수는 설정 하지 않으면 하 고 따라서의 기본값을 사용 하 여 `Nothing`합니다. 사진을 업로드 하는 경우 및 `ValidPictureUpload` 반환 `True`, `picture` 매개 변수가 메서드가 반환 하는 경우 업로드 된 이미지의 이진 데이터를 할당 된 `False`업데이트 워크플로 취소 하 고 이벤트 처리기가 종료 되었습니다.

`ValidPictureUpload(FileUpload)` 는 DetailsView s에서 리팩터링 메서드 코드에서 `ItemInserting` 이벤트 처리기가 따르는:


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample12.vb)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>8 단계: Jpg 바꿉니다 원래 범주 그림을

원래 8 범주 그림을 OLE 머리글에 래핑된 비트맵 파일로 점에 유의 하세요. 기존 레코드의 그림을 편집 하는 기능을 추가 했으므로 했으므로 잠시 Jpg 이러한 비트맵 바꿉니다. 현재 범주 그림 사용 하려면 계속 하려는 경우 다음 단계를 수행 하 여 Jpg 변환할 수 있습니다.

1. 비트맵 이미지를 하드 드라이브에 저장 합니다. 방문는 `UpdatingAndDeleting.aspx` 브라우저에서 페이지를 처음 8 개 범주를 각각에 대 한 이미지를 마우스 오른쪽 단추로 클릭 하 고 그림을 저장 하도록 선택 합니다.
2. 선택한 이미지 편집기에 이미지를 엽니다. 예를 들어 Microsoft 그림판을 사용할 수 있습니다.
3. JPG 이미지는 비트맵을 저장 합니다.
4. JPG 파일을 사용 하 여 편집 인터페이스를 통해 범주의 그림을 업데이트 합니다.

범주를 편집 하 고 JPG 이미지를 업로드 한 후 이미지 렌더링 되지 것입니다는 브라우저에서 때문에 `DisplayCategoryPicture.aspx` 페이지는 처음 8 개 범주 중 사용 된 그림에서 첫 번째 78 바이트를 제거 합니다. OLE 머리글 제거를 수행 하는 코드를 제거 하 여이 문제를 해결 합니다. 이 작업을 수행한 후의 `DisplayCategoryPicture.aspx``Page_Load` 이벤트 처리기를 다음 코드로 있어야 합니다.


[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample13.vb)]

> [!NOTE]
> `UpdatingAndDeleting.aspx` 삽입 및 인터페이스 편집 페이지 s 약간 더 많은 작업을 사용할 수 있습니다. `CategoryName` 및 `Description` DetailsView 및 GridView BoundFields TemplateFields로 변환 되어야 합니다. 이후 `CategoryName` 하지 못하도록 `NULL` 값을 한 RequiredFieldValidator 추가 해야 합니다. 및 `Description` TextBox를 여러 줄 텍스트 상자에 변환할 때문일 수 있습니다. I 이러한 마무리 작업을 실행으로 둡니다.


## <a name="summary"></a>요약

이 자습서 모양에 이진 데이터 작업을 완료 합니다. 이 자습서 및 이전 3에 살펴보았습니다 방법을 이진 데이터는 데이터베이스 내에서 직접 또는 파일 시스템에 저장할 수 있습니다. 사용자의 하드 드라이브에서 파일을 선택 하 고 있는 파일 시스템에 저장 하거나 이동할 수 있습니다이 데이터베이스에 삽입 웹 서버에 업로드 하 여 시스템에 이진 데이터를 제공 합니다. ASP.NET 2.0에는 이러한는 기대에 맞게 끌어서 놓기 인터페이스를 제공 하는 파일 업로드 컨트롤이 포함 됩니다. 그러나 설명한 것 처럼는 [파일 업로드](uploading-files-vb.md) 자습서, 파일 업로드 컨트롤은만 상대적으로 적은 파일 업로드는 메가바이트를 초과 하지 않는 이상적으로 적합 합니다. 또한에서 살펴본 편집 하 고 기존 레코드에서 이진 데이터를 삭제 하는 방법 뿐만 아니라 기본 데이터 모델을 업로드 한 데이터를 연결 하는 방법입니다.

자습서의 다음 집합에는 다양 한 캐싱 기술을 탐색합니다. 캐싱은 응용 프로그램 s 높이 수단을 제공 비용이 많이 드는 작업의 결과 가져오고 보다 신속 하 게 액세스할 수 있는 위치에 저장 하 여 전체 성능을 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피의 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](including-a-file-upload-option-when-adding-a-new-record-vb.md)
