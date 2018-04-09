---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 사용 권한 설정 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 7efe267975835e889950983126088f1b637c28fb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="93379-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="93379-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>
====================
<span data-ttu-id="93379-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="93379-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="93379-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="93379-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="93379-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="93379-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="93379-107">계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="93379-108">개요</span><span class="sxs-lookup"><span data-stu-id="93379-108">Overview</span></span>

<span data-ttu-id="93379-109">에 대 한 폴더 사용 권한을 설정 하면이 자습서는 *Elmah* 폴더에 배포 된 웹 사이트 응용 프로그램 해당 폴더에 로그 파일을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="93379-110">Visual Studio 개발 서버 (Cassini) 또는 IIS Express를 사용 하 여 Visual Studio에서 웹 응용 프로그램을 테스트할 때 응용 프로그램 id에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93379-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="93379-111">개발 컴퓨터의 관리자는 거의 하 고 모든 폴더에 모든 파일에 아무 것도 할 수 있는 전체 권한을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="93379-112">하지만 사이트에 할당 된 응용 프로그램 풀에 대해 정의 된 id에서 실행 하는 응용 프로그램에서 IIS를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="93379-113">이것은 일반적으로 제한 된 권한을 가진 시스템 정의 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="93379-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="93379-114">기본적으로 읽기와 웹 응용 프로그램의 파일 및 폴더에 대 한 실행 하지만 쓰기 권한이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="93379-115">응용 프로그램을 만들거나는 공통 업데이트 파일을 웹 응용 프로그램에서 필요 하는 경우에 문제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93379-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="93379-116">Elmah Contoso 대학 응용 프로그램에서의 XML 파일을 만듭니다는 *Elmah* 오류에 대 한 세부 정보를 저장 하려면 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="93379-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="93379-117">다음과 같이 Elmah를 사용 하지 않는 경우에 사이트 파일을 업로드 하거나 사이트의 폴더에 데이터를 쓰는 다른 작업을 수행 하는 사용자를 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="93379-118">미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="93379-119">테스트 오류 로깅 및 보고</span><span class="sxs-lookup"><span data-stu-id="93379-119">Test error logging and reporting</span></span>

<span data-ttu-id="93379-120">어떻게 표시 되는지 확인 응용 프로그램 하지 않는 올바르게 IIS에서 (했을 때 Visual Studio에서 테스트) 하지만, 일반적으로 Elmah로 로깅될 및 다음 세부 정보를 Elmah 오류 로그를 엽니다는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="93379-121">Elmah, XML 파일을 만들고 오류 세부 정보를 저장할 수 없는 경우 빈 오류 보고서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="93379-122">브라우저를 열고로 이동 `http://localhost/ContosoUniversity`, 후 같은 잘못 된 URL 요청 *Studentsxxx.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="93379-123">시스템에서 생성 된 오류 페이지가 대신 표시는 *GenericErrorPage.aspx* 때문에 페이지는 `customErrors` Web.config 파일에서 설정이 "RemoteOnly"이 고 IIS를 로컬로 실행:</span><span class="sxs-lookup"><span data-stu-id="93379-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![HTTP 404 오류 페이지](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="93379-125">이제 실행 *Elmah.axd* 오류 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="93379-126">관리자 계정 자격 증명으로 로그인 한 후 (&quot;admin&quot; 및 &quot;devpwd&quot;), Elmah XML 파일을 만들 수 없기 때문에 빈 오류 로그 페이지를 참조는 *Elmah*폴더:</span><span class="sxs-lookup"><span data-stu-id="93379-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![오류 로그 비어 있음](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="93379-128">Elmah 폴더에 대 한 쓰기 권한이 설정</span><span class="sxs-lookup"><span data-stu-id="93379-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="93379-129">폴더 사용 권한을 수동으로 설정 하거나는 자동 배포 프로세스 도중을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="93379-130">자동 만들기 복잡 한 MSBuild 코드 걸리며 처음 배포할 때가 작업을 수행 해야 하므로 다음 단계를 수동으로 수행 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="93379-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="93379-131">(배포 프로세스의이 부분을 확인 하는 방법에 대 한 정보를 참조 하십시오. [웹 게시에 대 한 폴더 권한을 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) Sayed Hashimi 블로그에서.)</span><span class="sxs-lookup"><span data-stu-id="93379-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="93379-132">**파일 탐색기**로 이동 *C:\inetpub\wwwroot\ContosoUniversity*합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="93379-133">마우스 오른쪽 단추로 클릭는 *Elmah* 폴더를 **속성**를 선택한 후는 **보안** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="93379-134">
              **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-134">Click **Edit**.</span></span>
3. <span data-ttu-id="93379-135">에 **Elmah에 대 한 권한을** 대화 상자에서 **DefaultAppPool**, 선택한 후는 **쓰기** 확인란에는 **허용** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="93379-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![ELMAH 폴더에 대 한 사용 권한](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="93379-137">(표시 되지 않으면 **DefaultAppPool** 에 **그룹 또는 사용자 이름** 목록 것이 자습서에서는 지정 된 다른 방법을 하는 데 사용한 컴퓨터에서 IIS 및 ASP.NET 4를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="93379-138">이 경우 어떤 id가 Contoso 대학 응용 프로그램에 할당 된 응용 프로그램 풀에서 사용 하 고 해당 id로 쓰기 권한을 부여 봅니다.</span><span class="sxs-lookup"><span data-stu-id="93379-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="93379-139">링크를 참조 응용 프로그램 풀 id에 대 한이 자습서의 끝에.) 클릭 **확인** 두 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="93379-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="93379-140">오류 로깅 및 보고를 다시 테스트</span><span class="sxs-lookup"><span data-stu-id="93379-140">Retest error logging and reporting</span></span>

<span data-ttu-id="93379-141">같은 방식으로 (잘못 된 URL 요청) 오류가 다시 발생 하 여 테스트 하 고 실행 된 **오류 로그** 페이지.</span><span class="sxs-lookup"><span data-stu-id="93379-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="93379-142">이 오류는 페이지에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="93379-142">This time the error appears on the page.</span></span>

![ELMAH 오류 로그 페이지](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="93379-144">요약</span><span class="sxs-lookup"><span data-stu-id="93379-144">Summary</span></span>

<span data-ttu-id="93379-145">완료 했으므로 Contoso 대학 하는 데 필요한 작업을 모두 로컬 컴퓨터에서 IIS에서 올바르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="93379-146">다음 자습서에서 생성 됩니다 사이트 공개적으로 사용할 수 있는 Azure에 배포 하 여.</span><span class="sxs-lookup"><span data-stu-id="93379-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="93379-147">추가 정보</span><span class="sxs-lookup"><span data-stu-id="93379-147">More information</span></span>

<span data-ttu-id="93379-148">이 예제에서는 Elmah 로그 파일을 저장할 수 없게 된 이유 상당히 당연 합니다.</span><span class="sxs-lookup"><span data-stu-id="93379-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="93379-149">IIS 추적을 사용 하 여 문제의 원인을; 명확 하지 않은 경우 참조 [문제 해결 실패 한 요청을 사용 하 여 추적 IIS 7에서](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) IIS.net 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="93379-150">응용 프로그램 풀 id에 권한을 부여 하는 방법에 대 한 자세한 내용은 참조 [응용 프로그램 풀 Id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) 및 [콘텐츠 파일 시스템 Acl을 통해 IIS에서 Secure](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) IIS.net 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93379-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="93379-151">[이전](deploying-to-iis.md)
> [다음](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="93379-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>
