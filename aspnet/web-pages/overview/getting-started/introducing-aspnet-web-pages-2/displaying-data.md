---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: "ASP.NET 웹 페이지를 소개 합니다.-데이터를 표시 합니다. | Microsoft Docs"
author: tfitzmac
description: "이 자습서를 WebMatrix에서 데이터베이스를 만드는 방법 및 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 데이터베이스 데이터 페이지에 표시 하는 방법을 보여 줍니다. Y... 가정"
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: fdb9af0ba87c7802c63451ac7aa422e0020b5719
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introducing-aspnet-web-pages---displaying-data"></a><span data-ttu-id="1aab8-104">데이터를 표시 하는 ASP.NET 웹 페이지-소개</span><span class="sxs-lookup"><span data-stu-id="1aab8-104">Introducing ASP.NET Web Pages - Displaying Data</span></span>
====================
<span data-ttu-id="1aab8-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1aab8-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1aab8-106">이 자습서를 WebMatrix에서 데이터베이스를 만드는 방법 및 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 데이터베이스 데이터 페이지에 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-106">This tutorial shows you how to create a database in WebMatrix and how to display database data in a page when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="1aab8-107">통해 시리즈를 완료 한 것으로 가정 [ASP.NET 웹 페이지 프로그래밍 소개](../introducing-razor-syntax-c.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-107">It assumes you have completed the series through [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md).</span></span>
> 
> <span data-ttu-id="1aab8-108">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="1aab8-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="1aab8-109">데이터베이스 및 데이터베이스 테이블을 만들려면 WebMatrix 도구를 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="1aab8-109">How to use WebMatrix tools to create a database and database tables.</span></span>
> - <span data-ttu-id="1aab8-110">데이터베이스에 데이터를 추가 하려면 WebMatrix 도구를 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="1aab8-110">How to use WebMatrix tools to add data to a database.</span></span>
> - <span data-ttu-id="1aab8-111">데이터베이스의 데이터 페이지에 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="1aab8-111">How to display data from the database on a page.</span></span>
> - <span data-ttu-id="1aab8-112">ASP.NET 웹 페이지에서 SQL 명령을 실행 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="1aab8-112">How to run SQL commands in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="1aab8-113">사용자 지정 하는 `WebGrid` 도우미 데이터 표시를 변경 하 고 페이징 및 정렬과 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-113">How to customize the `WebGrid` helper to change the data display and to add paging and sorting.</span></span>
>   
> 
> <span data-ttu-id="1aab8-114">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="1aab8-115">WebMatrix 데이터베이스 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-115">WebMatrix database tools.</span></span>
> - <span data-ttu-id="1aab8-116">`WebGrid`도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-116">`WebGrid` helper.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="1aab8-117">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="1aab8-117">What You'll Build</span></span>

<span data-ttu-id="1aab8-118">ASP.NET 웹 페이지에 이전 자습서에서 소개한 (*.cshtml* 파일), Razor 구문에 기본적인 및 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-118">In the previous tutorial, you were introduced to ASP.NET Web Pages (*.cshtml* files), to the basics of Razor syntax, and to helpers.</span></span> <span data-ttu-id="1aab8-119">이 자습서에서는 시리즈의 나머지 부분을 사용 하는 실제 웹 응용 프로그램을 만들기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-119">In this tutorial, you'll begin creating the actual web application that you'll use for the rest of the series.</span></span> <span data-ttu-id="1aab8-120">앱을 보고, 추가, 변경 및 영화에 대 한 정보를 삭제할 수 있는 간단한 영화 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="1aab8-120">The app is a simple movie application that lets you view, add, change, and delete information about movies.</span></span>

<span data-ttu-id="1aab8-121">이 자습서와 함께 마친 경우이 페이지 처럼 보이는 동영상 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-121">When you're done with this tutorial, you'll be able to view a movie listing that looks like this page:</span></span>

![CSS 클래스 이름으로 설정 하는 매개 변수가 포함 된 WebGrid 표시](displaying-data/_static/image1.png)

<span data-ttu-id="1aab8-123">그러나를 시작 하려면 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-123">But to begin, you have to create a database.</span></span>

## <a name="a-very-brief-introduction-to-databases"></a><span data-ttu-id="1aab8-124">데이터베이스에 대 한 매우 짧은 소개</span><span class="sxs-lookup"><span data-stu-id="1aab8-124">A Very Brief Introduction to Databases</span></span>

<span data-ttu-id="1aab8-125">이 자습서는 데이터베이스는 briefest 소개만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-125">This tutorial will provide only the briefest introduction to databases.</span></span> <span data-ttu-id="1aab8-126">데이터베이스 경험이 있다면이 짧은 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-126">If you have database experience, you can skip this short section.</span></span>

<span data-ttu-id="1aab8-127">데이터베이스 정보를 포함 하는 하나 이상의 테이블이 포함 &mdash; 예를 들어 테이블에 고객, 주문 및 공급 업체에 대 한 또는 학생, 교사, 클래스 및 등급에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-127">A database contains one or more tables that contain information &mdash; for example, tables for customers, orders, and vendors, or for students, teachers, classes, and grades.</span></span> <span data-ttu-id="1aab8-128">구조적으로 데이터베이스 테이블 스프레드시트 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-128">Structurally, a database table is like a spreadsheet.</span></span> <span data-ttu-id="1aab8-129">일반적인 주소록을 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1aab8-129">Imagine a typical address book.</span></span> <span data-ttu-id="1aab8-130">주소록에 각 항목에 대 한 (즉, 각 사용자에 대 한) 일부의 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 정보를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-130">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

![간단한 모눈으로 예제 데이터베이스 테이블](displaying-data/_static/image2.png)

<span data-ttu-id="1aab8-132">(행은 라고도 *레코드*, 및 열은 라고도 *필드*.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-132">(Rows are sometimes referred to as *records*, and columns are sometimes referred to as *fields*.)</span></span>

<span data-ttu-id="1aab8-133">대부분의 데이터베이스 테이블에 대 한 테이블에 고객 번호, 계좌 번호 등과 같은 고유한 값을 포함 하는 열을 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-133">For most database tables, the table has to have a column that contains a unique value, like a customer number, account number, and so on.</span></span> <span data-ttu-id="1aab8-134">이 값은 테이블의 라고 *기본 키*, 테이블의 각 행 식별을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-134">This value is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="1aab8-135">예제에서는 ID 열은 앞의 예제에 표시 된 주소록에 대 한 기본 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-135">In the example, the ID column is the primary key for the address book shown in the previous example.</span></span>

<span data-ttu-id="1aab8-136">데이터베이스에서 정보를 읽어 페이지에 표시 및 웹 응용 프로그램에서 작업을 수행 하는 작업 중 많은 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-136">Much of the work you do in web applications consists of reading information out of the database and displaying it on a page.</span></span> <span data-ttu-id="1aab8-137">역시 사용자 로부터 정보를 수집 하는 데이터베이스에 추가 하거나 이미 데이터베이스에 있는 레코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-137">You'll also often gather information from users and add it to a database, or you'll modify records that are already in the database.</span></span> <span data-ttu-id="1aab8-138">(다룰 것이 자습서 집합 과정에서 이러한 작업의 모든.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-138">(We'll cover all of these operations in the course of this tutorial set.)</span></span>

<span data-ttu-id="1aab8-139">데이터베이스 작업이 있으므로 매우 복잡할 수 있으며 전문된 지식 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-139">Database work can be enormously complex and can require specialized knowledge.</span></span> <span data-ttu-id="1aab8-140">이 자습서 집합에 대 한 하지만 기본 개념에 게 모든 설명 작업을 진행 하면서를 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-140">For this tutorial set, though, you have to understand only basic concepts, which will all be explained as you go.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="1aab8-141">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1aab8-141">Creating a Database</span></span>

<span data-ttu-id="1aab8-142">WebMatrix에는 데이터베이스를 만들 수 있으며 데이터베이스에 테이블을 만드는 쉽게 구성 하는 도구가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-142">WebMatrix includes tools that make it easy to create a database and to create tables in the database.</span></span> <span data-ttu-id="1aab8-143">(데이터베이스의 구조를 데이터베이스의 라고 *스키마*.) 이 자습서 집합에 대 한 하나의 테이블에 있는 데이터베이스를 만들어 &mdash; 영화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-143">(The structure of a database is referred to as the database's *schema*.) For this tutorial set, you'll create a database that has only one table in it &mdash; Movies.</span></span>

<span data-ttu-id="1aab8-144">따라서 아직 수행 하지 않은 경우 WebMatrix를 열고 이전 자습서에서 만든 WebPagesMovies 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-144">Open WebMatrix if you haven't already done so, and open the WebPagesMovies site that you created in the previous tutorial.</span></span>

<span data-ttu-id="1aab8-145">왼쪽된 창에서 클릭 된 **데이터베이스** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-145">In the left pane, click the **Database** workspace.</span></span>

![WebMatrix 데이터베이스 작업 영역 탭](displaying-data/_static/image3.png)

<span data-ttu-id="1aab8-147">데이터베이스 관련 작업을 표시 하는 리본 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-147">The ribbon changes to show database-related tasks.</span></span> <span data-ttu-id="1aab8-148">리본 메뉴에서 클릭 **새 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-148">In the ribbon, click **New Database**.</span></span>

!['새 데이터베이스' WebMatrix 리본 메뉴의 단추](displaying-data/_static/image4.png)

<span data-ttu-id="1aab8-150">WebMatrix는 SQL Server CE 데이터베이스를 만듭니다 (한 *.sdf* 파일) 사이트와 동일한 이름을 가진 &mdash; *WebPagesMovies.sdf*합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-150">WebMatrix creates a SQL Server CE database (an *.sdf* file) that has the same name as your site &mdash; *WebPagesMovies.sdf*.</span></span> <span data-ttu-id="1aab8-151">(여기에서는이 수행 하지 않습니다 되지만 있습니다 이름을 바꿀 수 파일을 어디에을 있는 *.sdf* 확장 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-151">(You won't do this here, but you can rename the file to anything you like, as long as it has an *.sdf* extension.)</span></span>

## <a name="creating-a-table"></a><span data-ttu-id="1aab8-152">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1aab8-152">Creating a Table</span></span>

<span data-ttu-id="1aab8-153">리본 메뉴에서 클릭 **새 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-153">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="1aab8-154">WebMatrix는 새 탭에 테이블 디자이너를 엽니다. (새 테이블 옵션을 사용할 수 없으면 있는지 확인 왼쪽의 트리 보기에서 새 데이터베이스를 선택 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-154">WebMatrix opens the table designer in a new tab. (If the New Table option isn't available, make sure that the new database is selected in the tree view on the left.)</span></span>

!['새 테이블' WebMatrix 리본 메뉴의 단추](displaying-data/_static/image5.png)

<span data-ttu-id="1aab8-156">위쪽 (워터 마크가 표시 "Enter 테이블 이름")에 텍스트 상자에 "영화"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-156">In the text box at the top (where the watermark says "Enter table name"), enter "Movies".</span></span>

![WebMatrix 데이터베이스 디자이너에서 테이블 이름을 입력](displaying-data/_static/image6.png)

<span data-ttu-id="1aab8-158">아래 테이블 이름 정의 하는 경우 개별 열입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-158">The pane underneath the table name is where you define individual columns.</span></span> <span data-ttu-id="1aab8-159">에 대 한는 *동영상* 테이블이이 자습서에서는 몇 개의 열만을 만듭니다: *ID*, *제목*, *장르*, 및 *연도*.</span><span class="sxs-lookup"><span data-stu-id="1aab8-159">For the *Movies* table in this tutorial, you'll create only a few columns: *ID*, *Title*, *Genre*, and *Year*.</span></span>

<span data-ttu-id="1aab8-160">에 **이름** 상자에 "ID"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-160">In the **Name** box, enter "ID".</span></span> <span data-ttu-id="1aab8-161">새 열에 대 한 모든 컨트롤을 활성화 여기에서 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-161">Entering a value here activates all the controls for the new column.</span></span>

<span data-ttu-id="1aab8-162">탭에 **데이터 형식** 목록을 열고 **int**합니다. 이 값은 ID 열 (number)을 정수 데이터에 포함 되어 있음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-162">Tab to the **Data Type** list and choose **int**. This value specifies that the ID column will contain integer (number) data.</span></span>

> [!NOTE]
> <span data-ttu-id="1aab8-163">않습니다 이름을 모든 여기 (훨씬) 있지만이 표의 이동 하려면 표준 Windows 키보드 제스처를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-163">We won't call it out any more here (much), but you can use standard Windows keyboard gestures to navigate in this grid.</span></span> <span data-ttu-id="1aab8-164">예를 들어 필드 사이 이동 수를 수 있습니다만 목록에 항목을 선택 하려면 입력을 시작 등입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-164">For example, you can tab between fields, you can just start typing in order to select an item in a list, and so on.</span></span>


<span data-ttu-id="1aab8-165">이전 탭에서 **Default Value** 상자 (즉, 비워두면).</span><span class="sxs-lookup"><span data-stu-id="1aab8-165">Tab past the **Default Value** box (that is, leave it blank).</span></span> <span data-ttu-id="1aab8-166">탭에 **기본 키가** 확인란을 선택 하 고 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-166">Tab to the **Is Primary Key** check box and select it.</span></span> <span data-ttu-id="1aab8-167">이 옵션은 지시 데이터베이스 하는 *ID* 열에 개별 행을 식별 하는 데이터가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-167">This option tells the database that the *ID* column will contain the data that identifies individual rows.</span></span> <span data-ttu-id="1aab8-168">(즉, 각 행 해야 고유한 값을 해당 행을 찾는 데 사용할 수 있는 ID 열에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-168">(That is, each row will have a unique value in the ID column that you can use to find that row.)</span></span>

<span data-ttu-id="1aab8-169">선택 된 **Id** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-169">Choose the **Is Identity** option.</span></span> <span data-ttu-id="1aab8-170">이 옵션에 다음 일련 번호에 대 한 각각의 새 행을 생성 해야 자동으로 데이터베이스를 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-170">This option tells the database that it should automatically generate the next sequential number for each new row.</span></span> <span data-ttu-id="1aab8-171">(의 **Id** 도 선택한 경우에 옵션이 작동은 **기본 키가** 옵션입니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-171">(The **Is Identity** option works only if you've also selected the **Is Primary Key** option.)</span></span>

<span data-ttu-id="1aab8-172">다음 표에서 행을 클릭 하거나 tab 키를 눌러 현재 행을 두 번입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-172">Click in the next grid row, or press Tab twice to finish the current row.</span></span> <span data-ttu-id="1aab8-173">제스처 중 하나는 현재 행을 저장 하 고 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-173">Either gesture saves the current row and starts the next one.</span></span> <span data-ttu-id="1aab8-174">에 **Default Value** 열에 따르면 이제 **Null**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-174">Notice that the **Default Value** column now says **Null**.</span></span> <span data-ttu-id="1aab8-175">(Null은 기본 값에 대 한 기본값 마치도록 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-175">(Null is the default value for the default value, so to speak.)</span></span>

<span data-ttu-id="1aab8-176">새 정의 되 면 **ID** 열 디자이너가이 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-176">When you've finished defining the new **ID** column, the designer will look like this illustration:</span></span>

![영화 테이블에 대 한 ID 열을 정의 하 고 나면 WebMatrix 데이터베이스 디자이너](displaying-data/_static/image7.png)

<span data-ttu-id="1aab8-178">다음 열을 만들려면 클릭에서 상자에는 **이름** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-178">To create the next column, click in the box in the **Name** column.</span></span> <span data-ttu-id="1aab8-179">열에 대 한 "제목"를 입력 한 다음 선택 **nvarchar** 에 대 한는 **데이터 형식** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-179">Enter "Title" for the column and then select **nvarchar** for the **Data Type** value.</span></span> <span data-ttu-id="1aab8-180">"Var" 부분의 **nvarchar** 이 열에 대 한 데이터가 필요에 따라 크기가 레코드 간에 다를 수 있습니다 하는 문자열을 될 것 이라는 데이터베이스에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-180">The "var" part of **nvarchar** tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="1aab8-181">("N" 접두사를 나타내는 "national" 필드는 알파벳 이나 쓰기 시스템에 대 한 문자 데이터를 저장할 수 있는지를 나타내는-필드 유니코드 데이터를 보유 하는, 즉.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-181">(The "n" prefix represents "national," which indicates that the field can hold character data for any alphabet or writing system — that is, the field holds Unicode data.)</span></span>

<span data-ttu-id="1aab8-182">선택 하는 경우 **nvarchar**, 필드에 대 한 최대 길이 입력할 수 있는 다른 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-182">When you choose **nvarchar**, another box appears where you can enter the maximum length for the field.</span></span> <span data-ttu-id="1aab8-183">이 자습서에서 다루게 영화 제목 없음 50 자 보다 긴 된다는 가정 하에서 50을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-183">Enter 50, on the assumption that no movie title that you'll work with in this tutorial will be longer than 50 characters.</span></span>

<span data-ttu-id="1aab8-184">Skip **Default Value** 선택을 취소 하 고는 **Null 허용** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-184">Skip **Default Value** and clear the **Allow Nulls** option.</span></span> <span data-ttu-id="1aab8-185">데이터베이스에 제목이 없는 데이터베이스에 입력을 영화를 되기를 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-185">You don't want the database to allow any movies to be entered into the database that don't have a title.</span></span>

<span data-ttu-id="1aab8-186">완료 하 고 다음 행으로 이동 하는 경우 디자이너는이 그림 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-186">When you're done and move to the next row, the designer looks like this illustration:</span></span>

![영화 테이블에 대 한 Title 열을 정의 하 고 나면 WebMatrix 데이터베이스 디자이너](displaying-data/_static/image8.png)

<span data-ttu-id="1aab8-188">반복 길이 제외 하 고 "장르" 라는 열을 만들려면 다음이 단계 방금 30으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-188">Repeat these steps to create a column named "Genre", except for the length, set it to just 30.</span></span>

<span data-ttu-id="1aab8-189">"Year." 라는 다른 열 만들기</span><span class="sxs-lookup"><span data-stu-id="1aab8-189">Create another column named "Year."</span></span> <span data-ttu-id="1aab8-190">데이터 형식에 대 한 선택 **nchar** (하지 **nvarchar**) 길이 4로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-190">For the data type, choose **nchar** (not **nvarchar**) and set the length to 4.</span></span> <span data-ttu-id="1aab8-191">Year, 할지 "1995" 또는 "2010"와 같은 4 자리 숫자를 사용 하 여 다양 한 크기 열 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-191">For the year, you're going to use a 4-digit number like "1995" or "2010", so you don't require a variable-sized column.</span></span>

<span data-ttu-id="1aab8-192">완료 된 디자인의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-192">Here's what the finished design looks like:</span></span>

![영화 테이블에 대해 정의 된 모든 필드가 후 WebMatrix 데이터베이스 디자이너](displaying-data/_static/image9.png)

<span data-ttu-id="1aab8-194">Ctrl + S를 누르거나 클릭 하 고 **저장** 빠른 실행 도구 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-194">Press Ctrl+S or click the **Save** button in the Quick Access toolbar.</span></span> <span data-ttu-id="1aab8-195">탭을 닫아 데이터베이스 디자이너를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-195">Close the database designer by closing the tab.</span></span>

## <a name="adding-some-example-data"></a><span data-ttu-id="1aab8-196">일부 예제 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-196">Adding Some Example Data</span></span>

<span data-ttu-id="1aab8-197">이 자습서 시리즈의 뒷부분에 나오는 양식에서 새 동영상을 입력할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-197">Later in this tutorial series you'll create a page where you can enter new movies in a form.</span></span> <span data-ttu-id="1aab8-198">그러나 지금은 다음 페이지에 표시할 수 있는 몇 가지 예제 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-198">For now, however, you can add some example data that you can then display on a page.</span></span>

<span data-ttu-id="1aab8-199">에 **데이터베이스** 를 보여 주는 트리는 WebMatrix에서 작업 영역에서 *.sdf* 앞에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-199">In the **Database** workspace in WebMatrix, notice that there's a tree that shows you the *.sdf* file you created earlier.</span></span> <span data-ttu-id="1aab8-200">새 노드를 열고 *.sdf* 파일을 선택한 다음 엽니다는 **테이블** 노드.</span><span class="sxs-lookup"><span data-stu-id="1aab8-200">Open the node for your new *.sdf* file, and then open the **Tables** node.</span></span>

![동영상 테이블에 트리와 WebMatrix 데이터베이스 작업 영역](displaying-data/_static/image10.png)

<span data-ttu-id="1aab8-202">마우스 오른쪽 단추로 클릭는 **동영상** 노드를 선택한 후 **데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-202">Right-click the **Movies** node and then choose **Data**.</span></span> <span data-ttu-id="1aab8-203">WebMatrix에 대 한 데이터를 입력할 수 있는 열립니다는 *동영상* 테이블:</span><span class="sxs-lookup"><span data-stu-id="1aab8-203">WebMatrix opens a grid where you can enter data for the *Movies* table:</span></span>

![WebMatrix (비어 있음)에서 데이터베이스 항목 표](displaying-data/_static/image11.png)

<span data-ttu-id="1aab8-205">클릭는 **제목** 열 "때 해리 충족 Sally"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-205">Click the **Title** column and enter "When Harry Met Sally".</span></span> <span data-ttu-id="1aab8-206">이동의 **장르** 열 (Tab 키를 사용할 수 있음) "로맨틱 코미디"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-206">Move to the **Genre** column (you can use the Tab key) and enter "Romantic Comedy".</span></span> <span data-ttu-id="1aab8-207">이동 된 **연도** 열 "1989"를 입력 하 고:</span><span class="sxs-lookup"><span data-stu-id="1aab8-207">Move to the **Year** column and enter "1989":</span></span>

![WebMatrix에서 하나의 레코드와의 데이터베이스 항목 표](displaying-data/_static/image12.png)

<span data-ttu-id="1aab8-209">Enter 키를 누릅니다 및 WebMatrix 새 동영상을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-209">Press Enter, and WebMatrix saves the new movie.</span></span> <span data-ttu-id="1aab8-210">에 **ID** 열에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-210">Notice that the **ID** column has been filled in.</span></span>

![WebMatrix에서 하나의 레코드 및 자동 생성 된 ID의 데이터베이스 항목 표](displaying-data/_static/image13.png)

<span data-ttu-id="1aab8-212">다른 동영상 (예를 들어 "Gone와 the 바람", "드라마", "1939")을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-212">Enter another movie (for example, "Gone with the Wind", "Drama", "1939").</span></span> <span data-ttu-id="1aab8-213">ID 열에 다시 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-213">The ID column is filled in again:</span></span>

![두 개의 레코드를 자동으로 생성 된 Id와 WebMatrix에서 데이터베이스 항목 표](displaying-data/_static/image14.png)

<span data-ttu-id="1aab8-215">세 번째 동영상 (예를 들어 "Ghostbusters", "코미디")을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-215">Enter a third movie (for example, "Ghostbusters", "Comedy").</span></span> <span data-ttu-id="1aab8-216">시험 사용 하지는 **연도** 열 비워 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-216">As an experiment, leave the **Year** column blank and then press Enter.</span></span> <span data-ttu-id="1aab8-217">선택 취소 하기 때문에 **Null 허용** 옵션을 데이터베이스에 오류를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-217">Because you unselected the **Allow Nulls** option, the database shows an error:</span></span>

![필요한 열 값을 비워 두면 '잘못 된 데이터' 오류 표시](displaying-data/_static/image15.png)

<span data-ttu-id="1aab8-219">클릭 **확인** 를 다시 이동 (으로 1984 "Ghostbusters"에 대 한 연도) 항목을 해결 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-219">Click **OK** to go back and fix the entry (the year for "Ghostbusters" is 1984), and then press Enter.</span></span>

<span data-ttu-id="1aab8-220">8 구성할 때까지 또는 하므로 여러 영화를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-220">Fill in several movies until you have 8 or so.</span></span> <span data-ttu-id="1aab8-221">(8 입력 쉽게 나중 페이징 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-221">(Entering 8 makes it easier to work with paging later.</span></span> <span data-ttu-id="1aab8-222">그러나에 너무 많지는 않은지, 지금은 일부를 입력 합니다.) 실제 데이터가 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-222">But if that's too many, enter just a few for now.) The actual data doesn't matter.</span></span>

![어느 레코드와 WebMatrix에서 데이터베이스 항목 표](displaying-data/_static/image16.png)

<span data-ttu-id="1aab8-224">오류 없이 모든 동영상을 입력 한 경우에 ID 값은 순차적입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-224">If you entered all the movies without any errors, the ID values are sequential.</span></span> <span data-ttu-id="1aab8-225">영화 불완전 한 레코드를 저장 하 려 한 경우 해당 ID 번호가 순차적 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-225">If you tried to save an incomplete movie record, the ID numbers might not be sequential.</span></span> <span data-ttu-id="1aab8-226">그렇다면 하는 방법을 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-226">If so, that's okay.</span></span> <span data-ttu-id="1aab8-227">숫자 모든 고유한 의미가 없으며 중요 한 것은에서 고유 하 고 *동영상* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-227">The numbers don't have any inherent meaning, and the only thing that's important is that they're unique in the *Movies* table.</span></span>

<span data-ttu-id="1aab8-228">데이터베이스 디자이너에 포함 된 탭을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-228">Close the tab that contains the database designer.</span></span>

<span data-ttu-id="1aab8-229">이제 웹 페이지에서이 데이터를 표시 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-229">Now you can turn to displaying this data on a web page.</span></span>

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a><span data-ttu-id="1aab8-230">WebGrid 도우미를 사용 하 여 데이터 페이지에 표시</span><span class="sxs-lookup"><span data-stu-id="1aab8-230">Displaying Data in a Page by Using the WebGrid Helper</span></span>

<span data-ttu-id="1aab8-231">사용 하려는 데이터를 페이지에 표시 하려면는 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-231">To display data in a page, you're going to use the `WebGrid` helper.</span></span> <span data-ttu-id="1aab8-232">이 도우미 디스플레이 표 또는 테이블 (행과 열)를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-232">This helper produces a display in a grid or table (rows and columns).</span></span> <span data-ttu-id="1aab8-233">볼 수 있듯이 수 상세 표 서식 및 기타 기능을 통해 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-233">As you'll see, you'll be able refine the grid with formatting and other features.</span></span>

<span data-ttu-id="1aab8-234">눈금을 실행 하려면 몇 줄의 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-234">To run the grid, you'll have to write a few lines of code.</span></span> <span data-ttu-id="1aab8-235">이러한 몇 줄은 거의 모든이 자습서에서 수행 하는 데이터 액세스에 대 한 패턴의 한 종류로 역할 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-235">These few lines will serve as a kind of pattern for almost all of the data access that you do in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="1aab8-236">실제로; 페이지에서 데이터를 표시 하기 위한 여러 옵션을 사용할 수 `WebGrid` 도우미는 한 방법일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-236">You actually have many options for displaying data on a page; the `WebGrid` helper is just one.</span></span> <span data-ttu-id="1aab8-237">선택한 이유 것이 자습서에 대 한 데이터를 표시 하는 가장 쉬운 방법은 이므로 및은 상당히 유연 하기 때문에.</span><span class="sxs-lookup"><span data-stu-id="1aab8-237">We chose it for this tutorial because it's the easiest way to display data and because it's reasonably flexible.</span></span> <span data-ttu-id="1aab8-238">다음 자습서 집합 데이터를 표시 하는 방법 보다 직접적으로 제어를 제공 하는 페이지에서 데이터로 작업 하는 자세한 "수동"으로 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-238">In the next tutorial set, you'll see how to use a more "manual" way to work with data in the page, which gives you more direct control over how to display the data.</span></span>


<span data-ttu-id="1aab8-239">WebMatrix에서 왼쪽된 창에서 클릭 된 **파일** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-239">In the left pane in WebMatrix, click the **Files** workspace.</span></span>

<span data-ttu-id="1aab8-240">만든 새 데이터베이스는에 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-240">The new database you created is in the *App\_Data* folder.</span></span> <span data-ttu-id="1aab8-241">폴더가 이미 하지 않은 경우 WebMatrix에 새 데이터베이스에 대해 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-241">If the folder didn't already exist, WebMatrix created it for your new database.</span></span> <span data-ttu-id="1aab8-242">(폴더 존재 했을 수 이전에 설치한 것 도우미.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-242">(The folder might have existed if you'd previously installed helpers.)</span></span>

<span data-ttu-id="1aab8-243">트리 보기에서 웹 사이트의 루트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-243">In the tree view, select the root of the website.</span></span> <span data-ttu-id="1aab8-244">웹 사이트의 루트를 선택 해야 합니다. 그렇지 않으면 응용 프로그램에 새 파일 추가 수\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="1aab8-244">You must select the root of the website; otherwise, the new file might be added to the App\_Data folder.</span></span>

<span data-ttu-id="1aab8-245">리본 메뉴에서 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-245">In the ribbon, click **New**.</span></span> <span data-ttu-id="1aab8-246">에 **파일 유형을 선택** 상자 **CSHTML**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-246">In the **Choose a File Type** box, choose **CSHTML**.</span></span>

<span data-ttu-id="1aab8-247">에 **이름** 상자에서 새 페이지 "Movies.cshtml" 이름 지정:</span><span class="sxs-lookup"><span data-stu-id="1aab8-247">In the **Name** box, name the new page "Movies.cshtml":</span></span>

!['영화' 페이지를 보여 주는 '파일 유형을 선택 합니다.' 대화 상자](displaying-data/_static/image17.png)

<span data-ttu-id="1aab8-249">클릭는 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-249">Click the **OK** button.</span></span> <span data-ttu-id="1aab8-250">WebMatrix의 몇 가지 기본 요소가 있는 새 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-250">WebMatrix opens a new file with some skeleton elements in it.</span></span> <span data-ttu-id="1aab8-251">먼저 데이터베이스에서 데이터를 가져올 수 있는 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-251">First you'll write some code to go get the data from the database.</span></span> <span data-ttu-id="1aab8-252">그런 다음 실제로 데이터를 표시 하려면 페이지에 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-252">Then you'll add markup to the page to actually display the data.</span></span>

### <a name="writing-the-data-query-code"></a><span data-ttu-id="1aab8-253">데이터 쿼리 코드를 작성</span><span class="sxs-lookup"><span data-stu-id="1aab8-253">Writing the Data Query Code</span></span>

<span data-ttu-id="1aab8-254">페이지의 위쪽 사이 `@{` 및 `}` 문자를 다음 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-254">At the top of the page, between the `@{` and `}` characters, enter the following code.</span></span> <span data-ttu-id="1aab8-255">(여는 태그와 닫는 중괄호 사이의이 코드를 입력 하 고 있는지 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-255">(Make sure that you enter this code between the opening and closing braces.)</span></span>

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

<span data-ttu-id="1aab8-256">첫 번째 줄은은 항상 첫 번째 단계는 데이터베이스와 작업을 수행할 하기 전에 이전에 만든 데이터베이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-256">The first line opens the database that you created earlier, which is always the first step before doing something with the database.</span></span> <span data-ttu-id="1aab8-257">알려 고 `Database.Open` 열려는 데이터베이스의 메서드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-257">You tell the `Database.Open` method name of the database to open.</span></span> <span data-ttu-id="1aab8-258">포함 하지 않는 공지 *.sdf* 이름에서입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-258">Notice that you don't include *.sdf* in the name.</span></span> <span data-ttu-id="1aab8-259">`Open` 메서드 찾고 가정는 *.sdf* 파일 (즉, *WebPagesMovies.sdf*) 하 고는 *.sdf* 중인 파일의 *앱\_ 데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-259">The `Open` method assumes that it's looking for an *.sdf* file (that is, *WebPagesMovies.sdf*) and that the *.sdf* file is in the *App\_Data* folder.</span></span> <span data-ttu-id="1aab8-260">(앞서 설명한 하는 *앱\_데이터* 폴더 이름이 예약 됩니다;이 시나리오는 ASP.NET에서는 해당 이름에 대 한을 가정 하는 위치 중 하나입니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-260">(Earlier we noted that the *App\_Data* folder is reserved; this scenario is one of the places where ASP.NET makes assumptions about that name.)</span></span>

<span data-ttu-id="1aab8-261">에 대 한 참조 라는 변수가에 배치 되는 데이터베이스를 열 때 `db`합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-261">When the database is opened, a reference to it is put into the variable named `db`.</span></span> <span data-ttu-id="1aab8-262">(있는 이름을 지정할 수 있습니다 아무 것도 있습니다.) `db` 변수는 데이터베이스와의 상호 작용 방법 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-262">(Which could be named anything.) The `db` variable is how you'll end up interacting with the database.</span></span>

<span data-ttu-id="1aab8-263">두 번째 줄은 실제로 사용 하 여 데이터베이스 데이터를 인출는 `Query` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1aab8-263">The second line actually fetches the database data by using the `Query` method.</span></span> <span data-ttu-id="1aab8-264">이 코드의 작동 방식 확인:는 `db` 변수에 열린된 데이터베이스에 대 한 참조가 있고 호출할는 `Query` 메서드를 사용 하 여는 `db` 변수 (`db.Query`).</span><span class="sxs-lookup"><span data-stu-id="1aab8-264">Notice how this code works: the `db` variable has a reference to the opened database, and you invoke the `Query` method by using the `db` variable (`db.Query`).</span></span>

<span data-ttu-id="1aab8-265">쿼리 자체가 있는 SQL `Select` 문.</span><span class="sxs-lookup"><span data-stu-id="1aab8-265">The query itself is a SQL `Select` statement.</span></span> <span data-ttu-id="1aab8-266">(SQL에 대 한 약간의 배경 나중에 설명 참조). 문에서 `Movies` 쿼리에 테이블을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-266">(For a little background about SQL, see the explanation later.) In the statement, `Movies` identifies the table to query.</span></span> <span data-ttu-id="1aab8-267">`*` 문자 지정 하면 쿼리 테이블에서 모든 열을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-267">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="1aab8-268">(또한를 나열할 수 열 개별적으로 쉼표로 구분 하 여.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-268">(You could also list columns individually, separated by commas.)</span></span>

<span data-ttu-id="1aab8-269">쿼리 결과 있는 경우 반환 되며에서 사용할 수는 `selectedData` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-269">The results of the query, if any, are returned and made available in the `selectedData` variable.</span></span> <span data-ttu-id="1aab8-270">다시, 변수 이름을 지정할 수 있습니다 아무 것도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-270">Again, the variable could be named anything.</span></span>

<span data-ttu-id="1aab8-271">마지막으로, 세 번째 줄 asp의 인스턴스를 사용 하려면는 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-271">Finally, the third line tells ASP.NET that you want to use an instance of the `WebGrid` helper.</span></span> <span data-ttu-id="1aab8-272">만들 (*인스턴스화할*)를 사용 하 여 도우미 개체는 `new` 키워드를 통해 쿼리 결과 전달 하 고는 `selectedData` 변수 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-272">You create (*instantiate*) the helper object by using the `new` keyword and pass it the query results via the `selectedData` variable.</span></span> <span data-ttu-id="1aab8-273">새 `WebGrid` 개체는 데이터베이스 쿼리 결과 함께 사용할 수 있습니다는 `grid` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-273">The new `WebGrid` object, along with the results of the database query, are made available in the `grid` variable.</span></span> <span data-ttu-id="1aab8-274">실제로 페이지에서 데이터를 표시 하려면 잠시 후에 해당 결과 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-274">You'll need that result in a moment to actually display the data in the page.</span></span>

<span data-ttu-id="1aab8-275">이 단계에서는 데이터베이스 열린, 데이터 참조 준비한 하 고 원하는 `WebGrid` 도우미 해당 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-275">At this stage, the database has been opened, you've gotten the data you want, and you've prepared the `WebGrid` helper with that data.</span></span> <span data-ttu-id="1aab8-276">다음 페이지에서 태그를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-276">Next is to create the markup in the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="1aab8-277">**구조적된 쿼리 언어 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="1aab8-277">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="1aab8-278">SQL은 데이터베이스의에서 데이터를 관리 하기 위한 대부분의 관계형 데이터베이스에서 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-278">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="1aab8-279">데이터를 검색 하 고, 업데이트 하 고 만들고 수정 하 고 데이터베이스 테이블에 데이터를 관리 하도록 하는 명령이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-279">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage data in database tables.</span></span> <span data-ttu-id="1aab8-280">SQL는 프로그래밍 언어 (예: C#)와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-280">SQL is different than a programming language (like C#).</span></span> <span data-ttu-id="1aab8-281">Sql을 원하는 데이터베이스에 알립니다 며 데이터베이스의 작업 데이터를 가져오거나 작업을 수행 하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1aab8-281">With SQL, you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="1aab8-282">다음은 몇 가지 SQL 명령의 예로 및 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-282">Here are examples of some SQL commands and what they do:</span></span>
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="1aab8-283">첫 번째 `Select` 문의 모든 열을 가져옵니다 (지정 된 `*`)에서 *영화* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-283">The first `Select` statement gets all the columns (specified by `*`) from the *Movies* table.</span></span>
> 
> <span data-ttu-id="1aab8-284">두 번째 `Select` 의 레코드에서 ID, 이름 및 Price 열을 인출 하는 문을 *제품* Price 열 값은 10 개 이상의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-284">The second `Select` statement fetches the ID, Name, and Price columns from records in the *Product* table whose Price column value is more than 10.</span></span> <span data-ttu-id="1aab8-285">이 명령은 이름 열의 값에 따라 알파벳 순서로 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-285">The command returns the results in alphabetical order based on the values of the Name column.</span></span> <span data-ttu-id="1aab8-286">가격 조건과 일치 하는 레코드가 없는, 빈 집합이 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-286">If no records match the price criteria, the command returns an empty set.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> <span data-ttu-id="1aab8-287">이 명령은에 새 레코드를 삽입는 *제품* 테이블을 1.99를 "Croissant", "A 잘 끊어지는 기쁨" 위해 Description 열 및 가격을 이름 열을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-287">This command inserts a new record into the *Product* table, setting the Name column to "Croissant", the Description column to "A flaky delight", and the price to 1.99.</span></span>
> 
> <span data-ttu-id="1aab8-288">숫자가 아닌 값을 지정 하는 단일 따옴표 (하지 큰따옴표, C#에서 같이)에 값 포함을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-288">Notice that when you're specifying a non-numeric value, the value is enclosed in single quotation marks (not double quotation marks, as in C#).</span></span> <span data-ttu-id="1aab8-289">텍스트 또는 날짜 값 주위 하지만 숫자 주위 하지 이러한 따옴표를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-289">You use these quotation marks around text or date values, but not around numbers.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> <span data-ttu-id="1aab8-290">이 명령은에서 레코드를 삭제는 *제품* 테이블 열이 있는 만료 날짜는 2008 년 1 월 1 일 보다 이전입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-290">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="1aab8-291">(명령은 가정 하 고 *제품* 테이블에 이러한 열이 물론.) MM/DD/YYYY 형식으로 날짜를 여기서 입력 하지만 로캘에 사용 되는 형식으로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-291">(The command assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="1aab8-292">`Insert` 및 `Delete` 명령 결과 집합을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-292">The `Insert` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="1aab8-293">대신, 이러한 명령에 의해 영향을 받은 레코드 수를 알려 주는 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-293">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="1aab8-294">이러한 작업 (예: 레코드 삽입 및 삭제)의 일부에 대 한 작업을 요청 하는 프로세스는 데이터베이스에 대 한 적절 한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-294">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="1aab8-295">데이터베이스에 연결할 때 사용자 이름 및 암호를 제공 해야 하는 프로덕션 데이터베이스에 대 한 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-295">That's why for production databases you often have to supply a user name and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="1aab8-296">SQL 명령의 수십 있지만 위의 명령과 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-296">There are dozens of SQL commands, but they all follow a pattern like the commands you see here.</span></span> <span data-ttu-id="1aab8-297">SQL 명령을 사용 하 여 테이블을 만들고 데이터베이스, 테이블에서 레코드의 수를 계산, 가격을 계산 보다 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-297">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>


### <a name="adding-markup-to-display-the-data"></a><span data-ttu-id="1aab8-298">데이터를 표시 하는 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-298">Adding Markup to Display the Data</span></span>

<span data-ttu-id="1aab8-299">내에서 `<head>` 요소를 집합 내용의 `<title>` "영화" 요소:</span><span class="sxs-lookup"><span data-stu-id="1aab8-299">Inside the `<head>` element, set contents of the `<title>` element to "Movies":</span></span>

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

<span data-ttu-id="1aab8-300">내에서 `<body>` 페이지의 요소에 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-300">Inside the `<body>` element of the page, add the following:</span></span>

[!code-html[Main](displaying-data/samples/sample3.html)]

<span data-ttu-id="1aab8-301">이제</span><span class="sxs-lookup"><span data-stu-id="1aab8-301">That's it.</span></span> <span data-ttu-id="1aab8-302">`grid` 변수는 값을 만들 때 만든는 `WebGrid` 이전 코드에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-302">The `grid` variable is the value you created when you created the `WebGrid` object in code earlier.</span></span>

<span data-ttu-id="1aab8-303">WebMatrix 트리 보기에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **브라우저에서 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-303">In the WebMatrix tree view, right-click the page and select **Launch in browser**.</span></span> <span data-ttu-id="1aab8-304">이 페이지와 같은 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-304">You'll see something like this page:</span></span>

![영화 테이블에서 기본 WebGrid 도우미 출력](displaying-data/_static/image18.png)

<span data-ttu-id="1aab8-306">해당 열으로 정렬 하려면 열 머리글 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-306">Click a column heading link to sort by that column.</span></span> <span data-ttu-id="1aab8-307">에 기본 제공 되는 기능에는 머리글을 클릭 하 여 정렬할 수는 **WebGrid** 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-307">Being able to sort by clicking a heading is a feature that's built into the **WebGrid** helper.</span></span>

<span data-ttu-id="1aab8-308">`GetHtml` 메서드, 해당 이름에서 알 수 있듯이 생성 데이터를 표시 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-308">The `GetHtml` method, as its name suggests, generates markup that displays the data.</span></span> <span data-ttu-id="1aab8-309">기본적으로는 `GetHtml` 메서드는 HTML을 생성 `<table>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-309">By default, the `GetHtml` method generates an HTML `<table>` element.</span></span> <span data-ttu-id="1aab8-310">(원하는 경우 확인할 수 있습니다 렌더링 브라우저에서 페이지의 원본을 확인 하 여.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-310">(If you want, you can verify the rendering by looking at the source of the page in the browser.)</span></span>

## <a name="modifying-the-look-of-the-grid"></a><span data-ttu-id="1aab8-311">눈금의 모양 수정</span><span class="sxs-lookup"><span data-stu-id="1aab8-311">Modifying the Look of the Grid</span></span>

<span data-ttu-id="1aab8-312">사용 하 여는 `WebGrid` 도우미 방금 했던 것 처럼은 간단 하지만 일반 결과 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-312">Using the `WebGrid` helper like you just did is easy, but the resulting display is plain.</span></span> <span data-ttu-id="1aab8-313">`WebGrid` 도우미에는 데이터가 표시 되는 방식을 제어할 수 있는 모든 종류의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-313">The `WebGrid` helper has all sorts of options that let you control how the data is displayed.</span></span> <span data-ttu-id="1aab8-314">이 자습서에서는 탐색에 너무 많은 있지만이 섹션은 알 수 있습니다 이러한 옵션 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-314">There are far too many to explore in this tutorial, but this section will give you an idea of some of those options.</span></span> <span data-ttu-id="1aab8-315">이후의 자습서이 시리즈의 몇 가지 추가 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-315">A few additional options will be covered in later tutorials in this series.</span></span>

### <a name="specifying-individual-columns-to-display"></a><span data-ttu-id="1aab8-316">에 표시할 개별 열 지정</span><span class="sxs-lookup"><span data-stu-id="1aab8-316">Specifying Individual Columns to Display</span></span>

<span data-ttu-id="1aab8-317">를 시작 하려면 특정 열만 표시 되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-317">To start, you can specify that you want to display only certain columns.</span></span> <span data-ttu-id="1aab8-318">기본적으로 앞서 살펴본 것 처럼 표 형식으로 표시에서 열의 모든 4는 *동영상* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-318">By default, as you've seen, the grid shows all four of the columns from the *Movies* table.</span></span>

<span data-ttu-id="1aab8-319">에 *Movies.cshtml* 파일, 대체는 `@grid.GetHtml()` 다음 방금 추가한 태그:</span><span class="sxs-lookup"><span data-stu-id="1aab8-319">In the *Movies.cshtml* file, replace the `@grid.GetHtml()` markup that you just added with the following:</span></span>

[!code-css[Main](displaying-data/samples/sample4.css)]

<span data-ttu-id="1aab8-320">포함 된 도우미 표시할 열을 판단할 수는 `columns` 에 대 한 매개 변수는 `GetHtml` 메서드와 열 모음을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-320">To tell the helper which columns to display, you include a `columns` parameter for the `GetHtml` method and pass in a collection of columns.</span></span> <span data-ttu-id="1aab8-321">컬렉션에 포함 하도록 각 열을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-321">In the collection, you specify each column to include.</span></span> <span data-ttu-id="1aab8-322">포함 하 여 표시 하는 개별 열을 지정 하는 `grid.Column` 개체를 원하는 데이터 열 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-322">You specify an individual column to display by including a `grid.Column` object, and pass in the name of the data column you want.</span></span> <span data-ttu-id="1aab8-323">(이러한 열은 SQL 쿼리 결과에 포함 되어야 합니다-는 `WebGrid` 도우미 쿼리에 의해 반환 되지 않은 열을 표시할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="1aab8-323">(These columns must be included in the SQL query results — the `WebGrid` helper cannot display columns that were not returned by the query.)</span></span>

<span data-ttu-id="1aab8-324">시작 된 *Movies.cshtml* 다시 시간과이 다음과 같은 표시를 얻게 하 고 브라우저에서 페이지 (ID 열이 없는 표시 되는지 확인):</span><span class="sxs-lookup"><span data-stu-id="1aab8-324">Launch the *Movies.cshtml* page in the browser again, and this time you get a display like the following one (notice that no ID column is displayed):</span></span>

![선택 된 열만를 보여 주는 WebGrid 표시](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a><span data-ttu-id="1aab8-326">눈금의 모양 변경</span><span class="sxs-lookup"><span data-stu-id="1aab8-326">Changing the Look of the Grid</span></span>

<span data-ttu-id="1aab8-327">이 집합에서 이후의 자습서에 대해 알아봅니다 중 일부는 열을 표시 하기 위한 몇 가지 더 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-327">There are quite a few more options for displaying columns, some of which will be explored in later tutorials in this set.</span></span> <span data-ttu-id="1aab8-328">지금은이 섹션에서는를 소개 방법으로 전체 표 스타일 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-328">For now, this section will introduce you to ways in which you can style the grid as a whole.</span></span>

<span data-ttu-id="1aab8-329">내에서 `<head>` 닫기 바로 전에 페이지의 섹션 `</head>` 태그에 다음 추가 `<style>` 요소:</span><span class="sxs-lookup"><span data-stu-id="1aab8-329">Inside the `<head>` section of the page, just before the closing `</head>` tag, add the following `<style>` element:</span></span>

[!code-css[Main](displaying-data/samples/sample5.css)]

<span data-ttu-id="1aab8-330">이 CSS 태그가 라는 클래스를 정의 합니다. `grid`, `head`등입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-330">This CSS markup defines classes named `grid`, `head`, and so on.</span></span> <span data-ttu-id="1aab8-331">별도의 이러한 스타일 정의 빠뜨릴 수도 수 *.css* 파일을 하는 페이지에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-331">You could also put these style definitions in a separate *.css* file and link that to the page.</span></span> <span data-ttu-id="1aab8-332">(실제로 수행 합니다는이 자습서 집합의 뒷부분에 나오는.) 하지만이 자습서에 대 한 작업을 쉽게 하려면 내부 데이터를 표시 하는 동일한 페이지.</span><span class="sxs-lookup"><span data-stu-id="1aab8-332">(In fact, you'll do that later in this tutorial set.) But to make things easy for this tutorial, they're inside the same page that displays the data.</span></span>

<span data-ttu-id="1aab8-333">가져올 수 이제는 `WebGrid` 이러한 스타일 클래스를 사용 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-333">Now you can get the `WebGrid` helper to use these style classes.</span></span> <span data-ttu-id="1aab8-334">도우미에 다양 한 속성 (예를 들어 `tableStyle`)이를 위해서는-CSS 스타일 클래스 이름을 할당 하 고 클래스 이름을 해당 도우미에서 렌더링 되는 태그의 일부로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-334">The helper has a number of properties (for example, `tableStyle`) for just this purpose — you assign a CSS style class name to them, and that class name is rendered as part of the markup that's rendered by the helper.</span></span>

<span data-ttu-id="1aab8-335">변경 된 `grid.GetHtml` 태그를 다음과 같이이 코드 이제 표시:</span><span class="sxs-lookup"><span data-stu-id="1aab8-335">Change the `grid.GetHtml` markup so that it now looks like this code:</span></span>

[!code-css[Main](displaying-data/samples/sample6.css)]

<span data-ttu-id="1aab8-336">기능 추가 되었으며 사용자가 추가한 `tableStyle`, `headerStyle`, 및 `alternatingRowStyle` 매개 변수를는 `GetHtml` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1aab8-336">What's new here is that you've added `tableStyle`, `headerStyle`, and `alternatingRowStyle` parameters to the `GetHtml` method.</span></span> <span data-ttu-id="1aab8-337">이러한 매개 변수 조금 전에 추가 된 CSS 스타일의 이름으로 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-337">These parameters have been set to the names of the CSS styles that you added a moment ago.</span></span>

<span data-ttu-id="1aab8-338">페이지를 실행 하 고이 시간 보면 다음과 이전 보다 훨씬 적은 일반 눈금:</span><span class="sxs-lookup"><span data-stu-id="1aab8-338">Run the page, and this time you see a grid that looks much less plain than before:</span></span>

![CSS 클래스 이름으로 설정 하는 매개 변수가 포함 된 WebGrid 표시](displaying-data/_static/image20.png)

<span data-ttu-id="1aab8-340">확인할 수는 `GetHtml` 생성 된 메서드를 볼 수 있습니다는 브라우저에서 페이지의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-340">To see what the `GetHtml` method generated, you can look at the source of the page in the browser.</span></span> <span data-ttu-id="1aab8-341">여기에서 세부 정보 모드에 있지만 중요 한 점은 같은 매개 변수를 지정 하 여 `tableStyle`, 다음과 같은 HTML 태그를 생성할 눈금을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-341">We won't go into detail here, but the important point is that by specifying parameters like `tableStyle`, you caused the grid to generate HTML tags like the following:</span></span>

`<table class="grid">`

<span data-ttu-id="1aab8-342">`<table>` 태그에는 `class` 이전에 추가한 CSS 규칙 중 하나를 참조 하는 특성이 여기에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-342">The `<table>` tag has had a `class` attribute added to it that references one of the CSS rules that you added earlier.</span></span> <span data-ttu-id="1aab8-343">이 코드는 기본 패턴을 보여 줍니다 &mdash; 에 대 한 다른 매개 변수는 `GetHtml` 메서드 사용된 하면 참조 CSS 클래스 메서드는 태그와 함께 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-343">This code shows you the basic pattern &mdash; different parameters for the `GetHtml` method let you reference CSS classes that the method then generates along with the markup.</span></span> <span data-ttu-id="1aab8-344">CSS 클래스를 통해 수행할 작업은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-344">What you do with the CSS classes is up to you.</span></span>

## <a name="adding-paging"></a><span data-ttu-id="1aab8-345">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="1aab8-345">Adding Paging</span></span>

<span data-ttu-id="1aab8-346">이 자습서에 대 한 마지막 작업으로 페이징 표에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-346">As the last task for this tutorial, you'll add paging to the grid.</span></span> <span data-ttu-id="1aab8-347">지금은 모든 동영상을 한 번에 표시할 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-347">Right now it's no problem to display all your movies at once.</span></span> <span data-ttu-id="1aab8-348">하지만 페이지 표시 긴 대기줄 수백 영화를 추가한 경우.</span><span class="sxs-lookup"><span data-stu-id="1aab8-348">But if you added hundreds of movies, the page display would get long.</span></span>

<span data-ttu-id="1aab8-349">페이지 코드에서 만드는 줄 변경는 `WebGrid` 다음 코드를 개체:</span><span class="sxs-lookup"><span data-stu-id="1aab8-349">In the page code, change the line that creates the `WebGrid` object to the following code:</span></span>

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

<span data-ttu-id="1aab8-350">앞에서 유일한 차이점은 사용자가 추가한는 `rowsPerPage` 3으로 설정 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-350">The only difference from before is that you've added a `rowsPerPage` parameter that's set to 3.</span></span>

<span data-ttu-id="1aab8-351">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-351">Run the page.</span></span> <span data-ttu-id="1aab8-352">눈금에는 시간을 더한 데이터베이스에서 동영상 페이징할 수 있는 탐색 링크에 3 행 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-352">The grid displays 3 rows at a time, plus navigation links that let you page through the movies in your database:</span></span>

![페이징 사용 하 여 WebGrid 디스플레이](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a><span data-ttu-id="1aab8-354">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="1aab8-354">Coming Up Next</span></span>

<span data-ttu-id="1aab8-355">다음 자습서에서는 양식에서 사용자 입력을 얻으려고 Razor 및 C# 코드를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-355">In the next tutorial, you'll learn how to use Razor and C# code to get user input in a form.</span></span> <span data-ttu-id="1aab8-356">제목 또는 장르의 영화를 찾을 수 있도록 동영상 페이지에는 검색 상자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aab8-356">You'll add a search box to the Movies page so that you can find movies by title or genre.</span></span>

## <a name="complete-listing-for-movies-page"></a><span data-ttu-id="1aab8-357">동영상 페이지에 대 한 전체 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="1aab8-357">Complete Listing for Movies Page</span></span>

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="1aab8-358">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1aab8-358">Additional Resources</span></span>

- [<span data-ttu-id="1aab8-359">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="1aab8-359">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)

>[!div class="step-by-step"]
<span data-ttu-id="1aab8-360">[이전](intro-to-web-pages-programming.md)
[다음](form-basics.md)</span><span class="sxs-lookup"><span data-stu-id="1aab8-360">[Previous](intro-to-web-pages-programming.md)
[Next](form-basics.md)</span></span>
