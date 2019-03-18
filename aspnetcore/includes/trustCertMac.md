---
ms.openlocfilehash: 33772d3ad8bbb1ffc54792f8c31834849d0f9567
ms.sourcegitcommit: 34bf9fc6ea814c039401fca174642f0acb14be3c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57964215"
---
<span data-ttu-id="9916c-101">Mac용 Visual Studio는 다음 메시지와 함께 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9916c-101">Visual Studio for Mac displays a dialog with the following message:</span></span>

<span data-ttu-id="9916c-102">*이 프로젝트는 SSL을 사용하도록 구성되었습니다. 브라우저에서 SSL 경고를 방지하기 위해 자체 서명된 인증서를 신뢰하도록 선택할 수 있습니다. IIS Express SSL 인증서를 신뢰하시겠습니까?*</span><span class="sxs-lookup"><span data-stu-id="9916c-102">*This project is configured to use SSL. To avoid SSL warnings in the browser you can choose to trust the self-signed certificate. Would you like to trust the IIS Express SSL certificate?*</span></span>

<span data-ttu-id="9916c-103">**예**를 선택하면 다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9916c-103">Select **Yes** and the following dialog is displayed:</span></span>

![보안 경고 대화 상자](~/getting-started/_static/cert.png)

<span data-ttu-id="9916c-105">개발 인증서를 신뢰하는 데 동의하는 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9916c-105">Select **Yes** if you agree to trust the development certificate.</span></span>

<span data-ttu-id="9916c-106">자세한 내용은 [ASP.NET Core HTTPS 개발 인증서 신뢰](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9916c-106">See [Trust the ASP.NET Core HTTPS development certificate](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos) for more information.</span></span>