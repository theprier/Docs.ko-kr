---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: "웹 패키지 배포에 대 한 매개 변수 구성 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 및 서비스 끝점 등의 매개 변수 값을 설정 하는 방법을 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: 12a4ba8ad30df43e7192500ad4514dfa9679f899
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="configuring-parameters-for-web-package-deployment"></a><span data-ttu-id="684ae-103">웹 패키지 배포에 대 한 매개 변수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-103">Configuring Parameters for Web Package Deployment</span></span>
====================
<span data-ttu-id="684ae-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="684ae-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="684ae-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="684ae-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="684ae-106">이 항목에서는 원격 IIS 웹 서버에 웹 패키지를 배포할 때 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 및 서비스 끝점 등의 매개 변수 값을 설정 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-106">This topic describes how to set parameter values, like Internet Information Services (IIS) web application names, connection strings, and service endpoints, when you deploy a web package to a remote IIS web server.</span></span>


<span data-ttu-id="684ae-107">빌드할 때 웹 응용 프로그램 프로젝트, 빌드 및 패키징 프로세스에서는 세 개의 키 파일 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-107">When you build a web application project, the build and packaging process generates three key files:</span></span>

- <span data-ttu-id="684ae-108">A *[프로젝트 이름].zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-108">A *[project name].zip* file.</span></span> <span data-ttu-id="684ae-109">웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-109">This is the web deployment package for your web application project.</span></span> <span data-ttu-id="684ae-110">이 패키지는 모든 어셈블리, 파일, 데이터베이스 스크립트 및 원격 IIS 웹 서버에서 웹 응용 프로그램을 다시 만드는 데 필요한 리소스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-110">This package contains all the assemblies, files, database scripts, and resources required to recreate your web application on a remote IIS web server.</span></span>
- <span data-ttu-id="684ae-111">A *[프로젝트 이름].deploy.cmd* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-111">A *[project name].deploy.cmd* file.</span></span> <span data-ttu-id="684ae-112">이는 원격 IIS 웹 서버에 웹 배포 패키지를 게시 하는 매개 변수가 있는 Web Deploy (MSDeploy.exe) 명령 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-112">This contains a set of parameterized Web Deploy (MSDeploy.exe) commands that publish your web deployment package to a remote IIS web server.</span></span>
- <span data-ttu-id="684ae-113">A *[프로젝트 name]. SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-113">A *[project name].SetParameters.xml* file.</span></span> <span data-ttu-id="684ae-114">MSDeploy.exe 명령에 매개 변수 값 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-114">This provides a set of parameter values to the MSDeploy.exe command.</span></span> <span data-ttu-id="684ae-115">이 파일의 값을 업데이트 하 고 웹 배포 매개 변수로 전달 된 명령줄 웹 패키지를 배포할 때 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-115">You can update the values in this file and pass it to Web Deploy as a command-line parameter when you deploy your web package.</span></span>

> [!NOTE]
> <span data-ttu-id="684ae-116">빌드 및 패키징 프로세스에 대 한 자세한 내용은 참조 하십시오. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-116">For more information on the build and packaging process, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>


<span data-ttu-id="684ae-117">*SetParameters.xml* 파일은 웹 응용 프로그램 프로젝트 파일 및 프로젝트 내에서 구성 파일에서 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-117">The *SetParameters.xml* file is dynamically generated from your web application project file and any configuration files within your project.</span></span> <span data-ttu-id="684ae-118">빌드하고 웹 게시 파이프라인 (WPP) 프로젝트를 패키지 배포 환경, 예: 대상 IIS 웹 응용 프로그램 및 데이터베이스 연결 문자열 사이 변경 가능성이 있는 변수를 많은 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-118">When you build and package your project, the Web Publishing Pipeline (WPP) will automatically detect lots of the variables that are likely to change between deployment environments, like the destination IIS web application and any database connection strings.</span></span> <span data-ttu-id="684ae-119">이러한 값은 자동으로 웹 배포 패키지에서 매개 변수가 있으며에 추가 된 *SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-119">These values are automatically parameterized in the web deployment package and added to the *SetParameters.xml* file.</span></span> <span data-ttu-id="684ae-120">예를 들어, 연결 문자열을 추가 하는 경우는 *web.config* 파일 웹 응용 프로그램 프로젝트에서 빌드 프로세스를이 변경 내용을 검색 하 고 항목을 추가 합니다는 *SetParameters.xml* 파일 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-120">For example, if you add a connection string to the *web.config* file in your web application project, the build process will detect this change and will add an entry to the *SetParameters.xml* file accordingly.</span></span>

<span data-ttu-id="684ae-121">이 자동 매개 변수화는 대부분의 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-121">In a lot of cases, this automatic parameterization will be sufficient.</span></span> <span data-ttu-id="684ae-122">그러나 응용 프로그램 설정 또는 서비스 끝점 Url과 같은 배포 환경 간에 다른 설정을 변경 해야 하는 경우 지시 해야 배포 패키지에 이러한 값을 매개 변수화 하는 에해당하는항목이추가WPP*SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-122">However, if your users need to vary other settings between deployment environments, like application settings or service endpoint URLs, you need to tell the WPP to parameterize these values in the deployment package and add corresponding entries to the *SetParameters.xml* file.</span></span> <span data-ttu-id="684ae-123">다음 섹션에서는이 작업을 수행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-123">The sections that follow explain how to do this.</span></span>

### <a name="automatic-parameterization"></a><span data-ttu-id="684ae-124">자동 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="684ae-124">Automatic Parameterization</span></span>

<span data-ttu-id="684ae-125">웹 응용 프로그램 패키지를 빌드할 때 WPP 이러한 것 들 매개 변수화 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-125">When you build and package a web application, the WPP will automatically parameterize these things:</span></span>

- <span data-ttu-id="684ae-126">대상 IIS 웹 응용 프로그램 경로 및 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-126">The destination IIS web application path and name.</span></span>
- <span data-ttu-id="684ae-127">모든 연결 문자열에 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-127">Any connection strings in your *web.config* file.</span></span>
- <span data-ttu-id="684ae-128">에 추가 하는 모든 데이터베이스에 대 한 연결 문자열은 **SQL 패키지 및 게시** 프로젝트 속성 페이지에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-128">Connection strings for any databases you add to the **Package/Publish SQL** tab in the project property pages.</span></span>

<span data-ttu-id="684ae-129">예를 들어, 빌드 및 패키징합니다 하는 경우는 [않아](the-contact-manager-solution.md) WPP 어떤 방식으로 매개 변수화 프로세스를 건드리지 않고 간단히 샘플 솔루션을 생성이 *ContactManager.Mvc.SetParameters.xml* 파일:</span><span class="sxs-lookup"><span data-stu-id="684ae-129">For example, if you were to build and package the [Contact Manager](the-contact-manager-solution.md) sample solution without touching the parameterization process in any way, the WPP would generate this *ContactManager.Mvc.SetParameters.xml* file:</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]


<span data-ttu-id="684ae-130">이 경우:</span><span class="sxs-lookup"><span data-stu-id="684ae-130">In this case:</span></span>

- <span data-ttu-id="684ae-131">**IIS 웹 응용 프로그램 이름** 매개 변수는 웹 응용 프로그램을 배포 하려면 IIS 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-131">The **IIS Web Application Name** parameter is the IIS path where you want to deploy the web application.</span></span> <span data-ttu-id="684ae-132">기본 값을 가져오는 **웹 패키지 및 게시** 프로젝트 속성 페이지의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-132">The default value is taken from the **Package/Publish Web** page in the project property pages.</span></span>
- <span data-ttu-id="684ae-133">**ApplicationServices Web.config 연결 문자열** 에서 생성 된 매개 변수는 **connectionStrings/추가** 요소에는 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-133">The **ApplicationServices-Web.config Connection String** parameter was generated from a **connectionStrings/add** element in the *web.config* file.</span></span> <span data-ttu-id="684ae-134">응용 프로그램 멤버 자격 데이터베이스에 연결 하는 데 사용 해야 하는 연결 문자열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-134">It represents the connection string that the application should use to contact the membership database.</span></span> <span data-ttu-id="684ae-135">여기 됩니다 제공 하는 값에는 배포 된 대체 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-135">The value you provide here will be substituted into the deployed *web.config* file.</span></span> <span data-ttu-id="684ae-136">배포 전에서 기본 값을 가져오는 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-136">The default value is taken from the pre-deployment *web.config* file.</span></span>

<span data-ttu-id="684ae-137">WPP에 생성 된 배포 패키지에서 이러한 속성 매개 변수화 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-137">The WPP also parameterizes these properties in the deployment package it generates.</span></span> <span data-ttu-id="684ae-138">배포 패키지를 설치할 때 이러한 속성에 대 한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-138">You can provide values for these properties when you install the deployment package.</span></span> <span data-ttu-id="684ae-139">에 설명 된 대로 수동으로 IIS 관리자를 통해 패키지를 설치 하면 [수동으로 웹 패키지 설치](manually-installing-web-packages.md), 설치 마법사에 대 한 매개 변수 값을 제공 하 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-139">If you install the package manually through IIS Manager, as described in [Manually Installing Web Packages](manually-installing-web-packages.md), the installation wizard prompts you to provide values for any parameters.</span></span> <span data-ttu-id="684ae-140">원격으로 사용 하 여 패키지를 설치 하는 경우는 *. deploy.cmd* 파일에 설명 된 대로 [웹 패키지 배포](deploying-web-packages.md),이 게 표시 되 웹 배포 *SetParameters.xml* 파일을 매개 변수 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-140">If you install the package remotely using the *.deploy.cmd* file, as described in [Deploying Web Packages](deploying-web-packages.md), Web Deploy will look to this *SetParameters.xml* file to provide the parameter values.</span></span> <span data-ttu-id="684ae-141">값을 편집할 수는 *SetParameters.xml* 파일을 수동으로 또는 자동화 된 빌드 및 배포 프로세스의 일부로 파일을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-141">You can edit the values in the *SetParameters.xml* file manually, or you can customize the file as part of an automated build and deployment process.</span></span> <span data-ttu-id="684ae-142">이 프로세스는이 항목의 뒷부분에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-142">This process is described in more detail later in this topic.</span></span>

### <a name="custom-parameterization"></a><span data-ttu-id="684ae-143">사용자 지정 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="684ae-143">Custom Parameterization</span></span>

<span data-ttu-id="684ae-144">더 복잡 한 배포 시나리오에서 프로젝트를 배포 하기 전에 추가 속성을 매개 변수화 하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-144">In more complex deployment scenarios, you'll often want to parameterize additional properties before you deploy your project.</span></span> <span data-ttu-id="684ae-145">일반적으로 모든 속성 및 설정을 대상 환경 간에 달라 집니다 매개 변수화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-145">Generally speaking, you should parameterize any properties and settings that will vary between destination environments.</span></span> <span data-ttu-id="684ae-146">이러한 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-146">These can include:</span></span>

- <span data-ttu-id="684ae-147">서비스 끝점에는 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-147">Service endpoints in the *web.config* file.</span></span>
- <span data-ttu-id="684ae-148">응용 프로그램 설정에는 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-148">Application settings in the *web.config* file.</span></span>
- <span data-ttu-id="684ae-149">하려는 다른 선언적 속성 지정 내용 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-149">Any other declarative properties that you want to prompt users to specify.</span></span>

<span data-ttu-id="684ae-150">이러한 속성을 매개 변수화 하는 가장 쉬운 방법은 추가 하는 것을 *parameters.xml* 파일을 웹 응용 프로그램 프로젝트의 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-150">The easiest way to parameterize these properties is to add a *parameters.xml* file to the root folder of your web application project.</span></span> <span data-ttu-id="684ae-151">예를 들어 연락처 관리자 솔루션에서는 ContactManager.Mvc 프로젝트에 포함 되어는 *parameters.xml* 루트 폴더에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-151">For example, in the Contact Manager solution, the ContactManager.Mvc project includes a *parameters.xml* file in the root folder.</span></span>

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

<span data-ttu-id="684ae-152">이 파일을 열는 단일 있음을 볼 수 있습니다 **매개 변수** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-152">If you open this file, you'll see that it contains a single **parameter** entry.</span></span> <span data-ttu-id="684ae-153">항목 XML 경로 언어 (XPath) 쿼리를 찾아에 ContactService Windows Communication Foundation (WCF) 서비스의 끝점 URL을 매개 변수화를 사용 하 여는 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-153">The entry uses an XML Path Language (XPath) query to locate and parameterize the endpoint URL of the ContactService Windows Communication Foundation (WCF) service in the *web.config* file.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]


<span data-ttu-id="684ae-154">외에 배포 패키지에는 끝점 URL을 매개 변수화를 WPP도 추가 하기 위해 해당 항목은 *SetParameters.xml* 배포 패키지와 함께 생성 되는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-154">In addition to parameterizing the endpoint URL in the deployment package, the WPP also adds a corresponding entry to the *SetParameters.xml* file that gets generated alongside the deployment package.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]


<span data-ttu-id="684ae-155">배포 패키지를 수동으로 설치 하는 경우 IIS 관리자는 해당 속성을 자동으로 매개 변수화 된와 함께 서비스 끝점 주소에 대 한 묻는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-155">If you install the deployment package manually, IIS Manager will prompt you for the service endpoint address alongside the properties that were parameterized automatically.</span></span> <span data-ttu-id="684ae-156">실행 하 여 배포 패키지를 설치 하는 경우는 *. deploy.cmd* 파일을 편집할 수 있습니다는 *SetParameters.xml* 파일에 대 한 값과 함께 서비스 끝점 주소에 대 한 값을 제공 하는 자동으로 매개 변수화 된는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-156">If you install the deployment package by running the *.deploy.cmd* file, you can edit the *SetParameters.xml* file to provide a value for the service endpoint address together with values for the properties that were parameterized automatically.</span></span>

<span data-ttu-id="684ae-157">만드는 방법에 대 한 자세한 내용은 *parameters.xml* 파일에서 참조 [하는 방법: 설치 되어 구성 배포 설정을 때는 패키지에 매개 변수 사용](https://msdn.microsoft.com/library/ff398068.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-157">For full details on how to create a *parameters.xml* file, see [How to: Use Parameters to Configure Deployment Settings When a Package is Installed](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="684ae-158">라는 프로시저 **Web.config 파일 설정에 대 한 배포 매개 변수를 사용 하려면** 단계별 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-158">The procedure named **To use deployment parameters for Web.config file settings** provides step-by-step instructions.</span></span>

## <a name="modifying-the-setparametersxml-file"></a><span data-ttu-id="684ae-159">SetParameters.xml 파일 수정</span><span class="sxs-lookup"><span data-stu-id="684ae-159">Modifying the SetParameters.xml File</span></span>

<span data-ttu-id="684ae-160">경우 수동으로 웹 응용 프로그램 패키지를 배포 하도록 계획 & #x 2014; 중 하나를 실행 하 여는 *. deploy.cmd* 파일 또는 명령줄 & #x 2014;에서 MSDeploy.exe를 실행 하 여 더 할 게 없습니다을 수동으로 편집 하 여 중지*SetParameters.xml* 배포 하기 전에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-160">If you plan to deploy the web application package manually&#x2014;either by running the *.deploy.cmd* file or by running MSDeploy.exe from the command line&#x2014;there's nothing to stop you manually editing the *SetParameters.xml* file prior to the deployment.</span></span> <span data-ttu-id="684ae-161">그러나 엔터프라이즈 규모 솔루션에서 작업할 경우 큰, 자동화 된 빌드 및 배포 프로세스의 일부로 웹 응용 프로그램 패키지를를 배포 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-161">However, if you're working on an enterprise-scale solution, you may need to deploy a web application package as part of a larger, automated build and deployment process.</span></span> <span data-ttu-id="684ae-162">이 시나리오에서는 Microsoft Build Engine (MSBuild)를 수정할 필요는 *SetParameters.xml* 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-162">In this scenario, you need the Microsoft Build Engine (MSBuild) to modify the *SetParameters.xml* file for you.</span></span> <span data-ttu-id="684ae-163">MSBuild를 사용 하 여 이렇게 하려면 **XmlPoke** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-163">You can do this by using the MSBuild **XmlPoke** task.</span></span>

<span data-ttu-id="684ae-164">[않아 샘플 솔루션](the-contact-manager-solution.md) 이 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-164">The [Contact Manager sample solution](the-contact-manager-solution.md) illustrates this process.</span></span> <span data-ttu-id="684ae-165">다음 코드 예제이 예제에 관련 된 정보만 표시 하도록 편집 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-165">The code examples that follow have been edited to show only the details that are relevant to this example.</span></span>

> [!NOTE]
> <span data-ttu-id="684ae-166">일반적으로 사용자 지정 프로젝트 파일에 대 한 소개와 샘플 솔루션에서 프로젝트 파일 모델의 광범위 한 개요를 참조 하십시오. [프로젝트 파일 이해](understanding-the-project-file.md) 및 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-166">For a broader overview of the project file model in the sample solution, and an introduction to custom project files in general, see [Understanding the Project File](understanding-the-project-file.md) and [Understanding the Build Process](understanding-the-build-process.md).</span></span>


<span data-ttu-id="684ae-167">관심 있는 매개 변수 값 환경별 프로젝트 파일에 속성으로 정의 된 첫째, (예를 들어 *Env Dev.proj*).</span><span class="sxs-lookup"><span data-stu-id="684ae-167">First, the parameter values of interest are defined as properties in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]


> [!NOTE]
> <span data-ttu-id="684ae-168">사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-168">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


<span data-ttu-id="684ae-169">다음으로 *Publish.proj* 파일은 이러한 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-169">Next, the *Publish.proj* file imports these properties.</span></span> <span data-ttu-id="684ae-170">때문에 각 *SetParameters.xml* 파일과 관련 된 한 *. deploy.cmd* 파일과 우리 궁극적으로 프로젝트 파일을 만들 각 호출 *. deploy.cmd* 파일, 프로젝트 파일을 만듭니다는 MSBuild *항목* 각 *. deploy.cmd* 서 대상의 속성을 정의 하 고 파일 *항목 메타 데이터*합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-170">Because each *SetParameters.xml* file is associated with a *.deploy.cmd* file, and we ultimately want the project file to invoke each *.deploy.cmd* file, the project file creates an MSBuild *item* for each *.deploy.cmd* file and defines the properties of interest as *item metadata*.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]


<span data-ttu-id="684ae-171">이 경우:</span><span class="sxs-lookup"><span data-stu-id="684ae-171">In this case:</span></span>

- <span data-ttu-id="684ae-172">**ParametersXml** 메타 데이터 값의 위치를 나타냅니다.는 *SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-172">The **ParametersXml** metadata value indicates the location of the *SetParameters.xml* file.</span></span>
- <span data-ttu-id="684ae-173">**IisWebAppName** 값은 웹 응용 프로그램을 배포 하려면 IIS 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-173">The **IisWebAppName** value is the IIS path to which you want to deploy the web application.</span></span>
- <span data-ttu-id="684ae-174">**MembershipDBConnectionString** 값은 멤버 자격 데이터베이스에 대 한 연결 문자열 및 **MembershipDBConnectionName** 값이 고 **이름** 특성 해당 매개 변수는 *SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-174">The **MembershipDBConnectionString** value is the connection string for the membership database, and the **MembershipDBConnectionName** value is the **name** attribute of the corresponding parameter in the *SetParameters.xml* file.</span></span>
- <span data-ttu-id="684ae-175">**ServiceEndpointValue** 값은 대상 서버에서 WCF 서비스에 대 한 끝점 주소 및 **ServiceEndpointParamName** 값은에서 해당 매개 변수의 이름 특성 *SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-175">The **ServiceEndpointValue** value is the endpoint address for the WCF service on the destination server, and the **ServiceEndpointParamName** value is the name attribute of the corresponding parameter in the *SetParameters.xml* file.</span></span>

<span data-ttu-id="684ae-176">마지막으로 *Publish.proj* 파일을는 **PublishWebPackages** 대상으로 사용 하 여는 **XmlPoke** 작업에서 이러한 값을 수정 하는 *SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-176">Finally, in the *Publish.proj* file, the **PublishWebPackages** target uses the **XmlPoke** task to modify these values in the *SetParameters.xml* file.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]


<span data-ttu-id="684ae-177">각 보면 **XmlPoke** 작업 4 가지 특성 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-177">You'll notice that each **XmlPoke** task specifies four attribute values:</span></span>

- <span data-ttu-id="684ae-178">**XmlInputPath** 특성은 태스크를 수정 하려는 파일을 찾을 위치를 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-178">The **XmlInputPath** attribute tells the task where to find the file you want to modify.</span></span>
- <span data-ttu-id="684ae-179">**쿼리** 특성은 변경 하려면 XML 노드를 식별 하는 XPath 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-179">The **Query** attribute is an XPath query that identifies the XML node you want to change.</span></span>
- <span data-ttu-id="684ae-180">**값** 특성은 선택 된 XML 노드를 삽입 하려면 새 값입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-180">The **Value** attribute is the new value you want to insert into the selected XML node.</span></span>
- <span data-ttu-id="684ae-181">**조건** 특성은 조건에서 작업을 실행 하거나 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-181">The **Condition** attribute is the criteria on which the task should run or not run.</span></span> <span data-ttu-id="684ae-182">이러한 경우 조건을 사용 하면에 null 또는 빈 값을 삽입 하려고 하지 않습니다는 *SetParameters.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-182">In these cases, the condition ensures that you don't try to insert a null or empty value into the *SetParameters.xml* file.</span></span>

## <a name="conclusion"></a><span data-ttu-id="684ae-183">결론</span><span class="sxs-lookup"><span data-stu-id="684ae-183">Conclusion</span></span>

<span data-ttu-id="684ae-184">이 항목의 역할을 설명는 *SetParameters.xml* 파일을 웹 응용 프로그램 프로젝트를 빌드할 때 생성 되는 방식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-184">This topic described the role of the *SetParameters.xml* file and explained how it's generated when you build a web application project.</span></span> <span data-ttu-id="684ae-185">추가 설정의 매개 변수화를 추가 하 여는 방법을 설명 하는 *parameters.xml* 파일을 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-185">It explained how you can parameterize additional settings by adding a *parameters.xml* file to your project.</span></span> <span data-ttu-id="684ae-186">도 수정 하는 방법을 설명는 *SetParameters.xml* 파일을 사용 하 여 더 큰, 자동화 된 빌드 프로세스의 일부로 **XmlPoke** 프로젝트 파일에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-186">It also described how you can modify the *SetParameters.xml* file as part of a larger, automated build process, by using the **XmlPoke** task in your project files.</span></span>

<span data-ttu-id="684ae-187">다음 항목 [웹 패키지 배포](deploying-web-packages.md), 배포 하는 방법 웹 패키지를 실행 하거나 설명의 *. deploy.cmd* 파일 또는 MSDeploy.exe를 사용 하 여 명령을 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-187">The next topic, [Deploying Web Packages](deploying-web-packages.md), describes how you can deploy a web package either by running the *.deploy.cmd* file or by using MSDeploy.exe commands directly.</span></span> <span data-ttu-id="684ae-188">두 경우 모두 지정할 수 있습니다 프로그램 *SetParameters.xml* 파일 배포 매개 변수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-188">In both cases, you can specify your *SetParameters.xml* file as a deployment parameter.</span></span>

## <a name="further-reading"></a><span data-ttu-id="684ae-189">추가 정보</span><span class="sxs-lookup"><span data-stu-id="684ae-189">Further Reading</span></span>

<span data-ttu-id="684ae-190">웹 패키지를 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-190">For information on how to create web packages, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="684ae-191">실제로 웹 패키지를 배포 하는 방법에 대 한 지침을 참조 하십시오. [웹 패키지 배포](deploying-web-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-191">For guidance on how to actually deploy a web package, see [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="684ae-192">만드는 방법에 대 한 단계별 연습은 *parameters.xml* 파일에서 참조 [하는 방법: 설치 되어 구성 배포 설정을 때는 패키지에 매개 변수 사용](https://msdn.microsoft.com/library/ff398068.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="684ae-192">For a step-by-step walkthrough on how to create a *parameters.xml* file, see [How to: Use Parameters to Configure Deployment Settings When a Package is Installed](https://msdn.microsoft.com/library/ff398068.aspx).</span></span>

<span data-ttu-id="684ae-193">매개 변수화 웹 배포에 대 한 일반적인 정보를 참조 하십시오. [웹 배포에서 매개 변수화 동작](https://go.microsoft.com/?linkid=9805119) (블로그 게시물).</span><span class="sxs-lookup"><span data-stu-id="684ae-193">For more general information on parameterization in Web Deploy, see [Web Deploy Parameterization in Action](https://go.microsoft.com/?linkid=9805119) (blog post).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="684ae-194">[이전](building-and-packaging-web-application-projects.md)
[다음](deploying-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="684ae-194">[Previous](building-and-packaging-web-application-projects.md)
[Next](deploying-web-packages.md)</span></span>
