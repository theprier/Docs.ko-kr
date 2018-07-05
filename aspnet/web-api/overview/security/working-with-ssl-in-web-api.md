---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: Web API에서에서 SSL 사용 | Microsoft Docs
author: MikeWasson
description: SSL 클라이언트 인증서를 사용 하 여 ASP.NET Web API를 사용 하 여 SSL을 사용 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4e14607f11fcd376b4ceca4bf7862259abe015e6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396632"
---
<a name="working-with-ssl-in-web-api"></a><span data-ttu-id="9be14-103">Web API에서에서 SSL 사용</span><span class="sxs-lookup"><span data-stu-id="9be14-103">Working with SSL in Web API</span></span>
====================
<span data-ttu-id="9be14-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9be14-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9be14-105">일반 HTTP를 통해 몇 가지 일반적인 인증 체계 보호 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-105">Several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="9be14-106">특히 기본 인증 및 폼 인증은 암호화 되지 않은 자격 증명을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-106">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="9be14-107">안전한 이러한 인증 체계 *해야* SSL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-107">To be secure, these authentication schemes *must* use SSL.</span></span> <span data-ttu-id="9be14-108">또한 클라이언트 인증 SSL 클라이언트 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-108">In addition, SSL client certificates can be used to authenticate clients.</span></span>

## <a name="enabling-ssl-on-the-server"></a><span data-ttu-id="9be14-109">서버에서 SSL을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9be14-109">Enabling SSL on the Server</span></span>

<span data-ttu-id="9be14-110">이상 IIS 7에서 SSL을 설정 하려면:</span><span class="sxs-lookup"><span data-stu-id="9be14-110">To set up SSL in IIS 7 or later:</span></span>

- <span data-ttu-id="9be14-111">페이지를 만들거나 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-111">Create or get a certificate.</span></span> <span data-ttu-id="9be14-112">테스트를 위해 자체 서명 된 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-112">For testing, you can create a self-signed certificate.</span></span>
- <span data-ttu-id="9be14-113">HTTPS 바인딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-113">Add an HTTPS binding.</span></span>

<span data-ttu-id="9be14-114">자세한 내용은 참조 하세요 [IIS 7에서 SSL을 설정 하는 방법을](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-114">For details, see [How to Set Up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<span data-ttu-id="9be14-115">로컬 테스트를 위해 Visual Studio에서 IIS Express에서 SSL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-115">For local testing, you can enable SSL in IIS Express from Visual Studio.</span></span> <span data-ttu-id="9be14-116">속성 창에서 설정 **SSL 사용** 하 **True**합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-116">In the Properties window, set **SSL Enabled** to **True**.</span></span> <span data-ttu-id="9be14-117">값을 적어 둡니다 **SSL URL**;이 URL을 사용 하 여 HTTPS 연결을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-117">Note the value of **SSL URL**; use this URL for testing HTTPS connections.</span></span>

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a><span data-ttu-id="9be14-118">Web API 컨트롤러에서 SSL 적용</span><span class="sxs-lookup"><span data-stu-id="9be14-118">Enforcing SSL in a Web API Controller</span></span>

<span data-ttu-id="9be14-119">HTTPS 및 HTTP 바인딩을 모두를 설정한 경우 클라이언트 사이트에 액세스 하려면 HTTP를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-119">If you have both an HTTPS and an HTTP binding, clients can still use HTTP to access the site.</span></span> <span data-ttu-id="9be14-120">다른 리소스는 SSL을 요구 하는 동안 HTTP를 통해 사용할 수 있는 몇 가지 리소스를 허용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-120">You might allow some resources to be available through HTTP, while other resources require SSL.</span></span> <span data-ttu-id="9be14-121">이 경우 보호 된 리소스에 대 한 SSL을 요구 하는 작업 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-121">In that case, use an action filter to require SSL for the protected resources.</span></span> <span data-ttu-id="9be14-122">다음 코드에서는 SSL을 확인 하는 Web API 인증 필터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-122">The following code shows a Web API authentication filter that checks for SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

<span data-ttu-id="9be14-123">Ssl을 사용 하는 모든 Web API 작업에이 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-123">Add this filter to any Web API actions that require SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a><span data-ttu-id="9be14-124">SSL 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="9be14-124">SSL Client Certificates</span></span>

<span data-ttu-id="9be14-125">SSL은 인증서 공개 키 인프라를 사용 하 여 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-125">SSL provides authentication by using Public Key Infrastructure certificates.</span></span> <span data-ttu-id="9be14-126">서버는 클라이언트에 서버를 인증 하는 인증서를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-126">The server must provide a certificate that authenticates the server to the client.</span></span> <span data-ttu-id="9be14-127">서버에 인증서를 제공 하기 위해 클라이언트에 대 한 자주 있지만 클라이언트를 인증 하는 한 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-127">It is less common for the client to provide a certificate to the server, but this is one option for authenticating clients.</span></span> <span data-ttu-id="9be14-128">클라이언트 인증서를 사용 하 여 SSL을 사용 하 여, 사용자에 게 서명 된 인증서를 배포 하는 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-128">To use client certificates with SSL, you need a way to distribute signed certificates to your users.</span></span> <span data-ttu-id="9be14-129">많은 응용 프로그램 형식에 대 한이 좋은 사용자 환경이 되지 않지만 일부 환경 (예를 들어, enterprise)는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-129">For many application types, this will not be a good user experience, but in some environments (for example, enterprise) it may be feasible.</span></span>

| <span data-ttu-id="9be14-130">장점</span><span class="sxs-lookup"><span data-stu-id="9be14-130">Advantages</span></span> | <span data-ttu-id="9be14-131">단점</span><span class="sxs-lookup"><span data-stu-id="9be14-131">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="9be14-132">-인증서 자격 증명은 사용자 이름/암호 보다 더 강력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-132">- Certificate credentials are stronger than username/password.</span></span> <span data-ttu-id="9be14-133">SSL 인증, 메시지 무결성 및 메시지 암호화를 사용 하 여 전체 보안 채널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-133">- SSL provides a complete secure channel, with authentication, message integrity, and message encryption.</span></span> | <span data-ttu-id="9be14-134">-가져올 하 고 PKI 인증서를 관리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-134">- You must obtain and manage PKI certificates.</span></span> <span data-ttu-id="9be14-135">-클라이언트 플랫폼 SSL 클라이언트 인증서를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-135">- The client platform must support SSL client certificates.</span></span> |

<span data-ttu-id="9be14-136">클라이언트 인증서를 수락 하도록 IIS를 구성 하려면 IIS 관리자를 열고 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-136">To configure IIS to accept client certificates, open IIS Manager and perform the following steps:</span></span>

1. <span data-ttu-id="9be14-137">트리 뷰에서 사이트 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-137">Click the site node in the tree view.</span></span>
2. <span data-ttu-id="9be14-138">두 번 클릭 합니다 **SSL 설정** 가운데 창에서 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-138">Double-click the **SSL Settings** feature in the middle pane.</span></span>
3. <span data-ttu-id="9be14-139">아래 **클라이언트 인증서**, 이러한 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-139">Under **Client Certificates**, select one of these options:</span></span> 

    - <span data-ttu-id="9be14-140">**수락**: IIS에서 클라이언트 인증서를 허용 되지만 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-140">**Accept**: IIS will accept a certificate from the client, but does not require one.</span></span>
    - <span data-ttu-id="9be14-141">**필요한**: 클라이언트 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-141">**Require**: Require a client certificate.</span></span> <span data-ttu-id="9be14-142">(이 옵션을 사용 하려면 선택 해야 "SSL 필요)</span><span class="sxs-lookup"><span data-stu-id="9be14-142">(To enable this option, you must also select "Require SSL")</span></span>

<span data-ttu-id="9be14-143">또한 ApplicationHost.config 파일에서 이러한 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-143">You can also set these options in the ApplicationHost.config file:</span></span>

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

<span data-ttu-id="9be14-144">합니다 **SslNegotiateCert** 플래그 IIS 인증서 클라이언트에서 허용 되지만 (IIS 관리자에서 "허용" 옵션와 동일) 세션이 필요 없음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-144">The **SslNegotiateCert** flag means IIS will accept a certificate from the client, but does not require one (equivalent to the "Accept" option in IIS Manager).</span></span> <span data-ttu-id="9be14-145">인증서를 요구 하도록 설정 합니다 **SslRequireCert** 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-145">To require a certificate, set the **SslRequireCert** flag.</span></span> <span data-ttu-id="9be14-146">테스트를 위해 로컬 applicationhost의 IIS Express에서 이러한 옵션을 또한 설정할 수 있습니다. "Documents\IISExpress\config"에 있는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-146">For testing, you can also set these options in IIS Express, in the local applicationhost.Config file, located in "Documents\IISExpress\config".</span></span>

### <a name="creating-a-client-certificate-for-testing"></a><span data-ttu-id="9be14-147">테스트에 대 한 클라이언트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="9be14-147">Creating a Client Certificate for Testing</span></span>

<span data-ttu-id="9be14-148">테스트 목적으로 사용할 수 있습니다 [MakeCert.exe](https://msdn.microsoft.com/library/bfsktky3.aspx) 클라이언트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-148">For testing purposes, you can use [MakeCert.exe](https://msdn.microsoft.com/library/bfsktky3.aspx) to create a client certificate.</span></span> <span data-ttu-id="9be14-149">테스트 루트 인증 기관을 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-149">First, create a test root authority:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

<span data-ttu-id="9be14-150">Makecert는 개인 키에 대 한 암호를 입력 하 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-150">Makecert will prompt you to enter a password for the private key.</span></span>

<span data-ttu-id="9be14-151">서버의 "신뢰할 수 있는 루트 인증 기관" 저장소를 다음과 같이 테스트 인증서를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-151">Next, add the certificate to the test server's "Trusted Root Certification Authorities" store, as follows:</span></span>

1. <span data-ttu-id="9be14-152">MMC를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-152">Open MMC.</span></span>
2. <span data-ttu-id="9be14-153">아래 **파일**를 선택 **스냅인 추가/제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-153">Under **File**, select **Add/Remove Snap-In**.</span></span>
3. <span data-ttu-id="9be14-154">선택 **컴퓨터 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-154">Select **Computer Account**.</span></span>
4. <span data-ttu-id="9be14-155">선택 **로컬 컴퓨터** 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-155">Select **Local computer** and complete the wizard.</span></span>
5. <span data-ttu-id="9be14-156">탐색 창에서 "신뢰할 수 있는 루트 인증 기관" 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-156">Under the navigation pane, expand the "Trusted Root Certification Authorities" node.</span></span>
6. <span data-ttu-id="9be14-157">에 **동작** 메뉴에서 **모든 작업**를 클릭 하 고 **가져오기** 인증서 가져오기 마법사를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-157">On the **Action** menu, point to **All Tasks**, and then click **Import** to start the Certificate Import Wizard.</span></span>
7. <span data-ttu-id="9be14-158">TempCA.cer 인증서 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-158">Browse to the certificate file, TempCA.cer.</span></span>
8. <span data-ttu-id="9be14-159">클릭 **엽니다**, 클릭 **다음** 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-159">Click **Open**, then click **Next** and complete the wizard.</span></span> <span data-ttu-id="9be14-160">(묻는 다시 암호를 입력 합니다.)</span><span class="sxs-lookup"><span data-stu-id="9be14-160">(You will be prompted to re-enter the password.)</span></span>

<span data-ttu-id="9be14-161">이제 첫 번째 인증서에서 서명 된 클라이언트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-161">Now create a client certificate that is signed by the first certificate:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a><span data-ttu-id="9be14-162">클라이언트 인증서를 사용 하 여 Web API에서</span><span class="sxs-lookup"><span data-stu-id="9be14-162">Using Client Certificates in Web API</span></span>

<span data-ttu-id="9be14-163">서버 쪽에서 호출 하 여 클라이언트 인증서를 가져올 수 있습니다 [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) 요청 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-163">On the server side, you can get the client certificate by calling [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) on the request message.</span></span> <span data-ttu-id="9be14-164">메서드를 클라이언트 인증서가 없으면 null을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-164">The method returns null if there is no client certificate.</span></span> <span data-ttu-id="9be14-165">를 반환 합니다는 **X509Certificate2** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9be14-165">Otherwise, it returns an **X509Certificate2** instance.</span></span> <span data-ttu-id="9be14-166">인증서 발급자 및 주체와 같이에서 내용을이 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-166">Use this object to get information from the certificate, such as the issuer and subject.</span></span> <span data-ttu-id="9be14-167">그런 다음 인증 및/또는 권한 부여에 대 한이 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9be14-167">Then you can use this information for authentication and/or authorization.</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
