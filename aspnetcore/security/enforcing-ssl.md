---
title: ASP.NET Core에 HTTPS를 적용 합니다.
author: rick-anderson
description: 웹 응용 프로그램에서 ASP.NET Core HTTPS/TLS를 요청 하는 방법을 보여 줍니다.
manager: wpickett
ms.author: riande
ms.date: 2/9/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/enforcing-ssl
ms.openlocfilehash: 2ebb975e1ea17698cee13ca00d3f5df4a5135e38
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="enforce-https-in-an-aspnet-core"></a>ASP.NET Core에 HTTPS를 적용 합니다.

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 문서에서는 다음과 같은 내용을 살펴봅니다.

- 모든 요청에 대 한 HTTPS가 필요 합니다.
- 모든 HTTP 요청을 HTTPS로 리디렉션하는 방법.

> [!WARNING]
> 수행 **하지** 사용 `RequireHttpsAttribute` 중요 한 정보를 수신 하는 웹 Api에 있습니다. `RequireHttpsAttribute` HTTP 상태 코드를 사용 하 여 HTTP에서 HTTPS로 브라우저를 리디렉션합니다. API 클라이언트 이해 하지 못하거나 리디렉션을 HTTP에서 HTTPS로 준수 수 있습니다. 이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다. 웹 Api 하거나 수행 해야합니다.
>
>* HTTP에서 수신 하지 않습니다.
>* 상태 코드 400 (잘못 된 요청)와 연결을 닫고 요청을 처리 하지 마십시오.

## <a name="require-https"></a>HTTPS가 필요

[RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute) HTTPS가 필요 하는 데 사용 됩니다. `[RequireHttpsAttribute]` 컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전역으로 적용 될 수 있습니다. 특성을 전역으로 적용 하려면 다음 코드를 추가 `ConfigureServices` 에 `Startup`:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

위의 강조 표시된 코드는 모든 요청에 `HTTPS` 를 사용하도록 강제하며, 그 결과 HTTP 요청은 무시됩니다. 다음에 강조 표시된 코드는 모든 HTTP 요청을 HTTPS로 리디렉션합니다.

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

자세한 내용은 참조 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting)합니다.

전역으로 HTTPS를 요구하는 것이 보안상 가장 안전한 모범 사례입니다 (`options.Filters.Add(new RequireHttpsAttribute());`). 적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성으로 전체적으로 HTTPS를 필요로 하는 컨트롤로 안전 하다 고 간주 되지 않습니다. 보장할 수는 `[RequireHttps]` 특성은 새 컨트롤러 및 Razor 페이지 추가 될 때 적용 됩니다.
