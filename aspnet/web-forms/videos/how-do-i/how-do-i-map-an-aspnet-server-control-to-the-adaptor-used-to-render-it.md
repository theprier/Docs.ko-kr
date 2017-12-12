---
uid: web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
title: "[어떻게 할까요?] ASP.NET 서버 컨트롤을 렌더링 하는 데 사용 된 어댑터 매핑할 | Microsoft Docs"
author: rick-anderson
description: "이 비디오 Chris Pels에서는 컨트롤 어댑터를 사용 하 여 실제로 c를 변경 하지 않고 ASP.NET 서버 컨트롤에 대 한 다른 렌더링을 제공 하는 방법을 보여줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/19/2008
ms.topic: article
ms.assetid: d4b498ef-8e1c-4fa2-9c35-1f32f20bb9b7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
msc.type: video
ms.openlocfilehash: 675874da54fac688fa4df70ea1efaba477d30139
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it"></a><span data-ttu-id="58d88-103">[어떻게 할까요?] 지도 ASP.NET 서버 컨트롤을 렌더링 하는 데 사용 된 어댑터</span><span class="sxs-lookup"><span data-stu-id="58d88-103">[How Do I:] Map an ASP.NET Server Control to the Adaptor Used to Render It</span></span>
====================
<span data-ttu-id="58d88-104">으로 [Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="58d88-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="58d88-105">이 비디오 Chris Pels에서 실제로 컨트롤 자체를 변경 하지 않고 ASP.NET 서버 컨트롤에 대 한 다른 렌더링을 제공 하는 컨트롤 어댑터를 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58d88-105">In this video Chris Pels will show how to use a control adaptor to provide different renderings for an ASP.NET server control without actually changing the control itself.</span></span> <span data-ttu-id="58d88-106">이 비디오에서는 같습니다 ASP.NET 컨트롤을 가로로 DIV 요소를 사용 하 여 기존의 UL 요소 대신 각 목록 항목을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58d88-106">In this video, an ASP.NET BulletList control will be adapted to display each list item horizontally using DIV elements instead of the traditional UL elements.</span></span> <span data-ttu-id="58d88-107">첫째, WebControlAdaptor 상속 하 고 다음 목록에서는 렌더링 하는 코드를 구현 하는 클래스를 만드는 방법을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="58d88-107">First, see how to create a class that inherits WebControlAdaptor and then implements the code to render the new list format.</span></span> <span data-ttu-id="58d88-108">다음으로 브라우저 정의 파일에서 ASP.NET 서버 컨트롤에 새 컨트롤 어댑터를 매핑하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="58d88-108">Next, learn how to map the new control adaptor to the ASP.NET server control in the .browser definition file.</span></span> <span data-ttu-id="58d88-109">다음 웹 사이트의 페이지에서 새 컨트롤 어댑터를 사용 하는 방법을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="58d88-109">Then see how to use the new control adaptor on pages in a web site.</span></span> <span data-ttu-id="58d88-110">마지막으로, 컨트롤 어댑터 모든 브라우저 또는 특정 유형의 브라우저와 연결할 수 있는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="58d88-110">Finally, learn how a control adaptor can be associated with either all browsers or specific types of browsers.</span></span>

[<span data-ttu-id="58d88-111">&#9654; (23 분) 비디오를 시청 하세요</span><span class="sxs-lookup"><span data-stu-id="58d88-111">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it)
