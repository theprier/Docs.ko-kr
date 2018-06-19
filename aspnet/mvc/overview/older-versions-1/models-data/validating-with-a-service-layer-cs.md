---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: 서비스 계층 (C#)을 사용한 유효성 검사 | Microsoft Docs
author: StephenWalther
description: 사용자 유효성 검사 논리에서 컨트롤러 작업 및 별도 서비스 계층으로 이동 하는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 설명 방법을 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 06042ac197cc54da767a94a44c57eb09bb3db9fa
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869038"
---
<a name="validating-with-a-service-layer-c"></a>서비스 계층 (C#)을 사용한 유효성 검사
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

> 사용자 유효성 검사 논리에서 컨트롤러 작업 및 별도 서비스 계층으로 이동 하는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 컨트롤러 계층에서 사용자 서비스 계층을 격리 하 여 문제의 날카로운 분리 유지할 수 있습니다에 대해 설명 합니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 유효성 검사를 수행 하는 한 가지 방법은 설명 하는 것입니다. 이 자습서에서는 사용자 유효성 검사 논리에 컨트롤러와 별도 서비스 계층으로 이동 하는 방법에 설명 합니다.

## <a name="separating-concerns"></a>문제를 구분합니다.

ASP.NET MVC 응용 프로그램을 빌드할 때에 컨트롤러 작업 내 하지 데이터베이스 논리를 배치 해야 합니다. 데이터베이스와 컨트롤러 논리를 혼합 하면 응용 프로그램 시간이 지날수록 관리 하기가 더 어렵습니다. 별도 저장소 계층에 모든 데이터베이스 논리를 배치 하는 않는 것이 좋습니다.

예를 들어 목록 1의 ProductRepository 라는 간단한 리포지토리를 포함 합니다. 제품 저장소는 모든 응용 프로그램에 대 한 데이터 액세스 코드를 포함합니다. 목록에는 제품 저장소 구현 하는 IProductRepository 인터페이스 포함 되어 있습니다.

**Listing 1 -- Models\ProductRepository.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

목록 2에서 컨트롤러의 index () 및 create () 작업의 저장소 계층을 사용합니다. 이 컨트롤러에는 데이터베이스 논리 없는지 확인 합니다. 저장소 계층을 만드는 문제의 확실 하 게 구분을 유지 관리할 수 있습니다. 컨트롤러 응용 프로그램 흐름 제어 논리를 담당 하 고 저장소는 데이터 액세스 논리를 담당 합니다.

**Listing 2 - Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a>서비스 계층을 만들려면

따라서 응용 프로그램 흐름 제어 논리는 컨트롤러에 속하며 저장소에서 데이터 액세스 논리 속하는 있습니다. 이 경우 않습니다를 배치할 유효성 검사 논리? 첫 번째 방법은 유효성 검사 논리에 배치 하는 *서비스 계층*합니다.

서비스 계층은 컨트롤러와 저장소 계층 간의 통신을 중재 하는 ASP.NET MVC 응용 프로그램에 있는 추가 계층입니다. 서비스 계층에는 비즈니스 논리를 포함 합니다. 특히, 유효성 검사 논리를 포함합니다.

예를 들어 보기 3의 제품 서비스 계층에 CreateProduct() 메서드가 있습니다. CreateProduct() 메서드는 새 제품을 제품 저장소에 제품을 전달 하기 전에 유효성을 검사 하려면 ValidateProduct() 메서드를 호출 합니다.

**3-Models\ProductService.cs 나열**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

저장소 계층 대신 서비스 계층을 사용 하도록 목록 4에는 제품 컨트롤러 업데이트 되었습니다. 컨트롤러 계층의 서비스 계층으로 통신 합니다. 서비스 계층은 저장소 계층을 설명 합니다. 각 레이어에 별도 책임입니다.

**Listing 4 - Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

제품 서비스 제품 컨트롤러 생성자에서 만들어졌는지 확인 합니다. 제품 서비스를 만들면 모델 상태 사전에서 서비스에 전달 됩니다. 제품 서비스 모델 상태를 사용 하 여 컨트롤러에 다시 유효성 검사 오류 메시지를 전달 합니다.

## <a name="decoupling-the-service-layer"></a>서비스 계층을 분리

우리는 컨트롤러 및 서비스 계층 한 격리 하지 못했습니다. 컨트롤러 및 서비스 계층에는 모델 상태를 통해 통신합니다. 즉, 서비스 계층 ASP.NET MVC 프레임 워크의 특정 기능에 종속 됩니다.

가능한 한 우리의 컨트롤러 레이어에서 서비스 계층을 분리 하려고 합니다. 이론적으로 모든 종류의 응용 프로그램 및 ASP.NET MVC 응용 프로그램 뿐만 아니라 서비스 계층을 사용할 수 했습니다. 예를 들어 나중에 수 하려고는 WPF 응용 프로그램에 대 한 프런트 엔드를 작성 합니다. 이 서비스 계층에서 ASP.NET MVC에 대 한 종속성을 제거 하는 방법을 모델 상태를 찾을 해야 했습니다.

목록 5에서이 서비스 계층에 모델 상태를 더 이상 사용 하도록 업데이트 되었습니다. 대신, IValidationDictionary 인터페이스를 구현 하는 모든 클래스를 사용 합니다.

**5-Models\ProductService.cs (분리) 목록**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

IValidationDictionary 인터페이스 목록 6에서 정의 됩니다. 이 간단한 인터페이스에는 단일 메서드 및 단일 속성이 있습니다.

**6-Models\IValidationDictionary.cs 나열**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

ModelStateWrapper 클래스의 이름을 나열 하는 7: 클래스 IValidationDictionary 인터페이스를 구현 합니다. 모델 상태 사전 생성자에 전달 하 여 ModelStateWrapper 클래스를 인스턴스화할 수 있습니다.

**Listing 7 - Models\ModelStateWrapper.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

마지막으로, 목록 8의 업데이트 된 컨트롤러는 해당 생성자에서 서비스 계층을 만들 때는 ModelStateWrapper를 사용 합니다.

**Listing 8 - Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

IValidationDictionary를 사용 하 여 인터페이스와 ModelStateWrapper 클래스 수 있습니다 완전히 우리의 컨트롤러 계층에서이 서비스 계층을 격리. 서비스 계층은 더 이상 모델 상태에 의존 합니다. 서비스 계층 IValidationDictionary 인터페이스를 구현 하는 모든 클래스를 전달할 수 있습니다. 예를 들어 WPF 응용 프로그램 단순 컬렉션 클래스와 IValidationDictionary 인터페이스를 구현할 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목표 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법을 설명 하는 것 이었습니다. 이 자습서에서는 모든 유효성 검사 논리에 컨트롤러와 별도 서비스 계층으로 이동 하는 방법을 배웠습니다. 또한 ModelStateWrapper 클래스를 만들어 컨트롤러 계층에서 사용자 서비스 계층을 격리 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](validating-with-the-idataerrorinfo-interface-cs.md)
> [다음](validation-with-the-data-annotation-validators-cs.md)
