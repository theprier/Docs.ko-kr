---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: ASP.NET 웹에서 자산 묶음 및 축소 페이지 (Razor) 사이트 | Microsoft Docs
author: microsoft
description: 묶음 및 축소 가지 키를 눌러 사이트를 더 빨리 내릴 수 있습니다. 여러 JavaScript (.js) 파일 또는 여러 연계 스타일 시트 (...를 결합 하면 번들
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: dd1b184846a7ac9c08df0212a69b154279791d1a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393804"
---
<a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="2118c-104">ASP.NET 웹 페이지 (Razor) 사이트에서 자산 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="2118c-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="2118c-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2118c-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2118c-106">묶음 및 축소 가지 키를 눌러 사이트를 더 빨리 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2118c-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="2118c-107">여러 JavaScript를 결합 하면 번들로 (*.js*) 파일 또는 여러 연계 스타일 시트 (*.css*) 파일을 한 번에 하나씩가 아닌 단위를 다운로드할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2118c-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="2118c-108">축소는 공백 아웃 하 고 다른 유형의 가능한 작은으로 다운로드 한 파일을 확인 하는 압축을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2118c-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="2118c-109">ASP.NET 웹 페이지 2의 RC 릴리스에 필요한 요소를 포함 하는 패키지는 Microsoft WebMatrix에서 제공 되지 않아 묶음 및 축소를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2118c-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="2118c-110">이 불편을 드려서 죄송 합니다.</span><span class="sxs-lookup"><span data-stu-id="2118c-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="2118c-111">패키지는 ASP.NET 웹 페이지 2 및 WebMatrix 2의 최종 릴리스 사용 가능 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2118c-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
