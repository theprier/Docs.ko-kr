---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: "ASP.NET 웹 페이지 (Razor) 문제 해결 가이드 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 ASP.NET Web Pages (Razor) 및 제안 된 일부 솔루션을 작업할 때 발생할 수 있는 문제를 설명 합니다. 소프트웨어 버전 ASP.NET 웹 페이지 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: 2e25e9c7cea937016301e0f11919adb9647ca216
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="aspnet-web-pages-razor-troubleshooting-guide"></a>ASP.NET 웹 페이지 (Razor) 문제 해결 가이드
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET Web Pages (Razor) 및 제안 된 일부 솔루션을 작업할 때 발생할 수 있는 문제를 설명 합니다.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서에서는 ASP.NET 웹 페이지 2에서 ASP.NET 웹 페이지 1.0 에서도 작동합니다.


이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [페이지 실행 문제](#Issues_Running_.cshtml_Pages)
- [Razor 코드 문제](#IssuesWithRazorCode)
- [멤버 자격 및 보안 문제](#membership)
- [전자 메일 문제](#email)
- [추가 리소스](#AdditionalResources)

일반적인 질문에 대 한 참조 [ASP.NET 웹 페이지 (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000)합니다.

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>페이지 실행 문제

다양 한 문제를 방지할 수 *.cshtml* 및 *.vbhtml* 제대로 실행 되는 페이지입니다. 이 섹션에는 일반적인 오류 메시지 목록과 가능한 원인 됩니다.

### <a name="http-error-403---forbidden-access-is-denied"></a>HTTP 오류 403-사용할 수 없음: 액세스가 거부 되었습니다.

*이 디렉터리 또는 사용자가 제공한 자격 증명을 사용 하 여 페이지를 볼 수 있는 권한이 없습니다.*

이 오류는 서버는 올바른 버전의.NET Framework를 실행 하지 않는 경우에 발생할 수 있습니다. (로컬 또는 원격) 서버를 실행 중인 컴퓨터에 설치 된.NET Framework 4 이상 있는지 확인 합니다. 또한 응용 프로그램 자체 올바른 버전을 실행 하도록 구성 되어 있는지 확인 합니다.

WebMatrix에서 작업 하는 동안이 문제를 로컬로 표시를 클릭는 **사이트** 작업 영역에서 클릭 하 여 treeview에서 다음 **설정을**합니다. 에 **.NET Framework 버전 선택** 목록에서 선택 **.NET 4 (통합)**합니다. 이 버전은 이미 설정 된 경우 관리자 권한으로 WebMatrix를 실행 하십시오.

웹 사이트의 루트에 하나 이상 있는지 확인 *.cshtml* 파일이 들어 있습니다.

웹 서버가 원격 서버에 있으면이 오류를 표시 되 면 서버 관리자를 게 문의 하십시오. 서버에.NET Framework 4 이상을 설치 되어 있는지 확인 합니다. 또한.net Framework의 해당 버전을 사용 하도록 구성 된 응용 프로그램 풀에서 응용 프로그램이 실행 되 고 있는지 확인 합니다.

서버에 대 한 제어를 사용 하는 경우 올바른 버전의.NET Framework 실행 중인지 확인 합니다. 실행 하 여 설치를 복구 해 보십시오는 `aspnet_regiis -iru` 명령입니다. (예를 들어.NET Framework를 설치한 후 IIS를 설치한 경우 IIS 구성 되지 않습니다 수 올바르게 ASP.NET 페이지를 실행 하도록.) 자세한 내용은 참조 [ASP.NET IIS 등록 도구 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)합니다.

### <a name="http-error-40314---forbidden"></a>HTTP 오류 403.14-사용 권한 없음

*웹 서버가이 디렉터리의 콘텐츠를 표시 하지 못하도록 구성 됩니다.*

보호 되는 리소스를 요청 하는 경우이 오류가 발생할 수 있습니다 (같은 *Web.config* 파일)가 있는 보호 되는 폴더 또는 (같은 *앱\_데이터* 또는 *앱\_코드*).

### <a name="http-error-40417---not-found"></a>HTTP 오류 404.17-찾을 수 없습니다

*요청한 콘텐츠가 스크립트로 표시 되 및 정적 파일 처리기에서 처리 되지 않습니다.*

서버에.NET Framework 4를 사용 하도록 올바르게 구성 되지 않은 또는 일부 이므로 나중에 코드를 인식 하지 않으므로 경우이 오류가 발생할 수 `@{ }` 블록입니다. 이전 버전에 대 한 설명을 참조 *HTTP 오류 403-사용할 수 없음: 액세스가 거부 되었습니다*합니다.

### <a name="http-error-4047---not-found"></a>HTTP 오류 404.7-찾을 수 없습니다

*파일 확장명을 거부 하도록 요청 필터링 모듈이 구성 되어*

이 오류는 경우에 발생할 수 있습니다 *.cshtml* 또는 *.vbhtml* 확장 서버에 명시적으로 차단 되었습니다. 이 문제의 증상 확장 이지만 포함 하는 Url 포함 하지 않는 경우 작동 하는 Url은 *.cshtml* 또는 *.vbhtml* 작동 하지 않습니다. 사이트의 확장을 다시 사용 가능한 솔루션은 *Web.config* 파일입니다. 다음 예제를 사용 하도록 설정 하는 방법의 *.cshtml* 확장 합니다.

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>HTTP 오류 404.8-찾을 수 없습니다

*HiddenSegment 섹션을 포함 하는 URL의 경로 거부 하도록 요청 필터링 모듈이 구성 됩니다.*

보호 되는 리소스를 요청 하는 경우이 오류가 발생할 수 있습니다 (같은 *Web.config* 파일)가 있는 보호 되는 폴더 또는 (같은 *앱\_데이터* 또는 *앱\_코드*).

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>이런이 종류의 페이지 ('/' 응용 프로그램에서 오류 서버) 처리 되지 않습니다.

HTTP 오류 404.17에 대 한 이전 설명을 참조 하십시오.

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Razor 코드 문제

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>이름 '*클래스*' 현재 컨텍스트에 존재 하지 않습니다

대개이 오류를 참조 하는 이유는는 `class` 참조 도우미를 있지만 도우미 설치 되어 있지 않습니다. 예를 들어 도우미를 사용 하려고 하지만에서 NuGet 패키지를 설치 하지 않은 경우이 오류가 표시 됩니다. WebMatrix의 갤러리를 사용 하 여 찾아서 도우미를 설치 합니다.

도우미를 설치 했지만 페이지 여전히 인식 하지 않는 것, 추가 시도 추가 `using` 코드에 문의 합니다. 에 `using` 문, 참조 도우미를 포함 하는 네임 스페이스입니다. ASP.NET 웹 도우미 패키지에 있는 기본 도우미는 예를 들어는 `System.Web.Helpers` 네임 스페이스입니다. 도우미를 사용 하려면 페이지의 위쪽이 줄을 추가 합니다.

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>멤버 자격 및 보안 문제

기본 제공 보안 (membership) 시스템 ASP.NET 웹 페이지 (Razor)에서 사용 중인 경우에 다음과 같은 문제가 발생할 수 있습니다.

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>이 메서드를 호출 하려면 "Membership.Provider" 속성 "ExtendedMembershipProvider"의 인스턴스를 여야 합니다.

이 오류를 나타낼 수 없는 `AspNetSqlMembershipProvider` 클래스가 구성 되어 있습니다. (으로 이루어졌다는 징후가 사이트 로컬로 제대로 작동 하지만 호스팅 공급자의 서버에 게시할 때이 오류가 발생 합니다.) 이 문제에 대 한 수정이 사이트의 다음을 추가 하 여 간단한 멤버 자격을 명시적으로 활성화 하는 *Web.config* 파일:

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>전자 메일 문제

전자 메일 보내기 관련 디버깅 하기 어려울 수 있습니다. SMTP 서버에 연결할 수는 초기 문제 수 있습니다. 연결이 성공 하는 경우 ASP.NET에 전달한 메시지에서 SMTP 서버에 있습니다. 그러나 메시지 자체를 보내는 SMTP 서버 수 없는 문제가 있을 수 있습니다.

응용 프로그램이 성공적으로 전자 메일을 보내지 않으면를 다음과 같이 하세요.

- SMTP 서버 이름을 방식은 다음과 같이 `smtp.provider.com` 또는 `smtp.provider.net`합니다. 그러나 사이트를 호스팅 공급자에 게시 하는 경우 SMTP 서버 이름을 해당 지점에서 않을 `localhost`합니다. 이 경우 게시 한 후 사이트 공급자의 서버에서 실행 되는 SMTP 서버 응용 프로그램의 관점에서 로컬 수 있기 때문에 발생 합니다. 서버 이름에 이러한 변경 의미를 게시 프로세스의 일부로 SMTP 서버 이름을 변경 해야 합니다.
- 포트 번호는 일반적으로 25입니다. 그러나 일부 공급자 사용 해야 할 포트 587 또는 일부 다른 포트입니다. 소유자를 확인 하는 SMTP 서버의 포트 번호도 기대 사용할 수 있습니다.
- 올바른 자격 증명을 사용 하 고 있는지 확인 합니다. 사이트를 호스팅 공급자에 게시 한 경우 특별히 설정 된 공급자가 전자 메일에 대 한 자격 증명을 사용 합니다. 이러한 자격 증명을 게시 하는 데 자격 증명과 다를 수 있습니다.
- 경우에 따라 자격 증명을 전혀 필요 하지 않습니다. 개인 ISP를 사용 하 여 전자 메일을 보내는 경우 전자 메일 공급자에 자격 증명 이미 알고 수 있습니다. 를 게시 한 후 로컬 컴퓨터에서 테스트 아니라 다른 자격 증명을 사용 하도록 할 수 있습니다.
- 전자 메일 공급자가 암호화를 사용 하는 경우 설정 `WebMail.EnableSsl` 를 `true`합니다.

전자 메일을 보내는 중 오류가 발생 하는 경우 다음과 같이 표시 하는 표준 ASP.NET 오류 메시지가 표시 될 수 있습니다.

![전자 메일에 문제가 있을 경우 ASP.NET 오류 메시지](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

사용 하 여 전자 메일을 보내는 문제를 디버깅할 수도 있습니다는 `try-catch` 다음 예제와 같이 블록입니다. 사용 하는 경우는 `try-catch` ASP.NET 블록의 표준 오류 메시지를 표시 하지 않습니다. 대신,에서 오류를 캡처할 수 있습니다는 `catch` 블록의 부분입니다.

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

에 대 한 적절 한 값으로 대체 `your-SMTP-server-name`등입니다. 이러한 방식으로 표시 될 수 있는 오류 메시지는 다음과 같습니다.

- *메일을 보내지 못했습니다.*

    또는

    *연결 된 구성원 시간 또는 연결 된 호스트에서 응답 하지 없어 연결 기간 후 올바르게 응답 하지 않아 연결 시도가 실패*

    이 오류는 일반적으로 응용 프로그램에서 SMTP 서버에 연결할 수 없습니다 의미 합니다. 서버 이름을 확인 하 고 포트 번호입니다.
- *사서함을 사용할 수 없습니다. 서버 응답: 5.1.0 &lt; someuser@invaliddomain &gt; 거부 보낸 사람: 잘못 된 보낸 도메인*

    이 메시지는 되었음을 나타낼 수 있습니다는 `From` 주소가 잘못 되었거나 없습니다.
- *지정된 된 문자열에 전자 메일 주소 형식이 없는 경우*

    이 오류를 나타낼 수 있습니다의 값은 `To` 또는 `From` 전자 메일 주소로 서 속성을 인식할 수 없습니다. (ASP.NET 확인할 수 없습니다. 전자 메일 주소가 올바른지 한다는 원하는 올바른 형식으로의  *name@domain.com* .)

> [!NOTE]
> 이 오류를 표시 하는 태그를 제거 (`@errorMessage`) 페이지를 라이브 사이트에 게시 하기 전에. 하지 사용자가 서버에서 얻을 수 있는 오류 메시지를 볼 수 있도록 하는 것이 좋습니다.


<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지(Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000)

[WebMatrix 및 ASP.NET 웹 페이지](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 웹 사이트에 대 한 포럼
