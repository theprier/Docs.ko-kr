---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: '6 부: ASP.NET 멤버 자격 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 6 부 ASP.NET 멤버 자격을 추가합니다.
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: 303c1edf548db1da9ef61d94bdd8157d6afbb2e4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804422"
---
<a name="part-6-aspnet-membership"></a>6 부: ASP.NET 멤버 자격
====================
[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다. 해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 6 부 ASP.NET 멤버 자격을 추가합니다.


## <a id="_Toc260221672"></a>  ASP.NET 멤버 자격 사용

![](tailspin-spyworks-part-6/_static/image1.png)

보안을 클릭 합니다.

![](tailspin-spyworks-part-6/_static/image1.jpg)

폼 인증 사용 한다고 있는지 확인 합니다.

![](tailspin-spyworks-part-6/_static/image2.jpg)

"Create User" 링크를 사용 하 여 몇 명의 사용자를 만듭니다.

![](tailspin-spyworks-part-6/_static/image3.jpg)

을 완료 한 후 솔루션 탐색기 창을 참조 및 보기를 새로 고칩니다.

![](tailspin-spyworks-part-6/_static/image2.png)

ASPNETDB를 합니다. MDF 세밀 하 게 작성 되었습니다. 이 파일을 사용 하면 멤버 자격 등 ASP.NET 핵심 서비스를 지원 하기 위해 표가 있습니다.

이제 체크 아웃 프로세스의 구현을 시작할 수 있습니다.

CheckOut.aspx 페이지를 만들어 시작 합니다.

CheckOut.aspx 페이지는 로그인 된 사용자 및 로그인 페이지에 로그인 하지 않은 사용자 리디렉션에 대 한 액세스 제한 됩니다 있도록 로그인 사용자를 사용할 수만 있어야 합니다.

이렇게 하려면 다음 web.config 파일의 구성 섹션을 추가 했습니다.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

ASP.NET Web Forms 응용 프로그램에 대 한 템플릿을 자동으로 인증 섹션을 web.config 파일에 추가 하 고 기본 로그인 페이지를 설정 합니다.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

에서는 Login.aspx 코드 숨김 사용자가 로그인 할 때 익명 장바구니 마이그레이션 파일을 수정 해야 합니다. 페이지 변경\_다음과 같이 이벤트를 로드 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

세션 이름을 새로 로그인된 한 사용자로 설정 하 고 MyShoppingCart 클래스에서 MigrateCart 메서드를 호출 하 여 사용자의 장바구니에 임시 세션 id를 변경 하기 위해 다음과 같은 "LoggedIn" 이벤트 처리기를 추가 하십시오. (.Cs 파일에서 구현 됨)

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

MigrateCart() 메서드 구현에는 다음과 같이 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

Checkout.aspx에서는 사용 하 여 한 EntityDataSource 및 GridView는 확인 페이지에서 당사의 쇼핑 카트 페이지에서 수행한 것 만큼 합니다.

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

GridView 제어권 MyList 이라는 "ondatabound" 이벤트 처리기를 지정\_RowDataBound 다음과 같이 해당 이벤트 처리기를 구현 해 보겠습니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

실행 중인 총 쇼핑 카트에 각 행은 바인딩되고 GridView의 맨 아래 행을 업데이트 하는 대로이 메서드가 유지 합니다.

이 단계에 배치 하려면 "review" 표시를 구현 했습니다.

보겠습니다 페이지로 코드 몇 줄을 추가 하 여 빈 카트 시나리오를 처리할\_Load 이벤트:

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

사용자가 "제출" 단추를 클릭할 때 제출 단추 클릭 이벤트 처리기에서 다음 코드를 실행 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

주문 제출 프로세스의 "핵심" SubmitOrder() 메서드의 MyShoppingCart 클래스에서 구현 될 것입니다.

SubmitOrder 작업이 수행 됩니다.

- 시장 바구니에 모든 품목을 가져와 새 주문 레코드를 만들고 연관된 된 OrderDetails 레코드를 사용 합니다.
- 배송 날짜를 계산 합니다.
- 쇼핑 카트를 지웁니다.


[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

이 샘플 응용 프로그램의 목적에 대 한 현재 날짜에 2 일을 추가 하기만 하면 운송 날짜를 계산 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

이제 응용 프로그램을 실행 시작부터 끝까지 쇼핑 프로세스 테스트를 허용 합니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-5.md)
> [다음](tailspin-spyworks-part-7.md)
