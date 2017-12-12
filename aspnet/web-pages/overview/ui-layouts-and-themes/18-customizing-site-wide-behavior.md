---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: "ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작을 사용자 지정 | Microsoft Docs"
author: tfitzmac
description: "이 장의 페이지 뿐 아니라 전체 웹 사이트 또는 전체 폴더를 설정 하는 방법에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: b1caa26a23517bd976addfefac89375ae965eb91
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a><span data-ttu-id="a9778-103">ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a9778-103">Customizing Site-Wide Behavior for ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="a9778-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a9778-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a9778-105">이 문서에는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 페이지에 대 한 사이트 측 설정을 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-105">This article explains how to make site-side settings for pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="a9778-106">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="a9778-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a9778-107">코드를 실행할 수 있도록 하는 방법 집합 (전역 값 또는 설정 도우미)는 사이트의 모든 페이지에 대 한 값.</span><span class="sxs-lookup"><span data-stu-id="a9778-107">How to run code that lets you set values (global values or helper settings) for all pages in a site.</span></span>
> - <span data-ttu-id="a9778-108">폴더의 모든 페이지에 대 한 값을 설정할 수 있는 코드를 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-108">How to run code that lets you set values for all pages in a folder.</span></span>
> - <span data-ttu-id="a9778-109">이전 및 이후 페이지 코드를 실행 하는 방법에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-109">How to run code before and after a page loads.</span></span>
> - <span data-ttu-id="a9778-110">중앙 오류 페이지를 오류를 보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-110">How to send errors to a central error page.</span></span>
> - <span data-ttu-id="a9778-111">폴더의 모든 페이지에 인증을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-111">How to add authentication to all pages in a folder.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a9778-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="a9778-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a9778-113">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="a9778-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="a9778-114">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="a9778-114">WebMatrix 3</span></span>
> - <span data-ttu-id="a9778-115">ASP.NET Web Helpers Library (NuGet 패키지)</span><span class="sxs-lookup"><span data-stu-id="a9778-115">ASP.NET Web Helpers Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="a9778-116">이 자습서는 ASP.NET 웹 페이지 3으로도 작동 하 고 Visual Studio 2013 (또는 Visual Studio Express 2013 for Web) 온다는 점만 다릅니다 ASP.NET Web Helpers Library를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-116">This tutorial also works with ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web), except you cannot use the ASP.NET Web Helpers Library.</span></span>


<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a><span data-ttu-id="a9778-117">ASP.NET 웹 페이지에 대 한 웹 사이트 시작 코드 추가</span><span class="sxs-lookup"><span data-stu-id="a9778-117">Adding Website Startup Code for ASP.NET Web Pages</span></span>

<span data-ttu-id="a9778-118">ASP.NET 웹 페이지에서 작성 하는 코드의 대부분에 대 한 개별 페이지는 해당 페이지에 대해 필요한 모든 코드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-118">For much of the code that you write in ASP.NET Web Pages, an individual page can contain all the code that's required for that page.</span></span> <span data-ttu-id="a9778-119">예를 들어 페이지에 전자 메일 메시지를 보내면 경우 단일 페이지에 해당 작업에 대 한 모든 코드를 저장할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-119">For example, if a page sends an email message, it's possible to put all the code for that operation in a single page.</span></span> <span data-ttu-id="a9778-120">이 전자 메일에 대 한 설정을 초기화 하는 코드를 포함할 수 있습니다 (즉, SMTP 서버에 대 한) 및 전자 메일 메시지를 보내기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-120">This can include the code to initialize the settings for sending email (that is, for the SMTP server) and for sending the email message.</span></span>

<span data-ttu-id="a9778-121">그러나 경우에 따라 사이트에서 모든 페이지를 실행 하기 전에 일부 코드를 실행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-121">However, in some situations, you might want to run some code before any page on the site runs.</span></span> <span data-ttu-id="a9778-122">이 사이트의 어디서 나 사용할 수 있는 값을 설정 하는 데 유용 (라고 *전역 값*.) 예를 들어 일부 도우미에 전자 메일 설정 또는 계정 키와 같은 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-122">This is useful for setting values that can be used anywhere in the site (referred to as *global values*.) For example, some helpers require you to provide values like email settings or account keys.</span></span> <span data-ttu-id="a9778-123">전역 값에서 이러한 설정을 사용 하려면 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-123">It can be handy to keep these settings in global values.</span></span>

<span data-ttu-id="a9778-124">명명 된 페이지를 만들어 이렇게 하려면  *\_AppStart.cshtml* 사이트의 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-124">You can do this by creating a page named *\_AppStart.cshtml* in the root of the site.</span></span> <span data-ttu-id="a9778-125">이 페이지에 있는 경우 요청 된 모든 페이지는 사이트에 처음으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-125">If this page exists, it runs the first time any page in the site is requested.</span></span> <span data-ttu-id="a9778-126">따라서 것이 전역 값을 설정 하는 코드를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-126">Therefore, it's a good place to run code to set global values.</span></span> <span data-ttu-id="a9778-127">(때문에  *\_AppStart.cshtml* 밑줄 전위는 사용자가 직접 요청 하는 경우에 ASP.NET 브라우저에 페이지 보내지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="a9778-127">(Because *\_AppStart.cshtml* has an underscore prefix, ASP.NET won't send the page to a browser even if users request it directly.)</span></span>

<span data-ttu-id="a9778-128">다음 다이어그램에서는 방법을  *\_AppStart.cshtml* 페이지 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-128">The following diagram shows how the *\_AppStart.cshtml* page works.</span></span> <span data-ttu-id="a9778-129">요청 된 페이지 들어오고 경우 이것이 첫 번째 요청에 대 한 페이지 ASP.NET 사이트의 첫 번째 확인 여부는  *\_AppStart.cshtml* 페이지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-129">When a request comes in for a page, and if this is the first request for any page in the site, ASP.NET first checks whether a *\_AppStart.cshtml* page exists.</span></span> <span data-ttu-id="a9778-130">이 경우 코드에서  *\_AppStart.cshtml* 페이지가 실행, 한 다음 요청된 된 페이지 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-130">If so, any code in the *\_AppStart.cshtml* page runs, and then the requested page runs.</span></span>

![[image]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a><span data-ttu-id="a9778-132">웹 사이트에 대 한 전역 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-132">Setting Global Values for Your Website</span></span>

1. <span data-ttu-id="a9778-133">WebMatrix 웹 사이트의 루트 폴더에 라는 파일을 만듭니다  *\_AppStart.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-133">In the root folder of a WebMatrix website, create a file named *\_AppStart.cshtml*.</span></span> <span data-ttu-id="a9778-134">파일은 사이트의 루트에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-134">The file must be in the root of the site.</span></span>
2. <span data-ttu-id="a9778-135">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-135">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    <span data-ttu-id="a9778-136">에 값을 저장 하는이 코드는 `AppState` 사이트의 모든 페이지에 자동으로 사용할 수 있는 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-136">This code stores a value in the `AppState` dictionary, which is automatically available to all pages in the site.</span></span> <span data-ttu-id="a9778-137">에  *\_AppStart.cshtml* 파일에 모든 태그가 들어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-137">Notice that the *\_AppStart.cshtml* file does not have any markup in it.</span></span> <span data-ttu-id="a9778-138">페이지가 됩니다 코드를 실행 하 고 원래 요청 된 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-138">The page will run the code and then redirect to the page that was originally requested.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a9778-139">에 코드를 배치할 때 주의 해야는  *\_AppStart.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-139">Be careful when you put code in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="a9778-140">코드에서 오류가 발생 한 경우는  *\_AppStart.cshtml* 파일을 웹 사이트 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-140">If any errors occur in code in the *\_AppStart.cshtml* file, the website won't start.</span></span>
3. <span data-ttu-id="a9778-141">루트 폴더에 명명 된 새 페이지를 만듭니다 *AppName.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-141">In the root folder, create a new page named *AppName.cshtml*.</span></span>
4. <span data-ttu-id="a9778-142">기본 태그 및 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-142">Replace the default markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    <span data-ttu-id="a9778-143">이 코드의 값을 추출는 `AppState` 개체에서 설정 하는  *\_AppStart.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="a9778-143">This code extracts the value from the `AppState` object that you set in the *\_AppStart.cshtml* page.</span></span>
5. <span data-ttu-id="a9778-144">실행 된 *AppName.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-144">Run the *AppName.cshtml* page in a browser.</span></span> <span data-ttu-id="a9778-145">(있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.) 페이지는 전역 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-145">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays the global value.</span></span> 

    ![[image]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a><span data-ttu-id="a9778-147">도우미에 대 한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-147">Setting Values for Helpers</span></span>

<span data-ttu-id="a9778-148">에 대 한 적절 하 게 사용은  *\_AppStart.cshtml* 파일은 사이트에서 사용 하 고 초기화 해야 하는 도우미에 대 한 값을 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-148">A good use for the *\_AppStart.cshtml* file is to set values for helpers that you use in your site and that have to be initialized.</span></span> <span data-ttu-id="a9778-149">일반적인 예로 전자 메일 설정에 대 한는 `WebMail` 도우미와에 대 한 개인 및 공개 키의 `ReCaptcha` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-149">Typical examples are email settings for the `WebMail` helper and the private and public keys for the `ReCaptcha` helper.</span></span> <span data-ttu-id="a9778-150">이와 같은 경우에 한 번으로 값을 설정할 수는  *\_AppStart.cshtml* 로 있습니다 하는 이미 설정한 모든 페이지에 대 한 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-150">In cases like these, you can set the values once in the *\_AppStart.cshtml* and then they're already set for all the pages in your site.</span></span>

<span data-ttu-id="a9778-151">이 절차에서는 설정 하는 방법을 보여 줍니다 `WebMail` 설정을 전역적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-151">This procedure shows you how to set `WebMail` settings globally.</span></span> <span data-ttu-id="a9778-152">(사용 하는 방법에 대 한 자세한 내용은 `WebMail` 도우미, 참조 [ASP.NET 웹 페이지 사이트에 전자 메일 추가](../getting-started/11-adding-email-to-your-web-site.md).)</span><span class="sxs-lookup"><span data-stu-id="a9778-152">(For more information about using the `WebMail` helper, see [Adding Email to an ASP.NET Web Pages Site](../getting-started/11-adding-email-to-your-web-site.md).)</span></span>

1. <span data-ttu-id="a9778-153">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)추가 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="a9778-153">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="a9778-154">아직 없는 경우는  *\_AppStart.cshtml* 파일, 웹 사이트의 루트 폴더에 라는 파일을 만들어  *\_AppStart.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-154">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
3. <span data-ttu-id="a9778-155">다음 추가 `WebMail` 설정을  *\_AppStart.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="a9778-155">Add the following `WebMail` settings to the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    <span data-ttu-id="a9778-156">수정 다음 전자 메일의 코드에서 관련된 설정:</span><span class="sxs-lookup"><span data-stu-id="a9778-156">Modify the following email related settings in the code:</span></span>

    - <span data-ttu-id="a9778-157">설정 `your-SMTP-host` 에 액세스할 수 있는 SMTP 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-157">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
    - <span data-ttu-id="a9778-158">설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-158">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="a9778-159">설정 `your-account-password` 를 SMTP 서버 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-159">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="a9778-160">설정 `your-email-address-here` 자신의 전자 메일 주소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-160">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="a9778-161">메시지에서 보내는 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-161">This is the email address that the message is sent from.</span></span> <span data-ttu-id="a9778-162">(다른 지정할 수는 일부 전자 메일 공급자 주저 하지 마시기 바랍니다 `From` 주소 및 사용자 이름으로 사용 합니다는 `From` 주소입니다.)</span><span class="sxs-lookup"><span data-stu-id="a9778-162">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

    <span data-ttu-id="a9778-163">SMTP 설정에 대 한 자세한 내용은 참조 [전자 메일 설정 구성](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) 문서의 [ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기](https://go.microsoft.com/fwlink/?LinkID=202899) 및 [보내는전자메일문제](https://go.microsoft.com/fwlink/?LinkId=253001#email)에 [ASP.NET 웹 페이지 (Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-163">For more information about SMTP settings, see [Configuring Email Settings](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) in the article [Sending Email from an ASP.NET Web Pages (Razor) Site](https://go.microsoft.com/fwlink/?LinkID=202899) and [Issues with Sending Email](https://go.microsoft.com/fwlink/?LinkId=253001#email) in the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>
- <span data-ttu-id="a9778-164">저장 된  *\_AppStart.cshtml* 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-164">Save the *\_AppStart.cshtml* file and close it.</span></span>
- <span data-ttu-id="a9778-165">웹 사이트의 루트 폴더에 명명 된 새 페이지를 만들 *TestEmail.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-165">In the root folder of a website, create new page named *TestEmail.cshtml*.</span></span>
- <span data-ttu-id="a9778-166">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-166">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
- <span data-ttu-id="a9778-167">실행 된 *TestEmail.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-167">Run the *TestEmail.cshtml* page in a browser.</span></span>
- <span data-ttu-id="a9778-168">전자 메일 메시지를 보내봅니다 누른 다음 필드에 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-168">Fill in the fields to send yourself an email message and then click **Send**.</span></span>
- <span data-ttu-id="a9778-169">메시지 참조 되도록 전자 메일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-169">Check your email to make sure you've gotten the message.</span></span>

<span data-ttu-id="a9778-170">이 예제에서 중요 한 부분은 일반적으로 변경 하지 않는 설정을-SMTP 서버와 전자 메일 자격 증명의 이름이 마음에-에 설정 된는  *\_AppStart.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-170">The important part of this example is that the settings that you don't usually change — like the name of your SMTP server and your email credentials — are set in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="a9778-171">이런 방식으로 다시 설정 각 페이지에서 전자 메일을 전송 하는 위치 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-171">That way you don't need to set them again in each page where you send email.</span></span> <span data-ttu-id="a9778-172">(몇 가지 이유로 이러한 설정을 변경 해야 하는 경우 설정할 수 있지만 개별적으로 페이지에 있습니다.) 페이지에서 일반적으로 받는 사람 및 전자 메일 메시지의 본문 같이 각 시간을 변경 하는 값만 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-172">(Although if for some reason you need to change those settings, you can set them individually in a page.) In the page, you only set the values that typically change each time, like the recipient and the body of the email message.</span></span>

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a><span data-ttu-id="a9778-173">폴더의 파일 전후 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-173">Running Code Before and After Files in a Folder</span></span>

<span data-ttu-id="a9778-174">사용할 수 있습니다 하는 것 처럼  *\_AppStart.cshtml* 코드를 작성 하는 사이트의에서 페이지를 실행 하기 전에, 이전 (및 이후)를 실행 하는 코드를 작성할 수 있습니다 실행 하는 특정 폴더의 모든 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-174">Just like you can use *\_AppStart.cshtml* to write code before pages in the site run, you can write code that runs before (and after) any page in a particular folder run.</span></span> <span data-ttu-id="a9778-175">동일한 레이아웃 페이지 설정 폴더의 모든 페이지에 대 한 또는 검사에 대 한 폴더에는 페이지를 실행 하기 전에 사용자가 로그인 하는 등의 작업에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-175">This is useful for things like setting the same layout page for all the pages in a folder, or for checking that a user is logged in before running a page in the folder.</span></span>

<span data-ttu-id="a9778-176">페이지에 대 한 특히 폴더를 만들 수 있습니다 코드 라는 파일에  *\_PageStart.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-176">For pages in particular folders, you can create code in a file named *\_PageStart.cshtml*.</span></span> <span data-ttu-id="a9778-177">다음 다이어그램에서는 방법을  *\_PageStart.cshtml* 페이지 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-177">The following diagram shows how the *\_PageStart.cshtml* page works.</span></span> <span data-ttu-id="a9778-178">에 대 한 ASP.NET 페이지에 대 한 요청이 들어올 경우 먼저 확인 한  *\_AppStart.cshtml* 페이지 및를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-178">When a request comes in for a page, ASP.NET first checks for a *\_AppStart.cshtml* page and runs that.</span></span> <span data-ttu-id="a9778-179">ASP.NET 있는지 여부를 확인 한 다음는  *\_PageStart.cshtml* 페이지 및 그렇다면를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-179">Then ASP.NET checks whether there's a *\_PageStart.cshtml* page, and if so, runs that.</span></span> <span data-ttu-id="a9778-180">요청된 된 페이지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-180">It then runs the requested page.</span></span>

<span data-ttu-id="a9778-181">내에서  *\_PageStart.cshtml* 페이지에서 요청 된 페이지를 포함 하 여 실행를 처리 하는 동안 위치를 지정할 수는 `RunPage` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a9778-181">Inside the *\_PageStart.cshtml* page, you can specify where during processing you want the requested page to run by including a `RunPage` method.</span></span> <span data-ttu-id="a9778-182">이렇게 하면 요청 된 페이지를 실행 하기 전에 코드를 실행 한 후 다시 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-182">This lets you run code before the requested page runs and then again after it.</span></span> <span data-ttu-id="a9778-183">포함 하지 않으면 `RunPage`, 모든 코드에  *\_PageStart.cshtml* 실행 되 고 요청된 된 페이지 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-183">If you don't include `RunPage`, all the code in *\_PageStart.cshtml* runs, and then the requested page runs automatically.</span></span>

![[image]](18-customizing-site-wide-behavior/_static/image3.jpg)

<span data-ttu-id="a9778-185">ASP.NET를 사용 하면 계층 구조를 만들  *\_PageStart.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-185">ASP.NET lets you create a hierarchy of *\_PageStart.cshtml* files.</span></span> <span data-ttu-id="a9778-186">넣을 수는  *\_PageStart.cshtml* 사이트의 루트에 있는 파일과 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-186">You can put a *\_PageStart.cshtml* file in the root of the site and in any subfolder.</span></span> <span data-ttu-id="a9778-187">페이지 요청 될 때는  *\_PageStart.cshtml* 파일 이어서 최상위 수준 (가장 가까운 사이트 루트) 실행에는  *\_PageStart.cshtml* 다음에서 파일 하위 폴더를 요청에 요청된 된 페이지를 포함 하는 폴더에 도달할 때까지 하위 폴더 구조가 아래의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-187">When a page is requested, the *\_PageStart.cshtml* file at the top-most level (nearest to the site root) runs, followed by the *\_PageStart.cshtml* file in the next subfolder, and so on down the subfolder structure until the request reaches the folder that contains the requested page.</span></span> <span data-ttu-id="a9778-188">모든 적용 가능한 후  *\_PageStart.cshtml* 파일 실행, 요청 된 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-188">After all the applicable *\_PageStart.cshtml* files have run, the requested page runs.</span></span>

<span data-ttu-id="a9778-189">예를 들어 다음과 같은 조합을 해야할  *\_PageStart.cshtml* 파일 및 *Default.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="a9778-189">For example, you might have the following combination of *\_PageStart.cshtml* files and *Default.cshtml* file:</span></span>

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

<span data-ttu-id="a9778-190">실행 하는 경우 */myfolder/default.cshtml*, 다음에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-190">When you run */myfolder/default.cshtml*, you'll see the following:</span></span>

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a><span data-ttu-id="a9778-191">폴더의 모든 페이지에 대 한 초기화 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-191">Running Initialization Code for All Pages in a Folder</span></span>

<span data-ttu-id="a9778-192">에 대 한 적절 하 게 사용  *\_PageStart.cshtml* 파일 단일 폴더에 모든 파일에 대해 동일한 레이아웃 페이지를 초기화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-192">A good use for *\_PageStart.cshtml* files is to initialize the same layout page for all files in a single folder.</span></span>

1. <span data-ttu-id="a9778-193">루트 폴더에서 라는 새 폴더를 만듭니다 *InitPages*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-193">In the root folder, create a new folder named *InitPages*.</span></span>
2. <span data-ttu-id="a9778-194">에 *InitPages* 라는 파일을 만들어 웹 사이트의 폴더  *\_PageStart.cshtml* 기본 태그 및 코드는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-194">In the *InitPages* folder of your website, create a file named *\_PageStart.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. <span data-ttu-id="a9778-195">웹 사이트의 루트에서 라는 폴더를 만듭니다 *Shared*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-195">In the root of the website, create a folder named *Shared*.</span></span>
4. <span data-ttu-id="a9778-196">에 *Shared* 폴더를 라는 파일을 만들어  *\_Layout1.cshtml* 기본 태그 및 코드는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-196">In the *Shared* folder, create a file named *\_Layout1.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. <span data-ttu-id="a9778-197">*InitPages* 폴더를 라는 파일을 만들어 *Content1.cshtml* 기존 콘텐츠는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-197">In the *InitPages* folder, create a file named *Content1.cshtml* and replace the existing content with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. <span data-ttu-id="a9778-198">에 *InitPages* 폴더를 명명 된 다른 파일을 만들 *Content2.cshtml* 기본 태그는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-198">In the *InitPages* folder, create another file named *Content2.cshtml* and replace the default markup with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. <span data-ttu-id="a9778-199">실행 *Content1.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-199">Run *Content1.cshtml* in a browser.</span></span> 

    ![[image]](18-customizing-site-wide-behavior/_static/image4.jpg)

    <span data-ttu-id="a9778-201">경우는 *Content1.cshtml* 실행 페이지는  *\_PageStart.cshtml* 파일 집합 `Layout` 설정 `PageData["MyBackground"]` 색입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-201">When the *Content1.cshtml* page runs, the *\_PageStart.cshtml* file sets `Layout` and also sets `PageData["MyBackground"]` to a color.</span></span> <span data-ttu-id="a9778-202">*Content1.cshtml*, 레이아웃 및 색이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-202">In *Content1.cshtml*, the layout and color are applied.</span></span>
8. <span data-ttu-id="a9778-203">디스플레이 *Content2.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-203">Display *Content2.cshtml* in a browser.</span></span> 

    <span data-ttu-id="a9778-204">초기화 페이지를 둘 다 동일한 페이지 레이아웃 및 색 사용 하기 때문에 레이아웃은 동일  *\_PageStart.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-204">The layout is the same, because both pages use the same layout page and color as initialized in *\_PageStart.cshtml*.</span></span>

## <a name="using-pagestartcshtml-to-handle-errors"></a><span data-ttu-id="a9778-205">사용 하 여 \_PageStart.cshtml 오류 처리</span><span class="sxs-lookup"><span data-stu-id="a9778-205">Using \_PageStart.cshtml to Handle Errors</span></span>

<span data-ttu-id="a9778-206">에 사용 된 다른는  *\_PageStart.cshtml* 파일 하나에서 발생할 수 있는 프로그래밍 오류 (예외)를 처리 하는 방법을 만드는 것 *.cshtml* 폴더에는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-206">Another good use for the *\_PageStart.cshtml* file is to create a way to handle programming errors (exceptions) that might occur in any *.cshtml* page in a folder.</span></span> <span data-ttu-id="a9778-207">이 예제에서는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-207">This example shows you one way to do this.</span></span>

1. <span data-ttu-id="a9778-208">루트 폴더에 라는 폴더를 만듭니다 *InitCatch*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-208">In the root folder, create a folder named *InitCatch*.</span></span>
2. <span data-ttu-id="a9778-209">에 *InitCatch* 라는 파일을 만들어 웹 사이트의 폴더  *\_PageStart.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-209">In the *InitCatch* folder of your website, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    <span data-ttu-id="a9778-210">요청된 된 페이지를 명시적으로 호출 하 여 실행 하면이 코드는 `RunPage` 내에서 메서드는 `try` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-210">In this code, you try running the requested page explicitly by calling the `RunPage` method inside a `try` block.</span></span> <span data-ttu-id="a9778-211">요청 된에서 프로그래밍 오류가 발생 한 경우 페이지 내의 코드는 `catch` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-211">If any programming errors occur in the requested page, the code inside the `catch` block runs.</span></span> <span data-ttu-id="a9778-212">코드는 페이지로 리디렉션합니다.이 경우 (*Error.cshtml*) 오류는 URL의 일부로 발생 하는 파일의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-212">In this case, the code redirects to a page (*Error.cshtml*) and passes the name of the file that experienced the error as part of the URL.</span></span> <span data-ttu-id="a9778-213">(만듭니다 페이지 곧.)</span><span class="sxs-lookup"><span data-stu-id="a9778-213">(You'll create the page shortly.)</span></span>
3. <span data-ttu-id="a9778-214">에 *InitCatch* 라는 파일을 만들어 웹 사이트의 폴더 *Exception.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-214">In the *InitCatch* folder of your website, create a file named *Exception.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    <span data-ttu-id="a9778-215">이 예제에 대 한 일이 페이지에 의도적으로 만들어지고 오류가 존재 하지 않는 데이터베이스 파일을 열려고 시도 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-215">For purposes of this example, what you're doing in this page is deliberately creating an error by trying to open a database file that doesn't exist.</span></span>
4. <span data-ttu-id="a9778-216">루트 폴더에 라는 파일을 만듭니다 *Error.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-216">In the root folder, create a file named *Error.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    <span data-ttu-id="a9778-217">이 페이지에서는 식에서에서 `@Request["source"]` url 값을 가져오고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-217">In this page, the expression `@Request["source"]` gets the value out of the URL and displays it.</span></span>
5. <span data-ttu-id="a9778-218">도구 모음에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-218">In the toolbar, click **Save**.</span></span>
6. <span data-ttu-id="a9778-219">실행 *Exception.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-219">Run *Exception.cshtml* in a browser.</span></span> 

    ![[image]](18-customizing-site-wide-behavior/_static/image5.jpg)

    <span data-ttu-id="a9778-221">오류가 발생 하기 때문에 *Exception.cshtml*,  *\_PageStart.cshtml* 페이지 리디렉션하는 *Error.cshtml* 메시지를 표시 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-221">Because an error occurs in *Exception.cshtml*, the *\_PageStart.cshtml* page redirects to the *Error.cshtml* file, which displays the message.</span></span>

    <span data-ttu-id="a9778-222">예외에 대 한 자세한 내용은 참조 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkID=251587)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-222">For more information about exceptions, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587).</span></span>

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-pagestartcshtml-to-restrict-folder-access"></a><span data-ttu-id="a9778-223">사용 하 여 \_PageStart.cshtml 폴더 액세스를 제한 하려면</span><span class="sxs-lookup"><span data-stu-id="a9778-223">Using \_PageStart.cshtml to Restrict Folder Access</span></span>

<span data-ttu-id="a9778-224">사용할 수도 있습니다는  *\_PageStart.cshtml* 파일을 폴더에 있는 모든 파일에 대 한 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-224">You can also use the *\_PageStart.cshtml* file to restrict access to all the files in a folder.</span></span>

1. <span data-ttu-id="a9778-225">WebMatrix를 사용 하 여 새 웹 사이트를 만들어는 **템플릿에서 사이트** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-225">In WebMatrix, create a new website using the **Site From Template** option.</span></span>
2. <span data-ttu-id="a9778-226">사용 가능한 템플릿에서 선택 **시작 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-226">From the available templates, select **Starter Site**.</span></span>
3. <span data-ttu-id="a9778-227">루트 폴더에 라는 폴더를 만듭니다 *AuthenticatedContent*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-227">In the root folder, create a folder named *AuthenticatedContent*.</span></span>
4. <span data-ttu-id="a9778-228">에 *AuthenticatedContent* 폴더를 라는 파일을 만들어  *\_PageStart.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-228">In the *AuthenticatedContent* folder, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    <span data-ttu-id="a9778-229">코드는 폴더의 모든 파일에 캐시 되는 것을 방지 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-229">The code starts by preventing all files in the folder from being cached.</span></span> <span data-ttu-id="a9778-230">(이 같은 공용 컴퓨터, 한 사용자의 캐시 된 페이지는 다음 사용자에 사용할 수 있도록 않도록 하려는 시나리오에 필요 합니다.) 다음으로 코드 여부는 사용자가 로그인 사이트에 폴더의 모든 페이지를 볼 수 있도록 하려면 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-230">(This is required for scenarios like public computers, where you don't want one user's cached pages to be available to the next user.) Next, the code determines whether the user has signed in to the site before they can view any of the pages in the folder.</span></span> <span data-ttu-id="a9778-231">사용자가 로그인 되지 않은 경우 코드 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-231">If the user is not signed in, the code redirects to the login page.</span></span> <span data-ttu-id="a9778-232">로그인 페이지 라는 쿼리 문자열 값을 포함 하는 경우 원래 요청 된 페이지에 사용자를 반환할 수 `ReturnUrl`합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-232">The login page can return the user to the page that was originally requested if you include a query string value named `ReturnUrl`.</span></span>
5. <span data-ttu-id="a9778-233">새 페이지를 만들고는 *AuthenticatedContent* 라는 폴더 *Page.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-233">Create a new page in the *AuthenticatedContent* folder named *Page.cshtml*.</span></span>
6. <span data-ttu-id="a9778-234">기본 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-234">Replace the default markup with the following:</span></span>  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. <span data-ttu-id="a9778-235">실행 *Page.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-235">Run *Page.cshtml* in a browser.</span></span> <span data-ttu-id="a9778-236">코드는 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-236">The code redirects you to a login page.</span></span> <span data-ttu-id="a9778-237">로그인 하기 전에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-237">You must register before logging in.</span></span> <span data-ttu-id="a9778-238">등록 로그인 한 후 페이지를 탐색 하 고 해당 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9778-238">After you've registered and logged in, you can navigate to the page and view its contents.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a9778-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a9778-239">Additional Resources</span></span>

[<span data-ttu-id="a9778-240">ASP.NET 웹 페이지 Razor 구문을 사용 하 여 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="a9778-240">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
