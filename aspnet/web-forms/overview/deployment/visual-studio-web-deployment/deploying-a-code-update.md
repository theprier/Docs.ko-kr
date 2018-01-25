---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: f6861c702c1ccb19e5a4eee484a622079e205f86
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="f4a83-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="f4a83-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>
====================
<span data-ttu-id="f4a83-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f4a83-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f4a83-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f4a83-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="f4a83-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="f4a83-107">계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="f4a83-108">개요</span><span class="sxs-lookup"><span data-stu-id="f4a83-108">Overview</span></span>

<span data-ttu-id="f4a83-109">초기 배포 후 유지 관리 하 고 웹 사이트 개발 작업 계속 되 고 장기 하기 전에 업데이트를 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="f4a83-110">이 자습서에서는 응용 프로그램 코드에 대 한 업데이트를 배포 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="f4a83-111">데이터베이스 변경; 구현 및이 자습서에서 배포 하는 업데이트를 초래 하지 않으므로 다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법에 대 한 차이점 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="f4a83-112">미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="f4a83-113">코드 변경</span><span class="sxs-lookup"><span data-stu-id="f4a83-113">Make a code change</span></span>

<span data-ttu-id="f4a83-114">에 추가할 응용 프로그램에 대 한 업데이트의 간단한 예,으로 **강사** 선택한 강사 여 courses 목록이 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="f4a83-115">실행 하는 경우는 **강사** 페이지 된다고을 알 수 있습니다 **선택** 표에서 링크 하는데 확인 이외의 행 배경 turn 회색 않으면 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![선택 된 instructors 페이지](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="f4a83-117">때 실행 되는 코드를 추가 하는 이제는 **선택** 링크를 클릭 하 고 선택한 강사 여 courses 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="f4a83-118">*Instructors.aspx*, 다음 태그를 추가 바로 뒤의 **ErrorMessageLabel** `Label` 제어:</span><span class="sxs-lookup"><span data-stu-id="f4a83-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="f4a83-119">페이지를 실행 하 고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-119">Run the page and select an instructor.</span></span> <span data-ttu-id="f4a83-120">해당 강사 여 과정의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-120">You see a list of courses taught by that instructor.</span></span>

    ![Courses 알게 된 instructors 페이지](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="f4a83-122">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="f4a83-123">코드 업데이트 테스트 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="f4a83-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="f4a83-124">테스트, 스테이징 및 프로덕션에 배포 하 여 게시 프로필을 사용 하려면 먼저 데이터베이스 게시 옵션을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="f4a83-125">더 이상 멤버 자격 데이터베이스에 대 한 grant 및 데이터 배포 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="f4a83-126">열기는 **웹 게시** ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 마법사 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="f4a83-127">클릭는 **테스트** 에서 프로 파일링 할는 **프로필** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="f4a83-128">클릭는 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="f4a83-129">**DefaultConnection** 에 **데이터베이스** 섹션을 선택 취소 된 **데이터베이스 업데이트** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="f4a83-130">클릭는 **프로필** 탭을 클릭 한 다음는 **준비** 에서 프로 파일링 할는 **프로필** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="f4a83-131">변경 내용을 저장 하려면 묻는 하는 경우는 **테스트** 프로필을 클릭 하 여 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="f4a83-132">준비 프로필에 동일한 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="f4a83-133">프로덕션 프로필에 동일한 변경 하는 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="f4a83-134">닫기는 **웹 게시** 마법사.</span><span class="sxs-lookup"><span data-stu-id="f4a83-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="f4a83-135">게시를 다시 실행 한 번의 클릭 하기만 하면 이제는 테스트 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="f4a83-136">이 프로세스를 더 빠르게 수행 하려면 사용할 수 있습니다는 **한 번 클릭으로 웹 게시** 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="f4a83-137">에 **보기** 메뉴 선택 **도구 모음** 선택한 후 **한 번 클릭으로 웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="f4a83-139">**솔루션 탐색기**, ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="f4a83-140">**한 번 클릭으로 웹 게시** 도구 모음에서 선택 된 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시** (왼쪽과 오른쪽을 가리키는 화살표가 있는 아이콘).</span><span class="sxs-lookup"><span data-stu-id="f4a83-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="f4a83-142">Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="f4a83-143">강사 페이지를 실행 하 고 강사 업데이트가 제대로 배포 되었는지 확인 하려면를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="f4a83-144">일반적인 회귀 테스트를 수행 (즉, 테스트 되는 새로운 변경 하지 않은 기존 기능이 해제 해야 하는 사이트의 나머지 부분)입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="f4a83-145">하지만이 자습서에 대 한 해당 단계를 건너뜁니다 고 업데이트를 스테이징 및 프로덕션 배포를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="f4a83-146">다시 배포 하면 어떤 파일이 변경 되어 자동으로 결정 웹 배포 및 복사본만 서버에 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="f4a83-147">기본적으로 웹 배포를 사용 하 여 마지막 변경 날짜 파일에 변경 된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="f4a83-148">소스 제어 시스템 파일 내용을 변경 하지 않는 경우에 날짜 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="f4a83-149">이 경우 다음 파일 체크섬 변경 된 파일을 확인 하는 데 웹 배포를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="f4a83-150">자세한 내용은 참조 [이유 수행 내 파일의 모든 가져오기 재배포 변경 하지 않은 있지만?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) ASP.NET 배포 FAQ에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="f4a83-151">배포 하는 동안 있는 오프 라인 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="f4a83-151">Take the application offline during deployment</span></span>

<span data-ttu-id="f4a83-152">배포 하는 변경에는 이제 단일 페이지에 대 한 간단한 변경이입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="f4a83-153">하지만 더 큰 변경에 배포 하는 경우에 따라 또는 코드와 데이터베이스 변경 내용을 배포 하 고 배포 완료 되기 전에 페이지 요청 하는 경우 사이트가 올바르게 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="f4a83-154">사용자가 배포 진행 중인 동안 사이트에 액세스 하지 못하도록 하려면 사용할 수 있습니다는 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="f4a83-155">라는 파일을 만들었을 때 *앱\_offline.htm* 응용 프로그램의 루트 폴더에 IIS에서는 응용 프로그램을 실행 하는 대신 해당 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="f4a83-156">배포 하는 동안 액세스를 방지 하려면 삽입 되므로 *앱\_offline.htm* 루트 폴더에 배포 프로세스를 실행 한 다음 제거 *앱\_offline.htm* 후 성공 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="f4a83-157">웹 배포를 자동으로 추가 기본값을 구성할 수 있습니다 *앱\_offline.htm* 배포 시작 시 서버에서 파일을 완료 되었을 때이 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="f4a83-158">수행 해야 하면 모든 작업을 수행 하는 게시 프로 파일 (.pubxml) 파일에 다음 XML 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="f4a83-159">이 자습서에 대 한 만들고 사용자 지정을 사용 하는 방법을 알아봅니다 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="f4a83-160">사용 하 여 *앱\_offline.htm* 준비 사이트에서 필요 하지 않습니다, 준비 사이트에 액세스 하는 사용자가 없기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="f4a83-161">하지만 프로덕션 환경에서 배포 하려는 방법을 모두 테스트를 준비를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-appofflinehtm"></a><span data-ttu-id="f4a83-162">앱 만들기\_offline.htm</span><span class="sxs-lookup"><span data-stu-id="f4a83-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="f4a83-163">**솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="f4a83-164">만들기는 **HTML 페이지** 라는 *앱\_offline.htm* (최종 "l"의 삭제는 *.html* 기본적으로 Visual Studio에서 확장명입니다).</span><span class="sxs-lookup"><span data-stu-id="f4a83-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="f4a83-165">템플릿 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="f4a83-166">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-166">Save and close the file.</span></span>

### <a name="copy-appofflinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="f4a83-167">복사 앱\_offline.htm 웹 사이트의 루트 폴더에</span><span class="sxs-lookup"><span data-stu-id="f4a83-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="f4a83-168">모든 FTP 도구를 사용 하 여 웹 사이트에 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="f4a83-169">[FileZilla](http://filezilla-project.org/) 은 인기 있는 FTP 도구 이며 스크린 샷에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="f4a83-170">다음 세 가지 FTP 도구를 사용 하려면 필요: FTP URL, 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="f4a83-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="f4a83-171">URL은 Azure 관리 포털에서 웹 사이트의 대시보드 페이지에 표시 되 고에서 사용자 이름 및 FTP에 대 한 암호를 확인할 수 있습니다는 *.publishsettings* 이전에 다운로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="f4a83-172">다음 단계에는 이러한 값을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="f4a83-173">Azure 관리 포털에서 클릭 **웹사이트** 탭 한 다음 스테이징 웹 사이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="f4a83-174">에 **대시보드** 페이지에서 FTP 호스트에 이름을 찾으려면 아래로 스크롤은 **빠른 보기** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f4a83-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP 호스트 이름](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="f4a83-176">준비를 열고 *.publishsettings* 메모장 이나 다른 텍스트 편집기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="f4a83-177">찾기의 `publishProfile` FTP 프로필에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="f4a83-178">복사는 `userName` 및 `userPWD` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 자격 증명](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="f4a83-180">FTP 도구 및 FTP URL에 로그온을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="f4a83-181">복사 *앱\_offline.htm* 에 솔루션 폴더에서는 */사이트/wwwroot* 준비 사이트에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![App_offline 복사](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="f4a83-183">준비 사이트의 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="f4a83-184">참조 하는 *앱\_offline.htm* 페이지 홈 페이지 대신 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![브라우저 창에서 app_offline.htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="f4a83-186">준비를 배포할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="f4a83-187">코드 업데이트 스테이징 및 프로덕션에 배포</span><span class="sxs-lookup"><span data-stu-id="f4a83-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="f4a83-188">**한 번 클릭으로 웹 게시** 도구 모음에서 선택 된 **준비** 게시 프로필을 클릭 한 다음 **웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="f4a83-189">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 브라우저 사이트의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="f4a83-190">*앱\_offline.htm* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="f4a83-191">성공적인 배포를 확인 하려면를 테스트 하려면 먼저 제거 해야는 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="f4a83-192">FTP 도구의 반환 및 delete **앱\_offline.htm** 준비 사이트에서.</span><span class="sxs-lookup"><span data-stu-id="f4a83-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="f4a83-193">브라우저에서 준비 사이트에서 강사 페이지를 열고 강사 업데이트가 제대로 배포 되었는지 확인 하려면 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="f4a83-194">준비에 대해 수행한 것 처럼 프로덕션에 대해 동일한 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="f4a83-195">변경 내용을 검토 하 고 특정 파일 배포</span><span class="sxs-lookup"><span data-stu-id="f4a83-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="f4a83-196">또한 visual Studio 2012는 개별 파일을 배포 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="f4a83-197">선택한 파일에 대 한 배포 된 버전과 로컬 버전 간의 차이점을 볼 대상 환경으로 파일을 배포 하거나 로컬 프로젝트에 대상 환경에서 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="f4a83-198">이 자습서의이 섹션에서 이러한 기능을 사용 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="f4a83-199">배포에 대 한 변경 확인</span><span class="sxs-lookup"><span data-stu-id="f4a83-199">Make a change to deploy</span></span>

1. <span data-ttu-id="f4a83-200">열기 *Content/Site.css*, 했는데에 대 한 블록의 `body` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="f4a83-201">에 대 한 값을 변경 `background-color` 에서 `#fff` 를 `darkblue`합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="f4a83-202">게시 미리 보기 창에서 변경 된 내용을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="f4a83-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="f4a83-203">사용 하는 경우는 **웹 게시** 마법사 프로젝트를 게시 하는 어떤 변경 하려고에서 파일을 두 번 클릭 하 여 게시를 볼 수 있습니다는 **미리 보기** 창.</span><span class="sxs-lookup"><span data-stu-id="f4a83-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="f4a83-204">ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="f4a83-205">**프로필** 드롭 다운 목록에서 **테스트** 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="f4a83-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="f4a83-206">클릭 **미리 보기**, 클릭 하 고 **미리 보기 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="f4a83-207">에 **미리 보기** 창에서 두 번 클릭 **Site.css**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![Site.css를 두 번 클릭](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="f4a83-209">**변경 내용 미리 보기가** 대화 상자에 배포 될 변경 내용 미리 보기에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![Site.css에 변경 내용 미리 보기](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="f4a83-211">두 번 클릭는 *Web.config* 파일인은 **변경 내용 미리 보기** 대화 상자 구성 변환 빌드 결과 보여 줍니다 및 게시 프로필 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="f4a83-212">이 시점에서 프로 비전 하지 않은 원인을 *Web.config* 변경 되어 변경 내용을 확인 하려는 서버에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="f4a83-213">그러나는 **변경 내용 미리 보기가** 창 두 가지 변경 내용이 올바르게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="f4a83-214">두 개의 XML 요소를 제거할 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="f4a83-215">이러한 요소를 선택 하면 게시 프로세스에 의해 추가 **실행 Code First 마이그레이션이 응용 프로그램 시작 시** 는 Code First 컨텍스트 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="f4a83-216">게시 프로세스가 것 같습니다. 제거 되지 것입니다 되지만 제거 되 고 있으므로 해당 요소를 추가 하기 전에 비교를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="f4a83-217">이 오류는 이후 릴리스에서 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="f4a83-218">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-218">Click **Close**.</span></span>
6. <span data-ttu-id="f4a83-219">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-219">Click **Publish**.</span></span>
7. <span data-ttu-id="f4a83-220">브라우저를 열면 테스트 사이트의 홈 페이지에 CTRL + f 5를 눌러 CSS 변경의 결과 확인 하기 위해 하드 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS 변경 결과](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="f4a83-222">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="f4a83-223">솔루션 탐색기에서 특정 파일 게시</span><span class="sxs-lookup"><span data-stu-id="f4a83-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="f4a83-224">파란색 배경을 고 원래 색으로 되돌리려면 싶으면 하지 않는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="f4a83-225">이 섹션에서는 특정 파일에서 직접 게시 하 여 원래 설정을 복원 합니다 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="f4a83-226">열기 *Content/Site.css* 및 복원는 `background-color` 설정을 `#fff`합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="f4a83-227">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Content/Site.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="f4a83-228">상황에 맞는 메뉴 옵션 3 개의 게시를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-228">The context menu shows three publish options.</span></span>

    ![솔루션 탐색기에서 옵션 게시](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="f4a83-230">클릭 **Site.css 변경 내용 미리 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="f4a83-231">대상 환경에 로컬 파일의 버전 사이의 차이 표시 하려면 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="f4a83-233">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **Site.css** 다시 클릭 하 고 **게시 Site.css**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="f4a83-234">**웹 게시 동작** 파일 게시 된 창에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![웹 게시 작업 창](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="f4a83-236">브라우저를 열고는 `http://localhost/contosouniversity` URL을 누르고 CTRL + f 5를 하드 되지만 새로 고쳐지지 CSS의 효과 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![기본 CSS 사용한 홈 페이지](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="f4a83-238">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="f4a83-239">요약</span><span class="sxs-lookup"><span data-stu-id="f4a83-239">Summary</span></span>

<span data-ttu-id="f4a83-240">이제 데이터베이스 변경 내용을 포함 하지 않는 응용 프로그램 업데이트를 배포 하는 여러 가지 방법을 살펴보았습니다 하 고 변경 내용을 업데이트할지 무엇 인지 확인 기대를 미리 보는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="f4a83-241">이제 강사 페이지에는 **Courses 알게** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f4a83-241">The Instructors page now has a **Courses Taught** section.</span></span>

![Courses 알게 된 instructors 페이지](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="f4a83-243">다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다: 데이터베이스를 강사 페이지를 birthdate 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a83-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f4a83-244">[이전](deploying-to-production.md)
[다음](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="f4a83-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
