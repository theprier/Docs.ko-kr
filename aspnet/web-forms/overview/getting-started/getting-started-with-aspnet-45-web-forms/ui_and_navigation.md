---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: UI 및 탐색 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: d2d4101455a85c53e016e567c0cf1337642f1863
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890244"
---
<a name="ui-and-navigation"></a>UI 및 탐색
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 Wingtip Toys 저장소 프런트 응용 프로그램의 기능을 지 원하는 기본 웹 응용 프로그램의 UI를 수정 합니다. 또한 간단한 추가한 바인딩되고 데이터 탐색 합니다. 이 자습서에서는 이전 자습서 "데이터 액세스 계층 만들기"를 바탕으로 하며 Wingtip Toys 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습 내용:

- Wingtip Toys 저장소 프런트 응용 프로그램의 기능을 지원 하도록 UI를 변경 하는 방법입니다.
- 페이지 탐색을 포함 하도록 HTML5 요소를 구성 하는 방법입니다.
- 특정 제품 데이터를 탐색 하는 데이터 기반 컨트롤을 만드는 방법.
- Entity Framework Code First를 사용 하 여 만든 데이터베이스의에서 데이터를 표시 하는 방법입니다.

ASP.NET Web Forms를 사용 하 여 웹 응용 프로그램에 대 한 동적 콘텐츠를 만들 수 있습니다. 각 ASP.NET 웹 페이지 (서버 기반 처리를 포함 하지 않는 페이지)를 정적 HTML 웹 페이지와 유사한 방식으로 만들어지지만 ASP.NET 웹 페이지에는 ASP.NET에서 인식 하 고 페이지를 실행할 때 HTML을 생성 하기 위해 처리 하는 추가 요소가 포함 됩니다.

정적 HTML 페이지 (*.htm* 또는 *.html* 파일)을 충족 하는 서버는 `Web` 파일을 읽고로 전송 하 여 요청-브라우저에 합니다. 반면, ASP.NET 웹 페이지를 요청 하는 사람 (*.aspx* 파일), 웹 서버에서 프로그램으로 페이지를 실행 합니다. 페이지 실행 되는 동안 값 계산, 읽기 또는 데이터베이스 정보를 작성 또는 다른 프로그램 호출 포함 하 여 웹 사이트에 필요한 모든 작업을 수행할 수 있습니다. 출력으로 페이지는 동적으로 태그 (예: html에서 요소)를 생성 하 고 동적이 출력 브라우저에 보냅니다.

## <a name="modifying-the-ui"></a>UI를 수정합니다.

이 자습서 시리즈를 수정 하 여 계속 해 서는 *Default.aspx* 페이지. 기본 서식 파일을 응용 프로그램을 만드는 데 사용 하 여 이미 설정 되어 있는 UI를 수정 합니다. 수정 작업을 수행 합니다 유형은 Web Forms 응용 프로그램을 만들 때 일반적입니다. 제목을 변경 하 고, 일부 콘텐츠를 대체 하 고, 불필요 한 기본 콘텐츠를 제거 하 여이 작업을 수행 합니다.

1. 열거나이 클래스로 전환 하는 *Default.aspx* 페이지.
2. 페이지에 표시 되 면 **디자인** 보기에서 전환할 **소스** 보기.
3. 에 있는 페이지의 위쪽에는 `@Page` 지시문 변경은 `Title` 아래의 노란색으로 강조 표시 된 대로 특성 "시작"을 합니다. 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. *Default.aspx* 페이지에서 모두에 포함 된 기본 콘텐츠 바꾸기는 `<asp:Content>` 태그도 나타나도록 태그 아래 합니다. 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. 저장 된 *Default.aspx* 페이지를 선택 하 여 **저장 Default.aspx** 에서 **파일** 메뉴.

   그 결과 *Default.aspx* 페이지는 다음과 같이 표시 됩니다. 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

예제에서는 설정한는 `Title` 특성에는 `@Page` 지시문입니다. HTML 브라우저를 서버 코드에 표시 되 면 `<%: Page.Title %>` 에 포함 된 내용이 확인 되는 `Title` 특성입니다.

ASP.NET 웹 페이지를 구성 하는 기본 요소를 포함 하는 예제 페이지. 페이지는 HTML 페이지, ASP.NET에만 적용 되는 요소와 함께에서와 같이 정적 텍스트를 포함 합니다. 에 포함 된 콘텐츠는 *Default.aspx* 페이지를 통합 하 여 마스터 페이지 콘텐츠를이 자습서의 뒷부분에서 설명 하는 합니다.

### <a name="page-directive"></a>@Page 지시문

일반적으로 ASP.NET Web Forms 페이지에 대 한 페이지 속성 및 구성 정보를 지정할 수 있도록 하는 지시문을 포함 합니다. 페이지에서 처리 하는 방법에 대 한 지침으로 ASP.NET에서 지시문은 사용 되는 있지만 브라우저로 전송 되는 태그의 일부로 렌더링 되지 않습니다.

가장 일반적으로 사용 되는 지시문이는 `@Page` 지시문에서 다음을 포함 하 여 페이지에 대 한 많은 구성 옵션을 지정할 수 있습니다.

1. 프로그래밍 언어 C#과 같은 페이지의 코드에 대 한 서버입니다.
2. 페이지 있는 단일 파일 페이지를 호출 하는 페이지에 직접 서버 코드 페이지 인지 또는 코드 숨김 페이지를 호출 하는 별도 클래스 파일에서 코드 페이지 인지 합니다.
3. 여부 페이지는 연결 된 마스터 페이지 있으며 따라서 콘텐츠 페이지 것으로 처리 해야 합니다.
4. 디버깅 및 추적 옵션입니다.

포함 되지 않은 경우는 `@Page` 페이지에서 지시문 또는 지시문 특정 설정 포함 되지 않은 한 설정에서 상속 되지 것입니다는 *Web.config* 구성 파일 또는 *Machine.config* 구성 파일입니다. *Machine.config* 파일은 컴퓨터에서 실행 하는 모든 응용 프로그램에 대 한 추가 구성 설정을 제공 합니다.

> [!NOTE] 
> 
> *Machine.config* 도 모든 가능한 구성 설정에 대 한 세부 정보를 제공 합니다.


### <a name="web-server-controls"></a>웹 서버 컨트롤

대부분의 ASP.NET Web Forms 응용 프로그램에서 사용자가 단추, 텍스트 상자, 목록, 등 페이지와 상호 작용할 수 있는 컨트롤을 추가 합니다. 이러한 웹 서버 컨트롤은 입력된 요소 및 HTML 단추와 유사 합니다. 그러나 서버 코드를 사용 하 여 속성을 설정할 수 있도록 서버에서 처리 됩니다. 이러한 컨트롤에는 서버 코드에서 처리할 수 있는 이벤트를 발생 시킵니다.

서버 컨트롤에는 페이지를 실행할 때 ASP.NET에서 인식 하는 특수 한 구문을 사용 합니다. ASP.NET 서버 컨트롤에 대 한 태그 이름으로 시작 된 `asp:` 접두사입니다. 따라서 ASP.NET을 인식 하 고 이러한 서버 컨트롤에서 처리할 수 있습니다. 접두사는 컨트롤은.NET Framework의 일부가 아닌 경우 달라질 수 있습니다. 외에 `asp:` 접두사, ASP.NET 서버 컨트롤에도 포함 된 `runat="server"` 특성 및 `ID` 서버 코드에서 컨트롤을 참조 하는 데 사용할 수 있는 합니다.

페이지를 실행 하는 경우 ASP.NET 서버 컨트롤을 식별 하 고 이러한 컨트롤에 연관 된 코드를 실행 합니다. 여러 컨트롤을 브라우저에 표시 되 면 페이지에 몇 가지 HTML 또는 기타 태그 렌더링 합니다.

### <a name="server-code"></a>서버 코드

대부분의 ASP.NET Web Forms 응용 프로그램 페이지를 처리할 때 서버에서 실행 되는 코드를 포함 합니다. 위에서 설명 했 듯이 ListView 컨트롤에 데이터 추가 등의 다양 한 작업을 수행 하 서버 코드를 사용할 수 있습니다. ASP.NET C#, Visual Basic, J#, 및 다른 사용자를 포함 하는 서버에서 실행 되도록 많은 언어를 지원 합니다.

ASP.NET 웹 페이지에 대 한 서버 코드를 작성 하기 위한 두 가지 모델을 지원 합니다. 단일 파일 모델에서의 코드 페이지를 여는 태그를 포함 하는 스크립트 요소에는 `runat="server"` 특성입니다. 또는 코드 숨김 모델 라고 하는 별도 클래스 파일에는 페이지에 대 한 코드를 만들 수 있습니다. 이 경우 ASP.NET Web Forms 페이지에는 일반적으로 서버 코드가 없는 포함합니다. 대신,는 `@Page` 지시문에 링크 하는 정보가 포함 됩니다는 *.aspx* 를 관련 된 코드 숨김 파일과 페이지입니다.

`CodeBehind` 에 포함 된 특성의 `@Page` 지시문 별도 클래스 파일의 이름을 지정 및 `Inherits` 특성 클래스는 페이지에 해당 하는 코드 숨김 파일의 이름을 지정 합니다.

### <a name="updating-the-master-page"></a>마스터 페이지를 업데이트합니다.

ASP.NET Web Forms의 마스터 페이지를 사용 하는 페이지에 대 한 일관 된 레이아웃 응용 프로그램에서 만들 수 있습니다. 응용 프로그램 디자인 및 일부 페이지 (또는 페이지 그룹)에 대해 원하는 표준 동작을 정의 하는 단일 마스터 페이지입니다. 그런 다음 위에서 설명한 것 처럼, 표시 하려는 콘텐츠가 포함 된 개별 콘텐츠 페이지를 만들 수 있습니다. 사용자가 콘텐츠 페이지를 요청 하는 경우 ASP.NET 콘텐츠 페이지의 내용을 사용 하 여 마스터 페이지의 레이아웃을 결합 하는 출력을 생성 하기 위해 마스터 페이지와 병합 합니다.

새 사이트에는 단일 표시할 로고를 모든 페이지에 있어야 합니다. 이 로고를 추가 하려면 마스터 페이지의 HTML을 수정할 수 있습니다.

1. **솔루션 탐색기**찾기 및 열기는 **Site.Master** 페이지.
2. 페이지에 있으면 **디자인** 보기에서 전환할 **소스** 보기.
3. 업데이트 하 여 마스터 페이지 **수정 또는 추가** 노란색으로 강조 표시 하는 태그: 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

이 HTML 라는 이미지가 표시 *logo.jpg* 에서 *이미지* 나중에 추가할 웹 응용 프로그램의 폴더입니다. 마스터 페이지를 사용 하는 페이지는 브라우저에 표시 되 면 로고가 표시 됩니다. 사용자도 다시 이동 되는 사용자가 로고를 클릭 하는 경우는 *Default.aspx* 페이지. HTML 앵커 태그 `<a>` 이미지 서버 컨트롤을 래핑하고 이미지 링크의 일부분으로 포함 될 수 있습니다. `href` 루트를 지정 하는 앵커 태그에 대 한 특성 "`~/`" 링크 위치와 웹 사이트입니다. 기본적으로는 *Default.aspx* 페이지는 사용자가 웹 사이트의 루트를 탐색할 때 표시 됩니다. **이미지** `<asp:Image>` 와 같은 추가 속성은 서버 컨트롤에 포함 `BorderStyle`, 브라우저에 표시 될 때 HTML로 렌더링 하는 합니다.

### <a name="master-pages"></a>마스터 페이지

마스터 페이지 확장.master 사용한 ASP.NET 파일입니다 (예를 들어 *Site.Master*) 정적 텍스트, HTML 요소 및 서버 컨트롤을 포함할 수 있는 미리 정의 된 레이아웃을 사용 합니다. 마스터 페이지 특별 한으로 식별 되 `@Master` 지시문의 `@Page` 일반에 사용 되는 지시문 *.aspx* 페이지입니다.

이외에 `@Master` 지시문, 마스터 페이지도 포함 한 페이지에 대 한 최상위 HTML 요소를 모두 같은 `html`, `head`, 및 `form`합니다. HTML을 사용 위에 추가 마스터 페이지의 예를 들어 `table` 레이아웃의 경우는 `img` 회사 로고, 정적 텍스트와 사이트에 대 한 공통 멤버를 처리 하는 서버 컨트롤에 대 한 요소입니다. HTML 및 ASP.NET 요소 마스터 페이지의 일부로 사용할 수 있습니다.

외에 정적 텍스트와 모든 페이지에 표시 되는 컨트롤, 마스터 페이지도는 하나 이상의 **ContentPlaceHolder** 컨트롤입니다. 이러한 자리 표시자 컨트롤 영역 대체 가능한 콘텐츠가 표시 되는 위치를 정의 합니다. 차례로 대체 가능한 콘텐츠가에 정의 된 콘텐츠 페이지와 같은 *Default.aspx*를 사용 하 여는 **콘텐츠** 서버 컨트롤입니다.

#### <a name="adding-image-files"></a>이미지 파일 추가

프로젝트 브라우저에 표시 될 때 표시 될 수 있도록 모든 제품 이미지와 함께 위에서 참조 되는 로고 이미지를 웹 응용 프로그램에 추가 되어야 합니다.

#### <a name="download-from-msdn-samples-site"></a>MSDN 샘플 사이트에서 다운로드 합니다.

[ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)

리소스를 포함 하는 다운로드는 *WingtipToys 자산* 샘플 응용 프로그램을 만드는 데 사용 되는 폴더입니다.

1. 그렇게 이미 하지 않은 경우 MSDN 샘플 사이트에서 위의 링크를 사용 하 여 압축 된 샘플 파일을 다운로드 합니다.
2. 를 다운로드 한.zip 파일을 열고 내용을 컴퓨터의 로컬 폴더에 복사 합니다.
3. 찾기 및 열기는 *WingtipToys 자산* 폴더입니다.
4. 끌어서 놓아 복사는 *카탈로그* 로컬 폴더에서의 웹 응용 프로그램 프로젝트의 루트 폴더는 **솔루션 탐색기** 의 Visual Studio입니다. 

    ![UI 및 탐색-파일 복사](ui_and_navigation/_static/image1.png)
5. 다음으로 라는 새 폴더를 만듭니다 *이미지* 마우스 오른쪽 단추로 클릭 하 여는 **WingtipToys** 프로젝트에서 **솔루션 탐색기** 선택 하 고 **추가**  - &gt; **새 폴더**합니다.
6. 복사는 *logo.jpg* 에서 파일의 *WingtipToys 자산* 폴더에 **파일 탐색기** 에 *이미지* 웹 응용 프로그램의 폴더 프로젝트에서 **솔루션 탐색기** 의 Visual Studio입니다.
7. 클릭는 **모든 파일 표시** 맨 위에 있는 옵션 **솔루션 탐색기** 새 파일에 표시 되지 않으면 파일의 목록을 업데이트 합니다.  
  
    **솔루션 탐색기** 이제 업데이트 된 프로젝트 파일을 표시 합니다. 

    ![UI 및 탐색-솔루션 탐색기](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>페이지 추가

웹 응용 프로그램 탐색을 추가 하기 전에 먼저를 탐색할 수 있는 두 개의 새 페이지를 추가 합니다. 이 자습서 시리즈의 뒷부분에 나오는 이러한 새 페이지에 제품과 제품 세부 정보를 표시 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **WingtipToys**, 클릭 **추가**, 클릭 하 고 **새 항목**합니다.   
 **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 그런 다음 선택 **마스터 페이지가 있는 웹 폼** 중간에서 나열 하 고 이름을 *ProductList.aspx*합니다. 

    ![UI 및 탐색-새 항목 추가 대화 상자](ui_and_navigation/_static/image3.png)
3. 선택 **Site.Master** 마스터 페이지를 새로 만든 연결할 *.aspx* 페이지. 

    ![UI 및 탐색-마스터 페이지 선택](ui_and_navigation/_static/image4.png)
4. 라는 추가 페이지가 추가 *ProductDetails.aspx* 도 이와 동일한 단계를 수행 하 여 합니다.

### <a name="updating-bootstrap"></a>부트스트랩 업데이트

Visual Studio 2013 프로젝트 템플릿을 사용 하 여 [부트스트랩](http://getbootstrap.com/), Twitter에서 만든 프레임 워크 레이아웃 및 테마 설정입니다. 다른 브라우저 창 크기에 맞게 레이아웃 동적으로 적용할 수는 반응 형 디자인을 제공 하기 위해 CSS3를 사용 하는 부트스트랩 합니다. 또한 쉽게 응용 프로그램의 모양과 느낌에 변경 내용을 적용 하려면 부트스트랩의 테마 설정 기능을 사용할 수 있습니다. 기본적으로 Visual Studio 2013에서 ASP.NET 웹 응용 프로그램 템플릿을 부트스트랩 NuGet 패키지로 포함 됩니다.

이 자습서에서는 부트스트랩 CSS 파일을 대체 하 여 Wingtip Toys 응용 프로그램의 모양과 느낌을 변경 합니다.

1. **솔루션 탐색기**열고는 *콘텐츠* 폴더입니다.
2. 마우스 오른쪽 단추로 클릭는 *bootstrap.css* 파일 및 파일 이름을 *부트스트랩 original.css*합니다.
3. 이름 바꾸기는 *bootstrap.min.css* 를 *부트스트랩 original.min.css*합니다.
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *콘텐츠* 폴더와 선택 **파일 탐색기에서 폴더 열기**합니다.  
   파일 탐색기에 표시 됩니다. 이 위치에 다운로드 한 부트스트랩 CSS 파일을 저장 됩니다.
5. 브라우저에서로 이동 [ http://Bootswatch.com ](http://bootswatch.com/)합니다.
6. Cerulean 테마 나타날 때까지 브라우저 창을 스크롤하십시오. 

    ![UI 및 탐색-Cerulean 테마](ui_and_navigation/_static/image5.png)
7. 둘 다 다운로드는 *bootstrap.css* 파일 및 *bootstrap.min.css* 파일을 여 *콘텐츠* 폴더입니다. 에 표시 되는 콘텐츠 폴더의 경로 사용 하 여는 **파일 탐색기** 이전에 연 창에 있습니다.
8. **Visual Studio** 맨 위에 있는 **솔루션 탐색기**, 선택는 **모든 파일 표시** 콘텐츠 폴더에 새 파일을 표시 하려면 옵션입니다. 

    ![UI 및 탐색-솔루션 탐색기](ui_and_navigation/_static/image6.png)

   두 개의 새 CSS 파일에 표시 됩니다는 **콘텐츠** 폴더 하지만 각 파일 이름 옆에 아이콘이 회색입니다. 즉, 프로젝트에 파일 아직 추가 되지 않습니다.
9. 마우스 오른쪽 단추로 클릭는 *bootstrap.css* 및 *bootstrap.min.css* 파일 및 선택 **프로젝트에 포함**합니다.   
   이 자습서의 뒷부분에 나오는 Wingtip Toys 응용 프로그램을 실행 하는 경우 새 UI 표시 됩니다.

> [!NOTE] 
> 
> ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여는 *Bundle.config* 부트스트랩 CSS 파일의 경로를 저장할 프로젝트의 루트에 파일입니다.


### <a name="modifying-the-default-navigation"></a>기본 탐색을 수정

응용 프로그램의 모든 페이지에 대 한 기본 탐색에 있는 순서가 지정 되지 않은 탐색 목록 요소를 변경 하 여 수정할 수는 *Site.Master* 페이지.

1. **솔루션 탐색기**을 찾아 엽니다는 *Site.Master* 페이지.
2. 순서가 지정 되지 않은 목록 아래에 표시 된 노란색으로 강조 표시 추가 탐색 링크를 추가 합니다.   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

각 줄 항목을 수정한 위의 html 보시 `<li>` 앵커 태그를 포함 하 `<a>` 링크와 함께 `href` 특성입니다. 각 `href` 웹 응용 프로그램에서 페이지를 가리킵니다. 다음이 링크 중 하나를 클릭 하면 브라우저에서 (같은 **제품**)에 포함 된 페이지로 이동 됩니다는 `href` (같은 **ProductList.aspx**). 이 자습서의 끝에 응용 프로그램을 실행 합니다.

> [!NOTE] 
> 
> 물결표 (`~`) 문자를 사용 하도록 지정 하는 `href` 경로 프로젝트의 루트에서 시작 합니다.


### <a name="adding-a-data-control-to-display-navigation-data"></a>탐색 데이터를 표시 하는 데이터 컨트롤 추가

다음으로, 모든 데이터베이스에서 범주를 표시 하는 컨트롤을 추가 합니다. 각 범주에 대 한 링크로 할는 *ProductList.aspx* 페이지. 사용자가 브라우저에서 범주 링크를 클릭 하면 제품 페이지로 이동 하는 및 선택한 범주와 관련 된 제품만 표시 합니다.

사용 하 여 한 **ListView** 컨트롤에는 데이터베이스에 포함 된 모든 범주를 표시 합니다. 추가 하는 **ListView** 마스터 페이지에 컨트롤:

1. 에 *Site.Master* 페이지에서 강조 표시 된 다음 추가 `<div>` 요소 **후** 는 `<div>` 요소를 포함 하는 `id="TitleContent"` 앞에 추가:  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

이 코드는 데이터베이스에서 모든 범주를 표시 합니다. **ListView** 각 범주 이름은 링크 텍스트로 표시 하 고에 대 한 링크를 포함 하는 컨트롤의 *ProductList.aspx* 포함 된 쿼리 문자열 값이 있는 페이지는 `ID` 범주입니다. 설정 하 여는 `ItemType` 속성에는 **ListView** 제어, 데이터 바인딩 식을 `Item` 내에서 사용할 수는 `ItemTemplate` 노드와 컨트롤은 강력한 형식입니다. 세부 정보를 선택할 수 있습니다는 `Item` 개체, IntelliSense를 사용 하 여 지정 하는 등의 `CategoryName`합니다. 이 코드는 컨테이너 내부에 포함 된 `<%#: %>` 하는 데이터 바인딩 식을 표시 합니다. (:)의 끝에 추가 하 여는 `<%#` 접두사, 데이터 바인딩 식의 결과 HTML로 인코딩된 합니다. 응용 프로그램은 교차 사이트에 대해 더 잘 보호 결과 HTML로 인코딩 되 면 스크립트 주입 (XSS) 및 HTML 삽입 공격입니다.

> [!NOTE] 
> 
> **팁**
> 
> 개발 중에 입력 하 여 코드를 추가 하면 확인할 수 있습니다는 개체의 유효한 멤버가 발견 되었음을 강력한 형식 데이터 컨트롤 IntelliSense에 따라 사용 가능한 멤버를 표시 합니다. 속성, 메서드 및 개체 등의 코드를 입력할 때 IntelliSense에서는 코드 컨텍스트에 따라 적절 한 옵션을 제공 합니다.


다음 단계에서 구현 됩니다는 `GetCategories` 메서드 데이터를 검색 합니다.

### <a name="linking-the-data-control-to-the-database"></a>데이터 컨트롤을 데이터베이스에 연결

데이터 컨트롤에 데이터를 표시할 수 있습니다, 전에 데이터베이스에 데이터 컨트롤을 연결 해야 합니다. 코드 숨김의 링크를 수정할 수 있습니다는 *Site.Master.cs* 파일입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Site.Master* 페이지 한 다음 클릭 **코드 보기**합니다. *Site.Master.cs* 파일이 편집기에서 열립니다.
2. 시작 부분 근처의 *Site.Master.cs* 파일, 포함 된 모든 네임 스페이스는 다음과 같이 표시 되도록 두 개의 추가 네임 스페이스를 추가 합니다.  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. 강조 표시 된 추가 `GetCategories` 후 메서드는 `Page_Load` 다음과 같이 이벤트 처리기.  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

위의 코드는 마스터 페이지를 사용 하는 모든 페이지는 브라우저에 로드 될 때 실행 됩니다. `ListView` 컨트롤 (명명 된 "에 categoryList")이이 자습서의 앞부분에서 추가한 모델 바인딩을 사용 하 여 데이터를 선택 합니다. 태그에는 `ListView` 설정한 컨트롤의 컨트롤 `SelectMethod` 속성을는 `GetCategories` 위에 표시 된 메서드. `ListView` 제어 호출은 `GetCategories` 페이지의 적절 한 시간 주기 메서드와 반환된 된 데이터에 자동 바인딩됩니다. 다음 자습서에서 데이터 바인딩 방법에 대 한 좀 더 자세히 배웁니다.

### <a name="running-the-application-and-creating-the-database"></a>응용 프로그램을 실행 하 고 데이터베이스를 만드는 중

이 자습서 시리즈의 앞부분에 나오는 있습니다 ("ProductDatabaseInitializer" 라고 함)는 이니셜라이저 클래스 만들어지고 지정에서이 클래스는 *global.asax.cs* 파일입니다. Entity Framework 응용 프로그램 때문에 처음으로 실행 될 때 데이터베이스를 생성 합니다는 `Application_Start` 에 포함 된 메서드는 *global.asax.cs* 파일 이니셜라이저 클래스를 호출 합니다. 이니셜라이저 클래스 모델 클래스를 사용 합니다 (`Category` 및 `Product`) 데이터베이스를 만들려면이 자습서 시리즈의 앞부분에 나오는 추가 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Default.aspx* 페이지로 돌아간 후 선택 **시작 페이지로 설정**합니다.
2. Visual Studio에서 **F5**합니다.   
 첫 번째 실행 하는 동안 모든 항목을 설정 하는 약간의 시간이 걸립니다.   
    ![UI 및 브라우저 창 탐색-](ui_and_navigation/_static/image7.png)  
 컴파일할 응용 프로그램 및 데이터베이스의 이름이 응용 프로그램을 실행 하면 *wingtiptoys.mdf* 에서 만들 수는 *앱\_데이터* 폴더입니다. 브라우저에서 범주 탐색 메뉴를 표시 됩니다. 이 메뉴는 데이터베이스에서 사용 하 고 범주를 검색 하 여 생성 되었습니다. 다음 자습서 탐색을 구현 합니다.
3. 실행 중인 응용 프로그램을 중지 하려면 브라우저를 닫습니다.

### <a name="reviewing-the-database"></a>데이터베이스를 검토합니다.

열기는 *Web.config* 파일을 연결 문자열 섹션을 살펴봅니다. 확인할 수 있습니다는 `AttachDbFilename` 를 가리키는 연결 문자열의 값은 `DataDirectory` 웹 응용 프로그램 프로젝트에 대 한 합니다. 값 `|DataDirectory|` 예약 값 나타내는 *앱\_데이터* 프로젝트의 폴더입니다. 이 폴더는 엔터티 클래스에서 만든 데이터베이스입니다.

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> 경우는 *앱\_데이터* 폴더 비어 있으면 선택 또는 폴더가 표시 되지 않습니다는 **새로 고침** 아이콘 차례로 **모든 파일 표시** 는 맨위에있는아이콘**솔루션 탐색기** 창. 확장의 너비는 **솔루션 탐색기** windows 모든 사용 가능한 아이콘을 표시 해야 할 수 있습니다.


에 포함 된 데이터를 검사할 수 이제는 *wingtiptoys.mdf* 사용 하 여 데이터베이스 파일의 **서버 탐색기** 창.

1. 확장 된 *앱\_데이터* 폴더입니다. 경우는 *앱\_데이터* 폴더가 표시 되지 않습니다. 위의 참고를 참조 하십시오.
2. 경우는 *wingtiptoys.mdf* 데이터베이스 파일은 표시를 선택는 **새로 고침** 아이콘 차례로 **모든 파일 표시** 맨 위에 있는 아이콘은 **솔루션 탐색기**  창.
3. 마우스 오른쪽 단추로 클릭는 *wingtiptoys.mdf* 데이터베이스 파일 및 선택 **열려**합니다.  
    **서버 탐색기** 표시 됩니다. 

    ![UI 및 탐색-서버 탐색기](ui_and_navigation/_static/image8.png)
4. 확장 된 *테이블* 폴더입니다.
5. 마우스 오른쪽 단추로 클릭는 **제품**테이블을 선택한 **테이블 데이터 표시**합니다.  
 **제품** 테이블이 표시 됩니다. 

    ![UI 및 탐색-Products 테이블](ui_and_navigation/_static/image9.png)
6. 이 보기에서는 보고 데이터를 수정할 수 있습니다는 **제품** 직접 테이블입니다.
7. 닫기는 **제품** 테이블 창.
8. 에 **서버 탐색기**를 마우스 오른쪽 단추로 클릭는 **제품** 다시 테이블을 선택한 **테이블 정의 열기**합니다.  
 데이터에 맞게 디자인 한는 **제품** 테이블이 표시 됩니다. 

    ![UI 및 탐색-제품 디자인](ui_and_navigation/_static/image10.png)
9. 에 **T-SQL** 탭에 테이블을 만드는 데 사용 하는 SQL DDL 문을 표시 합니다. UI에 사용할 수도 있습니다는 **디자인** 탭 스키마를 수정할 수 있습니다.
10. 에 **서버 탐색기**를 마우스 오른쪽 단추로 클릭 **WingtipToys** 선택한 데이터베이스 **연결 닫기**합니다.   
 Visual Studio에서 데이터베이스를 분리 하 여 데이터베이스 스키마는이 자습서 시리즈의 뒷부분에 나오는 수정할 수 없게 됩니다.
11. 으로 돌아와서 **솔루션 탐색기**선택 하 여는 **솔루션 탐색기** 탭의 맨 아래에 **서버 탐색기** 창.

## <a name="summary"></a>요약

이 자습서 시리즈의 일부 기본 UI, 그래픽, 페이지 및 탐색을 추가 했습니다. 또한 이전 자습서에서 추가 하는 데이터 클래스와에서 데이터베이스를 만든 웹 응용 프로그램을 실행 했습니다. 또한의 콘텐츠를 볼는 *제품* 데이터베이스를 직접 확인 하 여 데이터베이스의 테이블입니다. 다음 자습서에서 데이터 항목 및 데이터베이스에서 세부 정보를 표시 합니다.

## <a name="additional-resources"></a>추가 자료

[ASP.NET 웹 페이지 프로그래밍 소개](https://msdn.microsoft.com/library/ms178125.aspx)   
[ASP.NET 웹 서버 컨트롤 개요](https://msdn.microsoft.com/library/zsyt68f1.aspx)   
[CSS 자습서](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [이전](create_the_data_access_layer.md)
> [다음](display_data_items_and_details.md)
