---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 만들기는 MVC 3 Application with Razor and Unobtrusive JavaScript | Microsoft Docs
author: microsoft
description: 사용자 목록 샘플 웹 응용 프로그램에서는 Razor 보기 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 얼마나 간단한 지 보여 줍니다. 샘플 응용 프로그램 s...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/01/2010
ms.topic: article
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: 39ed35c1b7d5c702ffea6908daeac5ca12f1693e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398015"
---
<a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="e4506-104">만들기는 MVC 3 Razor 및 비간섭 JavaScript를 사용 하 여 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e4506-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>
====================
<span data-ttu-id="e4506-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e4506-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e4506-106">사용자 목록 샘플 웹 응용 프로그램에서는 Razor 보기 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 얼마나 간단한 지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="e4506-107">샘플 응용 프로그램 작성, 표시, 편집 및 삭제 사용자 등의 기능을 포함 하는 가상의 사용자 목록 웹 사이트를 만드는 ASP.NET MVC 버전 3 사용 하 여 새로운 Razor 보기 엔진 및 Visual Studio 2010을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="e4506-108">이 자습서에는 사용자 목록 샘플 ASP.NET MVC 3 응용 프로그램을 빌드하기 위해 수행 된 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="e4506-109">C# 및 VB 소스 코드를 사용 하 여 Visual Studio 프로젝트는 다음이 항목과 함께 사용할 수 있습니다: [다운로드](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="e4506-110">이 자습서에 대 한 질문이 있으면 게시 하세요 하는 [MVC 포럼](https://forums.asp.net/1146.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>


## <a name="overview"></a><span data-ttu-id="e4506-111">개요</span><span class="sxs-lookup"><span data-stu-id="e4506-111">Overview</span></span>

<span data-ttu-id="e4506-112">응용 프로그램 작성 하는 간단한 사용자 목록 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="e4506-113">사용자 입력, 보기 및 사용자 정보를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-113">Users can enter, view, and update user information.</span></span>

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="e4506-115">완료 된 VB와 C# 프로젝트를 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="e4506-116">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e4506-116">Creating the Web Application</span></span>

<span data-ttu-id="e4506-117">자습서를 시작 하려면 Visual Studio 2010 열고 사용 하 여 새 프로젝트를 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿.</span><span class="sxs-lookup"><span data-stu-id="e4506-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="e4506-118">응용 프로그램의 이름을 &quot;Mvc3Razor&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="e4506-119">[![새 MVC 3 프로젝트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="e4506-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="e4506-120">에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**Razor 보기 엔진을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![새 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="e4506-122">이 자습서에서는 하지 사용할 ASP.NET 멤버 자격 공급자에서 로그온 및 멤버 자격을 사용 하 여 연결 된 모든 파일을 삭제할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="e4506-123">**솔루션 탐색기**, 다음 파일 및 디렉터리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="e4506-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="e4506-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="e4506-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="e4506-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="e4506-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="e4506-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="e4506-127">*Views\Account* (및이 디렉터리의 모든 파일)</span><span class="sxs-lookup"><span data-stu-id="e4506-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="e4506-129">편집를  <em>\_Layout.cshtml</em> 내에서 태그를 바꾸고 파일을 `<div>` 라는 요소가 `logindisplay` 메시지와 함께 <em>&quot;</em>로그인 사용 안 함&quot;.</span><span class="sxs-lookup"><span data-stu-id="e4506-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="e4506-130">다음 예제에서는 새 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="e4506-131">모델 추가</span><span class="sxs-lookup"><span data-stu-id="e4506-131">Adding the Model</span></span>

<span data-ttu-id="e4506-132">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 클릭 하 고 **클래스**.</span><span class="sxs-lookup"><span data-stu-id="e4506-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="e4506-134">클래스 이름을 `UserModel`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-134">Name the class `UserModel`.</span></span> <span data-ttu-id="e4506-135">내용을 대체 합니다 *UserModel* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="e4506-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="e4506-136">`UserModel` 클래스는 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="e4506-137">으로 주석이 달린 클래스의 각 멤버는 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 에서 특성을 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="e4506-138">특성을 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스 웹 응용 프로그램에 대 한 자동 클라이언트 및 서버 쪽 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="e4506-139">열기는 `HomeController` 클래스 및 추가 `using` 지시문에 액세스할 수 있도록 합니다 `UserModel` 및 `Users` 클래스:</span><span class="sxs-lookup"><span data-stu-id="e4506-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="e4506-140">바로 뒤의 `HomeController` 선언 다음 주석 및에 대 한 참조 추가 `Users` 클래스:</span><span class="sxs-lookup"><span data-stu-id="e4506-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="e4506-141">`Users` 클래스는이 자습서에서 사용 하는 간단한 메모리 내 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="e4506-142">실제 응용 프로그램에서 데이터베이스를 사용 하면 사용자 정보 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="e4506-143">처음 몇 줄의 `HomeController` 파일은 다음 예제에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="e4506-144">사용자 모델을 스 캐 폴딩 마법사는 다음 단계에서 사용할 수 있도록 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="e4506-145">기본 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e4506-145">Creating the Default View</span></span>

<span data-ttu-id="e4506-146">다음 단계는 작업 메서드 및 사용자를 표시 하려면 보기를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="e4506-147">기존 삭제할 *Views\Home\Index* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="e4506-148">새로 만든 *인덱스* 사용자를 표시 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="e4506-149">에 `HomeController` 클래스의 내용을 대체 합니다 `Index` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="e4506-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="e4506-150">마우스 오른쪽 단추로 클릭 합니다 `Index` 메서드와 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="e4506-152">선택 된 **강력한 형식의 뷰를 만들** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="e4506-153">에 대 한 **데이터 클래스를 보려면**를 선택 **Mvc3Razor.Models.UserModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="e4506-154">(표시 되지 않는 경우 **Mvc3Razor.Models.UserModel** 에 **데이터 클래스 보기** 프로젝트를 빌드할 필요가 상자입니다.) 뷰 엔진 설정 되어 있는지 확인 하십시오 **Razor**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="e4506-155">설정 **콘텐츠를 볼** 하 **목록** 을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-155">Set **View content** to **List** and then click **Add**.</span></span>

![인덱스 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="e4506-157">새 보기에 전달 되는 사용자 데이터를 자동으로 스 캐 폴딩 합니다 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="e4506-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="e4506-158">새로 생성 된 검사할 *Views\Home\Index* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="e4506-159">합니다 **새로 만들기**를 **편집**를 **세부 정보**, 및 **삭제** 링크가 작동 하지 않습니다 하지만 페이지의 나머지 부분은 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="e4506-160">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-160">Run the page.</span></span> <span data-ttu-id="e4506-161">사용자의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-161">You see a list of users.</span></span>

![인덱스 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="e4506-163">열기는 *Index.cshtml* 바꾸고 파일을 `ActionLink` 에 대 한 태그 **편집**를 **세부 정보**, 및 **삭제** 다음 코드를 사용 하 여 :</span><span class="sxs-lookup"><span data-stu-id="e4506-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="e4506-164">사용자 이름에서 선택한 레코드를 찾는 데 ID로 사용 됩니다 합니다 **편집할**, **세부 정보**, 및 **삭제** 링크.</span><span class="sxs-lookup"><span data-stu-id="e4506-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="e4506-165">자세히 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="e4506-165">Creating the Details View</span></span>

<span data-ttu-id="e4506-166">다음 단계를 추가 하는 것을 `Details` 작업 메서드 및 사용자 세부 정보를 표시 하기 위해 보기.</span><span class="sxs-lookup"><span data-stu-id="e4506-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="e4506-168">다음 추가 `Details` 메서드를 home 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="e4506-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="e4506-169">마우스 오른쪽 단추로 클릭 합니다 `Details` 한 다음 선택한 메서드 <strong>뷰 추가</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="e4506-170">있는지 확인 합니다 <strong>데이터 클래스를 보려면</strong> 상자에 <strong>Mvc3Razor.Models.UserModel</strong><em>합니다.</em></span><span class="sxs-lookup"><span data-stu-id="e4506-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="e4506-171">설정 <strong>콘텐츠를 볼</strong> 하 <strong>세부 정보</strong> 을 클릭 한 다음 <strong>추가</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![세부 정보 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="e4506-173">응용 프로그램을 실행 하 고 세부 정보 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-173">Run the application and select a details link.</span></span> <span data-ttu-id="e4506-174">자동 스 캐 폴딩을 모델의 각 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-174">The automatic scaffolding shows each property in the model.</span></span>

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="e4506-176">편집 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="e4506-176">Creating the Edit View</span></span>

<span data-ttu-id="e4506-177">다음 추가 `Edit` 메서드를 home 컨트롤러.</span><span class="sxs-lookup"><span data-stu-id="e4506-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="e4506-178">이전 단계와 같이 뷰를 추가 하지만 설정 **콘텐츠 보기** 하 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![편집 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="e4506-180">응용 프로그램을 실행 하 고 사용자 중의 첫 번째 및 마지막 이름을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="e4506-181">하나라도 위반 하면 `DataAnnotation` 에 적용 된 제약 조건은 `UserModel` 클래스 폼을 제출할 때 표시 됩니다 서버 코드에서 생성 되는 유효성 검사 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="e4506-182">예를 들어, 첫 번째 이름을 변경한 경우 &quot;Ann&quot; 하 &quot;는&quot;폼을 제출 하는 경우 폼에 다음 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="e4506-183">이 자습서에서는 기본 키로 사용자 이름을 처리 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="e4506-184">따라서 사용자 이름 속성을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="e4506-185">에 *Edit.cshtml* 파일을 바로 뒤를 `Html.BeginForm` 문에 숨겨진 필드를 사용자 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="e4506-186">이렇게 하면 모델에 전달할 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="e4506-187">다음 코드 조각 표시의 배치를 `Hidden` 문:</span><span class="sxs-lookup"><span data-stu-id="e4506-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="e4506-188">대체는 `TextBoxFor` 하 고 `ValidationMessageFor` 사용 하 여 사용자 이름에 대 한 태그를 `DisplayFor` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="e4506-189">`DisplayFor` 메서드는 읽기 전용 요소와 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="e4506-190">다음 예제에서는 전체 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-190">The following example shows the completed markup.</span></span> <span data-ttu-id="e4506-191">원래 `TextBoxFor` 하 고 `ValidationMessageFor` Razor 주석 시작 및 끝 주석 문자로 호출 머릿말 (`@* *@`)</span><span class="sxs-lookup"><span data-stu-id="e4506-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="e4506-192">클라이언트 쪽 유효성 검사를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e4506-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="e4506-193">ASP.NET MVC 3의 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 두 플래그를 설정 해야 하 고 세 개의 JavaScript 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="e4506-194">응용 프로그램을 엽니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="e4506-195">확인 `that ClientValidationEnabled` 및 `UnobtrusiveJavaScriptEnabled` 로 설정 된 응용 프로그램 설정에 true입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="e4506-196">루트에서 다음 조각은 *Web.config* 파일에 올바른 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="e4506-197">설정 `UnobtrusiveJavaScriptEnabled` 비간섭 Ajax를 사용 하도록 설정 하 고 비 가시적인 클라이언트 유효성 검사를 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="e4506-198">비간섭 유효성 검사를 사용 하면 유효성 검사 규칙은 HTML5 특성으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="e4506-199">HTML5 특성 이름은 소문자, 숫자 및 대시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="e4506-200">설정 `ClientValidationEnabled` true로 설정 하면 클라이언트 쪽 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="e4506-201">응용 프로그램에서 이러한 키를 설정 하 여 *Web.config* 파일인 클라이언트 유효성 검사 및 전체 응용 프로그램에 대 한 비간섭 JavaScript를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="e4506-202">사용 하도록 설정 하거나 개별 뷰 또는 컨트롤러 메서드에서 다음 코드를 사용 하 여 이러한 설정을 사용 하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="e4506-203">렌더링된 된 보기에서 여러 개의 JavaScript 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="e4506-204">모든 보기에서 JavaScript를 포함 하는 쉬운 방법을 추가 하는 것은 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="e4506-205">대체는 `<head>` 의 요소를  *\_Layout.cshtml* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="e4506-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="e4506-206">처음 두 jQuery 스크립트에서 Microsoft Ajax 콘텐츠 배달 네트워크 (CDN)에 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="e4506-207">Microsoft Ajax CDN을 활용 하 여 응용 프로그램의 첫 번째 적중 성능을 크게 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="e4506-208">응용 프로그램을 실행 하 고 편집 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-208">Run the application and click an edit link.</span></span> <span data-ttu-id="e4506-209">브라우저에서 페이지의 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-209">View the page's source in the browser.</span></span> <span data-ttu-id="e4506-210">브라우저 소스를 폼의 많은 특성을 보여 줍니다. `data-val` (데이터 유효성 검사를 위해).</span><span class="sxs-lookup"><span data-stu-id="e4506-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="e4506-211">클라이언트 유효성 검사 규칙을 사용 하 여 입력된 필드를 포함 하는 클라이언트 유효성 검사 및 비간섭 JavaScript를 사용 하는 경우는 `data-val="true"` 비 가시적인 클라이언트 유효성 검사 트리거 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="e4506-212">예를 들어 합니다 `City` 모델의 필드에에서 지정 된 합니다 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 는 다음 예제와 같이 HTML 특성:</span><span class="sxs-lookup"><span data-stu-id="e4506-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="e4506-213">폼에 있는 특성은 추가 하는 각 클라이언트 유효성 검사 규칙에 대해 `data-val-rulename="message"`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="e4506-214">사용 하 여는 `City` 필드 이전 예제에 필요한 클라이언트 유효성 검사 규칙을 생성 합니다 `data-val-required` 특성 및 메시지 &quot;The City 필드는 필수&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="e4506-215">응용 프로그램을 실행, 사용자 중 하나를 편집 및 선택 취소 된 `City` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="e4506-216">필드에서 tab 키를 누르면, 클라이언트 쪽 유효성 검사 오류 메시지를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4506-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![필요한 도시](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="e4506-218">마찬가지로, 클라이언트 유효성 검사 규칙의 각 매개 변수에 특성이 추가 되는 형식은 `data-val-rulename-paramname=paramvalue`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="e4506-219">예를 들어, 합니다 `FirstName` 속성으로 주석이 달린 합니다 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성 및 3의 최소 길이 및 최대 길이는 8 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="e4506-220">명명 된 데이터 유효성 검사 규칙 `length` 매개 변수 이름이 `max` 및 매개 변수 값은 8입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="e4506-221">다음에 대해 생성 된 HTML 표시를 `FirstName` 사용자 중 하나를 편집 하는 경우 필드:</span><span class="sxs-lookup"><span data-stu-id="e4506-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="e4506-222">비 가시적인 클라이언트 유효성 검사에 대 한 자세한 내용은 항목을 참조 하세요 [ASP.NET MVC 3의 비간섭 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) Brad Wilson의 블로그에서입니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="e4506-223">ASP.NET MVC 3 베타의 경우에 따라 클라이언트 쪽 유효성 검사를 시작 하려면 양식을 제출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="e4506-224">이 최종 릴리스에서 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-224">This might be changed for the final release.</span></span>


## <a name="creating-the-create-view"></a><span data-ttu-id="e4506-225">만들기 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e4506-225">Creating the Create View</span></span>

<span data-ttu-id="e4506-226">다음 단계를 추가 하는 것을 `Create` 작업 메서드 및 사용자가 새 사용자를 만들 수 있도록 하려면 보기.</span><span class="sxs-lookup"><span data-stu-id="e4506-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="e4506-227">다음 추가 `Create` 메서드를 home 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="e4506-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="e4506-228">이전 단계와 같이 뷰를 추가 하지만 설정 **콘텐츠 보기** 하 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![뷰 만들기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="e4506-230">응용 프로그램 실행을 선택 합니다 **만들기** 링크를 선택한 새 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="e4506-231">`Create` 메서드 활용 클라이언트측 및 서버측 유효성 검사를 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="e4506-232">와 같은 공백을 포함 하는 사용자 이름을 입력 해 보세요 &quot;Ben X&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="e4506-233">사용자 이름 필드에 클라이언트 쪽 유효성 검사 오류를 탭 하는 경우 (`White space is not allowed`) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="e4506-234">Delete 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-234">Add the Delete method</span></span>

<span data-ttu-id="e4506-235">이 자습서를 완료 하려면 다음 추가 `Delete` 메서드를 home 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="e4506-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="e4506-236">추가 `Delete` 뷰 설정, 이전 단계와 같이 **콘텐츠를 보려면** 하 **삭제**.</span><span class="sxs-lookup"><span data-stu-id="e4506-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![뷰 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="e4506-238">이제 유효성 검사를 사용 하 여 ASP.NET MVC 3 application 간단 하지만 완벽 하 게 작동 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
