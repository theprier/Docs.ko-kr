---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
title: 데이터 웹에 이진 데이터 표시 (VB)를 제어 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 이진 데이터를 이미지 파일의 표시 및 f '다운로드' 링크의 프로 비전을 비롯 한 웹 페이지를 표시 하는 옵션에 살펴보겠습니다...
ms.author: aspnetcontent
ms.date: 03/27/2007
ms.assetid: 9201656a-e1c2-4020-824b-18fb632d2925
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: fe6a16a3ee601eb58ae9d51b599684b47392eba2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810296"
---
<a name="displaying-binary-data-in-the-data-web-controls-vb"></a>데이터 웹 컨트롤 (VB)에서 이진 데이터 표시
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_VB.exe) 또는 [PDF 다운로드](displaying-binary-data-in-the-data-web-controls-vb/_static/datatutorial55vb1.pdf)

> 이 자습서에서는 이진 데이터를 이미지 파일의 표시 및 PDF 파일에 대 한 '다운로드' 링크의 프로 비전을 포함 하 여 웹 페이지를 표시 하는 옵션에 살펴봅니다.


## <a name="introduction"></a>소개

이전 자습서에서 응용 프로그램 s 기본 데이터 모델을 사용 하 여 이진 데이터를 연결 하기 위한 두 가지 기술을 탐색 하 고 브라우저에서 웹 서버의 파일 시스템에 파일을 업로드 하려면 FileUpload 컨트롤을 사용 합니다. 에서는 데이터 모델을 사용 하 여 업로드 된 이진 데이터를 연결 하는 방법을 참조 하는 준비 합니다. 즉, 파일 업로드 및 파일 시스템에 저장 된 후에 파일 경로 적절 한 데이터베이스 레코드에 저장 되어야 합니다. 데이터가 데이터베이스에 직접 저장 되는, 업로드 된 이진 데이터를 파일 시스템에 저장할 수 없는 필요 하지만 데이터베이스에 삽입 해야 합니다.

그러나 데이터 모델을 사용 하 여 데이터 연결을 살펴보기 전에 최종 사용자에 게는 이진 데이터를 제공 하는 방법을 소개 하는 s 수 있습니다. 텍스트 데이터를 제공 하는 것은 충분 한 간단 하지만 이진 데이터 표시 하는 방법을? 종속, 물론 이진 데이터의 형식입니다. 이미지에 대 한 가능성이 하려는 이미지를 표시 합니다. Pdf, Microsoft Word 문서, ZIP 파일 및 다른 유형의 이진 데이터를 다운로드 링크를 제공 하는 것이 좋습니다.

데이터를 사용 하 여 해당 연결 된 텍스트 데이터와 함께 이진 데이터를 표시 하는 방법을 살펴보겠습니다이 자습서에서는 웹 GridView 및 DetailsView와 같은 제어 합니다. 다음 자습서에서는 데이터베이스를 사용 하 여 업로드 된 파일 연결에 대해 살펴보겠습니다.

## <a name="step-1-providingbrochurepathvalues"></a>1 단계: 제공`BrochurePath`값

합니다 `Picture` 열에는 `Categories` 테이블은 이미 다양 한 범주 이미지에 대 한 이진 데이터를 포함 합니다. 구체적으로 `Picture` 매끄럽지, 품질이 낮거나, 16 색 비트맵 이미지의 이진 콘텐츠를 보유 하는 각 레코드에 대 한 열입니다. 각 범주 이미지 172 픽셀 너비 120 픽셀 너비 이며 약 11 (kb)를 사용 합니다. 새로운 자세한의 이진 콘텐츠를 `Picture` 78 바이트를 포함 하는 열 [OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding) 이미지를 표시 하기 전에 제거 해야 하는 헤더입니다. 이 헤더 정보는 Microsoft Access Northwind 데이터베이스에 기반을 두고 있으므로 존재 합니다. Access에서 이진 데이터는 tacks이 헤더에는 OLE 개체 데이터 형식을 사용 하 여 저장 됩니다. 이제 그림을 표시 하기 위해 이러한 고품질 이미지의 헤더를 제거 하는 방법에 살펴보겠습니다. S 범주를 업데이트 하기 위한 인터페이스는 이후 자습서에서 빌드할 `Picture` 열 불필요 한 OLE 머리글 없이 해당 JPG 이미지를 사용 하 여 OLE 머리글을 사용 하는 이러한 비트맵 이미지를 바꿉니다.

이전 자습서에서 FileUpload 컨트롤을 사용 하는 방법에 살펴보았습니다. 따라서 진행 수 및 브로슈어 파일을 웹 서버 파일 시스템을 추가 합니다. 하지만이 작업을 수행 업데이트 하지 않습니다 합니다 `BrochurePath` 열에는 `Categories` 테이블입니다. 다음 자습서에서이 수행 하는 방법을 알아봅니다 되지만 지금은 직접이 열에 대 한 값을 제공 해야 합니다.

이 자습서가의 다운로드 7 PDF 브로슈어 파일에서 찾을 수 있습니다는 `~/Brochures` 폴더, Seafood 제외 하 고 범주를 각각에 대 한 합니다. 필자는 의도적으로 Seafood 브로슈어 모든 레코드는 관련 이진 데이터가 시나리오를 처리 하는 방법을 설명 하기 위해 추가 생략 합니다. 업데이트 하는 `Categories` 이러한 값을 사용 하 여 테이블을 마우스 오른쪽 단추로 클릭는 `Categories` 서버 탐색기에서 노드 테이블 데이터 표시를 선택 합니다. 그런 다음 브로슈어 파일 그림 1 에서처럼 브로슈어에 있는 각 범주에 대 한 가상 경로 입력 합니다. Seafood 범주에 대 한 없습니다 브로슈어 이므로 그대로 해당 `BrochurePath` s 열 값으로 `NULL`입니다.


[![범주 테이블의 BrochurePath 열에 대 한 값을 수동으로 입력](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.png)

**그림 1**: 수동으로 값을 입력 합니다 `Categories` 테이블 s `BrochurePath` 열 ([클릭 하 여 큰 이미지 보기](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.png))


## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>GridView의 브로슈어에 대 한 다운로드 링크를 제공 하는 2 단계:

사용 하 여는 `BrochurePath` 제공 된 값을 `Categories` 범주의 브로슈어 다운로드에 대 한 링크와 함께 각 범주를 나열 하는 GridView를 만들려면 준비가에서는 테이블입니다. 4 단계에서에서이 GridView 범주의 이미지도 표시할 확장할 예정입니다.

디자이너 도구 상자에서 GridView 드래그 하 여 시작 합니다 `DisplayOrDownloadData.aspx` 페이지에 `BinaryData` 폴더. 집합 GridView s `ID` 에 `Categories` GridView가 스마트 태그를 통해 새 데이터 원본에 연결 하려면 선택 합니다. 특히, 명명 된 ObjectDataSource에 바인딩할 `CategoriesDataSource` 사용 하 여 데이터를 검색 하는 `CategoriesBLL` s 개체 `GetCategories()` 메서드.


[![범주 및 공급 업체 Dropdownlist 포함 (None) 옵션](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.png)

**그림 2**: 명명 된 새 ObjectDataSource 만들려면 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.png))


[![CategoriesBLL 클래스를 사용 하는 ObjectDataSource 구성](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.png)

**그림 3**: ObjectDataSource 사용 하도록 구성 된 `CategoriesBLL` 클래스 ([클릭 하 여 큰 이미지 보기](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.png))


[![GetCategories() 메서드를 사용 하는 범주의 목록을 검색 합니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.png)

**그림 4**:의 범주 하 여 목록 검색을 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 자동으로 추가 하려면 BoundField 합니다 `Categories` GridView에 대 한는 `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`, 및 `BrochurePath` `DataColumn` s입니다. 계속 해 서 제거 합니다 `NumberOfProducts` BoundField 이후에 `GetCategories()` 메서드의 쿼리는이 정보를 검색 하지 않습니다. 제거는 `CategoryID` BoundField 및 이름 바꾸기는 `CategoryName` 및 `BrochurePath` BoundFields `HeaderText` 속성 범주 및 브로슈어, 각각. 다음과 같이 변경한 후 GridView 및 ObjectDataSource가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample1.aspx)]

브라우저를 통해이 페이지 (그림 5 참조). 8 개 범주의 나열 됩니다. 7 범주별으로 `BrochurePath` 값을 `BrochurePath` 해당 BoundField에 표시 되는 값입니다. Seafood 있는 `NULL` 값에 대 한 해당 `BrochurePath`, 빈 셀을 표시 합니다.


[![각 범주가의 이름, 설명 및 BrochurePath 값 목록](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.png)

**그림 5**: 각 범주의 이름, 설명 및 `BrochurePath` 값이 나열 됩니다 ([클릭 하 여 큰 이미지 보기](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.png))


텍스트를 표시 하지 않고는 `BrochurePath` 브로슈어에 대 한 링크를 만들려면 원하는 열입니다. 이렇게 하려면 제거를 `BrochurePath` BoundField HyperLinkField을으로 바꿉니다. 새 HyperLinkField s 설정 `HeaderText` 속성을 브로슈어, 해당 `Text` 보기 브로슈어 속성 및 해당 `DataNavigateUrlFields` 속성을 `BrochurePath`.


![HyperLinkField BrochurePath에 대 한 추가](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.gif)

**그림 6**:에 대 한 HyperLinkField 추가 `BrochurePath`


이렇게 그림 7 있듯이 GridView를 링크 열을 추가 됩니다. 보기 브로슈어 링크를 클릭 하 PDF 브라우저에서 직접 표시 하거나 사용자를 PDF reader가 설치 되었는지 여부에 따라 파일을 다운로드 및 s 브라우저 설정을 확인 합니다.


[![범주의 브로슈어 보기 브로슈어 링크를 클릭 하 여 볼 수 있습니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.png)

**그림 7**: 뷰 브로슈어 링크를 클릭 하는 범주의 브로슈어를 볼 수 있습니다 ([큰 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.png))


[![S 브로슈어 PDF의 범주 표시](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.png)

**그림 8**: The 범주의 브로슈어 PDF가 표시 됩니다 ([큰 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image14.png))


## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>브로슈어 없이 범주에 대 한 뷰 브로슈어 텍스트 숨기기

그림 7에서 알 수 있듯이, 합니다 `BrochurePath` HyperLinkField 표시 해당 `Text` 여부에 관계 없이 모든 레코드에 대 한 속성 값 (보기 브로슈어) 여기가 아닌`NULL` 에 대 한 값 `BrochurePath`합니다. 물론, 경우 `BrochurePath` 는 `NULL`, 링크 텍스트에 표시 됩니다 Seafood 범주가 포함 된 경우 (그림 7로 다시 참조). 보기 브로슈어 텍스트를 표시 하는 대신 것 없이 이러한 범주를 보유 하는 `BrochurePath` 값 브로슈어에 사용할 수 없는 같은 대체 텍스트를 표시 합니다.

이 동작을 제공 하기 위해를 TemplateField 내용이 기반으로 적절 한 출력을 생성 하는 페이지 메서드 호출을 통해 생성 되는 데 필요 합니다 `BrochurePath` 값입니다. 먼저 살펴보았습니다이 기법을 서식 지정에 [GridView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 자습서입니다.

선택 하 여는 HyperLinkField를 TemplateField로 설정 합니다 `BrochurePath` HyperLinkField 및 클릭 한 다음 변환에서이 필드를 TemplateField로 열 편집 대화 상자에서 연결 합니다.


![HyperLinkField templatefield로 변환](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.gif)

**그림 9**:는 HyperLinkField templatefield로 변환


이 사용 하 여 templatefield로 만들어집니다.는 `ItemTemplate` 하이퍼링크 웹을 포함 하는 컨트롤 `NavigateUrl` 속성이 바인딩되는 `BrochurePath` 값입니다. 이 태그는 메서드를 호출 하 여 바꿉니다 `GenerateBrochureLink`값의 전달 `BrochurePath`:


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample2.aspx)]

다음으로 만듭니다는 `Protected` 메서드는 ASP.NET에서 페이지 라는 s 코드 숨김 클래스 `GenerateBrochureLink` 를 반환 하는 `String` 받고는 `Object` 입력된 매개 변수로 합니다.


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample3.vb)]

이 방법을 결정 하는 경우에 전달 `Object` 값은 데이터베이스 `NULL` 고 그렇다면 범주 브로슈어 부족을 나타내는 메시지가 반환 합니다. 없는 경우에 그렇지는 `BrochurePath` 값을 해당 하이퍼링크에 표시 되 합니다. 경우는 `BrochurePath` 값은 s에 전달 된 표시 합니다 [ `ResolveUrl(url)` 메서드](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)합니다. 이 메서드는 전달 된-에서 확인 *url*, 대체 된 `~` 적절 한 가상 경로 사용 하 여 문자입니다. 예를 들어 응용 프로그램에서 루 팅 `/Tutorial55`, `ResolveUrl("~/Brochures/Meats.pdf")` 돌아갑니다 `/Tutorial55/Brochures/Meat.pdf`합니다.

그림 10 이러한 변경 내용을 적용 한 후 페이지를 보여 줍니다. Seafood 범주의 `BrochurePath` 필드에는 이제 브로슈어에 사용할 수 없는 텍스트가 표시 됩니다.


[![이러한 범주 없이 브로슈어에 대 한 텍스트 없음 브로슈어 사용 가능한 표시 됩니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image15.png)

**그림 10**: 이러한 범주 없이 브로슈어에 대해 표시 되는 텍스트 없음 브로슈어 사용할 수 있습니다 ([큰 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image16.png))


## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>3 단계: 범주의 그림을 표시 하는 웹 페이지 추가

사용자는 ASP.NET 페이지를 방문 하면 ASP.NET 페이지의 HTML 받습니다. 받은 HTML은 단순히 텍스트 및 이진 데이터가 포함 되지 않습니다. 이미지, 사운드 파일, Macromedia Flash 응용 프로그램, 포함 된 Windows Media Player 비디오 등을 같은 추가 이진 데이터, 웹 서버에 별도 리소스로 존재 합니다. HTML이이 파일에 대 한 참조를 포함 하지만 파일의 실제 내용이 포함 되지 않습니다.

HTML에서 예를 들어, 합니다 `<img>` 요소는 그림을 사용 하 여 참조를 사용 하는 `src` 같이 이미지 파일을 가리키는 특성:


[!code-html[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample4.html)]

브라우저에서이 HTML을 받으면 다른 요청을 다음 브라우저에 표시 하는 이미지 파일의 이진 콘텐츠를 검색 하는 웹 서버에 만듭니다. 모든 이진 데이터에 동일한 개념이 적용 됩니다. 2 단계에서에서 브로슈어 페이지의 HTML 태그의 일부로 브라우저에 전송 되지 않았습니다. 대신 렌더링된 된 HTML 제공 하이퍼링크를 클릭 하면 브라우저를 PDF 문서를 직접 요청을 발생 합니다.

를 표시 하거나 사용자가 데이터베이스 내에 상주 하는 이진 데이터를 다운로드 하도록 허용 하려면 데이터를 반환 하는 별도 웹 페이지를 생성 해야 합니다. 응용 프로그램에서 s 여기 이진 데이터 필드가 하나만 데이터베이스 범주의 그림에 직접 저장 합니다. 페이지를 해야 하므로, 호출 된 경우 특정 범주에 대 한 이미지 데이터를 반환 합니다.

새 ASP.NET 페이지를 추가 합니다 `BinaryData` 라는 폴더 `DisplayCategoryPicture.aspx`합니다. 이 작업을 수행 하는 경우 마스터 페이지 선택 확인란을 선택 하지 않은 상태로 유지 합니다. 이 페이지에서는 `CategoryID` querystring과 해당 범주의 s의 이진 데이터를 반환 값 `Picture` 열입니다. 이 페이지에서 아무 및 이진 데이터를 반환 하므로 HTML 섹션의 모든 태그는 필요 하지 않습니다. 따라서 왼쪽된 아래 모서리에서 원본 탭을 클릭 하 고 제외 하 고 페이지의 태그를 모두 제거 된 `<%@ Page %>` 지시문입니다. 즉, `DisplayCategoryPicture.aspx` s 선언적 태그는 한 줄 구성 되어야 합니다.


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample5.aspx)]

표시 되 면 합니다 `MasterPageFile` 특성을 `<%@ Page %>` 지시문을 제거 합니다.

S 페이지 코드 숨김 클래스에 다음 코드를 추가 합니다 `Page_Load` 이벤트 처리기:


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample6.vb)]

이 코드에서 읽기를 시작 합니다 `CategoryID` 라는 변수로 querystring 값 `categoryID`. 호출을 통해 사진 데이터를 검색 하는 다음에 `CategoriesBLL` s 클래스 `GetCategoryWithBinaryDataByCategoryID(categoryID)` 메서드. 이 데이터를 사용 하 여 클라이언트에 반환 되는 `Response.BinaryWrite(data)` 메서드를 전에이 메서드가 호출 되는 `Picture` 열 값의 OLE 머리글을 제거 해야 합니다. 만들어 이렇게를 `Byte` 라는 배열을 `strippedImageData` 78 정확 하 게 보유할는에 포함 된 내용 보다 작은 문자는 `Picture` 열입니다. 합니다 [ `Array.Copy` 메서드](https://msdn.microsoft.com/library/z50k9bft.aspx) 에서 데이터를 복사 하는 데 사용 됩니다 `category.Picture` 78 위치를 다시 시작 `strippedImageData`합니다.

`Response.ContentType` 속성을 지정 합니다 [MIME 형식을](http://en.wikipedia.org/wiki/MIME) 브라우저에 렌더링 하는 방법을 알 수 있도록 반환 되는 콘텐츠. 이후 합니다 `Categories` s 테이블 `Picture` 열 비트맵 이미지를 MIME 형식을 비트맵을 사용 여기 (이미지/bmp). MIME 형식을 생략 하면 대부분의 브라우저는 여전히 이미지 올바르게 표시할 이미지 파일 s 이진 데이터의 내용에 따라 형식을 유추할 수 있습니다. 그러나 해당 s MIME을 포함 하는 것이 좋습니다 가능한 경우을 입력 합니다. 참조 된 [Internet Assigned Numbers Authority 웹 사이트](http://www.iana.org/) 의 전체 목록은 [MIME 미디어 유형](http://www.iana.org/assignments/media-types/)합니다.

만든이 페이지를 사용 하 여 특정 범주의 그림 방문 하 여 볼 수 있습니다 `DisplayCategoryPicture.aspx?CategoryID=categoryID`합니다. 그림 11은 음료 범주의 그림에서 볼 수 있는 `DisplayCategoryPicture.aspx?CategoryID=1`합니다.


[![그림이 표시 됩니다 음료 범주 s](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image17.png)

**그림 11**: The 음료 범주의 그림이 표시 됩니다 ([큰 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image18.png))


경우에 방문할 때 `DisplayCategoryPicture.aspx?CategoryID=categoryID`'System.Byte ' 형식으로 ' System.DBNull' 종류의 개체를 캐스팅할 수 없습니다 읽는 예외가 발생 하면,이 일으킬 수 있는 두 가지 있습니다. 먼저 합니다 `Categories` 테이블 s `Picture` 열에서 허용 `NULL` 값입니다. 그러나 `DisplayCategoryPicture.aspx` 페이지에서 아닌 것으로 가정`NULL` 현재 값입니다. `Picture` 의 속성을 `CategoriesDataTable` 있을 경우 직접 액세스할 수 없습니다를 `NULL` 값입니다. 허용 하려는 경우 `NULL` 에 대 한 값을 `Picture` 열 d 포함 하려면 다음 조건:


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample7.vb)]

위의 코드에서는 일부 라는 파일을 이미지 된다는 s `NoPictureAvailable.gif` 에 `Images` 그림 없이 해당 범주의 표시 하려는 폴더입니다.

경우에이 예외를 발생 수를 `CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` 메서드의 `SELECT` 문이 임시 SQL 문을 사용 하 고 있습니다 ve TableAdapter s에 대 한 마법사를 다시 실행 하는 경우 발생할 수 있는 기본 쿼리의 열 목록으로 돌아갔습니다. 주 쿼리입니다. 확인 되도록 `GetCategoryWithBinaryDataByCategoryID` 메서드 s `SELECT` 문을 계속 포함 됩니다는 `Picture` 열입니다.

> [!NOTE]
> 때마다는 `DisplayCategoryPicture.aspx` 가 방문 하면 데이터베이스를 액세스 하 고 지정 된 범주의 그림 데이터가 반환 됩니다. 를 사용자가 마지막으로 본 후 범주의 그림 영업일 기준 t 변경 하지만 이것이 불필요 한 노동력 낭비입니다. 에 대 한 HTTP를 사용 하면 다행히 *조건부 가져옵니다*합니다. 조건부 GET을 사용 하 여 HTTP 요청을 하는 클라이언트를 따라 보냅니다는 [ `If-Modified-Since` HTTP 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) 클라이언트가 웹 서버에서이 리소스를 마지막으로 검색 시간과 날짜를 제공 하는 합니다. 웹 서버를 사용 하 여 응답할 수 있습니다이 날짜를 지정 하는 이후 콘텐츠가 변경 되지 않은 경우는 [수정 되지 않음 상태 코드 (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 요청 된 리소스의 콘텐츠를 다시 보내면 포기 하 고 있습니다. 즉,이 기술을 사용 클라이언트에서 마지막으로 액세스 하므로 수정 되지 않은 경우에 다시 리소스에 대 한 콘텐츠를 보낼 수 없도록 웹 서버를 필요가 없습니다.


그러나이 동작을 구현 하 추가 해야를 `PictureLastModified` 열을를 `Categories` 캡처할 때 테이블을 `Picture` 열을 확인 하기 위한 코드 뿐만 아니라 마지막으로 업데이트를 `If-Modified-Since` 헤더입니다. 대 한 자세한 내용은 합니다 `If-Modified-Since` 헤더 및 조건부 GET 워크플로 참조 하세요 [RSS 해커에 대 한 HTTP 조건부 GET](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) 및 [는 자세히 살펴보고 ASP.NET 페이지에서 HTTP 요청을 수행](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx)합니다.

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>4 단계: GridView를 범주 사진 표시

사용 하 여 표시할 수 있는 특정 범주의 그림을 표시 하는 웹 페이지 만들었으므로 합니다 [이미지 웹 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx) 또는 HTML `<img>` 요소를 가리키는 `DisplayCategoryPicture.aspx?CategoryID=categoryID`합니다. GridView에는 이미지 필드를 사용 하 여 DetailsView URL 데이터베이스 데이터에 의해 결정 됩니다 이미지를 표시할 수 있습니다. 이미지 필드를 포함 `DataImageUrlField` 하 고 `DataImageUrlFormatString` HyperLinkField s 처럼 작동 하는 속성 `DataNavigateUrlFields` 고 `DataNavigateUrlFormatString` 속성입니다.

S 보강할 수 있도록 합니다 `Categories` GridView에서 `DisplayOrDownloadData.aspx` 각 범주의 그림 표시로 이미지 필드를 추가 하 여 합니다. 단순히는 이미지 필드를 추가 하 고 설정 해당 `DataImageUrlField` 하 고 `DataImageUrlFormatString` 속성을 `CategoryID` 및 `DisplayCategoryPicture.aspx?CategoryID={0}`, 각각. 이 렌더링 하는 GridView 열을 만듭니다는 `<img>` 요소입니다 `src` 참조 특성 `DisplayCategoryPicture.aspx?CategoryID={0}`여기서 {0} GridView 행 s 바뀝니다 `CategoryID` 값입니다.


![GridView에는 이미지 필드를 추가 합니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.gif)

**그림 12**: GridView에는 이미지 필드를 추가 합니다.


Soothe 같습니다 GridView가 선언적 구문에는 이미지 필드를 추가한 후 다음:


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample8.aspx)]

브라우저를 통해이 페이지를 보려면 잠시 시간이 소요 됩니다. 이제 각 레코드 범주에 대 한 그림을 포함 하는 방법을 note 합니다.


[![각 행에 대 한 s 그림의 범주 표시](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image19.png)

**그림 13**: 각 행에 대 한 그림 표시 되는 범주 s ([큰 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image20.png))


## <a name="summary"></a>요약

이 자습서에서는 이진 데이터를 표시 하는 방법을 살펴보았습니다. 데이터 표시 방법을 데이터의 유형에 따라 달라 집니다. PDF 브로슈어 파일에 대 한 혜택을 제공 해 사용자 보기 브로슈어 링크를 클릭 하면 PDF 파일에 직접 사용자를 수행 합니다. 범주 s 그림 만든 다음 페이지를 검색 하 여 데이터베이스에서 이진 데이터를 반환 하 고 GridView에서 각 범주의 그림을 표시 하려면 해당 페이지를 사용 합니다.

이제는 우리 ve 삽입, 업데이트 및 이진 데이터를 사용 하 여 데이터베이스에 대 한 삭제를 수행 하는 방법을 검사할 준비가에서는 이진 데이터를 표시 하는 방법을 살펴보았습니다. 다음 자습서는 해당 데이터베이스 레코드를 사용 하 여 업로드 된 파일을 연결 하는 방법을 살펴보겠습니다. 그런 다음 자습서에서는 연결 된 해당 레코드가 제거 되 면 이진 데이터를 삭제 하는 방법 뿐만 아니라 기존 이진 데이터를 업데이트 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Teresa Murphy 및 Dave Gardner 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](uploading-files-vb.md)
> [다음](including-a-file-upload-option-when-adding-a-new-record-vb.md)
