---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[어떻게 할까요?] 사용자 지정 정보에 따라 ASP.NET 페이지의 캐싱 컨트롤 | Microsoft Docs'
author: rick-anderson
description: 이 비디오 Chris Pels 캐싱 사용자 지정 정보에 따라 ASP.NET 페이지에 대 한 조건을 제어 하는 방법을 보여 줍니다. 샘플 페이지 만들어집니다 및 O. 다음...
ms.author: aspnetcontent
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: d069b7798d3659e9f6786fb8d63862817fbdd68b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808696"
---
<a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="7779d-104">[어떻게 할까요?] 사용자 지정 정보에 따라 ASP.NET 페이지의 캐싱 컨트롤</span><span class="sxs-lookup"><span data-stu-id="7779d-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>
====================
<span data-ttu-id="7779d-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="7779d-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="7779d-106">이 비디오 Chris Pels 캐싱 사용자 지정 정보에 따라 ASP.NET 페이지에 대 한 조건을 제어 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7779d-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="7779d-107">사용자 지정 값을 포함 하는 VaryByCustom 특성을 사용 하 여 OutputCache 지시문을 사용 하는 다음와 샘플 페이지 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7779d-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="7779d-108">다음으로, 사용자 지정 특성의 처리를 제공 하는 global.asax 모듈에서 GetVaryCustomByString() 메서드 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7779d-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="7779d-109">메서드에 페이지의 캐시 된 버전을 고유 하 게 식별 하는 문자열로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7779d-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="7779d-110">마지막으로, 사용자 지정 값을 사용 하 여 캐싱을 사용할 수 있는 방법을 여러 가지 방법으로 웹 사이트에 대 한 자세한 내용은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7779d-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="7779d-111">&#9654;비디오 (12 분)</span><span class="sxs-lookup"><span data-stu-id="7779d-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
