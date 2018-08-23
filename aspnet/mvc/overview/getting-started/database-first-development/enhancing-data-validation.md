---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'ASP.NET MVC를 사용 하 여 먼저 EF Database: 데이터 유효성 검사 향상 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri...
ms.author: riande
ms.date: 12/29/2014
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: dbff33a1c4f47474adda82e796d9c292392142f2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837586"
---
<a name="ef-database-first-with-aspnet-mvc-enhancing-data-validation"></a>ASP.NET MVC를 사용 하 여 먼저 EF Database: 데이터 유효성 검사 향상
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.
> 
> 시리즈의이 부분 데이터 주석 유효성 검사 요구 사항을 지정 하 여 서식 지정을 표시 하는 데이터 모델에 추가 하는 방법에 중점을 둡니다. 의견 섹션에는 사용자의 의견에로 기반 향상 되었습니다.


## <a name="add-data-annotations"></a>데이터 주석 추가

이전 항목에서 살펴본 것 처럼 일부 데이터 유효성 검사 규칙의 사용자 입력에 자동으로 적용 됩니다. 예를 들어, 등급 속성에 대해 번호를 제공할 수 있습니다. 더 많은 데이터 유효성 검사 규칙을 지정 하려면 데이터 주석 모델 클래스에 추가할 수 있습니다. 이러한 주석은 지정된 된 속성에 대 한 웹 응용 프로그램 전체에서 적용 됩니다. 속성을 표시 되는 방법을 변경 하는 서식 특성을 적용할 수도 있습니다. 와 같은 텍스트 레이블에 사용 되는 값을 변경 합니다.

이 자습서에서는 데이터 FirstName, LastName 및 MiddleName 속성에 대해 제공 된 값의 길이 제한 하는 주석을 추가 합니다. 데이터베이스에서 이러한 값은 50 자로; 제한 그러나 웹 응용 프로그램에서 해당 문자 제한이 현재 적용 되지 않습니다. 이러한 값 중 하나에 대 한 50 개 이상의 문자를 제공 하는 사용자, 페이지 값을 데이터베이스에 저장 하려고 할 때 작동이 중단 됩니다. 또한 0에서 4 사이의 값으로 등급은 제한 합니다.

엽니다는 **Student.cs** 파일을 **모델** 폴더. 클래스에 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

Enrollment.cs에서 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

솔루션을 빌드합니다.

학생을 만들거나 편집 페이지로 이동 합니다. 50 개 이상의 문자를 입력 하려고 하면 오류 메시지가 표시 됩니다.

![오류 메시지를 표시 합니다.](enhancing-data-validation/_static/image1.png)

등록의 경우 편집을 위해 페이지를 찾아 4 위에 등급을 제공 하려고 합니다.

![엔터프라이즈급 범위 오류](enhancing-data-validation/_static/image2.png)

속성 및 클래스에 적용할 수는 데이터 유효성 검사 주석의 전체 목록을 참조 하세요 [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)합니다.

## <a name="add-metadata-classes"></a>메타 데이터 클래스를 추가 합니다.

데이터베이스를 변경 하지 않는 경우에 작동 모델 클래스에 직접 유효성 검사 특성을 추가 합니다. 그러나 모델 클래스를 다시 생성 하 여 데이터베이스를 변경 하 고 필요한 경우 모델 클래스에 적용 한 특성을 모두 손실 됩니다. 이 방법은 매우 비효율적이 고 중요 한 유효성 검사 규칙이 손실 발생 하기 쉬운 수 있습니다.

이 문제를 방지 하려면 특성을 포함 하는 메타 데이터 클래스를 추가할 수 있습니다. 메타 데이터 클래스 모델 클래스를 연결 하면 해당 특성은 모델에 적용 됩니다. 이 방법에서는 모델 클래스의 모든 메타 데이터 클래스에 적용 된 특성을 손실 하지 않고 다시 생성할 수 있습니다.

에 **모델** 폴더를 라는 클래스를 추가 **Metadata.cs**합니다.

![메타 데이터 클래스를 추가 합니다.](enhancing-data-validation/_static/image3.png)

Metadata.cs에서 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

이러한 메타 데이터 클래스에는 모든 모델 클래스를 이전에 적용 하는 유효성 검사 특성을 포함 합니다. 합니다 **표시** 특성 텍스트 레이블에 사용 되는 값을 변경 하는 데 사용 됩니다.

이제 메타 데이터 클래스를 사용 하 여 모델 클래스를 연결 해야 합니다.

에 **모델** 폴더를 라는 클래스를 추가 **PartialClasses.cs**합니다.

파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

각 클래스에으로 표시 되는 `partial` 클래스 및 각 자동으로 생성 된 클래스 이름 및 네임 스페이스를 일치 합니다. Partial 클래스에는 메타 데이터 특성을 적용 하 여 데이터 유효성 검사 특성을 자동으로 생성 된 클래스에 적용할 수 있는지 확인 합니다. 이러한 특성 메타 데이터 특성을 다시 생성 되지 않습니다는 partial 클래스에서 적용 되기 때문에 모델 클래스를 다시 생성 하면 손실 됩니다.

자동으로 생성 된 클래스를 다시 생성 하려면 ContosoModel.edmx 파일을 엽니다. 이번에 디자인 화면에서 마우스 오른쪽 단추로 클릭 **데이터베이스에서 모델 업데이트**합니다. 데이터베이스를 변경 하지 않은 경우에이 프로세스는 클래스를 다시 생성 됩니다. 에 **새로 고침** 탭을 선택 **테이블** 하 고 **마침**합니다.

![테이블 새로 고침](enhancing-data-validation/_static/image4.png)

변경 내용을 적용 하려면 ContosoModel.edmx 파일을 저장 합니다.

Student.cs 파일 또는 Enrollment.cs 파일을 열고 이전에 적용 된 데이터 유효성 검사 특성이 더 이상 파일을 확인 합니다. 그러나 응용 프로그램을 실행 하 고 데이터를 입력할 때 유효성 검사 규칙이 계속 적용 됩니다 확인 합니다.

> [!div class="step-by-step"]
> [이전](customizing-a-view.md)
> [다음](publish-to-azure.md)
