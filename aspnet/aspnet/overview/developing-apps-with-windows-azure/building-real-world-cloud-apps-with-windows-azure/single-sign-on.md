---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Single Sign-on (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: c988b4864ce7096de7f3ad69b845d3961b7dbc9e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819116"
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="e0e00-104">Single sign On (실제 클라우드 앱 빌드 Azure 사용 하 여)</span><span class="sxs-lookup"><span data-stu-id="e0e00-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="e0e00-105">하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e0e00-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="e0e00-106">[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="e0e00-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="e0e00-107">합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="e0e00-108">13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="e0e00-109">전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="e0e00-110">클라우드 앱을 개발 하는 경우 고려해 야 하는 많은 보안 문제가 있지만이 시리즈에 대 한 집중 하나만: single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="e0e00-111">이 질문 사람들이 종종 질문: "주로 작성 앱 내 회사의 직원 어떻게 이러한 클라우드 앱을 호스트 하 고 계속 사용 하는 내 직원 인지 알고 있어야 하 고 앱을 실행 중인 경우 온-프레미스 환경에서 사용 하는 동일한 보안 모델을 사용 하는 방화벽 내에서 호스팅되 "?</span><span class="sxs-lookup"><span data-stu-id="e0e00-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="e0e00-112">이 시나리오 사용 하도록 설정 하는 방법 중 하나를 Azure Active Directory (Azure AD) 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e0e00-113">Azure AD를 사용 하면 엔터프라이즈 기간 업무 (LOB) 응용 프로그램이 사용할 수 있도록 인터넷을 통해 및도 비즈니스 파트너에 게 이러한 앱을 제공 하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="e0e00-114">Azure AD 소개</span><span class="sxs-lookup"><span data-stu-id="e0e00-114">Introduction to Azure AD</span></span>

<span data-ttu-id="e0e00-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) 제공 [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 클라우드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="e0e00-116">주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-116">Key features include the following:</span></span>

- <span data-ttu-id="e0e00-117">온-프레미스 Active Directory와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="e0e00-118">앱에서 single sign-on 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="e0e00-119">와 같은 개방형 표준을 지 원하는 [SAML](http://en.wikipedia.org/wiki/SAML_2.0)를 [Ws-fed](http://en.wikipedia.org/wiki/WS-Federation), 및 [OAuth 2.0](http://oauth.net/2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="e0e00-120">엔터프라이즈 지원 [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="e0e00-121">인트라넷 응용 프로그램에 로그인 하는 직원을 사용 하도록 설정 하는 데 사용 하는 온-프레미스 Windows Server Active Directory 환경에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="e0e00-122">새로운 Azure AD 수행할 수 있도록 클라우드에서 디렉터리를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="e0e00-123">사용 가능한 기능 및 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="e0e00-124">온-프레미스 Active Directory;에서 완전히 독립 될 수 있습니다. 원하는 누구나 인터넷 앱에서 인증을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="e0e00-126">온-프레미스를 사용 하 여 통합할 수 있습니다 또는 AD입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-126">Or you can integrate it with your on-premises AD.</span></span>

![AD 및 WAAD 통합](single-sign-on/_static/image3.png)

<span data-ttu-id="e0e00-128">이제 온-프레미스를 인증할 수 있는 모든 직원을 방화벽을 열 또는 데이터 센터에 새 서버를 배포 하지 않고도 – 인터넷을 통해도 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="e0e00-129">알고 있고 지금를 사용 하 여 기능에서 내부 앱 단일-로그인을 제공 하는 모든 기존 Active Directory 환경을 활용 하 여 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="e0e00-130">AD와 Azure AD 간의이 연결에 대 한 웹 앱 및 모바일 장치를 클라우드에서 직원을 인증도 설정할 수 있습니다 하 고 수락 하도록 Office 365, SalesForce.com, 또는 Google 앱과 같은 타사 앱을 설정할 수 있습니다. 프로그램 직원의 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="e0e00-131">Office 365를 사용 하는 경우 이미 설정한 Azure AD를 사용 하 여 Office 365 인증 및 권한 부여에 대 한 Azure AD를 사용 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![타사 앱](single-sign-on/_static/image4.png)

<span data-ttu-id="e0e00-133">이 방식의 장점은 언제 든 지 조직의 추가 하거나 사용자를 삭제 합니다. 또는 사용자는 암호 변경, 온-프레미스 환경에서 현재 사용 하는 동일한 프로세스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="e0e00-134">모든 온-프레미스의 AD 변경 내용을 자동으로 전파 되는 클라우드 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="e0e00-135">회사를 사용 하거나 좋은 소식은 Office 365로 이동 하는 경우에 Azure AD를 Office 365 인증에 대 한 Azure AD를 사용 하기 때문에 자동으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="e0e00-136">사용할 수 있도록 쉽게 사용자 고유의 앱에서 Office 365를 사용 하는 동일한 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="e0e00-137">Azure AD 테 넌 트 설정</span><span class="sxs-lookup"><span data-stu-id="e0e00-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="e0e00-138">Azure AD 디렉터리를 Azure ad 라고 [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)를 상당히 쉽습니다 테 넌 트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="e0e00-139">보여드리겠습니다 개념을 설명 하기 위해 Azure 관리 포털에서 수행 방법 이지만 물론 다른 포털 함수 같은 가능 스크립트 또는 관리 API 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="e0e00-140">관리 포털에서 Active Directory 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-140">In the management portal click the Active Directory tab.</span></span>

![포털에서 WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="e0e00-142">Azure 계정에 대 한 Azure AD 테 넌 트를 자동으로 가집니다 및 클릭할 수는 **추가** 추가 디렉터리를 만들려면 페이지의 맨 위에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="e0e00-143">테스트 환경 및 프로덕션 환경에 대 한 예를 들어.</span><span class="sxs-lookup"><span data-stu-id="e0e00-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="e0e00-144">새 디렉터리 이름에 대 한 지 신중히 생각해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="e0e00-145">디렉터리 이름을 사용 하 고 혼동을 줄 수 있는 사용자 중 하나에 대해 다시 사용자 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![디렉터리 추가](single-sign-on/_static/image6.png)

<span data-ttu-id="e0e00-147">포털에는 만들기, 삭제 및이 환경 내에서 사용자 관리에 대 한 완벽 하 게 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="e0e00-148">예를 들어, 추가 사용자로 이동 합니다 **사용자** 탭을 클릭 합니다 **사용자 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![사용자 추가 단추](single-sign-on/_static/image7.png)

![사용자 대화 상자를 추가 합니다.](single-sign-on/_static/image8.png)

<span data-ttu-id="e0e00-151">이 디렉터리에만 존재 하는 새 사용자를 만들 수 있습니다 또는이 디렉터리에 사용자로이 디렉터리에 등록 된 사용자 또는 다른 Azure AD 디렉터리에서 사용자는 Microsoft 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="e0e00-152">(실제 디렉터리에 기본 도메인은 ContosoTest.onmicrosoft.com입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="e0e00-153">사용할 수도 있습니다 도메인에 contoso.com과 같은 고유한 선택.)</span><span class="sxs-lookup"><span data-stu-id="e0e00-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![사용자 형식](single-sign-on/_static/image9.png)

![사용자 대화 상자를 추가 합니다.](single-sign-on/_static/image10.png)

<span data-ttu-id="e0e00-156">역할에 사용자를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-156">You can assign the user to a role.</span></span>

![사용자 프로필](single-sign-on/_static/image11.png)

<span data-ttu-id="e0e00-158">및 계정의 임시 암호를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-158">And the account is created with a temporary password.</span></span>

![임시 암호](single-sign-on/_static/image12.png)

<span data-ttu-id="e0e00-160">이러한 방식으로 만든 사용자 수 즉시이 클라우드 디렉터리를 사용 하 여 웹 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="e0e00-161">그러나 enterprise single sign-on에 대 한 훌륭한 점은입니다 합니다 **디렉터리 통합** 탭:</span><span class="sxs-lookup"><span data-stu-id="e0e00-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![디렉터리 통합 탭](single-sign-on/_static/image13.png)

<span data-ttu-id="e0e00-163">디렉터리 통합을 사용 하는 경우 및 [도구를 다운로드](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), 조직 내에서 이미 사용 중인 기존 온-프레미스 Active Directory를 사용 하 여이 클라우드 디렉터리를 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="e0e00-164">그런 다음 모든 디렉터리에 저장 된 사용자가 표시 됩니다이 클라우드 디렉터리에서.</span><span class="sxs-lookup"><span data-stu-id="e0e00-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="e0e00-165">클라우드 앱에 기존 Active Directory 자격 증명을 사용 하 여 직원의 모든 인증 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="e0e00-166">이 모든 free-Azure AD 자체와 동기화 도구를</span><span class="sxs-lookup"><span data-stu-id="e0e00-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="e0e00-167">이 도구는 이러한 스크린샷은에서 알 수 있듯이 편리 하 게 사용할 있는 마법사.</span><span class="sxs-lookup"><span data-stu-id="e0e00-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="e0e00-168">이들은 지침은 기본 프로세스를 보여 주는 예로 든 것일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="e0e00-169">자세한 내용을 보려면 방법-을 수행-it, 링크를 참조 합니다 [리소스](#resources) 장의 끝에 있는 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image14.png)

<span data-ttu-id="e0e00-171">클릭 **다음**를 선택한 다음 Azure Active Directory 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image15.png)

<span data-ttu-id="e0e00-173">클릭 **다음**, 온-프레미스를 입력 한 다음 AD 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image16.png)

<span data-ttu-id="e0e00-175">클릭 **다음**, 그런 다음 클라우드에서 AD 암호의 해시를 저장 하려는 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image17.png)

<span data-ttu-id="e0e00-177">클라우드에 저장할 수 있는 암호 해시는 단방향 해시입니다. 실제 암호는 Azure AD에 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="e0e00-178">사용 해야 해시를 클라우드에 저장 하는 것에 대 한 않으려면 [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span><span class="sxs-lookup"><span data-stu-id="e0e00-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="e0e00-179">이 밖에도 [때 고려해 야 할 요인 ADFS를 사용할 것인지 선택](https://technet.microsoft.com/library/jj573653.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0e00-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="e0e00-180">ADFS 옵션에는 몇 가지 추가 구성 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="e0e00-181">클라우드에서 해시를 저장 하도록 선택 하면, 완료 및 도구를 클릭 하면 디렉터리 동기화를 시작 하는 경우 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image18.png)

<span data-ttu-id="e0e00-183">고 잠시 후에 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-183">And in a few minutes you're done.</span></span>

![WAAD 동기화 도구 구성 마법사](single-sign-on/_static/image19.png)

<span data-ttu-id="e0e00-185">Windows 2003 이상 조직에서 하나의 도메인 컨트롤러에서이 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="e0e00-186">및 다시 부팅 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-186">And no need to reboot.</span></span> <span data-ttu-id="e0e00-187">완료 하 고 모든 사용자는 클라우드에서 수행할 수 있습니다 하는 경우 웹 또는 SAML, OAuth 또는 Ws-fed를 사용 하 여 모바일 응용 프로그램에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="e0e00-188">이것이 얼마나 안전에 대 한 질문 가져올 경우에 따라 – Microsoft 사용지 않습니다 자신의 중요 한 비즈니스 데이터에 대 한?</span><span class="sxs-lookup"><span data-stu-id="e0e00-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="e0e00-189">및 그렇다고 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-189">And the answer is yes we do.</span></span> <span data-ttu-id="e0e00-190">예를 들어에서 내부 Microsoft SharePoint 사이트로 이동 [ https://microsoft.sharepoint.com/ ](https://microsoft.sharepoint.com/), 로그인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 로그인](single-sign-on/_static/image20.png)

<span data-ttu-id="e0e00-192">Microsoft가 ADFS를 사용 하도록 설정 되므로 Microsoft ID를 입력 하면 ADFS 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![ADFS 로그인](single-sign-on/_static/image21.png)

<span data-ttu-id="e0e00-194">및이 내부 응용 프로그램에 액세스할 수 있는 내부 Microsoft AD 계정에 저장 된 자격 증명을 입력 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint 사이트](single-sign-on/_static/image22.png)

<span data-ttu-id="e0e00-196">에서는 이미 Azure AD가 사용할 수 있지만 로그인 프로세스를 클라우드에서 Azure AD 디렉터리를 통해 송신 하기 전에를 설정 하는 ADFS 때문에 주로 AD 로그인 서버를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="e0e00-197">중요 한 문서, 소스 제어, 성능 관리 파일, 판매 보고서 및 클라우드에서 더 많은 저장 하 고 보안을 유지 하는 데이 정확히 동일한 솔루션을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="e0e00-198">Single sign on에 대 한 Azure AD를 사용 하는 ASP.NET 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e0e00-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="e0e00-199">Visual Studio에서는 몇 가지 스크린 샷을에서 알 수 있듯이 Azure AD single sign-on을 사용 하는 앱을 만드는 데 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="e0e00-200">새 ASP.NET 응용 프로그램, MVC 또는 Web Forms를 만들 때 기본 인증 방법은 ASP.NET Id입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="e0e00-201">클릭 하면 Azure AD를 변경 하는 **인증 변경** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![인증 변경](single-sign-on/_static/image23.png)

<span data-ttu-id="e0e00-203">조직 계정 선택, 사용자가 도메인 이름을 입력 하 고 Single Sign On 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![인증 대화 상자를 구성 합니다.](single-sign-on/_static/image24.png)

<span data-ttu-id="e0e00-205">앱 읽기를 제공 하거나 수도 디렉터리 데이터에 대 한 권한이 읽기/쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="e0e00-206">이렇게 하면 사용할 수는 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) 사용자의 전화 번호를 검색할 알아보십시오 경우 사무실에 마지막으로, 등를 기록 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e0e00-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="e0e00-207">수행 해야 하는 모든 Visual Studio는 자격 증명을 요청에 Azure AD 테 넌 트의 관리자에 대 한 한 다음 프로젝트와 새 응용 프로그램에 대 한 Azure AD 테 넌 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="e0e00-208">프로젝트를 실행 하면 로그인 페이지가 표시 됩니다 및 Azure AD 디렉터리에서 사용자의 자격 증명을 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![조직 계정 로그인](single-sign-on/_static/image25.png)

![로그인](single-sign-on/_static/image26.png)

<span data-ttu-id="e0e00-211">Azure에 앱을 배포할 때 수행 해야 하는 모든가 선택는 **조직 인증 사용** 확인란을 선택한 Visual Studio를 모든 구성의 이번 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![웹 게시](single-sign-on/_static/image27.png)

<span data-ttu-id="e0e00-213">Azure AD 인증을 사용 하는 앱을 빌드하는 방법을 보여 주는 전체 단계별 자습서에서 제공 되는 이러한 스크린 샷: [Azure Active Directory를 사용 하 여 ASP.NET 앱 개발](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="e0e00-214">요약</span><span class="sxs-lookup"><span data-stu-id="e0e00-214">Summary</span></span>

<span data-ttu-id="e0e00-215">이 장에서 Azure Active Directory, Visual Studio 및 ASP.NET을 쉽게 조직의 사용자에 대 한 인터넷 응용 프로그램에서 single sign-on을 설정 하는 것이 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="e0e00-216">사용자가 Active Directory를 사용 하 여 내부 네트워크에 로그온 하는를 사용 하 여 동일한 자격 증명을 사용 하 여 인터넷 응용 프로그램에 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="e0e00-217">합니다 [다음 장에서](data-storage-options.md) 클라우드 앱에 사용할 수 있는 데이터 저장소 옵션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="e0e00-218">자료</span><span class="sxs-lookup"><span data-stu-id="e0e00-218">Resources</span></span>

<span data-ttu-id="e0e00-219">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0e00-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="e0e00-220">[Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="e0e00-221">Windowsazure.com 사이트의 Azure AD 설명서에 대 한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="e0e00-222">단계별 자습서에 대 한 참조를 **개발** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="e0e00-223">[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="e0e00-224">Azure에서 multi-factor authentication에 대 한 설명서 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="e0e00-225">[조직 계정 인증 옵션](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="e0e00-226">Visual Studio 2013 새 프로젝트 대화 상자에서 Azure AD 인증 옵션에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="e0e00-227">[Microsoft Patterns and Practices-페더레이션 Id 패턴](https://msdn.microsoft.com/library/dn589790.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="e0e00-228">[방법: Azure Active Directory Sync 도구를 설치 하](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="e0e00-229">[Active Directory Federation Services 2.0 콘텐츠 맵](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="e0e00-230">ADFS 2.0에 대 한 설명서 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="e0e00-231">[Windows Azure AD 응용 프로그램에서 역할 기반 및 ACL 기반 권한 부여](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="e0e00-232">샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-232">Sample application.</span></span>
- <span data-ttu-id="e0e00-233">[Azure Active Directory Graph API 블로그](https://blogs.msdn.com/b/aadgraphteam/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="e0e00-234">[Access Control에서 BYOD 및 하이브리드 Id 인프라의 디렉터리 통합](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="e0e00-235">Tech Ed 2014 세션 비디오 Gayana Bagdasaryan 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e00-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e0e00-236">[이전](web-development-best-practices.md)
> [다음](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="e0e00-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
