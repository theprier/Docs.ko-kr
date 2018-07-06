---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 구성 및 계측 | Microsoft Docs
author: microsoft
description: 구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API pr 되도록 구성 변경 내용을 허용 하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 8437b13cae83208983f26e0a5042a5f6c19e516e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822909"
---
<a name="configuration-and-instrumentation"></a>구성 및 계측
====================
[Microsoft](https://github.com/microsoft)

> 구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API를 프로그래밍 방식으로 되도록 구성 변경 내용을 허용 합니다. 또한 많은 새 구성 설정이 새 구성 및 계측을 허용 합니다.


구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API를 프로그래밍 방식으로 되도록 구성 변경 내용을 허용 합니다. 또한 많은 새 구성 설정이 새 구성 및 계측을 허용 합니다.

이 모듈에서는 살펴보겠습니다 ASP.NET을 구성 API에서 읽기 및 ASP.NET 구성 파일에 쓰기와 관련 된와 ASP.NET 계측도 살펴보겠습니다. 또한 ASP.NET 추적의 새로운 기능을 설명 합니다.

## <a name="aspnet-configuration-api"></a>ASP.NET 구성 API

ASP.NET 구성 API를 사용 하면 개발, 배포 및 단일 프로그래밍 인터페이스를 사용 하 여 응용 프로그램 구성 데이터를 관리할 수 있습니다. 개발 하 고 구성 파일에서 XML을 직접 편집 하지 않고 ASP.NET 구성을 완료를 프로그래밍 방식으로 수정할 구성 API를 사용할 수 있습니다. 또한 구성 API 콘솔 응용 프로그램 및 개발 하는 스크립트, 웹 기반 관리 도구 및 Microsoft Management Console (MMC) 스냅인을 사용할 수 있습니다.

다음 두 가지 구성 관리 도구 구성 API를 사용 하 고.NET Framework 버전 2.0에 포함 된:

- 관리 작업을 간소화 하기 위해 구성 API를 사용 하는 ASP.NET MMC 스냅인 구성 계층 구조의 모든 수준에서 로컬 구성 데이터의 통합된 보기를 제공 합니다.
- 에 로컬 및 원격 응용 프로그램에 대 한 구성 설정을 관리할 수 있도록 하는 웹 사이트 관리 도구에서 호스트 되는 사이트를 포함 합니다.

ASP.NET 구성 API는 웹 사이트 및 응용 프로그램을 프로그래밍 방식으로 구성 하는 데 사용할 수 있는 ASP.NET 관리 개체의 집합을 구성 합니다. 관리 개체는.NET Framework 클래스 라이브러리로 구현 됩니다. 구성 API 프로그래밍 모델에 컴파일 타임에 데이터 형식을 적용 하 여 코드 일관성 및 안정성을 확인 하는 데 도움이 됩니다. 응용 프로그램 구성 관리를 쉽게 구성 API 구성 계층 구조의 모든 지점에서 서로 다른 별도 컬렉션으로 데이터를 보는 대신 단일 컬렉션으로 병합 되는 데이터를 볼 수 있습니다. 구성 파일입니다. 또한 구성 API를 사용 하는 구성 파일에서 XML을 직접 편집 하지 않고 전체 응용 프로그램 구성을 조작할 수 있습니다. 마지막으로, API는 웹 사이트 관리 도구와 같은 관리 도구를 지원 하 여 구성 작업을 간소화 합니다. 구성 API 컴퓨터 구성 파일의 생성을 지원 하 고 여러 컴퓨터에서 구성 스크립트를 실행 하 여 배포를 간소화 합니다.

> [!NOTE]
> 구성 API는 IIS 응용 프로그램 만들기를 지원 하지 않습니다.


## <a name="working-with-local-and-remote-configuration-settings"></a>로컬 및 원격 구성 설정 사용 하 여 작업

구성 개체를 사용 하는 컴퓨터와 같은 특정 물리적 엔터티 또는 응용 프로그램 또는 웹 사이트와 같은 논리 엔터티에 적용 되는 구성 설정을 병합 된 뷰를 나타냅니다. 지정된 된 논리 엔터티 원격 서버에서 로컬 컴퓨터에 있을 수 있습니다. 지정 된 엔터티에 대 한 구성 파일이 있으면 합니다 Machine.config 파일에 정의 된 대로 구성 개체의 기본 구성 설정을 나타냅니다.

다음 클래스에서 열린 구성 방법 중 하나를 사용 하 여 구성 개체를 가져올 수 있습니다.

1. 엔터티를 클라이언트 응용 프로그램인 경우 ConfigurationManager 클래스입니다.
2. 엔터티 웹 응용 프로그램인 경우 WebConfigurationManager 클래스입니다.

이러한 메서드는 다시 필요한 메서드 및 기본 구성 파일을 처리 하는 속성을 제공 하는 구성 개체를 반환 합니다. 이러한 파일을 읽거나 쓰기 위해 액세스할 수 있습니다.

### <a name="reading"></a>읽기

GetSection 또는 GetSectionGroup 메서드를 사용 하 여 구성 정보를 읽습니다. 사용자 또는 프로세스를 읽는 모든 계층의 구성 파일의 권한이 읽기 있어야 합니다.

> [!NOTE]
> 경로 매개 변수를 사용 하는 정적 GetSection 메서드를 사용 하는 경우 path 매개 변수는 코드가 실행 되는 응용 프로그램에 참조 해야 합니다. 그렇지 않으면 매개 변수 무시 되 고 현재 실행 중인 응용 프로그램에 대 한 구성 정보가 반환 됩니다.


### <a name="writing"></a>쓰기

구성 정보를 쓸 저장 방법 중 하나를 사용 합니다. 사용자 또는 쓰기를 포함 해야 하는 프로세스 구성 파일 및 디렉터리를 현재 구성 계층 구조 수준에 대 한 쓰기 권한과 뿐만 아니라 모든 계층에서 구성 파일에 대 한 읽기 권한이 있습니다.

지정 된 엔터티에 대 한 상속 된 구성 설정을 나타내는 구성 파일을 생성 하려면 다음 구성 저장 방법 중 하나를 사용 합니다.

1. 새 구성 파일을 만들려면 저장 메서드.
2. 다른 위치에 새 구성 파일을 생성 하기 위한 SaveAs 메서드.

## <a name="configuration-classes-and-namespaces"></a>구성 클래스 및 네임 스페이스

여러 구성 클래스 및 메서드는 서로 비슷합니다. 다음 표에서 가장 일반적으로 사용 되는 클래스와 네임 스페이스를 설명합니다.

| **구성 클래스 또는 네임 스페이스** | **설명** |
| --- | --- |
| [System.Configuration](https://msdn.microsoft.com/library/system.configuration.aspx) namespace | 모든.NET Framework 응용 프로그램에 대 한 기본 구성 클래스를 포함 합니다. 섹션 처리기 클래스가 GetSection 등 GetSectionGroup 메서드에서 섹션에 대 한 구성 데이터를 가져오기 위해 사용 됩니다. 이 두 메서드는 static이 아니고 합니다. |
| System.Configuration.Configuration 클래스 | 컴퓨터, 응용 프로그램, 웹 디렉터리 또는 다른 리소스에 대 한 구성 데이터의 집합을 나타냅니다. 이 클래스는 유용한 메서드가 GetSection 등 GetSectionGroup, 구성 설정을 업데이트 하 고 섹션 및 섹션 그룹에 대 한 참조를 얻는 포함 합니다. 이 클래스는 WebConfigurationManager 및 ConfigurationManager 클래스의 메서드와 같은 디자인 타임 구성 데이터를 가져오는 방법에 대 한 반환 형식으로 사용 됩니다. |
| System.Web.Configuration 네임 스페이스 | ASP.NET 구성 섹션에 정의 된 섹션 처리기 클래스가 포함 되어 있습니다 [ASP.NET 구성 설정](https://msdn.microsoft.com/library/b5ysx397.aspx)합니다. 섹션 처리기 클래스가 GetSection 등 GetSectionGroup 메서드에서 섹션에 대 한 구성 데이터를 가져오기 위해 사용 됩니다. |
| System.Web.Configuration.WebConfigurationManager class | 런타임 및 디자인 타임 구성 설정에 대 한 참조를 가져오기 위한 유용한 메서드를 제공 합니다. 이러한 메서드는 반환 형식으로 System.Configuration.Configuration 클래스를 사용 합니다. 이 클래스의 정적 GetSection 메서드 또는 System.Configuration.ConfigurationManager 클래스의 비정적 GetSection 메서드를 서로 교환해 서 사용할 수 있습니다. 웹 응용 프로그램 구성에 대 한 System.Configuration.ConfigurationManager 클래스 대신 System.Web.Configuration.WebConfigurationManager 클래스를 사용 하는 것이 좋습니다. |
| [System.Configuration.Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx) namespace | 사용자 지정 및 구성 공급자를 확장 하는 방법을 제공 합니다. 구성 시스템의 모든 공급자 클래스에 대 한 기본 클래스입니다. |
| [System.Web.Management](https://msdn.microsoft.com/library/system.web.management.aspx) namespace | 클래스 및 웹 응용 프로그램의 상태를 모니터링 및 관리에 대 한 인터페이스를 포함 합니다. 엄격히 말해,이 네임 스페이스는 구성 API의 일부로 간주 되지 않습니다. 예를 들어, 추적 및 이벤트 발생이 네임 스페이스의 클래스에 의해 수행 됩니다. |
| [System.Management.Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) 네임 스페이스 | 해당 관리 정보 및 잠재 고객에 게 Windows Management Instrumentation (WMI)를 통해 이벤트를 노출 하는 응용 프로그램의 계측을 위해 필요한 클래스를 제공 합니다. ASP.NET 상태 모니터링 이벤트를 제공 하도록 WMI를 사용 합니다. 엄격히 말해,이 네임 스페이스는 구성 API의 일부로 간주 되지 않습니다. |

## <a name="reading-from-aspnet-configuration-files"></a>ASP.NET 구성 파일에서 읽기

WebConfigurationManager 클래스는 ASP.NET 구성 파일에서 읽는 데 필요한 핵심 클래스입니다. 기본적으로 세 가지 단계를 ASP.NET 구성 파일을 읽는 것:

1. OpenWebConfiguration 메서드를 사용 하 여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대 한 참조를 가져옵니다.
3. 구성 파일에서 원하는 정보를 읽습니다.

개체가 나타내는 구성 특정 구성 파일을 나타내지 않습니다. 대신, 컴퓨터, 응용 프로그램 또는 웹 사이트의 구성에 병합 된 뷰를 나타냅니다. 다음 코드 샘플 이라는 웹 응용 프로그램의 구성을 나타내는 구성 개체를 인스턴스화하고 *ProductInfo*합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> 에 들어 있는 /ProductInfo 경로가 존재 하지 않으면 위의 코드는 반환할 지정 된 대로 기본 구성 합니다 machine.config 파일 note 합니다.


구성 개체를 만든 후에 다음 구성 설정을 검색할 GetSection 또는 GetSectionGroup 메서드를 사용할 수 있습니다. 다음 예제에서는 위의 ProductInfo 응용 프로그램에 대 한 가장 설정에 대 한 참조를 가져옵니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>ASP.NET 구성 파일에 쓰기

구성 파일에서 읽기와 같이 WebConfigurationManager 클래스는 Asp.NET 구성 파일에 쓰기 위한 핵심입니다. ASP.NET 구성 파일에 쓰기 위한 3 단계가 있습니다.

1. OpenWebConfiguration 메서드를 사용 하 여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대 한 참조를 가져옵니다.
3. 저장 또는 다른 이름으로 저장을 사용 하 여 구성 파일에서 원하는 정보를 쓸 메서드.

다음 코드를 변경할을 **디버그** 특성을 &lt;컴파일&gt; false 요소:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

이 코드를 실행 하는 경우는 **디버그** 특성을 &lt;컴파일&gt; 요소에 대해 false로 설정 됩니다는 *webApp* 응용 프로그램의 web.config 파일입니다.

## <a name="systemwebmanagement-namespace"></a>System.Web.Management Namespace

System.Web.Management 네임 스페이스의 클래스 및 ASP.NET 응용 프로그램의 상태를 모니터링 및 관리에 대 한 인터페이스를 제공 합니다.

로깅은 공급자를 사용 하 여 이벤트를 연결 하는 규칙을 정의 하 여 수행 됩니다. 규칙에는 공급자에 게 전송 되는 이벤트의 형식을 정의 합니다. 다음 기본 이벤트를 기록할 수 있습니다.

| **WebBaseEvent** | 모든 이벤트에 대 한 기본 이벤트 클래스입니다. 필수 포함 이벤트 코드, 이벤트 상세 코드, 날짜 및 이벤트가 발생 하는 시간과 같은 모든 이벤트에 대 한 속성 시퀀스 번호, 이벤트 메시지 및 이벤트 세부 정보입니다. |
| --- | --- |
| **WebManagementEvent** | 응용 프로그램 수명, 요청, 오류 및 이벤트 감사와 같은 관리 이벤트에 대 한 기본 이벤트 클래스입니다. |
| **WebHeartbeatEvent** | 유용한 런타임 상태 정보를 캡처할 정기적으로 응용 프로그램에서 생성 된 이벤트입니다. |
| **WebAuditEvent** | 권한 부여 실패, 암호 해독 실패 등의 상황을 표시 하는 데 사용 되는 보안 감사 이벤트에 대 한 기본 클래스 *등입니다.* |
| **WebRequestEvent** | 모든 정보 요청 이벤트에 대 한 기본 클래스입니다. |
| **WebBaseErrorEvent** | 오류 상태를 나타내는 모든 이벤트에 대 한 기본 클래스입니다. |

사용할 수 있는 공급자의 형식에는 이벤트 출력 이벤트 뷰어, SQL Server, Windows Management Instrumentation (WMI) 및 전자 메일을 보내도록 할 수 있습니다. 미리 구성 된 공급자 및 이벤트 매핑 이벤트 출력을 기록 하는 데 필요한 작업량을 줄입니다.

ASP.NET 2.0 시작 및 중지와 처리 되지 않은 예외가 로깅 응용 프로그램 도메인을 기준으로 이벤트를 기록 하는 이벤트 로그 공급자-의-기본을 사용 합니다. 이렇게 하면 일부 기본 시나리오에 설명 합니다. 예를 들어, 응용 프로그램 예외를 throw 하지만 사용자 오류를 저장 하지 않습니다 하 고 재현할 수 없는 가정해 봅니다. 기본 이벤트 로그 규칙을 보다 명확히 파악할 어떤 종류의 오류가 발생 한 예외 및 스택 정보를 수집할 수 있다면 것입니다. 또 다른 예에는 응용 프로그램에 세션 상태가 손실 되는 경우 적용 됩니다. 이 경우 응용 프로그램 도메인 재활용 되 고 응용 프로그램 도메인을 멈춘 이유 애초에 이벤트 로그에서 찾을 수 있습니다.

또한 상태 모니터링 시스템은 확장 가능 합니다. 예를 들어, 사용자 지정 웹 이벤트를 정의 하 고, 응용 프로그램 내에서 발생 하도록 하 고, 다음에 이벤트 정보를 공급자에 게 보낼 전자 메일 같은 규칙을 정의할 수 있습니다. 이 옵션을 사용 하면 상태 공급자를 모니터링 하 여 계측을 쉽게 연결할 수 있습니다. 또 다른 예로, 이벤트를 주문 처리 이며 SQL Server 데이터베이스에 각 이벤트를 전송 하는 규칙 설정 될 때마다 실행 수 없습니다. 행에 여러 번을 로그 및 이벤트 전자 메일 기반 공급자를 사용 하도록 설정 하려면 사용자가 실패할 때 이벤트를 발생 발생할 수도 있습니다.

기본 공급자 및 이벤트의 구성은 전역 Web.config 파일에 저장 됩니다. 전역 Web.config 파일에 저장 ASP.NET 1 합니다 Machine.config 파일에 저장 된 모든 웹 기반 설정을 x입니다. 전역 Web.config 파일은 다음 디렉터리에 있습니다.

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

합니다 &lt;healthMonitoring&gt; 전역 Web.config 파일의 섹션에서는 기본 구성 설정을 제공 합니다. 이러한 설정을 재정의 하거나 구현 하 여 고유한 설정을 구성할 수 있습니다 합니다 &lt;healthMonitoring&gt; 응용 프로그램에 대 한 Web.config 파일의 섹션입니다.

합니다 &lt;healthMonitoring&gt; 전역 Web.config 파일의 섹션에 다음 항목이 포함 되어 있습니다.

| **공급자** | 이벤트 뷰어, WMI, and SQL Server에 대 한 설정 공급자를 포함 합니다. |
| --- | --- |
| **eventMappings** | 다양 한 WebBase 클래스에 대 한 매핑을 포함합니다. 사용자 고유의 이벤트 클래스를 생성 하는 경우이 목록은 확장할 수 있습니다. 사용자 고유의 이벤트 클래스를 생성 하면 보다 세부적인 정보를 보낼 공급자를 통해. 예를 들어 전자 메일에 사용자 지정 이벤트를 전송 하는 동안 SQL Server에 전송할 수 있도록 처리 되지 않은 예외를 구성할 수 있습니다. |
| **rules** | 연결 공급자에 대 한 eventMappings 됩니다. |
| **buffering** | 공급자에 게 이벤트를 플러시하는 빈도 확인 하려면 SQL Server 및 전자 메일 공급자를 사용 합니다. |

전역 Web.config 파일에서 코드 예제는 다음과 같습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>이벤트 뷰어에서 이벤트를 저장 하는 방법

로깅 이벤트에 대 한 공급자 앞서 설명한 대로 이벤트 뷰어는 구성 전역 Web.config 파일에 있습니다. 기본적으로 모든 이벤트에 따라 **WebBaseErrorEvent** 하 고 **WebFailureAuditEvent** 로깅됩니다. 이벤트 로그에 추가 정보를 기록 하는 추가 규칙을 추가할 수 있습니다. 예를 들어, 모든 이벤트를 기록 하려는 경우 (*즉*를 기반으로 하는 모든 이벤트 **WebBaseEvent**), Web.config 파일에 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

이 규칙은 연결 된 **모든 이벤트** 이벤트 로그 공급자에 게 이벤트 맵. EventMapping와 공급자는 전역 Web.config 파일에 포함 됩니다.

## <a name="how-to-store-events-to-sql-server"></a>SQL Server에 대 한 이벤트를 저장 하는 방법

이 메서드를 사용 합니다 **ASPNETDB** Aspnet에서 생성 된 데이터베이스\_regsql.exe 도구입니다. 앱에서 두 파일 기반 데이터베이스를 사용 하는 LocalSqlServer 연결 문자열을 사용 하 여 기본 공급자\_데이터 폴더 또는 SQL Server의 로컬 SQLExpress 인스턴스. LocalSqlServer 연결 문자열 및는 SqlProvider 전역 Web.config 파일에서 구성 됩니다.

전역 Web.config 파일에서 LocalSqlServer 연결 문자열은 다음과 같습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Aspnet를 사용 해야 다른 SQL Server 인스턴스를 사용 하려는 경우\_regsql.exe 도구인 %windir%\Microsoft.Net\Framework\v2.0 찾을 수 있는\* 폴더입니다. Aspnet를 사용 하 여\_regsql.exe 도구 사용자 지정 생성 **ASPNETDB** SQL Server 인스턴스에서 데이터베이스 응용 프로그램 구성 파일에 연결 문자열을 추가 하 고 그런 다음 새을 사용 하 여 공급자를 추가 연결 문자열입니다. 했으면 합니다 **ASPNETDB** 는 eventMapping는 sqlProvider 연결할 규칙을 설정 해야 데이터베이스 생성 합니다.

SqlProvider 기본값을 사용 하거나 고유한 공급자를 구성, 이벤트 지도 사용 하 여 공급자를 연결 하는 규칙을 추가 해야 합니다. 다음 규칙을 위에서 만든 새 공급자를 연결 합니다 **모든 이벤트** 이벤트 맵. 이 규칙을 기준으로 모든 이벤트를 기록 합니다 **WebBaseEvent** MYASPNETDB 연결 문자열을 사용 하는 MySqlWebEventProvider로 보내야 합니다. 다음 코드는 event 맵이 사용 하 여 공급자를 연결 하는 규칙을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

SQL Server 오류 보내기만 하려는 경우에 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Wmi 이벤트를 전달 하는 방법

Wmi 이벤트를 전달할 수도 있습니다. WMI 공급자는 기본적으로 전역 Web.config 파일의 수에 대 한 구성 됩니다.

다음 코드 예제에서는 wmi 이벤트를 전달 하는 규칙을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

eventMapping 공급자 및 이벤트에 대 한 수신 대기 하는 WMI 수신기 응용 프로그램에 연결 하는 규칙을 추가 해야 합니다. 다음 코드 예제에서는 WMI 공급자에 연결 하는 규칙을 추가 합니다 **모든 이벤트** 이벤트 맵:

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>전자 메일에 이벤트를 전달 하는 방법

전자 메일에 대 한 이벤트를 전달할 수도 있습니다. 주의 이벤트 규칙으로 보낼 수 있습니다 실수로 직접 정보가 많이 하는 전자 메일 공급자에 매핑할 수 있습니다. SQL Server 또는 이벤트 로그에 더 적합 합니다. 전자 메일 공급자가 두; SimpleMailWebEventProvider 및 TemplatedMailWebEventProvider 합니다. 각 "템플릿" 및 "detailedTemplateErrors" 특성을 둘 다 에서만 사용할는 TemplatedMailWebEventProvider를 제외 하 고 동일한 구성 특성을 포함 합니다.

> [!NOTE]
> 이러한 전자 메일 공급자 중 둘 다 구성 됩니다. Web.config 파일에 추가 해야 합니다.


이러한 두 전자 메일 공급자 간의 주요 차이점은 수정할 수 없는 제네릭 템플릿에서 SimpleMailWebEventProvider 보내는 전자 메일입니다. 샘플 Web.config 파일을 다음 규칙을 사용 하 여 구성 된 공급자 목록에이 전자 메일 공급자를 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

다음 규칙이 메일 공급자에 연결할 추가 되어는 **모든 이벤트** 이벤트 맵:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 추적

ASP.NET 2.0의 추적 세 가지 주요 개선 사항이 있습니다.

1. 통합된 추적 기능
2. 추적 메시지에 대 한 프로그래밍 방식 액세스
3. 향상 된 응용 프로그램 수준 추적

## <a name="integrated-tracing-functionality"></a>기능 추적 통합

이제 asp.net 추적 출력을 System.Diagnostics.Trace 클래스에 의해 생성 된 메시지를 라우팅할 수 있으며 System.Diagnostics.Trace ASP.NET 추적에서 생성 된 메시지를 라우팅합니다. System.Diagnostics.Trace를 ASP.NET 계측 이벤트를 전달할 수도 있습니다. 이 기능을 제공 하 여 새 **writeToDiagnosticsTrace** 특성을 &lt;추적&gt; 요소입니다. 이 부울 값이 true 이면 모든 등록 된 수신기에 추적 메시지를 표시 하 여 ASP.NET 추적 메시지 사용에 대 한 System.Diagnostics 추적 인프라에 전달 됩니다.

## <a name="programmatic-access-to-trace-messages"></a>추적 메시지에 대 한 프로그래밍 방식 액세스

ASP.NET 2.0을 통해 모든 추적 메시지에 프로그래밍 방식으로 액세스할 수 있습니다 합니다 **TraceContextRecord** 클래스와 **TraceRecords** 컬렉션입니다. 추적 메시지에 액세스 하는 가장 효율적인 방법은 등록 하는 것을 **TraceContextEventHandler** (ASP.NET 2.0의 새로운 항목도) 대리자 처리할 새 **TraceFinished** 이벤트입니다. 그런 다음 원하는 대로 추적 메시지를 통해 루프 수 있습니다.

다음 코드 샘플에서는이 보여 줍니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

위의 예에서 TraceRecords 컬렉션을 반복 하 고 각 메시지를 응답 스트림에 쓸입니다.

## <a name="improved-application-level-tracing"></a>향상 된 응용 프로그램 수준 추적

응용 프로그램 수준 추적의 새로운 도입을 통해 향상 되었습니다 **mostRecent** 특성을 &lt;추적&gt; 요소입니다. 이 특성에 있는지 여부를 가장 최근의 응용 프로그램 수준 추적 출력을 표시 하 고 requestlimit 표시 되는 제한 초과 하는 오래 된 추적 데이터는 삭제 됩니다 지정 합니다. False 이면 requestLimit 특성에 도달할 때까지 요청에 대 한 추적 데이터가 표시 됩니다.

## <a name="aspnet-command-line-tools"></a>ASP.NET 명령줄 도구

ASP.NET의 구성을 지원 하기 위해 몇 가지 명령줄 도구가 있습니다. ASP.NET 개발자에 게 aspnet 익숙한\_regiis.exe 도구입니다. ASP.NET 2.0 구성에 도움이 다른 세 가지 명령줄 도구를 제공 합니다.

다음 명령줄 도구를 사용할 수 있습니다.

| **도구** | **사용 하 여** |
| --- | --- |
| **aspnet\_regiis.exe** | IIS 사용 하 여 ASP.NET의 등록을 허용합니다. 두 가지 버전이 도구는 Framework 폴더의 32 비트 시스템 및 (Framework64 폴더입니다.)에서 64 비트 시스템에 대 한 ASP.NET 2.0과 함께 제공 되는 32 비트 OS에서 64 비트 버전 설치 되지 않습니다. |
| **aspnet\_regsql.exe** | ASP.NET에서 SQL Server 공급자 사용에 대 한 Microsoft SQL Server 데이터베이스를 만들 추가 또는 기존 데이터베이스에서 옵션을 제거 하려면 ASP.NET SQL Server 등록 도구 사용 됩니다. Aspnet\_regsql.exe 파일은 폴더에 있는 [drive:]\WINDOWS\Microsoft.NET\Framework\versionNumber 웹 서버에 있습니다. |
| **aspnet\_regbrowsers.exe** | ASP.NET 브라우저 등록 도구를 구문 분석 하 고 모든 시스템 수준 브라우저 정의를 어셈블리로 컴파일합니다 및 전역 어셈블리 캐시에 어셈블리를 설치 합니다. 브라우저 정의 파일을 사용 하는 도구 (합니다. 브라우저 파일)는.NET Framework 브라우저 하위 디렉터리에서. 이 도구는 %SystemRoot%\Microsoft.NET\Framework\version\ 디렉터리에서 찾을 수 있습니다. |
| **aspnet\_compiler.exe** | ASP.NET 컴파일 도구를 사용 하면 내부 또는 프로덕션 서버와 같은 대상 위치에 배포에 대 한 ASP.NET 웹 응용 프로그램을 컴파일할 수 있습니다. 내부 컴파일에 응용 프로그램이 컴파일되는 동안 최종 사용자 응용 프로그램에 대 한 첫 번째 요청에서 지연이 발생 하지 않는 때문에 응용 프로그램 성능을 수 있습니다. |

때문에 aspnet\_regiis.exe 도구를 ASP.NET 2.0에 다루지 것 같습니다.

## <a name="aspnet-sql-server-registration-tool---aspnetregsqlexe"></a>ASP.NET SQL Server 등록 도구-aspnet\_regsql.exe

여러 유형의 ASP.NET SQL Server 등록 도구를 사용 하 여 옵션을 설정할 수 있습니다. 있습니다 SQL 연결을 지정, ASP.NET 응용 프로그램 서비스는 SQL Server를 사용 하 여 정보를 관리 데이터베이스 또는 테이블에는 SQL 캐시 종속성에 대 한 사용을 지정 하 고 추가 하거나 제거할 수 SQL Server를 사용 하 여 저장 프로시저 및 세션 상태에 대 한 지원.

여러 ASP.NET 응용 프로그램 서비스에 데이터 저장 및 검색 데이터 원본에서 관리 하는 공급자를 사용 합니다. 각 공급자 데이터 원본에 따라 다릅니다. ASP.NET 다음 ASP.NET 기능에 대 한 SQL Server 공급자를 포함 합니다.

- 멤버 자격 (합니다 [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) 클래스).
- 역할 관리 (합니다 [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) 클래스).
- 프로필 (합니다 [SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx) 클래스).
- 웹 파트 개인 설정 (합니다 [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx) 클래스).
- 웹 이벤트 (합니다 [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx) 클래스).

ASP.NET을 설치한 경우 Machine.config 파일 서버에 대 한 각 공급자에 의존 하는 ASP.NET 기능에 대 한 SQL Server 공급자를 지정 하는 구성 요소를 포함 합니다. 이러한 공급자는 SQL Server 2005 Express의 로컬 사용자 인스턴스에 연결 하는 기본적으로 구성 됩니다. 공급자가 사용 된 기본 연결 문자열을 변경 하면 컴퓨터 구성에서 구성 된 ASP.NET 기능 중 하나를 사용 하려면 먼저 설치 해야 합니다는 SQL Server 데이터베이스와 데이터베이스 요소 Aspnet를사용하여선택한기능에대한\_regsql.exe 합니다. SQL 등록 도구를 사용 하 여 지정 된 데이터베이스 아직 없는 경우 (aspnetdb 수는 기본 데이터베이스 명령줄에 지정 되지 않은 경우), 현재 사용자 스키마 만들기에 대 한 SQL 서버에도에서 데이터베이스를 만들 권한이 있어야 합니다. 그런 다음 데이터베이스 내의 lements 합니다.

### <a name="sql-cache-dependency"></a>SQL 캐시 종속성

ASP.NET 출력 캐싱는 고급 기능은 SQL 캐시 종속성 사용 하는 것입니다. SQL 캐시 종속성 작업의 두 가지 모드에서 지원: ASP.NET 구현의 테이블 폴링 및 SQL Server 2005의 쿼리 알림 기능을 사용 하는 두 번째 모드를 사용 합니다. 작업의 테이블 폴링 모드를 구성 하는 SQL 등록 도구를 사용할 수 있습니다.

### <a name="session-state"></a>세션 상태

기본적으로 세션 상태 값과 정보는 ASP.NET 프로세스 내의 메모리에 저장 됩니다. 또는 여러 웹 서버에서 공유할 수 있는 SQL Server 데이터베이스에 세션 데이터를 저장할 수 있습니다. SQL 등록 도구를 사용 하 여 세션 상태에 대 한 지정 된 데이터베이스 아직 없는 경우에 현재 사용자 데이터베이스 내의 스키마 요소를 만들 SQL Server를도 단위로 데이터베이스 만들기 권한이 있어야 합니다. 데이터베이스 존재 하는 경우 현재 사용자에서 기존 데이터베이스의 스키마 요소를 만들 권한이 있어야 합니다.

SQL server 세션 상태 데이터베이스를 설치 하려면 Aspnet\_regsql.exe 도구 및 명령 사용 하 여 다음 정보를 제공 합니다.

- SQL Server의 이름 인스턴스를 사용 하는 **-S** 옵션입니다.
- SQL Server를 실행 하는 컴퓨터에서 데이터베이스를 만들 수 있는 권한을 가진 계정의 로그온 자격 증명을 지정 합니다. 사용 하 여를 **-E** 현재 로그온 한 사용자를 사용 하거나 사용 하는 옵션을 **-U** 와 함께 사용자 ID를 지정 하는 옵션을 **-P** 암호를 지정 하는 옵션입니다.
- 합니다 **-ssadd** 세션 상태 데이터베이스를 추가 하려면 명령줄 옵션입니다.

기본적으로 Aspnet 사용할 수 없습니다\_regsql.exe 도구를 SQL Server 2005 Express Edition을 실행 하는 컴퓨터에서 세션 상태 데이터베이스를 설치 합니다.

### <a name="the-aspnet-browser-registration-tool---aspnetregbrowsersexe"></a>ASP.NET 브라우저 등록 도구-aspnet\_regbrowsers.exe

Machine.config 파일에 라는 섹션이 포함 된 asp.net 버전 1.1에서는 &lt;browserCaps&gt;합니다. 이 섹션에는 일련의 정규식에 따라 다양 한 브라우저에 대 한 구성을 정의 하는 XML 항목 포함 되어 있습니다. ASP.NET 버전 2.0에 대 한 새 합니다. 브라우저 파일 XML 항목을 사용 하 여 특정 브라우저의 매개 변수를 정의 합니다. 새로 추가 하 여 새 브라우저 정보를 추가 합니다. 브라우저 파일 시스템에 %SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers에 있는 폴더입니다.

브라우저 정보가 필요할 때마다 응용 프로그램.config 파일을 읽지 않으므로, 때문에 새을 만들 수 있습니다. 브라우저 파일 및 실행된 Aspnet\_regbrowsers.exe 어셈블리에 필요한 변경 작업을 추가 합니다. 이 정보를 선택 하도록 응용 프로그램 중 하나를 종료 해야 하므로 새 브라우저 정보를 즉시 액세스 하도록 서버를를 수 있습니다. 응용 프로그램의 현재 HttpRequest 브라우저 속성을 통해 브라우저 기능을 액세스할 수 있습니다.

Aspnet를 실행 하는 경우 다음 옵션을 사용할 수 있는\_regbrowser.exe:

| **옵션** | **설명** |
| --- | --- |
| **-?** | Aspnet 표시\_regbbrowsers.exe 명령 창에서 도움말 텍스트입니다. |
| **-i** | 브라우저 기능 런타임 어셈블리를 만들고 전역 어셈블리 캐시에 설치 합니다. |
| **-u** | 전역 어셈블리 캐시에서 브라우저 기능 런타임 어셈블리를 제거합니다. |

## <a name="the-aspnet-compilation-tool---aspnetcompilerexe"></a>ASP.NET 컴파일 도구-aspnet\_compiler.exe

일반적인 두 가지 방법으로 ASP.NET 컴파일 도구를 사용할 수 있습니다: 전체 컴파일 및 배포를 대상 출력 디렉터리를 지정 되는 위치에 대 한 컴파일.

### <a name="compiling-an-application-in-placehttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[현재 위치에서 응용 프로그램 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET 컴파일 도구 위치에서 응용 프로그램을 컴파일할 수, 따라서 일반적인 컴파일을 일으키는 응용 프로그램에 대 한 여러 요청의 동작을 모방 하는, 합니다. 미리 컴파일된 사이트의 사용자는 첫 번째 요청에서 페이지 컴파일로 인 한 지연을 발생 하지 않습니다.

내부에서 사이트를 미리 컴파일할 경우에 다음 항목이 적용 됩니다.

- 사이트의 파일 및 디렉터리 구조를 유지합니다.
- 사이트 서버에 사용 된 모든 프로그래밍 언어에 대 한 컴파일러 있어야 합니다.
- 컴파일 실패 한 파일이 있을 경우 전체 사이트 컴파일이 실패 합니다.

또한 새 소스 파일을 추가한 후 위치에서 응용 프로그램을 다시 컴파일할 수 있습니다. 도구를 포함 하지 않으면 새롭거나 변경 된 파일만 컴파일합니다 합니다 **-c** 옵션입니다.

> [!NOTE]
> 중첩 된 응용 프로그램을 포함 하는 응용 프로그램의 컴파일 중첩된 된 응용 프로그램을 컴파일되지 않습니다. 중첩된 된 응용 프로그램을 개별적으로 컴파일된 수 있어야 합니다.


### <a name="compiling-an-application-for-deploymenthttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[배포에 대 한 응용 프로그램 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

TargetDir 매개 변수를 지정 하 여 배포 (대상 위치로 컴파일)에 대 한 응용 프로그램을 컴파일합니다. TargetDir 웹 응용 프로그램에 대 한 최종 위치 수 또는 컴파일된 응용 프로그램을 다시 배포할 수도 있습니다. 사용 하는 **-u** 옵션을 변경할 수 있습니다 컴파일된 응용 프로그램에서 특정 파일에 다시 컴파일하지 않고 하는 방식으로 응용 프로그램을 컴파일하고 있습니다. Aspnet\_compiler.exe 정적 및 동적 파일 유형과 구분 작업을 수행 하 고 응용 프로그램을 만들 때 다른 방식으로 처리 합니다.

- 정적 파일 형식은 연결는 컴파일러가 하지 않거나 해당 파일을 같은 공급자 빌드를 하는 명명 된.css,.gif,.htm,.html,.jpg,.js와 같은 확장 등에 있어야 합니다. 이러한 파일은 단순히 유지 디렉터리 구조에서의 상대적 위치를 사용 하 여 대상 위치에 복사 됩니다.
- 동적 파일 유형은 연결된 컴파일러를 했거나.asax,.ascx,.ashx,.aspx,.browser,.master 등 ASP.NET 고유의 파일 이름 확장명을 사용 하 여 파일을 비롯 하 여 공급자를 작성 하는입니다. ASP.NET 컴파일 도구는 이러한 파일에서 어셈블리를 생성합니다. 경우는 **-u** 옵션을 생략 하면, 도구도 파일 이름 확장명을 사용 하 여 파일을 만듭니다. 원래 원본 파일은 어셈블리에 매핑되는 COMPILED 합니다. 을 보장 하기 위해 응용 프로그램 원본의 디렉터리 구조가 유지 되는 도구는 대상 응용 프로그램의 해당 위치에 자리 표시자 파일을 생성 합니다.

사용 해야 합니다 **-u** 컴파일된 응용 프로그램의 콘텐츠를 수정 될 수 있음을 나타내려면이 옵션을 합니다. 이 고, 그렇지 이후 수정 내용은 무시 됩니다 또는 런타임 오류가 발생 합니다.

다음 표에서 설명 하는 방법을 ASP.NET 컴파일 도구 핸들 다른 파일 형식의 경우 합니다 **-u** 옵션이 포함 됩니다.

| **파일 형식** | **컴파일러 동작** |
| --- | --- |
| .ascx, .aspx, .master | 이러한 파일은 코드 숨김 파일 및에 포함 된 모든 코드를 모두 포함 하는 태그 및 소스 코드를 분할할 &lt;스크립트 runat = "server"&gt; 요소입니다. 소스 코드 이름이 해싱 알고리즘을에서 파생 되는 어셈블리로 컴파일하고 어셈블리를 Bin 디렉터리에 배치 됩니다. 모든 인라인 코드, 즉, 묶인 코드를 **&lt; %** 하 고 **% &gt;** 대괄호, 태그로 포함 되어 있으며 컴파일되지 않습니다. 소스 파일과 동일한 이름의 새 파일 태그를 포함 하도록 생성 되 고 해당 출력 디렉터리에 배치 합니다. |
| .ashx, .asmx | 이러한 파일은 컴파일되지 않습니다 및 고 컴파일되지 출력 디렉터리로 이동 됩니다. 컴파일된 처리기 코드를 포함 하려는 경우 앱의 소스 코드 파일에 코드를 배치\_코드 디렉터리입니다. |
| .cs,.vb,.jsl,.cpp (앞에 나열 된 파일 형식에 대 한 코드 숨김 파일 제외) | 이러한 파일이 컴파일되고 참조 하는 어셈블리에 리소스로 포함 됩니다. 소스 파일을 출력 디렉터리에 복사 되지 않습니다. 코드 파일을 참조 하지 않는 경우 컴파일되지 않습니다. |
| 사용자 지정 파일 형식 | 이러한 파일을 컴파일되지 않습니다. 이러한 파일은 해당 출력 디렉터리에 복사 됩니다. |
| 앱의 코드 파일을 원본\_코드 하위 디렉터리 | 이러한 파일 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. |
| 앱에서.resx 및.resource 파일\_GlobalResources 하위 디렉터리 | 이러한 파일 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 앱 없음\_GlobalResources 하위 디렉터리 주 출력 디렉터리에 생성 되 고 원본 디렉터리에.resx 또는.resources 파일이 출력 디렉터리에 복사 됩니다. |
| 앱에서.resx 및.resource 파일\_LocalResources 하위 디렉터리 | 이러한 파일은 컴파일되지 않습니다 하 고 해당 출력 디렉터리에 복사 됩니다. |
| 앱의.skin 파일\_테마 하위 디렉터리 | .Skin 파일 및 정적 테마 파일에 컴파일되지 않은 하 고 해당 출력 디렉터리에 복사 됩니다. |
| .browser Web.config 정적 파일 형식 Bin 디렉터리에 이미 있는 어셈블리 | 이러한 파일은 출력 디렉터리에 있는 그대로 복사 됩니다. |

다음 표에서 설명 하는 방법을 ASP.NET 컴파일 도구 핸들 다른 파일 형식의 경우 합니다 **-u** 옵션을 생략 하면 됩니다.

| **파일 형식** | **컴파일러 동작** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | 이러한 파일은 코드 숨김 파일 및에 포함 된 모든 코드를 모두 포함 하는 태그 및 소스 코드를 분할할 &lt;스크립트 runat = "server"&gt; 요소입니다. 소스 코드 이름이 해싱 알고리즘에서 파생 되는 어셈블리로 컴파일됩니다. 결과 어셈블리를 Bin 디렉터리에 배치 됩니다. 모든 인라인 코드, 즉, 묶인 코드를 **&lt; %** 하 고 **% &gt;** 대괄호, 태그로 포함 되어 있으며 컴파일되지 않습니다. 컴파일러는 소스 파일과 동일한 이름의 태그를 포함할 새 파일을 만듭니다. 이러한 결과 파일이 Bin 디렉터리에 배치 됩니다. 또한 컴파일러가 소스 파일과 이름이 같지만 확장 파일을 만듭니다. 매핑 정보를 포함 하는 COMPILED 합니다. 합니다. 컴파일된 파일은 소스 파일의 원래 위치에 해당 하는 출력 디렉터리에 배치 됩니다. |
| .ascx | 이러한 파일은 태그 및 소스 코드에 분할 됩니다. 소스 코드를 어셈블리로 컴파일되고 이름이 해싱 알고리즘에서 파생 되는 Bin 디렉터리에 배치 됩니다. 태그 파일이 생성 됩니다. |
| .cs,.vb,.jsl,.cpp (앞에 나열 된 파일 형식에 대 한 코드 숨김 파일 제외) | .Ascx,.ashx 또는.aspx 파일에서 생성 된 어셈블리에서 참조 되는 소스 코드를 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 원본 파일이 복사 됩니다. |
| 사용자 지정 파일 형식 | 이러한 파일은 동적 파일 처럼 컴파일됩니다. 기반으로 하는 파일의 형식에 따라 컴파일러는 출력 디렉터리에 매핑 파일을 배치할 수 있습니다. |
| 앱의 파일\_코드 하위 디렉터리 | 이 하위 디렉터리에 소스 코드 파일 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. |
| 앱의 파일\_GlobalResources 하위 디렉터리 | 이러한 파일 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 앱 없음\_GlobalResources 하위 디렉터리 주 출력 디렉터리 아래에 생성 됩니다. 구성 파일 appliesTo를 지정 하는 경우 = "All".resx 및.resources 파일이 출력 디렉터리에 복사 됩니다. 참조 하는 경우 복사 되지 않습니다는 [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)합니다. |
| 앱에서.resx 및.resource 파일\_LocalResources 하위 디렉터리 | 두이 파일은 고유한 이름 가진 어셈블리에 컴파일됩니다를 Bin 디렉터리에 배치 합니다. .Resx 또는.resource 파일이 출력 디렉터리에 복사 됩니다. |
| 앱의.skin 파일\_테마 하위 디렉터리 | 테마 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 스텁 파일.skin 파일에 대해 생성 되 고 해당 출력 디렉터리에 배치 합니다. 정적 파일 (예:.css) 출력 디렉터리에 복사 됩니다. |
| .browser Web.config 정적 파일 형식 Bin 디렉터리에 이미 있는 어셈블리 | 이러한 파일은 출력 디렉터리에 있는 그대로 복사 됩니다. |

### <a name="fixed-assembly-nameshttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[고정된 어셈블리 이름](https://msdn.microsoft.com/library/ms229863.aspx##)

MSI Windows Installer를 사용 하 여 웹 응용 프로그램을 배포 하는 등의 일부 시나리오에는 어셈블리 또는 업데이트에 대 한 구성 설정을 확인 하는 일관 된 디렉터리 구조 뿐만 아니라 일관 된 파일 이름 및 콘텐츠를 사용을 해야 합니다. 이러한 경우에 사용할 수 있습니다 합니다 **-fixednames** ASP.NET 컴파일 도구 어셈블리로 컴파일해야를 지정 하는 옵션 where를 사용 하는 대신 각 소스 파일에 대 한 여러 페이지 어셈블리로 컴파일됩니다. 이 확장성을 사용 하 여 우려되는 경우 주의 해 서이 옵션을 사용 해야 하므로 많은 수의 어셈블리에 발생할 수 있습니다.

### <a name="strong-name-compilationhttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[강력한 이름 컴파일](https://msdn.microsoft.com/library/ms229863.aspx##)

**aptca**, **-delaysign**를 **-keycontainer** 하 고 **-keyfile** Aspnet를 사용할 수 있도록 옵션이 제공 됩니다\_ 사용 하지 않고 compiler.exe 만드는 강력한 이름의 어셈블리를 [강력한 이름 도구 (Sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) 개별적으로 합니다. 이들이 옵션 각각 해당를 **AllowPartiallyTrustedCallersAttribute**, **AssemblyDelaySignAttribute**하십시오 **AssemblyKeyNameAttribute**, 및  **AssemblyKeyFileAttribute**합니다.

이러한 특성 설명은이 과정의 범위를 벗어납니다.

## <a name="labs"></a>Labs

다음 랩 각 이전 실습실에 작성합니다. 순서 대로 수행 해야 합니다.

## <a name="lab-1-using-the-configuration-api"></a>랩 1: 구성 API 사용

1. 라는 새 웹 사이트를 만들 *mod9lab*합니다.
2. 새 웹 구성 파일을 사이트에 추가 합니다.
3. Web.config 파일에 다음을 추가 합니다.


[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

이렇게 하면 web.config 파일에 변경 내용을 저장할 수 있는 권한이 있다고 합니다.

1. Default.aspx로 새 레이블 컨트롤을 추가 하 고 ID를 변경 **lblDebugStatus**합니다.
2. Default.aspx로 새 단추 컨트롤을 추가 합니다.
3. 단추 컨트롤의 ID를 변경 **btnToggleDebug** 및 텍스트 **디버그 상태 설정/해제**합니다.
4. Default.aspx의 코드 숨김 파일에 대 한 코드 보기를 열고 추가 된 **를 사용 하 여** 문을 **System.Web.Configuration** 같이:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 클래스와이 페이지를 두 개의 private 변수를 추가\_아래와 같이 Init 메서드:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 페이지에 다음 코드를 추가\_부하:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 저장 하 고 default.aspx를 찾습니다. 레이블 컨트롤에 현재 디버그 상태를 표시 되는지 확인 합니다.
2. 디자이너에서 단추 컨트롤을 두 번 누릅니다 하 고 단추 컨트롤에 대 한 클릭 이벤트에 다음 코드를 추가 합니다.


[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 저장 하 고 default.aspx 찾아보기 단추를 클릭 합니다.
2. 각 단추 클릭 하 고 확인 한 후 web.config 파일을 엽니다는 **디버그** 특성을 &lt;컴파일&gt; 섹션입니다.

## <a name="lab-2-logging-application-restarts"></a>랩 2: 로깅 응용 프로그램 다시 시작

이 실습에서는 응용 프로그램 종료, 신생 업체 및 다시 컴파일 이벤트 뷰어에서 로깅을 설정/해제할 수 있도록 해 주는 코드를 만들게 됩니다.

1. Default.aspx로 DropDownList를 추가 하 고 ID ddlLogAppEvents로 변경 합니다.
2. 설정 된 **AutoPostBack** DropDownList 속성 **true**합니다.
3. DropDownList에 대 한 항목 컬렉션에 세 개의 항목을 추가 합니다. 확인 합니다 **텍스트** 첫 번째 항목에 대 한 *Select Value* 값-1입니다. 확인 합니다 **텍스트** 하 고 **값** 두 번째 항목의 **True** 하며 **텍스트** 및 **값** 세 번째 항목의 **False**합니다.
4. Default.aspx에 새 레이블을 추가 합니다. ID를 변경 **lblLogAppEvents**합니다.
5. Default.aspx에 대 한 코드 숨김 보기를 열고 아래와 같이 HealthMonitoringSection 형식의 변수에 대 한 새 선언을 추가 합니다.


[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 다음 코드 페이지에서 기존 코드를 추가\_Init:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. DropDownList 두 번 클릭을 SelectedIndexChanged 이벤트에 다음 코드를 추가 합니다.


[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Default.aspx를 찾습니다.
2. 드롭다운으로 **False**합니다.
3. 이벤트 뷰어에서 응용 프로그램 로그를 지웁니다.
4. 응용 프로그램에 대 한 디버그 특성을 변경 하려면 단추를 클릭 합니다.
5. 이벤트 뷰어에서 응용 프로그램 로그를 새로 고칩니다. 

    1. 모든 이벤트가 기록 된?
    2. 이유 또는 없습니까?
6. 드롭다운으로 **True입니다.**
7. 응용 프로그램에 대 한 디버그 특성을 설정/해제 단추를 클릭 합니다.
8. 응용 프로그램 로그인을 이벤트 뷰어를 새로 고칩니다. 

    1. 모든 이벤트가 기록 된?
    2. 앱 종료 이유는 무엇 이었습니까?
9. 켜기 및 로깅을 해제를 사용 하 여 실험 하 및 web.config 파일에 대 한 변경 내용을 확인 합니다.

## <a name="more-information"></a>자세한 정보:

ASP.NET 2.0의 공급자 모델을 사용 하면 다양 한 용도 멤버 자격, 프로필 등 대해서 뿐만 아니라 응용 프로그램 계측을 위해 사용자 고유의 공급자를 만들 수 있습니다. 텍스트 파일에 응용 프로그램 이벤트 로그에 사용자 지정 공급자 작성에 대 한 자세한 내용은 방문 [이 링크](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)합니다.
