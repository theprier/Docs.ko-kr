---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 모델 바인딩 및 web forms를 사용 하는 프로젝트에 추가 비즈니스 논리 레이어 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: 4ba1830ce51f257e18880f752b249dbeb77f504e
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021653"
---
<a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>모델 바인딩 및 web forms를 사용 하는 프로젝트에 비즈니스 논리 레이어 추가
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다. 이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.
> 
> 이 자습서에서는 비즈니스 논리 레이어를 사용 하 여 모델 바인딩을 사용 하는 방법을 보여 줍니다. 데이터 메서드를 호출 하려면 현재 페이지 이외의 개체가 사용 되도록 지정 OnCallingDataMethods 멤버를 설정 합니다.
> 
> 이 자습서에서 만든 프로젝트를 기반 합니다 [이전](retrieving-data.md) 시리즈의 파트입니다.
> 
> 할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트 다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다. 이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.


## <a name="what-youll-build"></a>만들 내용

모델 바인딩을 사용 하면 웹 페이지에 대 한 코드 숨김 파일에서 또는 별도 비즈니스 논리 클래스에서 데이터 상호 작용 코드를 배치할 수 있습니다. 이전 자습서에는 데이터 상호 작용 코드에 대 한 코드 숨김 파일을 사용 하는 방법을 살펴보았습니다. 이 방법은 소규모 사이트에 있지만 코드 반복 및 어려움 대규모 사이트 유지 관리 하는 경우 발생할 수 있습니다. 또한 프로그래밍 방식으로 추상화 계층이 없으므로 코드 숨김 파일에에서 있는 코드를 테스트 하는 것이 어려울 수 있습니다.

데이터 상호 작용 코드를 중앙 집중화 함으로써 모든 데이터와 상호 작용에 대 한 논리를 포함 하는 비즈니스 논리 레이어를 만들 수 있습니다. 그런 다음 웹 페이지에서 비즈니스 논리 계층을 호출합니다. 이 자습서에는 모든 비즈니스 논리 계층으로 이전 자습서에서 작성 한 코드를 이동한 다음 페이지에서 해당 코드를 사용 하는 방법을 보여 줍니다.

이 자습서에서는 다음을 수행 해야합니다.

1. 코드 숨김 파일에서 비즈니스 논리 레이어 코드 이동
2. 비즈니스 논리 계층에서 메서드를 호출 하 여 데이터 바인딩된 컨트롤 변경

## <a name="create-business-logic-layer"></a>비즈니스 논리 레이어 만들기

이제 웹 페이지에서 호출 되는 클래스를 만듭니다. 이 클래스의 메서드는 이전 자습서에서 사용 된 메서드를 유사 하 고 값 공급자 특성을 포함 합니다.

먼저 이라는 새 폴더를 추가 **BLL**합니다.

![폴더 추가](adding-business-logic-layer/_static/image1.png)

BLL 폴더에서 라는 새 클래스를 만듭니다 **SchoolBL.cs**합니다. 데이터 작업을 마치 원래 코드 숨김 파일에 있는 모든 포함 됩니다. 메서드는 메서드를 코드 숨김 파일에서와 거의 동일 하지만 일부 변경 내용이 포함 됩니다.

참고에서 가장 중요 한 변경의 인스턴스 내에서 코드를 실행 하 고 더 이상 되는 것 **페이지** 클래스입니다. 페이지 클래스를 포함 합니다 **tryupdatemodel에 전달** 메서드 및 **ModelState** 속성입니다. 이 코드는 비즈니스 논리 계층으로 이동 하면 이러한 멤버를 호출 하려면 페이지 클래스의 인스턴스는 더 이상. 를이 문제를 해결 하기 위해 추가 해야 합니다는 **ModelMethodContext** tryupdatemodel에 전달 하거나 ModelState에 액세스 하는 모든 메서드에 매개 변수입니다. 호출 tryupdatemodel에 전달 하거나 ModelState 검색할이 ModelMethodContext 매개 변수를 사용 합니다. 이 새 매개 변수에 대 한 계정 웹 페이지에 아무 것도 변경할 필요가 없습니다.

SchoolBL.cs에서 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>비즈니스 논리 계층에서 데이터를 검색할 기존 페이지를 수정 합니다.

마지막으로 쿼리를 사용 하 여 비즈니스 논리 계층을 사용 하 여 코드 숨김 파일에에서 Students.aspx, AddStudent.aspx, 및 Courses.aspx 페이지를 변환 합니다.

AddStudent, 학생과 강좌에 대 한 코드 숨김 파일에서 삭제 하거나 다음과 같은 쿼리 메서드를 주석:

- studentsGrid\_GetData
- studentsGrid\_UpdateItem
- studentsGrid\_DeleteItem
- addStudentForm\_InsertItem
- coursesGrid\_GetData

이제 해야 코드가 없는 데이터 작업에 관련 된 코드 숨김 파일에 있습니다.

합니다 **OnCallingDataMethods** 이벤트 처리기를 사용 하면 데이터 메서드를 사용 하는 개체를 지정할 수 있습니다. Students.aspx에서 해당 이벤트 처리기에 대 한 값을 추가 하 고 데이터 메서드 이름에는 비즈니스 논리 클래스의 메서드 이름을 변경 합니다.

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

Students.aspx에 대 한 코드 숨김 파일에서 CallingDataMethods 이벤트에 대 한 이벤트 처리기를 정의 합니다. 이 이벤트 처리기에서 데이터 작업에 대 한 비즈니스 논리 클래스를 지정합니다.

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

AddStudent.aspx에서 유사한 변경 내용을 확인 합니다.

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

Courses.aspx에서 유사한 변경 내용을 확인 합니다.

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

응용 프로그램을 실행 하 고 페이지의 모든 이전에 사용 했던 대로 작동 하는지 확인 합니다. 또한 유효성 검사 논리가 제대로 작동합니다.

## <a name="conclusion"></a>결론

이 자습서에서는 데이터 액세스 계층 및 비즈니스 논리 레이어를 사용 하도록 응용 프로그램 다시 구성 합니다. 지정한 데이터 컨트롤 데이터 작업에 대 한 현재 페이지 없는 개체를 사용 하 합니다.

> [!div class="step-by-step"]
> [이전](using-query-string-values-to-retrieve-data.md)
