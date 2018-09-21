---
title: 개별 사용자 계정을 사용 하 여 만든 ASP.NET Core 프로젝트를 기반으로 하는 문서
author: rick-anderson
description: 개별 사용자 계정을 사용 하 여 만든 ASP.NET Core 프로젝트를 기반으로 하는 문서를 검색 합니다.
ms.author: riande
ms.date: 11/30/2017
uid: security/authentication/individual
ms.openlocfilehash: ac843342ffc73632fbf9f6359c6c1a5878dcef0d
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523066"
---
# <a name="articles-based-on-aspnet-core-projects-created-with-individual-user-accounts"></a><span data-ttu-id="6f369-103">개별 사용자 계정을 사용 하 여 만든 ASP.NET Core 프로젝트를 기반으로 하는 문서</span><span class="sxs-lookup"><span data-stu-id="6f369-103">Articles based on ASP.NET Core projects created with individual user accounts</span></span>

<span data-ttu-id="6f369-104">ASP.NET Core Id는 "개별 사용자 계정" 옵션을 사용 하 여 Visual Studio에서 프로젝트 템플릿에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-104">ASP.NET Core Identity is included in project templates in Visual Studio with the "Individual User Accounts" option.</span></span>

<span data-ttu-id="6f369-105">인증 템플릿을 사용 하 여.NET Core CLI에서 사용할 수 있습니다 `-au Individual`:</span><span class="sxs-lookup"><span data-stu-id="6f369-105">The authentication templates are available in .NET Core CLI with `-au Individual`:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new mvc -au Individual
dotnet new webapi -au Individual
dotnet new webapp -au Individual
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new mvc -au Individual
dotnet new webapi -au Individual
dotnet new razor -au Individual
```

::: moniker-end

<a name="no"></a>
## <a name="no-authentication"></a><span data-ttu-id="6f369-106">인증 안 함</span><span class="sxs-lookup"><span data-stu-id="6f369-106">No Authentication</span></span>

<span data-ttu-id="6f369-107">인증을 사용 하 여.NET Core CLI에 지정 된 `-au` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-107">Authentication is specified in the .NET Core CLI with the `-au` option.</span></span> <span data-ttu-id="6f369-108">Visual Studio에는 **인증 변경** 대화 상자는 새 웹 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-108">In Visual Studio, the **Change Authentication** dialog is available for new web applications.</span></span> <span data-ttu-id="6f369-109">Visual Studio에서 새 웹 앱에 대 한 기본값은 **인증 없음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-109">The default for new web apps in Visual Studio is **No Authentication**.</span></span>

<span data-ttu-id="6f369-110">인증 안 함을 사용 하 여 만든 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="6f369-110">Projects created with no authentication:</span></span>

* <span data-ttu-id="6f369-111">웹 페이지 및 UI에 로그인 및 로그 아웃에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-111">Don't contain web pages and UI to sign in and sign out.</span></span>
* <span data-ttu-id="6f369-112">인증 코드를 포함 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="6f369-112">Don't contain authentication code.</span></span>

<a name="win"></a>
## <a name="windows-authentication"></a><span data-ttu-id="6f369-113">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="6f369-113">Windows Authentication</span></span>

<span data-ttu-id="6f369-114">Windows 인증을 사용 하 여.NET Core CLI에서 새 웹 앱에 대 한 지정 된 `-au Windows` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-114">Windows Authentication is specified for new web apps in the .NET Core CLI with the `-au Windows` option.</span></span> <span data-ttu-id="6f369-115">Visual Studio에서의 **인증 변경** 대화 상자를 사용 합니다 **Windows 인증** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-115">In Visual Studio, the **Change Authentication** dialog provides the **Windows Authentication** options.</span></span>

<span data-ttu-id="6f369-116">앱을 사용 하도록 구성 된 Windows 인증을 선택 합니다 [Windows Authentication IIS 모듈](xref:host-and-deploy/iis/modules)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-116">If Windows Authentication is selected, the app is configured to use the [Windows Authentication IIS module](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="6f369-117">Windows 인증 인트라넷 웹 사이트를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-117">Windows Authentication is intended for Intranet web sites.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f369-118">추가 자료</span><span class="sxs-lookup"><span data-stu-id="6f369-118">Additional resources</span></span>

<span data-ttu-id="6f369-119">다음 문서에는 개별 사용자 계정을 사용 하는 ASP.NET Core 템플릿에서 생성 된 코드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f369-119">The following articles show how to use the code generated in ASP.NET Core templates that use individual user accounts:</span></span>

* [<span data-ttu-id="6f369-120">SMS를 이용한 2단계 인증</span><span class="sxs-lookup"><span data-stu-id="6f369-120">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="6f369-121">ASP.NET Core의 계정 확인 및 암호 복구</span><span class="sxs-lookup"><span data-stu-id="6f369-121">Account confirmation and password recovery in ASP.NET Core</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="6f369-122">권한 부여로 보호 되는 사용자 데이터를 사용 하 여 ASP.NET Core 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6f369-122">Create an ASP.NET Core app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
