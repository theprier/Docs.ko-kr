---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 데이터베이스 만들기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 0e72359095e4c40ef7e56f1290a45ded257143c9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362358"
---
<a name="creating-a-database"></a>데이터베이스 만들기
====================
[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다. 방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.


이 섹션에서 사용 하 여 저장 하 고 영화 데이터를 검색 하는 새 SQL Express 데이터베이스를 만들 하려고 합니다. Visual Web Developer ide 보기 선택 | 서버 탐색기입니다. 데이터 연결을 마우스 오른쪽 단추로 클릭 하 고 연결 추가...

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

데이터 소스 선택 대화 상자에서 Microsoft SQL Server를 선택 하 고 계속을 선택 합니다.

![](getting-started-with-mvc-part4/_static/image2.png)

연결 추가 대화 상자에서 입력 ". \SQLEXPRESS"에서 서버 이름의 새 데이터베이스의 이름으로 "Movies"를 입력 합니다.

[![연결 대화 상자를 추가 합니다.](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

확인을 클릭 하면 해당 데이터베이스를 만들려는 경우 라는 나타납니다. 예 선택 합니다.

[![영화를 만드시겠습니까?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

이제 서버 탐색기에서 빈 데이터베이스를 했습니다.

![새 테이블 추가](getting-started-with-mvc-part4/_static/image7.png)

테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 추가 클릭 합니다. 테이블 디자이너에 표시 됩니다. Id "," 제목 "," ReleaseDate "," 장르 "및" 가격에 대 한 열을 추가 합니다. ID 열을 마우스 오른쪽 단추로 클릭 하 고 클릭 기본 키를 설정 합니다. 유사 내 디자인 분야는 다음과 같습니다.

[![데이터베이스 테이블 편집기](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

또한 Id 열을 선택 하 고 열 속성 아래에서 "Id 사양" "예."로 변경

[![IsIdentity-열 속성](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

수행할 적지, 도구 모음에서 저장 아이콘을 클릭 하거나 파일을 선택 | 메뉴에서 저장 하 고 테이블 이름을 "**영화**" (단일). 데이터베이스 및 테이블을 만들었습니다!

[![이름 선택](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

서버 탐색기로 돌아가서 Movie 테이블을 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시."를 선택 합니다. 데이터베이스에 일부 데이터가 있으므로 몇 가지 영화를 입력 합니다.

[![데이터베이스 테이블 편집](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>모델 만들기

이제 IDE의 오른쪽에서 솔루션 탐색기로 전환 하 고 Models 폴더를 마우스 오른쪽 단추로 클릭 및 추가 선택 합니다. | 새 항목입니다.

[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

새 데이터베이스에서 엔터티 모델을 만들 하려고 합니다. 이렇게 하면 클래스 집합을 쉽게 쿼리하고 데이터베이스 내에서 데이터를 조작 하는 프로젝트에 추가 됩니다. 대화 상자의 왼쪽에 데이터 노드를 선택 하 고 ADO.NET 엔터티 데이터 모델 항목 템플릿을 선택 합니다. Movies.edmx 이름을 지정 합니다.

[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

"추가" 단추를 클릭 합니다. 그런 다음 "엔터티 데이터 모델 마법사" 시작 됩니다.

표시 되는 새 대화 상자에서 데이터베이스에서 생성을 선택 합니다. 데이터베이스를 방금 만들었습니다 때문만 해야 새 데이터베이스 및 해당 테이블에 대 한 엔터티 프레임 워크에 알립니다. 웹 응용 프로그램의 구성에서 데이터베이스 연결 저장 옆에 클릭 합니다. 이제 테이블 및 동영상을 확인 확인란을 선택 하 고 완료 합니다.

[![엔터티 데이터 모델 마법사](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

이제 Entity Framework 디자이너에서 새 동영상 테이블을 참조 하 고 코드에서 액세스할 수 있습니다.

[![동영상-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

디자인 화면에서 "영화" 클래스를 볼 수 있습니다. 이 클래스를 데이터베이스에 "영화" 테이블에 매핑되고 각 속성에 테이블과 열에 매핑합니다. "영화" 클래스의 각 인스턴스는 "Movie" 테이블 내의 행에 대응 됩니다.

기본 이름 지정 및 Entity Framework에서 사용 되는 규칙을 매핑, 마음에 들지 않으면 변경 하거나 사용자 지정 하는 Entity Framework 디자이너를 사용할 수 있습니다. 이 응용 프로그램에서는 기본값을 사용 하 고 파일로 저장-됩니다.

이제 몇 가지 실제 데이터로 작업 해 보겠습니다!

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part3.md)
> [다음](getting-started-with-mvc-part5.md)
