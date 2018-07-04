---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: UI 및 탐색 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: f8570942c094edc0a2825613be634fbfb447b13c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37394280"
---
<a name="ui-and-navigation"></a>UI 및 탐색
====================
[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 Wingtip Toys 저장소 프런트 응용 프로그램의 기능을 지원 하도록 기본 웹 응용 프로그램의 UI를 수정 합니다. 또한 간단한 추가 하 고 탐색 하는 데이터 바인딩. 이 자습서는 이전 자습서 "데이터 액세스 레이어 만들기" 빌드하고 Wingtip Toys 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습할 내용:

- Wingtip Toys 저장소 프런트 응용 프로그램의 기능을 지원 하도록 UI를 변경 하는 방법입니다.
- 페이지 탐색을 포함 하는 HTML5 요소를 구성 하는 방법.
- 특정 제품 데이터를 이동 하기 위한 데이터 기반 컨트롤을 만드는 방법입니다.
- Entity Framework Code First를 사용 하 여 생성 된 데이터베이스에서 데이터를 표시 하는 방법입니다.

ASP.NET Web Forms를 사용 하면 웹 응용 프로그램에 대 한 동적 콘텐츠를 만들 수 있습니다. 각 ASP.NET 웹 페이지 (서버 기반 처리를 포함 하지 않는 페이지)에 정적 HTML 웹 페이지에 비슷한 방식으로 만들어지지만 ASP.NET 웹 페이지에는 ASP.NET 인식 하 고 페이지를 실행할 때 HTML을 생성 하는 프로세스는 추가 요소가 포함 됩니다.

정적 HTML 페이지를 사용 하 여 (*.htm* 또는 *.html* 파일)을 충족 하는 서버는 `Web` 파일을 읽고로 보내기 요청-브라우저에 합니다. 반면에 ASP.NET 웹 페이지를 요청 하는 사용자가 (*.aspx* 파일), 웹 서버에서 프로그램으로 페이지를 실행 합니다. 페이지 실행 되는 동안 값 계산, 읽기, 데이터베이스 정보를 작성 또는 다른 프로그램 호출 비롯 하 여 웹 사이트에 필요한 모든 작업을 수행할 수 있습니다. 해당 출력으로 페이지는 동적으로 (예: html에서 요소) 태그를 생성 하 고 브라우저에 동적이 출력을 보냅니다.

## <a name="modifying-the-ui"></a>UI를 수정합니다.

이 자습서 시리즈 계속 해 서 수정 하 여 합니다 *Default.aspx* 페이지입니다. 응용 프로그램을 만드는 데 기본 템플릿에 의해 이미 설정 되어 있는 UI를 수정 합니다. Web Forms 응용 프로그램을 만들 때 작업을 수행 하는 수정 유형은 일반적인 합니다. 제목을 변경, 일부 콘텐츠를 대체 하 고 불필요 한 기본 콘텐츠를 제거 하 여이 작업을 합니다.

1. 열거나으로 전환 합니다 *Default.aspx* 페이지입니다.
2. 페이지에 나타나면 **디자인** 보기에서 전환할 **원본** 보기.
3. 페이지의 맨 위에 있는 합니다 `@Page` 지시문을 변경 합니다 `Title` 아래에 노란색 강조 표시 된 대로 특성 "시작"을 합니다. 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. 또는 합니다 *Default.aspx* 페이지에서 모든에 포함 된 기본 콘텐츠 자리는 `<asp:Content>` 태그도 나타나도록 태그 아래입니다. 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. 저장 된 *Default.aspx* 선택 하 여 페이지 **Default.aspx 저장** 에서 **파일** 메뉴.

   결과 *Default.aspx* 페이지는 다음과 같이 표시 됩니다. 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

예에서 설정한 합니다 `Title` 특성을 `@Page` 지시문입니다. HTML 서버 코드를 브라우저에 표시 되 면 `<%: Page.Title %>` 에 포함 된 콘텐츠를 확인 합니다 `Title` 특성입니다.

예제 페이지는 ASP.NET 웹 페이지를 구성 하는 기본 요소를 포함 합니다. 페이지는 ASP.NET 관련 된 요소와 함께 HTML 페이지를에서 같이 정적 텍스트를 포함 합니다. 에 포함 된 콘텐츠를 *Default.aspx* 페이지는이 자습서의 뒷부분에서 설명 하는 마스터 페이지 콘텐츠를 사용 하 여 통합 될 예정입니다.

### <a name="page-directive"></a>@Page 지시문

일반적으로 ASP.NET Web Forms 페이지의 페이지 속성 및 구성 정보를 지정할 수 있도록 지시문이 포함 됩니다. 지시문은 사용 하 여 ASP.NET에서 명령으로 프로세스 페이지 하는 방법에 대 한 있지만 브라우저에 보내지는 태그의 일부로 렌더링 되지 않습니다.

자주 사용 하는 지시문이는 `@Page` 지시문 다음을 포함 하 여 페이지에 대 한 다양 한 구성 옵션을 지정할 수 있습니다.

1. 프로그래밍 언어 C#과 같은 페이지에서 코드에 대 한 서버입니다.
2. 페이지의 단일 파일 페이지를 호출 하는 페이지에서 직접 서버 코드를 사용 하 여 페이지 인지 또는 코드 숨김 페이지 라고 하는 별도 클래스 파일에서 코드를 사용 하 여 페이지 인지 합니다.
3. 여부 페이지가 연결 된 마스터 페이지를 포함 하 고 콘텐츠 페이지로 처리 되어야 하므로.
4. 디버깅 및 추적 옵션입니다.

포함 되지 않은 경우는 `@Page` 페이지 지시문 또는 지시문에는 특정 설정이 포함 되어 있지 않으면, 설정에서 상속 됩니다 합니다 *Web.config* 구성 파일 또는 *Machine.config* 구성 파일입니다. 합니다 *Machine.config* 파일은 컴퓨터에서 실행 하는 모든 응용 프로그램에 추가 구성 설정을 제공 합니다.

> [!NOTE] 
> 
> 합니다 *Machine.config* 모든 가능한 구성 설정에 대 한 자세한 정보도 제공 합니다.


### <a name="web-server-controls"></a>웹 서버 컨트롤

대부분의 ASP.NET Web Forms 응용 프로그램 단추, 텍스트 상자, 목록 등과 같은 페이지와 상호 작용할 수 있도록 컨트롤을 추가 합니다. 이러한 웹 서버 컨트롤은 HTML 단추 및 입력된 요소와 비슷합니다. 그러나 서버 코드를 사용 하 여 해당 속성을 설정할 수 있도록 서버에서 처리 됩니다. 이러한 컨트롤에는 서버 코드에서 처리할 수 있는 이벤트를 발생 시킵니다.

서버 컨트롤에는 ASP.NET 페이지를 실행할 때 인식 하는 특수 구문을 사용 합니다. ASP.NET 서버 컨트롤 태그 이름을 사용 하 여 시작을 `asp:` 접두사입니다. 따라서 ASP.NET을 인식 하 고 이러한 서버 컨트롤을 처리 합니다. 접두사는 컨트롤의.NET Framework의 일부가 아닌 경우 달라질 수 있습니다. 외에 `asp:` ASP.NET 서버 컨트롤 접두사를 포함 합니다 `runat="server"` 특성 및 `ID` 서버 코드에서 컨트롤을 참조 하는 데 사용할 수 있는 합니다.

페이지를 실행 하는 경우 ASP.NET 서버 컨트롤을 식별 하 고 해당 컨트롤과 연결 된 코드를 실행 합니다. 많은 컨트롤을 브라우저에 표시 되 면 페이지에 HTML 또는 기타 태그 렌더링 합니다.

### <a name="server-code"></a>서버 코드

대부분의 ASP.NET Web Forms 응용 프로그램 페이지를 처리할 때 서버에서 실행 되는 코드를 포함 합니다. 위에서 설명한 대로 서버 코드 ListView 컨트롤에 데이터 추가 등의 다양 한 작업에 사용할 수 있습니다. ASP.NET 등 C#, Visual Basic, J#에서는 서버에서 실행 하려면 여러 언어를 지원 합니다.

ASP.NET 웹 페이지에 대 한 서버 코드를 작성 하기 위한 두 가지 모델을 지원 합니다. 단일 파일 모델을 페이지에 대 한 코드는 여는 태그에 포함 되는 스크립트 요소에는 `runat="server"` 특성입니다. 또는 코드 숨김 모델 이라고 하는 별도 클래스 파일에서 페이지에 대 한 코드를 만들 수 있습니다. 이 경우 ASP.NET Web Forms 페이지 일반적으로 서버 코드가 없습니다. 대신 합니다 `@Page` 지시문에 링크 하는 정보가 포함 됩니다. 합니다 *.aspx* 해당 관련 된 코드 숨김 파일을 사용 하 여 페이지입니다.

`CodeBehind` 에 포함 된 특성을 `@Page` 지시문은 별도 클래스 파일의 이름을 지정 및 `Inherits` 특성 페이지에 해당 하는 코드 숨김 파일 내 클래스의 이름을 지정 합니다.

### <a name="updating-the-master-page"></a>마스터 페이지를 업데이트 하는 중

ASP.NET Web Forms에서 마스터 페이지를 사용 응용 프로그램에서 페이지에 일관 된 레이아웃을 만들 수 있습니다. 단일 마스터 페이지는 응용 프로그램에서 모양과 느낌 및 일부 페이지 (또는 페이지 그룹)에 대해 원하는 표준 동작을 정의 합니다. 그런 다음 위에서 설명한 것 처럼 표시 하려는 콘텐츠가 포함 된 개별 콘텐츠 페이지를 만들 수 있습니다. 사용자가 콘텐츠 페이지에 요청 하는 경우 ASP.NET 콘텐츠 페이지의 콘텐츠와 마스터 페이지의 레이아웃을 결합 하는 출력을 생성 하기 위해 마스터 페이지를 사용 하 여 하를 병합 합니다.

새 사이트에는 단일 로고를 모든 페이지에 표시 해야 합니다. 이 로고를 추가 하려면 마스터 페이지의 HTML을 수정할 수 있습니다.

1. **솔루션 탐색기**찾기 및 열기, 합니다 **Site.Master** 페이지입니다.
2. 페이지에 있으면 **디자인** 보기에서 전환할 **원본** 보기.
3. 마스터 페이지를 업데이트할 **수정 또는 추가** 노란색으로 강조 표시 하는 태그: 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

이 HTML 라는 이미지를 표시 됩니다 *logo.jpg* 에서 합니다 *이미지* 나중에 추가할 수 있는 웹 응용 프로그램의 폴더입니다. 마스터 페이지를 사용 하는 페이지를 브라우저에 표시 되 면 로고가 표시 됩니다. 사용자가 로고를 클릭 하면 사용자는 이동 다시 합니다 *Default.aspx* 페이지입니다. HTML 앵커 태그 `<a>` 이미지 서버 컨트롤을 래핑하고 이미지 링크의 일부로 포함 될 수 있습니다. `href` 루트를 지정 하는 앵커 태그에 대 한 특성 "`~/`" 링크 위치에 따라 웹 사이트입니다. 기본적으로 *Default.aspx* 웹 사이트의 루트에 사용자가 탐색 하면 페이지가 표시 됩니다. 합니다 **이미지** `<asp:Image>` 와 같은 추가 속성은 서버 컨트롤에 포함 `BorderStyle`를 브라우저에 표시 될 때 HTML로 렌더링 하는 합니다.

### <a name="master-pages"></a>마스터 페이지

마스터 페이지는 확장.master를 사용 하 여 ASP.NET 파일 (예를 들어 *Site.Master*) 정적 텍스트, HTML 요소 및 서버 컨트롤을 포함할 수 있는 미리 정의 된 레이아웃을 사용 합니다. 마스터 페이지는 특수 한으로 식별 되 `@Master` 대체 하는 지시문의 `@Page` 일반적인에 사용 되는 지시문 *.aspx* 페이지입니다.

외에 `@Master` 지시문에 마스터 페이지도 포함의 모든 페이지에 대 한 최상위 HTML 요소와 같은 `html`, `head`, 및 `form`합니다. 예를 들어 위에서 추가한 마스터 페이지에서 사용할 HTML `table` 레이아웃에 대 한는 `img` 회사 로고, 정적 텍스트 및 사이트에 대 한 일반적인 멤버 자격을 처리 하는 서버 컨트롤에 대 한 요소입니다. 마스터 페이지의 일부로 모든 HTML 및 ASP.NET 요소를 사용할 수 있습니다.

정적 텍스트와 모든 페이지에 표시 되는 컨트롤 외에도 마스터 페이지도 하나 이상 포함 **ContentPlaceHolder** 컨트롤입니다. 이러한 자리 표시자 컨트롤 영역을 대체할 수 있는 콘텐츠 표시 되는 위치를 정의 합니다. 대체할 수 있는 콘텐츠에에서 정의 된 콘텐츠 페이지와 같은 *Default.aspx*를 사용 하 여 합니다 **콘텐츠** 서버 컨트롤입니다.

#### <a name="adding-image-files"></a>이미지 파일 추가

프로젝트 브라우저에서 표시 될 때 표시 될 수 있도록 모든 제품 이미지와 함께 위에서 참조 되는 로고 이미지를 웹 응용 프로그램에 추가 되어야 합니다.

#### <a name="download-from-msdn-samples-site"></a>MSDN 샘플 사이트에서 다운로드 합니다.

[Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)

다운로드에는 리소스가 포함 된 *WingtipToys 자산* 샘플 응용 프로그램을 만드는 데 사용 되는 폴더입니다.

1. 이미 않았다면 MSDN 샘플 사이트에서 위의 링크를 사용 하 여 압축 된 샘플 파일을 다운로드 합니다.
2. 다운로드 되 면.zip 파일을 열고 내용을 컴퓨터의 로컬 폴더로 복사 합니다.
3. 찾기 및 열기를 *WingtipToys 자산* 폴더입니다.
4. 끌어서 놓아 복사 합니다 *카탈로그* 에서 웹 응용 프로그램 프로젝트의 루트에 로컬 폴더에서 폴더를 **솔루션 탐색기** Visual Studio의 합니다. 

    ![UI 및 탐색-파일 복사](ui_and_navigation/_static/image1.png)
5. 다음으로 라는 새 폴더를 만듭니다 *이미지* 마우스 오른쪽 단추로 클릭 합니다 **WingtipToys** 프로젝트 **솔루션 탐색기** 선택 하 고 **추가**  - &gt; **새 폴더**합니다.
6. 복사를 *logo.jpg* 에서 파일을 *WingtipToys 자산* 폴더에 **파일 탐색기** 에 *이미지* 웹 응용 프로그램의 폴더 프로젝트 **솔루션 탐색기** Visual Studio입니다.
7. 클릭 합니다 **모든 파일 표시** 맨 위에 있는 옵션 **솔루션 탐색기** 새 파일이 표시 되지 않는 경우 파일의 목록을 업데이트 합니다.  
  
    **솔루션 탐색기** 이제 업데이트 된 프로젝트 파일을 표시 합니다. 

    ![UI 및 탐색-솔루션 탐색기](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>페이지 추가

웹 응용 프로그램 탐색을 추가 하기 전에 처음으로 이동 하는 두 개의 새 페이지를 추가 합니다. 이 자습서 시리즈의 뒷부분에 나오는 이러한 새 페이지에서 제품 및 제품 세부 정보를 표시할 수 있습니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **WingtipToys**, 클릭 **추가**를 클릭 하 고 **새 항목**합니다.   
 **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 그런 다음 선택 **마스터 페이지를 사용 하 여 Web Form** 중간에서 나열 하 고 이름을 *ProductList.aspx*합니다. 

    ![UI 및 탐색-새 항목 추가 대화 상자](ui_and_navigation/_static/image3.png)
3. 선택 **Site.Master** 마스터 페이지를 새로 만든 연결할 *.aspx* 페이지입니다. 

    ![UI 및 탐색-마스터 페이지 선택](ui_and_navigation/_static/image4.png)
4. 라는 추가 페이지 추가 *ProductDetails.aspx* 이와 동일한 단계를 수행 하 여 합니다.

### <a name="updating-bootstrap"></a>부트스트랩을 업데이트 하는 중

Visual Studio 2013 프로젝트 템플릿을 사용 하 여 [부트스트랩](http://getbootstrap.com/), Twitter에서 만든 레이아웃 및 테마 프레임 워크입니다. 부트스트랩 CSS3를 사용 하 여 레이아웃 다른 브라우저 창 크기를 동적으로 조정할 수는 반응 형 디자인을 제공 합니다. 또한 쉽게 응용 프로그램의 모양 및 느낌이 변경 내용을 적용 하려면 부트스트랩 테마 기능을 사용할 수 있습니다. 기본적으로 Visual Studio 2013에서 ASP.NET 웹 응용 프로그램 템플릿을 NuGet 패키지로 부트스트랩을 포함합니다.

이 자습서에서는 Wingtip Toys 응용 프로그램의 모양과 느낌 부트스트랩 CSS 파일을 대체 하 여 변경 합니다.

1. **솔루션 탐색기**오픈 합니다 *콘텐츠* 폴더입니다.
2. 마우스 오른쪽 단추로 클릭 합니다 *bootstrap.css* 파일 및 파일 이름을 *부트스트랩 original.css*합니다.
3. 이름 바꾸기는 *bootstrap.min.css* 하 *부트스트랩 original.min.css*합니다.
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *콘텐츠* 폴더를 선택 **파일 탐색기에서 폴더 열기**합니다.  
   파일 탐색기에 표시 됩니다. 이 위치에 다운로드 한 부트스트랩 CSS 파일에 저장 됩니다.
5. 브라우저에서로 이동 [ http://Bootswatch.com ](http://bootswatch.com/)합니다.
6. Cerulean 테마 표시 될 때까지 브라우저 창을 스크롤하십시오. 

    ![UI 및 탐색-Cerulean 테마](ui_and_navigation/_static/image5.png)
7. 모두 다운로드 합니다 *bootstrap.css* 파일 및 *bootstrap.min.css* 파일을 합니다 *콘텐츠* 폴더입니다. 경로에 표시 되는 콘텐츠 폴더를 사용 합니다 **파일 탐색기** 이전에 열린 창입니다.
8. **Visual Studio** 맨 위에 있는 **솔루션 탐색기**를 선택 합니다 **모든 파일 표시** 콘텐츠 폴더에 새 파일을 표시 하는 옵션입니다. 

    ![UI 및 탐색-솔루션 탐색기](ui_and_navigation/_static/image6.png)

   두 개의 새 CSS 파일이 표시 됩니다는 **콘텐츠** 폴더 하지만 각 파일 이름 옆에 아이콘이 회색입니다. 즉, 프로젝트에 파일을 아직 추가 되지 않습니다.
9. 마우스 오른쪽 단추로 클릭 합니다 *bootstrap.css* 하며 *bootstrap.min.css* 파일과 선택 **프로젝트에 포함**합니다.   
   이 자습서의 뒷부분에 나오는 Wingtip Toys 응용 프로그램을 실행 하면 새 UI 표시 됩니다.

> [!NOTE] 
> 
> ASP.NET 웹 응용 프로그램 템플릿을 사용 하는 *Bundle.config* 부트스트랩 CSS 파일의 경로 저장 하려면 프로젝트의 루트에 있는 파일입니다.


### <a name="modifying-the-default-navigation"></a>기본 탐색을 수정

응용 프로그램에서 모든 페이지에 대 한 기본 탐색에 있는 순서가 지정 되지 않은 탐색 목록 요소를 변경 하 여 수정할 수는 *Site.Master* 페이지입니다.

1. **솔루션 탐색기**을 찾아 엽니다 합니다 *Site.Master* 페이지입니다.
2. 아래에 표시 된 순서가 지정 되지 않은 목록에는 노란색으로 강조 표시 추가 탐색 링크를 추가 합니다.   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

각 줄 항목을 수정 하는 위의 HTML에서 보듯이 `<li>` 앵커 태그를 포함 하 `<a>` 링크를 사용 하 여 `href` 특성입니다. 각 `href` 웹 응용 프로그램에서 페이지를 가리킵니다. 이러한 링크 중 하나를 클릭할 때 브라우저에서 (같은 **제품**), 이러한에 포함 된 페이지로 이동 됩니다는 `href` (같은 **ProductList.aspx**). 이 자습서의 끝에 응용 프로그램을 실행 합니다.

> [!NOTE] 
> 
> 물결표 (`~`) 문자를 사용 하는 지정 하는 `href` 경로 프로젝트의 루트에서 시작 합니다.


### <a name="adding-a-data-control-to-display-navigation-data"></a>탐색 데이터를 표시 하는 데이터 컨트롤 추가

그런 다음 모든 데이터베이스에서 범주를 표시 하는 컨트롤을 추가 합니다. 각 범주에 대 한 링크 역할을 할 합니다 *ProductList.aspx* 페이지입니다. 사용자가 브라우저에 범주 링크를 클릭 하면는 제품 페이지를 탐색 하며 선택한 범주와 관련 된 제품만 표시 합니다.

사용 하 여는 **ListView** 컨트롤을 데이터베이스에 포함 된 모든 범주를 표시 합니다. 추가 하는 **ListView** 마스터 페이지에 컨트롤:

1. 에 *Site.Master* 페이지에서 강조 표시 된 다음 추가 `<div>` 요소 **후** 는 `<div>` 요소를 포함 하는 `id="TitleContent"` 앞부분에서 추가한:  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

이 코드는 데이터베이스에서 모든 범주를 표시 합니다. **ListView** 각 범주 이름은 링크 텍스트로 표시 하 고 링크를 포함 하는 컨트롤을 *ProductList.aspx* 포함 된 쿼리 문자열 값이 있는 페이지를 `ID` 범주. 설정 하 여는 `ItemType` 속성에는 **ListView** 컨트롤을 데이터 바인딩 식을 `Item` 내에서 사용할 수는 `ItemTemplate` 노드와 컨트롤은 강력한 형식의 합니다. 세부 정보를 선택할 수 있습니다 합니다 `Item` IntelliSense를 사용 하 여 지정 하는 등 개체를 `CategoryName`입니다. 이 코드는 컨테이너 내에 포함 되어 `<%#: %>` 데이터 바인딩 식을 표시 하는 합니다. (:)의 끝에 추가 하 여는 `<%#` 접두사, 데이터 바인딩 식의 결과 HTML로 인코딩. 응용 프로그램은 교차 사이트에 대해 잘 보호 하 고 결과 HTML로 인코딩된 경우 주입 (XSS) 및 HTML 삽입 공격을 스크립팅 합니다.

> [!NOTE] 
> 
> **팁**
> 
> 개발 하는 동안 입력 하 여 코드를 추가 하면 됩니다는 개체의 유효한 멤버가 강력한 형식 데이터 컨트롤 IntelliSense에 따라 사용 가능한 멤버를 표시 합니다. 속성, 메서드 및 개체와 같은 코드를 입력할 때 IntelliSense 상황에 맞는 적절 한 코드 옵션을 제공 합니다.


다음 단계에서 구현 된 `GetCategories` 데이터를 검색 하는 방법.

### <a name="linking-the-data-control-to-the-database"></a>데이터 컨트롤을 데이터베이스에 연결

데이터 컨트롤에서 데이터를 표시할 수 있습니다, 전에 데이터베이스에 데이터 컨트롤을 연결 해야 합니다. 링크를가 하도록 뒤의 코드를 수정할 수 있습니다 합니다 *Site.Master.cs* 파일입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *Site.Master* 페이지를 클릭 한 다음 **코드 보기**합니다. 합니다 *Site.Master.cs* 파일이 편집기에서 열립니다.
2. 시작 부분의 합니다 *Site.Master.cs* 파일, 포함 된 모든 네임 스페이스는 다음과 같이 표시 되도록 두 개의 추가 네임 스페이스를 추가 합니다.  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. 강조 표시 된 추가 `GetCategories` 메서드는 `Page_Load` 같이 이벤트 처리기:  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

위의 코드는 마스터 페이지를 사용 하는 모든 페이지를 브라우저에 로드 될 때 실행 됩니다. `ListView` 컨트롤 (명명 된 "categoryList")이이 자습서의 앞부분에서 추가한 모델 바인딩을 사용 하 여 데이터를 선택 합니다. 태그에는 `ListView` 컨트롤을 설정한 컨트롤 `SelectMethod` 속성을는 `GetCategories` 위에 표시 된 메서드. 합니다 `ListView` 컨트롤을 호출 합니다 `GetCategories` 페이지의 적절 한 시간 주기 메서드와 반환된 된 데이터를 자동으로 바인딩합니다. 다음 자습서에서 데이터 바인딩 자세히 배웁니다.

### <a name="running-the-application-and-creating-the-database"></a>응용 프로그램을 실행 하 고 데이터베이스를 만드는 중

이 자습서 시리즈의 앞부분에 나오는 ("ProductDatabaseInitializer" 라고 함)는 이니셜라이저 클래스를 생성 하 고이이 클래스를 지정 합니다 *global.asax.cs* 파일입니다. Entity Framework 응용 프로그램 때문에 처음으로 실행 될 때 데이터베이스를 생성 합니다는 `Application_Start` 에 포함 된 메서드를 *global.asax.cs* 파일은 이니셜라이저 클래스를 호출 합니다. 이니셜라이저 클래스는 모델 클래스를 사용 하 여 (`Category` 고 `Product`) 데이터베이스를 만들려면이 자습서 시리즈의 앞부분에서 추가한 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *Default.aspx* 페이지를 선택 **시작 페이지로 설정**합니다.
2. 키를 눌러 Visual Studio에서에서 **F5**합니다.   
 첫 번째 실행 동안 모든 설정에 약간의 시간이 걸립니다.   
    ![UI 및 탐색-브라우저 Windows](ui_and_navigation/_static/image7.png)  
 응용 프로그램을 실행 하는 경우 응용 프로그램이 컴파일될 및 데이터베이스의 이름이 *wingtiptoys.mdf* 만들어집니다 합니다 *앱\_데이터* 폴더. 브라우저에서 범주 탐색 메뉴를 표시 됩니다. 이 메뉴는 데이터베이스에서 범주를 검색 하 여 생성 되었습니다. 다음 자습서에서는 탐색을 구현 합니다.
3. 실행 중인 응용 프로그램을 중지 하려면 브라우저를 닫습니다.

### <a name="reviewing-the-database"></a>데이터베이스를 검토합니다.

엽니다는 *Web.config* 파일 및 연결 문자열 섹션을 살펴봅니다. 볼 수 있습니다 합니다 `AttachDbFilename` 연결 문자열에 값을 `DataDirectory` 웹 응용 프로그램 프로젝트에 대 한 합니다. 값 `|DataDirectory|` 나타내는 예약 된 값인 합니다 *앱\_데이터* 프로젝트의 폴더입니다. 이 폴더는 엔터티 클래스에서 생성 된 데이터베이스가 있는 위치입니다.

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> 경우는 *앱\_데이터* 폴더 표시 되어 있지 않거나 빈 폴더가 있으면 선택 합니다 **새로 고침** 아이콘 차례로 합니다 **모든 파일 표시** 합니다 맨위에있는아이콘**솔루션 탐색기** 창입니다. 너비를 확장 합니다 **솔루션 탐색기** windows 모든 사용 가능한 아이콘을 표시 해야 할 수 있습니다.


이제 포함 된 데이터를 검사할 수 있습니다 합니다 *wingtiptoys.mdf* 사용 하 여 데이터베이스 파일을 **서버 탐색기** 창입니다.

1. 확장 된 *앱\_데이터* 폴더입니다. 경우는 *앱\_데이터* 폴더 표시 되지 않습니다. 위의 참고를 참조 하세요.
2. 경우는 *wingtiptoys.mdf* 데이터베이스 파일은 표시를 선택 합니다 **새로 고침** 아이콘 차례로 **모든 파일 표시** 맨 위에 있는 아이콘은 **솔루션 탐색기**  창입니다.
3. 마우스 오른쪽 단추로 클릭 합니다 *wingtiptoys.mdf* 데이터베이스 파일 및 선택 **오픈**합니다.  
    **서버 탐색기** 표시 됩니다. 

    ![UI 및 탐색-서버 탐색기](ui_and_navigation/_static/image8.png)
4. 확장 된 *테이블* 폴더입니다.
5. 마우스 오른쪽 단추로 클릭 합니다 **제품**선택한 테이블 **테이블 데이터 표시**합니다.  
 합니다 **제품** 테이블이 표시 됩니다. 

    ![UI 및 탐색-Products 테이블](ui_and_navigation/_static/image9.png)
6. 이 보기를 사용 하면 보고 데이터를 수정 합니다 **제품** 손으로 테이블입니다.
7. 닫기 합니다 **제품** 테이블 창입니다.
8. 에 **서버 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **제품** 선택한 테이블을 다시 **테이블 정의 열기**합니다.  
 데이터에 대 한 디자인 된 **제품** 테이블이 표시 됩니다. 

    ![UI 및 탐색-제품 디자인](ui_and_navigation/_static/image10.png)
9. 에 **T-SQL** 탭 테이블을 만들 때 사용한 SQL DDL 문이 표시 됩니다. UI를 사용할 수도 있습니다는 **디자인** 스키마를 수정 하는 탭 합니다.
10. 에 **서버 탐색기**를 마우스 오른쪽 단추로 클릭 **WingtipToys** 선택한 데이터베이스 **근접 연결**합니다.   
 Visual Studio에서 데이터베이스를 분리 하 여 데이터베이스 스키마를이 자습서 시리즈의 뒷부분에 나오는 수정할 수 있습니다.
11. 돌아갑니다 **솔루션 탐색기**를 선택 하 여는 **솔루션 탐색기** 아래쪽의 탭의 **서버 탐색기** 창.

## <a name="summary"></a>요약

이 자습서 시리즈의 일부 기본 UI, 그래픽, 페이지 및 탐색을 추가 했습니다. 또한 이전 자습서에서 추가한 데이터 클래스에서 데이터베이스를 만들 웹 응용 프로그램을 실행 했습니다. 또한 본 내용의 합니다 *제품* 데이터베이스를 직접 확인 하 여 데이터베이스의 테이블입니다. 다음 자습서에서는 데이터 항목 및 데이터베이스에서 세부 정보를 표시 합니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 프로그래밍 소개](https://msdn.microsoft.com/library/ms178125.aspx)   
[ASP.NET 웹 서버 컨트롤 개요](https://msdn.microsoft.com/library/zsyt68f1.aspx)   
[CSS 자습서](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [이전](create_the_data_access_layer.md)
> [다음](display_data_items_and_details.md)
