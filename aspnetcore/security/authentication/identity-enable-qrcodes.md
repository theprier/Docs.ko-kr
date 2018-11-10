---
title: ASP.NET Core에서 TOTP authenticator 앱에 대 한 QR 코드 생성 사용
author: rick-anderson
description: ASP.NET Core 2 단계 인증을 사용 하는 TOTP authenticator 앱에 대 한 QR 코드 생성을 활성화 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 08/14/2018
uid: security/authentication/identity-enable-qrcodes
ms.openlocfilehash: 437f354f71128a98bae9abdced291e04efc9f48e
ms.sourcegitcommit: fc7eb4243188950ae1f1b52669edc007e9d0798d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51225384"
---
# <a name="enable-qr-code-generation-for-totp-authenticator-apps-in-aspnet-core"></a><span data-ttu-id="63cd3-103">ASP.NET Core에서 TOTP authenticator 앱에 대 한 QR 코드 생성 사용</span><span class="sxs-lookup"><span data-stu-id="63cd3-103">Enable QR Code generation for TOTP authenticator apps in ASP.NET Core</span></span>

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="63cd3-104">QR 코드는 ASP.NET Core 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-104">QR Codes requires ASP.NET Core 2.0 or later.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="63cd3-105">ASP.NET Core 개별 인증을 위한 authenticator 응용 프로그램에 대 한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-105">ASP.NET Core ships with support for authenticator applications for individual authentication.</span></span> <span data-ttu-id="63cd3-106">두 단계 인증 (2FA) authenticator 앱의 경우는 시간 기반 일회용 암호 알고리즘 (TOTP)를 사용 하 여 권장 접근법 2FA 위한 업계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-106">Two factor authentication (2FA) authenticator apps, using a Time-based One-time Password Algorithm (TOTP), are the industry recommended approach for 2FA.</span></span> <span data-ttu-id="63cd3-107">2FA TOTP를 사용 하 여는 SMS 2FA 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-107">2FA using TOTP is preferred to SMS 2FA.</span></span> <span data-ttu-id="63cd3-108">Authenticator 앱에는 사용자가 자신의 사용자 이름과 암호를 확인 한 후 입력 해야 하는 6 to 8 자리 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-108">An authenticator app provides a 6 to 8 digit code which users must enter after confirming their username and password.</span></span> <span data-ttu-id="63cd3-109">일반적으로 authenticator 앱은 스마트 폰에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-109">Typically an authenticator app is installed on a smart phone.</span></span>

<span data-ttu-id="63cd3-110">ASP.NET Core 웹 앱 템플릿을 인증자를 지원 하지만 QRCode 생성에 대 한 지원을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-110">The ASP.NET Core web app templates support authenticators, but don't provide support for QRCode generation.</span></span> <span data-ttu-id="63cd3-111">QRCode 생성기 2FA 설치 하는 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-111">QRCode generators ease the setup of 2FA.</span></span> <span data-ttu-id="63cd3-112">이 문서는 과정을 안내 추가 [QR 코드](https://wikipedia.org/wiki/QR_code) 2FA 구성 페이지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-112">This document will guide you through adding [QR Code](https://wikipedia.org/wiki/QR_code) generation to the 2FA configuration page.</span></span>

## <a name="adding-qr-codes-to-the-2fa-configuration-page"></a><span data-ttu-id="63cd3-113">2FA 구성 페이지에 QR 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-113">Adding QR Codes to the 2FA configuration page</span></span>

<span data-ttu-id="63cd3-114">이러한 지침을 사용 *qrcode.js* 에서 https://davidshimjs.github.io/qrcodejs/ 리포지토리.</span><span class="sxs-lookup"><span data-stu-id="63cd3-114">These instructions use *qrcode.js* from the https://davidshimjs.github.io/qrcodejs/ repo.</span></span>

* <span data-ttu-id="63cd3-115">다운로드 합니다 [qrcode.js javascript 라이브러리](https://davidshimjs.github.io/qrcodejs/) 에 `wwwroot\lib` 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-115">Download the [qrcode.js javascript library](https://davidshimjs.github.io/qrcodejs/) to the `wwwroot\lib` folder in your project.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

* <span data-ttu-id="63cd3-116">지침을 따릅니다 [스 캐 폴드 Identity](xref:security/authentication/scaffold-identity) 생성할 */Areas/Identity/Pages/Account/Manage/EnableAuthenticator.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-116">Follow the instructions in [Scaffold Identity](xref:security/authentication/scaffold-identity) to generate */Areas/Identity/Pages/Account/Manage/EnableAuthenticator.cshtml*.</span></span>
* <span data-ttu-id="63cd3-117">*/Areas/Identity/Pages/Account/Manage/EnableAuthenticator.cshtml*를 찾습니다는 `Scripts` 파일의 끝에 있는 섹션:</span><span class="sxs-lookup"><span data-stu-id="63cd3-117">In */Areas/Identity/Pages/Account/Manage/EnableAuthenticator.cshtml*, locate the `Scripts` section at the end of the file:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

* <span data-ttu-id="63cd3-118">*Pages/Account/Manage/EnableAuthenticator.cshtml* (Razor 페이지) 또는 *Views/Manage/EnableAuthenticator.cshtml* (MVC)을 찾습니다는 `Scripts` 파일의 끝에 있는 섹션:</span><span class="sxs-lookup"><span data-stu-id="63cd3-118">In *Pages/Account/Manage/EnableAuthenticator.cshtml* (Razor Pages) or *Views/Manage/EnableAuthenticator.cshtml* (MVC), locate the `Scripts` section at the end of the file:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

```cshtml
@section Scripts {
    @await Html.PartialAsync("_ValidationScriptsPartial")
}
```

* <span data-ttu-id="63cd3-119">업데이트를 `Scripts` 섹션에 대 한 참조를 추가 하는 `qrcodejs` 추가한 라이브러리 및 QR 코드 생성에 대 한 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-119">Update the `Scripts` section to add a reference to the `qrcodejs` library you added and a call to generate the QR Code.</span></span> <span data-ttu-id="63cd3-120">다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-120">It should look as follows:</span></span>

```cshtml
@section Scripts {
    @await Html.PartialAsync("_ValidationScriptsPartial")

    <script type="text/javascript" src="~/lib/qrcode.js"></script>
    <script type="text/javascript">
        new QRCode(document.getElementById("qrCode"),
            {
                text: "@Html.Raw(Model.AuthenticatorUri)",
                width: 150,
                height: 150
            });
    </script>
}
```

* <span data-ttu-id="63cd3-121">이러한 지침에 대 한 링크를 제공 하는 단락을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-121">Delete the paragraph which links you to these instructions.</span></span>

<span data-ttu-id="63cd3-122">앱을 실행 하 고 QR 코드를 스캔 하 고 인증자 입증 하는 코드의 유효성을 검사 수 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-122">Run your app and ensure that you can scan the QR code and validate the code the authenticator proves.</span></span>

## <a name="change-the-site-name-in-the-qr-code"></a><span data-ttu-id="63cd3-123">QR 코드에서 사이트 이름 변경</span><span class="sxs-lookup"><span data-stu-id="63cd3-123">Change the site name in the QR Code</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="63cd3-124">처음 프로젝트를 만들 때 선택한 프로젝트 이름에서 QR 코드에서 사이트 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-124">The site name in the QR Code is taken from the project name you choose when initially creating your project.</span></span> <span data-ttu-id="63cd3-125">검색 하 여 변경할 수 있습니다 합니다 `GenerateQrCodeUri(string email, string unformattedKey)` 의 메서드를 */Areas/Identity/Pages/Account/Manage/EnableAuthenticator.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-125">You can change it by looking for the `GenerateQrCodeUri(string email, string unformattedKey)` method in the */Areas/Identity/Pages/Account/Manage/EnableAuthenticator.cshtml*.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="63cd3-126">처음 프로젝트를 만들 때 선택한 프로젝트 이름에서 QR 코드에서 사이트 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-126">The site name in the QR Code is taken from the project name you choose when initially creating your project.</span></span> <span data-ttu-id="63cd3-127">검색 하 여 변경할 수 있습니다 합니다 `GenerateQrCodeUri(string email, string unformattedKey)` 의 메서드를 *Pages/Account/Manage/EnableAuthenticator.cshtml.cs* (Razor 페이지) 파일 또는 *Controllers/ManageController.cs* (MVC) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-127">You can change it by looking for the `GenerateQrCodeUri(string email, string unformattedKey)` method in the *Pages/Account/Manage/EnableAuthenticator.cshtml.cs* (Razor Pages) file or the *Controllers/ManageController.cs* (MVC) file.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="63cd3-128">템플릿에서 기본 코드를 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-128">The default code from the template looks as follows:</span></span>

```csharp
private string GenerateQrCodeUri(string email, string unformattedKey)
{
    return string.Format(
        AuthenicatorUriFormat,
        _urlEncoder.Encode("Razor Pages"),
        _urlEncoder.Encode(email),
        unformattedKey);
}
```

<span data-ttu-id="63cd3-129">에 대 한 호출에서 두 번째 매개 변수 `string.Format` 은 사이트 이름에서 솔루션 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-129">The second parameter in the call to `string.Format` is your site name, taken from your solution name.</span></span> <span data-ttu-id="63cd3-130">모든 값을 변경할 수 있습니다 하지만 항상 URL 인코딩 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-130">It can be changed to any value, but it must always be URL encoded.</span></span>

## <a name="using-a-different-qr-code-library"></a><span data-ttu-id="63cd3-131">다른 QR 코드 라이브러리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="63cd3-131">Using a different QR Code library</span></span>

<span data-ttu-id="63cd3-132">기본 라이브러리를 사용 하 여 QR 코드 라이브러리를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-132">You can replace the QR Code library with your preferred library.</span></span> <span data-ttu-id="63cd3-133">HTML에는 `qrCode` 라이브러리 제공 하는 요소는 어떤 메커니즘에서 QR 코드를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-133">The HTML contains a `qrCode` element into which you can place a QR Code by whatever mechanism your library provides.</span></span>

<span data-ttu-id="63cd3-134">QR 코드에 대 한 올바른 형식의 URL은에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-134">The correctly formatted URL for the QR Code is available in the:</span></span>

* <span data-ttu-id="63cd3-135">`AuthenticatorUri` 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-135">`AuthenticatorUri` property of the model.</span></span>
* <span data-ttu-id="63cd3-136">`data-url` 속성에는 `qrCodeData` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-136">`data-url` property in the `qrCodeData` element.</span></span>

## <a name="totp-client-and-server-time-skew"></a><span data-ttu-id="63cd3-137">TOTP 클라이언트 및 서버 시간 오차</span><span class="sxs-lookup"><span data-stu-id="63cd3-137">TOTP client and server time skew</span></span>

<span data-ttu-id="63cd3-138">TOTP (시간 기반 일회용 암호) 인증을 정확 하 게 시간이 서버 및 인증 장치에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-138">TOTP (Time-based One-Time Password) authentication depends on both the server and authenticator device having an accurate time.</span></span> <span data-ttu-id="63cd3-139">토큰 30 초 동안 지속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-139">Tokens only last for 30 seconds.</span></span> <span data-ttu-id="63cd3-140">TOTP 2FA 로그인 실패 하는 경우에 서버에 정확 하 고 정확한 NTP 서비스에 동기화 된 것이 좋습니다 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63cd3-140">If TOTP 2FA logins are failing, check that the server time is accurate, and preferably synchronized to an accurate NTP service.</span></span>

::: moniker-end
