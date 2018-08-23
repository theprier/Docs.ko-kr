---
uid: web-pages/overview/security/16-adding-security-and-membership
title: 페이지 (Razor) 사이트를 ASP.NET 웹 보안 및 멤버 자격 추가 | Microsoft Docs
author: tfitzmac
description: 이 챕터의 일부 페이지에 로그인 하는 사용자만 사용할 수 있도록 웹 사이트를 보호 하는 방법을 보여 줍니다. (또한 표시 페이지 tha...를 만드는 방법
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: ae574706ecd14f1cafdb2d8b6340477e50246a32
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828503"
---
<a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 보안 및 멤버 자격 추가
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에는 일부 페이지에 로그인 하는 사용자만 사용할 수 있도록 ASP.NET Web Pages (Razor) 웹 사이트를 보호 하는 방법을 설명 합니다. (또한 배웁니다 누구나 액세스할 수 있는 페이지를 만드는 방법.)
> 
> **학습할 내용:** 
> 
> - 일부 페이지에 대 한 멤버만에 대 한 액세스를 제한할 수 있도록 등록 페이지 및 로그인 페이지에 있는 웹 사이트를 만드는 방법입니다.
> - 공용 및 회원 전용 페이지를 만드는 방법입니다.
> - 사이트에 대 한 다른 보안 권한이 있는 그룹에 된 역할을 정의 하는 방법 및 사용자 역할을 할당 하는 방법.
> - 멤버 계정 만들기 자동화 프로그램 (봇) 되지 않도록 하려면 CAPTCHA를 사용 하는 방법입니다.
>   
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - WebMatrix **시작 사이트** 템플릿.
> - 합니다 `WebSecurity` 도우미 및 `Roles` 클래스입니다.
> - `ReCaptcha` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - WebMatrix 3
> - ASP.NET Web Helpers Library


사용자가 로그인 할 수 있도록 웹 사이트를 설정할 수 있습니다 &#8212; 즉, 사이트 지원 되도록 *멤버 자격*합니다. 이 유용할 수 있습니다 여러 가지 이유로 합니다. 예를 들어 사이트에는 멤버에만 사용할 수 있는 페이지가 있을 수 있습니다. 경우에 따라 사용자가 의견을 남기 피드백을 보낼 수 하기 위해 로그인 할 필요할 수 있습니다.

웹 사이트 멤버 자격을 지 원하는 경우에 사용자 페이지의 일부 사이트에서 사용 하기 전에 로그인 반드시 불필요 합니다. 로그인 하지 않은 사용자로 알려져 *익명 사용자에 게*합니다.

사용자 웹 사이트에서 등록할 수 있습니다 하 고 사이트에 로그인 할 수 있습니다. 웹 사이트에는 사용자 이름 (전자 메일 주소) 및 사용자가 되도록 신원을 확인 하는 데 암호 필요 합니다. 로그인 및 사용자의 id를 확인 합니다.이 프로세스는 이라고 *인증*합니다.

다른 방법으로 보안 및 멤버 자격을 설정할 수 있습니다.

- 쉬운을 기반으로 새 사이트를 만들 때 WebMatrix를 사용 하는 경우는 **시작 사이트** 템플릿. 이 보안 및 멤버 자격에 대해 이미 구성 되어 템플릿과 이미 등록 페이지, 로그인 페이지 및 등입니다.

    템플릿에서 만든 사이트 사용자가 facebook, Google, 외부 사이트를 사용 하 여 로그인 하거나 Twitter를 사용 하는 옵션도 있습니다.
- Security는 기존 사이트에 추가 하려는 경우 또는 사용 하지 않으려는 경우 합니다 **시작 사이트** 템플릿을 고유한 등록 페이지와 로그인 페이지에 만들 수 있습니다.

이 문서에서는 첫 번째 옵션에 중점을 둡니다 &mdash; 를 사용 하 여 보안을 추가 하는 방법을 합니다 **시작 사이트** 템플릿. 또한 사용자 고유의 보안을 구현 하는 방법에 대 한 일부 기본 정보를 제공 하 고 작업을 수행 하는 방법에 대 한 자세한 정보에 대 한 링크를 제공 합니다. 별도 문서에 자세히 설명 된 외부 로그인을 사용 하는 방법에 대 한 내용은 이기도 합니다.

## <a name="creating-website-security-using-the-starter-site-template"></a>시작 사이트 템플릿을 사용 하 여 웹 사이트 보안

WebMatrix에서 사용할 수 있습니다는 **시작 사이트** 템플릿을 다음이 포함 된 웹 사이트를 만듭니다.

- 멤버에 대 한 사용자 이름 및 암호를 저장 하는 데 사용 되는 데이터베이스입니다.
- 익명 (신규) 사용자를 등록할 수 있는 등록 페이지입니다.
- 로그인 및 로그 아웃 페이지입니다.
- 암호 복구 및 다시 설정 페이지입니다.

다음 절차에는 사이트를 만들고 구성 하는 방법을 설명 합니다.

1. WebMatrix를 시작 및 합니다 **빠른 시작** 페이지에서 **사이트에서 템플릿을**합니다.
2. 선택 된 **시작 사이트** 템플릿과 클릭 **확인**합니다. WebMatrix에 새 사이트를 만듭니다.
3. 왼쪽된 창에서 클릭 합니다 **파일** 작업 영역 선택 기가 있습니다.
4. 웹 사이트의 루트 폴더에서 엽니다는  *\_AppStart.cshtml* 전역 설정을 포함 하는 데 사용 되는 특수 한 파일인 파일입니다. 사용 하 여 주석으로 처리 되는 일부 문이 포함 된 `//` 문자:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    이러한 문은 구성 된 `WebMail` 전자 메일을 보내는 데 사용할 수 있는 도우미입니다. 멤버 자격 시스템 전자 메일을 사용 하 여 자신의 암호를 변경 하려는 경우 또는 사용자가 등록할 때 확인 메시지를 보낼 수 있습니다. (예를 들어 사용자가 등록 한 후에 메일이 해당 등록 프로세스를 완료 하기 위해 클릭할 수 있는 링크를 포함 하는.)

    에 설명 된 대로 SMTP 서버에 액세스할 수 있어야 전자 메일 보내기 [ASP.NET Web Pages 사이트에 전자 메일 추가](https://go.microsoft.com/fwlink/?LinkId=202899)합니다. 이 중앙에 전자 메일 설정을 저장할  *\_AppStart.cshtml* 파일에 전자 메일을 보낼 수 있는 각 페이지에 반복 해 서 코드를 작성할 필요가 없습니다. (등록 데이터베이스를 설정 하도록 SMTP 설정을 구성할 필요가 없습니다; 사용자가 자신의 전자 메일 별칭의 유효성을 검사 하 고 사용자가 잊어버린된 암호를 재설정할 수 있도록 하려는 경우 SMTP 설정이 필요)
5. 문을 제거 하 여 주석 처리 제거 `//` 각각 앞에서.

    전자 메일 확인을 설정 하지 않으려면이 단계와 다음 단계를 건너뛸 수 있습니다. SMTP 값을 설정 하지 않은 경우 새 계정은 전자 메일을 확인 하지 않고 즉시 사용할 수 있습니다.
6. 코드에서 다음 전자 메일 관련 설정을 수정 합니다.

   - 설정 `WebMail.SmtpServer` 에 대 한 액세스를 해야 하는 SMTP 서버의 이름입니다.
   - 둡니다 `WebMail.EnableSsl` 로 `true`합니다. 이 설정을 암호화 하 여 SMTP 서버에 전송 되는 자격 증명을 보호 합니다.
   - 설정 `WebMail.UserName` SMTP 서버 계정의 사용자 이름입니다.
   - 설정 `WebMail.Password` SMTP 서버 계정의 암호입니다.
   - 설정 `WebMail.From` 고유한 전자 메일 주소입니다. 이 메시지에서 전송 되는 전자 메일 주소입니다.

     > [!NOTE] 
     > 
     > **팁** 이러한 속성 값에 대 한 자세한 내용은 참조 하세요. [전자 메일 설정 구성](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings) 에서 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkID=202906)합니다.
7. 저장 후 닫기  *\_AppStart.cshtml*합니다.
8. 실행 합니다 *Default.cshtml* 브라우저에서 페이지입니다.

    ![보안-멤버 자격-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > 속성의 인스턴스를 되도록 알려 주는 오류가 표시 되 면 `ExtendedMembershipProvider`, ASP.NET 웹 페이지 멤버 자격 시스템 (SimpleMembership)를 사용 하도록 사이트를 구성할 수 있습니다. 경우에 따라 호스팅 공급자의 서버가 로컬 서버와는 다르게 구성 된 경우 발생할 수 있습니다. 이 해결 하려면 사이트의 다음 요소를 추가 *Web.config* 파일:
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > 이 요소의 자식으로 추가 합니다 `<configuration>` 요소와의 피어를 `<system.web>` 요소입니다.
9. 페이지의 오른쪽 위 모퉁이 클릭 합니다 **등록** 링크 합니다. 합니다 *Register.cshtml* 페이지가 표시 됩니다.
10. 사용자 이름 및 암호를 입력 한 다음 클릭 **등록**합니다.

    ![보안-멤버 자격-3](16-adding-security-and-membership/_static/image2.png)

    웹 사이트를 만들 때 합니다 **시작 사이트** 템플릿, 라는 데이터베이스가 *StarterSite.sdf* 사이트에서 만든 *앱\_데이터* 폴더. 등록 하는 동안 사용자 정보는 데이터베이스에 추가 됩니다. SMTP 값을 설정 하는 경우 메시지는 전자 메일 주소로 전송 됩니다 사용한 등록을 완료할 수 있습니다.

    ![4-멤버 자격-보안](16-adding-security-and-membership/_static/image3.png)
11. 전자 메일 프로그램 이동 하 고 사이트에 확인 코드 및 하이퍼링크를 포함 하는 메시지를 찾습니다.
12. 계정을 활성화 하려면 하이퍼링크를 클릭 합니다. 확인 하이퍼링크 등록 확인 페이지를 엽니다.

    ![보안-멤버 자격-5](16-adding-security-and-membership/_static/image4.png)
13. 클릭 합니다 **로그인** 링크를 선택한 다음 등록 된 계정을 사용 하 여 로그인 합니다.

      로그인 한 후에 **로그인** 및 **등록** 링크 바뀝니다를 **로그 아웃** 링크 합니다. 로그인 이름 링크로 표시 됩니다. (링크 하면 암호를 변경할 수 있는 페이지로 이동 합니다.)

      ![6-보안-멤버 자격](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > 기본적으로 ASP.NET 웹 페이지 서버에 보낼 자격 증명이 일반 텍스트로 (사람이 읽을 수 있는 텍스트로). 프로덕션 사이트에서 보안 HTTP를 사용 해야 (라고도 https://를 *보안 소켓 레이어* 또는 SSL) 서버와 교환 되는 중요 한 정보를 암호화 합니다. 필수 전자 메일 수 메시지를 보낼 수 있도록 설정 하 여 SSL을 사용 하 여 `WebMail.EnableSsl=true` 이전 예제와 같이 합니다. SSL에 대 한 자세한 내용은 참조 하세요. [웹 통신 보안: 인증서, SSL 및 https://](https://go.microsoft.com/fwlink/?LinkId=208660)합니다.

## <a name="additional-membership-functionality-in-the-site"></a>사이트의 추가 멤버 자격 기능

사이트는 사용자가 자신의 계정을 관리할 수 있는 기타 기능을 포함 합니다. 사용자가 다음을 수행할 수 있습니다.

- 자신의 암호를 변경 합니다. 로그인 한 후에 사용자 이름 (링크)를 클릭할 수 있습니다. 그러면 해당 페이지에 새 암호를 만들 수 있습니다 (*Account/ChangePassword.cshtml*).
- 잊어버린된 암호를 복구 합니다. 로그인 페이지에는 링크 (**암호를 잊은 않았습니다?**) 페이지로 사용자를 사용 하는 (*Account/ForgotPassword.cshtml*) 전자 메일 주소를 입력할 수 있습니다. 사이트는 새 암호를 설정 하기 위해 클릭할 수 있는 링크가 있는 전자 메일 메시지를 보냅니다 (*Account/PasswordReset.cshtml*).

사용자가 나중에 설명 된 대로 외부 사이트를 사용 하 여 로그인 수도 할 수도 있습니다.

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>회원 전용 페이지 만들기

당분간, 웹 사이트의 모든 페이지를 이동할 수 누구나 합니다. 페이지에는 로그인 한 사용자 에게만 제공 하는 할 수 있지만 (즉, 멤버에). ASP.NET 로그인 멤버만 액세스할 수 있는 페이지를 만들 수 있습니다. 일반적으로 익명 사용자를 회원 전용 페이지에 액세스 하려고 하면 리디렉션할 로그인 페이지입니다.

이 절차에서는 로그인 한 사용자 에게만 사용할 수 있는 페이지를 포함 하는 폴더를 만들어야 합니다.

1. 사이트의 루트에서 새 폴더를 만듭니다. (리본 메뉴에서 아래에 있는 화살표를 클릭 **새로 만들기** 를 선택한 후 **새 폴더**.)
2. 새 폴더의 이름을 *멤버*합니다.
3. 내 합니다 *멤버* 폴더에 새 페이지를 만들고 이라는 *MembersInformation.cshtml*합니다.
4. 다음 코드와 태그를 사용 하 여 기존 콘텐츠를 바꿉니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    이 코드를 테스트 합니다 `IsAuthenticated` 의 속성을 `WebSecurity` 개체를 반환 하는 `true` 사용자가 로그인 하는 경우. 사용자가 로그인 하지 않은 경우, 호출 `Response.Redirect` 를 사용자에 게 보낼지를 *Login.cshtml* 페이지에 *계정* 폴더.

    리디렉션 URL에 포함 된 `returnUrl` 쿼리를 사용 하는 문자열 값 `Request.Url.LocalPath` 현재 페이지의 경로 설정 하 합니다. 설정 하는 경우는 `returnUrl` 다음과 같은 쿼리 문자열의 값 (및 반환 URL 로컬 경로인 경우)에 로그인 한 후 로그인 페이지를이 페이지에 사용자가 반환 됩니다.

    코드를 설정  *\_SiteLayout.cshtml* 해당 레이아웃 페이지와 페이지입니다. (한 레이아웃 페이지에 대 한 자세한 내용은 [ASP.NET Web Pages 사이트에서 일관 된 레이아웃을 만드는](https://go.microsoft.com/fwlink/?LinkId=202891).)
5. 사이트를 실행 합니다. 여전히 로그인을 클릭 합니다 **로그 아웃** 페이지의 맨 위에 있는 단추입니다.
6. 브라우저에서 페이지를 요청 */멤버/MembersInformation*합니다. 예를 들어 URL이 같습니다.

    `http://localhost:38366/Members/MembersInformation`

    (포트 번호 (38366) 아마도 달라 지므로 URL에서)

    로 리디렉션됩니다 합니다 *Login.cshtml* 페이지에 로그인 하지 않은 때문입니다.
7. 이전에 만든 계정을 사용 하 여 로그인 합니다. 로 다시 리디렉션됩니다 합니다 *MembersInformation* 페이지입니다. 로그인, 때문에이 이번 페이지 내용이 표시 됩니다.

여러 페이지에 대 한 액세스를 보호 하려면이 수행할 수 있습니다.

- 각 페이지에 보안 검사를 추가 합니다.
- 만들기는  *\_PageStart.cshtml* 보호 되는 페이지를 유지 하 고 있는 보안 검사를 추가할 수 있는 폴더의 페이지입니다. 합니다  *\_PageStart.cshtml* 페이지 폴더에 있는 모든 페이지에 대 한 전역 페이지의 일종으로 작동 합니다. 이 방법은에서 더 자세히 설명 되어 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)합니다.

## <a name="creating-security-for-groups-of-users-roles"></a>사용자 (역할)의 그룹에 대 한 보안 만들기

사이트에 멤버가 많은 경우 페이지를 확인 하 수 있도록 하기 전에 개별적으로 각 사용자에 대 한 권한을 확인 하려면 효율적인 아닙니다. 그룹을 만들 때 대신 수행할 수 있는 작업 또는 *역할*, 개별 멤버에 속하도록 합니다. 역할 기반 권한을 확인할 수 있습니다. 이 섹션에서는 만듭니다는 &quot;관리자&quot; 역할을 만든 다음 사용자에 액세스할 수 있는 페이지 (사용자에 속하는)에서 해당 역할입니다.

ASP.NET 멤버 자격 시스템 역할을 지원 하도록 설정 됩니다. 달리 멤버 자격 등록 및 로그인을 **시작 사이트** 템플릿에 포함 되어 있지 않습니다 역할을 관리 하는 페이지 수 있도록 합니다. (역할 관리는 사용자 작업을 하지 않고 관리 작업입니다.) 그러나 WebMatrix에서 멤버 자격 데이터베이스에서 직접 그룹을 추가할 수 있습니다.

1. WebMatrix에서를 클릭 합니다 **데이터베이스** 작업 영역 선택 기가 있습니다.
2. 왼쪽된 창에서 엽니다는 *StarterSite.sdf* 노드를 열고는 **테이블** 노드를 차례로 두 번 클릭 합니다 *웹 페이지\_역할* 테이블입니다.

    ![7-보안-멤버 자격](16-adding-security-and-membership/_static/image6.png)
3. 라는 역할을 추가 &quot;관리자&quot;합니다. 합니다 *RoleId* 필드 자동으로 채워집니다. (기본 키 이며에 설명 된 대로 식별 필드는 수로 설정 되었습니다 [ASP.NET Web Pages 사이트에서 데이터베이스를 사용 하 여 작업 소개](https://go.microsoft.com/fwlink/?LinkId=202893).)
4. 에 대 한 값은 메모를 *RoleId* 필드입니다. (첫 번째 역할 정의 하는 경우이 수는 1.)

    ![보안-멤버 자격-8](16-adding-security-and-membership/_static/image7.png)
5. 닫기 합니다 *웹 페이지\_역할* 테이블입니다.
6. 엽니다는 *UserProfile* 테이블입니다.
7. 기록해는 *UserId* 값 하나 이상의 사용자 테이블 및 테이블을 닫습니다.
8. 열기는 *웹 페이지\_UserInRoles* 테이블 및 입력을 *UserID* 및 *RoleID* 테이블에는 값입니다. 예를 들어 사용자 2에 배치 하는 &quot;관리자&quot; 역할 이러한 값을 입력 합니다.

    ![보안-멤버 자격-9](16-adding-security-and-membership/_static/image8.png)
9. 닫기 합니다 *웹 페이지\_UsersInRoles* 테이블입니다.

    역할 정의 했으므로 사용자에 게 해당 역할에 액세스할 수 있는 페이지를 구성할 수 있습니다.
10. 웹 사이트 루트 폴더 명명 된 새 페이지를 만듭니다 *AdminError.cshtml* 기존 콘텐츠를 다음 코드로 바꿉니다. 이 페이지에 대 한 액세스 허용 되지 경우에 사용자가 리디렉션되는 페이지 됩니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. 웹 사이트 루트 폴더 명명 된 새 페이지를 만듭니다 *AdminOnly.cshtml* 기존 코드를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    합니다 `Roles.IsUserInRole` 메서드가 반환 되는 `true` 현재 사용자 (이 예제의 경우 "admin" 역할)에 지정된 된 역할의 멤버인 경우.
12. 실행할 *Default.cshtml* 브라우저에서 기록 하지 않습니다. (한 경우 이미 로그인, 로그 아웃 합니다.)
13. 브라우저의 주소 표시줄에 추가할 *AdminOnly* url에서입니다. (즉, 요청 된 *AdminOnly.cshtml* 파일입니다.) 로 리디렉션됩니다 합니다 *AdminError.cshtml* 페이지에 사용자로 로그인 현재 되지 않았으므로 합니다 &quot;관리자&quot; 역할.
14. 돌아갑니다 *Default.cshtml* 에 추가 된 사용자로 로그인 합니다 &quot;관리자&quot; 역할입니다.
15. 이동할 *AdminOnly.cshtml* 페이지입니다. 이 이번에는 페이지가 표시 됩니다.

## <a name="preventing-automated-programs-from-joining-your-website"></a>웹 사이트를 가입에서 자동화 된 프로그램 방지

로그인 페이지에 자동화 된 프로그램이 중지 되지 것입니다 (라고도 *로봇 웹* 또는 *봇*) 웹 사이트에 등록 합니다. 이 절차에서는 등록 페이지에 대 한 ReCaptcha 테스트를 사용 하도록 설정 하는 방법을 설명 합니다.

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. ReCaptcha.Net에서 웹 사이트 등록 ([http://recaptcha.net](http://recaptcha.net)). 등록을 완료 하는 경우에 공개 키와 개인 키를 얻게 됩니다.
2. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.
3. 에 *계정* 폴더를 열고 파일의 이름은 *Register.cshtml*합니다.
4. 페이지의 맨 위에 있는 코드에서 다음 줄을 찾습니다 및 제거 하 여 이러한 주석 처리를 제거 합니다 `//` 주석 문자:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. 대체 `PRIVATE_KEY` 고유한 ReCaptcha 개인 키를 사용 하 여 합니다.
6. 페이지의 태그를 제거 합니다 `@*` 고 `*@` 페이지 태그에서 다음 줄에서 주석 문자:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. 대체 `PUBLIC_KEY` 넌 트 키를 사용 하 여 합니다.
8. 이미 제거 하지 않은, 경우에 제거 된 `<div>` 을 사용 하려면"CAPTCHA 확인..."로 시작 하는 텍스트를 포함 하는 요소입니다. (전체 제거 `<div>` 요소 및 해당 콘텐츠입니다.)

9. 실행할 *Default.cshtml* 브라우저에서 합니다. 사이트에 로그인 하는 경우 클릭 합니다 **로그 아웃** 링크 합니다.
10. 클릭 합니다 **등록** 에 연결 하 고 CAPTCHA 테스트를 사용 하 여 등록을 테스트 합니다.

     ![보안-멤버 자격-10](16-adding-security-and-membership/_static/image9.png)

에 대 한 자세한 내용은 합니다 `ReCaptcha` 도우미를 참조 하세요 [를 사용 하 여를 CATPCHA 방지 자동화 프로그램 (봇)에서 사용 하 여 ASP.NET 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=251967)합니다.

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>사용자가 수 있도록 외부 사이트를 사용 하 여 로그인

합니다 **시작 사이트** 템플릿은 코드 및 태그 수 있는 포함 Facebook Windows Live, Twitter, Google, Yahoo를 사용 하 여 로그인 합니다. 기본적으로이 기능은 사용 되지 않습니다. 일반적인 절차는 이러한 외부 공급자를 사용 하 여 로그인은이 사용자가 사용 합니다.

- 외부 사이트를 지원 하려면 어떤 결정 합니다.
- 필요한 경우 해당 사이트로 이동 하 고 로그인 앱을 설정 합니다. (예를 들어 해야 Facebook 로그인을 허용 하기 위해이 작업을 수행 합니다.)
- 사이트에서 공급자를 구성 합니다. 대부분의 경우에서 해야 할 몇 가지 코드의 주석을 제거 합니다  *\_AppStart.cshtml* 파일입니다.
- 태그 수 있도록 하는 등록 페이지를 추가 로그인에 대 한 외부 사이트로 연결 합니다. 일반적으로 필요 하 고 텍스트를 약간 변경 하는 태그를 복사할 수 있습니다.

항목에 대 한 단계별 지침을 찾을 수 있습니다 [ASP.NET 웹 페이지 사이트에서 외부 사이트에서 사용 하도록 설정 하면 로그인](https://go.microsoft.com/fwlink/?LinkId=251969)합니다.

사용자가 다른 사이트에서 로그인 한 후 사용자가 사이트에 반환 하 고 *연결* 사이트를 사용 하 여 로그인 합니다. 사실이 사용자의 외부 로그인에 대 한 사이트에서 멤버 자격 항목을 만듭니다. 이렇게 하면 외부 로그인을 사용 하 여 멤버 자격 (예: 역할)의 일반적인 기능을 사용할 수 있습니다.

## <a name="adding-security-to-an-existing-website"></a>기존 웹 사이트에 보안 추가

이 문서 앞부분의 절차를 사용 하 여 의존 하는 경우는 **시작 사이트** 템플릿을 웹 사이트 보안에 대 한 기준으로 합니다. 시작 하는 실용적이 지 않습니다 경우는 **시작 사이트** 템플릿 하거나 해당 템플릿을 기반으로 하는 사이트에서 관련 페이지를 복사할 구현할 수 있습니다 동일한 유형의 보안 고유한 사이트에서 직접 코딩 하 여 합니다. 동일한 형식의 페이지를 만든-등록, 로그인 및 등-를 사용 하 여 도우미 및 클래스 멤버 자격을 설정 합니다.

블로그 게시물에서 설명 하는 기본 프로세스 [ASP.NET Razor 보안을 구현 하는 가장 기본적인 방법은](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)합니다. 대부분의 작업 수행은 다음 메서드 및 속성을 사용 하는 `WebSecurity` 도우미:

- [WebSecurty.UserExists](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx), [WebSecurity.CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx). 이러한 메서드를 사용 하면 사용자가 등록 이미 되었는지 여부를 확인 하 고 등록 합니다.
- [WebSecurty.IsAuthenticated](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx)합니다. 이 속성에는 현재 사용자 기록 되는지 여부를 결정할 수 있습니다. 이러한가 이미 로그인 하지 않은 경우 로그인 페이지로 사용자를 리디렉션할 때 유용 합니다.
- [WebSecurity.Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx)하십시오 [WebSecurity.Logout](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx)합니다. 이러한 메서드 또는 out 사용자를 로그인 합니다.
- [WebSecurity.CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx)합니다. 이 속성은 (사용자가 로그인 하 고) 하는 경우 현재 사용자의 로그인 이름을 표시 하는 데 유용 합니다.
- [WebSecurity.ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx)합니다. 이 메서드는 등록에 대 한 전자 메일 확인을 설정 하는 경우에 유용 합니다. (자세한 내용은 블로그 게시물에 설명 되어 [ASP.NET Web Pages 보안에 대 한 확인 기능을 사용 하 여](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267).)

역할을 관리 하려면 사용할 수 있습니다 합니다 [역할](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx) 하 고 [멤버 자격](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx) 블로그 항목에 설명 된 대로 클래스입니다.

## <a name="additional-resources"></a>추가 리소스

- [사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [보안 웹 통신: 인증서, SSL 및 https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- [ASP.NET Razor 보안을 구현 하는 가장 기본적인 방법은](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240) 하 고 [ASP.NET 웹 페이지 보안에 대 한 확인 기능을 사용 하 여](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)입니다. 다음은 사용 하지 않고 ASP.NET 멤버 자격 기능을 구현 하는 방법에 설명 하는 블로그 게시물을 **시작 사이트** 템플릿.
- [ASP.NET 웹 페이지 사이트에서 외부 사이트 로그인 사용](https://go.microsoft.com/fwlink/?LinkId=251969)
- [WebSecurity 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99)) (MSDN)
- [SimpleRoleProvider 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99)) (MSDN)
- [SimpleMembershipProvider 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99)) (MSDN)
