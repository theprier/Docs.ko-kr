---
uid: web-pages/overview/data/working-with-files
title: ASP.NET 웹 페이지 (Razor) 사이트에서 파일 작업 | Microsoft Docs
author: tfitzmac
description: 이 읽기, 쓰기, 추가, 삭제 및 파일을 업로드 하는 방법을 설명 합니다.
ms.author: aspnetcontent
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 3778bc0041c56fe7164265fe565996aea5564bdf
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841606"
---
<a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="4bcc4-103">ASP.NET 웹 페이지 (Razor) 사이트에서 파일 사용</span><span class="sxs-lookup"><span data-stu-id="4bcc4-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="4bcc4-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4bcc4-105">이 문서는 읽기, 쓰기, 추가, 삭제 및 ASP.NET Web Pages (Razor) 사이트에서 파일을 업로드 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="4bcc4-106">이미지를 업로드 하 고 조작 하는 경우 (예를 들어, 대칭 이동 하거나 크기를 조정할)를 참조 하세요 [ASP.NET 웹 페이지 사이트에서 이미지를 사용 하 여 작업](https://go.microsoft.com/fwlink/?LinkId=202897)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).</span></span>
> 
> 
> <span data-ttu-id="4bcc4-107">**학습할 내용:**</span><span class="sxs-lookup"><span data-stu-id="4bcc4-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="4bcc4-108">텍스트 파일을 만들고 데이터를 작성 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="4bcc4-109">기존 파일에 데이터를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="4bcc4-110">파일 읽기를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="4bcc4-111">웹 사이트에서 파일을 삭제 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="4bcc4-112">사용자가 파일 하나 또는 여러 파일을 업로드 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="4bcc4-113">ASP.NET 문서에 도입 된 기능을 프로그래밍은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="4bcc4-114">`File` 개체 파일을 관리 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="4bcc4-115">`FileUpload` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="4bcc4-116">`Path` 경로 파일 이름을 조작할 수 있는 메서드를 제공 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4bcc4-117">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="4bcc4-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4bcc4-118">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="4bcc4-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="4bcc4-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="4bcc4-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="4bcc4-120">이 자습서 에서도 WebMatrix 3를 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-120">This tutorial also works with WebMatrix 3.</span></span>


<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="4bcc4-121">텍스트 파일을 만들고 데이터를 쓰려면</span><span class="sxs-lookup"><span data-stu-id="4bcc4-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="4bcc4-122">웹 사이트의 데이터베이스를 사용 하는 것 외에도 파일을 사용 하 여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="4bcc4-123">예를 들어 사이트에 대 한 데이터를 저장 하는 간단한 방법으로 텍스트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="4bcc4-124">(라고도 데이터 저장에 사용 되는 텍스트 파일을 *플랫 파일*.) 텍스트 파일 같은 다양 한 형식에 있을 수 있습니다 *.txt*하십시오 *.xml*, 또는 *.csv* (쉼표로 구분 된 값).</span><span class="sxs-lookup"><span data-stu-id="4bcc4-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="4bcc4-125">텍스트 파일에 데이터를 저장 하려는 경우 사용할 수 있습니다는 `File.WriteAllText` 만들 파일을 지정 하는 방법 및 데이터를 쓸입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="4bcc4-126">이 절차에서는 3 개를 사용 하 여 간단한 양식을 포함 하는 페이지를 만듭니다 `input` 요소 (이름, 성 및 전자 메일 주소) 및 **제출** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="4bcc4-127">사용자가 폼을 제출 하면 텍스트 파일에 사용자의 입력을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="4bcc4-128">라는 새 폴더를 만듭니다 *앱\_데이터*이미 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="4bcc4-129">웹 사이트의 루트에서 이라는 새 파일을 만듭니다 *UserData.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="4bcc4-130">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="4bcc4-131">HTML 태그는 세 개의 텍스트 상자를 사용 하 여 폼을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="4bcc4-132">코드를 사용 하 여는 `IsPost` 처리를 시작 하기 전에 페이지가 제출 되었는지 여부를 결정 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="4bcc4-133">첫 번째 작업은 사용자 입력을 가져와 변수에 할당 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="4bcc4-134">다음 코드를 다른 변수에 저장 되는 하나의 쉼표로 구분 된 문자열을 별도 변수 값을 연결 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="4bcc4-135">쉼표 구분 기호는 따옴표에 포함 된 문자열 (","), 사용자가 만드는 큰 문자열에 쉼표를 문자 그대로 포함 하는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="4bcc4-136">추가 데이터를 함께 연결의 끝 `Environment.NewLine`합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="4bcc4-137">이 줄 바꿈 (줄 바꿈 문자)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="4bcc4-138">이 모든 연결을 사용 하 여 만드는 항목은 다음과 같은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="4bcc4-139">(구분선을 포함 하는 보이지 않는 줄 끝입니다.)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="4bcc4-140">그런 다음 변수를 만듭니다 (`dataFile`) 데이터를 저장할 파일의 이름과 위치를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="4bcc4-141">몇 가지 특별 한 처리가 필요 위치를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="4bcc4-142">웹 사이트에서는 코드와 같은 절대 경로 참조 바람직하지 *C:\Folder\File.txt* 웹 서버의 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="4bcc4-143">웹 사이트를 이동 하는 경우에 절대 경로 잘못 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="4bcc4-144">또한 호스팅된 사이트 (아니라 사용자 고유의 컴퓨터) 일반적으로 모르는 올바른 경로 이란 코드를 작성할 때.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="4bcc4-145">하지만 경우에 따라 (예: 이제 파일을 작성 하는 것에 대 한) 전체 경로 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="4bcc4-146">솔루션을 사용 하는 것을 `MapPath` 메서드는 `Server` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="4bcc4-147">이 웹 사이트에 전체 경로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-147">This returns the complete path to your website.</span></span> <span data-ttu-id="4bcc4-148">사용자는 웹 사이트 루트에 대 한 경로 가져오려고 합니다 `~` 연산자 (represen 사이트의 가상 루트)를 `MapPath`입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="4bcc4-149">(같은, 하위 폴더 이름을 전달할 수도 있습니다 *~/App\_데이터 /*, 해당 하위 폴더에 대 한 경로 가져오려고 합니다.) 그런 다음 전체 경로 만들기 위해 모든 메서드에서 반환에 대 한 추가 정보를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="4bcc4-150">이 예제에서는 파일 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-150">In this example, you add a file name.</span></span> <span data-ttu-id="4bcc4-151">(자세한에서 파일 및 폴더 경로 사용 하는 방법에 대 한 [ASP.NET 웹 페이지 Razor 구문으로 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="4bcc4-152">파일에 저장 되는 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="4bcc4-153">이 폴더는에 설명 된 대로 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더 [ASP.NET Web Pages 사이트에서 데이터베이스를 사용 하 여 작업 소개](https://go.microsoft.com/fwlink/?LinkId=195209)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="4bcc4-154">합니다 `WriteAllText` 메서드는 `File` 개체 파일에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="4bcc4-155">이 메서드는 두 매개 변수: 쓸 실제 데이터를 쓸 파일의 이름 (경로)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="4bcc4-156">첫 번째 매개 변수 이름에는 `@` 접두사로 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="4bcc4-157">이 축 자 문자열 리터럴을 제공 하 고 문자를 ASP.NET에 지시 "/" 특별 한 방식으로 해석 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="4bcc4-158">(자세한 내용은 [로 ASP.NET 웹 프로그래밍 Razor 구문 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="4bcc4-159">파일을 저장 하도록 코드를 *앱\_데이터* 폴더, 응용 프로그램 해야 읽기 / 쓰기 권한 해당 폴더에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="4bcc4-160">개발 컴퓨터에서이 아닌 경우 일반적으로 문제</span><span class="sxs-lookup"><span data-stu-id="4bcc4-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="4bcc4-161">그러나 호스팅 공급자의 웹 서버에 사이트를 게시할 때에 해당 권한을 명시적으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="4bcc4-162">호스팅 공급자의 서버에서이 코드를 실행 하 고 오류가 발생 하는 경우 이러한 권한을 설정 하는 방법을 알아보려면 호스팅 공급자를 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="4bcc4-163">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="4bcc4-164">필드에 값을 입력 한 다음 클릭 **제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="4bcc4-165">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-165">Close the browser.</span></span>
- <span data-ttu-id="4bcc4-166">프로젝트에 돌아가서 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="4bcc4-167">엽니다는 *data.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-167">Open the *data.txt* file.</span></span> <span data-ttu-id="4bcc4-168">폼의 제출 된 데이터는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-168">The data you submitted in the form is in the file.</span></span> 

    ![[이미지]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="4bcc4-170">닫기 합니다 *data.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="4bcc4-171">기존 파일에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="4bcc4-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="4bcc4-172">이전 예제에서 사용한 `WriteAllText` 에 하나의 데이터 부분을 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="4bcc4-173">메서드를 다시 호출 하 고 동일한 파일 이름을 전달 하는 경우 기존 파일을 완전히 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="4bcc4-174">그러나 파일을 만든 후 종종 하려는 파일의 끝에 새 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="4bcc4-175">사용 하 여 수행할 수 있습니다 합니다 `AppendAllText` 메서드는 `File` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="4bcc4-176">웹 사이트에서의 복사본을 만듭니다는 *UserData.cshtml* 파일을 복사본의 이름을 *UserDataMultiple.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="4bcc4-177">코드 블록을 열기 전에 교체 `<!DOCTYPE html>` 다음 코드 블록을 사용 하 여 태그:</span><span class="sxs-lookup"><span data-stu-id="4bcc4-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="4bcc4-178">이 코드를 이전 예제에서 하나의 변경을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="4bcc4-179">사용 하는 대신 `WriteAllText`를 사용 하 여 `the AppendAllText` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="4bcc4-180">메서드는 마찬가지로 점을 제외 하 고 `AppendAllText` 데이터 파일의 끝에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="4bcc4-181">와 마찬가지로 `WriteAllText`, `AppendAllText` 존재 하지 않는 경우 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="4bcc4-182">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="4bcc4-183">필드에 대 한 값을 입력 한 다음 클릭 **제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="4bcc4-184">더 많은 데이터를 추가 하 고 양식을 다시 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="4bcc4-185">프로젝트에 반환, 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="4bcc4-186">엽니다는 *data.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-186">Open the *data.txt* file.</span></span> <span data-ttu-id="4bcc4-187">이제 방금 입력 한 새 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-187">It now contains the new data that you just entered.</span></span> 

    ![[이미지]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="4bcc4-189">읽고 파일에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="4bcc4-190">텍스트 파일에 데이터를 쓸 필요가 없는, 하는 경우에 하나에서 데이터를 읽는 해야 아마도 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="4bcc4-191">이 위해 다시 사용할 수는 `File` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="4bcc4-192">사용할 수 있습니다는 `File` 개별적으로 각 줄을 읽을 개체입니다 (줄 바꿈으로 구분 됨) 또는 분리 하는 방법에 관계 없이 개별 항목을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="4bcc4-193">이 절차를 읽고 앞의 예제에서 만든 데이터를 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="4bcc4-194">웹 사이트의 루트에서 이라는 새 파일을 만듭니다 *DisplayData.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="4bcc4-195">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="4bcc4-196">라는 변수를 앞의 예제에서 만든 파일을 참조 하 여 시작 하는 코드 `userData`,이 메서드 호출을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4bcc4-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="4bcc4-197">이 작업을 수행 하는 코드 내에 `if` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="4bcc4-198">파일을 읽는 경우 것이 좋습니다를 사용 하는 `File.Exists` 파일을 사용할 수 있는지 먼저 확인 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="4bcc4-199">또한 코드는 해당 파일이 비어 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="4bcc4-200">페이지의 본문에는 두 개의 `foreach` 하나는 서로 중첩 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="4bcc4-201">외부 `foreach` 루프 데이터 파일에서 한 번에 한 줄을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="4bcc4-202">파일의 줄 바꿈으로 줄은 정의 하는 예제의 경우 &#8212; 는 각 데이터 항목은 자체 줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="4bcc4-203">외부 루프는 새 항목을 만듭니다 (`<li>` 요소) 정렬 된 목록 내에서 (`<ol>` 요소).</span><span class="sxs-lookup"><span data-stu-id="4bcc4-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="4bcc4-204">내부 반복 항목 (필드)를 구분 기호로 쉼표를 사용 하 여 각 데이터 행을 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="4bcc4-205">(이전 예제에 따라, 즉, 각 줄에 세 개의 필드가 포함 되어 있는지 &#8212; 첫 번째 이름, 성 및 전자 메일 주소를 쉼표로 구분 합니다.) 내부 루프도 만듭니다.는 `<ul>` 데이터 줄에 각 필드에 대 한 항목 목록과 하나 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="4bcc4-206">코드는 배열을 두 데이터 형식을 사용 하는 방법을 보여 줍니다 및 `char` 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="4bcc4-207">배열 이므로 필요한를 `File.ReadAllLines` 메서드는 배열로 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="4bcc4-208">`char` 데이터 형식이 필요 하기 때문에 `Split` 메서드가 반환 되는 `array` 형식의 각 요소가 된 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="4bcc4-209">(배열에 대 한 자세한 내용은 [로 ASP.NET 웹 프로그래밍 Razor 구문 소개](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="4bcc4-210">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-210">Run the page in a browser.</span></span> <span data-ttu-id="4bcc4-211">위의 예제에서는 입력 한 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[이미지]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="4bcc4-213">**Microsoft Excel 쉼표로 구분 된 파일에서 데이터를 표시합니다.**</span><span class="sxs-lookup"><span data-stu-id="4bcc4-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="4bcc4-214">Microsoft Excel을 사용 하 여 쉼표로 구분 된 파일로 스프레드시트에 포함 된 데이터를 저장할 수 있습니다 (*.csv* 파일).</span><span class="sxs-lookup"><span data-stu-id="4bcc4-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="4bcc4-215">작업을 수행 하면 파일은 Excel 형식이 일반 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="4bcc4-216">스프레드시트의 각 행은 텍스트 파일의 줄 바꿈으로 구분 됩니다 하 고 각 데이터 항목을 쉼표로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="4bcc4-217">파일을 읽을 Excel 쉼표로 구분 된 코드에서 데이터 파일의 이름을 변경 하 여 이전 예제에 나와 있는 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>


<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="4bcc4-218">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="4bcc4-218">Deleting Files</span></span>

<span data-ttu-id="4bcc4-219">웹 사이트에서 파일을 삭제 하려면 사용 된 `File.Delete` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="4bcc4-220">이 절차에서는 사용자가 이미지를 삭제할 수 있도록 하는 방법을 보여 줍니다 (*.jpg* 파일)에서 *이미지* 폴더 파일의 이름을 알고 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4bcc4-221">**중요 한** 프로덕션 웹 사이트에서 일반적으로 제한할 있습니다 데이터를 변경 하려면 허용할 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="4bcc4-222">멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자 권한을 부여 하는 방법에 대 한 정보를 참조 하세요 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="4bcc4-223">웹 사이트를 라는 하위 폴더를 만듭니다 *이미지*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="4bcc4-224">하나 이상의 복사본 *.jpg* 파일에 *이미지* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="4bcc4-225">웹 사이트의 루트에서 이라는 새 파일을 만듭니다 *FileDelete.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="4bcc4-226">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="4bcc4-227">이 페이지는 사용자가 이미지 파일의 이름을 입력할 수 있는 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="4bcc4-228">입력 하지 합니다 *.jpg* 파일 이름 확장명;이 같은 파일 이름, 제한 하 여 도움이 하면 사이트에서 임의 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="4bcc4-229">코드는 사용자가 입력 하 고 전체 경로 생성 한 다음 파일 이름을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="4bcc4-230">코드 경로 만들려면 현재 웹 사이트 경로 사용 (에서 반환 되는 `Server.MapPath` 메서드), *이미지* 폴더 이름, 사용자가 제공한 이름 및 리터럴 문자열 ".jpg"입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="4bcc4-231">코드를 호출 하 여 파일을 삭제 하는 `File.Delete` 메서드를 사용자가 생성 하는 전체 경로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="4bcc4-232">끝 태그에 코드 파일이 삭제 된 확인 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="4bcc4-233">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-233">Run the page in a browser.</span></span> 

    ![[이미지]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="4bcc4-235">삭제 하 고 클릭 한 다음 파일의 이름을 입력 **제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="4bcc4-236">파일은 삭제 된 경우 페이지의 맨 아래에 있는 파일의 이름을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="4bcc4-237">수 있도록 사용자가 파일을 업로드</span><span class="sxs-lookup"><span data-stu-id="4bcc4-237">Letting Users Upload a File</span></span>

<span data-ttu-id="4bcc4-238">`FileUpload` 도우미 웹 사이트에 파일을 업로드 하는 사용자가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="4bcc4-239">아래 절차 사용자가 단일 파일을 업로드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="4bcc4-240">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)이전에 추가 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="4bcc4-241">에 *앱\_데이터* 폴더에 새 폴더를 만들고 이름을 *UploadedFiles*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="4bcc4-242">루트에서 이라는 새 파일을 만듭니다 *FileUpload.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="4bcc4-243">다음 페이지에서 기존 콘텐츠를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="4bcc4-244">페이지의 본문 부분에 사용 된 `FileUpload` 업로드 상자 및 잘 알려진 수 있는 단추를 만드는 도우미:</span><span class="sxs-lookup"><span data-stu-id="4bcc4-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[이미지]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="4bcc4-246">에 대해 설정한 속성을 `FileUpload` 도우미는 업로드할 파일에 대 한 단일 상자 및 지정 읽을 제출 단추를 삽입할 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="4bcc4-247">(문서의 뒷부분에서 상자를 더 추가 합니다.)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="4bcc4-248">클릭할 때 **업로드**, 페이지의 맨 위에 있는 코드 파일을 가져와 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="4bcc4-249">`Request` 양식 필드에서 값을 가져오려면 일반적으로 사용 하는 개체에는 `Files` 파일 (또는 파일)를 포함 하는 배열 업로드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="4bcc4-250">배열의 특정 위치에서 개별 파일을 가져올 수 있습니다 &#8212; 예를 들어, 첫 번째 업로드 된 파일을 가져오려면 얻게 `Request.Files[0]`을 두 번째 파일을 가져올 얻게 `Request.Files[1]`등에입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="4bcc4-251">(프로그래밍에서는 일반적으로 계산 0부터 시작 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="4bcc4-252">변수에 배치를 가져오는 파일을 업로드 하는 경우 (이때 `uploadedFile`) 하 여 조작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="4bcc4-253">업로드 된 파일의 이름을 확인 하려면 거 야 해당 `FileName` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="4bcc4-254">그러나 사용자 파일을 업로드 하는 경우 `FileName` 전체 경로 포함 하는 사용자의 원래 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="4bcc4-255">것 같이 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-255">It might look like this:</span></span>

    <span data-ttu-id="4bcc4-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="4bcc4-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="4bcc4-257">서버에 대 한 하지 사용자의 컴퓨터 경로가 없으므로 하지만 모든 경로 정보, 하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="4bcc4-258">원하는 실제 파일 이름 (*Sample.txt*).</span><span class="sxs-lookup"><span data-stu-id="4bcc4-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="4bcc4-259">사용 하 여 파일 경로에서 제거할 수 있습니다는 `Path.GetFileName` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="4bcc4-260">`Path` 개체는 다양 한 경로 제거 하 고, 경로 결합, 등을 사용할 수 있는 다음과 같은 메서드가 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="4bcc4-261">업로드 된 파일의 이름을, 받은 후에 웹 사이트에 업로드 된 파일을 저장 하려는 위치에 대 한 새 경로 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="4bcc4-262">결합 하는 예제의 경우 `Server.MapPath`, 폴더 이름 (*앱\_데이터/UploadedFiles*), 새로 제거 된 파일 이름과 새 경로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="4bcc4-263">업로드 된 파일을 호출할 수 있습니다 `SaveAs` 실제로 파일을 저장 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="4bcc4-264">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-264">Run the page in a browser.</span></span> 

    ![[이미지]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="4bcc4-266">클릭 **찾아보기** 업로드할 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[이미지]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="4bcc4-268">텍스트 상자 옆에 **찾아보기** 단추 경로 및 파일 위치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[이미지]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="4bcc4-270">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-270">Click **Upload**.</span></span>
8. <span data-ttu-id="4bcc4-271">웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="4bcc4-272">엽니다는 *UploadedFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="4bcc4-273">업로드 한 파일이 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-273">The file that you uploaded is in the folder.</span></span> 

    ![[이미지]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="4bcc4-275">수 있도록 사용자가 여러 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="4bcc4-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="4bcc4-276">이전 예제에서는 하나의 파일을 업로드 하는 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="4bcc4-277">사용할 수 있지만 `FileUpload` 한 번에 둘 이상의 파일을 업로드 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="4bcc4-278">한 번에 하나의 파일을 업로드 하는 지루한 사진 업로드 같은 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="4bcc4-279">(에 사진을 업로드 하는 방법에 대 한 읽을 수 있습니다 [ASP.NET 웹 페이지 사이트에서 이미지를 사용 하 여 작업](https://go.microsoft.com/fwlink/?LinkId=202897).) 이 예제에서는 동일한 기법을 사용 하 여 업로드 된 것 보다 더 있지만 사용자가 한 번에 두 개를 업로드 하도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="4bcc4-280">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="4bcc4-281">라는 새 페이지를 만듭니다 *FileUploadMultiple.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="4bcc4-282">다음 페이지에서 기존 콘텐츠를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="4bcc4-283">이 예제는 `FileUpload` 도우미 페이지의 본문에는 기본적으로 두 개의 파일을 업로드 하는 사용자가 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="4bcc4-284">때문에 `allowMoreFilesToBeAdded` 로 설정 된 `true`, 사용자가 업로드 상자를 더 추가할 수 있는 링크를 렌더링 하는 도우미:</span><span class="sxs-lookup"><span data-stu-id="4bcc4-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[이미지]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="4bcc4-286">사용자 업로드 하는 파일을 처리 하려면 코드를 사용 하 여 이전 예제에서 사용한 동일한 기본 기술을 &#8212; 에서 파일을 가져오는 `Request.Files` 한 후 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="4bcc4-287">(다양 한 작업을 포함 해야 할 파일 이름 및 경로 가져올 수 있습니다.) 이 이번 혁신 사용자 여러 파일을 업로드할 수 있습니다 여러 알 수 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="4bcc4-288">가져올 수를 확인 하려면 `Request.Files.Count`합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="4bcc4-289">반복 하면 직접이 번호로 `Request.Files`, 각 파일을 가져와 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="4bcc4-290">컬렉션을 알려진된 횟수를 반복 하려는 경우 사용할 수 있습니다는 `for` 루프를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="4bcc4-291">변수의 `i` 설정한 모든 상한값으로 0에서 전송 되는 임시 카운터 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="4bcc4-292">이 경우의 상한 값은 파일의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="4bcc4-293">있지만 일반적인 asp.net에서 시나리오 계산에 0에서 시작 하는 카운터를 상한값은 실제로 하나 보다 작은 파일 개수.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="4bcc4-294">(3 개의 파일을 업로드 하는 경우의 카운트가 0 2.)</span><span class="sxs-lookup"><span data-stu-id="4bcc4-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="4bcc4-295">`uploadedCount` 변수 합계를 모든 파일을 성공적으로 업로드 되 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="4bcc4-296">이 코드는 예상 되는 파일 업로드 할 수 있는 가능성을 차지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="4bcc4-297">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-297">Run the page in a browser.</span></span> <span data-ttu-id="4bcc4-298">브라우저는 페이지 및 두 업로드 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="4bcc4-299">두 개의 파일을 업로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-299">Select two files to upload.</span></span>
6. <span data-ttu-id="4bcc4-300">클릭 **다른 파일을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-300">Click **Add another file**.</span></span> <span data-ttu-id="4bcc4-301">페이지에는 새 업로드 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-301">The page displays a new upload box.</span></span> 

    ![[이미지]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="4bcc4-303">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-303">Click **Upload**.</span></span>
8. <span data-ttu-id="4bcc4-304">웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="4bcc4-305">엽니다는 *UploadedFiles* 폴더를 성공적으로 업로드 된 파일을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4bcc4-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="4bcc4-306">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4bcc4-306">Additional Resources</span></span>


[<span data-ttu-id="4bcc4-307">ASP.NET 웹 페이지 사이트에서 이미지 작업</span><span class="sxs-lookup"><span data-stu-id="4bcc4-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="4bcc4-308">CSV 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="4bcc4-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
