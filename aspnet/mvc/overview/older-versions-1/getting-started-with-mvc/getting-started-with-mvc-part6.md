---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 추가 된 메서드를 만들고 보기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 976df78ea22c30c094f70a57792d287f15d2c62d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400910"
---
<a name="adding-a-create-method-and-create-view"></a>추가 된 메서드를 만들고 보기
====================
[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다. 방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.


이 섹션에서 사용자가 데이터베이스에 새 영화를 만들 수 있게 하는 데 필요한 지원을 구현 하려고 합니다. 동영상/만들기 URL 동작을 구현 하 여이 작업을 수행 합니다.

두 단계로 구성 됩니다 영화/만들기 URL을 구현 합니다. 사용자가 영화/만들기 URL를 처음 방문할 때 새 동영상 입력을 채울 수 있는 HTML 폼 표시 하려고 합니다. 그런 다음 사용자가 폼 및 데이터를 서버에 다시 게시를 전송 하려고 게시 된 콘텐츠를 검색 하 고 데이터베이스에 저장 합니다.

두 create () 메서드 내에서 이러한 두 단계 MoviesController 클래스 내에서 구현 됩니다. 한 가지 방법은 표시 됩니다는 &lt;폼&gt; 사용자를 만드는 새 동영상을 작성 해야 합니다. 두 번째 방법은 사용자가 제출 하는 경우 게시 된 데이터를 처리 처리할 합니다 &lt;폼&gt; 서버에 백업 하 고 데이터베이스 내에서 새 동영상을 저장 합니다.

다음 코드는이 구현 하려면 MoviesController 클래스를 추가 합니다.

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

위의 코드는 모든 컨트롤러 내 해야 하는 코드를 포함 합니다.

Create View 템플릿을 사용 하 여 사용자에 게 폼을 표시 하는 이제 구현 해 보겠습니다. 첫 번째 Create 메서드를 마우스 오른쪽 단추로 클릭 하 고 영화 폼에 대 한 보기 템플릿을 만들려면 "뷰 추가"를 선택 합니다.

해당 보기 데이터 클래스로 보기 템플릿에서 "영화"을 전달 하려고 하 고 "스 캐 폴드" "만들기" 템플릿으로 하려고 한다는 것을 나타내려면 선택 합니다.

[![뷰 추가](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

추가 단추를 클릭 하면 \Movies\Create.aspx 템플릿 보기를 생성 됩니다. "콘텐츠 보기" 드롭다운에서 "만들기"를 선택 했기 때문에 뷰 추가 대화 상자 자동으로 "스 캐 폴드 된" 일부 기본 콘텐츠 한 합니다. 스 캐 폴딩을 만들 HTML &lt;폼&gt;, 유효성 검사 오류에 대 한 위치에서 메시지 및 스 캐 폴딩 영화를 알고, 이후 만들어질 레이블과 필드 클래스의 각 속성에 대 한 합니다.

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

데이터베이스 자동으로 영화 ID를 제공 하므로 참조 모델을 제거 필드로 보겠습니다. 만들기 보기에서 id입니다. 제거 후 7 줄 &lt;범례&gt;필드&lt;/legend&gt; 아직 ID 필드는 표시 된 대로 합니다.

보겠습니다 이제 새 동영상을 만들고 데이터베이스에 추가 합니다. 응용 프로그램을 다시 실행 하 여이 작업을 수행 하 고 방문 드리겠습니다는 "/ 영화" 새 영화를 추가 하려면 "만들기" 링크 URL을 클릭 합니다.

[![만들기-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

만들기 단추를 클릭 하면 되십시오 다시 (HTTP POST를 통해) 우리가 방금 만들었던 /Movies/Create 메서드에이 양식의 데이터를입니다. 시스템 자동으로 URL에서 "numTimes" 및 "name" 매개 변수는 데 걸린 시간과 메서드 앞에 있는 매개 변수에 매핑된 해당, 마찬가지로 시스템은 및 자동으로 수행 양식 필드 게시물에서 개체에 매핑합니다. 이 경우 "ReleaseDate" 및 "Title"와 같은 html 필드의 값은 동영상의 새 인스턴스를 올바른 속성에 자동으로 추가 됩니다.

보겠습니다 두 번째 Create 메서드는 MoviesController에서 다시 확인 합니다. "영화" 개체를 인수로 사용 하는 방법을 확인 합니다.

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

이 동영상 개체 만들기 작업 메서드를 사용 하 여 [HttpPost] 버전으로 전달한 다음 및 데이터베이스에 저장 하 고 영화 목록에 저장 된 결과 보여 주는 index () 작업 메서드를 다시 사용자 리디렉션됩니다.

[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

이 동영상은 하지만 잘못 및 데이터베이스 제목 없음를 사용 하 여 영화를 저장할 수 없습니다 확인 되지 것입니다. 사용자 데이터베이스 앞에 오류가 발생 했습니다 알려줍니다 수 하는 경우 유용한 것입니다. 응용 프로그램에 유효성 검사 지원을 추가 하 여이 다음을 하겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part5.md)
> [다음](getting-started-with-mvc-part7.md)
