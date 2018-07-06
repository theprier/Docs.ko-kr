---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 라우팅 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: aspnetcontent
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 968517100275822071e2101a4cfb978320f222f2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822719"
---
<a name="url-routing"></a>URL 라우팅
====================
[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 Wingtip Toys 샘플 응용 프로그램 URL 라우팅을 지원 하도록 수정 합니다. 라우팅 친숙 한, 기억 하기 쉽고 검색 엔진에서 더 잘 지원 되는 Url을 사용 하도록 웹 응용 프로그램을 사용 하도록 설정 합니다. 이 자습서는 이전 자습서 "멤버 자격 및 관리" 빌드하고 Wingtip Toys 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습할 내용:

- ASP.NET Web Forms 응용 프로그램에 대 한 경로 등록 하는 방법입니다.
- 웹 페이지에 경로 추가 하는 방법입니다.
- 경로 지원 하기 위해 데이터베이스에서 데이터를 선택 하는 방법입니다.

## <a name="aspnet-routing-overview"></a>ASP.NET 라우팅 개요

적용할 응용 프로그램을 구성할 수 있습니다 URL 라우팅 물리적 파일에 매핑되지 않는 Url을 요청 합니다. 요청 URL은 사용자가 웹 사이트에서 페이지를 찾으려면 브라우저에 입력 URL 하기만 하면 됩니다. 사용자에 게 의미 있는 의미 체계는 및 검색 엔진 최적화 (SEO)를 사용 하 여 도움이 되는 Url을 정의 하 라우팅을 사용 합니다.

기본적으로 Web Forms 템플릿에 포함 됩니다 [ASP.NET Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)합니다. 사용 하 여 구현 될 기본 라우팅 작업의 상당 *친화적 Url*합니다. 그러나이 자습서에서는 사용자 지정된 라우팅 기능을 추가 합니다.

URL 라우팅 사용자 지정 하기 전에 Wingtip Toys 샘플 응용 프로그램은 다음 URL을 사용 하 여 제품에 연결할 수 있습니다.:

`https://localhost:44300/ProductDetails.aspx?productID=2`

URL 라우팅 사용자 지정 하 여 Wingtip Toys 샘플 응용 프로그램 URL 읽기 쉬운를 사용 하 여 동일한 제품에 연결 합니다.

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>경로

경로 처리기에 매핑되는 URL 패턴입니다. 처리기는 Web Forms 응용 프로그램의.aspx 파일 등의 물리적 파일을 수 있습니다. 처리기가 요청을 처리 하는 클래스를 수도 있습니다. 경로 정의 하려면 URL 패턴, 처리기 및 필요에 따라 경로 대 한 이름을 지정 하 여 경로 클래스의 인스턴스를 만듭니다.

응용 프로그램에 추가 하 여 경로 추가 합니다 `Route` 개체를 정적 `Routes` 의 속성은 `RouteTable` 클래스입니다. 경로 속성을 `RouteCollection` 응용 프로그램에 대 한 모든 경로 저장 하는 개체입니다.

### <a name="url-patterns"></a>URL 패턴

URL 패턴을 리터럴 값 및 변수 자리 표시자 (URL 매개 변수 라고도 함)를 포함할 수 있습니다. 슬래시 기호로 구분 된 URL의 세그먼트에 있는 리터럴 및 자리 표시자 (`/`) 문자입니다.

에 웹 응용 프로그램에 요청이 수행 될 때에 URL 세그먼트 및 자리 표시자로 구문 분석 되 고 변수 값을 요청 처리기에 제공 됩니다. 이 프로세스는 쿼리 문자열의 데이터를 구문 분석 되 고 요청 처리기에 전달 하는 방법은 비슷합니다. 두 경우 모두 변수 정보가 URL에 포함 되며 키-값 쌍의 형태로 처리기에 전달 합니다. 쿼리 문자열에 대 한 키와 값을 URL에 있습니다. 경로 대 한 키는 URL 패턴에 정의 된 자리 표시자 이름 및 값만 URL에 있습니다.

URL 패턴을 괄호로 묶어 자리 표시자를 정의 ( `{` 고 `}` ). 세그먼트에 둘 이상의 자리 표시자를 정의할 수 있지만 자리 표시자를 리터럴 값으로 구분 되어야 합니다. 예를 들어 `{language}-{country}/{action}` 유효한 경로 패턴입니다. 그러나 `{language}{country}/{action}` 없는 리터럴 값 또는 자리 표시자 사이 구분 기호 이므로 올바른 패턴이 아닙니다. 따라서 라우팅 국가 자리 표시자에 대 한 값에서 언어 자리 표시자 값을 구분 하는 위치를 확인할 수 없습니다.

### <a name="mapping-and-registering-routes"></a>매핑 및 경로 등록 합니다.

Wingtip Toys 샘플 응용 프로그램의 페이지에 대 한 경로 포함할 수 있는 응용 프로그램을 시작 하는 경우 경로 등록 해야 합니다. 경로 등록 하려면 수정 된 `Application_Start` 이벤트 처리기입니다.

1. **솔루션 탐색기**Visual Studio의 찾기 및 열기를 *Global.asax.cs* 파일입니다.
2. 노란색으로 강조 표시 된 코드를 추가 합니다 *Global.asax.cs* 다음과 같이 파일:   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

Wingtip Toys 샘플 응용 프로그램 시작 되 면 호출 하 여 `Application_Start` 이벤트 처리기입니다. 이 이벤트 처리기의 끝을 `RegisterCustomRoutes` 메서드가 호출 됩니다. `RegisterCustomRoutes` 메서드를 호출 하 여 각 경로 추가 합니다 `MapPageRoute` 메서드를 `RouteCollection` 개체입니다. 경로 경로 이름, 경로 URL 및 실제 URL을 사용 하 여 정의 됩니다.

첫 번째 매개 변수 ("`ProductsByCategoryRoute`")의 경로 이름입니다. 필요할 때 경로 호출 하는 것이 됩니다. 두 번째 매개 변수 ("`Category/{categoryName}`") 친숙 한 대체 코드를 기반으로 동적이 될 수 있는 URL을 정의 합니다. 데이터를 기반으로 생성 되는 링크를 사용 하 여 데이터 컨트롤을 채우는 경우에이 경로 사용 합니다. 경로 다음과 같이 표시 됩니다.

[!code-csharp[Main](url-routing/samples/sample2.cs)]

괄호로 지정 된 된 동적 값을 포함 하는 경로의 두 번째 매개 변수 (`{ }`). 이 경우에 `categoryName` 적절 한 라우팅 경로 확인 하는 데 사용할 수 있는 변수가 있습니다.

> [!NOTE] 
> 
> **선택 사항**
> 
> 쉽게 이동 하 여 코드를 관리할 찾을 수 있습니다는 `RegisterCustomRoutes` 메서드는 별도 클래스입니다. 에 *논리* 폴더를 별도 만들기 `RouteActions` 클래스입니다. 위의 이동 `RegisterCustomRoutes` 메서드를 *Global.asax.cs* 파일을 새 `RoutesActions` 클래스입니다. 사용 합니다 `RoleActions` 클래스 및 `createAdmin` 메서드를 호출 하는 방법의 예로 `RegisterCustomRoutes` 메서드에서 *Global.asax.cs* 파일입니다.


알 수도 수 있습니다는 `RegisterRoutes` 사용 하 여 메서드 호출을 `RouteConfig` 맨 앞에 개체를 `Application_Start` 이벤트 처리기입니다. 이 호출이 기본 라우팅을 구현 하기 위해 수행 됩니다. 이 Visual Studio Web Forms 템플릿을 사용 하 여 응용 프로그램을 만들 때 기본 코드로 포함 되었습니다.

## <a name="retrieving-and-using-route-data"></a>검색 및 경로 데이터를 사용 하 여

위에서 설명한 대로 경로 정의할 수 있습니다. 에 추가한 코드를 `Application_Start` 이벤트 처리기는 *Global.asax.cs* 파일 경로 정의할 수 있는 로드 합니다.

### <a name="setting-routes"></a>경로 설정

경로 사용 하면 추가 코드를 추가 해야 합니다. 이 자습서에서는 사용 하 여 모델 바인딩을 검색 하는 `RouteValueDictionary` 데이터 컨트롤에서 데이터를 사용 하 여 경로 생성할 때 사용 되는 개체입니다. `RouteValueDictionary` 개체는 특정 제품 범주에 속하는 제품 이름 목록이 포함 됩니다. 데이터 및 경로에 따른 각 제품에 대 한 링크가 만들어집니다.

#### <a name="enable-routes-for-categories-and-products"></a>범주 및 제품에 대 한 경로 사용 하도록 설정

다음으로 응용 프로그램을 사용 하 여 업데이트를 `ProductsByCategoryRoute` 포함할 각 제품 범주 링크에 대 한 올바른 경로를 결정 합니다. 도 업데이트 합니다 *ProductList.aspx* 라우트된 각 제품에 대 한 링크를 포함 하는 페이지입니다. 하지만 링크를 표시할 변경 되기 전의 링크는 이제 사용 하 여 URL 라우팅 합니다.

1. **솔루션 탐색기**오픈 합니다 *Site.Master* 열려 있지 않으면 페이지입니다.
2. 업데이트를 **ListView** 라는 컨트롤 "`categoryList`" 노란색으로 강조 표시를 변경 하므로 태그를 다음과 같이 나타납니다.   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. **솔루션 탐색기**오픈 합니다 *ProductList.aspx* 페이지입니다.
4. 업데이트를 `ItemTemplate` 의 요소를 *ProductList.aspx* 태그를 다음과 같이 표시 되도록 노란색으로 강조 표시 된 업데이트를 사용 하 여 페이지:   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. 코드 숨김을 엽니다 *ProductList.aspx.cs* 강조 표시 된 노란색으로 다음 네임 스페이스를 추가 합니다.  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. 대체는 `GetProducts` 코드 숨김의 메서드 (*ProductList.aspx.cs*) 다음 코드를 사용 하 여:   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>제품 세부 정보에 대 한 코드를 추가 합니다.

이제 관련 코드를 업데이트 (*ProductDetails.aspx.cs*)에 대 한 합니다 *ProductDetails.aspx* 경로 데이터를 사용 하는 페이지입니다. 새 `GetProduct` 메서드 또한 이전 비 친화적인, 라우팅되지 않은 URL을 사용 하는 경우 사용자의 책갈피 링크에 있는 쿼리 문자열 값을 허용 합니다.

1. 대체는 `GetProduct` 코드 숨김의 메서드 (*ProductDetails.aspx.cs*) 다음 코드를 사용 하 여:   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>응용 프로그램 실행

업데이트 된 경로 확인 하려면 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.
2. 클릭 합니다 **제품** 페이지의 맨 위에 있는 링크입니다.  
 모든 제품에 표시 되는 *ProductList.aspx* 페이지입니다. (포트 번호로 사용) 다음 URL은 브라우저에 표시 됩니다.  
    `https://localhost:44300/ProductList`
3. 다음을 클릭 합니다 **자동차** 페이지의 위쪽 범주 링크 합니다.  
 카만에 표시 되는 *ProductList.aspx* 페이지입니다. (포트 번호로 사용) 다음 URL은 브라우저에 표시 됩니다.  
    `https://localhost:44300/Category/Cars`
4. 페이지에 나열 된 첫 번째 자동차의 이름이 포함 된 링크를 클릭 ("**로 변환할 수 있는 자동차**") 제품 정보를 표시 합니다.  
 (포트 번호로 사용) 다음 URL은 브라우저에 표시 됩니다.  
    `https://localhost:44300/Product/Convertible%20Car`
5. 그런 다음 브라우저에 (포트 번호로 사용) 다음 라우팅되지 않은 URL을 입력:  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 코드는 여전히 사용자의 책갈피 링크에 있는 경우에 대 한 쿼리 문자열을 포함 하는 URL을 인식 합니다.

## <a name="summary"></a>요약

이 자습서에서는 범주 및 제품에 대 한 경로 추가 했습니다. 모델 바인딩을 사용 하는 데이터 컨트롤을 사용 하 여 경로 통합할 수 있습니다 하는 방법을 배웠습니다. 다음 자습서에서는 전역 오류 처리를 구현 합니다.

## <a name="additional-resources"></a>추가 리소스

[Asp.net Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 Azure App Service에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [이전](membership-and-administration.md)
> [다음](aspnet-error-handling.md)
