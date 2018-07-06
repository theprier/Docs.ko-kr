---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
title: 기존 이진 데이터 (C#) 업데이트 및 삭제 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 어떻게 GridView 컨트롤을 간단히 편집 및 텍스트 데이터를 삭제 하는 것이 살펴보았습니다. 이 자습서에서 GridView 컨트롤도 확인 하는 방법을 참조 하는 중...
ms.author: aspnetcontent
ms.date: 03/27/2007
ms.assetid: 35798f21-1606-434b-83f8-30166906ef49
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
msc.type: authoredcontent
ms.openlocfilehash: d38f549004265810e80d09eeacd30bc6d640ae6c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804254"
---
<a name="updating-and-deleting-existing-binary-data-c"></a>기존 이진 데이터 (C#) 업데이트 및 삭제
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_CS.exe) 또는 [PDF 다운로드](updating-and-deleting-existing-binary-data-cs/_static/datatutorial57cs1.pdf)

> 이전 자습서에서 어떻게 GridView 컨트롤을 간단히 편집 및 텍스트 데이터를 삭제 하는 것이 살펴보았습니다. 이 자습서에서 알 수 방법을 GridView 컨트롤 하기가 편집 하 고 해당 이진 데이터를 데이터베이스에 저장 되는지 아니면 파일 시스템에 저장 된 이진 데이터를 삭제할 수 있습니다.


## <a name="introduction"></a>소개

이전 세 개의 자습서를 통해에서는 많은 양의 이진 데이터 작업에 대 한 기능을 추가 했습니다. 추가 하 여 시작 하는 것을 `BrochurePath` 열을는 `Categories` 테이블 및 아키텍처를 적절 하 게 업데이트 합니다. 또한 범주 테이블 s 기존 작업 하도록 데이터 액세스 계층 및 비즈니스 논리 계층 메서드를 추가 했습니다 `Picture` 이미지 파일의 이진 콘텐츠 s를 포함 하는 열입니다. 범주의 그림의를 사용 하 여 GridView의 이진 데이터를 브로슈어 다운로드 링크를 표시 하는 웹 페이지를 만들었습니다는 `<img>` 요소 기능이 사용자가 새 범주를 추가 하 여 해당 브로슈어 및 그림 데이터 업로드를 허용 하도록 DetailsView를 추가 합니다.

모든 주기 구현를 편집 하 고 편집을 사용 하는 GridView가 기본 제공 및 삭제 기능이이 자습서를 위해 수 있는 기존 범주를 삭제할 수 있습니다. 범주를 편집할 때 사용자 필요에 따라 새 사진을 업로드 하거나 기존 하나를 사용 하려면 계속 범주 수 됩니다. 브로슈어, 또는 사용 하 여 기존 브로슈어 새 브로슈어 업로드할 범주 연관 브로슈어 이상에 있음을 나타내기 위해 선택할 수 없습니다. Let s 시작!

## <a name="step-1-updating-the-data-access-layer"></a>1 단계: 업데이트 데이터 액세스 계층

DAL에 자동으로 생성 된 `Insert`, `Update`, 및 `Delete` 메서드에만 이러한 방법에 따라 생성 된 합니다 `CategoriesTableAdapter` s 기본 쿼리에 포함 하지 않는 `Picture` 열입니다. 따라서 합니다 `Insert` 고 `Update` 메서드 범주의 그림에 대 한 이진 데이터를 지정 하는 것에 대 한 매개 변수를 포함 하지 마십시오. 수행한 것 처럼 합니다 [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-cs.md), 업데이트에 대 한 새 TableAdapter 메서드를 만들어야 합니다 `Categories` 이진 데이터를 지정 하는 경우 테이블입니다.

입력 데이터 집합을 열고, 디자이너에서 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 추가 쿼리 상황에 맞는 메뉴를 선택한 launche TableAdapter 쿼리 구성 마법사. 이 마법사가 TableAdapter 쿼리가 데이터베이스에 액세스 해야 하는 방법을 궁금해 하 여 시작 됩니다. SQL 문 사용을 선택 하 고 클릭 합니다. 다음 단계를 생성할 쿼리 형식에 대 한 라는 메시지가 나타납니다. 새 레코드를 추가 하는 쿼리를 만드는 다시 이후로 `Categories` 테이블 업데이트를 선택 하 고 다음을 클릭 합니다.


[![업데이트 옵션을 선택 합니다.](updating-and-deleting-existing-binary-data-cs/_static/image1.gif)](updating-and-deleting-existing-binary-data-cs/_static/image1.png)

**그림 1**: 업데이트 옵션을 선택 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image2.png))


이제 지정 해야 합니다 `UPDATE` SQL 문입니다. 마법사가 자동으로 제안를 `UPDATE` TableAdapter s 주 쿼리에 해당 하는 문 (업데이트 하는 것을 `CategoryName`, `Description`, 및 `BrochurePath` 값). 문을 변경 하는 `Picture` 열이 함께 포함 됩니다는 `@Picture` 매개 변수를 다음과 같이:


[!code-sql[Main](updating-and-deleting-existing-binary-data-cs/samples/sample1.sql)]

마법사의 마지막 화면 새 TableAdapter 메서드 이름을 묻는 메시지가 나타납니다. 입력 `UpdateWithPicture` 하 고 마침을 클릭 합니다.


[![새 TableAdapter 메서드 UpdateWithPicture 이름](updating-and-deleting-existing-binary-data-cs/_static/image2.gif)](updating-and-deleting-existing-binary-data-cs/_static/image3.png)

**그림 2**: 새 TableAdapter 메서드 이름을 `UpdateWithPicture` ([클릭 하 여 큰 이미지 보기](updating-and-deleting-existing-binary-data-cs/_static/image4.png))


## <a name="step-2-adding-the-business-logic-layer-methods"></a>2 단계: 비즈니스 논리 계층 메서드를 추가합니다.

DAL을 업데이트 하는 것 외에도 업데이트 및 범주를 삭제 하는 메서드를 포함 하는 BLL을 업데이트 해야 합니다. 이들은 프레젠테이션 계층에서 호출 되는 방법입니다.

범주 삭제에 대해 사용할 수 있습니다 합니다 `CategoriesTableAdapter` 자동으로 생성 된 s `Delete` 메서드. 다음 메서드를 추가 합니다 `CategoriesBLL` 클래스:


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample2.cs)]

이 자습서에서는 s let-그림 이진 데이터를 필요로 하 고 호출 하는 범주를 업데이트 하기 위한 두 메서드를 만듭니다는 `UpdateWithPicture` 에 방금 추가한 메서드를 `CategoriesTableAdapter` 허용 하 고 다른 요소만 `CategoryName`, `Description`, 및 `BrochurePath`값을 사용 하 여 `CategoriesTableAdapter` 가 자동으로 생성 된 클래스 `Update` 문입니다. 두 메서드를 사용 하 여 기초가 되는 경우에 따라서는 범주의 그림 새 그림을 업로드할 경우 사용자가 해당 다른 필드와 함께 업데이트 하는 사용자 할 수 있습니다. 업로드 된 그림 s 이진 데이터에서 사용할 수 있습니다는 `UPDATE` 문입니다. 다른 경우에는 사용자만 유용할 수 업데이트, 예를 들어, 이름 및 설명 합니다. 경우에 `UPDATE` 에 대 한 이진 데이터를 필요로 하는 문을 `Picture` 열 물론 그런 다음 d 해야 해당 정보를 제공 합니다. 이 데이터베이스를 편집 중인 레코드에 대 한 그림 데이터 다시 가져오기에 추가로 이동을 해야 합니다. 따라서 원하는 두 `UPDATE` 메서드. 비즈니스 논리 계층에 범주를 업데이트 하는 경우 그림 데이터 제공 여부에 따라 결정 됩니다.

이 작업을 위해 두 개의 메서드를 추가 합니다 `CategoriesBLL` 명명 된 클래스 `UpdateCategory`합니다. 세 번째 허용 해야 `string` s를 `byte` 배열 및 `int` 입력으로 매개 변수, 3 초 `string` s 및 `int`합니다. `string` s 범주 이름, 설명 및 브로슈어 파일 경로 대 한 입력된 매개 변수는 합니다 `byte` 배열이 범주의 그림의 이진 내용에 대 한 및 `int` 하 게 식별 하는 `CategoryID` 업데이트할 레코드의 합니다. 첫 번째 오버 로드에는 전달 된 두 번째 경우를 호출 하는 공지 `byte` 배열이 `null`:


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample3.cs)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>3 단계: 삽입 및 보기 기능을 통해 복사

에 [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-cs.md) 라는 페이지를 만들었습니다 `UploadInDetailsView.aspx` GridView의 모든 범주를 나열 하 고 시스템에 새 범주를 추가할 DetailsView를 제공 합니다. 이 자습서에서 GridView 편집 및 삭제 지원을 포함 하도록 확장 합니다. 계속 작업 하는 대신 `UploadInDetailsView.aspx`, let s에는 대신에이 자습서가 변경 내용을 배치 합니다 `UpdatingAndDeleting.aspx` 동일한 폴더에서 페이지 `~/BinaryData`합니다. 복사 및 선언적 태그를 붙여 넣은 코드에서 `UploadInDetailsView.aspx` 에 `UpdatingAndDeleting.aspx`입니다.

열어서 시작 합니다 `UploadInDetailsView.aspx` 페이지입니다. 모든 선언적 구문 내에서 복사를 `<asp:Content>` 그림 3 에서처럼 요소입니다. 다음으로 열기 `UpdatingAndDeleting.aspx` 내에서이 태그를 붙여 해당 `<asp:Content>` 요소입니다. 마찬가지로,에서 코드를 복사 합니다 `UploadInDetailsView.aspx` s 코드 숨김 클래스 페이지 `UpdatingAndDeleting.aspx`합니다.


[![UploadInDetailsView.aspx에서 선언적 태그를 복사 합니다.](updating-and-deleting-existing-binary-data-cs/_static/image3.gif)](updating-and-deleting-existing-binary-data-cs/_static/image5.png)

**그림 3**:에서 선언적 태그 복사 `UploadInDetailsView.aspx` ([클릭 하 여 큰 이미지 보기](updating-and-deleting-existing-binary-data-cs/_static/image6.png))


선언적 태그 및 코드를 복사한 후 방문 `UpdatingAndDeleting.aspx`합니다. 동일한 출력 및 동일한 사용자 환경을 표시와 마찬가지로 `UploadInDetailsView.aspx` 이전 자습서에서 페이지입니다.

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>4 단계: 추가 ObjectDataSource에 GridView 지원 삭제

다시에서 설명한 대로 합니다 [An 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서에서는 기본 삭제 기능을 제공 하는 GridView 및 경우 확인란의 눈금에서 이러한 기능을 사용할 수 있습니다 기본 표 s 데이터 소스에서 삭제를 지원 합니다. 현재 ObjectDataSource GridView에 바인딩된 (`CategoriesDataSource`) 삭제 하는 것을 지원 하지 않습니다.

이 문제를 해결 하려면 마법사를 시작 하려면 ObjectDataSource가 스마트 태그에서 데이터 소스 구성 옵션을 클릭 합니다. 첫 번째 화면에는 ObjectDataSource를 사용 하도록 구성 되어 있는지를 표시 합니다 `CategoriesBLL` 클래스입니다. 다음을 누릅니다. 현재만 ObjectDataSource s `InsertMethod` 고 `SelectMethod` 속성을 지정 합니다. 그러나 마법사를 자동으로 채워진 드롭다운 목록을 사용 하 여 UPDATE 및 DELETE 탭에는 `UpdateCategory` 고 `DeleteCategory` 메서드를 각각. 때문에 이것이에 `CategoriesBLL` 클래스를 사용 하 여 이러한 메서드를 표시 하는 것을 `DataObjectMethodAttribute` 업데이트 및 삭제에 대 한 기본 메서드로 합니다.

이제 업데이트의 탭 드롭 다운 목록 (None)으로 설정 되지만 삭제의 탭 드롭 다운 목록을로 설정 된 상태로 두고 `DeleteCategory`합니다. 업데이트 지원을 추가 하려면 단계 6에서이 마법사를 반환 합니다.


[![DeleteCategory 메서드를 사용 하는 ObjectDataSource 구성](updating-and-deleting-existing-binary-data-cs/_static/image4.gif)](updating-and-deleting-existing-binary-data-cs/_static/image7.png)

**그림 4**: ObjectDataSource 사용 하도록 구성 된 `DeleteCategory` 메서드 ([클릭 하 여 큰 이미지 보기](updating-and-deleting-existing-binary-data-cs/_static/image8.png))


> [!NOTE]
> 마법사를 완료 하면 Visual Studio 필드 새로 고침 및 키 하려는 경우에 필드 제어 웹 데이터를 다시 생성 됩니다는 요청할 수 있습니다. 예를 선택 하면 사용자가 변경한 필드 사용자 지정 덮어씁니다. 아니요를 선택 합니다.


ObjectDataSource에 대 한 값에는 이제 해당 `DeleteMethod` 속성 뿐만 `DeleteParameter`합니다. 메서드를 지정 하는 마법사를 사용 하는 경우 Visual Studio 설정 ObjectDataSource s 회수 `OldValuesParameterFormatString` 속성을 `original_{0}`, 업데이트를 사용 하 여 문제가 발생 하며 메서드 호출을 삭제 합니다. 따라서이 속성을 완전히 지울 또는 기본값으로 재설정 `{0}`합니다. 이 ObjectDataSource 속성에 대해 메모리를 새로 고치는 경우 참조를 [An 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서입니다.

마법사를 완료 하 고 해결 한 후의 `OldValuesParameterFormatString`, ObjectDataSource가 선언적 태그는 다음과 유사 합니다.


[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample4.aspx)]

ObjectDataSource를 구성한 후 삭제 하 여 기능을 추가할 GridView GridView가 스마트 태그에서 삭제 사용 확인란을 선택 합니다. GridView에는 CommandField 추가이입니다 `ShowDeleteButton` 속성이 `true`합니다.


[![GridView의 삭제에 대 한 지원을 사용 하도록 설정](updating-and-deleting-existing-binary-data-cs/_static/image5.gif)](updating-and-deleting-existing-binary-data-cs/_static/image9.png)

**그림 5**: GridView에는 삭제에 대 한 지원을 사용 하도록 설정 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image10.png))


시간을 내어 삭제 기능을 테스트 합니다. 간의 외래 키가를 `Products` 테이블 s `CategoryID` 및 `Categories` s 테이블 `CategoryID`이므로 처음 8 개 범주 중 하나를 삭제 하려고 하면 외래 키 제약 조건 위반 예외를 얻을 수 있습니다. Out이 기능을 테스트 하려면 브로슈어 및 그림을 제공 하는 새 범주를 추가 합니다. 그림 6 에서처럼 내 테스트 범주 라는 테스트 브로슈어 파일을 포함 `Test.pdf` 그림을 테스트 합니다. 그림 7 테스트 범주를 추가한 다음 GridView를 보여 줍니다.


[![브로슈어 및 이미지를 사용 하 여 테스트 범주를 추가 합니다.](updating-and-deleting-existing-binary-data-cs/_static/image6.gif)](updating-and-deleting-existing-binary-data-cs/_static/image11.png)

**그림 6**: 브로슈어 및 이미지를 사용 하 여 테스트 범주를 추가 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image12.png))


[![테스트 범주를 삽입 한 후 GridView에 표시 됩니다.](updating-and-deleting-existing-binary-data-cs/_static/image7.gif)](updating-and-deleting-existing-binary-data-cs/_static/image13.png)

**그림 7**: 테스트 범주를 삽입 한 후 GridView에 표시 됩니다 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image14.png))


Visual Studio에서 솔루션 탐색기를 새로 고칩니다. 이제 새 파일에 표시 된 `~/Brochures` 폴더를 `Test.pdf` (그림 8 참조).

다음으로 인해 페이지가 포스트백 테스트 범주 행의 삭제 링크를 클릭 하며 `CategoriesBLL` s 클래스 `DeleteCategory` 메서드를 실행 합니다. DAL s 이렇게 하면 `Delete` 메서드를 적절 한 일으키는 `DELETE` 문은 데이터베이스를 전송할 수 있도록 합니다. 데이터는 다음 다시 바인딩 해 서 GridView 및 태그를 더 이상 제공 되지 테스트 범주를 사용 하 여 클라이언트로 다시 전송 됩니다.

삭제 워크플로 테스트 범주 레코드를 성공적으로 제거 하는 동안는 `Categories` 테이블 웹의 서버 파일 시스템에서 해당 브로슈어 파일을 제거 하지는 않았습니다. 솔루션 탐색기를 새로 고치고 확인할 수 있습니다 `Test.pdf` 에서 계속 대기 중임을 `~/Brochures` 폴더입니다.


![Test.pdf 파일을 웹 서버 파일 시스템에서 삭제 되지 않았습니다.](updating-and-deleting-existing-binary-data-cs/_static/image8.gif)

**그림 8**:는 `Test.pdf` 웹의 서버 파일 시스템에서 파일이 삭제 되지 않았습니다


## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>5 단계: 삭제 된 범주의 브로슈어 파일 제거

데이터베이스 외부의 이진 데이터를 저장 하는 단점 중 하나에 연결 된 데이터베이스 레코드가 삭제 될 때 이러한 파일을 정리 하려면 추가 단계를 수행 해야 하입니다. GridView 및 ObjectDataSource 전과 삭제 명령을 수행한 후 실행 하는 이벤트를 제공 합니다. 실제로 사전 및 사후 작업 이벤트에 대 한 이벤트 처리기를 생성 해야 합니다. 전에 `Categories` 레코드가 삭제 되 PDF의 파일 경로 확인 해야 하지만 t 하려는 경우에 몇 가지 예외가 범주 삭제 되지 않습니다 범주를 삭제 하기 전에 PDF를 삭제 하지 것입니다.

GridView s [ `RowDeleting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx) 발생 하는 동안 ObjectDataSource가의 삭제 명령을 호출 되기 전에 해당 [ `RowDeleted` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx) 후 발생 합니다. 다음 코드를 사용 하 여 이러한 두 이벤트에 대 한 이벤트 처리기를 만듭니다.


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample5.cs)]

에 `RowDeleting` 이벤트 처리기는 `CategoryID` 행의 GridView s에서 놓은 삭제할 `DataKeys` 컬렉션을 통해이 이벤트 처리기에 액세스할 수 있는 `e.Keys` 컬렉션. 다음으로 `CategoriesBLL` s 클래스 `GetCategoryByCategoryID(categoryID)` 삭제할 레코드에 대 한 정보를 반환 하기 위해 호출 됩니다. 하는 경우 반환 된 `CategoriesDataRow` 개체에 비-`NULL``BrochurePath` 페이지 변수에 저장 된 다음 값 `deletedCategorysPdfPath` 파일에서 삭제 될 수 있도록 합니다 `RowDeleted` 이벤트 처리기입니다.

> [!NOTE]
> 검색 하는 대신 합니다 `BrochurePath` 에 대 한 세부 정보를 `Categories` 에서 삭제할 레코드를 `RowDeleting` 이벤트 처리기 수 또는 추가 했습니다를 `BrochurePath` GridView s에 `DataKeyNames` 속성 레코드의 값을 액세스 및 통해 여 `e.Keys` 컬렉션입니다. 이렇게 약간 GridView가의 보기 상태 크기를 늘리거나 있지만 필요한 코드의 양을 줄일를 여정 데이터베이스에 저장 합니다.


S 기본 삭제 명령을 호출 되었고 ObjectDataSource GridView s 후 `RowDeleted` 이벤트 처리기에 발생 합니다. 데이터를 삭제 하는 중에 예외가 없습니다 및에 대 한 값이 있는 경우 `deletedCategorysPdfPath`, PDF 파일 시스템에서 삭제 됩니다. 참고 해당 그림 연관 된 범주 s 이진 데이터를 정리 하려면이 추가 코드가 필요 하지 않습니다. S 그림 데이터에 직접 데이터베이스에에서 저장 되므로 지금 삭제는 `Categories` 행에는 해당 범주의 그림 데이터도 삭제 합니다.

두 개의 이벤트 처리기를 추가한 후이 테스트 사례를 다시 실행 합니다. 범주를 삭제 하는 경우 해당 연결된 PDF도 삭제 됩니다.

기존 레코드가 연결 된 이진 데이터를 업데이트 하는 중 몇 가지 흥미로운 과제를 제공 합니다. 이 자습서의 나머지 부분 자세하게 살펴봅니다 브로슈어 및 사진 업데이트 기능을 추가 합니다. 6 단계에서는 그림을 업데이트 하는 중에 7 단계를 검색 하는 동안 브로슈어 정보를 업데이트 하는 기술을 살펴봅니다.

## <a name="step-6-updating-a-category-s-brochure"></a>6 단계: 업데이트 범주의 브로슈어

에 설명 된 대로 합니다 [An 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서에서는 GridView는 해당 기본 데이터 원본이 있으면 확인란의 틱 하 여 구현할 수 있는 기본 제공 행 수준 편집 지원을 제공 적절 하 게 구성 합니다. 현재는 `CategoriesDataSource` ObjectDataSource let s에 추가 되므로 지원, 업데이트를 포함 하도록 아직 구성 되지 않았습니다.

ObjectDataSource가의 마법사에서 데이터 소스 구성 링크를 클릭 하 고 두 번째 단계를 진행 합니다. 때문에 `DataObjectMethodAttribute` 에 사용 되는 `CategoriesBLL`, 업데이트 드롭 다운 목록을 자동으로 채워져야 합니다 `UpdateCategory` 4 개의 입력 매개 변수를 받아들이는 오버 로드 (모든 열에 대 한 하지만 `Picture`). 5 개의 매개 변수를 사용 하 여 오버 로드를 사용할 수 있도록이 변경 합니다.


[![그림에 대 한 매개 변수를 포함 하는 UpdateCategory 메서드를 사용 하는 ObjectDataSource 구성](updating-and-deleting-existing-binary-data-cs/_static/image9.gif)](updating-and-deleting-existing-binary-data-cs/_static/image15.png)

**그림 9**: ObjectDataSource를 사용 하 여 구성 합니다 `UpdateCategory` 에 대 한 매개 변수를 포함 하는 메서드 `Picture` ([클릭 하 여 큰 이미지 보기](updating-and-deleting-existing-binary-data-cs/_static/image16.png))


ObjectDataSource에 대 한 값에는 이제 해당 `UpdateMethod` 해당 뿐만 아니라 속성 `UpdateParameter` s입니다. Visual Studio 설정 ObjectDataSource가의 4 단계에서에서 설명 했 듯이 `OldValuesParameterFormatString` 속성을 `original_{0}` 데이터 소스 구성 마법사를 사용 하는 경우. 이 업데이트를 사용 하 여 문제를 일으킬를 메서드 호출을 삭제 합니다. 따라서이 속성을 완전히 지울 또는 기본값으로 재설정 `{0}`합니다.

마법사 완료 후 수정 된 `OldValuesParameterFormatString`, ObjectDataSource가 선언적 태그는 다음과 같아야 합니다.:


[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample6.aspx)]

GridView가 기본 제공 편집 기능을 켜려면 GridView가 스마트 태그에서 편집 사용 옵션을 선택 합니다. CommandField s를 설정 합니다 `ShowEditButton` 속성을 `true`, 결과 편집 단추 (및 편집 되는 행에 대 한 업데이트 및 Cancel 단추) 추가 합니다.


[![GridView 지원 편집 구성](updating-and-deleting-existing-binary-data-cs/_static/image10.gif)](updating-and-deleting-existing-binary-data-cs/_static/image17.png)

**그림 10**: 지원 편집 GridView 구성 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image18.png))


브라우저를 통해 페이지를 방문 하 고 행의 편집 단추 중 하나를 클릭 합니다. 합니다 `CategoryName` 고 `Description` BoundFields 입력란으로 렌더링 됩니다. `BrochurePath` TemplateField에는 `EditItemTemplate`계속 표시 되므로 해당 `ItemTemplate` 브로슈어에 대 한 링크입니다. 합니다 `Picture` 갖는 텍스트 상자로 이미지 필드 렌더링 `Text` 속성의 이미지 필드의 값이 할당 됩니다 `DataImageUrlField` 값을 예제의 `CategoryID`합니다.


[![GridView는 BrochurePath에 대 한 편집 인터페이스를 없습니다.](updating-and-deleting-existing-binary-data-cs/_static/image11.gif)](updating-and-deleting-existing-binary-data-cs/_static/image19.png)

**그림 11**: GridView 편집 인터페이스에 대 한 부족 `BrochurePath` ([클릭 하 여 큰 이미지 보기](updating-and-deleting-existing-binary-data-cs/_static/image20.png))


## <a name="customizing-thebrochurepaths-editing-interface"></a>사용자 지정을`BrochurePath`s 편집 인터페이스

편집 인터페이스를 만들어야 합니다 `BrochurePath` TemplateField로 사용자를 허용 하는:

- 으로 범주의 브로슈어 둡니다-인
- 새 브로슈어, 업로드 하 여 범주의 브로슈어 업데이트 또는
- 범주의 브로슈어 (범주에는 연결된 브로슈어를 더 이상 대/소문자)에서 완전히 제거 합니다.

또한 업데이트 해야 합니다 `Picture` 이미지 필드 s 편집 인터페이스 했지만 다룰 예정이 7 단계.

GridView가 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 선택 합니다 `BrochurePath` TemplateField의 `EditItemTemplate` 드롭 다운 목록에서. RadioButtonList 웹 컨트롤을 설정 하는이 템플릿의 경우 추가 해당 `ID` 속성을 `BrochureOptions` 및 해당 `AutoPostBack` 속성을 `true`입니다. 속성 창에서 줄임표를 클릭 합니다 `Items` 속성을 가져오는 `ListItem` 컬렉션 편집기입니다. 다음 세 가지 옵션을 함께 추가 `Value`의 1, 2 및 3, 각각.

- 사용 하 여 현재 브로슈어
- 현재 브로슈어 제거
- 새 브로슈어 업로드

첫 번째 설정 `ListItem` s `Selected` 속성을 `true`입니다.


![세 가지 ListItems RadioButtonList에 추가](updating-and-deleting-existing-binary-data-cs/_static/image12.gif)

**그림 12**: 3 개 추가 `ListItem` RadioButtonList s


RadioButtonList, 아래 라는 FileUpload 컨트롤을 추가 `BrochureUpload`합니다. 설정 해당 `Visible` 속성을 `false`입니다.


[![에 EditItemTemplate RadioButtonList 및 FileUpload 컨트롤 추가](updating-and-deleting-existing-binary-data-cs/_static/image13.gif)](updating-and-deleting-existing-binary-data-cs/_static/image21.png)

**그림 13**: RadioButtonList 및 FileUpload 컨트롤을 추가 합니다 `EditItemTemplate` ([클릭 하 여 큰 이미지 보기](updating-and-deleting-existing-binary-data-cs/_static/image22.png))


이 RadioButtonList 사용자에 대 한 세 가지 옵션을 제공합니다. FileUpload 컨트롤 업로드 새 브로슈어, 마지막 옵션을 선택한 경우에 표시 되도록 합니다. 이를 위해 RadioButtonList s에 대 한 이벤트 처리기를 만들고 `SelectedIndexChanged` 이벤트 다음 코드를 추가 합니다.


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample7.cs)]

RadioButtonList 및 FileUpload 컨트롤 템플릿에서 되므로 약간의 프로그래밍 방식으로 이러한 컨트롤을 액세스 하는 코드를 작성 해야 합니다. 합니다 `SelectedIndexChanged` 이벤트 처리기가 radiobuttonlist에 대 한 참조를 전달 합니다 `sender` 입력된 매개 변수입니다. FileUpload 컨트롤을 가져오려면 가져오고 RadioButtonList의 부모 컨트롤 사용 해야는 `FindControl("controlID")` 거기서에서 메서드. FileUpload 컨트롤 s RadioButtonList 및 FileUpload 컨트롤에 대 한 참조 한 후 `Visible` 속성이 `true` 경우에만 RadioButtonList s `SelectedValue` 는 3, equals는 `Value` 업로드 새 브로슈어 `ListItem`.

이 코드를 사용 하 여 시간을 내어 편집 인터페이스를 테스트 합니다. 행에 대 한 편집 단추를 클릭 합니다. 처음에 사용 하 여 현재 브로슈어 옵션을 선택 해야 합니다. 포스트백을 발생 시키는 선택한 인덱스를 변경 합니다. 세 번째 옵션을 선택 하는 경우 FileUpload 컨트롤을 표시, 숨겨져 그렇지 않은 경우. 그림 14 편집 단추를 클릭할 먼저; 때 편집 인터페이스를 보여 줍니다. 그림 15 업로드 새 브로슈어 옵션을 선택한 후 인터페이스를 보여 줍니다.


[![사용 하 여 현재 브로슈어 처음에 선택](updating-and-deleting-existing-binary-data-cs/_static/image14.gif)](updating-and-deleting-existing-binary-data-cs/_static/image23.png)

**그림 14**: 사용 하 여 현재 브로슈어 처음에 옵션을 선택 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image24.png))


[![FileUpload 컨트롤 업로드 새 브로슈어 옵션 표시를 선택합니다.](updating-and-deleting-existing-binary-data-cs/_static/image15.gif)](updating-and-deleting-existing-binary-data-cs/_static/image25.png)

**그림 15**: 업로드 새 브로슈어 옵션 표시 FileUpload 컨트롤을 선택 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image26.png))


## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>브로셔 저장 파일과 업데이트 된`BrochurePath`열

GridView의 업데이트 단추를 클릭 하면 해당 `RowUpdating` 이벤트가 발생 합니다. S 업데이트 명령을 호출 하는 ObjectDataSource와 다음 GridView의 `RowUpdated` 이벤트가 발생 합니다. 삭제 워크플로 사용 하 여 이러한 이벤트에 대 한 이벤트 처리기를 작성 해야 예: 합니다. 에 `RowUpdating` 기반으로 수행할 동작을 결정 해야 이벤트 처리기는 `SelectedValue` 의 `BrochureOptions` RadioButtonList:

- 경우는 `SelectedValue` 가 1 이면 동일한 계속 사용 하려는 `BrochurePath` 설정 합니다. ObjectDataSource가 설정 해야 하므로 `brochurePath` 매개 변수를 기존 `BrochurePath` 업데이트 되는 레코드의 값입니다. ObjectDataSource s `brochurePath` 를 사용 하 여 매개 변수를 설정할 수 있습니다 `e.NewValues["brochurePath"] = value`합니다.
- 경우는 `SelectedValue` 가 2 인 다음 s 레코드를 설정 하려고 `BrochurePath` 값을 `NULL`입니다. ObjectDataSource가 설정 하 여이 수행할 수 있습니다 `brochurePath` 매개 변수를 `Nothing`, 그러면 데이터베이스 `NULL` 에서 사용 되는 `UPDATE` 문. 제거 되는 기존 브로슈어 파일의 경우 기존 파일을 삭제 해야 합니다. 그러나 하고자 예외가 발생 하지 않고 업데이트를 완료 하는 경우이 작업을 수행 합니다.
- 경우는 `SelectedValue` 사용자는 PDF 파일 업로드에 확인 하 고 다음 파일 시스템에 저장 하 고 s 레코드를 업데이트 한 다음이 3 이면 `BrochurePath` 열 값입니다. 또한 기존 브로슈어 파일 대체 되는 경우 이전 파일을 삭제 해야 합니다. 그러나 하고자 예외가 발생 하지 않고 업데이트를 완료 하는 경우이 작업을 수행 합니다.

경우 완료 하는 데 필요한 단계 RadioButtonList s `SelectedValue` 는 3 DetailsView s에서 사용 되는 거의 동일 `ItemInserting` 이벤트 처리기입니다. 이 이벤트 처리기에 추가한 DetailsView 컨트롤에서 새 범주 레코드를 추가할 때 실행 되는 [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-cs.md)합니다. 따라서 아웃이 기능을 별도 메서드로 리팩터링 할 behooves 합니다. 구체적으로 옮긴 공통 기능을 확인 두 가지 방법으로:

- `ProcessBrochureUpload(FileUpload, out bool)` FileUpload 컨트롤 인스턴스 및 일부 유효성 검사 오류로 인해 취소 되도록 하는 경우 또는 삭제 또는 편집 작업을 계속할지 여부를 지정 하는 출력 부울 값을 입력으로 받아들입니다. 이 메서드는 저장된 된 파일에 경로 반환 하거나 `null` 없는 파일을 저장 하는 경우.
- `DeleteRememberedBrochurePath` 페이지 변수의 경로 지정 된 파일을 삭제 `deletedCategorysPdfPath` 하는 경우 `deletedCategorysPdfPath` 아닙니다 `null`합니다.

이러한 두 가지 방법에 대 한 코드는 다음과 같습니다. 간의 유사성 `ProcessBrochureUpload` 및 DetailsView의 `ItemInserting` 이전 자습서에서 이벤트 처리기입니다. 이 자습서에서는 이러한 새 메서드를 사용 하려면 DetailsView의 이벤트 처리기를 업데이트 합니다. 이 자습서를 참조 하는 수정 사항을 DetailsView의 이벤트 처리기에 연관 된 코드를 다운로드 합니다.


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample8.cs)]

GridView s `RowUpdating` 하 고 `RowUpdated` 이벤트 처리기를 사용 합니다 `ProcessBrochureUpload` 및 `DeleteRememberedBrochurePath` 메서드를 다음 코드와 같이:


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample9.cs)]

참고 하는 방법을 `RowUpdating` 이벤트 처리기에서 기반으로 적절 한 작업을 수행 하는 일련의 조건문을 사용 합니다 `BrochureOptions` RadioButtonList의 `SelectedValue` 속성 값입니다.

이 코드를 사용 하 여 범주를 편집할 수 있으며 해당 현재 브로슈어 따르거나 없습니다 브로슈어를 사용 하 여 새로 업로드 하 게 키를 누릅니다. 계속 해 서 사용해 보세요. 에 중단점을 설정 합니다 `RowUpdating` 및 `RowUpdated` 워크플로의 어느 정도 인지 확인할 이벤트 처리기입니다.

## <a name="step-7-uploading-a-new-picture"></a>7 단계: 새 사진 업로드

합니다 `Picture` 의 값으로 채워진 텍스트 상자로 인터페이스 렌더링을 편집 하는 이미지 필드 s 해당 `DataImageUrlField` 속성입니다. 편집 워크플로 중 GridView 매개 변수를 전달 매개 변수 s 이름의 ObjectDataSource에는 이미지 필드의 값 `DataImageUrlField` 속성 및 매개 변수 s 값 편집 인터페이스에 텍스트 상자에 입력 합니다. 이 동작은 이미지를 파일 시스템에 파일로 저장 하는 경우에 적합 하며 `DataImageUrlField` 이미지의 전체 URL을 포함 합니다. 이러한 상황을 사용 하 여 편집 인터페이스 사용자 변경할 수 있으며 데이터베이스에 다시 저장 하는 텍스트 상자에 이미지의 URL을 표시 합니다. 사실이 기본 인터페이스의 대상이 t 새 이미지를 업로드 하는 데 사용할 수 있지만 다른 현재 값에서 이미지의 URL을 변경 하 수 것입니다. 그러나이 자습서에서는 편집 인터페이스는 이미지 필드 기본값 충분 하지 않은 때문에 합니다 `Picture` 데이터베이스에 직접 저장 되는 이진 데이터 및 `DataImageUrlField` 속성 저장만 `CategoryID`합니다.

하는 경우이 자습서에는 이미지 필드를 사용 하 여 행을 편집 하는 사용자를 더 잘 이해 하려면 다음 예제를 살펴보세요: 사용자가 포함 된 행을 편집 `CategoryID` 일으키는 10는 `Picture` 값 10 사용 하 여 텍스트 상자로 렌더링 하는 이미지 필드입니다. 사용자를 50이 텍스트이 상자에 값을 변경 하 고 [업데이트] 단추를 클릭할 한다고 가정 합니다. 포스트백이 발생할 및 GridView 라는 매개 변수를 처음으로 만든 `CategoryID` 값이 50입니다. 그러나 GridView에서이 매개 변수를 보내기 전에 (및 `CategoryName` 하 고 `Description` 매개 변수), 값에 추가 됩니다.는 `DataKeys` 컬렉션. 따라서 덮어씁니다 합니다 `CategoryID` 매개 변수를 현재 행 s 기본 `CategoryID` 값을 10입니다. 즉, 인터페이스를 편집 하는 이미지 필드 s 영향을 주지 않습니다 편집 워크플로에이 자습서에 대 한 때문에 이미지 필드의 이름을 `DataImageUrlField` 속성과 표의 `DataKey` 값은 동일한 것입니다.

이미지 필드를 사용 하면 쉽게 데이터베이스 데이터를 기반으로 이미지를 표시 하려면, t 편집 인터페이스에는 입력란을 제공 하려는 하지 것입니다. 대신, 최종 사용자 범주의 그림을 변경 하는 데 사용할 수 있는 FileUpload 컨트롤을 제공 하려고 합니다. 달리는 `BrochurePath` 값을이 자습서에서는 각 범주는 그림에 있어야 할 ve 결정 합니다. 현재 그림을 남기 세요 없는 연결된 그림 사용자.vhd 새 그림을 수 없다는 메시지가 사용자에 게 t 필요 했습니다 하지 따라서-됩니다.

이미지 필드 s 편집 인터페이스를 사용자 지정 하려면를 TemplateField로 변환 해야 합니다. GridView가 스마트 태그에서 열 편집 링크를 클릭 하 고 이미지 필드를 선택한 TemplateField 링크로 Convert이이 필드를 클릭 합니다.


![이미지 필드를 TemplateField로 변환](updating-and-deleting-existing-binary-data-cs/_static/image16.gif)

**그림 16**:는 이미지 필드를 TemplateField로 변환


이 방식으로 templatefield로 변환 하는 이미지 필드를 TemplateField 템플릿 두 개가 생성 됩니다. 선언적 구문을 볼 수 있듯이, 합니다 `ItemTemplate` 포함 하는 이미지 웹 컨트롤 `ImageUrl` 이미지 필드에 기반 하는 데이터 바인딩 구문을 사용 하 여 속성에 할당 됩니다 `DataImageUrlField` 및 `DataImageUrlFormatString` 속성. `EditItemTemplate` TextBox를 포함입니다 `Text` 속성에 지정 된 값에 바인딩되는 `DataImageUrlField` 속성.


[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample10.aspx)]

업데이트 해야 합니다 `EditItemTemplate` FileUpload 컨트롤을 사용 합니다. S 스마트 태그 템플릿 편집 클릭 GridView에서 연결 하 고 다음을 선택 합니다 `Picture` TemplateField의 `EditItemTemplate` 드롭 다운 목록에서. 템플릿에서이 제거 하는 텍스트 상자를 표시 됩니다. 다음으로 설정 템플릿에 도구 상자에서 FileUpload 컨트롤을 끌어 해당 `ID` 에 `PictureUpload`입니다. 또한 범주의 그림을 변경 하려면 새 사진을 지정 텍스트를 추가 합니다. 동일한 범주의 그림 유지, 필드를 비워 둡니다도 템플릿에 합니다.


[![EditItemTemplate FileUpload 컨트롤을 추가](updating-and-deleting-existing-binary-data-cs/_static/image17.gif)](updating-and-deleting-existing-binary-data-cs/_static/image27.png)

**그림 17**: FileUpload 컨트롤을 추가 합니다 `EditItemTemplate` ([클릭 하 여 큰 이미지 보기](updating-and-deleting-existing-binary-data-cs/_static/image28.png))


편집 인터페이스를 사용자 지정한 후 진행 상황을 브라우저에서 봅니다. 읽기 전용 모드에서 행을 볼 때 범주의 이미지는 이전에 있었지만 편집 단추를 클릭 하면 그림 열 FileUpload 컨트롤 텍스트 렌더링 되었다고 표시 됩니다.


[![FileUpload 컨트롤을 포함 하는 편집 인터페이스](updating-and-deleting-existing-binary-data-cs/_static/image18.gif)](updating-and-deleting-existing-binary-data-cs/_static/image29.png)

**그림 18**: FileUpload 컨트롤을 포함 하는 편집 인터페이스 ([큰 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-cs/_static/image30.png))


ObjectDataSource를 호출 하도록 구성 되어 있는지를 회수 합니다 `CategoriesBLL` s 클래스 `UpdateCategory` 그림에 대 한 이진 데이터를 입력으로 허용 되는 방법을 `byte` 배열. 하지만이 배열에 있는 경우는 `null` 대체, 값 `UpdateCategory` 오버 로드 호출 되는 문제를 `UPDATE` 수정 하지 않는 SQL 문을 `Picture` 있으므로 s 범주를 현재 종료 열 그림은 그대로 유지 됩니다. GridView에서 따라서 `RowUpdating` 프로그래밍 방식으로 참조 해야 하는 이벤트 처리기는 `PictureUpload` FileUpload 제어 하 고 파일 업로드 된 경우를 결정 합니다. 업로드 되지 않았습니다 경우 저희 *되지* 값을 지정 하려면를 `picture` 매개 변수입니다. 반면, 파일에서 업로드 된 경우는 `PictureUpload` FileUpload 컨트롤 JPG 파일 인지 확인 하려고 합니다. 인 경우 해당 이진 내용을 통해 ObjectDataSource을 받을 `picture` 매개 변수입니다.

6 단계에서에서 사용 되는 코드를 사용 하 여 이미 여기에 필요한 코드의 대부분 있는 DetailsView s와 같은 `ItemInserting` 이벤트 처리기입니다. 따라서 필자 ve는 일반적인 기능을 새 메서드로 리팩터링 `ValidPictureUpload`, 업데이트 및는 `ItemInserting` 이 방법을 사용 하려면 이벤트 처리기입니다.

다음 코드를 추가 합니다 GridView의 시작과 `RowUpdating` 이벤트 처리기입니다. 이 s 인할 것 이므로 브로슈어 파일을 저장 하는 코드 앞에 야이 코드는 중요 한 그림이 잘못 되었습니다. 파일을 업로드 하는 경우 브로슈어 웹의 서버 파일 시스템에 저장 하려면.


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample11.cs)]

`ValidPictureUpload(FileUpload)` 메서드 유일한 입력된 매개 변수로 FileUpload 컨트롤에서는 업로드 된 파일의 확장명 JPG 업로드 된 파일 인지 확인을 확인 하 고 그림 파일을 업로드 하는 경우만 호출 됩니다. 경우 없는 파일을 업로드 하 고 그림 매개 변수를 설정 하지는 하므로 기본값을 사용 하 여 `null`입니다. 사진 업로드 된 경우 및 `ValidPictureUpload` 반환 `true`의 `picture` 매개 변수가 메서드에서 반환 되 면 업로드 된 이미지의 이진 데이터를 할당 된 `false`, 업데이트 워크플로 취소 되 고 이벤트 처리기가 종료 되었습니다.

합니다 `ValidPictureUpload(FileUpload)` DetailsView s에서 리팩터링 메서드 코드에서 `ItemInserting` 이벤트 처리기를 따릅니다.


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample12.cs)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>8 단계: JPGs 바꿉니다 원래 범주 그림을

원래 8 범주 그림 비트맵 파일은 OLE 머리글에 래핑되는 것을 기억 하십시오. 기존 레코드의 그림을 편집 하는 기능을 추가 했지만, 이제는 시간을 내어 JPGs 이러한 비트맵으로 바꿉니다. 현재 범주 그림을 사용 하 여 계속 하려는 경우 다음 단계를 수행 하 여 JPGs 변환할 수 있습니다.

1. 하드 드라이브에 비트맵 이미지를 저장 합니다. 방문을 `UpdatingAndDeleting.aspx` 브라우저에서 페이지를 처음 8 개 범주를 각각에 대 한 이미지를 마우스 오른쪽 단추로 클릭 하 고 그림을 저장 하도록 선택 합니다.
2. 원하는 이미지 편집기의 이미지를 엽니다. 예를 들어 Microsoft 그림판을 사용할 수 있습니다.
3. JPG 이미지 비트맵을 저장 합니다.
4. JPG 파일을 사용 하 여 편집 인터페이스를 통해 범주의 그림을 업데이트 합니다.

범주를 편집 하 고 JPG 이미지를 업로드 한 후 이미지에서에서 렌더링 되지 것입니다 브라우저 때문에 `DisplayCategoryPicture.aspx` 페이지는 처음 8 개 범주의 그림에서 첫 번째 78 바이트를 제거 합니다. OLE 머리글 제거를 수행 하는 코드를 제거 하 여이 문제를 해결 합니다. 이 작업을 수행한 후를 `DisplayCategoryPicture.aspx``Page_Load` 이벤트 처리기를 다음 코드로 있어야 합니다.


[!code-vb[Main](updating-and-deleting-existing-binary-data-cs/samples/sample13.vb)]

> [!NOTE]
> `UpdatingAndDeleting.aspx` 삽입 및 인터페이스를 편집 페이지 s 좀 더 많은 작업을 사용할 수 있습니다. 합니다 `CategoryName` 및 `Description` GridView 및 DetailsView BoundFields TemplateFields로 변환 되어야 합니다. 이후 `CategoryName` 허용 하지 않습니다 `NULL` 값을 RequiredFieldValidator 추가 해야 합니다. 및 `Description` 텍스트 상자를 여러 줄 텍스트 상자에 변환할 수 있습니다. I 이러한 마무리를 연습으로 둡니다.


## <a name="summary"></a>요약

이 자습서는 살펴보겠습니다 이진 데이터로 작업을 완료 합니다. 이 자습서에 이전 세 가지 방법을 이진 데이터 살펴보았습니다 데이터베이스 내에서 직접 또는 파일 시스템에 저장할 수 있습니다. 사용자가 하드 드라이브에서 파일을 선택 하 고 웹 서버에 있는 파일 시스템에 저장 하거나 이동할 수 있습니다 데이터베이스 삽입에 업로드 하 여 시스템에 이진 데이터를 제공 합니다. ASP.NET 2.0에는 이러한 인터페이스를 제공 끌어서 놓기 에서처럼 쉽지 FileUpload 컨트롤을 포함 합니다. 그러나 설명한 것 처럼 합니다 [파일 업로드](uploading-files-cs.md) 자습서에서는 FileUpload 컨트롤은만 상대적으로 적은 파일 업로드, 메가바이트를 초과 하지 않는 것이 좋습니다에 적합 합니다. 것도 편집 하 고 기존 레코드에서 이진 데이터를 삭제 하는 방법 뿐만 아니라 기본 데이터 모델을 사용 하 여 업로드 된 데이터를 연결 하는 방법을 살펴봅니다.

자습서의 다음 집합에서는 다양 한 캐싱 기술을 살펴봅니다. 캐시는 응용 프로그램 s를 개선 하기 위한 수단을 제공 비용이 많이 드는 작업의 결과 보다 신속 하 게 액세스할 수 있는 위치에 저장 하 여 전체적인 성능.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Teresa Murphy 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](including-a-file-upload-option-when-adding-a-new-record-cs.md)
> [다음](uploading-files-vb.md)
