---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 950ae17ebd6b0f15520c2a4e9372703f5374dfbe
ms.sourcegitcommit: 97d7a00bd39c83a8f6bccb9daa44130a509f75ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54098690"
---
<a name="adding-a-new-field"></a>새 필드 추가
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](sample/code-location.md)]

이 섹션에서는 Entity Framework Code First 마이그레이션을 데이터베이스에 변경 내용이 적용 되므로 일부 변경 내용은 모델 클래스로 마이그레이션하려 합니다.

기본적으로 사용 하는 경우 Entity Framework Code First 데이터베이스를 자동으로 만들려면이 자습서의 앞부분에서 수행한 것 처럼 Code First 테이블에 추가 데이터베이스를 데이터베이스의 스키마에서 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적 합니다. 동기화 하지 않은 경우 Entity Framework는 오류를 throw 합니다. 이 쉽게 발생할 수 있는 그렇지 않은 경우만 (모호한 오류가) 하 여 런타임 시 개발 시 문제를 추적 합니다.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>모델 변경에 대 한 Code First 마이그레이션을 설정

솔루션 탐색기로 이동 합니다. 마우스 오른쪽 단추로 클릭 합니다 *Movies.mdf* 파일을 선택 **삭제** 영화 데이터베이스를 제거 하려면. 표시 되지 않는 경우는 *Movies.mdf* 파일을 클릭 합니다 **모든 파일 표시** 아래에 빨간색 윤곽선이 표시 된 아이콘입니다.

![](adding-a-new-field/_static/image1.png)

오류가 없는지 확인 하려면 응용 프로그램을 빌드하십시오.

**도구** 메뉴에서 클릭 **NuGet 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

![팩 Man 추가](adding-a-new-field/_static/image2.png)

에 **패키지 관리자 콘솔** 창에는 `PM>` 입력 프롬프트

Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext

![](adding-a-new-field/_static/image3.png)

합니다 **Enable-migrations** 명령은 (위에 표시 됨)을 만듭니다는 *Configuration.cs* 새 파일 *마이그레이션을* 폴더입니다.

![](adding-a-new-field/_static/image4.png)

Visual Studio가 열립니다는 *Configuration.cs* 파일입니다. 대체는 `Seed` 의 메서드를 *Configuration.cs* 를 다음 코드로 파일:

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

아래의 빨간색 물결선을 마우스로 `Movie` 을 클릭 `Show Potential Fixes` 을 클릭 한 다음 **사용 하 여** **MvcMovie.Models;**

![](adding-a-new-field/_static/image5.png)

다음 항목을 추가 이렇게 문을 사용 하 여:

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> 첫 번째 마이그레이션을 호출 코드를 `Seed` 모든 마이그레이션 후 메서드 (즉, 호출 **데이터베이스 업데이트** 패키지 관리자 콘솔에서),이 메서드가 이미 삽입 되었거나 경우 삽입 된 행을 업데이트 하 고 있습니다 아직 존재 하지 마십시오.
> 
> 합니다 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드에 다음 코드에서는 "upsert" 작업을 수행 합니다.
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> 때문에 합니다 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 모든 마이그레이션을 사용 하 여 메서드 실행, 이기 때문에 추가 하려는 행 이미 있는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 데이터를 삽입할 수 없습니다. "[upsert](http://en.wikipedia.org/wiki/Upsert)" 작업이 이미 존재 하는 행을 삽입 하려는 경우는 오류를 방지할 수 있지만 사용자가 변경한 응용 프로그램을 테스트 하는 동안 데이터에 변경 내용을 재정의 합니다. 일부 테이블의 테스트 데이터를 사용 하 여 하지 않으려는 경우이 위해서는: 경우에 따라 테스트 하는 동안 데이터를 변경한 경우 원하는 데이터베이스 업데이트 후 유지 하려면 변경 내용을 합니다. 조건부 삽입 작업을 수행 하려는 경우: 존재 하지 않는 경우에 행을 삽입 합니다.   
> 
> 첫 번째 매개 변수가 전달 되는 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드는 행이 이미 존재 하는지 확인 하는 데 속성을 지정 합니다. 테스트 동영상 데이터를 제공 하는 대 한는 `Title` 목록의 각 제목은 고유 하므로이 목적을 위해 속성을 사용할 수 있습니다.
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> 이 코드 제목 고유 가정 합니다. 중복 된 제목에 수동으로 추가한 경우 마이그레이션을 수행한 다음에 다음 예외를 얻게 됩니다.   
> 
>  *시퀀스에 요소가 둘 이상*  
> 
> 에 대 한 자세한 내용은 합니다 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드를 참조 하십시오 [EF 4.3 AddOrUpdate 메서드를 사용 하 여 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)...


**프로젝트를 빌드하려면 CTRL-SHIFT-B를 누릅니다.** (다음 단계를 실패 함이 시점에서 작성 하지 않아도 됩니다.)

다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다. 이 마이그레이션은 바로 때문에 새 데이터베이스를 만들고 삭제 하는 *movie.mdf* 파일을 이전 단계에서.

에 **패키지 관리자 콘솔** 창에서 명령을 입력 합니다 `add-migration Initial` 초기 마이그레이션을 만들려면. 이름을 "초기"는 임의 이며 만든 마이그레이션 파일의 이름을 하는 데 사용 됩니다.

![](adding-a-new-field/_static/image6.png)

Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션* 폴더 (이름의 *{날짜 스탬프}\_Initial.cs* ),이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다. 마이그레이션 파일 이름이 사전 순서 지정에 도움이 되도록 타임 스탬프를 사용 하 여 고정 됩니다. 검사는 *{날짜 스탬프}\_Initial.cs* 파일을 만드는 지침 포함을 `Movies` 동영상 DB에 대 한 테이블입니다. 이 지침에서 데이터베이스를 업데이트 하는 경우 *{날짜 스탬프}\_Initial.cs* 파일에서는 실행 하 고 DB 스키마를 만듭니다. 그런 다음 **시드** 메서드 테스트 데이터로 DB를 채우기 위해 실행 됩니다.

에 **패키지 관리자 콘솔**을 명령을 입력 합니다 `update-database` 데이터베이스를 만들고 실행 하는 `Seed` 메서드.

![](adding-a-new-field/_static/image7.png)

테이블에서 이미 존재 하 고 만들 수 없습니다를 나타내는 오류를 받게 되 면 것 및 실행 하기 전에 데이터베이스를 삭제 한 후 응용 프로그램을 실행 했으므로 `update-database`합니다. 이 경우 삭제 합니다 *Movies.mdf* 파일을 다시 시도 `update-database` 명령입니다. 오류가 여전히 발생 하면, 마이그레이션 폴더 및 내용을 삭제 한 후이 페이지의 맨 위에 있는 지침을 사용 하 여 시작 (삭제 되는 *Movies.mdf* Enable-migrations 진행 한 다음 파일). 오류가 여전히 발생 하면, SQL Server 개체 탐색기를 열고 목록에서 데이터베이스를 제거 합니다.

응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다. 초기값 데이터가 표시 됩니다.

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>영화 모델에 등급 속성 추가

새로 추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다. 엽니다는 *Models\Movie.cs* 파일을 추가 합니다 `Rating` 다음과 같은 속성:

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

전체 `Movie` 다음 코드는 이제 다음과 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

(Ctrl + Shift + B) 응용 프로그램을 빌드하십시오.

새 필드를 추가 했으므로 합니다 `Movie` 클래스도 업데이트 해야 바인딩을 *허용 목록* 이 새 속성이 포함 되도록 합니다. 업데이트를 `bind` 특성에 대 한 `Create` 하 고 `Edit` 포함 하는 작업 메서드는 `Rating` 속성:

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

브라우저 보기에서 새 `Rating` 속성을 표시, 작성 및 편집하기 위해 보기 템플릿도 업데이트해야 합니다.

엽니다는 *\Views\Movies\Index.cshtml* 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤를 **가격** 열입니다. 추가한를 `<td>` 렌더링 템플릿의 끝 열을 `@item.Rating` 값입니다. 업데이트 된 다음과 같습니다 *Index.cshtml* 보기 템플릿은 다음과 같습니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

을 엽니다는 *\Views\Movies\Create.cshtml* 파일을 추가 합니다 `Rating` 다음 highlighed 태그를 사용 하 여 필드입니다. 이 입력란을 렌더링 하는 새 영화를 만들 때 등급을 지정할 수 있습니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

이제 새 지원 응용 프로그램 코드를 업데이트 했으므로 `Rating` 속성입니다.

응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다. 이 작업을 수행 하지만 나타납니다 다음 오류 중 하나:

![](adding-a-new-field/_static/image9.png)  
  
'MovieDBContext' 컨텍스트를 지 원하는 모델 데이터베이스를 만든 이후에 변경 되었습니다. Code First 마이그레이션을 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 (https://go.microsoft.com/fwlink/?LinkId=238269)합니다.

![](adding-a-new-field/_static/image10.png)

때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다릅니다 이제는 `Movie` 기존 데이터베이스의 테이블입니다. (데이터베이스 테이블에 `Rating` 열이 없습니다.)


오류를 해결하는 몇 가지 방법이 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 방법은 테스트 데이터베이스에서 활발한 개발을 수행할 때 개발 주기의 초기 단계에서 매우 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다. 그러나 단점은 데이터베이스의 기존 데이터를 손실 하는-있도록 있습니다 *하지* 프로덕션 데이터베이스에서이 방법을 사용 하려면! 테스트 데이터로 데이터베이스를 자동으로 시드하는 데 이니셜라이저를 사용하는 것은 종종 애플리케이션을 개발하는 효율적인 방법입니다. Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 참조 하세요. [ASP.NET MVC/Entity Framework 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터를 유지한다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.
3. Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.


이 자습서의 경우 Code First 마이그레이션을 사용합니다.

새 열에 대 한 값을 제공 하도록 Seed 메서드를 업데이트 합니다. Migrations\ configuration.cs 파일을 열고 각 영화 개체에 등급 필드를 추가 합니다.

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

솔루션을 연 다음 합니다 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.

`add-migration Rating`

`add-migration` 명령은 마이그레이션 프레임 워크에 DB 새 모델로 마이그레이션하는 데 필요한 코드를 만들고 현재 동영상 DB 스키마를 사용 하 여 현재 영화 모델 검사를 지시 합니다. 이름을 *등급* 는 임의 이며 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다. 마이그레이션 단계에 대 한 의미 있는 이름을 사용 하는 것이 유용 합니다.

이 명령은 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMigration` 파생 클래스에서 및를 `Up` 메서드는 새 열을 만드는 코드를 볼 수 있습니다.

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

솔루션을 작성 하 고 enter를 `update-database` 명령에 **패키지 관리자 콘솔** 창입니다.

다음 이미지에서 출력을 보여 줍니다.는 **패키지 관리자 콘솔** 창 (날짜 스탬프 앞 *등급* 다릅니다.)

![](adding-a-new-field/_static/image11.png)

다시 응용 프로그램을 실행 하 고 /Movies URL로 이동 합니다. 새 등급 필드를 볼 수 있습니다.

![](adding-a-new-field/_static/image12.png)

클릭 합니다 **새로 만들기** 새 영화를 추가 합니다. 참고 등급을 추가할 수 있습니다.

![7_CreateRioII](adding-a-new-field/_static/image13.png)

**만들기**를 클릭합니다. 등급을 포함 하 여 새 동영상을는 이제 영화 목록에 표시 합니다.

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

이제 프로젝트 migrations를 사용 하는 새 필드를 추가 하거나 그렇지 않은 경우 스키마를 업데이트할 때 데이터베이스를 삭제할 필요가 없습니다. 다음 섹션에서는에서는 더 많은 스키마 변경을 수행 하 고 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.

도 추가 해야 합니다 `Rating` 필드 템플릿 보기 편집, 세부 정보 및 삭제를 합니다.

"데이터베이스 업데이트" 명령에 입력할 수 있습니다 합니다 **패키지 관리자 콘솔** 창을 다시 및 없는 마이그레이션 코드 실행, 스키마 모델과 일치 하기 때문에 있습니다. 그러나 실행은 "데이터베이스 업데이트"를 실행 합니다 `Seed` 메서드를 다시 시드 데이터를 변경한 경우 변경 내용이 손실 됩니다 때문에 `Seed` 메서드 upsert 데이터입니다. 에 대 한 자세한 내용은 합니다 `Seed` 인기 있는 Tom Dykstra에서 메서드 [ASP.NET MVC/Entity Framework 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.

이 섹션에서는 모델 개체를 수정 및 변경 내용과 동기화 데이터베이스를 유지 하는 방법을 살펴보았습니다. 시나리오를 시도해 볼 수 있도록 샘플 데이터를 사용 하 여 새로 만든된 데이터베이스를 채우는 방법을 알아보았습니다. 이 Code First를 간단한 소개를 참조 하십시오 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 주체에 대 한 자세한 자습서에 대 한 합니다. 다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 될 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-search.md)
> [다음](adding-validation.md)
