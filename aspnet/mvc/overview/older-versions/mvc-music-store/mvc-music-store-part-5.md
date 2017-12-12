---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: "5 단계: 편집 양식 및 템플릿 | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 편집 양식 및 템플릿 5 부에 설명합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: cde6fe133291254531a797a434a4b2cdd226dd5f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-5-edit-forms-and-templating"></a>5 단계: 편집 양식 및 템플릿
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.
> 
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 편집 양식 및 템플릿 5 부에 설명합니다.


지난 장에서는 된 데이터베이스에서 데이터를 로드 하 고 표시 합니다. 이 장에서 활성화 하는 데이터를 편집 합니다.

## <a name="creating-the-storemanagercontroller"></a>StoreManagerController 만들기

라는 새 컨트롤러를 만들어 먼저 **StoreManagerController**합니다. 이 컨트롤러에 대 한 받겠습니다 ASP.NET MVC 3 도구 업데이트에서 사용할 수 있는 스 캐 폴딩 기능을 활용 합니다. 아래 표시 된 것과 같이 컨트롤러 추가 대화 상자에 대 한 옵션을 설정 합니다.

![](mvc-music-store-part-5/_static/image1.png)

추가 단추를 클릭할 때 ASP.NET MVC 3 스 캐 폴딩 메커니즘은을 좋은 양의 작업을 수행 하는 있는지 표시 됩니다.

- Entity Framework 지역 변수와 함께 새 StoreManagerController 만듭니다.
- StoreManager 폴더는 프로젝트의 Views 폴더를 추가합니다.
- 앨범 클래스에 강력한 형식의 Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, 및 Index.cshtml 뷰 추가

![](mvc-music-store-part-5/_static/image2.png)

새 StoreManager 컨트롤러 클래스 포함 CRUD (만들기, 읽기, 업데이트, 삭제) 앨범을 사용 하는 방법을 알고 있는 컨트롤러 작업 모델 클래스 및 데이터베이스 액세스를 위한 우리의 Entity Framework 컨텍스트를 사용 합니다.

## <a name="modifying-a-scaffolded-view"></a>스 캐 폴드 보기 수정

해이 코드를 생성 하는 동안는이 자습서 전체에서 작성 된 한 것 처럼 표준 ASP.NET MVC 코드를 기억 하는 것이 유용 합니다. 상용구 컨트롤러 코드를 작성 하 고 강력한 형식의 뷰를 수동으로 만드는 지출 시간을 저장 하기 위한 것에 있지만이 값은 앞에 변경 되어서는 방법에 대 한 주석에서 다이어 경고와 함께 표시 됩니다 생성 된 코드의 종류는 코드입니다. 이 코드를 이므로 변경 해야 합니다.

따라서 StoreManager 인덱스 뷰를 빠르게 편집할부터 시작 하겠습니다 (/ Views/StoreManager/Index.cshtml). 이 보기 편집 저장소에서 앨범을 나열 하는 테이블에 표시 됩니다 / 자세히 설명 / 링크를 삭제 하 고는 앨범의 공용 속성을 포함 합니다. AlbumArtUrl 필드가이 디스플레이의 매우 유용 하지 않으므로 제거 하겠습니다. &lt;테이블&gt; 섹션 코드 보기의 제거는 &lt;번째&gt; 및 &lt;td&gt; 아래의 강조 표시 된 줄에 표시 된 대로 AlbumArtUrl 참조를 둘러싼 요소:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

뷰 수정 된 코드는 다음과 같이 표시 됩니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>저장소 관리자 소개

이제 응용 프로그램을 실행 하 고/StoreManager/로 이동 합니다. 방금 수정한, 세부 정보를 편집 및 삭제에 대 한 링크를 사용 하 여 저장소에는 앨범의 목록을 보여 주는 저장 Manager 인덱스 표시 됩니다.

![](mvc-music-store-part-5/_static/image3.png)

편집 링크를 클릭 하면 Genre 및 아티스트에 대 한 드롭다운 목록을 포함 하 여 앨범에 대 한 필드를 사용 하 여 편집 폼이 표시 됩니다.

![](mvc-music-store-part-5/_static/image4.png)

아래에 다시 "목록에" 링크를 클릭 한 다음 앨범에 대 한 세부 정보 링크를 클릭 합니다. 이 개별 앨범에 대 한 세부 정보를 표시 합니다.

![](mvc-music-store-part-5/_static/image5.png)

뒤로 목록 링크를 클릭 하 여 다시 삭제 링크를 클릭 합니다. 확인 대화 상자, 앨범 세부 정보를 표시 하 고 삭제 하려는 있는지 되었는지 묻는 표시 합니다.

![](mvc-music-store-part-5/_static/image6.png)

맨 아래에 삭제 단추를 클릭 하는 앨범을 삭제 하 고 삭제 앨범 표시 인덱스 페이지로 돌아올 수 있습니다.

저장소 관리자를 사용 하 여 완료 하지 했지만 컨트롤러와 코드에서 시작 하도록 CRUD 작업에 대 한 보기 작업.

## <a name="looking-at-the-store-manager-controller-code"></a>저장소 관리자 컨트롤러가 코드 보기

저장소 관리자 컨트롤러가 좋은 양의 코드가 포함 되어 있습니다. 살펴보겠습니다이 위쪽에서 아래쪽으로. 컨트롤러는 MVC 컨트롤러 뿐만 아니라이 모델 네임 스페이스에 대 한 참조에 대 한 몇 가지 표준 네임 스페이스를 포함합니다. 컨트롤러에 데이터 액세스를 위해 각 컨트롤러 작업에서 사용 MusicStoreEntities의 private 인스턴스에 있습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>작업 관리자 인덱스 및 세부 정보를 저장 합니다.

인덱스 뷰 저장소 검색 방법에 대해 작업할 때 이전에 설명한 것 처럼 각 앨범 참조 Genre 및 음악가 정보를 포함 한 앨범 목록을 검색 합니다. 인덱스 뷰 표시 하려면 각 앨범 장르 이름과 아티스트 이름을 효율적이 고 원래 요청에이 정보에 대 한 쿼리는 컨트롤러 되 고 있으므로 있도록 연결 된 개체에 대 한 참조 팔 로우.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager 컨트롤러의 세부 정보 컨트롤러 작업 안내 드린 바 이전에-앨범에 대 한 쿼리 저장소 컨트롤러 상세 작업 동일 하 게 작동 find () 메서드를 사용 하는 id로 반환 하는 예제 보기에 있습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>작업 메서드 만들기

만들기 작업 메서드는 폼 입력을 처리 하기 때문에 지금까지 살펴본는 스토리는 약간 다릅니다. 사용자가 처음 방문 /StoreManager/만들기/은 빈 폼을 표시 됩니다. 이 HTML 페이지에 포함 됩니다는 &lt;양식&gt; 드롭다운 및 텍스트 상자를 포함 하는 요소는 앨범의 세부 정보를 입력할 수 있는 요소를 입력 합니다.

앨범 폼 값에 입력을 한 후에 데이터베이스 내에 저장할 응용 프로그램에 이러한 변경 내용을 다시 제출 하려면 [저장] 단추를 눌러 수 있습니다. "저장" 단추를 누를 때는 &lt;양식&gt; /StoreManager/만들기/URL로 다시 HTTP POST를 수행 하 고 제출는 &lt;양식&gt; HTTP POST의 일부로 값입니다.

ASP.NET MVC를 초기 HTTP GET 찾아보기는 /StoreManager/Create를 처리 하도록 하나 StoreManagerController 클래스-내에서 두 개의 별도 "만들기" 작업 메서드를 구현 하도록 함으로써 이러한 두 가지 URL 호출 시나리오의 논리를 쉽게 분할할 수 있습니다. / URL 및 다른 전송된 된 변경 내용이의 HTTP POST를 처리 하도록 합니다.

### <a name="passing-information-to-a-view-using-viewbag"></a>ViewBag을 사용 하 여 보기에 정보를 전달 합니다.

म ViewBag이이 자습서의 앞부분에서 사용한 하지만 많은 항목에 대 한 설명이 하지 않았습니다. ViewBag 보기에는 강력한 형식의 모델 개체를 사용 하지 않고 정보를 전달할 수 있도록 합니다. 이 경우 우리의 편집 HTTP-GET 컨트롤러 동작을 폼에는 드롭다운 목록 채우기 장르와 예술가 목록과 전달 해야 합니다. 되며 작업을 수행 하는 가장 간단한 방법은 ViewBag 항목으로 돌아갑니다.

ViewBag는 동적 개체를 이러한 속성을 정의 하는 코드를 작성 하지 않고도 ViewBag.Foo 또는 ViewBag.YourNameHere을 입력할 수 있습니다. 이 경우에 컨트롤러 코드 사용 하 여 ViewBag.GenreId ViewBag.ArtistId 하에서 폼을 제출 하는 드롭다운 값 GenreId 및 ArtistId, 앨범 속성은 설정 됩니다.

이러한 드롭다운 값 용도 위해 빌드되는 SelectList 개체를 사용 하 여 폼에 반환 됩니다. 이 작업은 수행 다음과 같은 코드를 사용 하 여:

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

이 개체를 만들에 세 개의 매개 변수가 사용 되는 작업 메서드 코드 알 수 있듯이:

- 드롭다운을 나타내려면 항목의 목록. 이 값은 문자열로-장르 목록을 전달할 것임 note 합니다.
- SelectList에 전달 되 고 다음 매개 변수는 선택 값. 이 SelectList 미리 목록에서 항목을 선택 하는 방법을 인식 하는 방법입니다. 이 상당히 비슷한 편집 폼에 살펴보기 하면 쉽게 이해할 수 됩니다.
- 마지막 매개 변수는 속성을 표시 합니다. 이 경우이을 나타내는 Genre.Name 속성 사용자에 게 표시 됩니다.

이 점을 염두에서 그런 다음 HTTP GET 만들기 동작 아주 간단-두 SelectLists ViewBag에 추가 됩니다를 (아직 생성 되지 않은) 때문에 폼에 모델 개체가 전달 됩니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>Drop 다운 Create View에서 표시 하는 HTML 도우미

드롭다운 값 목록 보기에 전달 하는 방식에 대 한 여태 이후 해당 값이 표시 되는 방법을 확인 하려면 뷰를 빠르게 확인을 보겠습니다. 코드 보기에서에서 (/ Views/StoreManager/Create.cshtml), 다음 호출에서는 장르 3 표시 다운 합니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

이 HTML 도우미-공용 보기 작업을 수행 하는 유틸리티 메서드 라고 합니다. HTML 도우미는 간결 하 고 읽을 수 있는 보기 코드를 유지 하는 데 매우 유용 합니다. Html.DropDownList 도우미 ASP.NET MVC에서 제공 되지만 응용 프로그램에서 다시 사용 됩니다 म 코드 보기에 대 한 고유한 도우미를 만들 수는 나중에 볼 수 있겠지만 합니다.

방금 Html.DropDownList 호출이 필요 하다는 메시지가 두 가지-get를 표시 하려면 목록 및 값 (있는 경우)는 미리 선택 되어 있어야 합니다. 수 있는 위치 해야 합니다. 첫 번째 매개 변수 GenreId, 모델 또는 ViewBag GenreId 라는 값을 찾으려는 DropDownList 지시 합니다. 두 번째 매개 변수 드롭다운 목록에서에서 선택한 처음으로 표시 하려면 값을 나타내는 데 사용 됩니다. 이 폼은 폼 만들기, 이후 되도록 미리 선택 된 값이 없는 이며 String.Empty 전달 됩니다.

### <a name="handling-the-posted-form-values"></a>폼 게시 값 처리

하기 전에 설명한 것 처럼 각 폼과 연결 된 두 가지 동작 메서드가 있습니다. 첫 번째 HTTP GET 요청을 처리 하 고 폼을 표시 합니다. 제출 된 양식 값을 포함 하는 HTTP POST 요청을 처리 하는 두 번째입니다. 컨트롤러 작업에 HTTP POST 요청에만 응답 해야 ASP.NET MVC를 알려 주는 [HttpPost] 특성이 있는지 확인 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

이 작업에는 4 개의 책임에 있습니다.

- 1. 폼 값 읽기
- 2. 폼 값 모든 유효성 검사 규칙을 통과 하는 경우 확인
- 3. 양식 전송이 유효한 경우 데이터를 저장 하 고 업데이트 된 목록을 표시 합니다.
- 4. 양식 전송 유효 하지 않을 경우 유효성 검사 오류가 있는 폼을 다시 표시

#### <a name="reading-form-values-with-model-binding"></a>모델 바인딩 폼 값 읽기

컨트롤러 작업 제목, 가격 및 AlbumArtUrl 용 GenreId 및 ArtistId (에서 드롭 다운 목록) 값 및 textbox 값이 포함 된 양식을 제출 하 여 처리 하 고 있습니다. 폼 값에 직접 액세스할 수 있지만 ASP.NET MVC에 기본 제공 되는 모델 바인딩 기능을 사용 하는 것이 좋습니다. 컨트롤러 작업 모델 형식을 매개 변수로 수행할 때는 ASP.NET MVC는 폼 입력 (뿐만 아니라 경로 및 쿼리 문자열 값)를 사용 하 여 해당 형식의 개체를 채우는 하려고 합니다. 이렇게 하기 이름이 예: 모델 개체의 속성을 일치 하는 값을 검색 하 여 새 앨범 개체 GenreId 값을 설정할 때 찾습니다 GenreId 이름의 입력 합니다. ASP.NET MVC의 표준 메서드를 사용 하 여 뷰를 만들 때 양식 항상 렌더링 됩니다 하므로이 필드 이름이 됩니다 방금 일치 속성 이름 입력된 필드 이름으로 사용 합니다.

#### <a name="validating-the-model"></a>모델 유효성 검사

모델을 ModelState.IsValid 간단한 호출 하 여 유효성을 검사 합니다. 에서는 앨범 클래스에 유효성 검사 규칙을 추가 하지는 않았지만 아직-이 검사를 확실히 없는 약간-하므로 지금 수행 합니다. 중요 한 것은이 ModelStat.IsValid 검사 나중에 변경 내용 유효성 검사 규칙에 컨트롤러 작업 코드에 대 한 업데이트를 필요로 하므로 예제의 모델에 입력 유효성 검사 규칙에 적용 됩니다.

#### <a name="saving-the-submitted-values"></a>전송 된 값을 저장합니다.

양식 전송이 유효성 검사를 통과 경우 데이터베이스에 값을 저장 하는 시간입니다. 앨범 컬렉션에 모델을 추가 하 고 SaveChanges를 호출 해 서 연결 해야 하는 Entity Framework와 함께

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework에는 값을 유지 하려면 적절 한 SQL 명령을 생성 합니다. 데이터를 저장 한 후에서는 컴퓨터의 업데이트를 알 수 있도록 앨범 목록으로 다시 리디렉션합니다. 이 RedirectToAction 원하는 표시 된 컨트롤러 동작의 이름으로 반환 하 여 수행 됩니다. 이 경우 인덱스 메서드입니다.

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>유효성 검사 오류가 있는 잘못 된 양식 제출 표시

잘못 된 양식 입력의 경우 드롭다운 값 (예: HTTP GET 경우) ViewBag에 추가 됩니다 및 바인딩된 모델 값 표시에 보기로 다시 전달 됩니다. 유효성 검사 오류를 사용 하 여 자동으로 표시 됩니다는 @Html.ValidationMessageFor HTML 도우미입니다.

#### <a name="testing-the-create-form"></a>테스트 폼 만들기

이 실행 아웃 응용 프로그램 및 찾아보기 /StoreManager/만들기 /-를 테스트 하려면이 안내해 StoreController 만들 HTTP GET 메서드에 의해 반환 된 되는 빈 형식.

값의 일부에 채운에서는 양식을 전송할 만들기 단추를 클릭 합니다.

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>편집 내용을 처리합니다.

편집 작업 쌍 (HTTP GET 및 HTTP POST) 작업 메서드 만들기 앞서 설명한 매우 비슷합니다. 편집 시나리오에서는 작업에는 편집 HTTP GET 메서드 로드 "id" 매개 변수에 따라 앨범 기존 앨범 이후 경로 통해 전달 합니다. 이 코드 앨범 AlbumId 검색 하기 위한 이전에 알아보았습니다 상세 컨트롤러 작업에서와 같습니다. 만들기와 마찬가지로 / HTTP GET 메서드가 값 드롭다운 ViewBag를 통해 반환 됩니다. 이 통해 돌아가려면 앨범 우리의 모델 개체와 뷰의 (앨범 클래스에 강력한 형식이) ViewBag을 통해 추가 데이터 (예: 장르 목록)을 전달 하는 동안 있습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

HTTP POST 편집 동작은 만들기 HTTP POST 작업에 매우 유사 합니다. 유일한 차이점은 db 새 앨범이 추가 하는 대신 합니다. 앨범 컬렉션에서는 찾는 앨범의 현재 인스턴스 db를 사용 하 여 합니다. Entry(album) 및 상태 수정한 날짜를 설정 합니다. 새로 만드는 대신 기존 앨범 수정 하는 것 엔터티 프레임 워크에 지시 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

응용 프로그램을 실행 하 고/StoreManger/를 찾아 다음 앨범에 대 한 편집 링크를 클릭 하 여이를 테스트할 수 있습니다.

![](mvc-music-store-part-5/_static/image9.png)

이 편집 HTTP GET 메서드에 의해 표시 된 편집 폼을 표시 합니다. 값의 일부에 채운 저장 단추를 클릭 합니다.

![](mvc-music-store-part-5/_static/image10.png)

이 폼 게시, 값을 저장 하 고 값이 업데이트 되었음을 보여 주는 앨범 목록에 us를 반환 합니다.

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>삭제를 처리합니다.

삭제 편집 하며 만들기, 양식 전송 처리 하도록 다른 컨트롤러 작업 확인 폼을 표시 한 컨트롤러 작업 사용 하 여 동일한 패턴을 따릅니다.

HTTP GET 삭제 컨트롤러 작업 우리의 이전 저장소 관리자 정보 컨트롤러 작업와 정확히 같습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

삭제 뷰 콘텐츠 템플릿을 사용 하 여 앨범 형식에 강력한 형식이 있는 양식이 표시 됩니다.

![](mvc-music-store-part-5/_static/image12.png)

Delete 서식 파일은 모델에 대 한 모든 필드를 표시 하지만 해당 다운 많이 간소화할 수 있습니다. 다음과 /Views/StoreManager/Delete.cshtml에서 코드 보기를 변경 합니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

간소화 된 삭제 확인을 표시 됩니다.

![](mvc-music-store-part-5/_static/image13.png)

삭제 단추를 클릭 하면 DeleteConfirmed 동작을 실행 하는 서버에 다시 게시할 폼입니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

다음 동작을 수행 하는 당사의 HTTP POST 삭제 컨트롤러 작업.

- 1. ID 별로 앨범 로드
- 2. 앨범 삭제 되 고 변경 내용 저장
- 3. 앨범 목록에서 제거 된 보여 주는 인덱스에 리디렉션

이 르 테스트 하려면 응용 프로그램을 실행 하 고 /StoreManager 찾습니다. 목록에서 앨범을 선택 하 고 삭제 링크를 클릭 합니다.

![](mvc-music-store-part-5/_static/image14.png)

우리의 삭제 확인 화면이 표시 됩니다.

![](mvc-music-store-part-5/_static/image15.png)

삭제 단추를 클릭 하면 앨범을 제거 하 고 앨범 삭제 했을 보여 주는 저장소 관리자 인덱스 페이지에 us를 반환 합니다.

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>사용자 지정 HTML 도우미를 사용 하 여 텍스트를 잘라내려면

저장소 관리자 인덱스 페이지와 하나 이상의 잠재적인 문제가 접수 했습니다. 우리의 앨범 제목 및 아티스트 Name 속성 수 모두 충분히 길게 우리의 표 서식을 오프 throw 할 수 있습니다. 이 보기에 여러 속성을 쉽게 자를 수 있도록 허용 하려면 사용자 지정 HTML 도우미를 만들어 보겠습니다.

![](mvc-music-store-part-5/_static/image17.png)

Razor의 @helper 구문 되었습니다 상당히 쉽게 보기에 사용 하기 위해 도우미 함수를 직접 만들 수 있습니다. /Views/StoreManager/Index.cshtml 보기를 연 후 바로 다음 코드를 추가 @model 선입니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

이 도우미 메서드는 문자열과 수 있도록 최대 길이 사용 합니다. 제공 된 텍스트에 지정 된 길이 보다 짧은 경우 도우미 결과 출력으로-됩니다. 긴 경우 다음 텍스트를 잘라냅니다 하 고 나머지 부분에 대 한 "..."를 렌더링 합니다.

이제 앨범 제목과 음악가 이름 속성을 25 자 미만 우리의 잘라내기 도우미를 사용할 수 있습니다. 이 새 잘라내기 도우미를 사용 하 여 전체 보기 코드 아래에 나타납니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

이제 /StoreManager/ URL를 살펴봅니다 앨범와 제목 우리의 최대 길이 아래 유지 됩니다.

![](mvc-music-store-part-5/_static/image18.png)

참고: 만들고 하나의 보기에는 도우미를 사용 하 여 간단한 예를 표시 합니다. 사이트 전체에서 사용할 수 있는 도우미 만들기에 대 한 자세한 내용은 내 블로그 게시물을 참조 합니다: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)


>[!div class="step-by-step"]
[이전](mvc-music-store-part-4.md)
[다음](mvc-music-store-part-6.md)
