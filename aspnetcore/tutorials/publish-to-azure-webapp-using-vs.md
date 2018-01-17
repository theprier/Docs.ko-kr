---
title: "Visual Studio를 사용하여 Azure에 ASP.NET Core 앱 게시"
author: rick-anderson
description: "Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다."
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 12/16/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/publish-to-azure-webapp-using-vs
ms.openlocfilehash: e8de630c4fa8cff5395f7246b91384d4725e4ca6
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
<span data-ttu-id="f85c6-104">/ko-kr</span><span class="sxs-lookup"><span data-stu-id="f85c6-104">/en-us</span></span>

# <a name="publish-an-aspnet-core-web-app-to-azure-app-service-using-visual-studio"></a><span data-ttu-id="f85c6-105">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="f85c6-105">Publish an ASP.NET Core web app to Azure App Service using Visual Studio</span></span>

<span data-ttu-id="f85c6-106">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs) 및 [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="f85c6-106">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs), and [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="f85c6-107">Mac에서 작업하고 있는 경우 [Mac용 Visual Studio에서 Azure에 게시](https://blog.xamarin.com/publish-azure-visual-studio-mac/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f85c6-107">See [Publish to Azure from Visual Studio for Mac](https://blog.xamarin.com/publish-azure-visual-studio-mac/) if you are working on a Mac.</span></span>

## <a name="set-up"></a><span data-ttu-id="f85c6-108">설치</span><span class="sxs-lookup"><span data-stu-id="f85c6-108">Set up</span></span>

* <span data-ttu-id="f85c6-109">계정이 없는 경우 [체험 Azure 계정](https://aka.ms/K5y5yh)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-109">Open a [free Azure account](https://aka.ms/K5y5yh) if you do not have one.</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="f85c6-110">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f85c6-110">Create a web app</span></span>

<span data-ttu-id="f85c6-111">Visual Studio 시작 페이지에서 **파일 > 새로 만들기 > 프로젝트...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-111">In the Visual Studio Start Page, select **File > New > Project...**</span></span>

![파일 메뉴](publish-to-azure-webapp-using-vs/_static/file_new_project.png)

<span data-ttu-id="f85c6-113">**새 프로젝트** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-113">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="f85c6-114">왼쪽 창에서 **.NET Core**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-114">In the left pane, select **.NET Core**.</span></span>
* <span data-ttu-id="f85c6-115">가운데 창에서 **ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-115">In the center pane, select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="f85c6-116">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-116">Select **OK**.</span></span>

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj.png)

<span data-ttu-id="f85c6-118">**새 ASP.NET Core 웹 응용 프로그램** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="f85c6-118">In the **New ASP.NET Core Web Application** dialog:</span></span>

* <span data-ttu-id="f85c6-119">**웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-119">Select **Web Application**.</span></span>
* <span data-ttu-id="f85c6-120">**인증 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-120">Select **Change Authentication**.</span></span>

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_2.png)

<span data-ttu-id="f85c6-122">**인증 변경** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-122">The **Change Authentication** dialog appears.</span></span> 

* <span data-ttu-id="f85c6-123">**개별 사용자 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-123">Select **Individual User Accounts**.</span></span>
* <span data-ttu-id="f85c6-124">**확인**을 선택하여 **새 ASP.NET Core 웹 응용 프로그램**으로 돌아간 다음 다시 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-124">Select **OK** to return to the **New ASP.NET Core Web Application**, then select **OK** again.</span></span>

![새 ASP.NET Core 웹 인증 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_auth.png) 

<span data-ttu-id="f85c6-126">Visual Studio는 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-126">Visual Studio creates the solution.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="f85c6-127">앱 실행</span><span class="sxs-lookup"><span data-stu-id="f85c6-127">Run the app</span></span>

* <span data-ttu-id="f85c6-128">Ctrl+F5를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-128">Press CTRL+F5 to run the project.</span></span>
* <span data-ttu-id="f85c6-129">**정보** 및 **연락처** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-129">Test the **About** and **Contact** links.</span></span>

![localhost의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/show.png)

### <a name="register-a-user"></a><span data-ttu-id="f85c6-131">사용자 등록</span><span class="sxs-lookup"><span data-stu-id="f85c6-131">Register a user</span></span>

* <span data-ttu-id="f85c6-132">**등록**을 선택하고 새 사용자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-132">Select **Register** and register a new user.</span></span> <span data-ttu-id="f85c6-133">가상의 전자 메일 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-133">You can use a fictitious email address.</span></span> <span data-ttu-id="f85c6-134">제출하면 페이지에 다음과 같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-134">When you submit, the page displays the following error:</span></span>

    <span data-ttu-id="f85c6-135">*“내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다. SQL 예외: 데이터베이스를 열 수 없습니다. 응용 프로그램 DB 컨텍스트에 대한 기존 마이그레이션 적용으로 이 문제를 해결할 수 있습니다.”*</span><span class="sxs-lookup"><span data-stu-id="f85c6-135">*"Internal Server Error: A database operation failed while processing the request. SQL exception: Cannot open the database. Applying existing migrations for Application DB context may resolve this issue."*</span></span>
* <span data-ttu-id="f85c6-136">**마이그레이션 적용**을 선택한 다음 페이지가 업데이트되면 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-136">Select **Apply Migrations** and, once the page updates, refresh the page.</span></span>

![내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다.](publish-to-azure-webapp-using-vs/_static/mig.png)

<span data-ttu-id="f85c6-140">앱은 새 사용자를 등록하는 데 사용한 전자 메일 및 **로그아웃** 링크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-140">The app displays the email used to register the new user and a **Log out** link.</span></span>

![Microsoft Edge에서 열린 웹 응용 프로그램.](publish-to-azure-webapp-using-vs/_static/hello.png)

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="f85c6-143">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="f85c6-143">Deploy the app to Azure</span></span>

<span data-ttu-id="f85c6-144">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-144">Right-click on the project in Solution Explorer and select **Publish...**.</span></span>

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

<span data-ttu-id="f85c6-146">**게시** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="f85c6-146">In the **Publish** dialog:</span></span>

* <span data-ttu-id="f85c6-147">**Microsoft Azure App Service**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-147">Select **Microsoft Azure App Service**.</span></span>
* <span data-ttu-id="f85c6-148">기어 아이콘을 선택한 다음 **프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-148">Select the gear icon and then select **Create Profile**.</span></span>
* <span data-ttu-id="f85c6-149">**프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-149">Select **Create Profile**.</span></span>

![게시 대화 상자](publish-to-azure-webapp-using-vs/_static/maas1.png)

### <a name="create-azure-resources"></a><span data-ttu-id="f85c6-151">Azure 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="f85c6-151">Create Azure resources</span></span>

<span data-ttu-id="f85c6-152">**App Service 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-152">The **Create App Service** dialog appears:</span></span>

* <span data-ttu-id="f85c6-153">구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-153">Enter your subscription.</span></span>
* <span data-ttu-id="f85c6-154">**앱 이름**, **리소스 그룹** 및 **App Service 계획** 항목 필드가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-154">The **App Name**, **Resource Group**, and **App Service Plan** entry fields are populated.</span></span> <span data-ttu-id="f85c6-155">이러한 이름을 유지하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-155">You can keep these names or change them.</span></span>

![App Service 대화 상자](publish-to-azure-webapp-using-vs/_static/newrg1.png)

* <span data-ttu-id="f85c6-157">**서비스** 탭을 선택하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-157">Select the **Services** tab to create a new database.</span></span>

* <span data-ttu-id="f85c6-158">녹색 **+** 아이콘을 선택하여 새 SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-158">Select the green **+** icon to create a new SQL Database</span></span>

![새 SQL Database](publish-to-azure-webapp-using-vs/_static/sql.png)

* <span data-ttu-id="f85c6-160">**SQL Database 구성** 대화 상자에서 **새로 만들기...**를 선택하여 새 데이터베이스 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-160">Select **New...** on the **Configure SQL Database** dialog to create a new database.</span></span>

![새 SQL Database 및 서버](publish-to-azure-webapp-using-vs/_static/conf.png)

<span data-ttu-id="f85c6-162">**SQL Server 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-162">The **Configure SQL Server** dialog appears.</span></span>

* <span data-ttu-id="f85c6-163">관리자 사용자 이름 및 암호를 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-163">Enter an administrator user name and password, and then select **OK**.</span></span> <span data-ttu-id="f85c6-164">기본 **서버 이름**을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-164">You can keep the default **Server Name**.</span></span> 

> [!NOTE]
> <span data-ttu-id="f85c6-165">"관리자"는 관리자 사용자 이름으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-165">"admin" is not allowed as the administrator user name.</span></span>

![SQL Server 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_servername.png)

* <span data-ttu-id="f85c6-167">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-167">Select **OK**.</span></span>

<span data-ttu-id="f85c6-168">Visual Studio가 **App Service 만들기** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-168">Visual Studio returns to the **Create App Service** dialog.</span></span>

* <span data-ttu-id="f85c6-169">**App Service 만들기** 대화 상자에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-169">Select **Create** on the **Create App Service** dialog.</span></span>

![SQL Database 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_final.png)

<span data-ttu-id="f85c6-171">Visual Studio는 Azure에서 웹앱 및 SQL Server를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-171">Visual Studio creates the Web app and SQL Server on Azure.</span></span> <span data-ttu-id="f85c6-172">이 단계는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-172">This step can take a few minutes.</span></span> <span data-ttu-id="f85c6-173">만든 리소스에 대한 자세한 내용은 [추가 리소스](#additonal-resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f85c6-173">For information on the resources created, see [Additonal resources](#additonal-resources).</span></span>

<span data-ttu-id="f85c6-174">배포가 완료되면 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-174">When deployment completes, select **Settings**:</span></span>

![SQL Server 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/set.png)

<span data-ttu-id="f85c6-176">**게시** 대화 상자의 **설정** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="f85c6-176">On the **Settings** page of the **Publish** dialog:</span></span>

  * <span data-ttu-id="f85c6-177">**데이터베이스**를 확장하고 **런타임 시 이 연결 문자열 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-177">Expand **Databases** and check **Use this connection string at runtime**.</span></span>
  * <span data-ttu-id="f85c6-178">**Entity Framework 마이그레이션**을 확장하고 **게시에 이 마이그레이션 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-178">Expand **Entity Framework Migrations** and check **Apply this migration on publish**.</span></span>

* <span data-ttu-id="f85c6-179">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-179">Select **Save**.</span></span> <span data-ttu-id="f85c6-180">Visual Studio가 **게시** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-180">Visual Studio returns to the **Publish** dialog.</span></span> 

![게시 대화 상자: 설정 패널](publish-to-azure-webapp-using-vs/_static/pubs.png)

<span data-ttu-id="f85c6-182">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-182">Click **Publish**.</span></span> <span data-ttu-id="f85c6-183">Visual Studio는 Azure에 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-183">Visual Studio publishs your app to Azure.</span></span> <span data-ttu-id="f85c6-184">배포가 완료되면 앱이 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-184">When the depoyment completes, the app is opened in a browser.</span></span>

### <a name="test-your-app-in-azure"></a><span data-ttu-id="f85c6-185">Azure에서 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="f85c6-185">Test your app in Azure</span></span>

* <span data-ttu-id="f85c6-186">**정보** 및 **연락처** 링크 테스트</span><span class="sxs-lookup"><span data-stu-id="f85c6-186">Test the **About** and **Contact** links</span></span>

* <span data-ttu-id="f85c6-187">새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="f85c6-187">Register a new user</span></span>

![Azure App Service의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/register.png)

### <a name="update-the-app"></a><span data-ttu-id="f85c6-189">앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="f85c6-189">Update the app</span></span>

* <span data-ttu-id="f85c6-190">*Pages/About.cshtml* Razor 페이지를 편집하고 내용을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-190">Edit the *Pages/About.cshtml* Razor page and change its contents.</span></span> <span data-ttu-id="f85c6-191">예를 들어 단락을 수정하여 “Hello ASP.NET Core!” 문구를 표시할 수 있습니다. [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]</span><span class="sxs-lookup"><span data-stu-id="f85c6-191">For example, you can modify the paragraph to say "Hello ASP.NET Core!": [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]</span></span>

* <span data-ttu-id="f85c6-192">프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-192">Right-click on the project and select **Publish...** again.</span></span>

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

* <span data-ttu-id="f85c6-194">앱이 게시된 후 변경 내용이 Azure에서 제공되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-194">After the app is published, verify the changes you made are available on Azure.</span></span>

![작업이 완료되었는지 확인합니다.](publish-to-azure-webapp-using-vs/_static/final.png)

### <a name="clean-up"></a><span data-ttu-id="f85c6-196">정리</span><span class="sxs-lookup"><span data-stu-id="f85c6-196">Clean up</span></span>

<span data-ttu-id="f85c6-197">앱 테스트를 완료하면 [Azure Portal](https://portal.azure.com/)로 이동하고 앱을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-197">When you have finished testing the app, go to the [Azure portal](https://portal.azure.com/) and delete the app.</span></span>

* <span data-ttu-id="f85c6-198">**리소스 그룹**을 선택한 다음 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-198">Select **Resource groups**, then select the resource group you created.</span></span>

![Azure Portal: 사이드바 메뉴에 있는 리소스 그룹](publish-to-azure-webapp-using-vs/_static/portalrg.png)

* <span data-ttu-id="f85c6-200">**리소스 그룹** 페이지에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-200">In the **Resource groups** page, select **Delete**.</span></span>

![Azure Portal: 리소스 그룹 페이지](publish-to-azure-webapp-using-vs/_static/rgd.png)

* <span data-ttu-id="f85c6-202">리소스 그룹의 이름을 입력하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-202">Enter the name of the resource group and select **Delete**.</span></span> <span data-ttu-id="f85c6-203">이 자습서에서 만든 앱과 다른 모든 리소스는 이제 Azure에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85c6-203">Your app and all other resources created in this tutorial are now deleted from Azure.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f85c6-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f85c6-204">Next steps</span></span>

* [<span data-ttu-id="f85c6-205">Visual Studio 및 Git을 사용하여 Azure에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="f85c6-205">Continuous Deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)

## <a name="additonal-resources"></a><span data-ttu-id="f85c6-206">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f85c6-206">Additonal resources</span></span>

* [<span data-ttu-id="f85c6-207">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f85c6-207">Azure App Service</span></span>](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="f85c6-208">Azure 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="f85c6-208">Azure resource groups</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups)
* [<span data-ttu-id="f85c6-209">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f85c6-209">Azure SQL Database</span></span>](https://docs.microsoft.com/en-us/azure/sql-database/)