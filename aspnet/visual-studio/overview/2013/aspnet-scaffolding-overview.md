---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013에서 ASP.NET 스 캐 폴딩 | Microsoft Docs
author: tfitzmac
description: ASP.NET 스 캐 폴딩에는 Visual Studio 2013에 포함 된 새 기능입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/09/2014
ms.topic: article
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: f014ef1439376349f49f10f1f4063945ab81e7c1
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369094"
---
<a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="f3afb-103">Visual Studio 2013에서 ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="f3afb-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>
====================
<span data-ttu-id="f3afb-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f3afb-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f3afb-105">ASP.NET 스 캐 폴딩에는 Visual Studio 2013에 포함 된 새 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>


## <a name="overview"></a><span data-ttu-id="f3afb-106">개요</span><span class="sxs-lookup"><span data-stu-id="f3afb-106">Overview</span></span>

<span data-ttu-id="f3afb-107">ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="f3afb-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="f3afb-108">Visual Studio 2013 MVC 및 Web API 프로젝트에 대 한 사전 설치 된 코드 생성기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="f3afb-109">신속 하 게 데이터 모델과 상호 작용 하는 코드를 추가 하려는 경우 프로젝트에 스 캐 폴딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="f3afb-110">스 캐 폴딩을 사용 하 여 프로젝트의 표준 데이터 작업을 개발 하는 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="f3afb-111">기본적으로 Visual Studio 2013 Web Forms 프로젝트를 생성 하는 코드를 지원 하지 않습니다 하지만 프로젝트에 MVC 종속성을 추가 하거나 확장을 설치 하 여 Web forms 스 캐 폴딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="f3afb-112">두 방법 모두는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-112">Both approaches are shown below.</span></span>

<span data-ttu-id="f3afb-113">Visual Studio 2013 업데이트 2 (현재 RC) 시나리오의 요구 사항에 맞게 ASP.NET 스 캐 폴딩 확장 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="f3afb-114">이 기능을 사용 하 여 사용자 지정된 스 캐 폴딩 템플릿을 만들고 새 스 캐 폴드 추가 대화 상자에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="f3afb-115">사용자 지정된 템플릿 내에서 스 캐 폴드 된 항목을 추가할 때 생성 되는 코드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="f3afb-116">자세한 내용은 [Visual Studio를 사용자 지정 스 캐 폴더 만들기](https://go.microsoft.com/fwlink/p/?LinkId=395029)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3afb-117">전제 조건</span><span class="sxs-lookup"><span data-stu-id="f3afb-117">Prerequisites</span></span>

<span data-ttu-id="f3afb-118">ASP.NET 스 캐 폴딩을 사용 하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="f3afb-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f3afb-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="f3afb-120">Web 개발자 도구 (기본 Visual Studio 2013 설치의 일부)</span><span class="sxs-lookup"><span data-stu-id="f3afb-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="f3afb-121">ASP.NET 웹 프레임 워크 및 도구 2013 (기본 Visual Studio 2013 설치의 일부)</span><span class="sxs-lookup"><span data-stu-id="f3afb-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="f3afb-122">MVC 또는 Web API 스 캐 폴드 된 항목 추가</span><span class="sxs-lookup"><span data-stu-id="f3afb-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="f3afb-123">스 캐 폴드를 추가할 프로젝트 또는 프로젝트 내에 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** – **새 스 캐 폴드 된 항목**다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![스 캐 폴드 항목 추가](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="f3afb-125">**스 캐 폴드 추가** 창 추가할 스 캐 폴드의 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![스 캐 폴드의 유형 선택](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="f3afb-127">합니다 **컨트롤러 추가** 창에는 Entity Framework 6에서 새 비동기 기능을 사용 하려는 지 여부를 포함 하 여 컨트롤러를 생성 하기 위한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![컨트롤러 추가](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="f3afb-129">관련 클래스 및 페이지에는 시나리오에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="f3afb-130">예를 들어, 다음 이미지에는 MVC 컨트롤러 및 이라는 영화 모델 클래스에 대 한 스 캐 폴딩을 통해 생성 된 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![생성된 된 파일](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="f3afb-132">Web forms 스 캐 폴드 된 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="f3afb-133">Web Forms 코드를 생성 하는 스 캐 폴딩에 추가 하려면 Visual Studio에 확장을 설치 하거나 MVC 종속성 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="f3afb-134">두 방법 모두 아래 나와 있지만 이러한 방법 중 하나를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="f3afb-135">확장을 스 캐 폴딩 하는 web Forms</span><span class="sxs-lookup"><span data-stu-id="f3afb-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="f3afb-136">스 캐 폴딩 Web Forms 프로젝트를 사용 하 여 사용할 수 있도록 하는 Visual Studio 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="f3afb-137">Visual Studio에서 선택 **도구가** 차례로 **확장 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="f3afb-138">이 대화 상자에서 검색에 대 한 Visual Studio 갤러리 **Web Forms 스 캐 폴딩**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![web forms 스 캐 폴딩 설치](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="f3afb-140">자세한 내용은 [Web Forms 스 캐 폴딩](https://go.microsoft.com/fwlink/p/?LinkId=396478)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="f3afb-141">MVC 종속성</span><span class="sxs-lookup"><span data-stu-id="f3afb-141">MVC Dependencies</span></span>

<span data-ttu-id="f3afb-142">MVC 종속성을 추가 하려면 선택 **추가** - **스 캐 폴드 된 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="f3afb-143">스 캐 폴드 추가 창에서 선택 **MVC 종속성**다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![MVC 종속성 추가](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="f3afb-145">두 가지 옵션이 있습니다; MVC 스 캐 폴딩에 대 한 최소 및 전체.</span><span class="sxs-lookup"><span data-stu-id="f3afb-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="f3afb-146">최소를 선택 하면 프로젝트에 NuGet 패키지 및 ASP.NET MVC에 대 한 참조만 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="f3afb-147">전체 옵션을 선택 하는 경우 MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="f3afb-148">스 캐 폴딩을 쉽게 사용 하려면 전체 종속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-148">To easily use scaffolding, select Full dependencies.</span></span>

![전체 종속성 선택](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="f3afb-150">종속성을 추가한 후 표시 됩니다는 **readme.txt** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="f3afb-151">프로젝트가 올바르게 작동 하는지 확인 하려면이 파일의 지침에 따라 신중 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="f3afb-152">Readme.txt 파일의 단계를 완료 하는 경우에 MVC 및 Web API에 대 한 이전 섹션에 표시 된 대로 새 스 캐 폴드 된 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="f3afb-153">자동으로 생성 된 뷰와 컨트롤러는 프로젝트 내에서 올바르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="f3afb-154">자습서</span><span class="sxs-lookup"><span data-stu-id="f3afb-154">Tutorials</span></span>

<span data-ttu-id="f3afb-155">참조는 사용자 지정된 스 캐 폴더를 만들려면 [Visual Studio를 사용자 지정 스 캐 폴더 만들기](https://go.microsoft.com/fwlink/p/?LinkId=395029)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="f3afb-156">생성된 된 파일을 사용자 지정 하려면 참조 [스 캐 폴드 된 새 항목 대화 상자에서 생성 된 파일을 사용자 지정 하는 방법을](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="f3afb-157">스 캐 폴딩을 사용 하는 예제에 대 한 **Database First 개발**를 참조 하십시오 [ASP.NET MVC를 사용 하 여 EF Database First](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="f3afb-158">스 캐 폴딩을 사용 하는 예는 **MVC** 프로젝트를 참조 하십시오 [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3afb-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="f3afb-159">스 캐 폴딩을 사용 하는 예는 **Web API** 프로젝트를 참조 하십시오 [Web API 2에서 특성 라우팅을 사용 하 여 REST API를 만들고](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="f3afb-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
