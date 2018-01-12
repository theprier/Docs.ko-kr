---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: "새 필드 추가 | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7427b4f7c6b7a00fe795053aac0f612471a163cd
ms.sourcegitcommit: 2b263e87217658caa42eedc4f9d2d21ef0ab5d59
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
<a name="adding-a-new-field"></a>새 필드 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE[Tutorial Note](sample/code-location.md)]

이 섹션에서는 변경 내용이 데이터베이스에 적용 되므로 일부 변경 내용이 모델 클래스 마이그레이션할 Entity Framework Code First 마이그레이션을 사용 합니다.

기본적으로를 사용 하 여 Entity Framework Code First 자동으로 데이터베이스를 만들려면이 자습서의 앞부분에서 마찬가지로 코드 첫 번째 테이블에 추가 데이터베이스는 데이터베이스의 스키마에서 생성 된 모델 클래스 동기화 되어 있는지 여부를 추적 해야 합니다. 동기화 하지 않을 경우 Entity Framework에서 오류가 발생 합니다. 이렇게 하면 그렇지 않으면만 찾을 수 (모호한 오류)에 의해 런타임 시 개발 시 문제를 추적 하기가 있습니다.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>Code First 마이그레이션을 모델 변경 내용에 대 한 설정

솔루션 탐색기로 이동 합니다. 마우스 오른쪽 단추로 클릭는 *Movies.mdf* 파일을 선택 **삭제** 영화 데이터베이스를 제거 하려면. 표시 되지 않으면는 *Movies.mdf* 파일, 클릭는 **모든 파일 표시** 빨간색 윤곽선에서 아래 표시 된 아이콘입니다.

![](adding-a-new-field/_static/image1.png)

오류가 없는 되도록 응용 프로그램을 빌드하십시오.

**도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

![팩 매뉴얼 추가](adding-a-new-field/_static/image2.png)

에 **패키지 관리자 콘솔** 창에는 `PM>` 입력 프롬프트

Enable-migrations-ContextTypeName MvcMovie.Models.MovieDBContext

![](adding-a-new-field/_static/image3.png)

**Enable-migrations** 명령은 (위에 표시)을 만듭니다는 *Configuration.cs* 를 새로운 파일 *마이그레이션* 폴더입니다.

![](adding-a-new-field/_static/image4.png)

Visual Studio가 열릴는 *Configuration.cs* 파일입니다. 대체는 `Seed` 에서 메서드는 *Configuration.cs* 를 다음 코드로 파일:

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

빨간색의 구불구불한 선이 아래에서 위로 마우스를 가져가고 `Movie` 클릭 `Show Potential Fixes` 클릭 하 고 **를 사용 하 여** **MvcMovie.Models;**

![](adding-a-new-field/_static/image5.png)

이렇게 하면 추가 되므로 다음 문을 사용 하 여:

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE] 
> 
> First 마이그레이션이 호출 코드의 `Seed` 모든 마이그레이션 후 메서드 (즉, 호출 **데이터베이스 업데이트** 패키지 관리자 콘솔에서),이 메서드는 이미 삽입 되었거나 경우 삽입 된 행을 업데이트 하 고 있습니다 아직 존재 하지 마십시오.
> 
> [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 다음 코드에서 메서드는 "upsert" 작업을 수행 합니다.
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> 때문에 [시드](https://msdn.microsoft.com/en-us/library/hh829453(v=vs.103).aspx) 모든 마이그레이션을 사용 하 여 메서드 실행, 때문에 추가 하려고 하는 행 이미 있는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 데이터를 삽입할 수 없습니다. "[upsert](http://en.wikipedia.org/wiki/Upsert)" 작업이 이미 존재 하는 행을 삽입 하려고 할 경우 수행 하는 오류를 방지할 수 있지만 응용 프로그램을 테스트 하는 동안 실행 한 데이터 변경 내용 보다 우선 합니다. 테스트 테이블의에서 데이터 일부 원하지 않을 수 있습니다이 위해서는: 경우에 따라 테스트 하는 동안 데이터를 변경 하면 원하는 변경 내용을 데이터베이스 업데이트 후 하 게 유지 합니다. 조건부 삽입 작업을 수행 하려는 경우: 존재 하지 않는 경우에 행을 삽입 합니다.   
>   
> 에 전달 된 첫 번째 매개 변수는 [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드 행 이미 존재 하는지 확인 하는 데 속성을 지정 합니다. 제공 하는 테스트 동영상 데이터에는 `Title` 속성 각 타이틀 목록에는 고유 하므로이 용도로 사용할 수 있습니다.
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> 이 코드에서는 titiles는 고유한 것을 가정 합니다. 중복 된 제목에 수동으로 추가한 경우에 마이그레이션을 수행 하는 다음에 다음과 같은 예외를 얻을 수 있습니다.   
>   
>  *시퀀스에 요소가 둘 이상*  
>   
> 에 대 한 자세한 내용은 [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드를 참조 [EF 4.3 AddOrUpdate 메서드로 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)...


**CTRL-SHIFT-B를 눌러 프로젝트를 빌드합니다.** (다음 단계 못합니다이 시점에서 작성 하지 않아도 됩니다.)

다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다. 이 마이그레이션은 만듭니다 바로 이러한 이유로 하는 새 데이터베이스를 삭제 하면는 *movie.mdf* 파일을 이전 단계에서 합니다.

에 **패키지 관리자 콘솔** 창에서 명령을 입력 `add-migration Initial` 초기 마이그레이션 만들려고 합니다. 이름은 "초기"는 임의로 지정 하며 만든 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다.

![](adding-a-new-field/_static/image6.png)

Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션* 폴더 (이름의 *{날짜 스탬프}\_Initial.cs* ),이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다. 마이그레이션 filename 미리 타임 스탬프가 순서 지정에 도움이 되도록 고정 됩니다. 검사는 *{날짜 스탬프}\_Initial.cs* 파일을 만드는 지침이 포함 된 `Movies` 영화 DB에 대 한 테이블입니다. 이 아래 지침에 설명 된 데이터베이스를 업데이트 하는 경우 *{날짜 스탬프}\_Initial.cs* 파일은 실행 된 후 DB 스키마를 만듭니다. 그런 다음 **시드** DB 테스트 데이터로 채우는 메서드가 실행 됩니다.

에 **패키지 관리자 콘솔**, 명령을 입력 `update-database` 데이터베이스를 만들고 실행 하는 `Seed` 메서드.

![](adding-a-new-field/_static/image7.png)

테이블이 이미 존재 하며 만들 수를 나타내는 오류가 발생할 경우 때문일 것 데이터베이스 삭제 되 고 실행 하기 전에 응용 프로그램을 실행 `update-database`합니다. 이 경우 삭제 된 *Movies.mdf* 파일을 다시 시도 `update-database` 명령입니다. 오류가 여전히 발생 하면 migrations 폴더 및 내용을 삭제 한 다음이 페이지의 위쪽에 대 한 지침이 포함 된 시작 (삭제 되 고 *Movies.mdf* 파일 Enable-migrations를 진행 합니다). 함을 여전히 발생 하면 SQL Server 개체 탐색기를 열고 목록에서 데이터베이스를 제거 합니다.

응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다. 시드 데이터가 표시 됩니다.

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>영화 모델에 등급 속성 추가

추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다. 열기는 *Models\Movie.cs* 파일을 추가 `Rating` 다음과 같은 속성:

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

전체 `Movie` 다음 코드 처럼 이제 보이는 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

(Ctrl + Shift + B) 응용 프로그램을 빌드하십시오.

새 필드를 추가 했으므로 때문에 `Movie` 클래스도 업데이트 해야 바인딩 *허용 목록을* 하므로이 새로운 속성이 포함 됩니다. 업데이트는 `bind` 특성 `Create` 및 `Edit` 포함 하도록 동작 메서드는 `Rating` 속성:

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

브라우저 보기에서 새 `Rating` 속성을 표시, 작성 및 편집하기 위해 보기 템플릿도 업데이트해야 합니다.

열기는 *\Views\Movies\Index.cshtml* 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤의 **가격** 열입니다. 다음 추가 `<td>` 열을 렌더링 하는 서식 파일의 끝 부분에서 `@item.Rating` 값입니다. 다음은 이러한 어떤 업데이트 된 *Index.cshtml* 보기 템플릿은 보입니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

을 열고는 *\Views\Movies\Create.cshtml* 파일을 추가 `Rating` 다음 highlighed 태그로 필드입니다. 이 렌더링 하는 텍스트 상자가 새 동영상 만들어질 때에 대 한 등급을 지정할 수 있습니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

새 지원 하기 위해 응용 프로그램 코드를 지금 업데이트 한 `Rating` 속성입니다.

응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다. 이 작업을 수행 하지만 표시 다음 오류 중 하나:

![](adding-a-new-field/_static/image9.png)  
  
'MovieDBContext' 컨텍스트를 백업 하는 모델 데이터베이스를 만든 후에 변경 되었습니다. Code First 마이그레이션을 사용 하 여 (https://go.microsoft.com/fwlink/?LinkId=238269) 데이터베이스를 업데이트 하는 것이 좋습니다.

![](adding-a-new-field/_static/image10.png)

때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다르면 이제는 `Movie` 기존 데이터베이스의 테이블입니다. (데이터베이스 테이블에 `Rating` 열이 없습니다.)


오류를 해결하는 몇 가지 방법이 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 방법은 테스트 데이터베이스에서 활발한 개발을 수행할 때 개발 주기의 초기 단계에서 매우 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다. 데이터베이스의 기존 데이터 손실의 단점은 하지만입니다-하므로 있습니다 *하지 않는* 는 프로덕션 데이터베이스에서이 방법을 사용! 응용 프로그램을 개발 하는 효율적인 방법으로 방식은를 자동으로 테스트 데이터로 데이터베이스를 시드하는 이니셜라이저를 사용 합니다. Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC/엔터티 프레임 워크 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터를 유지한다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.
3. Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.


이 자습서의 경우 Code First 마이그레이션을 사용합니다.

Seed 메서드를 업데이트 하는 새 열에 대 한 값을 제공 합니다. Migrations\Configuration.cs 파일을 열고 각 영화 개체에 Rating 필드를 추가 합니다.

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

솔루션을 작성 한 다음 엽니다는 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.

`add-migration Rating`

`add-migration` 명령 마이그레이션 프레임 워크에 현재 영화 DB 스키마와 현재 영화 모델을 점검 하 여 DB 새 모델을 마이그레이션하는 데 필요한 코드를 만들 지시 합니다. 이름을 *등급* 은 임의로 지정 하 고 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다. 마이그레이션 단계에 대 한 의미 있는 이름을 사용 하는 것이 좋습니다.

Visual Studio 새 정의 하는 클래스 파일을 엽니다이 명령이 완료 되 면 `DbMigration` 파생 클래스를 및는 `Up` 메서드 새 열을 만드는 코드를 볼 수 있습니다.

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

솔루션을 작성 한 다음 입력 된 `update-database` 명령에 **패키지 관리자 콘솔** 창.

다음 이미지는 출력에 표시는 **패키지 관리자 콘솔** 창 (날짜 스탬프 앞 *등급* 다릅니다.)

![](adding-a-new-field/_static/image11.png)

응용 프로그램을 다시 실행 하 고 /Movies URL로 이동 합니다. 새 등급 필드를 볼 수 있습니다.

![](adding-a-new-field/_static/image12.png)

클릭는 **새로 만들기** 새 동영상을 추가 하는 링크입니다. 참고에 대 한 등급을 추가할 수 있습니다.

![7_CreateRioII](adding-a-new-field/_static/image13.png)

**만들기**를 클릭합니다. 등급을 포함 하 여 새 동영상은 이제 나열 영화에서 표시:

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

이제 프로젝트 마이그레이션을 사용 하는 새 필드를 추가 하거나 그렇지 않으면 스키마를 업데이트할 때 데이터베이스를 삭제할 필요가 없습니다. 다음 섹션에서 더 많은 스키마 변경을 알아보고 마이그레이션을 사용 하 여 데이터베이스를 업데이트 하겠습니다.

도 추가 해야는 `Rating` 필드 템플릿 보기 편집, 정보 및 삭제를 합니다.

"update-database" 명령을 입력할 수는 **패키지 관리자 콘솔** 창을 다시 및 마이그레이션 코드가 없는 실행 스키마 모델 일치 하기 때문에 있습니다. 그러나 실행 됩니다 "데이터베이스 업데이트"를 실행 중인는 `Seed` 메서드를 다시, 초기값에 데이터를 변경한 경우 변경 내용이 손실 됩니다 때문에 `Seed` 메서드 upserts 데이터. 에 대 한 자세한 내용은 `Seed` 인기 있는 Tom Dykstra에서 메서드 [ASP.NET MVC/엔터티 프레임 워크 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.

이 섹션에서는 모델 개체를 수정할 데이터베이스의 변경 내용과 동기화 된 상태로 유지 하는 방법을 표시 합니다. 또한 시나리오를 체험할 수 있도록 샘플 데이터로 새로 만든된 데이터베이스를 채우는 하는 방법을 배웠습니다. 이 한 간단한 소개 Code First를 참조 하십시오. [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 주체에 대 한 자세한 자습서에 대 한 합니다. 다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 해야 할 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.

>[!div class="step-by-step"]
[이전](adding-search.md)
[다음](adding-validation.md)
