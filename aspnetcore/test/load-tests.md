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
# <a name="load-and-stress-testing-aspnet-core"></a>부하 및 스트레스 테스트 ASP.NET Core

부하 테스트 및 스트레스 테스트 성능이 뛰어난 웹 앱을 확인 해야 하 고 확장 가능한 됩니다. 목표는 서로 다른도 비슷한 테스트 자주 공유 합니다.

**부하 테스트**: 앱 응답 목표를 만족 하면서 특정 시나리오에 대 한 사용자 지정된 부하를 처리할 수 있는지 테스트 합니다. 앱이 정상 조건에서 실행 됩니다.

**스트레스 테스트**: 테스트 앱 안정성 꼭 필요한 경우 종종 긴 기간으로 실행 하는 경우:

* 높은 사용자 부하 – 스파이크 또는 서서히 늘려봅니다.
* 컴퓨팅 리소스를 제한 합니다.  

스트레스 상태에서 응용 프로그램 오류 로부터 복구를 정상적으로 예상 되는 동작을 반환? 앱은 부하가 *되지* 정상 조건에서 실행 합니다.

Visual Studio 2019는 부하 테스트 기능이 있는 Visual Studio의 최종 버전이 됩니다. 부하 테스트 도구가 필요한 고객의 경우 Apache JMeter, Akamai CloudTest, Blazemeter와 같은 대체 부하 테스트 도구를 사용하는 것이 좋습니다. 자세한 내용은 참조는 [Visual Studio 2019 미리 보기 릴리스 정보](/visualstudio/releases/2019/release-notes-preview#test-tools)합니다.

부하 테스트 서비스의 Azure DevOps 2020에 종료 될 예정입니다. 자세한 내용은 참조 [클라우드 기반 부하 테스트 서비스 수명 끝](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)합니다.

## <a name="visual-studio-tools"></a>Visual Studio Tools

Visual Studio를 사용 하면 만들기, 개발 및 웹 성능 및 부하 테스트를 디버그할 수 있습니다. 옵션은 웹 브라우저에서 작업을 기록 하 여 테스트를 만들 수 있습니다.

[빠른 시작: 부하 테스트 프로젝트 만들기](/visualstudio/test/quickstart-create-a-load-test-project?view=vs-2017) 만들기, 구성 및 부하 테스트를 Visual Studio 2017을 사용 하 여 프로젝트를 실행 하는 방법을 보여 줍니다.

자세한 내용은 [추가 리소스](#add)를 참조하세요.

부하 테스트는 온-프레미스에서 실행 하거나 Azure DevOps를 사용 하 여 클라우드에서 실행 하도록 구성할 수 있습니다.

## <a name="azure-devops"></a>Azure DevOps

사용 하 여 부하 테스트 실행을 시작할 수 있습니다 합니다 [Azure DevOps 테스트 계획](/azure/devops/test/load-test/index?view=vsts) 서비스입니다.

![](./load-tests/_static/azure-devops-load-test.png)

서비스는 다음과 같은 유형의 테스트 형식 지원합니다.

- Visual Studio 테스트를 Visual Studio에서 만든 웹 테스트 합니다.
- 보관 파일 내의 캡처된 HTTP 트래픽을 HTTP 보관 기반 테스트를 테스트 하는 동안 재생 됩니다.
- [URL 기반 테스트](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts) -테스트, 요청 형식, 헤더 및 쿼리 문자열을 로드 하는 Url을 지정할 수 있습니다. 실행 지속 시간 같은 매개 변수를 설정, 부하 패턴, 사용자 수 등을 구성할 수 있습니다.
- [Apache JMeter](https://jmeter.apache.org/) 테스트 합니다.

## <a name="azure-portal"></a>Azure 포털

[Azure 포털을 통해 설정 하 고 웹 앱 부하 테스트 실행](/azure/devops/test/load-test/app-service-web-app-performance-test?view=vsts) Azure portal에서 App Service의 성능 탭에서 직접.

![](./load-tests/_static/azure-appservice-perf-test.png)

테스트는 지정 된 URL 또는 Url을 여러 개를 테스트할 수 있는 Visual Studio 웹 테스트 파일을 사용 하 여 수동 테스트를 수 있습니다.

![](./load-tests/_static/azure-appservice-perf-test-config.png)

테스트의 끝이 보고서는 앱의 성능 특성을 표시 하도록 생성 됩니다. 예제에서는 통계 포함 됩니다.

- 평균 응답 시간
- 최대 처리량: 초당 요청 수
- 실패 백분율

## <a name="third-party-tools"></a>타사 도구

다음 목록은 다양 한 기능 집합을 사용 하 여 타사 웹 성능 도구를 보여 줍니다.

- [Apache JMeter](https://jmeter.apache.org/) : 부하 테스트 도구의 전체 기능 갖춘된 도구 모음입니다. 스레드 바인딩된: 사용자 당 하나의 스레드를 해야 합니다.
- [ab-Apache HTTP server 벤치마킹 도구](https://httpd.apache.org/docs/2.4/programs/ab.html)
- [Gatling](https://gatling.io/) : GUI 및 테스트 레코더를 사용 하 여 데스크톱 도구입니다. JMeter 보다 우수 합니다.
- [Locust.io](https://locust.io/) : 스레드에 의해 제한 되지 않습니다.

<a name="add"></a>
## <a name="additional-resources"></a>추가 리소스

[부하 테스트 블로그 시리즈](https://blogs.msdn.microsoft.com/charles_sterling/2015/06/01/load-test-series-part-i-creating-web-performance-tests-for-a-load-test/) 작성자: Charles Sterling 합니다. 날짜가 지정 된 항목 중 대부분은 여전히 관련이 있지만.
