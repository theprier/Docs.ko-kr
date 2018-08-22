---
uid: web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
title: '[어떻게 할까요?] ASP.NET 사용 하 여 전자 메일을 보낼 때 오류 처리를 구현 합니다. | Microsoft Docs'
author: rick-anderson
description: Chris Pels ASP.NET 사용 하 여 전자 메일을 전송 하는 경우 오류 처리를 구현 하는 방법을 보여 줍니다. 그 전자 메일을 보내는 ASP.NET 웹 페이지를 만듭니다, 그리고 lt. 구성 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/06/2008
ms.assetid: c02ffd50-aa19-4cdc-b1bf-760989979a61
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
msc.type: video
ms.openlocfilehash: 6708a0a22e621d08301fb4228ec6c6e5f599d57a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828634"
---
<a name="how-do-i-implement-error-handling-when-sending-email-with-aspnet"></a><span data-ttu-id="097f6-104">[어떻게 할까요?] ASP.NET 사용 하 여 전자 메일을 보낼 때 오류 처리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="097f6-104">[How Do I:] Implement Error Handling when Sending Email with ASP.NET</span></span>
====================
<span data-ttu-id="097f6-105">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="097f6-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="097f6-106">Chris Pels ASP.NET 사용 하 여 전자 메일을 전송 하는 경우 오류 처리를 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="097f6-106">Chris Pels shows how to implement error handling when sending an email with ASP.NET.</span></span> <span data-ttu-id="097f6-107">그는 전자 메일을 보내는 ASP.NET 웹 페이지를 생성, 구성 하는 방법을 보여 줍니다 &lt;mailSettings&gt; web.config 파일에서 System.Net.Mail 클래스 및 만들고 전자 메일 메시지를 전송 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="097f6-107">He creates an ASP.NET web page to send email, shows how to configure &lt;mailSettings&gt; in the web.config file, describes the System.Net.Mail class and how it's used to create and send email messages.</span></span> <span data-ttu-id="097f6-108">그 다음 SmtpStatusCode 열거형을 사용 하 여 전자 메일을 보낼 때 가능한 결과의 목록을 제공 하는 검토 및 전자 메일을 보낼 때 발생할 수 있는 오류에 대 한 정보를 제공 하는 System.Net.Mail 예외 클래스를 사용 하 여 오류 처리를 추가 합니다 SmtpClient 합니다.</span><span class="sxs-lookup"><span data-stu-id="097f6-108">He then adds error handling using System.Net.Mail exception classes, which provide information about errors that can occur when sending email, and reviews the SmtpStatusCode enumeration, which provides a list of possible outcomes when sending an email with the SmtpClient.</span></span> <span data-ttu-id="097f6-109">마지막으로, 예외가 발생 하 고 Visual Studio 디버거에서 정보를 처리 하는 오류를 검토 하는 테스트 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="097f6-109">Finally, he sends a test email that raises an exception and reviews the error handling information in the Visual Studio debugger.</span></span>

[<span data-ttu-id="097f6-110">&#9654;비디오 (24 분)</span><span class="sxs-lookup"><span data-stu-id="097f6-110">&#9654; Watch video (24 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-error-handling-when-sending-email-with-aspnet)
