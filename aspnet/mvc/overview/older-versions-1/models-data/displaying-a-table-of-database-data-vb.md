---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 데이터베이스 데이터 (VB)의 테이블 표시 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 데이터베이스 레코드 집합을 표시 하는 두 가지 방법에 살펴보겠습니다. 서식 지정 된 HTML에서 데이터베이스 레코드 집합 데이터는 두 가지 방법을 알아보겠습니다...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: d96f574c9284ab259b8733b3b8109ecd0b689aa8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828201"
---
<a name="displaying-a-table-of-database-data-vb"></a>데이터베이스 데이터 (VB)의 테이블 표시
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> 이 자습서에서는 데이터베이스 레코드 집합을 표시 하는 두 가지 방법에 살펴보겠습니다. HTML 표에 데이터베이스 레코드 집합 서식 지정 하는 두 가지 방법을 보여 줍니다. 먼저 뷰 내에서 직접 데이터베이스 레코드 서식을 지정할 수 있습니다 하는 방법을 보여 줍니다. 다음으로, 데이터베이스 레코드의 형식을 지정할 때 부분 활용을 걸릴 수 있습니다 하는 방법에 대해 살펴보겠습니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터의 HTML 테이블을 표시 하는 방법을 설명 합니다. 먼저 Visual Studio에 포함 된 스 캐 폴딩 도구를 사용 하 여 레코드 집합을 자동으로 표시 하는 보기를 생성 하는 방법에 알아봅니다. 다음으로, 데이터베이스 레코드의 형식을 지정할 때 템플릿으로 부분을 사용 하는 방법에 알아봅니다.

## <a name="create-the-model-classes"></a>모델 클래스 만들기

영화 데이터베이스 테이블에서 레코드 집합을 표시 하려고 합니다. 영화 데이터베이스 테이블에는 다음 열을 포함 합니다.

<a id="0.4_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | Int | False |
| 제목 | Nvarchar(200) | False |
| 책임자 | Nvarchar (50) | False |
| DateReleased | DateTime | False |


ASP.NET MVC 응용 프로그램의 영화 테이블을 나타내기 위해 모델 클래스를 만드는 해야 합니다. 이 자습서에서는 모델 클래스를 만들려면 Microsoft Entity Framework를 사용 했습니다.

> [!NOTE] 
> 
> 이 자습서에서는 Microsoft Entity Framework 사용합니다. 그러나 LINQ to SQL, NHibernate, 또는 ADO.NET을 포함 하 여 ASP.NET MVC 응용 프로그램에서 데이터베이스와 상호 작용 하는 다양 한 기술을 사용할 수 있는 알아야 할 것입니다.


엔터티 데이터 모델 마법사를 시작 하려면 다음이 단계를 수행 합니다.

1. 메뉴 옵션을 선택 하 고 솔루션 탐색기 창에서 Models 폴더를 마우스 오른쪽 단추로 클릭 **추가, 새 항목**합니다.
2. 선택 된 **데이터** 범주를 선택 합니다 **ADO.NET 엔터티 데이터 모델** 템플릿.
3. 데이터 모델의 이름을 *MoviesDBModel.edmx* 을 클릭 합니다 **추가** 단추입니다.

추가 단추를 클릭 하면 엔터티 데이터 모델 마법사 나타납니다 (그림 1 참조). 마법사를 완료 하려면 다음이 단계를 수행 합니다.

1. 에 **Model 콘텐츠 선택** 단계를 선택 합니다 **데이터베이스에서 생성** 옵션입니다.
2. 에 **데이터 연결 선택** 단계를 사용 하 여 합니다 *MoviesDB.mdf* 데이터 연결 및 이름 *MoviesDBEntities* 연결 설정 합니다. 클릭 합니다 **다음** 단추입니다.
3. 에 **데이터베이스 개체 선택** 단계, 테이블 노드를 확장 한 다음 동영상 테이블을 선택 합니다. 네임 스페이스를 입력 *모델* 을 클릭 합니다 **마침** 단추입니다.


[![LINQ to SQL 클래스 만들기](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**그림 01**: LINQ to SQL 클래스 만들기 ([큰 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image2.png))


엔터티 데이터 모델 마법사를 완료 한 후 엔터티 데이터 모델 디자이너가 열립니다. 디자이너에는 영화 엔터티 표시 됩니다 (그림 2 참조).


[![엔터티 데이터 모델 디자이너](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**그림 02**:은 엔터티 데이터 모델 디자이너 ([큰 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image4.png))


계속 하기 전에 하나의 변경 해야 합니다. 엔터티 데이터 마법사 라는 모델 클래스를 생성 *영화* 영화 데이터베이스 테이블을 나타내는입니다. 클래스의 이름을 수정 하려면 먼저 특정 영화를 나타내는 영화 클래스를 사용 해야, 하므로 *영화* of *영화* (단일 아니라 복수).

디자이너 화면의 클래스의 이름을 두 번 클릭 하 고 영화 Movies에서 클래스의 이름을 변경 하십시오. 이렇게 변경한 후 다음을 클릭 합니다 **저장** 단추 (플로피 디스크 아이콘) 동영상 클래스를 생성 합니다.

## <a name="create-the-movies-controller"></a>영화 컨트롤러 만들기

데이터베이스 레코드를 표현 하는 수단을 만들었으므로 이제 해당 동영상의 컬렉션을 반환 하는 컨트롤러를 만들 수 있습니다. Visual Studio 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 컨트롤러** (그림 3 참조).


[![메뉴 컨트롤러 추가](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**그림 03**: 컨트롤러 메뉴 추가 ([큰 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image6.png))


경우는 **컨트롤러 추가** MovieController 컨트롤러 이름 입력 대화 상자가 나타납니다 (그림 4 참조). 클릭 합니다 **추가** 단추를 새 컨트롤러를 추가 합니다.


[![컨트롤러 추가 대화 상자](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**그림 04**: 컨트롤러 추가 대화 상자 ([큰 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image8.png))


데이터베이스 레코드 집합이 반환 되도록 영화 컨트롤러에 의해 노출 index () 작업을 수정 해야 합니다. 목록 1에서 컨트롤러 같이 컨트롤러를 수정 합니다.

**1 – Controllers\MovieController.vb 나열**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

목록 1에서 MoviesDBEntities 클래스 MoviesDB 데이터베이스를 나타내는 데 사용 됩니다. 식 *엔터티. MovieSet.ToList()* 영화 데이터베이스 테이블에서 모든 동영상의 집합을 반환 합니다.

## <a name="create-the-view"></a>보기 만들기

HTML 표에 데이터베이스 레코드 집합을 표시 하는 가장 쉬운 방법은 Visual Studio에서 제공 하는 스 캐 폴딩을 활용 하는 경우

메뉴 옵션을 선택 하 여 응용 프로그램을 빌드합니다 **빌드, 솔루션 빌드**합니다. 열기 전에 응용 프로그램을 작성 해야 합니다 **뷰 추가** 대화 상자 또는 데이터 클래스 대화 상자에 나타나지 않습니다.

Index () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 5 참조).


[![뷰 추가](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**그림 05**: 뷰 추가 ([큰 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image10.png))


에 **뷰 추가** 대화 상자에서 레이블이 지정 된 확인란 **강력한 형식의 뷰를 만들**합니다. 영화 클래스를 선택 합니다 **데이터 클래스 보기**합니다. 선택 *목록을* 으로 **콘텐츠를 볼** (그림 6 참조). 이러한 옵션을 선택 하는 동영상 목록을 표시 하는 강력한 형식의 뷰를 생성 합니다.


[![뷰 추가 대화 상자](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**그림 06**: 뷰 추가 대화 상자 ([큰 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image12.png))


클릭 한 후 합니다 **추가** 단추, 목록 2에서 보기를 자동으로 생성 됩니다. 이 뷰는 동영상 컬렉션을 반복 하 고 각 동영상의 속성을 표시 하는 데 필요한 코드를 포함 합니다.

**Listing 2 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

메뉴 옵션을 선택 하 여 응용 프로그램을 실행할 수 있습니다 **디버그, 디버깅 시작** (또는 F5 키를 눌러). Internet Explorer를 시작 응용 프로그램을 실행 합니다. 그런 다음 /Movie URL로 이동 그림 7에서 페이지를 볼 수 있습니다.


[![동영상 테이블](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**그림 07**: 영화 테이블 ([큰 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image14.png))


그림 7에서 데이터베이스 레코드의 눈금의 모양에 대 한 아무 것도 마음에 들지 않는 경우 다음 수정할 수 있습니다 단순히 인덱스 보기. 예를 들어, 변경할 수 있습니다 합니다 *DateReleased* 헤더 *릴리스 날짜* 인덱스 뷰를 수정 하 여 합니다.

## <a name="create-a-template-with-a-partial"></a>부분을 사용 하 여 서식 파일 만들기

뷰를 너무 복잡해 때 부분으로 분할 하는 보기를 시작 하는 것이 좋습니다. 부분을 사용 하면 보기 쉽게 이해 하 고 유지 관리할 수 있습니다. 부분을 만들어 보겠습니다 각 영화 데이터베이스 레코드 형식을 지정 하는 템플릿으로 사용할 수 있습니다.

부분을 만들려면 다음이 단계를 수행 합니다.

1. Views\Movie 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가**합니다.
2. 레이블이 지정 된 확인란 *(.ascx) 부분 보기를 만드는*합니다.
3. 부분 이름을 *MovieTemplate*합니다.
4. 레이블이 지정 된 확인란 **강력한 형식의 뷰를 만들**합니다.
5. 영화를 선택 합니다 *데이터 클래스 보기*합니다.
6. 빈으로 선택 합니다 *콘텐츠 보기*합니다.
7. 클릭 합니다 **추가** 단추 부분을 프로젝트에 추가 합니다.

다음이 단계를 완료 한 후에 목록 3 처럼 보이는 부분 MovieTemplate 수정 합니다.

**3 – Views\Movie\MovieTemplate.ascx 나열**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

보기 3의 부분 레코드의 단일 행에 대 한 템플릿을 포함합니다.

수정 된 인덱스 뷰 목록 4 부분 MovieTemplate를 사용합니다.

**Listing 4 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

목록 4에서 뷰에 For 동영상의 모든 반복 하는 각 루프입니다. 각 영화에 대 한 부분 MovieTemplate 동영상 서식을 지정 하는 데 사용 됩니다. MovieTemplate RenderPartial() 도우미 메서드를 호출 하 여 렌더링 됩니다.

수정한 인덱스 뷰는 데이터베이스 레코드의 동일한 HTML 테이블을 렌더링합니다. 그러나 뷰를 크게 간소화 되었습니다.


RenderPartial() 메서드는 문자열을 반환 하지 않으므로 대부분의 다른 도우미 메서드는 다릅니다. 사용 하 여 RenderPartial() 메서드를 호출 해야 하므로 &lt;%Html.RenderPartial()&gt; of &lt;% = Html.RenderPartial() %&gt;합니다.


## <a name="summary"></a>요약

이 자습서의 목표는 HTML 테이블의 데이터베이스 레코드 집합을 표시 하는 방법을 설명 하는 것 이었습니다. 먼저 Microsoft Entity Framework를 활용 하 여 컨트롤러 작업에서 데이터베이스 레코드 집합을 반환 하는 방법을 알아보았습니다. 다음으로 Visual Studio 스 캐 폴딩을 사용 하 여 항목의 컬렉션을 자동으로 표시 하는 보기를 생성 하는 방법을 알아보았습니다. 마지막으로, 부분을 활용 하 여 보기를 간소화 하는 방법을 알아보았습니다. 각 데이터베이스 레코드를 서식을 지정할 수 있도록 부분을 템플릿으로 사용 하는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [이전](creating-model-classes-with-linq-to-sql-vb.md)
> [다음](performing-simple-validation-vb.md)
