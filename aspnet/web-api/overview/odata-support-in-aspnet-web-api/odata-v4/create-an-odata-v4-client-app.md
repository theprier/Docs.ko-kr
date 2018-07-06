---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: OData v4 클라이언트 앱 (C#) 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: 1e621988b43b4f012f113d7a52250879da56bb1c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818678"
---
<a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="b974f-102">OData v4 클라이언트 앱 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="b974f-102">Create an OData v4 Client App (C#)</span></span>
====================
<span data-ttu-id="b974f-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b974f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b974f-104">이전 자습서에서 CRUD 작업을 지 원하는 기본 OData 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="b974f-105">이제 서비스에 대 한 클라이언트를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="b974f-106">Visual Studio의 새 인스턴스를 시작 하 고 새 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="b974f-107">에 **새 프로젝트** 대화 상자에서 **설치 됨** &gt; **템플릿** &gt; **Visual C#** &gt; **Windows 데스크톱**를 선택 합니다 **콘솔 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="b974f-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="b974f-108">프로젝트 이름을 &quot;ProductsApp&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="b974f-109">또한 OData 서비스를 포함 하는 동일한 Visual Studio 솔루션에 콘솔 앱을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>


## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="b974f-110">OData 클라이언트 코드 생성기를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="b974f-111">**도구** 메뉴에서 **확장 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="b974f-112">선택 **Online** &gt; **Visual Studio 갤러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="b974f-113">검색 상자에서 검색할 &quot;OData 클라이언트 코드 생성기&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="b974f-114">클릭 **다운로드** VSIX를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="b974f-115">Visual Studio를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="b974f-116">OData 서비스를 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="b974f-116">Run the OData Service Locally</span></span>

<span data-ttu-id="b974f-117">Visual Studio에서 ProductService 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="b974f-118">기본적으로 Visual Studio가 응용 프로그램 루트에 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="b974f-119">URI; 참고 다음 단계에서 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="b974f-120">응용 프로그램을 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="b974f-121">동일한 솔루션에 두 프로젝트를 배치 하면 디버깅 하지 않고 ProductService 프로젝트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="b974f-122">다음 단계에서는 콘솔 응용 프로그램 프로젝트를 수정 하는 동안 실행 되는 서비스를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>


## <a name="generate-the-service-proxy"></a><span data-ttu-id="b974f-123">서비스 프록시를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-123">Generate the Service Proxy</span></span>

<span data-ttu-id="b974f-124">서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는.NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="b974f-125">프록시는 HTTP 요청에 대 한 메서드 호출으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="b974f-126">실행 하 여 프록시 클래스를 만듭니다는 [T4 템플릿](https://msdn.microsoft.com/library/bb126445.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="b974f-127">프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-127">Right-click the project.</span></span> <span data-ttu-id="b974f-128">선택 **추가할** &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="b974f-129">에 **새 항목 추가** 대화 상자에서 **Visual C# 항목** &gt; **코드** &gt; **OData 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="b974f-130">템플릿에 이름을 &quot;ProductClient.tt&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="b974f-131">클릭 **추가** 및 보안 경고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="b974f-132">이 시점에서 무시할 수 있는 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="b974f-133">Visual Studio에서 템플릿을 자동으로 실행 되었지만 템플릿의 일부 구성 설정은 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="b974f-134">ProductClient.odata.config 파일을 엽니다. 에 `Parameter` 요소인 ProductService 프로젝트 (이전 단계)에서 URI에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="b974f-135">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="b974f-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="b974f-136">템플릿을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-136">Run the template again.</span></span> <span data-ttu-id="b974f-137">솔루션 탐색기에서 ProductClient.tt 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **사용자 지정 도구 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="b974f-138">템플릿은은 ProductClient.cs 프록시를 정의 하는 명명 된 코드 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="b974f-139">OData 끝점을 변경 하는 경우 앱을 개발 하는 경우 프록시를 업데이트 하도록 다시 템플릿을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="b974f-140">서비스 프록시를 사용 하 여 OData 서비스를 호출 하려면</span><span class="sxs-lookup"><span data-stu-id="b974f-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="b974f-141">Program.cs 파일을 열고 상용구 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="b974f-142">값을 바꿉니다 *serviceUri* 앞에서 서비스 URI 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="b974f-143">앱을 실행 하는 경우 다음 출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b974f-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
