---
uid: web-pages/overview/data/working-with-files
title: ASP.NET 웹 페이지 (Razor) 사이트에 대 한 파일 작업 | Microsoft Docs
author: tfitzmac
description: 이 읽기, 쓰기, 추가, 삭제 및 파일을 업로드 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 0f119f8fb4873e55292203f21a2efd8f26793ae4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "28040225"
---
<a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="b70e2-103">ASP.NET 웹 페이지 (Razor) 사이트에 대 한 파일 작업</span><span class="sxs-lookup"><span data-stu-id="b70e2-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="b70e2-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b70e2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b70e2-105">이 문서에서는 읽기, 쓰기, 추가, 삭제 및 ASP.NET 웹 페이지 (Razor) 사이트의 파일을 업로드 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="b70e2-106">이미지를 업로드 하 고 조작 하려는 경우 (예를 들어 대칭 이동 또는 크기를 조정) 참조 [ASP.NET 웹 페이지 사이트에 이미지 작업](https://go.microsoft.com/fwlink/?LinkId=202897)합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).</span></span>
> 
> 
> <span data-ttu-id="b70e2-107">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="b70e2-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="b70e2-108">텍스트 파일을 만들고 데이터를 쓰려고 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="b70e2-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="b70e2-109">기존 파일에 데이터를 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="b70e2-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="b70e2-110">파일을 읽고 여기에서 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="b70e2-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="b70e2-111">웹 사이트에서 파일을 삭제 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="b70e2-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="b70e2-112">사용자가 파일 하나 또는 여러 파일 업로드 수 있도록 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="b70e2-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="b70e2-113">다음은 문서에 도입 된 기능을 프로그래밍 하는 ASP.NET입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="b70e2-114">`File` 파일을 관리 하는 방법을 제공 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="b70e2-115">`FileUpload` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="b70e2-116">`Path` 경로 파일 이름을 조작할 수 있도록 하는 메서드를 제공 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b70e2-117">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="b70e2-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b70e2-118">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="b70e2-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="b70e2-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="b70e2-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="b70e2-120">이 자습서는 WebMatrix 3 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-120">This tutorial also works with WebMatrix 3.</span></span>


<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="b70e2-121">텍스트 파일을 만들고 데이터를 쓰려면</span><span class="sxs-lookup"><span data-stu-id="b70e2-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="b70e2-122">웹 사이트의 데이터베이스를 사용 하는 것 외에도 파일을 작업할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="b70e2-123">예를 들어 사이트에 대 한 데이터를 저장 하는 간단한 방법으로 텍스트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="b70e2-124">(데이터를 저장 하는 데 사용 되는 텍스트 파일 라고도 *플랫 파일*.) 텍스트 파일 같은 서로 다른 형식으로 이어야 수 *.txt*, *.xml*, 또는 *.csv* (쉼표로 구분 된 값).</span><span class="sxs-lookup"><span data-stu-id="b70e2-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="b70e2-125">텍스트 파일에 데이터를 저장 하려는 경우 사용할 수 있습니다는 `File.WriteAllText` 만들기 위해 파일을 지정 하는 메서드 및 데이터를 쓰려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="b70e2-126">이 절차의 3 개는 단순 폼을 포함 하는 페이지 만듭니다 `input` 요소 (예: 이름, 성, 이름 및 전자 메일 주소) 및 **전송** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="b70e2-127">사용자가 폼을 제출 하는 경우 사용자의 입력 텍스트 파일에 저장할 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="b70e2-128">라는 새 폴더 만들기 *앱\_데이터*이미 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="b70e2-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="b70e2-129">웹 사이트의 루트에 라는 새 파일을 만들어 *UserData.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="b70e2-130">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="b70e2-131">HTML 태그를 세 가지 텍스트 상자는 폼을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="b70e2-132">코드를 사용 하 여는 `IsPost` 처리를 시작 하기 전에 페이지가 제출 되었는지 여부를 결정 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="b70e2-133">첫 번째 작업이 사용자 입력을 가져오고를 변수에 할당 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="b70e2-134">코드는 다음 하나의 쉼표로 구분 된 문자열을 다른 변수에 저장 됩니다에 별도 변수 값을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="b70e2-135">쉼표 구분 기호는 따옴표에 포함 된 문자열 (","), 쉼표 사용자가 만드는 큰 문자열에 문자 그대로 포함 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="b70e2-136">함께 연결 하는 데이터의 끝에 추가 `Environment.NewLine`합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="b70e2-137">이렇게 하면 줄 바꿈 (줄 바꿈 문자)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="b70e2-138">이 모든 연결 맞게 만들려는 다음과 같은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="b70e2-139">(나누기가 있는 보이지 않는 줄 끝에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="b70e2-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="b70e2-140">다음에 변수를 만듭니다 (`dataFile`)의 데이터를 저장할 파일의 이름과 위치를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="b70e2-141">위치를 설정 하려면 몇 가지 특수 한 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="b70e2-142">웹 사이트에서 같은 절대 경로를 코드에서 참조 하는 좋은 방법이 이기 *C:\Folder\File.txt* 웹 서버의 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="b70e2-143">웹 사이트 이동 되는 경우 절대 경로 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="b70e2-144">또한 호스팅된 사이트에 대 한 (는 컴퓨터에 다름) 일반적으로 모르는 올바른 경로 코드를 작성할 때는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="b70e2-145">하지만 경우에 따라 (예: now, 파일을 작성 하기 위한) 전체 경로 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="b70e2-146">솔루션 사용 하는 것은 `MapPath` 의 메서드는 `Server` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="b70e2-147">이 웹 사이트에 전체 경로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-147">This returns the complete path to your website.</span></span> <span data-ttu-id="b70e2-148">웹 사이트 루트, 사용자에 대 한 경로 가져올 수는 `~` 연산자 (represen에 사이트의 가상 루트)를 `MapPath`합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="b70e2-149">(같은, 하위 폴더 이름을 전달할 수도 있습니다 *~/App\_데이터 /*, 해당 하위 폴더에 대 한 경로 가져올 수 있습니다.) 그런 다음 전체 경로 만들기 위해 어떤 메서드가 반환에 대 한 추가 정보를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="b70e2-150">이 예제에서는 파일 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-150">In this example, you add a file name.</span></span> <span data-ttu-id="b70e2-151">(자세한 내용은에서 파일 및 폴더 경로를 사용 하는 방법에 대 한 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span><span class="sxs-lookup"><span data-stu-id="b70e2-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="b70e2-152">파일에 저장 되는 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="b70e2-153">이 폴더는에 설명 된 대로 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더 [ASP.NET 웹 페이지 사이트에서 데이터베이스 작업을 소개](https://go.microsoft.com/fwlink/?LinkId=195209)합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="b70e2-154">`WriteAllText` 의 메서드는 `File` 개체 파일에 데이터를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="b70e2-155">이 메서드는 두 개의 매개 변수: 쓰고, 파일 및 실제 쓸 데이터를의 이름 (경로)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="b70e2-156">첫 번째 매개 변수 이름에 `@` 접두사로 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="b70e2-157">이 asp 축 자 문자열 리터럴을 제공 하 고 있는지와 같은 문자 "/" 특별 한 방식 해석 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="b70e2-158">(자세한 내용은 참조 [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span><span class="sxs-lookup"><span data-stu-id="b70e2-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="b70e2-159">파일을 저장할 코드에 대 한 순서 대로 *앱\_데이터* 폴더, 응용 프로그램이 필요한 읽기 / 쓰기 해당 폴더에 대 한 권한.</span><span class="sxs-lookup"><span data-stu-id="b70e2-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="b70e2-160">개발 컴퓨터에서이 발생 하지 않습니다 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="b70e2-161">그러나 호스팅 공급자의 웹 서버에 사이트를 게시 하는 경우에 해당 권한을 명시적으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="b70e2-162">호스팅 공급자의 서버에서이 코드를 실행 하 고 오류가 발생 하는 경우에 이러한 권한을 설정 하는 방법을 알아보려면 호스팅 공급자와 함께 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="b70e2-163">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="b70e2-164">필드에 값을 입력 한 다음 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="b70e2-165">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-165">Close the browser.</span></span>
- <span data-ttu-id="b70e2-166">프로젝트에 반환 하 고 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="b70e2-167">열기는 *data.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-167">Open the *data.txt* file.</span></span> <span data-ttu-id="b70e2-168">폼에 제출 된 데이터는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-168">The data you submitted in the form is in the file.</span></span> 

    ![[image]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="b70e2-170">닫기는 *data.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="b70e2-171">기존 파일에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="b70e2-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="b70e2-172">이전 예제에서 사용한 `WriteAllText` 데이터의 한 부분에 이었죠 하는 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="b70e2-173">메서드를 다시 호출 하 고 동일한 파일 이름을 전달 하는 경우에 기존 파일을 완전히 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="b70e2-174">그러나 파일을 만든 후 종종 하려는 파일의 끝에 새 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="b70e2-175">사용 하 여 해당 하는 작업을 수행할 수는 `AppendAllText` 의 메서드는 `File` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="b70e2-176">웹 사이트의 사본을 *UserData.cshtml* 파일을 복사 이름을 *UserDataMultiple.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="b70e2-177">여는 앞의 코드 블록을 교체 `<!DOCTYPE html>` 다음 코드 블록으로 태그 지정:</span><span class="sxs-lookup"><span data-stu-id="b70e2-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="b70e2-178">이 코드를 이전 예제에서 하나의 변경을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="b70e2-179">사용 하는 대신 `WriteAllText`를 사용 하 여 `the AppendAllText` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b70e2-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="b70e2-180">메서드는 비슷하지만, 점을 제외 하 고 `AppendAllText` 데이터 파일의 끝에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="b70e2-181">와 마찬가지로 `WriteAllText`, `AppendAllText` 존재 하지 않는 경우 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="b70e2-182">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="b70e2-183">필드에 대 한 값을 입력 한 다음 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="b70e2-184">더 많은 데이터를 추가 하 고 폼을 다시 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="b70e2-185">사진은 자동으로 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="b70e2-186">열기는 *data.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-186">Open the *data.txt* file.</span></span> <span data-ttu-id="b70e2-187">이제 방금 입력 한 새 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-187">It now contains the new data that you just entered.</span></span> 

    ![[image]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="b70e2-189">읽고 파일에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="b70e2-190">텍스트 파일에 데이터를 쓸 필요가 없습니다 하는 경우에 있을 경우에 따라 하나에서 데이터를 읽이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="b70e2-191">이 위해 다시 사용할 수 있습니다는 `File` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="b70e2-192">사용할 수는 `File` 개별적으로 각 줄을 읽을 개체 (줄 바꿈으로 구분 됨) 또는 구분 하는 방법에 관계 없이 개별 항목을 읽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="b70e2-193">이 절차를 읽고 앞의 예제에서 만든 데이터를 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="b70e2-194">웹 사이트의 루트에 라는 새 파일을 만들어 *DisplayData.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="b70e2-195">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="b70e2-196">명명 된 변수에 앞의 예에서 만든 파일을 참조 하 여 시작 하는 코드 `userData`,이 메서드 호출을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b70e2-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="b70e2-197">이 작업을 수행 하는 코드는 내부에 `if` 문.</span><span class="sxs-lookup"><span data-stu-id="b70e2-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="b70e2-198">파일을 읽을 시기는 것이 좋습니다 사용 하는 `File.Exists` 는 파일을 사용할 수 있는지 여부를 먼저 확인 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="b70e2-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="b70e2-199">또한이 코드 파일이 비어 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="b70e2-200">페이지의 본문에는 두 개의 `foreach` 다른 중첩 된 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="b70e2-201">외부 `foreach` 루프 데이터 파일에서 한 번에 한 줄을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="b70e2-202">이 경우 줄은 파일에 줄 바꿈을 정의 &#8212; 즉, 각 데이터 항목은 별도 줄.</span><span class="sxs-lookup"><span data-stu-id="b70e2-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="b70e2-203">외부 루프는 새 항목을 만듭니다 (`<li>` 요소) 안에 정렬 된 목록 (`<ol>` 요소).</span><span class="sxs-lookup"><span data-stu-id="b70e2-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="b70e2-204">내부 반복 구분 기호로 쉼표를 사용 하는 항목 (필드)를 각 데이터 행을 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="b70e2-205">(이전 예제에 따라, 즉, 각 줄에 세 개의 필드가 포함 되어 있음을 &#8212; 이름, 성, 이름 및 전자 메일 주소를 각각 쉼표로 구분 하 여.) 내부 루프도 만듭니다.는 `<ul>` 데이터 줄의 각 필드에 대 한 항목 목록 및 한 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="b70e2-206">코드에는 두 개의 데이터 형식, 배열을 사용 하는 방법을 보여 줍니다. 및 `char` 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="b70e2-207">배열이 필요 하기 때문에 `File.ReadAllLines` 메서드는 배열로 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="b70e2-208">`char` 데이터 형식이 필요 하기 때문에 `Split` 메서드가 반환 되는 `array` 각 요소는 형식에서 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="b70e2-209">(배열에 대 한 정보를 참조 하십시오. [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span><span class="sxs-lookup"><span data-stu-id="b70e2-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="b70e2-210">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-210">Run the page in a browser.</span></span> <span data-ttu-id="b70e2-211">이전 예제에 대 한 입력 한 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[image]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="b70e2-213">**Microsoft Excel 쉼표로 구분 된 파일에서 데이터를 표시합니다.**</span><span class="sxs-lookup"><span data-stu-id="b70e2-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="b70e2-214">Microsoft Excel을 사용 하 여 쉼표로 구분 된 파일로 스프레드시트에 포함 된 데이터를 저장할 수 있습니다 (*.csv* 파일).</span><span class="sxs-lookup"><span data-stu-id="b70e2-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="b70e2-215">이렇게 하면 파일이 Excel 형식에 없는 일반 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="b70e2-216">스프레드시트에서 각 행의 텍스트 파일에 줄 바꿈을 구분 된 및 각 데이터 항목은 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="b70e2-217">파일을 읽을 Excel 쉼표로 구분 된 코드에서 데이터 파일의 이름을 변경 하면 이전 예제에 표시 된 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>


<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="b70e2-218">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="b70e2-218">Deleting Files</span></span>

<span data-ttu-id="b70e2-219">웹 사이트에서 파일을 삭제 하려면 사용할 수 있습니다는 `File.Delete` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b70e2-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="b70e2-220">이 절차에서는 사용자가 이미지를 삭제할 수 있도록 하는 방법을 보여 줍니다 (*.jpg* 파일)에서 프로그램 *이미지* 폴더 파일의 이름을 알고 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="b70e2-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b70e2-221">**중요 한** 프로덕션 웹 사이트의 하면 일반적으로 제한할 수 있는 사용자는 데이터를 변경 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="b70e2-222">멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자를 인증 하는 방법에 대 한 정보를 참조 하십시오. [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="b70e2-223">웹 사이트에서 라는 하위 폴더를 만듭니다 *이미지*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="b70e2-224">하나 이상의 복사 *.jpg* 로 파일은 *이미지* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="b70e2-225">웹 사이트의 루트에서 라는 새 파일을 만듭니다 *FileDelete.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="b70e2-226">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="b70e2-227">이 페이지는 사용자가 이미지 파일의 이름을 입력할 수 있는 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="b70e2-228">입력 하지는 *.jpg* 파일 이름 확장명; 파일 이름을 다음과 같이 제한 하 여 도움말 있습니다 하면 사용자가 사이트의 임의 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="b70e2-229">코드에는 사용자가 입력 하 고 전체 경로 생성 한 다음 파일 이름을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="b70e2-230">경로 만들려면 코드 사용 하 여 현재 웹 사이트 경로 (에서 반환 되는 `Server.MapPath` 메서드), *이미지* 폴더 이름, 사용자가 제공한 이름 및 리터럴 문자열로: ".jpg"입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="b70e2-231">코드를 호출 하 여 파일을 삭제 하는 `File.Delete` 메서드를 바로 전에 구성한 전체 경로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="b70e2-232">끝 태그에 코드 파일이 삭제 된 확인 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="b70e2-233">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-233">Run the page in a browser.</span></span> 

    ![[image]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="b70e2-235">마우스 클릭 한 다음 파일의 이름을 입력 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="b70e2-236">파일, 삭제 된 경우 파일의 이름이 페이지 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="b70e2-237">가 사용자가 업로드 파일</span><span class="sxs-lookup"><span data-stu-id="b70e2-237">Letting Users Upload a File</span></span>

<span data-ttu-id="b70e2-238">`FileUpload` 도우미 웹 사이트에 파일을 업로드 하는 사용자가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="b70e2-239">다음 절차 사용자가 단일 파일 업로드 수 있도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="b70e2-240">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)이전에 추가 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="b70e2-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="b70e2-241">에 *앱\_데이터* 폴더를 새 폴더를 만들고 이름을 *UploadedFiles*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="b70e2-242">만들 라는 새 파일의 루트를 *FileUpload.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="b70e2-243">다음 페이지에서 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="b70e2-244">페이지의 본문 부분은 사용 하 여는 `FileUpload` 도우미 업로드 상자와 사용자가 문제에 대해 있는 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[image]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="b70e2-246">에 대해 설정한 속성은 `FileUpload` 도우미 지정 업로드할 파일에 대 한 단일 박스 원하고 제출 단추 읽기를 원하는 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="b70e2-247">(문서의 뒷부분에서 상자를 더 추가 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b70e2-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="b70e2-248">사용자가 클릭할 때 **업로드**, 페이지 맨 위에 있는 코드 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="b70e2-249">`Request` 양식 필드의 값을 가져오는 일반적으로 사용 하는 개체에는 `Files` 파일 (또는 파일)를 포함 하는 배열 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="b70e2-250">배열의 특정 위치에서 개별 파일을 가져올 수 있습니다 &#8212; 예를 들어 첫 번째 업로드 된 파일을 가져오려면 얻게 `Request.Files[0]`을 두 번째 파일을 가져오는 얻게 `Request.Files[1]`등입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="b70e2-251">(프로그래밍에서는 계산을 일반적으로 0에서 시작 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b70e2-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="b70e2-252">변수에 배치 업로드 된 파일을 인출 하는 경우 (여기서 `uploadedFile`) 조작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="b70e2-253">업로드 된 파일의 이름을 확인 하려면 거 해당 `FileName` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="b70e2-254">그러나 사용자는 파일 업로드 `FileName` 전체 경로가 포함 된 사용자의 원래 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="b70e2-255">그는 다음과 같이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-255">It might look like this:</span></span>

    <span data-ttu-id="b70e2-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="b70e2-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="b70e2-257">그러나 하지 서버에 대 한 사용자의 컴퓨터에 대 한 경로 이기 때문에 모든 경로 정보를 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="b70e2-258">려는 실제 파일 이름 (*Sample.txt*).</span><span class="sxs-lookup"><span data-stu-id="b70e2-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="b70e2-259">사용 하 여 경로에서 파일만 제거할 수 있습니다는 `Path.GetFileName` 다음과 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="b70e2-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="b70e2-260">`Path` 개체는 경로 제거, 패스를 결합 하 고 등 하는 데 사용할 수 있는 다음과 같은 메서드의 수 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="b70e2-261">업로드 된 파일의 이름, 참조 되 면 웹 사이트에 업로드 된 파일을 저장 하려는 위치에 대 한 새 경로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="b70e2-262">결합 하는 경우에 `Server.MapPath`, 폴더 이름 (*앱\_데이터/UploadedFiles*), 및 새로 훼손된 파일 이름을 한 새 경로를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="b70e2-263">업로드 된 파일을 호출할 수 있습니다 `SaveAs` 메서드를 실제로 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="b70e2-264">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-264">Run the page in a browser.</span></span> 

    ![[image]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="b70e2-266">클릭 **찾아보기** 업로드할 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[image]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="b70e2-268">옆에 있는 텍스트 상자는 **찾아보기** 단추 경로 및 파일 위치를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[image]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="b70e2-270">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-270">Click **Upload**.</span></span>
8. <span data-ttu-id="b70e2-271">웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="b70e2-272">열기는 *UploadedFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="b70e2-273">업로드 한 파일은 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-273">The file that you uploaded is in the folder.</span></span> 

    ![[image]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="b70e2-275">수 있도록 사용자가 여러 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="b70e2-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="b70e2-276">이전 예에서 파일 하나만 업로드 하는 사용자가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="b70e2-277">하지만 사용할 수는 `FileUpload` 한 번에 둘 이상의 파일을 업로드 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="b70e2-278">한 번에 하나의 파일을 업로드 하는 중입니다.은 지루한 사진 업로드 같은 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="b70e2-279">(사진에 업로드 하는 방법에 대 한 읽을 수 [ASP.NET 웹 페이지 사이트에 이미지 작업](https://go.microsoft.com/fwlink/?LinkId=202897).) 이 예제에는 그 이상의 업로드에 동일한 기법을 사용할 수 있지만 사용자가 한 번에 두 개를 업로드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="b70e2-280">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)아직 없는 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="b70e2-281">명명 된 새 페이지를 만들고 *FileUploadMultiple.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="b70e2-282">다음 페이지에서 기존 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="b70e2-283">이 예제는 `FileUpload` 도우미 페이지의 본문에는 기본적으로 사용자가 두 파일을 업로드할 수 있도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="b70e2-284">때문에 `allowMoreFilesToBeAdded` 로 설정 된 `true`, 도우미 사용자가 업로드 상자를 더 추가할 수 있는 링크를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[image]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="b70e2-286">사용자 업로드 하는 파일을 처리 하려면 코드에서는 앞의 예제에서 사용한 동일한 기본 기술을 사용 &#8212; 에서 파일을 가져옵니다. `Request.Files` 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="b70e2-287">(다양 한 항목을 포함 하 여 수행 해야 올바른 파일 이름 및 경로 가져올 수 있습니다.) 이 이번 혁신은 사용자에 여러 파일 업로드 수를 알 수 없는 많은입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="b70e2-288">가져올 수를 확인 하려면 `Request.Files.Count`합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="b70e2-289">반복 하면 손 모양 아이콘이이 번호로 `Request.Files`차례로 각 파일을 인출 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="b70e2-290">컬렉션 전체 알려진된 횟수를 반복 하려는 경우 사용할 수 있습니다는 `for` 다음과 같은 루프:</span><span class="sxs-lookup"><span data-stu-id="b70e2-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="b70e2-291">변수 `i` 설정한 어떤 상한에는 0에서 전송 되는 임시 카운터 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="b70e2-292">이 경우 최대 파일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="b70e2-293">있지만 시나리오 ASP.NET에서 수 계산을 위한 일반적인 경우 처럼 0에서 시작 하는 카운터, 상한값은 실제로 하나 보다 작은 파일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="b70e2-294">(3 개의 파일을 업로드 하는 경우 개수는 0 ~ 2.)</span><span class="sxs-lookup"><span data-stu-id="b70e2-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="b70e2-295">`uploadedCount` 변수 합계를 모든 파일을 성공적으로 업로드 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="b70e2-296">이 코드는 예상 되는 파일을 업로드할 수 있는 가능성을 차지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="b70e2-297">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-297">Run the page in a browser.</span></span> <span data-ttu-id="b70e2-298">브라우저는 페이지 및 두 개의 업로드 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="b70e2-299">두 개의 파일을 업로드 하려면 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-299">Select two files to upload.</span></span>
6. <span data-ttu-id="b70e2-300">클릭 **다른 파일을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-300">Click **Add another file**.</span></span> <span data-ttu-id="b70e2-301">페이지는 새 업로드 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-301">The page displays a new upload box.</span></span> 

    ![[image]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="b70e2-303">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-303">Click **Upload**.</span></span>
8. <span data-ttu-id="b70e2-304">웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="b70e2-305">열기는 *UploadedFiles* 폴더 성공적으로 업로드 된 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b70e2-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="b70e2-306">추가 자료</span><span class="sxs-lookup"><span data-stu-id="b70e2-306">Additional Resources</span></span>


[<span data-ttu-id="b70e2-307">ASP.NET 웹 페이지 사이트에 이미지 작업</span><span class="sxs-lookup"><span data-stu-id="b70e2-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="b70e2-308">CSV 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="b70e2-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
