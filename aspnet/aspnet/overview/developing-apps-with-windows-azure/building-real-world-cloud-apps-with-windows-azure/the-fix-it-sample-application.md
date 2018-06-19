---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '부록: 수정 프로그램 것 샘플 응용 프로그램 (Azure 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs'
author: MikeWasson
description: 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 9a1fa36b34c4783b101bb27bc6931241e9251e10
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30876477"
---
<a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>부록: 수정 프로그램 것 샘플 응용 프로그램 (Azure 사용 하 여 실제 클라우드 앱 빌드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[이 프로젝트 수정 프로그램을 다운로드](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


이 부록의 내용에는 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 수정 샘플 응용 프로그램을 다운로드할 수에 대 한 추가 정보를 제공 하는 다음 섹션에서는 포함 되어 있습니다.

- [알려진된 문제](#knownissues)
- [모범 사례](#bestpractices)
- [로컬 컴퓨터에서 Visual Studio에서 앱을 실행 하는 방법](#run-in-vs)
- [Azure 앱 서비스 웹 앱을 Windows PowerShell 스크립트를 사용 하 여 기본 응용 프로그램을 배포 하는 방법](#deploybase)
- [Windows PowerShell 스크립트 문제 해결](#troubleshooting)
- [Azure 앱 서비스 웹 앱 및 Azure 클라우드 서비스를 처리 하는 큐와 응용 프로그램을 배포 하는 방법](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>알려진 문제

수정 앱 간단 하 게 가능한 한이 전자책에 제공 된 일부 패턴을 보여 주기 위해 원래 개발 되었습니다. 그러나 실제 응용 프로그램을 작성 하는 방법에 대 한 전자책 이므로, 우리 거쳐야 수정 코드 검토 및 테스트 프로세스를 어떻게 할 경우이 출시 된 소프트웨어에 대 한 유사 합니다. 다양 한 문제를 발견 했습니다 및 모든 실제 응용 프로그램에서와 마찬가지로 그 중 일부를 해결 하 고 그 중 일부에서는 지연 된 이후 릴리스로 합니다.

다음 목록에는 문제를 해결 해야 할 이유 중 하나 또는 다른 수정 샘플 응용 프로그램의 초기 릴리스에서 주소로 하지 하기로 결정에 대 한 프로덕션 응용 프로그램에 포함 됩니다.

### <a name="security"></a>보안

- 존재 하지 않는 소유자에 게 작업을 할당할 수 없다는 것을 확인 합니다.
- 할 수 있는 확인 하십시오. 확인 하 고 작성 하거나 할당 된 작업을 수정 합니다.
- 로그인 페이지 및 인증 쿠키에 대 한 HTTPS를 사용 합니다.
- 인증 쿠키에 대 한 제한 시간을 지정 합니다.

### <a name="input-validation"></a>입력된 유효성 검사

프로덕션 응용 프로그램 수행 하려면 일반적으로 수정 응용 프로그램 보다 더 많은 입력 유효성 검사 합니다. 예를 들어 이미지 크기가 이미지 업로드 제한 해야 합니다. 허용 된 파일 크기는 /입니다.

### <a name="administrator-functionality"></a>관리자 기능

관리자는 기존 작업에 대 한 소유권을 변경할 수 있어야 합니다. 예를 들어 작업의 작성자 관리 액세스를 사용 하지 않으면 작업을 유지 하기 위해 권한을 갖는 아무도 두면 회사를 않을 수 있습니다.

### <a name="queue-message-processing"></a>큐 메시지 처리

큐 메시지 수정 응용 프로그램에서 처리는 최소한의 코드를 사용 하 여 큐 중심 작업 패턴을 보여 주기 위해 간단한 되도록 설계 되었습니다. 이 간단한 코드는 실제 생산 응용 프로그램에 대 한 적절 한 수 없습니다.

- 코드는 각 큐 메시지를 한 번만 처리할 수는 보장 하지 않습니다. 큐에서 메시지를 받아야 하는 경우에 다음과 같은 다른 큐 수신기에 표시 되지 않는 메시지는 특정 제한 시간 기간. 제한 시간 메시지를 삭제 하기 전에 만료 되 면 메시지가 다시 표시 됩니다. 따라서 작업자 역할 인스턴스 메시지를 처리 하는 오랜 시간이 소요, 경우 논리적으로 동일한 메시지를 두 번 처리 가능 데이터베이스에 중복 된 작업에서으로 인해 발생 합니다. 이 문제에 대 한 자세한 내용은 참조 [Azure 저장소 큐를 사용 하 여](https://msdn.microsoft.com/library/ff803365.aspx#sec7)합니다.
- 메시지 검색 일괄 처리 하 여 큐 폴링 논리 더 비용 효율적일 수 있습니다. 호출할 때마다 [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), 트랜잭션 비용이 발생 합니다. 대신, 호출 수 [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (복수로 참고 ')는 단일 트랜잭션 내에서 여러 메시지를 가져옵니다. Azure 저장소 큐에 대 한 트랜잭션 비용이 매우 낮은 되므로 비용에 미치는 영향에 대부분의 시나리오에서 크지 않습니다.
- 큐 메시지 처리 코드에서 루프 멀티 코어 Vm을 효율적으로 사용 하지 않는 CPU 선호도 사용 하면 합니다. 더 나은 디자인 병렬로 여러 비동기 작업을 실행 하려면 작업 병렬 처리를 사용 합니다.
- 큐 메시지 처리만 기초적인 예외 처리를 있습니다. 코드 처리 되지 않습니다. 예를 들어 [포이즌 메시지](https://msdn.microsoft.com/library/ms789028.aspx)합니다. (메시지 처리 예외를 발생 시키는 경우 하 여 오류를 기록 하 고 메시지를 삭제 해야 또는 작업자 역할에서 다시 처리 하려고 및 루프가 무기한 계속 됩니다.)

### <a name="sql-queries-are-unbounded"></a>SQL 쿼리 바인딩되지 않습니다.

현재 수정 코드 인덱스 페이지에 대 한 쿼리를 반환할 수 있습니다 하는 행 수에 제한이 없음을 배치 합니다. 많은 양의 작업을 데이터베이스에 입력 하는 경우 수신 결과 목록의 크기 성능 문제가 발생할 수 있습니다. 솔루션은 페이징을 구현 하는 것입니다. 예를 들어 참조 [정렬, 필터링 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 페이징](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)합니다.

### <a name="view-models-recommended"></a>권장 모델 보기

수정 앱 FixItTask 엔터티 클래스를 사용 하 여 컨트롤러와 뷰 간에 정보를 전달 합니다. 모델 보기를 사용 하는 것이 좋습니다. 도메인 모델 (예: FixItTask 엔터티 클래스)는 필요한 데이터 지 속성에 대 한 데이터를 나타내는 보기 모델을 설계 하는 동안 기반으로 설계 되었습니다. 자세한 내용은 참조 [12 ASP.NET MVC 모범 사례](http://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)합니다.

### <a name="secure-image-blob-recommended"></a>권장 되는 보안 이미지 blob

수정 앱 스토어 이미지에 액세스할 수 있도록 모든 사용자에 게 URL를 찾습니다.을 의미 하는 public으로 이미지를 업로드 합니다. 공용이 아닌 이미지를 보안 할 수 없습니다.

### <a name="no-powershell-automation-scripts-for-queues"></a>큐에 대 한 PowerShell 자동화 스크립트가 없습니다

샘플 PowerShell 자동화 스크립트의 수정이 Azure 앱 서비스 웹 앱 내에서 실행 하는 기본 버전에 대해서만 작성 되었습니다. 설정 하 고 웹 응용 프로그램 및 큐 처리에 필요한 클라우드 서비스 환경에 배포에 대 한 스크립트를 제공 하지 않은 해 드립니다.

### <a name="special-handling-for-html-codes-in-user-input"></a>사용자 입력에 있는 HTML 코드에 대 한 특수 처리

ASP.NET에는 자동으로 사용자 입력된 텍스트 상자에 스크립트를 입력 하 여 악의적인 사용자가 사이트 간 스크립팅 공격이 시도할 수 있습니다는 여러 가지 방법으로 방지 합니다. 와 MVC `DisplayFor` 작업을 표시 하는 데 사용 되는 도우미 제목의 브라우저로 전송 되는 HTML로 인코딩하고 값을 자동으로 인식 합니다. 하지만 추가 조치를 취해야 할 프로덕션 응용 프로그램. 자세한 내용은 참조 [ASP.NET에서 유효성 검사 요청](https://msdn.microsoft.com/library/hh882339.aspx)합니다.

<a id="bestpractices"></a>
## <a name="best-practices"></a>최선의 구현 방법

다음은 코드 검토에서 검색 하 고 수정 응용 프로그램의 원래 버전의 테스트 된 후 수정 된 몇 가지 문제입니다. 사용 되 고 있지 특정 최상의 인식 일부 단순히 원래 코더로 인해 일부 코드를 신속 하 게 쓴 및 출시 된 소프트웨어에 대 한 의도 되지 않은 때문에 있습니다. 이 검토에서 이전에 배운 것 리 경우 여기에 문제를 나열 하는 것 및 테스트는 웹 응용 프로그램을 개발 하는 또한 다른 사용자에 게 도움이 될 수 있습니다.

### <a name="dispose-the-database-repository"></a>데이터베이스 저장소를 삭제 합니다.

`FixItTaskRepository` 클래스는 Entity Framework를 삭제 해야 `DbContext` 인스턴스. 구현 하 여 줄였습니다 `IDisposable` 에 `FixItTaskRepository` 클래스:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

AutoFac를 자동으로 삭제 하는 `FixItTaskRepository` 인스턴스를 명시적으로를 삭제할 필요가 없습니다.

또 다른 옵션은 제거 하는 `DbContext` 에서 멤버 변수 `FixItTaskRepository`, 로컬 만드는 `DbContext` 각 저장소 메서드 내에서 변수 내는 `using` 문. 예를 들어:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>DI 따라서 singleton 등록

인스턴스가 하나만 이후에 `PhotoService` 클래스 및 `Logger` 클래스가 필요한 경우 이러한 클래스 이어야 합니다 [종속성 주입을 위한 단일 인스턴스로 등록](https://code.google.com/p/autofac/wiki/InstanceScope) 에 *DependenciesConfig.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>보안: 사용자에 게 오류 세부 정보를 표시 안 함

원래 수정 앱 일반 오류 페이지 및 브라우저에 표시 되는 전체 스택 추적에서 데이터베이스 연결 오류와 같은 몇 가지 예외가 발생할 수 있도록 UI에 게 모든 예외가 전달 자동 하지 않았습니다. 자세한 오류 정보는 사용자의 악의적인 공격을 쉽게 경우가 수 있습니다. 해결 방법은 예외 세부 정보를 기록 하 고 오류 정보가 포함 되지 않은 사용자에 게 오류 페이지를 표시 하는 것입니다. 오류 페이지를 표시 하기 위해 추가 하 고 수정 응용 프로그램 로깅을 이미가 `<customErrors mode=On>` Web.config 파일에 있습니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

이렇게 하면 기본적으로 *Views\Shared\Error.cshtml* 오류에 대해 표시 되도록 합니다. 사용자 지정할 수 있습니다 *Error.cshtml* 또는 오류 페이지 뷰를 직접 만들고 추가 `defaultRedirect` 특성입니다. 특정 오류에 대 한 다른 오류 페이지를 지정할 수 있습니다.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>보안: 작업의 작성자에 의해 편집 허용

대시보드 인덱스 페이지 로그온 한 사용자가 만든 작업에만 표시 하지만 악의적인 사용자가 다른 사용자의 작업 ID와 URL을 생성할 수 있습니다. 코드를 추가 했습니다 *DashboardController.cs* 경우 404 반환할:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>예외를 무시 하지 마십시오

원래 수정 앱만 null을 반환 했습니다 다음 SQL 쿼리 결과로 발생 된 예외:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

이 경우 하 게 사용자에 게 처럼 보이지만 쿼리가 성공 방금 모든 행을 반환 하지 않았습니다. 해결 방법은 다시 catch 및 로깅에서 처리 한 예외를 throw 하는입니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>작업자 역할에서 모든 예외를 catch 합니다.

작업자 역할에서 처리 되지 않은 예외에는 VM이 재활용 될 하면, try catch 블록에서 작업을 수행 하 고 모든 예외를 처리할 모든 항목을 배치 하려고 합니다.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>엔터티 클래스에 문자열 속성에 대 한 길이 지정

간단한 코드를 표시 하기 위해 수정 응용 프로그램의 원래 버전 FixItTask 엔터티의 필드에 대 한 길이 지정 하지 않은 하 고 결과적으로 데이터베이스에는 varchar (max)로 정의 된 것입니다. 결과적으로, UI는 거의 모든 양을 입력을 수락 합니다. 데이터베이스에 대 한 열 크기를 확인 하 고 웹 페이지에서 사용자에 게 모두 적용 되는 지정 하 여 길이 집합 제한 입력:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>변경 하려면 예상 하지 못한 경우 읽기 전용으로 전용 멤버 표시

예를 들어는 `DashboardController` 클래스의 인스턴스 `FixItTaskRepository` 만들어지고로 정의한 하므로 변경 하려면 예상 되지 않습니다 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)합니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>Use list.Any() instead of list.Count() &gt; 0

모든 중요 한 하면 하나 이상의 항목 목록에 지정된 된 조건에 맞는지 사용 중인 경우는 [모든](https://msdn.microsoft.com/library/bb534972.aspx) 메서드를 반환 하기 때문에으로 기준에 맞는 항목을 찾을 수 있지만 `Count` 메서드는 항상 반복 하는 통해 모든 항목입니다. 대시보드 *Index.cshtml* 파일에는 원래이 코드에:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

이를 변경 했습니다.

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>MVC 도우미를 사용 하 여 MVC 뷰에 Url을 생성 합니다.

에 대 한는 **만들는 해결** 홈 페이지에서 수정 앱 하드 코딩는 앵커 요소:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

다음과 같은 보기/작업 링크는 것이 좋습니다 사용 하는 [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 도우미, 예:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>Thread.Sleep 대신 Task.Delay를 사용 하 여 작업자 역할에서

새 프로젝트 템플릿은 배치 `Thread.Sleep` 스레드가 중지 배정만 작업자 역할에 대 한 코드 샘플에서 추가 불필요 한 스레드를 생성 하는 스레드 풀 발생할 수 있습니다. 사용 하 여 방지할 수 있습니다 [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) 대신 합니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>Async void 방지

반환 비동기 메서드는 값을 반환할 필요가 없습니다, 하는 경우는 `Task` 형식 대신 `void`합니다.

이 예제에서는 `FixItQueueManager` 클래스: 

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

사용 해야 `async void` 최상위 이벤트 처리기에 대 한 합니다. 메서드를 정의 하는 경우 `async void`, 호출자에 게 없습니다 **await** 메서드는 메서드가 throw 하는 모든 예외를 catch 합니다. 자세한 내용은 참조 [비동기 프로그래밍에 대 한 모범 사례](https://msdn.microsoft.com/magazine/jj991977.aspx)합니다. 

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>취소 토큰을 사용 하 여 작업자 역할 루프 분해

일반적으로 **실행** 작업자 역할에서 메서드는 무한 루프를 포함 합니다. 작업자 역할을 중지 하는 경우는 [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 메서드를 호출 합니다. 내부 수행 되는 작업을 취소 하는이 메서드를 사용 해야는 **실행** 메서드와 종료 적절 하 게 합니다. 그렇지 않으면 작업 중간에 프로세스가 종료 될 수 있습니다.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>MIME 스니핑 프로시저 자동 취소

경우에 따라 Internet Explorer와 웹 서버에서 지정한 형식과 다른 MIME 형식을 보고 합니다. 예를 들어, 발견 한 경우 Internet Explorer HTML 콘텐츠 Content-type의 HTTP 응답 헤더와 함께 제공 되는 파일에: text/plain Internet Explorer 콘텐츠를 HTML로 렌더링 해야 함을 확인 합니다. 그러나이 "MIME 스니핑" 신뢰할 수 없는 콘텐츠를 호스팅하는 서버에 대 한 보안 문제를 발생할 수도 수 있습니다. 이 문제를 방지 하기 위해 Internet Explorer 8 MIME 형식을 결정 코드에 변경 사항을 수행한 및 응용 프로그램 개발자가 수 있도록 [MIME 스니핑 하지 않을](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)합니다. 다음 코드에 추가한는 *Web.config* 파일입니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>묶음 및 축소를 사용 하도록 설정

Visual Studio에서 새 웹 프로젝트를 만들 때 묶음 및 축소 JavaScript 파일의는 기본값으로 사용할 수 없습니다. 코드 줄을 BundleConfig.cs에 추가 되었습니다.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>인증 쿠키에 대 한 만료 제한 시간을 설정 합니다.

기본적으로 인증 쿠키 2 주 이내에 만료 됩니다. 더 짧은 시간은 더 안전 합니다. 이 설정을 변경할 수 있습니다 *StartupAuth.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>로컬 컴퓨터에서 Visual Studio에서 앱을 실행 하는 방법

수정 응용 프로그램을 실행 하는 방법은 두 가지가 있습니다.

- SQL 데이터베이스에 직접 새 작업을 기록 하는 기본 응용 프로그램을 실행 합니다.
- 작업을 만들어 큐와 백 엔드 서비스를 사용 하 여 응용 프로그램을 실행 합니다. 큐 패턴 장에서 설명 [큐 중심 작업 패턴](queue-centric-work-pattern.md)합니다.

<a id="runbase"></a>
### <a name="run-the-base-application"></a>기본 응용 프로그램 실행

1. 설치 [Visual Studio 2013 또는 Visual Studio 2013 Express for Web](https://www.visualstudio.com/downloads)합니다.
2. 설치는 [Azure SDK for.NET Visual Studio 2013 용입니다.](https://go.microsoft.com/fwlink/p/?linkid=323510&amp;clcid=0x409)
3. .zip 파일을 다운로드는 [MSDN 코드 갤러리](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)합니다.
4. 파일 탐색기에서.zip 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 한 다음 속성 창에서 차단 해제를 클릭 합니다.
5. 파일을 압축을 풉니다.
6. Visual Studio를 시작.sln 파일을 두 번 클릭 합니다.
7. 도구 메뉴에서 라이브러리 패키지 관리자 차례로 패키지 관리자 콘솔을 클릭 합니다.
8. 패키지 관리자 콘솔 (PMC)에서 복원을 클릭 합니다.
9. Visual Studio를 끝냅니다.
10. 시작 된 [Azure 저장소 에뮬레이터](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)합니다.
11. 이전 단계에서 닫은 솔루션 파일을 열면 Visual Studio를 다시 시작 합니다.
12. FixIt 프로젝트가 시작 프로젝트로 설정 되어 있는지 확인 하 고 CTRL + f 5를 눌러 프로젝트를 실행 합니다.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>큐 처리를 응용 프로그램을 실행 합니다.

1. 에 대 한 지침을 따르고 [기본 응용 프로그램을 실행](#runbase), 한 다음 브라우저를 닫고 Visual Studio를 닫습니다.
2. 관리자 권한으로 Visual Studio를 시작 합니다. (Azure 계산 에뮬레이터를 사용 합니다 및 하는 경우 관리자 권한이 필요 합니다.)
3. 응용 프로그램에서 *Web.config* 파일에 *MyFixIt* 프로젝트 (웹 프로젝트)의 값을 변경 하세요 `appSettings/UseQueues` "true"로: 

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. 경우는 [Azure 저장소 에뮬레이터](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 여전히 실행 되지 않습니다. 다시 시작 합니다.
5. FixIt 웹 프로젝트와 MyFixItCloudService 프로젝트를 동시에 실행 합니다.

    Visual Studio 2013을 사용 합니다.

   1. F5 키를 눌러 FixIt 프로젝트를 실행 합니다.
   2. **솔루션 탐색기**MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **디버그** -- **새 인스턴스 시작**합니다.

      Visual Studio 2013 Express for Web 사용:

   3. 솔루션 탐색기에서 FixIt 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.
   4. 선택 **여러 개의 시작 프로젝트**...
   5. 에 **동작** MyFixIt 및 MyFixItCloudService, 아래의 드롭다운 목록 선택 **시작**합니다.
   6. **확인**을 클릭합니다.
   7. F5 키를 눌러 프로젝트를 모두 실행 합니다.

      MyFixItCloudService 프로젝트를 실행할 때 Visual Studio는 Azure 계산 에뮬레이터를 시작 합니다. 방화벽 구성에 따라 방화벽을 통해 에뮬레이터를 허용 하도록 할 수 있습니다.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Azure 앱 서비스 웹 앱을 Windows PowerShell 스크립트를 사용 하 여 기본 응용 프로그램을 배포 하는 방법

설명 하기 위해는 [모든 자동화](automate-everything.md) 수정 응용 프로그램 패턴 azure에서 환경을 구성 하 고 새 환경에 프로젝트를 배포 하는 스크립트와 함께 제공 됩니다. 다음 지침에서는 스크립트를 사용 하는 방법을 설명 합니다.

큐를 사용 하지 않고 Azure에서 실행 하 고 변경 큐를 사용 하 여 로컬로 실행 하는 경우 다음 지침을 진행 하기 전에 false로 다시 UseQueues appSetting 값을 설정 했는지 확인 합니다.

이 지침에서는 이미 다운로드 하 고 수정 솔루션을 로컬에서 실행할 수 있는 Azure 계정 또는 Azure 구독이 있는 가정 관리 권한이 있는 합니다.

1. 설치는 **Azure PowerShell** 콘솔. 자세한 내용은 [Azure PowerShell 설치 및 구성 하는 방법을](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)합니다.

    이 사용자 지정 된 콘솔은 Azure 구독과 함께 작동 하도록 구성 됩니다. 에 설치 된 Azure 모듈의 *Program Files* 디렉터리가 고 자동으로 사용 된 모든 Azure PowerShell 콘솔에 가져옵니다.

    Windows PowerShell ISE 등의 다른 호스트 프로그램에서 작업 하려는 경우 사용 해야는 [Import-module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet을 Azure 모듈을 가져올 하거나 Azure 모듈의 명령을 사용 하 여 모듈 자동 가져오기를 트리거합니다.
2. Azure PowerShell을 시작는 **관리자 권한으로 실행** 옵션입니다.
3. 실행 된 [Set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) Azure PowerShell 실행 정책을 설정 하는 cmdlet `RemoteSigned`합니다. 입력 **Y** (예)에 대 한 정책 변경을 완료 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    이 설정은 디지털 서명 하지 않은 로컬 스크립트를 실행할 수 있습니다. (실행 정책을 설정할 수도 있습니다 `Unrestricted`, 나중에 차단 해제 단계에 대 한 필요성을 제거 합니다는 있지만이 보안상의 이유로 권장 되지 않습니다.)
4. 실행의 `Add-AzureAccount` cmdlet을 계정에 대 한 자격 증명으로 PowerShell을 설정 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    이러한 자격 증명 시간이 지나면 만료 되 고 다시 실행 해야는 `Add-AzureAccount` cmdlet. 자격 증명 만료 전에 시간 제한이이 전자책 작성 될 때 12 시간 합니다.
5. 여러 구독이 있는 경우 테스트 환경에서 만들려는 구독을 지정 하려면 Select-azuresubscription cmdlet을 사용 합니다.
6. 동일한 Azure 구독에 대 한 관리 인증서를 사용 하 여 가져오기는 `Get-AzurePublishSettingsFile` 및 `Import-AzurePublishSettingsFile` cmdlet. 이러한 cmdlet 중 첫 번째 인증서 파일을 다운로드 하 고 두 번째 것을 가져오려면 해당 파일의 위치 지정 합니다. > [!IMPORTANT]
   > 다운로드 한 파일을 안전한 위치에 보관 하거나 Azure 서비스를 관리 하는 데 사용할 수 있는 인증서를 포함 하기 때문에, 완료 되 면 삭제 됩니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    인증서는 사용 되는 SQL 데이터베이스 서버에서 방화벽 규칙을 설정 하기 위해 개발 컴퓨터의 IP 주소를 검색 하는 REST API 호출에 대 한 합니다.
7. 실행 된 [Set-location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (별칭은 `cd`, `chdir`, 및 `sl`) 스크립트가 포함 된 디렉터리로 이동 하 합니다. (에 위치 하는 *자동화* 수정 솔루션 폴더의 폴더입니다.) 디렉터리 이름에 공백이 포함 되어 있으면 경로 따옴표로 묶습니다. 예를 들어로 이동 하는 `c:\Sample Apps\FixIt\Automation` 디렉터리 다음 명령을 입력할 수 있습니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. 이러한 스크립트를 실행 하려면 Windows powershell을 사용 하 여는 [Unblock-file](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet. (스크립트 때문에 차단 됩니다 인터넷에서 다운로드 합니다.)

    > [!WARNING]
    > 실행 하기 전에 보안- `Unblock-File` 모든 스크립트 또는 실행 파일에 메모장에서 파일을 열고, 검사는 명령을 사용 하 고 모든 악성 코드가 포함 되지 않았는지 확인 합니다.

    예를 들어 다음 명령이 실행 되는 `Unblock-File` 현재 디렉터리에서 모든 스크립트에는 cmdlet입니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. Base (큐 처리)에 대 한 웹 앱을 만들려면 응용 프로그램을 수정, 환경 만들기 스크립트를 실행 합니다.

    필요한 `Name` 매개 변수는 데이터베이스의 이름을 지정 하 고 스크립트에서 만들어진 저장소 계정에도 사용 됩니다. 이름은은 azurewebsites.net 도메인 내에서 전역적으로 고유 해야 합니다. Fixit 또는 테스트와 같은 (또는 심지어는 예와 fixitdemo) 고유 하지 않은 이름을 지정 하는 경우는 `New-AzureWebsite` cmdlet 충돌이 보고 하는 내부 오류와 함께 실패 합니다. 스크립트를 웹 응용 프로그램, 저장소 계정 및 데이터베이스에 대 한 이름 요구 사항을 충족 하기 위해 모두 소문자 이름을 변환 합니다.

    필요한 `SqlDatabasePassword` 매개 변수는 SQL 데이터베이스에 대해 만들 관리자 계정의 암호를 지정 합니다. 암호에 특수 XML 문자를 포함 하지 않음 (&amp; &lt; &gt; ;). 스크립트 작성 된 Azure의 제한 사항 하지 하는 방식의 제한 사항입니다.

    예를 들어 "fixitdemo" 라는 웹 앱을 만들고 "Passw0rd1"의 SQL Server 관리자 암호를 사용 하려는 경우 다음 명령을 입력할 수 있습니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    Azurewebsites.net 도메인에서 이름이 고유 해야 하며 SQL 데이터베이스 암호 복잡성 요구 사항을 만족 해야 합니다. (Passw0rd1 예제에는 요구를 충족지 않습니다.)

    명령으로 시작 하는 참고 "입니다. \". 악성 스크립트 실행을 방지 하려면 Windows PowerShell 스크립트를 실행 하면 스크립트 파일의 정규화 된 경로 제공 해야 합니다. 점을 사용 하 여 현재 디렉터리를 나타낼 수 있습니다 (".\") 또는 같은 정규화 된 경로 제공 합니다.

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    스크립트에 대 한 자세한 내용을 사용 하 여 `Get-Help` cmdlet.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    사용할 수는 `Detailed`, `Full`, `Parameters`, 및 `Examples` 반환 되는 도움말을 필터링 하려면 Get-help cmdlet의 매개 변수입니다.

    스크립트 실패 하거나 "New-azurewebsite:: 호출 집합 AzureSubscription 및 Select-azuresubscription 첫 번째," 등의 오류를 생성 하는 경우 있습니다 수 완료 되지의 Azure PowerShell 구성 합니다.

    스크립트가 완료 된 후에 표시 된 대로 생성 된 리소스를 참조 하는 Azure 관리 포털을 사용할 수 있습니다는 [모든 자동화](automate-everything.md) 장 합니다.
10. 새 Azure 환경에 FixIt 프로젝트를 배포 하려면 사용 된 *AzureWebsite.ps1* 스크립트입니다. 예를 들어:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    배포를 수행할 때와 해결 Azure에서 실행 되는 브라우저를 엽니다.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell 스크립트 문제 해결

이러한 스크립트를 실행할 때 발생 한 가장 일반적인 오류는 사용 권한 관련 되어 있습니다. 다음 사항을 확인 `Add-AzureAccount` 및 `Import-AzurePublishSettingsFile` 성공 하 고 동일한 Azure 구독에 사용한 것입니다. 경우에 `Add-AzureAccount` 가 성공 해야 다시 실행 합니다. 추가 된 권한을 `Add-AzureAccount` 12 시간 후 만료 됩니다.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>개체 참조가 개체의 인스턴스로 설정되지 않았습니다.

스크립트 실행 하는 "개체 참조가 개체의 인스턴스로 설정 되지 않습니다" 즉, Windows PowerShell (이 null 참조 예외가) 프로세스에 개체를 찾을 수 없습니다와 같은 오류를 반환 하는 경우는 `Add-AzureAccount` cmdlet 스크립트를 다시 시도 하십시오.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: 서버에 내부 오류가 발생 했습니다.

`New-AzureWebsite` cmdlet 이름이 고유 하지 않을 때 azurewebsites.net 도메인에서 내부 오류를 반환 합니다. 이 오류를 해결 하려면 다른 값의 Name 매개 변수에 있는 이름에 대 한 사용 하 여 *새로 AzureWebsiteEnv.ps1*합니다.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>스크립트를 다시 시작

다시 시작 해야 하는 경우는 *새로 AzureWebsiteEnv.ps1* 스크립트 "스크립트가 완료 되" 메시지를 인쇄 하기 전에 실패 했으므로 하기 전에 만든 스크립트를 중지 하는 리소스를 삭제 하려고 할 수 있습니다. 예를 들어 스크립트를 이미 만든 ContosoFixItDemo 웹 앱과 이름이 같은 스크립트를 다시 실행 하는 경우에 이름이 사용 중에서 이므로 스크립트 실패 합니다.

리소스 중지 전에 만든 스크립트를 확인 하려면 다음 cmdlet을 사용 합니다.

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`:이 cmdlet을 실행 하는 데이터베이스 서버 이름을 파이프 `Get-AzureSqlDatabase`:  
    `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

이러한 리소스를 삭제 하려면 다음 명령을 사용 합니다. 데이터베이스 서버를 삭제 하면 자동으로 삭제 하면 서버와 연결 된 데이터베이스를 참고 합니다.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Azure 앱 서비스 웹 앱 및 Azure 클라우드 서비스를 처리 하는 큐와 응용 프로그램을 배포 하는 방법

큐를 사용 하도록 설정 하려면 다음과 같이 변경 하면 MyFixIt\Web.config 파일에서 이어야 합니다. 아래 `appSettings`의 값을 변경 `UseQueues` "true"로: 

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

다음 설명 된 대로 Azure 앱 서비스의 웹 앱에 MVC 응용 프로그램을 배포 [이전](#deploybase)합니다.

다음으로 새 Azure 클라우드 서비스를 만듭니다. 수정 응용 프로그램에 포함 된 스크립트 만들기 하지 않거나이 대 한 Azure 포털을 사용 해야 클라우드 서비스를 배포 합니다. 포털에서 클릭 **새로** -- **계산** – **클라우드 서비스** -- **빠른 생성**, 다음 URL을 입력 하 고 및 데이터 센터 위치입니다. 웹 앱을 배포한 동일한 데이터 센터를 사용 합니다.

![](the-fix-it-sample-application/_static/image1.png)

클라우드 서비스를 배포 하려면 먼저 구성 파일 중 일부를 업데이트 해야 합니다.

MyFixIt.WorkerRoler\app.config에서 아래 `connectionStrings`의 값을 바꿉니다는 `appdb` SQL 데이터베이스에 대 한 실제 연결 문자열과 연결 문자열입니다. 포털에서 연결 문자열을 가져올 수 있습니다. 포털에서 클릭 **SQL 데이터베이스** - **appdb** - **ADO.Net, ODBC, PHP 및 JDBC에 대 한 보기 SQL 데이터베이스 연결 문자열**합니다. ADO.NET 연결 문자열을 복사 하 고 값을 app.config 파일에 붙여넣습니다. 대체 "{프로그램\_암호\_여기}" 데이터베이스 암호를 사용 합니다. (에 데이터베이스 암호를 지정한 MVC 앱을 배포 하는 스크립트를 사용 하는 것으로 가정 합니다는 `SqlDatabasePassword` 매개 변수를 스크립팅 합니다.)

결과 다음과 같이 표시 됩니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

같은 MyFixIt.WorkerRoler\app.config 파일에 아래 `appSettings`, Azure 저장소 계정에 대 한 두 자리 표시자 값을 대체 합니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

포털에서 액세스 키를 가져올 수 있습니다. 참조 [저장소 계정을 관리 하는 방법을](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)합니다.

MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, Azure 저장소 계정에 대 한 동일한 두 자리 표시자 값을 대체 합니다.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

이제 클라우드 서비스를 배포할 준비가 되었습니다. 솔루션 탐색기 MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. 자세한 내용은 참조 하십시오. "[Azure에 응용 프로그램을 배포](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", 2 부에 [이 자습서](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)합니다.

> [!div class="step-by-step"]
> [이전](more-patterns-and-guidance.md)
