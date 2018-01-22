---
title: "클라우드 인증을 Azure Active Directory B2C"
author: camsoper
description: "ASP.NET Core와 Azure Active Directory B2C 인증을 설정 하는 방법을 알아봅니다."
ms.author: casoper
manager: wpickett
ms.date: 01/12/2018
ms.topic: tutorial
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/azure-ad-b2c
custom: mvc
ms.openlocfilehash: 5c4716022c61e33b0301fa0077f911dcc4b3628c
ms.sourcegitcommit: 459cb3289741a3f46325e605a617dc926ee0563d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2018
---
# <a name="cloud-authentication-with-azure-active-directory-b2c"></a><span data-ttu-id="a095a-103">클라우드 인증을 Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="a095a-103">Cloud authentication with Azure Active Directory B2C</span></span>

<span data-ttu-id="a095a-104">작성자: [Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="a095a-104">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="a095a-105">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C)는 웹 및 모바일 앱에 대 한 클라우드 id 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-105">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) is a cloud identity management solution for your web and mobile apps.</span></span> <span data-ttu-id="a095a-106">서비스는 클라우드 및 온-프레미스에서 호스트 되는 앱에 대 한 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-106">The service provides authentication for apps hosted in the cloud and on-premises.</span></span> <span data-ttu-id="a095a-107">인증 형식에는 엔터프라이즈 계정을 페더레이션 및 개별 계정, 소셜 네트워크 계정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-107">Authentication types include include individual accounts, social network accounts, and federated enterprise accounts.</span></span>  <span data-ttu-id="a095a-108">또한 Azure AD B2C 최소 구성으로 다단계 인증을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-108">Additionally, Azure AD B2C can provide multi-factor authentication with minimal configuration.</span></span>

<span data-ttu-id="a095a-109">이 자습서에 설명 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="a095a-109">In this tutorial, learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a095a-110">Azure Active Directory B2C 테 넌 트 만들기</span><span class="sxs-lookup"><span data-stu-id="a095a-110">Create an Azure Active Directory B2C tenant</span></span>
> * <span data-ttu-id="a095a-111">Azure AD B2C에 앱을 등록</span><span class="sxs-lookup"><span data-stu-id="a095a-111">Register an app in Azure AD B2C</span></span>
> * <span data-ttu-id="a095a-112">Visual Studio를 사용 하 여 인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 ASP.NET Core 웹 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="a095a-112">Use Visual Studio to create an ASP.NET Core web app configured to use the Azure AD B2C tenant for authentication</span></span>
> * <span data-ttu-id="a095a-113">Azure AD B2C 테 넌 트의 동작을 제어 하는 정책 구성</span><span class="sxs-lookup"><span data-stu-id="a095a-113">Configure policies controlling the behavior of the Azure AD B2C tenant</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a095a-114">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a095a-114">Prerequisites</span></span>

<span data-ttu-id="a095a-115">다음은이 연습에 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-115">The following are required for this walkthrough:</span></span>

* <span data-ttu-id="a095a-116">[Microsoft Azure 구독](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-116">[Microsoft Azure subscription](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span></span> 
* <span data-ttu-id="a095a-117">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (모든 버전)</span><span class="sxs-lookup"><span data-stu-id="a095a-117">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (any edition)</span></span>

## <a name="create-the-azure-active-directory-b2c-tenant"></a><span data-ttu-id="a095a-118">Azure Active Directory B2C 테 넌 트 만들기</span><span class="sxs-lookup"><span data-stu-id="a095a-118">Create the Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="a095a-119">Azure Active Directory B2C 테 넌 트 만들기 [설명서에 설명 된 대로](/azure/active-directory-b2c/active-directory-b2c-get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-119">Create an Azure Active Directory B2C tenant [as described in the documentation](/azure/active-directory-b2c/active-directory-b2c-get-started).</span></span> <span data-ttu-id="a095a-120">메시지가 표시 되 면 테 넌 트 Azure 구독과 연결 옵션인 경우이 자습서에 대 한</span><span class="sxs-lookup"><span data-stu-id="a095a-120">When prompted, associating the tenant with an Azure subscription is optional for this tutorial.</span></span>

## <a name="register-the-app-in-azure-ad-b2c"></a><span data-ttu-id="a095a-121">Azure AD B2C에 응용 프로그램을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-121">Register the app in Azure AD B2C</span></span>

<span data-ttu-id="a095a-122">새로 만든된 Azure AD B2C 테 넌 트에서 사용 하 여 앱을 등록 [설명서에 나와 있는 단계](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) 아래는 **웹 앱 등록** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a095a-122">In the newly created Azure AD B2C tenant, register your app using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) under the **Register a web app** section.</span></span> <span data-ttu-id="a095a-123">중지 된 **웹 응용 프로그램 클라이언트 암호를 만들** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a095a-123">Stop at the **Create a web app client secret** section.</span></span> <span data-ttu-id="a095a-124">이 자습서에 대 한 클라이언트 암호는 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-124">A client secret isn't required for this tutorial.</span></span> 

<span data-ttu-id="a095a-125">다음 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-125">Use the following values:</span></span>

| <span data-ttu-id="a095a-126">설정</span><span class="sxs-lookup"><span data-stu-id="a095a-126">Setting</span></span>                       | <span data-ttu-id="a095a-127">값</span><span class="sxs-lookup"><span data-stu-id="a095a-127">Value</span></span>                     | <span data-ttu-id="a095a-128">노트</span><span class="sxs-lookup"><span data-stu-id="a095a-128">Notes</span></span>                                                                                                                                                                                              |
|-------------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a095a-129">**이름**</span><span class="sxs-lookup"><span data-stu-id="a095a-129">**Name**</span></span>                      | <span data-ttu-id="a095a-130">*\<응용 프로그램 이름\>*</span><span class="sxs-lookup"><span data-stu-id="a095a-130">*\<app name\>*</span></span>            | <span data-ttu-id="a095a-131">입력 한 **이름** 소비자에 게 앱을 설명 하는 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-131">Enter a **Name** for the app that describes your app to consumers.</span></span>                                                                                                                                 |
| <span data-ttu-id="a095a-132">**웹 앱/웹 API**</span><span class="sxs-lookup"><span data-stu-id="a095a-132">**Include web app / web API**</span></span> | <span data-ttu-id="a095a-133">예</span><span class="sxs-lookup"><span data-stu-id="a095a-133">Yes</span></span>                       |                                                                                                                                                                                                    |
| <span data-ttu-id="a095a-134">**암시적 흐름 허용**</span><span class="sxs-lookup"><span data-stu-id="a095a-134">**Allow implicit flow**</span></span>       | <span data-ttu-id="a095a-135">예</span><span class="sxs-lookup"><span data-stu-id="a095a-135">Yes</span></span>                       |                                                                                                                                                                                                    |
| <span data-ttu-id="a095a-136">**회신 URL**</span><span class="sxs-lookup"><span data-stu-id="a095a-136">**Reply URL**</span></span>                 | `https://localhost:44300` | <span data-ttu-id="a095a-137">회신 Url은 Azure AD B2C 응용 프로그램을 요청 하는 모든 토큰을 반환 하는 위치 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-137">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> <span data-ttu-id="a095a-138">Visual Studio를 사용 하 여 회신 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-138">Visual Studio provides the Reply URL to use.</span></span> <span data-ttu-id="a095a-139">지금은 입력 `https://localhost:44300` 양식을 완성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-139">For now, enter `https://localhost:44300` to complete the form.</span></span> |
| <span data-ttu-id="a095a-140">**앱 ID URI**</span><span class="sxs-lookup"><span data-stu-id="a095a-140">**App ID URI**</span></span>                | <span data-ttu-id="a095a-141">비워</span><span class="sxs-lookup"><span data-stu-id="a095a-141">Leave blank</span></span>               | <span data-ttu-id="a095a-142">이 자습서에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-142">Not required for this tutorial.</span></span>                                                                                                                                                                    |
| <span data-ttu-id="a095a-143">**네이티브 클라이언트를 포함 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a095a-143">**Include native client**</span></span>     | <span data-ttu-id="a095a-144">아니요</span><span class="sxs-lookup"><span data-stu-id="a095a-144">No</span></span>                        |                                                                                                                                                                                                    |

> [!WARNING]
> <span data-ttu-id="a095a-145">경우 고려해 야 localhost가 아닌 회신 URL을 설정는 [회신 URL 목록에 허용 되는 제약 조건을](/azure/active-directory-b2c/active-directory-b2c-app-registration#choosing-a-web-app-or-api-reply-url)합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-145">If setting up a non-localhost Reply URL, be aware of the [constraints on what is allowed in the Reply URL list](/azure/active-directory-b2c/active-directory-b2c-app-registration#choosing-a-web-app-or-api-reply-url).</span></span> 

<span data-ttu-id="a095a-146">앱을 등록 한 후 테 넌 트에 있는 앱의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-146">After the app is registered, the list of apps in the tenant is displayed.</span></span> <span data-ttu-id="a095a-147">방금 등록 된 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-147">Select the app that was just registered.</span></span> <span data-ttu-id="a095a-148">선택 된 **복사** 아이콘의 오른쪽에는 **응용 프로그램 ID** 응용 프로그램 ID를 클립보드에 복사 하려면 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-148">Select the **Copy** icon to the right of the **Application ID** field to copy the Application ID to the clipboard.</span></span>

<span data-ttu-id="a095a-149">아무 것도 더 이번에 Azure AD B2C 테 넌 트에 구성할 수 있지만 브라우저 창을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-149">Nothing more can be configured in the Azure AD B2C tenant at this time, but leave the browser window open.</span></span> <span data-ttu-id="a095a-150">ASP.NET Core 응용 프로그램을 만든 후 더 복잡 한 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-150">There is more configuration after the ASP.NET Core app is created.</span></span>

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a><span data-ttu-id="a095a-151">Visual Studio 2017에서 ASP.NET Core 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a095a-151">Create an ASP.NET Core app in Visual Studio 2017</span></span>

<span data-ttu-id="a095a-152">Visual Studio 웹 응용 프로그램 템플릿은 인증에 Azure AD B2C 테 넌 트를 사용 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-152">The Visual Studio Web Application template can be configured to use the Azure AD B2C tenant for authentication.</span></span>

<span data-ttu-id="a095a-153">Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-153">In Visual Studio:</span></span>

1. <span data-ttu-id="a095a-154">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-154">Create a new ASP.NET Core Web Application.</span></span> 
2. <span data-ttu-id="a095a-155">선택 **웹 응용 프로그램** 템플릿 목록에서.</span><span class="sxs-lookup"><span data-stu-id="a095a-155">Select **Web Application** from the list of templates.</span></span>
3. <span data-ttu-id="a095a-156">선택 된 **인증 변경** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-156">Select the **Change Authentication** button.</span></span>
    
    ![변경 인증 단추](./azure-ad-b2c/_static/changeauth.png)

4. <span data-ttu-id="a095a-158">에 **인증 변경** 대화 상자에서 **개별 사용자 계정**를 선택한 후 **클라우드의 기존 사용자 저장소에 연결** 드롭다운에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-158">In the **Change Authentication** dialog, select **Individual User Accounts**, and then select **Connect to an existing user store in the cloud** in the dropdown.</span></span> 
    
    ![변경 인증 대화 상자](./azure-ad-b2c/_static/changeauthdialog.png)

5. <span data-ttu-id="a095a-160">다음 값을 갖는 양식을 작성 하 여:</span><span class="sxs-lookup"><span data-stu-id="a095a-160">Complete the form with the following values:</span></span>
    
    | <span data-ttu-id="a095a-161">설정</span><span class="sxs-lookup"><span data-stu-id="a095a-161">Setting</span></span>                       | <span data-ttu-id="a095a-162">값</span><span class="sxs-lookup"><span data-stu-id="a095a-162">Value</span></span>                                             |
    |-------------------------------|---------------------------------------------------|
    | <span data-ttu-id="a095a-163">**도메인 이름**</span><span class="sxs-lookup"><span data-stu-id="a095a-163">**Domain Name**</span></span>               | <span data-ttu-id="a095a-164">*\<B2C 테 넌 트의 도메인 이름\>*</span><span class="sxs-lookup"><span data-stu-id="a095a-164">*\<the domain name of your B2C tenant\>*</span></span>          |
    | <span data-ttu-id="a095a-165">**응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="a095a-165">**Application ID**</span></span>            | <span data-ttu-id="a095a-166">*\<클립보드의 응용 프로그램 ID를 붙여 넣습니다.\>*</span><span class="sxs-lookup"><span data-stu-id="a095a-166">*\<paste the Application ID from the clipboard\>*</span></span> |
    | <span data-ttu-id="a095a-167">**콜백 경로**</span><span class="sxs-lookup"><span data-stu-id="a095a-167">**Callback Path**</span></span>             | <span data-ttu-id="a095a-168">*\<기본값을 사용 하 여\>*</span><span class="sxs-lookup"><span data-stu-id="a095a-168">*\<use the default value\>*</span></span>                       |
    | <span data-ttu-id="a095a-169">**등록 또는 로그인 시 정책**</span><span class="sxs-lookup"><span data-stu-id="a095a-169">**Sign-up or sign-in policy**</span></span> | `B2C_1_SiUpIn`                                    |
    | <span data-ttu-id="a095a-170">**암호 재설정 정책**</span><span class="sxs-lookup"><span data-stu-id="a095a-170">**Reset password policy**</span></span>     | `B2C_1_SSPR`                                      |
    | <span data-ttu-id="a095a-171">**프로필 정책 편집**</span><span class="sxs-lookup"><span data-stu-id="a095a-171">**Edit profile policy**</span></span>       | <span data-ttu-id="a095a-172">*\<비워\>*</span><span class="sxs-lookup"><span data-stu-id="a095a-172">*\<leave blank\>*</span></span>                                 |

    <span data-ttu-id="a095a-173">선택의 **복사** 옆에 연결 **회신 URI** 회신 URI를 클립보드에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-173">Select the **Copy** link next to **Reply URI** to copy the Reply URI to the clipboard.</span></span> <span data-ttu-id="a095a-174">선택 **확인** 를 닫으려면는 **인증 변경** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a095a-174">Select **OK** to close the **Change Authentication** dialog.</span></span> <span data-ttu-id="a095a-175">선택 **확인** 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-175">Select **OK** to create the web app.</span></span>

## <a name="finish-the-b2c-app-registration"></a><span data-ttu-id="a095a-176">B2C 앱 등록 완료</span><span class="sxs-lookup"><span data-stu-id="a095a-176">Finish the B2C app registration</span></span>

<span data-ttu-id="a095a-177">B2C 앱 속성이 계속 열려 있는 브라우저 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-177">Return to the browser window with the B2C app properties still open.</span></span> <span data-ttu-id="a095a-178">임시 변경 **회신 URL** Visual Studio에서 복사한 이전 값으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-178">Change the temporary **Reply URL** specified earlier to the value copied from Visual Studio.</span></span> <span data-ttu-id="a095a-179">선택 **저장** 창의 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-179">Select **Save** at the top of the window.</span></span>

> [!TIP]
> <span data-ttu-id="a095a-180">회신 URL을 복사 하지 않은 웹 프로젝트 속성의 디버그 탭에서 SSL 주소를 사용 하 고 추가 **CallbackPath** 에서 값 *appsettings.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-180">If you didn't copy the Reply URL, use the SSL address from the Debug tab in the web project properties, and append the **CallbackPath** value from *appsettings.json*.</span></span>

## <a name="configure-policies"></a><span data-ttu-id="a095a-181">정책 구성</span><span class="sxs-lookup"><span data-stu-id="a095a-181">Configure policies</span></span>

<span data-ttu-id="a095a-182">에 Azure AD B2C 설명서의 단계를 사용 [등록 또는 로그인 시 정책 만들기](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy), 차례로 [암호 재설정 정책 만들기](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-password-reset-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-182">Use the steps in the Azure AD B2C documentation to [create a sign-up or sign-in policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy), and then [create a password reset policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-password-reset-policy).</span></span> <span data-ttu-id="a095a-183">에 대 한 설명서에 제공 된 예제 값을 사용 하 여 **Id 공급자**, **등록 특성**, 및 **응용 프로그램 클레임**합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-183">Use the example values provided in the documentation for **Identity providers**, **Sign-up attributes**, and **Application claims**.</span></span> <span data-ttu-id="a095a-184">사용 하 여 **지금 실행** 설명서에 설명 된 대로 정책을 테스트 하려면 단추는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-184">Using the **Run now** button to test the policies as described in the documentation is optional.</span></span>

> [!WARNING]
> <span data-ttu-id="a095a-185">정책 이름에 해당 정책을 사용한 같이 문서에 설명 된 대로 정확 하 게이 확인은 **인증 변경** Visual Studio에서 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a095a-185">Ensure the policy names are exactly as described in the documentation, as those policies were used in the **Change Authentication** dialog in Visual Studio.</span></span> <span data-ttu-id="a095a-186">정책 이름을 확인할 수 있습니다 *appsettings.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-186">The policy names can be verified in *appsettings.json*.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="a095a-187">앱 실행</span><span class="sxs-lookup"><span data-stu-id="a095a-187">Run the app</span></span>

<span data-ttu-id="a095a-188">키를 눌러 Visual Studio에서 **F5** 작성 하 고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-188">In Visual Studio, press **F5** to build and run the app.</span></span> <span data-ttu-id="a095a-189">웹 앱이 시작 된 후에 선택 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-189">After the web app launches, select **Sign in**.</span></span>

![응용 프로그램에 로그인](./azure-ad-b2c/_static/signin.png)

<span data-ttu-id="a095a-191">브라우저에서 Azure AD B2C 테 넌 트에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-191">The browser redirects to the Azure AD B2C tenant.</span></span> <span data-ttu-id="a095a-192">(하나는 정책을 테스트 생성) 하는 경우 기존 계정으로 로그인 하거나 선택 **지금 등록** 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-192">Sign in with an existing account (if one was created testing the policies) or select **Sign up now** to create a new account.</span></span> <span data-ttu-id="a095a-193">**암호를 잊으셨습니까?** 링크는 잊어버린된 암호를 재설정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-193">The **Forgot your password?** link is used to reset a forgotten password.</span></span>

![Azure AD B2C 로그인](./azure-ad-b2c/_static/b2csts.png)

<span data-ttu-id="a095a-195">성공적으로 로그인 한 후 브라우저에서 웹 앱으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-195">After successfully signing in, the browser redirects to the web app.</span></span>

![성공](./azure-ad-b2c/_static/success.png)

## <a name="next-steps"></a><span data-ttu-id="a095a-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a095a-197">Next steps</span></span>

<span data-ttu-id="a095a-198">이 자습서에서 배운 됩니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="a095a-198">In this tutorial, you will learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a095a-199">Azure Active Directory B2C 테 넌 트 만들기</span><span class="sxs-lookup"><span data-stu-id="a095a-199">Create an Azure Active Directory B2C tenant</span></span>
> * <span data-ttu-id="a095a-200">Azure AD B2C에 앱을 등록</span><span class="sxs-lookup"><span data-stu-id="a095a-200">Register an app in Azure AD B2C</span></span>
> * <span data-ttu-id="a095a-201">Visual Studio를 사용 하 여 인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 ASP.NET Core 웹 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="a095a-201">Use Visual Studio to create an ASP.NET Core Web Application configured to use the Azure AD B2C tenant for authentication</span></span>
> * <span data-ttu-id="a095a-202">Azure AD B2C 테 넌 트의 동작을 제어 하는 정책 구성</span><span class="sxs-lookup"><span data-stu-id="a095a-202">Configure policies controlling the behavior of the Azure AD B2C tenant</span></span>

<span data-ttu-id="a095a-203">ASP.NET Core 응용 프로그램은 인증을 위해 Azure AD B2C를 사용 하도록 구성 하는 [Authorize 특성](xref:security/authorization/simple) 응용 프로그램 보안에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-203">Now that the ASP.NET Core app is configured to use Azure AD B2C for authentication, the [Authorize attribute](xref:security/authorization/simple) can be used to secure your app.</span></span> <span data-ttu-id="a095a-204">학습 하 여 응용 프로그램 개발을 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-204">Continue developing your app by learning to:</span></span>

* <span data-ttu-id="a095a-205">[Azure AD B2C 사용자 인터페이스 사용자 지정](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-205">[Customize the Azure AD B2C user interface](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization).</span></span>
* <span data-ttu-id="a095a-206">[암호 복잡성 요구 사항을 구성](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-206">[Configure password complexity requirements](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity).</span></span>
* <span data-ttu-id="a095a-207">[Multi-factor authentication 사용](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-207">[Enable multi-factor authentication](/azure/active-directory-b2c/active-directory-b2c-reference-mfa).</span></span>
* <span data-ttu-id="a095a-208">추가 id 공급자와 같은 구성 [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter ](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), 등입니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-208">Configure additional identity providers, such as [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), and others.</span></span>
* <span data-ttu-id="a095a-209">[Azure AD Graph API를 사용 하 여](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) Azure AD B2C 테 넌 트에서 그룹 구성원 자격 등의 추가 사용자 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a095a-209">[Use the Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) to retrieve additional user information, such as group membership, from the Azure AD B2C tenant.</span></span>