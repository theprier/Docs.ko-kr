---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[어떻게 할까요?] ASP.NET에서 비동기적으로 전자 메일 보내기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서는 Chris Pels ASP.NET에서 System.Net.Mail 클래스를 사용 하 여 비동기 전자 메일 메시지를 보내는 방법을 보여 줍니다. 먼저 웹 si를 구성 하는 방법을 참조 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/24/2008
ms.topic: article
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: 69810f4c25b6b449168ca31af5df584c77d92e07
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395930"
---
<a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="2efa8-104">[어떻게 할까요?] ASP.NET에서 비동기적으로 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="2efa8-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>
====================
<span data-ttu-id="2efa8-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="2efa8-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="2efa8-106">이 비디오에서는 Chris Pels ASP.NET에서 System.Net.Mail 클래스를 사용 하 여 비동기 전자 메일 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="2efa8-107">사용 하 여 전자 메일 보내는 웹 사이트를 구성 하는 방법은 먼저 합니다 &lt;mailSettings&gt; web.config 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="2efa8-108">다음으로 전자 메일 정보를 입력 하는 것에 대 한 간단한 사용자 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="2efa8-109">만드는 방법은 다음 페이지에 대 한 코드 숨김에 전자 메일 메시지를 만들려면 MailMessage 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="2efa8-110">해당 프로세스의 일부로 전자 메일의 보내는 다음 비동기 콜백에 대 한 이벤트 처리기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="2efa8-111">이벤트 처리기에는 프로세스를 보내는 전자 메일에 대 한 정보를 제공 하는 AsynchCompletedEventArgs 클래스의 인스턴스를 사용 하는 방법을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2efa8-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="2efa8-112">마지막으로 테스트 전자 메일을 비동기적으로 전송 하 여 디버그 모드에서는 단계를 수행 하 고 프로세스에서 받은 실제 전자 메일을 보려면.</span><span class="sxs-lookup"><span data-stu-id="2efa8-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="2efa8-113">&#9654;비디오 (18 분)</span><span class="sxs-lookup"><span data-stu-id="2efa8-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
