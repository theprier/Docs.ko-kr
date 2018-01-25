---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: "구성 및 계측 | Microsoft Docs"
author: microsoft
description: "구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API 구성 변경 하려면 프로젝트를 만들 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 5780bfde928011f46c3f504aec927f2127f10d0d
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="configuration-and-instrumentation"></a>구성 및 계측
====================
by [Microsoft](https://github.com/microsoft)

> 구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API 구성 변경 내용을 프로그래밍 방식으로 만들 수 있습니다. 또한 다양 한 새 구성 설정을 존재 새 구성 및 계측을 허용 합니다.


구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API 구성 변경 내용을 프로그래밍 방식으로 만들 수 있습니다. 또한 다양 한 새 구성 설정을 존재 새 구성 및 계측을 허용 합니다.

이 단원에서는 다음과 같은 작용이 ASP.NET 구성 API에서 읽기 및 ASP.NET 구성 파일에 쓰는 관련 하 고 ASP.NET 계측도 설명 합니다. 또한 ASP.NET 추적에서 사용할 수 있는 새로운 기능을 설명 합니다.

## <a name="aspnet-configuration-api"></a>ASP.NET 구성 API

ASP.NET 구성 API를 사용 하면 개발, 배포 및 단일 프로그래밍 인터페이스를 사용 하 여 응용 프로그램 구성 데이터를 관리할 수 있습니다. 구성 API를 사용 하 여 개발 하 고 구성 파일에서 XML을 직접 편집 하지 않고도 ASP.NET 구성을 완료를 프로그래밍 방식으로 수정할 수 있습니다. 또한 콘솔 응용 프로그램 및 개발 하는 스크립트에서 웹 기반 관리 도구 및 스냅인 콘솔 MMC (Microsoft Management) 구성 API를 사용할 수 있습니다.

구성 API를 사용 하 고.NET Framework 버전 2.0에 포함 된 다음 두 가지 구성 관리 도구:

- 구성 API를 사용 하 여 관리 작업을 간소화를 ASP.NET MMC 스냅인 종합적 구성 계층 구조의 모든 수준에서 로컬 구성 데이터를 제공 합니다.
- 에 로컬 및 원격 응용 프로그램에 대 한 구성 설정을 관리할 수 있도록 하는 웹 사이트 관리 도구 등의 호스팅된 사이트입니다.

ASP.NET 구성 API 웹 사이트 및 응용 프로그램을 프로그래밍 방식으로 구성 하는 데 사용할 수 있는 ASP.NET 관리 개체의 집합을 구성 합니다. 관리 개체는.NET Framework 클래스 라이브러리로 구현 됩니다. 구성 API 프로그래밍 모델에 컴파일 타임에 데이터 형식을 적용 하 여 코드 일관성과 안정성을 보장 하는 데 도움이 됩니다. 쉽게 응용 프로그램 구성 관리 구성 API 구성 계층의 모든 지점에서 서로 다른 별도 컬렉션으로 데이터를 보고 하는 대신 하나의 컬렉션으로 병합 되는 데이터를 볼 수 있습니다. 구성 파일입니다. 또한 구성 API를 사용 하는 구성 파일에서 XML을 직접 편집 하지 않고도 전체 응용 프로그램 구성을 조작할 수 있습니다. 마지막으로, API 웹 사이트 관리 도구 등 관리 도구를 지원 하 여 구성 작업을 간소화 합니다. 구성 API는 컴퓨터에서 구성 파일을 만들고 여러 컴퓨터에서 구성 스크립트를 실행 하 여 배포를 간소화 합니다.

> [!NOTE]
> 구성 API는 IIS 응용 프로그램 만들기를 지원 하지 않습니다.


## <a name="working-with-local-and-remote-configuration-settings"></a>로컬 및 원격 구성 설정 작업

구성 개체를 사용 하는 컴퓨터와 같은 특정 물리적 엔터티 또는 응용 프로그램 또는 웹 사이트 등의 논리 엔터티에 적용 되는 구성 설정의 병합 된 보기를 나타냅니다. 지정된 된 논리 엔터티 원격 서버에서 로컬 컴퓨터에 있을 수 있습니다. 지정된 엔터티에 대 한 구성 파일이 있는 경우 Machine.config 파일에 정의 된 대로 구성 개체의 기본 구성 설정을 나타냅니다.

다음 클래스에서 열린 구성 방법 중 하나를 사용 하 여 구성 개체를 가져올 수 있습니다.

1. 엔터티 클라이언트 응용 프로그램이 면 ConfigurationManager 클래스입니다.
2. 엔터티 웹 응용 프로그램인 경우 WebConfigurationManager 클래스입니다.

이러한 메서드는에 필요한 메서드 및 기본 구성 파일을 처리 하는 속성을 제공 하는 구성 개체를 반환 됩니다. 이러한 파일을 읽거나 쓰기 위해 액세스할 수 있습니다.

### <a name="reading"></a>읽기

GetSection 또는 GetSectionGroup 메서드를 사용 하 여 구성 정보를 읽습니다. 사용자 또는 프로세스를 읽는 모든 계층의 구성 파일에 대 한 권한이 읽기 있어야 합니다.

> [!NOTE]
> Path 매개 변수를 사용 하는 정적 GetSection 메서드를 사용 하는 경우 path 매개 변수는 해당 코드가 실행 중인 응용 프로그램 참조 해야 합니다. 그렇지 않으면 매개 변수가 무시 되 고 현재 실행 중인 응용 프로그램에 대 한 구성 정보가 반환 됩니다.


### <a name="writing"></a>쓰기

구성 정보를 작성 하는 저장 메서드 중 하나를 사용 합니다. 사용자 또는 쓰기에 있어야 하는 프로세스 구성 파일 및 디렉터리 현재 구성 계층 구조 수준에 대 한 쓰기 권한과으로 모든 계층의 구성 파일에 읽기 권한.

지정된 된 엔터티에 대 한 상속 된 구성 설정을 나타내는 구성 파일을 생성 하려면 다음 구성 저장 방법 중 하나를 사용 합니다.

1. 새 구성 파일을 만들 Save 메서드.
2. SaveAs 메서드 다른 위치에 새 구성 파일을 생성 합니다.

## <a name="configuration-classes-and-namespaces"></a>클래스와 네임 스페이스

여러 구성 클래스 및 메서드는 서로 비슷합니다. 다음 표에서 가장 일반적으로 사용 되는 클래스와 네임 스페이스를 설명합니다.

| **구성 클래스 또는 네임 스페이스** | **설명** |
| --- | --- |
| [System.Configuration](https://msdn.microsoft.com/library/system.configuration.aspx) 네임 스페이스 | 모든.NET Framework 응용 프로그램에 대 한 주요 구성 클래스가 포함 됩니다. 섹션 처리기 클래스 GetSection GetSectionGroup 등의 방법 중에서 섹션에 대 한 구성 데이터를 가져오는 데 사용 됩니다. 이 두 메서드는 static이 아닌 합니다. |
| System.Configuration.Configuration 클래스 | 컴퓨터, 응용 프로그램, 웹 디렉터리 또는 다른 리소스에 대 한 구성 데이터의 집합을 나타냅니다. 이 클래스에는 유용한 메서드, 예: GetSection 및 GetSectionGroup, 구성 설정을 업데이트 하 고 섹션 및 섹션 그룹에 대 한 참조를 얻기에 대 한 포함 합니다. 이 클래스는 WebConfigurationManager 및 ConfigurationManager 클래스의 메서드와 같은 디자인 타임 구성 데이터를 가져오는 방법에 대 한 반환 형식으로 사용 됩니다. |
| System.Web.Configuration 네임 스페이스 | ASP.NET 구성 섹션에 정의 된 섹션 처리기 클래스를 포함 [ASP.NET 구성 설정](https://msdn.microsoft.com/library/b5ysx397.aspx)합니다. 섹션 처리기 클래스 GetSection GetSectionGroup 등의 방법 중에서 섹션에 대 한 구성 데이터를 가져오는 데 사용 됩니다. |
| System.Web.Configuration.WebConfigurationManager class | 런타임 및 디자인 타임 구성 설정에 대 한 참조를 가져오기 위한 유용한 메서드를 제공 합니다. 이러한 메서드는 반환 형식으로 System.Configuration.Configuration 클래스를 사용합니다. 이 클래스의 정적 GetSection 메서드 또는 System.Configuration.ConfigurationManager 클래스의 비정적 GetSection 메서드 같은 의미로 사용할 수 있습니다. 웹 응용 프로그램 구성에 대 한 System.Web.Configuration.WebConfigurationManager 클래스 System.Configuration.ConfigurationManager 클래스 대신이 좋습니다. |
| [System.Configuration.Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx) namespace | 사용자 지정 하 고 구성 공급자를 확장 하는 방법을 제공 합니다. 구성 시스템에 모든 공급자 클래스에 대 한 기본 클래스입니다. |
| [System.Web.Management](https://msdn.microsoft.com/library/system.web.management.aspx) namespace | 클래스와 웹 응용 프로그램의 상태를 모니터링 및 관리 하기 위한 인터페이스를 포함 합니다. 엄밀히 말해이 네임 스페이스 구성 API의 일부로 간주 되지 않습니다. 예를 들어 추적 및 이벤트 발생이 네임 스페이스의 클래스에 의해 수행 됩니다. |
| [System.Management.Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) 네임 스페이스 | 관리 정보 및 잠재 고객에 게 Windows Management Instrumentation (WMI)를 통해 이벤트를 노출 하는 응용 프로그램의 계측에 필요한 클래스를 제공 합니다. ASP.NET 상태 모니터링는 WMI 이벤트를 제공할 수 있습니다. 엄밀히 말해이 네임 스페이스 구성 API의 일부로 간주 되지 않습니다. |

## <a name="reading-from-aspnet-configuration-files"></a>ASP.NET 구성 파일에서 읽기

WebConfigurationManager 클래스는 ASP.NET 구성 파일에서 읽는 데 필요한 핵심 클래스입니다. 기본적으로 다음 세 단계로 ASP.NET 구성 파일을 읽는 가지가 있습니다.

1. OpenWebConfiguration 메서드를 사용 하 여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대 한 참조를 가져옵니다.
3. 구성 파일에서 원하는 정보를 읽습니다.

개체가 나타내는 구성 특정 구성 파일을 나타내지 않습니다. 대신, 컴퓨터, 응용 프로그램 또는 웹 사이트의 구성에 병합된 된 뷰를 나타냅니다. 다음 코드 샘플 이라는 웹 응용 프로그램의 구성을 나타내는 구성 개체를 인스턴스화하고 *ProductInfo*합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> Note는 /ProductInfo 경로가 존재 하지 않는 경우는 위의 코드는 반환 지정 된 대로 기본 구성 machine.config 파일에 있습니다.


구성 개체를 만든 후에 다음 구성 설정으로 드릴 GetSection 또는 GetSectionGroup 메서드를 사용할 수 있습니다. 다음 예제에서는 위의 ProductInfo 응용 프로그램에 대 한 가장 설정에 대 한 참조를 가져옵니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>ASP.NET 구성 파일에 쓰기

구성 파일에서 읽기를 마찬가지로 WebConfigurationManager 클래스에는 Asp.NET 구성 파일에 쓰기 위한 핵심입니다. ASP.NET 구성 파일을 작성 하는 세 가지 단계가 있습니다.

1. OpenWebConfiguration 메서드를 사용 하 여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대 한 참조를 가져옵니다.
3. 저장 또는 다른 이름으로 저장을 사용 하 여 구성 파일에서 원하는 정보를 쓸 메서드.

다음 코드 변경 내용과 **디버그** 특성에는 &lt;컴파일&gt; false로 요소:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

이 코드를 실행 하는 경우는 **디버그** 특성에는 &lt;컴파일&gt; 요소에 대해 false로 설정 됩니다는 *webApp* 응용 프로그램의 web.config 파일입니다.

## <a name="systemwebmanagement-namespace"></a>System.Web.Management Namespace

System.Web.Management 네임 스페이스의 클래스 및 ASP.NET 응용 프로그램의 상태를 모니터링 및 관리 하기 위한 인터페이스를 제공 합니다.

로깅은 이벤트 공급자와 연결 하는 규칙을 정의 하 여 수행 됩니다. 규칙에는 공급자에 게 전송 하는 이벤트의 형식을 정의 합니다. 다음 기본 이벤트를 기록할 수 있습니다.

| **WebBaseEvent** | 모든 이벤트에 대 한 기본 이벤트 클래스입니다. 필수 포함 이벤트 코드, 이벤트 정보 코드, 날짜 및 시간 이벤트가 발생 하는 등 모든 이벤트에 대 한 속성 시퀀스 번호, 이벤트 메시지 및 이벤트 정보입니다. |
| --- | --- |
| **WebManagementEvent** | 응용 프로그램 수명, 요청, 오류 및 이벤트 감사 등의 관리 이벤트에 대 한 기본 이벤트 클래스. |
| **WebHeartbeatEvent** | 유용한 런타임 상태 정보를 캡처할 규칙적인 간격으로 응용 프로그램에 의해 생성 된 이벤트입니다. |
| **WebAuditEvent** | 권한 부여 실패, 암호 해독 오류 등의 상황을 표시 하는 데 사용 되는 보안 감사 이벤트에 대 한 기본 클래스 *등입니다.* |
| **WebRequestEvent** | 모든 정보 요청 이벤트에 대 한 기본 클래스입니다. |
| **WebBaseErrorEvent** | 오류 상태를 나타내는 모든 이벤트에 대 한 기본 클래스입니다. |

사용할 수 있는 공급자 종류를 사용 하면 이벤트 출력 이벤트 뷰어, SQL Server, Windows Management Instrumentation (WMI) 및 전자 메일을 보낼 수 있도록 합니다. 미리 구성 된 공급자 및 이벤트 매핑 이벤트 출력을 기록 하는 데 필요한 작업 양을 줄입니다.

ASP.NET 2.0 시작 및 중지,으로 처리 되지 않은 예외 로깅 응용 프로그램 도메인을 기준으로 이벤트를 기록 하는 이벤트 로그 공급자의 the-기본적으로 사용 합니다. 이렇게 하면 기본 시나리오 중 일부를 다룬 것입니다. 예를 들어 응용 프로그램 예외를 throw 하지만 사용자 오류를 저장 하지는 않습니다를 재현할 수 없는 가정해 봅니다. 기본 이벤트 로그 규칙으로 알아둡니다 어떤 종류의 오류가 발생 한 예외 및 스택 정보를 수집할 수는 합니다. 또 다른 예에는 응용 프로그램은 세션 상태를 유지 하는 경우 적용 됩니다. 이 경우 응용 프로그램 도메인이 재활용 되 고 응용 프로그램 도메인을 멈춘 이유에 처음에 있는지 여부를 확인 하려면 이벤트 로그에서 볼 수 있습니다.

또한 상태 모니터링 시스템은 확장 가능 합니다. 예를 들어 사용자 지정 웹 이벤트를 정의 하 고, 응용 프로그램 내에서 발생 하도록 하 고, 다음 전자 메일 등 공급자에 이벤트 정보를 전송할 규칙을 정의할 수 있습니다. 이 상태 공급자를 모니터링 하 여 계측을 쉽게 연결할 수 있습니다. 또 다른 예로, 주문 처리 되 고 SQL Server 데이터베이스에 각 이벤트를 전송 하는 규칙을 설정할 때마다 이벤트를 발생 수 있습니다. 또한 사용자가 행을 여러 번 로그온 하 고 전자 메일 기반 공급자를 사용 하도록 이벤트를 설정 하지 못하면 이벤트를 발생 수 없습니다.

기본 공급자 및 이벤트에 대 한 구성은 전역 Web.config 파일에 저장 됩니다. 전역 Web.config 파일에서 ASP.NET 1 Machine.config 파일에 저장 된 모든 웹 기반 설정을 저장 x. 전역 Web.config 파일은 다음 디렉터리에 있습니다.

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

&lt;healthMonitoring&gt; 전역 Web.config 파일의 기본 구성 설정을 제공 합니다. 이러한 설정은 재정의 하거나 구현 하 여 자신만 설정을 구성할 수 있습니다는 &lt;healthMonitoring&gt; 응용 프로그램에 대 한 Web.config 파일의 섹션입니다.

&lt;healthMonitoring&gt; 전역 Web.config 파일의 섹션에는 다음과 같은 항목이 있습니다.

| **providers** | 이벤트 뷰어, WMI 및 SQL Server에 대 한 설정 공급자를 포함 합니다. |
| --- | --- |
| **eventMappings** | 다양 한 WebBase 클래스에 대 한 매핑을 포함합니다. 이벤트 클래스를 직접 생성 하는 경우이 목록을 확장할 수 있습니다. 이벤트 클래스를 직접 생성 하면 보다 세부적인 정보를 보낼 공급자를 통해. 예를 들어 전자 메일에 사용자 지정 이벤트를 전송 하는 동안 SQL 서버로 보낼 처리 되지 않은 예외를 구성할 수 있습니다. |
| **rules** | EventMappings 공급자에 연결 되어 있습니다. |
| **buffering** | SQL Server 및 전자 메일 공급자와 함께 공급자에 이벤트를 플러시하는 빈도 결정 하는 데 사용 합니다. |

다음은 전역 Web.config 파일에서 코드 예제입니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>이벤트를 이벤트 뷰어에 저장 하는 방법

이벤트 로깅에 대 한 공급자 앞에서 설명한 것 처럼 이벤트 뷰어는 구성 전역 Web.config 파일에. 기본적으로 모든 이벤트에 따라 **WebBaseErrorEvent** 및 **WebFailureAuditEvent** 기록 됩니다. 이벤트 로그에 추가 정보를 기록 하는 추가 규칙을 추가할 수 있습니다. 예를 들어, 모든 이벤트를 기록 하려는 경우 (*즉,*, 모든 이벤트에 따라 **WebBaseEvent**), Web.config 파일에 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

이 규칙에서 링크 하려는 **모든 이벤트** 이벤트 로그 공급자에 이벤트 매핑됩니다. EventMapping 및 공급자를 둘 다 글로벌 Web.config 파일에 포함 됩니다.

## <a name="how-to-store-events-to-sql-server"></a>SQL Server에 대 한 이벤트를 저장 하는 방법

이 메서드는 사용 된 **ASPNETDB** Aspnet에서 생성 된 데이터베이스\_regsql.exe 도구입니다. 기본 공급자 중 하나는 파일 기반 데이터베이스 응용 프로그램에서 사용 하 여 LocalSqlServer 연결 문자열을 사용 하 여\_데이터 폴더 또는 SQL Server의 로컬 SQLExpress 인스턴스에 있습니다. LocalSqlServer 연결 문자열과 SqlProvider 둘 다 글로벌 Web.config 파일에서 구성 됩니다.

전역 Web.config 파일에서 LocalSqlServer 연결 문자열은 다음과 같습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Aspnet 사용 해야 다른 SQL Server 인스턴스를 사용 하려는 경우\_%windir%\Microsoft.Net\Framework\v2.0 찾을 수 있는 regsql.exe 도구\* 폴더입니다. Aspnet를 사용 하 여\_regsql.exe 도구를 사용자 지정 생성 **ASPNETDB** SQL Server 인스턴스에 데이터베이스 연결 문자열에 응용 프로그램 구성 파일을 추가 하 고 다음 새를 사용 하 여 공급자를 추가 연결 문자열입니다. 있으면는 **ASPNETDB** 생성 하는 데이터베이스는 eventMapping는 sqlProvider에 연결할 규칙을 설정 하려면 필요 합니다.

SqlProvider 기본값을 사용 하거나 사용자 고유의 공급자를 구성 하는 경우 여부는 event 맵이 사용 하 여 공급자를 연결 하는 규칙을 추가 해야 합니다. 다음 규칙은 위에서 만든 새 공급자 연결에서 **모든 이벤트** 이벤트 맵. 이 규칙에 따라 모든 이벤트를 기록 합니다 **WebBaseEvent** MYASPNETDB 연결 문자열에서 사용할 MySqlWebEventProvider로 보내야 합니다. 다음 코드는 이벤트 맵 사용 하 여 공급자를 연결 하는 규칙을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

SQL Server 오류 보내기만 하려는 경우에 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Wmi 이벤트를 전달 하는 방법

Wmi 이벤트를 전달할 수도 있습니다. WMI 공급자는 기본적으로 글로벌 Web.config 파일에서 사용자에 대 한 구성 됩니다.

다음 코드 예제에서는 wmi 이벤트를 전달 하는 규칙을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

공급자 및 WMI 수신기 응용 프로그램의 이벤트를 수신 하도록 eventMapping 연결 하는 규칙을 추가 해야 합니다. WMI 공급자에 연결할 규칙을 추가 하는 다음 코드 예제는 **모든 이벤트** 이벤트 맵:

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-e-mail"></a>전자 메일에 대 한 이벤트를 전달 하는 방법

전자 메일에 대 한 이벤트를 전달할 수 있습니다. 주의 이벤트는 규칙 수 실수로 보내 처럼 사용자가 직접 정보도 많이 제공 하는 전자 메일 공급자에 매핑할 수 있습니다 하는 방법에 대 한 SQL Server 또는 이벤트 로그에 더 적합 해야 합니다. 두 명의 전자 메일 공급자가 있습니다. SimpleMailWebEventProvider 및 TemplatedMailWebEventProvider 합니다. 각 값에 동일한 구성 특성은 둘 다 에서만 사용할 수는 TemplatedMailWebEventProvider "템플릿" 및 "detailedTemplateErrors" 특성을 제외 하 고 있습니다.

> [!NOTE]
> 이러한 전자 메일 공급자 중 둘 다 구성 됩니다. Web.config 파일에 추가 해야 합니다.


이러한 두 전자 메일 공급자의 주요 차이점은 SimpleMailWebEventProvider 보내는 수정할 수 없는 일반 서식 파일에서 전자 메일입니다. 다음 규칙을 사용 하 여 구성 된 공급자의 목록에이 전자 메일 공급자를 추가 하는 샘플 Web.config 파일:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

전자 메일 공급자를 연결 하는 다음 규칙이 추가 되어는 **모든 이벤트** 이벤트 맵:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 추적

ASP.NET 2.0에는 추적 하는 주요 개선 사항은 세 가지가 있습니다.

1. 통합된 추적 기능
2. 추적 메시지에 대 한 프로그래밍 방식 액세스
3. 향상 된 응용 프로그램 수준 추적

## <a name="integrated-tracing-functionality"></a>통합 추적 기능

이제 추적 출력을 asp.net에서 System.Diagnostics.Trace 클래스에서 생성 된 메시지를 라우팅할 수 있으며 System.Diagnostics.Trace ASP.NET 추적에서 생성 된 메시지를 라우팅합니다. System.Diagnostics.Trace를 ASP.NET 계측 이벤트를 전달할 수도 있습니다. 이 기능을 제공 하 여 새 **writeToDiagnosticsTrace** 특성에는 &lt;추적&gt; 요소입니다. 이 부울 값이 true 이면 ASP.NET 추적 메시지는 등록 된 수신기에 추적 메시지를 표시 하 여 사용 하기 위해 System.Diagnostics 추적 인프라에 전달 됩니다.

## <a name="programmatic-access-to-trace-messages"></a>추적 메시지에 대 한 프로그래밍 방식 액세스

ASP.NET 2.0을 통해 모든 추적 메시지에 프로그래밍 방식으로 액세스할 수 있습니다는 **TraceContextRecord** 클래스 및 **TraceRecords** 컬렉션입니다. 등록 하는 추적 메시지에 액세스 하는 가장 효율적인 방법은 **TraceContextEventHandler** 대리자 (또한, ASP.NET 2.0의 새로운) 새 처리 하도록 **TraceFinished** 이벤트. 그런 다음 원하는 추적 메시지를 통해 루프 수 있습니다.

다음 코드 예제는이 보여줍니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

위의 예에서 TraceRecords 컬렉션을 반복 하면서 했으며 응답 스트림에 대 한 다음 각 메시지를 작성 합니다.

## <a name="improved-application-level-tracing"></a>향상 된 응용 프로그램 수준 추적

응용 프로그램 수준 추적 새의 도입을 통해 향상 되었습니다 **mostRecent** 특성에는 &lt;추적&gt; 요소입니다. 이 특성 최신 응용 프로그램 수준 추적 출력 표시 되 고 requestlimit 지정 된 제한 초과 하는 오래 된 추적 데이터는 삭제 여부를 지정 합니다. False 인 경우, requestLimit 특성에 도달할 때까지 요청에 대 한 추적 데이터가 표시 됩니다.

## <a name="aspnet-command-line-tools"></a>ASP.NET 명령줄 도구

ASP.NET의 구성에서 지원 하기 위해 몇 가지 명령줄 도구가 있습니다. ASP.NET 개발자에 게 aspnet 익숙한\_regiis.exe 도구입니다. ASP.NET 2.0 구성에 도움이 다른 3 개의 명령줄 도구를 제공 합니다.

다음과 같은 명령줄 도구를 사용할 수 있습니다.

| **도구** | **사용 하 여** |
| --- | --- |
| **aspnet\_regiis.exe** | IIS와 ASP.NET의 등록을 허용합니다. 두 가지 버전의이 도구는 프레임 워크 폴더에서 32 비트 시스템 및 Framework64 폴더입니다.) (에서 64 비트 시스템에 대 한 ASP.NET 2.0과 함께 제공 되 64 비트 버전 32 비트 운영 체제에 설치 되어 있지 않습니다. |
| **aspnet\_regsql.exe** | Asp.net에서 SQL Server 공급자에서 사용 하기 위해 Microsoft SQL Server 데이터베이스를 만들려고 하거나 추가 하거나 기존 데이터베이스에서 옵션을 제거 하는 ASP.NET SQL Server 등록 도구 사용 됩니다. Aspnet\_regsql.exe 파일은 폴더에 있는 [drive:]\WINDOWS\Microsoft.NET\Framework\versionNumber 웹 서버에 있습니다. |
| **aspnet\_regbrowsers.exe** | ASP.NET Browser Registration tool 구문 분석 및 모든 시스템 수준 브라우저 정의 어셈블리로 컴파일하고 전역 어셈블리 캐시에 어셈블리를 설치 합니다. 브라우저 정의 파일을 사용 하 여 도구 (합니다. 브라우저 파일)에서.NET Framework 브라우저 하위 디렉터리입니다. 이 도구는 %SystemRoot%\Microsoft.NET\Framework\version\ 디렉터리에서 찾을 수 있습니다. |
| **aspnet\_compiler.exe** | ASP.NET 컴파일 도구를 사용 하면 내부 또는 프로덕션 서버와 같은 대상 위치에 배포에 대 한 ASP.NET 웹 응용 프로그램을 컴파일할 수 있습니다. 내부 컴파일에 응용 프로그램이 컴파일되는 동안 최종 사용자가 응용 프로그램에 대 한 첫 번째 요청에서 지연 발생 하지 않으면 때문에 응용 프로그램 성능을 수 있습니다. |

때문에 aspnet\_regiis.exe 도구는 ASP.NET 2.0으로 새로운, म가 여기서 설명 하지 것입니다.

## <a name="aspnet-sql-server-registration-tool---aspnetregsqlexe"></a>ASP.NET SQL Server 등록 도구 aspnet\_regsql.exe

여러 유형의 SQL Server ASP.NET 등록 도구를 사용 하 여 옵션을 설정할 수 있습니다. SQL 연결, 지정 되는 ASP.NET 응용 프로그램 서비스 사용 하 여 SQL Server 정보를 관리, SQL 캐시 종속성에는 사용 된 데이터베이스나 테이블 지정 하 고 추가 하거나 제거할 수 있습니다 SQL Server를 사용 하 여 저장 프로시저 및 세션 상태에 대 한 지원.

여러 ASP.NET 응용 프로그램 서비스에 데이터 저장 및 검색 데이터 원본에서 관리 하는 공급자가 사용 합니다. 각 공급자는 데이터 원본에 특정 합니다. ASP.NET 다음 ASP.NET 기능에 대 한 SQL Server 공급자가 포함 되어 있습니다.

- 멤버 자격 (의 [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) 클래스).
- 역할 관리 (의 [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) 클래스).
- 프로필 (의 [SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx) 클래스).
- 웹 파트 개인 설정 (의 [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx) 클래스).
- 웹 이벤트 (의 [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx) 클래스).

ASP.NET을 설치 하는 경우 각각의 공급자를 사용 하는 ASP.NET 기능에 대 한 SQL Server 공급자를 지정 하는 구성 요소 서버에 대해 Machine.config 파일에 포함 됩니다. 이러한 공급자는 SQL Server 2005 Express의 로컬 사용자 인스턴스에 연결 하는 데 기본적으로 구성 됩니다. 공급자가 사용 되는 기본 연결 문자열을 변경 하면 컴퓨터 구성에서 구성 된 ASP.NET 기능 중 하나를 사용 하려면 먼저 설치 해야 합니다 SQL Server 데이터베이스와 데이터베이스 요소 Aspnet를사용하여선택한기능에대한\_regsql.exe 합니다. SQL 등록 도구를 사용 하 여 지정한 데이터베이스가 아직 없는 경우 (aspnetdb 수는 기본 데이터베이스 명령줄에 지정 되지 않은 경우), 현재 사용자는 SQL Server에서도 스키마 e를 만들 데이터베이스를 만들 수 있는 권한을 갖고 있어야 합니다 데이터베이스 내에서 lements 합니다.

### <a name="sql-cache-dependency"></a>SQL 캐시 종속성

ASP.NET 출력 캐싱을 고급 기능은 SQL 캐시 종속성 사용 하는 것입니다. SQL 캐시 종속성 지원 작업의 두 가지 모드: 하나 테이블 폴링 및 SQL Server 2005의 쿼리 알림 기능을 사용 하는 두 번째 모드의 ASP.NET 구현을 사용 합니다. 작업의 테이블 폴링 모드를 구성 하려면 SQL 등록 도구를 사용할 수 있습니다.

### <a name="session-state"></a>세션 상태

기본적으로 세션 상태 값 및 정보는 ASP.NET 프로세스 내의 메모리에 저장 됩니다. 또는 여러 웹 서버에서 공유할 수 있는, SQL Server 데이터베이스에 세션 데이터를 저장할 수 있습니다. SQL 등록 도구와 세션 상태에 대해 지정 하는 데이터베이스가 아직 없는 경우 현재 사용자 데이터베이스를 만들 SQL Server에서도 데이터베이스 내에서 스키마 요소를 만들 권한이 있어야 합니다. 데이터베이스가 있으면 현재 사용자는 기존 데이터베이스의 스키마 요소를 만들 수 있는 권한을 갖고 있어야 합니다.

세션 상태 데이터베이스를 SQL Server에 설치 하려면 실행 Aspnet\_regsql.exe 도구 고 명령 사용 하 여 다음 정보를 제공 합니다.

- SQL Server 이름 인스턴스를 사용 하는 **-S** 옵션입니다.
- SQL Server를 실행 하는 컴퓨터에서 데이터베이스를 만들 수 있는 권한을 가진 계정의 로그온 자격 증명을 지정 합니다. 사용 하 여는 **-E** 현재 로그온 한 사용자를 사용 하거나 사용 하는 옵션의 **-U** 사용자 ID를 지정 하는 옵션의 **-P** 암호를 지정 하는 옵션입니다.
- **-ssadd** 세션 상태 데이터베이스를 추가 하는 명령줄 옵션입니다.

기본적으로 Aspnet을 사용할 수 없습니다\_regsql.exe 도구를 SQL Server 2005 Express Edition을 실행 하는 컴퓨터에 세션 상태 데이터베이스를 설치 합니다.

### <a name="the-aspnet-browser-registration-tool---aspnetregbrowsersexe"></a>ASP.NET Browser Registration Tool-aspnet\_regbrowsers.exe

Machine.config 파일에 섹션이 포함 된 asp.net 버전 1.1에서는 &lt;browserCaps&gt;합니다. 이 섹션에는 일련의 정규식에 따라 다양 한 브라우저에 대 한 구성을 정의 하는 XML 항목 포함 되어 있습니다. ASP.NET 버전 2.0에 대 한 새 합니다. 브라우저 파일 XML 항목을 사용 하 여 특정 브라우저의 매개 변수를 정의 합니다. 새 브라우저에 추가 하 여 정보를 추가 합니다. 브라우저 파일 시스템에 %SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers에 있는 폴더입니다.

브라우저 정보가 필요할 때마다 응용 프로그램.config 파일을 읽지 않으므로, 때문에 새을 만들 수 있습니다. 브라우저 파일 및 실행된 Aspnet\_regbrowsers.exe를 어셈블리에 필요한 변경 작업을 추가 합니다. 따라서 서버를 정보를 선택 하도록 응용 프로그램 중 하나를 종료할 필요가 새 브라우저 정보에 즉시 액세스할 수 있습니다. 응용 프로그램의 현재 HttpRequest 브라우저 속성을 통해 브라우저 기능에 액세스할 수 있습니다.

Aspnet를 실행 하는 경우 다음 옵션을 사용할 수 있는\_regbrowser.exe:

| **옵션** | **설명** |
| --- | --- |
| **-?** | Aspnet 표시\_regbbrowsers.exe 명령 창에서 도움말 텍스트입니다. |
| **-i** | 런타임 브라우저 기능 어셈블리를 만들고 전역 어셈블리 캐시에 설치 합니다. |
| **-u** | 런타임 브라우저 기능 어셈블리를 전역 어셈블리 캐시에서 제거합니다. |

## <a name="the-aspnet-compilation-tool---aspnetcompilerexe"></a>ASP.NET Compilation Tool-aspnet\_compiler.exe

일반적인 두 가지 방법으로 ASP.NET 컴파일 도구를 사용할 수 있습니다: 내부 컴파일 및 배포, 대상 출력 디렉터리를 지정 위치에 대 한 컴파일을 위해.

### <a name="compiling-an-application-in-placehttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[현재 위치에서 응용 프로그램 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET Compilation tool 위치에서 응용 프로그램을 컴파일할 수, 즉, 일반 컴파일 오류를 발생 시킬 응용 프로그램에 대 한 여러 요청의 동작을 모방 합니다. 미리 컴파일된 사이트의 사용자는 첫 번째 요청에서 페이지 컴파일로 인 한 지연을 발생 하지 않습니다.

내부에서 사이트를 미리 컴파일하는 경우 다음 항목에 적용 됩니다.

- 사이트의 파일 및 디렉터리 구조를 유지합니다.
- 사이트 서버에서 사용 되는 모든 프로그래밍 언어에 대 한 컴파일러 있어야 합니다.
- 모든 파일에 컴파일 오류가 발생 하면 전체 사이트 컴파일이 실패 합니다.

새 소스 파일을 추가한 후 위치에서 응용 프로그램을 다시 컴파일할 수 있습니다. 포함 하지 않으면 새롭거나 변경 된 파일이 컴파일됩니다는 **-c** 옵션입니다.

> [!NOTE]
> 중첩 된 응용 프로그램을 포함 하는 응용 프로그램을 컴파일하는 중첩된 된 응용 프로그램을 컴파일하지 않습니다. 중첩된 된 응용 프로그램 별도로 컴파일해야 합니다.


### <a name="compiling-an-application-for-deploymenthttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[배포에 대 한 응용 프로그램 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

TargetDir 매개 변수를 지정 하 여 배포 (컴파일 대상 위치에)에 대 한 응용을 프로그램을 컴파일합니다. TargetDir 웹 응용 프로그램에 대 한 최종 위치 이거나 컴파일된 응용 프로그램을 다시 배포할 수 있습니다. 사용 하는 **-u** 옵션을 변경할 수 있습니다 컴파일된 응용 프로그램에서 특정 파일에 다시 컴파일하지 않고 하는 방식으로 응용 프로그램을 컴파일합니다. Aspnet\_compiler.exe에서는 정적 및 동적 파일 형식 구분 하 고 결과 응용 프로그램을 만들 때 다른 방식으로 처리 합니다.

- 정적 파일 형식은 관련된 컴파일러는 하지 않거나 파일을 같은 공급자 빌드를 하는 명명 된.css,.gif,.htm,.html,.jpg,.js 등의 확장에 있어야 합니다. 이러한 파일의 상대적 위치 유지 디렉터리 구조에서 대상 위치로 복사 하기만 하면 됩니다.
- 동적 파일 유형은 관련된 컴파일러 또는.asax,.ascx,.ashx,.aspx, 브라우저,.master, 등과 같은 ASP.NET 관련 파일 이름 확장명을 사용 하 여 파일을 포함 하 여 공급자를 빌드하는 것입니다. ASP.NET 컴파일 도구는 이러한 파일에서 어셈블리를 생성합니다. 경우는 **-u** 옵션을 생략 하면, 도구도 파일 이름 확장명으로 파일을 만듭니다. 원본 파일은 어셈블리에 매핑되는 COMPILED 합니다. 을 보장 하기 위해 응용 프로그램 소스 디렉터리 구조가 유지 되는 도구는 대상 응용 프로그램에 해당 위치에 자리 표시자 파일을 생성 합니다.

사용 해야 합니다는 **-u** 컴파일된 응용 프로그램의 콘텐츠를 수정 될 수 있음을 나타내려면이 옵션을 합니다. 그렇지 않으면 후속 수정 내용을 무시 되거나 때문에 런타임 오류가 발생 합니다.

다음 표에서 어떻게 ASP.NET 컴파일 도구 핸들 다른 파일 형식의 경우 설명는 **-u** 옵션이 포함 됩니다.

| **파일 형식** | **컴파일러 동작** |
| --- | --- |
| .ascx, .aspx, .master | 이러한 파일에 포함 된 모든 코드 및 코드 숨김 파일을 모두 포함 하는 태그 코드와 소스 코드도 분할 됩니다 &lt;스크립트 runat = "server"&gt; 요소입니다. 소스 코드 해싱 알고리즘에서 파생 된 이름 갖는 어셈블리로 컴파일하고 Bin 디렉터리에 저장 됩니다. 인라인 코드, 즉, 사이 포함 된 코드는  **&lt; %**  및  **% &gt;**  대괄호는 태그에 포함 되며 컴파일되지 않습니다. 새 파일의 소스 파일과 동일한 이름의 태그를 포함 하도록 만들고 해당 출력 디렉터리에 배치 합니다. |
| .ashx, .asmx | 이러한 파일 컴파일되고 고 컴파일되지 출력 디렉터리로 이동 됩니다. 컴파일된 처리기 코드 하려는 경우 앱의 소스 코드 파일에 코드를 배치\_코드 디렉터리입니다. |
| .cs,.vb,.jsl,.cpp (앞에서 나열 된 파일 형식에 대 한 코드 숨김 파일 제외) | 이러한 파일 컴파일되고 참조 하는 어셈블리에 리소스로 포함 됩니다. 소스 파일은 출력 디렉터리에 복사 되지 않습니다. 코드 파일을 참조 하지 않은 경우 컴파일되지 않습니다. |
| 사용자 지정 파일 형식 | 이러한 파일은 컴파일되지 않습니다. 이러한 파일은 해당 출력 디렉터리에 복사 됩니다. |
| 소스 코드 파일에서 응용 프로그램\_코드 하위 디렉터리 | 두이 파일은 어셈블리에 컴파일됩니다를 Bin 디렉터리에 배치 합니다. |
| 앱에서 파일을.resx 및.resource\_GlobalResources 하위 디렉터리 | 두이 파일은 어셈블리에 컴파일됩니다를 Bin 디렉터리에 배치 합니다. 앱\_주 출력 디렉터리에서 하위 디렉터리 GlobalResources 만들어지고.resx 또는.resources 파일의 원본 디렉터리에 있는 출력 디렉터리에 복사 됩니다. |
| 앱에서 파일을.resx 및.resource\_LocalResources 하위 디렉터리 | 이러한 파일 컴파일되고 해당 출력 디렉터리에 복사 됩니다. |
| 앱에서.skin 파일\_테마 하위 디렉터리 | .Skin 파일 및 정적 테마 파일 컴파일되지 않은 하 고 해당 출력 디렉터리에 복사 됩니다. |
| 브라우저 Web.config 정적 파일 형식을 Bin 디렉터리에 이미 있는 어셈블리 | 이러한 파일은 출력 디렉터리에 복사 됩니다. |

다음 표에서 어떻게 ASP.NET 컴파일 도구 핸들 다른 파일 형식의 경우 설명는 **-u** 옵션을 생략 합니다.

| **파일 형식** | **컴파일러 동작** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | 이러한 파일에 포함 된 모든 코드 및 코드 숨김 파일을 모두 포함 하는 태그 코드와 소스 코드도 분할 됩니다 &lt;스크립트 runat = "server"&gt; 요소입니다. 소스 코드는 해싱 알고리즘에서 파생 된 이름 갖는 어셈블리로 컴파일됩니다. 결과 어셈블리 Bin 디렉터리에 배치 됩니다. 인라인 코드, 즉, 사이 포함 된 코드는  **&lt; %**  및  **% &gt;**  대괄호는 태그에 포함 되며 컴파일되지 않습니다. 컴파일러는 소스 파일과 동일한 이름의 태그를 포함할 새 파일을 만듭니다. 이러한 결과 파일은 Bin 디렉터리에 배치 됩니다. 또한 컴파일러의 소스 파일과 동일한 이름의 하지만 확장명은 파일을 만듭니다. 매핑 정보를 포함 하는 컴파일된 합니다. 합니다. 컴파일된 파일은 소스 파일의 원래 위치에 해당 하는 출력 디렉터리에 배치 됩니다. |
| .ascx | 이러한 파일은 태그 및 소스 코드도 분할 됩니다. 소스 코드를 어셈블리에 컴파일되고 해싱 알고리즘에서 파생 된 형식의 이름으로 Bin 디렉터리에 배치 됩니다. 태그 파일이 생성 됩니다. |
| .cs,.vb,.jsl,.cpp (앞에서 나열 된 파일 형식에 대 한 코드 숨김 파일 제외) | .Ascx,.ashx, 또는.aspx 파일에서 생성 된 어셈블리에서 참조 되는 소스 코드를 어셈블리에 컴파일되고 Bin 디렉터리에 배치 됩니다. 원본 파일이 복사 됩니다. |
| 사용자 지정 파일 형식 | 이러한 파일은 동적 파일 처럼 컴파일됩니다. 에 기반 하는 파일의 형식에 따라 컴파일러 출력 디렉터리에 매핑 파일을 배치할 수 있습니다. |
| 응용 프로그램의 파일\_코드 하위 디렉터리 | 이 하위 디렉터리에서 소스 코드 파일 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. |
| 응용 프로그램의 파일\_GlobalResources 하위 디렉터리 | 두이 파일은 어셈블리에 컴파일됩니다를 Bin 디렉터리에 배치 합니다. 앱\_GlobalResources 하위 디렉터리는 기본 출력 디렉터리 아래에 생성 됩니다. 구성 파일 appliesTo를 지정 하는 경우 "All" =.resx 및.resources 파일은 출력 디렉터리에 복사 됩니다. 참조 되는 복사 되지 않습니다는 [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)합니다. |
| 앱에서 파일을.resx 및.resource\_LocalResources 하위 디렉터리 | 두이 파일은 고유한 이름으로 어셈블리에 컴파일됩니다를 Bin 디렉터리에 배치 합니다. .Resx 또는.resource 파일이 출력 디렉터리에 복사 됩니다. |
| 앱에서.skin 파일\_테마 하위 디렉터리 | 테마 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 스텁 파일.skin 파일에 대해 만들어지고 해당 출력 디렉터리에 배치 합니다. 정적 파일 (예:.css) 출력 디렉터리에 복사 됩니다. |
| 브라우저 Web.config 정적 파일 형식을 Bin 디렉터리에 이미 있는 어셈블리 | 이러한 파일은 출력 디렉터리에 복사 됩니다. |

### <a name="fixed-assembly-nameshttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[고정된 어셈블리 이름](https://msdn.microsoft.com/library/ms229863.aspx##)

MSI Windows Installer를 사용 하 여 웹 응용 프로그램 배포 등의 일부 시나리오에는 어셈블리 또는 업데이트에 대 한 구성 설정을 확인 하는 일관 된 디렉터리 구조 뿐만 아니라 일관 된 파일 이름과 콘텐츠를 사용을 해야 합니다. 이러한 경우에 사용할 수 있습니다는 **-fixednames** ASP.NET Compilation tool 어셈블리로 컴파일해야 있는지를 지정 하는 옵션 where를 사용 하는 대신 각 소스 파일에 대 한 여러 페이지 어셈블리로 컴파일됩니다. 많은 수의 어셈블리를 되므로 주의 하 여이 옵션을 사용 해야 확장성 고려 하는 경우 발생할 수 있습니다.

### <a name="strong-name-compilationhttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[강력한 이름의 컴파일](https://msdn.microsoft.com/library/ms229863.aspx##)

**aptca**, **-delaysign**, **-keycontainer** 및 **-keyfile** Aspnet를 사용할 수 있도록 옵션이 제공 됩니다\_ 사용 하지 않고 compiler.exe를 만드는 강력한 이름의 어셈블리는 [강력한 이름 도구 (Sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) 별도로 합니다. 이러한 옵션 각각 해당을 **AllowPartiallyTrustedCallersAttribute**, **AssemblyDelaySignAttribute**, **AssemblyKeyNameAttribute**, 및  **AssemblyKeyFileAttribute**합니다.

이러한 특성에 대 한 설명은이 과정의 범위를 벗어났습니다.

## <a name="labs"></a>랩

다음 랩 각각 이전 랩에 작성합니다. 순서 대로 수행 해야 합니다.

## <a name="lab-1-using-the-configuration-api"></a>구성 API를 사용 하는 랩 1:

1. 라는 새 웹 사이트를 만들 *mod9lab*합니다.
2. 새 웹 구성 파일을 사이트에 추가 합니다.
3. Web.config 파일에 다음을 추가 합니다.


[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

이렇게 하면 web.config 파일에 변경 내용을 저장 하는 권한이 있어야 합니다.

1. Default.aspx로 새 레이블 컨트롤을 추가 하 고 ID를 변경 **lblDebugStatus**합니다.
2. Default.aspx로 새 단추 컨트롤을 추가 합니다.
3. 단추 컨트롤의 ID를 변경 **btnToggleDebug** 텍스트를 **토글 디버그 상태**합니다.
4. Default.aspx의 코드 숨김 파일에 대 한 코드 보기를 열고 추가 **를 사용 하 여** 문을 **System.Web.Configuration** 다음과 같습니다.


[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 클래스 및 페이지에 두 개의 private 변수를 추가\_아래와 같이 Init 메서드:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 다음 코드 페이지를 추가\_부하:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 저장 하 고 default.aspx를 찾습니다. Label 컨트롤 현재 디버그 상태를 표시 되는지 확인 합니다.
2. Button 컨트롤 디자이너에서 두 번 클릭을 단추 컨트롤에 대 한 Click 이벤트에 다음 코드를 추가 합니다.


[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 저장 하 고 default.aspx를 찾은 다음 단추를 클릭 합니다.
2. 각 단추 클릭 하 고 확인 한 후 web.config 파일을 열고는 **디버그** 특성에 &lt;컴파일&gt; 섹션.

## <a name="lab-2-logging-application-restarts"></a>랩 2: 로깅 응용 프로그램 다시 시작

이 랩에서 응용 프로그램 종료, 시작 및 다시 컴파일 이벤트 뷰어에서 로깅을 설정/해제할 수 있도록 코드를 만듭니다.

1. Default.aspx로 DropDownList를 추가 하 고 ID ddlLogAppEvents로 변경 합니다.
2. 설정의 **AutoPostBack** DropDownList에 대 한 속성 **true**합니다.
3. 드롭다운 목록에 대 한 항목 컬렉션에 세 개의 항목을 추가 합니다. 확인 된 **텍스트** 첫 번째 항목에 대 한 *Select Value* 및-1 값입니다. 확인 된 **텍스트** 및 **값** 두 번째 항목의 **True** 및 **텍스트** 및 **값** 세 번째 항목의 **False**합니다.
4. Default.aspx로 새 레이블을 추가 합니다. ID를 변경 **lblLogAppEvents**합니다.
5. Default.aspx에 대 한 코드 숨김 보기를 열고 다음과 같이 HealthMonitoringSection 형식의 새로운 변수에 대 한 선언을 추가 합니다.


[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 다음 코드 페이지에서 기존 코드를 추가\_초기화:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. DropDownList 두 번 클릭을 SelectedIndexChanged 이벤트에 다음 코드를 추가 합니다.


[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Default.aspx를 찾습니다.
2. 드롭다운 목록으로 설정 **False**합니다.
3. 이벤트 뷰어에서 응용 프로그램 로그를 지웁니다.
4. 응용 프로그램에 대 한 디버그 특성을 변경 하려면 단추를 클릭 합니다.
5. 이벤트 뷰어에서 응용 프로그램 로그를 새로 고칩니다. 

    1. 모든 이벤트가 기록 된?
    2. 이유 또는 없습니까?
6. 드롭다운 목록으로 설정 **True입니다.**
7. 응용 프로그램에 대 한 디버그 특성을 설정/해제 단추를 클릭 합니다.
8. 응용 프로그램 로그인을 이벤트 뷰어를 새로 고칩니다. 

    1. 모든 이벤트가 기록 된?
    2. 응용 프로그램 종료에 대 한 이유는 무엇 이었습니까?
9. 켜기 및 끄기 로깅와 web.config 파일에 대 한 변경 내용을 확인 합니다.

## <a name="more-information"></a>추가 정보:

ASP.NET 2.0의 공급자 모델을 사용 하면 뿐만 아니라 응용 프로그램 계측 하지만 다양 한 용도 멤버 자격, 프로필 등의 사용자 고유의 공급자를 만들 수 있습니다. 사용자 지정 공급자를 텍스트 파일로 응용 프로그램 이벤트 로그를 작성 방법에 대 한 자세한 내용은 방문 [이 링크](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)합니다.
