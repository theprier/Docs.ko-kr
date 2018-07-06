---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: 웹 개발 모범 사례 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: 054fcad387608e136e8171f5d511ee7af1082bd0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824431"
---
<a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>웹 개발 모범 사례 (Azure 사용 하 여 빌드 실제 클라우드 앱)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


처음 세 패턴은 민첩 한 개발 프로세스; 설정에 대 한 되었습니다. 아키텍처 및 코드에 대 한 나머지가 됩니다. 이 웹 개발 모범 사례 컬렉션:

- [상태 비저장 웹 서버](#stateless) 스마트 부하 분산 합니다.
- [세션 상태를 방지](#sessionstate) (또는 것을 방지할 수 없습니다, 하는 경우 데이터베이스 보다는 분산된 캐시 사용).
- [CDN을 사용 하 여](#cdn) -에 지 캐시 정적 파일 자산 (이미지, 스크립트).
- [.NET 4.5의 비동기 지원을 사용 하 여](#async) 호출을 차단 하지 않도록 합니다.

이러한 사례는 클라우드 앱에 대 한 뿐 아니라 모든 웹 개발을 위한 유효 하 하지만 클라우드 앱에 대해 특히 중요 합니다. 클라우드 환경에서 제공 하는 매우 유연한 크기 조정의 사용을 최적화 하기 위해 함께 작동 합니다. 이러한 사례를 따르지 않으면 응용 프로그램을 확장 하려고 할 때 한계에 부 딪 실행할 수 있습니다.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>스마트 부하 분산 장치 상태 비저장 웹 계층

*상태 비저장 웹 계층* 웹 서버의 메모리 나 파일 시스템에서 응용 프로그램 데이터를 저장 하지 것을 의미 합니다. 상태 비저장 웹 계층을 유지를 사용 하면 모두 더 나은 고객 경험을 제공 하 고 비용을 절감할 수 있습니다.

- 웹 계층 상태 비저장 이며 부하 분산 장치 뒤에 응답할 수 있습니다 신속 하 게 응용 프로그램 트래픽의 변경 내용에 동적으로 추가 하거나 서버를 제거 하 여. 위치에 대 한 요금만 서버 리소스를 실제로 사용, 클라우드 환경에서 수요 변화에에서 응답 하는 해당 기능이 비용이 크게 절감으로 변환할 수 있습니다.
- 상태 비저장 웹 계층은 아키텍처 측면에서 훨씬 간단 하 게 응용 프로그램을 확장 합니다. 너무 응답 요구를 보다 신속 하 게 확장 하 고 개발 및 테스트에 적은 비용을 투자할 수 있습니다.
- 온-프레미스 서버와 같이 클라우드 서버 패치 되어; 경우에 따라 다시 부팅 필요 및 웹 계층 상태 비저장 인 경우 오류나 예기치 않은 동작이 발생 하지 서버가 일시적으로 중단 하는 경우 트래픽을 다시 라우팅하는 합니다.

대부분의 실제 응용 프로그램을 웹 세션;에 대 한 상태를 저장할 필요가 요점은 여기 웹 서버에 저장 되지 않습니다. 쿠키 또는 프로세스 서버 쪽 ASP.NET 세션 상태 캐시 공급자를 사용 하 여에서 클라이언트와 같은 다른 방법으로 상태를 저장할 수 있습니다. 파일에 저장할 수 있습니다 [Windows Azure Blob storage](unstructured-blob-storage.md) 로컬 파일 시스템 대신 합니다.

웹 계층은 상태 비저장 이어야 하는 경우 응용 프로그램을 Windows Azure 웹 사이트에서 확장을 얼마나 쉬운지의 예를 들어, 참조를 **확장** 관리 포털에서 Windows Azure 웹 사이트에 대 한 탭:

![크기 조정 탭](web-development-best-practices/_static/image1.png)

웹 서버를 추가 하려는 경우에 오른쪽으로 인스턴스 개수 슬라이더를 끌어만 있습니다. 5로 설정 하 고 클릭 **저장할**, 몇 초 이내 5 명의 웹 서버에에서 있으면 Windows Azure 웹 사이트의 트래픽을 처리 합니다.

![5 개의 인스턴스](web-development-best-practices/_static/image2.png)

인스턴스 수 1까지 다시 또는 3으로 간단 하 게 설정할 수 있습니다. 비용을 절약 하기 시작 백을 확장할 때 바로 Windows Azure 시가 아니라 분 단위로 청구 하기 때문에 있습니다.

또한 Windows Azure를 자동으로 늘리거나 CPU 사용량을 기준으로 하는 웹 서버 수를 확인할 수 있습니다. 다음 예제에서는 2 개를 웹 서버 수가 줄어듭니다 CPU 사용률이 60% 아래로 떨어지면에 CPU 사용량이 80%를 초과 되 면 웹 서버 수가 4의 최대 증가 합니다.

![CPU 사용량 기준 크기 조정](web-development-best-practices/_static/image3.png)

또는 사이트만 되도록 사용 중인 작업 시간을 알고 있는 경우? Windows Azure 주간 여러 서버를 실행 하 고 단일 서버 evenings, 일, 시간 및 주말 감소를 확인할 수 있습니다. 다음과 같은 일련의 스크린샷이 오전 8 시에서 오후 5 시 근무 시간 중 시간에 한 서버 및 4 대의 서버를 실행 하는 웹 사이트를 설정 하는 방법을 보여 줍니다.

![일정에 따라 크기 조정](web-development-best-practices/_static/image4.png)

![예약 시간 설정](web-development-best-practices/_static/image5.png)

![주간 일정](web-development-best-practices/_static/image6.png)

![Weeknight 일정](web-development-best-practices/_static/image7.png)

![주말 일정](web-development-best-practices/_static/image8.png)

물론이 모든 작업을 수행 하려면 포털와 같이 스크립트를

동적으로 추가 하거나 상태 비저장 웹 계층을 유지 하 여 server Vm 2 개를 제거 하려면 장애를 방지 된다면 스케일 아웃 응용 프로그램의 기능 Windows azure에서 거의 제한 되지 않습니다.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>세션 상태를 방지 합니다.

사용자 세션에 대 한 일종의 상태를 저장 하지 않으려면 실제 클라우드 앱에서 대개 유용 하지만 몇 가지 접근 방식을 성능 및 확장성을 다른 항목 보다 더 많은 영향을 합니다. 상태를 저장 해야 할 경우는 가장 좋은 방법은 상태의 크기를 작게 유지 하 고 쿠키에 저장 합니다. 다음 최상의 솔루션에 대 한 공급자를 사용 하 여 ASP.NET 세션 상태를 사용 하는 것 경우는 불가능 [메모리 내 분산된 캐시](distributed-caching.md#sessionstate)합니다. 성능 및 확장성 측면에서 최악의 솔루션의 경우 데이터베이스를 사용 하도록 지원 세션 상태 제공자

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>정적 파일 자산을 캐시 하도록 CDN을 사용 합니다.

CDN은 Content Delivery Network에 대 한 머리글자어입니다. CDN 공급자에 이미지 및 스크립트 파일과 같은 정적 파일 자산을 제공 하 고 공급자 사용자 응용 프로그램에 액세스 하는 경우 어디서 나 얻을 수 있도록 비교적 빠른 응답 및 짧은 대기 시간에 캐시 된 전 세계 데이터 센터에서 이러한 파일을 캐시 자산입니다. 이 사이트의 전체 부하 시간 속도 웹 서버의 부하를 줄입니다. Cdn은 광범위 하 게 지리적으로 분산 되는 대상에 도달 하는 경우에 특히 중요 합니다.

Windows Azure에 CDN, 및 Windows Azure 또는 모든 웹 호스팅 환경에서 실행 되는 응용 프로그램에서 다른 Cdn을 사용할 수 있습니다.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>.NET 4.5의 비동기 지원을 사용 하 여 호출 차단 방지

작업을 비동기적으로 처리를 더 간단 하 게 하기 위해 C# 및 VB 프로그래밍 언어를 개선 하는.NET 4.5. 비동기 프로그래밍의 장점은 여러 웹 서비스 호출을 동시에 시작 하려는 경우 같은 병렬 처리 상황에 대 한 아닙니다. 또한 웹 서버를 보다 효율적으로 수행할 수 있습니다 및 부하가 높은 상황에서 신뢰할 수 있는 합니다. 웹 서버를 사용할 수 있는 스레드 수가 제한에 있고 부하가 높은 상황에서 사용 중인 모든 스레드의 경우 들어오는 요청 스레드가 해제 될 때까지 기다려야 합니다. 응용 프로그램 코드에서 쿼리 및 웹 서비스 호출을 비동기적으로 데이터베이스와 같은 태스크를 처리 하지 않는 경우 서버 I/O 응답을 기다리는 동안 많은 스레드 불필요 하 게 연결 됩니다. 이 서버 부하가 높은 상황에서 처리할 수 있습니다 트래픽 양을 제한 합니다. 비동기 프로그래밍을 사용 하 여 웹 서비스 또는 데이터를 반환 하는 데이터베이스에 대 한 대기 중인 스레드는 새 요청을 처리 하는 최대 때까지 해제 데이터를 수신 합니다. 사용량이 많은 웹 서버에서 수백 또는 수천 개의 요청 다음 처리할 수 있습니다 신속 하 게 스레드를 확보할 수이 고, 그렇지 대기입니다.

앞서 살펴본 것 처럼 이러한 증가 하는 것 만큼 웹 사이트를 처리 하는 웹 서버의 수를 줄이려면으로 쉽습니다. 따라서 서버는 더 높은 처리량을 달성할 수 있습니다, 필요가 없으면 그렇지 않은 경우 보다 더 적은 서버는 지정 된 트래픽 볼륨에 대 한 필요 하기 때문에 비용을 줄일 수 있습니다 하 고 많은으로 합니다.

Web Forms, MVC 및 웹 API에 대 한 ASP.NET 4.5에서는.NET 4.5의 비동기 프로그래밍 모델에 대 한 지원이 포함 됩니다. Entity Framework 6에는 [Windows Azure 저장소 API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)합니다.

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5의 비동기 지원

ASP.NET 4.5의 비동기 프로그래밍 언어 뿐만 아니라도 MVC, Web Forms 및 Web API 프레임 워크에 추가 된 지원 되지 않습니다. 예를 들어, ASP.NET MVC 컨트롤러 동작 메서드 웹 요청에서 데이터를 수신 하 고 브라우저에 전송할 수 있도록 HTML을 만드는 다음 뷰로 데이터를 전달 합니다. 자주 작업 메서드는 웹 페이지에 표시 하기 위해 또는 웹 페이지에 입력 된 데이터를 저장 하는 데이터베이스 또는 웹 서비스에서 데이터를 가져올 해야 합니다. 이러한 시나리오에서는 비동기 작업 메서드를 손쉽게: 반환 하는 대신는 *ActionResult* 개체를 반환 하면 *태스크&lt;ActionResult&gt;*  메서드를 표시 사용 하 여 합니다 *비동기* 키워드입니다. 메서드 내부에서 코드 줄을 대기 시간을 포함 하는 작업을 시작 하는 경우 표시할 있습니다 await 키워드를 사용 합니다.

데이터베이스 쿼리에 대 한 리포지토리 메서드를 호출 하는 간단한 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

그리고은 데이터베이스 호출을 비동기적으로 처리 하는 동일한 메서드.

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

내부적으로 컴파일러는 해당 비동기 코드를 생성합니다. 응용 프로그램에 호출을 수행 하는 경우 `FindTaskByIdAsync`, ASP.NET을 사용 하 여 `FindTask` 요청 다음 작업자 스레드를 해제 하 고 다른 요청을 처리 하는 데 사용할 수 있도록 합니다. 경우는 `FindTask` 을 요청을 수행 하는 스레드를 호출 하는 다음에 오는 코드 처리를 계속 하려면 다시 시작 합니다. 될 때 까지는 그 중의 `FindTask` 요청 시작 되 고 있는 대기 하느라 정체 될 응답에 대 한 유용한 작업을 수행 하기 위한 스레드 데이터 반환 되 면 해야 합니다.

비동기 코드에 대 한 오버 헤드가 발생 하지만 낮은 부하 조건에서 오버 헤드는 그렇지 않은 경우 사용 가능한 스레드가 있을 때까지 보유 수는 요청을 처리할 수는 부하가 높은 조건 하는 동안 미미 합니다.

이러한 종류의 ASP.NET 1.1부터 비동기 프로그래밍을 할 수 있었습니다 했지만 작성 하는 것, 오류 발생률 및 디버그 하기가 어렵습니다. ASP.NET 4.5에서에 대 한 코딩을 간소화 했습니다 했으므로 더 이상 그럴 필요가 없는 이유는.

### <a name="async-support-in-entity-framework-6"></a>Entity Framework 6에 대 한 비동기 지원

4.5의 비동기 지원의 일환으로 웹 서비스 호출, 소켓 및 파일 시스템 I/O에 대 한 비동기 지원 출시 하지만 웹 응용 프로그램에 대 한 가장 일반적인 패턴은 데이터베이스에 도달 하 고 데이터 라이브러리 비동기를 지원 하지 않았습니다. 이제 Entity Framework 6에는 데이터베이스 액세스에 대 한 비동기 지원을 추가합니다.

Entity Framework 6 모든 메서드는 쿼리 또는 데이터베이스를 전송할 수 있도록 명령에는 비동기 버전입니다. 예제에서는 비동기 버전을 표시 합니다 *찾을* 메서드.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

삽입, 삭제, 업데이트 및 간단한 발견 한 뿐 아니라이 비동기 지원 작동을 LINQ 쿼리를 사용 하 여 작동 합니다.

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

`Async` 버전의는 `ToList` 메서드 이므로이 코드에서는 데이터베이스를 전송할 수 있도록 쿼리를 발생 시키는 메서드. `Where` 및 `OrderByDescending` 메서드는만 쿼리를 구성 하는 동안는 `ToListAsync` 메서드는 쿼리를 실행 하 고 응답을 저장를 `result` 변수입니다.

## <a name="summary"></a>요약

모든 웹 프로그래밍 프레임 워크 및 모든 클라우드 환경에서에서 여기에 설명 된 웹 개발 모범 사례를 구현할 수 있지만, 쉽게 ASP.NET 및 Windows Azure의 도구를 사용 했습니다. 이러한 패턴을 따르는 경우에 웹 계층을 쉽게 확장할 수 및 각 서버는 더 많은 트래픽을 처리할 수 있기 때문에 프로그램 비용을 최소화 됩니다.

합니다 [다음 장에서](single-sign-on.md) 클라우드 single sign-on 시나리오를 사용 하는 방법을 살펴봅니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조 하세요.

상태 비저장 웹 서버:

- [Microsoft Patterns and Practices-자동 크기 조정 지침](https://msdn.microsoft.com/library/dn589774.aspx)합니다.
- [사용 하지 않도록 설정 ARR 선호도 Windows Azure 웹 사이트에서 인스턴스](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)합니다. Erez benari 블로그 게시물에는 세션 선호도 Windows Azure 웹 사이트에 설명 합니다.

CDN:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 비디오 시리즈를 9 개 부분으로 구성 합니다. 에피소드 3 시작 1시 34분: 00에서 CDN을 참조 합니다.
- [Microsoft 패턴 및 사례 정적 콘텐츠 호스팅 패턴](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 검토](http://www.cdnreviews.com/)합니다. 여러 Cdn의 개요입니다.

비동기 프로그래밍:

- [ASP.NET MVC 4에서에서 비동기 메서드를 사용 하 여](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)입니다. Rick anderson 자습서입니다.
- [비동기 비동기를 사용 하 여 프로그래밍 및 Await (C# 및 Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx)합니다. MSDN 백서는 비동기 프로그래밍에 대 한 근거, ASP.NET 4.5의 작동 방식 및 구현 하는 코드를 작성 하는 방법을 설명 합니다.
- [Entity Framework 비동기 쿼리 및 저장](https://msdn.microsoft.com/data/jj819165)
- [비동기를 사용 하 여 ASP.NET 웹 응용 프로그램을 빌드하는 방법을](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)합니다. Rowan Miller의 비디오 프레젠테이션 합니다. 그래픽 데모를 포함 합니다. 비동기 프로그래밍의 부하가 높은 상황에서 웹 서버 처리량으로 증대할 쉽게 할 수 있습니다.
- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 비디오 시리즈를 9 개 부분으로 구성 합니다. 확장성 비동기 프로그래밍의 영향에 대 한 토론에 대 한 에피소드 4 및 8 에피소드를 참조 하십시오.
- [ASP.NET 4.5와 중요 한 과제는 비동기 메서드를 사용 하 여의 마법](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx)합니다. 비동기를 사용 하 여 ASP.NET Web Forms 응용 프로그램에서에 대 한 주로 Scott hanselman 블로그 게시물입니다.

추가 웹 개발 모범 사례에 대 한 다음 리소스를 참조 합니다.

- [수정이 샘플 응용 프로그램-모범 사례](the-fix-it-sample-application.md#bestpractices)합니다. 이 전자책에 대 한 부록 Fix It 응용 프로그램에서 구현 된 모범 사례의 수를 나열 합니다.
- [웹 개발자 검사 목록](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [이전](continuous-integration-and-continuous-delivery.md)
> [다음](single-sign-on.md)
