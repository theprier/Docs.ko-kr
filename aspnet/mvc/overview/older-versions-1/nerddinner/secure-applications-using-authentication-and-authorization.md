---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 | Microsoft Docs
author: microsoft
description: 9 단계에서는 사용자가 등록 해야 할 수 있도록 인증 및 권한 부여 우리의 업그레이드 되었으며 수정 응용 프로그램 보안을 추가 하는 방법을 보여 줍니다. 사이트를 만들 로그인...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 4a9b1e6d7d453bd8dc5a61b1f1cec4617af7d693
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874384"
---
<a name="secure-applications-using-authentication-and-authorization"></a>인증 및 권한 부여를 사용 하 여 응용 프로그램 보안
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 9 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 9 단계에서는 사용자가 등록 해야 할 수 있도록 인증 및 권한 부여 우리의 업그레이드 되었으며 수정 응용 프로그램 보안을 추가 하는 방법을 보여 줍니다. 사이트를 새 dinners를 만들고 호스팅하는 저녁 한 사용자만 로그인 나중에 편집할 수 있습니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-9-authentication-and-authorization"></a>업그레이드 되었으며 수정 9 단계: 인증 및 권한 부여

지금은 응용 프로그램 사용자에 게 부여 하 여 업그레이드 되었으며 수정 만들고 모든 dinner의 세부 정보를 편집할 수 있는 사이트를 방문 합니다. 바꿔보겠습니다이 사용자가을 등록 해야 하 고 새 dinners를 만들고 호스팅하는 저녁 한 사용자만 나중에 편집할 수 있도록 제한을 추가 하는 사이트에 로그인 합니다.

이 방법을 사용 하려면 인증 및 권한 부여 응용 프로그램 보안을 사용 합니다.

### <a name="understanding-authentication-and-authorization"></a>이해 인증 및 권한 부여

*인증* 식별 하 고 응용 프로그램에 액세스 하는 클라이언트의 id 유효성을 검사 하는 프로세스입니다. "인 최종 사용자 웹 사이트를 방문할 때" 식별 하는 방법에 대 한 것 보다 간단히 말해서 합니다. ASP.NET은 브라우저 사용자를 인증 하는 여러 가지 방법을 지원 합니다. 인터넷 웹 응용 프로그램에 사용 하는 가장 일반적인 인증 방법 "폼 인증" 라고 합니다. 폼 인증을 사용 하면 개발자가 응용 프로그램 내에서 HTML 로그인 양식을 작성 하 고 다음 최종 사용자는 데이터베이스 또는 다른 암호 자격 증명 저장소에 대해 전송 사용자 이름/암호 유효성을 검사할 수 있습니다. 사용자 이름/암호 조합이 올바른 경우 개발자는 앞으로 요청에서 사용자를 식별 하 여 암호화 된 HTTP 쿠키를 발급 하는 ASP.NET 다음 요청할 수 있습니다. त ु म 샘플 업그레이드 되었으며 수정 응용 프로그램 폼 인증을 사용 하 여 합니다.

*권한 부여* 인증된 된 사용자에 게 권한이 특정 URL/리소스를 액세스 하거나 작업을 수행할 수 있는지를 결정 하는 프로세스입니다. 예를 들어 업그레이드 되었으며 수정 응용 프로그램 내에서 하고자에 로그온 한 사용자만 액세스할 수 있도록 권한을 부여는 */Dinners/만들기* URL 새 Dinners 만듭니다. 또한는 저녁을 호스트 하는 사용자만 라인이 편집 하 고 다른 모든 사용자에 대 한 편집 액세스를 거부할 수 있도록 권한 부여 논리를 추가 하려고 합니다 합니다.

### <a name="forms-authentication-and-the-accountcontroller"></a>폼 인증 및는 AccountController

ASP.NET MVC에 대 한 기본 Visual Studio 프로젝트 템플릿이 새 ASP.NET MVC 응용 프로그램을 만들 때 자동으로 폼 인증을 설정 합니다. 자동으로 미리 작성 된 계정 로그인 페이지 구현 – 사이트 내에서 보안을 통합 하기 쉬운 실제로 프로젝트에 추가 합니다.

기본 Site.master 마스터 페이지에 액세스 하는 사용자 인증 되지 않은 경우 사이트의 오른쪽 위에에 "Log On" 링크를 표시 됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

사용자는 "Log On" 링크를 클릭 하 여 */계정/로그온* URL:

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

방문자가 등록 되지 않은 이렇게 하려면-에 있는 "Register" 링크를 클릭 하 여 */계정/레지스터* URL 계정 세부 정보를 입력 하 고:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

"Register" 단추를 클릭 하는 ASP.NET 멤버 자격 시스템 내에서 새 사용자를 만들고 폼 인증을 사용 하는 사이트에 사용자를 인증 합니다.

사용자가 로그인에 Site.master는 "시작 [username]!"에 출력 하는 페이지의 오른쪽 위에 변경 메시지 렌더링 되는 "로그 오프" 링크 하는 "Log On" 하나 대신 하십시오. "로그 오프" 링크를 클릭 하면 사용자를 로그 아웃 합니다.

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

위의 로그인, 로그 아웃 및 등록 기능 프로젝트를 만들 때 Visual Studio에서이 프로젝트에 추가 된 AccountController 클래스 내에서 구현 됩니다. AccountController에 대 한 UI \Views\Account 디렉터리 내 템플릿 보기를 사용 하 여 구현 됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController 클래스 전체에 암호화 된 인증 쿠키를 저장 하 고 사용자 이름/암호 유효성을 검사 하는 ASP.NET 멤버 자격 API는 ASP.NET 폼 인증 시스템을 사용 합니다. ASP.NET 멤버 자격 API는 확장 가능 하며 모든 암호 자격 증명 저장소에 사용할 수 있습니다. ASP.NET은 SQL 데이터베이스 내에서 나 Active Directory 내에서 사용자 이름/암호를 저장 하는 기본 제공 멤버 자격 공급자 구현 함께 제공 됩니다.

프로젝트의 루트에 있는 "web.config" 파일을 열고 찾고 여 업그레이드 되었으며 수정 응용 프로그램 사용 해야 하는 멤버 자격 공급자를 구성할 수 있습니다는 &lt;구성원&gt; 섹션 내에서. 프로젝트를 만들 때 추가 기본 web.config SQL 멤버 자격 공급자를 등록 하 고 "ApplicationServices" 라는 연결 문자열을 사용 하도록 구성 데이터베이스 위치를 지정 합니다.

기본 "ApplicationServices" 연결 문자열 (내에서 지정 된 된 &lt;connectionStrings&gt; web.config 파일의 섹션) SQL Express를 사용 하도록 구성 됩니다. "ASPNETDB 라는 SQL Express 데이터베이스를 가리키는. 응용 프로그램의 아래 MDF"" 응용 프로그램\_데이터 "디렉터리입니다. 이 데이터베이스 멤버 자격 API를 사용 하 여 응용 프로그램 내에서 처음으로 존재 하지 않으면 ASP.NET은 자동으로 데이터베이스를 만들고 그 안에 적절 한 멤버 자격 데이터베이스 스키마를 프로 비전:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

전체 SQL Server 인스턴스를 사용 하 여 (또는 원격 데이터베이스에 연결) 주고자 SQL Express를 사용 하는 대신 모든가 필요 할 일 경우 web.config 파일 내에서 "ApplicationServices" 연결 문자열을 업데이트 하 고 있는지 확인 하는 것은 적절 한 멤버 자격 스키마 가리키도록 데이터베이스에 추가 되었습니다. 실행할 수는 "aspnet\_regsql.exe" 멤버 자격 및 다른 ASP.NET 응용 프로그램 서비스에 대 한 적절 한 스키마는 데이터베이스를 추가 하려면 \Windows\Microsoft.NET\Framework\v2.0.50727\ 디렉터리 내 유틸리티입니다.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[Authorize] 필터를 사용 하 여 Dinners/만들기 URL 권한 부여

필요는 전혀 없고 보안 인증 및 계정 관리 구현 업그레이드 되었으며 수정 응용 프로그램에 대해 사용할 수 있도록 코드를 작성 합니다. 사용자가 응용 프로그램 및 사이트의 로그인/로그 아웃 새 계정을 등록할 수 있습니다.

이제 제어은 할 수 있는 일과 사이트 내에서 수행할 수 없습니다 방문자의 사용자 이름 및 인증 상태와 사용 하는 응용 프로그램에 권한 부여 논리를 추가할 수 있습니다 우리 합니다. "만들기" 작업 메서드에 DinnersController 클래스의 권한 부여 논리를 추가 하 여 시작 해 보겠습니다. 특히, 우리 내용의 하는 액세스 하는 사용자는 */Dinners/만들기* URL로 로그인 해야 합니다. 로그인 하지 않은 경우 하실에 로그인 페이지에 있도록 있습니다에 로그인 합니다.

이 논리를 구현 하는 것은 매우 쉽습니다. 할 일을 필요한 것이 만들기 작업 메서드에 [Authorize] 필터 특성을 추가 하는 것 같이:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC 작업 메서드에 선언적으로 적용할 수 있는 재사용 가능한 논리를 구현 하는 데 사용할 수 있는 "작업 필터"를 만들 수를 지원 합니다. [Authorize] 필터 ASP.NET MVC에서 제공 되는 기본 제공 작업 필터 중 하나 이며 개발자 작업 메서드와 컨트롤러 클래스에 권한 부여 규칙을 선언적으로 적용할 수 있습니다.

위에서 같이 매개 변수 없이 적용 될 때 동작 메서드가 요청 하는 사용자-에 로그인 해야 하 고 자동으로 리디렉션할 수 브라우저 로그인 url이 아닐 경우 [Authorize] 필터를 적용 합니다. 원래 요청 된 URL 쿼리 문자열 인수로 전달 되는이 페이지를 수행할 때 (예: / 계정/로그온? ReturnUrl = %2fDinners %2fCreate). AccountController은 로그인 한 후 사용자를 원래 요청 된 URL로 다시 리디렉션합니다 다음 됩니다.

[Authorize] 필터는 필요에 따라 사용자가 둘 다 로그온 및 허용 된 사용자 또는 허용 된 보안 역할의 구성원 목록 내에서 필요한 데 사용할 수 있는 "사용자" 또는 "역할" 속성을 지정 하는 기능을 지원 합니다. 예를 들어 아래 코드 Dinners/만들기 URL에 액세스 하려면 두 개의 특정 사용자, "scottgu" 및 "billg"만 허용 합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

코드 내에서 특정 사용자 이름을 포함 하지만 꽤 되지 않은 intainable 수는 경향이 있습니다. 더 높은 수준의 "역할"을 정의 하는 것이 좋습니다 코드 검사를 확인 하는 한 다음 데이터베이스 또는 active directory 시스템 (코드에서 외부에서 저장 될 실제 사용자 매핑 목록 가능)를 사용 하 여 역할에 사용자를 매핑해야 합니다. ASP.NET에이 사용자/역할 매핑을 수행 하는 데 도움이 됩니다 (원본을 비롯 SQL 및 Active Directory에 대 한) 역할 공급자의 기본 제공 집합 뿐만 아니라 기본 제공 역할 관리 API에 포함 되어 있습니다. 그런 다음 Dinners/만들기 URL에 액세스 하는 특정 "admin" 역할 내의 사용자만 사용할 수 있도록 코드를 업데이트할 수 있습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>만들 때 User.Identity.Name 속성을 사용 하 여 Dinners

컨트롤러의 기본 클래스에 노출 된 User.Identity.Name 속성을 사용 하 여 요청에 현재 로그인 한 사용자의 사용자를 검색할 수 있습니다.

이전 우리의 create () 동작 메서드의 POST HTTP 버전을 구현한 경우 했습니다. 하드 코드 된 저녁에 정적 문자열의 "HostedBy" 속성입니다. Dinner 만드는 호스트는 RSVP 자동으로 추가 수 있을 뿐만 아니라 이제 대신 User.Identity.Name 속성을 사용 하 여이 코드를 업데이트할 수 했습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

[Authorize] 특성을 create () 메서드를 추가 했으므로 때문에 ASP.NET MVC는 동작 메서드가 Dinners/만들기 URL을 방문 하는 사용자가 사이트에 로그인 하는 경우에 실행 되도록 합니다. 따라서 User.Identity.Name 속성 값의 유효한 사용자 이름에 항상 포함 됩니다.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>편집할 때 User.Identity.Name 속성을 사용 하 여 Dinners

이제 dinners 자체가 호스트의 속성을 편집만 수 있도록 사용자를 제한 하는 일부 권한 부여 논리를 추가 해 보겠습니다.

이 해결 하기 우리의 Dinner 개체 (내에서 앞에서 만든 partial Dinner.cs 클래스)에 "IsHostedBy(username)" 도우미 메서드를 추가 먼저 합니다. True 또는 false 제공된 사용자 Dinner HostedBy 속성과 일치와 중 대/소문자 구분 문자열 비교를 수행 하는 데 필요한 논리를 캡슐화 여부에 따라이 도우미 메서드를 반환 합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

म DinnersController 클래스 내에서 Edit() 작업 메서드에 [Authorize] 특성을 추가 합니다. 이 방법을 사용 하면 사용자를 요청에에 로그인 해야 하는 */Dinners/편집 / [id]* URL입니다.

다음 코드 Dinner.IsHostedBy(username) 도우미 메서드를 사용 하 여 로그인 한 사용자 Dinner 호스트와 일치 하는지 확인 하는 편집 메서드를 추가할 수 있습니다. 사용자가 호스트 하는 경우 "InvalidOwner" 보기 표시 되 고 해당 요청을 종료 합니다. 이 작업을 수행 하는 코드는 다음과 같습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

그런 다음 \Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가-선택할 수 있습니다&gt;보기 메뉴 명령 새로운 "InvalidOwner" 보기를 만듭니다. 채울 수 우리는 아래 오류 메시지:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

고 이제 사용자가 자신이 소유 하지 않는 dinner 편집 하려고 오류 메시지가 나타날 수 있습니다.

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Dinners도 삭제 하는 Dinner 호스트만 삭제할 수 확인 권한을 잠그는을 컨트롤러 내에서 delete () 작업 메서드에 대 한 같은 단계를 반복 수 있습니다.

### <a name="showinghiding-edit-and-delete-links"></a>표시/숨기기 편집 및 삭제 링크

म 우리의 세부 정보 URL에서 DinnersController 클래스의 편집 및 삭제 동작 메서드에 연결:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

현재 세부 정보 URL 방문자 dinner 호스트 인지에 관계 없이 편집 및 삭제 작업 링크가 나와 있습니다. 이제이 모양을 변경 링크는 방문한 사용자 dinner의 소유자 인 경우에 표시 됩니다.

우리의 DinnersController 내 Details() 작업 메서드 Dinner 개체를 검색 하 고 우리의 템플릿 보기를 모델 개체와 전달:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

조건부로 표시/숨기기 편집 및 삭제 링크는 Dinner.IsHostedBy() 아래와 같은 도우미 메서드를 사용 하 여이 보기 템플릿을 업데이트할 수 있습니다.:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>다음 단계

이제 살펴보겠습니다 어떻게 RSVP dinners AJAX를 사용 하 여에 대 한 인증 된 사용자 설정 가능 합니다.

> [!div class="step-by-step"]
> [이전](implement-efficient-data-paging.md)
> [다음](use-ajax-to-deliver-dynamic-updates.md)
