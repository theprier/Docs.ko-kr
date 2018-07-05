---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: ASP.NET 웹 페이지 소개-데이터를 표시 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 WebMatrix에서 데이터베이스를 만드는 방법 및 ASP.NET Web Pages (Razor)를 사용 하는 경우 페이지에서 데이터베이스 데이터를 표시 하는 방법입니다. Y 가정 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: de4ed9df2c65a1aaa4548b035c619cfa9bae7a8e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384971"
---
<a name="introducing-aspnet-web-pages---displaying-data"></a><span data-ttu-id="07e7a-104">ASP.NET 웹 페이지 소개-데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-104">Introducing ASP.NET Web Pages - Displaying Data</span></span>
====================
<span data-ttu-id="07e7a-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="07e7a-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="07e7a-106">이 자습서에서는 WebMatrix에서 데이터베이스를 만드는 방법 및 ASP.NET Web Pages (Razor)를 사용 하는 경우 페이지에서 데이터베이스 데이터를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-106">This tutorial shows you how to create a database in WebMatrix and how to display database data in a page when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="07e7a-107">통해 시리즈를 완료 했다고 가정 하 [ASP.NET 웹 페이지 프로그래밍 소개](../introducing-razor-syntax-c.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-107">It assumes you have completed the series through [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md).</span></span>
> 
> <span data-ttu-id="07e7a-108">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="07e7a-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="07e7a-109">WebMatrix 도구를 사용 하 여 데이터베이스와 데이터베이스 테이블을 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-109">How to use WebMatrix tools to create a database and database tables.</span></span>
> - <span data-ttu-id="07e7a-110">WebMatrix 도구를 사용 하 여 데이터베이스에 데이터를 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="07e7a-110">How to use WebMatrix tools to add data to a database.</span></span>
> - <span data-ttu-id="07e7a-111">데이터베이스에서 데이터 페이지를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-111">How to display data from the database on a page.</span></span>
> - <span data-ttu-id="07e7a-112">ASP.NET 웹 페이지에서 SQL 명령을 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-112">How to run SQL commands in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="07e7a-113">사용자 지정 하는 방법의 `WebGrid` 도우미 데이터 표시를 변경 하 고 페이징 및 정렬를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-113">How to customize the `WebGrid` helper to change the data display and to add paging and sorting.</span></span>
>   
> 
> <span data-ttu-id="07e7a-114">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="07e7a-115">WebMatrix는 데이터베이스 도구.</span><span class="sxs-lookup"><span data-stu-id="07e7a-115">WebMatrix database tools.</span></span>
> - <span data-ttu-id="07e7a-116">`WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-116">`WebGrid` helper.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="07e7a-117">만들 내용</span><span class="sxs-lookup"><span data-stu-id="07e7a-117">What You'll Build</span></span>

<span data-ttu-id="07e7a-118">이전 자습서에서는 ASP.NET Web Pages를 소개 했습니다 (*.cshtml* 파일), Razor 구문의 기본 사항 및 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-118">In the previous tutorial, you were introduced to ASP.NET Web Pages (*.cshtml* files), to the basics of Razor syntax, and to helpers.</span></span> <span data-ttu-id="07e7a-119">이 자습서에서는 시리즈의 나머지 부분에 사용 하는 실제 웹 응용 프로그램을 만들기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-119">In this tutorial, you'll begin creating the actual web application that you'll use for the rest of the series.</span></span> <span data-ttu-id="07e7a-120">앱을 보고, 추가, 변경 및 영화에 대 한 정보를 삭제할 수 있는 간단한 영화 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="07e7a-120">The app is a simple movie application that lets you view, add, change, and delete information about movies.</span></span>

<span data-ttu-id="07e7a-121">이 자습서를 완료 하는 경우에이 페이지 처럼 보이는 동영상 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-121">When you're done with this tutorial, you'll be able to view a movie listing that looks like this page:</span></span>

![CSS 클래스 이름으로 설정 하는 매개 변수가 포함 된 WebGrid 표시](displaying-data/_static/image1.png)

<span data-ttu-id="07e7a-123">하지만 데이터베이스 만들기를 시작 하려면 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-123">But to begin, you have to create a database.</span></span>

## <a name="a-very-brief-introduction-to-databases"></a><span data-ttu-id="07e7a-124">데이터베이스에 대 한 매우 간단한 소개</span><span class="sxs-lookup"><span data-stu-id="07e7a-124">A Very Brief Introduction to Databases</span></span>

<span data-ttu-id="07e7a-125">이 자습서에서는 데이터베이스에 대 한 명령을 소개만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-125">This tutorial will provide only the briefest introduction to databases.</span></span> <span data-ttu-id="07e7a-126">데이터베이스 환경에 있는 경우에이 짧은 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-126">If you have database experience, you can skip this short section.</span></span>

<span data-ttu-id="07e7a-127">데이터베이스 정보를 포함 하는 하나 이상의 테이블에 &mdash; 예를 들어, 고객, 주문 및 공급 업체 또는 학생, 교사, 클래스 및 등급에 대 한 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-127">A database contains one or more tables that contain information &mdash; for example, tables for customers, orders, and vendors, or for students, teachers, classes, and grades.</span></span> <span data-ttu-id="07e7a-128">구조적으로 데이터베이스 테이블을 스프레드시트 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-128">Structurally, a database table is like a spreadsheet.</span></span> <span data-ttu-id="07e7a-129">일반적인 주소록을 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-129">Imagine a typical address book.</span></span> <span data-ttu-id="07e7a-130">주소록의 각 항목에 대 한 (즉, 각 사용자에 대 한) 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 일부 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-130">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

![샘플 데이터베이스 테이블에 간단한 모눈으로](displaying-data/_static/image2.png)

<span data-ttu-id="07e7a-132">(행은 라고도 *레코드*, 및 열은 라고도 *필드*.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-132">(Rows are sometimes referred to as *records*, and columns are sometimes referred to as *fields*.)</span></span>

<span data-ttu-id="07e7a-133">대부분의 데이터베이스 테이블에 대 한 테이블에 고객 번호, 계좌 번호 등과 같은 고유한 값을 포함 하는 열을 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-133">For most database tables, the table has to have a column that contains a unique value, like a customer number, account number, and so on.</span></span> <span data-ttu-id="07e7a-134">이 값은 테이블의 이라고 *기본 키*을 및 테이블의 각 행을 식별 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-134">This value is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="07e7a-135">예제에서는 ID 열은 이전 예에서 같이 주소록에 대 한 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-135">In the example, the ID column is the primary key for the address book shown in the previous example.</span></span>

<span data-ttu-id="07e7a-136">웹 응용 프로그램에서 수행 하는 작업의 대부분 구성 데이터베이스에서 정보를 읽고 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-136">Much of the work you do in web applications consists of reading information out of the database and displaying it on a page.</span></span> <span data-ttu-id="07e7a-137">에서는 종종 사용자 로부터 정보를 수집 하 고 데이터베이스에 추가 하거나 이미 데이터베이스에 있는 레코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-137">You'll also often gather information from users and add it to a database, or you'll modify records that are already in the database.</span></span> <span data-ttu-id="07e7a-138">(다루게이 자습서 집합 과정에서 이러한 작업의 모든.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-138">(We'll cover all of these operations in the course of this tutorial set.)</span></span>

<span data-ttu-id="07e7a-139">데이터베이스 작업 때 매우 복잡할 수 있으며 전문된 지식 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-139">Database work can be enormously complex and can require specialized knowledge.</span></span> <span data-ttu-id="07e7a-140">이 자습서 집합에 대 한 그러나만 기본 개념을 모두 설명 하면서 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-140">For this tutorial set, though, you have to understand only basic concepts, which will all be explained as you go.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="07e7a-141">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="07e7a-141">Creating a Database</span></span>

<span data-ttu-id="07e7a-142">WebMatrix에는 쉽게 데이터베이스를 만들고 데이터베이스에서 테이블을 만드는 도구가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-142">WebMatrix includes tools that make it easy to create a database and to create tables in the database.</span></span> <span data-ttu-id="07e7a-143">(데이터베이스의 구조는 데이터베이스의 이라고 *스키마*.) 이 자습서 집합에 대 한 하나의 테이블에 있는 데이터베이스를 만들어 &mdash; 동영상입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-143">(The structure of a database is referred to as the database's *schema*.) For this tutorial set, you'll create a database that has only one table in it &mdash; Movies.</span></span>

<span data-ttu-id="07e7a-144">따라서 아직 수행 하지 않은 경우 WebMatrix를 열고 이전 자습서에서 만든 WebPagesMovies 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-144">Open WebMatrix if you haven't already done so, and open the WebPagesMovies site that you created in the previous tutorial.</span></span>

<span data-ttu-id="07e7a-145">왼쪽된 창에서 클릭 합니다 **데이터베이스** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-145">In the left pane, click the **Database** workspace.</span></span>

![WebMatrix 데이터베이스 작업 영역 탭](displaying-data/_static/image3.png)

<span data-ttu-id="07e7a-147">데이터베이스 관련 작업을 표시 하는 리본 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-147">The ribbon changes to show database-related tasks.</span></span> <span data-ttu-id="07e7a-148">리본 메뉴에서 클릭 **새 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-148">In the ribbon, click **New Database**.</span></span>

!['새 데이터베이스' WebMatrix 리본 단추](displaying-data/_static/image4.png)

<span data-ttu-id="07e7a-150">WebMatrix는 SQL Server CE 데이터베이스를 만듭니다 (프로그램 *.sdf* 파일) 사이트와 동일한 이름을 가진 &mdash; *WebPagesMovies.sdf*합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-150">WebMatrix creates a SQL Server CE database (an *.sdf* file) that has the same name as your site &mdash; *WebPagesMovies.sdf*.</span></span> <span data-ttu-id="07e7a-151">(여기에서 이렇게지 않습니다 하지만 붙어 있다면는 파일을 원하는 값으로 바꿀 수 있습니다는 *.sdf* 확장 합니다.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-151">(You won't do this here, but you can rename the file to anything you like, as long as it has an *.sdf* extension.)</span></span>

## <a name="creating-a-table"></a><span data-ttu-id="07e7a-152">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="07e7a-152">Creating a Table</span></span>

<span data-ttu-id="07e7a-153">리본 메뉴에서 클릭 **새 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-153">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="07e7a-154">WebMatrix는 새 탭에서 테이블 디자이너를 엽니다. (새 테이블 옵션을 사용할 수 없으면 확인 왼쪽의 트리 보기에서 새 데이터베이스가 선택 되어 있는지.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-154">WebMatrix opens the table designer in a new tab. (If the New Table option isn't available, make sure that the new database is selected in the tree view on the left.)</span></span>

!['새 테이블' WebMatrix 리본 단추](displaying-data/_static/image5.png)

<span data-ttu-id="07e7a-156">(위치: "테이블 이름 입력" 이라는 워터 마크) 맨 위에 있는 텍스트 상자에 "Movies"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-156">In the text box at the top (where the watermark says "Enter table name"), enter "Movies".</span></span>

![WebMatrix 데이터베이스 디자이너에서 테이블 이름 입력](displaying-data/_static/image6.png)

<span data-ttu-id="07e7a-158">테이블 이름 아래에 있는 개별 열을 정의 하는 위치는입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-158">The pane underneath the table name is where you define individual columns.</span></span> <span data-ttu-id="07e7a-159">에 대 한 합니다 *영화* 테이블이 자습서에서는 몇 개의 열만을 만든: *ID*, *제목*, *장르*, 및 *연도*.</span><span class="sxs-lookup"><span data-stu-id="07e7a-159">For the *Movies* table in this tutorial, you'll create only a few columns: *ID*, *Title*, *Genre*, and *Year*.</span></span>

<span data-ttu-id="07e7a-160">에 **이름을** 상자에 "ID"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-160">In the **Name** box, enter "ID".</span></span> <span data-ttu-id="07e7a-161">새 열에 대 한 모든 컨트롤을 활성화 여기에 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-161">Entering a value here activates all the controls for the new column.</span></span>

<span data-ttu-id="07e7a-162">탭의 **데이터 형식** 나열 하 고 선택 **int**합니다. 이 값은 ID 열 (정수) 데이터에 포함 되어 있음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-162">Tab to the **Data Type** list and choose **int**. This value specifies that the ID column will contain integer (number) data.</span></span>

> [!NOTE]
> <span data-ttu-id="07e7a-163">않습니다 이라고 부르는 것 모두 자세히 (훨씬) 하지만 표준 Windows 바로 제스처를 사용 하 여이 표에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-163">We won't call it out any more here (much), but you can use standard Windows keyboard gestures to navigate in this grid.</span></span> <span data-ttu-id="07e7a-164">예를 들어, 필드 간의 탭 수만 목록에 항목을 선택 하려면 입력을 시작 하 고 등 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-164">For example, you can tab between fields, you can just start typing in order to select an item in a list, and so on.</span></span>


<span data-ttu-id="07e7a-165">이전 탭의 **기본값** 상자 (즉, 빈 상태로 둠).</span><span class="sxs-lookup"><span data-stu-id="07e7a-165">Tab past the **Default Value** box (that is, leave it blank).</span></span> <span data-ttu-id="07e7a-166">탭의 **기본 키가** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-166">Tab to the **Is Primary Key** check box and select it.</span></span> <span data-ttu-id="07e7a-167">이 옵션을 사용 하면 데이터베이스는 합니다 *ID* 개별 행을 식별 하는 데이터 열이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-167">This option tells the database that the *ID* column will contain the data that identifies individual rows.</span></span> <span data-ttu-id="07e7a-168">(즉, 각 행은 경우 고유한 값을 해당 행을 찾는 데 사용할 수 있는 ID 열의)</span><span class="sxs-lookup"><span data-stu-id="07e7a-168">(That is, each row will have a unique value in the ID column that you can use to find that row.)</span></span>

<span data-ttu-id="07e7a-169">선택 된 **Id** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-169">Choose the **Is Identity** option.</span></span> <span data-ttu-id="07e7a-170">이 옵션을 각 새 행에 대해 다음 일련 번호를 자동으로 생성 하도록이 데이터베이스를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-170">This option tells the database that it should automatically generate the next sequential number for each new row.</span></span> <span data-ttu-id="07e7a-171">(합니다 **Id** 옵션이 선택한 경우에 작동 합니다 **기본 키가** 옵션입니다.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-171">(The **Is Identity** option works only if you've also selected the **Is Primary Key** option.)</span></span>

<span data-ttu-id="07e7a-172">다음 표에서 행을 클릭 하거나 tab 키를 눌러 현재 행을 두 번입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-172">Click in the next grid row, or press Tab twice to finish the current row.</span></span> <span data-ttu-id="07e7a-173">제스처 중 하나는 현재 행을 저장 하 고 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-173">Either gesture saves the current row and starts the next one.</span></span> <span data-ttu-id="07e7a-174">에 **기본값** 열 이제 라는 **Null**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-174">Notice that the **Default Value** column now says **Null**.</span></span> <span data-ttu-id="07e7a-175">(Null 임 기본값에 대 한 기본값 말하자면)</span><span class="sxs-lookup"><span data-stu-id="07e7a-175">(Null is the default value for the default value, so to speak.)</span></span>

<span data-ttu-id="07e7a-176">새 정의 완료 했습니다 **ID** 열 디자이너가이 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-176">When you've finished defining the new **ID** column, the designer will look like this illustration:</span></span>

![영화 테이블의 ID 열을 정의 하 고 나면 WebMatrix 데이터베이스 디자이너](displaying-data/_static/image7.png)

<span data-ttu-id="07e7a-178">다음 열을 만들려면에서 상자를 클릭 합니다 **이름을** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-178">To create the next column, click in the box in the **Name** column.</span></span> <span data-ttu-id="07e7a-179">열에 대 한 "Title"를 입력 하 고 선택한 **nvarchar** 에 대 한 합니다 **데이터 형식** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-179">Enter "Title" for the column and then select **nvarchar** for the **Data Type** value.</span></span> <span data-ttu-id="07e7a-180">"Var" 부분 **nvarchar** 지시 데이터베이스는이 열에 대 한 데이터는 문자열일 크기가 레코드에서 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-180">The "var" part of **nvarchar** tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="07e7a-181">("N" 접두사를 나타내는 필드는 알파벳 이나 쓰기 시스템에 대 한 문자 데이터를 저장할 수 있는지를 나타내는 "national"-필드에서 유니코드 데이터를 보유 하는,.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-181">(The "n" prefix represents "national," which indicates that the field can hold character data for any alphabet or writing system — that is, the field holds Unicode data.)</span></span>

<span data-ttu-id="07e7a-182">선택 하는 경우 **nvarchar**, 필드에 대 한 최대 길이 입력할 수 있는 다른 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-182">When you choose **nvarchar**, another box appears where you can enter the maximum length for the field.</span></span> <span data-ttu-id="07e7a-183">이 자습서에서 작업할 수 있는 영화 제목 없음 50 자 보다 긴 된다는 가정에 50을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-183">Enter 50, on the assumption that no movie title that you'll work with in this tutorial will be longer than 50 characters.</span></span>

<span data-ttu-id="07e7a-184">Skip **기본값** 선택을 취소 합니다 **Null 허용** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-184">Skip **Default Value** and clear the **Allow Nulls** option.</span></span> <span data-ttu-id="07e7a-185">제목 없는 모든 영화 데이터베이스에 입력을 허용 하도록 데이터베이스 하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-185">You don't want the database to allow any movies to be entered into the database that don't have a title.</span></span>

<span data-ttu-id="07e7a-186">완료 하 고 다음 행으로 이동 하는 경우 디자이너는이 그림은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-186">When you're done and move to the next row, the designer looks like this illustration:</span></span>

![동영상 테이블에 대 한 제목 열을 정의 하 고 나면 WebMatrix 데이터베이스 디자이너](displaying-data/_static/image8.png)

<span data-ttu-id="07e7a-188">반복 길이 제외 하 고 "장르" 라는 열을 만들려면 다음이 단계를 바로 30으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-188">Repeat these steps to create a column named "Genre", except for the length, set it to just 30.</span></span>

<span data-ttu-id="07e7a-189">"Year." 라는 다른 열 만들기</span><span class="sxs-lookup"><span data-stu-id="07e7a-189">Create another column named "Year."</span></span> <span data-ttu-id="07e7a-190">데이터 형식에 대 한 선택 **nchar** (없습니다 **nvarchar**) 길이 4로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-190">For the data type, choose **nchar** (not **nvarchar**) and set the length to 4.</span></span> <span data-ttu-id="07e7a-191">Year, 하려는 "1995" 또는 "2010"와 같은 4 자리 숫자를 사용 하 여 가변 열을 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-191">For the year, you're going to use a 4-digit number like "1995" or "2010", so you don't require a variable-sized column.</span></span>

<span data-ttu-id="07e7a-192">완료 된 디자인의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-192">Here's what the finished design looks like:</span></span>

![동영상 테이블에 대 한 모든 필드를 정의한 후 WebMatrix 데이터베이스 디자이너](displaying-data/_static/image9.png)

<span data-ttu-id="07e7a-194">Ctrl + S를 누르거나 클릭 합니다 **저장할** 빠른 실행 도구 모음 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-194">Press Ctrl+S or click the **Save** button in the Quick Access toolbar.</span></span> <span data-ttu-id="07e7a-195">탭 닫기 데이터베이스 디자이너를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-195">Close the database designer by closing the tab.</span></span>

## <a name="adding-some-example-data"></a><span data-ttu-id="07e7a-196">일부 예제 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-196">Adding Some Example Data</span></span>

<span data-ttu-id="07e7a-197">이 자습서 시리즈의 뒷부분에 나오는 형태로 새 영화를 입력할 수 있는 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-197">Later in this tutorial series you'll create a page where you can enter new movies in a form.</span></span> <span data-ttu-id="07e7a-198">그러나 이제 그런 다음 페이지에 표시할 수 있는 몇 가지 예제 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-198">For now, however, you can add some example data that you can then display on a page.</span></span>

<span data-ttu-id="07e7a-199">에 **데이터베이스** 보여주는 트리는 WebMatrix에서 작업 영역을 *.sdf* 앞에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-199">In the **Database** workspace in WebMatrix, notice that there's a tree that shows you the *.sdf* file you created earlier.</span></span> <span data-ttu-id="07e7a-200">새 노드를 엽니다 *.sdf* 파일을 연 다음 합니다 **테이블** 노드.</span><span class="sxs-lookup"><span data-stu-id="07e7a-200">Open the node for your new *.sdf* file, and then open the **Tables** node.</span></span>

![열린 동영상 테이블 트리를 사용 하 여 WebMatrix 데이터베이스 작업 영역](displaying-data/_static/image10.png)

<span data-ttu-id="07e7a-202">마우스 오른쪽 단추로 클릭 합니다 **영화** 노드를 선택한 후 **데이터**입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-202">Right-click the **Movies** node and then choose **Data**.</span></span> <span data-ttu-id="07e7a-203">WebMatrix에 대 한 데이터를 입력할 수 있는 표 열립니다는 *영화* 테이블:</span><span class="sxs-lookup"><span data-stu-id="07e7a-203">WebMatrix opens a grid where you can enter data for the *Movies* table:</span></span>

![WebMatrix (비어 있음)에서 데이터베이스 항목 표](displaying-data/_static/image11.png)

<span data-ttu-id="07e7a-205">클릭 합니다 **Title** 열 "때 Harry 충족 Sally"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-205">Click the **Title** column and enter "When Harry Met Sally".</span></span> <span data-ttu-id="07e7a-206">이동 합니다 **장르** (Tab 키를 사용할 수 있음) 열 "로맨틱 코미디"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-206">Move to the **Genre** column (you can use the Tab key) and enter "Romantic Comedy".</span></span> <span data-ttu-id="07e7a-207">으로 이동 합니다 **연도** 열 "1989"을 입력:</span><span class="sxs-lookup"><span data-stu-id="07e7a-207">Move to the **Year** column and enter "1989":</span></span>

![레코드 하나를 사용 하 여 WebMatrix에서 데이터베이스 항목 표](displaying-data/_static/image12.png)

<span data-ttu-id="07e7a-209">Press Enter, 및 WebMatrix에 새 영화를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-209">Press Enter, and WebMatrix saves the new movie.</span></span> <span data-ttu-id="07e7a-210">다음에 유의 합니다 **ID** 열 채워진 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-210">Notice that the **ID** column has been filled in.</span></span>

![WebMatrix에서 하나의 레코드와 자동으로 생성 된 ID의 데이터베이스 항목 표](displaying-data/_static/image13.png)

<span data-ttu-id="07e7a-212">다른 동영상 (예를 들어, "완료와 the 바람", "드라마", "1939")을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-212">Enter another movie (for example, "Gone with the Wind", "Drama", "1939").</span></span> <span data-ttu-id="07e7a-213">ID 열에 다시 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-213">The ID column is filled in again:</span></span>

![두 레코드 및 자동 생성 된 Id를 사용 하 여 WebMatrix에서 데이터베이스 항목 표](displaying-data/_static/image14.png)

<span data-ttu-id="07e7a-215">세 번째 동영상 (예: "Ghostbusters", "코미디")을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-215">Enter a third movie (for example, "Ghostbusters", "Comedy").</span></span> <span data-ttu-id="07e7a-216">으로 그대로 둡니다.는 **연도** 열 빈 및 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-216">As an experiment, leave the **Year** column blank and then press Enter.</span></span> <span data-ttu-id="07e7a-217">선택 취소 하면 되므로 합니다 **Null 허용** 옵션을 데이터베이스에 오류가 표시:</span><span class="sxs-lookup"><span data-stu-id="07e7a-217">Because you unselected the **Allow Nulls** option, the database shows an error:</span></span>

![필요한 열 값은 비워 두면 '잘못 된 데이터' 오류가 표시](displaying-data/_static/image15.png)

<span data-ttu-id="07e7a-219">클릭 **확인** 돌아가서 및 ("Ghostbusters"에 대 한 연도가 1984) 항목을 해결 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-219">Click **OK** to go back and fix the entry (the year for "Ghostbusters" is 1984), and then press Enter.</span></span>

<span data-ttu-id="07e7a-220">8 될 때까지 또는 있으므로 몇 가지 영화를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-220">Fill in several movies until you have 8 or so.</span></span> <span data-ttu-id="07e7a-221">(8 입력 쉽게 페이징 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-221">(Entering 8 makes it easier to work with paging later.</span></span> <span data-ttu-id="07e7a-222">하지만 너무 많은 경우, 입력 지금은 일부에 불과합니다.) 실제 데이터는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-222">But if that's too many, enter just a few for now.) The actual data doesn't matter.</span></span>

![두 레코드를 사용 하 여 WebMatrix에서 데이터베이스 항목 표](displaying-data/_static/image16.png)

<span data-ttu-id="07e7a-224">오류 없이 모든 영화를 입력 한 경우에 ID 값은 순차적입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-224">If you entered all the movies without any errors, the ID values are sequential.</span></span> <span data-ttu-id="07e7a-225">불완전 한 영화 레코드를 저장 하려고 하면 ID 번호가 순차적 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-225">If you tried to save an incomplete movie record, the ID numbers might not be sequential.</span></span> <span data-ttu-id="07e7a-226">그렇다면 좋은 현상입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-226">If so, that's okay.</span></span> <span data-ttu-id="07e7a-227">숫자는 고유한 의미가 없는 및만 가장 중요 한 것에서 고유 합니다 *영화* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-227">The numbers don't have any inherent meaning, and the only thing that's important is that they're unique in the *Movies* table.</span></span>

<span data-ttu-id="07e7a-228">데이터베이스 디자이너를 포함 하는 탭을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-228">Close the tab that contains the database designer.</span></span>

<span data-ttu-id="07e7a-229">이제 웹 페이지에서이 데이터의 표시에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-229">Now you can turn to displaying this data on a web page.</span></span>

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a><span data-ttu-id="07e7a-230">페이지 WebGrid 도우미를 사용 하 여 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="07e7a-230">Displaying Data in a Page by Using the WebGrid Helper</span></span>

<span data-ttu-id="07e7a-231">페이지에서 데이터를 표시 하려면 사용 하려는 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-231">To display data in a page, you're going to use the `WebGrid` helper.</span></span> <span data-ttu-id="07e7a-232">이 도우미 표 또는 테이블 (행 및 열) 표시를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-232">This helper produces a display in a grid or table (rows and columns).</span></span> <span data-ttu-id="07e7a-233">알 수 있듯이 서식 및 기타 기능을 사용 하 여 눈금 수 구체화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-233">As you'll see, you'll be able refine the grid with formatting and other features.</span></span>

<span data-ttu-id="07e7a-234">표를 실행 하려면 몇 줄의 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-234">To run the grid, you'll have to write a few lines of code.</span></span> <span data-ttu-id="07e7a-235">다음 몇 줄은이 자습서에서 수행 하는 데이터 액세스의 거의 모든 패턴의 한 종류로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-235">These few lines will serve as a kind of pattern for almost all of the data access that you do in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="07e7a-236">실제로 여러 가지 옵션이 페이지에 데이터를 표시 합니다. `WebGrid` 도우미 하나일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-236">You actually have many options for displaying data on a page; the `WebGrid` helper is just one.</span></span> <span data-ttu-id="07e7a-237">당사가 것이 자습서에 대 한 데이터를 표시 하는 가장 쉬운 방법은 이므로 및 합리적으로 유연한 이기 때문에.</span><span class="sxs-lookup"><span data-stu-id="07e7a-237">We chose it for this tutorial because it's the easiest way to display data and because it's reasonably flexible.</span></span> <span data-ttu-id="07e7a-238">다음 자습서 집합에서 데이터를 표시 하는 방법에 대해 보다 직접적인 제어를 제공 하는 페이지에서 데이터를 사용 하려면 "수동" 방법은 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-238">In the next tutorial set, you'll see how to use a more "manual" way to work with data in the page, which gives you more direct control over how to display the data.</span></span>


<span data-ttu-id="07e7a-239">WebMatrix에서 왼쪽된 창에서 클릭 합니다 **파일** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-239">In the left pane in WebMatrix, click the **Files** workspace.</span></span>

<span data-ttu-id="07e7a-240">만든 새 데이터베이스에는 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-240">The new database you created is in the *App\_Data* folder.</span></span> <span data-ttu-id="07e7a-241">폴더 존재 하지 않은 경우 WebMatrix에 새 데이터베이스에 대 한 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-241">If the folder didn't already exist, WebMatrix created it for your new database.</span></span> <span data-ttu-id="07e7a-242">(폴더 존재 했을 수 도우미를 이전에 설치한 경우.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-242">(The folder might have existed if you'd previously installed helpers.)</span></span>

<span data-ttu-id="07e7a-243">트리 뷰에서 웹 사이트의 루트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-243">In the tree view, select the root of the website.</span></span> <span data-ttu-id="07e7a-244">웹 사이트의 루트를 선택 해야 합니다. 앱에 새 파일을 추가할 수 있습니다이 고, 그렇지\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="07e7a-244">You must select the root of the website; otherwise, the new file might be added to the App\_Data folder.</span></span>

<span data-ttu-id="07e7a-245">리본 메뉴에서 클릭 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-245">In the ribbon, click **New**.</span></span> <span data-ttu-id="07e7a-246">에 **파일 형식을 선택** 상자에서 **CSHTML**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-246">In the **Choose a File Type** box, choose **CSHTML**.</span></span>

<span data-ttu-id="07e7a-247">에 **이름을** 상자에서 이름을 "Movies.cshtml" 새 페이지:</span><span class="sxs-lookup"><span data-stu-id="07e7a-247">In the **Name** box, name the new page "Movies.cshtml":</span></span>

!['영화' 페이지를 보여 주는 대화 상자 '파일 유형을 선택 합니다.'](displaying-data/_static/image17.png)

<span data-ttu-id="07e7a-249">클릭 합니다 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-249">Click the **OK** button.</span></span> <span data-ttu-id="07e7a-250">WebMatrix에 몇 가지 기본 요소를 사용 하 여 새 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-250">WebMatrix opens a new file with some skeleton elements in it.</span></span> <span data-ttu-id="07e7a-251">먼저 데이터베이스에서 데이터를 가져올 이동할 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-251">First you'll write some code to go get the data from the database.</span></span> <span data-ttu-id="07e7a-252">그런 다음 실제로 데이터를 표시 하려면 페이지에 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-252">Then you'll add markup to the page to actually display the data.</span></span>

### <a name="writing-the-data-query-code"></a><span data-ttu-id="07e7a-253">데이터 쿼리 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-253">Writing the Data Query Code</span></span>

<span data-ttu-id="07e7a-254">페이지의 맨 위에 있는 간의 합니다 `@{` 및 `}` 문자에는 다음 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-254">At the top of the page, between the `@{` and `}` characters, enter the following code.</span></span> <span data-ttu-id="07e7a-255">(여는 태그와 닫는 중괄호 사이의이 코드를 입력 하는 있는지 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-255">(Make sure that you enter this code between the opening and closing braces.)</span></span>

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

<span data-ttu-id="07e7a-256">첫 번째 줄은 항상 첫 번째 단계는 데이터베이스를 사용 하 여 작업을 수행 하기 전에 이전에 만든 데이터베이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-256">The first line opens the database that you created earlier, which is always the first step before doing something with the database.</span></span> <span data-ttu-id="07e7a-257">지시는 `Database.Open` 열려는 데이터베이스의 메서드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-257">You tell the `Database.Open` method name of the database to open.</span></span> <span data-ttu-id="07e7a-258">포함 하지 않는 통지 *.sdf* 이름에서입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-258">Notice that you don't include *.sdf* in the name.</span></span> <span data-ttu-id="07e7a-259">합니다 `Open` 메서드를 확인 하는 것에 대 한 가정를 *.sdf* 파일 (즉, *WebPagesMovies.sdf*) 하 고는 *.sdf* 파일은는 *앱\_ 데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-259">The `Open` method assumes that it's looking for an *.sdf* file (that is, *WebPagesMovies.sdf*) and that the *.sdf* file is in the *App\_Data* folder.</span></span> <span data-ttu-id="07e7a-260">(앞서는 합니다 *앱\_데이터* 폴더 이기;이 시나리오는 ASP.NET 해당 이름에 대 한 가정을 있는 위치 중 하나입니다.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-260">(Earlier we noted that the *App\_Data* folder is reserved; this scenario is one of the places where ASP.NET makes assumptions about that name.)</span></span>

<span data-ttu-id="07e7a-261">에 대 한 참조 라는 변수에 넣을 데이터베이스를 열 때 `db`합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-261">When the database is opened, a reference to it is put into the variable named `db`.</span></span> <span data-ttu-id="07e7a-262">(하는 이름을 지정할 수 있습니다 아무 것도 있습니다.) `db` 변수가 어떻게 데이터베이스와 상호 작용 남게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-262">(Which could be named anything.) The `db` variable is how you'll end up interacting with the database.</span></span>

<span data-ttu-id="07e7a-263">두 번째 줄은 실제로 사용 하 여 데이터베이스 데이터를 인출 합니다 `Query` 메서드.</span><span class="sxs-lookup"><span data-stu-id="07e7a-263">The second line actually fetches the database data by using the `Query` method.</span></span> <span data-ttu-id="07e7a-264">이 코드의 작동 원리를 알 수 있습니다: 합니다 `db` 변수가 열린된 데이터베이스에 대 한 참조 및 호출 하는 `Query` 메서드를 사용 하 여 합니다 `db` 변수 (`db.Query`).</span><span class="sxs-lookup"><span data-stu-id="07e7a-264">Notice how this code works: the `db` variable has a reference to the opened database, and you invoke the `Query` method by using the `db` variable (`db.Query`).</span></span>

<span data-ttu-id="07e7a-265">쿼리 자체는 SQL `Select` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-265">The query itself is a SQL `Select` statement.</span></span> <span data-ttu-id="07e7a-266">(SQL에 대 한 약간의 배경, 뒷부분 설명 참조). 문에서 `Movies` 쿼리 테이블을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-266">(For a little background about SQL, see the explanation later.) In the statement, `Movies` identifies the table to query.</span></span> <span data-ttu-id="07e7a-267">`*` 문자 쿼리가 테이블에서 모든 열을 반환 해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-267">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="07e7a-268">(또한를 나열할 수 열을 개별적으로 쉼표로 구분 하 여.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-268">(You could also list columns individually, separated by commas.)</span></span>

<span data-ttu-id="07e7a-269">쿼리 결과가 있는 경우 반환 되 고에서 사용 가능 합니다 `selectedData` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-269">The results of the query, if any, are returned and made available in the `selectedData` variable.</span></span> <span data-ttu-id="07e7a-270">마찬가지로 변수 이름을 지정할 수 있습니다 아무 것도 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-270">Again, the variable could be named anything.</span></span>

<span data-ttu-id="07e7a-271">마지막으로 세 번째 줄은 asp의 인스턴스를 사용 하려는 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-271">Finally, the third line tells ASP.NET that you want to use an instance of the `WebGrid` helper.</span></span> <span data-ttu-id="07e7a-272">만든 (*인스턴스화할*) 도우미 개체를 사용 하 여 합니다 `new` 키워드를 통해 쿼리 결과 전달 하 고는 `selectedData` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-272">You create (*instantiate*) the helper object by using the `new` keyword and pass it the query results via the `selectedData` variable.</span></span> <span data-ttu-id="07e7a-273">새 `WebGrid` 데이터베이스 쿼리 결과 함께 개체에서 제공 되는 `grid` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-273">The new `WebGrid` object, along with the results of the database query, are made available in the `grid` variable.</span></span> <span data-ttu-id="07e7a-274">페이지에서 데이터를 실제로 표시할 잠시 후에 발생을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-274">You'll need that result in a moment to actually display the data in the page.</span></span>

<span data-ttu-id="07e7a-275">이 단계에서는 데이터베이스 열린, 데이터를 받으신를 하 고 준비한는 `WebGrid` 데이터가 포함 된 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-275">At this stage, the database has been opened, you've gotten the data you want, and you've prepared the `WebGrid` helper with that data.</span></span> <span data-ttu-id="07e7a-276">다음 페이지에서 태그를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-276">Next is to create the markup in the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="07e7a-277">**구조적된 쿼리 언어 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="07e7a-277">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="07e7a-278">SQL은 데이터베이스에서 데이터를 관리 하는 것에 대 한 대부분의 관계형 데이터베이스에 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-278">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="07e7a-279">데이터를 검색 하 고 업데이트 하 고 만들기, 수정 및 데이터베이스 테이블에서 데이터를 관리할 수 있는 명령을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-279">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage data in database tables.</span></span> <span data-ttu-id="07e7a-280">SQL 프로그래밍 언어 (예: C#)와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-280">SQL is different than a programming language (like C#).</span></span> <span data-ttu-id="07e7a-281">SQL을 사용 하 여 원하는 항목을 데이터베이스에 알립니다 이며 데이터베이스의 데이터를 가져오는 작업을 수행 하는 방법을 파악 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-281">With SQL, you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="07e7a-282">다음은 일부 SQL 명령의 예로 및 용도:</span><span class="sxs-lookup"><span data-stu-id="07e7a-282">Here are examples of some SQL commands and what they do:</span></span>
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="07e7a-283">첫 번째 `Select` 문에 모든 열을 가져옵니다 (지정 된 `*`)에서 *영화* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-283">The first `Select` statement gets all the columns (specified by `*`) from the *Movies* table.</span></span>
> 
> <span data-ttu-id="07e7a-284">두 번째 `Select` 문을 레코드에서 ID, 이름 및 Price 열을 인출 합니다 *제품* 10 개가 넘는 가격 열 값이 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-284">The second `Select` statement fetches the ID, Name, and Price columns from records in the *Product* table whose Price column value is more than 10.</span></span> <span data-ttu-id="07e7a-285">명령 이름 열의 값을 기준으로 알파벳 순서로 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-285">The command returns the results in alphabetical order based on the values of the Name column.</span></span> <span data-ttu-id="07e7a-286">가격 조건과 일치 하는 레코드가 없는 경우 명령이 빈 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-286">If no records match the price criteria, the command returns an empty set.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> <span data-ttu-id="07e7a-287">이 명령에 새 레코드를 삽입 합니다 *제품* 테이블 1.99을 이름 열 "Croissant", "는 취약 한 만족" Description 열 및 가격을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-287">This command inserts a new record into the *Product* table, setting the Name column to "Croissant", the Description column to "A flaky delight", and the price to 1.99.</span></span>
> 
> <span data-ttu-id="07e7a-288">숫자가 아닌 값을 지정할 때 값은 단일 따옴표 안에 (없습니다 큰따옴표와 같이 C#)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-288">Notice that when you're specifying a non-numeric value, the value is enclosed in single quotation marks (not double quotation marks, as in C#).</span></span> <span data-ttu-id="07e7a-289">텍스트 또는 날짜 값을 관련 되지만 숫자 해결 하지 이러한 따옴표를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-289">You use these quotation marks around text or date values, but not around numbers.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> <span data-ttu-id="07e7a-290">이 명령에서 레코드를 삭제 합니다 *제품* 2008 년 1 월 1 일 이전인 만료 날짜 열이 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-290">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="07e7a-291">(명령 있다고 가정 합니다 *제품* 테이블에 이러한 열이 물론.) MM/DD/YYYY 형식으로 날짜는 여기에 입력 하는 있지만 해당 로캘에 사용 되는 형식으로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-291">(The command assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="07e7a-292">합니다 `Insert` 고 `Delete` 명령 결과 집합을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-292">The `Insert` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="07e7a-293">대신, 레코드 수를 명령에 의해 영향을 알려 주는 숫자로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-293">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="07e7a-294">이러한 작업 (예: 레코드 삽입 및 삭제)의 일부에 대 한 작업을 요청 하는 프로세스는 데이터베이스에 대 한 적절 한 권한이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-294">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="07e7a-295">데이터베이스에 연결할 때 사용자 이름 및 암호를 제공 해야 하는 프로덕션 데이터베이스에 대 한 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-295">That's why for production databases you often have to supply a user name and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="07e7a-296">SQL 명령 여러 가지가 있지만 모든 명령 다음과 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-296">There are dozens of SQL commands, but they all follow a pattern like the commands you see here.</span></span> <span data-ttu-id="07e7a-297">SQL 명령을 사용 하 여 데이터베이스 및 테이블을 만들고, 테이블의 레코드 개수, 가격 계산 보다 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-297">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>


### <a name="adding-markup-to-display-the-data"></a><span data-ttu-id="07e7a-298">데이터를 표시 하는 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-298">Adding Markup to Display the Data</span></span>

<span data-ttu-id="07e7a-299">내 합니다 `<head>` 요소 집합 내용의 `<title>` "Movies" 요소:</span><span class="sxs-lookup"><span data-stu-id="07e7a-299">Inside the `<head>` element, set contents of the `<title>` element to "Movies":</span></span>

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

<span data-ttu-id="07e7a-300">내부는 `<body>` 다음을 추가 하는 페이지의 요소:</span><span class="sxs-lookup"><span data-stu-id="07e7a-300">Inside the `<body>` element of the page, add the following:</span></span>

[!code-html[Main](displaying-data/samples/sample3.html)]

<span data-ttu-id="07e7a-301">이제</span><span class="sxs-lookup"><span data-stu-id="07e7a-301">That's it.</span></span> <span data-ttu-id="07e7a-302">합니다 `grid` 변수를 만들 때 만든 값인는 `WebGrid` 이전 코드에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-302">The `grid` variable is the value you created when you created the `WebGrid` object in code earlier.</span></span>

<span data-ttu-id="07e7a-303">WebMatrix 트리 보기에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **브라우저에서 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-303">In the WebMatrix tree view, right-click the page and select **Launch in browser**.</span></span> <span data-ttu-id="07e7a-304">이 페이지와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-304">You'll see something like this page:</span></span>

![동영상 테이블에서 기본 WebGrid 도우미 출력](displaying-data/_static/image18.png)

<span data-ttu-id="07e7a-306">해당 열으로 정렬 하려면 열 제목 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-306">Click a column heading link to sort by that column.</span></span> <span data-ttu-id="07e7a-307">머리글을 클릭 하 여 정렬할 수 있는 기능은 기본으로 제공 되는 **WebGrid** 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-307">Being able to sort by clicking a heading is a feature that's built into the **WebGrid** helper.</span></span>

<span data-ttu-id="07e7a-308">`GetHtml` 메서드 이름에서 알 수 있듯이, 생성 데이터를 표시 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-308">The `GetHtml` method, as its name suggests, generates markup that displays the data.</span></span> <span data-ttu-id="07e7a-309">기본적으로 `GetHtml` 메서드는 HTML을 생성 합니다. `<table>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-309">By default, the `GetHtml` method generates an HTML `<table>` element.</span></span> <span data-ttu-id="07e7a-310">(원한다 면 확인할 수 있습니다 렌더링 브라우저에서 페이지의 소스를 보면.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-310">(If you want, you can verify the rendering by looking at the source of the page in the browser.)</span></span>

## <a name="modifying-the-look-of-the-grid"></a><span data-ttu-id="07e7a-311">눈금의 모양 수정</span><span class="sxs-lookup"><span data-stu-id="07e7a-311">Modifying the Look of the Grid</span></span>

<span data-ttu-id="07e7a-312">사용 하는 `WebGrid` 도우미 방금 수행한 것 처럼 간단 하지만 결과 표시는 일반입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-312">Using the `WebGrid` helper like you just did is easy, but the resulting display is plain.</span></span> <span data-ttu-id="07e7a-313">`WebGrid` 도우미에는 데이터가 표시 되는 방식을 제어할 수 있는 모든 종류의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-313">The `WebGrid` helper has all sorts of options that let you control how the data is displayed.</span></span> <span data-ttu-id="07e7a-314">이 자습서에서는 탐색에 너무 많은 있지만이 섹션에서는 이러한 옵션 중 일부 아이디어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-314">There are far too many to explore in this tutorial, but this section will give you an idea of some of those options.</span></span> <span data-ttu-id="07e7a-315">이 시리즈의 뒷부분에 나오는 자습서에서 몇 가지 추가 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-315">A few additional options will be covered in later tutorials in this series.</span></span>

### <a name="specifying-individual-columns-to-display"></a><span data-ttu-id="07e7a-316">표시할 개별 열 지정</span><span class="sxs-lookup"><span data-stu-id="07e7a-316">Specifying Individual Columns to Display</span></span>

<span data-ttu-id="07e7a-317">를 시작 하려면 특정 열만 표시 되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-317">To start, you can specify that you want to display only certain columns.</span></span> <span data-ttu-id="07e7a-318">기본적으로 지금까지 살펴본 대로 표 형식으로 표시에서 열의 모든 4 합니다 *영화* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-318">By default, as you've seen, the grid shows all four of the columns from the *Movies* table.</span></span>

<span data-ttu-id="07e7a-319">에 *Movies.cshtml* 파일에서 바꾸기는 `@grid.GetHtml()` 다음을 사용 하 여 방금 추가한 태그:</span><span class="sxs-lookup"><span data-stu-id="07e7a-319">In the *Movies.cshtml* file, replace the `@grid.GetHtml()` markup that you just added with the following:</span></span>

[!code-css[Main](displaying-data/samples/sample4.css)]

<span data-ttu-id="07e7a-320">포함 된 도우미 표시할 열을 판단할 수는 `columns` 에 대 한 매개 변수는 `GetHtml` 메서드와 열의 컬렉션을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-320">To tell the helper which columns to display, you include a `columns` parameter for the `GetHtml` method and pass in a collection of columns.</span></span> <span data-ttu-id="07e7a-321">컬렉션에 포함할 각 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-321">In the collection, you specify each column to include.</span></span> <span data-ttu-id="07e7a-322">포함 하 여 표시할 개별 열을 지정 하는 `grid.Column` 개체 및 데이터 열 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-322">You specify an individual column to display by including a `grid.Column` object, and pass in the name of the data column you want.</span></span> <span data-ttu-id="07e7a-323">(이러한 열은 SQL 쿼리 결과에 포함 되어야 합니다-는 `WebGrid` 도우미 쿼리에 의해 반환 되지 않았습니다 하는 열을 표시할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="07e7a-323">(These columns must be included in the SQL query results — the `WebGrid` helper cannot display columns that were not returned by the query.)</span></span>

<span data-ttu-id="07e7a-324">시작 합니다 *Movies.cshtml* 마찬가지로 시간과이 다음과 같은 표시를 표시 하 고 브라우저에서 페이지 (ID 열이 없는 표시 되는지 확인):</span><span class="sxs-lookup"><span data-stu-id="07e7a-324">Launch the *Movies.cshtml* page in the browser again, and this time you get a display like the following one (notice that no ID column is displayed):</span></span>

![선택한 열만 표시 WebGrid 표시](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a><span data-ttu-id="07e7a-326">눈금의 모양 변경</span><span class="sxs-lookup"><span data-stu-id="07e7a-326">Changing the Look of the Grid</span></span>

<span data-ttu-id="07e7a-327">가지 열이이 집합에서 나중에 자습서에서 탐색할 수는 그 중 일부를 표시 하기 위한 몇 가지 더 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-327">There are quite a few more options for displaying columns, some of which will be explored in later tutorials in this set.</span></span> <span data-ttu-id="07e7a-328">지금은이 섹션에서는 소개 방법을 전체적으로 모눈 스타일 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-328">For now, this section will introduce you to ways in which you can style the grid as a whole.</span></span>

<span data-ttu-id="07e7a-329">내 합니다 `<head>` 닫기 전에 페이지의 섹션 `</head>` 태그를 다음 추가 `<style>` 요소:</span><span class="sxs-lookup"><span data-stu-id="07e7a-329">Inside the `<head>` section of the page, just before the closing `</head>` tag, add the following `<style>` element:</span></span>

[!code-css[Main](displaying-data/samples/sample5.css)]

<span data-ttu-id="07e7a-330">라는 클래스를 정의 하는이 CSS 태그가 `grid`, `head`등입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-330">This CSS markup defines classes named `grid`, `head`, and so on.</span></span> <span data-ttu-id="07e7a-331">별도의 이러한 스타일 정의 배치할 수도 있습니다 *.css* 파일 및 페이지에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-331">You could also put these style definitions in a separate *.css* file and link that to the page.</span></span> <span data-ttu-id="07e7a-332">(실제로 할 수 있습니다이 자습서 집합의 뒷부분에 나오는.) 하지만 작업 하면 간편 하 게이 자습서에 데이터를 표시 하는 동일한 페이지 내에서.</span><span class="sxs-lookup"><span data-stu-id="07e7a-332">(In fact, you'll do that later in this tutorial set.) But to make things easy for this tutorial, they're inside the same page that displays the data.</span></span>

<span data-ttu-id="07e7a-333">이제 가져올 수 있습니다는 `WebGrid` 이러한 스타일 클래스를 사용 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-333">Now you can get the `WebGrid` helper to use these style classes.</span></span> <span data-ttu-id="07e7a-334">도우미에 다양 한 속성 (예를 들어 `tableStyle`)이를 위해서는-CSS 스타일 클래스 이름에 할당 및 해당 클래스 이름을 도우미에서 렌더링 되는 태그의 일부로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-334">The helper has a number of properties (for example, `tableStyle`) for just this purpose — you assign a CSS style class name to them, and that class name is rendered as part of the markup that's rendered by the helper.</span></span>

<span data-ttu-id="07e7a-335">변경 된 `grid.GetHtml` 태그 하므로 이제이 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-335">Change the `grid.GetHtml` markup so that it now looks like this code:</span></span>

[!code-css[Main](displaying-data/samples/sample6.css)]

<span data-ttu-id="07e7a-336">새 여기서은 사용자가 추가한 `tableStyle`, `headerStyle`, 및 `alternatingRowStyle` 매개 변수는 `GetHtml` 메서드.</span><span class="sxs-lookup"><span data-stu-id="07e7a-336">What's new here is that you've added `tableStyle`, `headerStyle`, and `alternatingRowStyle` parameters to the `GetHtml` method.</span></span> <span data-ttu-id="07e7a-337">이러한 매개 변수를 조금 전에 추가한 CSS 스타일의 이름으로 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-337">These parameters have been set to the names of the CSS styles that you added a moment ago.</span></span>

<span data-ttu-id="07e7a-338">페이지를 실행 하 고이 시간 전에 보다 훨씬 일반 보이는 표가 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-338">Run the page, and this time you see a grid that looks much less plain than before:</span></span>

![CSS 클래스 이름으로 설정 하는 매개 변수가 포함 된 WebGrid 표시](displaying-data/_static/image20.png)

<span data-ttu-id="07e7a-340">어떻게 되는지 확인할 수는 `GetHtml` 생성 메서드를 보면 브라우저에서 페이지의 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-340">To see what the `GetHtml` method generated, you can look at the source of the page in the browser.</span></span> <span data-ttu-id="07e7a-341">여기에서 자세히 다루지는 것 이지만 중요 한 점은와 같은 매개 변수를 지정 하 여 `tableStyle`, 다음과 같은 HTML 태그를 생성 하는 표를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-341">We won't go into detail here, but the important point is that by specifying parameters like `tableStyle`, you caused the grid to generate HTML tags like the following:</span></span>

`<table class="grid">`

<span data-ttu-id="07e7a-342">`<table>` 태그 했습니다는 `class` 앞부분에서 추가한 CSS 규칙 중 하나를 참조 하는 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-342">The `<table>` tag has had a `class` attribute added to it that references one of the CSS rules that you added earlier.</span></span> <span data-ttu-id="07e7a-343">이 코드에서는 기본 패턴을 보여 줍니다 &mdash; 에 대 한 다양 한 매개 변수는 `GetHtml` 메서드 let 참조 CSS 클래스 메서드를 다음 태그와 함께 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-343">This code shows you the basic pattern &mdash; different parameters for the `GetHtml` method let you reference CSS classes that the method then generates along with the markup.</span></span> <span data-ttu-id="07e7a-344">CSS 클래스를 사용 하 여 여러분에 게 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-344">What you do with the CSS classes is up to you.</span></span>

## <a name="adding-paging"></a><span data-ttu-id="07e7a-345">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="07e7a-345">Adding Paging</span></span>

<span data-ttu-id="07e7a-346">이 자습서에 대 한 마지막 작업으로 페이징 표에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-346">As the last task for this tutorial, you'll add paging to the grid.</span></span> <span data-ttu-id="07e7a-347">지금 한 번에 모든 영화를 표시 하는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-347">Right now it's no problem to display all your movies at once.</span></span> <span data-ttu-id="07e7a-348">하지만 페이지 표시 길어지면는 수백 개의 영화를 추가한 경우.</span><span class="sxs-lookup"><span data-stu-id="07e7a-348">But if you added hundreds of movies, the page display would get long.</span></span>

<span data-ttu-id="07e7a-349">페이지 코드에서 만드는 줄에 변경 된 `WebGrid` 다음 코드는 개체:</span><span class="sxs-lookup"><span data-stu-id="07e7a-349">In the page code, change the line that creates the `WebGrid` object to the following code:</span></span>

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

<span data-ttu-id="07e7a-350">앞에서 유일한 차이점은 사용자가 추가한를 `rowsPerPage` 매개 변수를 3으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-350">The only difference from before is that you've added a `rowsPerPage` parameter that's set to 3.</span></span>

<span data-ttu-id="07e7a-351">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-351">Run the page.</span></span> <span data-ttu-id="07e7a-352">표 시간 및 데이터베이스에서 동영상 페이지 수 있도록 탐색 링크에 3 개의 행을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-352">The grid displays 3 rows at a time, plus navigation links that let you page through the movies in your database:</span></span>

![페이징 사용 하 여 WebGrid 표시](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a><span data-ttu-id="07e7a-354">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="07e7a-354">Coming Up Next</span></span>

<span data-ttu-id="07e7a-355">다음 자습서에서는 사용자 입력을 가져오는 형태로 Razor 및 C# 코드를 사용 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-355">In the next tutorial, you'll learn how to use Razor and C# code to get user input in a form.</span></span> <span data-ttu-id="07e7a-356">제목 또는 장르의 영화를 찾을 수 있도록 Movies 페이지로 검색 상자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e7a-356">You'll add a search box to the Movies page so that you can find movies by title or genre.</span></span>

## <a name="complete-listing-for-movies-page"></a><span data-ttu-id="07e7a-357">동영상 페이지에 대 한 전체 목록</span><span class="sxs-lookup"><span data-stu-id="07e7a-357">Complete Listing for Movies Page</span></span>

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="07e7a-358">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="07e7a-358">Additional Resources</span></span>

- [<span data-ttu-id="07e7a-359">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="07e7a-359">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> <span data-ttu-id="07e7a-360">[이전](intro-to-web-pages-programming.md)
> [다음](form-basics.md)</span><span class="sxs-lookup"><span data-stu-id="07e7a-360">[Previous](intro-to-web-pages-programming.md)
[Next](form-basics.md)</span></span>
