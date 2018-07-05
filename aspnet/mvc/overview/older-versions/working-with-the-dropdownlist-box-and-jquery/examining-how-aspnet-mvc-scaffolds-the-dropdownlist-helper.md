---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: ASP.NET MVC DropDownList 도우미를 스 캐 폴딩 하는 방법을 검사 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2012
ms.topic: article
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: ece3645f2b37550058a5c93bdd9badbc088ae11c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382967"
---
<a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>ASP.NET MVC DropDownList 도우미를 스 캐 폴딩 하는 방법 검사
====================
[Rick Anderson](https://github.com/Rick-Anderson)

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더를 선택 하 고 **컨트롤러 추가**합니다. 컨트롤러 이름을 **StoreManagerController**합니다. 에 대 한 옵션을 설정 합니다 **컨트롤러 추가** 아래 그림과에서 같이 대화 상자.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

편집 된 *StoreManager\Index.cshtml* 하 고 제거 `AlbumArtUrl`합니다. 제거 `AlbumArtUrl` 프레젠테이션 가독성을 향상 됩니다. 완성된 코드는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

엽니다는 *Controllers\StoreManagerController.cs* 파일을 찾을 `Index` 메서드. 추가 된 `OrderBy` 절을 변경 앨범 가격에 따라 정렬 됩니다. 전체 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

가격으로 정렬 됩니다 쉽게 데이터베이스에 변경 내용을 테스트 합니다. 메서드를 만들고 편집을 테스트 하는 경우 저장된 된 데이터는 첫 번째 나타납니다 낮은 가격을 사용할 수 있습니다.

엽니다는 *StoreManager\Edit.cshtml* 파일입니다. 범례 태그 바로 뒤에 다음 줄을 추가 합니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

다음 코드에서는이 변경의 컨텍스트를 보여 줍니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

`AlbumId` 앨범 레코드를 변경 하려면 필요 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 선택 합니다 **관리자** 링크를 클릭 합니다 **새로 만들기** 앨범에 연결할. 앨범 정보 저장을 확인 합니다. 앨범을 편집 하 고 변경 내용을 유지 됩니다 확인 합니다.

### <a name="the-album-schema"></a>앨범 스키마

`StoreManager` MVC 스 캐 폴딩 메커니즘을 통해 만든 컨트롤러 music store 데이터베이스를 참여 앨범 CRUD (만들기, 읽기, 업데이트, 삭제) 액세스를 허용 합니다. 앨범 정보에 대 한 스키마는 다음과 같습니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

합니다 `Albums` 앨범 장르 및 설명 테이블 저장 하지 않습니다, 외래 키를 저장 합니다 `Genres` 테이블입니다. `Genres` 테이블 장르 이름 및 설명을 포함 합니다. 마찬가지로 합니다 `Albums` 테이블은 앨범 artist 이름은 같지만 외래 키를 포함 하지 않습니다는 `Artists` 테이블입니다. `Artists` 테이블 artist's 이름을 포함 합니다. 데이터를 검사 하는 경우는 `Albums` 테이블에 외래 키를 포함 하는 각 행을 볼 수 있습니다 합니다 `Genres` 테이블과 외래 키를를 `Artists` 테이블입니다. 아래 이미지에서 일부 테이블 데이터를 표시 합니다 `Albums` 테이블입니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML 태그

HTML `<select>` 요소 (HTML에서 만든 [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미) 값 (예: 장르 목록)의 전체 목록을 표시 하는 데 사용 됩니다. 폼 편집에 대 한 select 목록에 현재 값을 확인 하면 현재 값을를 표시할 수 있습니다. 본 것이 이전에 선택한 값을 설정 했습니다 **코미디**합니다. Select 목록 범주 또는 외래 키 데이터를 표시 하거나 적합 합니다. `<select>` 장르 외래 키에 대 한 요소 표시 가능한 장르 이름 목록을 하지만 장르 속성이 장르 외래 키 값을 표시 하는 장르 이름이 아니라으로 업데이트 됩니다 폼을 저장 하는 경우. 아래 이미지에서는 선택한 장르 됩니다 **Disco** 음악가 이며 **Donna 여름**합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>코드 스 캐 폴드 된 ASP.NET MVC를 검사 합니다.

엽니다는 *Controllers\StoreManagerController.cs* 파일을 찾을 `HTTP GET Create` 메서드.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create` 메서드 두 개를 더한 [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) 개체를 `ViewBag`, artist 정보를 포함 하도록 여러 개 있는 장르 정보를 포함 한 합니다. 합니다 [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) 위에서 사용 하는 생성자 오버 로드는 세 가지 인수를 사용 합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *항목*:를 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 목록의 항목을 포함 합니다. 장르 목록을 반환한 위의 예에서 `db.Genres`합니다.
2. *dataValueField*: 속성의 이름을 합니다 **IEnumerable** 키 값이 포함 된 목록입니다. 위의 예에서 `GenreId` 고 `ArtistId`입니다.
3. *dataTextField*: 속성의 이름을 합니다 **IEnumerable** 표시할 정보를 포함 하는 목록입니다. 음악가 장르 테이블에는 `name` 필드를 사용 합니다.

열기는 *Views\StoreManager\Create.cshtml* 파일을 검사 합니다 `Html.DropDownList` genre 필드에 대 한 도우미 태그입니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

만들기 뷰는 첫 번째 줄에는 표시를 `Album` 모델입니다. 에 `Create` 위에 표시 된 모델이 전달 된 뷰에 하므로 메서드는 **null** `Album` 모델입니다. 이 시점에 만들기 새 앨범이 때문 모든 없었습니다 `Album` 에 대 한 데이터입니다.

합니다 [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 위에 표시 된 오버 로드를 모델로 바인딩할 필드의 이름입니다. 또한 사용 하 여이 이름에 대 한 확인을 **ViewBag** 개체를 포함 하는 [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) 개체입니다. 이 오버 로드를 사용 해야 하는 이름 합니다 **ViewBag SelectList** 개체 `GenreId`합니다. 두 번째 매개 변수 (`String.Empty`) 없는 항목이 선택 될 때 표시할 텍스트입니다. 이것이 우리가 원하는 새 앨범이 만들 때입니다. 두 번째 매개 변수를 제거 하 고 다음 코드를 사용:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

Select 목록에는 샘플에서 기본적으로 첫 번째 요소 또는 Rock 됩니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

검사는 `HTTP POST Create` 메서드.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

이 오버 로드는 `Create` 메서드는 `album` 게시 된 양식 값에서 ASP.NET MVC 모델 바인딩 시스템에서 만든 개체입니다. 모델 상태가 유효 하 고 데이터베이스 오류가 없는 경우 새 앨범을 제출 하면 새 앨범에 데이터베이스를 추가 됩니다. 다음 이미지는 새 앨범이 만드는 방법을 보여 줍니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

사용할 수는 [fiddler 도구](http://www.fiddler2.com/fiddler2/) 게시 된 양식 값을 검사할 앨범 개체를 만드는 ASP.NET MVC 모델 바인딩에서 사용 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).

### <a name="refactoring-the-viewbag-selectlist-creation"></a>ViewBag SelectList 생성 리팩터링

모두를 `Edit` 메서드 및 `HTTP POST Create` 메서드는 동일한 코드를 설정 하는 **SelectList** 에 **ViewBag**합니다. 티에서 [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself),이 코드 리팩터링 했습니다. 드리겠습니다이 사용 하 여 나중에 코드를 리팩터링 합니다.

장르 및 artist를 추가 하는 새 메서드를 만듭니다 **SelectList** 에 **ViewBag**합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

설정 두 줄을 `ViewBag` 각를 `Create` 및 `Edit` 메서드를 호출 하 여는 `SetGenreArtistViewBag` 메서드. 완성된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

새 앨범이 만들고 작동 하는 변경 내용을 확인 하려면 앨범을 편집 합니다.

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>DropDownList를 SelectList 명시적으로 전달

다음 ASP.NET MVC 스 캐 폴딩 사용 하 여 만들기 및 편집 보기 생성 **DropDownList** 오버 로드 합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

`DropDownList` 뷰 만들기에 대 한 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

때문에 `ViewBag` 속성에 대 한는 `SelectList` 이름은 `GenreId`, **DropDownList** 도우미를 사용 하 여를 `GenreId` **SelectList** 에 **ViewBag** . 다음과에서 **DropDownList** 오버 로드는 `SelectList` 명시적으로 전달 됩니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

열기는 *Views\StoreManager\Edit.cshtml* 파일을 열고 변경를 **DropDownList** 호출에 명시적으로 전달 합니다 **SelectList**, 위의 오버 로드를 사용 하 여 합니다. 장르 범주에 대해이 작업을 수행 합니다. 완료 된 코드는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

응용 프로그램을 실행 하 고 클릭 합니다 **관리자** 링크를 Jazz 앨범에 이동 하 고 선택 합니다 **편집** 링크 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

현재 선택한 장르가으로 Jazz를 표시 하는 대신 Rock 표시 됩니다. 때 문자열 인수 (바인딩할 속성) 및 **SelectList** 개체 이름이 같은, 선택한 값이 사용 되지 않습니다. 브라우저의 첫 번째 요소에 기본 제공 선택한 값의 경우는 **SelectList**(즉 **Rock** 위의 예제에서). 알려진 제한 사항 합니다 **DropDownList** 도우미입니다.

열기는 *Controllers\StoreManagerController.cs* 파일을 변경 합니다 **SelectList** 개체 이름을 `Genres` 및 `Artists`합니다. 완료 된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

장르 및 아티스트가 이름을 각 범주의 ID 이상만 포함 하는 범주에 대 한 더 나은 이름입니다. 앞서 수행한 리팩터링 결실을 합니다. 변경 하는 대신 합니다 **ViewBag** 네 가지 방법에는 변경 내용이 격리는 `SetGenreArtistViewBag` 메서드.

변경 된 **DropDownList** 호출 만들기에서 및 편집 보기를 사용 하도록 **SelectList** 이름입니다. 편집 보기에 대 한 새 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

Create view는 SelectList 첫 번째 항목은 표시 되지 않도록 방지 하기 위해 빈 문자열이 필요 합니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

새 앨범이 만들고 작동 하는 변경 내용을 확인 하려면 앨범을 편집 합니다. 앨범 Rock 이외의 장르를 사용 하 여 선택 하 여 편집 코드를 테스트 합니다.

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>보기 모델을 사용 하 여 DropDownList 도우미를 사용 하 여

ViewModels 폴더에서 새 클래스를 만들고 `AlbumSelectListViewModel`합니다. 코드는 `AlbumSelectListViewModel` 클래스를 다음으로:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

합니다 `AlbumSelectListViewModel` 생성자는 album, 아티스트, 장르 목록을 만들고 앨범을 포함 하는 개체 및 `SelectList` 장르 및 아티스트가 대 한 합니다.

프로젝트를 빌드 하므로 `AlbumSelectListViewModel` 사용할 수 있는 경우 다음 단계에서는 보기를 만듭니다.

추가 된 `EditVM` 메서드를는 `StoreManagerController`합니다. 완성된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

마우스 오른쪽 단추로 클릭 `AlbumSelectListViewModel`을 선택 **해결**, 한 다음 **MvcMusicStore.ViewModels;를 사용 하 여**입니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

다음을 추가할 수 또는 문을 사용 하 여:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

마우스 오른쪽 단추로 클릭 `EditVM` 선택한 **뷰 추가**합니다. 아래 표시 된 옵션을 사용 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

선택 **추가**, 그런 다음 내용의 합니다 *Views\StoreManager\EditVM.cshtml* 다음을 사용 하 여 파일:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

합니다 `EditVM` 원래 태그 매우 비슷합니다. `Edit` 다음 예외를 사용 하 여 태그입니다.

- 모델의 속성을 `Edit` 뷰는 형식입니다. `model.property`(예를 들어 `model.Title` ). 모델의 속성을 `EditVm` 뷰는 형식입니다. `model.Album.property`(예를 들어 `model.Album.Title`). 있기 때문입니다 합니다 `EditVM` 보기에 대 한 컨테이너를 전달 되는 `Album`아니라는 `Album` 에서처럼를 `Edit` 보기.
- 합니다 **DropDownList** 하지 뷰 모델에서 가져온 두 번째 매개 변수를 **ViewBag**합니다.
- **BeginForm** 도우미에는 `EditVM` 보기에 다시 명시적으로 게시를 `Edit` 작업 메서드. 다시 게시 하 여는 `Edit` 작업에서는 작성할 필요가 `HTTP POST EditVM` 작업 다시 사용할 수 있습니다 합니다 `HTTP POST` `Edit` 작업 합니다.

응용 프로그램을 실행 하 고 앨범을 편집 합니다. URL을 사용 하 여 변경 `EditVM`합니다. 필드를 변경 하 고 적중 합니다 **저장** 코드가 작동 중인지 확인 하는 단추입니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>어떤 방법을 언제 사용 하나요?

표시 된 세 방법 모두 acceptible 됩니다. 대부분의 개발자 explictily 전달 하려는 합니다 `SelectList` 에 `DropDownList` 를 사용 하 여를 `ViewBag`합니다. 이 방법은 컬렉션에 대 한 적합 한 이름을 사용 하 여 유연성을 제공 하는 추가 이점이 있습니다. 중요 한 점은 이름을 지정할 수 없습니다는 `ViewBag SelectList` 모델 속성 이름이 같은 개체입니다.

일부 개발자는 ViewModel 접근을 선호 합니다. 다른 자세한 태그를 고려 하 고 HTML ViewModel 방식의 단점은 생성 합니다.

이 섹션의 세 가지 방법을 사용 하 여 확보 합니다 **DropDownList** 범주 데이터를 사용 하 여 합니다. 다음 섹션에서는 새 범주를 추가 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [다음](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
