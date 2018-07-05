---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Code-Only 업데이트-12 8 배포 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: 39075d2e979076f88200ea595c92f95f38f35911
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374015"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="f7e52-103">SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Code-Only 업데이트-12 8 배포</span><span class="sxs-lookup"><span data-stu-id="f7e52-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>
====================
<span data-ttu-id="f7e52-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f7e52-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f7e52-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f7e52-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="f7e52-106">이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="f7e52-107">Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="f7e52-108">계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="f7e52-109">Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="f7e52-110">개요</span><span class="sxs-lookup"><span data-stu-id="f7e52-110">Overview</span></span>

<span data-ttu-id="f7e52-111">초기 배포 후 유지 관리 하 고 웹 사이트 개발의 작업 계속 되 고 오래 전에 하려는 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="f7e52-112">이 자습서에서는 응용 프로그램 코드에 대 한 업데이트를 배포 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="f7e52-113">이 업데이트는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 방법에 대 한 차이점 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="f7e52-114">미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="f7e52-115">코드 변경</span><span class="sxs-lookup"><span data-stu-id="f7e52-115">Making a Code Change</span></span>

<span data-ttu-id="f7e52-116">간단한 예로 업데이트 응용 프로그램을 추가 합니다 **강사** 선택한 강사가가 르 친 과정 목록을 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="f7e52-117">실행 하는 경우는 **강사** 페이지를 보면 있는지 **선택** 표의 링크 하지 확인 이외의 행 배경색 설정 회색 있지만.</span><span class="sxs-lookup"><span data-stu-id="f7e52-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

<span data-ttu-id="f7e52-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span></span>

<span data-ttu-id="f7e52-119">이제 때 실행 되는 코드를 추가 합니다 **선택** 링크를 클릭 하 고 선택한 강사가가 르 친 과정의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="f7e52-120">*Instructors.aspx*, 다음 태그를 추가 직후 합니다 **ErrorMessageLabel** `Label` 제어:</span><span class="sxs-lookup"><span data-stu-id="f7e52-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="f7e52-121">페이지를 실행 하 고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-121">Run the page and select an instructor.</span></span> <span data-ttu-id="f7e52-122">해당 강사가가 르 친 과정의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-122">You see a list of courses taught by that instructor.</span></span>

<span data-ttu-id="f7e52-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="f7e52-124">테스트 환경에 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="f7e52-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="f7e52-125">테스트 환경에 배포 게시를 다시 실행 한 번의 클릭 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="f7e52-126">이 프로세스를 더 빠르게 하려면 사용할 수 있습니다 합니다 **한 번 클릭으로 웹 게시** 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="f7e52-127">에 **뷰** 메뉴 선택 **도구 모음** 선택한 후 **한 번 클릭으로 웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="f7e52-129">**솔루션 탐색기**, ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="f7e52-130">**한 번 클릭으로 웹 게시** 도구 모음을 선택 합니다 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시** (왼쪽과 오른쪽을 가리키는 화살표가 있는 아이콘).</span><span class="sxs-lookup"><span data-stu-id="f7e52-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="f7e52-132">Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="f7e52-133">강사 페이지를 실행 하 고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="f7e52-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span></span>

<span data-ttu-id="f7e52-135">일반적으로 회귀 테스트를 수행 (즉, 테스트할 새로운 변경 사항을 기존 기능이 손상 하지 않는지 확인 하는 사이트의 나머지 부분).</span><span class="sxs-lookup"><span data-stu-id="f7e52-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="f7e52-136">하지만이 자습서에 대 한 해당 단계를 건너뜁니다 고 프로덕션에 업데이트를 배포를 진행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="f7e52-137">프로덕션에 대 한 초기 데이터베이스 상태를 다시 배포 방지</span><span class="sxs-lookup"><span data-stu-id="f7e52-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="f7e52-138">실제 응용 프로그램에서 사용자와 상호 작용 프로덕션 사이트에 초기 배포 후 데이터베이스 라이브 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="f7e52-139">따라서 모든 라이브 데이터 초기화는 초기 상태로의 멤버 자격 데이터베이스를 다시 배포 하지 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="f7e52-140">SQL Server Compact 데이터베이스에 파일이 있으므로 합니다 *앱\_데이터* 하는 파일에 있도록 배포 설정을 변경 하 여이 방지 해야 하는 폴더를 *앱\_데이터* 폴더 배포 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="f7e52-141">엽니다는 **프로젝트 속성** ContosoUniversity 프로젝트 및 선택 창 합니다 **웹 패키지 및 게시** 탭 합니다. 있는지 확인 합니다 **구성** 드롭다운 목록 상자에 **(릴리스) 활성** 또는 **릴리스** 선택 옵션을 선택 **앱에서파일을제외\_데이터 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="f7e52-143">디버그 빌드 구성에 대 한 동일 하 게 변경 하는 것이 좋습니다는 것을 나중에 디버그 빌드를 배포 하려는 경우: 변경 **구성** 하 **디버그** 를 선택한 **제외 앱에서 파일\_데이터 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="f7e52-144">저장 후 닫기 합니다 **웹 패키지 및 게시** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="f7e52-145">필요가 있는지 **대상에서 추가 파일 제거** 게시 프로필에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="f7e52-146">해당 옵션을 선택 하면 배포 프로세스를 앱에 있는 데이터베이스를 삭제 합니다\_배포 된 사이트에 데이터를 앱이 삭제 됩니다\_자체 데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="f7e52-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>


## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="f7e52-147">업데이트 하는 동안 프로덕션 사이트에 대 한 사용자 액세스를 방지</span><span class="sxs-lookup"><span data-stu-id="f7e52-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="f7e52-148">배포 하는 변경에는 이제 단일 페이지에 대 한 간단한 변경이입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="f7e52-149">하지만 대규모 변경 사항을 배포 하는 경우에 따라 하 고이 경우 사이트 수 작동 이상 하 게 배포 완료 되기 전에 사용자 페이지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="f7e52-150">이 방지 하려면 사용할 수 있는 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="f7e52-151">라는 파일을 적용할 시기 *앱\_offline.htm* 응용 프로그램의 루트 폴더에서 IIS 자동으로 파일을 표시는 응용 프로그램을 실행 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="f7e52-152">배포 하는 동안 액세스를 방지 하려면 배치 되므로 *앱\_offline.htm* 루트 폴더에서 배포 프로세스를 실행 한 다음 제거 *앱\_offline.htm*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="f7e52-153">**솔루션 탐색기**, (없습니다 프로젝트 중 하나) 솔루션을 마우스 오른쪽 단추로 **새 솔루션 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="f7e52-155">폴더의 이름을 *SolutionFiles*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="f7e52-156">새 폴더에 명명 된 HTML 페이지를 만듭니다 *앱\_offline.htm*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="f7e52-157">기존 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="f7e52-158">복사할 수는 있지만 합니다 *앱\_offline.htm* 파일을 FTP 연결을 사용 하 여 사이트 또는 **파일 관리자** 호스팅 공급자의 제어판에서 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="f7e52-159">이 자습서에서는 사용 된 **파일 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="f7e52-160">제어판을 열고 선택 **파일 관리자** 에서처럼 합니다 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="f7e52-161">선택 **contosouniversity.com** 차례로 **wwwroot** 응용 프로그램의 루트 폴더에 누른 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

<span data-ttu-id="f7e52-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span></span>

<span data-ttu-id="f7e52-163">에 **파일 업로드** 대화 상자를 선택 합니다 *앱\_offline.htm* 파일을 클릭 **업로드**.</span><span class="sxs-lookup"><span data-stu-id="f7e52-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

<span data-ttu-id="f7e52-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span></span>

<span data-ttu-id="f7e52-165">사이트의 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-165">Browse to your site's URL.</span></span> <span data-ttu-id="f7e52-166">표시 된 *앱\_offline.htm* 페이지 홈 페이지가 대신 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

<span data-ttu-id="f7e52-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span></span>

<span data-ttu-id="f7e52-168">이제 프로덕션 환경에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="f7e52-169">프로덕션 환경에 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="f7e52-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="f7e52-170">에 **한 번 클릭으로 웹 게시** 도구 모음에서 선택 합니다 **프로덕션** 게시 프로필을 클릭 한 다음 **웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="f7e52-171">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="f7e52-172">합니다 *앱\_offline.htm* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="f7e52-173">를 성공적으로 배포를 확인 하려면 테스트 전에 제거 해야 합니다 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="f7e52-174">반환 합니다 **파일 관리자** 제어판 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="f7e52-175">선택 **contosouniversity.com** 하 고 **wwwroot**를 선택 **앱\_offline.htm**를 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

<span data-ttu-id="f7e52-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span></span>

<span data-ttu-id="f7e52-177">브라우저에서 공용 사이트에서 강사 페이지를 열고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="f7e52-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="f7e52-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span></span>

<span data-ttu-id="f7e52-179">이제 데이터베이스 변경 내용을 포함 하지 않는 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="f7e52-180">다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7e52-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f7e52-181">[이전](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="f7e52-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
