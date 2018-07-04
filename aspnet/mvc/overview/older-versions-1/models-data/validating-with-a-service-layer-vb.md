---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: 서비스 계층 (VB)를 사용 하 여 유효성 검사 | Microsoft Docs
author: StephenWalther
description: 사용자 유효성 검사 논리는 별도 서비스 계층 및 컨트롤러 작업에서 이동 하는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 설명 하는 방법을 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: a914a7351e0faf6babf144d80512994d513ed12f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393227"
---
<a name="validating-with-a-service-layer-vb"></a>서비스 계층 (VB)를 사용 하 여 유효성 검사
====================
[Stephen walther가](https://github.com/StephenWalther)

> 사용자 유효성 검사 논리는 별도 서비스 계층 및 컨트롤러 작업에서 이동 하는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 컨트롤러 계층에서 서비스 계층을 격리 하 여 중요 한 부분의 분리를 선명 하 게 유지할 수 있습니다에 대해 설명 합니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 하나의 메서드를 설명 하는 것입니다. 이 자습서에서는 사용자 유효성 검사 논리에는 컨트롤러를 별도 서비스 계층으로 이동 하는 방법을 알아봅니다.

## <a name="separating-concerns"></a>문제를 구분합니다.

ASP.NET MVC 응용 프로그램을 빌드하면 컨트롤러 작업 내에서 데이터베이스 논리를 배치 해서는 안 됩니다. 데이터베이스 및 컨트롤러 논리를 혼합 하면 응용 프로그램 시간이 지남에 따라 유지 관리 하기가 더 어렵습니다. 별도 저장소 계층의 모든 데이터베이스 논리를 배치 하는 하는 것이 좋습니다.

예를 들어 목록 1은 ProductRepository 라는 간단한 리포지토리가 포함 되어 있습니다. 제품 리포지토리에 모든 응용 프로그램에 대 한 데이터 액세스 코드를 포함합니다. 목록에는 제품 리포지토리를 구현 하는 IProductRepository 인터페이스도를 포함 됩니다.

**1-Models\ProductRepository.vb 나열**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

목록 2의 컨트롤러는 해당 index () 및 create () 작업에서 저장소 계층을 사용합니다. 이 컨트롤러 데이터베이스 논리를 포함 하지 않습니다 확인 합니다. 저장소 계층을 만드는 문제를 깔끔하게 분리를 유지할 수 있습니다. 컨트롤러는 응용 프로그램 흐름 제어 논리를 담당 하 고 리포지토리는 데이터 액세스 논리를 담당 합니다.

**Listing 2 - Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a>서비스 레이어 만들기

따라서 응용 프로그램 흐름 제어 논리는 컨트롤러에 속해 및 데이터 액세스 논리 저장소에 속해 있습니다. 이런 경우 여기서 배치 하나요 사용자 유효성 검사 논리? 첫 번째 방법은 사용자 유효성 검사 논리에 배치 하는 *서비스 계층*합니다.

서비스 계층은 리포지토리 계층과 컨트롤러 간의 통신을 중재 하는 ASP.NET MVC 응용 프로그램에서 레이어를 추가 합니다. 서비스 계층에는 비즈니스 논리가 포함 됩니다. 특히 유효성 검사 논리를 포함합니다.

예를 들어 목록 3의 제품 서비스 계층은 CreateProduct() 메서드가 있습니다. CreateProduct() 메서드는 새 제품을 제품 리포지토리에 제품을 전달 하기 전에 유효성을 검사 하려면 ValidateProduct() 메서드를 호출 합니다.

**3-Models\ProductService.vb 나열**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

제품 컨트롤러 목록 4 리포지토리 계층 대신 서비스 계층을 사용 하도록 업데이트 되었습니다. 컨트롤러 계층은 서비스 계층에 설명합니다. 서비스 계층은 리포지토리 계층에 설명합니다. 각 계층에는 별도 책임을 갖습니다.

**Listing 4 - Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

제품 서비스 제품 컨트롤러 생성자에서 만들어졌는지 확인 합니다. 제품 서비스를 만들면 모델 상태 사전에서 서비스에 전달 됩니다. 제품 서비스 모델 상태를 사용 하 여 컨트롤러에 다시 유효성 검사 오류 메시지를 전달 합니다.

## <a name="decoupling-the-service-layer"></a>서비스 계층을 분리

에서는 컨트롤러와 한 서비스 계층을 격리 하지 못했습니다. 컨트롤러 및 서비스 계층에는 모델 상태를 통해 통신합니다. 즉, 서비스 계층 ASP.NET MVC 프레임 워크의 특정 기능에서 종속성을 갖습니다.

가능한 한이 컨트롤러 계층에서 서비스 계층을 격리 하려고 합니다. 이론적으로 응용 프로그램 및 ASP.NET MVC 응용 프로그램 뿐만 아니라 모든 유형의 사용 하 여 서비스 계층을 사용할 수 있어야 합니다. 예를 들어, 앞으로 것이 좋습니다는 WPF 응용 프로그램에 대 한 프런트 엔드를 빌드할 수 있습니다. 이 서비스 계층에서 ASP.NET MVC에 대 한 종속성을 제거 하는 방법을 모델 상태를 찾을 해야 했습니다.

목록 5에서이 서비스 계층 모델 상태가 더 이상 사용할 수 있도록 업데이트 되었습니다. 대신 IValidationDictionary 인터페이스를 구현 하는 클래스를 사용 합니다.

**5-Models\ProductService.vb (분리)를 나열 합니다.**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

IValidationDictionary 인터페이스 목록 6에서 정의 됩니다. 이 간단한 인터페이스는 단일 메서드와 단일 속성에 있습니다.

**6-Models\IValidationDictionary.cs 나열**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

나열 7에서는 ModelStateWrapper 클래스 라는 클래스 IValidationDictionary 인터페이스를 구현 합니다. 모델 상태 사전을 생성자에 전달 하 여 ModelStateWrapper 클래스를 인스턴스화할 수 있습니다.

**Listing 7 - Models\ModelStateWrapper.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

마지막으로 목록 8에서 업데이트 된 컨트롤러는 해당 생성자에서 서비스 계층을 만들면는 ModelStateWrapper를 사용 합니다.

**Listing 8 - Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

IValidationDictionary 인터페이스 및 ModelStateWrapper 클래스 사용을 완전히 우리의 컨트롤러 계층에서이 서비스 계층을 분리할. 서비스 계층은 더 이상 모델 상태에 따라 달라 집니다. 서비스 계층에 IValidationDictionary 인터페이스를 구현 하는 클래스를 전달할 수 있습니다. 예를 들어 WPF 응용 프로그램을 간단한 컬렉션 클래스를 사용 하 여 IValidationDictionary 인터페이스를 구현할 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법은 설명 하는 것 이었습니다. 이 자습서에서는 모든 유효성 검사 논리에 컨트롤러 및 별도 서비스 계층으로 이동 하는 방법을 알아보았습니다. 또한 ModelStateWrapper 클래스를 만들어 컨트롤러 계층에서 서비스 계층을 격리 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](validating-with-the-idataerrorinfo-interface-vb.md)
> [다음](validation-with-the-data-annotation-validators-vb.md)
