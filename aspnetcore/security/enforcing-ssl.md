---
title: "ASP.NET Core 응용 프로그램에서 SSL 강제 적용하기"
author: rick-anderson
description: "ASP.NET Core 웹 응용 프로그램에서 SSL을 강제 적용하는 방법을 보여줍니다."
keywords: ASP.NET Core, SSL, HTTPS, RequireHttpsAttribute, IIS Express
ms.author: riande
manager: wpickett
ms.date: 07/19/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/enforcing-ssl
ms.openlocfilehash: 6f2755a606000717ca8a57f045b1ef613c7f14f6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="enforcing-ssl-in-an-aspnet-core-app"></a>ASP.NET Core 응용 프로그램에서 SSL 강제 적용하기

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 문서에서는 다음과 같은 내용을 살펴봅니다:

- 모든 요청에 SSL을 필수로 강제하는 방법 (HTTPS 요청만 허용하는 방법)
- 모든 HTTP 요청을 HTTPS로 리디렉션 하는 방법

## <a name="require-ssl"></a>SSL 강제 적용하기

SSL을 필수로 지정하기 위해서는 [RequireHttpsAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute)가 사용됩니다. 이 특성은 컨트롤러나 메서드에 개별적으로 지정할 수도 있고, 다음과 같이 전역으로 구성할 수도 있습니다.

`Startup`의 `ConfigureServices`에 다음 코드를 추가합니다:

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-)]

위의 강조 표시된 코드는 모든 요청에 `HTTPS`를 사용하도록 강제하며, 그 결과 HTTP 요청은 무시됩니다. 반면, 다음에 강조 표시된 코드는 모든 HTTP 요청을 HTTPS로 리디렉션합니다:

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-)]

더 자세한 정보는 [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)를 참고하시기 바랍니다.

전역으로 HTTPS를 요구하는 것이 보안상 가장 안전한 모범 사례입니다 (`options.Filters.Add(new RequireHttpsAttribute());`). 모든 컨트롤러에 `[RequireHttps]` 특성을 적용하더라도 전역으로 HTTPS를 요구하는 것만큼 안전하지는 않은 것으로 간주됩니다. 응용 프로그램에 추가된 새로운 컨트롤러에 반드시 `[RequireHttps]` 특성이 적용될 것이라는 보장이 없기 때문입니다.
