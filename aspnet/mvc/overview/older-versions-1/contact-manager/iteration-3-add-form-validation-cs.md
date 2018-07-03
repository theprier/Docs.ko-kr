---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: '반복 #3-양식 유효성 검사 추가 (C#) | Microsoft Docs'
author: microsoft
description: 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 emai 유효성을 검사 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: a76e75f2d343764038142235c92e2db04e807778
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377008"
---
<a name="iteration-3--add-form-validation-c"></a>반복 #3-양식 유효성 검사 추가 (C#)
====================
[Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (C#)
  

이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다. 연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.

여러 반복에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-보기 좋게 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다. 예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 #6-테스트 중심 개발을 사용 합니다. 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복에서는 메일 그룹을 추가합니다.

- 반복 #7 – Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.


## <a name="this-iteration"></a>이 반복

연락처 관리자 응용 프로그램의이 두 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드에 대 한 값을 입력 하지 않고 연락처를 제출 합니다. 또한 전화 번호 및 전자 메일 주소 (그림 1 참조) 유효성을 검사 합니다.


[![새 프로젝트 대화 상자](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**그림 01**: 유효성 검사를 사용 하 여 폼 ([큰 이미지를 보려면 클릭](iteration-3-add-form-validation-cs/_static/image2.png))


이 반복에서 컨트롤러 작업에 직접 유효성 검사 논리를 추가합니다. 일반적으로 ASP.NET MVC 응용 프로그램에 유효성 검사를 추가 하려면 권장 되는 방법은 아닙니다. 별도의 응용 프로그램 s 유효성 검사 논리를 배치 하는 것이 좋습니다 [서비스 계층](http://martinfowler.com/eaaCatalog/serviceLayer.html)합니다. 다음 반복에서 응용 프로그램을 관리할 수 있도록 연락처 관리자 응용 프로그램을 리팩터링 했습니다.

이 반복에서 간단 하 게,에서는 모든 유효성 검사 코드를 직접 작성 합니다. 유효성 검사 코드를 직접 작성 하는 대신 유효성 검사 프레임 워크를 활용할 수 했습니다. 예를 들어, ASP.NET MVC 응용 프로그램에 대 한 유효성 검사 논리를 구현 하는 Microsoft Enterprise Library 유효성 검사 응용 프로그램 블록 (VAB)를 사용할 수 있습니다. 유효성 검사 응용 프로그램 블록에 대 한 자세한 내용은 다음을 참조 하세요.

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Create View에 유효성 검사 추가

만들기 뷰를 유효성 검사 논리를 추가 하 여 시작 s 수 있습니다. 다행 스럽게도 Visual Studio를 사용 하 여 만들기 뷰를 생성 하기 때문에 만들기 이미 뷰에 모든 필요한 사용자 인터페이스 논리 유효성 검사 메시지를 표시 합니다. 만들기 뷰 목록 1에 포함 됩니다.

**목록 1-\Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

HTML 폼 바로 위에 있는 Html.ValidationSummary() 도우미 메서드에 대 한 호출을 확인 합니다. 유효성 검사 오류 메시지 인이 메서드는 글머리 기호 목록에서 유효성 검사 메시지를 표시 합니다.

표시, 또한 각 폼 필드 옆에 나타나는 Html.ValidationMessage() 호출 합니다. ValidationMessage() 도우미에는 각 유효성 검사 오류 메시지가 표시 됩니다. 목록 1의 경우 별표는 유효성 검사 오류가 있을 때 표시 됩니다.

마지막으로, Html.TextBox() 도우미를 자동으로 렌더링 Cascading Style Sheet 클래스 도우미에서 표시 되는 속성을 사용 하 여 연결 유효성 검사 오류가 있을 때. Html.TextBox() 도우미 클래스가 렌더링 **입력 유효성 검사 오류**합니다.

새 ASP.NET MVC 응용 프로그램을 만들면 Site.css 명명 된 스타일 시트 콘텐츠 폴더에 자동으로 만들어집니다. 이 스타일 시트 유효성 검사 오류 메시지의 모양과 관련 된 CSS 클래스에 대 한 다음 정의 포함 합니다.

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

필드 유효성 검사 오류 클래스는 Html.ValidationMessage() 도우미에 의해 렌더링 된 출력 스타일 지정에 사용 됩니다. 입력 유효성 검사 오류 클래스 스타일 Html.TextBox() 도우미에 의해 렌더링 된 텍스트 (입력)에 사용 됩니다. 유효성 검사-요약-오류 클래스는 렌더링 Html.ValidationSummary() 도우미에 의해 순서가 지정 되지 않은 목록 스타일에 사용 됩니다.

> [!NOTE] 
> 
> 유효성 검사 오류 메시지의 모양을 사용자 지정 하려면이 섹션에 설명 된 스타일 시트 클래스를 수정할 수 있습니다.


## <a name="adding-validation-logic-to-the-create-action"></a>유효성 검사 논리를 추가 된 작업 만들기

현재, Create view 유효성 검사 오류 메시지를 모든 메시지를 생성 하는 논리를 작성 하지 않은 것 때문에 되지 표시 됩니다. 유효성 검사 오류 메시지를 표시 하려면 ModelState에 오류 메시지를 추가 해야 합니다.

> [!NOTE] 
> 
> UpdateModel() 메서드 오류 메시지를 추가 ModelState 자동으로 폼 필드의 값 속성에 할당 오류가 발생 하는 경우. 예를 들어, 날짜/시간 값을 받아들이는 BirthDate 속성에 "apple" 문자열을 할당 하려고 하면 다음 UpdateModel() 메서드는 오류를 추가 ModelState 합니다.


목록 2에서 수정 된 create () 메서드를 데이터베이스에 새 연락처를 삽입 하기 전에 연락처 클래스의 속성의 유효성을 검사 하는 새 섹션을 포함 합니다.

**2-Controllers\ContactController.cs (유효성 검사를 사용 하 여 만들기)를 나열합니다.**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

유효성 검사 섹션은 4 개의 고유한 유효성 검사 규칙을 적용합니다.

- FirstName 속성에는 길이가 0 보다 크고 있어야 합니다. (및의 공백 전적으로 구성 될 수 없습니다)
- LastName 속성에는 길이가 0 보다 크고 있어야 합니다. (및의 공백 전적으로 구성 될 수 없습니다)
- Phone 속성 값이 있으면 (길이가 0 보다 큰) Phone 속성에는 정규식과 일치 해야 합니다.
- 전자 메일 속성 값이 있으면 (길이가 0 보다 큰) 전자 메일 속성에는 정규식과 일치 해야 합니다.

유효성 검사 규칙 위반의 경우 오류 메시지가 AddModelError() 메서드를 사용 하 여 ModelState에 추가 됩니다. ModelState에 메시지를 추가 하는 속성의 이름 및 유효성 검사 오류 메시지의 텍스트를 제공 합니다. 이 오류 메시지는 Html.ValidationSummary() 및 Html.ValidationMessage() 도우미 메서드에서 보기에 표시 됩니다.

유효성 검사 규칙은 실행 후 ModelState의 IsValid 속성을 확인 합니다. ModelState에 유효성 검사 오류 메시지를 추가한 경우 IsValid 속성은 false를 반환 합니다. 유효성 검사에 실패할 경우 오류 메시지와 함께 만들기 양식은 다시 표시 됩니다.

> [!NOTE] 
> 
> 정규식 리포지토리에서 전화 번호 및 전자 메일 주소 유효성을 검사 하는 것에 대 한 정규식을 받았습니다. [*http://regexlib.com*](http://regexlib.com)


## <a name="adding-validation-logic-to-the-edit-action"></a>편집 작업으로 유효성 검사 논리를 추가합니다.

되 작업 연락처를 업데이트합니다. 되 작업 create () 작업으로 동일한 유효성 검사가 정확 하 게 수행 해야 합니다. 동일한 유효성 검사 코드를 복제 하는 대신 동일한 유효성 검사 메서드를 호출 하는 create () 및 되 작업 있도록 연락처 컨트롤러를 리팩터링 해야 했습니다.

수정 된 연락처 컨트롤러 클래스는 목록 3에 포함 됩니다. 이 클래스는 create () 및 되 작업 내에서 호출 되는 새 ValidateContact() 메서드가 있습니다.

**3-Controllers\ContactController.cs 나열**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>요약

이 반복에서 연락처 관리자 응용 프로그램 기본 양식 유효성 검사를 추가 했습니다. 유효성 검사 논리에는 사용자가 새 연락처를 제출 하거나 FirstName 및 LastName 속성 값을 제공 하지 않고 기존 연락처를 편집 하지 못하도록 합니다. 또한 사용자가 올바른 전화 번호 및 전자 메일 주소를 제공 해야 합니다.

이 반복에서 추가한 유효성 검사 논리를 연락처 관리자 응용 프로그램 가능한 가장 쉬운 방법으로 합니다. 그러나이 유효성 검사 논리는 컨트롤러 논리를 혼합 문제가 생기게 됩니다 우리 회사에 장기적으로. 응용 프로그램 유지 관리 하 고 시간이 지남에 따라 수정 하기가 더 어렵습니다 됩니다.

다음 반복에서에서는 리팩터링이 유효성 검사 논리 및 데이터베이스 액세스 논리는 컨트롤러입니다. 이점은 더 느슨하게 결합 하 고 유지 관리, 응용 프로그램을 만들 수 있도록 몇 가지 소프트웨어 디자인 원칙을 알아보겠습니다.

> [!div class="step-by-step"]
> [이전](iteration-2-make-the-application-look-nice-cs.md)
> [다음](iteration-4-make-the-application-loosely-coupled-cs.md)
