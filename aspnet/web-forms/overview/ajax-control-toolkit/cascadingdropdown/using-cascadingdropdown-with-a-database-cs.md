---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: CascadingDropDown을 사용 하 여 데이터베이스 (C#) | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: ed5057ee942ce57503b038cbd856fefaa3d287ce
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836060"
---
<a name="using-cascadingdropdown-with-a-database-c"></a>CascadingDropDown을 사용 하 여 데이터베이스 (C#)
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. 이 작업을 위해 특수 한 웹 서비스를 만들어야 합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 이 작업을 위해 특수 한 웹 서비스를 만들어야 합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). 데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.

이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내 합니다 &lt; `form` &gt; 요소):

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

다음 단계에서는 두 DropDownList 컨트롤은 필수입니다. 이 샘플에서 AdventureWorks에서 공급 업체 및 연락처 정보를 사용 하 여, 따라서 사용 가능한 공급 업체 및 사용 가능한 연락처에 대 한 하나의 목록을 만들겠습니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

그런 다음 두 CascadingDropDown extender는 페이지에 추가 되어야 합니다. 첫 번째 (공급 업체) 목록에서 하나 채우고 다른 두 번째 (연락처) 목록을 채웁니다. 다음 특성을 설정 해야 합니다.

- `ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL
- `ServiceMethod`합니다: 목록 항목을 제공 웹 메서드
- `TargetControlID`: 드롭다운 목록의 ID
- `Category`: 웹 메서드 호출에 제출 된 범주 정보
- `PromptText`: 비동기적으로 서버에서 목록 데이터를 로드할 때 표시 되는 텍스트
- `ParentControlID`: (선택 사항) 부모 드롭다운의 현재 목록 로드 하는 트리거 목록

사용 되는 프로그래밍 언어에 따라 해당 웹 서비스의 이름을 변경 하지만 다른 모든 특성 값이 동일 합니다. 첫 번째 드롭다운 목록에 대 한 CascadingDropDown 요소는 다음과 같습니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

두 번째 목록에 대 한 컨트롤 extender를 설정 해야 합니다.는 `ParentControlID` 연락처 목록의 요소를 연결 로드 공급 업체 목록 트리거에서 항목을 선택 하는 특성입니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

실제 작업은 다음 다음과 같이 설정 된 웹 서비스에서 수행 됩니다. `[ScriptService]` 특성은 사용, 그렇지 않으면 ASP.NET AJAX 클라이언트 쪽 스크립트 코드에서 웹 메서드를 액세스 하려면 JavaScript 프록시를 만들 수 없습니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

CascadingDropDown을 호출한 웹 메서드의 시그니처는 다음과 같습니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

반환 값 형식의 배열 이어야 하므로 `CascadingDropDownNameValue` 컨트롤 도구 키트에서 정의 됩니다. `GetVendors()` 메서드는 구현 하기가 매우 쉽습니다: AdventureWorks 데이터베이스에 연결 하 고 처음 25 명의 공급 업체를 쿼리 하는 코드입니다. 첫 번째 매개 변수를 `CascadingDropDownNameValue` 생성자는 두 번째 목록 항목의 캡션을 그 값 (html의 특성 값 &lt; `option` &gt; 요소). 코드는 다음과 같습니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

공급 업체에 대 한 연결 된 연락처를 가져오는 (메서드 이름: `GetContactsForVendor()`)는 조금 더 복잡 합니다. 먼저 첫 번째 드롭다운 목록에서 선택한는 공급 업체를 결정 해야 합니다. 해당 작업에 대 한 도우미 메서드를 정의 하는 컨트롤 도구 키트: 합니다 `ParseKnownCategoryValuesString()` 메서드가 반환 되는 `StringDictionary` 드롭다운 데이터 요소:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

보안상의 이유로이 데이터를 먼저 확인 합니다. 공급 업체 항목이 만약 (때문에 합니다 `Category` 첫 번째 CascadingDropDown 요소의 속성이 `"Vendor"`), 선택한 공급 업체의 ID를 검색할 수 있습니다:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

메서드의 나머지 이면 매우 간단 합니다. 공급 업체의 ID는 해당 공급 업체에 대 한 모든 연결 된 연락처를 검색 하는 SQL 쿼리에 대 한 매개 변수로 사용 됩니다. 다시 한 번 메서드 반환 형식의 배열을 `CascadingDropDownNameValue`합니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

ASP.NET 페이지를 로드 하 고 잠시 후 공급 업체 목록 25 개 항목으로 채워집니다. 하나의 항목을 선택 하 고 두 번째 드롭다운 목록을 데이터로 채워지는 방법을 확인 합니다.


[![첫 번째 목록은 자동으로 채워집니다.](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

첫 번째 목록은 자동으로 채워집니다 ([클릭 하 여 큰 이미지 보기](using-cascadingdropdown-with-a-database-cs/_static/image3.png))


[![두 번째 목록의 첫 번째 목록에서 선택 항목에 따라 채워집니다.](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

첫 번째 목록에서 선택 항목에 따라 두 번째 목록 채워집니다 ([클릭 하 여 큰 이미지 보기](using-cascadingdropdown-with-a-database-cs/_static/image6.png))

> [!div class="step-by-step"]
> [이전](filling-a-list-using-cascadingdropdown-cs.md)
> [다음](presetting-list-entries-with-cascadingdropdown-cs.md)
