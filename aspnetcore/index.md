---
title: "ASP.NET Core 소개"
author: rick-anderson
description: "ASP.NET Core를 소개합니다."
manager: wpickett
ms.author: riande
ms.date: 02/28/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: index
ms.openlocfilehash: 112e1e4dc4eed2cf0ee94741a52ce6625e1f42a6
ms.sourcegitcommit: 53ee14b9c8200f44705d8997c3619fa874192d45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="aspnet-core"></a>ASP.NET Core

작성자: [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Shaun Luttin](https://twitter.com/dicshaunary)

ASP.NET Core는 클라우드 기반 인터넷에 연결된 최신 응용 프로그램을 빌드하기 위한 플랫폼 간 고성능 [오픈 소스](https://github.com/aspnet/home) 프레임워크입니다. ASP.NET Core를 사용하면 다음과 같은 작업을 수행할 수 있습니다.

* 웹앱 및 서비스, [IoT](https://www.microsoft.com/internet-of-things/) 앱 및 모바일 백 엔드를 빌드합니다.
* Windows, macOS 및 Linux에서 즐겨 찾는 개발 도구를 사용합니다.
* 클라우드 또는 온-프레미스에 배포합니다.
* [.NET Core 또는.NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)를 실행합니다.

## <a name="why-use-aspnet-core"></a>ASP.NET Core를 사용하는 이유는 무엇인가요?

수백만 명의 개발자가 [ASP.NET 4.x](https://docs.microsoft.com/aspnet/overview)를 사용하여 웹앱을 만들었습니다(계속 사용 중). ASP.NET Core는 간결한 모듈식 프레임워크를 만드는 아키텍처 변경 내용을 포함한 ASP.NET 4.x의 새로운 디자인입니다.

ASP.NET Core는 다음과 같은 이점을 제공합니다.

* 웹 UI 및 웹 API를 동일한 과정으로 빌드합니다.
* [최신 클라이언트 쪽 프레임워크](xref:client-side/index) 및 워크플로 개발을 통합합니다.
* 클라우드를 갖춘 환경 기반 [구성 시스템](xref:fundamentals/configuration/index)입니다.
* [종속성 주입](xref:fundamentals/dependency-injection)이 기본 제공됩니다.
* 간단한 [고성능](https://github.com/aspnet/benchmarks) 모듈식 HTTP 요청 파이프라인을 포함합니다.
* [IIS](xref:host-and-deploy/iis/index), [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache), [Docker](xref:host-and-deploy/docker/index)에서 호스트하거나 고유한 프로세스에서 자체 호스트하는 기능이 있습니다.
* [.NET Core](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)를 대상으로 하는 경우 앱 버전을 함께 관리할 수 있습니다.
* 최신 웹 개발을 간소화하는 도구를 포함합니다.
* Windows, macOS 및 Linux에서 빌드하고 실행할 수 있습니다.
* 오픈 소스이며 [커뮤니티에 중점](https://live.asp.net/)을 둡니다.

ASP.NET Core는 완전히 [NuGet](https://www.nuget.org/) 패키지로 제공됩니다. NuGet 패키지를 사용하면 필요한 종속성만 포함하도록 앱을 최적화할 수 있습니다. 실제로 .NET Core를 대상으로 하는 ASP.NET Core 2.x 앱에는 [단일 NuGet 패키지](xref:fundamentals/metapackage)만 필요합니다. 작은 앱 노출 영역의 혜택에는 보안 강화, 서비스 절감, 성능 향상이 포함됩니다.

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a>ASP.NET Core MVC를 사용하여 웹 API 및 웹 UI 빌드

ASP.NET Core MVC에서는 [Web API](xref:tutorials/index#build-web-apis) 및 [웹앱](xref:tutorials/index#build-web-apps)을 빌드하는 기능을 제공합니다.

* [MVC(모델-뷰-컨트롤러) 패턴](xref:mvc/overview)을 통해 웹 API 및 웹앱을 [테스트 가능](testing/index.md)하게 합니다.
* [Razor 페이지](xref:mvc/razor-pages/index)(ASP.NET Core 2.0의 새로운 기능)는 웹 UI를 쉽게 빌드하고 생산성을 높일 수 있는 페이지 기반 프로그래밍 모델입니다.
* [Razor 태그](xref:mvc/views/razor)는 [Razor 페이지](xref:mvc/razor-pages/index) 및 [MVC 뷰](xref:mvc/views/overview)에 생산적인 구문을 제공합니다.
* [태그 도우미](xref:mvc/views/tag-helpers/intro)를 사용하면 서버 쪽 코드를 Razor 파일에서 HTML 요소를 만들고 렌더링하는 데 사용할 수 있습니다.
* [여러 데이터 형식 및 콘텐츠 협상](mvc/models/formatting.md)에 대한 기본 제공 지원을 통해 웹 API를 브라우저 및 모바일 장치를 포함한 다양한 클라이언트에 연결할 수 있습니다.
* [모델 바인딩](xref:mvc/models/model-binding)은 작업 메서드 매개 변수에 HTTP 요청의 데이터를 자동으로 매핑합니다.
* [유효성 검사 모델](xref:mvc/models/validation)은 자동으로 클라이언트와 서버 쪽 유효성 검사를 수행합니다.

## <a name="client-side-development"></a>클라이언트 쪽 개발

ASP.NET Core는 [Angular](xref:spa/angular), [React](xref:spa/react), [부트스트랩](xref:client-side/bootstrap) 등 유명한 클라이언트 쪽 프레임워크 및 라이브러리와 원활하게 통합합니다. 자세한 내용은 [클라이언트 쪽 개발](xref:client-side/index)을 참조하세요.

## <a name="aspnet-core-targeting-net-framework"></a>ASP.NET Core 대상 .NET Framework

ASP.NET Core는 .NET Core 또는 .NET Framework를 대상으로 지정할 수 있습니다. .NET Framework를 대상으로 지정한 ASP.NET Core 앱은 플랫폼 간 교차 사용이 불가능하며 &mdash;Windows에서만 실행됩니다. ASP.NET Core에서 .NET Framework를 대상으로 지정에 대한 지원은 제거되지 않을 예정입니다. 일반적으로 ASP.NET Core는 [.NET Standard](/dotnet/standard/net-standard) 라이브러리로 구성됩니다. .NET Standard 2.0으로 작성된 앱은 .NET Standard 2.0이 지원되는 모든 위치에서 실행됩니다.

.NET Core를 대상으로 지정하면 여러 이점이 있으며 이러한 장점은 릴리스마다 늘어나고 있습니다. .NET Framework에서 .NET Core의 몇 가지 장점은 다음과 같습니다.

* 플랫폼 간 사용 가능. macOS, Linux 및 Windows에서 실행됩니다.
* 향상된 성능
* Side-by-side 버전 관리.
* 새로운 API
* 소스 열기

.NET Framework에서 .NET Core 사이의 API 차이를 줄이기 위해 최선을 다하고 있습니다. [Windows 호환 팩](/dotnet/core/porting/windows-compat-pack)을 통해 수천 개의 Windows 전용 API를 .NET Core에서 사용할 수 있습니다. 이러한 API는 .NET Core 1.x에서 사용할 수 없습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 다음 리소스를 참조하세요.

* [Razor 페이지 시작](xref:tutorials/razor-pages/razor-pages-start)
* [ASP.NET Core 자습서](xref:tutorials/index)
* [ASP.NET Core 기본 사항](xref:fundamentals/index)
* [매주 ASP.NET 커뮤니티 스탠드업](https://live.asp.net/)은 팀의 진행률 및 계획을 다루고 새 블로그 및 타사 소프트웨어를 설명합니다.
