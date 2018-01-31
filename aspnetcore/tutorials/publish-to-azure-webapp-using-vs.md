---
title: "Visual Studio를 사용하여 Azure에 ASP.NET Core 앱 게시"
author: rick-anderson
description: "Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 12/16/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/publish-to-azure-webapp-using-vs
ms.openlocfilehash: d0e64c967ff332365981338809a47faf35d499ab
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="publish-an-aspnet-core-web-app-to-azure-app-service-using-visual-studio"></a><span data-ttu-id="5ee32-103">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="5ee32-103">Publish an ASP.NET Core web app to Azure App Service using Visual Studio</span></span>

<span data-ttu-id="5ee32-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs) 및 [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="5ee32-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs), and [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="5ee32-105">Mac에서 작업하고 있는 경우 [Mac용 Visual Studio에서 Azure에 게시](https://blog.xamarin.com/publish-azure-visual-studio-mac/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ee32-105">See [Publish to Azure from Visual Studio for Mac](https://blog.xamarin.com/publish-azure-visual-studio-mac/) if you are working on a Mac.</span></span>

## <a name="set-up"></a><span data-ttu-id="5ee32-106">설치</span><span class="sxs-lookup"><span data-stu-id="5ee32-106">Set up</span></span>

* <span data-ttu-id="5ee32-107">계정이 없는 경우 [체험 Azure 계정](https://aka.ms/K5y5yh)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-107">Open a [free Azure account](https://aka.ms/K5y5yh) if you don't have one.</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="5ee32-108">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5ee32-108">Create a web app</span></span>

<span data-ttu-id="5ee32-109">Visual Studio 시작 페이지에서 **파일 > 새로 만들기 > 프로젝트...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-109">In the Visual Studio Start Page, select **File > New > Project...**</span></span>

![파일 메뉴](publish-to-azure-webapp-using-vs/_static/file_new_project.png)

<span data-ttu-id="5ee32-111">**새 프로젝트** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-111">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="5ee32-112">왼쪽 창에서 **.NET Core**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-112">In the left pane, select **.NET Core**.</span></span>
* <span data-ttu-id="5ee32-113">가운데 창에서 **ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-113">In the center pane, select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="5ee32-114">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-114">Select **OK**.</span></span>

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj.png)

<span data-ttu-id="5ee32-116">**새 ASP.NET Core 웹 응용 프로그램** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="5ee32-116">In the **New ASP.NET Core Web Application** dialog:</span></span>

* <span data-ttu-id="5ee32-117">**웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-117">Select **Web Application**.</span></span>
* <span data-ttu-id="5ee32-118">**인증 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-118">Select **Change Authentication**.</span></span>

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_2.png)

<span data-ttu-id="5ee32-120">**인증 변경** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-120">The **Change Authentication** dialog appears.</span></span> 

* <span data-ttu-id="5ee32-121">**개별 사용자 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-121">Select **Individual User Accounts**.</span></span>
* <span data-ttu-id="5ee32-122">**확인**을 선택하여 **새 ASP.NET Core 웹 응용 프로그램**으로 돌아간 다음 다시 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-122">Select **OK** to return to the **New ASP.NET Core Web Application**, then select **OK** again.</span></span>

![새 ASP.NET Core 웹 인증 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_auth.png) 

<span data-ttu-id="5ee32-124">Visual Studio는 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-124">Visual Studio creates the solution.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="5ee32-125">앱 실행</span><span class="sxs-lookup"><span data-stu-id="5ee32-125">Run the app</span></span>

* <span data-ttu-id="5ee32-126">Ctrl+F5를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-126">Press CTRL+F5 to run the project.</span></span>
* <span data-ttu-id="5ee32-127">**정보** 및 **연락처** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-127">Test the **About** and **Contact** links.</span></span>

![localhost의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/show.png)

### <a name="register-a-user"></a><span data-ttu-id="5ee32-129">사용자 등록</span><span class="sxs-lookup"><span data-stu-id="5ee32-129">Register a user</span></span>

* <span data-ttu-id="5ee32-130">**등록**을 선택하고 새 사용자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-130">Select **Register** and register a new user.</span></span> <span data-ttu-id="5ee32-131">가상의 전자 메일 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-131">You can use a fictitious email address.</span></span> <span data-ttu-id="5ee32-132">제출하면 페이지에 다음과 같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-132">When you submit, the page displays the following error:</span></span>

    <span data-ttu-id="5ee32-133">*“내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다. SQL 예외: 데이터베이스를 열 수 없습니다. 응용 프로그램 DB 컨텍스트에 대한 기존 마이그레이션 적용으로 이 문제를 해결할 수 있습니다.”*</span><span class="sxs-lookup"><span data-stu-id="5ee32-133">*"Internal Server Error: A database operation failed while processing the request. SQL exception: Cannot open the database. Applying existing migrations for Application DB context may resolve this issue."*</span></span>
* <span data-ttu-id="5ee32-134">**마이그레이션 적용**을 선택한 다음 페이지가 업데이트되면 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-134">Select **Apply Migrations** and, once the page updates, refresh the page.</span></span>

![내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다.](publish-to-azure-webapp-using-vs/_static/mig.png)

<span data-ttu-id="5ee32-138">앱은 새 사용자를 등록하는 데 사용한 전자 메일 및 **로그아웃** 링크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-138">The app displays the email used to register the new user and a **Log out** link.</span></span>

![Microsoft Edge에서 열린 웹 응용 프로그램.](publish-to-azure-webapp-using-vs/_static/hello.png)

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="5ee32-141">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="5ee32-141">Deploy the app to Azure</span></span>

<span data-ttu-id="5ee32-142">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-142">Right-click on the project in Solution Explorer and select **Publish...**.</span></span>

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

<span data-ttu-id="5ee32-144">**게시** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="5ee32-144">In the **Publish** dialog:</span></span>

* <span data-ttu-id="5ee32-145">**Microsoft Azure App Service**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-145">Select **Microsoft Azure App Service**.</span></span>
* <span data-ttu-id="5ee32-146">기어 아이콘을 선택한 다음 **프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-146">Select the gear icon and then select **Create Profile**.</span></span>
* <span data-ttu-id="5ee32-147">**프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-147">Select **Create Profile**.</span></span>

![게시 대화 상자](publish-to-azure-webapp-using-vs/_static/maas1.png)

### <a name="create-azure-resources"></a><span data-ttu-id="5ee32-149">Azure 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="5ee32-149">Create Azure resources</span></span>

<span data-ttu-id="5ee32-150">**App Service 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-150">The **Create App Service** dialog appears:</span></span>

* <span data-ttu-id="5ee32-151">구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-151">Enter your subscription.</span></span>
* <span data-ttu-id="5ee32-152">**앱 이름**, **리소스 그룹** 및 **App Service 계획** 항목 필드가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-152">The **App Name**, **Resource Group**, and **App Service Plan** entry fields are populated.</span></span> <span data-ttu-id="5ee32-153">이러한 이름을 유지하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-153">You can keep these names or change them.</span></span>

![App Service 대화 상자](publish-to-azure-webapp-using-vs/_static/newrg1.png)

* <span data-ttu-id="5ee32-155">**서비스** 탭을 선택하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-155">Select the **Services** tab to create a new database.</span></span>

* <span data-ttu-id="5ee32-156">녹색 **+** 아이콘을 선택하여 새 SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-156">Select the green **+** icon to create a new SQL Database</span></span>

![새 SQL Database](publish-to-azure-webapp-using-vs/_static/sql.png)

* <span data-ttu-id="5ee32-158">**SQL Database 구성** 대화 상자에서 **새로 만들기...**를 선택하여 새 데이터베이스 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-158">Select **New...** on the **Configure SQL Database** dialog to create a new database.</span></span>

![새 SQL Database 및 서버](publish-to-azure-webapp-using-vs/_static/conf.png)

<span data-ttu-id="5ee32-160">**SQL Server 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-160">The **Configure SQL Server** dialog appears.</span></span>

* <span data-ttu-id="5ee32-161">관리자 사용자 이름 및 암호를 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-161">Enter an administrator user name and password, and then select **OK**.</span></span> <span data-ttu-id="5ee32-162">기본 **서버 이름**을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-162">You can keep the default **Server Name**.</span></span> 

> [!NOTE]
> <span data-ttu-id="5ee32-163">"관리자"는 관리자 사용자 이름으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-163">"admin" isn't allowed as the administrator user name.</span></span>

![SQL Server 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_servername.png)

* <span data-ttu-id="5ee32-165">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-165">Select **OK**.</span></span>

<span data-ttu-id="5ee32-166">Visual Studio가 **App Service 만들기** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-166">Visual Studio returns to the **Create App Service** dialog.</span></span>

* <span data-ttu-id="5ee32-167">**App Service 만들기** 대화 상자에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-167">Select **Create** on the **Create App Service** dialog.</span></span>

![SQL Database 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_final.png)

<span data-ttu-id="5ee32-169">Visual Studio는 Azure에서 웹앱 및 SQL Server를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-169">Visual Studio creates the Web app and SQL Server on Azure.</span></span> <span data-ttu-id="5ee32-170">이 단계는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-170">This step can take a few minutes.</span></span> <span data-ttu-id="5ee32-171">만든 리소스에 대한 자세한 내용은 [추가 리소스](#additonal-resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ee32-171">For information on the resources created, see [Additonal resources](#additonal-resources).</span></span>

<span data-ttu-id="5ee32-172">배포가 완료되면 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-172">When deployment completes, select **Settings**:</span></span>

![SQL Server 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/set.png)

<span data-ttu-id="5ee32-174">**게시** 대화 상자의 **설정** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="5ee32-174">On the **Settings** page of the **Publish** dialog:</span></span>

  * <span data-ttu-id="5ee32-175">**데이터베이스**를 확장하고 **런타임 시 이 연결 문자열 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-175">Expand **Databases** and check **Use this connection string at runtime**.</span></span>
  * <span data-ttu-id="5ee32-176">**Entity Framework 마이그레이션**을 확장하고 **게시에 이 마이그레이션 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-176">Expand **Entity Framework Migrations** and check **Apply this migration on publish**.</span></span>

* <span data-ttu-id="5ee32-177">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-177">Select **Save**.</span></span> <span data-ttu-id="5ee32-178">Visual Studio가 **게시** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-178">Visual Studio returns to the **Publish** dialog.</span></span> 

![게시 대화 상자: 설정 패널](publish-to-azure-webapp-using-vs/_static/pubs.png)

<span data-ttu-id="5ee32-180">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-180">Click **Publish**.</span></span> <span data-ttu-id="5ee32-181">Visual Studio는 Azure에 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-181">Visual Studio publishs your app to Azure.</span></span> <span data-ttu-id="5ee32-182">배포가 완료되면 앱이 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-182">When the depoyment completes, the app is opened in a browser.</span></span>

### <a name="test-your-app-in-azure"></a><span data-ttu-id="5ee32-183">Azure에서 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="5ee32-183">Test your app in Azure</span></span>

* <span data-ttu-id="5ee32-184">**정보** 및 **연락처** 링크 테스트</span><span class="sxs-lookup"><span data-stu-id="5ee32-184">Test the **About** and **Contact** links</span></span>

* <span data-ttu-id="5ee32-185">새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="5ee32-185">Register a new user</span></span>

![Azure App Service의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/register.png)

### <a name="update-the-app"></a><span data-ttu-id="5ee32-187">앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ee32-187">Update the app</span></span>

* <span data-ttu-id="5ee32-188">*Pages/About.cshtml* Razor 페이지를 편집하고 내용을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-188">Edit the *Pages/About.cshtml* Razor page and change its contents.</span></span> <span data-ttu-id="5ee32-189">예를 들어 단락을 수정하여 “Hello ASP.NET Core!” 문구를 표시할 수 있습니다. [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]</span><span class="sxs-lookup"><span data-stu-id="5ee32-189">For example, you can modify the paragraph to say "Hello ASP.NET Core!": [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]</span></span>

* <span data-ttu-id="5ee32-190">프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-190">Right-click on the project and select **Publish...** again.</span></span>

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

* <span data-ttu-id="5ee32-192">앱이 게시된 후 변경 내용이 Azure에서 제공되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-192">After the app is published, verify the changes you made are available on Azure.</span></span>

![작업이 완료되었는지 확인합니다.](publish-to-azure-webapp-using-vs/_static/final.png)

### <a name="clean-up"></a><span data-ttu-id="5ee32-194">정리</span><span class="sxs-lookup"><span data-stu-id="5ee32-194">Clean up</span></span>

<span data-ttu-id="5ee32-195">앱 테스트를 완료하면 [Azure Portal](https://portal.azure.com/)로 이동하고 앱을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-195">When you have finished testing the app, go to the [Azure portal](https://portal.azure.com/) and delete the app.</span></span>

* <span data-ttu-id="5ee32-196">**리소스 그룹**을 선택한 다음 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-196">Select **Resource groups**, then select the resource group you created.</span></span>

![Azure Portal: 사이드바 메뉴에 있는 리소스 그룹](publish-to-azure-webapp-using-vs/_static/portalrg.png)

* <span data-ttu-id="5ee32-198">**리소스 그룹** 페이지에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-198">In the **Resource groups** page, select **Delete**.</span></span>

![Azure Portal: 리소스 그룹 페이지](publish-to-azure-webapp-using-vs/_static/rgd.png)

* <span data-ttu-id="5ee32-200">리소스 그룹의 이름을 입력하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-200">Enter the name of the resource group and select **Delete**.</span></span> <span data-ttu-id="5ee32-201">이 자습서에서 만든 앱과 다른 모든 리소스는 이제 Azure에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ee32-201">Your app and all other resources created in this tutorial are now deleted from Azure.</span></span>

### <a name="next-steps"></a><span data-ttu-id="5ee32-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ee32-202">Next steps</span></span>

* [<span data-ttu-id="5ee32-203">Visual Studio 및 Git을 사용하여 Azure에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="5ee32-203">Continuous Deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)

## <a name="additonal-resources"></a><span data-ttu-id="5ee32-204">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5ee32-204">Additonal resources</span></span>

* [<span data-ttu-id="5ee32-205">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5ee32-205">Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="5ee32-206">Azure 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="5ee32-206">Azure resource groups</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)
* [<span data-ttu-id="5ee32-207">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5ee32-207">Azure SQL Database</span></span>](https://docs.microsoft.com/azure/sql-database/)
