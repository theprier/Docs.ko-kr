---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN 시작 클래스 검색 | Microsoft Docs
author: Praburaj
description: 이 자습서에는 OWIN 시작 클래스는 로드를 구성 하는 방법을 보여 줍니다. OWIN에 대 한 자세한 내용은 참조는 프로젝트 Katana 개요. 이 자습서를 하는 중...
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: 4e753187f1caae646402712c2abc28856ae71a79
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910709"
---
<a name="owin-startup-class-detection"></a><span data-ttu-id="6300f-105">OWIN 시작 클래스 검색</span><span class="sxs-lookup"><span data-stu-id="6300f-105">OWIN Startup Class Detection</span></span>
====================
<span data-ttu-id="6300f-106">하 여 [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="6300f-106">by [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="6300f-107">이 자습서에는 OWIN 시작 클래스는 로드를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-107">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="6300f-108">OWIN에 대 한 자세한 내용은 참조 하세요. [는 프로젝트 Katana 개요](an-overview-of-project-katana.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-108">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="6300f-109">Rick anderson이 자습서가 작성 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan 및 Howard Dierking ( [ @howard \_dierking](https://twitter.com/howard_dierking) ).</span><span class="sxs-lookup"><span data-stu-id="6300f-109">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="6300f-110">전제 조건</span><span class="sxs-lookup"><span data-stu-id="6300f-110">Prerequisites</span></span>
>
> [<span data-ttu-id="6300f-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6300f-111">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)


## <a name="owin-startup-class-detection"></a><span data-ttu-id="6300f-112">OWIN 시작 클래스 검색</span><span class="sxs-lookup"><span data-stu-id="6300f-112">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="6300f-113">모든 OWIN 응용 프로그램에 시작 클래스가 응용 프로그램 파이프라인에 대 한 구성 요소를 지정 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-113">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="6300f-114">여러 가지 방법으로 런타임에 startup 클래스를 연결할 수 있습니다, 호스팅 모델에 따라 있습니다 (OwinHost, IIS 및 IIS Express)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-114">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="6300f-115">이 자습서에 나와 있는 시작 클래스는 모든 호스팅 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-115">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="6300f-116">호스팅 런타임을 사용 하 여 다음 중 하나에 도달 startup 클래스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-116">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="6300f-117">**명명 규칙**: Katana 라는 클래스를 찾고 `Startup` 어셈블리 이름 또는 전역 네임 스페이스를 일치 하는 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-117">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="6300f-118">**OwinStartup 특성**:이 모드는 대부분의 개발자 startup 클래스를 지정 하는 데 걸리는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-118">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="6300f-119">다음 특성은으로 startup 클래스를 설정 합니다 `TestStartup` 클래스는 `StartupDemo` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-119">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="6300f-120">`OwinStartup` 특성 명명 규칙을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-120">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="6300f-121">이 특성을 사용 하 여 이름을 지정할 수도 있습니다, 있지만 이름을 사용 하도 사용 해야는 `appSetting` 구성 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-121">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="6300f-122">**구성 파일에서 appSetting 요소**: 합니다 `appSetting` 재정의 `OwinStartup` 특성 및 명명 규칙.</span><span class="sxs-lookup"><span data-stu-id="6300f-122">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="6300f-123">여러 시작 클래스를 할 수 있습니다 (사용 하 여 각는 `OwinStartup` 특성) 및 startup 클래스는 다음과 유사한 태그를 사용 하 여 구성 파일에서 로드할 구성:</span><span class="sxs-lookup"><span data-stu-id="6300f-123">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="6300f-124">또한 startup 클래스 및 어셈블리를 명시적으로 지정 하는 다음 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-124">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="6300f-125">구성 파일에 다음 XML의 친숙 한 시작 클래스 이름을 지정 `ProductionConfiguration`합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-125">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="6300f-126">위의 태그는 다음을 사용 하 여 사용 해야 합니다 `OwinStartup` 친숙 한 이름을 지정 하면 특성의 `ProductionStartup2` 클래스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-126">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="6300f-127">OWIN 시작 검색 추가 사용 하지 않도록 설정 합니다 `appSetting owin:AutomaticAppStartup` 값을 사용 하 여 `"false"` web.config 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-127">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="6300f-128">OWIN 시작을 사용 하 여 ASP.NET 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6300f-128">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="6300f-129">빈 Asp.Net 웹 응용 프로그램을 만들고 이름을 **StartupDemo**합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-129">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="6300f-130">-설치 `Microsoft.Owin.Host.SystemWeb` NuGet 패키지 관리자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-130">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="6300f-131">**도구** 메뉴에서 **NuGet 패키지 관리자**를 차례로 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-131">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="6300f-132">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-132">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="6300f-133">OWIN 시작 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-133">Add an OWIN startup class.</span></span> <span data-ttu-id="6300f-134">선택한 Visual Studio 2013에서 프로젝트를 클릭 마우스 오른쪽 단추로 **클래스 추가**합니다.-합니다 **새 항목 추가** 대화 상자에 입력 *OWIN* 검색 필드에 이름 Startup.cs로 변경 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-134">In Visual Studio 2013 right click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then click **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="6300f-135">추가 하려면 다음에 *Owin Startup 클래스*, 될에서 사용할 수 있는 합니다 **추가** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="6300f-135">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="6300f-136">또는 프로젝트를 마우스 오른쪽 단추로 클릭 수를 선택 **추가**을 선택한 후 **새 항목**를 선택한 후는 **Owin Startup 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-136">Alternatively, you can right click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="6300f-137">생성된 된 코드를 대체 합니다 *Startup.cs* 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="6300f-137">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="6300f-138">`app.Use` 람다 식은 OWIN 파이프라인에 지정 된 미들웨어 구성 요소를 등록 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-138">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="6300f-139">이 경우 들어오는 요청에 응답 하기 전에 들어오는 요청 로깅을 설정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-139">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="6300f-140">합니다 `next` 매개 변수는 대리자 ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [태스크](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) 파이프라인의 다음 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-140">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="6300f-141">`app.Run` 람다 식 들어오는 요청에 파이프라인 후크 및 응답 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-141">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="6300f-142">위의 코드에서 우리는 주석으로 처리를 `OwinStartup` 특성과 것 이라는 클래스를 실행 하는 규칙에 의존 하는 `Startup` 합니다.-키를 눌러 ***F5*** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-142">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="6300f-143">몇 번 새로 고침을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-143">Hit refresh a few times.</span></span>

    <span data-ttu-id="6300f-144">![](owin-startup-class-detection/_static/image4.png) 이 자습서에서는 이미지에 표시 된 숫자 참고: 참조 수가 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-144">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="6300f-145">밀리초 문자열 페이지를 새로 고칠 때 새 응답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-145">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="6300f-146">추적 정보를 볼 수는 **출력** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-146">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="6300f-147">자세한 시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="6300f-147">Add More Startup Classes</span></span>

<span data-ttu-id="6300f-148">이 단원의 다른 시작 클래스를 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-148">In this section we'll add another Startup class.</span></span> <span data-ttu-id="6300f-149">응용 프로그램에 여러 OWIN 시작 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-149">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="6300f-150">예를 들어, 다음 개발, 테스트 및 프로덕션에 대 한 시작 클래스를 만들 수는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-150">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="6300f-151">새 OWIN 시작 클래스를 만들고 이름을 `ProductionStartup`입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-151">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="6300f-152">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-152">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="6300f-153">컨트롤 F5 키를 눌러 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-153">Press Control F5 to run the app.</span></span> <span data-ttu-id="6300f-154">`OwinStartup` 프로덕션 startup 클래스를 실행 하는 특성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-154">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="6300f-155">다른 OWIN Startup 클래스를 만들고 이름을 `TestStartup`입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-155">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="6300f-156">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-156">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="6300f-157">합니다 `OwinStartup` 위의 특성 오버 로드는 지정 `TestingConfiguration` 으로 *친숙 한* Startup 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-157">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="6300f-158">열기는 *web.config* 파일과 Startup 클래스의 이름을 지정 하는 OWIN 앱 시작 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-158">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="6300f-159">컨트롤 F5 키를 눌러 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-159">Press Control F5 to run the app.</span></span> <span data-ttu-id="6300f-160">앱 설정 요소가 참조 하는 셀을 취하고 테스트 구성을 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-160">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="6300f-161">제거는 *친숙 한* 이름을 합니다 `OwinStartup` 특성을 `TestStartup` 클래스.</span><span class="sxs-lookup"><span data-stu-id="6300f-161">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="6300f-162">에 OWIN 앱 시작 키를 대체 합니다 *web.config* 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="6300f-162">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="6300f-163">되돌리기는 `OwinStartup` Visual Studio에서 생성 된 기본 특성 코드에 각 클래스에 있는 특성:</span><span class="sxs-lookup"><span data-stu-id="6300f-163">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="6300f-164">각 OWIN 앱 시작 키 아래 프로덕션 클래스를 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-164">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="6300f-165">마지막 시작 키 시작 구성 메서드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-165">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="6300f-166">다음 OWIN 앱 시작 키를 사용 하면 구성 클래스의 이름을 변경 하려면 `MyConfiguration` 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-166">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="6300f-167">Owinhost.exe를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6300f-167">Using Owinhost.exe</span></span>

1. <span data-ttu-id="6300f-168">다음 태그를 사용 하 여 Web.config 파일을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-168">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="6300f-169">이 경우이 마지막 키 wins `TestStartup` 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-169">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="6300f-170">PMC에서 Owinhost를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-170">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="6300f-171">응용 프로그램 폴더로 이동 (포함 된 폴더를 *Web.config* 파일) 및 명령 프롬프트 및 종류:</span><span class="sxs-lookup"><span data-stu-id="6300f-171">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="6300f-172">명령 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-172">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="6300f-173">URL로 브라우저 시작 `http://localhost:5000/`합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-173">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="6300f-174">OwinHost 위에 나열 된 시작 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-174">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="6300f-175">명령 창에서 enter 키를 눌러 OwinHost를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-175">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="6300f-176">에 `ProductionStartup` 클래스의 이름을 지정 하는 다음 OwinStartup 특성을 추가 합니다 *ProductionConfiguration*합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-176">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="6300f-177">명령 프롬프트 및 형식:</span><span class="sxs-lookup"><span data-stu-id="6300f-177">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="6300f-178">프로덕션 시작 클래스 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-178">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)
   <span data-ttu-id="6300f-179">응용 프로그램에 여러 시작 클래스 및이 예제에서는 시작 로드할 클래스를 런타임 시까지 지연 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-179">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="6300f-180">다음 런타임 시작 옵션을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6300f-180">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
