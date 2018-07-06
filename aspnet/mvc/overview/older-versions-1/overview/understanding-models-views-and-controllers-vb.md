---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
title: 모델, 뷰 및 컨트롤러 이해 (VB) | Microsoft Docs
author: StephenWalther
description: 모델, 뷰 및 컨트롤러에 대 한 자세한 내용은 이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램의 여러 부분을 소개합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: a106374a-5e74-4fd0-9ac0-1a32280e5d0d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
msc.type: authoredcontent
ms.openlocfilehash: c651201a34b9ab6b459d0f2ecf491b49feb64434
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399901"
---
<a name="understanding-models-views-and-controllers-vb"></a><span data-ttu-id="5dd92-104">모델, 뷰 및 컨트롤러 이해 (VB)</span><span class="sxs-lookup"><span data-stu-id="5dd92-104">Understanding Models, Views, and Controllers (VB)</span></span>
====================
<span data-ttu-id="5dd92-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="5dd92-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="5dd92-106">모델, 뷰 및 컨트롤러에 대 한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="5dd92-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="5dd92-107">이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램의 여러 부분을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>


<span data-ttu-id="5dd92-108">이 자습서 모델, 뷰 및 컨트롤러 수와 ASP.NET MVC의 대략적인 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="5dd92-109">즉, M을 설명 합니다 ', V', c ' ASP.NET MVC에서.</span><span class="sxs-lookup"><span data-stu-id="5dd92-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="5dd92-110">이 자습서를 읽은 후 ASP.NET MVC 응용 프로그램의 다른 부분이 함께 작동 하는 방법을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="5dd92-111">또한 ASP.NET Web Forms 응용 프로그램 또는 Active Server Pages 응용 프로그램에서 ASP.NET MVC 응용 프로그램의 아키텍처 차이점을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="5dd92-112">샘플 ASP.NET MVC 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5dd92-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="5dd92-113">ASP.NET MVC 웹 응용 프로그램을 만들기 위한 기본 Visual Studio 템플릿은 ASP.NET MVC 응용 프로그램의 다른 부분을 이해 하는 매우 간단한 샘플 응용 프로그램을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="5dd92-114">이 자습서의이 간단한 응용 프로그램의 활용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="5dd92-115">Visual Studio 2008을 실행 하 여 MVC 템플릿을 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들면 및 파일 메뉴 옵션을 선택 하면, 새 프로젝트 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="5dd92-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="5dd92-116">새 프로젝트 대화 상자에서 프로젝트 형식 (Visual Basic 또는 C#)에서 원하는 프로그래밍 언어를 선택 하 고 선택 **ASP.NET MVC 웹 응용 프로그램** 템플릿에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="5dd92-117">확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-117">Click the OK button.</span></span>


<span data-ttu-id="5dd92-118">[![새 프로젝트 대화 상자](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5dd92-118">[![New Project Dialog](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)</span></span>

<span data-ttu-id="5dd92-119">**그림 01**: 새 프로젝트 대화 상자 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5dd92-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image2.png))</span></span>


<span data-ttu-id="5dd92-120">새 ASP.NET MVC 응용 프로그램을 만들 때 합니다 **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="5dd92-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="5dd92-121">이 대화 상자를 사용 하면 ASP.NET MVC 응용 프로그램을 테스트 하는 것에 대 한 솔루션에 별도 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="5dd92-122">옵션을 선택 **아니요, 단위 테스트 프로젝트를 만들지 않습니다** 을 클릭 합니다 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>


<span data-ttu-id="5dd92-123">[![단위 테스트 대화 상자 만들기](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5dd92-123">[![Create Unit Test Dialog](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)</span></span>

<span data-ttu-id="5dd92-124">**그림 02**: 단위 테스트 만들기 대화 상자 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="5dd92-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image4.png))</span></span>


<span data-ttu-id="5dd92-125">새 ASP.NET MVC 후 응용 프로그램이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="5dd92-126">솔루션 탐색기 창에서 여러 파일과 폴더 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="5dd92-127">특히, 모델, 뷰 및 컨트롤러 라는 세 개의 폴더가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="5dd92-128">폴더 이름에서 추측할 수 있습니다,으로 이러한 폴더는 모델, 뷰 및 컨트롤러를 구현 하는 것에 대 한 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="5dd92-129">컨트롤러 폴더를 확장 하면 HomeController.vb 이라는 파일과 AccountController.vb 라는 파일로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-129">If you expand the Controllers folder, you should see a file named AccountController.vb and a file named HomeController.vb.</span></span> <span data-ttu-id="5dd92-130">Views 폴더를 확장 하는 경우 명명 된 계정에 홈 및 공유 하는 세 개의 하위 폴더 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="5dd92-131">홈 폴더를 확장 하면 About.aspx 및 Index.aspx (그림 3 참조) 라는 추가 파일 두 개가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="5dd92-132">이러한 파일은 기본 ASP.NET MVC 템플릿 사용 하 여 포함 된 샘플 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>


<span data-ttu-id="5dd92-133">[![솔루션 탐색기 창](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5dd92-133">[![The Solution Explorer Window](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)</span></span>

<span data-ttu-id="5dd92-134">**그림 03**:의 솔루션 탐색기 창 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5dd92-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image6.png))</span></span>


<span data-ttu-id="5dd92-135">메뉴 옵션을 선택 하 여 샘플 응용 프로그램을 실행할 수 있습니다 **디버그, 디버깅 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="5dd92-136">또는 F5 키를 눌러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="5dd92-137">ASP.NET 응용 프로그램을 처음으로 실행 하는 경우 디버그 모드를 사용 하는 것이 좋습니다. 그림 4의 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="5dd92-138">확인 단추를 클릭 하 고 응용 프로그램이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-138">Click the OK button and the application will run.</span></span>


<span data-ttu-id="5dd92-139">[![디버깅 해제 대화 상자](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5dd92-139">[![Debugging Not Enabled dialog](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)</span></span>

<span data-ttu-id="5dd92-140">**그림 04**: 디버깅 사용 안 함 대화 상자 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="5dd92-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image8.png))</span></span>


<span data-ttu-id="5dd92-141">ASP.NET MVC 응용 프로그램을 실행 하면 Visual Studio 웹 브라우저에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="5dd92-142">샘플 응용 프로그램은 두 개의 페이지로 구성 되어 있습니다: 인덱스 페이지와 정보 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="5dd92-143">응용 프로그램이 처음 시작 하는 경우 인덱스 페이지가 나타납니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="5dd92-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="5dd92-144">정보 페이지 맨 위에 있는 메뉴 링크를 클릭 하 여 이동할 응용 프로그램의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>


<span data-ttu-id="5dd92-145">[![인덱스 페이지](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5dd92-145">[![The Index Page](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)</span></span>

<span data-ttu-id="5dd92-146">**그림 05**:은 인덱스 페이지 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="5dd92-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image10.png))</span></span>


<span data-ttu-id="5dd92-147">브라우저의 주소 표시줄에 Url을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="5dd92-148">예를 들어 정보 메뉴 링크를 클릭 하면 브라우저 주소 표시줄에서 URL 변경 **/Home/에 대 한**합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="5dd92-149">브라우저 창을 닫고 Visual Studio로 돌아가서 경우 경로 홈/에 대 한 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="5dd92-150">파일이 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-150">The files don't exist.</span></span> <span data-ttu-id="5dd92-151">어떻게 이것이 가능 한가요?</span><span class="sxs-lookup"><span data-stu-id="5dd92-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="5dd92-152">URL 페이지와 같지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="5dd92-153">기존의 ASP.NET Web Forms 응용 프로그램 또는 Active Server Pages 응용 프로그램을 빌드할 때 URL 및 페이지 간의 한 일 대응이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="5dd92-154">서버의 SomePage.aspx 라는 페이지를 요청 하는 경우 다음 했습니다 더 있을 페이지 SomePage.aspx 라는 디스크.</span><span class="sxs-lookup"><span data-stu-id="5dd92-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="5dd92-155">좋지 않은 SomePage.aspx 파일이 없으면 얻게 **404-페이지를 찾을 수 없음** 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="5dd92-156">ASP.NET MVC 응용 프로그램을 빌드하는 경우 반면 없습니다 대응이 됩니다 브라우저의 주소 표시줄에 입력 하는 URL 및 응용 프로그램에서 발견 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="5dd92-157">ASP.NET MVC 응용 프로그램에 URL을 디스크에 페이지 대신 컨트롤러 작업에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="5dd92-158">기존 ASP 또는 ASP.NET 응용 프로그램, 브라우저 요청 페이지에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="5dd92-159">반면에 ASP.NET MVC 응용 프로그램에서 브라우저 요청 컨트롤러 작업에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="5dd92-160">ASP.NET Web Forms 응용 프로그램은 콘텐츠 중심입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="5dd92-161">ASP.NET MVC 응용 프로그램에 반대로 중심 응용 프로그램 논리 이며</span><span class="sxs-lookup"><span data-stu-id="5dd92-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="5dd92-162">ASP.NET 라우팅 이해</span><span class="sxs-lookup"><span data-stu-id="5dd92-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="5dd92-163">브라우저 요청을 호출 하는 ASP.NET 프레임 워크의 기능을 통해 컨트롤러 작업에 매핑하여 *ASP.NET 라우팅에서*합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="5dd92-164">ASP.NET 라우팅은 ASP.NET MVC 프레임 워크에서 사용 됩니다 *경로* 컨트롤러 작업에 들어오는 요청.</span><span class="sxs-lookup"><span data-stu-id="5dd92-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="5dd92-165">ASP.NET 라우팅 들어오는 요청을 처리 하는 경로 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="5dd92-166">이 경로 테이블에는 웹 응용 프로그램을 처음 시작할 때 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="5dd92-167">경로 테이블이 Global.asax 파일에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="5dd92-168">기본 MVC Global.asax 파일 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

<span data-ttu-id="5dd92-169">**목록 1-Global.asax**</span><span class="sxs-lookup"><span data-stu-id="5dd92-169">**Listing 1 - Global.asax**</span></span>

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample1.vb)]

<span data-ttu-id="5dd92-170">ASP.NET 응용 프로그램을 처음 시작 되 면 응용 프로그램\_start () 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="5dd92-171">목록 1에서이 메서드는 RegisterRoutes() 메서드를 호출 하 고 RegisterRoutes() 메서드 기본 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="5dd92-172">하나의 경로 기본 경로 테이블로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-172">The default route table consists of one route.</span></span> <span data-ttu-id="5dd92-173">이 기본 경로 (URL 세그먼트는 슬래시 사이 있는 것)는 세 개의 선분으로 들어오는 모든 요청을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="5dd92-174">첫 번째 세그먼트는 컨트롤러 이름에 매핑된, 두 번째 세그먼트는 작업 이름으로 매핑되고 최종 세그먼트는 id 라는 이름의 작업에 전달 된 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="5dd92-175">예를 들어 다음 URL을 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-175">For example, consider the following URL:</span></span>

<span data-ttu-id="5dd92-176">/ 제품/세부 정보/3</span><span class="sxs-lookup"><span data-stu-id="5dd92-176">/Product/Details/3</span></span>

<span data-ttu-id="5dd92-177">이 URL은 다음과 같은 세 개의 매개 변수를 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="5dd92-178">컨트롤러 = 제품</span><span class="sxs-lookup"><span data-stu-id="5dd92-178">Controller = Product</span></span>

<span data-ttu-id="5dd92-179">작업 세부 정보 =</span><span class="sxs-lookup"><span data-stu-id="5dd92-179">Action = Details</span></span>

<span data-ttu-id="5dd92-180">id = 3</span><span class="sxs-lookup"><span data-stu-id="5dd92-180">Id = 3</span></span>

<span data-ttu-id="5dd92-181">Global.asax 파일에 정의 된 기본 경로 세 매개 변수 모두에 대 한 기본 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="5dd92-182">기본 컨트롤러는 홈, 기본 작업은 인덱스 및 Id 기본값은 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="5dd92-183">염두에서 이러한 기본값을 사용 하 여 다음 URL을 구문 분석 방법을 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="5dd92-184">/ 직원</span><span class="sxs-lookup"><span data-stu-id="5dd92-184">/Employee</span></span>

<span data-ttu-id="5dd92-185">이 URL은 다음과 같은 세 개의 매개 변수를 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="5dd92-186">컨트롤러 직원 =</span><span class="sxs-lookup"><span data-stu-id="5dd92-186">Controller = Employee</span></span>

<span data-ttu-id="5dd92-187">작업 = 인덱스</span><span class="sxs-lookup"><span data-stu-id="5dd92-187">Action = Index</span></span>

<span data-ttu-id="5dd92-188">Id =</span><span class="sxs-lookup"><span data-stu-id="5dd92-188">Id = ��</span></span>

<span data-ttu-id="5dd92-189">마지막으로, 모든 URL을 제공 하지 않고 ASP.NET MVC 응용 프로그램을 열면 (예를 들어 `http://localhost`) URL은 다음과 같은 구문 분석:</span><span class="sxs-lookup"><span data-stu-id="5dd92-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="5dd92-190">컨트롤러 = 홈</span><span class="sxs-lookup"><span data-stu-id="5dd92-190">Controller = Home</span></span>

<span data-ttu-id="5dd92-191">작업 = 인덱스</span><span class="sxs-lookup"><span data-stu-id="5dd92-191">Action = Index</span></span>

<span data-ttu-id="5dd92-192">Id =</span><span class="sxs-lookup"><span data-stu-id="5dd92-192">Id = ��</span></span>

<span data-ttu-id="5dd92-193">HomeController 클래스에 대 한 index () 동작 요청이 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="5dd92-194">컨트롤러의 이해</span><span class="sxs-lookup"><span data-stu-id="5dd92-194">Understanding Controllers</span></span>

<span data-ttu-id="5dd92-195">컨트롤러는 MVC 응용 프로그램을 사용 하 여 사용자 상호 작용 하는 방법을 제어 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="5dd92-196">컨트롤러에는 ASP.NET MVC 응용 프로그램에 대 한 흐름 제어 논리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="5dd92-197">컨트롤러는 사용자 브라우저 요청을 수행 하는 경우 사용자에 게 다시 보낼 어떤 응답을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="5dd92-198">컨트롤러는 방금 클래스 (예를 들어, Visual Basic 또는 C# 클래스).</span><span class="sxs-lookup"><span data-stu-id="5dd92-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="5dd92-199">샘플 ASP.NET MVC 응용 프로그램 컨트롤러 폴더에 있는 HomeController.vb 라는 컨트롤러를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-199">The sample ASP.NET MVC application includes a controller named HomeController.vb located in the Controllers folder.</span></span> <span data-ttu-id="5dd92-200">HomeController.vb 파일의 내용은 나열 하는 2에서 재생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-200">The content of the HomeController.vb file is reproduced in Listing 2.</span></span>

<span data-ttu-id="5dd92-201">**2-HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="5dd92-201">**Listing 2 - HomeController.cs**</span></span>

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample2.vb)]

<span data-ttu-id="5dd92-202">HomeController index () 및 about () 라는 두 가지 방법에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="5dd92-203">이러한 두 메서드는 컨트롤러에 의해 노출 되는 두 가지 작업에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="5dd92-204">URL /Home/인덱스 HomeController.Index() 메서드를 호출 하 고 URL /Home/About HomeController.About() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="5dd92-205">모든 public 메서드를 컨트롤러의 컨트롤러 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="5dd92-206">이 대해 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-206">You need to be careful about this.</span></span> <span data-ttu-id="5dd92-207">이 브라우저에 올바른 URL을 입력 하 여 인터넷에 액세스할 수 있는 모든 사용자가 컨트롤러에 포함 된 모든 public 메서드를 호출할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="5dd92-208">뷰 이해</span><span class="sxs-lookup"><span data-stu-id="5dd92-208">Understanding Views</span></span>

<span data-ttu-id="5dd92-209">HomeController 클래스, index () 및 about ()에 의해 노출 된 두 명의 컨트롤러 작업 뷰를 둘 다 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="5dd92-210">뷰를 HTML 태그 및 브라우저에 전송 되는 콘텐츠를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="5dd92-211">보기는 페이지에 해당 하는 경우 ASP.NET MVC 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="5dd92-212">적절 한 위치에서 보기를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-212">You must create your views in the right location.</span></span> <span data-ttu-id="5dd92-213">HomeController.Index() 작업에는 다음 경로에 있는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="5dd92-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="5dd92-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="5dd92-215">HomeController.About() 작업에는 다음 경로에 있는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="5dd92-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="5dd92-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="5dd92-217">일반적으로 컨트롤러 작업에 대 한 뷰를 반환 하려는 경우 다음 해야 컨트롤러와 동일한 이름 가진 Views 폴더의 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="5dd92-218">하위 폴더 내에서 컨트롤러 작업으로 동일한 이름을 가진.aspx 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="5dd92-219">보기 3의 파일 about.aspx로 뷰를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-219">The file in Listing 3 contains the About.aspx view.</span></span>

<span data-ttu-id="5dd92-220">**3-About.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="5dd92-220">**Listing 3 - About.aspx**</span></span>

[!code-aspx[Main](understanding-models-views-and-controllers-vb/samples/sample3.aspx)]

<span data-ttu-id="5dd92-221">보기 3의 첫 번째 줄을 무시 하면 보기의 나머지 부분은 대부분 표준 HTML 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="5dd92-222">여기에 원하는 모든 HTML 입력 하 여 보기의 콘텐츠를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="5dd92-223">뷰는 Active Server Pages에서 ASP.NET Web Forms 페이지와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="5dd92-224">뷰를 HTML 콘텐츠와 스크립트에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="5dd92-225">원하는.NET에서 프로그래밍 언어 (예를 들어 C# 또는 Visual Basic.NET) 스크립트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="5dd92-226">스크립트를 사용 하 여 데이터베이스 데이터와 같은 동적 콘텐츠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="5dd92-227">모델 이해</span><span class="sxs-lookup"><span data-stu-id="5dd92-227">Understanding Models</span></span>

<span data-ttu-id="5dd92-228">컨트롤러에서 설명한 및 뷰를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="5dd92-229">모델을 설명 해야 하는 마지막 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="5dd92-230">MVC 모델 이란?</span><span class="sxs-lookup"><span data-stu-id="5dd92-230">What is an MVC model?</span></span>

<span data-ttu-id="5dd92-231">MVC 모델을 모든 뷰 또는 컨트롤러에 포함 되지 않은 응용 프로그램 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="5dd92-232">모델에 모든 응용 프로그램 비즈니스 논리, 유효성 검사 논리 및 데이터베이스 액세스 논리를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="5dd92-233">예를 들어,를 사용 하 여 데이터베이스에 액세스 Microsoft Entity Framework를 사용 하는 경우 다음은 Entity Framework 클래스 (.edmx 파일)에서 만든 Models 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="5dd92-234">보기와 관련 된 사용자 인터페이스를 생성 하는 논리만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="5dd92-235">컨트롤러의 오른쪽 보기를 반환 하거나 다른 작업 (흐름 제어)에 사용자를 리디렉션하는 데 필요한 논리는 최소 사항만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="5dd92-236">다른 모든 모델에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="5dd92-237">일반적으로 fat 모델과 스키 니 컨트롤러를 높여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="5dd92-238">컨트롤러 메서드는 코드 몇 줄만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="5dd92-239">컨트롤러 작업을 가져옵니다 너무 fat, 논리를 Models 폴더에 새 클래스 이동 고려해 야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="5dd92-240">요약</span><span class="sxs-lookup"><span data-stu-id="5dd92-240">Summary</span></span>

<span data-ttu-id="5dd92-241">이 자습서 웹 응용 프로그램을 ASP.NET MVC의 여러 부분의 높은 수준의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="5dd92-242">ASP.NET 라우팅에서 매핑되는 방식을 들어오는 브라우저 요청 특정 컨트롤러 작업에 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="5dd92-243">뷰를 브라우저에 반환 되는 방법을 컨트롤러를 오케스트레이션 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="5dd92-244">마지막으로 모델 응용 프로그램 비즈니스, 유효성 검사 및 데이터베이스 액세스 논리를 포함 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5dd92-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>
