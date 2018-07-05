---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 권한 설정 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 0660a464063783406a69caf663036811c8ac818e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802035"
---
<a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="dbb56-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 권한 설정</span><span class="sxs-lookup"><span data-stu-id="dbb56-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>
====================
<span data-ttu-id="dbb56-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="dbb56-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="dbb56-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="dbb56-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="dbb56-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="dbb56-107">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="dbb56-108">개요</span><span class="sxs-lookup"><span data-stu-id="dbb56-108">Overview</span></span>

<span data-ttu-id="dbb56-109">이 자습서에 대 한 폴더 사용 권한을 설정 합니다 *Elmah* 폴더에 배포 된 웹 사이트 응용 프로그램 폴더에 로그 파일을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="dbb56-110">Visual Studio 개발 서버 (Cassini) 또는 IIS Express를 사용 하 여 Visual Studio에서 웹 응용 프로그램을 테스트할 때 응용 프로그램 id에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="dbb56-111">개발 컴퓨터에서 관리자는 대부분을 모든 폴더의 모든 파일에 아무것도 할 권한이 전체.</span><span class="sxs-lookup"><span data-stu-id="dbb56-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="dbb56-112">하지만 사이트에 할당 되는 응용 프로그램 풀에 대해 정의 된 id에서 실행 되는 응용 프로그램이 IIS에서 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="dbb56-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="dbb56-113">일반적으로 권한이 제한 된 시스템 정의 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="dbb56-114">기본적으로 읽기와 웹 응용 프로그램의 파일 및 폴더에 대 한 실행 하지만 쓰기 권한이 정보를 참조 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="dbb56-115">응용 프로그램을 만들거나 웹 응용 프로그램에서 일반적인 업데이트 파일 해야 하는 경우 이것이 문제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="dbb56-116">Elmah를 Contoso University 응용 프로그램에서의 XML 파일을 만듭니다는 *Elmah* 오류에 대 한 세부 정보를 저장 하기 위해 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="dbb56-117">같은 Elmah를 사용 하지 않는 경우에 사이트 사용자가 파일을 업로드 하거나 사이트의 폴더에 데이터를 기록 하는 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="dbb56-118">미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="dbb56-119">테스트 오류 로깅 및 보고</span><span class="sxs-lookup"><span data-stu-id="dbb56-119">Test error logging and reporting</span></span>

<span data-ttu-id="dbb56-120">어떻게 표시 되는지 확인 응용 프로그램 하지 올바르게 IIS에서 (했을 때 Visual Studio에서 테스트) 하지만, 일반적으로 Elmah에서 로깅될를 열고 다음 세부 정보를 보려면 Elmah 오류 로그는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="dbb56-121">Elmah는 XML 파일을 만들고 오류 세부 정보를 저장할 수 없는 경우, 빈 오류 보고서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="dbb56-122">브라우저를 열고 이동할 `http://localhost/ContosoUniversity`, 한 다음 같은 잘못 된 URL을 요청 하 고 *Studentsxxx.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="dbb56-123">시스템에서 생성 된 오류 페이지가 대신 표시 합니다 *GenericErrorPage.aspx* 때문에 페이지를 `customErrors` Web.config 파일에서 설정이 "RemoteOnly"이 고 로컬로 실행 하는 IIS:</span><span class="sxs-lookup"><span data-stu-id="dbb56-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![HTTP 404 오류 페이지](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="dbb56-125">지금 실행 *Elmah.axd* 오류 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="dbb56-126">관리자 계정 자격 증명으로 로그인 한 후 (&quot;관리자&quot; 하 고 &quot;devpwd&quot;), Elmah는 XML 파일을 만들 수 없기 때문에 빈 오류 로그 페이지를 표시는 *Elmah*폴더:</span><span class="sxs-lookup"><span data-stu-id="dbb56-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![오류 로그 비어 있음](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="dbb56-128">Elmah 폴더에 대 한 쓰기 권한이 설정</span><span class="sxs-lookup"><span data-stu-id="dbb56-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="dbb56-129">폴더 사용 권한을 수동으로 설정 하거나 배포 프로세스의 자동 부분을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="dbb56-130">복잡 한 MSBuild 코드를 필요 하므로 자동 및 처음 배포할 때가 작업을 수행 해야 하므로 다음 단계를 수동으로 수행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="dbb56-131">(배포 프로세스의이 부분을 확인 하는 방법에 대 한 정보를 참조 하세요 [웹 게시에 폴더 권한 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) Sayed Hashimi의 블로그입니다.)</span><span class="sxs-lookup"><span data-stu-id="dbb56-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="dbb56-132">**파일 탐색기**, 이동할 *C:\inetpub\wwwroot\ContosoUniversity*합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="dbb56-133">마우스 오른쪽 단추로 클릭 합니다 *Elmah* 폴더를 선택 **속성**를 선택한 후는 **보안** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="dbb56-134">
              **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-134">Click **Edit**.</span></span>
3. <span data-ttu-id="dbb56-135">에 **Elmah에 대 한 권한을** 대화 상자에서 **DefaultAppPool**를 선택한 후는 **작성** 확인란을 **허용** 열.</span><span class="sxs-lookup"><span data-stu-id="dbb56-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![ELMAH 폴더에 대 한 사용 권한](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="dbb56-137">(표시 되지 않는 경우 **DefaultAppPool** 에 **그룹 또는 사용자 이름** 목록 아마도 데이 자습서에서 지정한 것 보다 몇 가지 다른 방법을 컴퓨터에 IIS 및 ASP.NET 4를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="dbb56-138">이런 경우 해당 id에 쓰기 권한 부여 확인 하 고 Contoso University 응용 프로그램에 할당 된 응용 프로그램 풀 id가 어떻게 되 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="dbb56-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="dbb56-139">링크를 참조 응용 프로그램 풀 id에 대 한이 자습서의 끝입니다.) 클릭 **확인** 두 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="dbb56-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="dbb56-140">오류 로깅 및 보고를 다시 테스트</span><span class="sxs-lookup"><span data-stu-id="dbb56-140">Retest error logging and reporting</span></span>

<span data-ttu-id="dbb56-141">동일한 방식으로 (잘못 된 URL 요청) 오류가 다시 발생 하 여 테스트 하 고 실행 합니다 **오류 로그** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="dbb56-142">이 오류는 페이지에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-142">This time the error appears on the page.</span></span>

![ELMAH의 오류 로그 페이지](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="dbb56-144">요약</span><span class="sxs-lookup"><span data-stu-id="dbb56-144">Summary</span></span>

<span data-ttu-id="dbb56-145">이제 마친 Contoso University 하는 데 필요한 작업을 모두 로컬 컴퓨터에 IIS에서 올바르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="dbb56-146">다음 자습서에서 생성 됩니다 사이트 공개적으로 사용할 수 있는 Azure에 배포 하 여.</span><span class="sxs-lookup"><span data-stu-id="dbb56-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="dbb56-147">추가 정보</span><span class="sxs-lookup"><span data-stu-id="dbb56-147">More information</span></span>

<span data-ttu-id="dbb56-148">이 예제에서는 Elmah 로그 파일을 저장할 수 없게 된 이유 비교적 명확 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb56-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="dbb56-149">IIS 추적을 사용 하 여 문제의 원인을 명확; 있지 않은 경우 참조 [문제 해결 실패 한 요청 추적 사용 IIS 7에서](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) IIS.net 사이트의.</span><span class="sxs-lookup"><span data-stu-id="dbb56-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="dbb56-150">응용 프로그램 풀 id에 사용 권한을 부여 하는 방법에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 풀 Id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) 하 고 [파일 시스템 Acl을 통해 IIS에서 콘텐츠 보호](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) IIS.net 사이트의.</span><span class="sxs-lookup"><span data-stu-id="dbb56-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dbb56-151">[이전](deploying-to-iis.md)
> [다음](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="dbb56-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>
