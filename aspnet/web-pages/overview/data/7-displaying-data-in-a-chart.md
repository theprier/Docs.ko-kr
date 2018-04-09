---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: ASP.NET 웹 페이지 (Razor)와 차트에 데이터를 표시 합니다. | Microsoft Docs
author: microsoft
description: 이 차트에 데이터를 표시 하는 방법을 설명 합니다. 이전 장에서 수동으로 및 표에서 데이터를 표시 하는 방법을 배웠습니다. 이 장에서 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2012
ms.topic: article
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 5cf17e54408d585e9a375b302b61b4e28d9b022a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>ASP.NET 웹 페이지 (Razor)와 차트에 데이터를 표시합니다.
====================
by [Microsoft](https://github.com/microsoft)

> 이 문서를 사용 하 여 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 데이터를 표시 하려면 차트를 사용 하는 방법에 설명 된 `Chart` 도우미입니다.
> 
> **학습할**:
> 
> - 차트에 데이터를 표시 하는 방법.
> - 기본 테마를 사용 하 여 차트 스타일을 지정 하는 방법입니다.
> - 차트를 저장 하는 방법 및 성능 향상을 위해 캐시 하는 방법입니다.
> 
> 다음은 문서에 도입 된 기능을 프로그래밍 하는 ASP.NET입니다.
> 
> - `Chart` 도우미입니다.
> 
> > [!NOTE]
> > 이 문서의 정보는 ASP.NET 웹 페이지 1.0 및 웹 페이지 2에 적용 됩니다.


<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>차트 도우미

그래픽 형식으로 데이터를 표시 하려는 경우 사용할 수 있습니다 `Chart` 도우미입니다. `Chart` 도우미 다양 한 차트 종류의에서 데이터를 표시 하는 이미지를 렌더링할 수 있습니다. 서식 및 레이블 지정에 대 한 다양 한 옵션을 지원 합니다. `Chart` 도우미 30 개 이상의 유형의 차트, Microsoft Excel 또는 다른 도구에서 사용 하 던 못할 수 있는 차트의 모든 형식을 포함 하 여 렌더링할 수 &#8212; 영역형 차트, 가로 막대형 차트, 세로 막대형 차트, 꺾은선형 차트 및 원형 차트는 자세히와 특수 차트 같은 주식형 차트입니다.

| **영역형 차트** ![설명: 영역형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image1.jpg) | **가로 막대형 차트** ![설명: 가로 막대형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **세로 막대형 차트** ![설명: 세로 막대형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image3.jpg) | **꺾은선형 차트** ![설명: 꺾은선형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **원형 차트** ![설명: 원형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image5.jpg) | **주식형 차트** ![설명: 주식형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>차트 요소

차트는 데이터와 범례, 축, 계열 등과 같은 추가 요소를 보여 줍니다. 다음 그림을 사용 하는 경우를 사용자 지정할 수 있는 한 차트 요소는 `Chart` 도우미입니다. 이 문서에서는 일부를 설정 하는 방법을 보여 줍니다 (모두는 아님) 이러한 요소입니다.

![차트 요소를 보여 주는 설명: 그림](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>데이터에서 차트 만들기

차트에 표시할 데이터 또는 XML 파일에 있는 데이터는 데이터베이스에서 반환 된 결과에서 배열을에서 수 있습니다.

### <a name="using-an-array"></a>배열을 사용 하 여

에 설명 된 대로 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890), 배열 유사한 항목의 컬렉션을 단일 변수에 저장할 수 있습니다. 차트에 포함할 데이터를 포함 하는 배열을 사용할 수 있습니다.

이 절차를 만드는 방법을 차트를 배열에 있는 데이터로 기본 차트 종류를 사용 하 여 보여 줍니다. 또한 페이지 내에서 차트를 표시 하는 방법을 보여 줍니다.

1. 라는 새 파일을 만들어 *ChartArrayBasic.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    먼저이 코드에서는 너비 및 높이 설정 하 고 새 차트를 만듭니다. 사용 하 여 차트 제목의 지정 된 `AddTitle` 메서드. 사용 데이터를 추가 하려면는 `AddSeries` 메서드. 이 예제를 사용 하 여는 `name`, `xValue`, 및 `yValues` 의 매개 변수는 `AddSeries` 메서드. `name` 매개 변수는 차트 범례에 표시 됩니다. `xValue` 매개 변수는 차트의 가로 축을 따라 표시 되는 데이터의 배열을 포함 합니다. `yValues` 매개 변수는 차트의 세로 축을 따라 하는 데 사용 되는 데이터의 배열을 포함 합니다.

    `Write` 메서드 실제로 차트를 렌더링 합니다. 이 경우에 차트 종류를 지정 하지 않은 때문에 `Chart` 도우미는 세로 막대형 차트는 해당 기본 차트를 렌더링 합니다.
3. 브라우저에서 페이지를 실행 합니다. 브라우저에서 차트를 표시합니다. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>데이터베이스 쿼리를 사용 하 여 차트 데이터에 대 한

차트에 표시할 정보는 데이터베이스에 있으면 데이터베이스 쿼리를 실행 하 고 결과의 데이터를 사용 하 여 차트를 만들 수 있습니다. 이 절차를 읽고 문서에서 만든 데이터베이스의 데이터를 표시 하는 방법을 보여 줍니다. [ASP.NET 웹 페이지 사이트에서 데이터베이스 작업을 소개](https://go.microsoft.com/fwlink/?LinkId=202893)합니다.

1. 추가 *앱\_데이터* 폴더가 아직 없는 경우 웹 사이트의 루트 폴더입니다.
2. 에 *앱\_데이터* 폴더를 명명 된 데이터베이스 파일을 추가 *SmallBakery.sdf* 에 설명 되어 있는 [ASP.NET웹페이지사이트의데이터베이스작업소개](https://go.microsoft.com/fwlink/?LinkId=202893).
3. 라는 새 파일을 만들어 *ChartDataQuery.cshtml*합니다.
4. 기존 콘텐츠를 다음으로 바꿉니다.   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    코드는 먼저 SmallBakery 데이터베이스 열리고 이라는 변수에 할당 `db`합니다. 이 변수는 나타냅니다는 `Database` 읽기 / 쓰기 데이터베이스를 사용할 수 있는 개체입니다. 다음으로 코드의 이름 및 각 제품의 가격을 얻으려고 SQL 쿼리를 실행 합니다. 새 차트를 만들고 차트의 호출 하 여 데이터베이스 쿼리를 전달 `DataBindTable` 메서드. 이 메서드는 두 개의 매개 변수:는 `dataSource` 쿼리에서 데이터에 대 한 매개 변수는 및 `xField` 매개 변수를 사용 하는 차트의 x 축에 사용 되는 데이터 열을 설정할 수 있습니다.

    사용 하는 대신는 `DataBindTable` 사용할 수는 `AddSeries` 의 메서드는 `Chart` 도우미입니다. `AddSeries` 메서드를 사용 설정할 수 있습니다는 `xValue` 및 `yValues` 매개 변수입니다. 예를 들어, 사용 하는 대신는 `DataBindTable` 다음과 같이 메서드:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    사용할 수는 `AddSeries` 다음과 같이 메서드:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    모두 동일한 결과 렌더링 합니다. `AddSeries` 메서드는 차트 종류와 데이터를 더 명시적으로 지정할 수 있으므로 보다 유연 하지만 `DataBindTable` 메서드는 유연성이 필요 하지 않으면 사용 하기가 더 쉽습니다.
5. 브라우저에서 페이지를 실행 합니다. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>XML 데이터를 사용 하 여

차트에 대 한 세 번째 옵션은 차트에 대 한 데이터와 XML 파일을 사용 하는 것입니다. 이 위해서는 XML 파일도 있어야 스키마 파일 (*.xsd* 파일) XML 구조를 설명 하는 합니다. 이 절차를 XML 파일에서 데이터를 읽는 방법을 보여 줍니다.

1. 에 *앱\_데이터* 폴더 라는 새 XML 파일을 만듭니다 *data.xml*합니다.
2. 기존 XML는 가상의 회사의 직원에 대 한 일부 XML 데이터를 다음과 같이 바꿉니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. 에 *앱\_데이터* 폴더 라는 새 XML 파일을 만듭니다 *data.xsd*합니다. (확장이 이번은 *.xsd*.)
4. 기존 XML을 다음으로 바꿉니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 웹 사이트의 루트에서 라는 새 파일을 만듭니다 *ChartDataXML.cshtml*합니다.
6. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    코드는 먼저 만듭니다는 `DataSet` 개체입니다. 이 개체는 XML 파일에서 읽은 및 스키마 파일의 정보에 따라 구성 하는 데이터를 관리 하려면 사용 됩니다. (코드의 맨 위에 문을 포함 하는 예 고 `using SystemData`합니다. 이 작업을 수행할 수 있도록 하는 데 필요한는 `DataSet` 개체입니다. 자세한 내용은 참조 [ &quot;Using&quot; 문 및 정규화 된 이름](#SB_UsingStatements) 이 문서의 뒷부분에 나오는.)

    그런 다음 코드는 만듭니다는 `DataView` 데이터 집합을 기반으로 하는 개체입니다. 차트에 바인딩할 수 있는 개체를 제공 하는 데이터 뷰의 &#8212; 즉, 읽기 및 출력 합니다. 차트를 사용 하 여 데이터에 바인딩하는 `AddSeries` 메서드 때 설명 했 듯이 배열 데이터 점을 제외 하 고이 시간을 차트로 만들 때는 `xValue` 및 `yValues` 매개 변수를 설정는 `DataView` 개체입니다.

    이 예제는 특정 차트 종류를 지정 하는 방법을 보여줍니다. 데이터에 추가 된 경우는 `AddSeries` 메서드는 `chartType` 원형 차트를 표시 하려면 매개 변수 설정도 합니다.
7. 브라우저에서 페이지를 실행 합니다. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using" 문 및 정규화 된 이름
> 
> Razor 구문이 있는 ASP.NET 웹 페이지를 기반으로 하는.NET Framework 구성 요소 (클래스)의 수천 이루어져 있습니다. 으로 구성 하는 이러한 모든 클래스를 사용 하려면 관리할 수 있도록 하려면 *네임 스페이스*, 라이브러리와 비슷하게는 합니다. 예를 들어는 `System.Web` 브라우저/서버 통신을 지 원하는 클래스를 포함 하는 네임 스페이스는 `System.Xml` 만들고 XML 파일을 읽는 데 사용 되는 클래스를 포함 하는 네임 스페이스 및 `System.Data` 작업할 수 있도록 하는 클래스를 포함 하는 네임 스페이스 데이터입니다.
> 
> .NET Framework의 클래스에 액세스 하려면 코드 뿐 아니라 클래스 이름 뿐만 아니라 클래스가 있는 네임 스페이스를 알고 있어야 합니다. 예를 들어, 사용 하려면는 `Chart` 도우미, 코드 찾이 필요가 `System.Web.Helpers.Chart` 네임 스페이스를 결합 하는 클래스 (`System.Web.Helpers`)를 클래스 이름 (`Chart`). 클래스의로 알려져 *정식* 이름 &#8212; .NET Framework는 (광활) 내에서 완전 하 고 명확한 위치입니다. 코드에서이 다음과 같습니다.
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 그러나 것은 번거로운 일일 (및 오류 발생 가능성도)를 클래스 또는 도우미를 참조할 때마다 이러한 long, 정규화 된 이름을 사용 해야 합니다. 따라서 쉽게 클래스 이름을 사용 하려면 *가져올* 일반적으로에 관심이 한 네임 스페이스는.NET Framework에서 여러 개의 네임 스페이스 중에서 약간 합니다. 네임 스페이스를 가져와야 하는 경우 클래스 이름만 사용할 수 있습니다 (`Chart`) 정규화 된 이름 대신 (`System.Web.Helpers.Chart`). 코드를 실행 하 고 클래스 이름에서 발생 하는 경우 해당 클래스를 찾기 위해 가져온 네임 스페이스에서 확인할 수 있습니다.
> 
> Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하 여 웹 페이지를 만들 때 일반적으로 동일한 클래스 집합인 때마다 사용을 포함 하는 `WebPage` 클래스, 다양 한 도우미 등에입니다. 웹 사이트를 만들 때마다 관련 네임 스페이스를 가져오는 작업을 저장 하려면 ASP.NET 구성 된가 모든 웹 사이트에 대 한 핵심 네임 스페이스의 집합을 자동으로 가져옵니다. 바로 이러한 이유로 네임 스페이스 또는; 지금까지 가져오기 처리 해야 하지 않은 작업 했던 모든 클래스를 이미 가져온 네임 스페이스에 있습니다.
> 
> 그러나 때로는 해야를 자동으로 가져온 네임 스페이스에 없는 클래스와 함께 작동 하도록 합니다. 이 경우 해당 클래스의 정규화 된 이름을 사용 하거나 또는 클래스를 포함 하는 네임 스페이스를 수동으로 가져올 수 있습니다. 사용 된 네임 스페이스를 가져오려면는 `using` 문 (`import` Visual Basic에서) 이전 예제에서 볼 수 있듯이, 문서.
> 
> 예를 들어는 `DataSet` 클래스에는 `System.Data` 네임 스페이스입니다. `System.Data` 네임 스페이스는 ASP.NET Razor 페이지를 자동으로 사용할 수 없습니다. 따라서 사용 하는 `DataSet` 의 정규화 된 이름을 사용 하 여 클래스, 다음과 같은 코드를 사용할 수 있습니다.
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 사용 해야 하는 경우는 `DataSet` 반복 해 서 클래스 다음과 같이 네임 스페이스를 가져오고 다음 클래스 이름만 사용 하 여 코드에서 수 있습니다.
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 추가할 수 있습니다 `using` 참조할 다른.NET Framework 네임 스페이스용 문입니다. 그러나 앞에서 설명한 것 처럼 필요가 없습니다 이렇게 자주 사용 하는 클래스의 대부분에서 사용 하기 위해 ASP.NET에서 자동으로 가져온 네임 스페이스에 있기 때문에 *.cshtml* 및 *.vbhtml* 페이지입니다.


<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>웹 페이지는 차트를 표시합니다.

예제에서 살펴본 지금까지 차트를 만들고 차트를 그래픽으로 브라우저에 직접 렌더링 되는 다음 합니다. 대부분의 경우에서 하지만 브라우저에서 단독으로 뿐 아니라 차트 페이지의 일부로 표시 하려는 합니다. 이렇게 하려면 2 단계 프로세스를 필요 합니다. 첫 번째 단계는 이미 살펴보았습니다 처럼 차트를 생성 하는 페이지를 만드는 것입니다.

결과 이미지는 다른 페이지에 표시 하는 두 번째 단계가입니다. HTML을 사용 하면 이미지를 표시 하려면 `<img>` 요소를 동일한 방식으로 모든 이미지를 표시 하는 것입니다. 그러나 참조 하는 대신는 *.jpg* 또는 *.png* 파일인은 `<img>` 요소 참조는 *.cshtml* 포함 된 파일은 `Chart` 도우미는 차트를 만듭니다. 표시 페이지 실행 하는 경우, `<img>` 요소의 출력을 가져옵니다는 `Chart` 도우미 하 고 차트를 렌더링 합니다.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. 라는 파일을 만들어 *ShowChart.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    코드를 사용 하 여는 `<img>` 에 앞에서 만든 차트를 표시 하는 요소는 *ChartArrayBasic.cshtml* 파일입니다.
3. 브라우저에서 웹 페이지를 실행 합니다. *ShowChart.cshtml* 파일에 포함 된 코드에 따라 차트 이미지의 표시는 *ChartArrayBasic.cshtml* 파일입니다.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>차트 스타일 지정

`Chart` 도우미 많은 수의 차트의 모양을 사용자 지정할 수 있는 옵션을 지원 합니다. 색, 글꼴, 테두리 및 등을 설정할 수 있습니다. 차트의 모양을 사용자 지정 하는 쉬운 방법을 사용 하는 것을 *테마*합니다. 테마는 글꼴, 색, 레이블, 색상표, 테두리 및 효과 사용 하 여 차트를 렌더링 하는 방법을 지정 하는 정보의 모음입니다. (참고 차트의 스타일 차트 종류를 나타내지 않습니다.)

다음 표에서 기본 테마를 나열합니다.

| 테마 | 설명 |
| --- | --- |
| `Vanilla` | 흰색 배경 기반 빨간색 열을 표시합니다. |
| `Blue` | 표시 파란색 파란색 배경의 그라데이션 열. |
| `Green` | 표시 열에 녹색 그라데이션 배경이 파란색입니다. |
| `Yellow` | 그라데이션 배경이 노란색인에서 주황색 열을 표시 합니다. |
| `Vanilla3D` | 흰색 배경 기반 3 차원 빨간색 열을 표시합니다. |

새 차트를 만들 때 사용 하는 테마를 지정할 수 있습니다.

1. 라는 새 파일을 만들어 *ChartStyleGreen.cshtml*합니다.
2. 다음 페이지에서 기존 내용을 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    이 코드는 데이터에 대 한 데이터베이스를 사용 하지만 추가 하는 이전 예제와 동일는 `theme` 를 만들 때 매개 변수는 `Chart` 개체입니다. 다음은 변경된 된 코드입니다.

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 브라우저에서 페이지를 실행 합니다. 이전에 동일한 데이터를 올바르게 표시 되는데 더 세련 된 차트를 찾습니다. 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>차트 저장

사용 하는 경우는 `Chart` 때 도우미를 살펴 보았으며 지금까지이 문서에서는 도우미가 다시 만듭니다 처음부터 차트를 호출할 때마다 합니다. 필요한 경우 차트에 대 한 코드 또한 데이터베이스를 다시 쿼리 또는 XML 파일 데이터를 가져오는 데 다시 읽습니다. 경우에 따라이 작업은 복잡 한 작업 같은 수를 쿼리 하는 데이터베이스는 크기가 클 경우 또는 XML 파일은 많은 양의 데이터를 포함 하는 경우. 동적으로 이미지를 만드는 과정 서버 리소스를 차지 차트에는 많은 데이터와 관계 없는, 경우에 있으며 많은 사람들이 페이지 또는 차트를 표시 하는 페이지를 요청 하는 경우 있을 수 있습니다 영향을 미치는 웹 사이트의 성능에 있습니다.

에 차트 만들기, 잠재적인 성능 영향을 줄이는 데 도움이 되는 첫 번째 차트 시간을 만들 수 있습니다에 필요 하 고 저장 하십시오. 방금 수 다시을 생성 하는 것이 아니라 차트 다시 필요한 저장된 된 버전을 렌더링 합니다.

다음과 같은이 방법으로 차트를 저장할 수 있습니다.

- (서버)에서 컴퓨터 메모리에 차트를 캐시 합니다.
- 차트를 이미지 파일로 저장 합니다.
- 차트를 XML 파일로 저장 합니다. 이 옵션에는 저장 하기 전에 차트를 수정할 수 있습니다.

### <a name="caching-a-chart"></a>차트를 캐시합니다.

차트를 만든 후에이 캐시할 수 있습니다. 차트를 캐시를 다시 표시 해야 하는 경우 다시 생성 될 필요가 없습니다 의미 합니다. 캐시에 차트를 저장 하는 경우 해당 차트에 고유 해야 하는 키를 지정 합니다.

서버 메모리가 부족 한 경우 캐시에 저장 하는 차트를 제거 될 수 있습니다. 또한 어떤 이유로 든 응용 프로그램 다시 시작 될 경우 캐시가 지워집니다. 따라서 캐시 된 차트와 함께 작동 하도록 표준 방법은 항상 캐시에 사용 되는 여부와 그렇지 않은 경우 먼저를 확인 하려면 다음을 만들거나 다시 만들 것입니다.

1. 웹 사이트의 루트에 라는 파일을 만들어 *ShowCachedChart.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>` 태그를 포함 한 `src` 특성을 가리키는 *ChartSaveToCache.cshtml* 파일을 쿼리 문자열로 페이지에는 키를 전달 합니다. 키 값이 들어 &quot;myChartKey&quot;합니다. *ChartSaveToCache.cshtml* 파일에 포함 되어는 `Chart` 차트를 만드는 도우미입니다. 잠시 후에이 페이지를 만듭니다.

    페이지의 끝에는 명명 된 페이지 링크 *ClearCache.cshtml*합니다. 또한 만들고 곧 하는 페이지입니다. 필요한는 *ClearCache.cshtml* 이 예제에 대 한 캐싱을 테스트에-은 링크 또는 캐시 된 차트와 함께 작업 하는 경우 일반적으로 포함 하는 페이지입니다.
3. 웹 사이트의 루트에 라는 새 파일을 만들어 *ChartSaveToCache.cshtml*합니다.
4. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    코드는 먼저 쿼리 문자열의 키 값으로 전달 된 아무 것도 있는지 여부를 확인 합니다. 코드를 호출 하 여 캐시에서 차트를 읽을 하려고 하는 등의 `GetFromCache` 메서드와 키를 전달 합니다. 사실은 해당 키 (처음 차트를 요청 했을 때)에서 캐시에 아무것도 없는 경우 코드는 일반적으로 차트를 만듭니다. 차트 완료 되 면 코드에 저장 된 캐시를 호출 하 여 `SaveToCache`합니다. 해당 메서드는 키 (하므로 차트 나중에 요청 수) 및 차트를 캐시에 저장 해야 하는 시간의 양이 필요 합니다. (정확한 시간 차트를 캐시 하는 해당 데이터 변경 될 수 있습니다 생각 얼마나 자주에 의존 합니다.) `SaveToCache` 방법을 사용 하려면는 `slidingExpiration` 매개 변수 &#8212; 이 설정 된 경우 true 이면 제한 시간 카운터를 차트에 액세스 하는 때마다 재설정 됩니다. 이 경우 실제로 의미를 차트의 캐시 항목 만료 2 분 후에 마지막으로 다른 사람이 액세스 차트. (상대 만료를 대신 사용 하는 절대 만료, 캐시 엔트리를 얼마나 자주 액세스 했는지에 관계 없이 캐시에 추가 된 후 2 분 정확히 유효 기간이 만료 될 의미입니다.)

    코드에서 사용 하는 마지막으로 `WriteFromCache` 메서드를 인출 하 고 캐시에서 차트를 렌더링 합니다. 이 메서드는 외부 참고는 `if` 가져오게 됩니다 차트 캐시에서 차트 처음에 있던 또는 생성 하 고 캐시에 저장 해야 하기 때문에 캐시를 확인 하는 블록입니다.

    예제에서는 다음에 유의 `AddTitle` 메서드 타임 스탬프를 포함 합니다. (현재 날짜 및 시간 추가 &#8212; `DateTime.Now` &#8212; 제목입니다.)
5. 명명 된 새 페이지를 만들고 *ClearCache.cshtml* 해당 콘텐츠는 다음과 같이 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    이 페이지를 사용 하는 `WebCache` 에 캐시 된 차트를 제거 하는 도우미 *ChartSaveToCache.cshtml*합니다. 앞에서 설명한 대로 다음과 같은 페이지를 가질 필요가 일반적으로 합니다. 만드는 여기 쉽게 캐싱을 테스트에 합니다.
6. 실행 된 *ShowCachedChart.cshtml* 브라우저에서 웹 페이지입니다. 페이지에 포함 된 코드에 따라 차트 이미지에 표시 됩니다는 *ChartSaveToCache.cshtml* 파일입니다. 차트 제목에 표시 될 타임 스탬프의 기록해 둡니다. 

    ![차트 제목에 타임 스탬프를 갖는 기본 차트 그림 설명:](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 브라우저를 닫습니다.
8. 실행 된 *ShowCachedChart.cshtml* 다시 합니다. 표시 타임 스탬프 동일한 이전 처럼 차트 다시 생성 하지 못했습니다 하지만 대신는 캐시에서 읽어 나타냅니다.
9. *ShowCachedChart.cshtml*, 클릭는 **캐시 지우기** 링크 합니다. 이 *ClearCache.cshtml*, 보고서 캐시 처리가 지워졌습니다.
10. 클릭는 **ShowCachedChart.cshtml 돌아가려면** 연결 하거나 다시 실행 *ShowCachedChart.cshtml* WebMatrix에서 합니다. 이 시간 타임 스탬프가 변경 되었는지 확인, 캐시를 지웠습니다 때문에 합니다. 따라서 코드 차트를 다시 생성 하 고 캐시에 다시 배치 했습니다.

### <a name="saving-a-chart-as-an-image-file"></a>차트를 이미지 파일로 저장

차트를 이미지 파일로 저장할 수도 있습니다 (예:로 *.jpg* 파일) 서버에서 합니다. 다음 이미지 파일 이미지를 동일한 방식으로 사용할 수 있습니다. 장점은 파일 임시 캐시에 저장 하지 않고 저장은입니다. (예: 1 시간 마다) 서로 다른 시간에 새 차트 이미지를 저장할 수 있으며 시간에 따라 발생 하는 변경의 영구 기록이 유지 합니다. 웹 응용 프로그램에 이미지 파일을 저장할 서버 폴더에 파일을 저장할 수 있는 권한이 있는지 확인 해야 하는 참고 합니다.

1. 웹 사이트의 루트에 라는 폴더를 만든  *\_ChartFiles* 아직 없는 경우.
2. 웹 사이트의 루트에 라는 새 파일을 만들어 *ChartSave.cshtml*합니다.
3. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    코드를 보려면 먼저 확인 여부는 *.jpg* 파일이 호출 하 여는 `File.Exists` 메서드. 코드에서는 새 파일이 없는 경우 `Chart` 배열에서 합니다. 이 이번에는 코드 호출은 `Save` 메서드와 전달은 `path` 을 차트를 저장할 파일 이름과 파일 경로 지정 하려면 매개 변수입니다. 페이지의 본문에는 `<img>` 를 가리키도록 경로 사용 하는 요소는 *.jpg* 표시할 파일입니다.
4. 실행 된 *ChartSave.cshtml* 파일입니다.
5. WebMatrix에 반환 합니다. 이미지 파일로 라는 사라졌는지 *chart01.jpg* 에 저장 된는  *\_ChartFiles* 폴더입니다.

### <a name="saving-a-chart-as-an-xml-file"></a>차트를 XML 파일로 저장

마지막으로 차트는 서버에서 XML 파일로 저장할 수 있습니다. 차트를 캐시 하거나 파일에 차트를 저장 하는 보다이 방법을 사용 하는 이점은 하려는 경우 차트를 표시 하기 전에 XML을 수정할 수 있습니다. 응용 프로그램에서 이미지 파일을 저장 하려는 폴더를 서버에 대 한 읽기/쓰기 권한이 있어야 합니다.

1. 웹 사이트의 루트에 라는 새 파일을 만들어 *ChartSaveXml.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    이 코드는 앞에서 본 캐시에 차트를 저장 하기 위한 XML 파일을 사용 하 여 코드와 비슷합니다. 코드를 호출 하 여 XML 파일의 존재 여부를 먼저 확인 된 `File.Exists` 메서드. 코드에서는 새 파일이 있으면 `Chart` 개체 및 파일 이름으로 전달 된 `themePath` 매개 변수입니다. 이 메서드는 XML 파일에 무엇이 기준으로 차트를 만듭니다. XML 파일 존재 하지 않는 경우 평상시 처럼 차트를 만들고 표준 호출 `SaveXml` 저장 합니다. 차트를 사용 하 여 렌더링 되는 `Write` 메서드를 때를 살펴 보았으며 하기 전에.

    캐싱 표시 되는 페이지와 마찬가지로이 코드는 차트 제목에 타임 스탬프를 포함 합니다.
3. 명명 된 새 페이지를 만들고 *ChartDisplayXMLChart.cshtml* 다음 태그를 추가 합니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. 실행 된 *ChartDisplayXMLChart.cshtml* 페이지. 차트가 표시 됩니다. 타임 스탬프에서에서 기록해 차트의 제목입니다.
5. 브라우저를 닫습니다.
6. WebMatrix에서 마우스 오른쪽 단추로 클릭는  *\_ChartFiles* 폴더를 클릭 하 여 **새로 고침**를 다음 폴더를 엽니다. *XMLChart.xml* 이 폴더에 파일을 만들지는 `Chart` 도우미입니다. 

    ![설명: 차트 도우미에서 만든 XMLChart.xml 파일을 보여 주는 _ChartFiles 폴더입니다.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. 실행 된 *ChartDisplayXMLChart.cshtml* 페이지를 다시 합니다. 차트는 처음 실행 페이지와 동일한 타임 스탬프를 보여줍니다. 이전에 저장 하는 XML에서 생성 되는 차트 때문입니다.
8. WebMatrix에서 엽니다는  *\_ChartFiles* 폴더와 삭제는 *XMLChart.xml* 파일입니다.
9. 실행 된 *ChartDisplayXMLChart.cshtml* 페이지를 한 번 더 합니다. 이 이번에 타임 스탬프가 업데이트 하기 때문에 `Chart` 도우미 XML 파일을 다시 만들 해야 했습니다. 원하는 경우 확인는  *\_ChartFiles* 폴더 및 XML 파일은 다시 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 자료

- [ASP.NET 웹에서 데이터베이스 작업 소개 사이트 페이지](https://go.microsoft.com/fwlink/?LinkId=202893)
- [성능 향상을 위해 사이트 페이지를 ASP.NET 웹에서 캐싱 사용](https://go.microsoft.com/fwlink/?LinkId=202903)
- [차트 클래스](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (MSDN에서 ASP.NET 웹 페이지 API 참조)
