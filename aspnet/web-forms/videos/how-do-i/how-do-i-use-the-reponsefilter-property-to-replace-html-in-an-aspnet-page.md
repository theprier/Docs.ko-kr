---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[어떻게 할까요?] ASP.NET 페이지의 HTML을 바꾸려면 Reponse.Filter 속성을 사용 하 여 | Microsoft Docs'
author: rick-anderson
description: 이 비디오 Chris Pels를 가로채 고 HTML 페이지에 전송 되 고 alter Reponse.Filter 속성을 사용 하는 방법을 보여 줍니다. 먼저 예제 페이지 w 생성 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/29/2009
ms.topic: article
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 3e7c1f2a947d185d7c2a01deb75e42c92ba914c3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26525532"
---
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="e2a16-104">[어떻게 할까요?] Reponse.Filter 속성을 사용 하 여 ASP.NET 페이지의 HTML을 바꾸려면</span><span class="sxs-lookup"><span data-stu-id="e2a16-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>
====================
<span data-ttu-id="e2a16-105">으로 [Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="e2a16-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="e2a16-106">이 비디오 Chris Pels를 가로채 고 HTML 페이지에 전송 되 고 alter Reponse.Filter 속성을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2a16-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="e2a16-107">먼저, 샘플 페이지를 단순 텍스트로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a16-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="e2a16-108">그런 다음 사용자의 브라우저에 보내지는 현재 스트림에 대 한 대체 스트림을로 제공 되는 사용자 지정 스트림 클래스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e2a16-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="e2a16-109">해당 사용자 지정 스트림 클래스는 페이지의 내용은 변경 하 고 다음 응답 스트림에 쓰여지는 스트림에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a16-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="e2a16-110">이 사용자 지정 스트림 클래스 함으로써 사용자의 브라우저에 보내지는 스키마가 변경 하는 기본 응답 스트림에 HTML 바꾸려면 Write 메서드가 사용자 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a16-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="e2a16-111">새 스트림 클래스 페이지 Response.Filter 속성에 할당 된 마지막으로,\_이벤트 페이지 콘텐츠를 변경 하기 위한 메커니즘을 제공 하 여 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a16-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="e2a16-112">&#9654; (13 분) 비디오를 시청 하세요</span><span class="sxs-lookup"><span data-stu-id="e2a16-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
