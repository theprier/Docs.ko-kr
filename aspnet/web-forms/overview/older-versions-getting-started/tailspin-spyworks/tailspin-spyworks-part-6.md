---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: '6 단계: ASP.NET 멤버 자격 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 6 부 ASP.NET 멤버 자격을 추가합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: 83e9bc780ea8face3e0f55fdf8c00e13b60f80a7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886812"
---
<a name="part-6-aspnet-membership"></a>6 단계: ASP.NET 멤버 자격
====================
으로 [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대해 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 매우 간단한는 하는 방법을 보여 줍니다. Off 쇼핑, 체크 아웃, 및 관리를 포함 하 여 온라인 상점에서는 만들려는 ASP.NET 4에서 멋진 새로운 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 6 부 ASP.NET 멤버 자격을 추가합니다.


## <a id="_Toc260221672"></a>  ASP.NET 멤버 자격 작업

![](tailspin-spyworks-part-6/_static/image1.png)

보안을 클릭 합니다.

![](tailspin-spyworks-part-6/_static/image1.jpg)

폼 인증 사용 하는 것이 있는지 확인 합니다.

![](tailspin-spyworks-part-6/_static/image2.jpg)

"Create User" 링크를 사용 하 여 몇 가지 사용자를 만듭니다.

![](tailspin-spyworks-part-6/_static/image3.jpg)

을 완료 한 후 솔루션 탐색기 창을 보기를 새로 고칩니다.

![](tailspin-spyworks-part-6/_static/image2.png)

ASPNETDB 합니다. MDF 세밀 하 게 생성 되었습니다. 이 파일에는 멤버와 같은 핵심 ASP.NET 서비스를 지원 하기 위해 테이블이 들어 있습니다.

이제 구현 하면 결제 과정을 시작할 수 있습니다.

CheckOut.aspx 페이지를 만들어 시작 합니다.

만 사용할 수 있으므로 로그인 한 사용자와 로그인 페이지에 로그인 하지 않은 리디렉션 사용자 액세스를 제한 합니다 우리 로그인 사용자에 게 CheckOut.aspx 페이지 여야 합니다.

이렇게 하려면 우리의 web.config 파일의 구성 섹션에 다음을 추가 합니다.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

자동으로 ASP.NET Web Forms 응용 프로그램에 대 한 서식 파일 우리의 web.config 파일에 인증 하는 섹션을 추가 하 고 기본 로그인 페이지를 설정 합니다.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

म Login.aspx 코드 숨김 마이그레이션할 익명 쇼핑 카트는 사용자가 로그인 하는 경우 파일을 수정 해야 합니다. 페이지 변경\_다음과 같이 이벤트를 로드 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

그런 다음 새로 로그인된 한 사용자를 세션 이름을 설정 하거나 MyShoppingCart 클래스에서 MigrateCart 메서드를 호출 하 여 하는 사용자의 쇼핑 카트에 임시 세션 id를 변경 하려면 다음과 같이 "LoggedIn" 이벤트 처리기를 추가 합니다. (.Cs 파일에서 구현)

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

MigrateCart() 메서드 구현에는 다음과 같이 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

Checkout.aspx 사용는 EntityDataSource 및는 GridView 우리의 체크 아웃 페이지에서에서 당사의 쇼핑 카트 페이지에서 수행한 것 처럼 합니다.

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

GridView 제어권 MyList 이라는 "ondatabound" 이벤트 처리기 지정\_RowDataBound 이제 다음과 같이 해당 이벤트 처리기를 구현 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

각 행은 바인딩되며 GridView의 맨 아래 행을 업데이트 하는 대로 누계는 쇼핑 카트를 유지 하는 메서드.

이 단계에서 배치할 주문의 "검토" 프레젠테이션을 구현 했습니다.

보겠습니다 가격 페이지에 몇 줄의 코드를 추가 하 여 빈 카트 시나리오를 처리할\_Load 이벤트:

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

사용자가 "제출" 단추를 클릭할 제출 단추 클릭 이벤트 처리기에서 다음 코드를 실행 하면 했습니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

주문 제출 프로세스의 "핵심" SubmitOrder() 방식의 MyShoppingCart 클래스에서 구현 하는 것입니다.

SubmitOrder을 수행합니다.

- 시장 바구니에는 모든 품목을 가져와서 새 주문 레코드와 연관된 된 OrderDetails 레코드를 만드는 데 사용할 합니다.
- 배송 날짜를 계산 합니다.
- 쇼핑 카트 선택을 취소 합니다.


[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

이 샘플 응용 프로그램의 목적에 대 한 배송 날짜 하기만 하면 현재 날짜에 2 일을 추가 하 여 계산 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

응용 프로그램을 지금 실행 처음부터 끝까지 쇼핑 프로세스 테스트를 허용 합니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-5.md)
> [다음](tailspin-spyworks-part-7.md)
