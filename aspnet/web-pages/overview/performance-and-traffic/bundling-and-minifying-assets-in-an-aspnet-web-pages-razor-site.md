---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: "묶음 및 축소 자산에는 ASP.NET 웹 페이지 (Razor) 사이트 | Microsoft Docs"
author: microsoft
description: "묶음 및 축소 가지 키를 눌러 사이트를 더 빠르게 만들 수 있습니다. JavaScript (.js) 파일 여러 개 또는 여러 연계 스타일 시트 (...를 결합 하면 번들"
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: df00b5c9e741e429011143d04121df97c1930602
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="b3c8a-104">묶음 및 축소 ASP.NET 웹 페이지 (Razor) 사이트의 자산</span><span class="sxs-lookup"><span data-stu-id="b3c8a-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="b3c8a-105">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b3c8a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b3c8a-106">묶음 및 축소 가지 키를 눌러 사이트를 더 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c8a-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="b3c8a-107">여러 JavaScript를 결합 하면 번들 (*.js*) 파일이 나 여러 연계 스타일 시트 (*.css*) 하도록 파일을 한 번에 하나씩이 아닌 단위를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c8a-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="b3c8a-108">축소 squeezes 공백 아웃 하 고 다른 종류의 압축을 가능한 작은으로 다운로드 한 파일을 확인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c8a-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="b3c8a-109">ASP.NET 웹 페이지 2 RC 릴리스 아직 필수 요소를 포함 하는 패키지를 Microsoft WebMatrix에서 사용할 수 없으므로 묶음 및 축소를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c8a-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="b3c8a-110">이 불편을 드려 죄송 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c8a-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="b3c8a-111">패키지는 ASP.NET 웹 페이지 2 및 WebMatrix 2의 최종 릴리스에서 사용 가능 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c8a-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
