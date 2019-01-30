---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기를 사용자 지정'
description: 이 자습서는 프레젠테이션을 개선할에 자동으로 생성 된 보기를 변경에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: c47d7c131eebbcd8811e31edda210d64cf4b9d6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55236499"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="0ac1e-103">자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0ac1e-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="0ac1e-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="0ac1e-105">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="0ac1e-106">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="0ac1e-107">이 자습서는 프레젠테이션을 개선할에 자동으로 생성 된 보기를 변경에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="0ac1e-108">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ac1e-109">학생 세부 정보 페이지에 강좌 추가</span><span class="sxs-lookup"><span data-stu-id="0ac1e-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="0ac1e-110">강좌 페이지에 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ac1e-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="0ac1e-111">Prerequisites</span></span>

* [<span data-ttu-id="0ac1e-112">데이터베이스 변경</span><span class="sxs-lookup"><span data-stu-id="0ac1e-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="0ac1e-113">과정 학생 정보 추가</span><span class="sxs-lookup"><span data-stu-id="0ac1e-113">Add courses to student detail</span></span>

<span data-ttu-id="0ac1e-114">생성된 된 코드는 응용 프로그램에 대 한 좋은 시작점을 제공 하지만 필요 하지 않습니다 모든 응용 프로그램에 필요한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="0ac1e-115">응용 프로그램의 특정 요구 사항에 맞게 코드를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="0ac1e-116">현재 응용 프로그램 선택한 학생에 대 한 등록된 과정을 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="0ac1e-117">이 섹션에서는 추가 등록된 과정을 각 학생에 대 한 합니다 **세부 정보** 학생에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="0ac1e-118">오픈 **뷰** > **학생** > *Details.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="0ac1e-119">마지막으로 아래 &lt;/dl&gt; 태그를 닫기 전에 &lt;/div&gt; 태그에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="0ac1e-120">이 코드에서는 선택한 학생에 대해 Enrollment 테이블의 각 레코드에 대 한 행을 표시 하는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="0ac1e-121">합니다 **표시** 메서드는 expression을 나타내는 개체 (modelItem)에 대 한 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="0ac1e-122">표시 메서드를 사용 하면 단순히 코드에서 속성 값을 포함) (대신 값의 해당 형식 및 해당 형식에 대 한 서식 파일에 따라 올바르게 서식이 지정 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="0ac1e-123">이 예제에서는 각 식 루프의 현재 레코드에서 단일 속성을 반환 하 고 값 형식은 기본 텍스트로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="0ac1e-124">강좌가 추가 확인</span><span class="sxs-lookup"><span data-stu-id="0ac1e-124">Confirm courses are added</span></span>

<span data-ttu-id="0ac1e-125">솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-125">Run the solution.</span></span> <span data-ttu-id="0ac1e-126">클릭 **학생의 목록을** 선택한 **세부 정보** 학습자 중 하나에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="0ac1e-127">보기에 포함 된 등록된 과정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-127">You will see the enrolled courses have been included in the view.</span></span>

![학생 등록](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="0ac1e-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ac1e-129">Next steps</span></span>
<span data-ttu-id="0ac1e-130">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ac1e-131">학생 세부 정보 페이지로 추가 과정</span><span class="sxs-lookup"><span data-stu-id="0ac1e-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="0ac1e-132">강좌 페이지에 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="0ac1e-133">데이터 주석 유효성 검사 요구 사항을 지정 및 서식을 추가 하는 방법을 알아보려면 다음 자습서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac1e-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0ac1e-134">데이터 유효성 검사 향상</span><span class="sxs-lookup"><span data-stu-id="0ac1e-134">Enhance data validation</span></span>](enhancing-data-validation.md)
