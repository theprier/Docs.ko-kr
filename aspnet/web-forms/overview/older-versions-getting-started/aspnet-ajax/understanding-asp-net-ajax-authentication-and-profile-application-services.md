---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: ASP.NET AJAX 인증 및 프로필 응용 프로그램 서비스 이해 | Microsoft Docs
author: scottcate
description: 인증 서비스 사용자가 인증 쿠키를 수신 하기 위해 자격 증명을 제공할 수 있으며 사용자를 허용 하려면 게이트웨이 서비스는...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2008
ms.topic: article
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: 323fec56f18281b5b5a3d312a2e4c4c7133e3f03
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393063"
---
<a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>ASP.NET AJAX 인증 및 프로필 응용 프로그램 서비스 이해
====================
[Scott Cate](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> 인증 서비스를 사용 하면 사용자가 인증 쿠키를 받으려면 자격 증명을 제공 하 고 ASP.NET에서 사용자 지정 사용자 프로필을 허용 하도록 게이트웨이 서비스를 제공 됩니다. ASP.NET AJAX 인증 서비스의 사용 하 여 표준 ASP.NET 폼 인증을 사용 하 여 호환 이므로 현재 폼 인증을 사용 하 여 응용 프로그램 (예: 로그인을 사용 하 여 제어)를 분리할 수 없는 AJAX 인증 서비스를 업그레이드 하 여 합니다.


## <a name="introduction"></a>소개

Microsoft는 많은 환경 업그레이드;.NET Framework 3.5의 일부로 제공 뿐만 아니라 새 개발 환경을 사용할 수 있지만 새로운 LINQ (Language-Integrated Query) 기능 및 향상 된 다른 언어 기능을 곧 출시 됩니다. 또한 몇 가지 친숙 한 기타 도구 집합, 특히 ASP.NET AJAX 확장 기능의.NET Framework 기본 클래스 라이브러리의 최상위 클래스 구성원으로 포함 되 고 됩니다. 이러한 확장 페이지의 부분 렌더링을 포함 하 여 전체 페이지 새로 고침 (ASP.NET 프로 파일링 API 포함), 클라이언트 스크립트 및 광범위 한 클라이언트 쪽 API를 통해 웹 서비스에 액세스 하는 기능을 요구 하지 않고 새로운 많은 리치 클라이언트 기능을 사용 하도록 설정 다양 한 ASP.NET 서버측 컨트롤 집합에서 표시 하는 컨트롤 스키마를 반영 하도록 설계 되었습니다.

이 백서를 구현 하 고 ASP.NET 프로 파일링의 사용을 살펴봅니다 하 고 폼 인증 서비스의 Microsoft ASP.NET AJAX ExtensionsThe AJAX 확장에 의해 노출 되는 대로 폼 인증으로 지원 하기가 무척 쉬워집니다 (물론 프로 파일링 서비스) 웹 서비스 프록시 스크립트를 통해 노출 됩니다. AJAX Extensions는 AuthenticationServiceManager 클래스를 통해 사용자 지정 인증도 지원 합니다.

이 백서는 Visual studio 2008 베타 2 릴리스 및.NET Framework 3.5를 기반으로 합니다. 이 백서는 또한 Visual Studio 2008 베타 2를 하지 Visual Web Developer Express를 사용 하는 Visual Studio의 사용자 인터페이스에 따라 연습을 제공 하는 가정 합니다. 몇 가지 코드 샘플에는 Visual Web Developer Express에서 사용할 수 없는 프로젝트 템플릿을 사용할 수 있습니다.

## <a name="profiles-and-authentication"></a>*프로필 및 인증*

Microsoft ASP.NET 프로필 및 인증 서비스는 ASP.NET 폼 인증 시스템에서 제공 하는 ASP.NET의 표준 구성 요소는 합니다. ASP.NET AJAX Extensions 스크립트 클라이언트 AJAX 라이브러리의 Sys.Services 네임 스페이스에서 상당히 간단한 모델을 통해 스크립트 프록시를 통해 이러한 서비스에 대 한 액세스를 제공합니다.

인증 서비스를 사용 하면 사용자가 인증 쿠키를 받으려면 자격 증명을 제공 하 고 ASP.NET에서 사용자 지정 사용자 프로필을 허용 하도록 게이트웨이 서비스를 제공 됩니다. ASP.NET AJAX 인증 서비스의 사용 하 여 표준 ASP.NET 폼 인증을 사용 하 여 호환 이므로 현재 폼 인증을 사용 하 여 응용 프로그램 (예: 로그인을 사용 하 여 제어)를 분리할 수 없는 AJAX 인증 서비스를 업그레이드 하 여 합니다.

프로필 서비스에 자동으로 통합 및 인증 서비스에 의해 제공 된 멤버 자격에 따라 사용자 데이터 저장을 허용 합니다. Web.config 파일에 의해 저장 된 데이터를 지정 하 고 다양 한 프로 파일링 서비스 공급자 데이터 관리를 처리 합니다. 인증 서비스와 마찬가지로 AJAX 프로필 서비스는 표준 ASP.NET 프로필 서비스와 호환 되므로 현재 ASP.NET 프로필 서비스의 기능을 통합 하는 페이지는 AJAX 지원을 포함 하 여 분리할 수 없는.

ASP.NET 인증 및 프로 파일링 서비스 자체를 응용 프로그램 통합이 백서에서는 범위를 벗어납니다. 항목에 대 한 자세한 내용은 MSDN 라이브러리 참조 문서에서 사용 하 여 멤버 자격에서 사용자 관리를 참조 [ https://msdn.microsoft.com/library/tw292whz.aspx ](https://msdn.microsoft.com/library/tw292whz.aspx)합니다. ASP.NET에는 ASP.NET 멤버 자격에 대 한 기본 인증 서비스 공급자는 SQL Server를 사용 하 여 멤버 자격을 자동으로 설정 하는 유틸리티도 포함 됩니다. 자세한 내용은 ASP.NET SQL Server 등록 도구 문서를 참조 하세요. (Aspnet\_regsql.exe)에서 [ https://msdn.microsoft.com/library/ms229862(vs.80).aspx ](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)합니다.

## <a name="using-the-aspnet-ajax-authentication-service"></a>*ASP.NET AJAX 인증 서비스를 사용 하 여*

Web.config 파일에는 ASP.NET AJAX 인증 서비스를 사용 해야 합니다.

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

인증 서비스 사용 하도록 ASP.NET 폼 인증 필요 하며 쿠키 (스크립트를 사용할 수 없습니다 쿠키 없는 세션 쿠키 없는 세션 URL 매개 변수가 필요 하므로) 클라이언트 브라우저에서 사용 하도록 설정 합니다.

AJAX 인증 서비스를 활성화 및 구성 되 면 클라이언트 스크립트는 Sys.Services.AuthenticationService 개체를 즉시 걸릴 수 있습니다. 클라이언트 스크립트를 활용 하기 위해 주로 할 합니다 `login` 메서드 및 `isLoggedIn` 속성입니다. 기본값을 제공 하기는 많은 수의 매개 변수를 허용할 수 있는 로그인 메서드에 대 한 몇 가지 속성이 있습니다.

*Sys.Services.AuthenticationService 멤버*

*로그인 방법:*

Login () 메서드는 사용자의 자격 증명을 인증 하는 요청을 시작 합니다. 이 메서드는 비동기적 이며 실행을 차단 하지 않습니다.

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| userName | 필수. 사용자 이름 인증입니다. |
| 암호 | 옵션 (기본값은 null)입니다. 사용자의 암호입니다. |
| isPersistent | 선택 사항 (기본값은 false)입니다. 여부 사용자의 인증 쿠키는 세션 간에 유지 되어야 합니다. False 인 경우 사용자가 로그 아웃 브라우저 닫히거나 세션이 만료 되 면 합니다. |
| redirectUrl | 옵션 (기본값은 null)입니다. 인증이 성공 하면 브라우저를 리디렉션할 대상 URL입니다. 이 매개 변수가 null 이거나 빈 문자열 이면 리디렉션되지 않습니다 발생 합니다. |
| customInfo | 옵션 (기본값은 null)입니다. 이 매개 변수 현재 사용 되지 않으며 나중에 사용 하기 위해 예약 됩니다. |
| loginCompletedCallback | 옵션 (기본값은 null)입니다. 성공적으로 완료 될 때 호출할 함수입니다. 를 지정 하는 경우이 매개 변수는 defaultLoginCompleted 속성을 재정의 합니다. |
| failedCallback | 옵션 (기본값은 null)입니다. 로그인에 실패 한 경우 호출 하는 함수입니다. 를 지정 하는 경우이 매개 변수는 defaultFailedCallback 속성을 재정의 합니다. |
| userContext | 옵션 (기본값은 null)입니다. 콜백 함수에 전달 되어야 하는 사용자 컨텍스트 데이터입니다. |

*값을 반환 합니다.*

이 함수는 반환 값을 포함 하지 않습니다. 그러나 여러 동작을이 함수에 대 한 호출 완료 시 포함 됩니다.

- 현재 페이지 새로 고칠 수 있거나 또는 변경할 수는 `redirectUrl` 매개 변수를 null도 아니고 빈 문자열입니다.
- 그러나 이면 매개 변수를 null 또는 빈 문자열인 경우 합니다 `loginCompletedCallback` 매개 변수 또는 `defaultLoginCompletedCallback` 속성 이라고 합니다.
- 웹 서비스 호출에 실패 하는 경우는 `failedCallback` 의 매개 변수 `defaultFailedCallback` 속성 이라고 합니다.

*로그 아웃 메서드:*

Logout() 메서드는 자격 증명 쿠키를 제거 하 고 웹 응용 프로그램에서 현재 사용자 로그 아웃 합니다.

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| redirectUrl | 옵션 (기본값은 null)입니다. 인증이 성공 하면 브라우저를 리디렉션할 대상 URL입니다. 이 매개 변수가 null 이거나 빈 문자열 이면 리디렉션되지 않습니다 발생 합니다. |
| logoutCompletedCallback | 옵션 (기본값은 null)입니다. 로그 아웃 성공적으로 완료 될 때 호출할 함수입니다. 를 지정 하는 경우이 매개 변수는 defaultLogoutCompleted 속성을 재정의 합니다. |
| failedCallback | 옵션 (기본값은 null)입니다. 로그인에 실패 한 경우 호출 하는 함수입니다. 를 지정 하는 경우이 매개 변수는 defaultFailedCallback 속성을 재정의 합니다. |
| userContext | 옵션 (기본값은 null)입니다. 콜백 함수에 전달 되어야 하는 사용자 컨텍스트 데이터입니다. |

*값을 반환 합니다.*

이 함수는 반환 값을 포함 하지 않습니다. 그러나 여러 동작을이 함수에 대 한 호출 완료 시 포함 됩니다.

- 현재 페이지 새로 고칠 수 있거나 또는 변경할 수는 `redirectUrl` 매개 변수를 null도 아니고 빈 문자열입니다.
- 그러나 이면 매개 변수를 null 또는 빈 문자열인 경우 합니다 `logoutCompletedCallback` 매개 변수 또는 `defaultLogoutCompletedCallback` 속성 이라고 합니다.
- 웹 서비스 호출에 실패 하는 경우는 `failedCallback` 의 매개 변수 `defaultFailedCallback` 속성 이라고 합니다.

*defaultFailedCallback 속성 (get, set):*

이 속성을 호출 해야 웹 서비스와 통신 오류가 발생 하는 함수를 지정 합니다. 대리자 (또는 함수 참조) 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음과 같은 시그니처가 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| 오류 | 오류 정보를 지정합니다. |
| userContext | 로그인 또는 로그 아웃 함수가 호출 되었을 때 제공 하는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultLoginCompletedCallback 속성 (get, set):*

이 속성 로그인 웹 서비스 호출이 완료 될 때 호출 해야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조) 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음과 같은 시그니처가 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| validCredentials | 사용자 올바른 자격 증명을 제공 하는지 여부를 지정 합니다. `true` 사용자가 성공적으로;에서 기록 하는 경우 그렇지 않으면 `false`합니다. |
| userContext | Login 함수를 호출한 경우에 제공 하는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultLogoutCompletedCallback 속성 (get, set):*

이 속성 로그 아웃 웹 서비스 호출이 완료 될 때 호출 해야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조) 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음과 같은 시그니처가 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| 결과 | 이 매개 변수는 항상 됩니다 `null`; 나중에 사용 하도록 예약 되어 있습니다. |
| userContext | Login 함수를 호출한 경우에 제공 하는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*isLoggedIn 속성 (get):*

이 속성은 사용자의 현재 인증 상태를 가져옵니다. 페이지 요청 중 ScriptManager 개체에 의해 설정 됩니다.

이 속성은 반환 `true` 반환이 고, 그렇지 않으면 사용자가 로그인 한 현재, `false`합니다.

*경로 속성 (get, set):*

이 속성은 프로그래밍 방식으로 인증 웹 서비스의 위치를 결정 합니다. 기본 인증 공급자 뿐만 아니라 하나를 재정의할 수 ScriptManager 컨트롤의 AuthenticationService 자식 노드의 경로 속성에 선언적으로 설정 (자세한 내용은 참조를 사용 하 여 사용자 지정 인증 서비스 공급자 항목 아래)입니다.

기본 인증 서비스의 위치는 변경 되지 않는 참고 합니다. 그러나 ASP.NET AJAX를 사용 하는 ASP.NET AJAX 인증 서비스 프록시와 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.

또한이 속성을 현재 사이트에서 스크립트 요청을 전달 하는 값을 설정할 해야 note 합니다. 현재 응용 프로그램 인증 자격 증명을 수신할 수 없습니다, 있으므로 것이 의미가 없습니다. 또한 기술 기본 AJAX 교차 사이트 요청을 게시 해야 하 고 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.

이 속성은 한 `String` 인증 웹 서비스에 경로 나타내는 개체입니다.

*timeout 속성 (get, set):*

이 속성의 인증 서비스 로그인 요청을 가정 하기 전에 대기할 시간 길이 실패 했습니다. 결정 합니다. 호출이 완료 되기를 기다리는 동안 제한 시간이 만료 되 면 요청이 실패 콜백을 호출 될 및 호출이 완료 되지 않습니다.

이 속성은 한 `Number` 인증 서비스에서 결과 기다릴 밀리초 수를 나타내는 개체입니다.

*인증 서비스에 로그인 하는 코드 샘플:*

다음 태그는 login 및 logout 메서드 AuthenticationService 클래스의 간단한 스크립트 호출을 사용 하 여 ASP.NET 페이지 예제입니다.

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>ASP.NET AJAX 통한 데이터 프로 파일링에 액세스

서비스 프로 파일링 ASP.NET은 또한 ASP.NET AJAX Extensions를 통해 노출 됩니다. ASP.NET 프로 파일링 서비스 사용자 데이터 저장 및 검색에 사용 되는 강력 하 고 세부적인 API에서 제공 되므로 탁월한 생산성 도구를 수 있습니다.

프로필 서비스 web.config;에서 사용할 수 있어야 합니다. 기본적으로 아닙니다. 이렇게 하려면는 `profileService` 자식 요소에 사용할 수 = true에 지정 된 web.config 및 읽거나 다음과 같이 작성 되는 속성 수 지정:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

프로필 서비스도 구성 되어야 합니다. 프로 파일링 서비스의 구성을이 백서의 범위 밖에 있는 경우에 그룹 프로필 구성 설정에 정의 된 대로 그룹 이름의 하위 속성으로 액세스할 수 있는지 확인 하는 것이 좋습니다. 예를 들어 지정 된 다음 프로필 섹션:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

클라이언트 스크립트 이름, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, 및 BackgroundColor ProfileService 클래스의 속성 필드의 속성으로 액세스할 수는 있습니다.

AJAX 프로 파일링 서비스 구성 되 면; 페이지에서 즉시 사용할 수는 그러나 사용 하기 전에 한 번 로드 해야 합니다.

*Sys.Services.ProfileService 멤버*

*속성 필드:*

속성 필드는 점 연산자 이름 규칙을 통해 참조 될 수 있는 자식 속성으로 모든 구성 된 프로필 데이터를 노출 합니다. 속성 그룹의 자식 속성 GroupName.PropertyName 라고 합니다. 사용자의 상태를 가져오려면 위의 예제에서는 프로필 구성에 다음 식별자를 사용할 수 있습니다.

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*메서드를 로드 합니다.*

서버에서 선택한 목록 또는 모든 속성을 로드합니다.

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| propertyNames | 옵션 (기본값은 null)입니다. 서버에서 로드할 속성입니다. |
| loadCompletedCallback | 옵션 (기본값은 null)입니다. 로드가 완료 될 때 호출할 함수입니다. |
| failedCallback | 옵션 (기본값은 null)입니다. 오류가 발생 하면 호출할 함수입니다. |
| userContext | 옵션 (기본값은 null)입니다. 콜백 함수에 전달할 컨텍스트 정보입니다. |

Load 함수에는 반환 값이 없습니다. 경우 호출이 성공적으로 완료를 호출 하거나 합니다 `loadCompletedCallback` 매개 변수 또는 `defaultLoadCompletedCallback` 속성입니다. 호출에 실패 하거나 제한 시간이 만료 되거나 합니다 `failedCallback` 매개 변수 또는 `defaultFailedCallback` 속성 호출 됩니다.

경우는 `propertyNames` 매개 변수를 지정 하지 않으면, 모든 읽기 구성 속성 서버에서 검색 됩니다.

*메서드를 저장 합니다.*

Save () 메서드를 사용자의 ASP.NET 프로필에 지정 된 속성 목록 (또는 모든 속성)를 저장합니다.

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| propertyNames | 옵션 (기본값은 null)입니다. 서버에 저장할 속성입니다. |
| saveCompletedCallback | 옵션 (기본값은 null)입니다. 저장할 때 호출할 함수를 완료 했습니다. |
| failedCallback | 옵션 (기본값은 null)입니다. 오류가 발생 하면 호출할 함수입니다. |
| userContext | 옵션 (기본값은 null)입니다. 콜백 함수에 전달할 컨텍스트 정보입니다. |

저장 함수에 반환 값이 없습니다. 호출이 성공적으로 완료 되 면 호출 됩니다 것를 `saveCompletedCallback` 매개 변수 또는 `defaultSaveCompletedCallback` 속성입니다. 호출에 실패 하거나 제한 시간이 만료 되거나 합니다 `failedCallback` 또는 `defaultFailedCallback` 속성 호출 됩니다.

경우는 `propertyNames` 매개 변수는 null, 모든 프로필 속성 서버로 전송 되 고 서버를 결정 하는 속성을 저장할 수 있습니다 하 고 수는 없습니다.

*defaultFailedCallback 속성 (get, set):*

이 속성을 호출 해야 웹 서비스와 통신 오류가 발생 하는 함수를 지정 합니다. 대리자 (또는 함수 참조) 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음과 같은 시그니처가 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| Error | 오류 정보를 지정합니다. |
| userContext | 때 제공 된 컨텍스트 정보를 사용자 지정 부하 또는 호출 된 함수를 저장 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultSaveCompleted 속성 (get, set):*

이 속성은 사용자의 프로필 데이터를 저장 하는 완료 될 때 호출 해야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조) 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음과 같은 시그니처가 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| numPropsSaved | 저장 된 속성의 수를 지정 합니다. |
| userContext | 때 제공 된 컨텍스트 정보를 사용자 지정 부하 또는 호출 된 함수를 저장 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultLoadCompleted 속성 (get, set):*

이 속성에는 사용자의 프로필 데이터 로드가 완료 될 때 호출 해야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조) 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음과 같은 시그니처가 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*매개 변수:*

| **매개 변수 이름** | **의미** |
| --- | --- |
| numPropsLoaded | 로드 되는 속성 수를 지정 합니다. |
| userContext | 때 제공 된 컨텍스트 정보를 사용자 지정 부하 또는 호출 된 함수를 저장 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*경로 속성 (get, set):*

이 속성은 프로그래밍 방식으로 프로필 웹 서비스의 위치를 결정 합니다. 기본 프로필 서비스 공급자 뿐만 아니라 하나를 재정의할 수 ScriptManager 컨트롤의 ProfileService 자식 노드의 경로 속성에 선언적으로 설정 합니다.

기본 프로필 서비스의 위치는 변경 되지 않는 참고 합니다. 그러나 ASP.NET AJAX를 사용 하는 ASP.NET AJAX 인증 서비스 프록시와 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.

또한이 속성을 현재 사이트에서 스크립트 요청을 전달 하는 값을 설정할 해야 note 합니다. 기술 기본 AJAX 교차 사이트 요청을 게시 해야 하 고 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.

이 속성은 한 `String` 프로필 웹 서비스에 경로 나타내는 개체입니다.

*timeout 속성 (get, set):*

이 속성 프로필 서비스 부하를 가정 하기 전에 기다리거나 요청 저장 기간에 실패 했습니다. 결정 합니다. 호출이 완료 되기를 기다리는 동안 제한 시간이 만료 되 면 요청이 실패 콜백을 호출 될 및 호출이 완료 되지 않습니다.

이 속성은 한 `Number` 프로필 서비스의 결과 기다릴 밀리초 수를 나타내는 개체입니다.

*코드 샘플: 페이지가 로드 될 때 프로필 데이터를 로드 합니다.*

다음 코드를 사용자가 인증 되었는지 여부를 확인 하 고 그렇다면 사용자의 기본 배경색으로 페이지의 로드 됩니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*사용자 지정 인증 서비스 공급자를 사용 하 여*

ASP.NET AJAX Extensions를 사용 하면 사용자 지정 웹 서비스를 통해 기능을 노출 하 여 사용자 지정 스크립트 인증 서비스 공급자를 만들 수 있습니다. 웹 서비스를 사용 하려면 두 가지 메서드를 노출 해야 합니다 `Login` 고 `Logout`; 기본 ASP.NET AJAX 인증 웹 서비스와 동일한 메서드 서명을 사용 하 여 이러한 메서드를 지정 해야 합니다.

사용자 지정 웹 서비스를 만든 후 클라이언트 스크립트를 통해 또는 코드에서 프로그래밍 방식으로 하 여 페이지에서 선언적으로 경로 지정 해야 합니다.

*경로 선언적으로 설정:*

경로 선언적으로 설정 하려면 ASP.NET 페이지에 ScriptManager 개체의 AuthenticationService 자식 포함.

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*코드에서 경로 설정 합니다.*

경로 프로그래밍 방식으로 설정 하려면 스크립트 관리자의 인스턴스를 통해 경로 지정 합니다.

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*스크립트의 경로 설정 합니다 하:*

경로 설정 하려면 프로그래밍 방식으로 스크립트에서 활용 된 `path` AuthenticationService 클래스의 속성:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*사용자 지정 인증에 대 한 샘플 웹 서비스*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>요약

ASP.NET 서비스-프로 파일링, 멤버 자격 및 인증 서비스 특히-클라이언트 브라우저에서 JavaScript에 쉽게 노출 됩니다. 따라서 같은 주요 작업을 수행 하 Updatepanel 컨트롤에 의존 하지 않고 원활 하 게 인증 메커니즘을 사용 하 여 해당 클라이언트 쪽 코드를 통합 하는 개발자. 웹 구성 설정을 활용 하 여 클라이언트로부터 프로필 데이터를 보호할 수 있습니다. 데이터가 없는 기본적으로 되며 개발자가 옵트인 해야 합니다 프로필 속성입니다.

또한 해당 하는 메서드 서명을 사용 하 여 간단한 웹 서비스 구현을 만들어 개발자는 이러한 내장 ASP.NET 서비스에 대 한 사용자 지정 스크립트 공급자를 만들 수 있습니다. 이러한 기술에 대 한 지원을 다양 한 범위의 특정 요구 사항에 맞게 유연성을 사용 하 여 개발자가 제공 하는 동안 다양 한 클라이언트 응용 프로그램 개발을 간소화 합니다.

## <a name="bio"></a>*사용자 정보*

Scott Cate 1997 년부터 Microsoft 웹 기술을 사용 하 여 왔습니다 이며 myKB.com의 대표이사로 서 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 전문적 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott 전자 메일을 통해 연락할 수 있습니다 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 저자의 블로그 또는 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-updatepanel-triggers.md)
> [다음](understanding-asp-net-ajax-localization.md)
