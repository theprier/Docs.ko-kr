---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: "HTML 편집기 컨트롤을 사용 하려면 어떻게 해야 합니까? (VB) | Microsoft Docs"
author: microsoft
description: "HTMLEditor는 쉽게 작성 하 고 도구 모음 단추를 통해 HTML 콘텐츠를 편집할 수 있도록 ASP.NET AJAX 컨트롤입니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: a34b3dd53f031856906eca923b6ad6f43a0aaecc
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="how-do-i-use-the-html-editor-control-vb"></a><span data-ttu-id="881e2-104">HTML 편집기 컨트롤을 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="881e2-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="881e2-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="881e2-105">(VB)</span></span>
====================
<span data-ttu-id="881e2-106">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="881e2-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="881e2-107">HTMLEditor는 쉽게 작성 하 고 도구 모음 단추를 통해 HTML 콘텐츠를 편집할 수 있도록 ASP.NET AJAX 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>


<span data-ttu-id="881e2-108">이 자습서의 목표 AJAX 컨트롤 도구 키트에 포함 된 HTML 편집기 컨트롤의 개요를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="881e2-109">HTML 편집기에 대 한 옵션이 글꼴 크기를 변경, 글꼴, 배경색을 변경, 전경색을 수정 텍스트 맞춤, 이미지, 추가 링크를 추가 하 고 수행 잘라내기, 복사 및 붙여넣기 작업 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="881e2-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>


<span data-ttu-id="881e2-110">[![HTML 편집기](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="881e2-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="881e2-111">**그림 01**: The HTML 편집기 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="881e2-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span></span>


<span data-ttu-id="881e2-112">HTML 편집기를 사용 하면 디자인 모드를 사용 하 여 콘텐츠를 입력 하거나 HTML을 직접 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="881e2-113">또한 HTML 콘텐츠를 미리 보려면 옵션으로 제공 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="881e2-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>


<span data-ttu-id="881e2-114">[![디자인, HTML 및 미리 보기 단추](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="881e2-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="881e2-115">**그림 02**: HTML, 디자인과 미리 보기 단추 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="881e2-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span></span>


<span data-ttu-id="881e2-116">이 자습서에서는 HTML 편집기를 표시 하는 방법, HTML 편집기에서 표시 되는 도구 모음 단추를 사용자 지정 하는 방법 및 사이트 간 스크립팅 공격을 방지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="881e2-117">HTML 편집기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="881e2-118">HTML 편집기에서 ASP.NET 페이지를 사용 하려면 먼저 페이지에 ScriptManager 컨트롤을 먼저 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="881e2-119">ScriptManager 컨트롤은 Visual Studio/Visual Web Developer Express 도구 상자에서 AJAX 확장 탭 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="881e2-120">페이지에서 다른 컨트롤 앞에 페이지의 맨 ScriptManager 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="881e2-121">예를 들어 배치할 수 있습니다 즉시 열기 서버 쪽 아래 &lt;양식&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="881e2-122">HTML 편집기 컨트롤은 들어 컨트롤의 다른 구성원과 도구 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="881e2-123">편집기 컨트롤 이름이 지정 됩니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="881e2-123">It is named the Editor control (see Figure 3).</span></span>


<span data-ttu-id="881e2-124">[![HTML 편집기 컨트롤](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="881e2-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="881e2-125">**그림 03**: The HTML 편집기 컨트롤 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="881e2-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span></span>


<span data-ttu-id="881e2-126">HTML 편집기 페이지를 끌어온 후 속성 시트에서 해당 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="881e2-127">예를 들어 일반적으로 원하는 너비와 높이 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="881e2-128">목록 1의 소스는 HTML 편집기를 포함 하는 ASP.NET 페이지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="881e2-129">**1-SimpleEditor.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="881e2-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

<span data-ttu-id="881e2-130">HTML 편집기 컨트롤, 단추 컨트롤 및 리터럴 컨트롤 목록 1의 페이지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="881e2-131">HTML 편집기의 내용이 리터럴 제어에 표시 단추를 클릭할 때 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="881e2-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>


<span data-ttu-id="881e2-132">[![HTML 편집기와 양식을 전송](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="881e2-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="881e2-133">**그림 04**: 양식을 HTML 편집기와 전송 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="881e2-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span></span>


<span data-ttu-id="881e2-134">HTML 편집기 Content 속성은 HTML 콘텐츠를 HTML 편집기에 입력 한 검색을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="881e2-135">주의이 HTML 콘텐츠 JavaScript 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="881e2-136">다음 섹션에서 JavaScript 주입 공격을 방지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="881e2-137">HTML 편집기 도구 모음 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="881e2-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="881e2-138">정확 하 게 단추를 사용자 지정할 수는 편집기에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="881e2-139">예를 들어 다음 HTML 편집기 HTML 모드로 전환 하지 못하게 하려면 HTML 탭을 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="881e2-140">글꼴 크기 드롭다운 목록을 포럼에 과도 하 게 큰 텍스트 만들기 하지 못하게 하려면 제거 하려는 경우도 또는 메시지 post (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="881e2-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>


<span data-ttu-id="881e2-141">[![사용자 지정된 된 HTML 편집기](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="881e2-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="881e2-142">**그림 05**: A HTML 편집기 사용자 지정 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="881e2-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span></span>


<span data-ttu-id="881e2-143">새 HTML 편집기의 기본 편집기 클래스에서 파생 하 여 도구 모음 단추를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="881e2-144">예를 들어 목록 2에서 사용자 지정 편집기 도구 모음 단추 굵게 및 기울임꼴만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="881e2-145">다른 모든 도구 모음 단추 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="881e2-146">또한, HTML 탭이 편집기의 맨 아래에서 제거 되었습니다 (않음 디자인 및 미리 보기 탭 아직 중지 되지 않은).</span><span class="sxs-lookup"><span data-stu-id="881e2-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="881e2-147">**2-응용 프로그램을 나열\_Code\CustomEditor.vb**</span><span class="sxs-lookup"><span data-stu-id="881e2-147">**Listing 2 - App\_Code\CustomEditor.vb**</span></span>

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

<span data-ttu-id="881e2-148">응용 프로그램에 목록 2의 클래스를 추가 해야\_클래스를 자동으로 컴파일되는 있도록 폴더를 코딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="881e2-149">하는 경우 앱\_폴더를 추가 하기만 하면 다음 웹 사이트의 코드 폴더가 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="881e2-150">사용자 지정 편집기를 만든 후 있습니다 추가할 수를 ASP.NET 페이지에 같은 방식으로 일반 HTML 편집기 (참조 코드 3) 추가.</span><span class="sxs-lookup"><span data-stu-id="881e2-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="881e2-151">**3-ShowCustomEditor.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="881e2-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="881e2-152">사이트 간 스크립팅 (XSS) 공격을 피하고</span><span class="sxs-lookup"><span data-stu-id="881e2-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="881e2-153">사용자 로부터 입력을 허용 하 고 웹 사이트에 해당 입력을 다시 표시 될 때마다 잠재적으로 교차 사이트 스크립팅 (XSS) 공격에 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="881e2-154">이론적으로, 악의적인 해커가 입력 다시 표시 되 면 실행 되는 JavaScript 코드를 제출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="881e2-155">사용자 암호 또는 기타 중요 한 정보를 도용 하는 JavaScript은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="881e2-156">일반적으로 HTML 웹 페이지에 표시 하기 전에 사용자 로부터 검색할 어떤 입력 인코딩 XSS 공격 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="881e2-157">그러나 HTML HTML 편집기의 출력 인코딩 것만 인코딩하지 &lt;스크립트&gt; 태그를 모든 HTML 태그 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="881e2-158">즉, 글꼴 종류, 글꼴 크기, 배경색 등 서식을 모두는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="881e2-159">주민 등록 번호-암호, 신용 카드 번호 등 사용자가-중요 한 정보를 수집 하는 경우 사용자는 HTML 편집기에서 검색 하는 인코딩되지 않은 콘텐츠가 표시 되지 해야 것입니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="881e2-160">신뢰할 수 있는 당사자가 웹 사이트에 HTML 콘텐츠를 다시 표시 하지는 또는 HTML 콘텐츠를 전송 하는 경우에만 HTML 편집기를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="881e2-161">예를 들어 블로그 응용 프로그램을 만들 경우 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="881e2-162">이 경우에는 블로그 게시물을 작성할 때 HTML 편집기를 사용 하려면 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="881e2-163">블로그 게시물을 전송 하는 유일한 한와, 아마도 악의적인 JavaScript 제출 자신 신뢰할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="881e2-164">그러나 익명 사용자가 의견을 게시 하도록 허용 하는 경우에 HTML 편집기를 사용 하를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="881e2-165">사용자는 암호 같은 중요 한 정보를 전송 하는 경우에 특히 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="881e2-166">잠재적으로, 악의적인 사용자는 암호를 도용 하는 것에 대 한 올바른 JavaScript를 포함 하는 comment을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="881e2-167">요약</span><span class="sxs-lookup"><span data-stu-id="881e2-167">Summary</span></span>

<span data-ttu-id="881e2-168">이 자습서에서는 들어에 포함 된 HTML 편집기 컨트롤에 간략하게 설명 함께 제공 된 있습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="881e2-169">HTML 편집기를 사용 하 여 사용자 로부터 풍부한 콘텐츠를 허용 하도록 서버에 콘텐츠를 전송 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="881e2-170">도 HTML 편집기에서 표시 되는 도구 모음 단추를 사용자 지정할 수는 방법을 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="881e2-171">마지막으로, 잠재적으로 악의적인 입력을 허용 하도록 HTML 편집기를 사용할 때 교차 사이트 스크립팅 공격을 방지 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="881e2-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="881e2-172">이전</span><span class="sxs-lookup"><span data-stu-id="881e2-172">Previous</span></span>](how-do-i-use-the-html-editor-control-cs.md)
