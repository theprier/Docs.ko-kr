---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: '반복 #2 – 확인 응용 프로그램 모양 꾸미기 (C#) | Microsoft Docs'
author: microsoft
description: 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: 89dc31d8ab0d73aac3a79a0a942121bb9a240eb7
ms.sourcegitcommit: a25b572eaed21791230c85416f449f66a405ec19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2018
ms.locfileid: "39396142"
---
<a name="iteration-2--make-the-application-look-nice-c"></a><span data-ttu-id="f3196-103">반복 #2 – 응용 프로그램 모양 꾸미기 (C#) 확인</span><span class="sxs-lookup"><span data-stu-id="f3196-103">Iteration #2 – Make the application look nice (C#)</span></span>
====================
<span data-ttu-id="f3196-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f3196-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f3196-105">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="f3196-105">Download Code</span></span>](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> <span data-ttu-id="f3196-106">이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-106">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="f3196-107">연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (C#)</span><span class="sxs-lookup"><span data-stu-id="f3196-107">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="f3196-108">이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-108">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="f3196-109">연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-109">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="f3196-110">여러 반복에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-110">We build the application over multiple iterations.</span></span> <span data-ttu-id="f3196-111">각 반복에서 점진적으로 응용 프로그램을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-111">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="f3196-112">이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-112">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="f3196-113">반복 #1-응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-113">Iteration #1 - Create the application.</span></span> <span data-ttu-id="f3196-114">첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-114">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="f3196-115">기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="f3196-115">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="f3196-116">반복 #2-보기 좋게 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-116">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="f3196-117">이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-117">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="f3196-118">반복 #3-양식 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-118">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="f3196-119">세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-119">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="f3196-120">사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-120">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="f3196-121">또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-121">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="f3196-122">반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-122">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="f3196-123">이 네 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-123">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="f3196-124">예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-124">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="f3196-125">반복 #5-단위 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-125">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="f3196-126">다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-126">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="f3196-127">데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-127">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="f3196-128">반복 #6-테스트 중심 개발을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-128">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="f3196-129">이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-129">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="f3196-130">이 반복에서는 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-130">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="f3196-131">반복 #7 – Ajax 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-131">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="f3196-132">일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-132">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="f3196-133">이 반복</span><span class="sxs-lookup"><span data-stu-id="f3196-133">This Iteration</span></span>

<span data-ttu-id="f3196-134">이 반복의 목표는 연락처 관리자 응용 프로그램의 모양을 향상 시킬 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-134">The goal of this iteration is to improve the appearance of the Contact Manager application.</span></span> <span data-ttu-id="f3196-135">현재, Contact Manager는 기본 ASP.NET MVC 뷰 마스터 페이지 및 연계 스타일 시트 (그림 1 참조)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-135">Currently, the Contact Manager uses the default ASP.NET MVC view master page and cascading style sheet (see Figure 1).</span></span> <span data-ttu-id="f3196-136">이러한 안 불량, 보이지만 t 원하는 모든 다른 ASP.NET MVC 웹 사이트와 마찬가지로 검색할 Contact Manager 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-136">These don t look bad, but I don t want the Contact Manager to look just like every other ASP.NET MVC website.</span></span> <span data-ttu-id="f3196-137">사용자 지정 파일을 사용 하 여 이러한 파일을 대체 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-137">I want to replace these files with custom files.</span></span>


<span data-ttu-id="f3196-138">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-138">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)</span></span>

<span data-ttu-id="f3196-139">**그림 01**: ASP.NET MVC 응용 프로그램의 기본 모양을 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-139">**Figure 01**: The default appearance of an ASP.NET MVC Application ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image2.png))</span></span>


<span data-ttu-id="f3196-140">이 반복 응용 프로그램의 시각적 디자인을 향상 시키기 위한 두 가지 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-140">In this iteration, I discuss two approaches to improving the visual design of our application.</span></span> <span data-ttu-id="f3196-141">먼저 하겠습니다 무료 ASP.NET MVC 디자인 템플릿을 다운로드 하기 위해 ASP.NET MVC 디자인 갤러리를 활용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f3196-141">First, I show you how to take advantage of the ASP.NET MVC Design gallery to download a free ASP.NET MVC design template.</span></span> <span data-ttu-id="f3196-142">ASP.NET MVC 디자인 갤러리를 사용 하면 모든 작업을 수행 하지 않고 전문 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-142">The ASP.NET MVC Design gallery enables you to create a professional web application without doing any work.</span></span>

<span data-ttu-id="f3196-143">연락처 관리자 응용 프로그램에 대 한 ASP.NET MVC 디자인 갤러리에서 템플릿을 사용 하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-143">I decided to not use a template from the ASP.NET MVC Design gallery for the Contact Manager application.</span></span> <span data-ttu-id="f3196-144">대신, 전문 디자인 회사에서 만든 사용자 지정 디자인을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-144">Instead, I had a custom design created by a professional design firm.</span></span> <span data-ttu-id="f3196-145">이 자습서의 2 부에서 최종 ASP.NET MVC 디자인을 만들려면 전문 디자인 회사를 사용 하 여 필자가 하는 방법을 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-145">In the second part of this tutorial, I explain how I worked with a professional design company to create the final ASP.NET MVC design.</span></span>

## <a name="the-aspnet-mvc-design-gallery"></a><span data-ttu-id="f3196-146">ASP.NET MVC 디자인 갤러리</span><span class="sxs-lookup"><span data-stu-id="f3196-146">The ASP.NET MVC Design Gallery</span></span>

<span data-ttu-id="f3196-147">ASP.NET MVC 디자인 갤러리는 Microsoft에서 제공 하는 무료 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-147">The ASP.NET MVC Design Gallery is a free resource provided by Microsoft.</span></span> <span data-ttu-id="f3196-148">ASP.NET MVC 갤러리 다음 주소에 위치한:</span><span class="sxs-lookup"><span data-stu-id="f3196-148">The ASP.NET MVC Gallery is located at the following address:</span></span>

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

<span data-ttu-id="f3196-149">ASP.NET MVC 디자인 갤러리는 ASP.NET MVC 프로젝트에서 사용 하기 위해 생성 된 무료 웹 사이트 디자인의 컬렉션을 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-149">The ASP.NET MVC Design Gallery hosts a collection of free website designs that were created specifically for using in an ASP.NET MVC project.</span></span> <span data-ttu-id="f3196-150">디자인은 커뮤니티의 회원이 업로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-150">Designs are uploaded by members of the community.</span></span> <span data-ttu-id="f3196-151">갤러리에는 방문자가 즐겨 찾는 설계에 대해 투표할 수 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="f3196-151">Visitors to the Gallery can vote for their favorite designs (see Figure 2).</span></span>


<span data-ttu-id="f3196-152">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-152">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)</span></span>

<span data-ttu-id="f3196-153">**그림 02**: The ASP.NET MVC 디자인 갤러리 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-153">**Figure 02**: The ASP.NET MVC Design Gallery ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image4.png))</span></span>


<span data-ttu-id="f3196-154">이 자습서를 작성 하는 대로 갤러리에서 가장 인기 있는 디자인은 David Hauser 여 년 10 월 이라는 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-154">As I write this tutorial, the most popular design in the gallery is a design named October by David Hauser.</span></span> <span data-ttu-id="f3196-155">다음 단계를 완료 하 여 ASP.NET MVC 프로젝트에 대 한이 디자인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-155">You can use this design for an ASP.NET MVC project by completing the following steps:</span></span>

1. <span data-ttu-id="f3196-156">클릭 합니다 **다운로드** October.zip 파일을 컴퓨터에 다운로드 하려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-156">Click the **Download** button to download the October.zip file to your computer.</span></span>
2. <span data-ttu-id="f3196-157">다운로드 한 October.zip 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭 합니다 **차단 해제** 단추 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="f3196-157">Right-click the downloaded October.zip file and click the **Unblock** button (see Figure 3).</span></span>
3. <span data-ttu-id="f3196-158">10 월 라는 폴더에 파일을 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-158">Unzip the file to a folder named October.</span></span>
4. <span data-ttu-id="f3196-159">10 월 폴더에 포함 된 DesignTemplate 폴더에서 모든 파일을 선택 합니다. 파일을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-159">Select all of the files from the DesignTemplate folder contained in the October folder, right-click the files, and select the menu option **Copy**.</span></span>
5. <span data-ttu-id="f3196-160">Visual Studio 솔루션 탐색기 창에서 ContactManager 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **붙여넣기** (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="f3196-160">Right-click the ContactManager project node in the Visual Studio Solution Explorer window and select the menu option **Paste** (see Figure 4).</span></span>
6. <span data-ttu-id="f3196-161">Visual Studio 메뉴 옵션을 선택 **편집, 찾기 및 바꾸기, 빠른 바꾸기** 바꾸고 *[MyProjectName]* 사용 하 여 *ContactManager* (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="f3196-161">Select the Visual Studio menu option **Edit, Find and Replace, Quick Replace** and replace *[MyProjectName]* with *ContactManager* (see Figure 5).</span></span>


<span data-ttu-id="f3196-162">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-162">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)</span></span>

<span data-ttu-id="f3196-163">**그림 03**: 웹에서 다운로드 한 파일을 차단 해제 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-163">**Figure 03**: Unblocking a file downloaded from the web ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image6.png))</span></span>


<span data-ttu-id="f3196-164">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-164">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)</span></span>

<span data-ttu-id="f3196-165">**그림 04**: 솔루션 탐색기에서 파일을 덮어쓸 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-165">**Figure 04**: Overwriting files in the Solution Explorer ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image8.png))</span></span>


<span data-ttu-id="f3196-166">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-166">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)</span></span>

<span data-ttu-id="f3196-167">**그림 05**: [ProjectName] ContactManager 바꿉니다 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-167">**Figure 05**: Replacing [ProjectName] with ContactManager ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image10.png))</span></span>


<span data-ttu-id="f3196-168">다음이 단계를 완료 한 후 웹 응용 프로그램의 새로운 디자인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-168">After you complete these steps, your web application will use the new design.</span></span> <span data-ttu-id="f3196-169">그림 6에서 페이지 년 10 월 디자인을 사용 하 여 연락처 관리자 응용 프로그램의 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-169">The page in Figure 6 illustrates the appearance of the Contact Manager application with the October design.</span></span>


<span data-ttu-id="f3196-170">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-170">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)</span></span>

<span data-ttu-id="f3196-171">**그림 06**: ContactManager 년 10 월 템플릿 사용 하 여 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-171">**Figure 06**: ContactManager with the October template ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image12.png))</span></span>


## <a name="creating-a-custom-aspnet-mvc-design"></a><span data-ttu-id="f3196-172">사용자 지정 ASP.NET MVC 디자인 만들기</span><span class="sxs-lookup"><span data-stu-id="f3196-172">Creating a Custom ASP.NET MVC Design</span></span>

<span data-ttu-id="f3196-173">ASP.NET MVC 디자인 갤러리에는 다양 한 디자인 스타일 좋은 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-173">The ASP.NET MVC Design Gallery has a good selection of different design styles.</span></span> <span data-ttu-id="f3196-174">갤러리는 ASP.NET MVC 응용 프로그램의 모양을 사용자 지정할 수 있는 간편한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-174">The Gallery provides you with a painless way to customize the appearance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="f3196-175">그리고 물론 갤러리에 큰 장점이 완전히 무료로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-175">And, of course, the Gallery has the big advantage of being completely free.</span></span>

<span data-ttu-id="f3196-176">그러나 웹 사이트에 대 한 완전히 고유한 설계를 만들 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-176">However, you might need to create a completely unique design for your website.</span></span> <span data-ttu-id="f3196-177">이런 경우는 웹 사이트 디자인 회사를 사용 하려면 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-177">In that case, it makes sense to work with a website design company.</span></span> <span data-ttu-id="f3196-178">연락처 관리자 응용 프로그램 디자인에 대 한이 방법을 사용 하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-178">I decided to take this approach for the design for the Contact Manager application.</span></span>

<span data-ttu-id="f3196-179">반복 # 1의 연락처 관리자를 압축 하 고 프로젝트 디자인 회사에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-179">I zipped up the Contact Manager from Iteration #1 and sent the project to the design company.</span></span> <span data-ttu-id="f3196-180">이러한 동작 t 문제가 없는 (아깝다는 에서도!), Visual Studio를 소유 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-180">They did not own Visual Studio (shame on them!), but that didn t present a problem.</span></span> <span data-ttu-id="f3196-181">Microsoft Visual Web Developer를 무료로 다운로드할 수 있었습니다 합니다 [ https://www.asp.net ](https://www.asp.net) 웹 사이트 및 Visual Web Developer에서 연락처 관리자 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-181">They were able to download Microsoft Visual Web Developer for free from the [https://www.asp.net](https://www.asp.net) website and open the Contact Manager application in Visual Web Developer.</span></span> <span data-ttu-id="f3196-182">몇 일, 이러한 그림 7의 설계를 생성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-182">In a couple of days, they had produced the design in Figure 7.</span></span>


<span data-ttu-id="f3196-183">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-183">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)</span></span>

<span data-ttu-id="f3196-184">**그림 07**: ASP.NET MVC Contact Manager 디자인 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-184">**Figure 07**: The ASP.NET MVC Contact Manager Design ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image14.png))</span></span>


<span data-ttu-id="f3196-185">두 개의 주 파일의 새 디자인은: 새 연계 스타일 시트 파일 및 새 보기 마스터 페이지 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-185">The new design consisted of two main files: a new cascading style sheet file and a new view master page file.</span></span> <span data-ttu-id="f3196-186">보기 마스터 페이지 레이아웃 및 ASP.NET MVC 응용 프로그램의 보기에 대 한 공유 콘텐츠를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-186">A view master page contains the layout and shared content for views in an ASP.NET MVC application.</span></span> <span data-ttu-id="f3196-187">예를 들어, 보기 마스터 페이지 그림 7에 헤더, 탐색 탭 및 표시 되는 바닥글을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-187">For example, the view master page includes the header, navigation tabs, and footer that appear in Figure 7.</span></span> <span data-ttu-id="f3196-188">Views\Shared 폴더에서 기존 Site.Master 뷰 마스터 페이지 디자인 회사에서 새 Site.Master 파일을 사용 하 여 덮어쓴 있나요</span><span class="sxs-lookup"><span data-stu-id="f3196-188">I overwrote the existing Site.Master view master page in the Views\Shared folder with the new Site.Master file from the design company,</span></span>

<span data-ttu-id="f3196-189">디자인 회사 연계 하는 새 스타일 시트 및 이미지 집합에도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-189">The design company also created a new cascading style sheet and set of images.</span></span> <span data-ttu-id="f3196-190">콘텐츠 폴더에 이러한 새 파일을 배치 하 고 기존 Site.css 파일을 덮어썼습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-190">I placed these new files in the Content folder and overwrote the existing Site.css file.</span></span> <span data-ttu-id="f3196-191">콘텐츠 폴더에 모든 정적 콘텐츠를 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-191">You should place all static content in the Content folder.</span></span>

<span data-ttu-id="f3196-192">새 디자인에서는 대화 상대 관리자에 대 한 이미지 편집 하 고 연락처를 삭제 하는 중에 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-192">Notice that the new design for the Contact Manager includes images for editing and deleting contacts.</span></span> <span data-ttu-id="f3196-193">연락처의 HTML 테이블에 있는 각 연락처 옆에 있는 편집 및 삭제 이미지로가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-193">An Edit and Delete image appear next to each contact in the HTML table of contacts.</span></span>

<span data-ttu-id="f3196-194">HTML을 사용 하 여 렌더링 된 다음 링크를 원래 합니다. 이와 같은 ActionLink() 도우미:</span><span class="sxs-lookup"><span data-stu-id="f3196-194">Originally, these links that were rendered with the HTML.ActionLink() helper like this:</span></span>

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

<span data-ttu-id="f3196-195">Html.ActionLink() 메서드 (HTML 메서드는 보안상의 이유로 링크 텍스트를 인코드) 이미지를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-195">The Html.ActionLink() method does not support images (the method HTML encodes the link text for security reasons).</span></span> <span data-ttu-id="f3196-196">따라서 같이 Url.Action() 호출 하 여 Html.ActionLink()에 대 한 호출을 대체 하나요:</span><span class="sxs-lookup"><span data-stu-id="f3196-196">Therefore, I replaced the calls to Html.ActionLink() with calls to Url.Action() like this:</span></span>

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

<span data-ttu-id="f3196-197">Html.ActionLink() 메서드는 전체 HTML 하이퍼링크를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-197">The Html.ActionLink() method renders an entire HTML hyperlink.</span></span> <span data-ttu-id="f3196-198">Url.Action() 메서드 없이 URL만을 다른 한편으로 렌더링 합니다 &lt;는&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-198">The Url.Action() method, on the other hand, renders just the URL without the &lt;a&gt; tag.</span></span>

<span data-ttu-id="f3196-199">표시, 또한 새 디자인 탭을 선택 또는 선택 하지 않은 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-199">Notice, furthermore, that the new design includes both selected and unselected tabs.</span></span> <span data-ttu-id="f3196-200">예를 들어, 그림 8에에서는 **새 연락처 만들기** 탭을 선택 하며 **내 연락처** 탭을 선택 하지 않으면.</span><span class="sxs-lookup"><span data-stu-id="f3196-200">For example, in Figure 8, the **Create New Contact** tab is selected and the **My Contacts** tab is not selected.</span></span>


<span data-ttu-id="f3196-201">[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="f3196-201">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)</span></span>

<span data-ttu-id="f3196-202">**그림 08**: 선택한 탭을 선택 취소 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="f3196-202">**Figure 08**: Selected and unselected tabs([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image16.png))</span></span>


<span data-ttu-id="f3196-203">탭을 선택 또는 선택 하지 않은 렌더링을 지원 하려면 사용자 지정 HTML 도우미는 MenuItemHelper 라는 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-203">To support rendering both selected and unselected tabs, I created a custom HTML helper named the MenuItemHelper.</span></span> <span data-ttu-id="f3196-204">이 도우미 메서드를 렌더링 중 하나를 &lt;li&gt; 태그 또는 &lt;li 클래스 "선택" =&gt; 현재 컨트롤러 및 작업 도우미에 전달 된 컨트롤러 및 작업 이름에 해당 하는 여부에 따라 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-204">This helper method renders either a &lt;li&gt; tag or a &lt;li class="selected"&gt; tag depending on whether the current controller and action corresponds to the controller and action name passed to the helper.</span></span> <span data-ttu-id="f3196-205">MenuItemHelper에 대 한 코드는 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-205">The code for the MenuItemHelper is contained in Listing 1.</span></span>

<span data-ttu-id="f3196-206">**1-Helpers\MenuItemHelper.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="f3196-206">**Listing 1 - Helpers\MenuItemHelper.cs**</span></span>

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

<span data-ttu-id="f3196-207">MenuItemHelper 클래스를 사용 하는 TagBuilder 내부적으로 작성 하는 &lt;li&gt; HTML 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-207">The MenuItemHelper uses the TagBuilder class internally to build the &lt;li&gt; HTML tag.</span></span> <span data-ttu-id="f3196-208">TagBuilder 클래스는 새 HTML 태그를 작성 해야 할 경우 사용할 수 있는 매우 유용한 유틸리티 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-208">The TagBuilder class is a very useful utility class that you can use whenever you need to build up a new HTML tag.</span></span> <span data-ttu-id="f3196-209">여기에 특성 추가, CSS 클래스를 추가, Id, 생성 및 s 태그를 수정 하기 위한 메서드 내부 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-209">It includes methods for adding attributes, adding CSS classes, generating Ids, and modifying the tag s inner HTML.</span></span>

## <a name="summary"></a><span data-ttu-id="f3196-210">요약</span><span class="sxs-lookup"><span data-stu-id="f3196-210">Summary</span></span>

<span data-ttu-id="f3196-211">이 반복에서 ASP.NET MVC 응용 프로그램의 시각적 디자인을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-211">In this iteration, we improved the visual design of our ASP.NET MVC application.</span></span> <span data-ttu-id="f3196-212">먼저, ASP.NET MVC 디자인 갤러리를 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-212">First, you were introduced to the ASP.NET MVC Design Gallery.</span></span> <span data-ttu-id="f3196-213">ASP.NET MVC 응용 프로그램에서 사용할 수 있는 ASP.NET MVC 디자인 갤러리에서 무료 디자인 템플릿을 다운로드 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-213">You learned how to download free design templates from the ASP.NET MVC Design Gallery that you can use in your ASP.NET MVC applications.</span></span>

<span data-ttu-id="f3196-214">다음으로, 기본 연계 스타일 시트 파일 및 마스터 뷰 페이지 파일을 수정 하 여 사용자 지정 디자인을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-214">Next, we discussed how you can create a custom design by modifying the default cascading style sheet file and master view page file.</span></span> <span data-ttu-id="f3196-215">새 디자인을 지원 하기 위해 연락처 관리자 응용 프로그램에 일부 사소한 변경을 수행 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-215">In order to support the new design, we had to make some minor changes to our Contact Manager application.</span></span> <span data-ttu-id="f3196-216">예를 들어 MenuItemHelper 또는 선택 하지 않은 탭이 표시 되는 명명 된 새 HTML 도우미를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-216">For example, we added a new HTML helper named the MenuItemHelper that displays selected and unselected tabs.</span></span>

<span data-ttu-id="f3196-217">다음 반복에서는 유효성 검사의 매우 중요 한 주제를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-217">In the next iteration, we tackle the very important subject of validation.</span></span> <span data-ttu-id="f3196-218">사용자 수 없습니다. 새 연락처를 먼저 사용자가 등 필요한 값을 제공 하지 않고 만들고 있는 성 응용 프로그램 유효성 검사 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3196-218">We add validation code to our application so that a user cannot create a new contact without supplying required values such as a person s first and last name.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f3196-219">[이전](iteration-1-create-the-application-cs.md)
> [다음](iteration-3-add-form-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f3196-219">[Previous](iteration-1-create-the-application-cs.md)
[Next](iteration-3-add-form-validation-cs.md)</span></span>
