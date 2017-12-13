---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: "SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 데이터베이스 업데이트-9/12 배포 | Microsoft Docs"
author: tdykstra
description: "이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 44faca6ac2cdb9193f5c7f6b1d7f5a26e6e22248
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a><span data-ttu-id="8a8dd-103">SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 데이터베이스 업데이트-9/12 배포</span><span class="sxs-lookup"><span data-stu-id="8a8dd-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Database Update - 9 of 12</span></span>
====================
<span data-ttu-id="8a8dd-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8a8dd-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8a8dd-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="8a8dd-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="8a8dd-106">이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="8a8dd-107">웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="8a8dd-108">계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="8a8dd-109">Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능을 표시, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Azure 앱 서비스 웹 앱을 배포 하는 방법을 보여 줍니다. 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="8a8dd-110">개요</span><span class="sxs-lookup"><span data-stu-id="8a8dd-110">Overview</span></span>

<span data-ttu-id="8a8dd-111">데이터베이스 변경 및 관련된 코드 변경 내용 확인이 자습서에서는 Visual Studio에서 변경 내용을 테스트 한 다음 테스트 환경과 프로덕션 환경에 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-111">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to both the test and production environments.</span></span>

<span data-ttu-id="8a8dd-112">미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="8a8dd-113">테이블에 새 열 추가</span><span class="sxs-lookup"><span data-stu-id="8a8dd-113">Adding a New Column to a Table</span></span>

<span data-ttu-id="8a8dd-114">이 섹션에서는 생년월일이 날짜 열을 추가한는 `Person` 하기 위한 기본 클래스는 `Student` 및 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-114">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="8a8dd-115">그런 다음 새 열이 표시 되도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-115">Then you update the page that displays instructor data so that it displays the new column.</span></span>

<span data-ttu-id="8a8dd-116">에 *ContosoUniversity.DAL* 프로젝트, 열기 *Person.cs* 의 끝에 다음 속성을 추가 하 고는 `Person` (있어야 닫는 중괄호 뒤 두) 클래스:</span><span class="sxs-lookup"><span data-stu-id="8a8dd-116">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

<span data-ttu-id="8a8dd-117">다음으로 새 열에 대 한 값을 제공 하도록 Seed 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-117">Next, update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="8a8dd-118">열기 *Migrations\Configuration.cs* 및 시작 하는 코드 블록을 바꾸기 `var instructors = new List<Instructor>` 생년월일 정보를 포함 하는 다음 코드 블록:</span><span class="sxs-lookup"><span data-stu-id="8a8dd-118">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

<span data-ttu-id="8a8dd-119">ContosoUniversity 프로젝트를 열고 *Instructors.aspx* 생년월일을 표시 하려면 새 서식 파일 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-119">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="8a8dd-120">고용 날짜 및 사무실 할당 용 간의 추가.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-120">Add it between the ones for hire date and office assignment:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

<span data-ttu-id="8a8dd-121">(코드 들여쓰기 위치에서 동기화를 가져온 경우 누르면 CTRL-K 및 CTRL D 자동으로 파일의 서식을 다시 지정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="8a8dd-121">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>

<span data-ttu-id="8a8dd-122">솔루션을 작성 한 다음 엽니다는 **패키지 관리자 콘솔** 창.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-122">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="8a8dd-123">ContosoUniversity.DAL으로 아직 선택 되어 있는지 확인은 **기본 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-123">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>

<span data-ttu-id="8a8dd-124">에 **패키지 관리자 콘솔** 창에서 **ContosoUniversity.DAL** 로 **기본 프로젝트**, 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-124">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

<span data-ttu-id="8a8dd-125">Visual Studio 새 정의 하는 클래스 파일을 엽니다이 명령이 완료 되 면 `DbMIgration` 클래스 및는 `Up` 메서드 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-125">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` class, and in the `Up` method you can see the code that creates the new column.</span></span>

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

<span data-ttu-id="8a8dd-127">솔루션을 작성 하 고 다음에 다음 명령을 입력 된 **패키지 관리자 콘솔** 창 (ContosoUniversity.DAL 프로젝트가 선택 되어 있는지 확인):</span><span class="sxs-lookup"><span data-stu-id="8a8dd-127">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

<span data-ttu-id="8a8dd-128">명령이 완료 되 면 응용 프로그램을 실행 하 고 강사 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-128">When the command finishes, run the application and select the Instructors page.</span></span> <span data-ttu-id="8a8dd-129">새에 것을 확인할 페이지를 로드 하는 경우 birth date 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-129">When the page loads, you see that it has the new birth date field.</span></span>

<span data-ttu-id="8a8dd-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="8a8dd-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="8a8dd-131">테스트 환경에 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="8a8dd-131">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="8a8dd-132">**솔루션 탐색기** ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-132">In **Solution Explorer** select the ContosoUniversity project.</span></span>

<span data-ttu-id="8a8dd-133">**한 번 클릭으로 웹 게시** 도구 모음에서 선택 된 **테스트** 게시 프로필을 클릭 하 고 **웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-133">In the **Web One Click Publish** toolbar, select the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="8a8dd-134">(도구 모음을 사용 하지 않도록 설정 하는 경우에서 ContosoUniversity 프로젝트를 선택 **솔루션 탐색기**.)</span><span class="sxs-lookup"><span data-stu-id="8a8dd-134">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

<span data-ttu-id="8a8dd-135">Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저 홈 페이지에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-135">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span> <span data-ttu-id="8a8dd-136">업데이트가 성공적으로 배포 되었는지 확인할 강사 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-136">Run the Instructors page to verify that the update was successfully deployed.</span></span> <span data-ttu-id="8a8dd-137">응용 프로그램을이 페이지에 대 한 데이터베이스에 액세스 하려고 하는 경우 Code First 데이터베이스 스키마를 업데이트 하 고 실행 된 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-137">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="8a8dd-138">예상 된 참조 페이지가 표시 **Birth Date** 날짜가 그 안에 있는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-138">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>

<span data-ttu-id="8a8dd-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8a8dd-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="8a8dd-140">데이터베이스 업데이트는 프로덕션 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="8a8dd-140">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="8a8dd-141">이제 프로덕션 환경에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-141">You can now deploy to production.</span></span> <span data-ttu-id="8a8dd-142">유일한 차이점은 사용 합니다 *앱\_offline.htm* 사용자가 사이트에 액세스 하 고 있으므로 변경 내용을 배포 하는 동안 데이터베이스를 업데이트 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-142">The only difference is that you'll use *app\_offline.htm* to prevent users from accessing the site and thus updating the database while you're deploying changes.</span></span> <span data-ttu-id="8a8dd-143">프로덕션 배포에는 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-143">For production deployment perform the following steps:</span></span>

- <span data-ttu-id="8a8dd-144">업로드는 *앱\_offline.htm* 프로덕션 사이트에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-144">Upload the *app\_offline.htm* file to the production site.</span></span>
- <span data-ttu-id="8a8dd-145">Visual Studio에서의 프로덕션 프로필을 선택는 **한 번 클릭으로 웹 게시** 도구 모음과 클릭 **웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-145">In Visual Studio, choose the Production profile in the **Web One Click Publish** toolbar and click **Publish Web**.</span></span>
- <span data-ttu-id="8a8dd-146">삭제 된 *앱\_offline.htm* 프로덕션 사이트의에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-146">Delete the *app\_offline.htm* file from the production site.</span></span>

> [!NOTE]
> <span data-ttu-id="8a8dd-147">응용 프로그램은 프로덕션 환경에서 사용 중인 동안 백업 계획을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-147">While your application is in use in the production environment you should be implementing a backup plan.</span></span> <span data-ttu-id="8a8dd-148">즉, 있습니다 해야 주기적으로 복사 된 *학교 Prod.sdf* 및 *aspnet Prod.sdf* 등의 몇 가지 세대를 유지 해야 하 고 보안 저장소 위치에 사이트 파일을 프로덕션에서 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-148">That is, you should be periodically copying the *School-Prod.sdf* and *aspnet-Prod.sdf* files from the production site to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="8a8dd-149">데이터베이스를 업데이트할 때 변경 직전의 백업 복사본을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-149">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="8a8dd-150">그런 다음 실수 하 고 프로덕션 환경에 배포한 후 때까지 검색 하지 않는 경우에 데이터베이스를 손상 되기 전의 상태로 복구할 수 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-150">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span>


<span data-ttu-id="8a8dd-151">Visual Studio는 브라우저에서 홈 페이지 URL을 열 때는 *앱\_offline.htm* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-151">When Visual Studio opens the home page URL in the browser, the *app\_offline.htm* page is displayed.</span></span> <span data-ttu-id="8a8dd-152">삭제 한 후의 *앱\_offline.htm* 파일인 업데이트가 성공적으로 배포 되었는지 확인할를 다시 홈 페이지를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-152">After you delete the *app\_offline.htm* file, you can browse to your home page again to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="8a8dd-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="8a8dd-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span></span>

<span data-ttu-id="8a8dd-154">이제 테스트 환경과 프로덕션에 대 한 데이터베이스 변경을 포함 하는 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-154">You've now deployed an application update that included a database change to both test and production.</span></span> <span data-ttu-id="8a8dd-155">다음 자습서 SQL Server Express 및 SQL Server를 SQL Server Compact에서 데이터베이스를 마이그레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a8dd-155">The next tutorial shows you how to migrate your database from SQL Server Compact to SQL Server Express and SQL Server.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="8a8dd-156">[이전](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[다음](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="8a8dd-156">[Previous](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[Next](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span></span>
