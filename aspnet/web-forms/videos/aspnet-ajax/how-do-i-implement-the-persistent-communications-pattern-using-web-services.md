---
uid: web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
title: '[어떻게 할까요?] 웹 서비스를 사용 하 여 지속적인 통신 패턴을 구현 하는 무엇입니까? | Microsoft 문서'
author: JoeStagner
description: 기존 웹 사이트에서 브라우저와 서버는 진행 중인 통신을 유지 하지 않습니다 하지만 통신을 수행 하는 사용자에 대 한 응답에만...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/22/2007
ms.topic: article
ms.assetid: 424c06cd-6d61-43cd-a1f2-d1a6b62e47b1
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
msc.type: video
ms.openlocfilehash: 8d7aac37b3b5b47f0533454f2d1d6f1f8677af99
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367476"
---
<a name="how-do-i-implement-the-persistent-communications-pattern-using-web-services"></a><span data-ttu-id="a6ecd-104">[어떻게 할까요?] 웹 서비스를 사용 하 여 지속적인 통신 패턴을 구현 하는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a6ecd-104">[How Do I:] Implement the Persistent Communications Pattern using Web Services?</span></span>
====================
<span data-ttu-id="a6ecd-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="a6ecd-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="a6ecd-106">기존 웹 사이트에서 브라우저와 서버 진행 중인 통신을 유지 관리 하지 않습니다 하지만 작업을 수행 하는 사용자에 대 한 응답에만 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ecd-106">In a traditional Web site the browser and the server do not maintain an ongoing communication, but communicate only in response to the user performing an action.</span></span> <span data-ttu-id="a6ecd-107">페이지의 응용 프로그램 컨테이너 되는 최신 웹 사이트에 브라우저 및 페이지 업데이트 작업을 수행 하는 사용자 없이 발생할 수 있도록 진행 중인 통신을 유지 하기 위해 서버에 대 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6ecd-107">In a modern Web site where the page becomes an application container, it can be advantageous for the browser and the server to maintain an ongoing communication so that page updates can occur without the user performing an action.</span></span> <span data-ttu-id="a6ecd-108">이 AJAX에 대 한 지속적인 통신 패턴 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ecd-108">This is known as the Persistent Communications Pattern for AJAX.</span></span> <span data-ttu-id="a6ecd-109">ASP.NET AJAX는 지속적인 통신 패턴을 구현 하는 웹 개발자를 위한 두 가지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ecd-109">ASP.NET AJAX provides two main ways for Web developers to implement the Persistent Communications Pattern.</span></span> <span data-ttu-id="a6ecd-110">이전 비디오에서 구현의 기반으로 ASP.NET AJAX UpdatePanel을 사용 하는 방법에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a6ecd-110">In an earlier video we saw how to use the ASP.NET AJAX UpdatePanel as the basis of the implementation.</span></span> <span data-ttu-id="a6ecd-111">이 비디오에서는 ASP.NET AJAX UpdatePanel의 필요성을 제거 하는 웹 서비스에 대 한 JavaScrpt 호출을 사용 하 여 동일한 패턴을 구현 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6ecd-111">In this video we learn how to implement the same pattern using a JavaScrpt call to a Web service, which removes the need for an ASP.NET AJAX UpdatePanel.</span></span>

[<span data-ttu-id="a6ecd-112">&#9654;비디오 (16 분)</span><span class="sxs-lookup"><span data-stu-id="a6ecd-112">&#9654; Watch video (16 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-the-persistent-communications-pattern-using-web-services)

> [!div class="step-by-step"]
> <span data-ttu-id="a6ecd-113">[이전](how-do-i-localize-an-aspnet-ajax-application.md)
> [다음](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span><span class="sxs-lookup"><span data-stu-id="a6ecd-113">[Previous](how-do-i-localize-an-aspnet-ajax-application.md)
[Next](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span></span>
