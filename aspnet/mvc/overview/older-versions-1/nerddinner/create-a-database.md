---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft Docs
author: microsoft
description: 2 단계 모두의 저녁 식사를 보유 하는 데이터베이스를 만들고 NerdDinner 응용 프로그램에 대 한 데이터를 회신 하는 단계를 보여 줍니다.
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: 2a2ed8c91aa3ec0da63cd8e8686ff601f6e66374
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818968"
---
<a name="create-a-database"></a>데이터베이스 만들기
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 2 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 2 단계 모두의 저녁 식사를 보유 하는 데이터베이스를 만들고 NerdDinner 응용 프로그램에 대 한 데이터를 회신 하는 단계를 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner 2 단계: 데이터베이스 만들기

사용 데이터베이스 NerdDinner 응용 프로그램에 대 한 Dinner 및 참석 여부 회신 데이터를 저장 합니다.

무료 SQL Server Express edition을 사용 하 여 데이터베이스를 만드는 다음 단계 표시 (의 V2를 사용 하 여 쉽게 설치할 수 있습니다 합니다 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)). SQL Server Express와 전체 SQL Server를 사용 하 여 작동 하는 모든 코드를 작성 합니다.

### <a name="creating-a-new-sql-server-express-database"></a>새 SQL Server Express 데이터베이스 만들기

에서는 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 시작 하 고 다음을 선택 합니다 **추가-&gt;새 항목** 메뉴 명령:

![](create-a-database/_static/image1.png)

Visual Studio의 "새 항목 추가" 대화 상자가 표시 됩니다. "데이터" 범주별으로 필터링 하 고 "SQL Server 데이터베이스" 항목 템플릿을 선택 하겠습니다.

![](create-a-database/_static/image2.png)

에서는 "NerdDinner.mdf" 만들고 적중 확인 하려는 SQL Server Express 데이터베이스를 이름을 지정 합니다. Visual Studio는 다음 문의 우리의 \App에이 파일을 추가 하고자 하는 경우\_데이터 디렉터리 (이미 디렉터리 읽기를 사용 하 여 설정 및 보안 Acl을 작성):

![](create-a-database/_static/image3.png)

"예"를 클릭 하 고 새 데이터베이스 생성 되며이 솔루션 탐색기에 추가 합니다.

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>데이터베이스 내에서 테이블 만들기

이제 새 빈 데이터베이스를 했습니다. 일부 테이블을 추가 해 보겠습니다.

이렇게 하려면 데이터베이스 및 서버를 관리할 수 있게 하는 Visual Studio 내에서 "서버 탐색기" 탭 창으로 이동 됩니다. SQL Server Express 데이터베이스를 \App에 저장 된\_응용 프로그램 데이터 폴더는 자동으로 내에 표시 서버 탐색기. "서버 탐색기" 창 맨 위에 있는 "데이터베이스에 연결" 아이콘을를 사용 하 여 추가 SQL Server 데이터베이스 (로컬 및 원격 모두)도 목록에 추가 하려면 필요에 따라 했습니다.

![](create-a-database/_static/image5.png)

두 테이블에 RSVP도 추적 하는 Dinners 및 다른 저장 하나 NerdDinner 데이터베이스 –에 추가 합니다. 새 테이블 데이터베이스 내에서 "테이블" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 테이블 추가" 메뉴 명령을 선택 하 여 만들 수 있습니다.

![](create-a-database/_static/image6.png)

테이블의 스키마를 구성할 수 있도록 하는 테이블 디자이너를 엽니다. "Dinners" 테이블에 대 한 10 개 열의 데이터가 추가 됩니다.

![](create-a-database/_static/image7.png)

테이블에 대 한 고유 기본 키 여야 할 "DinnerID" 열을 표시 하려고 합니다. 이 "DinnerID" 열을 마우스 오른쪽 단추로 클릭 하 고 "기본 키 설정" 메뉴 항목을 선택 하 여 구성할 수 있습니다.

![](create-a-database/_static/image8.png)

DinnerID 기본 키 작업을 수행 하는 것 외에도 할 뿐 아니라이 값은 새 데이터 행을 테이블에 추가 됨에 따라 자동으로 증가 "id" 열으로 구성 (첫 번째 삽입된 Dinner 행 1의 DinnerID 해야 합니다. 즉, 두 번째 삽입 한 행 DinnerID 갖습니다 2 등).

"DinnerID" 열을 선택 하 여이 작업을 수행 하 고 "열 속성" 편집기를 사용 하 여 "Yes" 열에 "(Identity입니다)" 속성을 설정 수 있습니다. 표준 id 기본값을 사용 하 여 (1부터 시작 하 고 각 새 Dinner 행에 1을 증가).

![](create-a-database/_static/image9.png)

Ctrl + S를 입력 하 여 또는 사용 하 여 테이블 저장 한 다음 됩니다 합니다 **파일-&gt;저장** 메뉴 명령입니다. 이 테이블의 이름을 지정 하는 라는 메시지가 나타납니다. 이름은 "Dinners":

![](create-a-database/_static/image10.png)

새 Dinners 테이블은 서버 탐색기에서 데이터베이스 내에서 표시 됩니다.

에서는 그런 다음 위의 단계를 반복 하 고 "RSVP" 테이블을 만듭니다. 사용 하 여이 테이블 3 열이 있어야 합니다. 기본 키로 RsvpID 열을 설정 하 고도 어렵게 id 열:

![](create-a-database/_static/image11.png)

저장 하 고 이름을 "RSVP" 지정 됩니다.

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>테이블 간의 외래 키 관계를 설정합니다.

이제 데이터베이스 내에서 두 테이블이 있습니다. 마지막 스키마 디자인 단계 각 Dinner 행 0 개 이상의 RSVP 행에 적용 되는 연결 수 있도록 이러한 두 테이블 간에 "일대다" 관계를 설정 됩니다. "Dinners" 테이블에서 "DinnerID" 열에 외래 키 관계에 RSVP 테이블의 "DinnerID" 열을 구성 하 여이 작업을 수행 합니다.

이렇게 하려면에서는 엽니다 참석 여부 회신은 테이블 디자이너에서는 서버 탐색기에서 두 번 클릭 합니다. 그 안의 "DinnerID" 열 선택 한 다음 마우스 오른쪽 단추로 클릭 하 고 "Relationshps..." 상황에 맞는 메뉴 명령을 선택:

![](create-a-database/_static/image12.png)

테이블 간의 관계를 설정 하기 사용할 수 있는 대화 상자가 표시 됩니다.

![](create-a-database/_static/image13.png)

대화 상자에 새 관계를 추가 하려면 [추가] 단추를 클릭 합니다. 관계를 추가한 후 대화 상자의 오른쪽에 속성 표 내에서 "테이블 및 열 사양" 트리 뷰 노드를 확장 하 고 오른쪽의 "..." 단추를 클릭 하겠습니다 했습니다.

![](create-a-database/_static/image14.png)

"..." 단추를 클릭 하면 테이블 및 열을 관계와 관련 한 가지 뿐만 아니라 관계 이름 수를 지정할 수 있는 다른 대화 상자를 표시 합니다.

"Dinners" 되도록 기본 키 테이블을 변경 하 고 기본 키로 Dinners 테이블 내에서 "DinnerID" 열을 선택 합니다. 외래 키 테이블 및 RSVP RSVP 테이블이 됩니다. DinnerID 열이 외래 키와 연결 됩니다.

![](create-a-database/_static/image15.png)

이제 RSVP 테이블의 각 행의를 저녁 테이블의 행과 연결 됩니다. SQL Server는 미국 –에 대 한 참조 무결성을 유지 되며 올바른 Dinner 행을 가리키지 않을 경우 새 RSVP 행을 추가할 수 없습니다. 또한 수 없게 됩니다 미국에서 참조 하는 행을 여전히 RSVP 없으면 Dinner 행을 삭제 합니다.

### <a name="adding-data-to-our-tables"></a>테이블에 데이터 추가

보겠습니다 Dinners 테이블에 일부 샘플 데이터를 추가 하 여 완료 합니다. 서버 탐색기 내에서 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시" 명령을 선택 하 여 테이블에 데이터를 추가할 수 있습니다.

![](create-a-database/_static/image16.png)

에서는 몇 가지 응용 프로그램을 구현 하는 대로 나중에 사용할 수는 Dinner 데이터 행 추가 합니다.

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>다음 단계

데이터베이스 작성을 마쳤습니다. 이제 쿼리 및 업데이트를 사용할 수 있는 모델 클래스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)
