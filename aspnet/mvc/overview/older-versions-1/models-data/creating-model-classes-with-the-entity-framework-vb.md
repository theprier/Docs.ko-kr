---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: Entity Framework (VB)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 Microsoft Entity Framework와 함께 ASP.NET MVC를 사용 하는 방법에 설명 합니다. ADO.NET 엔터티 Da 만들기 엔터티 마법사를 사용 하는 방법을 알아봅니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: 3442435c7b2b9ce2ce6bd016ba74fe671eb76f62
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-model-classes-with-the-entity-framework-vb"></a>Entity Framework (VB)를 사용 하 여 모델 클래스 만들기
====================
by [Microsoft](https://github.com/microsoft)

> 이 자습서에서는 Microsoft Entity Framework와 함께 ASP.NET MVC를 사용 하는 방법에 설명 합니다. ADO.NET 엔터티 데이터 모델을 만들려는 엔터티 마법사를 사용 하는 방법을 배웁니다. 이 자습서의 과정 동안 선택, 삽입, 업데이트 및 Entity Framework를 사용 하 여 데이터베이스 데이터를 삭제 하는 방법을 설명 하는 웹 응용 프로그램을 만들었습니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램을 빌드할 때 Microsoft Entity Framework를 사용 하 여 데이터 액세스 클래스를 만드는 방법을 설명 하는입니다. 이 자습서에서는 Microsoft Entity Framework의 이전 알지를 가정합니다. 이 자습서를 마치면 하 여 선택, 삽입, 업데이트, Entity Framework를 사용 하 여 데이터베이스 레코드를 삭제 하는 방법을 알아야 합니다.

Microsoft Entity Framework는 데이터베이스에서 데이터 액세스 계층을 자동으로 생성할 수 있도록 하는 개체 관계형 매핑 (O/RM) 도구입니다. Entity Framework를 사용 하면 데이터 액세스 클래스를 직접 작성 지루한 작업을 피할 수 있습니다.

> [!NOTE] 
> 
> ASP.NET MVC와 Microsoft Entity Framework 사이의 필수 연결이 없습니다. ASP.NET MVC와 함께 사용할 수 있는 Entity Framework에 대 한 대안 여러 가지가 있습니다. 예를 들어 Microsoft LINQ to SQL, NHibernate 또는 subsonic은 이러한 방식을 등의 다른 O/RM 도구를 사용 하 여 MVC 모델 클래스를 빌드할 수 있습니다.


를 ASP.NET MVC와 함께 Microsoft Entity Framework를 사용 하는 방법을 보여 주기 위해 간단한 샘플 응용 프로그램을 빌드합니다. 표시 하 고 동영상 데이터베이스 레코드를 편집할 수 있는 동영상 데이터베이스 응용 프로그램을 만들겠습니다.

이 자습서는 Visual Studio 2008 또는 Visual Web Developer 2008 서비스 팩 1 있다고 가정 합니다. Entity Framework를 사용 하려면 서비스 팩 1 필요 합니다. 다음 주소에서 Visual Studio 2008 서비스 팩 1 또는 서비스 팩 1 Visual Web Developer를 다운로드할 수 있습니다.

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)


## <a name="creating-the-movie-sample-database"></a>영화 샘플 데이터베이스 만들기

다음 열이 포함 된 동영상 라는 데이터베이스 테이블을 사용 하는 영화 데이터베이스 응용 프로그램:

| 열 이름 | 데이터 형식 | Null 허용 하 시겠습니까? | 기본 키가? |
| --- | --- | --- | --- |
| ID | int | False | True |
| 제목 | nvarchar(100) | False | False |
| 감독 | nvarchar(100) | False | False |

다음이 단계를 수행 하 여 ASP.NET MVC 프로젝트에이 테이블을 추가할 수 있습니다.

1. 응용 프로그램을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목입니다.**
2. **새 항목 추가** 대화 상자에서 **SQL Server 데이터베이스**, 이름을 MoviesDB.mdf, 데이터베이스를 지정 하 고 클릭는 **추가** 단추입니다.
3. 서버 탐색기/데이터베이스 탐색기 창을 열려면 MoviesDB.mdf 파일을 두 번 클릭 합니다.
4. MoviesDB.mdf 데이터베이스 연결 확장 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.
5. 테이블 디자이너에서 Id, 제목 및 감독 열을 추가 합니다.
6. 클릭는 **저장** 단추 (플로피의 아이콘에 포함)는 이름 동영상 새 테이블을 저장 하 합니다.

영화 데이터베이스 테이블을 만든 후에 테이블에 몇 가지 샘플 데이터를 추가 해야 합니다. 영화 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다. 표시 되는 표 형태에 가짜 동영상 데이터를 입력할 수 있습니다.

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델 만들기

Entity Framework를 사용 하려면 엔터티 데이터 모델을 만드는 필요 합니다. Visual Studio의 이용할 수 있습니다 *엔터티 데이터 모델 마법사* 데이터베이스에서 엔터티 데이터 모델을 자동으로 생성할 수 있습니다.

아래 단계를 수행합니다.

1. 솔루션 탐색기 창에 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 새 항목**합니다.
2. 에 **새 항목 추가** 대화 상자에서 데이터 범주를 선택 (그림 1 참조).
3. 선택 된 **ADO.NET 엔터티 데이터 모델** 템플릿을 엔터티 데이터 모델 MoviesDBModel.edmx, name을 지정 하 고 클릭는 **추가** 단추입니다. 클릭 하 고 **추가** 단추는 데이터 모델 마법사를 시작 합니다.
4. 에 **모델 콘텐츠 선택** 단계, 선택는 **는 데이터베이스에서 생성** 옵션의 **다음** 단추 (그림 2 참조).
5. 에 **데이터 연결 선택** 단계 MoviesDB.mdf 데이터베이스 연결을 엔터티 연결 설정 MoviesDBEntities, 이름을 지정 하 고 클릭 하 여 입력의 **다음** 단추 (그림 3 참조).
6. 에 **데이터베이스 개체 선택** 단계 영화 데이터베이스 테이블을 선택 하 고 클릭는 **마침** 단추 (그림 4 참조).

다음이 단계를 완료 한 후 ADO.NET 엔터티 데이터 모델 디자이너 (Entity Designer)가 열립니다.

**그림 1-새 엔터티 데이터 모델 만들기**

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

**그림 2 – 모델 내용을 단계를 선택 합니다.**

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

**그림 3 – 데이터 연결 선택**

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

**그림 4-데이터베이스 개체 선택**

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델 수정

엔터티 데이터 모델을 만든 후 엔터티 디자이너의 사용 하 여 모델을 수정할 수 있습니다 (그림 5 참조). 솔루션 탐색기 창 내에서 모델 폴더에 포함 된 MoviesDBModel.edmx 파일을 두 번 클릭 하 여 언제 든 지 엔터티 디자이너를 열 수 있습니다.

**그림 5 – ADO.NET 엔터티 데이터 모델 디자이너**

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

예를 들어 엔터티 모델 데이터 마법사에서 생성 하는 클래스의 이름을 변경 하는 Entity Designer를 사용할 수 있습니다. 마법사가 영화 라는 새 데이터 액세스 클래스를 만들었습니다. 즉, 마법사는 데이터베이스 테이블 이름이 매우 같은 클래스를 제공합니다. 이 클래스를 나타내는 특정 영화 인스턴스를 사용 합니다, 때문에 동영상에 대 한 동영상 클래스를 바꾼 해야 합니다.

엔터티 디자이너에서 클래스 이름을 두 번 클릭 하 고 새 이름을 입력할 수 엔터티 클래스 이름을 변경 하려는 경우 (그림 6 참조). 또는 엔터티 디자이너의 엔터티를 선택한 후 속성 창에서 엔터티의 이름을 변경할 수 있습니다.

**그림 6 – 엔터티 이름 변경**

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

후 저장 단추 (플로피 디스크 아이콘)를 클릭 하 여 수정 하 여 엔터티 데이터 모델을 저장 해야 합니다. 내부적으로 엔터티 디자이너의 Visual Basic.NET 클래스 집합을 생성합니다. 솔루션 탐색기 창에서 MoviesDBModel.Designer.vb 파일을 열어 이러한 클래스를 볼 수 있습니다.


다음에 Entity Designer를 사용 하 여 변경 내용을 덮어쓰게 됩니다 이후.designer.vb 파일의 코드를 수정 하지 마십시오. 경우.designer.vb 파일에 정의 된 엔터티 클래스의 기능을 확장 하려면 다음 만들 수 있습니다 *partial 클래스* 를 별도 파일입니다.


#### <a name="selecting-database-records-with-the-entity-framework"></a>Entity Framework와 함께 데이터베이스 레코드 선택

영화 레코드의 목록을 표시 하는 페이지를 만들어 영화 데이터베이스 응용 프로그램 작성을 시작 하겠습니다. Home 컨트롤러 목록 1의 index () 라는 동작을 노출 합니다. Index () 작업 모두 반환 영화 레코드 영화 데이터베이스 테이블에서 엔터티 프레임 워크를 활용 합니다.

**Listing 1 – Controllers\HomeController.vb**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

목록 1의 컨트롤러는 생성자를 포함 하는 것을 확인 합니다. 생성자 이라는 클래스 수준 필드를 초기화 합니다. \_db입니다. \_db 필드 Microsoft Entity Framework에 의해 생성 된 데이터베이스 엔터티를 나타냅니다. \_db 필드는 Entity Designer에서 생성 된 MoviesDBEntities 클래스의 인스턴스입니다.

\_db 필드는 index () 작업 내에서 영화 데이터베이스 테이블에서 레코드를 검색 하는 데 사용 됩니다. 식 \_db입니다. MovieSet 영화 데이터베이스 테이블에서 모든 레코드를 나타냅니다. 영화 집합이 영화 개체의 제네릭 컬렉션으로 변환 하 고 tolist () 메서드를 사용 하는: 목록 (의 동영상).

영화 레코드는 LINQ to Entities 사용 하 여 검색 됩니다. 목록 1의 index () 동작 LINQ를 사용 하 여 *메서드 구문을* 데이터베이스 레코드 집합을 검색할 수 있습니다. 원하는 경우 LINQ를 사용할 수 있습니다 *쿼리 구문을* 대신 합니다. 다음 두 문이 매우 동일한 작업을 수행 합니다.

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

가장 편리할 나오든 이들 LINQ 구문을 메서드 구문 또는 쿼리 구문을 사용 합니다. 두 방법 간의 성능에 차이가 – 유일한 차이점은 스타일입니다.

영화 레코드를 표시 하려면 보기 목록 2에 사용 됩니다.

**Listing 2 – Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

보기 목록 2에 포함 한 **각** 각 영화 레코드를 반복 하 고 동영상 레코드의 제목 및 감독 속성의 값을 표시 하는 루프입니다. 편집 및 삭제 링크 각 레코드 옆에 표시 되는지 확인 합니다. 동영상 추가 링크 보기의 아래쪽에 표시 되는 또한 (그림 7 참조).

**그림 7-인덱스 뷰**

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

인덱스 뷰는 한 *보기를 입력 한*합니다. 인덱스 보기에는 &lt;% 페이지 % @&gt; Inherits 특성이 포함 된 지시문입니다. Inherits 특성 ViewData.Model 속성 강력한 형식의 제네릭 목록 개체의 컬렉션 영화 – 목록 (의 동영상)을 캐스팅합니다.

## <a name="inserting-database-records-with-the-entity-framework"></a>Entity Framework와 함께 데이터베이스 레코드를 삽입합니다.

쉽게 데이터베이스 테이블에 새 레코드를 삽입할 수 있도록 Entity Framework를 사용할 수 있습니다. 코드 3 영화 데이터베이스 테이블에 새 레코드를 삽입 하는 데 사용할 수 있는 홈 컨트롤러 클래스에 추가 하는 두 개의 새 작업이 포함 되어 있습니다.

**3 – Controllers\HomeController.vb (추가 메서드)를 나열합니다.**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

첫 번째 add () 작업 보기를 반환합니다. 뷰에 새 동영상 데이터베이스 추가 대 한 양식이 있습니다 (그림 8 참조)를 기록 합니다. 폼을 제출 하는 경우 두 번째 add () 동작 호출 됩니다.

두 번째 add () 동작 AcceptVerbs 특성으로 데코레이팅되 어 있는지를 확인 합니다. HTTP POST 작업을 수행 하는 경우에이 작업을 호출할 수 있습니다. 즉,이 작업은 HTML 폼을 게시할 때만 호출할 수 있습니다.

두 번째 add () 동작 ASP.NET MVC TryUpdateModel() 메서드를 사용 하 여 Entity Framework 영화 클래스의 새 인스턴스를 만듭니다. TryUpdateModel() 메서드 add () 메서드에 전달 된 FormCollection의 필드 하며 영화 클래스에 이러한 HTML 폼 필드의 값을 할당 합니다.


Entity Framework를 사용할 때는 TryUpdateModel 또는 UpdateModel 메서드를 사용 하 여 엔터티 클래스의 속성을 업데이트 하는 경우 "white" 속성의 목록이 제공 해야 합니다.


다음으로, add () 작업 몇 가지 간단한 형태 유효성 검사를 수행합니다. 작업 제목 및 감독 속성에 값을 확인 합니다. 유효성 검사 오류가 있으면 유효성 검사 오류 메시지는 ModelState에 추가 됩니다.

유효성 검사 오류가 없는 경우 새 동영상 레코드는 Entity Framework를 사용 하 여 영화 데이터베이스 테이블에 추가 됩니다. 다음 두 줄의 코드를 사용 하 여 데이터베이스에 새 레코드가 추가 됩니다.

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

첫 번째 코드 줄 Entity Framework에 의해 추적 되 고 영화 집합에 새 동영상 엔터티를 추가 합니다. 기본 데이터베이스에 다시 추적 되 고 동영상에 변경 내용이 적용 된 두 번째 코드 줄에 저장 합니다.

**그림 8 – 추가 보기**

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a>Entity Framework와 함께 데이터베이스 레코드를 업데이트합니다.

거의 사용 했던 방금 새 데이터베이스 레코드를 삽입 하는 방법으로 Entity Framework와 함께 데이터베이스 레코드를 편집 하려면 동일한 방법을 따를 수 있습니다. 목록 4 Edit() 라는 두 개의 새 컨트롤러 작업을 포함 합니다. 첫 번째 Edit() 동작이 영화 레코드 편집에 대 한 HTML 폼을 반환 합니다. 두 번째 Edit() 동작 데이터베이스를 업데이트 하려고 합니다.

**4 – Controllers\HomeController.vb (편집 메서드)를 나열합니다.**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

두 번째 Edit() 동작 편집 중인 동영상의 Id와 일치 하는 데이터베이스에서 영화 레코드를 검색 하 여 시작 합니다. 다음 LINQ to Entities 문은 특정 Id와 일치 하는 첫 번째 데이터베이스 레코드를 가져와:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

다음으로, TryUpdateModel() 메서드 영화 엔터티 속성에 HTML 양식 필드의 값을 할당할 사용 됩니다. 허용 목록을 정확한 업데이트할 속성을 지정 하려면 제공 됨을 확인 합니다.

다음으로 영화 제목 및 감독 속성에 값을 확인 하려면 몇 가지 간단한 유효성 검사가 수행 됩니다. 두 속성 중 하나는 값이 없으면 유효성 검사 오류 메시지를 ModelState에 추가 되 고 ModelState.IsValid 값 false를 반환 하는 것입니다.

마지막으로 유효성 검사 오류가 있을 경우 다음 기본 영화 데이터베이스 테이블 업데이트 됩니다 변경으로 savechanges () 메서드를 호출 하 여.

데이터베이스 레코드를 편집할 때 데이터베이스 업데이트를 수행 하는 컨트롤러 동작을 편집 하 고 레코드의 Id를 전달 해야 합니다. 그렇지 않으면 컨트롤러 작업은 기본 데이터베이스에서 업데이트할 레코드 알지 합니다. 목록 5에 포함 된 편집 보기, 편집 하 고 데이터베이스 레코드의 Id를 나타내는 숨겨진된 양식 필드를 포함 합니다.

**Listing 5 – Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Entity Framework와 함께 데이터베이스 레코드를 삭제합니다.

이므로이 자습서에서 해결할 필요가 최종 데이터베이스 작업은 데이터베이스 레코드를 삭제 합니다. 특정 데이터베이스 레코드를 삭제할 컨트롤러 동작 목록 6에 사용할 수 있습니다.

**6-나열 \Controllers\HomeController.vb (삭제 작업)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

먼저 delete () 동작 Id와 일치 하는 엔터티 작업에 전달 된 영화를 검색 합니다. 다음으로 영화 뒤에 savechanges () 메서드에 의해 DeleteObject() 메서드를 호출 하 여 데이터베이스에서 삭제 됩니다. 마지막으로, 사용자가 인덱스 보기로 다시 리디렉션됩니다.

## <a name="summary"></a>요약

이 자습서의 목적은 Microsoft Entity Framework 및 ASP.NET MVC의 이용 하 여 데이터베이스 기반 웹 응용 프로그램을 구축 하는 방법을 보여 주기 위한 것 이었습니다. 선택, 삽입, 업데이트를 사용 하면 응용 프로그램을 빌드하고 데이터베이스 레코드를 삭제 하는 방법을 배웠습니다.

첫째, 엔터티 데이터 모델 마법사를 사용 하 여 Visual Studio 내에서 엔터티 데이터 모델을 생성 하는 방법을 설명 합니다. 다음으로 LINQ to Entities 사용 하 여 데이터베이스 테이블에서 데이터베이스 레코드의 집합을 검색 하는 방법을 배웁니다. 마지막으로 삽입, 업데이트 및 데이터베이스 레코드를 삭제 하는 Entity Framework을 사용 했습니다.

> [!div class="step-by-step"]
> [이전](validation-with-the-data-annotation-validators-cs.md)
> [다음](creating-model-classes-with-linq-to-sql-vb.md)
