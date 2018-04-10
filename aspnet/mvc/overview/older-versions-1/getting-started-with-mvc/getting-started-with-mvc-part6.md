---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 추가 된 메서드를 만들고 보기 만들기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 48e656a0c394b9db5baaec9c557ec38c4020d41b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="adding-a-create-method-and-create-view"></a>추가 된 메서드를 만들고 보기 만들기
====================
으로 [Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다. 방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.


이 섹션에서는 사용자가 데이터베이스에 새 동영상을 만들 수 있도록 하는 데 필요한 지원을 구현 것 이며 합니다. 영화/만들기 URL 동작을 구현 하 여 수행 합니다.

영화/만들기 URL 구현 두 단계로 구성 됩니다. 사용자가 동영상/만들기 URL를 처음 방문할 때 새 동영상을 입력 하 여 채울 수 있는 HTML 폼을 표시 하는 것이 좋습니다. 그런 다음 사용자가 폼과 데이터는 서버에 다시 게시를 전송 하려고 게시 된 콘텐츠를 검색 하 고 데이터베이스에 저장 합니다.

MoviesController 클래스 내에서 두 개의 create () 메서드 내에서 이러한 두 단계를 구현 합니다. 한 가지 방법은 표시 됩니다는 &lt;양식&gt; 사용자를 만들려면 새 동영상을 채울 해야 합니다. 두 번째 방법은 사용자가을 전송할 때 게시 된 데이터 처리를 처리할는 &lt;양식&gt; 를 서버에 백업 하 고 데이터베이스 내에서 새 동영상을 저장 합니다.

다음은 코드가를 구현 하려면 MoviesController 클래스를 추가 합니다.

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

위의 코드는 모든 컨트롤러 내에서 사용 해야 하는 코드를 포함 합니다.

이제 사용자에 게을 둔 양식을 표시 하는을 사용 해야 하는 Create View 템플릿을 구현 해 보겠습니다. 첫 번째 Create 메서드를 마우스 오른쪽 단추로 클릭 알아보고 영화 폼에 대 한 보기 템플릿을 만들려면 "뷰 추가"를 선택 하겠습니다.

해당 보기 데이터 클래스 보기 템플릿 "영화"를 전달 하려고 하 고 "만들기" 템플릿 "스 캐" 한다고 지정 하는 선택 하겠습니다.

[![뷰 추가](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

추가 단추를 클릭 한 후 드립니다 \Movies\Create.aspx 보기 템플릿 만들어질 수 있습니다. "만들기"를 "콘텐츠 보기" 드롭다운 목록에서 선택 것 때문에 뷰 추가 대화 상자 자동으로 "스 캐 폴드 된" 일부 기본 콘텐츠를 수행해 줍니다. 스 캐 폴딩을 HTML 만든 &lt;양식&gt;, 이동, 메시지 유효성 검사 오류에 대 한 전체 및 클래스의 각 속성에 대 한 레이블 및 필드 만든 동영상에 대 한 스 캐 폴딩 알고, 있으므로 합니다.

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

데이터베이스의 ID가 영화를 자동으로 제공 하며, 이므로 해당 참조 모델을 제거 해당 필드 보겠습니다. Id 만들기 시각입니다. 후 7 선을 제거 &lt;범례&gt;필드&lt;/legend&gt; 대로 않도록 하는 ID 필드 표시 합니다.

보겠습니다 이제 새 동영상을 만들고 데이터베이스에 추가 합니다. 응용 프로그램을 다시 실행 하 여 알아보고 방문 하겠습니다는 "/ 영화" 새 동영상을 추가 하려면 "만들기" 연결 URL을 클릭 합니다.

[![만들기-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

만들기 단추를 클릭가 게시 다시 (통해 HTTP POST) 방금 만든 /Movies/Create 메서드에이 폼에 데이터입니다. 때 시스템이 자동으로 url "numTimes" 및 "name" 매개 변수는 데 걸린 하 고 해당 메서드를 앞에 있는 매개 변수에 매핑된 마찬가지로 시스템은 자동으로 양식 필드에서 게시물을 가져오고 개체에 매핑합니다. 이 경우 "ReleaseDate" 및 "제목"와 같은 html 필드의 값을 자동으로 동영상의 새 인스턴스를 올바른 속성에 배치 됩니다.

이제 두 번째 Create 메서드 우리의 MoviesController에서 다시 확인 합니다. 걸리는 "영화" 개체를 인수로 사항을 참고 하십시오.

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

이 영화 개체가 만들기 작업 메서드의 [HttpPost] 버전에 전달 된 다음 및 데이터베이스에 저장 하 고 사용자 영화 목록에 저장 된 결과 보여 주는 index () 동작 메서드를 다시 리디렉션됩니다.

[![Windows Internet Explorer-동영상 목록](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

म 우리의 영화은 하지만 및 제목 없음 함께 동영상을 저장 하는 데이터베이스 허용 하지 않는 확인 되지 않습니다. 이 좋을 수 알립니다를 이전 데이터베이스에서 오류가 발생 했습니다. 응용 프로그램에 유효성 검사 지원을 추가 하 여 다음이 단계를 하겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part5.md)
> [다음](getting-started-with-mvc-part7.md)
