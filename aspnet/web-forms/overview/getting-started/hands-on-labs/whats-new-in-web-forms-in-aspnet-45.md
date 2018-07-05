---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5의에서 Forms 웹의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 새 버전의 ASP.NET Web Forms 다양 한 데이터로 작업 하는 경우 사용자 환경 개선에 집중 하는 향상 된 기능을 소개 합니다. 이전 버전의...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: f36c50b64ed2363ba648297a1424b638bf9d4af5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830414"
---
<a name="whats-new-in-web-forms-in-aspnet-45"></a><span data-ttu-id="12d02-104">Asp.net 4.5 Web Forms의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="12d02-104">What's New in Web Forms in ASP.NET 4.5</span></span>
====================
<span data-ttu-id="12d02-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="12d02-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="12d02-106">새 버전의 ASP.NET Web Forms 다양 한 데이터로 작업 하는 경우 사용자 환경 개선에 집중 하는 향상 된 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-106">The new version of ASP.NET Web Forms introduces a number of improvements focused on improving user experience when working with data.</span></span>
> 
> <span data-ttu-id="12d02-107">Web Forms, 데이터 바인딩 사용 하 여 개체 멤버의 값을 내보낼 때의 이전 버전에서는 bind () 또는 eval () 데이터 바인딩 식을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-107">In previous versions of Web Forms, when using data-binding to emit the value of an object member, you used the data-binding expressions Bind() or Eval().</span></span> <span data-ttu-id="12d02-108">새 버전의 ASP.NET에서 수 있다면 어떤 형식의 데이터 컨트롤을 새 ItemType 속성을 사용 하 여 바인딩할 것을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-108">In the new version of ASP.NET, you are able to declare what type of data a control is going to be bound to by using a new ItemType property.</span></span> <span data-ttu-id="12d02-109">이 속성을 설정 하면 강력한 형식의 변수를 사용 하 여 IntelliSense, 멤버 탐색 및 컴파일 타임 검사와 같은 Visual Studio 개발 환경의 전체 혜택을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-109">Setting this property will enable you to use a strongly-typed variable to receive the full benefits of the Visual Studio development experience, such as IntelliSense, member navigation, and compile-time checking.</span></span>
> 
> <span data-ttu-id="12d02-110">데이터 바인딩된 컨트롤을 사용 하 여 이제 지정할 수 있습니다도 선택, 업데이트, 삭제 및 데이터를 삽입에 대 한 사용자 고유의 사용자 지정 메서드 페이지 컨트롤 및 응용 프로그램 논리 간의 상호 작용을 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-110">With the data-bound controls, you can now also specify your own custom methods for selecting, updating, deleting and inserting data, simplifying the interaction between the page controls and your application logic.</span></span> <span data-ttu-id="12d02-111">또한 메서드 형식 매개 변수로 직접 페이지에서 데이터를 매핑할 수 있습니다 즉 asp.net 모델 바인딩 기능이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-111">Additionally, model binding capabilities have been added to ASP.NET, which means you can map data from the page directly into method type parameters.</span></span>
> 
> <span data-ttu-id="12d02-112">사용자 입력 유효성 검사 Web Forms의 최신 버전을 사용 하 여 더 쉬울 수도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-112">Validating user input should also be easier with the latest version of Web Forms.</span></span> <span data-ttu-id="12d02-113">유효성 검사 특성을 사용 하 여 모델 클래스를 이제 주석을 달 수 있습니다 합니다 **System.ComponentModel.DataAnnotations** 네임 스페이스 및 모든 사이트를 제어 하는 요청 사용자 정보를 사용 하 여 입력의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-113">You can now annotate your model classes with validation attributes from the **System.ComponentModel.DataAnnotations** namespace and request that all your site controls validate user input using that information.</span></span> <span data-ttu-id="12d02-114">Web Forms에서 클라이언트 쪽 유효성 검사는 jQuery, 수행 되는 클리너 클라이언트 쪽 코드 및 비 가시적인 JavaScript 기능을 제공 통합 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-114">Client-side validation in Web Forms is now integrated with jQuery, providing cleaner client-side code and unobtrusive JavaScript features.</span></span>
> 
> <span data-ttu-id="12d02-115">요청 유효성 검사 영역에서 향상 된 기능을 선택적으로 응용 프로그램의 특정 부분에 대 한 요청 유효성 검사를 해제 하거나 무효화 요청 데이터를 읽을 수 있도록 이루어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-115">In the request validation area, improvements have been made to make it easier to selectively turn off request validation for specific parts of your applications or read invalidated request data.</span></span>
> 
> <span data-ttu-id="12d02-116">몇 가지 개선이 이루어졌습니다 Web forms 서버 컨트롤 HTML5의 새로운 기능을 활용 하려면:</span><span class="sxs-lookup"><span data-stu-id="12d02-116">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>
> 
> - <span data-ttu-id="12d02-117">TextBox 컨트롤의 텍스트 모드 속성은 전자 메일, datetime 등 새 HTML5 입력된 형식을 지원 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-117">The TextMode property of the TextBox control has been updated to support the new HTML5 input types like email, datetime, and so on.</span></span>
> - <span data-ttu-id="12d02-118">이제 FileUpload 컨트롤이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-118">The FileUpload control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
> - <span data-ttu-id="12d02-119">유효성 검사기는 이제 지원 유효성 검사 HTML5 입력된 요소를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-119">Validator controls now support validating HTML5 input elements.</span></span>
> - <span data-ttu-id="12d02-120">이제 URL을 나타내는 특성이 있는 새 HTML5 요소 지원 runat =&quot;server&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-120">New HTML5 elements that have attributes that represent a URL now support runat=&quot;server&quot;.</span></span> <span data-ttu-id="12d02-121">결과적으로 같은 사용할 수 있습니다 ASP.NET 규칙 URL 경로에 ~를 나타내는 응용 프로그램 루트 연산자 (예를 들어 &lt;비디오 runat =&quot;server&quot; src =&quot;~/myVideo.wmv&quot; &gt; &lt;비디오/&gt;).</span><span class="sxs-lookup"><span data-stu-id="12d02-121">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat=&quot;server&quot; src=&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;).</span></span>
> - <span data-ttu-id="12d02-122">UpdatePanel 컨트롤 게시 HTML5 입력된 필드를 지원 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-122">The UpdatePanel control has been fixed to support posting HTML5 input fields.</span></span>
> 
> <span data-ttu-id="12d02-123">공식 ASP.NET 포털에서 ASP.NET WebForms 4.5의 새로운 기능의 더 많은 예제를 찾을 수 있습니다: [ASP.NET 4.5와 Visual Studio 2012의 새로운 기능](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)</span><span class="sxs-lookup"><span data-stu-id="12d02-123">In the official ASP.NET portal you can find more examples of the new features in ASP.NET WebForms 4.5: [What's New in ASP.NET 4.5 and Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)</span></span>
> 
> <span data-ttu-id="12d02-124">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-124">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="12d02-125">목표</span><span class="sxs-lookup"><span data-stu-id="12d02-125">Objectives</span></span>

<span data-ttu-id="12d02-126">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="12d02-126">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="12d02-127">강력한 데이터 바인딩 식을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="12d02-127">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="12d02-128">Web Forms에서 새 모델 바인딩 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-128">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="12d02-129">값 공급자를 사용 하 여 코드 숨김 방법 페이지 데이터를 매핑하기 위한</span><span class="sxs-lookup"><span data-stu-id="12d02-129">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="12d02-130">사용자 입력된 유효성 검사에 대 한 데이터 주석 사용</span><span class="sxs-lookup"><span data-stu-id="12d02-130">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="12d02-131">Web Forms에서 advange jQuery 사용한 unobstrusive 클라이언트 쪽 유효성 검사의 수행</span><span class="sxs-lookup"><span data-stu-id="12d02-131">Take advange of unobstrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="12d02-132">세분화 된 요청 유효성 검사 구현</span><span class="sxs-lookup"><span data-stu-id="12d02-132">Implement granular request validation</span></span>
- <span data-ttu-id="12d02-133">Web Forms에서 처리 하는 비동기 페이지를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-133">Implement asynchronous page processing in Web Forms</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="12d02-134">전제 조건</span><span class="sxs-lookup"><span data-stu-id="12d02-134">Prerequisites</span></span>

<span data-ttu-id="12d02-135">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-135">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="12d02-136">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="12d02-136">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="12d02-137">설정</span><span class="sxs-lookup"><span data-stu-id="12d02-137">Setup</span></span>

<span data-ttu-id="12d02-138">**설치 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="12d02-138">**Installing Code Snippets**</span></span>

<span data-ttu-id="12d02-139">편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-139">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="12d02-140">설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-140">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="12d02-141">이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 c:를 사용 하 여 코드 조각](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-141">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="12d02-142">연습</span><span class="sxs-lookup"><span data-stu-id="12d02-142">Exercises</span></span>

<span data-ttu-id="12d02-143">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-143">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="12d02-144">연습 1: 모델 ASP.NET Web Forms에서 바인딩</span><span class="sxs-lookup"><span data-stu-id="12d02-144">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>](#Exercise1)
2. [<span data-ttu-id="12d02-145">연습 2: 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="12d02-145">Exercise 2: Data Validation</span></span>](#Exercise2)
3. [<span data-ttu-id="12d02-146">연습 3: 비동기 페이지 처리에 ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="12d02-146">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="12d02-147">각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-147">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="12d02-148">이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-148">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="12d02-149">이 랩을 완료 하기 위한 예상 시간: **60 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-149">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a><span data-ttu-id="12d02-150">연습 1: 모델 ASP.NET Web Forms에서 바인딩</span><span class="sxs-lookup"><span data-stu-id="12d02-150">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>

<span data-ttu-id="12d02-151">ASP.NET Web Forms의 새 버전의 데이터로 작업할 때 환경 개선에 집중 하는 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-151">The new version of ASP.NET Web Forms introduces a number of enhancements focused on improving the experience when working with data.</span></span> <span data-ttu-id="12d02-152">이 연습에서는 전체에서 강력한 형식의 데이터 컨트롤에 알아봅니다을 모델 바인딩.</span><span class="sxs-lookup"><span data-stu-id="12d02-152">Throughout this exercise, you will learn about strongly typed data-controls and model binding.</span></span>

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a><span data-ttu-id="12d02-153">작업 1-강력한 형식의 데이터 바인딩을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="12d02-153">Task 1 - Using Strongly-Typed Data-Bindings</span></span>

<span data-ttu-id="12d02-154">이 태스크에서는 ASP.NET 4.5에서 사용할 수 있는 새 강력한 형식의 바인딩 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-154">In this task, you will discover the new strongly-typed bindings available in ASP.NET 4.5.</span></span>

1. <span data-ttu-id="12d02-155">엽니다는 **시작할** 솔루션에 있는 **소스/e x 1-ModelBinding/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="12d02-155">Open the **Begin** solution located at **Source/Ex1-ModelBinding/Begin/** folder.</span></span>

   1. <span data-ttu-id="12d02-156">일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-156">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="12d02-157">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-157">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="12d02-158">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="12d02-158">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="12d02-159">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-159">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="12d02-160">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-160">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="12d02-161">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-161">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="12d02-162">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-162">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="12d02-163">엽니다는 **Customers.aspx** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-163">Open the **Customers.aspx** page.</span></span> <span data-ttu-id="12d02-164">주 컨트롤에는 번호가 없는 목록을 배치 하 고 각 고객을 나열 하기 위한 내부 repeater 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-164">Place an unnumbered list in the main control and include a repeater control inside for listing each customer.</span></span> <span data-ttu-id="12d02-165">반복기 이름으로 설정할 **customersRepeater** 다음 코드와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-165">Set the repeater name to **customersRepeater** as shown in the following code.</span></span>

    <span data-ttu-id="12d02-166">Web Forms의 이전 버전의 경우 데이터 바인딩 개체에 대 한 멤버의 값을 내보낼 데이터 바인딩을 사용 하는 경우에 사용할는 Eval 메서드를 호출 하는 데이터 바인딩 식 전달 멤버의 이름을 문자열로 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-166">In previous versions of Web Forms, when using data-binding to emit the value of a member on an object you're data-binding to, you would use a data-binding expression, along with a call to the Eval method, passing in the name of the member as a string.</span></span>

    <span data-ttu-id="12d02-167">런타임 시 이러한 호출 Eval 현재 바인딩된 개체에 대해 리플렉션을 사용 하 여 지정 된 이름의 멤버의 값을 읽을 수를 HTML의 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-167">At runtime, these calls to Eval will use reflection against the currently bound object to read the value of the member with the given name, and display the result in the HTML.</span></span> <span data-ttu-id="12d02-168">이 방법은 매우 쉽게 unshaped 임의의 데이터에 대 한 데이터 바인딩.</span><span class="sxs-lookup"><span data-stu-id="12d02-168">This approach makes it very easy to data-bind against arbitrary, unshaped data.</span></span>

    <span data-ttu-id="12d02-169">그러나 다양 한 지원 (예: 정의로 이동), 탐색 및 컴파일 타임 검사, 멤버 이름에 대 한 IntelliSense를 비롯 한 Visual Studio에서 개발 타임 환경을 개선 기능 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-169">Unfortunately, you lose many of the great development-time experience features in Visual Studio, including IntelliSense for member names, support for navigation (like Go To Definition), and compile-time checking.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. <span data-ttu-id="12d02-170">엽니다는 **Customers.aspx.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-170">Open the **Customers.aspx.cs** file.</span></span>
4. <span data-ttu-id="12d02-171">다음 추가 문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-171">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. <span data-ttu-id="12d02-172">에 **페이지\_부하** 메서드를 고객의 목록 사용 하 여 반복기를 채우는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-172">In the **Page\_Load** method, add code to populate the repeater with the list of customers.</span></span>

    <span data-ttu-id="12d02-173">(코드 조각- *Forms 랩-Ex01-고객은 데이터 원본 바인드 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-173">(Code Snippet - *Web Forms Lab - Ex01 - Bind Customers Data Source*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    <span data-ttu-id="12d02-174">솔루션은 codefirst의 경우 함께 EntityFramework를 사용 하 여 만들고 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-174">The solution uses EntityFramework together with CodeFirst to create and access the database.</span></span> <span data-ttu-id="12d02-175">다음 코드에서는 customersRepeater 데이터베이스에서 모든 고객을 반환 하는 구체화 된 쿼리에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-175">In the following code, the customersRepeater is bound to a materialized query that returns all the customers from the database.</span></span>
6. <span data-ttu-id="12d02-176">키를 눌러 **F5** 솔루션을 실행 하 고 이동 하는 **고객** 페이지를 실행 중인 repeater를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="12d02-176">Press **F5** to run the solution and go to the **Customers** page to see the repeater in action.</span></span> <span data-ttu-id="12d02-177">솔루션에는 codefirst의 경우 사용 하는, 데이터베이스를 생성 하 고 응용 프로그램을 실행 하는 경우에 로컬 SQL Express 인스턴스에서 채워집니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-177">As the solution is using CodeFirst, the database will be created and populated in your local SQL Express instance when running the application.</span></span>

    <span data-ttu-id="12d02-178">![Repeater 사용 하 여 고객을 나열](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "repeater 사용 하 여 고객 목록")</span><span class="sxs-lookup"><span data-stu-id="12d02-178">![Listing the customers with a repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Listing the customers with a repeater")</span></span>

    <span data-ttu-id="12d02-179">*Repeater 사용 하 여 고객 목록*</span><span class="sxs-lookup"><span data-stu-id="12d02-179">*Listing the customers with a repeater*</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-180">Visual Studio 2012의 IIS Express는 기본 웹 개발 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-180">In Visual Studio 2012, IIS Express is the default Web development server.</span></span>
7. <span data-ttu-id="12d02-181">브라우저를 닫고 Visual Studio로 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-181">Close the browser and go back to Visual Studio.</span></span>
8. <span data-ttu-id="12d02-182">이제 강력한 형식의 바인딩을 사용 하는 구현을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-182">Now replace the implementation to use strongly typed bindings.</span></span> <span data-ttu-id="12d02-183">엽니다는 **Customers.aspx** 페이지를 사용 하 여 새 **ItemType** 특성을 설정 하는 반복기에는 **고객** 바인딩 형식으로 형식.</span><span class="sxs-lookup"><span data-stu-id="12d02-183">Open the **Customers.aspx** page and use the new **ItemType** attribute in the repeater to set the **Customer** type as the binding type.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    <span data-ttu-id="12d02-184">ItemType 속성을 사용 하면 어떤 유형의 데이터 컨트롤에 바인딩할 수 및 사용 하면 강력한 형식의 데이터 바인딩된 컨트롤 내에서 바인딩 선언에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-184">The ItemType property enables you to declare which type of data the control is going to be bound to and allows you to use strongly-typed binding inside the data-bound control.</span></span>
9. <span data-ttu-id="12d02-185">ItemTemplate 콘텐츠를 다음 코드로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-185">Replace the ItemTemplate content with the following code.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    <span data-ttu-id="12d02-186">위의 방법으로 단점 중 하나는 eval () 및 bind ()에 대 한 호출 바인딩된-속성 이름을 나타내는 문자열을 전달 하면 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-186">One downside with the above approaches is that the calls to Eval() and Bind() are late-bound - meaning you pass strings to represent the property names.</span></span> <span data-ttu-id="12d02-187">즉, 멤버 이름, (예: 정의로 이동), 코드 탐색에 대 한 지원 하거나 컴파일 타임 검사 지원에 대 한 Intellisense를 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-187">This means you don't get Intellisense for the member names, support for code navigation (like Go To Definition), nor compile-time checking support.</span></span>

    <span data-ttu-id="12d02-188">ItemType 속성을 설정 하면 데이터 바인딩 식의 범위에 생성 될 새 형식화 된 변수를 두 개: **항목** 하 고 **binditem을**입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-188">Setting the ItemType property causes two new typed variables to be generated in the scope of the data-binding expressions: **Item** and **BindItem**.</span></span> <span data-ttu-id="12d02-189">데이터 바인딩 식에서 이러한 강력한 형식의 변수를 사용할 수 있으며 Visual Studio 개발 환경의 모든 혜택을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-189">You can use these strongly typed variables in the data-binding expressions and get the full benefits of the Visual Studio development experience.</span></span>

    <span data-ttu-id="12d02-190">&quot; **:** &quot; 식에 사용 됩니다 자동으로 HTML 인코딩 보안 문제 (예: 사이트 간 스크립팅 공격)를 방지 하려면 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-190">The &quot;**:** &quot; used in the expression will automatically HTML-encode the output to avoid security issues (for example, cross-site scripting attacks).</span></span> <span data-ttu-id="12d02-191">이 표기법 사용 가능한.NET 4 이후를 작성 하는 응답에 대 한 되었지만 이제도 데이터 바인딩 식에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-191">This notation was available since .NET 4 for response writing, but now is also available in data-binding expressions.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-192">단방향 바인딩 항목 멤버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-192">The Item member works for one-way binding.</span></span> <span data-ttu-id="12d02-193">양방향 바인딩을 사용 하 여 수행 하려는 경우는 **binditem을** 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-193">If you want to perform two-way binding use the **BindItem** member.</span></span>

    <span data-ttu-id="12d02-194">![강력한 형식의 바인딩에 IntelliSense 지원을](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "바인딩에 강력한 IntelliSense 지원")</span><span class="sxs-lookup"><span data-stu-id="12d02-194">![IntelliSense support in strongly-typed binding](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "IntelliSense support in strongly-typed binding")</span></span>

    <span data-ttu-id="12d02-195">*강력한 형식의 바인딩에 IntelliSense 지원*</span><span class="sxs-lookup"><span data-stu-id="12d02-195">*IntelliSense support in strongly-typed binding*</span></span>
10. <span data-ttu-id="12d02-196">키를 눌러 **F5** 솔루션을 실행 하 여 변경 내용이 예상 대로 작동 하는지 확인 하려면 고객 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-196">Press **F5** to run the solution and go to the Customers page to make sure the changes work as expected.</span></span>

    <span data-ttu-id="12d02-197">![고객 세부 정보를 나열](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "고객 세부 정보를 나열 합니다.")</span><span class="sxs-lookup"><span data-stu-id="12d02-197">![Listing customer details](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "Listing customer details")</span></span>

    <span data-ttu-id="12d02-198">*고객 세부 정보를 나열합니다.*</span><span class="sxs-lookup"><span data-stu-id="12d02-198">*Listing customer details*</span></span>
11. <span data-ttu-id="12d02-199">브라우저를 닫고 Visual Studio로 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-199">Close the browser and go back to Visual Studio.</span></span>

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a><span data-ttu-id="12d02-200">작업 2-Web Forms에서 바인딩 소개 모델</span><span class="sxs-lookup"><span data-stu-id="12d02-200">Task 2 - Introducing Model Binding in Web Forms</span></span>

<span data-ttu-id="12d02-201">ASP.NET Web Forms의 이전 버전을 모두 검색 하 고 데이터 업데이트, 양방향 데이터 바인딩을 수행 하려는 경우 데이터 원본 개체를 사용 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-201">In previous versions of ASP.NET Web Forms, when you wanted to perform two-way data-binding, both retrieving and updating data, you needed to use a Data Source object.</span></span> <span data-ttu-id="12d02-202">이 수 개체 데이터 소스, SQL 데이터 원본, LINQ 데이터 소스 등입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-202">This could be an Object Data Source, a SQL Data Source, a LINQ Data Source and so on.</span></span> <span data-ttu-id="12d02-203">그러나 시나리오에 데이터를 처리 하는 것에 대 한 사용자 지정 코드를 필요한 경우 개체 데이터 소스를 사용 하는 데 필요한 만들었다가이 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-203">However if your scenario required custom code for handling the data, you needed to use the Object Data Source and this brought some drawbacks.</span></span> <span data-ttu-id="12d02-204">예를 들어, 한 복합 형식을 방지 하는 데 필요한 및 유효성 검사 논리를 실행 하는 경우 예외를 처리 하는 데 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-204">For example, you needed to avoid complex types and you needed to handle exceptions when executing validation logic.</span></span>

<span data-ttu-id="12d02-205">데이터 바인딩된 컨트롤을 새 버전의 ASP.NET Web Forms에서 모델 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-205">In the new version of ASP.NET Web Forms the data-bound controls support model binding.</span></span> <span data-ttu-id="12d02-206">이 수 선택 지정, 업데이트, 추가 및 삭제 논리를 호출 하 여 코드 숨김 파일에서 또는 다른 클래스에서 데이터 바인딩된 컨트롤에서 직접 메서드를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-206">This means that you can specify select, update, insert and delete methods directly in the data-bound control to call logic from your code-behind file or from another class.</span></span>

<span data-ttu-id="12d02-207">이 알아보려면 사용할지 GridView를 사용 하 여 새 제품 범주를 나열 하려면 **SelectMethod** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-207">To learn about this, you will use a GridView to list the product categories using the new **SelectMethod** attribute.</span></span> <span data-ttu-id="12d02-208">이 특성을 사용 하면 GridView 데이터를 검색 하는 메서드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-208">This attribute enables you to specify a method for retrieving the GridView data.</span></span>

1. <span data-ttu-id="12d02-209">엽니다는 **Products.aspx** 페이지 및 포함을 **GridView**.</span><span class="sxs-lookup"><span data-stu-id="12d02-209">Open the **Products.aspx** page and include a **GridView**.</span></span> <span data-ttu-id="12d02-210">아래와 같이 강력한 형식의 바인딩을 사용 하 여 정렬 및 페이징을 활성화 GridView를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-210">Configure the GridView as shown below to use strongly-typed bindings and enable sorting and paging.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. <span data-ttu-id="12d02-211">새 **SelectMethod** 를 호출 하는 GridView를 구성 하는 특성을 **GetCategories** 데이터를 선택 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-211">Use the new **SelectMethod** attribute to configure the GridView to call a **GetCategories** method to select the data.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. <span data-ttu-id="12d02-212">엽니다는 **Products.aspx.cs** 코드 숨김 파일을 추가한 다음 문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-212">Open the **Products.aspx.cs** code-behind file and add the following using statements.</span></span>

    <span data-ttu-id="12d02-213">(코드 조각- *Forms 랩-Ex01-네임 스페이스 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-213">(Code Snippet - *Web Forms Lab - Ex01 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. <span data-ttu-id="12d02-214">private 멤버를 추가 합니다 **제품** 클래스의 새 인스턴스를 할당 하 고 **ProductsContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-214">Add a private member in the **Products** class and assign a new instance of **ProductsContext**.</span></span> <span data-ttu-id="12d02-215">이 속성은 데이터베이스에 연결할 수 있는 Entity Framework 데이터 컨텍스트를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-215">This property will store the Entity Framework data context that enables you to connect to the database.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. <span data-ttu-id="12d02-216">만들기는 **GetCategories** LINQ를 사용 하 여 범주 목록을 검색 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-216">Create a **GetCategories** method to retrieve the list of categories using LINQ.</span></span> <span data-ttu-id="12d02-217">이 쿼리에 포함 되도록 합니다 **제품** 속성 GridView에는 각 범주에 대 한 제품의 양을 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-217">The query will include the **Products** property so the GridView can show the amount of products for each category.</span></span> <span data-ttu-id="12d02-218">메서드가 반환 되도록 쿼리를 나타내는 원시 IQueryable 개체 실행 페이지 수명 주기 나중에 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-218">Notice that the method returns a raw IQueryable object that represent the query to be executed later on the page lifecycle.</span></span>

    <span data-ttu-id="12d02-219">(코드 조각- *Forms-Ex01-랩 GetCategories 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-219">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="12d02-220">ASP.NET Web Forms의 이전 버전에서는 사용 하도록 설정 하면 정렬 및 페이징, 데이터 원본 개체 컨텍스트 내에서 사용자 고유의 리포지토리 논리를 사용 하 여 하는 데 필요한 사용자 지정 코드를 작성 하 고 필요한 모든 매개 변수를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-220">In previous versions of ASP.NET Web Forms, enabling sorting and paging using your own repository logic within an Object Data Source context, required to write your own custom code and receive all the necessary parameters.</span></span> <span data-ttu-id="12d02-221">데이터 바인딩 메서드는 IQueryable을 반환할 수 있습니다 하 고 쿼리를 나타냅니다이 이제 실행을 계속 ASP.NET 적절 한 정렬을 추가 하려면 쿼리 및 페이징 매개 변수를 수정 하는 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-221">Now, as the data-binding methods can return IQueryable and this represents a query still to be executed, ASP.NET can take care of modifying the query to add the proper sorting and paging parameters.</span></span>
6. <span data-ttu-id="12d02-222">키를 눌러 **F5** 사이트 디버깅을 시작 하 여 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-222">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="12d02-223">GridView GetCategories 메서드에서 반환 되는 범주를 사용 하 여 채워져 있는지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-223">You should see that the GridView is populated with the categories returned by the GetCategories method.</span></span>

    <span data-ttu-id="12d02-224">![모델 바인딩을 사용 하 여 GridView를 채우기를](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "모델 바인딩을 사용 하 여 GridView를 채우기를")</span><span class="sxs-lookup"><span data-stu-id="12d02-224">![Populating a GridView using model binding](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "Populating a GridView using model binding")</span></span>

    <span data-ttu-id="12d02-225">*모델 바인딩을 사용 하 여 GridView를 채우기를*</span><span class="sxs-lookup"><span data-stu-id="12d02-225">*Populating a GridView using model binding*</span></span>
7. <span data-ttu-id="12d02-226">키를 눌러 **SHIFT**+**F5** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-226">Press **SHIFT**+**F5** Stop debugging.</span></span>

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a><span data-ttu-id="12d02-227">작업 3-모델 바인딩에 대 한 값 공급자</span><span class="sxs-lookup"><span data-stu-id="12d02-227">Task 3 - Value Providers in Model Binding</span></span>

<span data-ttu-id="12d02-228">모델 바인딩 데이터 바인딩된 컨트롤에서 직접 데이터를 사용 하려면 사용자 지정 메서드를 지정할 수 뿐만 아니라 데이터 페이지에서 이러한 메서드에서 매개 변수를 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-228">Model binding not only enables you to specify custom methods to work with your data directly in the data-bound control, but also allows you to map data from the page into parameters from these methods.</span></span> <span data-ttu-id="12d02-229">메서드 매개 변수에 값의 데이터 원본을 지정 하려면 값 공급자 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-229">On the method parameter, you can use value provider attributes to specify the value's data source.</span></span> <span data-ttu-id="12d02-230">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="12d02-230">For example:</span></span>

- <span data-ttu-id="12d02-231">페이지의 컨트롤</span><span class="sxs-lookup"><span data-stu-id="12d02-231">Controls on the page</span></span>
- <span data-ttu-id="12d02-232">쿼리 문자열 값</span><span class="sxs-lookup"><span data-stu-id="12d02-232">Query string values</span></span>
- <span data-ttu-id="12d02-233">데이터 보기</span><span class="sxs-lookup"><span data-stu-id="12d02-233">View data</span></span>
- <span data-ttu-id="12d02-234">세션 상태</span><span class="sxs-lookup"><span data-stu-id="12d02-234">Session state</span></span>
- <span data-ttu-id="12d02-235">쿠키</span><span class="sxs-lookup"><span data-stu-id="12d02-235">Cookies</span></span>
- <span data-ttu-id="12d02-236">게시 된 양식 데이터</span><span class="sxs-lookup"><span data-stu-id="12d02-236">Posted form data</span></span>
- <span data-ttu-id="12d02-237">뷰 상태</span><span class="sxs-lookup"><span data-stu-id="12d02-237">View state</span></span>
- <span data-ttu-id="12d02-238">사용자 지정 값 공급자도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-238">Custom value providers are supported as well</span></span>

<span data-ttu-id="12d02-239">ASP.NET MVC 4를 사용한 모델 바인딩 지원은 유사한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-239">If you have used ASP.NET MVC 4, you will notice the model binding support is similar.</span></span> <span data-ttu-id="12d02-240">실제로 이러한 기능은 ASP.NET MVC에서 수행 되었으며로 이동 합니다 **System.Web** 어셈블리 에서도 Web Forms에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-240">Indeed, these features were taken from ASP.NET MVC and moved into the **System.Web** assembly to be able to use them on Web Forms as well.</span></span>

<span data-ttu-id="12d02-241">이 태스크에서는 모델 바인딩을 사용 하 여 filter 매개 변수를 받는 각 범주에 대 한 제품의 양에 따라 결과 필터링 할 GridView 업데이트할는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-241">In this task, you will update the GridView to filter its results by the amount of products for each category, receiving the filter parameter with model binding.</span></span>

1. <span data-ttu-id="12d02-242">로 다시 이동 합니다 **Products.aspx** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-242">Go back to the **Products.aspx** page.</span></span>
2. <span data-ttu-id="12d02-243">GridView의 맨 위에 추가 **레이블을** 및 **ComboBox** 아래와 같이 각 범주에 대 한 제품의 수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-243">At the top of the GridView, add a **Label** and a **ComboBox** to select the number of products for each category as shown below.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. <span data-ttu-id="12d02-244">추가 된 **있도록 EmptyDataTemplate** 경우 선택한 제품 수를 사용 하 여 범주 없음 메시지를 표시 하려면 GridView에 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-244">Add an **EmptyDataTemplate** to the GridView to show a message when there are no categories with the selected number of products.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. <span data-ttu-id="12d02-245">엽니다는 **Products.aspx.cs** 코드 숨김 및 다음을 추가 합니다 문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-245">Open the **Products.aspx.cs** code-behind and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. <span data-ttu-id="12d02-246">수정 합니다 **GetCategories** 정수를 수신 하는 방법 **minProductsCount** 인수 및 반환된 된 결과 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-246">Modify the **GetCategories** method to receive an integer **minProductsCount** argument and filter the returned results.</span></span> <span data-ttu-id="12d02-247">이 위해 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-247">To do this, replace the method with the following code.</span></span>

    <span data-ttu-id="12d02-248">(코드 조각- *Forms-Ex01-랩 GetCategories 2 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-248">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    <span data-ttu-id="12d02-249">새 **[컨트롤]** 특성을 **minProductsCount** 인수 ASP.NET 페이지에서 컨트롤을 사용 하 여 해당 값을 채워야 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-249">The new **[Control]** attribute on the **minProductsCount** argument will let ASP.NET know its value must be populated using a control in the page.</span></span> <span data-ttu-id="12d02-250">ASP.NET은 인수 (minProductsCount)의 이름과 일치 하는 모든 컨트롤에 대 한 확인 하 고 변환 컨트롤 값을 사용 하 여 매개 변수를 입력 하 고 필요한 매핑을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-250">ASP.NET will look for any control matching the name of the argument (minProductsCount) and perform the necessary mapping and conversion to fill the parameter with the control value.</span></span>

    <span data-ttu-id="12d02-251">또는 특성 값을 가져올 수 있는 위치에서 제어를 지정할 수 있는 오버 로드 된 생성자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-251">Alternatively, the attribute provides an overloaded constructor that enables you to specify the control from where to get the value.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-252">데이터 바인딩 기능에의 한 가지 목표 페이지 상호 작용을 위해 작성 해야 하는 코드의 양을 줄이는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-252">One goal of the data-binding features is to reduce the amount of code that needs to be written for page interaction.</span></span> <span data-ttu-id="12d02-253">[컨트롤] 값 공급자 외에도 메서드 매개 변수에서 다른 모델 바인딩 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-253">Apart from the [Control] value provider, you can use other model-binding providers in your method parameters.</span></span> <span data-ttu-id="12d02-254">그 중 일부는 작업 도입에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-254">Some of them are listed in the task introduction.</span></span>
6. <span data-ttu-id="12d02-255">키를 눌러 **F5** 사이트 디버깅을 시작 하 여 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-255">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="12d02-256">드롭다운 목록에서 제품을 선택 하 고 GridView 이제 업데이트 되는 방식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-256">Select a number of products in the drop-down list and notice how the GridView is now updated.</span></span>

    <span data-ttu-id="12d02-257">![필터링 드롭다운 목록에서 값을 사용 하 여 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "드롭다운 목록에서 값을 사용 하 여 GridView를 필터링 합니다.")</span><span class="sxs-lookup"><span data-stu-id="12d02-257">![Filtering the GridView with a drop-down list value](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "Filtering the GridView with a drop-down list value")</span></span>

    <span data-ttu-id="12d02-258">*드롭다운 목록에서 값을 사용 하 여 GridView를 필터링합니다.*</span><span class="sxs-lookup"><span data-stu-id="12d02-258">*Filtering the GridView with a drop-down list value*</span></span>
7. <span data-ttu-id="12d02-259">디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-259">Stop debugging.</span></span>

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a><span data-ttu-id="12d02-260">작업 4-를 사용 하 여 모델을 필터링 하는 것에 대 한 바인딩</span><span class="sxs-lookup"><span data-stu-id="12d02-260">Task 4 - Using Model Binding for Filtering</span></span>

<span data-ttu-id="12d02-261">이 태스크에서는 선택한 범주에 포함 된 제품을 표시 하는 GridView 자식 보조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-261">In this task, you will add a second, child GridView to show the products within the selected category.</span></span>

1. <span data-ttu-id="12d02-262">엽니다는 **Products.aspx** 페이지 및 범주 선택 단추를 자동으로 생성 하는 GridView를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-262">Open the **Products.aspx** page and update the categories GridView to auto-generate the Select button.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. <span data-ttu-id="12d02-263">두 번째 추가 **GridView** 라는 **productsGrid** 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-263">Add a second **GridView** named **productsGrid** at the bottom.</span></span> <span data-ttu-id="12d02-264">설정 합니다 **ItemType** 하 **WebFormsLab.Model.Product**의 **DataKeyNames** 에 **ProductId** 및 **SelectMethod**  하 **GetProducts**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-264">Set the **ItemType** to **WebFormsLab.Model.Product**, the **DataKeyNames** to **ProductId** and the **SelectMethod** to **GetProducts**.</span></span> <span data-ttu-id="12d02-265">설정할 **AutoGenerateColumns** 하 **false** ProductId, ProductName, 설명 및 UnitPrice에 대 한 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-265">Set **AutoGenerateColumns** to **false** and add the columns for ProductId, ProductName, Description and UnitPrice.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. <span data-ttu-id="12d02-266">엽니다는 **Products.aspx.cs** 코드 숨김 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-266">Open the **Products.aspx.cs** code-behind file.</span></span> <span data-ttu-id="12d02-267">구현 된 **GetProducts** GridView 범주에서 범주 ID를 받고 제품을 필터링 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="12d02-267">Implement the **GetProducts** method to receive the category ID from the category GridView and filter the products.</span></span> <span data-ttu-id="12d02-268">모델 바인딩에에서 선택한 행을 사용 하 여 매개 변수 값을 설정 합니다 **categoriesGrid**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-268">Model binding will set the parameter value using the selected row in the **categoriesGrid**.</span></span> <span data-ttu-id="12d02-269">인수 이름 및 컨트롤 이름을 일치 하지 않으면 이후 컨트롤 값 공급자에서 컨트롤의 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-269">Since the argument name and control name do not match, you should specify the name of the control in the Control value provider.</span></span>

    <span data-ttu-id="12d02-270">(코드 조각- *Forms-Ex01-랩 GetProducts 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-270">(Code Snippet - *Web Forms Lab - Ex01 - GetProducts*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="12d02-271">이 접근 방식을 쉽게 단위 이러한 메서드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-271">This approach makes it easier to unit test these methods.</span></span> <span data-ttu-id="12d02-272">여기서 Web Forms는 실행할 수 없습니다, 단위 테스트 컨텍스트를에서 [컨트롤] 특성은 특정 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-272">On a unit test context, where Web Forms is not executing, the [Control] attribute will not perform any specific action.</span></span>
4. <span data-ttu-id="12d02-273">엽니다는 **Products.aspx** 페이지 및 GridView 제품을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-273">Open the **Products.aspx** page and locate the products GridView.</span></span> <span data-ttu-id="12d02-274">선택한 제품을 편집 하는 것에 대 한 링크를 표시 하는 GridView 제품을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-274">Update the products GridView to show a link for editing the selected product.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. <span data-ttu-id="12d02-275">엽니다는 **ProductDetails.aspx** 바꾸고 코드 숨김 페이지의 **SelectProduct** 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-275">Open the **ProductDetails.aspx** page code-behind and replace the **SelectProduct** method with the following code.</span></span>

    <span data-ttu-id="12d02-276">(코드 조각- *Forms-Ex01-랩 SelectProduct 메서드 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-276">(Code Snippet - *Web Forms Lab - Ex01 - SelectProduct Method*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="12d02-277">에 **[QueryString]** 특성은 쿼리 문자열에는 productId 매개 변수에서 메서드 매개 변수를 채우는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-277">Notice that the **[QueryString]** attribute is used to fill the method parameter from a productId parameter in the query string.</span></span>
6. <span data-ttu-id="12d02-278">키를 눌러 **F5** 사이트 디버깅을 시작 하 여 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-278">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="12d02-279">GridView 범주의 모든 범주를 선택 하 고 제품 GridView 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-279">Select any category from the categories GridView and notice that the products GridView is updated.</span></span>

    <span data-ttu-id="12d02-280">![선택한 범주에서 제품을 보여 주는](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "선택한 범주의 제품 표시")</span><span class="sxs-lookup"><span data-stu-id="12d02-280">![Showing products from the selected category](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "Showing products from the selected category")</span></span>

    <span data-ttu-id="12d02-281">*선택한 범주의 제품 표시*</span><span class="sxs-lookup"><span data-stu-id="12d02-281">*Showing products from the selected category*</span></span>
7. <span data-ttu-id="12d02-282">클릭 합니다 **보기** ProductDetails.aspx 페이지를 열려면 제품에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-282">Click the **View** link on a product to open the ProductDetails.aspx page.</span></span>

    <span data-ttu-id="12d02-283">쿼리 문자열에서 productId 매개 변수를 사용 하는 SelectMethod를 사용 하 여 제품 페이지를 검색 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-283">Notice that the page is retrieving the product with the SelectMethod using the productId parameter from the query string.</span></span>

    <span data-ttu-id="12d02-284">![제품 세부 정보를 보는](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "제품 세부 정보 보기")</span><span class="sxs-lookup"><span data-stu-id="12d02-284">![Viewing the product details](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "Viewing the product details")</span></span>

    <span data-ttu-id="12d02-285">*제품 세부 정보 보기*</span><span class="sxs-lookup"><span data-stu-id="12d02-285">*Viewing the product details*</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-286">HTML에 대 한 설명을 입력할 수 있도록 다음 연습에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-286">The ability to type an HTML description will be implemented in the next exercise.</span></span>

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a><span data-ttu-id="12d02-287">작업 5-를 사용 하 여 모델 업데이트 작업에 대 한 바인딩</span><span class="sxs-lookup"><span data-stu-id="12d02-287">Task 5 - Using Model Binding for Update Operations</span></span>

<span data-ttu-id="12d02-288">이전 태스크에서 사용한 모델 바인딩을 주로 데이터를 선택 하면,이 작업에서 업데이트 작업에서 모델 바인딩을 사용 하는 방법을 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-288">In the previous task, you have used model binding mainly for selecting data, in this task you will learn how to use model binding in update operations.</span></span>

<span data-ttu-id="12d02-289">사용자가 범주를 업데이트 하는 GridView 범주를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-289">You will update the categories GridView to let the user update categories.</span></span>

1. <span data-ttu-id="12d02-290">엽니다는 **Products.aspx** 페이지 및 GridView 편집 단추를 자동으로 생성 하 여 새 범주를 업데이트 **UpdateMethod** 지정 하는 특성을 **UpdateCategory**선택한 항목을 업데이트 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-290">Open the **Products.aspx** page and update the categories GridView to auto-generate the Edit button and use the new **UpdateMethod** attribute to specify an **UpdateCategory** method to update the selected item.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    <span data-ttu-id="12d02-291">GridView DataKeyNames 특성 모델 바인딩된 개체를 고유 하 게 식별 하는 멤버를 정의 하 고 update 메서드를 최소한으로 받아야 매개 변수는 따라서 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-291">The DataKeyNames attribute in the GridView define which are the members that uniquely identify the model-bound object and therefore, which are the parameters the update method should at least receive.</span></span>
2. <span data-ttu-id="12d02-292">엽니다는 **Products.aspx.cs** 코드 숨김 파일 및 구현 합니다 **UpdateCategory** 메서드.</span><span class="sxs-lookup"><span data-stu-id="12d02-292">Open the **Products.aspx.cs** code-behind file and implement the **UpdateCategory** method.</span></span> <span data-ttu-id="12d02-293">메서드는 현재 범주를 로드 하 고 GridView에서 값을 채우는 다음 범주를 업데이트할 범주 ID를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-293">The method should receive the category ID to load the current category, populate the values from the GridView and then update the category.</span></span>

    <span data-ttu-id="12d02-294">(코드 조각- *Forms-Ex01-랩 UpdateCategory 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-294">(Code Snippet - *Web Forms Lab - Ex01 - UpdateCategory*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    <span data-ttu-id="12d02-295">새 **tryupdatemodel에 전달** 페이지 클래스의 메서드는 컨트롤의 값을 사용 하 여 페이지에서 모델 개체를 채우는 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-295">The new **TryUpdateModel** method in the Page class is responsible of populating the model object using the values from the controls in the page.</span></span> <span data-ttu-id="12d02-296">이 경우 업데이트 된 값을 편집 하 고 현재 GridView 행에서 대체할 합니다 **범주** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-296">In this case, it will replace the updated values from the current GridView row being edited into the **category** object.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-297">다음 연습에서는 개체를 편집 하는 경우 사용자가 입력 데이터 유효성 검사에 대 한 ModelState.IsValid의 사용법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-297">The next exercise will explain the usage of the ModelState.IsValid for validating the data entered by the user when editing the object.</span></span>
3. <span data-ttu-id="12d02-298">사이트를 실행 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-298">Run the site and go to the Products page.</span></span> <span data-ttu-id="12d02-299">범주를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-299">Edit a category.</span></span> <span data-ttu-id="12d02-300">새 이름을 입력 하 고 클릭 **업데이트** 의 변경 사항을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-300">Type a new name and then click **Update** to persist the changes.</span></span>

    <span data-ttu-id="12d02-301">![범주 편집](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "범주 편집")</span><span class="sxs-lookup"><span data-stu-id="12d02-301">![Editing categories](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "Editing categories")</span></span>

    <span data-ttu-id="12d02-302">*범주 편집*</span><span class="sxs-lookup"><span data-stu-id="12d02-302">*Editing categories*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a><span data-ttu-id="12d02-303">연습 2: 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="12d02-303">Exercise 2: Data Validation</span></span>

<span data-ttu-id="12d02-304">이 연습에서는 ASP.NET 4.5의 새로운 데이터 유효성 검사 기능에 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-304">In this exercise, you will learn about the new data validation features in ASP.NET 4.5.</span></span> <span data-ttu-id="12d02-305">Web Forms에서 새 비간섭 유효성 검사 기능을 사용해 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-305">You will check out the new unobtrusive validation features in Web Forms.</span></span> <span data-ttu-id="12d02-306">사용자 입력된 유효성 검사를 위해 응용 프로그램 모델 클래스에서 데이터 주석을 사용 하 고 마지막으로, 요청 유효성 검사 페이지에서 개별 컨트롤을 켜거나 끌 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-306">You will use data annotations in the application model classes for user input validation, and finally, you will learn how to turn on or off request validation to individual controls in a page.</span></span>

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a><span data-ttu-id="12d02-307">작업 1-비간섭 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="12d02-307">Task 1 - Unobtrusive Validation</span></span>

<span data-ttu-id="12d02-308">유효성 검사기를 포함 하 여 복잡 한 데이터를 사용 하 여 양식을 코드 중 약 60%를 나타낼 수 있는 페이지에 너무 많은 JavaScript 코드를 생성 하는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-308">Forms with complex data including validators tend to generate too much JavaScript code in the page, which can represent about 60% of the code.</span></span> <span data-ttu-id="12d02-309">비간섭 유효성 검사를 사용 하도록 설정, 사용 하 여 HTML 코드에 보다 명확 하 고 좀 더 깔끔하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-309">With unobtrusive validation enabled, your HTML code will look cleaner and tidier.</span></span>

<span data-ttu-id="12d02-310">이 섹션에서는 두 구성에 의해 생성 된 HTML 코드를 비교 하는 ASP.NET에서 비간섭 유효성 검사 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-310">In this section, you will enable unobtrusive validation in ASP.NET to compare the HTML code generated by both configurations.</span></span>

1. <span data-ttu-id="12d02-311">엽니다 **Visual Studio 2012** 연 합니다 **시작** 솔루션에는 **Source\Ex2 Validation\Begin** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-311">Open **Visual Studio 2012** and open the **Begin** solution located in the **Source\Ex2-Validation\Begin** folder of this lab.</span></span> <span data-ttu-id="12d02-312">또는 이전 연습에서 기존 솔루션에서 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-312">Alternatively, you can continue working on your existing solution from the previous exercise.</span></span>

   1. <span data-ttu-id="12d02-313">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-313">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="12d02-314">이렇게 하려면 솔루션 탐색기에서를 클릭 합니다 **WebFormsLab** 프로젝트 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-314">To do this, in the Solution Explorer, click the **WebFormsLab** project **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="12d02-315">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="12d02-315">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="12d02-316">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-316">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="12d02-317">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-317">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="12d02-318">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-318">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="12d02-319">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-319">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="12d02-320">키를 눌러 **F5** 웹 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-320">Press **F5** to start the web application.</span></span> <span data-ttu-id="12d02-321">고객에 게 페이지를 이동 합니다 **새 고객이 추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-321">Go to the Customers page and click the **Add a New Customer** link.</span></span>
3. <span data-ttu-id="12d02-322">브라우저 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기** 옵션 응용 프로그램에서 생성 된 HTML 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-322">Right-click on the browser page, and select **View Source** option to open the HTML code generated by the application.</span></span>

    <span data-ttu-id="12d02-323">![HTML 코드 페이지를 보여주는](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "HTML 코드 페이지를 표시 합니다.")</span><span class="sxs-lookup"><span data-stu-id="12d02-323">![Showing the page HTML code](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "Showing the page HTML code")</span></span>

    <span data-ttu-id="12d02-324">*HTML 코드 페이지를 표시합니다.*</span><span class="sxs-lookup"><span data-stu-id="12d02-324">*Showing the page HTML code*</span></span>
4. <span data-ttu-id="12d02-325">페이지 소스 코드를 통해 스크롤하여 ASP.NET가 JavaScript 코드 및 데이터의에서 유효성 검사기 페이지 유효성 검사를 수행 하 여 오류 목록 표시를 삽입에 있음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-325">Scroll through the page source code and notice that ASP.NET has injected JavaScript code and data validators in the page to perform the validations and show the error list.</span></span>

    <span data-ttu-id="12d02-326">![CustomerDetails 페이지의 JavaScript 코드를 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails 페이지의 JavaScript 유효성 검사 코드")</span><span class="sxs-lookup"><span data-stu-id="12d02-326">![Validation JavaScript code in CustomerDetails page](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "Validation JavaScript code in CustomerDetails page")</span></span>

    <span data-ttu-id="12d02-327">*CustomerDetails 페이지의 JavaScript 코드를 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="12d02-327">*Validation JavaScript code in CustomerDetails page*</span></span>
5. <span data-ttu-id="12d02-328">브라우저를 닫고 Visual Studio로 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-328">Close the browser and go back to Visual Studio.</span></span>
6. <span data-ttu-id="12d02-329">이제 비간섭 유효성 검사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-329">Now you will enable unobtrusive validation.</span></span> <span data-ttu-id="12d02-330">오픈 **Web.Config** 찾아서 **ValidationSettings:UnobtrusiveValidationMode** 키를 **AppSettings** 섹션 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="12d02-330">Open **Web.Config** and locate **ValidationSettings:UnobtrusiveValidationMode** key in the **AppSettings** section **.**</span></span> <span data-ttu-id="12d02-331">키 값을 설정 **WebForms**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-331">Set the key value to **WebForms**.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > <span data-ttu-id="12d02-332">이 속성을 설정할 수도 있습니다는 &quot; **페이지\_부하** &quot; 일부 페이지에 대해서만 비간섭 유효성 검사를 사용 하도록 설정 하려는 경우에는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-332">You can also set this property in the &quot;**Page\_Load**&quot; event in case you want to enable Unobtrusive Validation only for some pages.</span></span>
7. <span data-ttu-id="12d02-333">오픈 **CustomerDetails.aspx** 누릅니다 **F5** 웹 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-333">Open **CustomerDetails.aspx** and press **F5** to start the Web application.</span></span>
8. <span data-ttu-id="12d02-334">IE 개발자 도구를 열려면 F12 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-334">Press the F12 key to open the IE developer tools.</span></span> <span data-ttu-id="12d02-335">개발자 도구를 열면 스크립트 탭을 선택 합니다. 선택 **CustomerDetails.aspx** 사용 하 고 메뉴에서 페이지에 jQuery를 실행 하는 데 필요한 스크립트는 참고에 로드 되어 로컬 사이트에서 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-335">Once the developer tools is open, select the script tab. Select **CustomerDetails.aspx** from the menu and take note that the scripts required to run jQuery on the page have been loaded into the browser from the local site.</span></span>

    <span data-ttu-id="12d02-336">![로컬 IIS 서버에서 직접 파일을 로드 하는 jQuery JavaScript](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "로컬 IIS 서버에서 직접 파일 jQuery JavaScript를 로드 합니다.")</span><span class="sxs-lookup"><span data-stu-id="12d02-336">![Loading the jQuery JavaScript files directly from the local IIS server](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "Loading the jQuery JavaScript files directly from the local IIS server")</span></span>

    <span data-ttu-id="12d02-337">*로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드*</span><span class="sxs-lookup"><span data-stu-id="12d02-337">*Loading the jQuery JavaScript files directly from the local IIS server*</span></span>
9. <span data-ttu-id="12d02-338">Visual Studio로 돌아가서 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-338">Close the browser to return to Visual Studio.</span></span> <span data-ttu-id="12d02-339">엽니다는 **Site.Master** 찾아서 파일을 다시 합니다 **ScriptManager**.</span><span class="sxs-lookup"><span data-stu-id="12d02-339">Open the **Site.Master** file again and locate the **ScriptManager**.</span></span> <span data-ttu-id="12d02-340">특성을 추가 합니다 **EnableCdn** 속성 값을 가진 **True**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-340">Add the attribute **EnableCdn** property with the value **True**.</span></span> <span data-ttu-id="12d02-341">이렇게 하면 jQuery 로컬 사이트의 URL에서가 아니라 온라인 URL에서 로드 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-341">This will force jQuery to be loaded from the online URL, not from the local site's URL.</span></span>
10. <span data-ttu-id="12d02-342">오픈 **CustomerDetails.aspx** Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="12d02-342">Open **CustomerDetails.aspx** in Visual Studio.</span></span> <span data-ttu-id="12d02-343">사이트를 실행 하려면 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-343">Press the F5 key to run the site.</span></span> <span data-ttu-id="12d02-344">Internet Explorer가 열립니다는 한 번, F12 키를 눌러 개발자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-344">Once Internet Explorer opens, press the F12 key to open the developer tools.</span></span> <span data-ttu-id="12d02-345">선택 된 **스크립트** 탭을 선택한 다음 드롭다운 목록에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-345">Select the **Script** tab, and then take a look at the drop-down list.</span></span> <span data-ttu-id="12d02-346">온라인 jQuery CDN 아니라 로컬 사이트에서 jQuery JavaScript 파일 로드 되 더 이상 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-346">Note the jQuery JavaScript files are no longer being loaded from the local site, but rather from the online jQuery CDN.</span></span>

    <span data-ttu-id="12d02-347">![CDN에서 파일을 로드 하는 jQuery JavaScript](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "CDN에서 파일을 로드 하는 jQuery JavaScript")</span><span class="sxs-lookup"><span data-stu-id="12d02-347">![Loading the jQuery JavaScript files from the CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "Loading the jQuery JavaScript files from the CDN")</span></span>

    <span data-ttu-id="12d02-348">*CDN에서 jQuery JavaScript 파일 로드*</span><span class="sxs-lookup"><span data-stu-id="12d02-348">*Loading the jQuery JavaScript files from the CDN*</span></span>
11. <span data-ttu-id="12d02-349">다시 보기 원본 옵션을 사용 하 여 브라우저에서 HTML 페이지 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-349">Open the HTML page source code again using the View source option in the browser.</span></span> <span data-ttu-id="12d02-350">비간섭 유효성 검사를 사용 하 여 ASP.NET에 삽입된 된 JavaScript 코드와 교체 데이터 알림 \*특성입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-350">Notice that by enabling the unobtrusive validation ASP.NET has replaced the injected JavaScript code with data- \*attributes.</span></span>

    <span data-ttu-id="12d02-351">![비간섭 유효성 검사 코드](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "비간섭 유효성 검사 코드")</span><span class="sxs-lookup"><span data-stu-id="12d02-351">![Unobtrusive validation code](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "Unobtrusive validation code")</span></span>

    <span data-ttu-id="12d02-352">*비간섭 유효성 검사 코드*</span><span class="sxs-lookup"><span data-stu-id="12d02-352">*Unobtrusive validation code*</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-353">이 예제에서는 몇 가지 HTML 및 JavaScript 선만에 유효성 검사 요약 데이터 주석을 사용한 단순화 했습니다. 어떻게 하는 것이 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-353">In this example, you saw how a validation summary with Data annotations was simplified to only a few HTML and JavaScript lines.</span></span> <span data-ttu-id="12d02-354">이전에 비간섭 유효성 검사를 추가 하면 더 많은 유효성 검사 컨트롤 없이 클수록 JavaScript 유효성 검사 코드가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-354">Previously, without unobtrusive validation, the more validation controls you add, the bigger your JavaScript validation code will grow.</span></span>

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a><span data-ttu-id="12d02-355">작업 2-데이터 주석 사용한 모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="12d02-355">Task 2 - Validating the Model with Data Annotations</span></span>

<span data-ttu-id="12d02-356">ASP.NET 4.5 Web Forms에 대 한 데이터 주석 유효성 검사를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-356">ASP.NET 4.5 introduces data annotations validation for Web Forms.</span></span> <span data-ttu-id="12d02-357">각 입력의 유효성 검사 컨트롤 대신 모델 클래스에 제약 조건을 정의 하 고 모든 웹 응용 프로그램에서 사용할 이제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-357">Instead of having a validation control on each input, you can now define constraints in your model classes and use them across all your web application.</span></span> <span data-ttu-id="12d02-358">이 섹션에서는 새로 만들기/편집 고객 양식 유효성 검사에 대 한 데이터 주석을 사용 하는 방법을 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-358">In this section, you will learn how to use data annotations for validating a new/edit customer form.</span></span>

1. <span data-ttu-id="12d02-359">오픈 **CustomerDetail.aspx** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-359">Open **CustomerDetail.aspx** page.</span></span> <span data-ttu-id="12d02-360">고객 이름 및 두 번째 이름를 **EditItemTemplate** 하 고 **먼저** 섹션 RequiredFieldValidator 컨트롤을 사용 하 여 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-360">Notice that the customer first name and second name in the **EditItemTemplate** and **InsertItemTemplate** sections are validated using a RequiredFieldValidator controls.</span></span> <span data-ttu-id="12d02-361">각 유효성 검사기는 확인할 조건으로 만큼 유효성 검사기를 포함 해야 하므로 특정 조건에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-361">Each validator is associated to a particular condition, so you need to include as many validators as conditions to check.</span></span>
2. <span data-ttu-id="12d02-362">데이터 주석 유효성을 검사할 Customer 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-362">Add data annotations to validate the Customer model class.</span></span> <span data-ttu-id="12d02-363">열기 **Customer.cs** 클래스는 **모델** 폴더와 *데코 레이트* 데이터 주석 특성을 사용 하 여 각 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-363">Open **Customer.cs** class in the **Model** folder and *decorate* each property using data annotation attributes.</span></span>

    <span data-ttu-id="12d02-364">(코드 조각- *Forms 랩-Ex02-데이터 주석 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-364">(Code Snippet - *Web Forms Lab - Ex02 - Data Annotations*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > <span data-ttu-id="12d02-365">.NET framework 4.5에는 기존 데이터 주석 컬렉션을 확장 했습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-365">.NET Framework 4.5 has extended the existing data annotation collection.</span></span> <span data-ttu-id="12d02-366">다음은 일부 데이터 주석을 사용할 수 있습니다: [CreditCard] [Phone] [EmailAddress], [범위] [비교]를 [Url] [FileExtensions] [Required], [키], [RegularExpression].</span><span class="sxs-lookup"><span data-stu-id="12d02-366">These are some of the data annotations you can use: [CreditCard], [Phone], [EmailAddress], [Range], [Compare], [Url], [FileExtensions], [Required], [Key], [RegularExpression].</span></span>
    > 
    > <span data-ttu-id="12d02-367">몇 가지 사용 예:</span><span class="sxs-lookup"><span data-stu-id="12d02-367">Some usage examples:</span></span>
    > 
    > [키]: Specifies that an attribute is the unique identifier
[Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > <span data-ttu-id="12d02-369">또한 각 특성 내에서 고유한 오류 메시지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-369">You can also define your own error messages within each attribute.</span></span>
3. <span data-ttu-id="12d02-370">오픈 **CustomerDetails.aspx** 및 FormView 컨트롤에 EditItemTemplate 및 먼저 섹션의 첫 번째 및 마지막 이름 필드에 대 한 모든 RequiredFieldvalidators를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-370">Open **CustomerDetails.aspx** and remove all the RequiredFieldvalidators for the first and last name fields in the in EditItemTemplate and InsertItemTemplate sections of the FormView control.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > <span data-ttu-id="12d02-371">데이터 주석 사용의 장점 중 하나는 응용 프로그램 페이지에 유효성 검사 논리 중복 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-371">One advantage of using data annotations is that validation logic is not duplicated in your application pages.</span></span> <span data-ttu-id="12d02-372">모델에서 한 번 정의 하 고 데이터를 조작 하는 모든 응용 프로그램 페이지에 걸쳐 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-372">You define it once in the model, and use it across all the application pages that manipulate data.</span></span>
4. <span data-ttu-id="12d02-373">오픈 **CustomerDetails.aspx** 코드 숨김 및 SaveCustomer 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-373">Open **CustomerDetails.aspx** code-behind and locate the SaveCustomer method.</span></span> <span data-ttu-id="12d02-374">이 메서드는 새 고객 삽입 될 때 호출 됩니다 및 FormView 컨트롤 값에서 고객 매개 변수를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-374">This method is called when inserting a new customer and receives the Customer parameter from the FormView control values.</span></span> <span data-ttu-id="12d02-375">ASP.NET에서 실행 됩니다 매핑을 페이지 컨트롤 사이의 매개 변수 개체 않을 때 발생 하는 경우 모든 데이터 주석에 대 한 모델 유효성 검사 특성 및 있으면 발생 하는 오류와 함께 ModelState 사전을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-375">When the mapping between the page controls and the parameter object occurrs, ASP.NET will execute the model validation against all the data annotation attributes and fill the ModelState dictionary with the errors encountered, if any.</span></span>

    <span data-ttu-id="12d02-376">ModelState.IsValid 유효성 검사를 수행한 후 모델의 모든 필드가 유효 하면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-376">The ModelState.IsValid will only return true if all the fields on your model are valid after performing the validation.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. <span data-ttu-id="12d02-377">추가 된 **ValidationSummary** 끝 모델 오류 목록에 표시할 CustomerDetails 페이지의 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-377">Add a **ValidationSummary** control at the end of the CustomerDetails page to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    <span data-ttu-id="12d02-378">합니다 **ShowModelStateErrors** 로 설정 된 경우는 ValidationSummary에 새 속성을 컨트롤은 **true**, 컨트롤 ModelState 사전에서 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-378">The **ShowModelStateErrors** is a new property on the ValidationSummary control that when set to **true**, the control will show the errors from the ModelState dictionary.</span></span> <span data-ttu-id="12d02-379">이러한 오류는 데이터 주석 유효성 검사에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-379">These errors come from the data annotations validation.</span></span>
6. <span data-ttu-id="12d02-380">키를 눌러 **F5** 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-380">Press **F5** to run the Web application.</span></span> <span data-ttu-id="12d02-381">일부 잘못 된 값으로 양식을 완료 하 고 클릭 **저장할** 유효성 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-381">Complete the form with some erroneous values and click **Save** to execute validation.</span></span> <span data-ttu-id="12d02-382">맨 아래에 요약 오류를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-382">Notice the error summary at the bottom.</span></span>

    <span data-ttu-id="12d02-383">![데이터 주석 사용한 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "데이터 주석 사용한 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="12d02-383">![Validation with Data Annotations](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "Validation with Data Annotations")</span></span>

    <span data-ttu-id="12d02-384">*데이터 주석 사용한 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="12d02-384">*Validation with Data Annotations*</span></span>

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a><span data-ttu-id="12d02-385">작업 3-ModelState 사용 하 여 사용자 지정 데이터베이스 오류 처리</span><span class="sxs-lookup"><span data-stu-id="12d02-385">Task 3 - Handling Custom Database Errors with ModelState</span></span>

<span data-ttu-id="12d02-386">Web Forms의 이전 버전에서는 너무 긴 문자열 또는 고유 키 위반이 같은 데이터베이스 오류 처리 포함 될 수 있습니다 리포지토리 코드에서 예외를 throw 하 고 다음 오류를 표시 하려면 코드 숨김에 예외를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-386">In previous version of Web Forms, handling database errors such as a too long string or a unique key violation could involve throwing exceptions in your repository code and then handling the exceptions on your code-behind to display an error.</span></span> <span data-ttu-id="12d02-387">코드의 상당한 비교적 간단한 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-387">A great amount of code is required to do something relatively simple.</span></span>

<span data-ttu-id="12d02-388">Web Forms 4.5에서 ModelState 개체 모델 또는 데이터베이스에서 페이지에서 일관 된 방식으로 오류를 표시 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-388">In Web Forms 4.5, the ModelState object can be used to display the errors on the page, either from your model or from the database, in a consistent manner.</span></span>

<span data-ttu-id="12d02-389">이 태스크에서는 올바르게 데이터베이스 예외를 처리 하 고 ModelState 개체를 사용 하 여 사용자에 게 적절 한 메시지를 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-389">In this task, you will add code to properly handle database exceptions and show the appropriate message to the user using the ModelState object.</span></span>

1. <span data-ttu-id="12d02-390">응용 프로그램이 여전히 실행 되는 동안 중복 된 값을 사용 하는 범주의 이름을 업데이트 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-390">While the application is still running, try to update the name of a category using a duplicated value.</span></span>

    <span data-ttu-id="12d02-391">![중복 된 이름을 사용 하 여 범주를 업데이트](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "중복 된 이름을 사용 하 여 범주를 업데이트 하는 중")</span><span class="sxs-lookup"><span data-stu-id="12d02-391">![Updating a category with a duplicated name](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "Updating a category with a duplicated name")</span></span>

    <span data-ttu-id="12d02-392">*중복 된 이름을 사용 하 여 범주를 업데이트 하는 중*</span><span class="sxs-lookup"><span data-stu-id="12d02-392">*Updating a category with a duplicated name*</span></span>

    <span data-ttu-id="12d02-393">로 인해 예외가 발생 하는 &quot;고유&quot; 의 제약 조건을 합니다 **CategoryName** 열.</span><span class="sxs-lookup"><span data-stu-id="12d02-393">Notice that an exception is thrown due to the &quot;unique&quot; constraint of the **CategoryName** column.</span></span>

    <span data-ttu-id="12d02-394">![중복 된 범주 이름에 대 한 예외](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "중복 된 범주 이름에 대 한 예외")</span><span class="sxs-lookup"><span data-stu-id="12d02-394">![Exception for duplicated category names](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "Exception for duplicated category names")</span></span>

    <span data-ttu-id="12d02-395">*중복 된 범주 이름에 대 한 예외*</span><span class="sxs-lookup"><span data-stu-id="12d02-395">*Exception for duplicated category names*</span></span>
2. <span data-ttu-id="12d02-396">디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-396">Stop debugging.</span></span> <span data-ttu-id="12d02-397">에 **Products.aspx.cs** 코드 숨김 파일을 업데이트 합니다 **UpdateCategory** db에서 throw 한 예외를 처리 하는 방법. Savechanges () 메서드를 호출 하 고 오류를 추가 합니다 **ModelState** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-397">In the **Products.aspx.cs** code-behind file, update the **UpdateCategory** method to handle the exceptions thrown by the db.SaveChanges() method call and add an error to the **ModelState** object.</span></span>

    <span data-ttu-id="12d02-398">새 **tryupdatemodel에 전달** 메서드는 사용자가 제공 되는 폼 데이터를 사용 하 여 데이터베이스에서 검색 된 범주 개체를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-398">The new **TryUpdateModel** method updates the category object retrieved from the database using the form data provided by the user.</span></span>

    <span data-ttu-id="12d02-399">(코드 조각- *Forms 랩-Ex02-오류 UpdateCategory 처리 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-399">(Code Snippet - *Web Forms Lab - Ex02 - UpdateCategory Handle Errors*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > <span data-ttu-id="12d02-400">이상적으로 하면 DbUpdateException의 원인을 파악 하 고 근본 원인을 unique key 제약 조건 위반 인지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-400">Ideally, you would have to identify the cause of the DbUpdateException and check if the root cause is the violation of a unique key constraint.</span></span>
3. <span data-ttu-id="12d02-401">오픈 **Products.aspx** 추가한를 **ValidationSummary** 모델 오류 목록을 표시 하는 GridView 범주 아래에 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-401">Open **Products.aspx** and add a **ValidationSummary** control below the categories GridView to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. <span data-ttu-id="12d02-402">사이트를 실행 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-402">Run the site and go to the Products page.</span></span> <span data-ttu-id="12d02-403">중복 된 값을 사용 하 여 범주 이름을 업데이트 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-403">Try to update the name of a category using an duplicated value.</span></span>

    <span data-ttu-id="12d02-404">예외 처리 및 오류 메시지에 표시 합니다 **ValidationSummary** 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-404">Notice that the exception was handled and the error message appears in the **ValidationSummary** control.</span></span>

    <span data-ttu-id="12d02-405">![범주 오류 중복](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "범주 오류 중복")</span><span class="sxs-lookup"><span data-stu-id="12d02-405">![Duplicated category error](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "Duplicated category error")</span></span>

    <span data-ttu-id="12d02-406">*중복 된 범주 오류*</span><span class="sxs-lookup"><span data-stu-id="12d02-406">*Duplicated category error*</span></span>

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a><span data-ttu-id="12d02-407">ASP.NET Web Forms 4.5에서에서 유효성 검사 요청 작업 4-</span><span class="sxs-lookup"><span data-stu-id="12d02-407">Task 4 - Request Validation in ASP.NET Web Forms 4.5</span></span>

<span data-ttu-id="12d02-408">Asp.net에서 요청 유효성 검사 기능에는 특정 수준의 교차 사이트 스크립팅 (XSS) 공격에 대 한 기본 보호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-408">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="12d02-409">이전 버전의 ASP.NET 요청 유효성 검사 기본적으로 사용 하도록 설정한에 전체 페이지에 대해서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-409">In previous versions of ASP.NET, request validation was enabled by default and could only be disabled for an entire page.</span></span> <span data-ttu-id="12d02-410">새 버전의 ASP.NET Web Forms를 사용 하 여 이제, 단일 컨트롤에 대 한 요청 유효성 검사를 사용 하지 않도록 설정, 지연 요청 유효성 검사를 수행 하거나 액세스할 수 되지 않은 유효성이 검사 된 요청 데이터 (이렇게 할 경우 신중 하 게!).</span><span class="sxs-lookup"><span data-stu-id="12d02-410">With the new version of ASP.NET Web Forms you can now disable the request validation for a single control, perform lazy request validation or access un-validated request data (be careful if you do so!).</span></span>

1. <span data-ttu-id="12d02-411">키를 눌러 **ctrl+f5** 디버깅 하지 않고 사이트를 시작 하 여 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-411">Press **Ctrl+F5** to start the site without debugging and go to the Products page.</span></span> <span data-ttu-id="12d02-412">범주를 선택 하 고 클릭 합니다 **편집** 제품에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-412">Select a category and then click the **Edit** link on any of the products.</span></span>
2. <span data-ttu-id="12d02-413">예를 들어 HTML 태그를 포함 하 여 잠재적으로 위험한 콘텐츠가 포함 된 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-413">Type a description containing potentially dangerous content, for instance including HTML tags.</span></span> <span data-ttu-id="12d02-414">요청 유효성 검사로 인해 발생 한 예외에 대 한 공지를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-414">Take notice of the exception thrown due to the request validation.</span></span>

    <span data-ttu-id="12d02-415">![잠재적으로 위험한 콘텐츠가 포함 된 제품을 편집](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "잠재적으로 위험한 콘텐츠가 포함 된 제품 편집")</span><span class="sxs-lookup"><span data-stu-id="12d02-415">![Editing a product with potentially dangerous content](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "Editing a product with potentially dangerous content")</span></span>

    <span data-ttu-id="12d02-416">*잠재적으로 위험한 콘텐츠가 포함 된 제품 편집*</span><span class="sxs-lookup"><span data-stu-id="12d02-416">*Editing a product with potentially dangerous content*</span></span>

    <span data-ttu-id="12d02-417">![요청 유효성 검사로 인해 예외가](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "요청 유효성 검사로 인해 throw 된 예외")</span><span class="sxs-lookup"><span data-stu-id="12d02-417">![Exception thrown due to request validation](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "Exception thrown due to request validation")</span></span>

    <span data-ttu-id="12d02-418">*요청 유효성 검사로 인해 throw 된 예외*</span><span class="sxs-lookup"><span data-stu-id="12d02-418">*Exception thrown due to request validation*</span></span>
3. <span data-ttu-id="12d02-419">페이지를 닫고 Visual Studio에서 눌러 **shift+f5** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-419">Close the page and, in Visual Studio, press **SHIFT+F5** to stop debugging.</span></span>
4. <span data-ttu-id="12d02-420">엽니다는 **ProductDetails.aspx** 찾아서 페이지는 **설명** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-420">Open the **ProductDetails.aspx** page and locate the **Description** TextBox.</span></span>
5. <span data-ttu-id="12d02-421">새 추가 **ValidateRequestMode** 텍스트 상자에 속성으로 값을 설정 하 고 **사용 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-421">Add the new **ValidateRequestMode** property to the TextBox and set its value to **Disabled**.</span></span>

    <span data-ttu-id="12d02-422">새 **ValidateRequestMode** 특성을 사용 하면 각 컨트롤에 세부적으로 요청 유효성 검사를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-422">The new **ValidateRequestMode** attribute allows you to disable the request validation granularly on each control.</span></span> <span data-ttu-id="12d02-423">HTML 코드를 받을 수 있지만 페이지의 나머지 부분에 대 한 작업 유효성 검사를 유지 하려고 하는 입력에 사용 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-423">This is useful when you want to use an input that may receive HTML code, but want to keep the validation working for the rest of the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. <span data-ttu-id="12d02-424">키를 눌러 **F5** 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-424">Press **F5** to run the web application.</span></span> <span data-ttu-id="12d02-425">편집 제품 페이지를 다시 열고 HTML 태그를 포함 하 여 제품 설명을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-425">Open the edit product page again and complete a product description including HTML tags.</span></span> <span data-ttu-id="12d02-426">설명에 HTML 콘텐츠를 추가할 이제 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-426">Notice that you can now add HTML content to the description.</span></span>

    <span data-ttu-id="12d02-427">![제품 설명에 대 한 사용 하지 않도록 설정 하는 유효성 검사 요청](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "요청 제품 설명에 대 한 사용 하지 않도록 설정 하는 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="12d02-427">![Request validation disabled for the product description](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "Request validation disabled for the product description")</span></span>

    <span data-ttu-id="12d02-428">*제품 설명에 대 한 사용 하지 않도록 설정 하는 요청 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="12d02-428">*Request validation disabled for the product description*</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-429">프로덕션 응용 프로그램에서 HTML 태그를 안전 하 게 입력 되지 않도록 하는 사용자가 입력 한 HTML 코드를 삭제 해야 합니다 (예를 들어, 없습니다 &lt;스크립트&gt; 태그).</span><span class="sxs-lookup"><span data-stu-id="12d02-429">In a production application, you should sanitize the HTML code entered by the user to make sure only safe HTML tags are entered (for example, there are no &lt;script&gt; tags).</span></span> <span data-ttu-id="12d02-430">이 위해 사용할 수 있습니다 [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS)합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-430">To do this, you can use [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS).</span></span>
7. <span data-ttu-id="12d02-431">제품을 다시 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-431">Edit the product again.</span></span> <span data-ttu-id="12d02-432">이름 필드에 HTML 코드를 입력 하 고 클릭 **저장할**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-432">Type HTML code in the Name field and click **Save**.</span></span> <span data-ttu-id="12d02-433">설명 필드에 대 한 요청 유효성 검사를 비활성화만 되 고 잠재적으로 위험한 콘텐츠에 대해 여전히 유효성 검사 다시 필드의 나머지 부분을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-433">Notice that Request Validation is only disabled for the Description field and the rest of the fields re still validated against the potentially dangerous content.</span></span>

    <span data-ttu-id="12d02-434">![필드의 나머지 부분에서 사용 하도록 설정 하는 유효성 검사 요청](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "요청 필드의 나머지 부분에서 사용 하도록 설정 하는 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="12d02-434">![Request validation enabled in the rest of the fields](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "Request validation enabled in the rest of the fields")</span></span>

    <span data-ttu-id="12d02-435">*필드의 나머지 부분에서 사용 하도록 설정 하는 요청 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="12d02-435">*Request validation enabled in the rest of the fields*</span></span>

    <span data-ttu-id="12d02-436">ASP.NET Web Forms 4.5 지연 요청 유효성 검사를 수행 하는 새 요청 유효성 검사 모드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-436">ASP.NET Web Forms 4.5 includes a new request validation mode to perform request validation lazily.</span></span> <span data-ttu-id="12d02-437">로 설정 하는 요청 유효성 검사 모드를 사용 하 여 **4.5**이면 코드 액세스 부분 *Request.Form [&quot;키&quot;]*, ASP.NET 4.5의 요청 유효성 검사는 유일한 트리거 요청 유효성 검사 에 대 한 폼 컬렉션의 특정 요소에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-437">With the request validation mode set to **4.5**, if a piece of code accesses *Request.Form[&quot;key&quot;]*, ASP.NET 4.5's request validation will only trigger request validation for that specific element in the form collection.</span></span>

    <span data-ttu-id="12d02-438">또한 ASP.NET 4.5에는 Microsoft에서 ANTI-XSS 라이브러리 v4.0에서 주요 인코딩 루틴은 이제 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-438">Additionally, ASP.NET 4.5 now includes core encoding routines from the Microsoft Anti-XSS Library v4.0.</span></span> <span data-ttu-id="12d02-439">ANTI-XSS 인코딩 루틴은 새 구현 됩니다 *AntiXssEncoder* 새 형식을 찾을 **System.Web.Security.AntiXss** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-439">The Anti-XSS encoding routines are implemented by the new *AntiXssEncoder* type found in the new **System.Web.Security.AntiXss** namespace.</span></span> <span data-ttu-id="12d02-440">사용 하 여는 **encoderType** 를 사용 하도록 구성 하는 매개 변수 *AntiXssEncoder*, 새 인코딩 루틴을 사용 하 여 ASP.NET 내에 인코딩을 자동으로 모든 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-440">With the **encoderType** parameter configured to use *AntiXssEncoder*, all output encoding within ASP.NET automatically uses the new encoding routines.</span></span>
8. <span data-ttu-id="12d02-441">ASP.NET 4.5 요청 유효성 검사는 또한 요청 데이터에 대 한 유효성을 검사 되지 않은 액세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-441">ASP.NET 4.5 request validation also supports un-validated access to request data.</span></span> <span data-ttu-id="12d02-442">ASP.NET 4.5에는 새 컬렉션 속성을 추가 합니다 **HttpRequest** 라는 개체 **Unvalidated**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-442">ASP.NET 4.5 adds a new collection property to the **HttpRequest** object called **Unvalidated**.</span></span> <span data-ttu-id="12d02-443">로 이동 하는 경우 **HttpRequest.Unvalidated** Forms "," 문자열이 "," 쿠키 "," Url "및" 등을 포함 하 여 요청 데이터의 일반적인 부분 모두에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-443">When you navigate into **HttpRequest.Unvalidated** you have access to all of the common pieces of request data, including Forms, QueryStrings, Cookies, URLs, and so on.</span></span>

    <span data-ttu-id="12d02-444">![Request.Unvalidated 개체](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated 개체")</span><span class="sxs-lookup"><span data-stu-id="12d02-444">![Request.Unvalidated object](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated object")</span></span>

    <span data-ttu-id="12d02-445">*Request.Unvalidated 개체*</span><span class="sxs-lookup"><span data-stu-id="12d02-445">*Request.Unvalidated object*</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-446">**주의 해 서 HttpRequest.Unvalidated 속성을 사용 하세요!**</span><span class="sxs-lookup"><span data-stu-id="12d02-446">**Please use the HttpRequest.Unvalidated property with caution!**</span></span> <span data-ttu-id="12d02-447">신중 하 게에 원시 요청 데이터를 위험한 텍스트 라운드트립 및 모르는 고객에 게 렌더링 되지 않는 사용자 지정 유효성 검사를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-447">Make sure you carefully perform custom validation on the raw request data to ensure that dangerous text is not round-tripped and rendered back to unsuspecting customers!</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a><span data-ttu-id="12d02-448">연습 3: 비동기 페이지 처리에 ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="12d02-448">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>

<span data-ttu-id="12d02-449">이 연습에서는 ASP.NET Web Forms의 기능을 처리 하는 새 비동기 페이지에 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-449">In this exercise, you will be introduced to the new asynchronous page processing features in ASP.NET Web Forms.</span></span>

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a><span data-ttu-id="12d02-450">작업 1-제품 업데이트 페이지 업로드 하 고 이미지를 표시 하려면 세부 정보</span><span class="sxs-lookup"><span data-stu-id="12d02-450">Task 1 - Updating the Product Details Page to Upload and Show Images</span></span>

<span data-ttu-id="12d02-451">이 태스크에서는 사용자가 제품에 대 한 이미지 URL을 지정 하 여 읽기 전용 뷰에 표시를 허용 하도록 제품 정보 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-451">In this task, you will update the product details page to allow the user to specify an image URL for the product and display it in the read-only view.</span></span> <span data-ttu-id="12d02-452">동기적으로 다운로드 하 여 지정된 된 이미지의 로컬 복사본을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-452">You will create a local copy of the specified image by downloading it synchronously.</span></span> <span data-ttu-id="12d02-453">다음 태스크에서는이 구현을 비동기적으로 작동 하도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-453">In the next task, you will update this implementation to make it work asynchronously.</span></span>

1. <span data-ttu-id="12d02-454">열기 **Visual Studio 2012** 로드 합니다 **시작** 솔루션 **Source\Ex3 Async\Begin** 이 랩의이 폴더에서.</span><span class="sxs-lookup"><span data-stu-id="12d02-454">Open **Visual Studio 2012** and load the **Begin** solution located in **Source\Ex3-Async\Begin** from this lab's folder.</span></span> <span data-ttu-id="12d02-455">또는 이전 연습에서 기존 솔루션에 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-455">Alternatively, you can continue working on your existing solution from the previous exercises.</span></span>

   1. <span data-ttu-id="12d02-456">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-456">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="12d02-457">이렇게 하려면 솔루션 탐색기에서를 클릭 합니다 **WebFormsLab** 프로젝트를 마우스 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-457">To do this, in the Solution Explorer, click the **WebFormsLab** project and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="12d02-458">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="12d02-458">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="12d02-459">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-459">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="12d02-460">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-460">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="12d02-461">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-461">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="12d02-462">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-462">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="12d02-463">엽니다는 **ProductDetails.aspx** 원본 페이지 및 FormView의 ItemTemplate 제품 이미지를 표시 하려면 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-463">Open the **ProductDetails.aspx** page source and add a field in the FormView's ItemTemplate to show the product image.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. <span data-ttu-id="12d02-464">FormView의 EditTemplate에 이미지 URL을 지정 하는 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-464">Add a field to specify the image URL in the FormView's EditTemplate.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. <span data-ttu-id="12d02-465">엽니다는 **ProductDetails.aspx.cs** 코드 숨김 파일을 다음 네임 스페이스 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-465">Open the **ProductDetails.aspx.cs** code-behind file and add the following namespace directives.</span></span>

    <span data-ttu-id="12d02-466">(코드 조각- *Forms 랩-Ex03-네임 스페이스 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-466">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. <span data-ttu-id="12d02-467">만들기는 **UpdateProductImage** 로컬에서 원격 이미지를 저장 하는 방법 **이미지** 폴더 및 새 이미지 위치 값을 지닌 제품 엔터티를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-467">Create an **UpdateProductImage** method to store remote images in the local **Images** folder and update the product entity with the new image location value.</span></span>

    <span data-ttu-id="12d02-468">(코드 조각- *Forms-Ex03-랩 UpdateProductImage 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-468">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. <span data-ttu-id="12d02-469">업데이트를 **UpdateProduct** 메서드를 호출 합니다 **UpdateProductImage** 메서드.</span><span class="sxs-lookup"><span data-stu-id="12d02-469">Update the **UpdateProduct** method to call the **UpdateProductImage** method.</span></span>

    <span data-ttu-id="12d02-470">(코드 조각- *웹 폼 랩-Ex03-UpdateProductImage 호출*)</span><span class="sxs-lookup"><span data-stu-id="12d02-470">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Call*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. <span data-ttu-id="12d02-471">응용 프로그램을 실행 하는 제품에 대 한 이미지를 업로드 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-471">Run the application and try to upload an image for a product.</span></span> <span data-ttu-id="12d02-472">예를 들어 Office 클립 예술에서 다음 이미지 URL을 사용할 수 있습니다. [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span><span class="sxs-lookup"><span data-stu-id="12d02-472">For example, you can use the following image URL from Office Clip Arts: [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span></span>

    <span data-ttu-id="12d02-473">![제품에 대 한 이미지를 설정](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "제품에 대 한 이미지 설정")</span><span class="sxs-lookup"><span data-stu-id="12d02-473">![Setting an image for a product](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "Setting an image for a product")</span></span>

    <span data-ttu-id="12d02-474">*제품에 대 한 이미지 설정*</span><span class="sxs-lookup"><span data-stu-id="12d02-474">*Setting an image for a product*</span></span>

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a><span data-ttu-id="12d02-475">2-제품 세부 정보 페이지가 처리 비동기 추가 작업</span><span class="sxs-lookup"><span data-stu-id="12d02-475">Task 2 - Adding Asynchronous Processing to the Product Details Page</span></span>

<span data-ttu-id="12d02-476">이 태스크에서는 제품 정보 페이지를 비동기적으로 작동 하도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-476">In this task, you will update the product details page to make it work asynchronously.</span></span> <span data-ttu-id="12d02-477">ASP.NET 4.5의 비동기 페이지 처리를 사용 하 여-이미지 다운로드 프로세스-장기 실행 작업을 향상 시킬가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-477">You will enhance a long running task - the image download process - by using ASP.NET 4.5 asynchronous page processing.</span></span>

<span data-ttu-id="12d02-478">웹 응용 프로그램에서 비동기 메서드는 ASP.NET 스레드 풀이 사용 되는 방식을 최적화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-478">Asynchronous methods in web applications can be used to optimize the way ASP.NET thread pools are used.</span></span> <span data-ttu-id="12d02-479">ASP.NET 있습니다는 참가 대 한 스레드 풀의 스레드 수가 제한 요청, 따라서 모든 스레드를 사용 중인 경우 ASP.NET 새 요청을 거부 하기 시작, 응용 프로그램 오류 메시지를 보낼에 사이트를 사용할 수 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-479">In ASP.NET there are a limited number of threads in the thread pool for attending requests, thus, when all the threads are busy, ASP.NET starts to reject new requests, sends application error messages and makes your site unavailable.</span></span>

<span data-ttu-id="12d02-480">웹 사이트에 시간이 많이 걸리는 작업 오랜 시간 동안 할당 된 스레드를 차지 하기 때문에 비동기 프로그래밍을 위한 훌륭한 후보가.입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-480">Time-consuming operations on your web site are great candidates for asynchronous programming because they occupy the assigned thread for a long time.</span></span> <span data-ttu-id="12d02-481">장기 실행 요청, 많은 다양 한 요소를 사용 하 여 페이지 및 오프 라인 작업, 이러한 데이터베이스를 쿼리 또는 외부 웹 서버에 액세스 해야 하는 페이지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-481">This includes long running requests, pages with lots of different elements and pages that require offline operations, such querying a database or accessing an external web server.</span></span> <span data-ttu-id="12d02-482">비동기 메서드를 사용 하면 이러한 작업에 대 한 페이지를 처리 하는 동안 스레드가 해제 되며 스레드로 반환 장점은 풀 및 새 페이지 요청에 참가 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-482">The advantage is that if you use asynchronous methods for these operations, while the page is processing, the thread is freed and returned to the thread pool and can be used to attend to a new page request.</span></span> <span data-ttu-id="12d02-483">이 즉, 페이지에서 스레드 풀 스레드에 처리 시작 되 고 비동기 처리가 완료 된 후에 다른 곳에 처리를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-483">This means, the page will start processing in one thread from the thread pool and might complete processing in a different one, after the async processing completes.</span></span>

1. <span data-ttu-id="12d02-484">엽니다는 **ProductDetails.aspx** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-484">Open the **ProductDetails.aspx** page.</span></span> <span data-ttu-id="12d02-485">추가 합니다 **비동기** 특성을 **페이지** 요소로 설정 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-485">Add the **Async** attribute in the **Page** element and set it to **true**.</span></span> <span data-ttu-id="12d02-486">이 특성은 IHttpAsyncHandler 인터페이스를 구현 하는 ASP.NET에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-486">This attribute tells ASP.NET to implement the IHttpAsyncHandler interface.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. <span data-ttu-id="12d02-487">페이지를 실행 하는 스레드에 세부 정보를 표시할 페이지의 맨 아래에 레이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-487">Add a Label at the bottom of the page to show the details of the threads running the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. <span data-ttu-id="12d02-488">열어야 **ProductDetails.aspx.cs** 다음 네임 스페이스 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-488">Open up **ProductDetails.aspx.cs** and add the following namespace directives.</span></span>

    <span data-ttu-id="12d02-489">(코드 조각- *Forms 랩-Ex03-네임 스페이스 2 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-489">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. <span data-ttu-id="12d02-490">수정 된 **UpdateProductImage** 메서드를 비동기 작업을 사용 하 여 이미지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-490">Modify the **UpdateProductImage** method to download the image with an asynchronous task.</span></span> <span data-ttu-id="12d02-491">바꿉니다 합니다 **WebClient** **DownloadFile** 메서드를 **DownloadFileTaskAsync** 메서드 포함 및를 **await** 키워드.</span><span class="sxs-lookup"><span data-stu-id="12d02-491">You will replace the **WebClient** **DownloadFile** method with the **DownloadFileTaskAsync** method and include the **await** keyword.</span></span>

    <span data-ttu-id="12d02-492">(코드 조각- *Forms-Ex03-랩 UpdateProductImage 비동기 웹*)</span><span class="sxs-lookup"><span data-stu-id="12d02-492">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Async*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    <span data-ttu-id="12d02-493">RegisterAsyncTask는 다른 스레드에서 실행할 새 페이지 비동기 작업을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-493">The RegisterAsyncTask registers a new page asynchronous task to be executed in a different thread.</span></span> <span data-ttu-id="12d02-494">실행할 작업 (t)를 사용 하 여 람다 식을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-494">It receives a lambda expression with the Task (t) to be executed.</span></span> <span data-ttu-id="12d02-495">합니다 **await** 키워드는 **DownloadFileTaskAsync** 메서드 변환 후 비동기적으로 호출 되는 콜백 메서드의 나머지는 **DownloadFileTaskAsync** 메서드를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-495">The **await** keyword in the **DownloadFileTaskAsync** method converts the remainder of the method into a callback that is invoked asynchronously after the **DownloadFileTaskAsync** method has completed.</span></span> <span data-ttu-id="12d02-496">ASP.NET 자동으로 모든 HTTP 요청 원래 값을 유지 하 여 메서드의 실행을 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-496">ASP.NET will resume the execution of the method by automatically maintaining all the HTTP request original values.</span></span> <span data-ttu-id="12d02-497">.NET 4.5의 새로운 비동기 프로그래밍 모델을 사용 하면 콜백 함수나 연속 코드의 복잡성을 처리 하 고 컴파일러 및 동기 코드와 매우 비슷하며 비동기 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-497">The new asynchronous programming model in .NET 4.5 enables you to write asynchronous code that looks very much like synchronous code, and let the compiler handle the complications of callback functions or continuation code.</span></span>
    > [!NOTE]
    > <span data-ttu-id="12d02-498">RegisterAsyncTask 및 PageAsyncTask 된 이미.NET 2.0부터입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-498">RegisterAsyncTask and PageAsyncTask were already available since .NET 2.0.</span></span> <span data-ttu-id="12d02-499">Await 키워드는.NET 4.5의 비동기 프로그래밍 모델에서 새로운 기능과.NET WebClient 개체에서 새 TaskAsync 메서드와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-499">The await keyword is new from the .NET 4.5 asynchronous programming model and can be used together with the new TaskAsync methods from the .NET WebClient object.</span></span>
5. <span data-ttu-id="12d02-500">코드를 시작 및 실행이 완료 스레드를 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-500">Add code to display the threads on which the code started and finished executing.</span></span> <span data-ttu-id="12d02-501">이 작업을 수행 하려면 업데이트 된 **UpdateProductImage** 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-501">To do this, update the **UpdateProductImage** method with the following code.</span></span>

    <span data-ttu-id="12d02-502">(코드 조각- *Web Forms 랩-Ex03-Show 스레드*)</span><span class="sxs-lookup"><span data-stu-id="12d02-502">(Code Snippet - *Web Forms Lab - Ex03 - Show threads*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. <span data-ttu-id="12d02-503">웹 사이트를 엽니다 **Web.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-503">Open the web site's **Web.config** file.</span></span> <span data-ttu-id="12d02-504">다음 appSetting 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-504">Add the following appSetting variable.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. <span data-ttu-id="12d02-505">키를 눌러 **F5** 응용 프로그램을 실행 하는 제품에 대 한 이미지를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-505">Press **F5** to run the application and upload an image for the product.</span></span> <span data-ttu-id="12d02-506">시작 및 완료 된 코드를 다른 수 있는 스레드 ID를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-506">Notice the threads ID where the code started and finished may be different.</span></span> <span data-ttu-id="12d02-507">ASP.NET 스레드 풀에서 별도 스레드에서 실행 하는 비동기 작업 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-507">This is because asynchronous tasks run on a separate thread from ASP.NET thread pool.</span></span> <span data-ttu-id="12d02-508">작업이 완료 되 면 ASP.NET 태스크를 큐에 다시 배치 하 고 사용 가능한 스레드 중 하나를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-508">When the task completes, ASP.NET puts the task back in the queue and assigns any of the available threads.</span></span>

    <span data-ttu-id="12d02-509">![이미지를 비동기로 다운로드할](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "이미지를 비동기적으로 다운로드")</span><span class="sxs-lookup"><span data-stu-id="12d02-509">![Downloading an image asynchronously](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "Downloading an image asynchronously")</span></span>

    <span data-ttu-id="12d02-510">*이미지를 비동기적으로 다운로드*</span><span class="sxs-lookup"><span data-stu-id="12d02-510">*Downloading an image asynchronously*</span></span>

> [!NOTE]
> <span data-ttu-id="12d02-511">또한 Azure는 다음이 응용이 프로그램을 배포할 수 있습니다 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-511">Additionally, you can deploy this application to Azure following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="12d02-512">요약</span><span class="sxs-lookup"><span data-stu-id="12d02-512">Summary</span></span>

<span data-ttu-id="12d02-513">이 실습 랩에서 다음 개념 해결 되었으며 설명:</span><span class="sxs-lookup"><span data-stu-id="12d02-513">In this hands-on lab, the following concepts have been addressed and demonstrated:</span></span>

- <span data-ttu-id="12d02-514">강력한 데이터 바인딩 식을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="12d02-514">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="12d02-515">Web Forms에서 새 모델 바인딩 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-515">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="12d02-516">값 공급자를 사용 하 여 코드 숨김 방법 페이지 데이터를 매핑하기 위한</span><span class="sxs-lookup"><span data-stu-id="12d02-516">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="12d02-517">사용자 입력된 유효성 검사에 대 한 데이터 주석 사용</span><span class="sxs-lookup"><span data-stu-id="12d02-517">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="12d02-518">Web Forms에서 advange jQuery 사용한 unobstrusive 클라이언트 쪽 유효성 검사의 수행</span><span class="sxs-lookup"><span data-stu-id="12d02-518">Take advange of unobstrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="12d02-519">세분화 된 요청 유효성 검사 구현</span><span class="sxs-lookup"><span data-stu-id="12d02-519">Implement granular request validation</span></span>
- <span data-ttu-id="12d02-520">Web Forms에서 처리 하는 비동기 페이지를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-520">Implement asynchronous page processing in Web Forms</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="12d02-521">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="12d02-521">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="12d02-522">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="12d02-522">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="12d02-523">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-523">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="12d02-524">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-524">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="12d02-525">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Azure SDK를 사용 하 여</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-525">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="12d02-526">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-526">Click on **Install Now**.</span></span> <span data-ttu-id="12d02-527">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-527">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="12d02-528">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-528">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="12d02-529">![Visual Studio Express를 설치](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="12d02-529">![Install Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="12d02-530">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="12d02-530">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="12d02-531">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-531">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    <span data-ttu-id="12d02-533">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="12d02-533">*Accepting the license terms*</span></span>
5. <span data-ttu-id="12d02-534">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-534">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    <span data-ttu-id="12d02-536">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="12d02-536">*Installation progress*</span></span>
6. <span data-ttu-id="12d02-537">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-537">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    <span data-ttu-id="12d02-539">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="12d02-539">*Installation completed*</span></span>
7. <span data-ttu-id="12d02-540">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-540">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="12d02-541">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-541">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    <span data-ttu-id="12d02-543">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="12d02-543">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="12d02-544">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="12d02-544">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="12d02-545">이 부록은 Azure Portal에서 새 웹 사이트를 만들고 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-545">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="12d02-546">작업 1-Azure Portal에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="12d02-546">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="12d02-547">로 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-547">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-548">Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-548">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="12d02-549">등록할 수 있습니다 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-549">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="12d02-550">![Windows Azure 포털에 로그온](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Windows Azure 포털에 로그온")</span><span class="sxs-lookup"><span data-stu-id="12d02-550">![Log on to Windows Azure portal](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="12d02-551">*포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="12d02-551">*Log on to the Portal*</span></span>
2. <span data-ttu-id="12d02-552">클릭 **새로 만들기** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="12d02-552">Click **New** on the command bar.</span></span>

    <span data-ttu-id="12d02-553">![새 웹 사이트를 만드는](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="12d02-553">![Creating a new Web Site](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="12d02-554">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="12d02-554">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="12d02-555">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-555">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="12d02-556">선택한 **빨리 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-556">Then select **Quick Create** option.</span></span> <span data-ttu-id="12d02-557">새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-557">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-558">Azure는 웹 응용 프로그램을 제어 하 고 관리할 수 있는 클라우드에서 실행 중인 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-558">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="12d02-559">빠른 생성 옵션을 사용 하면 포털 외부에서 Azure에 완전된 한 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-559">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="12d02-560">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-560">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="12d02-561">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="12d02-561">![Creating a new Web Site using Quick Create](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="12d02-562">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="12d02-562">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="12d02-563">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-563">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="12d02-564">웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-564">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="12d02-565">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-565">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="12d02-566">![새 웹 사이트를 찾아](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="12d02-566">![Browsing to the new web site](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="12d02-567">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="12d02-567">*Browsing to the new web site*</span></span>

    <span data-ttu-id="12d02-568">![실행 중인 웹 사이트](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="12d02-568">![Web site running](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "Web site running")</span></span>

    <span data-ttu-id="12d02-569">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="12d02-569">*Web site running*</span></span>
6. <span data-ttu-id="12d02-570">포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-570">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="12d02-571">![웹 사이트 관리 페이지를 열어](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="12d02-571">![Opening the web site management pages](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="12d02-572">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="12d02-572">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="12d02-573">**대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.</span><span class="sxs-lookup"><span data-stu-id="12d02-573">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-574">합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Azure에 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-574">The *publish profile* contains all of the information required to publish a web application to Azure for each enabled publication method.</span></span> <span data-ttu-id="12d02-575">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-575">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="12d02-576">**Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Azure에 웹 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-576">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="12d02-577">![게시 프로필 다운로드 웹 사이트](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="12d02-577">![Downloading the web site publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="12d02-578">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="12d02-578">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="12d02-579">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-579">Download the publish profile file to a known location.</span></span> <span data-ttu-id="12d02-580">추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 Azure에 웹 응용 프로그램을 게시 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-580">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="12d02-581">![게시 프로필 파일을 저장](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="12d02-581">![Saving the publish profile file](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "Saving the publish profile")</span></span>

    <span data-ttu-id="12d02-582">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="12d02-582">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="12d02-583">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="12d02-583">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="12d02-584">응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-584">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="12d02-585">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-585">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="12d02-586">응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-586">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="12d02-587">SQL Database 서버에 Azure 관리 포털의 구독에서 볼 수 있습니다 **Sql Database** | **서버** | **서버대시보드**.</span><span class="sxs-lookup"><span data-stu-id="12d02-587">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="12d02-588">만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-588">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="12d02-589">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-589">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="12d02-590">만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-590">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="12d02-591">![SQL Database 서버 대시보드](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="12d02-591">![SQL Database Server Dashboard](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="12d02-592">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="12d02-592">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="12d02-593">다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-593">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="12d02-594">이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-594">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    <span data-ttu-id="12d02-596">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="12d02-596">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="12d02-597">한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-597">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    <span data-ttu-id="12d02-599">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="12d02-599">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="12d02-600">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="12d02-600">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="12d02-601">ASP.NET MVC 4 솔루션 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-601">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="12d02-602">에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-602">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="12d02-603">![응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="12d02-603">![Publishing the Application](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "Publishing the Application")</span></span>

    <span data-ttu-id="12d02-604">*웹 사이트를 게시합니다.*</span><span class="sxs-lookup"><span data-stu-id="12d02-604">*Publishing the web site*</span></span>
2. <span data-ttu-id="12d02-605">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-605">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="12d02-606">![게시 프로필 가져오기](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="12d02-606">![Importing the publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "Importing the publish profile")</span></span>

    <span data-ttu-id="12d02-607">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="12d02-607">*Importing publish profile*</span></span>
3. <span data-ttu-id="12d02-608">클릭 **연결의 유효성을 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-608">Click **Validate Connection**.</span></span> <span data-ttu-id="12d02-609">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-609">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12d02-610">연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-610">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="12d02-611">![연결 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="12d02-611">![Validating connection](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "Validating connection")</span></span>

    <span data-ttu-id="12d02-612">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="12d02-612">*Validating connection*</span></span>
4. <span data-ttu-id="12d02-613">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="12d02-613">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="12d02-614">![웹 배포 구성](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="12d02-614">![Web deploy configuration](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy configuration")</span></span>

    <span data-ttu-id="12d02-615">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="12d02-615">*Web deploy configuration*</span></span>
5. <span data-ttu-id="12d02-616">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-616">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="12d02-617">에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-617">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="12d02-618">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-618">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="12d02-619">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-619">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="12d02-620">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-620">Type a new database name.</span></span>

     <span data-ttu-id="12d02-621">![대상 연결 문자열 구성](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="12d02-621">![Configuring destination connection string](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="12d02-622">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="12d02-622">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="12d02-623">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-623">Then click **OK**.</span></span> <span data-ttu-id="12d02-624">데이터베이스를 만들라는 메시지가 나오면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-624">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="12d02-625">![데이터베이스를 만드는](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="12d02-625">![Creating the database](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "Creating the database string")</span></span>

    <span data-ttu-id="12d02-626">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="12d02-626">*Creating the database*</span></span>
7. <span data-ttu-id="12d02-627">기본 연결 텍스트 상자 내에서 사용 하 여 Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-627">The connection string you will use to connect to SQL Database in Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="12d02-628">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-628">Then click **Next**.</span></span>

    <span data-ttu-id="12d02-629">![SQL Database를 가리키는 연결 문자열](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="12d02-629">![Connection string pointing to SQL Database](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="12d02-630">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="12d02-630">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="12d02-631">에 **미리 보기** 페이지에서 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-631">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="12d02-632">![웹 응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="12d02-632">![Publishing the web application](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Publishing the web application")</span></span>

    <span data-ttu-id="12d02-633">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="12d02-633">*Publishing the web application*</span></span>
9. <span data-ttu-id="12d02-634">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-634">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="12d02-635">부록 c: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="12d02-635">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="12d02-636">코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-636">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="12d02-637">랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-637">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="12d02-638">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")</span><span class="sxs-lookup"><span data-stu-id="12d02-638">![Using Visual Studio code snippets to insert code into your project](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="12d02-639">*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="12d02-639">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="12d02-640">***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="12d02-640">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="12d02-641">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-641">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="12d02-642">시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-642">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="12d02-643">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-643">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="12d02-644">올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="12d02-644">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="12d02-645">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-645">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="12d02-646">![코드 조각 이름을 입력](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="12d02-646">![Start typing the snippet name](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "Start typing the snippet name")</span></span>

<span data-ttu-id="12d02-647">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="12d02-647">*Start typing the snippet name*</span></span>

<span data-ttu-id="12d02-648">![Tab 키를 눌러 강조 표시 된 코드 조각을](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="12d02-648">![Press Tab to select the highlighted snippet](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="12d02-649">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="12d02-649">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="12d02-650">![Tab 키를 다시 코드 조각 확장 됩니다](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")</span><span class="sxs-lookup"><span data-stu-id="12d02-650">![Press Tab again and the snippet will expand](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="12d02-651">*Tab 키를 다시 및 코드 조각에서는 확장*</span><span class="sxs-lookup"><span data-stu-id="12d02-651">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="12d02-652">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-652">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="12d02-653">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-653">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="12d02-654">선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-654">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="12d02-655">클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d02-655">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="12d02-656">![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")</span><span class="sxs-lookup"><span data-stu-id="12d02-656">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="12d02-657">*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="12d02-657">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="12d02-658">![클릭 하 여 목록에서 관련 코드 조각 선택](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "클릭 하 여 목록에서 관련 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="12d02-658">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="12d02-659">*클릭 하 여 목록에서 관련 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="12d02-659">*Pick the relevant snippet from the list, by clicking on it*</span></span>
