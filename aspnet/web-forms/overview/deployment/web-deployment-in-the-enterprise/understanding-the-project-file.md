---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 프로젝트 파일 이해 | Microsoft Docs
author: jrjlee
description: Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심입니다. 이 항목에서는 MSBuild에 대 한 개념적인 개요를 시작 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 89c5c7906ccfc453195b788cbc6393dc74cda1fb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377206"
---
<a name="understanding-the-project-file"></a><span data-ttu-id="eb05b-104">프로젝트 파일 이해</span><span class="sxs-lookup"><span data-stu-id="eb05b-104">Understanding the Project File</span></span>
====================
<span data-ttu-id="eb05b-105">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="eb05b-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="eb05b-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="eb05b-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="eb05b-107">Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-107">Microsoft Build Engine (MSBuild) project files lie at the heart of the build and deployment process.</span></span> <span data-ttu-id="eb05b-108">이 항목에서는 프로젝트 파일과 MSBuild에 대 한 개념적인 개요를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-108">This topic starts with a conceptual overview of MSBuild and the project file.</span></span> <span data-ttu-id="eb05b-109">가로질러 프로젝트 파일을 사용 하 여 실제 응용 프로그램을 배포 하는 방법의 예제를 통해 작동 하 고 프로젝트 파일을 사용 하 여 작업할 때 주요 구성 요소를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-109">It describes the key components you'll come across when you work with project files, and it works through an example of how you can use project files to deploy real-world applications.</span></span>
> 
> <span data-ttu-id="eb05b-110">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="eb05b-110">What you'll learn:</span></span>
> 
> - <span data-ttu-id="eb05b-111">어떻게 MSBuild는 프로젝트를 빌드하려면 MSBuild 프로젝트 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-111">How MSBuild uses MSBuild project files to build projects.</span></span>
> - <span data-ttu-id="eb05b-112">어떻게 MSBuild는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)와 같은 배포 기술과 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-112">How MSBuild integrates with deployment technologies, like the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>
> - <span data-ttu-id="eb05b-113">프로젝트 파일의 주요 구성 요소를 이해 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-113">How to understand the key components of a project file.</span></span>
> - <span data-ttu-id="eb05b-114">어떻게 빌드 및 복잡 한 응용 프로그램을 배포 하려면 프로젝트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-114">How you can use project files to build and deploy complex applications.</span></span>


## <a name="msbuild-and-the-project-file"></a><span data-ttu-id="eb05b-115">프로젝트 파일과 MSBuild</span><span class="sxs-lookup"><span data-stu-id="eb05b-115">MSBuild and the Project File</span></span>

<span data-ttu-id="eb05b-116">를 만들고 Visual Studio에서 솔루션을 빌드할 때 Visual Studio 솔루션의 각 프로젝트를 빌드하려면 MSBuild를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-116">When you create and build solutions in Visual Studio, Visual Studio uses MSBuild to build each project in your solution.</span></span> <span data-ttu-id="eb05b-117">모든 Visual Studio 프로젝트에 프로젝트 형식에 반영 하는 파일 확장명을 사용 하 여 MSBuild 프로젝트 파일을&#x2014;예를 들어 C# 프로젝트 (.csproj), Visual Basic.NET 프로젝트 (.vbproj) 또는 데이터베이스 프로젝트 (.dbproj).</span><span class="sxs-lookup"><span data-stu-id="eb05b-117">Every Visual Studio project includes an MSBuild project file, with a file extension that reflects the type of project&#x2014;for example, a C# project (.csproj), a Visual Basic.NET project (.vbproj), or a database project (.dbproj).</span></span> <span data-ttu-id="eb05b-118">프로젝트를 구축 하기 위해 MSBuild는 프로젝트에 연결 된 프로젝트 파일을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-118">In order to build a project, MSBuild must process the project file associated with the project.</span></span> <span data-ttu-id="eb05b-119">프로젝트 파일은 모든 정보 및 플랫폼 요구 사항, 버전 관리 정보, 웹 서버 또는 데이터베이스 서버 설정에 포함 하려면 콘텐츠와 마찬가지로 프로젝트를 빌드하려면 MSBuild 해야 한다는 지침을 포함 하는 XML 문서 및 수행 해야 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-119">The project file is an XML document that contains all the information and instructions that MSBuild needs in order to build your project, like the content to include, the platform requirements, versioning information, web server or database server settings, and the tasks that must be performed.</span></span>

<span data-ttu-id="eb05b-120">MSBuild 프로젝트 파일에 기반한 합니다 [MSBuild XML 스키마](https://msdn.microsoft.com/library/5dy88c2e.aspx), 이며 결과적으로 빌드 프로세스 전적으로 열고 투명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-120">MSBuild project files are based on the [MSBuild XML schema](https://msdn.microsoft.com/library/5dy88c2e.aspx), and as a result the build process is entirely open and transparent.</span></span> <span data-ttu-id="eb05b-121">또한 MSBuild 엔진을 사용 하려면 Visual Studio를 설치할 필요가 없습니다&#x2014;.NET Framework의 일부인 MSBuild.exe 실행 파일 및 명령 프롬프트에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-121">In addition, you don't need to install Visual Studio in order to use the MSBuild engine&#x2014;the MSBuild.exe executable is part of the .NET Framework, and you can run it from a command prompt.</span></span> <span data-ttu-id="eb05b-122">개발자는 MSBuild XML 스키마를 사용 하 여 프로젝트 빌드 및 배포 하는 방법을 정교 하 고 세분화 된 제어를 적용 하려면 사용자 고유의 MSBuild 프로젝트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-122">As a developer, you can craft your own MSBuild project files, using the MSBuild XML schema, to impose sophisticated and fine-grained control over how your projects are built and deployed.</span></span> <span data-ttu-id="eb05b-123">이러한 사용자 지정 프로젝트 파일이 Visual Studio에서 자동으로 생성 되는 프로젝트 파일과 동일한 방식으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-123">These custom project files work in exactly the same way as the project files that Visual Studio generates automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="eb05b-124">또한 Team Foundation Server (TFS)에서 팀 빌드 서비스를 사용 하 여 MSBuild 프로젝트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-124">You can also use MSBuild project files with the Team Build service in Team Foundation Server (TFS).</span></span> <span data-ttu-id="eb05b-125">예를 들어, 새 코드를 체크 인할 때 테스트 환경에 배포를 자동화 하려면 CI (지속적인 통합) 시나리오에서 프로젝트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-125">For example, you can use project files in continuous integration (CI) scenarios to automate deployment to a test environment when new code is checked in.</span></span> <span data-ttu-id="eb05b-126">자세한 내용은 [자동화 된 웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-126">For more information, see [Configuring Team Foundation Server for Automated Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span>


### <a name="project-file-naming-conventions"></a><span data-ttu-id="eb05b-127">프로젝트 파일 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="eb05b-127">Project File Naming Conventions</span></span>

<span data-ttu-id="eb05b-128">사용자 고유의 프로젝트 파일을 만들면 원하는 파일 확장명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-128">When you create your own project files, you can use any file extension you like.</span></span> <span data-ttu-id="eb05b-129">그러나 솔루션을 더 쉽게 다른 사람이 이해 하기에 대 한 이러한 일반적인 규칙을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-129">However, to make your solutions easier for others to understand, you should use these common conventions:</span></span>

- <span data-ttu-id="eb05b-130">프로젝트를 빌드하는 프로젝트 파일을 만들 때.proj 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-130">Use the .proj extension when you create a project file that builds projects.</span></span>
- <span data-ttu-id="eb05b-131">다른 프로젝트 파일로 가져올 다시 사용할 수 있는 프로젝트 파일을 만들 때.targets 확장명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-131">Use the .targets extension when you create a reusable project file to import into other project files.</span></span> <span data-ttu-id="eb05b-132">.Targets 확장명을 사용 하 여 파일 일반적으로 없는 빌드 아무 것도 자체를.proj 파일에 가져올 수 있는 지침 포함 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-132">Files with a .targets extension typically don't build anything themselves, they simply contain instructions that you can import into your .proj files.</span></span>

### <a name="integration-with-deployment-technologies"></a><span data-ttu-id="eb05b-133">배포 기술과 통합</span><span class="sxs-lookup"><span data-stu-id="eb05b-133">Integration with Deployment Technologies</span></span>

<span data-ttu-id="eb05b-134">ASP.NET 웹 응용 프로그램 및 ASP.NET MVC 웹 응용 프로그램과 같은 Visual Studio 2010에서 웹 응용 프로그램 프로젝트를 사용 하 여 했었다면 이러한 프로젝트 패키징 및 배포 대상 환경에 웹 응용 프로그램에 대 한 기본 제공 지원을 포함 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-134">If you've worked with web application projects in Visual Studio 2010, like ASP.NET web applications and ASP.NET MVC web applications, you'll know that these projects include built-in support for packaging and deploying the web application to a target environment.</span></span> <span data-ttu-id="eb05b-135">**속성** 이러한 프로젝트에 대해 페이지 **웹 패키지 및 게시** 및 **SQL 패키지 및 게시** 탭 구성 하는 데 사용할 수 있는 방법의 구성 요소에 응용 프로그램 패키지 되 고 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-135">The **Properties** pages for these projects include **Package/Publish Web** and **Package/Publish SQL** tabs that you can use to configure how the components of your application are packaged and deployed.</span></span> <span data-ttu-id="eb05b-136">표시 된 **웹 패키지 및 게시** 탭:</span><span class="sxs-lookup"><span data-stu-id="eb05b-136">This shows the **Package/Publish Web** tab:</span></span>

![](understanding-the-project-file/_static/image1.png)

<span data-ttu-id="eb05b-137">이러한 기능은 기본 기술으로 웹 게시 파이프라인 (WPP) 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-137">The underlying technology behind these capabilities is known as the Web Publishing Pipeline (WPP).</span></span> <span data-ttu-id="eb05b-138">WPP MSBuild를 기본적으로 제공 하 고 [웹 배포](https://go.microsoft.com/?linkid=9805122) 웹 응용 프로그램에 대 한 전체 빌드, 패키지 및 배포 프로세스를 제공 하기 위해 협력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-138">The WPP essentially brings MSBuild and [Web Deploy](https://go.microsoft.com/?linkid=9805122) together to provide a complete build, package, and deployment process for your web applications.</span></span>

<span data-ttu-id="eb05b-139">좋은 소식은 WPP 웹 프로젝트에 대 한 사용자 지정 프로젝트 파일을 만들 때 제공 하는 통합 지점 활용을 수행할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-139">The good news is that you can take advantage of the integration points that the WPP provides when you create custom project files for web projects.</span></span> <span data-ttu-id="eb05b-140">프로젝트 빌드, 웹 배포 패키지 만들기 및 단일 프로젝트 파일과 MSBuild에 대 한 단일 호출을 통해 원격 서버에서 이러한 패키지를 설치할 수 있는 프로젝트 파일에서 배포 지침을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-140">You can include deployment instructions in your project file, which allows you to build your projects, create web deployment packages, and install these packages on remote servers through a single project file and a single call to MSBuild.</span></span> <span data-ttu-id="eb05b-141">또한 빌드 프로세스의 일부로 다른 실행 파일을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-141">You can also call any other executables as part of your build process.</span></span> <span data-ttu-id="eb05b-142">예를 들어 스키마 파일에서 데이터베이스를 배포 VSDBCMD.exe 명령줄 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-142">For example, you can run the VSDBCMD.exe command-line tool to deploy a database from a schema file.</span></span> <span data-ttu-id="eb05b-143">이 항목의 과정을 통해 엔터프라이즈 배포 시나리오의 요구 사항에 맞게 이러한 기능은 활용할 수는 어떻게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-143">Over the course of this topic, you'll see how you can take advantage of these capabilities to meet the requirements of your enterprise deployment scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="eb05b-144">웹 응용 프로그램 배포 프로세스의 작동 방식에 대 한 자세한 내용은 참조 하세요. [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-144">For more information on how the web application deployment process works, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698.aspx).</span></span>


## <a name="the-anatomy-of-a-project-file"></a><span data-ttu-id="eb05b-145">프로젝트 파일의 분석</span><span class="sxs-lookup"><span data-stu-id="eb05b-145">The Anatomy of a Project File</span></span>

<span data-ttu-id="eb05b-146">빌드 프로세스를 자세히 살펴보기 전에 MSBuild 프로젝트 파일의 기본 구조를 숙지 하는 데는 몇 분 정도 걸리는 가치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-146">Before you look at the build process in more detail, it's worth taking a few moments to familiarize yourself with the basic structure of an MSBuild project file.</span></span> <span data-ttu-id="eb05b-147">이 섹션에서는 검토, 편집 또는 프로젝트 파일을 만들 때 발생 하는 보다 일반적인 요소의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-147">This section provides an overview of the more common elements that you'll encounter when you review, edit, or create a project file.</span></span> <span data-ttu-id="eb05b-148">특히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-148">In particular, you'll learn:</span></span>

- <span data-ttu-id="eb05b-149">사용 하는 방법 *속성* 빌드 프로세스에 대 한 변수를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-149">How to use *properties* to manage variables for the build process.</span></span>
- <span data-ttu-id="eb05b-150">사용 하는 방법 *항목* 다음과 같은 코드 파일은 빌드 프로세스에 대 한 입력을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-150">How to use *items* to identify the inputs to the build process, like code files.</span></span>
- <span data-ttu-id="eb05b-151">사용 하는 방법 *대상* 하 고 *작업* msbuild를 실행 지침을 제공 하를 사용 하 여 *속성* 및 *항목* 에서 다른 곳에서 정의 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-151">How to use *targets* and *tasks* to provide execution instructions to MSBuild, using *properties* and *items* defined elsewhere in the project file.</span></span>

<span data-ttu-id="eb05b-152">MSBuild 프로젝트 파일의 주요 요소 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-152">This shows the relationship between the key elements in an MSBuild project file:</span></span>

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a><span data-ttu-id="eb05b-153">프로젝트 요소</span><span class="sxs-lookup"><span data-stu-id="eb05b-153">The Project Element</span></span>

<span data-ttu-id="eb05b-154">합니다 [프로젝트](https://msdn.microsoft.com/library/bcxfsh87.aspx) 요소는 모든 프로젝트 파일의 루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-154">The [Project](https://msdn.microsoft.com/library/bcxfsh87.aspx) element is the root element of every project file.</span></span> <span data-ttu-id="eb05b-155">프로젝트 파일에 대 한 XML 스키마를 식별 하는 것 외에도 합니다 **프로젝트** 요소는 빌드 프로세스에 대 한 진입점을 지정 하는 특성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-155">In addition to identifying the XML schema for the project file, the **Project** element can include attributes to specify the entry points for the build process.</span></span> <span data-ttu-id="eb05b-156">예를 들어, 합니다 [Contact Manager 샘플 솔루션](the-contact-manager-solution.md)의 *Publish.proj* 파일 이라는 대상을 호출 하 여 빌드를 시작 해야 함을 지정 **FullPublish**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-156">For example, in the [Contact Manager sample solution](the-contact-manager-solution.md), the *Publish.proj* file specifies that the build should start by calling the target named **FullPublish**.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]


### <a name="properties-and-conditions"></a><span data-ttu-id="eb05b-157">속성 및 조건</span><span class="sxs-lookup"><span data-stu-id="eb05b-157">Properties and Conditions</span></span>

<span data-ttu-id="eb05b-158">일반적으로 프로젝트 파일을 성공적으로 빌드 및 프로젝트를 배포 하기 위해 다양 한 정보를 많이 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-158">A project file typically needs to provide lots of different pieces of information in order to successfully build and deploy your projects.</span></span> <span data-ttu-id="eb05b-159">이러한 정보에는 서버 이름, 연결 문자열, 자격 증명, 빌드 구성, 원본 및 대상 파일 경로 및 사용자 지정을 지원 하려면 포함 하려는 모든 기타 정보에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-159">These pieces of information could include server names, connection strings, credentials, build configurations, source and destination file paths, and any other information you want to include to support customization.</span></span> <span data-ttu-id="eb05b-160">프로젝트 파일 속성 내에서 정의 되어야 합니다는 [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-160">In a project file, properties must be defined within a [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) element.</span></span> <span data-ttu-id="eb05b-161">MSBuild 속성의 키-값 쌍으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-161">MSBuild properties consist of key-value pairs.</span></span> <span data-ttu-id="eb05b-162">내 합니다 **PropertyGroup** 속성 키를 정의 하는 요소, 요소 이름 및 속성 값을 정의 하는 요소의 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-162">Within the **PropertyGroup** element, the element name defines the property key and the content of the element defines the property value.</span></span> <span data-ttu-id="eb05b-163">예를 들어, 명명 된 속성을 정의할 수 있습니다 **ServerName** 하 고 **ConnectionString** 정적 서버 이름 및 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-163">For example, you could define properties named **ServerName** and **ConnectionString** to store a static server name and connection string.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]


<span data-ttu-id="eb05b-164">속성 값을 검색 하 형식을 사용 하면 <strong>$(</strong><em>PropertyName</em><strong>)</strong><em>.</em> 예를 들어의 값을 검색 하는 <strong>ServerName</strong> 속성 입력:</span><span class="sxs-lookup"><span data-stu-id="eb05b-164">To retrieve a property value, you use the format <strong>$(</strong><em>PropertyName</em><strong>)</strong><em>.</em>For example, to retrieve the value of the <strong>ServerName</strong> property, you would type:</span></span>


[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]


> [!NOTE]
> <span data-ttu-id="eb05b-165">방법의 예제 및이 항목의 뒷부분에 나오는 속성 값을 사용 하는 경우 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-165">You'll see examples of how and when to use property values later in this topic.</span></span>


<span data-ttu-id="eb05b-166">프로젝트 파일에서 정적 속성으로 정보를 포함 합니다. 아닌 경우 항상 빌드 프로세스를 관리 하는 이상적인 방법</span><span class="sxs-lookup"><span data-stu-id="eb05b-166">Embedding information as static properties in a project file is not always the ideal approach to managing the build process.</span></span> <span data-ttu-id="eb05b-167">많은 시나리오를 다른 원본에서 정보를 얻거나 궁극적인 목표는 사용자 명령 프롬프트에서 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-167">In a lot of scenarios, you'll want to obtain the information from other sources or empower the user to provide the information from the command prompt.</span></span> <span data-ttu-id="eb05b-168">MSBuild를 사용 하면 명령줄 매개 변수로 속성 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-168">MSBuild allows you to specify any property value as a command-line parameter.</span></span> <span data-ttu-id="eb05b-169">사용자 수에 대 한 값을 제공 하는 예를 들어 **ServerName** 실행 될 때 자신이 MSBuild.exe 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="eb05b-169">For example, the user could provide a value for **ServerName** when he or she runs MSBuild.exe from the command line.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="eb05b-170">MSBuild.exe를 사용 하 여 사용할 수 있습니다 스위치 인수에 대 한 자세한 내용은 참조 하세요. [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-170">For more information on the arguments and switches you can use with MSBuild.exe, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>


<span data-ttu-id="eb05b-171">환경 변수 및 기본 제공 프로젝트 속성의 값을 가져오려면 동일한 속성 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-171">You can use the same property syntax to obtain the values of environment variables and built-in project properties.</span></span> <span data-ttu-id="eb05b-172">일반적으로 사용 되는 속성에 많은 사용자에 대해 정의 된 및 관련 매개 변수 이름을 포함 하 여 프로젝트 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-172">Lots of commonly used properties are defined for you, and you can use them in your project files by including the relevant parameter name.</span></span> <span data-ttu-id="eb05b-173">예를 들어, 현재 프로젝트 플랫폼을 검색할&#x2014;예를 들어 **x86** 또는 **AnyCpu**&#x2014;포함 될 수 있습니다 합니다 **$** 에서 속성 참조 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-173">For example, to retrieve the current project platform&#x2014;for example, **x86** or **AnyCpu**&#x2014;you can include the **$(Platform)** property reference in your project file.</span></span> <span data-ttu-id="eb05b-174">자세한 내용은 [빌드 명령 및 속성 매크로](https://msdn.microsoft.com/library/c02as0cs.aspx)를 [일반적인 MSBuild 프로젝트 속성](https://msdn.microsoft.com/library/bb629394.aspx), 및 [예약 된 속성](https://msdn.microsoft.com/library/ms164309.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-174">For more information, see [Macros for Build Commands and Properties](https://msdn.microsoft.com/library/c02as0cs.aspx), [Common MSBuild Project Properties](https://msdn.microsoft.com/library/bb629394.aspx), and [Reserved Properties](https://msdn.microsoft.com/library/ms164309.aspx).</span></span>

<span data-ttu-id="eb05b-175">속성은 종종 함께에서 사용 됩니다 *조건을*합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-175">Properties are often used in conjunction with *conditions*.</span></span> <span data-ttu-id="eb05b-176">대부분의 MSBuild 요소를 지원 합니다 **조건을** 기반이 MSBuild 요소를 평가 해야 하는 조건을 지정할 수 있는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-176">Most MSBuild elements support the **Condition** attribute, which lets you specify the criteria upon which MSBuild should evaluate the element.</span></span> <span data-ttu-id="eb05b-177">예를 들어이 속성 정을 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-177">For example, consider this property definition:</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]


<span data-ttu-id="eb05b-178">MSBuild는이 속성 정의 처리할 때 먼저 확인 하 여부를 **$(OutputRoot)** 속성 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-178">When MSBuild processes this property definition, it first checks to see whether an **$(OutputRoot)** property value is available.</span></span> <span data-ttu-id="eb05b-179">속성 값이 비어 있으면&#x2014;즉, 사용자 되지 않은이 속성에 제공 된 값이&#x2014;조건이 **true** 속성 값을로 설정 됩니다 **... \Publish\Out**합니다. 사용자에서는이 속성에 대 한 값을 제공 하는 경우 조건이 **false** 정적 속성 값이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-179">If the property value is blank&#x2014;in other words, the user hasn't provided a value for this property&#x2014;the condition evaluates to **true** and the property value is set to **..\Publish\Out**. If the user has provided a value for this property, the condition evaluates to **false** and the static property value is not used.</span></span>

<span data-ttu-id="eb05b-180">다양 한 조건을 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [MSBuild 조건](https://msdn.microsoft.com/library/7szfhaft.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-180">For more information on the different ways in which you can specify conditions, see [MSBuild Conditions](https://msdn.microsoft.com/library/7szfhaft.aspx).</span></span>

### <a name="items-and-item-groups"></a><span data-ttu-id="eb05b-181">항목 및 항목 그룹</span><span class="sxs-lookup"><span data-stu-id="eb05b-181">Items and Item Groups</span></span>

<span data-ttu-id="eb05b-182">프로젝트 파일의 중요 한 역할 중 하나는 빌드 프로세스에 대 한 입력을 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-182">One of the important roles of the project file is to define the inputs to the build process.</span></span> <span data-ttu-id="eb05b-183">일반적으로 이러한 입력 파일이&#x2014;코드 파일, 구성 파일에서 명령 파일 및 다른 파일을 처리 하거나로 복사 해야 하는 빌드 프로세스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-183">Typically, these inputs are files&#x2014;code files, configuration files, command files, and any other files that you need to process or copy as part of the build process.</span></span> <span data-ttu-id="eb05b-184">MSBuild 프로젝트 스키마를이 입력 하 여 표시 됩니다 [항목](https://msdn.microsoft.com/library/ms164283.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-184">In the MSBuild project schema, these inputs are represented by [Item](https://msdn.microsoft.com/library/ms164283.aspx) elements.</span></span> <span data-ttu-id="eb05b-185">프로젝트 파일에서 항목 내에서 정의 해야 합니다는 [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-185">In a project file, items must be defined within an [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) element.</span></span> <span data-ttu-id="eb05b-186">마찬가지로 **속성** 요소에 이름을 지정할 수 있습니다는 **항목** 요소 원하는 대로 정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-186">Just like **Property** elements, you can name an **Item** element however you like.</span></span> <span data-ttu-id="eb05b-187">그러나 지정 해야 합니다는 **Include** 파일 또는 항목을 나타내는 와일드 카드를 식별 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-187">However, you must specify an **Include** attribute to identify the file or wildcard that the item represents.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]


<span data-ttu-id="eb05b-188">여러 번 지정 하 여 **항목** 동일한 이름의 요소를 효과적으로 만드는 리소스의 명명된 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-188">By specifying multiple **Item** elements with the same name, you're effectively creating a named list of resources.</span></span> <span data-ttu-id="eb05b-189">작업에서이 확인 하려면 Visual Studio에서 생성 하는 프로젝트 파일 중 하나에 대해 알아보겠습니다는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-189">A good way to see this in action is to take a look inside one of the project files that Visual Studio creates.</span></span> <span data-ttu-id="eb05b-190">예를 들어 합니다 *ContactManager.Mvc.csproj* 샘플 솔루션의 파일에는 각각 동일한 이름의 여러 항목 그룹을 많이 포함 **항목** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-190">For example, the *ContactManager.Mvc.csproj* file in the sample solution includes a lot of item groups, each with several identically named **Item** elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]


<span data-ttu-id="eb05b-191">이러한 방식으로 프로젝트 파일을 동일한 방식으로 처리 해야 하는 파일 목록을 생성 하는 MSBuild 지시는&#x2014;는 **참조** 목록은 성공적인 빌드를 한 곳에 있어야 하는 어셈블리를  **컴파일** 컴파일해야 하는 코드 파일을 포함 하는 목록 및 **콘텐츠** 목록에는 변경 되지 않은 상태로 복사 되어야 하는 리소스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-191">In this way, the project file is instructing MSBuild to construct lists of files that need to be processed in the same way&#x2014;the **Reference** list includes assemblies that must be in place for a successful build, the **Compile** list includes code files that must be compiled, and the **Content** list includes resources that must be copied unaltered.</span></span> <span data-ttu-id="eb05b-192">빌드 프로세스 참조 및이 항목 뒷부분의 해당이 항목을 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-192">We'll look at how the build process references and uses these items later in this topic.</span></span>

<span data-ttu-id="eb05b-193">항목 요소를 포함할 수도 [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-193">Item elements can also include [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) child elements.</span></span> <span data-ttu-id="eb05b-194">이러한 사용자 정의 키-값 쌍 이며 기본적으로 해당 항목에 관련 된 속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-194">These are user-defined key-value pairs and essentially represent properties that are specific to that item.</span></span> <span data-ttu-id="eb05b-195">예를 들어, 많은 합니다 **컴파일** 프로젝트 파일의 항목 요소에 포함 되어 **DependentUpon** 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-195">For example, a lot of the **Compile** item elements in the project file include **DependentUpon** child elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]


> [!NOTE]
> <span data-ttu-id="eb05b-196">사용자가 만든 항목 메타 데이터 외에 모든 항목 생성 시 공용 다양 한 메타 데이터가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-196">In addition to user-created item metadata, all items are assigned various common metadata on creation.</span></span> <span data-ttu-id="eb05b-197">자세한 내용은 [잘 알려진 항목 메타데이터](https://msdn.microsoft.com/library/ms164313.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb05b-197">For more information, see [Well-known Item Metadata](https://msdn.microsoft.com/library/ms164313.aspx).</span></span>


<span data-ttu-id="eb05b-198">만들 수 있습니다 **ItemGroup** 루트 수준 내의 요소 **프로젝트** 요소 또는 특정 내 **대상** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-198">You can create **ItemGroup** elements within the root-level **Project** element or within specific **Target** elements.</span></span> <span data-ttu-id="eb05b-199">**ItemGroup** 요소 기능도 **조건** 프로젝트 구성 또는 플랫폼와 같은 조건에 따라 빌드 프로세스에 대 한 입력을 조정할 수 있는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-199">**ItemGroup** elements also support **Condition** attributes, which lets you tailor the inputs to the build process according to conditions like the project configuration or platform.</span></span>

### <a name="targets-and-tasks"></a><span data-ttu-id="eb05b-200">대상 및 작업</span><span class="sxs-lookup"><span data-stu-id="eb05b-200">Targets and Tasks</span></span>

<span data-ttu-id="eb05b-201">MSBuild 스키마에는 [태스크](https://msdn.microsoft.com/library/77f2hx1s.aspx) 요소는 개별 빌드 명령 (또는 작업)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-201">In the MSBuild schema, a [Task](https://msdn.microsoft.com/library/77f2hx1s.aspx) element represents an individual build instruction (or task).</span></span> <span data-ttu-id="eb05b-202">MSBuild는 다양 한 미리 정의 된 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-202">MSBuild includes a multitude of predefined tasks.</span></span> <span data-ttu-id="eb05b-203">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="eb05b-203">For example:</span></span>

- <span data-ttu-id="eb05b-204">합니다 **복사** 태스크를 새 위치로 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-204">The **Copy** task copies files to a new location.</span></span>
- <span data-ttu-id="eb05b-205">합니다 **Csc** Visual C# 컴파일러를 호출 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-205">The **Csc** task invokes the Visual C# compiler.</span></span>
- <span data-ttu-id="eb05b-206">합니다 **Vbc** Visual Basic 컴파일러를 호출 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-206">The **Vbc** task invokes the Visual Basic compiler.</span></span>
- <span data-ttu-id="eb05b-207">합니다 **Exec** 작업이 지정된 된 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-207">The **Exec** task runs a specified program.</span></span>
- <span data-ttu-id="eb05b-208">합니다 **메시지** 태스크로 거에 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-208">The **Message** task writes a message to a logger.</span></span>

> [!NOTE]
> <span data-ttu-id="eb05b-209">기본적으로 사용할 수 있는 작업의 전체 세부 정보를 참조 하세요 [MSBuild 작업 참조](https://msdn.microsoft.com/library/7z253716.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-209">For full details of the tasks that are available out of the box, see [MSBuild Task Reference](https://msdn.microsoft.com/library/7z253716.aspx).</span></span> <span data-ttu-id="eb05b-210">사용자 고유의 사용자 지정 작업을 만드는 방법을 비롯 한 태스크에 대 한 자세한 내용은 참조 하세요 [MSBuild 작업](https://msdn.microsoft.com/library/ms171466.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-210">For more information on tasks, including how to create your own custom tasks, see [MSBuild Tasks](https://msdn.microsoft.com/library/ms171466.aspx).</span></span>


<span data-ttu-id="eb05b-211">작업에 항상 포함 되어야 합니다 [대상](https://msdn.microsoft.com/library/t50z2hka.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-211">Tasks must always be contained within [Target](https://msdn.microsoft.com/library/t50z2hka.aspx) elements.</span></span> <span data-ttu-id="eb05b-212">A **대상** 요소는 순차적으로 실행 되는 하나 이상의 작업 집합이 며 프로젝트 파일에는 여러 대상이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-212">A **Target** element is a set of one or more tasks that are executed sequentially, and a project file can contain multiple targets.</span></span> <span data-ttu-id="eb05b-213">작업 또는 작업 집합을 실행 하려는 경우 포함 된 대상을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-213">When you want to run a task, or a set of tasks, you invoke the target that contains them.</span></span> <span data-ttu-id="eb05b-214">예를 들어, 메시지를 기록 하는 간단한 프로젝트 파일이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-214">For example, suppose you have a simple project file that logs a message.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]


<span data-ttu-id="eb05b-215">명령줄에서 대상을 사용 하 여 호출할 수 있습니다 합니다 **/t** 대상을 지정 하는 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-215">You can invoke the target from the command line, by using the **/t** switch to specify the target.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]


<span data-ttu-id="eb05b-216">추가할 수 있습니다는 **DefaultTargets** 특성을 합니다 **프로젝트** 요소를 호출 하려는 대상을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-216">Alternatively, you can add a **DefaultTargets** attribute to the **Project** element, to specify the targets that you want to invoke.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]


<span data-ttu-id="eb05b-217">이 경우 명령줄에서 대상을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-217">In this case, you don't need to specify the target from the command line.</span></span> <span data-ttu-id="eb05b-218">프로젝트 파일을 간단히 지정할 수 있습니다 및 MSBuild를 호출 합니다 **FullPublish** 를 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-218">You can simply specify the project file, and MSBuild will invoke the **FullPublish** target for you.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]


<span data-ttu-id="eb05b-219">대상 및 작업을 모두 포함 될 수 있습니다 **조건을** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-219">Both targets and tasks can include **Condition** attributes.</span></span> <span data-ttu-id="eb05b-220">따라서 특정 조건이 충족 될 경우 전체 대상 또는 개별 태스크를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-220">As such, you can choose to omit entire targets or individual tasks if certain conditions are met.</span></span>

<span data-ttu-id="eb05b-221">일반적으로 유용한 작업 및 목표를 만든 경우에 속성 및 프로젝트 파일의 다른 곳에서 정의 된 항목을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-221">Generally speaking, when you create useful tasks and targets, you'll need to refer to the properties and items that you've defined elsewhere in the project file:</span></span>

- <span data-ttu-id="eb05b-222">속성 값을 사용 하려면 입력 <strong>$(</strong><em>PropertyName</em><strong>)</strong>여기서 <em>PropertyName</em> 이름인는 <strong>속성</strong> 요소 또는 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-222">To use a property value, type <strong>$(</strong><em>PropertyName</em><strong>)</strong>, where <em>PropertyName</em> is the name of the <strong>Property</strong> element or the name of the parameter.</span></span>
- <span data-ttu-id="eb05b-223">항목을 사용 하려면 입력 <strong>@(</strong><em>ItemName</em><strong>)</strong>여기서 <em>ItemName</em> 이름인 합니다 <strong>항목</strong> 요소.</span><span class="sxs-lookup"><span data-stu-id="eb05b-223">To use an item, type <strong>@(</strong><em>ItemName</em><strong>)</strong>, where <em>ItemName</em> is the name of the <strong>Item</strong> element.</span></span>

> [!NOTE]
> <span data-ttu-id="eb05b-224">동일한 이름의 여러 항목을 만드는 경우 목록 작성 하 고 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-224">Remember that if you create multiple items with the same name, you're building a list.</span></span> <span data-ttu-id="eb05b-225">반면, 동일한 이름의 여러 속성을 만드는 경우 마지막 속성 값을 입력 해야 이전 속성 덮어씁니다 동일한 이름을 가진&#x2014;속성을 단일 값을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-225">In contrast, if you create multiple properties with the same name, the last property value you provide will overwrite any previous properties with the same name&#x2014;a property can only contain a single value.</span></span>


<span data-ttu-id="eb05b-226">예를 들어,를 *Publish.proj* 샘플 솔루션에서 파일을 살펴봅니다 합니다 **BuildProjects** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-226">For example, in the *Publish.proj* file in the sample solution, take a look at the **BuildProjects** target.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]


<span data-ttu-id="eb05b-227">이 샘플에서는 이러한 요점을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-227">In this sample, you can observe these key points:</span></span>

- <span data-ttu-id="eb05b-228">경우는 **BuildingInTeamBuild** 매개 변수를 지정 하 고 값이 **true**, 어떤이 대상 내의 작업이 실행 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-228">If the **BuildingInTeamBuild** parameter is specified and has a value of **true**, none of the tasks within this target will be executed.</span></span>
- <span data-ttu-id="eb05b-229">대상의 단일 인스턴스가 포함 된 [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-229">The target contains a single instance of the [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) task.</span></span> <span data-ttu-id="eb05b-230">이 태스크를 사용 하면 다른 MSBuild 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-230">This task lets you build other MSBuild projects.</span></span>
- <span data-ttu-id="eb05b-231">합니다 **ProjectsToBuild** 항목 작업에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-231">The **ProjectsToBuild** item is passed to the task.</span></span> <span data-ttu-id="eb05b-232">이 항목에서 정의 된 모든 프로젝트 또는 솔루션 파일의 목록을 나타낼 수 있습니다 **ProjectsToBuild** 항목 그룹 내에서 요소 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-232">This item could represent a list of project or solution files, all defined by **ProjectsToBuild** item elements within an item group.</span></span> <span data-ttu-id="eb05b-233">이 경우에 **ProjectsToBuild** 항목에서 참조 하는 단일 솔루션 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-233">In this case, the **ProjectsToBuild** item refers to a single solution file.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- <span data-ttu-id="eb05b-234">에 전달 된 속성 값을 **MSBuild** 명명 된 매개 변수를 포함 하는 태스크 **OutputRoot** 및 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-234">The property values passed to the **MSBuild** task include parameters named **OutputRoot** and **Configuration**.</span></span> <span data-ttu-id="eb05b-235">이러한 값은 하지 않은 경우 제공 되는 경우 매개 변수 값 또는 정적 속성 값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-235">These are set to parameter values if they are provided, or static property values if they are not.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

<span data-ttu-id="eb05b-236">도 볼 수 있습니다 합니다 **MSBuild** 라는 대상이 호출 하는 태스크 **빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-236">You can also see that the **MSBuild** task invokes a target named **Build**.</span></span> <span data-ttu-id="eb05b-237">널리 사용 되는 사용자 지정 프로젝트 파일에 제공 되며 Visual Studio 프로젝트 파일에서 같은 몇 가지 기본 제공 대상 중 하나인 **빌드**를 **정리**, **다시**, 및 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-237">This is one of several built-in targets that are widely used in Visual Studio project files and are available to you in your custom project files, like **Build**, **Clean**, **Rebuild**, and **Publish**.</span></span> <span data-ttu-id="eb05b-238">대상 및 작업에 대 한 빌드 프로세스 제어를 사용 하 여 자세히 알아봅니다 합니다 **MSBuild** 특히,이 항목의 뒷부분에 나오는 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-238">You'll learn more about using targets and tasks to control the build process, and about the **MSBuild** task in particular, later in this topic.</span></span>

> [!NOTE]
> <span data-ttu-id="eb05b-239">대상에 대 한 자세한 내용은 참조 하세요. [MSBuild 대상](https://msdn.microsoft.com/library/ms171462.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-239">For more information on targets, see [MSBuild Targets](https://msdn.microsoft.com/library/ms171462.aspx).</span></span>


## <a name="splitting-project-files-to-support-multiple-environments"></a><span data-ttu-id="eb05b-240">여러 환경을 지원 하도록 프로젝트 파일 분</span><span class="sxs-lookup"><span data-stu-id="eb05b-240">Splitting Project Files to Support Multiple Environments</span></span>

<span data-ttu-id="eb05b-241">프로덕션 환경, 테스트 서버 및 스테이징 플랫폼 등 여러 환경에 솔루션을 배포할 수 있게 되기를 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-241">Suppose you want to be able to deploy a solution to multiple environments, like test servers, staging platforms, and production environments.</span></span> <span data-ttu-id="eb05b-242">구성을 이러한 환경 간에 크게 달라질 수 있습니다&#x2014;뿐만 아니라 서버 이름, 연결 문자열 및 등 측면에서 뿐만 아니라 자격 증명, 보안 설정 및 기타 요인의 많은 측면에서 잠재적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-242">The configuration may vary substantially between these environments&#x2014;not just in terms of server names, connection strings, and so on, but also potentially in terms of credentials, security settings, and lots of other factors.</span></span> <span data-ttu-id="eb05b-243">이 작업을 정기적으로 수행 해야 할 경우 대상 환경 전환 될 때마다 프로젝트 파일의 여러 속성을 편집 하려면 실제로 합당 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-243">If you need to do this regularly, it's not really expedient to edit multiple properties in your project file every time you switch the target environment.</span></span> <span data-ttu-id="eb05b-244">속성 값은 빌드 프로세스에 제공 되는 무한 목록이 필요에 적합 한 솔루션을 것도 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-244">Nor is it an ideal solution to require an endless list of property values to be provided to the build process.</span></span>

<span data-ttu-id="eb05b-245">다행히는 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-245">Fortunately there is an alternative.</span></span> <span data-ttu-id="eb05b-246">MSBuild를 사용 하면 빌드 구성에 여러 프로젝트 파일에 걸쳐 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-246">MSBuild lets you split your build configuration across multiple project files.</span></span> <span data-ttu-id="eb05b-247">작동 방식을 보려면이, 샘플 솔루션에서는 두 개의 사용자 지정 프로젝트 파일이 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-247">To see how this works, in the sample solution, notice that there are two custom project files:</span></span>

- <span data-ttu-id="eb05b-248">*Publish.proj*속성, 항목을 포함 하는, 및 모든 환경에 공통적으로 적용 되는 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-248">*Publish.proj*, which contains properties, items, and targets that are common to all environments.</span></span>
- <span data-ttu-id="eb05b-249">*Env Dev.proj*, 개발자 환경에 관련 된 속성을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-249">*Env-Dev.proj*, which contains properties that are specific to a developer environment.</span></span>

<span data-ttu-id="eb05b-250">이제 있음을 합니다 *Publish.proj* 파일에는 [가져오기](https://msdn.microsoft.com/library/92x05xfs.aspx) 여 바로 아래에 있는 요소를 **프로젝트** 태그.</span><span class="sxs-lookup"><span data-stu-id="eb05b-250">Now notice that the *Publish.proj* file includes an [Import](https://msdn.microsoft.com/library/92x05xfs.aspx) element, immediately beneath the opening **Project** tag.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]


<span data-ttu-id="eb05b-251">**가져올** 다른 MSBuild 프로젝트 파일의 내용을 현재 MSBuild 프로젝트 파일을 가져올 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-251">The **Import** element is used to import the contents of another MSBuild project file into the current MSBuild project file.</span></span> <span data-ttu-id="eb05b-252">이 경우에 **TargetEnvPropsFile** 매개 변수를 가져올 프로젝트 파일의 파일 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-252">In this case, the **TargetEnvPropsFile** parameter provides the filename of the project file you want to import.</span></span> <span data-ttu-id="eb05b-253">MSBuild를 실행할 때이 매개 변수에 대 한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-253">You can provide a value for this parameter when you run MSBuild.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]


<span data-ttu-id="eb05b-254">이 두 파일의 내용을 단일 프로젝트 파일에 효과적으로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-254">This effectively merges the contents of the two files into a single project file.</span></span> <span data-ttu-id="eb05b-255">이 방법을 사용 하면 유니버설 빌드 구성에 포함 된 프로젝트 파일 및 환경 관련 속성을 포함 하는 여러 보조 프로젝트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-255">Using this approach, you can create one project file containing your universal build configuration and multiple supplementary project files containing environment-specific properties.</span></span> <span data-ttu-id="eb05b-256">결과적으로, 다른 매개 변수 값을 사용 하 여 명령을 실행 하기만 하면 다른 환경으로 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-256">As a result, simply running a command with a different parameter value lets you deploy your solution to a different environment.</span></span>

![](understanding-the-project-file/_static/image3.png)

<span data-ttu-id="eb05b-257">이 방식으로 프로젝트 파일을 분할은 따라야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-257">Splitting your project files in this way is a good practice to follow.</span></span> <span data-ttu-id="eb05b-258">개발자가 여러 프로젝트 파일에서 유니버설 빌드 속성의 중복을 방지 하는 동안 단일 명령을 실행 하 여 여러 환경에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-258">It allows developers to deploy to multiple environments by running a single command, while avoiding the duplication of universal build properties across multiple project files.</span></span>

> [!NOTE]
> <span data-ttu-id="eb05b-259">사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-259">For guidance on how to customize the environment-specific project files for your own server environments, see [Configuring Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


## <a name="conclusion"></a><span data-ttu-id="eb05b-260">결론</span><span class="sxs-lookup"><span data-stu-id="eb05b-260">Conclusion</span></span>

<span data-ttu-id="eb05b-261">이 항목에서는 MSBuild 프로젝트 파일에 대 한 일반 소개를 제공 하 고 빌드 프로세스를 제어 하려면 사용자 고유의 사용자 지정 프로젝트 파일을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-261">This topic provided a general introduction to MSBuild project files and explained how you can create your own custom project files to control the build process.</span></span> <span data-ttu-id="eb05b-262">또한 범용 빌드 지침 및 환경별 빌드 속성을 쉽게 빌드 및 여러 대상에 프로젝트를 배포 하려면 프로젝트 파일을 분할할 개념이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-262">It also introduced the concept of splitting project files into universal build instructions and environment-specific build properties, to make it easy to build and deploy projects to multiple destinations.</span></span>

<span data-ttu-id="eb05b-263">다음 항목인 [빌드 프로세스를 이해](understanding-the-build-process.md), 현실적인 수준의 복잡성을 사용 하 여 솔루션의 배포를 통해 컨트롤 빌드 및 배포 하기 위해 프로젝트 파일을 사용 하는 방법을에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-263">The next topic, [Understanding the Build Process](understanding-the-build-process.md), provides more insight into how you can use project files to control build and deployment by walking you through the deployment of a solution with a realistic level of complexity.</span></span>

## <a name="further-reading"></a><span data-ttu-id="eb05b-264">추가 정보</span><span class="sxs-lookup"><span data-stu-id="eb05b-264">Further Reading</span></span>

<span data-ttu-id="eb05b-265">WPP 및 프로젝트 파일에 대 한 자세한 소개를 참조 하세요. [Microsoft 빌드 엔진 내:를 사용 하 여 MSBuild 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi William Bartholomew, ISBN: 978-0-7356-4524-0입니다.</span><span class="sxs-lookup"><span data-stu-id="eb05b-265">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="eb05b-266">[이전](setting-up-the-contact-manager-solution.md)
> [다음](understanding-the-build-process.md)</span><span class="sxs-lookup"><span data-stu-id="eb05b-266">[Previous](setting-up-the-contact-manager-solution.md)
[Next](understanding-the-build-process.md)</span></span>
