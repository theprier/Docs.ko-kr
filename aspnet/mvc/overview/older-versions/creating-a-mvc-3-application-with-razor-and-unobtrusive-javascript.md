---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 만드는 MVC 3 Application with Razor and Unobtrusive JavaScript | Microsoft Docs
author: microsoft
description: 사용자 목록 예제 웹 응용 프로그램 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다. 샘플 응용 프로그램 s 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/01/2010
ms.topic: article
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: 9b273f6827cad2078b581d6da7b127198dfddaa5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "30874696"
---
<a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>만드는 MVC 3 Application with Razor and Unobtrusive JavaScript
====================
by [Microsoft](https://github.com/microsoft)

> 사용자 목록 예제 웹 응용 프로그램 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다. 샘플 응용 프로그램 만들기, 표시, 편집 및 삭제 하는 중 사용자가 같은 기능을 포함 하는 가상의 사용자 목록 웹 사이트를 만드는 ASP.NET MVC 버전 3와 새로운 Razor 뷰 엔진 및 Visual Studio 2010을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서에서는 사용자 목록 샘플 ASP.NET MVC 3 응용 프로그램을 작성 하기 위해 수행 된 단계를 설명 합니다. C# 및 VB 소스 코드를 Visual Studio 프로젝트는이 항목에 수반: [다운로드](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)합니다. 이 자습서에 대 한 질문이 있으면 하십시오에 게시 하는 [MVC 포럼](https://forums.asp.net/1146.aspx)합니다.


## <a name="overview"></a>개요

에서는 빌드할 응용 프로그램은 간단한 사용자 목록 웹사이트입니다. 사용자가 입력, 보기 및 사용자 정보를 업데이트할 수 있습니다.

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

완료 된 VB 및 C# 프로젝트를 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)합니다.

## <a name="creating-the-web-application"></a>웹 응용 프로그램 만들기

이 자습서를 시작 하려면 Visual Studio 2010 열고 사용 하 여 새 프로젝트를 만들는 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿. 응용 프로그램의 이름을 &quot;Mvc3Razor&quot;합니다.

[![새 MVC 3 프로젝트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**Razor 뷰 엔진을 선택한 다음 클릭 **확인**합니다.

![새 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

이 자습서에서는 있습니다를 사용 하지 않는 ASP.NET 멤버 자격 공급자 로그온 및 멤버와 관련 된 모든 파일을 삭제할 수 있도록 합니다. **솔루션 탐색기**, 다음과 같은 파일 및 디렉터리를 제거 합니다.

- *Controllers\AccountController*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* (및이 디렉터리에 있는 모든 파일)

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

편집 된  <em>\_Layout.cshtml</em> 내부의 태그를 바꾸고 파일는 `<div>` 라는 요소 `logindisplay` 메시지와 함께 <em>&quot;</em>로그인 비활성화&quot;. 다음 예제에서는 새 태그를 보여 줍니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>모델 추가

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**, 클릭 하 고 **클래스**합니다.

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

클래스 이름을 `UserModel`로 지정합니다. 내용을 대체는 *UserModel* 를 다음 코드로 파일:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel` 클래스는 사용자가 나타냅니다. 클래스의 각 멤버는 주석을 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 에서 특성의 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스입니다. 에 있는 특성의 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스 웹 응용 프로그램에 대 한 자동 클라이언트 및 서버 쪽 유효성 검사를 제공 합니다.

열기는 `HomeController` 클래스 및 추가 `using` 액세스할 수 있도록 지시문은 `UserModel` 및 `Users` 클래스:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

바로 뒤의 `HomeController` 선언 다음 주석 및에 대 한 참조 추가 `Users` 클래스:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users` 클래스는이 자습서에서 사용 하는 간소화 된 메모리 내 데이터 저장소입니다. 실제 응용 프로그램에서 사용자 정보를 저장 하는 데이터베이스를 사용 합니다. 처음 몇 줄의 `HomeController` 파일은 다음 예제에 표시 됩니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

사용자 모델 스 캐 폴딩 마법사는 다음 단계에서 사용할 수 있도록 응용 프로그램을 작성 합니다.

## <a name="creating-the-default-view"></a>기본 보기를 만드는 방법

다음 단계는 작업 메서드 및 사용자가 표시 하려면 보기를 추가 하는 것입니다.

기존 삭제 *Views\Home\Index* 파일입니다. 새 만들려는 *인덱스* 파일을 사용자가 표시 됩니다.

에 `HomeController` 클래스의 내용을 대체는 `Index` 메서드를 다음 코드로:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

마우스 오른쪽 단추로 클릭는 `Index` 메서드와 클릭 **뷰 추가**합니다.

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

선택 된 **강력한 형식의 뷰 만들기** 옵션입니다. 에 대 한 **데이터 클래스 보기**선택, **Mvc3Razor.Models.UserModel**합니다. (표시 되지 않으면 **Mvc3Razor.Models.UserModel** 에 **데이터 클래스 보기** 프로젝트를 빌드하는 데 필요한 상자입니다.) 뷰 엔진 설정 되어 있는지 확인 **Razor**합니다. 설정 **콘텐츠를 볼** 를 **목록** 클릭 하 고 **추가**합니다.

![인덱스 뷰를 추가 합니다.](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

새 보기에 전달 되는 사용자 데이터를 자동으로 scaffolds는 `Index` 보기. 새로 생성 된 검사 *Views\Home\Index* 파일입니다. **새로 만들기**, **편집**, **세부 정보**, 및 **삭제** 나머지 페이지는 작동 하지만 링크가 작동 하지 않습니다. 페이지를 실행 합니다. 사용자의 목록을 표시 합니다.

![인덱스 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

열기는 *Index.cshtml* 파일 및 바꾸기는 `ActionLink` 에 대 한 태그 **편집**, **세부 정보**, 및 **삭제** 를 다음 코드로 :

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

사용자 이름에서 선택한 레코드를 찾는 데 ID로 사용 됩니다는 **편집**, **세부 정보**, 및 **삭제** 링크 합니다.

## <a name="creating-the-details-view"></a>세부 정보 보기를 만드는 방법

다음 단계를 추가 하는 것을 `Details` 동작 메서드 및 사용자 세부 정보를 표시 하기 위해 보기.

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

다음 추가 `Details` 메서드를 home 컨트롤러:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

마우스 오른쪽 단추로 클릭는 `Details` 메서드와 선택 <strong>뷰 추가</strong>합니다. 되어 있는지 확인은 <strong>데이터 클래스 보기</strong> 상자에 <strong>Mvc3Razor.Models.UserModel</strong><em>합니다.</em> 설정 <strong>콘텐츠를 볼</strong> 를 <strong>세부 정보</strong> 클릭 하 고 <strong>추가</strong>합니다.

![추가 세부 정보 보기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

응용 프로그램을 실행 하 고 세부 정보 링크를 선택 합니다. 자동 스 캐 폴딩 모델의 각 속성을 보여 줍니다.

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>편집 뷰 만들기

다음 추가 `Edit` 메서드를 home 컨트롤러입니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

이전 단계에서와 같이 뷰를 추가 하지만 설정 **콘텐츠를 볼** 를 **편집**합니다.

![편집 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

응용 프로그램을 실행 하 고 사용자가 중 하나의 이름과 성을 편집 합니다. 위반 하면 `DataAnnotation` 에 적용 된 제약 조건에서 `UserModel` 클래스에서는 양식을 제출 하기 보게 서버 코드에서 생성 되는 유효성 검사 오류입니다. 예를 들어, 첫 번째 이름을 변경 하면 &quot;Ann&quot; 를 &quot;A&quot;양식을 전송할 때, 폼에 다음 오류가 표시 됩니다.

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

이 자습서에서는 기본 키로 사용자 이름을 처리 하는 합니다. 따라서 사용자 이름 속성을 변경할 수 없습니다. 에 *Edit.cshtml* 파일, 바로 뒤의 `Html.BeginForm` 문, 숨겨진 필드를 사용자 이름을 설정 합니다. 이렇게 하면 속성을 모델에 전달할 수 있습니다. 다음 코드 조각 표시의 배치는 `Hidden` 문:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

대체는 `TextBoxFor` 및 `ValidationMessageFor` 와 사용자 이름에 대 한 태그는 `DisplayFor` 호출 합니다. `DisplayFor` 메서드는 읽기 전용 요소도 속성을 표시 합니다. 다음 예제에서는 완성 된 태그를 보여 줍니다. 원래 `TextBoxFor` 및 `ValidationMessageFor` 호출 주석으로 처리 되어 Razor 주석 시작 및 끝 주석 문자 (`@* *@`)

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>클라이언트 쪽 유효성 검사를 사용 하도록 설정

ASP.NET MVC 3의 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 두 플래그를 설정 해야 하 고 3 개의 JavaScript 파일을 포함 해야 합니다.

응용 프로그램의 열고 *Web.config* 파일입니다. 확인 `that ClientValidationEnabled` 및 `UnobtrusiveJavaScriptEnabled` 로 설정 된 응용 프로그램 설정에 true입니다. 조각 루트에서 *Web.config* 파일의 올바른 설정을 보여 줍니다.

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

설정 `UnobtrusiveJavaScriptEnabled` true를 사용 하면 비 가시적인 Ajax 및 비 가시적인 클라이언트 유효성 검사를 합니다. 비 가시적인 유효성 검사를 사용 하면 유효성 검사 규칙은 HTML5 특성으로 되어 있습니다. HTML5 특성 이름은 소문자, 숫자 및 대시만 구성할 수 있습니다.

설정 `ClientValidationEnabled` true 이면 클라이언트 쪽 유효성 검사를 합니다. 응용 프로그램에서 이러한 키를 설정 하 여 *Web.config* 파일, 클라이언트 유효성 검사 및 전체 응용 프로그램에 대 한 비 가시적인 JavaScript를 사용 합니다. 또한 다음 코드를 사용 하 여 컨트롤러 메서드 또는 개별 보기에서 이러한 설정을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

렌더링 된 보기에 여러 개의 JavaScript 파일을 포함 해야 합니다. 모든 보기에는 JavaScript를 포함 하는 쉬운 방법을를 추가 하는 것은 *Views\Shared\\_Layout.cshtml* 파일입니다. 대체는 `<head>` 의 요소는  *\_Layout.cshtml* 를 다음 코드로 파일:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

처음 두 jQuery 스크립트에서의 Microsoft Ajax CDN 콘텐츠 배달 네트워크 ()에 호스트 됩니다. Microsoft Ajax CDN을 활용 하 여 응용 프로그램의 최초로 성능을 크게 개선할 수 있습니다.

응용 프로그램을 실행 하 고 편집 링크를 클릭 합니다. 브라우저에서 페이지의 소스를 검토 합니다. 폼의 많은 특성을 표시 하는 브라우저 소스 `data-val` (에 대해 데이터 유효성 검사). 클라이언트 유효성 검사 규칙으로 입력된 필드를 포함 하는 클라이언트 유효성 검사 및 비간섭 JavaScript를 사용 하는 경우는 `data-val="true"` 비 가시적인 클라이언트 유효성 검사 트리거 특성입니다. 예를 들어는 `City` 모델의 필드로 데코레이팅 되었습니다는 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 그 결과 다음 예제에 표시 된 HTML 특성:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

각 클라이언트 유효성 검사 규칙에 대 한 특성이 있는 폼 추가 된 `data-val-rulename="message"`합니다. 사용 하는 `City` 필드 이전 예제를 필요한 클라이언트 유효성 검사 규칙 생성는 `data-val-required` 특성 및 메시지 &quot;The City 필드는 필수&quot;합니다. 응용 프로그램을 실행, 하나는 사용자를 편집 및 선택 취소 된 `City` 필드입니다. 필드에서 이동 하는 경우 클라이언트 쪽 유효성 검사 오류 메시지가 표시 됩니다.

![필요 시](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

마찬가지로, 클라이언트 유효성 검사 규칙의 각 매개 변수에 대해 특성이 추가 되는 형식을 포함 하는 `data-val-rulename-paramname=paramvalue`합니다. 예를 들어는 `FirstName` 속성으로 추적이 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성 및 3의 최소 길이 및 최대 길이가 8 지정 합니다. 명명 된 데이터 유효성 검사 규칙 `length` 매개 변수 이름이 `max` 및 매개 변수 값은 8입니다. 다음 테이블에 대해 생성 되는 HTML 나와 `FirstName` 사용자 중 하나를 편집 하는 경우 필드:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

비 가시적인 클라이언트 유효성 검사에 대 한 자세한 내용은 항목을 참조 하십시오. [ASP.NET MVC 3에서 비간섭 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) Brad Wilson의 블로그에서 합니다.

> [!NOTE]
> ASP.NET MVC 3 베타 버전에서는 클라이언트 쪽 유효성 검사를 시작 하기 위해 폼을 제출 해야 하는 경우도 있습니다. 이 최종 릴리스에 대 한 변경할 수 있습니다.


## <a name="creating-the-create-view"></a>만들기 뷰 만들기

다음 단계를 추가 하는 것을 `Create` 동작 메서드 및 사용자를 새 사용자를 만들 수 있도록 하려면 보기. 다음 추가 `Create` 메서드를 home 컨트롤러:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

이전 단계에서와 같이 뷰를 추가 하지만 설정 **콘텐츠를 볼** 를 **만들기**합니다.

![뷰 만들기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

응용 프로그램을 실행, 선택는 **만들기** 링크를 선택한 새 사용자를 추가 합니다. `Create` 메서드 자동으로에서는 클라이언트 쪽 및 서버측 유효성 검사 활용 합니다. 와 같은 경우를 포함 하는 사용자 이름을 입력 하려고 &quot;Ben X&quot;합니다. 클라이언트 쪽 유효성 검사 오류를 사용자 이름 필드에서 이동 하는 경우 (`White space is not allowed`) 표시 됩니다.

## <a name="add-the-delete-method"></a>Delete 메서드를 추가 합니다.

이 자습서를 수행 하려면 다음 추가 `Delete` 메서드를 home 컨트롤러:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

추가 `Delete` 설정 하 고 이전 단계에서와 같이 보기 **콘텐츠를 볼** 를 **삭제**합니다.

![뷰 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

유효성 검사는 간단 하지만 모든 기능을 갖춘 ASP.NET MVC 3 응용 프로그램을 해야 합니다.
