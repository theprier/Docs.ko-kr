---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 영화 모델 및 테이블 (C#)에 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: f6364e438bbb7e128945255a5150e1e84e593ac4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-new-field-to-the-movie-model-and-table-c"></a>영화 모델 및 테이블 (C#)에 새 필드 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [C# 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 선호 하는 경우 전환의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


이 섹션에서는 모델 클래스를 일부 변경 하 고 모델 변경 내용과 일치 하도록 데이터베이스 스키마를 업데이트 하는 방법을 알아보려면 합니다.

## <a name="adding-a-rating-property-to-the-movie-model"></a>영화 모델에 등급 속성 추가

추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다. 열기는 *Movie.cs* 파일을 추가 `Rating` 다음과 같은 속성:

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

전체 `Movie` 다음 코드 처럼 이제 보이는 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

사용 하 여 응용 프로그램을 다시 컴파일하는 **디버그** &gt; **빌드 영화** 메뉴 명령입니다.

업데이트 한 했으므로 `Model` 클래스도 업데이트 해야는 *\Views\Movies\Index.cshtml* 및 *\Views\Movies\Create.cshtml* 새 지원하기위해템플릿을보려면`Rating`속성입니다.

열기는 *\Views\Movies\Index.cshtml* 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤의 **가격** 열입니다. 다음 추가 `<td>` 열을 렌더링 하는 서식 파일의 끝 부분에서 `@item.Rating` 값입니다. 다음은 이러한 어떤 업데이트 된 *Index.cshtml* 보기 템플릿은 보입니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

을 열고는 *\Views\Movies\Create.cshtml* 파일을 폼의 끝 부분에 다음 태그를 추가 합니다. 이 렌더링 하는 텍스트 상자가 새 동영상 만들어질 때에 대 한 등급을 지정할 수 있습니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>데이터베이스 스키마의 차이점 및 모델 관리

새 지원 하기 위해 응용 프로그램 코드를 지금 업데이트 한 `Rating` 속성입니다.

이제 응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다. 이 작업을 수행 하지만 다음과 같은 오류가 표시 됩니다.

![](adding-a-new-field/_static/image1.png)

때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다르면 이제는 `Movie` 기존 데이터베이스의 테이블입니다. (데이터베이스 테이블에 `Rating` 열이 없습니다.)

기본적으로를 사용 하 여 Entity Framework Code First 자동으로 데이터베이스를 만들려면이 자습서의 앞부분에서 마찬가지로 코드 첫 번째 테이블에 추가 데이터베이스는 데이터베이스의 스키마에서 생성 된 모델 클래스 동기화 되어 있는지 여부를 추적 해야 합니다. 동기화 하지 않을 경우 Entity Framework에서 오류가 발생 합니다. 이렇게 하면 그렇지 않으면만 찾을 수 (모호한 오류)에 의해 런타임 시 개발 시 문제를 추적 하기가 있습니다. 방금 표시 된 오류 메시지가 표시 될 놓이게 되어 하는 동기화 확인 기능.

오류를 해결 하는 방법은 두 가지가 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 방법은 매우 편리 하 게 테스트 데이터베이스에 대해 개발을 수행할 때 함께 모델 및 데이터베이스 스키마를 신속 하 게 개발할 수 있기 때문입니다. 데이터베이스의 기존 데이터 손실의 단점은 하지만입니다-하므로 있습니다 *하지 않는* 는 프로덕션 데이터베이스에서이 방법을 사용!
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터를 유지한다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.

이 자습서에서는 첫 번째 방법을 사용 합니다-는 Entity Framework Code First 모델이 변경 언제 든 지 자동으로 데이터베이스를 다시 만드는으로 사용 해야 합니다.

## <a name="automatically-re-creating-the-database-on-model-changes"></a>자동으로 다시 모델 변경 내용에 데이터베이스를 만드는 중

Code First 자동으로 삭제 하 고 응용 프로그램에 대 한 모델을 변경 하면 언제 든 지 데이터베이스를 다시 생성 되도록 응용 프로그램을 업데이트 해 보겠습니다.

> [!NOTE] 
> 
> **경고** 자동으로 삭제 하 고 개발 또는 테스트 데이터베이스를 사용 하는 경우에 데이터베이스를 다시 작성이 접근 방식을 사용 하도록 설정 해야 하 고 *되지* 실제 데이터를 포함 하는 프로덕션 데이터베이스에서 합니다. 프로덕션 서버에서 사용 하 여 데이터가 손실 될 수 있습니다.


**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-new-field/_static/image2.png)

"MovieInitializer" 클래스를 이름을 지정 합니다. 업데이트는 `MovieInitializer` 다음 코드를 포함 하는 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

`MovieInitializer` 클래스 모델에 의해 사용 되는 데이터베이스는 삭제 후 모델 클래스를 변경할 경우 자동으로 다시 생성을 지정 합니다. 코드에는 `Seed` 메서드 시간을 자동으로 추가 하려면 데이터베이스에 있는 일부 기본 데이터를 지정 하는 생성 (또는 다시 생성). 이 데이터베이스를 채우는 예제 데이터를 수동으로 변경 하는 모델을 만들 때마다 채우기 할 필요 없이 유용 합니다.

정의 했으므로 `MovieInitializer` 응용 프로그램이 실행 될 때마다 확인 모델 클래스는 데이터베이스의 스키마와에서 다른 지 있도록를 연결 하려는 클래스입니다. 인 경우에 모델과 일치를 다음 예제 데이터는 데이터베이스를 채우는 데이터베이스를 다시 만들려고 이니셜라이저를 실행할 수 있습니다.

열기는 *Global.asax* 의 루트에 있는 파일의 `MvcMovies` 프로젝트:

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

*Global.asax* 파일 프로젝트에 대 한 전체 응용 프로그램을 정의 하 고 포함 하는 클래스를 포함 한 `Application_Start` 응용 프로그램을 처음 시작할 때 실행 되는 이벤트 처리기입니다.

두 개의 추가 하겠습니다. 파일의 맨 위에 문을 사용 하 여 합니다. Entity Framework 네임 스페이스를 참조 하는 첫 번째 및 두 번째 네임 스페이스를 참조 합니다. 여기서 우리의 `MovieInitializer` 생활 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

다음 찾기는 `Application_Start` 메서드 호출을 추가 하 고 `Database.SetInitializer` 아래와 같이 메서드의 시작 부분에서:

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

`Database.SetInitializer` 방금 추가한 문을 나타냅니다 데이터베이스에서 사용 된 `MovieDBContext` 인스턴스를 자동으로 삭제 하 고 일치 하지 않으면 스키마 및 데이터베이스를 다시 생성 해야 합니다. 예제 데이터에 지정 된 데이터베이스도 채웁니다 살펴본 것 처럼 및는 `MovieInitializer` 클래스입니다.

닫기는 *Global.asax* 파일입니다.

응용 프로그램을 다시 실행을 탐색 하 고 */Movies* URL입니다. 응용 프로그램이 시작 되 면 모델 구조는 데이터베이스 스키마를 더 이상 일치 하는지 검색 합니다. 자동으로 새 모델 구조와 일치 하도록 데이터베이스를 다시 생성 하 고는 샘플 동영상 데이터베이스에 데이터가 채워지고:

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

클릭는 **새로 만들기** 새 동영상을 추가 하는 링크입니다. 참고에 대 한 등급을 추가할 수 있습니다.

[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)

**만들기**를 클릭합니다. 등급을 포함 하 여 새 동영상은 이제 나열 영화에서 표시:

[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)

이 섹션에서는 모델 개체를 수정할 데이터베이스의 변경 내용과 동기화 된 상태로 유지 하는 방법을 표시 합니다. 또한 시나리오를 체험할 수 있도록 샘플 데이터로 새로 만든된 데이터베이스를 채우는 하는 방법을 배웠습니다. 다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 해야 할 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)
