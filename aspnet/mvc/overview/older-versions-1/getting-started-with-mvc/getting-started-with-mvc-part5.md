---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: "컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs"
author: shanselman
description: "ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 1a733accabcd10409f5611c31001397e97533fb6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="accessing-your-models-data-from-a-controller"></a>컨트롤러에서 모델의 데이터에 액세스
====================
으로 [Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다. 방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.


이 섹션에서는 하겠습니다를 새 MoviesController 클래스를 만들고 동영상 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 다시 표시 하는 일부 코드를 작성 합니다.

Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 MoviesController를 확인 합니다.

[![컨트롤러 추가](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

이 프로젝트 내에서 우리의 \Controllers 폴더 아래 새 "MoviesController.cs" 파일이 만들어집니다. 새로 지정된 된 데이터베이스에서 영화 목록을 검색 하려면 MovieController 보겠습니다 업데이트 합니다.

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

우리는 영화 1984 년 여름에 해제만 검색 되도록 LINQ 쿼리를 수행 합니다. 이 목록을 영화 다시 렌더링, 하므로 메서드를 마우스 오른쪽 단추로 클릭 하 고 만들 추가 보기를 선택 하는 보기 템플릿이 필요 합니다.

뷰 추가 대화 상자에서는 합니다 나타낼 목록을 전달 하는 것&lt;Movies.Models.Movie&gt; 우리의 보기 서식 파일에 있습니다. 달리 뷰 추가 대화 상자를 사용 하 고 "Empty"는 서식 파일을 만들도록 선택한 이전 시간을 나타낼 수이 이번 주시기 바랍니다 Visual Studio를 자동으로 "스 캐 폴드" 템플릿 보기 위해 몇 가지 기본 콘텐츠로. "보기 콘텐츠 드롭다운 메뉴 내에서"List"항목을 선택 하 여 수행 합니다.

포함을 만든 새 클래스 추가 보기 대화 상자 표시 하기 위해 응용 프로그램을 컴파일하는 데 필요 합니다.

![뷰 추가](getting-started-with-mvc-part5/_static/image3.png)

추가 클릭 시스템은 자동으로 코드를 생성 보기에 대 한 동영상 목록을 표시 하는 데에 대 한 합니다. 이 값은 좋은 변경 하는 &lt;h2&gt; Hello World 보기와 이전에 수행한 것 처럼 "My 영화 목록"와 같은 값으로 제목입니다.

[![동영상-Microsoft Visual Developer 2010 Express를 웹](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

ְ ְ ¿כ 주소 표시줄에 /Movies를 방문 합니다. 이제 고 했으므로 이러한 내용을 컨트롤러 내에 기본 쿼리를 사용 하 여 데이터베이스에서 데이터를 검색 동영상에서 인식 하는 보기에 데이터를 반환 합니다. 해당 보기 다음 동영상 목록을 통해 회전 하 고 us에 대 한 데이터 테이블을 만듭니다.

[![Windows Internet Explorer-동영상 목록](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

म 않습니다 수 구현-이 응용 프로그램으로 편집, 세부 정보 및 삭제 기능을 수행해 줍니다 스 캐 폴드 템플릿이 생성 하는 기본 링크 필요 하지 않습니다. /Movies/Index.aspx 파일을 열고 해당 구성 요소 제거 합니다.

이 업데이트 된 보기 템플릿 어 떠 해야 이러한 변경을 수행 되 면에 대 한 소스 코드는 다음과 같습니다.

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

필요 하지 않습니다, 링크 만드는 되므로이 예에 삭제 됩니다. 하지만 다음 그대로 우리의 새로 만들기 링크를 유지할 됩니다 있습니다! 해당 열이 제거 포함 앱 모양은 다음과 같습니다.

[![Windows Internet Explorer-동영상 목록](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

동영상 데이터의 간단한 목록을 했습니다. 그러나 "새로 만들기" 링크를 클릭 하면 살펴보겠습니다 오류가 대로 연결 되지 않았습니다! 만들기 동작 메서드를 구현 하 고 사용자가 데이터베이스에 새 동영상을 입력할 수 있도록 살펴보겠습니다.

>[!div class="step-by-step"]
[이전](getting-started-with-mvc-part4.md)
[다음](getting-started-with-mvc-part6.md)
