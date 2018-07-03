---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 37b996452dfa619ba1276a1aba562ed7efc579b5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389191"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="ed0b3-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="ed0b3-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>
====================
<span data-ttu-id="ed0b3-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ed0b3-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="ed0b3-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="ed0b3-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="ed0b3-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="ed0b3-107">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="ed0b3-108">개요</span><span class="sxs-lookup"><span data-stu-id="ed0b3-108">Overview</span></span>

<span data-ttu-id="ed0b3-109">데이터베이스 변경 및 관련된 코드 변경 확인이 자습서에서는 Visual Studio에서 변경 내용을 테스트 한 다음 테스트, 스테이징 및 프로덕션 환경에 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="ed0b3-110">자습서에는 먼저에서 Code First 마이그레이션을 관리 하는 데이터베이스를 업데이트 하는 방법을 보여 줍니다 하 고 dbDacFx 공급자를 사용 하 여 데이터베이스를 업데이트 하는 방법을 보여줍니다 나중에 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="ed0b3-111">미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="ed0b3-112">Code First 마이그레이션을 사용 하 여 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="ed0b3-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="ed0b3-113">Birth date 열을 추가 하면이 섹션에서는 합니다 `Person` 기본 클래스에 대 한 합니다 `Student` 및 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="ed0b3-114">새 열이 표시 되도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="ed0b3-115">마지막으로, 테스트, 스테이징 및 프로덕션에 변경 내용을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="ed0b3-116">응용 프로그램 데이터베이스의 테이블에 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="ed0b3-117">에 *ContosoUniversity.DAL* 프로젝트를 열고 *Person.cs* 끝에 다음 속성을 추가 하 고는 `Person` 클래스 (없어야 닫는 중괄호 다음 두):</span><span class="sxs-lookup"><span data-stu-id="ed0b3-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="ed0b3-118">다음으로 업데이트 된 `Seed` 메서드는 새 열에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="ed0b3-119">오픈 *migrations\ configuration.cs* 시작 하는 코드 블록을 바꾸고 `var instructors = new List<Instructor>` 생년월일 정보를 포함 하는 다음 코드 블록을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ed0b3-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="ed0b3-120">솔루션을 작성 하 고 엽니다는 **패키지 관리자 콘솔** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="ed0b3-121">ContosoUniversity.DAL으로 아직 선택 되어 있는지 확인 합니다 **기본 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="ed0b3-122">에 **패키지 관리자 콘솔** 창에서 **ContosoUniversity.DAL** 으로 **기본 프로젝트**, 다음 명령을 입력:</span><span class="sxs-lookup"><span data-stu-id="ed0b3-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="ed0b3-123">이 명령은 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMIgration` 클래스 및는 `Up` 메서드는 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="ed0b3-124">합니다 `Up` 변경 내용을 구현 하는 경우 메서드는 열을 만듭니다 및 `Down` 롤백하는 변경 하는 경우 메서드는 열을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="ed0b3-126">솔루션을 빌드하고에서 다음 명령을 입력 합니다 **패키지 관리자 콘솔** 창 (ContosoUniversity.DAL 프로젝트 여전히 선택 되어 있는지 확인):</span><span class="sxs-lookup"><span data-stu-id="ed0b3-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="ed0b3-127">Entity Framework를 실행 합니다 `Up` 메서드를 실행 합니다 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="ed0b3-128">강사 페이지에서 새 열을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="ed0b3-129">ContosoUniversity 프로젝트에서 엽니다 *Instructors.aspx* 생년월일에 표시할 새 템플릿 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="ed0b3-130">고용 날짜 및 office 할당 용 간에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="ed0b3-131">(코드 들여쓰기 동기화 되지 않는 경우를 누르면 CTRL + K와 CTRL-D 파일을 자동으로 서식을 다시 지정 하려면 다음 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="ed0b3-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="ed0b3-132">응용 프로그램을 실행 하 고 클릭 합니다 **강사** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="ed0b3-133">새에 참조 페이지를 로드 하는 경우 birth date 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![Birthdate 사용 하 여 강사 페이지](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="ed0b3-135">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="ed0b3-136">데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="ed0b3-136">Deploy the database update</span></span>

1. <span data-ttu-id="ed0b3-137">**솔루션 탐색기** ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="ed0b3-138">에 **한 번 클릭으로 웹 게시** 도구 모음에서 클릭 합니다 **테스트** 프로필을 게시 하 고 클릭 **웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="ed0b3-139">(도구 모음을 사용 하지 않도록 설정 하는 경우에서 ContosoUniversity 프로젝트를 선택 **솔루션 탐색기**.)</span><span class="sxs-lookup"><span data-stu-id="ed0b3-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="ed0b3-140">Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저의 홈 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="ed0b3-141">실행 합니다 **강사** 페이지 업데이트를 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="ed0b3-142">응용 프로그램에이 페이지에 대 한 데이터베이스에 액세스 하려고 하는 경우 Code First 데이터베이스 스키마를 업데이트 하 고 실행 되는 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="ed0b3-143">예상 된 참조 페이지를 표시 하는 경우 **Birth Date** 에 날짜 열입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="ed0b3-144">에 **한 번 클릭으로 웹 게시** 도구 모음에서 클릭 합니다 **준비** 프로필을 게시 하 고 클릭 **웹 게시**.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="ed0b3-145">실행 된 **강사** 페이지 업데이트를 성공적으로 배포 되었는지 확인 하려면 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="ed0b3-146">에 **한 번 클릭으로 웹 게시** 도구 모음에서 클릭 합니다 **프로덕션** 프로필을 게시 하 고 클릭 **웹 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="ed0b3-147">실행 합니다 **강사** 업데이트가 성공적으로 배포 되었는지 확인 하려면 프로덕션 환경에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="ed0b3-148">데이터베이스 변경 내용을 포함 하는 실제 프로덕션 응용 프로그램 업데이트에 대 한 일반적으로 수행 동안 응용 프로그램을 오프 라인 배포를 사용 하 여 *앱\_offline.htm*이전 자습서에서 보았듯이, 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="ed0b3-149">DbDacFx 공급자를 사용 하 여 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="ed0b3-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="ed0b3-150">이 섹션에서는 추가 *주석을* 열을는 *사용자* 멤버 자격 데이터베이스에서 테이블을 만들고 표시 하 고 각 사용자에 대 한 주석을 편집할 수 있는 페이지.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="ed0b3-151">다음 변경 내용을 테스트, 스테이징 및 프로덕션에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="ed0b3-152">멤버 자격 데이터베이스의 테이블에 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="ed0b3-153">Visual Studio에서 엽니다 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="ed0b3-154">확장 **(localdb) \v11.0**, 확장 **데이터베이스**를 확장 하 고 **aspnet ContosoUniversity** (되지 **aspnet-ContosoUniversity-Prod**) 펼쳐 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="ed0b3-155">표시 되지 않는 경우 **(localdb) \v11.0** 아래를 **SQL Server** 노드를 마우스 오른쪽 단추로 클릭 합니다 **SQL Server** 노드를 클릭 **SQL Server 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="ed0b3-156">에 **서버에 연결** 대화 상자에 입력 합니다 *(localdb) \v11.0* 으로 **서버 이름**를 클릭 하 고 **연결**.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="ed0b3-157">표시 되지 않는 경우 **aspnet ContosoUniversity**프로젝트를 실행 하 고 사용 하 여 로그인 합니다 *관리자* 자격 증명 (암호가 *devpwd*), 고 새로 고쳐서는  **SQL Server 개체 탐색기** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="ed0b3-158">마우스 오른쪽 단추로 클릭 합니다 **사용자가** 테이블을 마우스 클릭 **뷰 디자이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX 뷰 디자이너](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="ed0b3-160">디자이너에서 추가 *주석을* 열 게 *nvarchar (128)* null을 허용 하 고 클릭 하 고 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![주석 열 추가](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="ed0b3-162">에 **데이터베이스 업데이트 미리 보기** 상자를 클릭 합니다 **데이터베이스 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![데이터베이스 업데이트 미리 보기](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="ed0b3-164">표시 하 고 새 열을 편집 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="ed0b3-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="ed0b3-165">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **계정** ContosoUniversity 프로젝트에서 폴더를 클릭 **추가**를 클릭 하 고 **새 항목** .</span><span class="sxs-lookup"><span data-stu-id="ed0b3-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="ed0b3-166">새 **웹 폼 마스터 페이지를 사용 하 여** 하 고 이름을 *UserInfo.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="ed0b3-167">기본값을 그대로 *Site.Master* 마스터 페이지 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="ed0b3-168">에 다음 태그를 복사 합니다 `MainContent` `Content` 요소 (3 중 마지막 `Content` 요소).</span><span class="sxs-lookup"><span data-stu-id="ed0b3-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="ed0b3-169">마우스 오른쪽 단추로 클릭 합니다 *UserInfo.aspx* 페이지를 클릭 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="ed0b3-170">로그인에 *관리자* 사용자 자격 증명 (암호가 *devpwd*) 페이지 올바르게 작동 하는지 확인 하려면 사용자에 게 몇 가지 설명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![사용자 정보 페이지](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="ed0b3-172">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="ed0b3-173">데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="ed0b3-173">Deploy the database update</span></span>

<span data-ttu-id="ed0b3-174">DbDacFx 공급자를 사용 하 여 배포에 선택 해야 합니다 **데이터베이스 업데이트** 게시 프로필에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="ed0b3-175">그러나 초기 배포에 대 한이 옵션을 사용할 때도 구성한 일부 추가 SQL 스크립트를 실행할: 프로필에서 계속 되 고 다시 실행 되지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="ed0b3-176">엽니다는 **웹 게시** ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 하 여 마법사 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="ed0b3-177">선택 된 **테스트** 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="ed0b3-178">클릭 합니다 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="ed0b3-179">아래 **DefaultConnection**를 선택 **데이터베이스 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="ed0b3-180">초기 배포에 대해 실행 하도록 구성 된 추가 스크립트를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="ed0b3-181">클릭 **데이터베이스 업데이트 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="ed0b3-182">에 **데이터베이스 업데이트 구성** 대화 상자에서 지우기 확인란 옆에 *Grant.sql* 하 고 *aspnet-데이터-dev.sql*합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="ed0b3-183">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-183">Click **Close**.</span></span>
6. <span data-ttu-id="ed0b3-184">클릭 합니다 **미리 보기** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="ed0b3-185">아래 **데이터베이스** 의 오른쪽 **DefaultConnection**를 클릭 합니다 **데이터베이스 미리 보기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![데이터베이스 미리 보기](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="ed0b3-187">미리 보기 창에는 원본 데이터베이스의 스키마와 일치 하는 데이터베이스 스키마를 확인 하기 위해 대상 데이터베이스에서 실행 되는 스크립트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="ed0b3-188">스크립트에 새 열을 추가 하는 ALTER TABLE 명령을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="ed0b3-189">닫기 합니다 **Database 미리 보기** 대화 상자 및 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="ed0b3-190">Visual Studio 업데이트 된 응용 프로그램을 배포 하 고 브라우저의 홈 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="ed0b3-191">사용자 정보 페이지를 실행 (추가 *Account/UserInfo.aspx* 홈 페이지 url) 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="ed0b3-192">입력 하 여 로그인 해야 *admin* 하 고 *devpwd*합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="ed0b3-193">테이블의 데이터는 기본적으로 배포 되지 않습니다 및 개발에서 추가한 주석을 찾을 수 없습니다 있도록 데이터 배포 스크립트를 실행 하려면 구성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="ed0b3-194">이제에 변경 된 데이터베이스에 배포 하 여 페이지가 제대로 작동을 확인 하려면 스테이징에서 새 메모를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="ed0b3-195">스테이징 및 프로덕션에 배포 하려면 동일한 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="ed0b3-196">추가 스크립트를 사용 하지 않도록 설정 하려면 두는 것을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="ed0b3-197">테스트 프로필에 비해 유일한 차이점은 하나의 스크립트 준비에 사용 하지 않도록 설정 됩니다 하만 실행 하도록 구성 된 때문에 프로덕션 프로필 *aspnet-prod-data.sql*합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="ed0b3-198">스테이징 및 프로덕션에 대 한 자격 증명은 관리자 및 prodpwd입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="ed0b3-199">데이터베이스 변경 내용을 포함 하는 실제 프로덕션 응용 프로그램 업데이트에 대 한 일반적으로 수행 동안 응용 프로그램을 오프 라인 배포를 업로드 하 여 *앱\_offline.htm* 게시 하 고 삭제 하기 전에 나중에 볼 수 있듯이 [이전 자습서](deploying-a-code-update.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="ed0b3-200">요약</span><span class="sxs-lookup"><span data-stu-id="ed0b3-200">Summary</span></span>

<span data-ttu-id="ed0b3-201">이제 dbDacFx 공급자와 Code First 마이그레이션을 사용 하 여 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![Birthdate 사용 하 여 강사 페이지](deploying-a-database-update/_static/image8.png)

![사용자 정보 페이지](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="ed0b3-204">다음 자습서에서는 명령줄을 사용 하 여 배포를 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed0b3-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ed0b3-205">[이전](deploying-a-code-update.md)
> [다음](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="ed0b3-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
