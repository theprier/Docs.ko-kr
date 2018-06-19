---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: '반복 #3-추가 폼 유효성 검사 (C#) | Microsoft Docs'
author: microsoft
description: 세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 emai을 확인 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: b9353c32b2839fd760513982c5742bb8f521e94a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872366"
---
<a name="iteration-3--add-form-validation-c"></a>반복 #3-추가 폼 유효성 검사 (C#)
====================
by [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> 세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소, 전화 번호를 확인 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>ASP.NET MVC 연락처 관리 응용 프로그램 (C#) 빌드
  

이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다. 관리자에 게 문의 응용 프로그램을 사람 목록에 대 한 사용-이름, 전화 번호 및 전자 메일 주소-연락처 정보를 저장할 수 있습니다.

여러 반복을 통해에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-모양이 아닌 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-폼 유효성 검사를 추가 합니다. 세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소, 전화 번호를 확인 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다. 예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 6-테스트 기반 개발을 사용 합니다. 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복 메일 그룹을 추가합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.


## <a name="this-iteration"></a>이 반복

않아 응용 프로그램의이 두 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드에 값을 입력 하지 않고 연락처를 제출 합니다. 또한 전화 번호 및 전자 메일 주소 (그림 1 참조)을 확인 합니다.


[![새 프로젝트 대화 상자](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**그림 01**: 유효성 검사를 사용 하 여 폼 ([전체 크기 이미지를 보려면 클릭](iteration-3-add-form-validation-cs/_static/image2.png))


이 반복에서 컨트롤러 작업에 직접 유효성 검사 논리를 추가 했습니다. 일반적으로 ASP.NET MVC 응용 프로그램에 유효성 검사를 추가할 권장 방법은 아닙니다. 별도의 응용 프로그램 s 유효성 검사 논리를 배치 하는 것이 좋습니다 [서비스 계층](http://martinfowler.com/eaaCatalog/serviceLayer.html)합니다. 응용 프로그램을 더 쉽게 유지 관리할 않아 응용 프로그램을 리팩터링한 다음 반복에 있습니다.

이 반복에 간단 하 게,에서는 모든 유효성 검사 코드를 직접 작성 합니다. 유효성 검사 코드를 직접 작성 하는 대신 유효성 검사 프레임 워크를 활용할 수 있습니다. 예를 들어 ASP.NET MVC 응용 프로그램에 대 한 유효성 검사 논리를 구현 하는 Microsoft Enterprise 라이브러리 유효성 검사 응용 프로그램 블록 (VAB)를 사용할 수 있습니다. 유효성 검사 응용 프로그램 블록에 대 한 자세한 내용은 다음을 참조 하세요.

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>만들기 뷰에 유효성 검사 추가

만들기 뷰를 유효성 검사 논리를 추가 하 여 시작 s를 사용 합니다. 다행히 Visual Studio와 함께 만들기 뷰를 생성 했습니다 때문에 Create view 이미 포함 되어 모든 유효성 검사 메시지를 표시 하는 데 필요한 사용자 인터페이스 논리입니다. 만들기 뷰 목록 1에 포함 됩니다.

**목록 1-\Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

HTML 폼 바로 위에 있는 Html.ValidationSummary() 도우미 메서드에 대 한 호출을 확인 합니다. 유효성 검사 오류 메시지에 있는이 메서드는 글머리 기호 목록에서 유효성 검사 메시지를 표시 합니다.

공지, 또한 각 양식 필드 옆에 나타나는 Html.ValidationMessage()에 대 한 호출입니다. ValidationMessage() 도우미 각 유효성 검사 오류 메시지를 표시 합니다. 목록 1의 경우 별표 유효성 검사 오류가 있을 때 표시 됩니다.

마지막으로, Html.TextBox() 도우미 자동으로 렌더링 연계 스타일 시트 클래스 도우미에서 표시 되는 속성와 관련 된 유효성 검사 오류가 있을 때. 라는 클래스를 렌더링 하는 Html.TextBox() 도우미 **입력 유효성 검사 오류**합니다.

새 ASP.NET MVC 응용 프로그램을 만들 때 Site.css 명명 된 스타일 시트의 내용 폴더에서 자동으로 만들어집니다. 이 스타일 시트는 CSS 클래스 유효성 검사 오류 메시지의 모양에 대 한 다음 정의 포함 되어 있습니다.

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

필드 유효성 검사 오류 클래스 Html.ValidationMessage() 도우미에서 렌더링 된 출력 스타일에 사용 됩니다. Html.TextBox() 도우미에서 렌더링 되는 텍스트 (입력) 스타일을 지정 하는 입력 유효성 검사 오류 클래스 사용 됩니다. 유효성 검사 요약-오류 클래스 스타일을 렌더링 Html.ValidationSummary() 도우미에서 순서가 지정 되지 않은 목록 사용 됩니다.

> [!NOTE] 
> 
> 유효성 검사 오류 메시지의 모양을 사용자 지정 하려면이 섹션에 설명 된 스타일 시트 클래스를 수정할 수 있습니다.


## <a name="adding-validation-logic-to-the-create-action"></a>유효성 검사 논리를 추가 된 작업 만들기

지금 바로 사용, Create view 유효성 검사 오류 메시지를 모든 메시지를 생성 하는 논리 기록 되지 않은 것 이므로 되지 표시 됩니다. 유효성 검사 오류 메시지를 표시 하려면 ModelState에 오류 메시지를 추가 해야 합니다.

> [!NOTE] 
> 
> UpdateModel() 메서드 추가 오류 메시지 ModelState 자동으로 때 속성 양식 필드의 값을 할당 하는 동안 오류가 발생 합니다. 예를 들어 날짜/시간 값을 받아 들이는 BirthDate 속성에 "apple" 문자열을 할당 하려고 하면 다음 UpdateModel() 메서드 오류를 추가 ModelState 합니다.


목록 2에서 수정 된 create () 메서드는 데이터베이스에 새 연락처를 삽입 하기 전에 연락처 클래스의 속성의 유효성을 검사 하는 새 섹션을 포함 합니다.

**2-Controllers\ContactController.cs (유효성 검사와 함께 만들기)를 나열합니다.**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

유효성 검사 섹션에는 4 개의 고유한 유효성 검사 규칙이 적용 됩니다.

- FirstName 속성의 길이 0 보다 커야 있어야 합니다. (및 공백으로 이루어질 수 없습니다 것)
- LastName 속성이 0 보다 큰 길이 여야 합니다. (및 공백으로 이루어질 수 없습니다 것)
- Phone 속성 값이 있으면 (길이가 0 보다 큰) Phone 속성에 정규식과 일치 해야 합니다.
- 전자 메일 속성 값이 있으면 (길이가 0 보다 큰)의 전자 메일 속성에 정규식과 일치 해야 합니다.

유효성 검사 규칙 위반 되는 경우 오류 메시지가 AddModelError() 메서드를 사용 하 여 ModelState에 추가 됩니다. ModelState에 메시지를 추가 하는 경우 속성의 이름 및 유효성 검사 오류 메시지 텍스트 제공 합니다. 이 오류 메시지가 Html.ValidationSummary() 및 Html.ValidationMessage() 도우미 메서드에서 보기에 표시 됩니다.

유효성 검사 규칙을 실행 한 후의 ModelState IsValid 속성이 확인 됩니다. IsValid 속성 유효성 검사 오류 메시지 ModelState에 추가 되 면 false를 반환 합니다. 유효성 검사에 실패할 경우 오류 메시지와 함께 폼 만들기 다시 표시 됩니다.

> [!NOTE] 
> 
> 정규식 리포지토리에서 전화 번호 및 전자 메일 주소 유효성을 검사 하는 것에 대 한 정규식 수신 됨 [*http://regexlib.com*](http://regexlib.com)


## <a name="adding-validation-logic-to-the-edit-action"></a>편집 작업에 유효성 검사 논리를 추가합니다.

연락처를 업데이트 하는 Edit() 동작입니다. Edit() 동작 create () 작업으로 동일한 유효성 검사 정확 하 게 수행 해야 합니다. 동일한 유효성 검사 코드를 복제 하는 대신 동일한 유효성 검사 메서드를 호출 하는 create ()와 Edit() 동작을 연락처 컨트롤러를 리팩터링 해야 했습니다.

수정 된 연락처 컨트롤러 클래스 보기 3에 포함 됩니다. 이 클래스는 create ()와 Edit() 작업 내에서 호출 하는 새 ValidateContact() 메서드.

**3-Controllers\ContactController.cs 나열**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>요약

이 반복에서 기본적인 형태의 유효성 검사 않아 응용 프로그램을 추가 했습니다. 유효성 검사 논리에는 사용자가 새 연락처를 전송 하거나 FirstName 및 LastName 속성의 값을 제공 하지 않고 기존 연락처를 편집할 수 없습니다. 또한 사용자가 올바른 전화 번호 및 전자 메일 주소를 제공 해야 합니다.

이 반복에는 가장 쉬운 방법은 가능한에서 않아 응용 프로그램에 유효성 검사 논리를 추가 합니다. 그러나 트 컨트롤러 논리에 유효성 검사 논리를 혼합 문제가 생기게 됩니다 우리 장기적으로 합니다. 응용 프로그램 유지 관리 하 고 시간이 지남에 따라 수정 하기가 더 어려워집니다 됩니다.

다음 반복에 됩니다 리팩터링한 우리의 유효성 검사 논리 및 데이터베이스 액세스 논리는 컨트롤러입니다. 더 유지 하 고 느슨하게 결합 된 응용 프로그램을 만들 수 있도록 몇 가지 소프트웨어 디자인 원칙을 활용을 이동 합니다.

> [!div class="step-by-step"]
> [이전](iteration-2-make-the-application-look-nice-cs.md)
> [다음](iteration-4-make-the-application-loosely-coupled-cs.md)
