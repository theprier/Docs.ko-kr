---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 웹 배포에 적절 한 방식을 선택 | Microsoft Docs
author: jrjlee
description: 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상을 사용 하 여 작업할 때 다음 3 가지 주요 방법 가져오는 데 사용할 수 있습니다...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 0b21852a1db2862a8452e332021b55ce7f1db423
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836600"
---
<a name="choosing-the-right-approach-to-web-deployment"></a><span data-ttu-id="1702e-103">웹 배포에 적절 한 방식을 선택</span><span class="sxs-lookup"><span data-stu-id="1702e-103">Choosing the Right Approach to Web Deployment</span></span>
====================
<span data-ttu-id="1702e-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="1702e-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="1702e-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="1702e-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="1702e-106">인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상을 사용 하 여 작업할 때 세 가지 기본 방법이 패키징된 웹 응용 프로그램을 웹 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-106">When you work with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your packaged web applications onto a web server.</span></span> <span data-ttu-id="1702e-107">하거나 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-107">You can either:</span></span>
> 
> - <span data-ttu-id="1702e-108">대상으로 하 여 원격 위치에서 응용 프로그램을 배포 합니다 *웹 배포 에이전트 서비스가* (라고도 "원격 에이전트") 대상 서버에서.</span><span class="sxs-lookup"><span data-stu-id="1702e-108">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the "remote agent") on the destination server.</span></span>
> - <span data-ttu-id="1702e-109">주문형 웹 배포 (라고도 "임시 에이전트")를 사용 하 여 원격 위치에서 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-109">Deploy the application from a remote location using Web Deploy On Demand (also known as the "temp agent").</span></span>
> - <span data-ttu-id="1702e-110">대상으로 하 여 원격 위치에서 응용 프로그램을 배포 합니다 *IIS 웹 배포 처리기* 대상 서버에서.</span><span class="sxs-lookup"><span data-stu-id="1702e-110">Deploy the application from a remote location by targeting the *IIS Web Deploy Handler* on the destination server.</span></span>
> - <span data-ttu-id="1702e-111">수동으로 웹 패키지를 대상 서버로 복사 하 고 IIS 관리자를 통해 가져와서 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-111">Deploy the application by manually copying the web package to the destination server and importing it through IIS Manager.</span></span>
> 
> <span data-ttu-id="1702e-112">대상 웹 서버를 구성 하는 방법을 사용 하려는 배포 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-112">How you configure your destination web servers will depend on which approach to deployment you want to use.</span></span> <span data-ttu-id="1702e-113">이 항목에서는 배포에 어떤 접근 방식이 적합 한지 결정 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-113">This topic will help you decide which approach to deployment is right for you.</span></span>


<span data-ttu-id="1702e-114">이 표에서 가장 일반적으로 각 접근 방식에 맞는 시나리오와 함께 각 배포 접근 방법의 주요 장단점을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-114">This table shows the main advantages and disadvantages of each deployment approach, together with the scenarios that most typically suit each approach.</span></span>

| <span data-ttu-id="1702e-115">방법</span><span class="sxs-lookup"><span data-stu-id="1702e-115">Approach</span></span> | <span data-ttu-id="1702e-116">장점</span><span class="sxs-lookup"><span data-stu-id="1702e-116">Advantages</span></span> | <span data-ttu-id="1702e-117">단점</span><span class="sxs-lookup"><span data-stu-id="1702e-117">Disadvantages</span></span> | <span data-ttu-id="1702e-118">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="1702e-118">Typical Scenarios</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1702e-119">원격 에이전트</span><span class="sxs-lookup"><span data-stu-id="1702e-119">Remote Agent</span></span> | <span data-ttu-id="1702e-120">설정 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-120">It is easy to set up.</span></span> <span data-ttu-id="1702e-121">정기적으로 웹 응용 프로그램 및 콘텐츠 업데이트에는 것이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-121">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="1702e-122">사용자는 대상 서버의 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-122">The user must be an administrator on the target server.</span></span> <span data-ttu-id="1702e-123">사용자는 대체 자격 증명을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-123">the user can't supply alternative credentials.</span></span> | <span data-ttu-id="1702e-124">개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-124">Development environments.</span></span> <span data-ttu-id="1702e-125">테스트 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-125">Test environments.</span></span> |
| <span data-ttu-id="1702e-126">임시 에이전트</span><span class="sxs-lookup"><span data-stu-id="1702e-126">Temp Agent</span></span> | <span data-ttu-id="1702e-127">대상 컴퓨터에서 웹 배포를 설치할 필요가 없습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-127">There is no need to install Web Deploy on the target computer.</span></span> <span data-ttu-id="1702e-128">최신 버전의 웹 배포를 자동으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-128">The latest version of Web Deploy is automatically used.</span></span> | <span data-ttu-id="1702e-129">사용자는 대상 서버의 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-129">The user must be an administrator on the target server.</span></span> <span data-ttu-id="1702e-130">사용자는 대체 자격 증명을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-130">The user can't supply alternative credentials.</span></span> | <span data-ttu-id="1702e-131">개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-131">Development environments.</span></span> <span data-ttu-id="1702e-132">테스트 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-132">Test environments.</span></span> |
| <span data-ttu-id="1702e-133">웹 배포 처리기</span><span class="sxs-lookup"><span data-stu-id="1702e-133">Web Deploy Handler</span></span> | <span data-ttu-id="1702e-134">관리자가 아닌 사용자가 콘텐츠를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-134">Non-administrator users can deploy content.</span></span> <span data-ttu-id="1702e-135">정기적으로 웹 응용 프로그램 및 콘텐츠 업데이트에는 것이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-135">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="1702e-136">이 설정 하기 위해 훨씬 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-136">It is a lot more complex to set up.</span></span> | <span data-ttu-id="1702e-137">스테이징 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-137">Staging environments.</span></span> <span data-ttu-id="1702e-138">인트라넷 프로덕션 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-138">Intranet production environments.</span></span> <span data-ttu-id="1702e-139">호스 티 드 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-139">Hosted environments.</span></span> |
| <span data-ttu-id="1702e-140">오프 라인 배포</span><span class="sxs-lookup"><span data-stu-id="1702e-140">Offline Deployment</span></span> | <span data-ttu-id="1702e-141">매우 설정 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-141">It is very easy to set up.</span></span> <span data-ttu-id="1702e-142">격리 된 환경에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-142">It is suitable for isolated environments.</span></span> | <span data-ttu-id="1702e-143">수동으로 서버 관리자를 복사 하 고 때마다 웹 패키지를 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-143">The server administrator must manually copy and import the web package every time.</span></span> | <span data-ttu-id="1702e-144">인터넷 프로덕션 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-144">Internet-facing production environments.</span></span> <span data-ttu-id="1702e-145">격리 된 네트워크 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-145">Isolated network environments.</span></span> |
  

## <a name="using-the-remote-agent"></a><span data-ttu-id="1702e-146">원격 에이전트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1702e-146">Using the Remote Agent</span></span>

<span data-ttu-id="1702e-147">대상 서버에서 기본 설정을 사용 하 여 웹 배포를 설치할 때 웹 배포 에이전트 서비스 ("원격 에이전트") 자동으로 설치 및 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-147">When you install Web Deploy using the default settings on a destination server, the Web Deployment Agent Service (the "remote agent") is automatically installed and started.</span></span> <span data-ttu-id="1702e-148">기본적으로 원격 에이전트는이 주소에서 HTTP 끝점을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-148">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]


> [!NOTE]
> <span data-ttu-id="1702e-149">바꿀 수 있습니다 [*server*] 웹 서버의 컴퓨터 이름을 사용 하 여 웹 서버 또는 호스트 이름에 대 한 IP 주소를 확인 하는 웹 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-149">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="1702e-150">서버 관리자는이 끝점 주소를 지정 하 여 개발자 컴퓨터 또는 빌드 서버와 같은 원격 위치에서 웹 패키지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-150">Server administrators can deploy web packages from a remote location, like a developer machine or a build server, by specifying this endpoint address.</span></span> <span data-ttu-id="1702e-151">예를 들어, Fabrikam, Inc.에서 Matt Hink 개발자 컴퓨터 ContactManager.Mvc 웹 응용 프로그램 프로젝트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-151">For example, suppose Matt Hink at Fabrikam, Inc. has built the ContactManager.Mvc web application project on his developer machine.</span></span> <span data-ttu-id="1702e-152">빌드 프로세스와 함께 웹 패키지를 생성 한 *. deploy.cmd* 웹 배포 명령이 포함 된 파일 패키지를 설치 하는 데 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-152">The build process generates a web package, together with a *.deploy.cmd* file that contains the Web Deploy commands required to install the package.</span></span> <span data-ttu-id="1702e-153">Matt TESTWEB1 서버의 서버 관리자 인 경우 그의 개발자 컴퓨터에서이 명령을 실행 하 여 테스트 웹 서버에 웹 응용 프로그램을 배포할 수 그.</span><span class="sxs-lookup"><span data-stu-id="1702e-153">If Matt is a server administrator on the TESTWEB1 server, he can deploy the web application to the test web server by running this command on his developer machine:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]


<span data-ttu-id="1702e-154">사실 실제 웹 배포 실행 파일 Matt만 입력 해야 하므로 컴퓨터 이름을 제공 하는 경우 원격 에이전트의 끝점 주소를 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-154">In actual fact, the Web Deploy executable can infer the endpoint address of the remote agent if you provide the machine name, so Matt only needs to type this:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="1702e-155">웹 배포 명령줄 구문에 대 한 자세한 내용은 및 *. deploy.cmd* 파일을 참조 하세요 [방법: 설치 된 배포 패키지를 사용 하 여 deploy.cmd 파일](https://msdn.microsoft.com/library/ff356104.aspx).</span><span class="sxs-lookup"><span data-stu-id="1702e-155">For more information on Web Deploy command-line syntax and *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="1702e-156">원격 에이전트는 원격 위치에서 콘텐츠를 배포 하는 간단한 방법을 제공 하 고이 이렇게 한 번의 클릭 또는 자동화 된 배포 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-156">The remote agent offers a straightforward way to deploy content from a remote location, and this approach can work well with one-click or automated deployment.</span></span> <span data-ttu-id="1702e-157">그러나 도메인 관리자 또는 멤버인 대상 서버의 로컬 관리자 그룹의 배포 명령을 실행 하는 사용자 수도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-157">However, the user who runs the deployment command must also be either a domain administrator or a member of the local administrators group on the destination server.</span></span> <span data-ttu-id="1702e-158">또한 원격 에이전트 명령줄에서 대체 자격 증명을 전달할 수 없습니다 있도록 기본 인증을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-158">In addition, the remote agent doesn't support basic authentication, so you can't pass alternative credentials on the command line.</span></span>

<span data-ttu-id="1702e-159">원격 에이전트는 개발 또는 테스트 시나리오에서 개발자가 테스트 서버 환경에 대 한 전체 관리자 제어도 드물지 않습니다 않았고 응용 프로그램을 다시 작성 및 다시 매우 일반적으로 배포 하는 유용한 방법을 제공합니다 자주 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-159">The remote agent provides a useful approach to deployment in development or test scenarios, where it's not uncommon for developers to have full administrator control over a test server environment, and applications are typically rebuilt and redeployed very frequently.</span></span> <span data-ttu-id="1702e-160">그러나이 방법은 스테이징 또는 프로덕션 환경에 대 한 일반적으로 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-160">However, this approach is usually less acceptable for staging or production environments.</span></span>

<span data-ttu-id="1702e-161">원격 에이전트 방법을 사용 하는 시나리오의 종단 간 예제를 참조 하세요 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-161">For an end-to-end example of a scenario that uses the remote agent approach, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span>

## <a name="using-the-temp-agent"></a><span data-ttu-id="1702e-162">임시 에이전트 사용</span><span class="sxs-lookup"><span data-stu-id="1702e-162">Using the Temp Agent</span></span>

<span data-ttu-id="1702e-163">배포 하는 임시 에이전트 방법은 원격 에이전트 접근 방식은 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-163">The temp agent approach to deployment is similar to the remote agent approach.</span></span> <span data-ttu-id="1702e-164">그러나 원격 에이전트 방법을 달리 대상 웹 서버에서 웹 배포를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-164">However, in contrast to the remote agent approach, you don't need to install Web Deploy on the destination web server.</span></span> <span data-ttu-id="1702e-165">배포를 수행 하면 대신 대상 서버에 웹 배포 에이전트 서비스의 임시 버전을 설치 하는 웹 배포 및 IIS에 콘텐츠를 배포 하려면이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-165">Instead, when you perform the deployment, Web Deploy will install a temporary version of the web deployment agent service on the destination server and will use this to deploy your content to IIS.</span></span> <span data-ttu-id="1702e-166">배포가 완료 되 면 임시 파일을 모두 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-166">When the deployment is complete, all temporary files are removed.</span></span>

<span data-ttu-id="1702e-167">임시 에이전트 공급자 설정을 사용 하 여, 추가 하려는 경우는 **/g** 배포 명령 플래그:</span><span class="sxs-lookup"><span data-stu-id="1702e-167">If you want to use the temp agent provider setting, add the **/g** flag to your deployment command:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="1702e-168">사용할 수 없습니다 임시 에이전트가 대상 컴퓨터의 웹 배포 에이전트 서비스가 설치 된 경우 서비스를 실행 하지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-168">You can't use the temp agent if the web deployment agent service is installed on the destination computer, even if the service is not running.</span></span>


<span data-ttu-id="1702e-169">이 방식의 장점은 대상 서버에서의 웹 배포 설치를 유지 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-169">The advantage of this approach is that you don't need to maintain installations of Web Deploy on your destination servers.</span></span> <span data-ttu-id="1702e-170">또한 원본 및 대상 컴퓨터를 동일한 버전의 웹 배포 실행 되도록 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-170">Furthermore, you don't need to ensure that the source and destination computers are running the same version of Web Deploy.</span></span> <span data-ttu-id="1702e-171">그러나이 방법은 저하 원격 에이전트 접근 방식으로 동일한 보안 주체 제한에서 namely 콘텐츠를 배포 하려면 대상 서버의 로컬 관리자를 사용 해야 하 고 NTLM 인증만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-171">However, this approach suffers from the same principal limitations as the remote agent approach, namely that you must be a local administrator on the destination server in order to deploy content, and only NTLM authentication is supported.</span></span> <span data-ttu-id="1702e-172">임시 에이전트 접근 방식에는 또한 대상 환경의 훨씬 초기 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-172">The temp agent approach also requires a lot more initial configuration of the destination environment.</span></span>

<span data-ttu-id="1702e-173">임시 에이전트 사용에 대 한 자세한 내용은 참조 하세요. [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx) 하 고 [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-173">For more information on using the temp agent, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx) and [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

## <a name="using-the-web-deploy-handler"></a><span data-ttu-id="1702e-174">처리기는 웹을 사용 하 여 배포</span><span class="sxs-lookup"><span data-stu-id="1702e-174">Using the Web Deploy Handler</span></span>

<span data-ttu-id="1702e-175">IIS 7 이상에 대 한 웹 배포는 IIS 웹 배포 처리기를 통해 다른 배포 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-175">For IIS 7 onwards, Web Deploy offers an alternative deployment approach through the IIS Web Deploy Handler.</span></span> <span data-ttu-id="1702e-176">웹 배포 처리기는 IIS 웹 관리 서비스 (WMSvc)를 사용자가 원격 위치에서 IIS 웹 사이트를 관리할 수 있도록 설계 된와 밀접 하 게 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-176">The Web Deploy Handler is closely integrated with the IIS Web Management Service (WMSvc), which is designed to allow users to manage IIS websites from remote locations.</span></span>

<span data-ttu-id="1702e-177">기본적으로 원격 에이전트는이 주소에서 HTTP 끝점을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-177">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]


> [!NOTE]
> <span data-ttu-id="1702e-178">바꿀 수 있습니다 [*server*] 웹 서버의 컴퓨터 이름을 사용 하 여 웹 서버 또는 호스트 이름에 대 한 IP 주소를 확인 하는 웹 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-178">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="1702e-179">원격 에이전트와 임시 에이전트를 통해 웹 배포 처리기의 가장 큰 장점은 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포할 수 있도록 IIS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-179">The big advantage of the Web Deploy Handler over the remote agent, and the temp agent, is that you can configure IIS to allow non-administrator users to deploy applications and content to specific IIS websites.</span></span> <span data-ttu-id="1702e-180">웹 배포 명령에서는 매개 변수로 대체 자격 증명을 제공할 수 있도록 웹 배포 처리기는 또한 기본 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-180">The Web Deploy Handler also supports basic authentication, so you can provide alternative credentials as parameters in your Web Deploy commands.</span></span> <span data-ttu-id="1702e-181">주요 단점은 웹 배포 처리기가 처음 설정 하 고 구성 하려면 훨씬 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-181">The major drawback is that the Web Deploy Handler is initially a lot more complicated to set up and configure.</span></span>

<span data-ttu-id="1702e-182">관리자가 아닌 사용자의 경우 웹 관리 서비스 (WMSvc)만 하면 IIS에 연결할 서버 수준 연결이 아닌 사이트 수준 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-182">In the case of non-administrator users, the Web Management Service (WMSvc) will only allow the user to connect to IIS using a site-level connection, rather than a server-level connection.</span></span> <span data-ttu-id="1702e-183">특정 사이트에 액세스 하려면 끝점 주소에서 사이트별 쿼리 문자열을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-183">To access a particular site, you can include a site-specific query string in the endpoint address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]


<span data-ttu-id="1702e-184">예를 들어, 빌드 프로세스를 자동으로 모든 빌드가 성공한 후 스테이징 환경에 웹 응용 프로그램을 배포 하도록 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-184">For example, suppose a build process is configured to automatically deploy a web application to a staging environment after every successful build.</span></span> <span data-ttu-id="1702e-185">원격 에이전트 접근 방식, 사용 하는 경우 대상 서버에서 관리자로 빌드 프로세스 id를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-185">If you used the remote agent approach, you'd need to make the build process identity an administrator on your destination servers.</span></span> <span data-ttu-id="1702e-186">반면, 웹 배포 처리기 방식을 사용 하 여 제공할 수 있습니다 비관리자 사용자&#x2014;**FABRIKAM\stagingdeployer** 여기서&#x2014;이러한 특정 IIS 웹 사이트에만 되며 빌드 프로세스가 권한을 제공할 수 있습니다 웹 패키지를 배포 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-186">In contrast, using the Web Deploy Handler approach you can give a non-administrator user&#x2014;**FABRIKAM\stagingdeployer** in this case&#x2014;permission to a specific IIS website only, and the build process can provide these credentials to deploy the web package.</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]


> [!NOTE]
> <span data-ttu-id="1702e-187">웹 배포 명령줄 작업 구문에 대 한 자세한 내용은 참조 하세요. [웹 배포 명령줄 참조](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-187">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="1702e-188">사용 하 여 대 한 자세한 내용은 합니다 *. deploy.cmd* 파일을 참조 하세요 [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx).</span><span class="sxs-lookup"><span data-stu-id="1702e-188">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="1702e-189">웹 배포 처리기를 스테이징 환경, 호스팅된 환경 및 원격 액세스 서버를 사용할 수 있지만 관리자 자격 증명이 있는 인트라넷을 기반으로 프로덕션 환경에 배포 하는 유용한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-189">The Web Deploy Handler provides a useful approach to deployment in staging environments, hosted environments, and intranet-based production environments, where remote access to the server is available but administrator credentials are not.</span></span>

<span data-ttu-id="1702e-190">웹 배포 처리기 방법을 사용 하는 시나리오의 종단 간 예제를 참조 하세요 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-190">For an end-to-end example of a scenario that uses the Web Deploy Handler approach, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

## <a name="using-offline-deployment"></a><span data-ttu-id="1702e-191">오프 라인 배포를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1702e-191">Using Offline Deployment</span></span>

<span data-ttu-id="1702e-192">경우에 따라 가능한 또는 아닙니다 원격 위치에서 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포 하는 데 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-192">In some cases, it's not possible or practical to deploy applications and content to an IIS website from a remote location.</span></span> <span data-ttu-id="1702e-193">예를 들어, 원본 및 대상 컴퓨터를 격리 된 네트워크 또는 네트워크 세그먼트에 있을 수 있습니다 또는 방화벽 정책을 원격 액세스를 허용 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-193">For example, the source and destination computers may be in isolated networks or network segments, or firewall policy may not permit remote access.</span></span>

<span data-ttu-id="1702e-194">다음과 같은 시나리오에서 계속 사용할 수 있습니다 패키징 및 게시 웹 배포;의 기능 바로 사용할 수 없습니다 하 원격 위치에서.</span><span class="sxs-lookup"><span data-stu-id="1702e-194">In scenarios like these, you can still use the packaging and publishing capabilities of Web Deploy; you just can't use them from a remote location.</span></span> <span data-ttu-id="1702e-195">대신, 대상 서버에서 관리자로 서버에 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-195">Instead, an administrator on the destination server must copy the web package onto the server and import it through IIS Manager.</span></span>

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

<span data-ttu-id="1702e-196">오프 라인 배포 방식은 있는 경계 네트워크의 서버 제한 될 수 있습니다 내부 네트워크에서 컴퓨터와 연결 되는 인터넷 프로덕션 환경에서는 일반적으로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-196">The offline deployment approach is typically useful in Internet-facing production environments, where servers in a perimeter network may have restricted connectivity with computers in the internal network.</span></span>

<span data-ttu-id="1702e-197">오프 라인 배포 방법을 사용 하는 시나리오의 종단 간 예제를 참조 하세요 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-197">For an end-to-end example of a scenario that uses the offline deployment approach, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

## <a name="further-reading"></a><span data-ttu-id="1702e-198">추가 정보</span><span class="sxs-lookup"><span data-stu-id="1702e-198">Further Reading</span></span>

<span data-ttu-id="1702e-199">웹 배포 명령줄 작업 구문에 대 한 자세한 내용은 참조 하세요. [웹 배포 명령줄 참조](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-199">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="1702e-200">사용 하 여 대 한 자세한 내용은 합니다 *. deploy.cmd* 파일을 참조 하세요 [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx).</span><span class="sxs-lookup"><span data-stu-id="1702e-200">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>

<span data-ttu-id="1702e-201">원격 컴퓨터에서 웹 패키지를 배포할 수 있는 다양 한 방법에 대 한 보다 일반적인 지침을 참조 하세요 [를 사용 하 여 웹 배포 원격](https://technet.microsoft.com/library/ee461175(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-201">For more general guidance on the different ways in which you can deploy web packages from a remote computer, see [Using Web Deploy Remotely](https://technet.microsoft.com/library/ee461175(WS.10).aspx).</span></span> <span data-ttu-id="1702e-202">주문형 웹 배포 사용에 대 한 자세한 내용은 참조 하세요. [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1702e-202">For more information on using Web Deploy On Demand, see [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1702e-203">[이전](configuring-server-environments-for-web-deployment.md)
> [다음](scenario-configuring-a-test-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="1702e-203">[Previous](configuring-server-environments-for-web-deployment.md)
[Next](scenario-configuring-a-test-environment-for-web-deployment.md)</span></span>
