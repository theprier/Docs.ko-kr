---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: "프로젝트 파일을 이해 | Microsoft Docs"
author: jrjlee
description: "Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심 에합니다. 이 항목의 MSBuild에 대해 개념적으로 시작 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 09c3793e9cdddb7c42cf966f2d079245f441540c
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="understanding-the-project-file"></a><span data-ttu-id="d8f73-104">프로젝트 파일 이해</span><span class="sxs-lookup"><span data-stu-id="d8f73-104">Understanding the Project File</span></span>
====================
<span data-ttu-id="d8f73-105">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="d8f73-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="d8f73-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="d8f73-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="d8f73-107">Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심 에합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-107">Microsoft Build Engine (MSBuild) project files lie at the heart of the build and deployment process.</span></span> <span data-ttu-id="d8f73-108">이 항목에 대해 개념적으로 프로젝트 파일과 MSBuild로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-108">This topic starts with a conceptual overview of MSBuild and the project file.</span></span> <span data-ttu-id="d8f73-109">가로질러 예가 프로젝트 파일을 사용 하 여 실제 응용 프로그램을 배포 하는 방법을 통해 작동 하 고 프로젝트 파일을 사용 하 여 작업할 때 핵심 구성 요소를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-109">It describes the key components you'll come across when you work with project files, and it works through an example of how you can use project files to deploy real-world applications.</span></span>
> 
> <span data-ttu-id="d8f73-110">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="d8f73-110">What you'll learn:</span></span>
> 
> - <span data-ttu-id="d8f73-111">어떻게 MSBuild는 프로젝트를 빌드하기 위해 MSBuild 프로젝트 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-111">How MSBuild uses MSBuild project files to build projects.</span></span>
> - <span data-ttu-id="d8f73-112">인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)와 같은 배포 기술이, MSBuild 통합 방법</span><span class="sxs-lookup"><span data-stu-id="d8f73-112">How MSBuild integrates with deployment technologies, like the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>
> - <span data-ttu-id="d8f73-113">프로젝트 파일의 주요 구성 요소를 이해 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-113">How to understand the key components of a project file.</span></span>
> - <span data-ttu-id="d8f73-114">어떻게 프로젝트 파일을 빌드 및 복잡 한 응용 프로그램 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-114">How you can use project files to build and deploy complex applications.</span></span>


## <a name="msbuild-and-the-project-file"></a><span data-ttu-id="d8f73-115">MSBuild 및 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="d8f73-115">MSBuild and the Project File</span></span>

<span data-ttu-id="d8f73-116">만들고 Visual Studio에서 솔루션을 빌드할 때 Visual Studio 솔루션의 각 프로젝트를 빌드하려면 MSBuild를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-116">When you create and build solutions in Visual Studio, Visual Studio uses MSBuild to build each project in your solution.</span></span> <span data-ttu-id="d8f73-117">파일 확장명이 프로젝트 & #x 2014의 유형을 반영 하는 MSBuild 프로젝트 파일; 예를 들어 C# 프로젝트 (.csproj), Visual Basic.NET 프로젝트 (.vbproj) 또는 데이터베이스 프로젝트 (.dbproj) 모든 Visual Studio 프로젝트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-117">Every Visual Studio project includes an MSBuild project file, with a file extension that reflects the type of project&#x2014;for example, a C# project (.csproj), a Visual Basic.NET project (.vbproj), or a database project (.dbproj).</span></span> <span data-ttu-id="d8f73-118">MSBuild는 프로젝트를 빌드하려면 프로젝트와 연결 된 프로젝트 파일을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-118">In order to build a project, MSBuild must process the project file associated with the project.</span></span> <span data-ttu-id="d8f73-119">프로젝트 파일은 모든 정보 및 MSBuild 플랫폼 요구 사항, 버전 관리 정보, 웹 서버 또는 데이터베이스 서버 설정을 포함 하도록 콘텐츠와 마찬가지로 프로젝트를 구축 하기 위해 필요한는 지침을 포함 하는 XML 문서 및 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-119">The project file is an XML document that contains all the information and instructions that MSBuild needs in order to build your project, like the content to include, the platform requirements, versioning information, web server or database server settings, and the tasks that must be performed.</span></span>

<span data-ttu-id="d8f73-120">MSBuild 프로젝트 파일 기반으로 [MSBuild XML 스키마](https://msdn.microsoft.com/library/5dy88c2e.aspx), 따라서 빌드 프로세스는 완전히 열리고 투명 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-120">MSBuild project files are based on the [MSBuild XML schema](https://msdn.microsoft.com/library/5dy88c2e.aspx), and as a result the build process is entirely open and transparent.</span></span> <span data-ttu-id="d8f73-121">또한 MSBuild 엔진 & #x 2014 사용 하려면 Visual Studio를 설치할 필요가 없습니다; MSBuild.exe 실행 파일은.NET Framework의 일부 및 명령 프롬프트에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-121">In addition, you don't need to install Visual Studio in order to use the MSBuild engine&#x2014;the MSBuild.exe executable is part of the .NET Framework, and you can run it from a command prompt.</span></span> <span data-ttu-id="d8f73-122">개발자의 경우 MSBuild XML 스키마를 사용 하 여 프로젝트 빌드 및 배포 정교 하 고 세분화 된 제어를 적용 하려면 사용자 고유의 MSBuild 프로젝트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-122">As a developer, you can craft your own MSBuild project files, using the MSBuild XML schema, to impose sophisticated and fine-grained control over how your projects are built and deployed.</span></span> <span data-ttu-id="d8f73-123">이러한 사용자 지정 프로젝트 파일이 Visual Studio를 자동으로 생성 되는 프로젝트 파일과 같은 방식에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-123">These custom project files work in exactly the same way as the project files that Visual Studio generates automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f73-124">팀 빌드 서비스에서 Team Foundation Server (TFS)와 MSBuild 프로젝트 파일을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-124">You can also use MSBuild project files with the Team Build service in Team Foundation Server (TFS).</span></span> <span data-ttu-id="d8f73-125">예를 들어 배포를 자동화 하는 테스트 환경에 새 코드를 체크 인할 때 CI (연속 통합) 시나리오에서 프로젝트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-125">For example, you can use project files in continuous integration (CI) scenarios to automate deployment to a test environment when new code is checked in.</span></span> <span data-ttu-id="d8f73-126">자세한 내용은 참조 [자동화 된 웹 배포를 위해 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-126">For more information, see [Configuring Team Foundation Server for Automated Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span>


### <a name="project-file-naming-conventions"></a><span data-ttu-id="d8f73-127">프로젝트 파일 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="d8f73-127">Project File Naming Conventions</span></span>

<span data-ttu-id="d8f73-128">사용자 고유의 프로젝트 파일을 만들 때 원하는 파일 확장명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-128">When you create your own project files, you can use any file extension you like.</span></span> <span data-ttu-id="d8f73-129">그러나 솔루션을 다른 사람이 이해 하기 간단 하 게 하려면 이러한 일반적인 규칙을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-129">However, to make your solutions easier for others to understand, you should use these common conventions:</span></span>

- <span data-ttu-id="d8f73-130">프로젝트를 작성 하는 프로젝트 파일을 만들 때.proj 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-130">Use the .proj extension when you create a project file that builds projects.</span></span>
- <span data-ttu-id="d8f73-131">다른 프로젝트 파일로 가져올 다시 사용할 수 있는 프로젝트 파일을 만들 때.targets 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-131">Use the .targets extension when you create a reusable project file to import into other project files.</span></span> <span data-ttu-id="d8f73-132">.Targets 확장명을 가진 파일 일반적으로 하지 않는 빌드 아무 것도 자체, 단순히 포함.proj 파일로 가져올 수 있는 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-132">Files with a .targets extension typically don't build anything themselves, they simply contain instructions that you can import into your .proj files.</span></span>

### <a name="integration-with-deployment-technologies"></a><span data-ttu-id="d8f73-133">배포 기술과 통합</span><span class="sxs-lookup"><span data-stu-id="d8f73-133">Integration with Deployment Technologies</span></span>

<span data-ttu-id="d8f73-134">ASP.NET 웹 응용 프로그램 및 ASP.NET MVC 웹 응용 프로그램과 같은 Visual Studio 2010에서 웹 응용 프로그램 프로젝트와 함께 사용한 경우 이러한 프로젝트 패키징 및 대상 환경에 웹 응용 프로그램 배포에 대 한 기본 제공 지원이 포함 되어 있는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-134">If you've worked with web application projects in Visual Studio 2010, like ASP.NET web applications and ASP.NET MVC web applications, you'll know that these projects include built-in support for packaging and deploying the web application to a target environment.</span></span> <span data-ttu-id="d8f73-135">**속성** 페이지에 이러한 프로젝트에 포함 되어 **웹 패키지 및 게시** 및 **SQL 패키지 및 게시** 탭을 구성 하는 데 사용할 수 있는 방법의 구성 요소 프로그램 응용 프로그램 패키지 되 고 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-135">The **Properties** pages for these projects include **Package/Publish Web** and **Package/Publish SQL** tabs that you can use to configure how the components of your application are packaged and deployed.</span></span> <span data-ttu-id="d8f73-136">이 표시는 **웹 패키지 및 게시** 탭:</span><span class="sxs-lookup"><span data-stu-id="d8f73-136">This shows the **Package/Publish Web** tab:</span></span>

![](understanding-the-project-file/_static/image1.png)

<span data-ttu-id="d8f73-137">이러한 기능은 기본 기술으로 웹 게시 파이프라인 (WPP) 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-137">The underlying technology behind these capabilities is known as the Web Publishing Pipeline (WPP).</span></span> <span data-ttu-id="d8f73-138">WPP MSBuild를 기본적으로 제공 하 고 [웹 배포](https://go.microsoft.com/?linkid=9805122) 웹 응용 프로그램에 대 한 전체 빌드, 패키지 및 배포 프로세스를 제공 하기 위해 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-138">The WPP essentially brings MSBuild and [Web Deploy](https://go.microsoft.com/?linkid=9805122) together to provide a complete build, package, and deployment process for your web applications.</span></span>

<span data-ttu-id="d8f73-139">다행히도 WPP 웹 프로젝트에 대 한 사용자 지정 프로젝트 파일을 만들 때 제공 하는 통합 지점의 이용 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-139">The good news is that you can take advantage of the integration points that the WPP provides when you create custom project files for web projects.</span></span> <span data-ttu-id="d8f73-140">프로젝트 웹 배포 패키지를 만들 빌드하고 단일 프로젝트 파일과 MSBuild 한 번 호출을 통해 원격 서버에 이러한 패키지를 설치할 수 있는 프로젝트 파일의 배포 지침을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-140">You can include deployment instructions in your project file, which allows you to build your projects, create web deployment packages, and install these packages on remote servers through a single project file and a single call to MSBuild.</span></span> <span data-ttu-id="d8f73-141">또한 빌드 프로세스의 일부로 다른 실행 파일을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-141">You can also call any other executables as part of your build process.</span></span> <span data-ttu-id="d8f73-142">예를 들어 스키마 파일에서 데이터베이스를 배포 하려면 VSDBCMD.exe 명령줄 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-142">For example, you can run the VSDBCMD.exe command-line tool to deploy a database from a schema file.</span></span> <span data-ttu-id="d8f73-143">이 항목의 과정 동안 있습니다 사용할 수 있는 방법을 엔터프라이즈 배포 시나리오의 요구 사항을 충족 하기 위해 이러한 기능을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-143">Over the course of this topic, you'll see how you can take advantage of these capabilities to meet the requirements of your enterprise deployment scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f73-144">웹 응용 프로그램 배포 프로세스의 작동 방법에 대 한 자세한 내용은 참조 하십시오. [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-144">For more information on how the web application deployment process works, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698.aspx).</span></span>


## <a name="the-anatomy-of-a-project-file"></a><span data-ttu-id="d8f73-145">프로젝트 파일의 구조</span><span class="sxs-lookup"><span data-stu-id="d8f73-145">The Anatomy of a Project File</span></span>

<span data-ttu-id="d8f73-146">빌드 프로세스의 자세한 보기 전에 MSBuild 프로젝트 파일의 기본 구조를 파악 하는 몇 분 정도 가치가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-146">Before you look at the build process in more detail, it's worth taking a few moments to familiarize yourself with the basic structure of an MSBuild project file.</span></span> <span data-ttu-id="d8f73-147">이 섹션에서는 검토, 편집 또는 프로젝트 파일을 만들 때 발생 하는 보다 일반적인 요소의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-147">This section provides an overview of the more common elements that you'll encounter when you review, edit, or create a project file.</span></span> <span data-ttu-id="d8f73-148">특히, 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-148">In particular, you'll learn:</span></span>

- <span data-ttu-id="d8f73-149">사용 하는 방법 *속성* 빌드 프로세스에 대 한 변수를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-149">How to use *properties* to manage variables for the build process.</span></span>
- <span data-ttu-id="d8f73-150">사용 하는 방법 *항목* 다음과 같은 코드 파일을 빌드 프로세스에 대 한 입력을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-150">How to use *items* to identify the inputs to the build process, like code files.</span></span>
- <span data-ttu-id="d8f73-151">사용 하는 방법 *대상* 및 *작업* MSBuild를 실행 지침을 제공 하기를 사용 하 여 *속성* 및 *항목* 다른 위치에서 정의 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-151">How to use *targets* and *tasks* to provide execution instructions to MSBuild, using *properties* and *items* defined elsewhere in the project file.</span></span>

<span data-ttu-id="d8f73-152">MSBuild 프로젝트 파일의 주요 요소 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-152">This shows the relationship between the key elements in an MSBuild project file:</span></span>

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a><span data-ttu-id="d8f73-153">프로젝트 요소</span><span class="sxs-lookup"><span data-stu-id="d8f73-153">The Project Element</span></span>

<span data-ttu-id="d8f73-154">[프로젝트](https://msdn.microsoft.com/library/bcxfsh87.aspx) 요소는 모든 프로젝트 파일의 루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-154">The [Project](https://msdn.microsoft.com/library/bcxfsh87.aspx) element is the root element of every project file.</span></span> <span data-ttu-id="d8f73-155">프로젝트 파일에 대 한 XML 스키마를 식별 하는 것 외에도 **프로젝트** 요소 특성을 지정 하는 빌드 프로세스에 대 한 진입점을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-155">In addition to identifying the XML schema for the project file, the **Project** element can include attributes to specify the entry points for the build process.</span></span> <span data-ttu-id="d8f73-156">예를 들어는 [않아 샘플 솔루션](the-contact-manager-solution.md), *Publish.proj* 파일 빌드 대상 명명 된를 호출 하 여 시작 해야 함을 지정 **FullPublish**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-156">For example, in the [Contact Manager sample solution](the-contact-manager-solution.md), the *Publish.proj* file specifies that the build should start by calling the target named **FullPublish**.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]


### <a name="properties-and-conditions"></a><span data-ttu-id="d8f73-157">속성 및 조건</span><span class="sxs-lookup"><span data-stu-id="d8f73-157">Properties and Conditions</span></span>

<span data-ttu-id="d8f73-158">일반적으로 프로젝트 파일을 성공적으로 빌드 및 프로젝트를 배포 하려면 정보의 다양 한 요소를 많이 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-158">A project file typically needs to provide lots of different pieces of information in order to successfully build and deploy your projects.</span></span> <span data-ttu-id="d8f73-159">이러한 정보를이 바탕 서버 이름, 연결 문자열, 자격 증명, 빌드 구성, 원본 및 대상 파일 경로 및 사용자 지정을 지원 하기 위해 포함 시킬 다른 정보가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-159">These pieces of information could include server names, connection strings, credentials, build configurations, source and destination file paths, and any other information you want to include to support customization.</span></span> <span data-ttu-id="d8f73-160">프로젝트 파일에서 속성 내에서 정의 해야 합니다는 [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-160">In a project file, properties must be defined within a [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) element.</span></span> <span data-ttu-id="d8f73-161">MSBuild 속성 키-값 쌍으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-161">MSBuild properties consist of key-value pairs.</span></span> <span data-ttu-id="d8f73-162">내에서 **PropertyGroup** 요소, 요소 이름 속성 키를 정의 하 고 요소의 콘텐츠 속성 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-162">Within the **PropertyGroup** element, the element name defines the property key and the content of the element defines the property value.</span></span> <span data-ttu-id="d8f73-163">명명 된 속성을 정의할 수는 예를 들어 **ServerName** 및 **ConnectionString** 정적 서버 이름 및 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-163">For example, you could define properties named **ServerName** and **ConnectionString** to store a static server name and connection string.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]


<span data-ttu-id="d8f73-164">형식을 사용 하면 속성 값을 검색 하려면 **$(***PropertyName***) * * *.* 예를 들어의 값을 검색 하는 **ServerName** 속성 입력:</span><span class="sxs-lookup"><span data-stu-id="d8f73-164">To retrieve a property value, you use the format **$(***PropertyName***)***.*For example, to retrieve the value of the **ServerName** property, you would type:</span></span>


[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]


> [!NOTE]
> <span data-ttu-id="d8f73-165">이 항목의 뒷부분에 나오는 속성 값을 사용 하는 시기와 방법의 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-165">You'll see examples of how and when to use property values later in this topic.</span></span>


<span data-ttu-id="d8f73-166">프로젝트 파일에 포함 하는 정적 속성으로 정보는 항상 빌드 프로세스를 관리 하는 데 이상적인 접근 방법.</span><span class="sxs-lookup"><span data-stu-id="d8f73-166">Embedding information as static properties in a project file is not always the ideal approach to managing the build process.</span></span> <span data-ttu-id="d8f73-167">많은 시나리오에서 다른 소스에서 정보를 얻거나 명령 프롬프트에서 정보를 제공 하도록 사용자 권한 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-167">In a lot of scenarios, you'll want to obtain the information from other sources or empower the user to provide the information from the command prompt.</span></span> <span data-ttu-id="d8f73-168">MSBuild를 사용 하면 명령줄 매개 변수가 모든 속성 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-168">MSBuild allows you to specify any property value as a command-line parameter.</span></span> <span data-ttu-id="d8f73-169">사용자에 대 한 값을 제공할 수는 예를 들어 **ServerName** 실행 될 때 자신이 MSBuild.exe 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="d8f73-169">For example, the user could provide a value for **ServerName** when he or she runs MSBuild.exe from the command line.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="d8f73-170">인수 및 스위치 MSBuild.exe로 사용할 수 있습니다에 대 한 자세한 내용은 참조 하십시오. [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-170">For more information on the arguments and switches you can use with MSBuild.exe, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>


<span data-ttu-id="d8f73-171">환경 변수 및 기본 제공 프로젝트 속성의 값을 가져오려면 동일한 속성 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-171">You can use the same property syntax to obtain the values of environment variables and built-in project properties.</span></span> <span data-ttu-id="d8f73-172">일반적으로 사용 되는 속성의 많은 사용자에 대해 정의 된 및 관련 매개 변수 이름을 포함 하 여 프로젝트 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-172">Lots of commonly used properties are defined for you, and you can use them in your project files by including the relevant parameter name.</span></span> <span data-ttu-id="d8f73-173">예를 들어, 검색할 현재 프로젝트 플랫폼 & #x 2014; 예를 들어 **x86** 또는 **AnyCpu**& #x 2014; 포함할 수 있습니다는 **$(Platform)** 에서 속성 참조 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-173">For example, to retrieve the current project platform&#x2014;for example, **x86** or **AnyCpu**&#x2014;you can include the **$(Platform)** property reference in your project file.</span></span> <span data-ttu-id="d8f73-174">자세한 내용은 참조 [빌드 명령 및 속성 매크로](https://msdn.microsoft.com/library/c02as0cs.aspx), [일반적인 MSBuild 프로젝트 속성](https://msdn.microsoft.com/library/bb629394.aspx), 및 [예약 속성](https://msdn.microsoft.com/library/ms164309.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-174">For more information, see [Macros for Build Commands and Properties](https://msdn.microsoft.com/library/c02as0cs.aspx), [Common MSBuild Project Properties](https://msdn.microsoft.com/library/bb629394.aspx), and [Reserved Properties](https://msdn.microsoft.com/library/ms164309.aspx).</span></span>

<span data-ttu-id="d8f73-175">속성을 함께에서 사용 종종 *조건*합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-175">Properties are often used in conjunction with *conditions*.</span></span> <span data-ttu-id="d8f73-176">MSBuild 요소는 대부분 지원는 **조건** 특성으로, MSBuild는 요소를 평가 해야 하는 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-176">Most MSBuild elements support the **Condition** attribute, which lets you specify the criteria upon which MSBuild should evaluate the element.</span></span> <span data-ttu-id="d8f73-177">예를 들어이 속성 정을 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-177">For example, consider this property definition:</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]


<span data-ttu-id="d8f73-178">MSBuild 속성 정의이 처리할 때 먼저 확인 하 여부는 **$(OutputRoot)** 속성 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-178">When MSBuild processes this property definition, it first checks to see whether an **$(OutputRoot)** property value is available.</span></span> <span data-ttu-id="d8f73-179">속성 값이 빈 값 & #x 2014; 즉, 사용자 하지 않은 지정 된 값이 속성 & #x 2014에 대 한; 조건이 **true** 속성 값으로 설정 되 고 **... \Publish\Out**합니다. 이 속성에 대 한 값을 입력 조건이 **false** 고 정적 속성 값이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-179">If the property value is blank&#x2014;in other words, the user hasn't provided a value for this property&#x2014;the condition evaluates to **true** and the property value is set to **..\Publish\Out**. If the user has provided a value for this property, the condition evaluates to **false** and the static property value is not used.</span></span>

<span data-ttu-id="d8f73-180">조건을 지정할 수 있는 다양 한 방법에 대 한 자세한 내용은 참조 하십시오. [MSBuild 조건](https://msdn.microsoft.com/library/7szfhaft.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-180">For more information on the different ways in which you can specify conditions, see [MSBuild Conditions](https://msdn.microsoft.com/library/7szfhaft.aspx).</span></span>

### <a name="items-and-item-groups"></a><span data-ttu-id="d8f73-181">항목 및 항목 그룹</span><span class="sxs-lookup"><span data-stu-id="d8f73-181">Items and Item Groups</span></span>

<span data-ttu-id="d8f73-182">프로젝트 파일의 중요 한 역할 중 하나는 빌드 프로세스에 대 한 입력을 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-182">One of the important roles of the project file is to define the inputs to the build process.</span></span> <span data-ttu-id="d8f73-183">일반적으로 이러한 입력 파일 & #x 2014; 코드 파일과 구성 파일, 명령 파일을 처리 하거나로 복사 해야 하는 다른 파일 부 빌드 프로세스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-183">Typically, these inputs are files&#x2014;code files, configuration files, command files, and any other files that you need to process or copy as part of the build process.</span></span> <span data-ttu-id="d8f73-184">MSBuild 프로젝트 스키마에서이 입력으로 표시 됩니다 [항목](https://msdn.microsoft.com/library/ms164283.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-184">In the MSBuild project schema, these inputs are represented by [Item](https://msdn.microsoft.com/library/ms164283.aspx) elements.</span></span> <span data-ttu-id="d8f73-185">프로젝트 파일 항목 내에서 정의 되어야 합니다는 [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-185">In a project file, items must be defined within an [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) element.</span></span> <span data-ttu-id="d8f73-186">그러나 마찬가지로 **속성** 이름을 지정할 수 있습니다 요소는 **항목** 요소 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-186">Just like **Property** elements, you can name an **Item** element however you like.</span></span> <span data-ttu-id="d8f73-187">그러나 지정 해야 합니다는 **Include** 파일이 나 항목이 나타내는 와일드 카드를 식별 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-187">However, you must specify an **Include** attribute to identify the file or wildcard that the item represents.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]


<span data-ttu-id="d8f73-188">여러 번 지정 하 여 **항목** 동일한 이름 가진 요소를 효과적으로 만드는 리소스의 명명된 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-188">By specifying multiple **Item** elements with the same name, you're effectively creating a named list of resources.</span></span> <span data-ttu-id="d8f73-189">이 방법이 작동 되는지 확인 하는 데는 Visual Studio에서 생성 하는 프로젝트 파일 중 하나에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-189">A good way to see this in action is to take a look inside one of the project files that Visual Studio creates.</span></span> <span data-ttu-id="d8f73-190">예를 들어는 *ContactManager.Mvc.csproj* 파일 샘플 솔루션에 동일한 이름의 여러 각 항목 그룹을 많이 포함 **항목** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-190">For example, the *ContactManager.Mvc.csproj* file in the sample solution includes a lot of item groups, each with several identically named **Item** elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]


<span data-ttu-id="d8f73-191">이러한 방식으로 프로젝트 파일에는 동일한 방식으로 & #x 2014; 처리 해야 하는 파일의 목록을 생성 하는 MSBuild 지시은 **참조** 목록에는 성공적인빌드용준비해야하는어셈블리**컴파일** 을 컴파일해야 하는 코드 파일을 포함 하는 목록 및 **콘텐츠** 변경 되지 않고 복사 해야 하는 리소스 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-191">In this way, the project file is instructing MSBuild to construct lists of files that need to be processed in the same way&#x2014;the **Reference** list includes assemblies that must be in place for a successful build, the **Compile** list includes code files that must be compiled, and the **Content** list includes resources that must be copied unaltered.</span></span> <span data-ttu-id="d8f73-192">빌드 프로세스의 참조와 이러한 항목을 사용 하 여이 항목의 뒷부분에 나오는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-192">We'll look at how the build process references and uses these items later in this topic.</span></span>

<span data-ttu-id="d8f73-193">항목 요소를 포함할 수도 [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-193">Item elements can also include [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) child elements.</span></span> <span data-ttu-id="d8f73-194">이러한 사용자 정의 키-값 쌍 이며 기본적으로 해당 항목에 관련 된 속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-194">These are user-defined key-value pairs and essentially represent properties that are specific to that item.</span></span> <span data-ttu-id="d8f73-195">예를 들어 많은 **컴파일** 항목 요소는 프로젝트 파일에는 **DependentUpon** 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-195">For example, a lot of the **Compile** item elements in the project file include **DependentUpon** child elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]


> [!NOTE]
> <span data-ttu-id="d8f73-196">사용자가 만든 항목 메타 데이터 외에도 모든 항목 생성 시 다양 한 일반 메타 데이터를 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-196">In addition to user-created item metadata, all items are assigned various common metadata on creation.</span></span> <span data-ttu-id="d8f73-197">자세한 내용은 [잘 알려진 항목 메타데이터](https://msdn.microsoft.com/library/ms164313.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8f73-197">For more information, see [Well-known Item Metadata](https://msdn.microsoft.com/library/ms164313.aspx).</span></span>


<span data-ttu-id="d8f73-198">만들 수 있습니다 **ItemGroup** 루트 수준 내에서 요소 **프로젝트** 요소 또는 특정 내 **대상** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-198">You can create **ItemGroup** elements within the root-level **Project** element or within specific **Target** elements.</span></span> <span data-ttu-id="d8f73-199">**ItemGroup** 요소도 지원 **조건** 특성 프로젝트 구성 또는 플랫폼와 같은 조건에 따라 빌드 프로세스에 대 한 입력을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-199">**ItemGroup** elements also support **Condition** attributes, which lets you tailor the inputs to the build process according to conditions like the project configuration or platform.</span></span>

### <a name="targets-and-tasks"></a><span data-ttu-id="d8f73-200">대상 및 작업</span><span class="sxs-lookup"><span data-stu-id="d8f73-200">Targets and Tasks</span></span>

<span data-ttu-id="d8f73-201">MSBuild 스키마에는 [작업](https://msdn.microsoft.com/library/77f2hx1s.aspx) 요소는 개별 빌드 명령 (또는 작업)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-201">In the MSBuild schema, a [Task](https://msdn.microsoft.com/library/77f2hx1s.aspx) element represents an individual build instruction (or task).</span></span> <span data-ttu-id="d8f73-202">MSBuild는 다양 한 미리 정의 된 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-202">MSBuild includes a multitude of predefined tasks.</span></span> <span data-ttu-id="d8f73-203">예:</span><span class="sxs-lookup"><span data-stu-id="d8f73-203">For example:</span></span>

- <span data-ttu-id="d8f73-204">**복사** 작업을 새 위치로 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-204">The **Copy** task copies files to a new location.</span></span>
- <span data-ttu-id="d8f73-205">**Csc** Visual C# 컴파일러를 호출 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-205">The **Csc** task invokes the Visual C# compiler.</span></span>
- <span data-ttu-id="d8f73-206">**Vbc** Visual Basic 컴파일러를 호출 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-206">The **Vbc** task invokes the Visual Basic compiler.</span></span>
- <span data-ttu-id="d8f73-207">**Exec** 작업이 지정된 된 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-207">The **Exec** task runs a specified program.</span></span>
- <span data-ttu-id="d8f73-208">**메시지** 작업 메시지로 거를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-208">The **Message** task writes a message to a logger.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f73-209">곧바로 사용할 수 있는 작업의 전체 정보를 참조 하십시오. [MSBuild 작업 참조](https://msdn.microsoft.com/library/7z253716.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-209">For full details of the tasks that are available out of the box, see [MSBuild Task Reference](https://msdn.microsoft.com/library/7z253716.aspx).</span></span> <span data-ttu-id="d8f73-210">작업을 사용자 지정 작업을 만드는 방법에 대 한 자세한 내용은 참조 [MSBuild 작업](https://msdn.microsoft.com/library/ms171466.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-210">For more information on tasks, including how to create your own custom tasks, see [MSBuild Tasks](https://msdn.microsoft.com/library/ms171466.aspx).</span></span>


<span data-ttu-id="d8f73-211">작업에 항상 포함 되어야 합니다 [대상](https://msdn.microsoft.com/library/t50z2hka.aspx) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-211">Tasks must always be contained within [Target](https://msdn.microsoft.com/library/t50z2hka.aspx) elements.</span></span> <span data-ttu-id="d8f73-212">A **대상** 요소는 일련의 순차적으로 실행 되는 하나 이상의 작업 및 프로젝트 파일에는 여러 대상이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-212">A **Target** element is a set of one or more tasks that are executed sequentially, and a project file can contain multiple targets.</span></span> <span data-ttu-id="d8f73-213">작업 또는 작업 집합을 실행 하려는 경우 포함 된 대상을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-213">When you want to run a task, or a set of tasks, you invoke the target that contains them.</span></span> <span data-ttu-id="d8f73-214">예를 들어 메시지를 기록 하는 간단한 프로젝트 파일을 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-214">For example, suppose you have a simple project file that logs a message.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]


<span data-ttu-id="d8f73-215">명령줄에서 대상을 사용 하 여 호출할 수 있습니다는 **/t** 대상을 지정 하는 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-215">You can invoke the target from the command line, by using the **/t** switch to specify the target.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]


<span data-ttu-id="d8f73-216">추가할 수 있습니다는 **DefaultTargets** 특성을 **프로젝트** 요소를 호출 하려면 대상을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-216">Alternatively, you can add a **DefaultTargets** attribute to the **Project** element, to specify the targets that you want to invoke.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]


<span data-ttu-id="d8f73-217">이 경우 명령줄에서 대상을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-217">In this case, you don't need to specify the target from the command line.</span></span> <span data-ttu-id="d8f73-218">프로젝트 파일을 간단히 지정할 수 있으며 MSBuild를 호출 합니다는 **FullPublish** 대상에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-218">You can simply specify the project file, and MSBuild will invoke the **FullPublish** target for you.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]


<span data-ttu-id="d8f73-219">대상 및 작업을 모두 포함할 수 **조건** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-219">Both targets and tasks can include **Condition** attributes.</span></span> <span data-ttu-id="d8f73-220">따라서 특정 조건이 충족 될 경우 전체 대상 또는 개별 작업을 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-220">As such, you can choose to omit entire targets or individual tasks if certain conditions are met.</span></span>

<span data-ttu-id="d8f73-221">일반적으로 유용한 작업 및 목표를 만들 때에 속성 및 프로젝트 파일에서 다른 곳에서 정의 된 항목을 참조 해야:</span><span class="sxs-lookup"><span data-stu-id="d8f73-221">Generally speaking, when you create useful tasks and targets, you'll need to refer to the properties and items that you've defined elsewhere in the project file:</span></span>

- <span data-ttu-id="d8f73-222">속성 값을 사용 하려면 입력 **$(***PropertyName***)**여기서 *PropertyName* 의 이름인는 **속성** 이름이 나 요소는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-222">To use a property value, type **$(***PropertyName***)**, where *PropertyName* is the name of the **Property** element or the name of the parameter.</span></span>
- <span data-ttu-id="d8f73-223">항목을 사용 하려면 입력 **@(***ItemName***)**여기서 *ItemName* 의 이름인는 **항목** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-223">To use an item, type **@(***ItemName***)**, where *ItemName* is the name of the **Item** element.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f73-224">동일한 이름을 가진 여러 항목을 만들 목록을 작성 하 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-224">Remember that if you create multiple items with the same name, you're building a list.</span></span> <span data-ttu-id="d8f73-225">반면, 마지막 속성 값을 제공와 이름이 같은 & #x 2014 이전 속성을 덮어씁니다 동일한 이름을 가진 여러 속성을 만드는 경우; 속성에는 단일 값을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-225">In contrast, if you create multiple properties with the same name, the last property value you provide will overwrite any previous properties with the same name&#x2014;a property can only contain a single value.</span></span>


<span data-ttu-id="d8f73-226">예를 들어는 *Publish.proj* 샘플 솔루션에 파일을 살펴보세요는 **BuildProjects** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-226">For example, in the *Publish.proj* file in the sample solution, take a look at the **BuildProjects** target.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]


<span data-ttu-id="d8f73-227">이 샘플에서는 이러한 핵심 사항을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-227">In this sample, you can observe these key points:</span></span>

- <span data-ttu-id="d8f73-228">경우는 **BuildingInTeamBuild** 매개 변수를 지정 하 고 값이 **true**, 어떤이 대상 내의 태스크 실행 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-228">If the **BuildingInTeamBuild** parameter is specified and has a value of **true**, none of the tasks within this target will be executed.</span></span>
- <span data-ttu-id="d8f73-229">대상의 단일 인스턴스가 포함 된 [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-229">The target contains a single instance of the [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) task.</span></span> <span data-ttu-id="d8f73-230">이 태스크를 사용 하면 다른 MSBuild 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-230">This task lets you build other MSBuild projects.</span></span>
- <span data-ttu-id="d8f73-231">**ProjectsToBuild** 항목 작업에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-231">The **ProjectsToBuild** item is passed to the task.</span></span> <span data-ttu-id="d8f73-232">이 항목에서 정의 된 모든 프로젝트 또는 솔루션 파일의 목록을 나타낼 수 **ProjectsToBuild** 항목 그룹 내에서 요소를 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-232">This item could represent a list of project or solution files, all defined by **ProjectsToBuild** item elements within an item group.</span></span> <span data-ttu-id="d8f73-233">이 경우에 **ProjectsToBuild** 항목에서 참조 하는 단일 솔루션 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-233">In this case, the **ProjectsToBuild** item refers to a single solution file.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- <span data-ttu-id="d8f73-234">에 전달 된 속성 값은 **MSBuild** 명명 된 매개 변수를 포함 하는 작업 **OutputRoot** 및 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-234">The property values passed to the **MSBuild** task include parameters named **OutputRoot** and **Configuration**.</span></span> <span data-ttu-id="d8f73-235">그렇지 않은 경우 이러한 값이 제공 되는 경우 매개 변수 값 또는 정적 속성 값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-235">These are set to parameter values if they are provided, or static property values if they are not.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

<span data-ttu-id="d8f73-236">볼 수는 **MSBuild** 이라는 대상을 호출 하면 **빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-236">You can also see that the **MSBuild** task invokes a target named **Build**.</span></span> <span data-ttu-id="d8f73-237">이 널리 사용 되는 Visual Studio 프로젝트 파일 및 사용자 지정 프로젝트 파일에서 사용할 수에서 같은 몇 가지 기본 제공 대상 중 하나 **빌드**, **Clean**, **다시작성**, 및 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-237">This is one of several built-in targets that are widely used in Visual Studio project files and are available to you in your custom project files, like **Build**, **Clean**, **Rebuild**, and **Publish**.</span></span> <span data-ttu-id="d8f73-238">대상 및 빌드 프로세스를 제어 하 고에 대 한 작업을 사용 하는 방법에 대 한 자세히 알아보세요는 **MSBuild** 특히,이 항목의 뒷부분에 나오는 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-238">You'll learn more about using targets and tasks to control the build process, and about the **MSBuild** task in particular, later in this topic.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f73-239">대상에 대 한 자세한 내용은 참조 하십시오. [MSBuild 대상](https://msdn.microsoft.com/library/ms171462.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-239">For more information on targets, see [MSBuild Targets](https://msdn.microsoft.com/library/ms171462.aspx).</span></span>


## <a name="splitting-project-files-to-support-multiple-environments"></a><span data-ttu-id="d8f73-240">여러 환경을 지원 하기 위해 프로젝트 파일 분</span><span class="sxs-lookup"><span data-stu-id="d8f73-240">Splitting Project Files to Support Multiple Environments</span></span>

<span data-ttu-id="d8f73-241">솔루션을 테스트 서버, 준비 플랫폼 및 프로덕션 환경 같은 여러 환경을 배포할 수 있게 되기를 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-241">Suppose you want to be able to deploy a solution to multiple environments, like test servers, staging platforms, and production environments.</span></span> <span data-ttu-id="d8f73-242">구성을 이러한 환경 & #x 2014 간에 크게 달라질 수 있습니다; 뿐만 아니라 서버 이름, 연결 문자열 및 등의 관점에서 뿐만 아니라 자격 증명, 보안 설정 및 기타 요인의 많은 측면에서 잠재적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-242">The configuration may vary substantially between these environments&#x2014;not just in terms of server names, connection strings, and so on, but also potentially in terms of credentials, security settings, and lots of other factors.</span></span> <span data-ttu-id="d8f73-243">이 작업을 정기적으로 수행 해야 할 경우 대상 환경을 전환할 때마다 프로젝트 파일의 여러 속성을 편집 하려면 실제로 편리있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-243">If you need to do this regularly, it's not really expedient to edit multiple properties in your project file every time you switch the target environment.</span></span> <span data-ttu-id="d8f73-244">무한 목록이 빌드 프로세스에 제공 되는 속성 값을 요구 하도록 이상적인 솔루션 것도 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-244">Nor is it an ideal solution to require an endless list of property values to be provided to the build process.</span></span>

<span data-ttu-id="d8f73-245">다행히 대안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-245">Fortunately there is an alternative.</span></span> <span data-ttu-id="d8f73-246">MSBuild를 사용 하면 여러 프로젝트 파일에서 빌드 구성을 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-246">MSBuild lets you split your build configuration across multiple project files.</span></span> <span data-ttu-id="d8f73-247">어떻게 작동 하는지, 샘플 솔루션에 두 개의 사용자 지정 프로젝트 파일은을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-247">To see how this works, in the sample solution, notice that there are two custom project files:</span></span>

- <span data-ttu-id="d8f73-248">*Publish.proj*, 속성, 항목을 포함 하 고 모든 환경에 공통적으로 적용 되는 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-248">*Publish.proj*, which contains properties, items, and targets that are common to all environments.</span></span>
- <span data-ttu-id="d8f73-249">*Env Dev.proj*, 개발자 환경에 관련 된 속성을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-249">*Env-Dev.proj*, which contains properties that are specific to a developer environment.</span></span>

<span data-ttu-id="d8f73-250">이제 다음에 유의 *Publish.proj* 파일에 포함 되어는 [가져오기](https://msdn.microsoft.com/library/92x05xfs.aspx) 열기 바로 아래에 있는 요소 **프로젝트** 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-250">Now notice that the *Publish.proj* file includes an [Import](https://msdn.microsoft.com/library/92x05xfs.aspx) element, immediately beneath the opening **Project** tag.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]


<span data-ttu-id="d8f73-251">**가져올** 요소가 현재 MSBuild 프로젝트 파일에 다른 MSBuild 프로젝트 파일의 내용을 가져오기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-251">The **Import** element is used to import the contents of another MSBuild project file into the current MSBuild project file.</span></span> <span data-ttu-id="d8f73-252">이 경우에 **TargetEnvPropsFile** 매개 변수를 가져올 프로젝트 파일의 파일 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-252">In this case, the **TargetEnvPropsFile** parameter provides the filename of the project file you want to import.</span></span> <span data-ttu-id="d8f73-253">MSBuild를 실행할 때이 매개 변수에 대 한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-253">You can provide a value for this parameter when you run MSBuild.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]


<span data-ttu-id="d8f73-254">이 두 파일의 내용을 단일 프로젝트 파일에 효과적으로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-254">This effectively merges the contents of the two files into a single project file.</span></span> <span data-ttu-id="d8f73-255">이 방식에서는 유니버설 빌드 구성에 포함 된 하나의 프로젝트 파일 및 환경 관련 속성을 포함 하는 여러 보조 프로젝트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-255">Using this approach, you can create one project file containing your universal build configuration and multiple supplementary project files containing environment-specific properties.</span></span> <span data-ttu-id="d8f73-256">결과적으로, 다른 매개 변수 값으로 명령을 실행 하기만 하면 다른 환경에 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-256">As a result, simply running a command with a different parameter value lets you deploy your solution to a different environment.</span></span>

![](understanding-the-project-file/_static/image3.png)

<span data-ttu-id="d8f73-257">이러한 방식으로 프로젝트 파일 분할은 따라야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-257">Splitting your project files in this way is a good practice to follow.</span></span> <span data-ttu-id="d8f73-258">개발자가 여러 프로젝트 파일에서 유니버설 빌드 속성의 중복을 피하는 단일 명령을 실행 하 여 여러 환경에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-258">It allows developers to deploy to multiple environments by running a single command, while avoiding the duplication of universal build properties across multiple project files.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f73-259">사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-259">For guidance on how to customize the environment-specific project files for your own server environments, see [Configuring Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


## <a name="conclusion"></a><span data-ttu-id="d8f73-260">결론</span><span class="sxs-lookup"><span data-stu-id="d8f73-260">Conclusion</span></span>

<span data-ttu-id="d8f73-261">이 항목 MSBuild 프로젝트 파일에 대 한 일반 소개를 제공 하 고 빌드 프로세스 제어 기능을 해당 하는 사용자 지정 프로젝트 파일을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-261">This topic provided a general introduction to MSBuild project files and explained how you can create your own custom project files to control the build process.</span></span> <span data-ttu-id="d8f73-262">또한 프로젝트 파일에 유니버설 빌드 지침 및 환경별 빌드 속성을 쉽게 빌드하고 여러 대상에 프로젝트를 배포할 수 있도록 분할의 개념을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-262">It also introduced the concept of splitting project files into universal build instructions and environment-specific build properties, to make it easy to build and deploy projects to multiple destinations.</span></span>

<span data-ttu-id="d8f73-263">다음 항목인 [빌드 프로세스를 이해](understanding-the-build-process.md)를 볼 수 있게 현실적인 수준의 복잡 한 솔루션의 배포를 통해 제어 빌드 및 배포 프로젝트 파일을 사용 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-263">The next topic, [Understanding the Build Process](understanding-the-build-process.md), provides more insight into how you can use project files to control build and deployment by walking you through the deployment of a solution with a realistic level of complexity.</span></span>

## <a name="further-reading"></a><span data-ttu-id="d8f73-264">추가 정보</span><span class="sxs-lookup"><span data-stu-id="d8f73-264">Further Reading</span></span>

<span data-ttu-id="d8f73-265">프로젝트 파일 및 WPP에 대 한 자세한 소개를 참조 하십시오. [Microsoft Build Engine 안에: MSBuild를 사용 하 여 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 및 William Bartholomew, ISBN: 978-0-7356-4524-0입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f73-265">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="d8f73-266">[이전](setting-up-the-contact-manager-solution.md)
[다음](understanding-the-build-process.md)</span><span class="sxs-lookup"><span data-stu-id="d8f73-266">[Previous](setting-up-the-contact-manager-solution.md)
[Next](understanding-the-build-process.md)</span></span>
