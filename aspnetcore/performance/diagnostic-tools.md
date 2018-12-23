---
title: 성능 진단 도구
author: mjrousos
description: ASP.NET Core 앱에서 성능 문제를 진단 하는 데 유용한 도구입니다.
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.date: 12/07/2018
uid: performance/diagnostic-tools
ms.openlocfilehash: 3093b7d646e4fa943334c7b1e70ddc007ab18780
ms.sourcegitcommit: 1ea1b4fc58055c62728143388562689f1ef96cb2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53329206"
---
# <a name="performance-diagnostic-tools"></a>성능 진단 도구

[Mike Rousos](https://github.com/mjrousos)

이 문서에서는 ASP.NET Core의 성능 문제를 진단 하기 위한 도구를 나열 합니다.

## <a name="visual-studio-diagnostic-tools"></a>Visual Studio 진단 도구

합니다 [프로 파일링 및 진단 도구](/visualstudio/profiling) 성능 문제 조사를 시작 하는 것이 좋습니다는 Visual Studio에 기본 제공 합니다. 이러한 도구는 강력 하 고 Visual Studio 개발 환경에서 사용 하면 편리 합니다. ASP.NET Core 앱에서 CPU 사용량, 메모리 사용량 및 성능 이벤트의 분석을 허용 하는 도구입니다.

자세한 내용은 [Visual Studio 설명서](/visualstudio/profiling/profiling-overview)합니다.

## <a name="application-insights"></a>응용 프로그램 정보

[Application Insights](/azure/application-insights/app-insights-overview) 앱에 대 한 자세한 성능 데이터를 제공 합니다. Application Insights는 자동으로 응답 속도, 실패율, 종속성 응답 시간 등의 데이터를 수집 합니다. Application Insights는 앱에 사용자 지정 이벤트 및 특정 메트릭 로깅을 지원 합니다.

Application Insights는 다양 한 환경에서 사용할 수 있습니다.

* Azure에서 작동 하도록 최적화 되어 있습니다.
* 프로덕션, 개발 및 스테이징에서 작동합니다.
* 로컬로 작동 [Visual Studio](/azure/application-insights/app-insights-visual-studio) 또는 다른 호스팅 환경입니다.

자세한 내용은 [ASP.NET Core용 Application Insights](/azure/application-insights/app-insights-asp-net-core)를 참조하세요.

## <a name="perfview"></a>PerfView

[PerfView](https://github.com/Microsoft/perfview) 은.NET 성능 문제를 진단 하는 데 특별히.NET 팀에서 만든 성능 분석 도구입니다. PerfView는 CPU 사용량, 메모리 GC 동작, 성능 및 이벤트 벽 시계 시간 분석을 허용합니다.

PerfView 및 시작 하는 방법에 대 한 자세히 알아볼 수 있습니다 [PerfView 비디오 자습서](http://channel9.msdn.com/Series/PerfView-Tutorial) 또는 도구에서 사용할 수 있는 사용자 가이드를 참조 하 여 또는 [github](https://github.com/Microsoft/perfview)합니다.

## <a name="perfcollect"></a>PerfCollect

PerfView.NET 시나리오에 대 한 유용한 성능 분석 도구 이지만만 실행 됩니다 Windows 하므로 Linux 환경에서 실행 되는 ASP.NET Core 앱에서 추적을 수집에 사용할 수 없습니다.

[PerfCollect](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md) 네이티브 Linux 프로 파일링 도구를 사용 하는 bash 스크립트는 ([Perf](https://perf.wiki.kernel.org/index.php/Main_Page) 하 고 [LTTng](https://lttng.org/)) PerfView에서 분석할 수 있는 Linux에서 추적을 수집 하려면. PerfCollect은 PerfView를 직접 사용할 수 없는 위치는 Linux 환경에서 성능 문제가 표시 하는 경우에 유용 합니다. 대신 PerfCollect PerfView를 사용 하 여 Windows 컴퓨터에서 다음 분석 되는.NET Core 앱에서 추적을 수집할 수 있습니다.

설치 하 고 PerfCollect 시작 하는 방법에 대 한 자세한 내용은 [GitHub에서](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md)합니다.
