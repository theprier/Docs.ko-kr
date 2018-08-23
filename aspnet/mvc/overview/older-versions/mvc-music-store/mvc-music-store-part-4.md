---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4 부: 모델 및 데이터 액세스 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 4 부에서는 모델 및 데이터 액세스에 설명 합니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 6a07bf6c8a3fb926ae25fe1f6c9359e64cd7a290
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838790"
---
<a name="part-4-models-and-data-access"></a>4 부: 모델 및 데이터 액세스
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.
> 
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 4 부에서는 모델 및 데이터 액세스에 설명 합니다.


지금 우리 했습니다 되었습니다 전달 하기만 "더미 데이터"는 컨트롤러에서 우리의 보기 템플릿에 합니다. 이제 실제 데이터베이스를 연결할 준비가 되었습니다. 이 자습서는 데이터베이스 엔진으로 SQL Server Compact Edition (SQL CE 라고도 함)를 사용 하는 방법을 다루는 것입니다. SQL CE는 무료, 임베디드, 파일 기반 데이터베이스를 설치 및 구성으로 로컬 개발 매우 편리 하 게 필요 하지 않습니다.

## <a name="database-access-with-entity-framework-code-first"></a>데이터베이스 액세스와 엔터티 프레임 워크 코드 중심

ASP.NET MVC 3 프로젝트를 쿼리하고 데이터베이스 업데이트에 포함 된 EF (Entity Framework) 지원을 사용 하겠습니다. EF는 유연한 개체 관계형 매핑 (ORM) 데이터 개발자를 개체 지향 방식으로 데이터베이스에 저장 된 데이터를 쿼리하고 업데이트 된 API.

Entity Framework 버전 4에는 호출 코드 중심 개발 패러다임을 지원 합니다. 코드 중심 간단한 클래스 라고도 POCO ("plain old CLR object에서)를 작성 하 여 모델 개체를 만들 수 있습니다 및 데이터베이스 클래스에서 즉석에서 만들 수도 있습니다.

### <a name="changes-to-our-model-classes"></a>모델 클래스 변경

것을 활용 하는 Entity Framework에서 데이터베이스 만들기 기능이 자습서에서입니다. 작업을 수행 하기 전에 만들어 보겠습니다 몇 가지만 변경에서 나중에 사용 하는 몇 가지 추가 모델 클래스.

#### <a name="adding-the-artist-model-classes"></a>Artist 모델 클래스 추가

우리의 앨범 아티스트를 설명 하는 간단한 모델 클래스를 추가 해 보겠습니다 아티스트를 사용 하 여 연결 됩니다. 아래 표시 된 코드를 사용 하 여 Artist.cs 모델 폴더에 새 클래스를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>모델 클래스를 업데이트 하는 중

아래와 같이 Album 클래스를 업데이트 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

다음으로, 장르 클래스에 다음 업데이트를 확인 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-appdata-folder"></a>앱 추가\_데이터 폴더

앱 추가\_데이터 디렉터리를 프로젝트는 SQL Server Express 데이터베이스 파일을 저장 합니다. 앱\_데이터가 데이터베이스 액세스에 대 한 올바른 보안 권한이 이미 있는 ASP.NET의 특수 디렉터리입니다. 프로젝트 메뉴에서 선택한 ASP.NET 폴더 추가 앱\_데이터입니다.

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>Web.config 파일에서 연결 문자열 만들기

Entity Framework에는 데이터베이스에 연결 하는 방법을 알 수 있도록 웹 사이트의 구성 파일에 몇 줄을 추가 합니다. 프로젝트의 루트에 있는 Web.config 파일을 두 번 클릭 합니다.

![](mvc-music-store-part-4/_static/image2.png)

이 파일의 아래쪽으로 스크롤하여 추가 된 &lt;connectionStrings&gt; 아래와 같이 마지막 줄 바로 위에 섹션입니다.

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>컨텍스트 클래스 추가

Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 MusicStoreEntities.cs 라는 새 클래스를 추가 합니다.

![](mvc-music-store-part-4/_static/image3.png)

이 클래스는 Entity Framework 데이터베이스 컨텍스트를 나타내는 및는 우리의 만들기를 처리, 읽기, 업데이트 및 삭제 작업을 합니다. 이 클래스에 대 한 코드는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

이것이-없는 다른 구성, 특별 한 인터페이스, 등입니다. DbContext 기본 클래스를 확장 하 여 MusicStoreEntities 클래스는 우리 회사에 데이터베이스 작업을 처리할 수 있습니다. 이제 했으므로 후크 하는, 몇 가지 자세한 속성이 데이터베이스에 일부 추가 정보를 활용 하 여 모델 클래스를 추가 해 보겠습니다.

### <a name="adding-our-store-catalog-data"></a>저장소 카탈로그 데이터를 추가합니다.

"초기값" 데이터는 새로 만든된 데이터베이스를 추가 하는 Entity Framework의 기능 활용을 걸립니다 했습니다. 이 저장소 카탈로그를 장르와 예술가, 앨범의 목록으로 미리 채워집니다. MvcMusicStore Assets.zip 다운로드-이 자습서의 앞부분에서 사용 하 여 사이트 디자인 파일에 포함 된-Code 라는 폴더에 있는이 시드 데이터를 사용 하 여 클래스 파일을 있습니다.

코드 내에서 / Models 폴더 SampleData.cs 파일을 찾아 아래와 같이 프로젝트에서 Models 폴더에 넣습니다.

![](mvc-music-store-part-4/_static/image4.png)

이제 해당 SampleData 클래스에 대 한 Entity Framework를 코드 한 줄을 추가 해야 합니다. 응용 프로그램 맨 위에 다음 줄을 추가 하 고 열어서 프로젝트의 루트에서 Global.asax 파일을 두 번 클릭\_메서드를 시작 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

이 시점에서 프로젝트에 대 한 Entity Framework를 구성 하는 데 필요한 작업을 완료 했습니다.

## <a name="querying-the-database"></a>데이터베이스 쿼리

이제 "더미 데이터"를 사용 하는 대신 대신 호출 모든 해당 정보를 쿼리 하는 데이터베이스에는 StoreController를 업데이트 해 보겠습니다. 에 필드를 선언 하 여 먼저 합니다 **StoreController** storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 보관할:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>데이터베이스에서 쿼리 저장소 인덱스를 업데이트 하는 중

MusicStoreEntities 클래스는 Entity Framework에서 유지 관리 하 고 데이터베이스의 각 테이블에 대해 컬렉션 속성을 노출 합니다. 데이터베이스에서 모든 장르를 검색 하 여 StoreController 인덱스 작업을 업데이트 해 보겠습니다. 이전에 수행한 것이 문자열 데이터를 하드 코딩 합니다. 이제 우리가 대신 방금 컨텍스트를 사용할 수는 Entity Framework Generes 컬렉션:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

변경이 필요 하지 않은 데이터베이스에서 라이브 데이터 이제 반환 방금 전에-반환 하는 것 같은 StoreIndexViewModel 여전히 반환 되므로 보기 템플릿은에 발생 합니다.

프로젝트를 다시 실행 하 고 "/ 저장" url, 데이터베이스에서 모든 장르 목록을 이제 표시 됩니다 했습니다.

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>라이브 데이터를 사용 하려면 저장소 찾아보기 및 세부 정보를 업데이트 합니다.

사용 하 여/저장소/찾아보기? 장르 =*[일부 장르]* 작업 메서드를 검색 하는 장르 이름입니다. 두 항목이 동일한 장르 이름에 대 한 적이 없어야 했습니다 없으므로 사용할 수 있도록 하나의 결과 필요 합니다. LINQ에서 다음과 같은 적절 한 장르 개체에 대 한 쿼리 Single() 확장 (입력 하지이 아직):

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

단일 메서드를 사용 한다고 단일 장르 개체 이름과 정의한 값과 일치 되도록 지정 하는 매개 변수로 람다 식입니다. 위의 예에서 로드 하 고 단일 장르 개체 Disco를 일치 하는 이름 값을 사용 하 여 합니다.

장르 개체를 검색할 때도 로드 하려고 하는 다른 관련된 엔터티를 나타낼 수 있도록 하는 Entity Framework 기능을 알아보겠습니다. 이 기능은 쿼리 결과 셰이핑 하는 데 라고 하며 모든 필요한 정보를 검색 하려면 데이터베이스에 액세스 해야 하는 횟수를 줄일 수 있습니다. 관련된 앨범도 한다고 나타내려면 Genres.Include("Albums")에서 포함 하는 쿼리 업데이트에서는 장르를 검색에 대 한 앨범을 사전 인출 하려고 합니다. 이 단일 데이터베이스 요청에는 장르 및 앨범 데이터를 검색 하는 것 이므로 더 효율적입니다.

를 방해가 설명을 사용 하 여 다음과 같습니다.이 업데이트 된 찾아보기 컨트롤러 동작 표시 하는 방법

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

이제 각 장르에서 사용할 수 있는 앨범을 표시 하려면 저장소 찾아보기 보기를 업데이트할 수 있습니다. 템플릿 보기 (있는 /Views/Store/Browse.cshtml)을 열고 아래와 같이 앨범의 글머리 기호 목록을 추가 합니다.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

응용 프로그램을 실행 하 고 이동/저장소/찾아보기? 장르 = 데이터베이스에는 선택한 장르에 모든 앨범 표시에서 결과 가져오는 이제는 Jazz 보여 줍니다.

![](mvc-music-store-part-4/_static/image2.jpg)

에서는에서는 동일 하 게 ID를 가진 매개 변수 값과 일치 하는 앨범을 로드 하는 데이터베이스 쿼리를 사용 하 여 더미 데이터를 바꾸고 /Store/세부 정보 / [id] URL을 변경 합니다.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

응용 프로그램을 실행 하 고 /Store/Details/1 이동 결과 이제 데이터베이스에서 가져온 콘텐츠만 표시 됩니다.

![](mvc-music-store-part-4/_static/image5.png)

저장소 세부 정보 페이지는 앨범 앨범 ID로 표시할를 설정 했으므로 업데이트 해 보겠습니다 합니다 **찾아보기** 자세히 보기를 연결 하는 보기입니다. 연결할 저장소 인덱스에서 저장소 찾아보기 이전 섹션의 끝에 했던 것 처럼 정확히 Html.ActionLink에 사용 됩니다. 브라우저 보기에 대 한 전체 소스 아래에 나타납니다.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

우리는 지금 사용할 수 있는 앨범을 나열 하는 장르 페이지에는 스토어 페이지에서 찾을 수 및 앨범을 클릭 하 여 해당 앨범에 대 한 자세한 내용은 볼 수 있습니다.

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-3.md)
> [다음](mvc-music-store-part-5.md)
