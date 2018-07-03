---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: Entity Framework (VB)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 Microsoft Entity Framework를 사용 하 여 ASP.NET MVC를 사용 하는 방법을 알아봅니다. ADO.NET 엔터티 데이터를 만들려는 엔터티 마법사를 사용 하는 방법에 알아봅니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: efb8d7206cba2fd5d8db1817d57a4e2813cb5ace
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377190"
---
<a name="creating-model-classes-with-the-entity-framework-vb"></a>Entity Framework (VB)를 사용 하 여 모델 클래스 만들기
====================
[Microsoft](https://github.com/microsoft)

> 이 자습서에서는 Microsoft Entity Framework를 사용 하 여 ASP.NET MVC를 사용 하는 방법을 알아봅니다. ADO.NET 엔터티 데이터 모델을 만들려면 엔터티 마법사를 사용 하는 방법을 알아봅니다. 이 자습서의이 코스를 통해 선택, 삽입, 업데이트 및 Entity Framework를 사용 하 여 데이터베이스 데이터를 삭제 하는 방법을 보여 주는 웹 응용 프로그램을 빌드합니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램을 빌드할 때에 Microsoft Entity Framework를 사용 하 여 데이터 액세스 클래스를 만드는 방법을 설명 합니다. 이 자습서에서는 Microsoft Entity Framework의 이전 알지를 가정합니다. 이 자습서를 마치면 선택, 삽입, 업데이트 하려면 Entity Framework를 사용 하 여 데이터베이스 레코드를 삭제 하는 방법을 이해할 수 있습니다.

Microsoft Entity Framework는 개체 관계형 매핑 (O/RM) 도구는 데이터베이스에서 데이터 액세스 계층을 자동으로 생성할 수 있습니다. Entity Framework를 사용 하면 데이터 액세스 클래스를 직접 작성의 지루한 작업을 피할 수 있습니다.

> [!NOTE] 
> 
> ASP.NET MVC와 Microsoft Entity Framework 간의 필수 연결이 없습니다. ASP.NET MVC를 사용 하 여 사용할 수 있는 Entity Framework에 여러 가지 대안이 있습니다. 예를 들어 Microsoft LINQ to SQL, NHibernate 등 이나 SubSonic 등의 다른 O/RM 도구를 사용 하 여 MVC 모델 클래스를 빌드할 수 있습니다.


ASP.NET MVC를 사용 하 여 Microsoft Entity Framework를 사용 하는 방법을 보여 주기를 위해 간단한 샘플 응용 프로그램을 빌드 해 보겠습니다. 표시 하 고 영화 데이터베이스 레코드를 편집할 수 있는 영화 데이터베이스 응용 프로그램을 만듭니다.

이 자습서에서는 Visual Studio 2008 또는 Visual Web Developer 2008 서비스 팩 1을 사용 하 여 있다고 가정 합니다. Entity Framework를 사용 하려면 서비스 팩 1 해야 합니다. 다음 주소에서 Visual Studio 2008 서비스 팩 1 또는 서비스 팩 1을 사용 하 여 Visual Web Developer를 다운로드할 수 있습니다.

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)


## <a name="creating-the-movie-sample-database"></a>동영상 샘플 데이터베이스 만들기

영화 데이터베이스 응용 프로그램에서는 영화 라는 다음 열이 포함 된 데이터베이스 테이블을 사용 합니다.

| 열 이름 | 데이터 형식 | Null 허용 하 시겠습니까? | 기본 키가? |
| --- | --- | --- | --- |
| ID | int | False | True |
| 제목 | nvarchar(100) | False | False |
| 책임자 | nvarchar(100) | False | False |

다음이 단계를 수행 하 여 ASP.NET MVC 프로젝트에이 테이블을 추가할 수 있습니다.

1. 앱을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목입니다.**
2. **새 항목 추가** 대화 상자에서 **SQL Server 데이터베이스**이름을 데이터베이스 MoviesDB.mdf를 클릭 합니다 **추가** 단추입니다.
3. 서버 탐색기/데이터베이스 탐색기 창을 열려면 MoviesDB.mdf 파일을 두 번 클릭 합니다.
4. MoviesDB.mdf 데이터베이스 연결을 확장 하 고, 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.
5. 테이블 디자이너에서 Id, 제목 및 Director 열을 추가 합니다.
6. 클릭 합니다 **저장** 단추 (플로피의 아이콘에 포함) 이름 영화를 사용 하 여 새 테이블을 저장 합니다.

영화 데이터베이스 테이블을 만든 후에 테이블에 일부 샘플 데이터를 추가 해야 합니다. 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다. 표시 되는 모눈에 가짜 영화 데이터를 입력할 수 있습니다.

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델 만들기

Entity Framework를 사용 하려면 엔터티 데이터 모델을 만들려고 해야 합니다. Visual studio 이용할 수 있습니다 *엔터티 데이터 모델 마법사* 자동으로 데이터베이스에서 엔터티 데이터 모델을 생성 합니다.

아래 단계를 수행합니다.

1. 솔루션 탐색기 창에서 Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 새 항목**합니다.
2. 에 **새 항목 추가** 대화 상자에서 데이터 범주를 선택 (그림 1 참조).
3. 선택 합니다 **ADO.NET 엔터티 데이터 모델** 템플릿 이름을 엔터티 데이터 모델 MoviesDBModel.edmx을 클릭 합니다 **추가** 단추입니다. 클릭 하는 **추가** 단추는 데이터 모델 마법사를 시작 합니다.
4. 에 **Model 콘텐츠 선택** 단계를 선택는 **데이터베이스에서 생성** 옵션을 클릭 합니다 **다음** 단추 (그림 2 참조).
5. 에 **데이터 연결 선택** 단계, MoviesDB.mdf 데이터베이스 연결을 선택 하 고, 엔터티 연결 설정 MoviesDBEntities, 이름 및 클릭을 입력 합니다 **다음** 단추 (그림 3 참조).
6. **데이터베이스 개체 선택** 단계, 영화 데이터베이스 테이블을 선택 하 고 클릭 합니다 **마침** 단추 (그림 4 참조).

다음이 단계를 완료 한 후 ADO.NET 엔터티 데이터 모델 디자이너 (Entity Designer)가 열립니다.

**그림 1-새 엔터티 데이터 모델 만들기**

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

**그림 2 – 모델 내용을 단계 선택**

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

**그림 3 – 데이터 연결 선택**

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

**그림 4-데이터베이스 개체 선택**

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델을 수정합니다.

엔터티 데이터 모델을 만든 후 Entity Designer를 활용 하 여 모델을 수정할 수 있습니다 (그림 5 참조). 솔루션 탐색기 창 내에서 Models 폴더에 포함 된 MoviesDBModel.edmx 파일을 두 번 클릭 하 여 언제 든 지 Entity Designer를 열 수 있습니다.

**그림 5-ADO.NET 엔터티 데이터 모델 디자이너**

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

예를 들어, 엔터티 데이터 모델 마법사에서 생성 하는 클래스의 이름을 변경 하는 엔터티 디자이너를 사용할 수 있습니다. 마법사는 영화 라는 새 데이터 액세스 클래스를 만들었습니다. 즉, 마법사를 데이터베이스 테이블과 동일한 이름을 클래스를 제공합니다. 특정 영화 인스턴스를 나타내는 데이 클래스를 사용할 것, 이므로 Movies에서 클래스 영화를 바꾸어야 합니다.

엔터티 클래스를 바꾸려는 경우 Entity Designer에서 클래스 이름을 두 번 클릭 하 고 새 이름을 입력 수 있습니다 (그림 6 참조). 또는 Entity Designer에서 엔터티를 선택한 후 속성 창에서 엔터티의 이름을 변경할 수 있습니다.

**그림 6 – 엔터티 이름 변경**

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

저장 단추 (플로피 디스크 아이콘)를 클릭 하 여 수정 작업을 수행한 후에 엔터티 데이터 모델을 저장 해야 합니다. 내부적으로 Entity Designer는 Visual Basic.NET 클래스 집합을 생성합니다. 솔루션 탐색기 창에서 MoviesDBModel.Designer.vb 파일을 열어 이러한 클래스를 볼 수 있습니다.


변경 내용을 덮어씁니다 다음에 Entity Designer를 사용 하므로.designer.vb 파일의 코드를 수정 하지 마세요. .Designer.vb 파일에 정의 된 엔터티 클래스의 기능을 확장 하려는 경우 만들 수 있습니다 *partial 클래스* 를 별도 파일입니다.


#### <a name="selecting-database-records-with-the-entity-framework"></a>Entity Framework 사용 하 여 데이터베이스 레코드를 선택합니다.

영화 레코드 목록을 표시 하는 페이지를 만들어 영화 데이터베이스 응용 프로그램을 작성을 시작 해 보겠습니다. 목록 1에서 Home 컨트롤러 index () 라는 작업을 표시 합니다. Index () 작업을 모두 반환 영화 레코드의 영화 데이터베이스 테이블에서 Entity Framework를 활용 합니다.

**1 – Controllers\HomeController.vb 나열**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

목록 1에서 컨트롤러 생성자에 포함 되어 있는지 확인 합니다. 생성자는 초기화 라는 클래스 수준 필드 \_db입니다. \_db Microsoft Entity Framework에서 생성 된 데이터베이스 엔터티를 나타냅니다. \_db 필드는 Entity Designer에서 생성 된 MoviesDBEntities 클래스의 인스턴스입니다.

\_db 필드는 영화 데이터베이스 테이블에서 레코드를 검색에 index () 작업 내에서 사용 합니다. 식 \_db입니다. MovieSet 영화 데이터베이스 테이블에서 모든 레코드를 나타냅니다. Tolist () 메서드는 영화 집합이 Movie 개체의 제네릭 컬렉션 변환 데: 목록 (Of Movie).

영화 레코드는 LINQ to Entities 사용 하 여 검색 됩니다. Index () 작업 목록 1에서 LINQ를 사용 하 여 *메서드 구문을* 데이터베이스 레코드 집합을 검색 하 합니다. 원한다 면 LINQ를 사용할 수 있습니다 *쿼리 구문을* 대신 합니다. 다음 두 문은 똑같은 작업을 수행:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

가장 직관적인 있는 어떤 LINQ 구문을 메서드 구문 또는 쿼리 구문을 사용 합니다. 두 가지 방법 간의 성능에 차이가 – 유일한 차이점은 스타일입니다.

영화 레코드를 표시 하려면 보기 목록 2에 사용 됩니다.

**Listing 2 – Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

목록 2에서 뷰에 **각각에 대해** 각 영화 레코드를 반복 하 고 영화 레코드의 Title 및 디렉터 속성의 값을 표시 하는 루프입니다. 각 레코드 옆의 편집 및 삭제 링크를 표시 되는지 확인 합니다. 보기의 맨 아래에 동영상 추가 링크를 표시 하는 또한 (그림 7 참조).

**그림 7-인덱스 보기**

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

인덱스 뷰를 *뷰를 입력 한*합니다. 인덱스 보기에는 &lt;% @ 페이지 %&gt; Inherits 특성을 포함 하는 지시문입니다. Inherits 특성에는 강력한 형식의 제네릭 목록 개체의 컬렉션 영화 – 목록 (Of Movie) ViewData.Model 속성을 캐스팅합니다.

## <a name="inserting-database-records-with-the-entity-framework"></a>Entity Framework 사용 하 여 데이터베이스 레코드를 삽입합니다.

데이터베이스 테이블에 새 레코드를 삽입할 수 있도록 하려면 Entity Framework를 사용할 수 있습니다. 코드 3 영화 데이터베이스 테이블에 새 레코드를 삽입 하는 데 사용할 수 있는 홈 컨트롤러 클래스에 추가 하는 두 가지 새 작업을 포함 합니다.

**3 – Controllers\HomeController.vb (추가 메서드)를 나열합니다.**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

첫 번째 add () 작업에는 단순히 보기를 반환합니다. 보기에 새 영화 데이터베이스를 추가 하기 위한 양식이 있습니다 (그림 8 참조)를 기록 합니다. 폼을 제출 하는 경우 두 번째 add () 작업을 호출 됩니다.

두 번째 add () 작업 AcceptVerbs 특성으로 데코 레이트 된 있는지 확인 합니다. HTTP POST 작업을 수행 하는 경우에이 작업을 호출할 수 있습니다. 즉,이 작업 에서만 호출할 수는 HTML 폼 게시 하는 경우.

두 번째 add () 작업을 ASP.NET MVC TryUpdateModel() 메서드를 사용 하 여 Entity Framework 영화 클래스의 새 인스턴스를 만듭니다. TryUpdateModel() 메서드 add () 메서드에 전달 된 FormCollection 필드 하며 영화 클래스에 이러한 HTML 폼 필드의 값을 할당 합니다.


Entity Framework를 사용 하는 경우 UpdateModel 또는 tryupdatemodel에 전달 방법을 사용 하 여 엔터티 클래스의 속성을 업데이트 하는 경우 "white" 속성의 목록을 제공 해야 합니다.


그런 다음 add () 작업을 몇 가지 간단한 양식 유효성 검사를 수행합니다. 작업 제목 및 Director 속성 값이 있다고을 확인 합니다. 유효성 검사 오류가 있으면 유효성 검사 오류 메시지를 ModelState에 추가 됩니다.

유효성 검사 오류가 없을 경우 새 동영상 레코드는 엔터티 프레임 워크를 활용 하 여 영화 데이터베이스 테이블에 추가 됩니다. 새 레코드는 다음 두 줄의 코드를 사용 하 여 데이터베이스에 추가 됩니다.

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

코드의 첫 번째 줄 Entity Framework에 의해 추적 되 고 영화 집합에 새 영화 엔터티를 추가 합니다. 두 번째 코드 줄을 기본 데이터베이스에 다시 추적 되 고 영화를 무엇이 든 변경 사항이 저장 합니다.

**그림 8 – 추가 보기**

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a>Entity Framework를 사용 하 여 데이터베이스 레코드를 업데이트 하는 중

사용 했던만 새 데이터베이스 레코드를 삽입 하는 접근 방식으로 Entity Framework를 사용 하 여 데이터베이스 레코드를 편집 하려면 거의 동일한 방식을 따를 수 있습니다. 코드 4 되 라는 두 개의 새 컨트롤러 작업을 포함 되어 있습니다. 첫 번째 작업에서는 되는 영화 레코드 편집에 대 한 HTML 폼을 반환 합니다. 두 번째 되 작업 데이터베이스를 업데이트 하려고 합니다.

**4-Controllers\HomeController.vb (편집 메서드)를 나열합니다.**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

두 번째 되 작업을 편집 하 고 영화 Id와 일치 하는 데이터베이스에서 동영상 레코드를 검색 하 여 시작 합니다. 다음 LINQ to Entities 문 특정 Id와 일치 하는 첫 번째 데이터베이스 레코드를 가져와:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

다음으로, TryUpdateModel() 메서드는 HTML 폼 필드의 값을 영화 엔터티의 속성에 할당할 사용 됩니다. 허용 목록을 정확 하 게 업데이트할 속성을 지정 하려면 제공 되는 알 수 있습니다.

다음으로 영화 제목과 Director 속성 값에 있는지 확인 하려면 몇 가지 간단한 유효성 검사가 수행 됩니다. 속성 중 하나는 값이 없으면 유효성 검사 오류 메시지를 ModelState에 추가 되 고 ModelState.IsValid 값 false를 반환 하는 것입니다.

마지막으로 유효성 검사 오류가 없을 경우 다음 기본 영화 데이터베이스 테이블은 업데이트 변경 내용으로 savechanges () 메서드를 호출 하 여.

데이터베이스 레코드를 편집할 때 데이터베이스 업데이트를 수행 하는 컨트롤러 작업에 편집 중인 레코드의 Id를 전달 해야 합니다. 이 고, 그렇지 컨트롤러 작업 알 수 없습니다는 기본 데이터베이스에서 업데이트를 기록 합니다. 목록 5에 포함 된 편집 뷰를 편집 하 고 데이터베이스 레코드의 Id를 나타내는 숨겨진된 폼 필드를 포함 합니다.

**Listing 5 – Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Entity Framework 사용 하 여 데이터베이스 레코드를 삭제합니다.

이 자습서에서 해결 해야을 최종 데이터베이스 작업에는 데이터베이스 레코드 삭제 중입니다. 특정 데이터베이스 레코드를 삭제 하려면 목록 6에서 컨트롤러 작업을 사용할 수 있습니다.

**코드 6-\Controllers\HomeController.vb (삭제 작업)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

먼저 delete () 작업 Id와 일치 하는 엔터티 작업에 전달 된 영화를 검색 합니다. 다음으로 영화 DeleteObject() 메서드 뒤에 savechanges () 메서드를 호출 하 여 데이터베이스에서 삭제 됩니다. 마지막으로, 사용자가 인덱스 보기로 다시 리디렉션됩니다.

## <a name="summary"></a>요약

이 자습서의 목적은 ASP.NET MVC 및 Microsoft Entity Framework를 활용 하 여 데이터베이스 기반 웹 응용 프로그램을 구축 하는 방법을 설명 하는 것 이었습니다. 선택, 삽입, 업데이트 할 수 있는 응용 프로그램을 빌드하고 데이터베이스 레코드를 삭제 하는 방법을 알아보았습니다.

먼저 Visual Studio 내에서 엔터티 데이터 모델을 생성 하는 엔터티 데이터 모델 마법사를 사용할 수는 방법을 설명 합니다. 다음으로, LINQ to Entities 사용 하 여 데이터베이스 테이블에서 데이터베이스 레코드 집합을 검색 하는 방법에 알아봅니다. 마지막으로, 삽입, 업데이트 및 데이터베이스 레코드를 삭제 하려면 Entity Framework을 사용 했습니다.

> [!div class="step-by-step"]
> [이전](validation-with-the-data-annotation-validators-cs.md)
> [다음](creating-model-classes-with-linq-to-sql-vb.md)
