---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: 연결 복원 력 및 명령 인터 셉 션 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 01/13/2015
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: ab6a553100d704746840eaad512ec140d4576c44
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48911788"
---
<a name="connection-resiliency-and-command-interception-with-the-entity-framework-in-an-aspnet-mvc-application"></a>연결 복원 력 및 명령 인터 셉 션 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.

지금까지 응용 프로그램에서 실행 되었음을 로컬 IIS Express 개발 컴퓨터에 있습니다. 실제 응용 프로그램을 사용 하 여 인터넷을 통해 다른 사람들이 사용할 수 있도록 하려면 웹 호스팅 공급자를 배포 해야 하 고 데이터베이스 서버에 데이터베이스를 배포 해야 합니다.

이 자습서에서는 클라우드 환경에 배포 하는 경우 특히 가치가 있는 Entity Framework 6의 두 가지 기능을 사용 하는 방법을 알아봅니다: 연결 복원 력 (일시적인 오류에 대 한 자동 다시 시도) 및 명령 인터 셉 션 (모든 catch SQL 쿼리 데이터베이스에 전송 로그 또는 변경 하기 위해).

이 연결 복원 력 및 명령 인터 셉 션 자습서는 선택 사항입니다. 이 자습서를 건너뛰면 이후 자습서에서 몇 가지 사소한 측면을 조정 해야 합니다.

## <a name="enable-connection-resiliency"></a>연결 복원 력을 지원합니다

Windows Azure에 응용 프로그램을 배포할 때 Windows Azure SQL Database는 클라우드 데이터베이스 서비스에 데이터베이스 배포. 일시적인 연결 오류는 웹 서버와 데이터베이스 서버에 연결 될 때 직접 함께 동일한 데이터 센터에서 보다 클라우드 데이터베이스 서비스에 연결할 때 일반적으로 더 자주입니다. 클라우드 웹 서버 및 클라우드 데이터베이스 서비스는 동일한 데이터 센터에서 호스트 하는 경우에 연결이 자세한 네트워크 사이 부하 분산 장치와 같은 문제가 발생할 수 있습니다.

또한 클라우드 서비스는 일반적으로 공유 다른 사용자가 해당 응답성 이들에 의해 영향을 받을 수 있습니다. 및 데이터베이스에 대 한 액세스 제한이 적용 될 수 있습니다. 서비스 수준 계약 (SLA)에 허용 된 것 보다 더 많은 것 자주 액세스 하려는 경우 데이터베이스 서비스가 예외를 throw 의미를 제한 합니다.

클라우드 서비스에 액세스 하는 경우 많은 또는 대부분의 연결 문제는 일시적인, 즉, 이러한 자체적으로 해결를 짧은 시간 내에 있습니다. 따라서 데이터베이스 작업을 시도 하는 일반적으로 일시적인 오류의 유형을 가져올 때 잠시 및 작업이 성공할 수 후에 작업을 다시 시도할 수 있습니다. 자동으로 다시 시도 하 여 일시적인 오류를 처리 하는 경우 사용자에 게 훨씬 더 나은 환경을 제공할 수 있습니다 고객에 게 대부분의 숨기기. Entity Framework 6의 연결 복원 력 기능을 다시 시도 프로세스 못했음을 SQL 쿼리를 자동화 합니다.

연결 복원 력 기능은 특정 데이터베이스 서비스를 적절 하 게 구성 해야 합니다.

- 예외는 일시적인 알고 있습니다. 네트워크 연결이 일시적으로 끊김으로 인해 오류 예를 들어 프로그램 버그로 인 한 오류가 아니라 다시 시도 하려고 합니다.
- 이 적절 한 양의 실패 한 작업을 다시 시도 간의 시간을 대기 해야 합니다. 기다릴 수 있습니다 더 이상 일괄 처리에 대해 재시도 간에 보다 온라인 웹 페이지의 사용자 응답 때까지 기다리고 있습니다.
- 이를 적절 한 개수의 포기 하기 전까지 시간을 다시 시도 하세요. 온라인 응용 프로그램에서 사용 하는 일괄 처리에서 여러 번 재시도 수도 있습니다.

Entity Framework 공급자를 지 원하는 데이터베이스 환경에 수동으로 이러한 설정을 구성할 수 있지만 일반적으로 Windows Azure SQL Database를 사용 하는 온라인 응용 프로그램에 대 한 잘 작동 하는 기본 값으로 이미 구성 되어 및 이러한 설정은 Contoso University 응용 프로그램에 대 한 구현 됩니다.

클래스에서 파생 되는 어셈블리에서 만들어져 연결 복원 력을 지원 하기 위해 수행 해야 합니다 [DbConfiguration](https://msdn.microsoft.com/data/jj680699.aspx) 클래스 및 해당 클래스에서 SQL Database를 설정할 *실행 전략*, EF에는 에 대 한 또 다른 용어 *다시 시도 정책*합니다.

1. DAL 폴더에서 라는 클래스 파일을 추가 *SchoolConfiguration.cs*합니다.
2. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    파생 된 클래스에서 찾으면 코드를 자동으로 실행 하는 Entity Framework `DbConfiguration`합니다. 사용할 수는 `DbConfiguration` 클래스에서 그렇지 않은 경우 수행 하는 코드에서 구성 작업을 수행 하는 *Web.config* 파일입니다. 자세한 내용은 [EntityFramework 코드 기반 구성](https://msdn.microsoft.com/data/jj680699)합니다.
3. *StudentController.cs*, 추가 된 `using` 문을 `System.Data.Entity.Infrastructure`.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. 모든 변경 된 `catch` 해당 catch 블록 `DataException` 예외는 catch 되도록 `RetryLimitExceededException` 예외 대신 합니다. 예를 들어:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    사용한 `DataException` 친숙 한 "다시 시도" 메시지를 제공 하기 위해 일시적인 될 수 있는 오류를 식별 하려고 합니다. 반환 된 실제 예외에 래핑됩니다 및 일시적인 오류만는 이미 시도한 되었으며 여러 번 실패 했습니다. 다시 시도 정책에 설정한 했으므로 있지만 `RetryLimitExceededException` 예외입니다.

자세한 내용은 [Entity Framework 연결 복원 력 / 재시도 논리](https://msdn.microsoft.com/data/dn456835)합니다.

## <a name="enable-command-interception"></a>명령 인터 셉 션을 사용 하도록 설정

다시 시도 정책에 설정한 했으므로 테스트 하려면 어떻게 하면 예상 대로 작동 하는지 확인 하려면? 일시적인 오류 발생, 특히를 로컬로 실행 하는 시간과 실제 일시적 오류 자동화 된 단위 테스트를 통합 하기 힘든 것을 강제 적용 하기가 쉽지 않습니다. 연결 복원 력 기능을 테스트 하려면 SQL Server에 전송 하는 Entity Framework는 쿼리를 가로채 고는 일반적으로 일시적인 예외 형식을 사용 하 여 SQL 서버 응답을 대체 하는 방법을 해야 합니다.

클라우드 응용 프로그램에 대 한 모범 사례를 구현 하기 위해 쿼리 인터 셉 션을 사용할 수도 있습니다: [대기 시간 및 성공 또는 실패 외부 서비스에 대 한 모든 호출의 로그](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) 데이터베이스 서비스와 같은 합니다. EF6 제공을 [로깅 API를 전용](https://msdn.microsoft.com/data/dn469464) 로깅을 수행 하는 일을 쉽게 만들 수는 있지만 자습서의이 섹션에서는 Entity Framework를 사용 하는 방법을 알아봅니다 [인터 셉 션 기능](https://msdn.microsoft.com/data/dn469464) 모두 직접 로깅 및 일시적인 오류를 시뮬레이션 합니다.

### <a name="create-a-logging-interface-and-class"></a>로깅 인터페이스 및 클래스 만들기

A [로깅에 대 한 최상의](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) 인터페이스를 사용 하 여 작업을 수행 하는 호출을 System.Diagnostics.Trace 또는 logging 클래스에 하드 코딩 하는 대신 합니다. 쉽게 작업을 수행 해야 하는 경우 나중에 로깅 메커니즘을 변경 합니다. 이 섹션의 로깅 인터페이스와 해당/p를 구현 하는 클래스를 만들 수 >

1. 프로젝트에서 폴더를 만들고 이름을 *로깅*합니다.
2. 에 *로깅* 폴더를 라는 클래스 파일을 만듭니다 *ILogger.cs*, 템플릿 코드를 다음 코드로 바꾸고:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    인터페이스는 로그의 상대적 중요도를 나타내는 3 추적 수준 및 데이터베이스 쿼리와 같은 외부 서비스 호출에 대 한 대기 시간 정보를 제공 하도록 설계 된 것을 제공 합니다. 로깅 메서드 예외에 전달할 수 있는 오버 로드를 포함 합니다. 이 스택 추적 및 내부 예외를 포함 하 여 예외 정보 응용 프로그램 전체에서 각 로깅 메서드 호출에서 수행 되는에 의존 하지 않고 인터페이스를 구현 하는 클래스에 의해 안정적으로 기록 됩니다.

    TraceApi 메서드를 사용 하 여 SQL Database와 같은 외부 서비스를 호출할 때마다의 대기 시간을 추적할 수 있습니다.
3. 에 *로깅* 폴더를 라는 클래스 파일을 만듭니다 *Logger.cs*, 템플릿 코드를 다음 코드로 바꾸고:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    추적을 System.Diagnostics를 사용 하는 구현 합니다. 이 기능은 쉽게 생성 하 고 추적 정보를 사용 하는.NET의 기본 제공 합니다. 많은 "수신기" 예를 들어 파일에 로그가 기록 또는 Azure blob 저장소에 쓸 System.Diagnostics 추적 기능을 사용할 수 있습니다. 일부의 옵션 및 기타 리소스에 대 한 자세한 내용은 링크를 참조 하세요 [Visual Studio에서 Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)합니다. 이 자습서에 살펴봅니다만 Visual Studio에서 로그에 대 한 **출력** 창입니다.

    프로덕션 응용 프로그램의 수도 고려해 야 할 System.Diagnostics 이외의 추적 패키지 및 ILogger 인터페이스를 사용 하면 비교적 쉽게 작업을 수행 하려는 경우 다른 추적 메커니즘을 전환할 수 있습니다.

### <a name="create-interceptor-classes"></a>인터셉터 클래스 만들기

다음 쿼리 로깅 작업을 수행 하는 하나, 데이터베이스 및 일시적인 오류를 시뮬레이트하기 위해 하나를 송신 하려는 때마다에 Entity Framework를 호출 하는 클래스를 만들어야 합니다. 이러한 인터셉터 클래스에서 파생 되어야 합니다는 `DbCommandInterceptor` 클래스입니다. 쿼리 실행 될 때 자동으로 호출 되는 메서드 재정의 작성할 수 있습니다. 이러한 메서드를 검사 하거나 데이터베이스로 전송 되는지 쿼리 로그 및 결과 반환 Entity Framework를 직접도 데이터베이스에 쿼리를 전달 하지 않고 하거나 데이터베이스에 전송 되기 전에 쿼리를 변경할 수 있습니다.

1. 데이터베이스에 전송 되는 모든 SQL 쿼리는 인터셉터 클래스를 만들려면 라는 클래스 파일을 만듭니다 *SchoolInterceptorLogging.cs* 에 *DAL* 폴더 및 템플릿을 사용 하 여 코드 바꾸기 다음 코드는

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    이 코드는 성공적인 쿼리 또는 명령에 대 한 대기 시간 정보를 사용 하 여 정보 로그를 씁니다. 예외에 대 한 오류 로그를 만듭니다.
2. "Throw"를 입력 하는 경우 더미 일시적인 오류를 생성 하는 인터셉터 클래스를 만드는 합니다 **검색** 상자에서 라는 클래스 파일을 만듭니다 *SchoolInterceptorTransientErrors.cs* 합니다 에서*DAL* 폴더 및 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    이 재정의 코드는 `ReaderExecuting` 메서드를 여러 개의 데이터 행을 반환할 수 있는 쿼리에 대 한 호출 되는 합니다. 쿼리의 다른 형식에 대 한 연결 복원 력 확인 하려는 경우 재정의할 수 있습니다도 합니다 `NonQueryExecuting` 및 `ScalarExecuting` 메서드 로깅 인터셉터로 않습니다.

    학생 페이지를 실행 하 고 검색 문자열로 "Throw"를 입력 하는 경우이 코드는 오류 번호 20 이며, 일반적으로 일시적인 것으로 알려진 형식에 대 한 더미 SQL Database 예외를 만듭니다. 현재 인식 일시적으로 다른 오류 번호는 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501, 및 40613, 되지만 이러한 새 버전의 SQL Database는 변경 될 수 있습니다.

    코드는 Entity framework 쿼리를 실행 하 고 다시 쿼리 결과 전달 하는 대신 예외를 반환 합니다. 일시적인 예외 발생을 4 번 반환 되 고 다시 코드 돌아갑니다 데이터베이스에 쿼리를 전달 하는 일반적인 절차입니다.

    모든 항목을 기록 하기 때문에 Entity Framework가 성공 하 고 마지막으로, 이전 쿼리를 4 번 실행 하려고 하며 쿼리 결과 사용 하 여 페이지를 렌더링 하는 데 더는 응용 프로그램의 유일한 차이점은 있는지를 확인 수 있습니다.

    Entity Framework는 다시 시도 횟수를 구성할 수 있습니다. SQL 데이터베이스 실행 정책에 대 한 기본값 이기 때문에 코드를 4 번을 지정 합니다. 실행 정책을 변경 하면 했다면도 변경 코드에 일시적인 오류가 발생 하는 횟수를 지정 하는 합니다. Entity Framework는 throw 할 수 있도록 자세한 예외를 생성 하는 코드를 변경할 수도 있습니다는 `RetryLimitExceededException` 예외입니다.

    검색 상자에 입력 한 값 됩니다 `command.Parameters[0]` 고 `command.Parameters[1]` (하나는 첫 번째 이름과 마지막 이름에 대해 하나씩). 값 "% Throw %" 발견 되 면 "throw 할" 바뀝니다 이러한 매개 변수에서 "an" 학생이 몇 명 발견 되어 반환 될 수 있도록 합니다.

    이것이 응용 프로그램 UI에 대 한 일부 입력 변화에 따라 연결 복원 력 테스트 하는 편리한 방법입니다. 에 대 한 설명의 뒷부분에 설명 된 대로 모든 쿼리 또는 업데이트에 대 한 일시적인 오류를 생성 하는 코드를 작성할 수도 있습니다는 *DbInterception.Add* 메서드.
3. *Global.asax*, 다음 추가 `using` 문:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. 강조 표시 된 줄을 추가 하 여 `Application_Start` 메서드:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    이러한 줄의 코드는 Entity Framework가 데이터베이스에 쿼리를 보낼 때 실행 되도록 인터셉터 코드 원인입니다. 일시적인 오류 시뮬레이션에 대 한 별도 인터셉터 클래스를 생성 하 고 로깅, 독립적으로 활성화 및 비활성화할 수 있습니다 하는 알 수 있습니다.

    사용 하 여 인터셉터를 추가할 수는 `DbInterception.Add` 코드에서 아무 곳 이나 메서드에 있이 필요가 없습니다를 `Application_Start` 메서드. 실행 정책을 구성 하려면 이전에 만든 DbConfiguration 클래스에서이 코드를 배치 하는 방법도 있습니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    아무 곳에 나 넣으면이 코드를 실행 하지 않도록 주의 수 `DbInterception.Add` 동일한 인터셉터에 대 한 추가 인터셉터 인스턴스 얻을 하거나 한 번 이상. 예를 들어 로깅 인터셉터를 두 번 추가 하는 경우 모든 SQL 쿼리를 위한 두 개의 로그 표시 됩니다.

    인터셉터 등록 순서 대로 실행 됩니다 (순서는 `DbInterception.Add` 메서드). 순서는 인터셉터에서 수행 하는 내용에 따라 중요할 수 있습니다. 예를 들어, 인터셉터에 속하는 SQL 명령이 달라질는 `CommandText` 속성입니다. SQL 명령을 변경에 해당 하는 경우 다음 인터셉터는 원래 SQL 명령이 아니라 변경 된 SQL 명령을 받습니다.

    UI에서 다른 값을 입력 하 여 일시적인 오류가 발생할 수 있는 방식으로 일시적인 오류 시뮬레이션 코드를 작성 했습니다. 대신 항상 특정 매개 변수 값을 확인 하지 않고 일시적 예외 시퀀스를 생성 하는 인터셉터 코드를 작성할 수 있습니다. 그런 다음 일시적인 오류를 생성 하려는 경우에 인터셉터를 추가할 수 있습니다. 하지만이 작업을 수행, 추가 하지 마세요까지 인터셉터 데이터베이스 초기화 완료. 일시적인 오류를 생성 하려면 먼저에 즉, 엔터티 집합 하나에 쿼리와 같은 하나 이상의 데이터베이스 작업을 수행 합니다. Entity Framework 데이터베이스 초기화 하는 동안 여러 개의 쿼리를 실행 하 고 초기화 하는 동안 오류가 일관 되지 않은 상태가 가져올 컨텍스트입니다 발생할 수 있습니다 트랜잭션에서 실행 되지 않습니다.

## <a name="test-logging-and-connection-resiliency"></a>테스트 로깅, 연결 복원 력

1. 키를 눌러 **F5** 디버그 모드에서 응용 프로그램을 실행 한 다음 클릭 합니다 **학생** 탭 합니다.
2. Visual Studio 살펴보기 **출력** 창 추적 출력을 확인 합니다. 로 거에 의해 기록 된 로그를 이동 하려면 일부 JavaScript 오류가 구성 스크롤해야 할 수도 있습니다.

    데이터베이스에 전송 되는 실제 SQL 쿼리를 볼 수 있는지 확인 합니다. 일부 초기 쿼리 및 Entity Framework 시작 하는 데이터베이스 버전을 확인 하는 명령 및 마이그레이션 기록 테이블 (배웁니다 마이그레이션에 대 한 다음 자습서에서) 표시 됩니다. 가 얼마나 많은 학생 알아보려면 페이징에 대 한 쿼리를 표시 및 마지막으로 학생 데이터를 가져오는 쿼리를 참조 합니다.

    ![일반 쿼리에 대 한 로깅](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 에 **학생** 페이지에서 검색 문자열 "Throw"를 입력 하 고 클릭 **검색**합니다.

    ![검색 문자열을 throw](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    Entity Framework 다시 시도 하 고 쿼리가 여러 번 하는 동안 몇 초 정도 중단 브라우저 많다고 알 수 있습니다. 첫 번째 재시도 하면 매우 신속 하 게 각 추가 다시 시도 하기 전에 증가 하기 전에 대기 합니다. 각 다시 시도 호출 하기 전에 더 이상 기다리는이 프로세스 *지 수 백오프*합니다.

    표시 되는 경우 페이지를 보여 주는 학생 권한이 "는" 이름에서 출력 창을 확인 하 고 동일한 쿼리는 먼저 4 번 반환 일시적인 다섯 번을 시도 했습니다 보면 예외입니다. 각 일시적인 오류에 대 한 표시에서 일시적인 오류를 생성 하는 경우 작성 하는 로그를 `SchoolInterceptorTransientErrors` 클래스 ("Returning 일시적인 오류... 명령에 대 한") 하는 경우에 기록 된 로그 볼 `SchoolInterceptorLogging` 예외를 가져옵니다.

    ![재시도 보여 주는 로깅 출력](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    검색 문자열을 입력 하면 되므로 학생 데이터를 반환 하는 쿼리 매개 변수화 된:

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    매개 변수의 값을 기록 하지 않는 하 고 있지만 수행할 수 있습니다. 매개 변수 값을 참조 하려는 경우 매개 변수 값을 가져올 로깅 코드를 작성할 수 있습니다는 `Parameters` 의 속성을 `DbCommand` 인터셉터 메서드에서 수행 되는 개체입니다.

    참고 응용 프로그램을 중지 하 고 다시 시작 하지 않는 한이 테스트를 반복할 수 없습니다. 여러 번 실행 하는 단일 응용 프로그램 연결 복원 력을 테스트할 수 하려는 경우에 오류 카운터 다시 설정 하는 코드를 작성할 수 있습니다 `SchoolInterceptorTransientErrors`합니다.
4. 차이 보려면 실행 전략 (다시 시도 정책)가 주석 합니다 `SetExecutionStrategy` 줄 *SchoolConfiguration.cs*, 디버그 모드에서 학생 페이지를 다시 실행 하 고 다시 "Throw"를 검색 합니다.

    이 디버거 중지 생성된 된 첫 번째 예외에서 처음으로 쿼리를 실행 하려고 할 때에 즉시 합니다.

    ![더미 예외](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. 주석 처리를 제거 합니다 *SetExecutionStrategy* 줄 *SchoolConfiguration.cs*합니다.

## <a name="summary"></a>요약

이 자습서에서는 연결 복원 력을 지원 및 Entity Framework를 작성 하 고 데이터베이스를 전송 하는 SQL 명령을 기록 하는 방법을 살펴보았습니다. 다음 자습서에서는 Code First 마이그레이션을 사용 하 여 데이터베이스를 배포 하려면 인터넷에 응용 프로그램 배포.

이 자습서를 연결 하는 방법을 개선할 수 것에 의견을 남겨 주세요.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)
