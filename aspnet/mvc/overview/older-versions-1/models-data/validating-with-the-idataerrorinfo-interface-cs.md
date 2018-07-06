---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: IDataErrorInfo 인터페이스 (C#)를 사용 하 여 유효성 검사 | Microsoft Docs
author: StephenWalther
description: Stephen walther가 모델 클래스에서 IDataErrorInfo 인터페이스를 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: d3d3e379e5b2cfdd1385d724c0d9bf2a83ce339a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836029"
---
<a name="validating-with-the-idataerrorinfo-interface-c"></a>IDataErrorInfo 인터페이스 (C#)를 사용 하 여 유효성 검사
====================
[Stephen walther가](https://github.com/StephenWalther)

> Stephen walther가 모델 클래스에서 IDataErrorInfo 인터페이스를 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법은 설명 합니다. 사용자가 필요한 양식 필드에 대 한 값을 제공 하지 않고 HTML 폼을 제출 하지 못하도록 하는 방법에 알아봅니다. 이 자습서에서는 IErrorDataInfo 인터페이스를 사용 하 여 유효성 검사를 수행 하는 방법을 알아봅니다.

## <a name="assumptions"></a>Assumptions

이 자습서에서는 영화 데이터베이스 테이블과 MoviesDB 데이터베이스 사용 하겠습니다. 이 테이블에는 다음 열에 있습니다.

<a id="0.5_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | Int | False |
| 제목 | Nvarchar(100) | False |
| 책임자 | Nvarchar(100) | False |
| DateReleased | DateTime | False |


이 자습서에서는을 사용 하 여 Microsoft Entity Framework 내 데이터베이스 모델 클래스를 생성 합니다. Entity Framework에서 생성 되는 영화 클래스는 그림 1에 표시 됩니다.


[![영화 엔터티](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)

**그림 01**:는 영화 엔터티 ([큰 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))


> [!NOTE] 
> 
> Entity Framework를 사용 하 여 데이터베이스 모델 클래스를 생성 하는 방법에 대 한 자세한 내용은 참조 내 자습서 Entity Framework를 사용 하 여 모델 클래스 만들기.


## <a name="the-controller-class"></a>컨트롤러 클래스

목록 영화는 Home 컨트롤러를 사용 하 고 새 영화를 만듭니다. 이 클래스에 대 한 코드는 목록 1에 포함 됩니다.

**1-controllers\ homecontroller.cs를 나열합니다.**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

목록 1에서 Home 컨트롤러 클래스는 두 create () 동작을 포함 합니다. 첫 번째 작업에서는 새 동영상을 만들기 위한 HTML 폼을 표시 합니다. 두 번째 create () 작업을 데이터베이스에 새 동영상의 실제 삽입을 수행합니다. 두 번째 create () 작업은 첫 번째 create () 작업에 의해 표시 된 폼이 서버로 제출 되 면 호출 됩니다.

두 번째 create () 작업에 다음 코드 줄이 포함 되어 있는지 확인 합니다.

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

IsValid 속성 유효성 검사 오류가 있을 때 false를 반환 합니다. 이 경우 영화를 만들기 위한 HTML 양식을 포함 하는 Create view 다시 표시 됩니다.

## <a name="creating-a-partial-class"></a>Partial 클래스 만들기

영화 클래스는 Entity Framework에 의해 생성 됩니다. 솔루션 탐색기 창에서 MoviesDBModel.edmx 파일을 확장 하 고 MoviesDBModel.Designer.cs 파일을 코드 편집기에서 엽니다 영화 클래스에 대 한 코드를 볼 수 있습니다 (그림 2 참조).


[![영화 엔터티에 대 한 코드](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)

**그림 02**: 영화 엔터티에 대 한 코드 ([큰 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))


영화 클래스가 partial 클래스가입니다. 즉,을 영화 클래스의 기능을 확장 하는 동일한 이름 가진 다른 partial 클래스를 추가할 수 있습니다. 새 partial 클래스에 유효성 검사 논리를 추가 합니다.

Models 폴더에 2 목록에서 클래스를 추가 합니다.

**2-Models\Movie.cs 나열**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

목록 2의 클래스를 포함 합니다 *부분* 한정자입니다. 이 클래스를 추가 하는 속성이 나 메서드는 Entity Framework에서 생성 되는 영화 클래스의 일부가 됩니다.

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>OnChanging 및 OnChanged 부분 메서드를 추가합니다.

Entity Framework는 엔터티 클래스를 생성할 때 Entity Framework 부분 메서드를 클래스에 자동으로 추가 합니다. Entity Framework 클래스의 각 속성에 해당 하는 OnChanging 및 OnChanged 부분 메서드를 생성 합니다.

Entity Framework 영화 클래스의 경우 다음 메서드를 만듭니다.

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

해당 속성이 변경 되기 전에 OnChanging 메서드 오른쪽 라고 합니다. OnChanged 메서드 속성을 변경한 후 올바른 호출 됩니다.

영화 클래스에 유효성 검사 논리를 추가 하려면 이러한 부분 메서드를 활용할 수 있습니다. 보기 3의 영화 클래스 업데이트 제목 및 Director 속성을 비어 있지 않은 값을 할당 되어 있는지 확인 합니다.

> [!NOTE] 
> 
> 부분 메서드는 구현에 필요 없는 클래스에 정의 된 메서드입니다. 부분 메서드를 구현 하지 않으면 그런 다음 컴파일러는 메서드 시그니처를 제거 하 고 없으므로 메서드에 대 한 모든 호출 되는 부분 메서드와 관련 된 런타임 비용이 없습니다. Visual Studio 코드 편집기에서 키워드를 입력 하 여 부분 메서드를 추가할 수 있습니다 *부분* 뒤에 공간을 구현 하는 부분 목록을 봅니다.


**3-Models\Movie.cs 나열**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

예를 들어 Title 속성에 빈 문자열을 할당 하려고 하면 다음 오류 메시지에 할당 됩니다 라는 사전 \_오류입니다.

이 시점에서 실제로 때 아무 작업도 Title 속성에 빈 문자열을 할당 하 고 오류가 추가 됩니다 개인 \_오류 필드입니다. 이러한 유효성 검사 오류는 ASP.NET MVC 프레임 워크를 노출 하는 IDataErrorInfo 인터페이스를 구현 해야 합니다.

## <a name="implementing-the-idataerrorinfo-interface"></a>IDataErrorInfo 인터페이스를 구현합니다.

IDataErrorInfo 인터페이스를 첫 번째 버전부터.NET framework의 일부가 되었습니다. 이 인터페이스는 매우 단순한 인터페이스입니다.

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

클래스는 IDataErrorInfo 인터페이스를 구현 하는 경우에 ASP.NET MVC 프레임 워크 클래스의 인스턴스를 만들 때이 인터페이스를 사용 합니다. 예를 들어 Home 컨트롤러 create () 작업은 영화 클래스의 인스턴스를 수락합니다.

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

ASP.NET MVC 프레임 워크는 모델 바인더 (DefaultModelBinder)를 사용 하 여 create () 작업에 전달 하 여 동영상의 인스턴스를 만듭니다. 모델 바인더는 동영상 개체의 인스턴스를 HTML 양식 필드를 바인딩하여 동영상 개체의 인스턴스를 만들지는 일을 담당 합니다.

DefaultModelBinder 클래스는 IDataErrorInfo 인터페이스를 구현 하는지 여부를 검색 합니다. 클래스는이 인터페이스를 구현 하는 경우 모델 바인더는 클래스의 각 속성에 대 한 IDataErrorInfo.this 인덱서를 호출 합니다. 인덱서는 오류 메시지를 반환 하는 경우 모델 바인더는 상태를 자동으로 모델에이 오류 메시지를 추가 합니다.

또한는 DefaultModelBinder IDataErrorInfo.Error 속성을 확인합니다. 이 속성을 클래스와 연결 된 비 속성 특정 유효성 검사 오류를 나타내는 것입니다. 예를 들어, 다음 동영상 클래스의 여러 속성의 값에 따라 달라 지는 유효성 검사 규칙을 적용 하는 것이 좋습니다. 이 경우 오류 속성에서 유효성 검사 오류를 반환 합니다.

목록 4의 업데이트 된 영화 클래스는 IDataErrorInfo 인터페이스를 구현합니다.

**4-Models\Movie.cs (IDataErrorInfo 구현)를 나열 합니다.**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

인덱서 속성 확인 목록 4에는 \_errors 컬렉션 속성 이름에 해당 되는 키에 포함 되어 있는지 확인 하는 인덱서를 전달 합니다. 속성과 연결 된 유효성 검사 오류가 없는 경우 빈 문자열이 반환 됩니다.

홈 컨트롤러 수정 된 영화 클래스를 사용 하는 어떤 방식으로든에서 수정할 필요가 없습니다. 그림 3에 표시 되는 페이지 제목 또는 Director 양식 필드에 없는 값을 입력 하는 경우를 보여 줍니다.


[![작업 메서드를 자동으로 만들기](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)

**그림 03**: 값이 누락 된 폼 ([큰 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))


DateReleased 값은 자동으로 유효성 검사는 알 수 있습니다. 있으므로 DateReleased 속성이 NULL 값을 허용 하지 않습니다는 DefaultModelBinder 생성이 속성에 대 한 유효성 검사 오류를 자동으로 값에 없는 경우. 사용자 지정 모델 바인더를 생성 해야 하는 다음 DateReleased 속성에 대 한 오류 메시지를 수정 하려면.

## <a name="summary"></a>요약

이 자습서에서는 IDataErrorInfo 인터페이스를 사용 하 여 유효성 검사 오류 메시지를 생성 하는 방법을 알아보았습니다. 먼저 Entity Framework에서 생성 된 partial 영화 클래스의 기능을 확장 하는 부분 영화 클래스를 만들었습니다. 다음으로, 유효성 검사 논리 영화 클래스 OnTitleChanging() 및 OnDirectorChanging() 부분 메서드를 추가 했습니다. 마지막으로 ASP.NET MVC 프레임 워크에 이러한 유효성 검사 메시지를 노출 하기 위해 IDataErrorInfo 인터페이스를 구현 합니다.

> [!div class="step-by-step"]
> [이전](performing-simple-validation-cs.md)
> [다음](validating-with-a-service-layer-cs.md)
