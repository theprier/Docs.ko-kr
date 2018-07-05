---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 영화 모델 및 테이블 (C#)에 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 91b02f9991b714f8da2aa736c9ba5e58a7228350
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829074"
---
<a name="adding-a-new-field-to-the-movie-model-and-table-c"></a>영화 모델 및 테이블 (C#)에 새 필드 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [C# 버전 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 원한다 면으로 전환 합니다 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


이 섹션 모델 클래스에 일부 변경을 수행 하 고 모델 변경 내용과 일치 하도록 데이터베이스 스키마를 업데이트 하는 방법을 알아봅니다.

## <a name="adding-a-rating-property-to-the-movie-model"></a>영화 모델에 등급 속성 추가

새로 추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다. 엽니다는 *Movie.cs* 파일을 추가 합니다 `Rating` 다음과 같은 속성:

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

전체 `Movie` 다음 코드는 이제 다음과 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

사용 하 여 응용 프로그램을 다시 컴파일해야 합니다 **디버그** &gt; **영화 빌드** 메뉴 명령 합니다.

업데이트 했으므로 합니다 `Model` 클래스도 업데이트 해야 합니다 *\Views\Movies\Index.cshtml* 및 *\Views\Movies\Create.cshtml* 새 를지원하기위해템플릿을보려면`Rating`속성입니다.

엽니다는 *\Views\Movies\Index.cshtml* 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤를 **가격** 열입니다. 추가한를 `<td>` 렌더링 템플릿의 끝 열을 `@item.Rating` 값입니다. 업데이트 된 다음과 같습니다 *Index.cshtml* 보기 템플릿은 다음과 같습니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

다음으로 열고 합니다 *\Views\Movies\Create.cshtml* 파일과 폼의 끝 부분에 다음 태그를 추가 합니다. 이 입력란을 렌더링 하는 새 영화를 만들 때 등급을 지정할 수 있습니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>관리 모델과 데이터베이스 스키마의 차이점

이제 새 지원 응용 프로그램 코드를 업데이트 했으므로 `Rating` 속성입니다.

이제 응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다. 이렇게 하면 다음 오류가 표시 됩니다 그러나:

![](adding-a-new-field/_static/image1.png)

때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다릅니다 이제는 `Movie` 기존 데이터베이스의 테이블입니다. (데이터베이스 테이블에 `Rating` 열이 없습니다.)

기본적으로 사용 하는 경우 Entity Framework Code First 데이터베이스를 자동으로 만들려면이 자습서의 앞부분에서 수행한 것 처럼 Code First 테이블에 추가 데이터베이스를 데이터베이스의 스키마에서 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적 합니다. 동기화 하지 않은 경우 Entity Framework는 오류를 throw 합니다. 이 쉽게 발생할 수 있는 그렇지 않은 경우만 (모호한 오류가) 하 여 런타임 시 개발 시 문제를 추적 합니다. 동기화 확인 기능은 오류 메시지 표시를 방금 본 원인입니다.

오류를 해결 하는 방법은 두 가지가 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 접근 방식 이므로 매우 편리 하 게 테스트 데이터베이스에서 활발 한 개발을 수행 하는 경우 신속 하 게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다. 그러나 단점은 데이터베이스의 기존 데이터를 손실 하는-있도록 있습니다 *하지* 프로덕션 데이터베이스에서이 방법을 사용 하려면!
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터를 유지한다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.

이 자습서에서는 첫 번째 방법은 사용-는 Entity Framework Code First 모델을 변경 하 고 언제 든 지 자동으로 데이터베이스를 다시 만드는 해야 합니다.

## <a name="automatically-re-creating-the-database-on-model-changes"></a>모델 변경 내용에 데이터베이스를 자동으로 다시 생성

Code First 자동으로 삭제 하 고 응용 프로그램에 대 한 모델을 변경 하면 언제 든 지 데이터베이스를 다시 생성 되도록 응용 프로그램을 업데이트 해 보겠습니다.

> [!NOTE] 
> 
> **경고** 자동으로 삭제 하 고 개발 또는 테스트 데이터베이스를 사용 하는 경우에 데이터베이스를 다시 작성 하는이 방법을 사용 하도록 설정 해야 하 고 *되지* 실제 데이터가 포함 된 프로덕션 데이터베이스에서. 사용 하 여 프로덕션 서버의 데이터가 손실 될 수 있습니다.


**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-new-field/_static/image2.png)

"MovieInitializer" 클래스를 이름을 지정 합니다. 업데이트 된 `MovieInitializer` 다음 코드를 포함 하는 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

`MovieInitializer` 클래스 모델에서 사용 하는 데이터베이스는 삭제 후 모델 클래스를 변경할 경우 자동으로 다시 생성을 지정 합니다. 코드를 포함 한 `Seed` 때마다 자동으로 추가 하려면 데이터베이스에 있는 일부 기본 데이터를 지정 하는 방법에 만든 (또는 다시 생성). 이를 수동으로 변경 하는 모델 때마다 채우는 필요 없이 몇 가지 샘플 데이터를 사용 하 여 데이터베이스를 채우는 데 유용할 수가 있습니다.

정의한 했으므로 `MovieInitializer` 모델 클래스는 데이터베이스의 스키마에서 다른 지 여부를 확인 응용 프로그램이 실행 될 때마다가 있도록를 연결 하려는 클래스입니다. 경우에 모델과 일치 하 고 샘플 데이터를 사용 하 여 데이터베이스를 채우는 다음 데이터베이스를 다시 만들려면 이니셜라이저를 실행할 수 있습니다.

엽니다는 *Global.asax* 의 루트에 있는 파일을 `MvcMovies` 프로젝트:

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

*Global.asax* 프로젝트에 대 한 전체 응용 프로그램을 정의 하 고 포함 하는 클래스를 포함 하는 파일을 `Application_Start` 응용 프로그램을 처음 시작할 때 실행 되는 이벤트 처리기입니다.

두 개를 추가 해 보겠습니다 using 문을 파일의 맨 위로 이동 합니다. Entity Framework 네임 스페이스를 참조 하는 첫 번째 및 두 번째 네임 스페이스를 참조 합니다. 여기서는 `MovieInitializer` 삶을 클래스:

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

찾을 합니다 `Application_Start` 메서드 호출을 추가 하 고 `Database.SetInitializer` 아래와 같이 메서드의 시작 부분에서:

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

`Database.SetInitializer` 방금 추가한 문을 나타냅니다 데이터베이스에서 사용 하는 `MovieDBContext` 인스턴스를 자동으로 삭제 하 고 일치 하지 않으면 스키마 및 데이터베이스를 다시 생성 해야 합니다. 에 지정 된 샘플 데이터로 데이터베이스도 채웁니다 살펴본 것 처럼 및는 `MovieInitializer` 클래스입니다.

닫기 합니다 *Global.asax* 파일입니다.

응용 프로그램을 다시 실행 하 고 이동 합니다 */Movies* URL입니다. 응용 프로그램이 시작 되 면 모델 구조 데이터베이스 스키마를 더 이상 일치 하는지 검색 합니다. 자동으로 새 모델 구조와 일치 하도록 데이터베이스를 다시 생성 하 고 샘플 영화를 사용 하 여 데이터베이스를 채웁니다.

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

클릭 합니다 **새로 만들기** 새 영화를 추가 합니다. 참고 등급을 추가할 수 있습니다.

[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)

**만들기**를 클릭합니다. 등급을 포함 하 여 새 동영상을는 이제 영화 목록에 표시 합니다.

[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)

이 섹션에서는 모델 개체를 수정 및 변경 내용과 동기화 데이터베이스를 유지 하는 방법을 살펴보았습니다. 시나리오를 시도해 볼 수 있도록 샘플 데이터를 사용 하 여 새로 만든된 데이터베이스를 채우는 방법을 알아보았습니다. 다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 될 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)
