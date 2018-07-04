---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
title: 보호 하는 연결 문자열 및 기타 구성 정보 (C#) | Microsoft Docs
author: rick-anderson
description: 일반적으로 ASP.NET 응용 프로그램 Web.config 파일에서 구성 정보를 저장 합니다. 이 정보 중 일부 중요 한 및 보호를 보장 합니다. 규정...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/03/2007
ms.topic: article
ms.assetid: ad8dd396-30f7-4abe-ac02-a0b84422e5be
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
msc.type: authoredcontent
ms.openlocfilehash: e5ce4459a1b62fe851ce8a4cae50aed798f0d508
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378977"
---
<a name="protecting-connection-strings-and-other-configuration-information-c"></a>연결 문자열 및 기타 구성 정보 (C#)를 보호합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_CS.zip) 또는 [PDF 다운로드](protecting-connection-strings-and-other-configuration-information-cs/_static/datatutorial73cs1.pdf)

> 일반적으로 ASP.NET 응용 프로그램 Web.config 파일에서 구성 정보를 저장 합니다. 이 정보 중 일부 중요 한 및 보호를 보장 합니다. 기본적으로이 파일 제공 되지 않으므로 웹 사이트 방문자에 게 하지만 관리자 또는 해커가 웹 서버의 파일 시스템에 액세스 하 고 파일의 내용을 볼 수 있습니다. 이 자습서에서는 ASP.NET 2.0에서는 Web.config 파일의 섹션을 암호화 하 여 중요 한 정보를 보호 하기는 알아봅니다.


## <a name="introduction"></a>소개

ASP.NET 응용 프로그램에 대 한 구성 정보는 일반적으로 라는 XML 파일에 저장 됩니다 `Web.config`합니다. 이 자습서의 과정을 통해 업데이트를 `Web.config` 몇 번의 합니다. 만들 때를 `Northwind` 형식화 된 데이터 집합에는 [첫 번째 자습서](../introduction/creating-a-data-access-layer-cs.md), 예를 들어 연결 문자열 정보를 자동으로 추가 되었습니다 `Web.config` 에 `<connectionStrings>` 섹션. 나중에 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서는 수동으로 업데이트 `Web.config`추가는 `<pages>` 요소는 모든 프로젝트에 ASP.NET 페이지를 사용 해야 함을 나타내는 `DataWebControls` 테마입니다.

이후 `Web.config` 연결 문자열과 같은 중요 한 데이터를 포함할 수 것이 중요 하는 내용의 `Web.config` 안전 하 고 무단 뷰어에서 숨겨진 유지 합니다. 기본적으로 사용 하 여 파일에 HTTP 요청는 `.config` 확장 반환 하는 ASP.NET 엔진에 의해 처리 되는 *이런이 종류의 페이지를 제공 하지는* 그림 1에 표시 되는 메시지입니다. 즉, 방문자가 볼 수 없습니다 하 `Web.config` 파일 s 콘텐츠를 입력 하 여 간단히 http://www.YourServer.com/Web.config 해당 s 브라우저 주소 표시줄에 있습니다.


[![메시지를 제공 하지는 Web.config를 통해는 브라우저 반환 페이지의 입력이 방문](protecting-connection-strings-and-other-configuration-information-cs/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image1.png)

**그림 1**: 방문 `Web.config` 를 통해는 브라우저 반환이 페이지의 입력 메시지를 제공 하지는 ([클릭 하 여 큰 이미지 보기](protecting-connection-strings-and-other-configuration-information-cs/_static/image3.png))


그렇다면 공격자가 볼 수 있는 몇 가지 다른 악용을 찾을 수 있지만 프로그램 `Web.config` 파일 s 콘텐츠? 수는 공격자가 할 일이 정보를 사용 하 여 및 단계 내에서 중요 한 정보 보호를 강화 하기 위해 사용할 수 `Web.config`? 다행 스럽게도 대부분의 섹션에서 `Web.config` 중요 한 정보가 포함 되지 않습니다. 어떤 피해 수 공격자를 저지르는 기본 사용 되는 ASP.NET 페이지 테마의 이름을 알고 있는 경우?

그러나 특정 `Web.config` 섹션 연결 문자열, 사용자 이름, 암호, 서버 이름, 암호화 키 등을 포함할 수 있는 중요 한 정보를 포함 합니다. 이 정보는 일반적으로 다음 있는 `Web.config` 섹션:

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

이 자습서에서 이러한 중요 한 구성 정보를 보호 하는 기술을 살펴보겠습니다. 잘 알다시피 간편해 집니다를 프로그래밍 방식으로 암호화 및 암호 해독에 해당 하는 선택한 구성의 섹션에는 보호 된 구성 시스템을.NET Framework 버전 2.0에 포함 됩니다.

> [!NOTE]
> 이 자습서는 ASP.NET 응용 프로그램에서 데이터베이스에 연결 하기 위한 권장의 살펴보겠습니다 포함 되어 있습니다. 연결 문자열을 암호화 하는 것 외에도 강화 함으로써 안전 하 게에서 데이터베이스에 연결 하는 시스템을 보호할 수 있습니다.


## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>1 단계: ASP.NET 2.0 탐색 s 보호 구성 옵션

ASP.NET 2.0에는 암호화 및 해독 구성 정보에 대 한 보호 되는 구성 시스템을 포함 합니다. 프로그래밍 방식으로 암호화 또는 구성 정보를 암호 해독에 사용할 수 있는.NET Framework의 메서드가 포함 됩니다. 보호 되는 구성 시스템에서 사용 하는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 개발자가 어떤 암호화 구현에는 선택할 수 있습니다.

.NET Framework는 두 명의 보호 되는 구성 공급자를 사용 하 여 제공 됩니다.

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) -사용 된 비대칭 [RSA 알고리즘](http://en.wikipedia.org/wiki/Rsa) 암호화 및 암호 해독 합니다.
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) -Windows를 사용 하 여 [데이터 보호 API (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx) 암호화 및 암호 해독 합니다.

공급자 디자인 패턴을 구현 하는 보호 되는 구성 시스템 이므로 고유한 보호 되는 구성 공급자를 만들고 응용 프로그램에 연결할 수 있습니다. 참조 [보호 된 구성 공급자를 구현](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx) 이 프로세스에 대 한 자세한 내용은 합니다.

DPAPI 및 RSA 공급자가 암호화 및 암호 해독 루틴에 대 한 키를 사용 하 고 이러한 키에는 컴퓨터 또는 사용자 수준을 저장할 수 있습니다. 컴퓨터 수준 키가 웹 응용 프로그램 자체의 전용된 서버에서 실행 되는 시나리오에 적합 하거나 공유 해야 하는 서버에서 여러 응용 프로그램이 있는 경우 정보를 암호화 합니다. 사용자 수준 키가 없는 동일한 서버의 다른 응용 프로그램에 응용 프로그램 보호 s 구성 섹션을 암호 해독 하는 일을 할 수 해야 하는 공유 호스팅 환경에서 보다 안전한 옵션입니다.

이 자습서의 예제는 DPAPI 공급자 및 컴퓨터 수준 키를 사용 합니다. 암호화 살펴보겠습니다 특히를 `<connectionStrings>` 단원의 `Web.config`보호 되는 구성 시스템을 하나 대부분의 암호화를 사용할 수 있지만, `Web.config` 섹션. 사용자 수준 키를 사용 하 여 또는 RSA 공급자를 사용 하 여에 대 한 내용은이 자습서의 끝에 추가 정보 섹션의 리소스를 참조 하세요.

> [!NOTE]
> `RSAProtectedConfigurationProvider` 하 고 `DPAPIProtectedConfigurationProvider` 공급자에 등록 된 합니다 `machine.config` 공급자 이름 사용 하 여 파일 `RsaProtectedConfigurationProvider` 및 `DataProtectionConfigurationProvider`각각. 암호화 하거나 적절 한 공급자 이름을 제공 해야 하는 구성 정보를 해독 하는 경우 (`RsaProtectedConfigurationProvider` 또는 `DataProtectionConfigurationProvider`) 실제 형식 이름 대신 (`RSAProtectedConfigurationProvider` 고 `DPAPIProtectedConfigurationProvider`). 찾을 수 있습니다 합니다 `machine.config` 파일을 `$WINDOWS$\Microsoft.NET\Framework\version\CONFIG` 폴더입니다.


## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>2 단계: 프로그래밍 방식으로 암호화 하 고 구성 섹션을 암호 해독

몇 줄의 코드를 사용 하 여 암호화 또는 지정된 된 공급자를 사용 하 여 특정 구성 섹션을 암호를 해독할 수 있습니다. 코드를 곧 확인할 수 있듯이 하기만 프로그래밍 방식으로 적절 한 구성 섹션을 참조 하도록 호출 해당 `ProtectSection` 또는 `UnprotectSection` 메서드를 호출한 다음는 `Save` 변경 내용을 유지 하는 방법입니다. 또한.NET Framework 암호화 하 고 구성 정보를 해독할 수 있는 유용한 명령줄 유틸리티를 포함 합니다. 3 단계에서에서이 명령줄 유틸리티를 살펴봅니다.

S를 통해 프로그래밍 방식으로 보호 구성 정보를 보여 주기 위해 암호화 및 암호 해독에 대 한 단추를 포함 하는 ASP.NET 페이지를 만듭니다는 `<connectionStrings>` 단원의 `Web.config`합니다.

열어서 시작 합니다 `EncryptingConfigSections.aspx` 페이지에 `AdvancedDAL` 폴더입니다. 설정 디자이너 도구 상자에서 텍스트 상자 컨트롤을 끌어 해당 `ID` 속성을 `WebConfigContents`, 해당 `TextMode` 속성을 `MultiLine`, 및 해당 `Width` 고 `Rows` 95%와 15 속성 각각. 이 텍스트 상자 컨트롤의 내용을 표시 합니다 `Web.config` 를 신속 하 게 하는 경우 콘텐츠는 암호화 여부를 볼 수 있습니다. 물론 실제 응용 프로그램에서은 하지 않으려는의 내용을 표시 하려면 `Web.config`합니다.

텍스트 상자 아래에 라는 두 개의 단추 컨트롤을 추가 `EncryptConnStrings` 고 `DecryptConnStrings`입니다. 연결 문자열 암호화 및 암호를 해독 하는 연결 문자열에 해당 텍스트 속성을 설정 합니다.

이 시점에서 화면은 그림 2와 비슷하게 표시 됩니다.


[![페이지에 텍스트 상자와 두 개의 단추 웹 컨트롤 추가](protecting-connection-strings-and-other-configuration-information-cs/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image4.png)

**그림 2**: 페이지에 텍스트 상자 및 두 개의 단추 웹 컨트롤 추가 ([큰 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-cs/_static/image6.png))


다음으로 로드 하 고의 내용을 표시 하는 코드를 작성 해야 `Web.config` 에 `WebConfigContents` 페이지가 있는 경우 첫 번째 텍스트 상자에 로드 합니다. 페이지의 코드 숨김 클래스에 다음 코드를 추가 합니다. 이 코드는 메서드를 추가 `DisplayWebConfig` 에서 호출 합니다 `Page_Load` 이벤트 처리기 때 `Page.IsPostBack` 는 `false`:


[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample1.cs)]

`DisplayWebConfig` 메서드를 [ `File` 클래스](https://msdn.microsoft.com/library/system.io.file.aspx) 하 여 응용 프로그램을 엽니다 `Web.config` 파일을 [ `StreamReader` 클래스](https://msdn.microsoft.com/library/system.io.streamreader.aspx) 문자열과 합니다 내용을읽어[ `Path` 클래스](https://msdn.microsoft.com/library/system.io.path.aspx) 실제 경로를 생성 하는 `Web.config` 파일입니다. 이러한 세 클래스 모두에서 발견 되는 [ `System.IO` 네임 스페이스](https://msdn.microsoft.com/library/system.io.aspx)합니다. 결과적으로 추가 해야 합니다는 `using` `System.IO` 코드 숨김 클래스를, 또는 이러한 클래스 이름의 접두사의 맨 위에 문을 `System.IO.` 합니다.

다음으로 두 개의 단추 컨트롤에 대 한 이벤트 처리기를 추가 해야 `Click` 이벤트 암호화 및 해독 하는 데 필요한 코드를 추가 하 고는 `<connectionStrings>` DPAPI 공급자를 사용 하 여 컴퓨터 수준 키를 사용 하 여 섹션입니다. 디자이너에서 각 두 번 클릭 추가 하는 단추는 `Click` 코드 숨김에서 이벤트 처리기 클래스 및 다음 코드를 추가 합니다.


[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample2.cs)]

두 개의 이벤트 처리기에서 사용 되는 코드는 거의 동일 합니다. 현재 응용 프로그램 s에 대 한 정보를 가져와서 시작 둘 `Web.config` 를 통해 파일을 [ `WebConfigurationManager` 클래스](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx) s [ `OpenWebConfiguration` 메서드](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)합니다. 이 메서드는 지정된 된 가상 경로 대 한 웹 구성 파일을 반환합니다. 다음으로 `Web.config` s 파일 `<connectionStrings>` 섹션을 통해 액세스를 [ `Configuration` 클래스](https://msdn.microsoft.com/library/system.configuration.configuration.aspx) s [ `GetSection(sectionName)` 메서드](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx)를 반환 하는 [ `ConfigurationSection` ](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx) 개체입니다.

합니다 `ConfigurationSection` 개체에 포함을 [ `SectionInformation` 속성](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx) 추가 정보 및 구성 섹션에 대 한 기능을 제공 하는 합니다. 구성 섹션을 확인 하 여 암호화 되는지 여부를 확인할 수 있습니다 위의 코드로 합니다 `SectionInformation` s 속성 `IsProtected` 속성입니다. 섹션 수 암호화 하거나 해독할 통해 또한 합니다 `SectionInformation` s 속성 `ProtectSection(provider)` 고 `UnprotectSection` 메서드.

`ProtectSection(provider)` 메서드를 암호화할 때 사용 하 여 보호 되는 구성 공급자의 이름을 지정 하는 문자열 입력으로 받아들입니다. 에 `EncryptConnString` DataProtectionConfigurationProvider에 전달 하는 s 단추 이벤트 처리기는 `ProtectSection(provider)` 메서드 DPAPI 공급자가 사용 되도록 합니다. `UnprotectSection` 메서드는 구성 섹션 암호화에 사용 된 하 고 따라서 필요 하지 않습니다 모든 입력 매개 변수는 공급자를 확인할 수 있습니다.

호출한 후 합니다 `ProtectSection(provider)` 또는 `UnprotectSection` 호출 해야 합니다는 `Configuration` s 개체 [ `Save` 메서드](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx) 의 변경 사항을 유지 합니다. 호출 변경 내용을 저장 하 고 구성 정보 암호화 되거나 해독 `DisplayWebConfig` 업데이트 된 로드 `Web.config` TextBox 컨트롤에 대 한 콘텐츠.

위의 코드를 입력 하 고 나면 방문 하 여 테스트를 `EncryptingConfigSections.aspx` 브라우저를 통해 페이지입니다. 내용을 나열 하는 페이지를 처음에 표시 됩니다 `Web.config` 사용 하 여는 `<connectionStrings>` 일반 텍스트에 표시 된 섹션 (그림 3 참조).


[![페이지에 텍스트 상자와 두 개의 단추 웹 컨트롤 추가](protecting-connection-strings-and-other-configuration-information-cs/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image7.png)

**그림 3**: 페이지에 텍스트 상자 및 두 개의 단추 웹 컨트롤 추가 ([큰 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-cs/_static/image9.png))


이제 연결 문자열 암호화 단추를 클릭 합니다. 요청 유효성 검사를 사용 하는 경우 태그에서 다시 게시 합니다 `WebConfigContents` 텍스트 상자에 생성 됩니다는 `HttpRequestValidationException`, 잠재적으로 위험한 메시지를 표시 하는 `Request.Form` 값이 클라이언트에서 발견 되었습니다. ASP.NET 2.0에서 기본적으로 사용 되는 요청 유효성 검사를 포스트백 인코딩되지 않은 HTML을 포함 하는 것을 금지 하 고 스크립트 삽입 공격을 방지 하도록 설계 되었습니다. 이 검사에는 페이지 또는 응용 프로그램 수준 비활성화할 수 있습니다. 하지 않으려면이 페이지를 설정 합니다 `ValidateRequest` 로 설정 `false` 에서 `@Page` 지시문입니다. `@Page` 지시문의 페이지 s 선언적 태그의 맨 위에 위치 합니다.


[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample3.aspx)]

요청 유효성 검사, 용도 대 한 자세한 내용은 참조에 페이지 및 응용 프로그램 수준, 방법과 html 태그를 인코딩할 때 사용 하지 않도록 하는 방법 [요청 유효성 검사-스크립트 공격 방지](../../../../whitepapers/request-validation.md)합니다.

페이지에 대 한 요청 유효성 검사를 해제 한 후 연결 문자열 암호화 단추를 다시 클릭 하십시오. 포스트백에서 구성 파일에 액세스할 수는 고 `<connectionStrings>` 섹션 DPAPI 공급자를 사용 하 여 암호화 합니다. 새 표시할 입력란 그런 `Web.config` 콘텐츠입니다. 그림 4에서 알 수 있듯이는 `<connectionStrings>` 정보는 이제 암호화 합니다.


[![암호화 연결 문자열 단추 암호화를 클릭 하 여 &lt;connectionString&gt; 섹션](protecting-connection-strings-and-other-configuration-information-cs/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image10.png)

**그림 4**:는 암호화 연결 문자열 단추 암호화를 클릭 하 여 `<connectionString>` 섹션 ([클릭 하 여 큰 이미지 보기](protecting-connection-strings-and-other-configuration-information-cs/_static/image12.png))


암호화 `<connectionStrings>` 있지만 콘텐츠의 일부 섹션 내 컴퓨터에 생성 된 뒤의 `<CipherData>` 요소 간 결함을 위해 제거 되었습니다:


[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample4.xml)]

> [!NOTE]
> 합니다 `<connectionStrings>` 요소를 암호화 하는 데 사용 되는 공급자를 지정 합니다 (`DataProtectionConfigurationProvider`). 이 정보를 사용 하 여는 `UnprotectSection` 메서드는 연결 문자열 암호를 해독 단추를 클릭할 때입니다.


연결 문자열 정보를 액세스 하는 경우 `Web.config` -역시에서 SqlDataSource 컨트롤을 작성 하는 코드 또는 형식화 된 데이터 집합에서 TableAdapters에서 자동으로 생성 된 코드를 자동으로 해독 됩니다. 즉, 우리가 필요가 없습니다 추가 코드 또는 암호화 된 암호를 해독 하는 논리를 추가 하려면 `<connectionString>` 섹션입니다. 이 보여 주기 위해 이전 자습서 중 하나에 방문의 기본 보고 섹션에서 간단한 표시 자습서 등이 시간 (`~/BasicReporting/SimpleDisplay.aspx`). 그림 5에서 알 수 있듯이, 정확히 의도 한 대로, 암호화 된 연결 문자열 정보는 ASP.NET 페이지에서 자동으로 해독 되 고 나타내는 자습서 작동 합니다.


[![연결 문자열 정보를 자동으로 해독 하는 데이터 액세스 계층](protecting-connection-strings-and-other-configuration-information-cs/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image13.png)

**그림 5**: 연결 문자열 정보를 자동으로 해독 하는 데이터 액세스 계층 ([큰 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-cs/_static/image15.png))


되돌리려면는 `<connectionStrings>` 일반 텍스트 표현으로 다시 섹션에서 연결 문자열 암호를 해독 단추를 클릭 합니다. 포스트백 될 때의 연결 문자열을 표시 해야 `Web.config` 일반 텍스트에서입니다. 이 시점에서이 페이지 (그림 3 참조)를 처음 방문할 때 수행한 것과 같은 화면이 표시 됩니다.

## <a name="step-3-encrypting-configuration-sections-usingaspnetregiisexe"></a>3 단계: 암호화를 사용 하 여 구성 섹션`aspnet_regiis.exe`

.NET Framework는 다양 한 명령줄 도구에는 `$WINDOWS$\Microsoft.NET\Framework\version\` 폴더입니다. 에 [SQL 캐시 종속성 사용 하 여](../caching-data/using-sql-cache-dependencies-cs.md) 자습서에서는 예를 들어 살펴보았습니다를 사용 하 여는 `aspnet_regsql.exe` SQL 캐시 종속성에 필요한 인프라를 추가 하려면 명령줄 도구입니다. 이 폴더에 있는 다른 유용한 명령줄 도구를 [ASP.NET IIS Registration tool (`aspnet_regiis.exe`)](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx)합니다. 이름에서 알 수 있듯이 Microsoft의 전문적인 수준의 웹 서버, IIS와 ASP.NET 2.0 응용 프로그램을 등록 ASP.NET IIS 등록 도구를 주로 사용 됩니다. IIS 관련 기능 외에도 ASP.NET IIS 등록 도구를 사용할 수도 있습니다에 지정 된 구성 섹션을 암호 해독 또는 암호화 `Web.config`합니다.

다음 문을 사용 하 여 구성 섹션을 암호화 하는 데 일반 구문을 보여 줍니다는 `aspnet_regiis.exe` 명령줄 도구:


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample5.cmd)]

*섹션* (예: connectionStrings)를 암호화 하는 구성 섹션은 합니다 *물리적\_디렉터리* 웹 응용 프로그램의 루트 디렉터리의 완전 한 실제 경로 및 *공급자*  (예: DataProtectionConfigurationProvider) 사용 하 여 보호 되는 구성 공급자의 이름입니다. 또는 웹 응용 프로그램은 IIS에 등록 하는 경우에 다음 구문을 사용 하 여 실제 경로 대신 가상 경로 입력할 수 있습니다.


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample6.cmd)]

다음 `aspnet_regiis.exe` 예제에서는 암호화는 `<connectionStrings>` DPAPI 공급자를 사용 하 여 컴퓨터 수준 키를 사용 하 여 섹션:


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample7.cmd)]

마찬가지로,는 `aspnet_regiis.exe` 명령줄 도구를 구성 섹션을 해독에 사용할 수 있습니다. 사용 하는 대신 합니다 `-pef` 스위치를 사용 하 여 `-pdf` (또는 instead of `-pe`를 사용 하 여 `-pd`). 또한 않음을 유의 공급자 이름을 필요한 암호를 해독 하는 경우.


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample8.cmd)]

> [!NOTE]
> 실행 해야 컴퓨터에 특정 키를 사용 하는 DPAPI 공급자를 사용 하 고 있으므로 `aspnet_regiis.exe` 같은 컴퓨터에서 웹 페이지를 처리 하는 데 사용 되는입니다. 예를 들어, 로컬 개발 컴퓨터에서이 명령줄 프로그램을 실행 하 고 프로덕션 서버에 암호화 된 Web.config 파일을 업로드 한 다음 프로덕션 서버 없게 됩니다은 암호화 이후에 연결 문자열 정보를 해독 합니다. 개발 컴퓨터에 특정 키를 사용합니다. RSA 공급자는 RSA 키를 다른 컴퓨터로 내보낼 수 있기 때문에 이러한 제한이 없습니다.


## <a name="understanding-database-authentication-options"></a>데이터베이스 인증 옵션 이해

모든 응용 프로그램에 발급 하기 전에 `SELECT`, `INSERT`를 `UPDATE`, 또는 `DELETE` 쿼리는 Microsoft SQL Server 데이터베이스를 먼저 식별 해야 요청자입니다. 이 프로세스는 이라고 *인증* SQL Server 인증의 두 메서드를 제공 합니다.

- **Windows 인증** -응용 프로그램이 실행 되 고 있는 프로세스는 데이터베이스를 사용 하 여 통신에 사용 됩니다. Visual Studio 2005가의 ASP.NET Development Server를 통해 ASP.NET 응용 프로그램을 실행할 때 ASP.NET 응용 프로그램에서는 현재 로그온된 한 사용자의 id를 가정 합니다. ASP.NET 응용 프로그램 Microsoft 인터넷 정보 서버 (IIS)에 대 한 ASP.NET 응용 프로그램 일반적으로 가장할 `domainName``\MachineName` 또는 `domainName``\NETWORK SERVICE`이지만이 사용자 지정할 수 있습니다.
- **SQL 인증** -사용자 ID 및 암호 값은 인증에 대 한 자격 증명으로 제공 됩니다. SQL 인증을 사용 하 여 사용자 ID와 암호는 연결 문자열에 제공 됩니다.

Windows 인증 이므로 기본 SQL 인증 보다 더 안전 합니다. Windows 인증을 사용 하 여 연결 문자열은 사용자 이름 및 암호에서 무료 및 자격 증명을 웹 서버와 데이터베이스 서버를 두 개의 서로 다른 컴퓨터에 있는 경우 일반 텍스트로 네트워크를 통해 보내지지 않습니다. 그러나 SQL 인증을 사용 하 여 인증 자격 증명 연결 문자열에 하드 코딩 되며 웹 서버에서 데이터베이스 서버를 일반 텍스트로 전송 됩니다.

이 자습서는 Windows 인증을 사용 했습니다. 연결 문자열을 검사 하 여 인증 모드를 사용 하는 것을 확인할 수 있습니다. 연결 문자열 `Web.config` 이 자습서는 왔습니다.

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

Integrated Security = True 및 사용자 이름 및 암호의 부족 Windows 인증 사용 되 고 있음을 나타냅니다. 일부 연결의 용어 신뢰할 수 있는 연결 문자열 = Yes 또는 통합된 보안 = 통합 보안 대신 SSPI가 사용 = true 인 경우 세 가지 모두 Windows 인증을 사용 했지만 합니다.

다음 예제에서는 SQL 인증을 사용 하는 연결 문자열을 보여 줍니다. 연결 문자열에 자격 증명을 포함 하는 참고:

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

공격자가 사용자 응용 프로그램 s를 볼 수는 imagine `Web.config` 파일입니다. SQL 인증을 사용 하 여 인터넷을 통해 액세스할 수 있는 데이터베이스에 연결할 공격자가이 연결 문자열을 사용 하 여 SQL Management studio 또는 자체 웹 사이트의 ASP.NET 페이지에서 데이터베이스에 연결할 수 있습니다. 이 위협을 완화 하려면,의 연결 문자열 정보를 암호화 `Web.config` 보호 되는 구성 시스템을 사용 합니다.

> [!NOTE]
> 다른 SQL Server에서 사용할 수 있는 인증 유형에 대 한 자세한 내용은 참조 하세요. [Building Secure ASP.NET Applications: Authentication, Authorization, and Secure Communication](https://msdn.microsoft.com/library/aa302392.aspx)합니다. 추가 연결 문자열 예제 Windows 및 SQL 인증 구문 간의 차이점을 보여 주는 참조 하세요 [ConnectionStrings.com](http://www.connectionstrings.com/)합니다.


## <a name="summary"></a>요약

기본적으로 사용 하 여 파일을 `.config` 브라우저를 통해 ASP.NET 응용 프로그램에서 확장에 액세스할 수 없습니다. 이러한 종류의 파일에는 데이터베이스 연결 문자열, 사용자 이름 및 암호 같은 중요 한 정보를 포함 하 고 등 수 하기 때문에 반환 되지 않습니다. .NET 2.0에서 보호 되는 구성 시스템에 중요 한 정보를 암호화 하도록 지정 된 구성 섹션을 허용 하 여 보호를 강화 하는 데 도움이 됩니다. 두 명의 기본 제공 보호 되는 구성 공급자가: RSA 알고리즘 및 Windows 데이터 보호 API (DPAPI)를 사용 하는 하나를 사용 하는 것입니다.

이 자습서에서는 암호화 및 해독 DPAPI 공급자를 사용 하 여 구성을 설정 하는 방법에 살펴보았습니다. 이렇게 하려면 2 단계에서 보았듯이 프로그래밍 방식으로를 통해는 `aspnet_regiis.exe` 3 단계에서에서 설명 된 명령줄 도구입니다. 사용자 수준 키를 사용 하 여 RSA 공급자를 대신 사용에 대 한 자세한 내용은 추가 정보 섹션의 리소스를 참조 하세요.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [보안 된 ASP.NET 응용 프로그램 빌드: 인증, 권한 부여 및 보안 통신](https://msdn.microsoft.com/library/aa302392.aspx)
- [ASP.NET 2.0에서에서 구성 정보 암호화 응용 프로그램](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [암호화 `Web.config` ASP.NET 2.0의에서 값](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [방법: ASP.NET 2.0에서에서 구성 섹션 암호화 DPAPI를 사용 하 여](https://msdn.microsoft.com/library/ms998280.aspx)
- [방법: ASP.NET 2.0에서에서 구성 섹션을 암호화 하 RSA를 사용 하 여](https://msdn.microsoft.com/library/ms998283.aspx)
- [.NET 2.0에서에서 구성 API](http://www.odetocode.com/Articles/418.aspx)
- [Windows 데이터 보호](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Teresa Murphy 및 Randy Schmidt 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
> [다음](debugging-stored-procedures-cs.md)
