---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 반복 6-테스트 기반 개발 (C#)를 사용 하 여 | Microsoft Docs
author: microsoft
description: 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복에...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: 94502625f66d3eb08a24b8f2a369bf456a3367b1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="iteration-6--use-test-driven-development-c"></a><span data-ttu-id="17ee6-104">반복 6-테스트 기반 개발 (C#)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-104">Iteration #6 – Use test-driven development (C#)</span></span>
====================
<span data-ttu-id="17ee6-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="17ee6-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="17ee6-106">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="17ee6-106">Download Code</span></span>](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> <span data-ttu-id="17ee6-107">이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="17ee6-108">이 반복 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-108">In this iteration, we add contact groups.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="17ee6-109">ASP.NET MVC 연락처 관리 응용 프로그램 (C#) 빌드</span><span class="sxs-lookup"><span data-stu-id="17ee6-109">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="17ee6-110">이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="17ee6-111">관리자에 게 문의 응용 프로그램을 사람 목록에 대 한 사용-이름, 전화 번호 및 전자 메일 주소-연락처 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="17ee6-112">여러 반복을 통해에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="17ee6-113">각 반복에서 점진적으로 응용 프로그램을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="17ee6-114">이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="17ee6-115">반복 #1-응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="17ee6-116">첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한.</span><span class="sxs-lookup"><span data-stu-id="17ee6-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="17ee6-117">기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="17ee6-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="17ee6-118">반복 #2-모양이 아닌 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="17ee6-119">이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="17ee6-120">반복 #3-폼 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="17ee6-121">세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="17ee6-122">म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="17ee6-123">또한 전자 메일 주소, 전화 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="17ee6-124">반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="17ee6-125">이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-125">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="17ee6-126">예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="17ee6-127">반복 #5-단위 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="17ee6-128">다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="17ee6-129">데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="17ee6-130">반복 6-테스트 기반 개발을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="17ee6-131">이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="17ee6-132">이 반복 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="17ee6-133">반복 #7-Ajax 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="17ee6-134">일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="17ee6-135">이 반복</span><span class="sxs-lookup"><span data-stu-id="17ee6-135">This Iteration</span></span>

<span data-ttu-id="17ee6-136">않아 응용 프로그램의 이전 반복의 코드에 대 한 안전망을 제공 하는 단위 테스트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="17ee6-137">단위 테스트를 만들기 위한 동기 코드를 변경 하려면 복원 성도 뛰어납니다. 확인 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="17ee6-138">위치에 단위 테스트도 코드를 변경 하 고 즉시 기존 기능이 손상 여부를 알아야 수 우리 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="17ee6-139">이 반복에 완전히 다른 용도 대 한 단위 테스트 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="17ee6-140">이 반복 호출 하는 응용 프로그램 디자인 원칙의 일환으로 단위 테스트 사용 *테스트 기반 개발*합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="17ee6-141">테스트 기반 개발을 연습 하는 경우에 테스트를 먼저 작성 한 다음 테스트에 대 한 코드 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="17ee6-142">보다 정확 하 게 테스트 기반 개발 연습 하는 경우 세 가지 단계 코드를 만들 때 완료 하는 (빨강 / 녹색/리팩터링):</span><span class="sxs-lookup"><span data-stu-id="17ee6-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="17ee6-143">실패 (빨간색) 되는 단위 테스트 작성</span><span class="sxs-lookup"><span data-stu-id="17ee6-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="17ee6-144">단위 테스트 (녹색)를 전달 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="17ee6-145">(리팩터링) 코드를 리팩터링</span><span class="sxs-lookup"><span data-stu-id="17ee6-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="17ee6-146">첫째, 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-146">First, you write the unit test.</span></span> <span data-ttu-id="17ee6-147">단위 테스트 코드를 예상 하는 방법에 대 한 동작을 의도 표현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="17ee6-148">단위 테스트를 처음 만들 때 단위 테스트가 실패 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="17ee6-149">테스트는 테스트를 충족 하는 모든 응용 프로그램 코드를 작성 하지 않았습니다 때문에 실패 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="17ee6-150">다음으로 전달 하는 단위 테스트를 위해 충분 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="17ee6-151">목표 laziest, sloppiest 고 가능한 가장 빠른 방법으로 코드를 작성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="17ee6-152">응용 프로그램의 아키텍처에 대 한 시간 생각을 낭비 하지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="17ee6-153">대신, 최소한의 단위 테스트로 표현 된 설정 하려는 의도 충족 하는 데 필요한 코드를 작성에 초점을 맞추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="17ee6-154">마지막으로, 충분 한 코드를 작성 한 후 실행 다시 하 고 응용 프로그램의 전반적인 아키텍처는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="17ee6-155">이 단계를 다시 작성 (리팩터링) 소프트웨어 디자인을 이용 하 여 코드 패턴-리포지토리 패턴-같은 코드를 더 쉽게 유지 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="17ee6-156">단위 테스트에서 코드 검사는 때문에이 단계에서는 코드 fearlessly 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="17ee6-157">테스트 기반 개발을 수행 하 여 발생 하는 많은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="17ee6-158">첫째, 테스트 기반 개발을 강제로 실제로 기록해 야 하는 코드에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="17ee6-159">특정 테스트를 통과 하는 데 충분 한 코드 작성에 계속 포커스가 있는, 때문에 여행 중에 나에 만난 및 대량의 결코 사용 하는 코드를 작성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="17ee6-160">둘째, "먼저 테스트" 디자인 방법론 되도록 코드를 어떻게 사용할 것의 관점에서 코드를 작성할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="17ee6-161">즉, 테스트 기반 개발 연습 지속적으로 작성 하는 경우 테스트 사용자 관점에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="17ee6-162">따라서 보다 명확 하 고 쉽게 Api 테스트 기반 개발 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="17ee6-163">마지막으로, 테스트 기반 개발을 강제로 응용 프로그램을 작성 하는 일반적인 프로세스의 일부로 단위 테스트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="17ee6-164">마감일이 다음 프로젝트에 가까워지면 테스트는 일반적으로 먼저 창의 외부로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="17ee6-165">테스트 기반 개발 연습 반면에 때는 테스트 기반 개발 하면 단위 테스트 중앙 응용 프로그램을 구축 과정에 단위 테스트를 작성 하는 방법에 대 한 원동력이 될 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="17ee6-166">테스트 기반 개발에 대 한 자세한 내용은 것이 좋습니다. Michael 페더 책을 읽어 **작업 효과적으로 레거시 코드와 함께**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>


<span data-ttu-id="17ee6-167">이 반복에 않아 응용 프로그램에 새 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="17ee6-168">메일 그룹에 대 한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-168">We add support for Contact Groups.</span></span> <span data-ttu-id="17ee6-169">비즈니스와 같은 범주로 연락처를 구성 하는 담당자 그룹 및 친구 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="17ee6-170">이 새로운 기능 테스트 기반 개발 과정을 수행 하 여 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="17ee6-171">먼저 단위 테스트 작성 합니다 및 이러한 테스트에 대 한 코드의 모든 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="17ee6-172">테스트 내용을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-172">What Gets Tested</span></span>

<span data-ttu-id="17ee6-173">이전 반복에서 설명한 대로 일반적으로 또는 하지 않는 데이터 액세스 논리에 대 한 단위 테스트를 작성 논리 보기.</span><span class="sxs-lookup"><span data-stu-id="17ee6-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="17ee6-174">데이터베이스에 액세스 하는 상대적으로 느린 작업 이므로 데이터 액세스 논리에 대 한 t 쓰기 단위 테스트를 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="17ee6-175">자신에 게 맞는 t 뷰 논리에 대 한 단위 테스트를 쓰기 때문에 보기에 액세스 하는 상대적으로 속도가 느립니다 작업 웹 서버를 회전 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="17ee6-176">T 이내에 사용 해야 테스트 매우 빠르게에 반복 해 서 다시 실행할 수 있습니다 않으면 단위 테스트를 작성</span><span class="sxs-lookup"><span data-stu-id="17ee6-176">You shouldn t write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="17ee6-177">테스트 기반 개발, 단위 테스트에 고정 하기 때문에 집중 처음 컨트롤러 및 비즈니스 논리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="17ee6-178">에서는 데이터베이스 또는 뷰를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="17ee6-178">We avoid touching the database or views.</span></span> <span data-ttu-id="17ee6-179">T 성공한 데이터베이스를 수정 하거나이 자습서의 맨 끝까지이 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-179">We won t modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="17ee6-180">가장 먼저 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="17ee6-181">사용자 스토리 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee6-181">Creating User Stories</span></span>

<span data-ttu-id="17ee6-182">테스트 기반 개발 연습 하는 경우 항상 테스트를 작성 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="17ee6-183">질문을 즉시 발생이: 어떤 테스트를 먼저 작성 어떻게 결정 합니까?</span><span class="sxs-lookup"><span data-stu-id="17ee6-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="17ee6-184">이 질문의 답 집합을 작성 해야 [ **사용자 스토리**](http://en.wikipedia.org/wiki/User_stories)합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-184">To answer this question, you should write a set of [**user stories**](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="17ee6-185">사용자 스토리가 소프트웨어 요구 사항에 매우 간단한 (일반적으로 한 문장) 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="17ee6-186">사용자 관점에서 작성 하는 요구 사항에 대 한 일반적인 설명을 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="17ee6-187">여기서 s는 새 메일 그룹 기능에 필요한 기능을 설명 하는 사용자 스토리 집합:</span><span class="sxs-lookup"><span data-stu-id="17ee6-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="17ee6-188">사용자 연락처 그룹 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="17ee6-189">새 메일 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="17ee6-190">기존 연락처 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="17ee6-191">새 연락처를 만들 때 사용자 연락처 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="17ee6-192">기존 연락처를 편집할 때 사용자 연락처 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="17ee6-193">인덱스 뷰의 연락처 그룹 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="17ee6-194">사용자가 메일 그룹을 클릭할 때 일치 연락처 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="17ee6-195">사용자 스토리의이 목록에는 고객이 완전히 이해할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="17ee6-196">기술 구현 세부 사항 언급 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="17ee6-197">응용 프로그램을 빌드하는 단계에서 사용자 스토리 집합을 더 구체화 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="17ee6-198">(요구 사항) 여러 스토리로 사용자 스토리를 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="17ee6-199">예를 들어 새 연락처 그룹을 만들면 유효성 검사 참여 시켜야 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="17ee6-200">이름이 없는 연락처 그룹 제출 유효성 검사 오류를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="17ee6-201">사용자 스토리의 목록을 만든 후 첫 번째 단위 테스트를 작성할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="17ee6-202">메일 그룹의 목록 보기에 대 한 단위 테스트를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="17ee6-203">메일 그룹 나열</span><span class="sxs-lookup"><span data-stu-id="17ee6-203">Listing Contact Groups</span></span>

<span data-ttu-id="17ee6-204">이 첫 번째 사용자 스토리는 사용자 연락처 그룹 목록을 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="17ee6-205">테스트와 함께이 스토리를 나타내는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-205">We need to express this story with a test.</span></span>

<span data-ttu-id="17ee6-206">ContactManager.Tests 프로젝트에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 여 새 단위 테스트 만들기 선택 하면 **추가, 새 테스트**을 선택 하 고는 **단위 테스트** 서식 파일 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="17ee6-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="17ee6-207">새 단위 GroupControllerTest.cs를 테스트 하 고 클릭 이름은 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-207">Name the new unit test GroupControllerTest.cs and click the **OK** button.</span></span>


<span data-ttu-id="17ee6-208">[![GroupControllerTest 단위 테스트를 추가합니다.](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span></span>

<span data-ttu-id="17ee6-209">**그림 01**: GroupControllerTest 단위 테스트 추가 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image2.png))</span></span>


<span data-ttu-id="17ee6-210">첫 번째 단위 테스트 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="17ee6-211">이 테스트 그룹 컨트롤러의 index () 메서드 그룹 집합이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="17ee6-212">테스트 그룹의 컬렉션 데이터 보기에서 반환 하 되 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="17ee6-213">**1-Controllers\GroupControllerTest.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="17ee6-213">**Listing 1 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

<span data-ttu-id="17ee6-214">Visual Studio에서 목록 1의 코드를 먼저 입력 빨간색의 구불구불한 선 많은 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="17ee6-215">지금은 작성 GroupController 또는 그룹 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="17ee6-216">T에도 빌드를 활용해 서이 시점에서 응용 프로그램을 활용해 서 t 하므로 첫 번째 단위 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="17ee6-217">좋은 s입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-217">That s good.</span></span> <span data-ttu-id="17ee6-218">실패 한 테스트로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-218">That counts as a failing test.</span></span> <span data-ttu-id="17ee6-219">따라서에서는 이제 수 있는 권한이 응용 프로그램 코드를 작성을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="17ee6-220">이 테스트를 실행할 충분 한 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="17ee6-221">목록 2의 그룹 컨트롤러 클래스는 최소한의 단위 테스트를 통과 하는 데 필요한 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="17ee6-222">Index () 작업 그룹 (그룹 클래스 보기 3에 정의 됨)의 정적으로 코딩 된 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="17ee6-223">**Listing 2 - Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-223">**Listing 2 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

<span data-ttu-id="17ee6-224">**3-Models\Group.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="17ee6-224">**Listing 3 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

<span data-ttu-id="17ee6-225">첫 번째 단위 테스트 성공적으로 완료 된 후 GroupController 및 그룹 클래스는 프로젝트에 추가 했습니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="17ee6-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="17ee6-226">테스트를 통과 하는 데 필요한 최소 작업의 경험 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="17ee6-227">축 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-227">It is time to celebrate.</span></span>


<span data-ttu-id="17ee6-228">[![성공 했습니다!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-228">[![Success!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span></span>

<span data-ttu-id="17ee6-229">**그림 02**: 성공! 드 ( [전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image4.png))</span></span>


## <a name="creating-contact-groups"></a><span data-ttu-id="17ee6-230">메일 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee6-230">Creating Contact Groups</span></span>

<span data-ttu-id="17ee6-231">이제 두 번째 사용자 스토리에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="17ee6-232">새 메일 그룹을 만들 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="17ee6-233">테스트와 함께 이러한 의도 표현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="17ee6-234">테스트 목록 4에서 새 그룹을 사용 하 여 메서드 그룹 index () 메서드에 의해 반환 된 목록에 그룹을 추가 하는 create () 호출 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="17ee6-235">즉, 새 그룹을 만드는 경우 다음 I 할 수 있어야 index () 메서드에 의해 반환 된 그룹의 목록에서 새 그룹을 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="17ee6-236">**4-Controllers\GroupControllerTest.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="17ee6-236">**Listing 4 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

<span data-ttu-id="17ee6-237">테스트 목록 4에 그룹 컨트롤러 그룹 새 연락처를 사용 하 여 create () 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="17ee6-238">다음으로 테스트 그룹 컨트롤러 index () 메서드 호출에서 반환 하는 새 그룹 보기 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="17ee6-239">수정 된 그룹 컨트롤러 목록 5에 최소한의 새 테스트를 통과 하는 데 필요한 변경 내용이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="17ee6-240">**5-Controllers\GroupController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="17ee6-240">**Listing 5 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="17ee6-241">도메인에서 그룹 컨트롤러 목록 5의 새 create () 동작을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="17ee6-242">이 작업 그룹의 컬렉션에 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="17ee6-243">그룹의 컬렉션의 내용을 반환 하는 index () 동작 수정 되었다는 사실을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="17ee6-244">다시 한 번에서는 단위 테스트를 통과 하는 데 필요한 최소 운영 체제 미 설치를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="17ee6-245">그룹 컨트롤러에 이러한 변경을 수행, 후 모든 우리의 단위 테스트를 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="17ee6-246">유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="17ee6-246">Adding Validation</span></span>

<span data-ttu-id="17ee6-247">이 요구 사항은 사용자 스토리에 명시적으로 언급 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="17ee6-248">그러나 상태일 그룹 이름을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="17ee6-249">그렇지 않으면 연락처를 그룹으로 구성 됩니다 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="17ee6-250">목록 6이이 의도 표현 하는 새 테스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="17ee6-251">이 테스트 확인 모델 상태의 유효성 검사 오류 메시지에 이름이 결과 제공 하지 않고 그룹 만들기를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="17ee6-252">**6-Controllers\GroupControllerTest.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="17ee6-252">**Listing 6 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

<span data-ttu-id="17ee6-253">이 테스트를 충족 하기 위해 Name 속성 (참조 목록 7)에서는 그룹 클래스에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="17ee6-254">또한 유효성 검사 논리의 간단한 작업이 그룹 controller s create () 동작 (8 목록 참조)에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="17ee6-255">**7-Models\Group.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="17ee6-255">**Listing 7 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

<span data-ttu-id="17ee6-256">**Listing 8 - Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-256">**Listing 8 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

<span data-ttu-id="17ee6-257">유효성 검사와 데이터베이스 논리 그룹 컨트롤러 create () 동작을 지금에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="17ee6-258">현재 그룹 컨트롤러에서 사용 되는 데이터베이스는 메모리 내 컬렉션에 다르지 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="17ee6-259">리팩터링 하는 시간</span><span class="sxs-lookup"><span data-stu-id="17ee6-259">Time to Refactor</span></span>

<span data-ttu-id="17ee6-260">빨강/녹색/리팩터링 하는 세 번째 단계는 리팩터링 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="17ee6-261">이 시점에서 응용 프로그램의 디자인을 개선 하기 위해 리팩터링할 수 있습니다 어떻게 하는 것이 좋습니다.를 코드에서 다시 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="17ee6-262">리팩터링 단계는을 소프트웨어 디자인 원칙 및 패턴을 구현 하는 가장 좋은 방법은 대 한 하드 생각 하는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="17ee6-263">코드의 디자인을 개선 하기 위해 선택 하는 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="17ee6-264">기존 기능을 분리 us를 방해 하는 단위 테스트의 안전망 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="17ee6-265">지금 바로 사용, 그룹 controller은 잘 설계 된 소프트웨어의 관점에서 정리가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="17ee6-266">그룹 컨트롤러 유효성 검사 및 데이터 액세스 코드의 혼란된 정리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="17ee6-267">단일 책임 원칙을 위반을 방지 하려면 다양 한 클래스에 이러한 문제를 분리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="17ee6-268">리팩터링된 그룹 컨트롤러 클래스 목록 9에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="17ee6-269">컨트롤러는 ContactManager 서비스 계층을 사용 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="17ee6-270">연락처 컨트롤러와 사용 하는 동일한 서비스 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="17ee6-271">목록 10 유효성 검사, 나열 및 그룹 만들기를 지원 하기 위해 ContactManager 서비스 계층에 추가 된 새 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="17ee6-272">IContactManagerService 인터페이스는 새 메서드를 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="17ee6-273">목록 11 IContactManagerRepository 인터페이스를 구현 하는 새 FakeContactManagerRepository 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="17ee6-274">또한 IContactManagerRepository 인터페이스를 구현 하는 EntityContactManagerRepository 클래스와 달리 새 FakeContactManagerRepository 클래스는 데이터베이스와 통신 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="17ee6-275">FakeContactManagerRepository 클래스는 데이터베이스에 대 한 프록시로 메모리 내 컬렉션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="17ee6-276">이 단위 테스트에서이 클래스 가짜 저장소 계층으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="17ee6-277">**Listing 9 - Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-277">**Listing 9 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

<span data-ttu-id="17ee6-278">**Listing 10 - Controllers\ContactManagerService.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-278">**Listing 10 - Controllers\ContactManagerService.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

<span data-ttu-id="17ee6-279">**Listing 11 - Controllers\FakeContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-279">**Listing 11 - Controllers\FakeContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

<span data-ttu-id="17ee6-280">인터페이스 필요 IContactManagerRepository 수정 하는 데 EntityContactManagerRepository 클래스에서 CreateGroup() 및 ListGroups() 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="17ee6-281">이렇게 하려면 laziest 및 가장 빠른 방법은 스텁 메서드는 다음과 같은 추가 하기 위해입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]


<span data-ttu-id="17ee6-282">마지막으로, 이러한 변경 내용은 응용 프로그램의 디자인에 단위 테스트를 약간 수정을 만드는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="17ee6-283">이제 단위 테스트를 수행할 때의 FakeContactManagerRepository를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="17ee6-284">업데이트 된 GroupControllerTest 클래스 12 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="17ee6-285">**Listing 12 - Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-285">**Listing 12 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

<span data-ttu-id="17ee6-286">이러한 모든 하도록 한 후 변경 다시 한 번 모두 우리의 단위 테스트 통과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="17ee6-287">빨강/녹색/리팩터링의 전체 주기를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="17ee6-288">처음 두 개의 사용자 스토리 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="17ee6-289">이제 사용자 스토리에 명시 된 요구 사항을 대 한 단위 테스트를 지원 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="17ee6-290">사용자 스토리의 나머지 부분에서는 구현 빨강/녹색/리팩터링의 동일한 사이클을 반복 하는 작업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="17ee6-291">데이터베이스 수정</span><span class="sxs-lookup"><span data-stu-id="17ee6-291">Modifying our Database</span></span>

<span data-ttu-id="17ee6-292">그러나 우리 모든 단위 테스트에서 명시 된 요구 사항을 충족 않은 경우에 작업 수행 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="17ee6-293">여전히이 데이터베이스를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-293">We still need to modify our database.</span></span>

<span data-ttu-id="17ee6-294">새 그룹 데이터베이스 테이블을 만들려면 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-294">We need to create a new Group database table.</span></span> <span data-ttu-id="17ee6-295">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-295">Follow these steps:</span></span>

1. <span data-ttu-id="17ee6-296">서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="17ee6-297">테이블 디자이너에서 아래에 설명 된 두 개의 열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="17ee6-298">Id 열 primary key와 Id 열을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="17ee6-299">이름 그룹이 포함 된 플로피 아이콘을 클릭 하 여 새 테이블을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.11_table01"></a>


| <span data-ttu-id="17ee6-300">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="17ee6-300">**Column Name**</span></span> | <span data-ttu-id="17ee6-301">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="17ee6-301">**Data Type**</span></span> | <span data-ttu-id="17ee6-302">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="17ee6-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17ee6-303">ID</span><span class="sxs-lookup"><span data-stu-id="17ee6-303">Id</span></span> | <span data-ttu-id="17ee6-304">int</span><span class="sxs-lookup"><span data-stu-id="17ee6-304">int</span></span> | <span data-ttu-id="17ee6-305">False</span><span class="sxs-lookup"><span data-stu-id="17ee6-305">False</span></span> |
| <span data-ttu-id="17ee6-306">이름</span><span class="sxs-lookup"><span data-stu-id="17ee6-306">Name</span></span> | <span data-ttu-id="17ee6-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="17ee6-307">nvarchar(50)</span></span> | <span data-ttu-id="17ee6-308">False</span><span class="sxs-lookup"><span data-stu-id="17ee6-308">False</span></span> |


<span data-ttu-id="17ee6-309">다음으로 Contacts 테이블에서 모든 데이터를 삭제 해야 (성공한 그렇지 않으면 t 연락처 및 그룹이 테이블 간의 관계를 만들 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won t be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="17ee6-310">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-310">Follow these steps:</span></span>

1. <span data-ttu-id="17ee6-311">Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="17ee6-312">모든 행을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-312">Delete all of the rows.</span></span>

<span data-ttu-id="17ee6-313">다음으로 그룹 데이터베이스 테이블 및 기존 연락처 데이터베이스 테이블 간의 관계를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="17ee6-314">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-314">Follow these steps:</span></span>

1. <span data-ttu-id="17ee6-315">테이블 디자이너를 열고 서버 탐색기 창에서 Contacts 테이블을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="17ee6-316">GroupId 라는 Contacts 테이블에 새 정수 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="17ee6-317">외래 키 관계 대화 상자를 열려면 관계 단추 클릭 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="17ee6-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="17ee6-318">추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-318">Click the Add button.</span></span>
5. <span data-ttu-id="17ee6-319">테이블 및 열 사양 단추 옆에 있는 줄임표 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="17ee6-320">테이블 및 열 대화 상자에서 기본 키 테이블 및 기본 키 열으로 Id로 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="17ee6-321">외래 키 테이블과 외래 키 열으로 GroupId로 연락처를 선택 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="17ee6-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="17ee6-322">확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-322">Click the OK button.</span></span>
7. <span data-ttu-id="17ee6-323">아래 **INSERT 및 UPDATE 사양**, 값을 선택 **Cascade** 에 대 한 **삭제 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="17ee6-324">외래 키 관계 대화 상자를 닫고 닫기 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="17ee6-325">Contacts 테이블에 변경 내용을 저장 하려면 저장 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-325">Click the Save button to save the changes to the Contacts table.</span></span>


<span data-ttu-id="17ee6-326">[![데이터베이스 테이블 관계 만들기](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span></span>

<span data-ttu-id="17ee6-327">**그림 03**: 데이터베이스 테이블 관계 만들기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image6.png))</span></span>


<span data-ttu-id="17ee6-328">[![테이블 관계를 지정합니다.](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-328">[![Specifying table relationships](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span></span>

<span data-ttu-id="17ee6-329">**그림 04**: 테이블 관계 지정 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image8.png))</span></span>


### <a name="updating-our-data-model"></a><span data-ttu-id="17ee6-330">데이터 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="17ee6-330">Updating our Data Model</span></span>

<span data-ttu-id="17ee6-331">다음으로 새 데이터베이스 테이블을 나타내기 위해 데이터 모델을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="17ee6-332">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-332">Follow these steps:</span></span>

1. <span data-ttu-id="17ee6-333">엔터티 디자이너를 열려면 모델 폴더에서 ContactManagerModel.edmx 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="17ee6-334">디자이너 화면을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **데이터베이스에서 모델 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="17ee6-335">업데이트 마법사는 테이블 그룹과 마침을 클릭 선택 (그림 5 참조) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="17ee6-336">그룹 엔터티를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="17ee6-337">이름을 변경 하는 *그룹* 엔터티를 *그룹* (단 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="17ee6-338">연락처 엔터티 맨 아래에 표시 되는 그룹 탐색 속성을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="17ee6-339">이름을 변경 하는 *그룹* 탐색 속성을 *그룹* (단 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>


<span data-ttu-id="17ee6-340">[![데이터베이스에서 Entity Framework 모델을 업데이트합니다.](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span></span>

<span data-ttu-id="17ee6-341">**그림 05**: 데이터베이스에서 Entity Framework 모델을 업데이트 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image10.png))</span></span>


<span data-ttu-id="17ee6-342">다음이 단계를 완료 한 후 데이터 모델에는 연락처와 그룹에 모두 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="17ee6-343">엔터티 디자이너에는 두 엔터티 표시 됩니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="17ee6-343">The Entity Designer should show both entities (see Figure 6).</span></span>


<span data-ttu-id="17ee6-344">[![엔터티 디자이너 그룹 및 연락처를 표시 합니다.](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span></span>

<span data-ttu-id="17ee6-345">**그림 06**: 그룹 및 연락처를 표시 하는 Entity Designer ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image12.png))</span></span>


### <a name="creating-our-repository-classes"></a><span data-ttu-id="17ee6-346">저장소 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee6-346">Creating our Repository Classes</span></span>

<span data-ttu-id="17ee6-347">다음으로, 저장소 클래스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="17ee6-348">반복이 진행 되는 동안 새 메서드가 여러 개에 추가한 IContactManagerRepository 인터페이스 단위 테스트를 충족 하기 위해 코드를 작성 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="17ee6-349">IContactManagerRepository 인터페이스의 최종 버전 14 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="17ee6-350">**Listing 14 - Models\IContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-350">**Listing 14 - Models\IContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

<span data-ttu-id="17ee6-351">에서는 연락처 그룹 작업과 관련 된 방법 중 하나는 되지 않았습니까 실제로 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-351">We haven t actually implemented any of the methods related to working with contact groups.</span></span> <span data-ttu-id="17ee6-352">현재 EntityContactManagerRepository 클래스에 각 IContactManagerRepository 인터페이스에 나열 된 메일 그룹 방법의 스텁을 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="17ee6-353">예를 들어 ListGroups() 메서드는 현재 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

<span data-ttu-id="17ee6-354">스텁 메서드를 사용 하면 응용 프로그램을 컴파일 및 단위 테스트를 통과할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="17ee6-355">그러나 이제 속도가 실제로 이러한 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="17ee6-356">EntityContactManagerRepository 클래스의 최종 버전 목록 13에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="17ee6-357">**Listing 13 - Models\EntityContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="17ee6-357">**Listing 13 - Models\EntityContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a><span data-ttu-id="17ee6-358">보기 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee6-358">Creating the Views</span></span>

<span data-ttu-id="17ee6-359">ASP.NET MVC 응용 프로그램 기본 ASP.NET 뷰 엔진을 사용 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="17ee6-360">따라서 don t는 특정 단위 테스트에 대 한 응답에 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="17ee6-361">그러나 응용 프로그램 뷰 없이 쓸모 없게, 때문에 활용해 서 t를 만들고 연락처 관리자 응용 프로그램에 포함 된 뷰를 수정 하지 않고이 반복을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="17ee6-362">뷰를 만드는 다음과 같은 새 메일 그룹을 관리 하기 위한 (그림 7 참조) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="17ee6-363">Views\Group\Index.aspx-연락처 그룹의 목록 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="17ee6-364">Views\Group\Delete.aspx-연락처 그룹을 삭제 하기 위한 표시 확인 양식</span><span class="sxs-lookup"><span data-stu-id="17ee6-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>


<span data-ttu-id="17ee6-365">[![그룹 인덱스 보기](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-365">[![The Group Index view](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span></span>

<span data-ttu-id="17ee6-366">**그림 07**: The 그룹 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image14.png))</span></span>


<span data-ttu-id="17ee6-367">메일 그룹 포함 되도록 다음 기존 뷰를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="17ee6-368">Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="17ee6-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="17ee6-369">Views\Home\Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="17ee6-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="17ee6-370">Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="17ee6-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="17ee6-371">이 자습서와 함께 제공 하는 Visual Studio 응용 프로그램을 확인 하 여 수정 된 보기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="17ee6-372">예를 들어 그림 8에서는 연락처 인덱스 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-372">For example, Figure 8 illustrates the Contact Index view.</span></span>


<span data-ttu-id="17ee6-373">[![연락처 인덱스 뷰](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="17ee6-373">[![The Contact Index view](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span></span>

<span data-ttu-id="17ee6-374">**그림 08**: The 연락처 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="17ee6-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image16.png))</span></span>


## <a name="summary"></a><span data-ttu-id="17ee6-375">요약</span><span class="sxs-lookup"><span data-stu-id="17ee6-375">Summary</span></span>

<span data-ttu-id="17ee6-376">이 반복에 추가 했습니다 새로운 기능 않아 응용 프로그램에서 테스트 기반 개발 응용 프로그램 디자인 방법을 따라.</span><span class="sxs-lookup"><span data-stu-id="17ee6-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="17ee6-377">사용자 스토리 집합을 만들어 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="17ee6-378">사용자 스토리에서 명시 된 요구 사항을에 해당 하는 단위 테스트 집합이 만들었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="17ee6-379">마지막으로, 단위 테스트에 명시 된 요구 사항을 충족 하는 데 충분 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="17ee6-380">단위 테스트에 명시 된 요구 사항을 충족 하기 위해 충분 한 코드 작성를 완료 한 후이 데이터베이스 및 뷰 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="17ee6-381">데이터베이스에 새 그룹 테이블을 추가 하 고 우리의 Entity Framework 데이터 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="17ee6-382">또한 생성 하 고 뷰 집합을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="17ee6-383">-마지막 반복-다음 반복에서 Ajax 활용 하기 위해 응용 프로그램 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="17ee6-384">Ajax 활용 함으로써 않아 응용 프로그램의 성능 및 응답성을 향상 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee6-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="17ee6-385">[이전](iteration-5-create-unit-tests-cs.md)
> [다음](iteration-7-add-ajax-functionality-cs.md)</span><span class="sxs-lookup"><span data-stu-id="17ee6-385">[Previous](iteration-5-create-unit-tests-cs.md)
[Next](iteration-7-add-ajax-functionality-cs.md)</span></span>
