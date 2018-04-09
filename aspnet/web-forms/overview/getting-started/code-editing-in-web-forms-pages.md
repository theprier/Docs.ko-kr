---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: 코드를 Visual Studio 2013에서 ASP.NET Web Forms 편집 | Microsoft Docs
author: Erikre
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/03/2014
ms.topic: article
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 79b10df04432490d6338dadb8f7ddd36192beb3e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>Visual Studio 2013에서 코드 편집 ASP.NET Web Forms
====================
으로 [Erik Reitan](https://github.com/Erikre)

많은 ASP.NET Web Form 페이지에서 Visual Basic, C# 또는 다른 언어의 코드를 작성할 수 있습니다. Visual Studio에서 코드 편집기를 사용 하면 오류를 방지 하면서 코드를 빠르게 작성할 수 있습니다. 또한 편집기는 수행 해야 하는 작업의 양을 줄이는 데 도움을 재사용 가능한 코드를 만들 수 있습니다 방법을 제공 합니다.

이 연습에서는 Visual Studio code 편집기의 다양 한 기능을 설명 합니다.

이 연습에서는 다음 작업을 수행하는 방법을 배웁니다.

- 인라인 코딩 오류를 수정 합니다.
- 코드 리팩터링을 저장 합니다.
- 변수 및 개체의 이름을 바꿉니다.
- 코드 조각을 삽입 합니다.

## <a name="prerequisites"></a>전제 조건


이 연습을 완료하려면 다음 사항이 필요합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다. .NET Framework는 자동으로 설치 됩니다. 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013 for Web은 종종로 간주 Visual Studio이 자습서 시리즈 합니다.  
    >   
    > 이 연습에서는 선택 했다고 가정 Visual Studio를 사용 하는 경우는 **웹 개발** 설정의 컬렉션 처음으로 Visual Studio를 시작 합니다. 자세한 내용은 참조 [하는 방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.

  Visual Studio 및 ASP.NET에 대 한 소개를 참조 하십시오. [Visual Studio 2013에서 기본 ASP.NET 4.5 Web Forms 페이지를 만드는](creating-a-basic-web-forms-page.md)합니다.   
 

## <a name="creating-a-web-application-project-and-a-page"></a>웹 응용 프로그램 프로젝트 및 페이지 만들기

<a id="sectionToggle0"></a>

이 연습 부분에서는 웹 응용 프로그램 프로젝트를 만들고 새 페이지를 추가 합니다.

### <a name="to-create-a-web-application-project"></a>웹 응용 프로그램 프로젝트를 만들려면

1. Microsoft Visual Studio를 엽니다.
2. **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
    ![파일 메뉴](code-editing-in-web-forms-pages/_static/image1.png)

    **새 프로젝트** 대화 상자가 나타납니다.
3. 선택 된 **템플릿**  - &gt; **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹.
4. 선택 된 **ASP.NET 웹 응용 프로그램** 가운데 열에서 서식 파일입니다.
5. 프로젝트 이름을 ***BasicWebApp*** 클릭는 **확인** 단추입니다.   
![새 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image2.png)
6. 다음으로, 선택는 **Web Forms** 템플릿과 클릭은 **확인** 단추 프로젝트를 만듭니다.  
![새 ASP.NET 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio Web Forms 템플릿을 기반으로 하는 미리 작성 된 기능을 포함 하는 새 프로젝트를 만듭니다.


## <a name="creating-a-new-aspnet-web-forms-page"></a>새 ASP.NET Web Forms 페이지 만들기


사용 하 여 새 Web Forms 응용 프로그램을 만들 때는 **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 Visual Studio 추가 라는 ASP.NET 페이지 (Web Forms 페이지) *Default.aspx*다른 여러 파일 외에, 및 폴더입니다. 사용할 수는 *Default.aspx* 웹 응용 프로그램에 대 한 홈 페이지와 페이지입니다. 그러나이 연습에서는 만들고 새 페이지를 사용 합니다.

### <a name="to-add-a-page-to-the-web-application"></a>웹 응용 프로그램 페이지를 추가 하려면


1. **솔루션 탐색기**, 웹 응용 프로그램 이름을 마우스 오른쪽 단추로 클릭 (응용 프로그램 이름이이 자습서에서는 **BasicWebSite**)를 클릭 하 고 **추가**  - &gt; **새 항목**합니다.   
**새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 그런 다음 선택 **Web Form** 중간에서 나열 하 고 이름을 *FirstWebPage.aspx*합니다.   
    ![새 항목 추가 대화 상자](code-editing-in-web-forms-pages/_static/image4.png)
3. 클릭 **추가** Web Forms 페이지 프로젝트에 추가 합니다.  
 Visual Studio에 새 페이지에 만들어지고 열립니다.
4. 다음으로이 새 페이지의 기본 시작 페이지로 설정. **솔루션 탐색기**, 명명 된 새 페이지를 마우스 오른쪽 단추로 클릭 *FirstWebPage.aspx* 선택 **시작 페이지로 설정**합니다. 다음에 진행률을 테스트 하려면이 응용 프로그램을 실행할 때 자동으로 브라우저에서이 새 페이지를 표시 됩니다.


## <a name="correcting-inline-coding-errors"></a>인라인 코딩 오류를 수정 합니다.


Visual Studio의 코드 편집기를 사용 하면 코드를 작성 하 고 오류를 변경한 경우 코드 편집기를 사용 하면 오류를 수정 하려면 오류를 방지할 수 있습니다. 이 연습 부분에서는 편집기의 오류 수정 기능을 설명 하는 코드 줄을 작성 합니다.

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>Visual Studio에서 간단한 코드 오류를 해결 하려면


1. **디자인** 보기에 대 한 처리기를 만들 빈 페이지를 두 번 클릭은 **부하** 페이지에 대 한 이벤트입니다.   
   일부 코드를 작성 하는 장소로 이벤트 처리기를 사용 하는 있습니다.
2. 처리기를 내는 오류 메시지와 키를 눌러를 포함 하는 다음 줄을 입력 **ENTER**:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   누를 때 **ENTER**, 코드 편집기 놓이는 녹색 또는 빨간색 밑줄 (일반적으로 호출 &quot;구불구불한&quot; 줄)에서 문제가 있는 코드의 영역입니다. 녹색 밑줄 경고를 나타냅니다. 빨간색 밑줄 수정 해야 하는 오류를 나타냅니다. 

    위로 마우스 포인터를 가져가면 `myStr` 경고에 대 한를 알려 주는 도구 설명이 나타납니다. 또한 오류 메시지가 빨간색 밑줄 위로 마우스 포인터를 보유 합니다.

    다음 이미지는 밑줄을 사용 하 여 코드를 표시 합니다.

    ![디자인 뷰의 환영 텍스트](code-editing-in-web-forms-pages/_static/image5.png "디자인 뷰의 환영 텍스트")  
   세미콜론을 추가 하 여 오류를 수정 해야 `;` 줄의 끝에 있습니다. 경고 단순히 알리는 사용 하지 않은 `myStr` 아직 변수입니다.  

    > [!NOTE] 
    > 
    > Visual Studio에서 설정을 선택 하 여 서식을 현재 코드를 볼 **도구**  - &gt; **옵션**  - &gt; **글꼴 및 색**합니다.


## <a name="refactoring-and-renaming"></a>리팩터링 및 이름 바꾸기

리팩터링 쉽게 이해 하 고 해당 기능을 유지 하면서 유지 하기 위해 코드를 재구성을 포함 하는 소프트웨어 방법입니다. 간단한 예는 데이터베이스에서 데이터를 가져오는 이벤트 처리기에서 코드를 작성할 수 있습니다. 페이지를 개발할 때 여러 다른 처리기의 데이터에 액세스 할 경우 검색할 수 있습니다. 따라서 페이지에서 데이터 액세스 메서드를 만들어 처리기에서 메서드 호출을 삽입 하 여 페이지의 코드를 리팩터링 합니다.

코드 편집기에는 다양 한 리팩터링 작업을 수행할 수 있도록 도구가 포함 되어 있습니다. 이 연습에서는 두 가지 리팩터링 기법을 사용 합니다: 변수 이름을 바꾸고 메서드 추출 합니다. 리팩터링 있습니다 필드 캡슐화, 메서드 매개 변수를 지역 변수 승격 및 메서드 매개 변수를 관리 합니다. 이러한 리팩터링 옵션의 가용성을 코드에서의 위치에 따라 달라 집니다.

### <a name="refactoring-code"></a>코드 리팩터링

일반적인 리팩터링 시나리오 만들거나 추출 하는 메서드와 같은 다른 멤버 내에 있는 코드에서 메서드를 합니다. 이 원래 멤버의 크기를 줄이는 고 추출 된 코드 다시 사용할 수 있습니다.

이 연습 부분에서는 몇 가지 간단한 코드를 작성 한 다음 여기에서 한 메서드를 추출 합니다. 리팩터링 대해서는 C#, C# 프로그래밍 언어로 사용 하는 페이지를 만듭니다.

### <a name="to-extract-a-method-in-a-c-page"></a>C# 페이지의 메서드를 추출 하려면

1. 로 전환 **디자인** 보기.
2. 에 **도구 상자**에서 **표준** 탭을 끌어는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 페이지로 끌어옵니다.
3. 두 번 클릭은 **단추** 에 대 한 처리기를 만들 컨트롤을 해당 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트를 다음 강조 표시 된 코드를 추가:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   코드는 만듭니다는 **ArrayList** 개체 값을 사용 하 여이 로드 하는 루프를 사용 하 여 및 다음 다른 루프를 사용 하 여의 내용을 표시 하는 **ArrayList** 개체입니다.
4. 키를 눌러 **CTRL + f 5** 페이지를 실행 한 다음 클릭는 **단추** 되도록 다음과 같은 출력을 참조 하십시오.   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. 코드 편집기로 돌아가서 다음 이벤트 처리기에 다음 줄을 선택 합니다.   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. 선택 영역을 마우스 오른쪽 단추로 클릭 합니다. **리팩터링**를 선택한 후 **메서드 추출**합니다. 

    **메서드 추출** 대화 상자가 나타납니다.
7. 에 **새 메서드 이름** 상자에 입력 합니다 **DisplayArray**, 클릭 하 고 **확인**합니다. 

    코드 편집기에는 명명 된 새 메서드가 작성 `DisplayArray`에서 새 메서드를 호출 하 고는 **클릭** 원래 루프 처리기입니다.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. 키를 눌러 **CTRL + f 5** 페이지를 다시 실행 하 고 클릭 하 고 **단추**합니다.

    페이지 작동 하기 전과 동일 합니다. `DisplayArray` 메서드 어디에서 나 호출 될 수 있습니다 page 클래스에 있습니다.

## <a name="renaming-variables"></a>변수 이름 바꾸기

변수 뿐 아니라 개체를 사용 하는 경우에 코드에서 이미 참조 이름으로 변경는 것이 좋습니다. 그러나 변수 및 개체 이름을 바꾸는 코드 참조 중 하나의 이름을 바꾸지 되 면 중단를 발생할 수 있습니다. 따라서 리팩터링 옵션을 사용 하 여 이름을 바꿀 수 있습니다.

### <a name="to-use-refactoring-to-rename-a-variable"></a>리팩터링을 사용 하는 변수 이름을 바꾸려면


1. 에 **클릭** 이벤트 처리기를 다음 줄을 찾습니다.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. 변수 이름을 마우스 오른쪽 단추로 클릭 `alist`, 선택 **리팩터링**를 선택한 후 **이름 바꾸기**합니다.

    **이름 바꾸기** 대화 상자가 나타납니다.
3. 에 **새 이름을** 상자에 입력 합니다 **ArrayList1** 있는지 확인 하 고는 **참조 변경 내용 미리 보기** 확인란을 선택 합니다. 그런 다음 **확인**을 클릭합니다.

    **변경 내용 미리 보기** 대화 상자가 나타나고 바꾸려는 변수에 대 한 모든 참조를 포함 하는 트리를 표시 합니다.
4. 클릭 **적용** 를 닫으려면는 **변경 내용 미리 보기** 대화 상자.

    선택한 인스턴스를 구체적으로 참조 하는 변수 이름이 변경 됩니다. 그러나 하는 변수 `alist` 다음 줄에서 바뀌지 않습니다.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    변수 `alist` 이 줄에서 변경 하지 않으면 같은 값으로 변수를 표시 하지 않기 때문에 `alist` 이름을 바꾼 합니다. 변수 `alist` 에 `DisplayArray` 는 해당 메서드에 대 한 지역 변수를 선언 합니다. 리팩터링을 사용 하 여 변수를 바꾸려면 단순히; 편집기에서 찾기 및 바꾸기 작업을 수행할 때 보다 다른는 들 작동 하는 변수의 의미를 사용 하 여 리팩터링 이름 바꾸기 변수입니다.


## <a name="inserting-snippets"></a>조각 삽입

Web Forms 개발자가 자주 수행 해야 하는 많은 코딩 작업 때문에 코드 편집기의 코드 조각, 또는 미리 작성 된 코드 블록을 라이브러리를 제공 합니다. 페이지에 이러한 조각을 삽입할 수 있습니다.

Visual Studio에서 사용 하는 각 언어에 코드 조각을 삽입 하는 방법에 약간의 차이가 있습니다. 코드 조각을 삽입 하는 방법에 대 한 정보를 참조 하십시오. [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx)합니다. 코드 조각을 Visual C#에서 삽입 하는 방법에 대 한 정보를 참조 하십시오. [Visual C# 코드 조각](https://msdn.microsoft.com/library/z41h7fat.aspx)합니다.

## <a name="next-steps"></a>다음 단계

이 연습에서는 코드에서 오류를 수정, 리팩터링 코드, 변수, 이름 바꾸기 및 코드에 코드 조각을 삽입에 대 한 Visual Studio 2010 코드 편집기의 기본 기능에 설명 했습니다. 편집기에서 추가 기능 응용 프로그램을 쉽고 빠르게 개발을 가능 합니다. 예를 들어, 다음을 수행합니다.

- IntelliSense 옵션 수정, 코드 조각, 관리 및 코드 조각을 온라인 검색 같은 IntelliSense의 기능에 대해 알아보십시오. 자세한 내용은 [IntelliSense 사용](https://msdn.microsoft.com/library/hcw1s69b.aspx)을 참조하세요.
- 사용자 고유의 코드 조각을 만드는 방법을 알아봅니다. 자세한 내용은 참조 [만들기 및 사용 하 여 IntelliSense 코드 조각](https://msdn.microsoft.com/library/ms165392.aspx)
- IntelliSense 코드 조각, 코드 조각은 사용자 지정 하 고 문제 해결 등의 Visual Basic 관련 기능에 대해 자세히 알아보기 자세한 내용은 참조 [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx)
- C#에 대 한 자세한-리팩터링 및 코드 조각 같은 IntelliSense의 특정 기능입니다. 자세한 내용은 참조 [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)합니다.
