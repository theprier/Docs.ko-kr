---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 멤버 자격 및 관리 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: 166bc642ea2083f455be0648e424f0b0ae3b082c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="membership-and-administration"></a>멤버 자격 및 관리
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 사용자 지정 역할을 추가 하 고 ASP.NET Identity를 사용: Wingtip Toys 샘플 응용 프로그램을 업데이트 하는 방법을 보여 줍니다. 또한 한 관리 페이지를 사용자 지정 역할이 있는 사용자 추가 및 제거할 수 제품 웹 사이트에서 구현 하는 방법을 보여 줍니다.

[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md) ASP.NET 웹 응용 프로그램을 빌드하는 데 사용 되는 멤버 자격 시스템 이며 ASP.NET 4.5에서 사용할 수 있습니다. ASP.NET Id에 대 한 템플릿 뿐 아니라 Visual Studio 2013 Web Forms 프로젝트 템플릿을 [ASP.NET MVC](../../../../mvc/index.md), [ASP.NET Web API](../../../../web-api/index.md), 및 [ASP.NET 단일 페이지 응용 프로그램](../../../../single-page-application/index.md). 특히 빈 웹 응용 프로그램을 시작할 때 NuGet을 사용 하 여 ASP.NET Identity 시스템을 설치할 수 있습니다. 그러나이 자습서 시리즈 사용 하 여는 **Web Forms**projecttemplate ASP.NET Id 시스템을 포함 합니다. ASP.NET Id를 사용 하면 쉽게 응용 프로그램 데이터와 사용자 고유의 프로필 데이터를 통합할 수 있습니다. 또한 ASP.NET Identity을 사용 하면 응용 프로그램에서 사용자 프로필에 대 한 지 속성 모델을 선택할 수 있습니다. SQL Server 데이터베이스 또는 다른 데이터 저장소에 데이터를 저장할 수 포함 하 여 *NoSQL* Windows Azure 저장소 테이블 같은 데이터를 저장 합니다.

이 자습서에서는 이전 자습서 Wingtip Toys 자습서 시리즈의 "체크 아웃 및 결제 된 PayPal" 이라는 기반으로 합니다.

## <a name="what-youll-learn"></a>학습 내용:

- 코드를 사용 하 여 응용 프로그램에 사용자 지정 역할 및 사용자를 추가 하는 방법.
- 관리 폴더 및 페이지에 대 한 액세스를 제한 하는 방법.
- 사용자 지정 역할에 속하는 사용자에 대 한 탐색을 제공 하는 방법입니다.
- 채우는 모델 바인딩을 사용 하는 방법은 [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx) 제품 범주를 제어 합니다.
- 파일을 사용 하 여 웹 응용 프로그램에 업로드 하는 방법의 [파일 업로드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx) 제어 합니다.
- 유효성 검사 컨트롤을 사용 하 여 입력된 유효성 검사를 구현 하는 방법.
- 추가 하 고 응용 프로그램에서 제품을 제거 하는 방법.

## <a name="these-features-are-included-in-the-tutorial"></a>이러한 기능은 자습서에 포함 됩니다.

- ASP.NET ID
- 구성 및 권한 부여
- 모델 바인딩
- 비 가시적인 유효성 검사

ASP.NET Web Forms 멤버 자격 기능을 제공 합니다. 기본 템플릿을 사용 하면 응용 프로그램을 실행 하는 경우 즉시 사용할 수 있는 기본 제공 멤버 자격 기능을 사용할 수 있습니다. 이 자습서에서는 사용자 지정 역할을 추가 하 고 해당 역할에 사용자를 할당을 ASP.NET Identity를 사용 하는 방법을 보여 줍니다. 관리 폴더에 대 한 액세스를 제한 하는 방법에 설명 합니다. 사용자 지정 역할을 가진 사용자가 추가 제품을 제거 하 고 추가 된 후 제품을 미리 볼 수 있는 관리 폴더에는 페이지를 추가 합니다.

## <a name="adding-a-custom-role"></a>사용자 지정 역할 추가

ASP.NET Id를 사용 하 여 사용자 지정 역할을 추가한 코드를 사용 하 여 해당 역할에 사용자를 할당 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *논리* 폴더 및 새 클래스를 만듭니다.
2. 클래스의 새 이름을 *RoleActions.cs*합니다.
3. 다음과 같이 표시 되도록 코드를 수정 합니다.  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. **솔루션 탐색기**열고는 *Global.asax.cs* 파일입니다.
5. 수정 된 *Global.asax.cs* 다음과 같이 표시 되도록 노란색으로 강조 표시 하는 코드를 추가 하 여 파일:  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. 다음에 유의 `AddUserAndRole` 빨간색으로 밑줄이 그어져 있습니다. AddUserAndRole 코드를 두 번 클릭 합니다.  
   강조 표시 된 메서드의 시작 부분에 "A" 문자에 밑줄이 표시 됩니다.
7. 문자 "A" 위에 놓고 클릭에 대 한 메서드 스텁을 생성할 수 있도록 UI는 `AddUserAndRole` 메서드. 

    ![멤버 자격 및 Advministration-메서드 스텁 생성](membership-and-administration/_static/image1.png)
8. 이라는 옵션을 클릭 합니다.  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. 열기는 *RoleActions.cs* 에서 파일의 *논리* 폴더입니다.  
   `AddUserAndRole` 메서드가 클래스 파일에 추가 되었습니다.
10. 수정 된 *RoleActions.cs* 제거 하 여 파일의 `NotImplementedeException` 다음과 같이 표시 되도록 노란색으로 강조 표시 된 코드를 추가 하 고:  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

위의 코드는 먼저 멤버 자격 데이터베이스에 대 한 데이터베이스 컨텍스트를 설정합니다. 멤버 자격 데이터베이스도도 저장 됩니다는 *.mdf* 파일에 *앱\_데이터* 폴더입니다. 첫 번째 사용자가이 웹 응용 프로그램에 로그인 되 면이 데이터베이스를 볼 수 있게 됩니다. 

> [!NOTE] 
> 
> 제품 데이터와 함께 멤버 자격 데이터를 저장 하려는 경우 사용을 고려 동일한 **DbContext** 는 위의 코드에서 제품 데이터를 저장 하는 데 사용한 합니다.


 *내부* 키워드는 형식 (예: 클래스) 및 형식 멤버 (예: 메서드 또는 속성)에 대 한 액세스 한정자입니다. 내부 형식 또는 멤버는 같은 어셈블리에 포함 된 파일 내 에서만 액세스할 수 *(.dll* 파일). 응용 프로그램에 있는 어셈블리 파일을 빌드할 때 *(.dll*) 만들어지는 응용 프로그램을 실행할 때 실행 되는 코드를 포함 하 합니다. 

A `RoleStore` 역할 관리에 제공 하는 개체는 데이터베이스 컨텍스트를 기준으로 작성 합니다.

> [!NOTE] 
> 
> 때는 `RoleStore` 개체를 만드는 제네릭 사용 하 여 `IdentityRole` 유형입니다. 즉는 `RoleStore` 포함 하는 데만 허용 `IdentityRole` 개체입니다. 또한 제네릭을 사용 하 여 메모리에 리소스는 보다 효율적으로 처리할 합니다.


다음으로 `RoleManager` 개체를 기반으로 만들어집니다는 `RoleStore` 방금 만든 개체입니다. `RoleManager` 개체 노출 역할 관련 API의 변경 내용을 자동으로 저장 하는 데 사용할 수 있는 `RoleStore`합니다. `RoleManager` 포함 하는 데만 허용 `IdentityRole` 코드 사용 하기 때문에 개체는 `<IdentityRole>` 제네릭 형식입니다.

호출 하는 `RoleExists` 메서드를 "에서 특정" 역할 멤버 자격 데이터베이스에 있는지 확인 합니다. 그렇지 않은 역할이 만들어집니다.

그러나 만들기는 `UserManager` 보다 복잡 한 것 같습니다. 개체는 `RoleManager` 제어 것은 거의 동일 합니다. 여러 버전이 아닌 한 줄에 바로 코딩 합니다. 여기에서 전달 하는 매개 변수는 괄호에 포함 된 새 개체로 인스턴스화합니다.

그런 다음 새 "canEditUser" 사용자를 만들면 `ApplicationUser` 개체입니다. 다음 사용자를 성공적으로 만든 경우에 새 역할에 사용자를 추가 합니다.

> [!NOTE] 
> 
> 이 자습서 시리즈의 뒷부분에 나오는 "ASP.NET 오류 처리" 자습서 중 오류 처리에 업데이트 됩니다.


응용 프로그램이 시작 되 면 다음에 "canEditUser" 라는 사용자 라는 응용 프로그램의 "에서" 이라는 특정 역할로 추가 됩니다. 이 자습서의 뒷부분에 나오는 추가 하는 동안이 자습서는 추가 기능을 표시 하려면 "canEditUser" 사용자로 로그인 합니다. ASP.NET Id에 대 한 API 세부 정보를 참조 하십시오.는 [Microsoft.AspNet.Identity Namespace](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)합니다. ASP.NET Id 시스템을 초기화 하는 방법에 대 한 자세한 내용은 참조는 [AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)합니다.

### <a name="restricting-access-to-the-administration-page"></a>관리 페이지에 대 한 액세스 제한

Wingtip Toys 샘플 응용 프로그램에 익명 사용자와 로그인 한 사용자를 보고 하 여 제품을 구입할 수 있습니다. 그러나 사용자 지정 "에서 특정" 역할에 로그인 한 사용자 제한 된 페이지를 추가 하 고 제품을 제거 하기 위해 액세스할 수 있습니다.

#### <a name="add-an-administration-folder-and-page"></a>페이지 및 관리 폴더 추가

다음으로, 라는 폴더가 만들어집니다 *Admin* Wingtip Toys의 사용자 지정 역할에 속하는 "canEditUser" 사용자에 대 한 샘플 응용 프로그램입니다.

1. 프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**Wingtip Toys**)에서 **솔루션 탐색기** 선택 **추가**  - &gt; **새폴더**.
2. 새 폴더 이름을 *Admin*합니다.
3. 마우스 오른쪽 단추로 클릭는 *Admin* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
4. 선택 된 <strong>Visual C#</strong> - &gt; <strong>웹</strong> 왼쪽의 템플릿 그룹입니다. 중간 목록에서 선택 <strong>마스터 페이지가 있는 웹 폼</strong>, 이름을 <em>AdminPage.aspx</em><strong>,</strong> 선택한 후 <strong>추가</strong>합니다.
5. 선택 된 *Site.Master* 마스터 페이지로 파일을 다음 선택 **확인**합니다.

#### <a name="add-a-webconfig-file"></a>Web.config 파일 추가

추가 하 여 한 *Web.config* 파일을 *Admin* 폴더를 폴더에 포함 된 페이지에 대 한 액세스를 제한할 수 있습니다.

1. 마우스 오른쪽 단추로 클릭는 *Admin* 폴더와 선택 **추가**  - &gt; **새 항목**합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. Visual C# 웹 템플릿 목록에서 선택 <strong>웹 구성 파일</strong>중간 목록에서의 기본 이름을 그대로 <em>Web.config</em><strong>,</strong> 선택한 후 <strong>추가</strong>합니다.
3. 기존 XML에 콘텐츠를 교체는 *Web.config* 다음 파일:  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

저장 된 *Web.config* 파일입니다. *Web.config* 파일 지정 응용 프로그램의 "에서 특정" 역할에 속하는 사용자에 포함 된 페이지에 액세스할 수는 *Admin* 폴더입니다.

### <a name="including-custom-role-navigation"></a>사용자 지정 역할 탐색을 포함 하 여

응용 프로그램의 관리 섹션으로 이동 하는 사용자 지정 "에서 특정" 역할의 사용자를 사용 하도록 설정 하려면 링크를 추가 해야는 *Site.Master* 페이지. "에서 특정" 역할에 속하는 사용자 수를 볼 수는 **Admin** 에 연결 하 고 관리 섹션에 액세스 합니다.

1. 솔루션 탐색기에서 찾기 및 열기는 *Site.Master* 페이지.
2. "에서 특정" 역할의 사용자에 대 한 링크를 만들려면 다음 정렬 되지 않은 목록에는 노란색으로 강조 표시 하는 태그를 추가 `<ul>` 요소가 목록으로 표시 되도록 옵니다.  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. 열기는 *Site.Master.cs* 파일입니다. 확인는 **Admin** 노란색으로 강조 표시 된 코드를 추가 하 여 "canEditUser" 사용자 에게만 표시 되는 링크는 `Page_Load` 처리기입니다. `Page_Load` 처리기는 다음과 같이 표시 됩니다.   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

페이지를 로드 하는 경우 코드는 로그인 한 사용자의 "에서"특정 역할에 있는지 여부를 확인 합니다. 사용자가 "에서 특정" 역할에 대 한 링크를 포함 하는 span 요소에 속한 경우는 *AdminPage.aspx* 페이지 (및 따라서 범위 안에 링크) 표시 되도록 설정 됩니다.

### <a name="enabling-product-administration"></a>제품 관리를 사용 하도록 설정

지금까지 "에서 특정" 역할을 만든 서 "canEditUser" 사용자, 관리 폴더 및 관리 페이지를 추가 했습니다. 관리 폴더 및 페이지에 대 한 액세스 권한을 설정 하 고 응용 프로그램에 "에서 특정" 역할의 사용자에 대 한 탐색 링크를 추가 합니다. 다음, 태그를 추가 합니다는 *AdminPage.aspx* 페이지 하 고 코드를 *AdminPage.aspx.cs* "에서 특정" 역할이 있는 사용자를 추가 하 고 제품을 제거할 수 있게 하는 코드 숨김 파일입니다.

1. **솔루션 탐색기**열고는 *AdminPage.aspx* 에서 파일을 *Admin* 폴더입니다.
2. 기존 태그를 다음 코드로 바꿉니다.  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. 을 열고는 *AdminPage.aspx.cs* 마우스 오른쪽 단추로 클릭 하 여 코드 숨김 파일에서 *AdminPage.aspx* 클릭 하 고 **코드 보기**합니다.
4. 기존 코드는 *AdminPage.aspx.cs* 를 다음 코드로 코드 숨김 파일:  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

에 대해 입력 하는 코드에서는 *AdminPage.aspx.cs* 코드 숨김 파일을 호출 하는 클래스 `AddProducts` 데이터베이스에 추가 하는 제품의 실제 작업을 수행 합니다. 이 클래스는 이제 만들는 아직 존재 하지 않습니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *논리* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **코드** 왼쪽의 템플릿 그룹입니다. 그런 다음 선택 **클래스**중간에서 나열 하 고 이름을 *AddProducts.cs*합니다.   
   새 클래스 파일이 표시 됩니다.
3. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

*AdminPage.aspx* 페이지에서는 추가 하 고 제품을 제거 하려면 "에서 특정" 역할에 속하는 사용자입니다. 새 제품 추가 되 면 제품에 대 한 세부 정보 유효성이 검사 되 고 데이터베이스에 입력 합니다. 신제품은 웹 응용 프로그램의 모든 사용자에 게 즉시 사용할 수 있습니다.

#### <a name="unobtrusive-validation"></a>비 가시적인 유효성 검사

사용자가 제공 하는 제품 세부 정보는 *AdminPage.aspx* 유효성 검사 컨트롤을 사용 하 여 페이지 유효성을 검사 (`RequiredFieldValidator` 및 `RegularExpressionValidator`). 이러한 컨트롤은 자동으로 비 가시적인 유효성 검사를 사용 합니다. 비 가시적인 유효성 검사 페이지에서 유효성을 검사 하려면 서버에 이동 하지 않아도 즉 클라이언트 쪽 유효성 검사 논리에 대 한 JavaScript를 사용 하는 유효성 검사 컨트롤 수 있습니다. 기본적으로 비 가시적인 유효성 검사에 포함 되어는 *Web.config* 다음 구성 설정에 따라 파일:

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>정규식

제품 가격은 *AdminPage.aspx* 페이지를 사용 하 여 유효성이 검사 되는 **RegularExpressionValidator** 제어 합니다. 이 컨트롤에 연결된 된 입력된 컨트롤 ("AddProductPrice" 입력란)의 값이 정규식으로 지정 된 패턴과 일치 하는지 여부를 확인 합니다. 정규식은 패턴 일치 표기법을 빠르게 찾고 특정 문자 패턴 일치를 사용 하면입니다. **RegularExpressionValidator** 컨트롤 라는 속성이 포함 되어 `ValidationExpression` 아래와 같이 가격 입력 유효성을 검사 하는 데 사용 되는 정규식을 포함 하는:

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>파일 업로드 컨트롤

입력 및 유효성 검사 컨트롤 외에도 추가 **파일 업로드** 컨트롤을 *AdminPage.aspx* 페이지. 이 컨트롤은 파일을 업로드 하는 기능을 제공 합니다. 이 경우 이미지 파일을 업로드만 허용 하는 합니다. 코드 숨김 파일에서 (*AdminPage.aspx.cs*)는 `AddProductButton` 를 클릭 하면 코드 검사는 `HasFile` 속성은 **파일 업로드** 제어 합니다. 컨트롤에 파일 및 이미지에 저장 됩니다 (파일 확장명에 따라) 파일 형식에 허용 되는 경우 하는 경우는 *이미지* 폴더 및 *이미지/엄지* 응용 프로그램의 폴더입니다.

#### <a name="model-binding"></a>모델 바인딩

이 자습서 시리즈의 앞부분에 나오는 채울 때 사용 했던 모델 바인딩은 **ListView** 컨트롤은 **FormsView** 컨트롤은 **GridView** 컨트롤 및  **DetailView** 제어 합니다. 이 자습서를 사용 하 여 모델 바인딩 채우기는 **DropDownList** 제품 범주 목록 사용 하 여 제어 합니다.

에 추가 하는 태그는 *AdminPage.aspx* 파일에 포함 되어는 **DropDownList** 이라는 컨트롤 `DropDownAddCategory`:

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

모델 바인딩을 사용 하 여이 채우는 **DropDownList** 설정 하 여는 `ItemType` 특성 및 `SelectMethod` 특성입니다. `ItemType` 특성을 사용 하는 지정 된 `WingtipToys.Models.Category` 컨트롤을 채울 때 입력 합니다. 만들어이 자습서 시리즈의 시작 부분에이 형식 정의 `Category` 클래스 (아래 참조). `Category` 클래스에는 *모델* 폴더는 *Category.cs* 파일입니다.

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

`SelectMethod` 특성의는 **DropDownList** 컨트롤을 사용 하는 지정 된 `GetCategories` 메서드 (아래 참조) 즉 코드 숨김 파일에 포함 (*AdminPage.aspx.cs*).

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

이 메서드를 지정 하는 `IQueryable` 인터페이스에 대 한 쿼리를 평가 하는 데 사용 되는 `Category` 유형입니다. 반환 된 값 채우는 데 사용 되는 **DropDownList** 페이지의 태그에 (*AdminPage.aspx*).

설정 하 여 지정 된 목록의 각 항목에 대해 표시 되는 텍스트는 `DataTextField` 특성입니다. `DataTextField` 사용 하 여 특성의 `CategoryName` 의 `Category` (위와 같이)에 있는 각 범주를 표시 하는 클래스는 **DropDownList** 제어 합니다. 항목을 선택 하는 때 전달 되는 실제 값은 **DropDownList** 컨트롤이 기준는 `DataValueField` 특성입니다. `DataValueField` 특성이로 설정 된는 `CategoryID` 를 정의 `Category` 클래스 (위에 표시 됨).

### <a name="how-the-application-will-work"></a>응용 프로그램 작동 방법

"에서 특정" 역할에 속하는 사용자가 처음으로 페이지를 탐색할 때는 `DropDownAddCategory` **DropDownList** 컨트롤이 위에서 설명한 것 처럼 채워집니다. `DropDownRemoveProduct` **DropDownList** 컨트롤이도 같은 방법을 사용 하 여 제품으로 채워집니다. 범주 유형을 선택 하 고 제품 세부 정보를 추가 하는 "에서 특정" 역할에 속하는 사용자 (**이름**, **설명**, **가격**, 및 **이미지파일**). "에서 특정" 역할에 속하는 사용자가 클릭할 때는 **제품 추가** 단추는 `AddProductButton_Click` 트리거되는 이벤트 처리기입니다. `AddProductButton_Click` 코드 숨김 파일에 있는 이벤트 처리기 (*AdminPage.aspx.cs*) 허용 된 파일 형식 일치 하는지 확인 해야 하는 데 이미지 파일을 확인 *(.gif*, *.png*, *.jpeg*, 또는 *.jpg*). 그런 다음 해당 이미지 파일: Wingtip Toys 샘플 응용 프로그램의 폴더에 저장 됩니다. 다음으로 새로운 제품 데이터베이스에 추가 됩니다. 새 제품의 새 인스턴스를 추가 수행 하는 `AddProducts` 클래스를 만들고 이름이 제품입니다. `AddProducts` 클래스 라는 메서드가 `AddProduct`, 제품 개체는 데이터베이스에 제품을 추가 하려면이 메서드를 호출 합니다.

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

페이지의 쿼리 문자열 값으로 다시 로드 되어 코드 신제품 데이터베이스에 성공적으로 추가 하는 경우 `ProductAction=add`합니다.

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

페이지가 다시 로드 하는 경우 URL에 쿼리 문자열이 포함 됩니다. 페이지를 다시 로드 하 여 "에서 특정" 역할에 속하는 사용자 즉시 확인할 수 업데이트에는 **DropDownList** 컨트롤에 *AdminPage.aspx* 페이지. 또한 url 쿼리 문자열을 포함 하 여 페이지를 표시할 수는 성공 메시지 "에서 특정" 역할에 속하는 사용자.

경우는 *AdminPage.aspx* 다시 로드를 페이지의 `Page_Load` 이벤트 라고 합니다.

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

`Page_Load` 이벤트 처리기는 쿼리 문자열 값을 확인 하 고 성공 메시지를 표시할지 여부를 결정 합니다.

## <a name="running-the-application"></a>응용 프로그램 실행

시장 바구니에 응용 프로그램을 지금 추가 하는 방법을 알아보려면, 삭제 및 업데이트 항목을 실행할 수 있습니다. 쇼핑 카트 총액 시장 바구니에 있는 모든 항목의 총 비용을 반영 합니다.

1. 솔루션 탐색기에서 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
   브라우저가 열리고 표시는 *Default.aspx* 페이지.
2. 클릭는 **로그인** 페이지 맨 아래에 링크 합니다. 

    ![링크에 대 한 멤버 자격 및 관리-로그인](membership-and-administration/_static/image2.png)

   *Login.aspx* 페이지가 표시 됩니다.
3. 다음 사용자 이름 및 암호 사용:  
   사용자 이름: canEditUser@wingtiptoys.com  
   암호: Pa $$ word1 

    ![멤버 자격 및 관리-로그인 페이지](membership-and-administration/_static/image3.png)
4. 클릭는 **로그인** 페이지의 아래쪽에 있는 단추입니다.
5. 다음 페이지 맨 위에 있는 선택 된 **관리자** 으로 이동 하는 링크는 *AdminPage.aspx* 페이지. 

    ![멤버 자격 및 관리-관리자 링크](membership-and-administration/_static/image4.png)
6. 입력된 유효성 검사를 테스트 하려면 클릭는 **제품 추가** 한 제품 세부 정보를 추가 하지 않고 단추입니다. 

    ![멤버 자격 및 관리-관리자 페이지](membership-and-administration/_static/image5.png)

   필수 필드 메시지 표시 되는지 확인 합니다.
7. 새 제품에 대 한 세부 정보를 추가 하 고 클릭는 **제품 추가** 단추입니다. 

    ![멤버 자격 및 관리-제품 추가](membership-and-administration/_static/image6.png)
8. 선택 **제품** 새 제품을 볼 수 있는 맨 위 탐색 메뉴에서 추가 했습니다. 

    ![멤버 자격 및 관리-새 제품 표시](membership-and-administration/_static/image7.png)
9. 클릭는 **Admin** 링크 관리 페이지로 돌아갑니다.
10. 에 **제품 제거** 섹션 페이지의 설명에 따라 추가한 새 제품을 선택는 **DropDownListBox**합니다.
11. 클릭는 **제품 제거** 단추는 응용 프로그램에서 새 제품을 제거 합니다. 

    ![멤버 자격 및 관리-제거 제품](membership-and-administration/_static/image8.png)
12. 선택 **제품** 제품 제거 된 것을 확인 하려면 위쪽 탐색 메뉴에서 합니다.
13. 클릭 **로그 오프** 관리 모드에 있어야 합니다.   
    위쪽 탐색 창에 더 이상 표시에 **Admin** 메뉴 항목입니다.

## <a name="summary"></a>요약

이 자습서에서는 사용자 지정 역할 및 사용자 지정 역할을 관리 폴더 및 페이지에 대 한 제한 된 액세스에 속한 사용자를 추가 하 고 사용자 지정 역할에 속하는 사용자에 대 한 탐색을 제공 합니다. 모델 바인딩 채우는 데 사용 된 **DropDownList** 컨트롤에 데이터입니다. 구현 하는 **파일 업로드** 제어 및 유효성 검사 컨트롤입니다. 또한, 추가 하 고 데이터베이스에서 제품을 제거 하는 방법을 배웠습니다. 다음 자습서에서는 ASP.NET 라우팅을 구현 하는 방법을 설명 합니다.

## <a name="additional-resources"></a>추가 자료

[Web.config-권한 부여 요소](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET Id](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[Azure 웹 사이트에 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET Web Forms 응용 프로그램 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [이전](checkout-and-payment-with-paypal.md)
> [다음](url-routing.md)
