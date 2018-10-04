---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Azure 사용 하 여 실제 클라우드 앱 빌드 | Microsoft Docs
author: MikeWasson
description: 이 전자책에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 설명 합니다. 패턴은 적용에 개발 프로세스에는...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: c496e93d7517bc187514d5fa2dfa90d29c5f47f9
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48576315"
---
<a name="building-real-world-cloud-apps-with-azure"></a>Azure 사용 하 여 실제 클라우드 앱 빌드
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 이 전자책에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 설명 합니다. 패턴은 아키텍처 및 코딩 방식 뿐만 아니라 개발 프로세스에 적용 합니다.
> 
> 콘텐츠는 고 제공한 프레젠테이션을 Scott Guthrie를 개발한 여 문의 사항이 있으면 노르웨이 개발자 회의 NDC ())의 2013 년 6 월을 기반으로 ([1 부](http://vimeo.com/68215538)를 [2 부](http://vimeo.com/68215602)), 및에서 Microsoft Tech Ed 오스트레일리아 2013 년 9 월 ([1 부](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)하십시오 [2 부](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)). [다른 많은](more-patterns-and-guidance.md#acknowledgments) 업데이트 하 고 양식으로 비디오에서 전환 하는 동안 콘텐츠를 쌓아 왔습니다.


## <a name="intended-audience"></a>대상

클라우드로 이동을 고려 중이거나, 클라우드 용 개발에 대해 궁금한 점이 있거나 클라우드 개발 모르는 개발자 여기 가장 중요 한 개념 및 알아야 하는 방법의 간단한 개요를 찾을 수 있습니다. 개념은 구체적인 예제 및 기타 리소스에 대 한 자세한 내용은 각 장의 링크와 함께 설명 합니다. 예제 및 추가 리소스에 대 한 링크는 Microsoft 프레임 워크 및 서비스를 하지만 나와 있는 원칙 다른 웹 개발 프레임 워크에 적용 되며 클라우드 환경도 합니다.

여기에서 아이디어 데 도움이 되는 게 더 성공적인 클라우드를 위해 이미 개발 중인 개발자 경우가 있습니다. 계열의 각 장의 읽을 수 독립적으로 선택 하 고 관심이 있는 항목을 선택할 수 있도록 합니다.

Scott Guthrie의 감시 하는 사람 *실제 세계 클라우드 앱 빌드 Azure* 프레젠테이션 및 추가 및 업데이트 된 정보는 여기에서 찾을 해야 합니다.

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>클라우드 개발 패턴

이 전자책은 클라우드 개발에 대 한 패턴을 권장 13을 설명 합니다. "Pattern" 의미로 사용 됩니다 여기는 넓은 의미에서 작업을 수행 하는 것이 좋습니다: 개발, 설계 및 클라우드 앱을 코딩 하는 방법에 대 한 이동 하는 최선의 방법입니다. 이들은 도움이 되는 "성공 pit에 해당"을 수행 하는 경우 키 패턴입니다.

- [모든 것을 자동화](automate-everything.md)합니다.

    - 스크립트를 사용 하 여 효율성을 최대화 하 고 반복적인 프로세스에서 오류를 최소화 합니다.
    - Azure 관리 스크립트 데모:입니다.
- [소스 제어](source-control.md)입니다. 

    - DevOps 워크플로 용이 하 게 하려면 소스 제어에서 분기 구조를 설정 합니다.
    - 데모: 소스 제어에 스크립트를 추가 합니다.
    - 데모: 소스 제어에서 중요 한 데이터를 유지 합니다.
    - 데모: Visual Studio에서 Git을 사용 합니다.
- [지속적인 통합 및 업데이트](continuous-integration-and-continuous-delivery.md)합니다. 

    - 빌드 및 각 원본 제어 체크 인을 사용 하 여 배포를 자동화 합니다.
- [웹 개발 모범 사례](web-development-best-practices.md)합니다. 

    - 상태 비저장 웹 계층을 유지 합니다.
    - 데모: 크기 조정 및 Azure App Service의 Web Apps에서 자동 크기 조정 합니다.
    - 세션 상태를 방지 합니다.
    - CDN을 사용할 수 없을 때 대체 사용 하 여 CDN을 사용 합니다.
    - 비동기 프로그래밍 모델을 사용 합니다.
    - 데모: 비동기 ASP.NET MVC 및 Entity Framework에 있습니다.
- [Single sign on](single-sign-on.md)합니다. 

    - Azure Active Directory에 소개 합니다.
    - 데모: Azure Active Directory를 사용 하는 ASP.NET 앱을 만듭니다.
- [데이터 저장소 옵션](data-storage-options.md)합니다. 

    - 데이터 저장소의 형식입니다.
    - 적절 한 데이터 저장소를 선택 하는 방법입니다.
    - 데모: Azure SQL 데이터베이스입니다.
- [데이터 분할 전략](data-partitioning-strategies.md)합니다. 

    - 가로, 데이터를 분할 또는 관계형 데이터베이스 크기 조정을 용이 하 게 둘 다.
- [구조화 되지 않은 blob storage](unstructured-blob-storage.md)합니다. 

    - Blob service를 사용 하 여 클라우드에서 파일을 저장 합니다.
    - 데모: Fix It 응용 프로그램에서 blob storage를 사용 합니다.
- [장애를 견딜 수 디자인](design-to-survive-failures.md)합니다. 

    - 형식 오류입니다.
    - 오류 범위입니다.
    - Sla를 이해 합니다.
- [모니터링 및 원격 분석](monitoring-and-telemetry.md)합니다. 

    - 이유 모두 원격 분석 앱 구입 하며 앱 계측 하는 사용자 고유의 코드를 작성 합니다.
    - Azure 용 New Relic 데모:
    - 데모: Fix It 응용 프로그램에서 코드를 로깅.
    - 데모: Fix It 응용 프로그램에서 종속성 주입 합니다.
    - 데모: Azure에서 기본 제공 로깅 지원 합니다.
- [일시적인 오류 처리](transient-fault-handling.md)합니다. 

    - 일시적인 오류의 영향을 완화 하기 위해 스마트 재시도/백오프 논리를 사용 합니다.
    - 데모: 다시 시도/백오프 Entity Framework 6에서 합니다.
- [분산 캐싱](distributed-caching.md)합니다. 

    - 확장성을 개선 하 고 분산 캐싱을 사용 하 여 데이터베이스 트랜잭션 비용을 줄입니다.
- [큐 중심 작업 패턴](queue-centric-work-pattern.md)합니다. 

    - 고가용성을 사용 하도록 설정 하 고 느슨하게 웹 및 작업자 계층을 결합 하 여 확장성을 개선 합니다.
    - 데모: Fix It 응용 프로그램에서 Azure storage 큐.
- [더 많은 클라우드 앱 패턴 및 지침도](more-patterns-and-guidance.md)합니다.
- [부록: Fix It 응용 프로그램 예제](the-fix-it-sample-application.md)

    - 알려진 문제
    - 모범 사례
    - 다운로드, 빌드, 실행 및 배포 하는 방법.

이러한 패턴 모든 클라우드 환경에 적용 되지만 Microsoft 기술 및 Visual Studio, Team Foundation Service, ASP.NET 및 Azure 같은 서비스에 따라 예제를 사용 하 여 설명 하겠습니다 했습니다.

이 장의 나머지 부분이에서는이 Fix It 샘플 응용 프로그램 및 Fix It 응용 프로그램에서 실행 되는 Azure App Service 클라우드 환경에서 웹 앱을 소개 합니다.

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>샘플 응용 프로그램 수정

대부분의 스크린 샷 및이 전자책에 나와 있는 코드 예제에서 처음으로 개발한 Fix It 앱에 기반한 [Scott Guthrie](https://weblogs.asp.net/scottgu/) 권장 되는 클라우드 앱 개발 패턴 및 사례를 보여 줍니다.

![앱 홈 페이지 해결](introduction/_static/image1.png)

샘플 앱은 간단한 작업 항목 발권 시스템입니다. 버그를 발견 해야 하는 경우 티켓을 할당 하 고 다른 사용자를 로그인 하 고 할당 된 티켓을 볼 수를 만들고 티켓을 작업이 완료 되 면 완료 됨으로 표시 합니다.

표준 Visual Studio 웹 프로젝트입니다. ASP.NET MVC를 기반으로 하는 하 고 SQL Server 데이터베이스를 사용 합니다. IIS Express에서 로컬로 실행할 수 있습니다 하 고 클라우드에서 실행 하도록 Azure 웹 사이트에 배포할 수 있습니다. 폼 인증 및 로컬 데이터베이스를 사용 하 여 이나 Google 같은 소셜 공급자를 사용 하 여 기록할 수 있습니다. (나중에 살펴보겠습니다 Active Directory 조직 계정으로 로그인 하는 방법.)

![로그인 페이지](introduction/_static/image2.png)

로그인 되 면에서 티켓을 작성, 사용자에 게, 할당 및 업로드할 수 수정 하려는 항목의 그림입니다.

![Fix It 작업 만들기](introduction/_static/image3.png)

![작업에서 만든 수정](introduction/_static/image4.png)

완료 된 것으로, 티켓 세부 정보 보기 및 표시 항목에 할당 된 티켓을 참조 하십시오 만든 작업 항목의 진행률을 추적할 수 있습니다.

기능 측면에서 매우 간단한 앱 이지만 수백만 명의 사용자로 확장할 수 있습니다 하 고 데이터베이스 오류 및 연결 종료 등을 탄력적으로 대처할 수 있도록 구축 하는 방법을 배웁니다. 간단 하 게 시작 하 고 앱을 더 빠르고 효율적으로 개발 주기를 반복 하 여 하는 자동화 되 고 민첩 한 개발 워크플로를 만드는 방법을 배웁니다.

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>Azure App Service에서 웹 앱

Fix It 응용 프로그램에 사용 되는 클라우드 환경에는 웹 사이트 라고 하는 Azure의 서비스입니다. 이 서비스는 방식으로 Vm을 만들고 업데이트할를 유지 하지 않고도 Azure에서 고유한 웹 앱을 호스트, 설치 구성 하는 IIS, 등. Vm에서 사이트를 호스트 하 고 자동으로 백업 및 복구와 다른 서비스를 제공 합니다. 웹 사이트 서비스는 ASP.NET, Node.js, PHP 및 Python을 사용 하 여 작동합니다. Visual Studio, 웹 배포, FTP, Git 또는 TFS를 사용 하 여 매우 신속 하 게 배포할 수 있습니다. 이 일반적으로 몇 초 안에 배포를 시작 하는 시간 사이 업데이트는 인터넷을 통해 사용할 수 있는 시간. 시작 하려면 모든 무료 이며 트래픽 증가 따라 확장할 수 있습니다.

내부적으로 Azure App Service에서 Web Apps는 많은 아키텍처 구성 요소 및 사용자 고유의 Vm에서 IIS를 사용 하 여 웹 사이트를 호스트 하려는 경우 직접 작성 해야 하는 기능을 제공 합니다. 하나의 구성 요소 배포 끝점을 자동으로 IIS를 구성 하 고 사이트에서 실행 하려는 만큼 Vm에서 응용 프로그램을 설치 하는 경우

![배포 서비스](introduction/_static/image5.png)

IIS Vm에 직접 도달 하지 않게는 사용자 웹 사이트에 도달 하면, 겪는 [응용 프로그램 요청 라우팅 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) 부하 분산 장치. 사용자 고유의 서버를 사용 하 여 사용할 수 있습니다 이지만 장점은 해당 하는 수에 대 한 자동으로 설정 합니다. 세션 선호도, IIS에서 큐 깊이 같은 요인을 고려 하는 스마트 추론을 사용 하 고 CPU 사용량 각 컴퓨터를 Vm에 트래픽을 호스트 하는 웹 사이트.

![ARR 부하 분산 장치](introduction/_static/image6.png)

컴퓨터 다운 되 면 Azure 자동으로 순환에서 가져오는, 새 VM 인스턴스를 스핀업 및 새 인스턴스에-응용 프로그램에 대 한 중단 시간 없이 모든 트래픽을 전달 하기 시작 합니다.

![시스템 오류 로부터 자동 복구](introduction/_static/image7.png)

이 모두 자동으로 수행이 됩니다. 웹 사이트를 만들고 응용 프로그램을 배포 후 Windows PowerShell, Visual Studio 또는 Azure 관리 포털을 사용 하 여 수행 해야 됩니다.

쉽고 빠르게 단계별 자습서는 Visual Studio에서 웹 응용 프로그램을 만들고 Azure 웹 사이트를 배포 하는 방법을 보여주는 참조 하세요 [Azure 및 ASP.NET 시작](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.

<a id="summary"></a>
## <a name="summary"></a>요약

이 소개 항목 책 설명, 샘플 응용 프로그램의 스크린샷 및 Azure App Service 클라우드 환경에서 웹 앱에 간략하게 설명의 목록을 제공 했습니다. 클라우드 용으로 앱을 개발 하는 가장 큰 장점 중 하나는 테스트 환경 만들기 및 코드 배포와 같은 반복적인 개발 작업을 자동화 하기 쉽습니다. 주체는 수행 하는 방법을 합니다 [다음 장에서](automate-everything.md)합니다.

## <a name="resources"></a>자료

이 장에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

설명서:

- [Azure App Service의 웹 앱](https://azure.microsoft.com/services/app-service/web/)합니다. Web Apps에 대 한 Azure 설명서에 대 한 포털 페이지입니다.
- [Web Apps, Cloud Services 및 Vm: 사용 하는 경우?](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) WAWS이 챕터에 표시 된 것 처럼 Azure에서 웹 앱을 실행할 수 있습니다 하는 세 가지 방법 중 하나일 뿐입니다. 이 문서는 세 가지 방법 간의 차이점을 설명 하 고 시나리오에 적합 한 선택 하는 방법에 지침을 제공 합니다. 웹 사이트와 같은 클라우드 서비스는 Azure의 PaaS 기능입니다. Vm은 IaaS 기능을 합니다. IaaS와 PaaS의 설명에 대 한 참조를 [데이터 옵션](data-storage-options.md#paasiaas) 장입니다.

비디오:

- [Scott Guthrie 시작 단계 0-Azure 클라우드 OS 란?](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- [Stefan Schackow를 사용 하 여 웹 사이트 아키텍처-](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)합니다.
- [Nir Mashkowski를 사용 하 여 azure 웹 사이트 내부](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)합니다.

> [!div class="step-by-step"]
> [다음](automate-everything.md)
