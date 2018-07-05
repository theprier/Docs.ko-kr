---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: JQuery UI를 사용 하 여 DropDownList에 새 범주 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: e2528b74b714a3f691b07ed2429b3fe9eb3c2074
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802528"
---
<a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>JQuery UI를 사용 하 여 DropDownList에 새 범주 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

HTML `Select` 태그 고정된 범주 데이터 목록 표시에 적합 하지만 새 범주를 추가 해야 하는 경우도 많습니다. 데이터베이스에 있는 범주를 "Opera" 장르를 추가 하려는 경우를 가정? 이 섹션에서는 새 범주를 추가 하려면 사용할 수 있습니다 대화 상자를 추가 하려면 jQuery UI를 사용 합니다. 아래 이미지에서는 브라우저에서 UI를 제공 하는 방법을 보여 줍니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

사용자가 선택 하는 경우는 **새로운 장르 추가** 링크를 팝업 대화 상자를 묻는 새 장르 이름 (및 필요에 따라 설명). Show 아래 이미지는 **장르 추가** 팝업 대화 상자.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

새로운 장르 이름을 입력 하는 경우 및 **저장** 단추를 누르면 같은 상황이 발생 합니다.

1. AJAX 호출 데이터를 데이터베이스에 새 장르를 저장 하 고 JSON으로 새로운 장르 정보 (장르 이름 및 ID)를 반환 하는 장르 컨트롤러의 Create 메서드를 게시 합니다.
2. JavaScript는 select 목록에 새 장르 데이터를 추가합니다.
3. JavaScript는 새로운 장르 선택한 항목을 만듭니다.

   아래 그림과에서 **Opera** 가 데이터베이스에 추가 되 고 선택 합니다 **장르** 드롭다운 목록입니다. 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

엽니다는 *Views\StoreManager\Create.cshtml* 파일과 장르 태그를 다음으로 바꿉니다 다음 코드:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre` 부분 보기에서 JavaScript 및 jQuery 새로운 장르 추가 기능을 구현 하는 데 후크 모든 논리를 포함 합니다. 것은 간단 하 게 artist UI 사용 하 여 동일한 작업을 수행 하는 코드를 완료 했습니다.

솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *Views\StoreManager* 폴더를 선택 **추가**, 한 다음 **보기**합니다. 에 **뷰 이름** 입력, 입력 `_ChooseGenre` 선택한 **추가**합니다. 태그를 대체 합니다 *Views\StoreManager\\_ChooseGenre.cshtml* 다음 파일:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

첫 번째 줄 선언에 전달 하는 `Album` Create view 문이 모델 똑같이 모델로 합니다. 다음 몇 줄은는 **레이블** 도우미 태그입니다. 다음 줄은는 **DropDownList** 도우미 호출 원래 Create view와 정확히 동일 합니다. 이름의 링크를 추가 하는 다음 줄 `Add New Genre`, 및 단추와 같은 스타일입니다. 포함 된 줄 `ValidationMessageFor` 만들기 뷰에서 직접 복사 됩니다. 다음 줄:

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

ID를 사용 하 여 숨겨진된 div 만듭니다 `genreDialog`합니다. JQuery 후크 하는 데 사용 하는 우리의 **추가 장르** 대화 상자 ID 사용 하 여 `genreDialog` 이 div.에서 마지막으로 두 개의 스크립트 태그를 사용 하면 새 장르 추가 기능을 구현 하는 데 사용 하는 JavaScript 파일에 링크가 있습니다. 합니다 */Scripts/chooseGenre.js* 파일이 프로젝트에 자동으로 살펴보겠습니다이 자습서의 뒷부분에 제공 합니다.

응용 프로그램을 실행 하 고 클릭 합니다 **새로운 장르 추가** 단추입니다. 에 **추가 장르** 대화 상자에 입력 합니다 **Opera** 에 **이름** 입력된 상자.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

**저장** 단추를 클릭합니다. AJAX 호출 Opera 범주 및 다음 Opera 사용 하 여 드롭다운 목록을 채웁니다 만들고 Opera 선택한 장르가로 설정 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

아티스트, 제목 및 가격을 입력 하 고 선택 합니다 **만들기** 단추입니다. $8.99 미만의 가격을 입력 하면 인덱스 뷰의 맨 위에 있는 새 앨범이 나타납니다. 데이터베이스에 저장 된 새 앨범 항목을 확인 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

하나의 문자만 사용 하 여는 새로운 장르를 만들어 보세요. 다음 코드를 *Models\Genre.cs* 파일 장르 이름의 최소 및 최대 길이 설정 합니다.

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

클라이언트 쪽 유효성 검사 보고서 2 ~ 20 자 사이의 문자열을 입력 해야 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>어떻게는 새로운 장르를 검사 하는 데이터베이스 및 선택 목록에 추가 됩니다.

엽니다는 *Scripts\chooseGenre.js* 파일 및 코드를 검사 합니다.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

ID를 사용 하 여 두 번째 줄 `genreDialog` div 태그에 대화 상자를 만들려면 합니다 *Views\StoreManager\\_ChooseGenre.cshtml* 파일입니다. 대부분의 명명 된 매개 변수는 자체 설명 합니다. `autoOpen` 매개 변수를 false로 설정 선택 하는 **장르 만들기** 단추는 대화를 명시적으로 열 (이 설명에서 두 번째). 해당 대화 상자에 두 개의 단추를 **저장할** 하 고 **취소**합니다. 합니다 **취소** 단추 대화 상자를 닫습니다. 다음 코드에서는 합니다 **저장할** 함수 단추입니다.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

합니다 `var createGenreForm` 에서 선택 된 된 `createGenreForm` id입니다. 합니다 `createGenreForm` 에 다음 코드에 설정 된 ID는 *Views\Genre\\_CreateGenre.cshtml* 파일입니다.

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

[Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) 에 사용 되는 도우미 오버 로드는 *Views\Genre\\_CreateGenre.cshtml* 파일 양식을 제출 URL이 포함 된 작업 특성을 사용 하 여 HTML을 생성 합니다. 브라우저에서 만들기 album 페이지를 표시 하 고 브라우저에서 표시 원본을 선택 하 여이 확인할 수 있습니다. 다음 태그는 form 태그를 포함 하는 생성 된 HTML을 보여 줍니다.

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

JQuery `$.post` 줄 고, 작업 특성에 대 한 AJAX 호출을 통해 (`/StoreManager/Create`)에서 데이터를 전달 합니다 **장르 만들기** 대화 상자. 데이터의 새 장르 및 선택적 설명을 이름으로 구성 됩니다. AJAX 호출이 성공 하면 새 장르 이름 및 값 선택 태그에 추가 됩니다 하 고 새 장르 선택한 값으로 설정 됩니다. 동적으로 생성 된 태그 이기 때문에 브라우저에서 소스를 확인 하 여 새 선택 옵션을 볼 수 없습니다. IE 9 F12 개발자 도구를 사용 하 여 새 HTML을 볼 수 있습니다. Internet Explorer 9를 새 선택 옵션을 보려면 F12 개발자 도구를 시작 하려면 F12 키를 누릅니다. 만들기 페이지로 이동한 후는 새로운 장르를 추가 하는 새로운 장르 장르 선택 목록에서 선택 합니다. F12 개발자 도구:

1. HTML 탭을 선택 합니다.
2. 새로 고침 아이콘을 누릅니다.  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. 검색 상자에서 GenreID를 입력 합니다.
4. 다음 아이콘을 사용 하 여   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   다음 select 태그로 이동 합니다.

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. 마지막 옵션 값을 확장 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

에 다음 코드를 *Scripts\chooseGenre.js* 파일에는 방법을 보여 줍니다 합니다 **새 장르 추가** 단추 클릭 이벤트에 연결 됩니다 하는 방법과 **새 장르 추가** 대화 상자는 만들어집니다.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

첫 번째 줄에 연결 하는 클릭 함수를 만듭니다는 **새로운 장르 추가** 단추입니다. Views\StoreManager에서 다음과 같은 태그가\\_ChooseGenre.cshtml 파일 표시 하는 방법을 **새 장르 추가** 단추 만들어집니다:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Load 메서드를 만듭니다 및 장르 추가 대화 상자를 엽니다 및 jQuery 호출 `parse` 메서드 클라이언트 유효성 검사 대화 상자에 입력 된 데이터에서 발생 합니다.

이 섹션에서는 범주 데이터를 새 선택 목록에 추가할 수 있는 대화를 만드는 방법을 배웠습니다. 새 artist를 artist select 목록에 추가 하는 UI를 만들려면 동일한 절차를 따르면 됩니다. 이 자습서는 ASP.NET MVC HTML 도우미를 사용 하 여 작업의 개요를 제공 했습니다 **DropDownList**합니다. 작업에 대 한 자세한 내용은 합니다 **DropDownList**, 아래 추가 참조 섹션을 참조 하세요. 알려주세요이 자습서 도움이 되었으면 합니다.

Rick.Anderson[at]Microsoft.com

### <a name="additional-references"></a>추가 참조

- [자습서를 나열 하는 ASP.NET MVC – 계단식 드롭다운](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) 여 [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- [선택한](http://harvesthq.github.com/chosen/) 다중 선택 및 필터링을 지 원하는 JavaScript 플러그 인입니다.

### <a name="contributors"></a>참가자

- [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>검토자

- Jean Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)
- Mike 되
- Tom Dykstra

> [!div class="step-by-step"]
> [이전](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
