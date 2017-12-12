---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
title: "파일을 포함 하 여 업로드 옵션 (C#) 새 레코드를 추가 하는 경우 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에는 텍스트 데이터를 모두 입력 한 이진 파일을 업로드할 수 있는 웹 인터페이스를 만드는 방법을 보여 줍니다. 옵션 사용 가능한 t 보여 주기 위해 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: 362ade25-3965-4fb2-88d2-835c4786244f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
msc.type: authoredcontent
ms.openlocfilehash: fcb791868e6af9eef1614d039d11ef5232b40af5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="including-a-file-upload-option-when-adding-a-new-record-c"></a>새 레코드 (C#)를 추가할 때 파일 업로드 옵션을 포함 하 여
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_CS.exe) 또는 [PDF 다운로드](including-a-file-upload-option-when-adding-a-new-record-cs/_static/datatutorial56cs1.pdf)

> 이 자습서에는 텍스트 데이터를 모두 입력 한 이진 파일을 업로드할 수 있는 웹 인터페이스를 만드는 방법을 보여 줍니다. 파일 시스템에 저장 된 다른 동안 하나의 파일이 이진 데이터를 저장 하는 옵션을 설명 하기 위해 데이터베이스에 저장 됩니다.


## <a name="introduction"></a>소개

파일을 보내고 하려면 클라이언트에서 웹 서버에 데이터 W에에서 이진 데이터를 표시 하는 방법에 대해 파일 업로드 컨트롤을 사용 하는 방법을 알아보았습니다 응용 프로그램의 데이터 모델에 연결 된 이진 데이터를 저장 하기 위한 기술을 이전 두 자습서에서 살펴본 eb 컨트롤입니다. 에서는 데이터 모델을 사용 하지만 업로드 된 데이터를 연결 하는 방법에 대 한 대화를 아직 했습니다.

이 자습서에서는 새 범주를 추가 하려면 웹 페이지를 만듭니다. 범주의 이름 및 설명에 대 한 텍스트 상자 이외에이 페이지는 새 범주의 그림에 대 한 파일 업로드 컨트롤을 두 가지 및 브로슈어 하나 포함 해야 합니다. 업로드 된 그림은 새 레코드 s에 직접 저장 됩니다 `Picture` 열 브로슈어에 저장 하도록 하는 반면는 `~/Brochures` s 새 레코드에 저장 된 파일 경로 폴더 `BrochurePath` 열입니다.

이 새로운 웹 페이지를 만들기 전에 아키텍처를 업데이트 해야 합니다. `CategoriesTableAdapter` s 주 쿼리를 검색 하지 않습니다는 `Picture` 열입니다. 따라서 자동 생성 `Insert` 만 대 한 입력이 메서드는 `CategoryName`, `Description`, 및 `BrochurePath` 필드입니다. 4를 모두 입력 해야 하는 TableAdapter에는 다른 방법을 추가로 만들어야 한다는 따라서 `Categories` 필드입니다. `CategoriesBLL` 클래스는 비즈니스 논리 계층에서 업데이트 해야 합니다.

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>1 단계: 추가 된`InsertWithPicture`메서드는`CategoriesTableAdapter`

만들 때는 `CategoriesTableAdapter` 다시는 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-cs.md) 자습서에서는 구성 하 여 자동으로 생성 `INSERT`, `UPDATE`, 및 `DELETE` 문을 주 쿼리를 기반 합니다. 메서드 생성 DB 직접 접근 방식을 사용 하 여 TableAdapter를 지시 우리는 또한 `Insert`, `Update`, 및 `Delete`합니다. 이러한 메서드는 자동으로 생성 된 실행 `INSERT`, `UPDATE`, 및 `DELETE` 문 및 결과적 주 쿼리에서 반환 된 열을 기반으로 하는 입력된 매개 변수를 허용 합니다. 에 [파일 업로드](uploading-files-cs.md) 자습서 augmented 우리는 `CategoriesTableAdapter` s 주 쿼리를 사용 하는 `BrochurePath` 열.

이후는 `CategoriesTableAdapter` s 주 쿼리에서 참조 하지 않습니다는 `Picture` 열을 새 레코드를 추가 하거나에 대 한 값을 가진 기존 레코드를 업데이트할 수 있습니다는 `Picture` 열입니다. 이 정보를 캡처하려면, 우리는 새로운 방법이 이진 데이터로 레코드를 삽입 하는 데 특별히 사용 되는 TableAdapter의 만들거나 자동으로 생성 된 사용자를 지정할 수 있습니다 `INSERT` 문. 자동으로 생성 된 사용자 지정 문제가 `INSERT` 문은 위험 우리는 사용자 지정 마법사에 의해 덮어쓸 것입니다. 예를 들어, 사용자 지정 했습니다를 가정은 `INSERT` 의 사용을 포함 하도록 문을 `Picture` 열입니다. 이렇게 하면 TableAdapter s 업데이트는 `Insert` 메서드 범주의 그림 s 이진 데이터에 대 한 추가 입력된 매개 변수를 포함 하도록 합니다. 그런 다음이 DAL 메서드를 사용 하 고 프레젠테이션 계층을 통해이 BLL 메서드를 호출 하는 비즈니스 논리 계층에는 메서드를 만들 수 하 고 모든 아주 작동 합니다. 즉, 다음 시간까지 TableAdapter 구성 마법사를 통해 TableAdapter를 구성 했습니다. 마법사는 사용자 지정을 완료 하는 즉시는 `INSERT` 문을 덮어쓰게 됩니다는 `Insert` 메서드는 이전 상태로 되돌린 코드는 더 이상 컴파일되지 않습니다!

> [!NOTE]
> 임시 SQL 문 대신 저장된 프로시저를 사용 하는 경우이 불편은 비-문제. 이후 자습서를 참조 하는 대신이 임시 SQL 문이 저장된 프로시저를 사용 하 여 데이터 액세스 계층에서 탐색 합니다.


이 가능성을 방지 하려면 자동 생성 된 SQL 문 사용자 지정 하는 것이 아니라 함으로써, TableAdapter에 대 한 새 메서드를 대신 만든이 있습니다. 라는이 메서드를 `InsertWithPicture`에 대 한 값을 수락할는 `CategoryName`, `Description`, `BrochurePath`, 및 `Picture` 열 및 실행는 `INSERT` 새 레코드의 모든 4 개의 값을 저장 하는 문입니다.

열고 입력 데이터 집합 디자이너에서 마우스 오른쪽 단추로 클릭는 `CategoriesTableAdapter`의 헤더 상황에 맞는 메뉴에서 추가 쿼리를 선택 합니다. 요청 하는 TableAdapter 쿼리는 데이터베이스에 액세스 하는 방법으로 시작 하는 TableAdapter 쿼리 구성 마법사가 시작 됩니다. SQL 문 사용을 선택 하 고 클릭 합니다. 다음 단계에서는 메시지를 생성 쿼리 형식에 대 한 표시 합니다. 이후 새 레코드를 추가 하는 쿼리를 만드는 다시 우리는 `Categories` 테이블 삽입을 선택 하 고 다음을 클릭 합니다.


[![삽입 옵션을 선택 합니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.png)

**그림 1**: 삽입 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.png))


지금 지정 해야는 `INSERT` SQL 문입니다. 마법사가 자동으로 제안는 `INSERT` TableAdapter s 주 쿼리에 해당 하는 문입니다. 이 경우 그 s는 `INSERT` 문을 삽입 하는 `CategoryName`, `Description`, 및 `BrochurePath` 값입니다. 설명서를 업데이트 하는 `Picture` 열이 함께 포함 됩니다는 `@Picture` 매개 변수를 다음과 같이:


[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample1.sql)]

마법사의 마지막 화면에 새 TableAdapter 메서드 이름을 묻는 메시지가 나타납니다. 입력 `InsertWithPicture` 하 고 마침을 클릭 합니다.


[![새 TableAdapter 메서드 InsertWithPicture 이름](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.png)

**그림 2**: 새 TableAdapter 메서드 이름을 `InsertWithPicture` ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.png))


## <a name="step-2-updating-the-business-logic-layer"></a>2 단계: 비즈니스 논리 계층 업데이트

데이터 액세스 계층으로 직접 이동 하 여 우회를 만들어야 한다는 방금 만든 DAL 메서드를 호출 하는 BLL 메서드 대신 비즈니스 논리 계층와 프레젠테이션 계층 상호만 해야 하므로 (`InsertWithPicture`). 이 자습서에 메서드를 만듭니다는 `CategoriesBLL` 라는 클래스 `InsertWithPicture` 입력된으로 3을 수락 하 `string` s 및 `byte` 배열입니다. `string` s 범주 이름, 설명 및 브로슈어 파일 경로 대 한 입력된 매개 변수는 동안는 `byte` 범주의 그림의 이진 콘텐츠는 배열입니다. 다음 코드에서 볼 수 있듯이이 BLL 메서드 해당 DAL 메서드를 호출 합니다.


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample2.cs)]

> [!NOTE]
> 추가 하기 전에 입력 데이터 집합을 저장 했는지 확인는 `InsertWithPicture` BLL 메서드입니다. 이후는 `CategoriesTableAdapter` 클래스 코드는 자동으로 생성 된 형식화 된 데이터 집합에 따라 t 않으면 사용자는 먼저 변경 내용을 형식화 된 데이터 집합에 저장 하는 경우는 `Adapter` t 성공한 속성에 대해 알고는 `InsertWithPicture` 메서드.


## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>3 단계: 기존 범주 및 이진 데이터를 나열합니다.

이 자습서에서는 만듭니다는 최종 사용자는 시스템에 새 범주를 추가할 수 있는 페이지를 새 범주에 대 한 그림 및 브로슈어를 제공 합니다. 에 [이전 자습서](displaying-binary-data-in-the-data-web-controls-cs.md) 각 범주의 이름을 표시 하는 GridView TemplateField 및 ImageField 사용 설명, 그림 및 해당 브로슈어 다운로드 링크를 합니다. 이 자습서에서는 모두 모든 기존 범주를 나열 하 고 새 테스트를 만들 수를 허용 하는 페이지 만들기에 대 한 해당 기능을 복제 하는 s를 사용 합니다.

열어 시작는 `DisplayOrDownload.aspx` 에서 페이지는 `BinaryData` 폴더입니다. 소스 보기로 이동 하 고는 GridView 및 ObjectDataSource s 선언적 구문, 붙여 넣어 내에서 복사 된 `<asp:Content>` 요소에 `UploadInDetailsView.aspx`합니다. 또한 잊지 마십시오 통해 복사 하 여 `GenerateBrochureLink` 의 코드 숨김 클래스의에서 메서드를 `DisplayOrDownload.aspx` 를 `UploadInDetailsView.aspx`합니다.


[![복사 및 붙여넣기를 UploadInDetailsView.aspx DisplayOrDownload.aspx의 선언 구문](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.png)

**그림 3**: 선언적 구문에서 복사한 `DisplayOrDownload.aspx` 를 `UploadInDetailsView.aspx` ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.png))


선언적 구문을 복사한 후 및 `GenerateBrochureLink` 를 통해 메서드는 `UploadInDetailsView.aspx` 페이지에서 모든 항목을 복사 했는지 확인을 통해 제대로에 브라우저를 통해 페이지 보기. 8 개 범주를 나열 범주의 그림 뿐만 아니라 브로슈어 다운로드 링크를 포함 하는 GridView 표시 되어야 합니다.


[![이제 해당 이진 데이터와 함께 각 범주 표시](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.png)

**그림 4**: 있습니다 해야 이제 참조 각 범주에 따라 해당 이진 데이터 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.png))


## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>4 단계: 구성에서`CategoriesDataSource`지원 삽입 하려면

`CategoriesDataSource` ObjectDataSource에서 사용 하는 `Categories` GridView 현재 데이터를 삽입 하는 기능은 제공 하지 않습니다. 이 데이터 소스 제어를 통해 삽입을 지원 하려면 매핑할 해야 해당 `Insert` 의 내부 개체에서 메서드에 `CategoriesBLL`합니다. 특히, 매핑합니다 하려고는 `CategoriesBLL` 2 단계에서 다시 추가 하는 메서드 `InsertWithPicture`합니다.

ObjectDataSource s 스마트 태그에서 데이터 소스 구성 링크를 클릭 하 여 시작 합니다. 첫 번째 화면에 데이터 원본을 함께 작동 하도록 구성 하는 개체가 표시 `CategoriesBLL`합니다. 이 설정을 상태로 둡니다-되 고 클릭 데이터 메서드 정의 화면으로 이동 합니다. 삽입 탭으로 이동 하 고 선택 된 `InsertWithPicture` 드롭 다운 목록에서 메서드. 마법사를 완료 하려면 마침을 클릭 합니다.


[![ObjectDataSource InsertWithPicture 메서드를 사용 하도록 구성](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.png)

**그림 5**: ObjectDataSource 사용 하도록 구성 된 `InsertWithPicture` 메서드 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.png))


> [!NOTE]
> 마법사를 완료 되 면 Visual Studio 필드 새로 고침 및 키 하려는 경우에 필드 제어 웹 데이터를 다시 생성 됩니다는 요청할 수 있습니다. 예를 선택 하면 필드 사용자 지정 사용자가 변경한 내용이 덮어쓰게 됩니다 아니요를 선택 합니다.


마법사를 완료 한 후의 ObjectDataSource 포함 합니다에 대 한 값 해당 `InsertMethod` 속성으로 `InsertParameters` 4 개의 범주 열에 대 한 다음과 같은 선언적 태그가 보여줍니다.


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>5 단계: 삽입 인터페이스 만들기

First와에서 다루는 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md), DetailsView 컨트롤 삽입을 지원 하는 데이터 소스 컨트롤과 함께 사용할 때 활용할 수 있는 기본 제공 삽입 인터페이스를 제공 합니다. 사용자가 신속 하 게 새 범주를 추가할는 삽입 인터페이스를 영구적으로 렌더링 하는 GridView 위의이 페이지에 DetailsView 컨트롤을 추가 하는 s를 사용 합니다. DetailsView에 새 범주를 추가, 시 GridView 아래에 자동으로 새로 고침 고 새 범주를 표시 됩니다.

DetailsView 설정 GridView 위에 디자이너 도구 상자에서 끌어 시작 해당 `ID` 속성을 `NewCategory` 정리 하 고는 `Height` 및 `Width` 속성 값입니다. DetailsView s 스마트 태그에서 기존에 바인딩할 `CategoriesDataSource` 한 다음 삽입 사용 확인란을 선택 합니다.


[![DetailsView의 CategoriesDataSource에 바인딩하고 삽입 사용](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.png)

**그림 6**: DetailsView에 바인딩하는 `CategoriesDataSource` 삽입 사용 하 고 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image12.png))


설정의 삽입 인터페이스에서 DetailsView를 영구적으로 렌더링 하려면 해당 `DefaultMode` 속성을 `Insert`합니다.

DetailsView에 5 개의 BoundFields `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`, 및 `BrochurePath` 있지만 `CategoryID` 때문에 삽입 하는 인터페이스에 BoundField 렌더링 되지 않습니다는 `InsertVisible` 속성이 `false`합니다. 반환 되는 열이 있기 때문에 이러한 BoundFields 존재는 `GetCategories()` 메서드 데이터를 검색 하도록 호출 될는 ObjectDataSource를 합니다. 그러나 삽입에 대 한 우리 않는 대 한 값을 지정할 수 있도록 원하지 `NumberOfProducts`합니다. 또한 새 범주에 대 한 사진 업로드 수 있을 뿐만 아니라 브로슈어 PDF 업로드 하도록 허용 해야 합니다.

제거는 `NumberOfProducts` DetailsView 모두 및 다음 업데이트에서 BoundField는 `HeaderText` 의 속성은 `CategoryName` 및 `BrochurePath` BoundFields 범주와 브로슈어에 각각. 다음으로 변환 된 `BrochurePath` BoundField를 TemplateField로를이 새로운 TemplateField를 제공 하는 그림에 대 한 새 TemplateField 추가 `HeaderText` 그림의 값입니다. 이동의 `Picture` 한다는 간의 이므로 TemplateField는 `BrochurePath` TemplateField 및 CommandField 합니다.


![DetailsView의 CategoriesDataSource에 바인딩하고 삽입 사용](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.gif)

**그림 7**: DetailsView에 바인딩하는 `CategoriesDataSource` 삽입을 사용 하도록 설정


변환한 경우는 `BrochurePath` 필드 편집 대화 상자를 통해 TemplateField로 BoundField TemplateField는 포함 된 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate`합니다. 하지만만 `InsertItemTemplate` 가 필요 제한이 없으므로 다른 두 가지 서식 파일을 제거 합니다. 이 시점에서 DetailsView s 선언적 구문 다음과 같이 표시 됩니다.


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>브로슈어 및 그림 필드에 대 한 파일 업로드 컨트롤을 추가합니다.

현재는 `BrochurePath` TemplateField s `InsertItemTemplate` TextBox를 포함 하는 동안는 `Picture` TemplateField는 템플릿에 포함 되지 않습니다. 이러한 두 TemplateField s를 업데이트 해야 `InsertItemTemplate` 파일 업로드 컨트롤을 사용 하도록 합니다.

DetailsView s 스마트 태그에서 템플릿 편집 옵션을 선택 하 고 다음 선택에서 `BrochurePath` TemplateField의 `InsertItemTemplate` 드롭 다운 목록에서 합니다. TextBox를 제거한 다음 서식 파일을 도구 상자에서 파일 업로드 컨트롤을 끌어 옵니다. 파일 업로드 컨트롤 s 설정 `ID` 를 `BrochureUpload`합니다. 마찬가지로, 파일 업로드 컨트롤을 추가 `Picture` TemplateField의 `InsertItemTemplate`합니다. 이 파일 업로드 컨트롤 s 설정 `ID` 를 `PictureUpload`합니다.


[![InsertItemTemplate에 파일 업로드 컨트롤 추가](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image13.png)

**그림 8**: 파일 업로드 컨트롤을 추가 `InsertItemTemplate` ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image14.png))


에 추가 하는이 코드를 확인 한 후에 두 개의 TemplateField s 선언적 구문이 됩니다.


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample5.aspx)]

새 범주를 추가 하면 사용자 브로슈어와 그림의 올바른 파일 형식 인지 확인 하는 것이 좋습니다. 브로슈어에 대 한 사용자는 PDF를 제공 해야 합니다. 그림에 대 한 이미지 파일을 업로드 하려면 사용자 하지만 허용 म *모든* 이미지 파일이 나 특정 등의 형식, Gif 또는 Jpg 이미지 파일에만? 다른 파일 형식에 대 한 수 있도록 하기 위해 d 확장 해야는 `Categories` 이 형식을 통해 클라이언트에 게 보낼 수 있도록 파일 형식을 캡처하는 열을 포함 하도록 스키마를 `Response.ContentType` 에서 `DisplayCategoryPicture.aspx`합니다. 인할 우리는 이러한 열이만 특정 이미지 파일 형식을 제공 하기 위해 사용자가 제한 하려면 현명입니다. `Categories` 테이블 s 기존 이미지는 비트맵을 하지만 Jpg는 웹을 통해 제공 되는 이미지에 대 한 보다 적절 한 파일 형식입니다.

잘못 된 파일 형식을 업로드 하는 사용자, 삽입을 취소 하는 문제를 나타내는 메시지를 표시 해야 합니다. DetailsView 아래 Label 웹 컨트롤을 추가 합니다. 설정의 `ID` 속성을 `UploadWarning`아웃 지우기, 해당 `Text` 속성을 설정는 `CssClass` 경고로 속성 및 `Visible` 및 `EnableViewState` 속성을 `false`합니다. `Warning` CSS 클래스에 정의 된 `Styles.css` 큰, 빨간색, 기울임꼴, 굵은 글꼴의 텍스트를 렌더링 합니다.

> [!NOTE]
> 이상적으로 `CategoryName` 및 `Description` BoundFields TemplateFields 요소 및 구성 요소 인터페이스 사용자 지정 된 삽입으로 변환 됩니다. `Description` 예를 들어 인터페이스 삽입은 가능성이 더 적합할 여러 줄 텍스트 상자를 통해. 및 이후는 `CategoryName` 열을 허용 하지 않습니다 `NULL` 값을 한 RequiredFieldValidator 새 범주의 이름에 대 한 값을 제공 하는 사용자 확인에 추가 해야 합니다. 이러한 단계는 연습으로 판독기에 남아 있습니다. 다시 참조 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 에 대 한 데이터 수정 인터페이스 확대 살펴봅니다.


## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>6 단계: 웹 서버의 파일 시스템에 업로드 된 브로슈어 저장

사용자는 새 범주에 대 한 값을 입력 하 고 삽입 단추를 클릭, 포스트백이 발생할 고 삽입 워크플로 펼칩니다. 먼저, DetailsView s [ `ItemInserting` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx) 발생 합니다. 다음, ObjectDataSource s `Insert()` 메서드가 호출 되 면 새 레코드에 추가 되 고 결과 `Categories` 테이블입니다. DetailsView s 그 후 [ `ItemInserted` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx) 발생 합니다.

ObjectDataSource s 하기 전에 `Insert()` 메서드가 호출 되 면 먼저 적절 한 파일 형식을 사용자가 업로드 한을 확인 하 고 다음 브로슈어 PDF 웹 서버의 파일 시스템에 저장 해야 했습니다. DetailsView s에 대 한 이벤트 처리기를 만들고 `ItemInserting` 이벤트를 다음 코드를 추가 합니다.


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample6.cs)]

이벤트 처리기를 참조 하 여 시작 된 `BrochureUpload` DetailsView s 템플릿에서 파일 업로드 컨트롤입니다. 그런 다음 브로슈어 업로드 한 경우 업로드 된 파일의 확장명을 검사 합니다. 확장명 없는 경우 합니다. PDF, 다음 경고가 표시 됩니다, 취소 되는 insert 및 이벤트 처리기의 실행이 끝날 합니다.

> [!NOTE]
> 확실 한 기술 인지 확인 하는 업로드 된 파일은 PDF 문서에 대 한 않습니다 업로드 파일의 확장에 의존 합니다. 확장명을 가진 유효한 PDF 문서를 보유할 수 `.Brochure`, 또는 수 라인 PDF가 아닌 문서를 제공 받은 `.pdf` 확장 합니다. 파일 s 이진 콘텐츠를 더 확실히 파일 형식을 확인 하기 위해 프로그래밍 방식으로 검사할 해야 합니다. 이러한 철저 한 방법을 하지만 많습니다 개념을 세우; 확장을 확인 하는 것은 대부분의 경우 충분 합니다.


에 설명 된 대로 [파일 업로드](uploading-files-cs.md) 자습서, 파일 시스템에 저장 파일을 해당 사용자의 업로드 다른 s를 덮어쓰지 않습니다 하므로 때 주의 해야 합니다. 이 자습서와 업로드 된 파일은 동일한 이름을 사용 하려고 합니다. 그러나 파일에 이미 존재 하는 경우는 `~/Brochures` 같은 이름의 파일을 디렉터리 고유 이름을 발견 될 때까지 끝에 번호를 추가 합니다 했습니다. 예를 들어, 사용자 라는 브로슈어 파일을 업로드 하는 경우 `Meats.pdf`, 라는 파일은 이미 있지만 `Meats.pdf` 에 `~/Brochures` 폴더에 저장 된 파일 이름을 변경 합니다 `Meats-1.pdf`합니다. 존재 하는 경우 새 해 `Meats-2.pdf`, 등의 고유한 파일 이름이 발견 될 때까지 합니다.

다음 코드에서는 [ `File.Exists(path)` 메서드](https://msdn.microsoft.com/en-us/library/system.io.file.exists.aspx) 지정 된 파일 이름의 파일이 이미 있는지 확인 하려면. 이 경우 계속 충돌이 발생 하지 발견 될 때까지 브로슈어에 대 한 새 파일 이름을 시도 합니다.


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample7.cs)]

파일을 파일 시스템 및 ObjectDataSource s에 저장 해야 올바른 파일 이름을 찾은 `brochurePath``InsertParameter` 값이 파일 이름은 데이터베이스에 기록 됩니다 되도록 업데이트 해야 합니다. 다시에서 설명한 것 처럼는 *파일 업로드* 자습서 파일 수을 저장할 수 파일 업로드 컨트롤 s를 사용 하 여 `SaveAs(path)` 메서드. ObjectDataSource s 업데이트 하려면 `brochurePath` 매개 변수를 사용 하 여는 `e.Values` 컬렉션입니다.


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample8.cs)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>데이터베이스에 업로드 된 그림을 저장 하는 7 단계:

새에 업로드 된 그림을 저장 하려면 `Categories` 를 ObjectDataSource s에 업로드 된 이진 콘텐츠를 할당 해야 레코드, `picture` DetailsView s에서 매개 변수 `ItemInserting` 이벤트입니다. 그러나이 할당, 하기 전의 해야 먼저 업로드 그림은 JPG 및 다른 하지 일부 이미지 형식 인지를 확인 합니다. 6 단계에서와 같이 해당 형식을 확인 하려면 업로드 된 그림의 파일 확장명을 사용 하는 s를 사용 합니다.

동안는 `Categories` 테이블을 사용 하면 `NULL` 에 대 한 값은 `Picture` 열에서 모든 범주에 현재 있는 그림입니다. 이 페이지를 통해 새 범주를 추가할 때 그림을 제공 하도록 사용자를 강제로 s를 사용 합니다. 다음 코드는 사진 업로드 되었는지 확인 하는 적절 한 확장에 확인 합니다.


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample9.cs)]

이 코드를 배치할 *전에* 6 단계에서에서 코드를 그림 업로드에 문제가 있으면 브로슈어 파일이 파일 시스템에 저장 되기 전에 이벤트 처리기가 종료 됩니다.

적절 한 파일 업로드 한 있다고 가정할 경우 업로드 된 이진에 콘텐츠 할당 코드의 다음 행으로 그림 매개 변수의 값:


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample10.cs)]

## <a name="the-completeiteminsertingevent-handler"></a>전체`ItemInserting`이벤트 처리기

다음은 완성도 높이기 위해는 `ItemInserting` 전체에서 이벤트 처리기.


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample11.cs)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>8 단계: 수정 된`DisplayCategoryPicture.aspx`페이지

Let s 삽입 인터페이스를 테스트 하려면 잠시 및 `ItemInserting` 몇 가지 단계는 마지막에 대해 생성 된 이벤트 처리기입니다. 방문는 `UploadInDetailsView.aspx` 브라우저 및 범주를 추가 하지만 그림을 생략 하는 시도 통해 페이지 하거나 비 JPG 그림 이나 PDF가 아닌 브로슈어 지정 합니다. 이러한 경우에 오류 메시지가 표시 되 고 삽입 워크플로 취소 합니다.


[![경고 메시지는 표시 된 잘못 된 파일 형식이 업로드 된 경우](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image15.png)

**그림 9**: A 경고 메시지는 표시 된 잘못 된 파일 형식이 업로드 된 경우 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image16.png))


확인 한 후 해당 페이지에 업로드 되도록 그림 하려면 및 획득된 t PDF가 아닌 또는 비 JPG 파일을 저장할, 유효한 JPG 사진이 있는 새 범주를 추가할 브로슈어 필드를 비워 두면 합니다. 삽입 단추를 클릭 한 후 페이지는 다시 게시 하 고 새 레코드에 추가 됩니다는 `Categories` 데이터베이스에 직접 저장 s 업로드 된 이미지의 이진 내용 포함 된 테이블입니다. GridView 업데이트 되 고 새로 추가 된 범주에 대 한 행을 표시 하지만 새 범주의 그림 그림 10과 같이 올바르게 렌더링 되지 않습니다.


[![새 범주의 그림 표시 되지 않습니다](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image17.png)

**그림 10**: 그림 표시 되지 않으면 다음 새 범주 s ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image18.png))


새 그림 표시 되지 않으면 이유 때문입니다는 `DisplayCategoryPicture.aspx` 페이지 지정 된 범주의 그림을 반환 하는 OLE 머리글 있는 비트맵을 처리할 구성 되어 있습니다. 이 78 바이트 헤더에서 제거 됩니다는 `Picture` 다시 클라이언트에 전송 되기 전에 열 s 이진 내용입니다. 하지만 새 범주에 대 한 방금 업로드 JPG 파일에는이 OLE 머리글; 없는 합니다. 따라서 유효 하 고 필요한 바이트는 이미지 s 이진 데이터에서 제거 되 고 있습니다.

이제 두 비트맵 OLE 머리글 및 Jpg에 있기 때문는 `Categories` 테이블을 업데이트 해야 `DisplayCategoryPicture.aspx` 는 원래 8 범주에 대 한 스트라이프 OLE 머리글 않으며 최신 레코드를 범주에 대 한이 제거를 무시 합니다. 다음이 자습서에서 기존 레코드의 이미지를 업데이트 하는 방법을 검토 합니다 및 Jpg 되도록 모든 이전 범주 그림 업데이트 합니다. 지금은 다음 코드를 사용 하지만 `DisplayCategoryPicture.aspx` 그 원래 8 개 범주에 대 한 OLE 머리글을 남겨 두려면:


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample12.cs)]

이러한 변경으로 인해 JPG 이미지는 GridView에서 올바르게 렌더링 이제 합니다.


[![새 범주에 대 한 개의 JPG 이미지가 제대로 렌더링 됩니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image19.png)

**그림 11**: 새 범주에 대 한 The JPG 이미지는 올바로 렌더링 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image20.png))


## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>9 단계: 예외가 발생할 때 브로슈어 삭제

웹 서버의 파일 시스템에 이진 데이터를 저장할 경우의 과제 중 하나는 사이 데이터 모델 및 해당 이진 데이터를 소개 것입니다. 따라서 레코드가 삭제 될 때마다 해당 이진 데이터를 파일 시스템에서 제거도 해야 합니다. 이 값은 삽입할 때를 가져올 수 있습니다. 시나리오: 사용자는 유효한 그림 및 브로슈어를 지정 하는 새 범주를 추가 합니다. 포스트백이 발생할 삽입 단추를 클릭 하 고 DetailsView s 시 `ItemInserting` 브로슈어 웹 서버의 파일 시스템에 저장 되는 이벤트 발생 합니다. 다음, ObjectDataSource s `Insert()` 메서드를 호출 하는 `CategoriesBLL` s 클래스 `InsertWithPicture` 메서드를 호출 하 여 `CategoriesTableAdapter` s `InsertWithPicture` 메서드.

Now, 데이터베이스가 오프 라인 상태 이면 어떤 일이 생기 또는에 오류가 있으면는 `INSERT` SQL 문을? 명확 하 게 삽입 실패 하므로 데이터베이스에 없는 새 범주 행이 추가 됩니다. 하지만 웹 서버의 파일 시스템에 위치한 업로드 브로슈어 파일이 아직! 이 파일을 삽입 하는 워크플로 중에 예외가 발생할 때 삭제 해야 합니다.

이전에 설명한 대로 [처리 BLL-및 ASP.NET 페이지에서 DAL 수준 예외](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 자습서에서는 중첩 된 다양 한 계층을 통해 있게 아키텍처에서 예외가 throw 되 면입니다. DetailsView s에서 예외가 발생 한 경우 확인할 수 있습니다 프레젠테이션 계층에서 `ItemInserted` 이벤트입니다. 이 이벤트 처리기는 또한 ObjectDataSource s의 값을 제공 `InsertParameters`합니다. 따라서에 대 한 이벤트 처리기를 만들 수 있습니다는 `ItemInserted` ObjectDataSource s로 지정 된 파일을 삭제 하는 경우 예외가 발생 했습니다. 그리고 있다면 확인 하는 이벤트 `brochurePath` 매개 변수:


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample13.cs)]

## <a name="summary"></a>요약

이진 데이터를 포함 하는 레코드를 추가 하기 위한 웹 기반 인터페이스를 제공 하기 위해 수행 해야 하는 단계는 여러 가지가 있습니다. 데이터베이스에 직접 저장 되는 이진 데이터, 가능성 경우 이진 데이터가 삽입 되는 경우를 처리 하는 특정 메서드를 추가 합니다. 아키텍처를 업데이트 하려면 필요 합니다. 아키텍처를 업데이트 후 다음 단계는 각 이진 데이터 필드에 대 한 파일 업로드 컨트롤을 사용자 지정한 내용이 DetailsView를 사용 하 여 수행할 수 있는 삽입 인터페이스를 만드는 합니다. 업로드 된 데이터에 웹 서버의 파일 시스템에 저장 하거나 수 DetailsView s에서 데이터 원본 매개 변수 할당 `ItemInserting` 이벤트 처리기입니다.

파일 시스템에 이진 데이터를 저장 데이터를 데이터베이스에 직접 저장 하는 보다 추가 계획이 필요 합니다. 다른 s 덮어쓰지 하나의 s 사용자 업로드를 방지 하기 위해 명명 구성표를 선택 해야 합니다. 또한 데이터베이스 삽입이 실패 하는 경우 업로드 된 파일을 삭제 하려면 추가 단계를 수행 해야 합니다.

했습니다 브로슈어 및 그림을 하지만 사용 하 여 시스템에 새 범주를 추가할 수 있는 기존 범주 s 이진 데이터를 업데이트 하는 방법 또는 올바르게 삭제 된 범주에 대 한 이진 데이터를 제거 하는 방법을 확인 하는 아직 했습니다. 다음 자습서의이 두 항목을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Dave Gardner, Teresa 머피 및 박 광 준 Leigh 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](displaying-binary-data-in-the-data-web-controls-cs.md)
[다음](updating-and-deleting-existing-binary-data-cs.md)
