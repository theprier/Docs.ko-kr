---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: "유효성 검사 (C#) 모델에 추가 | Microsoft Docs"
author: Rick-Anderson
description: "컨트롤러 만들기"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: a1d6a6468a39f31c3af8779abbbced093288773c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adding-validation-to-the-model-c"></a>모델 (C#)에 유효성 검사 추가
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


이 섹션에서는 유효성 검사 논리를 추가 합니다는 `Movie` 모델과 하면 사용자가 만들거나 응용 프로그램을 사용 하 여 동영상을 편집 하는 언제 든 지 유효성 검사 규칙이 적용 되도록 유지 됩니다.

## <a name="keeping-things-dry"></a>건조 구성을

ASP.NET MVC의 핵심 디자인 개념 중 하나 드라이 ("하지 않는 반복 직접")입니다. ASP.NET MVC 기능 또는 동작을 한 번만 지정 한 다음 응용 프로그램에 everywhere 반영 하는 것이 권장 합니다. 이를 작성 해야 하는 코드의 양을 줄이고 유지 하기 위해 훨씬 쉽게 작성 하는 코드를 만들기.

ASP.NET MVC 및 Entity Framework Code First 제공 하는 유효성 검사 지원은 동작의 건조 원칙의 좋은 예입니다. (모델 클래스)의 한 지점에서 유효성 검사 규칙을 선언적으로 지정할 수 있습니다 및 다음 해당 규칙이 응용 프로그램의 모든 위치에서 적용 됩니다.

있습니다 사용할 수 있는 방법을이 유효성 검사 지원의 영화 응용 프로그램에서 살펴보겠습니다.

## <a name="adding-validation-rules-to-the-movie-model"></a>영화 모델에 유효성 검사 규칙 추가

일부 유효성 검사 논리를 추가 하 여 먼저는 `Movie` 클래스입니다.

*Movie.cs* 파일을 엽니다. 추가 `using` 문을 참조 하는 파일 맨 위에 있는 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) 네임 스페이스:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

네임 스페이스에는.NET Framework의 일부입니다. 모든 클래스 또는 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 된 집합을 제공 합니다.

이제 업데이트 된 `Movie` 클래스는 기본 제공 기능을 활용 하려면 [ `Required` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.requiredattribute.aspx), [ `StringLength` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), 및 [ `Range` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성 . 특성을 적용 대상의 예를 들어 다음 코드를 사용 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다. `Required` 특성 나타냅니다 속성 값을 가져야 합니다;이 샘플에서는 동영상은에 대 한 값은 `Title`, `ReleaseDate`, `Genre`, 및 `Price` 유효 하려면 속성입니다. `Range` 특성은 지정된 범위 내의 값을 제한합니다. `StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 필요에 따라 최소 길이를 설정할 수 있습니다.

코드는 먼저 응용 프로그램 데이터베이스에 변경 내용을 저장 하기 전에 모델 클래스에서 지정 된 유효성 검사 규칙 적용 되도록 보장 합니다. 예를 들어 아래 코드는 예외를 throw 할 때는 `SaveChanges` 메서드는, 여러 필요 하기 때문에 `Movie` 속성 값이 누락 되 고 가격 기본값은 0 (이 범위를 벗어났습니다).

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

.NET Framework에 의해 자동으로 적용 하는 유효성 검사 규칙을 만드는 것 사용 하면 확인 응용 프로그램 보다 강력 합니다. 또한 유효성 검사를 잊거나, 데이터베이스에 불량 데이터가 실수로 들어가지 않게 할 수 있습니다.

다음은 업데이트 된 항목에 대 한 전체 코드 *Movie.cs* 파일:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC에서 UI 유효성 검사 오류

응용 프로그램을 다시 실행을 탐색 하 고 */Movies* URL입니다.

클릭는 **만들 영화** 새 동영상을 추가 하는 링크입니다. 일부 잘못 된 값으로 양식을 작성 한 다음 클릭는 **만들기** 단추입니다.

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

어떻게 폼이 자동으로를 사용 하는 배경색 각 옆에 있는 적절 한 유효성 검사 오류 메시지가 방사 및 잘못 된 데이터를 포함 하는 텍스트 상자에 강조 표시를 확인 합니다. 주석이 지정 하면 지정 된 오류 문자열은 일치 하는 오류 메시지는 `Movie` 클래스입니다. 오류 (경우에 사용자가 JavaScript를 사용 하지 않도록 설정) (JavaScript 사용) 하는 클라이언트 쪽 및 서버측 모두 적용 됩니다.

실제 혜택은 한 줄의 코드를 변경 해야 하지 않은 `MoviesController` 클래스 또는 *Create.cshtml* UI이 유효성이 검사를 사용 하도록 설정 하려면 보기. 컨트롤러 및 자동으로이 자습서의 앞부분에서 만든 보기에서 특성을 사용 하 여 지정 된 유효성 검사 규칙을 받아서는 `Movie` 모델 클래스입니다.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>만들기 확인 하 고 작업 메서드를 작성할 유효성 검사에서 발생 하는 방법

컨트롤러나 보기에서 코드에 대한 업데이트 없이 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다. 다음 목록에서는 `Create` 의 메서드는 `MovieController` 클래스 표시 합니다. 만든 방법으로이 자습서의 앞부분에 나오는 것에서 변경 하기가 되지 않습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

첫 번째 작업 메서드 초기 만들기 폼이 표시 됩니다. 두 번째 폼 post를 처리 합니다. 두 번째 `Create` 메서드 호출 `ModelState.IsValid` 동영상에 모든 유효성 검사 오류가 있는지 확인 합니다. 이 메서드 호출에서는 개체에 적용된 모든 유효성 검사 특성을 평가합니다. 개체 유효성 검사 오류가 있으면는 `Create` 메서드 다시 표시 되 고 있습니다. 오류가 없으면 메서드가 데이터베이스에 새 동영상을 저장합니다.

다음은 이러한는 *Create.cshtml* 자습서의 앞부분에 나오는 스 캐 폴드 된 템플릿 보기. 이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

코드 사용 하는 여는 `Html.EditorFor` 출력 하는 도우미는 `<input>` 요소 각각에 대해 `Movie` 속성. 이 도우미 옆에 대 한 호출 되는 `Html.ValidationMessageFor` 도우미 메서드입니다. 이러한 두 개의 도우미 메서드를 보기에는 컨트롤러에 의해 전달 되는 모델 개체 사용 (이 경우는 `Movie` 개체). 적절 하 게 모델 및 표시 오류 메시지에 지정 된 유효성 검사 특성에 대 한 자동으로 검색 합니다.

이 방법에 대 한 훌륭한은 컨트롤러도 아니고 만들기 보기 템플릿이 알고 있는 아무 것도 표시 되는 특정 오류 메시지 또는 적용을 실제 유효성 검사 규칙에 대 한입니다. 유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다.

유효성 검사 논리를 나중에 변경 하려는 경우 정확 하 게 한 곳에서 그렇게 할 수 있습니다. 모든 유효성 검사 논리가 한 곳에 정의되어 모든 곳에서 사용되므로 응용 프로그램의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다. 이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다. 수 있음을 의미 하 고 완전히 건조 원칙을 적용 합니다.

## <a name="adding-formatting-to-the-movie-model"></a>영화 모델에 서식 추가

*Movie.cs* 파일을 엽니다. [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) 네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에 서식 특성을 제공 합니다. 적용 하는 [ `DisplayFormat` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성 및 [ `DataType` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 출시 날짜에 시작 및 끝 price 필드 열거형 값입니다. 다음 코드는 `ReleaseDate` 및 `Price` 는 적절 한 속성 [ `DisplayFormat` ](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성입니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

명시적으로 설정 수 또는 [ `DataFormatString` ](https://msdn.microsoft.com/en-us/library/system.string.format.aspx) 값입니다. 다음 코드와 날짜 형식 문자열을 사용 하 여 릴리스 날짜 속성 (즉, "d"). 않으려면 시간 릴리스 날짜의 일환으로 지정 하려면이 사용 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

다음 코드 형식에서 `Price` 통화로 속성입니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

전체 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러입니다.

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

이 시리즈의 다음 부분에서는 응용 프로그램을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.

>[!div class="step-by-step"]
[이전](adding-a-new-field.md)
[다음](improving-the-details-and-delete-methods.md)
