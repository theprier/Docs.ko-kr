---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft Docs
author: microsoft
description: 2 단계를 모두 dinner 보유 하는 데이터베이스를 만들고 RSVP 업그레이드 되었으며 수정 응용 프로그램에 대 한 데이터 단계를 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: ba28d671bf13ec54b83b876462e2c23f90310037
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869142"
---
<a name="create-a-database"></a>데이터베이스 만들기
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 2 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 2 단계를 모두 dinner 보유 하는 데이터베이스를 만들고 RSVP 업그레이드 되었으며 수정 응용 프로그램에 대 한 데이터 단계를 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-2-creating-the-database"></a>업그레이드 되었으며 수정 2 단계: 데이터베이스 만들기

업그레이드 되었으며 수정 응용 프로그램에 대 한 모든 Dinner 및 RSVP 데이터를 저장 하는 데이터베이스를 사용해 보겠습니다.

무료 SQL Server Express edition을 사용 하 여 데이터베이스를 만드는 다음 단계 표시 (v 2의를 사용 하 여 쉽게 설치할 수 있는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)). SQL Server Express 및 SQL Server 전체와 작동 하는 모든 코드를 작성 합니다.

### <a name="creating-a-new-sql-server-express-database"></a>새 SQL Server Express 데이터베이스 만들기

이 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 시작 알아보고 선택 하겠습니다는 **추가-&gt;새 항목** 메뉴 명령:

![](create-a-database/_static/image1.png)

이 Visual Studio의 "새 항목 추가" 대화 상자를 표시 합니다. "데이터" 범주별으로 필터링 알아보고 "SQL Server 데이터베이스" 항목 템플릿을 선택 하겠습니다.

![](create-a-database/_static/image2.png)

여기서 "NerdDinner.mdf" 만들고 적중 확인 하려는 SQL Server Express 데이터베이스를 이름을 지정 합니다. Visual Studio는 다음 문의 우리의 \App에이 파일에 추가 되기를 원하는\_데이터 디렉터리 (디렉터리가 이미 있는 모두 읽기 설정 및 보안 Acl 쓰기):

![](create-a-database/_static/image3.png)

"Yes"를 클릭 합니다 및 우리의 새 데이터베이스가 생성 되 고 우리의 솔루션 탐색기에 추가 합니다.

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>데이터베이스 내에서 테이블 만들기

비어 있는 새 데이터베이스를 했습니다. 일부 테이블을 추가 해 보겠습니다.

이렇게 하려면 데이터베이스 및 서버를 관리할 수 있게 하는 Visual Studio 내에서 "서버 탐색기" 탭 창으로 이동 됩니다 했습니다. SQL Server Express 데이터베이스는 \App에 저장 된\_응용 프로그램 데이터 폴더 서버 탐색기 내 표시 자동으로 됩니다. 추가 SQL Server 데이터베이스 (로컬 및 원격 모두)도 목록에 추가 하려면 "서버 탐색기" 창 맨 위에 있는 "데이터베이스에 연결" 아이콘을 사용 필요에 따라 했습니다.

![](create-a-database/_static/image5.png)

두 테이블을 저장 하 여 Dinners 고 다른 RSVP 통용 추적 하 여 업그레이드 되었으며 수정 데이터베이스에 추가 합니다. 데이터베이스 내에서 "Tables" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 테이블 추가" 메뉴 명령을 선택 하 여 새 테이블을 만들 수 있습니다.

![](create-a-database/_static/image6.png)

예제 테이블의 스키마를 구성할 수 있도록 하는 테이블 디자이너를 엽니다. "Dinners" 테이블에 대 한 데이터의 10 개의 열을 추가 합니다.

![](create-a-database/_static/image7.png)

"DinnerID" 열을 테이블에 대 한 고유 기본 키를 사용 하는 것이 좋습니다. "DinnerID" 열을 마우스 오른쪽 단추로 클릭 하 고 "기본 키 설정" 메뉴 항목을 선택 하 여이 구성할 수 있습니다.

![](create-a-database/_static/image8.png)

에 이외에 DinnerID 기본 키도 원하는 값을 가진 새 데이터 행을 테이블에 추가 되는 자동 증가 "id" 열으로 구성 (첫 번째 삽입 된 Dinner 행 1 DinnerID 갖습니다 합니다. 즉, 두 번째 삽입 된 행 DinnerID 갖습니다 2, 등).

म "DinnerID" 열을 선택 하 여이 작업을 수행 하 고 "열 속성" 편집기를 사용 하 여 "예"로 열에 "(Identity는)" 속성을 설정 수 있습니다. 표준 id 기본값을 사용 합니다 (1부터 시작 하 고 각 새 Dinner 행에 1를 증가 시키는):

![](create-a-database/_static/image9.png)

Ctrl + S를 입력 하 여 또는 사용 하 여 테이블을 저장 한 다음 하겠습니다는 **파일-&gt;저장** 메뉴 명령입니다. 테이블의 이름을 지정 하는 묻는 메시지가 나타납니다. 이름을 것 "Dinners":

![](create-a-database/_static/image10.png)

서버 탐색기에서 데이터베이스 내에서 새 Dinners 테이블 표시 한 다음 됩니다.

그런 다음 위의 단계를 반복 알아보고 "RSVP" 테이블을 만들 하겠습니다. 와이 테이블 3 개의 열이 있어야 합니다. RsvpID 열을 기본 키로 설정 하 고 또한 id 열인지 확인 합니다.

![](create-a-database/_static/image11.png)

저장 알아보고 "RSVP" 이름을 지정 하겠습니다.

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>테이블 간 외래 키 관계를 설정합니다.

했습니다 두 테이블 데이터베이스 내에서. 각 Dinner 행에 적용 되는 0 개 이상의 RSVP 행 연결 수 있도록 우리의 마지막 스키마 디자인 단계 – 이러한 두 테이블 간에 "일대다" 관계를 설정 하 됩니다. "Dinners" 테이블의 "DinnerID" 열에 외래 키 관계에 RSVP 테이블의 "DinnerID" 열을 구성 하 여 수행 됩니다.

이렇게 하려면 서버 탐색기에서 두 번 클릭 하 여 테이블 디자이너에서는 RSVP 테이블을 엽니다 했습니다. 그 안의 "DinnerID" 열 선택 다음 마우스 오른쪽 단추로 클릭 하 고 "Relationshps..."를 선택 합니다. 상황에 맞는 메뉴 명령:

![](create-a-database/_static/image12.png)

그러면 म 테이블 간의 관계를 설정 하는 데 사용할 수 있는 대화 상자를 표시 됩니다.

![](create-a-database/_static/image13.png)

대화 상자에 새 관계를 추가 하려면 "추가" 단추를 클릭 합니다. 관계 추가 되 면에 대화 상자에서 오른쪽에 속성 표 내에서 "테이블 및 열 사양" 트리 뷰 노드를 확장 하 고 열의 오른쪽에 있는 "..." 단추를 클릭 합니다 했습니다.

![](create-a-database/_static/image14.png)

"..." 단추를 클릭 하면 테이블 및 열, 관계에 참여 한다고 뿐만 아니라 관계의 이름을 하기 수를 지정할 수 있도록 하는 또 다른 대화 상자를 표시 합니다.

"Dinners" 되도록 기본 키 테이블을 변경 하 고 기본 키로 Dinners 테이블 내에서 "DinnerID" 열을 선택 합니다. 외래 키 테이블 및 RSVP RSVP 테이블이 됩니다. DinnerID 열이 외래 키로 연결 됩니다.

![](create-a-database/_static/image15.png)

이제 RSVP 테이블의 각 행은 Dinner 테이블의 행과 연결 됩니다. SQL Server 소중에 대 한 참조 무결성을 유지 되며에서 올바른 Dinner 행을 가리키지 않을 경우 새 RSVP 행을 추가할 수 있습니다. 또한 예방할 우리에서 참조 하는 행을 RSVP 여전히 없으면 Dinner 행을 삭제 합니다.

### <a name="adding-data-to-our-tables"></a>이 코드에서는 테이블에 데이터 추가

Dinners 테이블에 몇 가지 샘플 데이터를 추가 하 여 완료 해 보겠습니다. 에 서버 탐색기 내에서 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시" 명령을 선택 하 여 테이블에 데이터를 추가할 수 있습니다.

![](create-a-database/_static/image16.png)

나중에 응용 프로그램을 구현 하는 때 사용할 수 있는 Dinner 데이터 행을 몇 개 추가 하겠습니다.

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>다음 단계

이 데이터베이스를 만드는 하는 작업을 완료 했습니다. 이제 쿼리 하 고 업데이트를 사용할 수 있는 모델 클래스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)
