---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 특정 빌드 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 패키지 및 특정 이전 빌드에서를 스테이징 또는 프로덕션은 순서도 같은 새 대상 데이터베이스 스크립트를 배포 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: e788f02795fc83ac98c5a0ba307f16b0f506e489
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828870"
---
<a name="deploying-a-specific-build"></a><span data-ttu-id="d9920-103">특정 빌드 배포</span><span class="sxs-lookup"><span data-stu-id="d9920-103">Deploying a Specific Build</span></span>
====================
<span data-ttu-id="d9920-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="d9920-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="d9920-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="d9920-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="d9920-106">이 항목에서는 특정 이전 빌드에서 스테이징 또는 프로덕션 환경이 새 대상 데이터베이스 스크립트 및 웹 패키지를 배포 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-106">This topic describes how to deploy web packages and database scripts from a specific previous build to a new destination, like a staging or production environment.</span></span>


<span data-ttu-id="d9920-107">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="d9920-108">이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 및 배포 프로세스에 의해 제어 되는&#x2014;하나 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 빌드 명령이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="d9920-109">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="d9920-110">작업 개요</span><span class="sxs-lookup"><span data-stu-id="d9920-110">Task Overview</span></span>

<span data-ttu-id="d9920-111">지금까지이 자습서 집합의 항목에서는 빌드, 패키지 및 단일 단계의 일부로 웹 응용 프로그램 및 데이터베이스를 배포 하는 방법에 초점을 맞춘 했거나 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-111">Until now, the topics in this tutorial set have focused on how to build, package, and deploy web applications and databases as part of a single-step or automated process.</span></span> <span data-ttu-id="d9920-112">그러나 몇 가지 일반적인 시나리오에서 하려는 빌드 저장 폴더의 목록에서 배포 하는 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-112">However, in some common scenarios, you'll want to select the resources that you deploy from a list of builds in a drop folder.</span></span> <span data-ttu-id="d9920-113">즉, 최신 빌드를 배포 하려면 빌드 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-113">In other words, the latest build may not be the build you want to deploy.</span></span>

<span data-ttu-id="d9920-114">이전 항목에서 설명 하는 CI (지속적인 통합) 시나리오를 고려해 야 [배포를 만드는 빌드 정의 지 원하는](creating-a-build-definition-that-supports-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-114">Consider the continuous integration (CI) scenario described in the previous topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="d9920-115">빌드 정을 Team Foundation Server (TFS) 2010에서 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-115">You've created a build definition in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="d9920-116">TFS에 코드를 확인 하는 개발자, 때마다 팀 빌드는 코드를 작성 하, 빌드 프로세스의 일부로 웹 패키지 및 데이터베이스 스크립트를 만드는, 모든 단위 테스트를 실행 및 테스트 환경에 리소스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-116">Every time a developer checks code into TFS, Team Build will build your code, create web packages and database scripts as part of the build process, run any unit tests, and deploy your resources to a test environment.</span></span> <span data-ttu-id="d9920-117">빌드 정의 생성 하는 경우 구성 된 보존 정책에 따라 TFS 특정 개수의 이전 빌드를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-117">Depending on the retention policy you configured when you created the build definition, TFS will retain a certain number of previous builds.</span></span>

![](deploying-a-specific-build/_static/image1.png)

<span data-ttu-id="d9920-118">이제 테스트 환경에서 빌드 유효성 검사 중에 대해 테스트 및 스테이징 환경에 응용 프로그램을 배포할 준비가 되었습니다. 확인을 수행 했습니다 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-118">Now, suppose you've performed verification and validation testing against one of these builds in your test environment, and you're ready to deploy your application to a staging environment.</span></span> <span data-ttu-id="d9920-119">한편 개발자는 새 코드에 체크 인 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-119">In the meantime, developers may have checked in new code.</span></span> <span data-ttu-id="d9920-120">솔루션 다시 빌드 및 스테이징 환경에 배포 하지 않 및 스테이징 환경에 최신 빌드를 배포 하지 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-120">You don't want to rebuild the solution and deploy to the staging environment, and you don't want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="d9920-121">대신, 확인 하 고 테스트 서버에서 유효성을 검사 하는 특정 빌드를 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-121">Instead, you want to deploy the specific build that you've verified and validated on the test servers.</span></span>

<span data-ttu-id="d9920-122">이를 위해 Microsoft Build Engine (MSBuild) 웹 패키지 및 데이터베이스 스크립트를 생성 하는 특정 빌드를 찾을 수 있는 위치를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-122">To accomplish this, you need to tell the Microsoft Build Engine (MSBuild) where to find the web packages and database scripts that a specific build generated.</span></span>

## <a name="overriding-the-outputroot-property"></a><span data-ttu-id="d9920-123">OutputRoot 속성을 재정의</span><span class="sxs-lookup"><span data-stu-id="d9920-123">Overriding the OutputRoot Property</span></span>

<span data-ttu-id="d9920-124">에 [샘플 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)의 *Publish.proj* 파일 이라는 속성을 선언 **OutputRoot**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-124">In the [sample solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), the *Publish.proj* file declares a property named **OutputRoot**.</span></span> <span data-ttu-id="d9920-125">이름에서 알 수 있듯이, 빌드 프로세스를 생성 하는 모든 항목이 포함 된 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-125">As the name suggests, this is the root folder that contains everything that the build process generates.</span></span> <span data-ttu-id="d9920-126">에 *Publish.proj* 파일을 볼 수 있습니다 하는 합니다 **OutputRoot** 속성 모든 배포 리소스에 대 한 루트 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-126">In the *Publish.proj* file, you can see that the **OutputRoot** property refers to the root location for all deployment resources.</span></span>

> [!NOTE]
> <span data-ttu-id="d9920-127">**OutputRoot** 자주 사용 되는 속성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-127">**OutputRoot** is a commonly used property name.</span></span> <span data-ttu-id="d9920-128">Visual C# 및 Visual Basic 프로젝트 파일 모든 빌드 출력에 대 한 루트 위치를 저장 하려면이 속성을 선언할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-128">Visual C# and Visual Basic project files also declare this property to store the root location for all build outputs.</span></span>


[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]


<span data-ttu-id="d9920-129">웹 패키지를 배포 하 고 데이터베이스의 다른 위치에서 스크립트를 프로젝트 파일을 원하는 경우&#x2014;이전 TFS 빌드 출력 같은&#x2014;를 재정의 해야 하는 **OutputRoot** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-129">If you want your project file to deploy web packages and database scripts from a different location&#x2014;like the outputs of a previous TFS build&#x2014;you simply need to override the **OutputRoot** property.</span></span> <span data-ttu-id="d9920-130">팀 빌드 서버에 관련 빌드 폴더에 속성 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-130">You should set the property value to the relevant build folder on the Team Build server.</span></span> <span data-ttu-id="d9920-131">명령줄에서 MSBuild를 실행 했던, 경우에 대 한 값을 지정할 수 있습니다 **OutputRoot** 명령줄 인수:</span><span class="sxs-lookup"><span data-stu-id="d9920-131">If you were running MSBuild from the command line, you could specify a value for **OutputRoot** as a command-line argument:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]


<span data-ttu-id="d9920-132">그러나 실제로는 또한 건너 뛰 려는 **빌드할** 대상&#x2014;빌드 출력을 사용할 계획이 없다면 솔루션을 빌드에 대 한 지점이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-132">In practice, however, you'd also want to skip the **Build** target&#x2014;there's no point in building your solution if you don't plan to use the build outputs.</span></span> <span data-ttu-id="d9920-133">명령줄에서 실행 하려는 대상을 지정 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-133">You could do this by specifying the targets you want to execute from the command line:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]


<span data-ttu-id="d9920-134">그러나 대부분의 경우 TFS 빌드 정의를 위한 배포 논리를 작성할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-134">However, in most cases, you'll want to build your deployment logic into a TFS build definition.</span></span> <span data-ttu-id="d9920-135">이 통해 사용 하 여 사용자를 **큐에 빌드 대기** TFS 서버에 대 한 연결을 사용 하 여 Visual Studio 설치에서 배포를 트리거할 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-135">This enables users with the **Queue builds** permission to trigger the deployment from any Visual Studio installation with a connection to the TFS server.</span></span>

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a><span data-ttu-id="d9920-136">빌드를 배포 하는 빌드 정의 특정 만들기</span><span class="sxs-lookup"><span data-stu-id="d9920-136">Creating a Build Definition to Deploy Specific Builds</span></span>

<span data-ttu-id="d9920-137">다음 절차를 사용 하면 단일 명령으로 스테이징 환경에 대 한 트리거 배포 하는 빌드 정의 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-137">The next procedure describes how to create a build definition that enables users to trigger deployments to a staging environment with a single command.</span></span>

<span data-ttu-id="d9920-138">이 경우 빌드 정의를 실제로 아무 것도 생성 하지 않으려면&#x2014;원하는 사용자 지정 프로젝트 파일의 배포 논리를 실행 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-138">In this case, you don't want the build definition to actually build anything&#x2014;you just want it to execute the deployment logic in your custom project file.</span></span> <span data-ttu-id="d9920-139">합니다 *Publish.proj* 건너뛰는 조건부 논리를 포함 하는 파일을 **빌드** Team Build에서 파일을 실행 하는 경우 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-139">The *Publish.proj* file includes conditional logic that skips the **Build** target if the file is running in Team Build.</span></span> <span data-ttu-id="d9920-140">기본 제공을 평가 하 여 이렇게 **BuildingInTeamBuild** 속성을 자동으로 설정 됩니다 **true** Team Build에서 프로젝트 파일을 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="d9920-140">It does this by evaluating the built-in **BuildingInTeamBuild** property, which is automatically set to **true** if you run your project file in Team Build.</span></span> <span data-ttu-id="d9920-141">결과적으로, 빌드 프로세스를 건너뛸 수 있으며 기존 빌드를 배포 하려면 프로젝트 파일을 실행 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-141">As a result, you can skip the build process and simply run the project file to deploy an existing build.</span></span>

<span data-ttu-id="d9920-142">**배포를 수동으로 트리거하려면 빌드 정의를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="d9920-142">**To create a build definition to trigger deployment manually**</span></span>

1. <span data-ttu-id="d9920-143">Visual Studio 2010에서에 **팀 탐색기** 창 팀 프로젝트 노드를 마우스 오른쪽 단추로 클릭 **빌드**, 클릭 하 고 **새 빌드 정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-143">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](deploying-a-specific-build/_static/image2.png)
2. <span data-ttu-id="d9920-144">에 **일반적인** 탭에서 빌드 정의 이름을 지정 (예를 들어 **DeployToStaging**) 및 선택적 설명을입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-144">On the **General** tab, give the build definition a name (for example, **DeployToStaging**) and an optional description.</span></span>
3. <span data-ttu-id="d9920-145">에 **트리거** 탭을 선택 **수동-체크 인 새 빌드를 트리거 하지 않는**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-145">On the **Trigger** tab, select **Manual – Check-ins do not trigger a new build**.</span></span>
4. <span data-ttu-id="d9920-146">에 **빌드 기본값** 탭을 **다음 저장 폴더에 빌드 출력 복사** 상자에 drop 폴더의 범용 명명 규칙 (UNC) 경로 입력 합니다 (예를 들어,  **\\TFSBUILD\Drops**).</span><span class="sxs-lookup"><span data-stu-id="d9920-146">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](deploying-a-specific-build/_static/image3.png)
5. <span data-ttu-id="d9920-147">에 **프로세스** 탭의 **빌드 프로세스 파일** 드롭다운 목록에서 유지 **DefaultTemplate.xaml** 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-147">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="d9920-148">모든 새 팀 프로젝트에 추가 하는 기본 빌드 프로세스 템플릿 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-148">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="d9920-149">**빌드 프로세스 매개 변수** 테이블을 클릭 합니다 **빌드할 항목** 행을 클릭 하 고는 **줄임표** 단추.</span><span class="sxs-lookup"><span data-stu-id="d9920-149">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](deploying-a-specific-build/_static/image4.png)
7. <span data-ttu-id="d9920-150">에 **빌드할 항목** 대화 상자, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-150">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="d9920-151">에 **형식의 항목** 드롭다운 목록에서 **MSBuild 프로젝트 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-151">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
9. <span data-ttu-id="d9920-152">있는 하면 배포 프로세스를 제어, 파일을 선택한 다음 사용자 지정 프로젝트 파일의 위치를 찾습니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-152">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](deploying-a-specific-build/_static/image5.png)
10. <span data-ttu-id="d9920-153">에 **빌드할 항목** 대화 상자, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-153">In the **Items to Build** dialog box, click **OK**.</span></span>
11. <span data-ttu-id="d9920-154">에 **빌드 프로세스 매개 변수** 테이블을 확장 합니다 **고급** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d9920-154">In the **Build process parameters** table, expand the **Advanced** section.</span></span>
12. <span data-ttu-id="d9920-155">에 **MSBuild 인수** 행 환경별 프로젝트 파일의 위치를 지정 하 고 빌드 폴더의 위치에 대 한 자리 표시자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-155">In the **MSBuild Arguments** row, specify the location of your environment-specific project file and add a placeholder for the location of your build folder:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="d9920-156">재정의 해야 합니다 **OutputRoot** 될 때마다 빌드를 큐에 대기 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-156">You'll need to override the **OutputRoot** value every time you queue a build.</span></span> <span data-ttu-id="d9920-157">다음 절차에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-157">This is covered in the next procedure.</span></span>
13. <span data-ttu-id="d9920-158">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-158">Click **Save**.</span></span>

<span data-ttu-id="d9920-159">빌드를 트리거할 때 업데이트 해야 합니다 **OutputRoot** 배포할 빌드를 가리키도록 속성.</span><span class="sxs-lookup"><span data-stu-id="d9920-159">When you trigger a build, you need to update the **OutputRoot** property to point to the build you want to deploy.</span></span>

<span data-ttu-id="d9920-160">**빌드 정의에서 특정 빌드를 배포 하려면**</span><span class="sxs-lookup"><span data-stu-id="d9920-160">**To deploy a specific build from a build definition**</span></span>

1. <span data-ttu-id="d9920-161">에 **팀 탐색기** 창에서 빌드 정의 마우스 오른쪽 단추로 클릭 **새 빌드 큐 대기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-161">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](deploying-a-specific-build/_static/image7.png)
2. <span data-ttu-id="d9920-162">에 **빌드 큐 대기** 대화 상자의 **매개 변수** 탭을 확장 합니다 **고급** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d9920-162">In the **Queue Build** dialog box, on the **Parameters** tab, expand the **Advanced** section.</span></span>
3. <span data-ttu-id="d9920-163">에 **MSBuild 인수** 행에서 값을 **OutputRoot** 빌드 폴더의 위치를 사용 하 여 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-163">In the **MSBuild Arguments** row, replace the value of the **OutputRoot** property with the location of your build folder.</span></span> <span data-ttu-id="d9920-164">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="d9920-164">For example:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="d9920-165">빌드 폴더 경로의 끝에 후행 슬래시를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-165">Be sure to include a trailing slash at the end of the path to your build folder.</span></span>
4. <span data-ttu-id="d9920-166">클릭 **큐**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-166">Click **Queue**.</span></span>

<span data-ttu-id="d9920-167">빌드를 큐, 프로젝트 파일을 데이터베이스 스크립트를 배포 및 빌드 저장 폴더에서 웹 패키지에서 지정한 경우는 **OutputRoot** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-167">When you queue the build, the project file will deploy the database scripts and web packages from the build drop folder you specified in the **OutputRoot** property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d9920-168">결론</span><span class="sxs-lookup"><span data-stu-id="d9920-168">Conclusion</span></span>

<span data-ttu-id="d9920-169">이 항목에서는 분할 프로젝트 파일의 배포 모델을 사용 하 여 이전 특정 빌드에서 웹 패키지 및 데이터베이스 스크립트와 같은 배포 리소스를 게시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-169">This topic described how to publish deployment resources, like web packages and database scripts, from a specific previous build using the split project file deployment model.</span></span> <span data-ttu-id="d9920-170">재정의 하는 방법을 설명 하는 **OutputRoot** 속성 및 TFS를 배포 논리를 통합 하는 방법에 대 한 빌드 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-170">It explained how to override the **OutputRoot** property and how to incorporate the deployment logic into a TFS build definition.</span></span>

## <a name="further-reading"></a><span data-ttu-id="d9920-171">추가 정보</span><span class="sxs-lookup"><span data-stu-id="d9920-171">Further Reading</span></span>

<span data-ttu-id="d9920-172">빌드 정의 만드는 방법에 대 한 자세한 내용은 참조 하세요. [기본 빌드 정의 만듭니다](https://msdn.microsoft.com/library/ms181716.aspx) 하 고 [빌드 프로세스 정의](https://msdn.microsoft.com/library/ms181715.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-172">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="d9920-173">큐 빌드에 대 한 자세한 지침을 참조 하세요 [큐에 빌드 대기](https://msdn.microsoft.com/library/ms181722.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9920-173">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d9920-174">[이전](creating-a-build-definition-that-supports-deployment.md)
> [다음](configuring-permissions-for-team-build-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="d9920-174">[Previous](creating-a-build-definition-that-supports-deployment.md)
[Next](configuring-permissions-for-team-build-deployment.md)</span></span>
