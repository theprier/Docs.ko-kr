---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 76dc324134dc93c9552741fea9f1136abdc9184a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835756"
---
<a name="accessing-your-models-data-from-a-controller"></a>컨트롤러에서 모델의 데이터에 액세스
====================
[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다. 방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.


이 섹션에서는 하겠습니다 새 MoviesController 클래스를 만들고 영화 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 다시 표시 하는 일부 코드를 작성 합니다.

컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 MoviesController를 확인 합니다.

[![컨트롤러 추가](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

이 프로젝트 내에서 우리의 \Controllers 폴더 아래에 있는 새 "MoviesController.cs" 파일이 만들어집니다. 영화 목록에 새로 채워진된 데이터베이스에서 검색할 MovieController 업데이트 해 보겠습니다.

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

우리는 1984 년 여름부터 이후 출시 된 영화만 검색 되도록 LINQ 쿼리를 수행 합니다. 보기 템플릿을이 목록을 다시 영화 렌더링, 따라서 메서드에서 마우스 오른쪽 단추로 클릭 하 고 만들려면 추가 보기를 선택 해야 합니다.

뷰 추가 대화 상자 내 나타냅니다 목록을 전달 하는 것&lt;Movies.Models.Movie&gt; 보기 템플릿은 하 합니다. 뷰 추가 대화 상자를 사용 하 고 "Empty" 템플릿을 작성 하기로 했습니다. 이전 시간을 달리이 이번에는 나타냅니다 하려고 자동으로 "스 캐 폴딩" 보기 템플릿을 한 일부 기본 콘텐츠를 사용 하 여 Visual Studio 합니다. "보기 콘텐츠 드롭다운 메뉴에서"List"항목을 선택 하 여이 작업을 수행 합니다.

포함을 만든 경우 새 클래스 추가 보기 대화 상자에서 표시 하기 위해 응용 프로그램을 컴파일하는 데 필요 합니다.

![뷰 추가](getting-started-with-mvc-part5/_static/image3.png)

클릭 추가 하 고 자동으로 생성 됩니다 코드를 보려면 동영상 목록을 표시 하는 우리 회사에. 이 변경할 수 있는 좋은 기회를 &lt;h2&gt; Hello World 뷰를 사용 하 여 이전에 수행한 것과 같이 "내 Movie List" 같이 제목입니다.

[![동영상-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

응용 프로그램을 실행 하 고 주소 표시줄에 /Movies를 참조 하세요. 이제 했습니다 컨트롤러 내에서 기본 쿼리를 사용 하 여 데이터베이스에서 데이터를 검색 하 고 영화에 대 한 알고 있는 뷰로 데이터를 반환 합니다. 해당 보기 다음 동영상 목록을 통해 회전 하 고 우리 회사에 데이터 테이블을 만듭니다.

[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

에서는 되므로 스 캐 폴드 템플릿을 생성 하는 기본 링크를 필요가 없습니다이 응용 프로그램을 사용 하 여 편집, 세부 정보 및 삭제 기능을 구현 수 없습니다. /Movies/Index.aspx 파일을 열고 제거 합니다.

보기 템플릿은 업데이트 된 모양을 만들면 이러한 변경에 대 한 소스 코드는 다음과 같습니다.

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

에서는 필요가 있는 링크를 만들 되므로 예를 삭제 합니다. 그러나 다음으로 새로 만들기 링크를 유지 됩니다! 해당 열이 제거 포함 된 앱 모양은 다음과 같습니다.

[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

이제 영화 데이터의 단순 목록이 있습니다. 그러나 "새로 만들기" 링크를 클릭는 연결 되지 않았습니다으로 오류가 표시 됩니다 것! 만들기 동작 메서드를 구현 하 고 사용자가 데이터베이스에 새 영화를 입력할 수 있도록 보겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part4.md)
> [다음](getting-started-with-mvc-part6.md)
