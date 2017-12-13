---
uid: web-api/overview/security/external-authentication-services
title: "외부 인증 서비스가 ASP.NET web API (C#) | Microsoft Docs"
author: rmcmurray
description: "외부 인증 서비스를 사용 하 여 ASP.NET Web API에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2013
ms.topic: article
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: 5d6e6727f387d047e7b41a6efa0d2dadf467558e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="c6fca-103">외부 인증 서비스가 ASP.NET web API (C#)</span><span class="sxs-lookup"><span data-stu-id="c6fca-103">External Authentication Services with ASP.NET Web API (C#)</span></span>
====================
<span data-ttu-id="c6fca-104">으로 [Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="c6fca-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="c6fca-105">Visual Studio 2013 및 ASP.NET 4.5.1에 대 한 보안 옵션을 확장 [단일 페이지 응용 프로그램](../../../single-page-application/index.md) (SPA) 및 [웹 API](../../index.md) 몇 가지를 포함 하는 외부 인증 서비스와 통합 하는 서비스 OAuth/OpenID 및 소셜 미디어 인증 서비스: Microsoft 계정, Twitter, Facebook 및 Google 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-105">Visual Studio 2013 and ASP.NET 4.5.1 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>

### <a name="in-this-walkthrough"></a><span data-ttu-id="c6fca-106">이 연습에서</span><span class="sxs-lookup"><span data-stu-id="c6fca-106">In This Walkthrough</span></span>

- [<span data-ttu-id="c6fca-107">외부 인증 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c6fca-107">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="c6fca-108">샘플 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c6fca-108">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="c6fca-109">Facebook 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c6fca-109">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="c6fca-110">Google 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c6fca-110">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="c6fca-111">Microsoft 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c6fca-111">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="c6fca-112">Twitter 인증 사용</span><span class="sxs-lookup"><span data-stu-id="c6fca-112">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="c6fca-113">추가 정보</span><span class="sxs-lookup"><span data-stu-id="c6fca-113">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="c6fca-114">외부 인증 서비스를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-114">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="c6fca-115">정규화 된 도메인 이름을 사용 하 여 IIS Express를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-115">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="c6fca-116">Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="c6fca-116">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="c6fca-117">로컬 등록을 사용 하지 않도록 선택 사항:</span><span class="sxs-lookup"><span data-stu-id="c6fca-117">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="c6fca-118">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c6fca-118">Prerequisites</span></span>

<span data-ttu-id="c6fca-119">이 연습에서 예제를 수행 하려면 다음 조건이 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-119">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="c6fca-120">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c6fca-120">Visual Studio 2013</span></span>
- <span data-ttu-id="c6fca-121">다음과 같은 외부 인증 서비스 중 하나 이상에 대 한 계정:</span><span class="sxs-lookup"><span data-stu-id="c6fca-121">An account for at least one of the following external authentication services:</span></span>

    - <span data-ttu-id="c6fca-122">Google 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="c6fca-122">A Google user account</span></span>
    - <span data-ttu-id="c6fca-123">응용 프로그램 식별자 및 다음과 같은 소셜 미디어 인증 서비스 중 하나에 대 한 비밀 키와 함께 개발자 계정:</span><span class="sxs-lookup"><span data-stu-id="c6fca-123">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

        - <span data-ttu-id="c6fca-124">Microsoft 계정 ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="c6fca-124">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
        - <span data-ttu-id="c6fca-125">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="c6fca-125">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
        - <span data-ttu-id="c6fca-126">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="c6fca-126">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="c6fca-127">외부 인증 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c6fca-127">Using External Authentication Services</span></span>

<span data-ttu-id="c6fca-128">다양 한 개발을 줄이기 위해 웹 개발자 도움말을 현재 사용할 수 있는 외부 인증 서비스는 새로운 웹 응용 프로그램을 만들 때 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-128">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="c6fca-129">웹 사용자 일반적으로 여러 기존 계정이 있는 인기 있는 웹 서비스 및 소셜 미디어 웹 사이트에 대 한 따라서는 웹 응용 프로그램으로 구현 외부 웹 서비스 또는 소셜 미디어 웹 사이트에서 인증 서비스를 저장할 때 개발 시는 소요 된 인증 구현을 만들기.</span><span class="sxs-lookup"><span data-stu-id="c6fca-129">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="c6fca-130">웹 응용 프로그램에 대해 다른 계정을 만들지 않아도 및 다른 사용자 이름 및 암호를 기억 하지 않아도 최종 사용자가 저장 하는 외부 인증 서비스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-130">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="c6fca-131">이전에 개발자는 했습니다 두 가지 선택 사항: 자체 인증 구현을 만들거나 외부 인증 서비스 응용 프로그램에 통합 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-131">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="c6fca-132">가장 기본적인 수준에서 다음 다이어그램은 외부 인증 서비스를 사용 하도록 구성 된 웹 응용 프로그램에서 정보를 요청 하는 사용자 에이전트 (웹 브라우저)에 대 한 간단한 요청 흐름을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-132">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

<span data-ttu-id="c6fca-133">[![](external-authentication-services/_static/image2.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-133">[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)</span></span>

<span data-ttu-id="c6fca-134">위 다이어그램에 사용자 에이전트 (또는이 예제에서 웹 브라우저) 외부 인증 서비스에 웹 브라우저를 리디렉션하는 웹 응용 프로그램을 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-134">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="c6fca-135">사용자 에이전트 자격 증명을 외부 인증 서비스에 보내고 몇 가지 형태의 원래 웹 응용 프로그램에 외부 인증 서비스에서 사용자 에이전트를 리디렉션할 사용자 에이전트에 성공적으로 인증 하는 경우는 토큰의 사용자 에이전트에서 웹 응용 프로그램으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-135">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="c6fca-136">웹 응용 프로그램 외부 인증 서비스에서 사용자 에이전트를 성공적으로 인증 된 하 고 웹 응용 프로그램 사용자 에이전트에 대 한 추가 정보를 수집 토큰을 사용할 수 있는지 확인 하는 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-136">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="c6fca-137">응용 프로그램이 작업이 완료 되 면 사용자 에이전트의 정보를 처리 하는, 웹 응용 프로그램은 반환 권한 부여 설정에 따라 사용자 에이전트에 대 한 적절 한 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-137">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="c6fca-138">이 두 번째 예에서 사용자 에이전트는 웹 응용 프로그램 및 외부 권한 부여 서버와 협상 하 고 사용자에 대 한 추가 정보를 검색 하기 위해 외부 권한 부여 서버와 추가 통신을 수행 하는 웹 응용 프로그램 에이전트:</span><span class="sxs-lookup"><span data-stu-id="c6fca-138">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

<span data-ttu-id="c6fca-139">[![](external-authentication-services/_static/image4.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-139">[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)</span></span>

<span data-ttu-id="c6fca-140">Visual Studio 2013 및 ASP.NET 4.5.1 쉽게 외부 인증 서비스와의 통합 개발자를 위한 다음과 같은 인증 서비스에 대 한 기본 제공 통합을 제공 하 여:</span><span class="sxs-lookup"><span data-stu-id="c6fca-140">Visual Studio 2013 and ASP.NET 4.5.1 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="c6fca-141">Facebook</span><span class="sxs-lookup"><span data-stu-id="c6fca-141">Facebook</span></span>
- <span data-ttu-id="c6fca-142">Google</span><span class="sxs-lookup"><span data-stu-id="c6fca-142">Google</span></span>
- <span data-ttu-id="c6fca-143">Microsoft 계정 (Windows Live ID 계정)</span><span class="sxs-lookup"><span data-stu-id="c6fca-143">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="c6fca-144">Twitter</span><span class="sxs-lookup"><span data-stu-id="c6fca-144">Twitter</span></span>

<span data-ttu-id="c6fca-145">이 연습에 나와 있는 예제에서는 Visual Studio 2013과 함께 제공 되는 새 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 각 지원 되는 외부 인증 서비스를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-145">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2013.</span></span>

> [!NOTE]
> <span data-ttu-id="c6fca-146">필요한 경우에 FQDN 외부 인증 서비스에 대 한 설정에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-146">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="c6fca-147">이 요구 사항은 응용 프로그램 설정에 FQDN 클라이언트에서 사용 되는 FQDN과 일치 해야 하는 일부 외부 인증 서비스의 보안 제약 조건을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-147">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="c6fca-148">(각 외부 인증 서비스에 대해이 단계는 크게 달라질 수;이 코드는 필요한 각 외부 인증 서비스 및 이러한 설정을 구성 하는 방법에 대 한 설명서를 참조 해야 합니다.) 참조를 테스트이 환경에 대 한 FQDN을 사용 하려면 IIS Express를 구성 하는 경우는 [정규화 된 도메인 이름을 사용 하 여 IIS Express 구성](#FQDN) 이 연습 뒷부분의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-148">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>


<a id="SAMPLE"></a>
## <a name="creating-a-sample-web-application"></a><span data-ttu-id="c6fca-149">샘플 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c6fca-149">Creating a Sample Web Application</span></span>

<span data-ttu-id="c6fca-150">다음 단계를 안내 합니다 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 샘플 응용 프로그램 만들기 및 각이 연습의 뒷부분에서 외부 인증 서비스에 대 한이 샘플 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-150">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="c6fca-151">Visual Studio 2013 선택 시작 **새 프로젝트** 시작 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="c6fca-151">Start Visual Studio 2013 select **New Project** from the Start page.</span></span> <span data-ttu-id="c6fca-152">또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-152">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="c6fca-153">[![](external-authentication-services/_static/image6.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-153">[![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png)</span></span>

<span data-ttu-id="c6fca-154">경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 선택 **설치 됨** **템플릿** 확장 **Visual C#**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-154">When the **New Project** dialog box is displayed, select **Installed** **Templates** and expand **Visual C#**.</span></span> <span data-ttu-id="c6fca-155">아래 **Visual C#**선택, **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-155">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="c6fca-156">프로젝트 템플릿 목록에서 선택 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-156">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="c6fca-157">프로젝트에 대 한 이름을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-157">Enter a name for your project and click **OK**.</span></span>

<span data-ttu-id="c6fca-158">[![](external-authentication-services/_static/image8.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-158">[![](external-authentication-services/_static/image8.png "Click to Expand the Image")](external-authentication-services/_static/image7.png)</span></span>

<span data-ttu-id="c6fca-159">경우는 **새 ASP.NET 프로젝트** 표시, select는 **SPA** 템플릿을 **프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-159">When the **New ASP.NET Project** is displayed, select the **SPA** template and click **Create Project**.</span></span>

<span data-ttu-id="c6fca-160">[![](external-authentication-services/_static/image10.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-160">[![](external-authentication-services/_static/image10.png "Click to Expand the Image")](external-authentication-services/_static/image9.png)</span></span>

<span data-ttu-id="c6fca-161">대기 Visual studio 2013에서 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-161">Wait as Visual Studio 2013 creates your project.</span></span>

<span data-ttu-id="c6fca-162">[![](external-authentication-services/_static/image12.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-162">[![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png)</span></span>

<span data-ttu-id="c6fca-163">Visual Studio 2013 프로젝트 만들기 완료 되 면 열는 *Startup.Auth.cs* 에 있는 파일의 **앱\_시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-163">When Visual Studio 2013 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="c6fca-164">[![](external-authentication-services/_static/image14.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-164">[![](external-authentication-services/_static/image14.png "Click to Expand the Image")](external-authentication-services/_static/image13.png)</span></span>

<span data-ttu-id="c6fca-165">프로젝트를 처음 만들 때 외부 인증 서비스가 사용할 수에서 *Startup.Auth.cs* 파일; 허용 위치에 대 한 강조 표시 된 섹션으로, 다음 떠올릴 코드를 보여 줍니다. 외부 인증 서비스 및 ASP.NET 응용 프로그램과 Microsoft 계정, Twitter, Facebook 또는 Google 인증을 사용 하려면 모든 관련 설정:</span><span class="sxs-lookup"><span data-stu-id="c6fca-165">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="c6fca-166">F5 키를 눌러을 빌드하고 웹 응용 프로그램을 디버깅할 때 표시 되는 외부 인증 서비스가 없습니다 정의 된 로그인 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-166">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

<span data-ttu-id="c6fca-167">[![](external-authentication-services/_static/image16.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-167">[![](external-authentication-services/_static/image16.png "Click to Expand the Image")](external-authentication-services/_static/image15.png)</span></span>

<span data-ttu-id="c6fca-168">다음 섹션에서는 각 Visual Studio 2013에서 ASP.NET과 제공 하는 외부 인증 서비스를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-168">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2013.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="c6fca-169">Facebook 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c6fca-169">Enabling Facebook Authentication</span></span>

<span data-ttu-id="c6fca-170">Facebook을 사용 하 여 인증에 필요한 Facebook 개발자 계정을 만들 수 있습니다 하 고 프로젝트에 작동 하는 데는 응용 프로그램 ID와 Facebook의 비밀 키를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-170">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="c6fca-171">Facebook 개발자 계정을 만들고 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 정보를 참조 하십시오. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-171">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="c6fca-172">한 번에 받은 응용 프로그램 ID 및 비밀 키 웹 응용 프로그램에 대 한 Facebook 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-172">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="c6fca-173">프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="c6fca-173">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="c6fca-174">[![](external-authentication-services/_static/image18.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-174">[![](external-authentication-services/_static/image18.png "Click to Expand the Image")](external-authentication-services/_static/image17.png)</span></span>
2. <span data-ttu-id="c6fca-175">강조 표시 된 코드 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-175">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="c6fca-176">제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄을 주석 표시 한 후 응용 프로그램 ID 및 비밀 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-176">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="c6fca-177">이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-177">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="c6fca-178">웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Facebook 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-178">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    <span data-ttu-id="c6fca-179">[![](external-authentication-services/_static/image20.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-179">[![](external-authentication-services/_static/image20.png "Click to Expand the Image")](external-authentication-services/_static/image19.png)</span></span>
5. <span data-ttu-id="c6fca-180">클릭할 때는 **Facebook** 단추, 브라우저 Facebook 로그인 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-180">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    <span data-ttu-id="c6fca-181">[![](external-authentication-services/_static/image22.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-181">[![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)</span></span>
6. <span data-ttu-id="c6fca-182">Facebook 자격 증명을 입력 하 고를 클릭 한 후 **로그인**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 연관 시킬 프로그램 Facebook 계정:</span><span class="sxs-lookup"><span data-stu-id="c6fca-182">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    <span data-ttu-id="c6fca-183">[![](external-authentication-services/_static/image24.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-183">[![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)</span></span>
7. <span data-ttu-id="c6fca-184">사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Facebook 계정에 대 한:</span><span class="sxs-lookup"><span data-stu-id="c6fca-184">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    <span data-ttu-id="c6fca-185">[![](external-authentication-services/_static/image26.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-185">[![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)</span></span>

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="c6fca-186">Google 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c6fca-186">Enabling Google Authentication</span></span>

<span data-ttu-id="c6fca-187">Google은 단연 가장 쉬운 개발자 계정으로 필요 하지 않거나 다른 외부 인증 서비스와 응용 프로그램 ID 또는 비밀 키와 같은 추가 정보 필요 아니므로 사용할 수 있도록 외부 인증 서비스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-187">Google is by far the easiest of the external authentication services to enable because it doesn't require a developer account, nor does it require additional information like your application ID or secret key as the other external authentication services necessitate.</span></span>

<span data-ttu-id="c6fca-188">웹 응용 프로그램에 대 한 Google 인증을 사용 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-188">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="c6fca-189">프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="c6fca-189">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="c6fca-190">[![](external-authentication-services/_static/image28.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-190">[![](external-authentication-services/_static/image28.png "Click to Expand the Image")](external-authentication-services/_static/image27.png)</span></span>
2. <span data-ttu-id="c6fca-191">강조 표시 된 코드 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-191">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="c6fca-192">제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄의 주석 처리 제거 후 프로젝트를 다시 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-192">Remove the &quot;//&quot; characters to uncomment the highlighted line of code, and then recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="c6fca-193">웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Google 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-193">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    <span data-ttu-id="c6fca-194">[![](external-authentication-services/_static/image30.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-194">[![](external-authentication-services/_static/image30.png "Click to Expand the Image")](external-authentication-services/_static/image29.png)</span></span>
5. <span data-ttu-id="c6fca-195">클릭는 **Google** 단추 브라우저가 Google 로그인 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-195">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    <span data-ttu-id="c6fca-196">[![](external-authentication-services/_static/image32.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-196">[![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)</span></span>
6. <span data-ttu-id="c6fca-197">Google 자격 증명을 입력 하 고를 클릭 한 후 **로그인**, Google 웹 응용 프로그램 Google 계정에 액세스할 수 있는 권한이 있는지 확인 하 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-197">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    <span data-ttu-id="c6fca-198">[![](external-authentication-services/_static/image34.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-198">[![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)</span></span>
7. <span data-ttu-id="c6fca-199">클릭할 때 **Accept**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 을 Google 계정에 연결 하려는:</span><span class="sxs-lookup"><span data-stu-id="c6fca-199">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    <span data-ttu-id="c6fca-200">[![](external-authentication-services/_static/image36.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-200">[![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)</span></span>
8. <span data-ttu-id="c6fca-201">사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Google 계정에 대 한:</span><span class="sxs-lookup"><span data-stu-id="c6fca-201">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    <span data-ttu-id="c6fca-202">[![](external-authentication-services/_static/image38.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-202">[![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)</span></span>

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="c6fca-203">Microsoft 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c6fca-203">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="c6fca-204">Microsoft 인증에 필요한 개발자 계정을 만들 수 있습니다 및 클라이언트 ID와 클라이언트 암호가 작동 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-204">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="c6fca-205">Microsoft 개발자 계정 만들기 및 클라이언트 ID와 클라이언트 암호를 가져오는 방법에 대 한 정보를 참조 하십시오. [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-205">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="c6fca-206">한 번에 받은 소비자 키 및 소비자 암호 웹 응용 프로그램에 대 한 Microsoft 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-206">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="c6fca-207">프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="c6fca-207">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="c6fca-208">[![](external-authentication-services/_static/image40.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-208">[![](external-authentication-services/_static/image40.png "Click to Expand the Image")](external-authentication-services/_static/image39.png)</span></span>
2. <span data-ttu-id="c6fca-209">강조 표시 된 코드 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-209">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="c6fca-210">제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄을 주석 표시 한 후 클라이언트 ID와 클라이언트 암호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-210">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="c6fca-211">이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-211">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="c6fca-212">웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Microsoft 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-212">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    <span data-ttu-id="c6fca-213">[![](external-authentication-services/_static/image42.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-213">[![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)</span></span>
5. <span data-ttu-id="c6fca-214">클릭할 때는 **Microsoft** 단추, 브라우저 Microsoft 로그인 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-214">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    <span data-ttu-id="c6fca-215">[![](external-authentication-services/_static/image44.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-215">[![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)</span></span>
6. <span data-ttu-id="c6fca-216">Microsoft 자격 증명을 입력 하 고를 클릭 한 후 **로그인**, 웹 응용 프로그램에 Microsoft 계정에 액세스할 수 있는 권한이 있는지 확인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-216">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    <span data-ttu-id="c6fca-217">[![](external-authentication-services/_static/image46.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-217">[![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)</span></span>
7. <span data-ttu-id="c6fca-218">클릭할 때 **예**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 을 Microsoft 계정에 연결 하려는:</span><span class="sxs-lookup"><span data-stu-id="c6fca-218">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    <span data-ttu-id="c6fca-219">[![](external-authentication-services/_static/image48.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-219">[![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)</span></span>
8. <span data-ttu-id="c6fca-220">사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Microsoft 계정에 대 한:</span><span class="sxs-lookup"><span data-stu-id="c6fca-220">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    <span data-ttu-id="c6fca-221">[![](external-authentication-services/_static/image50.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-221">[![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)</span></span>

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="c6fca-222">Twitter 인증 사용</span><span class="sxs-lookup"><span data-stu-id="c6fca-222">Enabling Twitter Authentication</span></span>

<span data-ttu-id="c6fca-223">Twitter 인증에 필요한 개발자 계정을 만들 수 있습니다 및 소비자 키 및 소비자 암호 작동 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-223">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="c6fca-224">Twitter 개발자 계정을 만들고 소비자 키 및 소비자 암호를 가져오는 방법에 대 한 정보를 참조 하십시오. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-224">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="c6fca-225">한 번에 받은 소비자 키 및 소비자 암호 웹 응용 프로그램에 대 한 Twitter 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-225">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="c6fca-226">프로젝트를 연 Visual Studio 2013에서 열고는 *Startup.Auth.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="c6fca-226">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="c6fca-227">[![](external-authentication-services/_static/image52.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image51.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-227">[![](external-authentication-services/_static/image52.png "Click to Expand the Image")](external-authentication-services/_static/image51.png)</span></span>
2. <span data-ttu-id="c6fca-228">강조 표시 된 코드 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-228">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="c6fca-229">제거는 &quot; // &quot; 문자 코드를 강조 표시 된 줄을 주석 표시 한 후 소비자 키 및 소비자 암호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-229">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="c6fca-230">이러한 매개 변수를 추가한 후 프로젝트를 다시 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-230">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="c6fca-231">웹 브라우저에서 웹 응용 프로그램을 열고 f5 키를 눌러 Twitter 변수가 외부 인증 서비스 변수로 정의 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-231">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    <span data-ttu-id="c6fca-232">[![](external-authentication-services/_static/image54.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image53.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-232">[![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)</span></span>
5. <span data-ttu-id="c6fca-233">클릭할 때는 **Twitter** 단추, 브라우저 Twitter 로그인 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-233">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    <span data-ttu-id="c6fca-234">[![](external-authentication-services/_static/image56.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image55.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-234">[![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)</span></span>
6. <span data-ttu-id="c6fca-235">Twitter 자격 증명을 입력 하 고를 클릭 한 후 **Authorize 앱**, 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다를 묻는 메시지가 나타납니다에 대 한는 **사용자 이름** 연관 시킬 Twitter 계정:</span><span class="sxs-lookup"><span data-stu-id="c6fca-235">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    <span data-ttu-id="c6fca-236">[![](external-authentication-services/_static/image58.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image57.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-236">[![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)</span></span>
7. <span data-ttu-id="c6fca-237">사용자 이름을 입력 하 고 클릭 한 후의 **등록** 단추, 웹 응용 프로그램의 기본 표시 됩니다 **홈 페이지** Twitter 계정에 대 한:</span><span class="sxs-lookup"><span data-stu-id="c6fca-237">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    <span data-ttu-id="c6fca-238">[![](external-authentication-services/_static/image60.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image59.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-238">[![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)</span></span>

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="c6fca-239">추가 정보</span><span class="sxs-lookup"><span data-stu-id="c6fca-239">Additional Information</span></span>

<span data-ttu-id="c6fca-240">OAuth 및 OpenID를 사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 다음 Url을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c6fca-240">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [<span data-ttu-id="c6fca-241">https://go.microsoft.com/fwlink/?LinkID=252166</span><span class="sxs-lookup"><span data-stu-id="c6fca-241">https://go.microsoft.com/fwlink/?LinkID=252166</span></span>](https://go.microsoft.com/fwlink/?LinkID=252166)
- [<span data-ttu-id="c6fca-242">https://go.microsoft.com/fwlink/?LinkID=243995</span><span class="sxs-lookup"><span data-stu-id="c6fca-242">https://go.microsoft.com/fwlink/?LinkID=243995</span></span>](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="c6fca-243">외부 인증 서비스를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-243">Combining External Authentication Services</span></span>

<span data-ttu-id="c6fca-244">유연성을 높이기 위해 동시에 여러 외부 인증 서비스를 정의할 수 있습니다-이렇게 하면 웹 응용 프로그램의 사용자가 활성화 된 외부 인증 서비스가 중 어디에서 든 계정을 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-244">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

<span data-ttu-id="c6fca-245">[![](external-authentication-services/_static/image62.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image61.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-245">[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)</span></span>

<a id="FQDN"></a>
### <a name="configuring-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="c6fca-246">정규화 된 도메인 이름을 사용 하 여 IIS Express를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-246">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>

<span data-ttu-id="c6fca-247">일부 외부 인증 공급자와 같은 HTTP 주소를 사용 하 여 응용 프로그램 테스트를 지원 하지 않는 `http://localhost:port/`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-247">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="c6fca-248">이 문제를 해결 하려면 정적 정규화 된 도메인 이름 (FQDN) 매핑 호스트 파일을 추가한 테스트 하 고 디버깅에 대 한 FQDN을 사용 하려면 Visual Studio 2013에서 프로젝트 옵션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-248">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2013 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="c6fca-249">이렇게 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-249">To do so, use the following steps:</span></span>

- <span data-ttu-id="c6fca-250">호스트 파일 매핑 정적 FQDN을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-250">Add a static FQDN mapping your HOSTS file:</span></span>

    1. <span data-ttu-id="c6fca-251">창에서 관리자 권한 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-251">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="c6fca-252">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-252">Type the following command:</span></span>

        <span data-ttu-id="c6fca-253"><kbd>메모장 %WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="c6fca-253"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
    3. <span data-ttu-id="c6fca-254">호스트 파일에 다음과 같은 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-254">Add an entry like the following to the HOSTS file:</span></span>

        <span data-ttu-id="c6fca-255"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="c6fca-255"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
    4. <span data-ttu-id="c6fca-256">저장 하 고 호스트 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-256">Save and close your HOSTS file.</span></span>
- <span data-ttu-id="c6fca-257">FQDN을 사용 하도록 Visual Studio 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-257">Configure your Visual Studio project to use the FQDN:</span></span>

    1. <span data-ttu-id="c6fca-258">프로젝트를 Visual Studio 2013에서 연 클릭는 **프로젝트** 메뉴에서 다음 프로젝트의 속성을 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-258">When your project is open in Visual Studio 2013, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="c6fca-259">예를 들어, 선택할 수 **WebApplication1 속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-259">For example, you might select **WebApplication1 Properties**.</span></span>
    2. <span data-ttu-id="c6fca-260">선택 된 **웹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-260">Select the **Web** tab.</span></span>
    3. <span data-ttu-id="c6fca-261">에 대 한 FQDN을 입력에서 **프로젝트 Url**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-261">Enter your FQDN for the **Project Url**.</span></span> <span data-ttu-id="c6fca-262">예를 들어 입력 <kbd>http://www.wingtiptoys.com</kbd> 호스트 파일에 추가 되는 FQDN 매핑은 복제본이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="c6fca-262">For example, you would enter <kbd>http://www.wingtiptoys.com</kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>
- <span data-ttu-id="c6fca-263">IIS Express 응용 프로그램에 대 한 FQDN을 사용 하도록 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-263">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="c6fca-264">창에서 관리자 권한 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-264">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="c6fca-265">IIS Express 폴더에 변경 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-265">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="c6fca-266"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="c6fca-266"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="c6fca-267">응용 프로그램에 FQDN을 추가 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-267">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="c6fca-268"><kbd>appcmd.exe 설정 구성-section:system.applicationHost/sites / +&quot;[이름 = 'WebApplication1'].bindings. [ 프로토콜 bindingInformation'http ', = ='*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="c6fca-268"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

 <span data-ttu-id="c6fca-269">여기서 **WebApplication1** 프로젝트의 이름 및 **bindingInformation** 테스트에 사용할 포트 번호 및 FQDN을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-269">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="c6fca-270">Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="c6fca-270">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="c6fca-271">Microsoft 인증에 대 한 Windows Live에 응용 프로그램을 연결 하는 것은 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-271">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="c6fca-272">Windows Live에 응용 프로그램을 아직 연결 하지 않은 경우 다음 단계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-272">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="c6fca-273">찾아 [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) 고 Microsoft 계정 이름 및 메시지가 표시 되 면 암호를 입력 한 다음 클릭 **로그인**:</span><span class="sxs-lookup"><span data-stu-id="c6fca-273">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

    <span data-ttu-id="c6fca-274">[![](external-authentication-services/_static/image64.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image63.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-274">[![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png)</span></span>
2. <span data-ttu-id="c6fca-275">이름 및 메시지가 표시 되 면 응용 프로그램의 언어를 입력 한 다음 클릭 **동의**:</span><span class="sxs-lookup"><span data-stu-id="c6fca-275">Enter the name and language of your application when prompted, and then click **I accept**:</span></span>

    <span data-ttu-id="c6fca-276">[![](external-authentication-services/_static/image66.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image65.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-276">[![](external-authentication-services/_static/image66.png "Click to Expand the Image")](external-authentication-services/_static/image65.png)</span></span>
3. <span data-ttu-id="c6fca-277">에 **API 설정** 응용 프로그램 페이지에서 응용 프로그램 및 복사에 대 한 리디렉션 도메인을 입력 합니다.는 **클라이언트 ID** 및 **클라이언트 암호** 프로젝트에 대 한 다음 클릭 **저장**:</span><span class="sxs-lookup"><span data-stu-id="c6fca-277">On the **API Settings** page for your application, enter the redirect domain for your application and copy the **Client ID** and **Client secret** for your project, and then click **Save**:</span></span>

    <span data-ttu-id="c6fca-278">[![](external-authentication-services/_static/image68.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image67.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-278">[![](external-authentication-services/_static/image68.png "Click to Expand the Image")](external-authentication-services/_static/image67.png)</span></span>

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="c6fca-279">로컬 등록을 사용 하지 않도록 선택 사항:</span><span class="sxs-lookup"><span data-stu-id="c6fca-279">Optional: Disable Local Registration</span></span>

<span data-ttu-id="c6fca-280">현재 ASP.NET 로컬 등록 기능 자동된 프로그램 (bot) 계정; 멤버를 만드는 하는 것을 금지 하지 않습니다. 예를 들어 봇 방지 및 유효성 검사와 같은 기술을 사용 하 여 [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-280">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="c6fca-281">이 인해 로그인 페이지에 로컬 로그인 폼과 등록 링크를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-281">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="c6fca-282">이 위해 엽니다는  *\_Login.cshtml* 프로젝트에서 페이지 한 다음 로컬 로그인 패널 및 등록 링크에 대 한 줄을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-282">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="c6fca-283">다음 코드 예제와 같은 결과 페이지와 같은 모습:</span><span class="sxs-lookup"><span data-stu-id="c6fca-283">The resulting page should like like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="c6fca-284">로컬 로그인 패널과 등록 링크가 비활성화 된 후 로그인 페이지에는 설정한 상태 여야 하는 외부 인증 공급자만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6fca-284">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

<span data-ttu-id="c6fca-285">[![](external-authentication-services/_static/image70.png "클릭 하 여 이미지를 확장 합니다.")](external-authentication-services/_static/image69.png)</span><span class="sxs-lookup"><span data-stu-id="c6fca-285">[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)</span></span>
