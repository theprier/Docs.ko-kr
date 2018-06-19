---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 페이지 (Razor) 사이트를 ASP.NET 웹에서 일관 된 레이아웃 만들기 | Microsoft Docs
author: tfitzmac
description: '사이트에 대 한 웹 페이지를 보다 효율적으로 만들, 콘텐츠 (예: 머리글 및 바닥글) 웹 사이트를 가리키고 있습니다 c에 대 한 다시 사용할 수 있는 블록을 만들 수 있습니다...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/10/2014
ms.topic: article
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 2c7631017f7c0fb31f43320c2ab78baddd87b516
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26530242"
---
<a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="3fc0b-103">ASP.NET 웹 페이지 (Razor) 사이트에서 일관 된 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="3fc0b-103">Creating a Consistent Layout in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="3fc0b-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3fc0b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3fc0b-105">이 문서에서는 사용 하는 방법을 레이아웃 페이지에서 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 다시 사용할 수 있는 블록 콘텐츠 (예: 머리글 및 바닥글)으로 하 고 사이트에 있는 모든 페이지에 일관 된 모양을 만들 수에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-105">This article explains how you can use layout pages in an ASP.NET Web Pages (Razor) website to create reusable blocks of content (like headers and footers) and to create a consistent look for all the pages in the site.</span></span>
> 
> <span data-ttu-id="3fc0b-106">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="3fc0b-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="3fc0b-107">다시 사용할 수 있는 블록의 머리글 및 바닥글와 같은 콘텐츠를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-107">How to create reusable blocks of content like headers and footers.</span></span>
> - <span data-ttu-id="3fc0b-108">레이아웃을 사용 하 여 사이트에서 모든 페이지에 일관 된 모양을 만들 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-108">How to create a consistent look for all the pages in your site using a layout.</span></span>
> - <span data-ttu-id="3fc0b-109">레이아웃 페이지에 실행 시 데이터를 전달 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-109">How to pass data at run time to a layout page.</span></span>
> 
> <span data-ttu-id="3fc0b-110">다음은 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="3fc0b-111">여러 페이지에 삽입할 HTML 형식의 콘텐츠를 포함 하는 파일인 콘텐츠 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-111">Content blocks, which are files that contain HTML-formatted content to be inserted in multiple pages.</span></span>
> - <span data-ttu-id="3fc0b-112">레이아웃 페이지는 웹 사이트에서 페이지에서 공유할 수 있는 HTML 형식의 콘텐츠를 포함 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-112">Layout pages, which are pages that contain HTML-formatted content that can be shared by pages on the website.</span></span>
> - <span data-ttu-id="3fc0b-113">`RenderPage`, `RenderBody`, 및 `RenderSection` ASP.NET을 페이지 요소를 삽입할 위치를 알 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-113">The `RenderPage`, `RenderBody`, and `RenderSection` methods, which tell ASP.NET where to insert page elements.</span></span>
> - <span data-ttu-id="3fc0b-114">`PageData` 콘텐츠 블록 및 레이아웃 페이지 간에 데이터를 공유할 수 있는 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-114">The `PageData` dictionary that lets you share data between content blocks and layout pages.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3fc0b-115">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="3fc0b-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3fc0b-116">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3fc0b-116">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="3fc0b-117">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-117">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="about-layout-pages"></a><span data-ttu-id="3fc0b-118">레이아웃 페이지 정보</span><span class="sxs-lookup"><span data-stu-id="3fc0b-118">About Layout Pages</span></span>

<span data-ttu-id="3fc0b-119">대부분의 웹 사이트에는 머리글 및 바닥글 또는 변경 내용이에 기록 하는 사용자가 알려 주는 상자와 같은 모든 페이지에 표시 되는 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-119">Many websites have content that's displayed on every page, like a header and footer, or a box that tells users that they're logged in.</span></span> <span data-ttu-id="3fc0b-120">ASP.NET은 텍스트, 태그 및 일반 웹 페이지와 마찬가지로 코드를 포함할 수 있는 콘텐츠 블록이 있는 별도 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-120">ASP.NET lets you create a separate file with a content block that can contain text, markup, and code, just like a regular web page.</span></span> <span data-ttu-id="3fc0b-121">다음 정보를 표시 하려는 사이트의 다른 페이지에서 콘텐츠 블록을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-121">You can then insert the content block in other pages on the site where you want the information to appear.</span></span> <span data-ttu-id="3fc0b-122">이렇게 복사한 모든 페이지에 동일한 콘텐츠를 붙여 넣습니다. 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-122">That way you don't have to copy and paste the same content into every page.</span></span> <span data-ttu-id="3fc0b-123">다음과 같은 일반적인 콘텐츠 만들기도 쉽게 사이트 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-123">Creating common content like this also makes it easier to update your site.</span></span> <span data-ttu-id="3fc0b-124">콘텐츠를 변경 해야 하 고 방금 단일 파일을 업데이트할 수 있습니다 다음 변경 내용이 everywhere 반영 콘텐츠 삽입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-124">If you need to change the content, you can just update a single file, and the changes are then reflected everywhere the content has been inserted.</span></span>

<span data-ttu-id="3fc0b-125">다음 다이어그램에서는 콘텐츠 작업을 차단 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-125">The following diagram shows how content blocks work.</span></span> <span data-ttu-id="3fc0b-126">ASP.NET 지점에 콘텐츠 블록을 삽입 브라우저에서 페이지는 웹 서버에서를 요청 하는 경우 여기서는 `RenderPage` 메서드는 기본 페이지에서입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-126">When a browser requests a page from the web server, ASP.NET inserts the content blocks at the point where the `RenderPage` method is called in the main page.</span></span> <span data-ttu-id="3fc0b-127">완료 (병합된) 페이지를 브라우저에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-127">The finished (merged) page is then sent to the browser.</span></span>

![RenderPage 메서드를 현재 페이지에 참조 된 페이지를 삽입 하는 방법을 보여 주는 개념 다이어그램입니다.](3-creating-a-consistent-look/_static/image1.jpg)

<span data-ttu-id="3fc0b-129">이 절차에서는 별도 파일에 있는 두 개의 콘텐츠 블록 (머리글과 바닥글이)를 참조 하는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-129">In this procedure, you'll create a page that references two content blocks (a header and a footer) that are located in separate files.</span></span> <span data-ttu-id="3fc0b-130">사이트의 모든 페이지에서 이러한 동일한 콘텐츠 블록을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-130">You can use these same content blocks in any page in your site.</span></span> <span data-ttu-id="3fc0b-131">완료 되 면 다음과 같이 페이지 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-131">When you're done, you'll get a page like this:</span></span>

![스크린 샷 RenderPage 메서드에 대 한 호출을 포함 하는 페이지 실행 으로부터 만들어지는 브라우저에서 페이지를 표시 합니다.](3-creating-a-consistent-look/_static/image2.jpg)

1. <span data-ttu-id="3fc0b-133">웹 사이트의 루트 폴더에 라는 파일을 만듭니다 *Index.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-133">In the root folder of your website, create a file named *Index.cshtml*.</span></span>
2. <span data-ttu-id="3fc0b-134">기존 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-134">Replace the existing markup with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. <span data-ttu-id="3fc0b-135">루트 폴더에 라는 폴더를 만듭니다 *Shared*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-135">In the root folder, create a folder named *Shared*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3fc0b-136">것이 일반적 라는 폴더의 웹 페이지 간에 공유 되는 파일을 저장할 *Shared*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-136">It's common practice to store files that are shared among web pages in a folder named *Shared*.</span></span>
4. <span data-ttu-id="3fc0b-137">에 *Shared* 폴더 라는 파일을 만들어  *\_Header.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-137">In the *Shared* folder, create a file named *\_Header.cshtml*.</span></span>
5. <span data-ttu-id="3fc0b-138">다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-138">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    <span data-ttu-id="3fc0b-139">파일 이름으로  *\_Header.cshtml*, 밑줄로 (\_) 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-139">Notice that the file name is *\_Header.cshtml*, with an underscore (\_) as a prefix.</span></span> <span data-ttu-id="3fc0b-140">이름이 밑줄로 시작 하는 경우 ASP.NET 브라우저에 페이지를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-140">ASP.NET won't send a page to the browser if its name starts with an underscore.</span></span> <span data-ttu-id="3fc0b-141">이렇게 하면이 페이지를 요청 (실수로 또는 기타) 이러한 직접에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-141">This prevents people from requesting (inadvertently or otherwise) these pages directly.</span></span> <span data-ttu-id="3fc0b-142">실제로 이러한 페이지 &#8212; 요청할 수 있도록 하려면 사용자가 받지 않도록 하기 때문에 밑줄 이름 페이지에는 콘텐츠 블록을 사용 하는 것이 좋습니다. 다른 페이지에 삽입할 엄격 하 게 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-142">It's a good idea to use an underscore to name pages that have content blocks in them, because you don't really want users to be able to request these pages &#8212; they exist strictly to be inserted into other pages.</span></span>
6. <span data-ttu-id="3fc0b-143">*Shared* 폴더를 라는 파일을 만들어  *\_Footer.cshtml* 콘텐츠는 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-143">In the *Shared* folder, create a file named *\_Footer.cshtml* and replace the content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. <span data-ttu-id="3fc0b-144">에 *Index.cshtml* 페이지에 대 한 두 호출을 추가 합니다는 `RenderPage` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-144">In the *Index.cshtml* page, add two calls to the `RenderPage` method, as shown here:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    <span data-ttu-id="3fc0b-145">이 웹 페이지에는 콘텐츠 블록을 삽입 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-145">This shows how to insert a content block into a web page.</span></span> <span data-ttu-id="3fc0b-146">호출 하 여 `RenderPage` 메서드 하 고 해당 시점에 삽입할 내용을 파일의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-146">You call the `RenderPage` method and pass it the name of the file whose contents you want to insert at that point.</span></span> <span data-ttu-id="3fc0b-147">콘텐츠를 삽입 하는 여기에서  *\_Header.cshtml* 및  *\_Footer.cshtml* 로 파일은 *Index.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-147">Here, you're inserting the contents of the *\_Header.cshtml* and *\_Footer.cshtml* files into the *Index.cshtml* file.</span></span>
8. <span data-ttu-id="3fc0b-148">실행 된 *Index.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-148">Run the *Index.cshtml* page in a browser.</span></span> <span data-ttu-id="3fc0b-149">(WebMatrix에서에서 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 선택 **브라우저에서 시작**.)</span><span class="sxs-lookup"><span data-stu-id="3fc0b-149">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.)</span></span>
9. <span data-ttu-id="3fc0b-150">브라우저에서 페이지 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-150">In the browser, view the page source.</span></span> <span data-ttu-id="3fc0b-151">(예를 들어 Internet Explorer에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **소스 보기**.)</span><span class="sxs-lookup"><span data-stu-id="3fc0b-151">(For example, in Internet Explorer, right-click the page and then click **View Source**.)</span></span>

    <span data-ttu-id="3fc0b-152">이렇게 하면 인덱스 페이지 태그는 콘텐츠 블록으로 결합 하는 브라우저로 전송 되는 웹 페이지 태그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-152">This lets you see the web page markup that's sent to the browser, which combines the index page markup with the content blocks.</span></span> <span data-ttu-id="3fc0b-153">다음 예제에 대 한 렌더링 되는 페이지 소스 *Index.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-153">The following example shows the page source that's rendered for *Index.cshtml*.</span></span> <span data-ttu-id="3fc0b-154">에 대 한 호출 `RenderPage` 에 삽입 된 *Index.cshtml* 머리글 및 바닥글 파일의 실제 내용이로 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-154">The calls to `RenderPage` that you inserted into *Index.cshtml* have been replaced with the actual contents of the header and footer files.</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a><span data-ttu-id="3fc0b-155">레이아웃 페이지를 사용 하 여 일관 된 모양을</span><span class="sxs-lookup"><span data-stu-id="3fc0b-155">Creating a Consistent Look Using Layout Pages</span></span>

<span data-ttu-id="3fc0b-156">지금까지 여러 페이지에 동일한 콘텐츠를 포함 하도록 쉽도록 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-156">So far you've seen that it's easy to include the same content on multiple pages.</span></span> <span data-ttu-id="3fc0b-157">사이트에 대 한 일관 된 모양을 하는 보다 구조적인된 방법을 레이아웃 페이지를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-157">A more structured approach to creating a consistent look for a site is to use layout pages.</span></span> <span data-ttu-id="3fc0b-158">레이아웃 페이지, 웹 페이지의 구조를 정의 하지만 실제 콘텐츠를 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-158">A layout page defines the structure of a web page, but doesn't contain any actual content.</span></span> <span data-ttu-id="3fc0b-159">페이지 레이아웃을 만든 후에 콘텐츠를 포함 하는 레이아웃 페이지에 연결 하는 웹 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-159">After you've created a layout page, you can create web pages that contain the content and then link them to the layout page.</span></span> <span data-ttu-id="3fc0b-160">이러한 페이지에 표시 되는 페이지 레이아웃에 따라 포맷 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-160">When these pages are displayed, they'll be formatted according to the layout page.</span></span> <span data-ttu-id="3fc0b-161">(이러한 관점에서 레이아웃 페이지 역할을 다른 페이지에 정의 된 콘텐츠에 대 한 서식 파일의 종류 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3fc0b-161">(In this sense, a layout page acts as a kind of template for content that's defined in other pages.)</span></span>

<span data-ttu-id="3fc0b-162">레이아웃 페이지 것과 HTML 페이지를 제외 하 고 포함에 대 한 호출에서 `RenderBody` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-162">The layout page is just like any HTML page, except that it contains a call to the `RenderBody` method.</span></span> <span data-ttu-id="3fc0b-163">위치는 `RenderBody` 레이아웃 페이지의 메서드 콘텐츠 페이지의 정보를 포함 될 위치를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-163">The position of the `RenderBody` method in the layout page determines where the information from the content page will be included.</span></span>

<span data-ttu-id="3fc0b-164">다음 다이어그램은 어떻게 콘텐츠 페이지를 보여주며, 레이아웃 페이지의 최종된 웹 페이지를 생성 하기 위해 런타임 시 결합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-164">The following diagram shows how content pages and layout pages are combined at run time to produce the finished web page.</span></span> <span data-ttu-id="3fc0b-165">브라우저에서 콘텐츠 페이지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-165">The browser requests a content page.</span></span> <span data-ttu-id="3fc0b-166">콘텐츠 페이지에 페이지의 구조에 사용할 레이아웃 페이지를 지정 하는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-166">The content page has code in it that specifies the layout page to use for the page's structure.</span></span> <span data-ttu-id="3fc0b-167">레이아웃 페이지에서 콘텐츠가 지점에 삽입 됩니다 위치는 `RenderBody` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-167">In the layout page, the content is inserted at the point where the `RenderBody` method is called.</span></span> <span data-ttu-id="3fc0b-168">블록도 삽입할 수 레이아웃 페이지를 호출 하 여 콘텐츠는 `RenderPage` 메서드, 이전 섹션에서 수행한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-168">Content blocks can also be inserted into the layout page by calling the `RenderPage` method, the way you did in the previous section.</span></span> <span data-ttu-id="3fc0b-169">웹 페이지 완료 되 면 브라우저에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-169">When the web page is complete, it's sent to the browser.</span></span>

![스크린 샷 RenderBody 메서드에 대 한 호출을 포함 하는 페이지 실행 으로부터 만들어지는 브라우저에서 페이지를 표시 합니다.](3-creating-a-consistent-look/_static/image3.jpg)

<span data-ttu-id="3fc0b-171">다음 절차를 레이아웃 페이지 및 링크 콘텐츠 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-171">The following procedure shows how to create a layout page and link content pages to it.</span></span>

1. <span data-ttu-id="3fc0b-172">에 *Shared* 라는 파일을 만들어 웹 사이트의 폴더  *\_Layout1.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-172">In the *Shared* folder of your website, create a file named *\_Layout1.cshtml*.</span></span>
2. <span data-ttu-id="3fc0b-173">다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-173">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    <span data-ttu-id="3fc0b-174">사용 된 `RenderPage` 콘텐츠 블록을 삽입 하려면 레이아웃 페이지에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-174">You use the `RenderPage` method in a layout page to insert content blocks.</span></span> <span data-ttu-id="3fc0b-175">레이아웃 페이지를 한 번만 호출을 포함할 수 있습니다는 `RenderBody` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-175">A layout page can contain only one call to the `RenderBody` method.</span></span>
3. <span data-ttu-id="3fc0b-176">에 *Shared* 폴더를 라는 파일을 만듭니다  *\_Header2.cshtml* 다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-176">In the *Shared* folder, create a file named *\_Header2.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. <span data-ttu-id="3fc0b-177">루트 폴더에 새 폴더를 만들고 이름을 *스타일*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-177">In the root folder, create a new folder and name it *Styles*.</span></span>
5. <span data-ttu-id="3fc0b-178">에 *스타일* 폴더 라는 파일을 만들어 *Site.css* 다음과 같은 스타일 정의 추가 하 고:</span><span class="sxs-lookup"><span data-stu-id="3fc0b-178">In the *Styles* folder, create a file named *Site.css* and add the following style definitions:</span></span>

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    <span data-ttu-id="3fc0b-179">이러한 스타일 정의를 레이아웃 페이지와 스타일 시트를 사용할 수 있는 방법을 보여주기 여기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-179">These style definitions are here only to show how style sheets can be used with layout pages.</span></span> <span data-ttu-id="3fc0b-180">원하는 경우 이러한 요소에 대 한 사용자 고유의 스타일을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-180">If you want, you can define your own styles for these elements.</span></span>
6. <span data-ttu-id="3fc0b-181">루트 폴더에 라는 파일을 만듭니다 *Content1.cshtml* 다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-181">In the root folder, create a file named *Content1.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    <span data-ttu-id="3fc0b-182">레이아웃 페이지를 사용 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-182">This is a page that will use a layout page.</span></span> <span data-ttu-id="3fc0b-183">페이지 맨 위에 있는 코드 블록이이 콘텐츠 서식 지정 하는 데 어떤 레이아웃 페이지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-183">The code block at the top of the page indicates which layout page to use to format this content.</span></span>
7. <span data-ttu-id="3fc0b-184">실행 *Content1.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-184">Run *Content1.cshtml* in a browser.</span></span> <span data-ttu-id="3fc0b-185">렌더링된 된 페이지 형식을 사용 및 스타일 시트에 정의 된  *\_Layout1.cshtml* 및에 정의 된 텍스트 (콘텐츠) *Content1.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-185">The rendered page uses the format and style sheet defined in *\_Layout1.cshtml* and the text (content) defined in *Content1.cshtml*.</span></span>

    ![[image]](3-creating-a-consistent-look/_static/image4.jpg)

    <span data-ttu-id="3fc0b-187">그러면 동일한 레이아웃 페이지를 공유할 수 있는 추가 콘텐츠 페이지를 만들려면 6 단계를 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-187">You can repeat step 6 to create additional content pages that can then share the same layout page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3fc0b-188">폴더의 모든 콘텐츠 페이지에 대 한 동일한 레이아웃 페이지를 자동으로 사용할 수 있도록 사이트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-188">You can set up your site so that you can automatically use the same layout page for all the content pages in a folder.</span></span> <span data-ttu-id="3fc0b-189">자세한 내용은 참조 [사이트 전체의 동작을 사용자 지정 ASP.NET 웹 페이지에 대 한](https://go.microsoft.com/fwlink/?LinkId=202906)합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-189">For details, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906).</span></span>

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a><span data-ttu-id="3fc0b-190">여러 콘텐츠 섹션에 있는 레이아웃 페이지 디자인</span><span class="sxs-lookup"><span data-stu-id="3fc0b-190">Designing Layout Pages That Have Multiple Content Sections</span></span>

<span data-ttu-id="3fc0b-191">콘텐츠 페이지에 여러 영역 대체 가능한 콘텐츠가 있는 레이아웃을 사용 하려는 경우 유용한 섹션이 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-191">A content page can have multiple sections, which is useful if you want to use layouts that have multiple areas with replaceable content.</span></span> <span data-ttu-id="3fc0b-192">콘텐츠 페이지에서 각 섹션 된 고유 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-192">In the content page, you give each section a unique name.</span></span> <span data-ttu-id="3fc0b-193">(기본 섹션을 두면 명명 되지 않은.) 레이아웃 페이지에서 추가 된 `RenderBody` 명명 되지 않은 (기본값) 섹션의 표시 위치를 지정 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-193">(The default section is left unnamed.) In the layout page, you add a `RenderBody` method to specify where the unnamed (default) section should appear.</span></span> <span data-ttu-id="3fc0b-194">그런 다음 별도 추가 `RenderSection` 개별적으로 명명 된 섹션을 렌더링 하는 데 메서드.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-194">You then add separate `RenderSection` methods in order to render named sections individually.</span></span>

<span data-ttu-id="3fc0b-195">다음 다이어그램에서는 ASP.NET에서 여러 섹션으로 구분 하는 콘텐츠를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-195">The following diagram shows how ASP.NET handles content that's divided into multiple sections.</span></span> <span data-ttu-id="3fc0b-196">각 명명 된 섹션은 콘텐츠 페이지에 있는 섹션 블록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-196">Each named section is contained in a section block in the content page.</span></span> <span data-ttu-id="3fc0b-197">(이름을 `Header` 및 `List` 예제에서입니다.) 프레임 워크는 시점의 레이아웃 페이지에 콘텐츠 섹션을 삽입 위치는 `RenderSection` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-197">(They're named `Header` and `List` in the example.) The framework inserts content section into the layout page at the point where the `RenderSection` method is called.</span></span> <span data-ttu-id="3fc0b-198">명명 되지 않은 (기본값) 섹션의 지점에 삽입 됩니다 위치는 `RenderBody` 했 듯이 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-198">The unnamed (default) section is inserted at the point where the `RenderBody` method is called, as you saw earlier.</span></span>

![RenderSection 메서드를 현재 페이지에 대 한 참조 섹션을 삽입 하는 방법을 보여 주는 개념 다이어그램입니다.](3-creating-a-consistent-look/_static/image5.jpg)

<span data-ttu-id="3fc0b-200">이 절차에서는 여러 콘텐츠 섹션에 있는 콘텐츠 페이지를 만드는 방법과 여러 콘텐츠 섹션을 지 원하는 레이아웃 페이지를 사용 하 여 렌더링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-200">This procedure shows how to create a content page that has multiple content sections and how to render it using a layout page that supports multiple content sections.</span></span>

1. <span data-ttu-id="3fc0b-201">에 *Shared* 폴더 라는 파일을 만들어  *\_Layout2.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-201">In the *Shared* folder, create a file named *\_Layout2.cshtml*.</span></span>
2. <span data-ttu-id="3fc0b-202">다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-202">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    <span data-ttu-id="3fc0b-203">사용 된 `RenderSection` 헤더와 목록 섹션을 렌더링 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-203">You use the `RenderSection` method to render both the header and list sections.</span></span>
3. <span data-ttu-id="3fc0b-204">루트 폴더에 라는 파일을 만듭니다 *Content2.cshtml* 다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-204">In the root folder, create a file named *Content2.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    <span data-ttu-id="3fc0b-205">이 콘텐츠 페이지의 페이지 맨 위에 있는 코드 블록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-205">This content page contains a code block at the top of the page.</span></span> <span data-ttu-id="3fc0b-206">각 명명 된 섹션 섹션 블록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-206">Each named section is contained in a section block.</span></span> <span data-ttu-id="3fc0b-207">페이지의 나머지 기본 (명명 되지 않은) 콘텐츠 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-207">The rest of the page contains the default (unnamed) content section.</span></span>
4. <span data-ttu-id="3fc0b-208">실행 *Content2.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-208">Run *Content2.cshtml* in a browser.</span></span>

    ![스크린 샷 RenderSection 메서드에 대 한 호출을 포함 하는 페이지 실행 으로부터 만들어지는 브라우저에서 페이지를 표시 합니다.](3-creating-a-consistent-look/_static/image6.jpg)

## <a name="making-content-sections-optional"></a><span data-ttu-id="3fc0b-210">선택적 콘텐츠 섹션 만들기</span><span class="sxs-lookup"><span data-stu-id="3fc0b-210">Making Content Sections Optional</span></span>

<span data-ttu-id="3fc0b-211">일반적으로 콘텐츠 페이지에서 만드는 섹션 페이지 레이아웃 페이지에 정의 된 섹션을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-211">Normally, the sections that you create in a content page have to match sections that are defined in the layout page.</span></span> <span data-ttu-id="3fc0b-212">다음 중 하나가 발생 하는 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-212">You can get errors if any of the following occur:</span></span>

- <span data-ttu-id="3fc0b-213">콘텐츠 페이지 레이아웃 페이지에서 해당 섹션이 없습니다. 포함 된 섹션에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-213">The content page contains a section that has no corresponding section in the layout page.</span></span>
- <span data-ttu-id="3fc0b-214">레이아웃 페이지에 콘텐츠가 없는 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-214">The layout page contains a section for which there's no content.</span></span>
- <span data-ttu-id="3fc0b-215">레이아웃 페이지 같은 섹션을 두 번 이상 렌더링 하려고 하는 메서드 호출을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-215">The layout page includes method calls that try to render the same section more than once.</span></span>

<span data-ttu-id="3fc0b-216">그러나, 레이아웃 페이지에서 선택적 섹션을 선언 하 여 명명된 된 섹션에 대 한이 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-216">However, you can override this behavior for a named section by declaring the section to be optional in the layout page.</span></span> <span data-ttu-id="3fc0b-217">이 레이아웃 페이지를 공유할 수는 있지만 수 또는 특정 섹션에 대 한 콘텐츠가 없을 수도 있는 여러 콘텐츠 페이지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-217">This lets you define multiple content pages that can share a layout page but that might or might not have content for a specific section.</span></span>

1. <span data-ttu-id="3fc0b-218">열기 *Content2.cshtml* 하 고 다음 섹션을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-218">Open *Content2.cshtml* and remove the following section:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. <span data-ttu-id="3fc0b-219">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-219">Save the page and then run it in a browser.</span></span> <span data-ttu-id="3fc0b-220">콘텐츠 페이지 레이아웃 페이지, 즉 헤더 섹션에에서 정의 된 섹션에 대 한 콘텐츠를 제공 하지 않습니다 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-220">An error message is displayed, because the content page doesn't provide content for a section defined in the layout page, namely the header section.</span></span>

    ![RenderSection 메서드를 호출 하는 페이지를 실행 하는 경우 발생 하는 오류를 보여 주는 스크린 샷 하지만 해당 섹션에 제공 되지 않습니다.](3-creating-a-consistent-look/_static/image7.jpg)
3. <span data-ttu-id="3fc0b-222">에 *Shared* 폴더를 엽니다는  *\_Layout2.cshtml* 페이지 하 고이 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-222">In the *Shared* folder, open the *\_Layout2.cshtml* page and replace this line:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    <span data-ttu-id="3fc0b-223">다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="3fc0b-223">with the following code:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    <span data-ttu-id="3fc0b-224">대신 다음 코드 블록 동일한 결과 생성 된 코드의 이전 줄을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-224">As an alternative, you could replace the previous line of code with the following code block, which produces the same results:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. <span data-ttu-id="3fc0b-225">실행 된 *Content2.cshtml* 다시 브라우저에서 페이지.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-225">Run the *Content2.cshtml* page in a browser again.</span></span> <span data-ttu-id="3fc0b-226">(이 페이지를 브라우저에서 엽니다. 여전히 있으면 있습니다 방금 새로 고치면 됩니다.) 이 현재 페이지에 머리글이 있는 경우에 오류 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-226">(If you still have this page open in the browser, you can just refresh it.) This time the page is displayed with no error, even though it has no header.</span></span>

## <a name="passing-data-to-layout-pages"></a><span data-ttu-id="3fc0b-227">레이아웃 페이지에 대 한 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="3fc0b-227">Passing Data to Layout Pages</span></span>

<span data-ttu-id="3fc0b-228">레이아웃 페이지에서를 참조 해야 하는 콘텐츠 페이지에 정의 된 데이터를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-228">You might have data defined in the content page that you need to refer to in a layout page.</span></span> <span data-ttu-id="3fc0b-229">그렇다면 콘텐츠 페이지의 페이지 레이아웃에 데이터를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-229">If so, you need to pass the data from the content page to the layout page.</span></span> <span data-ttu-id="3fc0b-230">예를 들어 사용자의 로그인 상태를 표시 하는 것이 좋습니다 또는를 사용자 입력에 따라 콘텐츠 영역을 표시할지는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-230">For example, you might want to display the login status of a user, or you might want to show or hide content areas based on user input.</span></span>

<span data-ttu-id="3fc0b-231">데이터를 콘텐츠 페이지에서 페이지 레이아웃을 전달 하려면에 값을 정렬할 수 있습니다는 `PageData` 콘텐츠 페이지의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-231">To pass data from a content page to a layout page, you can put values into the `PageData` property of the content page.</span></span> <span data-ttu-id="3fc0b-232">`PageData` 속성은 페이지 사이 전달 하려면 데이터를 보유 하는 이름/값 쌍의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-232">The `PageData` property is a collection of name/value pairs that hold the data that you want to pass between pages.</span></span> <span data-ttu-id="3fc0b-233">레이아웃 페이지에서 다음의 값을 읽을 수는 `PageData` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-233">In the layout page, you can then read values out of the `PageData` property.</span></span>

<span data-ttu-id="3fc0b-234">다른 다이어그램 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-234">Here's another diagram.</span></span> <span data-ttu-id="3fc0b-235">ASP.NET 사용 하는 방법을 보여 줍니다이 중 하나는 `PageData` 속성 값을 전달 하는 콘텐츠 페이지 레이아웃 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-235">This one shows how ASP.NET can use the `PageData` property to pass values from a content page to the layout page.</span></span> <span data-ttu-id="3fc0b-236">ASP.NET 웹 페이지를 작성을 시작 하는 경우 생성 된 `PageData` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-236">When ASP.NET begins building the web page, it creates the `PageData` collection.</span></span> <span data-ttu-id="3fc0b-237">콘텐츠 페이지에 데이터를 저장 하는 코드를 작성 하는 `PageData` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-237">In the content page, you write code to put data in the `PageData` collection.</span></span> <span data-ttu-id="3fc0b-238">값에 `PageData` 컬렉션 콘텐츠 페이지의 다른 섹션 하거나 콘텐츠 블록을 추가 하 여 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-238">Values in the `PageData` collection can also be accessed by other sections in the content page or by additional content blocks.</span></span>

![콘텐츠 페이지 수는 PageData 사전을 채우는 하 고 페이지 레이아웃 페이지에 해당 정보를 전달 하는 방법을 보여 주는 개념 다이어그램](3-creating-a-consistent-look/_static/image8.jpg)

<span data-ttu-id="3fc0b-240">다음 절차에는 레이아웃 페이지에 콘텐츠 페이지에서 데이터를 전달 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-240">The following procedure shows how to pass data from a content page to a layout page.</span></span> <span data-ttu-id="3fc0b-241">페이지를 실행 하는 경우에 사용자가 페이지 레이아웃 페이지에 정의 된 목록을 표시 하거나 숨길 수 있는 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-241">When the page runs, it displays a button that lets the user hide or show a list that's defined in the layout page.</span></span> <span data-ttu-id="3fc0b-242">사용자가 단추를 클릭 하는 경우에 true/false (부울) 값 설정 된 `PageData` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-242">When users click the button, it sets a true/false (Boolean) value in the `PageData` property.</span></span> <span data-ttu-id="3fc0b-243">레이아웃 페이지 그 값을 읽고 false 인 경우 목록을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-243">The layout page reads that value, and if it's false, hides the list.</span></span> <span data-ttu-id="3fc0b-244">콘텐츠 페이지에도 값은 사용을 표시할지 여부를 결정 하는 **숨길 목록** 단추 또는 **목록 표시** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-244">The value is also used in the content page to determine whether to display the **Hide List** button or the **Show List** button.</span></span>

![[image]](3-creating-a-consistent-look/_static/image9.jpg)

1. <span data-ttu-id="3fc0b-246">루트 폴더에 라는 파일을 만듭니다 *Content3.cshtml* 다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-246">In the root folder, create a file named *Content3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    <span data-ttu-id="3fc0b-247">라는 두 가지의 데이터를 저장 하는 코드는 `PageData` 속성 &#8212; 제목 웹 페이지 및 true 또는 false 목록을 표시할 것인지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-247">The code stores two pieces of data in the `PageData` property &#8212; the title of the web page and true or false to specify whether to display a list.</span></span>

    <span data-ttu-id="3fc0b-248">ASP.NET 코드 블록을 사용 하 여 조건에 따라 페이지에 HTML 태그를 설정할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-248">Notice that ASP.NET lets you put HTML markup into the page conditionally using a code block.</span></span> <span data-ttu-id="3fc0b-249">예를 들어는 `if/else` 페이지의 본문에는 블록 폼을 표시 하는지 여부에 따라 결정 `PageData["ShowList"]` 설정을 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-249">For example, the `if/else` block in the body of the page determines which form to display depending on whether `PageData["ShowList"]` is set to true.</span></span>
2. <span data-ttu-id="3fc0b-250">에 *Shared* 폴더를 라는 파일을 만듭니다  *\_Layout3.cshtml* 다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-250">In the *Shared* folder, create a file named *\_Layout3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    <span data-ttu-id="3fc0b-251">레이아웃 페이지에 식이 포함 되어는 `<title>` 에서 제목 값을 가져오는 요소는 `PageData` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-251">The layout page includes an expression in the `<title>` element that gets the title value from the `PageData` property.</span></span> <span data-ttu-id="3fc0b-252">또한 사용 하 여는 `ShowList` 의 값은 `PageData` 속성을 목록 콘텐츠 블록을 표시할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-252">It also uses the `ShowList` value of the `PageData` property to determine whether to display the list content block.</span></span>
3. <span data-ttu-id="3fc0b-253">에 *Shared* 폴더를 라는 파일을 만듭니다  *\_List.cshtml* 다음 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-253">In the *Shared* folder, create a file named *\_List.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. <span data-ttu-id="3fc0b-254">실행 된 *Content3.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-254">Run the *Content3.cshtml* page in a browser.</span></span> <span data-ttu-id="3fc0b-255">페이지는 페이지의 왼쪽에 표시 목록에는 및 **숨길 목록** 아래쪽 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-255">The page is displayed with the list visible on the left side of the page and a **Hide List** button at the bottom.</span></span>

    ![목록 및 목록 숨기기 ' 라는 단추를 포함 하는 페이지를 보여주는 스크린샷.](3-creating-a-consistent-look/_static/image10.jpg)
5. <span data-ttu-id="3fc0b-257">클릭 **목록 숨기기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-257">Click **Hide List**.</span></span> <span data-ttu-id="3fc0b-258">목록 사라지고 단추가으로 변경 **목록 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-258">The list disappears and the button changes to **Show List**.</span></span>

    ![목록과 목록 표시 ' 라는 단추를 포함 하지 않는 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image11.jpg)
6. <span data-ttu-id="3fc0b-260">클릭는 **목록 표시** 단추 및 목록을 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fc0b-260">Click the **Show List** button, and the list is displayed again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3fc0b-261">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3fc0b-261">Additional Resources</span></span>


[<span data-ttu-id="3fc0b-262">ASP.NET 웹 페이지에 대 한 사이트 전체 동작을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3fc0b-262">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
