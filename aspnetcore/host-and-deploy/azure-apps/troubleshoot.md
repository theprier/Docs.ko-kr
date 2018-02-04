---
title: "Azure 앱 서비스에서 ASP.NET Core 문제 해결"
author: guardrex
description: "ASP.NET Core Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/31/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/troubleshoot
ms.openlocfilehash: 144af8e93bb935d07fd064d5f45b40faea4a2664
ms.sourcegitcommit: 7a87d66cf1d01febe6635c7306f2f679434901d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="troubleshoot-aspnet-core-on-azure-app-service"></a>Azure 앱 서비스에서 ASP.NET Core 문제 해결

[Luke Latham](https://github.com/guardrex)으로

이 문서에서는 설명 ASP.NET Core를 진단 하는 방법에 Azure 앱 서비스의 진단 도구를 사용 하 여 응용 프로그램 시작 문제입니다. 추가 문제 해결 권장 사항을 참조 하세요. [Azure 앱 서비스 진단 개요](/azure/app-service/app-service-diagnostics) 및 [하는 방법: Azure 앱 서비스 앱 모니터링](/azure/app-service/web-sites-monitor) Azure 설명서에서.

## <a name="app-startup-errors"></a>응용 프로그램 시작 오류

**502.5 프로세스 오류**  
작업자 프로세스가 실패합니다. 응용 프로그램을 시작 하지 않습니다.

[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 하지만 작업자 프로세스를 시작 하는 데 시작 되지 않습니다. 응용 프로그램 이벤트 로그를 자주 검사 이러한 유형의 문제를 해결 하는 데 도움이 됩니다. 에 설명 되어 로그에 액세스 하는 [응용 프로그램 이벤트 로그](#application-event-log) 섹션.

*502.5 프로세스 오류* 잘못 구성 된 응용 프로그램 작업자 프로세스가 실패 하면 오류 페이지가 반환 됩니다.

![브라우저 창에 502.5 프로세스 오류 페이지를 표시 합니다.](troubleshoot/_static/process-failure-page.png)

**500 내부 서버 오류**  
응용 프로그램 시작 하지만 오류는 서버에서 요청을 수행할 수행할 수 없습니다.

시작 하는 동안 또는 응답을 만드는 동안 응용 프로그램의 코드 내에서이 오류가 발생 합니다. 응답 없는 콘텐츠를 포함할 수 또는 응답으로 나타날 수 있습니다는 *500 내부 서버 오류* 브라우저에서 합니다. 응용 프로그램 이벤트 로그는 일반적으로 응용 프로그램이 정상적으로 시작 상태입니다. 서버의 관점에서는 사실입니다. 응용 프로그램 시작 않았습니다 하지만 유효한 응답을 생성할 수 없습니다. [Kudu 콘솔의 실행](#run-the-app-in-the-kudu-console) 또는 [ASP.NET Core 모듈 stdout 로그 사용](#aspnet-core-module-stdout-log) 문제를 해결 합니다.

## <a name="troubleshoot-app-startup-errors"></a>응용 프로그램 시작 오류 문제 해결

### <a name="application-event-log"></a>응용 프로그램 이벤트 로그

응용 프로그램 이벤트 로그에 액세스 하려면 사용 된 **진단 및 문제 해결** 블레이드는 Azure 포털에서:

1. Azure 포털에서에서 응용 프로그램의 블레이드를 여세요는 **응용 프로그램 서비스** 블레이드입니다.
1. 선택 된 **진단 및 문제 해결** 블레이드입니다.
1. 아래 **문제 범주를 선택**을 선택는 **웹 응용 프로그램 아래로** 단추입니다.
1. 아래 **제안 솔루션**에 대 한 창을 열고 **응용 프로그램 이벤트 로그 열기**합니다. 선택 된 **응용 프로그램 이벤트 로그 열기** 단추입니다.
1. 오류 검사 하 여 최신에서 제공 되는 *IIS AspNetCoreModule* 에 **소스** 열입니다.

사용 하는 대신은 **진단 및 문제 해결** 직접 사용 하 여 응용 프로그램 이벤트 로그 파일을 검사 하려면 블레이드는 [Kudu](https://github.com/projectkudu/kudu/wiki):

1. 선택 된 **고급 도구** 블레이드는 **개발 도구** 영역입니다. 선택 된 **이동&rarr;**  단추입니다. Kudu 콘솔이 새 브라우저 탭 또는 창으로 열립니다.
1. 페이지의 위쪽 탐색 모음을 사용 하 여 엽니다 **디버그 콘솔** 선택 **CMD**합니다.
1. 열기는 **LogFiles** 폴더입니다.
1. 연필 아이콘을 옆에 선택 된 *eventlog.xml* 파일입니다.
1. 로그를 검토 합니다. 가장 최근의 이벤트를 보려면 로그의 아래쪽으로 스크롤하십시오.

### <a name="run-the-app-in-the-kudu-console"></a>Kudu 콘솔에서 앱 실행

많은 시작 오류 응용 프로그램 이벤트 로그에서 유용한 정보를 생성 하지 않습니다. 앱을 실행할 수는 [Kudu](https://github.com/projectkudu/kudu/wiki) 오류를 검색 하도록 원격 실행 콘솔:

1. 선택 된 **고급 도구** 블레이드는 **개발 도구** 영역입니다. 선택 된 **이동&rarr;**  단추입니다. Kudu 콘솔이 새 브라우저 탭 또는 창으로 열립니다.
1. 페이지의 위쪽 탐색 모음을 사용 하 여 엽니다 **디버그 콘솔** 선택 **CMD**합니다.
1. 폴더 경로를 열어 **사이트** > **wwwroot**합니다.
1. 콘솔에서 사용 하 여 응용 프로그램의 어셈블리를 실행 하 여 앱을 실행 *dotnet.exe*합니다. 다음 명령에서에 대 한 응용 프로그램의 어셈블리의 이름을 바꾸어야 `<assembly_name>`:
   ```console
   dotnet .\<assembly_name>.dll
   ```
1. 오류를 보여 주는 응용 프로그램에서 콘솔 출력 Kudu 콘솔에 파이프 됩니다.

### <a name="aspnet-core-module-stdout-log"></a>ASP.NET Core 모듈 stdout 로그

ASP.NET Core 모듈 stdout 로그는 종종 응용 프로그램 이벤트 로그에서 찾을 수 없음 유용한 오류 메시지를 기록 합니다. 사용 하도록 설정 하 고 stdout 로그를 확인 하십시오.

1. 로 이동는 **진단 및 문제 해결** 블레이드 Azure 포털의.
1. 아래 **문제 범주를 선택**을 선택는 **웹 응용 프로그램 아래로** 단추입니다.
1. 아래 **제안 솔루션** > **Stdout 로그 리디렉션을 사용 하도록 설정**, 단추를 선택 **Web.Config를 편집할 Kudu 콘솔을 열고**합니다.
1. Kudu는에서 **진단 콘솔**, 폴더 경로를 열어 **사이트** > **wwwroot**합니다. 표시 아래로 스크롤하여는 *web.config* 목록 맨 아래에 파일입니다.
1. 옆의 연필 아이콘을 클릭는 *web.config* 파일입니다.
1. 설정 **stdoutLogEnabled** 를 `true` 변경 하 고는 **가 stdoutLogFile** 경로를: `\\?\%home%\LogFiles\stdout`합니다.
1. 선택 **저장** 업데이트 된 저장할 *web.config* 파일입니다.
1. 응용 프로그램에 요청을 수행 합니다.
1. Azure 포털에 반환 합니다. 선택 된 **고급 도구** 블레이드는 **개발 도구** 영역입니다. 선택 된 **이동&rarr;**  단추입니다. Kudu 콘솔이 새 브라우저 탭 또는 창으로 열립니다.
1. 페이지의 위쪽 탐색 모음을 사용 하 여 엽니다 **디버그 콘솔** 선택 **CMD**합니다.
1. 선택 된 **LogFiles** 폴더입니다.
1. 검사는 **Modified** 최신 수정 날짜를 사용 하 여 로그인의 stdout 편집 하려면 연필 아이콘을 선택 합니다.
1. 로그 파일을 열 때 오류가 표시 됩니다.

**기억해 야 합니다.** Stdout 문제 해결이 완료 될 때의 로깅이 사용 안 함

1. Kudu는에서 **진단 콘솔**, 경로에 return **사이트** > **wwwroot** 표시 하기 위해는 *web.config* 파일입니다. 열기는 **web.config** 연필 아이콘을 선택 하 여 다시 파일입니다.
1. 설정 **stdoutLogEnabled** 를 `false`합니다.
1. 선택 **저장** 파일을 저장 합니다.

> [!WARNING]
> Stdout 로그를 사용 하지 않도록 설정 하지 않으면 응용 프로그램 또는 서버 오류가 발생할 수 있습니다. 로그 파일 크기에 제한이 없음을 또는 로그 파일을 만들 수 있습니다.
>
> ASP.NET Core 응용 프로그램의 일상적인 로깅에 대 한 로그 파일 크기를 제한 하 고 로그를 회전 하는 로깅 라이브러리를 사용 합니다. 자세한 내용은 참조 [제 3 자 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)합니다.

## <a name="common-startup-errors"></a>일반적인 시작 오류 

참조는 [ASP.NET Core 오류 통칭](xref:host-and-deploy/azure-iis-errors-reference)합니다. 대부분의 응용 프로그램 시작을 방해 하는 일반적인 문제는 참조 항목에서 다룹니다.

## <a name="process-dump-for-a-slow-or-hanging-app"></a>느린 되거나 응용 프로그램에 대 한 프로세스 덤프

앱 느리게 응답 또는 요청에 응답 하지 때 참조 [Azure 앱 서비스의 느린 웹 앱 성능 문제 해결](/azure/app-service/app-service-web-troubleshoot-performance-degradation) 지침을 디버깅 합니다.

## <a name="remote-debugging"></a>원격 디버깅

참조 [원격 디버깅 문제 해결 Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 앱의 웹 앱 섹션](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug) Azure 설명서에서.

## <a name="application-insights"></a>응용 프로그램 정보

[Application Insights](https://azure.microsoft.com/services/application-insights/) 오류 로깅 및 보고 기능을 포함 하 여 Azure 응용 프로그램 서비스에 호스팅된 앱에서 원격 분석을 제공 합니다. Application Insights에서 응용 프로그램의 로깅 기능을 사용할 수 있게 하는 경우 응용 프로그램에서 시작 된 이후에 발생 하는 오류만 보고할 수 있습니다. 자세한 내용은 참조 [ASP.NET Core 용 Application Insights](/azure/application-insights/app-insights-asp-net-core)합니다.

## <a name="monitoring-blades"></a>블레이드를 모니터링합니다.

모니터링 블레이드 문제 해결 환경을 항목의 앞부분에서 설명 하는 방법에 대 한 대안을 제공 합니다. 500 시리즈 오류를 진단 하 이러한 블레이드를 사용할 수 있습니다.

ASP.NET Core 확장이 설치 되어 있는지 확인 합니다. 확장이 설치 되어 있지 않으면를 수동으로 설치할:

1. 에 **개발 도구** 블레이드 섹션은 **확장** 블레이드입니다.
1. **ASP.NET Core 확장** 는 목록에 표시 되어야 합니다.
1. 확장이 설치 되어 있지 않으면, 선택는 **추가** 단추입니다.
1. 선택 된 **ASP.NET Core 확장** 목록에서 합니다.
1. 선택 **확인** 약관을 수락 하도록 합니다.
1. 선택 **확인** 에 **확장 추가** 블레이드입니다.
1. 정보 팝업 메시지는 확장은 성공적으로 설치를 나타냅니다.

Stdout 로깅을 활성화 하지 않으면 다음이 단계를 따르십시오.

1. Azure 포털에서 선택 된 **고급 도구** 블레이드는 **개발 도구** 영역입니다. 선택 된 **이동&rarr;**  단추입니다. Kudu 콘솔이 새 브라우저 탭 또는 창으로 열립니다.
1. 페이지의 위쪽 탐색 모음을 사용 하 여 엽니다 **디버그 콘솔** 선택 **CMD**합니다.
1. 폴더 경로를 열어 **사이트** > **wwwroot** 고 표시 아래로 스크롤하여는 *web.config* 목록 맨 아래에 파일입니다.
1. 옆의 연필 아이콘을 클릭는 *web.config* 파일입니다.
1. 설정 **stdoutLogEnabled** 를 `true` 변경 하 고는 **가 stdoutLogFile** 경로를: `\\?\%home%\LogFiles\stdout`합니다.
1. 선택 **저장** 업데이트 된 저장할 *web.config* 파일입니다.

진단 로깅을 활성화 하려면 계속 수행 합니다.

1. Azure 포털에서 선택 된 **진단 로그** 블레이드입니다.
1. 선택 된 **에** 에 대 한 전환 **응용 프로그램 로깅 (파일 시스템)** 및 **자세한 오류 메시지**합니다. 선택 된 **저장** 블레이드 맨 위에 있는 단추입니다.
1. 실패 요청 이벤트 버퍼링 (FREB) 로깅 라고도 하는 실패 한 요청 추적을 포함 시키려면 선택 된 **에** 에 대 한 전환 **실패 한 요청 추적**합니다. 
1. 선택 된 **로그 스트림** 블레이드에서 아래에 즉시 표시 됩니다는 **진단 로그** 블레이드는 포털에서 합니다.
1. 응용 프로그램에 요청을 수행 합니다.
1. 로그 스트림 데이터 내에서 오류 원인을 표시 됩니다.

**기억해 야 합니다.** Stdout 문제 해결이 완료 될 때의 로깅이 사용 하지 않도록 설정 해야 합니다. 지침 참조는 [ASP.NET Core 모듈 stdout 로그](#aspnet-core-module-stdout-log) 섹션.

실패 한 요청 추적 로그 (FREB 로그)를 보려면:

1. 로 이동는 **진단 및 문제 해결** 블레이드 Azure 포털의.
1. 선택 **실패 한 요청 추적 로그** 에서 **지원 도구** 세로 막대의 영역입니다.

참조 [실패 한 요청 추적 항목 Azure 앱 서비스에서에서 웹 앱에 대 한 진단 로깅 사용 하도록 설정의 섹션](/azure/app-service/web-sites-enable-diagnostic-log#failed-request-traces) 및 [Azure에서 웹 앱에 대 한 응용 프로그램 성능 Faq: 실패 한 요청 추적을 끄려면 어떻게?](/azure/app-service/app-service-web-availability-performance-application-issues-faq#how-do-i-turn-on-failed-request-tracing) 자세한 내용은 합니다.

자세한 내용은 참조 [Azure 앱 서비스의 웹 앱에 대 한 진단 로깅 사용](/azure/app-service/web-sites-enable-diagnostic-log)합니다.

> [!WARNING]
> Stdout 로그를 사용 하지 않도록 설정 하지 않으면 응용 프로그램 또는 서버 오류가 발생할 수 있습니다. 로그 파일 크기에 제한이 없음을 또는 로그 파일을 만들 수 있습니다.
>
> ASP.NET Core 응용 프로그램의 일상적인 로깅에 대 한 로그 파일 크기를 제한 하 고 로그를 회전 하는 로깅 라이브러리를 사용 합니다. 자세한 내용은 참조 [제 3 자 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)합니다.

## <a name="additional-resources"></a>추가 리소스

* [ASP.NET Core의 오류 처리 소개](xref:fundamentals/error-handling)
* [ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)
* [Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 응용 프로그램 문제 해결](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio)
* ["502 잘못 된 게이트웨이" 및 "503 서비스를 사용할 수 없음" Azure 웹 앱에서 HTTP 오류 문제 해결](/app-service/app-service-web-troubleshoot-http-502-http-503)
* [Azure 앱 서비스의 느린 웹 앱 성능 문제 해결](/azure/app-service/app-service-web-troubleshoot-performance-degradation)
* [Azure에서 웹 앱에 대 한 응용 프로그램 성능 Faq](/azure/app-service/app-service-web-availability-performance-application-issues-faq)
* [Azure 금요일: Azure 앱 서비스의 진단 하 고 문제 해결 경험 (12 분 분량의 비디오)](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
