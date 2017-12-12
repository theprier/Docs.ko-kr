---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: "Single Sign-on (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs"
author: MikeWasson
description: "실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: f0d465b363652c691c203d608f2cb9d139e72fed
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>Single Sign-on (Azure로 응용 프로그램 빌딩 실제 클라우드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


클라우드 앱을 개발 하는 경우에 대해 생각 하는 많은 보안 문제가 있습니다 하지만이 계열에 대해 집중적으로 살펴봅니다 하나만: 단일 로그온 합니다. 질문 사람 자주 하는 질문 이것이: "주로 제가 앱; 회사 직원에 대 한 어떻게 이러한 앱은 클라우드에서 호스트 하 고 여전히 내 직원 알고 있고 앱을 실행 하는 경우 온-프레미스 환경에서 사용 하는 동일한 보안 모델을 사용 하도록 할 호스트 되는 방화벽 내 "? 이 시나리오 사용 하도록 설정 하는 방법 중 하나를 Azure Active Directory (Azure AD) 라고 합니다. Azure AD를 사용 하면 엔터프라이즈 기간 업무 (LOB) 응용 프로그램에서 사용할 수 있도록 인터넷을 통해 하 고도 비즈니스 파트너에 게 이러한 앱을 사용할 수 있도록 할 수 있습니다.

## <a name="introduction-to-azure-ad"></a>Azure AD 소개

[Azure AD](https://docs.microsoft.com/azure/active-directory/) 제공 [Active Directory](https://msdn.microsoft.com/en-us/library/windows/desktop/aa746492.aspx) 클라우드에 있습니다. 주요 기능은 다음과 같습니다.

- 온-프레미스 Active Directory와 통합합니다.
- Single sign on 여 응용 프로그램과 함께 수 있습니다.
- 와 같은 공개 표준을 지원 [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [Ws-fed](http://en.wikipedia.org/wiki/WS-Federation), 및 [OAuth 2.0](http://oauth.net/2/)합니다.
- 엔터프라이즈 지원 [Graph REST API](https://msdn.microsoft.com/en-us/library/hh974476.aspx)합니다.

인트라넷 응용 프로그램에 로그온 하는 직원을 사용 하도록 설정 하는 데 사용 하는 온-프레미스 Windows Server Active Directory 환경에 있다고 가정 합니다.

![](single-sign-on/_static/image1.png)

Azure AD 덕분에 작업을 수행할 수는 클라우드에서 디렉터리를 만듭니다. 사용 가능한 기능 및 쉽게 설정할 수 있습니다.

온-프레미스 Active Directory;에서 완전히 독립적일 수 있습니다. 에 원하는 누구나 인터넷 응용 프로그램에서 인증에 넣을 수 있습니다.

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

온-프레미스를 통합할 수 있습니다 또는 AD 합니다.

![AD 및 WAAD 통합](single-sign-on/_static/image3.png)

이제 온-프레미스를 인증할 수 있는 모든 직원을 방화벽을 열거나 데이터 센터에 모든 새 서버를 배포할 필요 없이-인터넷을 통해도 인증할 수 있습니다. 알고 있고 오늘날 제공 하기 위해 사용할에 내부 앱의 단일 로그온 기능에 있는 모든 기존 Active Directory 환경을 활용 하 여 계속할 수 있습니다.

AD와 Azure AD 간의이 연결 했습니다. 웹 앱 및 모바일 장치는 클라우드에서 직원을 인증 하는 할 수도 있습니다 하 고 수락 하도록 Office 365, SalesForce.com, 또는 Google 앱 등의 타사 앱을 활성화할 수 있습니다 프로그램 직원의 자격 증명입니다. Office 365를 사용 하는 경우 이미 설정한 Azure AD와 Office 365 인증 및 권한 부여에 대 한 Azure AD를 사용 하기 때문에 있습니다.

![타사 앱](single-sign-on/_static/image4.png)

이 방식의 장점은 언제 든 지 조직 추가 하거나, 사용자를 삭제 하는 암호 변경 또는 온-프레미스 환경에서 현재 사용 하는 과정과 동일를 사용 합니다. 모든 온-프레미스의 AD 변경 내용을 자동으로 전파 됩니다 클라우드 환경입니다.

회사는 사용 또는 다행 스럽게도 하는 Office 365로 이동 하는 경우 Azure AD를 Office 365 인증에 대 한 Azure AD를 사용 하기 때문에 자동으로 설정 해야 합니다. 사용할 수 있도록 쉽게 응용 프로그램에 Office 365를 사용 하는 동일한 인증 합니다.

## <a name="set-up-an-azure-ad-tenant"></a>Azure AD 테 넌 트 설정

Azure AD에서 Azure AD 디렉터리 라고 [테 넌 트](https://technet.microsoft.com/en-us/library/jj573650.aspx), 매우 쉽습니다 테 넌 트를 설정 하 고 있습니다. 개념을 설명 하기 위해 Azure 관리 포털에서 수행 방법을 보여 드리 려 우리 없지만 물론 다른 포털 함수 처럼 수 있습니다도 것 스크립트 또는 관리 API 사용 하 여 합니다.

관리 포털에서 Active Directory 탭을 클릭 합니다.

![포털에서 WAAD](single-sign-on/_static/image5.png)

Azure 계정에 대 한 Azure AD 테 넌 트를 자동으로 부여 되며을 클릭할 수는 **추가** 추가 디렉터리를 만드는 페이지의 맨 아래에 있는 단추입니다. 예를 들어 테스트 환경용 하나가 환경과 프로덕션 환경이을 할 수 있습니다. 새 디렉터리 이름에 대 한 신중 하 게 생각 합니다. 디렉터리에 대 한 사용자 이름을 사용 하 고 혼동 될 수 있는 사용자 중 하나에 다시 사용자 이름을 사용 합니다.

![디렉터리 추가](single-sign-on/_static/image6.png)

포털은 생성, 삭제 및이 환경 내의 사용자 관리에 대 한 전체를 지원 합니다. 예를 들어 추가 하려면 사용자로 이동 된 **사용자** 탭을 클릭는 **사용자 추가** 단추입니다.

![사용자 추가 단추](single-sign-on/_static/image7.png)

![추가 사용자 대화 상자](single-sign-on/_static/image8.png)

이 디렉터리에만 존재 하는 새 사용자 만들거나이 디렉터리에 사용자로이 디렉터리 또는 레지스터의 사용자 또는 다른 Azure AD 디렉터리에서 사용자는 Microsoft 계정을 등록할 수 있습니다. (실제 디렉터리는 기본 도메인 일 ContosoTest.onmicrosoft.com 합니다. 사용할 수도 있습니다 contoso.com 처럼 사용자가 선택한의 도메인입니다.)

![사용자 유형](single-sign-on/_static/image9.png)

![추가 사용자 대화 상자](single-sign-on/_static/image10.png)

사용자 역할에 할당할 수 있습니다.

![사용자 프로필](single-sign-on/_static/image11.png)

및 임시 암호 계정이 만들어집니다.

![임시 암호](single-sign-on/_static/image12.png)

이런 방식이으로 만들 사용자 수 즉시이 클라우드 디렉터리를 사용 하 여 웹 앱에 로그인 합니다.

그러나 enterprise single sign-on에 대 한 좋은 것은 **디렉터리 통합** 탭:

![디렉터리 통합 탭](single-sign-on/_static/image13.png)

디렉터리 통합을 사용 하는 경우 및 [도구 다운로드 하 여](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), 조직 내에 이미 사용 중인 기존 온-프레미스 Active Directory와 클라우드 디렉터리를 동기화 할 수 있습니다. 다음 디렉터리에 저장 된 사용자 모두에 표시 됩니다이 클라우드 디렉터리입니다. 이제 클라우드 앱에서 모든 기존 Active Directory 자격 증명을 사용 하 여 직원 들을 인증할 수 있습니다. 및이 모든 가능한 – 자체 Azure AD와 동기화 도구입니다.

이 도구는는 된 마법사를 사용 하기 쉬운 이러한 스크린샷은에서 볼 수 있습니다. 이들은 자세한 지침은, 단지 기본 프로세스를 보여 주는 예입니다. 자세한 내용은 방법-하려는 do-it의 링크를 참조는 [리소스](#resources) 장의 마지막 부분에 있습니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image14.png)

클릭 **다음**, 한 다음 Azure Active Directory 자격 증명을 입력 합니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image15.png)

클릭 **다음**, 온-프레미스를 입력 한 다음 AD 자격 증명입니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image16.png)

클릭 **다음**, 클라우드에서 AD 암호의 해시를 저장 하려는 경우를 나타내는입니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image17.png)

클라우드에 저장할 수 있는 암호 해시는 단방향 해시; 실제 암호는 Azure AD에 저장 되지 않습니다. 사용 해야 클라우드에서 강력한 해시에 대해 결정 한 경우 [Active Directory Federation Services](https://technet.microsoft.com/en-us/library/hh831502.aspx) (ADFS). 또한 [경우 고려해 야 할 기타 요인 ADFS 사용 여부를 선택](https://technet.microsoft.com/en-us/library/jj573653.aspx)합니다. ADFS 옵션에는 몇 가지 추가 구성 단계가 필요합니다.

클라우드에서 해시를 저장 하도록 선택 하면, 삭제 하 고 나면를 클릭할 때 디렉터리 동기화 도구가 시작 경우 **다음**합니다.

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image18.png)

잠시 후에 완료 되 고

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image19.png)

Windows 2003 이상, 조직에서 하나의 도메인 컨트롤러에서 실행 해야 합니다. 및를 재부팅 해야 합니다. 완료 되는 모든 사용자에 게 클라우드에 하 고 할 수 있는 모든 웹 또는 SAML, OAuth, 또는 Ws-fed를 사용 하 여 모바일 응용 프로그램에 single sign-on입니다.

이 보안에 대 한 요청한 가져올 경우에 따라 – Microsoft 사용지 않습니다 자신의 중요 한 비즈니스 데이터에 대 한? 및 그렇다고 수행 하는 것입니다. 에 내부 Microsoft SharePoint 사이트로 이동 하는 경우 등 [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), 로그인 하 라는 메시지가 가져옵니다.

![Office 365 로그인](single-sign-on/_static/image20.png)

Microsoft ADFS를 사용 하도록 설정한 하므로 Microsoft ID를 입력 하면 ad FS 로그인 페이지로 리디렉션됩니다.

![Ad FS 로그인](single-sign-on/_static/image21.png)

하며이 내부 응용 프로그램에 대 한 액세스는 내부 Microsoft AD 계정에 저장 된 자격 증명을 입력 해야 합니다.

![MS SharePoint 사이트](single-sign-on/_static/image22.png)

이미 Azure AD를 사용할 수 있게 하지만 로그인 프로세스를 클라우드에서 Azure AD 디렉터리를 통해 송신 하기 전에를 설정 하는 ADFS 해야 하기 때문에 주로 AD 로그인에 서버를 사용 합니다. 중요 한 문서, 소스 제어, 성능 관리 파일, 판매 보고서, 및 기타를 클라우드에 저장 하 고 보안을 설정 하려면이 정확히 동일한 솔루션을 사용 하는 합니다.

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>Single sign on에 대 한 Azure AD를 사용 하 여 ASP.NET 응용 프로그램 만들기

Visual Studio에서는 몇 가지 스크린 샷에서 볼 수 있듯이 single sign-on 용 Azure AD를 사용 하는 앱을 만드는 데 매우 쉽습니다.

새 ASP.NET 응용 프로그램, MVC 또는 Web Forms를 만들 때 기본 인증 방법은 ASP.NET Identity를입니다. Azure AD에는 변경 하려면는 **인증 변경** 단추입니다.

![인증 변경](single-sign-on/_static/image23.png)

조직 계정, 선택한 도메인 이름을 입력 Single Sign On 다음 선택 합니다.

![인증 대화 상자를 구성 합니다.](single-sign-on/_static/image24.png)

응용 프로그램 읽기를 제공 하거나 수도 디렉터리 데이터에 대 한 권한이 읽기/쓰기입니다. 이렇게 하면 사용할 수는 [Azure Graph REST API](https://msdn.microsoft.com/en-us/library/windowsazure/hh974476.aspx) 사용자의 전화 번호를 조회할 확인 하는 경우 변경 내용은 하면 사무실에 마지막 등으로 기록 합니다.

-할 모든 Visual Studio 자격 증명에 대 한 Azure AD 테 넌 트의 관리자에 대 한 문의 한 다음 새 응용 프로그램에 대 한 Azure AD 테 넌 트와 프로젝트를 구성 합니다.

프로젝트를 실행 하는 경우 로그인 페이지를 확인 하 고 Azure AD 디렉터리에서 사용자의 자격 증명을 로그인 할 수 있습니다.

![조직 계정 로그인](single-sign-on/_static/image25.png)

![로그인](single-sign-on/_static/image26.png)

선택은 Azure에 응용 프로그램을 배포할 때만 하면는 **조직 인증을 사용 하도록 설정** 확인란을 선택한 사용자에 대 한 모든 구성은 Visual Studio 다시 한 번 담당 합니다.

![웹 게시](single-sign-on/_static/image27.png)

이러한 스크린샷은 Azure AD 인증을 사용 하는 응용 프로그램을 빌드하는 방법을 보여 주는 전체 단계별 자습서에서 제공: [Azure Active Directory와 ASP.NET 응용 프로그램 개발](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)합니다.

## <a name="summary"></a>요약

이 장에서 Azure Active Directory, Visual Studio 및 ASP.NET을 쉽게에서 조직의 사용자에 대 한 인터넷 응용 프로그램에 single sign-on을 설정 하는 것이 살펴보았습니다. Active Directory를 사용 하 여 내부 네트워크에 로그온 하는 데 사용 하는 동일한 자격 증명을 사용 하 여 인터넷 응용 프로그램에서 사용자가 로그온 할 수 있습니다.

[다음 장에서](data-storage-options.md) 클라우드 앱에 사용할 수 있는 데이터 저장소 옵션을 살펴봅니다.

<a id="resources"></a>
## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조하세요.

- [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다. Windowsazure.com 사이트에서 Azure AD 설명서에 대 한 포털 페이지입니다. 단계별 자습서에 대 한 참조는 **개발** 섹션.
- [Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)합니다. Azure에서 다단계 인증에 대 한 설명서 포털 페이지입니다.
- [조직 계정 인증 옵션](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)합니다. Visual Studio 2013 새 프로젝트 대화 상자에서 Azure AD 인증 옵션을 설명 합니다.
- [Microsoft Patterns and Practices-Federated Identity 패턴](https://msdn.microsoft.com/en-us/library/dn589790.aspx)합니다.
- [방법: Azure Active Directory 동기화 도구 설치](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)합니다.
- [Active Directory Federation Services 2.0 콘텐츠 맵](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)합니다. ADFS 2.0에 대 한 설명서 링크를 제공 합니다.
- [Windows Azure AD 응용 프로그램에서 역할 기준 및 ACL 기반 권한 부여](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)합니다. 샘플 응용 프로그램입니다.
- [Azure Active Directory Graph API 블로그](https://blogs.msdn.com/b/aadgraphteam/)합니다.
- [액세스 제어에서 BYOD 및 하이브리드 Id 인프라의 디렉터리 통합](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)합니다. 기술 Ed 2014 세션 비디오 Gayana Bagdasaryan 여입니다.

>[!div class="step-by-step"]
[이전](web-development-best-practices.md)
[다음](data-storage-options.md)
