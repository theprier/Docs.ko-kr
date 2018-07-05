---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: 4d8a7d2a6faa0b03fff4416778101b47df2dd26e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371767"
---
<a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a><span data-ttu-id="77ddc-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환</span><span class="sxs-lookup"><span data-stu-id="77ddc-103">ASP.NET Web Deployment using Visual Studio: Web.config File Transformations</span></span>
====================
<span data-ttu-id="77ddc-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="77ddc-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="77ddc-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="77ddc-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="77ddc-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="77ddc-107">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="77ddc-108">개요</span><span class="sxs-lookup"><span data-stu-id="77ddc-108">Overview</span></span>

<span data-ttu-id="77ddc-109">이 자습서에서는 변경 프로세스를 자동화 하는 방법을 보여 줍니다 합니다 *Web.config* 다른 대상 환경에 배포할 때 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-109">This tutorial shows you how to automate the process of changing the *Web.config* file when you deploy it to different destination environments.</span></span> <span data-ttu-id="77ddc-110">대부분의 응용 프로그램 설정에는 *Web.config* 응용 프로그램을 배포할 때 달라 야 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-110">Most applications have settings in the *Web.config* file that must be different when the application is deployed.</span></span> <span data-ttu-id="77ddc-111">이러한 변경을 수행한 프로세스를 자동화 하는 상당히 지루한 작업 및 오류가 발생 하기 쉽습니다 배포할 때마다 수동으로 수행 하지 않아도 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-111">Automating the process of making these changes keeps you from having to do them manually every time you deploy, which would be tedious and error prone.</span></span>

<span data-ttu-id="77ddc-112">미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a><span data-ttu-id="77ddc-113">웹 배포 매개 변수 및 Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="77ddc-113">Web.config transformations versus Web Deploy parameters</span></span>

<span data-ttu-id="77ddc-114">변경 하는 프로세스를 자동화 하는 방법은 두 가지가 *Web.config* 파일 설정: [Web.config 변환](https://msdn.microsoft.com/library/dd465326.aspx) 하 고 [웹 배포 매개 변수](https://msdn.microsoft.com/library/ff398068.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-114">There are two ways to automate the process of changing *Web.config* file settings: [Web.config transformations](https://msdn.microsoft.com/library/dd465326.aspx) and [Web Deploy parameters](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="77ddc-115">A *Web.config* 변환 파일을 변경 하는 방법을 지정 하는 XML 태그를 포함 합니다 *Web.config* 배포 될 때 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-115">A *Web.config* transformation file contains XML markup that specifies how to change the *Web.config* file when it is deployed.</span></span> <span data-ttu-id="77ddc-116">특정 다른 변경 내용을 빌드 구성 및 특정 게시 프로필을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-116">You can specify different changes for specific build configurations and for specific publish profiles.</span></span> <span data-ttu-id="77ddc-117">기본 빌드 구성이 디버그 및 릴리스, 되며 사용자 지정 빌드 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-117">The default build configurations are Debug and Release, and you can create custom build configurations.</span></span> <span data-ttu-id="77ddc-118">게시 프로필은 일반적으로 대상 환경에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-118">A publish profile typically corresponds to a destination environment.</span></span> <span data-ttu-id="77ddc-119">(자세히 게시 프로필에 배웁니다 합니다 [IIS 테스트 환경으로 배포](deploying-to-iis.md) 자습서입니다.)</span><span class="sxs-lookup"><span data-stu-id="77ddc-119">(You'll learn more about publish profiles in the [Deploying to IIS as a Test Environment](deploying-to-iis.md) tutorial.)</span></span>

<span data-ttu-id="77ddc-120">다양 한 종류의에서 발견 되는 설정을 비롯 하 여 배포 하는 동안 구성 해야 하는 설정 지정 하려면 웹 배포 매개 변수를 사용할 수 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-120">Web Deploy parameters can be used to specify many different kinds of settings that must be configured during deployment, including settings that are found in *Web.config* files.</span></span> <span data-ttu-id="77ddc-121">지정 하는 데 사용 하는 경우 *Web.config* 파일 변경 내용이 웹 배포 매개 변수는 설정 하기가 더 복잡 하지만 배포할 때까지 설정 값을 알 수 없는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-121">When used to specify *Web.config* file changes, Web Deploy parameters are more complex to set up, but they are useful when you do not know the value to be set until you deploy.</span></span> <span data-ttu-id="77ddc-122">예를 들어, 엔터프라이즈 환경에서 만들 수 있습니다는 *배포 패키지* 프로덕션 환경에서 설치 하려면 IT 부서에서 사용자에 게 제공 하 고 해당 사용자를 연결 문자열 또는 하지 암호를 입력할 수 해야 합니다. 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-122">For example, in an enterprise environment, you might create a *deployment package* and give it to a person in the IT department to install in production, and that person has to be able to enter connection strings or passwords that you do not know.</span></span>

<span data-ttu-id="77ddc-123">이 자습서 시리즈에 설명 하는 시나리오의 경우 사전에 알고를 수행 하는 모든 항목을 *Web.config* 파일 이기 때문에 웹 배포 매개 변수를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-123">For the scenario that this tutorial series covers, you know in advance everything that has to be done to the *Web.config* file, so you do not need to use Web Deploy parameters.</span></span> <span data-ttu-id="77ddc-124">를 사용 하는 빌드 구성에 따라 다른 및 사용 하는 게시 프로필에 따라 다른 일부는 몇 가지 변환을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-124">You'll configure some transformations that differ depending on the build configuration used, and some that differ depending on the publish profile used.</span></span>

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a><span data-ttu-id="77ddc-125">Azure에서 Web.config 설정 지정</span><span class="sxs-lookup"><span data-stu-id="77ddc-125">Specifying Web.config settings in Azure</span></span>

<span data-ttu-id="77ddc-126">경우는 *Web.config* 변경 하려면 원하는 파일 설정에는 `<connectionStrings>` 또는 `<appSettings>` 요소를 자동화 하는 동안 변경 내용에 대 한 다른 옵션이 Azure App Service에서 Web Apps에 배포 하는 경우 및 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-126">If the *Web.config* file settings that you want to change are in the `<connectionStrings>` or the `<appSettings>` element, and if you are deploying to Web Apps in Azure App Service, you have another option for automating changes during deployment.</span></span> <span data-ttu-id="77ddc-127">Azure에서 적용 하려는 설정을 입력할 수는 **구성** 웹 앱에 대 한 관리 포털 페이지의 탭 (아래로 스크롤하여는 **앱 설정** 및 **연결 문자열**  섹션).</span><span class="sxs-lookup"><span data-stu-id="77ddc-127">You can enter the settings that you want to take effect in Azure in the **Configure** tab of the management portal page for your web app (scroll down to the **app settings** and **connection strings** sections).</span></span> <span data-ttu-id="77ddc-128">프로젝트를 배포할 때 Azure는 자동으로 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-128">When you deploy the project, Azure automatically applies the changes.</span></span> <span data-ttu-id="77ddc-129">자세한 내용은 [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-129">For more information, see [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

## <a name="default-transformation-files"></a><span data-ttu-id="77ddc-130">기본 변환 파일</span><span class="sxs-lookup"><span data-stu-id="77ddc-130">Default transformation files</span></span>

<span data-ttu-id="77ddc-131">**솔루션 탐색기**, 확장 *Web.config* 보려는 합니다 *Web.Debug.config* 하 고 *Web.Release.config* 변환 파일을 두 개의 기본 빌드 구성에 대해 기본적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-131">In **Solution Explorer**, expand *Web.config* to see the *Web.Debug.config* and *Web.Release.config* transformation files that are created by default for the two default build configurations.</span></span>

![Web.config_transform_files](web-config-transformations/_static/image1.png)

<span data-ttu-id="77ddc-133">Web.config 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 사용자 지정 빌드 구성에 대 한 변환 파일을 만들 수 있습니다 **Config 변환 추가** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-133">You can create transformation files for custom build configurations by right-clicking the Web.config file and choosing **Add Config Transforms** from the context menu.</span></span> <span data-ttu-id="77ddc-134">이 자습서를 수행할 필요가 없습니다 및 메뉴 옵션을 사용 하지 않으면 모든 사용자 지정 빌드 구성을 만들지 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-134">For this tutorial you don't need to do that, and the menu option is disabled, because you haven't created any custom build configurations.</span></span>

<span data-ttu-id="77ddc-135">나중을 만든 세 가지 자세한 변환 파일을 각각 테스트에 대 한 스테이징 및 프로덕션 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="77ddc-135">Later you'll create three more transformation files, one each for the test, staging, and production publish profiles.</span></span> <span data-ttu-id="77ddc-136">대상 환경에 종속 되므로 게시 프로필 변환 파일에서 처리할 수 있습니다 하는 설정의 일반적인 예는 테스트 또는 프로덕션에 대 한 다른 WCF 끝점.</span><span class="sxs-lookup"><span data-stu-id="77ddc-136">A typical example of a setting that you would handle in a publish profile transformation file because it depends on the destination environment is a WCF endpoint that is different for test versus production.</span></span> <span data-ttu-id="77ddc-137">만든 게시 프로필 변환 파일 나중에 자습서에서 사용 하 여 이동 하는 게시 프로필을 만든 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-137">You'll create publish profile transformation files in later tutorials after you create the publish profiles that they go with.</span></span>

## <a name="disable-debug-mode"></a><span data-ttu-id="77ddc-138">디버그 모드를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="77ddc-138">Disable debug mode</span></span>

<span data-ttu-id="77ddc-139">대상 환경은 대신 빌드 구성에 따라 달라 지는 설정의 예로 `debug` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-139">An example of a setting that depends on build configuration rather than destination environment is the `debug` attribute.</span></span> <span data-ttu-id="77ddc-140">릴리스 빌드의 경우 일반적으로 원하는 디버깅 사용 안 함에 배포 되는 환경에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-140">For a Release build, you typically want debugging disabled regardless of which environment you are deploying to.</span></span> <span data-ttu-id="77ddc-141">따라서 기본적으로 Visual Studio 프로젝트 템플릿 만들기 *Web.Release.config* 를 제거 하는 코드를 사용 하 여 파일을 변환 합니다 `debug` 에서 특성을 `compilation` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-141">Therefore, by default the Visual Studio project templates create *Web.Release.config* transform files with code that removes the `debug` attribute from the `compilation` element.</span></span> <span data-ttu-id="77ddc-142">기본 다음과 같습니다 *Web.Release.config*: 코드에서 주석으로 처리 되는 몇 가지 샘플 변환 코드 외에도 포함 합니다 `compilation` 요소를 제거 하는 `debug` 특성:</span><span class="sxs-lookup"><span data-stu-id="77ddc-142">Here is the default *Web.Release.config*: in addition to some sample transformation code that is commented out, it includes code in the `compilation` element that removes the `debug` attribute:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

<span data-ttu-id="77ddc-143">`xdt:Transform="RemoveAttributes(debug)"` 특성 것임을 지정 합니다 `debug` 에서 제거할 특성을 `system.web/compilation` 배포에서 요소 *Web.config* 파일.</span><span class="sxs-lookup"><span data-stu-id="77ddc-143">The `xdt:Transform="RemoveAttributes(debug)"` attribute specifies that you want the `debug` attribute to be removed from the `system.web/compilation` element in the deployed *Web.config* file.</span></span> <span data-ttu-id="77ddc-144">이 릴리스 빌드를 배포할 때마다 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-144">This will be done every time you deploy a Release build.</span></span>

## <a name="limit-error-log-access-to-administrators"></a><span data-ttu-id="77ddc-145">관리자에 게 오류 로그 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-145">Limit error log access to administrators</span></span>

<span data-ttu-id="77ddc-146">응용 프로그램을 실행 하는 동안 오류가 발생 하는 응용 프로그램 오류 시스템에서 생성 된 페이지 대신 일반 오류 페이지를 표시 하 고 사용 하는 경우는 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 오류 로깅 및 보고에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-146">If there's an error while the application runs, the application displays a generic error page in place of the system-generated error page, and it uses the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) for error logging and reporting.</span></span> <span data-ttu-id="77ddc-147">합니다 `customErrors` 응용 프로그램에서 요소 *Web.config* 오류 페이지를 지정 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="77ddc-147">The `customErrors` element in the application *Web.config* file specifies the error page:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

<span data-ttu-id="77ddc-148">오류 페이지를 보려면 일시적으로 변경 합니다 `mode` 특성은 `customErrors` "RemoteOnly"를 "On" 및 Visual Studio에서 응용 프로그램을 실행 하는 요소.</span><span class="sxs-lookup"><span data-stu-id="77ddc-148">To see the error page, temporarily change the `mode` attribute of the `customErrors` element from "RemoteOnly" to "On" and run the application from Visual Studio.</span></span> <span data-ttu-id="77ddc-149">와 같은 잘못 된 URL을 요청 하 여 오류를 발생 시킬 *Studentsxxx.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-149">Cause an error by requesting an invalid URL, such as *Studentsxxx.aspx*.</span></span> <span data-ttu-id="77ddc-150">IIS에서 생성 된 "리소스를 찾을 수 없습니다" 오류 대신 페이지를 표시 합니다 *GenericErrorPage.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-150">Instead of an IIS-generated "The resource cannot be found" error page, you see the *GenericErrorPage.aspx* page.</span></span>

![오류 페이지](web-config-transformations/_static/image2.png)

<span data-ttu-id="77ddc-152">오류 로그를 보려면 대체 URL에 사용 하 여 포트 번호 뒤 *elmah.axd* (예를 들어 `http://localhost:51130/elmah.axd`) Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-152">To see the error log, replace everything in the URL after the port number with *elmah.axd* (for example, `http://localhost:51130/elmah.axd`) and press Enter:</span></span>

![ELMAH 페이지](web-config-transformations/_static/image3.png)

<span data-ttu-id="77ddc-154">로 설정 해야 합니다 `customErrors` "RemoteOnly" 모드로 완료 되 면 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-154">Don't forget to set the `customErrors` element back to "RemoteOnly" mode when you're done.</span></span>

<span data-ttu-id="77ddc-155">개발 컴퓨터에 보안 위험이 있는 프로덕션 환경에서 오류 로그 페이지에 무료로 액세스할 수 있도록 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-155">On your development computer it's convenient to allow free access to the error log page, but in production that would be a security risk.</span></span> <span data-ttu-id="77ddc-156">관리자에 게 오류 로그 액세스를 제한 하는 권한 부여 규칙을 추가 하 고 제한 하면 작동 하는지 확인 하려는 프로덕션 사이트에 대 한 테스트 및 스테이징도에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-156">For the production site, you want to add an authorization rule that restricts error log access to administrators, and to make sure that the restriction works you want it in test and staging also.</span></span> <span data-ttu-id="77ddc-157">따라서이 릴리스 빌드를 배포할 때마다 및에 속해 있으므로 구현 하려는 또 다른 변화가 합니다 *Web.Release.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-157">Therefore this is another change that you want to implement every time you deploy a Release build, and so it belongs in the *Web.Release.config* file.</span></span>

<span data-ttu-id="77ddc-158">열기 *Web.Release.config* 새 추가한 `location` 닫기 직전 요소 `configuration` 태그를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-158">Open *Web.Release.config* and add a new `location` element immediately before the closing `configuration` tag, as shown here.</span></span>

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

<span data-ttu-id="77ddc-159">`Transform` 특성 값이 "Insert" 이면이 `location` 기존에 형제로 추가할 요소 `location` 요소에는 *Web.config* 파일.</span><span class="sxs-lookup"><span data-stu-id="77ddc-159">The `Transform` attribute value of "Insert" causes this `location` element to be added as a sibling to any existing `location` elements in the *Web.config* file.</span></span> <span data-ttu-id="77ddc-160">(이미 하나 `location` 권한 부여를 지정 하는 요소에 대 한 규칙은 **업데이트 크레딧** 페이지입니다.)</span><span class="sxs-lookup"><span data-stu-id="77ddc-160">(There is already one `location` element that specifies authorization rules for the **Update Credits** page.)</span></span>

<span data-ttu-id="77ddc-161">이제는 하이 올바르게 코딩 되도록 변환을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-161">Now you can preview the transform to make sure that you coded it correctly.</span></span>

<span data-ttu-id="77ddc-162">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Web.Release.config* 클릭 **Preview 변환**합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-162">In **Solution Explorer**, right-click *Web.Release.config* and click **Preview Transform**.</span></span>

![변환 메뉴 미리 보기](web-config-transformations/_static/image4.png)

<span data-ttu-id="77ddc-164">개발 보여 주는 페이지가 열립니다 *Web.config* 파일 및를 왼쪽에 배포 된 *Web.config* 파일 보이는지 오른쪽의 변경 내용을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-164">A page opens that shows you the development *Web.config* file on the left and what the deployed *Web.config* file will look like on the right, with changes highlighted.</span></span>

![디버그 변환의 미리 보기](web-config-transformations/_static/image5.png)

![위치 변환의 미리 보기](web-config-transformations/_static/image6.png)

<span data-ttu-id="77ddc-167">(미리 보기에서 알 수 있듯이 직접 작성 하지 않은 일부 추가 변경 사항에 대 한 변환: 일반적으로 관련 되어 이러한 기능에 영향을 주지는 공백을 제거 합니다.)</span><span class="sxs-lookup"><span data-stu-id="77ddc-167">( In the preview, you might notice some additional changes that you didn't write transforms for: these typically involve the removal of white space that doesn't affect functionality.)</span></span>

<span data-ttu-id="77ddc-168">배포 후 사이트를 테스트 하는 경우 권한 부여 규칙을이 유효한 지 확인도 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-168">When you test the site after deployment, you'll also test to verify that the authorization rule is effective.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="77ddc-169">**보안 정보** 프로덕션 응용 프로그램에서 public에 오류 세부 정보를 표시 하거나 공용 위치에 해당 정보를 저장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-169">**Security Note** Never display error details to the public in a production application, or store that information in a public location.</span></span> <span data-ttu-id="77ddc-170">공격자는 오류 정보를 사용 하 여 취약점으로 인 한 사이트를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-170">Attackers can use error information to discover vulnerabilities in a site.</span></span> <span data-ttu-id="77ddc-171">사용자 고유의 응용 프로그램에서 ELMAH를 사용 하는 경우 보안 위험을 최소화 하기 위해 ELMAH를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-171">If you use ELMAH in your own application, configure ELMAH to minimize security risks.</span></span> <span data-ttu-id="77ddc-172">이 자습서에서 ELMAH 예제 간주 되지 않아야 권장된 구성.</span><span class="sxs-lookup"><span data-stu-id="77ddc-172">The ELMAH example in this tutorial should not be considered a recommended configuration.</span></span> <span data-ttu-id="77ddc-173">예제 응용 프로그램에서 파일을 만들 수 있어야 하는 폴더를 처리 하는 방법을 보여 주기 위해 선택 된 경우</span><span class="sxs-lookup"><span data-stu-id="77ddc-173">It is an example that was chosen in order to illustrate how to handle a folder that the application must be able to create files in.</span></span> <span data-ttu-id="77ddc-174">자세한 내용은 [ELMAH 끝점을 보호](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-174">For more information, see [securing the ELMAH endpoint](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).</span></span>


## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a><span data-ttu-id="77ddc-175">처리할 수 있는 설정을 게시 프로필 변환 파일</span><span class="sxs-lookup"><span data-stu-id="77ddc-175">A setting that you'll handle in publish profile transformation files</span></span>

<span data-ttu-id="77ddc-176">일반적인 시나리오는 *Web.config* 파일에 배포 하는 각 환경에서 다 수 있어야 하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-176">A common scenario is to have *Web.config* file settings that must be different in each environment that you deploy to.</span></span> <span data-ttu-id="77ddc-177">예를 들어, WCF 서비스를 호출 하는 응용 프로그램 테스트 및 프로덕션 환경에서 다른 끝점을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-177">For example, an application that calls a WCF service might need a different endpoint in test and production environments.</span></span> <span data-ttu-id="77ddc-178">Contoso University 응용 프로그램에 이러한 종류의 설정도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-178">The Contoso University application includes a setting of this kind also.</span></span> <span data-ttu-id="77ddc-179">이 설정은 사이트의 페이지에는 사용자의 환경, 개발, 테스트 또는 프로덕션 같은 알려 주는 표시기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-179">This setting controls a visible indicator on a site's pages that tells you which environment you are in, such as development, test, or production.</span></span> <span data-ttu-id="77ddc-180">설정 값은 응용 프로그램 "(Dev)"를 추가 되 고 있는지 여부를 결정 하거나 "(테스트)"의 기본 제목을 합니다 *Site.Master* 마스터 페이지:</span><span class="sxs-lookup"><span data-stu-id="77ddc-180">The setting value determines whether the application will append "(Dev)" or "(Test)" to the main heading in the *Site.Master* master page:</span></span>

![환경 표시기](web-config-transformations/_static/image7.png)

<span data-ttu-id="77ddc-182">응용 프로그램 스테이징 또는 프로덕션에서 실행 중인 경우 환경 표시기는 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-182">The environment indicator is omitted when the application is running in staging or production.</span></span>

<span data-ttu-id="77ddc-183">Contoso University 웹 페이지에 설정 된 값을 읽을 `appSettings` 에 *Web.config* 어떤 환경에서 실행 중인 응용 프로그램을 확인 하기 위해 파일:</span><span class="sxs-lookup"><span data-stu-id="77ddc-183">The Contoso University web pages read a value that is set in `appSettings` in the *Web.config* file in order to determine what environment the application is running in:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

<span data-ttu-id="77ddc-184">값 "Test" 테스트 환경에 있고 "Prod" 스테이징 및 프로덕션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-184">The value should be "Test" in the test environment, and "Prod" for staging and production.</span></span>

<span data-ttu-id="77ddc-185">변환 파일에서 다음 코드는이 변환을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-185">The following code in a transform file will implement this transformation:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

<span data-ttu-id="77ddc-186">합니다 `xdt:Transform` 특성 값이이 변환의 용도에 기존 요소의 특성 값을 변경 하는 "SetAttributes" 나타냅니다는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-186">The `xdt:Transform` attribute value "SetAttributes" indicates that the purpose of this transform is to change attribute values of an existing element in the *Web.config* file.</span></span> <span data-ttu-id="77ddc-187">합니다 `xdt:Locator` 특성 값 "Match(key)" 수정할 요소를 하나 임을 나타냅니다입니다 `key` 일치 특성을 `key` 여기에 지정 된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-187">The `xdt:Locator` attribute value "Match(key)" indicates that the element to be modified is the one whose `key` attribute matches the `key` attribute specified here.</span></span> <span data-ttu-id="77ddc-188">만 다른 특성의는 `add` 요소는 `value`, 변경 될 사항 되며 배포에 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-188">The only other attribute of the `add` element is `value`, and that is what will be changed in the deployed *Web.config* file.</span></span> <span data-ttu-id="77ddc-189">하면 여기에 나온 코드는 `value` 특성을 `Environment` `appSettings` "Test"로 설정 되는 요소는 *Web.config* 배포 되는 파일.</span><span class="sxs-lookup"><span data-stu-id="77ddc-189">The code shown here causes the `value` attribute of the `Environment` `appSettings` element to be set to "Test" in the *Web.config* file that is deployed.</span></span>

<span data-ttu-id="77ddc-190">이 변환을 게시 프로필 변환 파일을 아직 만들지 않은에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-190">This transform belongs in the publish profile transform files, which you haven't created yet.</span></span> <span data-ttu-id="77ddc-191">만들고 테스트, 스테이징 및 프로덕션 환경에 대 한 게시 프로필을 만들 때이 변경 내용을 구현 하는 변환 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-191">You'll create and update the transform files that implement this change when you create the publish profiles for the test, staging, and production environments.</span></span> <span data-ttu-id="77ddc-192">로그인 할 수 있습니다는 [IIS에 배포](deploying-to-iis.md) 하 고 [프로덕션 환경에 배포](deploying-to-production.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-192">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

> [!NOTE]
> <span data-ttu-id="77ddc-193">이 설정은 때문에 합니다 `<appSettings>` 요소인 해야 Azure App Service 참조에서 Web Apps에 배포 하는 경우 변환 지정 하기 위한 또 다른 방법은 [Azure에서 지정 하는 Web.config 설정을](#watransforms) 의 앞부분에 나오는 이 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-193">Because this setting is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Web Apps in Azure App Service See [Specifying Web.config settings in Azure](#watransforms) earlier in this topic.</span></span>


## <a name="setting-connection-strings"></a><span data-ttu-id="77ddc-194">연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="77ddc-194">Setting connection strings</span></span>

<span data-ttu-id="77ddc-195">기본 변환 파일에서 연결 문자열을 업데이트 하는 방법을 보여 주는 예제를 포함 되어 있지만 대부분의 경우에서 하지 필요가 설정 연결 문자열 변환 하기 위해 게시 프로필의 연결 문자열을 지정할 수 있으므로.</span><span class="sxs-lookup"><span data-stu-id="77ddc-195">Although the default transform file contains an example that shows how to update a connection string, in most cases you do not need to set up connection string transformations, because you can specify connection strings in the publish profile.</span></span> <span data-ttu-id="77ddc-196">로그인 할 수 있습니다는 [IIS에 배포](deploying-to-iis.md) 하 고 [프로덕션 환경에 배포](deploying-to-production.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-196">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

## <a name="summary"></a><span data-ttu-id="77ddc-197">요약</span><span class="sxs-lookup"><span data-stu-id="77ddc-197">Summary</span></span>

<span data-ttu-id="77ddc-198">수행할 수 있는 만큼 이제 *Web.config* 변환 전에 게시 프로필을 만들고 배포 된 Web.config 파일의 수는 미리 보기를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-198">You have now done as much as you can with *Web.config* transformations before you create the publish profiles, and you've seen a preview of what will be in the deployed Web.config file.</span></span>

![위치 변환의 미리 보기](web-config-transformations/_static/image8.png)

<span data-ttu-id="77ddc-200">다음 자습서에서는 프로젝트 속성을 설정 해야 하는 배포 설정 작업의 처리 있습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-200">In the following tutorial, you'll take care of deployment set-up tasks that require setting project properties.</span></span>

## <a name="more-information"></a><span data-ttu-id="77ddc-201">추가 정보</span><span class="sxs-lookup"><span data-stu-id="77ddc-201">More Information</span></span>

<span data-ttu-id="77ddc-202">이 자습서에서 다루는 항목에 대 한 자세한 내용은 참조 하세요. [배포 하는 동안 대상 web.config 또는 app.config 파일의 설정을 변경 하려면 Web.config를 사용 하 여 변환](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) 에 대 한 웹 배포 콘텐츠 맵 Visual Studio 및 ASP.NET입니다.</span><span class="sxs-lookup"><span data-stu-id="77ddc-202">For more information about topics covered by this tutorial, see [Using Web.config transformations to change settings in the destination Web.config file or app.config file during deployment](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77ddc-203">[이전](preparing-databases.md)
> [다음](project-properties.md)</span><span class="sxs-lookup"><span data-stu-id="77ddc-203">[Previous](preparing-databases.md)
[Next](project-properties.md)</span></span>
