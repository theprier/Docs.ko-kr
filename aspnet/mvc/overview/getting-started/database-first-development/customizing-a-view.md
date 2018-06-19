---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 보기를 사용자 지정 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 8338603e032329ad03d47c6392e508aa07c6858e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30867660"
---
<a name="ef-database-first-with-aspnet-mvc-customizing-a-view"></a><span data-ttu-id="e4881-104">ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 보기를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e4881-104">EF Database First with ASP.NET MVC: Customizing a View</span></span>
====================
<span data-ttu-id="e4881-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e4881-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e4881-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="e4881-107">이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="e4881-108">생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="e4881-109">시리즈의이 부분 프레젠테이션을 강화 하기 위해 자동으로 생성 된 뷰를 변경 하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-109">This part of the series focuses on changing the automatically-generated views to enhance the presentation.</span></span>


## <a name="add-enrolled-courses-to-student-details"></a><span data-ttu-id="e4881-110">등록된 과정을 학생 세부 정보를 추가</span><span class="sxs-lookup"><span data-stu-id="e4881-110">Add enrolled courses to student details</span></span>

<span data-ttu-id="e4881-111">생성 된 코드 응용 프로그램을 위한 좋은 출발점을 제공 하지만 반드시을 제공 하지 않습니다는 응용 프로그램에 필요한 기능을 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-111">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="e4881-112">응용 프로그램의 특정 요구 사항에 맞게 코드를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-112">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="e4881-113">현재 응용 프로그램 선택한 학생에 대 한 등록된 과정을 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-113">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="e4881-114">이 섹션에서는 각 학생에에 대 한 등록된 과정을 추가 합니다는 **세부 정보** 학생에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-114">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="e4881-115">열기 **Students/Details.cshtml**, 마지막 아래 &lt;/dl&gt; 탭 닫기 전에 &lt;/div&gt; 태그에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-115">Open **Students/Details.cshtml**, and below the last &lt;/dl&gt; tab, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="e4881-116">이 코드는 선택한 학생에 대 한 등록 테이블의 각 레코드에 대 한 행을 표시 하는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-116">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="e4881-117">**디스플레이** 메서드는 expression을 나타내는 개체 (modelItem)에 대 한 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-117">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="e4881-118">Display 메서드를 사용 하 여 코드에서 속성 값을 간단히 삽입) 하는 것 (대신 값의 형식과 해당 형식에 대 한 서식 파일에 따라 올바르게 형식이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-118">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="e4881-119">이 예에서 각 식은 루프의 현재 레코드에서 단일 속성을 반환 하 고 값이 텍스트로 렌더링 되는 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-119">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

<span data-ttu-id="e4881-120">학생/인덱스 보기로 다시 이동 하 고 선택 **세부 정보** 학습자 중 하나에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-120">Browse to the Students/Index view again and select **Details** for one of the students.</span></span> <span data-ttu-id="e4881-121">등록 된 courses 들이 보기에 포함 되어 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4881-121">You will see the enrolled courses have been included in the view.</span></span>

![학생으로 등록](customizing-a-view/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="e4881-123">[이전](changing-the-database.md)
> [다음](enhancing-data-validation.md)</span><span class="sxs-lookup"><span data-stu-id="e4881-123">[Previous](changing-the-database.md)
[Next](enhancing-data-validation.md)</span></span>
