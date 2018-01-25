---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: "OData v4 클라이언트 앱 (C#) 만들기 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2014
ms.topic: article
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: 51a3c7b9c5b6525d6d82b9a45910f58b71268b7f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="7e722-102">OData v4 클라이언트 앱 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="7e722-102">Create an OData v4 Client App (C#)</span></span>
====================
<span data-ttu-id="7e722-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7e722-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7e722-104">이전 자습서에서 CRUD 작업을 지 원하는 기본 OData 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="7e722-105">이제 서비스에 대 한 클라이언트를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="7e722-106">Visual Studio의 새 인스턴스를 시작 하 고 새 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="7e722-107">에 **새 프로젝트** 대화 상자에서 **설치 됨** &gt; **템플릿** &gt; **Visual C#** &gt; **Windows 바탕 화면**, 선택는 **콘솔 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="7e722-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="7e722-108">프로젝트 이름을 &quot;ProductsApp&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="7e722-109">OData 서비스가 포함 된 Visual Studio 솔루션에 콘솔 응용 프로그램을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>


## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="7e722-110">OData 클라이언트 코드 생성기를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="7e722-111">**도구** 메뉴 선택 **확장명 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="7e722-112">선택 **온라인** &gt; **Visual Studio 갤러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="7e722-113">검색 상자에 검색 &quot;OData 클라이언트 코드 생성기&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="7e722-114">클릭 **다운로드** VSIX를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="7e722-115">Visual Studio를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="7e722-116">OData 서비스를 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="7e722-116">Run the OData Service Locally</span></span>

<span data-ttu-id="7e722-117">Visual Studio에서 ProductService 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="7e722-118">기본적으로 Visual Studio 응용 프로그램 루트에 대 한 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="7e722-119">참고 URI입니다. 다음 단계에서이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="7e722-120">응용 프로그램을 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="7e722-121">동일한 솔루션의 두 프로젝트를 설정 하는 경우에 디버깅 하지 않고 ProductService 프로젝트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="7e722-122">다음 단계에서 콘솔 응용 프로그램 프로젝트를 수정 하는 동안 실행 되는 서비스를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>


## <a name="generate-the-service-proxy"></a><span data-ttu-id="7e722-123">서비스 프록시를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-123">Generate the Service Proxy</span></span>

<span data-ttu-id="7e722-124">서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는.NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="7e722-125">프록시는 HTTP 요청에 대 한 메서드 호출으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="7e722-126">실행 하 여 프록시 클래스를 만듭니다는 [T4 템플릿](https://msdn.microsoft.com/library/bb126445.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="7e722-127">프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-127">Right-click the project.</span></span> <span data-ttu-id="7e722-128">선택 **추가** &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="7e722-129">에 **새 항목 추가** 대화 상자에서 **Visual C# 항목** &gt; **코드** &gt; **OData 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="7e722-130">템플릿에 이름을 &quot;ProductClient.tt&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="7e722-131">클릭 **추가** 보안 경고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="7e722-132">이 시점에서 무시할 수 있는 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="7e722-133">Visual Studio는 자동으로 서식 파일을 실행 하지만 서식 파일에 일부 구성 설정이 필요한 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="7e722-134">ProductClient.odata.config 파일을 엽니다. 에 `Parameter` 요소인 ProductService 프로젝트 (이전 단계)에서 URI에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="7e722-135">예:</span><span class="sxs-lookup"><span data-stu-id="7e722-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="7e722-136">서식 파일을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-136">Run the template again.</span></span> <span data-ttu-id="7e722-137">솔루션 탐색기에서 ProductClient.tt 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **사용자 지정 도구 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="7e722-138">템플릿은 라는 ProductClient.cs 프록시를 정의 하는 코드 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="7e722-139">OData 끝점을 변경 하면 응용 프로그램을 개발 하는 경우 프록시 업데이트 서식 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="7e722-140">OData 서비스를 호출 하 여 서비스 프록시를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7e722-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="7e722-141">Program.cs 파일을 열고 상용구 코드를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="7e722-142">값을 바꿉니다 *serviceUri* 앞에서 서비스 URI와 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="7e722-143">응용 프로그램을 실행 하면 다음 출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e722-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
