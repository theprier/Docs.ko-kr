---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Single Sign-on (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 82f2f99154d94074b03d580a0f491053d6f53bde
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="c958c-104">Single Sign-on (Azure로 응용 프로그램 빌딩 실제 클라우드)</span><span class="sxs-lookup"><span data-stu-id="c958c-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="c958c-105">여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c958c-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="c958c-106">[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="c958c-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="c958c-107">**실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="c958c-108">13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="c958c-109">전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="c958c-110">클라우드 앱을 개발 하는 경우에 대해 생각 하는 많은 보안 문제가 있습니다 하지만이 계열에 대해 집중적으로 살펴봅니다 하나만: 단일 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="c958c-111">질문 사람 자주 하는 질문 이것이: "주로 제가 앱; 회사 직원에 대 한 어떻게 이러한 앱은 클라우드에서 호스트 하 고 여전히 내 직원 알고 있고 앱을 실행 하는 경우 온-프레미스 환경에서 사용 하는 동일한 보안 모델을 사용 하도록 할 호스트 되는 방화벽 내 "?</span><span class="sxs-lookup"><span data-stu-id="c958c-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="c958c-112">이 시나리오 사용 하도록 설정 하는 방법 중 하나를 Azure Active Directory (Azure AD) 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c958c-113">Azure AD를 사용 하면 엔터프라이즈 기간 업무 (LOB) 응용 프로그램에서 사용할 수 있도록 인터넷을 통해 하 고도 비즈니스 파트너에 게 이러한 앱을 사용할 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="c958c-114">Azure AD 소개</span><span class="sxs-lookup"><span data-stu-id="c958c-114">Introduction to Azure AD</span></span>

<span data-ttu-id="c958c-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) 제공 [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 클라우드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="c958c-116">주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-116">Key features include the following:</span></span>

- <span data-ttu-id="c958c-117">온-프레미스 Active Directory와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="c958c-118">Single sign on 여 응용 프로그램과 함께 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="c958c-119">와 같은 공개 표준을 지원 [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [Ws-fed](http://en.wikipedia.org/wiki/WS-Federation), 및 [OAuth 2.0](http://oauth.net/2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="c958c-120">엔터프라이즈 지원 [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="c958c-121">인트라넷 응용 프로그램에 로그온 하는 직원을 사용 하도록 설정 하는 데 사용 하는 온-프레미스 Windows Server Active Directory 환경에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="c958c-122">Azure AD 덕분에 작업을 수행할 수는 클라우드에서 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="c958c-123">사용 가능한 기능 및 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="c958c-124">온-프레미스 Active Directory;에서 완전히 독립적일 수 있습니다. 에 원하는 누구나 인터넷 응용 프로그램에서 인증에 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="c958c-126">온-프레미스를 통합할 수 있습니다 또는 AD 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-126">Or you can integrate it with your on-premises AD.</span></span>

![AD 및 WAAD 통합](single-sign-on/_static/image3.png)

<span data-ttu-id="c958c-128">이제 온-프레미스를 인증할 수 있는 모든 직원을 방화벽을 열거나 데이터 센터에 모든 새 서버를 배포할 필요 없이-인터넷을 통해도 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="c958c-129">알고 있고 오늘날 제공 하기 위해 사용할에 내부 앱의 단일 로그온 기능에 있는 모든 기존 Active Directory 환경을 활용 하 여 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="c958c-130">AD와 Azure AD 간의이 연결 했습니다. 웹 앱 및 모바일 장치는 클라우드에서 직원을 인증 하는 할 수도 있습니다 하 고 수락 하도록 Office 365, SalesForce.com, 또는 Google 앱 등의 타사 앱을 활성화할 수 있습니다 프로그램 직원의 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="c958c-131">Office 365를 사용 하는 경우 이미 설정한 Azure AD와 Office 365 인증 및 권한 부여에 대 한 Azure AD를 사용 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![타사 앱](single-sign-on/_static/image4.png)

<span data-ttu-id="c958c-133">이 방식의 장점은 언제 든 지 조직 추가 하거나, 사용자를 삭제 하는 암호 변경 또는 온-프레미스 환경에서 현재 사용 하는 과정과 동일를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="c958c-134">모든 온-프레미스의 AD 변경 내용을 자동으로 전파 됩니다 클라우드 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="c958c-135">회사는 사용 또는 다행 스럽게도 하는 Office 365로 이동 하는 경우 Azure AD를 Office 365 인증에 대 한 Azure AD를 사용 하기 때문에 자동으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="c958c-136">사용할 수 있도록 쉽게 응용 프로그램에 Office 365를 사용 하는 동일한 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="c958c-137">Azure AD 테 넌 트 설정</span><span class="sxs-lookup"><span data-stu-id="c958c-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="c958c-138">Azure AD에서 Azure AD 디렉터리 라고 [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx), 매우 쉽습니다 테 넌 트를 설정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="c958c-139">개념을 설명 하기 위해 Azure 관리 포털에서 수행 방법을 보여 드리 려 우리 없지만 물론 다른 포털 함수 처럼 수 있습니다도 것 스크립트 또는 관리 API 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="c958c-140">관리 포털에서 Active Directory 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-140">In the management portal click the Active Directory tab.</span></span>

![포털에서 WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="c958c-142">Azure 계정에 대 한 Azure AD 테 넌 트를 자동으로 부여 되며을 클릭할 수는 **추가** 추가 디렉터리를 만드는 페이지의 맨 아래에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="c958c-143">예를 들어 테스트 환경용 하나가 환경과 프로덕션 환경이을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="c958c-144">새 디렉터리 이름에 대 한 신중 하 게 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="c958c-145">디렉터리에 대 한 사용자 이름을 사용 하 고 혼동 될 수 있는 사용자 중 하나에 다시 사용자 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![디렉터리 추가](single-sign-on/_static/image6.png)

<span data-ttu-id="c958c-147">포털은 생성, 삭제 및이 환경 내의 사용자 관리에 대 한 전체를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="c958c-148">예를 들어 추가 하려면 사용자로 이동 된 **사용자** 탭을 클릭는 **사용자 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![사용자 추가 단추](single-sign-on/_static/image7.png)

![추가 사용자 대화 상자](single-sign-on/_static/image8.png)

<span data-ttu-id="c958c-151">이 디렉터리에만 존재 하는 새 사용자 만들거나이 디렉터리에 사용자로이 디렉터리 또는 레지스터의 사용자 또는 다른 Azure AD 디렉터리에서 사용자는 Microsoft 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="c958c-152">(실제 디렉터리는 기본 도메인 일 ContosoTest.onmicrosoft.com 합니다. 사용할 수도 있습니다 contoso.com 처럼 사용자가 선택한의 도메인입니다.)</span><span class="sxs-lookup"><span data-stu-id="c958c-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com. You can also use a domain of your own choosing, like contoso.com.)</span></span>

![사용자 유형](single-sign-on/_static/image9.png)

![추가 사용자 대화 상자](single-sign-on/_static/image10.png)

<span data-ttu-id="c958c-155">사용자 역할에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-155">You can assign the user to a role.</span></span>

![사용자 프로필](single-sign-on/_static/image11.png)

<span data-ttu-id="c958c-157">및 임시 암호 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-157">And the account is created with a temporary password.</span></span>

![임시 암호](single-sign-on/_static/image12.png)

<span data-ttu-id="c958c-159">이런 방식이으로 만들 사용자 수 즉시이 클라우드 디렉터리를 사용 하 여 웹 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-159">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="c958c-160">그러나 enterprise single sign-on에 대 한 좋은 것은 **디렉터리 통합** 탭:</span><span class="sxs-lookup"><span data-stu-id="c958c-160">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![디렉터리 통합 탭](single-sign-on/_static/image13.png)

<span data-ttu-id="c958c-162">디렉터리 통합을 사용 하는 경우 및 [도구 다운로드 하 여](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), 조직 내에 이미 사용 중인 기존 온-프레미스 Active Directory와 클라우드 디렉터리를 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-162">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="c958c-163">다음 디렉터리에 저장 된 사용자 모두에 표시 됩니다이 클라우드 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-163">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="c958c-164">이제 클라우드 앱에서 모든 기존 Active Directory 자격 증명을 사용 하 여 직원 들을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-164">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="c958c-165">및이 모든 가능한 – 자체 Azure AD와 동기화 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-165">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="c958c-166">이 도구는는 된 마법사를 사용 하기 쉬운 이러한 스크린샷은에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-166">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="c958c-167">이들은 자세한 지침은, 단지 기본 프로세스를 보여 주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-167">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="c958c-168">자세한 내용은 방법-하려는 do-it의 링크를 참조는 [리소스](#resources) 장의 마지막 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-168">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image14.png)

<span data-ttu-id="c958c-170">클릭 **다음**, 한 다음 Azure Active Directory 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-170">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image15.png)

<span data-ttu-id="c958c-172">클릭 **다음**, 온-프레미스를 입력 한 다음 AD 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-172">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image16.png)

<span data-ttu-id="c958c-174">클릭 **다음**, 클라우드에서 AD 암호의 해시를 저장 하려는 경우를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-174">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image17.png)

<span data-ttu-id="c958c-176">클라우드에 저장할 수 있는 암호 해시는 단방향 해시; 실제 암호는 Azure AD에 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-176">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="c958c-177">사용 해야 클라우드에서 강력한 해시에 대해 결정 한 경우 [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span><span class="sxs-lookup"><span data-stu-id="c958c-177">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="c958c-178">또한 [경우 고려해 야 할 기타 요인 ADFS 사용 여부를 선택](https://technet.microsoft.com/library/jj573653.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-178">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="c958c-179">ADFS 옵션에는 몇 가지 추가 구성 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-179">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="c958c-180">클라우드에서 해시를 저장 하도록 선택 하면, 삭제 하 고 나면를 클릭할 때 디렉터리 동기화 도구가 시작 경우 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-180">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image18.png)

<span data-ttu-id="c958c-182">잠시 후에 완료 되 고</span><span class="sxs-lookup"><span data-stu-id="c958c-182">And in a few minutes you're done.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image19.png)

<span data-ttu-id="c958c-184">Windows 2003 이상, 조직에서 하나의 도메인 컨트롤러에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-184">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="c958c-185">및를 재부팅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-185">And no need to reboot.</span></span> <span data-ttu-id="c958c-186">완료 되는 모든 사용자에 게 클라우드에 하 고 할 수 있는 모든 웹 또는 SAML, OAuth, 또는 Ws-fed를 사용 하 여 모바일 응용 프로그램에 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-186">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="c958c-187">이 보안에 대 한 요청한 가져올 경우에 따라 – Microsoft 사용지 않습니다 자신의 중요 한 비즈니스 데이터에 대 한?</span><span class="sxs-lookup"><span data-stu-id="c958c-187">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="c958c-188">및 그렇다고 수행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-188">And the answer is yes we do.</span></span> <span data-ttu-id="c958c-189">에 내부 Microsoft SharePoint 사이트로 이동 하는 경우 등 [ https://microsoft.sharepoint.com/ ](https://microsoft.sharepoint.com/), 로그인 하 라는 메시지가 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-189">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 로그인](single-sign-on/_static/image20.png)

<span data-ttu-id="c958c-191">Microsoft ADFS를 사용 하도록 설정한 하므로 Microsoft ID를 입력 하면 ad FS 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-191">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![Ad FS 로그인](single-sign-on/_static/image21.png)

<span data-ttu-id="c958c-193">하며이 내부 응용 프로그램에 대 한 액세스는 내부 Microsoft AD 계정에 저장 된 자격 증명을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-193">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint 사이트](single-sign-on/_static/image22.png)

<span data-ttu-id="c958c-195">이미 Azure AD를 사용할 수 있게 하지만 로그인 프로세스를 클라우드에서 Azure AD 디렉터리를 통해 송신 하기 전에를 설정 하는 ADFS 해야 하기 때문에 주로 AD 로그인에 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-195">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="c958c-196">중요 한 문서, 소스 제어, 성능 관리 파일, 판매 보고서, 및 기타를 클라우드에 저장 하 고 보안을 설정 하려면이 정확히 동일한 솔루션을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-196">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="c958c-197">Single sign on에 대 한 Azure AD를 사용 하 여 ASP.NET 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c958c-197">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="c958c-198">Visual Studio에서는 몇 가지 스크린 샷에서 볼 수 있듯이 single sign-on 용 Azure AD를 사용 하는 앱을 만드는 데 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-198">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="c958c-199">새 ASP.NET 응용 프로그램, MVC 또는 Web Forms를 만들 때 기본 인증 방법은 ASP.NET Identity를입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-199">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="c958c-200">Azure AD에는 변경 하려면는 **인증 변경** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-200">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![인증 변경](single-sign-on/_static/image23.png)

<span data-ttu-id="c958c-202">조직 계정, 선택한 도메인 이름을 입력 Single Sign On 다음 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-202">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![인증 대화 상자를 구성 합니다.](single-sign-on/_static/image24.png)

<span data-ttu-id="c958c-204">응용 프로그램 읽기를 제공 하거나 수도 디렉터리 데이터에 대 한 권한이 읽기/쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-204">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="c958c-205">이렇게 하면 사용할 수는 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) 사용자의 전화 번호를 조회할 확인 하는 경우 변경 내용은 하면 사무실에 마지막 등으로 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-205">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="c958c-206">-할 모든 Visual Studio 자격 증명에 대 한 Azure AD 테 넌 트의 관리자에 대 한 문의 한 다음 새 응용 프로그램에 대 한 Azure AD 테 넌 트와 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-206">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="c958c-207">프로젝트를 실행 하는 경우 로그인 페이지를 확인 하 고 Azure AD 디렉터리에서 사용자의 자격 증명을 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-207">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![조직 계정 로그인](single-sign-on/_static/image25.png)

![로그인](single-sign-on/_static/image26.png)

<span data-ttu-id="c958c-210">선택은 Azure에 응용 프로그램을 배포할 때만 하면는 **조직 인증을 사용 하도록 설정** 확인란을 선택한 사용자에 대 한 모든 구성은 Visual Studio 다시 한 번 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-210">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![웹 게시](single-sign-on/_static/image27.png)

<span data-ttu-id="c958c-212">이러한 스크린샷은 Azure AD 인증을 사용 하는 응용 프로그램을 빌드하는 방법을 보여 주는 전체 단계별 자습서에서 제공: [Azure Active Directory와 ASP.NET 응용 프로그램 개발](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-212">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="c958c-213">요약</span><span class="sxs-lookup"><span data-stu-id="c958c-213">Summary</span></span>

<span data-ttu-id="c958c-214">이 장에서 Azure Active Directory, Visual Studio 및 ASP.NET을 쉽게에서 조직의 사용자에 대 한 인터넷 응용 프로그램에 single sign-on을 설정 하는 것이 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-214">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="c958c-215">Active Directory를 사용 하 여 내부 네트워크에 로그온 하는 데 사용 하는 동일한 자격 증명을 사용 하 여 인터넷 응용 프로그램에서 사용자가 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-215">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="c958c-216">[다음 장에서](data-storage-options.md) 클라우드 앱에 사용할 수 있는 데이터 저장소 옵션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-216">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="c958c-217">자료</span><span class="sxs-lookup"><span data-stu-id="c958c-217">Resources</span></span>

<span data-ttu-id="c958c-218">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c958c-218">For more information, see the following resources:</span></span>

- <span data-ttu-id="c958c-219">[Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-219">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="c958c-220">Windowsazure.com 사이트에서 Azure AD 설명서에 대 한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-220">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="c958c-221">단계별 자습서에 대 한 참조는 **개발** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c958c-221">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="c958c-222">[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-222">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="c958c-223">Azure에서 다단계 인증에 대 한 설명서 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-223">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="c958c-224">[조직 계정 인증 옵션](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-224">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="c958c-225">Visual Studio 2013 새 프로젝트 대화 상자에서 Azure AD 인증 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-225">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="c958c-226">[Microsoft Patterns and Practices-Federated Identity 패턴](https://msdn.microsoft.com/library/dn589790.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-226">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="c958c-227">[방법: Azure Active Directory 동기화 도구 설치](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-227">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="c958c-228">[Active Directory Federation Services 2.0 콘텐츠 맵](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-228">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="c958c-229">ADFS 2.0에 대 한 설명서 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-229">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="c958c-230">[Windows Azure AD 응용 프로그램에서 역할 기준 및 ACL 기반 권한 부여](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-230">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="c958c-231">샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-231">Sample application.</span></span>
- <span data-ttu-id="c958c-232">[Azure Active Directory Graph API 블로그](https://blogs.msdn.com/b/aadgraphteam/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-232">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="c958c-233">[액세스 제어에서 BYOD 및 하이브리드 Id 인프라의 디렉터리 통합](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)합니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-233">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="c958c-234">기술 Ed 2014 세션 비디오 Gayana Bagdasaryan 여입니다.</span><span class="sxs-lookup"><span data-stu-id="c958c-234">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c958c-235">[이전](web-development-best-practices.md)
> [다음](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="c958c-235">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
