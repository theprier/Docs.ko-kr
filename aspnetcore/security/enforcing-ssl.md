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
ms.openlocfilehash: 636077ea21581716308384ebf8d47c1e417a256a
ms.sourcegitcommit: b83a5f731a9c02bdb1cc1e3f9a8bf273eb5b33e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="enforcing-https-in-an-aspnet-core-app"></a><span data-ttu-id="fd09b-103">ASP.NET Core 응용 프로그램에서 HTTPS를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-103">Enforcing HTTPS in an ASP.NET Core app</span></span>

<span data-ttu-id="fd09b-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fd09b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="fd09b-105">이 문서에서는 표시 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="fd09b-105">This document shows how to:</span></span>

- <span data-ttu-id="fd09b-106">모든 요청에 대 한 HTTPS가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-106">Require HTTPS for all requests.</span></span>
- <span data-ttu-id="fd09b-107">HTTPS에 대 한 모든 HTTP 요청을 리디렉션하십시오.</span><span class="sxs-lookup"><span data-stu-id="fd09b-107">Redirect all HTTP requests to HTTPS.</span></span>

> [!WARNING]
> <span data-ttu-id="fd09b-108">수행 **하지** 사용 `RequireHttpsAttribute` 중요 한 정보를 수신 하는 웹 Api에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-108">Do **not** use `RequireHttpsAttribute` on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="fd09b-109">`RequireHttpsAttribute`HTTP 상태 코드를 사용 하 여 HTTP에서 HTTPS로 브라우저를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-109">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="fd09b-110">API 클라이언트 이해 하지 못하거나 리디렉션을 HTTP에서 HTTPS로 준수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-110">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="fd09b-111">이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-111">Such clients may send information over HTTP.</span></span> <span data-ttu-id="fd09b-112">웹 Api 하거나 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-112">Web APIs should either:</span></span>
>
>* <span data-ttu-id="fd09b-113">HTTP에서 수신 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-113">Not listen on HTTP.</span></span>
>* <span data-ttu-id="fd09b-114">상태 코드 400 (잘못 된 요청)와 연결을 닫고 요청을 처리 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="fd09b-114">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

## <a name="require-https"></a><span data-ttu-id="fd09b-115">HTTPS가 필요</span><span class="sxs-lookup"><span data-stu-id="fd09b-115">Require HTTPS</span></span>

<span data-ttu-id="fd09b-116">[RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute) HTTPS가 필요 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-116">The [RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute) is used to require HTTPS.</span></span> <span data-ttu-id="fd09b-117">`[RequireHttpsAttribute]`컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전역으로 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-117">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="fd09b-118">특성을 전역으로 적용 하려면 다음 코드를 추가 `ConfigureServices` 에 `Startup`:</span><span class="sxs-lookup"><span data-stu-id="fd09b-118">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

<span data-ttu-id="fd09b-119">앞의 강조 표시 된 코드에서는 모든 요청 사용 `HTTPS`이므로, HTTP 요청은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-119">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="fd09b-120">다음 강조 표시 된 코드를 HTTPS로 모든 HTTP 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-120">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

<span data-ttu-id="fd09b-121">자세한 내용은 참조 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-121">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>

<span data-ttu-id="fd09b-122">HTTPS를 전역적으로 요구 (`options.Filters.Add(new RequireHttpsAttribute());`) 보안 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-122">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="fd09b-123">적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성으로 전체적으로 HTTPS를 필요로 하는 컨트롤로 안전 하다 고 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-123">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="fd09b-124">보장할 수는 `[RequireHttps]` 특성은 새 컨트롤러 및 Razor 페이지 추가 될 때 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd09b-124">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>