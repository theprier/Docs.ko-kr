---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 인증 및 권한 부여를 사용 하 여 응용 프로그램 보안 | Microsoft Docs
author: microsoft
description: 9 단계에는 사용자를 등록 해야 합니다. 추가할 인증 및 권한 부여 NerdDinner 응용 프로그램을 보호 하는 방법을 보여 줍니다 만들려는 사이트에 로그인 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d28102c8b80433b58a42cadc70b26c9fb5bc4404
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369886"
---
<a name="secure-applications-using-authentication-and-authorization"></a>인증 및 권한 부여를 사용 하 여 응용 프로그램 보안
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 9 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 9 단계에는 사용자를 등록 해야 합니다. 추가할 인증 및 권한 부여 NerdDinner 응용 프로그램을 보호 하는 방법을 보여 줍니다 새 dinners 만들고를 저녁 식사를 호스트 하는 사용자만 사이트에 로그인 나중에 편집할 수 있습니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner 9 단계: 인증 및 권한 부여

지금 바로 누구나 응용 프로그램 부여는 NerdDinner 만들고 모든 dinner의 세부 정보를 편집 하는 기능 사이트를 방문 합니다. 사용자가 등록할 필요가 해 보겠습니다 변경 새 dinners 만들고를 저녁 식사를 호스트 하는 사용자만 나중에 편집할 수 있도록 제한을 추가 하는 사이트에 로그인 합니다.

이렇게 하려면 인증 및 권한 부여 응용 프로그램 보안을 사용 하겠습니다.

### <a name="understanding-authentication-and-authorization"></a>이해 인증 및 권한 부여

*인증* 식별 하 고 응용 프로그램에 액세스 하는 클라이언트의 id 유효성을 검사 하는 프로세스입니다. 간단히 말해 "인 최종 사용자 웹 사이트를 방문할 때" 식별 하는 방법에 대 한 것입니다. ASP.NET은 브라우저 사용자를 인증 하는 여러 방법을 지원 합니다. 인터넷 웹 응용 프로그램에 대 한 가장 일반적인 인증 방법은 사용 되는 "폼 인증" 라고 합니다. Forms 인증을 사용 하면 개발자가 해당 응용 프로그램 내에서 HTML 로그인 폼을 작성 한 다음 데이터베이스 또는 다른 암호 자격 증명 저장소에 대 한 최종 사용자가 제출 하는 사용자 이름/암호 유효성 검사를 합니다. 사용자 이름/암호 조합이 올바른 경우 개발자는 이후 요청에서 사용자를 식별 하 여 암호화 된 HTTP 쿠키를 발급 하는 ASP.NET 다음 요청할 수 있습니다. NerdDinner 응용 프로그램을 사용 하 여 폼 인증을 사용 하 여 합니다.

*권한 부여* 인증된 된 사용자가 특정 URL/리소스에 액세스 하거나 일부 작업을 수행할 권한이 있는지 여부를 결정 하는 프로세스입니다. 예를 들어, NerdDinner 응용 프로그램 내에서 하고자에 로그인 한 사용자만 액세스할 수 있도록 권한을 부여 합니다 *Dinners/만들기* URL 새 Dinners를 만듭니다. 에서는 또한 하려고를 저녁 식사를 호스트 하는 사용자만 편집할 하 고 다른 모든 사용자에 대 한 편집 액세스를 거부할 수 있도록 권한 부여 논리를 추가 합니다.

### <a name="forms-authentication-and-the-accountcontroller"></a>폼 인증 및는 AccountController

ASP.NET MVC에 대 한 기본 Visual Studio 프로젝트 템플릿을 새 ASP.NET MVC 응용 프로그램을 만들 때 자동으로 폼 인증을 설정 합니다. 자동으로 미리 작성된 된 계정 로그인 페이지 구현 용이 하다는 실제로 사이트 내에서 보안을 통합 하는 프로젝트에 추가 합니다.

이 액세스 하는 사용자가 인증 되지 않은 경우 사이트의 오른쪽 위에 있는 "Log On" 링크를 표시 하는 기본 Site.master 마스터 페이지:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

사용자는 "Log On" 링크를 클릭 하 여 */계정/로그온* URL:

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

방문자에 게 등록 하지 않은 이렇게 – 하도록 걸립니다 "등록" 링크를 클릭 하 여 */계정/등록* URL 계정 세부 정보를 입력 하 고:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

"등록" 단추를 클릭 하면 ASP.NET 멤버 자격 시스템 내에서 새 사용자를 만들고 폼 인증을 사용 하 여 사이트에 사용자를 인증 합니다.

Site.master 변경 출력을 "Welcome [username]!" 페이지의 오른쪽 위에 사용자에 로그인 한 경우 메시지 및 렌더링을 "로그 오프" 연결을 "로그온" 하나 대신 합니다. "로그 오프" 링크를 클릭 하면 사용자를 로그 아웃 합니다.

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

위의 로그인, 로그 아웃 및 등록 기능을 프로젝트를 만들 때 Visual Studio에서 프로젝트에 추가 된 AccountController 클래스 내에서 구현 됩니다. UI는 AccountController \Views\Account 디렉터리 내에서 템플릿 보기를 사용 하 여 구현 됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController 클래스 암호화 된 인증 쿠키 및 저장 하 고 사용자 이름/암호의 유효성을 검사 하는 ASP.NET 멤버 자격 API를 실행 하는 ASP.NET 폼 인증 시스템을 사용 합니다. ASP.NET 멤버 자격 API를 확장할 수 있는 이며 모든 암호 자격 증명 저장소로 사용할 수 있습니다. ASP.NET는 Active Directory 또는 SQL database 내에서 사용자 이름/암호를 저장 하는 기본 제공 멤버 자격 공급자 구현으로 제공 됩니다.

NerdDinner 응용 프로그램 프로젝트의 루트에 "web.config" 파일을 열고 찾고 여 사용 해야 하는 멤버 자격 공급자를 구성할 수 있습니다 합니다 &lt;멤버 자격&gt; 내의 섹션입니다. 프로젝트를 만들 때 추가 기본 web.config SQL 멤버 자격 공급자를 등록 하 고 "ApplicationServices" 라는 연결 문자열을 사용 하도록 구성 데이터베이스 위치를 지정 합니다.

기본 "ApplicationServices" 연결 문자열 (내에서 지정 된 합니다 &lt;connectionStrings&gt; web.config 파일의 섹션) SQL Express를 사용 하도록 구성 됩니다. "ASPNETDB 명명 된 SQL Express 데이터베이스를 가리키도록. MDF"응용 프로그램의" 앱\_Data "디렉터리입니다. 이 데이터베이스 멤버 자격 API를 사용 하 여 응용 프로그램 내에서 처음으로 존재 하지 않는 경우 ASP.NET 자동으로 데이터베이스를 만들고 그 안에 적절 한 멤버 자격 데이터베이스 스키마를 프로 비전 합니다.

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

web.config 파일 내에 있는 "ApplicationServices" 연결 문자열 업데이트 되었는지 확인 해야 하는 경우 SQL Express에 방문 하셔서 전체 SQL Server 인스턴스를 사용 하 여 (또는 원격 데이터베이스에 연결)를 사용 하는 대신 모든는 할 일은 적절 한 멤버 자격 스키마 이 가리키는 데이터베이스에 추가 되었습니다. 실행할 수 있습니다는 "aspnet\_regsql.exe" 데이터베이스에 멤버 자격 및 다른 ASP.NET 응용 프로그램 서비스에 대 한 적절 한 스키마를 추가 하려면 \Windows\Microsoft.NET\Framework\v2.0.50727\ 디렉터리 내에서 유틸리티입니다.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[Authorize] 필터를 사용 하 여 Dinners/만들기 URL 권한 부여

보안 인증 및 계정 관리 구현 NerdDinner 응용 프로그램을 사용 하도록 설정 하려면 코드를 작성할 필요가 없었습니다. 사용자가 응용 프로그램 및 사이트의 로그인/로그 아웃 사용 하 여 새 계정을 등록할 수 있습니다.

이제 응용 프로그램에 권한 부여 논리를 추가 하 고 인증 상태 및 방문자의 사용자 이름을 사용 하 여 어떤 수 하며 사이트 내에서 수행할 수 없습니다를 제어할 수 있습니다 했습니다. "만들기" 작업 메서드에 DinnersController 클래스의 권한 부여 논리를 추가 하 여 시작 해 보겠습니다. 특히 우리가 해야 하는 액세스 하는 사용자를 *Dinners/만들기* URL 로그인 해야 합니다. 로그인 하지 않은 경우 있도록 수에 로그인 할 로그인 페이지로 리디렉션됩니다 됩니다 것입니다.

이 논리를 구현 하는 것은 매우 쉽습니다. 해야 할 일이 만들기 작업 메서드에 [Authorize] 필터 특성을 추가 하는 것 같이:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC 작업 메서드에 선언적으로 적용할 수 있는 재사용 가능한 논리를 구현 하는 "작업 필터"를 만드는 기능을 지원 합니다. [Authorize] 필터를 ASP.NET MVC에서 제공 하는 기본 제공 작업 필터 중 하나 이며 개발자 작업 메서드와 컨트롤러 클래스에 권한 부여 규칙을 선언적으로 적용할 수 있습니다.

위에서 같이 매개 변수 없이 적용 될 때 동작 메서드가 요청 하는 사용자에서 로그인 해야 하 고 자동으로 리디렉션됩니다 브라우저를 로그인 url 그렇지 않은 경우 [Authorize] 필터를 적용 합니다. 처음에 요청한 URL 쿼리 문자열 인수로 전달 되는이 리디렉션을 수행할 때 (예: / 계정/로그온? ReturnUrl = %2fDinners %2fCreate). AccountController 로그인 되 면 사용자를 원래 요청 된 URL로 다시 리디렉션합니다 다음 됩니다.

[Authorize] 필터는 필요에 따라 사용자는 모두 로그온에 허용 된 사용자 또는 허용 된 보안 역할의 멤버 목록을 내에서 할 수 있는 "사용자" 또는 "역할" 속성을 지정 하는 기능을 지원 합니다. 예를 들어 아래 코드 허용 두 개의 특정 사용자, "scottgu" 및 "billg" Dinners/만들기 URL에 액세스 합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

코드 내에서 특정 사용자 이름을 포함 하지만 매우 되지 않은 intainable 수는 경향이 있습니다. 상위 수준 "역할"을 정의 하는 것이 좋습니다를 기준으로 코드를 검사 하 고 데이터베이스 또는 active directory 시스템 (활성화 코드에서 외부적으로 저장 될 실제 사용자 매핑 목록)을 사용 하 여 역할에 사용자를 매핑할 합니다. ASP.NET이 사용자/역할 매핑을 수행 하는 데 도움이 되는 역할 공급자 (비롯 하 여 SQL 및 Active Directory)의 기본 제공 집합 뿐만 아니라 기본 제공 역할 관리 API 포함 합니다. 그런 다음 Dinners/만들기 URL에 액세스 하는 특정 "관리" 역할 내의 사용자만 사용할 수 있도록 코드 업데이트 수 있습니다.:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>만들 때 User.Identity.Name 속성을 사용 하 여 Dinners

컨트롤러 기본 클래스에서 노출 User.Identity.Name 속성을 사용 하 여 요청에 현재 로그인 한 사용자의 사용자 이름을 검색할 수 있습니다.

이전 create () 작업 메서드는 HTTP POST 버전을 구현한 경우 했습니다 하드 코드 된 정적 문자열로 Dinner "HostedBy" 속성입니다. Dinner 만드는 호스트는 RSVP를 자동으로 추가 수 있을 뿐만 아니라 이제 대신 User.Identity.Name 속성을 사용 하 여이 코드를 업데이트할 수 있습니다 것:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Create () 메서드에 [Authorize] 특성을 추가 했지만, 때문에 ASP.NET MVC는 작업 메서드에서 Dinners/만들기 URL을 방문 하는 사용자가 사이트에 로그인 하는 경우에 실행 되도록 합니다. 따라서 User.Identity.Name 속성 값을 올바른 사용자 이름을 항상 포함 됩니다.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>편집할 때 User.Identity.Name 속성을 사용 하 여 Dinners

이제 호스트 자체가 dinners의 속성을 편집할 수만 있도록 사용자를 제한 하는 일부 권한 부여 논리를 추가 해 보겠습니다.

이 돕기 위해 "IsHostedBy(username)" 도우미 메서드를 (내에서 앞서 작성 Dinner.cs 부분 클래스)은 Dinner 개체에 추가 됩니다 했습니다. 이 도우미 메서드는 제공 된 사용자 이름을 Dinner HostedBy 속성과 일치 하 여부와 그 중 대/소문자 구분 문자열 비교를 수행 하는 데 필요한 논리를 캡슐화 따라 true 또는 false를 반환 합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

그런 다음 DinnersController 클래스 내에서 되 작업 메서드에 [Authorize] 특성을 추가 합니다. 그러면는 사용자가 로그인 해야 요청에는 */Dinners/편집 / [id]* URL입니다.

다음 코드 Dinner.IsHostedBy(username) 도우미 메서드를 사용 하 여 로그인 한 사용자 Dinner 호스트와 일치 하는지 확인 하는 편집 메서드를 추가할 수 있습니다. 사용자 호스트 없는 경우에서는 "InvalidOwner" 보기를 표시 하 고 해당 요청을 종료 합니다. 이 작업을 수행 하는 코드는 아래와 같습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

\Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 한 다음를 선택 하 고 추가-에서는&gt;새 "InvalidOwner" 보기를 만들려면 메뉴 명령을 보고 합니다. 사용 하 여 채웁니다 것은 오류 메시지가 아래:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

이제 사용자가 자신이 소유 하지 않는 저녁 식사를 편집 하려고 하는 경우 해당 오류 메시지가 표시 됩니다는

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Dinners도 삭제의 저녁 식사 호스트만 삭제할 수 있는지 확인 하는 권한 잠글 컨트롤러 내에서 delete () 작업 메서드에 대 한 동일한 단계를 반복할 수 했습니다.

### <a name="showinghiding-edit-and-delete-links"></a>표시/숨기기 편집 및 삭제 링크

정보 URL에서 DinnersController 클래스의 편집 및 삭제 동작 메서드에 연결 되어 했습니다.

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

현재 세부 정보 URL로 방문자의를 저녁 식사 호스트 인지에 관계 없이 편집 및 삭제 작업 링크가 표시 됩니다. 보겠습니다이 되도록 변경 링크는 방문한 사용자 dinner의 소유자 인 경우에 표시 됩니다.

저녁 식사 개체를 검색 하 고 보기 템플릿은를 모델 개체로 전달 하는 우리의 DinnersController 내의 Details() 작업 메서드:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

보기 템플릿은 조건부로 표시/숨기기 편집 및 삭제 링크를 아래와 같은 도우미 메서드 Dinner.IsHostedBy()를 사용 하 여 업데이트할 수 있습니다.

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>다음 단계

이제 살펴보겠습니다 참석 여부 회신 하기 dinners AJAX를 사용 하 여 인증 된 사용자가 사용할 수 하는 방법.

> [!div class="step-by-step"]
> [이전](implement-efficient-data-paging.md)
> [다음](use-ajax-to-deliver-dynamic-updates.md)
