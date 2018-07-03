---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'ASP.NET MVC를 사용 하 여 먼저 EF Database: 보기 사용자 지정 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: bfbcfd39dd1cf0abe89a00d2958ca010f0e5e109
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376500"
---
<a name="ef-database-first-with-aspnet-mvc-customizing-a-view"></a><span data-ttu-id="67fe3-104">ASP.NET MVC를 사용 하 여 먼저 EF Database: 보기 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="67fe3-104">EF Database First with ASP.NET MVC: Customizing a View</span></span>
====================
<span data-ttu-id="67fe3-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="67fe3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="67fe3-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="67fe3-107">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="67fe3-108">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="67fe3-109">시리즈의이 부분 프레젠테이션을 개선할에 자동으로 생성 된 보기를 변경에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-109">This part of the series focuses on changing the automatically-generated views to enhance the presentation.</span></span>


## <a name="add-enrolled-courses-to-student-details"></a><span data-ttu-id="67fe3-110">등록 된 과정 학생 세부 정보 추가</span><span class="sxs-lookup"><span data-stu-id="67fe3-110">Add enrolled courses to student details</span></span>

<span data-ttu-id="67fe3-111">생성된 된 코드는 응용 프로그램에 대 한 좋은 시작점을 제공 하지만 필요 하지 않습니다 모든 응용 프로그램에 필요한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-111">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="67fe3-112">응용 프로그램의 특정 요구 사항에 맞게 코드를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-112">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="67fe3-113">현재 응용 프로그램 선택한 학생에 대 한 등록된 과정을 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-113">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="67fe3-114">이 섹션에서는 추가 등록된 과정을 각 학생에 대 한 합니다 **세부 정보** 학생에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-114">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="67fe3-115">열기 **Students/Details.cshtml**, 및 마지막 아래 &lt;/dl&gt; 탭, 닫히기 전까지 &lt;/div&gt; 태그에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-115">Open **Students/Details.cshtml**, and below the last &lt;/dl&gt; tab, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="67fe3-116">이 코드에서는 선택한 학생에 대해 Enrollment 테이블의 각 레코드에 대 한 행을 표시 하는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-116">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="67fe3-117">합니다 **표시** 메서드는 expression을 나타내는 개체 (modelItem)에 대 한 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-117">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="67fe3-118">표시 메서드를 사용 하면 단순히 코드에서 속성 값을 포함) (대신 값의 해당 형식 및 해당 형식에 대 한 서식 파일에 따라 올바르게 서식이 지정 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-118">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="67fe3-119">이 예제에서는 각 식 루프의 현재 레코드에서 단일 속성을 반환 하 고 값 형식은 기본 텍스트로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-119">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

<span data-ttu-id="67fe3-120">학생/인덱스 보기로 다시 이동 및 선택 **세부 정보** 학습자 중 하나에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-120">Browse to the Students/Index view again and select **Details** for one of the students.</span></span> <span data-ttu-id="67fe3-121">보기에 포함 된 등록된 과정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67fe3-121">You will see the enrolled courses have been included in the view.</span></span>

![학생 등록](customizing-a-view/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="67fe3-123">[이전](changing-the-database.md)
> [다음](enhancing-data-validation.md)</span><span class="sxs-lookup"><span data-stu-id="67fe3-123">[Previous](changing-the-database.md)
[Next](enhancing-data-validation.md)</span></span>
