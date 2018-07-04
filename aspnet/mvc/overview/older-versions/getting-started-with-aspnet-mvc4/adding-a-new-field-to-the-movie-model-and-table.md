---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 영화 모델 및 테이블에 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: 25a29e783f02e66e1713d8120eb526e1a02961a3
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366478"
---
<a name="adding-a-new-field-to-the-movie-model-and-table"></a>영화 모델 및 테이블에 새 필드 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.


이 섹션에서는 Entity Framework Code First 마이그레이션을 데이터베이스에 변경 내용이 적용 되므로 일부 변경 내용은 모델 클래스로 마이그레이션하려 합니다.

기본적으로 사용 하는 경우 Entity Framework Code First 데이터베이스를 자동으로 만들려면이 자습서의 앞부분에서 수행한 것 처럼 Code First 테이블에 추가 데이터베이스를 데이터베이스의 스키마에서 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적 합니다. 동기화 하지 않은 경우 Entity Framework는 오류를 throw 합니다. 이 쉽게 발생할 수 있는 그렇지 않은 경우만 (모호한 오류가) 하 여 런타임 시 개발 시 문제를 추적 합니다.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>모델 변경에 대 한 Code First 마이그레이션을 설정

Visual Studio 2012를 사용 하는 경우 두 번 클릭 합니다 *Movies.mdf* 데이터베이스 도구를 열려면 솔루션 탐색기에서 파일입니다. Visual Studio Express for Web 알아보겠습니다 데이터베이스 탐색기, Visual Studio 2012 서버 탐색기에 표시 됩니다. Visual Studio 2010를 사용 하는 경우 SQL Server 개체 탐색기를 사용 합니다.

데이터베이스 도구 (데이터베이스 탐색기, 서버 탐색기 또는 SQL Server 개체 탐색기)에서 마우스 오른쪽 단추로 클릭 `MovieDBContext` 선택한 **삭제** 영화 데이터베이스를 삭제 합니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

솔루션 탐색기로 이동 합니다. 마우스 오른쪽 단추로 클릭 합니다 *Movies.mdf* 파일을 선택 **삭제** 영화 데이터베이스를 제거 하려면.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

오류가 없는지 확인 하려면 응용 프로그램을 빌드하십시오.

**도구** 메뉴에서 클릭 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

![팩 Man 추가](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

에 **패키지 관리자 콘솔** 창에는 `PM>` 프롬프트 "Enable-migrations-ContextTypeName MvcMovie.Models.MovieDBContext"를 입력 합니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

합니다 **Enable-migrations** 명령은 (위에 표시 됨)을 만듭니다는 *Configuration.cs* 새 파일 *마이그레이션을* 폴더입니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio가 열립니다는 *Configuration.cs* 파일입니다. 대체는 `Seed` 의 메서드를 *Configuration.cs* 를 다음 코드로 파일:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

아래의 빨간색 물결선을 마우스 오른쪽 단추로 클릭 `Movie` 선택한 **해결** 한 다음 **사용 하 여** **MvcMovie.Models;**

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

다음 항목을 추가 이렇게 문을 사용 하 여:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> 첫 번째 마이그레이션을 호출 코드를 `Seed` 모든 마이그레이션 후 메서드 (즉, 호출 **데이터베이스 업데이트** 패키지 관리자 콘솔에서),이 메서드가 이미 삽입 되었거나 경우 삽입 된 행을 업데이트 하 고 있습니다 아직 존재 하지 마십시오.


**프로젝트를 빌드하려면 CTRL-SHIFT-B를 누릅니다.** (다음 단계를 실패 하는 경우에 시점에서 빌드하지 마세요.)

다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다. 으로이 마이그레이션하는 것이 때문에 새 데이터베이스를 만들고 삭제 하는 *movie.mdf* 이전 단계에서 파일.

에 **패키지 관리자 콘솔** 창 "add-migration Initial" 명령을 초기 마이그레이션을 만들려면. 이름을 "초기"는 임의 이며 만든 마이그레이션 파일의 이름을 하는 데 사용 됩니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션* 폴더 (이름의 *{날짜 스탬프}\_Initial.cs* ),이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다. 마이그레이션 파일 이름이 사전 순서 지정에 도움이 되도록 타임 스탬프를 사용 하 여 고정 됩니다. 검사는 *{날짜 스탬프}\_Initial.cs* 파일인 동영상 DB에 대 한 동영상 테이블을 만드는 지침을 포함 합니다. 이 지침에서 데이터베이스를 업데이트 하는 경우 *{날짜 스탬프}\_Initial.cs* 파일에서는 실행 하 고 DB 스키마를 만듭니다. 그런 다음 **시드** 메서드 테스트 데이터로 DB를 채우기 위해 실행 됩니다.

에 **패키지 관리자 콘솔**, 명령 "업데이트-데이터베이스" 데이터베이스를 만들고 실행 하는 **초기값** 메서드.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

테이블에서 이미 존재 하 고 만들 수 없습니다를 나타내는 오류를 받게 되 면 것 및 실행 하기 전에 데이터베이스를 삭제 한 후 응용 프로그램을 실행 했으므로 `update-database`합니다. 이 경우 삭제 합니다 *Movies.mdf* 파일을 다시 시도 `update-database` 명령입니다. 오류가 여전히 발생 하면, 마이그레이션 폴더 및 내용을 삭제 한 후이 페이지의 맨 위에 있는 지침을 사용 하 여 시작 (삭제 되는 *Movies.mdf* Enable-migrations 진행 한 다음 파일).

응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다. 초기값 데이터가 표시 됩니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>영화 모델에 등급 속성 추가

새로 추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다. 엽니다는 *Models\Movie.cs* 파일을 추가 합니다 `Rating` 다음과 같은 속성:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

전체 `Movie` 다음 코드는 이제 다음과 클래스:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

사용 하 여 응용 프로그램 빌드를 **빌드할** &gt; **영화 빌드** 메뉴 명령 또는 CTRL SHIFT. 키를 눌러

업데이트 했으므로 합니다 `Model` 클래스도 업데이트 해야 합니다 *\Views\Movies\Index.cshtml* 및 *\Views\Movies\Create.cshtml* 새 표시하기위해템플릿을보려면`Rating`브라우저 보기에서 속성입니다.

엽니다는<em>\Views\Movies\Index.cshtml</em> 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤를 <strong>가격</strong> 열입니다. 추가한를 `<td>` 렌더링 템플릿의 끝 열을 `@item.Rating` 값입니다. 업데이트 된 다음과 같습니다 <em>Index.cshtml</em> 보기 템플릿은 다음과 같습니다.

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

다음으로 열고 합니다 *\Views\Movies\Create.cshtml* 파일과 폼의 끝 부분에 다음 태그를 추가 합니다. 이 입력란을 렌더링 하는 새 영화를 만들 때 등급을 지정할 수 있습니다.

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

이제 새 지원 응용 프로그램 코드를 업데이트 했으므로 `Rating` 속성입니다.

이제 응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다. 이 작업을 수행 하지만 나타납니다 다음 오류 중 하나:

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다릅니다 이제는 `Movie` 기존 데이터베이스의 테이블입니다. (데이터베이스 테이블에 `Rating` 열이 없습니다.)


오류를 해결하는 몇 가지 방법이 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 방법은 편리에서 테스트 데이터베이스는 활발 한 개발을 수행 하는 경우 신속 하 게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다. 그러나 단점은 데이터베이스의 기존 데이터를 손실 하는-있도록 있습니다 *하지* 프로덕션 데이터베이스에서이 방법을 사용 하려면! 테스트 데이터로 데이터베이스를 자동으로 시드하는 이니셜라이저를 사용 하는 종종 응용 프로그램을 개발 하는 효율적인 방법입니다. Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 참조 Tom Dykstra [ASP.NET MVC/Entity Framework 자습서](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터를 유지한다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.
3. Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.


이 자습서의 경우 Code First 마이그레이션을 사용합니다.

새 열에 대 한 값을 제공 하도록 Seed 메서드를 업데이트 합니다. Migrations\ configuration.cs 파일을 열고 각 영화 개체에 등급 필드를 추가 합니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

솔루션을 연 다음 합니다 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.

`add-migration AddRatingMig`

`add-migration` 명령은 마이그레이션 프레임 워크에 DB 새 모델로 마이그레이션하는 데 필요한 코드를 만들고 현재 동영상 DB 스키마를 사용 하 여 현재 영화 모델 검사를 지시 합니다. AddRatingMig는 임의 이며 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다. 마이그레이션 단계에 대 한 의미 있는 이름을 사용 하는 것이 유용 합니다.

이 명령은 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMIgration` 파생 클래스에서 및를 `Up` 메서드는 새 열을 만드는 코드를 볼 수 있습니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

솔루션을 빌드하고에서 "데이터베이스 업데이트" 명령을 입력 합니다 **패키지 관리자 콘솔** 창입니다.

다음 이미지는 출력을 표시 합니다 **패키지 관리자 콘솔** 창 (AddRatingMig 앞에 추가 하는 날짜 스탬프는 이와 다릅니다.)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

다시 응용 프로그램을 실행 하 고 /Movies URL로 이동 합니다. 새 등급 필드를 볼 수 있습니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

클릭 합니다 **새로 만들기** 새 영화를 추가 합니다. 참고 등급을 추가할 수 있습니다.

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

**만들기**를 클릭합니다. 등급을 포함 하 여 새 동영상을는 이제 영화 목록에 표시 합니다.

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

도 추가 해야 합니다 `Rating` 템플릿 보기를 편집, 세부 정보 및 SearchIndex 필드입니다.

"데이터베이스 업데이트" 명령에 입력할 수 있습니다 합니다 **패키지 관리자 콘솔** 창을 다시 및 내용이 적용 될, 스키마는 모델과 일치 하므로 합니다.

이 섹션에서는 모델 개체를 수정 및 변경 내용과 동기화 데이터베이스를 유지 하는 방법을 살펴보았습니다. 시나리오를 시도해 볼 수 있도록 샘플 데이터를 사용 하 여 새로 만든된 데이터베이스를 채우는 방법을 알아보았습니다. 다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 될 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)
