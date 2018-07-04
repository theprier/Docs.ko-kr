---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3649f0250e830b76c42d832e51038c2c52ed4561
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368216"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="69b69-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="69b69-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>
====================
<span data-ttu-id="69b69-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="69b69-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="69b69-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="69b69-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="69b69-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="69b69-107">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="69b69-108">개요</span><span class="sxs-lookup"><span data-stu-id="69b69-108">Overview</span></span>

<span data-ttu-id="69b69-109">초기 배포 후 유지 관리 하 고 웹 사이트 개발의 작업 계속 되 고 오래 전에 하려는 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="69b69-110">이 자습서에서는 응용 프로그램 코드에 대 한 업데이트를 배포 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="69b69-111">구현 하 고이 자습서에서 배포 된 업데이트는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 방법에 대 한 차이점 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="69b69-112">미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="69b69-113">코드 변경</span><span class="sxs-lookup"><span data-stu-id="69b69-113">Make a code change</span></span>

<span data-ttu-id="69b69-114">간단한 예로 업데이트 응용 프로그램을 추가 합니다 **강사** 선택한 강사가가 르 친 과정 목록을 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="69b69-115">실행 하는 경우는 **강사** 페이지를 보면 있는지 **선택** 표의 링크 하지 확인 이외의 행 배경색 설정 회색 있지만.</span><span class="sxs-lookup"><span data-stu-id="69b69-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![선택 된 강사 페이지](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="69b69-117">이제 때 실행 되는 코드를 추가 합니다 **선택** 링크를 클릭 하 고 선택한 강사가가 르 친 과정의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="69b69-118">*Instructors.aspx*, 다음 태그를 추가 직후 합니다 **ErrorMessageLabel** `Label` 제어:</span><span class="sxs-lookup"><span data-stu-id="69b69-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="69b69-119">페이지를 실행 하 고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-119">Run the page and select an instructor.</span></span> <span data-ttu-id="69b69-120">해당 강사가가 르 친 과정의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-120">You see a list of courses taught by that instructor.</span></span>

    ![르 친 과정을 사용 하 여 강사 페이지](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="69b69-122">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="69b69-123">테스트 환경에 코드 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="69b69-124">게시 프로필을 사용 하 여 테스트, 스테이징 및 프로덕션에 배포할 수 있습니다, 전에 데이터베이스 게시 옵션을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="69b69-125">멤버 자격 데이터베이스에 대 한 권한 부여 및 데이터 배포 스크립트를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="69b69-126">엽니다는 **웹 게시** ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 하 여 마법사 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="69b69-127">클릭 합니다 **테스트** 에서 프로 파일링 합니다 **프로필** 드롭 다운 목록.</span><span class="sxs-lookup"><span data-stu-id="69b69-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="69b69-128">클릭 합니다 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="69b69-129">아래 **DefaultConnection** 에 **데이터베이스** 섹션의 선택을 취소는 **데이터베이스 업데이트** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="69b69-130">클릭는 **프로필** 탭을 클릭 합니다 **스테이징** 에서 프로 파일링를 **프로필** 드롭 다운 목록.</span><span class="sxs-lookup"><span data-stu-id="69b69-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="69b69-131">변경 내용을 저장 하려는 경우 묻는 하는 경우는 **테스트** 프로 파일링, 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="69b69-132">스테이징 프로필에 동일한 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="69b69-133">프로덕션 프로필에서 동일 하 게 변경 하는 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="69b69-134">닫기 합니다 **웹 게시** 마법사.</span><span class="sxs-lookup"><span data-stu-id="69b69-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="69b69-135">테스트 환경에 배포 하는 것은 이제 실행 한 번의 클릭 하기만 하면 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="69b69-136">이 프로세스를 더 빠르게 하려면 사용할 수 있습니다 합니다 **한 번 클릭으로 웹 게시** 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="69b69-137">에 **뷰** 메뉴 선택 **도구 모음** 선택한 후 **한 번 클릭으로 웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="69b69-139">**솔루션 탐색기**, ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="69b69-140">**한 번 클릭으로 웹 게시** 도구 모음을 선택 합니다 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시** (왼쪽과 오른쪽을 가리키는 화살표가 있는 아이콘).</span><span class="sxs-lookup"><span data-stu-id="69b69-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="69b69-142">Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="69b69-143">강사 페이지를 실행 하 고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="69b69-144">일반적으로 회귀 테스트를 수행 (즉, 테스트할 새로운 변경 사항을 기존 기능이 손상 하지 않는지 확인 하는 사이트의 나머지 부분).</span><span class="sxs-lookup"><span data-stu-id="69b69-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="69b69-145">하지만이 자습서에서는 단계를 건너뛸 하 스테이징 및 프로덕션에 업데이트 배포를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="69b69-146">다시 배포 하면 웹 배포를 자동으로 결정 변경 된 파일 및 복사본에만 서버에 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="69b69-147">기본적으로 웹 배포를 사용 하 여 마지막 변경 날짜 파일에는 변경 된을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="69b69-148">일부 소스 제어 시스템 파일 내용을 변경 하지 않은 경우 날짜에도 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="69b69-149">이 경우 다음 파일 체크섬을 사용 하 여 변경 된 파일을 확인 하려면 웹 배포를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="69b69-150">자세한 내용은 [왜 수행 내 파일을 모두 다시 배포 해도 변경 하지 않지만?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) ASP.NET 배포 faq에서.</span><span class="sxs-lookup"><span data-stu-id="69b69-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="69b69-151">동안 응용 프로그램을 오프 라인 배포를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-151">Take the application offline during deployment</span></span>

<span data-ttu-id="69b69-152">배포 하는 변경에는 이제 단일 페이지에 대 한 간단한 변경이입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="69b69-153">하지만 대규모 변경 사항을 배포 하는 경우에 따라 또는 코드와 데이터베이스 변경 내용을 배포 및 배포 완료 되기 전에 사용자 페이지를 요청 하는 경우 사이트 올바르게 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="69b69-154">사용자가 배포가 진행에서 되는 동안 사이트에 액세스 하지 못하도록 하려면 사용할 수는 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="69b69-155">라는 파일을 적용할 시기 *앱\_offline.htm* 응용 프로그램의 루트 폴더에서 IIS 자동으로 파일을 표시는 응용 프로그램을 실행 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="69b69-156">배포 하는 동안 액세스를 방지 하려면 배치 되므로 *앱\_offline.htm* 루트 폴더에서 배포 프로세스를 실행 한 다음 제거 *앱\_offline.htm* 후 성공 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="69b69-157">기본값을 자동으로 적용할 웹 배포를 구성할 수 있습니다 *앱\_offline.htm* 배포 시작 시 서버에서 파일 및 완료 되 면 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="69b69-158">이렇게 모든 작업을 수행 하 게시 프로필 (.pubxml) 파일에 다음 XML 요소를 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="69b69-159">이 자습서에 대 한 표시를 만들고 사용자 지정을 사용 하는 방법 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="69b69-160">사용 하 여 *앱\_offline.htm* 스테이징 사이트에서 필요 하지 않습니다, 스테이징 사이트에 액세스 하는 사용자가 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="69b69-161">하지만 모든 프로덕션 환경에서 배포 하려는 방법을 테스트할 준비를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-appofflinehtm"></a><span data-ttu-id="69b69-162">앱 만들기\_offline.htm</span><span class="sxs-lookup"><span data-stu-id="69b69-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="69b69-163">**솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="69b69-164">만들기는 **HTML 페이지** 라는 *앱\_offline.htm* (에서 마지막 "l"을 삭제 합니다 *.html* 기본적으로 Visual Studio에서 확장명입니다).</span><span class="sxs-lookup"><span data-stu-id="69b69-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="69b69-165">템플릿 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="69b69-166">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-166">Save and close the file.</span></span>

### <a name="copy-appofflinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="69b69-167">앱 복사\_offline.htm 웹 사이트의 루트 폴더에</span><span class="sxs-lookup"><span data-stu-id="69b69-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="69b69-168">웹 사이트에 파일을 복사할 모든 FTP 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="69b69-169">[FileZilla](http://filezilla-project.org/) 인기 있는 FTP 도구 이며 스크린 샷에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="69b69-170">FTP 도구를 사용 하려면 다음 세 가지: FTP URL, 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="69b69-171">URL은 Azure 관리 포털에서 웹 사이트의 대시보드 페이지에 표시 되 고에서 사용자 이름 및 FTP에 대 한 암호를 찾을 수 있습니다 합니다 *.publishsettings* 앞에서 다운로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="69b69-172">다음 단계에는 이러한 값을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="69b69-173">Azure 관리 포털에서 클릭 **웹 사이트** 탭 한 다음 스테이징 웹 사이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="69b69-174">에 **대시보드** 페이지에서 FTP 호스트 이름 찾기까지 아래로 스크롤합니다 합니다 **간략 상태** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP 호스트 이름](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="69b69-176">준비를 엽니다 *.publishsettings* 메모장 이나 다른 텍스트 편집기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="69b69-177">찾기는 `publishProfile` FTP 프로필에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="69b69-178">복사 합니다 `userName` 고 `userPWD` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 자격 증명](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="69b69-180">FTP 도구 열고 FTP URL에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="69b69-181">복사본 *앱\_offline.htm* 솔루션 폴더에서의 */site/wwwroot* 스테이징 사이트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![App_offline 복사](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="69b69-183">스테이징 사이트의 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="69b69-184">표시 된 *앱\_offline.htm* 페이지 홈 페이지가 대신 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![브라우저 창에서 app_offline.htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="69b69-186">스테이징에 배포 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="69b69-187">스테이징 및 프로덕션에 코드 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="69b69-188">에 **한 번 클릭으로 웹 게시** 도구 모음에서 선택 합니다 **스테이징** 게시 프로필을 클릭 한 다음 **웹 게시**.</span><span class="sxs-lookup"><span data-stu-id="69b69-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="69b69-189">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="69b69-190">합니다 *앱\_offline.htm* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="69b69-191">를 성공적으로 배포를 확인 하려면 테스트 전에 제거 해야 합니다 *앱\_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="69b69-192">FTP 도구를 사용 하 여 돌아가서 삭제할 **앱\_offline.htm** 스테이징 사이트에서.</span><span class="sxs-lookup"><span data-stu-id="69b69-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="69b69-193">브라우저에서 스테이징 사이트에서 강사 페이지를 열고 업데이트를 성공적으로 배포 되었는지 확인 하려면 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="69b69-194">스테이징에 대해 수행한 것 처럼 프로덕션 환경에 동일한 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="69b69-195">변경 내용을 검토 하 고 특정 파일 배포</span><span class="sxs-lookup"><span data-stu-id="69b69-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="69b69-196">또한 visual Studio 2012는 개별 파일을 배포 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="69b69-197">선택한 파일에 대 한 배포 된 버전과 로컬 버전 간의 차이점을 볼, 대상 환경으로 파일을 배포 또는 대상 환경에서 로컬 프로젝트 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="69b69-198">이 자습서의이 섹션에서는 이러한 기능을 사용 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="69b69-199">배포 변경</span><span class="sxs-lookup"><span data-stu-id="69b69-199">Make a change to deploy</span></span>

1. <span data-ttu-id="69b69-200">오픈 *Content/Site.css*에 대 한 블록을 찾아서는 `body` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="69b69-201">값을 변경 `background-color` 에서 `#fff` 에 `darkblue`입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="69b69-202">게시 미리 보기 창에서 변경 내용을 보고합니다</span><span class="sxs-lookup"><span data-stu-id="69b69-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="69b69-203">사용 하는 경우는 **웹 게시** 프로젝트를 게시 하려면 마법사에서 파일을 두 번 클릭 하 여 게시할 변경은 상황을 볼 수 있습니다 합니다 **미리 보기** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="69b69-204">ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="69b69-205">합니다 **프로필** 드롭 다운 목록에서 선택 합니다 **테스트** 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="69b69-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="69b69-206">클릭 **미리 보기**를 클릭 하 고 **미리 보기 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="69b69-207">에 **미리 보기** 창에 두 번 클릭 **Site.css**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![Site.css를 두 번 클릭](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="69b69-209">합니다 **변경 내용 미리 보기** 대화 배포 되는 변경 내용 미리 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![Site.css에 변경 내용 미리 보기](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="69b69-211">두 번 클릭 합니다 *Web.config* 파일을를 **변경 내용 미리 보기** 대화 상자 구성 변환 빌드의 결과 보여 줍니다 및 게시 프로필 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="69b69-212">이 시점에서 수행 하지 않은 원인을 합니다 *Web.config* 변경 내용이 예상한 수 있으므로 서버에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="69b69-213">그러나 합니다 **변경 내용 미리 보기** 창 두 가지 변경 사항을 올바르게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="69b69-214">두 개의 XML 요소를 제거할 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="69b69-215">이러한 요소는 선택 하는 경우 게시 프로세스에 의해 추가 됩니다 **Execute Code First Migrations 응용 프로그램 시작 시** Code First 컨텍스트 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="69b69-216">비교는 제거 되지 것입니다 하지만 제거 되는 것 처럼 보입니다 하므로 게시 프로세스가 해당 요소를 추가 하기 전에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="69b69-217">이 오류는 향후 릴리스에서 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="69b69-218">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-218">Click **Close**.</span></span>
6. <span data-ttu-id="69b69-219">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-219">Click **Publish**.</span></span>
7. <span data-ttu-id="69b69-220">테스트 사이트의 홈 페이지로 브라우저가 열리면 CTRL + F5 키를 눌러 CSS 변경의 결과 확인 하기 위해 하드 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS 변경의 효과](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="69b69-222">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="69b69-223">솔루션 탐색기에서 특정 파일 게시</span><span class="sxs-lookup"><span data-stu-id="69b69-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="69b69-224">배경이 파란색 하 고 싶으면 원래 색으로 되돌릴 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="69b69-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="69b69-225">이 섹션에서 직접 특정 파일을 게시 하 여 원래 설정을 복원 하겠습니다 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="69b69-226">열기 *Content/Site.css* 및 복원 합니다 `background-color` 설정을 `#fff`합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="69b69-227">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *Content/Site.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="69b69-228">상황에 맞는 메뉴 옵션 세 개의 게시를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-228">The context menu shows three publish options.</span></span>

    ![솔루션 탐색기에서 옵션 게시](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="69b69-230">클릭 **Site.css에 변경 내용 미리 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="69b69-231">대상 환경에 로컬 파일 및 해당 버전 간의 차이점을 표시 하는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-콘텐츠/Site.css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="69b69-233">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **Site.css** 다시 누릅니다 **Site.css 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="69b69-234">합니다 **웹 게시 활동** 파일 게시 된 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![웹 게시 활동 창](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="69b69-236">브라우저를 열어는 `http://localhost/contosouniversity` URL을 누릅니다. 하드 시킬 ctrl+f5 CSS의 변경 결과 보려면 새로 고침 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![일반 CSS 사용 하 여 홈 페이지](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="69b69-238">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="69b69-239">요약</span><span class="sxs-lookup"><span data-stu-id="69b69-239">Summary</span></span>

<span data-ttu-id="69b69-240">데이터베이스 변경 내용을 포함 하지 않는 응용 프로그램 업데이트를 배포 하는 여러 방법을 확인 하 셨 고 업데이트될지 무엇 인지 확인 예상과 변경 내용 미리 보기 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="69b69-241">강사 페이지에는 **강좌를 수업** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-241">The Instructors page now has a **Courses Taught** section.</span></span>

![르 친 과정을 사용 하 여 강사 페이지](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="69b69-243">다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다: 강사 페이지를 데이터베이스로 생년월일 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b69-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="69b69-244">[이전](deploying-to-production.md)
> [다음](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="69b69-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
