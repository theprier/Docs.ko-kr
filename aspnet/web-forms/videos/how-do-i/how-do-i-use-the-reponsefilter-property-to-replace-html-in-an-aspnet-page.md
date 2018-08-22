---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[어떻게 할까요?] Reponse.Filter 속성을 사용 하 여 ASP.NET 페이지의 HTML 바꾸기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오 Chris Pels을 가로채는 HTML 페이지로 전송 되 고 alter Reponse.Filter 속성을 사용 하는 방법을 보여 줍니다. 먼저 샘플 페이지를 w를 만듭니다...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 0e8ae8b62bbb4ac1fc7e942cf3dd0438383cb510
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827782"
---
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="9b1b3-104">[어떻게 할까요?] Reponse.Filter 속성을 사용 하 여 ASP.NET 페이지의 HTML 바꾸기</span><span class="sxs-lookup"><span data-stu-id="9b1b3-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>
====================
<span data-ttu-id="9b1b3-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="9b1b3-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="9b1b3-106">이 비디오 Chris Pels을 가로채는 HTML 페이지로 전송 되 고 alter Reponse.Filter 속성을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b1b3-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="9b1b3-107">먼저 샘플 페이지는 몇 가지 간단한 텍스트를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1b3-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="9b1b3-108">그런 다음 사용자 지정 Stream 클래스는 사용자의 브라우저에 전송할 현재 스트림에 대 한 대체 스트림으로 역할을 하는 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1b3-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="9b1b3-109">사용자 지정 스트림 클래스는 페이지의 내용은 변경 하 고 다음 응답 스트림에 작성 된 스트림, 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1b3-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="9b1b3-110">이 사용자 지정 Stream 클래스의 Write 메서드가 있으므로 사용자의 브라우저에 전달 되는 내용 변경 기본 응답 스트림에 HTML 바꾸려면 사용자 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1b3-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="9b1b3-111">새 스트림 클래스 페이지에서 Response.Filter 속성에 할당 된 마지막으로,\_이벤트를 로드, 따라서 페이지 콘텐츠를 변경 하는 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1b3-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="9b1b3-112">&#9654;비디오 (13 분)</span><span class="sxs-lookup"><span data-stu-id="9b1b3-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
