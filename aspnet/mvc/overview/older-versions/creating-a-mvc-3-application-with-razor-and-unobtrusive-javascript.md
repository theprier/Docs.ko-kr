---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 만들기는 MVC 3 Application with Razor and Unobtrusive JavaScript | Microsoft Docs
author: microsoft
description: 사용자 목록 샘플 웹 응용 프로그램에서는 Razor 보기 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 얼마나 간단한 지 보여 줍니다. 샘플 응용 프로그램 s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: f60ca3e76fda8a18da1ad83e955e5e4759f5e3af
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829856"
---
<a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>만들기는 MVC 3 Razor 및 비간섭 JavaScript를 사용 하 여 응용 프로그램
====================
[Microsoft](https://github.com/microsoft)

> 사용자 목록 샘플 웹 응용 프로그램에서는 Razor 보기 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 얼마나 간단한 지 보여 줍니다. 샘플 응용 프로그램 작성, 표시, 편집 및 삭제 사용자 등의 기능을 포함 하는 가상의 사용자 목록 웹 사이트를 만드는 ASP.NET MVC 버전 3 사용 하 여 새로운 Razor 보기 엔진 및 Visual Studio 2010을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서에는 사용자 목록 샘플 ASP.NET MVC 3 응용 프로그램을 빌드하기 위해 수행 된 단계를 설명 합니다. C# 및 VB 소스 코드를 사용 하 여 Visual Studio 프로젝트는 다음이 항목과 함께 사용할 수 있습니다: [다운로드](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)합니다. 이 자습서에 대 한 질문이 있으면 게시 하세요 하는 [MVC 포럼](https://forums.asp.net/1146.aspx)합니다.


## <a name="overview"></a>개요

응용 프로그램 작성 하는 간단한 사용자 목록 웹 사이트입니다. 사용자 입력, 보기 및 사용자 정보를 업데이트할 수 있습니다.

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

완료 된 VB와 C# 프로젝트를 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)합니다.

## <a name="creating-the-web-application"></a>웹 응용 프로그램 만들기

자습서를 시작 하려면 Visual Studio 2010 열고 사용 하 여 새 프로젝트를 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿. 응용 프로그램의 이름을 &quot;Mvc3Razor&quot;합니다.

[![새 MVC 3 프로젝트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**Razor 보기 엔진을 선택한 다음 클릭 **확인**합니다.

![새 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

이 자습서에서는 하지 사용할 ASP.NET 멤버 자격 공급자에서 로그온 및 멤버 자격을 사용 하 여 연결 된 모든 파일을 삭제할 수 있도록 합니다. **솔루션 탐색기**, 다음 파일 및 디렉터리를 제거 합니다.

- *Controllers\AccountController*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* (및이 디렉터리의 모든 파일)

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

편집를  <em>\_Layout.cshtml</em> 내에서 태그를 바꾸고 파일을 `<div>` 라는 요소가 `logindisplay` 메시지와 함께 <em>&quot;</em>로그인 사용 안 함&quot;. 다음 예제에서는 새 태그를 보여 줍니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>모델 추가

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 클릭 하 고 **클래스**.

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

클래스 이름을 `UserModel`로 지정합니다. 내용을 대체 합니다 *UserModel* 를 다음 코드로 파일:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel` 클래스는 사용자를 나타냅니다. 으로 주석이 달린 클래스의 각 멤버는 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 에서 특성을 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스입니다. 특성을 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스 웹 응용 프로그램에 대 한 자동 클라이언트 및 서버 쪽 유효성 검사를 제공 합니다.

열기는 `HomeController` 클래스 및 추가 `using` 지시문에 액세스할 수 있도록 합니다 `UserModel` 및 `Users` 클래스:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

바로 뒤의 `HomeController` 선언 다음 주석 및에 대 한 참조 추가 `Users` 클래스:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users` 클래스는이 자습서에서 사용 하는 간단한 메모리 내 데이터 저장소입니다. 실제 응용 프로그램에서 데이터베이스를 사용 하면 사용자 정보 저장 됩니다. 처음 몇 줄의 `HomeController` 파일은 다음 예제에 나와 있습니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

사용자 모델을 스 캐 폴딩 마법사는 다음 단계에서 사용할 수 있도록 응용 프로그램을 작성 합니다.

## <a name="creating-the-default-view"></a>기본 뷰 만들기

다음 단계는 작업 메서드 및 사용자를 표시 하려면 보기를 추가 하는 것입니다.

기존 삭제할 *Views\Home\Index* 파일입니다. 새로 만든 *인덱스* 사용자를 표시 하는 파일입니다.

에 `HomeController` 클래스의 내용을 대체 합니다 `Index` 메서드를 다음 코드로:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

마우스 오른쪽 단추로 클릭 합니다 `Index` 메서드와 클릭 **뷰 추가**합니다.

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

선택 된 **강력한 형식의 뷰를 만들** 옵션입니다. 에 대 한 **데이터 클래스를 보려면**를 선택 **Mvc3Razor.Models.UserModel**합니다. (표시 되지 않는 경우 **Mvc3Razor.Models.UserModel** 에 **데이터 클래스 보기** 프로젝트를 빌드할 필요가 상자입니다.) 뷰 엔진 설정 되어 있는지 확인 하십시오 **Razor**합니다. 설정 **콘텐츠를 볼** 하 **목록** 을 클릭 한 다음 **추가**합니다.

![인덱스 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

새 보기에 전달 되는 사용자 데이터를 자동으로 스 캐 폴딩 합니다 `Index` 보기. 새로 생성 된 검사할 *Views\Home\Index* 파일입니다. 합니다 **새로 만들기**를 **편집**를 **세부 정보**, 및 **삭제** 링크가 작동 하지 않습니다 하지만 페이지의 나머지 부분은 기능입니다. 페이지를 실행 합니다. 사용자의 목록이 표시 됩니다.

![인덱스 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

열기는 *Index.cshtml* 바꾸고 파일을 `ActionLink` 에 대 한 태그 **편집**를 **세부 정보**, 및 **삭제** 다음 코드를 사용 하 여 :

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

사용자 이름에서 선택한 레코드를 찾는 데 ID로 사용 됩니다 합니다 **편집할**, **세부 정보**, 및 **삭제** 링크.

## <a name="creating-the-details-view"></a>자세히 보기 만들기

다음 단계를 추가 하는 것을 `Details` 작업 메서드 및 사용자 세부 정보를 표시 하기 위해 보기.

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

다음 추가 `Details` 메서드를 home 컨트롤러:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

마우스 오른쪽 단추로 클릭 합니다 `Details` 한 다음 선택한 메서드 <strong>뷰 추가</strong>합니다. 있는지 확인 합니다 <strong>데이터 클래스를 보려면</strong> 상자에 <strong>Mvc3Razor.Models.UserModel</strong><em>합니다.</em> 설정 <strong>콘텐츠를 볼</strong> 하 <strong>세부 정보</strong> 을 클릭 한 다음 <strong>추가</strong>합니다.

![세부 정보 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

응용 프로그램을 실행 하 고 세부 정보 링크를 선택 합니다. 자동 스 캐 폴딩을 모델의 각 속성을 보여 줍니다.

![설명](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>편집 보기 만들기

다음 추가 `Edit` 메서드를 home 컨트롤러.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

이전 단계와 같이 뷰를 추가 하지만 설정 **콘텐츠 보기** 하 **편집**합니다.

![편집 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

응용 프로그램을 실행 하 고 사용자 중의 첫 번째 및 마지막 이름을 편집 합니다. 하나라도 위반 하면 `DataAnnotation` 에 적용 된 제약 조건은 `UserModel` 클래스 폼을 제출할 때 표시 됩니다 서버 코드에서 생성 되는 유효성 검사 오류입니다. 예를 들어, 첫 번째 이름을 변경한 경우 &quot;Ann&quot; 하 &quot;는&quot;폼을 제출 하는 경우 폼에 다음 오류가 표시 됩니다.

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

이 자습서에서는 기본 키로 사용자 이름을 처리 하는 있습니다. 따라서 사용자 이름 속성을 변경할 수 없습니다. 에 *Edit.cshtml* 파일을 바로 뒤를 `Html.BeginForm` 문에 숨겨진 필드를 사용자 이름을 설정 합니다. 이렇게 하면 모델에 전달할 속성입니다. 다음 코드 조각 표시의 배치를 `Hidden` 문:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

대체는 `TextBoxFor` 하 고 `ValidationMessageFor` 사용 하 여 사용자 이름에 대 한 태그를 `DisplayFor` 호출 합니다. `DisplayFor` 메서드는 읽기 전용 요소와 속성을 표시 합니다. 다음 예제에서는 전체 태그를 보여 줍니다. 원래 `TextBoxFor` 하 고 `ValidationMessageFor` Razor 주석 시작 및 끝 주석 문자로 호출 머릿말 (`@* *@`)

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>클라이언트 쪽 유효성 검사를 사용 하도록 설정

ASP.NET MVC 3의 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 두 플래그를 설정 해야 하 고 세 개의 JavaScript 파일을 포함 해야 합니다.

응용 프로그램을 엽니다 *Web.config* 파일입니다. 확인 `that ClientValidationEnabled` 및 `UnobtrusiveJavaScriptEnabled` 로 설정 된 응용 프로그램 설정에 true입니다. 루트에서 다음 조각은 *Web.config* 파일에 올바른 설정을 보여 줍니다.

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

설정 `UnobtrusiveJavaScriptEnabled` 비간섭 Ajax를 사용 하도록 설정 하 고 비 가시적인 클라이언트 유효성 검사를 true로 합니다. 비간섭 유효성 검사를 사용 하면 유효성 검사 규칙은 HTML5 특성으로 되어 있습니다. HTML5 특성 이름은 소문자, 숫자 및 대시 구성할 수 있습니다.

설정 `ClientValidationEnabled` true로 설정 하면 클라이언트 쪽 유효성 검사 합니다. 응용 프로그램에서 이러한 키를 설정 하 여 *Web.config* 파일인 클라이언트 유효성 검사 및 전체 응용 프로그램에 대 한 비간섭 JavaScript를 사용 합니다. 사용 하도록 설정 하거나 개별 뷰 또는 컨트롤러 메서드에서 다음 코드를 사용 하 여 이러한 설정을 사용 하지 않도록 설정할 수도 있습니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

렌더링된 된 보기에서 여러 개의 JavaScript 파일을 포함 해야 합니다. 모든 보기에서 JavaScript를 포함 하는 쉬운 방법을 추가 하는 것은 *Views\Shared\\_Layout.cshtml* 파일입니다. 대체는 `<head>` 의 요소를  *\_Layout.cshtml* 를 다음 코드로 파일:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

처음 두 jQuery 스크립트에서 Microsoft Ajax 콘텐츠 배달 네트워크 (CDN)에 호스트 됩니다. Microsoft Ajax CDN을 활용 하 여 응용 프로그램의 첫 번째 적중 성능을 크게 개선할 수 있습니다.

응용 프로그램을 실행 하 고 편집 링크를 클릭 합니다. 브라우저에서 페이지의 소스를 봅니다. 브라우저 소스를 폼의 많은 특성을 보여 줍니다. `data-val` (데이터 유효성 검사를 위해). 클라이언트 유효성 검사 규칙을 사용 하 여 입력된 필드를 포함 하는 클라이언트 유효성 검사 및 비간섭 JavaScript를 사용 하는 경우는 `data-val="true"` 비 가시적인 클라이언트 유효성 검사 트리거 특성입니다. 예를 들어 합니다 `City` 모델의 필드에에서 지정 된 합니다 [필요한](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 는 다음 예제와 같이 HTML 특성:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

폼에 있는 특성은 추가 하는 각 클라이언트 유효성 검사 규칙에 대해 `data-val-rulename="message"`합니다. 사용 하 여는 `City` 필드 이전 예제에 필요한 클라이언트 유효성 검사 규칙을 생성 합니다 `data-val-required` 특성 및 메시지 &quot;The City 필드는 필수&quot;합니다. 응용 프로그램을 실행, 사용자 중 하나를 편집 및 선택 취소 된 `City` 필드입니다. 필드에서 tab 키를 누르면, 클라이언트 쪽 유효성 검사 오류 메시지를 참조 하세요.

![필요한 도시](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

마찬가지로, 클라이언트 유효성 검사 규칙의 각 매개 변수에 특성이 추가 되는 형식은 `data-val-rulename-paramname=paramvalue`합니다. 예를 들어, 합니다 `FirstName` 속성으로 주석이 달린 합니다 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성 및 3의 최소 길이 및 최대 길이는 8 지정 합니다. 명명 된 데이터 유효성 검사 규칙 `length` 매개 변수 이름이 `max` 및 매개 변수 값은 8입니다. 다음에 대해 생성 된 HTML 표시를 `FirstName` 사용자 중 하나를 편집 하는 경우 필드:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

비 가시적인 클라이언트 유효성 검사에 대 한 자세한 내용은 항목을 참조 하세요 [ASP.NET MVC 3의 비간섭 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) Brad Wilson의 블로그에서입니다.

> [!NOTE]
> ASP.NET MVC 3 베타의 경우에 따라 클라이언트 쪽 유효성 검사를 시작 하려면 양식을 제출 해야 합니다. 이 최종 릴리스에서 변경 될 수 있습니다.


## <a name="creating-the-create-view"></a>만들기 뷰 만들기

다음 단계를 추가 하는 것을 `Create` 작업 메서드 및 사용자가 새 사용자를 만들 수 있도록 하려면 보기. 다음 추가 `Create` 메서드를 home 컨트롤러:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

이전 단계와 같이 뷰를 추가 하지만 설정 **콘텐츠 보기** 하 **만들기**합니다.

![뷰 만들기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

응용 프로그램 실행을 선택 합니다 **만들기** 링크를 선택한 새 사용자를 추가 합니다. `Create` 메서드 활용 클라이언트측 및 서버측 유효성 검사를 자동으로 수행 합니다. 와 같은 공백을 포함 하는 사용자 이름을 입력 해 보세요 &quot;Ben X&quot;합니다. 사용자 이름 필드에 클라이언트 쪽 유효성 검사 오류를 탭 하는 경우 (`White space is not allowed`) 표시 됩니다.

## <a name="add-the-delete-method"></a>Delete 메서드를 추가 합니다.

이 자습서를 완료 하려면 다음 추가 `Delete` 메서드를 home 컨트롤러:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

추가 `Delete` 뷰 설정, 이전 단계와 같이 **콘텐츠를 보려면** 하 **삭제**.

![뷰 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

이제 유효성 검사를 사용 하 여 ASP.NET MVC 3 application 간단 하지만 완벽 하 게 작동 해야합니다.
