---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[어떻게 할까요?] AJAX의 방법 중에서 선택 페이지 업데이트? | Microsoft 문서'
author: JoeStagner
description: 이 비디오에서 Joe Stagner는 ASP.NET 응용 프로그램에서 AJAX 방식의 페이지 업데이트를 수행 하는 두 가지 주요 방법 비교 합니다. 첫 번째 메서드는 Upd를 사용 하는 중...
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 9f146c36ab2225e732a2a35d84bc4e6a616b22d5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830238"
---
<a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="f06cc-105">[어떻게 할까요?] AJAX의 방법 중에서 선택 페이지 업데이트?</span><span class="sxs-lookup"><span data-stu-id="f06cc-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>
====================
<span data-ttu-id="f06cc-106">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="f06cc-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="f06cc-107">이 비디오에서 Joe Stagner는 ASP.NET 응용 프로그램에서 AJAX 방식의 페이지 업데이트를 수행 하는 두 가지 주요 방법 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="f06cc-108">첫 번째 방법은 추가 코드 없이 클라이언트 쪽 이나 서버 쪽에서 작성 해야 하는 UpdatePanel을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="f06cc-109">UpdatePanel을 사용 하는 장점은 모든 항목이 자동으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="f06cc-110">페널티는 AJAX 요청 및 응답에 포함 될 데이터를 많이 필요한 클라이언트 및 서버를 전체 페이지 수명 주기를 실행할 필요는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="f06cc-111">두 번째 방법은 네트워크 콜백을 사용 하 여 추가 코드를 클라이언트 쪽 및 서버측 모두에서 작성 해야 하는 위치 하 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="f06cc-112">네트워크 콜백을 사용 하 여의 장점은 클라이언트에서 AJAX 요청 및 응답에 포함할 데이터를 거의 필요 하 고 서버에서 실행할 서비스 호출된 방법만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="f06cc-113">조기 결제 수수료 필요한 코드를 작성 하는 데 걸리는 시간과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="f06cc-114">Joe로 AJAX 방식의 페이지 업데이트의 두 가지 주요 방법 중에서 선택할 때 고려해 야 내용을 사용 하 여 비디오를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="f06cc-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="f06cc-115">(이 비디오에서 코드를 사용 합니다 [어떻게 하려면 ASP.NET AJAX와 함께](how-do-i-get-started-with-aspnet-ajax.md) 비디오 및 [ASP.NET AJAX와 함께 클라이언트 쪽 네트워크 콜백 만들기 구성 방법](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) 비디오입니다.)</span><span class="sxs-lookup"><span data-stu-id="f06cc-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="f06cc-116">&#9654;비디오 (11 분)</span><span class="sxs-lookup"><span data-stu-id="f06cc-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="f06cc-117">[이전](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [다음](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="f06cc-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>
