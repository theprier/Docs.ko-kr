---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: '5 부: 폼 편집 및 템플릿 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 5 부에서는 폼 편집 및 템플릿 설명합니다.
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: acb4a4c427870e375ff19823f0bdfa208438e899
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836003"
---
<a name="part-5-edit-forms-and-templating"></a>5 부: 폼 편집 및 템플릿
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.
> 
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 5 부에서는 폼 편집 및 템플릿 설명합니다.


이전 장에서 된 데이터베이스에서 데이터를 로드 하 고 표시 합니다. 이 챕터에서는 또한 데이터를 편집 지원할 예정입니다.

## <a name="creating-the-storemanagercontroller"></a>StoreManagerController 만들기

라는 새 컨트롤러 만들기부터 시작 합니다 **StoreManagerController**합니다. 이 컨트롤러에 대 한을 받겠습니다 ASP.NET MVC 3 도구 업데이트에서 사용할 수 있는 스 캐 폴딩 기능을 활용 합니다. 아래와 같이 컨트롤러 추가 대화 상자에 대 한 옵션을 설정 합니다.

![](mvc-music-store-part-5/_static/image1.png)

추가 단추를 클릭 하면 ASP.NET MVC 3 스 캐 폴딩 메커니즘을 적절 한 작업을 수행 하는 표시 됩니다.

- Entity Framework 지역 변수를 사용 하 여 새 StoreManagerController 만듭니다.
- 프로젝트의 Views 폴더에 StoreManager 폴더 추가
- Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, 및 Index.cshtml 보기를 강력한 앨범 클래스에 추가

![](mvc-music-store-part-5/_static/image2.png)

StoreManager 컨트롤러 클래스가 새로 포함 CRUD (만들기, 읽기, 업데이트, 삭제) 앨범을 사용 하는 방법을 알고 있는 컨트롤러 작업 모델 클래스 및 데이터베이스 액세스에는 Entity Framework 컨텍스트를 사용 합니다.

## <a name="modifying-a-scaffolded-view"></a>스 캐 폴드 된 뷰를 수정합니다.

이 코드에 우리 회사에 생성 되었습니다.이이 자습서 전체에서 작성 하는 것 처럼 표준 ASP.NET MVC 코드를 기억 하는 것이 반드시 합니다. 상용구 컨트롤러 코드를 작성 하 고 강력한 형식의 뷰를 수동으로 만드는 방법는 데 필요한 시간을 저장 하는 것 하지만 변화 하는 방법에 대 한 주석에서 심각한 경고를 사용 하 여 앞 나타날가 생성 된 코드의 종류를 코드입니다. 코드 이며 변경 해야 합니다.

따라서 StoreManager 인덱스 뷰에 빠른 편집을 사용 하 여 시작 해 보겠습니다 (/ Views/StoreManager/Index.cshtml). 이 보기에는 편집을 사용 하 여 스토어에서 앨범을 나열 하는 테이블 표시 됩니다 / 세부 정보 / 링크를 삭제 하 고 앨범의 공용 속성을 포함 합니다. 이 표시에서는 유용 하지 않으므로 AlbumArtUrl 필드를 제거 하겠습니다. &lt;테이블&gt; 섹션의 코드 보기를 제거 합니다 &lt;번째&gt; 및 &lt;td&gt; 아래 강조 표시 된 줄에 표시 된 대로 AlbumArtUrl 참조, 주변 요소:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

코드 수정 된 보기는 다음과 같이 표시 됩니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>저장소 관리자 소개

이제 응용 프로그램을 실행 하 고 StoreManager은 /로 이동 합니다. 방금 수정한, 세부 정보를 편집 및 삭제에 대 한 링크를 사용 하 여 저장소에는 앨범의 목록을 보여 주는 저장 Manager 인덱스 표시 됩니다.

![](mvc-music-store-part-5/_static/image3.png)

편집 링크를 클릭 하면 앨범, Genre 및 아티스트에 대 한 드롭다운을 포함 하 여 필드를 사용 하 여 편집 양식을 표시 됩니다.

![](mvc-music-store-part-5/_static/image4.png)

아래쪽에서 "목록으로 돌아가기" 링크를 클릭 하 고 앨범에 대 한 세부 정보 링크를 클릭 합니다. 그러면 개별 앨범에 대 한 세부 정보가 표시 됩니다.

![](mvc-music-store-part-5/_static/image5.png)

마찬가지로 목록 링크를 다시 클릭 삭제 링크를 클릭 합니다. 앨범 세부 정보를 표시 하 고 삭제 하려고 하는지 우리가 하는 경우 요청을 확인 대화 상자에서 표시 됩니다.

![](mvc-music-store-part-5/_static/image6.png)

맨 아래에서 삭제 단추를 클릭 하면 앨범은 삭제 되며 삭제 앨범을 보여 주는 인덱스 페이지로 돌아갑니다.

저장소 관리자를 사용 하 여 완료 되지 있지만 컨트롤러 및 보기 코드부터 CRUD 작업에 대 한 작업을 했습니다.

## <a name="looking-at-the-store-manager-controller-code"></a>저장소 관리자 컨트롤러 코드를 살펴보면

저장소 관리자 컨트롤러가 적절 한 코드를 포함합니다. 살펴보겠습니다이 위쪽에서에서 아래쪽입니다. 컨트롤러는 MVC 컨트롤러 뿐만 아니라 모델 네임 스페이스에 대 한 참조에 대 한 몇 가지 표준 네임 스페이스를 포함합니다. 컨트롤러에 MusicStoreEntities, 데이터 액세스를 위해 각 컨트롤러 작업에서 사용의 전용 인스턴스

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>작업 관리자 인덱스 및 세부 정보를 저장 합니다.

인덱스 보기에는 저장소 찾아보기 메서드에서 작업할 때 이전에 설명한 것 처럼 각 앨범 참조 장르 및 음악가 정보를 포함 한 앨범의 목록을 검색 합니다. 인덱스 보기 컨트롤러는 효율적이 고 원래 요청에서이 정보에 대 한 쿼리 중인 하므로 각 앨범 장르 이름 및 Artist 이름을 표시할 수 있습니다이 연결된 된 개체에 대 한 참조를 다음 됩니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager 컨트롤러의 세부 정보 컨트롤러 작업 정확히 동일 하 게 작동 우리가 작성 한 이전에-앨범에 대 한 쿼리 저장소 컨트롤러 세부 정보 작업 find () 메서드를 사용 하는 ID를 기준으로 다음이 보기로 돌아갑니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>작업 메서드 만들기

만들기 작업 메서드는 양식 입력을 처리 하기 때문에 지금까지 살펴본 것과 약간 다릅니다. 사용자가 먼저 방문 /StoreManager/만들기/빈 폼을 표시 되며 합니다. 이 HTML 페이지에 포함 됩니다는 &lt;폼&gt; 드롭다운 및 텍스트를 포함 하는 요소는 앨범의 세부 정보를 입력할 수 있는 요소를 입력 합니다.

앨범 폼 값에 입력을 한 후에 데이터베이스 내에 저장할 응용 프로그램에 이러한 변경 내용을 다시 제출 하려면 "저장" 단추를 눌러 수 있습니다. "저장" 단추를 누를 때 합니다 &lt;폼&gt; /StoreManager/만들기/URL로 다시 HTTP POST를 수행 하 고 제출 됩니다 합니다 &lt;폼&gt; HTTP POST의 일부로 값입니다.

ASP.NET MVC를 사용 하면 이러한 두 URL 호출 시나리오의 논리는 /StoreManager/Create 초기 HTTP GET 탐색을 처리 하는 StoreManagerController 클래스 – 내에서 두 개의 별도 "만들기" 작업 메서드를 구현 하도록 함으로써 쉽게 분할할 수 / URL 및 다른 전송된 된 변경 내용이의 HTTP POST를 처리 하도록 합니다.

### <a name="passing-information-to-a-view-using-viewbag"></a>ViewBag을 사용 하 여 보기에 정보 전달

이 자습서의 앞부분에서 ViewBag을 사용한 하지만 해에 대 한 별로 설명 하지 않았습니다. ViewBag을 사용 하면 강력한 형식의 모델 개체를 사용 하지 않고 보기에 정보를 전달할 수 있습니다. 이 경우이 편집 HTTP-GET 컨트롤러 작업 두 목록을 전달 장르 및 아티스트가를 폼에 드롭다운을 채우는 하며 작업을 수행 하는 가장 간단한 방법은 ViewBag 항목으로 반환 하는 것입니다.

ViewBag는 동적 개체를 해당 속성을 정의 하는 코드를 작성 하지 않고도 ViewBag.Foo 또는 ViewBag.YourNameHere는 입력할 수 있습니다. 이 경우 컨트롤러 코드 사용 ViewBag.GenreId 및 ViewBag.ArtistId GenreId 및 ArtistId, 설정 수는 앨범 속성 폼을 제출 하는 드롭다운 값 수 있도록 합니다.

이러한 드롭다운 값 위에 빌드되는 용도 위해 SelectList 개체를 사용 하 여 폼에 반환 됩니다. 이것은 다음과 같은 코드를 사용 하 여:

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

작업 메서드 코드에서 보듯이이 개체를 만들 세 개의 매개 변수를 사용 중인 됩니다.

- 드롭다운을 표시할 수는 항목의 목록입니다. Note는 문자열일 뿐 이것이-장르 목록을 전달 합니다.
- 다음 매개 변수는 SelectList에 전달 되 고 선택한 값입니다. 이 SelectList 미리 목록의 항목을 선택 하는 방법을 인식 하는 방법입니다. 이 매우 비슷하지만 편집 양식의 보면 이해 하기 쉬운 됩니다.
- 마지막 매개 변수는 표시할 수 속성입니다. 이 경우 사용자에 게 표시 됩니다 Genre.Name 속성 임을 나타내는이 합니다.

이 점을 염두에서 그런 다음 HTTP-GET 만들기 작업은 매우 간단-두 SelectLists ViewBag을에 추가 되 고 모델 개체가 없습니다 전달 됩니다 폼 (아직 생성 되지 않은) 때문.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>삭제 목록 보기 만들기 표시할 HTML 도우미

드롭다운 값 목록 보기에 전달 하는 방법을 소개한에 있으므로 해당 값이 표시 되는 방식을 확인 하려면 뷰를 빠르게 확인을 살펴보겠습니다. 코드 보기에서에서 (/ Views/StoreManager/Create.cshtml), 장르 드롭다운을 표시 하도록 다음 호출을 보면 다운 합니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

이 HTML 도우미-일반적인 보기 작업을 수행 하는 유틸리티 메서드 이라고 합니다. HTML 도우미 간결 하 고 읽을 수 있는 뷰 코드 유지에 매우 유용 합니다. Html.DropDownList 도우미 ASP.NET MVC에서 제공 하는 이지만 나중으로 코드 보기에서는 응용 프로그램에서 다시 사용에 대 한 고유한 도우미를 만들 수 있습니다.

위치를 표시할 목록 가져오기 및 값 (있는 경우)는 미리 선택 해야 합니다. 두 가지-누르세요 Html.DropDownList 호출 해야 합니다. 첫 번째 매개 변수, GenreId 모델 또는 ViewBag GenreId 라는 값을 검색할 DropDownList를 알려 줍니다. 두 번째 매개 변수는 표시할 값을 나타내는 드롭다운 목록에서에서 선택한 처음으로 사용 됩니다. 이 폼 만들기 양식을 이므로 값이 없는 미리 선택 된 되도록 하 고 String.Empty 전달 됩니다.

### <a name="handling-the-posted-form-values"></a>게시 된 양식 값 처리

전에 설명한 대로 각 폼에 연결 된 두 개의 작업 메서드 있습니다. 첫 번째는 HTTP GET 요청을 처리 하 고 폼을 표시 합니다. 제출 된 양식 값을 포함 하는 HTTP POST 요청을 처리 하는 두 번째입니다. 컨트롤러 작업에 HTTP POST 요청에만 응답 해야 ASP.NET MVC에 지시 하는 [HttpPost] 특성을 확인할 수 있습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

이 작업에는 네 가지 책임에 있습니다.

- 1. 폼 값 읽기
- 2. 폼 값 유효성 검사 규칙을 전달 하는 경우 확인
- 3. 폼 제출을 유효한 경우 데이터를 저장 하 고 업데이트 된 목록을 표시 합니다.
- 4. 폼 제출을 올바르지 않으면 유효성 검사 오류가 있는 양식을 다시 표시

#### <a name="reading-form-values-with-model-binding"></a>모델 바인딩 사용 하 여 폼 값 읽기

컨트롤러 작업 제목, 가격 및 AlbumArtUrl GenreId 및 ArtistId (드롭다운 목록에서 목록) 값 및 텍스트 상자 값을 포함 하는 폼 제출을 처리 하 고 있습니다. 폼 값에 직접 액세스할 수 있지만, ASP.NET MVC에 기본 제공 모델 바인딩 기능을 사용 하는 것이 좋습니다. 매개 변수로 모델 형식을 사용 하는 컨트롤러 작업을 하는 경우 ASP.NET MVC 양식 입력 (뿐만 아니라 경로 및 쿼리 문자열 값)를 사용 하 여 해당 형식의 개체를 채우는 하려고 합니다. 즉, 이름이 모델 개체의 속성을 예를 들어 일치 하는 값에 대 한 확인 하 여 새 앨범 개체 GenreId 값을 설정할 때 찾습니다 GenreId 이름의 입력 합니다. 표준 메서드를 사용 하 여 ASP.NET MVC에서 뷰를 만들 때 폼 항상 렌더링 됩니다이 필드 이름과 일치 하도록 속성 이름 입력된 필드 이름으로 사용 합니다.

#### <a name="validating-the-model"></a>모델 유효성 검사

모델은 ModelState.IsValid에 대 한 간단한 호출을 사용 하 여 유효성이 검사 됩니다. 앨범 클래스에 유효성 검사 규칙을 추가 하지 않은 것 아직이 검사 관련이 없는에 대해서는 조금-그럼 하겠습니다. 중요 한 점은이 ModelStat.IsValid 확인 유효성 검사 규칙에 대 한 후속 변경 컨트롤러 작업 코드에 대 한 업데이트가 필요 하지 않습니다, 모델에 입력 유효성 검사 규칙에 따라 조정 됩니다는입니다.

#### <a name="saving-the-submitted-values"></a>제출 된 값을 저장합니다.

폼 제출을 유효성 검사를 통과 인지 시간 값을 데이터베이스에 저장 합니다. 앨범 컬렉션에 모델을 추가 하 고 SaveChanges를 호출 해 서 연결 해야 하는 Entity Framework를 사용 하 여

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework에는 값을 유지 하려면 적절 한 SQL 명령을 생성 합니다. 데이터를 저장 한 후 우리 컴퓨터에서는 업데이트를 알 수 있도록 앨범의 목록으로 다시 리디렉션합니다. 이렇게 RedirectToAction 표시 하고자 컨트롤러 작업의 이름으로 반환 합니다. 이 경우에 경우 Index 메서드

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>잘못 된 양식 제출 유효성 검사 오류를 표시합니다.

잘못 된 양식 입력의 경우 드롭다운 값 (HTTP GET 예:) ViewBag에 추가 됩니다 하 고 바인딩된 모델 값 표시에 대 한 보기로 다시 전달 됩니다. 유효성 검사 오류를 사용 하 여 자동으로 표시 되는 @Html.ValidationMessageFor HTML 도우미입니다.

#### <a name="testing-the-create-form"></a>테스트 폼 만들기

이 out, 실행 및 테스트에 응용 프로그램 이동 /StoreManager/만들기 /-이 표시 됩니다 StoreController 만드는 HTTP GET 메서드에 의해 반환 된 빈 양식.

일부 값 입력 하 고 양식을 전송할 만들기 단추를 클릭 합니다.

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>편집 내용을 처리합니다.

방금 살펴본 만들기 작업 방법에 편집 작업 쌍 (HTTP-GET 및 HTTP-POST) 매우 비슷합니다. 편집 시나리오에서는 기존 앨범, 편집 HTTP-GET 메서드 로드 앨범 "id" 매개 변수를 기반으로 사용 하므로 경로 통해 전달 합니다. 이 코드 앨범 AlbumId 검색 하는 것에 대 한 이전에 살펴보았습니다 세부 정보 컨트롤러 작업에서와 같습니다. 만들기와 마찬가지로 HTTP GET 메서드 값 드롭다운 ViewBag을 통해 반환 됩니다. 이렇게 하면 돌아가려면 앨범은 모델 개체를 뷰 (Album 클래스에 강력한 형식인) ViewBag을 통해 추가 데이터 (예: 장르 목록)을 전달 하는 동안.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

HTTP POST 편집 작업을 만드는 HTTP POST 작업을 매우 비슷합니다. 유일한 차이점은는 db에 새 앨범이 추가 하는 대신 합니다. 앨범 컬렉션에서는 찾는 앨범의 현재 인스턴스 db를 사용 하 여 합니다. Entry(album) 및 해당 상태를 Modified로 설정 합니다. 새로 만드는 대신 기존 앨범 수정 엔터티 프레임 워크에 지시 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

이 응용 프로그램을 실행 하 고 이동/StoreManger/앨범에 대 한 편집 링크를 클릭 하 여 테스트할 수 있습니다.

![](mvc-music-store-part-5/_static/image9.png)

HTTP GET 편집 메서드에 의해 표시 된 편집 양식을 표시 됩니다. 일부 값 입력 하 고 저장 단추를 클릭 합니다.

![](mvc-music-store-part-5/_static/image10.png)

이 폼 게시, 값을 저장 및 앨범 목록에 표시 된 값이 업데이트 되었습니다 us를 반환 합니다.

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>삭제를 처리합니다.

삭제는 편집 및 만들기, 확인을 표시 하려면 하나의 컨트롤러 작업과 폼 제출을 처리 하는 다른 컨트롤러 작업을 사용 하 여 동일한 패턴을 따릅니다.

컨트롤러 HTTP-GET 삭제 작업에서는 이전 저장소 관리자 세부 정보 컨트롤러 작업으로 정확히 같습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

삭제 뷰 콘텐츠 템플릿을 사용 하 여 앨범 형식에 강력한 형식이 있는 양식이 표시 됩니다.

![](mvc-music-store-part-5/_static/image12.png)

Delete 템플릿 모델에 대 한 모든 필드를 보여주지만, 해당 하위 상당히 간소화할 수 있습니다. 다음과 /Views/StoreManager/Delete.cshtml에서 코드 보기를 변경 합니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

간소화 된 삭제 확인 메시지가 표시 됩니다.

![](mvc-music-store-part-5/_static/image13.png)

삭제 단추를 클릭 하면 폼이 DeleteConfirmed 동작을 실행 하는 서버에 다시 게시 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

다음 작업을 수행 하는 우리의 HTTP-POST 삭제 컨트롤러 작업:

- 1. ID 별로 앨범 로드
- 2. 앨범을 삭제 하 고 변경 내용을 저장
- 3. 앨범이 목록에서 제거 되었는지 보여 주는 인덱스에 리디렉션

이 테스트 하려면 응용 프로그램을 실행 하 고 /StoreManager 찾습니다. 목록에서 앨범을 선택 하 고 삭제 링크를 클릭 합니다.

![](mvc-music-store-part-5/_static/image14.png)

이 삭제 확인 화면이 표시 됩니다.

![](mvc-music-store-part-5/_static/image15.png)

삭제 단추를 클릭 하면 앨범을 제거 하 고 앨범 삭제 된 것을 보여 주는 Store Manager 인덱스 페이지로 돌아옵니다.

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>사용자 지정 HTML 도우미를 사용 하 여 텍스트를 잘라내려면

저장소 관리자 인덱스 페이지를 사용 하 여 잠재적인 문제 하나 밀집 되어 있습니다. Artist 이름과 앨범 제목 속성 수 둘 다 충분히 길게 우리의 표 서식을 해제 throw 할 수는 있습니다. 이 보기에서 여러 속성을 쉽게 자를 해도 된다고 허락 하는 사용자 지정 HTML 도우미를 만들어 보겠습니다.

![](mvc-music-store-part-5/_static/image17.png)

Razor의 @helper 구문에 매우 쉽게 해 주었다 보기에서 사용할 사용자 고유의 도우미 함수를 만들 수 있습니다. /Views/StoreManager/Index.cshtml 뷰를 연 후 바로 다음 코드를 추가 합니다 @model 줄.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

이 도우미 메서드는 문자열과 수 있도록 최대 길이 사용 합니다. 도우미 출력으로 제공 된 텍스트를 지정 된 길이 보다 짧은 경우-됩니다. 긴 경우 다음 텍스트를 잘라냅니다 하 고 나머지 부분에서는 "..."를 렌더링 합니다.

이제 앨범 제목 및 Artist 이름 속성이 모두 25 자 미만 되는지 확인 하는 잘라내기 도우미를 사용할 수 있습니다. 이 새 자르기 도우미를 사용 하 여 전체적인 코드를 아래에 나타납니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

이제 /StoreManager/ URL를 살펴봅니다 albums 및 제목 아래 최대 길이 유지 됩니다.

![](mvc-music-store-part-5/_static/image18.png)

참고: 만들고 도우미를 사용 하 여 10to8의 간단한 경우가 표시 됩니다. 사이트 전체에서 사용할 수 있는 도우미 만들기에 대 한 자세한 내용은 필자의 블로그 게시물을 참조 하세요. [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-4.md)
> [다음](mvc-music-store-part-6.md)
