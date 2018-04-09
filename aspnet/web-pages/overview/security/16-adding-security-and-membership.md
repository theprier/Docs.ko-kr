---
uid: web-pages/overview/security/16-adding-security-and-membership
title: (Razor) 사이트 페이지에 ASP.NET 웹 보안 및 구성원 자격 추가 | Microsoft Docs
author: tfitzmac
description: 이 장의 페이지 중 일부가 작업을 사용자에 게 로그인에 사용할 수 있도록 웹 사이트를 보호 하는 방법을 보여 줍니다. (도 확인할 수 페이지 tha...를 만드는 방법
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/24/2014
ms.topic: article
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: 351368a356a71e85d4abfdceac8d4f84e0b217f4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 보안 및 구성원 추가
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 페이지 중 일부가 작업을 사용자에 게 로그인에 사용할 수 있도록는 ASP.NET 웹 페이지 (Razor) 웹 사이트를 보호 하는 방법에 설명 합니다. (도 확인할 수 누구나 액세스할 수 있는 페이지를 만드는 방법입니다.)
> 
> **학습 내용:** 
> 
> - 일부 페이지에 대 한 멤버만에 대 한 액세스를 제한할 수 있도록 등록 및 로그인 페이지가 있는 웹 사이트를 만드는 방법.
> - 공용 및 멤버 전용 페이지를 만드는 방법입니다.
> - 사이트에 대 한 다른 보안 권한이 있는 그룹 역할을 정의 하는 방법 및 사용자 역할에 할당 하는 방법입니다.
> - 자동화 된 프로그램 (bot) 구성원 계정을 만드는 하지 않도록 하려면 CAPTCHA를 사용 하는 방법.
>   
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - WebMatrix는 **시작 사이트** 템플릿.
> - `WebSecurity` 도우미 및 `Roles` 클래스입니다.
> - `ReCaptcha` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3
> - ASP.NET Web Helpers Library


사용자가 로그인 할 수 있도록 웹 사이트를 설정할 수 &#8212; 즉, 사이트에서 지원 되도록 *구성원*합니다. 이 유용 여러 가지 이유로 합니다. 예를 들어 사이트 멤버에만 사용할 수 있는 여러 페이지가 있을 수 있습니다. 경우에 따라 사용자 피드백을 보낼 명령을 남길 수 있도록 로그인에 필요할 수 있습니다.

웹 사이트 멤버 자격을 지 원하는 경우에 사용자가 반드시 페이지 중 일부가 사이트에 사용 하기 전에 로그인 할 필요가 없습니다. 사용자가 로그인 하지 않은 라고 *익명 사용자에 게*합니다.

사용자 웹 사이트에 등록 하 고 사이트에 로그인 할 수 있습니다. 웹 사이트에는 사용자 이름 (전자 메일 주소) 및 사용자에 게 되도록 신원이 되는지 확인 하는 데 암호 필요 합니다. 로그인 하 고 사용자의 id를 확인 하는이 과정 라고 *인증*합니다.

다른 방법으로 보안 및 멤버 자격을 설정할 수 있습니다.

- WebMatrix를 사용 하는 쉽게 새 사이트를 기반으로 만드는 것입니다는 **시작 사이트** 템플릿. 이 서식 파일 보안과 멤버 자격에 대해 이미 구성 되어 있으며 이미 등록 페이지, 로그인 페이지 및 등입니다.

    템플릿을 통해 생성 된 사이트 사용자가 Facebook, Google와 같은 외부 사이트를 사용 하 여 로그인 하거나 Twitter 수 하는 옵션도 있습니다.
- 보안을 기존 사이트를 추가 하려는 경우 또는 사용 하지 않을 경우는 **시작 사이트** 서식 파일을 직접 등록 페이지, 로그인 페이지 및에 만들 수 있습니다.

이 문서에서는 첫 번째 옵션 &mdash; 를 사용 하 여 보안을 추가 하는 방법의 **시작 사이트** 템플릿. 또한 사용자 고유의 보안을 구현 하는 방법에 대 한 몇 가지 기본 정보를 제공 하 고 작업을 수행 하는 방법에 대 한 자세한 정보에 대 한 링크를 제공 합니다. 별도 문서에 자세히 설명 된 외부 로그인을 사용 하는 방법에 대 한 정보 이기도 합니다.

## <a name="creating-website-security-using-the-starter-site-template"></a>시작 사이트 템플릿의 사용 하 여 웹 사이트 보안 만들기

WebMatrix에서 사용할 수 있습니다는 **시작 사이트** 템플릿을를 다음을 포함 하는 웹 사이트를 만듭니다.

- 멤버의 사용자 이름과 암호를 저장 하는 데 사용 되는 데이터베이스입니다.
- 등록 페이지 (새로 만들기) 익명 사용자가 등록할 수 있습니다.
- 로그인 및 로그 아웃 페이지입니다.
- 암호 복구 및 다시 설정 페이지입니다.

다음 절차는 사이트를 만들고 구성 하는 방법을 설명 합니다.

1. WebMatrix를 시작 및는 **빠른 시작** 페이지에서 **템플릿에서 사이트**합니다.
2. 선택 된 **시작 사이트** 템플릿과 클릭 **확인**합니다. WebMatrix에 새 사이트를 만듭니다.
3. 왼쪽된 창에서 클릭 된 **파일** 작업 선택기입니다.
4. 웹 사이트의 루트 폴더를 열고는  *\_AppStart.cshtml* 전역 설정을 포함 하는 데 사용 되는 특수 한 파일에 있는 파일입니다. 주석 처리를 사용 하 여 일부 문이 포함 된 `//` 문자:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    이러한 문은 구성는 `WebMail` 도우미 전자 메일을 보내는 데 사용할 수 있습니다. 멤버 자격 시스템 암호를 변경 하려는 경우 또는 사용자가 등록할 때 확인 메시지를 보낼 전자 메일을 사용할 수 있습니다. (예를 들어 사용자가 등록 한 후 받게 등록 프로세스를 완료 하기 위해 클릭할 수 있는 링크가 포함 된 전자 메일.)

    에 설명 된 대로 SMTP 서버에 대 한 액세스 전자 메일을 보내는 필요 [ASP.NET 웹 페이지 사이트에 전자 메일 추가](https://go.microsoft.com/fwlink/?LinkId=202899)합니다. 이 중앙에 전자 메일 설정을 저장할  *\_AppStart.cshtml* 파일 전자 메일을 보낼 수 있는 각 페이지에 반복 해 서 코드를 작성할 필요가 없습니다. (등록 데이터베이스를 설정 하려면 SMTP 설정을 구성할 필요가 없습니다; 하기만 하면 SMTP 설정을 사용자의 전자 메일 별칭이에서 유효성을 검사 하며, 사용자 수 잊어버린된 암호를 재설정 하려는 경우)
5. 문을 제거 하 여 주석 처리 제거 `//` 각 앞입니다.

    전자 메일 확인을 설정 하지 않을 경우이 단계와 다음 단계를 건너뛸 수 있습니다. SMTP 값을 설정 하지 않은 경우 새 계정은 확인 전자 메일이 없이 즉시 사용할 수 있습니다.
6. 코드의 다음 전자 메일 관련 설정을 수정 합니다.

   - 설정 `WebMail.SmtpServer` 에 액세스할 수 있는 SMTP 서버의 이름입니다.
   - 둡니다 `WebMail.EnableSsl` 로 설정 `true`합니다. 이 설정을 암호화 하 여 SMTP 서버에 전송 되는 자격 증명을 보호 합니다.
   - 설정 `WebMail.UserName` SMTP 서버 계정의 사용자 이름에 있습니다.
   - 설정 `WebMail.Password` 를 SMTP 서버 계정의 암호입니다.
   - 설정 `WebMail.From` 자신의 전자 메일 주소로 합니다. 메시지에서 보내는 전자 메일 주소입니다.

     > [!NOTE] 
     > 
     > **팁** 이러한 속성에 대 한 값에 대 한 자세한 내용은 참조 하십시오. [전자 메일 설정 구성](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings) 에 [사이트 전체의 동작을 사용자 지정 ASP.NET 웹 페이지에 대 한](https://go.microsoft.com/fwlink/?LinkID=202906)합니다.
7. 저장 후 닫기  *\_AppStart.cshtml*합니다.
8. 실행 된 *Default.cshtml* 브라우저에서 페이지입니다.

    ![보안-멤버 자격-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > 속성의 인스턴스를 되도록 알리는 오류가 표시 되 면 `ExtendedMembershipProvider`, ASP.NET 웹 페이지 멤버 자격 시스템 (SimpleMembership)를 사용 하도록 사이트를 구성할 수 있습니다. 호스팅 공급자의 서버가 로컬 서버와 다르게 구성 된 경우에 발생할 경우에 따라 수 있습니다. 이 해결 하려면 다음 요소를 사이트의 추가 *Web.config* 파일:
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > 이 요소의 자식으로 추가 `<configuration>` 요소와의 피어로 `<system.web>` 요소입니다.
9. 페이지의 오른쪽 위 구석에 클릭는 **등록** 링크 합니다. *Register.cshtml* 페이지가 표시 됩니다.
10. 사용자 이름 및 암호를 입력 한 다음 클릭 **등록**합니다.

    ![보안-멤버 자격-3](16-adding-security-and-membership/_static/image2.png)

    웹 사이트를 만들 때의 **시작 사이트** 템플릿, 라는 데이터베이스 *StarterSite.sdf* 사이트의에서 만든 *앱\_데이터* 폴더입니다. 등록 하는 동안 사용자 정보가 데이터베이스에 추가 됩니다. SMTP 값으로 설정 하면 메시지는 전자 메일 주소로 전송 됩니다 사용한 등록을 완료할 수 있습니다.

    ![보안-멤버 자격-4](16-adding-security-and-membership/_static/image3.png)
11. 전자 메일 프로그램으로 이동한 사이트에 인증 코드 및 하이퍼링크를 포함 하는 메시지를 찾을 합니다.
12. 계정을 활성화 하려면 하이퍼링크를 클릭 합니다. 확인 하이퍼링크가 등록 확인 페이지를 엽니다.

    ![security-membership-5](16-adding-security-and-membership/_static/image4.png)
13. 클릭는 **로그인** 링크를 선택한 다음 등록 하는 계정을 사용 하 여 로그인 합니다.

      로그인 한 후는 **로그인** 및 **등록** 링크로 대체 됩니다는 **로그 아웃** 링크 합니다. 사용자의 로그인 이름 링크로 표시 됩니다. (링크 하면 페이지로 이동 하는 암호를 변경할 수 있습니다.)

      ![보안-멤버 자격-6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > 기본적으로 ASP.NET 웹 페이지 보낼 자격 증명 서버에 일반 텍스트로 (이해 하기 쉬운 텍스트로). 프로덕션 사이트 보안 HTTP를 사용 합니다 (https://, 또한 다음 이라고 알려집니다는 *보안 소켓 레이어* 또는 SSL) 서버와 교환 되는 중요 한 정보를 암호화 합니다. 필요한 전자 메일 수 메시지를 보낼 수 있도록 설정 하 여 SSL을 사용 하 여 `WebMail.EnableSsl=true` 앞의 예와 합니다. SSL에 대 한 자세한 내용은 참조 [웹 통신 보안: 인증서, SSL 및 https://](https://go.microsoft.com/fwlink/?LinkId=208660)합니다.

## <a name="additional-membership-functionality-in-the-site"></a>사이트에서 추가 멤버 자격 기능

사이트는 사용자가의 계정을 관리할 수 있는 기타 기능을 포함 합니다. 사용자가 다음을 수행할 수 있습니다.

- 암호를 변경 합니다. 로그인 한 후에 사용자 이름 (링크)을 클릭할 수 있습니다. 이 작업을 수행 하는 페이지에 새 암호를 만들 수 있습니다 (*Account/ChangePassword.cshtml*).
- 암호를 잊은 경우 복구 합니다. 로그인 페이지에는 링크 (**암호 잊으셨나요?**) 사용자가 페이지를 사용 하는 (*Account/ForgotPassword.cshtml*) 전자 메일 주소를 입력할 수 있습니다. 사이트에 새 암호를 설정 하기 위해 클릭할 수 있는 링크가 포함 되어 있는 전자 메일 메시지를 보냅니다 (*Account/PasswordReset.cshtml*).

사용자가 나중에 설명 된 대로 외부 사이트를 사용 하 여 로그인도 가능 하도록 할 수도 있습니다.

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>멤버 전용 페이지 만들기

시간 중인 누구나 웹 사이트의 모든 페이지를 볼 수 있는 합니다. 그러나에 로그인 한 사용자만 사용할 수 있는 페이지에 있어야 하는 경우가 있습니다 (즉, 멤버에). ASP.NET 멤버 로그인만 액세스할 수 있는 페이지를 만들 수 있습니다. 일반적으로 익명 사용자를 멤버 전용 페이지에 액세스 하려고 하면 리디렉션됩니다 로그인 페이지에 있습니다.

이 절차에서는 로그인 한 사용자에만 사용할 수 있는 페이지에 포함 될 폴더를 만들어야 합니다.

1. 사이트의 루트에서 새 폴더를 만듭니다. (리본 메뉴에서 아래쪽 화살표를 클릭 합니다. **새로** 선택한 후 **새 폴더**.)
2. 새 폴더 이름을 *멤버*합니다.
3. 내에서 *멤버* 폴더를 새 페이지를 만들고 이라는 *MembersInformation.cshtml*합니다.
4. 다음 코드와 태그 기존 내용을 바꿉니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    이 코드는 테스트는 `IsAuthenticated` 속성의는 `WebSecurity` 개체를 반환 하는 `true` 사용자가 로그인 하는 경우. 사용자가 로그인 하지 않은 경우, 코드를 호출 하 여 `Response.Redirect` 를 사용자에 게 보낼지는 *Login.cshtml* 페이지에 *계정* 폴더입니다.

    리디렉션 URL에 포함 한 `returnUrl` 쿼리를 사용 하는 문자열 값 `Request.Url.LocalPath` 현재 페이지의 경로를 설정 합니다. 설정 하는 경우는 `returnUrl` 다음과 같은 쿼리 문자열의 값 (및 반환 URL 로컬 경로인 경우)에 로그인 한 후 로그인 페이지가이 페이지를 사용자가 반환 됩니다.

    코드에서는 또한 설정  *\_SiteLayout.cshtml* 있으며 레이아웃 페이지와 페이지. (레이아웃 페이지에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에서 일관 된 레이아웃을 만드는](https://go.microsoft.com/fwlink/?LinkId=202891).)
5. 사이트를 실행 합니다. 로그인 계속을 클릭는 **로그 아웃** 페이지의 위쪽에 단추입니다.
6. 브라우저에서 페이지를 요청 */멤버/MembersInformation*합니다. 예를 들어 URL은 다음과 같이 표시 될 수 있습니다.

    `http://localhost:38366/Members/MembersInformation`

    ((38366) 포트 번호는가 됩니다 URL과 다릅니다.)

    리디렉션됩니다 하는 *Login.cshtml* 로그인 하지 않은 때문에 페이지입니다.
7. 앞에서 만든 계정을 사용 하 여 로그인 합니다. 으로 다시 리디렉션됩니다 하는 *MembersInformation* 페이지. 로그인 되어 있으므로이 현재 페이지 내용이 표시 합니다.

여러 페이지에 대 한 액세스를 보호 하려면이 수행할 수 있습니다.

- 각 페이지에 보안 검사를 추가 합니다.
- 만들기는  *\_PageStart.cshtml* 보호 되는 페이지를 유지 하 고는 보안 검사를 추가할 수 있는 폴더의 페이지에에서 있습니다.  *\_PageStart.cshtml* 페이지는 역할을 폴더에 있는 모든 페이지에 대 한 전역 페이지의 종류입니다. 이 방법은에서 더 자세하게 설명 [사이트 전체의 동작을 사용자 지정 ASP.NET 웹 페이지에 대 한](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)합니다.

## <a name="creating-security-for-groups-of-users-roles"></a>사용자 (역할)의 그룹에 대 한 보안 만들기

사이트에는 많은 멤버를 벗어나게 페이지가 표시 하기 전에 개별적으로 각 사용자에 대 한 권한이 있는지 확인 하는 효율적인있지 않습니다. 대신 그룹을 만들고는 수행할 수 있는 작업 또는 *역할*, 개별 멤버에 속함을 합니다. 그런 다음 역할에 따라 사용 권한을 확인할 수 있습니다. 이 섹션에서는 만듭니다는 &quot;관리자&quot; 역할 및 다음 인 사용자에 액세스할 수 있는 페이지를 만듭니다 (게 속한)에 해당 역할입니다.

ASP.NET 멤버 자격 시스템에서는 역할을 지원 합니다. 그러나 멤버 자격 등록 및 로그인을 달리는 **시작 사이트** 템플릿에 포함 되어 있지 않으면 역할을 관리 하는 데 도움이 되는 페이지입니다. (역할 관리는 사용자 작업을 보다는 관리 작업입니다.) 그러나 WebMatrix에서 멤버 자격 데이터베이스에 직접 그룹을 추가할 수 있습니다.

1. WebMatrix에서 클릭 된 **데이터베이스** 작업 선택기입니다.
2. 왼쪽된 창에서 열고는 *StarterSite.sdf* 노드를 열고는 **테이블** 노드를 차례로 두 번 클릭은 *웹 페이지\_역할* 테이블입니다.

    ![보안-멤버 자격-7](16-adding-security-and-membership/_static/image6.png)
3. 명명 된 역할을 추가 &quot;admin&quot;합니다. *RoleId* 필드가 자동으로 입력 됩니다. (기본 키 이며에 설명 된 대로 식별 필드 수로 설정 된 [ASP.NET 웹 페이지 사이트에서 데이터베이스 작업을 소개](https://go.microsoft.com/fwlink/?LinkId=202893).)
4. 에 대 한 값이 기록의 *RoleId* 필드입니다. (정의 하는 첫 번째 역할 이면 됩니다 1.)

    ![보안-멤버 자격-8](16-adding-security-and-membership/_static/image7.png)
5. 닫기는 *웹 페이지\_역할* 테이블입니다.
6. 열기는 *UserProfile* 테이블입니다.
7. 메모는 *UserId* 사용자 테이블과 닫힙니다 테이블에 하나 이상의 값입니다.
8. 열기는 *웹 페이지\_UserInRoles* 테이블을 입력 한 *UserID* 및 *RoleID* 테이블에는 값입니다. 예를 들어, 사용자 2에 배치 하는 &quot;admin&quot; 역할을 이러한 값을 입력 합니다.

    ![보안-멤버 자격-9](16-adding-security-and-membership/_static/image8.png)
9. 닫기는 *웹 페이지\_UsersInRoles* 테이블입니다.

    역할 정의가지고 해당 역할에 사용자에 액세스할 수 있는 페이지를 구성할 수 있습니다.
10. 웹 사이트 루트 폴더에 명명 된 새 페이지를 만듭니다 *AdminError.cshtml* 기존 콘텐츠를 다음 코드로 바꿉니다. 이 페이지에 대 한 액세스 허용 되지 않습니다 경우 사용자는 리디렉션됩니다 페이지 됩니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. 웹 사이트 루트 폴더에 명명 된 새 페이지를 만듭니다 *AdminOnly.cshtml* 기존 코드를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    `Roles.IsUserInRole` 메서드 반환 `true` 현재 사용자 (이 경우 "관리" 역할)에 지정된 된 역할의 멤버인 경우.
12. 실행 *Default.cshtml* 브라우저에서 하지만 기록 하지 않습니다. (한 경우 이미 로그인, 로그 아웃 합니다.)
13. 브라우저의 주소 표시줄에 추가 *AdminOnly* url에서입니다. (즉, 요청 된 *AdminOnly.cshtml* 파일입니다.) 리디렉션됩니다 하는 *AdminError.cshtml* 에 사용자로 로그인 현재 하지 않은 때문에 페이지는 &quot;관리자&quot; 역할입니다.
14. 으로 돌아와서 *Default.cshtml* 에 추가한 사용자로 로그인 하 고는 &quot;admin&quot; 역할입니다.
15. 찾아 *AdminOnly.cshtml* 페이지. 이 현재 페이지를 참조 합니다.

## <a name="preventing-automated-programs-from-joining-your-website"></a>웹 사이트에 참석 자동된 프로그램 방지

로그인 페이지에서는 자동화 된 프로그램이 중지 되지 않습니다 (라고도 *로봇 웹* 또는 *bot*) 웹 사이트에 등록 합니다. 이 절차에서는 등록 페이지에 대 한 ReCaptcha 테스트를 사용 하도록 설정 하는 방법을 설명 합니다.

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. ReCaptcha.Net에서 웹 사이트 등록 ([http://recaptcha.net](http://recaptcha.net)). 등록을 완료 하면, 공개 키와 개인 키를 볼 수 있습니다.
2. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)아직 없는 경우, 합니다.
3. 에 *계정* 폴더를 열고 파일의 이름은 *Register.cshtml*합니다.
4. 페이지 맨 위에 있는 코드에서 다음 줄 찾기 및 제거 하 여 주석 처리 제거는 `//` 주석 문자:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. 대체 `PRIVATE_KEY` 고유한 ReCaptcha 개인 키와 함께 합니다.
6. 페이지의 태그를 제거는 `@*` 및 `*@` 페이지 태그에 다음 줄에서 주석 문자:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. 대체 `PUBLIC_KEY` 사용자 키로 합니다.
8. 이미 제거 하지 않은, 경우 제거 된 `<div>` 을 사용 하려면"CAPTCHA 확인..."로 시작 하는 텍스트가 포함 된 요소입니다. (전체 제거 `<div>` 요소와 해당 내용입니다.)

9. 실행 *Default.cshtml* 브라우저에서 합니다. 사이트에 로그인 하 고, 클릭는 **로그 아웃** 링크 합니다.
10. 클릭는 **등록** 에 연결 하 고 CAPTCHA 테스트를 사용 하 여 등록을 테스트 합니다.

     ![보안-멤버 자격-10](16-adding-security-and-membership/_static/image9.png)

에 대 한 자세한 내용은 `ReCaptcha` 도우미, 참조 [를 사용 하 여 한 CATPCHA 자동화 된 프로그램 방지 (Bot)에서 사용 하 여 ASP.NET 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=251967)합니다.

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>사용자가 수 있도록 외부 사이트를 사용 하 여 로그인

**시작 사이트** 코드와 사용자가 수 있는 태그를 포함 하는 서식 파일 Facebook, Windows Live, Twitter, Google 또는 Yahoo를 사용 하 여 로그인 합니다. 기본적으로이 기능은 사용 되지 않습니다. 일반적인 절차는 이러한 외부 공급자를 사용 하 여 로그인은이 사용자가 사용 하기 위한:

- 외부 사이트를 지원 하려면 어떤 결정 합니다.
- 필요한 경우 해당 사이트로 이동 하 고 로그인 앱을 설정 합니다. (예를 들어 해야 Facebook 로그인 할 수 있도록이 작업을 수행 합니다.)
- 사이트의 공급자를 구성 합니다. 대부분의 경우에서 하기만 하면 일부 코드의 주석 처리를 제거 하는  *\_AppStart.cshtml* 파일입니다.
- 구독을 통해 사용자는 등록 페이지에 태그를 추가 합니다. 로그인에 대 한 외부 사이트에 링크 합니다. 일반적으로 필요 하 고 텍스트를 약간 변경 하는 태그를 복사할 수 있습니다.

항목에 대 한 단계별 지침을 찾을 수 있습니다 [ASP.NET 웹 페이지 사이트에서 외부 사이트에서 로그인을 사용 하도록 설정](https://go.microsoft.com/fwlink/?LinkId=251969)합니다.

사용자 사이트 사용자가 다른 사이트에서 로그인 한 후 돌아가면 및 *연결* 사이트에 로그인 합니다. 실제로 사용자의 외부 로그인에 대 한 사이트에 멤버 자격 항목을 만들어집니다. 이렇게 하면 멤버 자격 (예: 역할)의 일반적인 기능을 사용 하 여 외부 로그인을 사용 합니다.

## <a name="adding-security-to-an-existing-website"></a>보안을 기존 웹 사이트 추가

이 문서 앞부분의 절차를 사용 하 여 의존 하는 경우는 **시작 사이트** 템플릿을 웹 사이트 보안을 위한 기반으로 합니다. 시작 하는 적합 하지 않은 경우는 **시작 사이트** 템플릿에 해당 템플릿을 기반으로 하는 사이트에서 관련 페이지를 복사할 구현할 수 있습니다는 동일한 유형의 보안 자신의 사이트에 직접 코딩 하 여 합니다. 동일한 유형의 페이지를 만들-등록, 로그인 및 등-를 사용 하 여 도우미 및 클래스 멤버 자격을 설정 합니다.

블로그 게시물에 설명 하는 기본 프로세스 [ASP.NET Razor 보안을 구현 하는 가장 기본적인 방법은](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)합니다. 대부분의 작업이 수행 되는 다음의 메서드와 속성을 사용 하는 `WebSecurity` 도우미:

- [WebSecurty.UserExists](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx), [WebSecurity.CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx). 이러한 메서드를 사용 하면 누군가가 등록 이미 되어 있는지 여부를 확인 하 고를 등록 합니다.
- [WebSecurty.IsAuthenticated](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx)합니다. 이 속성에는 현재 사용자가 로그인 하는지 여부를 결정할 수 있습니다. 이러한가 이미 로그인 하지 않은 경우 사용자는 로그인 페이지를 리디렉션하려면 유용 합니다.
- [WebSecurity.Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx), [WebSecurity.Logout](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx). 이러한 메서드 또는 out 사용자를 로그인합니다.
- [WebSecurity.CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx). 이 속성은 현재 사용자의 로그인 이름 (사용자가 로그인 하 고) 하는 경우이 표시 하는 데 유용 합니다.
- [WebSecurity.ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx)합니다. 이 메서드는 등록에 대 한 전자 메일 확인을 설정 하는 경우에 유용 합니다. (세부 블로그 게시물에 설명 되어 [확인 기능을 사용 하 여 ASP.NET 웹 페이지 보안용](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267).)

역할을 관리 하려면 사용할 수 있습니다는 [역할](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx) 및 [구성원](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx) 블로그 항목에 설명 된 대로 클래스입니다.

## <a name="additional-resources"></a>추가 자료

- [사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [웹 통신을 보호: 인증서, SSL 및 https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- [ASP.NET Razor 보안을 구현 하는 가장 기본적인 방법은](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240) 및 [확인 기능을 사용 하 여 ASP.NET 웹 페이지 보안용](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)합니다. 다음은 사용 하지 않고 ASP.NET 멤버 자격 기능을 구현 하는 방법을 설명 하는 블로그 게시물은 **시작 사이트** 서식 파일입니다.
- [ASP.NET 웹 페이지 사이트에서 외부 사이트 로그인 사용](https://go.microsoft.com/fwlink/?LinkId=251969)
- [WebSecurity 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99)) (MSDN)
- [SimpleRoleProvider 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99)) (MSDN)
- [SimpleMembershipProvider 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99)) (MSDN)
