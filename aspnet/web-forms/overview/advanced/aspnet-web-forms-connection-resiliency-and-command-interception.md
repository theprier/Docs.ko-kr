---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: ASP.NET Web Forms 연결 복원 력 및 명령 인터 셉 션 | Microsoft Docs
author: Erikre
description: 이 자습서에서는 연결 복원 력 및 명령 인터 셉 션을 지원 하기 위해 샘플 응용 프로그램을 수정 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 039923a91d957765fa8b2c0cfe11abc8790c1e88
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829488"
---
<a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web Forms 연결 복원 력 및 명령 인터 셉 션
====================
[Erik Reitan](https://github.com/Erikre)

이 자습서에서는 Wingtip Toys 샘플 응용 프로그램 연결 복원 력 및 명령 인터 셉 션을 지원 하도록 수정 합니다. 연결 복원 력을 사용 하 여 Wingtip Toys 샘플 응용 프로그램으로 자동으로 다시 데이터 호출 클라우드 환경의 일반적인 일시적인 오류가 발생 합니다. 또한 명령 인터 셉 션을 구현 하 여 Wingtip Toys 샘플 응용 프로그램은 catch 모든 SQL 쿼리를 기록 하거나 변경 하려면 데이터베이스에 전송 합니다.

> [!NOTE] 
> 
> 이 Web Forms 자습서가 Tom Dykstra 다음 MVC 자습서를 기반으로 합니다.  
> [연결 복원 력 및 명령 인터 셉 션 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)


## <a name="what-youll-learn"></a>학습할 내용:

- 연결 복원 력을 제공 하는 방법입니다.
- 명령 인터 셉 션을 구현 하는 방법입니다.

## <a name="prerequisites"></a>전제 조건

시작 하기 전에 다음 소프트웨어를 컴퓨터에 설치 되어 있는지 확인 합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 나 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다. .NET Framework는 자동으로 설치 됩니다.
- Wingtip Toys 샘플 프로젝트, Wingtip Toys 프로젝트 내에서이 자습서에 언급 된 기능을 구현할 수 있도록 합니다. 다운로드 세부 정보를 제공 하는 다음 링크를 클릭 합니다.

    - [Getting Started with ASP.NET 4.5.1 Web Forms-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) (C#)
- 이 자습서를 완료 하기 전에 검토할 관련된 자습서 시리즈 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다. 자습서 시리즈에서는 익숙해져야 합니다 **WingtipToys** 프로젝트 및 코드입니다.

## <a name="connection-resiliency"></a>연결 복원력

고려해 야 할 한 가지 옵션에 데이터베이스를 배포 하 고 Windows Azure에 응용 프로그램을 고려할 때 **Windows** **Azure SQL Database**, 클라우드 데이터베이스 서비스입니다. 일시적인 연결 오류는 웹 서버와 데이터베이스 서버에 연결 될 때 직접 함께 동일한 데이터 센터에서 보다 클라우드 데이터베이스 서비스에 연결할 때 일반적으로 더 자주입니다. 클라우드 웹 서버 및 클라우드 데이터베이스 서비스는 동일한 데이터 센터에서 호스트 하는 경우에 연결이 자세한 네트워크 사이 부하 분산 장치와 같은 문제가 발생할 수 있습니다.

또한 클라우드 서비스는 일반적으로 공유 다른 사용자가 해당 응답성 이들에 의해 영향을 받을 수 있습니다. 및 데이터베이스에 대 한 액세스 제한이 적용 될 수 있습니다. 의미 제한 데이터베이스 서비스가 예외를 throw에서 허용 된 것 보다 더 자주 액세스 하려고 할 때 사용자 *서비스 수준 계약* (SLA).

클라우드 서비스에 액세스할 때 발생 하는 많은 또는 대부분의 연결 문제는 일시적인, 즉, 이러한 자체적으로 해결를 짧은 시간 내에 있습니다. 따라서 데이터베이스 작업을 시도 하는 일반적으로 일시적인 오류의 유형을 가져올 때 잠시 및 작업이 성공할 수 후에 작업을 다시 시도할 수 있습니다. 자동으로 다시 시도 하 여 일시적인 오류를 처리 하는 경우 사용자에 게 훨씬 더 나은 환경을 제공할 수 있습니다 고객에 게 대부분의 숨기기. Entity Framework 6의 연결 복원 력 기능을 다시 시도 프로세스 못했음을 SQL 쿼리를 자동화 합니다.

연결 복원 력 기능은 특정 데이터베이스 서비스를 적절 하 게 구성 해야 합니다.

1. 예외는 일시적인 알고 있습니다. 네트워크 연결이 일시적으로 끊김으로 인해 오류 예를 들어 프로그램 버그로 인 한 오류가 아니라 다시 시도 하려고 합니다.
2. 이 적절 한 양의 실패 한 작업을 다시 시도 간의 시간을 대기 해야 합니다. 기다릴 수 있습니다 더 이상 일괄 처리에 대해 재시도 간에 보다 온라인 웹 페이지의 사용자 응답 때까지 기다리고 있습니다.
3. 이를 적절 한 개수의 포기 하기 전까지 시간을 다시 시도 하세요. 온라인 응용 프로그램에서 사용 하는 일괄 처리에서 여러 번 재시도 수도 있습니다.

Entity Framework 공급자를 지 원하는 데이터베이스 환경에 수동으로 이러한 설정을 구성할 수 있습니다.

파생 되는 어셈블리의 클래스를 만드는 것 연결 복원 력을 지원 하기 위해 수행 해야 합니다 `DbConfiguration` 클래스 및 해당 클래스에서 Entity Framework에는 다시 시도 정책에 대 한 다른 용어는 SQL 데이터베이스 실행 전략을 설정 합니다.

### <a name="implementing-connection-resiliency"></a>연결 복원 력 구현

1. 다운로드 하 고 엽니다는 [WingtipToys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) 샘플 Visual Studio에서 Web Forms 응용 프로그램입니다.
2. 에 *논리* 폴더를 **WingtipToys** 응용 프로그램을 라는 클래스 파일을 추가 *WingtipToysConfiguration.cs*합니다.
3. 기존 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

파생 된 클래스에서 찾으면 코드를 자동으로 실행 하는 Entity Framework `DbConfiguration`합니다. 사용할 수는 `DbConfiguration` 클래스에서 그렇지 않은 경우 수행 하는 코드에서 구성 작업을 수행 하는 *Web.config* 파일입니다. 자세한 내용은 [EntityFramework 코드 기반 구성](https://msdn.microsoft.com/data/jj680699)합니다.

1. 에 *논리* 폴더를 열고 합니다 *AddProducts.cs* 파일입니다.
2. 추가 된 `using` 방침 `System.Data.Entity.Infrastructure` 노란색으로 강조 표시 된 대로:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. 추가 `catch` 차단 합니다 `AddProduct` 메서드 있도록를 `RetryLimitExceededException` 강조 표시 된 노란색으로 기록 됩니다:   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

추가 하 여는 `RetryLimitExceededException` 예외 로깅 향상을 제공 하거나 프로세스를 다시 시도를 선택할 수 있는 사용자에 게 오류 메시지가 표시 됩니다. Catch 하 여는 `RetryLimitExceededException` 오류만 일시적인 예외는 이미 시도 되었으며 여러 번 실패 했습니다. 반환 된 실제 예외에 래핑됩니다는 `RetryLimitExceededException` 예외입니다. 또한 일반 catch 블록도 추가 합니다. 에 대 한 자세한 내용은 합니다 `RetryLimitExceededException` 예외를 참조 하세요 [Entity Framework 연결 복원 력 / 다시 시도 논리](https://msdn.microsoft.com/data/dn456835)합니다.

## <a name="command-interception"></a>명령 인터 셉 션

다시 시도 정책에 설정한 했으므로 테스트 하려면 어떻게 하면 예상 대로 작동 하는지 확인 하려면? 일시적인 오류 발생, 특히를 로컬로 실행 하는 시간과 실제 일시적 오류 자동화 된 단위 테스트를 통합 하기 힘든 것을 강제 적용 하기가 쉽지 않습니다. 연결 복원 력 기능을 테스트 하려면 SQL Server에 전송 하는 Entity Framework는 쿼리를 가로채 고는 일반적으로 일시적인 예외 형식을 사용 하 여 SQL 서버 응답을 대체 하는 방법을 해야 합니다.

클라우드 응용 프로그램에 대 한 모범 사례를 구현 하기 위해 쿼리 인터 셉 션을 사용할 수도 있습니다: 외부 호출 대기 시간 및 성공 또는 실패의 모든 로그는 데이터베이스 서비스와 같은 서비스입니다.

자습서의이 섹션에서는 Entity Framework [ *인터 셉 션 기능* ](https://msdn.microsoft.com/data/dn469464) 로깅 및 일시적인 오류를 시뮬레이션 하는 것에 대 한 합니다.

### <a name="create-a-logging-interface-and-class"></a>로깅 인터페이스 및 클래스 만들기

로깅에 대 한 모범 사례를 사용 하 여 작업을 수행 하는 것을 [ `interface` ](https://msdn.microsoft.com/library/ms173156.aspx) 에 대 한 호출을 하드 코딩 하는 대신 `System.Diagnostics.Trace` 또는 로깅 클래스입니다. 쉽게 작업을 수행 해야 하는 경우 나중에 로깅 메커니즘을 변경 합니다. 따라서이 섹션에서는 만들어야 로깅 인터페이스 및 클래스를 구현 합니다.

위의 절차에 따라를 다운로드 하 고 열을 **WingtipToys** 샘플 Visual Studio에서 응용 프로그램입니다.

1. 폴더를 만듭니다는 **WingtipToys** 프로젝트 하 고 이름을 *로깅*합니다.
2. 에 *로깅* 폴더를 라는 클래스 파일을 만듭니다 *ILogger.cs* 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   인터페이스는 로그의 상대적 중요도를 나타내는 3 추적 수준 및 데이터베이스 쿼리와 같은 외부 서비스 호출에 대 한 대기 시간 정보를 제공 하도록 설계 된 것을 제공 합니다. 로깅 메서드 예외에 전달할 수 있는 오버 로드를 포함 합니다. 이 스택 추적 및 내부 예외를 포함 하 여 예외 정보 응용 프로그램 전체에서 각 로깅 메서드 호출에서 수행 되는에 의존 하지 않고 인터페이스를 구현 하는 클래스에 의해 안정적으로 기록 됩니다.  
  
   `TraceApi` 메서드를 사용 하면 SQL Database와 같은 외부 서비스를 호출할 때마다의 대기 시간을 추적할 수 있습니다.
3. 에 *로깅* 폴더를 라는 클래스 파일을 만듭니다 *Logger.cs* 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

구현을 사용 하 여 `System.Diagnostics` 추적을 수행 합니다. 이 기능은 쉽게 생성 하 고 추적 정보를 사용 하는.NET의 기본 제공 합니다. 여러 &quot;수신기&quot; 사용할 수 있는 `System.Diagnostics` 예를 들어 파일에 로그가 기록 또는 Windows Azure blob 저장소에 쓸 추적 합니다. 일부의 옵션 및 기타 리소스에 대 한 자세한 내용은 링크를 참조 하세요 [Visual Studio에서 Windows Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)합니다. 이 자습서에서는 Visual Studio에서 로그 찾아만 보겠습니다 **출력** 창입니다.

프로덕션 응용 프로그램에서 이외의 추적 프레임 워크를 사용 하는 것이 좋습니다 하려는 `System.Diagnostics`, 및 `ILogger` 인터페이스를 사용 하면 비교적 쉽게 작업을 수행 하려는 경우 다른 추적 메커니즘을 전환할 수 있습니다.

### <a name="create-interceptor-classes"></a>인터셉터 클래스 만들기

다음으로, 데이터베이스, 일시적인 오류를 시뮬레이트하기 위해 하나 및 로깅 작업을 수행 하는 하나에 쿼리를 전송할 것 때마다에 Entity Framework를 호출 하는 클래스를 만들어야 합니다. 이러한 인터셉터 클래스에서 파생 되어야 합니다는 `DbCommandInterceptor` 클래스입니다. 에 쿼리가 실행 될 때 자동으로 호출 되는 메서드 재정의 작성할 수 있습니다. 이러한 메서드를 검사 하거나 데이터베이스로 전송 되는지 쿼리 로그 및 결과 반환 Entity Framework를 직접도 데이터베이스에 쿼리를 전달 하지 않고 하거나 데이터베이스에 전송 되기 전에 쿼리를 변경할 수 있습니다.

1. 데이터베이스에 전송 되기 전에 모든 SQL 쿼리를 기록 하는 인터셉터 클래스를 만들려면 라는 클래스 파일을 만듭니다 *InterceptorLogging.cs* 에 *논리* 폴더 및 바꾸기 기본 코드를 코드를 다음과 같습니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   이 코드는 성공적인 쿼리 또는 명령에 대 한 대기 시간 정보를 사용 하 여 정보 로그를 씁니다. 예외에 대 한 오류 로그를 만듭니다.
2. 입력할 때 더미 일시적인 오류를 생성 하는 인터셉터 클래스를 만들려면 &quot;Throw&quot; 에 **이름** 라는 페이지에서 텍스트 상자 *AdminPage.aspx*, 클래스를 만듭니다 파일인 *InterceptorTransientErrors.cs* 에 *논리* 폴더 및 대체 기본 코드를 다음 코드로:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    이 재정의 코드는 `ReaderExecuting` 메서드를 여러 개의 데이터 행을 반환할 수 있는 쿼리에 대 한 호출 되는 합니다. 쿼리의 다른 형식에 대 한 연결 복원 력 확인 하려는 경우 재정의할 수 있습니다도 합니다 `NonQueryExecuting` 및 `ScalarExecuting` 메서드 로깅 인터셉터로 않습니다.  
  
   "관리자" 계정으로 로그인 하 고 선택 됩니다 나중에 **관리자** 위쪽 탐색 모음에서 연결 합니다. 그런 다음 합니다 *AdminPage.aspx* 페이지 라는 제품을 추가한 &quot;Throw&quot;합니다. 코드는 오류 번호 20 이며, 일반적으로 일시적인 것으로 알려진 형식에 대 한 더미 SQL Database 예외를 만듭니다. 현재 인식 일시적으로 다른 오류 번호는 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501, 및 40613, 되지만 이러한 새 버전의 SQL Database는 변경 될 수 있습니다. 제품 코드에 따르면는 "TransientErrorExample"으로 바뀝니다 합니다 *InterceptorTransientErrors.cs* 파일입니다.  
  
   코드는 Entity framework 쿼리를 실행 하 고 결과 다시 전달 하는 대신 예외를 반환 합니다. 일시적 예외가 반환 됩니다 *4 개의* 번 데이터베이스에 쿼리를 전달 하는 일반적인 프로시저 코드 되돌립니다 다음입니다.

    모든 항목을 기록 하기 때문에 Entity Framework가 성공 하 고 마지막으로, 이전 쿼리를 4 번 실행 하려고 하며 쿼리 결과 사용 하 여 페이지를 렌더링 하는 데 더는 응용 프로그램의 유일한 차이점은 있는지를 확인 수 있습니다.  
  
   Entity Framework는 다시 시도 횟수를 구성할 수 있습니다. SQL 데이터베이스 실행 정책에 대 한 기본값 이기 때문에 코드를 4 번을 지정 합니다. 실행 정책을 변경 하면 했다면도 변경 코드에 일시적인 오류가 발생 하는 횟수를 지정 하는 합니다. Entity Framework는 throw 할 수 있도록 자세한 예외를 생성 하는 코드를 변경할 수도 있습니다는 `RetryLimitExceededException` 예외입니다.
3. *Global.asax*, 다음 추가 문을 사용 하 여:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. 그런 다음 강조 표시 된 줄을 추가 합니다 `Application_Start` 메서드:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

이러한 줄의 코드는 Entity Framework가 데이터베이스에 쿼리를 보낼 때 실행 되도록 인터셉터 코드 원인입니다. 일시적인 오류 시뮬레이션에 대 한 별도 인터셉터 클래스를 생성 하 고 로깅, 독립적으로 활성화 및 비활성화할 수 있습니다 하는 알 수 있습니다.   
  
 사용 하 여 인터셉터를 추가할 수는 `DbInterception.Add` 코드에서 아무 곳 이나 메서드에 있이 필요가 없습니다를 `Application_Start` 메서드. 또 다른 옵션에 대 한 인터셉터를 추가 하지 않은 경우는 `Application_Start` 메서드를 업데이트 하거나 라는 클래스를 추가 하는 것 *WingtipToysConfiguration.cs* 끝의 생성자에 위의 코드는 `WingtipToysbConfiguration` 클래스입니다.

아무 곳에 나 넣으면이 코드를 실행 하지 않도록 주의 수 `DbInterception.Add` 동일한 인터셉터에 대 한 추가 인터셉터 인스턴스 얻을 하거나 한 번 이상. 예를 들어 로깅 인터셉터를 두 번 추가 하는 경우 모든 SQL 쿼리를 위한 두 개의 로그 표시 됩니다.

인터셉터 등록 순서 대로 실행 됩니다 (순서는 `DbInterception.Add` 메서드). 순서는 인터셉터에서 수행 하는 내용에 따라 중요할 수 있습니다. 예를 들어, 인터셉터에 속하는 SQL 명령이 달라질는 `CommandText` 속성입니다. SQL 명령을 변경에 해당 하는 경우 다음 인터셉터는 원래 SQL 명령이 아니라 변경 된 SQL 명령을 받습니다.

UI에서 다른 값을 입력 하 여 일시적인 오류가 발생할 수 있는 방식으로 일시적인 오류 시뮬레이션 코드를 작성 했습니다. 대신 항상 특정 매개 변수 값을 확인 하지 않고 일시적 예외 시퀀스를 생성 하는 인터셉터 코드를 작성할 수 있습니다. 그런 다음 일시적인 오류를 생성 하려는 경우에 인터셉터를 추가할 수 있습니다. 하지만이 작업을 수행, 추가 하지 마세요까지 인터셉터 데이터베이스 초기화 완료. 일시적인 오류를 생성 하려면 먼저에 즉, 엔터티 집합 하나에 쿼리와 같은 하나 이상의 데이터베이스 작업을 수행 합니다. Entity Framework 데이터베이스 초기화 하는 동안 여러 개의 쿼리를 실행 하 고 초기화 하는 동안 오류가 일관 되지 않은 상태가 가져올 컨텍스트입니다 발생할 수 있습니다 트랜잭션에서 실행 되지 않습니다.

## <a name="test-logging-and-connection-resiliency"></a>테스트 로깅, 연결 복원 력

1. Visual Studio에서 눌러 **F5** 디버그 모드 "관리자"의 "Pa$ $단어"를 사용 하 여 암호로 로그인 한 다음 응용 프로그램을 실행 합니다.
2. 선택 **관리자** 맨 위에 있는 탐색 모음에서.
3. 적절 한 설명, 가격 및 이미지 파일을 사용 하 여 "Throw" 라는 새 제품을 입력 합니다.
4. 키를 눌러 합니다 **제품 추가** 단추입니다.  
   Entity Framework 다시 시도 하 고 쿼리가 여러 번 하는 동안 몇 초 정도 중단 브라우저 많다고 알 수 있습니다. 첫 번째 재시도 매우 신속 하 게 발생 한 다음 각 추가 다시 시도 하기 전에 대기 증가 합니다. 각 다시 시도 호출 하기 전에 더 이상 기다리는이 프로세스 *지 수 백오프* 합니다.
5. 페이지는 더 이상 atttempting 로드할 때까지 기다립니다.
6. 프로젝트를 중지 하 고 Visual Studio 살펴보기 **출력** 창 추적 출력을 확인 합니다. 찾을 수 있습니다 합니다 **출력** 를 선택 하 여 창 **디버그**  - &gt; **Windows**  - &gt;  **출력**합니다. 이전에 거를 기록한 다른 여러 로그 스크롤해야 할 수도 있습니다.  
  
   데이터베이스에 전송 되는 실제 SQL 쿼리를 볼 수 있는지 확인 합니다. 표시 몇 가지 초기 쿼리 및 명령을 시작 하려면 Entity Framework는 데이터베이스 버전 및 마이그레이션 기록 테이블을 확인 합니다.   
    ![출력 창](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   참고 응용 프로그램을 중지 하 고 다시 시작 하지 않는 한이 테스트를 반복할 수 없습니다. 여러 번 실행 하는 단일 응용 프로그램 연결 복원 력을 테스트할 수 하려는 경우에 오류 카운터 다시 설정 하는 코드를 작성할 수 있습니다 `InterceptorTransientErrors` 합니다.
7. 차이 보려면 실행 전략 (다시 시도 정책)가 주석를 `SetExecutionStrategy` 줄 *WingtipToysConfiguration.cs* 파일을 *논리* 폴더에서 실행 하는 **관리자**  라는 제품을 추가한 페이지 디버그 모드에서 다시 &quot;Throw&quot; 다시 합니다.  
  
   이 디버거 중지 생성된 된 첫 번째 예외에서 처음으로 쿼리를 실행 하려고 할 때에 즉시 합니다.  
    ![디버깅-자세히 보기](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. 주석 처리를 제거 합니다 `SetExecutionStrategy` 줄을 *WingtipToysConfiguration.cs* 파일입니다.

## <a name="summary"></a>요약

이 자습서에서는 연결 복원 력 및 명령 인터 셉 션을 지원 하기 위해 Web Forms 샘플 응용 프로그램을 수정 하는 방법을 살펴보았습니다.

## <a name="next-steps"></a>다음 단계

연결 복원 력 및 명령 인터 셉 션 ASP.NET Web Forms에서 살펴본 후 ASP.NET Web Forms 항목을 검토 [ASP.NET 4.5의 비동기 메서드](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)합니다. 항목은 Visual Studio를 사용 하 여 비동기 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
