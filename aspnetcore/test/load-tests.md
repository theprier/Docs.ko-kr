---
title: ASP.NET Core 부하/스트레스 테스트
author: Jeremy-Meng
description: 몇 가지 주요 도구 및 부하 테스트 및 스트레스 테스트 ASP.NET Core 앱에 대 한 접근 방법에 설명 합니다.
ms.author: riande
ms.custom: mvc
ms.date: 01/04/2019
uid: test/loadtests
ms.openlocfilehash: 587df6e216943d3eeec779df4d0554dd0fc2fda0
ms.sourcegitcommit: 036d4b03fd86ca5bb378198e29ecf2704257f7b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57345430"
---
# <a name="load-and-stress-testing-aspnet-core"></a><span data-ttu-id="64b5d-103">부하 및 스트레스 테스트 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="64b5d-103">Load and stress testing ASP.NET Core</span></span>

<span data-ttu-id="64b5d-104">부하 테스트 및 스트레스 테스트 성능이 뛰어난 웹 앱을 확인 해야 하 고 확장 가능한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-104">Load testing and stress testing are important to ensure a web app is performant and scalable.</span></span> <span data-ttu-id="64b5d-105">목표는 서로 다른도 비슷한 테스트 자주 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-105">Their goals are different even they often share similar tests.</span></span>

<span data-ttu-id="64b5d-106">**부하 테스트**: 앱 응답 목표를 만족 하면서 특정 시나리오에 대 한 사용자 지정된 부하를 처리할 수 있는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-106">**Load tests**: Tests whether the app can handle a specified load of users for a certain scenario while still satisfying the response goal.</span></span> <span data-ttu-id="64b5d-107">앱이 정상 조건에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-107">The app is run under normal conditions.</span></span>

<span data-ttu-id="64b5d-108">**스트레스 테스트**: 테스트 앱 안정성 꼭 필요한 경우 종종 긴 기간으로 실행 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="64b5d-108">**Stress tests**: Tests app stability when running under extreme conditions and often a long period of time:</span></span>

* <span data-ttu-id="64b5d-109">높은 사용자 부하 – 스파이크 또는 서서히 늘려봅니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-109">High user load – either spikes or gradually increasing.</span></span>
* <span data-ttu-id="64b5d-110">컴퓨팅 리소스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-110">Limited computing resources.</span></span>  

<span data-ttu-id="64b5d-111">스트레스 상태에서 응용 프로그램 오류 로부터 복구를 정상적으로 예상 되는 동작을 반환?</span><span class="sxs-lookup"><span data-stu-id="64b5d-111">Under stress, can the app recover from failure and gracefully return to expected behavior?</span></span> <span data-ttu-id="64b5d-112">앱은 부하가 *되지* 정상 조건에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-112">Under stress, the app is *not* run under normal conditions.</span></span>

<span data-ttu-id="64b5d-113">Visual Studio 2019는 부하 테스트 기능이 있는 Visual Studio의 최종 버전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-113">Visual Studio 2019 will be the last version of Visual Studio with load test features.</span></span> <span data-ttu-id="64b5d-114">부하 테스트 도구가 필요한 고객의 경우 Apache JMeter, Akamai CloudTest, Blazemeter와 같은 대체 부하 테스트 도구를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-114">For customers requiring load testing tools, we recommend using alternate load testing tools such as Apache JMeter, Akamai CloudTest, Blazemeter.</span></span> <span data-ttu-id="64b5d-115">자세한 내용은 참조는 [Visual Studio 2019 미리 보기 릴리스 정보](/visualstudio/releases/2019/release-notes-preview#test-tools)합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-115">For more information, see the [Visual Studio 2019 Preview Release Notes](/visualstudio/releases/2019/release-notes-preview#test-tools).</span></span>

<span data-ttu-id="64b5d-116">부하 테스트 서비스의 Azure DevOps 2020에 종료 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-116">The load testing service in Azure DevOps is ending in 2020.</span></span> <span data-ttu-id="64b5d-117">자세한 내용은 참조 [클라우드 기반 부하 테스트 서비스 수명 끝](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-117">For more information see [Cloud-based load testing service end of life](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/).</span></span>

## <a name="visual-studio-tools"></a><span data-ttu-id="64b5d-118">Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="64b5d-118">Visual Studio Tools</span></span>

<span data-ttu-id="64b5d-119">Visual Studio를 사용 하면 만들기, 개발 및 웹 성능 및 부하 테스트를 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-119">Visual Studio allows users to create, develop, and debug web performance and load tests.</span></span> <span data-ttu-id="64b5d-120">옵션은 웹 브라우저에서 작업을 기록 하 여 테스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-120">An option is available to create tests by recording actions in web browser.</span></span>

<span data-ttu-id="64b5d-121">[빠른 시작: 부하 테스트 프로젝트 만들기](/visualstudio/test/quickstart-create-a-load-test-project?view=vs-2017) 만들기, 구성 및 부하 테스트를 Visual Studio 2017을 사용 하 여 프로젝트를 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-121">[Quickstart: Create a load test project](/visualstudio/test/quickstart-create-a-load-test-project?view=vs-2017) shows how to create, configure, and run a load test projects using Visual Studio 2017.</span></span>

<span data-ttu-id="64b5d-122">자세한 내용은 [추가 리소스](#add)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64b5d-122">See [Additional Resources](#add) for more information.</span></span>

<span data-ttu-id="64b5d-123">부하 테스트는 온-프레미스에서 실행 하거나 Azure DevOps를 사용 하 여 클라우드에서 실행 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-123">Load tests can be configured to run in on-premise or run in the cloud using Azure DevOps.</span></span>

## <a name="azure-devops"></a><span data-ttu-id="64b5d-124">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="64b5d-124">Azure DevOps</span></span>

<span data-ttu-id="64b5d-125">사용 하 여 부하 테스트 실행을 시작할 수 있습니다 합니다 [Azure DevOps 테스트 계획](/azure/devops/test/load-test/index?view=vsts) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-125">Load test runs can be started using the [Azure DevOps Test Plans](/azure/devops/test/load-test/index?view=vsts) service.</span></span>

![](./load-tests/_static/azure-devops-load-test.png)

<span data-ttu-id="64b5d-126">서비스는 다음과 같은 유형의 테스트 형식 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-126">The service supports the following types of test format:</span></span>

- <span data-ttu-id="64b5d-127">Visual Studio 테스트를 Visual Studio에서 만든 웹 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-127">Visual Studio test – web test created in Visual Studio.</span></span>
- <span data-ttu-id="64b5d-128">보관 파일 내의 캡처된 HTTP 트래픽을 HTTP 보관 기반 테스트를 테스트 하는 동안 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-128">HTTP Archive-based test – captured HTTP traffic inside archive is replayed during testing.</span></span>
- <span data-ttu-id="64b5d-129">[URL 기반 테스트](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts) -테스트, 요청 형식, 헤더 및 쿼리 문자열을 로드 하는 Url을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-129">[URL-based test](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts) – allows specifying URLs to load test, request types, headers, and query strings.</span></span> <span data-ttu-id="64b5d-130">실행 지속 시간 같은 매개 변수를 설정, 부하 패턴, 사용자 수 등을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-130">Run setting parameters such as duration, load pattern, number of users, etc., can be configured.</span></span>
- <span data-ttu-id="64b5d-131">[Apache JMeter](https://jmeter.apache.org/) 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-131">[Apache JMeter](https://jmeter.apache.org/) test.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="64b5d-132">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="64b5d-132">Azure portal</span></span>

<span data-ttu-id="64b5d-133">[Azure 포털을 통해 설정 하 고 웹 앱 부하 테스트 실행](/azure/devops/test/load-test/app-service-web-app-performance-test?view=vsts) Azure portal에서 App Service의 성능 탭에서 직접.</span><span class="sxs-lookup"><span data-stu-id="64b5d-133">[Azure portal allows setting up and running load testing of Web Apps,](/azure/devops/test/load-test/app-service-web-app-performance-test?view=vsts) directly from the Performance tab of the App Service in Azure portal.</span></span>

![](./load-tests/_static/azure-appservice-perf-test.png)

<span data-ttu-id="64b5d-134">테스트는 지정 된 URL 또는 Url을 여러 개를 테스트할 수 있는 Visual Studio 웹 테스트 파일을 사용 하 여 수동 테스트를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-134">The test can be a manual test with a specified URL, or a Visual Studio Web Test file, which can test multiple URLs.</span></span>

![](./load-tests/_static/azure-appservice-perf-test-config.png)

<span data-ttu-id="64b5d-135">테스트의 끝이 보고서는 앱의 성능 특성을 표시 하도록 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-135">At end of the test, reports are generated to show the performance characteristics of the app.</span></span> <span data-ttu-id="64b5d-136">예제에서는 통계 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-136">Example statistics include:</span></span>

- <span data-ttu-id="64b5d-137">평균 응답 시간</span><span class="sxs-lookup"><span data-stu-id="64b5d-137">Average response time</span></span>
- <span data-ttu-id="64b5d-138">최대 처리량: 초당 요청 수</span><span class="sxs-lookup"><span data-stu-id="64b5d-138">Max throughput: requests per second</span></span>
- <span data-ttu-id="64b5d-139">실패 백분율</span><span class="sxs-lookup"><span data-stu-id="64b5d-139">Failure percentage</span></span>

## <a name="third-party-tools"></a><span data-ttu-id="64b5d-140">타사 도구</span><span class="sxs-lookup"><span data-stu-id="64b5d-140">Third-party Tools</span></span>

<span data-ttu-id="64b5d-141">다음 목록은 다양 한 기능 집합을 사용 하 여 타사 웹 성능 도구를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-141">The following list contains third-party web performance tools with various feature sets:</span></span>

- <span data-ttu-id="64b5d-142">[Apache JMeter](https://jmeter.apache.org/) : 부하 테스트 도구의 전체 기능 갖춘된 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-142">[Apache JMeter](https://jmeter.apache.org/) : Full featured suite of load testing tools.</span></span> <span data-ttu-id="64b5d-143">스레드 바인딩된: 사용자 당 하나의 스레드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-143">Thread-bound: need one thread per user.</span></span>
- [<span data-ttu-id="64b5d-144">ab-Apache HTTP server 벤치마킹 도구</span><span class="sxs-lookup"><span data-stu-id="64b5d-144">ab - Apache HTTP server benchmarking tool</span></span>](https://httpd.apache.org/docs/2.4/programs/ab.html)
- <span data-ttu-id="64b5d-145">[Gatling](https://gatling.io/) : GUI 및 테스트 레코더를 사용 하 여 데스크톱 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-145">[Gatling](https://gatling.io/) : Desktop tool with a GUI and test recorders.</span></span> <span data-ttu-id="64b5d-146">JMeter 보다 우수 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-146">More performant than JMeter.</span></span>
- <span data-ttu-id="64b5d-147">[Locust.io](https://locust.io/) : 스레드에 의해 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-147">[Locust.io](https://locust.io/) : Not bounded by threads.</span></span>

<a name="add"></a>
## <a name="additional-resources"></a><span data-ttu-id="64b5d-148">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="64b5d-148">Additional Resources</span></span>

<span data-ttu-id="64b5d-149">[부하 테스트 블로그 시리즈](https://blogs.msdn.microsoft.com/charles_sterling/2015/06/01/load-test-series-part-i-creating-web-performance-tests-for-a-load-test/) 작성자: Charles Sterling 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b5d-149">[Load Test blog series](https://blogs.msdn.microsoft.com/charles_sterling/2015/06/01/load-test-series-part-i-creating-web-performance-tests-for-a-load-test/) by Charles Sterling.</span></span> <span data-ttu-id="64b5d-150">날짜가 지정 된 항목 중 대부분은 여전히 관련이 있지만.</span><span class="sxs-lookup"><span data-stu-id="64b5d-150">Dated but most of the topics are still relevant.</span></span>
