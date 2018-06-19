---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4 부: 모델 및 데이터 액세스 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 4 부에서는 모델 및 데이터 액세스에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 76671bbc7050d111b4d156c45584ba5aa4f1ea8f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879480"
---
<a name="part-4-models-and-data-access"></a>4 부: 모델 및 데이터 액세스
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.
> 
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 4 부에서는 모델 및 데이터 액세스에 설명 합니다.


"지금까지 म 했습니다 방금 되었습니다 더미 데이터" 우리의 컨트롤러에서를 전달 우리의 템플릿 보기. 이제 실제 데이터베이스 연결 준비가 되었습니다. 이 자습서에서는 데이터베이스 엔진으로 SQL Server Compact Edition (SQL CE 라고도 함)를 사용 하는 방법을 포함 합니다. SQL CE는 무료 이며, 포함 된 파일 기반 데이터베이스를 설치 및 구성 하므로 불편 로컬 개발에 대 한 필요 하지 않습니다.

## <a name="database-access-with-entity-framework-code-first"></a>데이터베이스 액세스와 Entity Framework 코드 중심

쿼리 및 데이터베이스를 업데이트 하도록 ASP.NET MVC 3 프로젝트에 포함 된 Entity Framework (EF) 지원을 사용 합니다. EF는 유연한 개체 관계형 매핑 (ORM) 데이터 개발자가 개체 지향 방식으로 데이터베이스에 저장 된 데이터를 쿼리하고 업데이트할 수 있는 API.

Entity Framework 버전 4 라는 코드 중심 개발 패러다임을 지원 합니다. 코드 중심 간단한 클래스 라고도 POCO ("old" CLR 개체에서)를 작성 하 여 모델 개체를 만들 수 있습니다 및를 사용 하 여 클래스에도 데이터베이스를 만들 수 있습니다.

### <a name="changes-to-our-model-classes"></a>모델 클래스에 대 한 변경

Entity Framework에서 데이터베이스 만들기 기능이이 자습서에서는 활용 수 됩니다 했습니다. 그 전에 하지만 만들어 보겠습니다 몇 가지 사소한 변경 내용을 나중에 사용할 예정 일부의 원인에 추가할 모델 클래스.

#### <a name="adding-the-artist-model-classes"></a>아티스트 모델 클래스를 추가합니다.

아티스트를 설명 하는 간단한 모델 클래스 추가 되므로 우리의 앨범 아티스트와 연결 됩니다. 아래 표시 된 코드를 사용 하 여 Artist.cs 라는 모델 폴더에 새 클래스를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>모델 클래스를 업데이트합니다.

아래와 같이 앨범 클래스를 업데이트 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

다음으로 장르 클래스에 다음 업데이트를 확인 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-appdata-folder"></a>앱 추가\_데이터 폴더

앱 추가\_우리의 SQL Server Express 데이터베이스 파일을 저장 하는 프로젝트에 데이터 디렉터리입니다. 응용 프로그램\_데이터에 대 한 데이터베이스 액세스에 대 한 올바른 보안 액세스 권한을 이미 ASP.NET에서 특별 한 디렉터리입니다. 프로젝트 메뉴에서 선택한 ASP.NET 폴더 추가 다음 앱\_데이터입니다.

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>Web.config 파일에서 연결 문자열 만들기

Entity Framework 데이터베이스에 연결 하는 방법을 알 수 있도록 웹 사이트의 구성 파일에 몇 줄만 추가 합니다. 프로젝트의 루트에 있는 Web.config 파일을 두 번 클릭 합니다.

![](mvc-music-store-part-4/_static/image2.png)

이 파일의 아래쪽으로 스크롤하여 추가 &lt;connectionStrings&gt; 다음과 같이 마지막 줄 바로 위에 섹션.

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>컨텍스트 클래스를 추가합니다.

모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 MusicStoreEntities.cs 라는 새 클래스를 추가 합니다.

![](mvc-music-store-part-4/_static/image3.png)

이 클래스는 Entity Framework 데이터베이스 컨텍스트를 나타내는 및 됩니다 우리의 만들기 처리, 읽기, 업데이트, 및 삭제 작업을 수행해 줍니다. 이 클래스에 대 한 코드는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

이제 끝났습니다-없는 다른 구성, 특수 인터페이스 등이 있습니다. DbContext 기본 클래스를 확장 하 여 MusicStoreEntities 클래스가 우리의 데이터베이스 작업을 수행해 줍니다를 처리할 수 있습니다. 연결 하는 작업을 두었습니다 이제 몇 가지 더 많은 속성 데이터베이스에는 추가 정보 중 일부를 활용 하려면 모델 클래스를 추가 해 보겠습니다.

### <a name="adding-our-store-catalog-data"></a>스토어 카탈로그 데이터를 추가합니다.

"Seed" 데이터는 새로 만든된 데이터베이스를 추가 하는 Entity Framework에는 기능을 해당 메뉴로 이동 합니다. 이 스토어 카탈로그를 장르, 아티스트 및 앨범 목록이 미리 채워집니다. 이 자습서의 앞부분에서 사용 되는 사이트 디자인 파일-포함 하는 MvcMusicStore Assets.zip 다운로드가 초기값 데이터로 명명 된 코드 폴더에 있는 클래스 파일을 있습니다.

코드 내에서 / Models 폴더 SampleData.cs 파일을 찾은 다음 아래와 같이 취급 프로젝트에서 Models 폴더에 넣습니다.

![](mvc-music-store-part-4/_static/image4.png)

이제 Entity Framework에 해당 SampleData 클래스에 대 한 정보를 코드 한 줄을 추가 해야 합니다. 열고 응용 프로그램 맨 위에 다음 줄을 추가 하는 프로젝트의 루트에 Global.asax 파일을 두 번 클릭\_메서드를 시작 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

이 시점에서 프로젝트에 대 한 Entity Framework를 구성 하는 데 필요한 작업을 완료 했습니다.

## <a name="querying-the-database"></a>데이터베이스 쿼리

이제 "데이터는 dummy"를 사용 하는 대신 대신 호출 데이터베이스로 넘어가면 모든 정보를 쿼리할 수 있도록 보겠습니다 우리의 StoreController를 업데이트 합니다. 에 필드를 선언 하 여 시작 합니다는 **StoreController** storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 포함 하려면:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>데이터베이스에서 쿼리 저장소 인덱스 업데이트

MusicStoreEntities 클래스는 Entity Framework에 의해 유지 관리 및 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다. 데이터베이스에 모든 장르 검색할 우리의 StoreController 인덱스 동작을 업데이트 해 보겠습니다. 이전에 수행한 것이 문자열 데이터를 하드 코딩 하 여 합니다. 이제 우리 대신 방금 context를 사용할 수 Entity Framework Generes 컬렉션:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

변경 없이 이러한 문제가 발생할 우리의 보기 템플릿에 म 반환 전에-우리는 반환 라이브 데이터 데이터베이스에서 이제 동일한 StoreIndexViewModel 여전히 반환 하는 것 해야 합니다.

프로젝트를 다시 실행 하 고 "/ 저장" URL을 방문 하십시오에서는 모든 장르 목록 데이터베이스에으로 이제 표시 됩니다.

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>라이브 데이터를 사용 하도록 스토어 찾아보기 및 세부 정보 업데이트

/ 저장소/찾아보기로? 장르 =*[일부 장르]* 동작 메서드에 우리는 장르에 대 한 이름을 기준으로 검색 합니다. 두 항목이 동일한 장르 이름에 대 한 적이 서는 안 있으므로 및 사용할 수 있도록 한 결과 라고만 생각는 합니다. 다음과 같이 적절 한 장르 개체에 대 한 쿼리를 LINQ에서 Single() 확장 (입력 하지 않은이 아직):

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

단일 메서드 한다고 단일 장르 개체 이름이 정의 된 값과 일치 되도록 지정 하는 매개 변수로 람다 식을 사용 합니다. 앞의 경우에서 Disco를 일치 하는 이름 값이 있는 단일 장르 개체를 로드 하는 했습니다.

장르 개체를 검색할 때 로드도 원하는 다른 관련된 엔터티를 나타낼 수 있도록 하는 Entity Framework 기능을 이동 합니다. 이 기능은 쿼리 결과 셰이핑 라고 하 고 모든 필요한 정보를 검색 하는 데이터베이스에 액세스 해야 하는 횟수를 줄일 수 있습니다. 하므로 쿼리를 나타내는 관련된 앨범도 한다고 Genres.Include("Albums")에서 포함할를 업데이트 하는 장르, 검색에 대 한 앨범을 사전 인출 하려고 합니다. 단일 데이터베이스 요청에서이 Genre 및 앨범 데이터를 검색 하므로 보다 효율적입니다.

방해가 설명 같습니다 우리의 업데이트 된 찾아보기 컨트롤러 동작 표시 하는 방법.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

이제 각 장르의 사용할 수 있는 앨범을 표시 하려면 저장소 찾아보기 보기를 업데이트할 수 있습니다. 보기 템플릿 (에 /Views/Store/Browse.cshtml)를 열고 아래와 같이 글머리 기호 목록이 앨범을 추가 합니다.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

응용 프로그램을 실행 하 고 탐색/저장소/찾아보기 하? 장르 = 우리의 선택한 장르에 모든 앨범 표시 하는 데이터베이스에서 결과 가져오는 이제 Jazz 표시 합니다.

![](mvc-music-store-part-4/_static/image2.jpg)

म 우리의 /Store/세부 정보 / [id] URL로 변경 하 고이 매개 변수 값과 일치 하는 ID를 가진 앨범을 로드 합니다. 데이터베이스 쿼리를 더미 데이터 바꿉니다 동일 하 게 됩니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

결과 이제 데이터베이스에서 찾아볼 되 고 응용 프로그램을 실행 하 고 /Store/Details/1을 찾아를 보여 줍니다.

![](mvc-music-store-part-4/_static/image5.png)

이제 업데이트 앨범 앨범 ID로 표시 하는 저장소 세부 정보 페이지를 설정 하는 **찾아보기** 자세히 보기에 연결 하는 보기입니다. 이전 섹션의 끝에 저장소 인덱스를 저장소 찾아보기 연결 했던 것 처럼 정확 하 게 Html.ActionLink를 사용 합니다. 브라우저 보기에 대 한 전체 소스 아래에 나타납니다.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

이 스토어 페이지에서 사용할 수 있는 앨범을 나열 하는 장르 페이지로 탐색할 수 이제 및 앨범을 클릭 하 여 해당 앨범에 대 한 정보를 볼 수 있습니다.

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-3.md)
> [다음](mvc-music-store-part-5.md)
