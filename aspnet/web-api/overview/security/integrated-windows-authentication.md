---
uid: web-api/overview/security/integrated-windows-authentication
title: 통합 Windows 인증 | Microsoft Docs
author: MikeWasson
description: 통합 Windows 인증을 사용 하 여 ASP.NET Web API에 설명 합니다.
ms.author: aspnetcontent
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: c15677b7aa66619f1ff32819585340ff497b937d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820408"
---
<a name="integrated-windows-authentication"></a><span data-ttu-id="5b952-103">통합된 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="5b952-103">Integrated Windows Authentication</span></span>
====================
<span data-ttu-id="5b952-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5b952-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5b952-105">통합된 Windows 인증에 Kerberos 또는 NTLM을 사용 하는 Windows 자격 증명을 사용 하 여 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="5b952-106">클라이언트 자격 증명 권한 부여 헤더를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="5b952-107">Windows 인증은 인트라넷 환경에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="5b952-108">자세한 내용은 [Windows 인증](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="5b952-109">장점</span><span class="sxs-lookup"><span data-stu-id="5b952-109">Advantages</span></span> | <span data-ttu-id="5b952-110">단점</span><span class="sxs-lookup"><span data-stu-id="5b952-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="5b952-111">-IIS에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-111">- Built into IIS.</span></span> <span data-ttu-id="5b952-112">-요청에 사용자 자격 증명을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="5b952-113">-클라이언트 컴퓨터는 도메인 (예를 들어 인트라넷 응용 프로그램)에 속하는 경우에 사용자를 자격 증명을 입력 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="5b952-114">-인터넷 응용 프로그램에 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="5b952-115">-클라이언트에서 Kerberos 또는 NTLM 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="5b952-116">클라이언트는 Active Directory 도메인에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="5b952-117">응용 프로그램이 Azure에서 호스트 되 고에 온-프레미스 Active Directory 도메인에 있는 경우에 Azure Active Directory를 사용 하 여 온-프레미스 AD를 페더레이션 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="5b952-118">이런 방식으로 사용자가 온-프레미스 자격 증명을 사용 하 여 기록할 수 있지만 Azure AD에서 인증을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="5b952-119">자세한 내용은 [Azure 인증](../../../visual-studio/overview/2012/windows-azure-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>


<span data-ttu-id="5b952-120">통합 Windows 인증을 사용 하는 응용 프로그램을 만들려면 MVC 4 프로젝트 마법사에서 "인트라넷 응용 프로그램" 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="5b952-121">이 프로젝트 템플릿은 Web.config 파일에서 다음 설정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="5b952-122">클라이언트 쪽에서 통합 Windows 인증을 지 원하는 모든 브라우저를 사용 하 여 작동 합니다 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) 대부분의 주요 브라우저를 포함 하는 인증 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="5b952-123">.NET 클라이언트 응용 프로그램을 **HttpClient** 클래스는 Windows 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="5b952-124">Windows 인증은 교차 사이트 요청 위조 (CSRF) 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="5b952-125">참조 [교차 사이트 요청 위조 (CSRF) 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b952-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
