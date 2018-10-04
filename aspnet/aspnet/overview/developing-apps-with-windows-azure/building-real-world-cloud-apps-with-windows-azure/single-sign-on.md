---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Single Sign-on (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 22ef4c2908783e513bfb6fb63364e71378cb8719
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48578434"
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>Single sign On (실제 클라우드 앱 빌드 Azure 사용 하 여)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


클라우드 앱을 개발 하는 경우 고려해 야 하는 많은 보안 문제가 있지만이 시리즈에 대 한 집중 하나만: single sign on입니다. 이 질문 사람들이 종종 질문: "주로 작성 앱 내 회사의 직원 어떻게 이러한 클라우드 앱을 호스트 하 고 계속 사용 하는 내 직원 인지 알고 있어야 하 고 앱을 실행 중인 경우 온-프레미스 환경에서 사용 하는 동일한 보안 모델을 사용 하는 방화벽 내에서 호스팅되 "? 이 시나리오 사용 하도록 설정 하는 방법 중 하나를 Azure Active Directory (Azure AD) 라고 합니다. Azure AD를 사용 하면 엔터프라이즈 기간 업무 (LOB) 응용 프로그램이 사용할 수 있도록 인터넷을 통해 및도 비즈니스 파트너에 게 이러한 앱을 제공 하는 수 있습니다.

## <a name="introduction-to-azure-ad"></a>Azure AD 소개

[Azure AD](https://docs.microsoft.com/azure/active-directory/) 제공 [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 클라우드에서 합니다. 주요 기능은 다음과 같습니다.

- 온-프레미스 Active Directory와 통합 됩니다.
- 앱에서 single sign-on 수 있습니다.
- 와 같은 개방형 표준을 지 원하는 [SAML](http://en.wikipedia.org/wiki/SAML_2.0)를 [Ws-fed](http://en.wikipedia.org/wiki/WS-Federation), 및 [OAuth 2.0](http://oauth.net/2/)합니다.
- 엔터프라이즈 지원 [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)합니다.

인트라넷 응용 프로그램에 로그인 하는 직원을 사용 하도록 설정 하는 데 사용 하는 온-프레미스 Windows Server Active Directory 환경에 있다고 가정 합니다.

![](single-sign-on/_static/image1.png)

새로운 Azure AD 수행할 수 있도록 클라우드에서 디렉터리를 만드는 것입니다. 사용 가능한 기능 및 쉽게 설정할 수 있습니다.

온-프레미스 Active Directory;에서 완전히 독립 될 수 있습니다. 원하는 누구나 인터넷 앱에서 인증을 넣을 수 있습니다.

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

온-프레미스를 사용 하 여 통합할 수 있습니다 또는 AD입니다.

![AD 및 WAAD 통합](single-sign-on/_static/image3.png)

이제 온-프레미스를 인증할 수 있는 모든 직원을 방화벽을 열 또는 데이터 센터에 새 서버를 배포 하지 않고도 – 인터넷을 통해도 인증할 수 있습니다. 알고 있고 지금를 사용 하 여 기능에서 내부 앱 단일-로그인을 제공 하는 모든 기존 Active Directory 환경을 활용 하 여 계속할 수 있습니다.

AD와 Azure AD 간의이 연결에 대 한 웹 앱 및 모바일 장치를 클라우드에서 직원을 인증도 설정할 수 있습니다 하 고 수락 하도록 Office 365, SalesForce.com, 또는 Google 앱과 같은 타사 앱을 설정할 수 있습니다. 프로그램 직원의 자격 증명입니다. Office 365를 사용 하는 경우 이미 설정한 Azure AD를 사용 하 여 Office 365 인증 및 권한 부여에 대 한 Azure AD를 사용 하기 때문에 있습니다.

![타사 앱](single-sign-on/_static/image4.png)

이 방식의 장점은 언제 든 지 조직의 추가 하거나 사용자를 삭제 합니다. 또는 사용자는 암호 변경, 온-프레미스 환경에서 현재 사용 하는 동일한 프로세스를 사용 합니다. 모든 온-프레미스의 AD 변경 내용을 자동으로 전파 되는 클라우드 환경입니다.

회사를 사용 하거나 좋은 소식은 Office 365로 이동 하는 경우에 Azure AD를 Office 365 인증에 대 한 Azure AD를 사용 하기 때문에 자동으로 설정 해야 합니다. 사용할 수 있도록 쉽게 사용자 고유의 앱에서 Office 365를 사용 하는 동일한 인증 합니다.

## <a name="set-up-an-azure-ad-tenant"></a>Azure AD 테 넌 트 설정

Azure AD 디렉터리를 Azure ad 라고 [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)를 상당히 쉽습니다 테 넌 트를 설정 합니다. 보여드리겠습니다 개념을 설명 하기 위해 Azure 관리 포털에서 수행 방법 이지만 물론 다른 포털 함수 같은 가능 스크립트 또는 관리 API 사용 하 여 합니다.

관리 포털에서 Active Directory 탭을 클릭 합니다.

![포털에서 WAAD](single-sign-on/_static/image5.png)

Azure 계정에 대 한 Azure AD 테 넌 트를 자동으로 가집니다 및 클릭할 수는 **추가** 추가 디렉터리를 만들려면 페이지의 맨 위에 있는 단추입니다. 테스트 환경 및 프로덕션 환경에 대 한 예를 들어. 새 디렉터리 이름에 대 한 지 신중히 생각해 야 합니다. 디렉터리 이름을 사용 하 고 혼동을 줄 수 있는 사용자 중 하나에 대해 다시 사용자 이름을 사용 합니다.

![디렉터리 추가](single-sign-on/_static/image6.png)

포털에는 만들기, 삭제 및이 환경 내에서 사용자 관리에 대 한 완벽 하 게 지원 합니다. 예를 들어, 추가 사용자로 이동 합니다 **사용자** 탭을 클릭 합니다 **사용자 추가** 단추입니다.

![사용자 추가 단추](single-sign-on/_static/image7.png)

![사용자 대화 상자를 추가 합니다.](single-sign-on/_static/image8.png)

이 디렉터리에만 존재 하는 새 사용자를 만들 수 있습니다 또는이 디렉터리에 사용자로이 디렉터리에 등록 된 사용자 또는 다른 Azure AD 디렉터리에서 사용자는 Microsoft 계정을 등록할 수 있습니다. (실제 디렉터리에 기본 도메인은 ContosoTest.onmicrosoft.com입니다. 사용할 수도 있습니다 도메인에 contoso.com과 같은 고유한 선택.)

![사용자 형식](single-sign-on/_static/image9.png)

![사용자 대화 상자를 추가 합니다.](single-sign-on/_static/image10.png)

역할에 사용자를 할당할 수 있습니다.

![사용자 프로필](single-sign-on/_static/image11.png)

및 계정의 임시 암호를 사용 하 여 만들어집니다.

![임시 암호](single-sign-on/_static/image12.png)

이러한 방식으로 만든 사용자 수 즉시이 클라우드 디렉터리를 사용 하 여 웹 앱에 로그인 합니다.

그러나 enterprise single sign-on에 대 한 훌륭한 점은입니다 합니다 **디렉터리 통합** 탭:

![디렉터리 통합 탭](single-sign-on/_static/image13.png)

디렉터리 통합을 사용 하는 경우 및 [도구를 다운로드](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), 조직 내에서 이미 사용 중인 기존 온-프레미스 Active Directory를 사용 하 여이 클라우드 디렉터리를 동기화 할 수 있습니다. 그런 다음 모든 디렉터리에 저장 된 사용자가 표시 됩니다이 클라우드 디렉터리에서. 클라우드 앱에 기존 Active Directory 자격 증명을 사용 하 여 직원의 모든 인증 수 있습니다. 이 모든 free-Azure AD 자체와 동기화 도구를

이 도구는 이러한 스크린샷은에서 알 수 있듯이 편리 하 게 사용할 있는 마법사. 이들은 지침은 기본 프로세스를 보여 주는 예로 든 것일 뿐입니다. 자세한 내용을 보려면 방법-을 수행-it, 링크를 참조 합니다 [리소스](#resources) 장의 끝에 있는 섹션입니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image14.png)

클릭 **다음**를 선택한 다음 Azure Active Directory 자격 증명을 입력 합니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image15.png)

클릭 **다음**, 온-프레미스를 입력 한 다음 AD 자격 증명입니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image16.png)

클릭 **다음**, 그런 다음 클라우드에서 AD 암호의 해시를 저장 하려는 경우를 나타냅니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image17.png)

클라우드에 저장할 수 있는 암호 해시는 단방향 해시입니다. 실제 암호는 Azure AD에 저장 되지 않습니다. 사용 해야 해시를 클라우드에 저장 하는 것에 대 한 않으려면 [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS). 이 밖에도 [때 고려해 야 할 요인 ADFS를 사용할 것인지 선택](https://technet.microsoft.com/library/jj573653.aspx). ADFS 옵션에는 몇 가지 추가 구성 단계가 필요합니다.

클라우드에서 해시를 저장 하도록 선택 하면, 완료 및 도구를 클릭 하면 디렉터리 동기화를 시작 하는 경우 **다음**합니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image18.png)

고 잠시 후에 완료 합니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image19.png)

Windows 2003 이상 조직에서 하나의 도메인 컨트롤러에서이 실행 해야 합니다. 및 다시 부팅 하지 않아도 됩니다. 완료 하 고 모든 사용자는 클라우드에서 수행할 수 있습니다 하는 경우 웹 또는 SAML, OAuth 또는 Ws-fed를 사용 하 여 모바일 응용 프로그램에서 single sign-on입니다.

이것이 얼마나 안전에 대 한 질문 가져올 경우에 따라 – Microsoft 사용지 않습니다 자신의 중요 한 비즈니스 데이터에 대 한? 및 그렇다고 작업을 수행 합니다. 예를 들어에서 내부 Microsoft SharePoint 사이트로 이동 [ https://microsoft.sharepoint.com/ ](https://microsoft.sharepoint.com/), 로그인 하 라는 메시지가 표시 됩니다.

![Office 365 로그인](single-sign-on/_static/image20.png)

Microsoft가 ADFS를 사용 하도록 설정 되므로 Microsoft ID를 입력 하면 ADFS 로그인 페이지로 리디렉션됩니다.

![ADFS 로그인](single-sign-on/_static/image21.png)

및이 내부 응용 프로그램에 액세스할 수 있는 내부 Microsoft AD 계정에 저장 된 자격 증명을 입력 하면 됩니다.

![MS SharePoint 사이트](single-sign-on/_static/image22.png)

에서는 이미 Azure AD가 사용할 수 있지만 로그인 프로세스를 클라우드에서 Azure AD 디렉터리를 통해 송신 하기 전에를 설정 하는 ADFS 때문에 주로 AD 로그인 서버를 사용 하는 것입니다. 중요 한 문서, 소스 제어, 성능 관리 파일, 판매 보고서 및 클라우드에서 더 많은 저장 하 고 보안을 유지 하는 데이 정확히 동일한 솔루션을 사용 하는 합니다.

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>Single sign on에 대 한 Azure AD를 사용 하는 ASP.NET 앱 만들기

Visual Studio에서는 몇 가지 스크린 샷을에서 알 수 있듯이 Azure AD single sign-on을 사용 하는 앱을 만드는 데 매우 쉽습니다.

새 ASP.NET 응용 프로그램, MVC 또는 Web Forms를 만들 때 기본 인증 방법은 ASP.NET Id입니다. 클릭 하면 Azure AD를 변경 하는 **인증 변경** 단추입니다.

![인증 변경](single-sign-on/_static/image23.png)

조직 계정 선택, 사용자가 도메인 이름을 입력 하 고 Single Sign On 선택 합니다.

![인증 대화 상자를 구성 합니다.](single-sign-on/_static/image24.png)

앱 읽기를 제공 하거나 수도 디렉터리 데이터에 대 한 권한이 읽기/쓰기입니다. 이렇게 하면 사용할 수는 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) 사용자의 전화 번호를 검색할 알아보십시오 경우 사무실에 마지막으로, 등를 기록 하는 경우.

수행 해야 하는 모든 Visual Studio는 자격 증명을 요청에 Azure AD 테 넌 트의 관리자에 대 한 한 다음 프로젝트와 새 응용 프로그램에 대 한 Azure AD 테 넌 구성 합니다.

프로젝트를 실행 하면 로그인 페이지가 표시 됩니다 및 Azure AD 디렉터리에서 사용자의 자격 증명을 로그인 할 수 있습니다.

![조직 계정 로그인](single-sign-on/_static/image25.png)

![로그인](single-sign-on/_static/image26.png)

Azure에 앱을 배포할 때 수행 해야 하는 모든가 선택는 **조직 인증 사용** 확인란을 선택한 Visual Studio를 모든 구성의 이번 담당 합니다.

![웹 게시](single-sign-on/_static/image27.png)

Azure AD 인증을 사용 하는 앱을 빌드하는 방법을 보여 주는 전체 단계별 자습서에서 제공 되는 이러한 스크린 샷: [Azure Active Directory를 사용 하 여 ASP.NET 앱 개발](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)합니다.

## <a name="summary"></a>요약

이 장에서 Azure Active Directory, Visual Studio 및 ASP.NET을 쉽게 조직의 사용자에 대 한 인터넷 응용 프로그램에서 single sign-on을 설정 하는 것이 살펴보았습니다. 사용자가 Active Directory를 사용 하 여 내부 네트워크에 로그온 하는를 사용 하 여 동일한 자격 증명을 사용 하 여 인터넷 응용 프로그램에 로그온 할 수 있습니다.

합니다 [다음 장에서](data-storage-options.md) 클라우드 앱에 사용할 수 있는 데이터 저장소 옵션을 살펴봅니다.

<a id="resources"></a>
## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조하세요.

- [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다. Windowsazure.com 사이트의 Azure AD 설명서에 대 한 포털 페이지입니다. 단계별 자습서에 대 한 참조를 **개발** 섹션입니다.
- [Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)합니다. Azure에서 multi-factor authentication에 대 한 설명서 포털 페이지입니다.
- [조직 계정 인증 옵션](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)합니다. Visual Studio 2013 새 프로젝트 대화 상자에서 Azure AD 인증 옵션에 설명 합니다.
- [Microsoft Patterns and Practices-페더레이션 Id 패턴](https://msdn.microsoft.com/library/dn589790.aspx)합니다.
- [방법: Azure Active Directory Sync 도구를 설치 하](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)합니다.
- [Active Directory Federation Services 2.0 콘텐츠 맵](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)합니다. ADFS 2.0에 대 한 설명서 링크를 제공 합니다.
- [Windows Azure AD 응용 프로그램에서 역할 기반 및 ACL 기반 권한 부여](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)합니다. 샘플 응용 프로그램입니다.
- [Azure Active Directory Graph API 블로그](https://blogs.msdn.com/b/aadgraphteam/)합니다.
- [Access Control에서 BYOD 및 하이브리드 Id 인프라의 디렉터리 통합](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)합니다. Tech Ed 2014 세션 비디오 Gayana Bagdasaryan 합니다.

> [!div class="step-by-step"]
> [이전](web-development-best-practices.md)
> [다음](data-storage-options.md)
