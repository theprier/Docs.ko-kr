---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 웹 배포에 적절 한 방식을 선택 | Microsoft Docs
author: jrjlee
description: 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상 작업할 때는 다음 3 가지 주요 방법 가져오는 데 사용할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d690744687af93a69743dc6ce6c853629f61f5d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="choosing-the-right-approach-to-web-deployment"></a><span data-ttu-id="e3493-103">웹 배포에 적합 한 접근 방식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-103">Choosing the Right Approach to Web Deployment</span></span>
====================
<span data-ttu-id="e3493-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="e3493-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="e3493-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="e3493-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="e3493-106">인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상 작업할 때는 다음 3 가지 주요 방법 웹 서버에 패키지에 포함 된 웹 응용 프로그램을 가져오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-106">When you work with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your packaged web applications onto a web server.</span></span> <span data-ttu-id="e3493-107">제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-107">You can either:</span></span>
> 
> - <span data-ttu-id="e3493-108">대상으로 하 여 원격 위치에서 응용 프로그램을 배포는 *웹 배포 에이전트 서비스가* (라고도 "원격 에이전트") 대상 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-108">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the "remote agent") on the destination server.</span></span>
> - <span data-ttu-id="e3493-109">웹 배포 요청 시 (또는 "임시 에이전트")를 사용 하 여 원격 위치에서 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-109">Deploy the application from a remote location using Web Deploy On Demand (also known as the "temp agent").</span></span>
> - <span data-ttu-id="e3493-110">대상으로 하 여 원격 위치에서 응용 프로그램 배포는 *IIS 웹 배포 처리기* 대상 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-110">Deploy the application from a remote location by targeting the *IIS Web Deploy Handler* on the destination server.</span></span>
> - <span data-ttu-id="e3493-111">수동으로 웹 패키지에서 대상 서버로 복사 하 고 IIS 관리자를 통해 가져와서 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-111">Deploy the application by manually copying the web package to the destination server and importing it through IIS Manager.</span></span>
> 
> <span data-ttu-id="e3493-112">대상 웹 서버를 구성 하는 방법에 사용 하려는 방법 배포에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-112">How you configure your destination web servers will depend on which approach to deployment you want to use.</span></span> <span data-ttu-id="e3493-113">이 항목은 어떤 배포 방법이 적합 한지 결정 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-113">This topic will help you decide which approach to deployment is right for you.</span></span>


<span data-ttu-id="e3493-114">이 표에서 가장 일반적으로 각 접근 방식에 따라 시나리오와 함께 각 배포 방법의 주요 장단점을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-114">This table shows the main advantages and disadvantages of each deployment approach, together with the scenarios that most typically suit each approach.</span></span>

| <span data-ttu-id="e3493-115">방법</span><span class="sxs-lookup"><span data-stu-id="e3493-115">Approach</span></span> | <span data-ttu-id="e3493-116">장점</span><span class="sxs-lookup"><span data-stu-id="e3493-116">Advantages</span></span> | <span data-ttu-id="e3493-117">단점</span><span class="sxs-lookup"><span data-stu-id="e3493-117">Disadvantages</span></span> | <span data-ttu-id="e3493-118">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="e3493-118">Typical Scenarios</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e3493-119">원격 에이전트</span><span class="sxs-lookup"><span data-stu-id="e3493-119">Remote Agent</span></span> | <span data-ttu-id="e3493-120">설정 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-120">It is easy to set up.</span></span> <span data-ttu-id="e3493-121">이 웹 응용 프로그램 및 콘텐츠를 정기적으로 업데이트에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-121">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="e3493-122">사용자는 대상 서버에서 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-122">The user must be an administrator on the target server.</span></span> <span data-ttu-id="e3493-123">사용자 대체 자격 증명을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-123">the user can't supply alternative credentials.</span></span> | <span data-ttu-id="e3493-124">개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-124">Development environments.</span></span> <span data-ttu-id="e3493-125">테스트 환경.</span><span class="sxs-lookup"><span data-stu-id="e3493-125">Test environments.</span></span> |
| <span data-ttu-id="e3493-126">임시 에이전트</span><span class="sxs-lookup"><span data-stu-id="e3493-126">Temp Agent</span></span> | <span data-ttu-id="e3493-127">대상 컴퓨터에 웹 배포를 설치 하지 않아도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-127">There is no need to install Web Deploy on the target computer.</span></span> <span data-ttu-id="e3493-128">최신 버전의 웹 배포를 자동으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-128">The latest version of Web Deploy is automatically used.</span></span> | <span data-ttu-id="e3493-129">사용자는 대상 서버에서 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-129">The user must be an administrator on the target server.</span></span> <span data-ttu-id="e3493-130">사용자 대체 자격 증명을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-130">The user can't supply alternative credentials.</span></span> | <span data-ttu-id="e3493-131">개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-131">Development environments.</span></span> <span data-ttu-id="e3493-132">테스트 환경.</span><span class="sxs-lookup"><span data-stu-id="e3493-132">Test environments.</span></span> |
| <span data-ttu-id="e3493-133">웹 배포 처리기</span><span class="sxs-lookup"><span data-stu-id="e3493-133">Web Deploy Handler</span></span> | <span data-ttu-id="e3493-134">관리자가 아닌 사용자가 콘텐츠를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-134">Non-administrator users can deploy content.</span></span> <span data-ttu-id="e3493-135">이 웹 응용 프로그램 및 콘텐츠를 정기적으로 업데이트에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-135">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="e3493-136">이를 설정 하려면 훨씬 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-136">It is a lot more complex to set up.</span></span> | <span data-ttu-id="e3493-137">스테이징 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-137">Staging environments.</span></span> <span data-ttu-id="e3493-138">인트라넷 프로덕션 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-138">Intranet production environments.</span></span> <span data-ttu-id="e3493-139">호스트 된 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-139">Hosted environments.</span></span> |
| <span data-ttu-id="e3493-140">오프 라인 배포</span><span class="sxs-lookup"><span data-stu-id="e3493-140">Offline Deployment</span></span> | <span data-ttu-id="e3493-141">매우를 설정 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-141">It is very easy to set up.</span></span> <span data-ttu-id="e3493-142">이 격리 된 환경에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-142">It is suitable for isolated environments.</span></span> | <span data-ttu-id="e3493-143">수동으로 서버 관리자를 복사 하 고 매번 웹 패키지를 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-143">The server administrator must manually copy and import the web package every time.</span></span> | <span data-ttu-id="e3493-144">인터넷 연결 프로덕션 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-144">Internet-facing production environments.</span></span> <span data-ttu-id="e3493-145">격리 된 네트워크 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-145">Isolated network environments.</span></span> |
  

## <a name="using-the-remote-agent"></a><span data-ttu-id="e3493-146">원격 에이전트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e3493-146">Using the Remote Agent</span></span>

<span data-ttu-id="e3493-147">대상 서버에서 기본 설정을 사용 하 여 웹 배포를 설치할 때 웹 배포 에이전트 서비스 ("원격 에이전트") 자동으로 설치 및 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-147">When you install Web Deploy using the default settings on a destination server, the Web Deployment Agent Service (the "remote agent") is automatically installed and started.</span></span> <span data-ttu-id="e3493-148">기본적으로 원격 에이전트는이 주소에 HTTP 끝점을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-148">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]


> [!NOTE]
> <span data-ttu-id="e3493-149">바꿀 수 있습니다 [*서버*] 웹 서버의 컴퓨터 이름, 웹 서버 또는 호스트 이름에 대 한 IP 주소 하는 확인을 웹 서버.</span><span class="sxs-lookup"><span data-stu-id="e3493-149">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="e3493-150">서버 관리자는이 끝점 주소를 지정 하 여 개발자 컴퓨터 또는 빌드 서버와 같은 원격 위치에서 웹 패키지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-150">Server administrators can deploy web packages from a remote location, like a developer machine or a build server, by specifying this endpoint address.</span></span> <span data-ttu-id="e3493-151">예를 들어, Fabrikam, Inc.에서 Matt Hink가 개발자 컴퓨터에서 ContactManager.Mvc 웹 응용 프로그램 프로젝트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-151">For example, suppose Matt Hink at Fabrikam, Inc. has built the ContactManager.Mvc web application project on his developer machine.</span></span> <span data-ttu-id="e3493-152">빌드 프로세스와 함께 웹 패키지를 생성 한 *. deploy.cmd* 패키지를 설치 하는 데 필요한 웹 배포 명령이 포함 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-152">The build process generates a web package, together with a *.deploy.cmd* file that contains the Web Deploy commands required to install the package.</span></span> <span data-ttu-id="e3493-153">Matt TESTWEB1 서버에서 서버 관리자 이면가 개발자 컴퓨터에서이 명령을 실행 하 여 테스트 웹 서버에 웹 응용 프로그램을 배포할 수 그:</span><span class="sxs-lookup"><span data-stu-id="e3493-153">If Matt is a server administrator on the TESTWEB1 server, he can deploy the web application to the test web server by running this command on his developer machine:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]


<span data-ttu-id="e3493-154">실제 팩트 Matt만에 다음과 같이 입력 해야 하므로 컴퓨터 이름을 제공 하는 경우 웹 배포 실행 파일 원격 에이전트의 끝점 주소를 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-154">In actual fact, the Web Deploy executable can infer the endpoint address of the remote agent if you provide the machine name, so Matt only needs to type this:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="e3493-155">웹 배포 명령줄 구문에 대 한 자세한 내용은 및 *. deploy.cmd* 파일, 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/library/ff356104.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-155">For more information on Web Deploy command-line syntax and *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="e3493-156">원격 에이전트는 원격 위치에서 콘텐츠를 배포 하는 간단한 방법을 제공 하 고이 방법은 한 번의 클릭 또는 자동화 된 배포 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-156">The remote agent offers a straightforward way to deploy content from a remote location, and this approach can work well with one-click or automated deployment.</span></span> <span data-ttu-id="e3493-157">그러나 대상 서버에서 로컬 관리자 그룹의 멤버 또는 도메인 관리자는 배포 명령을 실행 하는 사용자 수도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-157">However, the user who runs the deployment command must also be either a domain administrator or a member of the local administrators group on the destination server.</span></span> <span data-ttu-id="e3493-158">또한 원격 에이전트 명령줄에서 대체 자격 증명을 전달할 수 없으며 하므로 기본 인증을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-158">In addition, the remote agent doesn't support basic authentication, so you can't pass alternative credentials on the command line.</span></span>

<span data-ttu-id="e3493-159">원격 에이전트를 배포 개발 또는 테스트 시나리오를 여기서 개발자가 테스트 서버 환경에 대 한 전체 관리자 제어도 드물지 않습니다 및 응용 프로그램은 일반적으로 다시 작성 하며 매우 다시 배포에 유용한 접근 방법 제공 자주 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-159">The remote agent provides a useful approach to deployment in development or test scenarios, where it's not uncommon for developers to have full administrator control over a test server environment, and applications are typically rebuilt and redeployed very frequently.</span></span> <span data-ttu-id="e3493-160">그러나이 방법은 스테이징 또는 프로덕션 환경에 대 한 일반적으로 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-160">However, this approach is usually less acceptable for staging or production environments.</span></span>

<span data-ttu-id="e3493-161">원격 에이전트 접근 방식을 사용 하는 시나리오의 종단 간 예제를 보려면 [시나리오: 웹 배포를 위해 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-161">For an end-to-end example of a scenario that uses the remote agent approach, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span>

## <a name="using-the-temp-agent"></a><span data-ttu-id="e3493-162">임시 에이전트 사용</span><span class="sxs-lookup"><span data-stu-id="e3493-162">Using the Temp Agent</span></span>

<span data-ttu-id="e3493-163">배포 하는 임시 에이전트 방법은 원격 에이전트 접근 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-163">The temp agent approach to deployment is similar to the remote agent approach.</span></span> <span data-ttu-id="e3493-164">그러나 원격 에이전트 접근 방식을 달리 대상 웹 서버에 웹 배포를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-164">However, in contrast to the remote agent approach, you don't need to install Web Deploy on the destination web server.</span></span> <span data-ttu-id="e3493-165">배포를 수행 하는 경우 대신, 대상 서버에 웹 배포 에이전트 서비스의 임시 버전을 설치 합니다 웹 배포 및 IIS에 콘텐츠를 배포 하려면이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-165">Instead, when you perform the deployment, Web Deploy will install a temporary version of the web deployment agent service on the destination server and will use this to deploy your content to IIS.</span></span> <span data-ttu-id="e3493-166">배포가 완료 되 면 임시 파일을 모두 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-166">When the deployment is complete, all temporary files are removed.</span></span>

<span data-ttu-id="e3493-167">임시 에이전트 공급자 설정을 사용 하 여, 추가 하려는 경우는 **/g** 사용자의 배포 명령 플래그:</span><span class="sxs-lookup"><span data-stu-id="e3493-167">If you want to use the temp agent provider setting, add the **/g** flag to your deployment command:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="e3493-168">사용할 수 없습니다 임시 에이전트 웹 배포 에이전트 서비스가 대상 컴퓨터에 설치 된 경우는 서비스가 실행 되지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-168">You can't use the temp agent if the web deployment agent service is installed on the destination computer, even if the service is not running.</span></span>


<span data-ttu-id="e3493-169">이 방법의 장점은 대상 서버에 웹 배포의 설치를 유지 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-169">The advantage of this approach is that you don't need to maintain installations of Web Deploy on your destination servers.</span></span> <span data-ttu-id="e3493-170">또한 원본 및 대상 컴퓨터는 동일한 버전의 웹 배포를 실행 중인지 확인 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-170">Furthermore, you don't need to ensure that the source and destination computers are running the same version of Web Deploy.</span></span> <span data-ttu-id="e3493-171">그러나이 방법은 저하 원격 에이전트 방법으로 동일한 주 제한 사항을 즉 콘텐츠를 배포 하기 위해 대상 서버에서 로컬 관리자 여야 합니다. 및 NTLM 인증만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-171">However, this approach suffers from the same principal limitations as the remote agent approach, namely that you must be a local administrator on the destination server in order to deploy content, and only NTLM authentication is supported.</span></span> <span data-ttu-id="e3493-172">임시 에이전트 접근 방식을 대상 환경의 훨씬 더 초기 구성을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-172">The temp agent approach also requires a lot more initial configuration of the destination environment.</span></span>

<span data-ttu-id="e3493-173">임시 에이전트 사용에 대 한 자세한 내용은 참조 하십시오. [하는 방법: 설치 된 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/library/ff356104.aspx) 및 [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-173">For more information on using the temp agent, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx) and [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

## <a name="using-the-web-deploy-handler"></a><span data-ttu-id="e3493-174">처리기를 배포 하는 웹을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e3493-174">Using the Web Deploy Handler</span></span>

<span data-ttu-id="e3493-175">IIS 7부터에 대 한 웹 배포에서는 IIS 웹 배포 처리기를 통해 다른 배포 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-175">For IIS 7 onwards, Web Deploy offers an alternative deployment approach through the IIS Web Deploy Handler.</span></span> <span data-ttu-id="e3493-176">웹 배포 처리기 IIS 웹 관리 서비스 (WMSvc)를 통해 사용자가 원격 위치에서 IIS 웹 사이트를 관리할 수 있는 밀접 하 게 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-176">The Web Deploy Handler is closely integrated with the IIS Web Management Service (WMSvc), which is designed to allow users to manage IIS websites from remote locations.</span></span>

<span data-ttu-id="e3493-177">기본적으로 원격 에이전트는이 주소에 HTTP 끝점을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-177">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]


> [!NOTE]
> <span data-ttu-id="e3493-178">바꿀 수 있습니다 [*서버*] 웹 서버의 컴퓨터 이름, 웹 서버 또는 호스트 이름에 대 한 IP 주소 하는 확인을 웹 서버.</span><span class="sxs-lookup"><span data-stu-id="e3493-178">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="e3493-179">원격 에이전트와 임시 에이전트를 통해 웹 배포 처리기의 가장 큰 장점은 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포할 수 있도록 IIS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-179">The big advantage of the Web Deploy Handler over the remote agent, and the temp agent, is that you can configure IIS to allow non-administrator users to deploy applications and content to specific IIS websites.</span></span> <span data-ttu-id="e3493-180">웹 배포 명령에서는 매개 변수로 대체 자격 증명을 제공할 수 있도록 웹 배포 처리기는 또한 기본 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-180">The Web Deploy Handler also supports basic authentication, so you can provide alternative credentials as parameters in your Web Deploy commands.</span></span> <span data-ttu-id="e3493-181">주요 단점은 웹 배포 처리기가 처음 설정 및 구성에 훨씬 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-181">The major drawback is that the Web Deploy Handler is initially a lot more complicated to set up and configure.</span></span>

<span data-ttu-id="e3493-182">관리자가 아닌 사용자의 경우 웹 관리 서비스 (WMSvc)만 하면 사용자 IIS에 연결할 서버 수준 연결이 아닌 사이트 수준 연결을 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-182">In the case of non-administrator users, the Web Management Service (WMSvc) will only allow the user to connect to IIS using a site-level connection, rather than a server-level connection.</span></span> <span data-ttu-id="e3493-183">특정 사이트에 액세스 하는 끝점 주소에 사이트별 쿼리 문자열을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-183">To access a particular site, you can include a site-specific query string in the endpoint address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]


<span data-ttu-id="e3493-184">예를 들어 빌드 프로세스를 자동으로 모든 작업을 성공적으로 빌드한 후 스테이징 환경에 웹 응용 프로그램을 배포 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-184">For example, suppose a build process is configured to automatically deploy a web application to a staging environment after every successful build.</span></span> <span data-ttu-id="e3493-185">원격 에이전트 접근을 사용 하는 경우 대상 서버에서 관리자가 빌드 프로세스 id를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-185">If you used the remote agent approach, you'd need to make the build process identity an administrator on your destination servers.</span></span> <span data-ttu-id="e3493-186">반면, 웹 배포 처리기 방식을 사용 하 여 제공할 수 있습니다는 관리자가 아닌 사용자&#x2014;**FABRIKAM\stagingdeployer** 이 예제의&#x2014;이러한 특정 IIS 웹 사이트 에서만 및 빌드 프로세스에 대 한 사용 권한을 제공할 수 있습니다 웹 패키지를 배포 하는 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-186">In contrast, using the Web Deploy Handler approach you can give a non-administrator user&#x2014;**FABRIKAM\stagingdeployer** in this case&#x2014;permission to a specific IIS website only, and the build process can provide these credentials to deploy the web package.</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]


> [!NOTE]
> <span data-ttu-id="e3493-187">명령줄 작업 웹 배포 및 구문에 대 한 자세한 내용은 참조 하십시오. [배포 명령줄 참조 웹](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-187">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="e3493-188">사용 하 여 대 한 자세한 내용은 *. deploy.cmd* 파일에서 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/library/ff356104.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-188">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="e3493-189">웹 배포 처리기 배포 환경, 호스팅된 환경 및 인트라넷 기반 프로덕션 환경에서는 원격 액세스 서버를 사용할 수 있지만 관리자 자격 증명이 있는 준비에 유용한 접근 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-189">The Web Deploy Handler provides a useful approach to deployment in staging environments, hosted environments, and intranet-based production environments, where remote access to the server is available but administrator credentials are not.</span></span>

<span data-ttu-id="e3493-190">웹 배포 처리기 접근 방식을 사용 하는 시나리오의 종단 간 예제를 참조 하세요. [시나리오: 웹 배포에 대 한 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-190">For an end-to-end example of a scenario that uses the Web Deploy Handler approach, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

## <a name="using-offline-deployment"></a><span data-ttu-id="e3493-191">오프 라인 배포를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e3493-191">Using Offline Deployment</span></span>

<span data-ttu-id="e3493-192">경우에 따라 것 수 없거나 원격 위치에서 IIS 웹 사이트를 응용 프로그램 및 콘텐츠를 배포 하기에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-192">In some cases, it's not possible or practical to deploy applications and content to an IIS website from a remote location.</span></span> <span data-ttu-id="e3493-193">예를 들어 원본 및 대상 컴퓨터에 격리 된 네트워크 또는 네트워크 세그먼트 중이거나 방화벽 정책을 원격 액세스를 허용 하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-193">For example, the source and destination computers may be in isolated networks or network segments, or firewall policy may not permit remote access.</span></span>

<span data-ttu-id="e3493-194">이와 같은 시나리오에서 사용할 수 있습니다 패키징 및 게시 웹 배포;의 기능 바로 사용할 수 없습니다는 원격 위치에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-194">In scenarios like these, you can still use the packaging and publishing capabilities of Web Deploy; you just can't use them from a remote location.</span></span> <span data-ttu-id="e3493-195">대신, 대상 서버에서 관리자는 서버에 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-195">Instead, an administrator on the destination server must copy the web package onto the server and import it through IIS Manager.</span></span>

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

<span data-ttu-id="e3493-196">오프 라인 배포 방법은 여기서 경계 네트워크에에서 서버를 제한 한 내부 네트워크의 컴퓨터와 연결 되는 인터넷 연결 프로덕션 환경에서 일반적으로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-196">The offline deployment approach is typically useful in Internet-facing production environments, where servers in a perimeter network may have restricted connectivity with computers in the internal network.</span></span>

<span data-ttu-id="e3493-197">오프 라인 배포 방법을 사용 하 여 시나리오의 종단 간 예제를 보려면 [시나리오: 웹 배포를 위해 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-197">For an end-to-end example of a scenario that uses the offline deployment approach, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

## <a name="further-reading"></a><span data-ttu-id="e3493-198">추가 정보</span><span class="sxs-lookup"><span data-stu-id="e3493-198">Further Reading</span></span>

<span data-ttu-id="e3493-199">명령줄 작업 웹 배포 및 구문에 대 한 자세한 내용은 참조 하십시오. [배포 명령줄 참조 웹](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-199">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="e3493-200">사용 하 여 대 한 자세한 내용은 *. deploy.cmd* 파일에서 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/library/ff356104.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-200">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>

<span data-ttu-id="e3493-201">원격 컴퓨터에서 웹 패키지를 배포할 수 있는 다양 한 방법에 대 한 보다 일반적인 지침을 참조 하십시오. [를 사용 하 여 웹 배포 원격으로](https://technet.microsoft.com/library/ee461175(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-201">For more general guidance on the different ways in which you can deploy web packages from a remote computer, see [Using Web Deploy Remotely](https://technet.microsoft.com/library/ee461175(WS.10).aspx).</span></span> <span data-ttu-id="e3493-202">주문형 웹 배포 사용에 대 한 자세한 내용은 참조 하십시오. [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3493-202">For more information on using Web Deploy On Demand, see [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e3493-203">[이전](configuring-server-environments-for-web-deployment.md)
> [다음](scenario-configuring-a-test-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="e3493-203">[Previous](configuring-server-environments-for-web-deployment.md)
[Next](scenario-configuring-a-test-environment-for-web-deployment.md)</span></span>
