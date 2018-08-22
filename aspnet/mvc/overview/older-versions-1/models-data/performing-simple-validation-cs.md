---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
title: 수행 하는 간단한 유효성 검사 (C#) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 모델 상태 및 유효성 검사 HTML 도우미를 소개 하는 중...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 21383c9d-6aea-4bad-a99b-b5f2c9d6503f
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: 14d7857c64268df3b998e05797f749f03509dd4b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828663"
---
<a name="performing-simple-validation-c"></a>간단한 유효성 검사 (C#)를 수행합니다.
====================
[Stephen walther가](https://github.com/StephenWalther)

> ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 모델 상태 수 및 HTML 유효성 검사 도우미를 소개합니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행할 수는 방법을 설명 합니다. 예를 들어 사용자가 필수 필드에 대 한 값을 포함 하지 않는 양식을 제출 하지 못하도록 하는 방법에 알아봅니다. 모델 상태 및 유효성 검사 HTML 도우미를 사용 하는 방법을 알아봅니다.

## <a name="understanding-model-state"></a>모델 상태 이해

사용 하 여 모델 상태 또는 보다 정확 하 게 된 모델 상태 사전-유효성 검사 오류를 나타냅니다. 예를 들어 create () 작업 목록 1에서 데이터베이스를 Product 클래스를 추가 하기 전에 Product 클래스의 속성을 확인 합니다.


컨트롤러에 유효성 검사 또는 데이터베이스 논리를 추가 하는 권장 하지. 컨트롤러 응용 프로그램 흐름 제어와 관련 된 논리만 포함 해야 합니다. 간단 하 게 바로 가기를 취하고 있습니다.


**1-Controllers\ProductController.cs 나열**

[!code-csharp[Main](performing-simple-validation-cs/samples/sample1.cs)]

목록 1에서 Product 클래스의 이름, 설명 및 UnitsInStock 속성 유효성이 검사 됩니다. 이러한 속성 중 하나라도 실패 한 유효성 검사 테스트는 오류 (컨트롤러 클래스의 ModelState 속성에 의해 표현 됨) 모델 상태 사전에 추가 됩니다.

모델 상태에서 오류가 경우 ModelState.IsValid 속성이 false 반환 합니다. 이 경우 새 제품을 만들기 위한 HTML 양식 다시 표시 됩니다. 그렇지 않으면 유효성 검사 오류가 없을 경우 새 제품 데이터베이스에 추가 됩니다.

## <a name="using-the-validation-helpers"></a>유효성 검사 도우미를 사용 하 여

ASP.NET MVC 프레임 워크는 두 명의 유효성 검사 도우미: Html.ValidationMessage() 도우미와 Html.ValidationSummary() 도우미입니다. 보기에서 이러한 두 도우미를 사용 하 여 유효성 검사 오류 메시지를 표시 합니다.

Html.ValidationMessage() 및 Html.ValidationSummary() 도우미 ASP.NET MVC 스 캐 폴딩을 통해 자동으로 생성 되는 만들기 및 편집 보기에 사용 됩니다. 만들기 뷰를 생성 하려면 다음이 단계를 수행 합니다.

1. 제품 컨트롤러에서 create () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 1 참조).
2. 에 **뷰 추가** 대화 상자에서 레이블이 지정 된 확인란 **강력한 형식의 뷰를 만들** (그림 2 참조).
3. **데이터 클래스 보기** 드롭다운 목록에서 Product 클래스를 선택 합니다.
4. **콘텐츠 보기** 드롭다운 목록에서 만들기를 선택 합니다.
5. **추가** 단추를 클릭합니다.


뷰를 추가 하기 전에 응용 프로그램을 빌드하는 것이 있는지 확인 합니다. 클래스 목록에 나타나지이 고, 그렇지 합니다 **데이터 클래스 보기** 드롭다운 목록입니다.


[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)

**그림 01**: 뷰 추가 ([큰 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image2.png))


[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)

**그림 02**: 강력한 형식의 뷰 만들기 ([큰 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image4.png))


다음이 단계를 완료 한 후에 목록 2에서 만들기 뷰를 가져옵니다.

**2-Views\Product\Create.aspx 나열**

[!code-aspx[Main](performing-simple-validation-cs/samples/sample2.aspx)]

목록 2에서 Html.ValidationSummary() 도우미는 HTML 폼 위에 즉시 호출 됩니다. 이 도우미는 유효성 검사 오류 메시지 목록을 표시 하는 데 사용 됩니다. Html.ValidationSummary() 도우미 글머리 기호 목록에서 오류를 렌더링합니다.

Html.ValidationMessage() 도우미는 HTML 폼 필드의 각 항목 옆에 있는 호출 됩니다. 이 도우미는 폼 필드 오른쪽에 오류 메시지를 표시 하는 데 사용 됩니다. 목록 2의 경우 Html.ValidationMessage() 도우미 오류가 발생 하는 경우 별표를 표시 합니다.

그림 3에 있는 페이지에는 누락 된 필드와 값이 잘못 된 양식이 제출 되 면 유효성 검사 도우미에서 렌더링 하는 오류 메시지를 보여 줍니다.


[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)

**그림 03**: 문제가 있는 제출 The Create view ([큰 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image6.png))


HTML의 모양을 입력 필드는 유효성 검사 오류가 있을 때에 수정 하는 것을 확인 합니다. Html.TextBox() 도우미 렌더링을 *클래스 "입력 유효성 검사 오류" =* 유효성 검사 오류가 있을 경우 특성 속성에 연결 된 Html.TextBox() 도우미에서 렌더링 합니다.

세 가지 연계 스타일 시트 클래스 유효성 검사 오류의 모양을 제어 하는 데 사용 합니다.

- 입력-유효성 검사-error-적용 된 &lt;입력&gt; Html.TextBox() 도우미에 의해 렌더링 된 태그입니다.
- 필드-유효성 검사-error-적용 된 &lt;s p a n&gt; Html.ValidationMessage() 도우미에 의해 렌더링 된 태그입니다.
- 유효성 검사-요약-오류-를 적용 합니다 &lt;ul&gt; Html.ValidationSumamry() 도우미에 의해 렌더링 된 태그입니다.

이러한 연계 스타일 시트 클래스를 수정 하 고 따라서 콘텐츠 폴더에 있는 Site.css 파일을 수정 하 여 모양의 유효성 검사 오류를 수정할 수 있습니다.

> [!NOTE] 
> 
> HtmlHelper 클래스와 관련 된 CSS 유효성 검사의 이름을 검색에 대 한 읽기 전용 정적 속성을 포함 클래스입니다. 이러한 정적 속성에는 ValidationInputCssClassName, ValidationFieldCssClassName, 및 ValidationSummaryCssClassName 이름이 지정 됩니다.


## <a name="prebinding-validation-and-postbinding-validation"></a>Prebinding 유효성 검사 및 Postbinding 유효성 검사

제품을 만들기 위한 HTML 양식을 전송 하면 가격 필드와 UnitsInStock 필드에 대 한 값이 없는 잘못 된 값을 입력 하 고 하는 경우 그림 4에 표시 되는 유효성 검사 메시지를 얻을 수 있습니다. 수행할 유효성 검사 오류 메시지에 이러한 출처에서?


[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)

**그림 04**: Prebinding 유효성 검사 오류 ([큰 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image8.png))


실제로 두 가지 유형의 HTML 양식 필드는 클래스에 바인딩되고 양식 필드 클래스에 바인딩된 후에 생성 된 전에 생성 된 유효성 검사 오류 메시지-있습니다. 즉, prebinding 유효성 검사 오류 및 유효성 검사 오류 postbinding 합니다.

Create () 작업 목록 1에서 제품 컨트롤러에 의해 노출 된 Product 클래스의 인스턴스를 허용 합니다. Create 메서드의 시그니처는 다음과 같습니다.

[!code-csharp[Main](performing-simple-validation-cs/samples/sample3.cs)]

만들기 폼에서 HTML 폼 필드의 값에서 모델 바인더에 잠깐 productToCreate 클래스에 바인딩됩니다. 기본 모델 바인더 오류 메시지가 모델 상태를 자동으로 때 추가 양식 필드를 폼 속성을 바인딩할 수 없습니다.

기본 모델 바인더에서는 문자열 "apple"를 Product 클래스의 가격 속성에 바인딩할 수 없습니다. 10 진수 속성에 문자열을 할당할 수 없습니다. 따라서 모델 바인더 모델 상태 오류를 추가합니다.

또한 기본 모델 바인더를 null을 허용 하지 않는 속성에 null 값을 할당할 수 없습니다. 특히, 모델 바인더는 UnitsInStock 속성에 null 값을 할당할 수 없습니다. 이번에 모델 바인더를 포기 하 고 모델 상태 오류 메시지를 추가 합니다.

Prebinding 오류 메시지를 이러한 모양을 사용자 지정 하려는 경우 이러한 메시지에 대 한 리소스 문자열을 만들 해야 합니다.

## <a name="summary"></a>요약

이 자습서의 목표는 ASP.NET MVC 프레임 워크에서 유효성 검사의 기본 메커니즘을 설명 하는 것 이었습니다. 모델 상태 및 유효성 검사 HTML 도우미를 사용 하는 방법을 알아보았습니다. Prebinding 및 유효성 검사 postbinding 구분도 설명 했습니다. 다른 자습서에 컨트롤러 및 모델 클래스에 유효성 검사 코드를 이동 하기 위한 다양 한 전략을 하겠습니다.

> [!div class="step-by-step"]
> [이전](displaying-a-table-of-database-data-cs.md)
> [다음](validating-with-the-idataerrorinfo-interface-cs.md)
