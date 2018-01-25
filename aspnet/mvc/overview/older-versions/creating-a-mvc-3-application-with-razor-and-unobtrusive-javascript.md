---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: "만드는 MVC 3 Application with Razor and Unobtrusive JavaScript | Microsoft Docs"
author: microsoft
description: "사용자 목록 예제 웹 응용 프로그램 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다. 샘플 응용 프로그램 s 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/01/2010
ms.topic: article
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: 29b45c07b5498542abbf22c4c3001b1cee41edc9
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="152ae-104">만드는 MVC 3 Application with Razor and Unobtrusive JavaScript</span><span class="sxs-lookup"><span data-stu-id="152ae-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>
====================
<span data-ttu-id="152ae-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="152ae-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="152ae-106">사용자 목록 예제 웹 응용 프로그램 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="152ae-107">샘플 응용 프로그램 만들기, 표시, 편집 및 삭제 하는 중 사용자가 같은 기능을 포함 하는 가상의 사용자 목록 웹 사이트를 만드는 ASP.NET MVC 버전 3와 새로운 Razor 뷰 엔진 및 Visual Studio 2010을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="152ae-108">이 자습서에서는 사용자 목록 샘플 ASP.NET MVC 3 응용 프로그램을 작성 하기 위해 수행 된 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="152ae-109">C# 및 VB 소스 코드를 Visual Studio 프로젝트는이 항목에 수반: [다운로드](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="152ae-110">이 자습서에 대 한 질문이 있으면 하십시오에 게시 하는 [MVC 포럼](https://forums.asp.net/1146.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>


## <a name="overview"></a><span data-ttu-id="152ae-111">개요</span><span class="sxs-lookup"><span data-stu-id="152ae-111">Overview</span></span>

<span data-ttu-id="152ae-112">에서는 빌드할 응용 프로그램은 간단한 사용자 목록 웹사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="152ae-113">사용자가 입력, 보기 및 사용자 정보를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-113">Users can enter, view, and update user information.</span></span>

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="152ae-115">완료 된 VB 및 C# 프로젝트를 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="152ae-116">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="152ae-116">Creating the Web Application</span></span>

<span data-ttu-id="152ae-117">이 자습서를 시작 하려면 Visual Studio 2010 열고 사용 하 여 새 프로젝트를 만들는 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿.</span><span class="sxs-lookup"><span data-stu-id="152ae-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="152ae-118">응용 프로그램의 이름을 &quot;Mvc3Razor&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="152ae-119">[![새 MVC 3 프로젝트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="152ae-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="152ae-120">에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**Razor 뷰 엔진을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![새 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="152ae-122">이 자습서에서는 있습니다를 사용 하지 않는 ASP.NET 멤버 자격 공급자 로그온 및 멤버와 관련 된 모든 파일을 삭제할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="152ae-123">**솔루션 탐색기**, 다음과 같은 파일 및 디렉터리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="152ae-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="152ae-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="152ae-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="152ae-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="152ae-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="152ae-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="152ae-127">*Views\Account* (및이 디렉터리에 있는 모든 파일)</span><span class="sxs-lookup"><span data-stu-id="152ae-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="152ae-129">편집 된  *\_Layout.cshtml* 내부의 태그를 바꾸고 파일는 `<div>` 라는 요소 `logindisplay` 메시지와 함께  *&quot;* 로그인 비활성화&quot;.</span><span class="sxs-lookup"><span data-stu-id="152ae-129">Edit the *\_Layout.cshtml* file and replace the markup inside the `<div>` element named `logindisplay` with the message *&quot;*Login Disabled&quot;.</span></span> <span data-ttu-id="152ae-130">다음 예제에서는 새 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="152ae-131">모델 추가</span><span class="sxs-lookup"><span data-stu-id="152ae-131">Adding the Model</span></span>

<span data-ttu-id="152ae-132">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**, 클릭 하 고 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="152ae-134">클래스 이름을 `UserModel`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-134">Name the class `UserModel`.</span></span> <span data-ttu-id="152ae-135">내용을 대체는 *UserModel* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="152ae-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="152ae-136">`UserModel` 클래스는 사용자가 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="152ae-137">클래스의 각 멤버는 주석을 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 에서 특성의 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="152ae-138">에 있는 특성의 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스 웹 응용 프로그램에 대 한 자동 클라이언트 및 서버 쪽 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="152ae-139">열기는 `HomeController` 클래스 및 추가 `using` 액세스할 수 있도록 지시문은 `UserModel` 및 `Users` 클래스:</span><span class="sxs-lookup"><span data-stu-id="152ae-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="152ae-140">바로 뒤의 `HomeController` 선언 다음 주석 및에 대 한 참조 추가 `Users` 클래스:</span><span class="sxs-lookup"><span data-stu-id="152ae-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="152ae-141">`Users` 클래스는이 자습서에서 사용 하는 간소화 된 메모리 내 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="152ae-142">실제 응용 프로그램에서 사용자 정보를 저장 하는 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="152ae-143">처음 몇 줄의 `HomeController` 파일은 다음 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="152ae-144">사용자 모델 스 캐 폴딩 마법사는 다음 단계에서 사용할 수 있도록 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="152ae-145">기본 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="152ae-145">Creating the Default View</span></span>

<span data-ttu-id="152ae-146">다음 단계는 작업 메서드 및 사용자가 표시 하려면 보기를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="152ae-147">기존 삭제 *Views\Home\Index* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="152ae-148">새 만들려는 *인덱스* 파일을 사용자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="152ae-149">에 `HomeController` 클래스의 내용을 대체는 `Index` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="152ae-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="152ae-150">마우스 오른쪽 단추로 클릭는 `Index` 메서드와 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="152ae-152">선택 된 **강력한 형식의 뷰 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="152ae-153">에 대 한 **데이터 클래스 보기**선택, **Mvc3Razor.Models.UserModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="152ae-154">(표시 되지 않으면 **Mvc3Razor.Models.UserModel** 에 **데이터 클래스 보기** 프로젝트를 빌드하는 데 필요한 상자입니다.) 뷰 엔진 설정 되어 있는지 확인 **Razor**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="152ae-155">설정 **콘텐츠를 볼** 를 **목록** 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-155">Set **View content** to **List** and then click **Add**.</span></span>

![인덱스 뷰를 추가 합니다.](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="152ae-157">새 보기에 전달 되는 사용자 데이터를 자동으로 scaffolds는 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="152ae-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="152ae-158">새로 생성 된 검사 *Views\Home\Index* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="152ae-159">**새로 만들기**, **편집**, **세부 정보**, 및 **삭제** 나머지 페이지는 작동 하지만 링크가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="152ae-160">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-160">Run the page.</span></span> <span data-ttu-id="152ae-161">사용자의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-161">You see a list of users.</span></span>

![인덱스 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="152ae-163">열기는 *Index.cshtml* 파일 및 바꾸기는 `ActionLink` 에 대 한 태그 **편집**, **세부 정보**, 및 **삭제** 를 다음 코드로 :</span><span class="sxs-lookup"><span data-stu-id="152ae-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="152ae-164">사용자 이름에서 선택한 레코드를 찾는 데 ID로 사용 됩니다는 **편집**, **세부 정보**, 및 **삭제** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="152ae-165">세부 정보 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="152ae-165">Creating the Details View</span></span>

<span data-ttu-id="152ae-166">다음 단계를 추가 하는 것을 `Details` 동작 메서드 및 사용자 세부 정보를 표시 하기 위해 보기.</span><span class="sxs-lookup"><span data-stu-id="152ae-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="152ae-168">다음 추가 `Details` 메서드를 home 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="152ae-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="152ae-169">마우스 오른쪽 단추로 클릭는 `Details` 메서드와 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-169">Right-click inside the `Details` method and then select **Add View**.</span></span> <span data-ttu-id="152ae-170">되어 있는지 확인은 **데이터 클래스 보기** 상자에 **Mvc3Razor.Models.UserModel*** 합니다.*</span><span class="sxs-lookup"><span data-stu-id="152ae-170">Verify that the **View data class** box contains **Mvc3Razor.Models.UserModel***.*</span></span> <span data-ttu-id="152ae-171">설정 **콘텐츠를 볼** 를 **세부 정보** 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-171">Set **View content** to **Details** and then click **Add**.</span></span>

![추가 세부 정보 보기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="152ae-173">응용 프로그램을 실행 하 고 세부 정보 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-173">Run the application and select a details link.</span></span> <span data-ttu-id="152ae-174">자동 스 캐 폴딩 모델의 각 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-174">The automatic scaffolding shows each property in the model.</span></span>

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="152ae-176">편집 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="152ae-176">Creating the Edit View</span></span>

<span data-ttu-id="152ae-177">다음 추가 `Edit` 메서드를 home 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="152ae-178">이전 단계에서와 같이 뷰를 추가 하지만 설정 **콘텐츠를 볼** 를 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![편집 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="152ae-180">응용 프로그램을 실행 하 고 사용자가 중 하나의 이름과 성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="152ae-181">위반 하면 `DataAnnotation` 에 적용 된 제약 조건에서 `UserModel` 클래스에서는 양식을 제출 하기 보게 서버 코드에서 생성 되는 유효성 검사 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="152ae-182">예를 들어, 첫 번째 이름을 변경 하면 &quot;Ann&quot; 를 &quot;A&quot;양식을 전송할 때, 폼에 다음 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="152ae-183">이 자습서에서는 기본 키로 사용자 이름을 처리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="152ae-184">따라서 사용자 이름 속성을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="152ae-185">에 *Edit.cshtml* 파일, 바로 뒤의 `Html.BeginForm` 문, 숨겨진 필드를 사용자 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="152ae-186">이렇게 하면 속성을 모델에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="152ae-187">다음 코드 조각 표시의 배치는 `Hidden` 문:</span><span class="sxs-lookup"><span data-stu-id="152ae-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="152ae-188">대체는 `TextBoxFor` 및 `ValidationMessageFor` 와 사용자 이름에 대 한 태그는 `DisplayFor` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="152ae-189">`DisplayFor` 메서드는 읽기 전용 요소도 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="152ae-190">다음 예제에서는 완성 된 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-190">The following example shows the completed markup.</span></span> <span data-ttu-id="152ae-191">원래 `TextBoxFor` 및 `ValidationMessageFor` 호출 주석으로 처리 되어 Razor 주석 시작 및 끝 주석 문자 (`@* *@`)</span><span class="sxs-lookup"><span data-stu-id="152ae-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="152ae-192">클라이언트 쪽 유효성 검사를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="152ae-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="152ae-193">ASP.NET MVC 3의 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 두 플래그를 설정 해야 하 고 3 개의 JavaScript 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="152ae-194">응용 프로그램의 열고 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="152ae-195">확인 `that ClientValidationEnabled` 및 `UnobtrusiveJavaScriptEnabled` 로 설정 된 응용 프로그램 설정에 true입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="152ae-196">조각 루트에서 *Web.config* 파일의 올바른 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="152ae-197">설정 `UnobtrusiveJavaScriptEnabled` true를 사용 하면 비 가시적인 Ajax 및 비 가시적인 클라이언트 유효성 검사를 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="152ae-198">비 가시적인 유효성 검사를 사용 하면 유효성 검사 규칙은 HTML5 특성으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="152ae-199">HTML5 특성 이름은 소문자, 숫자 및 대시만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="152ae-200">설정 `ClientValidationEnabled` true 이면 클라이언트 쪽 유효성 검사를 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="152ae-201">응용 프로그램에서 이러한 키를 설정 하 여 *Web.config* 파일, 클라이언트 유효성 검사 및 전체 응용 프로그램에 대 한 비 가시적인 JavaScript를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="152ae-202">또한 다음 코드를 사용 하 여 컨트롤러 메서드 또는 개별 보기에서 이러한 설정을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="152ae-203">렌더링 된 보기에 여러 개의 JavaScript 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="152ae-204">모든 보기에는 JavaScript를 포함 하는 쉬운 방법을를 추가 하는 것은 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="152ae-205">대체는 `<head>` 의 요소는  *\_Layout.cshtml* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="152ae-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="152ae-206">처음 두 jQuery 스크립트에서의 Microsoft Ajax CDN 콘텐츠 배달 네트워크 ()에 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="152ae-207">Microsoft Ajax CDN을 활용 하 여 응용 프로그램의 최초로 성능을 크게 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="152ae-208">응용 프로그램을 실행 하 고 편집 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-208">Run the application and click an edit link.</span></span> <span data-ttu-id="152ae-209">브라우저에서 페이지의 소스를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-209">View the page's source in the browser.</span></span> <span data-ttu-id="152ae-210">폼의 많은 특성을 표시 하는 브라우저 소스 `data-val` (에 대해 데이터 유효성 검사).</span><span class="sxs-lookup"><span data-stu-id="152ae-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="152ae-211">클라이언트 유효성 검사 규칙으로 입력된 필드를 포함 하는 클라이언트 유효성 검사 및 비간섭 JavaScript를 사용 하는 경우는 `data-val="true"` 비 가시적인 클라이언트 유효성 검사 트리거 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="152ae-212">예를 들어는 `City` 모델의 필드로 데코레이팅 되었습니다는 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 그 결과 다음 예제에 표시 된 HTML 특성:</span><span class="sxs-lookup"><span data-stu-id="152ae-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="152ae-213">각 클라이언트 유효성 검사 규칙에 대 한 특성이 있는 폼 추가 된 `data-val-rulename="message"`합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="152ae-214">사용 하는 `City` 필드 이전 예제를 필요한 클라이언트 유효성 검사 규칙 생성는 `data-val-required` 특성 및 메시지 &quot;The City 필드는 필수&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="152ae-215">응용 프로그램을 실행, 하나는 사용자를 편집 및 선택 취소 된 `City` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="152ae-216">필드에서 이동 하는 경우 클라이언트 쪽 유효성 검사 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![필요 시](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="152ae-218">마찬가지로, 클라이언트 유효성 검사 규칙의 각 매개 변수에 대해 특성이 추가 되는 형식을 포함 하는 `data-val-rulename-paramname=paramvalue`합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="152ae-219">예를 들어는 `FirstName` 속성으로 추적이 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성 및 3의 최소 길이 및 최대 길이가 8 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="152ae-220">명명 된 데이터 유효성 검사 규칙 `length` 매개 변수 이름이 `max` 및 매개 변수 값은 8입니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="152ae-221">다음 테이블에 대해 생성 되는 HTML 나와 `FirstName` 사용자 중 하나를 편집 하는 경우 필드:</span><span class="sxs-lookup"><span data-stu-id="152ae-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="152ae-222">비 가시적인 클라이언트 유효성 검사에 대 한 자세한 내용은 항목을 참조 하십시오. [ASP.NET MVC 3에서 비간섭 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) Brad Wilson의 블로그에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="152ae-223">ASP.NET MVC 3 베타 버전에서는 클라이언트 쪽 유효성 검사를 시작 하기 위해 폼을 제출 해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="152ae-224">이 최종 릴리스에 대 한 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-224">This might be changed for the final release.</span></span>


## <a name="creating-the-create-view"></a><span data-ttu-id="152ae-225">만들기 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="152ae-225">Creating the Create View</span></span>

<span data-ttu-id="152ae-226">다음 단계를 추가 하는 것을 `Create` 동작 메서드 및 사용자를 새 사용자를 만들 수 있도록 하려면 보기.</span><span class="sxs-lookup"><span data-stu-id="152ae-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="152ae-227">다음 추가 `Create` 메서드를 home 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="152ae-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="152ae-228">이전 단계에서와 같이 뷰를 추가 하지만 설정 **콘텐츠를 볼** 를 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![뷰 만들기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="152ae-230">응용 프로그램을 실행, 선택는 **만들기** 링크를 선택한 새 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="152ae-231">`Create` 메서드 자동으로에서는 클라이언트 쪽 및 서버측 유효성 검사 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="152ae-232">와 같은 경우를 포함 하는 사용자 이름을 입력 하려고 &quot;Ben X&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="152ae-233">클라이언트 쪽 유효성 검사 오류를 사용자 이름 필드에서 이동 하는 경우 (`White space is not allowed`) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="152ae-234">Delete 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-234">Add the Delete method</span></span>

<span data-ttu-id="152ae-235">이 자습서를 수행 하려면 다음 추가 `Delete` 메서드를 home 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="152ae-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="152ae-236">추가 `Delete` 설정 하 고 이전 단계에서와 같이 보기 **콘텐츠를 볼** 를 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![뷰 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="152ae-238">유효성 검사는 간단 하지만 모든 기능을 갖춘 ASP.NET MVC 3 응용 프로그램을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="152ae-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
