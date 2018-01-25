---
uid: whitepapers/aspnet4/breaking-changes
title: "ASP.NET 4 주요 변경 내용 | Microsoft Docs"
author: rick-anderson
description: "이 문서에 적용 된.NET Framework 버전에 대 한 사용 하 여 만든 응용 프로그램에 영향을 줄 수 있는 4 릴리스의 변경 내용에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 98647830125670ee2ed43538d65fb3ce6ac40d0d
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-4-breaking-changes"></a>ASP.NET 4 주요 변경 내용
====================
> 이 문서에 적용 된.NET Framework 버전은 이전 버전에서 ASP.NET 4 베타 1, 베타 2 출시를 사용 하 여 만든 응용 프로그램에 영향을 줄 수 있는 4 릴리스의 변경 내용을 설명 합니다.
> 
> [이 백서를 다운로드 합니다.](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)


<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>목차

[Web.config 파일의 ControlRenderingCompatibilityVersion 설정](#0.1__Toc256770141 "_Toc256770141")  
[ClientIDMode 변경](#0.1__Toc256770142 "_Toc256770142")  
[HtmlEncode UrlEncode 지금 인코딩해야 작은따옴표](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET 페이지 (.aspx) 파서는 Stricter](#0.1__Toc256770144 "_Toc256770144")  
[브라우저 정의 파일 업데이트](#0.1__Toc256770145 "_Toc256770145")  
[System.Web.Mobile.dll 루트 웹 구성 파일에서 제거](#0.1__Toc256770146 "_Toc256770146")  
[ASP.NET 요청 유효성 검사](#0.1__Toc256770147 "_Toc256770147")  
[기본 해싱 알고리즘은 이제 HMACSHA256](#0.1__Toc256770148 "_Toc256770148")  
[새 ASP.NET 4 루트 구성과 관련 된 구성 오류](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 4 개의 자식 응용 프로그램 실패 시작 때 ASP.NET 2.0 또는 ASP.NET 3.5 응용 프로그램](#0.1__Toc256770150 "_Toc256770150")  
[ASP.NET 4 웹 사이트 시작 되지 않고 SharePoint가 설치 된 컴퓨터에서](#0.1__Toc256770151 "_Toc256770151")  
[HttpRequest.FilePath 속성 PathInfo 값을 더 이상 포함](#0.1__Toc256770152 "_Toc256770152")  
[ASP.NET 2.0 응용 프로그램에는 eurl.axd 참조 하는 HttpException 오류가 발생할 가능성이](#0.1__Toc256770153 "_Toc256770153")  
[IIS 7.5 또는 IIS 7에서 기본 문서에 이벤트 처리기 하지 발생 하지 않습니다 통합 모드](#0.1__Toc256770154 "_Toc256770154")  
[ASP.NET 코드 액세스 보안 (CA) 구현에 변경](#0.1__Toc256770155 "_Toc256770155")  
[이동 된 MembershipUser의에서 및 기타 형식 System.Web.Security Namespace](#0.1__Toc256770156 "_Toc256770156")  
[출력 캐싱 변경 내용을 변경 하려면 \* HTTP 헤더](#0.1__Toc256770157 "_Toc256770157")  
[Passport System.Web.Security 유형은 Obsolete](#0.1__Toc256770158 "_Toc256770158")  
[ASP.NET 4에에서 있는 이미지를 렌더링 하지 못함 MenuItem.PopOutImageUrl 속성](#0.1__Toc256770159 "_Toc256770159")  
[경로가 백슬래시를 포함 하는 경우 이미지를 렌더링 하 Menu.DynamicPopOutImageUrl 실패 하 게 되며 Menu.StaticPopOutImageUrl](#0.1__Toc256770160 "_Toc256770160")  
[Disclaimer](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Web.config 파일의 ControlRenderingCompatibilityVersion 설정

ASP.NET 컨트롤 태그 렌더링 방법을 보다 정확 하 게 지정할 수 있도록.NET Framework 4 버전에서에서 수정 되었습니다. .NET Framework의 이전 버전에서는 일부 컨트롤 태그를 사용 하지 않도록 설정할 수 없으므로 누렸던 내보내집니다. 기본적으로 ASP.NET 4이이 유형의 태그가 더 이상 생성 됩니다.

Visual Studio 2010을 사용 하 여 ASP.NET 2.0 또는 ASP.NET 3.5에서 응용 프로그램을 업그레이드 하는 도구에서 자동으로 추가 하는 설정을 `Web.config` 레거시 렌더링을 유지 하는 파일입니다. 그러나 .NET Framework 4를 대상으로 하도록 IIS에서 응용 프로그램 풀을 변경하여 응용 프로그램을 업그레이드하는 경우 ASP.NET은 기본적으로 새 렌더링 모드를 사용합니다. 새 렌더링 모드를 해제 하려면에서 다음 설정을 추가 `Web.config` 파일:

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

주요 렌더링 변경 하면 새 동작이 제공 하는 것은 다음과 같습니다.

- **이미지** 및 **ImageButton** 컨트롤은 더 이상 렌더링 한 `border="0"` 특성입니다.
- **BaseValidator** 여기에서 파생 되는 컨트롤을 클래스 및 유효성 검사를 더 이상 빨간색 텍스트로 기본적으로 렌더링 합니다.
- **htmlform에서** 컨트롤 렌더링 하지 않습니다는 **이름** 특성입니다.
- **테이블** 렌더링을 더 이상 제어는 `border="0"` 특성입니다.
- 사용자 입력을 위해 설계 되지 않은 컨트롤 (예를 들어는 **레이블** 컨트롤) 더 이상 렌더링는 `disabled="disabled"` 특성 경우 해당 **Enabled** 속성이로 설정 되어 **false**(또는 컨테이너 컨트롤에서이 설정을 상속 하는 경우).

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>ClientIDMode 변경 내용

**ClientIDMode** ASP.NET 4에서 설정을 통해 ASP.NET에서 생성 하는 방법을 지정할 수는 **id** HTML 요소에 대 한 특성입니다. ASP.NET의 이전 버전 기본 동작을 해당 하는 **AutoID** 설정인 **ClientIDMode**합니다. 그러나 기본 설정은 이제 **예측 가능**합니다.

Visual Studio 2010을 사용 하 여 ASP.NET 2.0 또는 ASP.NET 3.5에서 응용 프로그램을 업그레이드 하는 도구에서 자동으로 추가 하는 설정을 `Web.config` 이전 버전의.NET Framework의 동작을 유지 하는 파일입니다. 그러나 .NET Framework 4를 대상으로 하도록 IIS에서 응용 프로그램 풀을 변경하여 응용 프로그램을 업그레이드하는 경우 ASP.NET은 기본적으로 새 모드를 사용합니다. 새 클라이언트 ID 모드를 해제 하려면에서 다음 설정을 추가 `Web.config` 파일:

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>HtmlEncode UrlEncode 지금 인코딩해야 작은따옴표

ASP.NET 4에서는 **HtmlEncode** 및 **UrlEncode** 의 메서드는 **HttpUtility** 및 **HttpServerUtility** 에 클래스가 업데이트 되었으며 다음과 같이 작은따옴표 문자를 (')를 인코딩하십시오.

- **HtmlEncode** 메서드 인코딩합니다 작은따옴표 '.
- **UrlEncode** 메서드 %27 작은따옴표의 인스턴스를 인코딩합니다.

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET 페이지 (.aspx) 파서 Stricter은

ASP.NET 페이지에 대 한 페이지 파서 (`.aspx` 파일) 및 사용자 정의 컨트롤 (`.ascx` 파일) ASP.NET 4에서 엄격한 및 더 많은 인스턴스의 잘못 된 태그를 거부 합니다. 예를 들어 다음 코드 조각 두 개 이전 버전의 ASP.NET 구문 분석은 있지만 이제 ASP.NET 4의 파서 오류를 발생 시킵니다.

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

확인의 끝에 잘못 된 세미콜론은 **HiddenField** 태그입니다.

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

닫히지 않은 확인 **스타일** 특성으로 실행 되는 **CssClass** 특성입니다.

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>브라우저 정의 파일 업데이트

브라우저 정의 파일은 새롭고 업데이트된 브라우저 및 장치에 대한 정보를 포함하도록 업데이트되었습니다. Netscape Navigator와 같은 오래된 브라우저와 장치는 제거되었으며 Google Chrome 및 Apple iPhone과 같은 최신 브라우저와 장치가 추가되었습니다.

응용 프로그램에 제거된 브라우저 정의 중 하나를 상속하는 사용자 지정 브라우저 정의가 포함되어 있으면 오류가 표시됩니다. 예를 들어 경우는 `App_Browsers` IE2 브라우저 정의에서 상속 되는 브라우저 정의 포함 하는 폴더, 다음 구성 오류 메시지가 표시 됩니다.

- ID가 'IE2' 인 브라우저 또는 게이트웨이 요소를 찾을 수 없습니다.

> [!NOTE]
> **HttpBrowserCapabilities** 개체 (페이지의 의해 노출 되며 **Request.Browser** 속성) 브라우저 정의 파일에 의해 이루어집니다. 따라서 ASP.NET 4에서이 개체의 속성에 액세스 하 여 반환 되는 정보는 이전 버전의 ASP.NET에 반환 되는 정보 보다 다를 수 있습니다.


다음 폴더에서 브라우저 정의 파일을 복사 하 여 이전 브라우저 정의 파일에서 되돌릴 수 있습니다.

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

에 해당 파일을 복사 `\CONFIG\Browsers` ASP.NET 4에 대 한 폴더입니다. 파일을 복사한 후 실행 Aspnet\_regbrowsers.exe 명령줄 도구입니다.

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>System.Web.Mobile.dll 루트 웹 구성 파일에서 제거

System.Web.Mobile.dll 어셈블리에 대 한 루트에 포함 된 ASP.NET의 이전 버전에서는 `Web.config` 파일에 **어셈블리** 섹션입니다. 성능 향상을 위해이 어셈블리에 대 한 참조 제거 되었습니다.

System.Web.Mobile.dll 어셈블리는 ASP.NET 4에 포함 되어 있지만 사용 되지 않습니다. System.Web.Mobile.dll 어셈블리에서 형식을 사용 하려는 경우이 어셈블리에 대 한 참조를 하거나 루트 추가 `Web.config` 파일 또는 응용 프로그램에 `Web.config` 파일입니다. 예를 들어 (deprecated) ASP.NET 모바일 컨트롤 중 하나를 사용 하려는 경우 System.Web.Mobile.dll 어셈블리에 대 한 참조를 추가 해야 합니다는 `Web.config` 파일입니다.

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>ASP.NET 요청 유효성 검사

요청 유효성 검사 기능을 ASP.NET에서 특정 수준의 교차 사이트 스크립팅 (XSS) 공격에 대 한 기본 보호를 제공합니다. 이전 버전의 ASP에서 요청 유효성 검사는 기본적으로 활성화 되었습니다. 그러나 ASP.NET 페이지에만 적용 (`.aspx` 파일 및 해당 클래스 파일) 및 해당 페이지 된 실행 하는 경우에 합니다.

ASP.NET 4에서 기본적으로 요청은에 대해 유효성 검사가 모든 요청을 하기 전에 설정 되었기 때문에 **BeginRequest** 단계 HTTP 요청입니다. 결과적으로, 요청 유효성 검사는.aspx 페이지 요청 뿐 아니라 모든 ASP.NET 리소스에 대 한 요청에 적용 됩니다. 웹 서비스 호출 및 사용자 지정 HTTP 처리기와 같은 요청이 포함 됩니다. 사용자 지정 HTTP 모듈의 HTTP 요청 내용을 읽는 경우 요청 유효성 검사 활성 이기도 합니다.

결과적으로, 요청 유효성 검사 오류 이전에 오류를 트리거하지 않은 요청에 대 한 이제 발생할 수 있습니다. 요청 유효성 검사 기능을 ASP.NET 2.0의 동작으로 되돌리려면에 다음 설정이 추가 `Web.config` 파일:

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

그러나 XSS 될 수 있는 안전 하지 않은 HTTP 입력 공격 벡터 기존 처리기, 모듈 또는 기타 사용자 지정 코드에 잠재적으로 액세스 하는지 여부를 확인 하려면 요청 유효성 검사 오류를 분석 하는 것이 좋습니다.

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>기본 해싱 알고리즘은 이제 HMACSHA256

ASP.NET은 암호화 및 해시 알고리즘을 모두 사용하여 양식 인증 쿠키 및 보기 상태와 같은 데이터를 보호합니다. 기본적으로 ASP.NET 4에 대 한 해시 작업 쿠키 및 보기 상태 HMACSHA256 알고리즘은 이제 사용합니다. 이전 버전의 ASP 이전 HMACSHA1 알고리즘을 사용 합니다.

혼합된 ASP.NET 2.0/ASP.NET 4를 실행 하는 경우 영향을 받을 수 응용 프로그램 환경 같은 폼 인증 쿠키 데이터 across.NET 프레임 워크 버전을 작동 해야 합니다. 이전 HMACSHA1 알고리즘을 사용 하도록 ASP.NET 4 웹 응용 프로그램을 구성 하려면 다음 설정에 추가 `Web.config` 파일:

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>새 ASP.NET 4 루트 구성과 관련 된 구성 오류

루트 구성 파일 (의 `machine.config` 파일과 루트 `Web.config` 파일) 대부분의 ASP.NET 3.5에서에서 발견 된 상용구 구성 정보를 포함 하도록 업데이트 되었습니다는.NET Framework 4 (및 따라서 ASP.NET 4)에 응용 프로그램 `Web.config` 파일입니다. 관리 되는 IIS 7 및 IIS 7.5 구성 시스템의 복잡성 때문에 IIS 7.5 및 IIS 7 및 ASP.NET 4에서 ASP.NET 3.5 응용 프로그램을 실행 될 수 있습니다 ASP.NET 또는 IIS 구성 오류.

가능한 경우 Visual Studio 2010에서 프로젝트 업그레이드 도구를 사용 하 여 ASP.NET 3.5 응용 프로그램을 ASP.NET 4로 업그레이드 하는 것이 좋습니다. Visual Studio 2010을 자동으로 ASP.NET 3.5 응용 프로그램의 수정 `Web.config` ASP.NET 4에 대 한 적절 한 설정을 포함 하는 파일입니다.

그러나 되기 다시 컴파일하지 않고.NET Framework 4를 사용 하 여 ASP.NET 3.5 응용 프로그램을 실행 하는 시나리오는 지원된 합니다. 수동으로 응용 프로그램을 수정 해야 할 수는 경우 `Web.config` .NET Framework 4 및 IIS 7.5 또는 IIS 7에서 응용 프로그램을 실행 하기 전에 파일입니다.

다음 두 섹션에서는 소프트웨어의 다른 조합에 대 한 확인 해야 할 수 있는 변경 내용에 설명 합니다.

**Windows Vista SP1 또는 Windows Server 2008 SP1, 핫픽스 KB958854 아니고 s p 2 설치 됩니다.** 이 구성에서 IIS 7 구성 시스템 제대로 병합 하지 응용 프로그램의 관리 되는 구성 응용 프로그램 수준 비교 하 여 `Web.config` 파일 ASP.NET 2.0을 `machine.config` 파일입니다. 이 응용 프로그램 수준으로 인해 `Web.config` 파일에서.NET Framework 3.5 이상 포함 되어야 합니다는 **system.web.extensions** IIS 7 유효성 검사 오류가 발생 순서에 구성 섹션 정의 (요소).

그러나 응용 프로그램 수준을 수동으로 수정 `Web.config` Visual Studio 2008에 도입 된 원래 상용구 구성 섹션 정의 정확 하 게 일치 하지 않는 파일 항목에는 ASP.NET 구성 오류가 발생 합니다. (Visual Studio 2008에서 생성 되는 기본 구성 항목이 제대로 작동 합니다.) 일반적인 문제는 수동으로 수정 `Web.config` 파일 그대로 남겨는 **allowDefinition** 및 **로** 다양 한 구성 섹션에 있는 구성 특성 정의 합니다. 이 인해 응용 프로그램 수준에서 약식된 구성 섹션 사이 불일치가 `Web.config` 파일 및 ASP.NET 4에서 완전 한 정의 `machine.config` 파일입니다. 결과적으로, 실행 시 ASP.NET 4 구성 시스템 구성 오류를 throw합니다.

**Windows Vista SP2, Windows Server 2008 SP2, Windows 7, Windows Server 2008 R2 및 Windows Vista s p 1도 및 KB958854 핫픽스를 설치한 Windows Server 2008 SP1**

이 시나리오에서는 IIS 7 및 IIS 7.5 네이티브 구성 시스템 오류를 반환 구성에서 텍스트 비교를 수행 하기 때문에 **형식** 관리 되는 구성 섹션 처리기에 대해 정의 된 특성입니다. 때문에 모든 `Web.config` Visual Studio 2008 및 Visual Studio 2008 s p 1에서 생성 되는 파일에 대 한 형식 문자열에 "3.5" 있습니다는 **system.web.extensions** 와 관련 구성 섹션 처리기 않기 때문에 ASP.NET 4 `machine.config` 파일에 "4.0"는 **형식** 항상 Visual Studio 2008 또는 Visual Studio 2008 s p 1에서 생성 되는 응용 프로그램에서 동일한 구성 섹션 처리기 IIS 7에서 구성 유효성 검사 실패에 대 한 특성 및 IIS 7.5입니다.

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>이러한 문제를 해결합니다.

응용 프로그램 수준을 업데이트 하는 첫 번째 시나리오에 대 한 해결 `Web.config` 파일에서 구성 상용구 텍스트를 포함 하 여는 `Web.config` Visual Studio 2008에서 자동으로 생성 된 파일입니다.

첫 번째 시나리오에 대 한 다른 해결 방법은 Vista 또는 Windows Server 2008 서비스 팩 2 컴퓨터에 설치 하거나 KB958854 핫픽스를 설치 하려면 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) 올바른 해결 하려면 IIS 구성 시스템의 구성 병합 동작입니다. 그러나 이러한 작업 중 하나를 수행 하 고 나면 응용 프로그램 두 번째 시나리오에 대해 설명 하는 문제 때문에 구성 오류를 발생 가능성이 합니다.

두 번째 시나리오에 대 한 해결 하는 삭제 하거나 모든 하는 **system.web.extensions** 구성 섹션 정 및 구성 섹션 그룹 응용 프로그램 수준에서 정의 `Web.config` 파일입니다. 이러한 정의 일반적으로 응용 프로그램 수준 맨 위에 있는 `Web.config` 파일을 식별할 수 있습니다는 **configSections** 요소와 해당 자식 요소입니다.

두 시나리오 모두에 대 한 것이 좋습니다 수동으로 삭제 하는 **system.codedom** 필요 하지 않더라도 섹션.

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 4 개의 자식 응용 프로그램 실패 시작 때 ASP.NET 2.0 또는 ASP.NET 3.5 응용 프로그램

이전 버전의 ASP.NET을 실행하는 응용 프로그램의 자식으로서 구성된 ASP.NET 4 응용 프로그램은 구성 또는 컴파일 오류로 인해 시작하지 못할 수 있습니다. 다음 예제에서는 영향을 받는 응용 프로그램에 대 한 디렉터리 구조를 보여 줍니다.

`/parentwebapp`(ASP.NET 2.0 또는 ASP.NET 3.5를 사용 하도록 구성)  
`/childwebapp`(ASP.NET 4에서 사용 하도록 구성 됨)

응용 프로그램에는 `childwebapp` 폴더 IIS 7.5 또는 IIS 7에서 시작 하 고가 구성 오류를 보고 되지 것입니다. 오류 텍스트는 다음과 같은 메시지가 포함 됩니다.

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`
  

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

IIS 6에서 응용 프로그램의 경우에 `childwebapp` 폴더를 시작 하지 못할 수는 있지만 다른 오류를 보고 합니다. 예를 들어 오류 텍스트는 다음 내용이 포함 될 수 있습니다.

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

이러한 시나리오가 발생 하기 때문에 부모 응용 프로그램에서 구성 정보는 `parentwebapp` 하위 웹에서 사용 되는 최종 병합 된 구성 설정을 결정 하는 구성 정보의 계층의 일부인 폴더 응용 프로그램에 `childwebapp` 폴더입니다. IIS 6 또는 IIS 7 (또는 IIS 7.5)에서 ASP.NET 4 웹 응용 프로그램의 실행 여부,에 따라 IIS 구성 시스템 또는 ASP.NET 4 컴파일 시스템 오류를 반환 합니다.

이 문제를 해결 하 고 자식 ASP.NET 4 응용 프로그램에서 실행 되도록 하기 위해 따라야 하는 단계는 ASP.NET 4 응용 프로그램 IIS 7 (또는 IIS 7.5)에서 IIS 6에서 또는 실행 하는지 여부에 따라 다릅니다.

### <a name="step-1-iis-7-or-iis-75-only"></a>단계 1 (IIS 7.5 또는 IIS 7)

이 단계는 Windows Vista, Windows Server 2008, Windows 7 및 Windows Server 2008 r 2를 포함 하는 IIS 7.5 또는 IIS 7을 실행 하는 운영 체제에만 필요 합니다.

이동의 **configSections** 정의에 `Web.config` 부모 응용 프로그램 (ASP.NET 2.0 또는 ASP.NET 3.5를 실행 하는 응용 프로그램)의 파일의 루트에 `Web.config` the.NET Framework 2.0에 대 한 파일입니다. IIS 7 및 IIS 7.5 native 구성 시스템 검색에서 **configSections** 구성 파일의 계층 구조를 병합할 때 요소입니다. 이동 된 **configSections** 부모 웹 응용 프로그램의 정의 `Web.config` 루트 파일 `Web.config` 파일 자식 ASP.NET 4에 대해 발생 하는 구성 병합 프로세스에서 요소를 효과적으로 숨깁니다 응용 프로그램입니다.

32 비트 응용 프로그램 풀, 루트 또는 32 비트 운영 체제에서 `Web.config` ASP.NET 2.0 및 ASP.NET 3.5에 대 한 파일은 일반적으로 다음 폴더에 있습니다.

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

64 비트 응용 프로그램 풀, 루트 또는 64 비트 운영 체제에서 `Web.config` ASP.NET 2.0 및 ASP.NET 3.5에 대 한 파일은 일반적으로 다음 폴더에 있습니다.

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

이동 해야 하는 64 비트 컴퓨터에서 32 비트 및 64 비트 웹 응용 프로그램을 실행 하는 경우는 **configSections** 루트 요소를 `Web.config` 32 비트 및 64 비트 시스템 모두에 대 한 파일입니다.

삽입 했을 때는 **configSections** 루트에 있는 요소 `Web.config` 파일, 섹션 붙여 직후는 **구성** 요소입니다. 다음 예제에서는 어떤 윗부분 루트 `Web.config` 파일은 요소를 이동 완료 했을 때 같습니다.

> [!NOTE]
> 다음 예제에서는 줄 바꿈이 가독성을 높이기 위해.


[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>(모든 버전의 IIS) 2 단계

이 단계는 ASP.NET 4 자식 웹 응용 프로그램의 실행 여부 IIS 6에서 IIS 7 (또는 IIS 7.5)에 필요 합니다.

에 `Web.config` 부모 ASP.NET 2 또는 ASP.NET 3.5를 실행 하는 웹 응용 프로그램의 파일 추가 **위치** 태그 (IIS와 ASP.NET 구성 시스템)에 대 한 명시적으로 지정 하는 구성 항목에만 부모 웹 응용 프로그램에 적용 됩니다. 다음 예에서는 구문을 보여 줍니다.는 **위치** 추가할 요소입니다.

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

다음 예제와 방법을 **위치** 태그로 시작 하는 모든 구성 섹션을 래핑할를 사용 하는 **appSettings** 섹션 해 서 끝나는 **system.webServer**섹션.

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

1 및 2 단계를 완료 하면 자식 ASP.NET 4 웹 응용 프로그램 오류 없이 시작 됩니다.

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>ASP.NET 4 웹 사이트 시작 되지 않고 SharePoint가 설치 된 컴퓨터에서

SharePoint를 실행 하는 웹 서버는 `Web.config` SharePoint 웹 사이트의 루트에 배포 되는 파일 (예를 들어 `c:\inetpub\wwwroot\web.config` 기본 웹 사이트에 대 한). 이 `Web.config` 파일을 SharePoint에서는 사용자 지정 부분 신뢰 수준을 WSS 라는\_최소화 합니다.

이러한 종류의 SharePoint 웹 사이트의 자식으로 배포 되는 ASP.NET 4 웹 사이트를 실행 하려고 하면 다음과 같은 오류가 표시 됩니다.

`Could not find permission set named 'ASP.NET'.`

이 오류는 ASP.NET 4 코드 액세스 보안 (CA) 인프라는 ASP.NET을 명명 된 권한 집합을 찾기 때문에 발생 합니다. 하지만 WSS에서 참조 되는 구성 파일의 부분 신뢰를 사용\_최소는 해당 이름 가진 모든 사용 권한 집합입니다.

현재 버전의 ASP.NET과 호환 되는 데 사용할 수 있는 SharePoint 하지는 합니다. 결과적으로, 해서는 사이트 SharePoint 웹 아래에 자식 사이트로 ASP.NET 4 웹 사이트를 실행할 수 있습니다.

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>HttpRequest.FilePath 속성은 더 이상 PathInfo 값을 포함

이전 버전의 ASP.NET 포함 한 **PathInfo** 다양 한 파일 경로 관련 된 속성을 포함 하 여에서 반환 된 값에 값 **HttpRequest.FilePath**,  **HttpRequest.AppRelativeCurrentExecutionFilePath**, 및 **HttpRequest.CurrentExecutionFilePath**합니다. ASP.NET 4에 포함 되어 더 이상는 **PathInfo** 이러한 속성에서 반환 값의 값입니다. 대신,는 **PathInfo** 정보는에서 사용할 수 있는 **HttpRequest.PathInfo**합니다. 예를 들어 다음과 같은 URL 조각을 가정해 보겠습니다.

`/testapp/Action.mvc/SomeAction`

이전 버전의 ASP.NET **HttpRequest** 속성 다음 값을 갖습니다.

**HttpRequest.FilePath**: `/testapp/Action.mvc/SomeAction`

**HttpRequest.PathInfo**: (비어 있음)

ASP.NET 4에서 **HttpRequest** 속성은 대신 다음과 같은 값을 갖습니다.

**HttpRequest.FilePath**: `/testapp/Action.mvc`

**HttpRequest.PathInfo**: `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>ASP.NET 2.0 응용 프로그램에는 eurl.axd 참조 하는 HttpException 오류가 발생할 수 있습니다

IIS 6에서 ASP.NET 4에 설정한 후 (Windows Server 2003 또는 Windows Server 2003 R2)에서 IIS 6에서 실행 되는 ASP.NET 2.0 응용 프로그램에는 다음과 같은 오류가 발생할 수 있습니다.

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

이 오류는 전달 하기 때문에 ASP.NET 웹 사이트가 ASP.NET 4에서 사용 하도록 구성 되어 있는지를 발견 하면 ASP.NET 4의 기본 구성 요소 확장명 없는 URL의 ASP.NET 관리 되는 부분을 처리 하기 위해 발생 합니다. 그러나 ASP.NET 4 웹 사이트 아래에 있는 가상 디렉터리에 ASP.NET 2.0을 사용 하도록 구성 된 경우 "eurl.axd" 문자열이 포함 된 수정된 된 URL에서이 방식으로 결과에서 확장명 없는 URL을 처리 합니다. 수정 된 URL이 ASP.NET 2.0 응용 프로그램에 전송 됩니다. ASP.NET 2.0에는 "eurl.axd" 형식을 인식할 수 없습니다. 따라서 ASP.NET 2.0을 찾으려고 이라는 파일로 내보내집니다 `eurl.axd` 하 고 실행 합니다. 그러한 파일 존재 하기 때문에 요청은 실패 하며는 **HttpException** 예외입니다.

다음 옵션 중 하나를 사용 하 여이 문제를 해결할 수 있습니다.

### <a name="option-1"></a>옵션 1

ASP.NET 4 웹 사이트를 실행 하는 데 필요 하지 않은 경우에 ASP.NET 2.0을 대신 사용 하도록 사이트를 다시 매핑하십시오.

### <a name="option-2"></a>옵션 2

ASP.NET 4을 웹 사이트를 실행 하는 데 필요한 경우 ASP.NET 2.0에 매핑되는 다른 웹 사이트에 ASP.NET 2.0 자식 가상 디렉터리를 이동 합니다.

### <a name="option-3"></a>옵션 3

실용적인을 ASP.NET 2.0 웹 사이트를 다시 매핑할 수 또는 가상 디렉터리의 위치를 변경할 수 없는 경우 명시적으로 사용 하지 않도록 설정 확장명 없는 URL을 ASP.NET 4에서 처리 합니다. 다음 절차를 따르십시오.

1. Windows 레지스트리에서 다음 노드를 엽니다.

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. 새 **DWORD** 라는 값 **EnableExtensionlessUrls**합니다.
2. 설정 **EnableExtensionlessUrls** 0입니다. 그러면 확장명 없는 URL 동작을 해제합니다.
3. 레지스트리 값을 저장 하 고 레지스트리 편집기를 닫습니다.
4. 실행 된 **iisreset** 새 레지스트리 값을 읽을 수는 iis 명령줄 도구입니다.

> [!NOTE]
> 설정 **EnableExtensionlessUrls** 1로 확장명 없는 URL 동작을 사용 합니다. 값을 지정 하는 경우 기본 설정입니다.


<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>IIS 7.5 또는 IIS 7에서 기본 문서에 이벤트 처리기 하지 발생 하지 않습니다 통합 모드

ASP.NET 4를 변경 하는 수정 작업에 포함 되어 방법을 **동작** html 특성 **양식** 확장명 없는 URL 기본 문서를 확인할 때 요소가 렌더링 됩니다. 기본 문서를 확인 하는 확장명 없는 URL의 예로 들 수 [http://contoso.com/](http://contoso.com/)로 요청을 [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)합니다.

ASP.NET 4에는 이제 HTML 렌더링 **양식** 요소의 **동작** 에 매핑되는 기본 문서가 확장명 없는 URL에 요청이 있을 때 빈 문자열 특성 값입니다. 예를 들어, ASP.NET, 요청을의 이전 릴리스에서 [http://contoso.com](http://contoso.com) 요청을 초래 `Default.aspx`합니다. 해당 문서의 여 **양식** 태그는 다음 예제와 같이 렌더링 됩니다.

`<form action="Default.aspx" />`

ASP.NET 4에서 요청을 [http://contoso.com](http://contoso.com) 또한 요청을 발생 `Default.aspx`합니다. 그러나 이제 ASP.NET: 여는 HTML을 렌더링 **양식** 다음 예제와 같이 태그:

`<form action="" />`

이러한 차이 방식에이 따라 **동작** 특성이 렌더링 폼 게시 IIS 및 ASP.NET에서 처리 되는 방식 약간 변경 될 수 있습니다. 경우는 **동작** 특성은 빈 문자열을 IIS **DefaultDocumentModule** 개체 자식 요청을 만들어집니다 `Default.aspx`합니다. 대부분의 경우이 자식 요청은 응용 프로그램 코드에 투명 하 게 및 `Default.aspx` 페이지는 정상적으로 실행 합니다.

그러나 관리 코드와 IIS 7 또는 IIS 7.5 통합 모드 간의 잠재적 상호 작용으로 인해 관리되는 .aspx 페이지가 자식 요청 중에 제대로 작동하지 않을 수 있습니다. 하는 경우 다음 조건이 발생할 자식 요청을 한 `Default.aspx` 문서 오류 또는 예기치 않은 동작이 발생 합니다.

1. .Aspx 페이지와 브라우저로 전송 되는 **양식** 요소의 **동작** 특성이로 설정 ""입니다.
2. 폼이 ASP.NET에 다시 게시 합니다.
3. 관리 되는 HTTP 모듈 엔터티 본문의 특정 부분을 읽습니다. 예를 들어 모듈 읽고 **Request.Form** 또는 **Request.Params**합니다. 이렇게 하면 POST 요청의 엔터티 본문이 관리되는 메모리로 읽힙니다. 결과적으로 IIS 7 또는 IIS 7.5 통합 모드에서 실행 중인 모든 네이티브 코드 모듈에서 더 이상 엔터티 본문을 사용할 수 없습니다.
4. IIS **DefaultDocumentModule** 개체 결국를 실행 하 고는 자식 요청을 만듭니다는 `Default.aspx` 문서. 그러나 엔터티 본문은 이미 관리 코드에 의해 읽혔기 때문에 자식 요청에 보낼 수 있는 엔터티 본문이 없습니다.
5. 자식 요청에 대 한 처리기에 대 한 HTTP 파이프라인을 실행 하는 경우 `.aspx` handler-execute 단계 동안 파일을 실행 합니다.
6. 엔터티 본문이 이기 때문에 없는 폼 변수 및 뷰 상태가 없는 비워진 발생 해야 어떤 이벤트 (있는 경우)을 확인 하려면.aspx 페이지 처리기에 사용할 수 있는 이므로 합니다. 그 결과, 영향을 받는 .aspx 페이지의 포스트백 이벤트 처리기는 실행되지 않습니다.

다음과 같은 방법으로이 문제를 해결할 수 있습니다.

- 기본 문서를 요청 하는 동안 요청의 엔터티 본문에 액세스 하는 HTTP 모듈을 식별 하 고 관리 되는 요청에 대해서만 실행 되도록 구성할 수 수 있는지 여부를 결정 합니다. IIS 7 및 IIS 7.5 모두에 대해 통합된 모드의 경우 HTTP 모듈에서 모듈에 다음 특성을 추가 하 여 관리 되는 요청에 대해서만 실행 되도록 표시할 수 있습니다 **system.webServer/modules** 항목:

- `precondition="managedHandler"`

- 이 설정을 해제 합니다. 모듈에 대 한 요청 IIS 7 및 IIS 7.5 아닌 것으로 확인 요청을 관리 합니다. 기본 문서 요청에 대 한 확장명 없는 URL에 첫 번째 요청이입니다. 따라서 IIS로 실행 되지 않아 표시 되는 모든 관리 되는 모듈을 관리 되는 처리기의 전제 조건 초기 요청 처리 중입니다. 결과적으로, 실수로 관리 되는 모듈 엔터티 본문을 읽지 않습니다 하 고 엔터티 본문을 계속 사용할 수 기본 문서와 자식 요청에 따라 전달 됩니다.

- 문제가 있는 HTTP 모듈을 모든 요청에 대해 실행 해야 하는 경우 (정적 파일을 확인 하는 확장명 없는 Url에 대 한는 **DefaultDocumentModule** 등 관리 되는 요청에 대 한 개체), 여 영향을 받는.aspx 페이지를 명시적으로 수정 설정의 **작업** 속성 페이지의 **System.Web.UI.HtmlControls.HtmlForm** 비어 있지 않은 문자열을 제어 합니다. 예를 들어, 기본 문서는 `Default.aspx`, 명시적으로 설정 하는 페이지의 코드를 수정 된 **htmlform에서** 컨트롤의 **작업** 속성을 "Default.aspx"입니다.

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>ASP.NET 코드 액세스 보안 (CA) 구현에 대 한 변경

ASP.NET 2.0 및 확장에 의해 3.5에 추가 된 ASP.NET 기능.NET Framework 1.1 및 2.0 코드 액세스 보안 (CA) 모델을 사용 합니다. 그러나 ASP.NET 4의 CAS 구현은 크게 개선되었습니다. 결과적으로, 전역 어셈블리 캐시 (GAC)에서 실행 되는 신뢰할 수 있는 코드를 사용 하는 부분 신뢰 ASP.NET 응용 프로그램은 다양 한 보안 예외 실패할 수 있습니다. 시스템 수준의 정책에 광범위 하 게 수정 작업을 사용 하는 부분 신뢰 응용 프로그램 보안 예외와도 실패할 수 있습니다.

부분 신뢰 ASP.NET 4 응용 프로그램 동작에 ASP.NET 1.1 및 2.0을 사용 하 여 새 되돌릴 수 **legacyCasModel** 특성에 **신뢰** 다음 예제와 같이 구성 요소 :

`<trust level= "Medium" legacyCasModel="true" />`

레거시 CAS 모델 돌아갈 때 다음 이전 CA 동작은 활성화 됩니다.

- 컴퓨터 CAS 정책이 적용 됩니다.
- 단일 응용 프로그램 도메인에 여러 개의 서로 다른 권한 집합이 허용 됩니다.
- 명시적 사용 권한을 어설션 스택에 ASP.NET 또는 다른.NET Framework 코드 때 호출 되는 GAC의 어셈블리에 대 한 필요 하지 않습니다.

.NET Framework 4에 한 가지 시나리오를 되돌릴 수 없습니다: 비 웹 부분 신뢰 응용 프로그램 System.Web.dll 및 System.Web.Extensions.dll의 특정 Api를 더 이상 호출할 수 없습니다. 이전 버전의.NET Framework에서는 비 웹 부분 신뢰 응용 프로그램에서 명시적으로 부여 된 **AspNetHostingPermission** 사용 권한. 이러한 응용 프로그램에 사용 하 여 수 **System.Web.HttpUtility**에 **System.Web.ClientServices.\***  네임 스페이스 및 형식 멤버 자격, 역할 및 프로필 관련이 있습니다. 비 웹 부분 신뢰 응용 프로그램에서 이러한 형식을 호출 하는 더 이상.NET Framework 4에서 지원 됩니다.

> [!NOTE]
> **HtmlEncode** 및 **HtmlDecode** 의 기능은 **System.Web.HttpUtility** 클래스 새.NET Framework 4로 옮겨진  **System.Net.WebUtility** 클래스입니다. 응용 프로그램의 코드에서 새를 수정 하는 유일한 ASP.NET 기능을 사용 하는 동안 있는 되었으면 **WebUtility** 클래스를 대신 합니다.


다음은 ASP.NET 4에 있는 기본 CA 구현으로 변경 내용을 상위 수준 요약입니다.

- ASP.NET 응용 프로그램 도메인은 이제 유형이 같은 응용 프로그램 도메인입니다. 응용 프로그램 도메인 부분 신뢰 및 완전 신뢰 권한 부여 집합에만 사용할 수 있습니다.
- ASP.NET 부분 신뢰 권한 부여 집합은 모든 엔터프라이즈 수준, 컴퓨터 수준 또는 사용자 수준의 CAS 정책 별개입니다.
- ASP.NET 어셈블리 3.5 및 3.5 s p 1에서 제공 되는.NET Framework 4 투명도 모델을 사용 하도록 변환 되었습니다.
- ASP.NET의 사용 **AspNetHostingPermission** 특성 상당히 감소 되었습니다. 대부분의 경우가이 특성의 공용 ASP.NET Api에서 제거 되었습니다.
- ASP.NET 빌드 공급자가 만든 동적으로 컴파일된 어셈블리 명시적으로 투명으로 어셈블리를 표시 하도록 업데이트 되었습니다.
- 모든 ASP.NET 어셈블리는 APTCA 특성이 웹 호스팅 환경에만 적용 되는 방식에서으로 표시 됩니다. 부분적으로 신뢰할 수 있는 비 웹 호스팅 환경 ClickOnce 예: ASP.NET 어셈블리를 호출할 수 없습니다.

새 ASP.NET 4 코드 액세스 보안 모델에 대 한 자세한 내용은 참조 [ASP.NET 응용 프로그램의 코드 액세스 보안 사용 하 여](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx) MSDN 웹 사이트에 있습니다.

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>이동 된 MembershipUser 및 System.Web.Security Namespace의 다른 형식

ASP.NET 멤버 자격에 사용 되는 일부 형식에서 이동 된 `System.Web.dll` 새 System.Web.ApplicationServices.dll 어셈블리에 있습니다. 클라이언트 형식 및 확장된 .NET Framework SKU 형식 간 아키텍처 계층화 종속성을 해결하기 위해 형식을 이동했습니다.

웹 사이트 프로젝트 System.Web.ApplicationServices.dll ASP.NET 컴파일 시스템에서 기본적으로 사용 되는 참조 된 어셈블리 목록에 추가 되었기 때문에 이러한 형식에 이동 했기 때문에 문제를 갖지 않습니다. Visual Studio 2010에서 열어 이전 버전의 ASP.NET을 ASP.NET 4 사용 하 여 만든 웹 사이트 프로젝트를 업그레이드 하는 경우 프로젝트가 오류 없이 컴파일됩니다.

마찬가지로, Visual Studio 2010에서 열어 이전 버전의 ASP.NET을 ASP.NET 4에서 만든 웹 응용 프로그램 프로젝트를 업그레이드 하는 경우 업그레이드 프로세스는 프로젝트에 System.Web.ApplicationServices.dll에 대 한 참조를 추가 합니다. 따라서 웹 오류 없이 컴파일됩니다 응용 프로그램 프로젝트를 업그레이드 합니다.

또한이 이전 버전의 ASP.NET 사용 하 여 만든 컴파일된 (이진) 파일은 구성원 형식을 다른 어셈블리를 이동 하는 경우에 ASP.NET 4에서 오류 없이 실행 됩니다. ASP.NET 4 버전에 추가한 형식 정보를 전달 `System.Web.dll` 하는 자동으로 이러한 형식에 대 한 런타임 참조 유형에 대 한 새 위치에 라우팅합니다.

그러나 특정 구성원 자격 종류를 사용 하 고 이전 버전의 ASP.NET에서 업그레이드 한 클래스 라이브러리는 ASP.NET 4 프로젝트에서 사용 될 때 컴파일되지 못합니다. 예를 들어, 클래스 라이브러리 프로젝트를 컴파일하고 다음과 같은 오류를 보고 하려면 실패할 수 있습니다.

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
  

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

System.Web.ApplicationServices.dll를 클래스 라이브러리 프로젝트에 대 한 참조를 추가 하 여이 문제를 해결할 수 있습니다.

다음 목록에서는 *System.Web.Security* 형식에서 이동 된 `System.Web.dll` System.Web.ApplicationServices.dll에:

- *System.Web.Security.MembershipCreateStatus*
- *System.Web.Security.Membership.CreateUserException*
- *System.Web.Security.MembershipPasswordException*
- *System.Web.Security.MembershipPasswordFormat*
- *System.Web.Security.MembershipProvider*
- *System.Web.Security.MembershipProviderCollection*
- *System.Web.Security.MembershipUser*
- *System.Web.Security.MembershipUserCollection*
- *System.Web.Security.MembershipValidatePasswordEventHandler*
- *System.Web.Security.ValidatePasswordEventArgs*
- *System.Web.Security.RoleProvider*
- <a id="0.1_a"></a>*System.Web.Configuration.MembershipPasswordCompatibilityMode*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>출력 캐싱 변경 내용을 변경 하려면 \* HTTP 헤더

ASP.NET 1.0에서 버그로 인해 캐시 된 페이지를 지정 하는 `Location="ServerAndClient"` 내보낼 수는 출력 캐시 설정으로는 `Vary:*` 응답에서 HTTP 헤더입니다. 이로 인해 클라이언트 브라우저가 페이지를 로컬에 캐시하지 못했습니다.

ASP.NET 1.1에서의 **System.Web.HttpCachePolicy.SetOmitVaryStar** 를 표시 하지 않는 호출할 수 있는 메서드를 추가 `Vary:*` 헤더입니다. 이 메서드는 잠재적으로 중요 고려 되었지만 내보낸된 HTTP 헤더를 변경 때문에 선택 되었습니다 변화 합니다. 그러나 개발자가 되었습니다 헷 갈리 시 asp.net에서 동작 하 고 버그 보고서에 따르면 개발자는 기존 인식 하지 **SetOmitVaryStar** 동작 합니다.

ASP.NET 4에서 근본적인 문제 해결에 대 한 결정이. `Vary:*` HTTP 헤더는 더 이상 다음 지시문을 지정 하는 응답에서 내보내집니다.

`<%@OutputCache Location="ServerAndClient" %>`

결과적으로, **SetOmitVaryStar** 표시 하지 않기 위해 더 이상 필요 없는 `Vary:*` 헤더입니다.

지정 하는 응용 프로그램에서 `Location="ServerAndClient"` 에 **@ OutputCache** 페이지 지시문 표시 이름의 사용 권한에 포함 된 동작의 **위치** 특성의 값 즉, 페이지 됩니다 호출 하는 요구 하지 않고 브라우저에서 캐시할 수는 **SetOmitVaryStar** 메서드.

응용 프로그램의 페이지를 내보내야 하는 경우 `Vary:*`, 호출 된 **AppendHeader** 다음 예제와 같이 메서드:

`HttpResponse.AppendHeader("Vary","*");`

출력 캐싱을의 값을 변경할 수 또는 **위치** 특성을 "Server"입니다.

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Passport System.Web.Security 유형은 사용 되지 않음

Passport (이제 live Id)의 변경으로 인해 몇 년 동안 더 이상 지원 되지 않는 ASP.NET 2.0에서 작성 된 Passport 지원이 되었습니다. 5 가지 종류의 Passport 결과적으로, 관련 **System.Web.Security** 이제로 표시 됩니다는 **ObsoleteAttribute** 특성입니다.

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>MenuItem.PopOutImageUrl 속성 ASP.NET 4에에서 있는 이미지를 렌더링 하지 못함

ASP.NET 3.5에서는 *MenuItem.PopOutImageUrl* 속성을 사용 하면 메뉴 항목에 동적 하위 메뉴가 있음을 나타내기 위해 메뉴 항목에 표시 되는 이미지에 대 한 URL을 지정할 수 있습니다. 다음 예제에는 ASP.NET 3.5에서 태그에서이 속성을 지정 하는 방법을 보여 줍니다.

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

ASP.NET 4의 디자인 변경으로 인해 불일치 출력에 대해 렌더링 되는 *PopOutImageUrl* 속성에 대 한는 *MenuItem* 클래스입니다. 직접 이미지 URL을 지정 해야 하는 대신,는 *메뉴* 중 하나를 사용 하 여 제어는 *StaticPopOutImageUrl* 속성 또는 *DynamicPopOutImageUrl* 속성입니다. 정적 메뉴를 사용 하 여 작업할 때의 *Menu.StaticPopOutImageUrl* 속성 다음 예제와 같이 정적 메뉴 항목에는 하위 메뉴를 표시 하기 위해 표시 되는 이미지에 대 한 URL을 지정 합니다.

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

동적 메뉴를 사용 하는 경우 사용 된 *Menu.DynamicPopOutImageUrl* 속성을 통해 동적 메뉴 항목에 하위 메뉴가 있음을 나타내는 이미지에 대 한 URL을 지정 합니다. 다음 예제는 이전 쿼리와 비슷하지만 있지만 설정 하는 방법을 보여 줍니다.는 *DynamicPopOutImageUrl* 동적 메뉴에 대 한 속성.

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

경우는 *Menu.DynamicPopOutImageUrl* 속성이 설정 되지 않은 및 *Menu.DynamicEnableDefaultPopOutImage* 속성이 *false*, 이미지가 표시 되지 않습니다. 마찬가지로, 하는 경우는 *StaticPopOutImageUrl* 속성이 설정 되지 않은 및 *StaticEnableDefaultPopOutImage* 속성이 *false*, 이미지가 표시 되지 않습니다.

이러한 속성에 대 한 경로 설정 하면 백슬래시 대신 슬래시 (/) 사용 (\)합니다. 자세한 내용은 참조 [렌더링 이미지 때 경로 포함 백슬래시를 Menu.DynamicPopOutImageUrl 실패 하 게 되며 Menu.StaticPopOutImageUrl](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu.StaticPopOutImageUrl_and_Menu 합니다.") 이 문서의.

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>경로가 백슬래시를 포함 하는 경우 이미지를 렌더링 하 Menu.StaticPopOutImageUrl 및 Menu.DynamicPopOutImageUrl 실패

ASP.NET 4에서 사용 하 여 지정 하는 이미지는 *Menu.StaticPopOutImageUrl* 및 *Menu.DynamicPopOutImageUrl* 속성 경로 backlashes 있으면 렌더링 되지 것입니다 (\)합니다. 이것은 이전 버전의 ASP.NET에서 변경 합니다.

다음 예제에서는 *메뉴* 태그 표시 제어는 *StaticPopOutImageUrl* 백슬래시를 포함 하는 경로 사용 하 여 설정할 속성입니다. ASP.NET 4의 속성에 지정 된 이미지 렌더링 되지 않습니다.

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

이 문제를 해결 하려면에 지정 된 경로 값 변경의 *StaticPopOutImageUrl* 및 *DynamicPopOutImageUrl* 슬래시 (/)를 사용 하는 속성입니다. 다음 예제에서는이 변경 내용을 보여 줍니다.

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

이전 버전의 ASP.NET을 ASP.NET 4에서 마이그레이션된 응용 프로그램 있을 수 있습니다도 영향을 받지 때문에 *MenuItem.PopOutImageUrl* 속성이 변경 되었습니다. 자세한 내용은 참조 [ASP.NET 4에 있는 이미지를 렌더링 하지 못함 MenuItem.PopOutImageUrl 속성](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem.PopOutImageUrl_Propert") 이 문서의.

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.

Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.

다른 설명이 없는 한, 용례에 사용된 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 등은 실제 데이터가 아닙니다. 어떠한 실제 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.

© 2010 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
