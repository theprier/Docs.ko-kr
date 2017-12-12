---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
title: "연결 문자열 및 기타 구성 정보 (VB) 보호 | Microsoft Docs"
author: rick-anderson
description: "일반적으로 ASP.NET 응용 프로그램 Web.config 파일에 구성 정보를 저장합니다. 이 정보 중 일부가 민감하여 보호 수행 되도록 합니다. 정의... 하 여"
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/03/2007
ms.topic: article
ms.assetid: cd17dbe1-c5e1-4be8-ad3d-57233d52cef1
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
msc.type: authoredcontent
ms.openlocfilehash: 8eaa9f43a69620862c95194117a026be391e2fb6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="protecting-connection-strings-and-other-configuration-information-vb"></a>연결 문자열 및 기타 구성 정보 (VB)를 보호합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_VB.zip) 또는 [PDF 다운로드](protecting-connection-strings-and-other-configuration-information-vb/_static/datatutorial73vb1.pdf)

> 일반적으로 ASP.NET 응용 프로그램 Web.config 파일에 구성 정보를 저장합니다. 이 정보 중 일부가 민감하여 보호 수행 되도록 합니다. 기본적으로이 파일 제공 되지 않으므로 웹 사이트 방문자에 게 하지만 관리자나 해커가 웹 서버의 파일 시스템에 액세스 하 고 파일의 내용을 볼 수 있습니다. 이 자습서에서는 ASP.NET 2.0 Web.config 파일의 섹션을 암호화 하 여 중요 한 정보를 보호할 수 있도록 설명 합니다.


## <a name="introduction"></a>소개

ASP.NET 응용 프로그램에 대 한 구성 정보는 일반적으로 이라는 XML 파일에 저장 `Web.config`합니다. 이 자습서의 과정 동안 업데이트는 `Web.config` 는 소수의 시간입니다. 만들 때의 `Northwind` 형식화 된 데이터 집합에는 [첫 번째 자습서](../introduction/creating-a-data-access-layer-vb.md), 연결 문자열 정보를 자동으로 추가 된 예를 들어 `Web.config` 에 `<connectionStrings>` 섹션. 뒷부분에 나오는 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서는 수동으로 업데이트 했습니다. `Web.config`추가는 `<pages>` 요소 모든 프로젝트에 ASP.NET 페이지의 사용 해야 함을 나타내는 `DataWebControls` 테마입니다.

이후 `Web.config` 연결 문자열과 같은 중요 한 데이터가 포함 될 수는 것이 중요 하는 내용의 `Web.config` 안전 하 고 권한이 없는 사용자에 게 서 숨겨지면 유지 합니다. 기본적으로 사용 하 여 파일 모든 HTTP 요청는 `.config` 확장을 반환 하는 ASP.NET 엔진에 의해 처리 되는 *이 형식의 페이지가 제공 되지 않습니다* 그림 1에 표시 되는 메시지입니다. 즉, 방문자를 볼 수 없는 프로그램 `Web.config`의 내용을 입력 하 여 간단히 http://www.YourServer.com/Web.config 자신의 s 브라우저 주소 표시줄에 파일.


[![메시지를 서비스 하지 않는 Web.config를 통해 정도 브라우저 반환이 페이지의 입력을 방문 합니다.](protecting-connection-strings-and-other-configuration-information-vb/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image1.png)

**그림 1**: 방문 `Web.config` 통해 정도 브라우저 반환이 페이지의 입력 메시지를 서비스 하지 않는 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image3.png))


경우에 어떻게 공격자가를 볼 수 있는 몇 가지 다른 악용을 찾을 수 있지만 사용자 `Web.config` 파일 s 내용의? 수는 공격자가 수행 작업이 정보를 사용 및 추가 내에서 중요 한 정보를 보호 하기 위해 취할 수 단계 `Web.config`? 대부분의 섹션에서는 `Web.config` 중요 한 정보가 포함 되지 않습니다. 어떤 문제가 발생 수는 공격자가 장시간 기본 ASP.NET 페이지에서 사용 하는 테마의 이름을 알고 있는 경우?

그러나 특정 `Web.config` 섹션 연결 문자열, 사용자 이름, 암호, 서버 이름, 암호화 키 등을 포함할 수 있는 중요 한 정보를 포함 합니다. 일반적으로이 정보는 다음에서 있습니다 `Web.config` 섹션:

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

이 자습서에서는 이러한 중요 한 구성 정보를 보호 하기 위한 기술 살펴보겠습니다. 를 알 수 있듯이 보호 구성 시스템 선택 된 구성 섹션 암호화와 암호 해독을 프로그래밍 방식으로 적합을.NET Framework 버전 2.0에 포함 되어 있습니다.

> [!NOTE]
> 이 자습서를 살펴보고 ASP.NET 응용 프로그램에서 데이터베이스에 연결 하기 위한 권장 s로 마칩니다. 연결 문자열을 암호화 하는 것 외에도 적용 되도록 하 여 안전한 방법으로 데이터베이스에 연결 하는 시스템 보안을 강화 도울 수 있습니다.


## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>1 단계: ASP.NET 2.0 탐색 s 보호 구성 옵션

ASP.NET 2.0에는 보호 되는 구성 시스템 암호화 및 해독 구성 정보에 포함 되어 있습니다. 프로그래밍 방식으로 암호화 하거나 구성 정보를 해독 하는 데 사용할 수 있는.NET Framework의 메서드가 포함 됩니다. 보호 되는 구성 시스템에서 사용 하 여 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 개발자가 어떤 암호화 구현 사용 되는 선택할 수 있습니다.

.NET Framework는 두 명의 보호 되는 구성 공급자와 함께 제공:

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/en-us/library/system.configuration.rsaprotectedconfigurationprovider.aspx)-비대칭를 사용 하 여 [RSA 알고리즘](http://en.wikipedia.org/wiki/Rsa) 암호화 및 암호 해독 합니다.
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/en-us/system.configuration.dpapiprotectedconfigurationprovider.aspx)-Windows를 사용 하 여 [데이터 보호 API (DPAPI)](https://msdn.microsoft.com/en-us/library/ms995355.aspx) 암호화 및 암호 해독 합니다.

이기 때문에 공급자 디자인 패턴을 구현 하는 보호 되는 구성 시스템, 응용 프로그램에 연결 하 고 보호 되는 구성 공급자를 만들 수 있습니다. 참조 [보호 구성 공급자를 구현](https://msdn.microsoft.com/en-us/library/wfc2t3az(VS.80).aspx) 이 프로세스에 대 한 자세한 내용은 합니다.

DPAPI 및 RSA 공급자의 암호화 및 암호 해독 루틴에 대 한 키를 사용 하 고 이러한 키에는 컴퓨터 또는 사용자 수준을 저장할 수 있습니다. 암호화 된 정보를 공유 해야 하는 서버에서 여러 응용 프로그램이 있는 경우 또는 컴퓨터 수준 키가 자체 전용된 서버에서 웹 응용 프로그램이 실행 되는 시나리오에 적합 합니다. 사용자 수준 키가 없는 동일한 서버의 다른 응용 프로그램 프로그램 응용 프로그램 보호 s 구성 섹션을 암호 해독할 수 해야 하는 공유 호스팅 환경에서 보다 안전한 옵션입니다.

이 자습서에서는 예제는 DPAPI 공급자 및 컴퓨터 수준 키를 사용 합니다. 특히, 살펴보도록 하겠습니다 암호화는 `<connectionStrings>` 섹션 `Web.config`모든 대부분를 암호화 하는 보호 되는 구성 시스템을 사용할 수 있지만, `Web.config` 섹션. 사용자 수준 키를 사용 하는 RSA 공급자를 사용 하 여 또는 대 한 자세한 내용은이 자습서의 끝에 추가 정보 섹션의 리소스를 참조 하십시오.

> [!NOTE]
> `RSAProtectedConfigurationProvider` 및 `DPAPIProtectedConfigurationProvider` 에 등록 된 공급자는 `machine.config` 공급자 이름으로 파일 `RsaProtectedConfigurationProvider` 및 `DataProtectionConfigurationProvider`각각. 암호화 하거나 해독 구성 정보를 수집 해야 적절 한 공급자 이름을 제공 하는 경우 (`RsaProtectedConfigurationProvider` 또는 `DataProtectionConfigurationProvider`) 실제 유형 16 진수 (`RSAProtectedConfigurationProvider` 및 `DPAPIProtectedConfigurationProvider`). 찾을 수 있습니다는 `machine.config` 파일에 `$WINDOWS$\Microsoft.NET\Framework\version\CONFIG` 폴더입니다.


## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>2 단계: 프로그래밍 방식으로 암호화 하 고 구성 섹션을 암호 해독

코드 몇 줄만 암호화 하거나 지정 된 공급자를 사용 하는 특정 구성 섹션의 암호를 해독할 수 있습니다. 코드를 하겠지만, 알 수 있듯이 하기만 하면 프로그래밍 방식으로 적절 한 구성 섹션을 참조 하 호출 해당 `ProtectSection` 또는 `UnprotectSection` 메서드를 호출 합니다는 `Save` 메서드의 변경 사항을 유지 합니다. 또한.NET Framework 암호화 및 구성 정보를 해독할 수 있는 유용한 명령줄 유틸리티를 포함 합니다. 3 단계에서에서이 명령줄 유틸리티를 살펴보겠습니다.

프로그래밍 방식으로 보호 구성 정보를 보여 주기 위해 let s 암호화 및 암호 해독에 대 한 단추가 포함 된 ASP.NET 페이지를 만듭니다는 `<connectionStrings>` 섹션 `Web.config`합니다.

열어 시작는 `EncryptingConfigSections.aspx` 페이지에 `AdvancedDAL` 폴더입니다. 설정 디자이너 도구 상자에서 TextBox 컨트롤을 끌어 해당 `ID` 속성을 `WebConfigContents`, 해당 `TextMode` 속성을 `MultiLine`, 및 해당 `Width` 및 `Rows` 속성을 95%와 15, 각각. 이 텍스트 상자 컨트롤의 내용을 표시 합니다 `Web.config` 경우 콘텐츠는 암호화 여부를 빠르게 볼 수 있도록 합니다. 물론, 실제 응용 프로그램에서은 하지 않으려는의 내용을 표시 하려면 `Web.config`합니다.

텍스트 상자 아래에 이라는 단추 컨트롤 2 개를 추가 `EncryptConnStrings` 및 `DecryptConnStrings`합니다. 연결 문자열 암호화 및 암호를 해독 하는 연결 문자열을 텍스트 속성을 설정 합니다.

이 시점에서 화면 그림 2 비슷해야 합니다.


[![페이지에 텍스트 상자와 두 개의 단추 웹 컨트롤 추가](protecting-connection-strings-and-other-configuration-information-vb/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image4.png)

**그림 2**: 페이지에 텍스트 상자 및 단추 웹 컨트롤 2 개를 추가 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image6.png))


다음으로 로드 하 고의 내용을 표시 하는 코드를 작성 해야 `Web.config` 에 `WebConfigContents` 로드 하는 페이지가 있는 경우 첫 번째 텍스트 상자에 붙여넣습니다. 다음 코드 페이지의 코드 숨김 클래스를 추가 합니다. 라는 메서드를 추가 하는이 코드 `DisplayWebConfig` 에서 호출 된 `Page_Load` 이벤트 처리기 때 `Page.IsPostBack` 은 `False`:


[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample1.vb)]

`DisplayWebConfig` 메서드는 [ `File` 클래스](https://msdn.microsoft.com/en-us/library/system.io.file.aspx) 응용 프로그램 s 열려는 `Web.config` 파일을는 [ `StreamReader` 클래스](https://msdn.microsoft.com/en-us/library/system.io.streamreader.aspx) 문자열과 로해당내용을읽어[ `Path` 클래스](https://msdn.microsoft.com/en-us/library/system.io.path.aspx) 실제 경로를 생성 하는 `Web.config` 파일입니다. 이러한 세 클래스 모두에서 발견 되는 [ `System.IO` 네임 스페이스](https://msdn.microsoft.com/en-us/library/system.io.aspx)합니다. 따라서 추가 해야 합니다는 `Imports``System.IO` 는 코드 숨김 클래스 하거나, 이러한 클래스와 이름은 접두사의 맨 위에 문을`System.IO.`

다음으로, 두 개의 단추 컨트롤에 대 한 이벤트 처리기를 추가 해야 `Click` 이벤트 암호화 및 해독 하는 데 필요한 코드를 추가 하 고는 `<connectionStrings>` DPAPI 공급자와 함께 컴퓨터 수준 키를 사용 하 여 섹션. 디자이너에서 두 번 클릭 각 단추를 추가 하려면는 `Click` 코드 숨김의 이벤트 처리기 클래스 및 다음 코드를 추가 합니다.


[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample2.vb)]

두 개의 이벤트 처리기에 사용 되는 코드는 거의 동일 합니다. 현재 응용 프로그램 s에 대 한 정보를 가져와서 시작 모두 `Web.config` 를 통해 파일의 [ `WebConfigurationManager` 클래스](https://msdn.microsoft.com/en-us/library/system.web.configuration.webconfigurationmanager.aspx) s [ `OpenWebConfiguration` 메서드](https://msdn.microsoft.com/en-us/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)합니다. 이 메서드는 지정된 된 가상 경로 대 한 웹 구성 파일을 반환합니다. 다음으로 `Web.config` 파일 s `<connectionStrings>` 섹션을 통해 액세스 되는 [ `Configuration` 클래스](https://msdn.microsoft.com/en-us/library/system.configuration.configuration.aspx) s [ `GetSection(sectionName)` 메서드](https://msdn.microsoft.com/en-us/library/system.configuration.configuration.getsection.aspx)를 반환 하는 [ `ConfigurationSection` ](https://msdn.microsoft.com/en-us/library/system.configuration.configurationsection.aspx) 개체입니다.

`ConfigurationSection` 개체를 포함 한 [ `SectionInformation` 속성](https://msdn.microsoft.com/en-us/library/system.configuration.configurationsection.sectioninformation.aspx) 추가 정보 및 구성 섹션에 대 한 기능을 제공 하는 합니다. 구성 섹션 확인 하 여 암호화 되는지 여부를 확인할 수 있습니다 위의 코드로 `SectionInformation` 속성의 `IsProtected` 속성입니다. 섹션 수 암호화 하거나 해독할 통해 또한는 `SectionInformation` 속성 s `ProtectSection(provider)` 및 `UnprotectSection` 메서드.

`ProtectSection(provider)` 메서드 암호화할 때 사용할 보호 되는 구성 공급자의 이름을 지정 하는 문자열 입력으로 받아들입니다. 에 `EncryptConnString` 에 DataProtectionConfigurationProvider 전달 s 단추 이벤트 처리기는 `ProtectSection(provider)` 메서드 DPAPI 공급자가 사용 되도록 합니다. `UnprotectSection` 메서드는 구성 섹션 암호화에 사용 된 하 고 따라서 필요 하지 않습니다는 입력 매개 변수는 공급자를 확인할 수 있습니다.

호출한 후의 `ProtectSection(provider)` 또는 `UnprotectSection` 호출 해야 합니다는 `Configuration` 개체 s [ `Save` 메서드](https://msdn.microsoft.com/en-us/library/system.configuration.configuration.save.aspx) 의 변경 사항을 유지 합니다. 이라고 변경 사항을 저장 하 고 구성 정보 암호화 되었거나 암호가 해독 된 `DisplayWebConfig` 업데이트 된 로드 `Web.config` TextBox 컨트롤의 내용입니다.

위의 코드를 입력 하 고 나면 방문 하 여 테스트는 `EncryptingConfigSections.aspx` 브라우저를 통해 페이지입니다. 콘텐츠를 나열 하는 페이지가 처음 나타납니다 `Web.config` 와 `<connectionStrings>` 일반 텍스트에 표시 되는 섹션 (그림 3 참조).


[![페이지에 텍스트 상자와 두 개의 단추 웹 컨트롤 추가](protecting-connection-strings-and-other-configuration-information-vb/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image7.png)

**그림 3**: 페이지에 텍스트 상자 및 단추 웹 컨트롤 2 개를 추가 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image9.png))


이제 연결 문자열 암호화 단추를 클릭 합니다. 태그에서 다시 게시 요청 유효성 검사를 사용 하는 경우는 `WebConfigContents` TextBox 생성 됩니다는 `HttpRequestValidationException`, 잠재적으로 위험한 메시지를 표시 하는 `Request.Form` 값이 클라이언트에서 발견 되었습니다. ASP.NET 2.0에서 기본적으로 활성화 되어 있는 요청 유효성 검사는 인코딩되지 않은 HTML을 포함 하는 다시 게시 하는 작업이 금지 하 고 스크립트 삽입 공격을 방지 하도록 설계 되었습니다. 이 검사에는 페이지 또는 응용 프로그램 수준 비활성화할 수 있습니다. 설정 하지 않으려면이 페이지를 `ValidateRequest` 설정을 `False` 에 `@Page` 지시문입니다. `@Page` 지시문 페이지 s 선언적 태그의 위쪽에 있습니다.


[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample3.aspx)]

요청 유효성 검사의 용도 대 한 자세한 내용은 참조에 페이지 및 응용 프로그램 수준, 방법과 html 태그를 인코딩할 때 사용 하지 않도록 하는 방법 [요청 유효성 검사-스크립트 공격 방지](../../../../whitepapers/request-validation.md)합니다.

페이지에 대 한 요청 유효성 검사를 비활성화 한 후 연결 문자열 암호화 단추를 다시 클릭 하십시오. 다시 게시 될 구성 파일을 액세스는 해당 `<connectionStrings>` 섹션 DPAPI 공급자를 사용 하 여 암호화 합니다. TextBox 그러면 새 표시 하도록 업데이트 됩니다 `Web.config` 콘텐츠입니다. 그림 4에서 볼 수 있듯이 `<connectionStrings>` 정보는 이제 암호화 합니다.


[![암호화 연결 문자열 단추 암호화를 클릭 하 여 &lt;connectionString&gt; 섹션](protecting-connection-strings-and-other-configuration-information-vb/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image10.png)

**그림 4**:에서 암호화 연결 문자열 단추 암호화를 클릭 하 여 `<connectionString>` 섹션 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image12.png))


암호화 된 `<connectionStrings>` 내 컴퓨터에서 생성 된 섹션 뒤 있지만의 내용 중 일부는 `<CipherData>` 요소가 간단히 하기 위해 제거:


[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample4.xml)]

> [!NOTE]
> `<connectionStrings>` 암호화를 수행 하는 데 공급자를 지정 하는 요소 (`DataProtectionConfigurationProvider`). 이 정보를 사용 하 여는 `UnprotectSection` 메서드 연결 문자열의 암호를 해독 단추를 클릭할 때입니다.


연결 문자열 정보를 액세스할 때 `Web.config` -현재 사용자나 SqlDataSource 컨트롤에서 보겠습니다 코드 자동 생성 코드에서 형식화 된 데이터 집합에서 TableAdapters-자동으로 해독 됩니다. 추가 코드 또는 암호화 된 암호를 해독 하는 논리가 추가 필요가 없습니다 간단히 말해서 `<connectionString>` 섹션. 이 증명 하려면 이전 자습서 중 하나에 방문 등 기본 보고 섹션에서 간단한 표시 자습서의이 시간 (`~/BasicReporting/SimpleDisplay.aspx`). 그림 5에서 볼 수 있듯이 자습서를 찾아야, 암호화 된 연결 문자열 정보는 ASP.NET 페이지에 의해 자동으로 해독 되 고 나타내는 대로 정확 하 게 작동 합니다.


[![연결 문자열 정보를 자동으로 해독 하는 데이터 액세스 계층](protecting-connection-strings-and-other-configuration-information-vb/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image13.png)

**그림 5**: 연결 문자열 정보를 자동으로 해독 하는 데이터 액세스 계층 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image15.png))


되돌리려면는 `<connectionStrings>` 일반 텍스트 표현으로 다시 섹션에서 연결 문자열의 암호를 해독 단추를 클릭 합니다. 포스트백에서의 연결 문자열에 표시 되어야 `Web.config` 일반 텍스트에서입니다. 이 시점에서이 페이지 (그림 3에서 참조)를 처음 방문할 때와 같게 화면이 표시 됩니다.

## <a name="step-3-encrypting-configuration-sections-usingaspnetregiisexe"></a>사용 하 여 구성 섹션을 암호화 하는 3 단계:`aspnet_regiis.exe`

.NET Framework는 다양 한의 명령줄 도구는 `$WINDOWS$\Microsoft.NET\Framework\version\` 폴더입니다. 에 [를 사용 하 여 SQL 캐시 종속성](../caching-data/using-sql-cache-dependencies-vb.md) 자습서, 예를 들어, 살펴보았습니다를 사용 하는 `aspnet_regsql.exe` SQL 캐시 종속성에 필요한 인프라를 추가 하려면 명령줄 도구입니다. 이 폴더에 또 다른 유용한 명령줄 도구는는 [ASP.NET IIS 등록 도구 (`aspnet_regiis.exe`)](https://msdn.microsoft.com/en-us/library/k6h9cz8h(VS.80).aspx)합니다. 이름에서 알 수 있듯이 ASP.NET IIS 등록 도구는 Microsoft의 전문가 용 웹 서버를 IIS와 ASP.NET 2.0 응용 프로그램을 등록에 주로 사용 됩니다. IIS 관련 기능 외에도 ASP.NET IIS 등록 도구 사용할 수도 있습니다를 암호화 하거나 해독의 지정 된 구성 섹션 `Web.config`합니다.

다음 문을 사용 하는 구성 섹션을 암호화 하는 데 사용 되는 일반 구문을 보여 줍니다는 `aspnet_regiis.exe` 명령줄 도구:


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample5.cmd)]

*섹션* (예: connectionStrings)를 암호화 하는 구성 섹션은 *물리적\_디렉터리* 웹 응용 프로그램의 루트 디렉터리의 전체, 실제 경로 및 *공급자*  보호 되는 구성 공급자 (예: DataProtectionConfigurationProvider)의 이름입니다. 또는 웹 응용 프로그램 IIS에 등록 된 경우에 다음 구문을 사용 하 여 실제 경로 대신 가상 경로 입력할 수 있습니다.


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample6.cmd)]

다음 `aspnet_regiis.exe` 예제에서는 암호화는 `<connectionStrings>` DPAPI 공급자를 사용 하 여 컴퓨터 수준 키가 있는 섹션:


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample7.cmd)]

마찬가지로,는 `aspnet_regiis.exe` 구성 섹션의 암호를 해독 하는 명령줄 도구를 사용할 수 있습니다. 사용 하는 대신는 `-pef` 스위치를 사용 하 여 `-pdf` (또는 instead of `-pe`를 사용 하 여 `-pd`). 또한 참고가 암호를 해독 하는 경우 공급자 이름이 필요 하지 않습니다.


[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample8.cmd)]

> [!NOTE]
> 실행 해야 해당 컴퓨터에 한정 되는 키를 사용 하는 DPAPI 공급자를 사용 하 고 있으므로 `aspnet_regiis.exe` 같은 컴퓨터에서 웹 페이지는 제공 합니다. 예를 들어 로컬 개발 컴퓨터에서이 명령줄 프로그램을 실행 하 고 다음 프로덕션 서버에 암호화 된 Web.config 파일을 업로드 하는 경우 프로덕션 서버가 됩니다 암호화 이후 연결 문자열 정보를 해독할 수 없습니다. 개발 컴퓨터에 특정 키를 사용합니다. RSA 공급자가 다른 컴퓨터에 RSA 키를 내보낼 수 있기 때문에 이러한 제한이 없습니다.


## <a name="understanding-database-authentication-options"></a>데이터베이스 인증 옵션 이해

모든 응용 프로그램에 발급 하기 전에 `SELECT`, `INSERT`, `UPDATE`, 또는 `DELETE` Microsoft SQL Server 데이터베이스를 데이터베이스에 쿼리를 먼저 식별 해야 요청자입니다. 이 프로세스 라고 *인증* 및 SQL Server 인증의 두 가지 방법을 제공 합니다.

- **Windows 인증** -응용 프로그램을 실행 하는 프로세스는 데이터베이스와 통신 하는 데 사용 됩니다. Visual Studio 2005의 ASP.NET 개발 서버를 통해 ASP.NET 응용 프로그램을 실행할 때 ASP.NET 응용 프로그램에서는 현재 로그온된 한 사용자의 id를 사용 합니다. ASP.NET 응용 프로그램 Microsoft 인터넷 정보 서버 (IIS)에 대 한 ASP.NET 응용 프로그램 일반적으로의 id를 가장 `domainName``\MachineName` 또는 `domainName``\NETWORK SERVICE`않더라도 사용자을 지정할 수 있습니다.
- **SQL 인증** -사용자 ID와 암호 값은 인증에 대 한 자격 증명으로 제공 됩니다. SQL 인증 사용자 ID와 암호는 연결 문자열에 제공 됩니다.

하므로 Windows 인증은 기본 SQL 인증을 통해 것이 더 안전 합니다. Windows 인증으로 연결 문자열은 사용자 이름 및 암호에서 사용 가능한 되며 자격 증명이 웹 서버와 데이터베이스 서버가 있는 경우 두 개의 서로 다른 컴퓨터에서 일반 텍스트로 네트워크를 통해 보내지지 않습니다. 하지만 SQL 인증을 사용 인증 자격 증명 연결 문자열에 하드 코드 되며 웹 서버에서 데이터베이스 서버에 일반 텍스트로 전송 됩니다.

이 자습서는 Windows 인증을 사용 했습니다. 연결 문자열을 검사 하 여 인증 모드를 사용 하는 것을 알 수 있습니다. 연결 문자열을 `Web.config` 우리의 자습서에 대 한 되었습니다:

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

통합 보안 = True 및 사용자 이름 및 암호의 부족 Windows 인증이 사용 되 고 있음을 나타냅니다. 일부 연결에 용어 트러스트 된 연결 문자열 = Yes 또는 통합된 보안 = 통합 보안 대신 SSPI를 사용 = True 인 것 같지만 세 가지 모두 Windows 인증의 사용을 나타냅니다.

다음 예제에서는 SQL 인증을 사용 하는 연결 문자열을 보여 줍니다. 연결 문자열 내에 포함 된 자격 증명 참고:

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

공격자가 응용 프로그램 s 볼 수 있게 가정해 보세요. `Web.config` 파일입니다. SQL 인증을 사용 하 여 인터넷을 통해 액세스할 수 있는 데이터베이스에 연결할 공격자가이 연결 문자열을 사용 하 여 자신의 웹 사이트에서 ASP.NET 페이지 또는 SQL Management Studio를 통해 데이터베이스에 연결할 수 있습니다. 이 위협을 완화 하려면의 연결 문자열 정보를 암호화 `Web.config` 보호 되는 구성 시스템을 사용 합니다.

> [!NOTE]
> SQL Server에서 사용할 수 있는 인증의 서로 다른 형식에 대 한 자세한 내용은 참조 하십시오. [보안 ASP.NET 응용 프로그램: 인증, 권한 부여 및 보안 통신](https://msdn.microsoft.com/en-us/library/aa302392.aspx)합니다. 추가 연결 문자열의 Windows 및 SQL 인증 구문 차이점을 보여 주는 예제를 보려면 참조 [ConnectionStrings.com](http://www.connectionstrings.com/)합니다.


## <a name="summary"></a>요약

기본적으로 파일을 한 `.config` 브라우저를 통해 ASP.NET 응용 프로그램에서 확장에 액세스할 수 없습니다. 이러한 종류의 파일에 있으며 데이터베이스 연결 문자열, 사용자 이름 및 암호 같은 중요 한 정보가 포함 될 수 있습니다 때문에 반환 되지 않습니다. .NET 2.0에서 보호 되는 구성 시스템을 사용 하면 지정 된 구성 섹션 암호화 되도록 허용 하 여 중요 한 정보를 추가로 보호 합니다. 두 명의 기본 제공 보호 되는 구성 공급자가: 하나 RSA 알고리즘 하 고 다른 하나는 Windows DPAPI 데이터 보호 API ()를 사용 합니다.

이 자습서에서는 암호화 및 해독 DPAPI 공급자를 사용 하 여 구성을 설정 하는 방법을 찾았습니다. 이렇게 하려면 2 단계에서 설명한 것 처럼 프로그래밍 방식으로 통해 서는 `aspnet_regiis.exe` 3 단계에서에서 설명 된 명령줄 도구입니다. 사용자 수준 키를 사용 하 여 또는 RSA 공급자를 대신 사용 하 여 자세한 정보에 대 한 추가 정보 섹션에서 리소스를 참조 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [보안 ASP.NET 응용 프로그램 빌드: 인증, 권한 부여 및 보안 통신](https://msdn.microsoft.com/en-us/library/aa302392.aspx)
- [ASP.NET 2.0에서에서 구성 정보 암호화 응용 프로그램](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [암호화 `Web.config` ASP.NET 2.0의에서 값](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [방법: ASP.NET 2.0에서에서 구성 섹션 암호화 DPAPI를 사용 하 여](https://msdn.microsoft.com/en-us/library/ms998280.aspx)
- [방법: ASP.NET 2.0에서에서 구성 섹션을 암호화 하 RSA를 사용 하 여](https://msdn.microsoft.com/en-us/library/ms998283.aspx)
- [.NET 2.0 구성 API](http://www.odetocode.com/Articles/418.aspx)
- [Windows 데이터 보호](https://msdn.microsoft.com/en-us/library/ms995355.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피 및 Randy Schmidt 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
[다음](debugging-stored-procedures-vb.md)
