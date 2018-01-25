---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: "SignalR 응용 프로그램 유닛 테스트 | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 SignalR 2.0의 단위 테스트 기능을 사용 하는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: d767e1a9d27670387133e5a48a8f92f5bdd39d9e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="unit-testing-signalr-applications"></a><span data-ttu-id="b781a-103">단위 테스트 SignalR 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b781a-103">Unit Testing SignalR Applications</span></span>
====================
<span data-ttu-id="b781a-104">으로 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b781a-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="b781a-105">이 문서에서는 SignalR 2의 단위 테스트 기능을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-105">This article describes using the Unit Testing features of SignalR 2.</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="b781a-106">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="b781a-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="b781a-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b781a-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="b781a-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b781a-108">.NET 4.5</span></span>
> - <span data-ttu-id="b781a-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="b781a-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="b781a-110">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="b781a-110">Questions and comments</span></span>
> 
> <span data-ttu-id="b781a-111">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="b781a-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b781a-112">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="b781a-113">SignalR 응용 프로그램 유닛 테스트</span><span class="sxs-lookup"><span data-stu-id="b781a-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="b781a-114">SignalR 2에서 단위 테스트를 만드는 SignalR 응용 프로그램에 대 한 단위 테스트 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="b781a-115">SignalR 2에 포함 되어는 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 인터페이스를 테스트 하기 위한 허브 메서드를 시뮬레이션 하는 모의 개체를 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="b781a-116">이 섹션에서는 만든 응용 프로그램에 대 한 단위 테스트 추가 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 를 사용 하 여 [XUnit.net](https://github.com/xunit/xunit) 및 [Moq](https://github.com/Moq/moq4)합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="b781a-117">XUnit.net; 테스트를 제어 하는 데 사용 됩니다. Moq 만드는 데 사용할 됩니다는 [의 모의 알림](http://en.wikipedia.org/wiki/Mock_object) 테스트에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="b781a-118">원하는; 경우 다른 모의 프레임 워크를 사용할 수 있습니다. [NSubstitute](http://nsubstitute.github.io/) 도 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="b781a-119">이 자습서에서는 두 가지 방법으로 모의 개체를 설정 하는 방법을 설명: 사용 하 여 먼저는 `dynamic` 개체 (.NET Framework 4에 도입 된) 및 인터페이스를 사용 하 여 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="b781a-120">목차</span><span class="sxs-lookup"><span data-stu-id="b781a-120">Contents</span></span>

<span data-ttu-id="b781a-121">이 자습서는 다음 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="b781a-122">동적을 사용한 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="b781a-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="b781a-123">단위 테스트 유형별로</span><span class="sxs-lookup"><span data-stu-id="b781a-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="b781a-124">동적을 사용한 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="b781a-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="b781a-125">이 섹션에서 만든 응용 프로그램에 대 한 단위 테스트를 추가 합니다는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 동적 개체를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="b781a-126">설치는 [XUnit Runner 확장](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) Visual Studio 2013 용입니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="b781a-127">완료 하거나는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md)에서 완성 된 응용 프로그램을 다운로드 하거나 [MSDN 코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="b781a-128">시작 응용 프로그램의 다운로드 버전이 사용 하는 경우 열 **패키지 관리자 콘솔** 클릭 **복원** SignalR 패키지 프로젝트를 추가 하려면.</span><span class="sxs-lookup"><span data-stu-id="b781a-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![패키지를 복원](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="b781a-130">단위 테스트에 대 한 솔루션에 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="b781a-131">솔루션을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **추가**, **새 프로젝트...** . 아래는 **C#** 노드를 선택는 **Windows** 노드.</span><span class="sxs-lookup"><span data-stu-id="b781a-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="b781a-132">선택 **클래스 라이브러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-132">Select **Class Library**.</span></span> <span data-ttu-id="b781a-133">새 프로젝트의 이름을 **TestLibrary** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![테스트 라이브러리 만들기](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="b781a-135">SignalRChat 프로젝트에 테스트 라이브러리 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="b781a-136">마우스 오른쪽 단추로 클릭는 **TestLibrary** 프로젝트를 마우스 선택 **추가**, **참조 중...** . 선택 된 **프로젝트** 노드 아래의 **솔루션** 노드와 검사 **SignalRChat**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="b781a-137">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-137">Click **OK**.</span></span>

    ![프로젝트 참조 추가](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="b781a-139">SignalR, Moq, 및 XUnit 패키지에 추가 된 **TestLibrary** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b781a-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="b781a-140">에 **패키지 관리자 콘솔**설정는 **기본 프로젝트** 드롭다운을 **TestLibrary**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="b781a-141">콘솔 창에 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-141">Run the following commands in the console window:</span></span>

    - `Install-Package Microsoft.AspNet.SignalR`
    - `Install-Package Moq`
    - `Install-Package XUnit`

    ![패키지 설치](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="b781a-143">테스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-143">Create the test file.</span></span> <span data-ttu-id="b781a-144">마우스 오른쪽 단추로 클릭는 **TestLibrary** 프로젝트 **추가 중...** , **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="b781a-145">클래스의 새 이름을 **Tests.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="b781a-146">Tests.cs의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="b781a-147">위의 코드에서 테스트 클라이언트 사용 하 여 만들어집니다는 `Mock` 에서 개체는 [Moq](https://github.com/Moq/moq4) 형식의 라이브러리 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (SignalR 2.1에서 할당 `dynamic` 유형에 대 한 매개 변수입니다.) `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 프록시 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="b781a-148">`broadcastMessage` 함수는 다음에 대해 정의 된 모의 클라이언트에서 호출할 수 있도록는 `ChatHub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="b781a-149">테스트 엔진에서 호출 된 `Send` 의 메서드는 `ChatHub` 호출 하는 모의 클래스 `broadcastMessage` 함수.</span><span class="sxs-lookup"><span data-stu-id="b781a-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="b781a-150">키를 눌러 솔루션을 빌드합니다 **F6**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="b781a-151">단위 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-151">Run the unit test.</span></span> <span data-ttu-id="b781a-152">Visual Studio에서 선택 **테스트**, **Windows**, **테스트 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="b781a-153">테스트 탐색기 창에서 마우스 오른쪽 단추로 클릭 **HubsAreMockableViaDynamic** 선택 **선택 된 테스트 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="b781a-155">테스트 탐색기 창의 아래쪽 창 확인 하 여 테스트에 통과 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="b781a-156">창에서 테스트를 통과 했음이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-156">The window will show that the test passed.</span></span>

    ![테스트 통과](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="b781a-158">단위 테스트 유형별로</span><span class="sxs-lookup"><span data-stu-id="b781a-158">Unit testing by type</span></span>

<span data-ttu-id="b781a-159">이 섹션에서 만든 응용 프로그램에 대 한 테스트를 추가 합니다는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 테스트할 메서드를 포함 하는 인터페이스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="b781a-160">1-7 단계에서 완료 된 [동적을 사용한 단위 테스트](#dynamic) 위의 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="b781a-161">Tests.cs의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="b781a-162">위의 코드에서 인터페이스의 서명을 정의 생성 됩니다는 `broadcastMessage` 메서드 테스트 엔진에서는 모의 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="b781a-163">모의 클라이언트를 사용 하 여 만들고 그런 다음는 `Mock` 형식의 개체 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (SignalR 2.1에서 할당 `dynamic` 형식 매개 변수.) `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 프록시 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="b781a-164">테스트의 인스턴스를 만든 후 `ChatHub`, 다음의 모의 버전을 만듭니다는 `broadcastMessage` 메서드를 호출 하 여 호출 되는 `Send` 허브에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="b781a-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="b781a-165">키를 눌러 솔루션을 빌드합니다 **F6**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="b781a-166">단위 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-166">Run the unit test.</span></span> <span data-ttu-id="b781a-167">Visual Studio에서 선택 **테스트**, **Windows**, **테스트 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="b781a-168">테스트 탐색기 창에서 마우스 오른쪽 단추로 클릭 **HubsAreMockableViaDynamic** 선택 **선택 된 테스트 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="b781a-170">테스트 탐색기 창의 아래쪽 창 확인 하 여 테스트에 통과 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="b781a-171">창에서 테스트를 통과 했음이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b781a-171">The window will show that the test passed.</span></span>

    ![테스트 통과](unit-testing-signalr-applications/_static/image8.png)
