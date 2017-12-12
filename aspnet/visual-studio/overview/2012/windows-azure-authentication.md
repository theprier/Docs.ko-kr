---
uid: visual-studio/overview/2012/windows-azure-authentication
title: "Windows Azure 인증 | Microsoft Docs"
author: Rick-Anderson
description: "Windows Azure Active Directory 용 Microsoft ASP.NET 도구가 사용 하면 Windows Azure 웹 사이트에 호스팅된 웹 응용 프로그램에 대 한 인증을 사용 하도록 설정 하려면 단순..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2013
ms.topic: article
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1cb38d66bd0373159e54abf822fba9c5829774ac
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="windows-azure-authentication"></a>Windows Azure 인증
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> Windows Azure Active Directory를 사용 하면 간단 하 게에서 호스팅된 웹 응용 프로그램에 대 한 인증을 사용 하도록 설정에 대 한 Microsoft ASP.NET 도구 [Windows Azure 웹 사이트](https://www.windowsazure.com/en-us/home/features/web-sites/)합니다. Office 365 사용자 인증을 위해 조직, 온-프레미스 Active Directory에서 동기화 된 회사 계정 또는 사용자 고유의 사용자 지정 Windows Azure Active Directory 도메인에서 만든 사용자가 Windows Azure 인증을 사용할 수 있습니다. Windows Azure 인증을 사용 하도록 설정 단일을 사용 하 여 사용자를 인증 하는 응용 프로그램을 구성 [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) 테 넌 트입니다.
> 
> 클라우드 서비스에서 웹 역할에 대 한 ASP.NET Windows Azure 인증 도구를 사용할 수 없습니다 하지만 이후 릴리스에서 그러려면 계획 합니다. [Windows Identity Foundation](https://msdn.microsoft.com/en-us/library/hh291066(v=VS.110).aspx) (WIF)는 Windows Azure 웹 역할에서 지원 됩니다.
> 
> 온-프레미스 Active Directory와 Windows Azure Active Directory 테 넌 트 간의 동기화를 설정 하는 방법에 대 한 자세한 내용은 참조 하십시오 [구현 및 관리를 사용 하 여 AD FS 2.0 single sign on](https://technet.microsoft.com/en-us/library/jj205462.aspx)합니다.
> 
> Windows Azure Active Directory는 현재 보기로 사용할 수는 [무료 미리 보기 서비스](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.


## <a name="requirements"></a>요구 사항:

- Visual Studio 2012 또는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/en-us/products/express)
- [웹 도구 Visual Studio 2012 용 확장](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) 또는 [웹 도구 확장에 대 한 Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)
- [Microsoft ASP.NET Windows 용 도구 Visual Studio 2012 Azure Active Directory –](https://go.microsoft.com/fwlink/?LinkID=282306) 또는 [Windows 용 Microsoft ASP.NET 도구 Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>Visual Studio 2012를 사용한 ASP.NET 웹 응용 프로그램 만들기

이 자습서에서는 ASP.NET MVC 인트라넷 서식 파일 사용, Visual Studio 2012를 사용한 모든 웹 응용 프로그램을 만들 수 있습니다.

1. 새 ASP.NET MVC 4 인트라넷 응용 프로그램을 만들고 모든 기본값을 적용 합니다. (In 여야 **통과** net에 없고 **입력** net 프로젝트).  
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>(러 우면는 개념의 전역 관리자) 창을 Azure 인증을 사용 합니다.

예를 들어 (기존 Office 365 계정)를 통해 기존 Windows Azure Active Directory 테 넌 트가 없는 경우에 등록 하 여 새 테 넌 트를 만들 수 있습니다는 [새 Windows Azure Active Directory 계정](http://g.microsoftonline.com/0AX00en/5)합니다.

1. 프로젝트 메뉴에서 선택 **Windows Azure 인증 사용**:  
  
 ![](windows-azure-authentication/_static/image2.png)

2. 에 Windows Azure Active Directory 테 넌 트 (예: contoso.onmicrosoft.com)에 대 한 도메인을 입력 하 고 클릭 **사용**:

![](windows-azure-authentication/_static/image3.png)

3. 웹 인증 대화 상자에 있는 기호 Windows Azure Active Directory 테 넌 트의 관리자:  
  
 ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>관리자가 아닌는 개념의 여 Window Azure를 사용 하도록 설정

Windows Azure Active Directory 테 넌 트에 대 한 전역 관리자 권한이 없는 경우 응용 프로그램을 프로 비전 하는 것에 대 한 확인란 선택을 취소할 수 있습니다.

![](windows-azure-authentication/_static/image6.png)

대화 상자가 표시 된 **도메인**, **응용 프로그램 보안 주체 Id** 및 **회신 URL** Azure Active Directory와 응용 프로그램을 프로 비전 하기 위해 필요한 개념입니다. 응용 프로그램을 프로 비전에 충분 한 권한을 갖고 있는에이 정보를 제공 해야 합니다. 참조[single sign on Windows Azure Active Directory-ASP.NET 응용 프로그램으로 구현 하는 방법을](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) 서비스 사용자를 수동으로 만들려면 cmdlet을 사용 하는 방법에 대 한 자세한 내용은 합니다.  
응용 프로그램이 성공적으로 프로 비전을 클릭할 때 **계속 해 서 선택한 설정으로 web.config 업데이트**합니다. 클릭할 수 있는 업데이트를 프로 비전 하기 위해 대기 하는 동안 응용 프로그램 개발을 계속 하려는 경우 **에 가깝게 프로젝트 파일의 설정을 기억**합니다. 다음에 Windows Azure 인증 사용을 호출 하 고 프로 비전 확인란의 선택을 취소, 동일한 설정을 볼 수 있습니다 및 클릭할 수 있는 **계속**를 클릭 한 다음 **web.config에서이러한설정을적용**.

1. 응용 프로그램은 Windows Azure 인증용으로 구성 하 고 Windows Azure Active Directory와 사용자를 프로 비전 하는 동안 대기 합니다.
2. Windows Azure 인증을 응용 프로그램에 대해 사용 되 면 클릭 **닫기:** 

    ![](windows-azure-authentication/_static/image7.png)
3. F5 키를 눌러 응용 프로그램을 실행 합니다. 자동으로 로그인 페이지로 리디렉션됩니다 해야 합니다. 디렉터리 개념 사용자 자격 증명을 사용 하 여 응용 프로그램에 로그인 할...  

    ![](windows-azure-authentication/_static/image1.jpg)
4. 응용 프로그램에서 현재 자체 서명 된 테스트 인증서를 사용 하므로 인증서는 신뢰할 수 있는 인증 기관에서 발급 되지 않았습니다 지 브라우저에서 경고를 받습니다.

    이 경고는 무시 해도 됩니다 로컬 개발 하는 동안를 클릭 하 여 **이 웹 사이트를 계속 탐색 합니다.** 

    ![](windows-azure-authentication/_static/image8.png)
5. 이제 성공적으로 로그인 한 Windows Azure 인증을 사용 하 여 응용 프로그램에!

    ![](windows-azure-authentication/_static/image2.jpg)

Windows Azure를 사용 하면 인증 변경한 다음 응용 프로그램에:

- Anti 상호 사이트 요청 위조 ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) 클래스 ( *앱\_Start\AntiXsrfConfig.cs* ) 프로젝트에 추가 합니다.
- NuGet 패키지 `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` 프로젝트에 추가 합니다.
- Windows Identity Foundation 설정이 응용 프로그램에서 Windows Azure Active Directory 테 넌 트의 보안 토큰을 수락 하도록 구성 됩니다. 확장된 된 보기의 변경 내용을 확인 하려면 아래 이미지를 클릭은 *Web.config* 파일입니다.  
  
     ![](windows-azure-authentication/_static/image9.png)
- Windows Azure Active Directory 테 넌 트에 응용 프로그램에 대 한 서비스 사용자를 프로 비전 됩니다.
- HTTPS 사용 됩니다.

## <a name="deploy-the-application-to-windows-azure"></a>Windows Azure에 응용 프로그램 배포

자세한 내용은 참조 하십시오. [Windows Azure 웹 사이트에 ASP.NET 웹 응용 프로그램 배포](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)합니다.

Azure 웹 사이트에 Windows Azure 인증을 사용 하 여 응용 프로그램을 게시 합니다.

1. 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 선택 **게시:** 

    ![](windows-azure-authentication/_static/image3.jpg)
2. 웹 게시 대화 상자에서 다운로드 하 고 Azure 웹 사이트에 대 한 게시 프로필을 가져옵니다.

    ![](windows-azure-authentication/_static/image4.jpg)
3. **연결** 표시 탭의 **대상 URL** (응용 프로그램에 대 한 공용 웹 URL). 클릭 **연결 유효성 검사** 연결 테스트 하려면:

    ![](windows-azure-authentication/_static/image5.jpg)
4. 이 Azure 웹 사이트에 게시 한 경우 이전에 것이 좋습니다 검사는 **대상에서 추가 파일 제거** 응용 프로그램을 유지 하도록 설정을 완전히 게시 합니다. 공지는 **Windows Azure 인증 사용** 확인란은 slected 합니다.  

    ![](windows-azure-authentication/_static/image10.png)
5. : 옵션는 **미리 보기** 탭 클릭 **미리 보기 시작** 배포 파일을 볼 수 있습니다.

    ![](windows-azure-authentication/_static/image6.jpg)
6. 클릭 **게시 합니다.**

    대상 호스트에 대 한 Windows Azure 인증을 묻는 메시지가 나타납니다. 클릭 **사용** 계속 하려면:

    ![](windows-azure-authentication/_static/image11.png)
7. Windows Azure Active Directory 테 넌 트 관리자 자격 증명을 입력 합니다.

    ![](windows-azure-authentication/_static/image7.jpg)
8. 응용 프로그램이 성공적으로 게시 되 면 게시 된 웹 사이트에는 브라우저에서 열립니다.

    > [!NOTE]
    > 최대 5 분 (일반적으로 반드시 덜) 완전 하 게 프로 비전 할 Windows Azure Active Directory와 대상 호스트에 대 한 Windows Azure 인증을 사용 하도록 설정한 후 응용 프로그램에 대 한 걸릴 수 있습니다. 처음 실행할 때 응용 프로그램 ACS50001 오류가 나타나면: '[realm]' 이름 가진 신뢰 당사자를 찾을 수 없습니다, 다음 몇 분 정도 기다렸다가 및 응용 프로그램을 다시 실행 하십시오.
9. 메시지가 표시 되 면 디렉터리에 사용자로 로그온 합니다.

    ![](windows-azure-authentication/_static/image8.jpg)
10. Azure에 성공적으로 로그인 한 이제 Windows Azure 인증을 사용 하 여 응용 프로그램을 호스트 합니다.  
  
     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>알려진 문제

#### <a name="role-based-authorization-fails-when-using-windows-azure-authenticationopop"></a>역할 기반 권한 부여 실패 < 된 >< Windows Azure 인증을 사용 하는 경우 / 된 >

역할 기반 권한 부여를 수행할 수 있도록 Windows Azure 인증 필요한 역할 클레임을 현재 제공 하지 않습니다. Windows Azure Active Directory에서 < 된 >< 수동으로 검색 해야 하는 인증 된 사용자의 역할 / 된 >

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-stsopop"></a>오류에 대 한 Windows Azure 인증 결과가 포함 된 응용 프로그램에 검색 "ACS20016 도메인 로그인된 한 사용자 (live.com)의 모든 일치 하지 않습니다. 허용이 도메인 STS" < 된 >< / 된 >

Microsoft 계정 (예: hotmail.com, live.com, outlook.com)에 이미 로그인 한 Windows Azure 인증 사용 하도록 설정한 응용 프로그램에 액세스 하려고 하면 발생할 수 있습니다 400 오류 응답을 하기 때문에 Microsoft 계정 도메인 Windows Azure Active Directory에서 인식 되지 않습니다. 가 응용 프로그램에 로그인, 로그 아웃 Microsoft 계정에서 먼저. < 된 >< / 된 >

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificateopop"></a>이외의 다른 Windows Azure 인증을 사용할 수 있는 응용 프로그램 및 한 X509CertificateValidationMode에 로그인 없음 < 된 >< accounts.accesscontrol.windows.net 인증서에 대 한 인증서 유효성 검사 오류를 발생 / 된 >

인증서 유효성 검사 필요 하지 않으며 해제 해야 합니다. 발급자 인증서의 지문을 WSFederationAuthenticationModule. < 된 ><에서 유효성을 검사 / 된 >

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-stsopop"></a>웹 인증 대화 상자에 오류 표시 Windows Azure 인증을 사용 하려고 할 때 "ACS20016: 로그인된 한 사용자 (contoso.onmicrosoft.com)의 도메인이이 STS의 허용 되는 도메인과 일치 하지 않습니다." < 된 >< / 된 >

이전에 성공적으로 로그인 하면 동일한 Visual Studio 프로세스에서 서로 다른 Windows Azure Active Directory 계정을 사용 하 여이 오류가 나타날 수 있습니다. 지정한 계정에서 로그 아웃 하거나 Visual Studio를 다시 시작 합니다. 이전에 로그인 하 고 "로그인 상태 유지" 하는 옵션을 선택한 다음 선택을 취소 하면 브라우저 쿠키 합니다. < 된 >< 해야 할 수 / 된 >

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message-opop"></a>ACS20012: 요청이 않습니다. 유효한 Ws-federation 프로토콜 메시지 < 된 >< / 된 >

Azure 서비스 중 하나를 다른 Microsoft ID를 이미 로그인 하는 경우 발생할 수 있습니다. 사용 하 여 개인 브라우저 창을 IE에서 InPrivate 또는 Incognito 크롬에서 선택 하거나 모든 쿠키를 취소 합니다. < 된 >< / 된 >

## <a name="additional-resources"></a>추가 리소스

- [Microsoft ASP.NET Windows 용 도구 Visual Studio 2012 Azure Active Directory –](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci
- [Windows Azure 기능: Identity](https://docs.microsoft.com/azure/active-directory/)
- [TechNet: Windows Azure Active Directory](https://technet.microsoft.com/en-us/library/hh967619.aspx)
- [Windows Azure Active Directory: 조직에 대 한 앱을 개발 합니다.](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory: 여러 조직에 대 한 앱을 개발 합니다.](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [Single sign on Windows Azure Active Directory와 구현 하는 방법](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [Single Sign-on windows Azure Active Directory: 심층](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci
- [구현 및 관리를 사용 하 여 AD FS 2.0 single sign on](https://technet.microsoft.com/en-us/library/jj205462.aspx)
