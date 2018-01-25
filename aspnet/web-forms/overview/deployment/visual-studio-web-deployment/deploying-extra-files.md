---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 불필요 한 파일이 배포 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/23/2015
ms.topic: article
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: 46e18ba81c3db8bb04c5cb997bcc1607e4e38bae
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="7b387-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 그 외의 파일 배포</span><span class="sxs-lookup"><span data-stu-id="7b387-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>
====================
<span data-ttu-id="7b387-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7b387-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7b387-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="7b387-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="7b387-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="7b387-107">계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="7b387-108">개요</span><span class="sxs-lookup"><span data-stu-id="7b387-108">Overview</span></span>

<span data-ttu-id="7b387-109">이 자습서에는 Visual Studio 웹 게시 파이프라인 배포 중에 추가 작업을 수행 하려면 확장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="7b387-110">작업 대상 웹 사이트에 프로젝트 폴더에 없는 추가 파일을 복사 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="7b387-111">이 자습서에 대 한 하나의 추가 파일을 복사 합니다. *robots.txt*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="7b387-112">이 파일을 준비 속하지만 프로덕션에 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="7b387-113">[프로덕션 환경에 배포](deploying-to-production.md) tutorial 프로젝트에이 파일을 추가 하 고 프로덕션 구성 된 게시 프로필에는 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="7b387-114">이 자습서의 모든 파일을 배포 하려고 하지만 프로젝트에 포함 하지 않을 유용할 것이 상황을 처리 하는 대체 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="7b387-115">Robots.txt 파일 이동</span><span class="sxs-lookup"><span data-stu-id="7b387-115">Move the robots.txt file</span></span>

<span data-ttu-id="7b387-116">처리는 다른 방법에 대 한 준비 하려면 *robots.txt*, 자습서의이 섹션은 프로젝트에 포함 되지 않은 폴더에 파일 이동 및 삭제 하면 *robots.txt* 스테이징 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="7b387-117">해당 환경에 파일을 배포 하는의 새로운 메서드가 제대로 작동 하는지 확인할 수 있도록 준비에서 파일을 삭제 해야 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="7b387-118">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *robots.txt* 파일을 클릭 하 여 **프로젝트에서 제외**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="7b387-119">Windows 파일 탐색기를 사용 하 여 새 폴더를 솔루션 폴더에 만들고 이름을 *ExtraFiles*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="7b387-120">이동의 *robots.txt* 에서 파일을 *ContosoUniversity* 에 프로젝트 폴더는 *ExtraFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![ExtraFiles 폴더](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="7b387-122">FTP 도구를 사용 하 여 삭제 된 *robots.txt* 스테이징 웹 사이트에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="7b387-123">선택할 수 있습니다 **대상에서 추가 파일 제거** 아래 **파일 게시 옵션** 에 **설정을** 준비 게시 프로필을 탭 하 고 준비를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="7b387-124">업데이트 게시 프로필 파일</span><span class="sxs-lookup"><span data-stu-id="7b387-124">Update the publish profile file</span></span>

<span data-ttu-id="7b387-125">하기만 하면 *robots.txt* 를 배포 하기 위해 업데이트 해야 하는 유일한 게시 프로필은 준비 하도록 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="7b387-126">Visual Studio에서 열고 *Staging.pubxml*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="7b387-127">닫기 전에 파일의 끝에 `</Project>` 태그에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="7b387-128">이 코드에서는 새 *대상* 를 배포할 추가 파일을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="7b387-129">하나의 구성 됩니다는 MSBuild를 실행 하는 더 많은 작업 지정한 조건에 따라 또는.</span><span class="sxs-lookup"><span data-stu-id="7b387-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="7b387-130">`Include` 특성을 지정 파일을 찾을 수 있는 폴더 *ExtraFiles*프로젝트 폴더와 같은 수준에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="7b387-131">MSBuild는 해당 폴더와 하위 폴더 (이중 별표는 재귀 하위 폴더를 지정 하는 데 사용)로 재귀적으로에서 모든 파일을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="7b387-132">이 코드로 수 여러 파일 및 파일에에서 넣으면 포함 된 하위 폴더는 *ExtraFiles* 폴더 및 모든 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="7b387-133">`DestinationRelativePath` 요소 폴더와 파일 복사 되어야 함을 동일한 파일 및 폴더 구조에는 대상 웹 사이트의 루트 폴더에서 찾을 수는 지정 된 *ExtraFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="7b387-134">복사 하려는 경우는 *ExtraFiles* 폴더 자체는 `DestinationRelativePath` 번호 값은 *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="7b387-135">닫기 전에 파일의 끝에 `</Project>` 태그, 새 대상이 실행 하는 시기를 지정 하는 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="7b387-136">이 코드는 새 `CustomCollectFiles` 대상 대상 폴더에 파일을 복사 하는 대상을 실행 될 때마다 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="7b387-137">에 대 한 별도 대상 배포 패키지 만들기 및 게시 하 고 게시 하는 대신 배포 패키지를 사용 하 여 배포 하려는 경우 새 대상 대상을 모두에 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="7b387-138">*.pubxml* 파일은 이제 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="7b387-139">저장 하 고 닫습니다는 *Staging.pubxml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="7b387-140">스테이징에 게시</span><span class="sxs-lookup"><span data-stu-id="7b387-140">Publish to staging</span></span>

<span data-ttu-id="7b387-141">게시 한 번의 클릭을 사용 하 여 또는 명령줄 준비 프로필을 사용 하 여 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="7b387-142">한 번의 클릭을 사용 하는 경우 게시에서 확인할 수 있습니다는 **미리 보기** 창 있는 *robots.txt* 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="7b387-143">그렇지 않은 경우 FTP 도구를 사용 하 여 확인 하는 *robots.txt* 배포 후 파일은 웹 사이트의 루트 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="7b387-144">요약</span><span class="sxs-lookup"><span data-stu-id="7b387-144">Summary</span></span>

<span data-ttu-id="7b387-145">이 일련의 제 3 자 호스팅 공급자에 ASP.NET 웹 응용 프로그램 배포에 대 한 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="7b387-146">이 자습서에 포함 된 항목 중 하나에 대 한 자세한 내용은 참조는 [ASP.NET 배포 콘텐츠 맵](https://go.microsoft.com/fwlink/p/?LinkId=282413)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="7b387-147">추가 정보</span><span class="sxs-lookup"><span data-stu-id="7b387-147">More information</span></span>

<span data-ttu-id="7b387-148">MSBuild 파일을 사용 하는 방법을 알고 있는 경우에 코드를 작성 하 여 다른 많은 배포 작업을 자동화할 수 있습니다 *.pubxml* (프로필 관련 작업)에 대 한 파일 또는 프로젝트 *. wpp.targets* 파일 (하는 태스크 모든 프로필에 적용).</span><span class="sxs-lookup"><span data-stu-id="7b387-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="7b387-149">에 대 한 자세한 내용은 *.pubxml* 및 *. wpp.targets* 파일, 참조 [하는 방법: 게시 프로 파일 (.pubxml) 파일에서 배포 설정 편집 및. wpp.targets Visual Studio 웹에서 파일 프로젝트](https://msdn.microsoft.com/library/ff398069)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="7b387-150">MSBuild 코드에 대 한 기본적인 소개를 참조 하십시오. **프로젝트 파일의 분석** 에 [엔터프라이즈 배포 시리즈: 프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="7b387-151">를 고유한 시나리오에 대 한 작업을 수행 하는 MSBuild 파일을 사용 하는 방법을 확인 하려면이 가이드를 참조 하십시오.: [Microsoft Build Engine 안에: MSBuild를 사용 하 여 및 Team Foundation Build](http://msbuildbook.com) Sayed Ibraham Hashimi 및 William Bartholomew 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="7b387-152">감사의 글</span><span class="sxs-lookup"><span data-stu-id="7b387-152">Acknowledgements</span></span>

<span data-ttu-id="7b387-153">이 자습서 시리즈의 내용에 중요 한 기여를 수행한 다음 사람에 게 감사 하 고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="7b387-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="7b387-154">Alberto Poblacion, MVP &amp; MCT, 스페인</span><span class="sxs-lookup"><span data-stu-id="7b387-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="7b387-155">Jarod 퍼거슨, 데이터 플랫폼 개발 MVP United States</span><span class="sxs-lookup"><span data-stu-id="7b387-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="7b387-156">Harsh Mittal, Microsoft</span><span class="sxs-lookup"><span data-stu-id="7b387-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="7b387-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="7b387-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="7b387-158">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="7b387-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="7b387-159">Mike Pope, Microsoft</span><span class="sxs-lookup"><span data-stu-id="7b387-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="7b387-160">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="7b387-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="7b387-161">Raffaele Rialdi 이탈리아</span><span class="sxs-lookup"><span data-stu-id="7b387-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="7b387-162">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="7b387-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="7b387-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="7b387-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="7b387-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="7b387-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="7b387-165">[Scott 헌터, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="7b387-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="7b387-166">Srđan Božović, 세르비아</span><span class="sxs-lookup"><span data-stu-id="7b387-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="7b387-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="7b387-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="7b387-168">[이전](command-line-deployment.md)
[다음](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="7b387-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>
