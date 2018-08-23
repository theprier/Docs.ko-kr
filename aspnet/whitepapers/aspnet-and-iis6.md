---
uid: whitepapers/aspnet-and-iis6
title: Iis 6.0에서 ASP.NET 1.1 실행 | Microsoft Docs
author: rick-anderson
description: Windows Server 2003에서 IIS 6.0 및 ASP.NET 1.1 모두를 포함 하는 동안 이러한 구성 요소는 기본적으로 비활성화 됩니다. 이 백서에서는 IIS 6.0을 사용 하도록 설정 하는 중...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 38cd0abc1e9133b9b86cff6dd2759ce98ac5a115
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828830"
---
<a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="9db51-104">Iis 6.0에서 ASP.NET 1.1 실행</span><span class="sxs-lookup"><span data-stu-id="9db51-104">Running ASP.NET 1.1 with IIS 6.0</span></span>
====================
> <span data-ttu-id="9db51-105">Windows Server 2003에서 IIS 6.0 및 ASP.NET 1.1 모두를 포함 하는 동안 이러한 구성 요소는 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="9db51-106">이 백서는 IIS 6.0 및 ASP.NET 1.1을 사용 하도록 설정 하는 방법에 설명 하 고 IIS 및 ASP.NET에서 최적의 성능을 얻기 위해 다양 한 구성 설정을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="9db51-107">IIS 6.0 및 ASP.NET 1.1에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>


<span data-ttu-id="9db51-108">또한 인터넷 정보 서버 (IIS) 버전 6.0의 최신 버전을 포함 하는 Windows Server 2003을 사용 하 여 ASP.NET 1.1 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="9db51-109">IIS 6.0 및 ASP.NET 1.1 원활 하 게 통합 하도록 설계 되어 새 IIS 6.0 작업자 프로세스 모델 이제 기본적으로 ASP.NET을</span><span class="sxs-lookup"><span data-stu-id="9db51-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="9db51-110">ASP.NET 1.1은 기본적으로 설치 되지</span><span class="sxs-lookup"><span data-stu-id="9db51-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="9db51-111">Microsoft의 서버 운영 체제의 이전 버전과 달리 인터넷 정보 서버 (IIS) 기본적으로 사용 되지 않습니다. ASP.NET 1.1 것도 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="9db51-112">두 가지 방법으로 IIS를 사용 하도록 설정:</span><span class="sxs-lookup"><span data-stu-id="9db51-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="9db51-113">옵션 #1-IIS 서버 구성 마법사 사용</span><span class="sxs-lookup"><span data-stu-id="9db51-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="9db51-114">Windows Server 2003을 새 ' 서버 구성 마법사 '를 제대로 원하는 모드에서 서버를 구성 하기 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="9db51-115">마법사를 시작 하려면-관리자 권한으로 로그인 해야 하는 마법사를 실행 하려면 참고로 이동: 시작 | 프로그램 | 관리 도구 및 선택 ' 구성 서버 '입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="9db51-116">한 번 선택한 ' 서버 구성 마법사 ' 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="9db51-117">클릭 ' 다음 &gt;'.</span><span class="sxs-lookup"><span data-stu-id="9db51-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="9db51-118">클릭 ' 다음 &gt;'</span><span class="sxs-lookup"><span data-stu-id="9db51-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="9db51-119">이 화면에서 선택 해야 합니다 ' 구성 옵션으로 응용 프로그램 서버 (IIS, ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="9db51-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="9db51-120">클릭 ' 다음 &gt;'.</span><span class="sxs-lookup"><span data-stu-id="9db51-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="9db51-121">응용 프로그램 서버로 서버를 구성 하려면을 선택한 후 추가 기능을 설치할지 확인이 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="9db51-122">두 옵션 모두 기본적으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-122">Neither option is selected by default.</span></span> <span data-ttu-id="9db51-123">ASP.NET을 자동으로 사용 하려면 선택 ' ASP를 사용 하도록 설정 합니다. NET'.</span><span class="sxs-lookup"><span data-stu-id="9db51-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="9db51-124">클릭 ' 다음 &gt;'.</span><span class="sxs-lookup"><span data-stu-id="9db51-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="9db51-125">이 화면 설치 옵션은 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="9db51-126">클릭 ' 다음 &gt;'.</span><span class="sxs-lookup"><span data-stu-id="9db51-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="9db51-127">선택한 옵션을 설치 하는 동안에이 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="9db51-128">일반적으로 다른 대화 상자 표시 서비스를 설치 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9db51-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="9db51-129">수 또한 묻는 Windows 2003 Server 설치 CD의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="9db51-130">클릭 ' 다음 &gt;' 완료 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="9db51-131">[마침] 클릭-Windows Server 2003 이제 IIS 6.0 및 ASP.NET 1.1을 지원 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="9db51-132">IIS, ASP.NET 및 IIS를 수동으로 구성 하는 #2-옵션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9db51-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="9db51-133">' 구성 서버 마법사 '를 사용 하 고 싶지 않은 경우 제어판에서 IIS 6.0 및 ASP.NET 1.1 '프로그램 추가 / 제거'를 사용 하 여을 설치할 필요에 따라 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="9db51-134">먼저 제어판을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="9db51-135">그런 다음 ' 추가/제거 Windows 구성 요소에 ' ' Windows 구성 요소 마법사 '를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="9db51-136">강조 표시 하 고 ' 응용 프로그램 서버 '를 확인 하는 'Details'?'를 클릭 한 다음</span><span class="sxs-lookup"><span data-stu-id="9db51-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="9db51-137">단추:</span><span class="sxs-lookup"><span data-stu-id="9db51-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="9db51-138">ASP.NET을 설치 하려면 ' ASP 합니다. NET'.</span><span class="sxs-lookup"><span data-stu-id="9db51-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="9db51-139">Windows 구성 요소 마법사 반환 하려면 ' 확인'을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="9db51-140">클릭 ' 다음 &gt;' 설치를 시작 하려면 Windows 구성 요소 마법사에서:</span><span class="sxs-lookup"><span data-stu-id="9db51-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="9db51-141">일반적으로 다른 대화 상자 표시 서비스를 설치 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9db51-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="9db51-142">수 또한 묻는 Windows 2003 Server 설치 CD의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="9db51-143">설치가 완료 되 면 Windows 구성 요소 마법사의 마지막 화면을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="9db51-144">IIS 6.0 및 ASP.NET 1.1은 이제 구성 및 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="9db51-145">권장된 설정</span><span class="sxs-lookup"><span data-stu-id="9db51-145">Recommended Settings</span></span>

<span data-ttu-id="9db51-146">IIS 6.0과 ASP.NET 1.1을 실행 하는 경우에 ASP.NET에서 최적의 성능을 얻기 위해 권장 되는 여러 구성 설정이:</span><span class="sxs-lookup"><span data-stu-id="9db51-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="9db51-147">작업자 프로세스 메모리 한도 구성</span><span class="sxs-lookup"><span data-stu-id="9db51-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="9db51-148">작업자 프로세스 재활용 구성</span><span class="sxs-lookup"><span data-stu-id="9db51-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="9db51-149">작업자 프로세스 메모리 한도 구성</span><span class="sxs-lookup"><span data-stu-id="9db51-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="9db51-150">기본적으로 IIS 6.0의 IIS에서 사용할 수 있는 메모리 양에 제한을 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="9db51-151">ASP 합니다. NET의 캐시 기능은 캐시 메모리에서 사전에 사용 되지 않는 항목을 제거할 수 있도록 메모리의 제한 사항 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="9db51-152">IIS 6.0의 기능을 재활용 하는 메모리를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="9db51-153">이 오픈 인터넷 정보 서비스 관리자를 구성 하려면 (시작 | 프로그램 | 관리 도구 | 인터넷 정보 서비스)입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="9db51-154">열기 되 면 ' 응용 프로그램 풀 ' 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="9db51-155">각 응용 프로그램 풀:</span><span class="sxs-lookup"><span data-stu-id="9db51-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="9db51-156">예를 들어 응용 프로그램 풀에서 마우스 오른쪽 단추로 'DefaultAppPool' 및 '속성'을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="9db51-157">그런 다음 중 하나를 클릭 하 여 메모리 재활용을 사용 하도록 설정 ' 사용 된 최대 메모리 (메가바이트 단위). '.</span><span class="sxs-lookup"><span data-stu-id="9db51-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="9db51-158">값은 서버의 실제 가상이 아닌 메모리의 양보다 많을 수 없습니다는 유사한 추정치 512MB 이상의 실제 메모리 선택 310 사용 하 여 서버에 대 한 예: 실제 메모리의 60%입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="9db51-159">또한 최대 초과 하지 않는지 800MB 2GB 주소 공간을 사용 하는 경우 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="9db51-160">서버의 메모리 주소 공간 3 GB 인 경우 작업자 프로세스에 대 한 최대 메모리 제한을 1, 800 MB으로 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="9db51-161">'적용' 및 'OK' 속성 대화 상자를 종료 하려면 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="9db51-162">모든 사용 가능한 응용 프로그램 풀에 대해이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="9db51-163">재활용 작업자 구성</span><span class="sxs-lookup"><span data-stu-id="9db51-163">Configuring worker recycling</span></span>

<span data-ttu-id="9db51-164">기본적으로 IIS 6.0은 29 시간 마다 작업자 프로세스를 재활용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="9db51-165">ASP.NET을 실행 중인 응용 프로그램에 대 한 다소 공격적인 이며 자동 작업자 프로세스 재활용은 사용 하지 않도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="9db51-166">자동 작업자 프로세스 재활용을 사용 하지 않으려면 인터넷 정보 서비스 관리자를 열려면 먼저 (시작 | 프로그램 | 관리 도구 | 인터넷 정보 서비스)입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="9db51-167">열기 되 면 ' 응용 프로그램 풀 ' 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="9db51-168">각 응용 프로그램 풀:</span><span class="sxs-lookup"><span data-stu-id="9db51-168">For each application pool:</span></span>

1. <span data-ttu-id="9db51-169">예를 들어 응용 프로그램 풀에서 마우스 오른쪽 단추로 'DefaultAppPool' 및 '속성'을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="9db51-170">선택 취소 ' 분 단위로 작업자 프로세스 재생:':</span><span class="sxs-lookup"><span data-stu-id="9db51-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="9db51-171">'적용' 및 'OK' 속성 대화 상자를 종료 하려면 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="9db51-172">모든 사용 가능한 응용 프로그램 풀에 대해이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="9db51-173">파일 시스템에 대 한 쓰기 액세스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-173">Granting write access to the file system</span></span>

<span data-ttu-id="9db51-174">응용 프로그램에 파일 시스템에 대 한 쓰기 권한이 필요 하 고 NTFS를 사용 하는 경우는 목록 ACL (액세스 제어) 폴더 또는 파일의 ASP.NET 액세스 권한을 부여 하려면 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="9db51-175">예를 들어, ASP.NET을 부여 하 여 c:\inetpub\wwwroot에 대 한 쓰기 액세스 먼저 탐색기를 열고 디렉터리로 이동:</span><span class="sxs-lookup"><span data-stu-id="9db51-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="9db51-176">다음 예를 들어 'wwwroot' 속성과 선택 디렉터리를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="9db51-177">속성 대화 상자를 연 후 '보안' 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="9db51-178">C:\inetpub\wwwroot\ 디렉터리가 특수 디렉터리에는 특별 한 IIS 6.0 그룹 ' IIS\_WPG' 읽기 이미 부여 되어 &amp; 실행, 폴더 내용 보기 및 읽기 권한.</span><span class="sxs-lookup"><span data-stu-id="9db51-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="9db51-179">그러나 쓰기 권한을 부여 하려면 해야 쓰기에 대 한 허용 확인란을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="9db51-180">IIS 6.0은 이제이 폴더에 쓰기 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="9db51-181">이전에 유의 하 다음 단계-다른 폴더에 대 한 쓰기 권한을 부여 하려면, IIS를 추가 해야 할 수도\_WPG 그룹 아직 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="9db51-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="9db51-182">IIS에 쓰기 권한이 부여\_WPG ASP.NET 응용 프로그램을이 디렉터리에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="9db51-183">SQL Server를 사용 하 여 통합된 인증을 지 원하는</span><span class="sxs-lookup"><span data-stu-id="9db51-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="9db51-184">통합된 인증은 Windows NT 인증을 활용 하 여 SQL Server에 대 한 SQL Server 로그온 계정 유효성 검사를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="9db51-185">표준 SQL Server 로그온 프로세스를 사용 하지 않으려면이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="9db51-186">이 방법을 사용 하 여 네트워크 사용자 SQL Server Windows NT 네트워크 보안 프로세스에서 사용자 및 암호 정보를 가져오는 때문에 별도 로그온 id 또는 암호를 제공 하지 않고 SQL Server 데이터베이스를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="9db51-187">자격 증명 없이 응용 프로그램에 대 한 연결 문자열 내의 어느 저장 되기 때문에 좋은 선택 하는 ASP.NET 응용 프로그램에 대 한 통합된 인증 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="9db51-188">대신 SQL에 연결할 때 사용할 연결 문자열은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="9db51-189">이 연결 문자열에는 SQL Server에 액세스 하는 응용 프로그램의 Windows 자격 증명을 사용 하도록 SQL Server 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="9db51-190">ASP.NET/IIS 6의 경우 IIS에서 계정이 것이\_WPG 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="9db51-191">SQL Server와 ASP.NET 간의 통합된 인증을 사용 하려면 먼저 SQL Server 통합된 인증 또는 혼합 모드 인증에 대 한 구성 되어 있는지를 확인 해야이 확인 하기 위해 DBA를 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="9db51-192">이러한 두 가지 모드 중 하나에 SQL Server 인 경우에 통합된 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="9db51-193">SQL Server 엔터프라이즈 관리자를 열고 (시작 | 프로그램 | Microsoft SQL Server | 적절 한 서버를 선택 하 고 보안 폴더를 확장 하는 엔터프라이즈 관리자):</span><span class="sxs-lookup"><span data-stu-id="9db51-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="9db51-194">경우 ' BUILTINT\IIS\_WPG' 그룹 없는 로그인을 마우스 오른쪽 단추로 클릭 하 고 새 로그인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="9db51-195">에 ' 이름:' 텍스트 상자에 입력 하거나 붙여넣습니다 ' [Server/도메인 이름] \IIS\_WPG' Windows NT 사용자/그룹 선택 하 고 줄임표 단추 클릭 또는:</span><span class="sxs-lookup"><span data-stu-id="9db51-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="9db51-196">현재 컴퓨터의 IIS 선택\_WPG 그룹 하 고 'Add' 및 선택기를 닫으려면 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="9db51-197">그런 다음 기본 데이터베이스 및 데이터베이스에 액세스 권한을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="9db51-198">설정 하려면 기본 데이터베이스 예를 들어 아래 Northwind 선택 드롭다운 목록에서에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="9db51-199">다음으로, 데이터베이스 액세스 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="9db51-200">에 대 한 액세스를 허용 하려는 모든 데이터베이스에 대 한 허용 확인란을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="9db51-201">또한 해야 데이터베이스 역할 선택 db 검사\_소유자 로그인에 관리 하 고 선택한 데이터베이스를 사용 하는 데 필요한 모든 권한이 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="9db51-202">속성 대화 상자를 종료 하려면 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="9db51-203">ASP.NET 응용 프로그램은 이제 통합 된 SQL Server 인증을 지원 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="9db51-204">IIS 6.0 기본 모드로 ASP.NET 1.0을 실행 하지 마세요</span><span class="sxs-lookup"><span data-stu-id="9db51-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="9db51-205">IIS 5 호환 모드로 IIS 6.0에서 ASP.NET 1.0만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="9db51-206">IIS 5.0 호환성 모드에서 실행 되도록 ASP.NET 1.0을 구성 하려면 인터넷 서비스 관리자 및 웹 사이트를 마우스 오른쪽 단추로 클릭 열고 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db51-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="9db51-207">서비스 탭으로 전환 하 고 확인? IIS 5.0 격리 모드에서 WWW 서비스 실행 됨:</span><span class="sxs-lookup"><span data-stu-id="9db51-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
