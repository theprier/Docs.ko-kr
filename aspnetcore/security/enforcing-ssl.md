---
title: "ASP.NET Core 응용 프로그램에서 HTTPS를 적용합니다."
author: rick-anderson
description: "웹 응용 프로그램에서 ASP.NET Core HTTPS/TLS를 요청 하는 방법을 보여 줍니다."
manager: wpickett
ms.author: riande
ms.date: 2/9/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/enforcing-ssl
ms.openlocfilehash: dc320faf0048200412f131ea816f33f29ac023e1
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="enforcing-https-in-an-aspnet-core-app"></a>ASP.NET Core 응용 프로그램에서 HTTPS를 적용합니다.

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 문서에서는 표시 하는 방법:

- 모든 요청에 대 한 HTTPS가 필요 합니다.
- HTTPS에 대 한 모든 HTTP 요청을 리디렉션하십시오.

> [!WARNING]
> 수행 **하지** 사용 `RequireHttpsAttribute` 중요 한 정보를 수신 하는 웹 Api에 있습니다. `RequireHttpsAttribute` HTTP 상태 코드를 사용 하 여 HTTP에서 HTTPS로 브라우저를 리디렉션합니다. API 클라이언트 이해 하지 못하거나 리디렉션을 HTTP에서 HTTPS로 준수 수 있습니다. 이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다. 웹 Api 하거나 수행 해야합니다.
>
>* HTTP에서 수신 하지 않습니다.
>* 상태 코드 400 (잘못 된 요청)와 연결을 닫고 요청을 처리 하지 마십시오.

## <a name="require-https"></a>HTTPS가 필요

[RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute) HTTPS가 필요 하는 데 사용 됩니다. `[RequireHttpsAttribute]` 컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전역으로 적용 될 수 있습니다. 특성을 전역으로 적용 하려면 다음 코드를 추가 `ConfigureServices` 에 `Startup`:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

앞의 강조 표시 된 코드에서는 모든 요청 사용 `HTTPS`이므로, HTTP 요청은 무시 됩니다. 다음 강조 표시 된 코드를 HTTPS로 모든 HTTP 요청을 리디렉션합니다.

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

자세한 내용은 참조 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting)합니다.

HTTPS를 전역적으로 요구 (`options.Filters.Add(new RequireHttpsAttribute());`) 보안 모범 사례입니다. 적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성으로 전체적으로 HTTPS를 필요로 하는 컨트롤로 안전 하다 고 간주 되지 않습니다. 보장할 수는 `[RequireHttps]` 특성은 새 컨트롤러 및 Razor 페이지 추가 될 때 적용 됩니다.