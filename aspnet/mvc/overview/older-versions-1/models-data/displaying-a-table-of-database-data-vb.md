---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 데이터베이스 데이터 (VB)의 테이블 표시 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 I에 데이터베이스 레코드의 집합을 표시 하는 두 가지 방법을 보여 줍니다. 두 가지 방법으로 서식을 html에서 데이터베이스 레코드 집합이 ta 표시...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: dd871520f98aaae2d7b33d83b1646eb9eee88821
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="displaying-a-table-of-database-data-vb"></a>데이터베이스 데이터 (VB)의 테이블 표시
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> 이 자습서에서는 I에 데이터베이스 레코드의 집합을 표시 하는 두 가지 방법을 보여 줍니다. HTML 테이블에 데이터베이스 레코드 집합이 서식 지정 하는 두 가지 방법을 보여 줍니다. 첫째, 보기 내에서 직접 데이터베이스 레코드 서식을 지정할 수는 방법을 보여 줍니다. 다음으로, 있습니다 사용할 수 있는 방법을 부분의 데이터베이스 레코드의 서식을 지정할 때 방법을 보여 줍니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터의 HTML 테이블을 표시 하는 방법을 설명 하는입니다. 첫째, 레코드 집합을 자동으로 표시 하는 보기를 생성 하려면 Visual Studio에 포함 된 스 캐 폴딩 도구를 사용 하는 방법을 배웁니다. 다음으로, 데이터베이스 레코드의 서식을 지정할 때 부분을 템플릿으로 사용 하는 방법을 배웁니다.

## <a name="create-the-model-classes"></a>모델 클래스 만들기

영화 데이터베이스 테이블에서 레코드 집합을 표시 하려면 하겠습니다. 영화 데이터베이스 테이블에는 다음과 같은 열을 포함 되어 있습니다.

<a id="0.4_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | Int | False |
| 제목 | Nvarchar(200) | False |
| 감독 | NVarchar(50) | False |
| DateReleased | DateTime | False |


ASP.NET MVC 응용 프로그램의 영화 테이블을 나타내기 위해 모델 클래스를 만드는 필요 합니다. 이 자습서에서는 사용 하 여 Microsoft Entity Framework 모델 클래스를 만듭니다.

> [!NOTE] 
> 
> 이 자습서에서는 Microsoft Entity Framework를 사용 했습니다. 그러나 되기 LINQ to SQL, NHibernate 또는 ADO.NET을 포함 하 여 ASP.NET MVC 응용 프로그램에서 데이터베이스와 상호 작용할 수의 여러 다른 기술 사용할 수 있는 것을 알아야 합니다.


엔터티 데이터 모델 마법사를 시작 하려면 다음이 단계를 수행 합니다.

1. 솔루션 탐색기 창 및 메뉴 옵션 선택 모델 폴더를 마우스 오른쪽 단추로 클릭 **추가, 새 항목**합니다.
2. 선택 된 **데이터** 범주를 선택은 **ADO.NET 엔터티 데이터 모델** 템플릿.
3. 데이터 모델 이름을 *MoviesDBModel.edmx* 클릭는 **추가** 단추입니다.

추가 단추를 클릭 한 후에 엔터티 데이터 모델 마법사 나타납니다 (그림 1 참조). 마법사를 완료 하려면 다음이 단계를 수행 합니다.

1. 에 **모델 콘텐츠 선택** 선택 단계는 **데이터베이스에서 생성** 옵션입니다.
2. 에 **데이터 연결 선택** 단계를 사용 하 여는 *MoviesDB.mdf* 데이터 연결 및 이름 *MoviesDBEntities* 연결 설정에 대 한 합니다. 클릭는 **다음** 단추입니다.
3. 에 **데이터베이스 개체 선택** 단계, 테이블 노드를 확장 하 고, 영화 테이블을 선택 합니다. 네임 스페이스를 입력 *모델* 클릭는 **마침** 단추입니다.


[![LINQ to SQL 클래스 만들기](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**그림 01**: LINQ to SQL 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image2.png))


엔터티 데이터 모델 마법사를 완료 한 후 엔터티 데이터 모델 디자이너가 열립니다. 디자이너에는 영화 엔터티 표시 됩니다 (그림 2 참조).


[![엔터티 데이터 모델 디자이너](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**그림 02**: The 엔터티 데이터 모델 디자이너 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image4.png))


계속 하기 전에 하나의 변경 내용을 확인 해야 합니다. 라는 모델 클래스를 생성 하는 엔터티 데이터 마법사 *동영상* 영화 데이터베이스 테이블을 나타내는입니다. 영화 클래스 사용 하 여 특정 영화를 나타내는 합니다, 하므로 되려면 클래스의 이름을 수정 해야 *영화* 대신 *영화* (단 수 아님 복수).

디자이너 화면의 클래스 이름을 두 번 클릭 하 고 동영상에서 영화 클래스의 이름을 변경 하십시오. 이 변경 후 클릭는 **저장** 단추 (플로피 디스크 아이콘)를 영화 클래스를 생성 합니다.

## <a name="create-the-movies-controller"></a>영화 컨트롤러 만들기

데이터베이스 레코드를 표시 하는 방법을 설정 했으므로 동영상의 컬렉션을 반환 하는 컨트롤러를 만들 수 있습니다. Visual Studio 솔루션 탐색기 창 내에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 컨트롤러** (그림 3 참조).


[![메뉴 컨트롤러 추가](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**그림 03**: 컨트롤러 메뉴 추가 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image6.png))


경우는 **컨트롤러 추가** MovieController 컨트롤러 이름을 입력 대화 상자가 나타나면 (그림 4 참조). 클릭는 **추가** 단추를 새 컨트롤러를 추가 합니다.


[![컨트롤러 추가 대화 상자](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**그림 04**: 컨트롤러 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image8.png))


데이터베이스 레코드 집합 반환 되도록 영화 컨트롤러에 의해 노출 되는 index () 동작을 수정 해야 합니다. 목록 1의 컨트롤러 모양이 되도록 컨트롤러를 수정 합니다.

**Listing 1 – Controllers\MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

목록 1의 MoviesDBEntities 클래스 MoviesDB 데이터베이스를 나타내는 데 사용 됩니다. 식 *엔터티. MovieSet.ToList()* 영화 데이터베이스 테이블에서 모든 동영상의 집합을 반환 합니다.

## <a name="create-the-view"></a>보기 만들기

HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 가장 쉬운 방법은 Visual Studio에서 제공 하는 스 캐 폴딩 활용 하기 위해 됩니다.

메뉴 옵션을 선택 하 여 응용 프로그램을 빌드하도록 **빌드, 솔루션 빌드**합니다. 열기 전에 응용 프로그램을 작성 해야는 **뷰 추가** 대화 상자 또는 데이터 클래스 대화 상자에 표시 되지 않습니다.

Index () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 5 참조).


[![뷰 추가](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**그림 05**: 뷰 추가 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image10.png))


에 **뷰 추가** 대화 상자에서 확인란 확인 **강력한 형식의 뷰 만들기**합니다. 로 영화 클래스를 선택 하는 **데이터 클래스 보기**합니다. 선택 *목록* 로 **콘텐츠를 볼** (그림 6 참조). 이러한 옵션을 선택 하는 동영상 목록을 표시 하는 강력한 형식의 뷰를 생성 합니다.


[![뷰 추가 대화 상자](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**그림 06**: 뷰 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image12.png))


클릭 한 후의 **추가** 단추, 목록 2에서 보기를 자동으로 생성 됩니다. 이 보기는 동영상 컬렉션을 반복 하 고 각 동영상의 속성을 표시 하는 데 필요한 코드를 포함 합니다.

**Listing 2 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

메뉴 옵션을 선택 하 여 응용 프로그램을 실행할 수 있습니다 **디버그, 디버깅 시작** (또는 F5 키 누르기). Internet Explorer를 시작 응용 프로그램을 실행 합니다. 그런 다음 /Movie URL로 이동 그림 7에 있는 페이지를 볼 수 있습니다.


[![영화 테이블](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**그림 07**: 영화 테이블 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image14.png))


그림 7에 데이터베이스 레코드의 눈금의 모양에 대해 마음에 들지 않는 경우 다음 수정할 수 인덱스 뷰. 예를 들어, 변경할 수는 *DateReleased* 헤더를 *릴리스 날짜* 인덱스 뷰를 수정 하 여 합니다.

## <a name="create-a-template-with-a-partial"></a>Partial 서식 파일 만들기

뷰 너무 복잡해 경우 시작 부분으로 보기를 분리 하는 것이 좋습니다. 사용 하 여 부분 쉽게 보기 이해 하 고 유지 합니다. Partial를 만들 것 각 영화 데이터베이스 레코드의 서식을 지정 하려면는 템플릿으로 사용할 수 있습니다.

부분을 만들려면 다음이 단계를 수행 합니다.

1. Views\Movie 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가**합니다.
2. 확인란 확인 *(.ascx) 부분 뷰를 만들*합니다.
3. Partial 이름을 *MovieTemplate*합니다.
4. 확인란 확인 **강력한 형식의 뷰 만들기**합니다.
5. 동영상으로 선택 된 *데이터 클래스를 볼*합니다.
6. 비어 있지도 선택 된 *콘텐츠를 볼*합니다.
7. 클릭는 **추가** partial 프로젝트에 추가 하려면 단추입니다.

다음이 단계를 완료 한 후 목록 3 모양 MovieTemplate 부분을 수정 합니다.

**3 – Views\Movie\MovieTemplate.ascx 나열**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

보기 3의 부분에는 레코드의 단일 행에 대 한 템플릿을 포함합니다.

수정한 인덱스 뷰 목록 4에 부분 MovieTemplate를 사용합니다.

**Listing 4 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

목록 4에서 뷰에 For 동영상의 모든 반복 하는 각 루프입니다. 각 동영상에 대 한 부분 MovieTemplate 동영상 서식을 지정 하는 데 사용 됩니다. MovieTemplate RenderPartial() 도우미 메서드를 호출 하 여 렌더링 됩니다.

수정한 인덱스 뷰는 데이터베이스 레코드의 매우 같은 HTML 테이블을 렌더링합니다. 그러나 뷰 크게 간소화 되었습니다.


RenderPartial() 메서드는 문자열을 반환 하지 않으므로 대부분의 다른 도우미 메서드는 다릅니다. 사용 하 여 RenderPartial() 메서드를 호출 해야 따라서 &lt;% Html.RenderPartial() %&gt; 대신 &lt;% = Html.RenderPartial() %&gt;합니다.


## <a name="summary"></a>요약

이 자습서의 목표 HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 방법에 대해 설명 하는 것 이었습니다. 첫째, Microsoft Entity Framework을 이용 하 여 컨트롤러 작업에서 데이터베이스 레코드 집합을 반환 하는 방법을 배웠습니다. 다음으로, Visual Studio 스 캐 폴딩을 사용 하 여 항목의 컬렉션을 자동으로 표시 하는 보기를 생성 하는 방법을 배웠습니다. 마지막으로, 부분을 이용 하 여 뷰를 단순화 하는 방법을 배웠습니다. 각 데이터베이스 레코드를 서식을 지정할 수 있도록 템플릿으로 부분을 사용 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](creating-model-classes-with-linq-to-sql-vb.md)
> [다음](performing-simple-validation-vb.md)
