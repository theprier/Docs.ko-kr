---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 체크 아웃 및 PayPal 사용 하 여 지불 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: e516bcccdecce72d4fa6c705b0227ce873429e3c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386671"
---
<a name="checkout-and-payment-with-paypal"></a>체크 아웃 및 PayPal 사용 하 여 지불
====================
[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 Wingtip Toys 샘플 응용 프로그램 사용자 권한 부여, 등록 및 PayPal을 사용 하 여 결제를 포함 하도록 수정 하는 방법을 설명 합니다. 에 로그인 한 사용자만 제품을 구매 하려면 권한 부여를 해야 합니다. 이미 ASP.NET 4.5 Web Forms 프로젝트 템플릿의 기본 제공 사용자 등록 기능을 포함 해야 하는 작업의 대부분 됩니다. PayPal Express 체크 아웃 기능을 추가 합니다. 이 자습서에서는 테스트 환경에 없는 실제 금액 전송 될 있도록 PayPal 개발자를 사용할입니다. 이 자습서의 끝 쇼핑 카트, 체크 아웃 단추를 클릭 하 고 PayPal 테스트 웹 사이트에 데이터를 전송에 추가할 제품을 선택 하 여 응용 프로그램을 테스트 합니다. PayPal 테스트 웹 사이트에서 전달 하 고 결제 정보를 확인 하 고 로컬 Wingtip Toys 샘플 응용 프로그램을 확인 하 고 구매를 완료로 돌아와서는 있습니다.

해당 주소 확장성 및 보안에는 온라인 쇼핑에 전문화 된 여러 숙련 된 타사 지급 처리 프로세서를 있습니다. ASP.NET 개발자는 이점은 하나의 쇼핑을 구현 하 고 솔루션을 구매 하기 전에 타사 지불 솔루션을 활용 하 여 고려해 야 합니다.

> [!NOTE] 
> 
> Wingtip Toys 샘플 응용 프로그램은 ASP.NET 웹 개발자에 게 특정 ASP.NET 개념 및 사용할 수 있는 기능을 표시 하도록 설계 되었습니다. 이 샘플 응용 프로그램 확장성 및 보안 관련 하 여 가능한 모든 상황에 최적화 되지 않았습니다.


## <a name="what-youll-learn"></a>학습할 내용:

- 폴더의 특정 페이지에 대 한 액세스를 제한 하는 방법.
- 익명 쇼핑 카트에서 알려진된 쇼핑 카트를 만드는 방법입니다.
- 프로젝트에 대 한 SSL을 사용 하도록 설정 하는 방법.
- OAuth 공급자 프로젝트에 추가 하는 방법.
- PayPal을 사용 하 여 PayPal 테스트 환경을 사용 하 여 제품을 구매 하는 방법.
- PayPal에서 세부 정보를 표시 하는 방법에 **DetailsView** 제어 합니다.
- PayPal에서 가져온 정보를 사용 하 여 Wingtip Toys 응용 프로그램의 데이터베이스를 업데이트 하는 방법입니다.

## <a name="adding-order-tracking"></a>주문 추적 추가

이 자습서에서는 사용자가 만든 순서에서 데이터를 추적 하는 두 개의 새 클래스를 만들어야 합니다. 클래스에서 배송 정보, 구매 합계 및 지불 확인에 대 한 데이터를 추적 합니다.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Order 및 OrderDetail 모델 클래스 추가

이 자습서 시리즈의 앞부분에 나오는 범주, 제품에 대 한 스키마를 정의 하 고 쇼핑 카트에 항목을 만들어 합니다 `Category`, `Product`, 및 `CartItem` 클래스에 *모델* 폴더. 이제 제품 주문 및 주문 세부 정보에 대 한 스키마를 정의 하는 두 개의 새 클래스가 추가 됩니다.

1. 에 **모델** 폴더를 라는 새 클래스 추가 *Order.cs*합니다.   
   새 클래스 파일을 편집기에 표시 됩니다.
2. 기본 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. 추가 *OrderDetail.cs* 클래스는 *모델* 폴더입니다.
4. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

합니다 `Order` 및 `OrderDetail` 클래스 구매 및 전달에 사용 되는 주문 정보를 정의 하는 스키마를 포함 합니다.

또한 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 데이터베이스 컨텍스트 클래스를 업데이트 해야 합니다. 이렇게 하려면 새로 생성된 된 주문을 추가 하 고 `OrderDetail` 모델 클래스를 `ProductContext` 클래스입니다.

1. **솔루션 탐색기**찾기 및 열기, 합니다 *ProductContext.cs* 파일입니다.
2. 강조 표시 된 코드를 추가 합니다 *ProductContext.cs* 아래와 같이 파일:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

이 자습서 시리즈의 코드에서 이전에 설명한 것 처럼 합니다 *ProductContext.cs* 파일 추가 `System.Data.Entity` 네임 스페이스 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 합니다. 이 기능은 쿼리, 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 하는 기능을 포함 합니다. 위의 코드는 `ProductContext` 하 고 새로 추가한 Entity Framework 액세스를 추가 하는 클래스 `Order` 및 `OrderDetail` 클래스입니다.

## <a name="adding-checkout-access"></a>체크 아웃 액세스 추가

Wingtip Toys 샘플 응용 프로그램에서는 익명 사용자가 검토 하 고 쇼핑 카트에 제품을 추가 합니다. 그러나 익명 사용자 들이 하 고 쇼핑 카트에 추가 제품 구매를 선택 해야에 로그온 할 사이트입니다. 이러한 로그온 한 후 체크 아웃을 처리 하 고 프로세스를 구입 하는 웹 응용 프로그램의 제한 된 페이지에 액세스할 수 있습니다. 이러한 제한 된 페이지에 포함 된 합니다 *체크 아웃* 응용 프로그램의 폴더입니다.

### <a name="add-a-checkout-folder-and-pages"></a>체크 아웃 폴더 및 페이지 추가

이제 만들려는 합니다 *체크 아웃* 폴더 및 체크 아웃 프로세스 중에 고객에 게 표시 되는 것의 페이지입니다. 이 자습서의 뒷부분에서 이러한 페이지를 업데이트 합니다.

1. 프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**Wingtip Toys**)에서 **솔루션 탐색기** 선택한 **에 새 폴더 추가**합니다. 

    ![체크 아웃 및 PayPal-새 폴더를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image1.png)
2. 새 폴더의 이름을 *체크 아웃*합니다.
3. 마우스 오른쪽 단추로 클릭 합니다 *체크 아웃* 한 다음 선택한 폴더 **추가**-&gt;**새 항목**합니다. 

    ![체크 아웃 및 PayPal-새 항목을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image2.png)
4. **새 항목 추가** 대화 상자가 표시됩니다.
5. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 그런 다음, 가운데 창에서 선택 **마스터 페이지를 사용 하 여 Web Form**하 고 이름을 *CheckoutStart.aspx*합니다. 

    ![체크 아웃 및 지불 PayPal-를 사용 하 여 새 항목 추가 대화 상자](checkout-and-payment-with-paypal/_static/image3.png)
6. 이전과 마찬가지로 선택 합니다 *Site.Master* 마스터 페이지 파일입니다.
7. 다음 추가 페이지를 추가 합니다 *체크 아웃* 위와 동일한 단계를 사용 하 여 폴더:   

    - CheckoutReview.aspx
    - CheckoutComplete.aspx
    - CheckoutCancel.aspx
    - CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>Web.config 파일 추가

새로 추가 하 여 *Web.config* 파일을 합니다 *체크 아웃* 폴더에 포함 된 모든 페이지에 액세스를 제한할 수 있는 폴더입니다.

1. 마우스 오른쪽 단추로 클릭 합니다 *체크 아웃* 선택한 폴더 **추가**  - &gt; **새 항목**합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 그런 다음, 가운데 창에서 선택 **웹 구성 파일**의 기본 이름을 그대로 *Web.config*를 선택한 후 **추가**합니다.
3. 기존 XML 콘텐츠를 대체 합니다 *Web.config* 다음 파일:  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. 저장 된 *Web.config* 파일입니다.

*Web.config* 파일에는 웹 응용 프로그램의 모든 알 수 없는 사용자에 포함 된 페이지에 대 한 액세스를 거부 해야 지정 합니다 *체크 아웃* 폴더입니다. 그러나 사용자가 계정을 등록 하 고 로그온을 하는 경우 이러한 알려진된 사용자 되며 페이지에 액세스 해야 합니다 *체크 아웃* 폴더입니다.

ASP.NET 구성 계층 구조를 따르는지 확인 해야 여기서 각 *Web.config* 파일이 있는 폴더와 그 아래 자식 디렉터리의 모든 구성 설정을 적용 합니다.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>프로젝트에 대 한 SSL을 사용 하도록 설정

 Secure Sockets Layer (SSL)는 웹 서버 및 웹 클라이언트가 암호화를 사용 하 여 더 안전 하 게 통신할 수 있도록 정의 된 프로토콜입니다. SSL을 사용 하지 않으면 클라이언트와 서버 간에 전송 되는 데이터 패킷 스니핑 네트워크에 대 한 물리적 액세스를 사용 하 여 모든 사용자에 열려 있습니다. 또한 몇 가지 일반적인 인증 체계 보호 되지 않습니다 일반 HTTP를 통해. 특히 기본 인증 및 폼 인증은 암호화 되지 않은 자격 증명을 보냅니다. 보안 되도록 이러한 인증 체계는 SSL을 사용 해야 합니다. 

1. **솔루션 탐색기**를 클릭 합니다 **WingtipToys** 프로젝트를 선택한 다음 키를 누릅니다 **F4** 표시할를 **속성** 창입니다.
2. 변경 **SSL 사용** 에 `true`입니다.
3. 복사 합니다 **SSL URL** 나중에 사용할 수 있도록 합니다.   
 SSL url `https://localhost:44300/` 않으면 이전에 만든 SSL 웹 사이트 (아래와 같이).   
    ![프로젝트 속성](checkout-and-payment-with-paypal/_static/image4.png)
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **WingtipToys** 프로젝트 및 클릭 **속성**합니다.
5. 왼쪽된 탭에서 클릭 **웹**합니다.
6. 변경 된 **프로젝트 Url** 사용 하는 **SSL URL** 이전에 저장 합니다.   
    ![프로젝트 웹 속성](checkout-and-payment-with-paypal/_static/image5.png)
7. 키를 눌러 페이지를 저장할 **CTRL + S**입니다.
8. **Ctrl+F5**를 눌러 응용 프로그램을 실행합니다. Visual Studio에서 SSL 경고를 방지할 수 있도록 하는 옵션을 표시 합니다.
9. 클릭 **예** IIS Express SSL 인증서를 신뢰 하 여 계속 합니다.   
    ![IIS Express SSL 인증서 세부 정보](checkout-and-payment-with-paypal/_static/image6.png)  
 보안 경고가 표시 됩니다.
10. 클릭 **예** 에 localhost 인증서를 설치 합니다.   
    ![보안 경고 대화 상자](checkout-and-payment-with-paypal/_static/image7.png)  
 브라우저 창이 표시 됩니다.

이제 로컬로 SSL을 사용 하 여 웹 응용 프로그램 쉽게 테스트할 수 있습니다.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>OAuth 2.0 공급자 추가

ASP.NET Web Forms는 멤버 자격 및 인증에 대 한 향상 된 옵션을 제공 합니다. 이러한 향상 된이 기능 OAuth가 포함 됩니다. OAuth는 웹, 모바일 및 데스크톱 응용 프로그램에서 간단한 표준 메서드로 보안 권한 부여를 허용 하는 개방형 프로토콜입니다. ASP.NET Web Forms 템플릿을 OAuth를 사용 하 여 Facebook, Twitter, Google 및 Microsoft를 인증 공급자로 표시. 이 자습서에서는 인증 공급자로 Google만 사용, 있지만 공급자 중 하나를 사용 하는 코드를 쉽게 수정할 수 있습니다. 다른 공급자를 구현 하는 단계는이 자습서에서 단계와 매우 비슷합니다.

인증을 하는 것 외에도 자습서 권한 부여를 구현 하려면 역할도 사용 됩니다. 에 추가한 사용자만의 `canEdit` 역할 데이터를 변경할 수 있게 됩니다 (만들기, 편집 또는 연락처 삭제).

> [!NOTE] 
> 
> Windows Live 응용 프로그램 작업 웹 사이트에 대 한 라이브 URL에만 동의 로그인 테스트를 위해 로컬 웹 사이트 URL을 사용할 수 없습니다.


다음 단계를 사용 하면 Google 인증 공급자를 추가할 수 있습니다.

1. 엽니다는 *앱\_Start\Startup.Auth.cs* 파일입니다.
2. 주석 문자를 제거 합니다 `app.UseGoogleAuthentication()` 메서드도 표시 되는 메서드를 다음과 같이 나타나도록 합니다. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. 로 이동 합니다 [Google 개발자 콘솔](https://console.developers.google.com/)합니다. Google 개발자 메일 계정 (gmail.com)으로 로그인을 해야 합니다. Google 계정이 없으면 선택 합니다 **계정을 만들** 링크 합니다.   
   다음으로 보면 합니다 **Google 개발자 콘솔**합니다.   
    ![Google 개발자 콘솔](checkout-and-payment-with-paypal/_static/image8.png)
4. 클릭 합니다 **프로젝트 만들기** 단추 및 프로젝트 이름 및 ID (기본 값을 사용할 수 있음)를 입력 합니다. 클릭 합니다 **계약 확인란** 및 **만들기** 단추입니다.  

    ![Google-새 프로젝트](checkout-and-payment-with-paypal/_static/image9.png)

   몇 초 안에 새 프로젝트 생성 및 브라우저에 새 프로젝트 페이지가 표시 됩니다.
5. 왼쪽된 탭에서 클릭 **Api &amp; auth**를 클릭 하 고 **자격 증명**합니다.
6. 클릭 합니다 **새 클라이언트 ID 만들기** 아래에서 **OAuth**합니다.   
   합니다 **클라이언트 ID 만들기** 대화 상자가 표시 됩니다.   
    ![Google-클라이언트 ID 만들기](checkout-and-payment-with-paypal/_static/image10.png)
7. 에 **클라이언트 ID 만들기** 대화 상자에서 기본값을 그대로 **웹 응용 프로그램** 응용 프로그램 형식에 대 한 합니다.
8. 설정 합니다 **권한이 부여 된 JavaScript 원본** 이 자습서의 앞부분에서 사용한 SSL URL로 (`https://localhost:44300/` 다른 SSL 프로젝트를 만든 하지 않는 한).   
   이 URL은 응용 프로그램에 대 한 원본입니다. 이 샘플의 경우 localhost 테스트 URL만 입력할가 있습니다. 그러나 실제로 localhost 및 프로덕션 계정에 여러 개의 Url을 입력할 수 있습니다.
9. 설정 된 **Authorized Redirect URI** 다음과: 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   이 값은 URI는 ASP.NET OAuth 사용자가 google OAuth 서버와 통신할 수 있습니다. 위에서 사용 된 SSL URL을 기억 ( `https://localhost:44300/` 다른 SSL 프로젝트를 만든 하지 않는 한).
10. 클릭 합니다 **클라이언트 ID 만들기** 단추입니다.
11. Google 개발자 콘솔의 왼쪽된 메뉴에서를 클릭 합니다 **동의 화면** 메뉴 항목에 설정한 전자 메일 주소 및 제품 이름입니다. 양식을 완료 하면, 클릭 **저장할**합니다.
12. 클릭 합니다 **Api** 메뉴 항목, 아래로 스크롤하여를 클릭 합니다 **해제** 단추 옆에 **Google + API**합니다.   
    이 옵션을 수락 Google + API를 사용 하도록 설정 됩니다.
13. 업데이트 해야 합니다 **Microsoft.Owin** 버전 3.0.0으로 NuGet 패키지.   
    **도구** 메뉴에서 **NuGet 패키지 관리자** 선택한 후 **솔루션용 NuGet 패키지 관리**합니다.  
    **NuGet 패키지 관리** 창, 찾기 및 업데이트 합니다 **Microsoft.Owin** 버전 3.0.0으로 패키지 합니다.
14. Visual Studio에서 업데이트를 `UseGoogleAuthentication` 메서드를 *Startup.Auth.cs* 복사 및 붙여넣기 하 여 페이지를 **클라이언트 ID** 및 **클라이언트 암호** 메서드로 합니다. 합니다 **클라이언트 ID** 하 고 **클라이언트 비밀** 아래 표시 된 값은 샘플 및 작동 하지 것입니다. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. 키를 눌러 **ctrl+f5** 를 빌드하고 응용 프로그램을 실행 합니다. 클릭 합니다 **로그인** 링크 합니다.
16. 아래 **다른 서비스를 사용 하 여 로그인 할**, 클릭 **Google**합니다.  
    ![로그인](checkout-and-payment-with-paypal/_static/image11.png)
17. 자격 증명을 입력 해야 할 경우 자격 증명을 입력할 google 사이트로 리디렉션됩니다.  
    ![Google-로그인](checkout-and-payment-with-paypal/_static/image12.png)
18. 자격 증명을 입력 한 후 방금 만든 웹 응용 프로그램에 권한을 부여 하려면 묻는 메시지가 나타납니다.  
    ![프로젝트 기본 서비스 계정](checkout-and-payment-with-paypal/_static/image13.png)
19. 클릭 **수락**합니다. 이제 다시 이동 합니다는 **등록** 페이지의 **WingtipToys** Google 계정을 등록할 수 있는 응용 프로그램입니다.  
    ![Google 계정으로 등록](checkout-and-payment-with-paypal/_static/image14.png)
20. Gmail 계정에 사용 되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭 (즉, 인증에 사용할 하나)를 유지 하려는 합니다. 클릭 **로그인** 위와 같이 합니다.

### <a name="modifying-login-functionality"></a>로그인 기능 수정

이전에 설명한 것 처럼이 자습서 시리즈에서 대부분의 사용자 등록 기능에 포함 되어 ASP.NET Web Forms 템플릿에 기본적으로. 기본값을 수정 하는 이제 *Login.aspx* 하 고 *Register.aspx* 호출 하는 페이지는 `MigrateCart` 메서드. `MigrateCart` 메서드는 익명 쇼핑 카트를 사용 하 여 새로 로그인된 한 사용자를 연결 합니다. 사용자를 연결 하 고 쇼핑 카트, Wingtip Toys 샘플 응용 프로그램을 방문 하는 사용자의 쇼핑 카트를 유지할 수 됩니다.

1. **솔루션 탐색기**찾기 및 열기, 합니다 *계정* 폴더입니다.
2. 라는 코드 숨김 페이지를 수정 *Login.aspx.cs* 다음과 같이 표시 되도록 노란색으로 강조 표시 된 코드를 포함 하려면:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. 저장 된 *Login.aspx.cs* 파일입니다.

이제 경고에 대 한 정의가 없는 무시할 수 있습니다는 `MigrateCart` 메서드. 추가할 것이 자습서의 뒷부분에서 설명 합니다.

합니다 *Login.aspx.cs* 코드 숨김 파일은 로그인 메서드를 지원 합니다. 이 페이지에 "로그인" 단추가 표시 됩니다 Login.aspx 페이지를 검사 하 여 때 트리거를 클릭 합니다 `LogIn` 코드 숨김에 대 한 처리기입니다.

경우는 `Login` 메서드를 *Login.aspx.cs* 라고, 명명 된 장바구니의 새 인스턴스 `usersShoppingCart` 만들어집니다. 쇼핑 카트 (GUID)의 ID를 검색 하 고로 설정 된 `cartId` 변수입니다. 그런 다음, `MigrateCart` 모두 전달 메서드가 호출 되는 `cartId` 및이 방법에 로그인 한 사용자의 이름. 쇼핑 카트를 마이그레이션하면 익명 쇼핑 카트를 식별 하는 데 GUID 사용자 이름으로 대체 됩니다.

수정 하는 것 외에도 *Login.aspx.cs* 사용자가 로그인 할 때 쇼핑 카트를 마이그레이션하도록 코드 숨김 파일 수정 해야 합니다 *Register.aspx.cs 코드 숨김 파일* 쇼핑 카트를 마이그레이션하도록 때 사용자는 새 계정을 만듭니다 하 고 로그인 합니다.

1. 에 *계정* 폴더를 열고 코드 숨김 파일의 이름은 *Register.aspx.cs*합니다.
2. 다음과 같이 표시 되도록 노란색으로 코드를 포함 하 여 코드 숨김 파일을 수정 합니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. 저장 된 *Register.aspx.cs* 파일입니다. 다시 한 번에 대 한 경고를 무시 합니다 `MigrateCart` 메서드.

사용한 코드를 확인 합니다 `CreateUser_Click` 이벤트 처리기는에서 사용 되는 코드와 매우 비슷합니다는 `LogIn` 메서드. 사용자를 등록 하거나 사이트에 대 한 호출에서 로그를 `MigrateCart` 메서드 됩니다.

## <a name="migrating-the-shopping-cart"></a>장바구니 마이그레이션

사용 하 여 쇼핑 카트를 마이그레이션하도록 코드를 추가할 수는 로그인 및 등록 프로세스를 업데이트 했으므로 `MigrateCart` 메서드.

1. **솔루션 탐색기**, 찾을 합니다 *논리* 폴더를 *ShoppingCartActions.cs* 클래스 파일입니다.
2. 기존 코드에 노란색으로 강조 표시 하는 코드를 추가 합니다 *ShoppingCartActions.cs* 파일인 있도록의 코드를 *ShoppingCartActions.cs* 파일이 다음과 같이 표시 됩니다:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart` 메서드 기존 cartId를 사용 하 여 사용자의 쇼핑 카트를 찾습니다. 코드 쇼핑 카트에 항목을 모두 반복 하 고 대체 하는 다음으로 `CartId` 속성 (지정 된 대로 `CartItem` 스키마)에서 로그인 한 사용자 이름을 사용 하 여.

### <a name="updating-the-database-connection"></a>데이터베이스 연결 업데이트

이 자습서를 사용 하 여 수행 하는 경우는 **미리 빌드된** Wingtip Toys 샘플 응용 프로그램을 기본 멤버 자격 데이터베이스를 다시 만들어야 합니다. 기본 연결 문자열을 수정 하 여 멤버 자격 데이터베이스 응용 프로그램을 실행한 다음에 만들어집니다.

1. 엽니다는 *Web.config* 프로젝트의 루트에 있는 파일입니다.
2. 다음과 같이 표시 되도록 기본 연결 문자열을 업데이트 합니다.   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>PayPal 통합

PayPal는 온라인 merchants에서 지불을 수락 하는 웹 기반 청구 플랫폼. 이 자습서에는 다음 PayPal의 체크 아웃 Express 기능을 응용 프로그램에 통합 하는 방법을 설명 합니다. 빠른 체크 아웃 PayPal 해당 쇼핑 카트에 추가한 항목에 대 한 요금을 지불 하는 데 사용할 수가 있습니다.

### <a name="create-paylpal-test-accounts"></a>PaylPal 테스트 계정 만들기

테스트 환경 PayPal을 사용 하려면 만들고 해야 개발자 테스트 계정을 확인 합니다. 테스트 실행 계정 및 판매자 테스트 구매자를 만들려면 개발자 테스트 계정을 사용 합니다. 또한 개발자 테스트 계정 자격 증명을 Wingtip Toys 샘플 응용 프로그램을 PayPal 테스트 환경에 액세스할 수 있습니다.

1. 브라우저에서 사이트를 테스트 하는 PayPal 개발자로 이동 합니다.   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. PayPal 개발자 계정이 없다면 새 계정을 클릭 하 여 만들 **등록**등록 단계를 수행 하 고 있습니다. 기존 PayPal 개발자 계정이 있는 경우 클릭 하 여 로그인 **로그인**합니다. PayPal 개발자 계정의이 자습서의 뒷부분에 나오는 Wingtip Toys 샘플 응용 프로그램을 테스트 해야 합니다.
3. PayPal 개발자 계정에 대 한 등록만, PayPal 사용 하 여 PayPal 개발자 계정을 확인 해야 합니다. PayPal 전자 메일 계정으로 전송 하는 단계를 수행 하 여 계정을 확인할 수 있습니다. PayPal 개발자 계정에 확인 한 후 다시 로그인 PayPal 개발자 사이트를 테스트 합니다.
4. 이미 없다면 PayPal buyer 테스트 계정을 만들 필요가 PayPal 개발자 계정을 사용 하 여 PayPal 개발자 사이트에 로그인 후 하나 있습니다. PayPal 사이트 클릭 buyer 테스트 계정을 만들려면 합니다 **응용 프로그램** 탭을 클릭 한 다음 **샌드박스 계정**합니다.   
 합니다 **샌드박스 테스트 계정** 페이지가 표시 됩니다.   

    > [!NOTE] 
    > 
    > PayPal 개발자 사이트에는 이미 판매자 테스트 계정을 제공합니다.

    ![체크 아웃 및 PayPal-샌드박스 테스트 계정 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image15.png)
5. 샌드박스 테스트 계정 페이지에서 클릭 **계정 만들기**합니다.
6. 에 **테스트 계정 만들기** 페이지 테스트 계정 전자 메일 및 암호를 구매자를 선택 합니다.   

    > [!NOTE] 
    > 
    > Buyer 전자 메일 주소 및 암호를이 자습서의 끝에 Wingtip Toys 샘플 응용 프로그램을 테스트 해야 합니다.

    ![체크 아웃 및 PayPal-샌드박스 테스트 계정 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image16.png)
7. 클릭 하 여 buyer 테스트 계정을 만들 합니다 **계정 만들기** 단추입니다.  
 합니다 **샌드박스 테스트 계정** 페이지가 표시 됩니다. 

    ![체크 아웃 및 PayPal-PaylPal 계정 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image17.png)
8. 에 **샌드박스 테스트 계정** 페이지를 클릭 합니다 **진행자** 전자 메일 계정.  
    **프로필** 하 고 **알림** 옵션이 나타납니다.
9. 선택 된 **프로필** 옵션을 선택한 다음 클릭 **API 자격 증명이** 판매자 테스트 계정에 대 한 API 자격 증명을 보려면.
10. 테스트 API 자격 증명이 메모장에 복사 합니다.

테스트 환경 PayPal 표시 클래식 API 테스트 자격 증명 (사용자 이름, 암호 및 서명) Wingtip Toys 샘플 응용 프로그램에서 API 호출을 해야 합니다. 다음 단계에서는 자격 증명을 추가 합니다.

### <a name="add-paypal-class-and-api-credentials"></a>PayPal 클래스 및 API 자격 증명 추가

PayPal 코드의 대부분 단일 클래스에 배치 됩니다. 이 클래스는 PayPal을 사용 하 여 통신에 사용 된 메서드를 포함 합니다. 또한이 클래스는 PayPal 자격 증명을 추가 합니다.

1. Visual Studio 내에서 Wingtip Toys 샘플 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다 **논리** 한 다음 선택한 폴더 **추가**  - &gt; **새 항목**합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 아래 **Visual C#** 에서 합니다 **설치 됨** 창 왼쪽에서 선택 **코드**합니다.
3. 가운데 창에서 선택 **클래스**합니다. 이 새 클래스 이름을 **PayPalFunctions.cs**합니다.
4. **추가**를 클릭합니다.  
   새 클래스 파일을 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 가맹점 API는 자격 증명 (사용자 이름, 암호 및 서명) PayPal 테스트 환경에 함수 호출을 만들 수 있도록이 자습서의 앞부분에서 표시를 추가 합니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 이 샘플 응용 프로그램에서 C# 파일 (.cs)를 자격 증명을 간단히 추가 됩니다. 그러나 구현 된 솔루션에서는 구성 파일에서 자격 증명을 암호화 고려해 야 합니다.


NVPAPICaller 클래스 PayPal 기능의 대부분을 포함합니다. 클래스의 코드는 테스트 PayPal 테스트 환경에서 구매를 확인 하는 데 필요한 메서드를 제공 합니다. 다음 세 가지 PayPal 함수를 구매 하는 데 사용 됩니다.

- `SetExpressCheckout` 함수
- `GetExpressCheckoutDetails` 함수
- `DoExpressCheckoutPayment` 함수

합니다 `ShortcutExpressCheckout` 장바구니와 호출 테스트 구매 정보 및 제품 세부 정보를 수집 하는 메서드는 `SetExpressCheckout` PayPal 함수입니다. 합니다 `GetCheckoutDetails` 메서드 호출 및 구매 정보를 확인 합니다 `GetExpressCheckoutDetails` 테스트 구매 하기 전에 PayPal 함수입니다. 합니다 `DoCheckoutPayment` 메서드를 호출 하 여 테스트 환경에서 테스트 구매를 완료 합니다 `DoExpressCheckoutPayment` PayPal 함수입니다. 나머지 코드는 PayPal 메서드와 같은 문자열 인코딩, 디코딩 문자열, 배열 처리 및 자격 증명 확인 프로세스를 지원 합니다.

> [!NOTE] 
> 
> PayPal을 사용 하면 기준으로 선택적 구매 세부 정보를 포함할 수 있습니다 [PayPal의 API 사양](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)합니다. Wingtip Toys 샘플 응용 프로그램의 코드를 확장 하 여 다른 많은 선택적 필드 뿐만 아니라 지역화 세부 정보, 제품 설명, 세금, 고객 서비스 숫자를 포함할 수 있습니다.


반환 하 고 취소 Url에 지정 된 된 **ShortcutExpressCheckout** 메서드 포트 번호를 사용 합니다.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

일반적으로 Visual Web Developer에서 SSL을 사용 하 여 웹 프로젝트를 실행 하는 경우 포트 44300 웹 서버에 사용 됩니다. 위에 표시 된 것과 같이 포트 번호가 44300입니다. 응용 프로그램을 실행 하는 경우 다른 포트 번호를 볼 수 있습니다. 올바르게 설정할 코드에서 수행할 수 있도록 성공 하기 위해 포트 번호 요구 사항이이 자습서의 끝에 Wingtip Toys 샘플 응용 프로그램을 실행 합니다. 이 자습서의 다음 섹션에는 로컬 호스트 포트 번호를 검색 하 여 PayPal 클래스를 업데이트 하는 방법을 설명 합니다.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>PayPal 클래스에 LocalHost 포트 번호를 업데이트 합니다.

Wingtip Toys 샘플 응용 프로그램 PayPal 테스트 사이트로 이동 하 고 Wingtip Toys 샘플 응용 프로그램의 로컬 인스턴스를 반환 하 여 제품을 구입 합니다. 로컬로 실행 하는 포트 번호를 지정 해야 올바른 URL을 반환 하는 PayPal을 가지려면 위에서 언급 한 PayPal 코드에서 응용 프로그램 예제입니다.

1. 프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**WingtipToys**)에서 **솔루션 탐색기** 선택한 **속성**합니다.
2. 왼쪽된 열에서 선택 합니다 **웹** 탭 합니다.
3. 포트 번호를 검색 합니다 **프로젝트 Url** 상자입니다.
4. 필요한 경우 업데이트를 `returnURL` 하 고 `cancelURL` PayPal 클래스에서 (`NVPAPICaller`)에 *PayPalFunctions.cs* 웹 응용 프로그램의 포트 번호를 사용 하는 파일:   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

이제 추가한 코드는 로컬 웹 응용 프로그램에 대 한 예상 된 포트를 일치 합니다. PayPal 로컬 컴퓨터에 올바른 URL을 반환 하는 일을 할 수 있습니다.

### <a name="add-the-paypal-checkout-button"></a>PayPal 체크 아웃 단추를 추가 합니다.

샘플 응용 프로그램에 추가 된 기본 PayPal 함수는 했으므로 이러한 함수를 호출 하는 데 필요한 코드 및 태그 추가 시작할 수 있습니다. 첫째, 사용자는 쇼핑 카트 페이지에 표시 되는 체크 아웃 단추를 추가 해야 합니다.

1. 엽니다는 *ShoppingCart.aspx* 파일입니다.
2. 파일의 아래쪽으로 스크롤하여 찾을 `<!--Checkout Placeholder -->` 주석입니다.
3. 주석을 사용 하 여는 `ImageButton` 마크업은 다음과 같은 대체를 제어 합니다.  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. 에 *ShoppingCart.aspx.cs* 파일을 후 합니다 `UpdateBtn_Click` 파일의 끝 부분에 대 한 이벤트 처리기 추가 `CheckOutBtn_Click` 이벤트 처리기:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 또한를 *ShoppingCart.aspx.cs* 파일에 대 한 참조를 추가 합니다는 `CheckoutBtn`새 이미지 단추는 다음과 같이 참조 되도록 합니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 변경 내용을 모두 저장 합니다 *ShoppingCart.aspx* 파일 및 *ShoppingCart.aspx.cs* 파일입니다.
7. 메뉴에서 선택 **디버깅할**-&gt;**빌드 WingtipToys**합니다.  
   프로젝트를 다시 작성 됩니다 새로 추가 된 **ImageButton** 제어 합니다.

### <a name="send-purchase-details-to-paypal"></a>PayPal 구매 정보 보내기

클릭할 때 합니다 **체크 아웃** 쇼핑 카트 페이지에서 단추 (*ShoppingCart.aspx*), 구매 프로세스 시작 됩니다. 다음 코드는 제품을 구매 하는 데 필요한 첫 번째 PayPal 함수를 호출 합니다.

1. *체크 아웃* 폴더를 열고 코드 숨김 파일의 이름은 *CheckoutStart.aspx.cs*합니다.   
   코드 숨김 파일을 열고 해야 합니다.
2. 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

응용 프로그램의 사용자가 클릭할 때 합니다 **체크 아웃** 쇼핑 카트 페이지 브라우저에서 단추 이동 합니다 *CheckoutStart.aspx* 페이지. 경우는 *CheckoutStart.aspx* 로드 페이지는 `ShortcutExpressCheckout` 메서드가 호출 됩니다. 이 시점에서 사용자는 PayPal 테스트 웹 사이트로 전송 됩니다. PayPal 사이트에서 사용자 PayPal 자격 증명을 입력, 구매 정보를 검토, PayPal 계약에 동의 및 Wingtip Toys 샘플 응용 프로그램에 반환 합니다. 여기서는 `ShortcutExpressCheckout` 메서드가 완료 되 면 합니다. 경우는 `ShortcutExpressCheckout` 메서드가 완료 되 면 사용자를 리디렉션할 수는 *CheckoutReview.aspx* 에 지정 된 페이지는 `ShortcutExpressCheckout` 메서드. 이 Wingtip Toys 샘플 응용 프로그램 내에서 주문 세부 정보를 검토할 수 있습니다.

### <a name="review-order-details"></a>주문 세부 정보 검토

PayPal에서 반환 된 후의 *CheckoutReview.aspx* Wingtip Toys 샘플 응용 프로그램의 페이지에 주문 세부 정보가 표시 됩니다. 이 페이지에서는 사용자가 제품을 구입 하기 전에 주문 세부 정보를 검토 합니다. 합니다 *CheckoutReview.aspx* 페이지를 다음과 같이 만들 수 있어야 합니다.

1. 에 *체크 아웃* 폴더를 열고 페이지 라는 *CheckoutReview.aspx*합니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. 라는 코드 숨김 페이지를 엽니다 *CheckoutReview.aspx.cs* 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

합니다 **DetailsView** PayPal에서 반환 된 주문 세부 정보를 표시할 컨트롤을 사용 합니다. 위의 코드도 Wingtip Toys 데이터베이스에 주문 세부 정보를 저장 하는 또한는 `OrderDetail` 개체입니다. 사용자가 클릭할 때 합니다 **Complete Order** 리디렉션됩니다 단추를 *CheckoutComplete.aspx* 페이지.

> [!NOTE] 
> 
> **팁**
> 
> 태그에는 *CheckoutReview.aspx* 페이지에서 `<ItemStyle>` 태그에서 항목의 스타일을 변경 하는 합니다 **DetailsView** 페이지 하단에 있는 컨트롤. 페이지를 확인 하 여 **디자인 뷰** (선택 하 여 **디자인** Visual Studio의 왼쪽된 아래 모서리에), 다음을 선택 하는 **DetailsView** 컨트롤을 선택 합니다  **스마트 태그** (맨 위에 있는 화살표 아이콘 컨트롤의 오른쪽)를 볼 수는 **DetailsView 작업**합니다.
> 
> ![체크 아웃 및 지불 PayPal-를 사용 하 여 필드를 편집](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 선택 하 여 **필드 편집**서 **필드** 대화 상자가 표시 됩니다. 이 대화 상자에서 쉽게 제어할 수 있습니다 시각적 속성을 같은 **ItemStyle**의 합니다 **DetailsView** 제어 합니다.
> 
> ![체크 아웃 및 PayPal-필드 대화 상자를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image19.png)


### <a name="complete-purchase"></a>구매를 완료 합니다.

*CheckoutComplete.aspx* 페이지 PayPal에서 구매를 만듭니다. 사용자 클릭 해야 위에서 설명 했 듯이 합니다 **Complete Order** 응용 프로그램으로 이동 하기 전에 단추를 *CheckoutComplete.aspx* 페이지입니다.

1. 에 *체크 아웃* 폴더를 열고 페이지 라는 *CheckoutComplete.aspx*합니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. 라는 코드 숨김 페이지를 엽니다 *CheckoutComplete.aspx.cs* 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

경우는 *CheckoutComplete.aspx* 페이지가 로드 되는 `DoCheckoutPayment` 메서드가 호출 됩니다. 앞서 언급 했 듯이 `DoCheckoutPayment` 메서드 PayPal 테스트 환경에서 구매를 완료 합니다. PayPal 구매 주문을 완료 되 면 합니다 *CheckoutComplete.aspx* 지불 트랜잭션을 표시 하는 페이지 `ID` 구매자 합니다.

### <a name="handle-cancel-purchase"></a>구매 취소를 처리 합니다.

사용자를 구매를 취소 하기로 한 경우 리디렉션됩니다에 *CheckoutCancel.aspx* 페이지는 표시 순서 취소 되었습니다.

1. 라는 페이지를 엽니다 *CheckoutCancel.aspx* 에 *체크 아웃* 폴더입니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>구매 오류 처리

오류 구매 과정에서 처리 되는 합니다 *CheckoutError.aspx* 페이지입니다. 코드 숨김 합니다 *CheckoutStart.aspx* 페이지를 *CheckoutReview.aspx* 페이지 및 *CheckoutComplete.aspx* 페이지 각 리디렉션됩니다는  *CheckoutError.aspx* 페이지 오류가 발생 하는 경우.

1. 라는 페이지를 엽니다 *CheckoutError.aspx* 에 *체크 아웃* 폴더입니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

합니다 *CheckoutError.aspx* 체크 아웃 프로세스 중에 오류가 발생 하는 경우 오류 세부 정보를 사용 하 여 페이지가 표시 됩니다.

## <a name="running-the-application"></a>응용 프로그램 실행

제품을 구매 하는 방법은 응용 프로그램을 실행 합니다. 실행 된 PayPal에서 테스트 환경 note 합니다. 실제 미지불 교환 되 고 있습니다.

1. Visual Studio에서 파일은 모든 했는지 확인.
2. 웹 브라우저를 열고 이동할 [ https://developer.paypal.com ](https://developer.paypal.com/)합니다.
3. 이 자습서의 앞부분에서 만든 PayPal 개발자 계정으로 로그인 합니다.  
   PayPal의 개발자 sandbox에 로그인 할 필요가 [ https://developer.paypal.com ](https://developer.paypal.com/) express 체크 아웃을 테스트 합니다. 이 테스트, PayPal의 라이브 환경 필요가 PayPal의 샌드박스에 적용 됩니다.
4. Visual Studio에서 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
   브라우저를 열고 표시 데이터베이스 다시 작성 후 합니다 *Default.aspx* 페이지입니다.
5. "자동차"와 같은 제품 범주를 선택한 다음 클릭 하 여 다양 한 제품이 쇼핑 카트에 추가 **카트에 추가** 각 제품 옆에 있습니다.  
   쇼핑 카트는 선택한 제품을 표시 됩니다.
6. 클릭 합니다 **PayPal** 체크 아웃 하는 단추입니다. 

    ![체크 아웃 및 PayPal-카트를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image20.png)

   체크 아웃 해야 Wingtip Toys 샘플 응용 프로그램에 대 한 사용자 계정이 있다고 합니다.
7. 클릭 합니다 **Google** 기존 gmail.com 전자 메일 계정으로 로그인 페이지의 오른쪽에 링크 합니다.  
   Gmail.com 계정이 없는 경우에 테스트용 하나를 만들 수 있습니다 [www.gmail.com](https://www.gmail.com/)합니다. 또한 "등록"을 클릭 하 여 표준 로컬 계정을 사용할 수 있습니다. 

    ![체크 아웃 및 지불 PayPal-를 사용 하 여 로그인](checkout-and-payment-with-paypal/_static/image21.png)
8. Gmail 계정 및 암호를 로그인 합니다. 

    ![체크 아웃 및 PayPal-Gmail 로그인을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image22.png)
9. 클릭 합니다 **로그인** Wingtip Toys 샘플 응용 프로그램 사용자 이름에 gmail 계정을 등록 하는 단추입니다. 

    ![체크 아웃 및 PayPal-등록 계정 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal 테스트 사이트에서 추가 프로그램 **buyer** 전자 메일 주소 및이 자습서의 앞부분에서 만든 암호를 클릭 합니다 **로그인** 단추입니다. 

    ![체크 아웃 및 PayPal-PayPal 로그인을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image24.png)
11. PayPal 정책에 동의 하 고 클릭 합니다 **동의 함 및 계속** 단추입니다.  
    이 페이지는만 보면이 PayPal 계정을 사용 하 여 처음으로 표시 합니다. 이것은 테스트 계정에 실제 미지불 교환 note 다시 합니다. 

    ![체크 아웃 및 PayPal-PayPal 정책을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image25.png)
12. 테스트 환경 검토 페이지 및 클릭 PayPal에서 주문 정보를 검토할 **계속**합니다. 

    ![체크 아웃 및 PayPal-검토 정보를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image26.png)
13. 에 *CheckoutReview.aspx* 페이지에서 주문 금액을 확인 하 고 생성 된 배송 주소를 확인 합니다. 클릭 합니다 **Complete Order** 단추입니다. 

    ![체크 아웃 및 PayPal-순서 검토를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image27.png)
14. 합니다 **CheckoutComplete.aspx** 페이지는 지불 트랜잭션 id 

    ![체크 아웃 및 PayPal-전체 체크 아웃을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>데이터베이스를 검토합니다.

응용 프로그램을 실행 한 후 Wingtip Toys 샘플 응용 프로그램 데이터베이스의 업데이트 된 데이터를 검토 하 여 응용 프로그램에 성공적으로 제품의 구매 기록 볼 수 있습니다.

포함 된 데이터를 검사할 수 있습니다 합니다 *Wingtiptoys.mdf* 사용 하 여 데이터베이스 파일을 **데이터베이스 탐색기** 창 (**서버 탐색기** Visual Studio의 창) 수행한 것 처럼 이 자습서 시리즈의 앞부분에 나오는.

1. 열려 있는 경우 브라우저 창을 닫습니다.
2. Visual Studio에서 선택 합니다 **모든 파일 표시** 맨 위에 있는 아이콘 **솔루션 탐색기** 확장할 수 있도록 합니다 **앱\_데이터** 폴더입니다.
3. 확장 된 **앱\_데이터** 폴더입니다.  
 선택 해야 합니다 **모든 파일 표시** 폴더에 대 한 아이콘입니다.
4. 마우스 오른쪽 단추로 클릭 합니다 *Wingtiptoys.mdf* 데이터베이스 파일 및 선택 **오픈**합니다.  
    **서버 탐색기** 표시 됩니다.
5. 확장 된 **테이블** 폴더입니다.
6. 마우스 오른쪽 단추로 클릭 합니다 **주문을**선택한 테이블 **테이블 데이터 표시**합니다.  
 합니다 **주문** 테이블이 표시 됩니다.
7. 검토 합니다 **PaymentTransactionID** 성공적인 트랜잭션을 확인 하는 열입니다. 

    ![체크 아웃 및 PayPal-검토 데이터베이스를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image29.png)
8. 닫기 합니다 **주문** 테이블 창입니다.
9. 서버 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **OrderDetails** 선택한 테이블 **테이블 데이터 표시**합니다.
10. 검토를 `OrderId` 하 고 `Username` 값을 **OrderDetails** 테이블입니다. 이러한 값과 일치 하는 참고 합니다 `OrderId` 및 `Username` 에 포함 된 값을 **주문** 테이블.
11. 닫기 합니다 **OrderDetails** 테이블 창입니다.
12. Wingtip Toys 데이터베이스 파일을 마우스 오른쪽 단추로 클릭 (*Wingtiptoys.mdf*)을 선택 하 고 **근접 연결**합니다.
13. 표시 되지 않으면 합니다 **솔루션 탐색기** 창 클릭 **솔루션 탐색기** 맨 아래에 **서버 탐색기** 표시할 창은 **솔루션 탐색기**  다시 합니다.

## <a name="summary"></a>요약

이 자습서에서는 제품 구매를 추적 하는 주문과 주문 세부 정보 스키마를 추가 합니다. 또한 Wingtip Toys 샘플 응용 프로그램에 PayPal 기능을 통합 합니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 구성 개요](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 Azure App Service에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>고지 사항

이 자습서는 샘플 코드를 포함합니다. 이러한 샘플 코드는 어떤 종류의 보증 없이 "있는 그대로" 제공 됩니다. 따라서 Microsoft는 정확도, 무결성 또는 샘플 코드의 품질을 보장 하지 않습니다. 샘플 코드를 사용 하 여 사용자의 책임에 동의 합니다. 어떠한 상황는 Microsoft 지지를 어떤 방식으로 모든 샘플 코드의 경우 콘텐츠를 포함 하지만 여기에 오류나 누락 모든 샘플 코드, 콘텐츠, 손실 또는 모든 샘플 코드 사용으로 인해 발생 한 모든 종류의 손해에 제한 되지 않습니다. 이로써 알림이 표시 됩니다 및 배상, 저장 하며 Microsoft에서 모든 손실, 손실, 부상 또는 손상 종류 비롯, 제한 없이 여 occasioned 또는 자료를 게시 하면는에서 발생 하는 클레임에 대 한 동의 통지가 수행 전송에서 사용 하거나 여기 견해에 국한 되지 않음 등을 사용 합니다.

> [!div class="step-by-step"]
> [이전](shopping-cart.md)
> [다음](membership-and-administration.md)
