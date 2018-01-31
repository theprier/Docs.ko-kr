---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: "ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 데이터 유효성 검사 향상 | Microsoft Docs"
author: tfitzmac
description: "MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/29/2014
ms.topic: article
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 842496c2d3ec56fb81f2409dd7d05d800f83799b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="ef-database-first-with-aspnet-mvc-enhancing-data-validation"></a>ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 데이터 유효성 검사 향상
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.
> 
> 이 부분에서는 계열의 데이터 주석 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하려면 데이터 모델에 추가 하는 방법에 중점을 둡니다. 설명 섹션에는 사용자의 의견에로 기반 향상 되었습니다.


## <a name="add-data-annotations"></a>데이터 주석 추가

이전 항목에서 볼 수 있듯이 일부 데이터 유효성 검사 규칙 사용자 입력에 자동으로 적용 됩니다. 예를 들어 등급 속성에 대 한 번호를 제공할 수 있습니다. 더 많은 데이터 유효성 검사 규칙을 지정 하려면 데이터 주석 모델 클래스를 추가할 수 있습니다. 이러한 주석은 지정된 된 속성에 대 한 웹 응용 프로그램 전체에 적용 됩니다. 속성이 표시 되는 방식을 변경 하는 서식 특성을 적용할 수 있습니다. 와 같은 텍스트 레이블에 사용 되는 값을 변경 합니다.

이 자습서에서는 데이터 FirstName, LastName 및 MiddleName 속성에 대해 제공 된 값의 길이 제한 하는 주석을 추가 합니다. 데이터베이스에서 이러한 값은; 50 자로 제한 그러나 웹 응용 프로그램에서 해당 문자 제한 현재 적용 되지 않습니다. 이러한 값 중 하나에 대 한 50 개 이상의 문자를 제공 하는 사용자, 페이지를 데이터베이스에 값을 저장 하는 동안 작동이 중단 됩니다. 또한 0에서 4 사이의 값으로 등급을 제한 합니다.

열기는 **Student.cs** 파일에 **모델** 폴더입니다. 클래스에 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

Enrollment.cs, 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

솔루션을 빌드합니다.

편집 하거나 만들 학생에 대 한 페이지로 이동 합니다. 50 개 이상의 문자를 입력 하려고 하면 오류 메시지가 표시 됩니다.

![오류 메시지를 표시 합니다.](enhancing-data-validation/_static/image1.png)

등록을 편집 하기 위해 페이지를 찾아 4 위에 등급을 제공 하려고 합니다.

![등급 범위 오류](enhancing-data-validation/_static/image2.png)

속성 및 클래스를 적용할 수 있는 데이터 유효성 검사 주석 목록은 전체 참조 [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)합니다.

## <a name="add-metadata-classes"></a>메타 데이터 클래스를 추가 합니다.

변경할; 데이터베이스를 하지 않을 경우에 작동 모델 클래스에 직접 유효성 검사 특성을 추가 그러나 데이터베이스 변경 하 고 모델 클래스를 생성 해야 할 모델 클래스에 적용 한 특성을 모두 손실 됩니다. 이 방법은 매우 비효율적인 하 고 중요 한 유효성 검사 규칙이 손실 되는 경향이 수 있습니다.

이 문제를 방지 하려면 특성을 포함 하는 메타 데이터 클래스를 추가할 수 있습니다. 메타 데이터 클래스에 모델 클래스를 연결 하면 해당 특성은 모델에 적용 됩니다. 이 방법에서 모델 클래스의 모든 메타 데이터 클래스에 적용 된 특성을 손실 하지 않고 다시 생성할 수 있습니다.

에 **모델** 폴더 라는 클래스를 추가 **Metadata.cs**합니다.

![메타 데이터 클래스를 추가 합니다.](enhancing-data-validation/_static/image3.png)

Metadata.cs의 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

이러한 메타 데이터 클래스에는 이전에 모델 클래스에 적용 하는 유효성 검사 특성의 모두 포함 합니다. **디스플레이** 특성 텍스트 레이블에 사용 되는 값을 변경 하는 데 사용 됩니다.

이제 모델 클래스 메타 데이터 클래스와 연결 해야 합니다.

에 **모델** 폴더 라는 클래스를 추가 **PartialClasses.cs**합니다.

파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

각 클래스로 표시 된 통지는 `partial` 클래스 및 각 일치로 자동으로 생성 된 클래스 이름 및 네임 스페이스입니다. 메타 데이터 특성을 partial 클래스를 적용 하 여 데이터 유효성 검사 특성을 자동으로 생성 된 클래스에 적용 됩니다 있는지 확인 합니다. 이러한 특성의 메타 데이터 특성이 다시 생성 되지 않습니다 partial 클래스에 적용 되기 때문에 모델 클래스를 다시 생성 하면 손실 됩니다.

자동으로 생성 된 클래스를 다시 생성 하려면 ContosoModel.edmx 파일을 엽니다. 다시 한 번 단추로 클릭 하 고 디자인 화면 및 선택 **데이터베이스에서 모델 업데이트**합니다. 데이터베이스를 변경 하지 않은 경우에이 프로세스는 클래스 다시 생성 됩니다. 에 **새로 고침** 탭에서 **테이블** 및 **마침**합니다.

![테이블을 새로 고치려면](enhancing-data-validation/_static/image4.png)

변경 내용을 적용할 ContosoModel.edmx 파일을 저장 합니다.

Student.cs 파일이 나 Enrollment.cs 파일을 열고 더 이상 이전에 적용 된 데이터 유효성 검사 특성 파일의 수입니다. 그러나 응용 프로그램을 실행 하 고 데이터를 입력할 때 유효성 검사 규칙 여전히 적용 됩니다.

>[!div class="step-by-step"]
[이전](customizing-a-view.md)
[다음](publish-to-azure.md)
