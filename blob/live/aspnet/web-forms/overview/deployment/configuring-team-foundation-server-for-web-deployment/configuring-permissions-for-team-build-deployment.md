---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: "빌드 배포 팀의 사용 권한과 구성 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 자동화 된 b의 일부로 콘텐츠 웹 서버와 데이터베이스 서버를 배포 하려면 빌드 서버에 사용할 수 있도록 권한을 구성 하는 방법을 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: cb3d013d69e36f97335ea31dd6e4997772ba2d8e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="configuring-permissions-for-team-build-deployment"></a><span data-ttu-id="e5996-103">팀에 대 한 구성 권한 빌드 배포</span><span class="sxs-lookup"><span data-stu-id="e5996-103">Configuring Permissions for Team Build Deployment</span></span>
====================
<span data-ttu-id="e5996-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="e5996-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="e5996-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="e5996-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="e5996-106">이 항목에는 자동화 된 빌드 프로세스의 일부로 콘텐츠 웹 서버와 데이터베이스 서버를 배포 하려면 빌드 서버에 사용할 수 있도록 권한을 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-106">This topic describes how to configure permissions to enable your build server to deploy content to web servers and database servers as part of an automated build process.</span></span>


<span data-ttu-id="e5996-107">이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="e5996-108">이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 빌드 프로세스에 의해 제어 되는 두 프로젝트에 파일 & #x 2014; 포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="e5996-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="e5996-109">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="e5996-110">작업 개요</span><span class="sxs-lookup"><span data-stu-id="e5996-110">Task Overview</span></span>

<span data-ttu-id="e5996-111">Team Foundation Server (TFS) 2010 빌드 서비스를 설치할 때 서비스를 실행 하려는 id를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-111">When you install the Team Foundation Server (TFS) 2010 build service, you specify the identity with which you want the service to run.</span></span> <span data-ttu-id="e5996-112">기본적으로 네트워크 서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-112">By default, this is the Network Service account.</span></span> <span data-ttu-id="e5996-113">또는 도메인 계정을 사용 하 여 실행 되도록 빌드 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-113">Alternatively, you can configure the build service to run using a domain account.</span></span>

<span data-ttu-id="e5996-114">팀 빌드를 사용 하 여 자동화 하려는 및 Windows 인증을 요구 하는 모든 배포 작업은 빌드 서비스 id를 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-114">Any deployment tasks that require Windows authentication, and that you plan to automate using Team Build, will run using the build service identity.</span></span> <span data-ttu-id="e5996-115">따라서 빌드 서비스 id를 웹 서버와 데이터베이스 서버에 필요한 사용 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-115">As such, you'll need to grant the build service identity any required permissions on your web servers and your database servers.</span></span>

> [!NOTE]
> <span data-ttu-id="e5996-116">네트워크 서비스 계정으로 시스템 계정을 사용 하 여 다른 컴퓨터를 인증.</span><span class="sxs-lookup"><span data-stu-id="e5996-116">The Network Service account uses the machine account to authenticate to other computers.</span></span> <span data-ttu-id="e5996-117">컴퓨터 계정에는 다음 양식을 사용 *[도메인 이름]\[컴퓨터 이름]***$**& #x 2014 등 **FABRIKAM\TFSBUILD$**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-117">Machine accounts take the form *[domain name]\[machine name]***$**&#x2014;for example, **FABRIKAM\TFSBUILD$**.</span></span> <span data-ttu-id="e5996-118">이와 같이 빌드 서비스가 네트워크 서비스 id를 사용 하 여 실행을 빌드 서버에 대 한 컴퓨터 계정 id에 필요한 모든 권한을 부여 해야.</span><span class="sxs-lookup"><span data-stu-id="e5996-118">As such, if your build service runs using the Network Service identity, you should grant any required permissions to the machine account identity for your build server.</span></span>


## <a name="configuring-web-server-permissions"></a><span data-ttu-id="e5996-119">웹 서버 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="e5996-119">Configuring Web Server Permissions</span></span>

<span data-ttu-id="e5996-120">에 설명 된 대로 [웹 배포에 대 한 오른쪽 접근 방식을 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), 두 가지가 주요 원격 웹 서버에 웹 패키지를 배포 하려는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-120">As described in [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), there are two main approaches you can use if you want to deploy web packages to a remote web server:</span></span>

- <span data-ttu-id="e5996-121">대상으로 하 여 원격 위치에서 응용 프로그램 배포는 *웹 배포 에이전트 서비스가* (원격 에이전트 라고도 함) 대상 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-121">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the remote agent) on the destination server.</span></span>
- <span data-ttu-id="e5996-122">대상으로 하 여 원격 위치에서 응용 프로그램 배포는 *인터넷 정보 서비스* (*IIS) 웹 배포 처리기* 대상 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-122">Deploy the application from a remote location by targeting the *Internet Information Services* (*IIS) Web Deploy Handler* on the destination server.</span></span>

<span data-ttu-id="e5996-123">원격 에이전트에는 경우 두 가지 주요 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-123">The remote agent has two key limitations in this case:</span></span>

- <span data-ttu-id="e5996-124">원격 에이전트에는 NTLM 인증만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-124">The remote agent supports only NTLM authentication.</span></span> <span data-ttu-id="e5996-125">즉, 배포 빌드 서비스 id & #x 2014 사용 해야 합니다; 다른 계정을 가장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-125">In other words, the deployment must use the build service identity&#x2014;you can't impersonate another account.</span></span>
- <span data-ttu-id="e5996-126">원격 에이전트를 사용 하려면 배포를 수행 하는 계정에 대상 서버에서 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-126">To use the remote agent, the account that performs the deployment must be an administrator on the target server.</span></span>

<span data-ttu-id="e5996-127">함께, 이러한 두 가지 제한 구성 원격 에이전트 접근 방식이 자동된 팀 빌드 배포에 대 한 바람직하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-127">Together, these two limitations make the remote agent approach undesirable for an automated Team Build deployment.</span></span> <span data-ttu-id="e5996-128">이 방법을 사용 하려면 모든 대상 웹 서버에서 관리자 계정 빌드 서비스를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-128">To use this approach, you'd need to make the build service account an administrator on any target web servers.</span></span>

<span data-ttu-id="e5996-129">반면, 웹 배포 처리기 접근 방식에서는 다양 한 장점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-129">In contrast, the Web Deploy Handler approach offers various advantages:</span></span>

- <span data-ttu-id="e5996-130">웹 배포 처리기는 IIS 웹 배포 도구 (웹 배포)를 대체 계정의 자격 증명을 전달할 수 있도록 하는 HTTPS를 통해 기본 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-130">The Web Deploy Handler supports basic authentication over HTTPS, which allows you to pass the credentials of an alternative account to the IIS Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="e5996-131">관리자가 아닌 사용자가 웹 배포 처리기를 사용 하 여 특정 IIS 웹 사이트에 콘텐츠를 배포할 수 있도록 대상 웹 서버를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-131">You can configure target web servers to allow non-administrator users to deploy content to specific IIS websites using the Web Deploy Handler.</span></span>

<span data-ttu-id="e5996-132">결과적으로, 팀 빌드 웹 패키지 배포를 자동화 하는 경우 웹 배포 처리기를 대상으로 명확 하 게 보다 선호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-132">As a result, it's clearly preferable to target the Web Deploy Handler when you automate web package deployment from Team Build.</span></span> <span data-ttu-id="e5996-133">다음은 권장 되는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-133">This is the recommended process:</span></span>

1. <span data-ttu-id="e5996-134">배포에 사용할 권한이 낮은 도메인 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-134">Create a low-privileged domain account to use for the deployment.</span></span>
2. <span data-ttu-id="e5996-135">웹 배포 처리기를 구성 하 고에 설명 된 대로 계정에는 특정 IIS 웹 사이트에 콘텐츠를 배포 하는 데 필요한 권한을 부여 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-135">Configure the Web Deploy Handler and grant the account the required permissions to deploy content to a specific IIS website, as described in [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span>
3. <span data-ttu-id="e5996-136">웹 배포를 호출 및 웹 배포 처리기 대상, 기본 인증을 사용 하 고 도메인 계정의 자격 증명을 제공을 만든 배포를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-136">Invoke Web Deploy and target the Web Deploy Handler, using basic authentication and supplying the credentials of the domain account you created, to perform the deployment.</span></span>

<span data-ttu-id="e5996-137">에 [않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션을 인증 유형을 지정 (기본 또는 NTLM), 웹 배포 자격 증명 및 환경별 프로젝트 파일에서 끝점 주소 (원격 에이전트 또는 웹 배포 처리기).</span><span class="sxs-lookup"><span data-stu-id="e5996-137">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, you specify the authentication type (basic or NTLM), the Web Deploy credentials, and the endpoint address (remote agent or Web Deploy Handler) in the environment-specific project file.</span></span> <span data-ttu-id="e5996-138">이러한 값은 작성 하 고 프로젝트 파일에서 실행 될 때 웹 배포 명령 실행에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-138">These values are used to formulate and run a Web Deploy command when the project file is executed.</span></span> <span data-ttu-id="e5996-139">자세한 내용은 참조 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-139">For more information, see [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="e5996-140">웹 배포 처리기를 권한을 구성 하는 방법을 비롯 하 여를 구성 하는 방법에 대 한 자세한 내용은 참조 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-140">For more information on configuring the Web Deploy Handler, including how to configure permissions, see [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="e5996-141">원격 에이전트를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-141">For more information on configuring the remote agent, see [Configuring a Web Server for Web Deploy Publishing (Remote Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span>

## <a name="configuring-database-server-permissions"></a><span data-ttu-id="e5996-142">데이터베이스 서버 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="e5996-142">Configuring Database Server Permissions</span></span>

<span data-ttu-id="e5996-143">SQL Server로 데이터베이스를 배포 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-143">To deploy a database to SQL Server, you must:</span></span>

- <span data-ttu-id="e5996-144">SQL Server 인스턴스에 배포 하는 계정에 대 한 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-144">Create a login for the deploying account on the SQL Server instance.</span></span>
- <span data-ttu-id="e5996-145">로그인 권한을 부여 **DBCreator** SQL Server 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-145">Grant the login **DBCreator** permissions on the SQL Server instance.</span></span>
- <span data-ttu-id="e5996-146">초기 배포 후에 로그인 추가 **db\_소유자** 대상 데이터베이스 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-146">After the initial deployment, add the login to the **db\_owner** role on the target database.</span></span> <span data-ttu-id="e5996-147">후속 배포에는 기존 데이터베이스를 수정 하지 않고 있습니다 새 데이터베이스 만들기 때문에 이것이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-147">This is required because on subsequent deployments, you're modifying an existing database rather than creating a new database.</span></span>

<span data-ttu-id="e5996-148">NTLM 인증 또는 SQL Server 인증을 사용 하 여 SQL Server 인스턴스에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-148">You can authenticate to a SQL Server instance using either NTLM authentication or SQL Server authentication:</span></span>

- <span data-ttu-id="e5996-149">NTLM 인증을 사용 하는 경우 빌드 서비스 계정에 위에 설명 된 사용 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-149">If you use NTLM authentication, you need to grant the permissions described above to the build service account.</span></span>
- <span data-ttu-id="e5996-150">SQL Server 인증을 사용 하는 경우 SQL Server 계정에 위에 설명 된 사용 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-150">If you use SQL Server authentication, you need to grant the permissions described above to the SQL Server account.</span></span> <span data-ttu-id="e5996-151">데이터베이스를 배포 하는 사용 하 여 연결 문자열에 SQL Server 사용자 이름 및 암호를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-151">You also need to include the SQL Server user name and password in the connection string you use to deploy the database.</span></span>

<span data-ttu-id="e5996-152">데이터베이스 배포에 대 한 사용 권한을 구성 하는 방법에 대 한 단계별 정보를 참조 하십시오. [웹 배포 게시에 대 한 데이터베이스 서버 구성](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-152">For step-by-step details on how to configure permissions for database deployment, see [Configuring a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="e5996-153">결론</span><span class="sxs-lookup"><span data-stu-id="e5996-153">Conclusion</span></span>

<span data-ttu-id="e5996-154">이 시점에서 필요한 권한, 사용자에 게 열기 인증 옵션과 함께 팀 빌드 웹 응용 프로그램 및 데이터베이스 배포를 자동화 하는 경우를 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-154">At this point, you should understand the permissions required, together with the authentication options open to you, when you automate web application and database deployments from Team Build.</span></span> <span data-ttu-id="e5996-155">또한 IIS 웹 서버와 SQL Server 데이터베이스 서버에 필요한 권한을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-155">You should also be able to implement the necessary permissions on IIS web servers and SQL Server database servers.</span></span>

## <a name="further-reading"></a><span data-ttu-id="e5996-156">추가 정보</span><span class="sxs-lookup"><span data-stu-id="e5996-156">Further Reading</span></span>

<span data-ttu-id="e5996-157">원격 배포를 지원할 Windows 서버 환경 구성에 대 한 자세한 내용은 참조 하십시오. [웹 배포에 대 한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5996-157">For more information on configuring Windows server environments to support remote deployment, see [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="e5996-158">이전</span><span class="sxs-lookup"><span data-stu-id="e5996-158">Previous</span></span>](deploying-a-specific-build.md)
