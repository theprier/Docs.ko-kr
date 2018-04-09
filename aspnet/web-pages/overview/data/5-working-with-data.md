---
uid: web-pages/overview/data/5-working-with-data
title: ASP.NET 웹에서 데이터베이스 작업 소개 페이지 (Razor) 사이트 | Microsoft Docs
author: tfitzmac
description: 데이터베이스에서 데이터를 액세스 하 고 ASP.NET 웹 페이지를 사용 하 여 표시 하는 방법을 설명이 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2014
ms.topic: article
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 563074cf3e60717c2e6c336a2c282b4203f73b8b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹에서 데이터베이스 작업 소개 페이지 (Razor) 사이트
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 데이터베이스를 만들려면 Microsoft WebMatrix 도구를 사용 하는 방법 및 표시, 추가, 편집 및 데이터를 삭제할 수 있는 페이지를 만드는 방법을 설명 합니다.
> 
> **학습 내용:** 
> 
> - 데이터베이스를 만드는 방법.
> - 데이터베이스에 연결 하는 방법.
> - 웹 페이지에 데이터를 표시 하는 방법.
> - 삽입, 업데이트 및 데이터베이스 레코드를 삭제 하는 방법.
> 
> 다음은 문서에 도입 된 기능입니다.
> 
> - Microsoft SQL Server Compact Edition 데이터베이스를 사용 합니다.
> - SQL 쿼리를 사용 합니다.
> - `Database` 클래스
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서는 WebMatrix 3 에서도 작동합니다. ASP.NET Web Pages 3 및 Visual Studio 2013 (또는 Visual Studio Express 2013 for Web);를 사용할 수 있습니다. 그러나 사용자 인터페이스가 달라 집니다.


## <a name="introduction-to-databases"></a>데이터베이스 소개

일반적인 주소록을 가정해 보세요. 주소록에 각 항목에 대 한 (즉, 각 사용자에 대 한) 일부의 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 정보를 해야 합니다.

이와 같은 그림 데이터를 행과 열이 있는 테이블로 일반적인 방법은입니다. 데이터베이스의 경우 각 행은 종종 레코드 라고 합니다. 각 데이터 형식에 대 한 값을 포함 하는 각 열 (필드 라고도 함): 이름, 마지막 이름 및 등입니다.

| **ID** | **FirstName** | **LastName** | **주소** | **전자 메일** | **전화** |
| --- | --- | --- | --- | --- | --- |
| 1 | Jim | Abrus | 210 100th St SE Orcas WA 98031 | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234 Main St. 시애틀 WA 99011 | terry@cohowinery.com | 555 0101 |

대부분의 데이터베이스 테이블에 대 한 테이블에 고객 번호, 계좌 번호 등과 같은 고유 식별자가 포함 된 열입니다. 테이블의로 알려져 *기본 키*, 테이블의 각 행 식별을 사용 합니다. 예제에서는 ID 열은 주소록에 대 한 기본 키를 사용 합니다.

이 기본 데이터베이스의 개념을 이해 한 준비가 간단한 데이터베이스를 만들고 추가, 수정 및 데이터 삭제와 같은 작업을 수행 하는 방법을 알아봅니다.

> [!TIP] 
> 
> **관계형 데이터베이스**
> 
> 스프레드시트 및 텍스트 파일 등의 방법으로 많은 데이터를 저장할 수 있습니다. 그러나 대부분의 비즈니스 사용자에 대 한 데이터는 관계형 데이터베이스에 저장 됩니다.
> 
> 이 문서는 데이터베이스로 매우 밀접 하 게 이동 하지 않습니다. 그러나 좋습니다 것에 대 한 이해 합니다. 관계형 데이터베이스의 정보는 별도 테이블으로 논리적으로 구분 됩니다. 예를 들어 수업 및 학생 들에 대 한 학교에 대 한 데이터베이스 별도 테이블에 포함 될 수 있습니다. 데이터베이스 소프트웨어 (예: SQL Server) 지원 강력한 수 있는 명령을 동적으로 테이블 간의 관계를 설정 합니다. 예를 들어, 일정을 만들기 위해 학생과 클래스 간의 논리적 관계를 설정 하는 관계형 데이터베이스를 사용할 수 있습니다. 별도 테이블에 데이터를 저장할 테이블 구조의 간단 하 고 테이블에 중복 데이터를 보관할 필요가 줄어 데이터입니다.


## <a name="creating-a-database"></a>데이터베이스 만들기

이 절차에서는 WebMatrix에 포함 된 SQL Server Compact 데이터베이스 디자인 도구를 사용 하 여 SmallBakery 라는 데이터베이스를 만드는 방법을 보여 줍니다. 코드를 사용 하는 데이터베이스를 만들 수는 있지만 데이터베이스 및 WebMatrix와 같은 디자인 도구를 사용 하 여 데이터베이스 테이블을 만드는 대부분의 일반적인 됩니다.

1. WebMatrix를 시작 하 고 빠른 시작 페이지에서 클릭 **템플릿에서 사이트**합니다.
2. 선택 **빈 사이트**, 및는 **사이트 이름** 상자 "SmallBakery"를 입력 한 다음 클릭 **확인**합니다. 사이트 생성 되어 WebMatrix에 표시 됩니다.
3. 왼쪽된 창에서 클릭 된 **데이터베이스** 작업 영역입니다.
4. 리본 메뉴에서 클릭 **새 데이터베이스**합니다. 빈 데이터베이스는 사이트와 동일한 이름을 가진 생성 됩니다.
5. 왼쪽된 창에서 확장 된 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.
6. 리본 메뉴에서 클릭 **새 테이블**합니다. WebMatrix는 테이블 디자이너를 엽니다.

    ![[image]](5-working-with-data/_static/image1.jpg)
7. 클릭는 **이름** 열을 입력 하 고 &quot;Id&quot;합니다.
8. 에 **데이터 형식** 열에서 선택 **int**합니다.
9. 설정의 **기본 키가?** 및 **식별은?** 옵션을 **예**합니다.

    이름에서 알 수 있듯이 **기본 키가** 이 되도록 테이블의 기본 키의 데이터베이스에 알려 줍니다. **인증서가 Id** (1부터 시작)에 다음 일련 번호를 할당 하 고 자동으로 모든 새 레코드에 대 한 ID 번호를 만들려면 데이터베이스에 지시 합니다.
10. 다음 행을 클릭 합니다. 편집기에는 새 열 정의 시작합니다.
11. 이름 값에 대 한 입력 &quot;이름&quot;합니다.
12. 에 대 한 **데이터 형식**, 선택 &quot;nvarchar&quot; 길이 50으로 설정 합니다. *var* 의 일부가 `nvarchar` 이 열에 대 한 데이터가 필요에 따라 크기가 레코드 간에 다를 수 있습니다 하는 문자열을 될 것 이라는 데이터베이스에 알려 줍니다. (의 *n* 나타내는 접두사 *national*, 필드를 나타내는 모든 알파벳 문자 데이터를 보유할 수를 나타내는 또는 쓰기 시스템 &#8212; 즉, 필드 유니코드 데이터를 보유 합니다.)
13. 설정의 **Null 허용** 옵션을 **아니요**합니다. 이 강제 적용 하는 *이름* 열 비워 두면 되지 않습니다.
14. 라는 열이 동일한 프로세스를 사용 하 여 만들 *설명*합니다. 설정 **데이터 형식** 길이 및 설정에 대 한 "nvarchar"으로 **Null 허용** 를 false입니다.
15. व े ं 라는 *가격*합니다. 설정 **"money" 데이터 형식의** 설정 **Null 허용** 를 false입니다.
16. 맨 위에 있는 상자에서 테이블의 이름을 지정 &quot;제품&quot;합니다.

    완료 되 면 정의 다음과 같이 표시 됩니다.

    ![[image]](5-working-with-data/_static/image2.jpg)
17. 테이블을 저장 하려면 Ctrl + S를 누릅니다.

## <a name="adding-data-to-the-database"></a>데이터베이스에 데이터 추가

이제 문서의 뒷부분에서 다루게 하 여 데이터베이스에 몇 가지 샘플 데이터를 추가할 수 있습니다.

1. 왼쪽된 창에서 확장 된 **SmallBakery.sdf** 노드와 클릭 **테이블**합니다.
2. Product 테이블을 마우스 오른쪽 단추로 누른 **데이터**합니다.
3. 편집 창에서 다음 레코드를 입력 합니다.

    | **이름** | **설명** | **가격** |
    | --- | --- | --- |
    | 빵 | 매일 새로 기본 제공된 합니다. | 2.99 |
    | 딸기맛 Shortcake | 우리의 가든에서 유기적 딸기 사용해 서 변경 합니다. | 9.99 |
    | Apple 원형 | 어머니의 원형에만 두 번째입니다. | 12.99 |
    | Pecan 원형 | Pecans 원한다 면이입니다. | 10.99 |
    | 레몬 원형 | 세계에서 가장 좋은 lemons 사용해 서 변경 합니다. | 11.99 |
    | 컵 케이크 | 자녀가 및에서 kid이 도움이 됩니다. | 7.99 |

    에 대 한 어떤 것도 입력할 필요가 없습니다 기억는 *Id* 열입니다. 만들 때의 *Id* 설정 하면 열을 해당 **Id** 속성을 자동으로 입력을 true로 합니다.

    데이터 입력이 완료 되 면 테이블 디자이너는 다음과 같이 표시 됩니다.

    ![[image]](5-working-with-data/_static/image3.jpg)
4. 데이터베이스 데이터를 포함 하는 탭을 닫습니다.

## <a name="displaying-data-from-a-database"></a>데이터베이스에서 데이터 표시

에 데이터가 있는 데이터베이스 했으면, ASP.NET 웹 페이지에서 데이터를 표시할 수 있습니다. 표시할 테이블 행을 선택 하려면 명령을 데이터베이스에 전달 하는 SQL 문을 사용 합니다.

1. 왼쪽된 창에서 클릭 된 **파일** 작업 영역입니다.
2. 웹 사이트의 루트에 있는 라는 새로운 CSHTML 페이지 생성 *ListProducts.cshtml*합니다.
3. 기존 태그를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    열은 첫 번째 코드 블록에는 *SmallBakery.sdf* 앞에서 만든 파일 (데이터베이스). `Database.Open` 메서드 가정 하는 *.sdf* 파일은 웹 사이트의 *앱\_데이터* 폴더입니다. (는 지정할 필요가 없습니다는 *.sdf* 확장 &#8212; 이렇게 하면 실제로 `Open` 메서드 작동 하지 않습니다.)

    > [!NOTE]
    > *앱\_데이터* 폴더는 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다. 자세한 내용은 참조 [데이터베이스에 연결](#SB_ConnectingToADatabase) 이 문서의 뒷부분에 나오는 합니다.

    다음 SQL을 사용 하 여 데이터베이스를 쿼리 하는 요청 커졌을 `Select` 문:

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    문에서 `Product` 쿼리에 테이블을 식별 합니다. `*` 문자 지정 하면 쿼리 테이블에서 모든 열을 반환 해야 합니다. (또한를 나열할 수 열 개별적으로 열 중 일부만 표시 하려는 경우 쉼표로 구분 합니다.) `Order By` 절에서 데이터를 정렬 해야 하는 방법을 나타냅니다. &#8212; 하 여이 경우는 *이름* 열입니다. 즉, 데이터의 값에 따라 사전순으로 정렬 되는 *이름* 각 행에 대 한 열입니다.

    페이지 본문 태그 데이터를 표시 하는 데 사용 될 있는 HTML 테이블을 만듭니다. 내부는 `<tbody>` 요소를 사용는 `foreach` 루프 개별적으로 쿼리에 의해 반환 되는 각 데이터 행을 가져오도록 합니다. 각 데이터 행에 대 한 HTML 표 행 만들면 (`<tr>` 요소). 다음 HTML 테이블 셀을 만듭니다 (`<td>` 요소) 각 열에 대 한 합니다. 에 루프를 계속 실행 될 때마다 데이터베이스에서 사용 가능한 다음 행은는 `row` 변수 (이에서 설정한는 `foreach` 문). 사용할 수는 행의 개별 열을 가져오려면 `row.Name` 또는 `row.Description` 또는 원하는 모든 이름 열입니다.
4. 브라우저에서 페이지를 실행 합니다. (있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.) 페이지에는 다음과 같은 목록을 표시합니다.

    ![[image]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **구조적된 쿼리 언어 (SQL)**
> 
> SQL은 데이터베이스의에서 데이터를 관리 하기 위한 대부분의 관계형 데이터베이스에서 사용 되는 언어입니다. 데이터를 검색 하 고, 업데이트 하 고 만들고 수정 하 고 데이터베이스 테이블을 관리 하도록 하는 명령이 포함 됩니다. SQL (예: WebMatrix에서 사용 하는 것) 프로그래밍 언어와 다르면 sql 개념은 원하는 데이터베이스에 알립니다 하 고 데이터베이스의 작업 데이터를 가져오거나 작업을 수행 하는 방법을 알아보세요. 다음은 몇 가지 SQL 명령의 예로 및 용도입니다.
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 이 인출는 *Id*, *이름*, 및 *가격* 의 레코드에서 열은 *제품* 경우 테이블의 값 *가격* 10을 초과 하면 이며 결과의 값에 따라 알파벳 순서로 반환 된 *이름* 열입니다. 이 명령은 일치 하는 레코드가 없는 경우, 조건을 또는 빈 집합을 충족 하는 레코드를 포함 하는 결과 집합을 반환 합니다.
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> 에 새 레코드를 삽입는 *제품* 설정 테이블에서 *이름* 열을 &quot;크 라 상&quot;, *설명* 열&quot; 잘 끊어지는 기쁨&quot;, 1.99에 가격입니다.
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> 이 명령은에서 레코드를 삭제는 *제품* 테이블 열이 있는 만료 날짜는 2008 년 1 월 1 일 보다 이전입니다. (있다고 가정은 *제품* 테이블에 이러한 열이 물론.) MM/DD/YYYY 형식으로 날짜를 여기서 입력 하지만 로캘에 사용 되는 형식으로 입력 해야 합니다.
> 
> `Insert Into` 및 `Delete` 명령 결과 집합을 반환 하지 않습니다. 대신, 이러한 명령에 의해 영향을 받은 레코드 수를 알려 주는 숫자를 반환 합니다.
> 
> 이러한 작업 (예: 레코드 삽입 및 삭제)의 일부에 대 한 작업을 요청 하는 프로세스는 데이터베이스에 대 한 적절 한 권한이 있습니다. 이 인해 프로덕션 데이터베이스는 데이터베이스에 연결할 때 사용자 이름 및 암호를 제공 해야 합니다.
> 
> SQL 명령의 수십 있지만 이와 같은 패턴을 따릅니다. SQL 명령을 사용 하 여 테이블을 만들고 데이터베이스, 테이블에서 레코드의 수를 계산, 가격을 계산 보다 많은 작업을 수행할 수 있습니다.


## <a name="inserting-data-in-a-database"></a>데이터베이스에 데이터 삽입

이 섹션에서는 사용자가 새 제품을 추가할 수 있는 페이지를 만드는 방법을 보여 줍니다.는 *제품* 데이터베이스 테이블입니다. 새 제품 레코드를 삽입 한 후 페이지에 표시 됩니다 사용 하 여 업데이트 된 테이블의 *ListProducts.cshtml* 이전 섹션에서 만든 페이지입니다.

사용자가 입력 한 데이터는 데이터베이스에 대 한 유효한 지 확인 하려면 유효성 검사를 포함 하는 페이지입니다. 예를 들어 코드 페이지에서를 통해 필요한 모든 열에 대해 입력 된 값.

1. 웹 사이트에서 라는 새 CSHTML 파일을 만들어 *InsertProducts.cshtml*합니다.
2. 기존 태그를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    페이지 본문 이름, 설명 및 가격을 입력할 수 있도록 하는 세 가지 텍스트 상자를 사용 하 여 HTML 폼을 포함 합니다. 사용자가 클릭 하면는 **삽입** 단추, 페이지 맨 위에 있는 코드에 대 한 연결 열립니다는 *SmallBakery.sdf* 데이터베이스입니다. 사용자가 사용 하 여 전송 하는 값을 가져온 후의 `Request` 개체를 로컬 변수에 해당 값을 할당 합니다.

    필요한 각 열에 대 한 사용자 값을 입력 했는지 확인을 위해 등록할 각 `<input>` 유효성을 검사 하려는 요소:

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    `Validation` 도우미 각에 등록 한 필드에 값이 있는지 확인 합니다. 모든 필드를 확인 하 여 유효성 검사를 통과 했는지 여부를 테스트할 수 있습니다 `Validation.IsValid()`이며 일반적으로 수행한 사용자에 게 서 얻은 정보를 처리 하기 전에:

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    (의 `&&` 연산자 의미 AND-이 테스트는 *양식을 제출 하 여 이며 모든 필드가 유효성 검사를 통과 한 경우*.)

    모든 열의 유효성을 검사 하는 경우 (none 비어 있던), 계속 진행 하 고 데이터를 삽입 한 후 다음 표시 된 것 처럼 실행 하는 SQL 문을 만듭니다.

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    삽입할 값을 매개 변수 자리 표시자 포함 (`@0`, `@1`, `@2`).

    > [!NOTE]
    > 보안을 위해 항상 값을 전달할 매개 변수를 사용 하 여 SQL 문을 앞의 예제에 표시 합니다. 이렇게 하면 사용자의 데이터 유효성을 검사할 수 있을 뿐 아니라 데이터베이스 (SQL 삽입 공격 이라고 함)에 악의적인 명령이 보내려는 시도 방지는 데 도움이 됩니다.

    쿼리를 실행 하려면이 문을 사용의 자리 표시자를 대체할 값을 포함 하는 변수를 전달 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    후의 `Insert Into` 문이 실행,이 줄을 사용 하 여 제품을 나열 하는 페이지에는 사용자에 게 보냅니다.

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    유효성 검사에 성공 하지 않은 삽입을 건너뜁니다. 누적 된 오류 메시지 (있는 경우)를 표시할 수 있는 페이지에는 도우미를가 하는 대신,

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    태그에 스타일 블록 라는 CSS 클래스 정의 포함 되도록 공지 `.validation-summary-errors`합니다. 이 대해 기본적으로 사용 되는 CSS 클래스의 이름이 `<div>` 유효성 검사 오류가 포함 된 요소입니다. 유효성 검사 요약 오류 빨간색으로 표시 되 고 굵게 표시 된, 있지만 정의할 수 있습니다는 CSS 클래스 지정 하는 경우에 `.validation-summary-errors` 클래스를 원하는 서식을 표시 합니다.

### <a name="testing-the-insert-page"></a>삽입 페이지를 테스트합니다.

1. 브라우저에서 페이지를 표시 합니다. 페이지에는 다음 그림에 나와 있는 것과 유사한 양식을 표시 합니다.

    ![[image]](5-working-with-data/_static/image5.jpg)
2. 모든 열에 대 한 값을 입력 합니다. 하지만 남겨 두어야는 *가격* 열은 비워 합니다.
3. **삽입**을 클릭합니다. 다음 그림에 나와 있는 것 처럼 페이지는 오류 메시지를 표시 합니다. (새 레코드가 생성 됩니다.)

    ![[image]](5-working-with-data/_static/image6.jpg)
4. 완전히 양식을 작성 하 고 클릭 **삽입**합니다. 이 이번에는 *ListProducts.cshtml* 페이지가 표시 되 고 새 레코드를 표시 합니다.

## <a name="updating-data-in-a-database"></a>데이터베이스의 데이터 업데이트

데이터를 테이블에을 입력 한 후 업데이트 해야 합니다. 이 절차에서는 이전에 데이터 삽입을 위해 만든 것과 비슷한 두 개의 페이지를 만드는 방법을 보여 줍니다. 첫 번째 페이지 제품을 표시 하 고 사용자가 변경 하려면 하나를 선택할 수 있습니다. 두 번째 페이지에는 사용자가 실제로 편집 하 고 저장할 수 있습니다.

> [!NOTE] 
> 
> **중요 한** 프로덕션 웹 사이트의 하면 일반적으로 제한할 수 있는 사용자는 데이터를 변경 하는 합니다. 멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자를 인증 하는 방법에 대 한 정보를 참조 하십시오. [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.


1. 웹 사이트에서 라는 새 CSHTML 파일을 만들어 *EditProducts.cshtml*합니다.
2. 파일에서 기존 태그를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    이 페이지 간의 유일한 차이점 및 *ListProducts.cshtml* 페이지에서 이전 버전은이 페이지의 HTML 테이블 포함 하는 별도 열을 표시 하는 **편집** 링크 합니다. 이 링크를 클릭 하면에 걸리는 *UpdateProducts.cshtml* 페이지 (다음 만들게) 선택된 된 레코드를 편집할 수 있습니다.

    만드는 코드는 **편집** 링크:

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    이렇게 하면 HTML 만들어집니다 `<a>` 요소 인 `href` 특성은 동적으로 설정 합니다. `href` 특성 링크를 클릭할 때 표시할 페이지를 지정 합니다. 또한 전달 된 `Id` 링크에는 현재 행의 값입니다. 페이지를 실행 하는 경우 페이지 소스 이와 같은 링크를 포함할 수 있습니다.

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    다음에 유의 `href` 특성이로 설정 된 `UpdateProducts/n`여기서 *n* 제품입니다. 사용자가이 링크 중 하나를 클릭 하면 결과 URL 다음과 같이 표시 됩니다.

    `http://localhost:18816/UpdateProducts/6`

    즉, 제품 번호를 편집할 수는 URL에 전달 됩니다.
3. 브라우저에서 페이지를 표시 합니다. 페이지는 다음과 같은 형식으로 데이터를 표시합니다.

    ![[image]](5-working-with-data/_static/image7.jpg)

    다음으로, 사용자가 실제로 데이터를 업데이트할 수 있는 페이지를 만듭니다. 업데이트 페이지는 사용자가 입력 데이터 유효성 검사에 유효성 검사를 포함 합니다. 예를 들어 코드 페이지에서를 통해 필요한 모든 열에 대해 입력 된 값.
4. 웹 사이트에서 라는 새 CSHTML 파일을 만들어 *UpdateProducts.cshtml*합니다.
5. 파일에서 기존 태그를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    페이지의 본문에서 제품이 표시 되 고 사용자가 편집할 수 있는 HTML 폼을 포함 합니다. 표시할 제품을 가져오려면이 SQL 문을 사용할 수 있습니다.

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    그러면에 전달 되는 값과 일치 하는 ID를 가진 제품 선택은 `@0` 매개 변수입니다. (때문에 *Id* 기본 키 고 따라서 반드시 하나의 제품 레코드 현재까지 선택할 수 있습니다 이러한 방식으로, 고유 합니다.) 이를 전달 하는 ID 값을 가져올 `Select` 문을 다음 구문을 사용 하는 URL의 일부분으로 페이지에 전달 되는 값을 읽을 수 있습니다.

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    사용 제품 레코드를 실제로 페치 하려면는 `QuerySingle` 메서드 포함 된 단일 레코드를 반환 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    에 단일 행이 반환 되는 `row` 변수입니다. 각 열에서 데이터를 가져올 수 있고 다음과 같이 지역 변수에 할당 됩니다.

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    폼에 대 한 태그에서 이러한 값 표시 됩니다 자동으로 개별 텍스트 상자에 다음과 같은 포함 된 코드를 사용 하 여:

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    코드의 해당 부분 업데이트 될 제품 레코드를 표시 합니다. 레코드가 표시 된 사용자 개별 열 편집할 수 있습니다.

    사용자가 클릭 하 여 폼을 제출할 때는 **업데이트** 단추를 코드에는 `if(IsPost)` 블록이 실행 됩니다. 사용자의 값을 가져옵니다이 `Request` 개체를 변수에서 값을 저장 하 고 각 열 채워져 있는지 유효성을 검사 합니다. 유효성 검사에 통과 하는 경우 코드를 다음 SQL Update 문을 만듭니다.

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    SQL에서 `Update` 업데이트를 설정 하려면 값과 각 열을 지정 문입니다. 이 코드에서는 값 매개 변수 자리 표시자를 사용 하 여 지정 된 `@0`, `@1`, `@2`등입니다. (보안을 위해 앞에서 설명한 것 처럼 항상 값을 전달 해야 SQL 문에 매개 변수를 사용 하 여.)

    호출 하는 경우는 `db.Execute` SQL 문의 매개 변수에 해당 하는 순서로 값이 포함 된 변수를 전달할 메서드를:

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    후의 `Update` 문이 실행 된 사용자 편집 페이지를 다시 리디렉션합니다 하기 위해 다음 메서드를 호출 합니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    사용자 데이터베이스에 있는 데이터의 업데이트 된 프로그램 목록에 게 표시 하 고 다른 제품을 편집할 수 됩니다.
6. 페이지를 저장합니다.
7. 실행 된 *EditProducts.cshtml* 페이지 (업데이트 페이지 제외)을 클릭 한 다음 **편집** 편집할 제품을 선택 합니다. *UpdateProducts.cshtml* 선택한 레코드를 보여 주는 페이지가 표시 됩니다.

    ![[image]](5-working-with-data/_static/image8.jpg)
8. 클릭 하 여 변경한 **업데이트**합니다. 업데이트 된 데이터와 제품 목록은 다시 표시 됩니다.

## <a name="deleting-data-in-a-database"></a>데이터베이스의 데이터를 삭제합니다.

이 섹션에서는 사용자가 제품에서 삭제 하는 방법을 보여 줍니다.는 *제품* 데이터베이스 테이블입니다. 이 예제는 두 페이지로 구성 됩니다. 첫 번째 페이지에서 사용자는 삭제할 레코드를 선택 합니다. 삭제할 레코드는 레코드를 삭제할 것인지 확인 수 있는 두 번째 페이지에 표시 됩니다.

> [!NOTE] 
> 
> **중요 한** 프로덕션 웹 사이트의 하면 일반적으로 제한할 수 있는 사용자는 데이터를 변경 하는 합니다. 멤버 자격을 설정 하는 방법에 대 한 사이트에서 작업을 수행 하는 사용자 권한을 부여 하는 방법에 대 한 정보를 참조 하십시오. [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904)합니다.


1. 웹 사이트에서 라는 새 CSHTML 파일을 만들어 *ListProductsForDelete.cshtml*합니다.
2. 기존 태그를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    이 페이지는 비슷합니다는 *EditProducts.cshtml* 앞에서 페이지. 그러나 표시 하는 대신는 **편집** 링크 각 제품에 대 한 표시는 **삭제** 링크 합니다. **삭제** 링크가 포함된 된 다음 코드를 사용 하 여 태그에 작성 됩니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    사용자가 링크를 클릭할 때 다음과 같은 URL을 만듭니다.

    `http://<server>/DeleteProduct/4`

    라는 페이지를 호출 하는 URL *DeleteProduct.cshtml* (만들게 다음)를 삭제 하는 제품의 ID를 전달 하 고 (여기서 4).
3. 파일을 저장 하지만 열어 둡니다.
4. 명명 된 다른 CHTML 파일을 만들 *DeleteProduct.cshtml*합니다. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    이 페이지에서 호출 됩니다 *ListProductsForDelete.cshtml* 제품 삭제를 확인 하는 사용자가 있습니다. 삭제 될 제품을 나열 하려면 ID를 가져옵니다는 제품의 URL에서 삭제 하려면 다음 코드를 사용 하 여:

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    다음 페이지 실제로 레코드를 삭제 하는 단추를 클릭 하 여 사용자에 게 요청 합니다. 이 중요 한 보안 조치: 업데이트 또는 삭제 데이터 같은 웹 사이트의 중요 한 작업을 수행할 때는 이러한 작업 수행 항상 GET 작업 아님 POST 작업을 사용 합니다. GET 작업을 사용 하 여 삭제 작업을 수행할 수 있도록 사이트는 설치 하 고, 경우에 같은 URL을 전달할 수 누구나 `http://<server>/DeleteProduct/4` 하 고 원하는 모든 항목을 데이터베이스에서 삭제 합니다. 확인을 추가 하 고 POST를 사용 하 여 삭제를 수행할 수 있도록 페이지를 코딩 하 여 사이트에 보안을 유지할을 추가 합니다.

    실제 삭제 작업은 먼저 확인 하는 post 작업 인지 하 고 ID 비어 있지 하는 다음 코드를 사용 하 여 수행 됩니다.

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    코드에 지정된 된 레코드를 삭제 하 고 다음 사용자 목록 페이지를 다시 리디렉션합니다 하는 SQL 문을 실행 합니다.
5. 실행 *ListProductsForDelete.cshtml* 브라우저에서 합니다.

    ![[image]](5-working-with-data/_static/image9.jpg)
6. 클릭는 **삭제** 제품 중 하나에 대 한 링크입니다. *DeleteProduct.cshtml* 해당 레코드를 삭제 하도록 확인 페이지가 표시 됩니다.
7. 클릭는 **삭제** 단추입니다. 제품 레코드가 삭제 되 고 업데이트 된 제품 목록과 함께 페이지가 새로 고쳐집니다.

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>데이터베이스에 연결
> 
> 두 가지 방법으로 데이터베이스에 연결할 수 있습니다. 첫 번째 사용 하는 것의 `Database.Open` 메서드 및 데이터베이스 파일의 이름을 지정 하려면 (덜는 *.sdf* 확장):
> 
> `var db = Database.Open("SmallBakery");`
> 
> `Open` 메서드 가정 하는. *sdf* 파일은 웹 사이트의 *앱\_데이터* 폴더입니다. 이 폴더는 데이터를 보유를 위해 특별히 설계 되었습니다. 예를 들어 웹 사이트에 데이터를 읽고 쓰는 데 적절 한 권한을 보유 하 고 보안 조치로, WebMatrix 액세스가 허용 되지 않습니다 파일에이 폴더에서 합니다.
> 
> 두 번째 방법은 연결 문자열을 사용 하는 것입니다. 연결 문자열을 데이터베이스에 연결 하는 방법에 대 한 정보를 포함 합니다. 파일 경로 포함할 수 있습니다이 또는 사용자 이름 및 해당 서버에 연결 하는 데 암호와 함께 로컬 또는 원격 서버에 SQL Server 데이터베이스의 이름을 포함할 수 있습니다. (중앙에서 관리 되는 버전의 SQL Server에서 데이터를 유지 하는 경우와 같은 호스팅 공급자의 사이트에서 항상는 연결 문자열을 사용 하면 데이터베이스 연결 정보를 지정 합니다.)
> 
> WebMatrix에서 연결 문자열은 일반적으로 저장 이라는 XML 파일 *Web.config*합니다. 사용할 수 있습니다 이름에서 알 수 있듯이 *Web.config* 사이트 필요할 수 있는 모든 연결 문자열을 포함 하 여 사이트의 구성 정보를 저장 하 여 웹 사이트의 루트에 파일입니다. 연결 문자열의 예는 *Web.config* 파일 다음과 같을 수 있습니다.
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> 예제에서는 연결 문자열의 임의 위치에 서버에서 실행 되는 SQL Server 인스턴스에서 데이터베이스를 가리키지만 (로컬 달리 *.sdf* 파일). 에 대 한 적절 한 이름으로 대체 해야 `myServer` 및 `myDatabase`, SQL Server 로그인 값을 지정 하 고 `username` 및 `password`합니다. (사용자 이름 및 암호 값이 다르면 반드시 동일한 호스팅 공급자가 제공한 서버에 로그인 하기 위한 값 또는 Windows 자격 증명으로 합니다. 관리자를 확인 해야 하는 정확한 값에 대 한.)
> 
> `Database.Open` 메서드는 데이터베이스의 이름을 전달할 수 있기 때문에 유연 하 고, *.sdf* 에 저장 된 연결 문자열의 이름 또는 파일의 *Web.config* 파일입니다. 다음 예제에서는 이전 예제에서 설명 하는 연결 문자열을 사용 하 여 데이터베이스에 연결 하는 방법을 보여 줍니다.
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> 에서 설명한 것 처럼는 `Database.Open` 메서드를 사용 하면 데이터베이스 이름 또는 연결 문자열을 전달 하 고 사용 하는 그림 합니다. 배포할 때이 매우 유용할 (게시) 웹 사이트입니다. 사용할 수는 *.sdf* 파일에 *앱\_데이터* 개발 하 고 사이트를 테스트 하는 경우 폴더입니다. 프로덕션 서버에 사이트를 이동 하면에서 연결 문자열을 사용할 수 있습니다는 *Web.config* 으로 동일한 이름을 가진 파일을 여 *.sdf* 했지만 해당 호스팅 공급자의 가리키는 &#8212;없이 코드를 변경 합니다.
> 
> 마지막으로, 연결 문자열을 직접 사용 하려는 경우를 호출할 수 있습니다는 `Database.OpenConnectionString` 메서드와 패스에 하나의 이름 대신 실제 연결 문자열이 하는 것은 *Web.config* 파일입니다. 이 몇 가지 이유로 없는 연결 문자열에 대 한 액세스 하는 경우에 유용할 수 있습니다 (또는,와 같은 값을 *.sdf* 파일 이름) 페이지가 실행 될 때까지 합니다. 그러나 대부분의 시나리오에 사용할 수 있습니다 `Database.Open` 이 문서에 설명 된 대로 합니다.


## <a name="additional-resources"></a>추가 자료

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [SQL Server 또는 WebMatrix의 MySQL 데이터베이스에 연결](https://go.microsoft.com/fwlink/?LinkId=208661)
- [ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)
