---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: "연결 복원 력 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 명령 인터 셉 션 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/13/2015
ms.topic: article
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 1a28284e203904cc943e5e46b369e8a58ea5c820
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="connection-resiliency-and-command-interception-with-the-entity-framework-in-an-aspnet-mvc-application"></a>연결 복원 력 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 인터 셉 션 명령
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.


지금까지 응용 프로그램에 되었습니다에서 로컬로 실행 중 IIS Express에서 개발 컴퓨터. 실제 응용 프로그램을 인터넷을 통해 사용 하 여 다른 사람들이 사용할 수 있도록 하는 웹 호스팅 공급자를 배포 해야 하며 데이터베이스 서버에 데이터베이스를 배포 하 해야 합니다.

이 자습서에는 클라우드 환경에 배포 하는 경우에 특히 유용 Entity Framework 6의 두 가지 기능을 사용 하는 방법을 배우게 됩니다: 연결 복원 력 (일시적인 오류에 대 한 자동 다시 시도) 및 명령 인터 셉 션 (모든 catch SQL 쿼리 전송 로그 하거나 변경 하려면 데이터베이스).

이 연결 복원 력 및 명령 인터 셉 션 자습서 선택 사항입니다. 이 자습서를 건너뛰면 몇 가지 약간 조정 경우 이후 자습서에서 수행 될 수 있습니다.

## <a name="enable-connection-resiliency"></a>연결 복원 력 설정

Windows Azure에 응용 프로그램을 배포 하면 Windows Azure SQL 데이터베이스, 클라우드 데이터베이스 서비스에 데이터베이스를 배포 합니다. 일시적인 연결 오류는 경우 웹 서버와 데이터베이스 서버에 직접 연결 된 함께 동일한 데이터 센터에 클라우드 데이터베이스 서비스에 연결할 때 일반적으로 더 자주 발생 합니다. 클라우드 웹 서버와 클라우드 데이터베이스 서비스는 동일한 데이터 센터에서 호스팅되는, 경우에 연결이 더 많은 네트워크 간 부하 분산 장치와 같은 문제가 발생할 수 있습니다.

또한 클라우드 서비스는 일반적으로 공유 다른 사용자가 응답에 따라 달라질 수 있습니다. 및 데이터베이스에 대 한 액세스 제한을 적용 될 수 있습니다. 서비스 수준 계약 (SLA)에서 허용 하는 것 보다 더 많은 것 자주 액세스 하려고 할 때 데이터베이스 서비스 예외를 throw 의미를 제한 합니다.

클라우드 서비스에 액세스할 때 수가 많거나 대부분 연결 문제는 일시적인, 즉,은 자체적으로 해결 짧은 기간 동안 합니다. 따라서는 데이터베이스 작업을 시도 하 고 일반적으로 임시 오류 유형의 경우 짧은 대기 및 작업이 성공할 수 후에 작업을 다시 시도할 수 있습니다. 자동으로 다시 시도 하 여 일시적인 오류를 처리 하는 경우 사용자에 대 한 보다 나은 경험을 제공할 수 있습니다 대부분의 고객에 게 보이지 않는 수행 합니다. Entity Framework 6의 연결 복원 기능을 다시 시도 프로세스를 SQL 쿼리 실패 했음을 자동화 합니다.

특정 데이터베이스 서비스에 대 한 연결 복원 기능을 적절히 구성 되어야 합니다.

- 있기를 알고 있는 예외 일시적인 일 수 있습니다. 네트워크 연결에서 임시 손실로 인해 발생 한 오류 예를 들어 프로그램 버그로 인 한 오류 하지을 다시 시도 하려고 합니다.
- 후에 적절 한 양의 실패 한 작업의 다시 시도 간격을 대기 합니다. 대기할 수 있습니다 더 이상 일괄 처리에 대 한 재시도 간격 보다 온라인 웹 페이지의 사용자가 응답을 기다리는 여기서는 할 수 있습니다.
- 후에 적절 한 횟수를 포기 하기 전 다시 시도 합니다. 온라인 응용 프로그램에서 사용 하는 일괄 처리에서 번 더 다시 시도 할 수 있습니다.

Entity Framework 공급자에서 지 원하는 모든 데이터베이스 환경에 대해 수동으로 이러한 설정을 구성할 수 있지만 일반적으로 Windows Azure SQL 데이터베이스를 사용 하는 온라인 응용 프로그램에 대 한 잘 작동 하는 기본 값으로 이미 구성 및 이러한 설정은 Contoso 대학 응용 프로그램을 구현 합니다.

클래스에서 파생 하는 사용자 어셈블리에 만들어져 연결 복원 력 설정 하기 위해 해야 모든는 [DbConfiguration](https://msdn.microsoft.com/data/jj680699.aspx) 클래스와 해당 클래스에서 SQL 데이터베이스 설정 *실행 전략*, EF에서 변수인 에 대 한 다른 용어 *다시 시도 정책*합니다.

1. DAL 폴더에서 라는 클래스 파일을 추가 *SchoolConfiguration.cs*합니다.
2. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    파생 된 클래스에서 발견 하는 코드를 자동으로 실행 하는 Entity Framework `DbConfiguration`합니다. 사용할 수는 `DbConfiguration` 그렇지 않은 경우에 수행 하려면 코드에서 구성 작업을 수행 하는 클래스는 *Web.config* 파일입니다. 자세한 내용은 참조 [EntityFramework 코드 기반 구성](https://msdn.microsoft.com/data/jj680699)합니다.
3. *StudentController.cs*, 추가 `using` 문을 `System.Data.Entity.Infrastructure`합니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. 모든 변경 된 `catch` catch 하는 차단 `DataException` 예외를 포착할 수 있게 `RetryLimitExceededException` 예외 대신 합니다. 예:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    사용 하 던 `DataException` 친숙 한 "다시 시도" 메시지를 제공 하기 위해 일시적인 될 수 있는 오류를 식별 하려고 합니다. 하지만 다시 시도 정책에 설정한 했으므로 오류만 일시적인 일 수는 이미 시도 되어 여러 번 실패 했습니다 반환 된 실제 예외에 래핑됩니다는 `RetryLimitExceededException` 예외입니다.

자세한 내용은 참조 [Entity Framework 연결 복원 력 / 다시 시도 논리](https://msdn.microsoft.com/data/dn456835)합니다.

## <a name="enable-command-interception"></a>명령 인터 셉 션을 사용 하도록 설정

다시 시도 정책에 설정한 했으므로 어떻게 테스트 합니까 예상 대로 작동 하는지 확인? 일시적인 오류가 발생할 것인지, 특히를 로컬로 실행 하는 시점과 자동화 된 단위 테스트에 실제 일시적인 오류를 통합 하 특히 어려울 것 하기가 쉽지 않습니다. 연결 복원 기능을 테스트 하려면 SQL Server에 전송 하는 Entity Framework는 쿼리를 가로채 고 일반적으로 일시적인 예외 형식과 SQL 서버 응답을 대체 하는 방법이 필요 합니다.

클라우드 응용 프로그램에 대 한 모범 사례를 구현 하는 데 쿼리 인터셉터를 사용할 수도 있습니다: [대기 시간 및 성공 또는 실패 외부 서비스에 대 한 모든 호출의 기록](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) 예: 데이터베이스 서비스입니다. EF6 제공는 [로깅 API를 전용](https://msdn.microsoft.com/data/dn469464) 로깅, 보다 쉽게 만들 수는 있지만 자습서의이 섹션의 Entity Framework를 사용 하는 방법을 알아봅니다 [인터 셉 션 기능](https://msdn.microsoft.com/data/dn469464) 를 직접 모두에 대해 로깅 및 일시적인 오류를 시뮬레이션 하는 데 있습니다.

### <a name="create-a-logging-interface-and-class"></a>로깅 인터페이스 및 클래스 만들기

A [로깅에 대 한 최상의](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) 인터페이스를 사용 하 여 수행 하는 것 System.Diagnostics.Trace 또는 로깅 클래스에 대 한 호출을 하드 코딩 하는 대신 합니다. 이렇게 하기 위해 필요한 경우 나중에 로깅 메커니즘을 변경 하려면 쉽게 있습니다. 이 섹션의 로깅 인터페이스와 합니다. / p를 구현 하는 클래스를 만들 수 > 

1. 프로젝트의 폴더를 만들고 이름을 *로깅*합니다.
2. 에 *로깅* 폴더를 라는 클래스 파일을 만들 *ILogger.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    로그의 상대적 중요도를 나타내는 세 가지 추적 수준 및 데이터베이스 쿼리와 같은 외부 서비스 호출에 대 한 대기 시간 정보를 제공 하도록 지정 된 인터페이스를 제공 합니다. 로깅 메서드 예외에 전달할 수 있는 오버 로드를 갖고 있습니다. 이 응용 프로그램에 걸쳐 각 로깅 메서드 호출에서 수행 되 고에 의존 하지 않고 인터페이스를 구현 하는 클래스에서 스택 추적 및 내부 예외를 포함 하는 예외 정보를 안정적으로 기록 되도록 합니다.

    TraceApi 메서드를 사용 하 여 SQL 데이터베이스 같은 외부 서비스를 호출할 때마다 대기 시간을 추적할 수 있습니다.
3. 에 *로깅* 폴더를 라는 클래스 파일을 만들 *Logger.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    System.Diagnostics를 사용 하 여 추적 작업을 수행 하는 구현 합니다. 이 쉽게 생성 하 고 추적 정보를 사용 하 여.NET의 기본 제공 기능입니다. 많은 "수신자" 예를 들어 파일에 로그를 쓸 수 또는 azure에서 blob 저장소에 쓰려고 System.Diagnostics 추적으로 사용할 수 있습니다. 참조 하는 일부의 옵션 및 다른 리소스에 대 한 자세한 내용은 링크를 [Visual Studio에서 Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)합니다. Visual Studio에서이 자습서에 살펴봅니다만 로그 **출력** 창.

    ILogger 인터페이스를 사용 하면 비교적 쉽게 하는 작업을 결정 하는 경우 다른 추적 메커니즘으로 전환할 수과 프로덕션 응용 프로그램에서 System.Diagnostics 이외의 추적 패키지를 고려해 야 할 수입니다.

### <a name="create-interceptor-classes"></a>인터셉터 클래스 만들기

다음 Entity Framework에는 데이터베이스, 일시적인 오류를 시뮬레이션 하는 각각와 로깅 작업을 수행 하는 쿼리를 보낼 때마다을 호출 하는 클래스 만듭니다. 이러한 인터셉터 클래스에서 파생 되어야 합니다는 `DbCommandInterceptor` 클래스입니다. 여기에 쿼리를 실행 될 때 자동으로 호출 하는 메서드 재정의 작성할 수 있습니다. 이러한 메서드에 검사 하거나 데이터베이스로 전송 되는지 쿼리 기록 수 있으며 데이터베이스에 보내기 전에 쿼리를 변경 하거나 결과 반환 Entity Framework를 직접도 데이터베이스에 쿼리를 전달 하지 않고 수 있습니다.

1. 데이터베이스에 전송 된 모든 SQL 쿼리를 기록 하는 인터셉터 클래스를 만들려면 라는 클래스 파일을 만들 *SchoolInterceptorLogging.cs* 에 *DAL* 폴더 및 코드는 서식 파일 바꾸기 다음 코드는

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    이 코드는 성공적인 쿼리나 명령에 대 한 대기 시간 정보를 사용 하 여 정보 로그는 씁니다. 예외에 대 한 오류 로그를 만듭니다.
2. "Throw"를 입력 하면 더미 일시적인 오류를 생성 하는 인터셉터 클래스를 만드는 **검색** 상자에서 명명 된 클래스 파일을 만들 *SchoolInterceptorTransientErrors.cs* 는 에서*DAL* 폴더 및 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    재정의이 코드는 `ReaderExecuting` 메서드를 여러 개의 데이터 행을 반환할 수 있는 쿼리에 대 한 호출 됩니다. 재정의 다른 종류의 쿼리에 대 한 연결 복원 력 확인 하려는 경우는 `NonQueryExecuting` 및 `ScalarExecuting` 메서드 로깅 인터셉터로 않습니다.

    학생 페이지를 실행 하 고 검색 문자열과 "Throw"를 입력 하는 경우이 코드는 오류 번호 20, 일반적으로 일시적인 것으로 알려진 형식에 대 한 더미 SQL 데이터베이스 예외를 만듭니다. 현재 임시로 인식 다른 오류 번호는 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501, 및 40613, 아니지만 새 버전의 SQL 데이터베이스에서는 변경 될 수 있습니다.

    코드는 쿼리를 실행 하 고 다시 쿼리 결과 전달 하는 대신 Entity Framework에는 예외를 반환 합니다. 일시적인 예외가 4 번 반환 되 고 다시 코드 돌아갑니다 데이터베이스를 쿼리를 전달 하는 일반적인 절차입니다.

    모든 항목을 기록 하기 때문에 Entity Framework 후 성공 했습니다 4 번 쿼리를 실행 하려고 하 고 응용 프로그램의 유일한 차이점은 쿼리 결과 페이지를 렌더링 하는 데 더 많은 시간이 걸린다는 점을 볼 수 있습니다.

    Entity Framework에서 다시 시도 횟수는 구성할 수 없습니다. SQL 데이터베이스 실행 정책에 대 한 기본값 이기 때문에 코드를 4 번을 지정 합니다. 실행 정책을 변경 하면 했던도 변경에 일시적인 오류가 발생 하는 횟수를 지정 하는 코드를 여기 합니다. 변경할 수도 있습니다. Entity Framework는 발생 하는 자세한 예외를 생성 하는 코드는 `RetryLimitExceededException` 예외입니다.

    검색 상자에 입력 한 값 됩니다 `command.Parameters[0]` 및 `command.Parameters[1]` (하나 메서드 하나에 대 한 첫 번째 이름에 사용 됨). 값 "% Throw %" 발견 되 면 "throw 할" 이러한 매개 변수에서으로 바뀝니다 "an" 된 일부 학생 찾은 반환 됩니다.

    이것이 변경 된 응용 프로그램 UI에 대 한 일부 입력에 기반 하는 연결 복원 력을 테스트 하는 편리한 방법인입니다. 에 대 한 설명의 뒷부분에 설명 된 대로 모든 쿼리 또는 업데이트에 대 한 일시적인 오류를 생성 하는 코드를 작성할 수도 있습니다는 *DbInterception.Add* 메서드.
3. *Global.asax*, 다음 추가 `using` 문:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. 강조 표시 된 줄을 추가 하는 `Application_Start` 메서드:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    이러한 줄의 코드는 어떻게 사용 하면 인터셉터 코드는 Entity Framework 데이터베이스에 쿼리를 보낼 때 실행 되도록 합니다. 일시적인 오류 시뮬레이션에 대 한 별도 인터셉터 클래스를 생성 하 고 로깅, 있습니다에서 다를 수 있으므로 사용 하도록 설정 하 고 사용 하지 않도록 확인 합니다.

    사용 하 여 인터셉터를 추가할 수는 `DbInterception.Add` ; 코드에서 아무 곳 이나 메서드에 있이 필요는 없습니다는 `Application_Start` 메서드. 두 번째 방법은 실행 정책을 구성 하려면 이전에 만든 DbConfiguration 클래스에서이 코드를 삽입 하는 것입니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    아무 곳에 나 넣으면이 코드를 실행 하지 않도록 주의 수 `DbInterception.Add` 동일한 인터셉터에 대 한 한 번은 추가 인터셉터 인스턴스 있게 됩니다. 예를 들어 로깅 인터셉터를 두 번 추가 하는 경우 모든 SQL 쿼리를 위한 두 개의 로그에 표시 됩니다.

    인터셉터 등록 순서 대로 실행 됩니다 (되는 순서는 `DbInterception.Add` 메서드는). 순서는 인터셉터에서 수행 하는 작업에 따라 중요할 수 있습니다. 예를 들어 인터셉터 변경에 강 SQL 명령이 `CommandText` 속성입니다. 이 인해 SQL 명령을 변경, 다음 인터셉터 변경 된 SQL 명령 원래 SQL 명령 받게 됩니다.

    UI에 서로 다른 값을 입력 하 여 일시적인 오류가 발생할 수 있는 방식으로 일시적인 오류 시뮬레이션 코드를 작성 한 합니다. 대신 항상 특정 매개 변수 값을 검사 하지 않고 일시적 예외의 시퀀스를 생성 하는 인터셉터 코드를 작성할 수 있습니다. 그런 다음 일시적인 오류를 생성 하려는 경우에 인터셉터를 추가할 수 있습니다. 그러나이 작업을 수행 하는 경우 추가 하지 마십시오 될 때까지 인터셉터 데이터베이스 초기화가 완료 된 후. 즉, 일시적인 오류 생성을 시작 하기 전에 엔터티 집합 중 하나에 쿼리 등에서 하나 이상의 데이터베이스 작업을 수행 합니다. Entity Framework 데이터베이스 초기화 하는 동안 여러 개의 쿼리를 실행 하 고 초기화 하는 동안 오류 일관성 없는 상태로 가져오려는 컨텍스트 발생할 수와 트랜잭션에서 실행 되지 않습니다.

## <a name="test-logging-and-connection-resiliency"></a>테스트 로깅 및 연결 복원 력

1. F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 한 다음 클릭는 **학생** 탭 합니다.
2. Visual Studio를 살펴보고 **출력** 창 추적 출력을 볼 수 있습니다. 프로그램으로 작성 된 로그에 가져오려는 일부 JavaScript 오류 넘어가면 해야 합니다.

    데이터베이스에 전송 하는 실제 SQL 쿼리를 볼 수 있는지를 확인 합니다. 몇 가지 초기 쿼리 및 시작 하려면가 Entity Framework 데이터베이스 버전을 검사 하는 명령을 한 마이그레이션 기록 테이블 (알아봅니다 마이그레이션에 대 한 다음 자습서의) 표시 됩니다. 개수 학생, 알아보려면 페이징에 대 한 쿼리를 표시 및 학생 데이터를 가져오는 쿼리를 참조 하는 마지막으로.

    ![일반 쿼리에 대 한 로깅](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 에 **학생** 페이지 검색 문자열과 "Throw"를 입력 하 고 클릭 **검색**합니다.

    ![검색 문자열을 throw](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    Entity Framework는 쿼리를 다시 시도 여러 번 하는 동안 몇 초간 지연 브라우저 있다는 것을 확인할 수 있습니다. 첫 번째 다시 시도 오류 발생 매우 신속 하 게 한 다음 각 추가 다시 시도 하기 전에 증가 하기 전에 대기 합니다. 각 다시 시도 호출 하기 전에 더 이상 기다리는이 프로세스 *지 수 백오프*합니다.

    표시 될 때 페이지를 보여 주는 학생을 설치한 "에서" 이름에는 출력 창을 확인을 같은 쿼리에서 처음 4 번 반환 일시적인 다섯 번을 시도 했습니다 예외입니다. 각 일시적인 오류에 대 한 로그에서 일시적인 오류를 생성할 때 작성 하는 표시 됩니다는 `SchoolInterceptorTransientErrors` 클래스 ("Returning 일시적인 오류... 명령에 대 한") 확인할 수 경우 쓸 로그 `SchoolInterceptorLogging` 예외를 가져옵니다.

    ![로깅 출력을 다시 시도 횟수를 표시 합니다.](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    검색 문자열을 입력 한 후 학생 데이터를 반환 하는 쿼리 매개 변수화 됩니다.

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    매개 변수 값을 기록 하지 않는 중인 하지만 수행할 수 있습니다. 매개 변수 값을 확인 하려는에서 매개 변수 값을 가져오는 로깅 코드를 작성할 수 있습니다는 `Parameters` 의 속성은 `DbCommand` 인터셉터 메서드에 얻을 수 있는 개체입니다.

    참고가 응용 프로그램을 중지 하 고 다시 시작 하지 않는 한이 테스트를 반복할 수 없습니다. 오류 카운터를 다시 설정 하는 코드를 작성할 수를 응용 프로그램의 단일 실행 중에 여러 번 연결 복원 력을 테스트 하려는 경우 `SchoolInterceptorTransientErrors`합니다.
4. 차이 보려면 실행 전략 (다시 시도 정책)이 작업을 주석는 `SetExecutionStrategy` 줄 *SchoolConfiguration.cs*, 디버그 모드에서 학생 페이지를 다시 실행 하 고 다시 "Throw"를 검색 합니다.

    이 시간 디버거 중지 첫 번째 생성 된 예외에 처음으로 쿼리를 실행 하려고 할 때에 즉시 합니다.

    ![더미 예외](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. 주석 처리 제거는 *SetExecutionStrategy* 줄 *SchoolConfiguration.cs*합니다.

## <a name="summary"></a>요약

이 자습서에서는 연결 복원 력 및 Entity Framework를 작성 하 고 데이터베이스에 전송 하는 SQL 명령을 기록 하는 방법에 살펴보았습니다. 다음 자습서는 데이터베이스를 배포 하려면 Code First 마이그레이션을 사용 하 여 인터넷에 응용 프로그램을 배포 합니다.

이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[다음](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)
