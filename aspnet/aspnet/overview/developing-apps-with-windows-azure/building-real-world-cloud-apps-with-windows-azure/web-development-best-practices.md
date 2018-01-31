---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: "웹 개발 모범 사례 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs"
author: MikeWasson
description: "실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: de536a0ca39cb752c0962f0c4ae36eb00b586bff
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>웹 개발 모범 사례 (Azure로 응용 프로그램 빌딩 실제 클라우드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


처음 세 가지 패턴 민첩 한 개발 프로세스; 설정에 대 한 되었습니다. 아키텍처 및 코드에 대 한 나머지는 합니다. 이 컬렉션 웹 개발에 대 한 유용한 정보입니다.

- [상태 비저장 웹 서버의](#stateless) 스마트 부하 분산 장치 뒤 합니다.
- [세션 상태를 방지](#sessionstate) (또는 것을 피할 수 없는 경우 데이터베이스 대신 분산된 캐시 사용).
- [CDN을 사용 하 여](#cdn) 지 캐시 정적 파일 자산 (이미지, 스크립트)에 있습니다.
- [.NET 4.5의 비동기 지원을 사용 하 여](#async) 호출을 차단 하지 않기 위해 합니다.

이러한 사례 뿐 아니라 클라우드 앱에 대 한 모든 웹 개발에 사용할 수 있지만 클라우드 응용 프로그램에 특히 중요 합니다. 클라우드 환경에서 제공 되는 매우 유연한 확장 사용을 최적화 하기 위해 함께 작동 합니다. 이러한 사례를 따르지 않으면 응용 프로그램을 확장 하려고 할 때 제한이 발생 합니다.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>스마트 부하 분산 장치 뒤에 있는 상태 비저장 웹 계층

*상태 비저장 웹 계층* 웹 서버에 메모리 또는 파일 시스템에서 모든 응용 프로그램 데이터를 저장 하지 않는 것을 의미 합니다. 상태 비저장 웹 계층을 유지를 사용 하면 더 나은 사용자 환경을 제공 하 고 비용을 절약할 수 있습니다.

- 상태 비저장 웹 계층 부하 분산 장치 뒤에 배치 하는 경우 응답할 수 있습니다 신속 하 게 응용 프로그램 트래픽이의 변화에 따라 동적으로 추가 하거나 서버를 제거 하 여. 여기서의 요금만 지불 하기 위한 서버 리소스에 대 한 실제로 사용으로 클라우드 환경에서 변경 요청에 응답 하는 해당 기능이 크게 절감 효과를 변환할 수 있습니다.
- 상태 비저장 웹 계층은 구조적 측면에서 훨씬 간단 하 게 응용 프로그램을 확장 합니다. 너무 수 있도록 응답 요구를 보다 신속 하 게 확장 하 고 개발 및 테스트 하는 프로세스에 대 한 적은 비용을 지출할 수 있습니다.
- 온-프레미스 서버와 마찬가지로 클라우드 서버 패치를 적용 하 고 때때로; 다시 부팅 해야 및 상태 비저장 웹 계층의 경우 오류나 예기치 않은 동작이 발생 하지 않습니다 서버가 일시적으로 중단 하는 경우 트래픽을 다시 라우팅하는 기능입니다.

대부분의 실제 응용 프로그램 웹 세션;에 대 한 상태를 저장할 필요가 요점 웹 서버에 저장 되지 않습니다. 클라이언트 쿠키 또는 프로세스 서버 쪽 캐시 공급자를 사용 하 여 ASP.NET 세션 상태에 축소와 같은 다른 방법으로 상태를 저장할 수 있습니다. 파일에 저장할 수 있습니다 [Windows Azure Blob 저장소](unstructured-blob-storage.md) 로컬 파일 시스템 대신 합니다.

크기를 조정 하는 응용 프로그램 Windows Azure 웹 사이트에서 상태 비저장 웹 계층이 얼마나 쉬운지의 예를 들어 참조는 **배율** 관리 포털에서 Windows Azure 웹 사이트에 대 한 탭:

![크기 조정 탭](web-development-best-practices/_static/image1.png)

웹 서버를 추가 하려는 경우에 오른쪽에 인스턴스 수가 슬라이더를 끌 수 있습니다. 5로 설정 하 고 클릭 **저장**, 몇 초 이내 5 웹 서버에에서 있으면 Windows Azure 웹 사이트의 트래픽을 처리 합니다.

![5 개의 인스턴스](web-development-best-practices/_static/image2.png)

3 다운 또는 다시 1 아래로 인스턴스 수를 손쉽게 설정할 수 있습니다. 관련 비용을 시작 하면 뒤로 크기를 조정할 때 Windows Azure 따라 요금을 부과 분, 시가 아니라 때문에 즉시 합니다.

Windows Azure를 자동으로 늘리거나 CPU 사용량에 따라 웹 서버의 수를 알 수 있습니다. 다음 예제에서는 CPU 사용량 60% 미만이 되 면 웹 서버의 수는 2, 최소 줄어들고 CPU 사용률이 80% 이상이 되 면 웹 서버의 수를 최대 4까지 증가 합니다.

![CPU 사용량 기준의 크기를 조정합니다](web-development-best-practices/_static/image3.png)

또는 경우에 어떻게 생각 있는지 사이트만 사용 중 근무 시간 중? Windows Azure를 주간에 여러 서버를 실행 하 고 감소 evenings, nights, 단일 서버 및 주말에 알 수 있습니다. 다음 일련의 스크린 샷 오전 8 시에서 오후 5 시의 작업 시간 동안 4 대의 서버 및 서버 하나를 업무 외 시간에 실행 되도록 웹 사이트를 설정 하는 방법을 보여 줍니다.

![일정에 따라 크기를 조정합니다](web-development-best-practices/_static/image4.png)

![예약 시간 설정](web-development-best-practices/_static/image5.png)

![주간 일정](web-development-best-practices/_static/image6.png)

![Weeknight 일정](web-development-best-practices/_static/image7.png)

![주말 일정](web-development-best-practices/_static/image8.png)

및 물론이 모든 작업을 수행 하려면 포털에서와 같이 스크립트입니다.

으로 제한 요소를 동적으로 추가 또는 상태 비저장 웹 계층을 유지 하 여 서버 Vm을 제거 하지 않도록 쉽게 확장할 수 있는 응용 프로그램의 기능을 Windows Azure에서 거의 제한 되지 않습니다.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>세션 상태를 방지 합니다.

사용자 세션에 대 한 특정 형식의 상태를 저장 하지 않도록 하는 실제 클라우드 앱에 실용적이 지 종종 하지만 몇 가지 접근 방식을 성능 및 확장성을 다른 항목 보다 더 많은 영향을 줄 합니다. 상태를 저장 해야 하는 경우 가장 좋은 방법은 상태의 크기는 작게 유지 하 고 쿠키에 저장할 것입니다. 다음 가장 적합 한 솔루션에 대 한 공급자와 함께 ASP.NET 세션 상태를 사용 하는 것는 불가능 한 경우 [분산, 메모리 내 캐시](distributed-caching.md#sessionstate)합니다. 성능 및 확장성 측면에서 가장 좋지는 데이터베이스를 사용 하도록 세션 상태 공급자를 지원 합니다.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>CDN을 사용 하 여 정적 파일 자산을 캐시 하려면

CDN은 콘텐츠 배달 네트워크에 대 한 약어입니다. CDN 공급자에 이미지 및 스크립트 파일 등의 정적 파일 자산을 제공 하 고 상대적으로 빠른 응답 및 짧은 대기 시간에 대 한 캐시 된 얻을 때마다 응용 프로그램에 액세스 하는 사용자 수 있도록 공급자 전 세계 데이터 센터에서 이러한 파일을 캐시 자산에 합니다. 이 사이트의 전반적인 로드 시간이 더 적게 하 고 웹 서버의 로드 감소 합니다. Cdn이 지리적으로 분산 광범위 하 게 되는 대상 그룹을 연결 하려는 경우에 특히 중요 합니다.

Windows Azure에 CDN, 및 Windows Azure 또는 모든 웹 호스팅 환경에서 실행 하는 응용 프로그램에서 다른 Cdn을 사용할 수 있습니다.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>.NET 4.5의 비동기 지원을 사용 하 여 호출을 차단 하지 않기

작업을 비동기적으로 처리 하는 것 보다 훨씬 간단 하 게 하기 위해 C# 및 VB 프로그래밍 언어를 개선 하는.NET 4.5. 비동기 프로그래밍의 장점은 병렬 처리의 경우 동시에 여러 웹 서비스 호출을 시작할 경우와 같이 데 사용 되지 않습니다. 또한 웹 서버를 보다 효율적으로 수행할 수 있습니다 상태에서 신뢰할 수 있는 합니다. 웹 서버를 사용할 수 있는 스레드 수가 제한에 있고 부하가 높은 상황에서의 모든 스레드가 사용 중인 경우 들어오는 요청 스레드를 해제 될 때까지 기다려야 합니다. 응용 프로그램 코드는 비동기적으로 쿼리 및 웹 서비스 호출을 데이터베이스와 같은 태스크를 처리 하지 않는 경우 서버 I/O 응답에 대 한 대기 하는 동안 많은 스레드가 하느라 정체 불필요 하 게 됩니다. 부하가 높은 상황에서 서버가 처리할 수는 트래픽의 양을 제한 합니다. 비동기 프로그래밍을 사용 하면서 웹 서비스 또는 데이터를 반환 하는 데이터베이스에 대 한 대기 중인 스레드의 새 요청을 처리 하는 최대 때까지 해제 데이터에서 수신 합니다. 사용량이 많은 웹 서버에 수많은 요청 처리할 수 있습니다 신속 하 게 스레드를 확보할 수에 대 한 대기 그렇지 않은 것입니다.

앞에서 살펴본 것 처럼 늘리기 하는 것 만큼 웹 사이트를 처리 하는 웹 서버의 수를 줄이려면 같이 쉽습니다. 따라서 서버 처리량 우위를 얻을 수, 필요가 없으면 서버 수도 더 적은 주어진된 트래픽 볼륨에 대 한 그렇지 않은 경우 보다 필요 하기 때문에 비용이 감소 될 수도 있습니다 다양 하 고 있습니다.

.NET 4.5 비동기 프로그래밍 모델에 대 한 지원에에서 포함 된 ASP.NET 4.5 Web Forms, MVC 및 Web API; Entity Framework 6에 [Windows Azure 저장소 API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)합니다.

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5에서 비동기 지원

ASP.NET 4.5, 비동기 프로그래밍 언어 뿐만 아니라도 MVC, Web Forms 및 Web API 프레임 워크에 추가 된 지원 되지 않습니다. 예를 들어, ASP.NET MVC 컨트롤러 동작 메서드는 웹 요청에서 데이터를 수신 하 고 그러면이 브라우저에 보내야 하는 HTML 보기를 데이터를 전달 합니다. 자주 작업 메서드는 웹 페이지에 표시 하기 위해 또는 웹 페이지에 입력 된 데이터를 저장 하는 데이터베이스 또는 웹 서비스에서 데이터를 가져올 해야 합니다. 사용자 인터페이스에서 작업 메서드를 비동기로 만들려면 쉽게 있기: 반환 하는 대신는 *ActionResult* 개체를 반환 하면 *작업&lt;ActionResult&gt;*  메서드를 표시 하 고 와 *비동기* 키워드입니다. 메서드 내부를 코드의 줄 시작 대기 시간을 포함 하는 작업 하는 경우 표시할 있습니다 await 키워드로.

데이터베이스 쿼리에 대 한 저장소 메서드를 호출 하는 간단한 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

그리고 데이터베이스 호출을 비동기적으로 처리 하는 동일한 메서드 여기:

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

내부적 컴파일러는 해당 비동기 코드를 생성합니다. 응용 프로그램에 대 한 호출을 수행 하는 경우 `FindTaskByIdAsync`, ASP.NET을 사용 하면는 `FindTask` 요청 다음 작업자 스레드를 해제 하 고 다른 요청을 처리할 수 있게 합니다. 경우는 `FindTask` 요청이 수행 됩니다, 해당 호출 다음에 오는 코드 처리를 계속 하려면는 스레드를 다시 시작 합니다. 될 때 까지는 중간 동안는 `FindTask` 요청이 시작 되 고 있는 응답을 대기 하느라 정체 될 것 유용한 작업을 수행 하기 위한 스레드가 있는 때에 데이터가 반환 됩니다.

비동기 코드에 대 한 약간의 오버 헤드가 있지만 낮은 부하 조건에서 오버 헤드는 그렇지 않은 경우 사용 가능한 스레드를 기다리는를 보유할 수는 요청을 처리할 수 있는지 로드가 많은 상황에서 하는 동안 미미 합니다.

경과 했는데도 문제가 있다면 이러한 종류의 ASP.NET 1.1부터 비동기 프로그래밍을 수행할 수 있습니다 하지만 작성을 어렵게, 오류 발생률 및 디버그 하기 어렵습니다. ASP.NET 4.5에서에 대 한 코딩을 간소화 했습니다 했으므로는 다음과 같은 이유가 더 이상 작업을 수행할 필요가 없습니다.

### <a name="async-support-in-entity-framework-6"></a>Entity Framework 6의 비동기 지원

웹 서비스 호출, 소켓, 및 파일 시스템 I/O에 대 한 비동기 지원을 처음 출시 4.5에서 비동기 지원의 일환으로 하지만 웹 응용 프로그램에 대 한 가장 일반적인 패턴은 데이터베이스를 적중 하 및 우리의 데이터 라이브러리 비동기를 지원 하지 않았습니다. 이제 Entity Framework 6 데이터베이스 액세스에 대 한 비동기 지원을 추가합니다.

Entity Framework 6 쿼리 또는 데이터베이스에 보낼 명령의 발생 하는 모든 메서드는 비동기 버전을 갖고 있습니다. 비동기 버전을 표시 하는 예는 *찾을* 메서드.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

및 뿐 아니라에 대 한 삽입, 삭제, 업데이트 및 단순 검색 작업을이 비동기 지원, LINQ 쿼리와도 작동 합니다.

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

한 `Async` 버전의는 `ToList` 메서드 하면 쿼리를 데이터베이스에 전송 하는 메서드는이 코드입니다. `Where` 및 `OrderByDescending` 메서드는만 쿼리를 구성 하는 동안는 `ToListAsync` 쿼리를 실행 하 고에서 응답을 저장 하는 메서드는 `result` 변수 합니다.

## <a name="summary"></a>요약

모든 웹 프로그래밍 프레임 워크와 모든 클라우드 환경에서에서 여기에 설명 된 웹 개발 모범 사례를 구현할 수 있지만 도구를 쉽게 ASP.NET 및 Windows Azure에 있는 합니다. 이러한 패턴을 따르는 경우 웹 계층, 쉽게 확장할 수 있습니다 및 각 서버는 더 많은 트래픽을 처리할 수 있기 때문에 프로그램 비용을 최소화 합니다.

[다음 장에서](single-sign-on.md) 클라우드 single sign-on 시나리오를 사용 하는 방법을 살펴봅니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조 합니다.

상태 비저장 웹 서버:

- [Microsoft Patterns and Practices-자동 크기 조정 지침](https://msdn.microsoft.com/library/dn589774.aspx)합니다.
- [해제 ARR 인스턴스에서 Windows Azure 웹 사이트에서 선호도](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)합니다. 블로그 게시물 Erez Benari 하 여 세션 선호도 Windows Azure 웹 사이트에 설명 합니다.

CDN:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms 하 여 비디오 시리즈를 9 개 부분으로 구성 합니다. 1시 34분: 00에서 시작 하는 3 에피소드에서 CDN을 참조 합니다.
- [Microsoft 패턴 및 사례 정적 콘텐츠 호스팅 패턴](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 검토](http://www.cdnreviews.com/)합니다. 많은 Cdn 간략하게 설명 합니다.

비동기 프로그래밍:

- [비동기 메서드를 사용 하 여 ASP.NET MVC 4의에서](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)합니다. Rick anderson 자습서입니다.
- [비동기 사용한 비동기 프로그래밍 및 Await (C# 및 Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx)합니다. MSDN는 백서 비동기 프로그래밍에 대 한 설명, ASP.NET 4.5에서 작동 방식 및 구현 하는 코드를 작성 하는 방법을 설명 합니다.
- [Entity Framework 비동기 쿼리 및 저장](https://msdn.microsoft.com/data/jj819165)
- [비동기 사용 하 여 ASP.NET 웹 응용 프로그램을 작성 하는 방법](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)합니다. Rowan Miller의 비디오 프레젠테이션 합니다. 그래픽 데모 포함 어떻게 비동기 프로그래밍의 부하가 높은 상황에서 웹 서버 처리량을 크게 향상으로 기여할 수 있습니다.
- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms 하 여 비디오 시리즈를 9 개 부분으로 구성 합니다. 확장성 비동기 프로그래밍의 영향에 대 한 토론 에피소드 4 및 8 에피소드를 참조 하십시오.
- [ASP.NET 4.5 및 중요 한 취약점의 비동기 메서드를 사용 하 여 매직](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx)합니다. ASP.NET Web Forms 응용 프로그램에서 async 사용에 대 한 주로 Scott hanselman 블로그 게시물입니다.

추가 웹 개발 모범 사례에 대 한 다음 리소스를 참조 합니다.

- [수정 프로그램 응용 프로그램-모범 사례를 샘플](the-fix-it-sample-application.md#bestpractices)합니다. 이 전자책 부록 수정 응용 프로그램에서 구현 된 모범 사례 수를 나열 합니다.
- [웹 개발자 검사 목록](http://webdevchecklist.com/asp.net)

>[!div class="step-by-step"]
[이전](continuous-integration-and-continuous-delivery.md)
[다음](single-sign-on.md)
