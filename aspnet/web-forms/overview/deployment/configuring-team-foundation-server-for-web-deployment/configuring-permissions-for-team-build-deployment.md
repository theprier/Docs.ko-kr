---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 빌드 배포 팀에 대 한 권한 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 서버 및 데이터베이스 서버에는 자동화 된 b의 일부분으로 콘텐츠를 배포 하 여 빌드 서버를 사용 하도록 설정 하는 권한을 구성 하는 방법을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: f84e72bd5991b0407008ccdaff5243979cbb986e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384664"
---
<a name="configuring-permissions-for-team-build-deployment"></a><span data-ttu-id="4db16-103">빌드 배포 팀에 대 한 권한 구성</span><span class="sxs-lookup"><span data-stu-id="4db16-103">Configuring Permissions for Team Build Deployment</span></span>
====================
<span data-ttu-id="4db16-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="4db16-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="4db16-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="4db16-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="4db16-106">이 항목에서는 자동화 된 빌드 프로세스의 일부로 콘텐츠 웹 서버와 데이터베이스 서버를 배포 하 여 빌드 서버를 사용 하도록 설정 하는 권한을 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-106">This topic describes how to configure permissions to enable your build server to deploy content to web servers and database servers as part of an automated build process.</span></span>


<span data-ttu-id="4db16-107">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="4db16-108">이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="4db16-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="4db16-109">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="4db16-110">작업 개요</span><span class="sxs-lookup"><span data-stu-id="4db16-110">Task Overview</span></span>

<span data-ttu-id="4db16-111">Team Foundation Server (TFS) 2010 빌드 서비스를 설치할 때 서비스를 실행 하려는 id를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-111">When you install the Team Foundation Server (TFS) 2010 build service, you specify the identity with which you want the service to run.</span></span> <span data-ttu-id="4db16-112">기본적으로 네트워크 서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-112">By default, this is the Network Service account.</span></span> <span data-ttu-id="4db16-113">또는 도메인 계정을 사용 하 여 실행 하도록 빌드 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-113">Alternatively, you can configure the build service to run using a domain account.</span></span>

<span data-ttu-id="4db16-114">Windows 인증 및 Team Build를 사용 하 여 자동화할 하도록 계획 해야 하는 배포 작업은 빌드 서비스 id를 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-114">Any deployment tasks that require Windows authentication, and that you plan to automate using Team Build, will run using the build service identity.</span></span> <span data-ttu-id="4db16-115">따라서 빌드 서비스 id를 웹 서버 및 데이터베이스 서버에 대 한 필수 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-115">As such, you'll need to grant the build service identity any required permissions on your web servers and your database servers.</span></span>

> [!NOTE]
> <span data-ttu-id="4db16-116">네트워크 서비스 계정 컴퓨터 계정을 사용 하 여 다른 컴퓨터를 인증.</span><span class="sxs-lookup"><span data-stu-id="4db16-116">The Network Service account uses the machine account to authenticate to other computers.</span></span> <span data-ttu-id="4db16-117">컴퓨터 계정 형태가 * [도메인 이름]\[컴퓨터 이름] ***$**&#x2014;예를 들어 **FABRIKAM\TFSBUILD$**.</span><span class="sxs-lookup"><span data-stu-id="4db16-117">Machine accounts take the form *[domain name]\[machine name]***$**&#x2014;for example, **FABRIKAM\TFSBUILD$**.</span></span> <span data-ttu-id="4db16-118">이와 같이 빌드 서비스는 네트워크 서비스 id를 사용 하 여를 실행 하는 경우 빌드 서버에 대 한 컴퓨터 계정 id에 필요한 권한을 부여 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-118">As such, if your build service runs using the Network Service identity, you should grant any required permissions to the machine account identity for your build server.</span></span>


## <a name="configuring-web-server-permissions"></a><span data-ttu-id="4db16-119">웹 서버 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="4db16-119">Configuring Web Server Permissions</span></span>

<span data-ttu-id="4db16-120">에 설명 된 대로 [웹 배포에 오른쪽 접근 방식을 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), 두 가지 기본 원격 웹 서버에 웹 패키지를 배포 하려는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-120">As described in [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), there are two main approaches you can use if you want to deploy web packages to a remote web server:</span></span>

- <span data-ttu-id="4db16-121">대상으로 하 여 원격 위치에서 응용 프로그램을 배포 합니다 *웹 배포 에이전트 서비스가* (라고도: 원격 에이전트) 대상 서버에서.</span><span class="sxs-lookup"><span data-stu-id="4db16-121">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the remote agent) on the destination server.</span></span>
- <span data-ttu-id="4db16-122">대상으로 하 여 원격 위치에서 응용 프로그램을 배포 합니다 *인터넷 정보 서비스* (*IIS) 웹 배포 처리기* 대상 서버에서.</span><span class="sxs-lookup"><span data-stu-id="4db16-122">Deploy the application from a remote location by targeting the *Internet Information Services* (*IIS) Web Deploy Handler* on the destination server.</span></span>

<span data-ttu-id="4db16-123">원격 에이전트에는 경우 두 개의 키 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-123">The remote agent has two key limitations in this case:</span></span>

- <span data-ttu-id="4db16-124">원격 에이전트에는 NTLM 인증만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-124">The remote agent supports only NTLM authentication.</span></span> <span data-ttu-id="4db16-125">즉, 배포 빌드 서비스 id를 사용 해야 합니다&#x2014;다른 계정을 가장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-125">In other words, the deployment must use the build service identity&#x2014;you can't impersonate another account.</span></span>
- <span data-ttu-id="4db16-126">원격 에이전트를 사용 하려면 배포를 수행 하는 계정은 대상 서버의 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-126">To use the remote agent, the account that performs the deployment must be an administrator on the target server.</span></span>

<span data-ttu-id="4db16-127">함께 이러한 두 가지 제한 사항 확인 원격 에이전트 접근 방식은 팀 빌드 배포 자동화를 위해 바람직하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-127">Together, these two limitations make the remote agent approach undesirable for an automated Team Build deployment.</span></span> <span data-ttu-id="4db16-128">이 방법을 사용 하려면 모든 대상 웹 서버에서 관리자 계정 빌드 서비스를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-128">To use this approach, you'd need to make the build service account an administrator on any target web servers.</span></span>

<span data-ttu-id="4db16-129">반면, 웹 배포 처리기 접근 방식은 다양 한 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-129">In contrast, the Web Deploy Handler approach offers various advantages:</span></span>

- <span data-ttu-id="4db16-130">웹 배포 처리기는 IIS 웹 배포 도구 (웹 배포)를 대체 계정의 자격 증명을 전달할 수 있게 하는 HTTPS를 통해 기본 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-130">The Web Deploy Handler supports basic authentication over HTTPS, which allows you to pass the credentials of an alternative account to the IIS Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="4db16-131">관리자가 아닌 사용자가 웹 배포 처리기를 사용 하 여 특정 IIS 웹 사이트에 콘텐츠를 배포할 수 있도록 대상 웹 서버를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-131">You can configure target web servers to allow non-administrator users to deploy content to specific IIS websites using the Web Deploy Handler.</span></span>

<span data-ttu-id="4db16-132">결과적으로 더 명확 하 게 Team Build에서 웹 패키지 배포를 자동화 하는 경우 웹 배포 처리기를 대상으로 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-132">As a result, it's clearly preferable to target the Web Deploy Handler when you automate web package deployment from Team Build.</span></span> <span data-ttu-id="4db16-133">다음은 권장 되는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-133">This is the recommended process:</span></span>

1. <span data-ttu-id="4db16-134">배포에 사용할 권한이 낮은 도메인 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-134">Create a low-privileged domain account to use for the deployment.</span></span>
2. <span data-ttu-id="4db16-135">웹 배포 처리기를 구성 하 고에 설명 된 대로 계정을 특정 IIS 웹 사이트에 콘텐츠를 배포 하는 데 필요한 권한을 부여할 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-135">Configure the Web Deploy Handler and grant the account the required permissions to deploy content to a specific IIS website, as described in [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span>
3. <span data-ttu-id="4db16-136">Web Deploy를 호출 하 고 웹 배포 처리기 대상 도메인 계정의 자격 증명을 제공 및 기본 인증을 사용 하 여 작성 배포를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-136">Invoke Web Deploy and target the Web Deploy Handler, using basic authentication and supplying the credentials of the domain account you created, to perform the deployment.</span></span>

<span data-ttu-id="4db16-137">에 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션을 인증 유형을 지정 (기본 또는 NTLM), 웹 배포 자격 증명 및 환경 관련 프로젝트 파일에서 끝점 주소 (원격 에이전트 또는 웹 배포 처리기).</span><span class="sxs-lookup"><span data-stu-id="4db16-137">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, you specify the authentication type (basic or NTLM), the Web Deploy credentials, and the endpoint address (remote agent or Web Deploy Handler) in the environment-specific project file.</span></span> <span data-ttu-id="4db16-138">이러한 값을 작성 하 고 명령을 실행 하 여 웹 배포 프로젝트 파일이 실행 되는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-138">These values are used to formulate and run a Web Deploy command when the project file is executed.</span></span> <span data-ttu-id="4db16-139">자세한 내용은 [웹 배포 패키지](../web-deployment-in-the-enterprise/deploying-web-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-139">For more information, see [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="4db16-140">웹 배포 처리기, 권한을 구성 하는 방법을 비롯 하 여를 구성 하는 방법에 대 한 자세한 내용은 참조 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-140">For more information on configuring the Web Deploy Handler, including how to configure permissions, see [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="4db16-141">원격 에이전트를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-141">For more information on configuring the remote agent, see [Configuring a Web Server for Web Deploy Publishing (Remote Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span>

## <a name="configuring-database-server-permissions"></a><span data-ttu-id="4db16-142">데이터베이스 서버 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="4db16-142">Configuring Database Server Permissions</span></span>

<span data-ttu-id="4db16-143">데이터베이스에 SQL Server를 배포 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-143">To deploy a database to SQL Server, you must:</span></span>

- <span data-ttu-id="4db16-144">SQL Server 인스턴스에 배포 하는 계정에 대 한 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-144">Create a login for the deploying account on the SQL Server instance.</span></span>
- <span data-ttu-id="4db16-145">로그인에 부여할 **DBCreator** SQL Server 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-145">Grant the login **DBCreator** permissions on the SQL Server instance.</span></span>
- <span data-ttu-id="4db16-146">초기 배포 후에 로그인을 추가 합니다 **db\_소유자** 대상 데이터베이스의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-146">After the initial deployment, add the login to the **db\_owner** role on the target database.</span></span> <span data-ttu-id="4db16-147">후속 배포에는 기존 데이터베이스를 수정 하지 않고 있습니다 새 데이터베이스를 만들기 때문에 이것이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-147">This is required because on subsequent deployments, you're modifying an existing database rather than creating a new database.</span></span>

<span data-ttu-id="4db16-148">NTLM 인증 또는 SQL Server 인증을 사용 하 여 SQL Server 인스턴스를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-148">You can authenticate to a SQL Server instance using either NTLM authentication or SQL Server authentication:</span></span>

- <span data-ttu-id="4db16-149">NTLM 인증을 사용 하는 경우 빌드 서비스 계정은 위에 설명 된 사용 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-149">If you use NTLM authentication, you need to grant the permissions described above to the build service account.</span></span>
- <span data-ttu-id="4db16-150">SQL Server 인증을 사용 하는 경우 SQL Server 계정 위에 설명 된 사용 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-150">If you use SQL Server authentication, you need to grant the permissions described above to the SQL Server account.</span></span> <span data-ttu-id="4db16-151">데이터베이스를 배포 하는 연결 문자열에 SQL Server 사용자 이름 및 암호를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-151">You also need to include the SQL Server user name and password in the connection string you use to deploy the database.</span></span>

<span data-ttu-id="4db16-152">데이터베이스 배포에 대 한 사용 권한을 구성 하는 방법에 대 한 단계별 세부 정보를 참조 하세요 [웹 배포 게시에 대 한 데이터베이스 서버 구성](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-152">For step-by-step details on how to configure permissions for database deployment, see [Configuring a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="4db16-153">결론</span><span class="sxs-lookup"><span data-stu-id="4db16-153">Conclusion</span></span>

<span data-ttu-id="4db16-154">이 시점에서 필요한 사용 권한에, 열기, 인증 옵션과 함께 Team Build에서 웹 응용 프로그램 및 데이터베이스 배포를 자동화 하는 경우를 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-154">At this point, you should understand the permissions required, together with the authentication options open to you, when you automate web application and database deployments from Team Build.</span></span> <span data-ttu-id="4db16-155">또한 IIS 웹 서버와 SQL Server 데이터베이스 서버에 필요한 권한을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-155">You should also be able to implement the necessary permissions on IIS web servers and SQL Server database servers.</span></span>

## <a name="further-reading"></a><span data-ttu-id="4db16-156">추가 정보</span><span class="sxs-lookup"><span data-stu-id="4db16-156">Further Reading</span></span>

<span data-ttu-id="4db16-157">원격 배포를 지원 하도록 Windows 서버 환경 구성에 대 한 자세한 내용은 참조 하세요. [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4db16-157">For more information on configuring Windows server environments to support remote deployment, see [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4db16-158">이전</span><span class="sxs-lookup"><span data-stu-id="4db16-158">Previous</span></span>](deploying-a-specific-build.md)
