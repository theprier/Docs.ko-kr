---
uid: web-pages/overview/data/5-working-with-data
title: Asp.net에서 데이터베이스를 사용 하 여 작업 소개 페이지 (Razor) 사이트 | Microsoft Docs
author: Rick-Anderson
description: 데이터베이스에서 데이터에 액세스 하 여 ASP.NET 웹 페이지를 사용 하 여 표시 하는 방법을 설명이 합니다.
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: a688761c87376aa93463c13eaa07858d3acb9dc2
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021692"
---
<a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="2c947-103">Asp.net에서 데이터베이스를 사용 하 여 작업 소개 페이지 (Razor) 사이트</span><span class="sxs-lookup"><span data-stu-id="2c947-103">Introduction to Working with a Database in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="2c947-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2c947-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="2c947-105">이 문서는 ASP.NET Web Pages (Razor) 웹 사이트에서 데이터베이스를 만들려면 Microsoft WebMatrix 도구를 사용 하는 방법 및 표시, 추가, 편집 및 데이터를 삭제할 수 있는 페이지를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-105">This article describes how to use Microsoft WebMatrix tools to create a database in an ASP.NET Web Pages (Razor) website, and how to create pages that let you display, add, edit, and delete data.</span></span>
> 
> <span data-ttu-id="2c947-106">**학습할 내용:**</span><span class="sxs-lookup"><span data-stu-id="2c947-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="2c947-107">데이터베이스를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-107">How to create a database.</span></span>
> - <span data-ttu-id="2c947-108">데이터베이스에 연결 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-108">How to connect to a database.</span></span>
> - <span data-ttu-id="2c947-109">웹 페이지에서 데이터를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-109">How to display data in a web page.</span></span>
> - <span data-ttu-id="2c947-110">삽입, 업데이트 및 데이터베이스 레코드를 삭제 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="2c947-110">How to insert, update, and delete database records.</span></span>
> 
> <span data-ttu-id="2c947-111">다음은 문서에 도입 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-111">These are the features introduced in the article:</span></span>
> 
> - <span data-ttu-id="2c947-112">Microsoft SQL Server Compact Edition 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-112">Working with a Microsoft SQL Server Compact Edition database.</span></span>
> - <span data-ttu-id="2c947-113">SQL 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-113">Working with SQL queries.</span></span>
> - <span data-ttu-id="2c947-114">`Database` 클래스</span><span class="sxs-lookup"><span data-stu-id="2c947-114">The `Database` class.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2c947-115">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2c947-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="2c947-116">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="2c947-116">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="2c947-117">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="2c947-117">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="2c947-118">이 자습서 에서도 WebMatrix 3를 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-118">This tutorial also works with WebMatrix 3.</span></span> <span data-ttu-id="2c947-119">ASP.NET 웹 페이지 3 및 Visual Studio 2013 (또는 Visual Studio Express 2013 for Web)를 사용할 수 있습니다. 그러나 사용자 인터페이스는 이와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-119">You can use ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web); however, the user interface will be different.</span></span>


## <a name="introduction-to-databases"></a><span data-ttu-id="2c947-120">데이터베이스에 대 한 소개</span><span class="sxs-lookup"><span data-stu-id="2c947-120">Introduction to Databases</span></span>

<span data-ttu-id="2c947-121">일반적인 주소록을 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-121">Imagine a typical address book.</span></span> <span data-ttu-id="2c947-122">주소록의 각 항목에 대 한 (즉, 각 사용자에 대 한) 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 일부 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-122">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

<span data-ttu-id="2c947-123">다음과 같은 그림이 데이터 행과 열이 있는 테이블로 일반적인 방법은입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-123">A typical way to picture data like this is as a table with rows and columns.</span></span> <span data-ttu-id="2c947-124">데이터베이스 용어에서 각 행은 라고도 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-124">In database terms, each row is often referred to as a record.</span></span> <span data-ttu-id="2c947-125">(필드 라고도 함) 각 열 데이터의 각 형식에 대 한 값을 포함 합니다: 이름, 이름, 성 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-125">Each column (sometimes referred to as fields) contains a value for each type of data: first name, last name, and so on.</span></span>

| <span data-ttu-id="2c947-126">**ID**</span><span class="sxs-lookup"><span data-stu-id="2c947-126">**ID**</span></span> | <span data-ttu-id="2c947-127">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="2c947-127">**FirstName**</span></span> | <span data-ttu-id="2c947-128">**LastName**</span><span class="sxs-lookup"><span data-stu-id="2c947-128">**LastName**</span></span> | <span data-ttu-id="2c947-129">**주소**</span><span class="sxs-lookup"><span data-stu-id="2c947-129">**Address**</span></span> | <span data-ttu-id="2c947-130">**이메일**</span><span class="sxs-lookup"><span data-stu-id="2c947-130">**Email**</span></span> | <span data-ttu-id="2c947-131">**전화**</span><span class="sxs-lookup"><span data-stu-id="2c947-131">**Phone**</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2c947-132">1</span><span class="sxs-lookup"><span data-stu-id="2c947-132">1</span></span> | <span data-ttu-id="2c947-133">Jim</span><span class="sxs-lookup"><span data-stu-id="2c947-133">Jim</span></span> | <span data-ttu-id="2c947-134">Abrus</span><span class="sxs-lookup"><span data-stu-id="2c947-134">Abrus</span></span> | <span data-ttu-id="2c947-135">210 100 St SE Orcas 98031 WA</span><span class="sxs-lookup"><span data-stu-id="2c947-135">210 100th St SE Orcas WA 98031</span></span> | jim@contoso.com | <span data-ttu-id="2c947-136">555 0100</span><span class="sxs-lookup"><span data-stu-id="2c947-136">555 0100</span></span> |
| <span data-ttu-id="2c947-137">2</span><span class="sxs-lookup"><span data-stu-id="2c947-137">2</span></span> | <span data-ttu-id="2c947-138">Terry</span><span class="sxs-lookup"><span data-stu-id="2c947-138">Terry</span></span> | <span data-ttu-id="2c947-139">Adams</span><span class="sxs-lookup"><span data-stu-id="2c947-139">Adams</span></span> | <span data-ttu-id="2c947-140">1234 Main St. 시애틀 WA 99011</span><span class="sxs-lookup"><span data-stu-id="2c947-140">1234 Main St. Seattle WA 99011</span></span> | terry@cohowinery.com | <span data-ttu-id="2c947-141">555 0101</span><span class="sxs-lookup"><span data-stu-id="2c947-141">555 0101</span></span> |

<span data-ttu-id="2c947-142">대부분의 데이터베이스 테이블에 대 한 테이블에 고객 번호, 계좌 번호 등과 같은 고유 식별자가 포함 된 열을 있어야 합니다. 이 테이블의 이라고 *기본 키*을 및 테이블의 각 행을 식별 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-142">For most database tables, the table has to have a column that contains a unique identifier, like a customer number, account number, etc. This is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="2c947-143">예제에서는 ID 열이 주소록에 대 한 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-143">In the example, the ID column is the primary key for the address book.</span></span>

<span data-ttu-id="2c947-144">이 기본 데이터베이스의 개념을 이해 한 준비가 단순한 데이터베이스를 만들고 추가, 수정 및 삭제와 같은 작업을 수행 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-144">With this basic understanding of databases, you're ready to learn how to create a simple database and perform operations such as adding, modifying, and deleting data.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="2c947-145">**관계형 데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="2c947-145">**Relational Databases**</span></span>
> 
> <span data-ttu-id="2c947-146">다 수의 스프레드시트 및 텍스트 파일 등의 방법으로 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-146">You can store data in lots of ways, including text files and spreadsheets.</span></span> <span data-ttu-id="2c947-147">그러나 대부분의 비즈니스 용도로 데이터는 관계형 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-147">For most business uses, though, data is stored in a relational database.</span></span>
> 
> <span data-ttu-id="2c947-148">이 문서에서는 데이터베이스에 무척 깊게 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-148">This article doesn't go very deeply into databases.</span></span> <span data-ttu-id="2c947-149">그러나 수 찾게에 대 한 이해 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-149">However, you might find it useful to understand a little about them.</span></span> <span data-ttu-id="2c947-150">관계형 데이터베이스에서 정보를 별도 테이블에 논리적으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-150">In a relational database, information is logically divided into separate tables.</span></span> <span data-ttu-id="2c947-151">예를 들어, 학교에 대 한 데이터베이스 수업 및 학생에 대 한 별도 테이블을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-151">For example, a database for a school might contain separate tables for students and for class offerings.</span></span> <span data-ttu-id="2c947-152">데이터베이스 (예: SQL Server) 소프트웨어에서 지 원하는 강력한 명령을 수 있도록 동적으로 테이블 간의 관계를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-152">The database software (such as SQL Server) supports powerful commands that let you dynamically establish relationships between the tables.</span></span> <span data-ttu-id="2c947-153">예를 들어, 일정을 만들려면 학생 및 수업 간의 논리적 관계를 설정 하는 관계형 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-153">For example, you can use the relational database to establish a logical relationship between students and classes in order to create a schedule.</span></span> <span data-ttu-id="2c947-154">별도 테이블에 데이터를 저장할 테이블 구조의 복잡성이 줄어들고 테이블에 중복 데이터를 보관할 필요가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-154">Storing data in separate tables reduces the complexity of the table structure and reduces the need to keep redundant data in tables.</span></span>


## <a name="creating-a-database"></a><span data-ttu-id="2c947-155">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="2c947-155">Creating a Database</span></span>

<span data-ttu-id="2c947-156">이 절차를 WebMatrix에 포함 된 SQL Server Compact 데이터베이스 디자인 도구를 사용 하 여 SmallBakery 라는 데이터베이스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-156">This procedure shows you how to create a database named SmallBakery by using the SQL Server Compact Database design tool that's included in WebMatrix.</span></span> <span data-ttu-id="2c947-157">코드를 사용 하 여 데이터베이스를 만들 수 있지만 더 일반적인 데이터베이스 및 WebMatrix와 같은 디자인 도구를 사용 하 여 데이터베이스 테이블을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-157">Although you can create a database using code, it's more typical to create the database and database tables using a design tool like WebMatrix.</span></span>

1. <span data-ttu-id="2c947-158">WebMatrix를 시작 하 고 빠른 시작 페이지에서 클릭 **사이트에서 템플릿을**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-158">Start WebMatrix, and on the Quick Start page, click **Site From Template**.</span></span>
2. <span data-ttu-id="2c947-159">선택 **빈 사이트**, 및는 **사이트 이름** 상자에 "SmallBakery"를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-159">Select **Empty Site**, and in the **Site Name** box enter "SmallBakery" and then click **OK**.</span></span> <span data-ttu-id="2c947-160">사이트 생성 되어 WebMatrix에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-160">The site is created and displayed in WebMatrix.</span></span>
3. <span data-ttu-id="2c947-161">왼쪽된 창에서 클릭 합니다 **데이터베이스** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-161">In the left pane, click the **Databases** workspace.</span></span>
4. <span data-ttu-id="2c947-162">리본 메뉴에서 클릭 **새 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-162">In the ribbon, click **New Database**.</span></span> <span data-ttu-id="2c947-163">빈 데이터베이스는 사이트와 동일한 이름을 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-163">An empty database is created with the same name as your site.</span></span>
5. <span data-ttu-id="2c947-164">왼쪽된 창에서를 확장 합니다 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-164">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
6. <span data-ttu-id="2c947-165">리본 메뉴에서 클릭 **새 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-165">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="2c947-166">WebMatrix는 테이블 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-166">WebMatrix opens the table designer.</span></span>

    ![[이미지]](5-working-with-data/_static/image1.jpg)
7. <span data-ttu-id="2c947-168">클릭 합니다 **이름** 열 enter &quot;Id&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-168">Click in the **Name** column and enter &quot;Id&quot;.</span></span>
8. <span data-ttu-id="2c947-169">에 **데이터 형식** 열 선택 **int**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-169">In the **Data Type** column, select **int**.</span></span>
9. <span data-ttu-id="2c947-170">설정 합니다 **기본 키가?** 하 고 **식별 됩니다?** 옵션을 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-170">Set the **Is Primary Key?** and **Is Identify?** options to **Yes**.</span></span>

    <span data-ttu-id="2c947-171">이름에서 알 수 있듯이 **기본 키가** 이 되도록 테이블의 기본 키를 데이터베이스에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-171">As the name suggests, **Is Primary Key** tells the database that this will be the table's primary key.</span></span> <span data-ttu-id="2c947-172">**Id가** 자동으로 모든 새 레코드에 대 한 ID 번호를 만들려면 다음 일련 번호 (1부터 시작)을 할당 하는 데이터베이스를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-172">**Is Identity** tells the database to automatically create an ID number for every new record and to assign it the next sequential number (starting at 1).</span></span>
10. <span data-ttu-id="2c947-173">다음 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-173">Click in the next row.</span></span> <span data-ttu-id="2c947-174">편집기에는 새 열 정의 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-174">The editor starts a new column definition.</span></span>
11. <span data-ttu-id="2c947-175">이름 값에 대 한 입력 &quot;이름을&quot;입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-175">For the Name value, enter &quot;Name&quot;.</span></span>
12. <span data-ttu-id="2c947-176">에 대 한 **데이터 형식**, 선택 &quot;nvarchar&quot; 길이 50으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-176">For **Data Type**, choose &quot;nvarchar&quot; and set the length to 50.</span></span> <span data-ttu-id="2c947-177">합니다 *var* 의 일부로 `nvarchar` 지시 데이터베이스는이 열에 대 한 데이터는 문자열일 크기가 레코드에서 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-177">The *var* part of `nvarchar` tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="2c947-178">(합니다 *n* 나타내는 접두사 *national*필드는 알파벳을 나타내는 문자 데이터를 보유할 수를 나타내는, 쓰기 시스템 &#8212; 즉, 필드가 갖는 유니코드 데이터는.)</span><span class="sxs-lookup"><span data-stu-id="2c947-178">(The *n* prefix represents *national*, indicating that the field can hold character data that represents any alphabet or writing system &#8212; that is, that the field holds Unicode data.)</span></span>
13. <span data-ttu-id="2c947-179">설정 된 **Null 허용** 옵션을 **No**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-179">Set the **Allow Nulls** option to **No**.</span></span> <span data-ttu-id="2c947-180">이 적용 됩니다는 *이름을* 열은 비워 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-180">This will enforce that the *Name* column is not left blank.</span></span>
14. <span data-ttu-id="2c947-181">라는 열이 동일한 프로세스를 사용 하 여 만들 *설명을*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-181">Using this same process, create a column named *Description*.</span></span> <span data-ttu-id="2c947-182">설정할 **데이터 형식** "nvarchar"를 길이 및 설정에 대 한 50 **Null 허용** 를 false로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-182">Set **Data Type** to "nvarchar" and 50 for the length, and set **Allow Nulls** to false.</span></span>
15. <span data-ttu-id="2c947-183">명명 된 열을 만듭니다 *가격*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-183">Create a column named *Price*.</span></span> <span data-ttu-id="2c947-184">설정할 **"money" 데이터 형식의** 설정 **Null 허용** 를 false로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-184">Set **Data Type to "money"** and set **Allow Nulls** to false.</span></span>
16. <span data-ttu-id="2c947-185">맨 위에 있는 상자에서 테이블의 이름을 &quot;제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-185">In the box at the top, name the table &quot;Product&quot;.</span></span>

    <span data-ttu-id="2c947-186">완료 되 면 정의 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-186">When you're done, the definition will look like this:</span></span>

    ![[이미지]](5-working-with-data/_static/image2.jpg)
17. <span data-ttu-id="2c947-188">테이블을 저장 하려면 Ctrl + S를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-188">Press Ctrl+S to save the table.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="2c947-189">데이터베이스에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="2c947-189">Adding Data to the Database</span></span>

<span data-ttu-id="2c947-190">이제 문서의 뒷부분에서 작업할 수 있는 데이터베이스에 몇 가지 샘플 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-190">Now you can add some sample data to your database that you'll work with later in the article.</span></span>

1. <span data-ttu-id="2c947-191">왼쪽된 창에서를 확장 합니다 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-191">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
2. <span data-ttu-id="2c947-192">Product 테이블을 마우스 오른쪽 단추로 누른 **데이터**입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-192">Right-click the Product table and then click **Data**.</span></span>
3. <span data-ttu-id="2c947-193">편집 창에서 다음 레코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-193">In the edit pane, enter the following records:</span></span>

    | <span data-ttu-id="2c947-194">**이름**</span><span class="sxs-lookup"><span data-stu-id="2c947-194">**Name**</span></span> | <span data-ttu-id="2c947-195">**설명**</span><span class="sxs-lookup"><span data-stu-id="2c947-195">**Description**</span></span> | <span data-ttu-id="2c947-196">**가격**</span><span class="sxs-lookup"><span data-stu-id="2c947-196">**Price**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="2c947-197">이동</span><span class="sxs-lookup"><span data-stu-id="2c947-197">Bread</span></span> | <span data-ttu-id="2c947-198">구운된 새로 매일입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-198">Baked fresh every day.</span></span> | <span data-ttu-id="2c947-199">2.99</span><span class="sxs-lookup"><span data-stu-id="2c947-199">2.99</span></span> |
    | <span data-ttu-id="2c947-200">Strawberry Shortcake</span><span class="sxs-lookup"><span data-stu-id="2c947-200">Strawberry Shortcake</span></span> | <span data-ttu-id="2c947-201">우리의 가든에서 유기적 딸기를 사용 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-201">Made with organic strawberries from our garden.</span></span> | <span data-ttu-id="2c947-202">9.99</span><span class="sxs-lookup"><span data-stu-id="2c947-202">9.99</span></span> |
    | <span data-ttu-id="2c947-203">Apple 원형</span><span class="sxs-lookup"><span data-stu-id="2c947-203">Apple Pie</span></span> | <span data-ttu-id="2c947-204">Mom의 원형에만 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-204">Second only to your mom's pie.</span></span> | <span data-ttu-id="2c947-205">12.99</span><span class="sxs-lookup"><span data-stu-id="2c947-205">12.99</span></span> |
    | <span data-ttu-id="2c947-206">Pecan 원형</span><span class="sxs-lookup"><span data-stu-id="2c947-206">Pecan Pie</span></span> | <span data-ttu-id="2c947-207">Pecans을 원하는 경우이 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-207">If you like pecans, this is for you.</span></span> | <span data-ttu-id="2c947-208">10.99</span><span class="sxs-lookup"><span data-stu-id="2c947-208">10.99</span></span> |
    | <span data-ttu-id="2c947-209">레몬 원형</span><span class="sxs-lookup"><span data-stu-id="2c947-209">Lemon Pie</span></span> | <span data-ttu-id="2c947-210">전 세계에서 최상의 lemons를 사용 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-210">Made with the best lemons in the world.</span></span> | <span data-ttu-id="2c947-211">11.99</span><span class="sxs-lookup"><span data-stu-id="2c947-211">11.99</span></span> |
    | <span data-ttu-id="2c947-212">Cupcakes</span><span class="sxs-lookup"><span data-stu-id="2c947-212">Cupcakes</span></span> | <span data-ttu-id="2c947-213">자녀가 및에서 kid 이러한 선호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-213">Your kids and the kid in you will love these.</span></span> | <span data-ttu-id="2c947-214">7.99</span><span class="sxs-lookup"><span data-stu-id="2c947-214">7.99</span></span> |

    <span data-ttu-id="2c947-215">에 아무 것도 입력할 필요가 있는지를 기억 합니다 *Id* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-215">Remember that you don't have to enter anything for the *Id* column.</span></span> <span data-ttu-id="2c947-216">만들 때 합니다 *Id* 설정한 열을 해당 **Id** 속성을 true로 자동으로 채울 수를 발생 시키는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-216">When you created the *Id* column, you set its **Is Identity** property to true, which causes it to automatically be filled in.</span></span>

    <span data-ttu-id="2c947-217">데이터 입력 완료 하면 테이블 디자이너는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-217">When you're finished entering the data, the table designer will look like this:</span></span>

    ![[이미지]](5-working-with-data/_static/image3.jpg)
4. <span data-ttu-id="2c947-219">데이터베이스 데이터를 포함 하는 탭을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-219">Close the tab that contains the database data.</span></span>

## <a name="displaying-data-from-a-database"></a><span data-ttu-id="2c947-220">데이터베이스에서 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-220">Displaying Data from a Database</span></span>

<span data-ttu-id="2c947-221">가져온 후 데이터를 사용 하 여 데이터베이스에서 ASP.NET 웹 페이지에서 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-221">Once you've got a database with data in it, you can display the data in an ASP.NET web page.</span></span> <span data-ttu-id="2c947-222">표시할 테이블 행을 선택 하려면 데이터베이스에 전달 하는 명령에는 SQL 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-222">To select the table rows to display, you use a SQL statement, which is a command that you pass to the database.</span></span>

1. <span data-ttu-id="2c947-223">왼쪽된 창에서 클릭 합니다 **파일** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-223">In the left pane, click the **Files** workspace.</span></span>
2. <span data-ttu-id="2c947-224">웹 사이트의 루트에서 이라는 새 CSHTML 페이지를 만듭니다 *ListProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-224">In the root of the website, create a new CSHTML page named *ListProducts.cshtml*.</span></span>
3. <span data-ttu-id="2c947-225">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-225">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    <span data-ttu-id="2c947-226">첫 번째 코드 블록에서 엽니다는 *SmallBakery.sdf* 앞에서 만든 파일 (데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="2c947-226">In the first code block, you open the *SmallBakery.sdf* file (database) that you created earlier.</span></span> <span data-ttu-id="2c947-227">`Database.Open` 가정 메서드는 *.sdf* 웹 사이트의 파일은 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-227">The `Database.Open` method assumes that the *.sdf* file is in your website's *App\_Data* folder.</span></span> <span data-ttu-id="2c947-228">(지정할 필요가 없습니다는 *.sdf* 확장 &#8212; 사실 경우는 `Open` 메서드가 작동 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="2c947-228">(Notice that you don't need to specify the *.sdf* extension &#8212; in fact, if you do, the `Open` method won't work.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c947-229">합니다 *앱\_데이터* 폴더는 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-229">The *App\_Data* folder is a special folder in ASP.NET that's used to store data files.</span></span> <span data-ttu-id="2c947-230">자세한 내용은 [데이터베이스에 연결할](#SB_ConnectingToADatabase) 이 문서의 뒷부분에 나오는.</span><span class="sxs-lookup"><span data-stu-id="2c947-230">For more information, see [Connecting to a Database](#SB_ConnectingToADatabase) later in this article.</span></span>

    <span data-ttu-id="2c947-231">그런 다음 다음 SQL을 사용 하 여 데이터베이스를 쿼리 하는 요청을 만드는 `Select` 문:</span><span class="sxs-lookup"><span data-stu-id="2c947-231">You then make a request to query the database using the following SQL `Select` statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    <span data-ttu-id="2c947-232">문에서 `Product` 쿼리 테이블을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-232">In the statement, `Product` identifies the table to query.</span></span> <span data-ttu-id="2c947-233">`*` 문자 쿼리가 테이블에서 모든 열을 반환 해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-233">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="2c947-234">(또한를 나열할 수 열을 개별적으로 열 중 일부만 참조 하려는 경우 쉼표로 구분 된.) `Order By` 절은 데이터를 정렬 해야 하는 방법을 나타냅니다 &#8212; 하 여이 경우에 *이름* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-234">(You could also list columns individually, separated by commas, if you wanted to see only some of the columns.) The `Order By` clause indicates how the data should be sorted &#8212; in this case, by the *Name* column.</span></span> <span data-ttu-id="2c947-235">즉, 데이터의 값을 기준으로 사전순으로 정렬 하는 *이름을* 각 행에 대 한 열입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-235">This means that the data is sorted alphabetically based on the value of the *Name* column for each row.</span></span>

    <span data-ttu-id="2c947-236">페이지의 본문에서 태그 데이터를 표시 하는 데 사용할 수 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-236">In the body of the page, the markup creates an HTML table that will be used to display the data.</span></span> <span data-ttu-id="2c947-237">내부를 `<tbody>` 요소를 사용할를 `foreach` 루프를 개별적으로 쿼리에서 반환 되는 각 데이터 행을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-237">Inside the `<tbody>` element, you use a `foreach` loop to individually get each data row that's returned by the query.</span></span> <span data-ttu-id="2c947-238">HTML 테이블 행을 각 데이터 행에 대해 만든 (`<tr>` 요소).</span><span class="sxs-lookup"><span data-stu-id="2c947-238">For each data row, you create an HTML table row (`<tr>` element).</span></span> <span data-ttu-id="2c947-239">HTML 테이블 셀을 만든 다음 (`<td>` 요소) 각 열에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-239">Then you create HTML table cells (`<td>` elements) for each column.</span></span> <span data-ttu-id="2c947-240">루프를 계속 실행 될 때마다 데이터베이스에서 사용 가능한 다음 행은는 `row` 변수 (이에서 설정한는 `foreach` 문).</span><span class="sxs-lookup"><span data-stu-id="2c947-240">Each time you go through the loop, the next available row from the database is in the `row` variable (you set this up in the `foreach` statement).</span></span> <span data-ttu-id="2c947-241">사용할 수는 행의 개별 열을 가져오려고 `row.Name` 또는 `row.Description` 또는 원하는 무엇이 든 이름 열입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-241">To get an individual column from the row, you can use `row.Name` or `row.Description` or whatever the name is of the column you want.</span></span>
4. <span data-ttu-id="2c947-242">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-242">Run the page in a browser.</span></span> <span data-ttu-id="2c947-243">(페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 페이지에는 다음과 같은 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-243">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays a list like the following:</span></span>

    ![[이미지]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="2c947-245">**구조적된 쿼리 언어 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="2c947-245">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="2c947-246">SQL은 데이터베이스에서 데이터를 관리 하는 것에 대 한 대부분의 관계형 데이터베이스에 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-246">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="2c947-247">데이터를 검색 하 고 업데이트 하 고 만들기, 수정 및 데이터베이스 테이블을 관리 하도록 하는 명령을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-247">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage database tables.</span></span> <span data-ttu-id="2c947-248">SQL 프로그래밍 언어 (예: WebMatrix에서 사용 하는 것)에 대해 다릅니다. 이므로 sql 개념 원하는 데이터베이스에 알립니다 하는 것은 데이터베이스의 데이터를 가져오는 작업을 수행 하는 방법을 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-248">SQL is different than a programming language (like the one you're using in WebMatrix) because with SQL, the idea is that you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="2c947-249">다음은 일부 SQL 명령의 예로 및 용도:</span><span class="sxs-lookup"><span data-stu-id="2c947-249">Here are examples of some SQL commands and what they do:</span></span>
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="2c947-250">인출이 *Id*, *이름*, 및 *가격* 레코드의 열을 *제품* 테이블의 값 *가격* 10 개가 넘는 이며의 값을 기준으로 알파벳 순서로 결과 반환 합니다 *이름을* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-250">This fetches the *Id*, *Name*, and *Price* columns from records in the *Product* table if the value of *Price* is more than 10, and returns the results in alphabetical order based on the values of the *Name* column.</span></span> <span data-ttu-id="2c947-251">이 명령은 일치 하는 레코드가 경우 조건을 또는 빈 집합을 충족 하는 레코드를 포함 하는 결과 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-251">This command will return a result set that contains the records that meet the criteria, or an empty set if no records match.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> <span data-ttu-id="2c947-252">에 새 레코드를 삽입 하는이 *제품* 테이블을 설정 합니다 *이름* 열을 &quot;크 라 상&quot;의 *설명* 열&quot; 잘 끊어지는 만족&quot;, 및 1.99 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-252">This inserts a new record into the *Product* table, setting the *Name* column to &quot;Croissant&quot;, the *Description* column to &quot;A flaky delight&quot;, and the price to 1.99.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> <span data-ttu-id="2c947-253">이 명령에서 레코드를 삭제 합니다 *제품* 2008 년 1 월 1 일 이전인 만료 날짜 열이 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-253">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="2c947-254">(있다고 가정 합니다 *제품* 테이블에는 이러한 열입니다.) MM/DD/YYYY 형식으로 날짜는 여기에 입력 하는 있지만 해당 로캘에 사용 되는 형식으로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-254">(This assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="2c947-255">합니다 `Insert Into` 고 `Delete` 명령 결과 집합을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-255">The `Insert Into` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="2c947-256">대신, 레코드 수를 명령에 의해 영향을 알려 주는 숫자로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-256">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="2c947-257">이러한 작업 (예: 레코드 삽입 및 삭제)의 일부에 대 한 작업을 요청 하는 프로세스는 데이터베이스에 대 한 적절 한 권한이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-257">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="2c947-258">데이터베이스에 연결할 때 사용자 이름 및 암호를 제공 해야 하는 프로덕션 데이터베이스에 대 한 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-258">This is why for production databases you often have to supply a username and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="2c947-259">SQL 명령 여러 가지가 있지만 다음과 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-259">There are dozens of SQL commands, but they all follow a pattern like this.</span></span> <span data-ttu-id="2c947-260">SQL 명령을 사용 하 여 데이터베이스 및 테이블을 만들고, 테이블의 레코드 개수, 가격 계산 보다 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-260">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>


## <a name="inserting-data-in-a-database"></a><span data-ttu-id="2c947-261">데이터베이스에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="2c947-261">Inserting Data in a Database</span></span>

<span data-ttu-id="2c947-262">이 섹션에는 사용자가 새 제품을 추가할 수 있는 페이지를 만드는 방법을 보여 줍니다 합니다 *제품* 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-262">This section shows how to create a page that lets users add a new product to the *Product* database table.</span></span> <span data-ttu-id="2c947-263">새 제품 레코드를 삽입 한 후 페이지에 표시 됩니다 사용 하 여 업데이트 된 테이블의 *ListProducts.cshtml* 이전 섹션에서 만든 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-263">After a new product record is inserted, the page displays the updated table using the *ListProducts.cshtml* page that you created in the previous section.</span></span>

<span data-ttu-id="2c947-264">페이지는 사용자가 입력 데이터를 데이터베이스에 대 한 유효한 지 확인 하려면 유효성 검사를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-264">The page includes validation to make sure that the data that the user enters is valid for the database.</span></span> <span data-ttu-id="2c947-265">예를 들어 코드 페이지에서를 변경 하면 모든 필요한 열에 대 한 입력 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-265">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>

1. <span data-ttu-id="2c947-266">웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *InsertProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-266">In the website, create a new CSHTML file named *InsertProducts.cshtml*.</span></span>
2. <span data-ttu-id="2c947-267">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-267">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    <span data-ttu-id="2c947-268">페이지의 본문 이름, 설명 및 가격을 입력할 수 있도록 하는 세 가지 텍스트 상자를 사용 하 여 HTML 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-268">The body of the page contains an HTML form with three text boxes that let users enter a name, description, and price.</span></span> <span data-ttu-id="2c947-269">사용자가 클릭 하면 합니다 **삽입** 단추를 페이지의 맨 위에 있는 코드에 연결을 엽니다 합니다 *SmallBakery.sdf* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-269">When users click the **Insert** button, the code at the top of the page opens a connection to the *SmallBakery.sdf* database.</span></span> <span data-ttu-id="2c947-270">사용 하 여 사용자가 제출 하는 값을 다음 표시는 `Request` 개체 및 해당 값을 로컬 변수에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-270">You then get the values that the user has submitted by using the `Request` object and assign those values to local variables.</span></span>

    <span data-ttu-id="2c947-271">필요한 각 열에 대 한 사용자 값을 입력 했는지 확인을 위해 등록할 각 `<input>` 의 유효성을 검사 하려는 요소:</span><span class="sxs-lookup"><span data-stu-id="2c947-271">To validate that the user entered a value for each required column, you register each `<input>` element that you want to validate:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    <span data-ttu-id="2c947-272">`Validation` 도우미 등록 하는 필드의 각 값 임을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-272">The `Validation` helper checks that there is a value in each of the fields that you've registered.</span></span> <span data-ttu-id="2c947-273">모든 필드를 확인 하 여 유효성 검사를 통과 했는지 여부를 테스트할 수 있습니다 `Validation.IsValid()`는 사용자 로부터 얻을 수 있는 정보를 처리 하기 전에 일반적으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-273">You can test whether all the fields passed validation by checking `Validation.IsValid()`, which you typically do before you process the information you get from the user:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    <span data-ttu-id="2c947-274">(합니다 `&&` 연산자 의미 AND-이 테스트는 *양식을 제출 하 여 모든 필드 유효성 검사를 통과 한 경우*.)</span><span class="sxs-lookup"><span data-stu-id="2c947-274">(The `&&` operator means AND — this test is *If this is a form submission AND all the fields have passed validation*.)</span></span>

    <span data-ttu-id="2c947-275">모든 열 유효성을 검사 하는 경우 (none 인 빈) 데이터를 삽입 한 다음 다음과 같이 실행할 SQL 문을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-275">If all the columns validated (none were empty), you go ahead and create a SQL statement to insert the data and then execute it as shown next:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    <span data-ttu-id="2c947-276">매개 변수 자리 표시자를 포함 하면 삽입할 값 (`@0`, `@1`, `@2`).</span><span class="sxs-lookup"><span data-stu-id="2c947-276">For the values to insert, you include parameter placeholders (`@0`, `@1`, `@2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c947-277">보안 조치로, 항상 전달할 값 매개 변수를 사용 하는 SQL 문은 앞의 예제에서 볼 수 있듯이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-277">As a security precaution, always pass values to a SQL statement using parameters, as you see in the preceding example.</span></span> <span data-ttu-id="2c947-278">이렇게 하면 사용자의 데이터 유효성 검사를 더한 (때때로 SQL 삽입 공격 이라고 함) 데이터베이스에 악의적인 명령이 보내려는 시도 방지할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-278">This gives you a chance to validate the user's data, plus it helps protect against attempts to send malicious commands to your database (sometimes referred to as SQL injection attacks).</span></span>

    <span data-ttu-id="2c947-279">쿼리를 실행 하려면이 문을 사용 자리 표시자에 대 한 대체 값이 포함 된 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-279">To execute the query, you use this statement, passing to it the variables that contain the values to substitute for the placeholders:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    <span data-ttu-id="2c947-280">이후에 `Insert Into` 문이 실행,이 줄을 사용 하 여 제품을 나열 하는 페이지에 사용자를 보내려면:</span><span class="sxs-lookup"><span data-stu-id="2c947-280">After the `Insert Into` statement has executed, you send the user to the page that lists the products using this line:</span></span>

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    <span data-ttu-id="2c947-281">유효성 검사가 성공 하지 않은 경우에 삽입을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-281">If validation didn't succeed, you skip the insert.</span></span> <span data-ttu-id="2c947-282">누적 된 오류 메시지 (있는 경우)를 표시할 수 있는 페이지에서 도우미를 대신 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-282">Instead, you have a helper in the page that can display the accumulated error messages (if any):</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    <span data-ttu-id="2c947-283">태그에 스타일 블록 라는 CSS 클래스 정의 포함 되도록 알림 `.validation-summary-errors`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-283">Notice that the style block in the markup includes a CSS class definition named `.validation-summary-errors`.</span></span> <span data-ttu-id="2c947-284">이 기본적으로 사용 되는 CSS 클래스의 이름을 합니다 `<div>` 유효성 검사 오류를 포함 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-284">This is the name of the CSS class that's used by default for the `<div>` element that contains any validation errors.</span></span> <span data-ttu-id="2c947-285">CSS 클래스 유효성 검사 요약 오류 빨간색으로 표시 되 고에 굵게, 있지만 정의할 수를 지정 하는 경우에 `.validation-summary-errors` 원하는 서식 표시 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-285">In this case, the CSS class specifies that validation summary errors are displayed in red and in bold, but you can define the `.validation-summary-errors` class to display any formatting you like.</span></span>

### <a name="testing-the-insert-page"></a><span data-ttu-id="2c947-286">Insert 페이지 테스트</span><span class="sxs-lookup"><span data-stu-id="2c947-286">Testing the Insert Page</span></span>

1. <span data-ttu-id="2c947-287">브라우저에서 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-287">View the page in a browser.</span></span> <span data-ttu-id="2c947-288">페이지에는 다음 그림에 표시 되는 것과 비슷한 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-288">The page displays a form that's similar to the one that's shown in the following illustration.</span></span>

    ![[이미지]](5-working-with-data/_static/image5.jpg)
2. <span data-ttu-id="2c947-290">모든 열에 대 한 값을 입력 하지만 남겨 두어야 합니다 *가격* 열은 비워 둠 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-290">Enter values for all the columns, but make sure that you leave the *Price* column blank.</span></span>
3. <span data-ttu-id="2c947-291">**삽입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-291">Click **Insert**.</span></span> <span data-ttu-id="2c947-292">다음 그림에 나와 있는 것 처럼 페이지는 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-292">The page displays an error message, as shown in the following illustration.</span></span> <span data-ttu-id="2c947-293">(새 레코드가 생성 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="2c947-293">(No new record is created.)</span></span>

    ![[이미지]](5-working-with-data/_static/image6.jpg)
4. <span data-ttu-id="2c947-295">폼을 완전히 입력 하 고 클릭 **삽입**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-295">Fill the form out completely, and then click **Insert**.</span></span> <span data-ttu-id="2c947-296">이 이번에는 *ListProducts.cshtml* 페이지가 표시 되 고 새 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-296">This time, the *ListProducts.cshtml* page is displayed and shows the new record.</span></span>

## <a name="updating-data-in-a-database"></a><span data-ttu-id="2c947-297">데이터베이스의 데이터를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="2c947-297">Updating Data in a Database</span></span>

<span data-ttu-id="2c947-298">테이블에 데이터를 입력 한 후 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-298">After data has been entered into a table, you might need to update it.</span></span> <span data-ttu-id="2c947-299">이 절차 앞에 데이터 삽입을 위해 만든 것과 비슷한 두 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-299">This procedure shows you how to create two pages that are similar to the ones you created for data insertion earlier.</span></span> <span data-ttu-id="2c947-300">첫 번째 페이지는 제품을 표시 하 고 사용자가 변경 하나를 선택할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-300">The first page displays products and lets users select one to change.</span></span> <span data-ttu-id="2c947-301">두 번째 페이지를 사용 하면 사용자가 실제로 편집 하 고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-301">The second page lets the users actually make the edits and save them.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2c947-302">**중요 한** 프로덕션 웹 사이트에서 일반적으로 제한할 있습니다 데이터를 변경 하려면 허용할 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-302">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="2c947-303">멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자 권한을 부여 하는 방법에 대 한 정보를 참조 하세요 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-303">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="2c947-304">웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *EditProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-304">In the website, create a new CSHTML file named *EditProducts.cshtml*.</span></span>
2. <span data-ttu-id="2c947-305">파일의 기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-305">Replace the existing markup in the file with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    <span data-ttu-id="2c947-306">이 페이지 간의 유일한 차이점 및 *ListProducts.cshtml* 페이지에서 이전 버전은이 페이지의 HTML 테이블로 포함 하는 표시 하는 추가 열을 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-306">The only difference between this page and the *ListProducts.cshtml* page from earlier is that the HTML table in this page includes an extra column that displays an **Edit** link.</span></span> <span data-ttu-id="2c947-307">이 링크를 클릭 하면 소요 하는 *UpdateProducts.cshtml* 페이지 (만들게 될 다음) 선택한 레코드를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-307">When you click this link, it takes you to the *UpdateProducts.cshtml* page (which you'll create next) where you can edit the selected record.</span></span>

    <span data-ttu-id="2c947-308">만드는 코드를 확인 합니다 **편집** 링크:</span><span class="sxs-lookup"><span data-stu-id="2c947-308">Look at the code that creates the **Edit** link:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    <span data-ttu-id="2c947-309">이 HTML을 만듭니다 `<a>` 요소가 해당 `href` 특성은 동적으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-309">This creates an HTML `<a>` element whose `href` attribute is set dynamically.</span></span> <span data-ttu-id="2c947-310">`href` 특성 링크를 클릭할 때 표시할 페이지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-310">The `href` attribute specifies the page to display when the user clicks the link.</span></span> <span data-ttu-id="2c947-311">또한 전달 된 `Id` 링크를 현재 행의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-311">It also passes the `Id` value of the current row to the link.</span></span> <span data-ttu-id="2c947-312">페이지를 실행 하는 경우 페이지의 소스는 다음과 같은 링크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-312">When the page runs, the page source might contain links like these:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    <span data-ttu-id="2c947-313">다음에 유의 합니다 `href` 특성이로 설정 된 `UpdateProducts/n`여기서 *n* 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-313">Notice that the `href` attribute is set to `UpdateProducts/n`, where *n* is a product number.</span></span> <span data-ttu-id="2c947-314">사용자가 이러한 링크 중 하나를 클릭 하면 결과 URL 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-314">When a user clicks one of these links, the resulting URL will look something like this:</span></span>

    `http://localhost:18816/UpdateProducts/6`

    <span data-ttu-id="2c947-315">즉, 제품 번호를 편집할 수는 URL에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-315">In other words, the product number to be edited will be passed in the URL.</span></span>
3. <span data-ttu-id="2c947-316">브라우저에서 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-316">View the page in a browser.</span></span> <span data-ttu-id="2c947-317">페이지는 다음과 같은 형식으로 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-317">The page displays the data in a format like this:</span></span>

    ![[이미지]](5-working-with-data/_static/image7.jpg)

    <span data-ttu-id="2c947-319">다음으로, 사용자가 실제로 데이터를 업데이트할 수 있는 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-319">Next, you'll create the page that lets users actually update the data.</span></span> <span data-ttu-id="2c947-320">업데이트 페이지에 유효성 검사는 사용자가 입력 데이터 유효성 검사를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-320">The update page includes validation to validate the data that the user enters.</span></span> <span data-ttu-id="2c947-321">예를 들어 코드 페이지에서를 변경 하면 모든 필요한 열에 대 한 입력 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-321">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>
4. <span data-ttu-id="2c947-322">웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *UpdateProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-322">In the website, create a new CSHTML file named *UpdateProducts.cshtml*.</span></span>
5. <span data-ttu-id="2c947-323">파일의 기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-323">Replace the existing markup in the file with the following.</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    <span data-ttu-id="2c947-324">제품 표시 되는 위치 및 사용자가 편집할 수 있는 HTML 폼을 포함 하는 페이지의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-324">The body of the page contains an HTML form where a product is displayed and where users can edit it.</span></span> <span data-ttu-id="2c947-325">표시할 제품을 가져오려면이 SQL 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-325">To get the product to display, you use this SQL statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    <span data-ttu-id="2c947-326">이 ID에 전달 되는 값과 일치 하는 제품을 선택 합니다는 `@0` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-326">This will select the product whose ID matches the value that's passed in the `@0` parameter.</span></span> <span data-ttu-id="2c947-327">(때문에 *Id* 기본 핵심 이며 따라서 해야 하나의 제품 레코드 그 어느 때 선택할 수 있습니다 이러한 방식으로, 고유 합니다.) 이를 전달 하는 ID 값을 가져오려면 `Select` 문을 다음 구문을 사용 하 여 URL의 일부로 페이지에 전달 되는 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-327">(Because *Id* is the primary key and therefore must be unique, only one product record can ever be selected this way.) To get the ID value to pass to this `Select` statement, you can read the value that's passed to the page as part of the URL, using the following syntax:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    <span data-ttu-id="2c947-328">제품 레코드를 실제로 페치 하려면 사용는 `QuerySingle` 레코드 하나만 반환 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="2c947-328">To actually fetch the product record, you use the `QuerySingle` method, which will return just one record:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    <span data-ttu-id="2c947-329">단일 행에 반환 되는 `row` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-329">The single row is returned into the `row` variable.</span></span> <span data-ttu-id="2c947-330">각 열에서 데이터를 가져오기 하 고 다음과 같은 로컬 변수에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-330">You can get data out of each column and assign it to local variables like this:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    <span data-ttu-id="2c947-331">폼에 대 한 태그에서 이러한 값에에서 표시 됩니다 자동으로 개별 입력란 다음과 같은 포함 된 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="2c947-331">In the markup for the form, these values are displayed automatically in individual text boxes by using embedded code like the following:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    <span data-ttu-id="2c947-332">코드의 해당 부분 업데이트 제품 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-332">That part of the code displays the product record to be updated.</span></span> <span data-ttu-id="2c947-333">레코드가 표시 되 면 사용자 개별 열을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-333">Once the record has been displayed, the user can edit individual columns.</span></span>

    <span data-ttu-id="2c947-334">사용자가 클릭 하 여 폼을 제출 하는 경우는 **업데이트** 단추를의 코드는 `if(IsPost)` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-334">When the user submits the form by clicking the **Update** button, the code in the `if(IsPost)` block runs.</span></span> <span data-ttu-id="2c947-335">사용자의 값을 가져옵니다는 `Request` 개체 변수에 값을 저장 하 고 각 열 채워져 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-335">This gets the user's values from the `Request` object, stores the values in variables, and validates that each column has been filled in.</span></span> <span data-ttu-id="2c947-336">유효성 검사에 통과 하는 경우 코드를 다음 SQL Update 문을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-336">If validation passes, the code creates the following SQL Update statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    <span data-ttu-id="2c947-337">SQL에서 `Update` 문을 지정할 각 열 설정할 값을 업데이트 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-337">In a SQL `Update` statement, you specify each column to update and the value to set it to.</span></span> <span data-ttu-id="2c947-338">이 코드에서 값을 매개 변수 자리 표시자를 사용 하 여 지정 된 `@0`, `@1`, `@2`등입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-338">In this code, the values are specified using the parameter placeholders `@0`, `@1`, `@2`, and so on.</span></span> <span data-ttu-id="2c947-339">(보안상의 앞에서 설명한 대로 항상 값을 전달 해야 SQL 문에 매개 변수를 사용 하 여.)</span><span class="sxs-lookup"><span data-stu-id="2c947-339">(As noted earlier, for security, you should always pass values to a SQL statement by using parameters.)</span></span>

    <span data-ttu-id="2c947-340">호출 하는 경우는 `db.Execute` SQL 문의 매개 변수에 해당 하는 순서 대로 값이 포함 된 변수를 전달할 메서드:</span><span class="sxs-lookup"><span data-stu-id="2c947-340">When you call the `db.Execute` method, you pass the variables that contain the values in the order that corresponds to the parameters in the SQL statement:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    <span data-ttu-id="2c947-341">이후에 `Update` 문이 실행 된 사용자 편집 페이지를 다시 리디렉션할 하려면 다음 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-341">After the `Update` statement has been executed, you call the following method in order to redirect the user back to the edit page:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    <span data-ttu-id="2c947-342">사용자 데이터베이스의 데이터는 업데이트 된 목록을 표시 하 고 다른 제품을 편집할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-342">The effect is that the user sees an updated listing of the data in the database and can edit another product.</span></span>
6. <span data-ttu-id="2c947-343">페이지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-343">Save the page.</span></span>
7. <span data-ttu-id="2c947-344">실행 합니다 *EditProducts.cshtml* 페이지 (업데이트 페이지 제외) 하 고 클릭 한 다음 **편집** 편집할 제품을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-344">Run the *EditProducts.cshtml* page (not the update page) and then click **Edit** to select a product to edit.</span></span> <span data-ttu-id="2c947-345">합니다 *UpdateProducts.cshtml* 선택한 레코드를 보여 주는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-345">The *UpdateProducts.cshtml* page is displayed, showing the record you selected.</span></span>

    ![[이미지]](5-working-with-data/_static/image8.jpg)
8. <span data-ttu-id="2c947-347">변경 하 고 클릭 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-347">Make a change and click **Update**.</span></span> <span data-ttu-id="2c947-348">업데이트 된 데이터를 사용 하 여 제품 목록은 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-348">The products list is shown again with your updated data.</span></span>

## <a name="deleting-data-in-a-database"></a><span data-ttu-id="2c947-349">데이터베이스의 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-349">Deleting Data in a Database</span></span>

<span data-ttu-id="2c947-350">이 섹션에서는 사용자의 제품을 삭제 하도록 하는 방법을 보여 줍니다 합니다 *제품* 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-350">This section shows how to let users delete a product from the *Product* database table.</span></span> <span data-ttu-id="2c947-351">이 예제에서는 두 페이지로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-351">The example consists of two pages.</span></span> <span data-ttu-id="2c947-352">첫 번째 페이지에서 사용자를 삭제 하는 레코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-352">In the first page, users select a record to delete.</span></span> <span data-ttu-id="2c947-353">삭제할 레코드는 레코드를 삭제 하도록 확인을 두 번째 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-353">The record to be deleted is then displayed in a second page that lets them confirm that they want to delete the record.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2c947-354">**중요 한** 프로덕션 웹 사이트에서 일반적으로 제한할 있습니다 데이터를 변경 하려면 허용할 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-354">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="2c947-355">멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자 권한을 부여 하는 방법에 대 한 정보를 참조 하세요 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-355">For information about how to set up membership and about ways to authorize user to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="2c947-356">웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *ListProductsForDelete.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-356">In the website, create a new CSHTML file named *ListProductsForDelete.cshtml*.</span></span>
2. <span data-ttu-id="2c947-357">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-357">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    <span data-ttu-id="2c947-358">이 페이지는 비슷합니다는 *EditProducts.cshtml* 앞에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-358">This page is similar to the *EditProducts.cshtml* page from earlier.</span></span> <span data-ttu-id="2c947-359">그러나 표시 하는 대신는 **편집** 링크 각 제품에 대 한 표시를 **삭제** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-359">However, instead of displaying an **Edit** link for each product, it displays a **Delete** link.</span></span> <span data-ttu-id="2c947-360">합니다 **삭제** 링크가 포함된 된 다음 코드를 사용 하 여 태그에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-360">The **Delete** link is created using the following embedded code in the markup:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    <span data-ttu-id="2c947-361">이 사용자가 링크를 클릭할 때 다음과 같은 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-361">This creates a URL that looks like this when users click the link:</span></span>

    `http://<server>/DeleteProduct/4`

    <span data-ttu-id="2c947-362">라는 페이지를 호출 하는 URL *DeleteProduct.cshtml* (만들게 될 옆) 하 고 삭제할 제품의 ID를 전달 (여기에서는 4).</span><span class="sxs-lookup"><span data-stu-id="2c947-362">The URL calls a page named *DeleteProduct.cshtml* (which you'll create next) and passes it the ID of the product to delete (here, 4).</span></span>
3. <span data-ttu-id="2c947-363">파일을 저장 하지만 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-363">Save the file, but leave it open.</span></span>
4. <span data-ttu-id="2c947-364">라는 다른 CHTML 파일을 만듭니다 *DeleteProduct.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-364">Create another CHTML file named *DeleteProduct.cshtml*.</span></span> <span data-ttu-id="2c947-365">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-365">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    <span data-ttu-id="2c947-366">이 페이지에 의해 호출 됩니다 *ListProductsForDelete.cshtml* 고 사용자가 제품을 삭제 하도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-366">This page is called by *ListProductsForDelete.cshtml* and lets users confirm that they want to delete a product.</span></span> <span data-ttu-id="2c947-367">삭제할 제품을 나열 하려면 얻게 URL에서 삭제할 제품의 ID는 다음 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="2c947-367">To list the product to be deleted, you get the ID of the product to delete from the URL using the following code:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    <span data-ttu-id="2c947-368">페이지는 사용자가 실제로 레코드를 삭제 하는 단추를 클릭 한 다음 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-368">The page then asks the user to click a button to actually delete the record.</span></span> <span data-ttu-id="2c947-369">이 중요 한 보안 측정값을: 업데이트 또는 삭제와 같은 웹 사이트의 중요 한 작업을 수행할 때 이러한 작업이 이루어져야 합니다. 항상 가져오기 작업을 하지 POST 작업을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-369">This is an important security measure: when you perform sensitive operations in your website like updating or deleting data, these operations should always be done using a POST operation, not a GET operation.</span></span> <span data-ttu-id="2c947-370">가져오기 작업을 사용 하 여 삭제 작업을 수행할 수 있도록 사이트는 설정 하 고, 경우에 같은 URL을 전달할 수 있습니다 누구나 `http://<server>/DeleteProduct/4` 및 데이터베이스에서 원하는 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-370">If your site is set up so that a delete operation can be performed using a GET operation, anyone can pass a URL like `http://<server>/DeleteProduct/4` and delete anything they want from your database.</span></span> <span data-ttu-id="2c947-371">확인을 추가 하 고 POST를 사용 하 여 삭제를 수행할 수 있도록 페이지를 코딩 하 여 사이트에 보안 조치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-371">By adding the confirmation and coding the page so that the deletion can be performed only by using a POST, you add a measure of security to your site.</span></span>

    <span data-ttu-id="2c947-372">실제 삭제 작업은 post 작업을이 이며 ID 비어 있지는 먼저 확인 하는 다음 코드를 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-372">The actual delete operation is performed using the following code, which first confirms that this is a post operation and that the ID isn't empty:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    <span data-ttu-id="2c947-373">코드에 지정된 된 레코드를 삭제 하 고 다음 목록 페이지로 사용자를 리디렉션하는 SQL 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-373">The code runs a SQL statement that deletes the specified record and then redirects the user back to the listing page.</span></span>
5. <span data-ttu-id="2c947-374">실행할 *ListProductsForDelete.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-374">Run *ListProductsForDelete.cshtml* in a browser.</span></span>

    ![[이미지]](5-working-with-data/_static/image9.jpg)
6. <span data-ttu-id="2c947-376">클릭 합니다 **삭제** 제품 중 하나에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-376">Click the **Delete** link for one of the products.</span></span> <span data-ttu-id="2c947-377">합니다 *DeleteProduct.cshtml* 해당 레코드를 삭제할 것인지 확인 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-377">The *DeleteProduct.cshtml* page is displayed to confirm that you want to delete that record.</span></span>
7. <span data-ttu-id="2c947-378">클릭 합니다 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-378">Click the **Delete** button.</span></span> <span data-ttu-id="2c947-379">제품 레코드가 삭제 되 고는 업데이트 된 제품 목록으로 페이지가 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-379">The product record is deleted and the page is refreshed with an updated product listing.</span></span>

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a><span data-ttu-id="2c947-380">데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="2c947-380">Connecting to a Database</span></span>
> 
> <span data-ttu-id="2c947-381">두 가지 방법으로 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-381">You can connect to a database in two ways.</span></span> <span data-ttu-id="2c947-382">첫 번째 사용 하는 것을 `Database.Open` 메서드 및 데이터베이스 파일의 이름을 지정 하 (작은 합니다 *.sdf* 확장):</span><span class="sxs-lookup"><span data-stu-id="2c947-382">The first is to use the `Database.Open` method and to specify the name of the database file (less the *.sdf* extension):</span></span>
> 
> `var db = Database.Open("SmallBakery");`
> 
> <span data-ttu-id="2c947-383">합니다 `Open` 메서드가 있다고 가정 합니다. *sdf* 파일은 웹 사이트 *App\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-383">The `Open` method assumes that the .*sdf* file is in the website's *App\_Data* folder.</span></span> <span data-ttu-id="2c947-384">이 폴더는 데이터를 보유에 맞게 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-384">This folder is designed specifically for holding data.</span></span> <span data-ttu-id="2c947-385">예를 들어, 웹 사이트에 데이터를 읽고 쓸 수 있도록 적절 한 권한이 및 보안을 위해 WebMatrix 액세스를 허용 하지 파일에이 폴더에서.</span><span class="sxs-lookup"><span data-stu-id="2c947-385">For example, it has appropriate permissions to allow the website to read and write data, and as a security measure, WebMatrix does not allow access to files from this folder.</span></span>
> 
> <span data-ttu-id="2c947-386">두 번째 방법은 연결 문자열을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-386">The second way is to use a connection string.</span></span> <span data-ttu-id="2c947-387">연결 문자열을 데이터베이스에 연결 하는 방법에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-387">A connection string contains information about how to connect to a database.</span></span> <span data-ttu-id="2c947-388">파일 경로 포함할 수 있습니다 또는 사용자 이름 및 해당 서버에 연결할 암호와 함께 로컬 또는 원격 서버의 SQL Server 데이터베이스의 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-388">This can include a file path, or it can include the name of a SQL Server database on a local or remote server, along with a user name and password to connect to that server.</span></span> <span data-ttu-id="2c947-389">(중앙에서 관리 되는 버전의 SQL Server에서 데이터를 유지 하는 경우와 같은 호스팅 공급자의 사이트에서 하려면 항상 사용 하는 연결 문자열 데이터베이스 연결 정보를 지정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2c947-389">(If you keep data in a centrally managed version of SQL Server, such as on a hosting provider's site, you always use a connection string to specify the database connection information.)</span></span>
> 
> <span data-ttu-id="2c947-390">WebMatrix에서 연결 문자열은 일반적으로 저장 라는 XML 파일에 *Web.config*합니다. 이름에서 알 수 있듯이, 사용할 수는 *Web.config* 사이트 필요할 수 있는 연결 문자열을 포함 하 여 사이트의 구성 정보를 저장 하 여 웹 사이트의 루트에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-390">In WebMatrix, connection strings are usually stored in an XML file named *Web.config*. As the name implies, you can use a *Web.config* file in the root of your website to store the site's configuration information, including any connection strings that your site might require.</span></span> <span data-ttu-id="2c947-391">연결 문자열의 예는 *Web.config* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-391">An example of a connection string in a *Web.config* file might look like the following:</span></span>
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> <span data-ttu-id="2c947-392">예제에서는 연결 문자열을 가리키는 어딘가에 서버에서 실행 되는 SQL Server 인스턴스의 데이터베이스 (로컬 달리 *.sdf* 파일).</span><span class="sxs-lookup"><span data-stu-id="2c947-392">In the example, the connection string points to a database in an instance of SQL Server that's running on a server somewhere (as opposed to a local *.sdf* file).</span></span> <span data-ttu-id="2c947-393">에 대 한 적절 한 이름으로 대체 해야 `myServer` 하 고 `myDatabase`, SQL Server 로그인 값을 지정 하 고 `username` 및 `password`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-393">You would need to substitute the appropriate names for `myServer` and `myDatabase`, and specify SQL Server login values for `username` and `password`.</span></span> <span data-ttu-id="2c947-394">(사용자 이름 및 암호 값 같지 반드시 Windows 자격 증명 또는 호스팅 공급자가 제공한 서버에 로그인 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-394">(The username and password values are not necessarily the same as your Windows credentials or as the values that your hosting provider has given you for logging in to their servers.</span></span> <span data-ttu-id="2c947-395">관리자에 게 문의 해야 하는 정확한 값에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2c947-395">Check with the administrator for the exact values you need.)</span></span>
> 
> <span data-ttu-id="2c947-396">합니다 `Database.Open` 메서드는 데이터베이스의 이름을 전달할 수 있기 때문에 유연 *.sdf* 에 저장 된 연결 문자열의 이름 또는 파일을 *Web.config* 파일.</span><span class="sxs-lookup"><span data-stu-id="2c947-396">The `Database.Open` method is flexible, because it lets you pass either the name of a database *.sdf* file or the name of a connection string that's stored in the *Web.config* file.</span></span> <span data-ttu-id="2c947-397">다음 예제에서는 이전 예제에 나와 있는 연결 문자열을 사용 하 여 데이터베이스에 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-397">The following example shows how to connect to the database using the connection string illustrated in the previous example:</span></span>
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> <span data-ttu-id="2c947-398">언급 했 듯이 `Database.Open` 메서드를 사용 하면 데이터베이스 이름 또는 연결 문자열을 전달 하 고 사용 하는 그림 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-398">As noted, the `Database.Open` method lets you pass either a database name or a connection string, and it'll figure out which to use.</span></span> <span data-ttu-id="2c947-399">배포 하는 경우이 기능은 매우 유용 (게시) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-399">This is very useful when you deploy (publish) your website.</span></span> <span data-ttu-id="2c947-400">사용할 수는 *.sdf* 파일을 *앱\_데이터* 을 개발 하 고 사이트를 테스트 하는 경우 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-400">You can use an *.sdf* file in the *App\_Data* folder when you're developing and testing your site.</span></span> <span data-ttu-id="2c947-401">사이트를 프로덕션 서버로 이동할 때 연결 문자열을 사용할 수 있습니다 합니다 *Web.config* 와 동일한 이름을 가진 파일에 *.sdf* 있지만 호스팅 공급자의 가리키는 &#8212;코드를 변경할 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-401">Then when you move your site to a production server, you can use a connection string in the *Web.config* file that has the same name as your *.sdf* file but that points to the hosting provider's database &#8212; all without having to change your code.</span></span>
> 
> <span data-ttu-id="2c947-402">마지막으로, 연결 문자열을 직접 사용 하려는 경우 호출할 수 있습니다 합니다 `Database.OpenConnectionString` 메서드와 패스의 이름만 대신 해당 실제 연결 문자열을 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-402">Finally, if you want to work directly with a connection string, you can call the `Database.OpenConnectionString` method and pass it the actual connection string instead of just the name of one in the *Web.config* file.</span></span> <span data-ttu-id="2c947-403">어떤 이유로 없는 연결 문자열에 액세스 하는 경우에 유용할 수 있습니다 (에서 같은 값 또는 합니다 *.sdf* 파일 이름) 페이지 실행 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-403">This might be useful in situations where for some reason you don't have access to the connection string (or values in it, such as the *.sdf* file name) until the page is running.</span></span> <span data-ttu-id="2c947-404">그러나 대부분의 시나리오에서 사용할 수 있습니다 `Database.Open` 이 문서에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c947-404">However, for most scenarios, you can use `Database.Open` as described in this article.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2c947-405">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2c947-405">Additional Resources</span></span>

- [<span data-ttu-id="2c947-406">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="2c947-406">SQL Server Compact</span></span>](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [<span data-ttu-id="2c947-407">SQL Server 또는 WebMatrix에서 MySQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="2c947-407">Connecting to a SQL Server or MySQL Database in WebMatrix</span></span>](https://go.microsoft.com/fwlink/?LinkId=208661)
- [<span data-ttu-id="2c947-408">ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="2c947-408">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
