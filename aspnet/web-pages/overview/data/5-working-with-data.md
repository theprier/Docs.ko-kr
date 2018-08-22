---
uid: web-pages/overview/data/5-working-with-data
title: Asp.net에서 데이터베이스를 사용 하 여 작업 소개 페이지 (Razor) 사이트 | Microsoft Docs
author: tfitzmac
description: 데이터베이스에서 데이터에 액세스 하 여 ASP.NET 웹 페이지를 사용 하 여 표시 하는 방법을 설명이 합니다.
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: b6db23c6f9bba418dff7e6b50bbc1c54f13ccb70
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827801"
---
<a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>Asp.net에서 데이터베이스를 사용 하 여 작업 소개 페이지 (Razor) 사이트
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 ASP.NET Web Pages (Razor) 웹 사이트에서 데이터베이스를 만들려면 Microsoft WebMatrix 도구를 사용 하는 방법 및 표시, 추가, 편집 및 데이터를 삭제할 수 있는 페이지를 만드는 방법을 설명 합니다.
> 
> **학습할 내용:** 
> 
> - 데이터베이스를 만드는 방법입니다.
> - 데이터베이스에 연결 하는 방법입니다.
> - 웹 페이지에서 데이터를 표시 하는 방법입니다.
> - 삽입, 업데이트 및 데이터베이스 레코드를 삭제 하는 방법.
> 
> 다음은 문서에 도입 된 기능입니다.
> 
> - Microsoft SQL Server Compact Edition 데이터베이스를 사용합니다.
> - SQL 쿼리를 사용합니다.
> - `Database` 클래스
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서 에서도 WebMatrix 3를 사용 하 여 작동합니다. ASP.NET 웹 페이지 3 및 Visual Studio 2013 (또는 Visual Studio Express 2013 for Web)를 사용할 수 있습니다. 그러나 사용자 인터페이스는 이와 다릅니다.


## <a name="introduction-to-databases"></a>데이터베이스에 대 한 소개

일반적인 주소록을 가정해 보겠습니다. 주소록의 각 항목에 대 한 (즉, 각 사용자에 대 한) 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 일부 정보가 있습니다.

다음과 같은 그림이 데이터 행과 열이 있는 테이블로 일반적인 방법은입니다. 데이터베이스 용어에서 각 행은 라고도 레코드입니다. (필드 라고도 함) 각 열 데이터의 각 형식에 대 한 값을 포함 합니다: 이름, 이름, 성 및 등입니다.

| **ID** | **FirstName** | **LastName** | **주소** | **이메일** | **전화** |
| --- | --- | --- | --- | --- | --- |
| 1 | Jim | Abrus | 210 100 St SE Orcas 98031 WA | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234 Main St. 시애틀 WA 99011 | terry@cohowinery.com | 555 0101 |

대부분의 데이터베이스 테이블에 대 한 테이블에 고객 번호, 계좌 번호 등과 같은 고유 식별자가 포함 된 열을 있어야 합니다. 이 테이블의 이라고 *기본 키*을 및 테이블의 각 행을 식별 하는 데 사용할 수 있습니다. 예제에서는 ID 열이 주소록에 대 한 기본 키입니다.

이 기본 데이터베이스의 개념을 이해 한 준비가 단순한 데이터베이스를 만들고 추가, 수정 및 삭제와 같은 작업을 수행 하는 방법을 알아봅니다.

> [!TIP] 
> 
> **관계형 데이터베이스**
> 
> 다 수의 스프레드시트 및 텍스트 파일 등의 방법으로 데이터를 저장할 수 있습니다. 그러나 대부분의 비즈니스 용도로 데이터는 관계형 데이터베이스에 저장 됩니다.
> 
> 이 문서에서는 데이터베이스에 무척 깊게 이동 하지 않습니다. 그러나 수 찾게에 대 한 이해 하는 데 유용 합니다. 관계형 데이터베이스에서 정보를 별도 테이블에 논리적으로 구분 됩니다. 예를 들어, 학교에 대 한 데이터베이스 수업 및 학생에 대 한 별도 테이블을 포함할 수 있습니다. 데이터베이스 (예: SQL Server) 소프트웨어에서 지 원하는 강력한 명령을 수 있도록 동적으로 테이블 간의 관계를 설정 합니다. 예를 들어, 일정을 만들려면 학생 및 수업 간의 논리적 관계를 설정 하는 관계형 데이터베이스를 사용할 수 있습니다. 별도 테이블에 데이터를 저장할 테이블 구조의 복잡성이 줄어들고 테이블에 중복 데이터를 보관할 필요가 줄어듭니다.


## <a name="creating-a-database"></a>데이터베이스 만들기

이 절차를 WebMatrix에 포함 된 SQL Server Compact 데이터베이스 디자인 도구를 사용 하 여 SmallBakery 라는 데이터베이스를 만드는 방법을 보여 줍니다. 코드를 사용 하 여 데이터베이스를 만들 수 있지만 더 일반적인 데이터베이스 및 WebMatrix와 같은 디자인 도구를 사용 하 여 데이터베이스 테이블을 만드는 것입니다.

1. WebMatrix를 시작 하 고 빠른 시작 페이지에서 클릭 **사이트에서 템플릿을**합니다.
2. 선택 **빈 사이트**, 및는 **사이트 이름** 상자에 "SmallBakery"를 입력 한 다음 클릭 **확인**합니다. 사이트 생성 되어 WebMatrix에 표시 됩니다.
3. 왼쪽된 창에서 클릭 합니다 **데이터베이스** 작업 영역입니다.
4. 리본 메뉴에서 클릭 **새 데이터베이스**합니다. 빈 데이터베이스는 사이트와 동일한 이름을 사용 하 여 생성 됩니다.
5. 왼쪽된 창에서를 확장 합니다 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.
6. 리본 메뉴에서 클릭 **새 테이블**합니다. WebMatrix는 테이블 디자이너를 엽니다.

    ![[이미지]](5-working-with-data/_static/image1.jpg)
7. 클릭 합니다 **이름** 열 enter &quot;Id&quot;합니다.
8. 에 **데이터 형식** 열 선택 **int**합니다.
9. 설정 합니다 **기본 키가?** 하 고 **식별 됩니다?** 옵션을 **예**합니다.

    이름에서 알 수 있듯이 **기본 키가** 이 되도록 테이블의 기본 키를 데이터베이스에 알려 줍니다. **Id가** 자동으로 모든 새 레코드에 대 한 ID 번호를 만들려면 다음 일련 번호 (1부터 시작)을 할당 하는 데이터베이스를 알려 줍니다.
10. 다음 행을 클릭 합니다. 편집기에는 새 열 정의 시작합니다.
11. 이름 값에 대 한 입력 &quot;이름을&quot;입니다.
12. 에 대 한 **데이터 형식**, 선택 &quot;nvarchar&quot; 길이 50으로 설정 합니다. 합니다 *var* 의 일부로 `nvarchar` 지시 데이터베이스는이 열에 대 한 데이터는 문자열일 크기가 레코드에서 다를 수 있습니다. (합니다 *n* 나타내는 접두사 *national*필드는 알파벳을 나타내는 문자 데이터를 보유할 수를 나타내는, 쓰기 시스템 &#8212; 즉, 필드가 갖는 유니코드 데이터는.)
13. 설정 된 **Null 허용** 옵션을 **No**합니다. 이 적용 됩니다는 *이름을* 열은 비워 없습니다.
14. 라는 열이 동일한 프로세스를 사용 하 여 만들 *설명을*합니다. 설정할 **데이터 형식** "nvarchar"를 길이 및 설정에 대 한 50 **Null 허용** 를 false로 합니다.
15. 명명 된 열을 만듭니다 *가격*합니다. 설정할 **"money" 데이터 형식의** 설정 **Null 허용** 를 false로 합니다.
16. 맨 위에 있는 상자에서 테이블의 이름을 &quot;제품&quot;합니다.

    완료 되 면 정의 다음과 같이 표시 됩니다.

    ![[이미지]](5-working-with-data/_static/image2.jpg)
17. 테이블을 저장 하려면 Ctrl + S를 누릅니다.

## <a name="adding-data-to-the-database"></a>데이터베이스에 데이터 추가

이제 문서의 뒷부분에서 작업할 수 있는 데이터베이스에 몇 가지 샘플 데이터를 추가할 수 있습니다.

1. 왼쪽된 창에서를 확장 합니다 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.
2. Product 테이블을 마우스 오른쪽 단추로 누른 **데이터**입니다.
3. 편집 창에서 다음 레코드를 입력 합니다.

    | **이름** | **설명** | **가격** |
    | --- | --- | --- |
    | 이동 | 구운된 새로 매일입니다. | 2.99 |
    | Strawberry Shortcake | 우리의 가든에서 유기적 딸기를 사용 하 여 수행 합니다. | 9.99 |
    | Apple 원형 | Mom의 원형에만 두 번째입니다. | 12.99 |
    | Pecan 원형 | Pecans을 원하는 경우이 적합 합니다. | 10.99 |
    | 레몬 원형 | 전 세계에서 최상의 lemons를 사용 하 여 수행 합니다. | 11.99 |
    | Cupcakes | 자녀가 및에서 kid 이러한 선호 됩니다. | 7.99 |

    에 아무 것도 입력할 필요가 있는지를 기억 합니다 *Id* 열입니다. 만들 때 합니다 *Id* 설정한 열을 해당 **Id** 속성을 true로 자동으로 채울 수를 발생 시키는 합니다.

    데이터 입력 완료 하면 테이블 디자이너는 다음과 같습니다.

    ![[이미지]](5-working-with-data/_static/image3.jpg)
4. 데이터베이스 데이터를 포함 하는 탭을 닫습니다.

## <a name="displaying-data-from-a-database"></a>데이터베이스에서 데이터를 표시합니다.

가져온 후 데이터를 사용 하 여 데이터베이스에서 ASP.NET 웹 페이지에서 데이터를 표시할 수 있습니다. 표시할 테이블 행을 선택 하려면 데이터베이스에 전달 하는 명령에는 SQL 문을 사용할 수 있습니다.

1. 왼쪽된 창에서 클릭 합니다 **파일** 작업 영역입니다.
2. 웹 사이트의 루트에서 이라는 새 CSHTML 페이지를 만듭니다 *ListProducts.cshtml*합니다.
3. 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    첫 번째 코드 블록에서 엽니다는 *SmallBakery.sdf* 앞에서 만든 파일 (데이터베이스). `Database.Open` 가정 메서드는 *.sdf* 웹 사이트의 파일은 *앱\_데이터* 폴더입니다. (지정할 필요가 없습니다는 *.sdf* 확장 &#8212; 사실 경우는 `Open` 메서드가 작동 하지 않습니다.)

    > [!NOTE]
    > 합니다 *앱\_데이터* 폴더는 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다. 자세한 내용은 [데이터베이스에 연결할](#SB_ConnectingToADatabase) 이 문서의 뒷부분에 나오는.

    그런 다음 다음 SQL을 사용 하 여 데이터베이스를 쿼리 하는 요청을 만드는 `Select` 문:

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    문에서 `Product` 쿼리 테이블을 식별 합니다. `*` 문자 쿼리가 테이블에서 모든 열을 반환 해야 함을 지정 합니다. (또한를 나열할 수 열을 개별적으로 열 중 일부만 참조 하려는 경우 쉼표로 구분 된.) `Order By` 절은 데이터를 정렬 해야 하는 방법을 나타냅니다 &#8212; 하 여이 경우에 *이름* 열입니다. 즉, 데이터의 값을 기준으로 사전순으로 정렬 하는 *이름을* 각 행에 대 한 열입니다.

    페이지의 본문에서 태그 데이터를 표시 하는 데 사용할 수 있는 HTML 테이블을 만듭니다. 내부를 `<tbody>` 요소를 사용할를 `foreach` 루프를 개별적으로 쿼리에서 반환 되는 각 데이터 행을 가져옵니다. HTML 테이블 행을 각 데이터 행에 대해 만든 (`<tr>` 요소). HTML 테이블 셀을 만든 다음 (`<td>` 요소) 각 열에 대 한 합니다. 루프를 계속 실행 될 때마다 데이터베이스에서 사용 가능한 다음 행은는 `row` 변수 (이에서 설정한는 `foreach` 문). 사용할 수는 행의 개별 열을 가져오려고 `row.Name` 또는 `row.Description` 또는 원하는 무엇이 든 이름 열입니다.
4. 브라우저에서 페이지를 실행 합니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 페이지에는 다음과 같은 목록이 표시 됩니다.

    ![[이미지]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **구조적된 쿼리 언어 (SQL)**
> 
> SQL은 데이터베이스에서 데이터를 관리 하는 것에 대 한 대부분의 관계형 데이터베이스에 사용 되는 언어입니다. 데이터를 검색 하 고 업데이트 하 고 만들기, 수정 및 데이터베이스 테이블을 관리 하도록 하는 명령을 포함 합니다. SQL 프로그래밍 언어 (예: WebMatrix에서 사용 하는 것)에 대해 다릅니다. 이므로 sql 개념 원하는 데이터베이스에 알립니다 하는 것은 데이터베이스의 데이터를 가져오는 작업을 수행 하는 방법을 파악 합니다. 다음은 일부 SQL 명령의 예로 및 용도:
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 인출이 *Id*, *이름*, 및 *가격* 레코드의 열을 *제품* 테이블의 값 *가격* 10 개가 넘는 이며의 값을 기준으로 알파벳 순서로 결과 반환 합니다 *이름을* 열입니다. 이 명령은 일치 하는 레코드가 경우 조건을 또는 빈 집합을 충족 하는 레코드를 포함 하는 결과 집합을 반환 합니다.
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> 에 새 레코드를 삽입 하는이 *제품* 테이블을 설정 합니다 *이름* 열을 &quot;크 라 상&quot;의 *설명* 열&quot; 잘 끊어지는 만족&quot;, 및 1.99 가격입니다.
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> 이 명령에서 레코드를 삭제 합니다 *제품* 2008 년 1 월 1 일 이전인 만료 날짜 열이 있는 테이블입니다. (있다고 가정 합니다 *제품* 테이블에는 이러한 열입니다.) MM/DD/YYYY 형식으로 날짜는 여기에 입력 하는 있지만 해당 로캘에 사용 되는 형식으로 입력 해야 합니다.
> 
> 합니다 `Insert Into` 고 `Delete` 명령 결과 집합을 반환 하지 않습니다. 대신, 레코드 수를 명령에 의해 영향을 알려 주는 숫자로 반환 합니다.
> 
> 이러한 작업 (예: 레코드 삽입 및 삭제)의 일부에 대 한 작업을 요청 하는 프로세스는 데이터베이스에 대 한 적절 한 권한이 해야 합니다. 데이터베이스에 연결할 때 사용자 이름 및 암호를 제공 해야 하는 프로덕션 데이터베이스에 대 한 이유입니다.
> 
> SQL 명령 여러 가지가 있지만 다음과 같은 패턴을 따릅니다. SQL 명령을 사용 하 여 데이터베이스 및 테이블을 만들고, 테이블의 레코드 개수, 가격 계산 보다 많은 작업을 수행할 수 있습니다.


## <a name="inserting-data-in-a-database"></a>데이터베이스에 데이터 삽입

이 섹션에는 사용자가 새 제품을 추가할 수 있는 페이지를 만드는 방법을 보여 줍니다 합니다 *제품* 데이터베이스 테이블입니다. 새 제품 레코드를 삽입 한 후 페이지에 표시 됩니다 사용 하 여 업데이트 된 테이블의 *ListProducts.cshtml* 이전 섹션에서 만든 페이지입니다.

페이지는 사용자가 입력 데이터를 데이터베이스에 대 한 유효한 지 확인 하려면 유효성 검사를 포함 합니다. 예를 들어 코드 페이지에서를 변경 하면 모든 필요한 열에 대 한 입력 된 값입니다.

1. 웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *InsertProducts.cshtml*합니다.
2. 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    페이지의 본문 이름, 설명 및 가격을 입력할 수 있도록 하는 세 가지 텍스트 상자를 사용 하 여 HTML 폼을 포함 합니다. 사용자가 클릭 하면 합니다 **삽입** 단추를 페이지의 맨 위에 있는 코드에 연결을 엽니다 합니다 *SmallBakery.sdf* 데이터베이스입니다. 사용 하 여 사용자가 제출 하는 값을 다음 표시는 `Request` 개체 및 해당 값을 로컬 변수에 할당 합니다.

    필요한 각 열에 대 한 사용자 값을 입력 했는지 확인을 위해 등록할 각 `<input>` 의 유효성을 검사 하려는 요소:

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    `Validation` 도우미 등록 하는 필드의 각 값 임을 확인 합니다. 모든 필드를 확인 하 여 유효성 검사를 통과 했는지 여부를 테스트할 수 있습니다 `Validation.IsValid()`는 사용자 로부터 얻을 수 있는 정보를 처리 하기 전에 일반적으로 수행 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    (합니다 `&&` 연산자 의미 AND-이 테스트는 *양식을 제출 하 여 모든 필드 유효성 검사를 통과 한 경우*.)

    모든 열 유효성을 검사 하는 경우 (none 인 빈) 데이터를 삽입 한 다음 다음과 같이 실행할 SQL 문을 만들어 보겠습니다.

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    매개 변수 자리 표시자를 포함 하면 삽입할 값 (`@0`, `@1`, `@2`).

    > [!NOTE]
    > 보안 조치로, 항상 전달할 값 매개 변수를 사용 하는 SQL 문은 앞의 예제에서 볼 수 있듯이 합니다. 이렇게 하면 사용자의 데이터 유효성 검사를 더한 (때때로 SQL 삽입 공격 이라고 함) 데이터베이스에 악의적인 명령이 보내려는 시도 방지할 수 있도록 합니다.

    쿼리를 실행 하려면이 문을 사용 자리 표시자에 대 한 대체 값이 포함 된 변수를 전달 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    이후에 `Insert Into` 문이 실행,이 줄을 사용 하 여 제품을 나열 하는 페이지에 사용자를 보내려면:

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    유효성 검사가 성공 하지 않은 경우에 삽입을 건너뜁니다. 누적 된 오류 메시지 (있는 경우)를 표시할 수 있는 페이지에서 도우미를 대신 해야 합니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    태그에 스타일 블록 라는 CSS 클래스 정의 포함 되도록 알림 `.validation-summary-errors`합니다. 이 기본적으로 사용 되는 CSS 클래스의 이름을 합니다 `<div>` 유효성 검사 오류를 포함 하는 요소입니다. CSS 클래스 유효성 검사 요약 오류 빨간색으로 표시 되 고에 굵게, 있지만 정의할 수를 지정 하는 경우에 `.validation-summary-errors` 원하는 서식 표시 하는 클래스입니다.

### <a name="testing-the-insert-page"></a>Insert 페이지 테스트

1. 브라우저에서 페이지를 표시 합니다. 페이지에는 다음 그림에 표시 되는 것과 비슷한 폼을 표시 합니다.

    ![[이미지]](5-working-with-data/_static/image5.jpg)
2. 모든 열에 대 한 값을 입력 하지만 남겨 두어야 합니다 *가격* 열은 비워 둠 합니다.
3. **삽입**을 클릭합니다. 다음 그림에 나와 있는 것 처럼 페이지는 오류 메시지를 표시 합니다. (새 레코드가 생성 됩니다.)

    ![[이미지]](5-working-with-data/_static/image6.jpg)
4. 폼을 완전히 입력 하 고 클릭 **삽입**합니다. 이 이번에는 *ListProducts.cshtml* 페이지가 표시 되 고 새 레코드를 표시 합니다.

## <a name="updating-data-in-a-database"></a>데이터베이스의 데이터를 업데이트 하는 중

테이블에 데이터를 입력 한 후 업데이트 해야 합니다. 이 절차 앞에 데이터 삽입을 위해 만든 것과 비슷한 두 페이지를 만드는 방법을 보여 줍니다. 첫 번째 페이지는 제품을 표시 하 고 사용자가 변경 하나를 선택할 수입니다. 두 번째 페이지를 사용 하면 사용자가 실제로 편집 하 고 저장할 수 있습니다.

> [!NOTE] 
> 
> **중요 한** 프로덕션 웹 사이트에서 일반적으로 제한할 있습니다 데이터를 변경 하려면 허용할 사람입니다. 멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자 권한을 부여 하는 방법에 대 한 정보를 참조 하세요 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.


1. 웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *EditProducts.cshtml*합니다.
2. 파일의 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    이 페이지 간의 유일한 차이점 및 *ListProducts.cshtml* 페이지에서 이전 버전은이 페이지의 HTML 테이블로 포함 하는 표시 하는 추가 열을 **편집** 링크 합니다. 이 링크를 클릭 하면 소요 하는 *UpdateProducts.cshtml* 페이지 (만들게 될 다음) 선택한 레코드를 편집할 수 있습니다.

    만드는 코드를 확인 합니다 **편집** 링크:

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    이 HTML을 만듭니다 `<a>` 요소가 해당 `href` 특성은 동적으로 설정 됩니다. `href` 특성 링크를 클릭할 때 표시할 페이지를 지정 합니다. 또한 전달 된 `Id` 링크를 현재 행의 값입니다. 페이지를 실행 하는 경우 페이지의 소스는 다음과 같은 링크를 포함할 수 있습니다.

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    다음에 유의 합니다 `href` 특성이로 설정 된 `UpdateProducts/n`여기서 *n* 제품입니다. 사용자가 이러한 링크 중 하나를 클릭 하면 결과 URL 같이 표시 됩니다.

    `http://localhost:18816/UpdateProducts/6`

    즉, 제품 번호를 편집할 수는 URL에 전달 됩니다.
3. 브라우저에서 페이지를 표시 합니다. 페이지는 다음과 같은 형식으로 데이터를 표시합니다.

    ![[이미지]](5-working-with-data/_static/image7.jpg)

    다음으로, 사용자가 실제로 데이터를 업데이트할 수 있는 페이지를 만들어야 합니다. 업데이트 페이지에 유효성 검사는 사용자가 입력 데이터 유효성 검사를 포함 합니다. 예를 들어 코드 페이지에서를 변경 하면 모든 필요한 열에 대 한 입력 된 값입니다.
4. 웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *UpdateProducts.cshtml*합니다.
5. 파일의 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    제품 표시 되는 위치 및 사용자가 편집할 수 있는 HTML 폼을 포함 하는 페이지의 본문입니다. 표시할 제품을 가져오려면이 SQL 문을 사용할 수 있습니다.

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    이 ID에 전달 되는 값과 일치 하는 제품을 선택 합니다는 `@0` 매개 변수입니다. (때문에 *Id* 기본 핵심 이며 따라서 해야 하나의 제품 레코드 그 어느 때 선택할 수 있습니다 이러한 방식으로, 고유 합니다.) 이를 전달 하는 ID 값을 가져오려면 `Select` 문을 다음 구문을 사용 하 여 URL의 일부로 페이지에 전달 되는 값을 읽을 수 있습니다.

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    제품 레코드를 실제로 페치 하려면 사용는 `QuerySingle` 레코드 하나만 반환 하는 메서드:

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    단일 행에 반환 되는 `row` 변수입니다. 각 열에서 데이터를 가져오기 하 고 다음과 같은 로컬 변수에 할당할 수 있습니다.

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    폼에 대 한 태그에서 이러한 값에에서 표시 됩니다 자동으로 개별 입력란 다음과 같은 포함 된 코드를 사용 하 여:

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    코드의 해당 부분 업데이트 제품 레코드를 표시 합니다. 레코드가 표시 되 면 사용자 개별 열을 편집할 수 있습니다.

    사용자가 클릭 하 여 폼을 제출 하는 경우는 **업데이트** 단추를의 코드는 `if(IsPost)` 블록이 실행 됩니다. 사용자의 값을 가져옵니다는 `Request` 개체 변수에 값을 저장 하 고 각 열 채워져 있는지 확인 합니다. 유효성 검사에 통과 하는 경우 코드를 다음 SQL Update 문을 만듭니다.

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    SQL에서 `Update` 문을 지정할 각 열 설정할 값을 업데이트 하 합니다. 이 코드에서 값을 매개 변수 자리 표시자를 사용 하 여 지정 된 `@0`, `@1`, `@2`등입니다. (보안상의 앞에서 설명한 대로 항상 값을 전달 해야 SQL 문에 매개 변수를 사용 하 여.)

    호출 하는 경우는 `db.Execute` SQL 문의 매개 변수에 해당 하는 순서 대로 값이 포함 된 변수를 전달할 메서드:

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    이후에 `Update` 문이 실행 된 사용자 편집 페이지를 다시 리디렉션할 하려면 다음 메서드를 호출 합니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    사용자 데이터베이스의 데이터는 업데이트 된 목록을 표시 하 고 다른 제품을 편집할 수 됩니다.
6. 페이지를 저장합니다.
7. 실행 합니다 *EditProducts.cshtml* 페이지 (업데이트 페이지 제외) 하 고 클릭 한 다음 **편집** 편집할 제품을 선택 합니다. 합니다 *UpdateProducts.cshtml* 선택한 레코드를 보여 주는 페이지가 표시 됩니다.

    ![[이미지]](5-working-with-data/_static/image8.jpg)
8. 변경 하 고 클릭 **업데이트**합니다. 업데이트 된 데이터를 사용 하 여 제품 목록은 다시 표시 됩니다.

## <a name="deleting-data-in-a-database"></a>데이터베이스의 데이터를 삭제합니다.

이 섹션에서는 사용자의 제품을 삭제 하도록 하는 방법을 보여 줍니다 합니다 *제품* 데이터베이스 테이블입니다. 이 예제에서는 두 페이지로 이루어져 있습니다. 첫 번째 페이지에서 사용자를 삭제 하는 레코드를 선택 합니다. 삭제할 레코드는 레코드를 삭제 하도록 확인을 두 번째 페이지에 표시 됩니다.

> [!NOTE] 
> 
> **중요 한** 프로덕션 웹 사이트에서 일반적으로 제한할 있습니다 데이터를 변경 하려면 허용할 사람입니다. 멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자 권한을 부여 하는 방법에 대 한 정보를 참조 하세요 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.


1. 웹 사이트에서 이라는 새 CSHTML 파일을 만듭니다 *ListProductsForDelete.cshtml*합니다.
2. 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    이 페이지는 비슷합니다는 *EditProducts.cshtml* 앞에서 페이지입니다. 그러나 표시 하는 대신는 **편집** 링크 각 제품에 대 한 표시를 **삭제** 링크 합니다. 합니다 **삭제** 링크가 포함된 된 다음 코드를 사용 하 여 태그에서 생성 됩니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    이 사용자가 링크를 클릭할 때 다음과 같은 URL을 만듭니다.

    `http://<server>/DeleteProduct/4`

    라는 페이지를 호출 하는 URL *DeleteProduct.cshtml* (만들게 될 옆) 하 고 삭제할 제품의 ID를 전달 (여기에서는 4).
3. 파일을 저장 하지만 열어 둡니다.
4. 라는 다른 CHTML 파일을 만듭니다 *DeleteProduct.cshtml*합니다. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    이 페이지에 의해 호출 됩니다 *ListProductsForDelete.cshtml* 고 사용자가 제품을 삭제 하도록 확인 합니다. 삭제할 제품을 나열 하려면 얻게 URL에서 삭제할 제품의 ID는 다음 코드를 사용 하 여:

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    페이지는 사용자가 실제로 레코드를 삭제 하는 단추를 클릭 한 다음 요청 합니다. 이 중요 한 보안 측정값을: 업데이트 또는 삭제와 같은 웹 사이트의 중요 한 작업을 수행할 때 이러한 작업이 이루어져야 합니다. 항상 가져오기 작업을 하지 POST 작업을 사용 하 여 합니다. 가져오기 작업을 사용 하 여 삭제 작업을 수행할 수 있도록 사이트는 설정 하 고, 경우에 같은 URL을 전달할 수 있습니다 누구나 `http://<server>/DeleteProduct/4` 및 데이터베이스에서 원하는 항목을 삭제 합니다. 확인을 추가 하 고 POST를 사용 하 여 삭제를 수행할 수 있도록 페이지를 코딩 하 여 사이트에 보안 조치를 추가 합니다.

    실제 삭제 작업은 post 작업을이 이며 ID 비어 있지는 먼저 확인 하는 다음 코드를 사용 하 여 수행 됩니다.

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    코드에 지정된 된 레코드를 삭제 하 고 다음 목록 페이지로 사용자를 리디렉션하는 SQL 문을 실행 합니다.
5. 실행할 *ListProductsForDelete.cshtml* 브라우저에서 합니다.

    ![[이미지]](5-working-with-data/_static/image9.jpg)
6. 클릭 합니다 **삭제** 제품 중 하나에 대 한 링크입니다. 합니다 *DeleteProduct.cshtml* 해당 레코드를 삭제할 것인지 확인 페이지가 표시 됩니다.
7. 클릭 합니다 **삭제** 단추입니다. 제품 레코드가 삭제 되 고는 업데이트 된 제품 목록으로 페이지가 새로 고쳐집니다.

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>데이터베이스에 연결
> 
> 두 가지 방법으로 데이터베이스에 연결할 수 있습니다. 첫 번째 사용 하는 것을 `Database.Open` 메서드 및 데이터베이스 파일의 이름을 지정 하 (작은 합니다 *.sdf* 확장):
> 
> `var db = Database.Open("SmallBakery");`
> 
> 합니다 `Open` 메서드가 있다고 가정 합니다. *sdf* 파일은 웹 사이트 *App\_데이터* 폴더입니다. 이 폴더는 데이터를 보유에 맞게 설계 되었습니다. 예를 들어, 웹 사이트에 데이터를 읽고 쓸 수 있도록 적절 한 권한이 및 보안을 위해 WebMatrix 액세스를 허용 하지 파일에이 폴더에서.
> 
> 두 번째 방법은 연결 문자열을 사용 하는 것입니다. 연결 문자열을 데이터베이스에 연결 하는 방법에 대 한 정보를 포함 합니다. 파일 경로 포함할 수 있습니다 또는 사용자 이름 및 해당 서버에 연결할 암호와 함께 로컬 또는 원격 서버의 SQL Server 데이터베이스의 이름을 포함할 수 있습니다. (중앙에서 관리 되는 버전의 SQL Server에서 데이터를 유지 하는 경우와 같은 호스팅 공급자의 사이트에서 하려면 항상 사용 하는 연결 문자열 데이터베이스 연결 정보를 지정 합니다.)
> 
> WebMatrix에서 연결 문자열은 일반적으로 저장 라는 XML 파일에 *Web.config*합니다. 이름에서 알 수 있듯이, 사용할 수는 *Web.config* 사이트 필요할 수 있는 연결 문자열을 포함 하 여 사이트의 구성 정보를 저장 하 여 웹 사이트의 루트에 있는 파일입니다. 연결 문자열의 예는 *Web.config* 파일은 다음과 같습니다.
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> 예제에서는 연결 문자열을 가리키는 어딘가에 서버에서 실행 되는 SQL Server 인스턴스의 데이터베이스 (로컬 달리 *.sdf* 파일). 에 대 한 적절 한 이름으로 대체 해야 `myServer` 하 고 `myDatabase`, SQL Server 로그인 값을 지정 하 고 `username` 및 `password`합니다. (사용자 이름 및 암호 값 같지 반드시 Windows 자격 증명 또는 호스팅 공급자가 제공한 서버에 로그인 하는 값입니다. 관리자에 게 문의 해야 하는 정확한 값에 대 한 합니다.)
> 
> 합니다 `Database.Open` 메서드는 데이터베이스의 이름을 전달할 수 있기 때문에 유연 *.sdf* 에 저장 된 연결 문자열의 이름 또는 파일을 *Web.config* 파일. 다음 예제에서는 이전 예제에 나와 있는 연결 문자열을 사용 하 여 데이터베이스에 연결 하는 방법을 보여 줍니다.
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> 언급 했 듯이 `Database.Open` 메서드를 사용 하면 데이터베이스 이름 또는 연결 문자열을 전달 하 고 사용 하는 그림 됩니다. 배포 하는 경우이 기능은 매우 유용 (게시) 웹 사이트입니다. 사용할 수는 *.sdf* 파일을 *앱\_데이터* 을 개발 하 고 사이트를 테스트 하는 경우 폴더입니다. 사이트를 프로덕션 서버로 이동할 때 연결 문자열을 사용할 수 있습니다 합니다 *Web.config* 와 동일한 이름을 가진 파일에 *.sdf* 있지만 호스팅 공급자의 가리키는 &#8212;코드를 변경할 필요 없이 합니다.
> 
> 마지막으로, 연결 문자열을 직접 사용 하려는 경우 호출할 수 있습니다 합니다 `Database.OpenConnectionString` 메서드와 패스의 이름만 대신 해당 실제 연결 문자열을 *Web.config* 파일입니다. 어떤 이유로 없는 연결 문자열에 액세스 하는 경우에 유용할 수 있습니다 (에서 같은 값 또는 합니다 *.sdf* 파일 이름) 페이지 실행 될 때까지 합니다. 그러나 대부분의 시나리오에서 사용할 수 있습니다 `Database.Open` 이 문서에 설명 된 대로 합니다.


## <a name="additional-resources"></a>추가 리소스

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [SQL Server 또는 WebMatrix에서 MySQL 데이터베이스에 연결](https://go.microsoft.com/fwlink/?LinkId=208661)
- [ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)
