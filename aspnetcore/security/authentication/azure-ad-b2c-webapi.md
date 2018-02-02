---
title: "웹 Api와 Azure Active Directory B2C에에서 대 한 클라우드 인증"
author: camsoper
description: "ASP.NET Core 웹 API와 Azure Active Directory B2C 인증을 설정 하는 방법을 알아봅니다. 인증 된 웹 우체부를 사용 하 여 API를 테스트 합니다."
ms.author: casoper
manager: wpickett
ms.date: 01/25/2018
ms.topic: tutorial
ms.technology: aspnet
ms.prod: asp.net-core
ms.custom: mvc
uid: security/authentication/azure-ad-b2c-webapi
ms.openlocfilehash: a63bfc26bb6b0f5ea1c64641d6f57a3555d7f401
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="cloud-authentication-in-web-apis-with-azure-active-directory-b2c"></a><span data-ttu-id="fa2c9-104">웹 Api와 Azure Active Directory B2C에에서 대 한 클라우드 인증</span><span class="sxs-lookup"><span data-stu-id="fa2c9-104">Cloud authentication in web APIs with Azure Active Directory B2C</span></span>

<span data-ttu-id="fa2c9-105">작성자: [Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="fa2c9-105">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="fa2c9-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C)는 웹 및 모바일 앱에 대 한 클라우드 id 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) is a cloud identity management solution for web and mobile apps.</span></span> <span data-ttu-id="fa2c9-107">서비스는 클라우드 및 온-프레미스에서 호스트 되는 앱에 대 한 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-107">The service provides authentication for apps hosted in the cloud and on-premises.</span></span> <span data-ttu-id="fa2c9-108">인증 형식에는 엔터프라이즈 계정을 페더레이션 및 개별 계정, 소셜 네트워크 계정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-108">Authentication types include include individual accounts, social network accounts, and federated enterprise accounts.</span></span> <span data-ttu-id="fa2c9-109">또한 Azure AD B2C 최소 구성으로 다단계 인증을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-109">Additionally, Azure AD B2C can provide multi-factor authentication with minimal configuration.</span></span>

> [!TIP]
> <span data-ttu-id="fa2c9-110">Azure Active Directory (Azure AD) Azure AD B2C 별도 제품이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-110">Azure Active Directory (Azure AD) Azure AD B2C are separate product offerings.</span></span> <span data-ttu-id="fa2c9-111">Azure AD 테 넌 트 조직을 나타내고 Azure AD B2C 테 넌 트를 신뢰 당사자 응용 프로그램과 함께 사용할 id의 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-111">An Azure AD tenant represents an organization, while an Azure AD B2C tenant represents a collection of identities to be used with relying party applications.</span></span> <span data-ttu-id="fa2c9-112">자세한 내용은 참고 [Azure AD B2C: 질문과 대답 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-112">To learn more, see [Azure AD B2C: Frequently asked questions (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs).</span></span>

<span data-ttu-id="fa2c9-113">웹 Api에는 사용자 인터페이스가 없는, 이후 Azure AD B2C와 같은 보안 토큰 서비스에 사용자를 리디렉션할 수 있지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-113">Since web APIs have no user interface, they're unable to redirect the user to a secure token service like Azure AD B2C.</span></span> <span data-ttu-id="fa2c9-114">대신, API가 이미 Azure AD B2C를 사용 하 여 사용자를 인증 하는 호출 응용 프로그램에서 전달자 토큰을 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-114">Instead, the API is passed a bearer token from the calling app, which has already authenticated the user with Azure AD B2C.</span></span> <span data-ttu-id="fa2c9-115">다음 API를 직접 사용자 상호 작용 없이 토큰 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-115">The API then validates the token without direct user interaction.</span></span>

<span data-ttu-id="fa2c9-116">이 자습서에 설명 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="fa2c9-116">In this tutorial, learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fa2c9-117">Azure Active Directory B2C 테 넌 트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-117">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="fa2c9-118">Azure AD B2C에 Web API를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-118">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="fa2c9-119">인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 웹 API 키를 만들려면 Visual Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-119">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="fa2c9-120">Azure AD B2C 테 넌 트의 동작을 제어 하는 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-120">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="fa2c9-121">사용 하 여 우체부는 로그인 대화 상자를 표시 하는 웹 앱을 시뮬레이션 하는 토큰을 검색 하 고 web API에 대 한 요청을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-121">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa2c9-122">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="fa2c9-122">Prerequisites</span></span>

<span data-ttu-id="fa2c9-123">다음은이 연습에 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-123">The following are required for this walkthrough:</span></span>

* [<span data-ttu-id="fa2c9-124">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="fa2c9-124">Microsoft Azure subscription</span></span>](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* <span data-ttu-id="fa2c9-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (모든 버전)</span><span class="sxs-lookup"><span data-stu-id="fa2c9-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (any edition)</span></span>
* [<span data-ttu-id="fa2c9-126">Postman</span><span class="sxs-lookup"><span data-stu-id="fa2c9-126">Postman</span></span>](https://www.getpostman.com/postman)

## <a name="create-the-azure-active-directory-b2c-tenant"></a><span data-ttu-id="fa2c9-127">Azure Active Directory B2C 테 넌 트 만들기</span><span class="sxs-lookup"><span data-stu-id="fa2c9-127">Create the Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="fa2c9-128">Azure AD B2C 테 넌 트 만들기 [설명서에 설명 된 대로](/azure/active-directory-b2c/active-directory-b2c-get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-128">Create an Azure AD B2C tenant [as described in the documentation](/azure/active-directory-b2c/active-directory-b2c-get-started).</span></span> <span data-ttu-id="fa2c9-129">메시지가 표시 되 면 테 넌 트 Azure 구독과 연결 옵션인 경우이 자습서에 대 한</span><span class="sxs-lookup"><span data-stu-id="fa2c9-129">When prompted, associating the tenant with an Azure subscription is optional for this tutorial.</span></span>

## <a name="configure-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="fa2c9-130">등록 또는 로그인 시 정책 구성</span><span class="sxs-lookup"><span data-stu-id="fa2c9-130">Configure a sign-up or sign-in policy</span></span>

<span data-ttu-id="fa2c9-131">에 Azure AD B2C 설명서의 단계를 사용 하 여 [등록 또는 로그인 시 정책 만들기](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-131">Use the steps in the Azure AD B2C documentation to [create a sign-up or sign-in policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy).</span></span> <span data-ttu-id="fa2c9-132">정책 이름을 **SiUpIn**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-132">Name the policy **SiUpIn**.</span></span>  <span data-ttu-id="fa2c9-133">에 대 한 설명서에 제공 된 예제 값을 사용 하 여 **Id 공급자**, **등록 특성**, 및 **응용 프로그램 클레임**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-133">Use the example values provided in the documentation for **Identity providers**, **Sign-up attributes**, and **Application claims**.</span></span> <span data-ttu-id="fa2c9-134">사용 하 여 **지금 실행** 설명서에 설명 된 대로 정책을 테스트 하려면 단추는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-134">Using the **Run now** button to test the policy as described in the documentation is optional.</span></span>

## <a name="register-the-api-in-azure-ad-b2c"></a><span data-ttu-id="fa2c9-135">Azure AD B2C에 API를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-135">Register the API in Azure AD B2C</span></span>

<span data-ttu-id="fa2c9-136">새로 만든된 Azure AD B2C 테 넌 트에서 사용 하 여 API를 등록 [설명서에 나와 있는 단계](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api) 아래는 **web API 등록** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-136">In the newly created Azure AD B2C tenant, register your API using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api) under the **Register a web API** section.</span></span>

<span data-ttu-id="fa2c9-137">다음 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-137">Use the following values:</span></span>

| <span data-ttu-id="fa2c9-138">설정</span><span class="sxs-lookup"><span data-stu-id="fa2c9-138">Setting</span></span>                       | <span data-ttu-id="fa2c9-139">값</span><span class="sxs-lookup"><span data-stu-id="fa2c9-139">Value</span></span>               | <span data-ttu-id="fa2c9-140">노트</span><span class="sxs-lookup"><span data-stu-id="fa2c9-140">Notes</span></span>                                                                                  |
|-------------------------------|---------------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="fa2c9-141">**이름**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-141">**Name**</span></span>                      | <span data-ttu-id="fa2c9-142">*&lt;Api 앱 이름&gt;*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-142">*&lt;API name&gt;*</span></span>  | <span data-ttu-id="fa2c9-143">입력 한 **이름** 소비자에 게 앱을 설명 하는 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-143">Enter a **Name** for the app that describes your app to consumers.</span></span>                     |
| <span data-ttu-id="fa2c9-144">**웹 앱/웹 API**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-144">**Include web app / web API**</span></span> | <span data-ttu-id="fa2c9-145">예</span><span class="sxs-lookup"><span data-stu-id="fa2c9-145">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="fa2c9-146">**암시적 흐름 허용**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-146">**Allow implicit flow**</span></span>       | <span data-ttu-id="fa2c9-147">예</span><span class="sxs-lookup"><span data-stu-id="fa2c9-147">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="fa2c9-148">**회신 URL**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-148">**Reply URL**</span></span>                 | `https://localhost` | <span data-ttu-id="fa2c9-149">회신 Url은 Azure AD B2C 응용 프로그램을 요청 하는 모든 토큰을 반환 하는 위치 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-149">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> |
| <span data-ttu-id="fa2c9-150">**앱 ID URI**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-150">**App ID URI**</span></span>                | <span data-ttu-id="fa2c9-151">*api*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-151">*api*</span></span>               | <span data-ttu-id="fa2c9-152">URI는 실제 주소로 확인할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-152">The URI doesn't need to resolve to a physical address.</span></span> <span data-ttu-id="fa2c9-153">만 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-153">It only needs to be unique.</span></span>     |
| <span data-ttu-id="fa2c9-154">**네이티브 클라이언트를 포함 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-154">**Include native client**</span></span>     | <span data-ttu-id="fa2c9-155">아니요</span><span class="sxs-lookup"><span data-stu-id="fa2c9-155">No</span></span>                  |                                                                                        |

<span data-ttu-id="fa2c9-156">API를 등록 한 후 테 넌 트의 앱 및 Api의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-156">After the API is registered, the list of apps and APIs in the tenant is displayed.</span></span> <span data-ttu-id="fa2c9-157">방금 등록 된 API를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-157">Select the API that was just registered.</span></span> <span data-ttu-id="fa2c9-158">선택은 **복사** 아이콘의 오른쪽에는 **응용 프로그램 ID** 필드를 클립보드에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-158">Select the **Copy** icon to the right of the **Application ID** field to copy it to the clipboard.</span></span> <span data-ttu-id="fa2c9-159">선택 **범위 게시** 기본 확인 하 고 *user_impersonation* 범위가 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-159">Select **Published scopes** and verify the default *user_impersonation* scope is present.</span></span>

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a><span data-ttu-id="fa2c9-160">Visual Studio 2017에서 ASP.NET Core 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fa2c9-160">Create an ASP.NET Core app in Visual Studio 2017</span></span>

<span data-ttu-id="fa2c9-161">Visual Studio 웹 응용 프로그램 템플릿은 인증에 Azure AD B2C 테 넌 트를 사용 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-161">The Visual Studio Web Application template can be configured to use the Azure AD B2C tenant for authentication.</span></span>

<span data-ttu-id="fa2c9-162">Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-162">In Visual Studio:</span></span>

1. <span data-ttu-id="fa2c9-163">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-163">Create a new ASP.NET Core Web Application.</span></span> 
2. <span data-ttu-id="fa2c9-164">선택 **웹 API** 템플릿 목록에서.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-164">Select **Web API** from the list of templates.</span></span>
3. <span data-ttu-id="fa2c9-165">선택 된 **인증 변경** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-165">Select the **Change Authentication** button.</span></span>
    
    ![변경 인증 단추](./azure-ad-b2c-webapi/change-auth-button.png)

4. <span data-ttu-id="fa2c9-167">에 **인증 변경** 대화 상자에서 **개별 사용자 계정**를 선택한 후 **클라우드의 기존 사용자 저장소에 연결** 드롭다운에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-167">In the **Change Authentication** dialog, select **Individual User Accounts**, and then select **Connect to an existing user store in the cloud** in the dropdown.</span></span> 
    
    ![변경 인증 대화 상자](./azure-ad-b2c-webapi/change-auth-dialog.png)

5. <span data-ttu-id="fa2c9-169">다음 값을 갖는 양식을 작성 하 여:</span><span class="sxs-lookup"><span data-stu-id="fa2c9-169">Complete the form with the following values:</span></span>
    
    | <span data-ttu-id="fa2c9-170">설정</span><span class="sxs-lookup"><span data-stu-id="fa2c9-170">Setting</span></span>                       | <span data-ttu-id="fa2c9-171">값</span><span class="sxs-lookup"><span data-stu-id="fa2c9-171">Value</span></span>                                                 |
    |-------------------------------|-------------------------------------------------------|
    | <span data-ttu-id="fa2c9-172">**도메인 이름**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-172">**Domain Name**</span></span>               | <span data-ttu-id="fa2c9-173">*&lt;B2C 테 넌 트의 도메인 이름&gt;*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-173">*&lt;the domain name of your B2C tenant&gt;*</span></span>          |
    | <span data-ttu-id="fa2c9-174">**응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-174">**Application ID**</span></span>            | <span data-ttu-id="fa2c9-175">*&lt;클립보드의 응용 프로그램 ID를 붙여 넣습니다.&gt;*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-175">*&lt;paste the Application ID from the clipboard&gt;*</span></span> |
    | <span data-ttu-id="fa2c9-176">**등록 또는 로그인 시 정책**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-176">**Sign-up or sign-in policy**</span></span> | `B2C_1_SiUpIn`                                        |
    
    <span data-ttu-id="fa2c9-177">선택 **확인** 를 닫으려면는 **인증 변경** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-177">Select **OK** to close the **Change Authentication** dialog.</span></span> <span data-ttu-id="fa2c9-178">선택 **확인** 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-178">Select **OK** to create the web app.</span></span>

<span data-ttu-id="fa2c9-179">Visual Studio 라는 컨트롤러와 web API 만듭니다 *ValuesController.cs* GET 요청에 대 한 하드 코드 된 값을 반환 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-179">Visual Studio creates the web API with a controller named *ValuesController.cs* that returns hard-coded values for GET requests.</span></span> <span data-ttu-id="fa2c9-180">로 데코레이팅된 클래스의 [Authorize 특성](xref:security/authorization/simple)이므로 모든 요청 인증에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-180">The class is decorated with the [Authorize attribute](xref:security/authorization/simple), so all requests require authentication.</span></span>

## <a name="run-the-web-api"></a><span data-ttu-id="fa2c9-181">Web API를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-181">Run the web API</span></span>

<span data-ttu-id="fa2c9-182">Visual Studio에서 API를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-182">In Visual Studio, run the API.</span></span> <span data-ttu-id="fa2c9-183">Visual Studio는 API 루트 URL을 가리키는 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-183">Visual Studio launches a browser pointed at the API's root URL.</span></span> <span data-ttu-id="fa2c9-184">주소 표시줄에는 URL을 확인 하 고 백그라운드에서 실행 되는 API를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-184">Note the URL in the address bar, and leave the API running in the background.</span></span>

> [!NOTE]
> <span data-ttu-id="fa2c9-185">루트 URL에 대해 정의 된 컨트롤러 없음 이므로 브라우저 404 (찾을 수 없음 페이지) 오류를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-185">Since there is no controller defined for the root URL, the browser displays a 404 (page not found) error.</span></span> <span data-ttu-id="fa2c9-186">이는 예상된 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-186">This is expected behavior.</span></span>

## <a name="use-postman-to-get-a-token-and-test-the-api"></a><span data-ttu-id="fa2c9-187">우체부를 사용 하 여 테스트 하는 토큰을 가져오는 API</span><span class="sxs-lookup"><span data-stu-id="fa2c9-187">Use Postman to get a token and test the API</span></span>

<span data-ttu-id="fa2c9-188">[우체부](https://getpostman.com/postman) Api 웹 테스트를 위한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-188">[Postman](https://getpostman.com/postman) is a tool for testing web APIs.</span></span> <span data-ttu-id="fa2c9-189">이 자습서에서는 우체부는 사용자 대신 웹 API에 액세스 하는 웹 앱을 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-189">For this tutorial, Postman simulates a web app that accesses the web API on the user's behalf.</span></span>

### <a name="register-postman-as-a-web-app"></a><span data-ttu-id="fa2c9-190">웹 앱으로 우체부 등록</span><span class="sxs-lookup"><span data-stu-id="fa2c9-190">Register Postman as a web app</span></span>

<span data-ttu-id="fa2c9-191">Azure AD B2C 테 넌 트의 토큰을 얻을 수 있는 웹 앱을 시뮬레이션 하는 우체부, 이후 테 넌 트에서 웹 응용 프로그램으로 등록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-191">Since Postman simulates a web app that can obtain tokens from the Azure AD B2C tenant, it must be registered in the tenant as a web app.</span></span> <span data-ttu-id="fa2c9-192">사용 하 여 우체부 등록 [설명서에 나와 있는 단계](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) 아래는 **웹 앱 등록** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-192">Register Postman using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) under the **Register a web app** section.</span></span> <span data-ttu-id="fa2c9-193">중지 된 **웹 응용 프로그램 클라이언트 암호를 만들** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-193">Stop at the **Create a web app client secret** section.</span></span> <span data-ttu-id="fa2c9-194">이 자습서에 대 한 클라이언트 암호는 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-194">A client secret isn't required for this tutorial.</span></span> 

<span data-ttu-id="fa2c9-195">다음 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-195">Use the following values:</span></span>

| <span data-ttu-id="fa2c9-196">설정</span><span class="sxs-lookup"><span data-stu-id="fa2c9-196">Setting</span></span>                       | <span data-ttu-id="fa2c9-197">값</span><span class="sxs-lookup"><span data-stu-id="fa2c9-197">Value</span></span>                            | <span data-ttu-id="fa2c9-198">노트</span><span class="sxs-lookup"><span data-stu-id="fa2c9-198">Notes</span></span>                           |
|-------------------------------|----------------------------------|---------------------------------|
| <span data-ttu-id="fa2c9-199">**이름**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-199">**Name**</span></span>                      | <span data-ttu-id="fa2c9-200">우체부</span><span class="sxs-lookup"><span data-stu-id="fa2c9-200">Postman</span></span>                          |                                 |
| <span data-ttu-id="fa2c9-201">**웹 앱/웹 API**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-201">**Include web app / web API**</span></span> | <span data-ttu-id="fa2c9-202">예</span><span class="sxs-lookup"><span data-stu-id="fa2c9-202">Yes</span></span>                              |                                 |
| <span data-ttu-id="fa2c9-203">**암시적 흐름 허용**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-203">**Allow implicit flow**</span></span>       | <span data-ttu-id="fa2c9-204">예</span><span class="sxs-lookup"><span data-stu-id="fa2c9-204">Yes</span></span>                              |                                 |
| <span data-ttu-id="fa2c9-205">**회신 URL**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-205">**Reply URL**</span></span>                 | `https://getpostman.com/postman` |                                 |
| <span data-ttu-id="fa2c9-206">**앱 ID URI**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-206">**App ID URI**</span></span>                | <span data-ttu-id="fa2c9-207">*&lt;비워&gt;*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-207">*&lt;leave blank&gt;*</span></span>            | <span data-ttu-id="fa2c9-208">이 자습서에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-208">Not required for this tutorial.</span></span> |
| <span data-ttu-id="fa2c9-209">**네이티브 클라이언트를 포함 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-209">**Include native client**</span></span>     | <span data-ttu-id="fa2c9-210">아니요</span><span class="sxs-lookup"><span data-stu-id="fa2c9-210">No</span></span>                               |                                 |

<span data-ttu-id="fa2c9-211">새로 등록 된 웹 응용 프로그램에서 사용자 대신 web API에 액세스할 수 있는 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-211">The newly registered web app needs permission to access the web API on the user's behalf.</span></span>  

1. <span data-ttu-id="fa2c9-212">선택 **우체부** 앱 선택한 후 목록에서 **API 액세스** 왼쪽 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-212">Select **Postman** in the list of apps and then select **API access** from the menu on the left.</span></span>
2. <span data-ttu-id="fa2c9-213">선택 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-213">Select **+ Add**.</span></span>
3. <span data-ttu-id="fa2c9-214">에 **API 선택** 드롭다운에서 web API의 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-214">In the **Select API** dropdown, select the name of the web API.</span></span>
4. <span data-ttu-id="fa2c9-215">에 **선택 범위** 드롭다운에서 모든 범위가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-215">In the **Select Scopes** dropdown, ensure all scopes are selected.</span></span>
5. <span data-ttu-id="fa2c9-216">선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-216">Select **Ok**.</span></span>

<span data-ttu-id="fa2c9-217">전달자 토큰을 가져오는 데 필요한 것 처럼 우체부 응용 프로그램의 응용 프로그램 ID, note 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-217">Note the Postman app's Application ID, as it's required to obtain a bearer token.</span></span>

### <a name="create-a-postman-request"></a><span data-ttu-id="fa2c9-218">우체부 요청 만들기</span><span class="sxs-lookup"><span data-stu-id="fa2c9-218">Create a Postman request</span></span>

<span data-ttu-id="fa2c9-219">우체부를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-219">Launch Postman.</span></span> <span data-ttu-id="fa2c9-220">기본적으로 우체부 표시는 **새로 만들기** 대화 시작 시.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-220">By default, Postman displays the **Create New** dialog upon launching.</span></span> <span data-ttu-id="fa2c9-221">대화 상자 표시 되어 있지 않으면 선택 된 **+ 새로 만들기** 왼쪽 위에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-221">If the dialog isn't displayed, select the **+ New** button in the upper left.</span></span>

<span data-ttu-id="fa2c9-222">**새로 만들기** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="fa2c9-222">From the **Create New** dialog:</span></span>

1. <span data-ttu-id="fa2c9-223">선택 **요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-223">Select **Request**.</span></span>
    
    ![요청 단추](./azure-ad-b2c-webapi/postman-create-new.png)

2. <span data-ttu-id="fa2c9-225">입력 *값 가져오기* 에 **요청 이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-225">Enter *Get Values* in the **Request name** box.</span></span>
3. <span data-ttu-id="fa2c9-226">선택 **+ 모음 만들기** 요청을 저장 하기 위한 새 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-226">Select **+ Create Collection** to create a new collection for storing the request.</span></span> <span data-ttu-id="fa2c9-227">컬렉션 이름을 *ASP.NET Core 자습서* 한 다음 확인 표시를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-227">Name the collection *ASP.NET Core tutorials* and then select the checkmark.</span></span>
    
    ![새 컬렉션 만들기](./azure-ad-b2c-webapi/postman-create-collection.png)

4. <span data-ttu-id="fa2c9-229">선택 된 **ASP.NET Core 자습서로 저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-229">Select the **Save to ASP.NET Core tutorials** button.</span></span>

### <a name="test-the-web-api-withoutauthentication"></a><span data-ttu-id="fa2c9-230">Web API withoutauthentication 테스트</span><span class="sxs-lookup"><span data-stu-id="fa2c9-230">Test the web API withoutauthentication</span></span>

<span data-ttu-id="fa2c9-231">웹 API에 인증이 필요한을 확인 하려면 먼저 인증 없이 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-231">To verify that the web API requires authentication, first make a request without authentication.</span></span>

1. <span data-ttu-id="fa2c9-232">에 **요청 URL을 입력** 상자에 대 한 URL을 입력 합니다 `ValuesController`합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-232">In the **Enter request URL** box, enter the URL for `ValuesController`.</span></span> <span data-ttu-id="fa2c9-233">URL이 사용 하 여 브라우저에 표시 된 것과 동일 **api/값** 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-233">The URL is the same as displayed in the browser with **api/values** appended.</span></span> <span data-ttu-id="fa2c9-234">예를 들어 `https://localhost:44375/api/values`합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-234">An example would be `https://localhost:44375/api/values`.</span></span>
2. <span data-ttu-id="fa2c9-235">선택 된 **보낼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-235">Select the **Send** button.</span></span>
3. <span data-ttu-id="fa2c9-236">응답의 상태는 *401 권한 없음*합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-236">Note the status of the response is *401 Unauthorized*.</span></span>

    ![401 권한 없는 응답](./azure-ad-b2c-webapi/postman-401-status.png)

### <a name="obtain-a-bearer-token"></a><span data-ttu-id="fa2c9-238">전달자 토큰을 가져올</span><span class="sxs-lookup"><span data-stu-id="fa2c9-238">Obtain a bearer token</span></span>

<span data-ttu-id="fa2c9-239">Web API에 인증 된 요청을 하려면 전달자 토큰은 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-239">To make an authenticated request to the web API, a bearer token is required.</span></span> <span data-ttu-id="fa2c9-240">우체부를 통해 Azure AD B2C 테 넌 트에 로그인 하 고 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-240">Postman makes it easy to sign in to the Azure AD B2C tenant and obtain a token.</span></span>

1. <span data-ttu-id="fa2c9-241">에 **권한 부여** 탭에 **형식** 드롭다운 **OAuth 2.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-241">On the **Authorization** tab, in the **TYPE** dropdown, select **OAuth 2.0**.</span></span> <span data-ttu-id="fa2c9-242">에 **권한 부여 데이터를 추가할** 드롭다운 **요청 헤더**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-242">In the **Add authorization data to** dropdown, select **Request Headers**.</span></span> <span data-ttu-id="fa2c9-243">선택 **새 액세스 토큰 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-243">Select **Get New Access Token**.</span></span>
    
    ![설정 사용 하 여 권한 부여 탭](./azure-ad-b2c-webapi/postman-auth-tab.png)

2. <span data-ttu-id="fa2c9-245">완료 된 **새 액세스 토큰 가져오기** 다음과 같이 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="fa2c9-245">Complete the **GET NEW ACCESS TOKEN** dialog as follows:</span></span>
    
    | <span data-ttu-id="fa2c9-246">설정</span><span class="sxs-lookup"><span data-stu-id="fa2c9-246">Setting</span></span>                   | <span data-ttu-id="fa2c9-247">값</span><span class="sxs-lookup"><span data-stu-id="fa2c9-247">Value</span></span>                                                                                         | <span data-ttu-id="fa2c9-248">노트</span><span class="sxs-lookup"><span data-stu-id="fa2c9-248">Notes</span></span>                                                                                      |
    |---------------------------|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
    | <span data-ttu-id="fa2c9-249">**토큰 이름**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-249">**Token Name**</span></span>            | <span data-ttu-id="fa2c9-250">*&lt;토큰 이름&gt;*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-250">*&lt;token name&gt;*</span></span>                                                                          | <span data-ttu-id="fa2c9-251">토큰에 대 한 설명이 포함 된 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-251">Enter a descriptive name for the token.</span></span>                                                    |
    | <span data-ttu-id="fa2c9-252">**Grant 유형**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-252">**Grant Type**</span></span>            | <span data-ttu-id="fa2c9-253">암시적 방법</span><span class="sxs-lookup"><span data-stu-id="fa2c9-253">Implicit</span></span>                                                                                      |                                                                                            |
    | <span data-ttu-id="fa2c9-254">**콜백 URL**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-254">**Callback URL**</span></span>          | `https://getpostman.com/postman`                                                              |                                                                                            |
    | <span data-ttu-id="fa2c9-255">**인증 URL**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-255">**Auth URL**</span></span>              | `https://login.microsoftonline.com/<tenant domain name>/oauth2/v2.0/authorize?p=B2C_1_SiUpIn` | <span data-ttu-id="fa2c9-256">대체  *&lt;테 넌 트 도메인 이름&gt;*  꺾쇠 괄호 없이 테 넌 트의 도메인 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-256">Replace *&lt;tenant domain name&gt;* with the tenant's domain name without angle brackets.</span></span> |
    | <span data-ttu-id="fa2c9-257">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-257">**Client ID**</span></span>             | <span data-ttu-id="fa2c9-258">*&lt;우체부 응용 프로그램의 입력 <b>응용 프로그램 ID</b>&gt;*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-258">*&lt;enter the Postman app's <b>Application ID</b>&gt;*</span></span>                                       |                                                                                            |
    | <span data-ttu-id="fa2c9-259">**클라이언트 암호**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-259">**Client Secret**</span></span>         | <span data-ttu-id="fa2c9-260">*&lt;비워&gt;*</span><span class="sxs-lookup"><span data-stu-id="fa2c9-260">*&lt;leave blank&gt;*</span></span>                                                                         |                                                                                            |
    | <span data-ttu-id="fa2c9-261">**범위**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-261">**Scope**</span></span>                 | `https://<tenant domain name>/api/user_impersonation openid offline_access`                   | <span data-ttu-id="fa2c9-262">대체  *&lt;테 넌 트 도메인 이름&gt;*  꺾쇠 괄호 없이 테 넌 트의 도메인 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-262">Replace *&lt;tenant domain name&gt;* with the tenant's domain name without angle brackets.</span></span> |
    | <span data-ttu-id="fa2c9-263">**클라이언트 인증**</span><span class="sxs-lookup"><span data-stu-id="fa2c9-263">**Client Authentication**</span></span> | <span data-ttu-id="fa2c9-264">본문에 클라이언트 자격 증명 보내기</span><span class="sxs-lookup"><span data-stu-id="fa2c9-264">Send client credentials in body</span></span>                                                               |                                                                                            |
    
3. <span data-ttu-id="fa2c9-265">선택 된 **토큰 요청** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-265">Select the **Request Token** button.</span></span>

4. <span data-ttu-id="fa2c9-266">우체부 대화 상자에서 Azure AD B2C 테 넌 트의 기호를 포함 하는 새 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-266">Postman opens a new window containing the Azure AD B2C tenant's sign in dialog.</span></span> <span data-ttu-id="fa2c9-267">(하나는 정책을 테스트 생성) 하는 경우 기존 계정으로 로그인 하거나 선택 **지금 등록** 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-267">Sign in with an existing account (if one was created testing the policies) or select **Sign up now** to create a new account.</span></span> <span data-ttu-id="fa2c9-268">**암호를 잊으셨습니까?** 링크는 잊어버린된 암호를 재설정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-268">The **Forgot your password?** link is used to reset a forgotten password.</span></span>

5. <span data-ttu-id="fa2c9-269">성공적으로 로그인 한 후 창이 닫히고 및 **관리 액세스 토큰** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-269">After successfully signing in, the window closes and the **MANAGE ACCESS TOKENS** dialog appears.</span></span> <span data-ttu-id="fa2c9-270">선택 되며 맨 아래까지 아래로 스크롤합니다는 **사용 토큰** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-270">Scroll down to the bottom and select the **Use Token** button.</span></span>
    
    !["토큰 사용" 단추를 찾을 수 있는 위치](./azure-ad-b2c-webapi/postman-access-token.png)

### <a name="test-the-web-api-with-authentication"></a><span data-ttu-id="fa2c9-272">인증을 사용 하 여 웹 API를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-272">Test the web API with authentication</span></span>

<span data-ttu-id="fa2c9-273">선택의 **보낼** 단추 요청을 다시 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-273">Select the **Send** button to send the request again.</span></span> <span data-ttu-id="fa2c9-274">이 경우 응답 상태는 *200 확인* JSON 페이로드는 응답에 표시 되 고 **본문** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-274">This time, the response status is *200 OK* and the JSON payload is visible on the response **Body** tab.</span></span>
    
![페이로드 및 성공 상태](./azure-ad-b2c-webapi/postman-success.png)

## <a name="next-steps"></a><span data-ttu-id="fa2c9-276">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fa2c9-276">Next steps</span></span>

<span data-ttu-id="fa2c9-277">이 자습서에서는 다음 방법을 학습했습니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-277">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fa2c9-278">Azure Active Directory B2C 테 넌 트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-278">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="fa2c9-279">Azure AD B2C에 Web API를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-279">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="fa2c9-280">인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 웹 API 키를 만들려면 Visual Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-280">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="fa2c9-281">Azure AD B2C 테 넌 트의 동작을 제어 하는 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-281">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="fa2c9-282">사용 하 여 우체부는 로그인 대화 상자를 표시 하는 웹 앱을 시뮬레이션 하는 토큰을 검색 하 고 web API에 대 한 요청을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-282">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

<span data-ttu-id="fa2c9-283">학습 하 여 API 개발을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-283">Continue developing your API by learning to:</span></span>

* <span data-ttu-id="fa2c9-284">[ASP.NET Core 웹 앱을 Azure AD B2C를 사용 하 여 보안](xref:security/authentication/azure-ad-b2c)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-284">[Secure an ASP.NET Core web app using Azure AD B2C](xref:security/authentication/azure-ad-b2c).</span></span>
* <span data-ttu-id="fa2c9-285">[Azure AD B2C를 사용 하 여.NET 웹 앱에서.NET web API를 호출](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-285">[Call a .NET web API from a .NET web app using Azure AD B2C](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet).</span></span>
* <span data-ttu-id="fa2c9-286">[Azure AD B2C 사용자 인터페이스 사용자 지정](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-286">[Customize the Azure AD B2C user interface](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization).</span></span>
* <span data-ttu-id="fa2c9-287">[암호 복잡성 요구 사항을 구성](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-287">[Configure password complexity requirements](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity).</span></span>
* <span data-ttu-id="fa2c9-288">[Multi-factor authentication 사용](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-288">[Enable multi-factor authentication](/azure/active-directory-b2c/active-directory-b2c-reference-mfa).</span></span>
* <span data-ttu-id="fa2c9-289">추가 id 공급자와 같은 구성 [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter ](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), 등입니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-289">Configure additional identity providers, such as [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), and others.</span></span>
* <span data-ttu-id="fa2c9-290">[Azure AD Graph API를 사용 하 여](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) Azure AD B2C 테 넌 트에서 그룹 구성원 자격 등의 추가 사용자 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa2c9-290">[Use the Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) to retrieve additional user information, such as group membership, from the Azure AD B2C tenant.</span></span>