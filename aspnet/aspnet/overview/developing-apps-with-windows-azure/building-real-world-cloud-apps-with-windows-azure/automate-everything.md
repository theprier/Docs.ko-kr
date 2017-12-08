---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: "(Azure 사용 하 여 실제 클라우드 앱 빌드) 모든 것 자동화 | Microsoft Docs"
author: MikeWasson
description: "실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: cf1cb7b07ffe8750724e58e4fb66854c9a033a54
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="000e9-104">(Azure 사용 하 여 실제 클라우드 앱 빌드) 모든 것 자동화</span><span class="sxs-lookup"><span data-stu-id="000e9-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="000e9-105">여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="000e9-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="000e9-106">[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="000e9-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="000e9-107">**실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="000e9-108">13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="000e9-109">전자책에 대 한 소개를 참조 하십시오. [첫 번째 장](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="000e9-110">살펴보게 처음 세 가지 패턴에는 실제로 소프트웨어 개발 프로젝트에 있지만 특히 클라우드 프로젝트에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="000e9-111">이 방법은 개발 작업을 자동화 하는 방법에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="000e9-112">중요 한 항목 이므로 수동 프로세스 속도가 느리고 오류가 발생 하기 쉽습니다. 가능한 쉽게 빠르고 안정적 이며 agile 워크플로 설정할 수 만큼으로 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="000e9-113">되므로 클라우드 개발에 대 한 고유 하 게 중요 한 온-프레미스 환경에서 자동화 하기 어렵거나 있는 많은 작업을 쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="000e9-114">전체 테스트를 설정할 수는 예를 들어 새 웹 서버와 백 엔드 Vm을 포함 하 여 환경, 데이터베이스, blob 저장소 (파일 저장소), 큐 등입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="000e9-115">DevOps 워크플로</span><span class="sxs-lookup"><span data-stu-id="000e9-115">DevOps Workflow</span></span>

<span data-ttu-id="000e9-116">"DevOps." 라는 용어 들은 점점 더</span><span class="sxs-lookup"><span data-stu-id="000e9-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="000e9-117">용어를 개발 및 운영 작업을 통합 소프트웨어를 효율적으로 개발 해야 인식 부족 개발.</span><span class="sxs-lookup"><span data-stu-id="000e9-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="000e9-118">사용 하도록 설정 하려는 워크플로 유형은 하나 있습니다 수 있는 응용 프로그램을 개발, 배포의 프로덕션 사용에서 배울, 학습 한 내용에 대 한 응답에서 변경할와 빠르고 안정적으로 주기를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="000e9-119">일부 성공적인 클라우드 개발 팀에서 하루에 여러 번 실제 환경에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="000e9-120">주요 배포 하는 데 Azure 팀 업데이트 2-3 개월 마다 지금은 하지만 마다 기준 2 ~ 3 일 및 주 해제 마다 2-3 주 버전 부분 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="000e9-121">해당 흐름에 실제로 사용 하면 고객의 의견에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="000e9-122">파일을 수집 하려면 반복 가능 하 고 신뢰할 수 있는 고 예측 가능 하며 낮은 주기 시간을 포함 한 개발 및 배포 주기를 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps 워크플로](automate-everything/_static/image1.png)

<span data-ttu-id="000e9-124">즉, 기능에 대 한 아이디어가 있는 경우와 고객의 사용 및 사용자 의견 제공 때 사이의 시간을 가능한 한 짧게 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="000e9-125">처음 세 가지 패턴이 모든 항목이 소스 제어를 자동화 하 고 연속 통합 및 배달-는 이러한 종류의 프로세스를 사용 하도록 설정 하기 위해 권장 되는 모범 사례에 대 한 모든 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="000e9-126">Azure 관리 스크립트</span><span class="sxs-lookup"><span data-stu-id="000e9-126">Azure management scripts</span></span>

<span data-ttu-id="000e9-127">에 [이 전자책 소개](introduction.md), Azure 관리 포털-웹 기반 콘솔 에서도 언급 했 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="000e9-128">관리 포털을 사용 하면 모니터링 하 고 모든 Azure에 배포 하는 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="000e9-129">만들기 및 삭제와 같은 웹 앱 및 Vm 서비스, 해당 서비스를 구성, 서비스 작업을 모니터링 및 등을 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="000e9-130">좋은 도구 이지만 사용 하는 수동 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="000e9-131">모든 규모의 프로덕션 응용 프로그램을 개발 하려는 경우 특히 팀 환경에서에서 권장 하는 UI 알아보고 Azure를 탐색 하려면 포털을 통해 이동 하 고 있습니다 수행할 반복적인 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="000e9-132">관리 포털에서 또는 Visual Studio에서 수동으로 수행할 수 있는 거의 모든 나머지 관리 API를 호출 하 여 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="000e9-133">사용 하 여 스크립트를 작성할 수 있습니다 [Windows PowerShell](https://msdn.microsoft.com/en-us/library/windowsazure/jj156055.aspx), 같은 오픈 소스 프레임 워크를 사용할 수 있습니다 또는 [Chef](http://www.opscode.com/chef/) 또는 [Puppet](http://puppetlabs.com/puppet/what-is-puppet)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/en-us/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="000e9-134">또한 Mac 또는 Linux 환경에서 Bash 명령줄 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="000e9-135">Azure은 서로 다른 이러한 모든 환경에 대 한 Api 스크립트는 [.NET 관리 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) 스크립트 대신 코드를 작성 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="000e9-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="000e9-136">수정 앱에 대 한 테스트 환경을 직접 만들어 해당 환경에 프로젝트를 배포 및 프로세스를 자동화 하는 일부 Windows PowerShell 스크립트를 만들고 및 일부 이러한 스크립트의 내용을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="000e9-137">환경 만들기 스크립트</span><span class="sxs-lookup"><span data-stu-id="000e9-137">Environment creation script</span></span>

<span data-ttu-id="000e9-138">첫 번째 스크립트에서 살펴보게 라는 *새로 AzureWebsiteEnv.ps1*합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="000e9-139">수정 응용 프로그램에서 테스트를 위해 배포할 수 있음을 Azure 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="000e9-140">이 스크립트는 수행 하는 기본 작업에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="000e9-141">웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-141">Create a web app.</span></span>
- <span data-ttu-id="000e9-142">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-142">Create a storage account.</span></span> <span data-ttu-id="000e9-143">(필수 blob, 큐에 대 한 뒷부분에서 확인할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="000e9-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="000e9-144">SQL 데이터베이스 서버 및 두 개의 데이터베이스를 만듭니다: 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="000e9-145">저장소 계정 및 데이터베이스에 액세스 하는 앱은 사용 하는 Azure의 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="000e9-146">배포를 자동화 하는 설정 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="000e9-147">스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="000e9-147">Run the script</span></span>


> [!NOTE]
> <span data-ttu-id="000e9-148">이 부분의 장 스크립트와 명령을 실행 하기 위해 입력 하는 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="000e9-149">이 데모는 스크립트를 실행 하기 위해 알아야 하는 데 필요한 모든 것을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="000e9-150">사용법-하려는 do-it 단계별로 참조 [부록: The 것 샘플 응용 프로그램 수정](the-fix-it-sample-application.md#deploybase)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>


<span data-ttu-id="000e9-151">Azure 서비스를 관리 하는 PowerShell 스크립트를 실행 하려면 Azure PowerShell 콘솔을 설치 하 고 Azure 구독과 함께 작동 하도록 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="000e9-152">설정한 후에이 이와 같은 명령을 사용 하 여 수정 환경 만들기 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="000e9-153">`Name` 매개 변수는 데이터베이스 및 저장소 계정을 만들 때 사용할 이름을 지정 및 `SqlDatabasePassword` 매개 변수는 SQL 데이터베이스에 대해 만들 관리자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="000e9-154">다른 매개 변수는에서 살펴보게 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell 창](automate-everything/_static/image2.png)

<span data-ttu-id="000e9-156">스크립트가 완료 된 후 나타나면 관리 포털에서 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="000e9-157">두 개의 데이터베이스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-157">You'll find two databases:</span></span>

![데이터베이스](automate-everything/_static/image3.png)

<span data-ttu-id="000e9-159">저장소 계정:</span><span class="sxs-lookup"><span data-stu-id="000e9-159">A storage account:</span></span>

![저장소 계정](automate-everything/_static/image4.png)

<span data-ttu-id="000e9-161">및 웹 앱:</span><span class="sxs-lookup"><span data-stu-id="000e9-161">And a web app:</span></span>

![웹 사이트](automate-everything/_static/image5.png)

<span data-ttu-id="000e9-163">에 **구성** 탭 웹 앱에 대 한 저장소 계정 설정에 및 SQL 데이터베이스 연결 문자열에 대 한 설정의 수정이 반영 것 앱 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![connectionStrings 및 appSettings](automate-everything/_static/image6.png)

<span data-ttu-id="000e9-165">*자동화* 폴더 이제도 포함 되어는  *&lt;websitename&gt;.pubxml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="000e9-166">이 파일에는 MSBuild에서 방금 만든 Azure 환경에 응용 프로그램 배포에 사용할 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="000e9-167">예:</span><span class="sxs-lookup"><span data-stu-id="000e9-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="000e9-168">볼 수 있듯이 스크립트에 전체 테스트 환경 만들어지고 전체 프로세스는 약 90 초 후에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="000e9-169">테스트 환경 만들기가 팀의 다른 사용자에 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="000e9-170">도 빠르지만 할 뿐만 아니라 하나를 사용 하는 동일한 환경을 사용 하 고 있는지 확신할은 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="000e9-171">으로 확신 하는 경우 모든 사용자가 설정 수동으로 관리 포털 UI를 사용 하 여 매우 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="000e9-172">스크립트를 살펴보면</span><span class="sxs-lookup"><span data-stu-id="000e9-172">A look at the scripts</span></span>

<span data-ttu-id="000e9-173">이 작업을 수행 하는 3 개의 스크립트 실제로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="000e9-174">명령줄에서 하나를 호출 하 고 자동으로 사용 하 여 다른 두 작업 중 일부를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="000e9-175">*새 AzureWebSiteEnv.ps1* 은 기본 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="000e9-176">*새 AzureStorage.ps1* 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="000e9-177">*새 AzureSql.ps1* 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="000e9-178">기본 스크립트의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="000e9-178">Parameters in the main script</span></span>

<span data-ttu-id="000e9-179">기본 스크립트를 *새로 AzureWebSiteEnv.ps1*, 여러 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="000e9-180">두 개의 매개 변수 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-180">Two parameters are required:</span></span>

- <span data-ttu-id="000e9-181">스크립트를 만드는 웹 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="000e9-182">(이것은 또한 URL에 대 한 사용 되어: `<name>.azurewebsites.net`.)</span><span class="sxs-lookup"><span data-stu-id="000e9-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="000e9-183">스크립트는 데이터베이스 서버의 새 관리자에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="000e9-184">선택적 매개 변수를 사용 하는 데이터 센터 위치 (기본값: "미국 서 부"), 데이터베이스 서버 관리자 이름 (기본값은 "dbuser") 및 데이터베이스 서버에 대 한 방화벽 규칙을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="000e9-185">웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="000e9-185">Create the web app</span></span>

<span data-ttu-id="000e9-186">이 스크립트는 것을 호출 하 여 웹 앱을 만들기는 `New-AzureWebsite` cmdlet을 전달 하 여 웹 응용 프로그램 이름 및 위치 매개 변수 값:</span><span class="sxs-lookup"><span data-stu-id="000e9-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="000e9-187">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="000e9-187">Create the storage account</span></span>

<span data-ttu-id="000e9-188">기본 스크립트를 실행 한 후의 *새로 AzureStorage.ps1* 스크립트를 지정 하 "*&lt;websitename&gt;*저장소" 저장소 계정 이름에 대 한 동일한 데이터 센터의 위치 및 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-188">Then the main script runs the *New-AzureStorage.ps1* script, specifying "*&lt;websitename&gt;*storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="000e9-189">*새 AzureStorage.ps1* 호출은 `New-AzureStorageAccount` cmdlet을 저장소 계정 이므로 만들 계정 이름과 액세스 키 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="000e9-190">응용 프로그램의 blob 및 큐 저장소 계정에 액세스 하기 위해 이러한 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="000e9-191">새 저장소 계정을; 만들려면 항상 할 수 있습니다. 필요에 따라 기존 저장소 계정을 사용 하도록 지시 하는 매개 변수를 추가 하 여 스크립트를 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="000e9-192">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="000e9-192">Create the databases</span></span>

<span data-ttu-id="000e9-193">기본 스크립트는 다음 데이터베이스 생성 스크립트 실행 *새로 AzureSql.ps1*, after 기본 데이터베이스 설정 및 방화벽 규칙 이름:</span><span class="sxs-lookup"><span data-stu-id="000e9-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="000e9-194">데이터베이스 생성 스크립트는 개발 컴퓨터의 IP 주소를 검색 하 고 개발 컴퓨터에 연결 하 고 서버를 관리할 수 있도록 방화벽 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="000e9-195">그런 다음 데이터베이스 생성 스크립트 데이터베이스를 설정 하려면 몇 가지 단계를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="000e9-196">서버를 사용 하 여 만듭니다는 `New-AzureSqlDatabaseServer` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="000e9-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="000e9-197">서버를 관리 하 고 웹 응용 프로그램에 연결할 수 있도록 개발 컴퓨터를 사용 하도록 설정 하는 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="000e9-198">서버 이름 및 자격 증명을 사용 하 여 포함 된 데이터베이스 컨텍스트를 만듭니다.는 `New-AzureSqlDatabaseServerContext` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="000e9-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    <span data-ttu-id="000e9-199">`New-PSCredentialFromPlainText`호출 하는 스크립트에는 함수는 `ConvertTo-SecureString` 암호화 암호와 반환 하는 cmdlet는 `PSCredential` 형식 동일 개체는 `Get-Credential` cmdlet에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-199">`New-PSCredentialFromPlainText` is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="000e9-200">응용 프로그램 데이터베이스를 만들고 사용 하 여 멤버 자격 데이터베이스는 `New-AzureSqlDatabase` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="000e9-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="000e9-201">각 데이터베이스에 대해 로컬로 정의 된 함수 tocreates 연결 문자열을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-201">Calls a locally defined function tocreates a connection string for each database.</span></span> <span data-ttu-id="000e9-202">응용 프로그램 데이터베이스에 액세스 하려면이 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="000e9-203">Get SQLAzureDatabaseConnectionString 연결 문자열에 제공 된 매개 변수 값에서 생성 된 스크립트에 정의 된 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="000e9-204">데이터베이스 서버 이름 및 연결 문자열에 있는 해시 테이블을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="000e9-205">수정 앱은 별도 구성원 및 응용 프로그램 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="000e9-206">단일 데이터베이스에 멤버 자격 및 응용 프로그램 데이터를 저장 하는 것도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="000e9-207">앱 설정 및 연결 문자열 저장</span><span class="sxs-lookup"><span data-stu-id="000e9-207">Store app settings and connection strings</span></span>

<span data-ttu-id="000e9-208">Azure를 읽으려고 할 때 응용 프로그램에 반환 되는 항목을 자동으로 재정의 하는 연결 문자열 및 설정을 저장할 수 있도록 하는 기능에는 `appSettings` 또는 `connectionStrings` Web.config 파일의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="000e9-209">이것은 적용 하는 대신 [Web.config 변환](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="000e9-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="000e9-210">자세한 내용은 참조 [Azure에서 중요 한 데이터를 저장](source-control.md#appsettings) 이 전자책 (영문)의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="000e9-211">모든 Azure에 저장 환경 만들기 스크립트는 `appSettings` 및 `connectionStrings` 응용 프로그램이 Azure에서 실행 될 때 저장소 계정 및 데이터베이스에 액세스 해야 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="000e9-212">[New Relic](http://newrelic.com/) 에 대해서도 설명 하는 원격 분석 프레임 워크는 [모니터링 및 원격 분석](monitoring-and-telemetry.md) 장 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="000e9-213">환경 만들기 스크립트에는 웹 앱 설정을 New Relic에서 선택 되었는지 확인을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="000e9-214">배포 준비</span><span class="sxs-lookup"><span data-stu-id="000e9-214">Preparing for deployment</span></span>

<span data-ttu-id="000e9-215">프로세스의 끝 환경 만들기 스크립트는 배포 스크립트에 의해 사용 될 파일을 만드는 두 개의 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="000e9-216">게시 프로필을 만들고 이러한 함수 중 하나 *(&lt;websitename&gt;.pubxml* 파일).</span><span class="sxs-lookup"><span data-stu-id="000e9-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="000e9-217">게시 설정을 가져오지 Azure REST API를 호출 하는 코드와의 정보를 저장 한 *.publishsettings* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="000e9-218">서식 파일을 함께 해당 파일의 정보를 사용 합니다 (*pubxml.template*)를 만드는 *.pubxml* 게시 프로필을 포함 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="000e9-219">이 두 단계로 Visual Studio에서 수행할 작업을 시뮬레이션: 다운로드 한 *.publishsettings* 파일 및 게시 프로필을 만들려고 하는 가져오기.</span><span class="sxs-lookup"><span data-stu-id="000e9-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="000e9-220">다른 함수를 만드는 다른 템플릿 파일 (웹 사이트 environment.template)를 사용 하 여 한 *웹 사이트 있는 environment.xml* 배포 스크립트와 함께 ´ ֲ 설정이 포함 된 파일의 *.pubxml*파일입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="000e9-221">문제 해결 및 오류 처리</span><span class="sxs-lookup"><span data-stu-id="000e9-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="000e9-222">스크립트는 프로그램과 마찬가지로: 실패 및 일으킨 대상에 대 한 수 만큼 자주 확인 하려면 작업을 수행 하 고 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="000e9-223">이러한 이유로 환경 만들기 스크립트의 값을 변경 하는 `VerbosePreference` 변수 `SilentlyContinue` 를 `Continue` 모든 자세한 정보 메시지가 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="000e9-224">값도 변경는 `ErrorActionPreference` 에서 변수 `Continue` 를 `Stop`스크립트도 종료 되지 않는 오류가 발생할 경우 실행이 중지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="000e9-225">모든 작업을 수행 하기 전에 수행 되는 경우에 경과 된 시간을 계산할 수 있도록 스크립트 시작 시간을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="000e9-226">작업을 완료 한 후 스크립트 경과 된 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="000e9-227">및 스크립트는 모든 키 작업에 대 한 자세한 정보 메시지를 예를 들어 쓰기:</span><span class="sxs-lookup"><span data-stu-id="000e9-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="000e9-228">배포 스크립트</span><span class="sxs-lookup"><span data-stu-id="000e9-228">Deployment script</span></span>

<span data-ttu-id="000e9-229">어떤는 *새로 AzureWebsiteEnv.ps1* 환경 만들기에 대 한 스크립트는는 *게시 AzureWebsite.ps1* 이 스크립트는 응용 프로그램 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="000e9-230">배포 스크립트에서 웹 응용 프로그램의 이름을 가져옵니다는 *웹 사이트 있는 environment.xml* 환경 만들기 스크립트에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="000e9-231">배포 사용자 암호를 가져옵니다는 *.publishsettings* 파일:</span><span class="sxs-lookup"><span data-stu-id="000e9-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="000e9-232">실행 된 [MSBuild](http://msbuildbook.com/) 빌드되고 프로젝트를 배포 하는 명령:</span><span class="sxs-lookup"><span data-stu-id="000e9-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="000e9-233">지정한 경우는 `Launch` 호출 명령줄에서 매개 변수는 `Show-AzureWebsite` cmdlet을 웹 사이트 URL로 기본 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="000e9-234">이 이와 같은 명령을 사용 하 여 배포 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="000e9-235">브라우저에는 클라우드에서 실행 중인 사이트와 함께 엽니다 완료 되 면는 `<websitename>.azurewebsites.net` URL입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![Windows Azure에 배포 된 응용 프로그램 수정](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="000e9-237">요약</span><span class="sxs-lookup"><span data-stu-id="000e9-237">Summary</span></span>

<span data-ttu-id="000e9-238">이러한 스크립트와 동일한 단계 항상 동일한 옵션을 사용 하 여 같은 순서로 실행 되어야 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="000e9-239">이 팀의 각 개발자 하지 않습니다 무언가 누락 또는 잘못 변경 했더라도 계속 되거나 같은 방식으로 다른 팀 멤버의 환경이 나 프로덕션 환경에서 실제로 작동 하지 않는 자신의 컴퓨터에서 사용자 지정 항목을 배포 하 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="000e9-240">이와 비슷한 방식으로에서는 REST API, Windows PowerShell 스크립트, API,.NET 언어 또는 Linux 또는 Mac.에서 실행할 수 있는 Bash 유틸리티를 사용 하 여 관리 포털에서 수행할 수 있는 대부분의 Azure 관리 기능을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="000e9-241">에 [다음 장에서](source-control.md) 소스 코드를 보면 알아보고 소스 코드 리포지토리에 스크립트를 포함 해야 하는 이유를 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="000e9-242">리소스</span><span class="sxs-lookup"><span data-stu-id="000e9-242">Resources</span></span>

- <span data-ttu-id="000e9-243">[설치 하 고 Azure에 대 한 Windows PowerShell 구성](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="000e9-244">Azure PowerShell cmdlet을 설치 하는 방법 및 필요한 Azure를 관리 하기 위해 컴퓨터에 계정을 인증서를 설치 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="000e9-245">이것이 자체 PowerShell 학습을 위한 리소스의 링크를 포함 하기 때문에 시작 하는 좋은 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="000e9-246">[Azure 스크립트 센터](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="000e9-247">자습서 시작된, cmdlet 참조 설명서 및 소스 코드 및 예제 스크립트에 대 한 링크가 있는 Azure 서비스를 관리 하는 스크립트를 개발을 위한 리소스를 WindowsAzure.com 포털</span><span class="sxs-lookup"><span data-stu-id="000e9-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="000e9-248">[주말 Scripter: Azure 및 PowerShell 시작](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-248">[Weekend Scripter: Getting Started with Azure and PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="000e9-249">Windows PowerShell로 전용된 블로그의이 게시물 PowerShell을 사용 하 여 Azure 관리 기능에 대 한 기능을 충분히 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="000e9-250">[설치 하 고 Azure 플랫폼 간 명령줄 인터페이스를 구성](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="000e9-251">시작 자습서 시스템 Mac 및 Linux 뿐 아니라 Windows에서 작동 하는 Azure 스크립팅 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="000e9-252">[Azure Sdk를 다운로드 및 도구 항목의 명령줄 도구 섹션](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="000e9-253">설명서 및 명령줄 도구를 Azure에 대 한 관련 다운로드에 대 한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="000e9-254">[Azure 관리 라이브러리 및.NET을 사용 하 여 모든 것 자동화](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="000e9-255">Scott Hanselman Azure에 대 한.NET 관리 API를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="000e9-256">[Windows PowerShell 스크립트를 사용 하 여 개발 및 테스트 환경에 게시 하도록](https://msdn.microsoft.com/library/azure/dn642480.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="000e9-257">사용 하는 방법을 설명 하는 MSDN 설명서는 Visual Studio 웹 프로젝트에 자동으로 생성 하는 스크립트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="000e9-258">[Visual Studio 2013 용 PowerShell 도구](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="000e9-259">Visual Studio에서 Windows PowerShell에 대 한 언어 지원을 추가 하는 visual Studio 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="000e9-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="000e9-260">[이전](introduction.md)
[다음](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="000e9-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>
