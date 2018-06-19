---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: 소개 디버깅 ASP.NET 웹 페이지 (Razor) 사이트 | Microsoft Docs
author: tfitzmac
description: 디버깅 하는 것은 프로세스 오류 찾기 및 수정 하면 코드 페이지에서입니다. 이 장에서 몇 가지 도구와 기술을 디버그 하는 데 사용할 수 및 analyz...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: c28d63acda6e585f4aa64f294049c1790faac850
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30897507"
---
<a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a><span data-ttu-id="43496-104">소개 디버깅 ASP.NET 웹 페이지 (Razor) 사이트</span><span class="sxs-lookup"><span data-stu-id="43496-104">Introduction to Debugging ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="43496-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="43496-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="43496-106">이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지를 디버깅 하는 다양 한 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-106">This article explains various ways to debug pages in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="43496-107">디버깅 하는 것은 프로세스 오류 찾기 및 수정 하면 코드 페이지에서입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-107">Debugging is the process of finding and fixing errors in your code pages.</span></span>
> 
> <span data-ttu-id="43496-108">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="43496-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="43496-109">분석 하 고 페이지를 디버깅 하는 데 도움이 되는 정보를 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="43496-109">How to display information that helps analyze and debug pages.</span></span>
> - <span data-ttu-id="43496-110">Visual Studio에서 도구 디버깅을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-110">How to use debugging tools in Visual Studio.</span></span>
>   
> 
> <span data-ttu-id="43496-111">다음은 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-111">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="43496-112">`ServerInfo` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-112">The `ServerInfo` helper.</span></span>
> - <span data-ttu-id="43496-113">`ObjectInfo` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-113">`ObjectInfo` helper.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="43496-114">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="43496-114">Software versions</span></span>
> 
> 
> - <span data-ttu-id="43496-115">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="43496-115">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="43496-116">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="43496-116">Visual Studio 2013</span></span>
>   
> 
> <span data-ttu-id="43496-117">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-117">This tutorial also works with ASP.NET Web Pages 2.</span></span> <span data-ttu-id="43496-118">WebMatrix 3을 사용할 수 있지만 통합 된 디버거 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-118">You can use WebMatrix 3 but the integrated debugger is not supported.</span></span>


<span data-ttu-id="43496-119">오류 및 코드의 문제를 해결 하는 중요 한 부분은 되 게 처음에 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-119">An important aspect of troubleshooting errors and problems in your code is to avoid them in the first place.</span></span> <span data-ttu-id="43496-120">에 오류가 발생할 수 있는 코드의 섹션을 배치 하 여 할 수 있습니다 `try/catch` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-120">You can do that by putting sections of your code that are likely to cause errors into `try/catch` blocks.</span></span> <span data-ttu-id="43496-121">자세한 내용은 섹션을 참조에서 오류 처리에 [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890)합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-121">For more information, see the section on handling errors in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890).</span></span>

<span data-ttu-id="43496-122">`ServerInfo` 도우미는 페이지를 호스팅하는 웹 서버 환경에 대 한 정보의 개요를 제공 하는 진단 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-122">The `ServerInfo` helper is a diagnostic tool that gives you an overview of information about the web server environment that hosts your page.</span></span> <span data-ttu-id="43496-123">또한, 브라우저 페이지를 요청할 때 전송 되는 HTTP 요청 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-123">It also shows you HTTP request information that's sent when a browser requests the page.</span></span> <span data-ttu-id="43496-124">`ServerInfo` 현재 사용자 id는 요청한 브라우저의 종류를 표시 하는 도우미 등입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-124">The `ServerInfo` helper displays the current user identity, the type of browser that made the request, and so on.</span></span> <span data-ttu-id="43496-125">이러한 종류의 정보는 일반적인 문제를 해결 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-125">This kind of information can help you troubleshoot common issues.</span></span>

1. <span data-ttu-id="43496-126">라는 새 웹 페이지 생성 *ServerInfo.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-126">Create a new web page named *ServerInfo.cshtml*.</span></span>
2. <span data-ttu-id="43496-127">페이지의 끝 바로 앞에 닫는 `</body>` 태그, 추가 `@ServerInfo.GetHtml()`:</span><span class="sxs-lookup"><span data-stu-id="43496-127">At the end of the page, just before the closing `</body>` tag, add `@ServerInfo.GetHtml()`:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    <span data-ttu-id="43496-128">추가할 수는 `ServerInfo` 페이지의 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-128">You can add the `ServerInfo` code anywhere in the page.</span></span> <span data-ttu-id="43496-129">하지만 끝에 추가 됩니다 출력 별도로 유지 하면 다른 페이지 콘텐츠를 보다 쉽게 읽을 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="43496-129">But adding it at the end will keep its output separate from your other page content, which makes it easier to read.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="43496-130">**중요 한** 프로덕션 서버에 웹 페이지를 이동 하기 전에 웹 페이지에서 모든 진단 코드를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-130">**Important** You should remove any diagnostic code from your web pages before you move web pages to a production server.</span></span> <span data-ttu-id="43496-131">이에 적용 됩니다는 `ServerInfo` 으로 도우미는 다른 진단 기술이이 문서에서 코드 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-131">This applies to the `ServerInfo` helper as well as the other diagnostic techniques in this article that involve adding code to a page.</span></span> <span data-ttu-id="43496-132">이러한 종류의 정보를 악의적인 의도로 사람들에 게 유용한 될 수 있으므로 서버 및 비슷한 세부 정보에 서버 이름, 사용자 이름, 경로 대 한 정보를 참조 하 여 웹 사이트 방문자를 되기를 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-132">You don't want your website visitors to see information about your server name, user names, paths on your server, and similar details, because this type of information might be useful to people with malicious intent.</span></span>
3. <span data-ttu-id="43496-133">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-133">Save the page and run it in a browser.</span></span>

    ![디버깅-1](introduction-to-debugging/_static/image1.jpg)

    <span data-ttu-id="43496-135">`ServerInfo` 도우미 페이지에 4 개의 테이블의 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-135">The `ServerInfo` helper displays four tables of information in the page:</span></span>

   - <span data-ttu-id="43496-136">서버 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-136">Server Configuration.</span></span> <span data-ttu-id="43496-137">이 섹션에서는 호스팅 웹 서버 컴퓨터 이름, 버전을 실행 하는 ASP.NET, 도메인 이름 및 서버 시간을 포함 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-137">This section provides information about the hosting web server, including computer name, the version of ASP.NET you're running, the domain name, and server time.</span></span>
   - <span data-ttu-id="43496-138">ASP.NET 서버 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-138">ASP.NET Server Variables.</span></span> <span data-ttu-id="43496-139">이 섹션의 많은 HTTP 프로토콜 세부 정보 (호출된 HTTP 변수)에 대 한 세부 정보를 제공 하 고 있는 값이 각 웹 페이지 요청에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43496-139">This section provides details about the many HTTP protocol details (called HTTP variables) and values that are part of each web page request.</span></span>
   - <span data-ttu-id="43496-140">HTTP 런타임 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-140">HTTP Runtime Information.</span></span> <span data-ttu-id="43496-141">이 섹션에서는의 웹 페이지에서 실행 되는 Microsoft.NET Framework, 경로, 캐시, 등에 대 한 세부 정보 버전에 대해서는 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-141">This section provides details about that the version of the Microsoft .NET Framework that your web page is running under, the path, details about the cache, and so on.</span></span> <span data-ttu-id="43496-142">(에서 살펴본 것 처럼 [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890), ASP.NET 웹 페이지 Razor 구문을 기반으로 하는 광범위 한 소프트웨어는 Microsoft의 ASP.NET 웹 서버 기술, 기반을 사용 하 여 개발 라이브러리는.NET Framework를 호출 합니다.)</span><span class="sxs-lookup"><span data-stu-id="43496-142">(As you learned in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890), ASP.NET Web Pages using the Razor syntax are built on Microsoft's ASP.NET web server technology, which is itself built on an extensive software development library called the .NET Framework.)</span></span>
   - <span data-ttu-id="43496-143">환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-143">Environment Variables.</span></span> <span data-ttu-id="43496-144">이 섹션에서는 웹 서버의 모든 로컬 환경 변수 및 값의 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-144">This section provides a list of all the local environment variables and their values on the web server.</span></span>

     <span data-ttu-id="43496-145">모든 서버 및 요청 정보에 대 한 전체 설명은이 문서의 범위를 벗어납니다. 하지만 함을 확인할 수 있습니다는 `ServerInfo` 도우미 많은 진단 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-145">A full description of all the server and request information is beyond the scope of this article, but you can see that the `ServerInfo` helper returns a lot of diagnostic information.</span></span> <span data-ttu-id="43496-146">값에 대 한 자세한 내용은 하는 `ServerInfo` 반환 참조 [인식 환경 변수](https://technet.microsoft.com/library/dd560744(WS.10).aspx) Microsoft TechNet 웹 사이트 및 [IIS 서버 변수](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) MSDN 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-146">For more information about the values that `ServerInfo` returns, see [Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) on the Microsoft TechNet website and [IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) on the MSDN website.</span></span>

## <a name="embedding-output-expressions-to-display-page-values"></a><span data-ttu-id="43496-147">포함 출력 식 페이지 값을 표시 하려면</span><span class="sxs-lookup"><span data-stu-id="43496-147">Embedding Output Expressions to Display Page Values</span></span>

<span data-ttu-id="43496-148">다른 코드에서 관찰할 방법은 출력 식의 페이지에 포함 하려면입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-148">Another way to see what's happening in your code is to embed output expressions in the page.</span></span> <span data-ttu-id="43496-149">다음과 같이 추가 하 여 변수 값을 출력할 직접 수 아시다시피, `@myVariable` 또는 `@(subTotal * 12)` 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-149">As you know, you can directly output the value of a variable by adding something like `@myVariable` or `@(subTotal * 12)` to the page.</span></span> <span data-ttu-id="43496-150">코드에서 디버깅을 위해 중요 한 지점에 해당 출력 식을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-150">For debugging, you can place these output expressions at strategic points in your code.</span></span> <span data-ttu-id="43496-151">이 페이지에 실행 될 때 키 변수나 계산의 결과 값을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-151">This enables you to see the value of key variables or the result of calculations when your page runs.</span></span> <span data-ttu-id="43496-152">완료 하면 식 제거 하거나 주석 처리를 하 수 있습니다, 디버깅 합니다. 이 프로시저는 페이지를 디버깅 하는 데 포함된 식을 사용 하는 일반적인 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43496-152">When you're done debugging, you can remove the expressions or comment them out. This procedure illustrates a typical way to use embedded expressions to help debug a page.</span></span>

1. <span data-ttu-id="43496-153">라는 새로운 WebMatrix 페이지 생성 *OutputExpression.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-153">Create a new WebMatrix page that's named *OutputExpression.cshtml*.</span></span>
2. <span data-ttu-id="43496-154">페이지를 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="43496-154">Replace the page content with the following:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    <span data-ttu-id="43496-155">이 예제에서는 사용는 `switch` 문을의 값을 확인 하는 `weekday` 변수와 것이 어떤 요일에 따라 서로 다른 출력 메시지는 다음 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-155">The example uses a `switch` statement to check the value of the `weekday` variable and then display a different output message depending on which day of the week it is.</span></span> <span data-ttu-id="43496-156">예제에서는 `if` 블록 첫 번째 코드 블록 내에서 현재 평일 값을 1 일을 추가 하 여 요일을 차례로 임의로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-156">In the example, the `if` block within the first code block arbitrarily changes the day of the week by adding one day to the current weekday value.</span></span> <span data-ttu-id="43496-157">이해를 돕기 위해 도입 하는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-157">This is an error introduced for illustration purposes.</span></span>
3. <span data-ttu-id="43496-158">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-158">Save the page and run it in a browser.</span></span>

    <span data-ttu-id="43496-159">잘못 된 요일에 대 한 페이지에는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43496-159">The page displays the message for the wrong day of the week.</span></span> <span data-ttu-id="43496-160">모든 요일 실제로 이면 하루 나중에 대 한 메시지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43496-160">Whatever day of the week it actually is, you'll see the message for one day later.</span></span> <span data-ttu-id="43496-161">(코드는 의도적으로 잘못 된 날짜 값을 설정) 이므로 메시지 해제는 이유를 알고이 경우에 있지만, 실제로 종종 어렵습니다 작업 코드에 잘못 된 것 이며 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-161">Although in this case you know why the message is off (because the code deliberately sets the incorrect day value), in reality it's often hard to know where things are going wrong in the code.</span></span> <span data-ttu-id="43496-162">상황의 주요 개체 및 변수 값에 같은 찾아야 할를 디버깅 하려면 `weekday`합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-162">To debug, you need to find out what's happening to the value of key objects and variables such as `weekday`.</span></span>
4. <span data-ttu-id="43496-163">삽입 하 여 출력 식을 추가 하 여 `@weekday` 코드에서 주석으로 표시 된 두 위치에 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-163">Add output expressions by inserting `@weekday` as shown in the two places indicated by comments in the code.</span></span> <span data-ttu-id="43496-164">이러한 출력 식 코드 실행에서 해당 지점에서 변수의 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43496-164">These output expressions will display the values of the variable at that point in the code execution.</span></span>

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. <span data-ttu-id="43496-165">저장 하 고 브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-165">Save and run the page in a browser.</span></span>

    <span data-ttu-id="43496-166">페이지 실제 요일을 먼저 표시 한 다음 1 일, 및에서 결과 메시지 추가에서 발생 하는 업데이트 된 요일은 `switch` 문.</span><span class="sxs-lookup"><span data-stu-id="43496-166">The page displays the real day of the week first, then the updated day of the week that results from adding one day, and then the resulting message from the `switch` statement.</span></span> <span data-ttu-id="43496-167">두 변수 식에서 출력 (`@weekday`)에 HTML을 추가 하지 않은 때문에 날짜 사이 공백이 없어야 `<p>` 태그를 출력; 식이란 테스트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-167">The output from the two variable expressions (`@weekday`) has no spaces between the days because you didn't add any HTML `<p>` tags to the output; the expressions are just for testing.</span></span>

    ![디버깅-2](introduction-to-debugging/_static/image2.jpg)

    <span data-ttu-id="43496-169">이제 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-169">Now you can see where the error is.</span></span> <span data-ttu-id="43496-170">처음 표시 하면는 `weekday` 올바른 날짜 표시는 코드에서 변수를 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-170">When you first display the `weekday` variable in the code, it shows the correct day.</span></span> <span data-ttu-id="43496-171">표시 하면이 두 번째 시간 후의 `if` 코드에서 블록을 하루 하나으로 해제 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-171">When you display it the second time, after the `if` block in the code, the day is off by one.</span></span> <span data-ttu-id="43496-172">따라서 평일 변수의 첫 번째 및 두 번째 모양 간에 발생 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-172">So you know that something has happened between the first and second appearance of the weekday variable.</span></span> <span data-ttu-id="43496-173">실제 버그를 인 경우 이러한 종류의 접근 방식에서 문제가 발생 하는 코드의 위치를 파악할 도움이 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-173">If this were a real bug, this kind of approach would help you narrow down the location of the code that's causing the problem.</span></span>
6. <span data-ttu-id="43496-174">두 개의 출력 식 추가, 제거 및 해당 주의 일을 변경 하는 코드를 제거 하 여 페이지에서 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-174">Fix the code in the page by removing the two output expressions you added, and removing the code that changes the day of the week.</span></span> <span data-ttu-id="43496-175">다음 예제와 같이 코드의 나머지, 전체 블록:</span><span class="sxs-lookup"><span data-stu-id="43496-175">The remaining, complete block of code looks like the following example:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. <span data-ttu-id="43496-176">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-176">Run the page in a browser.</span></span> <span data-ttu-id="43496-177">이 시간 실제 요일에 대해 표시 하는 올바른 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43496-177">This time you see the correct message displayed for the actual day of the week.</span></span>

## <a name="using-the-objectinfo-helper-to-display-object-values"></a><span data-ttu-id="43496-178">ObjectInfo 도우미를 사용 하 여 개체 값을 표시 하려면</span><span class="sxs-lookup"><span data-stu-id="43496-178">Using the ObjectInfo Helper to Display Object Values</span></span>

<span data-ttu-id="43496-179">`ObjectInfo` 도우미 유형과 전달한 각 개체의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-179">The `ObjectInfo` helper displays the type and the value of each object you pass to it.</span></span> <span data-ttu-id="43496-180">(했던 것 처럼 위 예제의 출력 식을 사용 하 여) 코드에서 변수 및 개체의 값을 보는 데 사용할 수 있습니다 및 데이터 형식 개체에 대 한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-180">You can use it to view the value of variables and objects in your code (like you did with output expressions in the previous example), plus you can see data type information about the object.</span></span>

1. <span data-ttu-id="43496-181">명명 된 파일을 열고 *OutputExpression.cshtml* 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-181">Open the file named *OutputExpression.cshtml* that you created earlier.</span></span>
2. <span data-ttu-id="43496-182">다음 코드 블록을 페이지의 모든 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="43496-182">Replace all code in the page with the following block of code:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. <span data-ttu-id="43496-183">저장 하 고 브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-183">Save and run the page in a browser.</span></span>

    ![디버깅-4](introduction-to-debugging/_static/image3.jpg)

    <span data-ttu-id="43496-185">이 예제는 `ObjectInfo` 도우미에는 두 개의 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43496-185">In this example, the `ObjectInfo` helper displays two items:</span></span>

   - <span data-ttu-id="43496-186">형식입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-186">The type.</span></span> <span data-ttu-id="43496-187">첫 번째 형식은 `DayOfWeek`합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-187">For the first variable, the type is `DayOfWeek`.</span></span> <span data-ttu-id="43496-188">형식이 두 번째 변수의 `String`합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-188">For the second variable, the type is `String`.</span></span>
   - <span data-ttu-id="43496-189">값입니다.</span><span class="sxs-lookup"><span data-stu-id="43496-189">The value.</span></span> <span data-ttu-id="43496-190">이 경우 이미 페이지에서의 인사말 변수 값을 표시 하기 때문에 값이 다시 표시 변수를 전달 하는 경우 `ObjectInfo`합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-190">In this case, because you already display the value of the greeting variable in the page, the value is displayed again when you pass the variable to `ObjectInfo`.</span></span>

     <span data-ttu-id="43496-191">더 복잡 한 개체에 대 한는 `ObjectInfo` 도우미 자세한 정보를 표시할 수 &#8212; 기본적으로, 형식 및 값의 모든 개체의 속성을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-191">For more complex objects, the `ObjectInfo` helper can display more information &#8212; basically, it can display the types and values of all of an object's properties.</span></span>

## <a name="using-debugging-tools-in-visual-studio"></a><span data-ttu-id="43496-192">Visual Studio에서 디버깅 도구를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="43496-192">Using Debugging Tools in Visual Studio</span></span>

<span data-ttu-id="43496-193">보다 포괄적인 디버깅 환경을 사용 하 여 Visual Studio 2013 또는 무료 [Visual Studio Express 2013 for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express)합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-193">For a more comprehensive debugging experience, use Visual Studio 2013 or the free [Visual Studio Express 2013 for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express).</span></span> <span data-ttu-id="43496-194">Visual Studio와 함께 줄을 검사 하려는 코드에 중단점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-194">With Visual Studio, you can set a breakpoint in your code at the line that you want to inspect.</span></span>

![설정 된 중단점](introduction-to-debugging/_static/image1.png)

<span data-ttu-id="43496-196">웹 사이트를 테스트할 때 코드 실행이 중단점에서 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-196">When you test the web site, the executing code halts at the breakpoint.</span></span>

![중단점에 도달](introduction-to-debugging/_static/image2.png)

<span data-ttu-id="43496-198">변수 및 단계별로 코드에서 줄의 현재 값을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43496-198">You can examine the current values of the variables, and step through the code line-by-line.</span></span>

![값 표시](introduction-to-debugging/_static/image3.png)

<span data-ttu-id="43496-200">ASP.NET Razor 페이지를 디버깅 하려면 Visual Studio에서 통합 된 디버거를 사용 하는 방법에 대 한 정보를 참조 하십시오. [프로그래밍 ASP.NET 웹 페이지 (Razor)를 사용 하 여 Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854)합니다.</span><span class="sxs-lookup"><span data-stu-id="43496-200">For information about using the integrated debugger in Visual Studio to debug ASP.NET Razor pages, see [Programming ASP.NET Web Pages (Razor) Using Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43496-201">추가 자료</span><span class="sxs-lookup"><span data-stu-id="43496-201">Additional Resources</span></span>

- [<span data-ttu-id="43496-202">Visual Studio를 사용 하 여 ASP.NET 웹 페이지 (Razor) 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="43496-202">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?LinkId=205854)
- <span data-ttu-id="43496-203">[IIS 서버 변수](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="43496-203">[IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)</span></span>
- <span data-ttu-id="43496-204">[환경 변수를 인식](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)</span><span class="sxs-lookup"><span data-stu-id="43496-204">[Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)</span></span>
