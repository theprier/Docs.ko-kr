---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[어떻게 할까요?]  HTTP 헤더에 대 한 정보를 기반으로 한 ASP.NET 페이지 캐시 | Microsoft Docs'
author: rick-anderson
description: 이 비디오 Chris Pels 페이지의 HTTP 헤더의 정보에 따라 ASP.NET 출력 캐시의 페이지를 유지 하는 방법을 보여 줍니다. 첫 번째, 잠재적인 HTTP hea 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/26/2009
ms.topic: article
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: ce5ea10396d0fe31d72425e2431102a0cb0c3bd0
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
ms.locfileid: "28882219"
---
<a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="40784-104">[어떻게 할까요?]  HTTP 헤더에 대 한 정보를 기반으로 한 ASP.NET 페이지 캐시</span><span class="sxs-lookup"><span data-stu-id="40784-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>
====================
<span data-ttu-id="40784-105">으로 [Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="40784-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="40784-106">이 비디오 Chris Pels 페이지의 HTTP 헤더의 정보에 따라 ASP.NET 출력 캐시의 페이지를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40784-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="40784-107">첫째, 잠재적인 HTTP 헤더 값을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="40784-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="40784-108">그런 다음 샘플 페이지 만들어지고 OutputCache 지시문 "허용-언어"에서 사용자의 브라우저의 언어에 따라 캐싱을 제어 하는 HTTP 헤더 값을 포함 하는 VaryByHeader 특성 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40784-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="40784-109">영어로 설정 된 IE에서를 선택한 다음 프랑스어를 사용 하도록 설정 되어 있는 FireFox에서 샘플 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40784-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="40784-110">마지막으로, 캐시 정의 web.config 파일에서 CacheProfile를 이동 하는 옵션이 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40784-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="40784-111">&#9654; (12 분) 비디오를 시청 하세요</span><span class="sxs-lookup"><span data-stu-id="40784-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
