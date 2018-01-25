---
title: "ASP.NET Core 응용 프로그램에서 SSL을 강제 적용"
author: rick-anderson
description: "웹 응용 프로그램에서 ASP.NET Core SSL을 요구 하는 방법을 보여 줍니다."
ms.author: riande
manager: wpickett
ms.date: 07/19/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/enforcing-ssl
ms.openlocfilehash: f248e9c0463cf4a46a447a9c896b3276a50f5f08
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="enforcing-ssl-in-an-aspnet-core-app"></a><span data-ttu-id="8f13f-103">ASP.NET Core 응용 프로그램에서 SSL을 강제 적용</span><span class="sxs-lookup"><span data-stu-id="8f13f-103">Enforcing SSL in an ASP.NET Core app</span></span>

<span data-ttu-id="8f13f-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8f13f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="8f13f-105">이 문서에서는 표시 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="8f13f-105">This document shows how to:</span></span>

- <span data-ttu-id="8f13f-106">모든 요청 (HTTPS 요청에만 해당)에 대 한 SSL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-106">Require SSL for all requests (HTTPS requests only).</span></span>
- <span data-ttu-id="8f13f-107">HTTPS에 대 한 모든 HTTP 요청을 리디렉션하십시오.</span><span class="sxs-lookup"><span data-stu-id="8f13f-107">Redirect all HTTP requests to HTTPS.</span></span>

## <a name="require-ssl"></a><span data-ttu-id="8f13f-108">SSL 필요</span><span class="sxs-lookup"><span data-stu-id="8f13f-108">Require SSL</span></span>

<span data-ttu-id="8f13f-109">[RequireHttpsAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute) ssl을 사용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-109">The [RequireHttpsAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require SSL.</span></span> <span data-ttu-id="8f13f-110">컨트롤러 또는이 특성을 사용 하 여 메서드를 데코레이팅 할 수 있습니다 하거나 아래와 같이 전체적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-110">You can decorate controllers or methods with this attribute or you can apply it globally as shown below:</span></span>

<span data-ttu-id="8f13f-111">다음 코드를 추가 `ConfigureServices` 에 `Startup`:</span><span class="sxs-lookup"><span data-stu-id="8f13f-111">Add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-)]

<span data-ttu-id="8f13f-112">위의 강조 표시 된 코드에서는 모든 요청 사용 `HTTPS`, 따라서 HTTP 요청은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-112">The highlighted code above requires all requests use `HTTPS`, therefore HTTP requests are ignored.</span></span> <span data-ttu-id="8f13f-113">다음 강조 표시 된 코드를 HTTPS로 모든 HTTP 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-113">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-)]

<span data-ttu-id="8f13f-114">참조 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-114">See [URL Rewriting Middleware](xref:fundamentals/url-rewriting) for more information.</span></span>

<span data-ttu-id="8f13f-115">HTTPS를 전역적으로 요구 (`options.Filters.Add(new RequireHttpsAttribute());`) 보안 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-115">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="8f13f-116">적용 된 `[RequireHttps]` 모든 컨트롤러에는 특성으로 전체적으로 HTTPS를 필요로 하는 컨트롤로 안전 하다 고 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-116">Applying the `[RequireHttps]` attribute to all controller isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="8f13f-117">보장할 수 없습니다 적용할 저장 되므로 응용 프로그램에 추가 하는 새로운 컨트롤러는 `[RequireHttps]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f13f-117">You can't guarantee new controllers added to your app will remember to apply the `[RequireHttps]` attribute.</span></span>
