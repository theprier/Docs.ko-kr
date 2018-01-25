---
uid: mvc/overview/getting-started/database-first-development/publish-to-azure
title: "Azure에 데이터베이스에 첫 번째 MVC 사이트 게시 | Microsoft Docs"
author: tfitzmac
description: "MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/22/2014
ms.topic: article
ms.assetid: 7131f1c1-cef3-4396-ab44-ed4519676546
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/publish-to-azure
msc.type: authoredcontent
ms.openlocfilehash: eadc0f2b08df29f80fe53d03cf88cd3cdcecfb12
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="publish-mvc-database-first-site-to-azure"></a><span data-ttu-id="429a5-104">MVC 데이터베이스 첫 번째 사이트를 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="429a5-104">Publish MVC Database First site to Azure</span></span>
====================
<span data-ttu-id="429a5-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="429a5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="429a5-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="429a5-107">이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="429a5-108">생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="429a5-109">시리즈의이 부분 웹 응용 프로그램 및 데이터베이스를 Azure에 게시에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-109">This part of the series focuses on publishing the web app and database to Azure.</span></span> <span data-ttu-id="429a5-110">웹 응용 프로그램 및 데이터베이스를 게시 하는 방법에 대 한 자세한 내용은 하지만 실제로 자습서의 시작 부분에서 시작 해야 하는 단계를 수행 하려면이 항목을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-110">You can read this topic to learn about publishing a web app and database, but to actually perform the steps you must start at the beginning of the tutorial.</span></span> <span data-ttu-id="429a5-111">참조 [시작](setting-up-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-111">See [Getting Started](setting-up-database.md).</span></span>


## <a name="deploy-your-web-app-on-azure"></a><span data-ttu-id="429a5-112">Azure에 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="429a5-112">Deploy your web app on Azure</span></span>

<span data-ttu-id="429a5-113">이 자습서를 완료 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-113">You need an Azure account to complete this tutorial:</span></span>

- <span data-ttu-id="429a5-114">있습니다 수 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-114">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="429a5-115">있습니다 수 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-115">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

<span data-ttu-id="429a5-116">웹 앱을 게시 하려면 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-116">To publish your web app, right-click the project and select **Publish**.</span></span>

![사이트 게시](publish-to-azure/_static/image1.png)

<span data-ttu-id="429a5-118">Microsoft Azure 웹 사이트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-118">Select Microsoft Azure Websites.</span></span>

![Azure를 선택 합니다.](publish-to-azure/_static/image2.png)

<span data-ttu-id="429a5-120">Azure에 로그인 하지 않은 경우 Azure 계정 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-120">If you are not signed in to Azure, provide your Azure account credentials.</span></span> <span data-ttu-id="429a5-121">새 웹 앱을 만들려면 새로 만들기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-121">Then, select New to create a new web app.</span></span>

![새 사이트](publish-to-azure/_static/image3.png)

<span data-ttu-id="429a5-123">웹 앱에 대 한 고유한 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-123">Create a unique name for your web app.</span></span> <span data-ttu-id="429a5-124">이름 필드의 오른쪽에 녹색 확인 표시가 표시 이름은 고유 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-124">You will know the name is unique if you see a green check mark to the right of the name field.</span></span> <span data-ttu-id="429a5-125">웹 앱에 대 한 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-125">Select a region for your web app.</span></span> <span data-ttu-id="429a5-126">선택 **새 서버 만들기** 는 데이터베이스에 대 한이 새 데이터베이스 서버에 대 한 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-126">Select **Create new server** for the database, and provide a user name and password for this new database server.</span></span> <span data-ttu-id="429a5-127">완료 되 면 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-127">When finished, click **Create**.</span></span>

![사이트 만들기](publish-to-azure/_static/image4.png)

<span data-ttu-id="429a5-129">연결 값 이제 모두 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-129">Your connection values are now all set.</span></span> <span data-ttu-id="429a5-130">이러한 값을 변경 되지 않은 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-130">You can leave these values unchanged.</span></span>

![connection](publish-to-azure/_static/image5.png)

<span data-ttu-id="429a5-132">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-132">Click **Next**.</span></span>

<span data-ttu-id="429a5-133">설정의 경우 두 데이터베이스 연결 통지 지정-ApplicationDBContext 및 ContosoUniversityDataEntities 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-133">For Settings, notice that two database connections are specified - ApplicationDBContext and ContosoUniversityDataEntities.</span></span> <span data-ttu-id="429a5-134">ApplicationDBContext은 사용자 계정 테이블에 대 한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-134">ApplicationDBContext is the connection for user account tables.</span></span> <span data-ttu-id="429a5-135">이러한 값은 데이터베이스에 대 한 연결 문자열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-135">These values only show the connection strings for the databases.</span></span> <span data-ttu-id="429a5-136">사이트를 게시 하는 경우 이러한 데이터베이스 게시 될 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-136">It does not mean that these databases will be published when you publish your site.</span></span> <span data-ttu-id="429a5-137">웹 응용 프로그램 게시를 완료 한 후에 데이터베이스 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-137">You will publish your database project after you have finished publishing the web app.</span></span>

![](publish-to-azure/_static/image6.png)

<span data-ttu-id="429a5-138">데이터베이스 연결 옆에 있는 줄임표 (...)는 연결 문자열의 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-138">The ellipsis (...) next to the database connection shows you the details of the connection string.</span></span> <span data-ttu-id="429a5-139">ContosoUniversityDataEntities 옆의 줄임표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-139">Click the ellipsis next to ContosoUniversityDataEntities.</span></span>

![](publish-to-azure/_static/image7.png)

<span data-ttu-id="429a5-140">Note 데이터베이스 서버와 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-140">Note the name of the database server and the database.</span></span> <span data-ttu-id="429a5-141">서버 이름은 임의로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-141">The server name is randomly generated.</span></span> <span data-ttu-id="429a5-142">데이터베이스 이름이 단순 이름을 사용 하 여 사이트의  **\_db** 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-142">The database name is simple the name of your site with **\_db** appended.</span></span> <span data-ttu-id="429a5-143">나중에 데이터베이스에 게시할 때 두 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-143">You will need both names later when you publish your database.</span></span>

<span data-ttu-id="429a5-144">클릭 **확인** 하 여 데이터베이스 연결 문자열 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-144">Click **OK** to close the database connection string window.</span></span>

<span data-ttu-id="429a5-145">웹 게시 창에서 클릭 **다음** 미리 보기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-145">In the Publish Web window, click **Next** to see the preview.</span></span>

![](publish-to-azure/_static/image8.png)

<span data-ttu-id="429a5-146">게시 파일의 목록을 보려면 미리 보기 시작을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-146">You can click Start Preview to see a list of the files to publish.</span></span> <span data-ttu-id="429a5-147">이 이므로이 사이트를 게시 한 처음으로, 목록은 프로젝트의 모든 관련 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-147">Since this is the first time you have published this site, the list is every relevant file in the project.</span></span>

<span data-ttu-id="429a5-148">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-148">Click **Publish**.</span></span>

<span data-ttu-id="429a5-149">출력 창에는 게시의 결과 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-149">The Output pane will display the result of your publication.</span></span>

![](publish-to-azure/_static/image9.png)

<span data-ttu-id="429a5-150">를 게시 한 후 사이트가 immedialely 웹 브라우저에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-150">After publication, the site is immedialely launched in a web browser.</span></span> <span data-ttu-id="429a5-151">사이트를 배포 하 고 사이트에 새 사용자를 등록할 수 있습니다. 그러나 ContosoUniversityData 프로젝트에 있는 테이블 하지 아직 게시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-151">Your site has been deployed and you can register a new user to the site; however, your tables in the ContosoUniversityData project have not yet been published.</span></span> <span data-ttu-id="429a5-152">학생 링크의 경우 목록에서 클릭 하는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-152">If you click on the List of students link you will receive an error.</span></span>

## <a name="publish-database-to-sql-azure"></a><span data-ttu-id="429a5-153">SQL Azure에 데이터베이스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-153">Publish database to SQL Azure</span></span>

<span data-ttu-id="429a5-154">데이터베이스를 게시 하기 전에 로컬 컴퓨터에서 데이터베이스 서버에 연결할 수 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-154">Before publishing your database, you must make sure your local computer can connect to the database server.</span></span> <span data-ttu-id="429a5-155">데이터베이스 서버에 대 한 방화벽 컴퓨터가 데이터베이스에 연결할 수 있는 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-155">The firewall for your database server restricts which machines can connect to the database.</span></span> <span data-ttu-id="429a5-156">방화벽에 대 한 허용된 된 IP 주소에 컴퓨터의 IP 주소를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-156">You need to add the IP address of your computer to the allowed IP addresses for the firewall.</span></span>

<span data-ttu-id="429a5-157">Azure 포털을 통해 Azure 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-157">Login to your Azure account through the Azure portal.</span></span>

<span data-ttu-id="429a5-158">새 데이터베이스를 선택 하 고 선택 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-158">Select your new database and select **Manage**.</span></span>

![관리](publish-to-azure/_static/image10.png)

<span data-ttu-id="429a5-160">데이터베이스 서버 컴퓨터에서 연결을 허용 하도록 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-160">You must configure your database server to allow connections from your computer.</span></span> <span data-ttu-id="429a5-161">관리를 선택 하는 경우 데이터베이스 서버에 허용 된 경우 현재 IP 주소를 추가 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-161">When you select Manage, you are asked to add the current IP address as permitted to the database server.</span></span> <span data-ttu-id="429a5-162">예를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-162">Select Yes.</span></span>

![ip 주소 추가](publish-to-azure/_static/image11.png)

<span data-ttu-id="429a5-164">이전 단계에서 추가한 IP 주소를 연결에 대 한 구성 해야 유일한 IP 주소가 없는 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-164">There is a chance that the IP address you added in the previous step is not the only IP address you need to configure for connections.</span></span> <span data-ttu-id="429a5-165">연결 제대로 설정 되어 있는지 확인 하는 데이터베이스에 로그인을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-165">You can attempt to login to the database to see if the connections have been properly set up.</span></span> <span data-ttu-id="429a5-166">사용자 이름 및 앞에서 만든 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-166">Provide the user and password you created earlier.</span></span>

![login](publish-to-azure/_static/image12.png)

<span data-ttu-id="429a5-168">오류 메시지가 표시 되 면 다른 IP 주소를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-168">If you receive an error message, you need to add another IP address.</span></span> <span data-ttu-id="429a5-169">오류에 대 한 자세한 내용을 보려면 오류 메시지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-169">Click the error message to see more details about error.</span></span> <span data-ttu-id="429a5-170">세부 정보에서를 추가 해야 하는 IP 주소를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-170">In the details you will see the IP address that you need to add.</span></span> <span data-ttu-id="429a5-171">이 IP 주소를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-171">Note this IP address.</span></span>

![허용 되지 않음](publish-to-azure/_static/image13.png)

<span data-ttu-id="429a5-173">이 로그인 창을 닫고 Azure 포털로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-173">Close this login window, and return to the Azure portal.</span></span>

<span data-ttu-id="429a5-174">데이터베이스에 대 한 대시보드로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-174">Navigate to the Dashboard for your database.</span></span> <span data-ttu-id="429a5-175">클릭 **허용 IP 주소 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-175">Click **Manage allowed IP addresses**.</span></span>

![ip 주소 관리](publish-to-azure/_static/image14.png)

<span data-ttu-id="429a5-177">현재 오류 메시지에서 IP 주소를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-177">You must now add the IP address from the error message.</span></span> <span data-ttu-id="429a5-178">오류 메시지를 포함 하도록 허용 된 IP 주소 범위를 변경 하거나 해당 IP 주소를 별도 항목으로 추가 하십시오.</span><span class="sxs-lookup"><span data-stu-id="429a5-178">Either change the range of allowed IP addresses to include the one from the error message, or add that IP address as a separate entry.</span></span>

![새 주소를 추가 합니다.](publish-to-azure/_static/image15.png)

<span data-ttu-id="429a5-180">허용 된 IP 주소 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-180">Save the change to allowed IP addresses.</span></span>

<span data-ttu-id="429a5-181">관리를 클릭 하 고 데이터베이스에 다시 로그인 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="429a5-181">Click Manage, and try logging in again to the database.</span></span> <span data-ttu-id="429a5-182">방화벽에 대 한 허용된 된 IP 주소가 올바르게 구성 되어 되기까지 몇 분 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-182">You may need to wait a few minutes before the allowed IP addresses are correctly configured for the firewall.</span></span> <span data-ttu-id="429a5-183">데이터베이스에 성공적으로 로그인 할 수 있습니다 때 데이터베이스에 연결을 설정을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-183">When you can successfully log in the database, you have finished setting up your connection to the database.</span></span>

<span data-ttu-id="429a5-184">잠시 후에 데이터베이스 배포 결과 확인 하기 때문에이 관리 창을 열어 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-184">You can leave this management window open because you will check the result of your database deployment shortly.</span></span>

<span data-ttu-id="429a5-185">데이터베이스 프로젝트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-185">Return to your database project.</span></span> <span data-ttu-id="429a5-186">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-186">Right-click the project and select **Publish**.</span></span>

![데이터베이스 게시](publish-to-azure/_static/image16.png)

<span data-ttu-id="429a5-188">데이터베이스 게시 창에서 선택한 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-188">In the Publish Database window, select **Edit**.</span></span>

![편집](publish-to-azure/_static/image17.png)

<span data-ttu-id="429a5-190">서버에 대 한 데이터베이스 서버 및 인증 자격 증명의 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-190">Provide the name of the database server and your authentication credentials for the server.</span></span> <span data-ttu-id="429a5-191">자격 증명을 입력 한 후 사용 가능한 데이터베이스 목록에서 이전에 만든 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-191">After providing the credentials, select the database you created from the list of available databases.</span></span> <span data-ttu-id="429a5-192">Visual Studio는 기본적으로 만든 데이터베이스를 동일 않을 수도 있는 프로젝트의 이름으로 데이터베이스 필드의 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-192">By default, Visual Studio sets the name of the database field to the name of your project which might not be the same as the database you created.</span></span>

![](publish-to-azure/_static/image18.png)

<span data-ttu-id="429a5-193">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-193">Click OK.</span></span>

<span data-ttu-id="429a5-194">모든 연결 정보를 다시 입력 하지 않고 나중에 업데이트를 게시할 수 있도록이 프로필을 저장 하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-194">You will probably want to save this profile so you can publish updates in the future without re-entering all of the connection information.</span></span> <span data-ttu-id="429a5-195">**프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-195">Select **Create Profile**.</span></span>

![프로필 저장](publish-to-azure/_static/image19.png)

<span data-ttu-id="429a5-197">이라는 프로젝트에 파일을 만드는 **ContosoUniversityData.publish.xml**합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-197">It will create a file in your project named **ContosoUniversityData.publish.xml**.</span></span> <span data-ttu-id="429a5-198">데이터베이스를 Azure에 게시 하려면 다음에 단순히 해당 프로필을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-198">The next time you want to publish the database to Azure, simply load that profile.</span></span>

<span data-ttu-id="429a5-199">이제 클릭 **게시** Azure에서 데이터베이스를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-199">Now, click **Publish** to create the database on Azure.</span></span>

![게시](publish-to-azure/_static/image20.png)

<span data-ttu-id="429a5-201">잠시 동안 실행 한 후 게시 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-201">After running for a while, the publishing results are displayed.</span></span>

![results](publish-to-azure/_static/image21.png)

<span data-ttu-id="429a5-203">이제 데이터베이스에 대 한 관리 포털에 다시 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-203">Now, you can go back to the management portal for your database.</span></span> <span data-ttu-id="429a5-204">디자인 보기를 새로 고 3 테이블 미리 채워진된 데이터와 함께 배포 된 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-204">Refresh the design view, and notice the 3 tables with pre-filled data have been deployed.</span></span>

![새 테이블](publish-to-azure/_static/image22.png)

<span data-ttu-id="429a5-206">이제 Azure에 배포 되는 웹 응용 프로그램을 테스트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-206">Now you are ready to test the web app that is deployed to Azure.</span></span> <span data-ttu-id="429a5-207">Azure에서 웹 앱 (예: http://contosositeexample.azurewebsites.net/)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-207">Navigate to the web app on Azure (such as http://contosositeexample.azurewebsites.net/).</span></span> <span data-ttu-id="429a5-208">학생 목록에 대 한 링크를 클릭 하 고 학생을 위한 인덱스 보기 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-208">Click the link for List of students and you should see the index view for students.</span></span>

![보기](publish-to-azure/_static/image23.png)

<span data-ttu-id="429a5-210">경우에 따라 연결 및 데이터베이스 충분 한 시간을 적절히 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-210">Occasionally, the database and connection need a little time to be properly configured.</span></span> <span data-ttu-id="429a5-211">오류가 발생 하는 경우 몇 분 정도 기다린 후 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="429a5-211">If you receive an error, wait a few minutes and then try again.</span></span>

## <a name="conclusion"></a><span data-ttu-id="429a5-212">결론</span><span class="sxs-lookup"><span data-stu-id="429a5-212">Conclusion</span></span>

<span data-ttu-id="429a5-213">이 시리즈 사용자가 편집, 업데이트, 만들기 및 데이터를 삭제할 수 있는 기존 데이터베이스에서 코드를 생성 하는 방법의 간단한 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-213">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="429a5-214">프로젝트를 만들려면 ASP.NET MVC 5, Entity Framework, ASP.NET 스 캐 폴딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-214">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span>

<span data-ttu-id="429a5-215">Code First 개발의 기본 예제를 보려면 [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-215">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span>

<span data-ttu-id="429a5-216">고급 예제를 보려면 [ASP.NET MVC 4 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-216">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="429a5-217">Note DbContext API 첫 번째 데이터베이스의 데이터 작업에 사용 하는 첫 번째 코드에서 데이터 작업에 사용할 API와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-217">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="429a5-218">Database First 사용 하려는 경우에 코드 첫 번째 자습서에서 가져오고 동시성 충돌을 처리 관련된 데이터 읽기 및 업데이트와 같은 보다 복잡 한 시나리오를 처리 하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-218">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="429a5-219">유일한 차이점은 데이터베이스, 컨텍스트 클래스 및 엔터티 클래스 만들어지는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="429a5-219">The only difference is in how the database, context class, and entity classes are created.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="429a5-220">이전</span><span class="sxs-lookup"><span data-stu-id="429a5-220">Previous</span></span>](enhancing-data-validation.md)
