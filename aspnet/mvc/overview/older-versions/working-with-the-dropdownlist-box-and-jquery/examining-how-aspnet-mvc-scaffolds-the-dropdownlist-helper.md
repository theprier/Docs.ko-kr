---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: "ASP.NET MVC DropDownList 도우미 scaffolds 하는 방법을 검사 | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2012
ms.topic: article
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 737773ab424b3ec3b6139b8c238a60ca23de2e69
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>ASP.NET MVC DropDownList 도우미 scaffolds 하는 방법을 검사 합니다.
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더 및 다음 선택 **컨트롤러 추가**합니다. 컨트롤러 이름을 **StoreManagerController**합니다. 에 대 한 옵션을 설정는 **컨트롤러 추가** 아래 그림과 같이 대화 상자.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

편집 된 *StoreManager\Index.cshtml* 확인 하 여 제거 `AlbumArtUrl`합니다. 제거 `AlbumArtUrl` 프레젠테이션을 가독성을 향상 됩니다. 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

열기는 *Controllers\StoreManagerController.cs* 파일을 찾을 `Index` 메서드. 추가 `OrderBy` 절 하므로 앨범 가격으로 정렬 됩니다. 전체 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

가격으로 정렬 됩니다 간편한 방법이 데이터베이스에 변경 내용을 테스트할 수 있습니다. 편집을 테스트 하는 메서드를 만들 때 저장된 된 데이터는 첫 번째 표시 낮은 가격을 사용할 수 있습니다.

열기는 *StoreManager\Edit.cshtml* 파일입니다. 범례 태그 바로 뒤에 다음 줄을 추가 합니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

다음 코드에서는이 변경의 컨텍스트를 보여 줍니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

`AlbumId` 앨범 레코드를 변경 하려면 필요 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 선택는 **Admin** 링크를 선택 합니다는 **새로 만들기** 앨범을 링크 합니다. 앨범 정보가 저장 된 것을 확인 합니다. 앨범을 편집 하 고 변경 내용을 유지 됩니다 확인 합니다.

### <a name="the-album-schema"></a>앨범 스키마

`StoreManager` MVC 스 캐 폴딩 메커니즘으로 만들어진 컨트롤러 음악 저장소 데이터베이스에는 앨범에 대 한 CRUD (만들기, 읽기, 업데이트, 삭제) 액세스를 허용 합니다. 앨범 정보에 대 한 스키마는 다음과 같습니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

`Albums` 앨범 genre 및 설명에는 테이블에 저장 하지 않으므로, 외래 키를 저장 된 `Genres` 테이블입니다. `Genres` 테이블 장르 이름 및 설명을 포함 합니다. 마찬가지로,는 `Albums` 앨범 예술가 이름은 같지만 대 한 외래 키 테이블에 포함 하지 않습니다는 `Artists` 테이블입니다. `Artists` 테이블 음악가 이름을 포함 합니다. 데이터를 검사 하는 경우는 `Albums` 테이블에 외래 키를 포함 하는 각 행을 볼 수 있습니다는 `Genres` 테이블과 외래 키를는 `Artists` 테이블입니다. 아래 이미지의 일부 테이블 데이터 표시는 `Albums` 테이블입니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML 선택 태그

HTML `<select>` 요소 (HTML에서 만든 [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미) 값 (예: 장르 목록)의 전체 목록을 표시 하는 데 사용 됩니다. 편집 폼에 대 한 select 목록의 현재 값을 확인 하면 현재 값을 표시할 수 있습니다. 에 대해 살펴보았습니다이 이전에 선택한 값을 설정 했습니다 **코미디**합니다. Select 목록 범주 또는 외래 키 데이터를 표시 하기 위해 가장 좋습니다. `<select>` 장르 외래 키에 대 한 요소 표시 가능한 장르 이름의 목록을 하지만 양식을 저장 된 장르 외래 키 값으로 표시 된 장르 이름이 아니라 장르 속성이 업데이트 됩니다. 아래 그림에서는 선택한 genre가 **Disco** 음악가 이며 **Donna 여름**합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>코드 스 캐 폴드 된 ASP.NET MVC를 검사 합니다.

열기는 *Controllers\StoreManagerController.cs* 파일을 찾을 `HTTP GET Create` 메서드.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create` 메서드 두 개를 추가 [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) 개체는 `ViewBag`, 음악가 정보를 포함 하도록 여러 개 있는 장르 정보를 포함 하도록 한 합니다. [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) 위에서 사용한 생성자 오버 로드는 세 개의 인수를 사용 합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *항목*:는 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 목록에 항목을 포함 하 합니다. 반환 된 장르 목록 위의 예에서 `db.Genres`합니다.
2. *dataValueField*:에 속성의 이름은 **IEnumerable** 키 값이 포함 된 목록입니다. 위의 예에서 `GenreId` 및 `ArtistId`합니다.
3. *dataTextField*:에 속성의 이름은 **IEnumerable** 표시할 정보를 포함 하는 목록입니다. 예술가 장르 테이블에는 `name` 필드가 사용 됩니다.

열기는 *Views\StoreManager\Create.cshtml* 파일 및 검사는 `Html.DropDownList` genre 필드에 대 한 도우미 태그입니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

첫 번째 줄 만들기 뷰를 사용 한다고 표시는 `Album` 모델입니다. 에 `Create` 위에 표시 된 모델이 전달 된 보기 가져옵니다 하므로 메서드는 **null** `Album` 모델입니다. 이 시점에서 만드므로 새 앨범 모든 사항이 `Album` 것에 대 한 데이터입니다.

[Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 위에 표시 된 오버 로드를 모델 바인딩할 필드의 이름입니다. 또한 사용 하 여이 이름을 찾습니다는 **ViewBag** 포함 된 개체는 [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) 개체입니다. 이 오버 로드를 사용 해야 하는 이름을 **ViewBag SelectList** 개체 `GenreId`합니다. 두 번째 매개 변수 (`String.Empty`)은 선택 된 항목이 때 표시할 텍스트입니다. 이 새 앨범을 만들 때 원하는 대로 정확 하 게 합니다. 두 번째 매개 변수를 제거 하 고 다음 코드를 사용:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

Select 목록이 샘플의 기본적으로 첫 번째 요소 또는 록 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

검사 하 여 `HTTP POST Create` 메서드.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

이 오버 로드는 `Create` 메서드는 `album` 게시 된 양식 값에서 ASP.NET MVC 모델 바인딩 시스템이 생성 하는 개체입니다. 모델 상태가 유효 하 고 데이터베이스 오류가 없는 경우 새 앨범을 제출 하면 새 앨범이 데이터베이스를 추가 됩니다. 다음 이미지는 새 앨범 만드는 하는 방법을 보여 줍니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

사용할 수는 [fiddler 도구](http://www.fiddler2.com/fiddler2/) 게시 된 양식 값을 검사 하려면 해당 ASP.NET MVC 모델 바인딩 앨범 개체를 만드는 데 사용 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).

### <a name="refactoring-the-viewbag-selectlist-creation"></a>ViewBag SelectList 만들기 리팩터링

두는 `Edit` 메서드 및 `HTTP POST Create` 메서드는 동일한 코드를 설정 하는 **SelectList** 에 **ViewBag**합니다. 목적에 [건조](http://en.wikipedia.org/wiki/Don't_repeat_yourself),이 코드를 리팩터링한 됩니다. 만들면이 사용 하 여 나중에 코드를 리팩터링 합니다.

Genre 및 아티스트를 추가 하려면 새 메서드를 만들 **SelectList** 에 **ViewBag**합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

설정 두 줄을 바꿀는 `ViewBag` 각는 `Create` 및 `Edit` 메서드를 호출 하 여는 `SetGenreArtistViewBag` 메서드. 완성 된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

새 앨범이 만들고 작동 하는 변경 내용을 확인 하기 위해 앨범을 편집 합니다.

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>드롭다운 목록에는 SelectList를 명시적으로 전달

ASP.NET MVC 스 캐 폴딩 사용 하 여 만든 만들기 및 편집 뷰 다음 **DropDownList** 오버 로드 합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

`DropDownList` 뷰 만들기에 대 한 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

때문에 `ViewBag` 속성에 대 한는 `SelectList` 라는 `GenreId`, **DropDownList** 도우미 ´ ֲ는 `GenreId` **SelectList** 에 **ViewBag** . 다음에서 **DropDownList** 오버 로드는 `SelectList` 에 명시적으로 전달 됩니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

열기는 *Views\StoreManager\Edit.cshtml* 파일을 찾아 변경는 **DropDownList** 호출에서 명시적으로 전달 하도록는 **SelectList**, 위의 오버 로드를 사용 합니다. Genre 범주에 대 한이 작업을 수행 합니다. 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

응용 프로그램을 실행 하 고 클릭는 **관리자** 링크를 다음 Jazz 앨범으로 이동한 후 선택 된 **편집** 링크 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

현재 선택 된 장르로 Jazz 숨겨지므로 록 표시 됩니다. 때 문자열 인수 (바인딩할 속성) 및 **SelectList** 개체 이름이 같은, 선택한 값은 사용 되지 않습니다. 브라우저의 첫 번째 요소에 기본 제공 된 선택한 값 없음 이면는 **SelectList**(변수인 **록** 위의 예제에서). 이것은 알려진된 제한인은 **DropDownList** 도우미입니다.

열기는 *Controllers\StoreManagerController.cs* 파일 및 변경의 **SelectList** 개체 이름에 `Genres` 및 `Artists`합니다. 완성 된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

장르와 예술가 이름을 각 범주의 ID 보다 더을 포함 하는 범주에 대 한 더 나은 이름입니다. 이전에 수행한 리팩터링 지불 해야 합니다. 변경 하는 대신는 **ViewBag** 네 가지 메서드가 우리의 변경 내용이 격리 하는 `SetGenreArtistViewBag` 메서드.

변경 된 **DropDownList** 만들기에서 호출 하 고는 new를 사용 하는 보기를 편집할 **SelectList** 이름입니다. 편집 보기에 대 한 새 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

Create view는 SelectList 첫 번째 항목 표시 되지 않도록 방지 하는 빈 문자열을 필요 합니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

새 앨범이 만들고 작동 하는 변경 내용을 확인 하기 위해 앨범을 편집 합니다. 코드 편집 록 이외의 장르와 앨범을 선택 하 여 테스트 합니다.

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>뷰 모델을 사용 하 여 DropDownList 도우미 사용

명명 된 Viewmodel 폴더에서 새 클래스 만들기 `AlbumSelectListViewModel`합니다. 코드는 `AlbumSelectListViewModel` 다음을 사용 하 여 클래스:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

`AlbumSelectListViewModel` 생성자 앨범, 아티스트, 장르 목록 고 앨범을 포함 하는 개체를 만들고 및 `SelectList` 장르와 예술가 대 한 합니다.

프로젝트 빌드 하므로 `AlbumSelectListViewModel` 를 다음 단계에서 뷰를 만들 때 사용할 수 있습니다.

추가 `EditVM` 메서드는 `StoreManagerController`합니다. 완성 된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

마우스 오른쪽 단추로 클릭 `AlbumSelectListViewModel`선택, **해결**, 다음 **MvcMusicStore.ViewModels;를 사용 하 여**합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

또는 다음을 추가할 수 문을 사용 하 여:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

마우스 오른쪽 단추로 클릭 `EditVM` 선택 **뷰 추가**합니다. 아래 표시 된 옵션을 사용 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

선택 **추가**, 다음의 내용을 바꿉니다는 *Views\StoreManager\EditVM.cshtml* 다음 파일:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

`EditVM` 태그는 원래와 매우 유사 `Edit` 태그는 다음과 같은 예외가 있습니다.

- 모델 속성에는 `Edit` 보기는 `model.property`(예를 들어 `model.Title` ). 모델 속성에는 `EditVm` 보기는 `model.Album.property`(예를 들어 `model.Album.Title`). 때문는 `EditVM` 보기에 대 한 컨테이너를 전달 되는 `Album`이 아니라는 `Album` 에서 같이 `Edit` 보기.
- **DropDownList** 하지 뷰 모델에서 가져온 두 번째 매개 변수는 **ViewBag**합니다.
- **BeginForm** 도우미에는 `EditVM` 보기에 다시 명시적으로 게시는 `Edit` 동작 메서드. 에 다시 게시 하 여는 `Edit` 동작을 않아도 작성 하는 `HTTP POST EditVM` 동작 다시 사용할 수 있습니다는 `HTTP POST` `Edit` 동작 합니다.

응용 프로그램을 실행 하 고 앨범을 편집 합니다. URL이 사용 하도록 변경 `EditVM`합니다. 필드를 변경 하 고 적중는 **저장** 코드가 작동 중인지 확인 하는 단추입니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>어떤 방법이 언제 사용 하나요?

표시 된 세 방법 모두 acceptible 됩니다. Explictily 패스에는 개발자가 많습니다는 `SelectList` 에 `DropDownList` 를 사용 하는 `ViewBag`합니다. 이 방법에 컬렉션에 대 한 보다 적절 한 이름을 사용 하 여의 유연성을 제공 하는 추가 이점이 있습니다. 한 가지 주의할 점은 이름을 지정할 수 없습니다는 `ViewBag SelectList` 모델 속성 이름이 같은 개체입니다.

ViewModel 접근 방식을 선호 하는 개발자도 있습니다. 다른 고려 더 자세한 정보 표시 태그 및 생성 된 HTML ViewModel의 단점은 접근 합니다.

이 섹션에는 이전에 배운 것 세 가지 방법을 사용 하는 **DropDownList** 범주 데이터를 사용 합니다. 다음 섹션에서는 새 범주를 추가 하는 방법을 보여줍니다.

>[!div class="step-by-step"]
[이전](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[다음](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
