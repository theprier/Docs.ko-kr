---
title: ASP.NET Core 및 Azure를 사용 하 여 DevOps | 모니터링 및 디버그
author: CamSoper
description: Azure에서 호스팅되는 ASP.NET Core 앱에 대한 DevOps 파이프라인을 빌드하는 방법에 대한 종단 간 지침을 제공하는 가이드입니다.
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/monitor
ms.openlocfilehash: c2fc88493aee04d7ea2781d17e808581e89d2082
ms.sourcegitcommit: 29dfe436f54a27fbb4f6494bc639d16c75001fab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2018
ms.locfileid: "42909387"
---
# <a name="monitor-and-debug"></a><span data-ttu-id="9a56d-103">모니터링 및 디버그</span><span class="sxs-lookup"><span data-stu-id="9a56d-103">Monitor and debug</span></span>

<span data-ttu-id="9a56d-104">앱을 배포할 것 이므로 DevOps 파이프라인을 작성, 모니터링 하 고 앱의 문제를 해결 하는 방법을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-104">Having deployed the app and built a DevOps pipeline, it's important to understand how to monitor and troubleshoot the app.</span></span>

<span data-ttu-id="9a56d-105">이 섹션에서는 다음 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-105">In this section, you'll complete the following tasks:</span></span>

* <span data-ttu-id="9a56d-106">기본 모니터링 및 문제 해결 Azure portal에서 데이터 찾기</span><span class="sxs-lookup"><span data-stu-id="9a56d-106">Find basic monitoring and troubleshooting data in the Azure portal</span></span>
* <span data-ttu-id="9a56d-107">Azure Monitor 메트릭을 면밀히 검토 모든 Azure 서비스에서 제공 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-107">Learn how Azure Monitor provides a deeper look at metrics across all Azure services</span></span>
* <span data-ttu-id="9a56d-108">응용 프로그램 프로 파일링에 대 한 Application Insights를 사용 하 여 웹 앱 연결</span><span class="sxs-lookup"><span data-stu-id="9a56d-108">Connect the web app with Application Insights for app profiling</span></span>
* <span data-ttu-id="9a56d-109">로깅을 설정 하 고 로그를 다운로드할 수 있는 위치에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-109">Turn on logging and learn where to download logs</span></span>
* <span data-ttu-id="9a56d-110">Stream 로그를 실시간으로</span><span class="sxs-lookup"><span data-stu-id="9a56d-110">Stream logs in real time</span></span>
* <span data-ttu-id="9a56d-111">경고를 설정 하는 위치에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-111">Learn where to set up alerts</span></span>
* <span data-ttu-id="9a56d-112">원격 디버깅 Azure App Service web apps에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-112">Learn about remote debugging Azure App Service web apps.</span></span>

## <a name="basic-monitoring-and-troubleshooting"></a><span data-ttu-id="9a56d-113">기본 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9a56d-113">Basic monitoring and troubleshooting</span></span>

<span data-ttu-id="9a56d-114">App Service 웹 앱은 쉽게 실시간으로 모니터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-114">App Service web apps are easily monitored in real time.</span></span> <span data-ttu-id="9a56d-115">Azure portal 메트릭 이해 하기 쉬운 차트 및 그래프를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-115">The Azure portal renders metrics in easy-to-understand charts and graphs.</span></span>

1. <span data-ttu-id="9a56d-116">엽니다는 [Azure portal](https://portal.azure.com)로 이동한 다음 합니다 *mywebapp\<unique_number\>*  App Service.</span><span class="sxs-lookup"><span data-stu-id="9a56d-116">Open the [Azure portal](https://portal.azure.com), and then navigate to the *mywebapp\<unique_number\>* App Service.</span></span>

1. <span data-ttu-id="9a56d-117">합니다 **개요** 탭 최근 메트릭을 표시 하는 그래프를 포함 하 여 "a 일목요연" 유용한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-117">The **Overview** tab displays useful "at-a-glance" information, including graphs displaying recent metrics.</span></span>

    ![개요 패널](./media/monitoring/overview.png)

    * <span data-ttu-id="9a56d-119">**Http 5xx**: 서버 쪽 오류 개수, 일반적으로 ASP.NET Core 코드의 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-119">**Http 5xx**: Count of server-side errors, usually exceptions in ASP.NET Core code.</span></span>
    * <span data-ttu-id="9a56d-120">**데이터에서**: 웹 앱으로 들어오는 데이터 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-120">**Data In**: Data ingress coming into your web app.</span></span>
    * <span data-ttu-id="9a56d-121">**데이터 출력**: 클라이언트에 웹 앱에서 데이터를 송신 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-121">**Data Out**: Data egress from your web app to clients.</span></span>
    * <span data-ttu-id="9a56d-122">**요청**: HTTP 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-122">**Requests**: Count of HTTP requests.</span></span>
    * <span data-ttu-id="9a56d-123">**평균 응답 시간**: 평균 HTTP 요청에 응답 하도록 웹 앱에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-123">**Average Response Time**: Average time for the web app to respond to HTTP requests.</span></span>

    <span data-ttu-id="9a56d-124">여러 셀프 서비스 도구 문제 해결 및 최적화를 위한이 페이지에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-124">Several self-service tools for troubleshooting and optimization are also found on this page.</span></span>

    ![셀프 서비스 도구](./media/monitoring/wizards.png)

    * <span data-ttu-id="9a56d-126">**문제 진단 및 해결** 셀프 서비스 문제 해결사에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-126">**Diagnose and solve problems** is a self-service troubleshooter.</span></span>
    * <span data-ttu-id="9a56d-127">**Application Insights** 성능과 앱 동작을 프로 파일링 되며이 섹션의 뒷부분에서 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-127">**Application Insights** is for profiling performance and app behavior, and is discussed later in this section.</span></span>
    * <span data-ttu-id="9a56d-128">**App Service Advisor** 앱 환경을 튜닝 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-128">**App Service Advisor** makes recommendations to tune your app experience.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="9a56d-129">고급 모니터링</span><span class="sxs-lookup"><span data-stu-id="9a56d-129">Advanced monitoring</span></span>

<span data-ttu-id="9a56d-130">[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) 모든 메트릭을 모니터링 하 고 Azure 서비스에서 경고 설정에 대 한 중앙 집중식된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-130">[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) is the centralized service for monitoring all metrics and setting alerts across Azure services.</span></span> <span data-ttu-id="9a56d-131">Azure Monitor에서 관리자 수 세부적으로 성과 추적 하며 추세를 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-131">Within Azure Monitor, administrators can granularly track performance and identify trends.</span></span> <span data-ttu-id="9a56d-132">각 Azure 서비스는 자체 [메트릭 집합이](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics#microsoftwebsites-excluding-functions) Azure Monitor로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-132">Each Azure service offers its own [set of metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics#microsoftwebsites-excluding-functions) to Azure Monitor.</span></span>

## <a name="profile-with-application-insights"></a><span data-ttu-id="9a56d-133">Application Insights 사용 하 여 프로필</span><span class="sxs-lookup"><span data-stu-id="9a56d-133">Profile with Application Insights</span></span>

<span data-ttu-id="9a56d-134">[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) 웹 앱 및 사용자가 사용 하는 방법의 안정성 및 성능 분석에 대 한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-134">[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) is an Azure service for analyzing the performance and stability of web apps and how users use them.</span></span> <span data-ttu-id="9a56d-135">Application Insights의 데이터를 훨씬 광범위 하 고 Azure Monitor의 보다 수준이 깊은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-135">The data from Application Insights is broader and deeper than that of Azure Monitor.</span></span> <span data-ttu-id="9a56d-136">개발자와 관리자가 앱을 개선 하는 것에 대 한 키 정보를 사용 하 여 데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-136">The data can provide developers and administrators with key information for improving apps.</span></span> <span data-ttu-id="9a56d-137">Application Insights는 코드 변경 없이 Azure App Service 리소스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-137">Application Insights can be added to an Azure App Service resource without code changes.</span></span>

1. <span data-ttu-id="9a56d-138">엽니다는 [Azure portal](https://portal.azure.com)로 이동한 다음 합니다 *mywebapp\<unique_number\>*  App Service.</span><span class="sxs-lookup"><span data-stu-id="9a56d-138">Open the [Azure portal](https://portal.azure.com), and then navigate to the *mywebapp\<unique_number\>* App Service.</span></span>
1. <span data-ttu-id="9a56d-139">**개요** 탭을 클릭 합니다 **Application Insights** 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-139">From the **Overview** tab, click the **Application Insights** tile.</span></span>

    ![Application Insights 타일](./media/monitoring/app-insights.png)

1. <span data-ttu-id="9a56d-141">선택 된 **새 리소스 만들기** 라디오 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-141">Select the **Create new resource** radio button.</span></span> <span data-ttu-id="9a56d-142">기본 리소스 이름을 사용 하 고 Application Insights 리소스에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-142">Use the default resource name, and select the location for the Application Insights resource.</span></span> <span data-ttu-id="9a56d-143">위치는 웹 앱에 맞게 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-143">The location doesn't need to match that of your web app.</span></span>

    ![Application Insights 설정](./media/monitoring/new-app-insights.png)

1. <span data-ttu-id="9a56d-145">에 대 한 **런타임/프레임 워크**를 선택 **ASP.NET Core**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-145">For **Runtime/Framework**, select **ASP.NET Core**.</span></span> <span data-ttu-id="9a56d-146">기본 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-146">Accept the default settings.</span></span>
1. <span data-ttu-id="9a56d-147">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-147">Select **OK**.</span></span> <span data-ttu-id="9a56d-148">확인 메시지가 표시 되 면 선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-148">If prompted to confirm, select **Continue**.</span></span>
1. <span data-ttu-id="9a56d-149">리소스를 만든 후에 Application Insights 페이지로 직접 이동 하려면 Application Insights 리소스의 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-149">After the resource has been created, click the name of Application Insights resource to navigate directly to the Application Insights page.</span></span>

    ![새 Application Insights 리소스는 준비](./media/monitoring/new-app-insights-done.png)

<span data-ttu-id="9a56d-151">앱을 사용 하면 데이터를 누적 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-151">As the app is used, data accumulates.</span></span> <span data-ttu-id="9a56d-152">선택 **새로 고침** 새 데이터를 사용 하 여 블레이드를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-152">Select **Refresh** to reload the blade with new data.</span></span>

![Application Insights 개요 탭](./media/monitoring/app-insights-overview.png)

<span data-ttu-id="9a56d-154">Application Insights 추가 구성 없이 유용한 서버 쪽 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-154">Application Insights provides useful server-side information with no additional configuration.</span></span> <span data-ttu-id="9a56d-155">Application Insights에서 가장 많은 가치를 얻을 [Application Insights SDK를 사용 하 여 앱을 계측](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net-core)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-155">To get the most value from Application Insights, [instrument your app with the Application Insights SDK](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net-core).</span></span> <span data-ttu-id="9a56d-156">제대로 구성 되었으면 서비스 웹 서버 및 클라이언트 쪽 성능을 포함 하 여 브라우저에서 종단 간 모니터링을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-156">When properly configured, the service provides end-to-end monitoring across the web server and browser, including client-side performance.</span></span> <span data-ttu-id="9a56d-157">자세한 내용은 참조는 [Application Insights 설명서](https://docs.microsoft.com/azure/application-insights/app-insights-overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-157">For more information, see the [Application Insights documentation](https://docs.microsoft.com/azure/application-insights/app-insights-overview).</span></span>

## <a name="logging"></a><span data-ttu-id="9a56d-158">로깅</span><span class="sxs-lookup"><span data-stu-id="9a56d-158">Logging</span></span>

<span data-ttu-id="9a56d-159">웹 서버 및 응용 프로그램 로그는 Azure App Service에서 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-159">Web server and app logs are disabled by default in Azure App Service.</span></span> <span data-ttu-id="9a56d-160">다음 단계를 사용 하 여 로그를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-160">Enable the logs with the following steps:</span></span>

1. <span data-ttu-id="9a56d-161">열기는 [Azure portal](https://portal.azure.com)로 이동 합니다 *mywebapp\<unique_number\>*  App Service.</span><span class="sxs-lookup"><span data-stu-id="9a56d-161">Open the [Azure portal](https://portal.azure.com), and navigate to the *mywebapp\<unique_number\>* App Service.</span></span>
1. <span data-ttu-id="9a56d-162">왼쪽 메뉴에서 아래로 스크롤하여 합니다 **모니터링** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-162">In the menu to the left, scroll down to the **Monitoring** section.</span></span> <span data-ttu-id="9a56d-163">선택 **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-163">Select **Diagnostics logs**.</span></span>

    ![진단 로그 링크](./media/monitoring/logging.png)

1. <span data-ttu-id="9a56d-165">켜기 **응용 프로그램 로깅 (파일 시스템)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-165">Turn on **Application Logging (Filesystem)**.</span></span> <span data-ttu-id="9a56d-166">메시지가 표시 되 면 웹 앱에 로그인 하는 앱을 사용 하도록 설정 하려면 확장을 설치 하는 상자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-166">If prompted, click the box to install the extensions to enable app logging in the web app.</span></span>
1. <span data-ttu-id="9a56d-167">설정할 **웹 서버 로깅을** 하 **파일 시스템**입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-167">Set **Web server logging** to **File System**.</span></span>
1. <span data-ttu-id="9a56d-168">입력 된 **보존 기간** 일에서입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-168">Enter the **Retention Period** in days.</span></span> <span data-ttu-id="9a56d-169">예를 들어 30입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-169">For example, 30.</span></span>
1. <span data-ttu-id="9a56d-170">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-170">Click **Save**.</span></span>

<span data-ttu-id="9a56d-171">ASP.NET Core 및 웹 서버 (App Service) 로그는 웹 앱에 대 한 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-171">ASP.NET Core and web server (App Service) logs are generated for the web app.</span></span> <span data-ttu-id="9a56d-172">표시 되는 FTP/FTPS 정보를 사용 하 여 서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-172">They can be downloaded using the FTP/FTPS information displayed.</span></span> <span data-ttu-id="9a56d-173">암호는이 가이드의 앞부분에서 만든 배포 자격 증명으로 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-173">The password is the same as the deployment credentials created earlier in this guide.</span></span> <span data-ttu-id="9a56d-174">로그 수 [PowerShell 또는 Azure CLI를 사용 하 여 로컬 컴퓨터에 직접 스트리밍할](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log#download)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-174">The logs can be [streamed directly to your local machine with PowerShell or Azure CLI](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log#download).</span></span> <span data-ttu-id="9a56d-175">로그 수도 있습니다 [Application Insights에서 볼](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log#how-to-view-logs-in-application-insights)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-175">Logs can also be [viewed in Application Insights](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log#how-to-view-logs-in-application-insights).</span></span>

## <a name="log-streaming"></a><span data-ttu-id="9a56d-176">로그 스트리밍</span><span class="sxs-lookup"><span data-stu-id="9a56d-176">Log streaming</span></span>

<span data-ttu-id="9a56d-177">앱 및 웹 서버 로그는 포털을 통해 실시간으로에서 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-177">App and web server logs can be streamed in real time through the portal.</span></span>

1. <span data-ttu-id="9a56d-178">열기는 [Azure portal](https://portal.azure.com)로 이동 합니다 *mywebapp\<unique_number\>*  App Service.</span><span class="sxs-lookup"><span data-stu-id="9a56d-178">Open the [Azure portal](https://portal.azure.com), and navigate to the *mywebapp\<unique_number\>* App Service.</span></span>
1. <span data-ttu-id="9a56d-179">왼쪽 메뉴에서 아래로 스크롤하여 합니다 **모니터링** 선택한 섹션 **로그 스트림**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-179">In the menu to the left, scroll down to the **Monitoring** section and select **Log stream**.</span></span>

    ![로그 스트림 연결](./media/monitoring/log-stream.png)

<span data-ttu-id="9a56d-181">로그 수도 있습니다 [Azure CLI 또는 Azure PowerShell을 통해 스트리밍할](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log#streamlogs)Cloud Shell을 통해 등입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-181">Logs can also be [streamed via Azure CLI or Azure PowerShell](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log#streamlogs), including through the Cloud Shell.</span></span>

## <a name="alerts"></a><span data-ttu-id="9a56d-182">경고</span><span class="sxs-lookup"><span data-stu-id="9a56d-182">Alerts</span></span>

<span data-ttu-id="9a56d-183">Azure Monitor 해줍니다 [실시간으로 경고](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal) 메트릭, 관리 이벤트 및 기타 조건을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-183">Azure Monitor also provides [real time alerts](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal) based on metrics, administrative events, and other criteria.</span></span>

> <span data-ttu-id="9a56d-184">*참고: 경고 (클래식) 서비스에서 사용할 수만 현재 웹 앱 메트릭에 대해 경고 합니다.*</span><span class="sxs-lookup"><span data-stu-id="9a56d-184">*Note: Currently alerting on web app metrics is only available in the Alerts (classic) service.*</span></span>

<span data-ttu-id="9a56d-185">합니다 [경고 (클래식) 서비스](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitor-quick-resource-metric-alert-portal) 또는 Azure Monitor에서 찾을 수 있습니다 합니다 **모니터링** App Service 설정의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-185">The [Alerts (classic) service](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitor-quick-resource-metric-alert-portal) can be found in Azure Monitor or under the **Monitoring** section of the App Service settings.</span></span>

![경고 (클래식) 링크](./media/monitoring/alerts.png)

## <a name="live-debugging"></a><span data-ttu-id="9a56d-187">라이브 디버깅</span><span class="sxs-lookup"><span data-stu-id="9a56d-187">Live debugging</span></span>

<span data-ttu-id="9a56d-188">Azure App Service 일 수 있습니다 [Visual Studio를 사용 하 여 원격으로 디버그할](https://docs.microsoft.com/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug) 경우 로그 충분 한 정보를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-188">Azure App Service can be [debugged remotely with Visual Studio](https://docs.microsoft.com/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug) when logs don't provide enough information.</span></span> <span data-ttu-id="9a56d-189">그러나 원격 디버깅 디버그 기호를 사용 하 여 컴파일해야 하는 앱이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-189">However, remote debugging requires the app to be compiled with debug symbols.</span></span> <span data-ttu-id="9a56d-190">디버깅 하지 않아야 할 프로덕션 환경에서 제외 하 고 최후의 수단으로.</span><span class="sxs-lookup"><span data-stu-id="9a56d-190">Debugging shouldn't be done in production, except as a last resort.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9a56d-191">결론</span><span class="sxs-lookup"><span data-stu-id="9a56d-191">Conclusion</span></span>

<span data-ttu-id="9a56d-192">이 섹션에서는 다음 태스크를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-192">In this section, you completed the following tasks:</span></span>

* <span data-ttu-id="9a56d-193">기본 모니터링 및 문제 해결 Azure portal에서 데이터 찾기</span><span class="sxs-lookup"><span data-stu-id="9a56d-193">Find basic monitoring and troubleshooting data in the Azure portal</span></span>
* <span data-ttu-id="9a56d-194">Azure Monitor 메트릭을 면밀히 검토 모든 Azure 서비스에서 제공 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-194">Learn how Azure Monitor provides a deeper look at metrics across all Azure services</span></span>
* <span data-ttu-id="9a56d-195">응용 프로그램 프로 파일링에 대 한 Application Insights를 사용 하 여 웹 앱 연결</span><span class="sxs-lookup"><span data-stu-id="9a56d-195">Connect the web app with Application Insights for app profiling</span></span>
* <span data-ttu-id="9a56d-196">로깅을 설정 하 고 로그를 다운로드할 수 있는 위치에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-196">Turn on logging and learn where to download logs</span></span>
* <span data-ttu-id="9a56d-197">Stream 로그를 실시간으로</span><span class="sxs-lookup"><span data-stu-id="9a56d-197">Stream logs in real time</span></span>
* <span data-ttu-id="9a56d-198">경고를 설정 하는 위치에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-198">Learn where to set up alerts</span></span>
* <span data-ttu-id="9a56d-199">원격 디버깅 Azure App Service web apps에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a56d-199">Learn about remote debugging Azure App Service web apps.</span></span>

## <a name="additional-reading"></a><span data-ttu-id="9a56d-200">추가 참조 항목</span><span class="sxs-lookup"><span data-stu-id="9a56d-200">Additional reading</span></span>

* [<span data-ttu-id="9a56d-201">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9a56d-201">Troubleshoot ASP.NET Core on Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/host-and-deploy/azure-apps/troubleshoot)
* [<span data-ttu-id="9a56d-202">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="9a56d-202">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](https://docs.microsoft.com/aspnet/core/host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="9a56d-203">Application Insights를 사용 하 여 Azure 웹 앱 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="9a56d-203">Monitor Azure web app performance with Application Insights</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-azure-web-apps)
* [<span data-ttu-id="9a56d-204">Azure App Service에서 웹앱에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="9a56d-204">Enable diagnostics logging for web apps in Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log)
* [<span data-ttu-id="9a56d-205">Visual Studio를 사용하여 Azure App Service의 웹앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9a56d-205">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://docs.microsoft.com/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio)
* [<span data-ttu-id="9a56d-206">Azure 서비스에 대 한 Azure Monitor에서 클래식 메트릭 경고를 만들려면 Azure portal</span><span class="sxs-lookup"><span data-stu-id="9a56d-206">Create classic metric alerts in Azure Monitor for Azure services - Azure portal</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal)