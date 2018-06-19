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
<a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 대 한 파일 작업
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 읽기, 쓰기, 추가, 삭제 및 ASP.NET 웹 페이지 (Razor) 사이트의 파일을 업로드 하는 방법에 설명 합니다.
> 
> > [!NOTE]
> > 이미지를 업로드 하 고 조작 하려는 경우 (예를 들어 대칭 이동 또는 크기를 조정) 참조 [ASP.NET 웹 페이지 사이트에 이미지 작업](https://go.microsoft.com/fwlink/?LinkId=202897)합니다.
> 
> 
> **학습 내용:** 
> 
> - 텍스트 파일을 만들고 데이터를 쓰려고 하는 방법.
> - 기존 파일에 데이터를 추가 하는 방법.
> - 파일을 읽고 여기에서 표시 하는 방법.
> - 웹 사이트에서 파일을 삭제 하는 방법.
> - 사용자가 파일 하나 또는 여러 파일 업로드 수 있도록 하는 방법.
> 
> 다음은 문서에 도입 된 기능을 프로그래밍 하는 ASP.NET입니다.
> 
> - `File` 파일을 관리 하는 방법을 제공 하는 개체입니다.
> - `FileUpload` 도우미입니다.
> - `Path` 경로 파일 이름을 조작할 수 있도록 하는 메서드를 제공 하는 개체입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서는 WebMatrix 3 에서도 작동합니다.


<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a>텍스트 파일을 만들고 데이터를 쓰려면

웹 사이트의 데이터베이스를 사용 하는 것 외에도 파일을 작업할 수도 있습니다. 예를 들어 사이트에 대 한 데이터를 저장 하는 간단한 방법으로 텍스트 파일을 사용할 수 있습니다. (데이터를 저장 하는 데 사용 되는 텍스트 파일 라고도 *플랫 파일*.) 텍스트 파일 같은 서로 다른 형식으로 이어야 수 *.txt*, *.xml*, 또는 *.csv* (쉼표로 구분 된 값).

텍스트 파일에 데이터를 저장 하려는 경우 사용할 수 있습니다는 `File.WriteAllText` 만들기 위해 파일을 지정 하는 메서드 및 데이터를 쓰려고 합니다. 이 절차의 3 개는 단순 폼을 포함 하는 페이지 만듭니다 `input` 요소 (예: 이름, 성, 이름 및 전자 메일 주소) 및 **전송** 단추입니다. 사용자가 폼을 제출 하는 경우 사용자의 입력 텍스트 파일에 저장할 합니다.

1. 라는 새 폴더 만들기 *앱\_데이터*이미 존재 하지 않는 경우.
2. 웹 사이트의 루트에 라는 새 파일을 만들어 *UserData.cshtml*합니다.
3. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    HTML 태그를 세 가지 텍스트 상자는 폼을 만듭니다. 코드를 사용 하 여는 `IsPost` 처리를 시작 하기 전에 페이지가 제출 되었는지 여부를 결정 하는 속성입니다.

    첫 번째 작업이 사용자 입력을 가져오고를 변수에 할당 하는 것입니다. 코드는 다음 하나의 쉼표로 구분 된 문자열을 다른 변수에 저장 됩니다에 별도 변수 값을 연결 합니다. 쉼표 구분 기호는 따옴표에 포함 된 문자열 (","), 쉼표 사용자가 만드는 큰 문자열에 문자 그대로 포함 하기 때문에 있습니다. 함께 연결 하는 데이터의 끝에 추가 `Environment.NewLine`합니다. 이렇게 하면 줄 바꿈 (줄 바꿈 문자)를 추가 합니다. 이 모든 연결 맞게 만들려는 다음과 같은 문자열입니다.

    [!code-css[Main](working-with-files/samples/sample2.css)]

    (나누기가 있는 보이지 않는 줄 끝에 있습니다.)

    다음에 변수를 만듭니다 (`dataFile`)의 데이터를 저장할 파일의 이름과 위치를 포함 하 합니다. 위치를 설정 하려면 몇 가지 특수 한 처리 해야 합니다. 웹 사이트에서 같은 절대 경로를 코드에서 참조 하는 좋은 방법이 이기 *C:\Folder\File.txt* 웹 서버의 파일에 대 한 합니다. 웹 사이트 이동 되는 경우 절대 경로 문제가 발생 합니다. 또한 호스팅된 사이트에 대 한 (는 컴퓨터에 다름) 일반적으로 모르는 올바른 경로 코드를 작성할 때는 합니다.

    하지만 경우에 따라 (예: now, 파일을 작성 하기 위한) 전체 경로 필요가 있습니다. 솔루션 사용 하는 것은 `MapPath` 의 메서드는 `Server` 개체입니다. 이 웹 사이트에 전체 경로 반환 합니다. 웹 사이트 루트, 사용자에 대 한 경로 가져올 수는 `~` 연산자 (represen에 사이트의 가상 루트)를 `MapPath`합니다. (같은, 하위 폴더 이름을 전달할 수도 있습니다 *~/App\_데이터 /*, 해당 하위 폴더에 대 한 경로 가져올 수 있습니다.) 그런 다음 전체 경로 만들기 위해 어떤 메서드가 반환에 대 한 추가 정보를 연결할 수 있습니다. 이 예제에서는 파일 이름을 추가 합니다. (자세한 내용은에서 파일 및 폴더 경로를 사용 하는 방법에 대 한 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)

    파일에 저장 되는 *앱\_데이터* 폴더입니다. 이 폴더는에 설명 된 대로 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더 [ASP.NET 웹 페이지 사이트에서 데이터베이스 작업을 소개](https://go.microsoft.com/fwlink/?LinkId=195209)합니다.

    `WriteAllText` 의 메서드는 `File` 개체 파일에 데이터를 기록 합니다. 이 메서드는 두 개의 매개 변수: 쓰고, 파일 및 실제 쓸 데이터를의 이름 (경로)를 사용 합니다. 첫 번째 매개 변수 이름에 `@` 접두사로 문자입니다. 이 asp 축 자 문자열 리터럴을 제공 하 고 있는지와 같은 문자 "/" 특별 한 방식 해석 되지 않아야 합니다. (자세한 내용은 참조 [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)

    > [!NOTE]
    > 파일을 저장할 코드에 대 한 순서 대로 *앱\_데이터* 폴더, 응용 프로그램이 필요한 읽기 / 쓰기 해당 폴더에 대 한 권한. 개발 컴퓨터에서이 발생 하지 않습니다 일반적으로 합니다. 그러나 호스팅 공급자의 웹 서버에 사이트를 게시 하는 경우에 해당 권한을 명시적으로 설정 해야 합니다. 호스팅 공급자의 서버에서이 코드를 실행 하 고 오류가 발생 하는 경우에 이러한 권한을 설정 하는 방법을 알아보려면 호스팅 공급자와 함께 확인 합니다.

- 브라우저에서 페이지를 실행 합니다. 

    ![](working-with-files/_static/image1.jpg)
- 필드에 값을 입력 한 다음 클릭 **전송**합니다.
- 브라우저를 닫습니다.
- 프로젝트에 반환 하 고 보기를 새로 고칩니다.
- 열기는 *data.txt* 파일입니다. 폼에 제출 된 데이터는 파일입니다. 

    ![[image]](working-with-files/_static/image2.jpg)
- 닫기는 *data.txt* 파일입니다.

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a>기존 파일에 데이터 추가

이전 예제에서 사용한 `WriteAllText` 데이터의 한 부분에 이었죠 하는 텍스트 파일을 만듭니다. 메서드를 다시 호출 하 고 동일한 파일 이름을 전달 하는 경우에 기존 파일을 완전히 덮어씁니다. 그러나 파일을 만든 후 종종 하려는 파일의 끝에 새 데이터를 추가 합니다. 사용 하 여 해당 하는 작업을 수행할 수는 `AppendAllText` 의 메서드는 `File` 개체입니다.

1. 웹 사이트의 사본을 *UserData.cshtml* 파일을 복사 이름을 *UserDataMultiple.cshtml*합니다.
2. 여는 앞의 코드 블록을 교체 `<!DOCTYPE html>` 다음 코드 블록으로 태그 지정: 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    이 코드를 이전 예제에서 하나의 변경을 받았습니다. 사용 하는 대신 `WriteAllText`를 사용 하 여 `the AppendAllText` 메서드. 메서드는 비슷하지만, 점을 제외 하 고 `AppendAllText` 데이터 파일의 끝에 추가 합니다. 와 마찬가지로 `WriteAllText`, `AppendAllText` 존재 하지 않는 경우 파일을 만듭니다.
3. 브라우저에서 페이지를 실행 합니다.
4. 필드에 대 한 값을 입력 한 다음 클릭 **전송**합니다.
5. 더 많은 데이터를 추가 하 고 폼을 다시 제출 합니다.
6. 사진은 자동으로 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.
7. 열기는 *data.txt* 파일입니다. 이제 방금 입력 한 새 데이터를 포함 합니다. 

    ![[image]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a>읽고 파일에서 데이터를 표시 합니다.

텍스트 파일에 데이터를 쓸 필요가 없습니다 하는 경우에 있을 경우에 따라 하나에서 데이터를 읽이 필요 합니다. 이 위해 다시 사용할 수 있습니다는 `File` 개체입니다. 사용할 수는 `File` 개별적으로 각 줄을 읽을 개체 (줄 바꿈으로 구분 됨) 또는 구분 하는 방법에 관계 없이 개별 항목을 읽을 합니다.

이 절차를 읽고 앞의 예제에서 만든 데이터를 표시 하는 방법을 보여 줍니다.

1. 웹 사이트의 루트에 라는 새 파일을 만들어 *DisplayData.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    명명 된 변수에 앞의 예에서 만든 파일을 참조 하 여 시작 하는 코드 `userData`,이 메서드 호출을 사용 하 여:

    [!code-css[Main](working-with-files/samples/sample5.css)]

    이 작업을 수행 하는 코드는 내부에 `if` 문. 파일을 읽을 시기는 것이 좋습니다 사용 하는 `File.Exists` 는 파일을 사용할 수 있는지 여부를 먼저 확인 하는 메서드. 또한이 코드 파일이 비어 있는지 여부를 확인 합니다.

    페이지의 본문에는 두 개의 `foreach` 다른 중첩 된 반복 합니다. 외부 `foreach` 루프 데이터 파일에서 한 번에 한 줄을 가져옵니다. 이 경우 줄은 파일에 줄 바꿈을 정의 &#8212; 즉, 각 데이터 항목은 별도 줄. 외부 루프는 새 항목을 만듭니다 (`<li>` 요소) 안에 정렬 된 목록 (`<ol>` 요소).

    내부 반복 구분 기호로 쉼표를 사용 하는 항목 (필드)를 각 데이터 행을 분할 합니다. (이전 예제에 따라, 즉, 각 줄에 세 개의 필드가 포함 되어 있음을 &#8212; 이름, 성, 이름 및 전자 메일 주소를 각각 쉼표로 구분 하 여.) 내부 루프도 만듭니다.는 `<ul>` 데이터 줄의 각 필드에 대 한 항목 목록 및 한 목록을 표시 합니다.

    코드에는 두 개의 데이터 형식, 배열을 사용 하는 방법을 보여 줍니다. 및 `char` 데이터 형식입니다. 배열이 필요 하기 때문에 `File.ReadAllLines` 메서드는 배열로 데이터를 반환 합니다. `char` 데이터 형식이 필요 하기 때문에 `Split` 메서드가 반환 되는 `array` 각 요소는 형식에서 `char`합니다. (배열에 대 한 정보를 참조 하십시오. [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)
3. 브라우저에서 페이지를 실행 합니다. 이전 예제에 대 한 입력 한 데이터가 표시 됩니다. 

    ![[image]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> **Microsoft Excel 쉼표로 구분 된 파일에서 데이터를 표시합니다.**
> 
> Microsoft Excel을 사용 하 여 쉼표로 구분 된 파일로 스프레드시트에 포함 된 데이터를 저장할 수 있습니다 (*.csv* 파일). 이렇게 하면 파일이 Excel 형식에 없는 일반 텍스트로 저장 됩니다. 스프레드시트에서 각 행의 텍스트 파일에 줄 바꿈을 구분 된 및 각 데이터 항목은 쉼표로 구분 합니다. 파일을 읽을 Excel 쉼표로 구분 된 코드에서 데이터 파일의 이름을 변경 하면 이전 예제에 표시 된 코드를 사용할 수 있습니다.


<a id="Deleting_Files"></a>
## <a name="deleting-files"></a>파일 삭제

웹 사이트에서 파일을 삭제 하려면 사용할 수 있습니다는 `File.Delete` 메서드. 이 절차에서는 사용자가 이미지를 삭제할 수 있도록 하는 방법을 보여 줍니다 (*.jpg* 파일)에서 프로그램 *이미지* 폴더 파일의 이름을 알고 있는 경우.

> [!NOTE] 
> 
> **중요 한** 프로덕션 웹 사이트의 하면 일반적으로 제한할 수 있는 사용자는 데이터를 변경 하는 합니다. 멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자를 인증 하는 방법에 대 한 정보를 참조 하십시오. [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.


1. 웹 사이트에서 라는 하위 폴더를 만듭니다 *이미지*합니다.
2. 하나 이상의 복사 *.jpg* 로 파일은 *이미지* 폴더입니다.
3. 웹 사이트의 루트에서 라는 새 파일을 만듭니다 *FileDelete.cshtml*합니다.
4. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    이 페이지는 사용자가 이미지 파일의 이름을 입력할 수 있는 폼을 포함 합니다. 입력 하지는 *.jpg* 파일 이름 확장명; 파일 이름을 다음과 같이 제한 하 여 도움말 있습니다 하면 사용자가 사이트의 임의 파일을 삭제 합니다.

    코드에는 사용자가 입력 하 고 전체 경로 생성 한 다음 파일 이름을 읽습니다. 경로 만들려면 코드 사용 하 여 현재 웹 사이트 경로 (에서 반환 되는 `Server.MapPath` 메서드), *이미지* 폴더 이름, 사용자가 제공한 이름 및 리터럴 문자열로: ".jpg"입니다.

    코드를 호출 하 여 파일을 삭제 하는 `File.Delete` 메서드를 바로 전에 구성한 전체 경로 전달 합니다. 끝 태그에 코드 파일이 삭제 된 확인 메시지를 표시 합니다.
5. 브라우저에서 페이지를 실행 합니다. 

    ![[image]](working-with-files/_static/image5.jpg)
6. 마우스 클릭 한 다음 파일의 이름을 입력 **전송**합니다. 파일, 삭제 된 경우 파일의 이름이 페이지 맨 아래에 표시 됩니다.

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a>가 사용자가 업로드 파일

`FileUpload` 도우미 웹 사이트에 파일을 업로드 하는 사용자가 수 있습니다. 다음 절차 사용자가 단일 파일 업로드 수 있도록 하는 방법을 보여 줍니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)이전에 추가 하지 않은 경우.
2. 에 *앱\_데이터* 폴더를 새 폴더를 만들고 이름을 *UploadedFiles*합니다.
3. 만들 라는 새 파일의 루트를 *FileUpload.cshtml*합니다.
4. 다음 페이지에서 기존 내용을 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    페이지의 본문 부분은 사용 하 여는 `FileUpload` 도우미 업로드 상자와 사용자가 문제에 대해 있는 단추를 만듭니다.

    ![[image]](working-with-files/_static/image6.jpg)

    에 대해 설정한 속성은 `FileUpload` 도우미 지정 업로드할 파일에 대 한 단일 박스 원하고 제출 단추 읽기를 원하는 **업로드**합니다. (문서의 뒷부분에서 상자를 더 추가 합니다.)

    사용자가 클릭할 때 **업로드**, 페이지 맨 위에 있는 코드 파일을 저장 합니다. `Request` 양식 필드의 값을 가져오는 일반적으로 사용 하는 개체에는 `Files` 파일 (또는 파일)를 포함 하는 배열 업로드 합니다. 배열의 특정 위치에서 개별 파일을 가져올 수 있습니다 &#8212; 예를 들어 첫 번째 업로드 된 파일을 가져오려면 얻게 `Request.Files[0]`을 두 번째 파일을 가져오는 얻게 `Request.Files[1]`등입니다. (프로그래밍에서는 계산을 일반적으로 0에서 시작 해야 합니다.)

    변수에 배치 업로드 된 파일을 인출 하는 경우 (여기서 `uploadedFile`) 조작할 수 있도록 합니다. 업로드 된 파일의 이름을 확인 하려면 거 해당 `FileName` 속성입니다. 그러나 사용자는 파일 업로드 `FileName` 전체 경로가 포함 된 사용자의 원래 이름을 포함 합니다. 그는 다음과 같이 표시 될 수 있습니다.

    *C:\Users\Public\Sample.txt*

    그러나 하지 서버에 대 한 사용자의 컴퓨터에 대 한 경로 이기 때문에 모든 경로 정보를 바람직하지 않습니다. 려는 실제 파일 이름 (*Sample.txt*). 사용 하 여 경로에서 파일만 제거할 수 있습니다는 `Path.GetFileName` 다음과 같이 메서드:

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    `Path` 개체는 경로 제거, 패스를 결합 하 고 등 하는 데 사용할 수 있는 다음과 같은 메서드의 수 있는 유틸리티입니다.

    업로드 된 파일의 이름, 참조 되 면 웹 사이트에 업로드 된 파일을 저장 하려는 위치에 대 한 새 경로 작성할 수 있습니다. 결합 하는 경우에 `Server.MapPath`, 폴더 이름 (*앱\_데이터/UploadedFiles*), 및 새로 훼손된 파일 이름을 한 새 경로를 만들어야 합니다. 업로드 된 파일을 호출할 수 있습니다 `SaveAs` 메서드를 실제로 파일을 저장 합니다.
5. 브라우저에서 페이지를 실행 합니다. 

    ![[image]](working-with-files/_static/image7.jpg)
6. 클릭 **찾아보기** 업로드할 파일을 선택 합니다. 

    ![[image]](working-with-files/_static/image8.jpg)

    옆에 있는 텍스트 상자는 **찾아보기** 단추 경로 및 파일 위치를 포함 됩니다.

    ![[image]](working-with-files/_static/image9.jpg)
7. **업로드**를 클릭합니다.
8. 웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.
9. 열기는 *UploadedFiles* 폴더입니다. 업로드 한 파일은 폴더에 있습니다. 

    ![[image]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a>수 있도록 사용자가 여러 파일 업로드

이전 예에서 파일 하나만 업로드 하는 사용자가 수 있습니다. 하지만 사용할 수는 `FileUpload` 한 번에 둘 이상의 파일을 업로드 하는 도우미입니다. 한 번에 하나의 파일을 업로드 하는 중입니다.은 지루한 사진 업로드 같은 시나리오에 유용 합니다. (사진에 업로드 하는 방법에 대 한 읽을 수 [ASP.NET 웹 페이지 사이트에 이미지 작업](https://go.microsoft.com/fwlink/?LinkId=202897).) 이 예제에는 그 이상의 업로드에 동일한 기법을 사용할 수 있지만 사용자가 한 번에 두 개를 업로드 하는 방법을 보여 줍니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)아직 없는 경우, 합니다.
2. 명명 된 새 페이지를 만들고 *FileUploadMultiple.cshtml*합니다.
3. 다음 페이지에서 기존 내용을 바꿉니다.  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    이 예제는 `FileUpload` 도우미 페이지의 본문에는 기본적으로 사용자가 두 파일을 업로드할 수 있도록 구성 됩니다. 때문에 `allowMoreFilesToBeAdded` 로 설정 된 `true`, 도우미 사용자가 업로드 상자를 더 추가할 수 있는 링크를 렌더링 합니다.

    ![[image]](working-with-files/_static/image11.jpg)

    사용자 업로드 하는 파일을 처리 하려면 코드에서는 앞의 예제에서 사용한 동일한 기본 기술을 사용 &#8212; 에서 파일을 가져옵니다. `Request.Files` 저장 합니다. (다양 한 항목을 포함 하 여 수행 해야 올바른 파일 이름 및 경로 가져올 수 있습니다.) 이 이번 혁신은 사용자에 여러 파일 업로드 수를 알 수 없는 많은입니다. 가져올 수를 확인 하려면 `Request.Files.Count`합니다.

    반복 하면 손 모양 아이콘이이 번호로 `Request.Files`차례로 각 파일을 인출 하 고 저장 합니다. 컬렉션 전체 알려진된 횟수를 반복 하려는 경우 사용할 수 있습니다는 `for` 다음과 같은 루프:

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    변수 `i` 설정한 어떤 상한에는 0에서 전송 되는 임시 카운터 뿐입니다. 이 경우 최대 파일 수입니다. 있지만 시나리오 ASP.NET에서 수 계산을 위한 일반적인 경우 처럼 0에서 시작 하는 카운터, 상한값은 실제로 하나 보다 작은 파일 수입니다. (3 개의 파일을 업로드 하는 경우 개수는 0 ~ 2.)

    `uploadedCount` 변수 합계를 모든 파일을 성공적으로 업로드 하 고 저장 합니다. 이 코드는 예상 되는 파일을 업로드할 수 있는 가능성을 차지 합니다.
4. 브라우저에서 페이지를 실행 합니다. 브라우저는 페이지 및 두 개의 업로드 상자를 표시합니다.
5. 두 개의 파일을 업로드 하려면 선택 합니다.
6. 클릭 **다른 파일을 추가**합니다. 페이지는 새 업로드 상자를 표시합니다. 

    ![[image]](working-with-files/_static/image12.jpg)
7. **업로드**를 클릭합니다.
8. 웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.
9. 열기는 *UploadedFiles* 폴더 성공적으로 업로드 된 파일을 볼 수 있습니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 자료


[ASP.NET 웹 페이지 사이트에 이미지 작업](https://go.microsoft.com/fwlink/?LinkId=202897)

[CSV 파일로 내보내기](https://msdn.microsoft.com/library/ms155919.aspx)
