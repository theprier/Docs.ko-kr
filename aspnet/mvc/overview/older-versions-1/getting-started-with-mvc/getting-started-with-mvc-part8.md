---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 모델에 열 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 22a6c4e5a07e81d5876cc442e68926094e3a243d
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827739"
---
<a name="adding-a-column-to-the-model"></a>모델에 열 추가
====================
[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다. 방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.


이 섹션에서는 수는 데이터베이스의 스키마 변경 및 응용 프로그램 내에서 변경 내용을 처리 하는 방법을 안내 하려고 합니다.

동영상 테이블에 "등급" 열을 추가 해 보겠습니다. IDE로 돌아가서 데이터베이스 탐색기를 클릭 합니다. Movie 테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 정의 열기를 선택 합니다.

아래와 같이 "Rating" 열을 추가 합니다. 이제 모든 등급 않아도, 되므로 null 열 수 있습니다. 저장을 클릭 합니다.

[![동영상 테이블 편집](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

다음으로, 솔루션 탐색기에 반환 하 고 (상태인 \Models 폴더) Movies.edmx 파일을 엽니다. 디자인 화면 (흰색 영역)을 마우스 오른쪽 단추로 클릭 하 고 데이터베이스에서 모델 업데이트를 선택 합니다.

[![동영상-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

"업데이트 마법사" 시작 됩니다. 에 새로 고침 탭을 클릭 하 고 마침을 클릭 합니다. 영화 모델 클래스는 새 열을 사용 하 여 다음 업데이트 됩니다.

![업데이트 마법사 (2)](getting-started-with-mvc-part8/_static/image5.png)

완료를 클릭 하면 영화 엔터티 모델에 추가한 새 등급 열을 볼 수 있습니다.

[![영화 엔터티](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

데이터베이스 모델에서 열을 추가한 보기 모 르에 대 한 합니다.

## <a name="update-views-with-model-changes"></a>뷰 모델 변경 내용으로 업데이트

새 등급 열을 반영 하도록 템플릿 보기를 사용 하는 업데이트 수는 몇 가지가 있습니다. 뷰 추가 대화 상자를 통해이 생성 하 여 이러한 뷰를 만들었기 때문 없습니다 삭제 하 고 다시 다시 만듭니다. 그러나 일반적으로 사용자는 이미 수정 템플릿 해당 보기를 스 캐 폴드 된 초기 생성에서 및 추가 또는 만들기에 대 한 ID 필드를 사용 하 여 했던 것 처럼 수동으로, 방금 필드를 삭제 하려고 합니다.

\Views\Movies\Index.aspx 템플릿을 열고 추가 &lt;th&gt;등급&lt;/th&gt; Movie 테이블의 머리에 있습니다. 장르 후 마이닝를 추가 했습니다. 그런 다음 동일한 열 위치에 있지만 아래의 새 등급을 출력 하는 줄을 추가 합니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

최종 Index.aspx 템플릿은 다음과 같이 표시 됩니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

보겠습니다 다음 \Views\Movies\Create.aspx 템플릿을 열고 새 등급 속성에 대 한 레이블 및 텍스트를 추가 합니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

최종 Create.aspx 템플릿은 이렇게 확인 하 고 브라우저의 제목 및 보조 데이터베이스를 변경해 보겠습니다 &lt;h2&gt; "만들기는 영화" 여기에 있는 동안 같이 제목!

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

앱을 실행 하 고 만들기 페이지에 추가 된 데이터베이스에 새 필드를 완성 되었습니다. 등급-이 이번-새 동영상을 추가 하 고 만들기를 클릭 합니다.

[![Windows Internet Explorer 동영상-만들기](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

인덱스 페이지에 전송 하 고 만들기를 클릭 하면 새 영화는와 함께 나열 하는 경우 데이터베이스에 새 등급 열

[![영화 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

이 기본 자습서를 가져온 컨트롤러 뷰를 사용 하 여 연결 하 고 하드 코드 된 데이터를 전달 하기 시작 합니다. 생성 및 데이터베이스를 설계 하 고 일부 데이터를 저장 한 다음에 해당 합니다. 데이터베이스에서 데이터를 검색 하 고 HTML 테이블에 표시 합니다. 그런 다음 데이터를 추가 데이터베이스 자체에서 웹 응용 프로그램 내에서 사용자는 양식 만들기를 추가 했습니다. 유효성 검사를 추가 하 고 JavaScript를 사용 하 여 클라이언트 쪽에서 유효성 검사를 수행 합니다. 마지막으로 데이터를 새 열을 포함 하도록 데이터베이스를 변경 하 고 만들고이 새 데이터를 표시 하는 두 페이지를 업데이트 합니다.

이 중급 자습서를 진행 이제 바랍니다 "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" 다양 한 비디오 및 리소스 뿐만 아니라 [ https://asp.net/mvc ](https://asp.net/mvc) ASP.NET MVC에 대 한 더 자세한!

즐겨보세요!

- -Scott Hanselman [ http://hanselman.com ](http://hanselman.com) 하 고 [ @shanselman ](http://twitter.com/shanselman) Twitter에서.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part7.md)
