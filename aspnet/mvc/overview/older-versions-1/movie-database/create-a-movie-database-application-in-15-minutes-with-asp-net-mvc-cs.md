---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
title: ASP.NET MVC (C#) 15 분 내에 동영상 데이터베이스 응용 프로그램을 만들 | Microsoft Docs
author: StephenWalther
description: Stephen Walther 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램의 시작 끝나기를 작성 합니다. 이 자습서는 새로운 t 있는 사용자에 게 충분히 소개 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: dd1be137-91c5-47a8-8137-fecf0789c7f5
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
msc.type: authoredcontent
ms.openlocfilehash: 81e0ae42bc3e7656c933ba70920eaeeffa4c4bd6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877036"
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-c"></a>ASP.NET mvc (C#) 15 분 내에 동영상 데이터베이스 응용 프로그램 만들기
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

[코드 다운로드](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_CS.zip)

> Stephen Walther 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램의 시작 끝나기를 작성 합니다. 이 자습서는 ASP.NET MVC 응용 프로그램을 구축 하는 프로세스를 짐작할 배우려는 하 고는 ASP.NET MVC 프레임 워크를 처음 사용에 대 한 훌륭한 소개 합니다.


이 자습서의 목적은 "어떤 것과 같습니다"의 의미를 제공 하는 ASP.NET MVC 응용 프로그램을 빌드합니다. 이 자습서에는 전체 ASP.NET MVC 응용 프로그램 작성 시작에서 완료 하는 데 통해 blast 합니다. I 간단한 데이터베이스 기반 응용 프로그램 목록, 만들기, 하는 방법을 편집 데이터베이스 레코드를 보여 주는 빌드하는 방법을 보여 줍니다.

응용 프로그램을 구축 하는 프로세스를 간소화 하기 위해 Visual Studio 2008의 스 캐 폴딩 기능을 이동 합니다. 초기 코드 및이 컨트롤러, 모델 및 보기에 대 한 콘텐츠를 생성 하는 Visual Studio를 알려드리겠습니다.

Active Server Pages 또는 ASP.NET으로 작업 하는 경우 다음 찾아야 ASP.NET MVC 친숙 하 게 합니다. ASP.NET MVC 뷰는 Active Server Pages 응용 프로그램의 페이지과 매우 유사 합니다. 와 기존의 ASP.NET Web Forms 응용 프로그램과 마찬가지로 ASP.NET MVC를 제공은 다양 한 언어 및.NET framework에서 제공 하는 클래스에 대 한 전체 액세스 합니다.

좋겠습니다는이 자습서를 알려는 방법에 대 ASP.NET MVC 응용 프로그램을 작성 하는 환경을 유사한 및 다른 Active Server Pages 또는 ASP.NET Web Forms 응용 프로그램을 작성 하는 환경을 보다 의미입니다.

## <a name="overview-of-the-movie-database-application"></a>영화 데이터베이스 응용 프로그램의 개요

이러한 목표를 간단 하 게 하므로 매우 간단한 영화 데이터베이스 응용 프로그램을 빌드합니다. 영화 데이터베이스 응용 프로그램에서 세 가지를 수행 하는 것을 수 있습니다.

1. 영화 데이터베이스 레코드 집합 나열
2. 새 동영상 데이터베이스 레코드를 만듭니다
3. 기존 영화 데이터베이스 레코드를 편집 합니다.

다시, 간단 하 게 유지 하고자 하기 때문에 응용 프로그램을 빌드하는 데 필요한 ASP.NET MVC 프레임 워크의 기능의 최소 수의 장점은 이동 합니다. 예를 들어 우리 않습니다 활용 기반 개발 합니다.

응용 프로그램을 만들려면 각 다음 단계를 완료 해야 합니다.

1. ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기
2. 데이터베이스 만들기
3. 데이터베이스 모델 만들기
4. ASP.NET MVC 컨트롤러 만들기
5. ASP.NET MVC 뷰 만들기

## <a name="preliminaries"></a>준비 단계

Visual Studio 2008 또는 Visual Web Developer 2008 Express는 ASP.NET MVC 응용 프로그램을 빌드하는 필요 합니다. ASP.NET MVC 프레임 워크를 다운로드 해야 합니다.

Visual Studio 2008를 소유 하지 않는 경우 Visual Studio 2008의 90 일 평가판이 웹이 사이트에서 다운로드할 수 있습니다.

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

또는 만들 수 있습니다 ASP.NET MVC 응용 프로그램 Visual Web Developer Express 2008을 사용 합니다. Visual Web Developer Express를 사용 하려는 경우 서비스 팩 1을 갖고 있어야 합니다. Visual Web Developer 2008 Express 서비스 팩 1이 웹 사이트에서 다운로드할 수 있습니다.

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

Visual Studio 2008 또는 Visual Web Developer 2008을 설치한 후 ASP.NET MVC 프레임 워크를 설치 해야 합니다. 다음 웹 사이트에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> ASP.NET 프레임 워크 및 ASP.NET MVC 프레임 워크를 개별적으로 다운로드 하는 대신 웹 플랫폼 설치 관리자를 활용할 수 있습니다. 웹 플랫폼 설치 관리자는 설치 된 응용 프로그램을 쉽게 관리할 수 있도록 하는 응용 프로그램은 사용자의 컴퓨터:
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a>ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

Visual Studio 2008에서 새 ASP.NET MVC 웹 응용 프로그램 프로젝트를 만들어 보겠습니다. 메뉴 옵션을 선택 **파일, 새 프로젝트** 그림 1의 새 프로젝트 대화 상자를 볼 수 있습니다. 프로그래밍 언어와 C#을 선택 하 고 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿을 선택 합니다. 프로젝트 이름을 MovieApp를 지정 하 고 확인 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)

**그림 01**:의 새 프로젝트 대화 상자 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))


새 프로젝트 대화 상자 맨 위에 있는 드롭다운 목록에서.NET Framework 3.5를 선택 하거나 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿이 나타나지 있는지 확인 합니다.


새 MVC 웹 응용 프로그램 프로젝트를 만들 때마다 Visual Studio 별도 단위 테스트 프로젝트를 만들 것인지 묻는 메시지를 표시 합니다. 그림 2에 대화 상자가 나타납니다. 이어서 우리가 않습니다 수 만들고 테스트가이 자습서에서는 시간 제약 조건으로 인해 (예,이 대 한 약간 어느 정도 느끼는 해야) 선택은 **아니요** 옵션는 **확인** 단추입니다.

> [!NOTE] 
> 
> Visual Web Developer에서 테스트 프로젝트를 지원 하지 않습니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)

**그림 02**: The 단위 테스트 프로젝트 만들기 대화 상자 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))


ASP.NET MVC 응용 프로그램에 표준 집합이 폴더: 모델, 뷰 및 컨트롤러 폴더입니다. 솔루션 탐색기 창에서 폴더의이 표준 집합을 볼 수 있습니다. 영화 데이터베이스 응용 프로그램을 작성 하기 위해 각 모델, 뷰 및 컨트롤러 폴더에 파일을 추가 해야 합니다.

Visual Studio와 함께 새 MVC 응용 프로그램을 만들 때에 샘플 응용 프로그램을 가져옵니다. 처음부터 다시 시작 하려는 것 이므로이 샘플 응용 프로그램에 대 한 콘텐츠를 삭제 해야 합니다. 다음 파일 및 폴더를 삭제 해야 합니다.

- Controllers\HomeController.cs
- Views\Home

## <a name="creating-the-database"></a>데이터베이스를 만드는 중

영화 데이터베이스 레코드를 보관할 데이터베이스를 만들려는 해야 합니다. 다행히도 Visual Studio 라는 SQL Server Express는 무료 데이터베이스를 포함 합니다. 데이터베이스를 만들려면 다음이 단계를 수행 합니다.

1. 응용 프로그램을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다.
2. 선택 된 **데이터** 범주를 선택은 **SQL Server 데이터베이스** 서식 파일 (그림 3 참조).
3. 새 사용자 데이터베이스 이름을 *MoviesDB.mdf* 클릭는 **추가** 단추입니다.

앱에 있는 MoviesDB.mdf 파일을 두 번 클릭 하 여 데이터베이스에 연결할 수 데이터베이스를 만든 후\_데이터 폴더. MoviesDB.mdf 파일을 두 번 클릭 하면 서버 탐색기 창이 열립니다.

> [!NOTE] 
> 
> 서버 탐색기 창이 Visual Web Developer의 경우 데이터베이스 탐색기 창이 라고 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)

**그림 03**: Microsoft SQL Server 데이터베이스 만들기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))


다음으로 새 데이터베이스 테이블을 만들 필요 합니다. 서버 탐색기 창 내에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다. 이 메뉴 옵션을 선택 하면 데이터베이스 테이블 디자이너를 엽니다. 다음 데이터베이스 열을 만듭니다.

<a id="0.1_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | Int | False |
| 제목 | Nvarchar(100) | False |
| 감독 | Nvarchar(100) | False |
| DateReleased | DateTime | False |


첫 번째 열, Id 열에 두 특수 속성이 있습니다. 먼저, Id 열 기본 키 열으로 표시 해야 합니다. Id 열을 선택한 다음 클릭는 **기본 키 설정** 단추 (이 키를 처럼 생긴 아이콘). 둘째, Id 열을 Id 열으로 표시 해야 할 수도 있습니다. 열 속성 창에서 Id 사양 섹션까지 아래로 스크롤한 다음 확장 합니다. 변경 된 **Id** 속성 값을 **예**합니다. 작업을 완료 하는 경우 테이블 그림 4와 같아야 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)

**그림 04**: The 영화 데이터베이스 테이블 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))


새 테이블을 저장 하는 최종 단계가입니다. 저장 단추 (플로피 아이콘)를 클릭 하 고 새 테이블 이름을 영화를 지정 합니다.

테이블 생성을 완료 한 후 테이블에 일부 영화 레코드를 추가 합니다. 서버 탐색기 창에 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다. (그림 5 참조) 하 여 좋아하는 영화 목록을 입력 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)

**그림 05**: 영화 레코드 입력 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))


## <a name="creating-the-model"></a>모델 만들기

다음 데이터베이스를 표현 하는 클래스 집합을 만들 해야 합니다. 데이터베이스 모델을 만드는 해야 합니다. 예제의 데이터베이스 모델에 대 한 클래스를 자동으로 생성 하기 위해 Microsoft 엔터티 프레임 워크의 장점은 이동 합니다.

> [!NOTE] 
> 
> ASP.NET MVC 프레임 워크는 Microsoft Entity Framework 연결 되지 않습니다. 다양 한 개체 관계형 매핑을 사용 하 여 데이터베이스에 모델 클래스를 만들 수 있습니다 (또는 / M) 도구 LINQ to SQL, subsonic은 이러한 방식을, 및 NHibernate를 포함 합니다.


엔터티 데이터 모델 마법사를 시작 하려면 다음이 단계를 수행 합니다.

1. 솔루션 탐색기 창 및 메뉴 옵션 선택 모델 폴더를 마우스 오른쪽 단추로 클릭 **추가, 새 항목**합니다.
2. 선택 된 **데이터** 범주를 선택은 **ADO.NET 엔터티 데이터 모델** 템플릿.
3. 데이터 모델 이름을 *MoviesDBModel.edmx* 클릭는 **추가** 단추입니다.

추가 단추를 클릭 한 후에 엔터티 데이터 모델 마법사 나타납니다 (그림 6 참조). 마법사를 완료 하려면 다음이 단계를 수행 합니다.

1. 에 **모델 콘텐츠 선택** 선택 단계는 **데이터베이스에서 생성** 옵션입니다.
2. 에 **데이터 연결 선택** 단계를 사용 하 여는 *MoviesDB.mdf* 데이터 연결 및 이름 *MoviesDBEntities* 연결 설정에 대 한 합니다. 클릭는 **다음** 단추입니다.
3. 에 **데이터베이스 개체 선택** 단계, 테이블 노드를 확장 하 고, 영화 테이블을 선택 합니다. 네임 스페이스를 입력 *MovieApp.Models* 클릭는 **마침** 단추입니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)

**그림 06**: 엔터티 데이터 모델 마법사를 사용 하 여 데이터베이스 모델 생성 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))


엔터티 데이터 모델 마법사를 완료 한 후 엔터티 데이터 모델 디자이너가 열립니다. 디자이너는 영화 데이터베이스 테이블에 표시 됩니다 (그림 7 참조).


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)

**그림 07**: The 엔터티 데이터 모델 디자이너 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))


계속 하기 전에 하나의 변경 내용을 확인 해야 합니다. 라는 모델 클래스를 생성 하는 엔터티 데이터 마법사 *동영상* 영화 데이터베이스 테이블을 나타내는입니다. 영화 클래스 사용 하 여 특정 영화를 나타내는 합니다, 하므로 되려면 클래스의 이름을 수정 해야 *영화* 대신 *영화* (단 수 아님 복수).

디자이너 화면의 클래스 이름을 두 번 클릭 하 고 동영상에서 영화 클래스의 이름을 변경 하십시오. 이 변경 후 클릭는 **저장** 단추 (플로피 디스크 아이콘)를 영화 클래스를 생성 합니다.

## <a name="creating-the-aspnet-mvc-controller"></a>ASP.NET MVC 컨트롤러 만들기

다음 단계는 ASP.NET MVC 컨트롤러를 만드는 것입니다. 컨트롤러는 사용자 간의 ASP.NET MVC 응용 프로그램 상호 작용 하는 방식을 제어 하는 일을 담당 합니다.

아래 단계를 수행합니다.

1. 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 컨트롤러**합니다.
2. 컨트롤러 추가 대화 상자에 이름을 입력 *HomeController* 하 고 레이블이 확인란 **만들기, 업데이트 및 세부 정보 시나리오에 대 한 작업 메서드를 추가** (그림 8 참조).
3. 클릭는 **추가** 단추를 프로젝트에 새 컨트롤러를 추가 합니다.

다음이 단계를 완료 한 후 목록 1의 컨트롤러가 만들어집니다. 인덱스 세부 정보, 만들기, 명명 된 메서드에 있음 및 편집. 다음 섹션에서 작동 하도록 이러한 메서드를 얻으려고 하는 데 필요한 코드를 추가 하겠습니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)

**그림 08**: 새 ASP.NET MVC 컨트롤러 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))


**1 – Controllers\HomeController.cs 나열**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample1.cs)]

## <a name="listing-database-records"></a>데이터베이스 레코드 목록

Home 컨트롤러의 index () 메서드는 ASP.NET MVC 응용 프로그램에 대 한 기본 메서드입니다. ASP.NET MVC 응용 프로그램을 실행 하면 index () 메서드는 첫 번째 컨트롤러 메서드를 호출 합니다.

영화 데이터베이스 테이블에서 레코드의 목록을 표시 하는 index () 메서드를 사용 합니다. 데이터베이스의 이점은 index () 메서드와 함께 영화 데이터베이스 레코드를 검색 하려면 앞에서 만든 모델 클래스 이동 합니다.

라는 새 개인 필드가 포함 되도록 코드 2에서 HomeController 클래스를 수정한 후 I \_db입니다. MoviesDBEntities 클래스는 데이터베이스 모델 나타내며이 클래스는 데이터베이스와 통신을 사용 해야 합니다.

또한 목록 2의 index () 메서드를 수정 했습니다. Index () 메서드 MoviesDBEntities 클래스를 사용 하 여 영화 데이터베이스 테이블에서 모든 동영상 레코드를 검색 합니다. 식  *\_db입니다. MovieSet.ToList()* 영화 데이터베이스 테이블에서 모든 동영상 레코드의 목록을 반환 합니다.

영화 목록이 뷰에 전달 됩니다. 데이터 보기와 보기에 전달 되 View() 메서드에 전달 되는 모든 작업이 있습니다.

**2 – Controllers/HomeController.cs (수정 된 인덱스 메서드)를 나열 합니다.**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample2.cs)]

Index () 메서드 라는 인덱스 뷰를 반환 합니다. 영화 데이터베이스 레코드의 목록을 표시 하려면이 보기를 만드는 해야 합니다. 아래 단계를 수행합니다.


프로젝트가 빌드되어야 (메뉴 옵션을 선택 **빌드, 솔루션 빌드**) 열기 전에 **뷰 추가** 없는 클래스 또는 대화 상자에 표시 됩니다는 **데이터 클래스 보기** 드롭다운 목록입니다.


1. 코드 편집기에서 index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 9 참조).
2. 뷰 추가 대화 상자에서 레이블이 지정 된 확인란 확인 **강력한 형식의 뷰 만들기** 을 선택 합니다.
3. **콘텐츠를 볼** 드롭다운 목록에서 값을 선택 *목록*합니다.
4. **데이터 클래스 보기** 드롭다운 목록에서 값을 선택 *MovieApp.Models.Movie*합니다.
5. 새 만들려는 추가 단추를 클릭 (그림 10 참조)를 확인 합니다.

다음이 단계를 완료 한 후 Index.aspx 라는 새 뷰로 Views\Home 폴더에 추가 됩니다. 인덱스 보기의 내용은 보기 3에 포함 됩니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)

**그림 09**: 컨트롤러 동작으로 인해 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)

**그림 10**: 뷰 추가 대화 상자를 사용 하 여 새 보기 만들기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))


**Listing 3 – Views\Home\Index.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample3.aspx)]

인덱스 뷰는 모든 HTML 테이블 내에서 영화 데이터베이스 테이블에서 영화 레코드를 표시합니다. 보기는 ViewData.Model 속성으로 표현 되는 각 동영상을 반복 하는 foreach 루프를 포함 합니다. 그런 다음 F5 키를 클릭 하 여 응용 프로그램을 실행할 그림 11에서 웹 페이지를 볼 수 있습니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)

**그림 11**: The 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))


## <a name="creating-new-database-records"></a>새 데이터베이스 레코드 만들기

이전 섹션에서 만든 인덱스 보기에는 새 데이터베이스 레코드를 만들기 위한 링크가 포함 됩니다. 계속 해 서 논리를 구현 하 고 새 동영상 데이터베이스 레코드를 만드는 데 필요한 보기를 만드는 합니다.

Home 컨트롤러 create ()를 포함 합니다. 첫 번째 create () 메서드 매개 변수가 없습니다. Create () 메서드의이 오버 로드는 새 동영상 데이터베이스 레코드를 만들기 위한 HTML 폼을 표시 하는 데 사용 됩니다.

두 번째 create () 메서드가 FormCollection 매개 변수입니다. Create () 메서드의이 오버 로드는 새 동영상을 만들기 위한 HTML 폼이 서버에 게시 될 때 호출 됩니다. 이 두 번째 create () 메서드는 메서드가 HTTP POST 작업을 수행 하지 않는 한 호출 하지 못하도록 방지 AcceptVerbs 특성이 있는지를 확인 합니다.

이 두 번째 create () 메서드 목록 4에 업데이트 된 HomeController 클래스에서 수정 되었습니다. 새 버전의 create () 메서드 영화 매개 변수를 받아들이고 새 동영상 영화 데이터베이스 테이블에 삽입 하기 위한 논리를 포함 합니다.

> [!NOTE] 
> 
> 바인딩 특성을 확인 합니다. 않기 때문에 HTML 양식 으로부터 영화 Id 속성을 업데이트 하려면,이 속성을 명시적으로 제외 해야 합니다.


**4 – Controllers\HomeController.cs (수정 된 Create 메서드)를 나열 합니다.**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample4.cs)]

Visual Studio에서는 새 동영상 데이터베이스를 만들기 위한 양식을 만드는 쉽게 (그림 12 참조)를 기록 합니다. 아래 단계를 수행합니다.

1. 코드 편집기에서 create () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가**합니다.
2. 레이블이 지정 된 확인란 확인 **강력한 형식의 뷰 만들기** 을 선택 합니다.
3. **콘텐츠를 볼** 드롭다운 목록에서 값을 선택 *만들기*합니다.
4. **데이터 클래스 보기** 드롭다운 목록에서 값을 선택 *MovieApp.Models.Movie*합니다.
5. 클릭는 **추가** 단추를 새 뷰를 만듭니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)

**그림 12**: 만들기 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))


Visual Studio를 자동으로 목록 5에서 뷰를 생성합니다. 이 보기는 각 영화 클래스의 속성에 해당 하는 필드를 포함 하는 HTML 폼을 포함 합니다.

**Listing 5 – Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample5.aspx)]

> [!NOTE] 
> 
> 뷰 추가 대화 상자에서 생성 되는 HTML 형식 Id 양식 필드를 생성 합니다. Id 열이 Id 열 이기 때문에이 양식 필드 필요 하지 않으므로 안전 하 게 제거할 수 있습니다.


만들기 뷰를 추가한 후에 데이터베이스에 새 동영상 레코드를 추가할 수 있습니다. F5 키를 눌러 응용 프로그램을 실행 하 고 그림 13에서 양식을 보려면 새로 만들기 링크를 클릭 합니다. 완료 하 고 양식을 제출 하는 경우 새 동영상 데이터베이스 레코드가 생성 됩니다.

공지 폼 유효성 검사를 자동으로 가져옵니다. 동영상에 대 한 릴리스 날짜를 입력 하는 것을 잊은 하거나을 잘못 된 릴리스 날짜를 입력 하는 경우 폼이 다시 표시 및 릴리스 날짜 필드가 강조 표시 됩니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)

**그림 13**: 새 동영상 데이터베이스 레코드를 만드는 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))


## <a name="editing-existing-database-records"></a>기존 데이터베이스 레코드 편집

이전 섹션을 나열 하 고 새 데이터베이스 레코드를 만들 수 방법을 설명한 합니다. 이 최종 단원에서는 기존 데이터베이스 레코드를 편집할 수는 방법을 설명 합니다.

첫째, 편집 폼을 생성 해야 합니다. Visual Studio에서 편집 폼에 자동으로 생성 하므로이 단계가 쉽습니다. Visual Studio code 편집기에서 HomeController.cs 클래스를 열고이 단계를 수행 합니다.

1. 코드 편집기에서 Edit() 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 14 참조).
2. 확인란 확인 **강력한 형식의 뷰 만들기**합니다.
3. **콘텐츠를 볼** 드롭다운 목록에서 값을 선택 *편집*합니다.
4. **데이터 클래스 보기** 드롭다운 목록에서 값을 선택 *MovieApp.Models.Movie*합니다.
5. 클릭는 **추가** 단추를 새 뷰를 만듭니다.

Views\Home 폴더에 Edit.aspx 라는 새 뷰를 추가 이러한 단계를 완료 합니다. 이 보기는 HTML 폼 영화 레코드 편집을 위해 포함 되어 있습니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)

**그림 14**: 편집 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))


> [!NOTE] 
> 
> 편집 뷰 영화 Id 속성에 해당 하는 HTML 폼 필드를 포함 합니다. Id 속성의 값을 편집 하는 사람을 않도록 하기 때문에이 양식 필드를 제거 해야 합니다.


마지막으로, Home 컨트롤러 데이터베이스 레코드를 편집을 지원 하도록 수정 해야 합니다. 업데이트 된 HomeController 클래스 목록 6에 포함 됩니다.

**6-Controllers\HomeController.cs (편집 메서드)를 나열합니다.**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample6.cs)]

목록 6에서 Edit() 메서드의 두 오버 로드에 추가 논리를 추가 했습니다. 첫 번째 Edit() 메서드는 메서드에 전달 된 Id 매개 변수에 해당 하는 영화 데이터베이스 레코드를 반환 합니다. 두 번째 오버 로드는 데이터베이스에서 영화 레코드에 대 한 업데이트를 수행합니다.

공지 원래 영화를 검색 하 고 다음 데이터베이스의 기존 영화를 업데이트 하려면 ApplyPropertyChanges()를 호출 해야 합니다.

## <a name="summary"></a>요약

이 자습서는 ASP.NET MVC 응용 프로그램 작성 경험의 의미를 제공 하는 것 이었습니다. 검색 된 ASP.NET MVC 웹 응용 프로그램을 빌드하는 Active Server Pages 또는 ASP.NET 응용 프로그램을 작성 하는 환경을 매우 유사 하는 것이 좋겠습니다.

이 자습서에서는 ASP.NET MVC 프레임 워크의 가장 기본적인 기능만 검사 했습니다. 이후 자습서에서 우리 심층적으로 알아보기 컨트롤러, 컨트롤러 작업, 보기, 데이터 보기 및 HTML 도우미와 같은 항목입니다.

> [!div class="step-by-step"]
> [다음](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb.md)
