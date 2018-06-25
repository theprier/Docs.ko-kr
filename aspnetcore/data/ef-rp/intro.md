---
title: ASP.NET Core에서 Entity Framework Core를 사용한 Razor 페이지 - 자습서 1/8
author: rick-anderson
description: Entity Framework Core를 사용하여 Razor 페이지 앱을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/15/2017
uid: data/ef-rp/intro
ms.openlocfilehash: cadf36f4e1ff3776ad4139e1d7c4e9b73687bc5c
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36279232"
---
# <a name="razor-pages-with-entity-framework-core-in-aspnet-core---tutorial-1-of-8"></a><span data-ttu-id="90e0e-103">ASP.NET Core에서 Entity Framework Core를 사용한 Razor 페이지 - 자습서 1/8</span><span class="sxs-lookup"><span data-stu-id="90e0e-103">Razor Pages with Entity Framework Core in ASP.NET Core - Tutorial 1 of 8</span></span>

<span data-ttu-id="90e0e-104">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="90e0e-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="90e0e-105">Contoso University 샘플 웹앱은 EF(Entity Framework) Core 2.0 및 Visual Studio 2017을 사용하여 ASP.NET Core 2.0 MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-105">The Contoso University sample web app demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="90e0e-106">샘플 앱은 가상 Contoso University의 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-106">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="90e0e-107">학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-107">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="90e0e-108">이 페이지는 Contoso University 샘플 앱을 빌드하는 방법을 설명하는 일련의 자습서 중 첫 번째 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-108">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="90e0e-109">완성된 앱을 다운로드하거나 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="90e0e-109">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="90e0e-110">[지침을 다운로드하세요](xref:tutorials/index#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="90e0e-110">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90e0e-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="90e0e-111">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs.md)]

<span data-ttu-id="90e0e-112">[Razor 페이지](xref:razor-pages/index)에 익숙함.</span><span class="sxs-lookup"><span data-stu-id="90e0e-112">Familiarity with [Razor Pages](xref:razor-pages/index).</span></span> <span data-ttu-id="90e0e-113">신규 프로그래머는 이 시리즈를 시작하기 전에 [Razor 페이지 시작하기](xref:tutorials/razor-pages/razor-pages-start)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-113">New programmers should complete [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) before starting this series.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="90e0e-114">문제 해결</span><span class="sxs-lookup"><span data-stu-id="90e0e-114">Troubleshooting</span></span>

<span data-ttu-id="90e0e-115">해결할 수 없는 문제가 발생한 경우 일반적으로 [완료된 단계](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)와 코드를 비교하여 해결책을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-115">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots).</span></span> <span data-ttu-id="90e0e-116">일반적인 오류 목록 및 해결 방법은 [시리즈에서 마지막 자습서의 문제 해결 섹션](xref:data/ef-mvc/advanced#common-errors)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90e0e-116">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](xref:data/ef-mvc/advanced#common-errors).</span></span> <span data-ttu-id="90e0e-117">필요한 내용을 찾지 못한 경우 질문을 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 또는 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core)에 대한 [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-117">If you don't find what you need there, you can post a question to [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core) for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="90e0e-118">이 자습서 시리즈는 이전 자습서에서 수행되는 내용을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-118">This series of tutorials builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="90e0e-119">각 자습서를 성공적으로 완료한 후에 프로젝트 복사본의 저장을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-119">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="90e0e-120">문제가 발생한 경우 다시 처음으로 이동하는 대신 이전 자습서부터 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-120">If you run into problems, you can start over from the previous tutorial instead of going back to the beginning.</span></span> <span data-ttu-id="90e0e-121">또는 [완료된 단계](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)를 다운로드하고 완료된 단계를 사용하여 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-121">Alternatively, you can download a [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) and start over using the completed stage.</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="90e0e-122">Contoso University 웹앱</span><span class="sxs-lookup"><span data-stu-id="90e0e-122">The Contoso University web app</span></span>

<span data-ttu-id="90e0e-123">이러한 자습서에서 빌드한 앱은 기본 대학 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-123">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="90e0e-124">사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-124">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="90e0e-125">자습서에서 만든 화면 중 몇 가지 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-125">Here are a few of the screens created in the tutorial.</span></span>

![학생 인덱스 페이지](intro/_static/students-index.png)

![학생 편집 페이지](intro/_static/student-edit.png)

<span data-ttu-id="90e0e-128">이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 것과 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-128">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="90e0e-129">자습서는 UI가 아닌 Razor 페이지를 사용한 EF Core 자습서 위주로 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-129">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="90e0e-130">Razor 페이지 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="90e0e-130">Create a Razor Pages web app</span></span>

* <span data-ttu-id="90e0e-131">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-131">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="90e0e-132">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-132">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="90e0e-133">프로젝트 이름을 **ContosoUniversity**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-133">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="90e0e-134">코드를 복사/붙여넣을 때 네임스페이스와 일치할 수 있도록 프로젝트 이름을 *ContosoUniversity*로 지정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-134">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
 <span data-ttu-id="90e0e-135">![새 ASP.NET Core 웹 응용 프로그램](intro/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="90e0e-135">![new ASP.NET Core Web Application](intro/_static/np.png)</span></span>
* <span data-ttu-id="90e0e-136">드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-136">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="90e0e-137">![웹 응용 프로그램(Razor 페이지)](../../razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="90e0e-137">![Web Application (Razor Pages)](../../razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="90e0e-138">**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-138">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="90e0e-139">사이트 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="90e0e-139">Set up the site style</span></span>

<span data-ttu-id="90e0e-140">몇 가지 변경 내용으로 사이트 메뉴, 레이아웃 및 홈페이지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-140">A few changes set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="90e0e-141">*Pages/_Layout.cshtml*을 열고 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-141">Open *Pages/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="90e0e-142">모든 “ContosoUniversity”를 “Contoso University”로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-142">Change each occurrence of "ContosoUniversity" to "Contoso University."</span></span> <span data-ttu-id="90e0e-143">세 번 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-143">There are three occurrences.</span></span>

* <span data-ttu-id="90e0e-144">**학생**, **강좌**, **강사** 및 **부서**에 대한 메뉴 항목을 추가하고 **연락처** 메뉴 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-144">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="90e0e-145">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-145">The changes are highlighted.</span></span> <span data-ttu-id="90e0e-146">(모든 표시가 표시되지는 *않습니다*.)</span><span class="sxs-lookup"><span data-stu-id="90e0e-146">(All the markup is *not* displayed.)</span></span>

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-38,47&range=1-50)]

<span data-ttu-id="90e0e-147">*Pages/Index.cshtml*에서 다음 코드로 파일의 콘텐츠를 텍스트를 대체하여 ASP.NET 및 MVC에 대한 텍스트를 이 앱에 대한 텍스트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-147">In *Pages/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

<span data-ttu-id="90e0e-148">Ctrl+F5를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-148">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="90e0e-149">다음 자습서에서 만든 탭과 함께 홈페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-149">The home page is displayed with tabs created in the following tutorials:</span></span>

![Contoso University 홈페이지](intro/_static/home-page.png)

## <a name="create-the-data-model"></a><span data-ttu-id="90e0e-151">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="90e0e-151">Create the data model</span></span>

<span data-ttu-id="90e0e-152">Contoso University 앱에 대한 엔터티 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-152">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="90e0e-153">다음과 같은 세 가지 엔터티로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-153">Start with the following three entities:</span></span>

![과정-등록-학생 데이터 모델 다이어그램](intro/_static/data-model-diagram.png)

<span data-ttu-id="90e0e-155">`Student` 및 `Enrollment` 엔터티 사이에 일 대 다 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-155">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="90e0e-156">`Course` 및 `Enrollment` 엔터티 사이에 일 대 다 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-156">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="90e0e-157">학생은 여러 강좌에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-157">A student can enroll in any number of courses.</span></span> <span data-ttu-id="90e0e-158">강좌는 등록된 학생이 여러 명일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-158">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="90e0e-159">다음 섹션에서 각각에 대한 이러한 엔터티에 대한 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-159">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="90e0e-160">학생 엔터티</span><span class="sxs-lookup"><span data-stu-id="90e0e-160">The Student entity</span></span>

![학생 엔터티 다이어그램](intro/_static/student-entity.png)

<span data-ttu-id="90e0e-162">*모델* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-162">Create a *Models* folder.</span></span> <span data-ttu-id="90e0e-163">*모델* 폴더에서 다음 코드로 *Student.cs*라는 이름의 클래스 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-163">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="90e0e-164">`ID` 속성은 이 클래스에 해당하는 DB(데이터베이스) 테이블의 기본 키 열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-164">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="90e0e-165">기본적으로 EF 코어는 `ID` 또는 `classnameID`로 명명된 속성을 기본 키로 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-165">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span> <span data-ttu-id="90e0e-166">`classnameID`에서 `classname`은 앞의 예에 나온 `Student`와 같은 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-166">In `classnameID`, `classname` is the name of the class, such as `Student` in the preceding example.</span></span>

<span data-ttu-id="90e0e-167">`Enrollments` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-167">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="90e0e-168">탐색 속성은 이 엔터티와 관련된 다른 엔터티에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-168">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="90e0e-169">이 경우 `Student entity`의 `Enrollments` 속성은 해당 `Student`에 관련된 모든 `Enrollment` 엔터티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-169">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="90e0e-170">예를 들어 DB의 학생 행에 두 개의 관련 등록 행이 있는 경우 `Enrollments` 탐색 속성은 그 두 `Enrollment` 엔터티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-170">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="90e0e-171">관련된 `Enrollment` 행은 `StudentID` 열에서 해당 학생의 기본 키 값을 포함하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-171">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="90e0e-172">예를 들어 ID=1인 학생에 `Enrollment` 테이블의 두 개 행이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-172">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="90e0e-173">`Enrollment` 테이블에 `StudentID` = 1인 두 개의 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-173">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="90e0e-174">`StudentID`는 `Student` 테이블에서 학생을 지정하는 `Enrollment` 테이블의 외래 키입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-174">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="90e0e-175">탐색 속성이 여러 엔터티를 포함하는 경우 탐색 속성은 `ICollection<T>`와 같은 목록 유형이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-175">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="90e0e-176">`ICollection<T>`는 지정할 수 있으며, `List<T>` 또는 `HashSet<T>`와 같은 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-176">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="90e0e-177">`ICollection<T>`가 사용되는 경우 EF Core는 기본적으로 `HashSet<T>` 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-177">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="90e0e-178">여러 엔터티를 포함하는 탐색 속성은 다대다 및 일대다 관계에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-178">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="90e0e-179">등록 엔터티</span><span class="sxs-lookup"><span data-stu-id="90e0e-179">The Enrollment entity</span></span>

![등록 엔터티 다이어그램](intro/_static/enrollment-entity.png)

<span data-ttu-id="90e0e-181">*모델* 폴더에서 다음 코드로 *Enrollment.cs*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-181">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="90e0e-182">`EnrollmentID` 속성은 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-182">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="90e0e-183">이 엔터티는 `Student` 엔터티 같은 `ID` 대신 `classnameID` 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-183">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="90e0e-184">일반적으로 개발자는 하나의 패턴을 선택하여 데이터 모델 전체에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-184">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="90e0e-185">자습서의 뒷부분에서는 클래스 이름 없이 ID를 사용하여 더 손쉽게 데이터 모델에서 상속을 구현하는 내용이 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-185">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="90e0e-186">`Grade` 속성은 `enum`입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-186">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="90e0e-187">`Grade` 형식 선언 뒤에 있는 물음표는 `Grade` 속성이 nullable이라는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-187">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="90e0e-188">Null인 등급은 0 등급과는 다릅니다. Null은 알려지지 않거나 아직 등록되지 않은 등급을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-188">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="90e0e-189">`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-189">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="90e0e-190">`Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되므로 속성은 단일 `Student` 엔터티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-190">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="90e0e-191">`Student` 엔터티는 여러 `Enrollment` 엔터티를 포함하는 `Student.Enrollments` 탐색 속성과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-191">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="90e0e-192">`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-192">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="90e0e-193">`Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-193">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="90e0e-194">EF Core는 속성 이름이 `<navigation property name><primary key property name>`인 경우 외래 키로 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-194">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="90e0e-195">예를 들어 `Student` 탐색 속성의 경우 `Student` 엔터티의 기본 키가 `ID`이므로 `StudentID`입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-195">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="90e0e-196">외래 키 속성의 이름은 `<primary key property name>`으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-196">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="90e0e-197">예를 들어 `Course` 엔터티의 기본 키가 `CourseID`이므로 `CourseID`라고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-197">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="90e0e-198">강좌 엔터티</span><span class="sxs-lookup"><span data-stu-id="90e0e-198">The Course entity</span></span>

![강좌 엔터티 다이어그램](intro/_static/course-entity.png)

<span data-ttu-id="90e0e-200">*모델* 폴더에서 다음 코드로 *Course.cs*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-200">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="90e0e-201">`Enrollments` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-201">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="90e0e-202">`Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-202">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="90e0e-203">앱은 `DatabaseGenerated` 특성을 통해 DB가 생성하도록 하는 대신 기본 키를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-203">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="create-the-schoolcontext-db-context"></a><span data-ttu-id="90e0e-204">SchoolContext DB 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="90e0e-204">Create the SchoolContext DB context</span></span>

<span data-ttu-id="90e0e-205">특정 데이터 모델에 맞게 EF Core 기능을 조정하는 주 클래스는 DB 컨텍스트 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-205">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="90e0e-206">데이터 컨텍스트는 `Microsoft.EntityFrameworkCore.DbContext`에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-206">The data context is derived from `Microsoft.EntityFrameworkCore.DbContext`.</span></span> <span data-ttu-id="90e0e-207">데이터 컨텍스트는 데이터 모델에 포함되는 엔터티를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-207">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="90e0e-208">이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-208">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="90e0e-209">프로젝트 폴더에서 *Data*라는 이름의 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-209">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="90e0e-210">*Data* 폴더에서 다음 코드로 *SchoolContext.cs*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-210">In the *Data* folder create *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="90e0e-211">이 코드는 각 엔터티 집합에 대한 `DbSet` 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-211">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="90e0e-212">EF Core 용어에서:</span><span class="sxs-lookup"><span data-stu-id="90e0e-212">In EF Core terminology:</span></span>

* <span data-ttu-id="90e0e-213">엔터티 집합은 일반적으로 DB 테이블에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-213">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="90e0e-214">엔터티는 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-214">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="90e0e-215">`DbSet<Enrollment>` 및 `DbSet<Course>`는 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-215">`DbSet<Enrollment>` and `DbSet<Course>` can be omitted.</span></span> <span data-ttu-id="90e0e-216">`Student` 엔터티는 `Enrollment` 엔터티를 참조하고 `Enrollment` 엔터티는 `Course` 엔터티를 참조하기 때문에 EF Core는 이를 암시적으로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-216">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="90e0e-217">이 자습서의 경우 `DbSet<Enrollment>` 및 `DbSet<Course>`를 `SchoolContext`에 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-217">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

<span data-ttu-id="90e0e-218">DB가 만들어지면 EF Core는 `DbSet` 속성 이름과 동일한 이름을 갖는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-218">When the DB is created, EF Core creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="90e0e-219">컬렉션에 대한 속성 이름은 일반적으로 복수(Student가 아닌 Students)입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-219">Property names for collections are typically plural (Students rather than Student).</span></span> <span data-ttu-id="90e0e-220">개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-220">Developers disagree about whether table names should be plural.</span></span> <span data-ttu-id="90e0e-221">이러한 자습서의 경우 기본 동작은 DbContext에서 단수 테이블 이름을 지정하여 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-221">For these tutorials, the default behavior is overridden by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="90e0e-222">단수 테이블 이름을 지정하려면 다음 강조 표시된 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-222">To specify singular table names, add the following highlighted code:</span></span>

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="90e0e-223">종속성 주입으로 컨텍스트 등록</span><span class="sxs-lookup"><span data-stu-id="90e0e-223">Register the context with dependency injection</span></span>

<span data-ttu-id="90e0e-224">ASP.NET Core는 [종속성 주입](xref:fundamentals/dependency-injection)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-224">ASP.NET Core includes [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="90e0e-225">서비스(예: EF Core DB 컨텍스트)는 응용 프로그램 시작 중에 종속성 주입에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-225">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="90e0e-226">이러한 서비스(예: Razor 페이지)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-226">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="90e0e-227">DB 컨텍스트 인스턴스를 가져오는 생성자 코드는 자습서 뒷부분에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-227">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="90e0e-228">`SchoolContext`를 서비스로 등록하려면 *Startup.cs*를 열고 강조 표시된 줄을 `ConfigureServices` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-228">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="90e0e-229">`DbContextOptionsBuilder` 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-229">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="90e0e-230">로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-230">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="90e0e-231">`ContosoUniversity.Data` 및 `Microsoft.EntityFrameworkCore` 네임스페이스에 대한 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-231">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces.</span></span> <span data-ttu-id="90e0e-232">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-232">Build the project.</span></span>

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="90e0e-233">*appsettings.json* 파일을 열고 다음 코드에 표시된 대로 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-233">Open the *appsettings.json* file and add a connection string as shown in the following code:</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

<span data-ttu-id="90e0e-234">위의 연결 문자열은 `ConnectRetryCount=0`을 사용하여 [SQLClient](/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework)가 중단되는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-234">The preceding connection string uses `ConnectRetryCount=0` to prevent [SQLClient](/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) from hanging.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="90e0e-235">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="90e0e-235">SQL Server Express LocalDB</span></span>

<span data-ttu-id="90e0e-236">연결 문자열은 SQL Server LocalDB DB를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-236">The connection string specifies a SQL Server LocalDB DB.</span></span> <span data-ttu-id="90e0e-237">LocalDB는 프로덕션 사용이 아닌 앱 개발용으로 고안된 SQL Server Express 데이터베이스 엔진의 경량 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-237">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="90e0e-238">LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-238">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="90e0e-239">기본적으로 LocalDB는 *.mdf* DB 파일을 `C:/Users/<user>` 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-239">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="90e0e-240">코드를 추가하여 테스트 데이터로 DB 초기화</span><span class="sxs-lookup"><span data-stu-id="90e0e-240">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="90e0e-241">EF Core가 빈 DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-241">EF Core creates an empty DB.</span></span> <span data-ttu-id="90e0e-242">이 섹션에서는 테스트 데이터로 채울 *Seed* 메서드가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-242">In this section, a *Seed* method is written to populate it with test data.</span></span>

<span data-ttu-id="90e0e-243">*Data* 폴더에서 *DbInitializer.cs*라는 새 클래스 파일을 만들고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-243">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="90e0e-244">코드는 DB에 학생이 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-244">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="90e0e-245">DB에 학생이 없는 경우 DB는 테스트 데이터로 시드됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-245">If there are no students in the DB, the DB is seeded with test data.</span></span> <span data-ttu-id="90e0e-246">`List<T>` 컬렉션이 아닌 배열에 테스트 데이터를 로드하여 성능을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-246">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="90e0e-247">`EnsureCreated` 메서드는 자동으로 DB 컨텍스트에 대한 DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-247">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="90e0e-248">DB가 있는 경우 `EnsureCreated`는 DB를 수정하지 않고 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-248">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="90e0e-249">*Program.cs*에서 다음을 수행하는 `Main` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-249">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="90e0e-250">종속성 주입 컨테이너에서 DB 컨텍스트 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-250">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="90e0e-251">컨텍스트를 전달하는 시드 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-251">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="90e0e-252">시드 메서드가 완료되면 컨텍스트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-252">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="90e0e-253">다음 코드는 업데이트된 *Program.cs* 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-253">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

<span data-ttu-id="90e0e-254">처음으로 앱이 실행되고 DB가 생성되며 테스트 데이터로 시드됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-254">The first time the app is run, the DB is created and seeded with test data.</span></span> <span data-ttu-id="90e0e-255">데이터 모델이 업데이트되면:</span><span class="sxs-lookup"><span data-stu-id="90e0e-255">When the data model is updated:</span></span>
* <span data-ttu-id="90e0e-256">DB를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-256">Delete the DB.</span></span>
* <span data-ttu-id="90e0e-257">시드 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-257">Update the seed method.</span></span>
* <span data-ttu-id="90e0e-258">앱을 실행하면 새 시드된 DB가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-258">Run the app and a new seeded DB is created.</span></span> 

<span data-ttu-id="90e0e-259">이후의 자습서에서는 데이터 모델이 변경될 때 DB를 삭제하고 다시 작성하지 않고 DB가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-259">In later tutorials, the DB is updated when the data model changes, without deleting and re-creating the DB.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a><span data-ttu-id="90e0e-260">스캐폴드 도구 추가</span><span class="sxs-lookup"><span data-stu-id="90e0e-260">Add scaffold tooling</span></span>

<span data-ttu-id="90e0e-261">이 섹션에서는 Visual Studio 웹 코드 생성 패키지를 추가하는 데 PMC(패키지 관리자 콘솔)가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-261">In this section, the Package Manager Console (PMC) is used to add the Visual Studio web code generation package.</span></span> <span data-ttu-id="90e0e-262">스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-262">This package is required to run the scaffolding engine.</span></span>

<span data-ttu-id="90e0e-263">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-263">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="90e0e-264">PMC(패키지 관리자 콘솔)에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-264">In the Package Manager Console (PMC), enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

<span data-ttu-id="90e0e-265">위 명령은 \*.csproj 파일에 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-265">The previous command adds the NuGet packages to the \*.csproj file:</span></span>

[!code-xml[](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a><span data-ttu-id="90e0e-266">모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="90e0e-266">Scaffold the model</span></span>

* <span data-ttu-id="90e0e-267">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-267">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="90e0e-268">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-268">Run the following commands:</span></span>


 ```console
dotnet restore
dotnet tool install --global dotnet-aspnet-codegenerator --version 2.1.0
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```

<span data-ttu-id="90e0e-269">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="90e0e-269">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="90e0e-270">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-270">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>


<span data-ttu-id="90e0e-271">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-271">Build the project.</span></span> <span data-ttu-id="90e0e-272">빌드는 다음과 같은 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-272">The build generates errors like the following:</span></span>

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 <span data-ttu-id="90e0e-273">전체적으로 `_context.Student`를 `_context.Students`로 변경합니다(즉, “s”를 `Student`에 추가).</span><span class="sxs-lookup"><span data-stu-id="90e0e-273">Globally change `_context.Student` to `_context.Students` (that is, add an "s" to `Student`).</span></span> <span data-ttu-id="90e0e-274">7개 항목이 발견되어 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-274">7 occurrences are found and updated.</span></span> <span data-ttu-id="90e0e-275">다음 릴리스에서 [이 버그](https://github.com/aspnet/Scaffolding/issues/633)를 해결하기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-275">We hope to fix [this bug](https://github.com/aspnet/Scaffolding/issues/633) in the next release.</span></span>

[!INCLUDE [model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="90e0e-276">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="90e0e-276">Test the app</span></span>

<span data-ttu-id="90e0e-277">앱을 실행하고 **학생** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-277">Run the app and select the **Students** link.</span></span> <span data-ttu-id="90e0e-278">브라우저 너비에 따라 **학생** 링크가 페이지의 맨 위에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-278">Depending on the browser width, the **Students** link appears at the top of the page.</span></span> <span data-ttu-id="90e0e-279">**학생** 링크가 표시되지 않으면 오른쪽 위 모서리에 있는 탐색 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-279">If the **Students** link isn't visible, click the navigation icon in the upper right corner.</span></span>

![좁은 Contoso University 홈페이지](intro/_static/home-page-narrow.png)

<span data-ttu-id="90e0e-281">**만들기**, **편집** 및 **세부 정보** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-281">Test the **Create**, **Edit**, and **Details** links.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="90e0e-282">DB 보기</span><span class="sxs-lookup"><span data-stu-id="90e0e-282">View the DB</span></span>

<span data-ttu-id="90e0e-283">앱이 시작되면 `DbInitializer.Initialize`는 `EnsureCreated`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-283">When the app is started, `DbInitializer.Initialize` calls `EnsureCreated`.</span></span> <span data-ttu-id="90e0e-284">`EnsureCreated`는 DB가 존재하는지 감지하고 필요한 경우 DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-284">`EnsureCreated` detects if the DB exists, and creates one if necessary.</span></span> <span data-ttu-id="90e0e-285">DB에 학생이 없는 경우 `Initialize` 메서드는 학생을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-285">If there are no Students in the DB, the `Initialize` method adds students.</span></span>

<span data-ttu-id="90e0e-286">Visual Studio의 **보기** 메뉴에서 **SSOX(SQL Server 개체 탐색기)** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-286">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="90e0e-287">SSOX에서 **(localdb)\MSSQLLocalDB > 데이터베이스 > ContosoUniversity1**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-287">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="90e0e-288">**테이블** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-288">Expand the **Tables** node.</span></span>

<span data-ttu-id="90e0e-289">**학생** 테이블을 마우스 오른쪽 단추로 클릭하고, **데이터 보기**를 클릭하여 만든 열 및 테이블에 삽입된 행을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-289">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

<span data-ttu-id="90e0e-290"><em>.mdf</em> 및 <em>.ldf</em> DB 파일은 <em>C:\Users\\<yourusername></em> 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-290">The <em>.mdf</em> and <em>.ldf</em> DB files are in the <em>C:\Users\\<yourusername></em> folder.</span></span>

<span data-ttu-id="90e0e-291">앱 시작 시 다음 작업 흐름을 허용하는 `EnsureCreated`가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-291">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="90e0e-292">DB를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-292">Delete the DB.</span></span>
* <span data-ttu-id="90e0e-293">DB 스키마를 변경합니다(예: `EmailAddress` 필드 추가).</span><span class="sxs-lookup"><span data-stu-id="90e0e-293">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="90e0e-294">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-294">Run the app.</span></span>

<span data-ttu-id="90e0e-295">`EnsureCreated`가 `EmailAddress` 열이 있는 DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-295">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="90e0e-296">규칙</span><span class="sxs-lookup"><span data-stu-id="90e0e-296">Conventions</span></span>

<span data-ttu-id="90e0e-297">EF Core에서 수행하는 규칙 또는 가정의 사용으로 인해 EF Core에서 완벽한 DB를 만들기 위해 작성한 규칙의 양은 최소여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-297">The amount of code written in order for EF Core to create a complete DB is minimal because of the use of conventions, or assumptions that EF Core makes.</span></span>

* <span data-ttu-id="90e0e-298">`DbSet` 속성의 이름은 테이블 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-298">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="90e0e-299">`DbSet` 속성에서 참조하지 않는 엔터티의 경우 엔터티 클래스 이름이 테이블 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-299">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="90e0e-300">엔터티 속성 이름은 열 이름에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-300">Entity property names are used for column names.</span></span>

* <span data-ttu-id="90e0e-301">ID 또는 classnameID로 명명된 엔터티 속성은 기본 키 속성으로 인식됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-301">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="90e0e-302">속성 이름이 *<navigation property name><primary key property name>* 인 경우 외래 키 속성으로는 해석됩니다(예를 들어 `Student` 엔터티의 기본 키가 `ID`이므로 `Student` 탐색 속성의 경우 `StudentID`).</span><span class="sxs-lookup"><span data-stu-id="90e0e-302">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="90e0e-303">외래 키 속성의 이름을 *<primary key property name>* 으로 지정할 수 있습니다(예를 들어 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`이므로 `EnrollmentID`).</span><span class="sxs-lookup"><span data-stu-id="90e0e-303">Foreign key properties can be named *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="90e0e-304">기본 동작은 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-304">Conventional behavior can be overridden.</span></span> <span data-ttu-id="90e0e-305">예를 들어 이 자습서의 앞부분에 나온 것처럼 테이블 이름을 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-305">For example, the table names can be explicitly specified, as shown earlier in this tutorial.</span></span> <span data-ttu-id="90e0e-306">열 이름을 명시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-306">The column names can be explicitly set.</span></span> <span data-ttu-id="90e0e-307">기본 키와 외래 키를 명시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-307">Primary keys and foreign keys can be explicitly set.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="90e0e-308">비동기 코드</span><span class="sxs-lookup"><span data-stu-id="90e0e-308">Asynchronous code</span></span>

<span data-ttu-id="90e0e-309">비동기 프로그래밍은 ASP.NET Core 및 EF Core에 대한 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-309">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="90e0e-310">웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-310">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="90e0e-311">이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-311">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="90e0e-312">동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-312">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="90e0e-313">비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-313">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="90e0e-314">따라서 비동기 코드를 사용하면 서버 리소스를 더 효율적으로 사용할 수 있으며 서버가 지연 없이 더 많은 트래픽을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-314">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="90e0e-315">비동기 코드는 런타임 시 약간의 오버헤드를 도입합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-315">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="90e0e-316">트래픽이 높은 상황에서는 잠재적 성능 향상이 상당한 반면, 트래픽이 낮은 상황의 경우 성능 저하는 미미합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-316">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="90e0e-317">다음 코드에서 `async` 키워드, `Task<T>` 반환 값, `await` 키워드 및 `ToListAsync` 메서드는 비동기적으로 코드 실행을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-317">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="90e0e-318">`async` 키워드는 컴파일러가 다음을 수행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-318">The `async` keyword tells the compiler to:</span></span>

  * <span data-ttu-id="90e0e-319">메서드 본문의 부분에 대한 콜백을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-319">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="90e0e-320">반환되는 [작업](/dotnet/api/system.threading.tasks.task?view=netframework-4.7) 개체를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-320">Automatically create the [Task](/dotnet/api/system.threading.tasks.task?view=netframework-4.7) object that's returned.</span></span> <span data-ttu-id="90e0e-321">자세한 내용은 [작업 반환 형식](/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90e0e-321">For more information, see [Task Return Type](/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="90e0e-322">암시적 반환 형식 `Task`는 진행 중인 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-322">The implicit return type `Task` represents ongoing work.</span></span>

* <span data-ttu-id="90e0e-323">`await` 키워드로 인해 컴파일러는 메서드를 두 부분으로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-323">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="90e0e-324">첫 번째 부분은 비동기적으로 시작되는 작업을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-324">The first part ends with the operation that's started asynchronously.</span></span> <span data-ttu-id="90e0e-325">두 번째 부분은 작업이 완료될 때 호출되는 콜백 메서드에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-325">The second part is put into a callback method that's called when the operation completes.</span></span>

* <span data-ttu-id="90e0e-326">`ToListAsync`는 `ToList` 확장 메서드의 비동기 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-326">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="90e0e-327">EF Core를 사용하는 비동기 코드를 작성할 때 고려해야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-327">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="90e0e-328">쿼리 또는 명령을 DB에 보내는 명령문만 비동기적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-328">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="90e0e-329">여기에는 `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync` 및 `SaveChangesAsync`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-329">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="90e0e-330">`var students = context.Students.Where(s => s.LastName == "Davolio")`와 같은 `IQueryable`을 변경하는 명령문은 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-330">It doesn't include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="90e0e-331">EF Core 컨텍스트는 스레드로부터 안전하지 않습니다. 동시에 여러 작업을 수행하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="90e0e-331">An EF Core context isn't thread safe: don't try to do multiple operations in parallel.</span></span> 

* <span data-ttu-id="90e0e-332">비동기 코드의 성능 이점을 활용하려면 쿼리를 DB에 보내는 EF Core 메서드를 호출하는 경우 라이브러리 패키지(예: 페이징)가 비동기를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-332">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="90e0e-333">.NET에서의 비동기 프로그래밍에 대한 자세한 내용은 [비동기 개요](/dotnet/articles/standard/async)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90e0e-333">For more information about asynchronous programming in .NET, see [Async Overview](/dotnet/articles/standard/async).</span></span>

<span data-ttu-id="90e0e-334">다음 자습서에서는 기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="90e0e-334">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="90e0e-335">다음</span><span class="sxs-lookup"><span data-stu-id="90e0e-335">Next</span></span>](xref:data/ef-rp/crud)
