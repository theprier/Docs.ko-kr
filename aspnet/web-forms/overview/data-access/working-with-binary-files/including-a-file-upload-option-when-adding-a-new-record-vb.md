---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-vb
title: 파일을 포함 하 여 업로드 옵션 (VB) 새 레코드를 추가 하는 경우 | Microsoft Docs
author: rick-anderson
description: 이 자습서에는 텍스트 데이터를 모두 입력 한 이진 파일을 업로드할 수 있는 웹 인터페이스를 만드는 방법을 보여 줍니다. T 사용 가능한 옵션을 설명 하기 위해 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: 5776281d-4637-4d1e-a65b-2621d2cade44
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-vb
msc.type: authoredcontent
ms.openlocfilehash: 30cfdcf8e9b65f92b267509b4289d828b2532e65
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363147"
---
<a name="including-a-file-upload-option-when-adding-a-new-record-vb"></a>새 레코드 (VB)를 추가할 때 파일 업로드 옵션 포함
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_VB.exe) 또는 [PDF 다운로드](including-a-file-upload-option-when-adding-a-new-record-vb/_static/datatutorial56vb1.pdf)

> 이 자습서에는 텍스트 데이터를 모두 입력 한 이진 파일을 업로드할 수 있는 웹 인터페이스를 만드는 방법을 보여 줍니다. 다른 파일 시스템에 저장 됩니다 하는 동안 하나의 파일 이진 데이터를 저장 하는 옵션을 설명 하기 위해 데이터베이스에 저장 됩니다.


## <a name="introduction"></a>소개

클라이언트에서 웹 서버로 파일을 보내고 데이터 W에에서이 이진 데이터를 표시 하는 방법을 살펴봤습니다 FileUpload 컨트롤을 사용 하는 방법을 살펴보고 응용 프로그램의 데이터 모델을 사용 하 여 연결 된 이진 데이터를 저장 하는 기술을 살펴보았습니다 이전 두 자습서 eb 컨트롤입니다. 에서는 데이터 모델을 사용 하 여 업로드 된 데이터를 통해 연결 하는 방법에 설명 하는 준비 합니다.

이 자습서에서는 새 범주를 추가 하려면 웹 페이지를 만들겠습니다. 범주의 이름 및 설명 텍스트 상자 외에도이 페이지는 두 FileUpload 컨트롤 새 범주의 그림에 대 한 개와 브로슈어 포함 해야 합니다. 업로드 된 그림은 새 레코드 s에 직접 저장 됩니다 `Picture` 열, 브로슈어를 저장 하는 반면 합니다 `~/Brochures` 가 새 레코드에 저장 된 파일의 경로를 사용 하 여 폴더 `BrochurePath` 열.

이 새 웹 페이지를 만들기 전에 아키텍처를 업데이트 해야 합니다. 합니다 `CategoriesTableAdapter` 가 기본 쿼리를 검색 하지 않습니다는 `Picture` 열입니다. 결과적으로 자동 생성 `Insert` 에 대 한 입력만 메서드가 합니다 `CategoryName`, `Description`, 및 `BrochurePath` 필드입니다. 따라서 모든 4에서 요구 하는 TableAdapter에서 추가 메서드를 생성 해야 `Categories` 필드입니다. `CategoriesBLL` 클래스는 비즈니스 논리 계층에서 업데이트 해야 합니다.

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>1 단계: 추가`InsertWithPicture`메서드는`CategoriesTableAdapter`

만들 때를 `CategoriesTableAdapter` 년대 합니다 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에서는 구성 하 여 자동으로 생성 `INSERT`, `UPDATE`, 및 `DELETE` 문 쿼리를 기반으로 기본입니다. 또한 메서드를 생성 하는 DB 직접적인 접근 방식을 사용 하 여 TableAdapter를 지시 했습니다 `Insert`, `Update`, 및 `Delete`합니다. 이러한 메서드는 자동으로 생성 된 실행 `INSERT`, `UPDATE`, 및 `DELETE` 문 및 결과적으로 기본 쿼리에서 반환 된 열을 기반으로 하는 입력된 매개 변수를 허용 합니다. 에 [파일 업로드](uploading-files-vb.md) 제시 된 자습서는 `CategoriesTableAdapter` s 주 쿼리를 사용 하는 `BrochurePath` 열입니다.

이후를 `CategoriesTableAdapter` s 기본 쿼리에서 참조 하지 않습니다는 `Picture` 열을 새 레코드를 추가할 수 없으며 값을 사용 하 여 기존 레코드를 업데이트 했습니다는 `Picture` 열. 이 정보를 캡처하려면, 만들 수 있습니다 하거나 새 방법을 이진 데이터를 사용 하 여 레코드를 삽입 하는 데 특별히 사용 되는 TableAdapter의 또는 자동으로 생성 된 사용자 지정할 수 `INSERT` 문입니다. 자동 생성 사용자 지정 문제 `INSERT` 문이 우리가 위험이 마법사로 덮어쓸 우리의 사용자 지정 되었습니다. 예를 들어, 사용자 지정 했습니다 imagine 합니다 `INSERT` 사용을 포함 하도록 문을 `Picture` 열입니다. 이 tableadapter 업데이트 `Insert` 범주의 그림 s 이진 데이터에 대 한 추가 입력된 매개 변수를 포함 하는 방법입니다. 이 DAL 메서드를 사용 하 여 프레젠테이션 계층을 통해이 BLL 메서드를 호출 하는 비즈니스 논리 계층에 다음 메서드를 만들 수 및 모든 쌓아가는 작동 합니다. 즉, 다음 시간까지 TableAdapter 구성 마법사를 통해 TableAdapter를 구성 했습니다. 마법사는 사용자 지정을 완료 하는 즉시 합니다 `INSERT` 문을 덮어씁니다는 `Insert` 메서드는 이전 상태로 되돌리고 코드는 더 이상 컴파일되지!

> [!NOTE]
> 이 불편 하는 대신 임시 SQL 문이 저장된 프로시저를 사용 하는 경우 비-문제를입니다. 이후 자습서에서는 대신 임시 SQL 문이 저장된 프로시저를 사용 하 여 데이터 액세스 계층에 살펴봅니다.


이 가능성을 방지 하려면 자동 생성 된 SQL 문 사용자 지정 하는 것이 아니라 골치 아프게, TableAdapter에 대 한 새 메서드를 대신 만든을 있습니다. 라는이 메서드를 `InsertWithPicture`에 대 한 값을 수락할를 `CategoryName`, `Description`, `BrochurePath`, 및 `Picture` 열 및 실행는 `INSERT` 새 레코드에 4 개의 값을 저장 하는 문.

입력 데이터 집합을 열고, 디자이너에서 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 상황에 맞는 메뉴에서 추가 쿼리를 선택 합니다. TableAdapter 쿼리가 데이터베이스에 액세스 해야 하는 방법을 궁금해 하 여 시작 하는 TableAdapter 쿼리 구성 마법사가 시작 됩니다. SQL 문 사용을 선택 하 고 클릭 합니다. 다음 단계를 생성할 쿼리 형식에 대 한 라는 메시지가 나타납니다. 새 레코드를 추가 하는 쿼리를 만드는 다시 이후로 `Categories` 테이블 삽입을 선택 하 고 다음을 클릭 합니다.


[![삽입 옵션을 선택 합니다.](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image1.png)

**그림 1**: 삽입 옵션을 선택 ([큰 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image2.png))


이제 지정 해야 합니다 `INSERT` SQL 문입니다. 마법사가 자동으로 제안는 `INSERT` TableAdapter s 주 쿼리에 해당 하는 문입니다. 이 경우 해당 s는 `INSERT` 삽입 하는 문을 `CategoryName`, `Description`, 및 `BrochurePath` 값입니다. 문을 업데이트 되도록 합니다 `Picture` 열이 함께 포함 됩니다는 `@Picture` 매개 변수를 같이:


[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample1.sql)]

마법사의 마지막 화면 새 TableAdapter 메서드 이름을 묻는 메시지가 나타납니다. 입력 `InsertWithPicture` 하 고 마침을 클릭 합니다.


[![새 TableAdapter 메서드 InsertWithPicture 이름](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image3.png)

**그림 2**: 새 TableAdapter 메서드 이름을 `InsertWithPicture` ([클릭 하 여 큰 이미지 보기](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image4.png))


## <a name="step-2-updating-the-business-logic-layer"></a>2 단계: 비즈니스 논리 계층 업데이트

방금 만든 DAL 메서드를 호출 하는 BLL 메서드를 생성 해야 데이터 액세스 계층으로 직접 이동를 무시 하는 것이 아니라 프레젠테이션 계층 비즈니스 논리 레이어를 사용 하 여 인터페이스만 해야 하므로 (`InsertWithPicture`). 이 자습서에서 메서드를 만듭니다는 `CategoriesBLL` 라는 클래스 `InsertWithPicture` 입력된으로 3을 받아들이는 `String` s 및 `Byte` 배열입니다. `String` s 범주 이름, 설명 및 브로슈어 파일 경로 대 한 입력된 매개 변수는 하는 동안는 `Byte` 배열의 범주 그림의 이진 내용입니다. 다음 코드에서 알 수 있듯이,이 BLL 메서드는 해당 DAL 메서드를 호출 합니다.


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample2.vb)]

> [!NOTE]
> 추가 하기 전에 입력 데이터 집합을 저장 했는지를 `InsertWithPicture` BLL 방법입니다. 이후를 `CategoriesTableAdapter` 클래스 코드는 자동으로 생성 된 입력 데이터 집합에 기반한 don t 변경 내용을 입력 데이터 집합에 먼저 저장 하는 경우는 `Adapter` t 성공한 속성에 알고는 `InsertWithPicture` 메서드.


## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>3 단계: 기존 범주 및 해당 이진 데이터를 나열합니다.

이 자습서에서는 만들겠습니다 최종 사용자가 시스템에 새 범주를 추가할 수 있는 페이지를 새 범주에 대 한 그림 및 브로슈어를 제공 합니다. 에 [이전 자습서](displaying-binary-data-in-the-data-web-controls-vb.md) 각 s 범주 이름을 표시 하는 이미지 필드를 TemplateField로 GridView를 사용 했습니다 설명, 그림 및 해당 브로슈어 다운로드에 대 한 링크입니다. S를 페이지 모두 기존의 모든 범주를 나열 하 고 새로 만들 수 있습니다를 만들어이 자습서에서는 해당 기능을 복제할 수 있습니다.

열어서 시작 합니다 `DisplayOrDownload.aspx` 에서 페이지를 `BinaryData` 폴더입니다. 소스 뷰로 이동 하 고 GridView 및 ObjectDataSource가 선언적 구문을 내에서 붙여넣기를 복사 합니다 `<asp:Content>` 요소에 `UploadInDetailsView.aspx`입니다. 또한 잊지 복사할 합니다 `GenerateBrochureLink` 의 코드 숨김 클래스에서 메서드 `DisplayOrDownload.aspx` 에 `UploadInDetailsView.aspx`입니다.


[![복사 및 붙여넣기 UploadInDetailsView.aspx DisplayOrDownload.aspx에서 선언적 구문은](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image5.png)

**그림 3**: 복사 및 붙여넣기는 선언적 구문을 `DisplayOrDownload.aspx` 하 `UploadInDetailsView.aspx` ([클릭 하 여 큰 이미지 보기](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image6.png))


선언적 구문을 복사한 후 및 `GenerateBrochureLink` 를 통해 메서드를 `UploadInDetailsView.aspx` 페이지에서 보기는 모든 항목이 올바르게 복사 되었는지 조치 하도록 브라우저를 통해 페이지입니다. 8 가지 범주를 나열 범주의 그림 뿐만 아니라 브로슈어 다운로드 링크를 포함 하는 GridView 표시 되어야 합니다.


[![이제 해당 이진 데이터와 함께 각 범주 표시](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image7.png)

**그림 4**: 있습니다 해야 이제 참조 각 범주에 따라 해당 이진 데이터 ([큰 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image8.png))


## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>4 단계: 구성 된`CategoriesDataSource`지원 삽입 하려면

합니다 `CategoriesDataSource` ObjectDataSource 사용은 `Categories` GridView 현재 데이터를 삽입 하는 기능이 제공 하지 않습니다. 이 데이터 소스 컨트롤을 통해 삽입을 지원 하기 위해 매핑 해야 해당 `Insert` 메서드는 기본 개체의 메서드를 `CategoriesBLL`입니다. 매핑할 하고자 하는 특히 합니다 `CategoriesBLL` 2 단계에서 다시 추가한 메서드 `InsertWithPicture`합니다.

ObjectDataSource가 스마트 태그에서 데이터 소스 구성 링크를 클릭 하 여 시작 합니다. 첫 번째 화면을 사용 하려면 데이터 소스를 구성 하는 개체를 보여 줍니다. `CategoriesBLL`합니다. 이 설정을 상태로 둡니다-이며을 클릭 하 여 데이터 메서드 정의 화면으로 이동 합니다. 삽입 탭으로 이동 하 고 선택 된 `InsertWithPicture` 드롭 다운 목록에서 메서드. 마법사를 완료 하려면 마침을 클릭 합니다.


[![InsertWithPicture 메서드를 사용 하는 ObjectDataSource 구성](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image9.png)

**그림 5**: ObjectDataSource 사용 하도록 구성 된 `InsertWithPicture` 메서드 ([클릭 하 여 큰 이미지 보기](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image10.png))


> [!NOTE]
> 마법사를 완료 하면 Visual Studio 필드 새로 고침 및 키 하려는 경우에 필드 제어 웹 데이터를 다시 생성 됩니다는 요청할 수 있습니다. 예를 선택 하면 사용자가 변경한 필드 사용자 지정 덮어씁니다. 아니요를 선택 합니다.


ObjectDataSource 마법사를 완료 한 후 값이 포함 이제는 해당 `InsertMethod` 속성 뿐만 `InsertParameters` 4 개의 범주 열에 대 한 다음과 같은 선언적 태그를 보여 줍니다.


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>5 단계: 삽입 인터페이스를 만드는 방법

처음으로 설명 합니다 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md), DetailsView 컨트롤 삽입을 지 원하는 데이터 소스 컨트롤을 사용 하 여 작업할 때 사용할 수 있는 기본 제공 삽입 인터페이스를 제공 합니다. 가이 페이지는 사용자가 새 범주를 신속 하 게 추가할 수 있도록 삽입 인터페이스를 영구적으로 렌더링 하는 GridView 위에 DetailsView 컨트롤을 추가할 수 있습니다. DetailsView에서 새 범주를 추가 하면 시 그 아래에 있는 GridView는 자동으로 새로 고침 및 새 범주를 표시 합니다.

시작 된 DetailsView 설정 GridView 위에 디자이너 도구 상자에서 끌어 해당 `ID` 속성을 `NewCategory` 정리 및 합니다 `Height` 및 `Width` 속성 값입니다. DetailsView가 스마트 태그에서 기존에 바인딩 `CategoriesDataSource` 하 고 다음 확인란 삽입을 사용 하도록 설정 합니다.


[![DetailsView를 CategoriesDataSource 바인딩하고 삽입 사용](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image11.png)

**그림 6**: DetailsView를 바인딩하는 `CategoriesDataSource` 삽입을 사용 하도록 설정 하 고 ([클릭 하 여 큰 이미지 보기](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image12.png))


해당 삽입 인터페이스에 DetailsView를 영구적으로 렌더링 하려면 해당 `DefaultMode` 속성을 `Insert`입니다.

DetailsView에 5 개의 BoundFields `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`, 및 `BrochurePath` 있지만 `CategoryID` 때문에 BoundField 삽입 인터페이스에 렌더링 되지 않습니다 해당 `InsertVisible` 속성이 `False`합니다. 반환 된 열이 있기 때문에 이러한 BoundFields 존재는 `GetCategories()` ObjectDataSource 호출 해당 데이터를 검색 하는 메서드. 그러나 삽입에 대 한에서는 하지 t 사용자가 값을 지정할 수 있도록 하려는 `NumberOfProducts`합니다. 또한 새 범주에 대 한 사진 업로드 수 있을 뿐만 아니라 브로슈어 PDF 업로드 하도록 허용 해야 합니다.

제거를 `NumberOfProducts` BoundField DetailsView 모두와 다음 업데이트를 `HeaderText` 의 속성을 `CategoryName` 및 `BrochurePath` BoundFields 브로슈어, 범주에 각각. 다음으로 변환 합니다 `BrochurePath` BoundField를 TemplateField로이 새 TemplateField 제공 그림에 대 한 새 templatefield로 추가 하 고는 `HeaderText` 그림의 값입니다. 이동 합니다 `Picture` TemplateField 간에 되도록는 `BrochurePath` TemplateField 및 CommandField 합니다.


![DetailsView를 CategoriesDataSource 바인딩하고 삽입 사용](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image7.gif)

**그림 7**: DetailsView를 바인딩하는 `CategoriesDataSource` 삽입을 사용 하도록 설정


변환할 경우는 `BrochurePath` 필드 편집 대화 상자를 통해를 TemplateField로 BoundField를 TemplateField 포함를 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate`합니다. 하지만만 `InsertItemTemplate` 가 필요 되므로 자유롭게 다른 두 가지 서식 파일을 제거 합니다. 이 시점에서 DetailsView s 선언적 구문을 다음과 같이 표시 됩니다.


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>FileUpload 컨트롤 브로슈어 및 그림 필드에 추가

현재는 `BrochurePath` TemplateField s `InsertItemTemplate` 텍스트를 포함 하는 동안는 `Picture` TemplateField에 템플릿이 없습니다. 이러한 두 TemplateField s 업데이트 해야 `InsertItemTemplate` FileUpload 컨트롤을 사용 하도록 합니다.

DetailsView가 스마트 태그에서 템플릿 편집 옵션을 선택한 다음 선택 합니다 `BrochurePath` TemplateField의 `InsertItemTemplate` 드롭 다운 목록에서. 텍스트를 제거 하 고 서식 파일을 도구 상자에서 FileUpload 컨트롤을 끌어 옵니다. FileUpload 컨트롤 s 설정할 `ID` 에 `BrochureUpload`입니다. 마찬가지로, FileUpload 컨트롤을 추가 합니다 `Picture` TemplateField의 `InsertItemTemplate`입니다. 이 FileUpload 컨트롤 s 설정할 `ID` 에 `PictureUpload`입니다.


[![에 먼저 FileUpload 컨트롤 추가](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image13.png)

**그림 8**: FileUpload 컨트롤을 추가 합니다 `InsertItemTemplate` ([클릭 하 여 큰 이미지 보기](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image14.png))


이러한 추가 마치면 두 TemplateField s 선언적 구문이 됩니다.


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample5.aspx)]

사용자가 새 범주를 추가 하는 경우 브로슈어 및 그림의 올바른 파일 형식 인지 확인 하려고 합니다. 브로슈어, 사용자는 PDF를 제공 해야 합니다. 그림에서 사용자는 이미지 파일을 업로드 해야 하지만 허용 했습니다 *모든* 파일 또는 Jpg 또는 Gif와 같은 특정 형식의 이미지 파일에만 이미지? 다른 파일 형식에 대 한 있도록 d 확장 해야 합니다 `Categories` 이 형식을 통해 클라이언트에 보낼 수 있도록 파일 형식을 캡처하는 열을 포함 하도록 스키마 `Response.ContentType` 에서 `DisplayCategoryPicture.aspx`합니다. 인할 것 이므로 이러한 열이는 것만 특정 이미지 파일 형식을 제공 하기 위해 사용자를 제한 하는 것이 좋습니다. `Categories` 테이블 s 기존 이미지는 비트맵 되지만 JPGs 웹을 통해 제공 되는 이미지에 대 한 보다 적절 한 파일 형식입니다.

사용자는 잘못 된 파일 형식에 업로드 하는 경우 삽입을 취소 하 여 문제를 나타내는 메시지를 표시 해야 합니다. DetailsView 아래 레이블 웹 컨트롤을 추가 합니다. 설정 해당 `ID` 속성을 `UploadWarning`아웃의 선택을 취소 해당 `Text` 속성을 설정 합니다 `CssClass` 경고로 속성 및 `Visible` 하 고 `EnableViewState` 속성을 `False`. 합니다 `Warning` CSS 클래스에 정의 된 `Styles.css` 큰, 빨간색, 기울임꼴, 굵게 글꼴의 텍스트를 렌더링 합니다.

> [!NOTE]
> 이상적으로 `CategoryName` 고 `Description` BoundFields TemplateFields 및 삽입 인터페이스 사용자 지정 변환 됩니다. `Description` 여러 줄 텍스트 상자를 통해 가능성이 더 적합는 예를 들어 인터페이스를 삽입 합니다. 및 이후 합니다 `CategoryName` 열을 받아들이지 않습니다 `NULL` 값을 RequiredFieldValidator 새 범주의 이름에 대 한 값을 제공 하는 사용자 확인에 추가 해야 합니다. 다음이 단계를 연습으로 판독기에 남아 있습니다. 다시 가리킵니다 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 확대 데이터 수정 인터페이스에서 자세히 알아봅니다.


## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>6 단계: 웹 서버의 파일 시스템에 업로드 된 브로슈어 저장

사용자는 새 범주에 대 한 값을 입력 하 고 삽입 단추를 클릭, 포스트백이 발생할 고 삽입 워크플로 펼칩니다. 첫 번째, DetailsView s [ `ItemInserting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx) 발생 합니다. 다음으로 ObjectDataSource s `Insert()` 메서드가 호출 되 면 새 레코드에 추가 되는 결과 `Categories` 테이블입니다. 그런 다음 DetailsView s [ `ItemInserted` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx) 발생 합니다.

ObjectDataSource가 하기 전에 `Insert()` 메서드가 호출 되 면 먼저 적절 한 파일 형식을 사용자가 업로드 된를 확인 하 고 PDF 브로슈어의 웹의 서버 파일 시스템에 저장 해야 했습니다. DetailsView s에 대 한 이벤트 처리기를 만들고 `ItemInserting` 이벤트 다음 코드를 추가 합니다.


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample6.vb)]

이벤트 처리기를 참조 하 여 시작 된 `BrochureUpload` DetailsView s 템플릿에서 FileUpload 컨트롤입니다. 그런 다음 브로슈어에 업로드 한 경우 업로드 된 파일의 확장명 검사 됩니다. 확장이 없는 경우. PDF, 다음 경고가 표시 됩니다 하 고 삽입 취소 이벤트 처리기의 실행이 종료 합니다.

> [!NOTE]
> PDF 문서 업로드 된 파일 인지 확인 하는 확실 한 기법 아닙니다 업로드 파일의 확장에 의존 합니다. 확장을 사용 하 여 유효한 PDF 문서를 보유할 수 있습니다 `.Brochure`, 또는 수 아닌 PDF 문서를 지정 하는 `.pdf` 확장 합니다. 파일이 이진 콘텐츠를 더 확실히 파일 형식을 확인 하기 위해 프로그래밍 방식으로 검사할 해야 합니다. 이러한 철저 한 접근 방식을 그러나 많습니다 과도; 확장을 확인 하는 것은 대부분의 시나리오 충분 합니다.


에 설명 된 대로 합니다 [파일 업로드](uploading-files-vb.md) 자습서, 파일 시스템에 저장 파일을 해당 사용자가의 업로드 다른 s를 덮어쓰지 않습니다 있도록 때 주의 기울여야 합니다. 이 자습서에서는 업로드 된 파일과 같은 이름을 사용 하려고 합니다. 그러나 파일에 이미 존재 하는 경우는 `~/Brochures` 디렉터리는 동일한 파일 이름 가진 고유 이름의 찾을 때까지 끝에 번호를 추가 하겠습니다 했습니다. 예를 들어, 사용자 라는 브로슈어 파일을 업로드 하는 경우 `Meats.pdf`, 라는 파일이 이미 있지만 `Meats.pdf` 에 `~/Brochures` 폴더에 저장 된 파일 이름을 변경 했습니다 `Meats-1.pdf`합니다. 존재 하는 경우 새 해 `Meats-2.pdf`, 등의 고유한 파일 이름의 찾을 때까지 합니다.

다음 코드에서는 합니다 [ `File.Exists(path)` 메서드](https://msdn.microsoft.com/library/system.io.file.exists.aspx) 지정 된 파일 이름의 파일을 이미 있는지 확인 합니다. 따라서 계속 하는 경우 충돌이 발생 하지 발견 될 때까지 브로슈어에 대 한 새 파일 이름을 시도 하십시오.


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample7.vb)]

파일을 파일 시스템 및 ObjectDataSource s에 저장 해야 올바른 파일 이름을 찾은 `brochurePath``InsertParameter` 값이 파일 이름은 데이터베이스에 기록 되도록 업데이트 해야 합니다. 다시 살펴본 것 처럼 합니다 *파일 업로드* 자습서에서는 파일을 저장할 s FileUpload 컨트롤을 사용 하 여 `SaveAs(path)` 메서드. ObjectDataSource가 업데이트할 `brochurePath` 매개 변수를 사용 하 여는 `e.Values` 컬렉션입니다.


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample8.vb)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>데이터베이스에 업로드 된 그림을 저장 하는 7 단계:

새 업로드 된 그림을 저장할 `Categories` ObjectDataSource s에 업로드 한 이진 콘텐츠를 할당 하려면 먼저 레코드 `picture` DetailsView에서 매개 변수 `ItemInserting` 이벤트입니다. 그러나이 할당을 하기 전의 해야 먼저 업로드 된 그림 JPG 및 다른 않은 이미지 형식 인지를 확인 합니다. 6 단계와 같이 해당 형식이 정확 하 게 업로드 된 그림의 파일 확장명을 사용 하는 s 수 있습니다.

하는 동안를 `Categories` 테이블을 사용 하면 `NULL` 에 대 한 값을 `Picture` 열에 모든 범주에 현재 있는 그림입니다. 이 페이지를 통해 새 범주를 추가 하는 경우 그림을 제공 하도록 사용자를 강제로 s 수 있습니다. 다음 코드는 사진 업로드 된 및 적절 한 확장에 있는지 확인 합니다.


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample9.vb)]

이 코드를 배치할 *하기 전에* 6 단계에서에서 코드는 그림 업로드를 사용 하 여 문제가 있으면 브로슈어 파일은 파일 시스템에 저장 되기 전에 이벤트 처리기가 종료 됩니다.

적절 한 파일을 업로드 한 가정 코드의 다음 줄을 사용 하 여 그림 매개 변수의 값에 업로드 한 이진 콘텐츠를 할당:


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample10.vb)]

## <a name="the-completeiteminsertingevent-handler"></a>전체`ItemInserting`이벤트 처리기

완결성 같습니다는 `ItemInserting` 전체에서 이벤트 처리기:


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample11.vb)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>8 단계: 수정 된`DisplayCategoryPicture.aspx`페이지

Let s 삽입 인터페이스를 테스트 하려면 잠시 및 `ItemInserting` 몇 단계 지난 생성 된 이벤트 처리기입니다. 방문을 `UploadInDetailsView.aspx` 브라우저 및 그림에서 생략 범주를 추가 하려는 시도 통해 페이지 또는 비 JPG 사진이 나 PDF가 아닌 브로슈어를 지정 합니다. 이러한 경우에 오류 메시지가 표시 되 고 삽입 워크플로가 취소 합니다.


[![경고 메시지를 표시 하는 경우 잘못 된 파일 형식 업로드](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image15.png)

**그림 9**: 잘못 된 파일 형식 업로드 된 경우 표시 되는 경고 메시지는 ([큰 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image16.png))


확인 한 후 페이지 사진을 업로드할 필요 및 획득된 t PDF가 아닌 또는 비 JPG 파일을 사용할 수, 유효한 JPG 그림을 사용 하 여 새 범주 추가 브로슈어 필드를 비워 두면 됩니다. 삽입 단추를 클릭 한 후 페이지 포스트백 됩니다 및 새 레코드를 추가할 수는 `Categories` 데이터베이스에 직접 저장 s 이미지를 업로드 한 이진 콘텐츠를 사용 하 여 테이블입니다. GridView 업데이트 되 고 새로 추가 된 범주에 대 한 행을 표시 하지만 새 범주의 사진을 그림 10과 같이 올바르게 렌더링 되지 않습니다.


[![새 범주의의 그림 표시 되지 않습니다](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image17.png)

**그림 10**:의 새 종류 s 그림 표시 되지 않습니다 ([큰 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image18.png))


새 그림 표시 되지 이유 때문입니다는 `DisplayCategoryPicture.aspx` 지정한 범주의 그림을 반환 하는 페이지는 OLE 머리글 있는 비트맵을 처리 하도록 구성 되어 있습니다. 이 78 바이트 헤더에서 제거 되는 `Picture` 클라이언트로 다시 전송 되기 전에 열 s 이진 내용입니다. 이 OLE 머리글; 없는 새 범주의 방금 업로드 한 JPG 파일 따라서 유효 하 고 필요한 바이트 이미지 s 이진 데이터에서 제거 되 고 됩니다.

이제 두 비트맵 OLE 머리글 및 Jpg에 있기 때문 합니다 `Categories` 테이블을 업데이트 해야 `DisplayCategoryPicture.aspx` 원래 8 가지 범주에 대 한 제거 OLE 머리글 존재 하며 최신 범주 레코드를 위한이 제거를 무시 되도록 합니다. 다음 자습서에서는 검토 기존 레코드의 이미지를 업데이트 하는 방법 및 Jpg 수 있도록 모든 이전 범주 사진을 업데이트 됩니다. 이제 다음 코드를 사용 하지만 `DisplayCategoryPicture.aspx` 해당 원래 8 가지 범주에만 OLE 머리글을 제거 합니다.


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample12.vb)]

이 변경으로 JPG 이미지는 GridView에서 올바르게 렌더링 이제 합니다.


[![새 범주에 대 한 JPG 이미지 잘못 렌더링 됩니다.](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image19.png)

**그림 11**: 새 범주에 대 한 The JPG 이미지는 잘못 렌더링 ([큰 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image20.png))


## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>9 단계: 예외가 발생 하는 경우 브로슈어 삭제

웹 서버의 파일 시스템에 이진 데이터를 저장 하는 문제 중 하나 사이 데이터 모델 및 해당 이진 데이터는 소개입니다. 따라서 레코드가 삭제 될 때마다 파일 시스템에서 해당 이진 데이터를 제거도 해야 합니다. 이 값은을 삽입할 때 바로 가져올 수 있습니다. 다음 시나리오를 고려 합니다: 사용자는 유효한 그림 및 브로슈어 지정 새 범주를 추가 합니다. 포스트백이 발생할 삽입 단추를 클릭 및 DetailsView의 `ItemInserting` 브로슈어 웹의 서버 파일 시스템에 저장 되는 이벤트가 발생 합니다. 다음, ObjectDataSource s `Insert()` 메서드를 호출 하는 `CategoriesBLL` s 클래스 `InsertWithPicture` 메서드를 호출 하는 합니다 `CategoriesTableAdapter` s `InsertWithPicture` 메서드.

이제, 데이터베이스를 오프 라인 상태인 경우 어떻게 되나요 또는 오류 인지를 `INSERT` SQL 문을? 명확 하 게 삽입 실패 하므로 데이터베이스에 없는 새 범주 행이 추가 됩니다. 하지만 웹 서버의 파일 시스템에 위치한 업로드 브로슈어 파일이 아직! 이 파일을 삽입 워크플로 중에 예외가 발생 하는 경우 삭제 해야 합니다.

설명한 것 처럼 합니다 [처리 BLL 및 DAL 수준의 예외 ASP.NET 페이지에서](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) 자습서에서는 다양 한 계층을 통해 버블링 됩니다 아키텍처에 대 한 깊이 있는 내에서 예외가 throw 되 면 합니다. DetailsView s에서 예외가 발생 한 경우 확인할 수 있습니다 프레젠테이션 계층에서 `ItemInserted` 이벤트입니다. 이 이벤트 처리기는 또한 ObjectDataSource s의 값을 제공 `InsertParameters`합니다. 이벤트 처리기를 만들 수 있습니다 따라서 합니다 `ItemInserted` ObjectDataSource s로 지정 된 파일을 삭제 하는 이벤트 확인 되었으면 예외가 고 그렇다면 `brochurePath` 매개 변수:


[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample13.vb)]

## <a name="summary"></a>요약

이진 데이터를 포함 하는 레코드를 추가 하는 웹 기반 인터페이스를 제공 하기 위해 수행 해야 하는 단계는 여러 가지가 있습니다. 데이터베이스에 직접 저장 되는 이진 데이터, 해야 아키텍처에 업데이트 이진 데이터가 삽입 되는 경우를 처리 하는 특정 메서드를 추가 하는 것이 경우가 있습니다. 아키텍처를 업데이트 하면 다음 단계는 각 이진 데이터 필드에 대 한 FileUpload 컨트롤을 포함 하도록 사용자 지정 않은 DetailsView를 사용 하 여 수행할 수 있습니다 삽입 인터페이스를 만드는 것입니다. 업로드 된 데이터를 웹 서버의 파일 시스템에 저장 하거나 수 DetailsView에서 데이터 원본 매개 변수에 할당할 `ItemInserting` 이벤트 처리기입니다.

파일 시스템에 이진 데이터를 저장 하는 중 데이터베이스에 직접 데이터를 저장 하는 보다 더 많은 계획이 필요 합니다. 다른 s 덮어쓰지 하나의 사용자가의 업로드를 방지 하기 위해 이름 지정 체계를 선택 해야 합니다. 또한 데이터베이스 삽입이 실패 하는 경우 업로드 된 파일을 삭제 하려면 추가 단계를 수행 해야 합니다.

이제 브로슈어 및 그림 했지만 사용 하 여 시스템에 새 범주를 추가 하는 기능 ve 아직를 올바르게 삭제 된 범주에 대 한 이진 데이터를 제거 하는 방법 및 기존 범주 s 이진 데이터를 업데이트 하는 방법. 다음 자습서에서 이러한 두 항목을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dave Gardner, Teresa Murphy 및 박 광 준 Leigh 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-binary-data-in-the-data-web-controls-vb.md)
> [다음](updating-and-deleting-existing-binary-data-vb.md)
