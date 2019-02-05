---
uid: mvc/overview/getting-started/introduction/adding-search
title: 검색 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/22/2015
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: 31fd35ac63f3eb31d824e1710833ad83a0852ac9
ms.sourcegitcommit: a91e8dd2f4b788114c8bc834507277f4b5e8d6c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/04/2019
ms.locfileid: "55712265"
---
<a name="search"></a>검색
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="adding-a-search-method-and-search-view"></a>검색 방법 및 검색 뷰를 추가합니다.

이 섹션에서는 검색 기능을 추가 합니다 `Index` 작업 메서드를 사용 하면 영화 장르 또는 이름으로 검색 합니다.

## <a name="updating-the-index-form"></a>인덱스 형식 업데이트

업데이트 하 여 시작 합니다 `Index` 동작 메서드를 기존 `MoviesController` 클래스입니다. 코드는 다음과 같습니다.

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

첫 번째 줄을 `Index` 메서드는 다음 항목을 만듭니다 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 영화를 선택 하는 쿼리:

[!code-csharp[Main](adding-search/samples/sample2.cs)]

쿼리가 시점에서 정의 되었지만 데이터베이스에 대해 아직 실행 되지 않았습니다.

경우는 `searchString` 문자열을 포함 하는 매개 변수, 영화 쿼리는 다음 코드를 사용 하 여 검색 문자열의 값에 필터링 하도록 수정 됩니다.

[!code-csharp[Main](adding-search/samples/sample3.cs)]

위의 `s => s.Title` 코드는 [람다 식](https://msdn.microsoft.com/library/bb397687.aspx)입니다. 람다 식은 메서드 기반 되는 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 와 같은 표준 쿼리 연산자 메서드의 인수로 쿼리는 [여기서](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 메서드 위의 코드에 사용 합니다. LINQ 쿼리는 정의 될 때 또는 같은 메서드를 호출 하 여 수정 될 때 실행 되지 않습니다 `Where` 또는 `OrderBy`합니다. 대신 쿼리 실행이 지연, 즉, 실현된 된 값이 실제로 반복 될 때까지 식의 계산이 지연 되는 또는 [ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx) 메서드가 호출 됩니다. 에 `Search` 샘플에서 쿼리가 실행 되는 *Index.cshtml* 보기. 지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.

> [!NOTE]
> 합니다 [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 메서드 c# 코드가 아니라 위의 데이터베이스에서 실행 됩니다. 데이터베이스에서 [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 매핑됩니다 [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx)는 대/소문자 구분 합니다.

업데이트할 수 있습니다 이제는 `Index` 폼을 사용자에 게 표시 되는 보기입니다.

응용 프로그램을 실행 하 고 이동 */Movies/Index*합니다. 쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다. 필터링된 동영상이 표시됩니다.

![SearchQryStr](adding-search/_static/image1.png)

시그니처를 변경 하는 경우는 `Index` 명명 된 매개 변수를 포함 하는 방법 `id`, `id` 매개 변수는 일치를 `{id}` 기본값에 대 한 자리 표시자 경로 집합에는 *앱\_시작 RouteConfig.cs* 파일입니다.

[!code-json[Main](adding-search/samples/sample4.json)]

원래 `Index` 메서드는 다음과 같습니다:

[!code-csharp[Main](adding-search/samples/sample5.cs)]

수정 된 `Index` 메서드는 다음과 같습니다.

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

이제 쿼리 문자열 값이 아닌 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.

![](adding-search/_static/image2.png)

그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하지는 않습니다. UI를 추가할 수 있습니다 이제 영화를 필터링 합니다. 시그니처를 변경 하는 경우는 `Index` 경로 바인딩 ID 매개 변수를 전달 하는 방법을 테스트 하는 방법 변경는 하 `Index` 라는 문자열 매개 변수를 사용 하는 메서드 `searchString`:

[!code-csharp[Main](adding-search/samples/sample7.cs)]

열기는 *Views\Movies\Index.cshtml* 파일을 열고 바로 뒤 `@Html.ActionLink("Create New", "Create")`, 아래 강조 표시 된 폼 태그를 추가 합니다.

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

합니다 `Html.BeginForm` 도우미를 만듭니다 `<form>` 태그입니다. 합니다 `Html.BeginForm` 도우미 하면 폼이 사용자가 클릭 하 여 폼을 제출 하는 경우 자신에 게 게시 합니다 **필터** 단추입니다.

Visual Studio 2013이 표시 하 고 보기 파일을 편집 하는 경우 유용한 개선 합니다. 를 실행 하면 응용 프로그램 뷰 파일을 사용 하 여 open Visual Studio 2013 뷰를 표시 하는 올바른 컨트롤러 작업 메서드를 호출 합니다.

![](adding-search/_static/image3.png)

인덱스 뷰를 사용 하 여 위의 이미지에서과 같이 Visual Studio에서 열기, 탭 Ctr F5 또는 f5 키를 응용 프로그램을 실행 한 다음 동영상을 검색 해 보세요.

![](adding-search/_static/image4.png)

방법이 없는 `HttpPost` 오버 로드는 `Index` 메서드. 필요 없는, 메서드는 응용 프로그램의 상태를 변경 하지 않고 때문에 데이터를 필터링 합니다.

다음 `HttpPost Index` 메서드를 추가할 수 있습니다. 작업 호출자는 일치 하는 경우는 `HttpPost Index` 메서드 및 `HttpPost Index` 메서드는 아래 이미지에 표시 된 대로 실행 됩니다.

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

그러나 이 `HttpPost` 버전의 `Index` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다. 특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다. HTTP POST에 대 한 URL를 요청 하는 GET 요청 (xxxxx/Movies/Index)에 대 한 URL과 동일한-URL 자체의 검색 정보가 없습니다. 오른쪽 이제 검색 문자열 정보를 서버로 전송 됩니다는 양식 필드 값으로. 즉, URL에 친구를 보내거나 책갈피에 해당 검색 정보를 캡처할 수 없습니다.

솔루션의 오버 로드를 사용 하는 것 `BeginForm` 에 POST 요청을 URL로 검색 정보를 추가 하도록 하 고를 라우팅할 수 해야를 지정 하는 `HttpGet` 버전의는 `Index` 메서드. 매개 변수가 없는 기존 항목 바꾸기 `BeginForm` 다음 태그를 사용 하 여 메서드:

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

이제 검색을 제출할 때 URL 검색 쿼리 문자열을 포함 합니다. `HttpPost Index` 메서드가 있는 경우에도 검색은 `HttpGet Index` 작업 메서드로 이동합니다.

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>장르별 검색 추가

추가한 경우에 `HttpPost` 버전의는 `Index` 메서드를 지금 삭제 합니다.

다음으로, 사용자가 영화 장르 하 여 검색할 수 있도록 하는 기능을 추가 합니다. `Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-search/samples/sample11.cs)]

이 버전의 `Index` 메서드는 추가 매개 변수, 즉 `movieGenre`합니다. 코드의 처음 몇 줄 만들기는 `List` 데이터베이스에서 영화 장르를 포함 하는 개체입니다.

다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.

[!code-csharp[Main](adding-search/samples/sample12.cs)]

코드를 사용 하는 `AddRange` 제네릭 메서드의 `List` 목록에는 모든 고유 장르를 추가할 컬렉션입니다. (없이 `Distinct` 한정자를 중복 장르가 추가-코미디 샘플에서 두 번 추가할 수는 예를 들어). 코드에는 장르 목록을 저장 된 `ViewBag.MovieGenre` 개체입니다. 범주 데이터 (이러한 영화 장르의)으로 저장을 [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) 개체는 `ViewBag`, MVC 응용 프로그램에 대 한 일반적인 방식은 드롭다운 목록 상자에서 범주 데이터에 액세스 한 다음.

다음 코드를 확인 하는 방법을 보여 줍니다는 `movieGenre` 매개 변수입니다. 비어 있지 않으면 코드를 추가로 지정된 장르에 선택한 영화를 제한 하려면 영화 쿼리를 제한 합니다.

[!code-csharp[Main](adding-search/samples/sample13.cs)]

영화 목록 반복 될 때까지 쿼리가 데이터베이스에서 실행 되지에서 설명한 대로 (후 보기에서 발생 하는 `Index` 작업 메서드는 반환).

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>장르별 검색을 지원 하도록 인덱스 보기에 태그 추가

추가 `Html.DropDownList` 도우미를 *Views\Movies\Index.cshtml* 파일을 바로 앞의 `TextBox` 도우미입니다. 완료 된 태그는 다음과 같습니다.

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

다음 코드에서

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

매개 변수 "MovieGenre"에 대 한 키를 제공 합니다 `DropDownList` 찾으려고 도우미를 `IEnumerable<SelectListItem>` 에서 `ViewBag`. `ViewBag` 작업 메서드에서 채워졌습니다.

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

옵션 레이블을 제공 "All" 매개 변수입니다. 브라우저에서 선택한 항목을 검사 하는 경우 해당 "value" 특성이 비어 있음을 표시 됩니다. 컨트롤러만 필터링 때문 `if` 문자열이 아닙니다 `null` 이거나 비어 있으면 빈 값에 대 한 제출 `movieGenre` 모든 장르를 보여 줍니다.

또한 기본적으로 선택 하는 옵션을 설정할 수 있습니다. 컨트롤러의 코드를 변경 하는 기본 옵션으로 "코미디" 하려는 경우 다음과 같이 합니다.

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

응용 프로그램을 실행 하 고 이동할 */Movies/Index*합니다. 장르별, 동영상 이름별 및 모두 기준으로 검색을 시도해 보세요.

![](adding-search/_static/image8.png)

이 섹션에서는 검색 작업 메서드 및 사용자가 영화 제목과 장르 하 여 검색할 수 있는 보기를 만들었습니다. 다음 섹션에서 살펴보겠습니다 속성을 추가 하는 방법의 `Movie` 모델과 테스트 데이터베이스를 자동으로 만들어집니다 하는 이니셜라이저를 추가 하는 방법입니다.

> [!div class="step-by-step"]
> [이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-a-new-field.md)
