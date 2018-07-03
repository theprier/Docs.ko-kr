---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: (Azure 사용 하 여 실제 클라우드 앱 빌드) 모든 것을 자동화 | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
ms.technology: ''
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: 45d3d72454852217303050d17b678c4a5710dcb5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376785"
---
<a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="0bb4e-104">(Azure 사용 하 여 실제 클라우드 앱 빌드) 모든 것을 자동화합니다</span><span class="sxs-lookup"><span data-stu-id="0bb4e-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="0bb4e-105">하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0bb4e-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="0bb4e-106">[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="0bb4e-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="0bb4e-107">합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="0bb4e-108">13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="0bb4e-109">전자책 소개를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="0bb4e-110">살펴보겠습니다 처음 세 패턴은 모든 소프트웨어 개발 프로젝트에 있지만 클라우드 프로젝트에 특히에 실제로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="0bb4e-111">이 패턴은 개발 작업을 자동화 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="0bb4e-112">중요 한 항목을 있기 수동 프로세스 속도가 느리고 오류가 발생 하기 쉽습니다. 가능 하면 빠르고 안정적으로 agile 워크플로 설정으로 많은 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="0bb4e-113">되므로 고유 하 게 클라우드 개발에 대 한 온-프레미스 환경에서 자동화 하기가 어렵거나 되는 많은 작업을 쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="0bb4e-114">예를 들어, 전체 테스트를 설정할 수 있습니다 새 웹 서버와 백 엔드 Vm을 포함 하 여 환경, 데이터베이스, blob storage (파일 저장소), 큐 등입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="0bb4e-115">DevOps 워크플로</span><span class="sxs-lookup"><span data-stu-id="0bb4e-115">DevOps Workflow</span></span>

<span data-ttu-id="0bb4e-116">"DevOps." 라는 용어를 듣고 점점 더</span><span class="sxs-lookup"><span data-stu-id="0bb4e-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="0bb4e-117">용어는 소프트웨어를 효율적으로 개발 하기 위해 개발 및 운영 작업을 통합 해야 하는 인식에서 개발 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="0bb4e-118">사용 하도록 설정 하려는 워크플로 종류가 하나는 응용 프로그램을 개발, 배포의 프로덕션 사용에 대해 알아봅니다, 지금까지 배운에 대 한 응답에서이 변경 하 수 사이클 반복 하 여 빠르고 안정적으로.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="0bb4e-119">일부 성공적인 클라우드 개발 팀은 하루에 여러 번 라이브 환경에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="0bb4e-120">주 버전을 배포 하는 데 Azure 팀 업데이트 하지만 이제 2 ~ 3 개월 마다 모든 2 ~ 3 일 및 주 릴리스 2 ~ 3 주마다 부분 업데이트를 릴리스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="0bb4e-121">해당 주기를 실제로 사용 하면 고객 피드백에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="0bb4e-122">이 작업을 수행 하기 위해 반복 하 고 안정적 이며 예측 가능한 이며 낮은 주기 시간에는 개발 및 배포 주기를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps 워크플로](automate-everything/_static/image1.png)

<span data-ttu-id="0bb4e-124">즉, 기간 사이의 시간 기능에 대 한 아이디어가 있는 경우 고객은 사용 하 고 피드백을 제공 하는 경우 가능한 한 짧은 것 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="0bb4e-125">처음 세 패턴이 모든 항목이 소스 제어를 자동화 하 고 해당 유형의 프로세스를 사용 하도록 설정 하기 위해 권장 되는 모범 사례에 대 한 모든는 지속적인 통합 및 업데이트-키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="0bb4e-126">Azure 관리 스크립트</span><span class="sxs-lookup"><span data-stu-id="0bb4e-126">Azure management scripts</span></span>

<span data-ttu-id="0bb4e-127">에 [이 전자책은 소개](introduction.md), Azure 관리 포털-웹 기반 콘솔을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="0bb4e-128">관리 포털을 사용 하면 모니터링 하 고 모든 Azure에서 배포한 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="0bb4e-129">웹 앱 및 Vm과 같은 서비스를 삭제, 해당 서비스를 구성, 모니터링 서비스 작업을 만들고 등 쉬운 경우</span><span class="sxs-lookup"><span data-stu-id="0bb4e-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="0bb4e-130">뛰어난 도구 이지만 사용 하는 수동 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="0bb4e-131">특히 팀 환경에서에서 권장 하는 모든 규모의 프로덕션 응용 프로그램을 개발 하려는 경우 포털 배우고 Azure를 탐색 하기 위해 UI 통해 이동 하 고 반복 해 서 수행 됩니다 하는 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="0bb4e-132">관리 포털에서 또는 Visual Studio에서 수동으로 수행할 수 있는 거의 모든 REST 관리 API를 호출 하 여 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="0bb4e-133">사용 하 여 스크립트를 작성할 수 있습니다 [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), 또는 같은 오픈 소스 프레임 워크를 사용할 수 있습니다 [Chef](http://www.opscode.com/chef/) 하거나 [Puppet](http://puppetlabs.com/puppet/what-is-puppet)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="0bb4e-134">또한 Mac 또는 Linux 환경에서 Bash 명령줄 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="0bb4e-135">Azure는 다양 한 이러한 모든 환경에 대 한 스크립팅 Api 있고는 [.NET 관리 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) 스크립트 대신 코드를 작성 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="0bb4e-136">Fix It 응용 프로그램에 대 한 테스트 환경을 만들고 해당 환경에 프로젝트를 배포 프로세스를 자동화 하는 몇 가지 Windows PowerShell 스크립트 만들었습니다 및 이러한 스크립트의 내용 중 일부를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="0bb4e-137">환경 생성 스크립트</span><span class="sxs-lookup"><span data-stu-id="0bb4e-137">Environment creation script</span></span>

<span data-ttu-id="0bb4e-138">살펴보겠습니다 첫 번째 스크립트 라고 *새로 만들기-AzureWebsiteEnv.ps1*합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="0bb4e-139">Fix It 테스트용으로 앱을 배포할 수 있습니다 Azure 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="0bb4e-140">이 스크립트가 수행 하는 주요 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="0bb4e-141">웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-141">Create a web app.</span></span>
- <span data-ttu-id="0bb4e-142">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-142">Create a storage account.</span></span> <span data-ttu-id="0bb4e-143">(필수 blob 및 큐에 대 한 뒷부분에서 살펴보겠지만.)</span><span class="sxs-lookup"><span data-stu-id="0bb4e-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="0bb4e-144">SQL Database 서버 및 두 개의 데이터베이스를 만듭니다: 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="0bb4e-145">저장소 계정 및 데이터베이스에 액세스 하는 앱은 사용 하는 Azure의 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="0bb4e-146">배포를 자동화 하는 데 사용할 설정 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="0bb4e-147">스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-147">Run the script</span></span>


> [!NOTE]
> <span data-ttu-id="0bb4e-148">챕터의이 부분에는 스크립트 및 명령을 실행 하기 위해 입력 하는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="0bb4e-149">이 데모 스크립트를 실행 하기 위해 알아야 할 모든 것을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="0bb4e-150">단계별 방법-을 수행-it 지침은 [부록: The이 샘플 응용 프로그램 수정](the-fix-it-sample-application.md#deploybase)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>


<span data-ttu-id="0bb4e-151">Azure 서비스를 관리 하는 PowerShell 스크립트를 실행 하려면 Azure PowerShell 콘솔을 설치 하 고 Azure 구독을 사용 하도록 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="0bb4e-152">설정한 후에 다음과 같은 명령을 사용 하 여 Fix It 환경 만들기 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="0bb4e-153">`Name` 매개 변수는 데이터베이스 및 저장소 계정을 만들 때 사용할 이름을 지정 하며 `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 만들어질 관리자 계정에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="0bb4e-154">다른 매개 변수를 살펴본 후 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell 창](automate-everything/_static/image2.png)

<span data-ttu-id="0bb4e-156">스크립트가 완료 되 면 나타나면 관리 포털에서 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="0bb4e-157">두 개의 데이터베이스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-157">You'll find two databases:</span></span>

![Databases](automate-everything/_static/image3.png)

<span data-ttu-id="0bb4e-159">저장소 계정:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-159">A storage account:</span></span>

![저장소 계정](automate-everything/_static/image4.png)

<span data-ttu-id="0bb4e-161">및 웹 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-161">And a web app:</span></span>

![웹 사이트](automate-everything/_static/image5.png)

<span data-ttu-id="0bb4e-163">에 **구성** 탭 웹 앱에 대 한 저장소 계정 설정이 있습니다 및 SQL 데이터베이스 연결 문자열 설정 수정에 대 한이 앱을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![connectionStrings 및 appSettings](automate-everything/_static/image6.png)

<span data-ttu-id="0bb4e-165">합니다 *Automation* 폴더가 포함 하 고 있습니다를  *&lt;websitename&gt;.pubxml* 파일.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="0bb4e-166">이 파일에는 MSBuild가 방금 만든 Azure 환경에 응용 프로그램을 배포 하는 데 사용할 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="0bb4e-167">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="0bb4e-168">알 수 있듯이 스크립트에 전체 테스트 환경에 만들어지고 전체 프로세스는 약 90 초 후에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="0bb4e-169">테스트 환경 만들기를 하려는 팀의 누군가가 하는 경우에 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="0bb4e-170">빠르지만 할 뿐만 아니라도 이러한 확신할 수 있습니다 사용 하 고 있다고 environment를 사용 하는 것과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="0bb4e-171">으로 확신 하는 경우 모든 사용자가 작업을 수동으로 설정 관리 포털 UI를 사용 하 여 매우 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="0bb4e-172">스크립트 살펴보기</span><span class="sxs-lookup"><span data-stu-id="0bb4e-172">A look at the scripts</span></span>

<span data-ttu-id="0bb4e-173">이 작업을 수행 하는 세 가지 스크립트 실제로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="0bb4e-174">명령줄에서 하나를 호출 하 고 자동으로 사용 하 여 다른 두 작업 중 일부를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="0bb4e-175">*새 AzureWebSiteEnv.ps1* 은 주 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="0bb4e-176">*새 AzureStorage.ps1* 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="0bb4e-177">*새 AzureSql.ps1* 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="0bb4e-178">기본 스크립트의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="0bb4e-178">Parameters in the main script</span></span>

<span data-ttu-id="0bb4e-179">기본 스크립트를 *새로 만들기-AzureWebSiteEnv.ps1*, 여러 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="0bb4e-180">두 개의 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-180">Two parameters are required:</span></span>

- <span data-ttu-id="0bb4e-181">스크립트로 생성 된 웹 앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="0bb4e-182">(URL에도 사용 됩니다. `<name>.azurewebsites.net`.)</span><span class="sxs-lookup"><span data-stu-id="0bb4e-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="0bb4e-183">스크립트가 생성 하는 데이터베이스 서버의 새 관리자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="0bb4e-184">선택적 매개 변수를 사용 하는 데이터 센터 위치 (기본값: "미국 서 부"), 데이터베이스 서버 관리자 이름 (기본값은 "dbuser"), 및 데이터베이스 서버용 방화벽 규칙을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="0bb4e-185">웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0bb4e-185">Create the web app</span></span>

<span data-ttu-id="0bb4e-186">이 스크립트는 먼저 호출 하 여 웹 앱을 만들 되는 `New-AzureWebsite` cmdlet으로 전달 되도록 웹 앱 이름 및 위치 매개 변수 값:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="0bb4e-187">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="0bb4e-187">Create the storage account</span></span>

<span data-ttu-id="0bb4e-188">기본 스크립트를 실행 합니다는 <em>새로 만들기-AzureStorage.ps1</em> 스크립트를 지정 "<em>&lt;websitename&gt;</em>저장소" 저장소 계정 이름에 대 한 동일한 데이터 센터의 위치 및 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-188">Then the main script runs the <em>New-AzureStorage.ps1</em> script, specifying "<em>&lt;websitename&gt;</em>storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="0bb4e-189">*새 AzureStorage.ps1* 호출을 `New-AzureStorageAccount` 를 만들고 저장소 계정에이 cmdlet은 계정 이름과 액세스 키 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="0bb4e-190">응용 프로그램 blob 및 큐 저장소 계정에 액세스 하려면 이러한 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="0bb4e-191">새 저장소 계정을; 항상 원하는 수 없습니다. 필요에 따라 기존 저장소 계정을 사용 하도록 지시 하는 매개 변수를 추가 하 여 스크립트를 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="0bb4e-192">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0bb4e-192">Create the databases</span></span>

<span data-ttu-id="0bb4e-193">기본 스크립트는 다음 데이터베이스 생성 스크립트를 실행 *새로 만들기-AzureSql.ps1*, 후 기본 데이터베이스 설정 및 방화벽 규칙 이름:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="0bb4e-194">데이터베이스 생성 스크립트를 개발 컴퓨터의 IP 주소를 검색 하 고 개발 컴퓨터에 연결 하 고 서버를 관리할 수 있도록 방화벽 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="0bb4e-195">그런 다음 데이터베이스 생성 스크립트를 데이터베이스를 설정 하려면 몇 가지 단계를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="0bb4e-196">사용 하 여 서버를 만드는 `New-AzureSqlDatabaseServer` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="0bb4e-197">서버를 관리 하 고 웹 앱에 연결할 수 있도록 개발 컴퓨터를 사용 하도록 설정 하는 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="0bb4e-198">서버 이름 및 자격 증명을 사용 하 여 포함 된 데이터베이스 컨텍스트를 만듭니다.는 `New-AzureSqlDatabaseServerContext` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    <span data-ttu-id="0bb4e-199">`New-PSCredentialFromPlainText` 함수를 호출 하는 스크립트에는 `ConvertTo-SecureString` 반환 고 암호를 암호화 하는 cmdlet을 `PSCredential` 개체는 동일한 형식를 `Get-Credential` cmdlet을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-199">`New-PSCredentialFromPlainText` is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="0bb4e-200">응용 프로그램 데이터베이스를 만들고 사용 하 여 멤버 자격 데이터베이스를 `New-AzureSqlDatabase` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="0bb4e-201">각 데이터베이스에 대해 로컬로 정의 된 함수 tocreates 연결 문자열을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-201">Calls a locally defined function tocreates a connection string for each database.</span></span> <span data-ttu-id="0bb4e-202">응용 프로그램 데이터베이스에 액세스 하려면 이러한 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="0bb4e-203">Get-SQLAzureDatabaseConnectionString는 연결 문자열에 제공 된 매개 변수 값에서 만든 스크립트에 정의 된 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="0bb4e-204">데이터베이스 서버 이름 및 연결 문자열을 사용 하 여 해시 테이블을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="0bb4e-205">Fix It 응용 프로그램에서는 별도 멤버 자격 및 응용 프로그램 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="0bb4e-206">단일 데이터베이스에 멤버 자격 및 응용 프로그램 데이터를 삽입할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="0bb4e-207">앱 설정 및 연결 문자열 저장</span><span class="sxs-lookup"><span data-stu-id="0bb4e-207">Store app settings and connection strings</span></span>

<span data-ttu-id="0bb4e-208">설정 및 자동으로 읽으려고 할 때 응용 프로그램에 반환 되는 내용를 재정의 하는 연결 문자열을 저장할 수 있는 기능이 azure 합니다 `appSettings` 또는 `connectionStrings` Web.config 파일의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="0bb4e-209">적용 하는 대신 이것이 [Web.config 변환](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="0bb4e-210">자세한 내용은 [Azure에서 중요 한 데이터를 저장](source-control.md#appsettings) 이 전자책의 뒷부분에 나오는.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="0bb4e-211">환경 생성 스크립트는 모든 Azure에 저장 합니다 `appSettings` 및 `connectionStrings` 응용 프로그램을 Azure에서 실행 될 때 저장소 계정 및 데이터베이스에 액세스 해야 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="0bb4e-212">[New Relic](http://newrelic.com/) 는 원격 분석 프레임 워크에서 보여준 합니다 [모니터링 및 원격 분석](monitoring-and-telemetry.md) 장입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="0bb4e-213">환경 생성 스크립트에는 New Relic 설정이 전으로 되도록 웹 앱 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="0bb4e-214">배포 준비</span><span class="sxs-lookup"><span data-stu-id="0bb4e-214">Preparing for deployment</span></span>

<span data-ttu-id="0bb4e-215">프로세스의 끝 환경 만들기 스크립트 배포 스크립트에 의해 사용 될 파일을 만드는 두 가지 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="0bb4e-216">게시 프로필을 만들고 이러한 함수 중 하나 *(&lt;websitename&gt;.pubxml* 파일).</span><span class="sxs-lookup"><span data-stu-id="0bb4e-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="0bb4e-217">에 대 한 정보를 저장 및 게시 설정을 가져오려면 Azure REST API를 호출 하는 코드를 *.publishsettings* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="0bb4e-218">템플릿 파일을 함께 해당 파일에서 정보를 사용 하 여 (*pubxml.template*)를 만드는 합니다 *.pubxml* 게시 프로필을 포함 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="0bb4e-219">이 두 단계로 Visual Studio에서 수행할 작업을 시뮬레이션: 다운로드를 *.publishsettings* 파일과 게시 프로필을 만들려면 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="0bb4e-220">다른 함수가 다른 템플릿 파일 (웹 사이트-environment.template)를 사용 하 여 만듭니다는 *웹 사이트 environment.xml* 와 함께 배포 스크립트를 사용 하는 설정이 포함 된 파일을 *.pubxml*파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="0bb4e-221">문제 해결 및 오류 처리</span><span class="sxs-lookup"><span data-stu-id="0bb4e-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="0bb4e-222">프로그램 같은 스크립트는: 실패할 수 있습니다 및 오류와 원인이 무엇에 대 한 수 만큼를 알고 싶은 힘듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="0bb4e-223">따라서 환경 생성 스크립트의 값을 변경 합니다 `VerbosePreference` 변수를 `SilentlyContinue` 에 `Continue` 모든 세부 정보 표시 메시지 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="0bb4e-224">값도 변경 합니다 `ErrorActionPreference` 변수를 `Continue` 에 `Stop`스크립트도 비종료 오류가 발생할 경우 실행이 중지 되도록:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="0bb4e-225">모든 작업을 수행 하기 전에 스크립트가 완료 되 면 경과 된 시간을 계산할 수 있도록 시작 시간을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="0bb4e-226">작업이 완료 되 면 스크립트 경과 시간이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="0bb4e-227">및 스크립트의 모든 키 작업에 대 한 자세한 정보 메시지를 예를 들어 쓰기:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="0bb4e-228">배포 스크립트</span><span class="sxs-lookup"><span data-stu-id="0bb4e-228">Deployment script</span></span>

<span data-ttu-id="0bb4e-229">무엇을 *새 AzureWebsiteEnv.ps1* 환경 만들기에 대 한 스크립트는는 *게시 AzureWebsite.ps1* 스크립트는 응용 프로그램 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="0bb4e-230">배포 스크립트에서 웹 앱의 이름을 가져옵니다 합니다 *웹 사이트 environment.xml* 환경 생성 스크립트에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="0bb4e-231">배포 사용자 암호를 가져와서 합니다 *.publishsettings* 파일:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="0bb4e-232">실행 합니다 [MSBuild](http://msbuildbook.com/) 빌드 및 프로젝트를 배포 하는 명령:</span><span class="sxs-lookup"><span data-stu-id="0bb4e-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="0bb4e-233">지정한 경우는 `Launch` 명령줄에서 매개 변수를 호출 합니다 `Show-AzureWebsite` 웹 사이트 URL에 기본 브라우저를 열고 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="0bb4e-234">이 이와 같은 명령을 사용 하 여 배포 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="0bb4e-235">열어서 완료 되 면 브라우저의 클라우드에서 실행 하는 사이트를 사용 하 여는 `<websitename>.azurewebsites.net` URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![Windows Azure에 배포 된 앱 수정](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="0bb4e-237">요약</span><span class="sxs-lookup"><span data-stu-id="0bb4e-237">Summary</span></span>

<span data-ttu-id="0bb4e-238">이러한 스크립트를 사용 하 여 동일한 단계를 항상 동일한 옵션을 사용 하 여 동일한 순서로 실행할 수 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="0bb4e-239">이렇게 하면는 팀의 각 개발자 하지 사항을 놓치 셨습니까 엉망 항목 또는 다른 팀 멤버의 환경에서 또는 프로덕션 환경에서 동일한 방식으로 작동 하지 않습니다는 자신의 컴퓨터에서 사용자 지정 배포.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="0bb4e-240">유사한 방식으로 REST API, Windows PowerShell 스크립트, API,.NET 언어 또는 Linux 또는 Mac.에서 실행할 수 있는 Bash 유틸리티를 사용 하 여 관리 포털에서 수행할 수 있는 대부분의 Azure 관리 기능을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="0bb4e-241">에 [다음 장에서](source-control.md) 소스 코드를 확인 하 고 소스 코드 리포지토리에서 스크립트를 포함 하는 중요 한 이유는 설명 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="0bb4e-242">자료</span><span class="sxs-lookup"><span data-stu-id="0bb4e-242">Resources</span></span>

- <span data-ttu-id="0bb4e-243">[PowerShell 설치 및 구성 Windows Azure에 대 한](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="0bb4e-244">Azure PowerShell cmdlet을 설치 하는 방법 및 필요한 컴퓨터에 Azure를 관리 하기 위해 계정을 인증서를 설치 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="0bb4e-245">이 자체 PowerShell 학습을 위한 리소스에 대 한 링크 수도 있기 때문에 시작 하는 것이 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="0bb4e-246">[Azure 스크립트 센터](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="0bb4e-247">WindowsAzure.com 포털 시작된 자습서, cmdlet 참조 설명서와 소스 코드 및 샘플 스크립트에 대 한 링크를 사용 하 여 Azure 서비스를 관리 하는 스크립트를 개발 하기 위한 리소스</span><span class="sxs-lookup"><span data-stu-id="0bb4e-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="0bb4e-248">[주말 Scripter: Azure 및 PowerShell을 사용 하 여 시작](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-248">[Weekend Scripter: Getting Started with Azure and PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="0bb4e-249">Windows PowerShell에 전용된 블로그의이 게시물 PowerShell을 사용 하 여 Azure 관리 기능에 대 한 훌륭한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="0bb4e-250">[Azure 플랫폼 간 명령줄 인터페이스 설치 및 구성](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="0bb4e-251">시스템을 Windows 뿐만 아니라 Mac 및 Linux에서 작동 하는 Azure 스크립팅 프레임 워크에 대 한 시작 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="0bb4e-252">[Azure Sdk 다운로드 및 도구 항목의 명령줄 도구 섹션](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="0bb4e-253">설명서 및 azure 명령줄 도구와 관련 된 다운로드 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="0bb4e-254">[Azure 관리 라이브러리 및.NET을 사용 하 여 모든 것 자동화](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="0bb4e-255">Scott hanselman이 Azure에 대 한.NET 관리 API를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="0bb4e-256">[Windows PowerShell 스크립트를 사용 하 여 개발 및 테스트 환경에 게시할](https://msdn.microsoft.com/library/azure/dn642480.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="0bb4e-257">Visual Studio 웹 프로젝트에 대 한 자동으로 생성 하는 스크립트를 게시 하는 MSDN 설명서를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="0bb4e-258">[Visual Studio 2013 용 PowerShell 도구](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="0bb4e-259">Visual Studio에서 Windows PowerShell 언어 지원을 추가 하는 visual Studio 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb4e-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0bb4e-260">[이전](introduction.md)
> [다음](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="0bb4e-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>
