---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 데이터 주석 유효성 검사기 (VB)와 유효성 검사 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더 활용 합니다. 다양 한 유형의 유효성 검사기를 사용 하는 방법 알아보기...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/29/2009
ms.topic: article
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: d1987182a44a0ad3f91f455342dc934d1dd50267
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870169"
---
<a name="validation-with-the-data-annotation-validators-vb"></a>데이터 주석 유효성 검사기 (VB)와 유효성 검사
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더 활용 합니다. 다양 한 유형의 유효성 검사기 특성을 사용 하 고 Microsoft Entity Framework에서 사용 하는 방법에 알아봅니다.


이 자습서에서는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하려면 데이터 주석 유효성 검사기를 사용 하는 방법에 설명 합니다. 데이터 주석 유효성 검사기를 사용은 필수와 같은 하나 이상의 특성 – 또는 StringLength 특성을 추가 하면 – 클래스 속성에 유효성 검사를 수행할 수 있도록 합니다.

데이터 주석 유효성 검사기를 사용 하려면 먼저 데이터 주석 모델 바인더를 다운로드 해야 합니다. 클릭 하 여 데이터 주석 모델 바인더 예제는 CodePlex 웹 사이트에서 다운로드할 수 있습니다 [여기](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)합니다.


데이터 주석 모델 바인더에서 공식 Microsoft ASP.NET MVC 프레임 워크 부분이 아닌지 이해 하는 것이 유용 합니다. 데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 팀에 의해 생성 되었지만, 공식 제품 기술 지원 데이터 주석 모델 바인더에 대 한 설명 및이 자습서에 사용 된 Microsoft 제공 하지 않습니다.


## <a name="using-the-data-annotation-model-binder"></a>데이터 주석 모델 바인더를 사용 하 여

데이터 주석 모델 바인더에서 ASP.NET MVC 응용 프로그램을 사용 하려면 먼저 Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리와 System.ComponentModel.DataAnnotations.dll 어셈블리에 대 한 참조를 추가 해야 합니다. 메뉴 옵션을 선택 **프로젝트, 참조 추가**합니다. 그런 다음 클릭는 **찾아보기** 탭를 다운로드 (하 여 압축을 푼) 데이터 주석 모델 바인더 샘플 위치로 이동 (참조 **그림 1**).

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**그림 1**: 데이터 주석 모델 바인더에 대 한 참조를 추가 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-vb/_static/image3.png))

Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리와 System.ComponentModel.DataAnnotations.dll 어셈블리를 선택 하 고 클릭는 **확인** 단추입니다.


데이터 주석 모델 바인더 사용 하 여.NET Framework 서비스 팩 1에 포함 된 System.ComponentModel.DataAnnotations.dll 어셈블리를 사용할 수 없습니다. 데이터 주석 모델 바인더 샘플 다운로드에 포함 된 System.ComponentModel.DataAnnotations.dll 어셈블리의 버전을 사용 해야 합니다.


마지막으로, DataAnnotations 모델 바인더를 Global.asax 파일에 등록 해야 합니다. 응용 프로그램에 다음 코드 줄을 추가\_start () 이벤트 처리기를 응용 프로그램\_start () 메서드는 다음과 같습니다.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

이 줄의 코드 전체 ASP.NET MVC 응용 프로그램에 대 한 기본 모델 바인더는 DataAnnotationsModelBinder 등록합니다.

## <a name="using-the-data-annotation-validator-attributes"></a>데이터 주석 유효성 검사기 특성을 사용 하 여

데이터 주석 모델 바인더를 사용 하면 유효성 검사기 특성을 사용 하면 유효성 검사를 수행 합니다. System.ComponentModel.DataAnnotations 네임 스페이스에는 다음과 같은 유효성 검사기 특성이 포함 됩니다.

- 범위는-지정된 된 범위의 값 사이 해당 속성의 값이 있는지 여부를 확인할 수 있습니다.
- ReqularExpression-를 사용 하면 속성의 값이 지정 된 정규식 패턴과 일치 하는지 여부를 검증 합니다.
- 필요한 – 필요에 따라 속성을 표시할 수 있습니다.
- StringLength-를 사용 하는 문자열 속성에 대 한 최대 길이 지정할 수 있습니다.
- 유효성 검사-모든 유효성 검사기 특성에 대 한 기본 클래스입니다.

> [!NOTE] 
> 
> 표준 유효성 검사기의 유효성 검사 요구 사항 충족 되지 않은 경우 그런 다음 항상 해야 새 유효성 검사기 특성의 기본 유효성 검사 특성에서 상속 하 여 사용자 지정 유효성 검사기 특성을 만들 수 있습니다.


Product 클래스에 **목록 1** 이러한 유효성 검사기 특성을 사용 하는 방법을 보여 줍니다. 이름, 설명 및 UnitPrice 속성 표시 해야 하는 경우. Name 속성은 10 자 미만의 문자열 길이가 있어야 합니다. 마지막으로, UnitPrice 속성 통화 금액을 나타내는 정규식 패턴을 일치 해야 합니다.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**Listing 1**: Models\Product.vb

Product 클래스에는 하나의 추가 특성을 사용 하는 방법을 보여 줍니다: / / DisplayName 특성입니다. / / DisplayName 특성을 사용 하면 오류 메시지가 표시 되는 속성 때 속성의 이름을 수정할 수 있습니다. "UnitPrice 필드는 필수" 오류 메시지를 표시 하는 대신 오류 메시지 "Price 필드는 필수" 표시할 수 있습니다.

> [!NOTE] 
> 
> 완전히 유효성 검사기에서 표시 되는 오류 메시지 사용자 지정 하려는 경우 다음과 같이 유효성 검사기의 ErrorMessage 속성에 사용자 지정 오류 메시지를 할당할 수 있습니다. `<Required(ErrorMessage:="This field needs a value!")>`


Product 클래스에 사용할 수 있습니다 **목록 1** 에서 create () 컨트롤러 작업으로 **목록 2**합니다. 모델 상태 오류를 포함 하는 경우이 컨트롤러 작업 만들기 뷰를 다시 표시 됩니다.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**Listing 2**: Controllers\ProductController.vb

마지막으로,에서 보기를 만들 수 있습니다 **목록 3** create () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 **뷰 추가**합니다. 모델 클래스로 제품 클래스와 함께 강력한 형식의 뷰를 만듭니다. 선택 **만들기** 보기 콘텐츠 드롭다운 목록에서 (참조 **그림 2**).

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**그림 2**: 만들기 뷰 추가

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**Listing 3**: Views\Product\Create.aspx

> [!NOTE] 
> 
> 에 의해 생성 된 양식 만들기에서에서 Id 필드를 제거는 **뷰 추가** 메뉴 옵션입니다. Id 열에 해당 하는 Id 필드를 때문에 사용자가을이 필드에 대 한 값을 입력 하지 않으려면입니다.


제품을 만들기 위한 양식을 전송 하면 필수 필드에 대 한 값을 입력 하지 않으면 경우 유효성 검사 오류 메시지를 **그림 3** 표시 됩니다.

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**그림 3**: 누락 된 필수 필드

잘못 된 통화 금액을 다음 오류 메시지를 입력 하면 **그림 4** 표시 됩니다.

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**그림 4**: 잘못 된 통화 금액

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>데이터 주석 유효성 검사기를 사용 하 여 Entity Framework와 함께

Microsoft Entity Framework를 사용 하는 데이터 모델 클래스를 생성 하는 경우 클래스에 직접 유효성 검사기 특성 적용할 수 없습니다. Entity Framework Designer에서는 모델 클래스를 생성 하기 때문에 모델 클래스를 적용 한 변경 내용 다음에 디자이너에서 변경 하기를 덮어쓰게 됩니다.

Entity Framework에서 생성 된 클래스와 유효성 검사기를 사용 하려면 메타 데이터 클래스를 만들 해야 합니다. 유효성 검사기 실제 클래스를 적용 하는 대신 메타 데이터 클래스에 유효성 검사기를 적용 합니다.

예를 들어, Entity Framework를 사용 하 여 영화 클래스를 만든 가정해 보겠습니다 (참조 **그림 5**). 또한 영화 제목 및 감독 속성이 필수 속성을 확인 하려면 한다고 가정 합니다. 이 경우 partial 클래스와의 메타 데이터 클래스를 만들 수 있습니다 **목록 4**합니다.

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**그림 5**: Entity Framework에서 생성 된 영화 클래스

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**Listing 4**: Models\Movie.vb

에 있는 파일 **목록 4** 동영상, 동영상 메타 데이터 라는 두 개의 클래스를 포함 합니다. 영화 클래스는 partial 클래스입니다. DataModel.Designer.vb 파일에 포함 된 Entity Framework에서 생성 되는 partial 클래스에 해당 합니다.

현재.NET framework 부분 속성을 지원 하지 않습니다. 따라서 유효성 검사기 특성에 있는 파일에 정의 된 동영상 클래스의 속성에 유효성 검사기 특성을 적용 하 여 DataModel.Designer.vb 파일에 정의 된 동영상 클래스의 속성에 적용 하려면 방법이 있으면 **목록 4**.

영화 partial 클래스 동영상 메타 데이터 클래스를 가리키는 MetadataType 특성으로 데코레이팅되 어 있는지 확인 합니다. 동영상 메타 데이터 클래스는 영화 클래스의 속성에 대 한 프록시 속성을 포함합니다.

유효성 검사기 특성 동영상 메타 데이터 클래스의 속성에 적용 됩니다. 제목, 감독 및 DateReleased 속성 모두 필수 속성으로 표시 됩니다. 감독 속성 5 대 미만의 문자가 포함 된 문자열을 할당 합니다. / / DisplayName 특성 "Date 정식 필드는 필수입니다."와 같은 오류 메시지를 표시 하려면 DateReleased 속성에 적용 되는 마지막으로, 오류 대신 "DateReleased 필수 필드가입니다."

> [!NOTE] 
> 
> 공지 동영상 메타 데이터 클래스의 프록시 속성은 영화 클래스의 해당 속성을 동일한 형식을 나타낼 필요가 없습니다. 예를 들어 Director 속성이 영화 클래스에는 문자열 속성 및 동영상 메타 데이터 클래스의 개체 속성입니다.


에 있는 페이지 **그림 6** 동영상 속성에 대 한 잘못 된 값을 입력 하는 경우 반환 된 오류 메시지를 보여 줍니다.

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**그림 6**: Entity Framework와 유효성 검사기를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더를 활용 하는 방법을 배웠습니다. 다양 한 유형의 필수 등의 유효성 검사기 특성 및 StringLength 특성을 사용 하는 방법을 배웠습니다. 또한 Microsoft Entity Framework와 함께 작업 하는 경우 이러한 특성을 사용 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](validating-with-a-service-layer-vb.md)
