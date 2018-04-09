---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: ASP.NET 웹 페이지를 소개-WebMatrix를 사용 하 여 사이트를 게시 | Microsoft Docs
author: tfitzmac
description: 이 자습서에서 Microsoft WebMatrix 및 ASP.NET 웹 페이지를 소개 하는 자습서 집합입니다. T 사이트를 게시 하는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: 7b9bffac5cc72e1bea3f1b211cc03be2ccb8e499
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="2efa8-104">WebMatrix를 사용 하 여 사이트를 게시 하는 ASP.NET 웹 페이지-소개</span><span class="sxs-lookup"><span data-stu-id="2efa8-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>
====================
<span data-ttu-id="2efa8-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2efa8-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="2efa8-106">이 자습서에서 Microsoft WebMatrix 및 ASP.NET 웹 페이지를 소개 하는 자습서 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="2efa8-107">다른 사람이 사용할 수 있도록 사이트를 인터넷에 게시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="2efa8-108">통해 시리즈를 완료 한 것으로 가정 [ASP.NET 웹 페이지 사이트에 대 한 일관성 확인을 만드는](https://go.microsoft.com/fwlink/?LinkId=251585)합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="2efa8-109">사용 하 여 사이트를 게시 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="2efa8-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2efa8-110">Microsoft Azure</span></span>
> - <span data-ttu-id="2efa8-111">웹 호스팅 회사</span><span class="sxs-lookup"><span data-stu-id="2efa8-111">Web Hosting Company</span></span>


## <a name="about-publishing-your-site"></a><span data-ttu-id="2efa8-112">사이트에 게시 하는 방법에 대 한</span><span class="sxs-lookup"><span data-stu-id="2efa8-112">About Publishing Your Site</span></span>

<span data-ttu-id="2efa8-113">지금 까지는 페이지 테스트를 비롯 하 여 로컬 컴퓨터에서 모든 작업 작업을 수행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="2efa8-114">실행 하 여<em>.cshtml</em> 페이지를 사용한 적이 있다면 WebMatrix, IIS Express 즉에 기본 제공 되는 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="2efa8-115">하지만 물론 온다는 점만 다릅니다 만든 사이트를 볼 수 사람이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="2efa8-116">사용자 사이트와 함께 작업을 수 있게 하려면 인터넷에 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="2efa8-117">게시 포함 된 계정을 보유 해야 한다는 의미는 공용 웹 서버에 대 한 액세스를 이미 있는 경우가 아니면는 *클라우드 플랫폼* 또는 *호스팅 공급자*합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="2efa8-118">Microsoft Azure 같은 클라우드 플랫폼 응용 프로그램에 대 한 주문형 인프라를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="2efa8-119">호스팅 공급자는 공개적으로 액세스할 수 있는 웹 서버를 소유 하 고 있습니다 됩니다 대 여 회사 사이트에 대 한 공간.</span><span class="sxs-lookup"><span data-stu-id="2efa8-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="2efa8-120">호스팅 계획 한 달에 몇 달러 실행 (또는 심지어 무료) 한 달 대규모 상용 웹 사이트에 대 한 달러의 많은 수백 소규모 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="2efa8-121">인터넷 서비스 집에서 가져오는 데 사용할 수 있는 인터넷 서비스 공급자 (ISP)를 통해 공용 웹 서버에 대 한 액세스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="2efa8-122">그러나 호스팅 공급자는 ASP.NET 웹 페이지를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="2efa8-123">많은 Isp 하지 하지만 항상 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-123">Many ISPs don't, but it's always worth checking.</span></span>


<span data-ttu-id="2efa8-124">이 자습서에서는 게시 하는 방법에 대해 간략하게를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="2efa8-125">프로세스는 모든 호스팅 공급자에 대 한 약간 다르기 때문에 모든 항목에 대 한 정확한 세부 정보를 제공 하지 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="2efa8-126">하지만 프로세스의 작동 방식에 대 한 유용한 정보를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="2efa8-127">이 자습서에는 4 개의 섹션이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="2efa8-128">기본 페이지 설정</span><span class="sxs-lookup"><span data-stu-id="2efa8-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="2efa8-129">게시 (다음 중 하나를 선택)</span><span class="sxs-lookup"><span data-stu-id="2efa8-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="2efa8-130">a.</span><span class="sxs-lookup"><span data-stu-id="2efa8-130">a.</span></span> [<span data-ttu-id="2efa8-131">Microsoft Azure 사이트에 게시</span><span class="sxs-lookup"><span data-stu-id="2efa8-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="2efa8-132">b.</span><span class="sxs-lookup"><span data-stu-id="2efa8-132">b.</span></span> [<span data-ttu-id="2efa8-133">웹 호스팅 회사 사이트에 게시</span><span class="sxs-lookup"><span data-stu-id="2efa8-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="2efa8-134">라이브 사이트 업데이트: 다시 게시</span><span class="sxs-lookup"><span data-stu-id="2efa8-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="2efa8-135">기본 페이지 설정</span><span class="sxs-lookup"><span data-stu-id="2efa8-135">Setting up the default page</span></span>

<span data-ttu-id="2efa8-136">사용자가 웹 사이트에 대 한 기본 주소를 탐색 하는 경우 사이트에 대 한 기본 페이지가 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="2efa8-137">예를 들어 Default.htm www.contoso.com에는 사이트에 대 한 기본 페이지로 설정 되 면 다음로 이동 <strong>www.contoso.com</strong> 로 이동 하는 것과 같습니다 <strong>www.contoso.com/Default.htm</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-137">For example, when Default.htm is set as the default page for the site at www.contoso.com, then navigating to <strong>www.contoso.com</strong> is the same as navigating to <strong>www.contoso.com/Default.htm</strong>.</span></span>

<span data-ttu-id="2efa8-138">사이트에서 사용 하는 현재 **Default.cshtml** 기본 페이지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="2efa8-139">이 페이지는 사용자의 기본 페이지에 대 한 세밀 하 게 하지만이 자습서에서는 추가 하지 않은 모든 콘텐츠 해당 페이지에는 빈 페이지를 표시 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="2efa8-140">Default.cshtml 열고 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="2efa8-141">사이트에 게시할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-141">Now your site is ready for publication.</span></span> <span data-ttu-id="2efa8-142">첫째, 사이트, Azure로 배포 하는 방법 및 웹 호스팅 회사에 배포 하는 방법 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="2efa8-143">웹 사이트가 있으며 둘 다 옵션 작동 배포 옵션 중 하나를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="2efa8-144">Microsoft Azure 사이트에 게시</span><span class="sxs-lookup"><span data-stu-id="2efa8-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="2efa8-145">이 자습서는 Microsoft azure 사이트를 배포 하는 방법을 먼저 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="2efa8-146">Microsoft 계정, 로그인 하 여 Azure에서 최대 10 개의 무료 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="2efa8-147">이러한 무료 사이트는 사이트를 테스트 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="2efa8-148">항상 모든 사용 가능한 사이트를 사용 하지 않도록 하려면 나중에이 예제에서는 사이트를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="2efa8-149">몇 분에서에서 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2efa8-150">자세한 내용은 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="2efa8-151">WebMatrix 리본에서는 **게시** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix 리본 메뉴의 'publish' 단추](publishing/_static/image1.png)

<span data-ttu-id="2efa8-153">**사이트 게시** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="2efa8-154">Microsoft 계정에 로그인 하지 않은 경우에 대화 상자가 포함 됩니다는 **Azure를 시작** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="2efa8-155">이 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-155">Click this link.</span></span>

![사이트 게시](publishing/_static/image2.png)

<span data-ttu-id="2efa8-157">Microsoft 계정에 로그인 하지 않은 경우 로그인 할 수 있는 기회를 다시 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="2efa8-158">Azure에서 사이트를 게시 하려면 Microsoft 계정에 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![링크를](publishing/_static/image3.png)

<span data-ttu-id="2efa8-160">Microsoft 계정에 로그인 한 후 대화 상자는 Azure에서 새 사이트를 만들거나 Azure에서 기존 사이트 중 하나에 연결 하는 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![새 사이트 만들기](publishing/_static/image4.png)

<span data-ttu-id="2efa8-162">선택 **새 사이트를 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-162">Select **Create a new site**.</span></span>

<span data-ttu-id="2efa8-163">프로젝트의 이름을 **WebPagesMovies**, 사이트에 대 한 기본 이름은 **webpagesmovies.azurewebsites.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="2efa8-164">이 기본 이름은 가능성이 가장 높은 빨간색 느낌표가 표시 된 대로 사용할 수 있는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![기본 웹 사이트 이름](publishing/_static/image5.png)

<span data-ttu-id="2efa8-166">를 사용할 수 있는 사이트 이름을 변경 하 고 사용자의 위치 가까이 있는 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![변경 된 사이트 이름](publishing/_static/image6.png)

<span data-ttu-id="2efa8-168">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-168">Click **OK**.</span></span>

<span data-ttu-id="2efa8-169">WebMatrix performss 서버 사이트와 호환 되는지 확인 하는 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![호환성 테스트](publishing/_static/image7.png)

<span data-ttu-id="2efa8-171">선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-171">Select **Continue**.</span></span>

<span data-ttu-id="2efa8-172">호환성 테스트 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-172">The results of the compatibility test are displayed.</span></span>

![호환성 결과](publishing/_static/image8.png)

<span data-ttu-id="2efa8-174">선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-174">Select **Continue**.</span></span>

<span data-ttu-id="2efa8-175">WebMatrix는 파일 및 사이트에 게시 되는 데이터베이스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="2efa8-176">이 사이트를 게시 하는 처음으로 이므로 파일을 모두 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="2efa8-177">게시할 준비가 되지 않은 파일이 선택을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="2efa8-178">후속 게시에서 변경 된 파일만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="2efa8-179">참조 [라이브 사이트 업데이트: 재게시](#update)합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-179">See [Updating the Live Site: Republishing](#update).</span></span>

![게시 미리 보기](publishing/_static/image9.png)

<span data-ttu-id="2efa8-181">선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-181">Select **Continue**.</span></span>

<span data-ttu-id="2efa8-182">사이트에 Azure에 배포 된 배포 완료 되었음을 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![전체 게시](publishing/_static/image10.png)

<span data-ttu-id="2efa8-184">사이트 및 데이터베이스를 Azure에 게시 된 및 공개적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="2efa8-185">게시가 완료 되 고 사이트에 배포 된 표시를 나타내는 메시지의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="2efa8-186">인터넷에 연결 된 모든 사용자를 추가 하거나 데이터베이스에서 레코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="2efa8-187">웹 호스팅 회사 사이트에 게시</span><span class="sxs-lookup"><span data-stu-id="2efa8-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="2efa8-188">Azure에 게시 하지 않으려면 사이트는 웹 호스팅 회사를 대신 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="2efa8-189">클릭는 **웹 호스팅 찾기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-189">Click the **Find web hosting** link.</span></span>

![게시 설정 대화 상자에서 '웹 호스팅 찾기' 단추](publishing/_static/image12.png)

<span data-ttu-id="2efa8-191">ASP.NET을 지 원하는 호스팅 공급자를 나열 하는 Microsoft 사이트는 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![호스팅 공급자를 나열 하는 Microsoft 사이트에서 페이지](publishing/_static/image13.png)

<span data-ttu-id="2efa8-193">물론, 장기간 동안 필요할 수 있습니다 호스팅 기능 정확히 알고 이제 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="2efa8-194">다음은 몇 가지 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="2efa8-195">WebPagesMovies 사이트를 위해 추가 비용이 자주 하는 SQL Server에 대 한 별도 추가 기능을 포함 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="2efa8-196">사이트에 사용 하는 SQL Server Compact Edition는 독립적인 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="2efa8-197">그러나 수행 하는 몇 가지 이후 웹 사이트 작업에 대 한 SQL Server 액세스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="2efa8-198">생각 되 면 나중에 SQL Server 기능을 추가할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="2efa8-199">호스팅 공급자는 웹 배포 게시 프로토콜을 지원 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="2efa8-200">FTP 프로토콜을 사용 하 여 게시할 수는 있지만 웹 배포 사용 하려면 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="2efa8-201">일부 사이트 무료 평가 기간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="2efa8-202">무료 평가판 이면 게시를 시도 하는 좋은 방법 및 동안 호스팅 중인 계속 작업할 수 있도록 WebMatrix 및 ASP.NET 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="2efa8-203">마음에 드는 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-203">Pick one that you like.</span></span> <span data-ttu-id="2efa8-204">이 자습서에서는 있기 때문에 자습서 등을 만드는 것 하는 동안 해당 회사 사이트에 대 한 몇 개월 무료 사용자 수 있도록 프로 모션 DiscountASP.NET를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="2efa8-205">이 자습서에 대 한 호스팅 공급자의 선택한 다른 언어가 해당 회사의 인증으로 해석 해서는 안 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="2efa8-206">이해를 돕기 하나를 선택 해야 하지만 DiscountASP.NET 게시에 대 한 ASP.NET 웹 페이지 및 Web Deploy 프로토콜을 지 원하는 된 많은 회사 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>


<span data-ttu-id="2efa8-207">일반적으로 호스팅 공급자와 함께 등록 한 후에 회사 사용자 이름 및 암호를 웹 서버 및 등의 URL 포함 하는 메일 있습니다 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="2efa8-208">호스팅 회사에 Web Deploy 프로토콜을 지 원하는 경우 포함 하는 파일 게시 설정 하거나 하나를 다운로드 하면 보내는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="2efa8-209">게시 설정 파일을 간단 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="2efa8-210">가입 하 고 게시할 준비가 되 면 클릭는 **게시** WebMatrix 리본 메뉴의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="2efa8-211">**게시 설정** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="2efa8-212">호스팅 공급자는 게시 설정 파일을 전송, 클릭는 **게시 설정 가져오기** 에 연결 하 고 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="2efa8-213">호스팅 회사 전자 메일의 보낸 사람 값을 사용 하 여 게시 설정 파일에 없을 경우 필드에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="2efa8-214">다음은 무엇는 **게시 설정** 대화 상자를 완료 하면 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![게시 설정 대화 상자에서 게시 설정 입력](publishing/_static/image14.png)

<span data-ttu-id="2efa8-216">클릭 **연결 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-216">Click **Validate Connection**.</span></span> <span data-ttu-id="2efa8-217">대화 상자를 보고 하는 경우 모든 텍스트가 유효함을 **성공적으로 연결**, 호스팅 공급자의 서버와 통신할 수 있다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![성공 하는 경우 메시지 게시 설정이 올바른지](publishing/_static/image15.png)

<span data-ttu-id="2efa8-219">문제가 경우 WebMatrix 문제가 무엇 인지 파악 하 최적화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![문제가 있는 경우 오류 메시지 게시 설정](publishing/_static/image16.png)

<span data-ttu-id="2efa8-221">클릭 **저장** 여 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="2efa8-222">WebMatrix는 호스팅 사이트와 올바르게 통신할 수 있는지 확인 하는 테스트를 수행 하는 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![게시 프로세스의 테스트를 수행 하려면 제공 메시지](publishing/_static/image17.png)

<span data-ttu-id="2efa8-224">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-224">Click **Yes**.</span></span> <span data-ttu-id="2efa8-225">WebMatrix는 호스팅 공급자에 몇 가지 샘플 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="2efa8-226">호환성 테스트 수행 되는 경우 WebMatrix는 결과 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![게시 테스트의 결과](publishing/_static/image18.png)

<span data-ttu-id="2efa8-228">준비가 끝난 것 계속 진행 하 고 클릭 **계속** 실제 게시 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="2efa8-229">WebMatrix 찾습니다 어떤 파일에 사이트 및 (ा त, 없음)은 호스트 서버에 이미 있는 있으며 게시 프로세스의 미리 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![게시 프로세스에 업로드 하는 파일의 미리 보기](publishing/_static/image19.png)

<span data-ttu-id="2efa8-231">와 같은 사용자가 만든 웹 페이지를 포함 하는 게시 파일 목록이 *Movies.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="2efa8-232">또한 목록 파일을 데이터베이스에 대 한 SQL Server Compact Edition을 실행 하 고 등를 설치한 다음 도우미에 대 한 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="2efa8-233">결과적으로, 초기 게시 프로세스가 상당히 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="2efa8-234">**계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-234">Click **Continue**.</span></span> <span data-ttu-id="2efa8-235">WebMatrix는 호스팅 공급자의 서버에 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="2efa8-236">완료 되 면 상태 표시줄에 결과가 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-236">When it's done, the results are reported in the status bar:</span></span>

![게시 프로세스가 성공적으로 완료 되 면 상태 표시줄 메시지](publishing/_static/image20.png)

<span data-ttu-id="2efa8-238">라이브 사이트를 확인 하려면 상태 표시줄에 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="2efa8-239">추가 *동영상* URL로 표시 됩니다는 *Movies.cshtml* 만든 파일:</span><span class="sxs-lookup"><span data-stu-id="2efa8-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![영화 페이지를 보여 주는 라이브 사이트](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="2efa8-241">라이브 사이트 업데이트: 다시 게시</span><span class="sxs-lookup"><span data-stu-id="2efa8-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="2efa8-242">두 개 있는 사이트에 게시 (중 하나 또는 Azure에는 웹 호스팅 회사), 한 &mdash; 컴퓨터와 서비스 공급자에 있는 버전의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="2efa8-243">사이트를 개발 계속 좋을 것 (여기서도 하는 경우 다음 자습서 집합의 일부로).</span><span class="sxs-lookup"><span data-stu-id="2efa8-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="2efa8-244">이렇게 하면 서비스 공급자에 게 컴퓨터에서 변경 내용을 복사 하려면 사이트를 다시 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="2efa8-245">WebMatrix에서 게시 프로세스 파일이 사이트에서 변경 된를 확인 하 고 해당 파일을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="2efa8-246">다시 게시의 작동 방식을 확인 하려면 열고는 *Movies.cshtml* 사이트 일부 약간만 변경 하 고 다음 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="2efa8-247">예를 들어 제목을 변경 `Movies - Updated`합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="2efa8-248">클릭는 **게시** 리본의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="2efa8-249">WebMatrix 기능 변경 되 고 게시 하는 파일의 위치를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![재게시 작업을 위한 기록할 파일을 보여 주는 변경 된 [게시] 대화 상자](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="2efa8-251">기본적으로 WebMatrix 게시 데이터베이스 (*.sdf* 파일)만 사이트를 게시할 처음으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="2efa8-252">사이트에 게시 되 면 사용자 웹 사이트와 상호 작용 하는 라이브 사이트에 있는 데이터베이스는 일반적으로 사이트의 실제 데이터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="2efa8-253">라이브 데이터베이스를 덮어쓰지 매우 주의 해야 할는 *.sdf* 만 테스트 데이터를 포함 하는 컴퓨터에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="2efa8-254">바로 이러한 이유로 경고가 표시 **게시 모든 원격 데이터베이스를 덮어쓰게 됩니다**에 대 한 확인란 이유 및 *WebPagesMovies.sdf* 은 기본적으로 선택 취소 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>


<span data-ttu-id="2efa8-255">**계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-255">Click **Continue**.</span></span> <span data-ttu-id="2efa8-256">WebMatrix는 변경 된 파일을 게시 하 고 처음으로 게시와 같게 성공 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="2efa8-257">라이브 사이트 (클릭할 수 있는 성공 메시지의 링크 여전히 표시)로 이동 하 고 변경 내용을 게시 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="2efa8-258">**원격 파일 편집**</span><span class="sxs-lookup"><span data-stu-id="2efa8-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="2efa8-259">사이트를 변경 하 고 다음 다시 게시 하는 대신, WebMatrix 원격 파일을 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="2efa8-260">이 시나리오에서는 서비스 공급자에 있는 파일을 열면 및 WebMatrix 다운로드는 해당 복사본을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="2efa8-261">파일을 저장할 때마다 WebMatrix 사이트는 변경 내용을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="2efa8-262">원격 편집은 쉽게 라이브 사이트를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="2efa8-263">그러나 이러한 방식으로 수행한 변경 내용은 로컬 사이트에서 파일에 대해 동기화 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="2efa8-264">로컬 파일을 원격 사이트와 동기화 하려면 원격 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="2efa8-265">이 방법은 매우 비슷한 게시를 제외 하 고 반대 방향으로.</span><span class="sxs-lookup"><span data-stu-id="2efa8-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="2efa8-266">원격 편집 및 다운로드 원격 기능을 WebMatrix 여기에 대 한 더 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="2efa8-267">여러 사용자가 작업 서로 다른 컴퓨터에 동일한 사이트에서 수행 해야 하는 경우 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="2efa8-268">자세한 내용은 참조 [게시 및 WebMatrix 2 베타와 원격 사이트 편집](https://go.microsoft.com/fwlink/?LinkId=251591)합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2efa8-269">추가 자료</span><span class="sxs-lookup"><span data-stu-id="2efa8-269">Additional Resources</span></span>

- <span data-ttu-id="2efa8-270">[ASP.NET WebMatrix ASP.NET 웹 페이지 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), 게시 하는 좋은 장소 질문 및 답변 합니다.</span><span class="sxs-lookup"><span data-stu-id="2efa8-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2efa8-271">이전</span><span class="sxs-lookup"><span data-stu-id="2efa8-271">Previous</span></span>](layouts.md)
