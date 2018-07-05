---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: '1 부: 개요 및 프로젝트 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: 0540f3142d73fef616e30544bb1130b75c0bb436
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816307"
---
<a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="40f3a-102">1 부: 개요 및 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="40f3a-102">Part 1: Overview and Creating the Project</span></span>
====================
<span data-ttu-id="40f3a-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="40f3a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="40f3a-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="40f3a-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="40f3a-105">Entity Framework는 개체/관계형 매핑 프레임 워크는 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="40f3a-106">코드에서 도메인 개체 관계형 데이터베이스의 엔터티에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="40f3a-107">대부분의 경우 필요가 없습니다 데이터베이스 계층에 걱정할 수의 Entity Framework가 처리 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="40f3a-108">코드 개체를 조작 하 고 변경 내용을 데이터베이스에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="40f3a-109">자습서 정보</span><span class="sxs-lookup"><span data-stu-id="40f3a-109">About the Tutorial</span></span>

<span data-ttu-id="40f3a-110">이 자습서에서는 간단한 스토어 응용 프로그램을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="40f3a-111">응용 프로그램에 두 가지 주요 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-111">There are two main parts to the application.</span></span> <span data-ttu-id="40f3a-112">일반 사용자 제품 보기 및 orders를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="40f3a-113">관리자 만들기, 삭제 또는 제품을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="40f3a-114">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="40f3a-114">Skills You'll Learn</span></span>

<span data-ttu-id="40f3a-115">학습할 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="40f3a-116">ASP.NET Web API를 사용 하 여 Entity Framework를 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="40f3a-117">Knockout.js를 사용 하 여 동적 클라이언트 UI를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="40f3a-118">Web API를 사용 하 여 폼 인증을 사용 하 여 사용자를 인증 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="40f3a-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="40f3a-119">이 자습서는 자체 포함 된 경우에 다음 자습서를 먼저 읽기 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="40f3a-120">첫 번째 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="40f3a-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="40f3a-121">CRUD 작업을 지 원하는 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="40f3a-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="40f3a-122">에 대 한 지식을 [ASP.NET MVC](../../../../mvc/index.md) 에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="40f3a-123">개요</span><span class="sxs-lookup"><span data-stu-id="40f3a-123">Overview</span></span>

<span data-ttu-id="40f3a-124">다음은 높은 수준에서 응용 프로그램의 아키텍처가입니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="40f3a-125">ASP.NET MVC는 클라이언트에 대 한 HTML 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="40f3a-126">ASP.NET Web API (products 및 orders) 데이터에 대해 CRUD 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="40f3a-127">Entity Framework Web API에서 데이터베이스 엔터티를 사용 하는 C# 모델을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="40f3a-128">다음 다이어그램은 응용 프로그램의 다양 한 계층에서 도메인 개체 표현 되는 방식을 보여 줍니다: 데이터베이스 계층, 개체 모델 및 마지막 통신 형식에 HTTP 통해 클라이언트에 데이터를 전송 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="40f3a-129">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="40f3a-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="40f3a-130">Visual Web Developer Express 또는 정식 버전의 Visual Studio를 사용 하 여 자습서 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="40f3a-131">**시작** 페이지에서 클릭 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="40f3a-132">에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="40f3a-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="40f3a-133">아래 **Visual C#** 를 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="40f3a-134">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="40f3a-135">"ProductStore" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="40f3a-136">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="40f3a-137">"인터넷 응용 프로그램" 템플릿을 폼 인증을 지 원하는 ASP.NET MVC 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="40f3a-138">이제 응용 프로그램을 실행 하는 경우 일부 기능은 이미:</span><span class="sxs-lookup"><span data-stu-id="40f3a-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="40f3a-139">오른쪽 위 모서리에서 "등록" 링크를 클릭 하 여 새 사용자가 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="40f3a-140">"로그인" 링크를 클릭 하 여 등록된 한 사용자 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="40f3a-141">멤버 자격 정보는 자동으로 생성 되는 데이터베이스에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="40f3a-142">ASP.NET MVC에서 폼 인증에 대 한 자세한 내용은 참조 하세요. [연습: ASP.NET MVC에서 폼 인증 사용 하 여](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="40f3a-143">CSS 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="40f3a-143">Update the CSS File</span></span>

<span data-ttu-id="40f3a-144">이 단계는 표면적인 이지만 이전 스크린 샷은 다음과 같이 렌더링 된 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="40f3a-145">솔루션 탐색기에서 콘텐츠 폴더를 확장 하 고 Site.css 라는 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="40f3a-146">다음과 같은 CSS 스타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f3a-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="40f3a-147">다음</span><span class="sxs-lookup"><span data-stu-id="40f3a-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
