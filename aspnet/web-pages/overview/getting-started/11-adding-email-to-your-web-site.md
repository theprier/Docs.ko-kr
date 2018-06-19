---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: (Razor) 사이트 페이지는 ASP.NET 웹에서 전자 메일 보내기 | Microsoft Docs
author: tfitzmac
description: 이 장에서 웹 사이트에서 자동화 된 전자 메일 메시지를 전송 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 9be242d238c627a9557fe7ff7e596974e5b7d1c8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30896518"
---
<a name="sending-email-from-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c2fa1-103">ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="c2fa1-103">Sending Email from an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="c2fa1-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c2fa1-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c2fa1-105">이 문서에서는 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 웹 사이트에서 전자 메일 메시지를 전송 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-105">This article explains how to send an email message from a website when you use ASP.NET Web Pages (Razor).</span></span>
> 
> <span data-ttu-id="c2fa1-106">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="c2fa1-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c2fa1-107">웹 사이트에서 전자 메일 메시지를 보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-107">How to send an email message from your website.</span></span>
> - <span data-ttu-id="c2fa1-108">전자 메일 메시지에 파일을 첨부 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-108">How to attach a file to an email message.</span></span>
> 
> <span data-ttu-id="c2fa1-109">다음은 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="c2fa1-110">`WebMail` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-110">The `WebMail` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c2fa1-111">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c2fa1-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c2fa1-112">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="c2fa1-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="c2fa1-113">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a><span data-ttu-id="c2fa1-114">웹 사이트에서 전자 메일 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="c2fa1-114">Sending Email Messages from Your Website</span></span>

<span data-ttu-id="c2fa1-115">모든 종류의 웹 사이트에서 전자 메일 보내기 해야 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-115">There are all sorts of reasons why you might need to send email from your website.</span></span> <span data-ttu-id="c2fa1-116">사용자에 게 확인 메시지를 보낼 수 있습니다 (예: 새 사용자를 등록 합니다.) 자신에 게 알림을 보낼 수 있습니다 또는 `WebMail` 도우미를 사용 하면 쉽게 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-116">You might send confirmation messages to users, or you might send notifications to yourself (for example, that a new user has registered.) The `WebMail` helper makes it easy for you to send email.</span></span>

<span data-ttu-id="c2fa1-117">사용 하 여 `WebMail` 도우미, SMTP 서버에 액세스할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-117">To use the `WebMail` helper, you have to have access to an SMTP server.</span></span> <span data-ttu-id="c2fa1-118">(SMTP는 *Simple Mail Transfer Protocol*.) SMTP 서버에만 받는 사람의 서버로 메시지를 전달 하는 전자 메일 서버는 &#8212; 전자 메일의 아웃 바운드 측은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-118">(SMTP stands for *Simple Mail Transfer Protocol*.) An SMTP server is an email server that only forwards messages to the recipient's server &#8212; it's the outbound side of email.</span></span> <span data-ttu-id="c2fa1-119">호스팅 공급자를 사용 하 여 웹 사이트에 대 한 아마도 설정 하면 전자 메일을 가진 및 SMTP server 이름이 무엇 인지 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-119">If you use a hosting provider for your website, they probably set you up with email and they can tell you what your SMTP server name is.</span></span> <span data-ttu-id="c2fa1-120">회사 네트워크 내부 작업 관리자 또는 IT 부서 일반적으로 정보를 제공할 수 있습니다는 사용할 수 있는 SMTP 서버에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-120">If you're working inside a corporate network, an administrator or your IT department can usually give you the information about an SMTP server that you can use.</span></span> <span data-ttu-id="c2fa1-121">집에서 작업 하는 경우 해당 SMTP 서버의 이름을 알 수 있는 일반 전자 메일 공급자를 사용 하 여 테스트할 수도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-121">If you're working at home, you might even be able to test using your ordinary email provider, who can tell you the name of their SMTP server.</span></span> <span data-ttu-id="c2fa1-122">일반적으로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-122">You typically need:</span></span>

- <span data-ttu-id="c2fa1-123">SMTP 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-123">The name of the SMTP server.</span></span>
- <span data-ttu-id="c2fa1-124">포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-124">The port number.</span></span> <span data-ttu-id="c2fa1-125">이 거의 항상 25입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-125">This is almost always 25.</span></span> <span data-ttu-id="c2fa1-126">그러나 ISP 포트 587을 사용 하도록 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-126">However, your ISP may require you to use port 587.</span></span> <span data-ttu-id="c2fa1-127">전자 메일에 대 한 secure sockets layer (SSL)를 사용 하는 경우에 다른 포트를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-127">If you are using secure sockets layer (SSL) for email, you might need a different port.</span></span> <span data-ttu-id="c2fa1-128">전자 메일 공급자에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-128">Check with your email provider.</span></span>
- <span data-ttu-id="c2fa1-129">자격 증명 (사용자 이름, 암호)입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-129">Credentials (user name, password).</span></span>

<span data-ttu-id="c2fa1-130">이 절차에서는 두 개의 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-130">In this procedure, you create two pages.</span></span> <span data-ttu-id="c2fa1-131">첫 번째 페이지에는 기술 지원 형식으로 작성 된 하는 경우 설명을 입력 하는 사용자가 수 있는 폼을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-131">The first page has a form that lets users enter a description, as if they were filling in a technical-support form.</span></span> <span data-ttu-id="c2fa1-132">첫 번째 페이지는 두 번째 페이지에 해당 정보를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-132">The first page submits its information to a second page.</span></span> <span data-ttu-id="c2fa1-133">두 번째 페이지에서 코드는 사용자의 정보를 추출 하 고 전자 메일 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-133">In the second page, code extracts the user's information and sends an email message.</span></span> <span data-ttu-id="c2fa1-134">또한 문제 보고서를 받았는지 확인 하는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-134">It also displays a message confirming that the problem report has been received.</span></span>

![[image]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> <span data-ttu-id="c2fa1-136">이 예제를 단순하게 유지 하기 위해 코드를 초기화는 `WebMail` 도우미 right를 사용 하 여 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-136">To keep this example simple, the code initializes the `WebMail` helper right in the page where you use it.</span></span> <span data-ttu-id="c2fa1-137">그러나 실제 웹 사이트에 대 한 되는 글로벌 파일에 다음과 같은 초기화 코드를 저장 하는 것이 좋습니다 초기화는 `WebMail` 웹 사이트의 모든 파일에 대 한 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-137">However, for real websites, it's a better idea to put initialization code like this in a global file, so that you initialize the `WebMail` helper for all files in your website.</span></span> <span data-ttu-id="c2fa1-138">자세한 내용은 참조 [사이트 전체의 동작을 사용자 지정 ASP.NET 웹 페이지에 대 한](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-138">For more information, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).</span></span>


1. <span data-ttu-id="c2fa1-139">새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-139">Create a new website.</span></span>
2. <span data-ttu-id="c2fa1-140">명명 된 새 페이지 추가 *EmailRequest.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-140">Add a new page named *EmailRequest.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    <span data-ttu-id="c2fa1-141">에 `action` 는 form 요소의 특성으로 설정 되었습니다 *ProcessRequest.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-141">Notice that the `action` attribute of the form element has been set to *ProcessRequest.cshtml*.</span></span> <span data-ttu-id="c2fa1-142">이 대신 현재 페이지에 다시 해당 페이지에는 양식을 제출할 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-142">This means that the form will be submitted to that page instead of back to the current page.</span></span>
3. <span data-ttu-id="c2fa1-143">라는 새 페이지를 추가 *ProcessRequest.cshtml* 웹 사이트에 다음 코드와 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-143">Add a new page named *ProcessRequest.cshtml* to the website and add the following code and markup:</span></span>   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    <span data-ttu-id="c2fa1-144">코드 페이지에 제출 된 양식 필드 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-144">In the code, you get the values of the form fields that were submitted to the page.</span></span> <span data-ttu-id="c2fa1-145">다음 호출에서 `WebMail` 도우미의 `Send` 메서드를 만들고 메일 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-145">You then call the `WebMail` helper's `Send` method to create and send the email message.</span></span> <span data-ttu-id="c2fa1-146">이 경우 사용할 값을 폼에서 전송 된 값으로 연결 하는 텍스트의 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-146">In this case, the values to use are made up of text that you concatenate with the values that were submitted from the form.</span></span>

    <span data-ttu-id="c2fa1-147">이 페이지에 대 한 코드는 내부에 `try/catch` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-147">The code for this page is inside a `try/catch` block.</span></span> <span data-ttu-id="c2fa1-148">전송 시도가 이유로 모든 전자 메일 작동 하지 않는 경우 (예를 들어 설정 되지 오른쪽)의 코드는 `catch` 블록 실행 하 고 설정 하는 `errorMessage` 변수 발생 한 오류를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-148">If for any reason the attempt to send an email doesn't work (for example, the settings aren't right), the code in the `catch` block runs and sets the `errorMessage` variable to the error that has occurred.</span></span> <span data-ttu-id="c2fa1-149">(에 대 한 자세한 내용은 `try/catch` 블록 또는 `<text>` 태그, 참조 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span><span class="sxs-lookup"><span data-stu-id="c2fa1-149">(For more information about `try/catch` blocks or the `<text>` tag, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span></span>

    <span data-ttu-id="c2fa1-150">페이지의 본문에는 경우는 `errorMessage` 변수가 비어 (기본값) 이면 사용자에 게 전자 메일 메시지가 전송 된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-150">In the body of the page, if the `errorMessage` variable is empty (the default), the user sees a message that the email message has been sent.</span></span> <span data-ttu-id="c2fa1-151">경우는 `errorMessage` 변수는 메시지를 보내는 데 문제가 있었습니다 메시지가 사용자에 게 표시 true로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-151">If the `errorMessage` variable is set to true, the user sees a message that there's been a problem sending the message.</span></span>

    <span data-ttu-id="c2fa1-152">오류 메시지를 표시 하는 페이지의 부분에는 추가 테스트: `if(debuggingFlag)`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-152">Notice that in the portion of the page that displays an error message, there's an additional test: `if(debuggingFlag)`.</span></span> <span data-ttu-id="c2fa1-153">이 메일을 보내는 데 문제가 있는 경우 true로 설정할 수 있는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-153">This is a variable that you can set to true if you're having trouble sending email.</span></span> <span data-ttu-id="c2fa1-154">때 `debuggingFlag` 가 true 이면 추가 오류 메시지가 ASP.NET에서 전자 메일 메시지를 보내려고 시도할 때 보고 무엇이 든 보여 주는 표시 전자 메일을 보내는 데 문제가 있으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-154">When `debuggingFlag` is true, and if there's a problem sending email, an additional error message is displayed that shows whatever ASP.NET has reported when it tried to send the email message.</span></span> <span data-ttu-id="c2fa1-155">그러나 fair 경고,: ASP.NET 전자 메일 메시지를 보낼 수 없는 경우를 보고 하는 오류 메시지는 제네릭일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-155">Fair warning, though: the error messages that ASP.NET reports when it can't send an email message can be generic.</span></span> <span data-ttu-id="c2fa1-156">예를 들어 경우 (예를 들어 때문에 서버 이름에는 오류 내용을) ASP.NET SMTP 서버에 연결할 수 없습니다, 오류는 `Failure sending mail`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-156">For example, if ASP.NET can't contact the SMTP server (for example, because you made an error in the server name), the error is `Failure sending mail`.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="c2fa1-157">**중요 한** 예외 개체에서 오류 메시지를 가져올 때 (`ex` 코드에서)를 수행 *하지* 정기적으로 해당 메시지를 통해 사용자에 게 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-157">**Important** When you get an error message from an exception object (`ex` in the code), do *not* routinely pass that message through to users.</span></span> <span data-ttu-id="c2fa1-158">예외 개체에 사용자가 보아서는 안 하 고 보안 취약성도 일 수 있는 정보가 포함 되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-158">Exception objects often include information that users should not see and that can even be a security vulnerability.</span></span> <span data-ttu-id="c2fa1-159">바로 이러한 이유로이 코드에 변수가 포함 되어 `debuggingFlag` 오류 메시지를 표시 하는 스위치로 사용 되는 및 기본적으로 변수를 false로 설정 되어 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-159">That's why this code includes the variable `debuggingFlag` that's used as a switch to display the error message, and why the variable by default is set to false.</span></span> <span data-ttu-id="c2fa1-160">변수를 true (및 따라서 오류 메시지 표시)로 설정 해야 *만* 메일을 보내는 문제가 있는 경우를 디버깅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-160">You should set that variable to true (and therefore display the error message) *only* if you're having a problem with sending email and you need to debug.</span></span> <span data-ttu-id="c2fa1-161">문제를 해결 한 후에 설정할 `debuggingFlag` false로 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-161">Once you have fixed any problems, set `debuggingFlag` back to false.</span></span>

    <span data-ttu-id="c2fa1-162">수정 다음 전자 메일의 코드에서 관련된 설정:</span><span class="sxs-lookup"><span data-stu-id="c2fa1-162">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="c2fa1-163">설정 `your-SMTP-host` 에 액세스할 수 있는 SMTP 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-163">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="c2fa1-164">설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-164">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="c2fa1-165">설정 `your-account-password` 를 SMTP 서버 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-165">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="c2fa1-166">설정 `your-email-address-here` 자신의 전자 메일 주소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-166">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="c2fa1-167">메시지에서 보내는 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-167">This is the email address that the message is sent from.</span></span> <span data-ttu-id="c2fa1-168">(다른 지정할 수는 일부 전자 메일 공급자 주저 하지 마시기 바랍니다 `From` 주소 및 사용자 이름으로 사용 합니다는 `From` 주소입니다.)</span><span class="sxs-lookup"><span data-stu-id="c2fa1-168">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a><span data-ttu-id="c2fa1-169">전자 메일 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c2fa1-169">Configuring Email Settings</span></span>
     > 
     > <span data-ttu-id="c2fa1-170">SMTP 서버, 포트 번호 및에 대 한 올바른 설정을 있는지 확인 하는 경우에 따라 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-170">It can be a challenge sometimes to make sure you have the right settings for the SMTP server, port number, and so on.</span></span> <span data-ttu-id="c2fa1-171">다음은 이에 대한 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-171">Here are a few tips:</span></span>
     > 
     > - <span data-ttu-id="c2fa1-172">SMTP 서버 이름을 방식은 다음과 같이 `smtp.provider.com` 또는 `smtp.provider.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-172">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="c2fa1-173">그러나 사이트를 호스팅 공급자에 게시 하는 경우 SMTP 서버 이름을 해당 지점에서 않을 `localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-173">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="c2fa1-174">게시 한 후 사이트 공급자의 서버에서 실행 되는 전자 메일 서버 응용 프로그램의 관점에서 로컬 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-174">This is because after you've published and your site is running on the provider's server, the email server might be local from the perspective of your application.</span></span> <span data-ttu-id="c2fa1-175">게시 프로세스의 일부로 SMTP 서버 이름을 변경 해야 할 서버 이름에이 변경 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-175">This change in server names might mean you have to change the SMTP server name as part of your publishing process.</span></span>
     > - <span data-ttu-id="c2fa1-176">포트 번호는 일반적으로 25입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-176">The port number is usually 25.</span></span> <span data-ttu-id="c2fa1-177">그러나 일부 공급자 사용 해야 할 포트 587 또는 일부 다른 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-177">However, some providers require you to use port 587 or some other port.</span></span>
     > - <span data-ttu-id="c2fa1-178">올바른 자격 증명을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-178">Make sure that you use the right credentials.</span></span> <span data-ttu-id="c2fa1-179">사이트를 호스팅 공급자에 게시 한 경우 특별히 설정 된 공급자가 전자 메일에 대 한 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-179">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="c2fa1-180">이러한 게시에 사용할 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-180">These might be different from the credentials you use to publish.</span></span>
     > - <span data-ttu-id="c2fa1-181">경우에 따라 자격 증명을 전혀 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-181">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="c2fa1-182">개인 ISP를 사용 하 여 메일을 보내는 전자 메일 공급자 자격 증명 이미 알고 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-182">If you're sending email using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="c2fa1-183">를 게시 한 후 로컬 컴퓨터에서 테스트 아니라 다른 자격 증명을 사용 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-183">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
     > - <span data-ttu-id="c2fa1-184">전자 메일 공급자가 암호화를 사용 하는 경우 설정 해야 `WebMail.EnableSsl` 를 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-184">If your email provider uses encryption, you have to set `WebMail.EnableSsl` to `true`.</span></span>
4. <span data-ttu-id="c2fa1-185">실행 된 *EmailRequest.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-185">Run the *EmailRequest.cshtml* page in a browser.</span></span> <span data-ttu-id="c2fa1-186">(있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.)</span><span class="sxs-lookup"><span data-stu-id="c2fa1-186">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
5. <span data-ttu-id="c2fa1-187">사용자 이름 및 문제 설명, 입력 한 다음 클릭는 **전송** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-187">Enter your name and a problem description, and then click the **Submit** button.</span></span> <span data-ttu-id="c2fa1-188">리디렉션됩니다 하는 *ProcessRequest.cshtml* 페이지에서 메시지를 확인 하는 전자 메일 메시지를 보냅니다입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-188">You're redirected to the *ProcessRequest.cshtml* page, which confirms your message and which sends you an email message.</span></span> 

    ![[image]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a><span data-ttu-id="c2fa1-190">전자 메일을 사용 하 여 파일 전송</span><span class="sxs-lookup"><span data-stu-id="c2fa1-190">Sending a File Using Email</span></span>

<span data-ttu-id="c2fa1-191">전자 메일 메시지에 첨부 된 파일을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-191">You can also send files that are attached to email messages.</span></span> <span data-ttu-id="c2fa1-192">이 절차에서는 두 개의 HTML 페이지 및 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-192">In this procedure, you create a text file and two HTML pages.</span></span> <span data-ttu-id="c2fa1-193">전자 메일 첨부 파일로 텍스트 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-193">You'll use the text file as an email attachment.</span></span>

1. <span data-ttu-id="c2fa1-194">웹 사이트에 새 텍스트 파일을 추가 하 고 이름을 *MyFile.txt*합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-194">In the website, add a new text file and name it *MyFile.txt*.</span></span>
2. <span data-ttu-id="c2fa1-195">다음 텍스트를 복사 하는 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-195">Copy the following text and paste it in the file:</span></span> 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. <span data-ttu-id="c2fa1-196">*SendFile.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-196">Create a page named *SendFile.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. <span data-ttu-id="c2fa1-197">*ProcessFile.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-197">Create a page named *ProcessFile.cshtml* and add the following markup:</span></span> 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. <span data-ttu-id="c2fa1-198">수정 다음 전자 메일의 코드 예제를 관련된 설정:</span><span class="sxs-lookup"><span data-stu-id="c2fa1-198">Modify the following email related settings in the code from the example:</span></span>

    - <span data-ttu-id="c2fa1-199">설정 `your-SMTP-host` 에 액세스할 수 있는 SMTP 서버 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-199">Set `your-SMTP-host` to the name of an SMTP server that you have access to.</span></span>
    - <span data-ttu-id="c2fa1-200">설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-200">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="c2fa1-201">설정 `your-email-address-here` 자신의 전자 메일 주소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-201">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="c2fa1-202">메시지에서 보내는 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-202">This is the email address that the message is sent from.</span></span>
    - <span data-ttu-id="c2fa1-203">설정 `your-account-password` 를 SMTP 서버 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-203">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="c2fa1-204">설정 `target-email-address-here` 자신의 전자 메일 주소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-204">Set `target-email-address-here` to your own email address.</span></span> <span data-ttu-id="c2fa1-205">(에 따라 이전에 보내는 것과 일반적으로 전자 메일을 다른 사람에 게 테스트를 위해 있습니다 수 자신에 게 보냅니다.)</span><span class="sxs-lookup"><span data-stu-id="c2fa1-205">(As before, you'd normally send an email to someone else, but for testing, you can send it to yourself.)</span></span>
6. <span data-ttu-id="c2fa1-206">실행 된 *SendFile.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-206">Run the *SendFile.cshtml* page in a browser.</span></span>
7. <span data-ttu-id="c2fa1-207">사용자 이름, 제목 줄 및 연결할 텍스트 파일의 이름 입력 (*MyFile.txt*).</span><span class="sxs-lookup"><span data-stu-id="c2fa1-207">Enter your name, a subject line, and the name of the text file to attach (*MyFile.txt*).</span></span>
8. <span data-ttu-id="c2fa1-208">`Submit` 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-208">Click the `Submit` button.</span></span> <span data-ttu-id="c2fa1-209">이동 하는 이전에 *ProcessFile.cshtml* 페이지에서 메시지를 확인 하 고 하는 메시지를 보냅니다 전자 메일 첨부 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2fa1-209">As before, you're redirected to the *ProcessFile.cshtml* page, which confirms your message and which sends you an email message with the attached file.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c2fa1-210">추가 자료</span><span class="sxs-lookup"><span data-stu-id="c2fa1-210">Additional Resources</span></span>


- [<span data-ttu-id="c2fa1-211">ASP.NET 웹 페이지(Razor) 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="c2fa1-211">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)
- [<span data-ttu-id="c2fa1-212">Simple Mail Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="c2fa1-212">Simple Mail Transfer Protocol</span></span>](https://msdn.microsoft.com/library/aa480435.aspx)
- [<span data-ttu-id="c2fa1-213">ASP.NET 웹 페이지에 대 한 사이트 전체 동작을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c2fa1-213">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
