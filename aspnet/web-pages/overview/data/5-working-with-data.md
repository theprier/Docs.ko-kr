---
uid: web-pages/overview/data/5-working-with-data
title: "ASP.NET 웹에서 데이터베이스 작업 소개 페이지 (Razor) 사이트 | Microsoft Docs"
author: tfitzmac
description: "데이터베이스에서 데이터를 액세스 하 고 ASP.NET 웹 페이지를 사용 하 여 표시 하는 방법을 설명이 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2014
ms.topic: article
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 460af471a1b0650f8d782d582ce6cd9a06664d5c
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="41604-103">ASP.NET 웹에서 데이터베이스 작업 소개 페이지 (Razor) 사이트</span><span class="sxs-lookup"><span data-stu-id="41604-103">Introduction to Working with a Database in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="41604-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="41604-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="41604-105">이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 데이터베이스를 만들려면 Microsoft WebMatrix 도구를 사용 하는 방법 및 표시, 추가, 편집 및 데이터를 삭제할 수 있는 페이지를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-105">This article describes how to use Microsoft WebMatrix tools to create a database in an ASP.NET Web Pages (Razor) website, and how to create pages that let you display, add, edit, and delete data.</span></span>
> 
> <span data-ttu-id="41604-106">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="41604-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="41604-107">데이터베이스를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="41604-107">How to create a database.</span></span>
> - <span data-ttu-id="41604-108">데이터베이스에 연결 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="41604-108">How to connect to a database.</span></span>
> - <span data-ttu-id="41604-109">웹 페이지에 데이터를 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="41604-109">How to display data in a web page.</span></span>
> - <span data-ttu-id="41604-110">삽입, 업데이트 및 데이터베이스 레코드를 삭제 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="41604-110">How to insert, update, and delete database records.</span></span>
> 
> <span data-ttu-id="41604-111">다음은 문서에 도입 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-111">These are the features introduced in the article:</span></span>
> 
> - <span data-ttu-id="41604-112">Microsoft SQL Server Compact Edition 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-112">Working with a Microsoft SQL Server Compact Edition database.</span></span>
> - <span data-ttu-id="41604-113">SQL 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-113">Working with SQL queries.</span></span>
> - <span data-ttu-id="41604-114">`Database` 클래스</span><span class="sxs-lookup"><span data-stu-id="41604-114">The `Database` class.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="41604-115">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="41604-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="41604-116">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="41604-116">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="41604-117">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="41604-117">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="41604-118">이 자습서는 WebMatrix 3 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-118">This tutorial also works with WebMatrix 3.</span></span> <span data-ttu-id="41604-119">ASP.NET Web Pages 3 및 Visual Studio 2013 (또는 Visual Studio Express 2013 for Web);를 사용할 수 있습니다. 그러나 사용자 인터페이스가 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="41604-119">You can use ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web); however, the user interface will be different.</span></span>


## <a name="introduction-to-databases"></a><span data-ttu-id="41604-120">데이터베이스 소개</span><span class="sxs-lookup"><span data-stu-id="41604-120">Introduction to Databases</span></span>

<span data-ttu-id="41604-121">일반적인 주소록을 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="41604-121">Imagine a typical address book.</span></span> <span data-ttu-id="41604-122">주소록에 각 항목에 대 한 (즉, 각 사용자에 대 한) 일부의 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 정보를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-122">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

<span data-ttu-id="41604-123">이와 같은 그림 데이터를 행과 열이 있는 테이블로 일반적인 방법은입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-123">A typical way to picture data like this is as a table with rows and columns.</span></span> <span data-ttu-id="41604-124">데이터베이스의 경우 각 행은 종종 레코드 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-124">In database terms, each row is often referred to as a record.</span></span> <span data-ttu-id="41604-125">각 데이터 형식에 대 한 값을 포함 하는 각 열 (필드 라고도 함): 이름, 마지막 이름 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-125">Each column (sometimes referred to as fields) contains a value for each type of data: first name, last name, and so on.</span></span>

| <span data-ttu-id="41604-126">**ID**</span><span class="sxs-lookup"><span data-stu-id="41604-126">**ID**</span></span> | <span data-ttu-id="41604-127">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="41604-127">**FirstName**</span></span> | <span data-ttu-id="41604-128">**LastName**</span><span class="sxs-lookup"><span data-stu-id="41604-128">**LastName**</span></span> | <span data-ttu-id="41604-129">**주소**</span><span class="sxs-lookup"><span data-stu-id="41604-129">**Address**</span></span> | <span data-ttu-id="41604-130">**전자 메일**</span><span class="sxs-lookup"><span data-stu-id="41604-130">**Email**</span></span> | <span data-ttu-id="41604-131">**전화**</span><span class="sxs-lookup"><span data-stu-id="41604-131">**Phone**</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="41604-132">1</span><span class="sxs-lookup"><span data-stu-id="41604-132">1</span></span> | <span data-ttu-id="41604-133">Jim</span><span class="sxs-lookup"><span data-stu-id="41604-133">Jim</span></span> | <span data-ttu-id="41604-134">Abrus</span><span class="sxs-lookup"><span data-stu-id="41604-134">Abrus</span></span> | <span data-ttu-id="41604-135">210 100th St SE Orcas WA 98031</span><span class="sxs-lookup"><span data-stu-id="41604-135">210 100th St SE Orcas WA 98031</span></span> | jim@contoso.com | <span data-ttu-id="41604-136">555 0100</span><span class="sxs-lookup"><span data-stu-id="41604-136">555 0100</span></span> |
| <span data-ttu-id="41604-137">2</span><span class="sxs-lookup"><span data-stu-id="41604-137">2</span></span> | <span data-ttu-id="41604-138">Terry</span><span class="sxs-lookup"><span data-stu-id="41604-138">Terry</span></span> | <span data-ttu-id="41604-139">Adams</span><span class="sxs-lookup"><span data-stu-id="41604-139">Adams</span></span> | <span data-ttu-id="41604-140">1234 Main St. 시애틀 WA 99011</span><span class="sxs-lookup"><span data-stu-id="41604-140">1234 Main St. Seattle WA 99011</span></span> | terry@cohowinery.com | <span data-ttu-id="41604-141">555 0101</span><span class="sxs-lookup"><span data-stu-id="41604-141">555 0101</span></span> |

<span data-ttu-id="41604-142">대부분의 데이터베이스 테이블에 대 한 테이블에 고객 번호, 계좌 번호 등과 같은 고유 식별자가 포함 된 열입니다. 테이블의로 알려져 *기본 키*, 테이블의 각 행 식별을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-142">For most database tables, the table has to have a column that contains a unique identifier, like a customer number, account number, etc. This is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="41604-143">예제에서는 ID 열은 주소록에 대 한 기본 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-143">In the example, the ID column is the primary key for the address book.</span></span>

<span data-ttu-id="41604-144">이 기본 데이터베이스의 개념을 이해 한 준비가 간단한 데이터베이스를 만들고 추가, 수정 및 데이터 삭제와 같은 작업을 수행 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="41604-144">With this basic understanding of databases, you're ready to learn how to create a simple database and perform operations such as adding, modifying, and deleting data.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="41604-145">**관계형 데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="41604-145">**Relational Databases**</span></span>
> 
> <span data-ttu-id="41604-146">스프레드시트 및 텍스트 파일 등의 방법으로 많은 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-146">You can store data in lots of ways, including text files and spreadsheets.</span></span> <span data-ttu-id="41604-147">그러나 대부분의 비즈니스 사용자에 대 한 데이터는 관계형 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-147">For most business uses, though, data is stored in a relational database.</span></span>
> 
> <span data-ttu-id="41604-148">이 문서는 데이터베이스로 매우 밀접 하 게 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-148">This article doesn't go very deeply into databases.</span></span> <span data-ttu-id="41604-149">그러나 좋습니다 것에 대 한 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-149">However, you might find it useful to understand a little about them.</span></span> <span data-ttu-id="41604-150">관계형 데이터베이스의 정보는 별도 테이블으로 논리적으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-150">In a relational database, information is logically divided into separate tables.</span></span> <span data-ttu-id="41604-151">예를 들어 수업 및 학생 들에 대 한 학교에 대 한 데이터베이스 별도 테이블에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-151">For example, a database for a school might contain separate tables for students and for class offerings.</span></span> <span data-ttu-id="41604-152">데이터베이스 소프트웨어 (예: SQL Server) 지원 강력한 수 있는 명령을 동적으로 테이블 간의 관계를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-152">The database software (such as SQL Server) supports powerful commands that let you dynamically establish relationships between the tables.</span></span> <span data-ttu-id="41604-153">예를 들어, 일정을 만들기 위해 학생과 클래스 간의 논리적 관계를 설정 하는 관계형 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-153">For example, you can use the relational database to establish a logical relationship between students and classes in order to create a schedule.</span></span> <span data-ttu-id="41604-154">별도 테이블에 데이터를 저장할 테이블 구조의 간단 하 고 테이블에 중복 데이터를 보관할 필요가 줄어 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-154">Storing data in separate tables reduces the complexity of the table structure and reduces the need to keep redundant data in tables.</span></span>


## <a name="creating-a-database"></a><span data-ttu-id="41604-155">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="41604-155">Creating a Database</span></span>

<span data-ttu-id="41604-156">이 절차에서는 WebMatrix에 포함 된 SQL Server Compact 데이터베이스 디자인 도구를 사용 하 여 SmallBakery 라는 데이터베이스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41604-156">This procedure shows you how to create a database named SmallBakery by using the SQL Server Compact Database design tool that's included in WebMatrix.</span></span> <span data-ttu-id="41604-157">코드를 사용 하는 데이터베이스를 만들 수는 있지만 데이터베이스 및 WebMatrix와 같은 디자인 도구를 사용 하 여 데이터베이스 테이블을 만드는 대부분의 일반적인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-157">Although you can create a database using code, it's more typical to create the database and database tables using a design tool like WebMatrix.</span></span>

1. <span data-ttu-id="41604-158">WebMatrix를 시작 하 고 빠른 시작 페이지에서 클릭 **템플릿에서 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-158">Start WebMatrix, and on the Quick Start page, click **Site From Template**.</span></span>
2. <span data-ttu-id="41604-159">선택 **빈 사이트**, 및는 **사이트 이름** 상자 "SmallBakery"를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-159">Select **Empty Site**, and in the **Site Name** box enter "SmallBakery" and then click **OK**.</span></span> <span data-ttu-id="41604-160">사이트 생성 되어 WebMatrix에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-160">The site is created and displayed in WebMatrix.</span></span>
3. <span data-ttu-id="41604-161">왼쪽된 창에서 클릭 된 **데이터베이스** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-161">In the left pane, click the **Databases** workspace.</span></span>
4. <span data-ttu-id="41604-162">리본 메뉴에서 클릭 **새 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-162">In the ribbon, click **New Database**.</span></span> <span data-ttu-id="41604-163">빈 데이터베이스는 사이트와 동일한 이름을 가진 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-163">An empty database is created with the same name as your site.</span></span>
5. <span data-ttu-id="41604-164">왼쪽된 창에서 확장 된 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-164">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
6. <span data-ttu-id="41604-165">리본 메뉴에서 클릭 **새 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-165">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="41604-166">WebMatrix는 테이블 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41604-166">WebMatrix opens the table designer.</span></span>

    ![[image]](5-working-with-data/_static/image1.jpg)
7. <span data-ttu-id="41604-168">클릭는 **이름** 열을 입력 하 고 &quot;Id&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-168">Click in the **Name** column and enter &quot;Id&quot;.</span></span>
8. <span data-ttu-id="41604-169">에 **데이터 형식** 열에서 선택 **int**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-169">In the **Data Type** column, select **int**.</span></span>
9. <span data-ttu-id="41604-170">설정의 **기본 키가?** 및 **식별은?** 옵션을 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-170">Set the **Is Primary Key?** and **Is Identify?** options to **Yes**.</span></span>

    <span data-ttu-id="41604-171">이름에서 알 수 있듯이 **기본 키가** 이 되도록 테이블의 기본 키의 데이터베이스에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41604-171">As the name suggests, **Is Primary Key** tells the database that this will be the table's primary key.</span></span> <span data-ttu-id="41604-172">**인증서가 Id** (1부터 시작)에 다음 일련 번호를 할당 하 고 자동으로 모든 새 레코드에 대 한 ID 번호를 만들려면 데이터베이스에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-172">**Is Identity** tells the database to automatically create an ID number for every new record and to assign it the next sequential number (starting at 1).</span></span>
10. <span data-ttu-id="41604-173">다음 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-173">Click in the next row.</span></span> <span data-ttu-id="41604-174">편집기에는 새 열 정의 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-174">The editor starts a new column definition.</span></span>
11. <span data-ttu-id="41604-175">이름 값에 대 한 입력 &quot;이름&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-175">For the Name value, enter &quot;Name&quot;.</span></span>
12. <span data-ttu-id="41604-176">에 대 한 **데이터 형식**, 선택 &quot;nvarchar&quot; 길이 50으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-176">For **Data Type**, choose &quot;nvarchar&quot; and set the length to 50.</span></span> <span data-ttu-id="41604-177">*var* 의 일부가 `nvarchar` 이 열에 대 한 데이터가 필요에 따라 크기가 레코드 간에 다를 수 있습니다 하는 문자열을 될 것 이라는 데이터베이스에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41604-177">The *var* part of `nvarchar` tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="41604-178">(의 *n* 나타내는 접두사 *national*, 필드를 나타내는 모든 알파벳 문자 데이터를 보유할 수를 나타내는 또는 쓰기 시스템 &#8212; 즉, 필드 유니코드 데이터를 보유 합니다.)</span><span class="sxs-lookup"><span data-stu-id="41604-178">(The *n* prefix represents *national*, indicating that the field can hold character data that represents any alphabet or writing system &#8212; that is, that the field holds Unicode data.)</span></span>
13. <span data-ttu-id="41604-179">설정의 **Null 허용** 옵션을 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-179">Set the **Allow Nulls** option to **No**.</span></span> <span data-ttu-id="41604-180">이 강제 적용 하는 *이름* 열 비워 두면 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-180">This will enforce that the *Name* column is not left blank.</span></span>
14. <span data-ttu-id="41604-181">라는 열이 동일한 프로세스를 사용 하 여 만들 *설명*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-181">Using this same process, create a column named *Description*.</span></span> <span data-ttu-id="41604-182">설정 **데이터 형식** 길이 및 설정에 대 한 "nvarchar"으로 **Null 허용** 를 false입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-182">Set **Data Type** to "nvarchar" and 50 for the length, and set **Allow Nulls** to false.</span></span>
15. <span data-ttu-id="41604-183">व े ं 라는 *가격*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-183">Create a column named *Price*.</span></span> <span data-ttu-id="41604-184">설정 **"money" 데이터 형식의** 설정 **Null 허용** 를 false입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-184">Set **Data Type to "money"** and set **Allow Nulls** to false.</span></span>
16. <span data-ttu-id="41604-185">맨 위에 있는 상자에서 테이블의 이름을 지정 &quot;제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-185">In the box at the top, name the table &quot;Product&quot;.</span></span>

    <span data-ttu-id="41604-186">완료 되 면 정의 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-186">When you're done, the definition will look like this:</span></span>

    ![[image]](5-working-with-data/_static/image2.jpg)
17. <span data-ttu-id="41604-188">테이블을 저장 하려면 Ctrl + S를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="41604-188">Press Ctrl+S to save the table.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="41604-189">데이터베이스에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="41604-189">Adding Data to the Database</span></span>

<span data-ttu-id="41604-190">이제 문서의 뒷부분에서 다루게 하 여 데이터베이스에 몇 가지 샘플 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-190">Now you can add some sample data to your database that you'll work with later in the article.</span></span>

1. <span data-ttu-id="41604-191">왼쪽된 창에서 확장 된 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-191">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
2. <span data-ttu-id="41604-192">Product 테이블을 마우스 오른쪽 단추로 누른 **데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-192">Right-click the Product table and then click **Data**.</span></span>
3. <span data-ttu-id="41604-193">편집 창에서 다음 레코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-193">In the edit pane, enter the following records:</span></span>

    | <span data-ttu-id="41604-194">**이름**</span><span class="sxs-lookup"><span data-stu-id="41604-194">**Name**</span></span> | <span data-ttu-id="41604-195">**설명**</span><span class="sxs-lookup"><span data-stu-id="41604-195">**Description**</span></span> | <span data-ttu-id="41604-196">**가격**</span><span class="sxs-lookup"><span data-stu-id="41604-196">**Price**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="41604-197">빵</span><span class="sxs-lookup"><span data-stu-id="41604-197">Bread</span></span> | <span data-ttu-id="41604-198">매일 새로 기본 제공된 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-198">Baked fresh every day.</span></span> | <span data-ttu-id="41604-199">2.99</span><span class="sxs-lookup"><span data-stu-id="41604-199">2.99</span></span> |
    | <span data-ttu-id="41604-200">딸기맛 Shortcake</span><span class="sxs-lookup"><span data-stu-id="41604-200">Strawberry Shortcake</span></span> | <span data-ttu-id="41604-201">우리의 가든에서 유기적 딸기 사용해 서 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-201">Made with organic strawberries from our garden.</span></span> | <span data-ttu-id="41604-202">9.99</span><span class="sxs-lookup"><span data-stu-id="41604-202">9.99</span></span> |
    | <span data-ttu-id="41604-203">Apple 원형</span><span class="sxs-lookup"><span data-stu-id="41604-203">Apple Pie</span></span> | <span data-ttu-id="41604-204">어머니의 원형에만 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-204">Second only to your mom's pie.</span></span> | <span data-ttu-id="41604-205">12.99</span><span class="sxs-lookup"><span data-stu-id="41604-205">12.99</span></span> |
    | <span data-ttu-id="41604-206">Pecan 원형</span><span class="sxs-lookup"><span data-stu-id="41604-206">Pecan Pie</span></span> | <span data-ttu-id="41604-207">Pecans 원한다 면이입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-207">If you like pecans, this is for you.</span></span> | <span data-ttu-id="41604-208">10.99</span><span class="sxs-lookup"><span data-stu-id="41604-208">10.99</span></span> |
    | <span data-ttu-id="41604-209">레몬 원형</span><span class="sxs-lookup"><span data-stu-id="41604-209">Lemon Pie</span></span> | <span data-ttu-id="41604-210">세계에서 가장 좋은 lemons 사용해 서 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-210">Made with the best lemons in the world.</span></span> | <span data-ttu-id="41604-211">11.99</span><span class="sxs-lookup"><span data-stu-id="41604-211">11.99</span></span> |
    | <span data-ttu-id="41604-212">컵 케이크</span><span class="sxs-lookup"><span data-stu-id="41604-212">Cupcakes</span></span> | <span data-ttu-id="41604-213">자녀가 및에서 kid이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-213">Your kids and the kid in you will love these.</span></span> | <span data-ttu-id="41604-214">7.99</span><span class="sxs-lookup"><span data-stu-id="41604-214">7.99</span></span> |

    <span data-ttu-id="41604-215">에 대 한 어떤 것도 입력할 필요가 없습니다 기억는 *Id* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-215">Remember that you don't have to enter anything for the *Id* column.</span></span> <span data-ttu-id="41604-216">만들 때의 *Id* 설정 하면 열을 해당 **Id** 속성을 자동으로 입력을 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-216">When you created the *Id* column, you set its **Is Identity** property to true, which causes it to automatically be filled in.</span></span>

    <span data-ttu-id="41604-217">데이터 입력이 완료 되 면 테이블 디자이너는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-217">When you're finished entering the data, the table designer will look like this:</span></span>

    ![[image]](5-working-with-data/_static/image3.jpg)
4. <span data-ttu-id="41604-219">데이터베이스 데이터를 포함 하는 탭을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-219">Close the tab that contains the database data.</span></span>

## <a name="displaying-data-from-a-database"></a><span data-ttu-id="41604-220">데이터베이스에서 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="41604-220">Displaying Data from a Database</span></span>

<span data-ttu-id="41604-221">에 데이터가 있는 데이터베이스 했으면, ASP.NET 웹 페이지에서 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-221">Once you've got a database with data in it, you can display the data in an ASP.NET web page.</span></span> <span data-ttu-id="41604-222">표시할 테이블 행을 선택 하려면 명령을 데이터베이스에 전달 하는 SQL 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-222">To select the table rows to display, you use a SQL statement, which is a command that you pass to the database.</span></span>

1. <span data-ttu-id="41604-223">왼쪽된 창에서 클릭 된 **파일** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-223">In the left pane, click the **Files** workspace.</span></span>
2. <span data-ttu-id="41604-224">웹 사이트의 루트에 있는 라는 새로운 CSHTML 페이지 생성 *ListProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-224">In the root of the website, create a new CSHTML page named *ListProducts.cshtml*.</span></span>
3. <span data-ttu-id="41604-225">기존 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41604-225">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    <span data-ttu-id="41604-226">열은 첫 번째 코드 블록에는 *SmallBakery.sdf* 앞에서 만든 파일 (데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="41604-226">In the first code block, you open the *SmallBakery.sdf* file (database) that you created earlier.</span></span> <span data-ttu-id="41604-227">`Database.Open` 메서드 가정 하는 *.sdf* 파일은 웹 사이트의 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-227">The `Database.Open` method assumes that the *.sdf* file is in your website's *App\_Data* folder.</span></span> <span data-ttu-id="41604-228">(는 지정할 필요가 없습니다는 *.sdf* 확장 &#8212; 이렇게 하면 실제로 `Open` 메서드 작동 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="41604-228">(Notice that you don't need to specify the *.sdf* extension &#8212; in fact, if you do, the `Open` method won't work.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="41604-229">*앱\_데이터* 폴더는 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-229">The *App\_Data* folder is a special folder in ASP.NET that's used to store data files.</span></span> <span data-ttu-id="41604-230">자세한 내용은 참조 [데이터베이스에 연결](#SB_ConnectingToADatabase) 이 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-230">For more information, see [Connecting to a Database](#SB_ConnectingToADatabase) later in this article.</span></span>

    <span data-ttu-id="41604-231">다음 SQL을 사용 하 여 데이터베이스를 쿼리 하는 요청 커졌을 `Select` 문:</span><span class="sxs-lookup"><span data-stu-id="41604-231">You then make a request to query the database using the following SQL `Select` statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    <span data-ttu-id="41604-232">문에서 `Product` 쿼리에 테이블을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-232">In the statement, `Product` identifies the table to query.</span></span> <span data-ttu-id="41604-233">`*` 문자 지정 하면 쿼리 테이블에서 모든 열을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-233">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="41604-234">(또한를 나열할 수 열 개별적으로 열 중 일부만 표시 하려는 경우 쉼표로 구분 합니다.) `Order By` 절에서 데이터를 정렬 해야 하는 방법을 나타냅니다. &#8212; 하 여이 경우는 *이름* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-234">(You could also list columns individually, separated by commas, if you wanted to see only some of the columns.) The `Order By` clause indicates how the data should be sorted &#8212; in this case, by the *Name* column.</span></span> <span data-ttu-id="41604-235">즉, 데이터의 값에 따라 사전순으로 정렬 되는 *이름* 각 행에 대 한 열입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-235">This means that the data is sorted alphabetically based on the value of the *Name* column for each row.</span></span>

    <span data-ttu-id="41604-236">페이지 본문 태그 데이터를 표시 하는 데 사용 될 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41604-236">In the body of the page, the markup creates an HTML table that will be used to display the data.</span></span> <span data-ttu-id="41604-237">내부는 `<tbody>` 요소를 사용는 `foreach` 루프 개별적으로 쿼리에 의해 반환 되는 각 데이터 행을 가져오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-237">Inside the `<tbody>` element, you use a `foreach` loop to individually get each data row that's returned by the query.</span></span> <span data-ttu-id="41604-238">각 데이터 행에 대 한 HTML 표 행 만들면 (`<tr>` 요소).</span><span class="sxs-lookup"><span data-stu-id="41604-238">For each data row, you create an HTML table row (`<tr>` element).</span></span> <span data-ttu-id="41604-239">다음 HTML 테이블 셀을 만듭니다 (`<td>` 요소) 각 열에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-239">Then you create HTML table cells (`<td>` elements) for each column.</span></span> <span data-ttu-id="41604-240">에 루프를 계속 실행 될 때마다 데이터베이스에서 사용 가능한 다음 행은는 `row` 변수 (이에서 설정한는 `foreach` 문).</span><span class="sxs-lookup"><span data-stu-id="41604-240">Each time you go through the loop, the next available row from the database is in the `row` variable (you set this up in the `foreach` statement).</span></span> <span data-ttu-id="41604-241">사용할 수는 행의 개별 열을 가져오려면 `row.Name` 또는 `row.Description` 또는 원하는 모든 이름 열입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-241">To get an individual column from the row, you can use `row.Name` or `row.Description` or whatever the name is of the column you want.</span></span>
4. <span data-ttu-id="41604-242">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-242">Run the page in a browser.</span></span> <span data-ttu-id="41604-243">(있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.) 페이지에는 다음과 같은 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-243">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays a list like the following:</span></span>

    ![[image]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="41604-245">**구조적된 쿼리 언어 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="41604-245">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="41604-246">SQL은 데이터베이스의에서 데이터를 관리 하기 위한 대부분의 관계형 데이터베이스에서 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-246">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="41604-247">데이터를 검색 하 고, 업데이트 하 고 만들고 수정 하 고 데이터베이스 테이블을 관리 하도록 하는 명령이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-247">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage database tables.</span></span> <span data-ttu-id="41604-248">SQL (예: WebMatrix에서 사용 하는 것) 프로그래밍 언어와 다르면 sql 개념은 원하는 데이터베이스에 알립니다 하 고 데이터베이스의 작업 데이터를 가져오거나 작업을 수행 하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="41604-248">SQL is different than a programming language (like the one you're using in WebMatrix) because with SQL, the idea is that you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="41604-249">다음은 몇 가지 SQL 명령의 예로 및 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-249">Here are examples of some SQL commands and what they do:</span></span>
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="41604-250">이 인출는 *Id*, *이름*, 및 *가격* 의 레코드에서 열은 *제품* 경우 테이블의 값 *가격* 10을 초과 하면 이며 결과의 값에 따라 알파벳 순서로 반환 된 *이름* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-250">This fetches the *Id*, *Name*, and *Price* columns from records in the *Product* table if the value of *Price* is more than 10, and returns the results in alphabetical order based on the values of the *Name* column.</span></span> <span data-ttu-id="41604-251">이 명령은 일치 하는 레코드가 없는 경우, 조건을 또는 빈 집합을 충족 하는 레코드를 포함 하는 결과 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-251">This command will return a result set that contains the records that meet the criteria, or an empty set if no records match.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> <span data-ttu-id="41604-252">에 새 레코드를 삽입는 *제품* 설정 테이블에서 *이름* 열을 &quot;크 라 상&quot;, *설명* 열&quot; 잘 끊어지는 기쁨&quot;, 1.99에 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-252">This inserts a new record into the *Product* table, setting the *Name* column to &quot;Croissant&quot;, the *Description* column to &quot;A flaky delight&quot;, and the price to 1.99.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> <span data-ttu-id="41604-253">이 명령은에서 레코드를 삭제는 *제품* 테이블 열이 있는 만료 날짜는 2008 년 1 월 1 일 보다 이전입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-253">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="41604-254">(있다고 가정은 *제품* 테이블에 이러한 열이 물론.) MM/DD/YYYY 형식으로 날짜를 여기서 입력 하지만 로캘에 사용 되는 형식으로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-254">(This assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="41604-255">`Insert Into` 및 `Delete` 명령 결과 집합을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-255">The `Insert Into` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="41604-256">대신, 이러한 명령에 의해 영향을 받은 레코드 수를 알려 주는 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-256">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="41604-257">이러한 작업 (예: 레코드 삽입 및 삭제)의 일부에 대 한 작업을 요청 하는 프로세스는 데이터베이스에 대 한 적절 한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-257">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="41604-258">이 인해 프로덕션 데이터베이스는 데이터베이스에 연결할 때 사용자 이름 및 암호를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-258">This is why for production databases you often have to supply a username and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="41604-259">SQL 명령의 수십 있지만 이와 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="41604-259">There are dozens of SQL commands, but they all follow a pattern like this.</span></span> <span data-ttu-id="41604-260">SQL 명령을 사용 하 여 테이블을 만들고 데이터베이스, 테이블에서 레코드의 수를 계산, 가격을 계산 보다 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-260">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>


## <a name="inserting-data-in-a-database"></a><span data-ttu-id="41604-261">데이터베이스에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="41604-261">Inserting Data in a Database</span></span>

<span data-ttu-id="41604-262">이 섹션에서는 사용자가 새 제품을 추가할 수 있는 페이지를 만드는 방법을 보여 줍니다.는 *제품* 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-262">This section shows how to create a page that lets users add a new product to the *Product* database table.</span></span> <span data-ttu-id="41604-263">새 제품 레코드를 삽입 한 후 페이지에 표시 됩니다 사용 하 여 업데이트 된 테이블의 *ListProducts.cshtml* 이전 섹션에서 만든 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-263">After a new product record is inserted, the page displays the updated table using the *ListProducts.cshtml* page that you created in the previous section.</span></span>

<span data-ttu-id="41604-264">사용자가 입력 한 데이터는 데이터베이스에 대 한 유효한 지 확인 하려면 유효성 검사를 포함 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-264">The page includes validation to make sure that the data that the user enters is valid for the database.</span></span> <span data-ttu-id="41604-265">예를 들어 코드 페이지에서를 통해 필요한 모든 열에 대해 입력 된 값.</span><span class="sxs-lookup"><span data-stu-id="41604-265">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>

1. <span data-ttu-id="41604-266">웹 사이트에서 라는 새 CSHTML 파일을 만들어 *InsertProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-266">In the website, create a new CSHTML file named *InsertProducts.cshtml*.</span></span>
2. <span data-ttu-id="41604-267">기존 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41604-267">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    <span data-ttu-id="41604-268">페이지 본문 이름, 설명 및 가격을 입력할 수 있도록 하는 세 가지 텍스트 상자를 사용 하 여 HTML 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-268">The body of the page contains an HTML form with three text boxes that let users enter a name, description, and price.</span></span> <span data-ttu-id="41604-269">사용자가 클릭 하면는 **삽입** 단추, 페이지 맨 위에 있는 코드에 대 한 연결 열립니다는 *SmallBakery.sdf* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-269">When users click the **Insert** button, the code at the top of the page opens a connection to the *SmallBakery.sdf* database.</span></span> <span data-ttu-id="41604-270">사용자가 사용 하 여 전송 하는 값을 가져온 후의 `Request` 개체를 로컬 변수에 해당 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-270">You then get the values that the user has submitted by using the `Request` object and assign those values to local variables.</span></span>

    <span data-ttu-id="41604-271">필요한 각 열에 대 한 사용자 값을 입력 했는지 확인을 위해 등록할 각 `<input>` 유효성을 검사 하려는 요소:</span><span class="sxs-lookup"><span data-stu-id="41604-271">To validate that the user entered a value for each required column, you register each `<input>` element that you want to validate:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    <span data-ttu-id="41604-272">`Validation` 도우미 각에 등록 한 필드에 값이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-272">The `Validation` helper checks that there is a value in each of the fields that you've registered.</span></span> <span data-ttu-id="41604-273">모든 필드를 확인 하 여 유효성 검사를 통과 했는지 여부를 테스트할 수 있습니다 `Validation.IsValid()`이며 일반적으로 수행한 사용자에 게 서 얻은 정보를 처리 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="41604-273">You can test whether all the fields passed validation by checking `Validation.IsValid()`, which you typically do before you process the information you get from the user:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    <span data-ttu-id="41604-274">(의 `&&` 연산자 의미 AND-이 테스트는 *양식을 제출 하 여 이며 모든 필드가 유효성 검사를 통과 한 경우*.)</span><span class="sxs-lookup"><span data-stu-id="41604-274">(The `&&` operator means AND — this test is *If this is a form submission AND all the fields have passed validation*.)</span></span>

    <span data-ttu-id="41604-275">모든 열의 유효성을 검사 하는 경우 (none 비어 있던), 계속 진행 하 고 데이터를 삽입 한 후 다음 표시 된 것 처럼 실행 하는 SQL 문을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41604-275">If all the columns validated (none were empty), you go ahead and create a SQL statement to insert the data and then execute it as shown next:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    <span data-ttu-id="41604-276">삽입할 값을 매개 변수 자리 표시자 포함 (`@0`, `@1`, `@2`).</span><span class="sxs-lookup"><span data-stu-id="41604-276">For the values to insert, you include parameter placeholders (`@0`, `@1`, `@2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="41604-277">보안을 위해 항상 값을 전달할 매개 변수를 사용 하 여 SQL 문을 앞의 예제에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-277">As a security precaution, always pass values to a SQL statement using parameters, as you see in the preceding example.</span></span> <span data-ttu-id="41604-278">이렇게 하면 사용자의 데이터 유효성을 검사할 수 있을 뿐 아니라 데이터베이스 (SQL 삽입 공격 이라고 함)에 악의적인 명령이 보내려는 시도 방지는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-278">This gives you a chance to validate the user's data, plus it helps protect against attempts to send malicious commands to your database (sometimes referred to as SQL injection attacks).</span></span>

    <span data-ttu-id="41604-279">쿼리를 실행 하려면이 문을 사용의 자리 표시자를 대체할 값을 포함 하는 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-279">To execute the query, you use this statement, passing to it the variables that contain the values to substitute for the placeholders:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    <span data-ttu-id="41604-280">후의 `Insert Into` 문이 실행,이 줄을 사용 하 여 제품을 나열 하는 페이지에는 사용자에 게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41604-280">After the `Insert Into` statement has executed, you send the user to the page that lists the products using this line:</span></span>

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    <span data-ttu-id="41604-281">유효성 검사에 성공 하지 않은 삽입을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="41604-281">If validation didn't succeed, you skip the insert.</span></span> <span data-ttu-id="41604-282">누적 된 오류 메시지 (있는 경우)를 표시할 수 있는 페이지에는 도우미를가 하는 대신,</span><span class="sxs-lookup"><span data-stu-id="41604-282">Instead, you have a helper in the page that can display the accumulated error messages (if any):</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    <span data-ttu-id="41604-283">태그에 스타일 블록 라는 CSS 클래스 정의 포함 되도록 공지 `.validation-summary-errors`합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-283">Notice that the style block in the markup includes a CSS class definition named `.validation-summary-errors`.</span></span> <span data-ttu-id="41604-284">이 대해 기본적으로 사용 되는 CSS 클래스의 이름이 `<div>` 유효성 검사 오류가 포함 된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-284">This is the name of the CSS class that's used by default for the `<div>` element that contains any validation errors.</span></span> <span data-ttu-id="41604-285">유효성 검사 요약 오류 빨간색으로 표시 되 고 굵게 표시 된, 있지만 정의할 수 있습니다는 CSS 클래스 지정 하는 경우에 `.validation-summary-errors` 클래스를 원하는 서식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-285">In this case, the CSS class specifies that validation summary errors are displayed in red and in bold, but you can define the `.validation-summary-errors` class to display any formatting you like.</span></span>

### <a name="testing-the-insert-page"></a><span data-ttu-id="41604-286">삽입 페이지를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-286">Testing the Insert Page</span></span>

1. <span data-ttu-id="41604-287">브라우저에서 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-287">View the page in a browser.</span></span> <span data-ttu-id="41604-288">페이지에는 다음 그림에 나와 있는 것과 유사한 양식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-288">The page displays a form that's similar to the one that's shown in the following illustration.</span></span>

    ![[image]](5-working-with-data/_static/image5.jpg)
2. <span data-ttu-id="41604-290">모든 열에 대 한 값을 입력 합니다. 하지만 남겨 두어야는 *가격* 열은 비워 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-290">Enter values for all the columns, but make sure that you leave the *Price* column blank.</span></span>
3. <span data-ttu-id="41604-291">**삽입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-291">Click **Insert**.</span></span> <span data-ttu-id="41604-292">다음 그림에 나와 있는 것 처럼 페이지는 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-292">The page displays an error message, as shown in the following illustration.</span></span> <span data-ttu-id="41604-293">(새 레코드가 생성 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="41604-293">(No new record is created.)</span></span>

    ![[image]](5-working-with-data/_static/image6.jpg)
4. <span data-ttu-id="41604-295">완전히 양식을 작성 하 고 클릭 **삽입**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-295">Fill the form out completely, and then click **Insert**.</span></span> <span data-ttu-id="41604-296">이 이번에는 *ListProducts.cshtml* 페이지가 표시 되 고 새 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-296">This time, the *ListProducts.cshtml* page is displayed and shows the new record.</span></span>

## <a name="updating-data-in-a-database"></a><span data-ttu-id="41604-297">데이터베이스의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="41604-297">Updating Data in a Database</span></span>

<span data-ttu-id="41604-298">데이터를 테이블에을 입력 한 후 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-298">After data has been entered into a table, you might need to update it.</span></span> <span data-ttu-id="41604-299">이 절차에서는 이전에 데이터 삽입을 위해 만든 것과 비슷한 두 개의 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41604-299">This procedure shows you how to create two pages that are similar to the ones you created for data insertion earlier.</span></span> <span data-ttu-id="41604-300">첫 번째 페이지 제품을 표시 하 고 사용자가 변경 하려면 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-300">The first page displays products and lets users select one to change.</span></span> <span data-ttu-id="41604-301">두 번째 페이지에는 사용자가 실제로 편집 하 고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-301">The second page lets the users actually make the edits and save them.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="41604-302">**중요 한** 프로덕션 웹 사이트의 하면 일반적으로 제한할 수 있는 사용자는 데이터를 변경 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-302">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="41604-303">멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자를 인증 하는 방법에 대 한 정보를 참조 하십시오. [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-303">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="41604-304">웹 사이트에서 라는 새 CSHTML 파일을 만들어 *EditProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-304">In the website, create a new CSHTML file named *EditProducts.cshtml*.</span></span>
2. <span data-ttu-id="41604-305">파일에서 기존 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41604-305">Replace the existing markup in the file with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    <span data-ttu-id="41604-306">이 페이지 간의 유일한 차이점 및 *ListProducts.cshtml* 페이지에서 이전 버전은이 페이지의 HTML 테이블 포함 하는 별도 열을 표시 하는 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-306">The only difference between this page and the *ListProducts.cshtml* page from earlier is that the HTML table in this page includes an extra column that displays an **Edit** link.</span></span> <span data-ttu-id="41604-307">이 링크를 클릭 하면에 걸리는 *UpdateProducts.cshtml* 페이지 (다음 만들게) 선택된 된 레코드를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-307">When you click this link, it takes you to the *UpdateProducts.cshtml* page (which you'll create next) where you can edit the selected record.</span></span>

    <span data-ttu-id="41604-308">만드는 코드는 **편집** 링크:</span><span class="sxs-lookup"><span data-stu-id="41604-308">Look at the code that creates the **Edit** link:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    <span data-ttu-id="41604-309">이렇게 하면 HTML 만들어집니다 `<a>` 요소 인 `href` 특성은 동적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-309">This creates an HTML `<a>` element whose `href` attribute is set dynamically.</span></span> <span data-ttu-id="41604-310">`href` 특성 링크를 클릭할 때 표시할 페이지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-310">The `href` attribute specifies the page to display when the user clicks the link.</span></span> <span data-ttu-id="41604-311">또한 전달 된 `Id` 링크에는 현재 행의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-311">It also passes the `Id` value of the current row to the link.</span></span> <span data-ttu-id="41604-312">페이지를 실행 하는 경우 페이지 소스 이와 같은 링크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-312">When the page runs, the page source might contain links like these:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    <span data-ttu-id="41604-313">다음에 유의 `href` 특성이로 설정 된 `UpdateProducts/n`여기서 *n* 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-313">Notice that the `href` attribute is set to `UpdateProducts/n`, where *n* is a product number.</span></span> <span data-ttu-id="41604-314">사용자가이 링크 중 하나를 클릭 하면 결과 URL 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-314">When a user clicks one of these links, the resulting URL will look something like this:</span></span>

    `http://localhost:18816/UpdateProducts/6`

    <span data-ttu-id="41604-315">즉, 제품 번호를 편집할 수는 URL에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-315">In other words, the product number to be edited will be passed in the URL.</span></span>
3. <span data-ttu-id="41604-316">브라우저에서 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-316">View the page in a browser.</span></span> <span data-ttu-id="41604-317">페이지는 다음과 같은 형식으로 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-317">The page displays the data in a format like this:</span></span>

    ![[image]](5-working-with-data/_static/image7.jpg)

    <span data-ttu-id="41604-319">다음으로, 사용자가 실제로 데이터를 업데이트할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41604-319">Next, you'll create the page that lets users actually update the data.</span></span> <span data-ttu-id="41604-320">업데이트 페이지는 사용자가 입력 데이터 유효성 검사에 유효성 검사를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-320">The update page includes validation to validate the data that the user enters.</span></span> <span data-ttu-id="41604-321">예를 들어 코드 페이지에서를 통해 필요한 모든 열에 대해 입력 된 값.</span><span class="sxs-lookup"><span data-stu-id="41604-321">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>
4. <span data-ttu-id="41604-322">웹 사이트에서 라는 새 CSHTML 파일을 만들어 *UpdateProducts.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-322">In the website, create a new CSHTML file named *UpdateProducts.cshtml*.</span></span>
5. <span data-ttu-id="41604-323">파일에서 기존 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41604-323">Replace the existing markup in the file with the following.</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    <span data-ttu-id="41604-324">페이지의 본문에서 제품이 표시 되 고 사용자가 편집할 수 있는 HTML 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-324">The body of the page contains an HTML form where a product is displayed and where users can edit it.</span></span> <span data-ttu-id="41604-325">표시할 제품을 가져오려면이 SQL 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-325">To get the product to display, you use this SQL statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    <span data-ttu-id="41604-326">그러면에 전달 되는 값과 일치 하는 ID를 가진 제품 선택은 `@0` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-326">This will select the product whose ID matches the value that's passed in the `@0` parameter.</span></span> <span data-ttu-id="41604-327">(때문에 *Id* 기본 키 고 따라서 반드시 하나의 제품 레코드 현재까지 선택할 수 있습니다 이러한 방식으로, 고유 합니다.) 이를 전달 하는 ID 값을 가져올 `Select` 문을 다음 구문을 사용 하는 URL의 일부분으로 페이지에 전달 되는 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-327">(Because *Id* is the primary key and therefore must be unique, only one product record can ever be selected this way.) To get the ID value to pass to this `Select` statement, you can read the value that's passed to the page as part of the URL, using the following syntax:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    <span data-ttu-id="41604-328">사용 제품 레코드를 실제로 페치 하려면는 `QuerySingle` 메서드 포함 된 단일 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-328">To actually fetch the product record, you use the `QuerySingle` method, which will return just one record:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    <span data-ttu-id="41604-329">에 단일 행이 반환 되는 `row` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-329">The single row is returned into the `row` variable.</span></span> <span data-ttu-id="41604-330">각 열에서 데이터를 가져올 수 있고 다음과 같이 지역 변수에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-330">You can get data out of each column and assign it to local variables like this:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    <span data-ttu-id="41604-331">폼에 대 한 태그에서 이러한 값 표시 됩니다 자동으로 개별 텍스트 상자에 다음과 같은 포함 된 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41604-331">In the markup for the form, these values are displayed automatically in individual text boxes by using embedded code like the following:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    <span data-ttu-id="41604-332">코드의 해당 부분 업데이트 될 제품 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-332">That part of the code displays the product record to be updated.</span></span> <span data-ttu-id="41604-333">레코드가 표시 된 사용자 개별 열 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-333">Once the record has been displayed, the user can edit individual columns.</span></span>

    <span data-ttu-id="41604-334">사용자가 클릭 하 여 폼을 제출할 때는 **업데이트** 단추를 코드에는 `if(IsPost)` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-334">When the user submits the form by clicking the **Update** button, the code in the `if(IsPost)` block runs.</span></span> <span data-ttu-id="41604-335">사용자의 값을 가져옵니다이 `Request` 개체를 변수에서 값을 저장 하 고 각 열 채워져 있는지 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-335">This gets the user's values from the `Request` object, stores the values in variables, and validates that each column has been filled in.</span></span> <span data-ttu-id="41604-336">유효성 검사에 통과 하는 경우 코드를 다음 SQL Update 문을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41604-336">If validation passes, the code creates the following SQL Update statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    <span data-ttu-id="41604-337">SQL에서 `Update` 업데이트를 설정 하려면 값과 각 열을 지정 문입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-337">In a SQL `Update` statement, you specify each column to update and the value to set it to.</span></span> <span data-ttu-id="41604-338">이 코드에서는 값 매개 변수 자리 표시자를 사용 하 여 지정 된 `@0`, `@1`, `@2`등입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-338">In this code, the values are specified using the parameter placeholders `@0`, `@1`, `@2`, and so on.</span></span> <span data-ttu-id="41604-339">(보안을 위해 앞에서 설명한 것 처럼 항상 값을 전달 해야 SQL 문에 매개 변수를 사용 하 여.)</span><span class="sxs-lookup"><span data-stu-id="41604-339">(As noted earlier, for security, you should always pass values to a SQL statement by using parameters.)</span></span>

    <span data-ttu-id="41604-340">호출 하는 경우는 `db.Execute` SQL 문의 매개 변수에 해당 하는 순서로 값이 포함 된 변수를 전달할 메서드를:</span><span class="sxs-lookup"><span data-stu-id="41604-340">When you call the `db.Execute` method, you pass the variables that contain the values in the order that corresponds to the parameters in the SQL statement:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    <span data-ttu-id="41604-341">후의 `Update` 문이 실행 된 사용자 편집 페이지를 다시 리디렉션합니다 하기 위해 다음 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-341">After the `Update` statement has been executed, you call the following method in order to redirect the user back to the edit page:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    <span data-ttu-id="41604-342">사용자 데이터베이스에 있는 데이터의 업데이트 된 프로그램 목록에 게 표시 하 고 다른 제품을 편집할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-342">The effect is that the user sees an updated listing of the data in the database and can edit another product.</span></span>
6. <span data-ttu-id="41604-343">페이지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-343">Save the page.</span></span>
7. <span data-ttu-id="41604-344">실행 된 *EditProducts.cshtml* 페이지 (업데이트 페이지 제외)을 클릭 한 다음 **편집** 편집할 제품을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-344">Run the *EditProducts.cshtml* page (not the update page) and then click **Edit** to select a product to edit.</span></span> <span data-ttu-id="41604-345">*UpdateProducts.cshtml* 선택한 레코드를 보여 주는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-345">The *UpdateProducts.cshtml* page is displayed, showing the record you selected.</span></span>

    ![[image]](5-working-with-data/_static/image8.jpg)
8. <span data-ttu-id="41604-347">클릭 하 여 변경한 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-347">Make a change and click **Update**.</span></span> <span data-ttu-id="41604-348">업데이트 된 데이터와 제품 목록은 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-348">The products list is shown again with your updated data.</span></span>

## <a name="deleting-data-in-a-database"></a><span data-ttu-id="41604-349">데이터베이스의 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-349">Deleting Data in a Database</span></span>

<span data-ttu-id="41604-350">이 섹션에서는 사용자가 제품에서 삭제 하는 방법을 보여 줍니다.는 *제품* 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-350">This section shows how to let users delete a product from the *Product* database table.</span></span> <span data-ttu-id="41604-351">이 예제는 두 페이지로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-351">The example consists of two pages.</span></span> <span data-ttu-id="41604-352">첫 번째 페이지에서 사용자는 삭제할 레코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-352">In the first page, users select a record to delete.</span></span> <span data-ttu-id="41604-353">삭제할 레코드는 레코드를 삭제할 것인지 확인 수 있는 두 번째 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-353">The record to be deleted is then displayed in a second page that lets them confirm that they want to delete the record.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="41604-354">**중요 한** 프로덕션 웹 사이트의 하면 일반적으로 제한할 수 있는 사용자는 데이터를 변경 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-354">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="41604-355">멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자 권한을 부여 하는 방법에 대 한 정보를 참조 하십시오. [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-355">For information about how to set up membership and about ways to authorize user to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="41604-356">웹 사이트에서 라는 새 CSHTML 파일을 만들어 *ListProductsForDelete.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-356">In the website, create a new CSHTML file named *ListProductsForDelete.cshtml*.</span></span>
2. <span data-ttu-id="41604-357">기존 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41604-357">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    <span data-ttu-id="41604-358">이 페이지는 비슷합니다는 *EditProducts.cshtml* 앞에서 페이지.</span><span class="sxs-lookup"><span data-stu-id="41604-358">This page is similar to the *EditProducts.cshtml* page from earlier.</span></span> <span data-ttu-id="41604-359">그러나 표시 하는 대신는 **편집** 링크 각 제품에 대 한 표시는 **삭제** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-359">However, instead of displaying an **Edit** link for each product, it displays a **Delete** link.</span></span> <span data-ttu-id="41604-360">**삭제** 링크가 포함된 된 다음 코드를 사용 하 여 태그에 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-360">The **Delete** link is created using the following embedded code in the markup:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    <span data-ttu-id="41604-361">사용자가 링크를 클릭할 때 다음과 같은 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41604-361">This creates a URL that looks like this when users click the link:</span></span>

    `http://<server>/DeleteProduct/4`

    <span data-ttu-id="41604-362">라는 페이지를 호출 하는 URL *DeleteProduct.cshtml* (만들게 다음)를 삭제 하는 제품의 ID를 전달 하 고 (여기서 4).</span><span class="sxs-lookup"><span data-stu-id="41604-362">The URL calls a page named *DeleteProduct.cshtml* (which you'll create next) and passes it the ID of the product to delete (here, 4).</span></span>
3. <span data-ttu-id="41604-363">파일을 저장 하지만 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="41604-363">Save the file, but leave it open.</span></span>
4. <span data-ttu-id="41604-364">명명 된 다른 CHTML 파일을 만들 *DeleteProduct.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-364">Create another CHTML file named *DeleteProduct.cshtml*.</span></span> <span data-ttu-id="41604-365">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41604-365">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    <span data-ttu-id="41604-366">이 페이지에서 호출 됩니다 *ListProductsForDelete.cshtml* 제품 삭제를 확인 하는 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-366">This page is called by *ListProductsForDelete.cshtml* and lets users confirm that they want to delete a product.</span></span> <span data-ttu-id="41604-367">삭제 될 제품을 나열 하려면 ID를 가져옵니다는 제품의 URL에서 삭제 하려면 다음 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41604-367">To list the product to be deleted, you get the ID of the product to delete from the URL using the following code:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    <span data-ttu-id="41604-368">다음 페이지 실제로 레코드를 삭제 하는 단추를 클릭 하 여 사용자에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-368">The page then asks the user to click a button to actually delete the record.</span></span> <span data-ttu-id="41604-369">이 중요 한 보안 조치: 업데이트 또는 삭제 데이터 같은 웹 사이트의 중요 한 작업을 수행할 때는 이러한 작업 수행 항상 GET 작업 아님 POST 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-369">This is an important security measure: when you perform sensitive operations in your website like updating or deleting data, these operations should always be done using a POST operation, not a GET operation.</span></span> <span data-ttu-id="41604-370">GET 작업을 사용 하 여 삭제 작업을 수행할 수 있도록 사이트는 설치 하 고, 경우에 같은 URL을 전달할 수 누구나 `http://<server>/DeleteProduct/4` 하 고 원하는 모든 항목을 데이터베이스에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-370">If your site is set up so that a delete operation can be performed using a GET operation, anyone can pass a URL like `http://<server>/DeleteProduct/4` and delete anything they want from your database.</span></span> <span data-ttu-id="41604-371">확인을 추가 하 고 POST를 사용 하 여 삭제를 수행할 수 있도록 페이지를 코딩 하 여 사이트에 보안을 유지할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-371">By adding the confirmation and coding the page so that the deletion can be performed only by using a POST, you add a measure of security to your site.</span></span>

    <span data-ttu-id="41604-372">실제 삭제 작업은 먼저 확인 하는 post 작업 인지 하 고 ID 비어 있지 하는 다음 코드를 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-372">The actual delete operation is performed using the following code, which first confirms that this is a post operation and that the ID isn't empty:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    <span data-ttu-id="41604-373">코드에 지정된 된 레코드를 삭제 하 고 다음 사용자 목록 페이지를 다시 리디렉션합니다 하는 SQL 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-373">The code runs a SQL statement that deletes the specified record and then redirects the user back to the listing page.</span></span>
5. <span data-ttu-id="41604-374">실행 *ListProductsForDelete.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-374">Run *ListProductsForDelete.cshtml* in a browser.</span></span>

    ![[image]](5-working-with-data/_static/image9.jpg)
6. <span data-ttu-id="41604-376">클릭는 **삭제** 제품 중 하나에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-376">Click the **Delete** link for one of the products.</span></span> <span data-ttu-id="41604-377">*DeleteProduct.cshtml* 해당 레코드를 삭제 하도록 확인 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41604-377">The *DeleteProduct.cshtml* page is displayed to confirm that you want to delete that record.</span></span>
7. <span data-ttu-id="41604-378">클릭는 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-378">Click the **Delete** button.</span></span> <span data-ttu-id="41604-379">제품 레코드가 삭제 되 고 업데이트 된 제품 목록과 함께 페이지가 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="41604-379">The product record is deleted and the page is refreshed with an updated product listing.</span></span>

> [!TIP] 
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a><span data-ttu-id="41604-380">데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="41604-380">Connecting to a Database</span></span>
> 
> <span data-ttu-id="41604-381">두 가지 방법으로 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-381">You can connect to a database in two ways.</span></span> <span data-ttu-id="41604-382">첫 번째 사용 하는 것의 `Database.Open` 메서드 및 데이터베이스 파일의 이름을 지정 하려면 (덜는 *.sdf* 확장):</span><span class="sxs-lookup"><span data-stu-id="41604-382">The first is to use the `Database.Open` method and to specify the name of the database file (less the *.sdf* extension):</span></span>
> 
> `var db = Database.Open("SmallBakery");`
> 
> <span data-ttu-id="41604-383">`Open` 메서드 가정 하는. *sdf* 파일은 웹 사이트의 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-383">The `Open` method assumes that the .*sdf* file is in the website's *App\_Data* folder.</span></span> <span data-ttu-id="41604-384">이 폴더는 데이터를 보유를 위해 특별히 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-384">This folder is designed specifically for holding data.</span></span> <span data-ttu-id="41604-385">예를 들어 웹 사이트에 데이터를 읽고 쓰는 데 적절 한 권한을 보유 하 고 보안 조치로, WebMatrix 액세스가 허용 되지 않습니다 파일에이 폴더에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-385">For example, it has appropriate permissions to allow the website to read and write data, and as a security measure, WebMatrix does not allow access to files from this folder.</span></span>
> 
> <span data-ttu-id="41604-386">두 번째 방법은 연결 문자열을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-386">The second way is to use a connection string.</span></span> <span data-ttu-id="41604-387">연결 문자열을 데이터베이스에 연결 하는 방법에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-387">A connection string contains information about how to connect to a database.</span></span> <span data-ttu-id="41604-388">파일 경로 포함할 수 있습니다이 또는 사용자 이름 및 해당 서버에 연결 하는 데 암호와 함께 로컬 또는 원격 서버에 SQL Server 데이터베이스의 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-388">This can include a file path, or it can include the name of a SQL Server database on a local or remote server, along with a user name and password to connect to that server.</span></span> <span data-ttu-id="41604-389">(중앙에서 관리 되는 버전의 SQL Server에서 데이터를 유지 하는 경우와 같은 호스팅 공급자의 사이트에서 항상는 연결 문자열을 사용 하면 데이터베이스 연결 정보를 지정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="41604-389">(If you keep data in a centrally managed version of SQL Server, such as on a hosting provider's site, you always use a connection string to specify the database connection information.)</span></span>
> 
> <span data-ttu-id="41604-390">WebMatrix에서 연결 문자열은 일반적으로 저장 이라는 XML 파일 *Web.config*합니다. 사용할 수 있습니다 이름에서 알 수 있듯이 *Web.config* 사이트 필요할 수 있는 모든 연결 문자열을 포함 하 여 사이트의 구성 정보를 저장 하 여 웹 사이트의 루트에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-390">In WebMatrix, connection strings are usually stored in an XML file named *Web.config*. As the name implies, you can use a *Web.config* file in the root of your website to store the site's configuration information, including any connection strings that your site might require.</span></span> <span data-ttu-id="41604-391">연결 문자열의 예는 *Web.config* 파일 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41604-391">An example of a connection string in a *Web.config* file might look like the following:</span></span>
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> <span data-ttu-id="41604-392">예제에서는 연결 문자열의 임의 위치에 서버에서 실행 되는 SQL Server 인스턴스에서 데이터베이스를 가리키지만 (로컬 달리 *.sdf* 파일).</span><span class="sxs-lookup"><span data-stu-id="41604-392">In the example, the connection string points to a database in an instance of SQL Server that's running on a server somewhere (as opposed to a local *.sdf* file).</span></span> <span data-ttu-id="41604-393">에 대 한 적절 한 이름으로 대체 해야 `myServer` 및 `myDatabase`, SQL Server 로그인 값을 지정 하 고 `username` 및 `password`합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-393">You would need to substitute the appropriate names for `myServer` and `myDatabase`, and specify SQL Server login values for `username` and `password`.</span></span> <span data-ttu-id="41604-394">(사용자 이름 및 암호 값이 다르면 반드시 동일한 호스팅 공급자가 제공한 서버에 로그인 하기 위한 값 또는 Windows 자격 증명으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-394">(The username and password values are not necessarily the same as your Windows credentials or as the values that your hosting provider has given you for logging in to their servers.</span></span> <span data-ttu-id="41604-395">관리자를 확인 해야 하는 정확한 값에 대 한.)</span><span class="sxs-lookup"><span data-stu-id="41604-395">Check with the administrator for the exact values you need.)</span></span>
> 
> <span data-ttu-id="41604-396">`Database.Open` 메서드는 데이터베이스의 이름을 전달할 수 있기 때문에 유연 하 고, *.sdf* 에 저장 된 연결 문자열의 이름 또는 파일의 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-396">The `Database.Open` method is flexible, because it lets you pass either the name of a database *.sdf* file or the name of a connection string that's stored in the *Web.config* file.</span></span> <span data-ttu-id="41604-397">다음 예제에서는 이전 예제에서 설명 하는 연결 문자열을 사용 하 여 데이터베이스에 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41604-397">The following example shows how to connect to the database using the connection string illustrated in the previous example:</span></span>
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> <span data-ttu-id="41604-398">에서 설명한 것 처럼는 `Database.Open` 메서드를 사용 하면 데이터베이스 이름 또는 연결 문자열을 전달 하 고 사용 하는 그림 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-398">As noted, the `Database.Open` method lets you pass either a database name or a connection string, and it'll figure out which to use.</span></span> <span data-ttu-id="41604-399">배포할 때이 매우 유용할 (게시) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-399">This is very useful when you deploy (publish) your website.</span></span> <span data-ttu-id="41604-400">사용할 수는 *.sdf* 파일에 *앱\_데이터* 개발 하 고 사이트를 테스트 하는 경우 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-400">You can use an *.sdf* file in the *App\_Data* folder when you're developing and testing your site.</span></span> <span data-ttu-id="41604-401">프로덕션 서버에 사이트를 이동 하면에서 연결 문자열을 사용할 수 있습니다는 *Web.config* 으로 동일한 이름을 가진 파일을 여 *.sdf* 했지만 해당 호스팅 공급자의 가리키는 &#8212;없이 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-401">Then when you move your site to a production server, you can use a connection string in the *Web.config* file that has the same name as your *.sdf* file but that points to the hosting provider's database &#8212; all without having to change your code.</span></span>
> 
> <span data-ttu-id="41604-402">마지막으로, 연결 문자열을 직접 사용 하려는 경우를 호출할 수 있습니다는 `Database.OpenConnectionString` 메서드와 패스에 하나의 이름 대신 실제 연결 문자열이 하는 것은 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="41604-402">Finally, if you want to work directly with a connection string, you can call the `Database.OpenConnectionString` method and pass it the actual connection string instead of just the name of one in the *Web.config* file.</span></span> <span data-ttu-id="41604-403">이 몇 가지 이유로 없는 연결 문자열에 대 한 액세스 하는 경우에 유용할 수 있습니다 (또는,와 같은 값을 *.sdf* 파일 이름) 페이지가 실행 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-403">This might be useful in situations where for some reason you don't have access to the connection string (or values in it, such as the *.sdf* file name) until the page is running.</span></span> <span data-ttu-id="41604-404">그러나 대부분의 시나리오에 사용할 수 있습니다 `Database.Open` 이 문서에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="41604-404">However, for most scenarios, you can use `Database.Open` as described in this article.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="41604-405">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="41604-405">Additional Resources</span></span>

- [<span data-ttu-id="41604-406">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="41604-406">SQL Server Compact</span></span>](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [<span data-ttu-id="41604-407">SQL Server 또는 WebMatrix의 MySQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="41604-407">Connecting to a SQL Server or MySQL Database in WebMatrix</span></span>](https://go.microsoft.com/fwlink/?LinkId=208661)
- [<span data-ttu-id="41604-408">ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="41604-408">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
