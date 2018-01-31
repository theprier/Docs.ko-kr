---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: "모델에 열 추가 | Microsoft Docs"
author: shanselman
description: "ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 17ee105f596319423ac83cf718683ed293f952f3
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="adding-a-column-to-the-model"></a>모델에 열 추가
====================
으로 [Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다. 방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.


이 섹션에서는 하겠습니다를 데이터베이스의 스키마를 변경할를 응용 프로그램 내에서 변경 내용을 처리할 수 있습니다 어떻게 진행할 수 있습니다.

영화 테이블에 "등급" 열을 추가 해 보겠습니다. IDE로 다시 이동 하 고 데이터베이스 탐색기를 클릭 합니다. 영화 테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 정의 열기를 선택 합니다.

아래와 같이 "등급" 열을 추가 합니다. 이제 모든 등급 않아도, 되므로 열 수 null을 허용 합니다. 저장을 클릭 합니다.

[![영화 테이블 편집](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

다음으로, 솔루션 탐색기로 반환 하 고 (즉 \Models 폴더에) Movies.edmx 파일을 엽니다. 디자인 화면 (흰색 영역)을 마우스 오른쪽 단추로 클릭 하 고 데이터베이스에서 모델 업데이트를 선택 합니다.

[![동영상-Microsoft Visual 웹 Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

"업데이트 마법사" 시작 됩니다. 내에서 새로 고침 탭을 클릭 하 고 마침을 클릭 합니다. 영화 모델 클래스는 새 열이 포함 된 다음 업데이트 됩니다.

![업데이트 마법사 (2)](getting-started-with-mvc-part8/_static/image5.png)

마침을 클릭 한 후이 모델 영화 엔터티에 추가한 새 등급 열을 볼 수 있습니다.

[![영화 엔터티](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

데이터베이스 모델에서 열을 추가 했습니다 있지만 보기 항목에 대 한 알 수 없습니다.

## <a name="update-views-with-model-changes"></a>뷰 모델 변경 내용으로 업데이트

몇 가지 방법으로 새 등급 열을 반영 하기 위해 템플릿 보기를 사용 하 여 업데이트할 수 있습니다. 뷰 추가 대화 상자를 통해이 생성 하 여 이러한 보기를 만든 후 삭제할 하 고 다시 다시 만드십시오 수 있습니다. 그러나 일반적으로 초기 스 캐 폴드 생성에서 해당 템플릿 보기 수정을 이미 작성지 것입니다 사람과 추가 하 여 만들기에 대 한 ID 필드와 했던 것 처럼 마찬가지로 수동으로 필드를 삭제 해야 합니다.

\Views\Movies\Index.aspx 서식 파일을 열고 추가 &lt;번째&gt;등급&lt;/th&gt; 영화 테이블의 머리에 있습니다. Genre 후 마이닝를 추가 했습니다. 그런 다음 동일한 열 위치에 있지만 더 낮은 선을 추가 하 여이 새 등급을 출력 합니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

우리의 마지막 Index.aspx 서식 파일은 다음과 같이 표시 됩니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

보겠습니다 다음 \Views\Movies\Create.aspx 서식 파일을 열고 새 등급 속성이 대 한 레이블 및 텍스트를 추가 합니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

우리의 마지막 Create.aspx 서식 파일을 다음과 같이 표시 되며 바꿔보겠습니다 브라우저의 제목 및 보조 &lt;h2&gt; "만들기는 영화" 여기에 있을 때와 같은 값으로 제목!

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

응용 프로그램을 실행 하 고 만들기 페이지에 추가 된은 데이터베이스에 새 필드가 완성 되었습니다. 이 이번에는 등급--새 동영상을 추가 하 고 만들기를 클릭 키를 누릅니다.

[![동영상-Windows Internet Explorer 만들기](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

인덱스 페이지에 전송 하는 만들기를 클릭 하면 새 동영상이 함께 나열 하는 경우 데이터베이스에 새 등급 열

[![영화 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

이 기본 자습서 보기와 연결 하 고 하드 코드 된 데이터에 대 한 전달 컨트롤러를 만들기 시작 했습니다. 에서는 데이터베이스 디자인 하 고 만들고 일부 데이터를 저장 한 다음에 있습니다. 데이터베이스에서 데이터를 검색 하 고 HTML 테이블에 표시 합니다. 그런 다음 데이터를 추가할 데이터베이스 자체에서 웹 응용 프로그램의 사용자 수 있는 폼 만들기를 추가 했습니다. 유효성 검사를 추가 합니다. 그런 다음 JavaScript를 사용 하 여 클라이언트 쪽 유효성 검사를 수행 합니다. 마지막으로의 데이터를 새 열을 포함 하도록 데이터베이스를 변경 하 후 만들고 이러한 새 데이터를 표시 하는 두 개의 페이지를 업데이트 합니다.

이제 확인해이 중간 수준 자습서로 이동할 수 있습니다 "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" 뿐 아니라 많은 비디오 및 리소스에 [https://asp.net/mvc](https://asp.net/mvc) ASP.NET MVC에 대해 훨씬 더 자세한!

즐겨보세요!

- Scott Hanselman- [http://hanselman.com](http://hanselman.com) 및 [ @shanselman ](http://twitter.com/shanselman) Twitter에서.

>[!div class="step-by-step"]
[이전](getting-started-with-mvc-part7.md)
