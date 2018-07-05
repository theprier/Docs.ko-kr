---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 배포 추가 파일 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/23/2015
ms.topic: article
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: 41bea625a53afbf7b39c03a2e8a92a03ce144289
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371822"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="84b6c-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: Extra Files 배포</span><span class="sxs-lookup"><span data-stu-id="84b6c-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>
====================
<span data-ttu-id="84b6c-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="84b6c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="84b6c-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="84b6c-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="84b6c-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="84b6c-107">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="84b6c-108">개요</span><span class="sxs-lookup"><span data-stu-id="84b6c-108">Overview</span></span>

<span data-ttu-id="84b6c-109">이 자습서에는 Visual Studio 웹 게시를 배포 하는 동안 추가 작업을 수행 하는 파이프라인을 확장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="84b6c-110">작업 대상 웹 사이트에 프로젝트 폴더에 없는 추가 파일을 복사 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="84b6c-111">이 자습서에 대 한 하나의 여분 파일 복사: *robots.txt*합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="84b6c-112">스테이징이 아니라 프로덕션이이 파일을 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="84b6c-113">[프로덕션에 배포](deploying-to-production.md) tutorial 프로젝트에이 파일을 추가 하 고 프로덕션에 구성 된 게시 프로필에는 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="84b6c-114">이 자습서에서 배포 하려고 하지만 프로젝트에 포함 하지 않으려는 모든 파일에 대 한 유용한 것이 상황을 처리 하는 다른 방법은 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="84b6c-115">Robots.txt 파일로 이동</span><span class="sxs-lookup"><span data-stu-id="84b6c-115">Move the robots.txt file</span></span>

<span data-ttu-id="84b6c-116">처리의 다른 메서드에 대 한 준비가 *robots.txt*, 자습서의이 섹션에서는 프로젝트에 포함 되지 않은 폴더에 파일 이동 및 삭제할 *robots.txt* 준비 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="84b6c-117">해당 환경에 파일을 배포 하는 새로운 메서드가 제대로 작동 하는지 확인할 수 있도록 준비에서 파일을 삭제 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="84b6c-118">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *robots.txt* 파일을 클릭 **프로젝트에서 제외**합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="84b6c-119">솔루션 폴더에 새 폴더를 만들 Windows 파일 탐색기를 사용 하 고 이름을 *ExtraFiles*합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="84b6c-120">이동는 *robots.txt* 에서 파일을 *ContosoUniversity* 프로젝트 폴더를 *ExtraFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![ExtraFiles 폴더](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="84b6c-122">FTP 도구를 사용 하 여 삭제 합니다 *robots.txt* 스테이징 웹 사이트에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="84b6c-123">선택할 수 있습니다 **대상에서 추가 파일 제거** 아래에서 **파일 게시 옵션** 에 **설정** 스테이징 게시 프로필의 탭 및 스테이징에 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="84b6c-124">게시 프로필 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="84b6c-124">Update the publish profile file</span></span>

<span data-ttu-id="84b6c-125">하기만 하면 *robots.txt* 스테이징 배포를 업데이트 해야 할 유일한 게시 프로필은 준비 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="84b6c-126">Visual Studio에서 엽니다 *Staging.pubxml*합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="84b6c-127">닫기 전에 파일의 끝 `</Project>` 태그, 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="84b6c-128">이 코드를 만듭니다 *대상* 는 배포할 추가 파일을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="84b6c-129">MSBuild를 실행 하는 더 많은 작업 기반 지정한 조건으로 또는 대상 하나 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="84b6c-130">합니다 `Include` 특성은 파일을 찾을 폴더 지정 *ExtraFiles*프로젝트 폴더와 동일한 수준에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="84b6c-131">MSBuild 해당 폴더를 재귀적으로 하위 폴더 (double 별표는 하위 폴더를 지정 하는 데 사용)에서 모든 파일을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="84b6c-132">이 코드를 사용 하 여 배치할 수 있습니다 여러 파일 및 파일 내의 하위 폴더에는 *ExtraFiles* 폴더 및 모든 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="84b6c-133">합니다 `DestinationRelativePath` 폴더 및 파일 복사 되어야 함을 동일한 파일 및 폴더 구조에서 대상 웹 사이트의 루트 폴더에 있는 대로 요소를 지정 합니다 *ExtraFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="84b6c-134">복사 하려는 경우는 *ExtraFiles* 자체 폴더를 `DestinationRelativePath` 값 *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)* 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="84b6c-135">닫기 전에 파일의 끝 `</Project>` 태그, 새 대상을 실행 하는 시기를 지정 하는 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="84b6c-136">이 코드를 사용 하면 새 `CustomCollectFiles` 대상 폴더로 파일을 복사 하는 대상 실행 될 때마다 실행 될 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="84b6c-137">별도 대상 배포 패키지 만들기 및 게시 하 고 게시 하는 대신 배포 패키지를 사용 하 여 배포 하려는 경우 새 대상 모두 대상으로 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="84b6c-138">합니다 *.pubxml* 파일은 이제 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="84b6c-139">저장 후 닫기 합니다 *Staging.pubxml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="84b6c-140">스테이징 게시</span><span class="sxs-lookup"><span data-stu-id="84b6c-140">Publish to staging</span></span>

<span data-ttu-id="84b6c-141">한 번의 클릭을 사용 하 여 게시 또는 명령줄 스테이징 프로필을 사용 하 여 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="84b6c-142">한 번의 클릭을 사용 하는 경우 게시에서 확인할 수 있습니다 합니다 **미리 보기** 창입니다 *robots.txt* 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="84b6c-143">이 고, 그렇지 FTP 도구를 사용 하 여 확인 합니다 *robots.txt* 배포 후 웹 사이트의 루트 폴더에 파일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="84b6c-144">요약</span><span class="sxs-lookup"><span data-stu-id="84b6c-144">Summary</span></span>

<span data-ttu-id="84b6c-145">이 타사 호스팅 공급자에 ASP.NET 웹 응용 프로그램에 대 한 자습서이 시리즈를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="84b6c-146">이 자습서에서 다루는 항목에 대 한 자세한 내용은 참조는 [ASP.NET 배포 콘텐츠 맵](https://go.microsoft.com/fwlink/p/?LinkId=282413)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="84b6c-147">추가 정보</span><span class="sxs-lookup"><span data-stu-id="84b6c-147">More information</span></span>

<span data-ttu-id="84b6c-148">MSBuild 파일을 사용 하는 방법의 이름을 알고 있는 경우에 코드를 작성 하 여 다른 많은 배포 작업을 자동화할 수 있습니다 *.pubxml* (프로필 관련 작업용) 파일 또는 프로젝트 *. wpp.targets* 파일 (태스크는 모든 프로필에 적용).</span><span class="sxs-lookup"><span data-stu-id="84b6c-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="84b6c-149">에 대 한 자세한 내용은 *.pubxml* 하 고 *. wpp.targets* 파일을 참조 하세요 [방법: 게시 프로필 (.pubxml) 파일에서 배포 설정을 편집 및. wpp.targets Visual Studio 웹에서 파일 프로젝트](https://msdn.microsoft.com/library/ff398069)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="84b6c-150">MSBuild 코드에 대 한 기본적인 소개를 참조 하세요 **프로젝트 파일의 분석** 에 [엔터프라이즈 배포 시리즈: 프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="84b6c-151">고유한 시나리오에 대 한 작업을 수행 하는 MSBuild 파일을 사용 하는 방법에 알아보려면이 설명서를 참조 하세요.: [Microsoft 빌드 엔진 내:를 사용 하 여 MSBuild 및 Team Foundation Build](http://msbuildbook.com) Sayed Ibraham Hashimi William Bartholomew 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="84b6c-152">감사의 글</span><span class="sxs-lookup"><span data-stu-id="84b6c-152">Acknowledgements</span></span>

<span data-ttu-id="84b6c-153">이 자습서 시리즈의 콘텐츠에 중요 한 기여를 수행한 다음 사용자를 감사 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b6c-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="84b6c-154">Alberto Poblacion, MVP &amp; MCT, 스페인</span><span class="sxs-lookup"><span data-stu-id="84b6c-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="84b6c-155">데이터 플랫폼 개발 MVP Jarod Ferguson United States</span><span class="sxs-lookup"><span data-stu-id="84b6c-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="84b6c-156">Harsh Mittal, Microsoft</span><span class="sxs-lookup"><span data-stu-id="84b6c-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="84b6c-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="84b6c-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="84b6c-158">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="84b6c-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="84b6c-159">Mike 되, Microsoft</span><span class="sxs-lookup"><span data-stu-id="84b6c-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="84b6c-160">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="84b6c-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="84b6c-161">Raffaele Rialdi 이탈리아</span><span class="sxs-lookup"><span data-stu-id="84b6c-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="84b6c-162">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="84b6c-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="84b6c-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="84b6c-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="84b6c-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="84b6c-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="84b6c-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="84b6c-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="84b6c-166">Srđan Božović, 세르비아</span><span class="sxs-lookup"><span data-stu-id="84b6c-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="84b6c-167">[인 Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="84b6c-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="84b6c-168">[이전](command-line-deployment.md)
> [다음](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="84b6c-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>
