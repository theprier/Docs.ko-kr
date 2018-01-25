---
uid: web-api/overview/older-versions/self-host-a-web-api
title: "자체 호스트 하는 ASP.NET Web API 1 (C#) | Microsoft Docs"
author: MikeWasson
description: "ASP.NET Web API IIS가 필요 하지 않습니다. 호스트 프로세스에 고유한 web API를 자체 호스트할 수 있습니다. 이 자습서에서는 applic 콘솔 내 웹 API를 호스트 하는 방법을 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2012
ms.topic: article
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 564f859e73a88ac9c5f27e9b8f7409ec126642f8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="b64b2-105">자체 호스트 하는 ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="b64b2-105">Self-Host ASP.NET Web API 1 (C#)</span></span>
====================
<span data-ttu-id="b64b2-106">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b64b2-106">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b64b2-107">ASP.NET Web API IIS가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-107">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="b64b2-108">호스트 프로세스에 고유한 web API를 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-108">You can self-host a web API in your own host process.</span></span> <span data-ttu-id="b64b2-109">이 자습서에는 콘솔 응용 프로그램 내 웹 API를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-109">This tutorial shows how to host a web API inside a console application.</span></span>
> 
> <span data-ttu-id="b64b2-110">**새 응용 프로그램은 OWIN 자체 호스트 하는 Web API를 사용 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b64b2-110">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="b64b2-111">참조 [OWIN를 사용 하 여 자체 호스트 하는 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-111">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b64b2-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="b64b2-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b64b2-113">Web API 1</span><span class="sxs-lookup"><span data-stu-id="b64b2-113">Web API 1</span></span>
> - <span data-ttu-id="b64b2-114">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="b64b2-114">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="b64b2-115">콘솔 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b64b2-115">Create the Console Application Project</span></span>

<span data-ttu-id="b64b2-116">Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 **시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b64b2-116">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="b64b2-117">또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-117">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="b64b2-118">에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="b64b2-118">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="b64b2-119">아래 **Visual C#**선택, **Windows**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-119">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="b64b2-120">프로젝트 템플릿 목록에서 선택 **콘솔 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-120">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="b64b2-121">프로젝트 이름을 &quot;SelfHost&quot; 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-121">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="b64b2-122">대상 프레임 워크 (Visual Studio 2010) 설정</span><span class="sxs-lookup"><span data-stu-id="b64b2-122">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="b64b2-123">Visual Studio 2010을 사용 하는 경우.NET Framework 4.0 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-123">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="b64b2-124">(기본적으로 프로젝트 템플릿의 대상은 [.NET Framework 클라이언트 프로필](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="b64b2-124">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="b64b2-125">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-125">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="b64b2-126">에 **대상 프레임 워크** 드롭다운 목록에서.NET Framework 4.0 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-126">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="b64b2-127">를 변경 내용을 적용 하 라는 메시지가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-127">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="b64b2-128">NuGet 패키지 관리자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-128">Install NuGet Package Manager</span></span>

<span data-ttu-id="b64b2-129">NuGet 패키지 관리자는 가장 쉬운 방법 비 ASP.NET 프로젝트에 웹 API 어셈블리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-129">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="b64b2-130">NuGet 패키지 관리자가 설치 되어 있는지를 확인 하려면 클릭는 **도구** Visual Studio에서 메뉴.</span><span class="sxs-lookup"><span data-stu-id="b64b2-130">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="b64b2-131">실행 표시 되 면 **라이브러리 패키지 관리자**, NuGet 패키지 관리자를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-131">If you see a menu item called **Library Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="b64b2-132">설치 하려면 NuGet 패키지 관리자:</span><span class="sxs-lookup"><span data-stu-id="b64b2-132">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="b64b2-133">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-133">Start Visual Studio.</span></span>
2. <span data-ttu-id="b64b2-134">**도구** 메뉴 선택 **확장명 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-134">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="b64b2-135">에 **확장명 및 업데이트** 대화 상자에서 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-135">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="b64b2-136">"NuGet 패키지 관리자" 보이지 않으면 검색 상자에 "nuget 패키지 관리자"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-136">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="b64b2-137">NuGet 패키지 관리자를 선택 하 고 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-137">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="b64b2-138">다운로드가 완료 된 후 설치 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-138">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="b64b2-139">설치가 완료 된 후 Visual Studio를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-139">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="b64b2-140">웹 API NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="b64b2-140">Add the Web API NuGet Package</span></span>

<span data-ttu-id="b64b2-141">NuGet 패키지 관리자를 설치한 후 웹 API Self-Host 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-141">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="b64b2-142">**도구** 메뉴 선택 **라이브러리 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-142">From the **Tools** menu, select **Library Package Manager**.</span></span> <span data-ttu-id="b64b2-143">*참고*: 경우 하면이 메뉴가 표시 되지 않으면이 항목에서 해당 NuGet 패키지 관리자를 제대로 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-143">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="b64b2-144">선택 **솔루션용 NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="b64b2-144">Select **Manage NuGet Packages for Solution...**</span></span>
3. <span data-ttu-id="b64b2-145">에 **덩어리 패키지 관리** 대화 상자에서 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-145">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="b64b2-146">검색 상자에 입력 &quot;Microsoft.AspNet.WebApi.SelfHost&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-146">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="b64b2-147">ASP.NET Web API Self Host 패키지를 선택 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-147">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="b64b2-148">패키지 설치 된 후 클릭 **닫습니다** 는 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-148">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="b64b2-149">Microsoft.AspNet.WebApi.SelfHost, 하지 AspNetWebApi.SelfHost 라는 패키지를 설치할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-149">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>


![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="b64b2-150">모델과 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="b64b2-150">Create the Model and Controller</span></span>

<span data-ttu-id="b64b2-151">이 자습서로 동일한 모델 및 컨트롤러 클래스를 사용 하 여 [시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-151">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="b64b2-152">공용 클래스를 추가 `Product`합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-152">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="b64b2-153">공용 클래스를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-153">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="b64b2-154">이 클래스를 파생 **System.Web.Http.ApiController**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-154">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="b64b2-155">이 컨트롤러에 코드에 대 한 자세한 내용은 참조는 [시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-155">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="b64b2-156">이 컨트롤러는 세 가지 GET 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-156">This controller defines three GET actions:</span></span>

| <span data-ttu-id="b64b2-157">URI</span><span class="sxs-lookup"><span data-stu-id="b64b2-157">URI</span></span> | <span data-ttu-id="b64b2-158">설명</span><span class="sxs-lookup"><span data-stu-id="b64b2-158">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b64b2-159">/ api/제품</span><span class="sxs-lookup"><span data-stu-id="b64b2-159">/api/products</span></span> | <span data-ttu-id="b64b2-160">모든 제품의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-160">Get a list of all products.</span></span> |
| <span data-ttu-id="b64b2-161">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b64b2-161">/api/products/*id*</span></span> | <span data-ttu-id="b64b2-162">제품 id 가져오기</span><span class="sxs-lookup"><span data-stu-id="b64b2-162">Get a product by ID.</span></span> |
| <span data-ttu-id="b64b2-163">/api/products/?category=*category*</span><span class="sxs-lookup"><span data-stu-id="b64b2-163">/api/products/?category=*category*</span></span> | <span data-ttu-id="b64b2-164">범주별으로 제품의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-164">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="b64b2-165">Web API를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-165">Host the Web API</span></span>

<span data-ttu-id="b64b2-166">Program.cs 파일을 열고 다음을 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b64b2-166">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="b64b2-167">다음 코드를 추가 하는 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-167">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="b64b2-168">(선택 사항) HTTP URL Namespace 예약을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-168">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="b64b2-169">이 응용 프로그램에서 수신 하 `http://localhost:8080/`합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-169">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="b64b2-170">기본적으로 특정 HTTP 주소에서 수신 대기 하려면 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-170">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="b64b2-171">이 자습서를 실행 하면 따라서이 오류가 발생할 수 있습니다이: "HTTP URL http://+:8080/를 등록 하지 못했습니다" 두 가지 방법으로이 오류를 방지 하려면:</span><span class="sxs-lookup"><span data-stu-id="b64b2-171">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="b64b2-172">관리자 권한으로 Visual Studio를 실행 하거나</span><span class="sxs-lookup"><span data-stu-id="b64b2-172">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="b64b2-173">Netsh.exe를 사용 하 여 URL을 예약 하 고 사용자 계정 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-173">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="b64b2-174">Netsh.exe를 사용 하려면 관리자 권한으로 명령 프롬프트를 열고 다음 명령을: 다음 명령을 입력:</span><span class="sxs-lookup"><span data-stu-id="b64b2-174">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="b64b2-175">여기서 *machine\username과 같이* 는 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-175">where *machine\username* is your user account.</span></span>

<span data-ttu-id="b64b2-176">자체 호스팅을 완료 되 면 예약을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-176">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="b64b2-177">클라이언트 응용 프로그램 (C#)에서 Web API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-177">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="b64b2-178">Web API를 호출 하는 간단한 콘솔 응용 프로그램을 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-178">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="b64b2-179">새 콘솔 응용 프로그램 프로젝트를 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-179">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="b64b2-180">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로젝트 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-180">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="b64b2-181">라는 새 콘솔 응용 프로그램 만들기 &quot;ClientApp&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-181">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="b64b2-182">NuGet 패키지 관리자를 사용 하 여 ASP.NET Web API Core Libraries 패키지를 추가 하려면:</span><span class="sxs-lookup"><span data-stu-id="b64b2-182">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="b64b2-183">도구 메뉴에서 선택 **라이브러리 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-183">From the Tools menu, select **Library Package Manager**.</span></span>
- <span data-ttu-id="b64b2-184">선택 **솔루션용 NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="b64b2-184">Select **Manage NuGet Packages for Solution...**</span></span>
- <span data-ttu-id="b64b2-185">에 **NuGet 패키지 관리** 대화 상자에서 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-185">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="b64b2-186">검색 상자에 입력 &quot;Microsoft.AspNet.WebApi.Client&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-186">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="b64b2-187">Microsoft ASP.NET Web API Client Libraries 패키지를 선택 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-187">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="b64b2-188">ClientApp에 SelfHost 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-188">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="b64b2-189">솔루션 탐색기에서 ClientApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-189">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="b64b2-190">선택 **참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-190">Select **Add Reference**.</span></span>
- <span data-ttu-id="b64b2-191">에 **참조 관리자** 대화 아래 **솔루션**선택, **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-191">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="b64b2-192">SelfHost 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-192">Select the SelfHost project.</span></span>
- <span data-ttu-id="b64b2-193">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-193">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="b64b2-194">Client/Program.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-194">Open the Client/Program.cs file.</span></span> <span data-ttu-id="b64b2-195">다음 추가 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="b64b2-195">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="b64b2-196">정적 추가 **HttpClient** 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="b64b2-196">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="b64b2-197">모든 제품 ID로 제품 목록 및 목록 제품 범주별으로 나열 하려면 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-197">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="b64b2-198">이러한 각 방법의 동일한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-198">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="b64b2-199">호출 **HttpClient.GetAsync** 적합 한 URI에 GET 요청을 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-199">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="b64b2-200">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="b64b2-200">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="b64b2-201">이 메서드는 HTTP 응답 상태 오류 코드 이면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-201">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="b64b2-202">호출 **ReadAsAsync&lt;T&gt;**  를 HTTP 응답에서 CLR 형식을 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-202">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="b64b2-203">이 메서드는에 정의 된 확장 메서드를 **System.Net.Http.HttpContentExtensions**합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-203">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="b64b2-204">**GetAsync** 및 **ReadAsAsync** 메서드는 비동기 둘 다 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-204">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="b64b2-205">반환 **작업** 비동기 작업을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-205">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="b64b2-206">가져오기는 **결과** 속성은 작업이 완료 될 때까지 스레드를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-206">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="b64b2-207">비동기 호출을 수행 하는 방법을 비롯 한 HttpClient를 사용 하는 방법에 대 한 자세한 내용은 참조 [웹 API에서 정도.NET 클라이언트 호출](../advanced/calling-a-web-api-from-a-net-client.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-207">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="b64b2-208">이러한 메서드를 호출 하기 전에 BaseAddress를 설정 하도록 HttpClient 인스턴스에서 "`http://localhost:8080`"입니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-208">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="b64b2-209">예:</span><span class="sxs-lookup"><span data-stu-id="b64b2-209">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="b64b2-210">다음 출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b64b2-210">This should output the following.</span></span> <span data-ttu-id="b64b2-211">(SelfHost 응용 프로그램을 먼저 실행 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b64b2-211">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
