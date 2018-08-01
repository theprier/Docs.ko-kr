---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: '반복 #6-테스트 기반 개발 (VB)를 사용 하 여. | Microsoft Docs'
author: microsoft
description: 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복 하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 5108e427025f42424c2dc6b657806544f9f8eeaa
ms.sourcegitcommit: a25b572eaed21791230c85416f449f66a405ec19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2018
ms.locfileid: "39396116"
---
<a name="iteration-6--use-test-driven-development-vb"></a><span data-ttu-id="7b20b-104">반복 #6-사용 하 여 테스트 기반 개발 (VB)</span><span class="sxs-lookup"><span data-stu-id="7b20b-104">Iteration #6 – Use test-driven development (VB)</span></span>
====================
<span data-ttu-id="7b20b-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7b20b-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7b20b-106">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="7b20b-106">Download Code</span></span>](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> <span data-ttu-id="7b20b-107">이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="7b20b-108">이 반복에서는 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-108">In this iteration, we add contact groups.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="7b20b-109">연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (VB)</span><span class="sxs-lookup"><span data-stu-id="7b20b-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>
  

<span data-ttu-id="7b20b-110">이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="7b20b-111">연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="7b20b-112">여러 반복에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="7b20b-113">각 반복에서 점진적으로 응용 프로그램을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="7b20b-114">이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="7b20b-115">반복 #1-응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="7b20b-116">첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="7b20b-117">기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="7b20b-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="7b20b-118">반복 #2-보기 좋게 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="7b20b-119">이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="7b20b-120">반복 #3-양식 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="7b20b-121">세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="7b20b-122">사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="7b20b-123">또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="7b20b-124">반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="7b20b-125">이 네 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="7b20b-126">예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="7b20b-127">반복 #5-단위 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="7b20b-128">다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="7b20b-129">데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="7b20b-130">반복 #6-테스트 중심 개발을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="7b20b-131">이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="7b20b-132">이 반복에서는 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="7b20b-133">반복 #7 – Ajax 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="7b20b-134">일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="7b20b-135">이 반복</span><span class="sxs-lookup"><span data-stu-id="7b20b-135">This Iteration</span></span>

<span data-ttu-id="7b20b-136">연락처 관리자 응용 프로그램의 이전 반복에서 코드에 대 한 안전망을 제공 하는 단위 테스트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="7b20b-137">단위 테스트를 만들기 위한 동기 코드를 변경 하려면 복원 력이 더욱 높아집니다 확인 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="7b20b-138">곳에서 단위 테스트를 사용 하 여에서는 문제 없이 코드를 변경 하 고 기존 기능이 손상 여부는 곧바로 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="7b20b-139">이 반복 단위 테스트는 완전히 다른 용도로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="7b20b-140">이 반복 호출 하는 응용 프로그램 디자인 철학의 일부로 단위 테스트 사용 *테스트 기반 개발*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="7b20b-141">테스트 기반 개발을 연습 하는 경우 먼저 테스트를 작성 하 고 테스트에 대해 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="7b20b-142">보다 정확 하 게 테스트 기반 개발을 실행 하는 경우 세 가지 단계 코드를 만들 때 완료 하는 (빨강 / 녹색/리팩터링):</span><span class="sxs-lookup"><span data-stu-id="7b20b-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="7b20b-143">실패 (빨간색) 단위 테스트 작성</span><span class="sxs-lookup"><span data-stu-id="7b20b-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="7b20b-144">단위 테스트 (녹색)를 전달 하는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="7b20b-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="7b20b-145">(리팩터링) 코드를 리팩터링</span><span class="sxs-lookup"><span data-stu-id="7b20b-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="7b20b-146">먼저 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-146">First, you write the unit test.</span></span> <span data-ttu-id="7b20b-147">단위 테스트 코드를 예상 하는 방법에 대 한 동작을 의도 표현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="7b20b-148">단위 테스트를 처음 만들 때 단위 테스트 실패 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="7b20b-149">테스트를 충족 하는 응용 프로그램 코드를 작성 하지 않은 때문에 테스트가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="7b20b-150">다음으로 단위 테스트를 위해 충분 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="7b20b-151">목표 laziest, sloppiest 및 가능한 가장 빠른 방법으로 코드를 작성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="7b20b-152">응용 프로그램의 아키텍처에 대 한 시간 생각을 허비 하지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="7b20b-153">대신, 최소한의 단위 테스트에 의해 표현 하려는 의도 충족 하는 데 필요한 코드 작성에 집중 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="7b20b-154">마지막으로 충분 한 코드를 작성 한 후 뒤로 이동 하 고 응용 프로그램의 전반적인 아키텍처 고려 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="7b20b-155">(리팩터링)를 다시 작성할 때이 단계에서는 소프트웨어 디자인의 장점을 활용 하 여 코드 패턴-리포지토리 패턴-같은 코드를 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="7b20b-156">단위 테스트에서 코드 검사는 때문에이 단계에서는 코드 거침 없이 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="7b20b-157">테스트 중심 개발 연습에서 발생 하는 많은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="7b20b-158">첫 번째 테스트 기반 개발을 강제로 실제로 작성 해야 하는 코드 작성에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="7b20b-159">특정 테스트를 통과 하는 데 충분 한 코드 작성에 지속적으로 포커스가 있는, 때문에 엄청난 양의 사용 하지는 않는 코드를 쓰고 근본 원인을 제거 들어가게에서 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="7b20b-160">둘째, "먼저 테스트" 디자인 방법론을 강제로 코드를 사용 하는 방법의 관점에서 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="7b20b-161">즉, 테스트 기반 개발을 실행 하는 경우 지속적으로 작성 하는 테스트 사용자 관점에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="7b20b-162">따라서 깔끔하고 더 이해할 수 있는 Api 테스트 기반 개발 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="7b20b-163">마지막으로 테스트 기반 개발을 강제로 응용 프로그램을 작성 하는 일반적인 프로세스의 일부로 단위 테스트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="7b20b-164">프로젝트 최종 기한이 가까워지면 테스트는 일반적으로 창 이동 하는 첫 번째 가장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="7b20b-165">테스트 기반 개발을 캡처하므로 반면에 때는 테스트 기반 개발을 통해 단위 테스트 중앙 응용 프로그램을 빌드하는 프로세스 때문에 단위 테스트를 작성 하는 방법에 대 한 원동력이 될 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7b20b-166">테스트 기반 개발에 대 한 자세한 내용은 필자를 읽어 Michael Feathers 책 **Working Effectively with Legacy Code**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>


<span data-ttu-id="7b20b-167">이 반복에서 연락처 관리자 응용 프로그램에 새 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="7b20b-168">메일 그룹에 대 한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-168">We add support for Contact Groups.</span></span> <span data-ttu-id="7b20b-169">연락처와 같은 범주로 연락처를 구성 하는 그룹 및 친구 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="7b20b-170">이 새로운 기능 테스트 기반 개발 프로세스를 수행 하 여 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="7b20b-171">먼저 단위 테스트를 작성 하 고 모든이 테스트에 대 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="7b20b-172">어떤 테스트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-172">What Gets Tested</span></span>

<span data-ttu-id="7b20b-173">이전 반복에서 설명한 대로 일반적으로 데이터 액세스 논리에 대 한 단위 테스트를 작성 하거나 하지 논리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="7b20b-174">데이터베이스에 액세스 하는 느린 작업 이므로 데이터 액세스 논리에 대 한 t 쓰기 단위 테스트 하지.</span><span class="sxs-lookup"><span data-stu-id="7b20b-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="7b20b-175">뷰 논리에 대 한 t 쓰기 단위 테스트 보기에 액세스 하므로 작업이 비교적 느립니다는 웹 서버를 스핀업 하지.</span><span class="sxs-lookup"><span data-stu-id="7b20b-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="7b20b-176">T 해서는 테스트 매우 빠른에 반복 해 서 실행할 수 있습니다 하지 않는 한 단위 테스트를 작성</span><span class="sxs-lookup"><span data-stu-id="7b20b-176">You shouldn t write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="7b20b-177">테스트 기반 개발, 단위 테스트에 고정 하기 때문에 집중 처음 컨트롤러 및 비즈니스 논리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="7b20b-178">에서는 데이터베이스 또는 뷰를 변경 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7b20b-178">We avoid touching the database or views.</span></span> <span data-ttu-id="7b20b-179">T 땀이 자습서의 끝까지이 뷰를 만들거나 데이터베이스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-179">We won t modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="7b20b-180">테스트할 무엇부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="7b20b-181">사용자 스토리 만들기</span><span class="sxs-lookup"><span data-stu-id="7b20b-181">Creating User Stories</span></span>

<span data-ttu-id="7b20b-182">테스트 기반 개발을 실행 하는 경우 항상 테스트를 작성 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="7b20b-183">즉시 질문을 제기 합니다: 먼저 작성 하는 테스트를 어떻게 결정 하나요?</span><span class="sxs-lookup"><span data-stu-id="7b20b-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="7b20b-184">이 질문에 답하기 위해 집합이 써야 [ *사용자 스토리*](http://en.wikipedia.org/wiki/User_stories)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-184">To answer this question, you should write a set of [*user stories*](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="7b20b-185">사용자 스토리는 소프트웨어 요구 사항 (일반적으로 한 문장) 설명은 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="7b20b-186">사용자 관점에서 작성 하는 요구 사항에 대 한 기술적인 설명을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="7b20b-187">새 메일 그룹 기능에 필요한 기능을 설명 하는 사용자 스토리 집합 s는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="7b20b-188">사용자 연락처 그룹 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="7b20b-189">사용자는 새 메일 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="7b20b-190">기존 연락처 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="7b20b-191">새 연락처를 만들 때 사용자 연락처 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="7b20b-192">기존 연락처를 편집할 때 사용자 연락처 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="7b20b-193">인덱스 보기에 연락처 그룹 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="7b20b-194">사용자가 연락처 그룹을 클릭 하면 일치 연락처 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="7b20b-195">이 목록은 사용자 스토리는 고객에 의해 완전히 이해할 수 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="7b20b-196">기술 구현 세부 정보에 대 한 언급이 없는 경우</span><span class="sxs-lookup"><span data-stu-id="7b20b-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="7b20b-197">응용 프로그램을 빌드하는 단계에서 사용자 스토리 집합을 더 구체화 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="7b20b-198">사용자 스토리 (요구 사항) 여러 스토리로 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="7b20b-199">예를 들어, 새 연락처 그룹을 만드는 해야 한다는 유효성 검사를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="7b20b-200">이름이 없는 연락처 그룹 제출 유효성 검사 오류를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="7b20b-201">사용자 스토리의 목록을 만든 후 첫 번째 단위 테스트를 작성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="7b20b-202">연락처 그룹의 목록 보기에 대 한 단위 테스트를 만들어 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="7b20b-203">연락처 그룹 나열</span><span class="sxs-lookup"><span data-stu-id="7b20b-203">Listing Contact Groups</span></span>

<span data-ttu-id="7b20b-204">이 첫 번째 사용자 스토리 된다는 사용자는 연락처 그룹 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="7b20b-205">테스트를 사용 하 여이 스토리를 표현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-205">We need to express this story with a test.</span></span>

<span data-ttu-id="7b20b-206">ContactManager.Tests 프로젝트에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 여 새 단위 테스트를 만들 선택 **추가, 새 테스트**를 선택 하는 **단위 테스트** 템플릿 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="7b20b-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="7b20b-207">이름을 새 단위 테스트 GroupControllerTest.vb을 클릭 합니다 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-207">Name the new unit test GroupControllerTest.vb and click the **OK** button.</span></span>


<span data-ttu-id="7b20b-208">[![GroupControllerTest 단위 테스트를 추가합니다.](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span></span>

<span data-ttu-id="7b20b-209">**그림 01**: GroupControllerTest 단위 테스트 추가 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image2.png))</span></span>


<span data-ttu-id="7b20b-210">첫 번째 단위 테스트는 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="7b20b-211">이 테스트 그룹 컨트롤러의 index () 메서드 그룹 집합을 반환 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="7b20b-212">이 테스트는 그룹의 컬렉션은 보기에 반환 된 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="7b20b-213">**1-Controllers\GroupControllerTest.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="7b20b-213">**Listing 1 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

<span data-ttu-id="7b20b-214">목록 1 Visual Studio에서 코드를 처음 입력 하면 빨간색의 구불구불한 선 많이 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="7b20b-215">클래스는 GroupController 또는 그룹을 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="7b20b-216">T도 빌드가 하시면이 시점에서 응용 프로그램 t 수 있도록 첫 번째 단위 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="7b20b-217">좋은 s입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-217">That s good.</span></span> <span data-ttu-id="7b20b-218">실패 한 테스트로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-218">That counts as a failing test.</span></span> <span data-ttu-id="7b20b-219">따라서 이제 응용 프로그램 코드 작성을 시작할 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="7b20b-220">테스트를 실행 하려면 충분 한 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="7b20b-221">목록 2에서 그룹 컨트롤러 클래스의 단위 테스트를 통과 하는 데 필요한 코드는 최소 사항만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="7b20b-222">Index () 작업 그룹 (그룹 클래스는 목록 3에서 정의 됩니다.)의 정적으로 코딩 된 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="7b20b-223">**Listing 2 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-223">**Listing 2 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

<span data-ttu-id="7b20b-224">**3-Models\Group.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="7b20b-224">**Listing 3 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

<span data-ttu-id="7b20b-225">첫 번째 단위 테스트를 성공적으로 완료 GroupController 및 그룹 클래스를 프로젝트에 추가 했습니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="7b20b-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="7b20b-226">수행한 테스트를 통과 하는 데 필요한 최소 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="7b20b-227">축 하 하기 위해 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-227">It is time to celebrate.</span></span>


<span data-ttu-id="7b20b-228">[![성공 했습니다.](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-228">[![Success!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span></span>

<span data-ttu-id="7b20b-229">**그림 02**: 성공! ( [클릭 하 여 큰 이미지 보기](iteration-6-use-test-driven-development-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image4.png))</span></span>


## <a name="creating-contact-groups"></a><span data-ttu-id="7b20b-230">메일 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="7b20b-230">Creating Contact Groups</span></span>

<span data-ttu-id="7b20b-231">이제 두 번째 사용자 스토리에으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="7b20b-232">새 메일 그룹을 만들 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="7b20b-233">테스트를 사용 하 여이 의도 표현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="7b20b-234">목록 4에서 테스트 메서드는 새 그룹을 사용 하 여 index () 메서드에 의해 반환 되는 그룹 목록에 그룹을 추가 하는 create () 호출 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="7b20b-235">즉, 새 그룹을 만드는 경우 다음 필자 있어야 index () 메서드에 의해 반환 되는 그룹 목록에서 새 그룹을 다시 가져오는 데 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="7b20b-236">**4-Controllers\GroupControllerTest.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="7b20b-236">**Listing 4 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

<span data-ttu-id="7b20b-237">목록 4의 테스트 그룹 컨트롤러 새 연락처 그룹을 사용 하 여 create () 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="7b20b-238">다음으로 테스트 그룹 컨트롤러 index () 메서드 호출에서 반환 하는 새 그룹 데이터 보기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="7b20b-239">수정 된 그룹 컨트롤러 목록 5에 새 테스트를 통과 하는 데 필요한 변경 하는 최소 사항만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="7b20b-240">**Listing 5 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-240">**Listing 5 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="7b20b-241">그룹 컨트롤러 목록 5의 새 create () 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="7b20b-242">이 작업 그룹의 컬렉션에 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="7b20b-243">Index () 작업 그룹 컬렉션의 내용을 반환 수정 되었다는 사실을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="7b20b-244">다시 한 번 최소한 단위 테스트를 통과 하는 데 필요한 작업의 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="7b20b-245">그룹 컨트롤러에 이러한 변경을 수행, 후 모든 유닛 테스트를 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="7b20b-246">유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="7b20b-246">Adding Validation</span></span>

<span data-ttu-id="7b20b-247">이 요구 사항은 사용자 스토리에 명시적으로 언급 하지.</span><span class="sxs-lookup"><span data-stu-id="7b20b-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="7b20b-248">그러나 그룹 이름에 포함 하려면 적절 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="7b20b-249">그렇지 않으면 연락처를 그룹으로 구성 됩니다 하지 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="7b20b-250">코드 6이이 의도 표현 하는 새 테스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="7b20b-251">이 테스트에 유효성 검사 오류 메시지가 모델 상태에서 이름 결과 제공 하지 않고 그룹을 만들려고 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="7b20b-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

<span data-ttu-id="7b20b-253">이 테스트를 충족 하기 위해 그룹 클래스 (참조 코드 7)에 Name 속성을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="7b20b-254">또한 그룹 컨트롤러 create () 작업 (참조 코드 8) s에 짤막한 유효성 검사 논리를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="7b20b-255">**7-Models\Group.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="7b20b-255">**Listing 7 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

<span data-ttu-id="7b20b-256">**Listing 8 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-256">**Listing 8 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

<span data-ttu-id="7b20b-257">이제 create () 작업 그룹 컨트롤러 논리 유효성 검사 및 데이터베이스를 모두 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="7b20b-258">현재 그룹 컨트롤러에서 사용 하는 데이터베이스의 메모리 내 컬렉션을 이상의 아무 것도 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="7b20b-259">리팩터링 하는 시간</span><span class="sxs-lookup"><span data-stu-id="7b20b-259">Time to Refactor</span></span>

<span data-ttu-id="7b20b-260">리팩터링 부분은 빨강/녹색/리팩터링 하는 세 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="7b20b-261">이 시점에서 해야 코드에서 다시 실행 하 고 해당 디자인을 개선 하기 위해 응용 프로그램을 리팩터링할 수 있습니다 하는 방법을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="7b20b-262">리팩터링 단계는 소프트웨어 설계 원칙과 패턴을 구현 하는 최상의 방법에 대 한 하드 생각 하는 단계 이며</span><span class="sxs-lookup"><span data-stu-id="7b20b-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="7b20b-263">코드의 디자인을 향상 하도록 선택한 어떤 방식으로든 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="7b20b-264">미국 기존 기능이 망가질 하지 못하도록 하는 단위 테스트의 안전망 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="7b20b-265">현재는 그룹 컨트롤러 좋은 소프트웨어 설계의 관점에서 교통이 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="7b20b-266">그룹 컨트롤러 상호 의존성이 높은 교통이 복잡 유효성 검사 및 데이터 액세스 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="7b20b-267">단일 책임 원칙을 위반을 방지 하려면 이러한 문제를 다른 클래스로 분리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="7b20b-268">리팩터링된 그룹 컨트롤러 클래스는 9 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="7b20b-269">컨트롤러는 ContactManager 서비스 계층을 사용 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="7b20b-270">이것이 연락처 컨트롤러를 사용 하 여 사용 하는 것과 동일한 서비스 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="7b20b-271">코드 10 유효성 검사, 나열 및 그룹 만들기를 지원 하기 위해 ContactManager 서비스 계층에 추가 하는 새 메서드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="7b20b-272">IContactManagerService 인터페이스는 새 메서드를 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="7b20b-273">코드 11 IContactManagerRepository 인터페이스를 구현 하는 새 FakeContactManagerRepository 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="7b20b-274">또한 IContactManagerRepository 인터페이스를 구현 하는 EntityContactManagerRepository 클래스와 달리 새 FakeContactManagerRepository 클래스 데이터베이스와 통신 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="7b20b-275">FakeContactManagerRepository 클래스는 데이터베이스에 대 한 프록시로 메모리 내 컬렉션을를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="7b20b-276">가상 repository 계층으로이 클래스는 단위 테스트에서 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="7b20b-277">**Listing 9 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-277">**Listing 9 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

<span data-ttu-id="7b20b-278">**Listing 10 - Controllers\ContactManagerService.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-278">**Listing 10 - Controllers\ContactManagerService.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

<span data-ttu-id="7b20b-279">**11-Controllers\FakeContactManagerRepository.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="7b20b-279">**Listing 11 - Controllers\FakeContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]


<span data-ttu-id="7b20b-280">인터페이스를 사용 하려면 IContactManagerRepository 수정 하는 데 CreateGroup() 메서드와 ListGroups() EntityContactManagerRepository 클래스에서 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="7b20b-281">이렇게 하려면 laziest 쉽고 빠른 방법은 다음과 같습니다. 스텁 메서드는 다음과 같은 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="7b20b-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]


<span data-ttu-id="7b20b-282">마지막으로, 이러한 응용 프로그램의 디자인이 변경 해야 단위 테스트를 약간 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="7b20b-283">이제 단위 테스트를 수행 하는 경우는 FakeContactManagerRepository를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="7b20b-284">업데이트 된 GroupControllerTest 클래스 12 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="7b20b-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

<span data-ttu-id="7b20b-286">이러한 모든 만든 후 변경 이번에 단위 테스트 통과의 모든 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="7b20b-287">빨강/녹색/리팩터링의 전체 주기 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="7b20b-288">첫 번째 두 개의 사용자 스토리를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="7b20b-289">이제 사용자 스토리에 표현 된 요구 사항에 대 한 단위 테스트를 지원 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="7b20b-290">사용자 스토리의 나머지 부분을 구현 빨강/녹색/리팩터링의 동일한 주기를 반복 하는 작업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="7b20b-291">데이터베이스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-291">Modifying our Database</span></span>

<span data-ttu-id="7b20b-292">그러나 모든 단위 테스트에서 표현 된 요구 사항을 충족 한 것에 작업 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="7b20b-293">여전히 데이터베이스를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-293">We still need to modify our database.</span></span>

<span data-ttu-id="7b20b-294">새 그룹 데이터베이스 테이블을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-294">We need to create a new Group database table.</span></span> <span data-ttu-id="7b20b-295">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-295">Follow these steps:</span></span>

1. <span data-ttu-id="7b20b-296">서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="7b20b-297">테이블 디자이너에서 아래에 설명 된 두 개의 열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="7b20b-298">Id 열을 기본 키와 Id 열으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="7b20b-299">플로피의 아이콘을 클릭 하 여 그룹의 이름 사용 하 여 새 테이블을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.12_table01"></a>


| <span data-ttu-id="7b20b-300">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="7b20b-300">**Column Name**</span></span> | <span data-ttu-id="7b20b-301">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="7b20b-301">**Data Type**</span></span> | <span data-ttu-id="7b20b-302">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="7b20b-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b20b-303">ID</span><span class="sxs-lookup"><span data-stu-id="7b20b-303">Id</span></span> | <span data-ttu-id="7b20b-304">int</span><span class="sxs-lookup"><span data-stu-id="7b20b-304">int</span></span> | <span data-ttu-id="7b20b-305">False</span><span class="sxs-lookup"><span data-stu-id="7b20b-305">False</span></span> |
| <span data-ttu-id="7b20b-306">name</span><span class="sxs-lookup"><span data-stu-id="7b20b-306">Name</span></span> | <span data-ttu-id="7b20b-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="7b20b-307">nvarchar(50)</span></span> | <span data-ttu-id="7b20b-308">False</span><span class="sxs-lookup"><span data-stu-id="7b20b-308">False</span></span> |


<span data-ttu-id="7b20b-309">다음으로, Contacts 테이블에서 모든 데이터를 삭제 해야 (땀이 고, 그렇지 t 연락처 및 그룹이 테이블 간의 관계를 만들 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won t be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="7b20b-310">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-310">Follow these steps:</span></span>

1. <span data-ttu-id="7b20b-311">Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="7b20b-312">모든 행을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-312">Delete all of the rows.</span></span>

<span data-ttu-id="7b20b-313">다음으로 그룹 데이터베이스 테이블 및 기존 연락처 데이터베이스 테이블 간의 관계를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="7b20b-314">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-314">Follow these steps:</span></span>

1. <span data-ttu-id="7b20b-315">테이블 디자이너를 열고 서버 탐색기 창에서 Contacts 테이블을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="7b20b-316">GroupId 라는 Contacts 테이블에 새 정수 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="7b20b-317">외래 키 관계 대화 상자를 열려면 관계 단추를 클릭 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="7b20b-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="7b20b-318">추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-318">Click the Add button.</span></span>
5. <span data-ttu-id="7b20b-319">테이블 및 열 사양 단추 옆에 나타나는 줄임표 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="7b20b-320">테이블 및 열 대화 상자에서 기본 키 열으로 Id와 기본 키 테이블 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="7b20b-321">GroupId 외래 키 열으로 외래 키 테이블와 연락처를 선택 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="7b20b-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="7b20b-322">확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-322">Click the OK button.</span></span>
7. <span data-ttu-id="7b20b-323">아래 **INSERT 및 UPDATE 사양**에 값을 선택 **Cascade** 에 대 한 **삭제 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="7b20b-324">외래 키 관계 대화 상자를 닫으려면 닫기 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="7b20b-325">Contacts 테이블에 변경 내용을 저장 하려면 저장 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-325">Click the Save button to save the changes to the Contacts table.</span></span>


<span data-ttu-id="7b20b-326">[![데이터베이스 테이블 관계 만들기](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span></span>

<span data-ttu-id="7b20b-327">**그림 03**: 데이터베이스 테이블 관계 만들기 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image6.png))</span></span>


<span data-ttu-id="7b20b-328">[![테이블 관계를 지정합니다.](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-328">[![Specifying table relationships](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span></span>

<span data-ttu-id="7b20b-329">**그림 04**: 테이블 관계를 지정 합니다. ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image8.png))</span></span>


### <a name="updating-our-data-model"></a><span data-ttu-id="7b20b-330">데이터 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="7b20b-330">Updating our Data Model</span></span>

<span data-ttu-id="7b20b-331">다음으로 새 데이터베이스 테이블을 나타내는 데이터 모델을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="7b20b-332">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-332">Follow these steps:</span></span>

1. <span data-ttu-id="7b20b-333">엔터티 디자이너를 열려면 모델 폴더에서 ContactManagerModel.edmx 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="7b20b-334">디자이너의 화면을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **데이터베이스에서 모델 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="7b20b-335">업데이트 마법사에서 선택한 그룹 테이블 마침을 클릭 (그림 5 참조) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="7b20b-336">그룹 엔터티를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="7b20b-337">이름을 변경 합니다 *그룹* 엔터티의 *그룹* (단일).</span><span class="sxs-lookup"><span data-stu-id="7b20b-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="7b20b-338">연락처 엔터티 맨 아래에 표시 되는 그룹 탐색 속성을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="7b20b-339">이름을 변경 합니다 *그룹* 탐색 속성을 *그룹* (단 수 화) 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>


<span data-ttu-id="7b20b-340">[![데이터베이스에서 Entity Framework 모델을 업데이트합니다.](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span></span>

<span data-ttu-id="7b20b-341">**그림 05**: 데이터베이스에서 Entity Framework 모델을 업데이트 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image10.png))</span></span>


<span data-ttu-id="7b20b-342">다음이 단계를 완료 한 후 데이터 모델에는 연락처와 그룹 모두 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="7b20b-343">Entity Designer는 엔터티를 모두 표시 됩니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="7b20b-343">The Entity Designer should show both entities (see Figure 6).</span></span>


<span data-ttu-id="7b20b-344">[![그룹 및 연락처를 표시 하는 엔터티 디자이너](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span></span>

<span data-ttu-id="7b20b-345">**그림 06**: 그룹 및 연락처를 표시 하는 Entity Designer ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image12.png))</span></span>


### <a name="creating-our-repository-classes"></a><span data-ttu-id="7b20b-346">리포지토리 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="7b20b-346">Creating our Repository Classes</span></span>

<span data-ttu-id="7b20b-347">그런 다음 리포지토리 클래스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="7b20b-348">이 반복 과정을 통해 추가한 새 메서드가 여러 개 IContactManagerRepository 인터페이스에 단위 테스트를 충족 하기 위해 코드를 작성 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="7b20b-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="7b20b-349">IContactManagerRepository 인터페이스의 최종 버전 14 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="7b20b-350">**Listing 14 - Models\IContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-350">**Listing 14 - Models\IContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

<span data-ttu-id="7b20b-351">에서는 실제 EntityContactManagerRepository 클래스에서 연락처 그룹 작업과 관련 된 방법 중 하나는 되지 않았습니까 실제로 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-351">We haven t actually implemented any of the methods related to working with contact groups in our real EntityContactManagerRepository class.</span></span> <span data-ttu-id="7b20b-352">현재 EntityContactManagerRepository 클래스에 각 IContactManagerRepository 인터페이스에 나열 된 연락처 그룹 방법에 대 한 스텁 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="7b20b-353">예를 들어 ListGroups() 메서드는 현재 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

<span data-ttu-id="7b20b-354">스텁 메서드를 사용 하면 응용 프로그램을 컴파일 및 단위 테스트를 통과 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="7b20b-355">그러나 이제는 실제로 이러한 메서드를 구현 하는 시간</span><span class="sxs-lookup"><span data-stu-id="7b20b-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="7b20b-356">EntityContactManagerRepository 클래스의 최종 버전 13 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="7b20b-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="7b20b-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a><span data-ttu-id="7b20b-358">뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="7b20b-358">Creating the Views</span></span>

<span data-ttu-id="7b20b-359">ASP.NET MVC 응용 프로그램 기본 ASP.NET 뷰 엔진을 사용 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="7b20b-360">따라서 don t는 특정 단위 테스트에 대 한 응답에 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="7b20b-361">그러나 응용 프로그램에 정보를 보기 없으면 되므로 하시면 t를 만들어 연락처 관리자 응용 프로그램에 포함 된 뷰를 수정 하지 않고이 반복을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="7b20b-362">다음 새 뷰를 만드는 데 연락처 그룹 관리를 위한 (그림 7 참조) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="7b20b-363">Views\Group\Index.aspx-연락처 그룹 목록 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="7b20b-364">Views\Group\Delete.aspx-연락처 그룹을 삭제 하는 것에 대 한 확인 양식 표시</span><span class="sxs-lookup"><span data-stu-id="7b20b-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>


<span data-ttu-id="7b20b-365">[![그룹 인덱스 보기](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-365">[![The Group Index view](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span></span>

<span data-ttu-id="7b20b-366">**그림 07**: The 그룹 인덱스 보기 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image14.png))</span></span>


<span data-ttu-id="7b20b-367">연락처 그룹 포함 되도록 다음 기존 뷰를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="7b20b-368">Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="7b20b-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="7b20b-369">Views\Home\Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="7b20b-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="7b20b-370">Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="7b20b-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="7b20b-371">이 자습서와 함께 제공 되는 Visual Studio 응용 프로그램에서 확인 하 여 수정 된 보기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="7b20b-372">예를 들어, 그림 8에서는 연락처 인덱스 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-372">For example, Figure 8 illustrates the Contact Index view.</span></span>


<span data-ttu-id="7b20b-373">[![연락처 인덱스 보기](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7b20b-373">[![The Contact Index view](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span></span>

<span data-ttu-id="7b20b-374">**그림 08**: The 연락처 인덱스 보기 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="7b20b-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image16.png))</span></span>


## <a name="summary"></a><span data-ttu-id="7b20b-375">요약</span><span class="sxs-lookup"><span data-stu-id="7b20b-375">Summary</span></span>

<span data-ttu-id="7b20b-376">이 반복에 추가한 새 기능 연락처 관리자 응용 프로그램 테스트 기반 개발 응용 프로그램 디자인 방법론을 수행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="7b20b-377">사용자 스토리의 집합을 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="7b20b-378">사용자 스토리에 의해 표현 된 요구 사항에 해당 하는 단위 테스트 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="7b20b-379">마지막으로, 단위 테스트로 표현 된 요구 사항을 충족 하도록 충분 한 코드만 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="7b20b-380">단위 테스트로 표현 된 요구 사항을 충족 하도록 충분 한 코드를 작성 끝나면 데이터베이스 및 뷰를 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="7b20b-381">데이터베이스에 새 그룹 테이블을 추가 하 고 Entity Framework 데이터 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="7b20b-382">또한 생성 하 고 뷰 집합을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="7b20b-383">다음 반복-마지막 반복-에서는 Ajax를 활용 하도록 응용 프로그램에 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="7b20b-384">Ajax를 활용 하 여 연락처 관리자 응용 프로그램의 성능과 응답성 개선 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b20b-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7b20b-385">[이전](iteration-5-create-unit-tests-vb.md)
> [다음](iteration-7-add-ajax-functionality-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7b20b-385">[Previous](iteration-5-create-unit-tests-vb.md)
[Next](iteration-7-add-ajax-functionality-vb.md)</span></span>
