---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: "간단한 유효성 검사 (VB)를 수행 합니다. | Microsoft Docs"
author: StephenWalther
description: "ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 소개 모델 상태 및 유효성 검사 HTML 도우미 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bc4cdbcd267bcdd3e71abc4c52664ae62c5c02e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="performing-simple-validation-vb"></a>간단한 유효성 검사 (VB)를 수행합니다.
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 모델 상태 수 및 HTML 유효성 검사 도우미를 소개합니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하는 방법에 대해 설명 하는입니다. 예를 들어 필수 필드에 대 한 값을 포함 하지 않는 폼이 전송에서 다른 사용자를 방지 하는 방법을 배웁니다. 모델 상태 및 유효성 검사 HTML 도우미를 사용 하는 방법을 배웁니다.

## <a name="understanding-model-state"></a>모델 상태 이해

유효성 검사 오류를 나타내기 위해 모델 상태-또는-모델 상태 사전에서 보다 정확 하 게 사용 합니다. 예를 들어 create () 동작 목록 1의 데이터베이스에 제품 클래스를 추가 하기 전에 제품 클래스의 속성을 확인 합니다.


필자가 하지 추천 컨트롤러에 데이터베이스 또는 유효성 검사 논리를 추가 합니다. 컨트롤러 응용 프로그램 흐름 제어와 관련 된 논리만 포함 되어야 합니다. 바로 가기를 간단 하 게 수행 합니다.


**1-Controllers\ProductController.vb 나열**

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

목록 1의 제품 클래스의 이름, 설명 및 UnitsInStock 속성 유효성이 검사 됩니다. 이러한 속성 중 하나라도 실패 한 유효성 검사 테스트 오류가 (컨트롤러 클래스의 ModelState 속성에 의해 표현 됨) 모델 상태 사전에 추가 됩니다.

모델 상태에서 오류가 경우 ModelState.IsValid 속성이 false 반환 합니다. 이 경우 새 제품을 만들기 위한 HTML 폼 다시 표시 됩니다. 그렇지 않으면 유효성 검사 오류가 있을 경우 새 제품 데이터베이스에 추가 됩니다.

## <a name="using-the-validation-helpers"></a>유효성 검사 도우미를 사용 하 여

ASP.NET MVC 프레임 워크에는 두 명의 유효성 검사 도우미가 포함 되어: Html.ValidationMessage() 도우미와 Html.ValidationSummary() 도우미입니다. 보기에서 이러한 두 도우미 클래스를 사용 하 여 유효성 검사 오류 메시지를 표시 합니다.

Html.ValidationMessage() 및 Html.ValidationSummary() 도우미 ASP.NET MVC 스 캐 폴딩 하 여 자동으로 생성 되는 뷰 만들기 및 편집에에서 사용 됩니다. 만들기 뷰를 생성 하려면 다음이 단계를 수행 합니다.

1. 제품 컨트롤러에서 create () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 1 참조).
2. 에 **뷰 추가** 대화 상자에서 확인란 확인 **강력한 형식의 뷰 만들기** (그림 2 참조).
3. **데이터 클래스 보기** 드롭다운 목록에서 Product 클래스를 선택 합니다.
4. **콘텐츠를 볼** 드롭다운 목록에서 만들기를 선택 합니다.
5. **추가** 단추를 클릭합니다.


뷰를 추가 하기 전에 응용 프로그램을 작성 하 고 있는지 확인 합니다. 클래스의 목록에 나타나지 않습니다는 그렇지 않은 경우는 **데이터 클래스 보기** 드롭다운 목록입니다.


[![새 프로젝트 대화 상자](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)

**그림 01**: 뷰 추가 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image2.png))


[![새 프로젝트 대화 상자](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)

**그림 02**: 강력한 형식의 뷰 만들기 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image4.png))


다음이 단계를 완료 한 후에 목록 2의 만들기 뷰를 가져옵니다.

**2-Views\Product\Create.aspx 나열**

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

목록 2 Html.ValidationSummary() 도우미 HTML 폼 위에 바로 호출 됩니다. 이 도우미는 유효성 검사 오류 메시지 목록을 표시 하는 데 사용 됩니다. Html.ValidationSummary() 도우미 글머리 기호 목록에서 오류를 렌더링합니다.

각 HTML 폼 필드 옆에 있는 Html.ValidationMessage() 도우미 라고 합니다. 이 도우미는 양식 필드 오른쪽에 오류 메시지를 표시 하는 데 사용 됩니다. 목록 2의 경우는 오류가 있을 때 Html.ValidationMessage() 도우미는 별표를 표시 합니다.

그림 3에 있는 페이지는 누락 된 필드와 잘못 된 값이 폼이 전송 될 때 유효성 검사 도우미에서 렌더링 오류 메시지를 보여 줍니다.


[![새 프로젝트 대화 상자](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)

**그림 03**: 제출 된 문제는 Create view ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image6.png))


HTML의 모양을 필드는 유효성 검사 오류가 있을 때에 수정 됩니다 입력 있는지 확인 합니다. Html.TextBox() 도우미 렌더링 되는 *클래스 "입력 유효성 검사 오류" =* 특성 유효성 검사 오류가 있을 때 속성에 연결 된 Html.TextBox() 도우미에서 렌더링 합니다.

다음 세 가지가 연계 스타일 시트의 유효성 검사 오류 표시 모양을 제어 하는 데 사용 합니다.

- 입력-유효성 검사 오류-에 적용 된 &lt;입력&gt; Html.TextBox() 도우미에서 렌더링 되는 태그입니다.
- 에 적용 된 필드-유효성 검사 오류-는 &lt;걸쳐&gt; Html.ValidationMessage() 도우미에서 렌더링 되는 태그입니다.
- 유효성 검사-요약 오류-적용할는 &lt;ul&gt; Html.ValidationSumamry() 도우미에서 렌더링 되는 태그입니다.

이러한 연계 스타일 시트 클래스를 수정 하 고 따라서 콘텐츠 폴더에 있는 Site.css 파일을 수정 하 여 유효성 검사 오류의 모양을 수정할 수 있습니다.

> [!NOTE] 
> 
> HtmlHelper 클래스 CSS 관련 유효성 검사의 이름 검색에 대 한 읽기 전용 정적 속성에 포함 되어 클래스입니다. 이러한 정적 속성에는 ValidationInputCssClassName, ValidationFieldCssClassName, 및 ValidationSummaryCssClassName 이름이 지정 됩니다.


## <a name="prebinding-validation-and-postbinding-validation"></a>유효성 검사 및 Postbinding prebinding

제품을 만들기 위한 HTML 폼을 제출 하는 경우 price 필드 및 UnitsInStock 필드에 대 한 값에 대 한 잘못 된 값을 입력 하면 그림 4에 표시 되는 유효성 검사 메시지를 얻을 수 있습니다. 이러한 유효성 검사 오류 메시지에서 제공 않은 위치


[![새 프로젝트 대화 상자](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)

**그림 04**: Prebinding 유효성 검사 오류 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image8.png))


실제로 두 가지 유형의 HTML 양식 필드는 클래스에 바인딩되고 양식 필드는 클래스에 바인딩된 후에 생성 된 전에 생성 된 유효성 검사 오류 메시지-있습니다. 즉,는 prebinding 유효성 검사 오류 및 유효성 검사 오류 postbinding 합니다.

목록 1의 제품 컨트롤러에 의해 노출 되는 create () 동작 제품 클래스의 인스턴스를 허용 합니다. Create 메서드 시그니처는 다음과 같습니다.

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

모델 바인더를 호출 하는 방식으로 폼 만들기에서에서 HTML 폼 필드의 값 productToCreate 클래스에 바인딩됩니다. 기본 모델 바인더 오류 메시지가 모델 상태를 자동으로 때 추가 된 양식 필드 형식 속성에 바인딩할 수 없습니다.

기본 모델 바인더에서는 문자열 "apple"를 제품 클래스의 가격 속성에 바인딩할 수 없습니다. 10 진수 속성에 문자열을 할당할 수 없습니다. 따라서, 모델 바인더 모델 상태에 오류를 추가 합니다.

기본 모델 바인더도 할당할 수 없습니다 값 아무 것도 사용할 수 없는 값 Nothing 속성. 특히, 모델 바인더에 할당할 수 없습니다 값 아무 UnitsInStock 속성입니다. 다시 한 번, 모델 바인더를 포기 하 고 모델 상태 오류 메시지가 추가 됩니다.

Prebinding 오류 메시지를 이러한 모양을 사용자 지정 하려는 경우 이러한 메시지에 대 한 리소스 문자열을 만들 해야 합니다.

## <a name="summary"></a>요약

이 자습서의 목표는 ASP.NET MVC 프레임 워크에서 유효성 검사의 기본 메커니즘에 설명 하는 것 이었습니다. 모델 상태 및 유효성 검사 HTML 도우미를 사용 하는 방법을 배웠습니다. 유효성 검사 postbinding prebinding 간 구분을 논의 합니다. 다른 자습서에 모델 클래스를 컨트롤러에 유효성 검사 코드를 이동 하기 위한 다양 한 방법에 설명 합니다.

>[!div class="step-by-step"]
[이전](displaying-a-table-of-database-data-vb.md)
[다음](validating-with-the-idataerrorinfo-interface-vb.md)
