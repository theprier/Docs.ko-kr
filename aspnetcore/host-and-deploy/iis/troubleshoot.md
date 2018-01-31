---
title: "IIS에서 ASP.NET Core 문제 해결"
author: guardrex
description: "ASP.NET Core 응용 프로그램의 IIS 배포와 문제를 진단 하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: c68070a9cba5667504d1ad4927b02b73f83e6573
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="troubleshoot-aspnet-core-on-iis"></a>IIS에서 ASP.NET Core 문제 해결

[Luke Latham](https://github.com/guardrex)으로

문제를 진단 하려면 IIS 배포:

* 브라우저 출력을 검토합니다.
* **이벤트 뷰어**를 통해 시스템의 **응용 프로그램** 로그를 검사합니다.
* `stdout` 로깅을 사용하도록 설정합니다. **ASP.NET Core 모듈** 로그는 *web.config*에 있는 `<aspNetCore>` 요소의 *stdoutLogFile* 특성에 제공된 경로에 있습니다. 특성 값에 제공된 경로의 모든 폴더가 배포에 있어야 합니다. 설정 *stdoutLogEnabled* 를 `true`합니다. 사용 하는 앱의는 `Microsoft.NET.Sdk.Web` SDK를 만들려면는 *web.config* 기본 파일는 *stdoutLogEnabled* 설정을 `false`수동으로 제공는 *web.config* 파일 또는 파일을 사용할 수 있도록 수정 `stdout` 로깅.

이러한 세 가지 소스에서 정보를 사용 하 여는 [항목을 참조 하는 일반적인 오류](xref:host-and-deploy/azure-iis-errors-reference) 문제를 확인 하려면. 문제를 해결 하려면 제공 된 문제 해결 지시를 따릅니다.

*startupTimeLimit*(기본값: 120초) 및 *startupRetryCount*(기본값: 2) 모듈이 통과할 때까지 일반적인 몇 가지 오류는 브라우저, 응용 프로그램 로그 및 ASP.NET Core 모듈 로그에 표시되지 않습니다. 따라서 모듈에서 앱의 프로세스를 시작하지 못했다고 추론될 때까지 6분 정도 기다립니다.

앱이 제대로 작동하는지 확인하는 빠른 방법은 Kestrel에서 직접 앱을 실행하는 것입니다. 응용 프로그램으로 게시 된 경우는 [프레임 워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd), 실행 `dotnet <assembly_name>.dll` 배포 폴더에 있는 가장 응용 프로그램에 IIS 실제 경로입니다. 응용 프로그램으로 게시 된 경우는 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd)실행, 응용 프로그램의 명령 프롬프트에서 직접 실행 파일 `<assembly_name>.exe`, 배포 폴더에 있습니다. 응용 프로그램에서 사용할 수 있어야 Kestrel 5000 기본 포트에서 수신 하는 경우 `http://localhost:5000/`합니다. 응용 프로그램 Kestrel 끝점 주소에서 정상적으로 응답을 하는 경우 문제가 관련 역방향 프록시 구성 및 응용 프로그램 내에서 될 가능성이 적기 가능성이 큽니다.

스타일 시트, 스크립트 또는 응용 프로그램의 정적 파일에서 이미지에 대 한 간단한 정적 파일 요청을 수행 하는 역방향 프록시 제대로 작동 하는지 확인 하는 한 가지 방법은 *wwwroot* 를 사용 하 여 [정적 파일 미들웨어](xref:fundamentals/static-files). 를 앱에는 정적 파일 사용 될 수 있습니다 하지만 MVC 뷰 및 기타 끝점에서 실패 하는 경우 역방향 프록시 구성에 관련 될 가능성이 적기 및 더 (예, MVC 라우팅 또는 500 내부 서버 오류)에 앱 내에서 가능성이 가장 높은 문제가입니다.

에 환경 변수를 일시적으로 추가할 수 Kestrel IIS 뒤 정상적으로 시작 하는 경우 응용 프로그램은 성공적으로 로컬로 실행 한 후 시스템에서 실행 되지 않습니다 *web.config* 설정 하는 `ASPNETCORE_ENVIRONMENT` 를 `Development`합니다. 환경 응용 프로그램 시작을 재정의 하지으로 환경 변수 설정 수 있습니다는 [개발자 예외 페이지](xref:fundamentals/error-handling) 표시할 때 앱이 실행 합니다. 에 대 한 환경 변수를 설정 `ASPNETCORE_ENVIRONMENT` 이렇게에서만 권장 됩니다는 노출 되지 않습니다 준비/테스트 서버에 대 한 인터넷에 있습니다. 환경 변수를 제거 해야는 *web.config* 완료 되 면 파일입니다. 통해 환경 변수 설정에 대 한 내용은 *web.config*, 참조 [aspNetCore의 자식 요소 environmentVariables](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)합니다.

응용 프로그램 로깅을 사용하면 대부분의 경우에서 앱 또는 역방향 프록시 문제를 해결하는 데 도움이 됩니다. 자세한 내용은 [로깅](xref:fundamentals/logging/index)을 참조하세요.

마지막 문제 해결 팁 app 내에서 개발 컴퓨터 또는 패키지 버전에서.NET Core SDK 중 하나를 업그레이드 한 후 실행 되지 않은 응용 프로그램에 적용 됩니다. 경우에 따라 중요한 업그레이드를 수행할 때 일관되지 않은 패키지로 인해 응용 프로그램이 중단될 수 있습니다. 이러한 문제를 대부분 해결할 수 있습니다.

* 삭제 된 `bin` 및 `obj` 프로젝트의 폴더입니다.
* 캐시 지우기 패키지 `%UserProfile%\.nuget\packages\` 및 `%LocalAppData%\Nuget\v3-cache`합니다.
* 복원 및 프로젝트를 다시 작성 합니다.
* 서버에서 이전 배포를 다시 앱을 배포 하기 전에 완전히 삭제 되었는지 확인 합니다.

> [!TIP]
> 패키지 캐시의 선택을 취소 하는 편리한 방법을 실행 하는 것 `dotnet nuget locals all --clear` 명령 프롬프트에서 합니다.
> 
> 패키지 캐시를 지우기 수행할 수도 있습니다를 사용 하 여는 [nuget.exe](https://www.nuget.org/downloads) 도구 및 명령 실행 `nuget locals all -clear`합니다. *nuget.exe* NuGet 웹 사이트에서 별도로 구입 해야 하 고 Windows 10과 함께 제공 되는 설치 되지 않습니다.
<!--
> [!TIP]
> A convenient way to clear package caches is to:
>
> * Obtain the *NuGet.exe* tool from [NuGet.org](https://www.nuget.org/).
> * Add the path to *NuGet.exe* to the system PATH.
> * Execute `nuget locals all -clear` from a command prompt.
>
> Alternatively, execute `dotnet nuget locals all --clear` from a command prompt without obtaining *NuGet.exe*. -->

## <a name="additional-resources"></a>추가 리소스

* [ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
