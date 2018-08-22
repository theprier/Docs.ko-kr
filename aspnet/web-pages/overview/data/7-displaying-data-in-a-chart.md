---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: ASP.NET Web Pages (Razor)를 사용 하 여 차트의 데이터를 표시 합니다. | Microsoft Docs
author: microsoft
description: 이 차트에 데이터를 표시 하는 방법을 설명 합니다. 이전 장에서 수동으로 및 표에 데이터를 표시 하는 방법을 알아보았습니다. 이 장에서 설명 하는 중...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 00529355476e88c47ab790121ae77202aa5e7b76
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829617"
---
<a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>ASP.NET 웹 페이지 (Razor)를 사용 하 여 차트에 데이터 표시
====================
[Microsoft](https://github.com/microsoft)

> 이 문서를 사용 하 여 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 데이터를 표시할 차트를 사용 하는 방법을 설명 합니다 `Chart` 도우미입니다.
> 
> **학습할**:
> 
> - 차트의 데이터를 표시 하는 방법입니다.
> - 기본 테마를 사용 하 여 차트 스타일을 지정 하는 방법입니다.
> - 차트를 저장 하는 방법 및 성능 향상을 위해 캐시 하는 방법입니다.
> 
> ASP.NET 문서에 도입 된 기능을 프로그래밍은 다음과 같습니다.
> 
> - `Chart` 도우미입니다.
> 
> > [!NOTE]
> > 이 문서의 정보는 ASP.NET 웹 페이지 1.0 및 웹 페이지 2에 적용 됩니다.


<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>차트 도우미

그래픽 양식에서 데이터를 표시 하려는 경우 사용할 수 있습니다 `Chart` 도우미입니다. `Chart` 도우미 차트 종류의 다양 한 데이터를 표시 하는 이미지를 렌더링할 수 있습니다. 서식 및 레이블 지정에 대 한 다양 한 옵션을 지원 합니다. 합니다 `Chart` 도우미 30 개 이상의 유형의 차트, Microsoft Excel 또는 다른 도구에서 사용 하 던 못할 수 있는 차트의 모든 형식을 포함 하 여 렌더링할 수 있습니다 &#8212; 영역형 차트, 가로 막대형 차트, 세로 막대형 차트, 꺾은선형 차트 및 원형 차트는 자세히와 주식형 차트 등의 특수 차트.

| **영역형 차트** ![설명: 영역 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image1.jpg) | **가로 막대형 차트** ![설명: 가로 막대형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **세로 막대형 차트** ![설명: 세로 막대형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image3.jpg) | **꺾은선형 차트** ![설명: 꺽은선형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **원형 차트** ![설명: 원형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image5.jpg) | **주식형 차트** ![설명: 주식형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>차트 요소

차트는 데이터 및 범례, 축, 계열 등과 같은 추가 요소를 보여 줍니다. 다음 그림은 다양 한 사용 하는 경우 사용자 지정할 수 있는 차트 요소를 보여 줍니다는 `Chart` 도우미입니다. 이 문서에서는 일부를 설정 하는 방법을 보여 줍니다 (모두는 아님) 요소입니다.

![차트 요소를 보여 주는 설명: 그림](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>데이터에서 차트 만들기

데이터베이스에서 반환 된 결과에서 배열, 또는 XML 파일에 있는 데이터에서 차트에 표시할 데이터를 수 있습니다.

### <a name="using-an-array"></a>배열을 사용 하 여

에 설명 된 대로 [ASP.NET 웹 페이지 Razor 구문으로 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890), 배열을 사용 하면 유사한 항목의 컬렉션을 단일 변수에 저장 합니다. 차트에 포함 하려는 데이터를 포함 하도록 배열을 사용할 수 있습니다.

이 절차 어떻게 만들 수 있습니다 차트를 배열에 있는 데이터로 기본 차트 종류를 사용 하 여 보여 줍니다. 또한 페이지 내에서 차트를 표시 하는 방법을 보여 줍니다.

1. 라는 새 파일을 만듭니다 *ChartArrayBasic.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    코드를 먼저 새 차트를 만들고 해당 너비와 높이 설정 합니다. 사용 하 여 차트 제목의 지정 된 `AddTitle` 메서드. 사용할 데이터를 추가 하 여 `AddSeries` 메서드. 이 예제를 사용 하 여 합니다 `name`, `xValue`, 및 `yValues` 의 매개 변수는 `AddSeries` 메서드. `name` 매개 변수가 차트 범례에 표시 됩니다. `xValue` 매개 변수는 차트의 가로 축을 따라 표시 되는 데이터의 배열을 포함 합니다. `yValues` 매개 변수는 차트의 세로 축을 따라 하는 데 사용 되는 데이터의 배열을 포함 합니다.

    `Write` 메서드 실제로 차트를 렌더링 합니다. 이 경우 차트 종류를 지정 하지 않으므로 `Chart` 도우미 세로 막대형 차트는 해당 기본 차트를 렌더링 합니다.
3. 브라우저에서 페이지를 실행 합니다. 브라우저에는 차트가 표시 됩니다. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>데이터베이스 쿼리를 사용 하 여 차트 데이터에 대 한

차트에 표시할 정보를 데이터베이스에 있으면 데이터베이스 쿼리를 실행할 수 있으며 결과에서 데이터를 사용 하 여 차트를 만들 수 있습니다. 이 절차에서는 읽기 및 문서에서 만든 데이터베이스의 데이터를 표시 하는 방법을 보여 줍니다 [ASP.NET Web Pages 사이트에서 데이터베이스를 사용 하 여 작업 소개](https://go.microsoft.com/fwlink/?LinkId=202893)합니다.

1. 추가 된 *앱\_데이터* 폴더가 아직 없는 경우 웹 사이트의 루트 폴더입니다.
2. 에 *앱\_데이터* 폴더를 명명 된 데이터베이스 파일을 추가 *SmallBakery.sdf* 에 설명 되어 있는 [ASP.NET웹페이지사이트에서데이터베이스작업을소개](https://go.microsoft.com/fwlink/?LinkId=202893).
3. 라는 새 파일을 만듭니다 *ChartDataQuery.cshtml*합니다.
4. 기존 콘텐츠를 다음으로 바꿉니다.   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    코드를 먼저 SmallBakery 데이터베이스 열리고 라는 변수에 할당 `db`합니다. 이 변수는 나타냅니다는 `Database` 에서 읽기 및 쓰기 데이터베이스에 사용할 수 있는 개체입니다. 다음으로, 코드 이름 및 각 제품의 가격을 가져오는 SQL 쿼리를 실행 합니다. 코드는 새 차트를 만들고 차트의 호출 하 여 데이터베이스 쿼리를 전달 `DataBindTable` 메서드. 이 메서드는 두 매개 변수: 합니다 `dataSource` 매개 변수는 쿼리에서 데이터 및 `xField` 매개 변수를 사용 하면 차트의 x 축에 사용 되는 데이터 열을 설정 합니다.

    사용 하는 대신 합니다 `DataBindTable` 메서드를 사용할 수는 `AddSeries` 메서드의 `Chart` 도우미입니다. `AddSeries` 메서드를 사용 하면 설정 된 `xValue` 및 `yValues` 매개 변수입니다. 예를 들어, 사용 하는 대신는 `DataBindTable` 다음과 같이 메서드:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    사용할 수는 `AddSeries` 다음과 같이 메서드:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    둘 다 동일한 결과 렌더링 합니다. 합니다 `AddSeries` 메서드는 차트 종류 및 데이터를 더 명시적으로 지정할 수 있으므로 보다 유연 하지만 `DataBindTable` 메서드는 유동적인 필요가 없는 경우 사용 하기가 더 쉽습니다.
5. 브라우저에서 페이지를 실행 합니다. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>XML 데이터를 사용 하 여

차트에 대 한 세 번째 옵션을 차트의 데이터와 XML 파일을 사용 하는 것입니다. 이렇게 하려면 XML 파일에도 스키마 파일이 있어야 (*.xsd* 파일)는 XML 구조에 설명 합니다. 이 절차에서는 XML 파일에서 데이터를 읽는 방법을 보여 줍니다.

1. 에 *앱\_데이터* 폴더를 이라는 새 XML 파일을 만듭니다 *data.xml*합니다.
2. 기존 XML은 가상의 회사에서 직원에 대 한 일부 XML 데이터는 다음을 바꿉니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. 에 *앱\_데이터* 폴더를 이라는 새 XML 파일을 만듭니다 *data.xsd*합니다. (확장이 이번 됩니다 *.xsd*.)
4. 다음의 기존 XML을 바꿉니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 웹 사이트의 루트에서 이라는 새 파일을 만듭니다 *ChartDataXML.cshtml*합니다.
6. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    코드는 먼저 만듭니다는 `DataSet` 개체입니다. 이 개체는 XML 파일에서 읽고 스키마 파일의 정보에 따라 구성 하는 데이터 관리에 사용 됩니다. (코드의 맨 위에 문을 포함 하는 알림 `using SystemData`합니다. 작업을 수행할 수 있도록 하려면이 작업이 필요 합니다 `DataSet` 개체입니다. 자세한 내용은 [ &quot;Using&quot; 문 및 정규화 된 이름](#SB_UsingStatements) 이 문서의 뒷부분에 나오는.)

    그런 다음 코드는 만듭니다는 `DataView` 데이터 집합을 기반으로 하는 개체입니다. 차트에 바인딩할 수 있는 개체를 제공 하는 데이터 뷰 &#8212; 즉, 읽기 및 출력 합니다. 차트를 사용 하 여 데이터를 바인딩할를 `AddSeries` 메서드를 때 앞서 보았던 배열 데이터는 제외 하 고이 시간을 차트로 만들 때를 `xValue` 및 `yValues` 매개 변수를 설정는 `DataView` 개체입니다.

    또한이 예제는 특정 차트 종류를 지정 하는 방법을 보여줍니다. 데이터에 추가 되는 경우는 `AddSeries` 메서드는 `chartType` 원형 차트를 표시 하려면 매개 변수 설정도 합니다.
7. 브라우저에서 페이지를 실행 합니다. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using" 문 및 정규화 된 이름
> 
> Razor 구문이 있는 ASP.NET 웹 페이지의 기반이 되는.NET Framework 구성 요소 (클래스)은 수천 이루어져 있습니다. 으로 구성 하는 이러한 모든 클래스를 사용 하 여 작업을 관리할 수 있도록, 하려면 *네임 스페이스*, 라이브러리 등 어느 정도 합니다. 예를 들어 합니다 `System.Web` 네임 스페이스에는 브라우저/서버 통신을 지 원하는 클래스가 포함 되어 있습니다. 합니다 `System.Xml` 네임 스페이스에는 XML 파일을 읽고 만드는 데 사용 되는 클래스가 포함 되어 있습니다. 및 `System.Data` 네임 스페이스에는 사용할 수 있도록 하는 클래스가 포함 되어 있습니다. 데이터입니다.
> 
> .NET Framework의 지정 된 모든 클래스에 액세스 하려면 코드 뿐 아니라 클래스 이름 뿐만 아니라 클래스에 있는 네임 스페이스를 알고 있어야 합니다. 예를 들어, 사용 하기 위해를 `Chart` 도우미 코드 찾아야 할 합니다 `System.Web.Helpers.Chart` 네임 스페이스를 결합 하는 클래스 (`System.Web.Helpers`) 클래스 이름으로 (`Chart`). 이 클래스의 이라고 *정규화* 이름 &#8212; 의.NET Framework는 (광활) 내에서 해당 완전 하 고 명확한 위치 합니다. 코드에서이 다음과 같습니다.
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 그러나 작업은 번거롭습니다와 오류가 발생 하기 쉽습니다 도우미 클래스를 참조할 때마다 이러한 긴, 정규화 된 이름을 사용 해야 합니다. 따라서 클래스 이름을 사용 하 여 좀 더 쉽게 할 수 있습니다 *가져올* 일반적으로 관심을 한 네임 스페이스는.NET Framework의 여러 네임 스페이스 중 소수의 합니다. 네임 스페이스를 가져온 경우에 클래스 이름만 사용할 수 있습니다 (`Chart`) 대신 정규화 된 이름 (`System.Web.Helpers.Chart`). 코드를 실행 하는 클래스 이름이 발견을 해당 클래스를 찾으려면 가져온 네임 스페이스에 것 보일 수 있습니다.
> 
> Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하 여 웹 페이지를 만들 때 일반적으로 사용 된 동일한 클래스 집합 매번 포함을 `WebPage` 클래스, 다양 한 도우미를 등에입니다. 웹 사이트를 만들 때마다 관련 네임 스페이스를 가져오는 작업을 저장 하려면 모든 웹 사이트에 대 한 핵심 네임 스페이스의 집합을 자동으로 가져옵니다 ASP.NET 구성 됩니다. 이유는 바로 지금;까지 가져오거나 네임 스페이스를 사용 하 여 처리 적이 있습니다 작업을 했었다면 모든 클래스를 이미 가져온 네임 스페이스에 있습니다.
> 
> 그러나 때로는 해야를 자동으로 가져온 네임 스페이스에 포함 되지 않은 클래스를 사용 하 여 작동 합니다. 이 경우 해당 클래스의 정규화 된 이름을 사용 하거나 또는 클래스를 포함 하는 네임 스페이스를 수동으로 가져올 수 있습니다. 사용할 네임 스페이스를 가져오려면 합니다 `using` 문 (`import` Visual basic에서) 이전 예제에서 볼 수 있듯이, 문서.
> 
> 예를 들어, 합니다 `DataSet` 클래스에는 `System.Data` 네임 스페이스입니다. `System.Data` 네임 스페이스는 ASP.NET Razor 페이지에 자동으로 사용할 수 없습니다. 따라서 사용 하는 `DataSet` 클래스의 정규화 된 이름을 사용 하 여, 다음과 같은 코드를 사용할 수 있습니다.
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 사용 해야 하는 경우는 `DataSet` 반복적으로 클래스 같이 네임 스페이스를 가져오고 다음 코드에서 클래스 이름을 사용 하 여:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 추가할 수 있습니다 `using` 참조 하려는 다른.NET Framework 네임 스페이스용 문입니다. 그러나 앞에서 설명한 것 처럼 않아도 이렇게 자주 사용 하는 클래스의 대부분에서 사용 하기 위해 ASP.NET에서 자동으로 가져온 네임 스페이스에 있기 때문에 *.cshtml* 하 고 *.vbhtml* 페이지입니다.


<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>웹 페이지 내에서 차트를 표시합니다.

예제에서 살펴본 지금 차트를 만들고 차트 그래픽으로 브라우저에 직접 렌더링 되는 다음입니다. 대부분의 경우에서 하지만 브라우저에서 자체적으로 뿐 아니라 차트 페이지의 일부로 표시 하려는 합니다. 작업을 수행 하는 2 단계 프로세스가 필요 합니다. 먼저 이미 살펴본 것 처럼 차트를 생성 하는 페이지를 만드는 것입니다.

두 번째 단계 결과 이미지는 다른 페이지에 표시 됩니다. HTML을 사용 하면 이미지를 표시 하려면 `<img>` 같은 요소인 모든 이미지를 표시 하는 방식으로 합니다. 그러나 참조 하는 대신를 *.jpg* 또는 *.png* 파일을 `<img>` 요소 참조를 *.cshtml* 포함 된 파일은 `Chart` 도우미는 차트를 만듭니다. 표시 페이지를 실행 하는 경우, `<img>` 요소의 출력을 가져옵니다는 `Chart` 도우미 하 고 차트를 렌더링 합니다.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. 이라는 파일을 만듭니다 *ShowChart.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    코드를 사용 하는 `<img>` 앞에서 만든 차트를 표시 하려면 요소를 *ChartArrayBasic.cshtml* 파일.
3. 브라우저에서 웹 페이지를 실행 합니다. 합니다 *ShowChart.cshtml* 파일에 포함 된 코드에 따라 차트 이미지를 표시 합니다 *ChartArrayBasic.cshtml* 파일입니다.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>차트의 스타일 지정

`Chart` 도우미 많은 차트의 모양을 사용자 지정할 수 있는 옵션을 지원 합니다. 색, 글꼴, 테두리 및 등을 설정할 수 있습니다. 차트의 모양을 사용자 지정 하는 쉬운 방법을 사용 하는 것을 *테마*합니다. 테마는 글꼴, 색, 레이블, 색상표, 테두리 및 효과 사용 하 여 차트를 렌더링 하는 방법을 지정 하는 정보를 수집 합니다. (참고 차트의 스타일 차트 종류를 나타내지 않습니다.)

다음 표에서 기본 테마를 나열합니다.

| 테마 | 설명 |
| --- | --- |
| `Vanilla` | 흰색 배경에 빨간색 열을 표시합니다. |
| `Blue` | 표시 파란색 파란색 배경에 그라데이션 효과의 열입니다. |
| `Green` | 표시 열에 녹색 그라데이션 배경이 파란색입니다. |
| `Yellow` | 노랑 그라데이션 배경에서 주황색 열을 표시합니다. |
| `Vanilla3D` | 흰색 배경 기반 3 차원 빨간색 열을 표시합니다. |

새 차트를 만들 때 사용 하 여 테마를 지정할 수 있습니다.

1. 라는 새 파일을 만듭니다 *ChartStyleGreen.cshtml*합니다.
2. 다음 페이지에서 기존 콘텐츠를 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    이 코드는 데이터에 대 한 데이터베이스를 사용 하지만 추가 하는 이전 예제와 동일 합니다 `theme` 매개 변수를 만들 때의 `Chart` 개체입니다. 변경된 된 코드는 다음과 같습니다.

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 브라우저에서 페이지를 실행 합니다. 이전에 동일한 데이터를 표시 하지만 표시는 차트 모양은 더 세련 된: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>차트 저장

사용 하는 경우는 `Chart` 때 도우미 살펴본이 문서에서는 도우미를 다시 생성부터 차트 될 때마다 호출 됩니다. 필요한 경우 차트에 대 한 코드 또한 다시 데이터베이스를 쿼리 또는 다시 데이터를 가져올 XML 파일을 읽습니다. 일부 경우에 이렇게 같은 될 수 있습니다 복잡 한 작업을 쿼리 하는 데이터베이스가 큰 경우 또는 XML 파일에는 많은 양의 데이터를 포함 하는 경우. 서버 리소스를 동적으로 이미지를 만드는 과정은 차트 많은 양의 데이터를 포함 하지 않습니다, 경우에 많은 사람들이 페이지 또는 차트를 표시 하는 페이지를 요청 하는 경우 있습니다 수 있으며 영향 웹 사이트의 성능에 합니다.

차트 만들기의 잠재적인 성능 영향을 줄일 수 있도록, 첫 번째 차트 번 만들 수 있습니다 필요 하 고 저장 합니다. 차트 다시 생성 하는 대신 다시 필요할 때만 저장 된 버전을 가져올 하는 렌더링 합니다.

이러한 방식으로 차트를 저장할 수 있습니다.

- (서버)에서 컴퓨터 메모리에 있는 차트를 캐시 합니다.
- 차트를 이미지 파일로 저장 합니다.
- 차트를 XML 파일로 저장 합니다. 이 옵션을 통해 차트를 저장 하기 전에 수정할 수 있습니다.

### <a name="caching-a-chart"></a>차트를 캐시합니다.

차트를 만든 후에이 캐시할 수 있습니다. 차트 캐싱 다시 표시 해야 하는 경우 다시 생성 되도록이 없는 것을 의미 합니다. 캐시에서 차트를 저장 하면 차트 고유 해야 하는 키를 제공 합니다.

서버 메모리가 부족 한 경우 캐시에 저장 하는 차트를 제거할 수 있습니다. 또한 어떤 이유로 든 응용 프로그램 다시 시작 하면 캐시가 지워집니다. 따라서 캐시 된 차트를 사용 하 여 작업 하는 표준 방법은 항상 캐시에 사용할 수 있는 인지 여부와 그렇지 않은 경우 먼저를 확인 하려면 다음 만들거나 다시 만들어야 하는 합니다.

1. 웹 사이트의 루트로 라는 파일을 만듭니다 *ShowCachedChart.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>` 태그를 포함를 `src` 가리키는 특성을 *ChartSaveToCache.cshtml* 파일을 쿼리 문자열로 페이지에는 키를 전달 합니다. 키 값을 포함 &quot;myChartKey&quot;합니다. *ChartSaveToCache.cshtml* 파일에는 `Chart` 차트를 만드는 도우미입니다. 잠시 후에이 페이지를 만듭니다.

    페이지의 끝은 라는 페이지에 대 한 링크 *ClearCache.cshtml*합니다. 또한 만듭니다 곧 하는 페이지입니다. 해야 합니다 *ClearCache.cshtml* 이 예제에 대 한 캐싱 테스트할 때만-링크 또는 캐시 된 차트를 작업할 때 일반적으로 포함 된 페이지 아닙니다.
3. 웹 사이트의 루트에서 이라는 새 파일을 만듭니다 *ChartSaveToCache.cshtml*합니다.
4. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    코드는 먼저 쿼리 문자열에서 키 값으로 전달 된 아무 것도 있는지 여부를 확인 합니다. 따라서 코드에서 호출 하 여 캐시에서 차트를 읽을 하려고 하는 경우는 `GetFromCache` 메서드 및 키를 전달 합니다. 사실은 해당 키 (처음 차트 요청 되는 상황이)에서 캐시에 아무것도 없는 경우 코드는 일반적으로 차트를 만듭니다. 차트 완료 되 면 코드에 저장 캐시를 호출 하 여 `SaveToCache`입니다. 해당 메서드는 키 (따라서 차트 나중에 요청 수) 및 차트를 캐시에 저장 해야 하는 시간에 필요 합니다. (차트를 캐시 하는 정확한 시간을 나타내는 데이터 변경 될 수 있습니다 생각 빈도 따라 다릅니다.) `SaveToCache` 방법을 사용 하려면를 `slidingExpiration` 매개 변수 &#8212; 설정 된 경우 true 이면 제한 시간 카운터 차트에 액세스할 때마다 재설정 됩니다. 이 경우 적용 의미를 차트의 캐시 항목 만료 2 분 후에 마지막 사람이 차트에 액세스 합니다. (대신 슬라이딩 만료는 절대 만료를 캐시 엔트리에 액세스 된 있었습니다 빈도 관계 없이 캐시에 배치 된 후 2 분 정확 하 게 만료 되는 의미입니다.)

    마지막으로 코드를 사용 합니다 `WriteFromCache` 인출 하 고 캐시에서 차트를 렌더링 하는 메서드. 이 메서드는 외부는 `if` 블록 캐시에서 차트는 차트에 있었던 또는 생성 하 고 캐시에 저장 해야 하는지 여부를 가져오게 됩니다 때문에 캐시를 확인 합니다.

    예제에서는 다음에 유의 합니다 `AddTitle` 타임 스탬프를 포함 하는 메서드. (현재 날짜 및 시간 추가 &#8212; `DateTime.Now` &#8212; 제목입니다.)
5. 라는 새 페이지를 만듭니다 *ClearCache.cshtml* 내용을 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    이 페이지를 사용 합니다 `WebCache` 에 캐시 된 차트를 제거 하려면 도우미 *ChartSaveToCache.cshtml*합니다. 앞에서 설명한 대로 다음과 같은 페이지가 필요가 일반적으로 합니다. 만들 여기 쉽게 캐싱을 테스트에 합니다.
6. 실행 합니다 *ShowCachedChart.cshtml* 브라우저에서 웹 페이지입니다. 페이지에 포함 된 코드에 따라 차트 이미지를 표시 합니다 *ChartSaveToCache.cshtml* 파일입니다. 주의 타임 스탬프 라고 차트 제목에 표시 합니다. 

    ![차트 제목에 타임 스탬프를 사용 하 여 기본 차트 그림 설명:](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 브라우저를 닫습니다.
8. 실행 합니다 *ShowCachedChart.cshtml* 다시 합니다. 타임 스탬프는 동일 이전과 나타내지만 차트 다시 생성 하지 못했습니다 대신 캐시에서 읽은 알 수 있습니다.
9. *ShowCachedChart.cshtml*를 클릭 합니다 **캐시 지우기** 링크 합니다. 로 이동 *ClearCache.cshtml*, 캐시를 지웠습니다 있는지 보고 합니다.
10. 클릭 합니다 **ShowCachedChart.cshtml 돌아갑니다** 링크를 다시 실행 하거나 *ShowCachedChart.cshtml* WebMatrix에서. 이 이번 타임 스탬프가 변경 되었는지 확인, 하므로 캐시를 지웠습니다. 따라서 코드 차트를 다시 생성 하 고 캐시에 다시 배치 해야 합니다.

### <a name="saving-a-chart-as-an-image-file"></a>차트를 이미지 파일로 저장

차트를 이미지 파일로 저장할 수도 있습니다 (예는 *.jpg* 파일) 서버. 이미지 파일을 이미지 하는 방식으로 사용할 수 있습니다. 장점은 파일을 임시 캐시에 저장 되지 않고 저장 됩니다. (예: 매시간) 서로 다른 시간에 새 차트 이미지를 저장 하 고 변경 내용 시간이 지남에 따라 발생 하는의 영구 기록이 유지 수 있습니다. 웹 응용 프로그램에 이미지 파일을 저장 하려는 서버의 폴더로 파일을 저장할 수 있는 권한이 있는지 확인 해야 하는 참고 합니다.

1. 웹 사이트의 루트로 라는 폴더를 만듭니다  *\_ChartFiles* 아직 존재 하지 않는 경우.
2. 웹 사이트의 루트에서 이라는 새 파일을 만듭니다 *ChartSave.cshtml*합니다.
3. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    코드를 먼저 확인 여부를 합니다 *.jpg* 파일이 호출 하 여는 `File.Exists` 메서드. 코드에서는 새 파일이 없으면 `Chart` 배열에서입니다. 이 이번에는 호출을 `Save` 메서드와 전달은 `path` 을 여 차트를 저장할 파일 이름과 파일 경로 지정 하려면 매개 변수입니다. 페이지의 본문에는 `<img>` 요소를 가리키는 경로 사용 합니다 *.jpg* 표시할 파일입니다.
4. 실행 합니다 *ChartSave.cshtml* 파일입니다.
5. WebMatrix를 반환 합니다. 이미지 파일 이라는 통지 *chart01.jpg* 에 저장 됩니다 합니다  *\_ChartFiles* 폴더.

### <a name="saving-a-chart-as-an-xml-file"></a>차트를 XML 파일로 저장

마지막으로 차트는 서버에서 XML 파일로 저장할 수 있습니다. 차트를 캐시 하거나 파일로 저장 하는 차트를 통해이 메서드를 사용 하는 장점은 하려는 경우 차트를 표시 하기 전에 XML을 수정할 수 있습니다. 응용 프로그램에 이미지 파일을 저장 하려는 폴더를 서버에 대 한 읽기/쓰기 권한이 있어야 합니다.

1. 웹 사이트의 루트에서 이라는 새 파일을 만듭니다 *ChartSaveXml.cshtml*합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    이 코드는 앞서 살펴본 캐시에서 차트를 저장 하는 것에 대 한 XML 파일을 사용 하는 코드와 비슷합니다. 코드는 먼저 XML 파일을 호출 하 여 있는지 여부를 확인 합니다 `File.Exists` 메서드. 코드에서는 새 파일이 없으면 `Chart` 개체와 파일 이름을 전달 하 여 `themePath` 매개 변수입니다. 이 XML 파일에 따라 차트를 만듭니다. XML 파일 존재 하지 않는 경우 코드는 일반적인 차트를 만들고 호출 `SaveXml` 저장 합니다. 차트를 사용 하 여 렌더링 되는 `Write` 메서드인 것이 현상을 본 적입니다.

    캐싱 보여주는 페이지와 마찬가지로이 코드는 차트 제목에 타임 스탬프를 포함 합니다.
3. 라는 새 페이지를 만듭니다 *ChartDisplayXMLChart.cshtml* 다음 태그를 추가 합니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. 실행 합니다 *ChartDisplayXMLChart.cshtml* 페이지입니다. 차트 표시 됩니다. 타임 스탬프에서에서 주목 차트의 제목입니다.
5. 브라우저를 닫습니다.
6. WebMatrix에서 마우스 오른쪽 단추로 클릭 합니다  *\_ChartFiles* 폴더를 클릭 **새로 고침**, 한 다음 폴더를 엽니다. 합니다 *XMLChart.xml* 여이 폴더에 파일을 만들지는 `Chart` 도우미입니다. 

    ![설명: _ChartFiles 폴더 차트 도우미가 만든 XMLChart.xml 파일을 표시 합니다.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. 실행 합니다 *ChartDisplayXMLChart.cshtml* 페이지를 다시 합니다. 차트에는 페이지를 실행 하 고 첫 번째 시간으로 동일한 타임 스탬프를 보여 줍니다. 이전에 저장 하는 XML에서 차트를 생성할 때문입니다.
8. WebMatrix에서 엽니다는  *\_ChartFiles* 폴더와 삭제는 *XMLChart.xml* 파일입니다.
9. 실행 합니다 *ChartDisplayXMLChart.cshtml* 번 페이지입니다. 이 이번에 타임 스탬프가 업데이트 때문에 `Chart` 도우미 XML 파일을 다시 해야 합니다. 확인 합니다  *\_ChartFiles* 폴더 및 XML 파일은 다시 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [Asp.net에서 데이터베이스를 사용 하 여 작업 소개 사이트 페이지](https://go.microsoft.com/fwlink/?LinkId=202893)
- [성능 향상을 위해 사이트 페이지 Asp.net에서 캐싱 사용](https://go.microsoft.com/fwlink/?LinkId=202903)
- [차트 클래스](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (MSDN에서 ASP.NET Web Pages API 참조)
