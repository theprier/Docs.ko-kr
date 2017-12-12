---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: "ASP.NET Web Forms 연결 복원 력 및 명령 인터 셉 션 | Microsoft Docs"
author: Erikre
description: "이 자습서에서는 샘플 응용 프로그램 연결 복원 력 및 명령 인터 셉 션을 지원 하도록 수정 하는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2014
ms.topic: article
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 1c24ccd220bf6df09a958d07b13077f004da0a03
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web Forms 연결 복원 력 및 명령 인터 셉 션
====================
으로 [Erik Reitan](https://github.com/Erikre)

이 자습서에서는 연결 복원 력 및 명령 인터 셉 션을 지원 하도록 Wingtip Toys 샘플 응용 프로그램을 수정 합니다. 연결 복원 력 함으로써 Wingtip Toys 샘플 응용 프로그램 자동으로 다시 데이터 호출 클라우드 환경의 일시적인 오류 발생 시. 또한 명령 인터 셉 션을 구현 하 여 Wingtip Toys 샘플 응용 프로그램은 catch 모든 SQL 쿼리를 로그 하거나 변경 하려면 데이터베이스에 전송 합니다.

> [!NOTE] 
> 
> 이 Web Forms 자습서가 Tom Dykstra 다음 MVC 자습서를 기반으로 합니다.  
> [연결 복원 력 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 인터 셉 션 명령](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)


## <a name="what-youll-learn"></a>학습 내용:

- 연결 복원 력을 제공 하는 방법.
- 명령 인터 셉 션을 구현 하는 방법입니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/en-us/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/en-us/downloads#express-web)합니다. .NET Framework는 자동으로 설치 됩니다.
- Wingtip Toys 샘플 프로젝트를 Wingtip Toys 프로젝트 내에서이 자습서에 언급 된 기능을 구현할 수 있도록 합니다. 다운로드 세부 정보를 제공 하는 다음 링크를 클릭 합니다.

    - [ASP.NET 4.5.1 시작 Web Forms-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) (C#)
- 이 자습서를 완료 하기 전에 검토할 관련된 자습서 시리즈 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다. 자습서 시리즈 익히는 데 도움이 됩니다는 **WingtipToys** 프로젝트 및 코드입니다.

## <a name="connection-resiliency"></a>연결 복원 력

고려해 야 할 한 가지 옵션에 대 한 데이터베이스를 배포 하 고 Windows Azure에 응용 프로그램을 고려할 때 **Windows** **Azure SQL 데이터베이스**, 클라우드 데이터베이스 서비스입니다. 일시적인 연결 오류는 경우 웹 서버와 데이터베이스 서버에 직접 연결 된 함께 동일한 데이터 센터에 클라우드 데이터베이스 서비스에 연결할 때 일반적으로 더 자주 발생 합니다. 클라우드 웹 서버와 클라우드 데이터베이스 서비스는 동일한 데이터 센터에서 호스팅되는, 경우에 연결이 더 많은 네트워크 간 부하 분산 장치와 같은 문제가 발생할 수 있습니다.

또한 클라우드 서비스는 일반적으로 공유 다른 사용자가 응답에 따라 달라질 수 있습니다. 및 데이터베이스에 대 한 액세스 제한을 적용 될 수 있습니다. 의미를 조정 데이터베이스 서비스 예외를 throw에서 허용 하는 것 보다 더 자주 액세스 하려고 할 때 프로그램 *서비스 수준 계약* (SLA).

클라우드 서비스에 액세스할 때 발생 하는 많은 또는 대부분 연결 문제는 일시적인, 즉,은 자체적으로 해결 짧은 기간 동안 합니다. 따라서는 데이터베이스 작업을 시도 하 고 일반적으로 임시 오류 유형의 경우 짧은 대기 및 작업이 성공할 수 후에 작업을 다시 시도할 수 있습니다. 자동으로 다시 시도 하 여 일시적인 오류를 처리 하는 경우 사용자에 대 한 보다 나은 경험을 제공할 수 있습니다 대부분의 고객에 게 보이지 않는 수행 합니다. Entity Framework 6의 연결 복원 기능을 다시 시도 프로세스를 SQL 쿼리 실패 했음을 자동화 합니다.

특정 데이터베이스 서비스에 대 한 연결 복원 기능을 적절히 구성 되어야 합니다.

1. 있기를 알고 있는 예외 일시적인 일 수 있습니다. 네트워크 연결에서 임시 손실로 인해 발생 한 오류 예를 들어 프로그램 버그로 인 한 오류 하지을 다시 시도 하려고 합니다.
2. 후에 적절 한 양의 실패 한 작업의 다시 시도 간격을 대기 합니다. 대기할 수 있습니다 더 이상 일괄 처리에 대 한 재시도 간격 보다 온라인 웹 페이지의 사용자가 응답을 기다리는 여기서는 할 수 있습니다.
3. 후에 적절 한 횟수를 포기 하기 전 다시 시도 합니다. 온라인 응용 프로그램에서 사용 하는 일괄 처리에서 번 더 다시 시도 할 수 있습니다.

Entity Framework 공급자가 지 원하는 모든 데이터베이스 환경에 대해 수동으로 이러한 설정을 구성할 수 있습니다.

연결 복원 력 설정 하기 위해 해야 하는 클래스에서 파생 하는 사용자 어셈블리에서 만들는 `DbConfiguration` 클래스와 해당 클래스에서 Entity Framework에는 다시 시도 정책에 대 한 다른 용어는 SQL 데이터베이스 실행 전략을 설정 합니다.

### <a name="implementing-connection-resiliency"></a>연결 복원 력 구현

1. 다운로드 하 고 엽니다는 [WingtipToys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) 샘플 Visual Studio에서 Web Forms 응용 프로그램입니다.
2. 에 *논리* 의 폴더는 **WingtipToys** 응용 프로그램을 명명 된 클래스 파일 추가 *WingtipToysConfiguration.cs*합니다.
3. 기존 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

파생 된 클래스에서 발견 하는 코드를 자동으로 실행 하는 Entity Framework `DbConfiguration`합니다. 사용할 수는 `DbConfiguration` 그렇지 않은 경우에 수행 하려면 코드에서 구성 작업을 수행 하는 클래스는 *Web.config* 파일입니다. 자세한 내용은 참조 [EntityFramework 코드 기반 구성](https://msdn.microsoft.com/data/jj680699)합니다.

1. 에 *논리* 폴더를 엽니다는 *AddProducts.cs* 파일입니다.
2. 추가 `using` 문을 `System.Data.Entity.Infrastructure` 노란색으로 강조 표시 된 대로:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. 추가 `catch` 블록을 `AddProduct` 메서드 있도록는 `RetryLimitExceededException` 에 강조 표시 된 노란색으로 기록 됩니다.   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

추가 하 여는 `RetryLimitExceededException` 예외를 있습니다 또는 제공할 수 있습니다 더 잘 로깅 프로세스를 다시 시도 하도록 선택할 수 있는 사용자에 게 오류 메시지를 표시 합니다. Catch 하 여는 `RetryLimitExceededException` 예외, 오류만 일시적인 일 수는 이미 시도 되어 여러 번 실패 했습니다. 반환 된 실제 예외에 래핑됩니다는 `RetryLimitExceededException` 예외입니다. 또한 일반 catch 블록도 추가 합니다. 에 대 한 자세한 내용은 `RetryLimitExceededException` 예외를 참조 [Entity Framework 연결 복원 력 / 다시 시도 논리](https://msdn.microsoft.com/en-us/data/dn456835)합니다.

## <a name="command-interception"></a>인터 셉 션 명령

다시 시도 정책에 설정한 했으므로 어떻게 테스트 합니까 예상 대로 작동 하는지 확인? 일시적인 오류가 발생할 것인지, 특히를 로컬로 실행 하는 시점과 자동화 된 단위 테스트에 실제 일시적인 오류를 통합 하 특히 어려울 것 하기가 쉽지 않습니다. 연결 복원 기능을 테스트 하려면 SQL Server에 전송 하는 Entity Framework는 쿼리를 가로채 고 일반적으로 일시적인 예외 형식과 SQL 서버 응답을 대체 하는 방법이 필요 합니다.

클라우드 응용 프로그램에 대 한 모범 사례를 구현 하는 데 쿼리 인터셉터를 사용할 수도 있습니다: 데이터베이스 서비스와 같은 서비스에 외부 호출 대기 시간 및 성공 또는 실패의 모든 로그.

이 섹션의 자습서를 사용 하 여 Entity Framework [ *인터 셉 션 기능* ](https://msdn.microsoft.com/data/dn469464) 로깅 및 일시적인 오류를 시뮬레이션 하는 데 있습니다.

### <a name="create-a-logging-interface-and-class"></a>로깅 인터페이스 및 클래스 만들기

로깅에 대 한 모범 사례를 사용 하 여 작업을 수행 하는 프로그램 [ `interface` ](https://msdn.microsoft.com/library/ms173156.aspx) 에 대 한 호출을 하드 코딩 하는 대신 `System.Diagnostics.Trace` 또는 로깅 클래스입니다. 이렇게 하기 위해 필요한 경우 나중에 로깅 메커니즘을 변경 하려면 쉽게 있습니다. 따라서이 섹션에서는 로깅 인터페이스와 구현 하는 클래스를 만들 수 있습니다.

위의 절차에 따라, 다운로드 하 고 열은 **WingtipToys** 샘플 Visual Studio에서 응용 프로그램입니다.

1. 폴더를 만듭니다는 **WingtipToys** 프로젝트 하 고 이름을 *로깅*합니다.
2. 에 *로깅* 폴더 라는 클래스 파일을 만듭니다 *ILogger.cs* 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

 로그의 상대적 중요도를 나타내는 세 가지 추적 수준 및 데이터베이스 쿼리와 같은 외부 서비스 호출에 대 한 대기 시간 정보를 제공 하도록 지정 된 인터페이스를 제공 합니다. 로깅 메서드 예외에 전달할 수 있는 오버 로드를 갖고 있습니다. 이 응용 프로그램에 걸쳐 각 로깅 메서드 호출에서 수행 되 고에 의존 하지 않고 인터페이스를 구현 하는 클래스에서 스택 추적 및 내부 예외를 포함 하는 예외 정보를 안정적으로 기록 되도록 합니다.  
  
 `TraceApi` 메서드를 사용 하 여 SQL 데이터베이스 같은 외부 서비스를 호출할 때마다 대기 시간을 추적할 수 있습니다.
3. 에 *로깅* 폴더 라는 클래스 파일을 만듭니다 *Logger.cs* 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

구현에서 사용 `System.Diagnostics` 추적 작업을 수행 하 합니다. 이 쉽게 생성 하 고 추적 정보를 사용 하 여.NET의 기본 제공 기능입니다. 여러 &quot;수신기&quot; 함께 사용할 수 있습니다 `System.Diagnostics` 예를 들어 파일에 로그를 쓸 수 또는 Windows azure에서 blob 저장소에 쓸지를 추적 합니다. 참조 하는 일부의 옵션 및 다른 리소스에 대 한 자세한 내용은 링크를 [Visual Studio에서 Windows Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)합니다. 이 자습서에서는 살펴보겠습니다 Visual Studio에서 로그 **출력** 창.

프로덕션 응용 프로그램에서 이외의 추적 프레임 워크를 사용 하는 것이 좋습니다 하려는 `System.Diagnostics`, 및 `ILogger` 인터페이스를 사용 하면 비교적 쉽게 하는 작업을 결정 하는 경우 다른 추적 메커니즘으로 전환할 수 있습니다.

### <a name="create-interceptor-classes"></a>인터셉터 클래스 만들기

다음으로, Entity Framework에는 데이터베이스, 일시적인 오류를 시뮬레이션 하는 각각와 로깅 작업을 수행 하는 쿼리를 보낼 때마다을 호출 하는 클래스에 만들게 됩니다. 이러한 인터셉터 클래스에서 파생 되어야 합니다는 `DbCommandInterceptor` 클래스입니다. 작성 하는 쿼리는 실행 될 때 자동으로 호출 되는 메서드 재정의 합니다. 이러한 메서드에 검사 하거나 데이터베이스로 전송 되는지 쿼리 기록 수 있으며 데이터베이스에 보내기 전에 쿼리를 변경 하거나 결과 반환 Entity Framework를 직접도 데이터베이스에 쿼리를 전달 하지 않고 수 있습니다.

1. 데이터베이스에 전송 하기 전에 모든 SQL 쿼리를 기록 하는 인터셉터 클래스를 만들려면 라는 클래스 파일을 만들 *InterceptorLogging.cs* 에 *논리* 폴더 및 바꾸기 기본 코드는 다음 코드:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

 이 코드는 성공적인 쿼리나 명령에 대 한 대기 시간 정보를 사용 하 여 정보 로그는 씁니다. 예외에 대 한 오류 로그를 만듭니다.
2. 입력할 때 더미 일시적인 오류를 생성 하는 인터셉터 클래스를 만들려면 &quot;Throw&quot; 에 **이름** 라는 페이지에 있는 텍스트 상자 *AdminPage.aspx*, 클래스를 만듭니다 라는 파일 *InterceptorTransientErrors.cs* 에 *논리* 폴더 및 바꾸기 기본 코드를 다음 코드로:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    재정의이 코드는 `ReaderExecuting` 메서드를 여러 개의 데이터 행을 반환할 수 있는 쿼리에 대 한 호출 됩니다. 재정의 다른 종류의 쿼리에 대 한 연결 복원 력 확인 하려는 경우는 `NonQueryExecuting` 및 `ScalarExecuting` 메서드 로깅 인터셉터로 않습니다.  
  
 "관리자" 계정으로 로그인 하 고 선택 됩니다 나중의 **Admin** 위쪽 탐색 모음에서 링크 합니다. 그런 다음는 *AdminPage.aspx* 라는 제품을 추가한 페이지 &quot;Throw&quot;합니다. 코드는 오류 번호 20, 일반적으로 일시적인 것으로 알려진 형식에 대 한 더미 SQL 데이터베이스 예외를 만듭니다. 현재 임시로 인식 다른 오류 번호는 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501, 및 40613, 아니지만 새 버전의 SQL 데이터베이스에서는 변경 될 수 있습니다. 제품의 코드에서 따를 수 있습니다는 "TransientErrorExample"로 바뀝니다는 *InterceptorTransientErrors.cs* 파일입니다.  
  
 코드는 쿼리를 실행 하 고 뒤로 결과 전달 하는 대신 Entity Framework에는 예외를 반환 합니다. 일시적 예외가 반환 됩니다 *4 개의* 시간, 데이터베이스를 쿼리를 전달 하는 일반 프로시저 코드 되돌립니다 다음 합니다.

    모든 항목을 기록 하기 때문에 Entity Framework 후 성공 했습니다 4 번 쿼리를 실행 하려고 하 고 응용 프로그램의 유일한 차이점은 쿼리 결과 페이지를 렌더링 하는 데 더 많은 시간이 걸린다는 점을 볼 수 있습니다.  
  
 Entity Framework에서 다시 시도 횟수는 구성할 수 없습니다. SQL 데이터베이스 실행 정책에 대 한 기본값 이기 때문에 코드를 4 번을 지정 합니다. 실행 정책을 변경 하면 했던도 변경에 일시적인 오류가 발생 하는 횟수를 지정 하는 코드를 여기 합니다. 변경할 수도 있습니다. Entity Framework는 발생 하는 자세한 예외를 생성 하는 코드는 `RetryLimitExceededException` 예외입니다.
3. *Global.asax*, 다음 추가 문을 사용 하 여:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. 다음에 강조 표시 된 줄 추가 `Application_Start` 메서드:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

이러한 줄의 코드는 어떻게 사용 하면 인터셉터 코드는 Entity Framework 데이터베이스에 쿼리를 보낼 때 실행 되도록 합니다. 일시적인 오류 시뮬레이션에 대 한 별도 인터셉터 클래스를 생성 하 고 로깅, 있습니다에서 다를 수 있으므로 사용 하도록 설정 하 고 사용 하지 않도록 확인 합니다.   
  
 사용 하 여 인터셉터를 추가할 수는 `DbInterception.Add` ; 코드에서 아무 곳 이나 메서드에 있이 필요는 없습니다는 `Application_Start` 메서드. 다른 옵션에 대 한 인터셉터를 추가 하지 않은 경우는 `Application_Start` 메서드를 업데이트 하거나 라는 클래스를 추가 하는 것 *WingtipToysConfiguration.cs* 끝의 생성자에 위의 코드를 입력 하 고는 `WingtipToysbConfiguration` 클래스입니다.

아무 곳에 나 넣으면이 코드를 실행 하지 않도록 주의 수 `DbInterception.Add` 동일한 인터셉터에 대 한 한 번은 추가 인터셉터 인스턴스 있게 됩니다. 예를 들어 로깅 인터셉터를 두 번 추가 하는 경우 모든 SQL 쿼리를 위한 두 개의 로그에 표시 됩니다.

인터셉터 등록 순서 대로 실행 됩니다 (되는 순서는 `DbInterception.Add` 메서드는). 순서는 인터셉터에서 수행 하는 작업에 따라 중요할 수 있습니다. 예를 들어 인터셉터 변경에 강 SQL 명령이 `CommandText` 속성입니다. 이 인해 SQL 명령을 변경, 다음 인터셉터 변경 된 SQL 명령 원래 SQL 명령 받게 됩니다.

UI에 서로 다른 값을 입력 하 여 일시적인 오류가 발생할 수 있는 방식으로 일시적인 오류 시뮬레이션 코드를 작성 한 합니다. 대신 항상 특정 매개 변수 값을 검사 하지 않고 일시적 예외의 시퀀스를 생성 하는 인터셉터 코드를 작성할 수 있습니다. 그런 다음 일시적인 오류를 생성 하려는 경우에 인터셉터를 추가할 수 있습니다. 그러나이 작업을 수행 하는 경우 추가 하지 마십시오 될 때까지 인터셉터 데이터베이스 초기화가 완료 된 후. 즉, 일시적인 오류 생성을 시작 하기 전에 엔터티 집합 중 하나에 쿼리 등에서 하나 이상의 데이터베이스 작업을 수행 합니다. Entity Framework 데이터베이스 초기화 하는 동안 여러 개의 쿼리를 실행 하 고 초기화 하는 동안 오류 일관성 없는 상태로 가져오려는 컨텍스트 발생할 수와 트랜잭션에서 실행 되지 않습니다.

## <a name="test-logging-and-connection-resiliency"></a>테스트 로깅 및 연결 복원 력

1. 키를 눌러 Visual Studio에서 **F5** 디버그 모드를 "관리자"의 "Pa$ $단어"를 암호로 사용 하 여 로그인 한 다음 응용 프로그램을 실행 합니다.
2. 선택 **Admin** 위쪽 탐색 모음에서 합니다.
3. 적절 한 설명, 가격 및 이미지 파일과 함께 "Throw" 라는 새 제품을 입력 합니다.
4. 키를 눌러는 **제품 추가** 단추입니다.  
 Entity Framework는 쿼리를 다시 시도 여러 번 하는 동안 몇 초간 지연 브라우저 있다는 것을 확인할 수 있습니다. 첫 번째 다시 시도 매우 빠르게 수행 다음 각 추가 다시 시도 하기 전에 대기 증가 합니다. 각 다시 시도 호출 하기 전에 더 이상 기다리는이 프로세스 *지 수 백오프* 합니다.
5. 페이지는 더 이상 atttempting 로드할 때까지 기다립니다.
6. 프로젝트를 중지 하 고 Visual Studio 확인 **출력** 창 추적 출력을 볼 수 있습니다. 찾을 수 있습니다는 **출력** 창을 선택 하 여 **디버그**  - &gt; **Windows**  - &gt;  **출력**합니다. 이전에 거를 기록한 다른 여러 가지 로그 스크롤해야 할 수도 있습니다.  
  
 데이터베이스에 전송 하는 실제 SQL 쿼리를 볼 수 있는지를 확인 합니다. 표시 초기 쿼리 및 시작 하려면 Entity Framework에서 명령의 몇 가지 데이터베이스 버전 및 마이그레이션 기록 테이블을 확인 합니다.   
    ![출력 창](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
 참고가 응용 프로그램을 중지 하 고 다시 시작 하지 않는 한이 테스트를 반복할 수 없습니다. 오류 카운터를 다시 설정 하는 코드를 작성할 수를 응용 프로그램의 단일 실행 중에 여러 번 연결 복원 력을 테스트 하려는 경우 `InterceptorTransientErrors` 합니다.
7. 차이 보려면 실행 전략 (다시 시도 정책)이 작업을 주석는 `SetExecutionStrategy` 줄 *WingtipToysConfiguration.cs* 파일에 *논리* 실행 폴더는 **관리자**  다시 디버그 모드에서 페이지 및 명명 된 제품 추가 &quot;Throw&quot; 다시 합니다.  
  
 이 시간 디버거 중지 첫 번째 생성 된 예외에 처음으로 쿼리를 실행 하려고 할 때에 즉시 합니다.  
    ![디버깅-자세히 보기](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. 주석 처리 제거는 `SetExecutionStrategy` 줄은 *WingtipToysConfiguration.cs* 파일입니다.

## <a name="summary"></a>요약

이 자습서에서는 연결 복원 력 및 명령 인터 셉 션을 지원 하도록 Web Forms 샘플 응용 프로그램을 수정 하는 방법을 살펴보았습니다.

## <a name="next-steps"></a>다음 단계

연결 복원 력 및 ASP.NET Web Forms의 명령 인터 셉 션을 검토 한 후에 ASP.NET Web Forms 항목 검토 [ASP.NET 4.5의 비동기 메서드](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)합니다. 이 항목에서는 Visual Studio를 사용 하 여 비동기 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 설명 합니다.
