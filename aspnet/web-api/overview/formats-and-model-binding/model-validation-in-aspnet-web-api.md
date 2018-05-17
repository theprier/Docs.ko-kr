---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API의에서 유효성 검사 모델 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/20/2012
ms.topic: article
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 409a91eceb8baa48a7dded1b850d59a27cec2c60
ms.sourcegitcommit: 5ae0c125ee3bbd324edef3818d1d160f4dd84602
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
<a name="model-validation-in-aspnet-web-api"></a>ASP.NET Web API의에서 모델 유효성 검사
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

클라이언트 데이터를 보내면 web API, 데이터 처리를 수행 하기 전에 유효성 검사 하려는 경우가 많습니다. 이 문서에 주석을 모델, 데이터 유효성 검사에 대 한 주석을 사용 하 여 및 web API의에서 유효성 검사 오류를 처리 하는 방법을 보여 줍니다.

## <a name="data-annotations"></a>데이터 주석

ASP.NET Web API에서에서 특성을 사용할 수는 [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) 네임 스페이스를 모델에서 속성에 대 한 유효성 검사 규칙을 설정 합니다. 다음과 같은 모델을 유의 하십시오.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

ASP.NET MVC에서 모델 유효성 검사를 사용한 경우에 익숙한 확인 해야 합니다. **필요한** 특성에 따르면는 `Name` 속성이 null이 아니어야 합니다. **범위** 특성에 따르면 `Weight` 0에서 999 사이 여야 합니다.

클라이언트가 보내는 다음 JSON 표현으로 POST 요청을 가정 합니다.

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

클라이언트가 포함 되지 않은 것을 확인할 수 있습니다는 `Name` 속성으로 표시 된 필요 합니다. 웹 API은 JSON으로 변환 하는 경우는 `Product` 유효성을 검사할 인스턴스는 `Product` 유효성 검사 특성에 대 한 합니다. 사용자 컨트롤러 작업에서 모델이 유효한 지 여부를 확인할 수 있습니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

모델 유효성 검사는 클라이언트 데이터 안전 하다는 보장 하지 않습니다. 추가 유효성 검사는 응용 프로그램의 다른 계층에 필요할 수 있습니다. (예를 들어 데이터 계층 적용할 수 있습니다 foreign key 제약 조건.) 자습서 [Entity Framework를 사용 하 여 웹 API를 사용 하 여](../data/using-web-api-with-entity-framework/part-1.md) 이러한 문제 중 일부를 살펴보고 있습니다.

**"아래 게시"**: 클라이언트가 일부 속성을 벗어날 때 발생 하는 방식도 게시 합니다. 예를 들어 클라이언트가 보내는 다음 있다고 가정 합니다.

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

클라이언트에 대 한 값을 지정 하지 않은 여기서 `Price` 또는 `Weight`합니다. JSON 포맷터는 0으로 누락 된 속성의 기본값을 할당합니다.

![](model-validation-in-aspnet-web-api/_static/image1.png)

모델 상태가 유효 하므로 0은 이러한 속성에 대 한 유효한 값입니다. 이 문제가 있는지 여부를 각 시나리오에 따라 달라 집니다. 예를 들어 update 작업에서 하려는 "0"과 "설정 하지 않습니다." 구분 Null을 허용 하 고 설정 값을 설정 하는 클라이언트를 강제로 표시 하려면 속성을 만듭니다는 **필요한** 특성:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"게시 과도 하 게"**: 클라이언트 보낼 수도 *자세한* 예상 보다 데이터입니다. 예를 들어:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

JSON에 존재 하지 않는 속성 ("색")을 포함 하는 여기에서 `Product` 모델입니다. 이 경우 JSON 포맷터는 단순히이 값을 무시합니다. (XML 포맷터의 동일한 작업을 수행 합니다.) 모델에 읽기 전용으로 사용 하는 속성이 있는 경우 문제가 발생 하는 과도 하 게 게시 합니다. 예를 들어:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

사용자가 업데이트를 받지 않도록는 `IsAdmin` 속성 관리자 자신 수준으로 상승 하 고! 가장 안전한 전략 보내도록 허용 하는 클라이언트는 정확히 일치 하는 모델 클래스를 사용 하는 것입니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Brad Wilson의 블로그 게시물 "[입력 유효성 검사 vs. Validation in ASP.NET MVC 모델](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"좋은 설명은 아래 게시와 과도 하 게 게시 하는 중에 있습니다. ASP.NET MVC 2에 대 한 게시물 인 문제가 될 웹 API와 여전히 관련이 있습니다.


## <a name="handling-validation-errors"></a>유효성 검사 오류 처리

Web API가 자동으로 오류를 반환 하지 클라이언트에 유효성 검사가 실패할 때입니다. 컨트롤러 작업 모델 상태를 확인 하 고 적절 하 게 응답을 원하는 경우.

컨트롤러 동작이 호출 되기 전에 모델 상태를 확인 하는 작업 필터를 만들 수 있습니다. 다음 코드 예를 보여 줍니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

모델 유효성 검사에 실패 하는 경우이 필터는 유효성 검사 오류를 포함 하는 HTTP 응답을 반환 합니다. 이 경우에 컨트롤러 동작 호출 되지 않습니다.

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

모든 Web API 컨트롤러에이 필터를 적용 하려면 필터의 인스턴스를 추가 **HttpConfiguration.Filters** 구성 하는 동안 컬렉션:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

또 다른 옵션은 개별 컨트롤러 또는 컨트롤러 동작 특성으로 필터를 설정 하려면:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
