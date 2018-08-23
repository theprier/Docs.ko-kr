---
uid: whitepapers/request-validation
title: 요청 유효성 검사-스크립트 공격 방지 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 여기서 기본적으로 응용 프로그램 금지에서 인코딩되지 않은 HTML 콘텐츠 submitt 처리 하는 asp.net 요청 유효성 검사 기능을 설명 하는 중...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 087f30428602137e01f574825f3ebcd4db9285ff
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837506"
---
<a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="58e8f-103">요청 유효성 검사-스크립트 공격 방지</span><span class="sxs-lookup"><span data-stu-id="58e8f-103">Request Validation - Preventing Script Attacks</span></span>
====================
> <span data-ttu-id="58e8f-104">이 문서는 여기서 기본적으로 응용 프로그램 금지에서 서버로 전송 하는 인코딩되지 않은 HTML 콘텐츠를 처리 하는 asp.net 요청 유효성 검사 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="58e8f-105">응용 프로그램 HTML 데이터를 안전 하 게 처리 하도록 디자인 된 경우에이 요청 유효성 검사 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="58e8f-106">ASP.NET 1.1 및 ASP.NET 2.0에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>


<span data-ttu-id="58e8f-107">요청 유효성 검사, 버전 1.1부터 ASP.NET의 기능을 포함 하는 인코딩되지 않은 HTML 콘텐츠를 허용 하지 못하도록 서버를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="58e8f-108">이 기능은 가능해 집니다 클라이언트 스크립트 코드 또는 HTML 수 수 자신도 서버로 전송, 저장 및 다른 사용자에 게 표시 한 다음 몇 가지 스크립트 삽입 공격을 방지 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="58e8f-109">여전히 좋습니다 모든 입력된 데이터를 유효성 검사를 적절 한 경우 HTML 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="58e8f-110">예를 들어, 사용자의 전자 메일 주소 및 다음 저장소 데이터베이스에서 전자 메일 주소를 요청 하는 웹 페이지를 만들 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="58e8f-111">사용자가 입력 &lt;스크립트&gt;경고 ("hello from 스크립트")&lt;/script&gt; 유효한 전자 메일 주소 대신 해당 데이터가 표시 되 면이 스크립트를 실행할 수 경우 콘텐츠가 제대로 인코딩되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="58e8f-112">Asp.net 요청 유효성 검사 기능에서에서이 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="58e8f-113">이 기능은 유용</span><span class="sxs-lookup"><span data-stu-id="58e8f-113">Why this feature is useful</span></span>

<span data-ttu-id="58e8f-114">대부분의 사이트는 간단한 스크립트 삽입 공격에 열려 있는지 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="58e8f-115">이러한 공격의 목적은 잠재적 해커의 사이트에 사용자를 리디렉션할 클라이언트 스크립트를 실행 하거나 HTML을 표시 하 여 사이트를 손상 시키기 인지 스크립트 주입 공격은 웹 개발자와 씨름 해야 하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="58e8f-116">스크립트 삽입 공격 ASP.NET, ASP, 또는 다른 웹 개발 기술을 사용 하는 모든 웹 개발자에 게 문제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="58e8f-117">사전에 ASP.NET 요청 유효성 검사 기능을 해당 콘텐츠를 허용 하도록 결정 하는 개발자는 서버에서 처리 해야 하는 인코딩되지 않은 HTML 콘텐츠를 허용 하지 않음으로써 이러한 공격을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="58e8f-118">예상 결과: 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="58e8f-118">What to expect: Error Page</span></span>

<span data-ttu-id="58e8f-119">아래의 스크린 샷에서 몇 가지 샘플 ASP.NET 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="58e8f-120">이 코드 결과 텍스트 상자에 일부 텍스트를 입력할 수 있는 간단한 페이지에서 실행 단추를 클릭 하 고 텍스트 레이블 컨트롤에 표시:</span><span class="sxs-lookup"><span data-stu-id="58e8f-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="58e8f-121">그러나 JavaScript와 같은 된 `<script>alert("hello!")</script>` 를 입력 하 고 예외를 얻게 제출:</span><span class="sxs-lookup"><span data-stu-id="58e8f-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="58e8f-122">오류 메시지를 나타내는 '잠재적으로 위험한 Request.Form 값이 발견 되었습니다' 정확 하 게 발생 한 문제 및 동작을 변경 하는 방법에 대 한 설명에 자세한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="58e8f-123">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="58e8f-123">For example:</span></span>

<span data-ttu-id="58e8f-124">요청 유효성 검사가 잠재적으로 위험한 클라이언트 입력된 값을 검색 하 고 요청의 처리가 중단 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="58e8f-125">이 값에는 사이트 간 스크립팅 공격 등의 응용 프로그램의 보안을 손상 시키는 시도가 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="58e8f-126">요청 유효성 검사를 사용 하지 않도록 설정 하 여 수 `validateRequest=false` Page 지시문 또는 구성 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="58e8f-127">그러나는 응용 프로그램이 명시적으로 확인 모든 입력이 경우 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="58e8f-128">요청 유효성 검사는 페이지를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="58e8f-128">Disabling request validation on a page</span></span>

<span data-ttu-id="58e8f-129">요청 유효성 검사 설정 해야 하는 페이지를 사용 하지 않도록 설정 합니다 `validateRequest` 페이지 지시문의 특성 `false`:</span><span class="sxs-lookup"><span data-stu-id="58e8f-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="58e8f-130">요청 유효성 검사를 사용 하지 않도록 설정 하는 경우 페이지에 콘텐츠를 제출할 수 있습니다. 확인 페이지 개발자의 책임은 제대로 인코딩된 또는 처리입니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="58e8f-131">응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="58e8f-131">Disabling request validation for your application</span></span>

<span data-ttu-id="58e8f-132">응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정, 수정 또는 응용 프로그램에 대 한 Web.config 파일을 만들어 하며 validateRequest 특성을 설정 합니다 `<pages />` 섹션을 `false`:</span><span class="sxs-lookup"><span data-stu-id="58e8f-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="58e8f-133">서버의 모든 응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하려는 경우 Machine.config 파일을이 수정이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="58e8f-134">요청 유효성 검사를 사용 하지 않도록 설정 하는 경우 응용 프로그램에 콘텐츠를 제출할 수 있습니다. 인지 확인 하려면 응용 프로그램 개발자의 책임은 제대로 인코딩된 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="58e8f-135">아래 코드는 요청 유효성 검사를 해제 하도록 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="58e8f-136">텍스트 상자에 다음 JavaScript에 들어 갔으 면 이제 `<script>alert("hello!")</script>` 결과:</span><span class="sxs-lookup"><span data-stu-id="58e8f-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="58e8f-137">이 방지 하려면 기능을 해제 하는 요청 유효성 검사를 사용 하 여 필요한 HTML로 인코딩합니다 콘텐츠를입니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="58e8f-138">Html 콘텐츠를 인코딩 방법</span><span class="sxs-lookup"><span data-stu-id="58e8f-138">How to HTML encode content</span></span>

<span data-ttu-id="58e8f-139">요청 유효성 검사를 사용 하지 않도록 설정한를 경우 콘텐츠를 HTML 인코딩하 나중에 사용할 저장 되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="58e8f-140">HTML 인코딩을 자동으로 대체할 모든 '&lt;'또는'&gt;' (다른 여러 기호)와 함께 해당 HTML을 사용 하 여 인코딩 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="58e8f-141">예를 들어, '&lt;'으로 바뀝니다'&amp;lt;' 및 '&gt;'바뀝니다'&amp;gt;'.</span><span class="sxs-lookup"><span data-stu-id="58e8f-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="58e8f-142">표시할 이러한 특수 코드를 사용 하는 브라우저는 '&lt;'또는'&gt;' 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="58e8f-143">콘텐츠를 쉽게 HTML로 인코딩된 사용 하 여 서버 수를 `Server.HtmlEncode(string)` API.</span><span class="sxs-lookup"><span data-stu-id="58e8f-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="58e8f-144">콘텐츠 일 수도 있습니다 쉽게 HTML 디코딩된,를 사용 하 여 표준 HTML 되돌릴는 `Server.HtmlDecode(string)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="58e8f-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="58e8f-145">발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e8f-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
