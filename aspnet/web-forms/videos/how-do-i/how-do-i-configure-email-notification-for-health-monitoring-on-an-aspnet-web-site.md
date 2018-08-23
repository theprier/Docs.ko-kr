---
uid: web-forms/videos/how-do-i/how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site
title: '[어떻게 할까요?] ASP.NET 웹 사이트에서 상태 모니터링에 대 한 전자 메일 알림 구성 | Microsoft Docs'
author: rick-anderson
description: 이 비디오 Chris Pels ASP.NET 웹 사이트의 상태 모니터링에 대 한 전자 메일 알림을 구성 하는 방법을 보여 줍니다. 먼저 e 전송을 구성 하는 방법을 참조 하는 중...
ms.author: riande
ms.date: 09/11/2008
ms.assetid: 1fa884c0-582e-4dc6-abb6-a5ec70d43ffb
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site
msc.type: video
ms.openlocfilehash: 205e02cf5fce8cd80afa15b462e3784be7b40fbf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837043"
---
<a name="how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site"></a><span data-ttu-id="81cfd-104">[어떻게 할까요?] ASP.NET 웹 사이트에 대 한 모니터링 상태에 대 한 전자 메일 알림 구성</span><span class="sxs-lookup"><span data-stu-id="81cfd-104">[How Do I:] Configure Email Notification for Health Monitoring on an ASP.NET Web Site</span></span>
====================
<span data-ttu-id="81cfd-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="81cfd-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="81cfd-106">이 비디오 Chris Pels ASP.NET 웹 사이트의 상태 모니터링에 대 한 전자 메일 알림을 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81cfd-106">In this video Chris Pels shows how to configure email notification for health monitoring in an ASP.NET web site.</span></span> <span data-ttu-id="81cfd-107">먼저 사용 하 여 ASP.NET 웹 사이트에서 전자 메일 전송을 구성 하는 방법을 참조 합니다 &lt;emailSettings&gt; web.config 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="81cfd-107">First, see how to configure the sending of email in an ASP.NET web site through the use of the &lt;emailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="81cfd-108">다음으로, 상태 모니터링 이벤트 공급자에 대 한 전자 메일을 보내면 SimpleMailWebEventProvider를 추가 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81cfd-108">Next, learn how to add the SimpleMailWebEventProvider which sends emails for health monitoring events as a provider.</span></span> <span data-ttu-id="81cfd-109">그런 다음 표준 상태 모니터링 컴퓨터 수준 상태 모니터링 구성을 검사 하 여 전자 메일 알림을 사용 하 여 사용할 수 있는 이벤트를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="81cfd-109">Then see the standard health monitoring events that can be used with email notification by examining the machine level health monitoring configuration.</span></span> <span data-ttu-id="81cfd-110">사용 가능한 이벤트를 검토 한 후 전자 메일 공급자에 게 "모든 이벤트"를 매핑하는 규칙 구현을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="81cfd-110">After reviewing the available events see a rule implemented that maps the "All Events" to the email provider.</span></span> <span data-ttu-id="81cfd-111">웹 사이트를 시작할 때 여러 통의 전자 메일은 다음 전송 하며 Outlook에서 받으면를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cfd-111">Upon starting the web site several emails are then sent and examined when they are received in Outlook.</span></span> <span data-ttu-id="81cfd-112">마지막으로, 상태 모니터링 전자 메일 공급자에 매핑된 수 이벤트는 몇 가지 기본 원칙에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cfd-112">Finally, some basic principles of which events might be mapped to the health monitoring email provider are discussed.</span></span>

[<span data-ttu-id="81cfd-113">&#9654;비디오 (25 분)</span><span class="sxs-lookup"><span data-stu-id="81cfd-113">&#9654; Watch video (25 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site)
